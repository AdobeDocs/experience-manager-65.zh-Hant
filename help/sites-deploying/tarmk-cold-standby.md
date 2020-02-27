---
title: 如何使用TarMK Cold Standby運行AEM
seo-title: 如何使用TarMK Cold Standby運行AEM
description: 瞭解如何建立、設定和維護TarMK Cold Standby設定。
seo-description: 瞭解如何建立、設定和維護TarMK Cold Standby設定。
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
translation-type: tm+mt
source-git-commit: c5e6098b62ff7e3e787b5f0f3c3b32a35e3981c6

---


# 如何使用TarMK Cold Standby運行AEM{#how-to-run-aem-with-tarmk-cold-standby}

## 簡介 {#introduction}

Tar Micro Kernel的Cold Standby（冷備用）容量允許一個或多個備用AEM實例連接到主實例。 同步進程只表示它只從主實例到備用實例完成。

備用實例的目的是保證主儲存庫的即時資料拷貝，並確保在主儲存庫因任何原因不可用時快速切換而不丟失資料。

內容在主實例和備用實例之間線性同步，不會對檔案或儲存庫損壞進行任何完整性檢查。 由於這種設計，備用實例是主實例的精確副本，無法幫助緩解主實例的不一致性。

>[!NOTE]
>
>「冷備用」功能旨在保護作者實例上需要高可用性的情 **形** 。 若使用Tar Micro Kernel發佈執行個體需 **要高可用性** ,Adobe建議使用發佈群組。
>
>如需更多可用部署的資訊，請參閱「建議 [的部署](/help/sites-deploying/recommended-deploys.md) 」頁面。

## 運作方式 {#how-it-works}

在主要AEM例項上，會開啟TCP連接埠，並監聽傳入的訊息。 目前，從系統將向主系統發送兩種消息：

* 請求當前頭段ID的消息
* 要求具有指定ID之區段資料的訊息

備用設備定期請求主設備當前頭的段ID。 如果區段在本機未知，則會擷取該區段。 如果區段已顯示，則會比較區段，並視需要要求參考區段。

>[!NOTE]
>
>待機實例不接收任何類型的請求，因為它們僅以同步模式運行。 備用實例上唯一可用的部分是Web控制台，以便便於進行捆綁和服務配置。

典型的TarMK冷備用部署：

![chlimage_1](assets/chlimage_1.png)

## 其他特性 {#other-characteristics}

### 魯棒性 {#robustness}

資料流設計用於自動檢測和處理連接和網路相關問題。 所有資料包都與校驗和捆綁在一起，一旦連接或損壞的資料包發生重試機制時，就會觸發。

#### 效能 {#performance}

在主實例上啟用TarMK Cold Standby對效能幾乎沒有可衡量的影響。 額外的CPU消耗非常低，額外的硬碟和網路IO不應產生和效能問題。

在待機狀態下，同步過程中的CPU消耗會很高。 由於該過程不是多線程的，因此不能通過使用多個內核來加速。 如果沒有變更或傳輸任何資料，則不會有可衡量的活動。 連接速度會因硬體和網路環境而異，但不取決於儲存庫的大小或SSL使用。 在估計初始同步所需的時間或在主節點上同時更改了大量資料時，應牢記這一點。

#### 安全性 {#security}

假設所有實例都運行在同一內部網安全區域，則安全漏洞的風險大大降低。 不過，您可以在從系統和主系統之間啟用SSL連接，從而添加額外的安全層。 這樣做會降低資料被中間人所破壞的可能性。

此外，您還可以通過限制傳入請求的IP地址來指定允許連接的備用實例。 這應有助於確保內部網中的任何人都不能複製儲存庫。

>[!NOTE]
>
>建議在作為Coldy備用設定一部分的Dispatcher和伺服器之間添加負載平衡器。 應將負載平衡器配置為僅將用戶流量引導到主實 **例** ，以確保一致性，並防止內容通過Cold Standby機制以外的其他方式被複製到備用實例。

## 建立AEM tarMK Cold Standby設定 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>與舊版相比，AEM 6.3中「區段」節點儲存區和「備用儲存區」服務的PID已變更，如下所示：
>
>* 來自org.apache.jackrabbit.oak。**plugins**.segment.standby.standby.StandbyStoreService to org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* 來自org.apache.jackrabbit.oak。**plugins**.segment.SegmentNodeStoreService to org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>
請務必進行必要的組態調整，以反映此變更。

要建立TarMK冷備用安裝，首先需要通過將主安裝資料夾的整個檔案系統副本複製到新位置來建立備用實例。 然後，您可以使用將指定其角色（或）的執行模式來啟 `primary` 動每個 `standby`例項。

以下是建立具有一個主實例和一個備用實例的設定時需要遵循的過程：

1. 安裝AEM。

1. 關閉實例，並將其安裝資料夾複製到冷備用實例的運行位置。 即使從不同的電腦執行，請務必為每個檔案夾提供描述性名稱(例如 *aem-primary**或aem-standby*)，以區分執行個體。
1. 轉到主實例的安裝資料夾，並：

   1. 檢查並刪除您可能在 `aem-primary/crx-quickstart/install`

   1. 建立檔案夾，名為 `install.primary``aem-primary/crx-quickstart/install`

   1. 在 `aem-primary/crx-quickstart/install/install.primary`
   1. 在相同位置創 `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` 建名為的檔案，並相應地進行配置。 有關配置選項的詳細資訊，請參 [閱Configuration](/help/sites-deploying/tarmk-cold-standby.md#configuration)。

   1. 如果您正將AEM tarMK例項與外部資料存放區搭配使用，請建立名為 `crx3` 的檔 `aem-primary/crx-quickstart/install` 案夾 `crx3`

   1. 將資料儲存配置檔案放在資料夾 `crx3` 中。
   例如，如果您使用外部檔案資料存放區執行AEM TarMK例項，則需要下列設定檔案：

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`
   以下是主要實例的示例配置：

   **org** .apache. **jackrabbit.oak.segment.SegmentNodeStoreService.config的範例**

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

1. 啟動主模式，確保指定主運行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 建立 **org.apache.jackrabbit.oak.segment套件的新Apache Sling Logging Logger** 。 將記錄檔層級設為「除錯」，並將其記錄檔輸出指向個別的記錄檔，例如 */logs/tarmk-coldstandby.log*。 如需詳細資訊，請參 [閱記錄](/help/sites-deploying/configure-logging.md)。
1. 轉到備用實例的 **位置** ，並通過運行jar啟動它。
1. 建立與主日誌配置相同的日誌配置。 然後，停止例項。
1. 接下來，準備備用實例。 您可以通過執行與主實例相同的步驟來執行此操作：

   1. 刪除您可能擁有的任何檔案 `aem-standby/crx-quickstart/install`。
   1. 建立新資料夾，名稱 `install.standby` 為 `aem-standby/crx-quickstart/install`

   1. 建立兩個名為：

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. 建立新資料夾，名稱 `crx3` 為 `aem-standby/crx-quickstart/install`

   1. 建立資料儲存區組態，並將它放在下方 `aem-standby/crx-quickstart/install/crx3`。 在此範例中，您需要建立的檔案為：

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. 編輯檔案並建立必要的設定。
   以下是典型備用實例的示例配置檔案：

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

1. 使用備用 **運行模式** ，啟動備用實例：

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

此服務也可通過Web控制台進行配置，方法是：

1. 前往Web主控台： *https://serveraddress:serverport/system/console/configMgr*
1. 正在尋找名為 **Apache Jackrabbit Oak Segment Tar Cold Standby Service的服務** ，然後按兩下它以編輯設定。
1. 儲存設定，然後重新啟動執行個體，讓新設定生效。

>[!NOTE]
>
>您可以隨時檢查例項的角色，方法是檢查Sling Settings Web Console中主 **要****或備用執行模** 式的存在。

>若要這麼做，請前往 *https://localhost:4502/system/console/status-slingsettings* ，並勾 **選「執行模式」** 行。
>

## 首次同步 {#first-time-synchronization}

準備完成並首次啟動備用後，當備用接近主備份時，實例之間將會出現大量網路通信。 您可以查閱日誌來觀察同步的狀態。

在待機 *tarmk-coldstandby.log中*，您將看到以下條目：

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

在備用的 *error.log中*，您應看到如下條目：

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

在上述記錄程式碼 *片段中，10.20.30.40* 是主要的IP位址。

在主 **tarmk** - ** coldstandby.log中，您會看到以下條目：

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

在這種情況下，日誌中提及的「客戶端」是備用 **實例** 。

一旦這些項目停止出現在記錄中，您就可以放心地假設同步程式已完成。

雖然上述項目顯示輪詢機制正常運作，但瞭解是否有任何資料在發生輪詢時同步通常很有用。 若要這麼做，請尋找下列項目：

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

此外，當使用非共用功能執行時， `FileDataStore`像下列這類訊息會確認二進位檔案已正確傳輸：

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 設定 {#configuration}

以下OSGi設定可用於Cold Standby服務：

* **** 持續配置：如果啟用，則會將配置儲存在儲存庫中，而不是傳統的OSGi配置檔案中。 建議在生產系統上禁用此設定，以使備用系統不會提取主配置。

* **`mode`模式(**):這將選擇實例的運行模式。

* **** 埠（埠）:用於通信的埠。 預設值為 `8023`。

* **`primary.host`主主機(**):-主實例的主機。 此設定僅適用於備用設備。
* **`interval`同步間隔(**):-此設定確定同步請求之間的間隔，並且僅適用於備用實例。

* **`primary.allowed-client-ip-ranges`允許的IP範圍(**):-主伺服器允許連接的IP範圍。
* **`secure`安全(**):啟用SSL加密。 為了使用此設定，必須在所有例項上啟用此設定。
* **`standby.readtimeout`備用讀超時(**):從備用實例發出的請求超時（以毫秒為單位）。 建議的逾時設定為43200000。 通常建議您將逾時值設為至少12小時。

* **`standby.autoclean`備用自動清除(**):如果同步週期中儲存的大小增加，請調用清除方法。

>[!NOTE]
強烈建議主資料庫ID和備用資料庫ID不同，以便對於「卸載」之類的服務可以單獨區分。
確保涵蓋此內容的最佳方式是在待機裝置上刪除 *sling.id* 檔案，然後重新啟動執行個體。

## 故障切換過程 {#failover-procedures}

如果主實例因任何原因而失敗，您可以通過更改以下詳細說明的啟動運行模式，將其中一個備用實例設定為承擔主實例的角色：

>[!NOTE]
還需要修改配置檔案，以便它們與用於主實例的設定匹配。

1. 轉到安裝備用實例的位置，然後停止它。

1. 如果已使用設定配置了負載平衡器，則此時可以從負載平衡器配置中刪除主。
1. 從備用安 `crx-quickstart` 裝資料夾中備份資料夾。 在設定新備用時，可將其用作起點。

1. 使用runmode重新啟動 `primary` 實例：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 向負載平衡器添加新主要。
1. 建立並啟動新的備用實例。 如需詳細資訊，請參閱上述「建立AEM TarMK [冷備用設定」的程式](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)。

## 將修補程式套用至冷待機設定 {#applying-hotfixes-to-a-cold-standby-setup}

建議將修補程式套用至Cold Standby設定的方式是將它們安裝至主要執行個體，然後將它複製至已安裝修補程式的新Cold Standby執行個體。

您可依照下列步驟進行：

1. 前往JMX主控台並使用**org.apache.jackrabbit.oak來停止冷備用例項上的同步程式：狀態（「備用」）**bean。 有關如何執行此操作的詳細資訊，請參閱「監控」一 [節](#monitoring)。
1. 停止冷備用實例。
1. 在主實例上安裝Hotfix。 如需如何安裝修補程式的詳細資訊，請參 [閱How to Work With Packages](/help/sites-administering/package-manager.md)。
1. 在安裝後測試實例以瞭解問題。
1. 通過刪除其安裝資料夾來刪除冷備用實例。
1. 通過將主實例的整個安裝資料夾的檔案系統副本複製到冷備用實例的位置來停止它並克隆它。
1. 重新配置新建立的克隆以充當冷備用實例。 如需詳細資訊，請 [參閱「建立AEM TarMK Cold Standby Setup」。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 啟動主實例和冷備用實例。

## 監控 {#monitoring}

此功能會使用JMX或MBeans公開資訊。 這樣，您就可以使用 [JMX控制台檢查待機和主設備的當前狀態](/help/sites-administering/jmx-console.md)。 這些資訊可在名為的MBean中 `type org.apache.jackrabbit.oak:type="Standby"`找到 `Status`。

**備用**

觀察待機實例時，您將公開一個節點。 ID通常是通用UUID。

此節點有五個只讀屬性：

* `Running:` 指示同步進程是否正在運行的布爾值。

* `Mode:` 客戶：後跟用於標識實例的UUID。 請注意，每次更新配置時，此UUID都會變更。

* `Status:` 目前狀態的文字表示( `running` 如 `stopped`或)。

* `FailedRequests:`連續錯誤的數量。
* `SecondsSinceLastSuccess:` 自上次成功與伺服器通信以來的秒數。 如果未 `-1` 成功通信，則顯示。

還有三種可調用的方法：

* `start():` 啟動同步進程。
* `stop():` 停止同步進程。
* `cleanup():` 對待機運行清除操作。

**主要**

觀察主伺服器通過MBean公開一些一般資訊， MBean的ID值是TarMK備用服務使用的埠號（預設為8023）。 大多數方法和屬性與待機方法和屬性相同，但有些不同：

* `Mode:` 將始終顯示值 `primary`。

此外，還可以檢索與主設備連接的多達10個客戶機（備用實例）的資訊。 MBean ID是實例的UUID。 這些MBean沒有可調用的方法，但有一些非常有用的只讀屬性：

* `Name:` 用戶端的ID。
* `LastSeenTimestamp:` 文本表示中最後一個請求的時間戳。
* `LastRequest:` 客戶的最後要求。
* `RemoteAddress:` 客戶機的IP地址。
* `RemotePort:` 用於上次請求的客戶端的埠。
* `TransferredSegments:` 傳送至此用戶端的區段總數。
* `TransferredSegmentBytes:`傳送到此客戶機的位元組數。

## 冷備用儲存庫維護 {#cold-standby-repository-maintenance}

### 修訂清除 {#revision-clean}

>[!NOTE]
如果在主實 [例上運行「聯機修訂清除](/help/sites-deploying/revision-cleanup.md) 」，則不需要下面顯示的手動過程。 此外，如果您使用「線上修訂清除」，則 `cleanup ()` 將自動執行備用實例的操作。

>[!NOTE]
請勿在備用系統上運行離線修訂清除。 不需要它，也不會降低區段儲存區大小。

Adobe建議定期執行維護作業，以防止儲存庫隨著時間過長而增長。 要手動執行冷備用儲存庫維護，請執行以下步驟：

1. 前往JMX主控台並使用 **org.apache.jackrabbit.oak來停止備用例項上的備用程式：狀態（「備用」）** Bean。 有關如何執行此操作的詳細資訊，請參閱上節的監 [控](/help/sites-deploying/tarmk-cold-standby.md#monitoring)。

1. 停止主要AEM例項。
1. 在主實例上運行oak壓縮工具。 有關詳細資訊，請參 [閱維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。
1. 啟動主實例。
1. 使用與第一步中所述的相同JMX Bean，在備用實例上啟動備用進程。
1. 觀看日誌並等待同步完成。 此時，備用儲存庫可能出現大幅增長。
1. 對備用 `cleanup()` 實例運行操作，使用與第一步中所述的相同JMX Bean。

備用實例與主實例完成同步可能需要比平時更長的時間，因為離線壓縮可以有效重寫儲存庫歷史記錄，因此計算儲存庫中的更改需要更多的時間。 還應指出，一旦此過程完成，備用儲存庫的大小將與主儲存庫的大小大致相同。

作為替代方法，在主系統上運行壓縮後，主系統資訊庫可以手動複製到備用系統上，實際上每次壓縮運行時都重建備用系統。

### 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

在檔案資料儲存實例上不時運行廢棄項目收集非常重要，否則，已刪除的二進位檔案將保留在檔案系統中，最終填滿驅動器。 要運行廢棄項目收集，請遵循以下過程：

1. 如上節所述，運行冷備用儲存庫 [維護](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance)。
1. 在維護過程完成並重新啟動實例後：

   * 在主系統上，如本文所述，透過相關的JMX Bean執行資料存放區廢棄項目 [收集](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console)。
   * 在待機狀態下，資料存放區廢棄項目收集僅能透過 **BlobGarbageCollection** MBean使用 `startBlobGC()`。 **RepositoryManagement **MBean不可用於備用。
   >[!NOTE]
   如果您未使用共用資料存放區，則必須先在主要儲存區上執行廢棄項目收集，然後再在備用儲存區上執行。

