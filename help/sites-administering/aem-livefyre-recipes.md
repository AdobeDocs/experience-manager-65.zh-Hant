---
title: AEM Livefyre 指導方針
seo-title: AEM Livefyre Recipes
description: Adobe Experience Manager Livefyre 常見使用案例的逐步指示。
seo-description: Step-by-step instructions on common use cases for Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
exl-id: 7ccd67a7-9945-48c1-9986-f4eaf0f2b961
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 4%

---

# AEM Livefyre 指導方針{#aem-livefyre-recipes}

Adobe Experience Manager Livefyre 常見使用案例的逐步指示。

## 使用現成可用的Livefyre AEM元件組織UGC，並使用Livefyre Media Wall顯示 {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

媒體塗鴉牆可將社交和原生Livefyre內容串流至即時社交塗鴉牆中。 根據您的使用案例和需求，有多種方式可在AEM中實作Media Wall。

AEM Livefyre套件提供現成可用的實作，而傳統整合則可提供建立自訂Livefyre AEM元件的功能。

### AEM整合 {#aem-integration}

AEM 6.1、6.2SP1、6.3、6.4和6.4 SP1可使用Livefyre Adobe Experience Manager套件。 不支援AEM 5.x和6.0。 如需詳細指示，請參閱 [與Livefyre整合](https://helpx.adobe.com/tw/experience-manager/6-4/sites/administering/using/livefyre.html).

若要查看哪些Livefyre應用程式受支援，請參閱 [Livefyre應用程式的AEM支援對照表](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### 傳統實作(適用於自訂的AEM元件) {#traditional-implementation-for-customized-aem-components}

有三種方式可將Livefyre實施至自訂AEM元件或其他CMS，例如WordPress、Sitecore或DemandWare。 傳統的Livefyre整合不受CMS限制。

**方法1:設計器應用程式實作**

* **什麼：** 整合Livefyre應用程式最簡單、最快速的方式。 您可以設計、設定及產生自訂的JavaScript內嵌程式碼，以便在數分鐘內整合頁面上的媒體塗鴉牆應用程式。
* **方法：**  [建立、預覽、發佈和內嵌媒體塗鴉牆應用程式](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **範例：** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**方法2:SDK實作**

* **什麼：** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) 是核心程式庫，為網站上的應用程式和驗證提供技術支援。 它定義了全球 *window.Livefyre* 物件和單一公用方法， *Livefyre.require*，可載入其他Livefyre JavaScript程式庫，協助內嵌Livefyre應用程式並與協力廠商使用者驗證平台整合。

* **如何**: [使用Livefyre JavaScript SDK的streamhub-wallpackage](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **範例**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

有關使用SDK的進階自訂，請參閱 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**方法3:API實作**

* 若要建立自訂的體驗和資料視覺效果，您可以使用 [Bootstrap和串流API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

請務必遵循 [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand)，和 [Instagram](https://en.instagram-brand.com/) 建置UGC的UI時顯示准則。

### Media Wall驗證整合 {#media-wall-authentication-integration}

若為需要驗證的媒體塗鴉牆整合，請參閱：

* [自訂單一登入整合](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 適用於AEM Identity Management
* [身分整合](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 適用於第三方驗證平台

### 使用案例概述 {#use-case-overview}

身為AEM客戶，我想使用現成可用的Livefyre AEM元件來組織UGC，並使用Livefyre Media Wall來顯示：

實作步驟：

1. [快速入門](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [設定AEM以使用Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [將AEM Media Wall元件拖放至頁面](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [設定串流並新增規則以組織UGC並顯示在「媒體塗鴉牆」元件上](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html)

有關流式處理UGC的培訓視頻，請參見 [在Adobe Experience Manager Livefyre中建立自動內容資料流並搜尋社交內容](https://helpx.adobe.com/experience-manager/tutorials.html).

### 客戶範例 {#customer-examples}

* [CNN傳媒城](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA巡迴賽媒體牆](https://www.pgatour.com/social-hub.html)

若要建立自訂的體驗和資料視覺效果，您可以使用 [Bootstrap和串流API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

若為需要驗證的Livefyre應用程式，請參閱 [身分整合](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 適用於第三方驗證平台。

* [PGA巡迴賽媒體牆](https://www.pgatour.com/social-hub.html)
* [逾時](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## 使用AEM元件整合Livefyre意見或傳統Livefyre整合 {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM整合 {#aem-integration-1}

AEM 6.1、6.2SP1、6.3、6.4和6.4 SP1可使用Livefyre Adobe Experience Manager套件。 不支援AEM 5.x和6.0。 如需詳細指示，請參閱 [與Livefyre整合](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### 傳統實作(適用於自訂的AEM元件) {#traditional-implementation-for-customized-aem-components-1}

有三種方式可將Livefyre意見應用程式實作至自訂AEM元件或其他CMS，例如WordPress、Sitecore或DemandWare。 傳統的Livefyre整合不受CMS限制。

**方法1:設計器應用程式實作**

* **什麼：** 整合Livefyre應用程式最簡單、最快速的方式。 您可以設計、設定及產生自訂的JavaScript內嵌程式碼，以便在數分鐘內整合頁面上的媒體塗鴉牆應用程式。
* **方法：** [建立、預覽、發佈和內嵌注釋應用程式](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **範例：** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**方法2:SDK實作**

* **什麼：** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) 是核心程式庫，為網站上的應用程式和驗證提供技術支援。 它定義了全球 *window.Livefyre* 物件和單一公用方法， *Livefyre.require*，可載入其他Livefyre JavaScript程式庫，協助內嵌Livefyre應用程式並與協力廠商使用者驗證平台整合。

* **方法：**

   * 使用建立集合/應用程式 [CollectionMeta代號](https://experienceleague.adobe.com/docs/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * 整合 [評論應用程式](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/comments/c-comments-integration.html) 內嵌程式碼結構移入網站。

* **範例：**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

如需使用SDK的進階自訂，請參閱 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**方法3:API實作**

* 若要建立自訂的體驗和資料視覺效果，您可以使用 [Bootstrap和串流API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Comments應用驗證整合 {#comments-app-authentication-integration}

* [自訂單一登入整合](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 適用於AEM Identity Management
* [身分整合](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 適用於第三方驗證平台

### 客戶範例 {#customer-examples-1}

* [普瓦斯（金伯利·克拉克）](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## 使用Livefyre AEM Assets整合以在AEM Assets中匯入UGC {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre設定(針對UGC組織與Rights Management):**

1. [設定串流並新增規則以組織UGC至Livefyre資產資料庫資料夾](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html).

   1. 有關流式處理UGC的培訓視頻，請參見 [在Adobe Experience Manager Livefyre中建立自動內容資料流並搜尋社交內容](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [在Livefyre Asset Library資料夾中收集、組織及管理已組織的UGC](https://experienceleague.adobe.com/docs/livefyre/using/library/assets/c-assets.html).

   1. 如需有關在Livefyre Studio Asset Library中建立和管理資料夾的訓練影片，請參閱 [在Adobe Experience Manager Livefyre中使用Assets](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [使用Livefyre Studio的已組織UGC請求權限](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**AEM設定(用於將UGC匯入AEM Assets):**

1. [快速入門](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [設定AEM以使用Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [將Livefyre策劃的UGC匯入AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [澳大利亞旅遊](https://www.australia.com/en-us)

## 使用AEM元件或傳統Livefyre整合整合Livefyre審核 {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM整合 {#aem-integration-2}

AEM 6.1、6.2SP1、6.3、6.4和6.4 SP1可使用Livefyre Adobe Experience Manager套件。 不支援AEM 5.x和6.0。 如需詳細指示，請參閱 [與Livefyre整合](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

查看元件不是AEM 6.1支援的元件。請檢查 [AEM所有Livefyre應用程式的支援矩陣](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### 傳統實作(適用於自訂的AEM元件) {#traditional-implementation-for-customized-aem-components-2}

有兩種方式可將Livefyre Reviews App實作至自訂AEM元件或其他CMS，例如WordPress、Sitecore或DemandWare。 傳統的Livefyre整合不受CMS限制。

**方法1:SDK實作**

* **什麼：** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) 是核心程式庫，為網站上的應用程式和驗證提供技術支援。 它定義了全球 *window.Livefyre* 物件和單一公用方法， *Livefyre.require*，可載入其他Livefyre JavaScript程式庫，協助內嵌Livefyre應用程式並與協力廠商使用者驗證平台整合。

* **方法：**

   * 建立審核 [CollectionMeta代號](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) 指定要在「審閱集合」中儲存的元資料。
   * 整合 [評論應用程式](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) 使用 *Livefyre.js* 內嵌程式碼結構

* **範例：**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

如需使用SDK的進階自訂，請參閱 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**方法2:API實作**

* 若要建立自訂的體驗和資料視覺效果，您可使用Bootstrap和串流API來使用Livefyre和社交資料，從草稿開始建立Livefyre應用程式。

您可以找到其他評等和審核API [此處](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Comments應用驗證整合 {#comments-app-authentication-integration-1}

* [自訂單一登入整合](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 適用於AEM Identity Management
* [身分整合](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 適用於第三方驗證平台

### 客戶範例 {#customer-examples-2}

* [逾時](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)
