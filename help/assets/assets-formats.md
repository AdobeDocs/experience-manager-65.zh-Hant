---
title: 資產支援的格式
description: AEM Assets和Dynamic Media支援的檔案格式清單以及每種格式支援的功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 84c6cc47d84656be587cc6a268b8ddc2e1e39635

---


# 支援的資產格式 {#assets-supported-formats}

AEM Assets支援多種檔案格式，而各種功能對不同MIME類型的支援也各不相同。

若要將AEM Assets與其他符合標準的數位資產管理(DAM)解決方案和案頭軟體整合，請使用Adobe的可擴充中繼資料平台(XMP)。

使用圖例瞭解支援等級。

| 支援等級 | 說明 |
|:---:|---|
| ✓ | 支援 |
| * | 支援附加功能 |
| - | 不適用 |

## AEM Assets中支援的點陣影像格式 {#supported-raster-image-formats}

| 格式 | 儲存 | 中繼資料管理 | 中繼資料擷取 | 產生縮圖 | 互動式編輯 | 中繼資料回寫 | 分析 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PGM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD **¹** | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

**¹** 從PSD檔案擷取合併的影像。 它是由Adobe Photoshop產生並包含在PSD檔案中的影像。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

## 動態媒體中支援的點陣影像格式(#supported-raster-image-formats-dynamic-media)

| 格式 | 上傳<br> （輸入格式） | 建立影像預設集<br><br><br> （輸出格式） | 預覽<br><br> 動態轉譯 | 傳送<br> 動態轉譯<br> | 下載<br><br> 動態轉譯 |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PSD **¹** | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |

**¹** 從PSD檔案擷取合併的影像。 它是由Adobe Photoshop產生並包含在PSD檔案中的影像。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

除了上述資訊外，請考慮下列事項：

* EPS檔案的支援僅適用於點陣影像。 例如，預設不支援EPS向量影像的縮圖產生。 若要新增支援，請 [設定ImageMagick](best-practices-for-imagemagick.md)。 若要整合協力廠商工具以啟用其他功能，請參 [閱命令列式媒體處理常式](media-handlers.md#command-line-based-media-handler)。

* 將中繼資料回寫新增至處理常式時，可用於PSB檔案格 `NComm` 式。

* 若要使用Dynamic Media預覽並產生EPS檔案的動態轉譯，請參閱 [Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 對於EPS檔案，PostScript Document Structuring Convention(PS-Adobe)3.0版或更新版本支援中繼資料回寫。

## 動態媒體中不支援的點陣影像格式(#unsupported-image-formats-dynamic-media)

下表說明動態媒體中不支援的點陣影像格 *式* 子類型。 該表還介紹了可用於檢測此類檔案的建議方法。

| 格式 | 什麼不支援？ | 建議的檢測方法 |
|---|---|---|
| JPEG | 初始三個位元組不正確的檔案。 | 要識別JPEF檔案，其初始三個位元組必須 `ff d8 ff`。 如果它們是其他任何內容，則不會分類為JPEG。<br>·沒有軟體工具可協助解決此問題。<br>·讀取檔案初始三個位元組的小型C++/java程式應能夠檢測到這些類型的檔案。<br>·最好追蹤此類檔案的來源，並查看產生檔案的工具。 |
| PNG | IDAT區塊大小大於100 MB的檔案。 | 您可以使用C++中 [的libpng](http://www.libpng.org/pub/png/libpng.html) 來偵測此問題。 |
| PSB |  | 如果檔案類型為PSB，請使用exiftool。<br>ExifTool記錄檔中的範例：<br>1。 File type: `PSB` |
| PSD | 不支援色域不是CMYK、RGB、灰階或點陣圖的檔案。<br>不支援DuoTone、Lab和索引色域。 | 如果「顏色」模式為「雙色調」，則使用ExifTool。<br>ExifTool記錄檔中的範例：<br>1。 顏色模式： `Duotone` |
|  | 具有突然結尾的檔案。 | Adobe無法偵測到此狀況。 此外，這類檔案無法使用Adobe PhotoShop開啟。 Adobe建議您檢查用來建立此類檔案的工具，並在來源進行疑難排解。 |
|  | 位元深度大於16的檔案。 | 如果位元深度大於16，請使用ExifTool。<br>ExifTool記錄檔中的範例：<br>1。 位元深度： `32` |
|  | 具有Lab色域的檔案。 | 如果顏色模式為Lab，請使用exiftool。<br>ExifTool記錄檔中的範例：<br>1。 顏色模式： `Lab` |
| TIFF | 具有浮點資料的檔案。 也就是說，不支援具有32位元深度的TIFF檔案。 | 如果MIME類型為且SampleFormat的值 `image/tiff` 中包含，請使 `Float` 用ExifTool。 ExifTool記錄檔中的範例：<br>1。 MIME類型：范 `image/tiff`<br>例格式： `Float #`<br>2. MIME類型：范 `image/tiff`<br>例格式： `Float; Float; Float; Float` |
|  | 具有Lab色域的檔案。 | 如果顏色模式為Lab，請使用ExifTool。<br>ExifTool記錄檔中的範例：<br>1。 顏色模式： `Lab` |

## 支援的PDF點陣化器程式庫 {#supported-pdf-rasterizer-library}

Adobe PDF Rasterizer程式庫可針對大型且內容密集的Adobe Illustrator和PDF檔案產生高品質的縮圖和預覽。 Adobe建議針對下列項目使用PDF點陣化器程式庫：

* 需要大量資源處理的內容密集型AI/PDF檔案。
* AI/PDF檔案，預設不會產生縮圖。
* AI檔案搭配Pantone Matching System(PMS)色彩。

請參 [閱使用PDF點陣化器](aem-pdf-rasterizer.md)。

## 支援的影像轉碼程式庫 {#supported-image-transcoding-library}

Adobe Imaging Rodcing程式庫是執行核心影像處理功能（例如編碼、轉碼、重新取樣和調整大小）的影像處理解決方案。

影像轉碼程式庫支援JPG/JPEG、PNG（8位元和16位元）、GIF、BMP、TIFF/壓縮TIFF（除了32位元TIFF檔案和PTIFF檔案外）、ICO和ICN MIME類型。

請參閱 [影像轉碼程式庫](imaging-transcoding-library.md)。

## 支援的相機原始資料 {#supported-camera-raw}

Adobe Camera Raw程式庫可讓AEM Assets擷取原始影像。 請參閱 [Camera Raw支援](camera-raw.md)。

## 支援的資產檔案格式 {#supported-document-formats}

資產管理功能支援的檔案格式如下：

| 格式 | 儲存 | 中繼資料<br> 管理 | 中繼資料擷取<br> (Metadata Extraction) | 產生縮圖<br> (Thumbnail Generation) | 互動式編輯<br> | 回寫中繼資料<br> (Metadata) | [分析](touch-ui-asset-insights.md) | [連線資產](use-assets-across-connected-assets-instances.md) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| RTF | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| TXT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLS | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| PS | ✓ | ✓ |  |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |  |

## 動態媒體中支援的檔案格式(##supported-document-formats-dynamic-media)

| 格式 | 上傳<br> （輸入格式） | 建立影像預設集<br><br><br> （輸出格式） | 預覽<br><br> 動態轉譯 | 傳送<br> 動態轉譯<br> | 下載<br><br> 動態轉譯 |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |

除了上述功能外，請考慮下列事項：

* 若要使用Dynamic Media為PDF檔案產生動態轉譯，請參閱 [Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 若要使用Dynamic Media預覽並產生AI檔案的動態轉譯，請參閱 [Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 若要使用動態媒體來產生INDD檔案的動態轉譯，請參 [閱InDesign(INDD)檔案格式](../assets/managing-image-presets.md#indesign-indd-file-format)。

## 支援的多媒體格式 {#supported-multimedia-formats}

|  | 儲存 | 中繼資料管理 | 中繼資料擷取 | 產生縮圖 | FFMPEG轉碼 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | - | * |
| MIDI | ✓ | ✓ |  | - | * |
| 3GP | ✓ | ✓ |  | - | * |
| MP3 | ✓ | ✓ | ✓ | - | * |
| MPG | ✓ | ✓ |  | - | * |
| OGA | ✓ | ✓ |  | - | * |
| OGG | ✓ | ✓ |  | - | * |
| RA | ✓ | ✓ |  | - | * |
| WAV | ✓ | ✓ |  | - | * |
| WMA | ✓ | ✓ |  | - | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## 動態媒體中支援的輸入視訊格式，以進行轉碼 {#supported-input-video-formats-for-dynamic-media-transcoding}

| 視訊副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC（所有描述檔） |  |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV(DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHDAvid AVR | Apple Intemiderate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（向量動畫檔案） |
| WMV | Windows Media 9 | WMV3(v9)、WMV2(v8)、WMV1(v7)、GoToMeeting(G2M2、G2M3、G2M4) | Microsoft螢幕(MSS2)、Microsoft Photo Story(WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V間隔 | XVID、DIVX、HDV、MiniDV(DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3(IV30)、MJPEG、Microsoft Video 1(MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | 西奧拉， VP3，狄拉克 |  |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | 馬特羅斯卡 | H264/AVC |  |
| R3D、RM | 紅色原始影片 | MJPEG 2000 |  |
| RAM、RM | RealVideo | 不支援 | 實數G2(RV20)、實數8(RV30)、實數10(RV40) |
| FLAC | 原生Flac | 免費無損音訊轉碼器 |  |
| MJ2 | Motion JPEG 2000 | 動態JPEG 2000編碼解碼器 |  |

## 支援的封存格式 {#supported-archive-formats}

下表涵蓋支援的封存格式以及常見DAM工作流程的適用性。

| 格式 | 儲存 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 動態媒體傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## 其他支援的格式 {#other-supported-formats}

下表說明常用DAM工作流程對其他幾種檔案格式的適用性。 所有檔案都支援一般的DAM功能，例如儲存、版本修訂、ACL、工作流程、發佈和中繼資料管理（動態媒體傳送除外）。

| 格式 | 儲存 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 動態媒體傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript（當設定有自己的傳送網域時） |  |  |  |  |  | ✓ |

## Supported MIME types {#supported-mime-types}

依預設，AEM會使用副檔名來偵測檔案類型。 AEM可從檔案內容中偵測到它。 對於後者，請 [!UICONTROL 在AEM Web Console的Day CQ] DAM Mime Type Service  ，選取「從內容偵測MIME」選項。

CRXDE Lite中提供支援的MIME類型清單，網址為 `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`。

請參 [閱配置基於MIME類型的上載作業參數支援](config-dynamic.md)。

另請參 [閱啟用MIME類型型資產/Scene7上傳工作參數支援](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。

| 副檔名 | MIME類型/ Internet媒體類型 | 預設jobParam值 | 允許的jobParam值 |
|---|---|---|---|
| 影像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 預設jobParam會套用至所有影像MIME類型資產。<ul><li>[knowngBackgroundOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_knockout_background_options.html)</li><li>manualCropOptions</li><li>[autoColorCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_auto_color_crop_options)</li><li>[autoTransparentCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_auto_transparent_crop_options)</li><li>[colorManagementOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_color_management_options.html)</li><li>[autoSetCreationOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_auto_set_creation_options.html)</li><li>[emailSetting](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/string_constants/index.html?f=r_email_settings)</li><li>[xmpKeywords](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_xmp_keywords)</li><li>[unsharpMaskOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_unsharp_mask_options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_exclude_master_video_from_avs) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_post_script_options.html)</li><li> [illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_illustrator_options.html)</li></ul> |
| AIFF | 音訊/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdf選項](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_pdf_options) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_post_script_options)</li><li>[illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_illustrator_options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_photoshop_options)</li><li>[photoshopLayerOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_photoshop_layer_options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [啟用MIME類型型資產/Scene7上傳工作參數支援](../sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。

