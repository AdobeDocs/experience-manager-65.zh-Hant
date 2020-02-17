---
title: 開發AEM的SPA
seo-title: 開發AEM的SPA
description: 本文提出在雇用前端開發人員為AEM開發SPA時應考慮的重要問題，並概述AEM在AEM上部署開發的SPA時的SPA架構。
seo-description: 本文提出在雇用前端開發人員為AEM開發SPA時應考慮的重要問題，並概述AEM在AEM上部署開發的SPA時的SPA架構。
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# 開發AEM的SPA{#developing-spas-for-aem}

單頁應用程式(SPA)可為網站使用者提供引人入勝的體驗。 開發人員希望能夠使用SPA架構建立網站，而作者則想在AEM中順暢地編輯內容，以供使用此類架構建立的網站使用。

本文提出在與前端開發人員接洽以開發AEM的SPA時應考慮的重要問題，並概述AEM在AEM上部署SPA的架構。

>[!NOTE]
>
>SPA編輯器是建議的解決方案，適用於需要以SPA架構為基礎的用戶端轉換（例如React或Angular）的專案。

## AEM的SPA開發原則 {#spa-development-principles-for-aem}

在AEM上開發單頁應用程式時，前端開發人員在建立SPA時會遵循標準最佳實務。 如果您是前端開發人員，除了遵循這些一般最佳實務以及少數AEM特定原則外，您的SPA將能與 [AEM及其內容製作功能搭配運作](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)。

* **[可移植性](/help/sites-developing/spa-architecture.md#portability)-**—— 與任何元件一樣，元件應盡可能便攜。 SPA應使用可攜式和可重複使用的元件來建立。
* **[AEM Drives Site Structure](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**—— 前端開發人員會建立元件並擁有其內部結構，但需仰賴AEM來定義網站的內容結構。
* **[動態演算](/help/sites-developing/spa-architecture.md#dynamic-rendering)**-所有演算都應為動態。
* **[動態路由](#dynamic-routing)-**SPA負責路由，AEM會監聽路由並根據路由回遷。 任何路由都應是動態的。

如果您在開發SPA時牢記這些原則，將盡可能有彈性，並且能提供未來最佳證明，同時啟用所有支援的AEM製作功能。

如果您不需要支援AEM製作功能，可能需要考慮不同的 [SPA設計模型](/help/sites-developing/spa-architecture.md#spa-design-models)。

### 便攜性 {#portability}

與開發任何元件時一樣，您的元件的設計方式應能最大化其可移植性。 任何不利於元件可移植性或可重複使用性的模式都應避免，以確保未來的相容性、彈性和可維護性。

產生的SPA應使用高度可攜式和可重複使用的元件來建立。

### AEM Drives Site Structure {#aem-drives-site-structure}

前端開發人員必須認為自己負責建立用來建立應用程式的SPA元件庫。 前端顯影器可完全控制元件的內部結構。 [不過，AEM隨時擁有網站的結構。](/help/sites-developing/spa-overview.md)

這表示前端開發人員可在元件入口點之前或之後新增客戶內容，也可在元件內進行協力廠商呼叫。 不過，例如，前端開發人員無法完全控制元件的巢狀結構。

### 動態演算 {#dynamic-rendering}

SPA只應仰賴動態轉換內容。 這是AEM擷取和轉譯內容結構所有子系的預設期望值。 [](/help/sites-developing/spa-architecture.md#portability)

任何指向特定內容的明確轉譯都會視為靜態轉譯，雖然支援此功能，但將不相容於AEM的內容製作功能。 這也違背了可攜性的 [原則](/help/sites-developing/spa-architecture.md#portability)。

### 動態路由 {#dynamic-routing}

與渲染一樣，所有路由都應是動態的。 在AEM中， [SPA應一律擁有路由](/help/sites-developing/spa-routing.md) ,AEM會監聽路由並依此擷取內容。

任何靜態路由都違反可 [攜性原則](/help/sites-developing/spa-architecture.md#portability) ，而且與AEM的內容製作功能不相容，限制了作者。 例如，使用靜態路由時，如果內容作者想要變更路由或變更頁面，則必須要求前端開發人員完成。

## SPA Starter Kit的Maven Archetype {#maven-archetype-for-spa-starter-kit}

Adobe建議您運用 [Maven Archetype for SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype) ，協助您針對AEM開始自己的SPA專案。

## SPA設計模型 {#spa-design-models}

如果遵循 [在AEM中開發SPA的原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) ，則您的SPA將可與所有支援的AEM內容製作功能搭配運作。 [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

然而，在某些情況下，這並非完全必要。 下表概述了各種設計模型、它們的優點和缺點。

<table>
 <tbody>
  <tr>
   <th><strong>設計模型<br /> </strong></th>
   <th><strong>優勢</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <td>AEM可當成無頭CMS使用，而不使用 <a href="/help/sites-developing/spa-reference-materials.md">SPA編輯器SDK架構。</a></td>
   <td>前端開發人員可完全控制應用程式。</td>
   <td><p>內容製作者無法運用AEM的內容製作體驗。</p> <p>如果程式碼包含靜態參考或路由，則程式碼既不可攜式，也不可重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>前端開發人員使用SPA Editor SDK架構，但只會為內容作者開啟部分區域。</td>
   <td>開發人員只要在應用程式的限制區域啟用編寫功能，就能控制應用程式。</td>
   <td><p>內容作者只能使用AEM的一組有限的內容製作體驗。</p> <p>如果程式碼包含靜態參照或路由，則程式碼既不可攜式，也不可重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>專案完全運用SPA編輯器SDK，而前端元件則開發為程式庫，而應用程式的內容結構則委派給AEM。</td>
   <td><p>應用程式可重複使用且可攜式。</p> <p>內容作者可以使用AEM的內容製作體驗來編輯應用程式。<br /> </p> <p>SPA與範本編輯器相容。</p> </td>
   <td><p>開發人員無法控制應用程式的結構以及委派給AEM的內容部分。</p> <p>開發人員仍可針對非使用AEM製作的內容保留應用程式的區域。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>雖然AEM支援所有模型，但只有實作第三個模型(進而遵循AEM中建議的 [SPA開發原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem))，內容作者才能與AEM中的SPA內容互動並加以編輯。
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## 將現有SPA移轉至AEM {#migrating-existing-spas-to-aem}

一般而言，如果您的SPA遵循 [AEM的SPA開發原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)，則您的SPA將可在AEM中運作，並可使用AEM SPA編輯器進行編輯。

請依照下列步驟，讓您現有的SPA準備好與AEM搭配運作。

1. **將您的JS元件設為模組化。**

   使它們能夠以任何順序、位置和大小呈現。
1. **使用我們SDK提供的容器，將您的元件置於螢幕上。**

   AEM提供頁面和段落系統元件供您使用。
1. **為每個JS元件建立AEM元件。**

   AEM元件會定義對話方塊和JSON輸出。

## 前端開發人員的指示 {#instructions-for-front-end-developers}

招募前端開發人員以建立AEM的SPA時，主要的工作是同意元件及其JSON模型。

以下是前端開發人員在開發AEM的SPA時需要遵循的步驟概要。

1. **同意元件及其JSON模型**

   前端開發人員和後端AEM開發人員需要就哪些元件是必要的以及模型達成一致，以便從SPA元件到後端元件進行一對一的比對。

   AEM元件在提供編輯對話方塊和匯出元件模型時，仍然很有必要。

1. **在React元件中，透過`this.props.cqModel`**

   在元件達成一致且JSON模型就位後，前端開發人員就可免費開發SPA，而且只要透過存取JSON模型即可 `this.props.cqModel`。

1. **實作元件的方`render()`法**

   前端開發人員可依其所 `render()` 認為的適當方式實作方法，並可使用屬性的欄 `cqModel` 位。 這會輸出將插入頁面的DOM和HTML片段。 這是在React中建立應用程式的標準方式。

1. **將元件對應至AEM資源類型(透過`MapTo()`**

   該映射儲存元件類，並由提供的元件內部使用，以基 `Container` 於給定資源類型檢索和動態實例化元件。

   這是前端與後端之間的「黏合劑」，讓編輯者知道反應元件對應的元件。

   和 `Page` 是 `ResponsiveGrid` 擴展基礎的類的好示例 `Container`。

1. **將元件定義為參`EditConfig`數，以便`MapTo()`**

   此參數是必要的，以告知編輯器，如何將元件命名為at，但尚未轉譯或沒有要轉譯的內容。

1. **擴充提供的`Container`頁面和容器類別**

   頁面和段落系統應擴充此類別，讓委派至內部元件如預期般運作。

1. **實作使用HTML5`History`API的路由選擇解決方案。**

   啟用 `ModelRouter` 後，調用和 `pushState` 函 `replaceState` 數將觸發請求， `PageModelManager` 以提取模型的缺失片段。

   目前版本僅支 `ModelRouter` 援使用指向Sling Model入口點實際資源路徑的URL。 它不支援使用虛名URL或別名。

   可禁 `ModelRouter` 用或配置為忽略規則表達式清單。

## AEM-不可知論者 {#aem-agnostic}

這些程式碼區塊說明您的React和Angular元件不需要Adobe或AEM專用的元件。

* JavaScript元件內的一切都與AEM無關。
* 但AEM的特定功能是，JS元件必須與MapTo協助程式對應至AEM元件。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

幫 `MapTo` 手是「黏合」，可讓後端和前端元件搭配使用：

* 它會告訴JS容器（或JS段落系統）JS元件要負責轉譯JSON中每個元件。
* 它會新增HTML資料屬性至JS元件轉譯的HTML，讓SPA編輯器知道在編輯元件時要向作者顯示哪些對話方塊。

如需一般使用和建 `MapTo` 立AEM適用之SPA的詳細資訊，請參閱您所選架構的快速入門手冊。

* [AEM中的SPA快速入門- React](/help/sites-developing/spa-getting-started-react.md)
* [AEM中的SPA快速入門- Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM架構與SPA {#aem-architecture-and-spas}

使用SPA時，AEM的一般架構（包括開發、製作和發佈環境）不會變更。 不過，瞭解SPA開發如何與此架構整合，會有所幫助。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **構建環境**

   這是檢出SPA應用程式源和元件源的源的位置。

   * NPM clientlib產生器會從SPA專案建立用戶端程式庫。
   * Maven將會擷取該程式庫，並由Maven Build外掛程式與AEM Author的元件一起部署。

* **AEM 作者**

   內容是在AEM作者上建立，包括編寫SPA。

   在編寫環境中使用SPA編輯器編輯SPA時：

   1. SPA要求外部HTML。
   1. CSS已載入。
   1. 載入SPA應用程式的Javascript。
   1. 執行SPA應用程式時，會要求JSON，讓應用程式可建立包含屬性的頁面DOM `cq-data` 。
   1. 此屬 `cq-data` 性可讓編輯者載入其他頁面資訊，以便知道元件有哪些編輯組態可供使用。

* **AEM 發佈**

   在此處，編寫的內容和編譯庫（包括SPA應用程式對象、clientlibs和元件）將發佈供公共使用。

* **Dispatcher / CDN**

   Dispatcher可當成AEM的快取層，供網站的訪客使用。

   * 處理請求的方式與在AEM Author上的方式類似，但是沒有請求頁面資訊，因為這只是編輯者需要的。
   * 快取Javascript、CSS、JSON和HTML，最佳化頁面以快速傳送。

>[!NOTE]
>
>在AEM內部，不需要執行Javascript建立機制或執行Javascript本身。 AEM僅托管SPA應用程式中編譯的對象。

## 後續步驟 {#next-steps}

如需AEM中簡易SPA的結構及運作方式的概觀，請參閱 [React](/help/sites-developing/spa-getting-started-react.md) 和 [Angular的入門指南](/help/sites-developing/spa-getting-started-angular.md)。

如需建立您自己SPA的逐步指南，請參閱「AEM SPA編輯器快速入門- WKND [事件教學課程」](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

如需動態模型至元件對應的詳細資訊，以及它在AEM中SPA中的運作方式，請參閱SPA的動態模型至元件對 [應文章](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您想要在AEM中針對React或Angular以外的架構實作SPA，或只想深入瞭解AEM的SPA SDK的運作方式，請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 文章。
