---
title: 在AEM 6中設定節點儲存區和資料儲存區
seo-title: 在AEM 6中設定節點儲存區和資料儲存區
description: 瞭解如何設定節點儲存區和資料儲存區，以及如何執行資料儲存區廢棄項目收集。
seo-description: 瞭解如何設定節點儲存區和資料儲存區，以及如何執行資料儲存區廢棄項目收集。
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 在AEM 6中設定節點儲存區和資料儲存區{#configuring-node-stores-and-data-stores-in-aem}

## 簡介 {#introduction}

在Adobe Experience Manager(AEM)中，二進位資料可獨立於內容節點儲存。 二進位資料被儲存在資料儲存中，而內容節點被儲存在節點儲存中。

可以使用OSGi配置配置資料儲存和節點儲存。 每個OSGi配置都使用永久標識符(PID)被引用。

## 配置步驟 {#configuration-steps}

要同時配置節點儲存和資料儲存，請執行以下步驟：

1. 將AEM快速入門JAR檔案複製至其安裝目錄。
1. 在安裝目 `crx-quickstart/install` 錄中建立資料夾。
1. 首先，通過建立一個配置檔案來配置節點儲存，該配置檔案的名稱為要在目錄中使用的節點儲存選 `crx-quickstart/install` 項。

   例如，Document節點儲存區（AEM的MongoMK實作的基礎）會使用檔案 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`。

1. 編輯檔案並設定您的設定選項。
1. 使用您要使用的資料存放區的PID建立設定檔。 編輯檔案以設定配置選項。

   >[!NOTE]
   >
   >有關配 [置選項，請參閱節點存](#node-store-configurations) 儲 [配置和資料儲存配置](#data-store-configurations) 。

1. 啟動AEM。

## 節點儲存配置 {#node-store-configurations}

>[!CAUTION]
>
>較新版本的Oak採用新的OSGi組態檔命名方案和格式。 新命名方案要求將配置檔案命名為 **.config** ，而新格式要求鍵入值，並在此處 [說明](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)。
>
>如果您從舊版Oak升級，請確定您先備份資料 `crx-quickstart/install`夾。 升級後，將資料夾的內容還原到升級的安裝，並將配置檔案的副檔名從 **.cfg** 修改 **為。config**。
>
>如果您正在閱讀本文以準備從 **AEM 5.x安裝進行升級** ，請務必先參閱 [升級檔案](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) 。

### 區段節點儲存區 {#segment-node-store}

區段節點儲存區是Adobe在AEM6中實作TarMK的基礎。 它使用 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID進行配置。

>[!CAUTION]
>
>「區段」節點儲存區的PID已從 `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` AEM 6變更為 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` AEM 6.3。請務必進行必要的組態調整，以反映此變更。

您可以設定下列選項：

* `repository.home`:儲存與儲存庫相關資料的儲存庫主目錄的路徑。 依預設，區段檔案會儲存在目錄 `crx-quickstart/segmentstore` 下。

* `tarmk.size`:區段的最大大小(MB)。 預設上限為256MB。
* `customBlobStore`:指示使用自訂資料存放區的布林值。 AEM 6.3及更新版本的預設值為true。 在AEM 6.3之前，預設值為false。

以下是範例檔 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 案：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Document Node Store {#document-node-store}

檔案節點儲存區是AEM MongoMK實作的基礎。 它使用 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 可使用下列配置選項：

* `mongouri`:連接 [到Mongo資料庫](https://docs.mongodb.org/manual/reference/connection-string/) 所需的MongoURI。 預設值為 `mongodb://localhost:27017`

* `db`:Mongo資料庫的名稱。 預設值為 **Oak**``. However, new AEM 6 installations use **aem-author** ``作為預設資料庫名。

* `cache`:快取大小(MB)。 這會分佈在DocumentNodeStore中使用的各種快取中。 預設值為 `256`

* `changesSize`:Mongo中用於快取比較輸出的封頂系列大小(MB)。 預設值為 `256`

* `customBlobStore`:指示將使用自訂資料存放區的布林值。 預設值為 `false`。

以下是範例檔 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` 案：

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## 資料儲存配置 {#data-store-configurations}

在處理大量二進位檔案時，建議使用外部資料存放區，而非預設節點儲存區，以發揮最大效能。

例如，如果您的專案需要大量的媒體資產，將它們儲存在「檔案」或「S3資料存放區」下，將比直接儲存在MongoDB中更快速地存取它們。

File Data Store提供比MongoDB更好的效能，而Mongo備份和恢復操作在大量資產的情況下也較慢。

以下說明不同資料儲存區和組態的詳細資訊。

>[!NOTE]
>
>為啟用自訂資料存放區，您必須確 `customBlobStore` 定在 `true` Node Store組態檔(區段節點存放區[或](/help/sites-deploying/data-store-config.md#segment-node-store) 檔案節點存放區 [](/help/sites-deploying/data-store-config.md#document-node-store))中設定。

### 檔案資料存放區 {#file-data-store}

這是Jackrabbit 2中 [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) 的實作。 它提供了一種將二進位資料作為普通檔案儲存在檔案系統上的方法。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID。

這些配置選項可用：

* `repository.home`:儲存各種儲存庫相關資料的儲存庫主目錄的路徑。 預設情況下，二進位檔案將儲存在目 `crx-quickstart/repository/datastore` 錄下

* `path`:儲存檔案的目錄的路徑。 如果指定，則優先於值 `repository.home`

* `minRecordLength`:資料儲存中儲存的檔案的最小大小（以位元組為單位）。 小於此值的二進位內容會內嵌在內。

>[!NOTE]
>
>使用NAS儲存共用檔案資料儲存時，請確保只使用高效能設備以避免效能問題。

## Amazon S3 Data Store {#amazon-s-data-store}

AEM可設定為將資料儲存在Amazon的Simple Storage Service(S3)中。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID進行配置。

為了啟用S3資料儲存功能，需要下載並安裝包含S3資料儲存連接器的功能包。 前往 [Adobe Repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/) ，從1.10.x版的功能套件下載最新版本（例如com.adobe.granite.oak.s3connector-1.10.0.zip）。 此外，您也需要下載並安裝AEM 6.5版本注意事項頁面中所列的最 [新AEM Service Pack](/help/release-notes/sp-release-notes.md) 。

>[!NOTE]
>
>將AEM與TarMK搭配使用時，預設會在中儲存二進位檔 `FileDataStore`案。 若要搭配S3資料儲存區使用TarMK，您必須使用執行 `crx3tar-nofds` 模式啟動AEM，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以按如下方式安裝和配置S3連接器：

1. 將功能套件zip檔案的內容解壓縮至暫存資料夾。

1. 轉至臨時資料夾並導航到以下位置：

   ```xml
   jcr_root/libs/system/install
   ```

   將上述位置的所有內容複製至 `<aem-install>/crx-quickstart/install.`

1. 如果AEM已設定成可搭配Tar或MongoDB儲存，請先從****&lt;aem-install>***/*crx-quickstart*/*install* 資料夾移除任何現有的設定檔案，然後再繼續。 需要移除的檔案包括：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回已提取功能包的臨時位置，並複製以下資料夾的內容：

   * `jcr_root/libs/system/config`
   至

   * `<aem-install>/crx-quickstart/install`
   請確定您僅複製當前配置所需的配置檔案。 對於專用資料儲存和共用資料儲存設定，都會複製文 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 件。

   >[!NOTE]
   >
   >在群集設定中，逐個對群集的所有節點執行上述步驟。 此外，請務必對所有節點使用相同的S3設定。

1. 編輯檔案並新增設定所需的設定選項。
1. 啟動AEM。

### 升級至新版1.8.x S3連接器 {#upgrading-to-a-new-version-of-the-x-s-connector}

如果您需要升級至新版本的1.8.x S3連接器（例如，從1.8.0升級至1.8.1），請遵循下列步驟：

1. 停止AEM例項。

1. 導覽至 `<aem-install>/crx-quickstart/install/15` AEM安裝資料夾中，並備份其內容。
1. 備份後，通過刪除資料夾中的所有jar檔案來刪除S3連接器的舊版本及其相依 `<aem-install>/crx-quickstart/install/15` 性，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**
   >[!NOTE]
   >
   >上述檔案名稱僅用於圖示用途，且未確定。

1. 從 [Adobe Repository下載最新版1.8.x功能套件](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)。
1. 將內容解壓縮至個別的檔案夾，然後導覽至 `jcr_root/libs/system/install/15`。
1. 將jar檔案複製 **至AEM安裝資料夾中的**&lt;aem-install>/crx-quickstart/install/15。
1. 啟動AEM並檢查連接器功能。

您可以使用配置檔案和以下選項：

* accessKey:AWS訪問密鑰。
* secretKey:AWS秘密訪問密鑰。 **** 注意：或者， [IAM角色](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) ，可用於身份驗證。 如果您使用的是IAM角色，則不再需要指定 `accessKey` 和 `secretKey`。

* s3Bucket:桶名。
* s3地區：桶區域。
* 路徑：資料儲存的路徑。 預設值為 **&lt;AEM安裝資料夾>/儲存庫／資料存放區**
* minRecordLength:應儲存在資料儲存中的對象的最小大小。 最低／預設值 **為16KB。**
* maxCachedBinarySize:大小小於或等於此大小的二進位檔案將儲存在記憶體快取中。 大小（以位元組為單位）。 預設值為**17408 **(17 KB)。

* cacheSize:快取的大小。 該值以位元組為單位指定。 預設值 **為64GB**。
* 機密：僅在對共用資料儲存設定使用無二進位複製時使用。
* stagingSplitPercentage:配置為用於轉移非同步上載的快取大小的百分比。 預設值為 **10**。
* uploadThreads:用於非同步上載的上載線程數。 預設值為 **10**。
* stagingPurgeInterval:從預備快取中清除已完成上載的間隔（秒）。 預設值為 **300** 秒（5分鐘）。
* stagingRetryInterval:失敗上載的重試間隔（秒）。 預設值為 **600** 秒（10分鐘）。

### 時段區域選項 {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>美國標準</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>美國西部</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>美國西部（北加州）</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>歐盟（愛爾蘭）<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>亞太地區（新加坡）<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>亞太地區（雪梨）<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>亞太地區（東京）</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>南美洲（聖保羅）<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>

**DataStore快取**

>[!NOTE]
>
>DataStore的實作 `S3DataStore`，並 `CachingFileDataStore` 支 `AzureDataStore` 援本機檔案系統快取。 當DataStore `CachingFileDataStore` 位於NFS（網路檔案系統）上時，該實施非常有用。


從舊版快取實作（Oak 1.6之前版本）升級時，本機檔案系統快取目錄的結構有所不同。 在舊快取結構中，已下載和已上載的檔案都直接放在快取路徑下。 新結構將下載和上載分開，並將它們儲存在名為和快取路徑 `upload` 下的 `download` 兩個目錄中。 升級程式應順暢無阻，而且應排程任何擱置中的上傳，而且在初始化時，快取中任何先前下載的檔案都會放入快取中。

您也可以使用oak-run命令，離線 `datastorecacheupgrade` 升級快取。 有關如何執行命令的詳細資訊，請查看 [oak](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) -run模組的自述檔案。

快取有大小限制，可使用cacheSize參數加以設定。

**下載**

在從DataStore存取請求的檔案/blob之前，將檢查本地快取中的記錄。 當快取在快取中新增檔案時超過設定的限制(請參 `cacheSize` 閱參數)時，會逐出部分檔案以回收空間。

**非同步上傳**

快取支援非同步上傳至DataStore。 檔案會在本機儲存（在檔案系統上），而非同步作業會開始上傳檔案。 非同步上傳的數量受測試快取大小的限制。 測試快取的大小是使用參數來設定 `stagingSplitPercentage` 的。 此參數定義用於測試快取的快取大小百分比。 此外，可下載的快取百分比會計 **算為(100 -`stagingSplitPercentage`)*`cacheSize`**。

非同步上載是多線程的，並且線程數是通過使用參數來配 `uploadThreads` 置的。

上載完成後，檔案將移到主下載快取。 當測試快取大小超過其限制時，檔案會同步上傳至DataStore，直到先前的非同步上傳完成，而且測試快取中的空間又可用。 已上載檔案通過由參數配置間隔的週期性作業從轉移區域中 `stagingPurgeInterval` 刪除。

失敗的上載（例如，由於網路中斷）將被置於重試隊列上並定期重試。 重試間隔是使用配置的 `stagingRetryInterval parameter`。

#### 使用Amazon S3配置無聯機複製 {#configuring-binaryless-replication-with-amazon-s}

要使用S3配置無聯機複製，需要執行以下步驟：

1. 安裝作者和發佈例項，並確定它們已正確啟動。
1. 通過開啟一個頁面到https://localhost:4502/etc/replication/agents.author/publish.html ，轉到複製代理 *設定*。
1. 按「 **Settings** （設定）」區段中的「Edit **** （編輯）」按鈕。
1. 將「序列 **化類型** 」選項變更 **為「無二進位」**。

1. 在傳輸URI中 `binaryless`新 `true`增參數&quot;=&quot;。 變更後，URI的外觀應類似下列：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新啟動所有作者和發佈例項，讓變更生效。

#### 使用S3和MongoDB建立群集 {#creating-a-cluster-using-s-and-mongodb}

1. 使用以下命令解壓縮CQ快速啟動：

   `java -jar cq-quickstart.jar -unpack`

1. 解壓縮AEM後，請在安裝目錄 *crx-quickstart*/*install中建立資料夾*。

1. 在資料夾內建立以下兩個 `crx-quickstart` 檔案：

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*。*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*
   建立檔案後，視需要新增設定選項。

1. 如上所述，安裝S3資料存放區所需的兩個組合。
1. 請確定已安裝MongoDB且執行 `mongod` 個體。
1. 使用下列命令啟動AEM:

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 對第二個AEM例項重複步驟1至4。
1. 啟動第二個AEM例項。

#### 配置共用資料儲存 {#configuring-a-shared-data-store}

1. 首先，在共用資料儲存區所需的每個執行個體上建立資料儲存區設定檔案：

   * 如果您使用的 `FileDataStore`是，請建立名為的檔 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 案，並將它放在檔案 `<aem-install>/crx-quickstart/install` 夾中。

   * 如果使用S3做為資料儲存，請在資料夾中建立名 `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 稱為 `<aem-install>/crx-quickstart/install` 的檔案，如上所示。

1. 修改每個實例上的資料儲存配置檔案以指向同一資料儲存。 如需詳細資訊，請參 [閱本文章](/help/sites-deploying/data-store-config.md#data-store-configurations)。
1. 如果實例已從現有伺服器中克隆，則需要在儲存庫離線時使用 `clusterId` 最新的oak-run工具來刪除新實例。 您需要執行的命令是：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果配置了「段」節點儲存，則需要指定儲存庫路徑。 預設情況下，路徑為 `<aem-install-folder>/crx-quickstart/repository/segmentstore.` If a Document node store is configured you can use [Mongo Connection String URI](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >Oak-run工具可從以下位置下載：
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >請注意，需要根據您與AEM安裝搭配使用的Oak版本，使用不同版本的工具。 請在使用此工具之前，先檢查下列版本需求清單：
   >
   >
   >
   >    * 對於Oak **1.2.x版** ，請使用Oak-run **1.2.12或更新版本**
   >    * 若是比上 **述版本更新的Oak版本**，請使用符合您AEM安裝Oak核心的Oak-run版本。


1. 最後，驗證配置。 為此，您需要查找每個正在共用資料儲存庫的唯一檔案。 檔案的格式為，其中 `repository-[UUID]`UUID是每個單獨儲存庫的唯一標識符。

   因此，正確的配置應具有與共用資料儲存的儲存庫相同的唯一檔案。

   檔案的儲存方式不同，視資料儲存區而定：

   * 對於文 `FileDataStore` 件，在資料儲存資料夾的根路徑下建立檔案。
   * 對於文 `S3DataStore` 件，檔案是在資料夾下配置的S3儲存桶中創 `META` 建的。

## Azure 資料存放區 {#azure-data-store}

AEM可設定為將資料儲存在Microsoft的Azure儲存服務中。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID進行配置。

為啟用Azure資料儲存功能，必須下載並安裝包含Azure連接器的功能套件。 前往 [Adobe Repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) ，從1.6.x版的功能套件下載最新版本（例如com.adobe.granite.oak.azureblobconnector-1.6.3.zip）。

>[!NOTE]
>
>將AEM與TarMK搭配使用時，依預設會將二進位檔案儲存在FileDataStore中。 若要搭配Azure DataStore使用TarMK，您必須使用執行模式 `crx3tar-nofds` 啟動AEM，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可依下列方式安裝及設定Azure連接器：

1. 將功能套件zip檔案的內容解壓縮至暫存資料夾。

1. 轉到臨時資料夾，並將其內容復 `jcr_root/libs/system/install` 制到該文 `<aem-install>crx-quickstart/install` 件夾。
1. 如果AEM已設定為可搭配Tar或MongoDB儲存，請先從資料夾移除任何現有的設定檔案，然 `/crx-quickstart/install` 後再繼續。 需要移除的檔案包括：

   ForMongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   針對TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回已提取特徵包的臨時位置，並將其內容復 `jcr_root/libs/system/config` 制到文 `<aem-install>/crx-quickstart/install` 件夾。
1. 編輯配置檔案並添加設定所需的配置選項。
1. 啟動AEM。

您可以使用配置檔案和以下選項：

* azureSas=&quot;&quot;:在1.6.3版的連接器中，新增了Azure共用存取簽名(SAS)支援。 **如果配置檔案中同時存在SAS和儲存憑據，則SAS具有優先順序。** 有關SAS的更多資訊，請參 [閱官方文檔](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1)。 請確定&#39;=&#39;字元已逸出為&#39;\=&#39;。

* azureBlobEndpoint=&quot;&quot;:Azure Blob端點。 例如，https://&lt;storage-account>.blob.core.windows.net。
* accessKey=&quot;&quot;:儲存帳戶名稱。 如需Microsoft Azure驗證認證的詳細資訊，請參閱官方 [檔案](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account)。

* secretKey=&quot;&quot;:儲存訪問密鑰。 請確定&#39;=&#39;字元已逸出為&#39;\=&#39;。
* container=&quot;&quot;:Microsoft Azure blob儲存容器名稱。 容器是一組膨脹體的群組。 如需詳細資訊，請閱讀官 [方檔案](https://msdn.microsoft.com/en-us/library/dd135715.aspx)。
* maxConnections=&quot;&quot;:每個操作同時發出請求的併發數。 預設值為1。
* maxErrorRetry=&quot;&quot;:每個請求的重試次數。 預設值為3。
* socketTimeout=&quot;&quot;:請求使用的逾時間隔（以毫秒為單位）。 預設值為5分鐘。

除了上述設定外，您也可以設定下列設定：

* 路徑：資料儲存的路徑。 預設值為 `<aem-install>/repository/datastore.`
* RecordLength:應儲存在資料儲存中的對象的最小大小。 預設值為16KB。
* maxCachedBinarySize:大小小於或等於此大小的二進位檔案將儲存在記憶體快取中。 大小（以位元組為單位）。 預設值為17408(17 KB)。
* cacheSize:快取的大小。 該值以位元組為單位指定。 預設為64GB。
* 機密：僅在對共用資料儲存設定使用無二進位複製時使用。
* stagingSplitPercentage:配置為用於轉移非同步上載的快取大小的百分比。 預設值為10。
* uploadThreads:用於非同步上載的上載線程數。 預設值為10。
* stagingPurgeInterval:從預備快取中清除已完成上載的間隔（秒）。 預設值為300秒（5分鐘）。
* stagingRetryInterval:失敗上載的重試間隔（秒）。 預設值為600秒（10分鐘）。

>[!NOTE]
>
>所有設定都應放在引號之間，例如：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Data store garbage collection {#data-store-garbage-collection}

資料儲存廢棄項目收集過程用於移除資料儲存中任何未使用的檔案，從而釋放過程中的寶貴磁碟空間。

您可以透過下列方式執行資料存放區廢棄項目收集：

1. 前往位於https://&lt;serveraddress:port>/system/console/jmx的 *JMX主控台*
1. 正在搜索 **RepositoryManagement。** 在找到儲存庫管理器MBean後，按一下它可開啟可用選項。
1. 捲動至頁面結尾，然後按一下 **startDataStoreGC(boolean markOnly)連結** 。
1. 在下列對話方塊中，輸 `false` 入參 `markOnly` 數，然後按一下 **叫用**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >參 `markOnly` 數表示垃圾收集的掃描階段是否運行。

## 共用資料存放區的資料存放區廢棄項目收集 {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>在叢集或共用資料存放區設定（使用Mongo或區段Tar）中執行廢棄項目收集時，記錄檔可能會顯示有關無法刪除特定點滴ID的警告。 這是因為在先前廢棄項目收集中刪除的blob ID被其他沒有ID刪除資訊的群集或共用節點重新錯誤引用。 因此，在執行廢棄項目收集時，當嘗試刪除上次執行中已刪除的ID時，它會記錄警告。 此行為不會影響效能或功能。

有了較新版本的AEM，資料存放區廢棄項目收集也可以在多個儲存庫共用的資料存放區上執行。 若要在共用資料存放區上執行資料存放區廢棄項目收集，請執行下列步驟：

1. 請確保為資料儲存廢棄項目收集配置的任何維護任務在共用資料儲存的所有儲存庫實例上都被禁用。
1. 在共用資料儲存的所 [有儲存庫實例上](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) ，分別運 **** 行「二進位廢棄項收集」中提及的步驟。 不過，請務必在按一下「叫 `true` 用」按 `markOnly` 鈕前輸入參數：

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有例項上完成上述程式後，從任何例項重新執行資料 **存放** 廢棄項目收集：

   1. 轉到JMX控制台並選擇Repository Manager Mbean。
   1. 按一下「 **Click startDataStoreGC(boolean markOnly)** 」連結。
   1. 在以下對話方塊中， `false` 再次輸入 `markOnly` 參數。
   這會整理使用之前使用的標籤階段找到的所有檔案，並刪除資料儲存區中未使用的其餘檔案。

