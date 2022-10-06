---
title: 監控的最佳實務 [!DNL Assets] 部署
description: 監控環境和效能的最佳實務 [!DNL Adobe Experience Manager] 部署後進行部署。
contentOwner: AG
role: Admin, Architect
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---

# 監控的最佳實務 [!DNL Adobe Experience Manager Assets] 部署 {#assets-monitoring-best-practices}

從 [!DNL Experience Manager Assets] 從立場看，監測應包括觀察和報告以下過程和技術：

* 系統CPU
* 系統記憶體使用
* 系統磁碟IO和IO等待時間
* 系統網路IO
* 用於堆利用率和非同步進程（如工作流）的JMX MBean
* OSGi控制台運行狀況檢查

通常， [!DNL Experience Manager Assets] 可通過兩種方式進行監控：即即時監控和長期監控。

## 即時監視 {#live-monitoring}

您應在開發的效能測試階段或高負載情況下執行即時監控，以了解環境的效能特性。 通常應使用一套工具來執行即時監控。 以下是一些建議：

* [Visual VM](https://visualvm.github.io/):Visual VM使您能夠查看詳細的Java VM資訊，包括CPU使用量、Java記憶體使用量。 此外，它還可讓您取樣並評估在部署中執行的程式碼。
* [頂端](https://man7.org/linux/man-pages/man1/top.1.html):Top是開啟儀表板的Linux命令，該儀表板顯示使用情況統計資訊，包括CPU、記憶體和IO使用情況。 它提供執行個體上所發生情況的概觀。
* [Htop](https://hisham.hm/htop/):Htop是互動式程式檢視器。 除了Top提供的功能外，它還提供詳細的CPU和記憶體使用。 Htop可安裝在大部分的Linux系統上，使用 `yum install htop` 或 `apt-get install htop`.

* Iotop:Iotop是磁碟IO使用情況的詳細儀表板。 它顯示的條形和儀表，用於描述使用磁碟IO的過程及其使用量。 Iotop可安裝在大部分的Linux系統上，使用 `yum install iotop` 或 `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/):Iftop顯示有關乙太網/網路使用的詳細資訊。 Iftop會針對使用乙太網的實體顯示每個通訊通道的統計資料，以及其使用的頻寬量。 Iftop可安裝在大部分的Linux系統上，使用 `yum install iftop` 或 `apt-get install iftop`.

* Java飛行記錄器(JFR):來自Oracle的商業工具，可在非生產環境中自由使用。 如需詳細資訊，請參閱 [Java飛行記錄器在CQ運行時診斷中的應用](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` 檔案：您可以調查 [!DNL Experience Manager] `error.log` 檔案，以取得系統中記錄之錯誤的詳細資訊。 使用命令 `tail -F quickstart/logs/error.log` 來識別要調查的錯誤。
* [工作流程主控台](/help/sites-administering/workflows.md):運用工作流程主控台來監控延遲或卡住的工作流程。

通常，您會一起使用這些工具，以取得有關 [!DNL Experience Manager] 部署。

>[!NOTE]
>
>這些工具是標準工具，不直接受Adobe支援。 他們不需要額外的授權。

![chlimage_1-33](assets/chlimage_1-143.png)

*圖：使用Visual VM工具進行即時監視。*

![chlimage_1-32](assets/chlimage_1-142.png)

## 長期監測 {#long-term-monitoring}

長期監控 [!DNL Experience Manager] 部署涉及在更長時間內監視受監視的同一部分。 也包含定義環境專屬的警報。

### 日誌聚合和報告 {#log-aggregation-and-reporting}

有數種工具可用於匯總日誌，例如Splunk(TM)和Elastic Search、Logstash和Kabana(ELK)。 評估您的正常運行時間 [!DNL Experience Manager] 部署時，您必須了解系統的特定記錄事件，並根據這些事件建立警報。 對您的開發和操作實踐有良好的了解，可幫助您更好地了解如何調整日誌聚合過程以生成關鍵警報。

### 環境監控 {#environment-monitoring}

環境監控包括監控下列項目：

* 網路吞吐量
* 磁碟IO
* 記憶體
* CPU利用率
* JMX MBean
* 外部網站

您需要外部工具，例如NewRelic(TM)和AppDynamics(TM)來監視每個項目。 使用這些工具，您可以定義系統特有的警報，例如高系統利用率、工作流備份、運行狀況檢查失敗或未驗證的網站訪問。 Adobe不建議使用任何特定工具而非其他工具。 尋找適合您的工具，並運用它來監控討論的項目。

#### 內部應用程式監控 {#internal-application-monitoring}

內部應用程式監控包括監控構成 [!DNL Experience Manager] 堆疊，包括JVM、內容存放庫，以及透過平台上建置的自訂應用程式程式碼進行監控。 通常，它通過JMX Mbeans來執行，這些JMX Mbeans可以直接由許多流行的監控解決方案進行監控，如SolarWinds(TM)、HP OpenView(TM)、Hyperic(TM)、Zabbix(TM)等。 對於不支援直接連接到JMX的系統，可以編寫shell指令碼以提取JMX資料，並以它們本來理解的格式將其公開到這些系統。

預設情況下不啟用對JMX Mbeans的遠程訪問。 有關通過JMX進行監視的詳細資訊，請參見 [使用JMX技術進行監控和管理](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

在許多情況下，需要基線來有效監視統計資料。 要建立基線，請在預定時段內的正常工作條件下觀察系統，然後識別正常度量。

**JVM監視**

和任何基於Java的應用程式棧一樣， [!DNL Experience Manager] 取決於透過基礎Java虛擬機提供給它的資源。 您可以透過JVM公開的Platform MXBean來監視其中許多資源的狀態。 如需MXBean的詳細資訊，請參閱 [使用Platform MBean伺服器和Platform MXBean](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

以下是可監視JVM的一些基線參數：

記憶體

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* 例項：所有伺服器
* 警報閾值：當堆或非堆記憶體利用率超過相應最大記憶體的75%時。
* 警報定義：系統記憶體不足或代碼中出現記憶體洩漏。 分析線程轉儲以達到定義。

>[!NOTE]
>
>此Bean提供的資訊以位元組表示。

線程

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* 例項：所有伺服器
* 警報閾值：當線程數大於基線的150%時。
* 警報定義：要麼存在活動的失控進程，要麼低效操作消耗了大量資源。 分析線程轉儲以達到定義。

**監視[!DNL Experience Manager]**

[!DNL Experience Manager] 還通過JMX公開一組統計和操作。 這些功能有助於評估系統運行狀況並在潛在問題影響用戶之前找出這些問題。 如需詳細資訊，請參閱 [檔案](/help/sites-administering/jmx-console.md) on [!DNL Experience Manager] JMX MBean。

以下是一些基線參數，您可以監視 [!DNL Experience Manager]:

復寫代理

* MBean: `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* 例項：一個製作和所有發佈執行個體（適用於排清代理）
* 警報閾值：若 `QueueBlocked` is `true` 或 `QueueNumEntries` 大於基線的150%。

* 警報定義：系統中是否存在阻止的隊列，表明複製目標已關閉或無法訪問。 網路或基礎架構問題通常會導致過多的條目排隊，從而對系統效能產生負面影響。

>[!NOTE]
>
>對於MBean和URL參數，請替換 `<AGENT_NAME>` 以及您要監視的復寫代理的名稱。

會話計數器

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository統計資訊&quot;,type*=&quot;RepositoryStats&quot;
* 例項：所有伺服器
* 警報閾值：開啟的工作階段超過基線超過50%時。
* 警報定義：工作階段可透過程式碼開啟，且永不關閉。 隨著時間的推移，這可能會緩慢發生，最終導致系統記憶體洩漏。 雖然系統上的工作階段數應會有所波動，但不應持續增加。

健康狀態檢查

健康狀態檢查 [操作儀表板](/help/sites-administering/operations-dashboard.md#health-reports) 有相應的JMX MBean用於監視。 但是，您可以編寫自定義運行狀況檢查以公開其他系統統計資訊。

以下是有助於監控的現成可用健康狀態檢查：

* 系統檢查
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * 例項：一個作者，所有發佈伺服器
   * 警報閾值：狀態不確定時
   * 警報定義：其中一個度量的狀態為「警告」或「嚴重」。 檢查日誌屬性，了解問題原因的詳細資訊。

* 復寫佇列

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * 例項：一個作者，所有發佈伺服器
   * 警報閾值：狀態不確定時
   * 警報定義：其中一個度量的狀態為「警告」或「嚴重」。 檢查日誌屬性，以了解有關導致此問題的隊列的詳細資訊。

* 回應效能

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * 例項：所有伺服器
   * 警報持續時間：狀態不確定時
   * 警報定義：其中一個度量的狀態為「警告」或「關鍵」狀態。 檢查日誌屬性，以了解有關導致此問題的隊列的詳細資訊。

* 查詢效能

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * 例項：一個作者，所有發佈伺服器
   * 警報閾值：狀態不確定時
   * 警報定義：一個或多個查詢在系統中運行緩慢。 檢查日誌屬性，以了解有關導致問題的查詢的詳細資訊。

* 作用中組合

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * 例項：所有伺服器
   * 警報閾值：狀態不確定時
   * 警報定義：系統上存在非活動或未解析的OSGi捆綁。 檢查log屬性，以取得造成問題的套件組合的詳細資訊。

* 日誌錯誤

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * 例項：所有伺服器
   * 警報閾值：狀態不確定時
   * 警報定義：記錄檔中有錯誤。 檢查日誌屬性，了解問題原因的詳細資訊。

## 共同問題和決議  {#common-issues-and-resolutions}

在監控過程中，如果您遇到問題，以下是一些疑難排解工作，您可以執行以解決 [!DNL Experience Manager] 部署：

* 如果使用TarMK，請經常執行Tar壓縮。 如需詳細資訊，請參閱 [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* 檢查 `OutOfMemoryError` 記錄檔。 如需詳細資訊，請參閱 [分析記憶體問題](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).

* 檢查日誌中是否有對未索引查詢、樹遍歷或索引遍歷的任何引用。 這表示未索引的查詢或未充分索引的查詢。 有關優化查詢和索引效能的最佳實踐，請參見 [查詢和索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* 使用工作流程主控台來確認您的工作流程是否如預期般執行。 如有可能，將多個工作流程簡化為單一工作流程。
* 重新訪問即時監視，並查找任何特定資源的其他瓶頸或高消費者。
* 調查來自客戶端網路的出口點和指向的入口點 [!DNL Experience Manager] 部署網路，包括dispatcher。 這些經常是瓶頸區。 如需詳細資訊，請參閱 [資產網路考量事項](/help/assets/assets-network-considerations.md).
* 放大您的 [!DNL Experience Manager] 伺服器。 您的大小可能不足 [!DNL Experience Manager] 部署。 Adobe客戶支援可協助您識別伺服器的大小是否不足。
* 檢查 `access.log` 和 `error.log` 某個時段的條目檔案出錯。 尋找可能表示自訂程式碼異常的模式。 將它們新增至您監視的事件清單。
