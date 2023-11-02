---
title: AEM中的SPA快速入門 — React
seo-title: Getting Started with SPAs in AEM - React
description: 本文介紹了一個SPA應用計畫範例，說明它是如何組合在一起的，並可讓您使用React框架快速啟動並執行您自己的SPA。
seo-description: This article presents a sample SPA application, explains how it is put together, and lets you get up-and-running with your own SPA quickly using the React framework.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 4%

---

# AEM中的SPA快速入門 — React{#getting-started-with-spas-in-aem-react}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能使用SPA架構建立網站，而作者則想在AEM中順暢地編輯使用SPA架構建立之網站的內容。

SPA編寫功能提供全方位的解決方案，可支援AEM中的SPA。 本文介紹React架構上的簡化SPA應用程式，說明其如何組合，讓您快速啟動並執行自己的SPA。

>[!NOTE]
>
>本文章內容以React架構為基礎。 有關Angular架構的對應檔案，請參閱 [AEM中的SPA快速入門 — Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>對於需要以SPA框架為基礎的使用者端轉譯(例如React或Angular)專案，建議使用SPA編輯器解決方案。

## 簡介 {#introduction}

本文概述簡單的SPA的基本功能，以及您需要瞭解的最少運作資訊。

如需SPA在AEM中運作方式的詳細資訊，請參閱下列檔案：

* [SPA 簡介和逐步解說](/help/sites-developing/spa-walkthrough.md)
* [SPA製作簡介](/help/sites-developing/spa-overview.md)
* [SPA 藍圖](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>為了能夠在SPA內製作內容，內容必須儲存在AEM中，並由內容模型公開。
>
>若在AEM外部開發的SPA未遵循內容模型合約，將無法編寫。

本檔案將逐步解說使用React架構建立的簡化SPA結構，並說明其運作方式，以便您將此瞭解套用至您自己的SPA。

## 相依性、設定和建置 {#dependencies-configuration-and-building}

除了預期的React相依性之外，範例SPA還可以運用其他程式庫，以更有效率地建立SPA。

### 相依性 {#dependencies}

此 `package.json` 檔案定義整體SPA套件的需求。 此處列出運作中AEM的最小SPA相依性。

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

由於此範例是以React架構為基礎，因此中有兩個React專用相依性是此架構中的必備專案： `package.json` 檔案：

```
react
 react-dom
```

此 `aem-clientlib-generator` 用於隨著建置流程自動建立使用者端程式庫。

`"aem-clientlib-generator": "^1.4.1",`

可找到更多相關詳細資訊 [在此填入GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>的最低版本 `aem-clientlib-generator` 「必要」為1.4.1。

此 `aem-clientlib-generator` 的設定位置： `clientlib.config.js` 檔案如下所示。

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### 正在建置 {#building}

實際建立應用程式 [Webpack](https://webpack.js.org/) 用於整合，以及自動建立使用者端程式庫的aem-clientlib-generator。 因此， build指令將類似於：

`"build": "webpack && clientlib --verbose"`

建置後，封裝可以上傳到AEM執行個體。

### AEM 專案原型 {#aem-project-archetype}

任何 AEM 專案都應利用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支援使用 React 或 Angular 的 SPA 專案並利用 SPA SDK。

## 應用程式結構 {#application-structure}

如前所述，包含相依性並建置您的應用程式後，您將會擁有可上傳至SPA執行個體的有效AEM套件。

本檔案的下一節將帶您瞭解AEM中SPA的結構、驅動應用程式的重要檔案，以及它們如何協同運作。

簡化的影像元件可作為範例，但應用程式的所有元件都根據相同的概念。

### index.js {#index-js}

SPA的進入點當然是 `index.js` 此處顯示的檔案已簡化，以專注於重要內容。

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

的主要功能 `index.js` 就是利用 `ReactDOM.render` 函式，可判斷DOM中要插入應用程式的位置。

這是此函式的標準用法，並非此範例應用程式所特有。

#### 靜態具現化 {#static-instantiation}

使用元件範本（例如JSX）以靜態方式例項化元件時，必須將值從模型傳遞至元件的屬性。

### App.js {#app-js}

透過轉譯應用程式， `index.js` 呼叫 `App.js`，此處以簡化版顯示，著重於重要內容。

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 主要用途是包裝構成應用程式的根元件。 任何應用程式的進入點是頁面。

### Page.js {#page-js}

轉譯頁面時， `App.js` 呼叫 `Page.js` 此處以簡化版列出。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

在此範例中 `AppPage` 類別擴充 `Page`，其中包含後續可使用的內部內容方法。

此 `Page` 擷取頁面模型的JSON表示法，並處理內容以包裝/裝飾頁面的每個元素。 進一步詳細資訊，請參閱 `Page` 可以在檔案中找到 [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

呈現頁面時，元件(例如 `Image.js` 如此處所示，皆可呈現。

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

AEM中SPA的核心構想是將該SPA元件對應至AEM元件，並在修改內容時更新元件（反之亦然）。 檢視檔案 [SPA編輯器概觀](/help/sites-developing/spa-overview.md) 以取得此通訊模式的摘要。

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

此 `MapTo` 方法將SPA元件對應至AEM元件。 它支援使用單一字串或字串陣列。

`ImageEditConfig` 是組態物件，可為編輯器提供產生預留位置所需的中繼資料，有助於啟用元件的製作功能

如果沒有內容，則會提供標籤做為預留位置，以代表空白內容。

#### 動態傳遞的屬性 {#dynamically-passed-properties}

來自模型的資料會以元件屬性的形式動態傳遞。

## 匯出可編輯的內容 {#exporting-editable-content}

您可以匯出元件並使其可編輯。

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

此 `MapTo` 函式傳回 `Component` 這是延伸所提供的構成的結果 `PageClass` 類別名稱和屬性啟用編寫功能。 此元件可匯出以供稍後在應用程式的標籤中具現化。

使用匯出時 `MapTo` 或 `withModel` 函式， `Page` 元件，以 `ModelProvider` 可讓標準元件存取最新版本頁面模型或該頁面模型中的精確位置的元件。

如需詳細資訊，請參閱 [SPA Blueprint檔案](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>依預設，使用時您會收到元件的整個模型 `withModel` 函式。

## 在SPA元件之間共用資訊 {#sharing-information-between-spa-components}

單頁應用程式內的元件定期需要共用資訊。 有幾種建議的方法可以達成此目的，依複雜度遞增的順序列示如下。

* **選項1：** 集中邏輯並廣播至必要的元件，例如透過使用React Context。
* **選項2：** 使用狀態庫（例如Redux）共用元件狀態。
* **選項3：** 透過自訂和擴充容器元件來利用物件階層。

## 後續步驟 {#next-steps}

如需建立您自己的SPA的逐步指南，請參閱 [AEM SPA編輯器快速入門 — WKND事件教學課程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

如需有關如何組織自己以開發適用於AEM的SPA的詳細資訊，請參閱文章 [為AEM開發SPA](/help/sites-developing/spa-architecture.md).

如需有關動態模型到元件對應的更多詳細資訊，以及它如何在AEM的SPA中運作，請參閱文章 [SPA的動態模型至元件對應](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

如果您想在AEM中為React或Angular以外的框架實作SPA，或只是想深入瞭解適用於AEM的SPA SDK的運作方式，請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 文章。
