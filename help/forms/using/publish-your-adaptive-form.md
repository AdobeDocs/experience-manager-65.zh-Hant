---
title: 「教學課程：發佈最適化表單」
description: 將調適型表單發佈為AEM頁面、將表單內嵌至AEM Sites頁面，或將調適型表單內嵌至外部網頁
contentOwner: khsingh
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# 教學課程：發佈最適化表單 {#tutorial-publish-your-adaptive-form}

![Hero-image](do-not-localize/13-publish-your-adaptive-form-small.png)

本教學課程是 [建立第一個最適化表單](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 數列。 建議您依照序列時間順序來瞭解、執行和示範完整的教學課程使用案例。

最適化表單準備就緒後，您可以發佈表單，以供一般使用者使用。 一般使用者可在任何裝置和網際網路瀏覽器上開啟已發佈的表單。 發佈調適型表單時，表單和相關內容會從AEM製作例項複製到AEM發佈例項。 一般使用者可透過發佈執行個體使用此表單。

您有以下方法可發佈調適型表單：

* [將最適化表單發佈為AEM頁面](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [將最適化表單內嵌到AEM Sites頁面中](#embed-the-adaptive-form-in-an-aem-sites-page)
* [將最適化表單內嵌到外部網頁中(託管在AEM外部的非AEM網頁)](../../forms/using/publish-your-adaptive-form.md)

## 開始之前 {#before-you-start}

* **[設定AEM Forms發佈執行個體](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**：發佈執行個體是AEM的公開執行個體 [!DNL Forms] 在發佈模式下執行。 在生產環境中，發佈執行個體位於組織的防火牆之外。
* **[設定復寫與反向復寫](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**：復寫會將內容從製作執行個體複製到發佈執行個體，並將使用者輸入（例如表單輸入）從發佈執行個體傳回製作執行個體。

## 將最適化表單發佈為AEM頁面 {#publish-the-adaptive-form-as-an-aem-page}

將最適化表單發佈為AEM頁面時，整個網頁將僅包含發佈的表單。 您可以使用最適化表單的URL，從其他網頁將其連結。 若要發佈 **shipping-address-add-update-form** AEM頁面適用性表單：

1. 登入AEM [!DNL Forms] 編寫執行個體並在AEM中找到shipping-address-add-update-form最適化表單 [!DNL Forms] UI。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 選取shipping-address-add-update-form最適化表單，然後選取 **[!UICONTROL 發佈]**. 隨即顯示對話方塊，其中包含與最適化表單相關的資產。 選取 **[!UICONTROL 發佈]**. 最適化表單已發佈，且成功對話方塊隨即顯示。
1. 在發佈執行個體上開啟表單。 一般使用者可填寫並提交表單。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 將最適化表單內嵌到AEM Sites頁面中 {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] 可讓表單開發人員在AEM中順暢地內嵌最適化表單 [!DNL Sites] 頁面。 嵌入式調適型表單功能齊全，使用者無需離開頁面即可填寫並提交表單。它有助於使用者停留在網頁上其他元素的內容中，同時與表單互動。

AEM [!DNL Forms] 提供元件AEM [!DNL Forms] 容器，用於將最適化表單內嵌到AEM [!DNL Sites] 頁面。 依預設，元件在AEM中不可見 [!DNL Sites] 容器。 執行以下步驟以啟用AEM [!DNL Forms] 容器元件以及將最適化表單內嵌到AEM中 [!DNL Sites] 頁面：

1. 在We.Retail網站中建立並開啟頁面以進行編輯。 例如， [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). 最適化表單已內嵌至 [!DNL Sites] 頁面。

   您也可以將最適化表單內嵌在現有的We.Retail中 [!DNL Site's] 頁面。 例如，「關於美國」頁面 [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). 這可節省您建立頁面的時間。 以下步驟使用新建立的頁面。

   We.Retail網站隨附AEM。 如果您尚未安裝We.Retail網站，請參閱 [We.Retail參考實作](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) 安裝網站。

1. 選取 ![屬性](assets/properties.png) 頁面資訊，並選取 **[!UICONTROL 編輯範本]** 新建立的We.Retail網站頁面中的選項。 頁面範本會在瀏覽器的新標籤中開啟。
1. 在內選取 **[!UICONTROL 配置容器]** 方塊並選取 ![摘要管理](assets/feedmanagement.png). 在 **[!UICONTROL 允許的元件]** 標籤，展開 **[!UICONTROL 一般]** 摺疊式功能表，選取 **[!UICONTROL AEM表單]** 選項，然後選取 ![儲存圖示](assets/save_icon.svg). AEM [!DNL Forms] 已針對頁面啟用容器元件。

1. 開啟包含AEM的瀏覽器索引標籤 [!DNL Sites] 步驟1中開啟的頁面。 選取 **[!UICONTROL 將元件拖曳到這裡]** 方塊並選取 **+.** 在 **[!UICONTROL 插入新元件]** 方塊，選取 **[!UICONTROL AEM表單]**. 此 **[!UICONTROL AEM Forms容器]** 元件會新增至頁面。
1. 選取 **[!UICONTROL AEM Forms容器]** 元件並選取 ![configure-icon](assets/configure-icon.svg). 具有AEM屬性的對話方塊 [!DNL Forms] 容器隨即顯示。 在 **[!UICONTROL 資產路徑]** 欄位，瀏覽並選取shipping-address-add-update-form最適化表單。 選取 ![儲存圖示](assets/save_icon.svg). 最適化表單已內嵌在頁面中。
1. 發佈最適化表單和 [!DNL Sites] 頁面。 以下是您需要考慮的幾點：

   * 如果您發佈AEM [!DNL Sites] 首次登入的頁面，且包含內嵌表單，發佈 [!DNL Sites] 頁面和內嵌表單。
   * 如果您只修改已發佈網站頁面中的內嵌表單，請發佈原始表單，所做的變更會反映在已發佈的網站頁面中。 已發佈的網站頁面包含對表單的引用，不需要重新發佈頁面。
   * 如果您修改 [!DNL Sites] 頁面和內嵌表單，重新發佈 [!DNL Sites] 頁面和表單。

     ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   將送貨與帳單地址變更表單新增至AEM [!DNL Sites] 頁面。

## 將最適化表單內嵌在外部網頁中 {#embed-the-adaptive-form-in-an-external-webpage}

您可以在外部網頁中插入幾行JavaScript，將調適型表單內嵌至外部網頁(託管在AEM外部的非AEM網頁)。 JavaScript程式碼會傳送HTTP要求給AEM [!DNL Forms] 最適化表單和相關資源的伺服器，並將最適化表單新增到網頁。 如需詳細步驟，請參閱 [將最適化表單內嵌至外部網頁](/help/forms/using/embed-adaptive-form-external-web-page.md).
