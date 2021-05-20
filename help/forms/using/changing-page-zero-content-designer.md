---
title: 在設計器中更改頁面零內容
seo-title: 在設計器中更改頁面零內容
description: 在非Adobe PDF檢視器中檢視XFA PDF時，您知道如何變更PDF的「Page Zero」（頁面零）上顯示的訊息？
seo-description: 在非Adobe PDF檢視器中檢視XFA PDF時，您知道如何變更PDF的「Page Zero」（頁面零）上顯示的訊息？
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
feature: 適用性表單
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 2%

---

# 更改設計器{#changing-page-zero-content-in-designer}中的頁面零內容

當非Adobe PDF檢視器（例如[!DNL Chrome]或[!DNL Firefox]中的預設PDF檢視器）無法讀取PDF/XFA表單的內容時，預設會顯示「頁面零」內容。 預設的Page Zero訊息如下所示。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] 「設計器」的版本允許您更改「頁面零」上顯示的消息。要更改「零頁」消息，請執行以下步驟：

1. 確保已安裝[!DNL AEM Forms]版本的Designer。 您可以從設計工具的「關於」畫面中檢查版本。

1. 開啟您要變更「頁面零」內容的表單。

1. 按一下「**[!UICONTROL 檔案]** > **[!UICONTROL 表單屬性]**」。

1. 在[!UICONTROL 表單屬性]對話方塊中，按一下![加號](assets/plus.png)（加號圖示）以新增自訂屬性。

1. 指定&#x200B;**_pagezerocontent**&#x200B;作為屬性的名稱。
1. 以RTF格式新增「頁面零」訊息作為值。 例如：


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. 將表單儲存為PDF。

1. 在瀏覽器中檢視PDF表單，確認訊息已更新。 上述範例值顯示如下：

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>當您重新開啟表單時，您剛建立的自訂屬性可能無法在「表單屬性」對話方塊中正確顯示。 不過，此功能正常運作，表單會顯示更新的「頁面零」訊息。
