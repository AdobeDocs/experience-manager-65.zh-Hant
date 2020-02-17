---
title: SCF車把助手
seo-title: SCF車把助手
description: 使用SCF的Handlebars Helper方法
seo-description: 使用SCF的Handlebars Helper方法
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# SCF車把助手 {#scf-handlebars-helpers}

| **[‹功能基本工具](essentials.md)** | **[伺服器端自訂‹](server-customize.md)** |
|---|---|
|  | **[用戶端自訂的‹](client-customize.md)** |

Handlebars Helpers（幫手）是可從Handlebars指令碼調用的方法，以便於與SCF元件配合工作。

實施包括客戶端和伺服器端定義。 開發人員也可以建立自訂的輔助工具。

隨AEM Communities提供的自訂SCF幫助器，在用戶端資料庫 [中定義](../../help/sites-developing/clientlibs.md):

* /etc/clientlibs/social/commons/scf/helpers.js

>[!NOTE]
>
>請務必安裝最 [新的Communities功能套件](deploy-communities.md#latestfeaturepack)。

## 縮寫 {#abbreviate}

協助程式，可傳回符合maxWords和maxLength屬性的縮寫字串。

要縮寫的字串會提供為內容。 如果未提供內容，則會傳回空字串。

首先，內容會修剪為maxLength，然後內容會切割為字詞並縮小為maxWords。

如果safeString設為true，則傳回的字串為SafeString。

### 參數 {#parameters}

* **內容**:字串

   （可選）預設為空字串

* **maxLength**:數字

   （可選）預設值是內容的長度。

* **maxWords**:數字

   （可選）預設為修剪字串中的字詞數。

* **safeString**:布林值

   （可選）若為true，則傳回Handlebars.SafeString()。 預設為false。

### 範例 {#examples}

```
{{abbreviate subject maxWords=2}}

/*
If subject =
    "AEM Communities - Site Creation Wizard"

Then abbreviate would return
    "AEM Communities".
*/
```

```
{{{abbreviate message safeString=true maxLength=30}}}

/*
If message =
    "The goal of AEM Communities is to quickly create a community engagement site."

Then abbreviate would return
    "The goal of AEM Communities is"
*/
```

## 內容載入更多資訊 {#content-loadmore}

在div下方新增兩個範圍的協助工具，一個用於全文，另一個用於較少的文字，並可在兩個檢視之間切換。

### 參數 {#parameters-1}

* **內容**:字串

   （可選）預設為空字串。

* **numChars**:數字

   （選用）不顯示全文時要顯示的字元數。 預設值為100。

* **moreText**:字串

   （選用）要顯示的文字，指出要顯示的文字較多。 預設為「更多」。

* **橢圓文字**:字串

   （選用）要顯示的文字，指出有隱藏文字。 預設值為&quot;。..&quot;。

* **safeString**:布林值

   （選用）布林值，指出是否在傳回結果前套用Handlebars.SafeString()。 預設為false。

### 例如 {#example}

```
{{content-loadmore  context numChars=32  moreText="go on"  ellipsesText="..." }}

/*
If context =
    "Here is the initial less content and this is more content."

Then content-loadmore would return
    "Here is the initial less content<span class="moreelipses">...</span> <span class="scf-morecontent"><span>and this is more content.</span>  <a href="" class="scf-morelink" evt="click=toggleContent">go on</a></span>"
*/
```

## DateUtil {#dateutil}

傳回格式化日期字串的協助工具。

### 參數 {#parameters-2}

* **內容**:數字

   （可選）從1970年1月1日（紀元）起的毫秒值偏移。 預設為目前日期。

* **格式**:字串

   （選用）要套用的日期格式。 預設值為&quot;YYYY-MM-DDTHH:mm:ss.sssZ&quot;，結果顯示為&quot;2015-03-18T18:17:13-07:00&quot;

### 範例 {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Equals {#equals}

依照等式條件傳回內容的輔助工具。

### 參數 {#parameters-3}

* **lvalue**:字串

   要比較的左側值

* **rvalue**:字串

   要比較的右側值

### 例如 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

一種塊幫助程式，它根據字串分隔的 [模式清單](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) ，測試WCM模式的當前值。

### 參數 {#parameters-4}

* **內容**:字串

   （選用）要翻譯的字串。 如果未提供預設值，則為必要值。

* **模式**:字串

   （選用）以逗號分隔的 [WCM模式清單](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) ，以測試是否已設定。

### 例如 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

這個助手會覆蓋Handlebars幫手&#39;i18n&#39;。

另請參 [閱「在JavaScript程式碼中國際化字串」](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)。

### 參數 {#parameters-5}

* **內容**:字串

   （選用）要翻譯的字串。 如果未提供預設值，則為必要值。

* **預設**:字串

   （選用）要翻譯的預設字串。 若未提供內容，則為必要項目。

* **注釋**:字串

   （可選）翻譯提示

### 例如 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Include {#include}

一種幫助程式，用於將元件作為模板中的非現有資源包括在一起。

這允許以寫程式方式定制資源，比以JCR節點添加的資源更容易。 請參 [閱添加或包含社群元件](scf.md#add-or-include-a-communities-component)。

只包含少數幾個Communities元件。 對於AEM 6.1，可包含的是 [注釋](essentials-comments.md)、評 [分](rating-basics.md)、審 [核](reviews-basics.md)和 [投](essentials-voting.md)票注釋。

此協助程式僅適用於伺服器端，提供類似 [cq:include](../../help/sites-developing/taglib.md) for JSP指令碼的功能。

### 參數 {#parameters-6}

* **內容**:字串或物件

   （可選，除非提供相對路徑）

   用 `this`於傳遞目前內容

   用於 `this.id` 獲取在上的資源，以 `id` 呈現請求的resourceType

* **resourceType**:字串

   （可選）資源類型將預設為上下文中的資源類型

* **範本**:字串

   元件指令碼的路徑

* **路徑**:字串

   （必要）資源的路徑。 如果路徑是相對的，則必須提供上下文，否則會傳回空字串。

* **編寫已停用**:布林值

   （可選）預設為false。 僅供內部使用。

### 例如 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

這將包含新的注釋元件，位 `this.id` 於+ /comments

## IncludeClientLib {#includeclientlib}

包含AEM html用戶端資料庫的協助工具，可以是js、css或主題資料庫。 對於不同類型的多個包含項目（例如js和css），此標籤需要在Handlebars指令碼中多次使用。

此協助程式僅適用於伺服器端，提供類似 [ui:includeClientLib](../../help/sites-developing/taglib.md) for JSP指令碼的功能。

### 參數 {#parameters-7}

* **類別**:字串

   （可選）逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有Javascript和CSS程式庫。 主題名稱會從請求中擷取。

* **主題**:字串

   （可選）逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有主題相關程式庫（CSS和JS）。 主題名稱會從請求中擷取。

* **js**:字串

   （可選）逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有Javascript程式庫。

* **css**:字串

   （可選）逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有CSS程式庫。

### 範例 {#examples-2}

```
// all: js + theme (theme-js + css)
{{includeClientLib categories="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// only js libs
{{includeClientLib js="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// theme only (theme-js + css)
{{includeClientLib theme="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// css only
{{includeClientLib css="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
```

## Pretty-time {#pretty-time}

一種幫助程式，用於顯示已經過多少時間到截止點，之後顯示常規日期格式。

例如：

* 12小時前
* 7天前

### 參數 {#parameters-8}

* **內容**:數字

   過去與「現在」比較的時間。 時間表示為自1970年1月1日（時元）起的毫秒值偏移。

* **daysCutform**:數字

   切換到實際日期前的天數。 預設值為60。

### 例如 {#example-5}

```
{{pretty-time this.published daysCutoff=7}}

/*
Depending on how long in the past, may return

  "3 minutes ago"

  "3 hours ago"

  "3 days ago"
*/
```

## Xss-html {#xss-html}

為HTML元素內容編碼來源字串以協助防範XSS的輔助程式。

注意：這不是驗證器，不用於寫入屬性值。

### 參數 {#parameters-9}

* **內容**:物件

   要編碼的HTML

### 例如 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

一種幫助程式，用於對源字串進行編碼，以便寫入HTML屬性值，以幫助防止XSS。

注意：這不是驗證器，不用於寫入actionalable屬性（href、src、事件處理常式）。

### 參數 {#parameters-10}

* **內容**:物件

   要編碼的HTML

### 例如 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

一種協助程式，可編碼來源字串以寫入JavaScript字串內容，以協助防範XSS。

注意：這不是驗證器，不用於寫入任意JavaScript。

### 參數 {#parameters-11}

* **內容**:物件

   要編碼的HTML

### 例如 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

協助程式，可淨化URL，將其寫入為HTML href或srce屬性值，以協助防範XSS。

注意：這可能會傳回空字串

### 參數 {#parameters-12}

* **內容**:物件

   要淨化的URL

### 例如 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js基本概述 {#handlebars-js-basic-overview}

從 [Handlebars.js檔案快速概觀協助功能](https://handlebarsjs.com/expressions.html):

* Handlebars協助呼叫是簡單的識別碼（協助程式的*name *），後面接著零個或多個空格分隔的參數。
* 參數可以是簡單的字串、數字、布林值或JSON物件，以及可選的索引鍵值配對（雜湊引數）序列，做為最後一個參數。
* 雜湊引數中的索引鍵必須是簡單識別碼。
* 雜湊引數中的值是Handlebars運算式：簡單識別碼、路徑或字串。
* Handlebars幫手 `this`隨時都能找到目前的情境。
* 上下文可以是字串、數字、布林值或JSON資料物件。
* 可以將嵌套在當前上下文中的對象作為上下文傳遞，例如 `this.url` 或 `this.id` （請參見以下簡單和塊幫助器示例）。

* 區塊輔助工具是可從範本中任何位置呼叫的功能。 他們每次都可以使用不同的上下文，叫用範本的區塊零次或多次。 它們包含{{#*name*}}和{{/*name*}}之間的上下文。

* Handlebars為名為「選項」的幫手提供最終參數。 特殊物件「選項」包括

   * 可選私人資料(options.data)
   * 來自呼叫的可選金鑰值屬性(options.hash)
   * 能夠調用自身(options.fn())
   * 能夠叫用本身的逆函式(options.inverse())

* 建議從協助程式傳回的HTML字串內容為SafeString。

### Handlebars.js檔案中的簡單輔助工具範例： {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>{{#posts}}<li>{{{link_to "Post"}}}</li>{{/posts}}</ul>'

var template = Handlebars.compile(source);

template(context);
```

會演算：

&lt;ul>&lt;li>&lt;a href=&quot;/pots/hello-world&quot;>貼文！&lt;/a>&lt;/li>&lt;/ul>

### Handlebars.js檔案中的區塊輔助工具範例： {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

會演算：&lt;ul>&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>&lt;/ul>

## 定制SCF幫助器 {#custom-scf-helpers}

自訂輔助工具必須在伺服器端和用戶端上實作，尤其是在傳送資料時。 對於SCF，當伺服器在要求頁面時，會針對特定元件產生HTML時，大部份的範本都會在伺服器端編譯和轉譯。

### 伺服器端自訂協助工具 {#server-side-custom-helpers}

若要在伺服器端實作和註冊自訂SCF協助程式，只需實作Java介面 [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)，將它設為 [](../../help/sites-developing/the-basics.md#osgi) OSGi服務，並將它安裝為OSGi套件的一部分。

例如：

### FooTextHelper.java {#footexthelper-java}

```java
/** Custom Handlebars Helper */

package com.my.helpers;

import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

import com.adobe.cq.social.handlebars.api.TemplateHelper;
import com.github.jknack.handlebars.Options;

@Service
@Component
public class FooTextHelper implements TemplateHelper<String>{

    @Override
    public CharSequence apply(String context, Options options) throws IOException {
        return "foo-" + context;
    }

    @Override
    public String getHelperName() {
        return "foo-text";
    }

    @Override
    public Class<String> getContextType() {
        return String.class;
    }
}
```

>[!NOTE]
>
>還必須為伺服器端建立幫助程式。
>
>該元件在登錄用戶的客戶端上重新呈現，如果找不到客戶端幫助程式，則該元件將消失。

### 用戶端自訂協助工具 {#client-side-custom-helpers}

客戶端幫助者是通過調用註冊的Handlebars指令碼 `Handlebars.registerHelper()`。
例如：

### custom-helpers.js {#custom-helpers-js}

```
function(Handlebars, SCF, $CQ) {

    Handlebars.registerHelper('foo-text', function(context, options) {
        if (!context) {
            return "";
        }
        return "foo-" + context;
    });

})(Handlebars, SCF, $CQ);
```

自訂用戶端協助工具必須新增至自訂用戶端程式庫。
clientlib必須：

* 包含依賴項 `cq.social.scf`
* 在Handlebars載入後載入
* 包含在 [內](clientlibs.md)

注意：SCF幫助器的定義如 `/etc/clientlibs/social/commons/scf/helpers.js`中。

| **[‹功能基本工具](essentials.md)** | **[伺服器端自訂‹](server-customize.md)** |
|---|---|
|  | **[用戶端自訂的‹](client-customize.md)** |

