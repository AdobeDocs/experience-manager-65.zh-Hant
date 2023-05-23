---
title: 「教程：發佈自適應表單」
seo-title: "Tutorial: Publish your adaptive form"
description: 將自適應表單發佈AEM為頁面，將表單嵌入到AEM Sites頁面，或將自適應表單嵌入到外部網頁
seo-description: Publish the adaptive form as an AEM page, embed the form to an AEM Sites page, or embed the adaptive form in an external webpage
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# 教程：發佈自適應表單 {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

本教程是 [建立第一個自適應窗體](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 的下界。 建議按時間順序按系列進行操作，以瞭解、執行和演示完整的教程使用案例。

自適應表單準備好後，您可以發佈該表單，使其可供最終用戶使用。 最終用戶可以在任何設備和網際網路瀏覽器上開啟發佈的表單。 當發佈自適應表單時，表單和相關內容從作者實AEM例複製到AEM發佈實例。 表單通過發佈實例提供給最終用戶。

您可以使用以下方法發佈自適應表單：

* [將自適應表單發佈為頁AEM面](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [在AEM Sites頁中嵌入自適應表單](#embed-the-adaptive-form-in-an-aem-sites-page)
* [將自適應表單嵌入到外部網頁(外部托管AEM的非網頁AEM)](../../forms/using/publish-your-adaptive-form.md)

## 開始之前 {#before-you-start}

* **[設定AEM Forms發佈實例](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:發佈實例是面向公共的實AEM例 [!DNL Forms] 在發佈模式下運行。 在生產環境中，發佈實例位於組織防火牆之外。
* **[設定複製和反向複製](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:複製將內容從作者實例複製到發佈實例，並將用戶輸入（例如，表單輸入）從發佈實例複製到作者實例。

## 將自適應表單發佈為頁AEM面 {#publish-the-adaptive-form-as-an-aem-page}

當自適應表單作為頁面發佈AEM時，整個網頁只包含已發佈表單。 可以使用自適應表單的URL從其他網頁連結它。 發佈 **裝運地址 — 添加 — 更新 — 表單** 自適應窗AEM體：

1. 登錄到AEM [!DNL Forms] 建立實例並在中查找shipping-address-add-update-form自適應表AEM單 [!DNL Forms] UI。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 選擇裝運地址 — 添加 — 更新 — 表單自適應表單並點擊 **[!UICONTROL 發佈]**。 顯示包含與自適應表單相關的資產的對話框。 點擊 **[!UICONTROL 發佈]**。 將發佈自適應表單，並顯示成功對話框。
1. 在發佈實例上開啟窗體。 表單可供最終用戶填寫和提交。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 在AEM Sites頁中嵌入自適應表單 {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] 允許窗體開發人員在 [!DNL Sites] 的子菜單。 嵌入式自適應表單功能齊全，用戶無需離開頁面即可填寫和提交表單。 它幫助用戶保持在網頁上其他元素的上下文中並同時與表單交互。

AEM [!DNL Forms] 提供元件AEM, [!DNL Forms] 容器，將自適應表單嵌入到 [!DNL Sites] 的子菜單。 預設情況下，元件在中不可AEM見 [!DNL Sites] 容器。 執行以下步驟以啟AEM用 [!DNL Forms] 容器元件和將自適應表單嵌入AEM [!DNL Sites] 頁面：

1. 在We.Retail網站中建立並開啟頁面進行編輯。 比如說， [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 自適應表單嵌入到 [!DNL Sites] 的子菜單。

   您還可以將自適應表單嵌入到現有We.Retail中 [!DNL Site's] 的子菜單。 例如，「關於美國」頁 [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 它為您節省了建立頁面的時間。 以下步驟使用新建立的頁面。

   We.Retail網站隨附AEM。 如果未安裝We.Retail站點，請參閱 [We.Retail Reference實施](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) 安裝站點。

1. 點擊 ![屬性](assets/properties.png) 頁面資訊並選擇 **[!UICONTROL 編輯模板]** 的子菜單。 頁面的模板將在瀏覽器的新頁籤中開啟。
1. 在 **[!UICONTROL 佈局容器]** 盒子和點擊 ![饋管](assets/feedmanagement.png)。 在 **[!UICONTROL 允許的元件]** 的 **[!UICONTROL 常規]** 折疊式，選擇 **[!UICONTROL 窗AEM體]** 選項，然後按一下 ![保存表徵圖](assets/save_icon.svg)。 AEM [!DNL Forms] 已為頁面啟用容器元件。

1. 開啟包含 [!DNL Sites] 的子菜單。 點擊 **[!UICONTROL 將元件拖動到此處]** 盒子和點擊 **+。** 在 **[!UICONTROL 插入新元件]** 框，點擊 **[!UICONTROL 窗AEM體]**。 的 **[!UICONTROL AEM Forms集裝箱]** 元件即添加到頁面。
1. 點擊 **[!UICONTROL AEM Forms集裝箱]** 元件和抽頭 ![配置表徵圖](assets/configure-icon.svg)。 具有以下屬性的對話AEM框 [!DNL Forms] 出現容器。 在 **[!UICONTROL 資產路徑]** 欄位中，瀏覽並選擇shipping-address-add-update-form自適應窗體。 點擊 ![保存表徵圖](assets/save_icon.svg)。 自適應表單嵌入到頁面中。
1. 同時發佈自適應窗體和 [!DNL Sites] 的子菜單。 以下是需要考慮的幾點：

   * 如果發佈AEM [!DNL Sites] 首次發佈，並且它包括嵌入的表單 [!DNL Sites] 的子菜單。
   * 如果僅修改已發佈網站頁中的嵌入表單，則發佈原始表單並將更改反映在已發佈網站頁中。 發佈的網站頁面包含對表單的引用，不需要重新發佈該頁面。
   * 如果修改 [!DNL Sites] 頁面和嵌入表單，重新發佈 [!DNL Sites] 的子菜單。

      ![嵌入式站點](assets/embed-in-aem-sites.png)
   添加到的發運和開單地址更改表AEM單 [!DNL Sites] 的子菜單。

## 將自適應表單嵌入到外部網頁 {#embed-the-adaptive-form-in-an-external-webpage}

通過在外部網頁中插入幾行JavaScript，可AEM以將自適AEM應表單嵌入到外部網頁（外部承載的非網頁）。 JavaScript代碼將HTTP請求發送到AEM [!DNL Forms] 伺服器，用於自適應表單和相關資源，並將自適應表單添加到網頁。 有關詳細步驟，請參見 [將自適應表單嵌入到外部網頁](/help/forms/using/embed-adaptive-form-external-web-page.md)。
