---
title: 社交元件架構
seo-title: Social Component Framework
description: 社交元件框架(SCF)簡化了配置、定制和擴展Communities元件的過程
seo-description: The social component framework (SCF) simplifies the process of configuring, customizing, and extending Communities components
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
source-git-commit: 1d5cfff10735ea31dc0289b6909851b8717936eb
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 0%

---

# 社交元件架構 {#social-component-framework}

社交元件架構(SCF)簡化了在伺服器端和用戶端配置、自訂和擴充Communities元件的程式。

該框架的好處：

* **功能**:80%的使用案例幾乎或不需自訂，即可輕鬆整合。
* **可外觀**:一致地使用CSS樣式的HTML屬性。
* **可擴充**:元件實施是物件導向的，輕鬆運用業務邏輯 — 易於在伺服器上添加增量業務登錄。
* **靈活**:輕鬆覆蓋和自訂的簡單無邏輯JavaScript範本。
* **無障礙**:HTTP API支援從任何用戶端（包括行動應用程式）張貼。
* **攜帶型**:整合/內嵌至任何以任何技術建置的網頁。

使用互動式探索製作或發佈例項 [社群元件指南](components-guide.md).

## 概觀 {#overview}

在SCF中，元件由SocialComponent POJO、Handlebars JS範本（用於呈現元件）和CSS（用於設定元件樣式）組成。

Handlebars JS範本可擴充模型/檢視JS元件，以處理使用者與用戶端上元件的互動。

如果元件需要支援資料修改，則可寫入SocialComponent API實作，以支援編輯/儲存與傳統Web應用程式中模型/資料物件類似的資料。 此外，可以添加操作（控制器）和操作服務以處理操作請求、執行業務邏輯以及在模型/資料對象上調用API。

SocialComponent API可延伸，以提供用戶端對檢視層或HTTP用戶端所需的資料。

### 如何為客戶端呈現頁面 {#how-pages-are-rendered-for-client}

![scf-page呈現](assets/scf-overview.png)

### 元件自訂和擴充功能 {#component-customization-and-extension}

若要自訂或擴充元件，您只會將覆蓋圖和擴充功能寫入/apps目錄，簡化升級至未來版本的程式。

* 外觀設定：
   * 僅 [CSS需要編輯](client-customize.md#skinning-css).
* 外觀：
   * 變更JS範本和CSS。
* 外觀、風格和UX:
   * 變更JS範本、CSS和 [延伸/覆寫Javascript](client-customize.md#extending-javascript).
* 要修改「JS模板」或「GET」端點的可用資訊：
   * 擴充 [SocialComponent](server-customize.md#socialcomponent-interface).
* 若要在操作期間新增自訂處理：
   * 撰寫 [操作擴展](server-customize.md#operationextension-class).
* 若要新增自訂操作：
   * 建立新 [Sling後操作](server-customize.md#postoperation-class).
   * 使用現有 [OperationServices](server-customize.md#operationservice-class) 視需要。
   * 視需要新增Javascript程式碼，從用戶端叫用您的操作。

## 伺服器端架構 {#server-side-framework}

該框架提供API以訪問伺服器上的功能，並支援客戶端與伺服器之間的交互。

### Java API {#java-apis}

Java API提供抽象類別和介面，這些類別和介面可輕鬆繼承或子類別。

主要類在 [伺服器端自訂](server-customize.md) 頁面。

瀏覽 [儲存資源提供程式概述](srp.md) 了解如何使用UGC。

### HTTP API {#http-api}

HTTP API支援為PhoneGap應用程式、原生應用程式及其他整合和綜合應用程式輕鬆自訂和選擇用戶端平台。 此外，HTTP API允許社區站點作為服務運行，而無需客戶端，這樣框架元件可以整合到任何基於技術構建的任何網頁中。

### HTTP API -GET要求 {#http-api-get-requests}

架構會針對每個SocialComponent提供HTTP型API端點。 端點的存取方式為使用「.social.json」選取器+擴充功能傳送GET要求至資源。 使用Sling時，系統會將要求傳送至 `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. 將資源(resourceType)傳遞至 `SocialComponentFactoryManager` 並接收能夠選擇 `SocialComponent` 代表資源。

1. 調用工廠並接收 `SocialComponent` 能夠處理資源和請求。
1. 調用 `SocialComponent`，會處理要求並傳回結果的JSON表示法。
1. 傳回JSON回應給用戶端。

**`GET Request`**

預設GETservlet監聽SocialComponent使用可自訂JSON回應的.social.json請求。

![scf框架](assets/scf-framework.png)

### HTTP API -POST要求 {#http-api-post-requests}

除了GET（讀取）操作外，框架還定義了端點模式以啟用元件上的其他操作，包括建立、更新和刪除。 這些端點是HTTP API，可接受輸入並以HTTP狀態代碼或JSON回應物件回應。

該框架端點模式使CUD操作可擴展、可重複使用和可測試。

**`POST Request`**

每個SocialComponent操作都有SlingPOST：操作。 每個操作的業務邏輯和維護代碼都包在OperationService中，該OperationService可通過HTTP API或從其他位置作為OSGi服務訪問。 提供了用於動作之前/之後的支援可插拔操作擴展的鈎。

![scf-post-request](assets/scf-post-request.png)

### 儲存資源提供程式(SRP) {#storage-resource-provider-srp}

若要了解如何處理儲存在 [社群內容存放區](working-with-srp.md)，請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和存放庫使用概觀。
* [SRP和UGC要點](srp-and-ugc.md) - SRP API公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則。

### 伺服器端自訂 {#server-side-customizations}

瀏覽 [伺服器端自訂](server-customize.md) 有關在伺服器端自訂Communities元件的業務邏輯和行為的資訊。

## Handlebars JS範本語言 {#handlebars-js-templating-language}

新框架中更明顯的變化之一是使用 `Handlebars JS` (HBS)範本語言，一種用於伺服器用戶端轉譯的熱門開放原始碼技術。

HBS指令碼簡單、無邏輯、在伺服器和客戶端上編譯、易於覆蓋和定制，並且自然地與客戶端UX綁定，因為HBS支援客戶端呈現。

此架構提供 [手把手幫手](handlebars-helpers.md) 在開發SocialComponents時很有用。

在伺服器上，Sling解析GET請求時，會識別將用來回應請求的指令碼。 如果指令碼是HBS範本(.hbs),Sling會將要求委派給Handlebars引擎。 然後，Handlebars引擎將從適當的SocialComponentFactory中取得SocialComponent、建立內容並呈現HTML。

### 無訪問限制 {#no-access-restriction}

Handlebars(HBS)範本檔案(.hbs)類似於.jsp和.html範本檔案，但它們可用於在用戶端瀏覽器和伺服器上呈現。 因此，請求用戶端範本的用戶端瀏覽器將從伺服器接收.hbs檔案。

這需要Sling搜尋路徑中的所有HBS範本（/libs/或/apps底下的任何.hbs檔案）可由任何使用者從製作或發佈中擷取。

不得禁止HTTP存取.hbs檔案。

### 添加或包含社區元件 {#add-or-include-a-communities-component}

大多數Communities元件必須 *新增* 作為Sling可定址資源時。 Communities的一些元件可能是 *包含* 在範本中作為非現有資源，以允許動態包含和自訂寫入使用者產生內容(UGC)的位置。

無論是哪種情況，元件的 [必要的客戶端庫](clientlibs.md) 也必須有。

**新增元件**

新增元件是指新增資源（元件）例項的程式，例如從元件瀏覽器(sidekick)拖曳至作者編輯模式中的頁面時。

結果會是par節點底下的JCR子節點，即Sling可定址。

**包含元件**

包括元件是指將參照新增至 [「非現有」資源](srp.md#for-non-existing-resources-ners) （無JCR節點），例如使用指令碼語言。

自AEM 6.1起，當元件以動態方式包含而非新增時，即可在製作*設計*模式中編輯元件的屬性。

只能動態加入少數幾個AEM Communities元件。 它們是：

* [評論](essentials-comments.md)
* [評等](rating-basics.md)
* [評論](reviews-basics.md)
* [投票](essentials-voting.md)

此 [社群元件指南](components-guide.md) 允許切換可包含的元件，使其不會新增至包含中。

**使用Handlebars時** 範本語言，則會使用 [包含協助程式](handlebars-helpers.md#include) 通過指定其resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**使用JSP時**，則會使用標籤包含資源 [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>若要動態新增元件至頁面，而非將元件新增或加入範本，請參閱 [元件側載](sideloading.md).

### Handlebars Helpers {#handlebars-helpers}

請參閱 [SCF Handlebars幫助器](handlebars-helpers.md) 以獲取SCF中提供的自定義幫助程式的清單和說明。

## 用戶端架構 {#client-side-framework}

### 模型檢視Javascript架構 {#model-view-javascript-framework}

此架構包含 [骨幹.js](https://www.backbonejs.org/)，此元件為模型檢視的JavaScript架構，以促進開發豐富的互動式元件。 物件導向的性質支援可擴展/可重複使用的框架。 借由HTTP API可簡化用戶端與伺服器之間的通訊。

該框架利用伺服器端Handlebars模板來呈現客戶端的元件。 這些模型以HTTP API產生的JSON回應為基礎。 視圖將自身綁定到由Handlebars模板生成的HTML，並提供交互性。

### CSS慣例 {#css-conventions}

以下是定義和使用CSS類的建議慣例：

* 使用命名空間明確的CSS類別選取器名稱，並避免使用「標題」、「影像」等通用名稱。
* 定義特定類選擇器樣式，使CSS樣式表能夠與頁面上的其他元素和樣式配合使用。 例如：`.social-forum .topic-list .li { color: blue; }`
* 保留由JavaScript驅動的UX的樣式的CSS類別，與CSS類別分開。

### 用戶端自訂 {#client-side-customizations}

若要自訂用戶端上Communities元件的外觀和行為，請參閱 [用戶端自訂](client-customize.md)，其中包含下列資訊：

* [覆蓋](client-customize.md#overlays)
* [擴充功能](client-customize.md#extensions)
* [HTML標籤](client-customize.md#htmlmarkup)
* [設定CSS外觀](client-customize.md#skinning-css)
* [擴充Javascript](client-customize.md#extending-javascript)
* [SCF的Clientlibs](client-customize.md#clientlibs-for-scf)

## 功能和元件要點 {#feature-and-component-essentials}

開發人員的基本資訊如 [功能和元件要點](essentials.md) 區段。

如需其他開發人員資訊，請參閱 [編碼准則](code-guide.md) 區段。

## 疑難排解 {#troubleshooting}

常見問題和已知問題於 [疑難排解](troubleshooting.md) 區段。
