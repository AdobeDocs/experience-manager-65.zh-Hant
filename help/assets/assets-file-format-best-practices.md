---
title: 處理支援檔案格式的最佳範例
description: 使用 [!DNL Experience Manager Assets]處理各種支援檔案類型的最佳實務。
contentOwner: AG
role: 管理員
feature: 資產管理，開發人員工具
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# 資產檔案格式最佳實務{#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] 支援許多專屬和協力廠商的檔案格式程式庫，以符合使用者的多種檔案支援需求。支援的Adobe程式庫包括[!DNL Adobe Camera Raw]、Gibson、Adobe PDF點陣化器和[!DNL Adobe InDesign Server]。 此外，[!DNL Experience Manager Assets]支援協力廠商程式庫，包括[!DNL ImageMagick]、[!DNL TwelveMonkeys]等。

有關支援的檔案格式，請參見[Assets supported formats](/help/assets/assets-formats.md)。

>[!TIP]
>
>如果您在Adobe Managed Services(AMS)上使用[!DNL Experience Manager]，如果您打算處理大量大型PSD或PSB檔案，請聯絡Adobe客戶服務。 與Adobe客戶服務代表合作，為您的AMS部署實作這些最佳實務，並為Adobe的專有格式選擇最佳的工具和模型。 [!DNL Experience Manager] 可能無法處理高解析度、超過30000 x 23000像素的PSB檔案。

## [!DNL Adobe Camera Raw] 資料庫  {#adobe-camera-raw-library}

為獲得最佳效能，Adobe建議使用[!DNL Adobe Camera Raw]程式庫來處理RAW和DNG檔案。

[!DNL Adobe Camera Raw] 資料庫支援CMYK色彩描述檔作為輸入。但是，它僅支援JPEG格式的輸出，並且在RGB顏色空間中生成輸出。 它不會在縮圖中保留原始檔案的色域（例如CMYK）。

如需詳細資訊，請參閱[Camera Raw支援](/help/assets/camera-raw.md)。

## Adobe PDF光柵化器庫{#adobe-pdf-rasterizer-library}

為獲得最佳結果，Adobe建議對下列檔案使用Adobe PDF點陣化器程式庫：

* 大量、內容密集的PDF檔案
* 未在包裝盒中產生縮圖的AI檔案
* 對於具有專色(PMS)顏色的AI檔案

使用PDF點陣化器產生的縮圖和預覽，比現成可用的點陣化輸出更具品質。 Adobe PDF點陣化器程式庫不支援任何色域轉換。 不論來源PDF檔案的色域為何，Adobe PDF點陣化器只會產生RGB輸出。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe建議您使用[!DNL Adobe InDesign Server]擷取[!DNL Adobe InDesign]特定轉譯，例如IDML和HTML。 如需詳細資訊，請參閱[在Adobe InDesign](/help/assets/managing-linked-subassets.md#refai)中新增Experience Manager資產作為參考。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] 透過全球、可擴充且效能最佳化的網路，即時產生和提供多種多樣化內容。它提供互動式檢視體驗，並簡化數位宣傳管理程式。 有關啟用[!DNL Dynamic Media]的詳細資訊，請參閱[配置Dynamic Media](/help/assets/config-dynamic.md)。

目前，[!DNL Dynamic Media]可支援每個檔案高達15 GB的內容。

## ImageMagick程式庫{#imagemagick-library}

Adobe建議在下列情況下使用ImageMagick程式庫：

* 生成EPS檔案的縮略圖轉譯。
* 保留影像描述檔資訊。
* 保留透明度。
* 處理PSD和PSB檔案。

要瞭解如何在[!DNL Experience Manager]中設定[!DNL ImageMagick]庫，請參閱[使用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 如需最佳使用方式，請參閱[設定ImageMagick](/help/assets/best-practices-for-imagemagick.md)的最佳實務。

## 影像轉碼程式庫{#image-transcoding-library}

Adobe影像轉碼程式庫是執行核心影像處理功能的影像處理解決方案，包括影像編碼、轉碼、重新取樣、調整大小等。

映像轉碼庫支援以下MIME類型：

* JPG/JPEG
* PNG（8位元和16位元）
* GIF
* BMP
* TIFF/壓縮TIFF（除32位元Tiff和PTiff外）。
* ICO
* ICN

如需詳細資訊，請參閱[影像轉碼程式庫](/help/assets/imaging-transcoding-library.md)。
