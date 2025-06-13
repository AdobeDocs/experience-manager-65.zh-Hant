---
title: 在AEM 6中設定節點存放區和資料存放區
description: 瞭解如何設定節點存放區和資料存放區，以及如何執行資料存放區記憶體回收。
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '3461'
ht-degree: 1%

---

# 在AEM 6中設定節點存放區和資料存放區{#configuring-node-stores-and-data-stores-in-aem}

## 簡介 {#introduction}

在Adobe Experience Manager (AEM)中，二進位資料可與內容節點分開儲存。 二進位資料儲存在資料存放區中，而內容節點儲存在節點存放區中。

資料存放區和節點存放區都可以使用OSGi設定來設定。 每個OSGi設定都是使用持續性識別碼(PID)來參考。

## 設定步驟 {#configuration-steps}

若要同時設定節點存放區和資料存放區，請執行下列步驟：

1. 將AEM quickstart JAR檔案複製到其安裝目錄。
1. 在安裝目錄中建立資料夾`crx-quickstart/install`。
1. 首先，建立組態檔，使用您要在`crx-quickstart/install`目錄中使用的節點存放區選項名稱來設定節點存放區。

   例如，Document節點存放區(AEM的MongoMK實作基礎)使用檔案`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`。

1. 編輯檔案，並設定組態選項。
1. 以您要使用之資料存放區的PID建立設定檔。 編輯檔案以設定組態選項。

   >[!NOTE]
   >
   >如需組態選項，請參閱[節點存放區組態](#node-store-configurations)和[資料存放區組態](#data-store-configurations)。

1. 啟動AEM。

## 節點存放區設定 {#node-store-configurations}

>[!CAUTION]
>
>較新版本的Oak採用新的命名方案和格式用於OSGi設定檔案。 新的命名配置需要名稱為&#x200B;**.config**&#x200B;的組態檔，而新格式需要輸入值。 如需詳細資訊，請參閱[Apache Sling布建模型和Apache SlingStart — 預設設定格式](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)。
>
>如果您從舊版Oak升級，請務必先備份`crx-quickstart/install`資料夾。 升級之後，將資料夾的內容還原至升級後的安裝，並將組態檔的副檔名從&#x200B;**.cfg**&#x200B;修改為&#x200B;**.config**。

### 區段節點存放區 {#segment-node-store}

區段節點存放區是Adobe在AEM6中實施TarMK的基礎。 它使用`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID進行設定。

>[!CAUTION]
>
>區段節點存放區的PID已從AEM 6的`org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions`變更為AEM 6.3中的`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService`。請務必進行必要的設定調整以反映此變更。

您可以設定下列選項：

* `repository.home`：儲儲存儲存存庫相關資料的儲存庫本位目錄路徑。 依預設，區段檔案儲存在`crx-quickstart/segmentstore`目錄下。

* `tarmk.size`：區段的大小上限（以MB為單位）。 預設最大為256MB。
* `customBlobStore`：表示使用自訂資料存放區的布林值。 AEM 6.3及更高版本的預設值為true。 AEM 6.3之前的版本預設為false。

以下是範例`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`檔案：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 檔案節點存放區 {#document-node-store}

檔案節點存放區是AEM實施MongoMK的基礎。 它使用`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 下列組態選項可供使用：

* `mongouri`：連線至Mongo資料庫所需的[MongoURI](https://docs.mongodb.org/manual/reference/connection-string/)。 預設值為`mongodb://localhost:27017`

* `db`： Mongo資料庫的名稱。 預設為&#x200B;**Oak** ``. However, new AEM 6 installations use **aem-author** ``作為預設資料庫名稱。

* `cache`：快取大小（以MB為單位）。 這會分散在DocumentNodeStore中使用的各種快取之間。 預設值為`256`

* `changesSize`： Mongo中用於快取diff輸出的限定集合大小（以MB為單位）。 預設值為`256`

* `customBlobStore`：表示使用自訂資料存放區的布林值。 預設為 `false`。

以下是範例`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`檔案：

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## 資料存放區設定 {#data-store-configurations}

在處理大量二進位檔時，建議您使用外部資料存放區，而非預設節點存放區，以發揮最大效能。

例如，如果您的專案需要許多媒體資產，將它們儲存在File或S3 Data Store底下，比直接將它們儲存在MongoDB中更快獲得存取許可權。

檔案資料存放區提供比MongoDB更好的效能，而且大量資產的Mongo備份和還原作業也較慢。

不同資料存放區和設定的詳細資訊如下所述。

>[!NOTE]
>
>若要啟用自訂資料存放區，您必須確定在個別節點存放區組態檔（[區段節點存放區](/help/sites-deploying/data-store-config.md#segment-node-store)或[檔案節點存放區](/help/sites-deploying/data-store-config.md#document-node-store)）中，`customBlobStore`已設為`true`。

### 檔案資料存放區 {#file-data-store}

這是Jackrabbit 2中的[FileDataStore](https://jackrabbit.apache.org/api/trunk/org/apache/jackrabbit/core/data/FileDataStore.html)實作。 它提供一種將二進位資料儲存為檔案系統上一般檔案的方法。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID。

這些組態選項可供使用：

* `repository.home`：儲存各種存放庫相關資料的存放庫首頁路徑。 依照預設，二進位檔案會儲存在`crx-quickstart/repository/datastore`目錄下

* `path`：要儲存檔案的目錄路徑。 若指定，則優先於`repository.home`值

* `minRecordLength`：儲存在資料存放區的檔案大小下限（位元組）。 系統會內嵌小於此值的二進位內容。

>[!NOTE]
>
>使用NAS來儲存共用檔案資料存放區時，請務必只使用高效能裝置以避免效能問題。

## Amazon S3資料存放區 {#amazon-s-data-store}

AEM可設定為將資料儲存在Amazon的Simple Storage Service (S3)。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID進行設定。

>[!NOTE]
>
>AEM 6.5支援在Amazon的S3中儲存資料，但並未延伸至在其他平台中儲存資料，因為這些平台的廠商可能有自己的Amazon S3 API實作。

若要啟用S3資料存放區功能，必須下載及安裝包含S3資料存放區聯結器的Feature Pack。 前往[Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)並從Feature Pack 1.10.x版（例如com.adobe.granite.oak.s3connector-1.10.0.zip）下載最新版本。 此外，您必須下載並安裝[AEM 6.5發行說明](/help/release-notes/release-notes.md)頁面上列出的最新AEM Service Pack。

>[!NOTE]
>
>搭配TarMK使用AEM時，二進位檔預設會儲存在`FileDataStore`中。 若要搭配S3資料存放區使用TarMK，您必須使用`crx3tar-nofds`執行模式啟動AEM，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以依照以下步驟安裝和設定S3 Connector：

1. 將Feature Pack zip檔案的內容解壓縮至暫存資料夾。

1. 移至暫存資料夾，並導覽至下列位置：

   ```xml
   jcr_root/libs/system/install
   ```

   將以上位置的所有內容複製到`<aem-install>/crx-quickstart/install.`

1. 如果AEM已設定為搭配Tar或MongoDB儲存體使用，請先從***&lt;aem-install>***/*crx-quickstart*/*install*&#x200B;資料夾移除任何現有的設定檔，然後再繼續。 必須移除的檔案包括：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 回到已擷取功能套件的暫存位置，並複製下列資料夾的內容：

   * `jcr_root/libs/system/config`

   至

   * `<aem-install>/crx-quickstart/install`

   請確定您僅複製目前組態所需的組態檔。 對於專用資料存放區和共用資料存放區設定，請複製`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`檔案。

   >[!NOTE]
   >
   >在叢集設定中，請逐一在叢集的所有節點上執行上述步驟。 此外，請務必對所有節點使用相同的S3設定。

1. 編輯檔案並新增安裝程式所需的設定選項。
1. 啟動AEM。

## 升級至新版1.10.x S3 Connector {#upgrading-to-a-new-version-of-the-s-connector}

若要升級為1.10.x S3聯結器的新版本（例如從1.10.0到1.10.4），請遵循下列步驟：

1. 停止AEM執行個體。

1. 導覽至AEM安裝資料夾中的`<aem-install>/crx-quickstart/install/15`，並備份其內容。
1. 備份之後，刪除S3 Connector的舊版本及其相依性，方法是刪除`<aem-install>/crx-quickstart/install/15`資料夾中的所有jar檔案，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述檔案名稱僅供說明之用。

1. 從[Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)下載最新版的1.10.x Feature Pack。
1. 將內容解壓縮至個別資料夾，然後導覽至`jcr_root/libs/system/install/15`。
1. 將jar檔案複製到AEM安裝資料夾中的&#x200B;**&lt;aem-install>**/crx-quickstart/install/15。
1. 啟動AEM並檢查聯結器功能。

您可以使用包含下列詳細選項的組態檔。

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

### S3 Connector組態檔選項 {#s3-connector-configuration-file-options}

>[!NOTE]
>
>S3聯結器同時支援IAM使用者驗證和IAM角色驗證。 若要使用IAM角色驗證，請忽略組態檔中的`accessKey`和`secretKey`值。 然後，S3聯結器會預設為指派給執行個體的[IAM角色](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html)。

| 索引鍵 | 說明 | 預設 | 必要 |
| --- | --- | --- | --- |
| accessKey | 可存取貯體之IAM使用者的存取金鑰ID。 | | 是，當不使用IAM角色時。 |
| secretKey | 可存取貯體的IAM使用者機密存取金鑰。 | | 是，當不使用IAM角色時。 |
| cacheSize | 本機快取的大小（位元組）。 | 64GB | 不適用。 |
| connectionTimeout | 設定初始建立連線時逾時前的等待時間（毫秒）。 | 10000 | 不適用。 |
| maxCachedBinarySize | 大小小於或等於此值（位元組）的二進位檔儲存在記憶體快取中。 | 17408 (17 KB) | 不適用。 |
| maxConnections | 設定允許的開啟HTTP連線數目上限。 | 50 | 不適用。 |
| maxErrorRetry | 設定失敗（可重試）要求的重試次數上限。 | 3 | 不適用。 |
| minRecordLength | 應儲存在資料存放區中的物件大小下限（位元組）。 | 16384 | 不適用。 |
| 路徑 | AEM資料存放區的本機路徑。 | `crx-quickstart/repository/datastore` | 不適用。 |
| proxyHost | 設定使用者端連線時所使用的選用代理主機。 | | 不適用。 |
| proxyPort | 設定使用者端連線所透過的可選Proxy連線埠。 | | 不適用。 |
| s3Bucket | S3儲存貯體的名稱。 | | 是 |
| s3EndPoint | S3 REST API端點。 | | 不適用。 |
| s3Region | 貯體所在的區域。 如需詳細資訊，請參閱此[頁面](https://docs.aws.amazon.com/general/latest/gr/s3.html)。 | AWS執行個體執行所在的區域。 | 不適用。 |
| socketTimeout | 設定在連線逾時並關閉之前，透過已建立且開啟的連線傳輸資料所需的等待時間（毫秒）。 | 50000 | 不適用。 |
| stagingPurgeInterval | 從暫存快取中清除已完成的上傳的間隔（秒）。 | 300 | 不適用。 |
| stagingRetryInterval | 重試失敗的上傳間隔（以秒為單位）。 | 600 | 不適用。 |
| stagingSplitPercentage | 用於暫存非同步上載的`cacheSize`百分比。 | 10 | 不適用。 |
| uploadThreads | 用於非同步上傳的上傳執行緒數量。 | 10 | 不適用。 |
| writeThreads | 透過S3 Transfer Manager寫入時使用的並行執行緒數目。 | 10 | 不適用。 |

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
>`S3DataStore`、`CachingFileDataStore`和`AzureDataStore`的DataStore實作支援本機檔案系統快取。 當DataStore位於NFS （網路檔案系統）上時，`CachingFileDataStore`實作很有用。

從舊的快取實作(Oak 1.6以前版本)升級時，本機檔案系統快取目錄的結構會有差異。 在舊的快取結構中，下載的檔案和上傳的檔案都直接放在快取路徑下。 新結構會將下載和上傳分開，並將它們儲存在快取路徑下名為`upload`和`download`的兩個目錄中。 升級程式應該要流暢無礙，任何擱置的上傳都應排程進行上傳，且任何先前下載在快取中的檔案都會在初始化時放入快取中。

您也可以使用Oak-run的`datastorecacheupgrade`命令離線升級快取。 如需有關如何執行命令的詳細資訊，請檢查Oak-run模組的[讀我檔案](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md)。

快取具有大小限制，可使用cacheSize引數加以設定。

#### 下載 {#downloads}

從DataStore存取要求的檔案/blob之前，會先檢查本機快取是否有記錄。 將檔案新增至快取時，若快取超過設定的限制（請參閱`cacheSize`引數），則會收回部分檔案以回收空間。

#### 非同步上傳 {#async-upload}

快取支援非同步上傳至DataStore。 檔案會存放在本機的快取中（在檔案系統上），且會開始進行非同步工作來上傳檔案。 非同步上傳的數目受限於分段快取的大小。 使用`stagingSplitPercentage`引數設定暫存快取的大小。 此引數會定義用於暫存快取的快取大小百分比。 此外，下載可用的快取百分比計算為&#x200B;**(100 - `stagingSplitPercentage`) &#42;`cacheSize`**。

非同步上傳是多執行緒，且使用`uploadThreads`引數設定執行緒數目。

上傳完成後，檔案會移至主要下載快取。 當暫存快取大小超過其限制時，檔案會同步上傳至DataStore，直到前一個非同步上傳完成且暫存快取中再次有可用空間為止。 上傳的檔案會透過週期性工作（其間隔由`stagingPurgeInterval`引數設定）從臨時區域移除。

失敗的上傳（例如，由於網路中斷）會置於重試佇列並定期重試。 使用`stagingRetryInterval parameter`設定重試間隔。

#### 使用Amazon S3設定無二進位檔復寫 {#configuring-binaryless-replication-with-amazon-s}

若要使用S3設定無二進位式複製，必須執行下列步驟：

1. 安裝作者和發佈執行個體，並確定它們已正確啟動。
1. 開啟&#x200B;*https://localhost:4502/etc/replication/agents.author/publish.html*&#x200B;的頁面，前往復寫代理程式設定。
1. 按&#x200B;**設定**&#x200B;區段中的&#x200B;**編輯**&#x200B;按鈕。
1. 將&#x200B;**序列化**&#x200B;型別選項變更為&#x200B;**少二進位**。

1. 在傳輸URI中新增引數&quot; `binaryless`= `true`&quot;。 在變更後，URI應該看起來類似以下內容：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新啟動所有製作和發佈執行個體，讓變更生效。

#### 使用S3和MongoDB建立叢集 {#creating-a-cluster-using-s-and-mongodb}

1. 使用以下命令解壓縮CQ快速入門：

   `java -jar cq-quickstart.jar -unpack`

1. 解壓縮AEM後，請在安裝目錄&#x200B;*crx-quickstart*/*install*&#x200B;中建立資料夾。

1. 在`crx-quickstart`資料夾中建立這兩個檔案：

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*。*設定*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*。*設定*

   建立檔案後，視需要新增設定選項。

1. 依照上述說明，安裝S3資料存放區所需的兩個套件組合。
1. 確定已安裝MongoDB且正在執行`mongod`的執行個體。
1. 使用下列命令啟動AEM：

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 對第二個AEM例項重複步驟1到4。
1. 啟動第二個AEM執行個體。

#### 設定共用資料存放區 {#configuring-a-shared-data-store}

1. 首先，在共用資料存放區所需的每個執行個體上建立資料存放區設定檔案：

   * 如果您使用`FileDataStore`，請建立名為`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`的檔案，並將其放在`<aem-install>/crx-quickstart/install`資料夾中。

   * 如果使用S3做為資料存放區，請在`<aem-install>/crx-quickstart/install`資料夾中建立名為`rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`的檔案，如上所述。

1. 修改每個執行個體上的資料存放區組態檔，使其指向相同的資料存放區。 如需詳細資訊，請參閱[資料存放區組態](/help/sites-deploying/data-store-config.md#data-store-configurations)。
1. 如果執行個體是從現有的伺服器複製的，您必須在存放庫離線時使用最新的Oak-run工具移除新執行個體的`clusterId`。 您必須執行的命令為：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果已設定區段節點存放區，則必須指定存放庫路徑。 依預設，路徑為`<aem-install-folder>/crx-quickstart/repository/segmentstore.`如果設定了Document節點存放區，則您可以使用[Mongo連線字串URI](https://docs.mongodb.org/manual/reference/connection-string/)。

   >[!NOTE]
   >
   >可以從以下位置下載Oak執行的工具：
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >您必須根據您在安裝AEM時所使用的Oak版本，使用不同版本的工具。 在使用工具之前，請檢視以下版本需求清單：
   >
   >
   >
   >    * 若為Oak版本&#x200B;**1.2.x**，請使用Oak執行的&#x200B;**1.2.12或更新版本**
   >    * 若是比上述&#x200B;**更新的Oak版本**，請使用與AEM安裝的Oak核心相符的Oak-run版本。
   >
   >

1. 最後，驗證設定。 若要驗證，請尋找由共用該檔案的每個存放庫新增到資料存放區的唯一檔案。 檔案的格式為`repository-[UUID]`，其中UUID是每個個別存放庫的唯一識別碼。

   因此，正確的設定應具有與共用資料存放區的存放庫相同數目的唯一檔案。

   根據資料存放區，檔案的儲存方式不同：

   * 針對`FileDataStore`，檔案會在資料存放區資料夾的根路徑下建立。
   * 針對`S3DataStore`，檔案是在`META`資料夾下已設定的S3儲存貯體中建立的。

## Azure 資料存放區 {#azure-data-store}

AEM可設定為將資料儲存在Microsoft®的Azure儲存服務。 它使用`org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID進行設定。

若要啟用Azure資料存放區功能，必須下載並安裝包含Azure Connector的功能套件。 前往[Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/)並從Feature Pack 1.6.x版（例如com.adobe.granite.oak.azureblobconnector-1.6.3.zip）下載最新版本。

>[!NOTE]
>
>搭配TarMK使用AEM時，二進位檔預設會儲存在FileDataStore中。 若要搭配Azure DataStore使用TarMK，您必須使用`crx3tar-nofds`執行模式啟動AEM，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以依照以下步驟安裝和設定Azure聯結器：

1. 將Feature Pack zip檔案的內容解壓縮至暫存資料夾。

1. 移至暫存資料夾，並將`jcr_root/libs/system/install`的內容複製到`<aem-install>crx-quickstart/install`資料夾。
1. 如果AEM已設定為搭配Tar或MongoDB儲存體使用，請先從`/crx-quickstart/install`資料夾移除任何現有的設定檔，然後再繼續。 必須移除的檔案包括：

   ForMongoMK：

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   對於TarMK：

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回功能套件已擷取的暫存位置，並將`jcr_root/libs/system/config`的內容複製到`<aem-install>/crx-quickstart/install`資料夾。
1. 編輯組態檔並新增安裝程式所需的組態選項。
1. 啟動AEM。

您可以搭配下列選項使用組態檔：

* azureSas=」：在聯結器的1.6.3版本中，新增了Azure共用存取簽章(SAS)支援。 **如果組態檔中同時存在SAS和儲存認證，則SAS具有優先權。**&#x200B;如需SAS的詳細資訊，請參閱[正式檔案](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview)。 請確定&#39;=&#39;字元已逸出，如&#39;\=&#39;。

* azureBlobEndpoint=&quot;： Azure Blob端點。 例如，https://&lt;storage-account>.blob.core.windows.net。
* accessKey=&quot;：儲存體帳戶名稱。 如需Microsoft® Azure驗證認證的詳細資訊，請參閱[正式檔案](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create)。

* secretKey=&quot;：儲存體存取金鑰。 請確定&#39;=&#39;字元已逸出，如&#39;\=&#39;。
* container=&quot;： Microsoft® Azure Blob儲存容器名稱。 容器是一組Blob。 如需其他詳細資訊，請閱讀[正式檔案](https://learn.microsoft.com/en-us/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata?redirectedfrom=MSDN)。
* maxConnections=&quot;：每個作業同時發出的要求數目。 預設值為 1。
* maxErrorRetry=&quot;&quot;：每個請求的重試次數。 預設值為 3。
* socketTimeout=&quot;： 預設值為5分鐘。

除了上述設定外，您也可以設定下列設定：

* path：資料存放區的路徑。 預設值為`<aem-install>/repository/datastore.`
* RecordLength：應該儲存在資料存放區中的物件大小下限。 預設值為16 KB。
* maxCachedBinarySize：大小小於或等於此大小的二進位檔儲存在記憶體快取中。 大小以位元組為單位。 預設值為17408 (17 KB)。
* cacheSize：快取的大小。 此值是以位元組為單位指定的。 預設值為64 GB。
* 機密：僅在使用無二進位檔復寫進行共用資料存放區設定時使用。
* stagingSplitPercentage：設定為用於中繼非同步上傳的快取大小百分比。 預設值為 10。
* uploadThreads：用於非同步上傳的上傳執行緒數量。 預設值為 10。
* stagingPurgeInterval：從暫存快取中清除已完成上載的間隔（秒）。 預設值為300秒（5分鐘）。
* stagingRetryInterval：失敗上傳的重試間隔（秒）。 預設值為600秒（10分鐘）。

>[!NOTE]
>
>所有設定都應放在引號之間，例如：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## 資料存放區記憶體回收 {#data-store-garbage-collection}

資料存放區廢棄專案收集程式可用來移除資料存放區中所有未使用的檔案，進而在程式中釋放寶貴的磁碟空間。

您可以透過以下方式執行資料存放區記憶體回收：

1. 前往位於&#x200B;*https://&lt;serveraddress：port>/system/console/jmx*&#x200B;的JMX主控台
1. 正在搜尋&#x200B;**RepositoryManagement。**&#x200B;找到存放庫管理員MBean後，按一下它即可顯示可用的選項。
1. 捲動至頁面結尾，然後按一下&#x200B;**startDataStoreGC（布林值markOnly）**&#x200B;連結。
1. 在下列對話方塊中，輸入`markOnly`引數的`false`，然後按一下&#x200B;**叫用**：

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >`markOnly`參數列示記憶體回收的掃描階段是否執行。

## 共用資料存放區的資料存放區廢棄專案收集 {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>在叢集或共用資料存放區中執行記憶體回收時，設定（使用Mongo或Segment Tar）記錄可能會顯示無法刪除某些blob ID的警告。 在先前的記憶體回收專案中刪除的Blob ID會再次被其他沒有ID刪除相關資訊的叢集或共用節點錯誤參考。 因此，執行記憶體回收時，會在嘗試刪除上次執行中已刪除的ID時記錄警告。 此行為不會影響效能或功能。

>[!NOTE]
>
>如果您使用共用資料存放區設定，且資料存放區廢棄專案收集已停用，執行Lucene二進位清理工作可能會突然增加使用的磁碟空間。 請考慮執行下列動作，在所有作者和發佈執行個體上停用BlobTracker：
>
>1. 停止AEM執行個體。
>2. 在`crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`檔案中新增`blobTrackSnapshotIntervalInSecs=L"0"`引數。 此引數需要Oak 1.12.0、1.10.2或更新版本。
>3. 重新啟動AEM執行個體。

使用較新版本的AEM，資料存放區記憶體回收也可以在多個存放庫共用的資料存放區上執行。 若要在共用資料存放區上執行資料存放區記憶體回收，請執行下列步驟：

1. 請確定所有共用資料存放區的存放庫執行個體上，針對資料存放區廢棄專案收集設定的所有維護任務都已停用。
1. 在共用資料存放區的&#x200B;**所有**&#x200B;存放庫執行個體上個別執行[二進位記憶體回收](/help/sites-deploying/data-store-config.md#data-store-garbage-collection)中提到的步驟。 不過，在按一下[叫用]按鈕之前，請務必輸入`markOnly`引數的`true`：

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有執行個體上完成上述程式後，從&#x200B;**任一**&#x200B;執行個體再次執行資料存放區記憶體回收：

   1. 前往JMX主控台，然後選取「儲存區域管理員Mbean」。
   1. 按一下&#x200B;**Click startDataStoreGC（布林值markOnly）**&#x200B;連結。
   1. 在下列對話方塊中，再次輸入`markOnly`引數的`false`。

   所有找到的檔案會使用之前使用的標籤階段進行整理，並從資料存放區中刪除未使用的其餘檔案。
