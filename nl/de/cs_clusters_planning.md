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


# Einrichtung Ihrer Cluster und Workerknoten planen
{: #plan_clusters}
Konzipieren Sie Ihren Standardcluster mit {{site.data.keyword.containerlong}} für maximale Verfügbarkeit und Kapazität für Ihre App.

## Hoch verfügbare Cluster
{: #ha_clusters}

Die Wahrscheinlichkeit, dass Ihre Benutzer Ausfallzeiten verzeichnen, ist geringer, wenn Sie Ihre Apps auf mehrere Workerknoten, Zonen und Cluster verteilen. Integrierte Funktionen wie Lastausgleich (Load Balancing) und Isolation erhöhen die Ausfallsicherheit gegenüber möglichen Fehlerbedingungen mit Hosts, Netzen oder Apps.
{: shortdesc}

Betrachten Sie diese potenziellen Clusterkonfigurationen, die nach zunehmendem Grad der Verfügbarkeit angeordnet sind.

![Hochverfügbarkeit für Cluster](images/cs_cluster_ha_roadmap_multizone.png)

1. Ein [Einzelzonencluster](#single_zone) mit mehreren Workerknoten in einem Worker-Pool.
2. Ein [Mehrzonencluster](#multizone), der Workerknoten über Zonen hinweg in einer Region verteilt.
3. [Mehrere Cluster](#multiple_clusters), die über Zonen oder Regionen hinweg eingerichtet werden und über eine globale Lastausgleichsfunktion verbunden sind.

## Einzelzonencluster
{: #single_zone}

Um die Verfügbarkeit für Ihre App zu verbessern und einen Failover für den Fall zu ermöglichen, dass ein Workerknoten in Ihrem Cluster nicht verfügbar ist, fügen Sie Ihrem Einzelzonencluster zusätzliche Workerknoten hinzu.
{: shortdesc}

<img src="images/cs_cluster_singlezone.png" alt="Hochverfügbarkeit für Cluster in einer einzelnen Zone" width="230" style="width:230px; border-style: none"/>

Standardmäßig wird der Einzelzonencluster mit einem Worker-Pool konfiguriert, der den Namen `default` hat. Der Worker-Pool gruppiert Workerknoten mit derselben Konfiguration, wie z. B. dem Maschinentyp, die Sie während der Clustererstellung definiert haben. Sie können Ihrem Cluster weitere Workerknoten hinzufügen, indem Sie [die Größe eines vorhandenen Worker-Pools ändern](cs_clusters.html#resize_pool) oder [einen neuen Worker-Pool hinzufügen](cs_clusters.html#add_pool).

Wenn Sie weitere Workerknoten hinzufügen, können App-Instanzen auf mehrere Workerknoten verteilt werden. Wenn ein Workerknoten ausfällt, werden die App-Instanzen auf den verfügbaren Workerknoten weiter ausgeführt. Kubernetes plant Pods von nicht verfügbaren Workerknoten automatisch neu, um die Leistung und Kapazität für Ihre App zu gewährleisten. Um sicherzustellen, dass die Pods gleichmäßig auf die Workerknoten verteilt werden, implementieren Sie [Pod-Affinität](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#inter-pod-affinity-and-anti-affinity-beta-feature).

**Kann ich einen Einzelzonencluster in einen Mehrzonencluster konvertieren?**</br>
Ja, wenn sich der Cluster in einer der [ unterstützten Metropolen mit mehreren Zonen](cs_regions.html#zones) befindet. Weitere Informationen finden Sie im Abschnitt [Von eigenständigen Workerknoten auf Worker-Pools aktualisieren](cs_cluster_update.html#standalone_to_workerpool).


**Muss ich Mehrzonencluster verwenden?**</br>
Nein. Sie können so viele Einzelzonencluster erstellen, wie Sie möchten. Möglicherweise bevorzugen Sie tatsächlich Einzelzonencluster für ein vereinfachtes Management oder für den Fall, dass Ihr Cluster sich in einer bestimmten [Stadt mit einer einzigen Zone](cs_regions.html#zones) befinden muss.


## Mehrzonencluster
{: #multizone}

Mit {{site.data.keyword.containerlong}} können Sie Mehrzonencluster erstellen. Die Wahrscheinlichkeit, dass Ihre Benutzer Ausfallzeiten verzeichnen, ist geringer, wenn Sie Ihre Apps mithilfe von Worker-Pools auf mehrere Workerknoten und Zonen verteilen. Integrierte Funktionen wie der Lastausgleich erhöhen die Ausfallsicherheit bei potenziellen Zonenausfällen mit Hosts, Netzwerken oder Apps. Wenn Ressourcen in einer Zone inaktiv sind, werden Ihre Cluster-Workloads in den anderen Zonen immer noch verarbeitet. **Hinweis**: Es sind nur Einzelzonencluster für {{site.data.keyword.Bluemix_dedicated_notm}}-Instanzen verfügbar.
{: shortdesc}

**Was ist ein Worker-Pool?**</br>
Bei einem Worker-Pool handelt es sich um eine Sammlung von Workerknoten mit derselben Version, wie Maschinentyp, CPU und Speicher. Wenn Sie einen Cluster erstellen, wird automatisch ein Worker-Pool für Sie erstellt. Sie können neue `ibmcloud ks worker-pool`-Befehle verwenden, um die Workerknoten in Ihrem Pool über Zonen zu verteilen, Workerknoten zum Pool hinzuzufügen oder Workerknoten zu aktualisieren.

**Kann ich noch eigenständige Workerknoten verwenden?**</br>
Das bisherige Cluster-Setup mit eigenständigen Workerknoten wird zwar noch unterstützt, jedoch nicht mehr weiterentwickelt. Stellen Sie sicher, dass Sie [einen Worker-Pool zu Ihrem Cluster hinzufügen](cs_clusters.html#add_pool) und anschließend [zur Verwendung von Worker-Pools migrieren](cs_cluster_update.html#standalone_to_workerpool), um Ihre Workerknoten anstelle von eigenständigen Workerknoten zu organisieren.

**Kann ich einen Einzelzonencluster in einen Mehrzonencluster konvertieren?**</br>
Ja, wenn sich der Cluster in einer der [ unterstützten Metropolen mit mehreren Zonen](cs_regions.html#zones) befindet. Weitere Informationen finden Sie im Abschnitt [Von eigenständigen Workerknoten auf Worker-Pools aktualisieren](cs_cluster_update.html#standalone_to_workerpool).


### Ich möchte mehr über die Mehrzonenclusterkonfiguration erfahren
{: #mz_setup}

<img src="images/cs_cluster_multizone.png" alt="Hochverfügbarkeit für Mehrzonencluster" width="500" style="width:500px; border-style: none"/>


Sie können zusätzliche Zonen zu Ihrem Cluster hinzufügen, um die Workerknoten in den Worker-Pools über mehrere Zonen in einer Region zu replizieren. Mehrzonencluster sind so konzipiert, dass die Pods gleichmäßig auf die Workerknoten und Zonen verteilt werden, um die Verfügbarkeit und Wiederherstellung nach einem Ausfall zu gewährleisten. Wenn die Workerknoten nicht gleichmäßig über die Zonen verteilt sind oder die Kapazität in einer der Zonen nicht ausreicht, kann der Kubernetes-Scheduler möglicherweise nicht alle angeforderten Pods planen. Daher können Pods in den Status **Anstehend** wechseln, bis eine ausreichende Kapazität verfügbar ist. Wenn Sie das Standardverhalten ändern möchten, damit der Kubernetes-Scheduler Pods in Zonen optimal verteilen kann, verwenden Sie die [Pod-Affinitätsrichtlinie](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#inter-pod-affinity-and-anti-affinity-beta-feature) `preferredDuringSchedulingIgnoredDuringExecution`.

**Warum benötige ich Workerknoten in drei Zonen?** </br>
Durch die Verteilung der Arbeitslast auf drei Zonen wird die hohe Verfügbarkeit Ihre App für den Fall sichergestellt, dass eine oder zwei Zonen nicht verfügbar sind. Zusätzlich kann eine solche Verteilung Ihr Cluster-Setup auch kosteneffizienter machen. Sie fragen sich, warum das so ist? Hier ist ein Beispiel.

Angenommen, Sie benötigen einen Workerknoten mit sechs Kernen, um die Arbeitslast für Ihre App zu verarbeiten. Für eine höhere Verfügbarkeit Ihres Clusters stehen Ihnen die folgenden Optionen zur Verfügung:

- **Ressourcen in einer anderen Zone duplizieren:** Mit dieser Option erhalten Sie zwei Workerknoten mit jeweils sechs Kernen in jeder Zone, wodurch insgesamt 12 Kerne verfügbar sind. </br>
- **Ressourcen auf drei Zonen verteilen:** Mit dieser Option stellen Sie drei Kerne pro Zone bereit, wodurch Sie eine Gesamtkapazität von neun Kernen erhalten. Um Ihre Arbeitslast verarbeiten zu können, müssen zwei Zonen gleichzeitig aktiv sein. Wenn eine Zone nicht verfügbar ist, können die anderen beiden Zonen die Arbeitslast verarbeiten. Wenn zwei Zonen nicht verfügbar sind, können die drei verbleibenden Kerne die Arbeitslast übernehmen. Durch die Bereitstellung von drei Kernen pro Zone können Sie mit kleineren Maschinen arbeiten und gleichzeitig die Kosten senken.</br>

**Wie wird mein Kubernetes-Master eingerichtet?** </br>
Ein Mehrzonencluster wird mit einem einzigen Kubernetes-Master eingerichtet, der im selben Metrobereich wie die Worker bereitgestellt wird. Wenn sich die Worker beispielsweise in einer oder mehreren Zonen des Typs `dal10`, `dal12` oder `dal13` befinden, befindet sich der Master in der Metropole 'Dallas' mit mehreren Zonen.

**Was passiert, wenn der Kubernetes-Master nicht mehr verfügbar ist?** </br>
Der [Kubernetes-Master](cs_tech.html#architecture) ist die Hauptkomponente, die den Cluster betriebsbereit hält. Der Master speichert Clusterressourcen und ihre Konfigurationen in der etcd-Datenbank, die als Single Point of Truth für Ihren Cluster dient. Der Kubernetes-API-Server dient als Haupteinstiegspunkt für alle Anforderungen der Clusterverwaltung von den Workerknoten zum Master oder wenn Sie mit Ihren Clusterressourcen interagieren möchten.<br><br>Wenn ein Masterausfall auftritt, werden Ihre Workloads weiterhin auf den Workerknoten ausgeführt, Sie können jedoch erst wieder `kubectl`-Befehle verwenden, um mit Ihren Clusterressourcen zu arbeiten oder den Clusterzustand anzuzeigen, wenn der Kubernetes-API-Server im Master wieder betriebsbereit ist. Wenn ein Pod während des Ausfalls des Masters inaktiv ist, kann der Pod erst wieder ausgeführt werden, wenn der Workerknoten den Kubernetes-API-Server wieder erreichen kann.<br><br>Während eines Masterausfalls können Sie `ibmcloud ks`-Befehle weiterhin für die {{site.data.keyword.containerlong_notm}}-API ausführen, um mit Ihren Infrastrukturressourcen zu arbeiten (z. B. Workerknoten oder VLANs). Wenn Sie die aktuelle Clusterkonfiguration ändern, indem Sie Workerknoten zum Cluster hinzufügen oder aus ihm entfernen, werden die Änderungen erst wirksam, wenn der Master wieder betriebsbereit ist. **Hinweis**: Ein Workerknoten darf während eines Masterausfalls nicht neu gestartet werden. Durch diese Aktion werden die Pods aus dem Workerknoten entfernt. Da der Kubernetes-API-Server nicht verfügbar ist, können die Pods nicht auf andere Workerknoten im Cluster umgestellt werden.


Um Ihren Cluster vor einem Ausfall des Kubernetes-Masters oder in Regionen zu schützen, in denen Mehrzonencluster nicht verfügbar sind, können Sie [mehrere Cluster einrichten und diese mit einer globalen Lastausgleichsfunktion verbinden](#multiple_clusters).

**Muss ich etwas tun, damit der Master über Zonen hinweg mit den Workern kommunizieren kann?**</br>
Ja. Wenn Sie über mehrere VLANs für einen Cluster, mehrere Teilnetze in demselben VLAN oder einen Cluster mit mehreren Zonen verfügen, müssen Sie [VLAN-Spanning](/docs/infrastructure/vlans/vlan-spanning.html#vlan-spanning) für Ihr Konto für die IBM Cloud-Infrastruktur (SoftLayer) aktivieren, damit die Workerknoten in dem privaten Netz miteinander kommunizieren können. Um diese Aktion durchführen zu können, müssen Sie über die [Infrastrukturberechtigung](cs_users.html#infra_access) **Netz > VLAN-Spanning im Netz verwalten** verfügen oder Sie können den Kontoeigner bitte, diese zu aktivieren. Um zu prüfen, ob das VLAN-Spanning bereits aktiviert ist, verwenden Sie den [Befehl](/docs/containers/cs_cli_reference.html#cs_vlan_spanning_get) `ibmcloud ks vlan-spanning-get`. Wenn Sie {{site.data.keyword.BluDirectLink}} verwenden, müssen Sie stattdessen eine [ VRF-Funktion (Virtual Router Function)](/docs/infrastructure/direct-link/subnet-configuration.html#more-about-using-vrf) verwenden. Um VRF zu aktivieren, wenden Sie sich an Ihren Ansprechpartner für die IBM Cloud-Infrastruktur (SoftLayer).

**Wie kann ich meine Benutzer über das öffentliche Internet auf meine App zugreifen lassen?**</br>
Sie können Ihre Apps über eine Ingress-Lastausgleichsfunktion für Anwendungen (ALB) oder einen LoadBalancer-Service zugänglich machen.

- **Ingress-Lastausgleichsfunktion für Anwendungen (ALB):** Standardmäßig werden öffentliche ALBs automatisch in jeder Zone in Ihrem Cluster erstellt und aktiviert. Außerdem wird auch automatisch eine Cloudflare-Lastausgleichsfunktion für mehrere Zonen (Multizone Load Balancer, MZLB) für Ihren Cluster erstellt und bereitgestellt, sodass eine MZLB für jede Region vorhanden ist. Die MZLB stellt die IP-Adressen Ihrer ALBs hinter denselben Hostnamen und aktiviert die Zustandsprüfungen für diese IP-Adressen, um zu ermitteln, ob sie verfügbar sind oder nicht. Wenn Sie beispielsweise Workerknoten in drei (3) Zonen in der Region 'Vereinigte Staaten (Osten)' haben, hat der Hostname `yourcluster.us-east.containers.appdomain.cloud` drei ALB-IP-Adressen. Der MZLB-Status überprüft die öffentliche ALB-IP in jeder Zone des Clusters und hält die Ergebnisse der DNS-Suche auf der Basis dieser Zustandsprüfungen aktualisiert. Weitere Informationen finden Sie im Abschnitt [Komponenten und Architektur von Ingress](cs_ingress.html#planning).

- **Lastenausgleichsservices:** Lastenausgleichsservices werden nur in einer Zone konfiguriert. Eingehende Anforderungen an Ihre App werden von dieser einen Zone an alle App-Instanzen in anderen Zonen weitergeleitet. Wenn diese Zone nicht mehr verfügbar ist, ist Ihre App möglicherweise nicht über das Internet erreichbar. Um einem Ausfall einer einzelnen Zone gerecht zu werden, können Sie zusätzliche LoadBalancer-Services in weiteren Zonen einrichten. Weitere Informationen finden Sie im Abschnitt zu den hoch verfügbaren [LoadBalancer-Services](cs_loadbalancer.html#multi_zone_config).

**Kann ich persistenten Speicher für meinen Mehrzonencluster einrichten?**</br>
Verwenden Sie für hoch verfügbaren persistenten Speicher einen Cloud-Service wie [{{site.data.keyword.cloudant_short_notm}}](/docs/services/Cloudant/getting-started.html#getting-started-with-cloudant) or [{{site.data.keyword.cos_full_notm}}](/docs/services/cloud-object-storage/about-cos.html#about-ibm-cloud-object-storage).

Der NFS-Datei- und -Blockspeicher kann nicht über Zonen hinweg gemeinsam genutzt werden. Persistente Datenträger können nur in der Zone verwendet werden, in der sich die tatsächliche Speichereinheit befindet. Wenn Sie über NFS-Datei- oder -Blockspeicher in Ihrem Cluster verfügen, den Sie weiterhin verwenden möchten, müssen Sie Regions- und Zonenbezeichnungen auf vorhandene persistente Datenträger anwenden. Mithilfe dieser Bezeichnungen kann 'kube-scheduler' bestimmen, wo eine App geplant werden soll, die den persistenten Datenträger verwendet. Führen Sie den folgenden Befehl aus und ersetzen Sie `<meincluster>` durch den Namen Ihres Clusters.

```
bash <(curl -Ls https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/file-pv-labels/apply_pv_labels.sh) <meincluster>
```
{: pre}

** Ich habe meinen Mehrzonencluster erstellt. Warum gibt es immer noch immer nur eine Zone? Wie füge ich Zonen zu meinem Cluster hinzu?**</br>
Wenn Sie [Ihren Mehrzonencluster mit der CLI erstellen](cs_clusters.html#clusters_cli), wird der Cluster zwar erstellt, Sie müssen jedoch Zonen zum Worker-Pool hinzufügen, um den Prozess abzuschließen. Damit sich der Cluster über mehrere Zonen erstreckt, muss er sich in einer [Metropole mit mehreren Zonen](cs_regions.html#zones) befinden. Informationen zum Hinzufügen einer Zone zu Ihrem Cluster und zum Verteilen von Workerknoten auf Zonen finden Sie im Abschnitt [Zone zu Ihrem Cluster hinzufügen](cs_clusters.html#add_zone).

### Wie wird sich das zukünftige Management meiner Cluster vom aktuellen Management unterscheiden?
{: #mz_new_ways}

Mit der Einführung von Worker-Pools können Sie eine neue Gruppe von APIs und Befehlen zum Verwalten des Clusters verwenden. Sie finden diese neuen Befehle auf der [Seite mit der CLI-Dokumentation](cs_cli_reference.html#cs_cli_reference). In Ihrem Terminal können Sie sie durch Ausführen des Befehls `ibmcloud ks help` anzeigen.

In der folgenden Tabelle werden die alten und neuen Methoden für einige allgemeine Aktionen dern Clusterverwaltung miteinander verglichen.
<table summary="Die Tabelle enthält die Beschreibung der neuen Vorgehensweisen zum Ausführen von Mehrzonenbefehlen. Die Tabellenzeilen enthalten von links nach rechts die Beschreibung in der ersten Spalte, die alte Vorgehensweise in der zweiten Spalte und die neue Vorgehensweise für Worker-Pools mit mehreren Zonen in der dritten Spalte.">
<caption>Neue Methoden für Befehle für Worker-Pools mit mehreren Zonen.</caption>
  <thead>
  <th>Beschreibung</th>
  <th>Alte eigenständige Workerknoten</th>
  <th>Neue Worker-Pools mit mehreren Zonen</th>
  </thead>
  <tbody>
    <tr>
    <td>Hinzufügen von Workerknoten zum Cluster.</td>
    <td><strong>Veraltet</strong>: <code>ibmcloud ks worker-add</code> zum Hinzufügen eigenständiger Workerknoten.</td>
    <td><ul><li>Um andere Maschinentypen als Ihren vorhandenen Pool hinzuzufügen, erstellen Sie einen neuen Worker-Pool: [Befehl <code>ibmcloud ks worker-pool-create</code>](cs_cli_reference.html#cs_worker_pool_create).</li>
    <li>Wenn Sie Workerknoten zu einem vorhandenen Pool hinzufügen möchten, ändern Sie die Anzahl der Knoten pro Zone im Pool: [Befehl <code>ibmcloud ks worker-pool-resize</code>](cs_cli_reference.html#cs_worker_pool_resize).</li></ul></td>
    </tr>
    <tr>
    <td>Entfernen von Workerknoten aus dem Cluster.</td>
    <td><code>ibmcloud ks worker-rm</code>: Sie können diesen Befehl immer noch zum Löschen eines problematischen Workerknoten aus dem Cluster verwenden.</td>
    <td><ul><li>Wenn ein Worker-Pool nicht ausgeglichen ist, z. B. nach dem Entfernen eines Workerknotens, gleichen Sie ihn neu aus: [Befehl <code>ibmcloud ks worker-pool-rebalance</code>](cs_cli_reference.html#cs_rebalance).</li>
    <li>Um die Anzahl der Workerknoten in einem Pool zu reduzieren, ändern Sie die Anzahl pro Zone (Mindestwert '1'): [Befehl <code>ibmcloud ks worker-pool-resize</code>](cs_cli_reference.html#cs_worker_pool_resize).</li></ul></td>
    </tr>
    <tr>
    <td>Verwenden Sie ein neues VLAN für Workerknoten.</td>
    <td><strong>Veraltet</strong>: Fügen Sie einen neuen Workerknoten hinzu, der das neue private oder öffentliche VLAN verwendet: <code>ibmcloud ks worker-add</code>.</td>
    <td>Legen Sie den Worker-Pool so fest, dass er ein anderes öffentliches oder privates VLAN als zuvor verwendet: [Befehl <code>ibmcloud ks zone-network-set</code>](cs_cli_reference.html#cs_zone_network_set).</td>
    </tr>
  </tbody>
  </table>

## Mehrere Cluster, die mit einer globalen Lastausgleichsfunktion verbunden sind
{: #multiple_clusters}

Um Ihre App bei einem Ausfall eines Kubernetes-Masters zu schützen und für Regionen, in denen Mehrzonencluster nicht verfügbar sind, können Sie mehrere Cluster in verschiedenen Zonen in einer Region erstellen und diese mit einer globalen Lastausgleichsfunktion verbinden.
{: shortdesc}

<img src="images/cs_multiple_cluster_zones.png" alt="Hochverfügbarkeit für mehrere Cluster" width="700" style="width:700px; border-style: none"/>

Um Ihre Arbeitslast auf mehrere Cluster zu verteilen, müssen Sie eine globale Lastausgleichsfunktion einrichten und die IP-Adressen der Lastausgleichsfunktionen für Anwendungen (ALBs) oder LoadBalancer-Services zu Ihrer Domäne hinzufügen. Durch das Hinzufügen dieser IP-Adressen können Sie eingehenden Datenverkehr zwischen Ihren Clustern weiterleiten. Damit die globale Lastausgleichsfunktion erkennen kann, ob einer der Cluster nicht verfügbar ist, sollten Sie in Betracht ziehen, jeder IP-Adresse eine Ping-basierte Statusprüfung hinzuzufügen. Wenn Sie diese Prüfung einrichten, überprüft Ihr DNS-Provider regelmäßig mit Ping die IP-Adressen, die Sie zu Ihrer Domäne hinzugefügt haben. Wenn eine IP-Adresse nicht mehr verfügbar ist, wird der Datenverkehr nicht mehr an diese IP-Adresse gesendet. Kubernetes startet jedoch nicht automatisch erneut Pods von dem nicht verfügbaren Cluster auf Workerknoten in verfügbaren Clustern. Wenn Kubernetes die Pods automatisch in verfügbaren Clustern erneut starten soll, sollten Sie einen [Mehrzonencluster](#multizone) einrichten.

**Warum benötige ich drei Cluster in drei Zonen?** </br>
Ähnlich wie bei der Verwendung von [drei Zonen in Mehrzonenclustern](#multizone) können Sie mehr Verfügbarkeit für Ihre App bereitstellen, indem Sie drei Cluster über Zonen hinweg einrichten. Sie können auch Kosten reduzieren,, indem Sie sich kleinere Maschinen für die Verarbeitung Ihrer Arbeitslast anschaffen.

**Was ist, wenn ich mehrere Cluster in mehreren Regionen einrichten möchte?** </br>
Sie können mehrere Cluster in verschiedenen Regionen eines geografischen Standortes (wie 'Vereinigte Staaten (Süden)' und 'Vereinigte Staaten (Osten)') oder über geografische Standorte hinweg ('Vereinigte Staaten (Süden)' und 'Mitteleuropa') einrichten. Beide Setups bieten das gleiche Maß an Verfügbarkeit für Ihre App, sind aber bei der gemeinsamen Nutzung von Daten und der Datenreplikation komplexer als andere Lösungen. In den meisten Fällen reicht es aus, am selben geografischen Standort zu bleiben. Wenn Sie jedoch Benutzer auf der ganzen Welt haben, kann es besser sein, einen Cluster dort einzurichten, wo sich Ihre Benutzer befinden, damit diese keine langen Wartezeiten beim Senden einer Anforderung an Ihre App haben.

**Gehen Sie wie folgt vor, um eine globale Lastausgleichsfunktion für mehrere Cluster einzurichten:**

1. [Erstellen Sie Cluster](cs_clusters.html#clusters) in mehreren Zonen oder Regionen.
2. Wenn Sie über mehrere VLANs für einen Cluster, mehrere Teilnetze in demselben VLAN oder einen Cluster mit mehreren Zonen verfügen, müssen Sie [VLAN-Spanning](/docs/infrastructure/vlans/vlan-spanning.html#vlan-spanning) für Ihr Konto für die IBM Cloud-Infrastruktur (SoftLayer) aktivieren, damit die Workerknoten in dem privaten Netz miteinander kommunizieren können. Um diese Aktion durchführen zu können, müssen Sie über die [Infrastrukturberechtigung](cs_users.html#infra_access) **Netz > VLAN-Spanning im Netz verwalten** verfügen oder Sie können den Kontoeigner bitte, diese zu aktivieren. Um zu prüfen, ob das VLAN-Spanning bereits aktiviert ist, verwenden Sie den [Befehl](/docs/containers/cs_cli_reference.html#cs_vlan_spanning_get) `ibmcloud ks vlan-spanning-get`. Wenn Sie {{site.data.keyword.BluDirectLink}} verwenden, müssen Sie stattdessen eine [ VRF-Funktion (Virtual Router Function)](/docs/infrastructure/direct-link/subnet-configuration.html#more-about-using-vrf) verwenden. Um VRF zu aktivieren, wenden Sie sich an Ihren Ansprechpartner für die IBM Cloud-Infrastruktur (SoftLayer).
3. Stellen Sie in jedem Cluster Ihre App mit einer [Lastausgleichsfunktion für Anwendungen (ALB)](cs_ingress.html#ingress_expose_public) oder einem [LoadBalancer-Service](cs_loadbalancer.html#config) bereit.
4. Listen Sie für jeden Cluster die öffentlichen IP-Adressen für Ihre ALBs oder LoadBalancer-Services auf.
   - Gehen Sie wie folgt vor, um die IP-Adresse aller öffentlichen aktivierten ALBs in Ihrem Cluster aufzulisten:
     ```
     ibmcloud ks albs --cluster <clustername_oder_-id>
     ```
     {: pre}

   - Gehen Sie wie folgt vor, um die IP-Adresse für den LoadBalancer-Service aufzulisten:
     ```
     kubectl describe service <mein_service>
     ```
     {: pre}

     Die IP-Adresse für **Load Balancer Ingress** ist die portierbare IP-Adresse, die dem LoadBalancer-Service zugewiesen wurde.

4.  Richten Sie eine globale Lastausgleichsfunktion ein, indem Sie {{site.data.keyword.Bluemix_notm}} Internet Services (CIS) verwenden oder eine eigene globale Lastausgleichsfunktion einrichten.

    **Gehen Sie wie folgt vor, um eine globale CIS-Lastausgleichsfunktion zu verwenden:**:
    1.  Richten Sie den Service ein, indem Sie die Schritte 1 bis 4 in der [Einführung in {{site.data.keyword.Bluemix_notm}} Internet Services (CIS)](/docs/infrastructure/cis/getting-started.html#getting-started-with-ibm-cloud-internet-services-cis-) ausführen.
        *  Die Schritte 1 bis 3 führen Sie durch die Bereitstellung der Serviceinstanz, das Hinzufügen Ihrer App-Domäne und die Konfiguration Ihrer Namensserver.
        * Schritt 4 führt Sie durch die Erstellung von DNS-Datensätzen. Erstellen Sie einen DNS-Datensatz für alle IP-Adressen der ALBs oder Lastausgleichsfunktionen, die Sie erfasst haben. Diese DNS-Datensätze ordnen Ihre App-Domäne allen Ihren Cluster-ALBs oder Lastausgleichsfunktionen zu und stellen sicher, dass Anforderungen an Ihre App-Domäne in einem Umlaufzyklus an Ihre Cluster weitergeleitet werden.
    2. [Fügen Sie Statusprüfungen](/docs/infrastructure/cis/glb-setup.html#add-a-health-check) für die ALBs oder die Lastausgleichsfunktionen hinzu. Sie können dieselbe Statusprüfung für die ALBs oder Lastausgleichsfunktionen in allen Clustern verwenden oder bestimmte Statusprüfungen erstellen, die für bestimmte Cluster verwendet werden.
    3. [Fügen Sie einen Ursprungspool](/docs/infrastructure/cis/glb-setup.html#add-a-pool) für jeden Cluster hinzu, indem Sie die ALB- oder Lastausgleichsfunktions-IPs des Clusters hinzufügen. Wenn Sie beispielsweise über drei Cluster mit jeweils zwei ALBs verfügen, erstellen Sie drei Ursprungspools, die jeweils zwei ALB-IP-Adressen aufweisen. Fügen Sie jedem Ursprungspool, den Sie erstellen, eine Statusprüfung hinzu.
    4. [Fügen Sie eine globale Lastausgleichsfunktion hinzu](/docs/infrastructure/cis/glb-setup.html#set-up-and-configure-your-load-balancers).

    **Gehen Sie wie folgt vor, um Ihre eigene globale Lastausgleichsfunktion zu verwenden:**:
    1. Konfigurieren Sie Ihre Domäne für die Weiterleitung des eingehenden Datenverkehrs an Ihre ALB oder LoadBalancer-Services, indem Sie die IP-Adressen aller öffentlichen aktivierten ALBs und LoadBalancer-Services in Ihre Domäne hinzufügen.
    2. Aktivieren Sie für jede IP-Adresse eine Ping-basierte Statusüberprüfung, damit Ihr DNS-Provider fehlerhafte IP-Adressen erkennen kann. Wird eine fehlerhafte IP-Adresse erkannt, wird der Datenverkehr nicht mehr an diese IP-Adresse weitergeleitet.

## Private Cluster
{: #private_clusters}

{{site.data.keyword.containerlong_notm}} richtet Ihren Cluster standardmäßig mit Zugriff auf ein privates VLAN und ein öffentliches VLAN ein. Das private VLAN bestimmt die private IP-Adresse, die dem jeweiligen Workerknoten zugeordnet ist. Diese Adresse stellt für jeden Workerknoten eine private Netzschnittstelle bereit. Das öffentliche VLAN ermöglicht es den Workerknoten, automatisch und sicher eine Verbindung zum Master herzustellen.

Wenn Sie den Cluster sperren möchten, um privaten Datenverkehr über das private VLAN zu ermöglichen, den öffentlichen Datenverkehr über das öffentliche VLAN aber zu blockieren, können Sie [den Cluster unter Verwendung von Calico-Netzrichtlinien vor öffentlichem Zugriff schützen](cs_network_cluster.html#both_vlans_private_services). Diese Calico-Netzrichtlinien vermeiden nicht die Kommunikation der Workerknoten mit dem Master. Sie können auch die Anfälligkeit für Sicherheitslücken im Cluster begrenzen, ohne den öffentlichen Datenverkehr durch das [Isolieren von Workloads im Netzbetrieb zu Edge-Workerknoten](cs_edge.html) zu sperren.

Wenn Sie einen Cluster erstellen möchten, der nur über Zugriff auf ein privates VLAN verfügt, können Sie einen privaten Einzelzonen- oder Mehrzonencluster erstellen. Wenn Ihre Workerknoten jedoch nur mit einem privaten VLAN verbunden sind, können die Workerknoten nicht automatisch eine Verbindung zum Master herstellen. Sie müssen eine Gateway-Appliance konfigurieren, um die Netzkonnektivität zwischen den Workerknoten und dem Master bereitzustellen.
**Hinweis**: Sie können einen Cluster, der mit einem öffentlichen und privaten VLAN verbunden ist, nicht in einen ausschließlich privaten Cluster konvertieren. Durch das Entfernen aller öffentlichen VLANs aus einem Cluster werden mehrere Clusterkomponenten gestoppt. Sie müssen einen neuen Cluster anhand der folgenden Schritte erstellen.

Gehen Sie wie folgt vor, wenn Sie einen Cluster erstellen möchten, der nur über Zugriff auf ein privates VLAN verfügt:

1.  Überprüfen Sie die Informationen in [Ausschließlich private Clusternetze planen](cs_network_cluster.html#private_vlan).
2.  Konfigurieren Sie Ihre Gateway-Appliance für die Netzkonnektivität. Beachten Sie, dass Sie [die erforderlichen Ports und IP-Adressen](cs_firewall.html#firewall_outbound) in Ihrer Firewall öffnen und [VLAN-Spanning für die Teilnetze aktivieren](cs_subnets.html#vra-routing) müssen.
3.  [Erstellen Sie einen Cluster unter Verwendung der CLI](cs_clusters.html#clusters_cli), indem Sie das Flag `--private-only` angeben.
4.  Wenn Sie eine App mithilfe eines NodePort-Service, eines Service für eine Lastausgleichsfunktion oder eines Ingress-Service in einem privaten Netz zugänglich machen möchten, lesen Sie die Informationen im Abschnitt [Nur private externe Netze für private VLAN-Konfiguration planen](cs_network_planning.html#private_vlan). Auf den Service kann nur über die private IP-Adresse zugegriffen werden und Sie müssen die Ports in Ihrer Firewall so konfigurieren, dass sie die private IP-Adresse verwenden.


## Worker-Pools und Workerknoten
{: #planning_worker_nodes}

Ein Kubernetes-Cluster besteht aus Workerknoten, die in Worker-Pools gruppiert sind und zentral vom Kubernetes-Master überwacht und verwaltet werden. Clusteradministratoren entscheiden, wie sie den Cluster aus Workerknoten einrichten, um sicherzustellen, dass den Clusterbenutzern alle Ressourcen für die Bereitstellung und Ausführung von Apps im Cluster zur Verfügung stehen.
{:shortdesc}

Wenn Sie einen Standardcluster erstellen, werden die Workerknoten mit denselben Speicher-, CPU- und Plattenspeicherspezifikationen (Typ) in Ihrer IBM Cloud-Infrastruktur (SoftLayer) in Ihrem Namen bestellt und dem Standard-Worker-Pool in Ihrem Cluster hinzugefügt. Jedem Workerknoten werden eine eindeutige Workerknoten-ID und ein Domänenname zugewiesen, die nach dem Erstellen des Clusters nicht geändert werden dürfen. Sie können zwischen virtuellen oder physischen Servern (Bare-Metal-Servern) wählen. Abhängig von dem ausgewählten Grad an Hardware-Isolation können virtuelle Workerknoten als gemeinsam genutzte oder als dedizierte Knoten eingerichtet werden. Wenn Sie Ihrem Cluster unterschiedliche Typen hinzufügen möchten, [erstellen Sie einen weiteren Worker-Pool](cs_cli_reference.html#cs_worker_pool_create).

Kubernetes beschränkt die maximale Anzahl von Workerknoten, die in einem Cluster vorhanden sein können. Weitere Informationen finden Sie unter [Worker node and pod quotas ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/setup/cluster-large/).



## Verfügbare Hardware für Workerknoten
{: #shared_dedicated_node}

Wenn Sie einen Standardcluster in {{site.data.keyword.Bluemix_notm}} erstellen, wählen Sie, ob Ihre Worker-Pools aus Workerknoten bestehen, die entweder physische Maschinen (Bare-Metal-Maschinen) sind oder die virtuelle Maschinen sind, die auf physischer Hardware ausgeführt werden. Sie wählen außerdem den Typ des Workerknotens oder die Kombination aus Speicher-, CPU- und anderen Maschinenspezifikationen (wie z. B. Plattenspeicher).
{:shortdesc}

![Hardwaresystemerweiterungen für Workerknoten in einem Standardcluster](images/cs_clusters_hardware.png)

Wenn Sie mehr als einen Typ des Workerknotens benötigen, müssen Sie für jeden Typ einen Worker-Pool erstellen. Wenn Sie einen kostenlosen Cluster erstellen, wird Ihr Workerknoten automatisch als gemeinsam genutzter, virtueller Knoten im Konto der IBM Cloud-Infrastruktur (SoftLayer) bereitgestellt. Berücksichtigen Sie bei Ihrer Planung [das Limit des Mindestschwellenwerts für den Workerknoten](#resource_limit_node) von 10 % der Gesamtspeicherkapazität.

Sie können Cluster mithilfe der [Konsolen-UI](cs_clusters.html#clusters_ui) oder mithilfe der [CLI](cs_clusters.html#clusters_cli) bereitstellen.

Wählen Sie eine der folgenden Optionen aus, um zu entscheiden, welchen Typ von Worker-Pool Sie wünschen.
* [Virtuelle Maschinen](#vm)
* [Physische Maschinen (Bare-Metal-Maschinen)](#bm)
* [SDS-Maschinen (Software-defined Storage)](#sds)

### Virtuelle Maschinen
{: #vm}

Virtuelle Maschinen bieten eine größere Flexibilität, schnellere Bereitstellungszeiten und mehr automatische Skalierbarkeitsfunktionen als Bare-Metal-Maschinen und sind zudem kostengünstiger. Sie können virtuelle Maschinen für die meisten allgemeinen Anwendungsfälle, wie Test- und Entwicklungsumgebungen, Staging- und Produktionsumgebungen, Mikroservices und Business-Apps, verwenden. Allerdings müssen bei der Leistung Kompromisse gemacht werden. Wenn Sie für RAM-, GPU- oder datenintensive Arbeitslasten eine Datenverarbeitung mit hoher Leistung benötigen, verwenden Sie [Bare-Metal-Maschinen](#bm).
{: shortdesc}

**Soll gemeinsam genutzte oder dedizierte Hardware verwendet werden?**</br>
Wenn Sie einen virtuellen Standardcluster erstellen, müssen Sie auswählen, ob die zugrunde liegende Hardware von mehreren {{site.data.keyword.IBM_notm}} Kunden gemeinsam genutzt werden kann (Multi-Tenant-Konfiguration) oder ob Sie die ausschließlich Ihnen vorbehaltene, dedizierte Nutzung vorziehen (Single-Tenant-Konfiguration).

* **In einer Multi-Tenant-Konfiguration mit gemeinsam genutzter Hardware**: Physische Ressourcen wie CPU und Speicher werden von allen virtuellen Maschinen, die auf derselben physischen Hardware bereitgestellt werden, gemeinsam genutzt. Um sicherzustellen, dass jede virtuelle Maschine unabhängig von anderen Maschinen ausgeführt werden kann, segmentiert ein VM-Monitor, d. h. eine Überwachungsfunktion für virtuelle Maschinen, die auch als Hypervisor bezeichnet wird, die physischen Ressourcen in isolierte Entitäten und ordnet diese einer virtuellen Maschine als dedizierte Ressourcen zu. Dies wird als Hypervisor-Isolation bezeichnet.
* **In einer Single-Tenant-Konfiguration mit dedizierter Hardware**: Die Nutzung aller physischen Ressourcen ist ausschließlich Ihnen vorbehalten. Sie können mehrere Workerknoten als virtuelle Maschinen auf demselben physischen Host bereitstellen. Ähnlich wie bei der Multi-Tenant-Konfiguration stellt der Hypervisor auch hier sicher, dass jeder Workerknoten seinen Anteil an den verfügbaren physischen Ressourcen erhält.

Gemeinsam genutzte Knoten sind in der Regel kostengünstiger als dedizierte Knoten, weil die Kosten für die ihnen zugrunde liegende Hardware von mehreren Kunden getragen werden. Bei der Entscheidungsfindung hinsichtlich gemeinsam genutzter Knoten versus dedizierter Knoten sollten Sie mit Ihrer Rechtsabteilung Rücksprache halten, um zu klären, welcher Grad an Infrastrukturisolation und Compliance für Ihre App-Umgebung erforderlich ist.

**Was sind die allgemeinen Features von VMs?**</br>
Virtuelle Maschinen verwenden lokale Platten anstelle von SAN (Storage Area Networking) für die Zuverlässigkeit. Zu den Vorteilen zählen ein höherer Durchsatz beim Serialisieren von Bytes für die lokale Festplatte und weniger Beeinträchtigungen des Dateisystems aufgrund von Netzausfällen. Jede VM bietet eine Netzgeschwindigkeit von 1000 Mb/s, 25 GB primären lokalen Plattenspeicher für das Dateisystem des Betriebssystems und 100 GB sekundären lokalen Plattenspeicher für Daten (wie die Containerlaufzeit und `kubelet`). Der lokale Speicher auf dem Workerknoten ist nur für die kurzfristige Verarbeitung vorgesehen; die primäre und die sekundäre Platte werden gelöscht, wenn Sie den Workerknoten aktualisieren oder erneut laden. Informationen zu persistenten Speicherlösungen finden Sie im Abschnitt [Persistenten Hochverfügbarkeitsspeicher planen](cs_storage_planning.html#storage_planning).

**Was passiert, wenn ich über veraltete `u1c`- oder `b1c`-Maschinentypen verfüge?**</br>
Zu Beginn der Verwendung von `u2c`- und `b2c`-Maschinentypen [aktualisieren Sie die Maschinentypen durch Hinzufügen von Workerknoten](cs_cluster_update.html#machine_type).

**Welche Typen sind bei virtuellen Maschinen verfügbar?**</br>
Maschinentypen variieren je nach Zone. Um die in Ihrer Zone verfügbaren Maschinentypen anzuzeigen, führen Sie den Befehl `ibmcloud ks machine-types <zone>` aus. Sie können außerdem die verfügbaren [Bare-Metal](#bm)- oder [SDS](#sds)-Maschinentypen ansehen.

<table>
<caption>Verfügbare virtuelle Maschinentypen in {{site.data.keyword.containerlong_notm}}.</caption>
<thead>
<th>Name und Anwendungsfall</th>
<th>Kerne/Speicher</th>
<th>Primäre/Sekundäre Platte</th>
<th>Netzgeschwindigkeit</th>
</thead>
<tbody>
<tr>
<td><strong>Virtuell, u2c.2x4</strong>: Verwenden Sie diese kompakte virtuelle Maschine für Schnelltests, Machbarkeitsnachweise und weitere leichte Workloads.</td>
<td>2/4 GB</td>
<td>25 GB/100 GB</td>
<td>1000 MB/s</td>
</tr>
<tr>
<td><strong>Virtuell, b2c.4x16</strong>: Wählen Sie diese ausgeglichene virtuelle Maschine für Tests und Entwicklung und weitere leichte Workloads.</td>
<td>4/16 GB</td>
<td>25 GB/100 GB</td>
<td>1000 MB/s</td>
</tr>
<tr>
<td><strong>Virtuell, b2c.16x64</strong>: Wählen Sie diese ausgeglichene virtuelle Maschine für mittlere Workloads aus.</td></td>
<td>16/64 GB</td>
<td>25 GB/100 GB</td>
<td>1000 MB/s</td>
</tr>
<tr>
<td><strong>Virtuell, b2c.32x128</strong>: Wählen Sie diese ausgeglichene virtuelle Maschine für mittlere bis große Workloads, wie eine Datenbank und eine dynamische Website mit vielen gleichzeitigen Benutzern, aus.</td></td>
<td>32/128 GB</td>
<td>25 GB/100 GB</td>
<td>1000 MB/s</td>
</tr>
<tr>
<td><strong>Virtuell, b2c.56x242</strong>: Wählen Sie diese ausgeglichene virtuelle Maschine für große Workloads, wie eine Datenbank und mehrere Apps mit vielen gleichzeitigen Benutzern, aus.</td></td>
<td>56/242 GB</td>
<td>25 GB/100 GB</td>
<td>1000 MB/s</td>
</tr>
<tr>
<td><strong>Virtuell, c2c.16x16</strong>: Verwenden Sie diesen Typ, wenn Sie eine gleichmäßige Verteilung der Rechenressourcen vom Workerknoten für geringe Workloads wünschen.</td></td>
<td>16 / 16 GB</td>
<td>25 GB/100 GB</td>
<td>1000 MB/s</td>
</tr><tr>
<td><strong>Virtuell, c2c.16x32</strong>: Verwenden Sie diesen Typ, wenn Sie ein 1:2-Verhältnis von CPU- und Speicherressourcen vom Workerknoten für geringe bis mittlere Workloads wünschen.</td></td>
<td>16 / 32 GB</td>
<td>25 GB/100 GB</td>
<td>1000 MB/s</td>
</tr><tr>
<td><strong>Virtuell, c2c.32x32</strong>: Verwenden Sie diesen Typ, wenn Sie eine gleichmäßige Verteilung der Rechenressourcen vom Workerknoten für mittlere Workloads wünschen.</td></td>
<td>32 GB/ 32 GB</td>
<td>25 GB/100 GB</td>
<td>1000 MB/s</td>
</tr><tr>
<td><strong>Virtuell, c2c.32x64</strong>: Verwenden Sie diesen Typ, wenn Sie ein 1:2-Verhältnis von CPU- und Speicherressourcen vom Workerknoten für mittlere Workloads wünschen.</td></td>
<td>32 GB/64 GB</td>
<td>25 GB/100 GB</td>
<td>1000 MB/s</td>
</tr>
</tbody>
</table>

### Physische Maschinen (Bare-Metal-Maschinen)
{: #bm}

Sie können Ihre Workerknoten als physischen Single-Tenant-Server bereitstellen, der auch als Bare-Metal-Server bezeichnet wird.
{: shortdesc}

**Wie unterscheiden sich Bare-Metal-Maschinen von VMs?**</br>
Mit Bare-Metal haben Sie direkten Zugriff auf die physischen Ressourcen auf der Maschine, wie z. B. Speicher oder CPU. Durch diese Konfiguration wird der Hypervisor der virtuellen Maschine entfernt, der physische Ressourcen zu virtuellen Maschinen zuordnet, die auf dem Host ausgeführt werden. Stattdessen sind alle Ressourcen der Bare-Metal-Maschine ausschließlich dem Worker gewidmet, also müssen Sie sich keine Sorgen machen, dass "lärmende Nachbarn" Ressourcen gemeinsam nutzen oder die Leistung verlangsamen. Physische Maschinentypen verfügen über einen größeren lokalen Speicher als virtuelle und einige verfügen zudem über RAID zur Steigerung der Datenverfügbarkeit. Der lokale Speicher auf dem Workerknoten ist nur für die kurzfristige Verarbeitung vorgesehen; die primäre und die sekundäre Platte werden gelöscht, wenn Sie den Workerknoten aktualisieren oder erneut laden. Informationen zu persistenten Speicherlösungen finden Sie im Abschnitt [Persistenten Hochverfügbarkeitsspeicher planen](cs_storage_planning.html#storage_planning).

**Bietet mir Bare-Metal mehr Möglichkeiten als VMs - abgesehen von besseren Spezifikationen für die Leistung?**</br>
Ja. Mit Bare-Metal haben Sie die Möglichkeit, Trusted Compute zu aktivieren, um Ihre Workerknoten auf Manipulation zu überprüfen. Wenn Sie Trusted Compute während der Clustererstellung nicht aktivieren, dies jedoch später nachholen möchten, können Sie den [Befehl](cs_cli_reference.html#cs_cluster_feature_enable) `ibmcloud ks feature-enable` verwenden. Nachdem Sie Trusted Compute aktiviert haben, können Sie es später nicht mehr inaktivieren. Sie können einen neuen Cluster ohne Trusted Compute erstellen. Weitere Informationen zur Funktionsweise von Trusted Compute während des Startprozesses für den Knoten finden Sie in [{{site.data.keyword.containerlong_notm}} mit Trusted Compute](cs_secure.html#trusted_compute). Trusted Compute ist nur auf Clustern mit Kubernetes Version 1.9 oder höher verfügbar, die bestimmte Bare-Metal-Maschinentypen aufweisen. Bei der Ausführung des [Befehls `ibmcloud ks machine-types <zone>`](cs_cli_reference.html#cs_machine_types) können Sie im Feld **Trustable** ablesen, welche Maschinen Trusted Compute unterstützen. Beispielsweise unterstützen die GPU-Typen `mgXc` Trusted Compute nicht.

**Bare-Metal scheint nur Vorteile zu bieten. Was sollte mich davon abhalten, diese Lösung zu bestellen?**</br>
Die Nutzung von Bare-Metal-Servern ist teurer als die Nutzung virtueller Server. Bare-Metal-Server eignen sich für Hochleistungsanwendungen, die mehr Ressourcen und mehr Hoststeuerung benötigen.

**Wichtig**: Die Abrechnung für Bare-Metal-Server erfolgt monatlich. Wenn Sie einen Bare-Metal-Server vor Monatsende stornieren, werden Ihnen die Kosten bis zum Ende dieses Monats belastet. Das Buchen und Stornieren von Bare-Metal-Servern ist ein manueller Prozess in Ihrem IBM Cloud-Infrastrukturkonto (SoftLayer). Er kann länger als einen Geschäftstag dauern.

**Welche Bare-Metal-Typen kann ich bestellen?**</br>
Maschinentypen variieren je nach Zone. Um die in Ihrer Zone verfügbaren Maschinentypen anzuzeigen, führen Sie den Befehl `ibmcloud ks machine-types <zone>` aus. Sie können außerdem die verfügbaren [VM](#vm)- oder [SDS](#sds)-Maschinentypen ansehen.

Bare-Metal-Maschinen sind für verschiedene Anwendungsfälle optimiert (z. B. für RAM-intensive, datenintensive oder GPU-intensive Workloads).

Wählen Sie einen Maschinentyp mit der richtigen Speicherkonfiguration aus, um Ihre Workload zu unterstützen. Einige Typen verfügen über eine Kombination aus den folgenden Platten und Speicherkonfigurationen. Beispielsweise können bestimmte Typen über eine SATA-Primärplatte mit einer unformatierten SSD-Sekundärplatte verfügen.

* **SATA**: Ein herkömmliches Magnetplattenspeichergerät, das häufig als primärer Datenträger des Workerknotens verwendet wird, auf dem das Dateisystem des Betriebssystems gespeichert ist.
* **SSD**: Ein Solid-State-Speichergerät für hohe Leistungsdaten.
* **Raw**: Das Speichergerät ist nicht formatiert und es steht die volle Kapazität zur Verfügung.
* **RAID**: Das Speichergerät verteilt die Daten für Redundanz und Leistung, abhängig von der jeweiligen RAID-Stufe. Die nutzbare Plattenkapazität variiert daher.


<table>
<caption>Verfügbare Bare-Metal-Maschinentypen in {{site.data.keyword.containerlong_notm}}.</caption>
<thead>
<th>Name und Anwendungsfall</th>
<th>Kerne/Speicher</th>
<th>Primäre/Sekundäre Platte</th>
<th>Netzgeschwindigkeit</th>
</thead>
<tbody>
<tr>
<td><strong>RAM-intensiv, Bare-Metal, mr1c.28x512</strong>: Maximieren Sie den verfügbaren RAM-Speicher für Ihre Workerknoten.</td>
<td>28/512 GB</td>
<td>2 TB SATA/960 GB SSD</td>
<td>10000 MB/s</td>
</tr>
<tr>
<td><strong>GPU, Bare-Metal, mg1c.16x128</strong>: Wählen Sie diesen Typ für rechenintensive Workloads, wie Datenverarbeitungen mit hoher Leistung, maschinelles Lernen oder 3D-Anwendungen, aus. Dieser Typ verfügt über eine physische Tesla K80-Karte mit zwei GPUs (Graphics Processing Units) pro Karte für insgesamt zwei GPUs.</td>
<td>16/128 GB</td>
<td>2 TB SATA/960 GB SSD</td>
<td>10000 MB/s</td>
</tr>
<tr>
<td><strong>GPU, Bare-Metal, mg1c.28x256</strong>: Wählen Sie diesen Typ für rechenintensiv Workloads, wie Datenverarbeitungen mit hoher Leistung, maschinelles Lernen oder 3D-Anwendungen, aus. Dieser Typ verfügt über zwei physische Tesla K80-Karten, die zwei GPUs (Graphics Processing Units) pro Karte für insgesamt vier GPUs aufweisen.</td>
<td>28/256 GB</td>
<td>2 TB SATA/960 GB SSD</td>
<td>10000 MB/s</td>
</tr>
<tr>
<td><strong>Datenintensiv, Bare-Metal, md1c.16x64.4x4tb</strong>: Verwenden Sie diesen Typ für einen beträchtlichen Teil des lokalen Plattenspeichers, einschließlich RAID zur Steigerung der Datenverfügbarkeit, für Workloads wie verteilte Dateisysteme, große Datenbanken und Big-Data-Analysen.</td>
<td>16/64 GB</td>
<td>2 x 2 TB RAID1/4 x 4 TB SATA RAID10</td>
<td>10000 MB/s</td>
</tr>
<tr>
<td><strong>Datenintensiv, Bare-Metal, md1c.28x512.4x4tb</strong>: Verwenden Sie diesen Typ für einen beträchtlichen Teil des lokalen Plattenspeichers, einschließlich RAID zur Steigerung der Datenverfügbarkeit, für Workloads wie verteilte Dateisysteme, große Datenbanken und Big-Data-Analysen.</td>
<td>28/512 GB</td>
<td>2 x 2 TB RAID1/4 x 4 TB SATA RAID10</td>
<td>10000 MB/s</td>
</tr>
<tr>
<td><strong>Ausgeglichen, Bare-Metal, mb1c.4x32</strong>: Verwenden Sie diesen Typ für ausgeglichene Workloads, für die mehr Ressourcen für die Datenverarbeitung benötigt werden, als virtuelle Maschinen bieten können.</td>
<td>4/32 GB</td>
<td>2 TB SATA/2 TB SATA</td>
<td>10000 MB/s</td>
</tr>
<tr>
<td><strong>Ausgeglichen, Bare-Metal, mb1c.16x64</strong>: Verwenden Sie diesen Typ für ausgeglichene Workloads, für die mehr Ressourcen für die Datenverarbeitung benötigt werden, als virtuelle Maschinen bieten können.</td>
<td>16/64 GB</td>
<td>2 TB SATA/960 GB SSD</td>
<td>10000 MB/s</td>
</tr>
<tr>
</tbody>
</table>

### SDS-Maschinen (Software-defined Storage)
{: #sds}

SDS-Typen (SDS = Software-Defined Storage) sind physische Maschinen, die mit einer zusätzlichen unformatierten Platten für den physischen lokalen Speicher bereitgestellt werden. Im Gegensatz zur primären und sekundären lokalen Platte werden diese unformatierten Platten beim Aktualisieren oder erneuten Laden eines Workerknotens nicht gelöscht. Da sich die Daten auf derselben Maschine wie der Rechenknoten befinden, eignen sich SDS-Maschinen für hohe Workloads.
{: shortdesc}

**Wann verwende ich SDS-Typen?**</br>
Normalerweise verwenden Sie SDS-Maschinen in den folgenden Fällen:
*  Wenn Sie ein SDS-Add-on für den Cluster verwenden, müssen Sie eine SDS-Maschine verwenden.
*  Wenn Ihre App ein [StatefulSet ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) ist, das lokalen Speicher voraussetzt, können Sie SDS-Maschinen verwenden und [lokale Kubernetes-PVs (Beta) ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/blog/2018/04/13/local-persistent-volumes-beta/) einrichten.
*  Möglicherweise haben Sie angepasste Apps oder Cluster-Add-ons, die SDS oder lokalen Speicher erfordern. Wenn Sie z. B. logDNA verwenden möchten, müssen Sie einen SDS-Maschinentyp verwenden.

Informationen zu weiteren Speicherlösungen finden Sie im Abschnitt [Persistenten Hochverfügbarkeitsspeicher planen](cs_storage_planning.html#storage_planning).

**Welche SDS-Typen kann ich bestellen?**</br>
Maschinentypen variieren je nach Zone. Um die in Ihrer Zone verfügbaren Maschinentypen anzuzeigen, führen Sie den Befehl `ibmcloud ks machine-types <zone>` aus. Sie können außerdem die verfügbaren [Bare-Metal](#bm)- oder [VM](#vm)-Maschinentypen ansehen.

Wählen Sie einen Maschinentyp mit der richtigen Speicherkonfiguration aus, um Ihre Workload zu unterstützen. Einige Typen verfügen über eine Kombination aus den folgenden Platten und Speicherkonfigurationen. Beispielsweise können bestimmte Typen über eine SATA-Primärplatte mit einer unformatierten SSD-Sekundärplatte verfügen.

* **SATA**: Ein herkömmliches Magnetplattenspeichergerät, das häufig als primärer Datenträger des Workerknotens verwendet wird, auf dem das Dateisystem des Betriebssystems gespeichert ist.
* **SSD**: Ein Solid-State-Speichergerät für hohe Leistungsdaten.
* **Raw**: Das Speichergerät ist nicht formatiert und es steht die volle Kapazität zur Verfügung.
* **RAID**: Das Speichergerät verteilt die Daten für Redundanz und Leistung, abhängig von der jeweiligen RAID-Stufe. Die nutzbare Plattenkapazität variiert daher.


<table>
<caption>Verfügbare SDS-Maschinentypen in {{site.data.keyword.containerlong_notm}}.</caption>
<thead>
<th>Name und Anwendungsfall</th>
<th>Kerne/Speicher</th>
<th>Primäre/Sekundäre Platte</th>
<th>Zusätzliche unformatierte Platten</th>
<th>Netzgeschwindigkeit</th>
</thead>
<tbody>
<tr>
<td><strong>Bare-Metal mit SDS, ms2c.4x32.1.9tb.ssd</strong>: Wenn Sie zusätzlichen lokalen Speicher zur Leistungssteigerung benötigen, verwenden Sie diesen Typ mit hoher Plattenkapazität, der SDS (Software-Defined Storage) unterstützt.</td>
<td>4/32 GB</td>
<td>2 TB SATA/960 GB SSD</td>
<td>1,9 TB Raw SSD</td>
<td>10000 MB/s</td>
</tr>
<tr>
<td><strong>Bare-Metal mit SDS, ms2c.16x64.1.9tb.ssd</strong>: Wenn Sie zusätzlichen lokalen Speicher zur Leistungssteigerung benötigen, verwenden Sie diesen Typ mit hoher Plattenkapazität, der SDS (Software-Defined Storage) unterstützt.</td>
<td>16/64 GB</td>
<td>2 TB SATA/960 GB SSD</td>
<td>1,9 TB Raw SSD</td>
<td>10000 MB/s</td>
</tr>
<tr>
<td><strong>Bare-Metal mit SDS, ms2c.28x256.3.8tb.ssd</strong>: Wenn Sie zusätzlichen lokalen Speicher zur Leistungssteigerung benötigen, verwenden Sie diesen Typ mit hoher Plattenkapazität, der SDS (Software-defined Storage) unterstützt.</td>
<td>28/256 GB</td>
<td>2 TB SATA/1,9 TB SSD</td>
<td>3,8 TB Raw SSD</td>
<td>10000 MB/s</td>
</tr>
<tr>
<td><strong>Bare-Metal mit SDS, ms2c.28x512.4x3.8tb.ssd</strong>: Wenn Sie zusätzlichen lokalen Speicher zur Leistungssteigerung benötigen, verwenden Sie diesen Typ mit hoher Plattenkapazität, der SDS (Software-defined Storage) unterstützt.</td>
<td>28/512 GB</td>
<td>2 TB SATA/1,9 TB SSD</td>
<td>4 Platten, 3,8 TB Raw SSD</td>
<td>10000 MB/s</td>
</tr>
</tbody>
</table>

## Speicherbegrenzung für Workerknoten
{: #resource_limit_node}

{{site.data.keyword.containerlong_notm}} legt für jeden Workerknoten eine Speicherbegrenzung fest. Wenn Pods, die auf einem Workerknoten ausgeführt werden, diese Speicherbegrenzung überschreiten, werden die Pods entfernt. In Kubernetes wird diese Begrenzung als [harte Räumungsschwelle ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/tasks/administer-cluster/out-of-resource/#hard-eviction-thresholds) bezeichnet.
{:shortdesc}

Wenn Ihre Pods häufig entfernt werden, fügen Sie zusätzliche Workerknoten zu Ihrem Cluster hinzu oder legen Sie [Ressourcenbegrenzungen ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#resource-requests-and-limits-of-pod-and-container) für die Pods fest.

**Jede Maschine hat einen Mindestschwellenwert, der 10 % der Gesamtspeicherkapazität entspricht**. Wenn weniger Speicher auf dem Workerknoten als der zulässige Mindestschwellenwert verfügbar ist, entfernt Kubernetes den Pod sofort. Wenn ein anderer Workerknoten verfügbar ist, wird die Planung für den Pod auf diesem Workerknoten neu erstellt. Wenn Sie beispielsweise mit einer virtuellen Maschine des Typs `b2c.4x16` arbeiten, ist die Gesamtspeicherkapazität dieser Maschine 16 GB. Wenn weniger als 1600 MB (10 %) Speicher verfügbar ist, können neue Pods nicht auf diesem Workerknoten terminiert werden, sondern werden auf einem anderen Workerknoten terminiert. Wenn kein anderer Workerknoten verfügbar ist, können die neuen Workerknoten nicht terminiert werden.

Um zu sehen, wie viel Speicher auf dem Workerknoten belegt ist, führen Sie [`kubectl top node ` ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/reference/kubectl/overview/#top) aus.

## Automatische Wiederherstellung für Ihren Workerknoten
{: #autorecovery}

Kritische Komponenten - wie z. B. `containerd`, `kubelet`, `kube-proxy` und `calico` - müssen richtig ausgeführt werden, damit die Kubernetes-Workerknoten einen einwandfreiem Zustand aufweisen. Im Laufe der Zeit können diese Komponenten kaputt gehen und ihre Workerknoten möglicherweise in einem nicht funktionsbereiten Zustand versetzen. Nicht funktionsbereite Workerknoten verringern die Gesamtkapazität des Clusters und können zu Ausfallzeiten für Ihre App führen.
{:shortdesc}

Sie können [Statusprüfungen für Ihre Workerknoten konfigurieren und die automatische Wiederherstellung aktiveren](cs_health.html#autorecovery). Wenn die automatische Wiederherstellung basierend auf den konfigurierten Prüfungen einen nicht ordnungsgemäß funktionierenden Workerknoten erkennt, löst das System eine Korrekturmaßnahme, wie das erneute Laden des Betriebssystems, auf dem Workerknoten aus. Weitere Informationen zur Funktionsweise der automatischen Wiederherstellung finden Sie im [Blogbeitrag zur automatischen Wiederherstellung![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2017/12/autorecovery-utilizes-consistent-hashing-high-availability/).

<br />

