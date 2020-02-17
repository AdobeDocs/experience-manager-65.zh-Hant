---
title: 監控AEM Assets部署的最佳實務
description: 部署AEM例項後，監控其環境與效能的最佳實務。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b0555655bceda4b1ac4a9f14029778387b223c2f

---


# 監控AEM Assets部署的最佳實務 {#assets-monitoring-best-practices}

從Adobe Experience Manager(AEM)資產的角度來看，監控應包括觀察和報告下列流程和技術：

* 系統CPU
* 系統記憶體使用
* 系統磁碟IO和IO等待時間
* 系統網路IO
* JMX MBeans用於堆積利用率和非同步進程，例如工作流程
* OSGi控制台運行狀況檢查

通常，AEM Assets可透過兩種方式進行監控：即時監控和長期監控。

## 即時監控 {#live-monitoring}

您應在開發的效能測試階段或在高負載情況下執行即時監控，以瞭解您環境的效能特性。 通常，應使用一套工具來執行即時監控。 以下是一些建議：

* [Visual VM](https://visualvm.java.net/):Visual VM可讓您查看詳細的Java VM資訊，包括CPU使用量、Java記憶體使用量。 此外，它還可讓您取樣並評估執行於例項的程式碼。
* [頂部](https://man7.org/linux/man-pages/man1/top.1.html):頂端是Linux命令，可開啟控制面板，顯示使用狀況統計資料，包括CPU、記憶體和IO使用狀況。 它提供執行個體現狀的高階概述。
* [頂端](https://hisham.hm/htop/):Htop是互動式流程檢視器。 除了Top提供的功能外，它還提供詳細的CPU和記憶體使用情況。 Htop可以安裝在大部分的Linux系統上，使用 `yum install htop` 或 `apt-get install htop`。

* [Iotop](https://guichaz.free.fr/iotop/):Iotop是磁碟IO使用情況的詳細儀表板。 它顯示了描述使用磁碟IO的進程及其使用量的條和米。 Iotop可以安裝在大部分的Linux系統上，使用 `yum install iotop` 或 `apt-get install iotop`。

* [Iftop](https://www.ex-parrot.com/pdw/iftop/):Iftop顯示有關乙太網／網路使用的詳細資訊。 Iftop會根據使用乙太網的實體的通信通道統計資訊以及它們使用的頻寬量。 Iftop可使用或安裝在大多數Linux `yum install iftop` 系統 `apt-get install iftop`上。

* Java Flight Recorder(JFR):Oracle提供的一種商業工具，可在非生產環境中自由使用。 如需詳細資訊，請 [參閱如何使用Java Flight Recorder來診斷CQ執行階段問題](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq)。
* AEM error.log檔案：您可以調查AEM error.log檔案，以取得系統中記錄之錯誤的詳細資訊。 使用命令 `tail -F quickstart/logs/error.log` 識別您應調查的錯誤。
* [工作流程主控台](/help/sites-administering/workflows.md):運用工作流程主控台來監控落後或停滯的工作流程。

通常，您會搭配使用這些工具，以取得有關AEM例項效能的完整概念。

>[!NOTE]
>
>這些工具是標準工具，Adobe不直接支援。 他們不需要額外的授權。

![chlimage_1-33](assets/chlimage_1-143.png)

*圖：使用Visual VM工具進行即時監控*


![chlimage_1-32](assets/chlimage_1-142.png)

## 長期監控 {#long-term-monitoring}

AEM例項的長期監控包括對受即時監控的相同部分進行較長時間的監控。 它還包括定義特定於您環境的警報。

### 日誌聚合和報告 {#log-aggregation-and-reporting}

有幾種工具可用於聚合日誌，例如Splunk(TM)和Elastic Search/Logstash/Kabana(ELK)。 若要評估AEM例項的正常運作時間，請務必瞭解系統特定的記錄事件並根據事件建立警報。 熟悉您的開發和操作實踐有助於您更好地瞭解如何調整日誌聚合過程以生成關鍵警報。

### 環境監控 {#environment-monitoring}

環境監控包括監控以下內容：

* 網路吞吐量
* 磁碟IO
* 記憶體
* CPU使用率
* JMX MBeans
* 外部網站

您需要NewRelic(TM)和AppDynamics(TM)等外部工具來監控每個項目。 使用這些工具，您可以定義系統專用的警報，例如系統使用率高、工作流程備份、運行狀況檢查失敗或未驗證的網站存取。 Adobe不建議使用任何特定工具，而不建議使用其他工具。 尋找適合您的工具，並運用它來監控討論的項目。

#### 內部應用程式監控 {#internal-application-monitoring}

內部應用程式監視包括監視組成AEM堆疊的應用程式元件，包括JVM、內容存放庫，以及透過平台上建立的自訂應用程式程式碼進行監視。 通常，它是通過JMX Mbeans進行的，它可由許多常用的監控解決方案直接進行監控，如SolarWinds(TM),HP openView(TM),Hyperic(TM),Zabbix(TM)等。 對於不支援直接連線至JMX的系統，您可編寫shell指令碼來擷取JMX資料，並以他們本身瞭解的格式將它公開給這些系統。

預設情況下，未啟用對JMX Mbeans的遠程訪問。 有關通過JMX進行監視的詳細資訊，請參 [閱使用JMX技術監視和管理](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html)。

在許多情況下，需要基線來有效監控統計資料。 要建立基線，請在預定時間段內觀察系統在正常工作條件下，然後識別正常度量。

**JVM監控**

和任何以Java為基礎的應用程式堆疊一樣，AEM會依賴透過基礎Java Virtual Machine提供給它的資源。 您可以透過JVM公開的平台MXBeans來監視其中許多資源的狀態。 有關MXBeans的詳細資訊，請參 [閱使用平台MBean伺服器和平台MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html)。

以下是一些可監視JVM的基線參數：

記憶體

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* 例項：所有伺服器
* 警報閾值：當堆或非堆記憶體利用率超過相應最大記憶體的75%時。
* 警報定義：系統記憶體不足，或代碼中出現記憶體洩漏。 分析線程轉儲以獲得定義。

>[!Note]
>
>此Bean提供的資訊以位元組表示。

線程

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* 例項：所有伺服器
* 警報閾值：當線程數大於基線的150%時。
* 警報定義：要麼存在活動的失控進程，要麼低效操作消耗大量資源。 分析線程轉儲以獲得定義。

**AEM監控**

AEM也透過JMX公開一組統計資料和作業。 這些功能有助於評估系統運行狀況，並在潛在問題影響用戶之前找出它們。 如需詳細資訊，請參 [閱](/help/sites-administering/jmx-console.md) AEM JMX MBeans的檔案。

以下是您可針對AEM監控的一些基準參數：

複製代理

* MBean: `com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>"`
* 例項：一個作者和所有發佈實例（用於刷新代理）
* 警報閾值：當值為或 `QueueBlocked` 值 `true` 大於基 `QueueNumEntries` 線的150%時。

* 警報定義：系統中存在阻止的隊列，表明複製目標已關閉或無法訪問。 通常，網路或基礎架構問題會導致過多條目被排入隊列，從而對系統效能產生不利影響。

>[!Note]
>
>對於MBean和URL參數，請 `<AGENT_NAME>` 以要監視的複製代理的名稱替換。

作業計數器

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository統計資料&quot;,type*=&quot;RepositoryStats&quot;
* 例項：所有伺服器
* 警報閾值：當開啟的工作階段超過基準50%時。
* 警報定義：可透過程式碼來開啟工作階段，但絕不關閉。 這可能會隨著時間推移而緩慢發生，最終導致系統記憶體洩漏。 雖然會話數在系統上應會有所波動，但不應持續增加。

健康狀態檢查

Health checks that are available in the [operations dashboard](/help/sites-administering/operations-dashboard.md#health-reports) have correspond JMX MBeans for monitoring. 不過，您可以編寫自訂的健全性檢查，以公開其他系統統計資料。

以下是一些現成可用的運行狀況檢查，這些檢查對於監控是有益的：

* 系統檢查
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * 例項：一個作者，所有發佈伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：其中一個量度的狀態為「警告」或「嚴重」。 檢查日誌屬性，以瞭解有關問題原因的詳細資訊。

* 複製隊列

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck `
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * 例項：一個作者，所有發佈伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：其中一個量度的狀態為「警告」或「嚴重」。 檢查日誌屬性，以瞭解有關導致此問題的隊列的詳細資訊。

* 回應效能

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * 例項：所有伺服器
   * 警報持續時間：當狀態不正常時
   * 警報定義：其中一個度量的狀態為「警告」或「嚴重」。 檢查日誌屬性，以瞭解有關導致此問題的隊列的詳細資訊。

* 查詢效能

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * 例項：一個作者，所有發佈伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：一個或多個查詢在系統中運行緩慢。 有關導致此問題的查詢的詳細資訊，請查看日誌屬性。

* 作用中組合

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * 例項：所有伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：系統上存在非活動或未解析的OSGi捆綁包。 請查看log屬性，以取得導致此問題的叢集的詳細資訊。

* 日誌錯誤

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * 例項：所有伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：日誌檔案中出現錯誤。 請查看log屬性，以取得問題原因的詳細資訊。

## 常見問題和解決方案 {#common-issues-and-resolutions}

在監控程式中，如果您遇到問題，請執行下列疑難排解工作，以解決AEM例項的常見問題：

* 如果使用TarMK，請經常執行Tar壓縮。 有關詳細資訊，請參 [閱維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。
* 檢查 `OutOfMemoryError` 日誌。 有關詳細資訊，請參 [閱分析記憶體問題](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)。

* 檢查日誌中是否有任何對未索引查詢、樹遍歷或索引遍歷的引用。 這表示未索引的查詢或索引不足的查詢。 有關優化查詢和索引效能的最佳實踐，請參 [閱查詢和索引的最佳實踐](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。
* 使用工作流程主控台來驗證您的工作流程是否如預期般執行。 如果可能，將多個工作流程簡化為單一工作流程。
* 重新造訪即時監控，並尋找其他瓶頸或特定資源的高消費者。
* 調查來自用戶端網路的出口點，以及AEM例項網路的入口點，包括發送器。 這些往往是瓶頸領域。 如需詳細資訊，請參閱「資 [產」網路考量事項](/help/assets/assets-network-considerations.md)。
* 調整AEM伺服器的大小。 您的AEM例項可能大小不足。 Adobe支援可協助您識別伺服器的大小是否不足。
* 檢查和 `access.log` 檔案 `error.log` 中是否有項目出現問題。 尋找可能表示自訂代碼異常的模式。 將它們新增至您所監視的事件清單。
