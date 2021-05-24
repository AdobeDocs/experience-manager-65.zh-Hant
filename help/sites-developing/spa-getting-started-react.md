---
title: AEM中的SPA快速入門 — React
seo-title: AEM中的SPA快速入門 — React
description: 本文提供範例SPA應用程式，說明其組合方式，並可讓您使用React架構快速上手並執行自己的SPA。
seo-description: 本文提供範例SPA應用程式，說明其組合方式，並可讓您使用React架構快速上手並執行自己的SPA。
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 2%

---

# AEM中的SPA快速入門 — React{#getting-started-with-spas-in-aem-react}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能使用SPA架構建立網站，而作者則想在AEM中為使用SPA架構建立的網站順暢地編輯內容。

SPA製作功能提供全方位的解決方案，可支援AEM中的SPA。 本文介紹React架構上的簡化SPA應用程式，說明其組合方式，讓您能夠快速上手並執行自己的SPA。

>[!NOTE]
>
>本文以React架構為基礎。 如需Angular架構的對應檔案，請參閱[AEM中SPA快速入門 — Angular](/help/sites-developing/spa-getting-started-angular.md)。

>[!NOTE]
>
>若專案需要SPA架構的用戶端轉譯(例如React或Angular),SPA Editor是建議的解決方案。

## 簡介 {#introduction}

本文概述簡單SPA的基本功能，以及您執行作業所需了解的最低限度。

如需SPA在AEM中如何運作的詳細資訊，請參閱下列檔案：

* [SPA簡介和逐步說明](/help/sites-developing/spa-walkthrough.md)
* [SPA製作簡介](/help/sites-developing/spa-overview.md)
* [SPA Blueprint](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>為了能在SPA內製作內容，內容必須儲存在AEM中，並由內容模型公開。
>
>若SPA不遵守內容模型合約，則在AEM外部開發的Analytics將無法授權。

本檔案將逐步說明使用React架構建立的簡化SPA的結構，並說明其運作方式，以便您將這項了解套用至您自己的SPA。

## 相依性、配置和構建{#dependencies-configuration-and-building}

除了預期的React相依性外，範例SPA還可運用其他程式庫，讓SPA的建立更有效率。

### 相依關係 {#dependencies}

`package.json`檔案定義了整體SPA套件的要求。 此處列出運作中SPA的最低AEM相依性。

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

因為此範例以React架構為基礎，`package.json`檔案中必須有兩個React特定相依性：

```
react
 react-dom
```

系統會運用`aem-clientlib-generator`，讓用戶端程式庫的建立作為建立程式的一部分而自動執行。

`"aem-clientlib-generator": "^1.4.1",`

如需其詳細資訊，請前往[這裡的GitHub。](https://github.com/wcm-io-frontend/aem-clientlib-generator)

>[!CAUTION]
>
>所需的`aem-clientlib-generator`最低版本為1.4.1。

`aem-clientlib-generator`在`clientlib.config.js`檔案中配置如下。

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

實際建置應用程式時，除了可自動建立用戶端程式庫的aem-clientlib-generator外，還可運用[Webpack](https://webpack.js.org/)進行轉譯。 因此，build命令將類似於：

`"build": "webpack && clientlib --verbose"`

建置後，可將套件上傳至AEM例項。

### AEM 專案原型 {#aem-project-archetype}

任何AEM專案都應運用[AEM專案原型](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/developing/archetype/overview.html)，這可支援使用React或Angular的SPA專案，並運用SPA SDK。

## 應用程式結構{#application-structure}

如先前所述，包括相依性和建立應用程式，讓您得到可上傳至AEM例項的有效SPA套件。

本檔案的下一節將帶您了解AEM中SPA的架構方式、驅動應用程式的重要檔案，以及它們如何共同運作。

以簡化的影像元件為例，但應用程式的所有元件都以相同的概念為基礎。

### index.js {#index-js}

進入SPA的入口點當然是此處顯示的`index.js`檔案簡化，以著重於重要內容。

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

`index.js`的主要函式是運用`ReactDOM.render`函式，以判斷DOM中要插入應用程式的位置。

此為此函式的標準使用，並非此範例應用程式所獨有。

#### 靜態實例化{#static-instantiation}

使用元件模板（如JSX）靜態實例化元件時，必須將值從模型傳遞到元件的屬性。

### App.js {#app-js}

透過呈現應用程式，`index.js`會呼叫`App.js`，此處以簡化版本顯示，以著重於重要內容。

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` 主要作用是包裝構成應用程式的根元件。任何應用程式的進入點都是頁面。

### Page.js {#page-js}

透過呈現頁面，`App.js`會呼叫此處所列的`Page.js`簡化版本。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

在此示例中，`AppPage`類擴展`Page`，它包含隨後可使用的內部內容方法。

`Page`會擷取頁面模型的JSON表示法，並處理內容以包裝/裝飾頁面的每個元素。 有關`Page`的進一步詳細資訊，請參閱文檔[SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)。

### Image.js {#image-js}

透過轉譯的頁面，即可轉譯此處所示的元件，例如`Image.js`。

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

AEM中SPA的核心思想是將SPA元件對應至AEM元件，以及在修改內容時更新元件（反之亦然）。 有關此通信模型的摘要，請參閱文檔[SPA編輯器概述](/help/sites-developing/spa-overview.md)。

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

`MapTo`方法將SPA元件對應至AEM元件。 支援使用單一字串或字串陣列。

`ImageEditConfig` 是配置對象，通過為編輯器提供必要的元資料來生成佔位符，有助於啟用元件的創作功能

如果沒有內容，則會提供標籤作為預留位置來表示空白內容。

#### 動態傳遞的屬性{#dynamically-passed-properties}

來自模型的資料會以元件屬性的形式動態傳遞。

## 導出可編輯的內容{#exporting-editable-content}

您可以匯出元件，使其保持可編輯狀態。

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

`MapTo`函式返回`Component`，該函式是組合的結果，該組合使用啟用創作的類名和屬性擴展提供的`PageClass`。 此元件可匯出至，稍後在應用程式的標籤中實例化。

使用`MapTo`或`withModel`函式導出時，`Page`元件會用`ModelProvider`元件包住，該元件提供標準元件訪問頁面模型的最新版本或該頁面模型中的精確位置。

如需詳細資訊，請參閱[SPA Blueprint檔案](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743)。

>[!NOTE]
>
>預設情況下，使用`withModel`函式時，將接收元件的整個模型。

## 在SPA元件{#sharing-information-between-spa-components}之間共用資訊

單頁應用程式中的元件必須經常共用資訊。 執行此作業有數種建議方法，如下所列，其複雜度會隨之增加。

* **選項1:** 集中邏輯並廣播至必要的元件，例如使用React Context。
* **選項2:** 使用狀態程式庫（例如Redux）來共用元件狀態。
* **選項3:** 自訂和擴充容器元件，以運用物件階層。

## 後續步驟{#next-steps}

如需建立自己的SPA的逐步指南，請參閱[AEM SPA編輯器快速入門 — WKND事件教學課程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

如需如何組織您自己開發SPA for AEM的詳細資訊，請參閱[開發SPA for AEM](/help/sites-developing/spa-architecture.md)一文。

有關動態模型到元件映射及其在AEM中在SPA內如何運作的詳細資訊，請參閱文章[SPA的動態模型到元件映射](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

若您想在AEM中針對React或Angular以外的架構實作SPA，或只想深入探討SPA SDK for AEM的運作方式，請參閱[SPA Blueprint](/help/sites-developing/spa-blueprint.md)文章。
