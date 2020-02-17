---
title: AEM Livefyre Recipes
seo-title: AEM Livefyre Recipes
description: Adobe Experience Manager Livefyre常見使用案例的逐步指示。
seo-description: Adobe Experience Manager Livefyre常見使用案例的逐步指示。
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# AEM Livefyre Recipes{#aem-livefyre-recipes}

Adobe Experience Manager Livefyre常見使用案例的逐步指示。

## 使用現成可用的Livefyre AEM元件來組織UGC，並使用Livefyre Media Wall來顯示 {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

媒體塗鴉牆將社交和原生Livefyre內容串流至即時社交塗鴉牆。 在AEM中實作媒體塗鴉牆有多種方式，視您的使用案例和需求而定。

AEM Livefyre套件提供現成可用的實作，而傳統整合則提供建立自訂Livefyre AEM元件的功能。

### AEM整合 {#aem-integration}

Livefyre Adobe Experience Manager套件適用於AEM 6.1、6.2SP1、6.3、6.4和6.4 SP1。 不支援AEM 5.x和6.0。 如需詳細指示，請參 [閱「與Livefyre整合」](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)。

若要查看支援哪些Livefyre應用程式，請參閱Livefyre應 [用程式的AEM支援矩陣](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)。

### 傳統實作（適用於自訂的AEM元件） {#traditional-implementation-for-customized-aem-components}

在自訂AEM元件或其他CMS（例如WordPress、Sitecore或DemandWare）中實作Livefyre有三種方式。 傳統的Livefyre整合不受CMS限制。

**方法1:設計人員應用程式實作**

* **** 什麼：整合Livefyre應用程式的最簡單、最快速方式。 您可以設計、設定並產生自訂的JavaScript內嵌程式碼，在幾分鐘內將媒體塗鴉牆應用程式整合在頁面上。
* **** 方式： 建 [立、預覽、發佈和內嵌媒體塗鴉牆應用程式](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** 範例： [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**方法2:SDK實作**

* **** 什麼：Livefyre [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) .js是核心資料庫，可為網站上的「應用程式」和「驗證」提供支援。 它定義全域 *window.Livefyre* 物件和單一公用方法 *Livefyre.require*，可用來載入其他Livefyre JavaScript程式庫，以協助內嵌Livefyre應用程式並與協力廠商使用者驗證平台整合。

* **方式**:使 [用Livefyre javaScript SDK的streamhub-wallpackage](https://marketing.adobe.com/resources/help/en_US/livefyre/?f=c_media_wall_app&s=c_media_wall_integration)

* **範例**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

如需使用SDK的進階自訂，請參閱 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk)。

**方法3:API實作**

* 若要建立自訂的體驗和資料視覺化，您可使用引導和串流API，從頭開始使用Livefyre和社交資料來 [建立Livefyre應用程式](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)。

在建立UGC的UI時，請 [確定您依照Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html)、 [Facebook](https://en.facebookbrand.com/guidelines/brand)和 [](https://en.instagram-brand.com/) Instagram的顯示准則。

### 媒體牆驗證整合 {#media-wall-authentication-integration}

如需驗證的媒體牆整合，請參閱：

* [自訂AEM身分識別管理](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 的單一登入整合
* [協力廠商驗證平台的Identity Integration](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) （識別整合）

### 使用案例概觀 {#use-case-overview}

身為AEM客戶，我想使用現成可用的Livefyre AEM元件來組織UGC，並使用Livefyre Media Wall來顯示：

實施步驟：

1. [快速入門](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [設定AEM以使用Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [將AEM Media Wall元件拖放至您的頁面](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [設定串流並新增規則以組織UGC並顯示在「媒體塗鴉牆」元件上](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)

如需有關串流UGC的訓練影片，請參 [閱「在Adobe Experience Manager Livefyre中建立自動內容串流和搜尋社交內容」](https://helpx.adobe.com/experience-manager/tutorials.html)。

### 客戶範例 {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA巡迴賽媒體牆](https://www.pgatour.com/social-hub.html)

若要建立自訂的體驗和資料視覺化，您可使用引導和串流API，從頭開始使用Livefyre和社交資料來 [建立Livefyre應用程式](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)。

若為需要驗證的Livefyre應用程式，請參閱 [協力廠商驗證平台的Identity Integration](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) 。

* [PGA巡迴賽媒體牆](https://www.pgatour.com/social-hub.html)
* [逾時](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## 使用AEM元件或傳統Livefyre整合整合Livefyre注釋 {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM整合 {#aem-integration-1}

Livefyre Adobe Experience Manager套件適用於AEM 6.1、6.2SP1、6.3、6.4和6.4 SP1。 不支援AEM 5.x和6.0。 如需詳細指示，請參 [閱「與Livefyre整合」](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)。

### 傳統實作（適用於自訂的AEM元件） {#traditional-implementation-for-customized-aem-components-1}

在自訂AEM元件或其他CMS（例如WordPress、Sitecore或DemandWare）中實作Livefyre注釋應用程式有三種方式。 傳統的Livefyre整合不受CMS限制。

**方法1:設計人員應用程式實作**

* **** 什麼：整合Livefyre應用程式的最簡單、最快速方式。 您可以設計、設定並產生自訂的JavaScript內嵌程式碼，在幾分鐘內將媒體塗鴉牆應用程式整合在頁面上。
* **** 方式：建 [立、預覽、發佈和內嵌注釋應用程式](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** 範例： [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**方法2:SDK實作**

* **** 什麼：Livefyre [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) .js是核心資料庫，可為網站上的「應用程式」和「驗證」提供支援。 它定義全域 *window.Livefyre* 物件和單一公用方法 *Livefyre.require*，可用來載入其他Livefyre JavaScript程式庫，以協助內嵌Livefyre應用程式並與協力廠商使用者驗證平台整合。

* **方式：**

   * 使用CollectionMeta Token建立系列/ [應用程式](https://marketing.adobe.com/resources/help/en_US/livefyre/t_create_a_collectionmeta_token.html)。
   * 使用 [Livefyre.js內嵌程式碼結構](https://marketing.adobe.com/resources/help/en_US/livefyre/c_comments_integration.html) ，將注釋應用程式整合至網站。

* **** 範例： [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

如需使用SDK的進階自訂，請參閱 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk)。

**方法3:API實作**

* 若要建立自訂的體驗和資料視覺化，您可使用引導和串流API，從頭開始使用Livefyre和社交資料來 [建立Livefyre應用程式](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)。

### 注釋應用程式驗證整合 {#comments-app-authentication-integration}

* [自訂AEM身分識別管理](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 的單一登入整合
* [協力廠商驗證平台的Identity Integration](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) （識別整合）

### 客戶範例 {#customer-examples-1}

* [Pose(Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## 使用Livefyre AEM Assets整合，在AEM Assets中匯入UGC {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre設定（適用於UGC組織與Rights Management）:**

1. [設定串流並新增規則，將UGC組織至Livefyre資產庫資料夾](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)。

   1. 如需有關串流UGC的訓練影片，請參 [閱「在Adobe Experience Manager Livefyre中建立自動內容串流和搜尋社交內容」](https://helpx.adobe.com/experience-manager/tutorials.html)。

1. [在Livefyre資產庫資料夾中收集、組織及管理精選的UGC](https://marketing.adobe.com/resources/help/en_US/livefyre/c_assets.html)。

   1. 如需有關在Livefyre studio資產庫中建立和管理資料夾的訓練影片，請參 [閱Adobe Experience Manager Livefyre中的「使用資產」](https://helpx.adobe.com/experience-manager/tutorials.html)。

1. [使用Livefyre studio申請優質的UGC的權利](https://marketing.adobe.com/resources/help/en_US/livefyre/c_how_requesting_rights_works.html)。

**AEM設定（用於將UGC匯入AEM Assets）:**

1. [快速入門](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [設定AEM以使用Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [將Livefyre組織的UGC匯入AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Tourism Australia](https://www.australia.com/en-us)

## 使用AEM元件或傳統Livefyre整合來整合Livefyre評論 {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM整合 {#aem-integration-2}

Livefyre Adobe Experience Manager套件適用於AEM 6.1、6.2SP1、6.3、6.4和6.4 SP1。 不支援AEM 5.x和6.0。 如需詳細指示，請參 [閱「與Livefyre整合」](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)。

Reviews Component不是AEM 6.1支援的元件。請檢查所有 [Livefyre應用程式的AEM支援矩陣](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)。

### 傳統實作（適用於自訂的AEM元件） {#traditional-implementation-for-customized-aem-components-2}

在自訂AEM元件或其他CMS（例如WordPress、Sitecore或DemandWare）中實作Livefyre Reviews應用程式有兩種方式。 傳統的Livefyre整合不受CMS限制。

**方法1:SDK實作**

* **** 什麼：Livefyre [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) .js是核心資料庫，可為網站上的「應用程式」和「驗證」提供支援。 它定義全域 *window.Livefyre* 物件和單一公用方法 *Livefyre.require*，可用來載入其他Livefyre JavaScript程式庫，以協助內嵌Livefyre應用程式並與協力廠商使用者驗證平台整合。

* **方式：**

   * 建立Reviews [CollectionMeta Token](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) ，以指定要儲存在Reviews Collection中的中繼資料。
   * 使用 [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) Livefyre.js內嵌程式碼結構，將Reviews App ** into Sites

* **** 範例： [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

如需使用SDK的進階自訂，請參閱 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk)。

**方法2:API實作**

* 若要建立自訂的體驗和資料視覺化，您可使用引導和串流API，從頭開始使用Livefyre和社交資料來建立Livefyre應用程式。

您可在這裡找到其他評分和評論 [API](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews)。

### 注釋應用程式驗證整合 {#comments-app-authentication-integration-1}

* [自訂AEM身分識別管理](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 的單一登入整合
* [協力廠商驗證平台的Identity Integration](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) （識別整合）

### 客戶範例 {#customer-examples-2}

* [逾時](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

