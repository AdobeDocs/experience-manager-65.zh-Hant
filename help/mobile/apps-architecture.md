---
title: 行動應用程式的頁面範本
seo-title: 行動應用程式的頁面範本
description: 請依照本頁進一步瞭解頁面範本。 您為應用程式建立的頁面元件是以/libs/mobileapps/components/angular/ng-page元件為基礎。
seo-description: 請依照本頁進一步瞭解頁面範本。 您為應用程式建立的頁面元件是以/libs/mobileapps/components/angular/ng-page元件為基礎。
uuid: c53901c9-5974-4c6b-ac61-1c094a93c9d6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: cfc7ad16-965e-4075-bc4d-5630abeaba55
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 行動應用程式的頁面範本 {#page-templates-for-mobile-apps}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

## 行動應用程式的頁面範本 {#page-templates-for-mobile-apps-1}

您為應用程式建立的頁面元件是以/libs/mobileapps/components/angular/ng-page元件(在本機伺服[器上的CRXDE Lite中開啟](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page))為基礎。 此元件包含以下JSP指令碼，供元件繼承或覆蓋：

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

使用屬性判斷應用程式的名 `applicationName` 稱，並透過pageContext公開它。

包含head.jsp和body.jsp。

### head.jsp {#head-jsp}

寫出應 `<head>` 用程式頁面的元素。

如果您想要覆寫應用程式的檢視區中繼屬性，這是您覆寫的檔案。

依照最佳實務，應用程式會將用戶端程式庫的css部分包含在標題中，而JS會包含在關閉&lt;元 `body>` 素中。

### body.jsp {#body-jsp}

根據是否檢測到wcmMode(!= WCMMode.DISABLED)，以判斷頁面是開啟以進行編寫，還是開啟為發佈頁面。

**作者模式**

在作者模式中，每個個別頁面會個別呈現。 Angular不處理頁面間的路由選擇，ng-view也不用於載入包含頁面元件的部分模板。 而是透過標籤將頁面範本(template.jsp)的內容包含在伺服器 `cq:include` 端。

此策略可讓作者具備功能（例如在段落系統中新增和編輯元件、Sidekick、設計模式等）函式而不進行修改。 依賴用戶端轉譯的頁面（例如應用程式的頁面）在AEM作者模式中無法正常執行。

請注意，template.jsp include會包裝在包含指 `div` 令的元素中 `ng-controller` 。 這種結構使得DOM內容與控制器相連結。 因此，雖然在用戶端呈現的頁面會失敗，但個別元件仍能正常運作（請參閱下方「元件」一節）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**發佈模式**

在發佈模式中（例如使用「內容同步」匯出應用程式時），所有頁面都會變成單一頁面應用程式(SPA)。 (若要瞭解SPA，請使用Angular教學課程，具體 [為https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07))。

SPA中只有一個HTML頁面(包含元素的頁 `<html>` 面)。 此頁面稱為「版面範本」。 在Angular術語中，它是&quot;。..我們應用程式中所有檢視的通用範本。」 請將此頁面視為「頂層應用程式頁面」。 依慣例，頂層應用程式頁面是您 `cq:Page` 應用程式中最靠近根目錄的節點（而非重新導向）。

由於應用程式的實際URI在發佈模式中不會變更，因此此頁面對外部資產的參考必須使用相對路徑。 因此，提供了一種特殊影像元件，其在渲染用於導出的影像時考慮了該頂層頁面。

作為SPA，此版面範本頁面只會產生具有ng-view指令的div元素。

```xml
 <div ng-view ng-class="transition"></div>
```

Angular route服務使用此元素來顯示應用程式中每個頁面的內容，包括目前頁面（包含在template.jsp中）的可授權內容。

body.jsp檔案包含header.jsp和footer.jsp，兩者皆為空白。 如果您想要在每個頁面上提供靜態內容，可以在應用程式中覆寫這些指令碼。

最後，Javascript clientlibs會包含在&lt;body>元素的底部，包括兩個在伺服器上產生的特殊JS檔案： *&lt;page name>*.angular-app-module.js和 *&lt;page name>*.angular-app-controllers.js。

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

此指令碼定義應用程式的Angular模組。 此指令碼的輸出連結到模板元件的其餘部分通過ng-page.jsp中的元素生成的標籤 `html` ，該元素包含以下屬性：

```xml
ng-app="<c:out value='${applicationName}'/>"
```

此屬性向Angular指示此DOM元素的內容應連結到以下模組。 此模組會將檢視（在AEM中，這些檢視會是cq:Page資源）與對應的控制器連結。

此模組還定義了名為的頂級控制器， `AppController` 該控制器將變 `wcmMode` 量暴露到該範圍，並配置從中獲取內容同步更新負載的URI。

最後，此模組會重複每個子頁面（包括本身），並呈現每個頁面的路由片段內容（透過angul-route-fragment.js選擇器與延伸功能），包括它作為Angular的\$routeProvider的組態項目。 換言之，\$routeProvider會告訴應用程式，當要求指定路徑時，要呈現哪些內容。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

此指令碼會產生必須採用下列格式的JavaScript片段：

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

此代碼向$routeProvider(定義於angular-app-module.js.jsp)表示「/&lt;路徑>」將由位於的資源處理 `templateUrl`，並由 `controller` （下一步將會看到）連線。

如有必要，您可以覆寫此指令碼，以處理更複雜的路徑，包括含變數的路徑。 此範例可在與AEM一起安裝的/apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp指令碼中看到：

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

在Angular中，控制器將變數連線到\$scope中，將其暴露在視圖中。 angular-app-controllers.js.jsp指令碼遵循angular-app-module.js.jsp所示的模式，其會重複每個子系頁面（包括自身），並輸出每個頁面所定義的控制器片段(透過controller.js.jsp)。 它定義的模組被調用， `cqAppControllers` 並且必須列為頂層應用程式模組的從屬關係，以便頁面控制器可用。

### controller.js.jsp {#controller-js-jsp}

controller.js.jsp指令碼會為每個頁面產生控制器片段。 此控制器片段採用下列形式：

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

請注意，此 `data` 變數會指派Angular方法傳回的 `$http.get` 承諾。 如有需要，此頁面中包含的每個元件都可讓某些。json內容可供使用（透過其angular.json.jsp指令碼），並在解析時對此請求的內容採取行動。 在行動裝置上，由於只需存取檔案系統，所以要求的速度非常快。

為使元件以這種方式成為控制器的一部分，它應擴展/libs/mobileapps/components/angular/ng-component元件並包括該屬 `frameworkType: angular` 性。

### template.jsp {#template-jsp}

petmale.jsp首先在body.jsp節中介紹，它只包含頁面的parsys。 在發佈模式中，此內容會直接參考（位於&lt;page-path>.template.html），並透過在\$routeProvider上設定的templateUrl載入SPA。

此指令碼中的parsys可配置為接受任何類型的元件。 但是，在處理為傳統網站（而非SPA）建立的元件時，必須格外小心。 例如，基礎影像元件僅能在頂層應用程式頁面上正常運作，因為它不是設計來參考應用程式內的資產。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

此指令碼只會輸出頂層Angular應用程式模組的Angular相依性。 angular-app-module.js.jsp會參考它。

### header.jsp {#header-jsp}

將靜態內容置於應用程式頂端的指令碼。 此內容會包含在頂層頁面中，不在ng-view的範圍內。

### footer.jsp {#footer-jsp}

將靜態內容置於應用程式底部的指令碼。 此內容會包含在頂層頁面中，不在ng-view的範圍內。

### js_clientlibs.jsp {#js-clientlibs-jsp}

覆寫此指令碼以包含您的JavaScript用戶端。

### css_clientlibs.jsp {#css-clientlibs-jsp}

覆寫此指令碼以包含您的CSSclientlib。

## 應用程式元件 {#app-components}

應用程式元件不僅必須適用於AEM例項（發佈或作者），而且當應用程式內容透過「內容同步」匯出至檔案系統時也必須適用。 因此，元件必須包含下列特性：

* PhoneGap應用程式中的所有資產、範本和指令碼必須相對參考。
* 如果AEM例項以作者或發佈模式運作，則連結的處理方式會有所不同。

### 相對資產 {#relative-assets}

PhoneGap應用程式中任何指定資產的URI不僅會依平台而有所不同，而且在應用程式的每次安裝中都是唯一的。 例如，請注意iOS模擬器中執行之應用程式的下列URI:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

請注意路徑中的GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;。

身為PhoneGap開發人員，您所關心的內容位於www目錄下。 若要存取應用程式資產，請使用相對路徑。

若要複合此問題，您的PhoneGap應用程式會使用單頁應用程式(SPA)模式，讓基本URI（排除雜湊）永不變更。 因此，您參考的每個資產、範本或指令 **碼都必須相對於頂層頁面。** 頂層頁面通過和初始化「角度」路由和控制 `*<name>*.angular-app-module.js` 器 `*<name>*.angular-app-controllers.js`。 此頁面應是距資料庫根目錄最近的頁面， *does *extend a sling:redirect.

有幾種輔助方法可用來處理相對路徑：

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

若要查看其使用範例，請開啟位於/libs/mobileapps/components/angular的mobileapps來源。

### 連結 {#links}

連結必須使用 `ng-click="go('/path')"` 函式來支援所有WCM模式。 此函式取決於範圍變數的值，以正確判斷連結動作：

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

當我 `$scope.wcmMode == true` 們以一般方式處理每個導覽事件時，結果會是URL的路徑和／或頁面部分變更。

或者，如 `$scope.wcmMode == false`果每個導覽事件導致URL的雜湊部分變更，而雜湊部分由Angular的ngRoute模組內部解析。

### 元件指令碼詳細資訊 {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

當偵測到「編輯」模式時，此指令碼會顯示元件內容或適當的預留位置。

#### template.jsp {#template-jsp-1}

template.jsp指令碼將呈現元件的標籤。 如果相關元件是由從AEM擷取的JSON資料所驅動(例如&#39;ng-text&#39;:/libs/mobileapps/components/angular/ng-text/template.jsp)，則此指令碼將負責將標籤與頁面控制器範圍所公開的資料連線。

不過，效能需求有時會要求不執行用戶端範本（亦即資料系結）。 在這種情況下，只需在伺服器端轉換元件的標籤，它就會包含在頁面範本內容中。

#### opperise.jsp {#overhead-jsp}

在由JSON資料驅動的元件中（例如&#39;ng-text&#39;）:/libs/mobileapps/components/angular/ng-text)，開銷。jsp可用於從template.jsp中刪除所有Java代碼。 然後從template.jsp參考此變數，而它在請求中公開的任何變數都可供使用。 此策略鼓勵將邏輯與表現分離，並限制從現有元件衍生新元件時必須複製和貼上的程式碼量。

#### controller.js.jsp {#controller-js-jsp-1}

如「AEM頁面範本」中所述，每個元件都可輸出JavaScript片段，以使用承諾所公開的JSON `data` 內容。 遵循Angular約定，控制器僅應用於為範圍指定變數。

#### angular.json.jsp {#angular-json-jsp}

此指令碼會包含在頁面寬度的「&lt;page-name>.angular.json」檔案中，該檔案會針對每個延伸ng-page的頁面匯出。 在此檔案中，元件開發人員可公開元件所需的任何JSON結構。 在&#39;ng-text&#39;範例中，此結構僅包含元件的文字內容，以及指示元件是否包含rich text的標幟。

Geometrixx outdoors應用程式產品元件是更複雜的範例(/apps/geometrixx-outdoors-app/components/angular/ng-product):

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## CLI資產下載內容 {#contents-of-the-cli-assets-download}

從Apps主控台下載CLI資產以針對特定平台最佳化這些資產，然後使用PhoneGap命令列整合(CLI)API建立應用程式。 保存到本地檔案系統的ZIP檔案的內容具有以下結構：

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

這是隱藏目錄，根據您目前的作業系統設定，您可能看不到它。 如果您打算修改包含的應用程式勾點，您應設定您的作業系統，以顯示此目錄。

#### .cordova/hooks/ {#cordova-hooks}

此目錄包含 [CLI掛接](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)。 掛接目錄中的資料夾包含在構建過程中精確點處執行的node.js指令碼。

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add目錄包含該 `copy_AMS_Conifg.js` 檔案。 此指令碼會複製設定檔，以支援Adobe Mobile services分析的集合。

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

After-prepare目錄包含該 `copy_resource_files.js` 檔案。 此指令碼會將許多圖示和啟動顯示畫面影像複製到特定平台的位置。

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add目錄包含該 `install_plugins.js` 檔案。 此指令碼會重複Cordova增效模組識別碼清單，並安裝它偵測到的目前尚未提供的識別碼。

此策略不需要您在每次執行Maven命令時，將外掛程式整合併安裝 `content-package:install` 至AEM。 將檔案簽入SCM系統的替代策略需要重複打包和安裝活動。

#### .cordova/hooks/Other Hooks {#cordova-hooks-other-hooks}

視需要加入其他勾點。 有下列可用的勾點（如Phonegap範例hello world app所提供）:

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_prepare
* before_prepare
* after_run
* before_run

#### platforms/ {#platforms}

在您對項目執行命令之前，此目 `phonegap run <platform>` 錄是空的。 目前， `<platform>` 可以是 `ios` 或 `android`。

建立特定平台的應用程式後，就會建立對應的目錄，並包含特定平台的應用程式碼。

#### plugins/ {#plugins}

外掛程式目錄是由您執行命令後，檔案中列 `.cordova/hooks/before_platform_add/install_plugins.js` 出的每個外掛程式填 `phonegap run <platform>` 入。 目錄最初是空的。

#### www/ {#www}

www目錄包含實作應用程式外觀和行為的所有網頁內容（HTML、JS和CSS檔案）。 除下述例外，此內容源自AEM，並透過「內容同步」匯出至其靜態表單。

#### www/config.xml {#www-config-xml}

PhoneGap [檔案將此](https://docs.phonegap.com) 檔案稱為「全域設定檔」。 config.xml包含許多應用程式屬性，例如應用程式名稱、應用程式「偏好設定」（例如iOS網頁檢視是否允許捲動），以及僅由PhoneGap組建版本使用的外掛程式相依 *性* 。

config.xml檔案是AEM中的靜態檔案，會透過「內容同步」以「現況」匯出。

#### www/index.html {#www-index-html}

index.html檔案會重新導向至應用程式的起始頁面。

config.xml檔案包含元 `content` 素：

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

在 [PhoneGap檔案中](https://docs.phonegap.com)，此元素說明為「選用&lt;content>元素會在頂層Web資產目錄中定義應用程式的開始頁面。 預設值為index.html，它通常會出現在專案的頂層www目錄中。」

如果index.html檔案不存在，PhoneGap建置會失敗。 因此，會包含此檔案。

#### www/res {#www-res}

res目錄包含啟動顯示畫面影像和圖示。 在建 `copy_resource_files.js` 立階段，指令碼會將檔案複製到其特定平台 `after_prepare` 的位置。

#### www/etc {#www-etc}

根據慣例，在AEM中， /etc節點包含靜態clientlib內容。 etc目錄包含Topcoat、AngularJS和Geometrixx-clientlibsall程式庫。

#### www/apps {#www-apps}

應用程式目錄包含與啟動顯示頁面相關的程式碼。 AEM應用程式啟動顯示頁面的獨特特點是，它會在沒有使用者互動的情況下初始化應用程式。 因此，應用程式的clientlib內容（包括CSS和JS）最小，才能發揮最大效能。

#### www/content {#www-content}

內容目錄包含應用程式的其餘網頁內容。 內容可包含（但不限於）下列檔案：

* HTML頁面內容，直接在AEM中編寫
* 與AEM元件相關聯的影像資產
* 伺服器端指令碼產生的JavaScript內容
* 描述頁面或元件內容的JSON檔案

#### www/package.json {#www-package-json}

package.json檔案是資訊清單檔案，會列出完整內容同步 **下載** 所包含的檔案。 此檔案也包含產生內容同步裝載的時間戳記(`lastModified`)。 從AEM要求部分更新應用程式時，會使用此屬性。

#### www/package-update.json {#www-package-update-json}

如果此裝載是整個應用程式的下載，此資訊清單會包含檔案的確切清單 `package.json`。

但是，如果此裝載是部分更新， `package-update.json` 則僅包含包含在此特定裝載中的檔案。
