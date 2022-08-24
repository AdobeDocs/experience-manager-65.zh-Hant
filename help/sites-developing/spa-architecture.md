---
title: 開SPA發AEM
seo-title: Developing SPAs for AEM
description: 本文介紹了在讓前端開發人員開發SPAAEM FOR時需要考慮的重要問題，並概述了在部署已開發開發產品時AEM應SPA當考慮的體SPA系結構。
seo-description: This article presents important questions to consider when engaging a front-end developer to develop a SPA for AEM as well as gives an overview of the architecture of AEM with respect to SPAs to keep in mind when deploying a developed SPA on AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 1%

---

# 開SPA發AEM{#developing-spas-for-aem}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能夠使用框架構建站SPA點，而作者希望無縫地編輯使用這AEM種框架構建的站點的內容。

本文介紹了在讓前端開發人員開發用於SPA的系AEM統時需要考慮的重要問題，並概AEM述了在上的部SPA署體AEM系。

>[!NOTE]
>
>編輯SPA器是需要基於框架的SPA客戶端呈現(例如，反應或Angular)的項目的推薦解決方案。

## SPA發展原AEM則 {#spa-development-principles-for-aem}

開發單頁應用程式AEM時，假定前端開發人員在建立時遵守標準的最佳SPA做法。 如果作為前端開發人員，您遵循這些一般最佳實踐和AEM少數特定原則，則SPA您將能夠 [AEM及其內容創作能力](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)。

* **[便攜性](/help/sites-developing/spa-architecture.md#portability) -** 與任何元件一樣，元件應盡可能便攜。 應該SPA使用可移植和可重複使用的元件來構建。
* **[驅動AEM器站點結構](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**  — 前端開發人員建立元件並擁有其內部結構，但依AEM賴於定義站點的內容結構。
* **[動態渲染](/help/sites-developing/spa-architecture.md#dynamic-rendering)**  — 所有渲染都應是動態的。
* **[動態路由](#dynamic-routing) -** 路SPA由負責並監聽AEM路由並基於其讀取。 任何路由都應是動態的。

如果您在開發時牢記這些原則，SPA則在啟用所有受支援的創作功能時，它將盡可能靈活並經得起未AEM來考驗。

如果您不需要支援創AEM作功能，則可能需要考慮其他功能 [SPA設計模型](/help/sites-developing/spa-architecture.md#spa-design-models)。

### 便攜性 {#portability}

與開發任何元件一樣，您的元件的設計方式應最大限度地提高其可移植性。 任何與元件的可移植性或可重用性相抵觸的模式都應避免，以確保將來的相容性、靈活性和可維護性。

因此，應SPA該使用高度便攜和可重複使用的元件來構建。

### 驅動AEM器站點結構 {#aem-drives-site-structure}

前端開發人員必須認為自己負責建立用於構建應用SPA的元件庫。 前端顯影劑對元件的內部結構具有完全控制。 [然AEM而，這個網站的結構是隨時擁有的。](/help/sites-developing/spa-overview.md)

這意味著前端開發人員可以在元件入口點之前或之後添加客戶內容，還可以在元件內進行第三方呼叫。 但是，例如，前端開發人員無法完全控制元件的嵌套方式。

### 動態渲染 {#dynamic-rendering}

只SPA應依賴內容的動態呈現。 這是讀取和呈現內AEM容結構的所有子級的預設期望值。

任何指向特定內容的顯式渲染都被視為靜態渲染，儘管受支援，但與內容創作功AEM能不相容。 這也違背了 [可移植性](/help/sites-developing/spa-architecture.md#portability)。

### 動態路由 {#dynamic-routing}

與呈現一樣，所有路由都應是動態的。 在AEM, [應SPA該始終擁有](/help/sites-developing/spa-routing.md) 並AEM根據它來提取內容。

任何靜態路由都與 [便攜性原則](/help/sites-developing/spa-architecture.md#portability) 並限製作者與的內容創作功能不兼AEM容。 例如，使用靜態路由，如果內容作者想更改路由或更改頁面，則他或她必須要求前端開發人員執行此操作。

## AEM 專案原型 {#aem-project-archetype}

任何AEM項目都應利用 [項AEM目原型](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/developing/archetype/overview.html)，它支SPA持使用React或Angular的項目，並利SPA用SDK。

## 設SPA計模型 {#spa-design-models}

如果 [C.發展SPA原AEM則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) 之後，您的SPA所有受支援內容創作功AEM能都可用。

但是，有些情況並非完全必要。 下表概述了各種設計模型、其優點和缺點。

<table>
 <tbody>
  <tr>
   <th><strong>設計模型<br /> </strong></th>
   <th><strong>優點</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <td>用作AEM無頭CMS，而不使用 <a href="/help/sites-developing/spa-reference-materials.md">編SPA輯器SDK框架。</a></td>
   <td>前端開發者完全控制該應用。</td>
   <td><p>內容作者無法利AEM用內容創作體驗。</p> <p>如果代碼包含靜態引用或路由，則它既不可移植，也不可重用。</p> <p>不允許使用模板編輯器，因此前端開發人員必須通過JCR維護可編輯的模板。</p> </td>
  </tr>
  <tr>
   <td>前端開發人員使用SPAEditor SDK框架，但只向內容作者開啟某些區域。</td>
   <td>開發人員僅在應用程式的限制區域啟用創作，從而保持對應用程式的控制。</td>
   <td><p>內容作者僅限於一組有限的內容AEM創作體驗。</p> <p>如果代碼包含靜態引用或路由，則代碼可能既不可移植，也不可重複使用。</p> <p>不允許使用模板編輯器，因此前端開發人員必須通過JCR維護可編輯的模板。</p> </td>
  </tr>
  <tr>
   <td>本項目充分利SPA用了Editor SDK，將前端元件開發為庫，並將應用程式的內容結構委託給AEM它。</td>
   <td><p>該應用可重用且便攜。</p> <p>內容作者可以使用內容創作體驗AEM編輯應用。<br /> </p> <p>與模SPA板編輯器相容。</p> </td>
   <td><p>開發人員無法控制應用程式的結構和委託給的內容部分AEM。</p> <p>開發人員仍然可以為不打算使用創作的內容保留應用的區AEM域。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>儘管所有型號都在中AEM受支援，但僅通過實施第三種型號(並因此遵循建議 [SPA發展原AEM則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem))的內容作者能否與中的內容進行交互和編SPA輯，AEM這是他們習慣的。

## 將現有遷SPA移到AEM {#migrating-existing-spas-to-aem}

通常，如SPA果您 [SPA發展原AEM則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)，則SPA將使用AEM編輯器進行編AEM輯。

請執行以下步驟，使現SPA有的可用AEM。

1. **將JS元件模組化。**

   使它們能夠按任意順序、位置和大小呈現。
1. **使用SDK提供的容器將元件放在螢幕上。**

   提AEM供頁面和段落系統元件供您使用。
1. **為每個AEMJS元件建立元件。**

   組AEM件定義對話框和JSON輸出。

## 前端開發人員說明 {#instructions-for-front-end-developers}

在為前端開發人員建立元件時，主要SPA任AEM務是就元件及其JSON模型達成一致。

以下是前端開發人員在為開發時需要遵循的SPA步驟AEM。

1. **同意元件及其JSON模型**

   前端開發人員和後AEM端開發人員需要就哪些元件是必需的以及模型達成一致，以便從元件到後端元件之間SPA實現一對一匹配。

   元AEM件在提供編輯對話框和導出元件模型時仍是必不可少的。

1. **在React元件中，通過`this.props.cqModel`**

   一旦元件達成一致並且JSON模型就位，前端開發人員就可以免費開發SPA，並且只需通過 `this.props.cqModel`。

1. **實現元件 `render()` 方法**

   前端開發人員實施 `render()` 方法，並可使用 `cqModel` 屬性。 這將輸出將插入頁面的DOM和HTML片段。 這是在React中構建應用的標準方法。

1. **將元件映射到AEM資源類型`MapTo()`**

   映射儲存元件類，並由提供的 `Container` 元件，用於根據給定的資源類型檢索和動態實例化元件。

   這是前端和後端之間的「粘合」，因此編輯器知道反應元件對應哪些元件。

   的 `Page` 和 `ResponsiveGrid` 是擴展基礎的類的好例子 `Container`。

1. **定義元件 `EditConfig` 作為參數`MapTo()`**

   此參數對於告訴編輯器如何將元件命名為尚未呈現或沒有要呈現的內容時是必需的。

1. **擴展所提供的 `Container` 頁面和容器類**

   頁面和段落系統應擴展此類，以便向內部元件委派可以按預期方式工作。

1. **實施使用HTML5的路由解決方案 `History` API。**

   當 `ModelRouter` 已啟用，正在調用 `pushState` 和 `replaceState` 函式將觸發對 `PageModelManager` 以提取模型的缺失片段。

   當前版本的 `ModelRouter` 僅支援使用指向Sling Model入口點的實際資源路徑的URL。 它不支援使用虛榮URL或別名。

   的 `ModelRouter` 可以禁用或配置為忽略規則運算式清單。

## 不AEM可知 {#aem-agnostic}

這些代碼塊說明您的React和Angular元件不需要任何Adobe或特定AEM的內容。

* JavaScript元件內的所有內容都是不AEM可知的。
* 但是，JS元件AEM必須映射到具有MapTo幫助AEM程式的元件。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

的 `MapTo` helper是「膠水」，它允許後端和前端元件相匹配：

* 它告訴JS容器（或JS段落系統）JS元件負責呈現JSON中存在的每個元件。
* 它向JS元件呈現的HTML添加HTML資料屬性，以便編輯SPA器知道編輯元件時要向作者顯示的對話框。

有關使用的詳細資訊 `MapTo` 並構SPA建AEM，請參閱所選框架的入門指南。

* [入門 — SPA反AEM應](/help/sites-developing/spa-getting-started-react.md)
* [入門 — SPAAngular](/help/sites-developing/spa-getting-started-angular.md)

## 建AEM築SPA {#aem-architecture-and-spas}

使用時，AEM包括開發、創作和發佈環境的一般體系結構不會變SPA化。 但是，瞭解開發如何適SPA合此體系結構是有幫助的。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **構建環境**

   這是應用程式源和SPA元件源的源被檢出的位置。

   * NPM客戶端庫生成器從項目建立客戶端SPA庫。
   * 該庫將由Maven佔用，並由Maven Build插件以及AEM Author的元件部署。

* **AEM 作者**

   內容在作者上創AEM建，包括創SPA作。

   在創SPA作環境中使用SPA編輯器編輯時：

   1. 請求SPA外部HTML。
   1. 已載入CSS。
   1. 已載入應用SPA程式的Javascript。
   1. 執行應SPA用程式時，將請求JSON，允許應用生成包含 `cq-data` 屬性。
   1. 此 `cq-data` 屬性允許編輯器載入附加頁資訊，以便它知道哪些編輯配置可用於元件。

* **AEM 發佈**

   這是為公共消費發佈所創作的內容和已編SPA譯庫（包括應用程式對象、客戶端和元件）的地方。

* **分發程式/CDN**

   調度器用作站點訪AEM問者的快取層。

   * 處理請求的方式與AEM作者上的請求方式類似，但是沒有請求頁面資訊，因為編輯器只需要此資訊。
   * Javascript、CSS、JSON和HTML已快取，從而優化頁面以快速傳遞。

>[!NOTE]
>
>內部AEM不需要執行Javascript生成機制或執行Javascript本身。 只AEM承載應用程式中的已編SPA譯對象。

## 後續步驟 {#next-steps}

有關簡單結構的SPA概AEM述及其工作原理，請參閱兩者的入門指南 [反應](/help/sites-developing/spa-getting-started-react.md) 和 [Angular](/help/sites-developing/spa-getting-started-angular.md)。

有關建立自己的逐步指南的SPA資訊，請參閱 [編輯器入AEM門SPA- WKND事件教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

有關動態模型到元件映射及其在中的工作方式的詳細SPA信AEM息，請參閱文章 [動態模型到元件的映SPA射](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您希望在SPAReact或AEMAngular之外的框架中實施，或只是希望深入瞭解SDK的工SPA作方AEM式，請參閱 [藍SPA圖](/help/sites-developing/spa-blueprint.md) 文章。
