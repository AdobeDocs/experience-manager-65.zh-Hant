---
title: 如何在JEE伺服器群集上配置和診斷AEM Forms?
description: 瞭解如何在JEE伺服器群集上配置和診斷AEM Forms
exl-id: 230fc2f1-e6e5-4622-9950-dae9449ed3f6
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '4033'
ht-degree: 0%

---

# 在JEE伺服器群集上配置和排除AEM Forms故障 {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## 先決知識 {#prerequisites}

熟悉AEM Forms的JEE 、 JBoss 、 WebSphere和Webogic應用程式伺服器、 Red Hat Linux 、 SUSE Linux 、MicrosoftWindows 、IBMAIX或Sun Solaris作業系統、Oracle、IBMDB2或SQL Server資料庫伺服器和Web環境。

## 用戶級別 {#user-level}

進階

JEE群集上的AEM Forms是一種拓撲，旨在使JEE上的AEM Forms能夠抵御群集節點的故障並擴展系統容量，使其超出單個節點的能力。 群集將多個節點合併到一個共用資料的單個邏輯系統中，並允許事務在執行中跨越多個節點。 群集是在JEE上擴展AEM Forms的最常見方法，因為可以支援處理任何工作負載組合的任何服務組合。 JEE群集上的AEM Forms不一定最適合所有類型的部署，特別是，非群集伺服器負載平衡體系結構在許多情況下可能是合適的。

本文檔旨在討論特定配置要求和您在JEE群集上可能遇到的AEM Forms問題區域。

## 群集中有什麼？ {#what-is-in-cluster}

JEE上的AEM Forms群集節點彼此通信並共用資訊，使群集作為一個整體具有單一一致的配置和應用程式狀態。 在群集內共用資訊以多種不同的方式同時完成，這些方式在不同的上下文中使用。 基本資訊共用方法如下圖所示：

![應用程式伺服器群集](assets/application-server-cluster.jpg)

### 應用程式伺服器群集 {#application-server-cluster}

JEE群集上的AEM Forms依賴於底層應用程式伺服器的群集功能。 應用程式伺服器群集使群集配置能夠作為一個整體進行管理，並提供諸如Java命名和目錄介面(JNDI)之類的低級群集服務，這些服務使軟體元件能夠在群集中彼此查找。 群集服務的複雜程度以及應用程式伺服器所依賴的底層技術相關性。 WebSphere和WebLogic具有複雜的群集管理功能，而JBoss則有非常基本的方法。

### GemFire快取 {#gemfire-cache}

GemFire快取是在每個群集節點中實現的分佈式快取機制。 節點彼此查找並建立單個邏輯快取，該快取在節點之間保持一致。 相互查找的節點聯合在一起，以維護圖1中顯示為雲的單個名義快取。 與GDS和資料庫不同，快取是純名義實體。 實際的快取內容儲存在記憶體中，並儲存在 `LC_TEMP` 目錄。

### 資料庫 {#database}

通過JDBC資料源IDP_DS、EDC_DS等訪問的JEE上的AEM Forms資料庫由群集的所有節點共用。 關於JEE上的AEM Forms狀態的大多數持久資料，如正在進行的事務、與正在進行的事務相關聯的用戶資料、關於系統設定如何設定的資料等，都位於此資料庫中。

### 全局文檔儲存 {#global-document-storage}

全局文檔儲存(GDS)是AEM FormsJEE上的文檔管理器（IDPDocument類）使用的基於檔案系統的儲存區域。 GDS儲存群集的所有節點必須可訪問的短壽命和長壽命檔案。

### 其他項目 {#other-items}

除了這些主要共用資源外，還有其他具有特定群集行為的項目，如Quartz。 Quartz是AEM Forms在JEE上使用的調度子系統，它使用資料庫表來保存其對已調度的內容和正在運行的已調度活動的瞭解。 對於單節點安裝和群集，石英必須進行不同的配置，並且它從JEE設定上的其他AEM Forms得到提示。

## 常見配置問題 {#common-configuration}

在JEE群集上維護或診斷AEM Forms最令人沮喪的一點是，沒有單一位置可以確認群集是否正常。 為了確認集群中的所有設備都運行良好，需要進行一些調查和分析，並根據集群配置的錯誤情況，對集群操作存在多種故障模式。 下圖說明了一個配置不正確的群集，其中多個共用資源被不正確地共用。

![配置不正確的群集](assets/bad-configuration-cluster.png)

要記住的有趣且重要的一點是，您需要熟悉群集的工作方式以及群集中需要查找和驗證的內容種類，即使您不打算在群集中的JEE上運行AEM Forms。 這是因為JEE上的AEM Forms的某些部分可能會採取錯誤操作群集的提示，並採取您不期望的群集行為。

那麼，上圖中的共用配置有什麼問題？ 以下各節介紹了問題：

### (1)GemFire群集配置 {#gemfire-cluster-configuration}

Gemfire快取可能出了幾個問題。 兩種典型情形是：

* 應該能夠找到彼此的節點無法這樣做。

* 不應被群集化的節點可以彼此查找，並在不應該時共用快取。

如果您有要群集的節點，則必須在網路上找到彼此。 預設情況下，它們通過組播UDP消息來完成此操作。 每個節點發送廣播消息通告其存在，並且任何接收此類消息的節點開始與它找到的其他節點通話。 這種自動發現方法很常見，很多類型的軟體和設備都這樣做。

自動發現的一個常見問題是，多播消息可能會被網路過濾，作為網路策略的一部分，或者由於軟體防火牆規則，或者可能根本無法通過節點之間存在的網路進行路由。 由於使UDP自動發現在複雜網路中工作通常比較困難，因此生產部署通常使用一種替代發現方法：TCP定位器。 有關TCP定位器的一般討論可參考文獻。

**我如何知道我是使用定位器還是UDP?**

以下JVM屬性控制GemFire快取用於查找其他節點的方法。

多播設定：

* `adobe.cache.multicast-port`:用於與分佈式系統的其他成員通信的組播埠。 如果此設定為零，則會禁用成員發現和分發的多播。

* `gemfire.mcast-address` （可選）:覆蓋Gemfire使用的預設IP地址。

TCP定位器設定：

* `adobe.cache.cluster-locators`:系統成員用於與正在運行的定位器通信的所有定位器的TCP定位器和TCP定位器埠的IP地址/主機名。

該清單必須包括當前正在使用的所有位置，並且必須為群集系統的每個成員一致地配置。

如果TCP定位器清單為空，則不使用定位器，而使用組播方法。

**如何檢查TCP定位器是否正在運行？**

首先，如果正在使用TCP定位器，則所有群集節點上的JVM屬性中應列出TCP定位器：

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

無需在JEE群集節點上運行AEM Forms上的定位程式 — 如果需要，可以在與群集分開的其他系統上運行。 多個系統可以運行定位器，通常認為最好的做法是將定位器在兩個位置運行，以避免定位器單次故障可能導致群集重新啟動問題。 在運行定位器的每個系統上，您應該能夠使用以下命令驗證這些電腦是否正在運行：

`netstat -an | grep 22345`

預期的回應應是：

`tcp 0 0 *.22345 *.* LISTEN`

另一個驗證命令是：

`ps -ef | grep gemfire`

預期的應答應該是這樣的：

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**如何查看GemFire認為群集中的節點？**

GemFire生成日誌資訊，可用於診斷GemFire快取已發現和採用的群整合員。 這可用於驗證是否找到了所有正確的群整合員，並且沒有發生額外的或不正確的群集節點發現。 GemFire的日誌檔案位於JEE臨時目錄上配置的AEM Forms:

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

後面的數字字串 `adobeZZ_` 是伺服器節點唯一的，因此必須搜索臨時目錄的實際內容。 後面的兩個字元 `adobe` 依賴於應用程式服務類型：或 `wl`。 `jb`或 `ws`。

以下示例日誌顯示了當雙節點群集發現自身時會發生的情況。

在第一個節點AP-HP8上：

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

在另一個節點上，AP-HP7 :

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**如果GemFire正在查找它不應該查找的節點怎麼辦？**

共用公司網路的每個不同群集應使用一組單獨的TCP定位器（如果使用TCP定位器），或使用組播UDP配置的單獨UDP埠號。 由於UDP自動發現是JEE上AEM Forms的預設配置，且同一預設埠33456可能正被多個群集使用，因此不嘗試通信的群集可能會意外地這樣做，例如，生產群集和QA群集應保持獨立，但可能通過UDP多播彼此連接。

在群集引導期間，在GemFire群集不正確的網路中可能發現重複埠時，最常見的情況是。 您可能會發現，引導過程在沒有明確原因的情況下失敗。 通常，會出現以下錯誤：

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

在這種情況下，引導程式正與GemFire一起訪問所需的表，而通過JDBC訪問的表與GemFire返回的快取表資訊之間存在不一致，GemFire返回的表資訊來自具有不同基礎資料庫的其他群集。

雖然在引導期間，重複的埠經常會變得明顯，但是以後可能會出現這種情況，當群集在其他群集的引導發生後關閉，或者當網路配置被更改為使以前隔離的群集（出於多播目的）對彼此可見時，會重新啟動。

要診斷這些情況，最好查看GemFire日誌並仔細考慮是否只找到預期的節點。 要糾正問題，必須改變

`adobe.cache.multicast-port`

屬性到一個或兩個群集上的不同值。

### 2)GDS共用 {#gds-sharing}

GDS共用是在JEE本身的AEM Forms之外的O/S級別配置的，在O/S級別，必須安排相同的共用目錄結構才能用於所有群集節點。 在Windows類型系統上，通常通過設定檔案共用來完成此操作，檔案共用從一個節點到另一個節點，或從遠程檔案系統（如NAS設備）到所有節點。 在UNIX系統上， GDS共用通常通過NFS檔案共用完成，同樣，從一個節點到另一個節點，或從NAS裝置完成。

群集的可能故障模式是此遠程檔案共用不可用或存在細微問題。 遠程裝載可能因網路問題、安全設定或配置不正確而失敗。 系統重新啟動可能導致在幾天或幾週前對配置進行的更改生效，並且這可能導致意外。

**如果NFS共用無法裝載，會發生什麼情況？**

在UNIX上，即使裝載失敗， NFS裝載映射到目錄結構的方式也允許可用的GDS目錄可用。 考慮：

* NAS伺服器：NFS共用資料夾/u01/iapply/livecycle_gds
* 節點1:指向共用資料夾（承載在資料庫伺服器上）的裝載點，位於此處：/u01/iapply/livecycle_gds
* 節點2:指向共用資料夾（承載在資料庫伺服器上）的裝載點，位於此處：/u01/iapply/livecycle_gds

* LCES指定GDS的路徑：/u01/iapply/livecycle_gds

如果節點1上的裝載失敗，目錄結構仍將包含指向空裝載點的路徑/u01/iapply/liveccycle_gds，並且該節點將顯示為正常運行。 但是，由於GDS內容實際上並未與其他節點共用，因此群集將無法正常運行。 這可能發生，也確實發生了，結果是群集以神秘的方式失敗。

最佳做法是安排事情，使Linux裝載點不用作GDS的根，而是用其中的某個目錄作為GDS根：

* 如果您有NFS伺服器，則它可能有一個目錄：/some/storage/lc_cluster_dev/LC_GDS
* 在群集節點上，您有一個裝載點：/u01/iapply/shared
* 裝載nfs_server:/some/storage/lc_cluster_dev/u01/iapply/shared
* 將GDS指向/u01/iapply/shared/LC_GDS

現在，如果由於某種原因裝載未成功，則裸機裝載點不包含LC_GDS目錄，並且您的群集將可預測地失敗，因為它根本找不到任何GDS。

**如何驗證所有節點是否都看到相同的GDS並具有權限？**

通過SSH或telnet到UNIX節點，或通過遠程案頭到Windows系統，以互動式用戶身份訪問每個節點，最好驗證GDS訪問和共用。 您應該能夠導航到每個節點上配置的GDS目錄或檔案系統，並從所有其他節點中可見的每個節點建立test檔案。

請注意JEE上的AEM Forms所使用的用戶ID。 在Windows全包安裝中，這是本地管理員。 在UNIX上，它可以是在啟動指令碼或應用程式伺服器配置中配置的特定服務用戶。 此用戶ID必須能夠在所有節點上均等地建立和操作GDS檔案。

在UNIX系統上， NFS配置通常預設不信任對檔案和對象的根所有權或根訪問權限。 如果您以root用戶身份運行應用程式伺服器，則主要需要在NFS伺服器、裝載檔案的節點上指定選項，或同時指定兩者，以允許雙向訪問和控制由一個節點建立並由另一個節點訪問的檔案。

### （三）資料庫共用 {#database-sharing}

要使群集正常運行，所有群整合員必須共用同一資料庫。 大致來說，這種錯誤的範圍是：

* 意外地在單獨的群集節點上設定IDP_DS、EDC_DS、AdobeDefaultSA_DS或其他所需資料源時不同，因此節點指向不同的資料庫。
* 意外地設定了多個單獨的節點以共用資料庫，而這些節點不應共用。

根據您的應用程式伺服器，JDBC連接在群集範圍中定義可能是自然的，因此不同節點上不能有不同的定義。 但是，在Jboss上，完全可以設定事項，以便資料源（如IDP_DS）指向節點1上的一個資料庫，而指向節點2上的其他資料。

相反的問題實際上更常見 — 即JEE節點上的多個獨立（或群集）的AEM Forms在它們不打算時意外指向同一架構的情況。 當DBA不知不覺地向DEV和QA設定團隊提供JEE資料庫的連接資訊上的單個AEM Forms時，最常發生這種情況，因為他們都沒有意識到DEV和QA實例需要單獨的資料庫。

## 應用程式伺服器群集 {#application-server-cluster-1}

要在JEE群集上成功實現AEM Forms，必須將應用程式伺服器配置為群集並正確運行。 在WebSphere和Weblogic中，這是一個簡單明瞭的、記錄詳實的過程。 在Jboss中，群集配置更易操作，而確保節點配置為充當群集並實際查找和彼此通信可能是一項挑戰。 JBoss內部依賴JGroups,JGroups使用UDP多播來查找和協調對等節點，而GemFire中提到的一些問題可能會發生，例如節點在應該時無法彼此查找，或者在不該時彼此查找。

引用:

* [通過JBoss群集提供高可用性企業服務](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [OracleWebLogic伺服器 — 使用群集](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### 如何檢查JBoss是否正確群集？ {#check-jboss-clustering}

當JBoss啟動時，當發現群整合員時，有關加入群集的節點的INFO級別消息將記錄到日誌檔案/控制台。

如果在運行時通過 — g命令行選項指定了群集名稱，則將看到類似於以下消息的消息：

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### 石英調度器 {#quartz-scheduler}

在大多數情況下，AEM Forms在JEE中使用群集中的內部Quartz調度程式，意在自動遵循JEE上AEM Forms的全局群集配置。 但是，#2794033存在一個錯誤，如果TCP定位器用於Gemfire而不是多播自動發現，則會導致Quartz的自動群集配置失敗。 在這種情況下，Quartz將錯誤地以非群集模式運行。 這將在Quartz表中產生死鎖和資料損壞。 8.2.x版的副作用比9.0版更嚴重，因為石英並未被使用太多，但仍然存在。

解決此問題的方法如下：8.2.1.2 QF2.143和9.0.0.2 QF2.44。

還有一種解決方法，即設定以下兩個屬性：

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

請注意，一個設定使用「cluster」和「locators」之間的句點，另一個設定使用連字元。 這比應用軟體補丁程式容易實現，風險也小，但它涉及人為地建立令人困惑的、命名錯誤的附加配置設定。

### 如何檢查Quartz是否作為單個節點或群集運行？ {#check-quartz}

要確定Quartz如何配置自己，您必須查看AEM Forms在JEE調度程式服務上在啟動期間生成的消息。 這些消息在INFO嚴重性下生成，可能需要調整日誌級別並重新啟動才能獲取消息。 在AEM FormsJEE啟動序列中，Quartz初始化以以下行開始：

資訊  `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad在日誌中查找第一行非常重要，因為某些應用程式伺服器也使用Quartz，並且它們的Quartz實例不應與AEM Forms在JEE Scheduler服務上使用的實例混淆。 這表示計畫程式服務正在啟動，其後的行將告訴您它是否正在群集模式下啟動。 此序列中顯示了幾條消息，這是最後一條「已啟動」消息，顯示了Quartz的配置方式：

這裡給出了Quartz實例的名稱： `IDPSchedulerService_$_ap-hp8.ottperflab.adobe.com1312883903975`。 調度程式的Quartz實例的名稱將始終以字串開頭 `IDPSchedulerService_$_`。 附加到此結尾的字串將告訴您Quartz是否在群集模式下運行。 從節點主機名和長數字字串生成的長唯一標識符，此處 `ap-hp8.ottperflab.adobe.com1312883903975`，表示它在群集中運行。 如果它以單個節點運行，則標識符將為兩位數，「20」：

資訊  `[org.quartz.core.QuartzScheduler]` 調度程式 `IDPSchedulerService_$_20` 。
必須對所有群集節點分別執行此檢查，因為每個節點的調度程式獨立地確定是否以群集模式運行。

### 如果Quartz以錯誤的模式運行，會導致哪些問題？ {#quartz-running-in-wrong-mode}

如果Quartz設定為以單個節點運行，但實際運行在群集中並與其他節點共用Quartz資料庫表，這將導致AEM Forms在JEE調度程式服務上的不可靠操作，並且通常伴有資料庫死鎖。 這是一種非常典型的堆棧跟蹤，您可能會在這種情況下看到：

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Couldn't remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### 如何同步群集中的系統時鐘？ {#ynchronize-system-clocks-cluster}

對於一個集群來說，必須使所有集群節點上的時鐘保持緊密的同步。 手工操作無法充分完成，必須通過非常經常運行的某種形式的時間同步服務來完成。 所有節點上的時鐘必須彼此在一秒內。 最佳做法要求不僅群集節點，而且負載平衡器、資料庫伺服器、 GDS NAS伺服器和任何其他元件都同步。

Windows時間同步通常為域控制器。 UNIX系統可以使用NTP將其同步到其他時間源。 如果可能，最好將所有系統(包括JEE節點上的AEM Forms和其他系統元件)同步到同一源。

即使在最臨時的test環境中，手動設定節點上的時鐘也是遠遠不夠的。 手動設定時鐘不會提供足夠精確的同步，並且兩個節點上的時鐘不可避免地會彼此漂移，即使只在一天的時間內。 主動時間同步機制是可靠集群運行的關鍵。

### 負載平衡器 {#load-balancer}

提供用戶交互服務的群集的一個典型要求是HTTP負載平衡器，它將在群集中分發HTTP請求。 在JEE群集上成功使用具有AEM Forms的負載平衡器需要配置以下內容：

* 會話粘性

* URL重寫規則

* 節點健康檢查

### 我應該如何處理負載平衡器運行狀況檢查功能？ {#load-balancer-health-check}

可以將某些負載平衡器配置為對負載平衡的節點執行定期運行狀況檢查。 通常，這是負載平衡器將嘗試訪問的應用程式函式的URL。 如果負載成功，則假定節點是健康的，並保留在負載平衡集中。 如果URL載入失敗，則假定節點有故障，並從集中刪除。 通常，運行狀況檢查URL只是連接到JEE AdminUI登錄頁上的AEM Forms。 這不是群整合員的理想運行狀況檢查，最好是實施一個短時間的進程並使用REST API URL作為運行狀況檢查函式。

## 臨時檔案路徑和類似的群集設定 {#temporary-file-path-cluster-settings}

在JEE上，AEM Forms內的某些檔案路徑設定是在群集範圍內建立的，並且在每個節點上具有相同的有效設定，但在每個節點上都獨立解釋以引用本地檔案。 要考慮的關鍵是字型路徑設定和臨時目錄設定。 轉到AdminUI核心配置螢幕（首頁>設定>核心繫統>核心配置）

應檢查以下設定：

1. 臨時目錄的位置
1. Adobe伺服器字型目錄的位置
1. 客戶字型目錄的位置
1. 系統字型目錄的位置
1. 資料服務配置檔案的位置

群集中每個配置設定只有一個路徑設定。 例如，您的臨時目錄位置可能是 `/home/project/QA2/LC_TEMP`。 在群集中，每個節點實際上都必須可以訪問此特定路徑。 如果一個節點具有預期的臨時檔案路徑，而另一個節點沒有，則無法正常工作的節點將無法正常工作。

雖然這些檔案和路徑可以在節點之間共用或單獨放置，或在遠程檔案系統上，但通常最好是在本地節點磁碟儲存上提供本地副本。

尤其不應在節點之間共用臨時目錄路徑。 應使用與用於驗證GDS的過程類似的過程來驗證臨時目錄是否未共用：轉到每個節點，在路徑設定指示的路徑中建立一個臨時檔案，然後驗證其他節點不共用該檔案。 臨時目錄路徑應引用每個節點上的本地磁碟儲存（如果可能），並應選中。

對於每個路徑設定，確保該路徑實際存在，並且可從群集中的每個節點訪問，使用JEE上運行的AEM Forms所依據的有效使用標識。 字型目錄內容必須可讀。 臨時目錄必須允許讀、寫和控制。
