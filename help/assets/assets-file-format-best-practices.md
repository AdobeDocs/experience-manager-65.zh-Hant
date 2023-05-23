---
title: 處理支援的檔案格式的最佳做法
description: 處理各種受支援的檔案類型的最佳做法 [!DNL Experience Manager Assets]。
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 3%

---

# 資產檔案格式最佳做法 {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] 支援許多專有和第三方檔案格式庫，以滿足用戶的各種檔案支援需求。 支援的Adobe庫包括： [!DNL Adobe Camera Raw]、吉布森、Adobe PDF·拉斯特里澤 [!DNL Adobe InDesign Server]。 另外， [!DNL Experience Manager Assets] 支援第三方庫，包括 [!DNL ImageMagick]。 [!DNL TwelveMonkeys]等等。

有關支援的檔案格式，請參見 [資產支援的格式](/help/assets/assets-formats.md)。

>[!TIP]
>
>如果您使用 [!DNL Experience Manager] 在Adobe托管服務(AMS)上，如果您計畫處理大量大型PSD或PSB檔案，請聯繫Adobe客戶支援。 與Adobe客戶支援代表合作，為您的AMS部署實施這些最佳做法，並為Adobe的專有格式選擇盡可能最佳的工具和型號。 [!DNL Experience Manager] 可能無法處理超過 30000 x 23000 像素的極高解析度 PSB 檔案。

## [!DNL Adobe Camera Raw] 庫 {#adobe-camera-raw-library}

為獲得最佳效能，Adobe建議使用 [!DNL Adobe Camera Raw] RAW和DNG檔案庫。

[!DNL Adobe Camera Raw] 庫支援CMYK顏色配置檔案作為輸入。 但是，它以RGB色空間生成輸出，並且僅支援JPEG格式的輸出。 它不會在縮略圖中保留源檔案的彩色空間（例如CMYK）。

有關詳細資訊，請參見 [Camera Raw支援](/help/assets/camera-raw.md)。

## Adobe PDF·拉斯特里澤圖書館 {#adobe-pdf-rasterizer-library}

為獲得最佳結果，Adobe建議將Adobe PDF光柵化器庫用於以下檔案：

* 內容密集型重量PDF檔案
* 未在框外生成縮略圖的AI檔案
* 對於具有SPOT(PMS)顏色的AI檔案

使用PDF光柵化器生成的縮略圖和預覽與出廠時的光柵輸出相比質量更好。 Adobe PDFRasterizer庫不支援任何色彩空間轉換。 無論源PDF檔案的顏色空間如何，Adobe PDF光柵化器僅生成RGB輸出。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe建議您使用 [!DNL Adobe InDesign Server] 提取 [!DNL Adobe InDesign] — 特定格式副本，如IDML和HTML。 有關詳細資訊，請參見 [將Experience Manager資產添加為Adobe InDesign的參考](/help/assets/managing-linked-subassets.md#refai)。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] 通過其全球、可擴展且效能優化的網路即時生成和提供多種豐富內容的變體。 它提供互動式觀看體驗，並簡化數字營銷管理流程。 有關啟用的詳細資訊 [!DNL Dynamic Media]，請參閱 [配置Dynamic Media](/help/assets/config-dynamic.md)。

目前， [!DNL Dynamic Media] 每個檔案最多可支援15 GB的內容。

## ImageMagick庫 {#imagemagick-library}

Adobe建議在以下情形中使用ImageMagick庫：

* 為EPS檔案生成縮略圖格式副本。
* 保留影像配置檔案資訊。
* 保持透明度。
* 處理PSD和PSB檔案。

知道如何設定 [!DNL ImageMagick] 庫 [!DNL Experience Manager]，請參閱 [使用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 有關最佳用途，請參見 [配置ImageMagick的最佳做法](/help/assets/best-practices-for-imagemagick.md)。

## 影像轉碼庫 {#image-transcoding-library}

Adobe影像轉碼庫是執行核心影像處理功能的影像處理解決方案，包括影像編碼、轉碼、重新採樣、調整大小等。

映像轉碼庫支援以下MIME類型：

* JPG/JPEG
* PNG（8位和16位）
* GIF
* BMP
* TIFF/壓縮TIFF（除32位Tatix和PTiffs外）。
* 伊科
* ICN

有關詳細資訊，請參閱 [映像轉碼庫](/help/assets/imaging-transcoding-library.md)。
