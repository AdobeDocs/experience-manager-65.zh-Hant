---
title: 應用剖析
seo-title: The Anatomy of an App
description: 此頁提供您為應用程式建立的頁面元件的說明，這些元件基於/libs/mobileapps/components/angular/ng-page元件(在本地伺服器上CRXDE Lite)。
seo-description: This page provides description of the page components that you create for your app are based on the /libs/mobileapps/components/angular/ng-page component (CRXDE Lite on a local server).
uuid: 4c1a74c1-85af-4a79-b723-e9fbfc661d35
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 55667e62-a61b-4794-b292-8d54929c41ac
exl-id: ab4f1c61-be83-420e-a339-02cf1f33efed
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '2691'
ht-degree: 0%

---

# 應用剖析{#the-anatomy-of-an-app}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

## 移動應用的頁面模板 {#page-templates-for-mobile-apps}

您為應用程式建立的頁面元件基於/libs/mobileapps/components/angular/ng-page元件([在本地伺服器上CRXDE Lite開啟](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page))。 此元件包含以下JSP指令碼，您的元件繼承或覆蓋這些指令碼：

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

使用 `applicationName` 屬性，並通過pageContext公開它。

包括head.jsp和body.jsp。

### head.jsp {#head-jsp}

寫出 `<head>` 應用頁面的元素。

如果要覆蓋應用的視區元屬性，則此檔案是您覆蓋的檔案。

按照最佳做法，應用程式將客戶端庫的css部分包含在頭中，而JS則包含在結尾&lt; `body>` 的子菜單。

### body.jsp {#body-jsp}

根據是否檢測到wcmMode(!),Angular頁的正文將呈現不同= WCMMode.DISABLED)，以確定該頁面是為創作開啟的，還是作為已發佈頁面開啟的。

**作者模式**

在作者模式下，每個單獨的頁面都單獨呈現。 Angular不處理頁面間的路由，也不使用ng-view來載入包含頁面元件的部分模板。 相反，頁面模板(template.jsp)的內容通過 `cq:include` 標籤。

此策略使作者能夠實現功能（如在段落系統中添加和編輯元件、Sidekick、設計模式等） 函式。 依賴客戶端呈現的頁面在作者模式下表現不AEM佳。

請注意，template.jsp包含在 `div` 包含 `ng-controller` 指令。 此結構允許將DOM內容與控制器連結。 因此，儘管在客戶端上呈現自己的頁面會失敗，但執行此操作的單個元件仍能正常工作（請參閱下面「元件」部分）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**發佈模式**

在發佈模式（如使用內容同步導出應用程式時）中，所有頁面都變成一個頁面應用(SPA)。 (要瞭解有SPA關資訊，請使用Angular教程，具體 [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07)。)

在(包含以下項的頁SPA面)中只有一個HTML頁 `<html>` 元素)。 此頁稱為「佈局模板」。 在Angular術語中，是&quot;。..適用於應用程式中所有視圖的模板。」 將此頁面視為「頂級應用頁面」。 按慣例，頂級應用程式頁面是 `cq:Page` 最靠近根節點（且不是重定向）的應用程式節點。

由於應用的實際URI在發佈模式下不會更改，因此此頁中對外部資產的引用必須使用相對路徑。 因此，提供了一種特殊影像元件，其在呈現用於導出的影像時考慮到該頂級頁面。

作為SPA一種，此佈局模板頁只生成具有ng-view指令的div元素。

```xml
 <div ng-view ng-class="transition"></div>
```

angular路由服務使用此元素來顯示應用程式中每個頁面的內容，包括當前頁面（包含在template.jsp中）的可授權內容。

body.jsp檔案包含header.jsp和footer.jsp，兩者為空。 如果要在每個頁面上提供靜態內容，可以在應用中覆蓋這些指令碼。

最後，Javascript客戶端包含在 &lt;body> 元素，包括伺服器上生成的兩個特殊JS檔案： *&lt;page name=&quot;&quot;>*.angular-app-module.js和 *&lt;page name=&quot;&quot;>*.angular-app-controllers.js。

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

此指令碼定義應用程式的Angular模組。 此指令碼的輸出連結到模板元件的其餘部分通過 `html` ng-page.jsp中的元素，該元素包含以下屬性：

```xml
ng-app="<c:out value='${applicationName}'/>"
```

此屬性指示Angular此DOM元素的內容應連結到以下模組。 此模組將視圖(在AEM這些視圖中為cq:Page資源)與相應的控制器連結。

此模組還定義了名為 `AppController` 這暴露了 `wcmMode` 變數到作用域，並配置從中獲取內容同步更新負載的URI。

最後，此模組將迭代到每個子體頁面（包括其自身），並呈現每個頁面的路由碎片(通過angular-route-fragment.js選擇器和擴展)的內容，包括它作為Angular$routeProvider的配置條目。 換句話說，$routeProvider會告訴應用在請求給定路徑時要呈現的內容。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

此指令碼生成必須採用以下形式的JavaScript片段：

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

此代碼向$routeProvider(在angular-app-module.js.jsp中定義)表示「/&lt;path>「將由位於的資源處理 `templateUrl`，並通過 `controller` （下一節我們將討論）。

如有必要，可以覆蓋此指令碼以處理更複雜的路徑，包括那些具有變數的路徑。 在/apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp指令碼中，可以看到以下示例AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

在Angular中，控制器將$scope中的變數連接起來，使其暴露在視圖中。 angular-app-controllers.js.jsp指令碼遵循angular-app-module.js.jsp所示的模式，它迭代通過每個子體頁面（包括其自身）並輸出每個頁面定義的控制器片段(通過controller.js.jsp)。 它定義的模組稱為 `cqAppControllers` 並且必須作為頂級應用模組的依賴關係列出，以便頁面控制器可用。

### controller.js.jsp {#controller-js-jsp}

controller.js.jsp指令碼為每個頁生成控制器片段。 此控制器片段採用以下形式：

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

請注意 `data` 變數已分配由Angular返回的承諾 `$http.get` 的雙曲餘切值。 如果需要，此頁中包含的每個元件都可以使某些.json內容可用(通過其angular.json.jsp指令碼)，並在解析此請求時對其內容執行操作。 移動設備上的請求非常快，因為它只是訪問檔案系統。

為使元件以這種方式成為控制器的一部分，它應擴展/libs/mobileapps/components/angular/ng-component元件並包括 `frameworkType: angular` 屬性。

### template.jsp {#template-jsp}

首先在body.jsp節中介紹，template.jsp只包含頁面的parsys。 在發佈模式下，此內容直接引用(在 &lt;page-path>.template.html)，並通過在SPA$routeProvider上配置的templateUrl載入到中。

此指令碼中的parsys可配置為接受任何類型的元件。 但是，在處理為傳統網站（而非傳統網站）構建的元件時必須SPA小心。 例如，基礎映像元件僅在頂級應用程式頁面上正常工作，因為它不是設計為引用應用程式內部的資產。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

此指令碼只輸出頂級Angular應用模組的Angular依賴項。 angular-app-module.js.jsp引用了它。

### header.jsp {#header-jsp}

將靜態內容放置在應用頂部的指令碼。 此內容由頂級頁面包含，位於ng-view範圍之外。

### footer.jsp {#footer-jsp}

將靜態內容放在應用底部的指令碼。 此內容由頂級頁面包含，位於ng-view範圍之外。

### js_clientlibs.jsp {#js-clientlibs-jsp}

覆蓋此指令碼以包括JavaScript客戶端。

### css_clientlibs.jsp {#css-clientlibs-jsp}

覆蓋此指令碼以包括CSS客戶端。

## 應用程式元件 {#app-components}

應用程式元件不僅必須在實AEM例（發佈或作者）上工作，而且當應用程式內容通過內容同步導出到檔案系統時也必須工作。 因此，元件必須包括以下特徵：

* 必須相對引用PhoneGap應用程式中的所有資產、模板和指令碼。
* 如果實例以作者或發佈模式AEM操作，則對連結的處理會有所不同。

### 相對資產 {#relative-assets}

PhoneGap應用程式中任何給定資產的URI不僅在每個平台上不同，而且在應用程式的每個安裝上都是唯一的。 例如，請注意在iOS模擬器中運行的應用的以下URI:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

請注意路徑中的GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;。

作為PhoneGap開發人員，您所關心的內容位於www目錄下。 要訪問應用程式資產，請使用相對路徑。

要複合此問題，您的PhoneGap應用程式使用單頁應用(SPA)模式，以便基本URI（不包括哈希）永不更改。 因此，您引用的每個資產、模板或指令碼**必須相對於頂級頁面。 **頂級頁根據以下條件初始化Angular路由和控制器 `*<name>*.angular-app-module.js` 和 `*<name>*.angular-app-controllers.js`。 此頁應是與儲存庫根目錄最接近的*不*擴展sling:redirect的頁。

有幾種幫助方法可用於處理相對路徑：

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

要查看其使用示例，請開啟位於/libs/mobileapps/components/angular的mobileapps源。

### 連結 {#links}

連結必須使用 `ng-click="go('/path')"` 功能支援所有WCM模式。 此函式取決於作用域變數的值以正確確定連結操作：

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

當 `$scope.wcmMode == true` 我們以通常的方式處理每個導航事件，以便結果是對URL的路徑和/或頁面部分的更改。

或者，如果 `$scope.wcmMode == false`，每個導航事件都會導致URL的散列部分發生更改，該散列部分由Angular的ngRoute模組在內部解析。

### 元件指令碼詳細資訊 {#component-script-details}

![chlimage_1-144](assets/chlimage_1-144.png)

#### ng-component.jsp {#ng-component-jsp}

此指令碼在檢測到「編輯」模式時顯示元件內容或合適的佔位符。

#### template.jsp {#template-jsp-1}

template.jsp指令碼將呈現元件的標籤。 如果所涉元件由從中提取的JSON資料驅動AEM(例如「ng-text」：/libs/mobileapps/components/angular/ng-text/template.jsp)，則此指令碼將負責將標籤與頁面的控制器作用域所暴露的資料連接起來。

但是，效能要求有時要求不執行客戶端模板（亦即資料綁定）。 在這種情況下，只需在伺服器端呈現元件的標注，並將其包含在頁面模板內容中。

#### overhead.jsp {#overhead-jsp}

在由JSON資料驅動的元件中（如「ng-text」）:/libs/mobileapps/components/angular/ng-text)、opperaince.jsp可用於從template.jsp中刪除所有Java代碼。 然後從template.jsp引用該變數，並且該變數在請求中顯示的任何變數都可供使用。 此策略鼓勵將邏輯與呈現分離，並限制從現有元件派生新元件時必須複製和貼上的代碼量。

#### controller.js.jsp {#controller-js-jsp-1}

如頁面模AEM板中所述，每個元件都可以輸出JavaScript片段，以使用由 `data` 答應。 遵循Angular約定，控制器只應用於為作用域分配變數。

#### angular.json.jsp {#angular-json-jsp}

此指令碼作為片段包含在頁面範圍的「」中&lt;page-name>.angular.json&quot;檔案，它為擴展ng-page的每頁導出。 在此檔案中，元件開發人員可以公開元件所需的任何JSON結構。 在「ng-text」示例中，此結構只包括元件的文本內容和指示元件是否包括富文本的標誌。

Geometrixx室外應用程式產品元件是一個更複雜的示例(/apps/geometrixx-outdoors-app/components/angular/ng-product):

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

從應用程式控制台下載CLI資產，以針對特定平台優化這些資產，然後使用PhoneGap命令行整合(CLI)API構建應用。 保存到本地檔案系統的ZIP檔案的內容具有以下結構：

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

### 科爾多瓦 {#cordova}

這是一個隱藏目錄，根據您當前的OS設定，您可能看不到它。 您應配置OS，以便在計畫修改其包含的應用掛接時，此目錄是可見的。

#### .cordova/掛接/ {#cordova-hooks}

此目錄包含 [CLI掛接](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/)。 掛接目錄中的資料夾包含在生成過程中精確點執行的node.js指令碼。

#### .cordova/hooks/afterplatform_add/ {#cordova-hooks-after-platform-add}

after-platform_add目錄包含 `copy_AMS_Conifg.js` 的子菜單。 此指令碼複製配置檔案以支援Adobe移動服務分析的集合。

#### .cordova/hooks/prepare/ {#cordova-hooks-after-prepare}

準備後目錄包含 `copy_resource_files.js` 的子菜單。 此指令碼將許多表徵圖和閃屏影像複製到特定於平台的位置。

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add目錄包含 `install_plugins.js` 的子菜單。 此指令碼通過Cordova插件標識符清單迭代，安裝它檢測到的不可用的插件。

此策略不要求每次Maven的安裝時都AEM捆綁和安裝插件 `content-package:install` 命令。 將檔案簽入SCM系統的替代策略需要重複捆綁和安裝活動。

#### .cordova/hooks/其他掛接 {#cordova-hooks-other-hooks}

根據需要包括其他掛接。 以下掛接可用（如Phonegap示例hello world應用提供）:

* 生成後
* 生成前
* 編譯後
* 編譯前
* 後
* 之前
* 後值
* 先於模擬
* after_platform_add
* 之前_平台_添加
* 後_平台_ls
* 之前_平台_ls
* 後_平台_rm
* 之前_平台_rm
* 後_plugin_add
* 之前_plugin_add
* 後_plugin_ls
* 之前_plugin_ls
* 後_plugin_rm
* 在_plugin_rm之前
* 後準備
* 在準備之前
* 運行後
* 運行前

#### 平台/ {#platforms}

此目錄為空，直到您執行 `phonegap run <platform>` 的子菜單。 目前， `<platform>` 可以 `ios` 或 `android`。

在為特定平台構建應用程式後，將建立相應的目錄，並包含特定於平台的應用程式碼。

#### 插件/ {#plugins}

插件目錄由中列出的每個插件填充 `.cordova/hooks/before_platform_add/install_plugins.js` 檔案 `phonegap run <platform>` 的子菜單。 目錄最初為空。

#### 萬維網 {#www}

www目錄包含實現應用外觀和行為的所有Web內容(HTML、JS和CSS檔案)。 除下面所述的例外外，此內容源自AEM，並通過內容同步導出到其靜態格式。

#### www/config.xml {#www-config-xml}

的 [PhoneGap文檔](https://docs.phonegap.com) 將此檔案稱為「全局配置檔案」。 config.xml包含許多應用屬性，如應用的名稱、應用「首選項」(例如，iOSWebview是否允許溢出滾動)和插件依賴關係 *僅* 由PhoneGap生成使用。

config.xml檔案是中的靜態文AEM件，通過內容同步按原樣導出。

#### www/index.html {#www-index-html}

index.html檔案重定向到應用的起始頁。

config.xml檔案包含 `content` 元素：

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

在 [PhoneGap文檔](https://docs.phonegap.com)，此元素描述為「可選」 &lt;content> 元素在頂級web資產目錄中定義應用程式的起始頁。 預設值為index.html，它通常出現在項目的頂級ww目錄中。&quot;

如果不存在index.html檔案，則PhoneGap生成失敗。 因此，此檔案被包括。

#### ww/res {#www-res}

res目錄包含閃屏影像和表徵圖。 的 `copy_resource_files.js` 指令碼將檔案複製到其平台特定的位置 `after_prepare` 構建階段。

#### 萬維網 {#www-etc}

按慣例，在/etcAEM節點中包含靜態客戶端庫內容。 etc目錄包含Topcoat、AngularJS和Geometrixxng-clientlibsall庫。

#### ww/apps {#www-apps}

應用目錄包含與閃屏頁相關的代碼。 應用的啟動頁的獨特AEM特點是它在不進行用戶交互的情況下初始化應用。 因此，應用的客戶端庫內容（CSS和JS）是最小的，以最大限度地提高效能。

#### www/內容 {#www-content}

內容目錄包含應用的其餘Web內容。 內容可以包括（但不限於）下列檔案：

* HTML頁面內容，直接在AEM中
* 與元件關聯的映AEM像資產
* 伺服器端指令碼生成的JavaScript內容
* 描述頁面或元件內容的JSON檔案

#### www/package.json {#www-package-json}

package.json檔案是一個清單檔案，它列出 **全** 內容同步下載包括。 此檔案還包含生成內容同步負載的時間戳( `lastModified`)。 此屬性用於請求應用的部分更新AEM。

#### www/package-update.json {#www-package-update-json}

如果此負載是整個應用的下載，則此清單包含檔案的確切清單 `package.json`。

但是，如果此負載是部分更新， `package-update.json` 僅包含包含在此特定負載中的檔案。

### 後續步驟 {#the-next-steps}

一旦你瞭解了應用的解剖結構，請參閱 [單頁應用程式](/help/mobile/phonegap-single-page-applications.md)。
