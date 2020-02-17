---
title: 建立和添加模板和元件
seo-title: 建立和添加模板和元件
description: 請依照本頁進行，以瞭解如何建立範本和元件並新增至您的應用程式。 頁面使用Geometrixx Unlimited App作為包含範例應用程式範本和頁面範本的應用程式。
seo-description: 請依照本頁進行，以瞭解如何建立範本和元件並新增至您的應用程式。 頁面使用Geometrixx Unlimited App作為包含範例應用程式範本和頁面範本的應用程式。
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 建立和添加模板和元件 {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

AEM Mobile On-Demand提供完整設定的應用程式範本、文章範本和文章元件。

We.Unlimited App是範例範本，代表可完全設定且可管理的AEM Mobile隨選應用程式的殼層。

建立新應用程式時選取此範例範本，可提供AEM mobile功能豐富式儀表板。

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>若要從AEM Mobile Apps Control Center管理您的應用程式和行動應用程式內容，請參閱 [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

## 建立應用程式範本 {#creating-app-templates}

應用程式範本可用來建立新應用程式，並當成頁面範本和元件的集合，這些範本和元件代表應用程式的基準或基礎。 範本會印出一些基本屬性，以適當的方式引導應用程式。 一般而言，客戶不會建立太多的應用程式。

應用程式範本提供簡單的方式，來運用開發人員建立的現有設計，以便在AEM中建立新應用程式。

根據其他應用程式的範本建立新應用程式時，您會得到一個應用程式，其起點代表建立應用程式的應用程式。

根據應用程式範本建立新應用程式的步驟：

1. 導覽至AEM mobile應用程式目錄： *&lt;server-url>/aem/apps.html/content/mobileapps*
1. 選擇「 **建立** —>應 **用程式** 」，如下所示

使用此範本建立應用程式後，您就可以將文章、橫幅和系列新增至應用程式。 若要重新造訪、建立文章、橫幅和系列，請參閱內容 [管理動作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)。

>[!NOTE]
>
>或者，您也可以選取AEM開發人員提供給您的範例應用程式範本，例如 **We.Unlimited** app。 如果您在應用程式中使用此範例範本，您會收到一些要處理的範例文章和系列。 您可以選擇使用範例範本和元件、自訂現有範本和元件，或為應用程式建立新範本和元件。

>[!CAUTION]
>
>設定 ***redirectTarget*** 屬性
>
>使用其中一個應用程式範本時，開發人員會定義應用程式的內容。 不過，開發人員必須知道應用程式在jcr中的建立位置以及redirectTarget屬 ***性的值*** 。
>
>redirectTarget ****** 是以建立應用程式作業的一部分來計算，如果應用程式範本中有redirectTarget屬性，且redirectTarget的值定義為相對，則會嘗試解析路徑。 當建立應用程式程式在應用程式範本中找到redirectTarget的相對值時，該值會附加至建立應用程式的已解析位置。
>
>例如，如果應用程式範本定義 ***redirectTarget*** ，其值為「*lanugage-masters/en*」，而應用程式是在「*/content/mobileapps/fooApp*」中建立，則在建立應用程式後重新導向Target的最終值將是「**/content/mobileapps/mobileapps/fooApp/language-masters」。


## 建立內容範本 {#creating-content-templates}

每個實體類型都有兩個現成的範本。 以下是：

* **** 預設範本：用於內容建立，具有適用的預設屬性／結構
* **** 匯入的範本：用於從AEM mobile匯入內容，並包含適用的預設屬性／結構

### 文章範本 {#article-templates}

「無限制文章」是代表典型AEM Mobile隨選文章版面的範例範本。

1. 按一下「管 **理文** 章」 **中的+** ，以建立新文章。 您可以選擇「不限 **數量的文章** 」或 **「Rich Text」文章**。 下圖顯示可讓您從這兩個文章範本中選擇的選項。

1. 按一 **下** 「下一步」以定義文章中繼資料，例如文章名稱／標題、說明、作者、抽象、部門、縮圖影像、文章存取等。
1. 按一 **下** 「下一步」以填入廣告屬性。
1. 按一 **下** 「下一步」以輸入文章影像或社交媒體影像
1. 按一 **下** 「下一步」，選擇此新文章的系列連結。
1. 按一 **下** 「下一步」，輸入社交共用的詳細資訊。
1. 按一 **下「建立** 」以完成使用範例建立文章的程式。 您可以按一 **下「完成** 」或「 **編輯文章** 」來編輯本文的屬性。

![chlimage_1-71](assets/chlimage_1-71.png)

### 新增元件至文章 {#adding-components-to-article}

建立後，作者就可以新增元件（例如文字和影像）來編輯文章的內容。 文章是AEM頁面範本的擴充功能。

選取文章，您要編輯，然後按一下「編 **輯** 」，將元件新增至文章。

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

選擇左側面&#x200B;**板上的&#39;**+&#39;，將元件新增至文章。

![chlimage_1-74](assets/chlimage_1-74.png)

### 建立現成可用的範本 {#creating-out-of-the-box-templates}

沒有現成的文章範本，但是自訂範本應該擴充的預設範本，請參閱Geometrixx Unlimited App&#39;s [Article範本範例](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article)。

超出一般AEM範本的關鍵屬性需要屬性包括；

***dps-resourceType=&quot;dps:Article&quot;***

此屬性可確保AEM頁面被識別為AEM mobile目標文章頁面。

依據AEM範本，您可以將任何預設屬性或子節點新增至範本的 ***jcr:content***。

### 橫幅和系列範本 {#banner-and-collection-templates}

>[!CAUTION]
>
>橫幅和系列沒有內容，因此其建立不支援自訂範本。

## 建立和添加元件 {#creating-and-adding-components}

元件使用並允許存取Widget，而這些元件則用來轉換內容。

程式碼儲存庫中包含簡單元件，其來源可在AEM中找到。 之後，也可在CRXDE Lite中在本機開啟。

>[!NOTE]
>
>目前AEM mobile沒有提供現成可用的元件。


您可以新增元件至頁面。 任何元件都可用於AEM mobile應用程式，但套用時可能無法正確呈現。

不過，若沒有在AEM中轉譯的自訂匯出內容同步處理常式，自訂元件可能無法正確匯出及上傳至AEM Mobile On-Demand Services。

在元件已包含在AEM頁面中，以及其他幾個建置區塊元件後，您就可以將另一個元件新增至頁面或編輯現有元件。

**要向頁面添加另一個元件：**

1. 選擇該頁面，並確保您處於編輯模式，方法是透過編輯器標題右上角的下拉式清單
1. 使用編輯器標題中最左側的圖示切換側面板
1. 選擇「組 **件** 」頁籤
1. 將其中一個可用元件拖放至頁面

![chlimage_1-75](assets/chlimage_1-75.png)

**要編輯現有元件：**

1. 選擇該頁面，並確定您處於「編 **輯** 」模式並選擇元件
1. 點選扳手圖示以設定元件

>[!NOTE]
>
>您可以在AEM中建立元件，並使用「使用CRXDE Lite開發」自 [訂相同的元件](/help/sites-developing/developing-with-crxde-lite.md)。 當您自訂現有元件做為需求後，就可以使用「管理文章」下的「編輯」選項，將它新增至頁面中，如上圖所示。 ********

>[!NOTE]
>
>請參閱「 [AEM mobile中範本和元件開發的最佳實務](/help/mobile/best-practices-aem-mobile.md) 」（英文）。

### 後續步驟 {#the-next-steps}

* [使用內容屬性匯出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [具備內容同步功能的行動裝置](/help/mobile/mobile-ondemand-contentsync.md)