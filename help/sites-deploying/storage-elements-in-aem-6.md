---
title: AEM 6.5中的儲存元素
seo-title: AEM 6.5中的儲存元素
description: 了解AEM 6.5中可用的節點儲存實作，以及如何維護存放庫。
seo-description: 了解AEM 6.5中可用的節點儲存實作，以及如何維護存放庫。
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---

# AEM 6.5{#storage-elements-in-aem}中的儲存元素

在本文中，我們將介紹：

* [AEM 6中的儲存概觀](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6 {#overview-of-storage-in-aem}中的儲存概觀

AEM 6最重要的變更之一，是存放庫層級的創新功能。

目前，AEM6中提供兩種節點儲存實作：Tar儲存和MongoDB儲存。

### Tar儲存{#tar-storage}

#### 運行新安裝的AEM實例(Tar Storage {#running-a-freshly-installed-aem-instance-with-tar-storage})

>[!CAUTION]
>
>區段節點存放區的PID已從org.apache.jackrabbit.oak變更。**AEM 6.3中舊版AEM 6的plugins**.segment.SegmentNodeStoreService外掛程式轉換為org.apache.jackrabbit.oak.segment.SegmentNodeStoreService。請務必進行必要的設定調整，以反映此變更。

依預設，AEM 6會使用Tar儲存來儲存節點和二進位檔，使用預設設定選項。 要手動配置其儲存設定，請遵循以下過程：

1. 下載AEM 6 Quickstart Jar，並將其放入新資料夾中。
1. 執行以解壓縮AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 在安裝目錄中建立名為`crx-quickstart\install`的資料夾。

1. 在新建立的資料夾中建立名為`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`的檔案。

1. 編輯檔案並設定配置選項。 區段節點存放區提供下列選項，此為AEM Tar儲存實作的基礎：

   * `repository.home`:儲存各種儲存庫相關資料的儲存庫首頁路徑。依預設，區段檔案會儲存在crx-quickstart/segmentstore目錄下。
   * `tarmk.size`:段的最大大小(MB)。預設為256MB。

1. 啟動AEM。

### Mongo儲存{#mongo-storage}

#### 運行新安裝的AEM實例(Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage})

AEM 6可依照下列程式設定為透過MongoDB儲存執行：

1. 下載AEM 6 Quickstart Jar，並將其放入新資料夾中。
1. 執行下列命令來解壓縮AEM:

   `java -jar cq-quickstart-6.jar -unpack`

1. 請確保已安裝MongoDB且`mongod`的實例正在運行。 有關詳細資訊，請參閱[安裝MongoDB](https://docs.mongodb.org/manual/installation/)。
1. 在安裝目錄中建立名為`crx-quickstart\install`的資料夾。
1. 通過在`crx-quickstart\install`目錄中建立配置檔案以配置要使用的配置名稱來配置節點儲存。

   文檔節點儲存(是AEM MongoDB儲存實現的基礎)使用名為`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`的檔案

1. 編輯檔案並設定配置選項。 可使用下列選項：

   * `mongouri`:連 [](https://docs.mongodb.org/manual/reference/connection-string/) 接到Mongo資料庫所需的MongoURI。預設值為`mongodb://localhost:27017`
   * `db`:Mongo資料庫的名稱。依預設，新的AEM 6安裝會使用&#x200B;**aem-author**&#x200B;作為資料庫名稱。
   * `cache`:快取大小(MB)。這分佈在DocumentNodeStore中使用的各種快取中。 預設為256。
   * `changesSize`:用於快取差異輸出的Mongo中封閉集合的大小(MB)。預設為256。
   * `customBlobStore`:指示將使用自訂資料存放區的布林值。預設值為false。

1. 使用您要使用的資料儲存的PID建立配置檔案，並編輯該檔案以設定配置選項。 有關詳細資訊，請參閱[配置節點儲存和資料儲存](/help/sites-deploying/data-store-config.md)。

1. 執行以下作業，啟動AEM 6 jar並帶有MongoDB儲存後端：

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   其中&#x200B;**`-r`**&#x200B;是後端執行模式。 在此範例中，會從MongoDB支援開始。

#### 禁用透明大頁{#disabling-transparent-huge-pages}

Red Hat Linux使用名為Transparent Heage Pages(THP)的記憶體管理算法。 當AEM執行微調讀取和寫入時，THP會針對大型作業而最佳化。 因此，建議您同時在Tar和Mongo儲存上停用THP。 若要停用演算法，請依照下列步驟操作：

1. 在您選擇的文字編輯器中開啟`/etc/grub.conf`檔案。
1. 將以下行添加到&#x200B;**grub.conf**&#x200B;檔案中：

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
>此外，您也可以諮詢下列資源：
>
>* 有關Red Hat Linux上的透明大頁的詳細資訊，請參見這篇[文章](https://access.redhat.com/solutions/46111)。
>* 有關Linux調整提示，請參見這篇[文章](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

>



## 維護儲存庫{#maintaining-the-repository}

每個對儲存庫的更新都會建立新的內容修訂。 因此，每次更新時，存放庫的大小都會增加。 為避免儲存庫增長失控，需要清理舊修訂版本以釋放磁碟資源。 此維護功能稱為修訂清除。 修訂清除機制將從儲存庫中移除過時資料，從而回收磁碟空間。 如需修訂清除的詳細資訊，請參閱[修訂清除頁面](/help/sites-deploying/revision-cleanup.md)。
