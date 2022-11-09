---
title: 開發SPA for AEM
seo-title: Developing SPAs for AEM
description: 本文提出在請前端開發人員開發SPA for AEM時應考慮的重要問題，並概述AEM的SPA架構，以備在AEM上部署開發的SPA時時所銘記。
seo-description: This article presents important questions to consider when engaging a front-end developer to develop a SPA for AEM as well as gives an overview of the architecture of AEM with respect to SPAs to keep in mind when deploying a developed SPA on AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 1%

---

# 開發SPA for AEM{#developing-spas-for-aem}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能使用SPA架構建立網站，而作者則想在AEM中為使用此架構建立的網站順暢地編輯內容。

本文提出在請前端開發人員開發SPA for AEM時應考慮的重要問題，並概述AEM在AEM上部署的架構。

>[!NOTE]
>
>若專案需要SPA架構的用戶端轉譯(例如React或Angular),SPA Editor是建議的解決方案。

## SPA的AEM開發原則 {#spa-development-principles-for-aem}

在AEM上開發單頁應用程式時，會假設前端開發人員在建立SPA時遵守標準最佳實務。 若您是前端開發人員，請遵循這些一般最佳實務以及幾項AEM專屬原則，您的SPA將可與 [AEM及其內容製作功能](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[便攜性](/help/sites-developing/spa-architecture.md#portability) -** 與任何元件一樣，元件應盡可能便攜。 SPA應使用可移植且可重複使用的元件來建立。
* **[AEM驅動器站點結構](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**  — 前端開發人員建立元件並擁有其內部結構，但需仰賴AEM來定義網站的內容結構。
* **[動態演算](/help/sites-developing/spa-architecture.md#dynamic-rendering)**  — 所有呈現應為動態。
* **[動態路由](#dynamic-routing) -** SPA會負責路由，AEM會監聽路由並據此擷取。 任何路由都應是動態的。

在開發SPA時，如果您應牢記這些原則，在啟用所有支援的AEM製作功能時，將盡可能提供靈活且未來的驗證。

如果您不需要支援AEM製作功能，則可能需要考慮不同的功能 [SPA設計模型](/help/sites-developing/spa-architecture.md#spa-design-models).

### 便攜性 {#portability}

與開發任何元件時一樣，您的元件的設計方式應最大限度地提高其可移植性。 任何與元件的可移植性或可重用性相抵觸的模式都應避免，以確保將來的相容性、靈活性和可維護性。

產生的SPA應包含高度可攜帶且可重複使用的元件。

### AEM驅動器站點結構 {#aem-drives-site-structure}

前端開發人員必須自認為負責建立用於建立應用程式的SPA元件程式庫。 前端顯影劑對元件的內部結構具有完全控制。 [但AEM隨時擁有網站的結構。](/help/sites-developing/spa-overview.md)

這表示前端開發人員可以在元件入口點之前或之後新增客戶內容，也可以在元件內進行第三方呼叫。 不過，前端開發人員無法完全控制元件的巢狀內嵌方式。

### 動態演算 {#dynamic-rendering}

SPA應僅依賴內容的動態轉譯。 這是AEM擷取並轉譯內容結構的所有子項的預設期望。

任何指向特定內容的明確轉譯都視為靜態轉譯，雖然受支援，但與AEM內容製作功能不相容。 這也違反了 [可攜性](/help/sites-developing/spa-architecture.md#portability).

### 動態路由 {#dynamic-routing}

與呈現一樣，所有路由也應是動態的。 在AEM中， [SPA應始終擁有路由](/help/sites-developing/spa-routing.md) 而AEM會監聽它，並據此擷取內容。

任何靜態路由都適用於 [可移植性原則](/help/sites-developing/spa-architecture.md#portability) 並因與AEM的內容製作功能不相容而限製作者。 例如，使用靜態路由時，如果內容作者想要變更路由或變更頁面，則必須要求前端開發人員執行此動作。

## AEM 專案原型 {#aem-project-archetype}

任何AEM專案皆應運用 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)，可支援使用React或Angular的SPA專案，並運用SPA SDK。

## SPA設計模型 {#spa-design-models}

若 [在AEM中開發SPA的原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) ，您的SPA將可搭配所有支援的AEM內容製作功能運作。

然而，在某些情況下，這並非完全必要。 下表概述了各種設計模型、其優點和缺點。

<table>
 <tbody>
  <tr>
   <th><strong>設計模型<br /> </strong></th>
   <th><strong>優點</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <td>AEM可作為無頭式CMS使用，而不使用 <a href="/help/sites-developing/spa-reference-materials.md">SPA Editor SDK架構。</a></td>
   <td>前端開發人員可完全控制應用程式。</td>
   <td><p>內容作者無法運用AEM內容製作體驗。</p> <p>如果代碼包含靜態引用或路由，則該代碼既不可移植，也不可重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>前端開發人員使用SPA Editor SDK架構，但只會向內容作者開啟部分區域。</td>
   <td>開發人員只會在應用程式的限制區域中啟用編寫功能，即可控制應用程式。</td>
   <td><p>內容作者受限於一組有限的AEM內容製作體驗。</p> <p>如果代碼包含靜態引用或路由，則該代碼可能不可移植或不可重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>專案會充分運用SPA Editor SDK，而前端元件會開發為程式庫，且應用程式的內容結構會委派給AEM。</td>
   <td><p>應用程式可重複使用且可攜帶。</p> <p>內容作者可使用AEM內容製作體驗來編輯應用程式。<br /> </p> <p>SPA與範本編輯器相容。</p> </td>
   <td><p>開發人員無法控制應用程式的結構和委派給AEM的內容部分。</p> <p>開發人員仍可針對不想使用AEM製作的內容，保留應用程式的區域。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>雖然AEM支援所有模型，但只有實作第三個模型(並因此遵循建議 [SPA在AEM中的開發原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem))，內容作者就能像習慣一樣與AEM中的SPA內容互動及編輯。

## 將現有SPA移轉至AEM {#migrating-existing-spas-to-aem}

一般而言，如果您的SPA遵循 [SPA的AEM開發原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)，您的SPA將可在AEM中運作，且可使用AEM SPA編輯器編輯。

請依照下列步驟操作，讓現有的SPA準備好搭配AEM使用。

1. **將JS元件設為模組化。**

   使它們能夠按任意順序、位置和大小呈現。
1. **使用SDK提供的容器，將元件放在畫面上。**

   AEM提供頁面和段落系統元件供您使用。
1. **為每個JS元件建立AEM元件。**

   AEM元件會定義對話方塊和JSON輸出。

## 前端開發人員的指示 {#instructions-for-front-end-developers}

讓前端開發人員建立SPA for AEM的主要任務是同意元件及其JSON模型。

以下概述前端開發人員在開發SPA for AEM時需遵循的步驟。

1. **同意元件及其JSON模型**

   前端開發人員和後端AEM開發人員必須就哪些元件和模型達成一致，以便從SPA元件到後端元件進行一對一的比對。

   AEM元件在提供編輯對話方塊和匯出元件模型時，仍大部分是必要的。

1. **在React元件中，透過`this.props.cqModel`**

   一旦同意元件並建置JSON模型後，前端開發人員就可以免費開發SPA，並只需透過存取JSON模型即可 `this.props.cqModel`.

1. **實作元件的 `render()` 方法**

   前端開發人員會實施 `render()` 方法，並可使用 `cqModel` 屬性。 這會輸出DOM以及要插入頁面的HTML片段。 這是在React中建立應用程式的標準方式。

1. **透過將元件對應至AEM資源類型`MapTo()`**

   映射儲存元件類，由提供的內部使用 `Container` 元件，以根據指定的資源類型來擷取元件並以動態方式具現化元件。

   這是前端與後端之間的「膠水」，讓編輯器知道反應元件對應的元件。

   此 `Page` 和 `ResponsiveGrid` 是擴展基礎的類的好示例 `Container`.

1. **定義元件的 `EditConfig` 作為參數`MapTo()`**

   此參數是必要的，用於告知編輯器，在尚未呈現或沒有要呈現的內容時，應如何命名元件。

1. **擴充提供的 `Container` 頁面和容器類別**

   頁面和段落系統應擴展此類，以使對內部元件的委派能夠正常工作。

1. **實作使用HTML5的路由解決方案 `History` API。**

   當 `ModelRouter` 已啟用，請呼叫 `pushState` 和 `replaceState` 函式會觸發向 `PageModelManager` 來擷取模型的遺失片段。

   的目前版本 `ModelRouter` 僅支援使用URL，指向Sling Model登入點的實際資源路徑。 不支援使用虛名URL或別名。

   此 `ModelRouter` 可以停用或設定為忽略規則運算式清單。

## AEM — 不可知 {#aem-agnostic}

這些程式碼區塊說明React和Angular元件如何不需要任何Adobe或AEM專用的項目。

* JavaScript元件內的所有項目均可在AEM中知曉。
* 但AEM的特定功能是，JS元件必須透過MapTo協助程式對應至AEM元件。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

此 `MapTo` helper是「膠水」，可讓後端和前端元件相配：

* 它會告訴JS容器（或JS段落系統）哪個JS元件要負責轉譯JSON中呈現的每個元件。
* 它會將HTML資料屬性新增至JS元件轉譯的HTML，讓SPA編輯器知道在編輯元件時要向作者顯示哪個對話方塊。

如需使用的詳細資訊 `MapTo` 和一般建置SPA for AEM，請參閱所選架構的快速入門手冊。

* [AEM中的SPA快速入門 — React](/help/sites-developing/spa-getting-started-react.md)
* [AEM中SPA快速入門 — Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM架構與SPA {#aem-architecture-and-spas}

使用SPA時，AEM的一般架構（包括開發、製作和發佈環境）不會變更。 不過，了解SPA開發如何融入此架構會很有幫助。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **組建環境**

   這是簽出SPA應用程式源和元件源的源。

   * NPM clientlib產生器會從SPA專案建立用戶端程式庫。
   * 該程式庫將由Maven擷取，並由Maven Build外掛程式與AEM Author的元件一起部署。

* **AEM 作者**

   內容是在AEM作者上建立，包括製作SPA。

   在製作環境中使用SPA編輯器編輯SPA時：

   1. SPA會要求外部HTML。
   1. CSS已載入。
   1. 已載入SPA應用程式的Javascript。
   1. 執行SPA應用程式時，會要求JSON，讓應用程式可建置頁面的DOM，包括 `cq-data` 屬性。
   1. 此 `cq-data` 屬性可讓編輯器載入其他頁面資訊，以便知道元件有哪些編輯設定可用。

* **AEM 發佈**

   這是發佈製作內容和已編譯程式庫(包括SPA應用程式成品、clientlib和元件)以供公眾使用的地方。

* **Dispatcher / CDN**

   Dispatcher可作為網站訪客的AEM快取層。

   * 處理請求的方式與AEM作者上的相似，不過不會要求頁面資訊，因為編輯器只需要這項資訊。
   * 系統會快取Javascript、CSS、JSON和HTML，最佳化頁面以快速傳送。

>[!NOTE]
>
>在AEM內，不需要執行Javascript建置機制或執行Javascript本身。 AEM只會托管SPA應用程式中已編譯的成品。

## 後續步驟 {#next-steps}

如需AEM中簡單SPA的結構及運作方式的概觀，請參閱兩者的快速入門手冊 [React](/help/sites-developing/spa-getting-started-react.md) 和 [Angular](/help/sites-developing/spa-getting-started-angular.md).

如需建立自己的SPA的逐步指南，請參閱 [AEM SPA Editor - WKND Events教學課程快速入門](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

如需動態模型與元件對應，以及其在AEM中於SPA內如何運作的詳細資訊，請參閱文章 [SPA的動態模型與元件對應](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

若您想在AEM中針對React或Angular以外的架構實作SPA，或只想深入探討SPA SDK for AEM的運作方式，請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 文章。
