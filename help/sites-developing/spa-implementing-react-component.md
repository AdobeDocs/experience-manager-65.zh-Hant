---
title: 針對 SPA 實作 React元件
seo-title: Implementing a React Component for SPA
description: 本文舉例說明如何調整一個簡單、現有的React元件來與編輯器AEMSPA配合。
seo-description: This article presents an example of how to adapt a simple, existing React component to work with the AEM SPA Editor.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: afd2afe182d65e64c0ad851b86021886078a9dd5
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 11%

---

# 針對 SPA 實作 React元件{#implementing-a-react-component-for-spa}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能夠使用框架構建站SPA點，而作者希望無縫地編輯AEM使用框架構建的站SPA點的內容。

創SPA作功能提供了全面的解決方案，SPA支援AEM內。 本文舉例說明如何調整一個簡單、現有的React元件來與編輯器AEMSPA配合。

>[!NOTE]
>
>編輯SPA器是需要基於框架的SPA客戶端呈現(例如，反應或Angular)的項目的推薦解決方案。

## 簡介 {#introduction}

由於與編輯器之間需要AEM並建立的簡單輕量SPA合同SPA，所以使用現有的Javascript應用程式並對其進行修改以供與inSPA的使AEM用是一件簡單的事。

本文說明了We.Retail Journal示例中的天氣元件示例SPA。

你應該熟悉 [應用程式SPA的結AEM構](/help/sites-developing/spa-getting-started-react.md) 讀這篇文章之前。

>[!CAUTION]
>此文檔使用 [We.Retail Journal應用](https://github.com/adobe/aem-sample-we-retail-journal) 僅供演示之用。 它不應用於任何專案。
>
>任何 AEM 專案都應利用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)，它支援使用 React 或 Angular 的 SPA 專案並利用 SPA SDK。

## 天氣元件 {#the-weather-component}

天氣元件位於We.Retail Journal應用的左上角。 它顯示已定義位置的當前天氣，動態提取天氣資料。

### 使用天氣小部件 {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

在編輯器中創SPA作SPA內容時，天氣元件將作為任何其AEM他元件顯示，並帶有工具欄且可編輯。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

可以像其他元件一樣在對話中更新城AEM市。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

該更改被保留，並且元件會使用新天氣資料自動更新自己。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 氣象元件實施 {#weather-component-implementation}

氣象元件實際上基於一個公開可用的React元件，稱為 [應對開放天氣](https://www.npmjs.com/package/react-open-weather)，已調整為We.Retail Journal示例應用程式中的一個組SPA件。

以下是NPM文檔中關於React Open Weather元件使用情況的片段。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

查看自定義天氣元件的代碼( `Weather.js`)，在We.Retail Journal應用程式中：

* **北京地鐵16號線**:根據需要載入「React Open Weather」小部件。
* **北京地鐵46號線**:的 `MapTo` 函式將此React元件與相應AEM的元件關聯，以便在編輯器中SPA編輯。

* **線路22-29**:的 `EditConfig` 定義，檢查是否填充了城市，並定義值（如果為空）。

* **31-44號線**:天氣元件擴展了 `Component` 類和提供Reacte Open Weather元件的NPM使用文檔中定義的所需資料，並呈現該元件。

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

雖然後端元件必須已經存在，但前端開發人員可以利用We.Retail Journal中的React Open Weather元件，SPA只需很少編碼。

## 下一步 {#next-step}

有關開發的詳細信SPA息，請AEM參閱文章 [開SPA發AEM](/help/sites-developing/spa-architecture.md)。
