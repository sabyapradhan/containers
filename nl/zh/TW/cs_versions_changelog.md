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



# 版本變更日誌
{: #changelog}

檢視可供 {{site.data.keyword.containerlong}} Kubernetes 叢集使用之主要、次要及修補程式更新的版本變更資訊。變更包含 Kubernetes 及 {{site.data.keyword.Bluemix_notm}} Provider 元件的更新。
{:shortdesc}

如需主要、次要和修補程式版本以及次要版本間之移轉動作的相關資訊，請參閱 [Kubernetes 版本](cs_versions.html)。
{: tip}

如需自舊版以來的變更相關資訊，請參閱下列變更日誌。
-  1.11 版[變更日誌](#111_changelog)。
-  1.10 版[變更日誌](#110_changelog)。
-  1.9 版[變更日誌](#19_changelog)。
-  已淘汰或不受支援版本之變更日誌的[保存檔](#changelog_archive)。

**附註**：部分變更日誌適用於_工作者節點修正套件_，而且僅適用於工作者節點。您必須[套用這些修補程式](cs_cli_reference.html#cs_worker_update)，以確保工作者節點的安全規範。其他變更日誌適用於_主節點修正套件_，而且僅適用於叢集主節點。可能未自動套用主要修正套件。您可以選擇[手動套用它們](cs_cli_reference.html#cs_cluster_update)。如需修補程式類型的相關資訊，請參閱[更新類型](cs_versions.html#update_types)。

</br>

## 1.11 版變更日誌
{: #111_changelog}

檢閱下列變更。


### 主節點修正套件 1.11.3_1527（2018 年 10 月 15 日發行）的變更日誌
{: #1113_1527}

<table summary="自 1.11.3_1524 版以來進行的變更">
<caption>自 1.11.3_1524 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>已修正 `calico-node` 容器備妥探測，以更適當的處理節點失效。</td>
</tr>
<tr>
<td>叢集更新</td>
<td>N/A</td>
<td>N/A</td>
<td>已修正從不受支援的版本更新主節點時的叢集附加程式更新問題。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.11.3_1525（2018 年 10 月 10 日發行）的變更日誌
{: #1113_1525}

<table summary="自 1.11.3_1524 版以來進行的變更">
<caption>自 1.11.3_1524 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>核心</td>
<td>4.4.0-133</td>
<td>4.4.0-137</td>
<td>已更新工作者節點映像檔與 [CVE-2018-14633、CVE-2018-17182 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-137.163/changelog) 的核心更新。</td>
</tr>
<tr>
<td>非作用中階段作業逾時</td>
<td>N/A</td>
<td>N/A</td>
<td>基於合規性，將非作用中階段作業逾時設為 5 分鐘。</td>
</tr>
</tbody>
</table>


### 1.11.3_1524（2018 年 10 月 2 日發行）的變更日誌
{: #1113_1524}

<table summary="自 1.11.3_1521 版以來進行的變更">
<caption>自 1.11.3_1521 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>containerd</td>
<td>1.1.3</td>
<td>1.1.4</td>
<td>請參閱 [containerd 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/containerd/containerd/releases/tag/v1.1.4)。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.11.3-91 版</td>
<td>1.11.3-100 版</td>
<td>已更新負載平衡器錯誤訊息中的文件鏈結。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間類別</td>
<td>N/A</td>
<td>N/A</td>
<td>已移除 IBM 檔案儲存空間類別中的重複 `reclaimPolicy` 參數。<br><br>
此外，現在，當您更新叢集主節點時，預設 IBM 檔案儲存空間類別會維持不變。如果您要變更預設儲存空間類別，請執行 `kubectl patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`，並將 `<storageclass>` 取代為儲存空間類別的名稱。</td>
</tr>
</tbody>
</table>

### 1.11.3_1521（2018 年 9 月 20 日發行）的變更日誌
{: #1113_1521}

<table summary="自 1.11.2_1516 版以來進行的變更">
<caption>自 1.11.2_1516 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.11.2-71 版</td>
<td>1.11.3-91 版</td>
<td>已更新為支援 Kubernetes 1.11.3 版。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間類別</td>
<td>N/A</td>
<td>N/A</td>
<td>已移除 IBM 檔案儲存空間類別中的 `mountOptions`，以使用工作者節點所提供的預設值。<br><br>
此外，現在，當您更新叢集主節點時，預設 IBM 檔案儲存空間類別會維持 `ibmc-file-bronze`。如果您要變更預設儲存空間類別，請執行 `kubectl patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`，並將 `<storageclass>` 取代為儲存空間類別的名稱。</td>
</tr>
<tr>
<td>金鑰管理服務提供者</td>
<td>N/A</td>
<td>N/A</td>
<td>已新增在叢集中使用 Kubernetes 金鑰管理服務 (KMS) 提供者的能力，以支援 {{site.data.keyword.keymanagementservicefull}}。當您[在叢集中啟用 {{site.data.keyword.keymanagementserviceshort}}](cs_encrypt.html#keyprotect) 時，會加密您的所有 Kubernetes 密碼。</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>1.11.2 版</td>
<td>1.11.3 版</td>
<td>請參閱 [Kubernetes 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.11.3)。</td>
</tr>
<tr>
<td>Kubernetes DNS Autoscaler</td>
<td>1.1.2-r2</td>
<td>1.2.0</td>
<td>請參閱 [Kubernetes DNS Autoscaler 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes-incubator/cluster-proportional-autoscaler/releases/tag/1.2.0)。</td>
</tr>
<tr>
<td>日誌循環</td>
<td>N/A</td>
<td>N/A</td>
<td>已切換成使用 `systemd` 計時器，而非 `cronjobs`，以防止 `logrotate` 在未於 90 天內重新載入或更新的工作者節點上失敗。**附註**：在此次要版本的所有舊版中，Cron 工作失敗之後會填滿主要磁碟，因為日誌不會循環。在工作者節點作用 90 天但未進行更新或重新載入之後，Cron 工作就會失敗。如果日誌填滿整個主要磁碟，則工作者節點會進入失敗狀態。使用 `ibmcloud ks worker-reload` [指令](cs_cli_reference.html#cs_worker_reload)或 `ibmcloud ks worker-update` [指令](cs_cli_reference.html#cs_worker_update)，即可修正工作者節點。</td>
</tr>
<tr>
<td>root 密碼有效期限</td>
<td>N/A</td>
<td>N/A</td>
<td>基於合規性，工作者節點的 root 密碼會在 90 天後到期。如果您的自動化工具需要以 root 身分登入工作者節點，或依賴以 root 身分執行的 Cron 工作，則可以登入工作者節點並執行 `chage -M -1 root` 來停用密碼有效期限。**附註**：如果您的安全規範需求可避免以 root 身分執行或移除密碼有效期限，則請不要停用有效期限。相反地，您可以至少每 90 天[更新](cs_cli_reference.html#cs_worker_update)或[重新載入](cs_cli_reference.html#cs_worker_reload)工作者節點一次。</td>
</tr>
<tr>
<td>工作者節點運行環境元件（`kubelet`、`kube-proxy`、`containerd`）</td>
<td>N/A</td>
<td>N/A</td>
<td>已移除主要磁碟上的運行環境元件的相依關係。主要磁碟滿載時，此加強功能可避免工作者節點失敗。</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/A</td>
<td>N/A</td>
<td>定期清除暫時性裝載裝置，以防止它們變成無界限。此動作解決 [Kubernetes 問題 57345 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/issues/57345)。</td>
</tr>
</tbody>
</table>

### 1.11.2_1516（2018 年 9 月 4 日發行）的變更日誌
{: #1112_1516}

<table summary="自 1.11.2_1514 版以來進行的變更">
<caption>自 1.11.2_1514 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>3.1.3 版</td>
<td>3.2.1 版</td>
<td>請參閱 [Calico 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.projectcalico.org/v3.2/releases/#v321)。</td>
</tr>
<tr>
<td>containerd</td>
<td>1.1.2</td>
<td>1.1.3</td>
<td>請參閱 [`containerd` 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/containerd/containerd/releases/tag/v1.1.3)。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.11.2-60 版</td>
<td>1.11.2-71 版</td>
<td>已變更雲端提供者配置，可更恰當地處理 `externalTrafficPolicy` 設為 `local` 之負載平衡器服務的更新。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間外掛程式配置</td>
<td>N/A</td>
<td>N/A</td>
<td>已從 IBM 所提供檔案儲存空間類別的裝載選項中移除預設 NFS 版本。主機的作業系統現在會與 IBM Cloud 基礎架構 (SoftLayer) NFS 伺服器協議 NFS 版本。若要手動設定特定的 NFS 版本，或變更主機作業系統所協議 PV 的 NFS 版本，請參閱[變更預設 NFS 版本](cs_storage_file.html#nfs_version_class)。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.11.2_1514（2018 年 8 月 23 日發行）的變更日誌
{: #1112_1514}

<table summary="自 1.11.2_1513 版以來進行的變更">
<caption>自 1.11.2_1513 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>已更新 `systemd` 來修正 `cgroup` 洩漏。</td>
</tr>
<tr>
<td>核心</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>已更新工作者節點映像檔與 [CVE-2018-3620、CVE-2018-3646 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://usn.ubuntu.com/3741-1/) 的核心更新。</td>
</tr>
</tbody>
</table>

### 1.11.2_1513（2018 年 8 月 14 日發行）的變更日誌
{: #1112_1513}

<table summary="自 1.10.5_1518 版以來進行的變更">
<caption>自 1.10.5_1518 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>containerd</td>
<td>N/A</td>
<td>1.1.2</td>
<td>`containerd` 會將 Docker 取代為 Kubernetes 的新容器運行環境。請參閱 [`containerd` 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/containerd/containerd/releases/tag/v1.1.2)。如需您必須採取的動作，請參閱[移轉至 `containerd` 作為容器運行環境](cs_versions.html#containerd)。</td>
</tr>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>`containerd` 會將 Docker 取代為 Kubernetes 的新容器運行環境，來加強效能。如需您必須採取的動作，請參閱[移轉至 `containerd` 作為容器運行環境](cs_versions.html#containerd)。</td>
</tr>
<tr>
<td>etcd</td>
<td>3.2.14 版</td>
<td>3.2.18 版</td>
<td>請參閱 [etcd 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/coreos/etcd/releases/v3.2.18)。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.10.5-118 版</td>
<td>1.11.2-60 版</td>
<td>已更新為支援 Kubernetes 1.11 版。此外，負載平衡器 Pod 現在使用新的 `ibm-app-cluster-critical` Pod 優先順序類別。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間外掛程式</td>
<td>334</td>
<td>338</td>
<td>已將 `incubator` 版本更新為 1.8。檔案儲存空間會佈建給您選取的特定區域。除非您使用多區域叢集，並且需要[新增地區及區域標籤](cs_storage_basics.html#multizone)，否則無法更新現有（靜態）PV 實例標籤。</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>1.10.5 版</td>
<td>1.11.2 版</td>
<td>請參閱 [Kubernetes 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.11.2)。</td>
</tr>
<tr>
<td>Kubernetes 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>已更新叢集 Kubernetes API 伺服器的 OpenID Connect 配置，以支援 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 存取群組。已針對叢集的 Kubernetes API 伺服器將 `Priority` 新增至 `--enable-admission-plugins` 選項，並已將叢集配置為支援 Pod 優先順序。如需相關資訊，請參閱：<ul><li>[IAM 存取群組](cs_users.html#rbac)</li>
<li>[配置 Pod 優先順序](cs_pod_priority.html#pod_priority)</li></ul></td>
</tr>
<tr>
<td>Kubernetes Heapster</td>
<td>1.5.2 版</td>
<td>1.5.4 版</td>
<td>已增加 `heapster-nanny` 容器的資源限制。請參閱 [Kubernetes Heapster 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/heapster/releases/tag/v1.5.4)。</td>
</tr>
<tr>
<td>記載配置</td>
<td>N/A</td>
<td>N/A</td>
<td>容器日誌目錄現在是 `/var/log/pods/`，而非前一個 `/var/lib/docker/containers/`。</td>
</tr>
</tbody>
</table>

<br />


## 1.10 版變更日誌
{: #110_changelog}

檢閱下列變更。

### 主節點修正套件 1.10.8_1527（2018 年 10 月 15 日發行）的變更日誌
{: #1108_1527}

<table summary="自 1.10.8_1527 版以來進行的變更">
<caption>自 1.10.8_1527 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>已修正 `calico-node` 容器備妥探測，以更適當的處理節點失效。</td>
</tr>
<tr>
<td>叢集更新</td>
<td>N/A</td>
<td>N/A</td>
<td>已修正從不受支援的版本更新主節點時的叢集附加程式更新問題。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.10.8_1525（2018 年 10 月 10 日發行）的變更日誌
{: #1108_1525}

<table summary="自 1.10.8_1527 版以來進行的變更">
<caption>自 1.10.8_1527 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>核心</td>
<td>4.4.0-133</td>
<td>4.4.0-137</td>
<td>已更新工作者節點映像檔與 [CVE-2018-14633、CVE-2018-17182 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-137.163/changelog) 的核心更新。</td>
</tr>
<tr>
<td>非作用中階段作業逾時</td>
<td>N/A</td>
<td>N/A</td>
<td>基於合規性，將非作用中階段作業逾時設為 5 分鐘。</td>
</tr>
</tbody>
</table>


### 1.10.8_1524（2018 年 10 月 2 日發行）的變更日誌
{: #1108_1524}

<table summary="自 1.10.7_1520 版以來進行的變更">
<caption>自 1.10.7_1520 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>金鑰管理服務提供者</td>
<td>N/A</td>
<td>N/A</td>
<td>已新增在叢集中使用 Kubernetes 金鑰管理服務 (KMS) 提供者的能力，以支援 {{site.data.keyword.keymanagementservicefull}}。當您[在叢集中啟用 {{site.data.keyword.keymanagementserviceshort}}](cs_encrypt.html#keyprotect) 時，會加密您的所有 Kubernetes 密碼。</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>1.10.7 版</td>
<td>1.10.8 版</td>
<td>請參閱 [Kubernetes 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.8)。</td>
</tr>
<tr>
<td>Kubernetes DNS Autoscaler</td>
<td>1.1.2-r2</td>
<td>1.2.0</td>
<td>請參閱 [Kubernetes DNS Autoscaler 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes-incubator/cluster-proportional-autoscaler/releases/tag/1.2.0)。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.10.7-146 版</td>
<td>1.10.8-172 版</td>
<td>已更新為支援 Kubernetes 1.10.8 版。此外，已更新負載平衡器錯誤訊息中的文件鏈結。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間類別</td>
<td>N/A</td>
<td>N/A</td>
<td>已移除 IBM 檔案儲存空間類別中的 `mountOptions`，以使用工作者節點所提供的預設值。已移除 IBM 檔案儲存空間類別中的重複 `reclaimPolicy` 參數。<br><br>
此外，現在，當您更新叢集主節點時，預設 IBM 檔案儲存空間類別會維持不變。如果您要變更預設儲存空間類別，請執行 `kubectl patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`，並將 `<storageclass>` 取代為儲存空間類別的名稱。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.10.7_1521（2018 年 9 月 20 日發行）的變更日誌
{: #1107_1521}

<table summary="自 1.10.7_1520 版以來進行的變更">
<caption>自 1.10.7_1520 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>日誌循環</td>
<td>N/A</td>
<td>N/A</td>
<td>已切換成使用 `systemd` 計時器，而非 `cronjobs`，以防止 `logrotate` 在未於 90 天內重新載入或更新的工作者節點上失敗。**附註**：在此次要版本的所有舊版中，Cron 工作失敗之後會填滿主要磁碟，因為日誌不會循環。在工作者節點作用 90 天但未進行更新或重新載入之後，Cron 工作就會失敗。如果日誌填滿整個主要磁碟，則工作者節點會進入失敗狀態。使用 `ibmcloud ks worker-reload` [指令](cs_cli_reference.html#cs_worker_reload)或 `ibmcloud ks worker-update` [指令](cs_cli_reference.html#cs_worker_update)，即可修正工作者節點。</td>
</tr>
<tr>
<td>工作者節點運行環境元件（`kubelet`、`kube-proxy`、`docker`）</td>
<td>N/A</td>
<td>N/A</td>
<td>已移除主要磁碟上的運行環境元件的相依關係。主要磁碟滿載時，此加強功能可避免工作者節點失敗。</td>
</tr>
<tr>
<td>root 密碼有效期限</td>
<td>N/A</td>
<td>N/A</td>
<td>基於合規性，工作者節點的 root 密碼會在 90 天後到期。如果您的自動化工具需要以 root 身分登入工作者節點，或依賴以 root 身分執行的 Cron 工作，則可以登入工作者節點並執行 `chage -M -1 root` 來停用密碼有效期限。**附註**：如果您的安全規範需求可避免以 root 身分執行或移除密碼有效期限，則請不要停用有效期限。相反地，您可以至少每 90 天[更新](cs_cli_reference.html#cs_worker_update)或[重新載入](cs_cli_reference.html#cs_worker_reload)工作者節點一次。</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/A</td>
<td>N/A</td>
<td>定期清除暫時性裝載裝置，以防止它們變成無界限。此動作解決 [Kubernetes 問題 57345 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/issues/57345)。</td>
</tr>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>已停用預設 Docker 橋接器，因此 `172.17.0.0/16` IP 範圍現在用於專用路徑。如果您依賴直接在主機上執行 `docker` 指令或使用可裝載 Docker Socket 的 Pod 以在工作者節點中建置 Docker 容器，則請從下列選項中進行選擇。<ul><li>若要確保建置容器時的外部網路連線，請執行 `docker build . --network host`。</li>
<li>若要明確建立要在建置容器時使用的網路，請執行 `docker network create`，然後使用此網路。</li></ul>
**附註**：與 Docker Socket 或 Docker 具有直接相依關係嗎？[移轉至 `containerd`（而非 `docker`）作為容器運行環境](cs_versions.html#containerd)，因此您的叢集已準備好要執行 Kubernetes 1.11 版或更新版本。</td>
</tr>
</tbody>
</table>

### 1.10.7_1520（2018 年 9 月 4 日發行）的變更日誌
{: #1107_1520}

<table summary="自 1.10.5_1519 版以來進行的變更">
<caption>自 1.10.5_1519 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>3.1.3 版</td>
<td>3.2.1 版</td>
<td>請參閱 Calico [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.projectcalico.org/v3.2/releases/#v321)。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.10.5-118 版</td>
<td>1.10.7-146 版</td>
<td>已更新為支援 Kubernetes 1.10.7 版。此外，已變更雲端提供者配置，可更恰當地處理 `externalTrafficPolicy` 設為 `local` 之負載平衡器服務的更新。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間外掛程式</td>
<td>334</td>
<td>338</td>
<td>已將 incubator 版本更新為 1.8。檔案儲存空間會佈建給您選取的特定區域。除非您使用多區域叢集，並且需要新增地區及區域標籤，否則無法更新現有（靜態）PV 實例的標籤。<br><br> 已從 IBM 所提供檔案儲存空間類別的裝載選項中移除預設 NFS 版本。主機的作業系統現在會與 IBM Cloud 基礎架構 (SoftLayer) NFS 伺服器協議 NFS 版本。若要手動設定特定的 NFS 版本，或變更主機作業系統所協議 PV 的 NFS 版本，請參閱[變更預設 NFS 版本](cs_storage_file.html#nfs_version_class)。</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>1.10.5 版</td>
<td>1.10.7 版</td>
<td>請參閱 Kubernetes [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.7)。</td>
</tr>
<tr>
<td>Kubernetes Heapster 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>已增加 `heapster-nanny` 容器的資源限制。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.10.5_1519（2018 年 8 月 23 日發行）的變更日誌
{: #1105_1519}

<table summary="自 1.10.5_1518 版以來進行的變更">
<caption>自 1.10.5_1518 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>已更新 `systemd` 來修正 `cgroup` 洩漏。</td>
</tr>
<tr>
<td>核心</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>已更新工作者節點映像檔與 [CVE-2018-3620、CVE-2018-3646 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://usn.ubuntu.com/3741-1/) 的核心更新。</td>
</tr>
</tbody>
</table>


### 工作者節點修正套件 1.10.5_1518（2018 年 8 月 13 日發行）的變更日誌
{: #1105_1518}

<table summary="自 1.10.5_1517 版以來進行的變更">
<caption>自 1.10.5_1517 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Ubuntu 套件</td>
<td>N/A</td>
<td>N/A</td>
<td>已安裝 Ubuntu 套件的更新。</td>
</tr>
</tbody>
</table>

### 1.10.5_1517（2018 年 7 月 27 日發行）的變更日誌
{: #1105_1517}

<table summary="自 1.10.3_1514 版以來進行的變更">
<caption>自 1.10.3_1514 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>3.1.1 版</td>
<td>3.1.3 版</td>
<td>請參閱 Calico [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.projectcalico.org/v3.1/releases/#v313)。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.10.3-85 版</td>
<td>1.10.5-118 版</td>
<td>已更新為支援 Kubernetes 1.10.5 版。此外，LoadBalancer 服務 `create failure` 事件現在包括所有可攜式子網路錯誤。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間外掛程式</td>
<td>320</td>
<td>334</td>
<td>已將持續性磁區建立的逾時從 15 分鐘增加至 30 分鐘。已將預設計費類型變更為 `hourly`。已將裝載選項新增至預先定義的儲存空間類別。在 IBM Cloud 基礎架構 (SoftLayer) 帳戶的 NFS 檔案儲存空間實例中，已將 **Notes** 欄位變更為 JSON 格式，並已新增 PV 部署至其中的 Kubernetes 名間空間。為了支援多區域叢集，已將區域及地區標籤新增至持續性磁區。</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>1.10.3 版</td>
<td>1.10.5 版</td>
<td>請參閱 Kubernetes [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.5)。</td>
</tr>
<tr>
<td>核心</td>
<td>N/A</td>
<td>N/A</td>
<td>對高效能網路工作負載的工作者節點網路設定做出少量改善。</td>
</tr>
<tr>
<td>OpenVPN 用戶端</td>
<td>N/A</td>
<td>N/A</td>
<td>在 `kube-system` 名稱空間中執行的 OpenVPN 用戶端 `vpn` 部署，現在是由 Kubernetes `addon-manager` 管理。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.10.3_1514（2018 年 7 月 3 日發行）的變更日誌
{: #1103_1514}

<table summary="自 1.10.3_1513 版以來進行的變更">
<caption>自 1.10.3_1513 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>核心</td>
<td>N/A</td>
<td>N/A</td>
<td>已最佳化高效能網路工作負載的 `sysctl`。</td>
</tr>
</tbody>
</table>


### 工作者節點修正套件 1.10.3_1513（2018 年 6 月 21 日發行）的變更日誌
{: #1103_1513}

<table summary="自 1.10.3_1512 版以來進行的變更">
<caption>自 1.10.3_1512 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>對於非加密的機型，當重新載入或更新工作者節點時，會取得全新的檔案系統來清理次要磁碟。</td>
</tr>
</tbody>
</table>

### 1.10.3_1512（2018 年 6 月 12 日發行）的變更日誌
{: #1103_1512}

<table summary="自 1.10.3_1510 版以來進行的變更">
<caption>自 1.10.1_1510 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>1.10.1 版</td>
<td>1.10.3 版</td>
<td>請參閱 Kubernetes [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.3)。</td>
</tr>
<tr>
<td>Kubernetes 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>已針對叢集的 Kubernetes API 伺服器將 `PodSecurityPolicy` 新增至 `--enable-admission-plugins` 選項，並已將叢集配置為支援 Pod 安全政策。如需相關資訊，請參閱[配置 Pod 安全原則](cs_psp.html)。</td>
</tr>
<tr>
<td>Kubelet 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>啟用 `--authentication-token-webhook` 選項，支援 API 載送及服務帳戶記號，以對 `kubelet` HTTPS 端點進行鑑別。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.10.1-52 版</td>
<td>1.10.3-85 版</td>
<td>已更新為支援 Kubernetes 1.10.3 版。</td>
</tr>
<tr>
<td>OpenVPN 用戶端</td>
<td>N/A</td>
<td>N/A</td>
<td>已將 `livenessProbe` 新增至 `kube-system` 名稱空間中執行的 OpenVPN 用戶端 `vpn` 部署。</td>
</tr>
<tr>
<td>核心更新</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>新的工作者節點映像檔與 [CVE-2018-3639 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639) 的核心更新。</td>
</tr>
</tbody>
</table>



### 工作者節點修正套件 1.10.1_1510（2018 年 5 月 18 日發行）的變更日誌
{: #1101_1510}

<table summary="自 1.10.1_1509 版以來進行的變更">
<caption>自 1.10.1_1509 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>修正以處理您使用區塊儲存空間外掛程式時發生的錯誤。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.10.1_1509（2018 年 5 月 16 日發行）的變更日誌
{: #1101_1509}

<table summary="自 1.10.1_1508 版以來進行的變更">
<caption>自 1.10.1_1508 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>您在 `kubelet` 根目錄中儲存的資料，現在儲存在工作者節點機器的較大次要磁碟上。</td>
</tr>
</tbody>
</table>

### 1.10.1_1508（2018 年 5 月 1 日發行）的變更日誌
{: #1101_1508}

<table summary="自 1.9.7_1510 版以來進行的變更">
<caption>自 1.9.7_1510 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>2.6.5 版</td>
<td>3.1.1 版</td>
<td>請參閱 Calico [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.projectcalico.org/v3.1/releases/#v311)。</td>
</tr>
<tr>
<td>Kubernetes Heapster</td>
<td>1.5.0 版</td>
<td>1.5.2 版</td>
<td>請參閱 Kubernetes Heapster [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/heapster/releases/tag/v1.5.2)。</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>1.9.7 版</td>
<td>1.10.1 版</td>
<td>請參閱 Kubernetes [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.1)。</td>
</tr>
<tr>
<td>Kubernetes 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>針對叢集的 Kubernetes API 伺服器，已將 <code>StorageObjectInUseProtection</code> 新增至 <code>--enable-admission-plugins</code> 選項。</td>
</tr>
<tr>
<td>Kubernetes DNS</td>
<td>1.14.8</td>
<td>1.14.10</td>
<td>請參閱 Kubernetes DNS [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/dns/releases/tag/1.14.10)。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.9.7-102 版</td>
<td>1.10.1-52 版</td>
<td>已更新成支援 Kubernetes 1.10 版。</td>
</tr>
<tr>
<td>GPU 支援</td>
<td>N/A</td>
<td>N/A</td>
<td>[圖形處理裝置 (GPU) 容器工作負載](cs_app.html#gpu_app)支援現在可用於排程及執行。如需可用的 GPU 機型清單，請參閱[工作者節點的硬體](cs_clusters_planning.html#shared_dedicated_node)。如需相關資訊，請參閱 Kubernetes 文件來[排程 GPU ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://kubernetes.io/docs/tasks/manage-gpus/scheduling-gpus/)。</td>
</tr>
</tbody>
</table>

<br />


## 1.9 版變更日誌
{: #19_changelog}

檢閱下列變更。

### 主節點修正套件 1.9.10_1530（2018 年 10 月 15 日發行）的變更日誌
{: #1910_1530}

<table summary="自 1.9.10_1527 版以來進行的變更">
<caption>自 1.9.10_1527 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>叢集更新</td>
<td>N/A</td>
<td>N/A</td>
<td>已修正從不受支援的版本更新主節點時的叢集附加程式更新問題。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.9.10_1528（2018 年 10 月 10 日發行）的變更日誌
{: #1910_1528}

<table summary="自 1.9.10_1527 版以來進行的變更">
<caption>自 1.9.10_1527 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>核心</td>
<td>4.4.0-133</td>
<td>4.4.0-137</td>
<td>已更新工作者節點映像檔與 [CVE-2018-14633、CVE-2018-17182 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-137.163/changelog) 的核心更新。</td>
</tr>
<tr>
<td>非作用中階段作業逾時</td>
<td>N/A</td>
<td>N/A</td>
<td>基於合規性，將非作用中階段作業逾時設為 5 分鐘。</td>
</tr>
</tbody>
</table>


### 1.9.10_1527（2018 年 10 月 2 日發行）的變更日誌
{: #1910_1527}

<table summary="自 1.9.10_1523 版以來進行的變更">
<caption>自 1.9.10_1523 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.9.10-192 版</td>
<td>1.9.10-219 版</td>
<td>已更新負載平衡器錯誤訊息中的文件鏈結。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間類別</td>
<td>N/A</td>
<td>N/A</td>
<td>已移除 IBM 檔案儲存空間類別中的 `mountOptions`，以使用工作者節點所提供的預設值。已移除 IBM 檔案儲存空間類別中的重複 `reclaimPolicy` 參數。<br><br>
此外，現在，當您更新叢集主節點時，預設 IBM 檔案儲存空間類別會維持不變。如果您要變更預設儲存空間類別，請執行 `kubectl patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`，並將 `<storageclass>` 取代為儲存空間類別的名稱。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.9.10_1524（2018 年 9 月 20 日發行）的變更日誌
{: #1910_1524}

<table summary="自 1.9.10_1523 版以來進行的變更">
<caption>自 1.9.10_1523 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>日誌循環</td>
<td>N/A</td>
<td>N/A</td>
<td>已切換成使用 `systemd` 計時器，而非 `cronjobs`，以防止 `logrotate` 在未於 90 天內重新載入或更新的工作者節點上失敗。**附註**：在此次要版本的所有舊版中，Cron 工作失敗之後會填滿主要磁碟，因為日誌不會循環。在工作者節點作用 90 天但未進行更新或重新載入之後，Cron 工作就會失敗。如果日誌填滿整個主要磁碟，則工作者節點會進入失敗狀態。使用 `ibmcloud ks worker-reload` [指令](cs_cli_reference.html#cs_worker_reload)或 `ibmcloud ks worker-update` [指令](cs_cli_reference.html#cs_worker_update)，即可修正工作者節點。</td>
</tr>
<tr>
<td>工作者節點運行環境元件（`kubelet`、`kube-proxy`、`docker`）</td>
<td>N/A</td>
<td>N/A</td>
<td>已移除主要磁碟上的運行環境元件的相依關係。主要磁碟滿載時，此加強功能可避免工作者節點失敗。</td>
</tr>
<tr>
<td>root 密碼有效期限</td>
<td>N/A</td>
<td>N/A</td>
<td>基於合規性，工作者節點的 root 密碼會在 90 天後到期。如果您的自動化工具需要以 root 身分登入工作者節點，或依賴以 root 身分執行的 Cron 工作，則可以登入工作者節點並執行 `chage -M -1 root` 來停用密碼有效期限。**附註**：如果您的安全規範需求可避免以 root 身分執行或移除密碼有效期限，則請不要停用有效期限。相反地，您可以至少每 90 天[更新](cs_cli_reference.html#cs_worker_update)或[重新載入](cs_cli_reference.html#cs_worker_reload)工作者節點一次。</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/A</td>
<td>N/A</td>
<td>定期清除暫時性裝載裝置，以防止它們變成無界限。此動作解決 [Kubernetes 問題 57345 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/issues/57345)。</td>
</tr>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>已停用預設 Docker 橋接器，因此 `172.17.0.0/16` IP 範圍現在用於專用路徑。如果您依賴直接在主機上執行 `docker` 指令或使用可裝載 Docker Socket 的 Pod 以在工作者節點中建置 Docker 容器，則請從下列選項中進行選擇。<ul><li>若要確保建置容器時的外部網路連線，請執行 `docker build . --network host`。</li>
<li>若要明確建立要在建置容器時使用的網路，請執行 `docker network create`，然後使用此網路。</li></ul>
**附註**：與 Docker Socket 或 Docker 具有直接相依關係嗎？[移轉至 `containerd`（而非 `docker`）作為容器運行環境](cs_versions.html#containerd)，因此您的叢集已準備好要執行 Kubernetes 1.11 版或更新版本。</td>
</tr>
</tbody>
</table>

### 1.9.10_1523（2018 年 9 月 4 日發行）的變更日誌
{: #1910_1523}

<table summary="自 1.9.9_1522 版以來進行的變更">
<caption>自 1.9.9_1522 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.9.9-167 版</td>
<td>1.9.10-192 版</td>
<td>已更新為支援 Kubernetes 1.9.10 版。此外，已變更雲端提供者配置，可更恰當地處理 `externalTrafficPolicy` 設為 `local` 之負載平衡器服務的更新。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間外掛程式</td>
<td>334</td>
<td>338</td>
<td>已將 incubator 版本更新為 1.8。檔案儲存空間會佈建給您選取的特定區域。除非您使用多區域叢集，並且需要新增地區及區域標籤，否則無法更新現有（靜態）PV 實例的標籤。<br><br>已從 IBM 所提供檔案儲存空間類別的裝載選項中移除預設 NFS 版本。主機的作業系統現在會與 IBM Cloud 基礎架構 (SoftLayer) NFS 伺服器協議 NFS 版本。若要手動設定特定的 NFS 版本，或變更主機作業系統所協議 PV 的 NFS 版本，請參閱[變更預設 NFS 版本](cs_storage_file.html#nfs_version_class)。</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>1.9.9 版</td>
<td>1.9.10 版</td>
<td>請參閱 Kubernetes [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.10)。</td>
</tr>
<tr>
<td>Kubernetes Heapster 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>已增加 `heapster-nanny` 容器的資源限制。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.9.9_1522（2018 年 8 月 23 日發行）的變更日誌
{: #199_1522}

<table summary="自 1.9.9_1521 版以來進行的變更">
<caption>自 1.9.9_1521 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>已更新 `systemd` 來修正 `cgroup` 洩漏。</td>
</tr>
<tr>
<td>核心</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>已更新工作者節點映像檔與 [CVE-2018-3620、CVE-2018-3646 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://usn.ubuntu.com/3741-1/) 的核心更新。</td>
</tr>
</tbody>
</table>


### 工作者節點修正套件 1.9.9_1521（2018 年 8 月 13 日發行）的變更日誌
{: #199_1521}

<table summary="自 1.9.9_1520 版以來進行的變更">
<caption>自 1.9.9_1520 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Ubuntu 套件</td>
<td>N/A</td>
<td>N/A</td>
<td>已安裝 Ubuntu 套件的更新。</td>
</tr>
</tbody>
</table>

### 1.9.9_1520（2018 年 7 月 27 日發行）的變更日誌
{: #199_1520}

<table summary="自 1.9.8_1517 版以來進行的變更">
<caption>自 1.9.8_1517 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.9.8-141 版</td>
<td>1.9.9-167 版</td>
<td>已更新為支援 Kubernetes 1.9.9 版。此外，LoadBalancer 服務 `create failure` 事件現在包括所有可攜式子網路錯誤。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間外掛程式</td>
<td>320</td>
<td>334</td>
<td>已將持續性磁區建立的逾時從 15 分鐘增加至 30 分鐘。已將預設計費類型變更為 `hourly`。已將裝載選項新增至預先定義的儲存空間類別。在 IBM Cloud 基礎架構 (SoftLayer) 帳戶的 NFS 檔案儲存空間實例中，已將 **Notes** 欄位變更為 JSON 格式，並已新增 PV 部署至其中的 Kubernetes 名間空間。為了支援多區域叢集，已將區域及地區標籤新增至持續性磁區。</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>1.9.8 版</td>
<td>1.9.9 版</td>
<td>請參閱 Kubernetes [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.9)。</td>
</tr>
<tr>
<td>核心</td>
<td>N/A</td>
<td>N/A</td>
<td>對高效能網路工作負載的工作者節點網路設定做出少量改善。</td>
</tr>
<tr>
<td>OpenVPN 用戶端</td>
<td>N/A</td>
<td>N/A</td>
<td>在 `kube-system` 名稱空間中執行的 OpenVPN 用戶端 `vpn` 部署，現在是由 Kubernetes `addon-manager` 管理。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.9.8_1517（2018 年 7 月 3 日發行）的變更日誌
{: #198_1517}

<table summary="自 1.9.8_1516 版以來進行的變更">
<caption>自 1.9.8_1516 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>核心</td>
<td>N/A</td>
<td>N/A</td>
<td>已最佳化高效能網路工作負載的 `sysctl`。</td>
</tr>
</tbody>
</table>


### 工作者節點修正套件 1.9.8_1516（2018 年 6 月 21 日發行）的變更日誌
{: #198_1516}

<table summary="自 1.9.8_1515 版以來進行的變更">
<caption>自 1.9.8_1515 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>對於非加密的機型，當重新載入或更新工作者節點時，會取得全新的檔案系統來清理次要磁碟。</td>
</tr>
</tbody>
</table>

### 1.9.8_1515（2018 年 6 月 19 日發行）的變更日誌
{: #198_1515}

<table summary="自 1.9.7_1513 版以來進行的變更">
<caption>自 1.9.7_1513 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>1.9.7 版</td>
<td>1.9.8 版</td>
<td>請參閱 [Kubernetes 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.8)。</td>
</tr>
<tr>
<td>Kubernetes 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>已針對叢集的 Kubernetes API 伺服器將 PodSecurityPolicy 新增至 --admission-control 選項，並已將叢集配置為支援 Pod 安全政策。如需相關資訊，請參閱[配置 Pod 安全原則](cs_psp.html)。</td>
</tr>
<tr>
<td>IBM Cloud Provider</td>
<td>1.9.7-102 版</td>
<td>1.9.8-141 版</td>
<td>已更新為支援 Kubernetes 1.9.8 版。</td>
</tr>
<tr>
<td>OpenVPN 用戶端</td>
<td>N/A</td>
<td>N/A</td>
<td>已將 <code>livenessProbe</code> 新增至 <code>kube-system</code> 名稱空間中執行的 OpenVPN 用戶端 <code>vpn</code> 部署。</td>
</tr>
</tbody>
</table>


### 工作者節點修正套件 1.9.7_1513（2018 年 6 月 11 日發行）的變更日誌
{: #197_1513}

<table summary="自 1.9.7_1512 版以來進行的變更">
<caption>自 1.9.7_1512 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>核心更新</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>新的工作者節點映像檔與 [CVE-2018-3639 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639) 的核心更新。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.9.7_1512（2018 年 5 月 18 日發行）的變更日誌
{: #197_1512}

<table summary="自 1.9.7_1511 版以來進行的變更">
<caption>自 1.9.7_1511 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>修正以處理您使用區塊儲存空間外掛程式時發生的錯誤。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.9.7_1511（2018 年 5 月 16 日發行）的變更日誌
{: #197_1511}

<table summary="自 1.9.7_1510 版以來進行的變更">
<caption>自 1.9.7_1510 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>您在 `kubelet` 根目錄中儲存的資料，現在儲存在工作者節點機器的較大次要磁碟上。</td>
</tr>
</tbody>
</table>

### 1.9.7_1510（2018 年 4 月 30 日發行）的變更日誌
{: #197_1510}

<table summary="自 1.9.3_1506 版以來進行的變更">
<caption>自 1.9.3_1506 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>1.9.3 版</td>
<td>1.9.7 版</td>
<td><p>請參閱 [Kubernetes 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.7)。此版本處理 [CVE-2017-1002101 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002101) 及 [CVE-2017-1002102 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002102) 漏洞。</p><p><strong>附註</strong>：現在，`secret`、`configMap`、`downwardAPI` 及預期的磁區已裝載為唯讀磁區。先前，應用程式可以將資料寫入至這些磁區，但系統可以自動回復資料。如果您的應用程式依賴先前不安全的行為，請相應地修改它們。</p></td>
</tr>
<tr>
<td>Kubernetes 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>針對叢集的 Kubernetes API 伺服器，已將 `admissionregistration.k8s.io/v1alpha1=true` 新增至 `--runtime-config` 選項。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.9.3-71 版</td>
<td>1.9.7-102 版</td>
<td>`NodePort` 及 `LoadBalancer` 服務現在支援[保留用戶端來源 IP](cs_loadbalancer.html#node_affinity_tolerations)，方法為將 `service.spec.externalTrafficPolicy` 設為 `Local`。</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>針對較舊叢集，修正[邊緣節點](cs_edge.html#edge)容忍設定。</td>
</tr>
</tbody>
</table>

<br />


## 保存
{: #changelog_archive}

不受支援的 Kubernetes 版本：
*  [1.8 版](#18_changelog)
*  [1.7 版](#17_changelog)

### 1.8 版變更日誌（不受支援）
{: #18_changelog}

檢閱下列變更。

### 工作者節點修正套件 1.8.15_1521（2018 年 9 月 20 日發行）的變更日誌
{: #1815_1521}

<table summary="自 1.8.15_1520 版以來進行的變更">
<caption>自 1.8.15_1520 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>日誌循環</td>
<td>N/A</td>
<td>N/A</td>
<td>已切換成使用 `systemd` 計時器，而非 `cronjobs`，以防止 `logrotate` 在未於 90 天內重新載入或更新的工作者節點上失敗。**附註**：在此次要版本的所有舊版中，Cron 工作失敗之後會填滿主要磁碟，因為日誌不會循環。在工作者節點作用 90 天但未進行更新或重新載入之後，Cron 工作就會失敗。如果日誌填滿整個主要磁碟，則工作者節點會進入失敗狀態。使用 `ibmcloud ks worker-reload` [指令](cs_cli_reference.html#cs_worker_reload)或 `ibmcloud ks worker-update` [指令](cs_cli_reference.html#cs_worker_update)，即可修正工作者節點。</td>
</tr>
<tr>
<td>工作者節點運行環境元件（`kubelet`、`kube-proxy`、`docker`）</td>
<td>N/A</td>
<td>N/A</td>
<td>已移除主要磁碟上的運行環境元件的相依關係。主要磁碟滿載時，此加強功能可避免工作者節點失敗。</td>
</tr>
<tr>
<td>root 密碼有效期限</td>
<td>N/A</td>
<td>N/A</td>
<td>基於合規性，工作者節點的 root 密碼會在 90 天後到期。如果您的自動化工具需要以 root 身分登入工作者節點，或依賴以 root 身分執行的 Cron 工作，則可以登入工作者節點並執行 `chage -M -1 root` 來停用密碼有效期限。**附註**：如果您的安全規範需求可避免以 root 身分執行或移除密碼有效期限，則請不要停用有效期限。相反地，您可以至少每 90 天[更新](cs_cli_reference.html#cs_worker_update)或[重新載入](cs_cli_reference.html#cs_worker_reload)工作者節點一次。</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/A</td>
<td>N/A</td>
<td>定期清除暫時性裝載裝置，以防止它們變成無界限。此動作解決 [Kubernetes 問題 57345 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/issues/57345)。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.8.15_1520（2018 年 8 月 23 日發行）的變更日誌
{: #1815_1520}

<table summary="自 1.8.15_1519 版以來進行的變更">
<caption>自 1.8.15_1519 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>已更新 `systemd` 來修正 `cgroup` 洩漏。</td>
</tr>
<tr>
<td>核心</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>已更新工作者節點映像檔與 [CVE-2018-3620、CVE-2018-3646 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://usn.ubuntu.com/3741-1/) 的核心更新。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.8.15_1519（2018 年 8 月 13 日發行）的變更日誌
{: #1815_1519}

<table summary="自 1.8.15_1518 版以來進行的變更">
<caption>自 1.8.15_1518 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Ubuntu 套件</td>
<td>N/A</td>
<td>N/A</td>
<td>已安裝 Ubuntu 套件的更新。</td>
</tr>
</tbody>
</table>

### 1.8.15_1518（2018 年 7 月 27 日發行）的變更日誌
{: #1815_1518}

<table summary="自 1.8.13_1516 版以來進行的變更">
<caption>自 1.8.13_1516 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.8.13-176 版</td>
<td>1.8.15-204 版</td>
<td>已更新為支援 Kubernetes 1.8.15 版。此外，LoadBalancer 服務 `create failure` 事件現在包括所有可攜式子網路錯誤。</td>
</tr>
<tr>
<td>IBM 檔案儲存空間外掛程式</td>
<td>320</td>
<td>334</td>
<td>已將持續性磁區建立的逾時從 15 分鐘增加至 30 分鐘。已將預設計費類型變更為 `hourly`。已將裝載選項新增至預先定義的儲存空間類別。在 IBM Cloud 基礎架構 (SoftLayer) 帳戶的 NFS 檔案儲存空間實例中，已將 **Notes** 欄位變更為 JSON 格式，並已新增 PV 部署至其中的 Kubernetes 名間空間。為了支援多區域叢集，已將區域及地區標籤新增至持續性磁區。</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>1.8.13 版</td>
<td>1.8.15 版</td>
<td>請參閱 Kubernetes [版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.8.15)。</td>
</tr>
<tr>
<td>核心</td>
<td>N/A</td>
<td>N/A</td>
<td>對高效能網路工作負載的工作者節點網路設定做出少量改善。</td>
</tr>
<tr>
<td>OpenVPN 用戶端</td>
<td>N/A</td>
<td>N/A</td>
<td>在 `kube-system` 名稱空間中執行的 OpenVPN 用戶端 `vpn` 部署，現在是由 Kubernetes `addon-manager` 管理。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.8.13_1516（2018 年 7 月 3 日發行）的變更日誌
{: #1813_1516}

<table summary="自 1.8.13_1515 版以來進行的變更">
<caption>自 1.8.13_1515 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>核心</td>
<td>N/A</td>
<td>N/A</td>
<td>已最佳化高效能網路工作負載的 `sysctl`。</td>
</tr>
</tbody>
</table>


### 工作者節點修正套件 1.8.13_1515（2018 年 6 月 21 日發行）的變更日誌
{: #1813_1515}

<table summary="自 1.8.13_1514 版以來進行的變更">
<caption>自 1.8.13_1514 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>對於非加密的機型，當重新載入或更新工作者節點時，會取得全新的檔案系統來清理次要磁碟。</td>
</tr>
</tbody>
</table>

### 1.8.13_1514（2018 年 6 月 19 日發行）的變更日誌
{: #1813_1514}

<table summary="自 1.8.11_1512 版以來進行的變更">
<caption>自 1.8.11_1512 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>1.8.11	版</td>
<td>1.8.13 版</td>
<td>請參閱 [Kubernetes 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.8.13)。</td>
</tr>
<tr>
<td>Kubernetes 配置</td>
<td>N/A</td>
<td>N/A</td>
<td>已針對叢集的 Kubernetes API 伺服器將 PodSecurityPolicy 新增至 --admission-control 選項，並已將叢集配置為支援 Pod 安全政策。如需相關資訊，請參閱[配置 Pod 安全原則](cs_psp.html)。</td>
</tr>
<tr>
<td>IBM Cloud Provider</td>
<td>1.8.11-126 版</td>
<td>1.8.13-176 版</td>
<td>已更新為支援 Kubernetes 1.8.13 版。</td>
</tr>
<tr>
<td>OpenVPN 用戶端</td>
<td>N/A</td>
<td>N/A</td>
<td>已將 <code>livenessProbe</code> 新增至 <code>kube-system</code> 名稱空間中執行的 OpenVPN 用戶端 <code>vpn</code> 部署。</td>
</tr>
</tbody>
</table>


### 工作者節點修正套件 1.8.11_1512（2018 年 6 月 11 日發行）的變更日誌
{: #1811_1512}

<table summary="自 1.8.11_1511 版以來進行的變更">
<caption>自 1.8.11_1511 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>核心更新</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>新的工作者節點映像檔與 [CVE-2018-3639 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639) 的核心更新。</td>
</tr>
</tbody>
</table>


### 工作者節點修正套件 1.8.11_1511（2018 年 5 月 18 日發行）的變更日誌
{: #1811_1511}

<table summary="自 1.8.11_1510 版以來進行的變更">
<caption>自 1.8.11_1510 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>修正以處理您使用區塊儲存空間外掛程式時發生的錯誤。</td>
</tr>
</tbody>
</table>

### 工作者節點修正套件 1.8.11_1510（2018 年 5 月 16 日發行）的變更日誌
{: #1811_1510}

<table summary="自 1.8.11_1509 版以來進行的變更">
<caption>自 1.8.11_1509 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>您在 `kubelet` 根目錄中儲存的資料，現在儲存在工作者節點機器的較大次要磁碟上。</td>
</tr>
</tbody>
</table>


### 1.8.11_1509（2018 年 4 月 19 日發行）的變更日誌
{: #1811_1509}

<table summary="自 1.8.8_1507 版以來進行的變更">
<caption>自 1.8.8_1507 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>1.8.8 版</td>
<td>1.8.11	版</td>
<td><p>請參閱 [Kubernetes 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.8.11)。此版本處理 [CVE-2017-1002101 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002101) 及 [CVE-2017-1002102 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002102) 漏洞。</p><p><strong>附註</strong>：現在，`secret`、`configMap`、`downwardAPI` 及預期的磁區已裝載為唯讀磁區。先前，應用程式可以將資料寫入至這些磁區，但系統可以自動回復資料。如果您的應用程式依賴先前不安全的行為，請相應地修改它們。</p></td>
</tr>
<tr>
<td>暫停容器映像檔</td>
<td>3.0</td>
<td>3.1</td>
<td>移除已繼承的孤立已休眠處理程序。</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.8.8-86 版</td>
<td>1.8.11-126 版</td>
<td>`NodePort` 及 `LoadBalancer` 服務現在支援[保留用戶端來源 IP](cs_loadbalancer.html#node_affinity_tolerations)，方法為將 `service.spec.externalTrafficPolicy` 設為 `Local`。</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>針對較舊叢集，修正[邊緣節點](cs_edge.html#edge)容忍設定。</td>
</tr>
</tbody>
</table>

<br />


### 1.7 版變更日誌（不受支援）
{: #17_changelog}

檢閱下列變更。

#### 工作者節點修正套件 1.7.16_1514（2018 年 6 月 11 日發行）的變更日誌
{: #1716_1514}

<table summary="自 1.7.16_1513 版以來進行的變更">
<caption>自 1.7.16_1513 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>核心更新</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>新的工作者節點映像檔與 [CVE-2018-3639 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639) 的核心更新。</td>
</tr>
</tbody>
</table>

#### 工作者節點修正套件 1.7.16_1513（2018 年 5 月 18 日發行）的變更日誌
{: #1716_1513}

<table summary="自 1.7.16_1512 版以來進行的變更">
<caption>自 1.7.16_1512 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>修正以處理您使用區塊儲存空間外掛程式時發生的錯誤。</td>
</tr>
</tbody>
</table>

#### 工作者節點修正套件 1.7.16_1512（2018 年 5 月 16 日發行）的變更日誌
{: #1716_1512}

<table summary="自 1.7.16_1511 版以來進行的變更">
<caption>自 1.7.16_1511 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>您在 `kubelet` 根目錄中儲存的資料，現在儲存在工作者節點機器的較大次要磁碟上。</td>
</tr>
</tbody>
</table>

#### 1.7.16_1511（2018 年 4 月 19 日發行）的變更日誌
{: #1716_1511}

<table summary="自 1.7.4_1509 版以來進行的變更">
<caption>自 1.7.4_1509 版以來的變更</caption>
<thead>
<tr>
<th>元件</th>
<th>舊版</th>
<th>現行版本</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>1.7.4 版</td>
<td>1.7.16 版	</td>
<td><p>請參閱 [Kubernetes 版本注意事項 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/kubernetes/kubernetes/releases/tag/v1.7.16)。此版本處理 [CVE-2017-1002101 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002101) 及 [CVE-2017-1002102 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002102) 漏洞。</p><p><strong>附註</strong>：現在，`secret`、`configMap`、`downwardAPI` 及預期的磁區已裝載為唯讀磁區。先前，應用程式可以將資料寫入至這些磁區，但系統可以自動回復資料。如果您的應用程式依賴先前不安全的行為，請相應地修改它們。</p></td>
</tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>1.7.4-133 版</td>
<td>1.7.16-17 版</td>
<td>`NodePort` 及 `LoadBalancer` 服務現在支援[保留用戶端來源 IP](cs_loadbalancer.html#node_affinity_tolerations)，方法為將 `service.spec.externalTrafficPolicy` 設為 `Local`。</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>針對較舊叢集，修正[邊緣節點](cs_edge.html#edge)容忍設定。</td>
</tr>
</tbody>
</table>
