---
title: 在AEM 6中配置節點儲存區和資料儲存區
seo-title: 在AEM 6中配置節點儲存區和資料儲存區
description: 了解如何配置節點儲存區和資料儲存區，以及如何執行資料儲存區垃圾收集。
seo-description: 了解如何配置節點儲存區和資料儲存區，以及如何執行資料儲存區垃圾收集。
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
feature: 設定
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: e7038e9c2949cb6326470d0248b640e576c7f919
workflow-type: tm+mt
source-wordcount: '3487'
ht-degree: 0%

---

# 在AEM 6中配置節點儲存區和資料儲存區{#configuring-node-stores-and-data-stores-in-aem}

## 簡介 {#introduction}

在Adobe Experience Manager(AEM)中，二進位資料可與內容節點分開儲存。 二進位資料儲存在資料儲存器中，而內容節點儲存在節點儲存器中。

可以使用OSGi配置配置資料儲存和節點儲存。 每個OSGi設定都使用永久識別碼(PID)來參照。

## 配置步驟 {#configuration-steps}

要配置節點儲存和資料儲存，請執行以下步驟：

1. 將AEM Quickstart JAR檔案複製到其安裝目錄。
1. 在安裝目錄中建立資料夾`crx-quickstart/install`。
1. 首先，通過在`crx-quickstart/install`目錄中建立一個配置檔案，該配置檔案包含要使用的節點儲存選項的名稱。

   例如，Document節點存放區(是AEM MongoMK實作的基礎)使用檔案`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`。

1. 編輯檔案，並設定您的設定選項。
1. 使用您要使用的資料存放區的PID建立設定檔案。 編輯檔案以設定配置選項。

   >[!NOTE]
   >
   >有關配置選項，請參閱[節點儲存配置](#node-store-configurations)和[資料儲存配置](#data-store-configurations)。

1. 啟動AEM。

## 節點儲存配置 {#node-store-configurations}

>[!CAUTION]
>
>較新版本的Oak對OSGi組態檔採用新的命名配置和格式。 新的命名方案要求名為&#x200B;**.config**&#x200B;的配置檔案，而新格式要求鍵入值，且[記錄在此處](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)。
>
>如果您從舊版Oak升級，請務必先備份`crx-quickstart/install`資料夾。 升級後，將資料夾的內容還原到升級的安裝，並將配置檔案的擴展從&#x200B;**.cfg**&#x200B;修改為&#x200B;**.config**。
>
>如果您正在閱讀本文章以準備從&#x200B;**AEM 5.x**&#x200B;安裝進行升級，請務必先參閱[升級](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html)檔案。

### 區段節點存放區 {#segment-node-store}

區段節點存放區是Adobe在AEM6中實作TarMK的基礎。 它使用`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID進行配置。

>[!CAUTION]
>
>AEM 6.3中「區段」節點存放區的PID已從AEM 6的`org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions`變更為`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService`。請務必進行必要的設定調整，以反映此變更。

您可以設定下列選項：

* `repository.home`:儲存與儲存庫相關資料的儲存庫首頁路徑。預設情況下，段檔案儲存在`crx-quickstart/segmentstore`目錄下。

* `tarmk.size`:段的最大大小(MB)。預設最大值為256MB。
* `customBlobStore`:指示已使用自訂資料存放區的布林值。AEM 6.3及更新版本的預設值為true。 AEM 6.3之前的預設值為false。

以下是範例`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`檔案：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 文檔節點儲存 {#document-node-store}

檔案節點存放區是AEM MongoMK實作的基礎。 它使用`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 可使用下列設定選項：

* `mongouri`:連 [](https://docs.mongodb.org/manual/reference/connection-string/) 接到Mongo資料庫所需的MongoURI。預設值為`mongodb://localhost:27017`

* `db`:Mongo資料庫的名稱。預設值為&#x200B;**Oak** ``. However, new AEM 6 installations use **aem-author** ``作為預設資料庫名稱。

* `cache`:快取大小(MB)。這分佈在DocumentNodeStore中使用的各種快取中。 預設值為`256`

* `changesSize`:用於快取差異輸出的Mongo中封閉集合的大小(MB)。預設值為`256`

* `customBlobStore`:指示將使用自訂資料存放區的布林值。預設值為`false`。

以下是範例`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`檔案：

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## 資料儲存配置 {#data-store-configurations}

處理大量二進位檔時，建議使用外部資料存放區，而非預設節點存放區，以發揮最大效能。

例如，如果您的項目需要大量介質資產，則將它們儲存在檔案或S3資料儲存區下將使訪問這些資產的速度比直接儲存在MongoDB中更快。

File Data Store提供的效能比MongoDB更好，而且Mongo備份和還原操作在大量資產的情況下也更慢。

有關不同資料存放區和設定的詳細資訊如下。

>[!NOTE]
>
>若要啟用自訂資料存放區，您必須確定在個別節點存放區組態檔（[區段節點存放區](/help/sites-deploying/data-store-config.md#segment-node-store)或[檔案節點存放區](/help/sites-deploying/data-store-config.md#document-node-store)）中，將`customBlobStore`設為`true`。

### 檔案資料存放區 {#file-data-store}

這是Jackrabbit 2中[FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html)的實作。 它提供了將二進位資料作為普通檔案儲存在檔案系統上的方法。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID。

可使用下列設定選項：

* `repository.home`:儲存各種儲存庫相關資料的儲存庫首頁路徑。預設情況下，二進位檔案將儲存在`crx-quickstart/repository/datastore`目錄下

* `path`:儲存檔案的目錄路徑。如果指定，則其優先於`repository.home`值

* `minRecordLength`:資料儲存中儲存的檔案的最小大小（以位元組為單位）。小於此值的二進位內容會內嵌。

>[!NOTE]
>
>使用NAS儲存共用檔案資料儲存時，請確保僅使用高效能設備，以避免效能問題。

## Amazon S3 Data Store {#amazon-s-data-store}

AEM可設定為將資料儲存在Amazon的簡單儲存服務(S3)中。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID進行配置。

若要啟用S3資料存放區功能，必須下載並安裝包含S3資料存放區連接器的功能套件。 前往[Adobe存放庫](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)，並從1.10.x版的Feature Pack(例如com.adobe.granite.oak.s3connector-1.10.0.zip)下載最新版本。 此外，您也需要下載及安裝[AEM 6.5發行說明](/help/release-notes/sp-release-notes.md)頁面所列的最新AEM Service Pack。

>[!NOTE]
>
>將AEM與TarMK搭配使用時，二進位檔預設會儲存在`FileDataStore`中。 若要將TarMK與S3資料存放區搭配使用，您必須使用`crx3tar-nofds`執行模式啟動AEM，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以依照下列方式安裝及設定S3 Connector:

1. 將Feature Pack zip檔案的內容解壓縮至臨時資料夾。

1. 前往臨時資料夾，並導覽至下列位置：

   ```xml
   jcr_root/libs/system/install
   ```

   將上述位置的所有內容複製到`<aem-install>/crx-quickstart/install.`

1. 如果AEM已設定為可搭配Tar或MongoDB儲存使用，請在繼續操作前，從***&lt;aem-install>***/*crx-quickstart*/*install*&#x200B;資料夾中移除任何現有的組態檔。 需要移除的檔案包括：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回已提取Feature Pack的臨時位置，並複製以下資料夾的內容：

   * `jcr_root/libs/system/config`

   至

   * `<aem-install>/crx-quickstart/install`

   請確保僅複製當前配置所需的配置檔案。 對於專用資料儲存和共用資料儲存設定，都會複製`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`檔案。

   >[!NOTE]
   >
   >在群集設定中，逐個在群集的所有節點上執行上述步驟。 此外，請務必對所有節點使用相同的S3設定。

1. 編輯檔案並新增設定所需的設定選項。
1. 啟動AEM。

### 升級至1.10.x S3連接器的新版本 {#upgrading-to-a-new-version-of-the-s-connector}

如果您需要升級至新版本的1.10.x S3連接器(例如，從1.10.0升級至1.10.4)，請遵循下列步驟：

1. 停止AEM例項。

1. 導覽至AEM安裝資料夾中的`<aem-install>/crx-quickstart/install/15`，並備份其內容。
1. 備份後，請刪除`<aem-install>/crx-quickstart/install/15`資料夾中的所有jar檔案，以刪除舊版S3 Connector及其相依性，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述檔案名稱僅供圖說之用。

1. 從[Adobe存放庫](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)下載最新版1.8.x Feature Pack。
1. 將內容解壓縮至個別資料夾，然後導覽至`jcr_root/libs/system/install/15`。
1. 將jar檔案複製到AEM安裝資料夾中的&#x200B;**&lt;aem-install>**/crx-quickstart/install/15。
1. 啟動AEM並檢查連接器功能。

您可搭配下列選項使用設定檔案：

* accessKey:AWS訪問密鑰。
* secretKey:AWS密鑰訪問密鑰。 **注：** 或者， [IAM](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) 角色可用於身份驗證。如果您使用IAM角色，則不再需要指定`accessKey`和`secretKey`。

* s3Bucket:貯體名稱。
* s3地區：桶區。
* 路徑：資料儲存的路徑。 預設值為&#x200B;**&lt;AEM install folder>/repository/datastore**
* minRecordLength:應儲存在資料儲存區中的對象的最小大小。 最小/預設值為&#x200B;**16KB。**
* maxCachedBinarySize:大小小於或等於此大小的二進位檔會儲存在記憶體快取中。 大小為位元組。 預設為**17408 **(17 KB)。

* cacheSize:快取的大小。 值以位元組為單位指定。 預設值為&#x200B;**64GB**。
* 機密：僅在共用資料存放區設定使用無二進位檔復寫時使用。
* stagingSplitPercentage:配置為用於暫存非同步上載的快取大小的百分比。 預設值為&#x200B;**10**。
* uploadThreads:用於非同步上載的上載線程數。 預設值為&#x200B;**10**。
* stagingPurgeInterval:從暫存快取清除已完成上傳的間隔（秒）。 預設值為&#x200B;**300**&#x200B;秒（5分鐘）。
* stagingRetryInterval:失敗上傳的重試間隔（秒）。 預設值為&#x200B;**600**&#x200B;秒（10分鐘）。

### 貯體區域選項 {#bucket-region-options}

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
   <td>美國西部（北加利福尼亞）</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>歐盟（愛爾蘭）<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>亞太（新加坡）<br /> </td>
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
   <td>南美（聖保羅）<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>

**DataStore快取**

>[!NOTE]
>
>`S3DataStore`、`CachingFileDataStore`和`AzureDataStore`的DataStore實施支援本地檔案系統快取。 當DataStore位於NFS（網路檔案系統）時，`CachingFileDataStore`實現非常有用。


從舊版快取實作（Oak 1.6之前）升級時，本機檔案系統快取目錄的結構會有所差異。 在舊快取結構中，下載的檔案和上傳的檔案都直接放在快取路徑下。 新結構將下載和上載分離，並將它們儲存在快取路徑下名為`upload`和`download`的兩個目錄中。 升級程式應順暢無礙，且任何待上傳內容都應排程上傳，且任何先前下載的檔案都會在初始化時放入快取中。

您也可以使用oak-run的`datastorecacheupgrade`命令，以離線方式升級快取。 如需如何執行命令的詳細資訊，請查看oak-run模組的[readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md)檔案。

快取有大小限制，可使用cacheSize參數進行配置。

**下載內容**

在從DataStore訪問請求的檔案/blob之前，將檢查本地快取中的記錄。 當快取在快取中添加檔案時超過配置的限制（請參見`cacheSize`參數）時，將逐出某些檔案以回收空間。

**非同步上傳**

快取支援非同步上傳至DataStore。 檔案會存放在本機、快取中（在檔案系統上），且非同步作業會開始上傳檔案。 非同步上傳的數量受中繼快取的大小限制。 預備快取的大小是使用`stagingSplitPercentage`參數來配置的。 此參數定義用於暫存快取的快取大小百分比。 此外，下載可用的快取百分比計算為&#x200B;**(100 - `stagingSplitPercentage`)*`cacheSize`**。

非同步上傳為多線程，且使用`uploadThreads`參數配置線程數。

上傳完成後，檔案會移至主下載快取。 當中繼快取大小超過其限制時，檔案會同步上傳至DataStore，直到先前的非同步上傳完成，且中繼快取中的空間可再次使用為止。 上傳的檔案會由間隔由`stagingPurgeInterval`參數設定的定期作業從測試區域中移除。

失敗的上載（例如，由於網路中斷）將放在重試隊列上並定期重試。 重試間隔是使用`stagingRetryInterval parameter`配置的。

#### 使用Amazon S3設定無二進位檔復寫 {#configuring-binaryless-replication-with-amazon-s}

若要使用S3設定無二進位檔復寫，需執行下列步驟：

1. 安裝製作和發佈例項，並確定它們已正確啟動。
1. 開啟頁面至&#x200B;*https://localhost:4502/etc/replication/agents.author/publish.html*，前往復寫代理設定。
1. 按&#x200B;**Settings**&#x200B;部分中的&#x200B;**Edit**&#x200B;按鈕。
1. 將&#x200B;**序列化**&#x200B;類型選項變更為&#x200B;**二進位減**。

1. 在傳輸URI中添加參數&quot; `binaryless`= `true`&quot;。 變更後，uri看起來應類似下列：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新啟動所有製作和發佈執行個體，讓變更生效。

#### 使用S3和MongoDB建立叢集 {#creating-a-cluster-using-s-and-mongodb}

1. 使用下列命令解壓縮CQ快速入門：

   `java -jar cq-quickstart.jar -unpack`

1. 解壓縮AEM後，在安裝目錄&#x200B;*crx-quickstart*/*install*&#x200B;內建立資料夾。

1. 在`crx-quickstart`資料夾中建立以下兩個檔案：

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*。*設定*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*。*設定*

   建立檔案後，視需要新增設定選項。

1. 依照上述說明安裝S3資料存放區所需的兩個套件組合。
1. 確保已安裝MongoDB且`mongod`的實例正在運行。
1. 使用下列命令啟動AEM :

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 對第二個AEM例項重複步驟1到4。
1. 啟動第二個AEM例項。

#### 配置共用資料儲存 {#configuring-a-shared-data-store}

1. 首先，在共用資料儲存所需的每個執行個體上建立資料儲存設定檔案：

   * 如果您使用`FileDataStore`，請建立名為`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`的檔案，並將其放入`<aem-install>/crx-quickstart/install`資料夾中。

   * 如果使用S3作為資料儲存，請如上方在`<aem-install>/crx-quickstart/install`資料夾中建立名為`rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`的檔案。

1. 修改每個執行個體上的資料存放區組態檔，以指向相同的資料存放區。 如需詳細資訊，請參閱[本文](/help/sites-deploying/data-store-config.md#data-store-configurations)。
1. 如果執行個體已從現有伺服器複製，當存放庫離線時，您需要使用最新的oak-run工具來移除新執行個體的`clusterId`。 您需要執行的命令為：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果已設定區段節點存放區，則需指定存放庫路徑。 預設情況下，路徑為`<aem-install-folder>/crx-quickstart/repository/segmentstore.`如果配置了文檔節點儲存，則可以使用[Mongo連接字串URI](https://docs.mongodb.org/manual/reference/connection-string/)。

   >[!NOTE]
   >
   >Oak-run工具可從以下位置下載：
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >請注意，您需根據AEM安裝使用的Oak版本，使用不同版本的工具。 使用此工具之前，請先檢查下方的版本需求清單：
   >
   >
   >
   >    * 若為Oak版本&#x200B;**1.2.x**，請使用Oak-run **1.2.12或更新版本**
   >    * 若Oak版本&#x200B;**較上方**&#x200B;較新，請使用符合AEM安裝之Oak核心的Oak-run版本。


1. 最後，驗證設定。 若要這麼做，您需要尋找共用資料儲存庫的每個存放庫所新增的唯一檔案。 檔案的格式為`repository-[UUID]`，其中UUID是每個個別存放庫的唯一識別碼。

   因此，正確的配置應具有與共用資料儲存的儲存庫相同的唯一檔案。

   檔案的儲存方式會有所不同，具體取決於資料儲存：

   * 對於`FileDataStore`，檔案建立在資料儲存資料夾的根路徑下。
   * 對於`S3DataStore`，檔案會建立在`META`資料夾下已設定的S3儲存貯體中。

## Azure 資料存放區 {#azure-data-store}

AEM可設定為將資料儲存在Microsoft的Azure儲存服務中。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID進行配置。

若要啟用Azure資料儲存功能，必須下載並安裝包含Azure連接器的功能套件。 前往[Adobe存放庫](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/)，並從1.6.x版的Feature Pack（例如com.adobe.granite.oak.azurebconnector-1.6.3.zip）下載最新版本。

>[!NOTE]
>
>將AEM與TarMK搭配使用時，二進位檔預設會儲存在FileDataStore中。 若要將TarMK與Azure DataStore搭配使用，您需要使用`crx3tar-nofds`執行模式啟動AEM，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以依照下列方式安裝及設定Azure連接器：

1. 將Feature Pack zip檔案的內容解壓縮至臨時資料夾。

1. 轉到臨時資料夾，將`jcr_root/libs/system/install`的內容複製到`<aem-install>crx-quickstart/install`資料夾。
1. 如果AEM已配置為使用Tar或MongoDB儲存，請先從`/crx-quickstart/install`資料夾中刪除任何現有配置檔案，然後再繼續。 需要移除的檔案包括：

   MongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   若為TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回已提取Feature Pack的臨時位置，並將`jcr_root/libs/system/config`的內容複製到`<aem-install>/crx-quickstart/install`資料夾。
1. 編輯設定檔案並新增設定所需的設定選項。
1. 啟動AEM。

您可搭配下列選項使用設定檔案：

* azureSas=&quot;&quot;:在連接器1.6.3版中，新增了Azure共用存取簽名(SAS)支援。 **如果配置檔案中同時存在SAS和儲存憑據，則SAS具有優先順序。** 有關SAS的更多資訊，請參 [閱官方檔案](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1)。請確定「=」字元會以「\=」的形式逸出。

* azureBlobEndpoint=&quot;&quot;:Azure Blob端點。 例如， https://&lt;storage-account>.blob.core.windows.net。
* accessKey=&quot;&quot;:儲存帳戶名稱。 有關Microsoft Azure身份驗證憑據的更多詳細資訊，請參閱[官方文檔](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account)。

* secretKey=&quot;&quot;:儲存存取金鑰。 請確定「=」字元會以「\=」的形式逸出。
* container=&quot;&quot;:Microsoft Azure blob儲存容器名稱。 容器是一組blob的分組。 有關其他詳細資訊，請閱讀[官方文檔](https://msdn.microsoft.com/en-us/library/dd135715.aspx)。
* maxConnections=&quot;&quot;:每個操作同時發出的請求數。 預設值為 1。
* maxErrorRetry=&quot;&quot;:每個請求的重試次數。 預設值為 3。
* socketTimeout=&quot;&quot;:用於請求的逾時間隔（以毫秒為單位）。 預設值為5分鐘。

除了上述設定外，您也可以設定下列設定：

* 路徑：資料儲存的路徑。 預設值為`<aem-install>/repository/datastore.`
* RecordLength:應儲存在資料儲存區中的對象的最小大小。 預設為16KB。
* maxCachedBinarySize:大小小於或等於此大小的二進位檔會儲存在記憶體快取中。 大小為位元組。 預設為17408(17 KB)。
* cacheSize:快取的大小。 值以位元組為單位指定。 預設為64GB。
* 機密：僅在共用資料存放區設定使用無二進位檔復寫時使用。
* stagingSplitPercentage:配置為用於暫存非同步上載的快取大小的百分比。 預設值為 10。
* uploadThreads:用於非同步上載的上載線程數。 預設值為 10。
* stagingPurgeInterval:從暫存快取清除已完成上傳的間隔（秒）。 預設值為300秒（5分鐘）。
* stagingRetryInterval:失敗上傳的重試間隔（秒）。 預設值為600秒（10分鐘）。

>[!NOTE]
>
>所有設定都應放在引號之間，例如：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## 資料儲存垃圾收集 {#data-store-garbage-collection}

資料儲存垃圾收集過程用於移除資料儲存中任何未使用的檔案，從而釋放該過程中的寶貴磁碟空間。

您可以通過以下方式運行資料儲存垃圾收集：

1. 轉到位於&#x200B;*https://&lt;serveraddress:port>/system/console/jmx*&#x200B;的JMX控制台
1. 正在搜索&#x200B;**RepositoryManagement。** 找到儲存庫管理器MBean後，按一下該MBean以開啟可用選項。
1. 捲動至頁面結尾，然後按一下&#x200B;**startDataStoreGC(boolean markOnly)**&#x200B;連結。
1. 在以下對話方塊中，為`markOnly`參數輸入`false`，然後按一下&#x200B;**叫用**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >`markOnly`參數表示垃圾收集的掃描階段是否將運行。

## 共用資料儲存的資料儲存垃圾收集 {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>在叢集或共用資料存放區設定（含Mongo或Segment Tar）中執行垃圾收集時，記錄檔可能會顯示無法刪除某些Blob ID的警告。 這是因為以前垃圾收集中刪除的blob ID被沒有ID刪除資訊的其他群集或共用節點重新錯誤引用。 因此，執行垃圾收集時，會在嘗試刪除上次執行中已刪除的ID時記錄警告。 此行為不會影響效能或功能。

>[!NOTE]
> 如果您使用共用資料儲存設定且資料儲存垃圾收集已停用，則運行Lucene Binary清除任務可能會突然增加使用的磁碟空間。 若要避免此情況，您必須依下列方式在所有製作和發佈執行個體上停用BlobTracker:
>
> 1. 停止AEM例項。
> 2. 在`crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`檔案中新增`blobTrackSnapshotIntervalInSecs=L"0"`參數。 此參數需有Oak 1.12.0、1.10.2或更新版本。
> 3. 重新啟動AEM例項。


使用較新的AEM版本時，資料存放區垃圾收集也可在多個存放庫共用的資料存放區上執行。 為了能夠在共用資料儲存上運行資料儲存垃圾收集，請執行以下步驟：

1. 請確保在共用資料儲存的所有儲存庫實例上禁用為資料儲存垃圾收集配置的任何維護任務。
1. 在共用資料儲存的&#x200B;**所有**&#x200B;儲存庫實例上，分別運行[二進位垃圾收集](/help/sites-deploying/data-store-config.md#data-store-garbage-collection)中提及的步驟。 不過，在按一下「叫用」按鈕之前，請務必為`markOnly`參數輸入`true`:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有執行個體上完成上述程式後，請從執行個體的&#x200B;**any**&#x200B;再次執行資料儲存垃圾收集：

   1. 轉到JMX控制台，並選擇儲存庫管理器Mbean。
   1. 按一下&#x200B;**按一下startDataStoreGC(boolean markOnly)**&#x200B;連結。
   1. 在以下對話框中，再次為`markOnly`參數輸入`false`。
   這會整理使用之前使用的標籤階段找到的所有檔案，並刪除資料存放區中未使用的其餘檔案。
