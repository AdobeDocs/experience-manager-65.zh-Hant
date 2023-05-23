---
title: 網頁響應性設計
seo-title: Responsive design for web pages
description: 通過響應性設計，可以在多個設備上以多個方向有效地顯示相同的頁面
seo-description: With responsive design, the same pages can be effectively displayed on multiple devices in multiple orientations
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '5336'
ht-degree: 0%

---

# 網頁響應性設計{#responsive-design-for-web-pages}

>[!NOTE]
>
>Adobe建議對SPA需要基於單頁應用程式框架的客戶端呈現的項目使用編輯器(如 _反應_)。 [深入了解](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>各種示例都基於Geometrixx樣本內容，該內容不再隨(AEMAdobe Experience Manager)一起提供，而We.Retail已取而代之。 查看文檔 [We.Retail Reference實施](/help/sites-developing/we-retail.md#we-retail-geometrixx) 下載和安裝Geometrixx。

設計網頁，使其適應顯示網頁的客戶端視圖。 通過響應設計，在兩個方向上的多個設備上可以有效地顯示相同的頁面。 下圖演示了頁面響應視區大小變化的一些方法：

* 佈局：對較小的視區使用單列佈局，對較大的視區使用多列佈局。
* 文本大小：在較大的視區中使用較大的文本大小（如適當時，如標題）。
* 內容：在較小的設備上顯示時，僅包括最重要的內容。
* 導航：提供了用於訪問其它頁面的設備特定工具。
* 影像：正在提供適合客戶端視區的影像格式副本。 根據窗口尺寸。

![chlimage_1-4](assets/chlimage_1-4a.png)

開發Adobe Experience Manager(AEM)應用程式，生成適應多個窗口大小和方向的HTML5頁。 例如，以下視區寬度範圍對應於各種設備類型和方向

* 最大寬度為480像素（電話、縱向）
* 最大寬度為767像素（電話、橫向）
* 768像素和979像素之間的寬度（平板、縱向）
* 寬度介於980像素和1199像素之間（平板、橫向）
* 寬度為1200像素或更大（台式機）

有關實施響應性設計行為的資訊，請參閱以下主題：

* [媒體查詢](/help/sites-developing/responsive.md#using-media-queries)
* [流體網格](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [自適應影像](/help/sites-developing/responsive.md#using-adaptive-images)

在設計時，使用 **[!UICONTROL 側腳]** 預覽不同螢幕大小的頁面。

## 在你發展之前 {#before-you-develop}

在開發支AEM持網頁的應用程式之前，應作出若干設計決定。 例如，您必須具有以下資訊：

* 您所針對的設備。
* 目標視區大小。
* 每個目標視區大小的頁面佈局。

### 應用程式結構 {#application-structure}

典型的應AEM用程式結構支援所有響應性設計實現：

* 頁面元件位於/apps/下&#x200B;*應用程式名*/元件
* 模板位於/apps/下&#x200B;*應用程式名*/模板
* 設計位於/etc/designs下

## 使用媒體查詢 {#using-media-queries}

媒體查詢允許選擇性使用CSS樣式進行頁面呈現。 開發工AEM具和功能使您能夠高效地在應用程式中實施介質查詢。

W3C組提供 [媒體查詢](https://www.w3.org/TR/mediaqueries-3/) 描述此CSS3功能和語法的建議。

### 建立CSS檔案 {#creating-the-css-file}

在CSS檔案中，根據所針對設備的屬性定義媒體查詢。 以下實施策略對於管理每個媒體查詢的樣式是有效的：

* 使用ClientLibraryFolder定義呈現頁面時組裝的CSS。
* 在單獨的CSS檔案中定義每個媒體查詢和關聯樣式。 使用表示媒體查詢的設備功能的檔案名非常有用。
* 在單獨的CSS檔案中定義所有設備通用的樣式。
* 在ClientLibraryFolder的css.txt檔案中，按照組裝的CSS檔案中的要求對清單CSS檔案進行排序。

的 `We.Retail` 媒體示例使用此策略在網站設計中定義樣式。 使用的CSS檔案 `We.Retail` 在 `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`。

下表列出了css子資料夾中的檔案。

<table>
 <tbody>
  <tr>
   <th>檔案名</th>
   <th>說明</th>
   <th>媒體查詢</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>常用樣式。</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>常用樣式，由TwitterBootstrap定義。</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>寬或寬為1200像素的所有介質的樣式。</td>
   <td><p>@media(最小寬度：1200像素){<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>介質的樣式，介於980像素和1199像素之間。</td>
   <td><p>@media(最小寬度：980像素)和(最大寬度：1199像素){<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>介質的樣式，介於768像素和979像素之間。 </td>
   <td><p>@media(最小寬度：768像素)和(最大寬度：979像素){<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>寬度小於768像素的所有媒體的樣式。</td>
   <td><p>@media(最大寬度：767像素){<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>寬度小於481像素的所有媒體的樣式。</td>
   <td>@media(最大寬度：480像素){<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

中的css.txt檔案 `/etc/designs/weretail/clientlibs` 資料夾列出了客戶端庫資料夾包含的CSS檔案。 檔案的順序實現樣式優先。 隨著設備大小的減小，樣式會更加具體。

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

**提示**:描述性檔案名使您可以輕鬆確定目標視區大小。

### 將媒體查詢與頁AEM面一起使用 {#using-media-queries-with-aem-pages}

在頁面元件的JSP指令碼中包括客戶端庫資料夾。 這樣做有助於生成包含媒體查詢的CSS檔案並引用該檔案。

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>的 `apps.weretail.all` 客戶端庫資料夾嵌入客戶端庫。

JSP指令碼生成引用樣式表的以下HTML代碼：

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## 預覽特定設備 {#previewing-for-specific-devices}

以不同視區大小查看頁面的預覽，以便可以test響應設計的行為。 在 **[!UICONTROL 預覽]** 模式， **[!UICONTROL 側腳]** 包括 **[!UICONTROL 設備]** 用於選擇設備的下拉菜單。 選擇設備時，頁面會更改以適應視區大小。

![chlimage_1-5](assets/chlimage_1-5a.png)

在中啟用設備預覽 **[!UICONTROL 側腳]**，必須配置頁面和 **[!UICONTROL MobileEmulator提供程式]** 服務。 另一個頁面配置控制顯示在 **[!UICONTROL 設備]** 清單框。

### 添加設備清單 {#adding-the-devices-list}

的 **[!UICONTROL 設備]** 清單 **[!UICONTROL 側腳]** 當您的頁面包含呈現 **[!UICONTROL 設備]** 清單框。 添加 **[!UICONTROL 設備]** 清單 **[!UICONTROL 側腳]**，包括 `/libs/wcm/mobile/components/simulator/simulator.jsp` 指令碼 `head` 的子菜單。

在JSP中包括以下代碼，該代碼定義 `head` 部分：

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

要查看示例，請開啟 `/apps/weretail/components/page/head.jsp` 的子菜單。

### 註冊頁面元件以進行模擬 {#registering-page-components-for-simulation}

要啟用設備模擬器以支援您的頁面，請使用MobileEmulatorProvider工廠服務註冊您的頁面元件並定義 `mobile.resourceTypes` 屬性。

使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。

例如，要建立 ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` 在應用程式中的節點：

* 父資料夾： `/apps/application_name/config`
* 名稱: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   - `*alias*` 需要尾碼，因為MobileEmulatorProvider服務是出廠服務。 使用此工廠唯一的別名。

* jcr:primaryType: `sling:OsgiConfig`

添加以下節點屬性：

* 名稱: `mobile.resourceTypes`
* 類型: `String[]`
* 值：呈現網頁的頁面元件的路徑。 例如，geometrixx-media應用使用以下值：

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### 指定設備組 {#specifying-the-device-groups}

要指定「設備」清單中顯示的設備組，請添加 `cq:deviceGroups` 屬性 `jcr:content` 的子目錄。 屬性值是到設備組節點的路徑陣列。

設備組節點位於 `/etc/mobile/groups` 的子菜單。

例如，Geometrixx Media站點的根頁面是 `/content/geometrixx-media`。 的 `/content/geometrixx-media/jcr:content` node包含以下屬性：

* 名稱: `cq:deviceGroups`
* 類型: `String[]`
* 值: `/etc/mobile/groups/responsive`

使用「工具」控制台 [建立和編輯設備組](/help/sites-developing/groupfilters.md)。

>[!NOTE]
>
>對於用於響應設計的設備組，請編輯設備組，並在「常規」頁籤上選擇「禁用模擬器」。 此選項可防止模擬器旋轉盤出現，這與響應設計無關。

## 使用自適應影像 {#using-adaptive-images}

可以使用媒體查詢來選擇要在頁面中顯示的影像資源。 但是，使用媒體查詢條件化其使用的每個資源都會下載到客戶端。 媒體查詢僅確定是否顯示下載的資源。

對於大型資源（如映像），下載所有資源並不是對客戶端資料管道的有效使用。 要有選擇地下載資源，請在媒體查詢執行選擇後使用JavaScript啟動資源請求。

以下策略載入使用媒體查詢選擇的單個資源：

1. 為資源的每個版本添加DIV元素。 將資源的URI作為屬性值包含。 瀏覽器不會將屬性解釋為資源。
1. 將媒體查詢添加到每個適合該資源的DIV元素。
1. 當載入文檔或調整窗口大小時，JavaScript代碼test每個DIV元素的媒體查詢。
1. 根據查詢結果，確定要包括的資源。
1. 在引用資源的DOM中插入HTML元素。

### 使用JavaScript評估媒體查詢 {#evaluating-media-queries-using-javascript}

Oracle的 [MediaQueryList介面](https://drafts.csswg.org/cssom-view/#the-mediaquerylist-interface) W3C定義的媒體查詢。 您可以將邏輯應用到媒體查詢結果並執行針對當前窗口的指令碼：

* 實現MediaQueryList介面的瀏覽器支援 `window.matchMedia()` 的子菜單。 此函式test給定字串的媒體查詢。 函式返回 `MediaQueryList` 提供對查詢結果訪問的對象。

* 對於不實現該介面的瀏覽器，可以使用 `matchMedia()` 聚合填充，如 [matchMedia.js](https://github.com/paulirish/matchMedia.js)，可自由使用的JavaScript庫。

#### 選擇媒體特定資源 {#selecting-media-specific-resources}

W3C [畫素](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element) 使用媒體查詢確定用於影像元素的源。 圖片元素使用元素屬性將媒體查詢與影像路徑相關聯。

免費 [picturefild.js庫](https://github.com/scottjehl/picturefill) 提供與建議的類似功能 `picture` 元素，並使用類似的策略。 picturemild.js庫調用 `window.matchMedia` 評估為一組 `div` 元素。 每個 `div` 元素還指定影像源。 源在媒體查詢 `div` 元素返回 `true`。

的 `picturefill.js` 庫需要與以下示例類似的HTML代碼：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

在呈現頁面時， picturefull.js插入 `img` 元素作為 `<div data-picture>` 元素：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

在頁AEM面中， `data-src` attribute是儲存庫中資源的路徑。

### 在中實現自適應圖AEM像 {#implementing-adaptive-images-in-aem}

要在應用程式中實AEM現自適應影像，必須添加所需的JavaScript庫，並在頁面中包括所需的HTML標籤。

**資料庫**

獲取以下JavaScript庫並將其包含在客戶端庫資料夾中：

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) （對於不實現MediaQueryList介面的瀏覽器）
* [picturefild.js](https://github.com/scottjehl/picturefill)
* jquery.js(通過 `/etc/clientlibs/granite/jquery` 客戶端庫資料夾（類別= jquery）
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) （在調整窗口大小後發生一次的jquery事件）

**提示：** 可以通過 [嵌入](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)。

**HTML**

建立生成picturemild.js代碼所需的div元素的元件。 在頁AEM中， data-src屬性的值是儲存庫中資源的路徑。 例如，頁面元件可以硬編碼媒體查詢和DAM中影像格式副本的相關路徑。 或者，建立一個自定義影像元件，使作者能夠選擇影像格式副本或指定運行時呈現選項。

下面的示例HTML從同一影像的兩個DAM格式副本中選擇。

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>自適應影像基礎元件實現自適應影像：
>
>* 客戶端庫資料夾： `/libs/foundation/components/adaptiveimage/clientlibs`
>* 生成HTML的指令碼： `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>後續部分提供了有關此元件的詳細資訊。

### 瞭解影像呈AEM現 {#understanding-image-rendering-in-aem}

要自定義影像呈現，您應瞭解預設的靜態AEM影像呈現實現。 提AEM供Image元件和影像呈現Servlet，它們可一起為網頁呈現影像。 當Image元件包含在頁面的段落系統中時，將發生以下事件序列：

1. 創作：作者編輯影像元件以指定要包括在HTML頁中的影像檔案。 檔案路徑儲存為Image元件節點的屬性值。
1. 頁面請求：頁面元件的JSP生成HTML代碼。 「影像」元件的JSP將生成一個img元素並將其添加到頁面。
1. 映像請求：Web瀏覽器載入頁面，並根據img元素的src屬性請求影像。
1. 影像呈現：影像呈現Servlet將影像返回到Web瀏覽器。

![chlimage_1-6](assets/chlimage_1-6a.png)

例如，Image元件的JSP將生成以下HTML元素：

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

當瀏覽器載入頁面時，它會使用src屬性的值作為URL來請求影像。 Sling分解URL:

* 資源: `/content/mywebsite/en/_jcr_content/par/image_0`
* 檔案副檔名： `.jpg`
* 選擇器: `img`
* 字尾: `1358372073597.jpg`

的 `image_0` 節點具有 `jcr:resourceType` 值 `foundation/components/image`，其中 `sling:resourceSuperType` 值 `foundation/components/parbase`。 parbase元件包括img.GET.java指令碼，該指令碼與選擇器和請求URL的檔案副檔名相匹配。 CQ使用此指令碼(servlet)來呈現影像。

要查看指令碼的原始碼，請使用CRXDE Lite開啟 `/libs/foundation/components/parbase/img.GET.java`
的子菜單。

## 縮放當前視區大小的影像 {#scaling-images-for-the-current-viewport-size}

根據客戶端視區的特性在運行時縮放影像以提供符合響應設計原則的影像。 使用與靜態影像呈現相同的設計模式，使用servlet和創作元件。

元件必須執行以下任務：

* 將映像資源的路徑和所需維度儲存為屬性值。
* 生成 `div` 包含用於呈現影像的媒體選擇器和服務調用的元素。

>[!NOTE]
>
>Web客戶端使用matchMedia和Picturefill JavaScript庫（或類似的庫）來評估媒體選擇器。

處理映像請求的Servlet必須執行以下任務：

* 從元件屬性中檢索影像的路徑和尺寸。
* 根據屬性縮放影像並返回影像。

**可用解決方案**

安AEM裝以下可使用或擴展的實現。

* 生成媒體查詢的Adaptive Image Foundation元件，以及對縮放影像的Adaptive Image Component Servlet的HTTP請求。
* Commons軟體包安裝改變影像解析度的Image Reference Modification Servlet示例Servlet。

### 瞭解自適應影像元件 {#understanding-the-adaptive-image-component}

自適應影像元件生成對自適應影像元件Servlet的調用，以呈現根據設備螢幕調整大小的影像。 該元件包括以下資源：

* JSP:添加將媒體查詢與對Adaptive Image Component Servlet的調用關聯的div元素。
* 客戶端庫：客戶端資料夾是 `cq:ClientLibraryFolder` 組合matchMedia聚合填充JavaScript庫和修改的Picturelink JavaScript庫的。
* 編輯對話框：的 `cq:editConfig` 節點覆蓋CQ基礎影像元件，以便刪除目標建立自適應影像元件而不是基礎影像元件。

#### 添加DIV元素 {#adding-the-div-elements}

adaptive-image.jsp指令碼包含以下代碼，用於生成div元素和媒體查詢：

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

的 `path` 變數包含當前資源（自適應映像元件節點）的路徑。 代碼生成一系列 `div` 具有以下結構的元素：

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

的值 `data-scr` attribute是一個URL,Sling解析為呈現影像的自適應影像元件Servlet。 資料 — 媒體屬性包含根據客戶端屬性計算的媒體查詢。

以下HTML代碼是 `div` JSP生成的元素：

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### 更改影像大小選擇器 {#changing-the-image-size-selectors}

如果自定義自適應影像元件並更改寬度選擇器，則還必須配置自適應影像元件Servlet以支援寬度。

### 瞭解自適應映像元件Servlet {#understanding-the-adaptive-image-component-servlet}

自適應影像元件Servlet根據指定的寬度調整JPEG影像的大小，並設定JPEG質量。

#### 自適應影像元件Servlet的介面 {#the-interface-of-the-adaptive-image-component-servlet}

自適應影像元件Servlet綁定到預設的Sling Servlet，並支援.jpg、.jpeg、.gif和.png檔案副檔名。 servlet選擇器為img。

>[!CAUTION]
>
>對於自適應格式副本，不支AEM持動畫.gif檔案。

因此，Sling將以下格式的HTTP請求URL解析為此servlet:

`*path-to-node*.img.*extension*`

例如，Sling使用URL轉發HTTP請求 `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` 到自適應映像元件Servlet。

另外兩個選擇器指定請求的影像寬度和JPEG質量。 下面的示例請求寬度為480像素且中等質量的影像：

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**支援的映像屬性**

Servlet接受有限數量的影像寬度和質量。 預設情況下支援以下寬度（以像素為單位）:

* 完整
* 320
* 480
* 476
* 620

全值表示無縮放。

支援以下JPEG質量值：

* 低
* 中
* 高

數值分別為0.4、0.82和1.0。

**更改預設支援的寬度**

使用Web控制台([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))或sling:OsgiConfig節點，以配置Adobe CQ自適應映像元件Servlet的支援寬度。

有關如何配置服務的AEM資訊，請參見 [配置OSGi](/help/sites-deploying/configuring-osgi.md)。

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Web控制台</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>服務或節點名稱</th>
   <td>「配置」頁籤上的服務名是「Adobe CQ自適應映像元件Servlet」</td>
   <td>com.day.cq.wcm.foundation.impl。 AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>屬性</th>
   <td><p>支援的寬度</p>
    <ul>
     <li>要添加支援的寬度，請按一下+按鈕並輸入正整數。</li>
     <li>要刪除支援的寬度，請按一下關聯的 — 按鈕。</li>
     <li>要修改支援的寬度，請編輯欄位值。</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>該屬性是多值字串值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 實施詳細資訊 {#implementation-details}

的 `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` 類擴展 [摘要ImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 類。 AdaptiveImageComponentServlet原始碼位於 `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` 的子菜單。

類使用Felix SCR注釋來配置Servlet所關聯的資源類型和檔案副檔名以及第一個選擇器的名稱。

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

Servlet使用屬性SCR注釋來設定預設支援的影像質量和尺寸。

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

的 `AbstractImageServlet` 類提供 `doGet` 處理HTTP請求的方法。 此方法確定與請求關聯的資源，從儲存庫中檢索資源屬性，並在 [影像上下文](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 的雙曲餘切值。

>[!NOTE]
>
>的 [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) 類提供 `getFileReference method`，檢索資源的 `fileReference` 屬性。

的 `AdaptiveImageComponentServlet` 類覆蓋 `createLayer` 的雙曲餘切值。 該方法從影像資源獲取路徑和請求的影像寬度 `ImageContext` 的雙曲餘切值。 然後，它調用 `info.geometrixx.commons.impl.AdaptiveImageHelper` 類，執行實際影像縮放。

AdaptiveImageComponentServlet類也會覆蓋writeLayer方法。 該方法將JPEG質量應用於影像。

### 影像引用修改Servlet(常用Geometrixx) {#image-reference-modification-servlet-geometrixx-common}

示例「影像參照修改Servlet」為img元素生成尺寸屬性，以在網頁上縮放影像。

#### 調用Servlet {#calling-the-servlet}

Servlet已綁定到 `cq:page` 支援.jpg檔案副檔名。 Servlet選擇器為 `image`。 因此，Sling將以下格式的HTTP請求URL解析為此servlet:

`path-to-page-node.image.jpg`

例如，Sling使用URL轉發HTTP請求 `http://localhost:4502/content/geometrixx/en.image.jpg` 到映像引用修改Servlet。

另外三個選擇器指定所請求的影像寬度、高度和（可選）質量。 下面的示例請求寬度為770像素、高度為360像素和中等質量的影像。

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**支援的映像屬性**

Servlet接受有限數量的影像尺寸和質量值。

預設情況下支援以下值(widthxheight):

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

支援以下影像質量值：

* 低
* 中
* 高

使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。

#### 指定映像資源 {#specifying-the-image-resource}

映像路徑、維度和質量值必須儲存為儲存庫中節點的屬性：

* 節點名稱為 `image`。
* 父節點是 `jcr:content` 節點 `cq:page` 資源。

* 影像路徑儲存為名為 `fileReference`。

創作頁面時，使用 **側腳** 指定影像並添加 `image` 節點到頁面屬性：

1. 在 **側腳**，按一下 **頁面** ，然後按一下 **頁面屬性**。
1. 按一下 **影像** 的子菜單。
1. 按一下&#x200B;**「確定」**。

#### 實施詳細資訊 {#implementation-details-1}

info.geometrixx.commons.impl.servlet.ImageReferenceModificationServlet類擴展了 [摘要ImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 類。 如果安裝了cq-geometrixx-commons-pkg軟體包，則ImageReferenceModificationServlet原始碼位於 `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` 的子菜單。

類使用Felix SCR注釋來配置Servlet所關聯的資源類型和檔案副檔名以及第一個選擇器的名稱。

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

Servlet使用屬性SCR注釋來設定預設支援的影像質量和尺寸。

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

的 `AbstractImageServlet` 類提供 `doGet` 處理HTTP請求的方法。 此方法確定與調用關聯的資源，從儲存庫中檢索資源屬性，並將它們保存在 [影像上下文](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 的雙曲餘切值。

的 `ImageReferenceModificationServlet` 類覆蓋 `createLayer` 實現確定要呈現的影像資源的邏輯。 該方法檢索頁的子節點 `jcr:content` 節點命名 `image`。 安 [影像](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/Image.html) 從此建立對象 `image` 節點和 `getFileReference` 方法從 `fileReference` 影像節點的屬性。

>[!NOTE]
>的 [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) 類提供getFileReference方法。

## 開發流體格柵 {#developing-a-fluid-grid}

使您AEM能夠高效地實施流體網格。 本頁介紹如何整合流體網格或現有網格實現(如 [Bootstrap](https://github.com/topics/twitter-bootstrap?l=css))AEM。

如果您不熟悉流體網格，請參閱 [流體網格簡介](/help/sites-developing/responsive.md#developing-a-fluid-grid) 的子菜單。 本文對流體網格的設計作了概述和指導。

### 使用頁面元件定義網格 {#defining-the-grid-using-a-page-component}

使用頁面元件生成定義頁面內容塊的HTML元素。 頁面引用的ClientLibraryFolder提供控制內容塊佈局的CSS:

* 頁面元件：添加表示內容塊行的div元素。 表示內容塊的div元素包括作者添加內容的parsys元件。
* 客戶端庫資料夾：提供包含div元素的媒體查詢和樣式的CSS檔案。

例如，示例geometrixx-media應用程式套件含media-home元件。 此頁元件插入兩個指令碼，生成兩個 `div` 類元素 `row-fluid`:

* 第一行包含 `div` 類元素 `span12` （內容跨12列）。 的 `div` 元素包含parsys元件。

* 第二行包含兩個 `div` 元素，類之一 `span8` 和班上的其他人 `span4`。 每個 `div` 元素包括parsys元件。

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
>當元件包含多個 `cq:include` 參照parsys元件的元素，每個元素 `path` 屬性必須具有其他值。

#### 縮放頁面元件網格 {#scaling-the-page-component-grid}

與geometrix-media頁元件(`/etc/designs/geometrixx-media`)包含 `clientlibs` ClientLibraryFolder。 此ClientLibraryFolder為 `row-fluid` 類， `span*` 類和 `span*` 類是 `row-fluid` 類。 介質查詢可根據不同的視區大小重新定義樣式。

以下示例CSS是這些樣式的子集。 此子集側重於 `span12`。 `span8`, `span4` 類和介質查詢，以獲取兩個視區大小。 請注意CSS的以下特性：

* 的 `.span` 樣式使用絕對數字定義元素寬度。
* 的 `.row-fluid .span*` 樣式將元素寬度定義為父項的百分比。 百分比從絕對寬度計算。
* 對較大視區的媒體查詢會指定較大的絕對寬度。

>[!NOTE]
>
>Geometrixx Media示例整合 [Bootstrap](https://getbootstrap.com/2.0.2/) JavaScript框架中流體網格的實現。 Bootstrap框架提供bootstrap.css檔案。

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

#### 重新定位頁面元件網格中的內容 {#repositioning-content-in-the-page-component-grid}

示例Geometrixx Media應用程式的頁面在寬視區中水準分佈內容塊行。 在較小的視區中，相同的塊垂直分佈。 下面的示例CSS顯示了為媒體首頁元件生成的HTML代碼實現此行為的樣式：

* 「歡迎使用媒體」頁的預設CSS將 `float:left` 樣式 `span*` 內部類 `row-fluid` 類。

* 對較小視區的介質查詢分配 `float:none` 樣式。

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

#### 模組化頁面元件 {#tip-modularize-your-page-components}

將元件模組化，以便有效地使用代碼。 您的站點可能使用幾種不同類型的頁面，如歡迎頁、文章頁或產品頁。 每種類型的頁面都包含不同類型的內容，並且可能使用不同的佈局。 但是，當每個佈局的某些元素在多個頁面上是公用的時，您可以重新使用實現該佈局部分的代碼。

**使用頁面元件覆蓋**

建立首頁元件，該元件提供用於生成頁面各部分的指令碼，如 `head` 和 `body` 部分和 `header`。 `content`, `footer` 在身體內。

建立使用首頁元件作為 `cq:resourceSuperType`。 這些元件包括可根據需要覆蓋首頁指令碼的指令碼。

例如，goemetrix-media應用程式套件括頁面元件( `sling:resourceSuperType` 是基礎頁元件)。 幾個子元件（如文章、類別和媒體首頁）使用此頁面元件作為 `sling:resourceSuperType`。 每個子元件都包括一個content.jsp檔案，該檔案將覆蓋頁元件的content.jsp檔案。

**重用指令碼**

建立多個JSP指令碼，這些指令碼生成多個頁面元件通用的行和列組合。 例如， `content.jsp` 文章的指令碼和media-home元件都引用 `8x4col.jsp` 的下界。

**按目標視區大小組織CSS樣式**

在單獨的檔案中包括不同視區大小的CSS樣式和媒體查詢。 使用客戶端庫資料夾來連接它們。

### 將元件插入頁面網格 {#inserting-components-into-the-page-grid}

當元件生成單個內容塊時，通常頁面元件建立的網格控制內容的放置。

作為作者，內容塊可以以各種大小和相對位置呈現。 內容文本不應使用相對方向來引用其他內容塊。

如有必要，元件應提供其生成的HTML代碼所需的任何CSS或JavaScript庫。 使用元件內的客戶端庫資料夾，以便生成CSS和JS檔案。 要公開檔案， [建立依賴關係或嵌入庫](/help/sites-developing/clientlibs.md#creating-client-library-folders) 位於/etc資料夾下的另一個客戶端庫資料夾中。

**子網格**

如果元件包含多個內容塊，則在行內添加內容塊以在頁面上建立子網格：

* 使用與包含頁元件相同的類名，以便可以將div元素表示為行和內容塊。
* 要覆蓋頁面設計的CSS實現的行為，請為行div元素使用第二個類名，並在客戶端庫資料夾中提供關聯的CSS。

例如， `/apps/geometrixx-media/components/2-col-article-summary` 元件生成兩列內容。 它生成的HTML具有以下結構：

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

的 `.row-fluid .span6` 頁面的CSS的選擇器應用於 `div` 此HTML中相同類和結構的元素。 但是，該元件還包括/apps/geometrixx-media/components/2-col-article-summary/clientlibs客戶端庫資料夾：

* CSS使用與頁面元件相同的媒體查詢，以在相同的離散頁面寬度上建立佈局更改。
* 選擇器使用 `multi-col-article-summary` 行的類 `div` 要覆蓋頁面行為的元素 `row-fluid` 類。

例如，以下樣式包含在 `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` 檔案：

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

## 流體網格簡介 {#introduction-to-fluid-grids}

流體網格使頁面佈局能夠適應客戶端視區的尺寸。 網格由邏輯列和行組成，這些列和行將內容塊定位在頁面上。

* 列確定內容塊的水準位置和寬度。
* 行確定內容塊的相對垂直位置。

使用HTML5技術，您可以實施網格並操縱網格以適應不同視區大小的頁面佈局：

* HTML `div` 元素包含跨某些列的內容塊。
* 當這些div元素中的一個或多個元素共用公共父div元素時，它們包含一行。

### 使用離散寬度 {#using-discrete-widths}

對於要瞄準的每個視區寬度範圍，使用靜態頁寬和內容塊等寬。 手動調整瀏覽器窗口大小時，對內容大小的更改會在離散窗口寬度（也稱為斷點）處發生。 因此，頁面設計被更緊密地粘合，從而最大化用戶體驗。

#### 縮放網格 {#scaling-the-grid}

使用網格縮放內容塊以適應不同的視區大小。 內容塊跨過特定數目的列。 隨著列寬的增加或減小以適合不同的視口尺寸，內容塊的寬度相應地增加或減少。 縮放可支援大型和中型視區，這些視區的寬度足以容納內容塊的並排放置。

![](do-not-localize/chlimage_1-1a.png)

#### 重新定位網格中的內容 {#repositioning-content-in-the-grid}

內容塊的大小可以受最小寬度的限制，超過此寬度的縮放不再有效。 對於較小的視區，網格可用於垂直分佈內容塊，而不是水準分佈。

![](do-not-localize/chlimage_1-2a.png)

### 設計網格 {#designing-the-grid}

確定必須將內容塊放置在頁面上的列和行。 頁面佈局決定了跨網格的列和行數。

**列數**

包括足夠的列，以便對所有視區大小水準放置所有佈局中的內容塊。 使用的列數超過當前需要的列數，因此您可以適應將來的頁面設計。

**行內容**

使用行控制內容塊的垂直定位。 確定共用同一行的內容塊：

* 任何佈局中水準地彼此相鄰的內容塊位於同一行中。
* 水準（寬視區）和垂直（小視區）相鄰的內容塊位於同一行。

### 網格實現 {#grid-implementations}

建立CSS類和樣式，以便控制頁面上內容塊的佈局。 頁面設計通常基於視區內內容塊的相對大小和位置。 視區確定內容塊的實際大小。 CSS必須考慮相對大小和絕對大小。 可以使用三種類型的CSS類實現流體網格：

* 類 `div` 是所有行的容器的元素。 此類設定網格的絕對寬度。
* 類 `div` 表示行的元素。 此類控制其包含的內容塊的水準或垂直定位。
* 類 `div` 表示不同寬度的內容塊的元素。 寬度以父級（行）的百分比表示。

目標視區寬度（及其關聯的媒體查詢）標定了用於頁面佈局的離散寬度。

#### 內容塊的寬度 {#widths-of-content-blocks}

通常， `width` 內容塊類的樣式基於頁面和網格的以下特徵：

* 用於每個目標視區大小的絕對頁寬。 已知值。
* 每個頁寬的網格列的絕對寬度。 確定這些值。
* 每列的相對寬度佔總頁寬的百分比。 計算這些值。

CSS包括使用以下結構的一系列媒體查詢：

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

使用以下算法作為開發頁面的元素類和CSS樣式的起點。

1. 為包含所有行的div元素定義類名，例如 `content.`
1. 為表示行的div元素定義CSS類，如 `row-fluid`。
1. 定義內容塊元素的類名。 所有可能的寬度（以列跨度計算）都需要類。 例如，使用 `span3` 類 `div` 跨三列的元素，使用 `span4` 四個列的跨度的類。 定義網格中列的類數。

1. 對於您所瞄準的每個視區大小，將相應的媒體查詢添加到CSS檔案。 在每個介質查詢中添加以下項：

   * 選擇器 `content` 類，例如 `.content{}`。
   * 每個跨類的選擇器，例如 `.span3{ }`。
   * 選擇器 `row-fluid` 類，例如 `.row-fluid{ }`
   * 跨類的選擇器，例如，行流類內的類 `.row-fluid span3 { }`。

1. 為每個選擇器添加寬度樣式：

   1. 設定寬度 `content` 選擇器到頁面的絕對大小，例如 `width:480px`。
   1. 將所有行流體選擇器的寬度設定為100%。
   1. 將所有範圍選擇器的寬度設定為內容塊的絕對寬度。 普通網格使用相同寬度的均勻分佈列： `(absolute width of page)/(number of columns)`。
   1. 設定 `.row-fluid .span` 選擇器佔總寬度的百分比。 使用 `(absolute span width)/(absolute page width)*100` 公式。

#### 定位行中的內容塊 {#positioning-content-blocks-in-rows}

使用 `.row-fluid` 類，因此您可以控制行中的內容塊是水準排列還是垂直排列。

* 的 `float:left` 或 `float:right` 樣式導致子元素（內容塊）的水準分佈。

* 的 `float:none` 樣式導致子元素的垂直分佈。

將樣式添加到 `.row-fluid` 選擇器。 根據您用於該媒體查詢的頁面佈局設定值。 例如，下圖說明了一行，該行在寬視區中水準分佈內容，在窄視區中垂直分佈內容。

![](do-not-localize/chlimage_1-3a.png)

以下CSS可以實現此行為：

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

#### 為內容塊分配類 {#assigning-classes-to-content-blocks}

對於要定位的每個視區大小的頁面佈局，確定每個內容塊所跨越的列數。 然後，確定用於這些內容塊的div元素的類。

建立div類後，可以使用應用程式實AEM現網格。
