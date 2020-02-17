---
title: 單頁應用程式
seo-title: 單頁應用程式
description: 請依照本頁來瞭解單頁應用程式，也就是說，您可以建立執行與案頭或行動應用程式相同的應用程式。
seo-description: 請依照本頁來瞭解單頁應用程式，也就是說，您可以建立執行與案頭或行動應用程式相同的應用程式。
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 單頁應用程式{#single-page-applications}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

[單頁應用程式](https://en.wikipedia.org/wiki/Single-page_application) (SPA)已達到臨界規模，被廣泛認為是使用Web技術建立順暢體驗的最有效模式。 透過遵循SPA模式，您可以建立與案頭或行動應用程式相同的應用程式，但由於應用程式以開放Web標準為基礎，因此可觸及到多種裝置平台和外形規格。

一般而言，SPA的效能比傳統的頁面型網站更好，因為SPA通常只載入一次完整的HTML頁面 **** （包括CSS、JS和支援字型內容），然後只載入每次應用程式中狀態變更時所需的內容。 此狀態變更的必要項目可能會視所選技術而有所不同，但通常會包含單一HTML片段以取代現有的「檢視」，以及執行JS程式碼區塊以連線新檢視並執行任何可能必要的用戶端範本轉換。 支援範本快取機制，或使用Adobe phoneGap離線存取範本內容，可進一步改善此狀態變更的速度。

AEM 6.1支援透過AEM Apps建立和管理SPA。 本文將介紹SPA的概念，以及它們如何運用 [AngularJS](https://angularjs.org/) ，將您的品牌帶入App Store和Google Play。

## AEM應用程式中的SPA {#spa-in-aem-apps}

AEM Apps中的單頁應用程式架構可讓AngularJS應用程式發揮高效能，同時讓作者（或其他非技術人員）透過觸控最佳化拖放編輯器環境來建立和管理應用程式的內容，而傳統上，編輯器環境是專為管理網站而保留的。 已使用AEM建立網站？ 您會發現，使用AEM Apps可輕鬆重複使用您的內容、元件、工作流程、資產和權限。

## AngularJS應用程式模組 {#angularjs-application-module}

AEM Apps會為您處理大部分的AngularJS設定，包括將應用程式的頂層模組組合在一起。 預設情況下，此模組名為&#39;AEMAngularApp&#39;，負責生成該模組的指令碼可在/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp中找到（並覆蓋）。

應用程式初始化的一部分包括指定應用程式所依賴的AngularJS模組。 應用程式使用的模組清單是由位於/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp的指令碼所指定，並可由您自己應用程式的頁面元件覆蓋，以納入您應用程式需要的任何其他AngularJS模組。 例如，請比較上述指令碼與Geometrixx實作(位於/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)。

為支援應用程式中不同狀態之間的導覽，angular-app-module指令碼會重複您頂層應用程式頁面的所有子頁面，以產生一組「路由」，並設定Angular的$routeProvider服務上的每條路徑。 如需實際運作的範例，請參閱Geometrixx Outdoors應用程式範例產生的角度應用程式模組指令碼：（連結需要本機例項） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

深入到生成的AEMAngularApp，您將發現一系列指定如下的路由：

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

上述範例特別說明將參數傳入路徑的範例。 在此範例中，我們指出當要求符合指定模式的路徑(/content/phonegap/geometrixx-outdoors/en/home/products/:id)時，應由home/products.template.html範本處理，並使用&#39;contentphoneggeometrixxoutsenhomeproducts&#39;控制器。

templateUrl屬性指定了在請求此路由時要載入的模板。 此範本將包含AEM元件（已包含在頁面上）的HTML，以及連接應用程式用戶端所需的任何AngularJS指令。 如需Geometrixx元件中AngularJS指令的範例，請檢視swipe-carousel的template.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)的第45行。

## 頁面控制器 {#page-controllers}

在Angular自己的單字中，「控制器是用於增大角度範圍的JavaScript建構子。」 (來[源](https://docs.angularjs.org/guide/controller))AEM應用程式中的每個頁面都會自動連線至控制器，讓任何指定其中一個的控制器都可加以 `frameworkType` 擴充 `angular`。 以ng-text元件為例(/libs/mobileapps/components/angular/ng-text)，包括cq:template節點，可確保每次將此元件新增至包含此重要屬性的頁面時，都能使用此節點。

如需更複雜的控制器範例，請開啟ng-template-page controller.jsp指令碼（位於/apps/geometrixx-outdoors-app/components/angular/ng-template-page）。 特別感興趣的是執行時產生的Javascript程式碼，其呈現如下：

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

在上述範例中，您會注意到，我們正從服務中擷取參數，然後將其按摩至JSON資料儲存在的目錄結構中。 `$routeParams` 以此方式處 `id` 理sku，我們可提供單一產品範本，可針對潛在數以千計的不同產品呈現產品資料。 這是一個可擴充性大得多的模型，它要求在（可能）龐大的產品資料庫中，每個項目都有一條單獨的路由。

這裡還有兩個元件：ng-product會利用其從上述呼叫中擷取的資料來擴大范 `$http` 圍。 此頁上也有ng-image，這反過來也會增加範圍，並增加它從回應中擷取的值。 通過Angular公司的服 `$http` 務，每個元件將耐心等待，直到請求完成並實現它所創造的承諾。

## 後續步驟 {#the-next-steps}

瞭解「單頁應用程式」後，請參閱「使用PhoneGap CLI [開發應用程式」](/help/mobile/phonegap-apps-pg-cli.md)。
