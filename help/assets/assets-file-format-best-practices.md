---
title: 使用AEM Assets處理各種支援檔案格式的最佳實務。
description: 使用AEM Assets處理各種支援檔案類型的最佳實務。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# 資產檔案格式最佳實務 {#assets-file-format-best-practices}

AEM Assets支援許多專屬和協力廠商的檔案格式程式庫，以符合使用者的多種檔案支援需求。 支援的Adobe程式庫包括Adobe Camera Raw、Gibson、Adobe PDF Rasterizer和Adobe inDesign Server。 此外，AEM Assets還支援協力廠商資料庫，包括ImageMagick、TwelveMones等。

如需支援的檔案格式，請參閱「 [Assets支援的格式」](/help/assets/assets-formats.md)。

>[!TIP]
>
>如果您在Adobe Managed Services(AMS)上使用Experience Manager，如果您打算處理大量大型PSD或PSB檔案，請聯絡Adobe支援。 與Adobe客戶服務代表合作，針對您的AMS部署實作這些最佳實務，並為Adobe的專屬格式選擇最佳的工具和模型。

## Adobe Camera raw資料庫 {#adobe-camera-raw-library}

為獲得最佳效能，Adobe建議使用Adobe Camera raw程式庫來處理RAW和DNG檔案。

Adobe Camera raw程式庫支援CMYK色彩描述檔作為輸入。 但是，它僅支援JPEG格式的輸出，並且在RGB顏色空間中生成輸出。 它不會在縮圖中保留原始檔案的色域（例如CMYK）。

如需詳細資訊，請參 [閱Camera raw支援](/help/assets/camera-raw.md)。

## Adobe PDF Rasterizer程式庫 {#adobe-pdf-rasterizer-library}

為獲得最佳效果，Adobe建議對下列檔案使用Adobe PDF Rasterizer程式庫：

* 大量、內容密集的PDF檔案
* 未在包裝盒中產生縮圖的AI檔案
* 對於具有專色(PMS)顏色的AI檔案

使用PDF點陣化器產生的縮圖和預覽，比現成可用的點陣化輸出更具品質。 Adobe PDF Rasterizer程式庫不支援任何色域轉換。 不論來源PDF檔案的色域為何，Adobe PDF Rasterizer都只會產生RGB輸出。

## Adobe inDesign Server {#adobe-indesign-server}

Adobe建議您使用Adobe inDesign server擷取Adobe inDesign專用的轉譯，例如IDML和HTML。 如需詳細資訊，請 [參閱「在Adobe inDesign中新增AEM資產作為參考」](/help/assets/managing-linked-subassets.md#refai)。

## 動態媒體  {#dynamic-media}

動態媒體透過其全球、可擴充且最佳化效能的網路，即時產生並提供多種多樣化內容。 它提供互動式檢視體驗，並簡化數位宣傳管理程式。 如需啟用動態媒體的詳細資訊，請參 [閱設定動態媒體](/help/assets/config-dynamic.md)。

目前，動態媒體可支援每個檔案高達20 GB的內容。

## ImageMagick程式庫 {#imagemagick-library}

Adobe建議在下列情況下使用ImageMagick程式庫：

* 為EPS檔案生成縮略圖轉譯
* 若要保留影像描述檔資訊
* 要保留透明度
* 要處理PSD和PSB檔案

若要瞭解如何在AEM中設定ImageMagic程式庫，請參 [閱使用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 如需最佳使用方式，請參 [閱設定ImageMagick的最佳實務](/help/assets/best-practices-for-imagemagick.md)。

## 影像轉碼程式庫 {#image-transcoding-library}

Adobe Imaging Rodcing Library是影像處理解決方案，可執行核心影像處理功能，包括影像編碼、轉碼、重新取樣、調整大小等。

映像轉碼庫支援以下MIME類型：

* JPG/JPEG
* PNG（8位元和16位元）
* GIF
* BMP
* TIFF/壓縮TIFF（除32位元Tiff和PTiff外）。
* ICO
* ICN

如需詳細資訊，請參 [閱影像轉碼程式庫](/help/assets/imaging-transcoding-library.md)。
