---
title: 在設計人員中變更頁面零內容
seo-title: 在設計人員中變更頁面零內容
description: 您知道在非Adobe PDF檢視器中檢視XFA PDF時，如何變更XFA PDF「零頁」上顯示的訊息？
seo-description: 您知道在非Adobe PDF檢視器中檢視XFA PDF時，如何變更XFA PDF「零頁」上顯示的訊息？
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
translation-type: tm+mt
source-git-commit: f778f8f6acf5f091465b8ec6a0b94bd30758e082

---


# 在設計人員中變更頁面零內容{#changing-page-zero-content-in-designer}

當非Adobe PDF檢視器（例如Chrome或Firefox中的預設PDF檢視器）無法讀取PDF/XFA表單的內容時，預設會顯示「零頁」內容。 預設「頁面零」訊息如下所示。

![defaultpage0message](assets/defaultpage0message.png)

AEM Forms Feature Pack 1版的Designer可讓您變更顯示在Page Zero上的訊息。 要更改「零頁」消息，請執行以下步驟：

1. 請確定您已安裝AEM Forms Feature Pack 1版Designer。 您可以從設計人員的「關於」畫面中檢查版本。

1. 開啟您要變更「零頁」內容的表單。

1. 按一 **下「檔案>表單屬性」**。

1. 在「表單屬性」對話方塊中，按 ![一下加號](assets/plus.png) （加號圖示）以新增自訂屬性。

1. 指定 **_pagezerocontent** （屬性名稱）。
1. 以Rich Text格式新增「零頁」訊息為值。 例如：

   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. 將表單儲存為PDF。

1. 在瀏覽器中檢視PDF表格，確認訊息已更新。 上述範例值顯示如下：

   ![更改消息](assets/changedmessage.png)

>[!NOTE]
>
>當您重新開啟表單時，您剛建立的自訂屬性可能無法正確顯示在「表單屬性」對話方塊中。 不過，它運作正常，而且表單會顯示更新的「零頁」訊息。

