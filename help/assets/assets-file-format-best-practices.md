---
title: 處理支援的檔案格式的最佳實務
description: 使用 [!DNL Experience Manager Assets]處理各種支援檔案類型的最佳實務。
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Assets檔案格式最佳實務 {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] 支援許多專有和第三方檔案格式庫，以滿足用戶的不同檔案支援需求。支援的Adobe庫包括[!DNL Adobe Camera Raw]、Gibson、Adobe PDF模擬轉譯器和[!DNL Adobe InDesign Server]。 此外，[!DNL Experience Manager Assets]支援第三方程式庫，包括[!DNL ImageMagick]、[!DNL TwelveMonkeys]等。

如需支援的檔案格式，請參閱[Assets supported formats](/help/assets/assets-formats.md)。

>[!TIP]
>
>如果您在Adobe Managed Services(AMS)上使用[!DNL Experience Manager]，如果您打算處理大量大型PSD或PSB檔案，請聯絡Adobe客戶支援。 與Adobe客戶支援代表合作，為您的AMS部署實作這些最佳實務，並為Adobe的專屬格式選擇最佳的工具和模型。 [!DNL Experience Manager] 可能無法處理超過30000 x 23000像素的高解析度PSB檔案。

## [!DNL Adobe Camera Raw] 資料庫 {#adobe-camera-raw-library}

為獲得最佳效能，Adobe建議對RAW和DNG檔案使用[!DNL Adobe Camera Raw]程式庫。

[!DNL Adobe Camera Raw] 庫支援CMYK顏色配置檔案作為輸入。但是，它會以RGB色域產生輸出，並僅支援以JPEG格式輸出。 它不會在縮圖中保留源檔案顏色空間（例如CMYK）。

如需詳細資訊，請參閱[Camera Raw支援](/help/assets/camera-raw.md)。

## Adobe PDF模擬轉譯器資料庫 {#adobe-pdf-rasterizer-library}

為獲得最佳結果，Adobe建議對下列檔案使用Adobe PDF模擬轉譯器程式庫：

* 大量且內容密集的PDF檔案
* 未在盒內產生縮圖的AI檔案
* 適用於具有專色(PMS)顏色的AI檔案

與現成的點陣輸出相比，使用PDF模擬轉譯器產生的縮圖和預覽的品質更佳。 Adobe PDF模擬轉譯器程式庫不支援任何色域轉換。 無論來源PDF檔案的色域為何，Adobe PDF模擬轉譯器只會產生RGB輸出。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe建議您使用[!DNL Adobe InDesign Server]擷取[!DNL Adobe InDesign]特定轉譯，例如IDML和HTML。 如需詳細資訊，請參閱[在Adobe InDesign](/help/assets/managing-linked-subassets.md#refai)中新增Experience Manager資產作為參考。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] 通過其全球、可擴展和效能優化的網路即時生成和提供多種多樣化內容。它提供互動式檢視體驗，並簡化數位行銷活動管理程式。 有關啟用[!DNL Dynamic Media]的詳細資訊，請參閱[配置Dynamic Media](/help/assets/config-dynamic.md)。

目前，[!DNL Dynamic Media]可支援每個檔案高達15 GB的內容。

## ImageMagick程式庫 {#imagemagick-library}

Adobe建議在下列情況下使用ImageMagick程式庫：

* 為EPS檔案產生縮圖轉譯。
* 保留影像設定檔資訊。
* 保持透明度。
* 處理PSD和PSB檔案。

若要了解如何在[!DNL Experience Manager]中設定[!DNL ImageMagick]程式庫，請參閱[使用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 如需最佳用法，請參閱[設定ImageMagick](/help/assets/best-practices-for-imagemagick.md)的最佳實務。

## 影像轉碼程式庫 {#image-transcoding-library}

Adobe影像轉碼程式庫是執行核心影像處理功能的影像處理解決方案，包括影像編碼、轉碼、重新取樣、調整大小等。

Imaging Conding Library支援下列MIME類型：

* JPG/JPEG
* PNG（8位元和16位元）
* GIF
* BMP
* TIFF/壓縮TIFF（32位Tiff和PTiff除外）。
* 伊科
* ICN

如需詳細資訊，請參閱[影像轉碼程式庫](/help/assets/imaging-transcoding-library.md)。
