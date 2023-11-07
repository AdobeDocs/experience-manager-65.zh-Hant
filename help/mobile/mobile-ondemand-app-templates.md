---
title: 建立和新增範本和元件
seo-title: Creating and Adding Templates and Components
description: 請依照本頁面的說明進行，瞭解如何建立範本和元件並新增至您的應用程式。 頁面使用Geometrixx Unlimited應用程式作為包含範例應用程式範本和頁面範本的應用程式。
seo-description: Follow this page to learn about creating and adding templates and components to your app. The page uses Geometrixx Unlimited App as the app that contains a sample app template and page templates.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
exl-id: 5f050baa-fe10-4acc-ad32-de20793edc13
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---

# 建立和新增範本和元件 {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

AEM Mobile On-Demand提供完整設定的應用程式範本、文章範本和文章元件。

We.Unlimited應用程式是範例範本，代表可完整設定及管理的AEM Mobile隨選應用程式的外殼。

在建立應用程式時選取此範例範本，可提供AEM Mobile豐富的儀表板。

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>若要從AEM Mobile應用程式控制中心管理您的應用程式和行動應用程式內容，請參閱 [AEM Mobile應用程式控制面板](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

## 建立應用程式範本 {#creating-app-templates}

應用程式範本是用來建立應用程式，並作為頁面範本和元件的集合，代表應用程式的基準或基礎。 範本會列出一些基本屬性，以便以適當的方式領導應用程式。 一般而言，客戶不會建立太多應用程式。

應用程式範本可讓您輕鬆使用開發人員建立的現有設計，以便在AEM中建立新的應用程式。

根據其他應用程式的範本建立應用程式時，您會得到其起點代表在其中建立該應用程式之應用程式的應用程式。

根據應用程式範本建立應用程式的步驟：

1. 導覽至AEM Mobile應用程式目錄： *&lt;server-url>/aem/apps.html/content/mobileapps*
1. 選取 **建立** —> **應用程式** 如下所示

使用此範本建立應用程式後，您可以將文章、橫幅和集合新增至應用程式。 若要重新造訪、建立文章、橫幅和集合，請參閱 [內容管理動作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

>[!NOTE]
>
>您也可以選取範例應用程式範本，例如 **We.Unlimited** 應用程式，由AEM開發人員提供。 如果您的應用程式使用此範例範本，會取得一些要處理的範例文章和集合。 您可以選擇使用範例範本和元件、自訂現有範本和元件，或為應用程式建立新範本和元件。

>[!CAUTION]
>
>設定 ***redirecttarget*** 屬性
>
>使用其中一個應用程式範本時，開發人員會定義應用程式的內容。 不過，開發人員必須知道在jcr中建立應用程式的位置，以及 ***redirecttarget*** 屬性。
>
>此 ***redirecttarget*** 如果應用程式範本中有redirectTarget屬性可用，且redirectTarget的值定義為相對，系統會在建立應用程式操作過程中計算並嘗試解析路徑。 當建立應用程式程式在應用程式範本中找到redirectTarget的相對值時，該值會附加至建立應用程式的已解析位置。
>
>例如，如果應用程式範本定義 ***redirecttarget*** ，值為&quot;*lanugage-master/en*「」，而應用程式建立於「*/content/mobileapps/fooApp*&quot;，建立應用程式後，redirectTarget的最終值將會是&quot;*/content/mobileapps/fooApp/language-masters/en*「。
>

## 建立內容範本 {#creating-content-templates}

每個實體型別都有兩個現成的範本。 說明如下：

* **預設範本：** 用於建立具有適用預設屬性/結構的內容
* **匯入的範本：** 用於從AEM Mobile匯入內容，並具備適用的預設屬性/結構

### 文章範本 {#article-templates}

Unlimited文章是範例範本，代表典型的AEM Mobile隨選文章版面。

1. 在 **管理文章**，選取 **+**  以建立文章。 您可以選擇 **Unlimited文章** 或 **RTF文章**. 下圖顯示的選項可讓您從這兩個文章範本的任何一個中進行選擇。

1. 按一下 **下一個** 定義文章中繼資料，例如文章名稱/標題、說明、作者、摘要、部門、縮圖影像、文章存取權等。
1. 按一下 **下一個** 填入廣告屬性。
1. 按一下 **下一個** 若要輸入文章影像或社群媒體影像
1. 按一下 **下一個** 以選擇此新文章的集合連結。
1. 按一下 **下一個** 以輸入社交分享的詳細資料。
1. 按一下 **建立** 以使用範例完成建立文章的程式。 您可以按一下 **完成** 或 **編輯文章** 編輯本文的內容。

![chlimage_1-71](assets/chlimage_1-71.png)

### 新增元件至文章 {#adding-components-to-article}

建立後，作者可以新增文字和影像等元件來編輯文章內容。 文章是AEM頁面範本的擴充功能。

選取要編輯的文章，然後按一下 **編輯** 將元件新增至文章。

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

選擇&#39;**+**」以新增元件至文章。

![chlimage_1-74](assets/chlimage_1-74.png)

### 建立現成可用的範本 {#creating-out-of-the-box-templates}

沒有立即可用的文章範本，不過自訂範本有應擴充的預設範本，請參閱Geometrixx Unlimited應用程式的 [文章範本範例](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article).

超出一般AEM範本必要屬性的關鍵屬性包括；

***dps-resourceType=&quot;dps：Article&quot;***

此屬性可確保將AEM頁面辨識為AEM Mobile目標文章頁面。

根據AEM範本，您可以將任何預設屬性或子節點新增到範本的 ***jcr：content***.

### 橫幅和系列範本 {#banner-and-collection-templates}

>[!CAUTION]
>
>橫幅和集合沒有內容，因此其建立不支援自訂範本。

## 建立和新增元件 {#creating-and-adding-components}

元件會使用並允許存取Widget，且這些元件會用於轉譯內容。

程式碼存放庫中包含簡單元件，其來源可以在AEM中找到。 接著，也可以在CRXDE Lite本機開啟它。

>[!NOTE]
>
>目前沒有為AEM Mobile提供的現成元件。
>

您可以將元件新增至頁面。 任何元件都可以在AEM Mobile應用程式中使用，但在套用時，可能無法正確呈現。

不過，若無在AEM中轉譯的自訂匯出內容同步處理常式，自訂元件可能無法正確地匯出並上傳至AEM Mobile On-demand Services。

一旦元件已連同數個其他建置區塊元件納入AEM頁面，您就可以新增其他元件至頁面或編輯現有元件。

**新增其他元件至頁面：**

1. 選擇頁面，並透過編輯器標題右上角的下拉式清單，確定您處於編輯模式
1. 使用編輯器標題中最左側的圖示切換側面板
1. 選取 **元件** 標籤
1. 將其中一個可用元件拖放至頁面

![chlimage_1-75](assets/chlimage_1-75.png)

**若要編輯現有元件，請執行下列動作：**

1. 選擇該頁面，並確保您位於 **編輯** 模式並選取元件
1. 點選扳手圖示以設定元件

>[!NOTE]
>
>您可以在AEM中建立元件，並使用自訂相同的元件 [使用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md). 一旦您根據需求自訂了現有的元件，您就可以使用 **編輯** 下的選項 **管理文章** 如上圖所示。

>[!NOTE]
>
>請參閱 [範本和元件開發的最佳作法](/help/mobile/best-practices-aem-mobile.md) 在AEM Mobile中。

### 後續步驟 {#the-next-steps}

* [使用內容屬性匯出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [具有內容同步功能的行動裝置](/help/mobile/mobile-ondemand-contentsync.md)
