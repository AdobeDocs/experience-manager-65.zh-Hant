---
title: 使用PDF模擬轉譯器產生轉譯
description: 使用Adobe PDF模擬轉譯器資料庫產生高品質的縮圖和轉譯。
contentOwner: AG
role: Developer, Administrator
feature: 開發人員工具，轉譯
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: fbabf714a3b5066fdef144a4092eaad7e8a6b370
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# 使用PDF模擬轉譯器{#using-pdf-rasterizer}

將內容密集型的大型PDF或AI檔案上傳至[!DNL Adobe Experience Manager Assets]時，預設程式庫可能無法產生準確的輸出。 Adobe的PDF模擬轉譯器程式庫可產生比預設程式庫的輸出更可靠且精確的輸出。 Adobe建議在下列情況下使用PDF模擬轉譯器程式庫：

Adobe建議針對下列項目使用PDF模擬轉譯器程式庫：

* 大量且內容密集的AI檔案或PDF檔案。
* 預設不會產生縮圖的AI檔案和PDF檔案。
* AI檔案具有Pantone Matching System(PMS)顏色。

使用PDF模擬轉譯器產生的縮圖和預覽比現成可用的輸出品質更好，因此可提供跨裝置一致的檢視體驗。 Adobe PDF模擬轉譯器程式庫不支援任何色域轉換。 無論來源檔案的色域為何，都會輸出至RGB。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip)在[!DNL Adobe Experience Manager]部署上安裝PDF模擬轉譯器套件。

   >[!NOTE]
   >
   >PDF模擬轉譯器程式庫僅適用於Windows和Linux。

1. 在`https://[aem_server]:[port]/workflow`存取[!DNL Assets]工作流程主控台。 開啟[!UICONTROL DAM更新資產]工作流程。

1. 若要防止使用預設方法產生PDF檔案和AI檔案的縮圖和Web轉譯，請遵循下列步驟：

   * 開啟「處理縮圖&#x200B;]**」步驟，並視需要在「縮圖**[!UICONTROL &#x200B;縮圖&#x200B;]**」標籤下的「略過Mime類型]** 」欄位中新增`application/pdf`或`application/postscript`。**[!UICONTROL **[!UICONTROL 

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在&#x200B;**[!UICONTROL Web Enabled Image]**&#x200B;標籤中，根據您的需求，在&#x200B;**[!UICONTROL Skip List]**&#x200B;下添加`application/pdf`或`application/postscript`。

   ![略過影像格式縮圖處理的設定](assets/web_enabled_imageskiplist.png)

1. 開啟&#x200B;**[!UICONTROL 模擬化PDF/AI影像預覽轉譯]**&#x200B;步驟，並移除您要略過預設預覽影像轉譯產生的MIME類型。 例如，從&#x200B;**[!UICONTROL MIME類型]**&#x200B;清單中刪除MIME類型`application/pdf`、`application/postscript`或`application/illustrator`。

   ![process_arguments](assets/process_arguments.png)

1. 將&#x200B;**[!UICONTROL PDF模擬轉譯器處理程式]**&#x200B;步驟從側面板拖曳至&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟的下方。
1. 為&#x200B;**[!UICONTROL PDF模擬轉譯器處理常式]**&#x200B;步驟配置以下參數：

   * MIME類型：`application/pdf`或`application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小：319:319, 140:100, 48:48。 視需要新增自訂縮圖設定。

   `PDFRasterizer`命令的命令行參數可以包括：

   * `-d`:用於使文本、向量圖稿和影像平滑渲染的標籤。建立更優質的影像。 但是，包含此參數會導致命令執行緩慢並增加影像大小。

   * `-s`:最大影像尺寸（高度或寬度）。這會轉換為每頁的DPI。 如果頁面大小不同，每個頁面可能會以不同的數量縮放。 預設為實際頁面大小。

   * `-t`:輸出影像類型。有效類型為JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`:輸入PDF的路徑。此為必要參數。

   * `-h`: 說明


1. 要刪除中間格式副本，請選擇&#x200B;**[!UICONTROL 刪除生成的格式副本]**。
1. 若要讓PDF模擬轉譯器產生Web轉譯，請選取「**[!UICONTROL 產生Web轉譯]**」。

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 在&#x200B;**[!UICONTROL Web Enabled Image]**&#x200B;頁簽中指定設定。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 儲存工作流程。
1. 若要啟用PDF模擬轉譯器以使用PDF程式庫處理PDF頁面，請從[!UICONTROL Workflow]主控台開啟&#x200B;**[!UICONTROL DAM Process Subasset]**&#x200B;模型。
1. 從側面板，拖動&#x200B;**[!UICONTROL 建立啟用Web的影像轉譯]**&#x200B;步驟下的「PDF模擬轉譯器處理常式」步驟。
1. 為&#x200B;**[!UICONTROL PDF模擬轉譯器處理常式]**&#x200B;步驟配置以下參數：

   * MIME類型：`application/pdf`或`application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小：`319:319`、`140:100`、`48:48`。 視需要新增自訂縮圖設定。

   `PDFRasterizer`命令的命令行參數可以包括：

   * `-d`:用於使文本、向量圖稿和影像平滑渲染的標籤。建立更優質的影像。 但是，包含此參數會導致命令執行緩慢並增加影像大小。

   * `-s`:最大影像尺寸（高度或寬度）。這會轉換為每頁的DPI。 如果頁面大小不同，每個頁面可能會以不同的數量縮放。 預設為實際頁面大小。

   * `-t`:輸出影像類型。有效類型為JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`:輸入PDF的路徑。此為必要參數。

   * `-h`: 說明


1. 要刪除中間格式副本，請選擇&#x200B;**[!UICONTROL 刪除生成的格式副本]**。
1. 若要讓PDF模擬轉譯器產生Web轉譯，請選取「**[!UICONTROL 產生Web轉譯]**」。

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 在&#x200B;**[!UICONTROL Web Enabled Image]**&#x200B;頁簽中指定設定。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 儲存工作流程。
1. 將PDF檔案或AI檔案上傳至[!DNL Experience Manager Assets]。 PDF模擬轉譯器會為檔案產生縮圖和網頁轉譯。
