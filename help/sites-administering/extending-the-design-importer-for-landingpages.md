---
title: 擴充及設定著陸頁面的Design Importer
seo-title: 擴充及設定著陸頁面的Design Importer
description: 瞭解如何為登陸頁面設定Design Importer。
seo-description: 瞭解如何為登陸頁面設定Design Importer。
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec

---


# 擴充及設定著陸頁面的Design Importer{#extending-and-configuring-the-design-importer-for-landing-pages}

本節說明如何設定，並視需要擴充著陸頁面的設計匯入工具。 在匯入後使用著陸頁面，在著陸頁面 [中涵蓋。](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**讓設計匯入工具擷取您的自訂元件**

以下是讓設計匯入工具識別自訂元件的邏輯步驟

1. 建立TagHandler

   * 標籤處理常式是處理特定類型HTML標籤的POJO。 您TagHandler可處理的HTML標籤「種類」是透過TagHandlerFactory的OSGi屬性「tagpattern.name」來定義。 此OSGi屬性實質上是一個regex，應符合您要處理的輸入html標籤。 所有巢狀標籤都會擲回您的標籤處理常式以進行處理。 例如，如果您註冊的div包含巢狀的&lt;p>標籤，&lt;p>標籤也會擲回您的TagHandler，這取決於您要如何處理它。
   * 標籤處理常式介麵類似於SAX內容處理常式介面。 它會接收每個html標籤的SAX事件。 身為標籤處理常式提供者，您必須實作某些由設計匯入工具架構自動呼叫的生命週期方法。

1. 建立其對應的TagHandlerFactory。

   * 標籤處理常式工廠是OSGi元件（單例），負責您標籤處理常式的產生例項。
   * 您的標籤處理常式工廠必須公開名為&quot;tagpattern.name&quot;的OSGi屬性，該值與輸入html標籤相符。
   * 如果有多個標籤處理常式與輸入html標籤相符，則會選取排名較高的標籤處理常式。 排名本身會公開為OSGi屬 **性service.ranking**。
   * TagHandlerFactory是OSGi元件。 您要提供給TagHandler的任何參照都必須透過此工廠。

1. 如果您想要覆寫預設值，請確定您的TagHandlerFactory有更好的排名。

>[!CAUTION]
>
>用於匯入登陸頁面的Design Importer已 [在AEM 6.5中停用](/help/release-notes/deprecated-removed-features.md#deprecated-features)。

## 準備HTML以匯入 {#preparing-the-html-for-import}

建立匯入工具頁面後，您可以匯入完整的HTML登陸頁面。 若要匯入HTML登陸頁面，您必須先將其內容壓縮至設計套件。 設計套件包含您的HTML登陸頁面以及參考的資產（影像、css、圖示、指令碼等）。

以下快速參考表提供如何準備HTML以匯入的範例：

著陸頁面快速參考表

[取得檔案](assets/cheatsheet.zip)

### Zip檔案版面配置與需求 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>此時，ZIP檔案只能包含一個HTML頁面或一個頁面的一部分。

郵遞區號的範例版面如下：

* /index.html ->著陸頁面HTML檔案
* /css ->以新增至CSSclientlib
* /img ->所有影像和資產
* /js ->以新增至JS clientlib

此版面是以HTML5 Boilerplate最佳實務版面為基礎。 如需詳細資訊，請造訪 [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>設計套件至少必 **須包含****根層級的index.html** 檔案。 如果要匯入的著陸頁面也有行動版本，則zip必須包含 **mobile.index.html** ，以及 **根層級的index.html** 。

### 準備著陸頁面HTML {#preparing-the-landing-page-html}

若要能夠匯入HTML，您必須將畫布div新增至著陸頁面HTML。

畫布div是html **div** , `id="cqcanvas"` 必須插入HTML標籤中， `<body>` 且必須包住要轉換的內容。

新增畫布div後著陸頁面HTML的範例片段如下：

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

當您匯入著陸頁面時，您可以選擇依現狀匯入頁面，這表示在匯入著陸頁面後，您無法編輯AEM中任何匯入的項目（您仍可在頁面上新增其他AEM元件）。

在匯入著陸頁面之前，您可能想要轉換著陸頁面的某些部分，讓這些部分成為可編輯的AEM元件。 這可讓您在匯入著陸頁面設計後，快速編輯著陸頁面的部分。

若要這麼做，請將 `data-cq-component` 元件新增至您匯入的HTML檔案中的適當元件。

以下章節說明如何編輯HTML檔案，以便將登陸頁面的某些部分轉換為不同的可編輯AEM元件。 Components are detail in [Landing Pages Components.（著陸頁面元件）](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)。

>[!NOTE]
>
>HTML markup to convert parts of the landing page into AEM components have a long form and a shorthand tag declaration. 這兩者都針對每個元件進行說明。

### 限制 {#limitations}

在匯入之前，請注意下列限制：

### &amp;lt;body>標籤上應用的類或ID等任何屬性都不會保留 {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

如果任何屬性（例如id或class）套用在body標籤上，則 `<body id="container">` 在匯入後不會保留它。 因此，要導入的設計不應與標籤上應用的屬性有任何相 `<body>` 依性。

### 拖放郵遞區號 {#drag-and-drop-zip}

Internet explorer和Firefox 3.6版及舊版不支援拖放zip上傳。 若要在使用這些瀏覽器時上傳設計，請按一下放置檔案區域以開啟檔案上傳對話方塊，並使用該對話方塊上傳您的設計。

支援設計zip的「拖放」瀏覽器為Chrome、Safari5.x、Firefox 4和更新版本。

### 不支援Modernizr {#modernizr-is-not-supported}

`Modernizr.js` 是以javascript為基礎的工具，可偵測瀏覽器的原生功能，並偵測它們是否適合html5元素。 使用Modernizr來增強舊版不同瀏覽器支援的設計，可能會在登陸頁面解決方案中造成匯入問題。 `Modernizr.js` Design匯入工具不支援指令碼。

### 在導入設計包時不保留頁面屬性 {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

任何頁面屬性（例如自訂網域、強制HTTPS等）設定在匯入設計套件之前（使用「空白著陸頁面」範本）的頁面，會在匯入設計後遺失。 因此，建議的做法是在匯入設計套件後設定頁面屬性。

### 假定僅HTML標籤 {#html-only-markup-assumed}

在導入時，會基於安全原因和為了避免導入和發佈無效標籤而清理標籤。 這假定僅HTML標籤，且所有其他形式的元素（例如內嵌SVG或Web元件）將被過濾掉。

### 文字 {#text}

HTML標籤，以在設計套件的HTML `foundation/components/text`中插入文字元件():

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

在HTML中加入上述標籤，會執行下列動作：

* 在匯入設計套件後建立的著陸頁 `sling:resourceType=foundation/components/text`面中，建立可編輯的AEM文字元件()。
* 將已創 `text` 建文本元件的屬性設定為包含在中的HTML `div`。

**Shorthand component tag declaration**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**含清單的文字**

要添加包含清單的文本，請執行以下操作：

* 1st
* 2nd

可在RTE編輯器中編輯的：

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**含顏色的文字**

要添加可在RTE編輯器中編輯的帶顏色（粉紅色）的文本：

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### 標題 {#title}

HTML markup to insert a title component( `wcm/landingpage/components/title`)in the HTML within design package:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

在HTML中加入上述標籤，會執行下列動作：

* 在匯入設計套件後建立的著陸頁 `sling:resourceType=wcm/landingpage/components/title`面中，建立可編輯的AEM標題元件()。
* 將已創 `jcr:title` 建標題元件的屬性設定為div內包住的標題標籤內的文本。
* 將屬性 `type` 設為標題標籤，在本例中 `h1`。

標題元件支援7種類型- `h1, h2, h3, h4, h5, h6` 和 `default`。

**Shorthand component tag declaration**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 影像 {#image}

HTML標籤，可在設計套件內的HTML中插入影像元件(foundation/components/image):

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

在HTML中加入上述標籤，會執行下列動作：

* 在匯入設計套件後建立的著陸頁 `sling:resourceType=foundation/components/image`面中，建立可編輯的AEM影像元件()。
* 將已創 `fileReference` 建映像元件的屬性設定為src屬性中指定的映像的導入路徑。
* 將屬性 `alt` 設定為img標籤中alt屬性的值。
* 將屬 `title` 性設為img標籤中的title屬性值。
* 將屬 `width` 性設定為img標籤中width屬性的值。
* 將屬性 `height` 設為img標籤中height屬性的值。

**Shorthand component tag declaration:**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### Absolute URL img src not supported within Image component Div {#absolute-url-img-src-not-supported-within-image-component-div}

如果嘗 `<img>` 試使用絕對URL src的標籤進行元件轉換，則會引 **發適當的UnsupportedTagContentException** 。 例如，不支援下列項目：

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

但是，不屬於「影像元件div」的img標籤支援絕對URL影像。

### 行動要求元件 {#call-to-action-components}

您可以將著陸頁面的一部分標籤為匯入為「可編輯的動作呼叫元件」-這些匯入的動作呼叫元件可在匯入著陸頁面後加以編輯。 AEM包含下列CTA元件：

* 點進連結——可讓您新增文字連結，在點按時會將訪客帶往目標URL。
* 圖形連結——可讓您新增在點按時將訪客帶往目標URL的影像。

#### 點進連結 {#click-through-link}

此CTA元件可用來在登陸頁面上新增文字連結。

支援的屬性

* 標籤，含粗體、斜體和底線選項
* 目標URL，支援協力廠商和AEM URL
* 頁面演算選項（相同視窗、新視窗等）

HTML標籤，以在匯入的zip中包含點進元件。 這裡href對應至目標URL,「檢視產品詳細資訊」對應至標籤等。

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

**Shorthand component tag declaration**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### 圖形連結 {#graphical-link}

此CTA元件可用來新增任何在著陸頁面上具有連結的圖形影像。 影像可以是簡單按鈕或任何圖形影像做為背景。 當點按影像時，使用者會被帶到元件屬性中指定的目標URL。 它是「行動呼籲」群組的一部分。

支援的屬性

* 影像裁切、旋轉
* 暫留文字、說明、大小(px)
* 目標URL，支援協力廠商和AEM URL
* 頁面演算選項（相同視窗、新視窗等）

HTML標籤，以在匯入的zip中包含圖形連結元件。 此處href將映射至目標url,img src將是演算影像，&quot;title&quot;將被當作暫留文字等等。

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Shorthand component tag declaration**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>若要建立點進圖形連結，您必須在div內包住錨點標籤和影像標籤(含屬 `data-cq-component="clickthroughgraphicallink"` 性)。
>
>eg. `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>不支援使用CSS將影像與錨點標籤建立關聯的其他方式，例如下列標籤將無法運作：
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>與 `css .hasbackground { background-image: pathtoimage }`


### 銷售機會表單 {#lead-form}

銷售機會表單是用於收集訪客／銷售機會描述檔資訊的表單。 這些資訊可以儲存，稍後再使用這些資訊進行有效的行銷。 這些資訊通常包括標題、姓名、電子郵件、出生日期、地址、興趣等。 它是「CTA銷售機會表單」群組的一部分。

**支援的功能**

* 預先定義的銷售機會欄位- sidekick中提供名字、姓氏、地址、dob、性別、about、userId、emailId、submit按鈕。 只需在銷售機會表單中拖放必要元件即可。
* 在這些元件的協助下，作者可以設計獨立的銷售機會表單，這些欄位對應於銷售機會表單欄位。 在單機版或匯入的zip應用程式中，使用者可以使用cq:form或cta lead form欄位新增額外欄位，並依需求命名和設計欄位。
* 使用CTA銷售機會表單的特定預先定義名稱映射銷售機會表單欄位，例如- firstName（銷售機會表單中的名字）等。
* 未映射至銷售機會表單的欄位將會映射至cq:form元件- text, radio, checkbox, dropdown, hidden, password.
* 使用者可使用「標籤」標籤來提供標題，並可使用樣式屬性「class」來提供樣式（僅適用於CTA銷售機會表單元件）。
* 「感謝」頁面和訂閱清單可提供為表單的隱藏參數（顯示在index.htm中），或從「銷售機會表單的開始」編輯列新增／編輯

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/tw/user/register/thank_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* 可從每個元件的編輯配置中提供所需約束。

HTML標籤，以在匯入的zip中包含圖形連結元件。 此處&quot;firstName&quot;已映射至銷售機會表單firstName等，但核取方塊除外——這兩個核取方塊會映射至cq:form下拉式元件。

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

AEM parsys元件是可包含其他AEM元件的容器元件。 可在匯入的HTML中新增parsys元件。 這可讓使用者在匯入可編輯的AEM元件後，仍可將其新增／刪除至著陸頁面。

段落系統可讓使用者使用sidekick新增元件。

HTML markup to insert a parsys component( `foundation/components/parsys`)in the HTML within design package:

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

在HTML中加入上述標籤會執行下列動作：

* 在匯入設計套件後建立的著陸頁面中插入AEM parsys元件(foundation/components/parsys)。
* 使用預設元件初始化sidekick。 將元件從sidekick拖曳至parsys元件，即可將新元件新增至著陸頁面。
* 兩個標題元件也是parsys的一部分。

### 目標 {#target}

目標元件顯示頁面上的體驗內容。 您可以在促銷活動中建立許多體驗，而目標元件可動態地將不同體驗的內容顯示給造訪頁面的不同使用者。

html標籤可插入目標元件，並在促銷活動中建立不同的體驗：

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

除了指定匯入的元件是否為可編輯的AEM元件外，您也可以在匯入設計套件之前先設定下列項目：

* 透過擷取匯入的HTML中定義的中繼資料來設定頁面屬性。
* 在HTML中指定charset編碼。
* 覆蓋匯入工具頁面範本。

### 透過擷取在匯入的HTML中定義的中繼資料來設定頁面屬性 {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

Following metadata declared in the head of the imported HTML shall be extracted and preserved by design importer as property &quot;jcr:description&quot;:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

HTML標籤中的Lang屬性集由設計匯入工具擷取並保留為屬性&quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### 在html中指定charset編碼 {#specifying-the-charset-encoding-in-the-html}

設計匯入工具會讀取匯入的HTML中指定的編碼。 可指定編碼如下：

`<meta charset="UTF-8">`

*或*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

如果匯入的HTML中未指定任何編碼，則設計匯入工具設定的預設編碼為UTF-8。

### 覆蓋範本 {#overlaying-template}

The Blank Landing Page template can be overlayed by creating a new one at: `/apps/<appName>/designimporter/templates/<templateName>`

在這裡說明在AEM中建立新範本的 [步驟](/help/sites-developing/templates.md)。

### 從「著陸」頁面轉介元件 {#referring-a-component-from-landing-page}

假設您有要在HTML中使用data-cq-component屬性來參照的元件，如此，設計匯入工具就會在此處轉譯元件包含。 例如，您要引用表元件( `resourceType = /libs/foundation/components/table`)。 HTML中需要新增下列項目：

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component中的路徑應為該元件的resourceType。

### Best Practices {#best-practices}

不建議使用類似下列的CSS選擇器，以便與在匯入時標籤為元件轉換的元素搭配使用。

| E > F | E元素的an f元素子項 | [子組合器](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | an F element immediated preceded by an E element | [相鄰同級組合器](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | an F element preceded by an E element | [一般同級組合器](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | an E element, root of the document | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | an E element, the n-th child of its parent | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | an E element, the n-th child of its parent, counting from the last one | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | an E element, the n-th sibling of its type | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | an E element, the n-th sibling of its type, counting from the last one | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

這是因為匯入後，會新增其他html元素（例如&lt;div>標籤）至產生的Html。

* 另外，也不建議使用依循類似上述結構的指令碼，以搭配標示為轉換為AEM元件的元素使用。
* 不建議在標籤標籤上使用樣式進行元件轉換，例如&lt;div data-cq-component=&quot;&amp;ast;&quot;>。
* 設計版面應遵循HTML5 Boilerplate的最佳實務。 詳細內容： [https://html5boilerplate.com/](https://html5boilerplate.com/)。

## 配置OSGI模組 {#configuring-osgi-modules}

透過OSGI主控台可設定的公開屬性的元件如下：

* 著陸頁面設計匯入工具
* 著陸頁面產生器
* 行動著陸頁面產生器
* 著陸頁面項目預處理器

下表簡要說明了這些屬性：

<table>
 <tbody>
  <tr>
   <td><strong>元件</strong></td>
   <td><strong>屬性名稱</strong></td>
   <td><strong>屬性說明 </strong></td>
  </tr>
  <tr>
   <td>著陸頁面設計匯入工具</td>
   <td>擷取篩選</td>
   <td>用於從抽取中過濾檔案的規則運算式清單。 <br /> 與任何指定模式相符的郵遞區號項目會從擷取中排除</td>
  </tr>
  <tr>
   <td>著陸頁面產生器</td>
   <td>檔案模式</td>
   <td>「著陸頁面產生器」可設定為處理符合由檔案模式定義的規則運算式的HTML檔案。</td>
  </tr>
  <tr>
   <td>行動著陸頁面產生器</td>
   <td>檔案模式</td>
   <td>「著陸頁面產生器」可設定為處理符合由檔案模式定義的規則運算式的HTML檔案。</td>
  </tr>
  <tr>
   <td> </td>
   <td>裝置群組</td>
   <td>要支援的設備組清單。</td>
  </tr>
  <tr>
   <td>著陸頁面項目預處理器</td>
   <td>搜尋模式 </td>
   <td>要搜索的模式，在存檔條目內容中。 此規則運算式與項目內容逐行比對。 匹配時，匹配文本將被指定的替換模式替換。<br /> 請參 <br /> 閱以下關於著陸頁面項目預處理器目前限制的附註。</td>
  </tr>
  <tr>
   <td> </td>
   <td>取代圖樣</td>
   <td>取代找到的匹配項的模式。 您可使用規則運算式群組參考，例如$1、$2。 此外，此模式還支援在匯入期間以實際值解析的關鍵字{designPath}。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**著陸頁面項目預處理器的目前限制：**
>如果您需要對搜尋模式進行任何變更，在開啟felix屬性編輯器時，您需要手動新增反斜線字元以逸出規則運算式元字元。 如果您不手動新增反斜線字元，則會將regex視為無效，且不會取代舊的字元。
>
>例如，若預設組態為
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>而且，您需要取代 >`CQ_DESIGN_PATH` 在搜 `VIPURL` 尋模式中，則您的搜尋模式應如下所示：
`/\* *VIPURL *\*/ *(['"])`

## 疑難排解 {#troubleshooting}

導入設計包時，可能會遇到一些錯誤，如本節所述。

### 使用著陸頁面相關元件初始化sidekick {#initialization-of-sidekick-with-landing-page-relevant-components}

如果設計套件包含parsys元件標籤，則在匯入後，sidekick會開始顯示著陸頁面相關元件。 您可以將新元件拖放至著陸頁面內的parsys元件上。 您也可以前往設計模式，並將新元件新增至sidekick。

### 匯入期間顯示的錯誤訊息 {#error-messages-displayed-during-import}

如果發生任何錯誤（例如，匯入的套件不是有效的zip），設計匯入將不會匯入套件，而會在拖放方塊正上方的頁面上顯示錯誤訊息。 此處說明錯誤案例的範例。 更正錯誤後，您可以將更新的zip重新匯入至相同的空白著陸頁面。 拋出錯誤的不同藍本如下：

* 匯入的設計套件不是有效的zip封存。
* 匯入的設計套件頂層不包含index.html。

### 匯入後顯示的警告 {#warnings-displayed-after-import}

如果有任何警告（例如，HTML是指套件中不存在的影像），設計匯入工具會匯入zip，但同時在「結果窗格」上顯示問題／警告清單，按一下問題連結會顯示警告清單，指出設計套件中的任何問題。 設計匯入工具會擷取並顯示警告的不同藍本如下：

* HTML是指套件中不存在的影像。
* HTML是指套件中不存在的指令碼。
* HTML是指套件中不存在的樣式。

### AEM中儲存的ZIP檔案位於何處？ {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

在匯入著陸頁面後，檔案（影像、css、js等）within design package are stored in the following location in AEM:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

假設著陸頁面是在促銷活動We.Retail下建立，且著陸頁面的名稱為 **myBlankLandingPage** ，則儲存Zip檔案的位置如下：

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

的CSS，如 `box` 下：

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

然後 `box img` 在設計匯入工具中使用，產生的著陸頁面會顯示並未保留格式。 若要解決這個問題，請注意AEM會在CSS中新增div標籤，並據以重寫程式碼。 否則，某些CSS規則將無效。

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
此外，設計人員應注意，匯入工具只會識別 **id=cqcanvas** 標籤內的程式碼，否則不會保留設計。

