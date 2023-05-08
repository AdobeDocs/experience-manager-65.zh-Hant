---
title: 應用程式的解剖
seo-title: The Anatomy of an App
description: 本頁面說明您為應用程式建立的頁面元件是以/libs/mobileapps/components/angular/ng-page元件(本機伺服器上的CRXDE Lite)為基礎。
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

# 應用程式的解剖{#the-anatomy-of-an-app}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

## 行動應用程式的頁面範本 {#page-templates-for-mobile-apps}

您為應用程式建立的頁面元件是以/libs/mobileapps/components/angular/ng-page元件([在本機伺服器上以CRXDE Lite方式開啟](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page))。 此元件包含以下JSP指令碼，您的元件會繼承或覆蓋這些指令碼：

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

使用 `applicationName` 屬性，並透過pageContext公開。

包含head.jsp和body.jsp。

### head.jsp {#head-jsp}

寫出 `<head>` 應用程式頁面的元素。

如果您想要覆寫應用程式的檢視區中繼屬性，此為您覆寫的檔案。

依照最佳實務，應用程式會在標題中包含用戶端資料庫的css部分，而JS則包含在結尾的&lt; `body>` 元素。

### body.jsp {#body-jsp}

根據是否偵測到wcmMode,Angular頁面的內文呈現不同(!= WCMMode.DISABLED)，以判斷頁面是開啟以進行編寫，還是開啟為已發佈頁面。

**製作模式**

在製作模式中，每個個別頁面會個別呈現。 Angular不處理頁面間的路由，也不是用於載入包含頁面元件的部分範本的ng檢視。 而是會透過 `cq:include` 標籤。

此策略可啟用作者功能（例如在段落系統中新增和編輯元件、Sidekick、設計模式等） 函式而無須修改。 需要用戶端轉譯的頁面（例如應用程式的頁面）在AEM製作模式中無法正常運作。

請注意，template.jsp包含已包裝在 `div` 包含 `ng-controller` 指令。 此結構可讓DOM內容與控制器連結。 因此，雖然在用戶端呈現自己的頁面會失敗，但個別元件仍可正常運作（請參閱下方「元件」一節）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**發佈模式**

在發佈模式（例如使用內容同步匯出應用程式時），所有頁面都會變成單頁應用程式(SPA)。 (若要了解SPA，請使用Angular教學課程，具體說明 [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

SPA中只有一個HTML頁面(包含 `<html>` 元素)。 此頁面稱為「版面範本」。 在Angular術語中，它是「……此範本是應用程式中所有檢視的通用範本。」 將此頁面視為「頂層應用程式頁面」。 依照慣例，頂層應用程式頁面為 `cq:Page` 最接近根（而非重新導向）之應用程式的節點。

由於應用程式的實際URI不會在發佈模式中變更，因此來自此頁面的外部資產參考必須使用相對路徑。 因此，提供了一種特殊影像元件，在呈現要導出的影像時考慮此頂級頁面。

作為SPA，此版面範本頁面只會產生具有ng-view指令的div元素。

```xml
 <div ng-view ng-class="transition"></div>
```

angular路由服務使用此元素來顯示應用程式中每個頁面的內容，包括目前頁面的可授權內容（包含在template.jsp中）。

body.jsp檔案包含header.jsp和footer.jsp，這些檔案為空。 如果您想要在每個頁面上提供靜態內容，您可以在應用程式中覆寫這些指令碼。

最後，javascript clientlibs會包含在 &lt;body> 元素，包括伺服器上產生的兩個特殊JS檔案： *&lt;page name=&quot;&quot;>*.angular-app-module.js和 *&lt;page name=&quot;&quot;>*.angular-app-controllers.js。

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

此指令碼定義應用程式的Angular模組。 此指令碼的輸出連結到模板的其餘元件通過 `html` ng-page.jsp中的元素，包含下列屬性：

```xml
ng-app="<c:out value='${applicationName}'/>"
```

此屬性會指出此DOM元素的內容應連結至下列模組。 此模組會將檢視(在AEM中會是cq:Page資源)與對應的控制器連結。

此模組還定義了一個頂級控制器，名為 `AppController` 會公開 `wcmMode` 變數，並設定從中擷取內容同步更新裝載的URI。

最後，此模組會反覆處理每個子系頁面（包括本身），並轉譯每個頁面的路由片段內容(透過angular-route-fragment.js選取器和擴充功能)，包括作為Angular$routeProvider的設定項目。 換言之，$routeProvider會告訴應用程式當請求指定路徑時要呈現的內容。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

此指令碼會產生必須採用下列形式的JavaScript片段：

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

此代碼指示$routeProvider(在angular-app-module.js.jsp中定義)「/」&lt;path>&#39;將由位於的資源處理 `templateUrl`，並透過 `controller` （我們下一步將討論）。

如有必要，您可以覆寫此指令碼以處理更複雜的路徑，包括含有變數的路徑。 在隨AEM安裝的/apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp指令碼中可看到此示例：

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

在Angular中，控制者會在$scope中匯整變數，將其顯示在檢視中。 angular-app-controllers.js.jsp指令碼遵循angular-app-module.js.jsp所示的模式，即它在每個子體頁面（包括自身）中反覆執行，並輸出每個頁面定義的控制器片段(透過controller.js.jsp)。 其定義的模組稱為 `cqAppControllers` 和必須列為頂層應用程式模組的相依性，頁面控制器才可供使用。

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

請注意， `data` 變數會被指派給Angular傳回的promise `$http.get` 方法。 如有需要，此頁面中包含的每個元件都可讓某些.json內容可供使用(透過其angular.json.jsp指令碼)，並在解析此請求時對其內容採取行動。 請求在行動裝置上非常快，因為它只會存取檔案系統。

為了以這種方式成為控制器的一部分，元件應擴展/libs/mobileapps/components/angular/ng-component元件並包括 `frameworkType: angular` 屬性。

### template.jsp {#template-jsp}

petmale.jsp是首先在body.jsp區段中引入，它只包含頁面的parsys。 在發佈模式中，會直接參照此內容(在 &lt;page-path>.template.html)，並透過$routeProvider上設定的templateUrl載入SPA中。

此指令碼中的parsys可以配置為接受任何類型的元件。 不過，在處理針對傳統網站(而非SPA)建置的元件時，必須謹慎處理。 例如，基礎影像元件只有在頂層應用程式頁面上才能正確運作，因為其設計並非要參考應用程式內的資產。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

此指令碼只會輸出頂層Angular應用程式模組的Angular相依性。 angular-app-module.js.jsp會參考此函式。

### header.jsp {#header-jsp}

將靜態內容放置在應用程式頂端的指令碼。 此內容會由頂層頁面包含，不在ng-view範圍內。

### footer.jsp {#footer-jsp}

將靜態內容放置在應用程式底部的指令碼。 此內容會由頂層頁面包含，不在ng-view範圍內。

### js_clientlibs.jsp {#js-clientlibs-jsp}

覆寫此指令碼以包含您的JavaScript用戶端。

### css_clientlibs.jsp {#css-clientlibs-jsp}

覆蓋此指令碼以包含您的CSS客戶端。

## 應用程式元件 {#app-components}

應用程式元件不僅必須在AEM執行個體（發佈或製作）上運作，而且必須在應用程式內容透過內容同步匯出至檔案系統時運作。 因此，元件必須包含下列特性：

* PhoneGap應用程式中的所有資產、範本和指令碼必須相對引用。
* 如果AEM例項在製作或發佈模式中運作，連結的處理方式會有所不同。

### 相對資產 {#relative-assets}

PhoneGap應用程式中任何指定資產的URI不僅會依各平台而有所不同，而且應用程式的每個安裝都是唯一的。 例如，請注意下列在iOS模擬器中執行之應用程式的URI:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

請注意路徑中的GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;。

作為PhoneGap開發人員，您關注的內容位於www目錄下。 若要存取應用程式資產，請使用相對路徑。

若要複合此問題，您的PhoneGap應用程式會使用單頁應用程式(SPA)模式，使基本URI（排除雜湊）永不變更。 因此，您參考的每個資產、范**或指令碼都必須相對於您的頂層頁面。 **頂層頁通過以下方式初始化Angular路由和控制器： `*<name>*.angular-app-module.js` 和 `*<name>*.angular-app-controllers.js`. 此頁面應是距存放庫根目錄最近的頁面，*不會*延伸sling:redirect。

處理相對路徑時有數種輔助方法：

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

若要查看其使用範例，請開啟位於/libs/mobileapps/components/angular的mobileapps來源。

### 連結 {#links}

連結必須使用 `ng-click="go('/path')"` 功能，以支援所有WCM模式。 此函式取決於範圍變數的值，才能正確判斷連結動作：

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

當 `$scope.wcmMode == true` 我們會以通常的方式處理每個導覽事件，因此會變更URL的路徑和/或頁面部分。

或者，如果 `$scope.wcmMode == false`，則每個導覽事件都會導致URL的雜湊部分變更，而雜湊部分會由Angular的ngRoute模組在內部解析。

### 元件指令碼詳細資訊 {#component-script-details}

![chlimage_1-144](assets/chlimage_1-144.png)

#### ng-component.jsp {#ng-component-jsp}

檢測到「編輯」模式時，此指令碼將顯示元件內容或適當的佔位符。

#### template.jsp {#template-jsp-1}

template.jsp指令碼將呈現元件的標籤。 如果相關元件是由從AEM擷取的JSON資料驅動（例如「ng-text」）:/libs/mobileapps/components/angular/ng-text/template.jsp)，則此指令碼將負責將標籤與頁面的控制器範圍公開的資料進行佈線。

但是，效能要求有時會要求不執行任何用戶端範本（亦即資料捆綁）。 在此情況下，只需在伺服器端轉譯元件的標籤，元件就會包含在頁面範本內容中。

#### overhead.jsp {#overhead-jsp}

在由JSON資料驅動的元件中（例如「ng-text」）:/libs/mobileapps/components/angular/ng-text), interprise.jsp可用來從template.jsp移除所有Java代碼。 然後會從template.jsp參考此變數，而它在請求上公開的任何變數都可供使用。 此策略鼓勵將邏輯與呈現分離，並限制從現有元件衍生新元件時必須複製和貼上的程式碼量。

#### controller.js.jsp {#controller-js-jsp-1}

如AEM頁面範本中所述，每個元件都可輸出JavaScript片段，以使用 `data` 承諾。 遵循Angular慣例，控制器僅應用於將變數指派給範圍。

#### angular.json.jsp {#angular-json-jsp}

此指令碼作為片段包含在頁面範圍內的「&lt;page-name>.angular.json&#39;檔案，會針對延伸ng-page的每個頁面匯出。 在此檔案中，元件開發人員可公開元件所需的任何JSON結構。 在「ng-text」示例中，此結構僅包括元件的文本內容，以及指示元件是否包括RTF的標誌。

Geometrixx戶外應用程式產品元件是更複雜的範例(/apps/geometrixx-outdoors-app/components/angular/ng-product):

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

## CLI Assets下載內容 {#contents-of-the-cli-assets-download}

從Apps控制台下載CLI資產，針對特定平台最佳化資產，然後使用PhoneGap命令列整合(CLI)API建立應用程式。 您保存到本地檔案系統的ZIP檔案的內容具有以下結構：

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

這是隱藏的目錄，根據您當前的作業系統設定，您可能看不到。 如果您打算修改作業系統所包含的應用程式鈎點，則應設定作業系統，以便顯示此目錄。

#### .cordova/hooks/ {#cordova-hooks}

此目錄包含 [CLI掛接](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/). 鈎點目錄中的資料夾包含在建立期間精確點執行的node.js指令碼。

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add目錄包含 `copy_AMS_Conifg.js` 檔案。 此指令碼會複製設定檔案以支援AdobeMobile Services分析的收集。

#### .cordova/hooks/after prepare/ {#cordova-hooks-after-prepare}

after-prepare目錄包含 `copy_resource_files.js` 檔案。 此指令碼將多個表徵圖和閃屏影像複製到平台特定的位置。

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add目錄包含 `install_plugins.js` 檔案。 此指令碼會反覆顯示Cordova外掛程式識別碼清單，安裝它偵測到的識別碼尚未可用。

此策略不要求您每次在Maven上將外掛程式捆綁並安裝至AEM `content-package:install` 命令。 將檔案簽入SCM系統的替代策略需要重複捆綁和安裝活動。

#### .cordova/hooks/其他鈎點 {#cordova-hooks-other-hooks}

視需要包含其他鈎點。 下列鈎點可供使用（如Phonegap範例hello world應用程式所提供）:

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

#### 平台/ {#platforms}

此目錄為空，直到您執行 `phonegap run <platform>` 命令。 目前， `<platform>` 可以是 `ios` 或 `android`.

為特定平台建立應用程式後，會建立對應目錄，其中包含特定平台的應用程式程式碼。

#### plugins/ {#plugins}

外掛程式目錄會由列於 `.cordova/hooks/before_platform_add/install_plugins.js` 檔案 `phonegap run <platform>` 命令。 目錄最初為空。

#### www/ {#www}

www目錄包含實作應用程式外觀和行為的所有Web內容(HTML、JS和CSS檔案)。 除了下文所述的例外情況，此內容源自AEM，並透過「內容同步」匯出為靜態格式。

#### www/config.xml {#www-config-xml}

此 [PhoneGap檔案](https://docs.phonegap.com) 將此檔案稱為「全域設定檔案」。 config.xml包含許多應用程式屬性，例如應用程式名稱、應用程式「偏好設定」(例如iOS網頁檢視是否允許捲動)，以及 *僅限* 由PhoneGap組建使用。

config.xml檔案是AEM中的靜態檔案，會透過「內容同步」依原樣匯出。

#### www/index.html {#www-index-html}

index.html檔案會重新導向至應用程式的起始頁面。

config.xml檔案包含 `content` 元素：

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

在 [phoneGap檔案](https://docs.phonegap.com)，此元素會說明為「選用 &lt;content> 元素會在頂層web資產目錄中定義應用程式的開始頁面。 預設值為index.html，它通常顯示在項目的頂級ww目錄中。」

如果index.html檔案不存在，PhoneGap組建會失敗。 因此，會包含此檔案。

#### www/res {#www-res}

res目錄包含閃屏影像和表徵圖。 此 `copy_resource_files.js` 指令碼會在 `after_prepare` 建置階段。

#### ww/etc {#www-etc}

根據慣例，在AEM中， /etc節點包含靜態clientlib內容。 etc目錄包含Topcoat、AngularJS和Geometrixxng-clientlibsall庫。

#### www/apps {#www-apps}

應用程式目錄包含與閃屏頁面相關的代碼。 AEM應用程式開始顯示頁面的獨特之處在於，它會在不進行使用者互動的情況下初始化應用程式。 因此，應用程式的clientlib內容（包括CSS和JS）會降至最低，以發揮最大效能。

#### www/content {#www-content}

內容目錄包含應用程式的其餘Web內容。 內容可包含但不限於下列檔案：

* HTML頁面內容，是直接在AEM中製作
* 與AEM元件相關聯的影像資產
* 伺服器端指令碼產生的JavaScript內容
* 說明頁面或元件內容的JSON檔案

#### www/package.json {#www-package-json}

package.json檔案是資訊清單檔案，會列出 **完整** 內容同步下載包含。 此檔案也包含產生內容同步裝載的時間戳記( `lastModified`)。 從AEM要求部分更新應用程式時，會使用此屬性。

#### www/package-update.json {#www-package-update-json}

如果此裝載是整個應用程式的下載，此資訊清單會包含檔案的確切清單，如 `package.json`.

不過，如果此裝載為部分更新， `package-update.json` 僅包含此特定裝載中包含的檔案。

### 後續步驟 {#the-next-steps}

一旦你了解了應用的解剖結構，請參閱 [單頁應用程式](/help/mobile/phonegap-single-page-applications.md).
