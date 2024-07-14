---
title: 單頁應用程式
description: 依照本頁瞭解單頁應用程式，即您可以建立與案頭或行動應用程式執行方式相同的應用程式。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 1%

---

# 單頁應用程式{#single-page-applications}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

[單頁應用程式](https://en.wikipedia.org/wiki/Single-page_application) (SPA)已達臨界品質，被廣泛視為使用Web技術建立順暢體驗的最有效模式。 遵循SPA模式，您可以建立與案頭或行動應用程式具有相同執行效果的應用程式，但因其以開放式Web標準為基礎，而可觸及多種裝置平台與外型規格。

一般而言，SPA的效能較傳統以頁面為基礎的網站來得好，因為它們通常只載入完整的HTML頁面&#x200B;**一次** （包括CSS、JS和支援的字型內容），然後只載入每次應用程式中發生狀態變更時所需的內容。 此狀態變更所需的專案可能會因所選技術而有所不同，但通常包含單一HTML片段，以取代現有的「檢視」，以及執行JS程式碼區塊，以連線新檢視並執行任何可能必要的使用者端範本轉譯。 此狀態變更的速度可以透過支援範本快取機制進一步改善，甚至可在使用Adobe PhoneGap時離線存取範本內容。

AEM 6.1支援透過AEM應用程式建置和管理SPA。 本文介紹SPA背後的概念，以及這些概念如何使用[AngularJS](https://angularjs.org/)將您的品牌帶到App Store和Google Play。

## AEM應用程式中的SPA {#spa-in-aem-apps}

AEM Apps中的單頁應用程式架構可提供AngularJS應用程式的高效能，同時讓作者（或其他非技術人員）透過傳統上為管理網站而保留的觸控最佳化、拖放式編輯器環境，建立及管理應用程式的內容。 已經有使用AEM建立的網站？ AEM應用程式可讓您輕鬆重複使用內容、元件、工作流程、資產和許可權。

## AngularJS應用程式模組 {#angularjs-application-module}

AEM應用程式可為您處理大部分AngularJS設定，包括組合應用程式的頂層模組。 依預設，此模組名為「AEMAngularApp」，負責產生此模組的指令碼可以在/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp找到（和覆蓋）。

應用程式初始化的部分步驟包括指定應用程式相依的AngularJS模組。 您的應用程式所使用的模組清單是由/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp中的指令碼所指定，並可由您自己的應用程式頁面元件覆蓋，以提取您應用程式所需的任何其他AngularJS模組。 例如，將以上指令碼與Geometrixx實作(位於/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)進行比較。

為了支援應用程式中不同狀態之間的導覽，angular — 應用程式 — 模組指令碼會逐一檢視您頂層應用程式頁面的所有下級頁面，以產生一組「路由」，並設定Angular$routeProvider服務上的每個路徑。 如需實際操作的範例，請檢視angular應用程式範例產生的Geometrixx Outdoors — 應用程式 — 模組指令碼： （連結需要本機執行個體） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

在挖掘產生的AEMAngularApp時，您會找到一系列指定的路由，如下所示：

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

上述範例特別說明將引數作為路徑的一部分傳遞的範例。 在此範例中，這可表示請求符合指定模式(/content/phonegap/geometrixx-outdoors/en/home/products/：id)的路徑時，該路徑應由home/products.template.html範本處理並使用「contentphonegapgeometrixxoutdoorsenhomeproducts」控制器。

當要求此路由時要載入的範本是由templateUrl屬性所指定。 此範本包含頁面中已包含之AEM元件的HTML，以及連線應用程式使用者端所需的任何AngularJS指示。 如需Geometrixx元件中AngularJS指示詞的範例，請參閱swipe-carousel的template.jsp (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)的第45行。

## 頁面控制項 {#page-controllers}

用Angular自己的話說，「控制器是JavaScript建構函式，用來擴大Angular範圍。」 （[來源](https://docs.angularjs.org/guide/controller)） AEM App中的每個頁面都會自動連線到控制器，任何指定`angular`之`frameworkType`的控制器都可以增強該控制器。 以ng-text元件為例(/libs/mobileapps/components/angular/ng-text)，包括cq：template節點，每次將這個元件新增到頁面時，都會包含這個重要屬性。

如需更複雜的控制器範例，請開啟ng-template-page controller.jsp指令碼(在/apps/geometrixx-outdoors-app/components/angular/ng-template-page)。 其中特別有趣的是執行時產生的JavaScript程式碼，其呈現方式如下：

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

在上述範例中，從`$routeParams`服務中取得引數，然後將參陣列合成儲存JSON資料的目錄結構。 以這種方式處理SKU `id`，您就可以提供單一產品範本，可呈現可能數千種不同產品的產品資料。 這是一種更可擴充的模型，需要（潛在）大型產品資料庫中每個專案的個別路由。

同時有兩個元件在運作： ng-product會使用它從上述`$http`呼叫中擷取的資料來擴大範圍。 此頁面上也有一個ng-image，這反過來也會擴大範圍，使其包含從回應擷取的值。 藉由Angular的`$http`服務，每個元件會耐心等待要求完成並履行它建立的Promise。

## 後續步驟 {#the-next-steps}

瞭解單頁應用程式後，請參閱[使用PhoneGap CLI開發應用程式](/help/mobile/phonegap-apps-pg-cli.md)。
