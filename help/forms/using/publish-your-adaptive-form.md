---
title: 「教學課程：發佈最適化表單」
seo-title: 「教學課程：發佈最適化表單」
description: 將最適化表單發佈為AEM頁面、將表單內嵌至AEM網站頁面，或將最適化表單內嵌至外部網頁
seo-description: 將最適化表單發佈為AEM頁面、將表單內嵌至AEM網站頁面，或將最適化表單內嵌至外部網頁
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# 教學課程：發佈最適化表單 {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

本教學課程是「建立您的第 [一個最適化表單](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 」系列的步驟。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

最適化表單準備就緒後，您就可以發佈表單，讓使用者也能使用。 使用者可在任何裝置和網際網路瀏覽器上開啟已發佈的表格。 發佈最適化表單時，表單和相關內容會從AEM作者例項複製到AEM發佈例項。 表單可透過發佈例項提供給使用者使用。

您有下列方法可發佈最適化表單：

* [將最適化表單發佈為AEM頁面](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [在AEM網站頁面中內嵌最適化表單](#embed-the-adaptive-form-in-an-aem-sites-page)
* [將最適化表單內嵌於外部網頁（AEM以外代管的非AEM網頁）](../../forms/using/publish-your-adaptive-form.md)

## 開始之前 {#before-you-start}

* **[設定AEM Forms發佈例項](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:發佈例項是以發佈模式執行之AEM Forms的公開對應例項。 在生產環境中，發佈實例不在組織的防火牆外。
* **[設定複製和反向複製](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:複製會將內容從作者實例複製到發佈實例，並將用戶輸入（例如，表單輸入）從發佈實例返回作者實例。

## 將最適化表單發佈為AEM頁面 {#publish-the-adaptive-form-as-an-aem-page}

當最適化表單發佈為AEM頁面時，整個網頁只包含已發佈的表單。 您可以使用最適化表單的URL，從其他網頁連結表單。 若要將 **shipping-address-add-update-form** adaptive表單發佈為AEM頁面：

1. 登入AEM Forms作者例項，並在AEM Forms UI中找到shipping-address-add-update-form最適化表單。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 選擇運送地址——新增——更新——表單最適化表單，然後點選「發 **布」**。 將顯示包含與最適化表單相關的資產的對話框。 點選「 **發佈**」。 最適化表單會發佈，並出現成功對話方塊。
1. 在發佈例項上開啟表格。 此表格可供一般使用者填寫及提交。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 在AEM網站頁面中內嵌最適化表單 {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM Forms可讓表單開發人員將最適化表單完美地內嵌在AEM Sites頁面中。 內嵌的最適化表單功能完整，使用者可填寫並提交表單，而不需離開頁面。 它可協助使用者在網頁上保留其他元素的內容，並同時與表單互動。

AEM Forms提供元件AEM Forms Container，可將最適化表單內嵌至AEM Sites頁面。 依預設，元件在AEM Sites容器中不可見。 執行下列步驟以啟用AEM Forms Container元件，並將最適化表單內嵌在AEM Sites頁面：

1. 在We.Retail網站中建立並開啟頁面以進行編輯。 例如， [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 最適化表單會內嵌至網站頁面。

   您也可以將最適化表單內嵌在現有的We.Retail網站頁面中。 例如，ABOUT US頁面 [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 它可為您節省建立頁面的時間。 以下步驟使用新建的頁面。

   We.Retail網站隨附AEM。 如果您未安裝We.Retail網站，請參閱「 [We.Retail Reference Implementation](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) 」安裝網站。

1. 點選 ![屬性頁](assets/properties.png) ，並在新建立的We.Retail網站頁面中選取「編 **輯範本** 」選項。 頁面的範本會在瀏覽器的新標籤中開啟。
1. 在版面容器 **方塊內點選** ，然後點選 ![feedmanagement](assets/feedmanagement.png)。 在「允 **許的元件** 」索引標籤中，展開「一般 **」accordion，選取** AEM Form **（AEM表單）選項，然後點選**![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/AEM_6_3_Forms_save.PNG)。 AEM Forms Container元件已針對頁面啟用。

1. 開啟包含在步驟1中開啟之AEM Sites頁面的瀏覽器標籤。 點選「拖 **曳元件到此處** 」方塊，然後點選 **+。** 在「插入 **新元件」方塊中** ，點選 **「AEM表單」。** AEM **Forms Container** 元件會新增至頁面。
1. 點選 **AEM Forms容器元件** ，然後點選 ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/6-2/cmppr.png)。 此時會出現一個對話方塊，其中包含AEM Forms容器的屬性。 在「資 **產路徑** 」欄位中，瀏覽並選取shipping-address-add-update-form最適化表單。 點選 ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/icons/AEM_6_3_Forms_save.PNG)。 最適化表單內嵌在頁面中。
1. 同時發佈最適化表單和網站頁面。 以下是需要考慮的幾點：

   * 如果您是第一次發佈AEM網站頁面，而且其中包含內嵌表單，請發佈網站頁面和內嵌表單。
   * 如果您只修改發佈網站頁面中的內嵌表單，請發佈原始表單，而變更會反映在發佈的網站頁面中。 發佈的網站頁面包含表單的參考，不需要重新發佈頁面。
   * 如果您修改網站頁面和內嵌表單，請重新發佈網站頁面和表單。
   ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   新增至「AEM網站」頁面的「送貨和帳單地址變更」表單。

## 將自適應表單嵌入外部網頁 {#embed-the-adaptive-form-in-an-external-webpage}

您可以在外部網頁中插入幾行JavaScript，將最適化表單內嵌至外部網頁（AEM外部代管的非AEM網頁）。 JavaScript程式碼會傳送HTTP要求至AEM Forms伺服器，以取得最適化表單和相關資源，並將最適化表單新增至網頁。 如需詳細步驟，請 [參閱將最適化表單內嵌至外部網頁](/help/forms/using/embed-adaptive-form-external-web-page.md)。
