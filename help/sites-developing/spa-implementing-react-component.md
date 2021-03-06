---
title: 針對 SPA 實作 React元件
seo-title: 針對 SPA 實作 React元件
description: 本文舉例說明如何調整簡單、現有的React元件，以便搭配AEM SPA編輯器使用。
seo-description: 本文舉例說明如何調整簡單、現有的React元件，以便搭配AEM SPA編輯器使用。
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 7%

---

# 針對 SPA 實作 React元件{#implementing-a-react-component-for-spa}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能使用SPA架構建立網站，而作者則想在AEM中為使用SPA架構建立的網站順暢地編輯內容。

SPA製作功能提供全方位的解決方案，可支援AEM中的SPA。 本文舉例說明如何調整簡單、現有的React元件，以便搭配AEM SPA編輯器使用。

>[!NOTE]
>
>若專案需要SPA架構的用戶端轉譯(例如React或Angular),SPA Editor是建議的解決方案。

## 簡介 {#introduction}

由於AEM需要並在SPA與SPA編輯器之間建立簡單輕量的合約，採用現有的Javascript應用程式並加以調整，以便與AEM中的SPA搭配使用，是相當簡單的作法。

本文說明We.Retail Journal範例SPA上天氣元件的範例。

閱讀本文之前，您應先熟悉SPA應用程式的[結構，以適用於AEM](/help/sites-developing/spa-getting-started-react.md)。

>[!CAUTION]
>本檔案僅將[We.Retail Journal應用程式](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)用於示範用途。 它不應用於任何項目工作。
>
>任何AEM專案都應運用[AEM專案原型](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/developing/archetype/overview.html)，這可支援使用React或Angular的SPA專案，並運用SPA SDK。

## 天氣元件{#the-weather-component}

We.Retail Journal應用程式左上角有天氣元件。 它會顯示已定義位置的目前天氣，以動態提取天氣資料。

### 使用天氣小工具{#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

在SPA編輯器中編寫SPA內容時，天氣元件會以任何其他AEM元件的形式顯示，並帶有完整的工具列，且是可編輯的。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

您可以像其他AEM元件一樣，在對話方塊中更新城市。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

變更會持續存在，而元件會隨著新氣象資料自動更新。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 氣象元件實施{#weather-component-implementation}

天氣元件實際上是以公開可用的React元件（稱為[React Open Weather](https://www.npmjs.com/package/react-open-weather)）為基礎，這些元件已調整為在We.Retail Journal示例SPA應用程式中作為元件使用。

以下是NPM檔案中React Open Weather元件使用情形的片段。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

檢閱We.Retail Journal應用程式中自訂天氣元件(`Weather.js`)的代碼：

* **第16行**:React Open Weather Widget會視需要載入。
* **第46行**:函 `MapTo` 數將此React元件與對應的AEM元件相關，以便在SPA編輯器中編輯它。

* **第22-29行**:已定 `EditConfig` 義，檢查城市是否已填入，並定義值（如果空）。

* **第31-44行**:Weather元件可擴充類 `Component` 別，並提供React Open Weather元件的NPM使用說明檔案中定義的必要資料，並轉譯元件。

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

雖然後端元件必須已存在，但前端開發人員可以利用We.Retail Journal SPA中的React Open Weather元件，只需很少的編碼。

## 下一步 {#next-step}

如需開發SPA for AEM的詳細資訊，請參閱[開發SPA for AEM](/help/sites-developing/spa-architecture.md)一文。
