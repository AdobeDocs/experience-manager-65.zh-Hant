---
title: 社會構成框架
seo-title: Social Component Framework
description: 社交元件框架(SCF)簡化了配置、定制和擴展社區元件的過程
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

# 社會構成框架 {#social-component-framework}

社交元件框架(SCF)簡化了在伺服器端和客戶端上配置、定制和擴展社區元件的過程。

該框架的好處：

* **功能**:開箱即用，易於整合，而80%的使用案例很少或沒有定制。
* **剝皮**:CSS樣式的HTML屬性的一致使用。
* **可擴展**:元件實現是物件導向的，輕鬆的業務邏輯 — 易於在伺服器上添加增量業務登錄。
* **靈活**:簡單的無邏輯的Javascript模板，易於疊加和自定義。
* **可訪問**:HTTP API支援從任何客戶端（包括移動應用）發佈。
* **攜帶型**:整合/嵌入任何基於任何技術構建的網頁。

使用互動式瀏覽作者或發佈實例 [社區元件指南](components-guide.md)。

## 概觀 {#overview}

在SCF中，元件由SocialComponent POJO、Handlebars JS模板（用於呈現元件）和CSS（用於對元件進行樣式化）組成。

「Handlebar JS模板」可以擴展模型/視圖JS元件，以處理用戶與客戶端上元件的交互。

如果元件需要支援資料的修改，則可以編寫SocialComponent API的實現以支援編輯/保存類似於傳統Web應用程式中模型/資料對象的資料。 此外，可以添加操作（控制器）和操作服務以處理操作請求、執行業務邏輯以及調用模型/資料對象上的API。

SocialComponent API可以被擴展，以提供客戶端對視圖層或HTTP客戶端所需的資料。

### 如何為客戶端呈現頁面 {#how-pages-are-rendered-for-client}

![scf-page呈現](assets/scf-overview.png)

### 元件定制和擴展 {#component-customization-and-extension}

要自定義或擴展元件，您只將覆蓋和擴展寫入/apps目錄，這簡化了升級到未來版本的過程。

* 對於外觀：
   * 僅 [CSS需要編輯](client-customize.md#skinning-css)。
* 外觀：
   * 更改JS模板和CSS。
* Look、Feel和UX:
   * 更改JS模板、CSS和 [擴展/覆蓋Javascript](client-customize.md#extending-javascript)。
* 要修改JS模板或GET端點可用的資訊：
   * 擴展 [社交元件](server-customize.md#socialcomponent-interface)。
* 要在操作期間添加自定義處理：
   * 寫入 [操作擴展](server-customize.md#operationextension-class)。
* 要添加新的自定義操作：
   * 新建 [吊具後操作](server-customize.md#postoperation-class)。
   * 使用現有 [運營服務](server-customize.md#operationservice-class) 按需要。
   * 添加Javascript代碼以根據需要從客戶端調用您的操作。

## 伺服器端框架 {#server-side-framework}

該框架提供API以訪問伺服器上的功能並支援客戶端與伺服器之間的交互。

### Java API {#java-apis}

Java API提供易於繼承或子類的抽象類和介面。

在 [伺服器端定制](server-customize.md) 的子菜單。

訪問 [儲存資源提供程式概述](srp.md) 瞭解與UGC的合作。

### HTTP API {#http-api}

HTTP API支援為PhoneGap應用、本機應用和其他整合和混合提供易於自定義和選擇的客戶端平台。 此外，HTTP API允許社區站點作為服務而不使用客戶端運行，從而框架元件可以整合到任何基於任何技術構建的任何網頁中。

### HTTP API -GET請求 {#http-api-get-requests}

對於每個SocialComponent，該框架都提供基於HTTP的API終結點。 通過向資源發送GET請求（帶「.social.json」選擇器+副檔名）來訪問終結點。 使用Sling，請求將提交給 `DefaultSocialGetServlet`。

**`DefaultSocialGetServlet`**

1. 將資源(resourceType)傳遞到 `SocialComponentFactoryManager` 並接收能夠選擇 `SocialComponent` 代表資源。

1. 調用工廠並接收 `SocialComponent` 能夠處理資源和請求。
1. 調用 `SocialComponent`，處理請求並返回結果的JSON表示。
1. 返回對客戶端的JSON響應。

**`GET Request`**

預設GETservlet偵聽SocialComponent用可自定義JSON響應的.social.json請求。

![scf框架](assets/scf-framework.png)

### HTTP API -POST請求 {#http-api-post-requests}

除了GET（讀取）操作外，框架還定義端點模式以啟用元件上的其他操作，包括建立、更新和刪除。 這些端點是HTTP API，它們接受輸入，並使用HTTP狀態代碼或JSON響應對象進行響應。

該框架端點模式使CUD操作具有可擴充性、可重用性和可測試性。

**`POST Request`**

每個SocialComponent操作都有SlingPOST：操作。 每個操作的業務邏輯和維護代碼都包裝在OperationService中，該OperationService可通過HTTP API訪問，或作為OSGi服務從其他位置訪問。 提供了用於動作之前/之後的可插拔操作擴展的掛接。

![scf後請求](assets/scf-post-request.png)

### 儲存資源提供程式(SRP) {#storage-resource-provider-srp}

瞭解處理儲存在 [社區內容儲存](working-with-srp.md)，請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC軟體包](srp-and-ugc.md) - SRP API實用程式方法和示例。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。

### 伺服器端自定義 {#server-side-customizations}

訪問 [伺服器端自定義](server-customize.md) 有關自定義伺服器端社區元件的業務邏輯和行為的資訊。

## 車把JS模板語言 {#handlebars-js-templating-language}

在新框架中，一個更明顯的變化是 `Handlebars JS` (HBS)模板化語言，一種常用的開源技術，用於伺服器 — 客戶端渲染。

HBS指令碼簡單、無邏輯，可在伺服器和客戶端上編譯，易於覆蓋和自定義，並自然與客戶端UX綁定，因為HBS支援客戶端呈現。

該框架提供了 [車把幫助器](handlebars-helpers.md) 在開發SocialComponents時非常有用。

在伺服器上，當Sling解析GET請求時，它標識將用於響應請求的指令碼。 如果指令碼是HBS模板(.hbs),Sling會將請求委託給Handlebar引擎。 然後，車把引擎將從相應的SocialComponentFactory中獲取SocialComponent，構建上下文並呈現HTML。

### 無訪問限制 {#no-access-restriction}

車把(HBS)模板檔案(.hbs)與.jsp和.html模板檔案類似，不過它們可用於在客戶端瀏覽器和伺服器上呈現。 因此，請求客戶端模板的客戶端瀏覽器將從伺服器接收.hbs檔案。

這要求任何用戶都可以從作者或發佈中讀取sling搜索路徑中的所有HBS模板（/libs/或/apps下的任何.hbs檔案）。

可能不禁止對.hbs檔案的HTTP訪問。

### 添加或包括社區元件 {#add-or-include-a-communities-component}

大多數社區元件必須 *添加* 作為Sling可定址資源。 選擇的幾個社區元件可能是 *包括* 在模板中作為非現有資源，以允許動態包含和自定義寫入用戶生成內容(UGC)的位置。

無論哪種情況，元件 [所需的客戶端庫](clientlibs.md) 也必須在場。

**添加元件**

添加元件是指添加資源（元件）實例的過程，例如在作者編輯模式下從元件瀏覽器（側腳）拖動到頁面時。

結果是在par節點下的JCR子節點，即Sling可定址。

**包括元件**

包括元件是指將參照添加到 [&quot;非現有&quot;資源](srp.md#for-non-existing-resources-ners) （無JCR節點），例如使用指令碼語言。

截至AEM6.1，當動態地包括而不是添加元件時，可以在作者*design *模式下編輯元件的屬性。

只能動態地包括選定的幾個AEM Communities元件。 它們是：

* [評論](essentials-comments.md)
* [評等](rating-basics.md)
* [評論](reviews-basics.md)
* [投票](essentials-voting.md)

的 [社區元件指南](components-guide.md) 允許切換可包含元件，使其不被添加到包含中。

**使用車把時** 模板語言，非現有資源使用 [包含幫助程式](handlebars-helpers.md#include) 通過指定其resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**使用JSP時**，使用標籤包含資源 [cq：包括](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>要將元件動態添加到頁面，而不是將其添加或包含在模板中，請參見 [元件旁載入](sideloading.md)。

### 把手幫助程式 {#handlebars-helpers}

請參閱 [SCF把手幫助器](handlebars-helpers.md) 以獲取SCF中可用的自定義幫助程式的清單和說明。

## 客戶端框架 {#client-side-framework}

### 模型視圖Javascript框架 {#model-view-javascript-framework}

該框架包括 [骨幹.js](https://www.backbonejs.org/)，一個模型視圖JavaScript框架，便於開發豐富、交互的元件。 物件導向的性質支援一個可擴展/可重用的框架。 通過HTTP API簡化了客戶端與伺服器之間的通信。

該框架利用伺服器端的Handlebars模板為客戶端呈現元件。 模型基於HTTP API生成的JSON響應。 視圖將自身綁定到由Handlebars模板生成的HTML，並提供交互性。

### CSS約定 {#css-conventions}

以下是定義和使用CSS類的建議約定：

* 使用明確命名空間的CSS類選擇器名稱，並避免使用「heading」、「image」等通用名稱。
* 定義特定類選擇器樣式，以便CSS樣式表可以與頁面上的其他元素和樣式一起使用。 例如：`.social-forum .topic-list .li { color: blue; }`
* 使用CSS類進行造型，與JavaScript驅動的UX的CSS類分開。

### 客戶端自定義 {#client-side-customizations}

對於自定義客戶端上社區元件的外觀和行為，請參考 [客戶端自定義](client-customize.md)，其中包括有關以下資訊：

* [覆蓋](client-customize.md#overlays)
* [擴展](client-customize.md#extensions)
* [HTML標籤](client-customize.md#htmlmarkup)
* [外觀CSS](client-customize.md#skinning-css)
* [擴展Javascript](client-customize.md#extending-javascript)
* [SCF的客戶端](client-customize.md#clientlibs-for-scf)

## 功能和元件要素 {#feature-and-component-essentials}

開發人員的基本資訊在 [功能和元件要素](essentials.md) 的子菜單。

其他開發人員資訊可在 [編碼准則](code-guide.md) 的子菜單。

## 疑難排解 {#troubleshooting}

有關常見問題和已知問題的介紹，請參閱 [故障排除](troubleshooting.md) 的子菜單。
