---
title: 效能調整 [!DNL Assets].
description: 相關建議與指引 [!DNL Experience Manager] 設定、硬體、軟體和網路元件的變更，以移除瓶頸並最佳化效能。 [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2740'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 效能調整指南 {#assets-performance-tuning-guide}

一個 [!DNL Experience Manager Assets] 安裝程式包含數個硬體、軟體和網路元件。 視您的部署情況而定，您可能需要對硬體、軟體和網路元件進行特定組態變更，以移除效能瓶頸。

此外，識別並遵守某些軟硬體最佳化准則，有助於建立堅實的基礎，讓您的 [!DNL Experience Manager Assets] 部署，滿足效能、擴充能力及可靠性的期望。

效能不佳 [!DNL Experience Manager Assets] 可能會影響互動式效能、資產處理、下載速度和其他區域的使用者體驗。

事實上，效能最佳化是您在為任何專案建立目標度量之前所執行的根本任務。

以下是您發現的某些主要重點領域，並可在效能問題對使用者造成影響之前加以修正。

## Platform {#platform}

雖然Experience Manager在數個平台上都有支援，但Adobe發現對Linux和Windows上的原生工具有最大的支援，這有助於實現最佳效能和容易實作。 理想情況下，您應該部署64位元作業系統，以滿足 [!DNL Experience Manager Assets] 部署。 和任何Experience Manager部署一樣，您應該儘可能實作TarMK。 雖然TarMK無法擴展至單一編寫執行個體之外，但發現其效能比MongoMK好。 您可以新增TarMK解除安裝執行個體，以提升的工作流程處理能力。 [!DNL Experience Manager Assets] 部署。

### 暫存資料夾 {#temp-folder}

若要改善資產上傳時間，請為Java臨時目錄使用高效能儲存。 在Linux和Windows上，可以使用RAM磁碟機或SSD。 在雲端型環境中，可以使用同等的高速儲存型別。 例如，在Amazon EC2中， [暫存磁碟機](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 磁碟機可用於暫存資料夾。

假設伺服器具有足夠的記憶體，請設定RAM磁碟機。 在Linux上，執行下列命令來建立8 GB RAM磁碟機：

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows作業系統上，使用協力廠商驅動程式來建立RAM磁碟機，或只使用高效能儲存裝置（例如SSD）。

一旦高效能暫存磁碟區準備就緒，請設定JVM引數 `-Djava.io.tmpdir`. 例如，您可以將下列JVM引數新增至 `CQ_JVM_OPTS` 中的變數 `bin/start` 指令碼 [!DNL Experience Manager]：

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java設定 {#java-configuration}

### Java版本 {#java-version}

Adobe建議部署 [!DNL Experience Manager Assets] 在Java 8上以發揮最佳效能。

<!-- TBD: Link to the latest official word around Java.
-->

### JVM引數 {#jvm-parameters}

設定下列JVM引數：

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## 資料存放區和記憶體設定 {#data-store-and-memory-configuration}

### 檔案資料存放區設定 {#file-data-store-configuration}

建議所有使用者將資料存放區與區段存放區分開 [!DNL Experience Manager Assets] 使用者。 此外，設定 `maxCachedBinarySize` 和 `cacheSizeInMB` 引數有助於將效能最大化。 設定 `maxCachedBinarySize` 可以保留在快取中的最小檔案大小。 指定記憶體中的快取大小，以用於內的資料存放區 `cacheSizeInMB`. Adobe建議將此值設定在棧積總大小的2-10%之間。 不過，負載/效能測試可協助判斷理想的設定。

### 設定緩衝影像快取的大小上限 {#configure-the-maximum-size-of-the-buffered-image-cache}

將大量資產上傳到時 [!DNL Adobe Experience Manager]，若要允許記憶體消耗量出現非預期的尖峰，並防止JVM因OutOfMemoryErrors而失敗，請減少緩衝影像快取設定的大小上限。 請考量您有最大棧積(- `Xmx`引數)、1GB的Oak BlobCache和2GB的檔案快取設定。 在這種情況下，緩衝快取最多需要1.25 GB和記憶體，因此對於非預期的尖峰僅會留下0.75 GB的記憶體。

在OSGi Web主控台中設定緩衝快取大小。 在 `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`，設定屬性 `cq.dam.image.cache.max.memory` 位元組。 例如，1073741824是1 GB (1024 x 1024 x 1024 = 1 GB)。

從Experience Manager6.1 SP1，如果您使用 `sling:osgiConfig` 節點以設定此屬性，請確定將資料型別設定為Long。 如需詳細資訊，請參閱 [CQBufferedImageCache在資產上傳期間會消耗棧積](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### 共用的資料存放區 {#shared-data-stores}

實作S3或共用檔案資料存放區有助於在大規模實作中節省磁碟空間並提高網路輸送量。 如需使用共用資料存放區優點的詳細資訊，請參閱 [Assets規模調整指南](/help/assets/assets-sizing-guide.md).

### S3資料存放區 {#s-data-store}

下列S3資料存放區組態( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)已協助Adobe從現有檔案資料存放區中擷取12.8 TB的二進位大型物件(BLOB)，並存放至客戶網站的S3資料存放區：

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## 網路最佳化 {#network-optimization}

Adobe建議啟用HTTPS，因為許多公司都有會偵聽HTTP流量的防火牆，這會嚴重影響上傳和損毀檔案。 對於大型檔案上傳，請確定使用者已連線到網路，因為WiFi網路會快速飽和。 如需識別網路瓶頸的准則，請參閱 [Assets規模調整指南](/help/assets/assets-sizing-guide.md). 若要藉由分析網路拓撲來評估網路效能，請參閱 [資產網路考量事項](/help/assets/assets-network-considerations.md).

主要來說，您的網路最佳化策略取決於可用的頻寬量以及您的負載 [!DNL Experience Manager] 執行個體。 常見的設定選項，包括防火牆或代理程式，有助於改善網路效能。 請謹記以下要點：

* 根據您的執行個體型別（小、中、大），請確定您有足夠的網路頻寬來執行Experience Manager執行個體。 在下列情況下，充足的頻寬配置尤其重要： [!DNL Experience Manager] 託管於AWS上。
* 若您的 [!DNL Experience Manager] 執行個體在AWS上託管，您可以透過多樣化的縮放原則獲益。 如果使用者預期高負載，請放大執行個體。 縮減大小，以處理中度/低負載。
* HTTPS：大部分使用者都有會偵聽HTTP流量的防火牆，這可能會對檔案上傳造成負面影響，甚至在上傳作業期間損壞檔案。
* 大型檔案上傳：確保使用者已透過有線連線連線到網路（WiFi連線會快速飽和）。

## 工作流程 {#workflows}

### 暫時性工作流程 {#transient-workflows}

儘可能設定 [!UICONTROL DAM更新資產] 工作流程轉換為暫時性。 設定可大幅減少處理工作流程所需的間接成本，因為在此情況下，工作流程不需要通過正常的追蹤和封存程式。

1. 瀏覽至 `/miscadmin` 在 [!DNL Experience Manager] 部署位置 `https://[aem_server]:[port]/miscadmin`.

1. 展開 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]** > **[!UICONTROL dam]**.

1. 開啟 **[!UICONTROL DAM更新資產]**. 從浮動工具面板，切換至 **[!UICONTROL 頁面]** 標籤，然後按一下 **[!UICONTROL 頁面屬性]**.

1. 選取 **[!UICONTROL 暫時性工作流程]** 並按一下 **[!UICONTROL 確定]**.

   >[!NOTE]
   >
   >部分功能不支援暫時性工作流程。 若您的 [!DNL Assets] 部署需要這些功能，請勿設定暫時性工作流程。

在無法使用暫時性工作流程的情況下，請定期執行工作流程清除以刪除已封存的 [!UICONTROL DAM更新資產] 工作流程可確保系統效能不會降低。

通常每週執行清除工作流程。 不過，在資源密集的情況（例如大規模資產擷取期間），您可以更頻繁地執行。

若要設定工作流程清除，請透過OSGi主控台新增新的「AdobeGranite工作流程清除」設定。 接著，設定並排程工作流程，使其成為每週維護時段的一部分。

如果清除執行時間過長，則會逾時。 因此，您應該確保永久刪除工作完成，以避免因工作流程數量過多而導致永久刪除工作流程無法完成的情況。

例如，執行許多非暫時性工作流程（建立工作流程例項節點）後，您就可以執行 [ACS AEM Commons工作流程移除程式](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) 臨機操作。 它會立即移除多餘的已完成工作流程例項，而不是等候AdobeGranite工作流程清除排程器執行。

### 最大平行作業數 {#maximum-parallel-jobs}

根據預設， [!DNL Experience Manager] 執行的最大平行作業數等於伺服器上的處理器數。 此設定的問題是當負載很重時，所有的處理器都被 [!UICONTROL DAM更新資產] 工作流程，降低UI回應速度並防止 [!DNL Experience Manager] 執行其他可保護伺服器效能與穩定性的程式。 若要將此值設為伺服器上可用處理器的一半，請執行下列步驟：

1. 開啟 [!DNL Experience Manager] 作者，存取 `https://[aem_server]:[port]/system/console/slingevent`.

1. 按一下 **[!UICONTROL 編輯]** 例如，在與您的實施相關的每個工作流程佇列上， **[!UICONTROL Granite暫時工作流程佇列]**.

1. 更新值 **[!UICONTROL 最大平行作業數]** 並按一下 **[!UICONTROL 儲存]**.

將佇列設定為可用處理器的一半，是可行的解決方案。 不過，您可能必須增加或減少此數目，才能達到最大輸送量，並依環境進行調整。 暫時性和非暫時性工作流程和其他程式（例如外部工作流程）有單獨的佇列。 如果數個佇列設定為50%的處理器同時啟動，系統可能會快速超載。 大量使用的佇列在使用者實作中差異極大。 因此，您可能必須周全地設定這些伺服器，才能在不犧牲伺服器穩定性的情況下，發揮最大效率。

### DAM更新資產設定 {#dam-update-asset-configuration}

此 [!UICONTROL DAM更新資產] 工作流程包含針對工作設定的完整步驟套件，例如Dynamic Media PTIFF產生和 [!DNL Adobe InDesign Server] 整合。 不過，大多數使用者可能不需要執行其中的數個步驟。 Adobe建議您建立 [!UICONTROL DAM更新資產] 工作流程模型，並移除任何不必要的步驟。 在此情況下，請更新啟動器， [!UICONTROL DAM更新資產] 以指向新模型。

執行 [!UICONTROL DAM更新資產] 工作流程可能會大幅增加檔案資料存放區的大小。 Adobe執行的實驗結果顯示，如果在8小時內執行約5500個工作流程，資料存放區大小可以增加約400 GB。

這是一種臨時性的增加，當您執行資料存放區廢棄專案收集工作後，資料存放區會恢復為原始大小。

通常資料存放區記憶體回收任務會與其他排程的維護任務一起每週執行。

如果您的磁碟空間有限，請執行 [!UICONTROL DAM更新資產] 在工作流程中，請考慮更頻繁地排程記憶體回收工作。

#### 產生執行階段轉譯 {#runtime-rendition-generation}

客戶在其網站上或使用各種大小和格式的影像，或分發給業務合作夥伴。 由於每個轉譯都會增加存放庫中資產的足跡，Adobe建議您謹慎使用此功能。 若要減少處理和儲存影像所需的資源量，您可以在執行階段產生這些影像，而不是在擷取期間做為轉譯。

許多Sites客戶會實作影像servlet，在請求影像時調整大小並裁切，這會對發佈執行個體施加額外的負載。 不過，只要可以快取這些影像，挑戰就能緩解。

另一種方法是使用Dynamic Media技術完全放棄影像操控。 此外，您可以部署Brand Portal，不僅負責從以下系統產生轉譯： [!DNL Experience Manager] 基礎架構，以及整個發佈階層。

#### ImageMagick {#imagemagick}

如果您自訂 [!UICONTROL DAM更新資產] 若要使用ImageMagick產生轉譯的工作流程，Adobe建議您修改 `policy.xml` 檔案位於 `/etc/ImageMagick/`. 依預設，ImageMagick會使用OS磁碟區上的整個可用磁碟空間，以及可用的記憶體。 在「 」中變更下列設定 `policymap` 部分 `policy.xml` 以限制這些資源。

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

此外，請將ImageMagick的暫存資料夾路徑設定在 `configure.xml` 檔案（或透過設定環境變數） `MAGICK_TEMPORARY_PATH`)至具有足夠空間和IOPS的磁碟分割區。

>[!CAUTION]
>
>如果ImageMagick使用所有可用的磁碟空間，錯誤設定可能會使伺服器不穩定。 使用ImageMagick處理大型檔案所需的原則變更可能會影響 [!DNL Experience Manager] 效能。 如需詳細資訊，請參閱 [安裝及設定ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` 和 `configure.xml` 檔案位於 `/usr/lib64/ImageMagick-&#42;/config/` 而非 `/etc/ImageMagick/`另請參閱 [ImageMagick檔案](https://www.imagemagick.org/script/resources.php) 設定檔的位置。

如果您使用 [!DNL Experience Manager] 如果您打算處理大量大型PSD或PSB檔案，請在AdobeManaged Services (AMS)時聯絡Adobe客戶支援。 與Adobe客戶支援代表合作，針對您的AMS部署實作這些最佳實務，並針對Adobe的專有格式選擇最佳可行的工具和模型。 [!DNL Experience Manager] 可能無法處理超過 30000 x 23000 像素的極高解析度 PSB 檔案。

### XMP回寫 {#xmp-writeback}

XMP回寫會在修改中繼資料時更新原始資產 [!DNL Experience Manager]，會產生下列結果：

* 資產本身已修改
* 已建立資產的版本
* [!UICONTROL DAM更新資產] 對資產執行

列出的結果會消耗相當多的資源。 因此，Adobe建議在不需要時停用XMP回寫。 如需詳細資訊，請參閱 [XMP回寫](/help/assets/xmp-writeback.md).

如果勾選執行工作流程旗標，匯入大量中繼資料可能會導致資源密集的XMP回寫活動。 在精益伺服器使用期間規劃這類匯入，以免影響其他使用者的效能。

## 複製 {#replication}

將資產復寫至大量發佈執行個體時（例如在Sites實作中），Adobe建議您使用鏈結復寫。 在這種情況下，製作執行個體會複製到單一發佈執行個體，接著複製到其他發佈執行個體，釋放製作執行個體。

### 設定鏈結復寫 {#configure-chain-replication}

1. 選擇您要用來連結復寫的發佈執行個體
1. 在該發佈執行個體上新增指向其他發佈執行個體的復寫代理
1. 在每個復寫代理程式上，啟用「觸發器」標籤上的「接收時」

>[!NOTE]
>
>Adobe不建議自動啟用資產。 不過，如有必要，Adobe建議將此作為工作流程的最後步驟，通常是DAM更新資產。

## 搜尋索引 {#search-indexes}

安裝 [最新Service Pack](/help/release-notes/release-notes.md) 和效能相關的Hotfix，因為這些通常包含系統索引的更新。 另請參閱 [效能調整秘訣](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) 針對某些索引最佳化。

為您經常執行的查詢建立自訂索引。 如需詳細資訊，請參閱 [分析緩慢查詢的方法](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 和 [製作自訂索引](/help/sites-deploying/queries-and-indexing.md). 如需查詢和索引最佳實務的其他深入分析，請參閱 [查詢和建立索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene索引設定 {#lucene-index-configurations}

可對Oak索引設定進行一些最佳化，以協助改進 [!DNL Experience Manager Assets] 效能。 更新索引設定以改善重新索引時間：

1. 開啟CRXDe `/crx/de/index.jsp` 並以管理使用者身分登入。
1. 瀏覽至 `/oak:index/lucene`.
1. 新增 `String[]` 屬性 `excludedPaths` 含值 `/var`， `/etc/workflow/instances`、和 `/etc/replication`.
1. 瀏覽至 `/oak:index/damAssetLucene`. 新增 `String[]` 屬性 `includedPaths` 含值 `/content/dam`. 儲存變更。

如果您的使用者不需要進行資產的全文搜尋，例如在PDF檔案中搜尋文字，然後停用它。 您可以停用全文檢索索引來改善索引效能。 若要停用 [!DNL Apache Lucene] 文字擷取，請遵循下列步驟：

1. 在 [!DNL Experience Manager] 介面，存取 [!UICONTROL 封裝管理員].
1. 上傳並安裝套裝，請前往 [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### 猜測總數 {#guess-total}

建立產生大型結果集的查詢時，請使用 `guessTotal` 引數，以避免在執行時佔用大量記憶體。

## 已知問題 {#known-issues}

### 大型檔案 {#large-files}

有兩個與中的大型檔案相關的主要已知問題 [!DNL Experience Manager]. 當檔案大小超過2 GB時，冷待命同步處理可能會發生記憶體不足的情況。 在某些情況下，它會防止待命同步處理執行。 在其他情況下，這會造成主要執行個體當機。 這種情況適用於中的任何檔案 [!DNL Experience Manager] 大於2GB，包括內容套件。

同樣地，當檔案在使用共用S3資料存放區時達到2 GB的大小時，可能需要一些時間才能將檔案從快取完全儲存至檔案系統。 因此，使用無二進位檔的復寫時，在復寫完成之前，二進位檔資料可能尚未儲存。 這種情況可能會導致問題，尤其是當資料可用性很重要時。

## 效能測試 {#performance-testing}

代表每 [!DNL Experience Manager] 部署，建立效能測試制度，以便快速找出並解決瓶頸問題。 以下是需要關注的一些關鍵領域。

### 網路測試 {#network-testing}

針對客戶的所有網路效能顧慮，請執行以下工作：

* 測試客戶網路內的網路效能
* 從Adobe網路內測試網路效能。 對於AMS客戶，請與您的CSE合作，從Adobe網路內部進行測試。
* 從另一個存取點測試網路效能
* 使用網路效能指標工具
* 針對Dispatcher進行測試

### [!DNL Experience Manager] 部署測試 {#aem-deployment-testing}

若要透過有效率的CPU使用率和負載共用，將延遲降至最低並達到高輸送量，請監視您的效能 [!DNL Experience Manager] 定期部署。 尤其是：

* 針對執行負載測試 [!DNL Experience Manager] 部署。
* 監視上傳效能和UI回應能力。

## [!DNL Experience Manager Assets] 績效檢查清單和資產管理任務的影響 {#checklist}

* 啟用HTTPS以繞過任何企業HTTP流量嗅探器。
* 使用有線連線上傳大量資產。
* 在Java 8上部署。
* 設定最佳的JVM引數。
* 設定檔案系統資料存放區或S3資料存放區。
* 停用子資產產生。 如果啟用，AEM工作流程會為多頁資產中的每個頁面建立個別資產。 這些頁面都是個別資產，會消耗額外的磁碟空間、需要版本設定和其他工作流程處理。 如果您不需要個別頁面，請停用子資產產生和頁面擷取活動。
* 啟用暫時性工作流程。
* 調整Granite工作流程佇列以限制並行工作。
* 設定 [!DNL ImageMagick] 以限制資源消耗。
* 從移除不必要的步驟 [!UICONTROL DAM更新資產] 工作流程。
* 設定工作流程和版本清除。
* 使用最新Service Pack和Hotfix最佳化索引。 請向Adobe客戶支援洽詢任何可能提供的其他索引最佳化。
* 使用guessTotal來最佳化查詢效能。
* 如果您設定 [!DNL Experience Manager] 從檔案內容偵測檔案型別(透過啟用 **[!UICONTROL Day CQ DAM Mime型別服務]** 在 **[!UICONTROL AEM Web Console]**)，在非尖峰時段大量上傳許多檔案，因為它耗用大量資源。
