---
title: 使用PDF柵格化器生成格式副本
description: 使用Adobe PDFRasterizer庫生成高質量縮略圖和格式副本。
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 使用PDF光柵化器 {#using-pdf-rasterizer}

將大型、內容密集型PDF或AI檔案上載到 [!DNL Adobe Experience Manager Assets]，預設庫可能無法生成準確的輸出。 Adobe的PDF光柵化器庫與預設庫的輸出相比，可以生成更可靠和更準確的輸出。 Adobe建議對以下情形使用PDF光柵化器庫：

Adobe建議使用PDF光柵化器庫進行以下操作：

* 內容密集型AI檔案或PDF檔案。
* 預設情況下不生成縮略圖的AI檔案和PDF檔案。
* AI檔案具有Pantone匹配系統(PMS)顏色。

使用PDF光柵化器生成的縮略圖和預覽與出廠輸出相比質量更好，因此可跨設備提供一致的查看體驗。 Adobe PDF光柵化器庫不支援任何顏色空間轉換。 它始終輸出到RGB，而與源檔案的顏色空間無關。

1. 將PDFRasterizer軟體包安裝到 [!DNL Adobe Experience Manager] 部署 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip)。

   >[!NOTE]
   >
   >PDFRasterizer庫僅適用於Windows和Linux。

1. 訪問 [!DNL Assets] 工作流控制台 `https://[aem_server]:[port]/workflow`。 開啟 [!UICONTROL DAM更新資產] 工作流。

1. 要防止使用預設方法生成PDF檔案和AI檔案的縮略圖和Web格式副本，請執行以下步驟：

   * 開啟 **[!UICONTROL 處理縮略圖]** 步驟，然後添加 `application/pdf` 或 `application/postscript` 的 **[!UICONTROL 跳過MIME類型]** 欄位 **[!UICONTROL 縮略圖]** 按鈕。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在 **[!UICONTROL 啟用Web的影像]** 頁籤，添加 `application/pdf` 或 `application/postscript` 在 **[!UICONTROL 跳過清單]** 取決於您的要求。

   ![用於跳過影像格式的縮略圖處理的配置](assets/web_enabled_imageskiplist.png)

1. 開啟 **[!UICONTROL 柵格化PDF/AI影像預覽格式副本]** 步驟，並刪除要跳過預設預覽影像格式副本生成的MIME類型。 例如，刪除MIME類型 `application/pdf`。 `application/postscript`或 `application/illustrator` 從 **[!UICONTROL MIME類型]** 清單框。

   ![process_arguments](assets/process_arguments.png)

1. 拖動 **[!UICONTROL PDF光柵化器處理程式]** 從側面板向下 **[!UICONTROL 處理縮略圖]** 的子菜單。
1. 為 **[!UICONTROL PDF光柵化器處理程式]** 步驟：

   * MIME類型： `application/pdf` 或 `application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 添加縮略圖大小：319:319, 140:100, 48:48。 如有必要，添加自定義縮略圖配置。

   的命令行參數 `PDFRasterizer` 命令可包括以下內容：

   * `-d`:用於使文本、向量圖稿和影像平滑呈現的標誌。 建立更優質的影像。 但是，包括此參數會導致命令運行緩慢並增大影像大小。

   * `-s`:最大影像尺寸（高度或寬度）。 這將被轉換為每頁的DPI。 如果頁面大小不同，則每個頁面都可能按不同的量進行縮放。 預設值為實際頁面大小。

   * `-t`:輸出影像類型。 有效類型為JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`:輸入PDF的路徑。 它是強制參數。

   * `-h`: 說明


1. 要刪除中間格式副本，請選擇 **[!UICONTROL 刪除生成的格式副本]**。
1. 要讓PDF柵格化器生成Web格式副本，請選擇 **[!UICONTROL 生成Web格式副本]**。

   ![generate_web_grestibles1](assets/generate_web_renditions1.png)

1. 指定 **[!UICONTROL 啟用Web的影像]** 頁籤。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 保存工作流。
1. 要啟用PDF光柵化器以使用PDF庫處理PDF頁，請開啟 **[!UICONTROL DAM進程子集]** 模型 [!UICONTROL 工作流] 控制台。
1. 從側面板中，將PDF柵格化處理程式步驟拖到 **[!UICONTROL 建立啟用Web的影像格式副本]** 的子菜單。
1. 為 **[!UICONTROL PDF光柵化器處理程式]** 步驟：

   * MIME類型： `application/pdf` 或 `application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 添加縮略圖大小： `319:319`。 `140:100`。 `48:48`。 根據需要添加自定義縮略圖配置。

   的命令行參數 `PDFRasterizer` 命令可包括以下內容：

   * `-d`:用於使文本、向量圖稿和影像平滑呈現的標誌。 建立更優質的影像。 但是，包括此參數會導致命令運行緩慢並增大影像大小。

   * `-s`:最大影像尺寸（高度或寬度）。 這將被轉換為每頁的DPI。 如果頁面大小不同，則每個頁面都可能按不同的量進行縮放。 預設值為實際頁面大小。

   * `-t`:輸出影像類型。 有效類型為JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`:輸入PDF的路徑。 它是強制參數。

   * `-h`: 說明


1. 要刪除中間格式副本，請選擇 **[!UICONTROL 刪除生成的格式副本]**。
1. 要讓PDF柵格化器生成Web格式副本，請選擇 **[!UICONTROL 生成Web格式副本]**。

   ![生成_web_greftis](assets/generate_web_renditions.png)

1. 指定 **[!UICONTROL 啟用Web的影像]** 頁籤。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 保存工作流。
1. 將PDF檔案或AI檔案上載到 [!DNL Experience Manager Assets]。 PDF光柵化器為檔案生成縮略圖和Web格式副本。
