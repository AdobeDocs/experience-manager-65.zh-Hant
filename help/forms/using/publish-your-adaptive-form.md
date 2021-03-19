---
title: 「教學課程：發佈最適化表單」
seo-title: 「教學課程：發佈最適化表單」
description: 將最適化表單發佈AEM為頁面、將表單內嵌至AEM Sites頁面，或將最適化表單內嵌於外部網頁
seo-description: 將最適化表單發佈AEM為頁面、將表單內嵌至AEM Sites頁面，或將最適化表單內嵌於外部網頁
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: 適用性表單
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 1%

---


# 教學課程：發佈最適化表單{#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

本教程是[建立第一個自適應表單](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的一個步驟。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

最適化表單準備就緒後，您就可以發佈表單，讓使用者也能使用。 使用者可在任何裝置和網際網路瀏覽器上開啟已發佈的表格。 發佈最適化表單時，表單和相關內容會從作者例項複製AEM至發佈AEM例項。 表單可透過發佈例項提供給使用者使用。

您有下列方法可發佈最適化表單：

* [將最適化表單發佈為頁AEM面](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [將最適化表單嵌入AEM Sites頁面](#embed-the-adaptive-form-in-an-aem-sites-page)
* [將最適化表單嵌入外部網頁(非AEM外部網頁AEM)](../../forms/using/publish-your-adaptive-form.md)

## 開始{#before-you-start}之前

* **[設定AEM Forms發佈例項](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:發佈例項是以發佈模式執行的AEM公開對應例項。 [!DNL Forms] 在生產環境中，發佈實例不在組織的防火牆外。
* **[設定複製和反向複製](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:複製會將內容從作者實例複製到發佈實例，並將用戶輸入（例如，表單輸入）從發佈實例返回作者實例。

## 將最適化表單發佈AEM為頁面{#publish-the-adaptive-form-as-an-aem-page}

當最適化表單發佈為頁AEM面時，整個網頁只包含已發佈表單。 您可以使用最適化表單的URL，從其他網頁連結表單。 要將&#x200B;**shipping-address-add-update-form**&#x200B;最適化表單發佈為AEM頁面：

1. 登入AEM[!DNL Forms]作者例項，並在[!DNL Forms] UI中找到shipping-address-add-update-form自適AEM應表單。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 選擇shipping-address-add-update-form最適化表單，然後點選&#x200B;**[!UICONTROL Publish]**。 將顯示包含與最適化表單相關的資產的對話框。 點選&#x200B;**[!UICONTROL Publish]**。 最適化表單會發佈，並出現成功對話方塊。
1. 在發佈例項上開啟表格。 此表格可供一般使用者填寫及提交。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 將最適化表單內嵌在AEM Sites頁面{#embed-the-adaptive-form-in-an-aem-sites-page}

AEM[!DNL Forms]可讓表單開發人員在AEM[!DNL Sites]頁面中順暢地內嵌最適化表單。 內嵌的最適化表單功能完整，使用者可填寫並提交表單，而不需離開頁面。 它可協助使用者在網頁上保留其他元素的內容，並同時與表單互動。

AEM [!DNL Forms]提供元件AEM[!DNL Forms]容器，將最適化表格嵌入AEM[!DNL Sites]頁面。 依預設，元件在[!DNL Sites]容器AEM中不可見。 執行以下步驟以啟AEM用[!DNL Forms]容器元件並將最適化表單嵌入AEM[!DNL Sites]頁面：

1. 在We.Retail網站中建立並開啟頁面以進行編輯。 例如，[https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 最適化表單已內嵌至[!DNL Sites]頁面。

   您也可以將最適化表單內嵌在現有的We.Retail [!DNL Site's]頁面中。 例如，ABOUT US頁[https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 它可為您節省建立頁面的時間。 以下步驟使用新建的頁面。

   We.Retail網站隨附AEM。 如果您未安裝We.Retail網站，請參閱[We.Retail Reference Implementation](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html)安裝網站。

1. 點選![properties](assets/properties.png)頁面資訊，並在新建立的We.Retail網站頁面中選取「編輯範本」(**[!UICONTROL Edit Template)選項。]**&#x200B;頁面的範本會在瀏覽器的新標籤中開啟。
1. 在&#x200B;**[!UICONTROL 版面容器]**&#x200B;方塊內點選並點選![feedmanagement](assets/feedmanagement.png)。 在&#x200B;**[!UICONTROL 允許的元件]**&#x200B;標籤中，展開&#x200B;**[!UICONTROL 一般]** accordion，選擇&#x200B;**[!UICONTROL AEM Form]**&#x200B;選項，然後點選![save_icon](assets/save_icon.svg)。 頁面AEM的[!DNL Forms]容器元件已啟用。

1. 開啟包含在步AEM驟1中開啟之[!DNL Sites]頁面的瀏覽器標籤。 點選「**[!UICONTROL 拖曳元件至此處]**」方塊並點選「**+」。** 在「插入 **[!UICONTROL 新元件」]** 方塊中，點 **[!UICONTROL 選「表AEM單」]**。將&#x200B;**[!UICONTROL AEM Forms容器]**&#x200B;元件添加到頁面中。
1. 點選&#x200B;**[!UICONTROL AEM Forms容器]**&#x200B;元件並點選![configure-icon](assets/configure-icon.svg)。 此時將出現一個屬性為AEM[!DNL Forms]容器的對話框。 在&#x200B;**[!UICONTROL 資產路徑]**&#x200B;欄位中，瀏覽並選取shipping-address-add-update-form最適化表單。 點選![save_icon](assets/save_icon.svg)。 最適化表單內嵌在頁面中。
1. 同時發佈最適化表單和[!DNL Sites]頁面。 以下是需要考慮的幾點：

   * 如果您首次AEM發佈[!DNL Sites]頁面並且該頁面包含內嵌表單，請發佈[!DNL Sites]頁面和內嵌表單。
   * 如果您只修改發佈網站頁面中的內嵌表單，請發佈原始表單，而變更會反映在發佈的網站頁面中。 發佈的網站頁面包含表單的參考，不需要重新發佈頁面。
   * 如果您修改[!DNL Sites]頁面和內嵌表單，請重新發佈[!DNL Sites]頁面和表單。

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   已在[!DNL Sites]頁面中添加AEM「發運和開單地址更改」表單。

## 將最適化表單內嵌於外部網頁{#embed-the-adaptive-form-in-an-external-webpage}

您可以在外部網頁中插入幾行JavaScript，將適AEM應性表單AEM內嵌至外部網頁（非外部網頁）。 JavaScript程式碼會傳送HTTP要求至AEM[!DNL Forms]伺服器，以取得最適化表單和相關資源，並將最適化表單新增至網頁。 如需詳細步驟，請參閱[將最適化表單內嵌至外部網頁](/help/forms/using/embed-adaptive-form-external-web-page.md)。
