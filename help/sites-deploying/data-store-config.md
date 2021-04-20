---
title: 在6中配置節點儲存和資料存AEM儲
seo-title: 在6中配置節點儲存和資料存AEM儲
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
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3424'
ht-degree: 0%

---


# 在6{#configuring-node-stores-and-data-stores-in-aem}中配置節AEM點儲存和資料儲存

## 簡介 {#introduction}

在Adobe Experience Manager(AEM)中，二進位資料可以獨立於內容節點儲存。 二進位資料被儲存在資料儲存器中，而內容節點被儲存在節點儲存器中。

可以使用OSGi配置配置資料儲存和節點儲存。 每個OSGi配置都使用永久標識符(PID)被引用。

## 配置步驟{#configuration-steps}

要同時配置節點儲存和資料儲存，請執行以下步驟：

1. 將快速啟AEM動JAR檔案複製到其安裝目錄。
1. 在安裝目錄中建立`crx-quickstart/install`資料夾。
1. 首先，通過建立一個配置檔案，其名稱為要在`crx-quickstart/install`目錄中使用的節點儲存選項，配置節點儲存。

   例如，Document節點儲存(是AEMMongoMK實施的基礎)使用檔案`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`。

1. 編輯檔案並設定您的設定選項。
1. 使用您要使用的資料存放區的PID建立設定檔。 編輯檔案以設定配置選項。

   >[!NOTE]
   >
   >有關配置選項，請參見[節點儲存配置](#node-store-configurations)和[資料儲存配置](#data-store-configurations)。

1. 開始AEM。

## 節點儲存配置{#node-store-configurations}

>[!CAUTION]
>
>較新版本的Oak採用新的OSGi組態檔命名方案和格式。 新命名方案要求將配置檔案命名為&#x200B;**.config** ，而新格式要求鍵入值，並且此處記錄的[。](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)
>
>如果您從舊版Oak升級，請確定您先備份`crx-quickstart/install`資料夾。 升級後，將資料夾的內容還原到升級的安裝，並將配置檔案的副檔名從&#x200B;**.cfg**&#x200B;修改為&#x200B;**.config**。
>
>如果您正在閱讀本文以準備從&#x200B;**AEM 5.x**&#x200B;安裝進行升級，請務必先參閱[upgrade](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html)說明檔案。

### 區段節點儲存{#segment-node-store}

分段節點儲存是AdobeTarMK在AEM6中實現的基礎。 它使用`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID進行配置。

>[!CAUTION]
>
>「區段」節點儲存的PID已從6的`org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions`變AEM更為6.AEM3的`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService`。請務必進行必要的組態調整，以反映此變更。

您可以設定下列選項：

* `repository.home`:儲存與儲存庫相關資料的儲存庫主目錄的路徑。預設情況下，段檔案儲存在`crx-quickstart/segmentstore`目錄下。

* `tarmk.size`:區段的最大大小(MB)。預設上限為256MB。
* `customBlobStore`:指示使用自訂資料存放區的布林值。6.3及更新版本AEM的預設值為true。 在6.AEM3之前，預設值為false。

以下是範例`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`檔案：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 文檔節點儲存{#document-node-store}

文檔節點儲存是MongoMK實AEM現的基礎。 它使用`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 可使用下列配置選項：

* `mongouri`:連接 [](https://docs.mongodb.org/manual/reference/connection-string/) 到Mongo資料庫所需的MongoURI。預設值為`mongodb://localhost:27017`

* `db`:Mongo資料庫的名稱。預設值為&#x200B;**Oak** ``. However, new AEM 6 installations use **aem-author** ``作為預設資料庫名。

* `cache`:快取大小(MB)。這會分佈在DocumentNodeStore中使用的各種快取中。 預設值為`256`

* `changesSize`:Mongo中用於快取比較輸出的封頂系列大小(MB)。預設值為`256`

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

## 資料儲存配置{#data-store-configurations}

在處理大量二進位檔案時，建議使用外部資料存放區，而非預設節點儲存區，以發揮最大效能。

例如，如果您的專案需要大量的媒體資產，將它們儲存在「檔案」或「S3資料存放區」下，將比直接儲存在MongoDB中更快速地存取它們。

File Data Store提供比MongoDB更好的效能，而Mongo備份和恢復操作在大量資產的情況下也較慢。

以下說明不同資料儲存區和組態的詳細資訊。

>[!NOTE]
>
>為了啟用自定義資料儲存，您需要確保在相應的節點儲存配置檔案（[段節點儲存](/help/sites-deploying/data-store-config.md#segment-node-store)或[文檔節點儲存](/help/sites-deploying/data-store-config.md#document-node-store)）中將`customBlobStore`設定為`true`。

### 檔案資料存放區 {#file-data-store}

這是Jackrabbit 2中[FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html)的實作。 它提供了一種將二進位資料作為普通檔案儲存在檔案系統上的方法。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID。

這些配置選項可用：

* `repository.home`:儲存各種儲存庫相關資料的儲存庫主目錄的路徑。預設情況下，二進位檔案將儲存在`crx-quickstart/repository/datastore`目錄下

* `path`:儲存檔案的目錄的路徑。如果指定，則優先於`repository.home`值

* `minRecordLength`:資料儲存中儲存的檔案的最小大小（以位元組為單位）。小於此值的二進位內容會內嵌在內。

>[!NOTE]
>
>使用NAS儲存共用檔案資料儲存時，請確保只使用高效能設備以避免效能問題。

## AmazonS3資料儲存{#amazon-s-data-store}

可AEM以配置為將資料儲存在Amazon的簡單儲存服務(S3)中。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID進行配置。

為了啟用S3資料儲存功能，需要下載並安裝包含S3資料儲存連接器的功能包。 前往[Adobe資料庫](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)，從1.10.x版的功能套件下載最新版本（例如com.adobe.granite.oak.s3connector-1.10.0.zip）。 此外，您還需要下載並安裝[ AEM AEM 6.5發行說明](/help/release-notes/sp-release-notes.md)頁面中所列的最新Service Pack。

>[!NOTE]
>
>與TarMK搭AEM配使用時，預設會將二進位檔儲存在`FileDataStore`中。 要將TarMK與S3資料儲存一起使用，需AEM要開始使用`crx3tar-nofds`運行模式，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以按如下方式安裝和配置S3連接器：

1. 將功能套件zip檔案的內容解壓縮至暫存資料夾。

1. 轉至臨時資料夾並導航到以下位置：

   ```xml
   jcr_root/libs/system/install
   ```

   將上述位置的所有內容複製到`<aem-install>/crx-quickstart/install.`

1. 如果已AEM經配置為使用Tar或MongoDB儲存，請在繼續操作之前，從****&lt;aem-install>**/*crx-quickstart*/*install*&#x200B;資料夾中刪除任何現有配置檔案。 需要移除的檔案包括：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回已提取功能包的臨時位置，並複製以下資料夾的內容：

   * `jcr_root/libs/system/config`

   至

   * `<aem-install>/crx-quickstart/install`

   請確定您僅複製當前配置所需的配置檔案。 對於專用資料儲存和共用資料儲存設定，都複製`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`檔案。

   >[!NOTE]
   >
   >在群集設定中，逐個對群集的所有節點執行上述步驟。 此外，請務必對所有節點使用相同的S3設定。

1. 編輯檔案並新增設定所需的設定選項。
1. 開始AEM。

### 升級至新版1.10.x S3連接器{#upgrading-to-a-new-version-of-the-s-connector}

如果您需要升級至新版本的1.10.x S3連接器（例如，從1.10.0升級至1.10.4），請遵循下列步驟：

1. 停止實AEM例。

1. 導覽至安裝資料夾中的`<aem-install>/crx-quickstart/install/15`AEM並備份其內容。
1. 備份後，通過刪除`<aem-install>/crx-quickstart/install/15`資料夾中的所有jar檔案來刪除舊版S3 Connector及其從屬關係，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述檔案名稱僅用於圖例。

1. 從[Adobe資料庫](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)下載最新版的1.8.x功能包。
1. 將內容解壓縮至個別的資料夾，然後導覽至`jcr_root/libs/system/install/15`。
1. 將jar檔案複製到安裝資料夾中的&#x200B;**&lt;aem-install>**/crx-quickstart/install/15AEM。
1. 啟動AEM並檢查連接器功能。

您可以使用配置檔案和以下選項：

* accessKey:AWS訪問密鑰。
* secretKey:AWS秘密訪問密鑰。 **注意：** 或者， [IAM](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) 角色可用於驗證。如果您使用IAM角色，則不再需要指定`accessKey`和`secretKey`。

* s3Bucket:桶名。
* s3地區：桶區域。
* 路徑：資料儲存的路徑。 預設值為&#x200B;**&lt;AEMinstall folder>/repository/datastore**
* minRecordLength:應儲存在資料儲存中的對象的最小大小。 最小／預設值為&#x200B;**16KB。**
* maxCachedBinarySize:大小小於或等於此大小的二進位檔案將儲存在記憶體快取中。 大小（以位元組為單位）。 預設值為**17408 **(17 KB)。

* cacheSize:快取的大小。 該值以位元組為單位指定。 預設值為&#x200B;**64GB**。
* 機密：僅在對共用資料儲存設定使用無二進位複製時使用。
* stagingSplitPercentage:配置為用於轉移非同步上載的快取大小的百分比。 預設值為&#x200B;**10**。
* uploadThreads:用於非同步上載的上載線程數。 預設值為&#x200B;**10**。
* stagingPurgeInterval:從預備快取中清除已完成上載的間隔（秒）。 預設值為&#x200B;**300**&#x200B;秒（5分鐘）。
* stagingRetryInterval:失敗上載的重試間隔（秒）。 預設值為&#x200B;**600**&#x200B;秒（10分鐘）。

### 貯體區域選項{#bucket-region-options}

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
>`S3DataStore`、`CachingFileDataStore`和`AzureDataStore`的DataStore實作支援本機檔案系統快取。 `CachingFileDataStore`實施在DataStore位於NFS（網路檔案系統）上時非常有用。


從舊版快取實作（Oak 1.6之前版本）升級時，本機檔案系統快取目錄的結構有所不同。 在舊快取結構中，已下載和已上載的檔案都直接放在快取路徑下。 新結構將下載和上載分離，並將它們儲存在快取路徑下名為`upload`和`download`的兩個目錄中。 升級程式應順暢無阻，而且應排程任何擱置中的上傳，而且在初始化時，快取中任何先前下載的檔案都會放入快取中。

您也可以使用oak-run的`datastorecacheupgrade`命令離線升級快取。 有關如何執行命令的詳細資訊，請查看[readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md)中有關oak-run模組的資訊。

快取有大小限制，可使用cacheSize參數加以設定。

**下載**

在從DataStore存取請求的檔案/blob之前，將檢查本地快取中的記錄。 當快取在向快取中添加檔案時超出配置的限制（請參見`cacheSize`參數）時，將逐出某些檔案以回收空間。

**非同步上傳**

快取支援非同步上傳至DataStore。 檔案會在本機儲存（在檔案系統上），而非同步作業會開始上傳檔案。 非同步上傳的數量受測試快取大小的限制。 使用`stagingSplitPercentage`參數來設定預備快取的大小。 此參數定義用於測試快取的快取大小百分比。 此外，可下載的快取百分比會計算為&#x200B;**(100 - `stagingSplitPercentage`)*`cacheSize`**。

非同步上載是多線程的，並且線程數是使用`uploadThreads`參數配置的。

上載完成後，檔案將移到主下載快取。 當測試快取大小超過其限制時，檔案會同步上傳至DataStore，直到先前的非同步上傳完成，而且測試快取中的空間又可用。 已上載檔案由週期性作業從轉移區域中刪除，其間隔由`stagingPurgeInterval`參數配置。

失敗的上載（例如，由於網路中斷）將被置於重試隊列上並定期重試。 重試間隔是使用`stagingRetryInterval parameter`配置的。

#### 使用AmazonS3 {#configuring-binaryless-replication-with-amazon-s}配置無聯機複製

要使用S3配置無聯機複製，需要執行以下步驟：

1. 安裝作者和發佈例項，並確定它們已正確啟動。
1. 轉到複製代理設定，方法是開啟到&#x200B;*https://localhost:4502/etc/replication/agents.author/publish.html*&#x200B;的頁。
1. 按&#x200B;**Settings**&#x200B;部分中的&#x200B;**Edit**&#x200B;按鈕。
1. 將&#x200B;**Serialization**&#x200B;類型選項更改為&#x200B;**二進位小於**。

1. 在傳輸URI中添加參數&quot; `binaryless`= `true`&quot;。 變更後，URI的外觀應類似下列：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新啟動所有作者和發佈例項，讓變更生效。

#### 使用S3和MongoDB {#creating-a-cluster-using-s-and-mongodb}建立群集

1. 使用以下命令解壓縮CQ快速啟動：

   `java -jar cq-quickstart.jar -unpack`

1. 解AEM壓縮後，在安裝目錄&#x200B;*crx-quickstart*/*install*&#x200B;內建立一個資料夾。

1. 在`crx-quickstart`資料夾中建立下列兩個檔案：

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*。*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*。*config*

   建立檔案後，視需要新增設定選項。

1. 如上所述，安裝S3資料存放區所需的兩個組合。
1. 請確定已安裝MongoDB且`mongod`的實例正在運行。
1. 以下AEM命令開始：

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 對第二個實例重複步驟1到AEM4。
1. 啟動第二個AEM例項。

#### 配置共用資料儲存{#configuring-a-shared-data-store}

1. 首先，在共用資料儲存區所需的每個執行個體上建立資料儲存區設定檔案：

   * 如果您使用`FileDataStore`，請建立名為`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`的檔案，並將它放在`<aem-install>/crx-quickstart/install`資料夾中。

   * 如果使用S3作為資料儲存，請在`<aem-install>/crx-quickstart/install`資料夾中建立名為`rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`的檔案，如上所示。

1. 修改每個實例上的資料儲存配置檔案以指向同一資料儲存。 如需詳細資訊，請參閱[本文](/help/sites-deploying/data-store-config.md#data-store-configurations)。
1. 如果實例已從現有伺服器中克隆，則需要在儲存庫離線時使用最新的oak-run工具刪除新實例的`clusterId`。 您需要執行的命令是：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果配置了「段」節點儲存，則需要指定儲存庫路徑。 預設情況下，路徑為`<aem-install-folder>/crx-quickstart/repository/segmentstore.`如果配置了Document節點儲存，則可以使用[Mongo Connection String URI](https://docs.mongodb.org/manual/reference/connection-string/)。

   >[!NOTE]
   >
   >Oak-run工具可從以下位置下載：
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >請注意，必鬚根據您與安裝搭配使用的Oak版本，使用不同版本的工AEM具。 請在使用此工具之前，先檢查下列版本需求清單：
   >
   >
   >
   >    * 對於Oak版本&#x200B;**1.2.x**，請使用Oak-run **1.2.12或更新版本**
   >    * 對於比上述&#x200B;**更新的Oak版本**，請使用符合您安裝Oak核心的Oak-run版AEM本。


1. 最後，驗證配置。 為此，您需要查找每個正在共用資料儲存庫的唯一檔案。 檔案的格式為`repository-[UUID]` ，其中UUID是每個單獨儲存庫的唯一標識符。

   因此，正確的配置應具有與共用資料儲存的儲存庫相同的唯一檔案。

   檔案的儲存方式不同，視資料儲存區而定：

   * 對於`FileDataStore`，檔案是在資料儲存資料夾的根路徑下建立的。
   * 對於`S3DataStore`，在`META`資料夾下配置的S3儲存桶中建立檔案。

## Azure 資料存放區 {#azure-data-store}

可AEM以配置為在Microsoft的Azure儲存服務中儲存資料。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID進行配置。

為啟用Azure資料儲存功能，必須下載並安裝包含Azure連接器的功能套件。 前往[Adobe資料庫](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/)，從1.6.x版的功能套件下載最新版本（例如com.adobe.granite.oak.azureblobconnector-1.6.3.zip）。

>[!NOTE]
>
>與TarMK搭AEM配使用時，預設會將二進位檔儲存在FileDataStore中。 若要搭配Azure DataStore使用TarMK，您必須AEM開始使用`crx3tar-nofds`執行模式，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可依下列方式安裝及設定Azure連接器：

1. 將功能套件zip檔案的內容解壓縮至暫存資料夾。

1. 轉到臨時資料夾，將`jcr_root/libs/system/install`的內容複製到`<aem-install>crx-quickstart/install`資料夾。
1. 如果AEM已配置為使用Tar或MongoDB儲存，請在繼續操作之前，從`/crx-quickstart/install`資料夾中刪除任何現有配置檔案。 需要移除的檔案包括：

   ForMongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   針對TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回已提取特徵包的臨時位置，並將`jcr_root/libs/system/config`的內容複製到`<aem-install>/crx-quickstart/install`資料夾。
1. 編輯配置檔案並添加設定所需的配置選項。
1. 開始AEM。

您可以使用配置檔案和以下選項：

* azureSas=&quot;&quot;:在1.6.3版的連接器中，新增了Azure共用存取簽名(SAS)支援。 **如果配置檔案中同時存在SAS和儲存憑據，則SAS具有優先順序。** 有關SAS的更多資訊，請參 [閱官方文檔](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1)。請確定&#39;=&#39;字元已逸出為&#39;\=&#39;。

* azureBlobEndpoint=&quot;&quot;:Azure Blob端點。 例如，https://&lt;storage-account>.blob.core.windows.net。
* accessKey=&quot;&quot;:儲存帳戶名稱。 有關Microsoft Azure驗證憑證的詳細資訊，請參閱[官方檔案](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account)。

* secretKey=&quot;&quot;:儲存訪問密鑰。 請確定&#39;=&#39;字元已逸出為&#39;\=&#39;。
* container=&quot;&quot;:Microsoft Azure Blob儲存容器名稱。 容器是一組膨脹體的群組。 如需詳細資訊，請閱讀[官方檔案](https://msdn.microsoft.com/en-us/library/dd135715.aspx)。
* maxConnections=&quot;&quot;:每個操作同時發出請求的併發數。 預設值為 1。
* maxErrorRetry=&quot;&quot;:每個請求的重試次數。 預設值為 3。
* socketTimeout=&quot;&quot;:請求使用的逾時間隔（以毫秒為單位）。 預設值為5分鐘。

除了上述設定外，您也可以設定下列設定：

* 路徑：資料儲存的路徑。 預設值為`<aem-install>/repository/datastore.`
* RecordLength:應儲存在資料儲存中的對象的最小大小。 預設值為16KB。
* maxCachedBinarySize:大小小於或等於此大小的二進位檔案將儲存在記憶體快取中。 大小（以位元組為單位）。 預設值為17408(17 KB)。
* cacheSize:快取的大小。 該值以位元組為單位指定。 預設為64GB。
* 機密：僅在對共用資料儲存設定使用無二進位複製時使用。
* stagingSplitPercentage:配置為用於轉移非同步上載的快取大小的百分比。 預設值為 10。
* uploadThreads:用於非同步上載的上載線程數。 預設值為 10。
* stagingPurgeInterval:從預備快取中清除已完成上載的間隔（秒）。 預設值為300秒（5分鐘）。
* stagingRetryInterval:失敗上載的重試間隔（秒）。 預設值為600秒（10分鐘）。

>[!NOTE]
>
>所有設定都應放在引號之間，例如：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## 資料儲存廢棄項目收集{#data-store-garbage-collection}

資料儲存廢棄項目收集過程用於移除資料儲存中任何未使用的檔案，從而釋放過程中的寶貴磁碟空間。

您可以透過下列方式執行資料存放區廢棄項目收集：

1. 轉到位於&#x200B;*https://&lt;serveraddress:port>/system/console/jmx*&#x200B;的JMX控制台
1. 正在搜索&#x200B;**RepositoryManagement。** 在找到儲存庫管理器MBean後，按一下它可開啟可用選項。
1. 捲動至頁面結尾，然後按一下&#x200B;**startDataStoreGC(boolean markOnly)**&#x200B;連結。
1. 在以下對話框中，為`markOnly`參數輸入`false`，然後按一下&#x200B;**叫用**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >`markOnly`參數表示垃圾收集的掃描階段是否將運行。

## 共用資料儲存{#data-store-garbage-collection-for-a-shared-data-store}的資料儲存廢棄項目收集

>[!NOTE]
>
>在叢集或共用資料存放區設定（使用Mongo或區段Tar）中執行廢棄項目收集時，記錄檔可能會顯示有關無法刪除特定點滴ID的警告。 這是因為在先前廢棄項目收集中刪除的blob ID被其他沒有ID刪除資訊的群集或共用節點重新錯誤引用。 因此，在執行廢棄項目收集時，當嘗試刪除上次執行中已刪除的ID時，它會記錄警告。 此行為不會影響效能或功能。

在較新版本的AEM資料庫中，也可以在多個儲存庫共用的資料儲存上運行資料儲存廢棄項目收集。 若要在共用資料存放區上執行資料存放區廢棄項目收集，請執行下列步驟：

1. 請確保為資料儲存廢棄項目收集配置的任何維護任務在共用資料儲存的所有儲存庫實例上都被禁用。
1. 在共用資料儲存的&#x200B;**所有**&#x200B;儲存庫實例上分別運行[二進位廢棄項收集](/help/sites-deploying/data-store-config.md#data-store-garbage-collection)中提及的步驟。 但是，請務必在按一下「調用」按鈕之前為`markOnly`參數輸入`true`:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有實例上完成上述過程後，從實例的&#x200B;**any**&#x200B;再次運行資料儲存廢棄項目收集：

   1. 轉到JMX控制台並選擇Repository Manager Mbean。
   1. 按一下&#x200B;**按一下startDataStoreGC(boolean markOnly)**&#x200B;連結。
   1. 在以下對話框中，再次為`markOnly`參數輸入`false`。

   這會整理使用之前使用的標籤階段找到的所有檔案，並刪除資料儲存區中未使用的其餘檔案。

