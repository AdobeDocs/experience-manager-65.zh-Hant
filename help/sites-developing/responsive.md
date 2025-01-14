---
title: 網頁的回應式設計
description: 透過回應式設計，相同的頁面可有效地以多個方向顯示在多個裝置上。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '5272'
ht-degree: 0%

---

# 網頁的回應式設計{#responsive-design-for-web-pages}

{{ue-over-mobile}}

>[!NOTE]
>
>各種範例是根據AEM (Adobe Experience Manager)不再隨附的Geometrixx範例內容，已由We.Retail取代。 如需如何下載和安裝Geometrixx，請參閱檔案[We.Retail參考實作](/help/sites-developing/we-retail.md#we-retail-geometrixx)。

設計您的網頁，使其適應顯示它們的使用者端檢視區。 透過回應式設計，相同的頁面可以有效的在兩個方向的多個裝置上顯示。 下圖示範頁面回應檢視區大小變更的一些方式：

* 配置：對較小的檢視區使用單欄配置，對較大的檢視區使用多欄配置。
* 文字大小：在較大的檢視區中使用較大的文字大小（如標題）。
* 內容：在較小裝置上顯示時，僅包含最重要的內容。
* 導覽：裝置專用的工具可供存取其他頁面。
* 影像：提供適合使用者端檢視區的影像轉譯。 視窗尺寸而定。

![chlimage_1-4](assets/chlimage_1-4a.png)

開發可產生HTML5頁面（可適應多種視窗大小和方向）的Adobe Experience Manager (AEM)應用程式。 例如，下列檢視區寬度範圍會與各種裝置型別和方向相對應

* 最大寬度480畫素（手機、直向）
* 最大寬度767畫素（手機、橫向）
* 介於768畫素和979畫素之間的寬度（平板電腦，縱向）
* 介於980畫素和1199畫素之間的寬度（平板電腦，橫向）
* 寬度1200畫素或更高（案頭）

請參閱下列主題，以取得關於實作回應式設計行為的資訊：

* [媒體查詢](/help/sites-developing/responsive.md#using-media-queries)
* [流動格線](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [最適化影像](/help/sites-developing/responsive.md#using-adaptive-images)

在設計時，使用&#x200B;**[!UICONTROL Sidekick]**&#x200B;來預覽您各種熒幕大小的頁面。

## 開發之前 {#before-you-develop}

在開發支援網頁的AEM應用程式之前，您應該先做出數個設計決策。 例如，您必須擁有下列資訊：

* 您正在定位的裝置。
* 目標檢視區大小。
* 每個目標檢視區大小的頁面配置。

### 應用程式結構 {#application-structure}

典型的AEM應用程式結構支援所有回應式設計實施：

* 頁面元件位於/apps/*application_name*/components之下
* 範本位於/apps/*application_name*/templates之下
* 設計位於/etc/designs之下

## 使用媒體查詢 {#using-media-queries}

媒體查詢可讓您在頁面轉譯時選擇性使用CSS樣式。 AEM開發工具和功能可讓您在應用程式中有效率地實作媒體查詢。

W3C群組提供說明此CSS3功能與語法的[媒體查詢](https://www.w3.org/TR/mediaqueries-3/)建議。

### 建立CSS檔案 {#creating-the-css-file}

在CSS檔案中，根據您鎖定目標的裝置屬性定義媒體查詢。 下列實作策略可有效管理每個媒體查詢的樣式：

* 使用ClientLibraryFolder定義在轉譯頁面時組合的CSS。
* 在不同的CSS檔案中定義每個媒體查詢和相關樣式。 使用代表媒體查詢之裝置功能的檔案名稱會很有用。
* 定義個別CSS檔案中所有裝置通用的樣式。
* 在ClientLibraryFolder的css.txt檔案中，依組合的CSS檔案的必要順序排列CSS檔案。

`We.Retail`媒體範例使用此策略來定義網站設計中的樣式。 `We.Retail`使用的CSS檔案位於`*/apps/weretail/clientlibs/clientlib-site/less/grid.less`。

下表列出css子資料夾中的檔案。

<table>
 <tbody>
  <tr>
   <th>檔案名稱</th>
   <th>說明</th>
   <th>媒體查詢</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>通用樣式。</td>
   <td>不適用</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>通用樣式，由TwitterBootstrap定義。</td>
   <td>不適用</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>所有寬度或寬度為1200畫素之媒體的樣式。</td>
   <td><p>@media （最小寬度： 1200畫素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>介於980畫素和1199畫素寬之間的媒體樣式。</td>
   <td><p>@media （最小寬度： 980畫素）和（最大寬度： 1199畫素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>介於768畫素和979畫素寬之間的媒體樣式。 </td>
   <td><p>@media （最小寬度： 768畫素）和（最大寬度： 979畫素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>寬度小於768畫素的所有媒體樣式。</td>
   <td><p>@media （最大寬度： 767畫素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>寬度小於481畫素的所有媒體樣式。</td>
   <td>@media （最大寬度： 480畫素） {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

`/etc/designs/weretail/clientlibs`資料夾中的css.txt檔案會列出使用者端資料庫資料夾所包含的CSS檔案。 檔案的順序會實作樣式優先順序。 裝置大小減少時，樣式會更加具體。

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**提示**：描述性檔案名稱可讓您輕鬆識別目標檢視區大小。

### 搭配AEM頁面使用媒體查詢 {#using-media-queries-with-aem-pages}

在頁面元件的JSP指令碼中包含使用者端程式庫資料夾。 這麼做有助於產生包含媒體查詢的CSS檔案，並參考該檔案。

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>`apps.weretail.all`使用者端資料庫資料夾內嵌clientlibs資料庫。

JSP指令碼會產生下列參考樣式表的HTML代碼：

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## 預覽特定裝置 {#previewing-for-specific-devices}

檢視不同檢視區大小的頁面預覽，以便測試回應式設計的行為。 在&#x200B;**[!UICONTROL 預覽]**&#x200B;模式中，**[!UICONTROL Sidekick]**&#x200B;包含您用來選取裝置的&#x200B;**[!UICONTROL 裝置]**&#x200B;下拉式功能表。 選取裝置時，頁面會隨著檢視區大小而改變。

![chlimage_1-5](assets/chlimage_1-5a.png)

若要在&#x200B;**[!UICONTROL Sidekick]**&#x200B;中啟用裝置預覽，您必須設定頁面和&#x200B;**[!UICONTROL MobileEmulatorProvider]**&#x200B;服務。 另一個頁面設定會控制出現在&#x200B;**[!UICONTROL 裝置]**&#x200B;清單中的裝置清單。

### 新增裝置清單 {#adding-the-devices-list}

當您的頁面包含轉譯&#x200B;**[!UICONTROL 裝置]**&#x200B;清單的JSP指令碼時，**[!UICONTROL 裝置]**&#x200B;清單會顯示在&#x200B;**[!UICONTROL Sidekick]**&#x200B;中。 若要將&#x200B;**[!UICONTROL 裝置]**&#x200B;清單新增至&#x200B;**[!UICONTROL Sidekick]**，請在頁面的`head`區段中包含`/libs/wcm/mobile/components/simulator/simulator.jsp`指令碼。

在定義`head`區段的JSP中包含以下程式碼：

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

若要檢視範例，請以CRXDE Lite開啟`/apps/weretail/components/page/head.jsp`檔案。

### 登入要模擬的頁面元件 {#registering-page-components-for-simulation}

若要啟用裝置模擬器來支援您的頁面，請使用MobileEmulatorProvider Factory服務註冊您的頁面元件，並定義`mobile.resourceTypes`屬性。

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得完整詳細資訊。

例如，若要在應用程式中建立` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)`節點：

* 父資料夾： `/apps/application_name/config`
* 名稱：`com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

  需要 — `*alias*`尾碼，因為MobileEmulatorProvider服務是工廠服務。 使用這個工廠唯一的任何別名。

* `jcr:primaryType`: `sling:OsgiConfig`

新增下列節點屬性：

* 名稱：`mobile.resourceTypes`
* 類型：`String[]`
* 值：呈現網頁之頁面元件的路徑。 例如， geometrixx-media應用程式會使用以下值：

  ```
  geometrixx-media/components/page
   geometrixx-unlimited/components/pages/page
   geometrixx-unlimited/components/pages/coverpage
   geometrixx-unlimited/components/pages/issue
  ```

### 指定裝置群組 {#specifying-the-device-groups}

若要指定出現在[裝置]清單中的裝置群組，請新增`cq:deviceGroups`屬性至網站根頁面的`jcr:content`節點。 屬性的值是裝置群組節點的路徑陣列。

裝置群組節點位於`/etc/mobile/groups`資料夾中。

例如，Geometrixx Media網站的根頁面為`/content/geometrixx-media`。 `/content/geometrixx-media/jcr:content`節點包含下列屬性：

* 名稱：`cq:deviceGroups`
* 類型：`String[]`
* 值： `/etc/mobile/groups/responsive`

使用[工具]主控台[建立及編輯裝置群組](/help/sites-developing/groupfilters.md)。

>[!NOTE]
>
>對於您用於回應式設計的裝置群組，請編輯裝置群組，然後在「一般」標籤上選取「停用模擬器」。 此選項會防止出現模擬器輪播，這與回應式設計無關。
>

## 使用自適應影像 {#using-adaptive-images}

您可以使用媒體查詢來選取要在頁面中顯示的影像資源。 不過，使用媒體查詢來將其使用條件化的每個資源都會下載到使用者端。 媒體查詢只會決定是否顯示下載的資源。

對於大型資源（例如影像），下載所有資源並非有效使用使用者端的資料管道。 若要選擇性地下載資源，請在媒體查詢執行選取範圍後，使用JavaScript來起始資源要求。

以下策略會載入使用媒體查詢選擇的單一資源：

1. 為資源的每個版本新增DIV元素。 將資源的URI加入為屬性值的值。 瀏覽器不會將屬性解譯為資源。
1. 將媒體查詢新增至適用於資源的每個DIV元素。
1. 當檔案載入或視窗調整大小時，JavaScript程式碼會測試每個DIV元素的媒體查詢。
1. 根據查詢的結果，決定要納入的資源。
1. 在參照資源的DOM中插入HTML元素。

### 使用JavaScript評估媒體查詢 {#evaluating-media-queries-using-javascript}

W3C定義的[MediaQueryList介面](https://drafts.csswg.org/cssom-view/#the-mediaquerylist-interface)實作可讓您使用JavaScript評估媒體查詢。 您可以將邏輯套用至媒體查詢結果，並執行目前視窗的目標指令碼：

* 實作MediaQueryList介面的瀏覽器支援`window.matchMedia()`函式。 此函式根據給定字串測試媒體查詢。 此函式傳回`MediaQueryList`物件，以提供查詢結果的存取權。

* 對於未實作介面的瀏覽器，您可以使用`matchMedia()`多邊形填滿，例如[matchMedia.js](https://github.com/paulirish/matchMedia.js)，這是免費提供的JavaScript資料庫。

#### 選取媒體專用資源 {#selecting-media-specific-resources}

W3C [圖片元素](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element)使用媒體查詢來決定影像元素要使用的來源。 圖片元素會使用元素屬性，將媒體查詢與影像路徑建立關聯。

免費可用的[picturefill.js程式庫](https://github.com/scottjehl/picturefill)提供與建議的`picture`元素類似的功能，並使用類似的策略。 picturefill.js程式庫呼叫`window.matchMedia`以評估為一組`div`元素定義的媒體查詢。 每個`div`專案也會指定影像來源。 當`div`元素的媒體查詢傳回`true`時，會使用來源。

`picturefill.js`程式庫需要類似下列範例的HTML碼：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

轉譯頁面時，picturefull.js會插入`img`元素做為`<div data-picture>`元素的最後一個子項：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

在AEM頁面中，`data-src`屬性的值是存放庫中資源的路徑。

### 在AEM中實作最適化影像 {#implementing-adaptive-images-in-aem}

若要在AEM應用程式中實作最適化影像，您必須新增必要的JavaScript程式庫，並在您的頁面中包含必要的HTML標籤。

**資料庫**

取得下列JavaScript程式庫，並將其納入使用者端程式庫資料夾：

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) （針對未實作MediaQueryList介面的瀏覽器）
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (可透過`/etc/clientlibs/granite/jquery`使用者端資料庫資料夾(category = jquery)取得)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) （在視窗調整大小後發生一次的jquery事件）

**秘訣：**&#x200B;您可以透過[內嵌](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)自動串連多個使用者端資料庫資料夾。

**HTML**

建立可產生picturefill.js程式碼所需之必要div元素的元件。 在AEM頁面中，data-src屬性的值是儲存庫中資源的路徑。 例如，頁面元件可以硬式編碼媒體查詢和DAM中影像轉譯的相關路徑。 或者，建立自訂影像元件，讓作者選取影像轉譯或指定執行階段轉譯選項。

以下範例HTML會從相同影像的兩個DAM轉譯中選取。

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>最適化影像基礎元件會實作最適化影像：
>
>* 使用者端資料庫資料夾： `/libs/foundation/components/adaptiveimage/clientlibs`
>* 產生HTML的指令碼： `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>後續段落提供此元件的詳細資訊。
>

### 瞭解AEM中的影像演算 {#understanding-image-rendering-in-aem}

若要自訂影像演算，您應瞭解預設的AEM靜態影像演算實作。 AEM提供影像元件和影像轉譯servlet，可搭配使用以轉譯網頁的影像。 將影像元件納入頁面的段落系統時，會發生下列事件順序：

1. 製作：作者可編輯影像元件，以指定要包含在HTML頁面中的影像檔案。 檔案路徑會儲存為影像元件節點的屬性值。
1. 頁面請求：頁面元件的JSP會產生HTML代碼。 影像元件的JSP會產生影像元素，並將其新增至頁面。
1. 影像要求：網頁瀏覽器載入頁面，並根據img元素的src屬性要求影像。
1. 影像演算：影像演算servlet會將影像傳回至網頁瀏覽器。

![chlimage_1-6](assets/chlimage_1-6a.png)

例如，影像元件的JSP會產生下列HTML元素：

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

瀏覽器載入頁面時，會使用src屬性的值做為URL來要求影像。 Sling會解壓縮URL：

* 資源： `/content/mywebsite/en/_jcr_content/par/image_0`
* 副檔名： `.jpg`
* 選取器： `img`
* 字尾： `1358372073597.jpg`

`image_0`節點的`jcr:resourceType`值為`foundation/components/image`，它的`sling:resourceSuperType`值為`foundation/components/parbase`。 parbase元件包含img.java指令碼，此指令碼符合選取器和請求URL的副檔名GET。 CQ會使用此指令碼(servlet)來轉譯影像。

若要檢視指令碼的原始碼，請使用CRXDE Lite開啟`/libs/foundation/components/parbase/img.GET.java`
檔案。

## 根據目前檢視區大小縮放影像 {#scaling-images-for-the-current-viewport-size}

在執行階段根據使用者端檢視區的特性縮放影像，以提供符合回應式設計原則的影像。 使用servlet和編寫元件，使用與靜態影像演算相同的設計模式。

元件必須執行下列工作：

* 將影像資源的路徑和所需尺寸儲存為屬性值。
* 產生包含媒體選擇器及轉譯影像之服務呼叫的`div`元素。

>[!NOTE]
>
>Web使用者端使用matchMedia和Picturefill JavaScript程式庫（或類似的程式庫）來評估媒體選取器。
>

處理影像要求的servlet必須執行下列工作：

* 從元件屬性擷取影像的路徑和尺寸。
* 根據屬性縮放影像並傳回影像。

**可用的解決方案**

AEM會安裝下列實施，供您使用或擴充。

* 產生媒體查詢的自我調整影像基礎元件，以及對可縮放影像的自我調整影像元件Servlet的HTTP請求。
* GeometrixxCommons套件會安裝會改變影像解析度的影像參考修改Servlet範例servlet。

### 瞭解自我調整影像元件 {#understanding-the-adaptive-image-component}

最適化影像元件會產生最適化影像元件Servlet呼叫，以根據裝置熒幕調整大小的影像進行演算。 此元件包含下列資源：

* JSP：新增將媒體查詢與對最適化影像元件Servlet的呼叫相關聯的div元素。
* 使用者端資料庫： clientlibs資料夾是一個`cq:ClientLibraryFolder`，它會組合matchMedia polyfill JavaScript資料庫和修改過的Picturefill JavaScript資料庫。
* 編輯對話方塊： `cq:editConfig`節點會覆寫CQ Foundation影像元件，讓放置目標建立最適化影像元件，而非基礎影像元件。

#### 新增DIV元素 {#adding-the-div-elements}

adaptive-image.jsp指令碼包含以下產生div元素和媒體查詢的程式碼：

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

`path`變數包含目前資源的路徑（最適化影像元件節點）。 程式碼會產生具有下列結構的一系列`div`元素：

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

`data-scr`屬性的值是Sling解析為轉譯影像的最適化影像元件Servlet的URL。 data-media屬性包含根據使用者端屬性評估的媒體查詢。

下列HTML程式碼是JSP產生的`div`專案範例：

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### 變更影像大小選取器 {#changing-the-image-size-selectors}

如果您自訂最適化影像元件並變更寬度選擇器，則也必須設定最適化影像元件Servlet以支援寬度。

### 瞭解自我調整影像元件Servlet {#understanding-the-adaptive-image-component-servlet}

自我調整影像元件Servlet會根據指定的寬度調整JPEG影像的大小，並設定JPEG品質。

#### 自我調整影像元件Servlet的介面 {#the-interface-of-the-adaptive-image-component-servlet}

最適化影像元件Servlet繫結至預設的Sling servlet，並支援.jpg、.jpeg、.gif和.png副檔名。 Servlet選擇器為img。

>[!CAUTION]
>
>AEM不支援動畫.gif檔案以進行最適化轉譯。

因此，Sling將以下格式的HTTP請求URL解析為此servlet：

`*path-to-node*.img.*extension*`

例如，Sling會將URL為`http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg`的HTTP要求轉送至最適化影像元件Servlet。

另外兩個選擇器可指定要求的影像寬度和JPEG品質。 下列範例會要求寬度480畫素和中等品質的影像：

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**支援的影像屬性**

此servlet接受有限數量的影像寬度和品質。 預設支援下列寬度（畫素）：

* 完整
* 320
* 480
* 476
* 620

完整值表示沒有縮放。

支援下列JPEG品質值：

* 低
* 中
* 高

數值分別為0.4、0.82和1.0。

**正在變更預設支援的寬度**

使用Web主控台([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))或sling：OsgiConfig節點來設定Adobe CQ最適化影像元件Servlet的支援寬度。

如需如何設定AEM服務的詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>網頁主控台</th>
   <th>sling：OsgiConfig</th>
  </tr>
  <tr>
   <th>服務或節點名稱</th>
   <td>「設定」標籤上的服務名稱是Adobe CQ最適化影像元件Servlet</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>屬性</th>
   <td><p>支援的寬度</p>
    <ul>
     <li>若要新增支援的寬度，請按一下+按鈕並輸入正整數。</li>
     <li>若要移除支援的寬度，請按一下相關聯的 — 按鈕。</li>
     <li>若要修改支援的寬度，請編輯欄位值。</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>屬性是多值字串值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 實作詳細資料 {#implementation-details}

`com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet`類別會擴充[AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html)類別。 AdaptiveImageComponentServlet原始程式碼位於`/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl`資料夾中。

類別會使用Felix SCR註解來設定與servlet關聯的資源型別和檔案副檔名，以及第一個選取器的名稱。

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

此servlet使用「屬性SCR」註解來設定預設支援的影像品質和尺寸。

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

`AbstractImageServlet`類別提供處理HTTP要求的`doGet`方法。 此方法會判斷與要求關聯的資源、從存放庫擷取資源屬性，並在[ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html)物件中傳回這些屬性。

>[!NOTE]
>
>[com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html)類別提供`getFileReference method`，它會擷取資源`fileReference`屬性的值。

`AdaptiveImageComponentServlet`類別會覆寫`createLayer`方法。 此方法會從`ImageContext`物件取得影像資源的路徑及要求的影像寬度。 然後它會呼叫`info.geometrixx.commons.impl.AdaptiveImageHelper`類別的方法，執行實際的影像縮放。

AdaptiveImageComponentServlet類別也會覆寫writeLayer方法。 此方法會將JPEG品質套用至影像。

### 影像參考修改Servlet (通用Geometrixx) {#image-reference-modification-servlet-geometrixx-common}

範例影像參考修改Servlet會產生影像元素的大小屬性，以縮放網頁上的影像。

#### 呼叫servlet {#calling-the-servlet}

此servlet繫結至`cq:page`資源，並支援.jpg副檔名。 此servlet選擇器是`image`。 因此，Sling將以下格式的HTTP請求URL解析為此servlet：

`path-to-page-node.image.jpg`

例如，Sling將URL為`http://localhost:4502/content/geometrixx/en.image.jpg`的HTTP要求轉送至影像參考修改Servlet。

另外三個選擇器可指定要求的影像寬度、高度和（選擇性）品質。 下列範例會要求寬度770畫素、高度360畫素和中等品質的影像。

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**支援的影像屬性**

此servlet接受有限數量的影像尺寸與品質值。

預設支援下列值(widthxheight)：

* 256x192
* 370x150
* 480x200
* 127x127
* 770x360
* 620x290
* 480x225
* 320x150
* 375x175
* 303x142
* 1170x400
* 940x340
* 770x300
* 480x190

支援下列影像品質值：

* 低
* 中
* 高

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得完整詳細資訊。

#### 指定影像資源 {#specifying-the-image-resource}

影像路徑、尺寸和品質值必須儲存為存放庫中節點的屬性：

* 節點名稱為`image`。
* 父節點是`cq:page`資源的`jcr:content`節點。

* 影像路徑會儲存為名為`fileReference`之屬性的值。

編寫頁面時，請使用&#x200B;**Sidekick**&#x200B;來指定影像並將`image`節點新增至頁面屬性：

1. 在&#x200B;**Sidekick**&#x200B;中，按一下&#x200B;**頁面**&#x200B;標籤，然後按一下&#x200B;**頁面屬性**。
1. 按一下&#x200B;**影像**&#x200B;索引標籤並指定影像。
1. 按一下&#x200B;**「確定」**。

#### 實作詳細資料 {#implementation-details-1}

info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet類別延伸[AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html)類別。 如果您已安裝cq-geometrixx-commons-pkg套件，則ImageReferenceModificationServlet原始程式碼位於`/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets`資料夾中。

類別會使用Felix SCR註解來設定與servlet關聯的資源型別和檔案副檔名，以及第一個選取器的名稱。

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

此servlet使用「屬性SCR」註解來設定預設支援的影像品質和尺寸。

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

`AbstractImageServlet`類別提供處理HTTP要求的`doGet`方法。 此方法會判斷與呼叫相關聯的資源、從存放庫擷取資源屬性，並將它們儲存在[ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html)物件中。

`ImageReferenceModificationServlet`類別會覆寫`createLayer`方法，並實作決定要轉譯之影像資源的邏輯。 方法會擷取頁面`jcr:content`節點（名為`image`）的子節點。 從此`image`節點建立[影像](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/Image.html)物件，且`getFileReference`方法會從影像節點的`fileReference`屬性傳回影像檔案的路徑。

>[!NOTE]
>[com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html)類別提供getFileReferencemethod。
>

## 開發流動網格 {#developing-a-fluid-grid}

AEM可讓您有效率且有效地實作流動網格。 此頁面說明如何將流動網格或現有的網格實作(例如[Bootstrap](https://github.com/topics/twitter-bootstrap?l=css))整合到您的AEM應用程式中。

如果您不熟悉流動網格，請參閱本頁底部的[流動網格簡介](/help/sites-developing/responsive.md#developing-a-fluid-grid)一節。 此簡介提供流動格點的概觀及其設計手冊。

### 使用Page元件定義網格 {#defining-the-grid-using-a-page-component}

使用頁面元件來產生定義頁面內容區塊的HTML元素。 頁面參考的ClientLibraryFolder提供可控制內容區塊版面的CSS：

* 頁面元件：新增代表內容區塊列的div元素。 代表內容區塊的div元素包含parsys元件，可供作者新增內容。
* 使用者端程式庫資料夾：提供CSS檔案，其中包含媒體查詢和div元素的樣式。

例如，範例geometrixx-media應用程式包含media-home元件。 此頁面元件插入兩個指令碼，產生類別`row-fluid`的兩個`div`元素：

* 第一列包含類別`span12`的`div`專案（內容跨越12欄）。 `div`元素包含parsys元件。

* 第二列包含兩個`div`元素，其中一個是類別`span8`，另一個是類別`span4`。 每個`div`元素都包含parsys元件。

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>當元件包含參照parsys元件的多個`cq:include`元素時，每個`path`屬性都必須有不同的值。
>

#### 縮放頁面元件格線 {#scaling-the-page-component-grid}

與geometrixx-media頁面元件(`/etc/designs/geometrixx-media`)關聯的設計包含`clientlibs` ClientLibraryFolder。 此ClientLibraryFolder定義屬於`row-fluid`類別之子系的`row-fluid`類別、`span*`類別和`span*`類別的CSS樣式。 媒體查詢可讓樣式針對不同的檢視區大小重新定義。

以下範例CSS是這些樣式的子集。 此子集主要針對`span12`、`span8`和`span4`類別，以及兩個檢視區大小的媒體查詢。 請注意CSS的下列特性：

* `.span`樣式使用絕對數字定義元素寬度。
* `.row-fluid .span*`樣式會將元素寬度定義為父項的百分比。 百分比是以絕對寬度計算。
* 較大檢視區的媒體查詢會指派較大的絕對寬度。

>[!NOTE]
>
>Geometrixx Media範例將[Bootstrap](https://getbootstrap.com/2.0.2/) JavaScript架構整合到其Fluid Grid實作中。 Bootstrap架構提供bootstrap.css檔案。

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### 在頁面元件格線中重新定位內容 {#repositioning-content-in-the-page-component-grid}

範例Geometrixx Media應用程式的頁面會在寬檢視區中水準分佈內容區塊列。 在較小的檢視區中，相同的區塊會垂直分佈。 以下範例CSS顯示為media-home頁面元件產生的HTML程式碼實施此行為的樣式：

* Media-welcome頁面的預設CSS會為`row-fluid`類別內的`span*`類別指派`float:left`樣式。

* 較小檢視區的媒體查詢會為相同類別指派`float:none`樣式。

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### 將頁面元件模組化 {#tip-modularize-your-page-components}

將元件模組化，以便有效使用程式碼。 您的網站可能會使用數種不同型別的頁面，例如歡迎頁面、文章頁面或產品頁面。 每種型別的頁面包含不同型別的內容，且可能會使用不同的版面。 不過，當每個版面的某些元素在多個頁面中很通用時，您可以重複使用實作該版面部分的程式碼。

**使用頁面元件覆蓋**

建立主要頁面元件，該元件提供用於產生頁面各個部分的指令碼，例如`head`和`body`區段，以及內文中的`header`、`content`和`footer`區段。

建立使用首頁面元件做為`cq:resourceSuperType`的其他頁面元件。 這些元件包括視需要覆寫首頁面指令碼的指令碼。

例如，goemetrixx-media應用程式包含頁面元件（`sling:resourceSuperType`是基礎頁面元件）。 數個子元件（例如article、category和media-home）會使用此頁面元件做為`sling:resourceSuperType`。 每個子元件都包含content.jsp檔案，此檔案會覆寫頁面元件的content.jsp檔案。

**重複使用指令碼**

建立多個JSP命令檔，以產生多個頁面元件通用的列和欄組合。 例如，文章的`content.jsp`指令碼和media-home元件都參考`8x4col.jsp`指令碼。

**依目標檢視區大小組織CSS樣式**

在個別檔案中包含不同檢視區大小的CSS樣式和媒體查詢。 使用使用者端資源庫資料夾來串連它們。

### 將元件插入頁面格線 {#inserting-components-into-the-page-grid}

當元件產生單一內容區塊時，通常頁面元件建立的格線會控制內容的放置。

身為作者，內容區塊可以各種大小和相對位置轉譯。 內容文字不應使用相對方向來參照其他內容區塊。

如有必要，元件應提供其產生的HTML程式碼所需的任何CSS或JavaScript程式庫。 在元件內使用使用者端程式庫資料夾，以產生CSS和JS檔案。 若要公開檔案，請[建立相依性或將資料庫](/help/sites-developing/clientlibs.md#creating-client-library-folders)內嵌在/etc資料夾下的另一個使用者端資料庫資料夾中。

**子網格**

如果元件包含多個內容區塊，請在列中新增內容區塊，以在頁面上建立子格線：

* 使用與容納頁面元件相同的類別名稱，以便您可以將div元素表示為列和內容區塊。
* 若要覆寫頁面設計之CSS實作的行為，請為row div元素使用第二個類別名稱，並在使用者端程式庫資料夾中提供關聯的CSS。

例如，`/apps/geometrixx-media/components/2-col-article-summary`元件會產生兩欄內容。 它產生的HTML具有以下結構：

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

頁面CSS的`.row-fluid .span6`選取器套用至此HTML中相同類別和結構的`div`元素。 不過，元件也包含/apps/geometrixx-media/components/2-col-article-summary/clientlibs使用者端程式庫資料夾：

* CSS使用與頁面元件相同的媒體查詢，以相同的分散頁面寬度建立版面變更。
* 選取器使用列`div`元素的`multi-col-article-summary`類別來覆寫頁面`row-fluid`類別的行為。

例如，`/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css`檔案中包含下列樣式：

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## 流動格線簡介 {#introduction-to-fluid-grids}

流動格點可讓頁面版面配置適應使用者端檢視區的尺寸。 網格由邏輯欄和列組成，這些欄和列在頁面上放置內容區塊。

* 欄決定內容區塊的水平位置和寬度。
* 列決定內容區塊的相對垂直位置。

使用HTML5技術，您可以實作格線並加以操控，讓頁面配置適應不同的檢視區大小：

* HTML`div`元素包含跨越某些欄的內容區塊。
* 當這些div元素中的一個或多個共用共同的父項div元素時，它們會組成一列。

### 使用獨立寬度 {#using-discrete-widths}

針對您定位的每個檢視區寬度範圍，請使用靜態頁面寬度和固定寬度的內容區塊。 手動調整瀏覽器視窗大小時，內容大小的變更會在分散的視窗寬度（也稱為中斷點）發生。 因此，頁面設計會更緊密地粘著，最大化使用者體驗。

#### 縮放格線 {#scaling-the-grid}

使用格點來縮放內容區塊，以因應不同的檢視區大小。 內容區塊跨越特定數量的欄。 當欄寬增加或減少以符合不同的檢視區大小時，內容區塊的寬度也會相應地增加或減少。 縮放可支援寬到足以容納內容區塊並排放置的大中型檢視區。

![兩個格點的影像，其中一個的縮放比例小於另一個。](do-not-localize/chlimage_1-1a.png)

#### 在格線中重新定位內容 {#repositioning-content-in-the-grid}

內容區塊的大小可由最小寬度限制，超出此寬度限制後，縮放便不再有效。 對於較小的檢視區，格點可用於垂直分配內容區塊，而非水準分配。

![兩個格點的影像，其中一個格點的重新定位位置小於另一個。](do-not-localize/chlimage_1-2a.png)

### 設計格線 {#designing-the-grid}

決定必須在頁面上放置內容區塊的欄和列。 您的頁面配置會決定跨越網格的欄和列數。

**欄數**

包含足夠的欄，以水準地放置所有版面中的內容區塊（針對所有檢視區大小）。 使用的欄數超過目前所需的數目，因此您可以因應未來的頁面設計。

**列內容**

使用列來控制內容區塊的垂直位置。 決定共用相同列的內容區塊：

* 在任何版面配置中彼此水準相鄰的內容區塊位於同一列。
* 水準（較寬的檢視區）和垂直（較小的檢視區）彼此相鄰的內容區塊位於同一列。

### 格線實施 {#grid-implementations}

建立CSS類別和樣式，讓您能夠控制頁面上內容區塊的版面。 頁面設計通常是根據檢視區內內容區塊的相對大小和位置而定。 檢視區決定內容區塊的實際大小。 您的CSS必須考慮相對和絕對大小。 您可以使用三種型別的CSS類別來實作流動網格：

* `div`元素的類別，是所有資料列的容器。 此類別會設定格線的絕對寬度。
* 代表資料列之`div`元素的類別。 此類別控制其包含的內容區塊的水平或垂直位置。
* 代表不同寬度內容區塊的`div`元素類別。 寬度以父項（列）的百分比表示。

目標檢視區寬度（及其相關媒體查詢）會區分用於版面配置的離散寬度。

#### 內容區塊寬度 {#widths-of-content-blocks}

一般而言，內容區塊類別的`width`樣式是根據您的頁面和格線的下列特性：

* 您用於每個目標檢視區大小的絕對頁面寬度。 已知值。
* 每個頁面寬度之格線欄的絕對寬度。 您可以決定這些值。
* 每一欄的相對寬度，以總頁面寬度的百分比表示。 您會計算這些值。

CSS包含一系列使用下列結構的媒體查詢：

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

使用以下演演算法作為開發頁面的元素類別和CSS樣式的起點。

1. 定義包含所有資料列之div專案的類別名稱，例如`content.`
1. 為代表資料列的div元素（例如`row-fluid`）定義CSS類別。
1. 定義內容區塊元素的類別名稱。 所有可能的寬度都需要類別（以欄跨度為單位）。 例如，對跨越三欄的`div`個元素使用`span3`類別，對跨越四欄的元素使用`span4`類別。 定義格線中欄的類別數。

1. 針對您定位的每個檢視區大小，新增對應的媒體查詢至CSS檔案。 在每個媒體查詢中新增下列專案：

   * `content`類別的選取器，例如`.content{}`。
   * 每個範圍類別的選取器，例如`.span3{ }`。
   * `row-fluid`類別的選取器，例如`.row-fluid{ }`
   * 位於資料列流動類別內部的跨度類別選取器，例如`.row-fluid span3 { }`。

1. 為每個選取器新增寬度樣式：

   1. 將`content`選取器的寬度設定為頁面的絕對大小，例如`width:480px`。
   1. 將所有資料列流動選取器的寬度設定為100%。
   1. 將所有範圍選取器的寬度設定為內容區塊的絕對寬度。 平凡的格線使用相同寬度的平均分配資料行： `(absolute width of page)/(number of columns)`。
   1. 將`.row-fluid .span`選取器的寬度設定為總寬度的百分比。 使用`(absolute span width)/(absolute page width)*100`公式計算此寬度。

#### 將內容區塊放置在列中 {#positioning-content-blocks-in-rows}

使用`.row-fluid`類別的浮點樣式，以便您可以控制列中的內容區塊是水準還是垂直排列。

* `float:left`或`float:right`樣式造成子專案（內容區塊）的水準分佈。

* `float:none`樣式造成子元素的垂直分佈。

將樣式新增至每個媒體查詢內的`.row-fluid`選取器。 根據您用於該媒體查詢的頁面版面配置設定值。 例如，下圖說明為寬檢視區水準分佈內容，為窄檢視區垂直分佈內容的列。

![一列中有兩個內容區塊的影像，第二個影像顯示該列已重新定位。](do-not-localize/chlimage_1-3a.png)

下列CSS可以實作此行為：

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### 將類別指派給內容區塊 {#assigning-classes-to-content-blocks}

針對您定位的每個檢視區大小的頁面配置，決定每個內容區塊所跨越的欄數。 然後，決定要將哪個類別用於這些內容區塊的div元素。

建立div類別後，您可以使用AEM應用程式實作網格。
