---
title: 社交元件架構
seo-title: 社交元件架構
description: 社交元件框架(SCF)簡化了配置、定制和擴展Communities元件的過程
seo-description: 社交元件框架(SCF)簡化了配置、定制和擴展Communities元件的過程
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 0%

---

# 社交元件架構{#social-component-framework}

社交元件架構(SCF)簡化了在伺服器端和用戶端配置、自訂和擴充Communities元件的程式。

該框架的好處：

* **功能**:80%的使用案例幾乎或不需自訂，即可輕鬆整合。
* **可外觀**:對CSS樣式一致地使用HTML屬性。
* **可擴充**:元件實施是物件導向的，輕鬆運用業務邏輯 — 易於在伺服器上添加增量業務登錄。
* **彈性**:輕鬆覆蓋和自訂的簡單無邏輯JavaScript範本。
* **可存取**:HTTP API支援從任何用戶端（包括行動應用程式）張貼。
* **可攜式**:整合/內嵌至任何以任何技術建置的網頁。

使用互動式[社群元件指南](components-guide.md)探索製作或發佈執行個體。

## 概覽 {#overview}

在SCF中，元件由SocialComponent POJO、Handlebars JS範本（用於呈現元件）和CSS（用於設定元件樣式）組成。

Handlebars JS範本可擴充模型/檢視JS元件，以處理使用者與用戶端上元件的互動。

如果元件需要支援資料修改，則可寫入SocialComponent API實作，以支援編輯/儲存與傳統Web應用程式中模型/資料物件類似的資料。 此外，可以添加操作（控制器）和操作服務以處理操作請求、執行業務邏輯以及在模型/資料對象上調用API。

SocialComponent API可延伸，以提供用戶端對檢視層或HTTP用戶端所需的資料。

### 如何為客戶端呈現頁面{#how-pages-are-rendered-for-client}

![scf-page呈現](assets/scf-overview.png)

### 元件定制和擴展{#component-customization-and-extension}

若要自訂或擴充元件，您只會將覆蓋圖和擴充功能寫入/apps目錄，簡化升級至未來版本的程式。

* 外觀設定：
   * 只有[CSS需要編輯](client-customize.md#skinning-css)。
* 外觀：
   * 變更JS範本和CSS。
* 外觀、風格和UX:
   * 變更JS範本、CSS和[延伸/覆寫Javascript](client-customize.md#extending-javascript)。
* 要修改「JS模板」或「GET」端點的可用資訊：
   * 擴充[SocialComponent](server-customize.md#socialcomponent-interface)。
* 若要在操作期間新增自訂處理：
   * 編寫[OperationExtension](server-customize.md#operationextension-class)。
* 若要新增自訂操作：
   * 建立新的[Sling Post Operation](server-customize.md#postoperation-class)。
   * 視需要使用現有的[OperationServices](server-customize.md#operationservice-class)。
   * 視需要新增Javascript程式碼，從用戶端叫用您的操作。

## 伺服器端架構{#server-side-framework}

該框架提供API以訪問伺服器上的功能，並支援客戶端與伺服器之間的交互。

### Java API {#java-apis}

Java API提供抽象類別和介面，這些類別和介面可輕鬆繼承或子類別。

主要類在[伺服器端自訂](server-customize.md)頁面上描述。

請訪問[儲存資源提供程式概述](srp.md)了解如何使用UGC。

### HTTP API {#http-api}

HTTP API支援為PhoneGap應用程式、原生應用程式及其他整合和綜合應用程式輕鬆自訂和選擇用戶端平台。 此外，HTTP API允許社區站點作為服務運行，而無需客戶端，這樣框架元件可以整合到任何基於技術構建的任何網頁中。

### HTTP API -GET要求{#http-api-get-requests}

架構會針對每個SocialComponent提供HTTP型API端點。 端點的存取方式為使用「.social.json」選取器+擴充功能傳送GET要求至資源。 使用Sling時，會將要求傳送至`DefaultSocialGetServlet`。

**`DefaultSocialGetServlet`**

1. 將資源(resourceType)傳遞至`SocialComponentFactoryManager`並接收能夠選擇代表資源的`SocialComponent`的SocialComponentFactory。

1. 調用工廠並接收能夠處理資源和請求的`SocialComponent`。
1. 叫用`SocialComponent`，處理要求並傳回結果的JSON表示。
1. 傳回JSON回應給用戶端。

**`GET Request`**

預設GETservlet監聽SocialComponent使用可自訂JSON回應的.social.json請求。

![scf框架](assets/scf-framework.png)

### HTTP API -POST要求{#http-api-post-requests}

除了GET（讀取）操作外，框架還定義了端點模式以啟用元件上的其他操作，包括建立、更新和刪除。 這些端點是HTTP API，可接受輸入並以HTTP狀態代碼或JSON回應物件回應。

該框架端點模式使CUD操作可擴展、可重複使用和可測試。

**`POST Request`**

每個SocialComponent操作都有SlingPOST：操作。 每個操作的業務邏輯和維護代碼都包在OperationService中，該OperationService可通過HTTP API或從其他位置作為OSGi服務訪問。 提供了用於動作之前/之後的支援可插拔操作擴展的鈎。

![scf-post-request](assets/scf-post-request.png)

### 儲存資源提供程式(SRP){#storage-resource-provider-srp}

若要了解如何處理儲存在[社群內容存放區](working-with-srp.md)中的UGC，請參閱：

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP API公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則。

### 伺服器端自訂{#server-side-customizations}

有關自定義伺服器端Communities元件的業務邏輯和行為的資訊，請訪問[伺服器端自定義](server-customize.md)。

## Handlebars JS模板語言{#handlebars-js-templating-language}

新架構中更顯著的變更之一，是使用[Handlebars JS範本語言(HBS)](https://www.handlebarsjs.com/)，這是伺服器用戶端轉譯的熱門開放原始碼技術。

HBS指令碼簡單、無邏輯、在伺服器和客戶端上編譯、易於覆蓋和定制，並且自然地與客戶端UX綁定，因為HBS支援客戶端呈現。

此架構提供數個[Handlebars helpers](handlebars-helpers.md)，在開發SocialComponents時相當實用。

在伺服器上，Sling解析GET請求時，會識別將用來回應請求的指令碼。 如果指令碼是HBS範本(.hbs),Sling會將要求委派給Handlebars引擎。 然後，Handlebars引擎將從適當的SocialComponentFactory中取得SocialComponent，建立內容，並轉譯HTML。

### 無訪問限制{#no-access-restriction}

Handlebars(HBS)範本檔案(.hbs)類似於.jsp和.html範本檔案，但它們可用於在用戶端瀏覽器和伺服器上呈現。 因此，請求用戶端範本的用戶端瀏覽器將從伺服器接收.hbs檔案。

這需要Sling搜尋路徑中的所有HBS範本（/libs/或/apps底下的任何.hbs檔案）可由任何使用者從製作或發佈中擷取。

不得禁止HTTP存取.hbs檔案。

### 添加或包含社區元件{#add-or-include-a-communities-component}

大部分的Communities元件必須&#x200B;*新增*&#x200B;作為Sling可定址資源。 在模板中選擇的幾個Communities元件可以&#x200B;*包括*&#x200B;作為非現有資源，以允許動態地包含和定制寫入用戶生成內容(UGC)的位置。

無論是哪種情況，元件的[必要的客戶端庫](clientlibs.md)也必須存在。

**新增元件**

新增元件是指新增資源（元件）例項的程式，例如從元件瀏覽器(sidekick)拖曳至作者編輯模式中的頁面時。

結果會是par節點底下的JCR子節點，即Sling可定址。

**包含元件**

包括元件是指在範本內新增參考至[&quot;non-existing&quot; resource](srp.md#for-non-existing-resources-ners)(no JCR node)的程式，例如使用指令碼語言。

自AEM 6.1起，當元件以動態方式包含而非新增時，即可在製作*設計*模式中編輯元件的屬性。

只能動態加入少數幾個AEM Communities元件。 它們是：

* [評論](essentials-comments.md)
* [評等](rating-basics.md)
* [評論](reviews-basics.md)
* [投票](essentials-voting.md)

[社區元件指南](components-guide.md)允許切換可包含的元件，使其不被添加到要包含的元件。

**使用Handlebarstemplating** 語言時，會使用include helper來包含非現有資 [源，](handlebars-helpers.md#include) 方法是指定其resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**使用JSP**&#x200B;時，會使用標籤cq包含 [資源：include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>若要動態地將元件新增至頁面，而非將元件新增或加入範本，請參閱[元件側載](sideloading.md)。

### Handlebars Helpers {#handlebars-helpers}

有關SCF中可用的自定義幫助器的清單和說明，請參閱[SCF Handlebars Helpers](handlebars-helpers.md)。

## 用戶端架構{#client-side-framework}

### 模型檢視Javascript架構{#model-view-javascript-framework}

此架構包含[Backbone.js](https://www.backbonejs.org/)的擴充功能，此為模型檢視的JavaScript架構，可協助開發豐富的互動式元件。 物件導向的性質支援可擴展/可重複使用的框架。 借由HTTP API可簡化用戶端與伺服器之間的通訊。

該框架利用伺服器端Handlebars模板來呈現客戶端的元件。 這些模型以HTTP API產生的JSON回應為基礎。 視圖將自身綁定到由Handlebars模板生成的HTML，並提供交互性。

### CSS約定{#css-conventions}

以下是定義和使用CSS類的建議慣例：

* 使用命名空間明確的CSS類別選取器名稱，並避免使用「標題」、「影像」等通用名稱。
* 定義特定類選擇器樣式，使CSS樣式表能夠與頁面上的其他元素和樣式配合使用。 例如：`.social-forum .topic-list .li { color: blue; }`
* 保留由JavaScript驅動的UX的樣式的CSS類別，與CSS類別分開。

### 用戶端自訂{#client-side-customizations}

若要自訂用戶端上Communities元件的外觀和行為，請參考[用戶端自訂](client-customize.md)，其中包含下列資訊：

* [覆蓋](client-customize.md#overlays)
* [擴充功能](client-customize.md#extensions)
* [HTML標籤](client-customize.md#htmlmarkup)
* [設定CSS外觀](client-customize.md#skinning-css)
* [擴充Javascript](client-customize.md#extending-javascript)
* [SCF的Clientlibs](client-customize.md#clientlibs-for-scf)

## 功能和元件要點{#feature-and-component-essentials}

[功能和元件要件](essentials.md)區段中有關開發人員的基本資訊。

可在[編碼指南](code-guide.md)部分找到其他開發人員資訊。

## 疑難排解 {#troubleshooting}

[疑難排解](troubleshooting.md)一節將說明常見問題和已知問題。
