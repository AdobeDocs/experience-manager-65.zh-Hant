---
title: 如何使用TarMK冷待命執行AEM
description: 瞭解如何建立、設定和維護TarMK冷待命設定。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '2666'
ht-degree: 0%

---

# 如何使用TarMK冷待命執行AEM{#how-to-run-aem-with-tarmk-cold-standby}

## 簡介 {#introduction}

Tar微核心的冷待命容量可讓一或多個待命Adobe Experience Manager (AEM)執行個體連線到主要執行個體。 同步處理只是一種方式，表示它只能從主要執行個體到待命執行個體完成。

待命執行個體的目的是保證主存放庫的即時資料副本，並確保在主存放庫因任何原因無法使用時，能夠快速切換資料，而不會遺失資料。

內容會在主要執行個體和待命執行個體之間線性同步，而不會對檔案或存放庫損毀進行任何完整性檢查。 因為此設計，待命執行個體是主要執行個體的精確副本，無法協助緩解主要執行個體上的不一致。

>[!NOTE]
>
>「冷待命」功能旨在保護&#x200B;**作者**&#x200B;執行個體上需要高可用性的情況。 對於使用Tar Micro Kernel的&#x200B;**Publish**&#x200B;執行個體需要高可用性的情況，Adobe建議使用發佈陣列。
>
>如需更多可用部署的資訊，請參閱[建議的部署](/help/sites-deploying/recommended-deploys.md)頁面。

>[!NOTE]
>
>當設定「待命」執行處理，或從「主要」節點衍生時，它只允許存取下列主控台（用於管理相關活動）：
>
>* OSGI Web主控台
>
>無法存取其他主控台。

## 運作方式 {#how-it-works}

在主要的AEM執行個體上，會開啟TCP連線埠並聆聽傳入的訊息。 目前，從屬端傳送給主屬端的訊息有兩種型別：

* 要求目前標題的區段ID的訊息
* 要求具有指定ID之區段資料的訊息

待命會定期要求主要磁碟機目前磁頭的區段ID。 如果區段在本機不明，則會擷取該區段。 如果已存在，則會比較區段並在必要時請求引用的區段。

>[!NOTE]
>
>待命執行個體未收到任何型別的請求，因為它們僅以同步模式執行。 待命執行個體上唯一可用的區段是Web主控台，以便於套件組合和服務組態。

典型的TarMK冷待命部署：

![chlimage_1](assets/chlimage_1.png)

## 其他特性 {#other-characteristics}

### 穩健性 {#robustness}

資料流程的設計可自動偵測及處理連線及網路相關問題。 所有封包都隨檢查加和一起捆綁，當連線發生問題或封包損壞時，會觸發重試機制。

#### 效能 {#performance}

在主要執行個體上啟用TarMK冷待命幾乎對效能沒有可衡量的影響。 額外的CPU耗用量很低，額外的硬碟和網路IO應該不會產生效能問題。

在待命狀態下，您可能會在同步處理期間耗用大量的CPU。 因為程式不是多執行緒，所以使用多核心無法加快速度。 如果未變更或傳輸任何資料，則沒有可測量的活動。 連線速度視硬體與網路環境而異，但並不取決於存放庫的大小或SSL使用。 在預估初始同步所需的時間或在主要節點上同時變更許多資料時，請記住這一點。

#### 安全性 {#security}

假設所有執行個體都在相同的內部網路安全性區域中執行，安全性違規的風險就會大幅降低。 不過，您可以透過啟用從裝置與主裝置之間的SSL連線來新增額外的安全層。 如此一來，資料就有可能被中間人破壞。

此外，您可以限制傳入要求的IP位址，以指定允許連線的待命執行個體。 這應該有助於保證內部網路中的任何人都無法複製存放庫。

>[!NOTE]
>
>建議在Dispatcher與冷待命設定中的伺服器之間新增負載平衡器。 負載平衡器應設定為僅將使用者流量導向至&#x200B;**主要**&#x200B;執行個體。 這是確保一致性，並防止透過冷待命機制以外的方式在待命執行個體上複製內容所必需的。

## 建立AEM TarMK冷待命設定 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>與先前版本相比，AEM 6.3中區段節點存放區和待命存放區服務的PID已變更，如下所示：
>
>* 從org.apache.jackrabbit.oak.將&#x200B;**plugins**.segment.standby.standby.store.StandbyStoreService新增至org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* 從org.apache.jackrabbit.oak.將&#x200B;**plugins**.segment.SegmentNodeStoreService新增至org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>進行必要的設定調整，以反映此變更。

若要建立TarMK冷待命設定，請先執行主要安裝資料夾的整個檔案系統複製到新位置，以建立待命執行處理。 然後，您可以使用指定其角色（ `primary`或`standby`）的執行模式來啟動每個執行個體。

以下是建立具有一個主要執行個體和一個待命執行個體的設定所必須遵循的程式：

1. 安裝AEM。

1. 關閉執行個體，並將其安裝資料夾複製到執行冷待命執行個體的位置。 即使您是從不同的電腦執行，請務必為每個資料夾指定描述性名稱（例如&#x200B;*aem-primary*&#x200B;或&#x200B;*aem-standby*），以區別執行個體。
1. 移至主要執行個體的安裝資料夾，並：

   1. 檢查並刪除任何您在`aem-primary/crx-quickstart/install`下可能有的先前OSGi設定

   1. 在`aem-primary/crx-quickstart/install`下建立名為`install.primary`的資料夾

   1. 為`aem-primary/crx-quickstart/install/install.primary`下偏好的節點存放區和資料存放區建立必要的設定
   1. 在相同位置建立名為`org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`的檔案，並加以設定。 如需組態選項的詳細資訊，請參閱[組態](/help/sites-deploying/tarmk-cold-standby.md#configuration)。

   1. 如果您搭配外部資料存放區使用AEM TarMK執行個體，請在`aem-primary/crx-quickstart/install`下建立名為`crx3`的資料夾`crx3`

   1. 將資料存放區組態檔放在`crx3`資料夾中。

   例如，如果您使用外部檔案資料存放區來執行AEM TarMK執行個體，則需要下列組態檔：

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   在下方尋找主要執行個體的設定範例：

   ****&#x200B;的範例&#x200B;**org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config的範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config的範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 啟動主要執行模式，確定您指定主要執行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 為&#x200B;**org.apache.jackrabbit.oak.segment**&#x200B;封裝建立Apache Sling記錄記錄記錄器。 將記錄層級設為[偵錯]，並將其記錄輸出指向個別的記錄檔，例如&#x200B;*/logs/tarmk-coldstandby.log*。 如需詳細資訊，請參閱[記錄](/help/sites-deploying/configure-logging.md)。
1. 移至&#x200B;**待命**&#x200B;執行個體的位置，然後執行jar來啟動它。
1. 建立與主要記錄檔相同的記錄設定。 接著，停止執行個體。
1. 接下來，準備待命執行個體。 您可以透過執行與主要執行處理相同的步驟來執行此操作：

   1. 刪除您在`aem-standby/crx-quickstart/install`下可能有的任何檔案。
   1. 在`aem-standby/crx-quickstart/install`下建立名為`install.standby`的資料夾

   1. 建立兩個組態檔，稱為：

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. 在`aem-standby/crx-quickstart/install`下建立名為`crx3`的資料夾

   1. 建立資料存放區組態，並將其放在`aem-standby/crx-quickstart/install/crx3`下。 在此範例中，您必須建立的檔案為：

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. 編輯檔案並建立必要的設定。

   以下是典型待命執行個體的組態檔範例：

   **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config的範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config的範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config的範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 使用待命執行模式啟動&#x200B;**待命**&#x200B;執行個體：

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

您也可以透過Web主控台以下列方式設定服務：

1. 前往網頁主控台： *https://serveraddress:serverport/system/console/configMgr*
1. 正在尋找名為&#x200B;**Apache Jackrabbit Oak Segment Tar Cold Standby Service**&#x200B;的服務，並連按兩下以編輯設定。
1. 儲存設定，然後重新啟動執行個體，新設定即可生效。

>[!NOTE]
>
>您可以隨時檢查Sling設定Web主控台中&#x200B;**主要**&#x200B;或&#x200B;**待命**&#x200B;執行模式是否存在，以檢查執行個體的角色。
>
>您可以前往&#x200B;*https://localhost:4502/system/console/status-slingsettings*&#x200B;並檢查&#x200B;**「執行模式」**&#x200B;行來完成此操作。

## 首次同步處理 {#first-time-synchronization}

準備完成且首次啟動待命後，當待命到主要位置為止時，執行個體之間會存在大量網路流量。 您可以參閱記錄檔來觀察同步化的狀態。

在待命&#x200B;*tarmk-coldstandby.log*&#x200B;中，您可以看到下列專案：

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

在待命的&#x200B;*error.log*&#x200B;中，您應該會看到類似以下的專案：

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

在上述記錄檔片段中，*10.20.30.40*&#x200B;是主要的IP位址。

在&#x200B;**primary** *tarmk-coldstandby.log*&#x200B;中，您會看到下列專案：

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message 's.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd' from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

在這種情況下，記錄檔中提到的「使用者端」是&#x200B;**待命**&#x200B;執行個體。

一旦這些專案停止顯示在記錄中，您就可以安全地假設同步程式已完成。

雖然上述專案顯示輪詢機制運作正常，但瞭解在輪詢發生時是否有任何資料同步通常會有幫助。 若要這麼做，請尋找類似以下的專案：

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

此外，以非共用的`FileDataStore`執行時，類似下列的訊息會確認二進位檔案已正確傳輸：

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 設定 {#configuration}

下列OSGi設定適用於「冷待命」服務：

* **保留組態：**&#x200B;如果啟用，這會將此組態儲存在存放庫中，而非傳統的OSGi組態檔。 Adobe建議您將此設定保留在生產系統上停用，這樣待命狀態就不會提取主要設定。

* **模式(`mode`)：**&#x200B;這會選擇執行個體的執行模式。

* **連線埠（連線埠）：**&#x200B;用於通訊的連線埠。 預設為 `8023`。

* **主要主機(`primary.host`)：** — 主要執行個體的主機。 此設定僅適用於待命。
* **同步間隔(`interval`)：** — 此設定會決定同步要求之間的間隔，而且僅適用於待命執行個體。

* **允許的IP範圍(`primary.allowed-client-ip-ranges`)：** — 主要允許連線的IP範圍。
* **安全(`secure`)：**&#x200B;啟用SSL加密。 若要使用此設定，必須在所有執行個體上啟用它。
* **待命讀取逾時(`standby.readtimeout`)：**&#x200B;從待命執行個體發出的要求逾時（毫秒）。 使用的預設值為60000 （一分鐘）。

* **待命自動清除(`standby.autoclean`)：**&#x200B;如果存放區的大小在同步處理週期中增加，請呼叫清除方法。

>[!NOTE]
>
>Adobe建議主要和待命資料庫採用不同的存放庫ID，以便可分別識別解除安裝等服務的身分。
>
>若要確保涵蓋此範圍，最好的方式是刪除待命環境上的&#x200B;*sling.id*，然後重新啟動執行個體。

## 容錯移轉程式 {#failover-procedures}

如果主要執行個體因任何原因而失敗，您可以變更啟動執行模式，將其中一個待命執行個體設定為扮演主要執行個體的角色，如下所述：

>[!NOTE]
>
>編輯組態檔，使其符合用於主要執行個體的設定。

1. 移至待命執行個體的安裝位置，然後停止。

1. 如果您有使用設定設定的負載平衡器，此時您可以從負載平衡器的設定中移除主要負載平衡器。
1. 從待命安裝資料夾備份`crx-quickstart`資料夾。 當設定新的待命時，它可以作為起點。

1. 使用`primary`執行模式重新啟動執行個體：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 將新的主要專案新增到負載平衡器。
1. 建立並啟動新的待命執行個體。 如需詳細資訊，請參閱上文[建立AEM TarMK冷待命安裝程式](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)的程式。

## 將Hotfix套用至冷待命設定 {#applying-hotfixes-to-a-cold-standby-setup}

將Hotfix套用至冷待命設定的建議方式，是將它們安裝至主要執行個體，然後將其複製至已安裝了Hotfix的新冷待命執行個體。

您可以依照下列步驟執行此操作：

1. 前往JMX主控台並使用**org.apache.jackrabbit.oak： Status (&quot;Standby&quot;)**bean，停止冷待命執行個體上的同步化程式。 如需如何執行此動作的詳細資訊，請參閱[監視](#monitoring)一節。
1. 停止冷待命執行個體。
1. 在主要執行個體上安裝Hotfix。 如需如何安裝Hotfix的詳細資訊，請參閱[如何使用套件](/help/sites-administering/package-manager.md)。
1. 測試執行個體安裝後是否有問題。
1. 透過刪除其安裝資料夾來移除冷待命執行個體。
1. 停止主要執行個體並複製它，方法是執行其整個安裝資料夾的檔案系統復本，複製到冷待命的位置。
1. 重新設定新建立的翻制，使其作為冷待命執行處理。 請參閱[建立AEM TarMK冷待命安裝程式。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 啟動主要和冷待命執行處理。

## 監控 {#monitoring}

此功能會使用JMX或MBean公開資訊。 如此一來，您就可以使用[JMX主控台](/help/sites-administering/jmx-console.md)來檢查待命和主裝置的目前狀態。 可以在`type org.apache.jackrabbit.oak:type="Standby"`的MBean （名為`Status`）中找到該資訊。

**待命**

觀察待命執行個體時，您會公開一個節點。 ID通常是通用的UUID。

此節點有五個唯讀屬性：

* `Running:`布林值，指出同步處理是否正在執行。

* `Mode:`使用者端：後面接著用來識別執行個體的UUID。 每次更新設定時，此UUID都會變更。

* `Status:`目前狀態的文字表示法（如`running`或`stopped`）。

* `FailedRequests:`連續錯誤數。
* `SecondsSinceLastSuccess:`自上次與伺服器成功通訊以來的秒數。 如果未成功通訊，則會顯示`-1`。

此外還有三種可叫用方法：

* `start():`開始同步處理作業。
* `stop():`停止同步處理作業。
* `cleanup():`在待命系統上執行清除作業。

**主要**

觀察主要主機會透過MBean （其ID值是TarMK待命服務正在使用的連線埠號碼，預設為8023）公開某些一般資訊。 大部分的方法和屬性與待命的相同，但有些則不同：

* `Mode:`一律顯示值`primary`。

此外，最多可以擷取十個連線至主版的使用者端（待命執行處理）的資訊。 MBean ID是執行個體的UUID。 這些MBean沒有可叫用的方法，但有一些有用的唯讀屬性：

* `Name:`使用者端識別碼。
* `LastSeenTimestamp:`文字表示中最後一個請求的時間戳記。
* `LastRequest:`使用者端的最後一個要求。
* `RemoteAddress:`使用者端的IP位址。
* `RemotePort:`使用者端用於上次要求的連線埠。
* `TransferredSegments:`傳輸至此使用者端的區段總數。
* `TransferredSegmentBytes:`傳輸至此使用者端的位元組總數。

## 冷待命存放庫維護 {#cold-standby-repository-maintenance}

### 修訂清除 {#revision-clean}

>[!NOTE]
>
>如果您在主要執行個體上執行[線上修訂清除](/help/sites-deploying/revision-cleanup.md)，則不需要以下顯示的手動程式。 此外，如果您使用線上修訂清除，待命執行個體上的`cleanup ()`作業會自動執行。

>[!NOTE]
>
>請勿在待命時執行離線修訂清除。 此變數並非必要，且不會減少區段存放區大小。

Adobe建議定期執行維護作業，以防止隨著時間推移存放庫過度成長。 若要手動執行冷待命存放庫維護，請遵循下列步驟：

1. 前往JMX主控台並使用&#x200B;**org.apache.jackrabbit.oak： Status (&quot;Standby&quot;)** bean，停止待命執行個體的待命程式。 如需如何執行此動作的詳細資訊，請參閱上文[監視](/help/sites-deploying/tarmk-cold-standby.md#monitoring)一節。

1. 停止主要AEM執行個體。
1. 在主要執行個體上執行Oak壓縮工具。 如需詳細資訊，請參閱[維護存放庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。
1. 啟動主要執行個體。
1. 使用第一個步驟中所述的相同JMX Bean在待命執行處理上啟動待命處理作業。
1. 觀察記錄並等待同步完成。 目前待命存放庫可能會大幅增加。
1. 使用第一個步驟中所述的相同JMX Bean，在待命執行個體上執行`cleanup()`作業。

待命執行個體完成與主要執行個體的同步化可能需要比平常更長的時間，因為離線壓縮會有效重寫存放庫歷史記錄，因此計算存放庫中的變更需要更多時間。 此程式完成後，待命資料庫的大小與主要資料庫的大小大致相同。

作為替代方法，主要存放庫可在主要存放庫上執行壓縮後手動複製到待命，基本上是在每次壓縮執行時重建待命。

### 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

請務必不時對檔案資料存放區執行個體執行記憶體回收，否則，刪除的二進位檔會保留在檔案系統上，最終會填滿磁碟機。 若要執行記憶體回收，請遵循下列程式：

1. 執行冷待命存放庫維護，如上節[所述](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance)。
1. 維護程式完成且執行個體重新啟動後：

   * 在主要上，透過[本文章](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console)中所述的相關JMX Bean執行資料存放區記憶體回收。
   * 待命時，只能透過&#x200B;**BlobGarbageCollection** MBean - `startBlobGC()`使用資料存放區記憶體回收。 **RepositoryManagement** MBean在待命狀態中無法使用。

   >[!NOTE]
   >
   >如果您未使用共用資料存放區，請先在主磁碟區上執行記憶體回收，然後在待命磁碟區上執行。
