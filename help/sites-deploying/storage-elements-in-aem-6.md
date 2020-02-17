---
title: AEM 6.5中的儲存元素
seo-title: AEM 6.5中的儲存元素
description: 瞭解AEM 6.5中提供的節點儲存實作，以及如何維護儲存庫。
seo-description: 瞭解AEM 6.5中提供的節點儲存實作，以及如何維護儲存庫。
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# AEM 6.5中的儲存元素{#storage-elements-in-aem}

在本文中，我們將介紹：

* [AEM 6中的儲存空間概觀](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6中的儲存空間概觀 {#overview-of-storage-in-aem}

AEM 6最重要的變更之一，就是存放庫層級的創新。

目前，AEM6提供兩種節點儲存實作：Tar儲存空間和MongoDB儲存空間。

### Tar Storage {#tar-storage}

#### 使用Tar Storage執行新安裝的AEM例項 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>區段節點儲存區的PID已從org.apache.jackrabbit.oak變更。**plugins**.segment.SegmentNodeStoreService（舊版AEM 6中），在AEM 6.3中將其整合為org.apache.jackrabbit.oak.segment.SegmentNodeStoreService。請務必進行必要的組態調整，以反映此變更。

依預設，AEM 6會使用Tar儲存空間，使用預設的設定選項來儲存節點和二進位檔。 要手動配置其儲存設定，請遵循以下過程：

1. 下載AEM 6快速入門jar並將它放入新資料夾。
1. 執行下列動作，解壓縮AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 在安裝目錄中 `crx-quickstart\install` 建立名為的資料夾。

1. 在新建立的資 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` 料夾中建立檔案。

1. 編輯檔案並設定配置選項。 以下選項適用於「區段節點儲存區」，這是AEM Tar儲存區實作的基礎：

   * `repository.home`:儲存各種儲存庫相關資料的儲存庫主目錄的路徑。 依預設，區段檔案會儲存在crx-quickstart/segmentstore目錄下。
   * `tarmk.size`:區段的最大大小(MB)。 預設為256MB。

1. 啟動AEM。

### Mongo Storage {#mongo-storage}

#### 使用Mongo Storage執行新安裝的AEM例項 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6可依下列程式設定為與MongoDB儲存一起執行：

1. 下載AEM 6快速入門JAR並將它放入新資料夾。
1. 執行下列命令，解壓縮AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 請確定已安裝MongoDB且正在運 `mongod` 行實例。 如需詳細資訊，請參 [閱安裝MongoDB](https://docs.mongodb.org/manual/installation/)。
1. 在安裝目錄中 `crx-quickstart\install` 建立名為的資料夾。
1. 通過建立一個配置檔案，使用要在目錄中使用的配置的名稱來配置節點存 `crx-quickstart\install` 儲。

   Document Node Store（AEM的MongoDB儲存實作的基礎）使用名為 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. 編輯檔案並設定您的設定選項。 可使用下列選項：

   * `mongouri`:連接 [到Mongo資料庫](https://docs.mongodb.org/manual/reference/connection-string/) 所需的MongoURI。 預設值為 `mongodb://localhost:27017`
   * `db`:Mongo資料庫的名稱。 依預設，新的AEM 6安裝會 **使用aem-author** 作為資料庫名稱。
   * `cache`:快取大小(MB)。 這會分佈在DocumentNodeStore中使用的各種快取中。 預設值為256。
   * `changesSize`:Mongo中用於快取比較輸出的封頂系列大小(MB)。 預設值為256。
   * `customBlobStore`:指示將使用自訂資料存放區的布林值。 預設值為false。

1. 使用您要使用的資料存放區的PID建立設定檔案，並編輯檔案以設定設定設定選項。 如需詳細資訊，請參 [閱設定節點儲存區和資料儲存區](/help/sites-deploying/data-store-config.md)。

1. 執行下列動作，以啟動具有MongoDB儲存後端的AEM 6jar:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   其中 **`-r`** 是後端執行模式。 在此範例中，它將從MongoDB支援開始。

#### 停用透明巨型頁面 {#disabling-transparent-huge-pages}

Red Hat linux使用稱為透明巨頁(THP)的記憶體管理演算法。 當AEM執行精細的讀取和寫入時，THP會針對大型作業進行最佳化。 因此，建議您同時在Tar和Mongo儲存上停用THP。 若要停用演算法，請依照下列步驟進行：

1. 在您選擇的 `/etc/grub.conf` 文字編輯器中開啟檔案。
1. 將以下行添加到 **grub.conf檔案** :

   ```
   transparent_hugepage=never
   ```

1. 最後，請執行下列動作，檢查設定是否已生效：

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，則上述命令的輸出應為：

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>此外，您也可以參考下列資源：
>
>* 如需Red Hat linux上透明巨頁的詳細資訊，請參閱本 [文](https://access.redhat.com/solutions/46111)。
>* 如需Linux微調秘訣，請參閱本 [文](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。
>



## 維護儲存庫 {#maintaining-the-repository}

每個對儲存庫的更新都會建立新的內容修訂。 因此，隨著每次更新，儲存庫的大小都會增大。 為了避免儲存庫增長失控，需要清理舊版本以釋放磁碟資源。 此維護功能稱為「修訂清除」。 「修訂清除」機制將通過從儲存庫中刪除過時資料來回收磁碟空間。 有關「修訂清除」的詳細資訊，請閱讀「修訂清 [除」頁](/help/sites-deploying/revision-cleanup.md)。
