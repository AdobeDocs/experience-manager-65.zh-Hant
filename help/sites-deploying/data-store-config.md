---
title: 在AEM 6中配置節點儲存區和資料儲存區
description: 了解如何配置節點儲存區和資料儲存區，以及如何執行資料儲存區垃圾收集。
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: 461424de9158e14e251037004ea3590ed35bb4a0
workflow-type: tm+mt
source-wordcount: '3584'
ht-degree: 2%

---

# 在AEM 6中配置節點儲存區和資料儲存區{#configuring-node-stores-and-data-stores-in-aem}

## 簡介 {#introduction}

在Adobe Experience Manager(AEM)中，二進位資料可與內容節點分開儲存。 二進位資料儲存在資料儲存器中，而內容節點儲存在節點儲存器中。

可以使用OSGi配置配置資料儲存和節點儲存。 每個OSGi設定都使用永久識別碼(PID)來參照。

## 配置步驟 {#configuration-steps}

要配置節點儲存和資料儲存，請執行以下步驟：

1. 將AEM Quickstart JAR檔案複製到其安裝目錄。
1. 建立資料夾 `crx-quickstart/install` （在安裝目錄中）。
1. 首先，請建立配置檔案，使用您要在 `crx-quickstart/install` 目錄。

   例如，Document節點存放區(是AEM MongoMK實作的基礎)會使用檔案 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. 編輯檔案，並設定您的設定選項。
1. 使用您要使用的資料存放區的PID建立設定檔案。 編輯檔案以設定配置選項。

   >[!NOTE]
   >
   >請參閱 [節點儲存配置](#node-store-configurations) 和 [資料儲存配置](#data-store-configurations) ，以了解設定選項。

1. 啟動AEM。

## 節點儲存配置 {#node-store-configurations}

>[!CAUTION]
>
>較新版本的Oak對OSGi組態檔採用新的命名配置和格式。 新的命名配置要求將配置檔案命名為 **.config** 而新格式需要輸入值，且為 [這裡](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>如果您從舊版Oak升級，請務必備份 `crx-quickstart/install`中。 升級後，將資料夾的內容還原到升級的安裝，並修改配置檔案的擴展 **.cfg** to **.config**.
>
>若您正在閱讀本文章，以準備從 **AEM 5.x** 安裝時，請務必諮詢 [升級](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) 檔案。

### 區段節點存放區 {#segment-node-store}

區段節點存放區是Adobe在AEM6中實作TarMK的基礎。 它會使用 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID用於配置。

>[!CAUTION]
>
>「區段」節點儲存區的PID已從 `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` AEM 6到 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` 在AEM 6.3中。請務必進行必要的設定調整，以反映此變更。

您可以設定下列選項：

* `repository.home`:儲存與儲存庫相關資料的儲存庫首頁路徑。 依預設，區段檔案會儲存在 `crx-quickstart/segmentstore` 目錄。

* `tarmk.size`:段的最大大小(MB)。 預設最大值為256MB。
* `customBlobStore`:指示已使用自訂資料存放區的布林值。 AEM 6.3及更新版本的預設值為true。 AEM 6.3之前的預設值為false。

以下是範例 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 檔案：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 文檔節點儲存 {#document-node-store}

檔案節點存放區是AEM MongoMK實作的基礎。 它會使用 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 可使用下列設定選項：

* `mongouri`:此 [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) 連接到Mongo資料庫所需。 預設為 `mongodb://localhost:27017`

* `db`:Mongo資料庫的名稱。 預設為 **Oak** ``. However, new AEM 6 installations use **aem-author** ``作為預設資料庫名稱。

* `cache`:快取大小(MB)。 這分佈在DocumentNodeStore中使用的各種快取中。 預設為 `256`

* `changesSize`:用於快取差異輸出的Mongo中封閉集合的大小(MB)。 預設為 `256`

* `customBlobStore`:指示將使用自訂資料存放區的布林值。 預設為 `false`。

以下是範例 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` 檔案：

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
>若要啟用自訂資料存放區，您必須確定 `customBlobStore` 設為 `true` 在相應的節點儲存配置檔案([區段節點存放區](/help/sites-deploying/data-store-config.md#segment-node-store) 或 [文檔節點儲存](/help/sites-deploying/data-store-config.md#document-node-store))。

### 檔案資料存放區 {#file-data-store}

這是 [FileDataStore](https://jackrabbit.apache.org/api/trunk/org/apache/jackrabbit/core/data/FileDataStore.html) 在傑克拉布2號。 它提供了將二進位資料作為普通檔案儲存在檔案系統上的方法。 它會使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID。

可使用下列設定選項：

* `repository.home`:儲存各種儲存庫相關資料的儲存庫首頁路徑。 依預設，二進位檔案會儲存在 `crx-quickstart/repository/datastore` 目錄

* `path`:儲存檔案的目錄路徑。 如果指定，則優先於 `repository.home` value

* `minRecordLength`:資料儲存中儲存的檔案的最小大小（以位元組為單位）。 小於此值的二進位內容會內嵌。

>[!NOTE]
>
>使用NAS儲存共用檔案資料儲存時，請確保僅使用高效能設備，以避免效能問題。

## Amazon S3 Data Store {#amazon-s-data-store}

AEM可設定為將資料儲存在Amazon的簡單儲存服務(S3)中。 它會使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID用於配置。

若要啟用S3資料存放區功能，必須下載並安裝包含S3資料存放區連接器的功能套件。 前往 [Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) 並從功能套件1.10.x版下載最新版本(例如com.adobe.granite.oak.s3connector-1.10.0.zip)。 此外，您也需要下載及安裝列於 [AEM 6.5發行說明](/help/release-notes/release-notes.md) 頁面。

>[!NOTE]
>
>將AEM與TarMK搭配使用時，二進位檔預設會儲存在 `FileDataStore`. 若要將TarMK與S3資料存放區搭配使用，您必須使用 `crx3tar-nofds` 例如runmode:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以依照下列方式安裝及設定S3 Connector:

1. 將Feature Pack zip檔案的內容解壓縮至臨時資料夾。

1. 前往臨時資料夾，並導覽至下列位置：

   ```xml
   jcr_root/libs/system/install
   ```

   將上述位置的所有內容複製至 `<aem-install>/crx-quickstart/install.`

1. 如果AEM已配置為與Tar或MongoDB儲存一起使用，請從***中刪除任何現有配置檔案&lt;aem-install>***/*crx-quickstart*/*安裝* 資料夾。 需要移除的檔案包括：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回已提取Feature Pack的臨時位置，並複製以下資料夾的內容：

   * `jcr_root/libs/system/config`

   至

   * `<aem-install>/crx-quickstart/install`

   請確保僅複製當前配置所需的配置檔案。 對於專用資料儲存和共用資料儲存設定，都會複製 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 檔案。

   >[!NOTE]
   >
   >在群集設定中，逐個在群集的所有節點上執行上述步驟。 此外，請務必對所有節點使用相同的S3設定。

1. 編輯檔案並新增設定所需的設定選項。
1. 啟動AEM。

## 升級至1.10.x S3連接器的新版本 {#upgrading-to-a-new-version-of-the-s-connector}

如果您需要升級至新版本的1.10.x S3連接器(例如，從1.10.0升級至1.10.4)，請遵循下列步驟：

1. 停止AEM例項。

1. 導覽至 `<aem-install>/crx-quickstart/install/15` 在AEM安裝資料夾中，並備份其內容。
1. 備份後，請刪除中的所有jar檔案，以刪除舊版S3 Connector及其相依性 `<aem-install>/crx-quickstart/install/15` 資料夾，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述檔案名稱僅供圖說之用。

1. 從下載1.10.x功能套件的最新版本，請前往 [Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. 將內容解壓縮至個別資料夾，然後導覽至 `jcr_root/libs/system/install/15`.
1. 將jar檔案複製到 **&lt;aem-install>**/crx-quickstart/install/15(在AEM安裝資料夾中)。
1. 啟動AEM並檢查連接器功能。

您可以使用設定檔案及下列詳細說明的選項。

<!--
* accessKey: The AWS access key.
* secretKey: The AWS secret access key. **Note:** When the `accessKey` or `secretKey` is not specified then the [IAM role](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) is used for authentication.
* s3Bucket: The bucket name.
* s3Region: The bucket region.
* path: The path of the data store. The default is **&lt;AEM install folder&gt;/repository/datastore**
* minRecordLength: The minimum size of an object that should be stored in the data store. The minimum/default is **16KB.**
* maxCachedBinarySize: Binaries with size less than or equal to this size will be stored in memory cache. The size is in bytes. The default is **17408 **(17 KB).
* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret: Only to be used if using binaryless replication for shared datastore setup.
* stagingSplitPercentage: The percentage of cache size configured to be used for staging asynchronous uploads. The default value is **10**.
* uploadThreads: The number of uploads threads that are used for asynchronous uploads. The default value is **10**.
* stagingPurgeInterval: The interval in seconds for purging finished uploads from the staging cache. The default value is **300** seconds (5 minutes).
* stagingRetryInterval: The retry interval in seconds for failed uploads. The default value is **600** seconds (10 minutes).
-->

### S3連接器組態檔選項 {#s3-connector-configuration-file-options}

>[!NOTE]
>
>S3連接器支援IAM用戶身份驗證和IAM角色身份驗證。 要使用IAM角色身份驗證，請忽略 `accessKey` 和 `secretKey` 值。 S3連接器將預設為 [IAM角色](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) 指派給例項。

| 金鑰 | 說明 | 預設 | 必要 |
| --- | --- | --- | --- |
| accessKey | 具有儲存桶訪問權限的IAM用戶的Access Key ID。 |  | 是，當不使用IAM角色時。 |
| secretKey | 具有儲存桶訪問權限的IAM用戶的秘密訪問密鑰。 |  | 是，當不使用IAM角色時。 |
| cacheSize | 本地快取的大小（以位元組為單位）。 | 64GB | 否. |
| connectionTimeout | 設定在最初建立連接時超時之前等待的時間（以毫秒為單位）。 | 10000 | 否. |
| maxCachedBinarySize | 大小小於或等於此值的二進位檔（以位元組為單位）將儲存在記憶體快取中。 | 17408(17 KB) | 否. |
| maxConnections | 設定允許的開啟HTTP連線數量上限。 | 50 | 否. |
| maxErrorRetry | 設定失敗（可檢索）請求的最大重試次數。 | 3 | 否. |
| minRecordLength | 應儲存在資料儲存區中的對象的最小大小（以位元組為單位）。 | 16384 | 否. |
| 路徑 | AEM資料存放區的本機路徑。 | `crx-quickstart/repository/datastore` | 否. |
| proxyHost | 設定客戶端將通過的可選代理主機。 |  | 否. |
| proxyPort | 設定客戶端將通過的可選代理埠。 |  | 否. |
| s3Bucket | S3儲存貯體的名稱。 |  | 是 |
| s3EndPoint | S3 REST API端點。 |  | 否. |
| s3Region | 貯體所在的地區。 看這個 [頁面](https://docs.aws.amazon.com/general/latest/gr/s3.html) 以取得更多詳細資訊。 | 執行AWS例項的地區。 | 否. |
| socketTimeout | 設定在連接超時和關閉之前，通過已建立的開啟連接傳輸資料的等待時間（以毫秒為單位）。 | 50000 | 否. |
| stagingPurgeInterval | 從預備快取清除已完成上傳的間隔（秒）。 | 300 | 否. |
| stagingRetryInterval | 重試上傳失敗的間隔（秒）。 | 600 | 否. |
| stagingSplitPercentage | 百分比 `cacheSize` 用於測試非同步上傳。 | 10 | 否. |
| uploadThreads | 用於非同步上載的上載線程數。 | 10 | 否. |
| writeThreads | 用於通過S3傳輸管理器寫入的併發線程數。 | 10 | 否. |

<!---
### Bucket region options {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>US West</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (Northern California)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU (Ireland)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>South America (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>
-->

### DataStore快取 {#data-store-caching}

>[!NOTE]
>
>DataStore實施 `S3DataStore`, `CachingFileDataStore` 和 `AzureDataStore` 支援本機檔案系統快取。 此 `CachingFileDataStore` 當DataStore位於NFS（網路檔案系統）時，實施很有用。

從舊版快取實作（Oak 1.6之前）升級時，本機檔案系統快取目錄的結構會有所差異。 在舊快取結構中，下載的檔案和上傳的檔案都直接放在快取路徑下。 新結構會隔離下載和上傳，並將它們儲存在名為 `upload` 和 `download` 在快取路徑下。 升級程式應順暢無礙，且任何待上傳內容都應排程上傳，且任何先前下載的檔案都會在初始化時放入快取中。

您也可以使用 `datastorecacheupgrade` oak-run命令。 有關如何執行命令的詳細資訊，請檢查 [讀我檔案](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) 用於oak-run模組。

快取有大小限制，可使用cacheSize參數進行配置。

#### 下載 {#downloads}

在從DataStore訪問請求的檔案/blob之前，將檢查本地快取中的記錄。 當快取超過設定的限制時(請參閱 `cacheSize` 參數)，而將檔案新增至快取中，則會逐出部分檔案以回收空間。

#### 非同步上傳 {#async-upload}

快取支援非同步上傳至DataStore。 檔案會存放在本機、快取中（在檔案系統上），且非同步工作會開始上傳檔案。 非同步上傳的數量受中繼快取的大小限制。 預備快取的大小是使用 `stagingSplitPercentage` 參數。 此參數定義用於暫存快取的快取大小百分比。 此外，下載可用的快取百分比計算為 **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

非同步上傳是多執行緒，且執行緒數目是使用 `uploadThreads` 參數。

上傳完成後，檔案會移至主下載快取。 當中繼快取大小超過其限制時，檔案會同步上傳至DataStore，直到先前的非同步上傳完成，且中繼快取中的空間可再次使用為止。 上傳的檔案會由定期作業從測試區域中移除，而期間由 `stagingPurgeInterval` 參數。

失敗的上載（例如，由於網路中斷）將放在重試隊列上並定期重試。 重試間隔的設定方式為： `stagingRetryInterval parameter`.

#### 使用Amazon S3設定無二進位檔復寫 {#configuring-binaryless-replication-with-amazon-s}

若要使用S3設定無二進位檔復寫，需執行下列步驟：

1. 安裝製作和發佈例項，並確定它們已正確啟動。
1. 開啟一個頁面以前往 *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. 按下 **編輯** 按鈕 **設定** 區段。
1. 變更 **序列化** 鍵入選項 **二進位減**.

1. 新增參數「 `binaryless`= `true`&quot;在傳輸uri中。 變更後，uri看起來應類似下列：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新啟動所有製作和發佈執行個體，讓變更生效。

#### 使用S3和MongoDB建立叢集 {#creating-a-cluster-using-s-and-mongodb}

1. 使用下列命令解壓縮CQ快速入門：

   `java -jar cq-quickstart.jar -unpack`

1. 解壓縮AEM後，在安裝目錄內建立資料夾 *crx-quickstart*/*安裝*.

1. 在內建立這兩個檔案 `crx-quickstart` 資料夾：

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   建立檔案後，視需要新增設定選項。

1. 依照上述說明安裝S3資料存放區所需的兩個套件組合。
1. 確認已安裝MongoDB，且執行個體為 `mongod` 執行中。
1. 使用下列命令啟動AEM :

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 對第二個AEM例項重複步驟1到4。
1. 啟動第二個AEM例項。

#### 配置共用資料儲存 {#configuring-a-shared-data-store}

1. 首先，在共用資料儲存所需的每個執行個體上建立資料儲存設定檔案：

   * 如果您使用 `FileDataStore`，建立名為的檔案 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 並放入 `<aem-install>/crx-quickstart/install` 檔案夾。

   * 如果使用S3做為資料存放區，請建立名為的檔案 `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 在 `<aem-install>/crx-quickstart/install` 資料夾。

1. 修改每個執行個體上的資料存放區組態檔，以指向相同的資料存放區。 如需詳細資訊，請參閱 [這篇文章](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. 如果執行個體已從現有伺服器複製，您需要移除 `clusterId` 執行工具，在存放庫離線時使用最新的oak-run工具。 您需要執行的命令為：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果已設定區段節點存放區，則需指定存放庫路徑。 依預設，路徑為 `<aem-install-folder>/crx-quickstart/repository/segmentstore.` 如果配置了文檔節點儲存，則可以使用 [Mongo連接字串URI](https://docs.mongodb.org/manual/reference/connection-string/).

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
   >    * 適用於Oak版本 **1.2.x** 使用Oak-run **1.2.12或更新版本**
   >    * 適用於Oak版本 **較上文更新**，請使用符合AEM安裝之Oak核心的Oak-run版本。


1. 最後，驗證設定。 若要這麼做，您需要尋找共用資料儲存庫的每個存放庫所新增的唯一檔案。 檔案的格式為 `repository-[UUID]`，其中UUID是每個個別存放庫的唯一識別碼。

   因此，正確的配置應具有與共用資料儲存的儲存庫相同的唯一檔案。

   檔案的儲存方式會有所不同，具體取決於資料儲存：

   * 若 `FileDataStore` 檔案會建立在資料儲存資料夾的根路徑下。
   * 若 `S3DataStore` 檔案會建立在已設定的S3貯體中，位於 `META` 檔案夾。

## Azure 資料存放區 {#azure-data-store}

AEM可設定為將資料儲存在Microsoft的Azure儲存服務中。 它會使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID用於配置。

若要啟用Azure資料儲存功能，必須下載並安裝包含Azure連接器的功能套件。 前往 [Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) 並從功能套件1.6.x版下載最新版本（例如com.adobe.granite.oak.azurebconnector-1.6.3.zip）。

>[!NOTE]
>
>將AEM與TarMK搭配使用時，二進位檔預設會儲存在FileDataStore中。 若要將TarMK與Azure DataStore搭配使用，您必須使用 `crx3tar-nofds` 例如runmode:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以依照下列方式安裝及設定Azure連接器：

1. 將Feature Pack zip檔案的內容解壓縮至臨時資料夾。

1. 轉到臨時資料夾，並複製 `jcr_root/libs/system/install` 到 `<aem-install>crx-quickstart/install` 檔案夾。
1. 如果AEM已設定為可搭配Tar或MongoDB儲存使用，請從 `/crx-quickstart/install` 資料夾。 需要移除的檔案包括：

   MongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   若為TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回已提取Feature Pack的臨時位置，並複製 `jcr_root/libs/system/config` 到 `<aem-install>/crx-quickstart/install` 檔案夾。
1. 編輯設定檔案並新增設定所需的設定選項。
1. 啟動AEM。

您可搭配下列選項使用設定檔案：

* azureSas=&quot;&quot;:在連接器1.6.3版中，新增了Azure共用存取簽名(SAS)支援。 **如果配置檔案中同時存在SAS和儲存憑據，則SAS具有優先順序。** 有關SAS的詳細資訊，請參閱 [官方檔案](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1). 請確定「=」字元會以「\=」的形式逸出。

* azureBlobEndpoint=&quot;&quot;:Azure Blob端點。 例如， https://&lt;storage-account>.blob.core.windows.net。
* accessKey=&quot;&quot;:儲存帳戶名稱。 如需Microsoft Azure驗證憑證的詳細資訊，請參閱 [官方檔案](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;:儲存存取金鑰。 請確定「=」字元會以「\=」的形式逸出。
* container=&quot;&quot;:Microsoft Azure blob儲存容器名稱。 容器是一組blob的分組。 如需其他詳細資訊，請閱讀 [官方檔案](https://msdn.microsoft.com/en-us/library/dd135715.aspx).
* maxConnections=&quot;&quot;:每個操作同時發出的請求數。 預設值為 1。
* maxErrorRetry=&quot;&quot;:每個請求的重試次數。 預設值為 3。
* socketTimeout=&quot;&quot;:用於請求的逾時間隔（以毫秒為單位）。 預設值為5分鐘。

除了上述設定外，您也可以設定下列設定：

* 路徑：資料儲存的路徑。 預設為 `<aem-install>/repository/datastore.`
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

1. 前往位於 *https://&lt;serveraddress:port>/system/console/jmx*
1. 搜尋 **儲存庫管理。** 找到儲存庫管理器MBean後，按一下該MBean以開啟可用選項。
1. 捲動至頁面結尾，然後按一下 **startDataStoreGC(boolean markOnly)** 連結。
1. 在下列對話方塊中，輸入 `false` 針對 `markOnly` 參數，然後按一下 **叫用**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >此 `markOnly` paramater表示垃圾收集的掃描階段是否將運行。

## 共用資料儲存的資料儲存垃圾收集 {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>在叢集或共用資料存放區設定（含Mongo或Segment Tar）中執行垃圾收集時，記錄檔可能會顯示無法刪除某些Blob ID的警告。 這是因為以前垃圾收集中刪除的blob ID被沒有ID刪除資訊的其他群集或共用節點重新錯誤引用。 因此，執行垃圾收集時，會在嘗試刪除上次執行中已刪除的ID時記錄警告。 此行為不會影響效能或功能。

>[!NOTE]
>
>如果您使用共用資料儲存設定且資料儲存垃圾收集已停用，則運行Lucene Binary清除任務可能會突然增加使用的磁碟空間。 若要避免此情況，您必須依下列方式在所有製作和發佈執行個體上停用BlobTracker:
>
>1. 停止AEM例項。
>2. 新增 `blobTrackSnapshotIntervalInSecs=L"0"` 參數 `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 檔案。 此參數需有Oak 1.12.0、1.10.2或更新版本。
>3. 重新啟動AEM例項。


使用較新的AEM版本時，資料存放區垃圾收集也可在多個存放庫共用的資料存放區上執行。 為了能夠在共用資料儲存上運行資料儲存垃圾收集，請執行以下步驟：

1. 請確保在共用資料儲存的所有儲存庫實例上禁用為資料儲存垃圾收集配置的任何維護任務。
1. 執行 [二進位垃圾收集](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) 逐個 **all** 共用資料存放區的存放庫例項。 不過，請務必輸入 `true` 針對 `markOnly` 參數，再按一下叫用按鈕：

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有執行個體上完成上述程式後，請再次從執行資料儲存垃圾收集 **any** 例項：

   1. 轉到JMX控制台，並選擇儲存庫管理器Mbean。
   1. 按一下 **按一下startDataStoreGC（布林值markOnly）** 連結。
   1. 在下列對話方塊中，輸入 `false` 針對 `markOnly` 參數。
   這會整理使用之前使用的標籤階段找到的所有檔案，並刪除資料存放區中未使用的其餘檔案。
