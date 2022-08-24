---
title: 監控的最佳做法 [!DNL Assets] 部署
description: 監控環境和效能的最佳實踐 [!DNL Adobe Experience Manager] 部署後進行部署。
contentOwner: AG
role: Admin, Architect
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 1%

---

# 監控的最佳做法 [!DNL Adobe Experience Manager Assets] 部署 {#assets-monitoring-best-practices}

從 [!DNL Experience Manager Assets] 從立場看，監測應包括觀察和報告以下過程和技術：

* 系統CPU
* 系統記憶體使用
* 系統磁碟IO和IO等待時間
* 系統網路IO
* JMX MBean用於堆利用率和非同步進程（如工作流）
* OSGi控制台運行狀況檢查

通常， [!DNL Experience Manager Assets] 可以通過兩種方式進行監測，即即時監測和長期監測。

## 即時監視 {#live-monitoring}

您應在開發的效能測試階段或高負載情況下執行即時監控，以瞭解環境的效能特徵。 通常，應使用一套工具執行即時監視。 以下是一些建議：

* [可視虛擬機](https://visualvm.github.io/):Visual VM使您能夠查看詳細的Java VM資訊，包括CPU使用率、Java記憶體使用率。 此外，它還允許您對在部署上運行的代碼進行採樣和評估。
* [頂部](https://man7.org/linux/man-pages/man1/top.1.html):Top是開啟儀表板的Linux命令，顯示使用情況統計資訊，包括CPU、記憶體和IO使用情況。 它提供了對實例發生情況的高級概述。
* [赫托普](https://hisham.hm/htop/):Htop是互動式進程查看器。 除了Top提供的功能外，它還提供詳細的CPU和記憶體使用。 Htop可以安裝在大多數Linux系統上， `yum install htop` 或 `apt-get install htop`。

* Iotop:Iotop是一個詳細的磁碟IO使用情況儀表板。 它顯示描述使用磁碟IO的進程及其使用量的條形和米。 Iotop可安裝在大多數Linux系統上， `yum install iotop` 或 `apt-get install iotop`。

* [Iftop](https://www.ex-parrot.com/pdw/iftop/):Iftop顯示有關乙太網/網路使用情況的詳細資訊。 Iftop顯示使用乙太網的實體的每個通信通道統計資訊以及它們使用的頻寬量。 Iftop可以安裝在大多數Linux系統上， `yum install iftop` 或 `apt-get install iftop`。

* Java飛行記錄器(JFR):一種來自Oracle的商業工具，您可以在非生產環境中自由使用。 有關詳細資訊，請參閱 [如何利用Java飛行記錄器診斷CQ運行時問題](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq)。
* [!DNL Experience Manager] `error.log` 檔案：你可以調查 [!DNL Experience Manager] `error.log` 檔案，獲取系統中記錄的錯誤的詳細資訊。 使用命令 `tail -F quickstart/logs/error.log` 確定要調查的錯誤。
* [工作流控制台](/help/sites-administering/workflows.md):利用工作流控制台監視滯後或停滯的工作流。

通常，您會一起使用這些工具，以全面瞭解您的 [!DNL Experience Manager] 部署。

>[!NOTE]
>
>這些工具是標準工具，不直接受Adobe支援。 它們不需要額外的許可證。

![chlimage_1-33](assets/chlimage_1-143.png)

*圖：使用Visual VM工具進行即時監視。*

![chlimage_1-32](assets/chlimage_1-142.png)

## 長期監測 {#long-term-monitoring}

長期監測 [!DNL Experience Manager] 部署涉及對受即時監視的相同部分進行更長時間的監視。 它還包括定義特定於您的環境的警報。

### 日誌聚合和報告 {#log-aggregation-and-reporting}

有幾種工具可用於聚合日誌，例如Splunk(TM)和Elastic Search、Logstash和Kabana(ELK)。 評估您的正常運行時間 [!DNL Experience Manager] 部署時，瞭解特定於系統的日誌事件並基於這些事件建立警報非常重要。 對您的開發和操作實踐的深入瞭解可以幫助您更好地瞭解如何調整日誌聚合過程以生成關鍵警報。

### 環境監測 {#environment-monitoring}

環境監控包括以下監控：

* 網路吞吐量
* 磁碟IO
* 記憶體
* CPU利用率
* JMX MBean
* 外部網站

您需要外部工具，如NewRelic(TM)和AppDynamics(TM)來監視每個項目。 使用這些工具，您可以定義特定於系統的警報，例如系統利用率高、工作流備份、運行狀況檢查失敗或未經身份驗證的網站訪問。 Adobe不建議使用任何特定工具。 查找適合您的工具，並利用它來監視所討論的項目。

#### 內部應用程式監控 {#internal-application-monitoring}

內部應用程式監控包括監控構成 [!DNL Experience Manager] 堆棧，包括JVM、內容儲存庫，以及通過平台上構建的自定義應用程式碼進行監視。 一般來說，它通過JMX Mbeans進行，這些JMX Mbeans可以由許多流行的監控解決方案直接進行監控，如SolarWinds(TM),HP OpenView(TM),Hyperic(TM),Zabbix(TM)等。 對於不支援與JMX直接連接的系統，可以編寫shell指令碼以提取JMX資料並將其以它們本機理解的格式暴露給這些系統。

預設情況下未啟用對JMX Mbeans的遠程訪問。 有關通過JMX進行監視的詳細資訊，請參見 [利用JMX技術進行監控和管理](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html)。

在許多情況下，需要基線來有效監視統計資料。 要建立基線，請在正常工作條件下觀察系統一段預定時間，然後識別正常度量。

**JVM監視**

與任何基於Java的應用程式堆棧一樣， [!DNL Experience Manager] 取決於通過基礎Java虛擬機提供給它的資源。 您可以通過JVM公開的平台MXBean監視其中許多資源的狀態。 有關MXBean的詳細資訊，請參見 [使用平台MBean伺服器和平台MXBean](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html)。

下面是一些可監視JVM的基線參數：

記憶體

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* 實例：所有伺服器
* 警報閾值：當堆或非堆記憶體利用率超過相應最大記憶體的75%時。
* 警報定義：系統記憶體不足或代碼中出現記憶體洩漏。 分析線程轉儲以達到定義。

>[!NOTE]
>
>此Bean提供的資訊以位元組表示。

線程

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* 實例：所有伺服器
* 警報閾值：當線程數大於基線的150%時。
* 警報定義：要麼存在活動失控進程，要麼低效操作會消耗大量資源。 分析線程轉儲以達到定義。

**監視器[!DNL Experience Manager]**

[!DNL Experience Manager] 還通過JMX公開一組統計和操作。 這些功能有助於評估系統運行狀況並在潛在問題影響用戶之前找出它們。 有關詳細資訊，請參見 [文檔](/help/sites-administering/jmx-console.md) 上 [!DNL Experience Manager] JMX MBean。

下面是一些可監視的基線參數 [!DNL Experience Manager]:

複製代理

* MBean: `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* 實例：一個作者和所有發佈實例（用於刷新代理）
* 警報閾值：當 `QueueBlocked` 是 `true` 或 `QueueNumEntries` 大於基線的150%。

* 警報定義：系統中存在阻止的隊列，表明複製目標已關閉或無法訪問。 通常，網路或基礎架構問題會導致過多條目排隊，這可能會對系統效能造成負面影響。

>[!NOTE]
>
>對於MBean和URL參數，替換 `<AGENT_NAME>` 和要監視的複製代理的名稱。

會話計數器

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository統計&quot;，類型*= &quot;資料庫統計&quot;
* 實例：所有伺服器
* 警報閾值：當開啟的會話超過基線超過50%時。
* 警報定義：會話可以通過一段代碼開啟，並且永不關閉。 這可能會隨著時間推移緩慢發生，並最終導致系統記憶體洩漏。 雖然系統上的會話數應該有所波動，但不應持續增加。

健康狀態檢查

中提供的運行狀況檢查 [操作面板](/help/sites-administering/operations-dashboard.md#health-reports) 具有相應的JMX MBean進行監視。 但是，您可以編寫自定義運行狀況檢查以公開其他系統統計資訊。

下面是一些有助於監控的現成運行狀況檢查：

* 系統檢查
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * 實例：一個作者，所有發佈伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：其中一個度量的狀態為「警告」或「嚴重」。 檢查日誌屬性以瞭解問題原因的詳細資訊。

* 複製隊列

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * 實例：一個作者，所有發佈伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：其中一個度量的狀態為「警告」或「嚴重」。 有關導致此問題的隊列的詳細資訊，請檢查日誌屬性。

* 響應效能

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * 實例：所有伺服器
   * 警報持續時間：當狀態不正常時
   * 警報定義：其中一個度量的狀態為「警告」或「嚴重」。 有關導致此問題的隊列的詳細資訊，請檢查日誌屬性。

* 查詢效能

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * 實例：一個作者，所有發佈伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：一個或多個查詢在系統中運行緩慢。 有關導致此問題的查詢的詳細資訊，請檢查日誌屬性。

* 作用中組合

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * 實例：所有伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：系統上存在非活動或未解析的OSGi捆綁包。 有關導致此問題的捆綁包的詳細資訊，請檢查日誌屬性。

* 日誌錯誤

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * 實例：所有伺服器
   * 警報閾值：當狀態不正常時
   * 警報定義：日誌檔案中有錯誤。 檢查日誌屬性以瞭解問題原因的詳細資訊。

## 共同問題和決議  {#common-issues-and-resolutions}

在監視過程中，如果遇到問題，您可以執行一些故障排除任務來解決與 [!DNL Experience Manager] 部署：

* 如果使用TarMK，請經常運行Tar壓縮。 有關詳細資訊，請參閱 [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。
* 檢查 `OutOfMemoryError` 日誌。 有關詳細資訊，請參見 [分析記憶體問題](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)。

* 檢查日誌中是否有對未索引查詢、樹遍歷或索引遍歷的引用。 這表示未編製索引的查詢或索引不足的查詢。 有關優化查詢和索引效能的最佳做法，請參見 [查詢和索引的最佳做法](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。
* 使用工作流控制台驗證工作流是否按預期方式執行。 如果可能，將多個工作流壓縮為單個工作流。
* 重新訪問即時監控，並尋找其他瓶頸或特定資源的高消費者。
* 調查來自客戶端網路的出口點和指向 [!DNL Experience Manager] 部署網路，包括調度程式。 這些往往是瓶頸領域。 有關詳細資訊，請參見 [資產網路注意事項](/help/assets/assets-network-considerations.md)。
* 將您的 [!DNL Experience Manager] 伺服器。 您的大小可能不足 [!DNL Experience Manager] 部署。 Adobe客戶支援可幫助您確定伺服器是否超過大小。
* 檢查 `access.log` 和 `error.log` 出現問題時的條目檔案。 查找可能表示自定義代碼異常的模式。 將它們添加到您監視的事件清單中。
