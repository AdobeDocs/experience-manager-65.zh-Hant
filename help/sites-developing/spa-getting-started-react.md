---
title: AEM中的SPA快速入門- React
seo-title: AEM中的SPA快速入門- React
description: 本文提供範例SPA應用程式，說明其組合方式，並讓您使用React架構快速啟動並執行您自己的SPA。
seo-description: 本文提供範例SPA應用程式，說明其組合方式，並讓您使用React架構快速啟動並執行您自己的SPA。
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# AEM中的SPA快速入門- React{#getting-started-with-spas-in-aem-react}

單頁應用程式(SPA)可為網站使用者提供引人入勝的體驗。 開發人員希望能夠使用SPA架構建立網站，而作者則想在AEM中為使用SPA架構建立的網站順暢地編輯內容。

SPA製作功能提供完整的解決方案，以支援AEM中的SPA。 本文介紹React架構上的簡化SPA應用程式，並說明其組合方式，讓您快速啟動並執行自己的SPA。

>[!NOTE]
>
>本文基於React框架。 如需Angular架構的對應檔案，請參 [閱「AEM - Angular中SPA快速入門」](/help/sites-developing/spa-getting-started-angular.md)。

>[!NOTE]
>
>SPA編輯器是建議的解決方案，適用於需要以SPA架構為基礎的用戶端轉換（例如React或Angular）的專案。

## 簡介 {#introduction}

本文摘述了簡單SPA的基本功能，以及您需要瞭解的最低功能，以便讓您的SPA運作。

如需SPA在AEM中運作的詳細資訊，請參閱下列檔案：

* [SPA簡介與逐步說明](/help/sites-developing/spa-walkthrough.md)
* [SPA製作簡介](/help/sites-developing/spa-overview.md)
* [SPA藍圖](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>為了能夠在SPA中製作內容，內容必須儲存在AEM中，並由內容模型公開。
>
>如果AEM以外開發的SPA不遵守內容模型合約，則無法授權。

本檔案將逐步介紹使用React架構建立的簡化SPA的結構，並說明其運作方式，讓您將此理解套用至您自己的SPA。

## 相依性、配置和構建 {#dependencies-configuration-and-building}

除了預期的React相依性外，範例SPA還可運用其他程式庫，讓建立SPA更有效率。

### 相依關係 {#dependencies}

該 `package.json` 檔案定義了整個SPA包的要求。 此處列出工作SPA的最低AEM相依性。

```
  "dependencies": {
    "@adobe/cq-react-editable-components": "~1.0.3",
    "@adobe/cq-spa-component-mapping": "~1.0.3",
    "@adobe/cq-spa-page-model-manager": "~1.0.4"
  }
```

由於此示例基於React框架，因此檔案中必須有兩個React-specific依賴 `package.json` 項：

```
react
 react-dom
```

利用 `aem-clientlib-generator` 此工具，在建立程式中自動建立用戶端程式庫。

`"aem-clientlib-generator": "^1.4.1",`

有關它的詳細資訊，請 [參閱此處](https://github.com/wcm-io-frontend/aem-clientlib-generator)。

>[!CAUTION]
>
>所需的最低 `aem-clientlib-generator` 版本為1.4.1。

檔案 `aem-clientlib-generator` 中的配置如 `clientlib.config.js` 下所示。

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

實際建立應用程式時，除了 [](https://webpack.js.org/) aem-clientlib-generator以自動建立用戶端程式庫外，還運用Webpack進行轉譯。 因此，build命令將類似：

`"build": "webpack && clientlib --verbose"`

建立後，套件就可以上傳至AEM例項。

### SPA Starter Kit的Maven Archetype {#maven-archetype-for-spa-starter-kit}

Adobe建議您運用 [Maven Archetype for SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype) ，協助您針對AEM開始自己的SPA專案。

## 應用程式結構 {#application-structure}

納入相依性並依照先前所述建立應用程式，將會留下您可上傳至AEM例項的正常SPA套件。

本檔案的下一節將帶您瞭解AEM中的SPA結構、驅動應用程式的重要檔案，以及它們如何搭配運作。

以簡化的影像元件為例，但應用程式的所有元件都是以相同的概念為基礎。

### index.js {#index-js}

進入SPA的入口點當然是此處所示 `index.js` 的檔案，可簡化以著重於重要內容。

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/cq-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

其主要功能 `index.js` 是運用函式來 `ReactDOM.render` 判斷DOM中要插入應用程式的位置。

這是此函式的標準使用，並非此範例應用程式的唯一使用。

#### 靜態實例化 {#static-instantiation}

當使用元件模板（如JSX）靜態實例化元件時，必須將值從模型傳遞到元件的屬性。

### App.js {#app-js}

透過轉譯應用程 `index.js` 式， `App.js`呼叫會以簡化版本顯示，以專注於重要內容。

```
import {Page, withModel } from '@adobe/cq-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 主要用來包覆構成應用程式的根元件。 任何應用程式的入口點都是頁面。

### Page.js {#page-js}

透過轉譯頁面，呼 `App.js` 叫會列 `Page.js` 在此處的簡化版本中。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/cq-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

在此範例中， `AppPage` 類別會 `Page`延伸，其中包含內部內容方法，然後可加以使用。

這 `Page` 會擷取頁面模型的JSON表示法，並處理內容以包覆／裝飾頁面的每個元素。 有關的詳細資 `Page` 訊，請參閱檔案 [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)。

### Image.js {#image-js}

在轉譯頁面時，可轉譯元件， `Image.js` 如此處所示。

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/cq-react-editable-components';

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

AEM中SPA的核心理念是將SPA元件對應至AEM元件，並在修改內容時更新元件（反之亦然）。 有關此通訊模 [型的摘要，請參閱文檔](/help/sites-developing/spa-overview.md) SPA編輯器概述。

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

方法 `MapTo` 會將SPA元件對應至AEM元件。 它支援使用單一字串或字串陣列。

`ImageEditConfig` 是配置對象，通過為編輯器提供生成佔位符所需的元資料來啟用元件的編寫功能

如果沒有內容，則會提供標籤作為預留位置來表示空內容。

#### 動態傳遞的屬性 {#dynamically-passed-properties}

來自模型的資料會動態傳遞為元件的屬性。

## 匯出可編輯的內容 {#exporting-editable-content}

您可以匯出元件並保留其可編輯性。

```
import React, { Component } from 'react';
import { MapTo } from '@cq/cq-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

函 `MapTo` 數返回 `Component` 合成結果，該合成結果擴展了提供的類名和屬 `PageClass` 性，使編寫成功成為可能。 此元件可匯出為稍後在應用程式的標籤中執行個體化。

使用或函 `MapTo` 數導出時，元件會用元件 `withModel``Page``ModelProvider` 包住，該元件可讓標準元件存取最新版本的頁面模型或該頁面模型中的精確位置。

如需詳細資訊，請參 [閱SPA Blueprint檔案](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743)。

>[!NOTE]
>
>預設情況下，在使用函式時，會接收元件的整個模 `withModel` 型。

## 在SPA元件之間共用資訊 {#sharing-information-between-spa-components}

單頁應用程式中的元件必須定期共用資訊。 有幾種建議的方法可做到，如下列出，增加了複雜性。

* **** 選項1:例如，使用React Context將邏輯和廣播集中到必要的元件。
* **** 選項2:使用狀態庫（例如Redux）來共用元件狀態。
* **** 選項3:自訂和擴充容器元件，以運用物件階層。

## 後續步驟 {#next-steps}

如需建立您自己SPA的逐步指南，請參閱「AEM SPA編輯器快速入門- WKND [事件教學課程」](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

如需如何組織您自己為AEM開發SPA的詳細資訊，請參閱「為AEM開 [發SPA」文章](/help/sites-developing/spa-architecture.md)。

如需動態模型至元件對應的詳細資訊，以及它在AEM中SPA中的運作方式，請參閱SPA的動態模型至元件對 [應文章](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您想要在AEM中針對React或Angular以外的架構實作SPA，或只想深入瞭解AEM的SPA SDK的運作方式，請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 文章。
