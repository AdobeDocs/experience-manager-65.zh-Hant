---
title: 支援的檔案格式和MIME類型
description: ' [!DNL Assets] and [!DNL Dynamic Media] 支援的檔案格式和MIME類型，以及每種格式支援的功能。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 376bb4496c1e875f8d129dd79d67e3347be726ac
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 10%

---


# [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}支援的格式

[!DNL Experience Manager Assets] 支援多種檔案格式，而各種功能都支援不同的MIME類型。若要將[!DNL Assets]與其他符合標準的數位資產管理(DAM)解決方案和案頭軟體整合，請使用Adobe的[!DNL Extensible Metadata Platform](XMP)。

使用圖例瞭解支援等級。

| 支援等級 | 說明 |
| :-----------: | ------------------------------ |
| ý | 支援 |
| * | 支援附加功能 |
| - | 不適用 |

## [!DNL Experience Manager] {#supported-raster-image-formats}中支援的點陣影像格式

[!DNL Assets]中支援的點陣影像格式包括：

| 格式 | 儲存 | 中繼資料管理 | 中繼資料擷取 | 產生縮圖 | 編輯 | 中繼資料回寫 | 分析 |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ý | ý | ý | ý | ý | ý | ý |
| GIF | ý | ý | ý | ý | ý | - | ý |
| TIFF | ý | ý | ý | ý | - | ý | ý |
| JPEG | ý | ý | ý | ý | ý | ý | ý |
| BMP | ý | ý | ý | ý | ý | - | ý |
| PNM | ý | ý | - | - | - | - | ý |
| PGM | ý | ý | - | - | - | - | ý |
| PBM | ý | ý | - | - | - | - | ý |
| PPM | ý | ý | - | - | - | - | ý |
| PSD‡ | ý | ý | ý | ý | - | - | ý |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ý | ý | ý | ý | - | ý | - |
| PICT | - | - | - | - | - | - | ý |
| PSB | ý | ý | ý | ý | - | - | - |

‡合併的影像是從PSD檔案擷取。 它是由Adobe Photoshop產生並包含在PSD檔案中的影像。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

[!DNL Dynamic Media]中支援的點陣影像格式包括：

| 格式 | Upload<br>（輸入格式） | 建立<br>影像<br>預設<br>（輸出格式） | 預覽<br> dynamic<br>轉譯 | 傳送<br> dynamic<br>轉譯 | 下載<br> dynamic<br>轉譯 |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ý | ý | ý | ý | ý |
| GIF | ý | ý | ý | ý | ý |
| TIFF | ý | ý | ý | ý | ý |
| JPEG | ý | ý | ý | ý | ý |
| BMP | ý | - | - | - | - |
| PSD‡ | ý | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ý | ý | ý | ý | ý |
| PICT | ý | - | - | - | - |

‡合併的影像是從PSD檔案擷取。 它是由Adobe Photoshop產生並包含在PSD檔案中的影像。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

除了上述資訊外，請考慮下列事項：

* EPS檔案的支援僅適用於點陣影像。 例如，預設不支援EPS向量影像的縮圖產生。 要添加支援，請[配置ImageMagick](best-practices-for-imagemagick.md)。 若要整合協力廠商工具以啟用其他功能，請參閱[命令列式媒體處理常式](media-handlers.md#command-line-based-media-handler)。

* 將中繼資料回寫新增至`NComm`處理常式時，PSB檔案格式會運作。

* 若要使用[!DNL Dynamic Media]預覽並產生EPS檔案的動態轉譯，請參閱[Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式。](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 對於EPS檔案，PostScript Document Structuring Convention(PS-Adobe)3.0版或更新版本支援中繼資料回寫。

## 支援的3D格式{#support-3d-formats}

支援下列3D格式清單。

另請參閱[在動態媒體中使用3D資產。](/help/assets/assets-3d.md)

| 格式 | 儲存 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 縮圖預覽 | 3D預覽 | 動態媒體傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ý | ý | ý |  | ý | ý | - | - |
| gLB | ý | ý | ý | ý | ý | - | ý | ý |
| gLTF | ý | ý | ý |  | ý | - | ý | - |
| OBJ | ý | ý | ý | ý | ý | - | ý | ý |
| STL | ý | ý | ý | ý | ý | - | ý | ý |
| USDz | ý | ý | ý | ý | ý | - | - | ý |

## 動態媒體{#unsupported-image-formats-dynamic-media}中不支援的點陣影像格式

下列清單說明動態媒體中支援&#x200B;*not*&#x200B;的點陣影像檔案格式子類型。

另請參閱[偵測動態媒體不支援的檔案格式。](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html)

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援色域不是CMYK、RGB、灰階或點陣圖的PSD檔案。 不支援DuoTone、Lab和索引色域。
* 位元深度大於16的PSD檔案。
* 具有浮點資料的TIFF檔案。
* 具有Lab色域的TIFF檔案。

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](http://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## 支援的PDF點陣化器程式庫{#supported-pdf-rasterizer-library}

Adobe PDF Rasterizer程式庫可針對大型且內容密集的[!DNL Adobe Illustrator]和PDF檔案產生高品質的縮圖和預覽。 Adobe建議針對下列項目使用PDF點陣化器程式庫：

* 需要大量資源處理的內容密集型AI/PDF檔案。
* AI/PDF檔案，預設不會產生縮圖。
* AI檔案搭配Pantone Matching System(PMS)色彩。

請參閱[使用PDF點陣化器](aem-pdf-rasterizer.md)。

## 支援的影像轉碼程式庫{#supported-image-transcoding-library}

Adobe Imaging Rodcing程式庫是執行核心影像處理功能（例如編碼、轉碼、重新取樣和調整大小）的影像處理解決方案。

影像轉碼程式庫支援JPG/JPEG、PNG（8位元和16位元）、GIF、BMP、TIFF/壓縮TIFF（除了32位元TIFF檔案和PTIFF檔案外）、ICO和ICN MIME類型。

請參閱[影像轉碼程式庫](imaging-transcoding-library.md)。

## 支援的Camera Raw {#supported-camera-raw}

[!DNL Adobe Camera Raw]程式庫可讓[!DNL Assets]內嵌原始影像。 請參閱[Camera Raw支援](camera-raw.md)。

## 支援的[!DNL Assets]檔案格式{#supported-document-formats}

資產管理功能支援的檔案格式如下：

| 格式 | 儲存 | [中繼資料管理](metadata.md) | 全文<br>擷取 | [中繼資料擷取](metadata.md) | 產生縮圖<br> | [子資產抽取](managing-linked-subassets.md) | [中繼資料回寫](xmp-writeback.md) | [連線資產](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ý | ý | - | ý | ý | ý | ý | - |
| DOC | ý | ý | ý | ý | - | - | - | ý |
| DOCX | ý | ý | ý | ý | - | - | - | ý |
| ODT | ý | ý | ý | - | - | - | - | ý |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ý | ý | ý | ý | ý | ý | ý | ý |
| HTML | ý | ý | ý | - | - | - | - | ý |
| RTF | ý | ý | ý | - | - | - | - | ý |
| TXT | ý | ý | ý | - | - | - | - | ý |
| XLS | ý | ý | ý | - | - | - | - | ý |
| XLSX | ý | ý | ý | ý | - | - | - | ý |
| ODS | ý | ý | ý | - | - | - | - | - |
| PPT | ý | ý | ý | ý | ý | ý | - | ý |
| PPTX | ý | ý | ý | ý | ý | ý | - | ý |
| ODP | ý | ý | ý | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ý | ý | - | ý | ý | ý | ý | - |
| PS | ý | ý | - | - | - | - | - | - |
| QXP | ý | ý | - | - | - | - | - | - |
| EPUB | ý | ý | - | ý | ý | - | - | - |

## 動態媒體{#supported-document-formats-dynamic-media}中支援的檔案格式

| 格式 | Upload<br>（輸入格式） | 建立<br>影像<br>預設<br>（輸出格式） | 預覽<br> dynamic<br>轉譯 | 傳送<br> dynamic<br>轉譯 | 下載<br> dynamic<br>轉譯 |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ý | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ý | ý | ý | ý | ý |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ý | - | - | - | - |

除了上述功能外，請考慮下列事項：

* 若要使用Dynamic Media為PDF檔案產生動態轉譯，請參閱[Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 若要使用動態媒體來預覽並產生AI檔案的動態轉譯，請參閱[Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 若要使用動態媒體為INDD檔案產生動態轉譯，請參閱[InDesign(INDD)檔案格式](../assets/managing-image-presets.md#indesign-indd-file-format)。

## 支援的多媒體格式{#supported-multimedia-formats}

|  | 儲存 | 中繼資料管理 | 中繼資料擷取 | 產生縮圖 | FFmpeg轉碼 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ý | ý | - | - | * |
| MIDI | ý | ý | - | - | * |
| 3GP | ý | ý | - | - | * |
| MP3 | ý | ý | ý | - | * |
| MPG | ý | ý | - | - | * |
| OGA | ý | ý | - | - | * |
| OGG | ý | ý | - | - | * |
| RA | ý | ý | - | - | * |
| WAV | ý | ý | - | - | * |
| WMA | ý | ý | - | - | * |
| DVI | ý | ý | - | * | * |
| FLV | ý | ý | - | * | * |
| M4V | ý | ý | - | * | * |
| MPEG | ý | ý | - | * | * |
| OGV | ý | ý | - | * | * |
| MOV | ý | ý | - | * | * |
| WMV | ý | ý | - | * | * |
| SWF | ý | ý | - | - | - |

## 動態媒體中支援的輸入視訊格式，以轉碼{#supported-input-video-formats-for-dynamic-media-transcoding}

| 視訊副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC（所有描述檔） | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV(DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHDAvid AVR | Apple Intemiderate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（向量動畫檔案） |
| WMV | Windows Media 9 | WMV3(v9)、WMV2(v8)、WMV1(v7)、GoToMeeting(G2M2、G2M3、G2M4) | Microsoft螢幕(MSS2)、Microsoft Photo Story(WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V間隔 | XVID、DIVX、HDV、MiniDV(DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3(IV30)、MJPEG、Microsoft Video 1(MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV, OGG | Ogg | 西奧拉， VP3，狄拉克 | - |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | 馬特羅斯卡 | H264/AVC | - |
| R3D、RM | 紅色原始影片 | MJPEG 2000 | - |
| RAM、RM | RealVideo | 不支援 | 實數G2(RV20)、實數8(RV30)、實數10(RV40) |
| FLAC | 原生Flac | 免費無損音訊轉碼器 | - |
| MJ2 | Motion JPEG 2000 | 動態JPEG 2000編碼解碼器 | - |

## 支援的封存格式{#supported-archive-formats}

下表涵蓋支援的封存格式以及常見DAM工作流程的適用性。

| 格式 | 儲存 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 動態媒體傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ý | ý | ý | ý | ý | - |
| JAR | ý | ý | ý | ý | ý | - |
| RAR | ý | ý | ý | ý | ý | - |
| TAR | ý | ý | ý | ý | ý | - |
| ZIP | ý | ý | ý | ý | ý | ý |

## 其他支援的格式{#other-supported-formats}

以下說明DAM通常功能對於一些特定檔案格式的適用性。

| 格式 | 儲存 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 動態媒體傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ý | ý | ý | ý | ý | - |
| CSS | ý | ý | ý | ý | ý | ý |
| VTT | ý | ý | ý | ý | ý | ý |
| XML | ý | ý | ý | ý | ý | ý |
| JavaScript（當設定有自己的傳送網域時） | - | - | - | - | - | ý |

>[!NOTE]
>
>上傳和散發JavaScript檔案可能是安全的，也可能不安全。 如有需要，可使用覆蓋來防止使用者上傳JS檔案。

## 支援的MIME類型{#supported-mime-types}

預設情況下，[!DNL Experience Manager]使用檔案副檔名檢測檔案類型。 [!DNL Experience Manager] 可以從檔案內容中檢測到。對於後者，在[!DNL Experience Manager] Web控制台的[!UICONTROL Day CQ DAM Mime Type Service]中選擇[!UICONTROL 從內容]檢測MIME選項。

CRXDE Lite中提供支援的MIME類型清單，位於`/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`。

| 副檔名 | MIME類型/ Internet媒體類型 | 預設jobParam值 | 允許的jobParam值 |
|---|---|---|---|
| 影像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 預設jobParam會套用至所有影像MIME類型資產。<ul><li>[knowngBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | 音訊/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdf選項](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| TTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [啟用MIME類型型資產和Dynamic Media Classic上傳工作參數支援](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。
>* [配置基於MIME類型的上載作業參數支援](config-dynamic.md)。

