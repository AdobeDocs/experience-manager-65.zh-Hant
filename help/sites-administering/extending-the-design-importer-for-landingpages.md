---
title: 擴展和配置登錄頁的設計導入程式
seo-title: Extending and Configuring the Design Importer for Landing Pages
description: 瞭解如何為登錄頁配置設計導入程式。
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

# 擴展和配置登錄頁的設計導入程式{#extending-and-configuring-the-design-importer-for-landing-pages}

本節介紹如何配置並根據需要擴展登錄頁的設計導入程式。 導入後使用登錄頁 [登錄頁。](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**使設計導入程式提取您的自定義元件**

以下是使設計導入程式識別您的自定義元件的邏輯步驟

1. 建立TagHandler

   * 標籤處理程式是處理特定類型的HTML標籤的POJO。 TagHandler可以處理的HTML標籤的「種類」是通過TagHandlerFactory的OSGi屬性「tagpattern.name」定義的。 此OSGi屬性實質上是一個規則運算式，它應與要處理的輸入html標籤匹配。 所有嵌套的標籤都將拋出給標籤處理程式以進行處理。 例如，如果註冊的div包含嵌套 &lt;p> 標籤， &lt;p> 標籤也會被拋出到TagHandler中，您將決定您希望如何處理它。
   * 標籤處理程式介面與SAX內容處理程式介麵類似。 它接收每個html標籤的SAX事件。 作為標籤處理程式提供程式，您需要實現某些由設計導入程式框架自動調用的生命週期方法。

1. 建立其相應的TagHandlerFactory。

   * 標籤處理程式工廠是一個OSGi元件(singleton)，負責生成標籤處理程式的實例。
   * 標籤處理程式工廠必須公開名為「tagpattern.name」的OSGi屬性，其值與輸入html標籤匹配。
   * 如果有多個標籤處理程式與輸入html標籤匹配，則選取排名較高的標籤處理程式。 排名本身被公之於眾，被視為OSGi屬性 **服務。排名**。
   * TagHandlerFactory是OSGi元件。 您希望提供給TagHandler的任何引用都必須通過此工廠。

1. 如果要覆蓋預設值，請確保TagHandlerFactory具有更好的排名。

>[!CAUTION]
>
>用於導入登錄頁的設計導入程式， [不建議使用AEM6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features)。

## 準備HTML以導入 {#preparing-the-html-for-import}

建立導入程式頁後，可以導入完整的HTML登錄頁。 要導入HTML登錄頁，您需要先將其內容壓縮到設計包中。 設計包包含您的HTML登錄頁以及引用的資產（影像、css、表徵圖、指令碼等）。

以下作弊表提供了如何準備導入HTML的示例：

登錄頁作弊表

[取得檔案](assets/cheatsheet.zip)

### Zip檔案佈局和要求 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>此時，ZIP檔案只能包含一個HTML頁或一頁的一部分。

zip的示例佈局如下：

* /index.html ->登錄頁HTML檔案
* /css ->添加到CSS客戶端庫
* /img ->所有映像和資產
* /js ->添加到JS客戶端庫

佈局基於HTML5 Boilerplate最佳實踐佈局。 閱讀更多內容 [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>至少，設計包 **必須** 包含 **索引.html** 檔案。 如果要導入的登錄頁也具有移動版本，則zip必須包含 **mobile.index.html** 以及 **索引.html** 在根級別。

### 準備登錄頁HTML {#preparing-the-landing-page-html}

要能夠導入HTML，需要向登錄頁HTML添加畫布div。

畫布div是html **div** 與 `id="cqcanvas"` 必須插入HTML `<body>` 標籤，並且必須包裝要轉換的內容。

添加canvas div後登錄頁HTML的示例片段如下：

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

### 準備HTML以包含可編輯組AEM件 {#preparing-the-html-to-include-editable-aem-components}

導入登錄頁時，您可以選擇按原樣導入頁面，這意味著在導入登錄頁後，您無法編輯中的任何導入項AEM(您仍然可以在頁面中添加AEM其他元件)。

在導入登錄頁之前，您可能希望轉換登錄頁的某些部分，以便它們是可編輯的組AEM件。 這樣，即使導入登錄頁設計後，您也可以快速編輯登錄頁的部分。

通過添加 `data-cq-component` 導入的HTML檔案中的相應元件。

以下部分介紹如何編輯HTML檔案，以便將登錄頁的某些部分轉換為不同的可編輯AEM元件。 元件詳細描述如下： [登錄頁元件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)。

>[!NOTE]
>
>HTML標籤將登錄頁的部分轉換為AEM元件具有長格式和速記標籤聲明。 對每個元件都進行了說明。

### 限制 {#limitations}

在導入之前，請注意以下限制：

### 未保留在&amp;lt;body>標籤上應用的類或ID等任何屬性 {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

如果在body標籤上應用了諸如id或類之類的屬性 `<body id="container">` 那麼在導入後就不會保留。 因此，所導入的設計不應與應用於 `<body>` 標籤。

### 拖放zip {#drag-and-drop-zip}

Internet Explorer和Firefox 3.6及更低版本不支援拖放zip上載。 要使用這些瀏覽器上載設計時，請按一下放置檔案區域以開啟檔案上載對話框，並使用該對話框上載設計。

支援設計zip「拖放」的瀏覽器是Chrome、Safari5.x、Firefox 4及更高版本。

### 不支援Modernizr {#modernizr-is-not-supported}

`Modernizr.js` 是基於javascript的工具，它檢測瀏覽器的本機功能，並檢測它們是否適合html5元素。 使用Modernizr增強不同瀏覽器舊版本支援的設計可能會導致登錄頁解決方案中的導入問題。 `Modernizr.js` 設計導入程式不支援指令碼。

### 導入設計包時不保留頁面屬性 {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

任何頁屬性（例如自定義域、強制HTTPS等） 在導入設計包之前為頁面設定（使用「空白登錄頁」模板），在導入設計後將丟失。 因此，建議的做法是在導入設計包後設定頁面屬性。

### HTML僅假定標籤 {#html-only-markup-assumed}

在導入時，出於安全原因和為了避免導入和發佈無效標籤而對標籤進行清理。 這假定僅HTML標籤，並且所有其它形式的元素(如內聯SVG或Web元件)將被過濾掉。

### 文字 {#text}

HTML標籤以插入文本元件( `foundation/components/text`)在設計包HTML中：

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

在HTML中包括上述標籤，將執行以下操作：

* 建立可編AEM輯的文本元件( `sling:resourceType=foundation/components/text`)。
* 設定 `text` 建立的文本元件的屬性 `div`。

**速記元件標籤聲明**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**帶清單的文本**

添加包含清單的文本：

* 1st
* 2nd

可在RTE編輯器中編輯：

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**帶顏色的文本**

添加可在RTE編輯器中編輯的帶顏色（粉紅色）的文本：

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### 標題 {#title}

HTML標注以插入標題元件( `wcm/landingpage/components/title`)在設計包HTML中：

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

在HTML中包括上述標籤，將執行以下操作：

* 建立可編輯AEM的標題元件( `sling:resourceType=wcm/landingpage/components/title`)。
* 設定 `jcr:title` 包含在div中的標題標籤中的文本的已建立標題元件的屬性。
* 設定 `type` 標題標籤的屬性，在本例中 `h1`。

標題元件支援7種類型 —  `h1, h2, h3, h4, h5, h6` 和 `default`。

**速記元件標籤聲明**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 影像 {#image}

HTML標籤，用於在設計包內的HTML中插入影像元件（基礎/元件/影像）:

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

在HTML中包括上述標籤，將執行以下操作：

* 建立可編輯AEM的影像元件( `sling:resourceType=foundation/components/image`)。
* 設定 `fileReference` 建立的影像元件的屬性到在src屬性中指定的影像導入到的路徑。
* 設定 `alt` 屬性到img標籤中alt屬性的值。
* 設定 `title` 屬性到img標籤中title屬性的值。
* 設定 `width` 屬性到img標籤中width屬性的值。
* 設定 `height` 屬性到img標籤中height屬性值。

**速記元件標籤聲明：**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### 影像元件Div中不支援絕對URL img src {#absolute-url-img-src-not-supported-within-image-component-div}

如果 `<img>` 嘗試使用絕對url src進行元件轉換的標籤， **UnsupportedTagContentException** 。 例如，不支援以下內容：

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

但是，對於不屬於「影像元件div」的img標籤，則支援絕對URL影像。

### 行動要求元件 {#call-to-action-components}

您可以將導入的登錄頁的一部分標籤為「可編輯的操作呼叫元件」 — 此類導入的操作呼叫元件可以在導入登錄頁後進行編輯。 包AEM括以下CTA元件：

* 按一下「通過連結」(Through Link) — 用於添加文本連結，按一下該連結時訪問者將訪問目標URL。
* 圖形連結 — 用於添加按一下時訪問者訪問目標URL的影像。

#### 按一下「通過」連結 {#click-through-link}

此CTA元件可用於在登錄頁上添加文本連結。

支援的屬性

* 標籤，帶粗體、斜體和下划線選項
* 目標URL，支援第三方和AEMURL
* 頁面呈現選項（相同窗口、新窗口等）

HTML標籤，以在導入的zip中包含按一下過元件。 此處href映射到目標url，「查看產品詳細資訊」映射到標籤等。

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

此元件可用於任何獨立應用程式，也可從zip導入。

**速記元件標籤聲明**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### 圖形連結 {#graphical-link}

此CTA元件可用於添加登錄頁上具有連結的任何圖形影像。 影像可以是簡單按鈕或任何作為背景的圖形影像。 按一下影像後，用戶將被帶到元件屬性中指定的目標URL。 它是「行動要求」組的一部分。

支援的屬性

* 影像裁剪，旋轉
* 懸停文本、說明、大小（以px為單位）
* 目標URL，支援第三方和AEMURL
* 頁面呈現選項（相同窗口、新窗口等）

HTML標籤，以在導入的zip中包含圖形連結元件。 此處href將映射到目標url,img src將作為渲染影像，「title」將作為懸停文本等。

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
>要建立點擊式圖形連結，需要將錨點標籤和影像標籤包裝在div中 `data-cq-component="clickthroughgraphicallink"` 屬性。
>
>例如 `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>不支援使用CSS將影像與錨點標籤關聯的其他方法，例如，以下標籤將不起作用：
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>與 `css .hasbackground { background-image: pathtoimage }`

### 銷售機會表單 {#lead-form}

潛在顧客表單是用於收集訪問者/潛在顧客的個人資料資訊的表單。 該資訊可以被儲存並稍後用於基於該資訊進行有效的營銷。 此資訊通常包括標題、姓名、電子郵件、出生日期、地址、興趣等。 它是「CTA Lead表單」組的一部分。

**支援的功能**

* 預定義的潛在客戶欄位 — 旁接中提供了名字、姓氏、地址、dob、性別、關於、userId、emailId、submit按鈕。 只需在銷售線索表單中拖放所需元件即可。
* 在這些元件的幫助下，作者可以設計一個獨立的銷售線索表單，這些欄位對應於銷售線索表單欄位。 在獨立或導入的zip應用程式中，用戶可以使用cq:form或cta lead表單欄位添加額外欄位，根據要求命名和設計這些欄位。
* 使用CTA潛在顧客表單的特定預定義名稱映射潛在顧客表單域，例如 — firstName作為潛在顧客表單中的名字，依此類推。
* 未映射到潛在顧客表單的欄位將映射到cq:form元件 — 文本、單選按鈕、複選框、下拉清單、隱藏、密碼。
* 用戶可以使用「label」標籤提供標題，並可以使用樣式屬性「class」（僅適用於CTA潛在顧客表單元件）提供樣式。
* 「感謝」頁面和訂閱清單可以作為表單的隱藏參數（在index.htm中顯示）提供，也可以從「潛在顧客表單的開始」編輯欄添加/編輯

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* 例如 — 所需約束可通過每個元件的編輯配置提供。

HTML標籤，以在導入的zip中包含圖形連結元件。 此處，「firstName」映射到潛在顧客表單firstName等，但複選框除外 — 這兩個複選框映射到cq:form下拉清單元件。

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

### 帕爾瑟 {#parsys}

parsys組AEM件是可包含其他元件的容AEM器元件。 可以在導入HTML中添加parsys元件。 這允許用戶將可編輯的元件AEM添加/刪除到登錄頁，即使在導入後也是如此。

段落系統使用戶能夠使用邊框添加元件。

HTML標籤以插入parsys元件( `foundation/components/parsys`)在設計包HTML中：

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

在HTML中包括上述標籤將執行以下操作：

* 在導AEM入設計包後建立的登錄頁中插入parsys元件(foundation/components/parsys)。
* 使用預設元件初始化邊鍵。 通過將元件從側腳拖到parsys元件上，可以將新元件添加到登錄頁。
* 兩個標題元件也是parsys的一部分。

### 目標 {#target}

目標元件顯示頁面上的體驗內容。 一個活動中可以建立許多體驗，目標元件可以動態地將不同體驗的內容顯示給訪問該頁面的不同用戶。

用於插入目標元件並在市場活動中建立不同體驗的html標籤：

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

## 其他導入選項 {#additional-importing-options}

除了指定導入的元件是否是可編AEM輯的元件外，還可在導入設計包之前配置以下元件：

* 通過提取導入HTML中定義的元資料來設定頁面屬性。
* 在HTML中指定字元集編碼。
* 覆蓋導入程式頁面模板。

### 通過提取在導入的HTML中定義的元資料來設定頁面屬性 {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

在進口HTML的頭部申報的下列元資料，應由設計進口商提取並保存為&quot;jcr:description&quot;屬性：

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

設計導入程式應將HTML標籤中設定的Lang屬性作為屬性「jcr:language」進行提取和保留

* &lt;html lang=&quot;en&quot;>

### 在html中指定字元集編碼 {#specifying-the-charset-encoding-in-the-html}

設計導入程式讀取導入HTML中指定的編碼。 可以按如下方式指定編碼：

`<meta charset="UTF-8">`

*或*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

如果導入的HTML中未指定編碼，則設計導入程式設定的預設編碼為UTF-8。

### 覆蓋模板 {#overlaying-template}

通過在以下位置建立新登錄頁模板，可以覆蓋空白登錄頁模板： `/apps/<appName>/designimporter/templates/<templateName>`

將說明在中建立新模板AEM的步驟 [這裡](/help/sites-developing/templates.md)。

### 從登錄頁引用元件 {#referring-a-component-from-landing-page}

假設您有一個要在HTML中引用的元件，該元件使用data-cq-component屬性，這樣設計導入程式就會在此處呈現一個元件。 例如，要引用表元件( `resourceType = /libs/foundation/components/table`)。 需要在HTML中添加以下內容：

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component中的路徑應為該元件的resourceType。

### 最佳做法 {#best-practices}

建議不要使用與下列選擇器類似的CSS選擇器，以便與在導入時標籤為要進行元件轉換的元素一起使用。

| E > F | E元素的F元素子項 | [子組合符](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | 緊跟在E元素前面的F元素 | [相鄰同級組合器](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | 前面帶有E元素的F元素 | [普通同級組合符](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E：根 | E元素，文檔的根 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | an E元素，其父代的第n個子代 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | 一個E元素，其父代的第n個子代，從最後一個元素開始計算 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：第n個類型(n) | an E元素，其類型的第n個同級 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E：第n個(n)類型 | an E元素，其類型的第n個同級，從最後一個計數 | [結構偽類](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

這是由於附加的html元素如 &lt;div> 標籤將在導入後添加到生成的Html中。

* 另外，不建議使用依賴於類似上述結構的指令碼與標籤為轉換為元件的元AEM素一起使用。
* 在標籤標籤上使用樣式進行元件轉換，如 &lt;div data-cq-component=&quot;&amp;ast;&quot;> 不推薦。
* 設計佈局應遵循HTML5 Boilerplate的最佳做法。 更多內容： [https://html5boilerplate.com/](https://html5boilerplate.com/)。

## 配置OSGI模組 {#configuring-osgi-modules}

公開可通過OSGI控制台配置的屬性的元件如下：

* 登錄頁設計導入程式
* 登錄頁生成器
* 移動登錄頁生成器
* 登錄頁條目預處理器

下表簡要介紹了這些屬性：

<table>
 <tbody>
  <tr>
   <td><strong>Component</strong></td>
   <td><strong>屬性名稱</strong></td>
   <td><strong>屬性說明 </strong></td>
  </tr>
  <tr>
   <td>登錄頁設計導入程式</td>
   <td>提取篩選器</td>
   <td>用於從抽取中篩選檔案的規則運算式清單。 <br /> 將從抽取中排除與任何指定模式匹配的Zip條目</td>
  </tr>
  <tr>
   <td>登錄頁生成器</td>
   <td>檔案模式</td>
   <td>可以將登錄頁生成器配置為處理與由檔案模式定義的規則運算式匹配的HTML檔案。</td>
  </tr>
  <tr>
   <td>移動登錄頁生成器</td>
   <td>檔案模式</td>
   <td>可以將登錄頁生成器配置為處理與由檔案模式定義的規則運算式匹配的HTML檔案。</td>
  </tr>
  <tr>
   <td> </td>
   <td>裝置群組</td>
   <td>要支援的設備組清單。</td>
  </tr>
  <tr>
   <td>登錄頁條目預處理器</td>
   <td>搜索模式 </td>
   <td>要在存檔條目內容中搜索的模式。 此規則運算式與條目內容逐行匹配。 匹配後，匹配文本將替換為指定的替換模式。<br /> <br /> 有關登錄頁條目預處理程式的當前限制，請參閱下面的注釋。</td>
  </tr>
  <tr>
   <td> </td>
   <td>替換陣列</td>
   <td>替換找到的匹配項的模式。 可以使用規則運算式組引用，如$1、$2。 此外，此模式支援在導入過程中使用實際值解析的關鍵字{designPath}。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**登錄頁條目預處理程式的當前限制：**
>如果需要對搜索模式進行任何更改，則在開啟felix屬性編輯器時，需要手動添加反斜線字元以轉義規則運算式元字元。 如果不手動添加反斜線字元，則規則運算式被視為無效，不會替換舊的。
>
>例如，如果預設配置為
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>你需要替換 >`CQ_DESIGN_PATH` 與 `VIPURL` 在搜索模式中，搜索模式應如下所示：
`/\* *VIPURL *\*/ *(['"])`

## 疑難排解 {#troubleshooting}

在導入設計包時，可能會遇到幾個錯誤，如本節所述。

### 使用登錄頁相關元件初始化側腳 {#initialization-of-sidekick-with-landing-page-relevant-components}

如果設計包包含parsys元件標籤，則在導入後，旁環開始顯示登錄頁相關元件。 可將新元件拖放到登錄頁中的parsys元件上。 您還可以進入設計模式，並將新元件添加到側腳。

### 導入期間顯示的錯誤消息 {#error-messages-displayed-during-import}

如果出現任何錯誤（例如，導入的包不是有效的zip），設計導入將不導入包，而是在拖放框正上方的頁面頂部顯示錯誤消息。 此處介紹了錯誤情形的示例。 更正錯誤後，可以將更新的zip重新導入到同一空白登錄頁。 引發錯誤的不同情況如下：

* 導入的設計包不是有效的zip存檔。
* 導入的設計包在頂層不包含index.html。

### 導入後顯示的警告 {#warnings-displayed-after-import}

如果出現任何警告(例如，HTML是指包中不存在的影像)，設計導入程式將導入zip，但同時在結果窗格上顯示問題/警告清單，按一下問題連結將顯示警告清單，指出設計包中的任何問題。 以下是設計導入程式捕獲和顯示警告的不同方案：

* HTML是指包中不存在的映像。
* HTML是指包中不存在的指令碼。
* HTML是指包中不存在的樣式。

### ZIP檔案的檔案儲存在哪AEM里？ {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

導入登錄頁後，檔案（影像、css、js等） 設計包內的以下位置儲存在AEM:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

假設登錄頁是在市場活動We.Retail下建立的，登錄頁的名稱是 **myBlankLandingPage** 然後儲存Zip檔案的位置如下：

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### 未保留格式 {#formatting-not-preserved}

建立CSS時，請注意以下限制：

如果文本和（可編輯）影像類似於以下內容：

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

在類上應用CSS `box` 如下：

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

然後 `box img` 在設計導入程式中使用，生成的登錄頁未保留格式。 要解決此問題，請注意在CSSAEM中添加div標籤並相應地重寫代碼。 否則，某些CSS規則將無效。

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
此外，設計人員應該知道， **id=cqcanvas** 標籤由導入程式識別，否則不會保留設計。
