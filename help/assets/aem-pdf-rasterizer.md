---
title: 使用PDF點陣化器產生轉譯
description: 使用Adobe PDF點陣化器程式庫產生高品質的縮圖和轉譯。
contentOwner: AG
role: 開發人員、管理員
feature: 開發人員工具，轉譯
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# 使用PDF點陣化器{#using-pdf-rasterizer}

當您將大型且內容密集的PDF或AI檔案上傳至[!DNL Adobe Experience Manager Assets]時，預設程式庫可能無法產生正確的輸出。 Adobe的PDF點陣化器程式庫可產生比預設程式庫的輸出更可靠、更精確的輸出。 Adobe建議在下列情況下使用PDF點陣化器程式庫：

Adobe建議使用PDF點陣化器程式庫以進行下列工作：

* 大量、內容密集的AI檔案或PDF檔案。
* AI檔案和PDF檔案，預設會產生縮圖。
* AI檔案搭配Pantone Matching System(PMS)色彩。

使用PDF點陣化器產生的縮圖和預覽，與現成可用的輸出相比，品質更佳，因此可跨裝置提供一致的檢視體驗。 Adobe PDF點陣化器程式庫不支援任何色域轉換。 無論來源檔案的色域為何，都會輸出為RGB。

1. 在[軟體散發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg)的[!DNL Adobe Experience Manager]部署中安裝PDF點陣化器套件。

   >[!NOTE]
   >
   >PDF點陣化器程式庫僅適用於Windows和Linux。

1. 訪問`https://[aem_server]:[port]/workflow`處的[!DNL Assets]工作流控制台。 開啟[!UICONTROL DAM更新資產]工作流程。

1. 若要防止使用預設方法產生PDF檔案和AI檔案的縮圖和Web轉譯，請依照下列步驟進行：

   * 視需要開啟「處理縮圖&#x200B;]**」步驟，並在「縮圖]**」標籤下的「略過Mime類型&#x200B;]**」欄位中新增`application/pdf`或`application/postscript`。**[!UICONTROL **[!UICONTROL **[!UICONTROL 

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在&#x200B;**[!UICONTROL 啟用Web的映像]**&#x200B;標籤中，根據您的要求在&#x200B;**[!UICONTROL 跳過清單]**&#x200B;下添加`application/pdf`或`application/postscript`。

   ![略過影像格式縮圖處理的設定](assets/web_enabled_imageskiplist.png)

1. 開啟&#x200B;**[!UICONTROL 點陣化PDF/AI影像預覽轉譯]**&#x200B;步驟，並移除您要略過預設產生預覽影像轉譯的MIME類型。 例如，從&#x200B;**[!UICONTROL MIME類型]**&#x200B;清單中刪除MIME類型`application/pdf`、`application/postscript`或`application/illustrator`。

   ![process_arguments](assets/process_arguments.png)

1. 將&#x200B;**[!UICONTROL PDF點陣化器處理常式]**&#x200B;步驟從側面板拖曳至&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟的下方。
1. 為&#x200B;**[!UICONTROL PDF點陣化器處理常式]**&#x200B;步驟設定下列引數：

   * MIME類型：`application/pdf`或`application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小：319:319, 140:100, 48:48。 視需要新增自訂縮圖設定。

   `PDFRasterizer`命令的命令行參數可以包括：

   * `-d`:標幟可讓文字、向量圖稿和影像順暢呈現。建立更高品質的影像。 不過，加入此參數會導致命令執行緩慢，並增加影像大小。

   * `-s`:最大影像尺寸（高度或寬度）。這會針對每個頁面轉換為DPI。 如果頁面大小不同，每個頁面可能會依不同的數量進行縮放。 預設值為實際頁面大小。

   * `-t`:輸出影像類型。有效類型有JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`:輸入PDF的路徑。此參數為強制參數。

   * `-h`: 說明


1. 要刪除中間轉譯，請選擇&#x200B;**[!UICONTROL 刪除已生成的轉譯]**。
1. 若要讓PDF點陣化器產生Web轉譯，請選取「產生Web轉譯」**[!UICONTROL 。]**

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 在&#x200B;**[!UICONTROL 啟用Web的映像]**&#x200B;頁籤中指定設定。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 儲存工作流程。
1. 若要啟用PDF點陣化器以處理含PDF程式庫的PDF頁面，請從[!UICONTROL Workflow]主控台開啟&#x200B;**[!UICONTROL DAM Process Subasset]**&#x200B;模型。
1. 從側面板，將「PDF點陣化器處理常式」步驟拖曳至&#x200B;**[!UICONTROL 「建立啟用網頁的影像轉譯」步驟]**&#x200B;下方。
1. 為&#x200B;**[!UICONTROL PDF點陣化器處理常式]**&#x200B;步驟設定下列引數：

   * MIME類型：`application/pdf`或`application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小：`319:319`、`140:100`、`48:48`。 視需要新增自訂縮圖設定。

   `PDFRasterizer`命令的命令行參數可以包括：

   * `-d`:標幟可讓文字、向量圖稿和影像順暢呈現。建立更高品質的影像。 不過，加入此參數會導致命令執行緩慢，並增加影像大小。

   * `-s`:最大影像尺寸（高度或寬度）。這會針對每個頁面轉換為DPI。 如果頁面大小不同，每個頁面可能會依不同的數量進行縮放。 預設值為實際頁面大小。

   * `-t`:輸出影像類型。有效類型有JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`:輸入PDF的路徑。此參數為強制參數。

   * `-h`: 說明


1. 要刪除中間轉譯，請選擇&#x200B;**[!UICONTROL 刪除已生成的轉譯]**。
1. 若要讓PDF點陣化器產生Web轉譯，請選取「產生Web轉譯」**[!UICONTROL 。]**

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 在&#x200B;**[!UICONTROL 啟用Web的映像]**&#x200B;頁籤中指定設定。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 儲存工作流程。
1. 將PDF檔案或AI檔案上傳至[!DNL Experience Manager Assets]。 PDF點陣化器會產生檔案的縮圖和網頁轉譯。
