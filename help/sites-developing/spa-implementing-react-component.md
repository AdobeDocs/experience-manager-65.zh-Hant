---
title: 針對 SPA 實作 React元件
description: 本文會介紹如何調整簡單的現有React元件，以搭配Adobe Experience Manager (AEM) SPA Editor使用。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 9%

---


# 針對 SPA 實作 React元件{#implementing-a-react-component-for-spa}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能使用SPA架構建立網站，而作者則想在Adobe Experience Manager (AEM)中為使用SPA架構建立的網站順暢地編輯內容。

SPA製作功能提供全方位的解決方案，可支援AEM中的SPA。 本文將以範例說明如何調整簡單的現有React元件，以搭配AEM SPA Editor使用。

{{ue-over-spa}}

## 簡介 {#introduction}

由於AEM需要簡易且輕量的合約，且在SPA和SPA Editor之間建立，因此在AEM中運用現有的JavaScript應用程式並將其調整為可與SPA搭配使用，是一件簡單明瞭的事。

本文說明We.Retail Journal範例SPA上的天氣元件範例。

在閱讀本文之前，您應該先熟悉AEM[&#128279;](/help/sites-developing/spa-getting-started-react.md)的SPA應用程式的結構。

>[!CAUTION]
>本檔案僅將[We.Retail Journal應用程式](https://github.com/adobe/aem-sample-we-retail-journal)用於示範用途。 請勿用於任何專案工作。
>
>任何 AEM 專案都應使用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支援使用 React 或 Angular 的 SPA 專案並使用 SPA SDK。

## 天氣元件 {#the-weather-component}

氣象元件可在We.Retail Journal應用程式左上角找到。 它會顯示定義位置的目前氣象，以動態方式提取天氣資料。

### 使用天氣Widget {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

在SPA編輯器中編寫SPA的內容時，天氣元件會像任何其他AEM元件一樣顯示、包含工具列且可以編輯。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

城市可在對話方塊中更新，就像任何其他AEM元件一樣。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

此變更會持續存在，而元件會自動以新的天氣資料更新。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 天氣元件實施 {#weather-component-implementation}

天氣元件是以公開可用的React元件為基礎，稱為[React Open Weather](https://www.npmjs.com/package/react-open-weather)。 它已調整為可在We.Retail Journal範例SPA應用程式中當做元件使用。

以下是React Open Weather元件用途的NPM檔案片段。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

檢閱We.Retail Journal應用程式中自訂天氣元件( `Weather.js`)的程式碼：

* **第16**&#x200B;行： React Open Weather Widget已視需要載入。
* **第46**&#x200B;行： `MapTo`函式將此React元件與對應的AEM元件建立關聯，以便在SPA編輯器中編輯它。

* **行22-29**：已定義`EditConfig`，正在檢查是否已填入城市，如果空白，則定義值。

* **行31-44**： Weather元件會擴充`Component`類別，並提供React Open Weather元件之NPM使用檔案中所定義的必要資料，以及呈現元件。

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

雖然後端元件必須已存在，但前端開發人員可以在We.Retail Journal SPA中使用React Open Weather元件，且幾乎沒有程式碼。

## 下一步 {#next-step}

如需有關為AEM開發SPA的詳細資訊，請參閱文章[為AEM開發SPA](/help/sites-developing/spa-architecture.md)。
