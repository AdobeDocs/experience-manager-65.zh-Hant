---
title: 支援的檔案格式和MIME類型
description: 支援的檔案格式和MIME類型 [!DNL Assets] 和 [!DNL Dynamic Media] 以及每種格式支援的功能。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 9%

---

# 支援的格式 [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] 支援多種檔案格式，而且每種功能對不同MIME類型的支援各不相同。 要整合 [!DNL Assets] 與其他符合標準的數字資產管理(DAM)解決方案和案頭軟體一起，使用Adobe [!DNL Extensible Metadata Platform] (XMP)。

請參閱圖例以了解支援程度。

| 支援程度 | 說明 |
| :-----------: | ------------------------------ |
| ✓ | 支援 |
| &#42; | 支援附加功能 |
| − | 不適用 |

## 支援的點陣影像格式 [!DNL Experience Manager] {#supported-raster-image-formats}

支援的點陣影像格式 [!DNL Assets] 為：

| 格式 | 儲存空間 | 中繼資料管理 | 中繼資料擷取 | 縮圖產生 | 編輯 | 中繼資料回寫 | 分析 |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PNM | ✓ | ✓ | - | - | - | - | ✓ |
| PGM | ✓ | ✓ | - | - | - | - | ✓ |
| PBM | ✓ | ✓ | - | - | - | - | ✓ |
| PPM | ✓ | ✓ | - | - | - | - | ✓ |
| PSD協定 | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | - | ✓ | - |
| PICT | - | - | - | - | - | - | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | - | - | - |

*從PSD檔案擷取合併的影像。 這是由Adobe Photoshop產生並包含在PSD檔案中的影像。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

除了上述資訊外，請考量下列事項：

* EPS檔案的支援僅適用於點陣影像。 例如，預設不支援EPS向量影像的縮圖產生。 要添加支援， [配置ImageMagick](best-practices-for-imagemagick.md). 若要整合協力廠商工具以啟用其他功能，請參閱 [基於命令行的媒體處理程式](media-handlers.md#command-line-based-media-handler).

* 將中繼資料回寫新增至 `NComm` 處理常式。

* 對於EPS檔案， PostScript檔案結構約定(PS-Adobe)3.0版或更新版本支援中繼資料回寫。

## 支援的3D格式 {#support-3d-formats}

支援下列3D格式清單。

另請參閱 [在Dynamic Media中使用3D資產。](/help/assets/assets-3d.md)

| 格式 | 儲存空間 | 版本設定 | 工作流程 | 發佈 | 存取控制 | 縮圖預覽 | 3D預覽 | Dynamic Media傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## 支援的PDF模擬轉譯器程式庫 {#supported-pdf-rasterizer-library}

Adobe PDF模擬轉譯器程式庫會針對大型且內容密集型項目產生高品質的縮圖和預覽 [!DNL Adobe Illustrator] 和PDF檔案。 Adobe建議對下列項目使用PDF模擬轉譯器程式庫：

* 需要大量資源來處理的內容密集型AI/PDF檔案。
* AI/PDF檔案，預設不會產生縮圖。
* 具有Pantone匹配系統(PMS)顏色的AI檔案。

請參閱 [使用PDF模擬轉譯器](aem-pdf-rasterizer.md).

## 支援的影像轉碼程式庫 {#supported-image-transcoding-library}

Adobe影像轉碼程式庫是執行核心影像處理功能（例如編碼、轉碼、重新取樣和調整大小）的影像處理解決方案。

影像轉碼程式庫支援JPG/JPEG、PNG（8位元和16位元）、GIF、BMP、TIFF/壓縮TIFF(32位元TIFF檔案和PTIFF檔案除外)、ICO和ICN MIME類型。

請參閱 [影像轉碼程式庫](imaging-transcoding-library.md).

## 支援的Camera Raw {#supported-camera-raw}

此 [!DNL Adobe Camera Raw] 程式庫啟用 [!DNL Assets] 擷取原始影像。 請參閱 [Camera Raw支援](camera-raw.md).

## 支援 [!DNL Assets] 檔案格式 {#supported-document-formats}

資產管理功能支援的文檔格式如下：

| 格式 | 儲存空間 | [中繼資料管理](metadata.md) | 全文<br> 摘取 | [中繼資料擷取](metadata.md) | 縮圖<br> 產生 | [子資產提取](managing-linked-subassets.md) | [中繼資料回寫](xmp-writeback.md) | [連線資產](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| DOC | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| RTF | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| TXT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLS | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODS | ✓ | ✓ | ✓ | - | - | - | - | - |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| ODP | ✓ | ✓ | ✓ | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| PS | ✓ | ✓ | - | - | - | - | - | - |
| QXP | ✓ | ✓ | - | - | - | - | - | - |
| ePub | ✓ | ✓ | - | ✓ | ✓ | - | - | - |

## 支援的多媒體格式 {#supported-multimedia-formats}

|  | 儲存空間 | 中繼資料管理 | 中繼資料擷取 | 縮圖產生 | FFmpeg轉碼 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | - | - | &#42; |
| MIDI | ✓ | ✓ | - | - | &#42; |
| 3GP | ✓ | ✓ | - | - | &#42; |
| MP3 | ✓ | ✓ | ✓ | - | &#42; |
| MPG | ✓ | ✓ | - | - | &#42; |
| OGA | ✓ | ✓ | - | - | &#42; |
| OGG | ✓ | ✓ | - | - | &#42; |
| RA | ✓ | ✓ | - | - | &#42; |
| WAV | ✓ | ✓ | - | - | &#42; |
| WMA | ✓ | ✓ | - | - | &#42; |
| DVI | ✓ | ✓ | - | &#42; | &#42; |
| FLV | ✓ | ✓ | - | &#42; | &#42; |
| M4V | ✓ | ✓ | - | &#42; | &#42; |
| MPEG | ✓ | ✓ | - | &#42; | &#42; |
| OGV | ✓ | ✓ | - | &#42; | &#42; |
| MOV | ✓ | ✓ | - | &#42; | &#42; |
| WMV | ✓ | ✓ | - | &#42; | &#42; |
| SWF | ✓ | ✓ | - | - | - |

## 支援的封存格式 {#supported-archive-formats}

下表說明支援的封存格式和通用DAM工作流程的適用性。

| 格式 | 儲存空間 | 版本設定 | 工作流程 | 發佈 | 存取控制 | Dynamic Media傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## 其他支援的格式 {#other-supported-formats}

以下說明幾種特定檔案格式的一般DAM功能的適用性。

| 格式 | 儲存空間 | 版本設定 | 工作流程 | 發佈 | 存取控制 | Dynamic Media傳送 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript（若已設定自己的傳送網域） | - | - | - | - | - | ✓ |

>[!NOTE]
>
>上傳和分發JavaScript檔案可能是安全的，也可能不安全。 如有必要，您可以使用覆蓋來防止使用者上傳JS檔案。

## 支援的MIME類型 {#supported-mime-types}

依預設， [!DNL Experience Manager] 會使用檔案副檔名檢測檔案類型。 [!DNL Experience Manager] 可從檔案的內容中偵測。 若是後者，請選取 [!UICONTROL 從內容中檢測MIME] 選項 [!UICONTROL Day CQ DAM Mime類型服務] 在 [!DNL Experience Manager] Web主控台。

支援的MIME類型清單可在以下CRXDE Lite取得： `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| 副檔名 | MIME類型/ Internet媒體類型 | 預設jobParam值 | 允許的jobParam值 |
|---|---|---|---|
| 影像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 預設的jobParam會套用至所有影像MIME類型資產。<ul><li>[trunkdownBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| 檔案 | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>應用程式/eps</li><li>application/x-eps</li><li>影像/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | 影像/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | 視頻/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | 視頻/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF /TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | 視頻/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

## Dynamic Media — 支援的轉碼輸入視訊格式 {#supported-input-video-formats-for-dynamic-media-transcoding}

| 影片副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
|---|---|---|---|
| AVI | A/V插播 | XVID、DIVX、HDV、MiniDV(DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3(IV30)、MJPEG、Microsoft® Video 1(MS-CRAM) |
| FLV、F4V | AdobeFlash | H264/AVC, Flix VP6, H263, Sorenson | SWF（向量動畫檔案） |
| M4V | Apple iTunes | H264/AVC | - |
| MKV | 馬特羅斯卡 | H264/AVC | - |
| MOV, QT | Apple QuickTime | H264/AVC、Apple ProRes422和HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV(DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple中級，Apple動畫 |
| MP4 | MPEG-4 | H264/AVC（所有配置檔案） | - |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| MXF‡ | MXF | Sony XDCAM、MPEG-2、MPEG-4、松下DVCPro | - |
| 奧格夫、奧格 | 奧格 | 蒂奧拉，VP3，狄拉克 | - |
| WebM | WebM | Google VP8 | - |
| WMV | Windows Media 9 | WMV3(v9)、WMV2(v8)、WMV1(v7)、GoToMeeting(G2M2、G2M3、G2M4) | Microsoft®螢幕(MSS2)、Microsoft®照片(WVP2) |

*此視訊格式尚不支援與Dynamic Media中的互動式視訊搭配使用，或與Experience Manager Assets中的附註搭配使用。

## Dynamic Media — 支援的檔案格式 {#supported-document-formats-dynamic-media}

| 格式 | 上傳<br> （輸入格式） | 建立<br> 影像<br> 預設集<br> （輸出格式） | 預覽<br> 動態<br> 轉譯 | 傳遞<br> 動態<br> 轉譯 | 下載<br> 動態<br> 轉譯 |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) （請參閱下方附註） | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>針對安全PDF，僅支援上傳。

除了上述功能外，請考量下列事項：

* 若要使用Dynamic Media產生PDF檔案的動態轉譯，請參閱 [Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 若要使用Dynamic Media來預覽和產生AI檔案的動態轉譯，請參閱 [Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 若要使用Dynamic Media產生INDD檔案的動態轉譯，請參閱 [InDesign(INDD)檔案格式](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media — 支援的點陣影像格式 {#supported-raster-image-formats-dynamic-media}

| 格式 | 上傳<br> （輸入格式） | 建立<br> 影像<br> 預設集<br> （輸出格式） | 預覽<br> 動態<br> 轉譯 | 傳遞<br> 動態<br> 轉譯 | 下載<br> 動態<br> 轉譯 | 設定支援此格式的類型 |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/image-sets.md), [混合媒體](/help/assets/mixed-media-sets.md)，和 [回轉](/help/assets/spin-sets.md) |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/image-sets.md), [混合媒體](/help/assets/mixed-media-sets.md)，和 [回轉](/help/assets/spin-sets.md) |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/image-sets.md), [混合媒體](/help/assets/mixed-media-sets.md)，和 [回轉](/help/assets/spin-sets.md) |
| BMP | ✓ | - | - | - | - | [影像](/help/assets/image-sets.md), [混合媒體](/help/assets/mixed-media-sets.md)，和 [回轉](/help/assets/spin-sets.md) |
| PSD協定 | ✓ | - | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| PICT | ✓ | - | - | - | - | - |

*從PSD檔案擷取合併的影像。 這是由Adobe Photoshop產生並包含在PSD檔案中的影像。 根據設定，合併的影像可能是實際影像，也可能不是實際影像。

* EPS檔案的支援僅適用於點陣影像。 例如，預設不支援EPS向量影像的縮圖產生。 要添加支援， [配置ImageMagick](best-practices-for-imagemagick.md). 若要整合協力廠商工具以啟用其他功能，請參閱 [基於命令行的媒體處理程式](media-handlers.md#command-line-based-media-handler).

* 使用 [!DNL Dynamic Media] 若要預覽和產生EPS檔案的動態轉譯，請參閱 [Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式。](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 對於EPS檔案， PostScript檔案結構約定(PS-Adobe)3.0版或更新版本支援中繼資料回寫。

## Dynamic Media — 不支援的點陣影像格式 {#unsupported-image-formats-dynamic-media}

以下清單描述光柵影像檔案格式的子類型： *not* 支援Dynamic Media。

另請參閱 [偵測不支援的Dynamic Media檔案格式](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html) 知識庫文章。

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援具有CMYK、RGB、灰度或點陣圖以外的顏色空間的PSD檔案。 不支援DuoTone、Lab和索引色空間。
* PSD位深度大於16的檔案。
* TIFF具有浮點資料的檔案。
* TIFF具有Lab色域的檔案。

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media — 支援的3D格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支援下列3D格式。

另請參閱 [在Dynamic Media中使用3D資產](/help/assets/assets-3d.md).

| 3D檔案副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | 模型/gltf二進位 | 將材料和紋理作為單一資產包含。 |
| OBJ | WaveFront 3D對象檔案 | application/x-tgif |  |
| STL | 光固化成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用場景描述Zip封存 | model/vnd.usdz+zip | *僅支援擷取；沒有可用的檢視或互動。* USDZ是專屬的3D格式，可由Safari和iOS裝置原生檢視。 |

>[!MORELIKETHIS]
>
>* [啟用MIME類型型資產和Dynamic Media Classic上傳工作參數支援](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [配置基於MIME類型的上載作業參數支援](config-dynamic.md).

