---
title: 效能調整 [!DNL Assets].
description: 關於 [!DNL Experience Manager] 配置、對硬體、軟體和網路元件的更改，以消除瓶頸並優化 [!DNL Experience Manager Assets]。
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2746'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 效能調整指南 {#assets-performance-tuning-guide}

安 [!DNL Experience Manager Assets] 安裝程式包含許多硬體、軟體和網路元件。 根據部署方案，您可能需要對硬體、軟體和網路元件進行特定的配置更改，以消除效能瓶頸。

此外，確定並遵守某些硬體和軟體優化准則有助於建立一個良好的基礎，使您能夠 [!DNL Experience Manager Assets] 部署以滿足效能、可擴充性和可靠性方面的期望。

效能差 [!DNL Experience Manager Assets] 可以影響用戶在交互效能、資產處理、下載速度等方面的體驗。

事實上，效能優化是您在為任何項目建立目標度量之前執行的一項基本任務。

以下是一些關鍵重點領域，您可以圍繞這些領域發現並修復效能問題，以免它們對用戶產生影響。

## Platform {#platform}

雖然Experience Manager在許多平台上都受支援，但Adobe在Linux和Windows上發現對本機工具的支援最強，這有助於實現最佳效能和易於實施。 理想情況下，您應部署64位作業系統，以滿足 [!DNL Experience Manager Assets] 部署。 與任何Experience Manager部署一樣，您應盡可能實施TarMK。 雖然TarMK不能擴展到單個作者實例之外，但發現它比MongoMK效能更好。 您可以添加TarMK卸載實例，以提高您的工作流處理能力 [!DNL Experience Manager Assets] 部署。

### 臨時資料夾 {#temp-folder}

要縮短資產上載時間，請為Java臨時目錄使用高效能儲存。 在Linux和Windows上，可以使用RAM驅動器或SSD。 在基於雲的環境中，可使用等效的高速儲存類型。 例如，在AmazonEC2中， [短暫驅動](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 驅動器可用於臨時資料夾。

假設伺服器具有充足的記憶體，請配置RAM驅動器。 在Linux上，運行以下命令以建立8 GB RAM驅動器：

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows OS上，使用第三方驅動程式建立RAM驅動器或僅使用高效能儲存（如SSD）。

高效能臨時卷準備好後，請設定JVM參數 `-Djava.io.tmpdir`。 例如，可以將下面的JVM參數添加到 `CQ_JVM_OPTS` 變數 `bin/start` 指令碼 [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java配置 {#java-configuration}

### Java版本 {#java-version}

Adobe建議部署 [!DNL Experience Manager Assets] 在Java 8上獲得最佳效能。

<!-- TBD: Link to the latest official word around Java.
-->

### JVM參數 {#jvm-parameters}

設定以下JVM參數：

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## 資料儲存和記憶體配置 {#data-store-and-memory-configuration}

### 檔案資料儲存配置 {#file-data-store-configuration}

建議將資料儲存與段儲存分離 [!DNL Experience Manager Assets] 。 此外，配置 `maxCachedBinarySize` 和 `cacheSizeInMB` 參數有助於最大化效能。 設定 `maxCachedBinarySize` 到快取中可保存的最小檔案大小。 指定記憶體中快取的大小，以用於內的資料儲存 `cacheSizeInMB`。 Adobe建議將此值設定為堆總大小的2-10%。 但是，負載/效能測試可以幫助確定理想的設定。

### 配置緩衝的影像快取的最大大小 {#configure-the-maximum-size-of-the-buffered-image-cache}

將大量資產上載到 [!DNL Adobe Experience Manager]，要允許記憶體消耗出現意外的峰值，並防止JVM在OutOfMemoryErrors中失敗，請減小已緩衝映像快取的已配置最大大小。 考慮一個系統具有最大堆(- `Xmx`參數)(5 GB),Oak BlobCache設定為1 GB，文檔快取設定為2 GB。 在這種情況下，緩衝的快取將最大佔用1.25 GB的記憶體和記憶體，這將僅保留0.75 GB的記憶體，以防出現意外的尖峰。

在OSGi Web控制台中配置緩衝快取大小。 在 `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`，設定屬性 `cq.dam.image.cache.max.memory` 位元組。 例如，1073741824為1 GB(1024 x 1024 x 1024 = 1 GB)。

從Experience Manager6.1 SP1，如果您使用 `sling:osgiConfig` 用於配置此屬性的節點，請確保將資料類型設定為「長」。 有關詳細資訊，請參閱 [CQBufferedImageCache在資產上載期間消耗堆](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)。

### 共用資料儲存 {#shared-data-stores}

實施S3或共用檔案資料儲存有助於在大規模實施中節省磁碟空間和增加網路吞吐量。 有關使用共用資料儲存的利弊的詳細資訊，請參見 [資產規模確定指南](/help/assets/assets-sizing-guide.md)。

### S3資料儲存 {#s-data-store}

以下S3資料儲存配置( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)幫助Adobe從現有檔案資料儲存中提取12.8 TB的二進位大對象(BLOB)到客戶站點的S3資料儲存中：

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

## 網路優化 {#network-optimization}

Adobe建議啟用HTTPS，因為許多公司都有防火牆來嗅探HTTP通信，這會對上載和損壞檔案產生不利影響。 對於大檔案上載，請確保用戶有有線連接到網路，因為WiFi網路會迅速飽和。 有關確定網路瓶頸的指導，請參見 [資產規模確定指南](/help/assets/assets-sizing-guide.md)。 要通過分析網路拓撲來評估網路效能，請參見 [資產網路注意事項](/help/assets/assets-network-considerations.md)。

主要是，您的網路優化策略取決於可用頻寬的數量和負載 [!DNL Experience Manager] 實例。 通用配置選項（包括防火牆或代理）有助於提高網路效能。 以下是需要牢記的關鍵點：

* 根據您的實例類型（小、中、大），確保您有足夠的網路頻寬用於您的Experience Manager實例。 如果 [!DNL Experience Manager] 是在AWS。
* 如果 [!DNL Experience Manager] 實例托管在AWS上，通過使用通用的擴展策略，您將受益。 如果用戶期望負載較高，請更新實例。 將其縮小到適中/低負載。
* HTTPS:大多數用戶都有防火牆來嗅探HTTP通信量，這可能會對上載檔案或在上載操作期間損壞的檔案產生負面影響。
* 大檔案上載：確保用戶有有線網路連接到網路（WiFi連接快速飽和）。

## 工作流程 {#workflows}

### 臨時工作流 {#transient-workflows}

盡可能設定 [!UICONTROL DAM更新資產] 工作流到「暫留」。 該設定大大減少了處理工作流所需的開銷，因為在這種情況下，工作流不需要通過正常的跟蹤和存檔過程。

1. 導航到 `/miscadmin` 的 [!DNL Experience Manager] 部署 `https://[aem_server]:[port]/miscadmin`。

1. 展開 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]** > **[!UICONTROL 壩]**。

1. 開啟 **[!UICONTROL DAM更新資產]**。 從浮動工具面板切換到 **[!UICONTROL 頁面]** ，然後按一下 **[!UICONTROL 頁面屬性]**。

1. 選擇 **[!UICONTROL 臨時工作流]** 按一下 **[!UICONTROL 確定]**。

   >[!NOTE]
   >
   >某些功能不支援臨時工作流。 如果 [!DNL Assets] 部署需要這些功能，不要配置臨時工作流。

在無法使用臨時工作流時，定期運行工作流清除以刪除存檔的工作流 [!UICONTROL DAM更新資產] 工作流以確保系統效能不會降低。

通常，每週執行清除工作流。 但是，在資源密集型情形中，例如在大規模資產接收期間，您可以更頻繁地執行它。

要配置工作流清除，請通過OSGi控制台添加新的Adobe花崗岩工作流清除配置。 接下來，將工作流配置為每週維護窗口的一部分並安排其時間。

如果清除操作時間過長，則超時。 因此，您應確保清除作業完成，以避免由於工作流數量過多而無法完成清除工作流的情況。

例如，在執行大量非暫時性工作流（建立工作流實例節點）後，您可以執行 [ACS公AEM域工作流刪除程式](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) 在臨時基礎上。 它會立即刪除冗餘、已完成的工作流實例，而不是等待Adobe的「花崗岩工作流清除」計畫程式運行。

### 最大並行作業數 {#maximum-parallel-jobs}

預設情況下， [!DNL Experience Manager] 運行與伺服器上處理器數量相等的最大並行作業數。 此設定的問題是，在負載較重時，所有處理器都被 [!UICONTROL DAM更新資產] 工作流，降低UI響應速度並防止 [!DNL Experience Manager] 避免運行其他保護伺服器效能和穩定性的進程。 作為一種良好的做法，通過執行以下步驟將此值設定為伺服器上可用處理器的一半：

1. 開 [!DNL Experience Manager] 作者，訪問 `https://[aem_server]:[port]/system/console/slingevent`。

1. 按一下 **[!UICONTROL 編輯]** 在與您的實現相關的每個工作流隊列上，例如 **[!UICONTROL 花崗岩瞬態工作流隊列]**。

1. 更新的值 **[!UICONTROL 最大並行作業數]** 按一下 **[!UICONTROL 保存]**。

將隊列設定為可用處理器的一半是一個可行的解決方案。 但是，您可能必須增加或減少此數量，以實現最大吞吐量並按環境進行調整。 對於臨時工作流和非臨時工作流以及其他進程（如外部工作流），有單獨的隊列。 如果多個隊列設定為50%的處理器同時處於活動狀態，則系統可以快速過載。 大量使用的隊列在用戶實施中差別很大。 因此，您可能必須仔細配置它們以實現最高效率，而不犧牲伺服器穩定性。

### DAM更新資產配置 {#dam-update-asset-configuration}

的 [!UICONTROL DAM更新資產] 工作流包含為任務配置的全套步驟，如Dynamic MediaPTIFF生成和 [!DNL Adobe InDesign Server] 整合。 但是，大多數用戶可能不需要這些步驟中的幾個步驟。 Adobe建議您建立 [!UICONTROL DAM更新資產] 工作流模型，並刪除任何不必要的步驟。 在本例中，請更新 [!UICONTROL DAM更新資產] 指向新模型。

運行 [!UICONTROL DAM更新資產] 工作流會大幅增加檔案資料儲存的大小。 通過Adobe執行的實驗結果表明，如果在8小時內執行約5500個工作流，則資料儲存大小可以增加約400 GB。

它是臨時增加，在您運行資料儲存垃圾收集任務後，資料儲存將恢復為其原始大小。

通常，資料儲存垃圾收集任務與其他計畫維護任務一起每週運行。

如果磁碟空間有限，請運行 [!UICONTROL DAM更新資產] 工作流集中，考慮更頻繁地調度垃圾收集任務。

#### 運行時格式副本生成 {#runtime-rendition-generation}

客戶在其網站上使用各種大小和格式的影像，或將其分發給業務合作夥伴。 因為每個格式副本都會增加儲存庫中資產的佔用空間，所以Adobe建議明智地使用此功能。 要減少處理和儲存影像所需的資源量，您可以在運行時生成這些影像，而不是在攝取期間作為呈現形式。

許多站點客戶實施了一個映像servlet，在請求映像時調整大小並裁剪映像，這會給發佈實例帶來額外的負載。 但是，只要可以快取這些映像，就可以緩解這一挑戰。

另一種方法是利用Dynamic Media技術完全放棄影像處理。 此外，您還可以部署Brand Portal，它不僅從 [!DNL Experience Manager] 基礎架構，還有整個發佈層。

#### 影像馬吉克 {#imagemagick}

如果自定義 [!UICONTROL DAM更新資產] 使用ImageMagick生成格式副本的工作流，Adobe建議您修改 `policy.xml` 檔案 `/etc/ImageMagick/`。 預設情況下， ImageMagick使用OS卷上的整個可用磁碟空間和可用記憶體。 在 `policymap` 部分 `policy.xml` 限制這些資源。

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

此外，在 `configure.xml` 檔案(或通過設定環境變數 `MAGICK_TEMPORARY_PATH`)到具有足夠空間和IOPS的磁碟分區。

>[!CAUTION]
>
>如果ImageMagick使用所有可用磁碟空間，錯誤配置可能會使伺服器不穩定。 使用ImageMagick處理大型檔案所需的策略更改可能會影響 [!DNL Experience Manager] 效能。 有關詳細資訊，請參見 [安裝和配置ImageMagick](/help/assets/best-practices-for-imagemagick.md)。

>[!NOTE]
>
>影像馬吉克 `policy.xml` 和 `configure.xml` 檔案可在 `/usr/lib64/ImageMagick-&#42;/config/` 而不是 `/etc/ImageMagick/`.請參見 [ImageMagick文檔](https://www.imagemagick.org/script/resources.php) 的子菜單。

如果您使用 [!DNL Experience Manager] 在Adobe托管服務(AMS)上，如果您計畫處理大量大型PSD或PSB檔案，請聯繫Adobe客戶支援。 與Adobe客戶支援代表合作，為您的AMS部署實施這些最佳做法，並為Adobe的專有格式選擇盡可能最佳的工具和型號。 [!DNL Experience Manager] 可能無法處理超過 30000 x 23000 像素的極高解析度 PSB 檔案。

### XMP寫 {#xmp-writeback}

在XMP中修改元資料時，寫回會更新原始資產 [!DNL Experience Manager]，這將導致以下結果：

* 資產本身已修改
* 將建立資產的版本
* [!UICONTROL DAM更新資產] 針對資產運行

所列結果消耗了大量資源。 因此，Adobe建議XMP在不需要寫回時禁用寫回。 有關詳細資訊，請參見 [XMP寫](/help/assets/xmp-writeback.md)。

如果選中了運行工作流標誌，則導入大量元資料XMP可能導致資源密集型寫回活動。 在精益伺服器使用期間計畫此類導入，以便不影響其他用戶的效能。

## 複製 {#replication}

在將資產複製到大量發佈實例（例如，在「站點」實施中）時，Adobe建議您使用鏈複製。 在這種情況下，作者實例複製到單個發佈實例，而該實例又複製到其他發佈實例，釋放作者實例。

### 配置鏈複製 {#configure-chain-replication}

1. 選擇要將複製連結到的發佈實例
1. 在該發佈實例上添加指向其他發佈實例的複製代理
1. 在每個複製代理上，在「觸發器」頁籤上啟用「接收時」

>[!NOTE]
>
>Adobe不建議自動激活資產。 但是，如有必要，Adobe建議將此操作作為工作流中的最後一步，通常是DAM更新資產。

## 搜索索引 {#search-indexes}

安裝 [最新的Service Pack](/help/release-notes/release-notes.md) 和與效能相關的修補程式，因為這些修補程式通常包括對系統索引的更新。 請參閱 [效能優化提示](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) 進行索引優化。

為經常運行的查詢建立自定義索引。 有關詳細資訊，請參閱 [分析慢查詢的方法](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 和 [編製自定義索引](/help/sites-deploying/queries-and-indexing.md)。 有關查詢和索引最佳做法的其他見解，請參見 [查詢和索引的最佳做法](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### Lucene索引配置 {#lucene-index-configurations}

可以對Oak索引配置進行一些優化，以幫助改進 [!DNL Experience Manager Assets] 效能。 更新索引配置以縮短重新索引時間：

1. 開啟CRXDe `/crx/de/index.jsp` 以管理用戶身份登錄。
1. 瀏覽到 `/oak:index/lucene`。
1. 添加 `String[]` 屬性 `excludedPaths` 帶值 `/var`。 `/etc/workflow/instances`, `/etc/replication`。
1. 瀏覽到 `/oak:index/damAssetLucene`。 添加 `String[]` 屬性 `includedPaths` 值 `/content/dam`。 保存更改。

如果您的用戶不需要對資產進行全文搜索，例如，在PDF文檔中搜索文本，然後將其禁用。 通過禁用全文索引，可提高索引效能。 禁用 [!DNL Apache Lucene] 文本抽取，請執行以下步驟：

1. 在 [!DNL Experience Manager] 介面，訪問 [!UICONTROL 包管理器]。
1. 上傳並安裝可用的軟體包，網址為 [disable_indexingbinarytextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip)。

### 猜測總計 {#guess-total}

建立生成大結果集的查詢時，請使用 `guessTotal` 參數，以避免在運行記憶體時佔用大量記憶體。

## 已知問題 {#known-issues}

### 大檔案 {#large-files}

中有兩個與大型檔案相關的已知問題 [!DNL Experience Manager]。 當檔案大小超過2 GB時，冷備用同步可能會出現記憶體不足的情況。 在某些情況下，它會阻止備用同步運行。 在其它情況下，它會導致主實例崩潰。 此方案適用於中的任何檔案 [!DNL Experience Manager] 大於2GB ，包括內容包。

同樣，當使用共用S3資料儲存時檔案大小達到2 GB時，檔案可能需要一段時間才能從快取完全保留到檔案系統。 因此，在使用無二進位複製時，可能在複製完成之前未保留二進位資料。 這種情況可能導致問題，特別是在資料可用性非常重要的情況下。

## 效能測試 {#performance-testing}

每 [!DNL Experience Manager] 部署，建立可快速發現和解決瓶頸的效能測試機制。 以下是需要重點關注的一些關鍵領域。

### 網路測試 {#network-testing}

對於客戶關心的所有網路效能問題，請執行以下任務：

* Test客戶網路內的網路效能
* Test網路效能。 對於AMS客戶，請與您的CSE一起從Adobe網路中test。
* Test其他接入點的網路效能
* 使用網路基準工具
* Test調度程式

### [!DNL Experience Manager] 部署測試 {#aem-deployment-testing}

要通過高效的CPU利用率和負載共用來最大限度地減少延遲並實現高吞吐量，請監控您的效能 [!DNL Experience Manager] 定期部署。 特別是：

* 對運行載入test [!DNL Experience Manager] 部署。
* 監視上載效能和UI響應。

## [!DNL Experience Manager Assets] 效能核對表和資產管理任務的影響 {#checklist}

* 啟用HTTPS繞過任何公司HTTP通信偵聽器。
* 使用有線連接進行重資產上載。
* 在Java 8上部署。
* 設定最佳JVM參數。
* 配置檔案系統資料儲存或S3資料儲存。
* 禁用子集生成。 如果啟用該功能，AEM則工作流將為多頁資產中的每頁建立單獨的資產。 這些頁中的每一頁都是一個單獨的資產，它佔用了額外的磁碟空間，需要版本控制和附加的工作流處理。 如果不需要單獨的頁面，請禁用子組生成和頁面提取活動。
* 啟用臨時工作流。
* 調整花崗岩工作流隊列以限制併發作業。
* 配置 [!DNL ImageMagick] 限制資源消耗。
* 從中刪除不必要的步驟 [!UICONTROL DAM更新資產] 工作流。
* 配置工作流和版本清除。
* 使用最新的Service Pack和修補程式優化索引。 請咨詢Adobe客戶支援，瞭解是否有其他可用的索引優化。
* 使用guessTotal優化查詢效能。
* 如果配置 [!DNL Experience Manager] 從檔案內容中檢測檔案類型(通過啟用 **[!UICONTROL 第CQ天DAM MIME類型服務]** 的 **[!UICONTROL Web控AEM制台]**)，在非高峰時段批量上載許多檔案，因為它佔用大量資源。
