---
title: 建立和添加模板和元件
seo-title: Creating and Adding Templates and Components
description: 請按照此頁瞭解如何建立模板和元件並將其添加到應用。 該頁使用Geometrixx Unlimited應用作為包含示例應用模板和頁面模板的應用。
seo-description: Follow this page to learn about creating and adding templates and components to your app. The page uses Geometrixx Unlimited App as the app that contains a sample app template and page templates.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
exl-id: 5f050baa-fe10-4acc-ad32-de20793edc13
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# 建立和添加模板和元件 {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

AEM Mobile按需提供完全配置的應用模板、文章模板和文章元件。

We.Unlimited App是一個示例模板，代表完全可配置和可管理的AEM Mobile按需應用程式的外殼。

建立新應用時選擇此示例模板將提供AEM Mobile功能豐富的儀表板。

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>要從AEM Mobile應用控制中心管理您的應用程式和移動應用程式內容，請參閱 [AEM Mobile應用程式儀表板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

## 建立應用模板 {#creating-app-templates}

應用模板用於建立新應用，並用作表示應用基線或基礎的頁面模板和元件的集合。 模板會標籤一些基本屬性，以便以適當的方式引導應用。 通常，客戶不會總體建立太多應用。

應用程式模板提供了一種利用開發人員建立的現有設計的簡便方法，這些設計用於在中建立新應AEM用。

在基於另一個應用的模板建立新應用時，您將得到一個應用，該應用的起始點代表從中建立該應用的應用。

基於應用模板建立新應用的步驟：

1. 導航到AEM Mobile應用目錄： *&lt;server-url>/aem/apps.html/內容/移動應用*
1. 選擇 **建立** —> **應用** 如下所示

使用此模板建立應用後，您可以將文章、條幅和集合添加到應用。 要重新訪問、建立文章、橫幅和收藏，請參閱 [內容管理操作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)。

>[!NOTE]
>
>或者，您也可以選擇示例應用模板，例如 **無限** 應用程式，由開發人員提供AEM給您。 如果您將此示例模板用於您的應用，則您將獲得一些要處理的示例文章和集合。 您可以選擇使用示例模板和元件、自定義現有模板和元件，或為您的應用建立新模板和元件。

>[!CAUTION]
>
>設定 ***重定向目標*** 屬性
>
>使用其中一個應用模板時，開發人員定義應用程式的內容。 但是，開發人員必須知道在jcr中建立應用程式的位置以及 ***重定向目標*** 屬性。
>
>的 ***重定向目標*** 作為建立應用程式操作的一部分進行計算，並嘗試解析路徑（如果有redirectTarget屬性可作為應用程式模板的一部分），並且redirectTarget的值定義為相對。 當建立應用程式進程在應用程式模板中找到redirectTarget的相對值時，該值將附加到應用程式建立位置的解析位置。
>
>例如，如果應用模板定義 ***重定向目標*** 值為&quot;*拉努加格大師/昂*&#39;&#39;，並且應用是在&#39;&#39;*/content/mobileapps/fooApp*&quot;，建立應用後redirectTarget的最終值將為&quot;*/content/mobileapps/fooApp/language-masters/en*。

## 建立內容模板 {#creating-content-templates}

每個圖元類型都有兩個現成的模板。 說明如下：

* **預設模板：** 用於使用適用的預設屬性/結構建立內容
* **導入的模板：** 用於從AEM Mobile導入內容，具有適用的預設屬性/結構

### 文章模板 {#article-templates}

「無限制文章」是表示典型AEM Mobile按需文章佈局的示例模板。

1. 按一下 **+** 在 **管理文章** 的子菜單。 您可以選擇 **無限制文章** 或 **富文本文章**。 下圖顯示了允許您從以下兩種文章模板中選擇的選項。

1. 按一下 **下一個** 定義文章元資料，如文章名稱/標題、說明、作者、抽象、部門、縮略圖、文章訪問等。
1. 按一下 **下一個** 來填充播發屬性。
1. 按一下 **下一個** 輸入文章影像或社交媒體影像
1. 按一下 **下一個** 選擇此新文章到的集合連結。
1. 按一下 **下一個** 中各屬性的附加資訊。
1. 按一下 **建立** 完成使用示例建立項目的過程。 按一下 **完成** 或 **編輯文章** 編輯此文章的屬性。

![chlimage_1-71](assets/chlimage_1-71.png)

### 向文章添加元件 {#adding-components-to-article}

建立後，作者可以通過添加文本和影像等元件來編輯文章的內容。 文章是頁面模AEM板的擴展。

選擇要編輯的文章，然後按一下 **編輯** 添加元件。

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

選擇「**+**」，將元件添加到文章中。

![chlimage_1-74](assets/chlimage_1-74.png)

### 建立現成模板 {#creating-out-of-the-box-templates}

沒有現成的文章模板，但是有一個預設模板應該擴展，請參閱Geometrixx Unlimited應用 [文章模板示例](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article)。

除普通模板外的關鍵屬AEM性要求屬性包括：

***dps-resourceType=&quot;dps:Article&quot;***

此屬性確保AEM該頁面被識別為AEM Mobile目標文章頁面。

根據模AEM板，您可以將任何預設屬性或子節點添加到模板的 ***jcr：內容***。

### 橫幅和集合模板 {#banner-and-collection-templates}

>[!CAUTION]
>
>條幅和集合沒有內容，因此其建立不支援自定義模板。

## 建立和添加元件 {#creating-and-adding-components}

元件使用和允許訪問小部件，這些元件用於呈現內容。

代碼儲存庫中包含一個簡單元件，其源位於中AEM。 隨後，也可以在本地以CRXDE Lite開啟。

>[!NOTE]
>
>目前沒有為AEM Mobile提供現成的元件。

可以將元件添加到頁面。 任何元件都可以在AEM Mobile應用中使用，但應用時可能無法正確呈現。

但是，如果沒有在中呈現的自定義導出內容同步處理程式，自定義元件可能無法正確導出並上載到AEM Mobile On-demand ServicesAEM。

一旦元件已包括在頁面中AEM，以及幾個其它構建塊元件，您就可以將另一個元件添加到頁面或編輯現有元件。

**要向頁面添加其他元件：**

1. 選擇該頁面，並確保您處於編輯模式，通過編輯器標題右上角的下拉清單
1. 使用編輯器標題中最左側的表徵圖切換側面板
1. 選擇 **元件** 頁籤
1. 將其中一個可用元件拖放到頁面上

![chlimage_1-75](assets/chlimage_1-75.png)

**要編輯現有元件：**

1. 選擇該頁面並確保您 **編輯** 模式並選擇元件
1. 點擊扳手錶徵圖以配置元件

>[!NOTE]
>
>可以在中建立元件，AEM並使用 [用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md)。 將現有元件自定義為您的要求後，可以使用 **編輯** 選項 **管理文章** 如上圖所示。

>[!NOTE]
>
>請參閱 [模板和元件開發的最佳做法](/help/mobile/best-practices-aem-mobile.md) 在AEM Mobile。

### 後續步驟 {#the-next-steps}

* [使用內容屬性導出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [帶內容同步的移動](/help/mobile/mobile-ondemand-contentsync.md)
