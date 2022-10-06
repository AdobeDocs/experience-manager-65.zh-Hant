---
title: 建立和新增範本和元件
seo-title: Creating and Adding Templates and Components
description: 請參照本頁面，了解如何建立範本和元件並新增至您的應用程式。 頁面使用Geometrixx Unlimited應用程式作為包含範例應用程式範本和頁面範本的應用程式。
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

# 建立和新增範本和元件 {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM Mobile On-Demand提供完整設定的應用程式範本、文章範本和文章元件。

We.Unlimited App是範例範本，代表可完全設定且可管理的AEM Mobile On-Demand應用程式的殼層。

建立新應用程式時選取此範本，可提供AEM Mobile功能豐富的控制面板。

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>若要從AEM Mobile Apps Control Center管理您的應用程式和行動應用程式內容，請參閱 [AEM Mobile應用程式控制面板](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

## 建立應用程式範本 {#creating-app-templates}

應用程式範本可用來建立新應用程式，並可作為頁面範本和元件的集合，這些範本和元件代表應用程式的基準或基礎。 範本會戳記某些基本屬性，以適當方式引導應用程式。 一般而言，客戶不會總建立太多應用程式。

應用程式範本可讓您輕鬆運用開發人員建立的現有設計，以在AEM內建立新應用程式。

根據其他應用程式的範本建立新應用程式時，您會得到一個應用程式，其起始點代表建立該應用程式時所在的應用程式。

根據應用程式範本建立新應用程式的步驟：

1. 導覽至AEM Mobile應用程式目錄： *&lt;server-url>/aem/apps.html/content/mobileapps*
1. 選擇 **建立** —> **應用程式** 如下所示

使用此範本建立應用程式後，您就可以將文章、橫幅和集合新增至應用程式。 若要重新造訪、建立文章、橫幅和集合，請參閱 [內容管理動作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

>[!NOTE]
>
>或者，您也可以選取範例應用程式範本，例如 **We.Unlimited** 應用程式，由AEM開發人員提供給您。 如果您將此範例範本用於應用程式，您會看到一些範例文章和集合可供使用。 您可以選擇使用範本和元件範例、自訂現有範本和元件，或為應用程式建立新範本和元件。

>[!CAUTION]
>
>設定 ***redirectTarget*** 屬性
>
>使用其中一個應用程式範本時，開發人員會定義應用程式的內容。 不過，開發人員必須知道應用程式在jcr中建立的位置，以及 ***redirectTarget*** 屬性。
>
>此 ***redirectTarget*** 會計算為建立應用程式操作的一部分，並嘗試解析路徑（如果應用程式範本中有可用的redirectTarget屬性，且redirectTarget的值定義為相對）。 當建立應用程式程式在應用程式範本中找到redirectTarget的相對值時，該值會附加至建立應用程式的解析位置。
>
>例如，如果應用程式範本定義 ***redirectTarget*** 值為&quot;*拉努加吉·馬斯特斯/恩*」，而應用程式是在「*/content/mobileapps/fooApp*&quot;，在建立應用程式後redirectTarget的最終值將是&quot;*/content/mobileapps/fooApp/language-masters/en*」。

## 建立內容範本 {#creating-content-templates}

每個實體類型都有兩個現成的範本。 說明如下：

* **預設範本：** 用適用的預設屬性/結構建立內容
* **導入的模板：** 用於從AEM Mobile匯入內容，且適用的預設屬性/結構

### 文章範本 {#article-templates}

「無限制文章」是代表典型AEM Mobile隨選文章版面的範例範本。

1. 按一下 **+** in **管理文章** 來建立新文章。 您可以選擇 **無限制文章** 或 **RTF文章**. 下圖顯示的選項可讓您從這兩個文章範本中選擇任何一個。

1. 按一下 **下一個** 定義文章元資料，例如「文章名稱/標題」、「說明」、「作者」、「抽象」、「部門」、「縮圖影像」、「文章存取」等。
1. 按一下 **下一個** 填寫廣告屬性。
1. 按一下 **下一個** 輸入文章影像或社交媒體影像
1. 按一下 **下一個** 來選擇此新文章的集合連結。
1. 按一下 **下一個** 以輸入社交分享的詳細資訊。
1. 按一下 **建立** 以完成使用範例建立文章的程式。 按一下 **完成** 或 **編輯文章** 編輯此文章的屬性。

![chlimage_1-71](assets/chlimage_1-71.png)

### 新增元件至文章 {#adding-components-to-article}

建立後，作者可以新增文字和影像等元件來編輯文章的內容。 文章是AEM頁面範本的擴充功能。

選取要編輯的文章，然後按一下 **編輯** 新增元件至文章。

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

選擇「**+**「 」，將元件新增至文章。

![chlimage_1-74](assets/chlimage_1-74.png)

### 建立現成可用的範本 {#creating-out-of-the-box-templates}

沒有現成可用的文章範本，不過自訂範本有應擴充的預設範本，請參閱Geometrixx Unlimited應用程式的 [文章範本範例](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article).

一般AEM範本以外的關鍵屬性需要屬性包括；

***dps-resourceType=&quot;dps:Article&quot;***

此屬性可確保將AEM頁面辨識為AEM Mobile目標文章頁面。

如同AEM範本，您可以將任何預設屬性或子節點新增至範本的 ***jcr:content***.

### 橫幅和系列範本 {#banner-and-collection-templates}

>[!CAUTION]
>
>橫幅和集合沒有內容，因此其建立不支援自訂範本。

## 建立和新增元件 {#creating-and-adding-components}

元件使用和允許訪問Widget，這些用於呈現內容。

程式碼存放庫中包含簡單元件，可在AEM中找到其來源。 隨後，也可以在本地以CRXDE Lite開啟。

>[!NOTE]
>
>目前未提供現成可用的AEM Mobile元件。

您可以將元件新增至頁面。 任何元件皆可用於AEM Mobile應用程式中，但套用後，可能無法正確呈現。

不過，若沒有可在AEM中轉譯的自訂匯出內容同步處理常式，自訂元件可能無法正確匯出及上傳至AEM Mobile On-demand Services。

在元件已包含在AEM頁面中後，您就可以新增其他元件至頁面或編輯現有的元件，以及搭配一些其他建置區塊元件。

**若要新增其他元件至頁面：**

1. 選擇該頁面，並透過編輯器標題右上角的下拉式清單，確定您處於編輯模式
1. 使用編輯器標題中最左側的圖示切換側面板
1. 選取 **元件** 標籤
1. 將其中一個可用元件拖放至頁面上

![chlimage_1-75](assets/chlimage_1-75.png)

**要編輯現有元件，請執行以下操作：**

1. 選擇該頁面，並確定您位於 **編輯** 模式並選取元件
1. 點選扳手圖示以設定元件

>[!NOTE]
>
>您可以在AEM中建立元件，並使用 [使用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md). 將現有元件自訂為您的需求後，即可使用 **編輯** 選項 **管理文章** 如上圖所示。

>[!NOTE]
>
>請參閱 [範本和元件開發的最佳實務](/help/mobile/best-practices-aem-mobile.md) 在AEM Mobile。

### 後續步驟 {#the-next-steps}

* [使用內容屬性來匯出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [具有內容同步的行動裝置](/help/mobile/mobile-ondemand-contentsync.md)
