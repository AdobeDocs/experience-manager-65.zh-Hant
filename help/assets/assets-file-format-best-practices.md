---
title: 處理支援檔案格式的最佳範例
description: 使用處理各種支援檔案類型的最佳實務 [!DNL Experience Manager Assets]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# 資產檔案格式最佳實務 {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] 支援許多專屬和協力廠商的檔案格式程式庫，以符合使用者的多種檔案支援需求。 支援的Adobe程式庫 [!DNL Adobe Camera Raw]包括、Gibson、Adobe PDF Rasterizer和 [!DNL Adobe InDesign Server]。 此外，還 [!DNL Experience Manager Assets] 支援協力廠商資料庫， [!DNL ImageMagick]包括 [!DNL TwelveMonkeys]、等等。

如需支援的檔案格式，請參閱「 [Assets支援的格式」](/help/assets/assets-formats.md)。

>[!TIP]
>
>如果您正在使 [!DNL Experience Manager] 用Adobe Managed Services(AMS)，如果您打算處理大量大型PSD或PSB檔案，請聯絡Adobe客戶服務。 與Adobe客戶服務代表合作，針對您的AMS部署實作這些最佳實務，並為Adobe的專屬格式選擇最佳的工具和模型。 [!DNL Experience Manager] 可能無法處理高解析度、超過30000 x 23000像素的PSB檔案。

## [!DNL Adobe Camera Raw] 資料庫 {#adobe-camera-raw-library}

為獲得最佳效能，Adobe建議使 [!DNL Adobe Camera Raw] 用RAW和DNG檔案的程式庫。

[!DNL Adobe Camera Raw] 資料庫支援CMYK色彩描述檔作為輸入。 但是，它僅支援JPEG格式的輸出，並且在RGB顏色空間中生成輸出。 它不會在縮圖中保留原始檔案的色域（例如CMYK）。

如需詳細資訊，請參 [閱Camera Raw支援](/help/assets/camera-raw.md)。

## Adobe PDF Rasterizer程式庫 {#adobe-pdf-rasterizer-library}

為獲得最佳效果，Adobe建議對下列檔案使用Adobe PDF Rasterizer程式庫：

* 大量、內容密集的PDF檔案
* 未在包裝盒中產生縮圖的AI檔案
* 對於具有專色(PMS)顏色的AI檔案

使用PDF點陣化器產生的縮圖和預覽，比現成可用的點陣化輸出更具品質。 Adobe PDF Rasterizer程式庫不支援任何色域轉換。 不論來源PDF檔案的色域為何，Adobe PDF Rasterizer都只會產生RGB輸出。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe建議您使 [!DNL Adobe InDesign Server] 用擷取 [!DNL Adobe InDesign]特定轉譯，例如IDML和HTML。 如需詳細資訊，請 [參閱「在Adobe InDesign中新增Experience Manager資產作為參考」](/help/assets/managing-linked-subassets.md#refai)。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] 透過全球、可擴充且效能最佳化的網路，即時產生和提供多種多樣化內容。 它提供互動式檢視體驗，並簡化數位宣傳管理程式。 如需啟用的詳細資 [!DNL Dynamic Media]訊，請 [參閱設定動態媒體](/help/assets/config-dynamic.md)。

目前， [!DNL Dynamic Media] 每個檔案最多可支援15 GB的內容。

## ImageMagick程式庫 {#imagemagick-library}

Adobe建議在下列情況下使用ImageMagick程式庫：

* 生成EPS檔案的縮略圖轉譯。
* 保留影像描述檔資訊。
* 保留透明度。
* 處理PSD和PSB檔案。

要瞭解如何在中設定 [!DNL ImageMagick] 庫，請 [!DNL Experience Manager]參 [閱使用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 如需最佳使用方式，請參 [閱設定ImageMagick的最佳實務](/help/assets/best-practices-for-imagemagick.md)。

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
