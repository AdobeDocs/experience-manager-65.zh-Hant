---
title: Social元件架構
seo-title: Social元件架構
description: 社交元件架構(SCF)可簡化設定、自訂和擴充社群元件的程式
seo-description: 社交元件架構(SCF)可簡化設定、自訂和擴充社群元件的程式
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Social元件架構 {#social-component-framework}

社交元件架構(SCF)可簡化在伺服器端和用戶端上設定、自訂和擴充社群元件的程式。

該框架的優點：

* **功能**:80%的使用案例只需少量或不需自訂，即可輕鬆整合
* **可變更外觀**:CSS樣式的HTML屬性使用一致
* **可擴充**:元件實施是物件導向的，並輕鬆處理業務邏輯——易於在伺服器上添加增量業務登錄
* **彈性**:簡單、無邏輯的Javascript範本，可輕鬆覆蓋和自訂
* **可存取**:HTTP API支援從任何用戶端發佈內容，包括行動應用程式
* **可攜式**:整合／嵌入任何以任何技術為基礎的網頁

使用互動式社群元件指南，探索作者或發佈 [例項](components-guide.md)。

## 概覽 {#overview}

在SCF中，元件由SocialComponent POJO、Handlebars JS範本（用於轉換元件）和CSS（用於設定元件樣式）組成。

Handlebars JS範本可擴充模型／檢視JS元件，以處理使用者與用戶端上元件的互動。

如果元件需要支援資料修改，則可編寫SocialComponent API的實作，以支援編輯／儲存類似傳統Web應用程式中模型／資料物件的資料。 此外，可以添加操作（控制器）和操作服務以處理操作請求、執行業務邏輯和調用模型／資料對象上的API。

SocialComponent API可擴充，以提供用戶端對檢視層或HTTP用戶端所需的資料。

### 如何為客戶呈現頁面 {#how-pages-are-rendered-for-client}

![chlimage_1-25](assets/chlimage_1-25.png)

### 元件自訂與擴充功能 {#component-customization-and-extension}

若要自訂或擴充元件，您只需將覆蓋和擴充功能寫入/apps目錄，以簡化升級至未來版本的程式。

* 針對外觀設定
   * 只有 [CSS需要編輯](client-customize.md#skinning-css)
* 外觀和感覺
   * 變更JS範本和CSS
* 針對外觀、感覺和UX
   * 變更JS範本、CSS和擴充／覆 [寫Javascript](client-customize.md#extending-javascript)
* 修改JS範本或GET端點的可用資訊
   * 擴充 [SocialComponent](server-customize.md#socialcomponent-interface)
* 在操作過程中添加自定義處理
   * 編寫 [OperationExtension](server-customize.md#operationextension-class)
* 若要新增自訂作業
   * 建立新的 [Sling Post Operation](server-customize.md#postoperation-class)
   * 視需要使 [用現有的OperationServices](server-customize.md#operationservice-class)
   * 視需要新增Javascript程式碼，從用戶端叫用您的作業

## 伺服器端架構 {#server-side-framework}

此架構提供API來存取伺服器上的功能，並支援用戶端與伺服器之間的互動。

### Java API {#java-apis}

Java API提供可輕鬆繼承或子分類的抽象類別和介面。

主類在「伺服器端定 [制」頁中介紹](server-customize.md) 。

請造 [訪儲存資源提供商概述](srp.md) ，以瞭解如何使用UGC。

### HTTP API {#http-api}

HTTP API支援PhoneGap應用程式、原生應用程式和其他整合與綜合應用程式的輕鬆自訂和用戶端平台選擇。 此外，HTTP API允許社區站點作為服務運行，而無需客戶端，這樣框架元件就可以整合到任何基於任何技術構建的網頁中。

### HTTP API —— 取得要求 {#http-api-get-requests}

對於每個SocialComponent，架構都提供以HTTP為基礎的API端點。 透過傳送GET要求至具有「.social.json」選擇器+副檔名的資源，即可存取端點。 使用Sling，請求即會遞交至 `DefaultSocialGetServlet`。

The `DefaultSocialGetServlet`

1. 將資源(resourceType)傳遞至， `SocialComponentFactoryManager`並接收能夠選擇表示資源 `SocialComponent`的SocialComponentFactory。

1. 調用工廠並接收 `SocialComponent`能夠處理資源和請求的。
1. 叫用 `SocialComponent`處理請求並傳回結果的JSON表示法。
1. 傳回JSON回應給用戶端。

**`GET Request`**

預設的GET servlet會監聽SocialComponent以可自訂JSON回應的。social.json請求。

![chlimage_1-26](assets/chlimage_1-26.png)

### HTTP API —— 貼文要求 {#http-api-post-requests}

除了GET（讀取）操作之外，框架還定義了端點模式，以便對元件啟用其他操作，包括建立、更新和刪除。 這些端點是HTTP API，可接受輸入並以HTTP狀態碼或JSON回應物件回應。

該框架端點模式使CUD操作具有可擴充性、可重用性和可測試性。

**`POST Request`**

每個SocialComponent作業都有Sling POST:operation。 每個操作的業務邏輯和維護代碼都包在OperationService中，該OperationService可通過HTTP API或從其他位置作為OSGi服務訪問。 提供了支援可插拔操作擴展的鈎子，用於前／後動作。

![chlimage_1-27](assets/chlimage_1-27.png)

### 儲存資源提供商(SRP) {#storage-resource-provider-srp}

若要瞭解如何處理儲存在社群內容 [商店的UGC](working-with-srp.md)，請參閱

* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP API公用程式方法與範例
* [使用SRP存取UGC](accessing-ugc-with-srp.md) —— 編碼准則

### 伺服器端自訂 {#server-side-customizations}

請造 [訪伺服器端自訂](server-customize.md) ，以取得自訂伺服器端社群元件商業邏輯與行為的相關資訊。

## Handlebars JS範本語言 {#handlebars-js-templating-language}

新架構中更引人注目的改變之一，是使用 [Handlebars JS範本語言(HBS)](https://www.handlebarsjs.com/)，這是一種常用的開放原始碼技術，用於伺服器——用戶端轉換。

HBS指令碼簡單、無邏輯、可在伺服器和用戶端上編譯、易於覆蓋和自訂，而且自然地與用戶端UX系結，因為HBS支援用戶端轉譯。

此架構提供數種 [Handlebars幫助器](handlebars-helpers.md) ，在開發SocialComponents時十分有用。

在伺服器上，當Sling解析GET請求時，它會識別將用來回應請求的指令碼。 如果指令碼是HBS範本(.hbs),Sling會將要求委派至Handlebars Engine。 然後，Handlebars引擎會從適當的SocialComponentFactory取得SocialComponent、建立內容並轉換HTML。

### 無存取限制 {#no-access-restriction}

Handlebar(HBS)範本檔案(.hbs)與。jsp和。html範本檔案類似，但它們可用於在用戶端瀏覽器和伺服器上轉換。 因此，請求用戶端範本的用戶端瀏覽器會從伺服器接收。hbs檔案。

這要求sling搜尋路徑中的所有HBS範本（/libs/或/apps下的任何。hbs檔案）都可由任何使用者從作者或發佈擷取。

HTTP存取。hbs檔案不得禁止。

### 添加或包含社群元件 {#add-or-include-a-communities-component}

Most Communities元件必須 *新增* ，做為Sling可定址資源。 在模板中可以包含一 *些Communities元件* ，作為非現有資源，以允許動態地包含和定制用戶生成內容(UGC)的寫入位置。

在這兩種情況下，元件的必 [要用戶端程式庫](clientlibs.md) ，也必須存在。

**新增元件**

新增元件是指新增資源（元件）例項的程式，例如從元件瀏覽器（側腳）拖曳至作者編輯模式中的頁面。

結果是par節點下的JCR子節點，即Sling可定址。

**包含元件**

包括元件是指在模板中添加對「非現有」資源 [](srp.md#for-non-existing-resources-ners) （無JCR節點）的引用的過程，如使用指令碼語言。

自AEM 6.1起，當元件動態包含而非新增時，就可以在作者*design *mode中編輯元件的屬性。

只能動態包含部分的AEM Communities元件。 它們是：

* [評論](essentials-comments.md)
* [評等](rating-basics.md)
* [評論](reviews-basics.md)
* [投票](essentials-voting.md)

「社 [群元件指南](components-guide.md) 」允許將可包含的元件從新增至包含。

**使用Handlebars模板語言** ，通過指定其resourceType，使用 [include helper](handlebars-helpers.md#include) ，包括非現有資源：

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**使用JSP**&#x200B;時，會使用標籤 [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>若要動態新增元件至頁面，而非將元件新增或加入範本中，請參閱元 [件側載](sideloading.md)。

### Handlebars Helpers {#handlebars-helpers}

如需 [SCF中提供的定製幫助的清單和說明，請參見SCF Handlebars Helpers](handlebars-helpers.md) 。

## 用戶端架構 {#client-side-framework}

### 模型——檢視Javascript架構 {#model-view-javascript-framework}

此架構包含 [Backbone.js的擴充功能](https://www.backbonejs.org/)，此為模型檢視的JavaScript架構，可協助開發多樣化的互動式元件。 物件導向的性質支援一個可擴展／可重用的框架。 借由HTTP API，可簡化用戶端與伺服器間的通訊。

該框架利用伺服器端的Handlebars模板為客戶端渲染元件。 這些模型是以HTTP API產生的JSON回應為基礎。 這些視圖會與Handlebars範本產生的HTML系結，並提供互動功能。

### CSS慣例 {#css-conventions}

以下是定義和使用CSS類別的建議慣例：

* 使用清楚命名的CSS類別選擇器名稱，並避免使用一般名稱，例如「標題」、「影像」等。
* 定義特定類別選擇器樣式，讓CSS樣式表能與頁面上的其他元素和樣式搭配使用。 例如： `.social-forum .topic-list .li { color: blue; }`
* 將CSS類別與JavaScript所驅動之UX的CSS類別分開

### 用戶端自訂 {#client-side-customizations}

若要自訂用戶端上社群元件的外觀和行為，請參考用戶端自訂 [(Client-Side Customizations](client-customize.md))，其中包含下列資訊：

* [覆蓋](client-customize.md#overlays)
* [擴充功能](client-customize.md#extensions)
* [HTML標籤](client-customize.md#htmlmarkup)
* [設定CSS外觀](client-customize.md#skinning-css)
* [擴充Javascript](client-customize.md#extending-javascript)
* [SCF的Clientlibs](client-customize.md#clientlibs-for-scf)

## 功能與元件基本功能 {#feature-and-component-essentials}

「功能與元件基本工具」一節將說明開 [發人員的基本資訊](essentials.md) 。

其他開發人員資訊請參閱「編碼指 [南」一節](code-guide.md) 。

## 疑難排解 {#troubleshooting}

疑難排解一節中介紹了常見問題 [和已知問](troubleshooting.md) 題。

