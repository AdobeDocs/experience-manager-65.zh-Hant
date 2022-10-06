---
title: 單頁應用程式
seo-title: Single Page Applications
description: 請依照本頁了解單頁應用程式，即您可以建立執行與案頭或行動應用程式相同的應用程式。
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
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

[單頁應用程式](https://en.wikipedia.org/wiki/Single-page_application) (SPA)已達到臨界量，被廣泛視為使用網頁技術建立順暢體驗的最有效模式。 通過遵循SPA模式，您可以建立一個應用程式，該應用程式的效能與案頭或移動應用程式相同，但由於其在開放Web標準中的基礎，它可以到達多個設備平台和外形因素。

一般而言，SPA的效能會比傳統的頁面型網站來得高，因為這些網站通常會載入完整的HTML頁面 **僅一次** （包括CSS、JS和支援的字型內容），然後只載入應用程式中每次狀態變更時的必要項目。 此狀態變更的必要條件可能會根據所選技術集而有所不同，但通常包含單一HTML片段以取代現有的「檢視」，以及執行JS程式碼區塊以匯整新檢視並執行任何可能必要的用戶端範本轉譯。 支援範本快取機制，或如果使用Adobe PhoneGap，甚至離線存取範本內容，可進一步改善此狀態變更的速度。

AEM 6.1支援透過AEM應用程式建置和管理SPA。 本文將介紹SPA背後的概念及其運用方式 [AngularJS](https://angularjs.org/) 將您的品牌帶入App Store和Google Play。

## AEM應用程式中的SPA {#spa-in-aem-apps}

AEM應用程式中的單頁應用程式架構可支援AngularJS應用程式的高效能，同時讓作者（或其他非技術人員）能透過觸控最佳化的拖放編輯器環境來建立和管理應用程式的內容，此環境傳統上是專為管理網站而保留。 已使用AEM建立網站？ 您會發現，使用AEM應用程式可輕鬆重複使用您的內容、元件、工作流程、資產和權限。

## AngularJS應用程式模組 {#angularjs-application-module}

AEM應用程式可為您處理大部分的AngularJS設定，包括將應用程式的頂層模組整合在一起。 預設情況下，此模組名為&#39;AEMAngularApp&#39;，負責生成該模組的指令碼可在/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp找到（並覆蓋）。

應用程式初始化的一部分包括指定應用程式所仰賴的AngularJS模組。 應用程式使用的模組清單是由/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp上的指令碼指定，並可由您自己的應用程式的頁面元件覆蓋，以提取應用程式需要的任何其他AngularJS模組。 例如，將上述指令碼與Geometrixx實作(位於/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)作比較。

為了支援在應用程式中的不同狀態之間進行導覽，angular應用程式模組指令碼會反覆顯示頂層應用程式頁面的所有子系頁面，以產生一組「路由」，並設定Angular的$routeProvider服務上的每個路徑。 如需實務外觀的範例，請參閱angular應用程式範例產生的Geometrixx Outdoors應用程式模組指令碼：（連結需要本機執行個體） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

深入到生成的AEMAngularApp，您會發現一系列指定路由，如下所示：

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

上述範例特別說明將參數傳遞為路徑一部分的範例。 在此範例中，我們指出當請求符合指定模式(/content/phonegap/geometrixx-outdoors/en/home/products/:id)的路徑時，應由home/products.template.html範本處理，並使用「contentphonegapegeometrixxoutdoorssenhomeproducts」控制器。

當請求此路由時要載入的模板由templateUrl屬性指定。 此範本將包含頁面上已包含之AEM元件的HTML，以及連接應用程式用戶端所需的任何AngularJS指令。 以Geometrixx元件中的AngularJS指令為例，請查看swipe-carousel的template.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)的第45行。

## 頁面控制器 {#page-controllers}

在Angular自己的單詞中，「控制器是JavaScript建構函式，用於擴大Angular範圍。」 ([來源](https://docs.angularjs.org/guide/controller))AEM應用程式中的每個頁面都會自動連線至控制器，該控制器可供指定 `frameworkType` of `angular`. 以ng-text元件為例(/libs/mobileapps/components/angular/ng-text)，包括cq:template節點，可確保每次將此元件新增至頁面時，其中都包含這個重要屬性。

如需更複雜的控制器範例，請開啟ng-template-page controller.jsp指令碼(位於/apps/geometrixx-outdoors-app/components/angular/ng-template-page)。 特別感興趣的是執行時產生的javascript程式碼，其轉譯如下：

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

在上例中，您會注意到，我們採用 `$routeParams` 服務，然後將其按摩至儲存JSON資料的目錄結構中。 通過處理SKU `id` 透過這種方式，我們可以提供單一產品範本，為可能數千種不同的產品轉譯產品資料。 這是一個可擴充性更強的模型，它要求（可能）大規模產品資料庫中的每個項目都有單獨的路由。

此處還有兩個元件：ng-product會利用其從上述網站擷取的資料來擴大範圍 `$http` 呼叫。 此頁面上也有ng-image，這反過來也會以它從回應中擷取的值來擴大範圍。 根據Angular `$http` 服務中，每個元件會耐心等候，直到請求完成，並履行其建立的承諾。

## 後續步驟 {#the-next-steps}

了解單頁應用程式後，請參閱 [使用PhoneGap CLI開發應用程式](/help/mobile/phonegap-apps-pg-cli.md).
