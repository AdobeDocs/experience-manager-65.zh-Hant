---
title: 監控的最佳實務 [!DNL Assets] 部署
description: 監控環境與效能的最佳實務 [!DNL Adobe Experience Manager] 部署後部署。
contentOwner: AG
role: Admin, Architect
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---

# 監控的最佳實務 [!DNL Adobe Experience Manager Assets] 部署 {#assets-monitoring-best-practices}

從 [!DNL Experience Manager Assets] 從觀點來看，監控應包括觀察和報告以下流程和技術：

* 系統CPU
* 系統記憶體使用量
* 系統磁碟IO和IO等候時間
* 系統網路IO
* 棧積使用和非同步程式（例如工作流程）的JMX MBean
* OSGi主控台健康情況檢查

通常 [!DNL Experience Manager Assets] 監控方式有兩種：即時監控和長期監控。

## 即時監視 {#live-monitoring}

您應在開發的效能測試階段或高負載情況下執行即時監視，以瞭解環境的效能特性。 通常應使用一套工具來執行即時監視。 以下是一些建議：

* [Visual VM](https://visualvm.github.io/)：Visual VM可讓您檢視詳細的Java VM資訊，包括CPU使用量、Java記憶體使用量。 此外，它可讓您取樣並評估在部署上執行的程式碼。
* [上](https://man7.org/linux/man-pages/man1/top.1.html)：頂端是開啟控制面板的Linux命令，其中顯示使用狀況統計資料，包括CPU、記憶體和IO使用狀況。 它提供執行個體上所發生事件的整體概觀。
* [Htop](https://hisham.hm/htop/)： Htop是互動式程式檢視器。 除了Top提供的資訊外，還提供詳細的CPU和記憶體使用狀況。 Htop可使用安裝在大多數Linux系統上 `yum install htop` 或 `apt-get install htop`.

* Iotop： Iotop是磁碟IO使用情況的詳細儀表板。 它會顯示長條圖和公尺，描繪使用磁碟IO的流程及其使用的數量。 大部分的Linux系統都可以使用安裝Iotop `yum install iotop` 或 `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/)： Iftop會顯示有關乙太網路/網路使用的詳細資訊。 Iftop會針對使用乙太網路的實體，顯示每個通訊通道的統計資料，以及實體使用的頻寬量。 Iftop可使用安裝在大部分的Linux系統上 `yum install iftop` 或 `apt-get install iftop`.

* Java Flight Recorder (JFR)：Oracle中的商業工具，您可以在非生產環境中自由使用。 如需詳細資訊，請參閱 [如何使用Java Flight Recorder來診斷CQ執行階段問題](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` 檔案：您可以調查 [!DNL Experience Manager] `error.log` 檔案以取得系統中記錄的錯誤詳細資訊。 使用指令 `tail -F quickstart/logs/error.log` 以識別要調查的錯誤。
* [工作流程主控台](/help/sites-administering/workflows.md)：運用工作流程主控台來監視落後或卡住的工作流程。

通常，您會搭配使用這些工具，全面瞭解您的電腦的效能 [!DNL Experience Manager] 部署。

>[!NOTE]
>
>這些工具是標準工具，Adobe不直接支援。 它們不需要額外的授權。

![chlimage_1-33](assets/chlimage_1-143.png)

*圖：使用Visual VM工具的即時監視。*

![chlimage_1-32](assets/chlimage_1-142.png)

## 長期監視 {#long-term-monitoring}

長期監控 [!DNL Experience Manager] 部署涉及監視較長時間以及即時監視的相同部分。 此外也包含定義環境專屬的警報。

### 記錄彙總與報告 {#log-aggregation-and-reporting}

有數個工具可用於彙總記錄，例如Splunk(TM)和Elastic Search、Logstash和Kabana (ELK)。 若要評估您的應用程式 [!DNL Experience Manager] 部署，請務必瞭解系統特定的記錄事件，並根據這些事件建立警報。 瞭解您的開發和營運實務有助於您進一步瞭解如何調整記錄彙總程式，以產生嚴重警報。

### 環境監視 {#environment-monitoring}

環境監視包括監視以下專案：

* 網路輸送量
* 磁碟IO
* 記憶體
* CPU使用率
* JMX MBeans
* 外部網站

您需要外部工具，例如NewRelic(TM)和AppDynamics(TM)來監視每個專案。 使用這些工具，您可以定義系統特定的警示，例如，高系統使用率、工作流程備份、健康狀態檢查失敗，或未驗證的網站存取。 Adobe不建議使用任何優於其他工具的特定工具。 尋找適合您的工具，並用來監視討論的專案。

#### 內部應用程式監視 {#internal-application-monitoring}

內部應用程式監視包括監視組成以下專案的應用程式元件： [!DNL Experience Manager] 棧疊，包括JVM、內容存放庫，以及透過平台上建置的自訂應用程式程式碼進行監控。 一般而言，這項作業是透過JMX Mbeans執行，並可由許多常用的監控解決方案直接監控，例如SolarWinds (TM)、HP OpenView(TM)、Hyperic(TM)、Zabbix(TM)及其他。 對於不支援直接連線至JMX的系統，您可以編寫殼層指令碼來擷取JMX資料，並以這些系統原生可理解的格式將其公開給這些系統。

預設不會啟用JMX Mbean的遠端存取。 如需透過JMX進行監視的詳細資訊，請參閱 [使用JMX技術進行監控和管理](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

在許多情況下，需要基準線來有效地監視統計資料。 若要建立基準線，請在正常工作條件下觀察預先確定的期間，然後識別正常數度。

**JVM監視**

和任何Java應用程式棧疊一樣， [!DNL Experience Manager] 取決於透過底層Java虛擬機器器提供給它的資源。 您可以透過JVM公開的Platform MXBean監視許多這些資源的狀態。 如需有關MXBean的詳細資訊，請參閱 [使用Platform MBean Server和Platform MXBean](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

以下是您可以針對JVM監控的一些基準引數：

記憶體

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* 執行個體：所有伺服器
* 警報臨界值：當棧積或非棧積記憶體使用率超過對應最大記憶體的75%時。
* 警報定義：可能是系統記憶體不足，或是程式碼中有記憶體流失。 分析執行緒傾印以得到定義。

>[!NOTE]
>
>此Bean提供的資訊以位元組表示。

Threads

* MBean： `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* 執行個體：所有伺服器
* 警報臨界值：當執行緒的數目大於基準的150%時。
* 警報定義：可能是因為有作用中的失控程式，或是低效的作業耗用大量資源。 分析執行緒傾印以得到定義。

**監視[!DNL Experience Manager]**

[!DNL Experience Manager] 也會透過JMX公開一組統計資料和作業。 這些功能有助於評估系統健康狀況，並在潛在問題影響使用者之前識別它們。 如需詳細資訊，請參閱 [檔案](/help/sites-administering/jmx-console.md) 於 [!DNL Experience Manager] JMX MBean。

以下是您可以監控的一些基準線引數 [!DNL Experience Manager]：

復寫代理

* MBean： `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* 執行個體：一個作者和所有發佈執行個體（適用於排清代理程式）
* 警報臨界值：當 `QueueBlocked` 是 `true` 或的值 `QueueNumEntries` 大於基準的150%。

* 警報定義：系統中出現封鎖的佇列，表示複製目標已關閉或無法連線。 網路或基礎架構問題通常會導致過多專案排入佇列，進而對系統效能造成負面影響。

>[!NOTE]
>
>對於MBean和URL引數，請取代 `<AGENT_NAME>` 名稱為要監督的復寫代理程式。

工作階段計數器

* MBean： `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL： */system/console/jmx/org.apache.jackrabbit.oak：id=7，name=&quot;OakRepository Statistics&quot;，type*=&quot;RepositoryStats&quot;
* 執行個體：所有伺服器
* 警報臨界值：當開啟的工作階段超過基準線50%以上時。
* 警報定義：工作階段可能會透過程式碼開啟，但絕不會關閉。 隨著時間推移，這種情況可能會慢慢發生，最終導致系統中的記憶體遺失。 雖然系統上的工作階段數應該會波動，但不應持續增加。

健康狀態檢查

可在下列位置使用的健康狀態檢查： [操作控制面板](/help/sites-administering/operations-dashboard.md#health-reports) 有對應的JMX MBean用於監視。 不過，您可以撰寫自訂健康情況檢查，以公開其他系統統計資料。

以下是可協助監控的現成健康情況檢查：

* 系統檢查
   * MBean： `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * 執行個體：一個作者，所有發佈伺服器
   * 警報臨界值：當狀態不是「正常」時
   * 警報定義：其中一個度量的狀態為WARN或CRITICAL。 檢查記錄屬性，以取得問題原因的詳細資訊。

* 復寫佇列

   * MBean： `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * 執行個體：一個作者，所有發佈伺服器
   * 警報臨界值：當狀態不是「正常」時
   * 警報定義：其中一個度量的狀態為WARN或CRITICAL。 檢查記錄屬性，以取得造成問題之佇列的詳細資訊。

* 回應效能

   * MBean： `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * 執行個體：所有伺服器
   * 警示持續時間：當狀態不是「正常」時
   * 警報定義：其中一個度量的狀態為WARN或CRITICAL。 檢查記錄屬性，以取得造成問題之佇列的詳細資訊。

* 查詢效能

   * MBean： `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * 執行個體：一個作者，所有發佈伺服器
   * 警報臨界值：當狀態不是「正常」時
   * 警報定義：一或多個查詢在系統中執行緩慢。 檢查記錄屬性，以取得關於導致問題的查詢的詳細資訊。

* 作用中組合

   * MBean： `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * 執行個體：所有伺服器
   * 警報臨界值：當狀態不是「正常」時
   * 警報定義：系統上存在非使用中或未解析的OSGi組合。 檢查記錄屬性，以取得導致問題的套件組合的相關資訊。

* 日誌錯誤

   * MBean： `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * 執行個體：所有伺服器
   * 警報臨界值：當狀態不是「正常」時
   * 警報定義：記錄檔中有錯誤。 檢查記錄屬性，以取得問題原因的詳細資訊。

## 常見問題與解決方法  {#common-issues-and-resolutions}

在監視過程中，如果您遇到問題，以下提供一些您可以執行的疑難排解工作，以解決的常見問題 [!DNL Experience Manager] 部署：

* 如果使用TarMK，請經常執行Tar壓縮。 如需詳細資訊，請參閱 [維護存放庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* 檢查 `OutOfMemoryError` 記錄。 如需詳細資訊，請參閱 [分析記憶體問題](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).

* 檢查記錄檔中是否有未編制索引的查詢、樹狀結構周遊或索引周遊的參考。 這些表示未編制索引的查詢或索引不足的查詢。 如需最佳化查詢和索引效能的最佳實務，請參閱 [查詢和建立索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* 使用工作流程主控台，驗證您的工作流程是否如預期般執行。 如有可能，請將多個工作流程壓縮為單一工作流程。
* 重新造訪即時監控，並尋找其他瓶頸或任何特定資源的高消費者。
* 調查來自使用者端網路的匯出點，以及匯入點到 [!DNL Experience Manager] 部署網路，包括Dispatcher。 這些通常是瓶頸區域。 如需詳細資訊，請參閱 [資產網路考量事項](/help/assets/assets-network-considerations.md).
* 放大您的 [!DNL Experience Manager] 伺服器。 您的尺寸可能不足 [!DNL Experience Manager] 部署。 Adobe客戶支援可協助您識別伺服器是否過小。
* 檢查 `access.log` 和 `error.log` 發生錯誤時輸入專案的檔案。 尋找可能表示自訂程式碼異常的模式。 將它們新增至您監視的事件清單。
