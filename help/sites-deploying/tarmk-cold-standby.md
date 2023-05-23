---
title: TarMK冷備AEM用如何運行
seo-title: How to Run AEM with TarMK Cold Standby
description: 瞭解如何建立、配置和維護TarMK冷備用設定。
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
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 0%

---

# TarMK冷備AEM用如何運行{#how-to-run-aem-with-tarmk-cold-standby}

## 簡介 {#introduction}

Tar Micro Kernel的冷備用容量允許一個或多個備用實例AEM連接到主實例。 同步進程只是一種方式，它只表示它只從主實例到備用實例完成。

備用實例的目的是保證主資料庫的即時資料副本，並確保快速切換而不會因任何原因導致主資料庫不可用。

內容在主實例和備用實例之間線性同步，無需對檔案或儲存庫損壞進行任何完整性檢查。 由於這種設計，備用實例是主實例的精確副本，無法幫助緩解主實例上的不一致。

>[!NOTE]
>
>「冷備用」功能旨在保護在以下情況下需要高可用性的情形 **作者** 實例。 對於需要高可用性的情況， **發佈** 實例使用Tar Micro Kernel,Adobe建議使用發佈場。
>
>有關更多可用部署的資訊，請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md) 的子菜單。

>[!NOTE]
>
>在設定備用實例或從主節點派生備用實例時，它僅允許訪問以下控制台（用於與管理相關的活動）:
>
>* OSGI Web控制台
>
>其他控制台無法訪問。

## 它的工作原理 {#how-it-works}

在主實AEM例上，TCP埠已開啟並正在偵聽傳入消息。 當前，從屬機將向主機發送兩種類型的消息：

* 請求當前頭的段ID的消息
* 請求具有指定ID的段資料的消息

待機定期請求主機當前頭的段ID。 如果該段在本地未知，則將檢索該段。 如果已經存在，則會比較這些段，並在必要時也會請求引用的段。

>[!NOTE]
>
>備用實例沒有接收任何類型的請求，因為它們只在同步模式下運行。 備用實例上唯一可用的部分是Web控制台，以便於捆綁和服務配置。

典型的TarMK冷備用部署：

![chlimage_1](assets/chlimage_1.png)

## 其他特徵 {#other-characteristics}

### 魯棒性 {#robustness}

資料流設計用於自動檢測和處理連接和網路相關問題。 所有資料包都與校驗和捆綁在一起，一旦連接問題或損壞的資料包發生重試機制就會觸發。

#### 效能 {#performance}

在主實例上啟用TarMK冷備用對效能幾乎沒有可衡量的影響。 額外的CPU消耗非常低，額外的硬碟和網路IO不應產生和效能問題。

在待機狀態下，在同步過程中，CPU消耗會很高。 由於過程不是多線程的，因此無法使用多個內核來加速。 如果沒有更改或傳輸任何資料，則將沒有可衡量的活動。 連接速度會因硬體和網路環境而異，但不取決於儲存庫的大小或SSL使用情況。 在估計初始同步所需的時間或在主節點上同時更改了大量資料時，應牢記這一點。

#### 安全性 {#security}

假設所有實例都運行在同一內部網安全區域中，則安全違規風險大大降低。 但是，您可以通過啟用從伺服器與主伺服器之間的SSL連接來添加額外的安全層。 這樣做會降低資料被中間人破壞的可能性。

此外，您還可以通過限制傳入請求的IP地址來指定允許連接的備用實例。 這應有助於確保Intranet中的任何人都無法複製儲存庫。

>[!NOTE]
>
>建議在作為Coldy Standby設定一部分的Dispatcher和伺服器之間添加負載平衡器。 應將負載平衡器配置為僅將用戶通信定向到 **主** 實例，以確保一致性，並防止內容通過Cold Standby機制以外的其他方式複製到備用實例上。

## 建立AEMTarMK冷備用設定 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>與以前版本相比，段節點儲存和備用儲存服務的PID在AEM6.3中發生了更改，如下所示：
>
>* org.apache.jackrabbit.oak。**插件**.segment.standby.store.StandbyStoreService到org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* org.apache.jackrabbit.oak。**插件**.segment.SegmentNodeStoreService到org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>確保進行必要的配置調整以反映此更改。

為了建立TarMK冷備用安裝，您首先需要通過執行主安裝資料夾的整個檔案系統副本到新位置來建立備用實例。 然後，您可以使用將指定其角色的運行模式啟動每個實例( `primary` 或 `standby`)。

下面是建立具有一個主實例和一個備用實例的安裝程式所需要遵循的步驟：

1. 安裝AEM。

1. 關閉實例，並將其安裝資料夾複製到冷備用實例將從其運行的位置。 即使從不同的電腦運行，也要確保為每個資料夾提供描述性名稱(如 *主* 或 *aem待機*)以區分實例。
1. 轉到主實例的安裝資料夾，並：

   1. 檢查並刪除您可能在以下位置擁有的任何先前OSGi配置 `aem-primary/crx-quickstart/install`

   1. 建立名為 `install.primary` 在 `aem-primary/crx-quickstart/install`

   1. 為以下位置的首選節點儲存和資料儲存建立所需的配置 `aem-primary/crx-quickstart/install/install.primary`
   1. 建立名為 `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` 並相應配置。 有關配置選項的詳細資訊，請參見 [配置](/help/sites-deploying/tarmk-cold-standby.md#configuration)。

   1. 如果將TarMK實例與AEM外部資料儲存區一起使用，請建立名為 `crx3` 在 `aem-primary/crx-quickstart/install` 命名 `crx3`

   1. 將資料儲存配置檔案放在 `crx3` 的子菜單。

   例如，如果您正在運行具有外部文AEM件資料儲存的TarMK實例，則需要以下配置檔案：

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   在下面，您將找到主實例的示例配置：

   **示例** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 啟動主模式，確保指定主運行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 為建立新的Apache Sling日誌記錄器 **org.apache.jackrabbit.oak.segment** 檔案。 將日誌級別設定為「調試」，並將其日誌輸出指向單獨的日誌檔案，如 */logs/tarmk-coldstandby.log*。 有關詳細資訊，請參見 [記錄](/help/sites-deploying/configure-logging.md)。
1. 轉到 **備用** 實例，然後運行jar啟動它。
1. 建立與主日誌配置相同的日誌配置。 然後，停止實例。
1. 接下來，準備備用實例。 通過執行與主實例相同的步驟，可以執行此操作：

   1. 刪除您可能在下面的所有檔案 `aem-standby/crx-quickstart/install`。
   1. 建立名為 `install.standby` 在 `aem-standby/crx-quickstart/install`

   1. 建立兩個名為：

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. 建立名為 `crx3` 在 `aem-standby/crx-quickstart/install`

   1. 建立資料儲存配置並將其放在 `aem-standby/crx-quickstart/install/crx3`。 在此示例中，需要建立的檔案是：

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. 編輯檔案並建立必要的配置。

   以下是典型備用實例的示例配置檔案：

   **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 啟動 **備用** 實例：

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

也可以通過Web控制台通過以下方式配置服務：

1. 轉到Web控制台： *https://serveraddress:serverport/system/console/configMgr*
1. 正在查找名為 **Apache Jackrabbit Oak Segment Tar冷備用服務** 並按兩下它以編輯設定。
1. 保存設定並重新啟動實例，以便新設定生效。

>[!NOTE]
>
>您可以隨時檢查實例的角色，方法是檢查 **主** 或 **備用** Sling Settings Web控制台中的runmodes。
>
>這可以通過 *https://localhost:4502/system/console/status-slingsettings* 檢查 **&quot;運行模式&quot;** 。

## 首次同步 {#first-time-synchronization}

準備完成並首次啟動備用後，當備用接近主實例時，實例之間將會出現大量網路流量。 您可以查閱日誌來觀察同步的狀態。

待機 *tarmk-coldstandby.log*，您會看到以下條目：

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

在待命的 *錯誤.log*，您應看到以下條目：

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

在上述日誌片段中， *10.20.30.40* 是主IP地址。

在 **主** *tarmk-coldstandby.log*，您會看到以下條目：

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

在本例中，日誌中提到的「客戶端」是 **備用** 實例。

一旦這些條目停止出現在日誌中，您就可以放心地假定同步過程已完成。

儘管上述條目顯示輪詢機制正常工作，但瞭解是否在輪詢發生時有任何資料正在同步通常非常有用。 為此，請查找以下條目：

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

此外，當使用非共用運行時 `FileDataStore`，以下消息將確認正在正確傳輸二進位檔案：

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 設定 {#configuration}

以下OSGi設定可用於冷備用服務：

* **持久配置：** 如果啟用，則會將配置儲存在儲存庫中，而不是傳統的OSGi配置檔案。 建議在生產系統上禁用此設定，以便主配置不會被備用系統拉動。

* **模式(`mode`):** 這將選擇實例的運行模式。

* **埠（埠）:** 用於通信的埠。 預設為 `8023`。

* **主主機(`primary.host`):**  — 主實例的主機。 此設定僅適用於備用。
* **同步間隔(`interval`):**  — 此設定確定同步請求之間的間隔，並且僅適用於備用實例。

* **允許的IP範圍(`primary.allowed-client-ip-ranges`):**  — 主伺服器允許連接的IP範圍。
* **安全(`secure`):** 啟用SSL加密。 為了利用此設定，必須在所有實例上啟用此設定。
* **待機讀取超時(`standby.readtimeout`):** 從備用實例發出的請求超時（毫秒）。 使用的預設值是60000（1分鐘）。

* **備用自動清除(`standby.autoclean`):** 如果儲存的大小在同步週期上增加，則調用清理方法。

>[!NOTE]
>
>強烈建議主和備用機具有不同的儲存庫ID，以便對於卸載等服務可以單獨確定它們。
>
>確保覆蓋此內容的最佳方法是刪除 *sling.id* 檔案，然後重新啟動實例。

## 故障轉移過程 {#failover-procedures}

如果主實例因任何原因失敗，可以通過更改啟動運行模式將其中一個備用實例設定為充當主實例的角色，具體如下所述：

>[!NOTE]
>
>還需要修改配置檔案，以便它們與主實例使用的設定相匹配。

1. 轉到安裝備用實例的位置，並停止它。

1. 如果已使用安裝程式配置了負載平衡器，則可以在此時從負載平衡器配置中刪除主平衡器。
1. 備份 `crx-quickstart` 從備用安裝資料夾中找到的資料夾。 在設定新備用時，它可以用作起點。

1. 使用 `primary` 運行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 向負載平衡器中添加新的主資料。
1. 建立並啟動新的備用實例。 有關詳細資訊，請參閱上面的步驟 [建立AEMTarMK冷備用設定](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)。

## 將熱修復程式應用於冷備用設定 {#applying-hotfixes-to-a-cold-standby-setup}

將修補程式應用到冷備份安裝程式的建議方法是將它們安裝到主實例，然後將其克隆到安裝了修補程式的新冷備份實例中。

您可以按照以下步驟執行此操作：

1. 通過轉到JMX控制台並使用**org.apache.jackrabbit.oak停止冷備用實例上的同步過程：狀態（「待機」）**bean。 有關如何執行此操作的詳細資訊，請參閱 [監視](#monitoring)。
1. 停止冷備用實例。
1. 在主實例上安裝修補程式。 有關如何安裝修補程式的詳細資訊，請參見 [如何使用包](/help/sites-administering/package-manager.md)。
1. Test安裝後問題的實例。
1. 通過刪除其安裝資料夾來刪除冷備用實例。
1. 停止主實例並克隆它，方法是將其整個安裝資料夾的檔案系統副本複製到冷備用資料夾的位置。
1. 重新配置新建立的克隆以充當冷備用實例。 有關其他詳細資訊，請參閱 [建立AEMTarMK冷備用設定。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 啟動主實例和冷備用實例。

## 監控 {#monitoring}

該功能使用JMX或MBean公開資訊。 這樣，您可以使用 [JMX控制台](/help/sites-administering/jmx-console.md)。 在MBean中可找到該資訊 `type org.apache.jackrabbit.oak:type="Standby"`命名 `Status`。

**待機**

觀察待機實例時，您將公開一個節點。 ID通常是泛型UUID。

此節點有五個只讀屬性：

* `Running:` 指示同步進程是否正在運行的布爾值。

* `Mode:` 客戶端：後跟用於標識實例的UUID。 請注意，每次更新配置時，此UUID都會更改。

* `Status:` 當前狀態的文本表示(如 `running` 或 `stopped`)。

* `FailedRequests:`連續錯誤數。
* `SecondsSinceLastSuccess:` 自上次成功與伺服器通信以來的秒數。 它將顯示 `-1` 未成功通信。

還有三種可調用的方法：

* `start():` 啟動同步進程。
* `stop():` 停止同步進程。
* `cleanup():` 在待機狀態下運行清理操作。

**主要**

觀察主伺服器通過ID值為TarMK備用服務使用的埠號的MBean公開一些一般資訊（預設情況下為8023）。 大多數方法和屬性與待機相同，但有些不同：

* `Mode:` 將始終顯示值 `primary`。

此外，還可以檢索與主設備連接的多達10個客戶機（備用實例）的資訊。 MBean ID是實例的UUID。 這些MBean沒有可調用的方法，但有一些非常有用的只讀屬性：

* `Name:` 客戶端的ID。
* `LastSeenTimestamp:` 文本表示中最後一個請求的時間戳。
* `LastRequest:` 客戶的最後一個請求。
* `RemoteAddress:` 客戶端的IP地址。
* `RemotePort:` 客戶端用於上次請求的埠。
* `TransferredSegments:` 傳輸到此客戶端的段總數。
* `TransferredSegmentBytes:`傳輸到此客戶端的位元組總數。

## 冷備用儲存庫維護 {#cold-standby-repository-maintenance}

### 修訂清除 {#revision-clean}

>[!NOTE]
>
>如果您運行 [聯機修訂版清除](/help/sites-deploying/revision-cleanup.md) 在主實例上，不需要下面介紹的手動過程。 此外，如果使用「線上修訂版清除」， `cleanup ()` 將自動執行對備用實例的操作。

>[!NOTE]
>
>請勿在備用系統上運行離線修訂版清除。 不需要，也不會減小分段儲存的大小。

Adobe建議定期運行維護，以防止儲存庫隨時間推移過度增長。 要手動執行冷備用儲存庫維護，請執行以下步驟：

1. 通過轉到JMX控制台並使用 **org.apache.jackrabbit.oak:狀態（「待機」）** 豆。 有關如何執行此操作的詳細資訊，請參閱上面的 [監視](/help/sites-deploying/tarmk-cold-standby.md#monitoring)。

1. 停止主實AEM例。
1. 在主實例上運行橡木壓縮工具。 有關詳細資訊，請參閱 [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。
1. 啟動主實例。
1. 使用與第一步中描述的相同JMX Bean在備用實例上啟動備用進程。
1. 監視日誌並等待同步完成。 此時，備用儲存庫可能會大幅增長。
1. 運行 `cleanup()` 在備用實例上執行操作，使用與第一步中描述的相同JMX Bean。

備用實例完成與主實例的同步可能比通常花費的時間長，因為離線壓縮可以有效地重寫儲存庫歷史記錄，因此計算儲存庫中的更改需要更長時間。 還應注意的是，一旦此過程完成，備用系統上的儲存庫大小將與主系統上的儲存庫大小大致相同。

作為替代方法，在主儲存庫上運行壓縮後，可以手動將主儲存庫複製到備用儲存庫，實際上是每次壓縮運行時都重建備用儲存庫。

### 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

在檔案資料儲存實例上不時運行垃圾回收非常重要，否則，已刪除的二進位檔案將保留在檔案系統上，最終會填滿驅動器。 要運行垃圾收集，請執行以下步驟：

1. 運行冷備用儲存庫維護，如一節所述 [上](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance)。
1. 維護過程完成並重新啟動實例後：

   * 在主系統上，通過相關的JMX Bean運行資料儲存垃圾收集，如中所述 [這篇文章](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console)。
   * 在待機時，資料儲存垃圾收集僅通過 **BlobGarbageCollection** MBean - `startBlobGC()`。 **RepositoryManagement **MBean在備用系統上不可用。

   >[!NOTE]
   >
   >如果您未使用共用資料儲存，則垃圾回收首先必須在主儲存上運行，然後在備用儲存上運行。
