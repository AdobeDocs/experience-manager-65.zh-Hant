---
title: 在6中配置節點儲存和數AEM據儲存
description: 瞭解如何配置節點儲存和資料儲存以及如何執行資料儲存垃圾收集。
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: 4e68a8a8d84d0ffa1d28ab13c196731e58b4cf9a
workflow-type: tm+mt
source-wordcount: '3447'
ht-degree: 0%

---

# 在6中配置節點儲存和數AEM據儲存{#configuring-node-stores-and-data-stores-in-aem}

## 簡介 {#introduction}

在Adobe Experience Manager(AEM)中，二進位資料可以獨立於內容節點儲存。 二進位資料被儲存在資料儲存中，而內容節點被儲存在節點儲存中。

可以使用OSGi配置配置資料儲存和節點儲存。 每個OSGi配置使用持久標識符(PID)被引用。

## 配置步驟 {#configuration-steps}

要配置節點儲存和資料儲存，請執行以下步驟：

1. 將快速AEM啟動JAR檔案複製到其安裝目錄。
1. 建立資料夾 `crx-quickstart/install` 的子菜單。
1. 首先，通過建立包含要在中使用的節點儲存選項名稱的配置檔案來配置節點儲存 `crx-quickstart/install` 的子菜單。

   例如，文檔節點儲存(是AEMMongoMK實現的基礎)使用檔案 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`。

1. 編輯檔案並設定配置選項。
1. 使用要使用的資料儲存的PID建立配置檔案。 編輯檔案以設定配置選項。

   >[!NOTE]
   >
   >請參閱 [節點儲存配置](#node-store-configurations) 和 [資料儲存配置](#data-store-configurations) 的子菜單。

1. 開始AEM。

## 節點儲存配置 {#node-store-configurations}

>[!CAUTION]
>
>Oak的新版本為OSGi配置檔案採用了新的命名方案和格式。 新命名方案要求對配置檔案命名 **.config** 而新格式需要鍵入值，並且 [此處](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)。
>
>如果從較舊版本的Oak升級，請確保備份 `crx-quickstart/install`資料夾。 升級後，將資料夾的內容還原到已升級的安裝，並修改配置檔案的副檔名 **.cfg** 至 **.config**。
>
>如果您正在閱讀本文，以準備從 **AEM 5.x** 安裝，確保您 [升級](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) 文檔。

### 段節點儲存 {#segment-node-store}

段節點儲存是Adobe在6中實現TarMK的基礎AEM。 它使用 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` 用於配置的PID。

>[!CAUTION]
>
>段節點儲存的PID已從 `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` AEM6到 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` 6AEM.3確保進行必要的配置調整以反映此更改。

可以配置以下選項：

* `repository.home`:儲存與儲存庫相關資料的儲存庫主目錄的路徑。 預設情況下，段檔案儲存在 `crx-quickstart/segmentstore` 的子菜單。

* `tarmk.size`:段的最大大小(MB)。 預設最大值為256MB。
* `customBlobStore`:指示使用自定義資料儲存的布爾值。 6.3及更高版本AEM的預設值為true。 6.AEM3之前的預設值為false。

以下是示例 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 檔案：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 文檔節點儲存 {#document-node-store}

文檔節點儲存是MongoMK實AEM現的基礎。 它使用 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 以下配置選項可用：

* `mongouri`:的 [蒙戈URI](https://docs.mongodb.org/manual/reference/connection-string/) 連接到Mongo資料庫所需。 預設值為 `mongodb://localhost:27017`

* `db`:Mongo資料庫的名稱。 預設值為 **橡樹** ``. However, new AEM 6 installations use **aem-author** ``作為預設資料庫名。

* `cache`:快取大小(MB)。 它分佈在DocumentNodeStore中使用的各種快取中。 預設值為 `256`

* `changesSize`:Mongo中用於快取差異輸出的封蓋集合的大小(MB)。 預設值為 `256`

* `customBlobStore`:指示將使用自定義資料儲存的布爾值。 預設為 `false`。

以下是示例 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` 檔案：

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## 資料儲存配置 {#data-store-configurations}

在處理大量二進位檔案時，建議使用外部資料儲存而不是預設節點儲存，以最大化效能。

例如，如果您的項目需要大量媒體資產，則將它們儲存在檔案或S3資料儲存下會使訪問它們比直接儲存在MongoDB中更快。

與MongoDB相比，檔案資料儲存提供了更好的效能，而且Mongo備份和恢復操作在大量資產的情況下也更慢。

下面介紹了不同資料儲存和配置的詳細資訊。

>[!NOTE]
>
>要啟用自定義資料儲存，您需要確保 `customBlobStore` 設定為 `true` 在相應的節點儲存配置檔案([段節點儲存](/help/sites-deploying/data-store-config.md#segment-node-store) 或 [文檔節點儲存](/help/sites-deploying/data-store-config.md#document-node-store))。

### 檔案資料存放區 {#file-data-store}

這是 [檔案資料儲存](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) 《野兔2》 它提供了一種將二進位資料作為普通檔案儲存在檔案系統上的方法。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID。

這些配置選項可用：

* `repository.home`:儲存各種儲存庫相關資料的儲存庫主目錄的路徑。 預設情況下，二進位檔案將儲存在 `crx-quickstart/repository/datastore` 目錄

* `path`:儲存檔案的目錄的路徑。 如果指定，則優先於 `repository.home` 值

* `minRecordLength`:資料儲存中儲存的檔案的最小大小（以位元組為單位）。 小於此值的二進位內容將被內嵌。

>[!NOTE]
>
>使用NAS儲存共用檔案資料儲存時，請確保僅使用高效能設備以避免效能問題。

## AmazonS3資料儲存 {#amazon-s-data-store}

可AEM以配置為在Amazon的簡單儲存服務(S3)中儲存資料。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 用於配置的PID。

為了啟用S3資料儲存功能，需要下載並安裝包含S3資料儲存連接器的功能包。 轉到 [Adobe儲存庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) 並從功能包的1.10.x版本下載最新版本(例如com.adobe.granite.oak.s3connector-1.10.0.zip)。 此外，您還需要下載和安裝AEM上列出的最新Service Pack [AEM6.5發行說明](/help/release-notes/release-notes.md) 的子菜單。

>[!NOTE]
>
>與TarMKAEM一起使用時，二進位檔案將預設儲存在 `FileDataStore`。 要將TarMK與S3資料儲存區一起使用，需AEM要使用 `crx3tar-nofds` runmode，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以按如下方式安裝和配置S3連接器：

1. 將功能包zip檔案的內容解壓到臨時資料夾。

1. 轉到臨時資料夾並導航到以下位置：

   ```xml
   jcr_root/libs/system/install
   ```

   將上述位置的所有內容複製到 `<aem-install>/crx-quickstart/install.`

1. 如AEM果已配置為使用Tar或MongoDB儲存，請從***中刪除任何現有配置檔案&lt;aem-install>***/*crx快速啟動*/*安裝* 資料夾。 需要刪除的檔案包括：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回到提取功能包的臨時位置，並複製以下資料夾的內容：

   * `jcr_root/libs/system/config`

   至

   * `<aem-install>/crx-quickstart/install`

   確保僅複製當前配置所需的配置檔案。 對於專用資料儲存和共用資料儲存設定，複製 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 的子菜單。

   >[!NOTE]
   >
   >在群集設定中，逐個對群集的所有節點執行上述步驟。 另外，確保對所有節點使用相同的S3設定。

1. 編輯檔案並添加安裝程式所需的配置選項。
1. 開始AEM。

### 升級到新版本的1.10.x S3連接器 {#upgrading-to-a-new-version-of-the-s-connector}

如果需要升級到1.10.x S3連接器的新版本(例如，從1.10.0到1.10.4)，請執行以下步驟：

1. 停止實AEM例。

1. 導航到 `<aem-install>/crx-quickstart/install/15` 的子AEM目錄。
1. 備份後，通過刪除S3連接器中的所有jar檔案，刪除舊版本的S3連接器及其依賴項 `<aem-install>/crx-quickstart/install/15` 資料夾，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述檔案名僅用於圖示。

1. 從下載 [Adobe儲存庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)。
1. 將內容解壓縮到單獨的資料夾，然後導航到 `jcr_root/libs/system/install/15`。
1. 將jar檔案複製到 **&lt;aem-install>**/crx-quickstart/install/15AEM。
1. 啟AEM動並檢查連接器功能。

可將配置檔案與以下選項一起使用：

* accessKey:AWS接入密鑰。
* 密鑰：AWS的秘密訪問密鑰。 **注：** 當 `accessKey` 或 `secretKey` 未指定 [IAM角色](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) 用於驗證。
* s3Bucket:儲存段名稱。
* s3區域：桶區域。
* 路徑：資料儲存的路徑。 預設值為 **&lt;aem install=&quot;&quot; folder=&quot;&quot;>/資料庫/資料儲存庫**
* minRecordLength:應儲存在資料儲存中的對象的最小大小。 最小/預設值為 **16KB。**
* maxCachedBinarySize:大小小於或等於此大小的二進位檔案將儲存在記憶體快取中。 大小以位元組為單位。 預設值為**17408 **(17 KB)。

* cacheSize:快取的大小。 該值以位元組為單位指定。 預設值為 **64GB**。
* 機密：僅在將無聯機複製用於共用資料儲存設定時使用。
* stagingSplitPercentage:配置為用於暫存非同步上載的快取大小的百分比。 預設值為 **10**。
* 上載線程：用於非同步上載的上載線程數。 預設值為 **10**。
* stagingPurgeInterval:從暫存快取清除已完成上載的間隔（秒）。 預設值為 **300** 秒（5分鐘）。
* 臨時重試間隔：上載失敗的重試間隔（秒）。 預設值為 **600** 秒（10分鐘）。

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
   <td>亞太（雪梨）<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>亞太（東京）</td>
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
>DataStore實現 `S3DataStore`。 `CachingFileDataStore` 和 `AzureDataStore` 支援本地檔案系統快取。 的 `CachingFileDataStore` 當DataStore位於NFS（網路檔案系統）上時，實現非常有用。

從較舊的快取實現（Oak 1.6之前）升級時，本地檔案系統快取目錄的結構存在差異。 在舊快取結構中，下載的檔案和上載的檔案都直接放在快取路徑下。 新結構將下載和上載分離，並將它們儲存在名為 `upload` 和 `download` 在快取路徑下。 升級過程應是無縫的，任何掛起的上載都應安排上載，並且在初始化時，快取中任何先前下載的檔案都將放入快取中。

您還可以使用 `datastorecacheupgrade` 橡樹跑。 有關如何執行命令的詳細資訊，請檢查 [自述](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) 橡木跑道艙。

快取具有大小限制，可使用cacheSize參數配置。

**下載**

在從DataStore訪問請求的檔案/blob之前，將檢查本地快取中的記錄。 當快取超出配置的限制時(請參見 `cacheSize` 參數)時，將檔案添加到快取中，然後將逐出某些檔案以回收空間。

**非同步上載**

快取支援非同步上載到DataStore。 檔案將在快取中（在檔案系統上）本地存放，非同步作業將開始上載檔案。 非同步上載的數量受暫存快取大小的限制。 使用 `stagingSplitPercentage` 的下界。 此參數定義用於暫存快取的快取大小的百分比。 此外，可用於下載的快取百分比計算為 **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**。

非同步上載是多線程的，並且線程數是通過 `uploadThreads` 的下界。

上載完成後，檔案將移到主下載快取。 當臨時快取大小超過其限制時，檔案將同步上載到DataStore，直到先前的非同步上載完成，並且在臨時快取中再次有可用空間。 上載的檔案通過週期作業從暫存區域中刪除，該定期作業的間隔由 `stagingPurgeInterval` 的下界。

失敗的上載（例如，由於網路中斷）會被置於重試隊列中並定期重試。 使用 `stagingRetryInterval parameter`。

#### 使用AmazonS3配置無聯機複製 {#configuring-binaryless-replication-with-amazon-s}

要使用S3配置無二進位複製，需要執行以下步驟：

1. 安裝作者和發佈實例並確保它們已正確啟動。
1. 開啟頁面以轉到 *https://localhost:4502/etc/replication/agents.author/publish.html*。
1. 按 **編輯** 按鈕 **設定** 的子菜單。
1. 更改 **序列化** 類型選項 **二進位**。

1. 添加參數&#39;&#39; `binaryless`= `true`」。 更改後，URI應與以下內容類似：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新啟動所有作者和發佈實例以使更改生效。

#### 使用S3和MongoDB建立群集 {#creating-a-cluster-using-s-and-mongodb}

1. 使用以下命令解包CQ快速啟動：

   `java -jar cq-quickstart.jar -unpack`

1. 解壓AEM縮後，在安裝目錄內建立一個資料夾 *crx快速啟動*/*安裝*。

1. 在 `crx-quickstart` 資料夾：

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*。*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*。*配置*

   建立檔案後，根據需要添加配置選項。

1. 按上述說明安裝S3資料儲存所需的兩個捆綁包。
1. 確保已安裝MongoDB並且已安裝 `mongod` 正在運行。
1. 以下AEM命令開始：

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 對第二個實例重複步驟1AEM至4。
1. 啟動第二個AEM實例。

#### 配置共用資料儲存 {#configuring-a-shared-data-store}

1. 首先，在共用資料儲存所需的每個實例上建立資料儲存配置檔案：

   * 如果使用 `FileDataStore`，建立名為 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 然後放在 `<aem-install>/crx-quickstart/install` 的子菜單。

   * 如果使用S3作為資料儲存，請建立名為 `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 的 `<aem-install>/crx-quickstart/install` 資料夾。

1. 修改每個實例上的資料儲存配置檔案以指向同一資料儲存。 有關詳細資訊，請參見 [這篇文章](/help/sites-deploying/data-store-config.md#data-store-configurations)。
1. 如果實例已從現有伺服器中克隆，則需要刪除 `clusterId` 在儲存庫離線時使用最新的oak-run工具。 您需要運行的命令是：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果配置了段節點儲存，則需要指定儲存庫路徑。 預設情況下，路徑為 `<aem-install-folder>/crx-quickstart/repository/segmentstore.` 如果配置了文檔節點儲存，則可以使用 [Mongo連接字串URI](https://docs.mongodb.org/manual/reference/connection-string/)。

   >[!NOTE]
   >
   >Oak-run工具可從以下位置下載：
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >請注意，根據您在安裝時使用的Oak版本，需要使用不同版本的工AEM具。 使用該工具之前，請檢查下面的版本要求清單：
   >
   >
   >
   >    * 對於Oak版本 **1.2.x** 使用橡樹嶺 **1.2.12或更新**
   >    * 對於Oak版本 **比上面更新**，使用與安裝Oak內核相匹配的Oak-runAEM版本。


1. 最後，驗證配置。 為此，您需要查找由共用資料儲存的每個儲存庫添加到資料儲存的唯一檔案。 檔案的格式為 `repository-[UUID]`，其中UUID是每個單個儲存庫的唯一標識符。

   因此，正確的配置應具有與共用資料儲存的儲存庫相同的唯一檔案。

   檔案儲存方式不同，具體取決於資料儲存方式：

   * 對於 `FileDataStore` 檔案是在資料儲存資料夾的根路徑下建立的。
   * 對於 `S3DataStore` 檔案是在配置的S3儲存桶中 `META` 的子菜單。

## Azure 資料存放區 {#azure-data-store}

可AEM以配置為在Microsoft的Azure儲存服務中儲存資料。 它使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` 用於配置的PID。

為了啟用Azure資料儲存功能，需要下載並安裝包含Azure連接器的功能包。 轉到 [Adobe儲存庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) 並從功能包的1.6.x版下載最新版本(例如com.adobe.granite.oak.azureblobconnector-1.6.3.zip)。

>[!NOTE]
>
>與TarMKAEM一起使用時，預設情況下二進位檔案將儲存在FileDataStore中。 若要將TarMK與Azure DataStore一起使用，AEM您需要開始使用 `crx3tar-nofds` runmode，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以按如下方式安裝和配置Azure連接器：

1. 將功能包zip檔案的內容解壓到臨時資料夾。

1. 轉到臨時資料夾並複製 `jcr_root/libs/system/install` 到 `<aem-install>crx-quickstart/install` 的子菜單。
1. 如果AEM已配置為使用Tar或MongoDB儲存，請從 `/crx-quickstart/install` 資料夾。 需要刪除的檔案包括：

   ForMongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   對於TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回到提取特徵包的臨時位置並複製 `jcr_root/libs/system/config` 到 `<aem-install>/crx-quickstart/install` 的子菜單。
1. 編輯配置檔案並添加安裝程式所需的配置選項。
1. 開始AEM。

可將配置檔案與以下選項一起使用：

* azureSas=&quot;&quot;:在連接器1.6.3版中，添加了Azure共用訪問簽名(SAS)支援。 **如果配置檔案中同時存在SAS和儲存憑據，則SAS具有優先順序。** 有關SAS的詳細資訊，請參閱 [正式檔案](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1)。 確保「=」字元像「\=」一樣轉義。

* azureBlobEndpoint=&quot;&quot;:Azure Blob終結點。 例如，https://&lt;storage-account>.blob.core.windows.net。
* accessKey=&quot;&quot;:儲存帳戶名。 有關MicrosoftAzure身份驗證憑據的詳細資訊，請參閱 [正式檔案](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account)。

* secretKey=&quot;&quot;:儲存訪問密鑰。 確保「=」字元像「\=」一樣轉義。
* container=&quot;&quot;:MicrosoftAzure Blob儲存容器名稱。 容器是一組Blob的分組。 有關其他詳細資訊，請閱讀 [正式檔案](https://msdn.microsoft.com/en-us/library/dd135715.aspx)。
* maxConnections=&quot;&quot;:每個工序同時請求的併發數。 預設值為 1。
* maxErrorRetry=&quot;&quot;:每個請求的重試次數。 預設值為 3。
* socketTimeout=&quot;&quot;:用於請求的超時間隔（毫秒）。 預設值為5分鐘。

除上述設定外，還可以配置以下設定：

* 路徑：資料儲存的路徑。 預設值為 `<aem-install>/repository/datastore.`
* 記錄長度：應儲存在資料儲存中的對象的最小大小。 預設為16KB。
* maxCachedBinarySize:大小小於或等於此大小的二進位檔案將儲存在記憶體快取中。 大小以位元組為單位。 預設為17408(17 KB)。
* cacheSize:快取的大小。 該值以位元組為單位指定。 預設為64GB。
* 機密：僅在將無聯機複製用於共用資料儲存設定時使用。
* stagingSplitPercentage:配置為用於暫存非同步上載的快取大小的百分比。 預設值為 10。
* 上載線程：用於非同步上載的上載線程數。 預設值為 10。
* stagingPurgeInterval:從暫存快取清除已完成上載的間隔（秒）。 預設值為300秒（5分鐘）。
* 臨時重試間隔：上載失敗的重試間隔（秒）。 預設值為600秒（10分鐘）。

>[!NOTE]
>
>所有設定都應放在引號之間，例如：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## 資料儲存垃圾收集 {#data-store-garbage-collection}

資料儲存垃圾收集過程用於去除資料儲存中任何未使用的檔案，從而釋放該過程中寶貴的磁碟空間。

您可以通過以下方式運行資料儲存垃圾收集：

1. 正在轉到位於 *https://&lt;serveraddress:port>/system/console/jmx*
1. 搜索 **儲存庫管理。** 找到儲存庫管理器MBean後，按一下它可開啟可用選項。
1. 滾動到頁面結尾，然後按一下 **startDataStoreGC（布爾markOnly）** 的子菜單。
1. 在以下對話框中，輸入 `false` 為 `markOnly` 參數，然後按一下 **調用**:

   ![chlimage-1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >的 `markOnly` paramater表示垃圾收集的掃描階段是否將運行。

## 共用資料儲存的資料儲存垃圾收集 {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>在群集或共用資料儲存設定（使用Mongo或Segment Tar）中執行垃圾收集時，日誌可能會顯示無法刪除某些Blob ID的警告。 這是因為先前垃圾收集中刪除的Blob ID被沒有ID刪除資訊的其他群集或共用節點錯誤地再次引用。 因此，當執行垃圾收集時，它會在嘗試刪除上次運行中已刪除的ID時記錄警告。 此行為不影響效能或功能。

>[!NOTE]
> 如果您使用共用資料儲存設定，並且已禁用資料儲存垃圾收集，則運行Lucene Binary清理任務可能會突然增加所用的磁碟空間。 為避免這種情況，您需要在所有作者和發佈實例上禁用BlobTracker，如下所示：
>
> 1. 停止實AEM例。
> 2. 添加 `blobTrackSnapshotIntervalInSecs=L"0"` 參數 `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 的子菜單。 此參數需要Oak 1.12.0、1.10.2或更高版本。
> 3. 重新啟動實AEM例。


使用較新版本AEM的，資料儲存垃圾收集也可以在由多個儲存庫共用的資料儲存上運行。 為了能夠在共用資料儲存上運行資料儲存垃圾收集，請執行以下步驟：

1. 確保為資料儲存垃圾收集配置的任何維護任務在共用資料儲存的所有儲存庫實例上都被禁用。
1. 運行中提及的步驟 [二進位垃圾收集](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) 單獨 **全部** 共用資料儲存的儲存庫實例。 但是，請確保輸入 `true` 為 `markOnly` 參數，然後按一下「調用」按鈕：

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有實例上完成上述過程後，再次運行資料儲存垃圾收集 **任何** 例：

   1. 轉到JMX控制台，然後選擇Repository Manager Mbean。
   1. 按一下 **按一下startDataStoreGC（布爾標籤僅）** 的子菜單。
   1. 在以下對話框中，輸入 `false` 為 `markOnly` 的雙曲餘切值。
   這將整理使用之前使用的標籤階段找到的所有檔案，並從資料儲存中刪除未使用的其餘檔案。
