---
title: 如何在JEE伺服器叢集上設定和疑難排解AEM Forms?
description: 了解如何在JEE伺服器叢集上設定和疑難排解AEM Forms
exl-id: 230fc2f1-e6e5-4622-9950-dae9449ed3f6
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '4033'
ht-degree: 0%

---

# 在JEE伺服器叢集上設定和疑難排解AEM Forms {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## 必備知識 {#prerequisites}

熟悉JEE、JBoss、WebSphere和Webogic應用程式伺服器、Red Hat Linux、SUSE Linux、Microsoft Windows、IBM AIX或Sun Solaris作業系統、Oracle、IBM DB2或SQL Server資料庫伺服器以及Web環境上的AEM Forms。

## 使用者層級 {#user-level}

進階

JEE叢集上的AEM Forms是一種拓撲，其設計目的是讓JEE上的AEM Forms能夠抵御叢集節點的故障，並擴展系統容量，使其超出單一節點的能力。 群集將多個節點合併到單個邏輯系統中，該邏輯系統共用資料並允許事務在執行時跨越多個節點。 叢集是在JEE上擴充AEM Forms的最一般方式，因為可支援處理任何工作負載組合的任何服務組合。 JEE叢集上的AEM Forms不一定最適合所有類型的部署，尤其是非叢集伺服器負載平衡架構在許多情況下可能最合適。

本檔案旨在討論JEE叢集上AEM Forms的特定設定需求和可能遇到的問題。

## 叢集中有什麼？ {#what-is-in-cluster}

JEE叢集節點上的AEM Forms彼此通訊並共用資訊，讓叢集整體具備單一一致的設定和應用程式狀態。 在群集內以多種不同方式同時共用資訊，這些方式用於不同的上下文。 下圖說明了基本資訊共用方法：

![應用程式伺服器群集](assets/application-server-cluster.jpg)

### 應用程式伺服器群集 {#application-server-cluster}

JEE叢集上的AEM Forms需仰賴基礎應用程式伺服器的叢集功能。 應用程式伺服器群集使群集配置能夠作為一個整體進行管理，並提供諸如Java命名和目錄介面(JNDI)之類的低級群集服務，使軟體元件能夠在群集中互相查找。 群集服務的複雜程度以及應用程式伺服器所依賴的底層技術依賴性。 WebSphere和WebLogic具有複雜的群集管理功能，而JBoss則具有非常基本的方法。

### GemFire快取 {#gemfire-cache}

GemFire快取是在每個群集節點中實現的分佈式快取機制。 節點之間互相查找，並構建一個在節點之間保持一致的邏輯快取。 互相查找的節點聯在一起，以維護圖1中顯示為雲的單個名義快取。 與GDS和資料庫不同，快取是純名義實體。 實際快取內容儲存在記憶體中，並儲存在每個群集節點的`LC_TEMP`目錄中。

### 資料庫 {#database}

JEE資料庫上的AEM Forms（通過JDBC資料源IDP_DS、EDC_DS和其他方式訪問）由群集的所有節點共用。 關於JEE上AEM Forms狀態的大部分持續性資料，例如正在進行的交易、與持續交易相關聯的使用者資料、關於如何設定系統設定的資料等，都位於此資料庫中。

### 全局文檔儲存 {#global-document-storage}

全域檔案儲存(GDS)是以檔案系統為基礎的儲存區域，由JEE上AEM Forms內的檔案管理員（IDPDocument類別）使用。 GDS儲存短期和長期檔案，這些檔案必須可供群集的所有節點訪問。

### 其他項目 {#other-items}

除了這些主要共用資源外，還有其他具有特定叢集行為的項目，例如Quartz。 Quartz是AEM Forms在JEE上使用的排程器子系統，它使用資料庫表來掌握已排程的項目和已排程的活動執行情況。 針對單節點安裝和叢集，石英的配置必須不同，而且JEE設定中會收到其他AEM Forms的提示。

## 常見配置問題 {#common-configuration}

在JEE叢集上維護或疑難排解AEM Forms最令人沮喪的一點，就是沒有單一位置可以正確確認叢集是否正常。 要確認集群中的所有設備都完好，需要進行一些調查和分析，並根據集群配置的錯誤情況，對集群操作存在多種故障模式。 下圖顯示了配置不正確的群集，其中多個共用資源被不當共用。

![配置不正確的群集](assets/bad-configuration-cluster.png)

要記住的有趣且重要的一點是，您需要熟悉叢集的運作方式，以及叢集中要尋找和驗證的項目類型，即使您不打算在叢集中於JEE上執行AEM Forms。 這是因為JEE上的AEM Forms某些部分可能會拿出錯誤運作叢集的提示，採取您不期望的叢集行為。

那麼，上圖中的共用配置有什麼問題？ 以下幾節將說明問題：

### (1)GemFire群集配置 {#gemfire-cluster-configuration}

Gemfire快取可能會發生數個錯誤。 兩種典型情況為：

* 應該能夠彼此找到的節點無法找到。

* 不應被群集的節點彼此查找，並在不應該共用快取時共用快取。

如果您有要群集的節點，則必須在網路上找到彼此。 預設情況下，它們通過多播UDP消息來執行此操作。 每個節點發送廣告消息，通告其存在，任何接收這種消息的節點開始與它找到的其他節點通話。 這種自動發現的方法很常見，許多類型的軟體和設備都這樣做。

自動發現的一個常見問題是，多播消息可能被網路過濾為網路策略的一部分或由於軟體防火牆規則，或者可能根本無法通過節點之間存在的網路進行路由。 由於使UDP自動發現在複雜網路中工作通常比較困難，生產部署使用替代發現方法是常見的做法：TCP定位器。 在參考中可以找到TCP定位器的一般性討論。

**如何知道我是使用定位器還是UDP?**

以下JVM屬性控制GemFire快取查找其他節點時使用的方法。

多播設定：

* `adobe.cache.multicast-port`:用於與分佈式系統的其他成員通信的多播埠。如果此設定為零，則會禁用成員發現和分發的多播。

* `gemfire.mcast-address` （可選）:覆寫Gemfire使用的預設IP位址。

TCP定位器設定：

* `adobe.cache.cluster-locators`:系統成員用於與運行的定位器通信的所有定位器的TCP定位器和TCP定位器埠的IP地址/主機名。

該清單必須包含當前使用的所有位置，並且必須為群集系統的每個成員進行一致配置。

如果TCP定位器清單為空，則不使用定位器，而是使用多播方法。

**如何檢查我的TCP定位器是否正在運行？**

首先，如果正在使用TCP定位器，則所有群集節點上的JVM屬性中應列出您的TCP定位器：

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

不必在JEE叢集節點上在AEM Forms上執行定位程式，也可以視需要在與叢集不同的其他系統上執行。 多個系統可以運行定位器，通常認為最好讓定位器在兩個位置運行，以防定位器的單個故障可能導致群集重新啟動問題。 在運行定位器的每個系統上，您應該能夠使用以下命令來驗證它們是否在這些電腦上運行：

`netstat -an | grep 22345`

預期的回應應為：

`tcp 0 0 *.22345 *.* LISTEN`

另一個驗證命令是：

`ps -ef | grep gemfire`

預期的回應應如下所示：

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**如何看到GemFire認為群集中有哪些節點？**

GemFire會生成日誌資訊，這些資訊可用於診斷GemFire快取發現和採用的群整合員。 這可用來驗證是否找到了所有正確的群整合員，並且沒有發生額外的或不正確的群集節點發現。 GemFire的記錄檔位於JEE臨時目錄中已設定的AEM Forms :

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

`adobeZZ_`之後的數值字串對於伺服器節點是唯一的，因此您必須搜索臨時目錄的實際內容。 `adobe`之後的兩個字元取決於應用程式伺服器類型：`wl`、`jb`或`ws`。

下列範例記錄顯示雙節點叢集發現自身時會發生什麼事。

在第一個節點上，AP-HP8:

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

**如果GemFire找到不該找到的節點呢？**

共用公司網路的每個不同群集都應使用一組單獨的TCP定位器（如果使用了TCP定位器），或者使用多播UDP配置時使用一個單獨的UDP埠號。 由於UDP自動發現是JEE上AEM Forms的預設配置，且同一預設埠33456可能被多個群集使用，因此不應嘗試通信的群集可能會意外地這樣做 — 例如，生產群集和QA群集應保持獨立，但可通過UDP多播相互連接。

在群集的引導過程中，最常見的情況是，在GemFire未正確群集的網路中可能發現重複的埠。 您可能會發現，引導過程失敗，但沒有明確的原因。 通常會出現下列錯誤：

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

在這種情況下，bootstrapper正與GemFire協作以訪問所需表，通過JDBC訪問的表與GemFire返回的快取表資訊之間存在不一致，快取表資訊來自具有不同基礎資料庫的不同群集。

雖然重複埠在引導期間通常會變得明顯，但是，在其他群集的引導出現時，當群集在關閉後重新啟動，或當網路配置更改為使先前為多播目的而隔離的群集彼此可見時，這種情況有可能在以後顯示。

要診斷這些情況，最好查看GemFire日誌，並仔細考慮是否只找到預期的節點。 要糾正此問題，必須更改

`adobe.cache.multicast-port`

屬性中的任何一個或兩個叢集上的不同值。

### 2)GDS共用 {#gds-sharing}

GDS共用是在JEE本身的AEM Forms外部設定，在O/S層級，您必須安排相同的共用目錄結構才能供所有叢集節點使用。 在Windows類型系統上，通常通過設定一個檔案共用來完成，該檔案共用可以從一個節點到另一個節點，也可以從一個遠程檔案系統（如NAS設備）到所有節點。 在UNIX系統上， GDS共用通常通過NFS檔案共用來完成，同樣，從一個節點到另一個節點，或從NAS設備完成。

群集可能的故障模式是，此遠程檔案共用不可用或存在細微問題。 遠程裝載可能因網路問題、安全設定或配置錯誤而失敗。 系統重新啟動可能會導致在事前幾天或幾週所做的配置更改生效，並且這可能導致意外。

**如果NFS共用無法裝載，會發生什麼？**

在UNIX上，將NFS裝載映射到目錄結構的方式允許使用看似可用的GDS目錄，即使裝載失敗也是如此。 請考慮：

* NAS伺服器：NFS共用資料夾/u01/iapply/livecycle_gds
* 節點1:位於以下位置的共用資料夾（托管在資料庫伺服器上）的裝載點：/u01/iapply/livecycle_gds
* 節點2:位於以下位置的共用資料夾（托管在資料庫伺服器上）的裝載點：/u01/iapply/livecycle_gds

* LCES指定GDS的路徑：/u01/iapply/livecycle_gds

如果節點1上的裝載失敗，目錄結構仍將包含指向空裝載點的路徑/u01/iapply/livecycle_gds，且該節點將顯示為正確運行。 但是，由於GDS內容實際上並未與其他節點共用，因此群集將無法正常運行。 這可能而且確實會發生，結果是叢集以神秘的方式失敗。

最佳做法是安排事項，使Linux裝載點不作為GDS的根，而是作為GDS根，其中的某個目錄作為GDS根：

* 如果您有NFS伺服器，則可能有目錄：/some/storage/lc_cluster_dev/LC_GDS
* 在群集節點上，您有一個裝載點：/u01/iapply/shared
* 裝載nfs伺服器(_S):/some/storage/lc_cluster_dev/u01/iapply/shared
* 將GDS指向/u01/iapply/shared/LC_GDS

現在，如果由於某種原因裝載未成功，則裸裝載點不包含LC_GDS目錄，並且您的群集將可預測地失敗，因為它根本找不到任何GDS。

**如何確認所有節點都看到相同的GDS並擁有權限？**

通過SSH或telnet到UNIX節點，或通過遠程案頭到Windows系統，以互動用戶身份訪問每個節點，最好驗證GDS訪問和共用。 您應該能夠導航到每個節點上配置的GDS目錄或檔案系統，並從所有其他節點中可見的每個節點建立測試檔案。

請注意AEM Forms在JEE上運作時所使用的使用者ID。 在Windows全包安裝中，這是本地管理員。 在UNIX上，它可能是在啟動指令碼或應用程式伺服器配置中配置的特定服務用戶。 此用戶ID必須能夠在所有節點上均等地建立和操作GDS檔案。

在UNIX系統上，NFS配置通常預設不信任對檔案和對象的根所有權或根訪問權限。 如果您以超級用戶身份運行應用程式伺服器，則主要需要在NFS伺服器、裝載檔案的節點或兩者上指定選項，以允許雙邊訪問和控制由一個節點建立並由另一個節點訪問的檔案。

### （三）資料庫共用 {#database-sharing}

要使群集正常工作，所有群整合員必須共用同一資料庫。 大致而言，這種錯誤的可能性是：

* 意外地在不同的群集節點上設定了IDP_DS、EDC_DS、AdobeDefaultSA_DS或其他所需的資料源，使節點指向不同的資料庫。
* 意外設定了多個不應共用資料庫的獨立節點。

根據您的應用程式伺服器，JDBC連接在群集作用域中定義可能是自然的，因此不同節點上不能有不同的定義。 不過，在Jboss上，完全可以設定項目，讓IDP_DS等資料來源指向節點1上的一個資料庫，但指向節點2上的其他資料。

相反的問題其實更常見，也就是說，JEE節點上的多個獨立（或叢集）AEM Forms節點無意中指向同一個架構的情況。 最常發生的情況是，DBA不知不覺地向DEV和QA設定團隊發佈了JEE資料庫上的單個AEM Forms的連接資訊，但沒有一個DBA意識到DEV和QA實例需要單獨的資料庫。

## 應用程式伺服器群集 {#application-server-cluster-1}

若要在JEE叢集上成功部署AEM Forms，必須將應用程式伺服器設定為叢集並正確運作。 在WebSphere和Weblogic中，這是一個簡單明瞭的、記錄有效的過程。 在Jboss中，群集配置更實際，而確保節點配置為充當群集，並且實際上彼此查找和通信可能是一項挑戰。 JBoss內部依賴JGroup,JGroup使用UDP多播來查找並協調對等節點，而GemFire中提到的一些問題可能發生，例如節點在應該時無法彼此查找，或者在不應該時彼此查找。

引用:

* [通過JBoss群集提供高可用性企業服務](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [OracleWebLogic伺服器 — 使用群集](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### 如何檢查JBoss是否正確叢集？ {#check-jboss-clustering}

當JBoss啟動時，當發現群整合員時，有關加入叢集的節點的INFO級別消息將記錄到日誌檔案/控制台。

如果在運行時通過 — g命令行選項指定了群集名稱，您將看到類似以下的消息：

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### 石英排程器 {#quartz-scheduler}

在大部分情況下，JEE上的AEM Forms在叢集中使用內部Quartz排程器，一般是要自動遵循JEE上AEM Forms的全域叢集設定。 但是，存在#2794033錯誤，如果TCP定位器用於Gemfire而不是多播自動發現，則會導致Quartz的自動群集配置失敗。 在這種情況下，Quartz將不正確地以非群集模式運行。 這將在Quartz表中產生死鎖和資料損壞。 在8.2.x版中，副作用比9.0版更嚴重，因為石英沒有使用太多，但仍然存在。

針對此問題提供下列修正：8.2.1.2 QF2.143和9.0.0.2 QF2.44。

此外也有一個解決方案，即設定這兩個屬性：

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

請注意，某個設定使用「叢集」和「定位器」之間的句號，另一個則使用連字型大小。 與應用軟體補丁程式相比，這易於實施，風險也更低，但它涉及人為地建立一個令人困惑的、名稱錯誤的配置設定。

### 如何檢查Quartz是否作為單個節點或群集運行？ {#check-quartz}

若要判斷Quartz如何自行設定，您必須查看AEM Forms在JEE排程器服務上於啟動期間產生的訊息。 這些消息在INFO嚴重性時生成，可能需要調整日誌級別並重新啟動才能獲取消息。 在JEE上的AEM Forms啟動序列中，Quartz初始化從以下行開始：

INFO `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad
請務必在記錄中找出第一行，因為某些應用程式伺服器也使用Quartz，且其Quartz例項不應與AEM Forms在JEE排程器服務上使用的例項混淆。 這表示調度程式服務正在啟動，其後面的線路將告訴您它是否在群集模式下正確啟動。 此序列中會顯示多條消息，這是顯示Quartz配置方式的最後一條「已啟動」消息：

此處提供了Quartz實例的名稱：`IDPSchedulerService_$_ap-hp8.ottperflab.adobe.com1312883903975`。 調度程式的Quartz實例的名稱將始終以字串`IDPSchedulerService_$_`開頭。 附加到此結尾的字串將告訴您Quartz是否在群集模式下運行。 從節點的主機名和長位字串（此處`ap-hp8.ottperflab.adobe.com1312883903975`）生成的長唯一標識符指示它正在群集中運行。 如果以單一節點運作，則識別碼會是兩位數字「20」：

INFO `[org.quartz.core.QuartzScheduler]`計畫程式`IDPSchedulerService_$_20`已啟動。
必須對所有群集節點單獨執行此檢查，因為每個節點的調度程式獨立地確定是否在群集模式下運行。

### 如果Quartz以錯誤的模式運行，會導致哪些問題？ {#quartz-running-in-wrong-mode}

如果Quartz設定為以單個節點運行，但實際運行在群集中，並與其他節點共用Quartz資料庫表，則這將導致AEM Forms在JEE調度程式服務上的不可靠操作，並且通常伴隨著資料庫死鎖。 這是相當典型的堆棧跟蹤，在此情況下可能會看到：

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

為了使群集平穩運行，所有群集節點上的時鐘必須緊密同步。 手工操作無法充分完成，必須通過某種定期運行的時間同步服務來完成。 所有節點上的時鐘必須位於彼此的一秒內。 最佳做法要求不僅群集節點，而且還要同步負載平衡器、資料庫伺服器、 GDS NAS伺服器和任何其他元件。

Windows時間同步通常為域控制器。 UNIX系統可以使用NTP同步到不同的時間源。 最好將所有系統(包括JEE節點上的AEM Forms和其他系統元件)同步到同一源（如果可能）。

即使在最臨時的測試環境中，手動設定節點上的時鐘也絕對不夠。 手動設定時鐘不會提供足夠精確的同步，而且兩個節點上的時鐘不可避免地會彼此相對漂移，即使只在一天的時間內。 主動時間同步機制對於可靠的集群運行至關重要。

### 負載平衡器 {#load-balancer}

提供使用者互動式服務的叢集的典型需求，是將在整個叢集中分發HTTP要求的HTTP負載平衡器。 在JEE叢集上成功搭配AEM Forms使用負載平衡器時，需要設定下列項目：

* 工作階段黏著度

* URL重寫規則

* 節點健康檢查

### 我該如何處理負載平衡器運行狀況檢查功能？ {#load-balancer-health-check}

某些負載平衡器可配置為對負載平衡的節點執行定期運行狀況檢查。 通常，這是負載平衡器將嘗試存取之應用程式函式的URL。 如果負載成功，則假設節點運行良好，並保留在負載平衡集中。 如果URL無法載入，系統會假設節點有錯誤，並從集中刪除。 一般而言，健康狀況檢查URL只會連線至JEE AdminUI登入頁面上的AEM Forms。 這不是群整合員的理想運行狀況檢查，最好實施短期進程並使用REST API URL作為運行狀況檢查函式。

## 臨時檔案路徑和類似的群集設定 {#temporary-file-path-cluster-settings}

JEE上的AEM Forms中，某些檔案路徑設定會在叢集範圍內建立，且在每個節點上都有相同的有效設定，但會在每個節點上獨立解譯，以參照本機檔案。 需要考慮的關鍵字是字型路徑設定和臨時目錄設定。 前往「AdminUI核心設定」畫面（首頁>設定>核心繫統>核心設定）

應檢查下列設定：

1. 臨時目錄的位置
1. Adobe伺服器字型目錄的位置
1. 客戶字型目錄的位置
1. 系統字型目錄的位置
1. 資料服務配置檔案的位置

群集中每個配置設定只有一個路徑設定。 例如，您的Temp目錄位置可能是`/home/project/QA2/LC_TEMP`。 在群集中，每個節點實際上都必須具有此特定路徑的可訪問性。 如果一個節點有預期的臨時檔案路徑，而另一個節點沒有，則無法正常運作的節點。

雖然這些檔案和路徑可以在節點之間共用或單獨定位，或在遠程檔案系統上共用，但通常最佳做法是它們是本地節點磁碟儲存上的本地副本。

特別是，節點之間不應共用臨時目錄路徑。 應使用與所述驗證GDS的過程類似的過程來驗證臨時目錄是否未共用：轉至每個節點，在路徑設定指示的路徑中建立臨時檔案，然後驗證其他節點是否不共用該檔案。 臨時目錄路徑應引用每個節點上的本地磁碟儲存（如果可能），並應被檢查。

對於每個路徑設定，請確定路徑實際存在，並且可從叢集中的每個節點存取，使用AEM Forms在JEE上執行時所使用的有效使用身分識別。 字型目錄內容必須可讀。 臨時目錄必須允許讀取、寫入和控制。
