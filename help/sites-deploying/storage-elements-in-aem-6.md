---
title: 6.5中AEM的儲存元素
seo-title: Storage Elements in AEM 6.5
description: 瞭解6.5中提供的節點AEM儲存實施以及如何維護儲存庫。
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

# 6.5中AEM的儲存元素{#storage-elements-in-aem}

本文包括以下內容：

* [6中的儲存概AEM述](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## 6中的儲存概AEM述 {#overview-of-storage-in-aem}

6中最重要的變AEM化之一是儲存庫級別的創新。

目前，在AEM6中有兩種節點儲存實現：Tar儲存和MongoDB儲存。

### 焦油儲存 {#tar-storage}

#### 使用Tar Storage運行新AEM安裝的實例 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>段節點儲存的PID已從org.apache.jackrabbit.oak更改。**插件**.segment.SegmentNodeStoreService，早期版本為AEMorg.apache.jackrabbit.oak.segment.SegmentNodeStoreService,AEM版本為6.3。確保進行必要的配置調整，以反映更改。

預設情況下， AEM 6使用Tar儲存來儲存節點和二進位檔案，使用預設配置選項。 您可以通過執行以下操作手動配置其儲存設定：

1. 下載AEM6快速啟動jar並將其放在新資料夾中。
1. 通過運AEM行解壓縮：

   `java -jar cq-quickstart-6.jar -unpack`

1. 建立名為 `crx-quickstart\install` 的子菜單。

1. 建立名為 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` 的子菜單。

1. 編輯檔案並設定配置選項。 以下選項可用於段節點儲存，這是Tar儲存實施AEM的基礎：

   * `repository.home`:儲存各種與儲存庫相關資料的儲存庫主目錄的路徑。 預設情況下，段檔案將儲存在crx-quickstart/segmentstore目錄下。
   * `tarmk.size`:段的最大大小(MB)。 預設為256 MB。

1. 開始AEM。

### Mongo儲存 {#mongo-storage}

#### 使用Mongo儲存AEM運行新安裝的實例 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

按AEM照以下步驟配置6以使用MongoDB儲存運行：

1. 下載AEM6快速啟動jar並將其放入新資料夾中。
1. 運行AEM以下命令解包：

   `java -jar cq-quickstart-6.jar -unpack`

1. 確保已安裝MongoDB，並且 `mongod` 正在運行。 有關詳細資訊，請參見 [安裝MongoDB](https://docs.mongodb.org/manual/installation/)。
1. 建立名為 `crx-quickstart\install` 的子菜單。
1. 通過建立配置檔案來配置節點儲存區，該配置檔案的名稱是要在 `crx-quickstart\install` 的子菜單。

   文檔節點儲存(是AEMMongoDB儲存實現的基礎)使用名為 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. 編輯檔案並設定配置選項。 以下選項可用：

   * `mongouri`:的 [蒙戈URI](https://docs.mongodb.org/manual/reference/connection-string/) 連接到Mongo資料庫所需。 預設值為 `mongodb://localhost:27017`
   * `db`:Mongo資料庫的名稱。 預設情況下，新AEM6個安裝使用 **aem作者** 作為資料庫名。
   * `cache`:快取大小(MB)。 此快取大小分佈在DocumentNodeStore中使用的各種快取中。 預設值為256。
   * `changesSize`:Mongo中用於快取差異輸出的封蓋集合的大小(MB)。 預設值為256。
   * `customBlobStore`:指示使用自定義資料儲存的布爾值。 預設值為false。

1. 使用要使用的資料儲存的PID建立配置檔案，並編輯該檔案以設定配置選項。 有關詳細資訊，請參閱 [配置節點儲存和資料儲存](/help/sites-deploying/data-store-config.md)。

1. 通過運AEM行以下命令，啟動具有MongoDB儲存後端的6jar:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   後端運行模式為 **`-r`**，該示例以MongoDB支援開始。

#### 禁用透明大頁 {#disabling-transparent-huge-pages}

Red Hat® Linux®使用稱為「透明大頁」(THP)的記憶體管理算法。 執行細AEM粒度的讀取和寫入時，THP會針對大型操作而優化。 因此，建議您在Tar和Mongo儲存上禁用THP。 要禁用該算法，請執行以下步驟：

1. 開啟 `/etc/grub.conf` 的子菜單。
1. 將以下行添加到 **grub.conf** 檔案：

   ```
   transparent_hugepage=never
   ```

1. 最後，通過運行以下命令檢查設定是否生效：

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，則上述命令的輸出應為：

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>請查閱以下資源：
>
>* 有關Red Hat® Linux®上的透明大頁的詳細資訊，請參閱 [文章](https://access.redhat.com/solutions/46111)。
* 有關Linux®調整提示，請參閱 [文章](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hant)。
>


## 維護儲存庫 {#maintaining-the-repository}

每個對儲存庫的更新都建立一個內容修訂版。 因此，每次更新後，儲存庫的大小都會增大。 為避免儲存庫增長失控，必須清理舊版本以釋放磁碟資源。 此維護功能稱為修訂版清除。 修訂版清除機制通過從儲存庫中刪除過時資料來回收磁碟空間。 有關修訂版清除的詳細資訊，請閱讀 [「修訂版清除」頁](/help/sites-deploying/revision-cleanup.md)。
