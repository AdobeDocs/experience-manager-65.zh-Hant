---
title: 資產效能調整指南
description: 有關AEM設定、變更硬體、軟體和網路元件以排除瓶頸並最佳化AEM Assets效能的建議和指引。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


<!-- TBD: Formatting using backticks. Add UICONTROL tag. Redundant info as reviewed by engineering. -->

# 資產效能調整指南 {#assets-performance-tuning-guide}

Adobe Experience Manager(AEM)資產設定包含許多硬體、軟體和網路元件。 根據您的部署方案，您可能需要對硬體、軟體和網路元件進行特定配置更改以消除效能瓶頸。

此外，識別並遵守特定硬體和軟體最佳化准則，有助於建立健全的基礎，讓您的AEM Assets部署符合效能、延展性和可靠性的期望。

AEM Assets的效能不佳可能會影響使用者在互動式效能、資產處理、下載速度和其他方面的使用體驗。

事實上，效能最佳化是您在建立任何專案的目標量度之前所執行的基本工作。

以下是您發現並修正效能問題後，才會對使用者產生影響的特定重點領域。

## 平台 {#platform}

雖然AEM在許多平台上都受支援，但Adobe在Linux和Windows上對原生工具的支援最多，這有助於提供最佳效能並簡化實施。 最理想的情況是，您應部署64位元作業系統，以符合AEM Assets部署的高記憶體需求。 如同任何AEM部署，您應盡可能實作TarMK。 雖然TarMK無法擴展至單一作者執行個體，但其效能比MongoMK強。 您可以新增TarMK卸載例項，以提高AEM Assets部署的工作流程處理能力。

### 臨時資料夾 {#temp-folder}

若要改善資產上傳時間，請針對Java臨時目錄使用高效能的儲存空間。 在Linux和Windows上，可使用RAM驅動器或SSD。 在雲端環境中，可使用等同的高速儲存類型。 例如，在Amazon EC2中， [臨時資料夾可](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 以使用「臨時驅動器」。

假設伺服器記憶體充足，請配置RAM驅動器。 在Linux上，運行以下命令以建立8 GB的RAM驅動器：

```
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows OS上，使用協力廠商驅動程式來建立RAM磁碟機，或只使用高效能的儲存空間，例如SSD。

高效能臨時卷準備就緒後，請設定JVM參數 `-Djava.io.tmpdir`。 例如，您可將下方的JVM參數新增至AEM `CQ_JVM_OPTS` 指令碼 `bin/start` 中的變數：

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java配置 {#java-configuration}

### Java版本 {#java-version}

Adobe建議將AEM Assets部署在Java 8上，以獲得最佳效能。

>[!NOTE]
>
>Oracle自2015年4月起停止發佈Java 7的更新。

### JVM參數 {#jvm-parameters}

您應設定下列JVM參數：

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## 資料儲存和記憶體配置 {#data-store-and-memory-configuration}

### 檔案資料儲存區組態 {#file-data-store-configuration}

建議所有AEM Assets使用者將資料存放區與區段存放區分開。 此外，設定和參 `maxCachedBinarySize` 數可 `cacheSizeInMB` 協助發揮最大效能。 設 `maxCachedBinarySize` 置為可保存在快取中的最小檔案大小。 指定記憶體中快取的大小，以用於內的資料儲存 `cacheSizeInMB`。 Adobe建議您將此值設定為堆積大小總計的2-10%。 不過，負載／效能測試可協助您決定理想的設定。

### 配置緩衝映像快取的最大大小 {#configure-the-maximum-size-of-the-buffered-image-cache}

當將大量資產上傳至Adobe Experience Manager時，為了允許記憶體使用量出現意外的尖峰，並防止JVM因OutOfMemoryErrors而失敗，請減少已設定的緩衝影像快取最大大小。 例如，您有一個系統的堆積(- `Xmx`param)上限為5 GB,Oak BlobCache設為1 GB，檔案快取設為2 GB。 在這種情況下，緩衝快取最多需要1.25 GB的記憶體，因此，當出現意外的尖峰時，僅需0.75 GB的記憶體。

在OSGi Web Console中配置緩衝快取大小。 在 `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`，以位元組為單 `cq.dam.image.cache.max.memory` 位設定屬性。 例如，1073741824是1 GB(1024 x 1024 x 1024 = 1 GB)。

在AEM 6.1 SP1中，如果您使用節點來設 `sling:osgiConfig` 定此屬性，請務必將資料類型設定為「長」。 如需詳細資訊，請參 [閱CQBufferedImageCache在資產上傳期間耗用堆](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)。

### 共用資料儲存區 {#shared-data-stores}

實施S3或共用檔案資料儲存有助於在大規模實施中節省磁碟空間並提高網路吞吐量。 如需使用共用資料儲存區的利弊資訊，請參閱資產 [調整指南](/help/assets/assets-sizing-guide.md)。

### S3 data store {#s-data-store}

下列S3資料存放區設定( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)協助Adobe從現有檔案資料存放區擷取12.8 TB的二進位大型物件(BLOB)至客戶網站的S3資料存放區：

```
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

Adobe建議啟用HTTPS，因為許多公司都有防火牆來監聽HTTP流量，這會對上傳和損毀檔案造成負面影響。 對於大型檔案上傳，請確定使用者有連線至網路，因為WiFi網路會快速飽和。 有關確定網路瓶頸的指導，請參 [閱資產規模指南](/help/assets/assets-sizing-guide.md)。 要通過分析網路拓撲來評估網路效能，請參 [閱Assets Network Considerations](/help/assets/assets-network-considerations.md)。

您的網路最佳化策略主要取決於可用頻寬的數量，以及AEM例項的負載。 常見配置選項（包括防火牆或代理）有助於提高網路效能。 以下是需要記住的一些要點：

* 視您的例項類型（小型、中度、大型）而定，請確定您的AEM例項有足夠的網路頻寬。 如果AEM是在AWS上代管，則適當的頻寬分配尤為重要。
* 如果您的AEM實例是在AWS上代管的，則您可以擁有多功能擴展策略。 如果使用者預期負載較高，請調整執行個體的大小。 縮小它的大小以適中／低負載。
* HTTPS:大部分使用者都有防火牆來監聽HTTP流量，這可能會對上傳檔案或在上傳作業期間損毀檔案造成負面影響。
* 大型檔案上傳：確保用戶有到網路的有線連接（WiFi連接快速飽和）。

## 工作流程 {#workflows}

### 瞬態工作流程 {#transient-workflows}

盡可能將「DAM更新資產」工作流程設為「暫時」。 此設定可大幅降低處理工作流程所需的開銷，因為在本例中，工作流程不需要經過一般的追蹤和封存程式。

>[!NOTE]
>
>依預設，DAM更新資產工作流程會在AEM 6.3中設為「暫時」。在這種情況下，您可以略過以下過程。

1. 導覽至 `/miscadmin` AEM例項中，網址為 `https://[aem_server]:[port]/miscadmin`。
1. 展開「 **[!UICONTROL 工具]** >工 **[!UICONTROL 作流程]** > **[!UICONTROL 模型]** > **** dam」。
1. 開啟 **[!UICONTROL DAM更新資產]**。 從浮動工具面板切換至「頁面」索 **[!UICONTROL 引標籤]** ，然後按一下「 **[!UICONTROL 頁面屬性」]**。
1. 選擇「 **[!UICONTROL 暫時工作流]** 」，然後按一下「 **[!UICONTROL 確定」]**。

   >[!NOTE]
   >
   >有些功能不支援暫時性工作流程。 如果您的AEM Assets部署需要這些功能，請勿設定暫時工作流程。

在無法使用暫時性工作流程的情況下，請定期執行工作流程清除，以刪除封存的DAM更新資產工作流程，以確保系統效能不會降低。

通常，每週執行清除工作流。 但是，在資源密集的情形中（例如在大規模資產擷取期間），您可以更頻繁地執行它。

若要設定工作流程清除，請透過OSGi主控台新增新的Adobe Granite Workflow Purge設定。 接著，設定並排程工作流程作為每週維護視窗的一部分。

如果清除過長時間，就會逾時。 因此，您應確保清除作業完成，以避免由於工作流數過多而導致清除工作流無法完成的情況。

例如，在執行許多非暫時性的工作流程（可建立工作流程例項節點）後，您就可以在臨機基礎上執行 [ACS AEM Commons Workflow Refler](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) 。 它會立即移除冗餘、已完成的工作流程例項，而不需等待Adobe Granite Workflow Purge排程器執行。

### 最大並行作業數 {#maximum-parallel-jobs}

依預設，AEM會執行與伺服器上處理器數目相等的最大並行作業數。 此設定的問題在於，在負載較重的期間，所有處理器都會被DAM更新資產工作流程佔用，降低UI回應速度，並防止AEM執行其他可保障伺服器效能與穩定性的程式。 作為一個好做法，請通過執行以下步驟將此值設定為伺服器上可用處理器的一半：

1. 在「AEM作者」上，請至 `https://[aem_server]:[port]/system/console/slingevent`。
1. 按一 **[!UICONTROL 下與您的實作相關的每個工作流程佇列(例如]** Granite Transient Workflow Queue)上的「編輯」 ****。
1. 更新「最大並行作 **[!UICONTROL 業數」的值]** ，然後按一下「 **[!UICONTROL 保存」]**。

首先，將隊列設定到一半的可用處理器是一個可行的解決方案。 不過，您可能必須增加或減少此數量，才能達到最大的吞吐量，並依環境進行調整。 瞬態和非瞬態工作流程以及其他程式（例如外部工作流程）有不同的佇列。 如果多個隊列設定為50%的處理器同時處於活動狀態，則系統可以快速過載。 大量使用的佇列在使用者實作中會大不相同。 因此，您可能必須仔細配置它們，以達到最大效率，而不必犧牲伺服器穩定性。

### DAM更新資產設定 {#dam-update-asset-configuration}

DAM更新資產工作流程包含為工作設定的完整步驟套件，例如產生Scene7 PTIFF和InDesign server整合。 不過，大部分使用者可能不需要其中幾個步驟。 Adobe建議您建立DAM更新資產工作流程模型的自訂復本，並移除任何不必要的步驟。 在此情況下，請更新DAM更新資產的啟動器，以指向新模型。

深入執行DAM更新資產工作流程可大幅增加檔案資料存放區的大小。 Adobe進行的實驗結果顯示，如果在8小時內執行約5500個工作流程，資料存放區大小可增加約400 GB。

這是臨時增加，在運行資料儲存廢棄項目收集任務後，資料儲存將恢復為其原始大小。

通常，資料儲存廢棄項目收集任務與其他計畫維護任務一起每週運行。

如果您有有限的磁碟空間並密集執行DAM更新資產工作流程，請考慮更頻繁地排程廢棄項目收集工作。

#### 產生執行時期轉譯 {#runtime-rendition-generation}

客戶在其網站上使用各種大小和格式的影像，或將影像發佈給商業合作夥伴。 由於每個轉譯都會增加資產在儲存庫中的佔用空間，Adobe建議您審慎地使用此功能。 為了減少處理和儲存影像所需的資源量，您可以在執行時期產生這些影像，而不是在擷取時當做轉譯。

許多網站客戶會實作影像servlet，在要求影像時調整影像大小並裁切影像，這會對發佈例項造成額外負載。 不過，只要可以快取這些影像，挑戰就可以減輕。

另一種方法是使用Scene7技術完全放棄影像控制。 此外，您還可以部署品牌入口網站，不僅負責從AEM基礎架構接手轉譯產生責任，還負責整個發佈層。

#### ImageMagick {#imagemagick}

如果您自訂「DAM更新資產」工作流程，以使用ImageMagick產生轉譯，Adobe建議您在 `policy.xml` 修改檔 `/etc/ImageMagick/`案。 預設情況下，ImageMagick使用OS卷上的整個可用磁碟空間和可用記憶體。 在的部分中進行以下配 `policymap` 置更改 `policy.xml` 以限制這些資源。

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

此外，將檔案中ImageMagick的臨時資料夾的路徑(或通過設定環境變數 `configure.xml``MAGIC_TEMPORARY_PATH`)設定為具有足夠空間和IOPS的磁碟分區。

>[!CAUTION]
>
>如果ImageMagick使用所有可用磁碟空間，錯誤配置可能會使伺服器不穩定。
>
>使用ImageMagick處理大型檔案所需的原則變更可能會影響AEM效能。 如需詳細資訊，請參 [閱安裝和設定ImageMagick](/help/assets/best-practices-for-imagemagick.md)。

>[!NOTE]
>
>ImageMagick和 `policy.xml` 檔案可在中取 `configure.xml` 代。請參 `/usr/lib64/ImageMagick-&#42;/config/` 閱 `/etc/ImageMagick/`ImageMagick文檔 [](https://www.imagemagick.org/script/resources.php) ，瞭解配置檔案的位置。

>[!TIP]
>
>如果您在Adobe Managed Services(AMS)上使用Experience Manager，如果您打算處理大量大型PSD或PSB檔案，請聯絡Adobe支援。 與Adobe客戶服務代表合作，針對您的AMS部署實作這些最佳實務，並為Adobe的專屬格式選擇最佳的工具和模型。

### XMP writeback {#xmp-writeback}

每當在AEM中修改中繼資料時，XMP回寫會更新原始資產，這會產生下列結果：

* 資產本身已修改
* 會建立資產的版本
* DAM更新資產會針對資產執行

所列結果消耗了大量資源。 因此，Adobe建議 [停用XMP回寫](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)（如果不需要）。

如果已勾選執行工作流程標幟，匯入大量中繼資料可能會造成資源密集的XMP回寫活動。 在精簡伺服器使用期間規劃此類匯入，以免影響其他使用者的效能。

## 複寫 {#replication}

當將資產複製至大量發佈例項（例如在Sites實作中）時，Adobe建議您使用鏈式複製。 在這種情況下，作者實例會複製到單一發佈實例，而該實例又會複製到其他發佈實例，釋放作者實例的空間。

### 配置鏈複製 {#configure-chain-replication}

1. 選擇要將複製連結到
1. 在該發佈實例上添加指向其他發佈實例的複製代理
1. 在每個複製代理上，在「觸發器」頁籤上啟用「接收時」

>[!NOTE]
>
>Adobe不建議自動啟動資產。 不過，如有必要，Adobe建議您將此作為工作流程（通常是DAM更新資產）的最後步驟。

## 搜尋索引 {#search-indexes}

請確定您實作了最新的Service pack和與效能相關的修補程式，因為它們通常包含系統索引的更新。 請參 [閱某些索引最佳化的](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 「效能調整提示」。

為經常運行的查詢建立自定義索引。 如需詳細資訊，請參 [閱分析慢速查詢和建立自訂索引](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html)[的方法](/help/sites-deploying/queries-and-indexing.md)。 如需查詢和索引最佳實務的其他深入資訊，請參 [閱查詢和索引最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### Lucene索引配置 {#lucene-index-configurations}

您可對Oak索引設定進行一些最佳化，以協助改善AEM Assets效能。 更新索引配置以縮短重新索引時間：

1. 開啟CRXDe `/crx/de/index.jsp` 並以管理使用者身分登入
1. 瀏覽至 `/oak:index/lucene`
1. 新增String[] 屬性 `excludedPaths` 及值 `/var`、 `/etc/workflow/instances`和 `/etc/replication`。
1. 瀏覽至 `/oak:index/damAssetLucene`。 新增具 `String[]` 有值 `includedPaths` 的屬性 `/content/dam`。
1. 儲存.

（僅限AEM6.1和6.2）更新ntBaseLucene索引以改善資產刪除和移動效能：

1. 瀏覽至 `/oak:index/ntBaseLucene/indexRules/nt:base/properties`
1. 添加兩個nt：非結構化節點 `slingResource` 並在 `damResolvedPath` 下 `/oak:index/ntBaseLucene/indexRules/nt:base/properties`
1. 在節點上設定以下屬性(其 `ordered` 中 `propertyIndex` 和屬性類型為 `Boolean`:

   ```
   slingResource
   name="sling:resource"
   ordered=false
   propertyIndex= true
   type="String"
   damResolvedPath
   name="dam:resolvedPath"
   ordered=false
   propertyIndex=true
   type="String"
   ```

1. 在節 `/oak:index/ntBaseLucene` 點上，設定屬性 `reindex=true`。 按一下「 **[!UICONTROL 全部儲存]**」。
1. 監視error.log以查看索引完成時間：已完成索引的重新索引： [/oak:index/ntBaseLucene]
1. 您也可以看到，在CRXDe中重新整理/oak:index/ntBaseLucene節點，因為reindex屬性會返回false，所以已完成索引
1. 索引完成後，返回CRXDe並將這兩個索引上的&quot;type&quot;屬性設定為disabled

   * */oak:index/slingResource*
   * */oak:index/damResolvedPath*

1. 按一下「全部儲存」

禁用Lucene文本提取：

如果您的使用者不需要搜尋資產內容（例如搜尋PDF檔案中的文字），則您可以停用此功能來改善索引效能。

1. 前往AEM套件管理員/crx/packmgr/index.jsp
1. 上傳並安裝下方的套件

[取得檔案](assets/disable_indexingbinarytextextraction-10.zip)

### 猜測總計 {#guess-total}

建立生成大結果集的查詢時，請使用參 `guessTotal` 數來避免在運行時佔用大量記憶體。

## 已知問題 {#known-issues}

### 大型檔案 {#large-files}

AEM中有兩個與大型檔案相關的主要已知問題。 當檔案大小超過2 GB時，冷備用同步可能會出現記憶體不足的情況。 在某些情況下，它會阻止備用同步運行。 在其他情況下，會造成主要例項當機。 此案例適用於AEM中大於2GB的任何檔案，包括內容套件。

同樣地，當使用共用S3資料儲存區時檔案大小達到2 GB時，檔案從快取完全保存到檔案系統可能需要一些時間。 因此，在使用無二進位複製時，可能在複製完成之前無法保存二進位資料。 這種情況可能會導致問題，尤其是當資料的可用性很重要時。

## 效能測試 {#performance-testing}

針對每個AEM部署，建立效能測試制度，以快速找出並解決瓶頸。 以下是需要重點討論的一些關鍵領域。

### 網路測試 {#network-testing}

對於客戶對網路效能的所有顧慮，請執行以下任務：

* 從客戶網路測試網路效能
* 從Adobe網路測試網路效能。 對於AMS客戶，請與您的CSE合作，在Adobe網路中進行測試。
* 從另一個接入點測試網路效能
* 使用網路基準工具
* 對調度程式進行測試

### AEM例項測試 {#aem-instance-testing}

若要透過有效的CPU使用率和負載分享，將延遲降至最低並達到高吞吐量，請定期監控AEM執行個體的效能。 特別是：

* 針對AEM例項執行載入測試
* 監控上傳效能和UI回應速度

## AEM Assets績效檢查清單及資產管理工作的影響 {#checklist}

* 讓HTTPS繞過任何公司HTTP流量Sniffer
* 使用有線連線上傳大量資產
* 部署在Java 8。
* 設定最佳JVM參數
* 配置檔案系統資料儲存或S3資料儲存
* 啟用暫時工作流程
* 調整Granite工作流程佇列以限制併發工作
* 配置ImageMagick以限制資源消耗
* 從「DAM更新資產」工作流程移除不必要的步驟
* 配置工作流和版本清除
* 使用最新的Service pack和修補程式來最佳化索引。 請洽詢Adobe支援，以取得任何其他可用的索引最佳化。
* 使用guessTotal來最佳化查詢效能。
* 如果您設定AEM以從檔案內容偵測檔案類型(在 **[!UICONTROL AEM Web Console中啟用]** Day CQ DAM Mime Type Service ****)，請在非尖峰時段大量上傳許多檔案，因為它耗用大量資源。
