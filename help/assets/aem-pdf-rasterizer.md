---
title: 使用PDF模擬轉譯器來產生轉譯
description: 使用Adobe PDF模擬轉譯器資料庫產生高品質的縮圖和轉譯。
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# 使用PDF模擬轉譯器 {#using-pdf-rasterizer}

當您上傳大型且需要大量內容的PDF或AI檔案至[!DNL Adobe Experience Manager Assets]時，預設程式庫可能無法產生準確的輸出。 與預設程式庫的輸出相比，Adobe的PDF模擬轉譯器程式庫可產生更可靠且精確的輸出。 Adobe建議在下列情況下使用PDF模擬轉譯器資料庫：

Adobe建議針對下列專案使用PDF模擬轉譯器資料庫：

* 大量且需要大量內容的AI檔案或PDF檔案。
* 預設不會產生AI檔案和含縮圖的PDF檔案。
* 具有Pantone比對系統(PMS)顏色的AI檔案。

使用PDF模擬轉譯器產生的縮圖和預覽，其品質優於現成可用的輸出，因此可提供跨裝置的一致檢視體驗。 Adobe PDF模擬轉譯器資料庫不支援任何色域轉換。 無論來源檔案的色域為何，一律會輸出為RGB。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.6.zip)在您的[!DNL Adobe Experience Manager]PDF上安裝模擬轉譯器套件。

   >[!NOTE]
   >
   >PDF模擬轉譯器程式庫僅適用於Windows和Linux®。

1. 存取位於`https://[aem_server]:[port]/workflow`的[!DNL Assets]工作流程主控台。 開啟[!UICONTROL DAM更新資產]工作流程。

1. 若要防止使用預設方法為PDF檔案和AI檔案產生縮圖和網頁轉譯，請遵循下列步驟：

   * 開啟&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟，並視需要在&#x200B;**[!UICONTROL 縮圖]**&#x200B;標籤下的&#x200B;**[!UICONTROL 略過MIME型別]**&#x200B;欄位中新增`application/pdf`或`application/postscript`。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在&#x200B;**[!UICONTROL 啟用網頁的影像]**&#x200B;標籤中，根據您的需求，在&#x200B;**[!UICONTROL 略過清單]**&#x200B;下新增`application/pdf`或`application/postscript`。

   ![略過影像格式縮圖處理的設定](assets/web_enabled_imageskiplist.png)

1. 開啟&#x200B;**[!UICONTROL 點陣化PDF/AI影像預覽轉譯]**&#x200B;步驟，並移除您要略過預設產生預覽影像轉譯的MIME型別。 例如，從&#x200B;**[!UICONTROL MIME型別]**&#x200B;清單中移除MIME型別`application/pdf`、`application/postscript`或`application/illustrator`。

   ![process_arguments](assets/process_arguments.png)

1. 將&#x200B;**[!UICONTROL PDF模擬轉譯器處理常式]**&#x200B;步驟從側面板拖曳到&#x200B;**[!UICONTROL 處理縮圖]**&#x200B;步驟下方。
1. 為&#x200B;**[!UICONTROL PDF模擬轉譯器處理常式]**&#x200B;步驟設定下列引數：

   * MIME型別： `application/pdf`或`application/postscript`
   * 命令： `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小：319:319、140:100、48:48。 如有必要，請新增自訂縮圖設定。

   `PDFRasterizer`命令的命令列引數可以包含下列專案：

   * `-d`：啟用平滑呈現文字、向量圖稿和影像的旗標。 建立品質更好的影像。 但是，包含此引數會導致命令執行速度緩慢並增加影像大小。

   * `-s`：影像維度上限（高度或寬度）。 這會轉換為每一頁的DPI。 如果頁面大小不同，則每個頁面可能會以不同的量縮放。 預設為實際頁面大小。

   * `-t`：輸出影像型別。 有效型別為JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`：輸入PDF的路徑。 此為必要引數。

   * `-h`：說明

1. 若要刪除中繼轉譯，請選取&#x200B;**[!UICONTROL 刪除產生的轉譯]**。
1. 若要讓PDF模擬轉譯器產生Web轉譯，請選取&#x200B;**[!UICONTROL 產生Web轉譯]**。

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 在&#x200B;**[!UICONTROL 啟用網頁的影像]**&#x200B;索引標籤中指定設定。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 儲存工作流程。
1. 若要啟用PDF模擬轉譯器以使用PDF資料庫處理PDF頁面，請從[!UICONTROL 工作流程]主控台開啟&#x200B;**[!UICONTROL DAM處理子資產]**&#x200B;模型。
1. 從側面板，將PDF模擬轉譯器處理常式步驟拖曳至&#x200B;**[!UICONTROL 建立啟用Web的影像轉譯]**&#x200B;步驟下。
1. 為&#x200B;**[!UICONTROL PDF模擬轉譯器處理常式]**&#x200B;步驟設定下列引數：

   * MIME型別： `application/pdf`或`application/postscript`
   * 命令： `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小： `319:319`、`140:100`、`48:48`。 視需要新增自訂縮圖設定。

   `PDFRasterizer`命令的命令列引數可以包含下列專案：

   * `-d`：啟用平滑呈現文字、向量圖稿和影像的旗標。 建立品質更好的影像。 但是，包含此引數會導致命令執行速度緩慢並增加影像大小。

   * `-s`：影像維度上限（高度或寬度）。 這會轉換為每一頁的DPI。 如果頁面大小不同，則每個頁面可能會以不同的量縮放。 預設為實際頁面大小。

   * `-t`：輸出影像型別。 有效型別為JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`：輸入PDF的路徑。 此為必要引數。

   * `-h`：說明

1. 若要刪除中繼轉譯，請選取&#x200B;**[!UICONTROL 刪除產生的轉譯]**。
1. 若要讓PDF模擬轉譯器產生Web轉譯，請選取&#x200B;**[!UICONTROL 產生Web轉譯]**。

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 在&#x200B;**[!UICONTROL 啟用網頁的影像]**&#x200B;索引標籤中指定設定。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 儲存工作流程。
1. 將PDF檔案或AI檔案上傳至[!DNL Experience Manager Assets]。 PDF模擬轉譯器會產生檔案的縮圖和Web轉譯。
