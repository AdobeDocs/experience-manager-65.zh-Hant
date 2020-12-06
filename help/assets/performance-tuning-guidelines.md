---
title: 效能調整 [!DNL Assets]。
description: 關於 [!DNL Experience Manager] 配置、更改硬體、軟體和網路元件以消除瓶頸並優化 [!DNL Experience Manager Assets]效能的建議和指導。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '2744'
ht-degree: 0%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 效能調整指南  {#assets-performance-tuning-guide}

[!DNL Experience Manager Assets]設定包含許多硬體、軟體和網路元件。 根據您的部署方案，您可能需要對硬體、軟體和網路元件進行特定配置更改以消除效能瓶頸。

此外，識別並遵守某些硬體和軟體優化指南有助於建立可靠的基礎，使您的[!DNL Experience Manager Assets]部署能夠滿足對效能、可擴充性和可靠性的期望。

在[!DNL Experience Manager Assets]中效能不彰可能會影響使用者在互動式效能、資產處理、下載速度等方面的體驗。

事實上，效能最佳化是您在建立任何專案的目標量度之前所執行的基本工作。

以下是您發現並修正效能問題後，才會對使用者產生影響的特定重點領域。

## 平台 {#platform}

雖然Experience Manager在多種平台上都受到支援，但Adobe在Linux和Windows上對原生工具的支援最為強大，這有助於提供最佳效能並簡化實作。 理想情況下，您應部署64位元作業系統，以符合[!DNL Experience Manager Assets]部署的高記憶體需求。 如同任何Experience Manager部署，您應盡可能實作TarMK。 雖然TarMK無法擴展至單一作者執行個體，但其效能比MongoMK強。 您可以新增TarMK卸載例項，以提高[!DNL Experience Manager Assets]部署的工作流程處理能力。

### 臨時資料夾{#temp-folder}

若要改善資產上傳時間，請針對Java臨時目錄使用高效能的儲存空間。 在Linux和Windows上，可使用RAM驅動器或SSD。 在雲端環境中，可使用等同的高速儲存類型。 例如，在Amazon EC2中，[臨時驅動器](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)可用於臨時資料夾。

假設伺服器記憶體充足，請配置RAM驅動器。 在Linux上，運行以下命令以建立8 GB的RAM驅動器：

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows OS上，使用協力廠商驅動程式來建立RAM磁碟機，或只使用高效能的儲存空間，例如SSD。

高效能臨時卷準備就緒後，請設定JVM參數`-Djava.io.tmpdir`。 例如，您可將下面的JVM參數新增至[!DNL Experience Manager]`bin/start`指令碼中的`CQ_JVM_OPTS`變數：

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java配置{#java-configuration}

### Java版本{#java-version}

Adobe建議在Java 8上部署[!DNL Experience Manager Assets]以取得最佳效能。

<!-- TBD: Link to the latest official word around Java.
-->

### JVM參數{#jvm-parameters}

設定以下JVM參數：

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## 資料儲存和記憶體配置{#data-store-and-memory-configuration}

### 檔案資料儲存配置{#file-data-store-configuration}

建議所有[!DNL Experience Manager Assets]使用者將資料存放區與區段存放區分開。 此外，設定`maxCachedBinarySize`和`cacheSizeInMB`參數有助於將效能提升到最高。 將`maxCachedBinarySize`設定為快取中可保存的最小檔案大小。 指定`cacheSizeInMB`中用於資料儲存的記憶體快取大小。 Adobe建議您將此值設定為堆積大小總計的2-10%。 不過，負載／效能測試可協助您決定理想的設定。

### 配置緩衝映像快取的最大大小{#configure-the-maximum-size-of-the-buffered-image-cache}

當將大量資產上傳至[!DNL Adobe Experience Manager]時，為了允許記憶體使用量出現意外的尖峰，並防止JVM因OutOfMemoryErrors而失敗，請減少已設定的緩衝影像快取最大大小。 例如，您有一個系統，其最大堆積(- `Xmx`param)為5 GB,Oak BlobCache設為1 GB，檔案快取設為2 GB。 在這種情況下，緩衝快取最多需要1.25 GB的記憶體，因此，當出現意外的尖峰時，僅需0.75 GB的記憶體。

在OSGi Web Console中配置緩衝快取大小。 在`https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`處，以位元組為單位設定屬性`cq.dam.image.cache.max.memory`。 例如，1073741824是1 GB(1024 x 1024 x 1024 = 1 GB)。

在Experience Manager 6.1 SP1中，如果您使用`sling:osgiConfig`節點來設定此屬性，請務必將資料類型設定為「長」。 如需詳細資訊，請參閱[CQBufferedImageCache在資產上傳期間耗用堆](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)。

### 共用資料儲存{#shared-data-stores}

實施S3或共用檔案資料儲存有助於在大規模實施中節省磁碟空間並提高網路吞吐量。 有關使用共用資料儲存的利弊的詳細資訊，請參閱[資產調整指南](/help/assets/assets-sizing-guide.md)。

### S3資料儲存{#s-data-store}

下列S3資料存放區設定(`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)協助Adobe從現有檔案資料存放區擷取12.8 TB的二進位大型物件(BLOB)至客戶網站的S3資料存放區：

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

## 網路優化{#network-optimization}

Adobe建議啟用HTTPS，因為許多公司都有防火牆來監聽HTTP流量，這會對上傳和損毀檔案造成負面影響。 對於大型檔案上傳，請確定使用者有連線至網路，因為WiFi網路會快速飽和。 有關確定網路瓶頸的指導，請參見[資產調整指南](/help/assets/assets-sizing-guide.md)。 要通過分析網路拓撲來評估網路效能，請參見[ Assets網路注意事項](/help/assets/assets-network-considerations.md)。

主要是，您的網路優化策略取決於可用頻寬量和[!DNL Experience Manager]實例的負載。 常見配置選項（包括防火牆或代理）有助於提高網路效能。 以下是需要記住的一些要點：

* 視您的例項類型（小型、中型、大型）而定，請確定您有足夠的網路頻寬供您的Experience Manager例項使用。 如果[!DNL Experience Manager]是AWS托管的，則適當的頻寬分配尤其重要。
* 如果您的[!DNL Experience Manager]實例是在AWS上托管的，則您可以通過使用多功能擴展策略來獲益。 如果使用者預期負載較高，請調整執行個體的大小。 縮小它的大小以適中／低負載。
* HTTPS:大部分使用者都有防火牆來監聽HTTP流量，這可能會對上傳檔案或在上傳作業期間損毀檔案造成負面影響。
* 大型檔案上傳：確保用戶有到網路的有線連接（WiFi連接快速飽和）。

## 工作流程 {#workflows}

### 暫時工作流程{#transient-workflows}

盡可能將[!UICONTROL DAM更新資產]工作流程設為「暫時」。 此設定可大幅降低處理工作流程所需的開銷，因為在本例中，工作流程不需要經過一般的追蹤和封存程式。

1. 導覽至[!DNL Experience Manager]部署中`https://[aem_server]:[port]/miscadmin`的`/miscadmin`。

1. 展開&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]** > **[!UICONTROL dam]**。

1. 開啟&#x200B;**[!UICONTROL DAM更新資產]**。 從浮動工具面板切換至&#x200B;**[!UICONTROL Page]**&#x200B;標籤，然後按一下&#x200B;**[!UICONTROL Page Properties]**。

1. 選擇&#x200B;**[!UICONTROL 瞬態工作流]**&#x200B;並按一下&#x200B;**[!UICONTROL 確定]**。

   >[!NOTE]
   >
   >有些功能不支援暫時性工作流程。 如果您的[!DNL Assets]部署需要這些功能，請勿設定暫時工作流程。

在無法使用暫時工作流程的情況下，請定期執行工作流程清除，以刪除已封存的[!UICONTROL DAM更新資產]工作流程，以確保系統效能不會降低。

通常，每週執行清除工作流。 但是，在資源密集的情形中（例如在大規模資產擷取期間），您可以更頻繁地執行它。

若要設定工作流程清除，請透過OSGi主控台新增新的Adobe Granite Workflow Purge設定。 接著，設定並排程工作流程作為每週維護視窗的一部分。

如果清除過長時間，就會逾時。 因此，您應確保清除作業完成，以避免由於工作流數過多而導致清除工作流無法完成的情況。

例如，在執行許多非暫時性的工作流程（可建立工作流程例項節點）後，您就可以臨機執行[ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html)。 它會立即移除冗餘、已完成的工作流程例項，而不需等待Adobe Granite Workflow Purge排程器執行。

### 最大並行作業數{#maximum-parallel-jobs}

預設情況下， [!DNL Experience Manager]運行的並行作業數量上限等於伺服器上處理器的數量。 此設定的問題在於，在負載較重的期間，所有處理器都由[!UICONTROL DAM更新資產]工作流程佔用，降低UI回應速度，並防止[!DNL Experience Manager]執行其他保護伺服器效能和穩定性的程式。 作為一個好做法，請通過執行以下步驟將此值設定為伺服器上可用處理器的一半：

1. 在[!DNL Experience Manager]作者上，訪問`https://[aem_server]:[port]/system/console/slingevent`。

1. 在與您的實作相關的每個工作流程佇列上，按一下「**[!UICONTROL 編輯]**」，例如「Granite Transient Workflow Queue」(Granite Transient Workflow Queue)]**。**[!UICONTROL 

1. 更新&#x200B;**[!UICONTROL 最大並行作業數]**&#x200B;的值，然後按一下&#x200B;**[!UICONTROL 保存]**。

首先，將隊列設定到一半的可用處理器是一個可行的解決方案。 不過，您可能必須增加或減少此數量，才能達到最大的吞吐量，並依環境進行調整。 瞬態和非瞬態工作流程以及其他程式（例如外部工作流程）有不同的佇列。 如果多個隊列設定為50%的處理器同時處於活動狀態，則系統可以快速過載。 大量使用的佇列在使用者實作中會大不相同。 因此，您可能必須仔細配置它們，以達到最大效率，而不必犧牲伺服器穩定性。

### DAM更新資產配置{#dam-update-asset-configuration}

[!UICONTROL DAM更新資產]工作流程包含為任務配置的完整步驟套件，例如動態媒體PTIFF產生和[!DNL Adobe InDesign Server]整合。 不過，大部分使用者可能不需要其中幾個步驟。 Adobe建議您建立[!UICONTROL DAM更新資產]工作流程模型的自訂復本，並移除任何不必要的步驟。 在此情況下，請更新[!UICONTROL DAM Update Asset]的啟動器，以指向新型號。

深入執行[!UICONTROL DAM更新資產]工作流程可大幅增加檔案資料存放區的大小。 Adobe進行的實驗結果顯示，若在8小時內執行約5500個工作流程，資料存放區大小可增加約400 GB。

這是臨時增加，在運行資料儲存廢棄項目收集任務後，資料儲存將恢復為其原始大小。

通常，資料儲存廢棄項目收集任務與其他計畫維護任務一起每週運行。

如果您的磁碟空間有限，並深入執行[!UICONTROL DAM更新資產]工作流程，請考慮更頻繁地排程廢棄項目收集工作。

#### 執行時期轉譯產生{#runtime-rendition-generation}

客戶在其網站上使用各種大小和格式的影像，或將影像發佈給商業合作夥伴。 由於每個轉譯都會增加資產在儲存庫中的佔用空間，Adobe建議您審慎地使用此功能。 為了減少處理和儲存影像所需的資源量，您可以在執行時期產生這些影像，而不是在擷取時當做轉譯。

許多網站客戶會實作影像servlet，在要求影像時調整大小並裁切影像，這會對發佈例項造成額外負載。 不過，只要可以快取這些影像，挑戰就可以減輕。

另一種方法是使用動態媒體技術完全切換影像控制。 此外，您還可以部署品牌入口網站，不僅負責[!DNL Experience Manager]基礎架構的轉譯產生責任，還負責整個發佈層。

#### ImageMagick {#imagemagick}

如果您自訂[!UICONTROL DAM更新資產]工作流程，以使用ImageMagick產生轉譯，Adobe建議您修改`/etc/ImageMagick/`的`policy.xml`檔案。 預設情況下，ImageMagick使用OS卷上的整個可用磁碟空間和可用記憶體。 在`policy.xml`的`policymap`區段中進行以下配置更改以限制這些資源。

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

此外，將`configure.xml`檔案（或通過設定環境變數`MAGIC_TEMPORARY_PATH`）中ImageMagick的臨時資料夾的路徑設定為具有足夠空間和IOPS的磁碟分區。

>[!CAUTION]
>
>如果ImageMagick使用所有可用磁碟空間，錯誤配置可能會使伺服器不穩定。 使用ImageMagick處理大型檔案所需的策略更改可能會影響[!DNL Experience Manager]效能。 如需詳細資訊，請參閱[安裝及設定ImageMagick](/help/assets/best-practices-for-imagemagick.md)。

>[!NOTE]
>
>ImageMagick `policy.xml`和`configure.xml`檔案可在`/usr/lib64/ImageMagick-&#42;/config/`取代`/etc/ImageMagick/`取得。如需設定檔案的位置，請參閱[ImageMagick檔案](https://www.imagemagick.org/script/resources.php)。

如果您在Adobe Managed Services(AMS)上使用[!DNL Experience Manager]，如果您打算處理大量大型PSD或PSB檔案，請聯絡Adobe客戶服務。 與Adobe客戶服務代表合作，針對您的AMS部署實作這些最佳實務，並為Adobe的專屬格式選擇最佳的工具和模型。 [!DNL Experience Manager] 可能無法處理高解析度、超過30000 x 23000像素的PSB檔案。

### XMP回寫{#xmp-writeback}

每當在[!DNL Experience Manager]中修改中繼資料時，XMP回寫會更新原始資產，這會產生下列結果：

* 資產本身已修改
* 會建立資產的版本
* [!UICONTROL DAM更新資] 產會針對資產執行

所列結果消耗了大量資源。 因此，Adobe建議在不需要時，停用XMP回寫](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)。[

如果已勾選執行工作流程標幟，匯入大量中繼資料可能會造成資源密集的XMP回寫活動。 在精簡伺服器使用期間規劃此類匯入，以免影響其他使用者的效能。

## 複寫 {#replication}

當將資產複製至大量發佈例項（例如在Sites實作中）時，Adobe建議您使用鏈式複製。 在這種情況下，作者實例會複製到單一發佈實例，而該實例又會複製到其他發佈實例，釋放作者實例的空間。

### 配置鏈複製{#configure-chain-replication}

1. 選擇要將複製連結到
1. 在該發佈實例上添加指向其他發佈實例的複製代理
1. 在每個複製代理上，在「觸發器」頁籤上啟用「接收時」

>[!NOTE]
>
>Adobe不建議自動啟動資產。 不過，如有必要，Adobe建議您將此作為工作流程（通常是DAM更新資產）的最後步驟。

## 搜索索引{#search-indexes}

請確定您實作了最新的Service Pack和與效能相關的修補程式，因為它們通常包含系統索引的更新。 有關某些索引優化，請參見[效能調整提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

為經常運行的查詢建立自定義索引。 如需詳細資訊，請參閱[分析慢速查詢的方法](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html)和[建立自訂索引](/help/sites-deploying/queries-and-indexing.md)。 有關查詢和索引最佳實踐的其他深入資訊，請參閱[查詢和索引的最佳實踐](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### Lucene索引配置{#lucene-index-configurations}

您可對Oak索引組態進行一些最佳化，以協助改善[!DNL Experience Manager Assets]效能。 更新索引配置以縮短重新索引時間：

1. 開啟CRXDe `/crx/de/index.jsp`並以管理使用者身分登入。
1. 瀏覽至`/oak:index/lucene`。
1. 新增`String[]`屬性`excludedPaths`，其值為`/var`、`/etc/workflow/instances`和`/etc/replication`。
1. 瀏覽至`/oak:index/damAssetLucene`。 新增`String[]`屬性`includedPaths`，其值為`/content/dam`。 儲存變更。

如果您的使用者不需要對資產進行全文搜尋，例如，在PDF檔案中搜尋文字，然後停用它。 通過禁用全文索引，可以提高索引效能。 要禁用[!DNL Apache Lucene]文本抽取，請執行以下步驟：

1. 在[!DNL Experience Manager]介面中，訪問[!UICONTROL Package Manager]。
1. 上傳並安裝可在[disable_indexingbinarytextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip)取得的套件。

### 猜測總計{#guess-total}

在建立生成大結果集的查詢時，請使用`guessTotal`參數以避免運行這些查詢時佔用大量記憶體。

## 已知問題 {#known-issues}

### 大型檔案{#large-files}

[!DNL Experience Manager]中有兩個與大型檔案相關的已知問題。 當檔案大小超過2 GB時，冷備用同步可能會出現記憶體不足的情況。 在某些情況下，它會阻止備用同步運行。 在其他情況下，會造成主要例項當機。 此案例適用於[!DNL Experience Manager]中大於2GB的任何檔案，包括內容封裝。

同樣地，當檔案在使用共用S3資料儲存時達到2 GB大小時，檔案從快取完全保存到檔案系統可能需要一些時間。 因此，在使用無二進位複製時，可能在複製完成之前無法保存二進位資料。 這種情況可能會導致問題，尤其是當資料的可用性很重要時。

## 效能測試{#performance-testing}

針對每個[!DNL Experience Manager]部署，建立可快速識別並解決瓶頸的效能測試機制。 以下是需要重點討論的一些關鍵領域。

### 網路測試{#network-testing}

對於客戶對網路效能的所有顧慮，請執行以下任務：

* 從客戶網路測試網路效能
* 從Adobe網路測試網路效能。 對於AMS客戶，請與您的CSE合作，在Adobe網路中進行測試。
* 從另一個接入點測試網路效能
* 使用網路基準工具
* 對調度程式進行測試

### [!DNL Experience Manager] 部署測試  {#aem-deployment-testing}

為了透過有效的CPU使用率和負載分享功能，將延遲降至最低並實現高吞吐量，請定期監控[!DNL Experience Manager]部署的效能。 尤其是：

* 對[!DNL Experience Manager]部署執行負載測試。
* 監控上傳效能和UI回應速度。

## [!DNL Experience Manager Assets] 績效檢查表和資產管理任務的影響  {#checklist}

* 讓HTTPS繞過任何公司HTTP流量Sniffer。
* 使用有線連線上傳大量資產。
* 部署在Java 8。
* 設定最佳JVM參數。
* 配置檔案系統資料儲存或S3資料儲存。
* 停用子資產產生。 如果已啟用，AEM的工作流程會針對多頁資產中的每個頁面建立個別的資產。 這些頁面都是個別資產，會佔用額外的磁碟空間、需要版本修訂以及額外的工作流程處理。 如果您不需要個別頁面，請停用子資產產生和頁面擷取活動。
* 啟用暫時性工作流程。
* 調整Granite工作流程佇列以限制併發工作。
* 配置[!DNL ImageMagick]以限制資源消耗。
* 從[!UICONTROL DAM更新資產]工作流程移除不必要的步驟。
* 設定工作流程和版本清除。
* 使用最新的Service Pack和修補程式來最佳化索引。 請洽詢Adobe客戶服務，以取得其他可用的索引最佳化。
* 使用guessTotal來最佳化查詢效能。
* 如果您設定[!DNL Experience Manager]以從檔案內容偵測檔案類型（在&#x200B;**[!UICONTROL AEM Web Console]**&#x200B;中啟用&#x200B;**[!UICONTROL Day CQ DAM Mime Type Service]**），請在非尖峰時段大量上傳許多檔案，因為它耗用大量資源。
