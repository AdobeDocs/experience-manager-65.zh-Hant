---
title: 在 Designer 中變更頁面零內容
description: 您知道在非Adobe PDF檢視器中檢視XFA PDF時，如何變更顯示在第0頁的訊息？
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Forms Designer,Designer
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 1af3c3d4-88d7-5e0f-813c-eb70824bfcdd
    internal-label: Forms Designer
  - id: 794033c1-20ea-55a4-a8a6-b1107e12deb0
    internal-label: Designer
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 6%
---
# 在 Designer 中變更頁面零內容 {#changing-page-zero-content-in-designer}

當非Adobe PDF檢視器（例如[!DNL Chrome]或[!DNL Firefox]中的預設PDF檢視器）無法讀取PDF/XFA表單的內容時，預設會顯示「頁面零」內容。 預設的「頁面零」訊息顯示如下。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms]版Designer可讓您變更顯示在第0頁的訊息。 若要變更「頁面零」訊息，請執行下列步驟：

1. 確定您已安裝[!DNL AEM Forms]版本的Designer。 您可以從設計工具的「關於」畫面中檢查版本。

1. 開啟您要變更「頁面零」內容的表單。

1. 按一下&#x200B;**[!UICONTROL 檔案]** > **[!UICONTROL 表單屬性]**。

1. 在[!UICONTROL 表單屬性]對話方塊中，按一下![加號](assets/plus.png) （加號圖示）以新增自訂屬性。

1. 將&#x200B;**_pagezerocontent**&#x200B;指定為屬性的名稱。
1. 新增RTF格式的「頁面零」訊息作為值。 例如：


   `<body xmlns="http://www.w3.org/1999/xhtml" xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/acrreader.</p></body>`

1. 將表單儲存為PDF。

1. 在瀏覽器中檢視PDF表單，以確認訊息已更新。 上述範例值顯示如下：

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>當您重新開啟表單時，您建立的自訂屬性可能無法正確顯示在表單屬性對話方塊中。 不過，它仍可正常運作，且表單會顯示更新的「頁面零」訊息。
