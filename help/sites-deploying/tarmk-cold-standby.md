---
title: 如何使用TarMK冷待機執行AEM
seo-title: How to Run AEM with TarMK Cold Standby
description: 了解如何建立、設定和維護TarMK冷備用設定。
seo-description: Learn how to create, configure and maintain a TarMK Cold Standby setup.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: 88e4d8b56aa844e9a264615250971d0afdb68137
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 0%

---

# 如何使用TarMK冷待機執行AEM{#how-to-run-aem-with-tarmk-cold-standby}

## 簡介 {#introduction}

Tar Micro Kernel的「冷備用」容量允許一個或多個備用AEM實例連接到主實例。 同步過程只表示它只從主實例到備用實例執行。

備用實例的目的是保證主儲存庫的即時資料副本，並確保快速切換，而不會因任何原因導致主資料庫不可用而丟失資料。

主要執行個體和備用執行個體之間會線性同步內容，不會進行任何完整性檢查，以檢查檔案或存放庫是否損毀。 由於這種設計，備用實例是主實例的精確副本，無助於緩解主實例上的不一致。

>[!NOTE]
>
>「冷待機」功能旨在保護需要高可用性的情況 **作者** 例項。 對於需要高可用性的情況 **發佈** 執行個體使用Tar Micro Kernel,Adobe建議使用發佈伺服器陣列。
>
>如需更多可用部署的資訊，請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md) 頁面。

>[!NOTE]
>
>設定備用實例或從主節點派生的實例時，它僅允許訪問以下控制台（用於管理相關活動）:
>
>* OSGI Web主控台
>
>無法存取其他主控台。

## 運作方式 {#how-it-works}

在主AEM實例上，開啟一個TCP埠並監聽傳入的消息。 目前，從伺服器將向主伺服器發送兩種類型的消息：

* 請求當前頭段ID的消息
* 使用指定ID要求區段資料的訊息

備用設備定期請求主設備的當前頭的段ID。 如果區段在本機未知，則會擷取該區段。 如果已存在，則會比較區段，並視需要請求參考的區段。

>[!NOTE]
>
>待機實例不接收任何類型的請求，因為它們只在同步模式下運行。 備用執行個體上唯一可用的區段是Web主控台，以方便套件和服務設定。

典型的TarMK冷備部署：

![chlimage_1](assets/chlimage_1.png)

## 其他特性 {#other-characteristics}

### 魯棒性 {#robustness}

資料流設計用於自動檢測和處理連接和網路相關問題。 所有資料包都與校驗和捆綁在一起，並且一旦連接或損壞的資料包出現問題，就會觸發重試機制。

#### 效能 {#performance}

在主實例上啟用TarMK冷備對效能幾乎沒有可衡量的影響。 額外的CPU消耗非常低，額外的硬碟和網路IO不應產生和效能問題。

在待機狀態上，在同步過程中，您會發現CPU消耗很高。 由於該過程不是多線程的，因此不能使用多個內核來加快速度。 如果沒有資料更改或傳輸，則沒有可衡量的活動。 連接速度會因硬體和網路環境而異，但不取決於儲存庫的大小或SSL的使用。 在預估初始同步所需時間或在主節點同時變更大量資料時，您應謹記這一點。

#### 安全性 {#security}

假設所有實例在同一內部網路安全區域中運行，則安全違規的風險大大降低。 不過，您仍可啟用從伺服器與主伺服器之間的SSL連線，以新增額外的安全層。 這樣會降低資料被中間人破壞的可能性。

此外，您還可以通過限制傳入請求的IP地址來指定允許連接的備用實例。 這應有助於確保內部網路中的任何人都無法複製儲存庫。

>[!NOTE]
>
>建議在作為Coldy待機設定一部分的Dispatcher與伺服器之間新增負載平衡器。 負載平衡器應設定為僅將使用者流量導向至 **主要** 執行個體，以確保一致性，並防止內容透過「冷備」機制以外的其他方式複製到備用執行個體上。

## 建立AEM TarMK冷待機設定 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>AEM 6.3中「區段」節點存放區和「待機存放區」服務的PID與舊版相比已變更，如下所示：
>
>* 來自org.apache.jackrabbit.oak。**外掛程式**.segment.standby.store.StandbyStoreService轉至org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* 來自org.apache.jackrabbit.oak。**外掛程式**.segment.SegmentNodeStoreService至org.apache.jackrabbit.oak.segment.SegmentNodeStoreService

>
>請務必進行必要的設定調整，以反映此變更。

要建立TarMK冷備用安裝，首先需要通過將主安裝資料夾的整個安裝資料夾執行檔案系統拷貝到新位置來建立備用實例。 然後，您可以以將指定其角色( `primary` 或 `standby`)。

以下是需要遵循的過程，以便使用一個主實例和一個備用實例建立安裝程式：

1. 安裝AEM。

1. 關閉實例，並將其安裝資料夾複製到冷備用實例運行的位置。 即使從不同的電腦執行，請務必為每個資料夾提供描述性名稱(例如 *aem-primary* 或 *aem-standby*)來區分執行個體。
1. 轉至主實例的安裝資料夾，並：

   1. 檢查並刪除您可能在下的任何先前OSGi設定 `aem-primary/crx-quickstart/install`

   1. 建立名為 `install.primary` 在 `aem-primary/crx-quickstart/install`

   1. 為下的首選節點儲存區和資料儲存區建立所需的配置 `aem-primary/crx-quickstart/install/install.primary`
   1. 建立檔案，稱為 `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` 在相同位置，並據此進行設定。 如需設定選項的詳細資訊，請參閱 [設定](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. 如果您將AEM TarMK例項與外部資料存放區搭配使用，請建立名為 `crx3` 在 `aem-primary/crx-quickstart/install` 已命名 `crx3`

   1. 將資料儲存配置檔案放入 `crx3` 檔案夾。

   例如，如果您使用外部檔案資料存放區執行AEM TarMK例項，則需要下列組態檔：

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   以下是主要執行個體的設定範例：

   **範例** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

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

1. 為建立新的Apache Sling Logging Logger **org.apache.jackrabbit.oak.segment** 包。 將記錄層級設為「Debug」，並將其記錄輸出指向個別的記錄檔，例如 */logs/tarmk-coldstandby.log*. 如需詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md).
1. 前往 **待機** 執行個體，然後執行jar以啟動。
1. 建立與主要伺服器相同的記錄設定。 然後，停止執行個體。
1. 接下來，準備備用實例。 您可以執行與主要執行個體相同的步驟來執行此作業：

   1. 刪除您可能在下面的任何檔案 `aem-standby/crx-quickstart/install`.
   1. 建立名為 `install.standby` 在 `aem-standby/crx-quickstart/install`

   1. 建立兩個名為的配置檔案：

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. 建立名為 `crx3` 在 `aem-standby/crx-quickstart/install`

   1. 建立資料儲存配置並將其置於 `aem-standby/crx-quickstart/install/crx3`. 在此範例中，您需要建立的檔案為：

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. 編輯檔案並建立必要的設定。

   典型備用實例的配置檔案示例如下：

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

1. 啟動 **待機** 執行個體（使用備用執行模式）:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

服務也可透過Web主控台進行設定，方法如下：

1. 前往Web主控台： *https://serveraddress:serverport/system/console/configMgr*
1. 尋找名為 **Apache Jackrabbit Oak Segment Tar Cold Standby Service** 並按兩下以編輯設定。
1. 儲存設定並重新啟動執行個體，讓新設定生效。

>[!NOTE]
>
>您可以隨時檢查執行個體是否具備 **主要** 或 **待機** 在Sling Settings Web Console中執行模式。
>
>您可以前往 *https://localhost:4502/system/console/status-slingsettings* 並檢查 **&quot;運行模式&quot;** 行。

## 首次同步 {#first-time-synchronization}

準備完成且首次啟動備用後，當備用接近主伺服器時，執行個體之間會有大量網路流量。 您可以查閱記錄，以觀察同步的狀態。

待機 *tarmk-coldstandby.log*，您會看到下列項目：

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

在待命 *error.log*，您應會看到下列項目：

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

在上述記錄片段中， *10.20.30.40* 是主要的IP位址。

在 **主要** *tarmk-coldstandby.log*，您會看到下列項目：

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

在此情況下，記錄中提及的「用戶端」為 **待機** 例項。

一旦這些項目停止出現在記錄中，您就可以安全地假設同步程式已完成。

雖然上述項目顯示輪詢機制正常運作，但了解是否有任何資料在輪詢發生時同步通常很有用。 若要這麼做，請尋找下列項目：

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

此外，當以非共用執行時 `FileDataStore`，則下列訊息將確認已正確傳輸二進位檔案：

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 設定 {#configuration}

以下OSGi設定可用於冷待機服務：

* **保留配置：** 如果啟用，則會將設定儲存在存放庫中，而非傳統的OSGi組態檔。 建議在生產系統上將此設定保持禁用狀態，以便備用系統不會提取主配置。

* **模式(`mode`):** 這會選擇執行個體的執行模式。

* **埠（埠）:** 用於通信的埠。 預設為 `8023`.

* **主主機(`primary.host`):**  — 主實例的主機。 此設定僅適用於待機。
* **同步間隔(`interval`):**  — 此設定確定同步請求之間的間隔，並且僅適用於備用實例。

* **允許的IP範圍(`primary.allowed-client-ip-ranges`):**  — 主要允許連接的IP範圍。
* **安全(`secure`):** 啟用SSL加密。 若要使用此設定，必須在所有執行個體上啟用此設定。
* **待機讀取超時(`standby.readtimeout`):** 從備用實例發出的請求的超時（毫秒）。 使用的預設值為60000（1分鐘）。

* **備用自動清除(`standby.autoclean`):** 如果儲存區大小在同步週期中增加，請呼叫清除方法。

>[!NOTE]
>
>強烈建議主要和備用資料庫具有不同的儲存庫ID，以便對於卸載等服務單獨不可識別它們。
>
>若要確定已涵蓋此範圍，最好刪除 *sling.id* 檔案，然後重新啟動執行個體。

## 故障轉移過程 {#failover-procedures}

如果主實例因任何原因而失敗，您可以通過更改啟動運行模式來設定其中一個備用實例以承擔主實例的角色，如下所述：

>[!NOTE]
>
>還需要修改配置檔案，使它們與用於主實例的設定匹配。

1. 轉到安裝備用實例的位置，然後停止它。

1. 如果已使用安裝程式配置了負載平衡器，則可以在此時從負載平衡器的配置中刪除主配置。
1. 備份 `crx-quickstart` 從備用安裝資料夾取得的資料夾。 設定新待機時，可將其用作起始點。

1. 使用重新啟動執行個體 `primary` 執行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 向負載平衡器添加新主。
1. 建立並啟動新的備用實例。 如需詳細資訊，請參閱上述程式，位於 [建立AEM TarMK冷待機設定](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## 將Hotfix套用至冷待機設定 {#applying-hotfixes-to-a-cold-standby-setup}

建議將hotfix套用至冷態設定，方法是將它們安裝至主要執行個體，然後將其複製至新的冷態備用執行個體，並安裝hotfix。

您可以依照下列步驟來執行此操作：

1. 前往JMX主控台並使用**org.apache.jackrabbit.oak停止冷備執行個體上的同步程式：狀態（「待機」）**Bean。 如需如何執行此動作的詳細資訊，請參閱 [監控](#monitoring).
1. 停止冷備用實例。
1. 在主要執行個體上安裝Hotfix。 如需如何安裝Hotfix的詳細資訊，請參閱 [如何使用套件](/help/sites-administering/package-manager.md).
1. 在安裝後測試執行個體是否有問題。
1. 通過刪除其安裝資料夾來刪除冷備用實例。
1. 通過將主實例的整個安裝資料夾的檔案系統副本複製到冷備用資料夾的位置，停止該主實例並克隆它。
1. 重新配置新建立的克隆以充當冷備用實例。 如需其他詳細資訊，請參閱 [建立AEM TarMK冷待機設定。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 啟動主備實例和冷備實例。

## 監控 {#monitoring}

此功能使用JMX或MBean公開資訊。 這樣，您可以使用 [JMX控制台](/help/sites-administering/jmx-console.md). 可在以下MBean中找到資訊： `type org.apache.jackrabbit.oak:type="Standby"`已命名 `Status`.

**待機**

觀察待機執行個體時，您會公開一個節點。 ID通常是通用UUID。

此節點有五個唯讀屬性：

* `Running:` 指示同步進程是否正在運行的布爾值。

* `Mode:` 客戶端：後接用於識別例項的UUID。 請注意，每次更新設定時，此UUID都會變更。

* `Status:` 當前狀態的文本表示(如 `running` 或 `stopped`)。

* `FailedRequests:`連續錯誤的數量。
* `SecondsSinceLastSuccess:` 自上次成功與伺服器通訊以來的秒數。 會顯示 `-1` 如果尚未成功通信。

還有三種可調用的方法：

* `start():` 啟動同步過程。
* `stop():` 停止同步過程。
* `cleanup():` 在待機上運行清理操作。

**主要**

觀察主要資訊會透過MBean公開一些一般資訊，其ID值是TarMK備用服務使用的埠號（預設為8023）。 大多數方法和屬性與待機方法和屬性相同，但有些不同：

* `Mode:` 一律會顯示值 `primary`.

此外，可檢索與主機連接的最多10個客戶機（備用實例）的資訊。 MBean ID是執行個體的UUID。 這些MBean沒有可調用的方法，但有一些非常有用的只讀屬性：

* `Name:` 用戶端的ID。
* `LastSeenTimestamp:` 以文字表示的上次請求的時間戳記。
* `LastRequest:` 客戶的最後一個請求。
* `RemoteAddress:` 客戶端的IP地址。
* `RemotePort:` 客戶端用於最後一個請求的埠。
* `TransferredSegments:` 轉移給此客戶的區段總數。
* `TransferredSegmentBytes:`傳輸到此客戶端的位元組總數。

## 冷備用儲存庫維護 {#cold-standby-repository-maintenance}

### 修訂清除 {#revision-clean}

>[!NOTE]
>
>如果您執行 [線上修訂清除](/help/sites-deploying/revision-cleanup.md) 在主要執行個體上，不需要下列手動程式。 此外，如果您使用「線上修訂清除」，則 `cleanup ()` 待機實例的操作將自動執行。

>[!NOTE]
>
>請勿在待機狀態上執行離線修訂清除。 不需要，也不會縮小區段存放區大小。

Adobe建議定期運行維護，以防止儲存庫隨著時間的推移而過度增長。 要手動執行冷備用儲存庫維護，請執行以下步驟：

1. 轉到JMX控制台並使用 **org.apache.jackrabbit.oak:狀態（「待機」）** 豆。 如需如何執行此動作的詳細資訊，請參閱上節： [監控](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. 停止主要AEM例項。
1. 在主要執行個體上執行oak壓縮工具。 如需詳細資訊，請參閱 [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. 啟動主實例。
1. 使用第一步中所述的相同JMX Bean，在備用實例上啟動備用進程。
1. 觀看日誌並等待同步完成。 此時，備用儲存庫可能會大幅增長。
1. 執行 `cleanup()` 在備用實例上操作，使用第一步中所述的相同JMXbean。

備用實例完成與主實例的同步可能需要比平常更長的時間，因為離線壓縮可以有效重寫儲存庫歷史記錄，因此計算儲存庫中的更改需要更長時間。 還應指出，此程式完成後，待機儲存庫的大小將與主儲存庫的大小大致相同。

或者，在主資料庫上運行壓縮後，主資料庫可以手動複製到備用資料庫，基本上每次壓縮運行時都重建備用資料庫。

### 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

不時對檔案資料存放區實例運行垃圾收集非常重要，否則，已刪除的二進位檔案將保留在檔案系統上，最終填滿驅動器。 要運行垃圾收集，請執行以下過程：

1. 如一節所述，運行冷備用儲存庫維護 [abos](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. 維護過程完成並重新啟動實例後：

   * 在主伺服器上，通過相關的JMX Bean運行資料儲存垃圾收集，如 [這篇文章](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * 待機時，資料儲存垃圾收集僅可透過 **BlobGarbageCollection** MBean - `startBlobGC()`. **RepositoryManagement **MBean在待機狀態上不可用。

   >[!NOTE]
   >
   >如果您未使用共用資料儲存，則首先必須在主系統上運行垃圾收集，然後在待機系統上運行。
