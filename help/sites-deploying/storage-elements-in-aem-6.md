---
title: AEM 6.5中的儲存元素
description: 瞭解AEM 6.5中可用的節點儲存實施以及如何維護存放庫。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: db7830895c8a2d1b7228dc4780296d43f15776df
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# AEM 6.5中的儲存元素{#storage-elements-in-aem}

本文涵蓋下列內容：

* [AEM 6儲存空間概覽](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [維護存放庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6儲存空間概覽 {#overview-of-storage-in-aem}

AEM 6最重要的變更之一是存放庫層級的創新。

目前，AEM6提供兩種節點儲存實作： Tar儲存和MongoDB儲存。

### Tar儲存 {#tar-storage}

#### 使用Tar儲存體執行全新安裝的AEM執行個體 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>區段節點存放區的PID已從org.apache.jackrabbit.oak變更。在AEM 6舊版的&#x200B;**plugins**.segment.SegmentNodeStoreService中新增至AEM 6.3中的org.apache.jackrabbit.oak.segment.SegmentNodeStoreService。請確定已進行必要的設定調整，以便反映變更。

依預設，AEM 6會使用Tar儲存空間，使用預設的設定選項來儲存節點和二進位檔案。 您可以執行下列動作，手動設定其儲存設定：

1. 下載AEM 6快速入門Jar並將其放入新資料夾中。
1. 透過執行以下動作解壓縮AEM：

   `java -jar cq-quickstart-6.jar -unpack`

1. 在安裝目錄中建立名為`crx-quickstart\install`的資料夾。

1. 在新建立的資料夾中建立名為`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`的檔案。

1. 編輯檔案並設定組態選項。 下列選項適用於「區段節點存放區」，這是AEM Tar儲存體實作的基礎：

   * `repository.home`：儲存各種存放庫相關資料的存放庫首頁路徑。 依預設，區段檔案會儲存在crx-quickstart/segmentstore目錄下。
   * `tarmk.size`：區段的大小上限（以MB為單位）。 預設值為256 MB。

1. 啟動AEM。

### Mongo儲存 {#mongo-storage}

#### 使用Mongo Storage執行全新安裝的AEM執行個體 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6可設定為使用MongoDB儲存體執行，請遵循以下程式：

1. 下載AEM 6快速入門Jar並將其放入新資料夾中。
1. 執行下列命令以解壓縮AEM：

   `java -jar cq-quickstart-6.jar -unpack`

1. 確定已安裝MongoDB且正在執行`mongod`的執行個體。 如需詳細資訊，請參閱[安裝MongoDB](https://docs.mongodb.org/manual/installation/)。
1. 在安裝目錄中建立名為`crx-quickstart\install`的資料夾。
1. 建立組態檔，使用您要在`crx-quickstart\install`目錄中使用的組態名稱來設定節點存放區。

   檔案節點存放區(AEM MongoDB儲存實作的基礎)使用名為`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`的檔案

1. 編輯檔案並設定組態選項。 下列選項可供使用：

   * `mongouri`：連線至Mongo資料庫所需的[MongoURI](https://docs.mongodb.org/manual/reference/connection-string/)。 預設值為`mongodb://localhost:27017`
   * `db`： Mongo資料庫的名稱。 根據預設，新的AEM 6安裝使用&#x200B;**aem-author**&#x200B;作為資料庫名稱。
   * `cache`：快取大小(MB)。 此快取大小分佈於DocumentNodeStore中使用的各種快取中。 預設值為256。
   * `changesSize`： Mongo中用於快取diff輸出的限定集合大小（以MB為單位）。 預設值為256。
   * `customBlobStore`：表示使用自訂資料存放區的布林值。 預設值為false。

1. 以您要使用之資料存放區的PID建立設定檔案，並編輯檔案以設定設定選項。 如需詳細資訊，請參閱[設定節點存放區和資料存放區](/help/sites-deploying/data-store-config.md)。

1. 執行，啟動具有MongoDB儲存後端的AEM 6 jar：

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   其中後端執行模式為&#x200B;**`-r`**，範例從MongoDB支援開始。

#### 停用透明大型頁面 {#disabling-transparent-huge-pages}

Red Hat® Linux®使用稱為Transparent Great Pages (THP)的記憶體管理演演算法。 雖然AEM會執行微調的讀取和寫入，但THP已針對大型作業最佳化。 因此，建議您在Tar和Mongo儲存空間中停用THP。 若要停用演演算法，請執行下列步驟：

1. 在您選擇的文字編輯器中開啟`/etc/grub.conf`檔案。
1. 將下列行加入&#x200B;**grub.conf**&#x200B;檔案：

   ```
   transparent_hugepage=never
   ```

1. 最後，執行以檢查設定是否已生效：

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果停用THP，上述指令的輸出應該是：

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>請參閱下列資源：
>
>* 如需Red Hat® Linux®上透明大型頁面的詳細資訊，請參閱Red Hat®客戶入口網站的下列文章： [如何在Red Hat Enterprise Linux 6、7和8中使用、監視和停用透明大型頁面？](https://access.redhat.com/solutions/46111)
>* 如需Linux®調整秘訣，請參閱[效能最佳化](/help/sites-deploying/configuring-performance.md)。
>

## 維護存放庫 {#maintaining-the-repository}

存放庫的每次更新都會建立內容修訂版本。 因此，隨著每次更新，存放庫的大小都會增加。 為避免儲存庫成長不受控制，必須清理舊修訂以釋放磁碟資源。 此維護功能稱為「修訂清除」。 修訂清除機制會從存放庫中移除過時的資料，以回收磁碟空間。 如需修訂清除的詳細資訊，請閱讀[修訂清除頁面](/help/sites-deploying/revision-cleanup.md)。
