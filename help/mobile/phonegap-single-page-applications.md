---
title: 單頁應用程式
seo-title: Single Page Applications
description: 按照此頁瞭解單頁應用程式，即，您可以建立與案頭或移動應用程式執行相同操作的應用程式。
seo-description: Follow this page to learn about single page applications, that is, you can create an application that performs identically to a desktop or mobile application.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 1%

---

# 單頁應用程式{#single-page-applications}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

[單頁應用程式](https://en.wikipedia.org/wiki/Single-page_application) (SPA)已達到臨界質量，被廣泛認為是利用Web技術構建無縫體驗的最有效模式。 通過遵循SPA模式，您可以建立與案頭或移動應用程式效能相同但由於其在開放Web標準中的基礎而達到多種設備平台和外形規格的應用程式。

一般來說，SPA與傳統的基於頁面的網站相比，它們的效能更高，因為它們通常載入一個完整的HTML頁 **僅一次** （包括CSS、JS和支援字型內容），然後在應用程式中每次發生狀態更改時只準確載入所需的內容。 此狀態更改所需的內容可能因所選技術集而異，但通常包括替換現有「view」的單個HTML片段，以及執行JS代碼塊以連接新視圖並執行可能需要的任何客戶端模板呈現。 通過支援模板快取機制，或者如果使用Adobe PhoneGap，甚至對模板內容的離線訪問，可以進一步提高這種狀態改變的速度。

AEM6.1支援通過應用程式SPA的構AEM建和管理。 本文將介紹Web服務背後的概念以及SPA它們如何利用 [角JS](https://angularjs.org/) 把你的品牌帶到App Store和Google Play。

## 在應SPA用AEM中 {#spa-in-aem-apps}

應用程式中的單頁應用程式框架支援AngularJS應用程式的高效能，同時授權作者（或其他非技術人員）通過傳統上為管理網站而保留的觸控優化拖放編輯器環境建立和管理應用程式的內容。 已經建好了AEM? 您會發現，使用應用程式可以輕鬆地重新使用您的內容、元件、工作流、資產AEM和權限。

## AngularJS應用程式模組 {#angularjs-application-module}

應AEM用為您處理大部分AngularJS配置，包括將應用程式的頂級模組組合起來。 預設情況下，此模組名為「AEMAngularApp」，負責生成該模組的指令碼可在/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp中找到（並重疊）。

應用程式初始化的一部分涉及指定應用程式所依賴的AngularJS模組。 應用程式使用的模組清單由位於/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp的指令碼指定，並且可以由您自己的應用程式的頁面元件覆蓋，以拉入應用程式所需的任何附加AngularJS模組。 例如，將上述指令碼與Geometrixx實現(位於/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)進行比較。

為支援在應用中的不同狀態之間進行導航，angular-app-module指令碼會迭代遍歷頂級應用頁面的所有子體頁面，以生成一組「路由」，並配置Angular的$routeProvider服務上的每個路徑。 有關此操作在實踐中的效果的示例，請看angular應用示例生成的Geometrixx Outdoors應用模組指令碼：（連結需要本地實例） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

深入到生成的AEMAngularApp後，您將發現一系列指定如下的路由：

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

上述示例特別說明了將參數作為路徑的一部分傳遞的示例。 在本示例中，我們指示當請求滿足指定模式(/content/phonegap/geometrixx-outdoors/en/home/products/:id)的路徑時，應使用home/products.template.html模板並使用「contentphonegapegeotrixxoutdoosenhomeproducts」控制器來處理該路徑。

請求此路由時要載入的模板由templateUrl屬性指定。 此模板將包含來自頁AEM面中包含的元件的HTML，以及連接應用程式客戶端所需的任何AngularJS指令。 有關Geometrixx元件中的AngularJS指令的示例，請查看輕掃 — 旋轉盤的template.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)的第45行。

## 頁面控制器 {#page-controllers}

用Angular自己的話來說，「控制器是用於擴展Angular範圍的JavaScript建構子。」 ([源](https://docs.angularjs.org/guide/controller))應用程式中的每AEM個頁面都會自動連接到控制器，該控制器可由指定 `frameworkType` 共 `angular`。 以ng-text元件為例(/libs/mobileapps/components/angular/ng-text)，包括cq:template節點，該節點確保每次將此元件添加到頁面時都包含此重要屬性。

對於更複雜的控制器示例，請開啟ng-template-page controller.jsp指令碼(位於/apps/geometrixx-outdoors-app/components/angular/ng-template-page)。 特別感興趣的是它在執行時生成的javascript代碼，該代碼呈現如下：

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

在上例中，您將注意到，我們從 `$routeParams` 服務，然後將其按摩到JSON資料所儲存的目錄結構中。 通過處理SKU `id` 通過這種方式，我們能夠提供單個產品模板，該模板可以呈現可能成千上萬個不同產品的產品資料。 這是一個可擴展得多的模型，它要求在（可能的）大規模產品資料庫中的每個項目都有單獨的路由。

這裡還有兩個組成部分：ng-product用它從上面提取的資料擴大範圍 `$http` 呼叫。 此頁上還有ng-image，這反過來又增加了範圍，使其具有從響應中檢索到的值。 根據Angular `$http` 服務，每個元件將耐心等待，直到請求完成並履行它所創造的承諾。

## 後續步驟 {#the-next-steps}

瞭解單頁應用程式後，請參閱 [使用PhoneGap CLI開發應用](/help/mobile/phonegap-apps-pg-cli.md)。
