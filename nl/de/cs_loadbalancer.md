---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}



# Apps mit Lastausgleichsfunktionen zugänglich machen
{: #loadbalancer}

Machen Sie einen Port zugänglich und verwenden Sie eine portierbare IP-Adresse für die Layer 4-Lastausgleichsfunktion, um auf eine containerisierte App zuzugreifen.
{:shortdesc}



## Komponenten und Architektur der Lastausgleichsfunktion
{: #planning}

Wenn Sie einen Standardcluster erstellen, stellt {{site.data.keyword.containerlong_notm}} automatisch ein portierbares öffentliches Teilnetz und ein portierbares privates Teilnetz bereit.

* Das portierbare öffentliche Teilnetz stellt eine portierbare öffentliche IP-Adresse bereit, die von der [öffentlichen Ingress-Standard-ALB](cs_ingress.html) verwendet wird. Die restlichen vier portierbaren öffentlichen IP-Adressen können verwendet werden, um einzelne Apps dem Internet zugänglich zu machen, indem ein öffentlicher Service für die Lastausgleichsfunktion erstellt wird.
* Das portierbare öffentliche Teilnetz stellt eine portierbare private IP-Adresse bereit, die von der [privaten Ingress-Standard-ALB](cs_ingress.html#private_ingress) verwendet wird. Die restlichen vier portierbaren privaten IP-Adressen können verwendet werden, um einzelne Apps einem privaten Netz zugänglich zu machen, indem ein privater Service für die Lastausgleichsfunktion erstellt wird.

Portierbare öffentliche und private IP-Adressen sind statisch und ändern sich nicht, wenn ein Workerknoten entfernt wird. Wenn der Workerknoten, auf dem sich die IP-Adresse der Lastausgleichsfunktion befindet, entfernt wird, wird die IP-Adresse von einem Keepalive-Dämon, der die IP kontinuierlich überwacht, automatisch in einen anderen Workerknoten verschoben. Sie können Ihrer Lastausgleichsfunktion jeden beliebigen Port zuweisen und sind dabei nicht an einen bestimmten Portnummernbereich gebunden.

Ein Service für die Lastausgleichsfunktion macht die App auch über die NodePort-Instanzen des Service verfügbar. Auf [Knotenports (NodePorts)](cs_nodeport.html) kann über jede öffentliche und private IP-Adresse für jeden Knoten innerhalb des Clusters zugegriffen werden. Informationen zum Blockieren des Datenverkehrs an Knotenports während der Verwendung eines Service für die Lastausgleichsfunktion finden Sie im Abschnitt [Eingehenden Datenverkehr an Service für die Lastausgleichsfunktion oder NodePort-Service steuern](cs_network_policy.html#block_ingress).

Der Service für die Lastausgleichsfunktion fungiert als externer Einstiegspunkt für eingehende Anforderungen an die App. Wenn Sie vom Internet aus auf den Service für die Lastausgleichsfunktion zugreifen möchten, können Sie die öffentliche IP-Adresse der Lastausgleichsfunktion in Verbindung mit der zugewiesenen Portnummer im Format `<IP_address>:<port>` verwenden. Das folgende Diagramm veranschaulicht, wie eine Lastausgleichsfunktion die Kommunikation vom Internet an eine App leitet.

<img src="images/cs_loadbalancer_planning.png" width="550" alt="App in {{site.data.keyword.containerlong_notm}} mithilfe einer Lastausgleichsfunktion zugänglich machen" style="width:550px; border-style: none"/>

1. Eine Anforderung an Ihre App verwendet die öffentliche IP-Adresse der Lastausgleichsfunktion und den zugeordneten Port auf dem Workerknoten.

2. Die Anforderung wird automatisch an die interne Cluster-IP-Adresse und den internen Port des Service für die Lastausgleichsfunktion weitergeleitet. Auf die interne Cluster-IP-Adresse kann nur aus dem Cluster selbst heraus zugegriffen werden.

3. `kube-proxy` leitet die Anforderung an den Kubernetes-Service für die Lastausgleichsfunktion für die App weiter.

4. Die Anforderung wird an die private IP-Adresse des App-Pods weitergeleitet. Die Quellen-IP-Adresse des Anforderungspakets wird in die öffentliche IP-Adresse des Workerknotens geändert, auf dem der App-Pod ausgeführt wird. Wenn mehrere App-Instanzen im Cluster bereitgestellt werden, leitet die Lastausgleichsfunktion die Anforderungen zwischen den App-Pods weiter.

**Mehrzonencluster**:

Wenn Sie über einen Mehrzonencluster verfügen, werden App-Instanzen in Pods auf Workern in den verschiedenen Zonen bereitgestellt. Das folgende Diagramm veranschaulicht, wie eine klassische Lastausgleichsfunktion die Kommunikation vom Internet an eine App in einem Mehrzonencluster leitet.

<img src="images/cs_loadbalancer_planning_multizone.png" width="500" alt="Verwendung des Service für Lastausgleichsfunktion für den Lastausgleich von Apps in Mehrzonencluster" style="width:500px; border-style: none"/>

Standardmäßig wird jede Lastausgleichsfunktion nur in einer Zone eingerichtet. Um eine hohe Verfügbarkeit zu erreichen, müssen Sie eine Lastausgleichsfunktion in jeder Zone bereitstellen, in der sich App-Instanzen befinden. Anforderungen werden von den Lastausgleichsfunktionen in verschiedenen Zonen in einem Umlaufzyklus bearbeitet. Darüber hinaus leitet jede Lastausgleichsfunktion Anforderungen an die App-Instanzen in ihrer eigenen Zone und an App-Instanzen in anderen Zonen weiter.

<br />


## Öffentlichen oder privaten Zugriff auf eine App in einem Mehrzonencluster aktivieren
{: #multi_zone_config}

Hinweis:
  * Dieses Feature ist nur für Standardcluster verfügbar.
  * Von den Services für die Lastausgleichsfunktion wird die TLS-Terminierung nicht unterstützt. Wenn für Ihre App eine TLS-Terminierung erforderlich ist, können Sie die App mithilfe von [Ingress](cs_ingress.html) bereitstellen oder für die Verwaltung der TLS-Terminierung konfigurieren.

Vorbemerkungen:
  * Ein Service für die Lastausgleichsfunktion mit einer portierbaren privaten IP-Adresse verfügt weiterhin auf jedem Workerknoten über einen offenen öffentlichen Knotenport. Informationen zum Hinzufügen einer Netzrichtlinie zur Verhinderung von öffentlichem Datenverkehr finden Sie unter dem Thema [Eingehenden Datenverkehr blockieren](cs_network_policy.html#block_ingress).
  * Sie müssen in jeder Zone eine Lastausgleichsfunktion bereitstellen und jeder Lastausgleichsfunktion wird in dieser Zone eine eigene IP-Adresse zugewiesen. Um öffentliche Lastausgleichsfunktionen zu erstellen, muss mindestens ein öffentliches VLAN portierbare Teilnetze aufweisen, die in jeder Zone verfügbar sind. Um private Lastausgleichsfunktionsservices hinzufügen zu können, muss mindestens ein privates VLAN portierbare Teilnetze aufweisen, die in jeder Zone verfügbar sind. Informationen zum Hinzufügen von Teilnetzen finden Sie im Abschnitt [Teilnetze für Cluster konfigurieren](cs_subnets.html).
  * Wenn Sie den Datenaustausch im Netz auf Edge-Workerknoten beschränken, müssen Sie sicherstellen, dass in jeder Zone mindestens zwei [Edge-Workerknoten](cs_edge.html#edge) aktiviert sind. Wenn Edge-Workerknoten in einigen Zonen aktiviert sind, in anderen jedoch nicht, werden die Lastausgleichsfunktionen nicht gleichmäßig implementiert. Lastausgleichsfunktionen werden in einigen Zonen auf Edge-Knoten, in anderen Zonen jedoch auf regulären Knoten bereitgestellt.
  * Wenn Sie über mehrere VLANs für einen Cluster, mehrere Teilnetze in demselben VLAN oder einen Cluster mit mehreren Zonen verfügen, müssen Sie [VLAN-Spanning](/docs/infrastructure/vlans/vlan-spanning.html#vlan-spanning) für Ihr Konto für die IBM Cloud-Infrastruktur (SoftLayer) aktivieren, damit die Workerknoten in dem privaten Netz miteinander kommunizieren können. Um diese Aktion durchführen zu können, müssen Sie über die [Infrastrukturberechtigung](cs_users.html#infra_access) **Netz > VLAN-Spanning im Netz verwalten** verfügen oder Sie können den Kontoeigner bitte, diese zu aktivieren. Um zu prüfen, ob das VLAN-Spanning bereits aktiviert ist, verwenden Sie den [Befehl](/docs/containers/cs_cli_reference.html#cs_vlan_spanning_get) `ibmcloud ks vlan-spanning-get`. Wenn Sie {{site.data.keyword.BluDirectLink}} verwenden, müssen Sie stattdessen eine [ VRF-Funktion (Virtual Router Function)](/docs/infrastructure/direct-link/subnet-configuration.html#more-about-using-vrf) verwenden. Um VRF zu aktivieren, wenden Sie sich an Ihren Ansprechpartner für die IBM Cloud-Infrastruktur (SoftLayer).


Gehen Sie wie folgt vor, um einen Service für die Lastausgleichsfunktion in einem Mehrzonencluster einzurichten:
1.  [Stellen Sie die App für den Cluster bereit](cs_app.html#app_cli). Wenn Sie dem Cluster die App bereitstellen, wird mindestens ein Pod für Sie erstellt, von dem die App im Container ausgeführt wird. Stellen Sie sicher, dass Sie zur Bereitstellung im Metadatenabschnitt der Konfigurationsdatei eine Bezeichnung hinzufügen. Diese Bezeichnung ist zur Identifizierung aller Pods erforderlich, in denen Ihre App ausgeführt wird, damit sie in den Lastenausgleich aufgenommen werden können.

2.  Erstellen Sie einen Service für die App, den Sie öffentlich zugänglich machen möchten. Damit Ihre App im öffentlichen Internet oder in einem privaten Netz verfügbar wird, müssen Sie einen Kubernetes-Service für die App erstellen. Sie müssen den Service so konfigurieren, dass alle Pods, aus denen die App besteht, in den Lastenausgleich eingeschlossen sind.
  1. Erstellen Sie eine Servicekonfigurationsdatei namens `myloadbalancer.yaml` (Beispiel).
  2. Definieren Sie einen Service für die Lastausgleichsfunktion für die App, die Sie zugänglich machen möchten. Sie können eine Zone und eine IP-Adresse angeben.

      ```
      apiVersion: v1
      kind: Service
      metadata:
        name: myloadbalancer
        annotations:
          service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: <öffentlich_oder_privat>
          service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "<zone>"
      spec:
        type: LoadBalancer
        selector:
          <selektorschlüssel>: <selektorwert>
        ports:
         - protocol: TCP
             port: 8080
          loadBalancerIP: <ip-adresse>
      ```
      {: codeblock}

      <table>
      <caption>Erklärung der Komponenten der YAML-Datei</caption>
      <thead>
      <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
      </thead>
      <tbody>
      <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type:</code>
        <td>Annotation zum Angeben des Typs der Lastausgleichsfunktion. Zulässige Werte sind <code>private</code> und <code>public</code>. Bei der Erstellung einer öffentlichen Lastausgleichsfunktion in Clustern in öffentlichen VLANs ist diese Annotation nicht erforderlich.</td>
      </tr>
      <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-zone:</code>
        <td>Annotation zum Angeben der Zone, in der der Service für die Lastausgleichsfunktion bereitgestellt wird. Um Zonen anzuzeigen, führen Sie den Befehl <code>ibmcloud ks zones</code> aus.</td>
      </tr>
      <tr>
        <td><code>selector</code></td>
        <td>Geben Sie das Paar aus Kennzeichnungsschlüssel (<em>&lt;selektorschlüssel&gt;</em>) und Wert (<em>&lt;selektorwert&gt;</em>) ein, das Sie für die Ausrichtung auf die Pods, in denen Ihre App ausgeführt wird, verwenden möchten. Um die Pods als Ziel auszuwählen und in den Servicelastausgleich einzubeziehen, überprüfen Sie die Werte für <em>&lt;selektorschlüssel&gt;</em> und <em>&lt;selektorwert&gt;</em>. Stellen Sie sicher, dass es sich hierbei um dasselbe <em>Schlüssel/Wert</em>-Paar handelt, das Sie im Abschnitt <code>spec.template.metadata.labels</code> der YAML-Bereitstellungsdatei verwendet haben.</td>
      </tr>
      <tr>
        <td><code>port</code></td>
        <td>Der Port, den der Service überwacht.</td>
      </tr>
      <tr>
        <td><code>loadBalancerIP</code></td>
        <td>Optional: Um eine private Lastausgleichsfunktion zu erstellen oder um eine bestimmte portierbare IP-Adresse für eine öffentliche Lastausgleichsfunktion zu verwenden, ersetzen Sie <em>&lt;ip-adresse&gt;</em> durch die IP-Adresse, die Sie verwenden möchten. Wenn Sie eine Zone angeben, muss sich die IP-Adresse in diesem VLAN oder in dieser Zone befinden. Wenn Sie keine IP-Adresse angeben, gehen Sie wie folgt vor:<ul><li>Wenn sich Ihr Cluster in einem öffentlichen VLAN befindet, dann wird eine portierbare öffentliche IP-Adresse verwendet. Die meisten Cluster befinden sich in einem öffentlichen VLAN.</li><li>Wenn Ihr Cluster ausschließlich in einem privaten VLAN verfügbar ist, wird eine portierbare private IP-Adresse verwendet.</li></td>
      </tr>
      </tbody></table>

      Beispiel einer Konfigurationsdatei zum Erstellen eines privaten klassischen Service für die Lastausgleichsfunktion, von dem eine angegebene IP-Adresse in `dal12` verwendet wird:

      ```
      apiVersion: v1
      kind: Service
      metadata:
        name: myloadbalancer
        annotations:
          service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
          service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "dal12"
      spec:
        type: LoadBalancer
        selector:
          app: nginx
        ports:
         - protocol: TCP
           port: 8080
        loadBalancerIP: 172.21.xxx.xxx
      ```
      {: codeblock}

  3. Optional: Konfigurieren Sie eine Firewall, indem Sie `loadBalancerSourceRanges` im Abschnitt **spec** angeben. Weitere Informationen enthält die [Kubernetes-Dokumentation ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/tasks/access-application-cluster/configure-cloud-provider-firewall/).

  4. Erstellen Sie den Service in Ihrem Cluster.

      ```
      kubectl apply -f myloadbalancer.yaml
      ```
      {: pre}

3. Stellen Sie sicher, dass der LoadBalancer-Service erstellt wurde. Ersetzen Sie _&lt;mein_service&gt;_ durch den Namen des LoadBalancer-Service, den Sie im vorherigen Schritt erstellt haben.

    ```
    kubectl describe service myloadbalancer
    ```
    {: pre}

    **Hinweis:** Es kann ein paar Minuten dauern, bis der LoadBalancer-Service ordnungsgemäß erstellt und die App verfügbar ist.

    CLI-Beispielausgabe:

    ```
    Name:                   myloadbalancer
    Namespace:              default
    Labels:                 <keine>
    Selector:               app=liberty
    Type:                   LoadBalancer
    Zone:                   dal10
    IP:                     172.21.xxx.xxx
    LoadBalancer Ingress:   169.xx.xxx.xxx
    Port:                   <nicht angegeben> 8080/TCP
    NodePort:               <nicht angegeben> 32040/TCP
    Endpoints:              172.30.xxx.xxx:8080
    Session Affinity:       None
    Events:
      FirstSeen	LastSeen	Count	From			SubObjectPath	Type	 Reason			          Message
      ---------	--------	-----	----			-------------	----	 ------			          -------
      10s		    10s		    1	    {service-controller }	  Normal CreatingLoadBalancer	Creating load balancer
      10s		    10s		    1	    {service-controller }		Normal CreatedLoadBalancer	Created load balancer
    ```
    {: screen}

    Die IP-Adresse für **LoadBalancer Ingress** ist die portierbare IP-Adresse, die dem LoadBalancer-Service zugewiesen wurde.

4.  Wenn Sie eine öffentliche Lastausgleichsfunktion erstellt haben, dann greifen Sie über das Internet auf Ihre App zu.
    1.  Öffnen Sie Ihren bevorzugten Web-Browser.
    2.  Geben Sie die portierbare öffentliche IP-Adresse der Lastausgleichsfunktion und des Ports ein.

        ```
        http://169.xx.xxx.xxx:8080
        ```
        {: codeblock}        

5. Wenn Sie die [Beibehaltung der Quellen-IP für einen LoadBalancer-Service ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") aktivieren](https://kubernetes.io/docs/tutorials/services/source-ip/#source-ip-for-services-with-typeloadbalancer), stellen Sie sicher, dass App-Pods auf den Edge-Workerknoten geplant sind, indem Sie [Edge-Knoten-Affinität zu App-Pods hinzufügen](cs_loadbalancer.html#edge_nodes). App-Pods müssen auf Edge-Knoten geplant werden, um eingehende Anforderungen empfangen zu können.

6. Um eingehende Anforderungen von anderen Zonen an Ihre App zu bearbeiten, wiederholen Sie die obigen Schritte, um eine Lastausgleichsfunktion in jeder Zone hinzuzufügen.

7. Optional: Ein LoadBalancer-Service macht Ihre App auch über die NodePort-Instanzen des Service verfügbar. Auf [Knotenports (NodePorts)](cs_nodeport.html) kann über jede öffentliche und private IP-Adresse für jeden Knoten innerhalb des Clusters zugegriffen werden. Informationen zum Blockieren des Datenverkehrs an Knotenports während der Verwendung eines Service für die Lastausgleichsfunktion finden Sie im Abschnitt [Eingehenden Datenverkehr an Service für die Lastausgleichsfunktion oder NodePort-Service steuern](cs_network_policy.html#block_ingress).

## Öffentlichen oder privaten Zugriff auf eine App in einem Einzelzonencluster aktivieren
{: #config}

Vorbemerkungen:

-   Dieses Feature ist nur für Standardcluster verfügbar.
-   Es muss eine portierbare öffentliche oder private IP-Adresse verfügbar sein, die Sie dem Service für die Lastausgleichsfunktion (Load Balancer) zuweisen können.
-   Ein Service für die Lastausgleichsfunktion mit einer portierbaren privaten IP-Adresse verfügt weiterhin auf jedem Workerknoten über einen offenen öffentlichen Knotenport. Informationen zum Hinzufügen einer Netzrichtlinie zur Verhinderung von öffentlichem Datenverkehr finden Sie unter dem Thema [Eingehenden Datenverkehr blockieren](cs_network_policy.html#block_ingress).

Gehen Sie wie folgt vor, um einen Service für die Lastausgleichsfunktion zu erstellen:

1.  [Stellen Sie die App für den Cluster bereit](cs_app.html#app_cli). Wenn Sie dem Cluster die App bereitstellen, wird mindestens ein Pod für Sie erstellt, von dem die App im Container ausgeführt wird. Stellen Sie sicher, dass Sie zur Bereitstellung im Metadatenabschnitt der Konfigurationsdatei eine Bezeichnung hinzufügen. Diese Bezeichnung ist zur Identifizierung aller Pods erforderlich, in denen Ihre App ausgeführt wird, damit sie in den Lastenausgleich aufgenommen werden können.
2.  Erstellen Sie einen Service für die App, den Sie öffentlich zugänglich machen möchten. Damit Ihre App im öffentlichen Internet oder in einem privaten Netz verfügbar wird, müssen Sie einen Kubernetes-Service für die App erstellen. Sie müssen den Service so konfigurieren, dass alle Pods, aus denen die App besteht, in den Lastenausgleich eingeschlossen sind.
    1.  Erstellen Sie eine Servicekonfigurationsdatei namens `myloadbalancer.yaml` (Beispiel).

    2.  Definieren Sie einen LoadBalancer-Service für die App, die Sie zugänglich machen möchten.
        ```
        apiVersion: v1
        kind: Service
        metadata:
          name: myloadbalancer
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: <öffentlich_oder_privat>
        spec:
          type: LoadBalancer
          selector:
            <selektorschlüssel>: <selektorwert>
          ports:
           - protocol: TCP
             port: 8080
          loadBalancerIP: <ip-adresse>
        ```
        {: codeblock}

        <table>
        <caption>Erklärung der Komponenten der YAML-Datei</caption>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
        </thead>
        <tbody>
        <tr>
          <td>`service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type:`
          <td>Annotation zum Angeben des Typs der Lastausgleichsfunktion. Zulässige Werte sind `private` und `public`. Bei der Erstellung einer öffentlichen Lastausgleichsfunktion in Clustern in öffentlichen VLANs ist diese Annotation nicht erforderlich.</td>
        </tr>
        <tr>
          <td><code>selector</code></td>
          <td>Geben Sie das Paar aus Kennzeichnungsschlüssel (<em>&lt;selektorschlüssel&gt;</em>) und Wert (<em>&lt;selektorwert&gt;</em>) ein, das Sie für die Ausrichtung auf die Pods, in denen Ihre App ausgeführt wird, verwenden möchten. Um die Pods als Ziel auszuwählen und in den Servicelastausgleich einzubeziehen, überprüfen Sie die Werte für <em>&lt;selektorschlüssel&gt;</em> und <em>&lt;selektorwert&gt;</em>. Stellen Sie sicher, dass es sich hierbei um dasselbe <em>Schlüssel/Wert</em>-Paar handelt, das Sie im Abschnitt <code>spec.template.metadata.labels</code> der YAML-Bereitstellungsdatei verwendet haben.</td>
        </tr>
        <tr>
          <td><code>port</code></td>
          <td>Der Port, den der Service überwacht.</td>
        </tr>
        <tr>
          <td><code>loadBalancerIP</code></td>
          <td>Optional: Um eine private Lastausgleichsfunktion zu erstellen oder um eine bestimmte portierbare IP-Adresse für eine öffentliche Lastausgleichsfunktion zu verwenden, ersetzen Sie <em>&lt;ip-adresse&gt;</em> durch die IP-Adresse, die Sie verwenden möchten. Wenn Sie keine IP-Adresse angeben, gehen Sie wie folgt vor:<ul><li>Wenn sich Ihr Cluster in einem öffentlichen VLAN befindet, dann wird eine portierbare öffentliche IP-Adresse verwendet. Die meisten Cluster befinden sich in einem öffentlichen VLAN.</li><li>Wenn Ihr Cluster ausschließlich in einem privaten VLAN verfügbar ist, wird eine portierbare private IP-Adresse verwendet.</li></td>
        </tr>
        </tbody></table>

        Beispiel einer Konfigurationsdatei zum Erstellen eines privaten klassischen Service für die Lastausgleichsfunktion, von dem eine angegebene IP-Adresse verwendet wird:

        ```
        apiVersion: v1
        kind: Service
        metadata:
          name: myloadbalancer
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
        spec:
          type: LoadBalancer
          selector:
            app: nginx
          ports:
           - protocol: TCP
             port: 8080
          loadBalancerIP: 172.21.xxx.xxx
        ```
        {: codeblock}

    3.  Optional: Konfigurieren Sie eine Firewall, indem Sie `loadBalancerSourceRanges` im Abschnitt **spec** angeben. Weitere Informationen enthält die [Kubernetes-Dokumentation ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/tasks/access-application-cluster/configure-cloud-provider-firewall/).

    4.  Erstellen Sie den Service in Ihrem Cluster.

        ```
        kubectl apply -f myloadbalancer.yaml
        ```
        {: pre}

        Wenn der Lastenausgleichsservice erstellt wird, wird der Lastenausgleichsfunktion automatisch eine portierbare IP-Adresse zugewiesen. Ist keine portierbare IP-Adresse verfügbar, schlägt die Erstellung Ihres Lastenausgleichsservice fehl.

3.  Stellen Sie sicher, dass der Lastenausgleichsservice erstellt wurde.

    ```
    kubectl describe service myloadbalancer
    ```
    {: pre}

    **Hinweis:** Es kann ein paar Minuten dauern, bis der LoadBalancer-Service ordnungsgemäß erstellt und die App verfügbar ist.

    CLI-Beispielausgabe:

    ```
    Name:                   myloadbalancer
    Namespace:              default
    Labels:                 <none>
    Selector:               app=liberty
    Type:                   LoadBalancer
    Location:               dal10
    IP:                     172.21.xxx.xxx
    LoadBalancer Ingress:   169.xx.xxx.xxx
    Port:                   <unset> 8080/TCP
    NodePort:               <unset> 32040/TCP
    Endpoints:              172.30.xxx.xxx:8080
    Session Affinity:       None
    Events:
      FirstSeen	LastSeen	Count	From			SubObjectPath	Type	 Reason			          Message
      ---------	--------	-----	----			-------------	----	 ------			          -------
      10s		    10s		    1	    {service-controller }	  Normal CreatingLoadBalancer	Creating load balancer
      10s		    10s		    1	    {service-controller }		Normal CreatedLoadBalancer	Created load balancer
    ```
    {: screen}

    Die IP-Adresse für **LoadBalancer Ingress** ist die portierbare IP-Adresse, die dem LoadBalancer-Service zugewiesen wurde.

4.  Wenn Sie eine öffentliche Lastausgleichsfunktion erstellt haben, dann greifen Sie über das Internet auf Ihre App zu.
    1.  Öffnen Sie Ihren bevorzugten Web-Browser.
    2.  Geben Sie die portierbare öffentliche IP-Adresse der Lastausgleichsfunktion und des Ports ein.

        ```
        http://169.xx.xxx.xxx:8080
        ```
        {: codeblock}

5. Wenn Sie die [Beibehaltung der Quellen-IP für einen LoadBalancer-Service ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") aktivieren](https://kubernetes.io/docs/tutorials/services/source-ip/#source-ip-for-services-with-typeloadbalancer), stellen Sie sicher, dass App-Pods auf den Edge-Workerknoten geplant sind, indem Sie [Edge-Knoten-Affinität zu App-Pods hinzufügen](cs_loadbalancer.html#edge_nodes). App-Pods müssen auf Edge-Knoten geplant werden, um eingehende Anforderungen empfangen zu können.

6. Optional: Ein LoadBalancer-Service macht Ihre App auch über die NodePort-Instanzen des Service verfügbar. Auf [Knotenports (NodePorts)](cs_nodeport.html) kann über jede öffentliche und private IP-Adresse für jeden Knoten innerhalb des Clusters zugegriffen werden. Informationen zum Blockieren des Datenverkehrs an Knotenports während der Verwendung eines Service für die Lastausgleichsfunktion finden Sie im Abschnitt [Eingehenden Datenverkehr an Service für die Lastausgleichsfunktion oder NodePort-Service steuern](cs_network_policy.html#block_ingress).

<br />


## Knotenaffinität und Tolerierungen zu App-Pods für eine Quellen-IP hinzufügen
{: #node_affinity_tolerations}

Wenn eine Clientanforderung an Ihre App an Ihren Cluster gesendet wird, wird die Anforderung an den Pod für den LoadBalancer-Service weitergeleitet, der Ihre App verfügbar macht. Wenn ein App-Pod nicht auf demselben Workerknoten vorhanden ist wie der Lastausgleichsfunktions-Pod, leitet die Lastausgleichsfunktion die Anforderung an einen App-Pod auf einem anderen Workerknoten weiter. Die Quellen-IP-Adresse des Pakets wird in die öffentliche IP-Adresse des Workerknotens geändert, auf dem der App-Pod ausgeführt wird.

Um die ursprüngliche Quellen-IP-Adresse der Clientanforderung beizubehalten, können Sie die [Quellen-IP ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip) für LoadBalancer-Services aktivieren. Die TCP-Verbindung wird bis zu den App-Pods fortgesetzt, sodass die App die tatsächliche IP-Adresse des Initiators sehen kann. Das Beibehalten der IP des Clients ist nützlich, z. B. wenn App-Server Sicherheits- und Zugriffssteuerungsrichtlinien genügen müssen.

Nachdem Sie die Quellen-IP aktiviert haben, müssen Lastausgleichsfunktions-Pods Anforderungen an App-Pods weiterleiten, die auf demselben Workerknoten bereitgestellt sind. In der Regel werden auch Lastausgleichsfunktions-Pods auf den Workerknoten bereitgestellt, auf denen sich die App-Pods befinden. Es kann jedoch vorkommen, dass die Lastausgleichsfunktions-Pods und die App-Pods nicht auf demselben Workerknoten geplant sind:

* Sie verfügen Edge-Knoten, auf die ein Taint angewendet wurde und auf denen deshalb nur Lastausgleichsfunktions-Pods bereitgestellt werden können. App-Pods dürfen auf diesen Knoten nicht bereitgestellt werden.
* Ihr Cluster ist mit mehreren öffentlichen oder privaten VLANs verbunden und Ihre App-Pods werden unter Umständen auf Workerknoten bereitgestellt, die nur mit einem VLAN verbunden sind. Lastausgleichsfunktions-Pods lassen sich möglicherweise nicht auf solchen Workerknoten bereitstellen, weil die IP-Adresse der Lastausgleichsfunktion mit einem anderen VLAN als die Workerknoten verbunden ist.

Um zu erzwingen, dass Ihre App auf bestimmten Workerknoten bereitgestellt wird, auf denen auch Lastausgleichsfunktions-Pods bereitgestellt werden können, müssen Sie Affinitätsregeln und Tolerierungen zu Ihrer App-Bereitstellung hinzufügen.

### Affinitätsregeln und Tolerierungen für Edge-Knoten hinzufügen
{: #edge_nodes}

Wenn Sie [Workerknoten als Edge-Knoten kennzeichnen](cs_edge.html#edge_nodes) und zudem [Taints auf Edge-Knoten anwenden](cs_edge.html#edge_workloads), werden Lastausgleichsfunktions-Pods nur auf diesen Edge-Knoten bereitgestellt und App-Pods können nicht auf Edge-Knoten implementiert werden. Wenn die Quellen-Ip für den LoadBalancer-Service aktiviert ist, können die Lastausgleichsfunktions-Pods auf den Edge-Knoten eingehende Anforderungen nicht an die App-Pods auf anderen Workerknoten weiterleiten.
{:shortdesc}

Um zu erzwingen, dass Ihre App-Pods auf Edge-Knoten bereitgestellt werden, fügen Sie eine [Affinitätsregel ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#node-affinity-beta-feature) für den Edge-Knoten und eine [Tolerierung ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/#concepts) zur App-Bereitstellung hinzu.

Beispiel für die YAML-Bereitstellungsdatei mit Edge-Knoten-Affinität und -Tolerierung:

```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: with-node-affinity
spec:
  template:
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: dedicated
                operator: In
                values:
                - edge
      tolerations:
        - key: dedicated
          value: edge
...
```
{: codeblock}

In beiden Abschnitten **affinity** und **tolerations** ist der Wert `dedicated` für `key` und der Wert `edge` für `value` angegeben.

### Affinitätsregeln für mehrere öffentliche oder private VLANs hinzufügen
{: #edge_nodes_multiple_vlans}

Wenn Ihr Cluster mit mehreren öffentlichen oder privaten VLANs verbunden ist, werden Ihre App-Pods unter Umständen auf Workerknoten bereitgestellt, die nur mit einem VLAN verbunden sind. Wenn die IP-Adresse der Lastausgleichsfunktion mit einem anderen VLAN als diese Workerknoten verbunden ist, werden die Lastausgleichsfunktions-Pods nicht auf diesen Workerknoten bereitgestellt.
{:shortdesc}

Wenn die Quellen-IP aktiviert ist, planen Sie App-Pods auf Workerknoten, die dasselbe VLAN wie die IP-Adresse der Lastausgleichsfunktion aufweisen, indem Sie eine Affinitätsregel zur App-Bereitstellung hinzufügen.

Vorbereitende Schritte: [Melden Sie sich an Ihrem Konto an. Geben Sie als Ziel die entsprechende Region und - sofern anwendbar - die Ressourcengruppe an. Legen Sie den Kontext für den Cluster fest.](cs_cli_install.html#cs_cli_configure)

1. Rufen Sie die IP-Adresse des LoadBalancer-Service ab. Suchen Sie im Feld **LoadBalancer Ingress** nach der IP-Adresse.
    ```
    kubectl describe service <name_des_loadbalancer-service>
    ```
    {: pre}

2. Rufen Sie die VLAN-ID ab, mit der Ihr LoadBalancer-Service verbunden ist.

    1. Listen Sie portierbare öffentliche VLANs für Ihren Cluster auf.
        ```
        ibmcloud ks cluster-get <clustername_oder_-id> --showResources
        ```
        {: pre}

        Beispielausgabe:
        ```
        ...

        Subnet VLANs
        VLAN ID   Subnet CIDR       Public   User-managed
        2234947   10.xxx.xx.xxx/29  false    false
        2234945   169.36.5.xxx/29   true     false
        ```
        {: screen}

    2. Suchen Sie in der Ausgabe unter **Subnet VLANs** nach der Teilnetz-CIDR, die mit der IP-Adresse der Lastausgleichsfunktion übereinstimmt, die Sie zuvor abgerufen haben, und notieren Sie sich die VLAN-ID.

        Wenn die IP-Adresse des LoadBalancer-Service beispielsweise `169.36.5.xxx` lautet, ist das passende Teilnetz in der Beispielausgabe aus dem vorherigen Schritt `169.36.5.xxx/29`. Die VLAN-ID, mit der das Teilnetz verbunden ist, lautet `2234945`.

3. [Fügen Sie eine Affinitätsregel ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#node-affinity-beta-feature) zu der App-Bereitstellung für die VLAN-ID hinzu, die Sie sich im vorherigen Schritt notiert haben.

    Wenn Sie beispielsweise über mehrere VLANs verfügen, aber Ihre App-Pods nur auf Workerknoten im öffentlichen VLAN `2234945` bereitstellen möchten.

    ```
    apiVersion: extensions/v1beta1
    kind: Deployment
    metadata:
      name: with-node-affinity
    spec:
      template:
        spec:
          affinity:
            nodeAffinity:
              requiredDuringSchedulingIgnoredDuringExecution:
                nodeSelectorTerms:
                - matchExpressions:
                  - key: publicVLAN
                    operator: In
                    values:
                    - "2234945"
    ...
    ```
    {: codeblock}

    In der YAML-Beispieldatei enthält der Abschnitt **affinity** den Wert `publicVLAN` für `key` und den Wert `"2234945"` für `value`.

4. Wenden Sie die aktualisierte Bereitstellungskonfigurationsdatei an.
    ```
    kubectl apply -f with-node-affinity.yaml
    ```
    {: pre}

5. Überprüfen Sie, dass die App-Pods auf Workerknoten bereitgestellt werden, die mit dem designierten VLAN verbunden sind.

    1. Listen Sie die Pods in Ihrem Cluster auf. Ersetzen Sie `<selector>` durch die Bezeichnung, die Sie für die App verwendet haben.
        ```
        kubectl get pods -o wide app=<selektor>
        ```
        {: pre}

        Beispielausgabe:
        ```
        NAME                   READY     STATUS              RESTARTS   AGE       IP               NODE
        cf-py-d7b7d94db-vp8pq  1/1       Running             0          15d       172.30.xxx.xxx   10.176.48.78
        ```
        {: screen}

    2. Geben Sie in der Ausgabe einen Pod für Ihre App an. Notieren Sie sich die Knoten-ID (**NODE**) des Workerknotens, auf dem sich der Pod befindet.

        In der Beispielausgabe aus dem vorherigen Schritt befindet sich der App-Pod `cf-py-d7b7d94db-vp8pq` auf dem Workerknoten `10.176.48.78`.

    3. Listen Sie die Details für den Workerknoten auf.

        ```
        kubectl describe node <workerknoten-ID>
        ```
        {: pre}

        Beispielausgabe:

        ```
        Name:                   10.xxx.xx.xxx
        Role:
        Labels:                 arch=amd64
                                beta.kubernetes.io/arch=amd64
                                beta.kubernetes.io/os=linux
                                failure-domain.beta.kubernetes.io/region=us-south
                                failure-domain.beta.kubernetes.io/zone=dal10
                                ibm-cloud.kubernetes.io/encrypted-docker-data=true
                                kubernetes.io/hostname=10.xxx.xx.xxx
                                privateVLAN=2234945
                                publicVLAN=2234967
        ...
        ```
        {: screen}

    4. Überprüfen Sie im Abschnitt **Labels** der Ausgabe, dass es sich bei dem öffentlichen oder privaten VLAN um das VLAN handelt, das Sie in den vorherigen Schritten angegeben haben.

