---
title: 使用PDF模擬轉譯器來產生轉譯
description: 使用Adobe PDF模擬轉譯器資料庫產生高品質的縮圖和轉譯。
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 使用PDF模擬轉譯器 {#using-pdf-rasterizer}

當您將大型且內容密集型PDF或AI檔案上傳至 [!DNL Adobe Experience Manager Assets]，則預設程式庫可能無法產生正確的輸出。 Adobe的PDF模擬轉譯器程式庫可產生比預設程式庫的輸出更可靠且精確的輸出。 Adobe建議在下列情況下使用PDF模擬轉譯器程式庫：

Adobe建議對下列項目使用PDF模擬轉譯器程式庫：

* 大量且內容密集的AI檔案或PDF檔案。
* AI檔案和PDF檔案，預設不會產生縮圖。
* 具有Pantone匹配系統(PMS)顏色的AI檔案。

使用PDF模擬轉譯器產生的縮圖和預覽比現成可用的輸出品質更好，因此可提供跨裝置的一致檢視體驗。 Adobe PDF模擬轉譯器程式庫不支援任何色域轉換。 它一律會輸出為「RGB」，而不考慮來源檔案的色域。

1. 在您的 [!DNL Adobe Experience Manager] 部署 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip).

   >[!NOTE]
   >
   >PDF模擬轉譯器程式庫僅適用於Windows和Linux。

1. 存取 [!DNL Assets] 工作流控制台 `https://[aem_server]:[port]/workflow`. 開啟 [!UICONTROL DAM更新資產] 工作流程。

1. 若要防止使用預設方法產生PDF檔案和AI檔案的縮圖和Web轉譯，請遵循下列步驟：

   * 開啟 **[!UICONTROL 處理縮圖]** 步驟，然後新增 `application/pdf` 或 `application/postscript` 在 **[!UICONTROL 跳過Mime類型]** 欄位 **[!UICONTROL 縮圖]** 標籤。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在 **[!UICONTROL 啟用Web的映像]** 標籤，新增 `application/pdf` 或 `application/postscript` 在 **[!UICONTROL 略過清單]** 視您的需求而定。

   ![略過影像格式縮圖處理的設定](assets/web_enabled_imageskiplist.png)

1. 開啟 **[!UICONTROL 柵格化PDF/AI影像預覽轉譯]** 步驟，並移除您要略過預設預覽影像轉譯產生的MIME類型。 例如，移除MIME類型 `application/pdf`, `application/postscript`，或 `application/illustrator` 從 **[!UICONTROL MIME類型]** 清單。

   ![process_arguments](assets/process_arguments.png)

1. 拖曳 **[!UICONTROL PDF模擬轉譯器處理常式]** 從側面板向下 **[!UICONTROL 處理縮圖]** 步驟。
1. 為 **[!UICONTROL PDF模擬轉譯器處理常式]** 步驟：

   * MIME類型： `application/pdf` 或 `application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小：319:319, 140:100, 48:48。 視需要新增自訂縮圖設定。

   的命令行參數 `PDFRasterizer` 命令可包含下列項目：

   * `-d`:用於使文本、向量圖稿和影像平滑渲染的標籤。 建立更優質的影像。 但是，包含此參數會導致命令執行緩慢並增加影像大小。

   * `-s`:最大影像尺寸（高度或寬度）。 這會轉換為每頁的DPI。 如果頁面大小不同，每個頁面可能會以不同的數量縮放。 預設為實際頁面大小。

   * `-t`:輸出影像類型。 有效類型包括JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`:輸入PDF的路徑。 此為必要參數。

   * `-h`: 說明


1. 若要刪除中間轉譯，請選取 **[!UICONTROL 刪除生成的格式副本]**.
1. 若要讓PDF模擬轉譯器產生Web轉譯，請選取 **[!UICONTROL 生成Web格式副本]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 在 **[!UICONTROL 啟用Web的映像]** 標籤。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 儲存工作流程。
1. 若要啟用PDF模擬轉譯器以使用PDF程式庫處理PDF頁面，請開啟 **[!UICONTROL DAM程式子資產]** 從 [!UICONTROL 工作流程] 控制台。
1. 從側面板，拖曳PDF模擬轉譯器處理常式步驟至 **[!UICONTROL 建立啟用Web的影像轉譯]** 步驟。
1. 為 **[!UICONTROL PDF模擬轉譯器處理常式]** 步驟：

   * MIME類型： `application/pdf` 或 `application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小： `319:319`, `140:100`, `48:48`. 視需要新增自訂縮圖設定。

   的命令行參數 `PDFRasterizer` 命令可包含下列項目：

   * `-d`:用於使文本、向量圖稿和影像平滑渲染的標籤。 建立更優質的影像。 但是，包含此參數會導致命令執行緩慢並增加影像大小。

   * `-s`:最大影像尺寸（高度或寬度）。 這會轉換為每頁的DPI。 如果頁面大小不同，每個頁面可能會以不同的數量縮放。 預設為實際頁面大小。

   * `-t`:輸出影像類型。 有效類型包括JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`:輸入PDF的路徑。 此為必要參數。

   * `-h`: 說明


1. 若要刪除中間轉譯，請選取 **[!UICONTROL 刪除生成的格式副本]**.
1. 若要讓PDF模擬轉譯器產生Web轉譯，請選取 **[!UICONTROL 生成Web格式副本]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 在 **[!UICONTROL 啟用Web的映像]** 標籤。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 儲存工作流程。
1. 上傳PDF檔案或AI檔案至 [!DNL Experience Manager Assets]. PDF模擬轉譯器會為檔案產生縮圖和網頁轉譯。
