---
title: 擴充和設定登錄頁面的設計匯入工具
seo-title: Extending and Configuring the Design Importer for Landing Pages
description: 了解如何為登錄頁面設定設計匯入工具。
seo-description: Learn how to configure the Design Importer for landing pages.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3503'
ht-degree: 0%

---

# 擴充和設定登錄頁面的設計匯入工具{#extending-and-configuring-the-design-importer-for-landing-pages}

本節說明如何設定，並視需要為登錄頁面擴充設計匯入工具。 匯入後使用登錄頁面在 [登陸頁面。](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**讓設計匯入工具擷取自訂元件**

以下是讓設計匯入工具辨識自訂元件的邏輯步驟

1. 建立TagHandler

   * 標籤處理常式是POJO，可處理特定類型的HTML標籤。 您的TagHandler可以處理的「kind」HTML標籤是通過TagHandlerFactory的OSGi屬性「tagpattern.name」定義的。 此OSGi屬性實質上是規則運算式，應符合您要處理的輸入html標籤。 所有巢狀標籤都會擲回至您的標籤處理常式以進行處理。 例如，如果註冊包含巢狀的div &lt;p> 標籤， &lt;p> 標籤也會擲回至您的TagHandler，這取決於您要如何處理。
   * 標籤處理程式介麵類似於SAX內容處理程式介面。 它會收到每個html標籤的SAX事件。 作為標籤處理常式提供者，您需要實作某些生命週期方法，這些方法會由設計匯入工具架構自動呼叫。

1. 建立其對應的TagHandlerFactory。

   * 標籤處理常式工廠是OSGi元件（單例），負責產生標籤處理常式的例項。
   * 您的標籤處理常式工廠必須公開名為「tagpattern.name」的OSGi屬性，其值與輸入html標籤相符。
   * 如果有多個標籤處理常式與輸入html標籤相符，則會挑選排名較高的處理常式。 排名本身以OSGi屬性公開 **service.ranking**.
   * TagHandlerFactory是OSGi元件。 要提供給TagHandler的任何引用必須通過此工廠。

1. 如果您想要覆寫預設值，請確定您的TagHandlerFactory有更好的排名。

>[!CAUTION]
>
>設計匯入工具，用於匯入登錄頁面， [已於AEM 6.5中淘汰](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## 準備匯入HTML {#preparing-the-html-for-import}

建立匯入工具頁面後，您可以匯入完整的HTML登陸頁面。 若要匯入HTML登錄頁面，您必須先將其內容壓縮至設計套件中。 設計套件包含您的HTML登陸頁面以及參考的資產（影像、css、圖示、指令碼等）。

以下速查表提供了如何準備導入HTML的示例：

登錄頁面速查表

[取得檔案](assets/cheatsheet.zip)

### Zip檔案配置和需求 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>此時，ZIP檔案只能包含一個HTML頁面或一個頁面的一部分。

郵遞區號的範例配置如下：

* /index.html ->登錄頁面HTML檔案
* /css ->以新增至CSS clientlib
* /img ->所有影像和資產
* /js ->新增至JS clientlib

版面是以「HTML5模板最佳實務」版面為基礎。 如需詳細資訊，請參閱 [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>至少，設計包 **必須** 包含 **index.html** 檔案。 如果要匯入的登錄頁面也有行動版本，則郵遞區號必須包含 **mobile.index.html** 與 **index.html** 在根層級。

### 準備登錄頁面HTML {#preparing-the-landing-page-html}

若要匯入HTML，您需要將畫布div新增至登錄頁面HTML。

畫布div是html **div** with `id="cqcanvas"` 必須插入HTML `<body>` 標籤，必須包裝要用於轉換的內容。

新增畫布div後，登錄頁面HTML的範例片段如下：

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### 準備HTML以包含可編輯的AEM元件 {#preparing-the-html-to-include-editable-aem-components}

匯入登錄頁面時，您可以選擇依原樣匯入頁面，這表示匯入登錄頁面後，您無法編輯AEM中的任何匯入項目(您仍可在頁面上新增其他AEM元件)。

匯入登錄頁面之前，您可能想要轉換登錄頁面的某些部分，使其成為可編輯的AEM元件。 這可讓您在匯入登錄頁面設計後，快速編輯登錄頁面的部分。

若要這麼做，請新增 `data-cq-component` 至您匯入之HTML檔案中的適當元件。

以下章節說明如何編輯HTML檔案，以便將登錄頁面的某些部分轉換為不同可編輯的AEM元件。 如需詳細說明，請參閱 [登錄頁面元件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>HTML標籤可將登錄頁面的部分轉換為AEM元件，其格式長且標籤聲明簡短。 每個元件都會說明兩者。

### 限制 {#limitations}

匯入前，請注意下列限制：

### 不會保留在&amp;lt;body>標籤上應用的類或ID之類的屬性 {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

如果任何屬性（例如，ID或類別）已套用至Body標籤上 `<body id="container">` 則匯入後不會保留。 因此，所匯入的設計不應對套用於 `<body>` 標籤。

### 拖放zip {#drag-and-drop-zip}

Internet Explorer和Firefox 3.6版及舊版不支援拖放郵遞區號上傳。 若要在使用這些瀏覽器時上傳設計，請按一下拖放檔案區域以開啟檔案上傳對話方塊，然後使用該對話方塊上傳您的設計。

支援「拖放」設計zip的瀏覽器為Chrome、Safari5.x、Firefox 4及更新版本。

### 不支援現代化 {#modernizr-is-not-supported}

`Modernizr.js` 是以javascript為基礎的工具，可偵測瀏覽器的原生功能，並偵測它們是否適合html5元素。 使用Modernizr來增強舊版不同瀏覽器支援的設計，可能會在登錄頁面解決方案中造成匯入問題。 `Modernizr.js` 設計匯入工具不支援指令碼。

### 匯入設計套件時不會保留頁面屬性 {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

任何頁面屬性（例如自訂網域、強制HTTPS等） 在匯入設計套件之前為頁面設定（使用空白登陸頁面範本），在匯入設計後會遺失。 因此，建議的作法是在匯入設計套件後設定頁面屬性。

### 僅HTML標籤假設 {#html-only-markup-assumed}

在導入時，由於安全原因和為了避免導入和發佈無效標籤，對標籤進行清理。 這會假設僅HTML標籤，且將篩選掉所有其他形式的元素，例如內嵌SVG或Web元件。

### 文字 {#text}

HTML標籤以插入文本元件( `foundation/components/text`)(在設計套件中的HTML中：

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

在HTML中加入上述標籤，會執行下列操作：

* 建立可編輯的AEM文字元件( `sling:resourceType=foundation/components/text`)，在匯入設計套件後建立的登錄頁面中。
* 設定 `text` 已建立文本元件的屬性，包含在 `div`.

**速記元件標籤聲明**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**包含清單的文字**

要添加包含清單的文本，請執行以下操作：

* 第1
* 第2

可在RTE編輯器中編輯的檔案：

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**帶顏色的文本**

若要新增可在RTE編輯器中編輯的彩色（粉紅色）文字：

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### 標題 {#title}

HTML標籤以插入標題元件( `wcm/landingpage/components/title`)(在設計套件中的HTML中：

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

在HTML中加入上述標籤，會執行下列操作：

* 建立可編輯的AEM標題元件( `sling:resourceType=wcm/landingpage/components/title`)，在匯入設計套件後建立的登錄頁面中。
* 設定 `jcr:title` 已建立標題元件的屬性，以包住div的標題標籤內的文字。
* 設定 `type` 屬性至標題標籤中，在此例中為 `h1`.

標題元件支援7種類型 —  `h1, h2, h3, h4, h5, h6` 和 `default`.

**速記元件標籤聲明**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 影像 {#image}

HTML標籤，以在設計套件內的HTML中插入影像元件(foundation/components/image):

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

在HTML中加入上述標籤，會執行下列操作：

* 建立可編輯的AEM影像元件( `sling:resourceType=foundation/components/image`)，在匯入設計套件後建立的登錄頁面中。
* 設定 `fileReference` 已建立映像元件的屬性，指向在src屬性中指定的映像被導入的路徑。
* 設定 `alt` 屬性的值（在img標籤中）。
* 設定 `title` 屬性中的值。
* 設定 `width` 屬性中的width屬性值。
* 設定 `height` 屬性中的height屬性值。

**速記元件標籤聲明：**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### 影像元件Div內不支援絕對URL img src {#absolute-url-img-src-not-supported-within-image-component-div}

若 `<img>` 會嘗試對元件轉換使用絕對url src的標籤，適當 **UnsupportedTagContentException** 已引發。 例如，不支援下列項目：

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

但是，非影像元件div一部分的img標籤支援絕對URL影像。

### 行動要求元件 {#call-to-action-components}

您可以將要匯入的登錄頁面部分標示為「可編輯的動作呼叫元件」 — 這類匯入的動作呼叫元件，可在匯入登錄頁面後加以編輯。 AEM包含下列CTA元件：

* 點進連結 — 可讓您新增文字連結，當點按連結時，會將訪客帶往目標URL。
* 圖形連結 — 可讓您新增在點按時將訪客帶往目標URL的影像。

#### 點進連結 {#click-through-link}

此CTA元件可用來在登錄頁面上新增文字連結。

支援的屬性

* 標籤，帶粗體、斜體和下划線選項
* Target URL，支援第三方和AEM URL
* 頁面呈現選項（相同視窗、新視窗等）

HTML標籤，將點進元件包含在匯入的zip中。 此處href對應至目標url、「檢視產品詳細資料」對應至標籤等。

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

此元件可用於任何獨立應用程式，或可從zip匯入。

**速記元件標籤聲明**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### 圖形連結 {#graphical-link}

此CTA元件可用來新增任何圖形影像，其中包含登陸頁面上的連結。 影像可以是簡單按鈕或任何以圖形影像作為背景的影像。 點按影像時，會將使用者帶至元件屬性中指定的目標URL。 這是「行動呼籲」群組的一部分。

支援的屬性

* 影像裁切、旋轉
* 暫留文字、說明、像素大小
* Target URL，支援第三方和AEM URL
* 頁面呈現選項（相同視窗、新視窗等）

HTML標籤，在匯入的zip中包含圖形連結元件。 此處href將映射至目標url, img src將是呈現影像，「title」將被視為暫留文本等。

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**速記元件標籤聲明**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>若要建立點進圖形連結，您需要將錨點標籤和影像標籤包住div內部，並使用 `data-cq-component="clickthroughgraphicallink"` 屬性。
>
>例如。 `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>不支援使用CSS將影像與錨點標籤建立關聯的其他方法，例如下列標籤將無法運作：
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>與 `css .hasbackground { background-image: pathtoimage }`

### 銷售機會表單 {#lead-form}

銷售機會表單是用於收集訪客/銷售機會設定檔資訊的表單。 這些資訊可以儲存，並稍後用於根據這些資訊進行有效的營銷。 此資訊通常包括標題、姓名、電子郵件、出生日期、地址、興趣等。 它是「CTA銷售機會表單」群組的一部分。

**支援的功能**

* 預先定義的銷售機會欄位 — 名字、姓氏、地址、dob、性別、關於、userId、emailId、submit按鈕可在sidekick中使用。 只需在銷售機會表單中拖放所需元件即可。
* 在這些元件的協助下，作者可以設計獨立銷售機會表單，這些欄位對應至銷售機會表單欄位。 在獨立或匯入的zip應用程式中，使用者可以使用cq:form或cta銷售機會表單欄位來新增額外欄位、命名，並根據需求進行設計。
* 使用CTA銷售機會表單的特定預先定義名稱（例如 — firstName for first-name for lead form）映射銷售機會表單欄位，以此類推。
* 未對應至銷售機會表單的欄位會對應至cq:form元件 — 文字、選項、核取方塊、下拉式清單、隱藏、密碼。
* 使用者可使用「標籤」標籤來提供標題，並可使用樣式屬性「class」來提供樣式（僅適用於CTA銷售機會表單元件）。
* 「感謝」頁面和訂閱清單可以作為表單的隱藏參數提供（顯示在index.htm中），也可以從「銷售機會表單的開始」的編輯欄新增/編輯

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* 每個元件的編輯組態可提供所需的限制，例如。

HTML標籤，在匯入的zip中包含圖形連結元件。 此處，「firstName」對應至銷售機會表單firstName等，但核取方塊除外 — 這兩個核取方塊對應至cq:form下拉式元件。

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

AEM parsys元件是可包含其他AEM元件的容器元件。 可以在匯入HTML中新增parsys元件。 這可讓使用者在匯入登錄頁面後，仍將可編輯的AEM元件新增/刪除至登錄頁面。

段落系統可讓使用者使用sidekick新增元件。

HTML標籤以插入parsys元件( `foundation/components/parsys`)(在設計套件中的HTML中：

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

在HTML中加入上述標籤會執行下列動作：

* 在匯入設計套件後建立的登陸頁面中插入AEM parsys元件(foundation/components/parsys)。
* 使用預設元件初始化sidekick。 可將新元件從sidekick拖曳元件至parsys元件，以將其新增至登錄頁面。
* 兩個標題元件也是parsys的一部分。

### 目標 {#target}

目標元件會顯示頁面上的體驗內容。 您可以在促銷活動中建立許多體驗，而目標元件可動態地顯示來自不同體驗的內容給造訪頁面的不同使用者。

要插入目標元件，以及在促銷活動中建立不同體驗的html標籤：

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## 其他匯入選項 {#additional-importing-options}

除了指定匯入的元件是否為可編輯的AEM元件外，您也可以在匯入設計套件之前設定下列項目：

* 擷取匯入HTML中定義的中繼資料，以設定頁面屬性。
* 在HTML中指定字元集編碼。
* 覆蓋匯入工具頁面範本。

### 透過擷取匯入HTML中定義的中繼資料來設定頁面屬性 {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

設計匯入工具應擷取並保留在匯入HTML標題中宣告的下列中繼資料，並將其保留為「jcr:description」屬性：

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

HTML標籤中設定的Lang屬性應由設計匯入工具擷取並保留為屬性&quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### 在html中指定字元集編碼 {#specifying-the-charset-encoding-in-the-html}

設計匯入工具會讀取匯入HTML中指定的編碼。 可指定如下編碼：

`<meta charset="UTF-8">`

*或*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

如果未在匯入的HTML中指定任何編碼，則設計匯入工具設定的預設編碼為UTF-8。

### 覆蓋範本 {#overlaying-template}

您可以在下列位置建立新的登錄頁面，以覆蓋空白登錄頁面範本： `/apps/<appName>/designimporter/templates/<templateName>`

說明在AEM中建立新範本的步驟 [此處](/help/sites-developing/templates.md).

### 從登陸頁面轉介元件 {#referring-a-component-from-landing-page}

假設您有要在HTML中使用data-cq-component屬性參照的元件，讓設計匯入工具在此處轉譯元件包含。 例如，您要參照表格元件( `resourceType = /libs/foundation/components/table`)。 需要在HTML中新增下列項目：

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component中的路徑應為元件的resourceType。

### 最佳作法 {#best-practices}

若要搭配在匯入時標示為要進行元件轉換的元素使用，不建議使用類似下列的CSS選取器。

| E > F | E元素的F元素子項 | [子組合器](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | F元素前面緊接著E元素 | [相鄰同級組合器](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | 前面有E元素的F元素 | [一般同級組合器](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | E元素，文檔的根 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | an E元素，其父項的n子項 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | 一個E元素，即其父項的第n個子項，從最後一個計數 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | an E元素，其類型的第n個同級 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | an E元素，其類型的第n個同級，從最後一個計數 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

這是因為其他html元素如 &lt;div> 標籤會在匯入後新增至產生的Html。

* 也不建議使用依賴上述結構的指令碼，以搭配標示為要轉換為AEM元件的元素使用。
* 在標籤標籤上使用樣式進行元件轉換，例如 &lt;div data-cq-component=&quot;&amp;ast;&quot;> 不建議使用。
* 設計配置應遵循HTML5模板的最佳實務。 深入了解： [https://html5boilerplate.com/](https://html5boilerplate.com/).

## 設定OSGI模組 {#configuring-osgi-modules}

公開可透過OSGI控制台設定之屬性的元件如下：

* 登陸頁面設計匯入工具
* 登陸頁面產生器
* 行動登陸頁面產生器
* 登錄頁條目預處理器

下表簡要說明了這些屬性：

<table>
 <tbody>
  <tr>
   <td><strong>Component</strong></td>
   <td><strong>屬性名稱</strong></td>
   <td><strong>屬性說明 </strong></td>
  </tr>
  <tr>
   <td>登陸頁面設計匯入工具</td>
   <td>擷取篩選器</td>
   <td>用於從擷取中篩選檔案的規則運算式清單。 <br /> 與任何指定模式相符的郵遞區號項目會從解壓縮中排除</td>
  </tr>
  <tr>
   <td>登陸頁面產生器</td>
   <td>檔案模式</td>
   <td>登錄頁面產生器可設定為處理符合由檔案模式定義之規則運算式的HTML檔案。</td>
  </tr>
  <tr>
   <td>行動登陸頁面產生器</td>
   <td>檔案模式</td>
   <td>登錄頁面產生器可設定為處理符合由檔案模式定義之規則運算式的HTML檔案。</td>
  </tr>
  <tr>
   <td> </td>
   <td>裝置群組</td>
   <td>要支援的設備組清單。</td>
  </tr>
  <tr>
   <td>登錄頁條目預處理器</td>
   <td>搜尋模式 </td>
   <td>要在存檔條目內容中搜索的模式。 此規則運算式逐行與登入內容相符。 匹配後，匹配的文本將替換為指定的替換模式。<br /> <br /> 請參閱以下關於登錄頁面條目預處理程式的當前限制的備注。</td>
  </tr>
  <tr>
   <td> </td>
   <td>取代圖樣</td>
   <td>取代找到之相符項目的模式。 您可以使用規則運算式群組參考，例如$1、$2。 此外，此模式支援在匯入期間以實際值解析的關鍵字，如{designPath}。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**登錄頁條目預處理器的當前限制：**
>如果您需要對搜尋模式進行任何變更，當您開啟felix屬性編輯器時，需要手動新增反斜線字元以逸出規則運算式中繼字元。 如果您不手動新增反斜線字元，則規則運算式會視為無效，且不會取代舊的字元。
>
>例如，如果預設設定為
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>你需要替換 >`CQ_DESIGN_PATH` with `VIPURL` 在搜尋模式中，您的搜尋模式應如下所示：
`/\* *VIPURL *\*/ *(['"])`

## 疑難排解 {#troubleshooting}

匯入設計套件時，您可能會遇到數個錯誤，如本節所述。

### 使用登陸頁面相關元件初始化sidekick {#initialization-of-sidekick-with-landing-page-relevant-components}

如果設計套件包含parsys元件標籤，則匯入後，sidekick會開始顯示登錄頁面的相關元件。 您可以將新元件拖放至著陸頁面內的parsys元件。 您也可以前往設計模式，並將新元件新增至sidekick。

### 匯入期間顯示錯誤訊息 {#error-messages-displayed-during-import}

如果發生任何錯誤（例如，匯入的套件不是有效的zip），設計匯入將不會匯入套件，而會在拖放方塊的正上方的頁面上方顯示錯誤訊息。 此處說明錯誤情況的範例。 更正錯誤後，您可以將更新的zip重新匯入至相同的空白登陸頁面。 擲回錯誤的不同情況如下：

* 導入的設計包不是有效的zip存檔。
* 導入的設計包在頂層不包含index.html。

### 匯入後顯示警告 {#warnings-displayed-after-import}

若有任何警告(例如，HTML是指套件中不存在的影像)，設計匯入工具將會匯入zip，但同時在「結果窗格」上顯示問題/警告清單，按一下問題連結，會顯示警告清單，指出設計套件中的任何問題。 設計匯入工具擷取並顯示警告的不同情況如下：

* HTML是指套件中不存在的影像。
* HTML是指套件內不存在的指令碼。
* HTML是指套件中不存在的樣式。

### ZIP檔案儲存在AEM中的位置？ {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

匯入登錄頁面後，檔案（影像、css、js等） 設計套件內儲存於AEM中的下列位置：

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

假設在促銷活動We.Retail下建立登錄頁面，且登錄頁面的名稱為 **myBlankLandingPage** 然後儲存Zip檔案的位置如下：

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### 未保留格式 {#formatting-not-preserved}

建立CSS時，請注意下列限制：

如果文字和（可編輯）影像類似下列：

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

的CSS `box` 如下所示：

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

然後 `box img` 在設計匯入工具中使用，產生的登錄頁面似乎並未保留格式。 若要解決此問題，請注意AEM在CSS中新增div標籤，並據此重寫程式碼。 否則，某些CSS規則將會無效。

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
此外，設計人員應注意，只有 **id=cqcanvas** 標籤是匯入工具所識別，否則不會保留設計。
