---
title: SCF Handlebars幫助器
seo-title: SCF Handlebars幫助器
description: Handlebars幫助程式方法便於使用SCF
seo-description: Handlebars幫助程式方法便於使用SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 1%

---

# SCF Handlebars Helpers {#scf-handlebars-helpers}

| **[⇐功能要點](essentials.md)** | **[伺服器端自訂⇒](server-customize.md)** |
|---|---|
|  | **[用戶端自訂⇒](client-customize.md)** |

Handlebars Helpers（幫助器）是可從Handlebars指令碼調用的方法，以便於使用SCF元件。

實施包含用戶端和伺服器端定義。 開發人員也可以建立自訂的協助工具。

隨AEM Communities提供的自定義SCF幫助器在[客戶端庫](../../help/sites-developing/clientlibs.md)中定義：

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>請務必安裝[最新的Communities功能包](deploy-communities.md#latestfeaturepack)。

## 縮略 {#abbreviate}

協助者，可傳回符合maxWords和maxLength屬性的縮寫字串。

要縮寫的字串會提供為內容。 如果未提供內容，則會傳回空字串。

首先，上下文被裁切為maxLength，然後上下文被切割為單詞，並減為maxWords。

如果safeString設為true，則返回的字串為SafeString。

### 參數 {#parameters}

* **內容**:字串

   （選用）預設為空字串

* **maxLength**:數字

   （選用）預設為內容的長度。

* **maxWords**:數字

   （選用）預設為裁切字串中的字詞數。

* **safeString**:布林值

   （選用）若為true，則傳回Handlebars.SafeString()。 預設為false。

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

## Content-loadmore {#content-loadmore}

協助您在div下方新增兩個範圍，一個適用於全文，另一個適用於較少的文字，並可在兩個檢視之間切換。

### 參數 {#parameters-1}

* **內容**:字串

   （選用）預設為空字串。

* **numChars**:數字

   （選用）未顯示全文時要顯示的字元數。 預設為100。

* **更多文字**:字串

   （可選）要顯示的文字，指出要顯示的文字更多。 預設為「更多」。

* **點文字**:字串

   （可選）要顯示的文字，指出有隱藏的文字。 預設為「……」。

* **safeString**:布林值

   （選用）布林值，指出是否要在傳回結果之前套用Handlebars.SafeString()。 預設為false。

### 範例 {#example}

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

傳回格式化日期字串的協助程式。

### 參數 {#parameters-2}

* **內容**:數字

   （選用）從1970年1月1日(Epoch)起的毫秒數值偏移。 預設為目前日期。

* **格式**:字串

   （選用）要套用的日期格式。 預設值為&quot;YYYY-MM-DDTHH:mm:ss.ssZ&quot;，結果顯示為&quot;2015-03-18T18:17:13-07:00&quot;

### 範例{#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## 等於 {#equals}

根據相等條件傳回內容的協助者。

### 參數 {#parameters-3}

* **值**:字串

   要比較的左手值。

* **值**:字串

   要比較的右側值。

### 範例 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

一種塊輔助程式，用於根據字串分隔的模式清單測試[WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html)的當前值。

### 參數 {#parameters-4}

* **內容**:字串

   （選用）要翻譯的字串。 若未提供預設值，則為必要。

* **模式**:字串

   （選用）以逗號分隔的[WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html)清單，以測試是否已設定。

### 範例 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

該幫手將覆蓋Handlebars幫手「i18n」。

另請參閱[在JavaScript程式碼](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)中將字串國際化。

### 參數 {#parameters-5}

* **內容**:字串

   （選用）要翻譯的字串。 若未提供預設值，則為必要。

* **預設**:字串

   （選用）要翻譯的預設字串。 若未提供內容，則為必要。

* **註解**:字串

   （選用）翻譯提示

### 範例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 包括 {#include}

在範本中將元件作為非現有資源的協助程式。

這允許以寫程式方式定制資源，比添加為JCR節點的資源的可能性更容易。 請參閱[添加或包含社區元件](scf.md#add-or-include-a-communities-component)。

只有選取的幾個Communities元件是可包含的。 對於AEM 6.1，可包含的包括[comments](essentials-comments.md)、[rating](rating-basics.md)、[reviews](reviews-basics.md)和[voting](essentials-voting.md)。

此協助程式僅適用於伺服器端，提供與JSP指令碼的[cq:include](../../help/sites-developing/taglib.md)類似的功能。

### 參數 {#parameters-6}

* **內容**:字串或物件

   （可選，除非提供相對路徑）

   使用`this`傳遞當前上下文。

   使用`this.id`在`id`獲取資源，以呈現請求的resourceType。

* **resourceType**:字串

   （可選）資源類型將預設為上下文中的資源類型。

* **範本**:字串

   元件指令碼的路徑。

* **路徑**:字串

   （必要）資源的路徑。 如果路徑為相對路徑，則必須提供內容，否則會傳回空字串。

* **authoringDisabled**:布林值

   （選用）預設為false。 僅供內部使用。

### 範例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

這將包括位於`this.id` + /comments的新注釋元件。

## IncludeClientLib {#includeclientlib}

包含AEM html用戶端程式庫的協助程式，可以是js、css或主題程式庫。 對於不同類型的多個包含（例如js和css），此標籤需要在Handlebars指令碼中使用多次。

此幫助程式僅適用於伺服器端，它提供的功能與JSP指令碼的[ui:includeClientLib](../../help/sites-developing/taglib.md)類似。

### 參數 {#parameters-7}

* **類別**:字串

   （選用）逗號分隔的用戶端程式庫類別清單。 這會包含指定類別的所有Javascript和CSS程式庫。 主題名稱會從請求中擷取。

* **主題**:字串

   （選用）逗號分隔的用戶端程式庫類別清單。 這將包含指定類別的所有主題相關程式庫（包括CSS和JS）。 主題名稱會從請求中擷取。

* **js**:字串

   （選用）逗號分隔的用戶端程式庫類別清單。 這會包含指定類別的所有Javascript程式庫。

* **css**:字串

   （選用）逗號分隔的用戶端程式庫類別清單。 這會包含指定類別的所有CSS程式庫。

### 範例{#examples-2}

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

顯示已經過多少時間到截止點的協助程式，之後會顯示一般日期格式。

例如：

* 12小時前
* 7天前

### 參數 {#parameters-8}

* **內容**:數字

   以前比較「現在」的時間。 時間以毫秒值表示，從1970年1月1日(Epoch)算起。

* **daysCustoft**:數字

   切換為實際日期前的天數。 預設為60。

### 範例 {#example-5}

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

為HTML元素內容編碼源字串以幫助防止XSS的幫助程式。

注意：這不是驗證器，也不用於寫入屬性值。

### 參數 {#parameters-9}

* **內容**:物件

   要編碼的HTML。

### 範例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

一種幫助程式，對源字串進行編碼，以便寫入到HTML屬性值，以幫助防止XSS。

注意：這不是驗證器，也不用於寫入可動作屬性（href、src、事件處理常式）。

### 參數 {#parameters-10}

* **內容**:物件

   要編碼的HTML。

### 範例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

一種協助程式，可對來源字串進行編碼，以便寫入JavaScript字串內容，以協助抵御XSS。

注意：這不是驗證器，也不用於寫入至任意JavaScript。

### 參數 {#parameters-11}

* **內容**:物件

   要編碼的HTML。

### 範例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

協助程式，可處理URL，將其寫入為HTML href或srce屬性值，以協助防範XSS。

注意：這可能會傳回空字串

### 參數 {#parameters-12}

* **內容**:物件

   要處理的URL。

### 範例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js基本概述{#handlebars-js-basic-overview}

[Handlebars.js檔案](https://handlebarsjs.com/expressions.html)中協助函式的快速概述：

* Handlebars幫手調用是簡單的標識符（幫手的&#x200B;*name*），後面跟著零個或多個以空格分隔的參數。
* 參數可以是簡單的字串、數字、布林值或JSON物件，以及作為最後一個參數的機碼值組（雜湊引數）的選用序列。
* 雜湊引數中的金鑰必須是簡單識別碼。
* 雜湊引數中的值是Handlebars運算式：簡單識別碼、路徑或字串。
* 當前上下文`this`始終可用於Handlebars幫手。
* 內容可以是字串、數字、布林值或JSON資料物件。
* 可以將嵌套在當前上下文中的對象作為上下文傳遞（例如`this.url`或`this.id`）（請參見以下簡單和塊幫助器示例）。

* 塊幫助程式是可以從模板中的任何位置調用的函式。 他們每次都可透過不同內容叫用範本區塊零次或多次。 它們包含{{#*name*}}和{{/*name*}}之間的上下文。

* Handlebars為名為「options」的幫手提供最終參數。 特殊物件「options」包括

   * 可選專用資料(options.data)
   * 呼叫的選用索引鍵值屬性(options.hash)
   * 調用本身(options.fn())
   * 調用本身的逆函式(options.inverse())

* 建議從協助程式傳回的HTML字串內容為SafeString。

### Handlebars.js檔案中的簡單協助程式範例：{#an-example-of-a-simple-helper-from-handlebars-js-documentation}

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

會呈現：

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>貼！&lt;/a>&lt;/li>
&lt;/ul>

### Handlebars.js檔案中的區塊協助程式範例：{#an-example-of-a-block-helper-from-handlebars-js-documentation}

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

會呈現：
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>耶胡達&lt;/a>&lt;/li>
&lt;/ul>

## 自定義SCF幫助器{#custom-scf-helpers}

必須在伺服器端和用戶端上實作自訂協助程式，尤其是在傳送資料時。 對於SCF，當伺服器在請求頁面時為指定元件生成HTML時，大多數模板都在伺服器端編譯和呈現。

### 伺服器端自訂協助程式{#server-side-custom-helpers}

若要在伺服器端實作和註冊自訂SCF協助程式，只需實作Java介面[TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)，將其設為[OSGi服務](../../help/sites-developing/the-basics.md#osgi)，並作為OSGi套件的一部分進行安裝即可。

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
>也必須為用戶端建立為伺服器端建立的協助程式。
>
>在登入使用者的用戶端上會重新轉譯元件，如果找不到用戶端協助程式，元件就會消失。

### 客戶端自定義幫助器{#client-side-custom-helpers}

客戶端幫助程式是通過調用`Handlebars.registerHelper()`註冊的Handlebars指令碼。
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

必須將自訂用戶端協助程式新增至自訂用戶端程式庫。
clientlib必須：

* 包括對`cq.social.scf`的依賴項。
* 載入Handlebars後載入。
* [included](clientlibs.md)。

注意：在`/etc/clientlibs/social/commons/scf/helpers.js`中定義了SCF幫助器。

| **[⇐功能要點](essentials.md)** | **[伺服器端自訂⇒](server-customize.md)** |
|---|---|
|  | **[用戶端自訂⇒](client-customize.md)** |
