---
title: 在設計器中更改頁面零內容
seo-title: Changing Page Zero content in Designer
description: 在非Adobe PDF查看器中查看XFAPDF時，您知道如何更改XFA頁面零頁上顯示的消息？
seo-description: Do you know how you can change the message displayed on Page Zero of an XFA PDF when viewing it in a non-Adobe PDF viewer?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
feature: Adaptive Forms
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# 在設計器中更改頁面零內容 {#changing-page-zero-content-in-designer}

當非Adobe PDF查看器(如中的預設PDF查看器)時，預設顯示「零頁」內容 [!DNL Chrome] 或 [!DNL Firefox]，無法讀取PDF/XFA表單的內容。 下面顯示預設的「零頁」消息。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] Designer版本允許您更改「零頁」上顯示的消息。 要更改「零頁」消息，請執行以下步驟：

1. 確保您 [!DNL AEM Forms] 已安裝Designer版本。 可以從設計器的「關於」螢幕中檢查版本。

1. 開啟要更改「零頁」內容的表單。

1. 按一下 **[!UICONTROL 檔案]** > **[!UICONTROL 窗體屬性]**。

1. 在 [!UICONTROL 窗體屬性] 對話框，按一下 ![加](assets/plus.png) （加號表徵圖）以添加自定義屬性。

1. 指定 **_pagezerocontent** 作為屬性的名稱。
1. 以RTF格式將新的「零頁」消息添加為值。 例如：


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. 將表單另存為PDF。

1. 在瀏覽器中查看PDF表單以確認消息已更新。 上面的示例值如下所示：

   ![更改消息](assets/changedmessage.png)

>[!NOTE]
>
>當您重新開啟表單時，您剛建立的自定義屬性可能不會正確顯示在「表單屬性」對話框中。 但是，它工作正常，表單顯示更新的「零頁」消息。
