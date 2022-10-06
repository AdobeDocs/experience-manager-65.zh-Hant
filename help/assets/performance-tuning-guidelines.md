---
title: 效能調整 [!DNL Assets].
description: 關於 [!DNL Experience Manager] 配置、對硬體、軟體和網路元件的更改，以消除瓶頸並優化 [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 效能調整指南 {#assets-performance-tuning-guide}

安 [!DNL Experience Manager Assets] 安裝程式包含許多硬體、軟體和網路元件。 根據您的部署方案，您可能需要對硬體、軟體和網路元件進行特定配置更改，以消除效能瓶頸。

此外，識別並遵守某些硬體和軟體優化指南有助於建立良好的基礎，使您的 [!DNL Experience Manager Assets] 部署以滿足效能、可擴充性和可靠性方面的期望。

在 [!DNL Experience Manager Assets] 可能會影響互動式效能、資產處理、下載速度等方面的使用者體驗。

事實上，效能最佳化是您在為任何專案建立目標量度之前所執行的基本任務。

以下是您可在發現效能問題並修正其後，再對使用者造成影響的關鍵重點區域。

## 平台 {#platform}

雖然Experience Manager在多種平台上受支援，但Adobe在Linux和Windows上對本機工具的支援最強，這有助於實現最佳效能和易於實施。 理想情況下，您應部署64位作業系統，以滿足 [!DNL Experience Manager Assets] 部署。 如同任何Experience Manager部署，您應盡可能實作TarMK。 雖然TarMK無法擴展至單一製作例項以外，但其執行效能比MongoMK好。 您可以新增TarMK卸載例項，以提升您的工作流程處理能力 [!DNL Experience Manager Assets] 部署。

### 臨時資料夾 {#temp-folder}

若要改善資產上傳時間，請對Java臨時目錄使用高效能儲存。 在Linux和Windows上，可使用RAM驅動器或SSD。 在基於雲的環境中，可以使用等效的高速儲存類型。 例如，在Amazon EC2中， [短暫的行駛](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 驅動器可用於臨時資料夾。

假設伺服器有足夠的記憶體，請配置RAM驅動器。 在Linux上，運行以下命令以建立8 GB RAM驅動器：

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows OS上，使用第三方驅動程式建立RAM驅動器，或僅使用高效能儲存（如SSD）。

在高效能臨時卷準備就緒後，設定JVM參數 `-Djava.io.tmpdir`. 例如，您可以將下方的JVM參數新增至 `CQ_JVM_OPTS` 變數 `bin/start` 指令碼 [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java配置 {#java-configuration}

### Java版本 {#java-version}

Adobe建議部署 [!DNL Experience Manager Assets] 在Java 8上以獲得最佳效能。

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

建議將資料存放區與區段存放區分開， [!DNL Experience Manager Assets] 使用者。 此外，設定 `maxCachedBinarySize` 和 `cacheSizeInMB` 參數可協助最大化效能。 設定 `maxCachedBinarySize` 到快取中可保留的最小檔案大小。 指定要用於內資料儲存的記憶體內快取的大小 `cacheSizeInMB`. Adobe建議您將此值設定為堆大小總計的2-10%之間。 不過，負載/效能測試有助於確定理想的設定。

### 配置緩衝映像快取的最大大小 {#configure-the-maximum-size-of-the-buffered-image-cache}

將大量資產上傳至 [!DNL Adobe Experience Manager]，若要允許記憶體耗用量出現非預期的尖峰，並防止JVM因OutOfMemoryErrors而失敗，請減少已設定的緩衝影像快取的最大大小。 假設您有一個系統具有最大堆(- `Xmx`參數)(5 GB)、Oak BlobCache設定為1 GB，檔案快取設定為2 GB。 在這種情況下，緩衝快取最多需要1.25 GB和記憶體，這將僅留下0.75 GB記憶體，以備意外的尖峰。

在OSGi Web控制台中配置緩衝快取大小。 At `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`，請設定屬性 `cq.dam.image.cache.max.memory` 位元組。 例如，1073741824為1 GB(1024 x 1024 x 1024 = 1 GB)。

從Experience Manager6.1 SP1，如果您使用 `sling:osgiConfig` 用於配置此屬性的節點，請確保將資料類型設定為Long。 如需詳細資訊，請參閱 [CQBufferedImageCache在資產上傳期間取用堆](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### 共用資料儲存 {#shared-data-stores}

實作S3或共用檔案資料存放區有助於在大規模實作中節省磁碟空間並增加網路吞吐量。 如需使用共用資料存放區的優點和缺點的詳細資訊，請參閱 [資產規模調整指南](/help/assets/assets-sizing-guide.md).

### S3資料儲存 {#s-data-store}

以下S3資料儲存配置( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)幫助Adobe從現有檔案資料儲存區提取12.8 TB的二進位大型物件(BLOB)至客戶網站的S3資料儲存區：

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

Adobe建議啟用HTTPS，因為許多公司都有可偵聽HTTP流量的防火牆，這會對上傳和損毀檔案造成負面影響。 對於大型檔案上傳，請確保用戶有有線連接到網路，因為WiFi網路很快就飽和了。 有關確定網路瓶頸的指南，請參見 [資產規模調整指南](/help/assets/assets-sizing-guide.md). 要通過分析網路拓撲來評估網路效能，請參見 [資產網路考量事項](/help/assets/assets-network-considerations.md).

主要取決於可用頻寬的數量和負載 [!DNL Experience Manager] 例項。 常見的配置選項（包括防火牆或代理）有助於提高網路效能。 請謹記以下幾點：

* 根據您的執行個體類型（小、中、大），請確保您擁有足夠的網路頻寬供您的Experience Manager執行個體使用。 如果 [!DNL Experience Manager] 托管於AWS。
* 若您的 [!DNL Experience Manager] 例項托管於AWS上，您可透過通用的擴充政策受益。 如果使用者預期會有高負載，請更新執行個體。 縮減其大小以適度/低負載。
* HTTPS:大部分的使用者都有可偵聽HTTP流量的防火牆，這可能會對上傳檔案或在上傳作業期間損毀的檔案造成負面影響。
* 大檔案上載：確保用戶有到網路的有線連接（WiFi連接快速飽和）。

## 工作流程 {#workflows}

### 暫時性工作流程 {#transient-workflows}

盡可能設定 [!UICONTROL DAM更新資產] 工作流程至暫時。 此設定可大幅降低處理工作流程所需的開銷，因為在此情況下，工作流程不需要通過正常的追蹤和封存流程。

1. 導覽至 `/miscadmin` 在 [!DNL Experience Manager] 部署 `https://[aem_server]:[port]/miscadmin`.

1. 展開 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]** > **[!UICONTROL 壩]**.

1. 開啟 **[!UICONTROL DAM更新資產]**. 從浮動工具面板，切換至 **[!UICONTROL 頁面]** ，然後按一下 **[!UICONTROL 頁面屬性]**.

1. 選擇 **[!UICONTROL 暫時性工作流程]** 按一下 **[!UICONTROL 確定]**.

   >[!NOTE]
   >
   >有些功能不支援暫時性工作流程。 若您的 [!DNL Assets] 部署需要這些功能，請勿配置暫時性工作流程。

如果無法使用暫時性工作流程，請定期執行工作流程清除以刪除已封存的 [!UICONTROL DAM更新資產] 確保系統效能不會降低的工作流程。

通常每週執行清除工作流程。 不過，在資源密集型情況（例如在大規模資產擷取期間）中，您可以更頻繁地執行它。

若要設定工作流程清除，請透過OSGi主控台新增「AdobeGranite工作流程清除」設定。 接下來，在每週維護窗口中配置並計畫工作流。

如果清除執行時間太長，就會逾時。 因此，您應確保清除作業完成，以避免因工作流程數量過多而導致清除工作流程無法完成的情況。

例如，執行許多非暫時性工作流程後（會建立工作流程例項節點），您可以執行 [ACS AEM Commons工作流程移除器](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) 臨機。 它會立即移除冗餘、已完成的工作流程例項，而非等待AdobeGranite工作流程清除排程器執行。

### 最大並行作業數 {#maximum-parallel-jobs}

依預設， [!DNL Experience Manager] 運行的最大並行作業數等於伺服器上的處理器數。 此設定的問題在於，在負載過重時，所有處理器都被佔用 [!UICONTROL DAM更新資產] 工作流程，減緩UI回應速度並防止 [!DNL Experience Manager] 運行其他保護伺服器效能和穩定性的進程。 作為一個良好做法，請執行以下步驟，將此值設定為伺服器上可用處理器的一半：

1. 開啟 [!DNL Experience Manager] 作者，存取 `https://[aem_server]:[port]/system/console/slingevent`.

1. 按一下 **[!UICONTROL 編輯]** 例如， **[!UICONTROL Granite暫時工作流程佇列]**.

1. 更新 **[!UICONTROL 最大並行作業數]** 按一下 **[!UICONTROL 儲存]**.

將隊列設定為可用處理器的一半是一個可行的解決方案。 但是，您可能必須增加或減少此數量，以實現最大吞吐量，並按環境調整。 暫時和非暫時性工作流程以及其他程式（例如外部工作流程）有不同的佇列。 如果設定為50%的處理器同時處於活動狀態的多個隊列，則系統可以快速超載。 大量使用的佇列在不同使用者實施中大不相同。 因此，您可能必須仔細配置它們，以實現最高效率，而不犧牲伺服器穩定性。

### DAM更新資產設定 {#dam-update-asset-configuration}

此 [!UICONTROL DAM更新資產] 工作流程包含為工作設定的完整步驟套裝，例如Dynamic Media PTIFF產生和 [!DNL Adobe InDesign Server] 整合。 不過，大部分使用者可能不需要執行其中幾個步驟。 Adobe建議您建立 [!UICONTROL DAM更新資產] 工作流程模型，並移除任何不必要的步驟。 在此情況下，請更新 [!UICONTROL DAM更新資產] 指向新模型。

執行 [!UICONTROL DAM更新資產] 工作流程可大幅增加檔案資料存放區的大小。 由Adobe進行的實驗結果表明，如果在8小時內執行約5500個工作流程，則資料存放區大小可增加約400 GB。

這是臨時增加，在運行資料儲存垃圾收集任務後，資料儲存被還原為原始大小。

通常，資料存放區垃圾收集任務與其他計畫維護任務一起每週運行。

如果磁碟空間有限，則運行 [!UICONTROL DAM更新資產] 集中工作流程，考慮更頻繁地安排垃圾收集任務。

#### 生成運行時格式副本 {#runtime-rendition-generation}

客戶在其網站上使用各種大小和格式的影像，或用於分發給業務合作夥伴。 由於每個轉譯都會增加儲存庫中資產的空間，因此Adobe建議審慎使用此功能。 若要減少處理和儲存影像所需的資源量，您可以在執行階段產生這些影像，而非在擷取期間以轉譯的形式產生。

許多Sites客戶會實作影像servlet，在要求影像時調整大小並裁切影像，這會對發佈例項造成額外負載。 不過，只要可快取這些影像，就可緩解挑戰。

另一種方法是使用Dynamic Media技術完全切換影像處理。 此外，您可以部署Brand Portal，不僅可接管 [!DNL Experience Manager] 基礎架構，也包括整個發佈層級。

#### ImageMagick {#imagemagick}

如果您自訂 [!UICONTROL DAM更新資產] 使用ImageMagick產生轉譯的工作流程，Adobe建議您修改 `policy.xml` 檔案位置 `/etc/ImageMagick/`. 預設情況下，ImageMagick會使用作業系統卷上的整個可用磁碟空間和可用記憶體。 在 `policymap` 區段 `policy.xml` 來限制這些資源。

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

此外，在 `configure.xml` 檔案（或設定環境變數） `MAGICK_TEMPORARY_PATH`)到具有足夠空間和IOPS的磁碟分區。

>[!CAUTION]
>
>如果ImageMagick使用所有可用磁碟空間，配置錯誤可能會使伺服器不穩定。 使用ImageMagick處理大型檔案所需的策略更改可能會影響 [!DNL Experience Manager] 效能。 如需詳細資訊，請參閱 [安裝和配置ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` 和 `configure.xml` 檔案可在 `/usr/lib64/ImageMagick-&#42;/config/` 而非 `/etc/ImageMagick/`。請參閱 [ImageMagick檔案](https://www.imagemagick.org/script/resources.php) ，以了解設定檔的位置。

如果您使用 [!DNL Experience Manager] 如果您打算處理大量大型PSD或PSB檔案，請在Adobe Managed Services(AMS)上聯絡Adobe客戶支援。 與Adobe客戶支援代表合作，為您的AMS部署實作這些最佳實務，並為Adobe的專屬格式選擇最佳的工具和模型。 [!DNL Experience Manager] 可能無法處理超過30000 x 23000像素的高解析度PSB檔案。

### XMP回寫 {#xmp-writeback}

XMP回寫會在中修改中繼資料時更新原始資產 [!DNL Experience Manager]，會產生下列結果：

* 資產本身已修改
* 資產的版本已建立
* [!UICONTROL DAM更新資產] 針對資產執行

所列結果消耗了大量資源。 因此，Adobe建議在不需要時停用XMP回寫。 如需詳細資訊，請參閱 [XMP回寫](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html).

如果已勾選執行工作流程標幟，匯入大量中繼資料可能會導致耗用大量資源的XMP回寫活動。 在精益伺服器使用期間規劃此類匯入，以免其他使用者的效能受到影響。

## 複寫 {#replication}

將資產複製至大量發佈執行個體時（例如在Sites實作中）,Adobe建議您使用鏈式復寫。 在這種情況下，製作例項會複製到單一發佈例項，然後複製到其他發佈例項，釋放製作例項。

### 配置鏈複製 {#configure-chain-replication}

1. 選擇要用於將複製連結到
1. 在該發佈執行個體上，新增指向其他發佈執行個體的復寫代理
1. 在這些復寫代理上，在「觸發器」標籤上啟用「接收時」

>[!NOTE]
>
>Adobe不建議自動啟用資產。 不過，如有需要，Adobe建議您將此作為工作流程的最後一步，通常是DAM更新資產。

## 搜索索引 {#search-indexes}

安裝 [最新Service Pack](/help/release-notes/release-notes.md) 和效能相關的Hotfix，因為這些修正通常包含系統索引的更新。 請參閱 [效能調整提示](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) 來進行索引最佳化。

為您經常運行的查詢建立自定義索引。 如需詳細資訊，請參閱 [分析慢速查詢的方法](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 和 [自訂索引](/help/sites-deploying/queries-and-indexing.md). 如需查詢和索引最佳實務的其他相關分析，請參閱 [查詢和建立索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene索引配置 {#lucene-index-configurations}

您可以對Oak索引設定進行一些最佳化，以協助改善 [!DNL Experience Manager Assets] 效能。 更新索引配置以改進重新索引時間：

1. 開啟CRXDe `/crx/de/index.jsp` 並以管理使用者身分登入。
1. 瀏覽至 `/oak:index/lucene`.
1. 新增 `String[]` 屬性 `excludedPaths` 值 `/var`, `/etc/workflow/instances`，和 `/etc/replication`.
1. 瀏覽至 `/oak:index/damAssetLucene`. 新增 `String[]` 屬性 `includedPaths` 值 `/content/dam`. 儲存變更。

如果您的使用者不需要對資產執行全文搜尋，例如搜尋PDF檔案中的文字，然後加以停用。 通過禁用全文索引，可以提高索引效能。 禁用 [!DNL Apache Lucene] 文字擷取，請依照下列步驟執行：

1. 在 [!DNL Experience Manager] 介面，存取 [!UICONTROL 封裝管理員].
1. 上傳並安裝可於 [disable_indexingbinarytexttraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### 猜測總計 {#guess-total}

建立生成大型結果集的查詢時，請使用 `guessTotal` 參數，以避免執行時記憶體使用率過高。

## 已知問題 {#known-issues}

### 大型檔案 {#large-files}

有兩個主要已知問題與 [!DNL Experience Manager]. 當檔案的大小大於2 GB時，冷備用同步可能會出現記憶體不足的情況。 在某些情況下，它會阻止備用同步運行。 在其他情況下，會造成主要執行個體當機。 此情境適用於 [!DNL Experience Manager] 大於2GB，包括內容套件。

同樣，當檔案在使用共用S3資料儲存時達到2 GB大小時，檔案可能需要一些時間才能從快取完全保存到檔案系統。 因此，使用無二進位複製時，可能無法在複製完成之前保存二進位資料。 這種情況可能會導致問題，尤其是在資料的可用性非常重要時。

## 效能測試 {#performance-testing}

每 [!DNL Experience Manager] 部署，建立效能測試制度，以便快速發現並解決瓶頸。 以下是需要關注的一些關鍵領域。

### 網路測試 {#network-testing}

針對客戶的所有網路效能問題，請執行以下任務：

* 從客戶網路內測試網路效能
* 從Adobe網路內測試網路效能。 若為AMS客戶，請與您的CSE合作，從Adobe網路內進行測試。
* 從另一個接入點測試網路效能
* 使用網路基準工具
* 對Dispatcher進行測試

### [!DNL Experience Manager] 部署測試 {#aem-deployment-testing}

要通過高效的CPU利用率和負載共用來最大限度地減少延遲並實現高吞吐量，請監視您的效能 [!DNL Experience Manager] 定期部署。 特別是：

* 對 [!DNL Experience Manager] 部署。
* 監控上傳效能和UI回應。

## [!DNL Experience Manager Assets] 績效清單和資產管理任務的影響 {#checklist}

* 啟用HTTPS來繞過任何企業HTTP流量偵測器。
* 使用有線連線上傳大量資產。
* 在Java 8上部署。
* 設定最佳JVM參數。
* 配置檔案系統資料儲存或S3資料儲存。
* 停用子資產產生。 如果已啟用，AEM工作流程會為多頁資產中的每個頁面建立個別資產。 這些頁面都是個別資產，會耗用額外的磁碟空間、需要版本設定，以及處理額外的工作流程。 如果您不需要個別頁面，請停用子資產產生和頁面擷取活動。
* 啟用暫時性工作流程。
* 調整Granite工作流程佇列，以限制同時執行的工作。
* 設定 [!DNL ImageMagick] 限制資源消耗。
* 移除 [!UICONTROL DAM更新資產] 工作流程。
* 設定工作流程和版本清除。
* 使用最新的Service Pack和Hotfix來最佳化索引。 請向Adobe客戶支援洽詢任何其他可用的索引最佳化。
* 使用guessTotal來最佳化查詢效能。
* 如果您設定 [!DNL Experience Manager] 從檔案的內容檢測檔案類型(通過啟用 **[!UICONTROL Day CQ DAM Mime類型服務]** 在 **[!UICONTROL AEM Web Console]**)，請在非尖峰時段大量上傳許多檔案，因為它耗用大量資源。
