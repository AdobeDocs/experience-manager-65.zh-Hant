---
title: AEM 6.5中的儲存元素
seo-title: Storage Elements in AEM 6.5
description: 了解AEM 6.5中可用的節點儲存實作，以及如何維護存放庫。
seo-description: Learn about the node storage implementations available in AEM 6.5 and how to maintain the repository.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 1%

---

# AEM 6.5中的儲存元素{#storage-elements-in-aem}

本文涵蓋下列內容：

* [AEM 6中的儲存概觀](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6中的儲存概觀 {#overview-of-storage-in-aem}

AEM 6最重要的變更之一，是存放庫層級的創新功能。

目前，AEM6中提供兩種節點儲存實作：Tar儲存和MongoDB儲存。

### Tar儲存 {#tar-storage}

#### 使用Tar Storage執行新安裝的AEM執行個體 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>「區段」節點存放區的PID已從org.apache.jackrabbit.oak變更。**外掛程式** AEM 6.3中舊版AEM 6中的.segment.SegmentNodeStoreService轉換為org.apache.jackrabbit.oak.segment.SegmentNodeStoreService。請務必進行必要的設定調整，以反映變更。

依預設，AEM 6會使用Tar儲存來儲存節點和二進位檔，使用預設設定選項。 您可以執行下列操作，手動配置其儲存設定：

1. 下載AEM 6 Quickstart Jar，並將其放入新資料夾中。
1. 執行以解壓縮AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 建立名為 `crx-quickstart\install` （在安裝目錄中）。

1. 建立檔案，稱為 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` 在新建立的資料夾中。

1. 編輯檔案並設定配置選項。 區段節點存放區提供下列選項，此為AEM Tar儲存實作的基礎：

   * `repository.home`:儲存各種與儲存庫相關資料的儲存庫首頁的路徑。 依預設，區段檔案會儲存在crx-quickstart/segmentstore目錄下。
   * `tarmk.size`:段的最大大小(MB)。 預設為256 MB。

1. 啟動AEM。

### Mongo儲存 {#mongo-storage}

#### 使用Mongo儲存執行新安裝的AEM執行個體 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6可依照下列程式設定為透過MongoDB儲存執行：

1. 下載AEM 6 Quickstart Jar，並將其放入新資料夾中。
1. 執行下列命令來解壓縮AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 請確定已安裝MongoDB，且 `mongod` 執行中。 如需詳細資訊，請參閱 [安裝MongoDB](https://docs.mongodb.org/manual/installation/).
1. 建立名為 `crx-quickstart\install` （在安裝目錄中）。
1. 建立組態檔，使用您要在 `crx-quickstart\install` 目錄。

   Document Node Store(是AEM MongoDB儲存實作的基礎)使用檔案，稱為 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. 編輯檔案並設定配置選項。 可使用下列選項：

   * `mongouri`:此 [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) 連接到Mongo資料庫所需。 預設為 `mongodb://localhost:27017`
   * `db`:Mongo資料庫的名稱。 依預設，新的AEM 6安裝會使用 **aem-author** 作為資料庫名稱。
   * `cache`:快取大小(MB)。 此快取大小分佈在DocumentNodeStore中使用的各種快取中。 預設為256。
   * `changesSize`:用於快取差異輸出的Mongo中封閉集合的大小(MB)。 預設為256。
   * `customBlobStore`:指示已使用自訂資料存放區的布林值。 預設值為false。

1. 使用要使用的資料儲存的PID建立配置檔案，並編輯該檔案以設定配置選項。 如需詳細資訊，請參閱 [配置節點儲存和資料儲存](/help/sites-deploying/data-store-config.md).

1. 執行以下作業，啟動AEM 6 jar並帶有MongoDB儲存後端：

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   後端執行模式為 **`-r`**，此範例以MongoDB支援開頭。

#### 禁用透明大頁 {#disabling-transparent-huge-pages}

Red Hat® Linux®使用名為「透明大頁」(THP)的記憶體管理算法。 當AEM執行微調讀取和寫入時，THP會針對大型作業而最佳化。 因此，建議您同時在Tar和Mongo儲存上停用THP。 若要停用演算法，請依照下列步驟操作：

1. 開啟 `/etc/grub.conf` 檔案。
1. 將下列行新增至 **grub.conf** 檔案：

   ```
   transparent_hugepage=never
   ```

1. 最後，檢查設定是否已通過運行生效：

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，則上述命令的輸出應為：

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>請參閱下列資源：
>
>* 有關Red Hat® Linux®上的透明大頁的詳細資訊，請參見此 [文章](https://access.redhat.com/solutions/46111).
* 有關Linux®調整提示，請參見以下內容 [文章](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hant).
>


## 維護儲存庫 {#maintaining-the-repository}

每個對儲存庫的更新都會建立內容修訂。 因此，每次更新時，存放庫的大小都會增加。 為避免儲存庫增長失控，必須清理舊修訂版本以釋放磁碟資源。 此維護功能稱為修訂清除。 修訂清除機制會移除存放庫中的過時資料，以回收磁碟空間。 如需修訂清除的詳細資訊，請參閱 [修訂清除頁面](/help/sites-deploying/revision-cleanup.md).
