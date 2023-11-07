---
title: 為Adobe Experience Manager開發SPA
description: 本文介紹當請前端開發人員為Adobe Experience Manager (AEM)開發SPA時需要考慮的重要問題，並提供AEM有關SPA的架構概覽，以便在在AEM上部署開發的SPA時牢記在心。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 6%

---

# 針對 AEM 開發 SPA{#developing-spas-for-aem}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能使用SPA架構建立網站，而作者則想在Adobe Experience Manager (AEM)中順暢地編輯使用這類架構建立之網站的內容。

本文介紹當請前端開發人員為AEM開發SPA時應考慮的重要問題，並概述有關在AEM上部署SPA的AEM架構。

>[!NOTE]
>
>對於需要以SPA框架為基礎的使用者端轉譯(例如React或Angular)專案，建議使用SPA編輯器解決方案。

## AEM的SPA開發原則 {#spa-development-principles-for-aem}

在 AEM 開發單頁應用程式是假設前端開發人員在建立 SPA 時有遵守標準最佳做法。如果您身為前端開發人員，遵循這些一般最佳實務和一些AEM特定原則，您的SPA將可在下列程式碼中運作： [AEM及其內容製作功能](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[可攜性](/help/sites-developing/spa-architecture.md#portability) -** 與任何元件一樣，應該儘可能將元件建置為可攜式。 SPA 應該使用可攜帶和可重複使用的元件建置。
* **[AEM 促成網站結構](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** - 前端開發人員建立元件並擁有其內部結構，但依賴 AEM 來定義網站的內容結構。
* **[動態呈現](/help/sites-developing/spa-architecture.md#dynamic-rendering)** - 所有呈現都應該是動態的。
* **[動態路由](#dynamic-routing) -** SPA負責製程，AEM會接聽該製程並根據該製程進行擷取。 任何路由也應該是動態的。

如果您在開發SPA時牢記這些原則，在啟用所有支援的AEM編寫功能時，將會儘可能靈活且符合未來需求。

如果您不需要支援AEM編寫功能，您可能需要考慮其他功能 [SPA設計模型](/help/sites-developing/spa-architecture.md#spa-design-models).

### 可攜性 {#portability}

如同開發任何元件一樣，元件的設計應儘可能提高可攜性。 應避免任何影響元件可攜性或重複使用的模式，以確保日後相容性、彈性和可維護性。

產生的SPA應使用可高度攜式且可重複使用的元件來建置。

### AEM磁碟機網站結構 {#aem-drives-site-structure}

前端開發人員必須自行負責建立用於建置應用程式的SPA元件程式庫。 前端開發人員可完全控制元件的內部結構。 [但是，AEM在任何時候都擁有網站結構。](/help/sites-developing/spa-overview.md)

這表示前端開發人員可在元件進入點之前或之後新增客戶內容，且也可以在元件內進行第三方呼叫。 但是，前端開發人員無法完全控制元件的巢狀內嵌方式，例如，

### 動態演算 {#dynamic-rendering}

SPA應該僅依賴內容的動態呈現。 這是AEM擷取並轉譯內容結構之所有子項的預設預期。

任何指向特定內容的明確呈現都會視為靜態呈現，雖然支援此功能，但不會與AEM內容製作功能相容。 這也違反了 [可攜性](/help/sites-developing/spa-architecture.md#portability).

### 動態路由 {#dynamic-routing}

如同轉譯一樣，所有路由也應是動態的。 在AEM中 [SPA應該一律擁有路由](/help/sites-developing/spa-routing.md) 和AEM會監聽它，並根據它擷取內容。

任何靜態路由都適用於 [可攜性原則](/help/sites-developing/spa-architecture.md#portability) 和因為與AEM的內容製作功能不相容而限製作者。 例如，使用靜態路由，如果內容作者想要變更路由或變更頁面，作者必須要求前端開發人員這麼做。

## AEM 專案原型 {#aem-project-archetype}

任何 AEM 專案都應使用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支援使用 React 或 Angular 的 SPA 專案並使用 SPA SDK。

## SPA設計模型 {#spa-design-models}

如果 [在AEM中開發SPA的原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) 後續步驟，則您的SPA將可搭配所有支援的AEM內容製作功能運作。

不過，在某些情況下，這並非完全必要。 下表概述各種設計模型、其優點和缺點。

<table>
 <tbody>
  <tr>
   <th><strong>設計模型<br /> </strong></th>
   <th><strong>優點</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <td>AEM用作Headless CMS，而不使用 <a href="/help/sites-developing/spa-reference-materials.md">SPA編輯器SDK架構。</a></td>
   <td>前端開發人員可完全控制應用程式。</td>
   <td><p>內容作者無法使用AEM內容製作體驗。</p> <p>如果程式碼包含靜態參照或路由，就無法移植或重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>前端開發人員使用SPA Editor SDK架構，但只對內容作者開啟部分割槽域。</td>
   <td>開發人員僅會在應用程式的受限制區域中啟用撰寫功能，以保留對應用程式的控制。</td>
   <td><p>內容作者受限於有限的AEM內容製作體驗。</p> <p>如果程式碼包含靜態參考或路由，則可能無法移植或重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>專案會完全使用SPA編輯器SDK，而前端元件會開發為程式庫，而應用程式的內容結構會委派給AEM。</td>
   <td><p>應用程式可重複使用且可移植。</p> <p>內容作者可使用AEM內容製作體驗來編輯應用程式。<br /> </p> <p>SPA與範本編輯器相容。</p> </td>
   <td><p>開發人員無法控制應用程式的結構和委派給AEM的內容部分。</p> <p>開發人員仍可保留應用程式的區域，以供不應使用AEM編寫的內容使用。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>雖然AEM支援所有模型，但僅實作第三種（並因而遵循建議的） [AEM中的SPA開發原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem))內容作者是否能夠在AEM中與自訂的SPA內容互動及編輯內容。

## 將現有SPA移轉至AEM {#migrating-existing-spas-to-aem}

一般而言，如果您的SPA遵循 [AEM的SPA開發原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)，則您的SPA將會在AEM中運作，並可使用AEM SPA編輯器進行編輯。

請依照下列步驟，讓現有的SPA準備好搭配AEM使用。

1. **將您的JS元件模組化。**

   使其能夠以任何順序、位置和大小呈現。
1. **使用Adobe SDK提供的容器，將您的元件放置在畫面上。**

   AEM提供頁面和段落系統元件供您使用。
1. **為每個JS元件建立AEM元件。**

   AEM元件會定義對話方塊和JSON輸出。

## 面向前端開發人員的說明 {#instructions-for-front-end-developers}

與前端開發人員共同建立AEM適用的SPA，主要工作是就元件及其JSON模型達成共識。

以下概述前端開發人員在為AEM開發SPA時需要遵循的步驟。

1. **同意元件及其JSON模型**

   前端開發人員和後端AEM開發人員需要就哪些元件是必要元件和模型達成共識，以便從SPA元件與後端元件進行一對一比對。

   仍需要使用AEM元件來提供編輯對話方塊及匯出元件模型。

1. **在React元件中，透過存取模型`this.props.cqModel`**

   在同意元件且JSON模型就緒後，前端開發人員即可自由開發SPA，並可透過存取JSON模型 `this.props.cqModel`.

1. **實作元件的 `render()` 方法**

   前端開發人員實作 `render()` 方法會適當地顯示，而且可以使用 `cqModel` 屬性。 這會輸出插入頁面的DOM和HTML片段。 這是在React中建立應用程式的標準方式。

1. **透過將元件對應至AEM資源型別`MapTo()`**

   對應會儲存元件類別，並由提供的內部使用 `Container` 元件，可根據指定的資源型別擷取及動態例項化元件。

   這相當於前端和後端之間的「粘合」，因此編輯器可以知道哪些元件與react元件相對應。

   此 `Page` 和 `ResponsiveGrid` 是擴充基底的類別的良好範例 `Container`.

1. **定義元件的 `EditConfig` 作為引數`MapTo()`**

   只要尚未轉譯或沒有可轉譯的內容，此引數是告訴編輯器元件應如何命名所必需的。

1. **擴充提供的 `Container` 頁面和容器的類別**

   頁面和段落系統應該擴充此類別，好讓委派給內部元件的功能可如預期運作。

1. **實作路由解決方案，該解決方案使用HTML5 `History` API。**

   當 `ModelRouter` 已啟用，呼叫 `pushState` 和 `replaceState` 函式觸發要求 `PageModelManager` 以擷取模型的遺失片段。

   目前版本的 `ModelRouter` 僅支援使用指向Sling模型進入點的實際資源路徑的URL。 不支援使用虛名URL或別名。

   此 `ModelRouter` 可停用或設定為忽略規則運算式清單。

## 與AEM無關 {#aem-agnostic}

這些程式碼區塊說明您的React和Angular元件如何不需要任何特定於Adobe或AEM的內容。

* JavaScript元件內的所有內容都與AEM無關。
* 不過，AEM的專屬之處在於，JS元件必須使用MapTo協助程式對應至AEM元件。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

此 `MapTo` 協助程式是讓後端和前端元件搭配在一起的「粘合劑」：

* 它會告訴JS容器（或JS段落系統）哪個JS元件負責轉譯JSON中存在的每個元件。
* 它會將HTML資料屬性新增至JS元件轉譯的HTML，這樣SPA編輯器就知道在編輯元件時要向作者顯示的對話方塊。

如需關於使用的詳細資訊 `MapTo` 以及建置SPA for AEM的一般資訊，請參閱所選架構的快速入門手冊。

* [AEM中的SPA快速入門 — React](/help/sites-developing/spa-getting-started-react.md)
* [AEM中的SPA快速入門 — Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM架構和SPA {#aem-architecture-and-spas}

AEM的一般架構（包括開發、編寫和發佈環境）在使用SPA時不會變更。 不過，瞭解SPA開發如何適應此架構會很有幫助。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **組建環境**

  這是出庫SPA應用程式來源和元件來源的位置。

   * NPM clientlib產生器會從SPA專案建立使用者端程式庫。
   * 該程式庫由Maven取得，並由Maven Build外掛程式與元件部署到AEM Author。

* **AEM 作者**

  內容是在AEM作者上建立，包括編寫SPA。

  在編寫環境中使用SPA編輯器編輯SPA時：

   1. SPA會要求外部HTML。
   1. CSS已載入。
   1. SPA應用程式的JavaScript已載入。
   1. 執行SPA應用程式時，系統會要求JSON，允許應用程式建立頁面的DOM，包括 `cq-data` 屬性。
   1. 這個 `cq-data` 屬性可讓編輯器載入其他頁面資訊，以便知道元件有哪些編輯設定可用。

* **AEM 發佈**

  這是發佈編寫的內容和編譯的程式庫(包括SPA應用程式成品、clientlibs和元件)以供公眾使用的位置。

* **Dispatcher / CDN**

  Dispatcher是網站訪客的AEM快取階層。

   * 要求的處理方式類似於AEM作者上的要求，不過不會要求頁面資訊，因為只有編輯器需要它。
   * 快取JavaScript、CSS、JSON和HTML，最佳化頁面以快速傳送。

>[!NOTE]
>
>在AEM內，不需要執行JavaScript建置機制或執行JavaScript本身。 AEM僅代管來自SPA應用程式的編譯成品。

## 後續步驟 {#next-steps}

如需如何在AEM中建構簡單SPA及其運作方式的概觀，請參閱兩者的快速入門手冊 [React](/help/sites-developing/spa-getting-started-react.md) 和 [angular](/help/sites-developing/spa-getting-started-angular.md).

如需建立您自己的SPA的逐步指南，請參閱 [AEM SPA編輯器快速入門 — WKND事件教學課程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

如需有關動態模型到元件對應的更多詳細資訊，以及它如何在AEM的SPA中運作，請參閱文章 [SPA的動態模型至元件對應](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

如果您想在AEM中為React或Angular以外的框架實作SPA，或只是想深入瞭解適用於AEM的SPA SDK的運作方式，請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 文章。
