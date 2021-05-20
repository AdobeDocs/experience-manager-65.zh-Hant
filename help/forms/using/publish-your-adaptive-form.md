---
title: 「教學課程：發佈最適化表單」
seo-title: 「教學課程：發佈最適化表單」
description: 將最適化表單發佈為AEM頁面、將表單內嵌至AEM Sites頁面，或將最適化表單內嵌至外部網頁
seo-description: 將最適化表單發佈為AEM頁面、將表單內嵌至AEM Sites頁面，或將最適化表單內嵌至外部網頁
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: 適用性表單
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 1%

---

# 教學課程：發佈最適化表單{#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

本教學課程是[建立第一個最適化表單](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的步驟。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

最適化表單準備就緒後，您就可以發佈表單，讓一般使用者能使用。 最終用戶可以在任何設備和網際網路瀏覽器上開啟已發佈的表單。 發佈最適化表單時，表單和相關內容會從AEM製作例項複製到AEM發佈例項。 表單可透過發佈例項供一般使用者使用。

您有下列方法可發佈最適化表單：

* [以AEM頁面發佈最適化表單](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [將最適化表單內嵌在AEM Sites頁面中](#embed-the-adaptive-form-in-an-aem-sites-page)
* [將最適化表單嵌入外部網頁(在AEM外部托管的非AEM網頁)](../../forms/using/publish-your-adaptive-form.md)

## 開始之前{#before-you-start}

* **[設定AEM Forms發佈例項](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:發佈例項是以發佈模式執行之AEM的 [!DNL Forms] 公開顯示例項。在生產環境中，發佈例項位於組織的防火牆之外。
* **[設定復寫和反向復寫](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:復寫會將內容從製作例項複製到發佈例項，並從發佈例項傳回使用者輸入（例如表單輸入）至製作例項。

## 將最適化表單發佈為AEM頁面{#publish-the-adaptive-form-as-an-aem-page}

當最適化表單發佈為AEM頁面時，整個網頁僅包含已發佈的表單。 您可以使用最適化表單的URL，從其他網頁連結該URL。 若要將&#x200B;**shipping-add-update-form**&#x200B;適用性表單發佈為AEM頁面：

1. 登入AEM [!DNL Forms]製作例項，並在AEM [!DNL Forms] UI中找到shipping-add-update-form適用性表單。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 選取運送地址 — add-update-form適用性表單，然後點選&#x200B;**[!UICONTROL Publish]**。 隨即顯示對話方塊，其中包含與最適化表單相關的資產。 點選「**[!UICONTROL 發佈]**」。 最適化表單已發佈，且會顯示成功對話方塊。
1. 在發佈執行個體上開啟表單。 表單可供一般使用者填寫及提交。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 將最適化表單內嵌在AEM Sites頁面{#embed-the-adaptive-form-in-an-aem-sites-page}中

AEM [!DNL Forms]可讓表單開發人員將最適化表單流暢內嵌至AEM [!DNL Sites]頁面。 內嵌的最適化表單功能齊全，使用者無需離開頁面即可填寫及提交表單。 可協助使用者停留在網頁上其他元素的內容中，並同時與表單互動。

AEM [!DNL Forms]提供元件AEM [!DNL Forms]容器，將最適化表單內嵌至AEM [!DNL Sites]頁面。 依預設，元件不會顯示在AEM [!DNL Sites]容器中。 執行下列步驟以啟用AEM [!DNL Forms]容器元件，並將最適化表單嵌入AEM [!DNL Sites]頁面：

1. 在We.Retail網站中建立並開啟頁面以進行編輯。 例如， [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 適用性表單已內嵌至[!DNL Sites]頁面。

   您也可以將最適化表單嵌入現有的We.Retail [!DNL Site's]頁面。 例如，「關於美國」頁面[https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 這可為您節省建立頁面的時間。 下列步驟使用新建立的頁面。

   We.Retail網站隨附AEM。 如果您未安裝We.Retail網站，請參閱[We.Retail Reference Implementation](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html)安裝網站。

1. 點選![properties](assets/properties.png)頁面資訊，然後在新建立的We.Retail網站頁面中選取&#x200B;**[!UICONTROL 編輯範本]**&#x200B;選項。 頁面範本會在瀏覽器的新索引標籤中開啟。
1. 在&#x200B;**[!UICONTROL 版面容器]**&#x200B;方塊內點選，然後點選![feedmanagement](assets/feedmanagement.png)。 在「**[!UICONTROL 允許的元件]**」標籤中，展開「**[!UICONTROL 一般]**」設定追蹤器，選取「**[!UICONTROL AEM表單]**」選項，然後點選「![save_icon](assets/save_icon.svg)」。 已為頁面啟用AEM [!DNL Forms]容器元件。

1. 開啟包含在步驟1中開啟之AEM [!DNL Sites]頁面的瀏覽器標籤。 點選「 **[!UICONTROL Drag components here]**」方塊，然後點選「 **+」。** 在「插 **[!UICONTROL 入新元]** 件」方塊中，點 **[!UICONTROL 選「AEM表單」]**。將&#x200B;**[!UICONTROL AEM Forms容器]**&#x200B;元件新增至頁面。
1. 點選&#x200B;**[!UICONTROL AEM Forms容器]**&#x200B;元件，然後點選![configure-icon](assets/configure-icon.svg)。 此時將出現一個具有AEM [!DNL Forms]容器屬性的對話框。 在&#x200B;**[!UICONTROL 資產路徑]**&#x200B;欄位中，瀏覽並選取運送地址 — add-update-form適用性表單。 點選![save_icon](assets/save_icon.svg)。 最適化表單已內嵌於頁面中。
1. 同時發佈最適化表單和[!DNL Sites]頁面。 以下是需要考慮的幾點：

   * 如果您是第一次發佈AEM [!DNL Sites]頁面，且其中包含內嵌表單，請發佈[!DNL Sites]頁面和內嵌表單。
   * 如果您只修改已發佈網站頁面中的內嵌表單，則發佈原始表單，而變更會反映在已發佈網站頁面中。 已發佈的網站頁面包含對表單的參考，不需要重新發佈頁面。
   * 如果修改[!DNL Sites]頁面和內嵌表單，請重新發佈[!DNL Sites]頁面和表單。

      ![內嵌 — aem-sites](assets/embed-in-aem-sites.png)
   在AEM [!DNL Sites]頁面中新增了「運送和帳單地址變更」表單。

## 將最適化表單嵌入外部網頁{#embed-the-adaptive-form-in-an-external-webpage}

您可以在外部網頁中插入幾行JavaScript，將最適化表單嵌入外部網頁(AEM外部托管的非AEM網頁)。 JavaScript程式碼會傳送HTTP要求至AEM [!DNL Forms]伺服器，以取得最適化表單和相關資源，並將最適化表單新增至網頁。 如需詳細步驟，請參閱[將最適化表單內嵌至外部網頁](/help/forms/using/embed-adaptive-form-external-web-page.md)。
