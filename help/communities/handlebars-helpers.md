---
title: SCF把手幫助器
seo-title: SCF Handlebars Helpers
description: 使用SCF方便工作的Handlebar Helper方法
seo-description: Handlebars Helper methods to facilitate work with SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 2%

---

# SCF把手幫助器 {#scf-handlebars-helpers}

| **[⇐功能要點](essentials.md)** | **[伺服器端定制⇒](server-customize.md)** |
|---|---|
|  | **[客戶端定制⇒](client-customize.md)** |

Handlebar Helpers（幫助程式）是從Handlebar指令碼調用的方法，以便於使用SCF元件。

該實現包括客戶端和伺服器端定義。 開發人員也可以建立自定義幫助程式。

與AEM Communities一起提供的自定義SCF幫助器在 [客戶端庫](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>確保安裝 [最新社區功能包](deploy-communities.md#latestfeaturepack)。

## 縮寫 {#abbreviate}

返回符合maxWords和maxLength屬性的縮寫字串的幫助程式。

要縮寫的字串將作為上下文提供。 如果未提供上下文，則返回空字串。

首先，將上下文裁切為maxLength，然後將上下文切割為單詞，並縮小為maxWords。

如果safeString設定為true，則返回的字串為SafeString。

### 參數 {#parameters}

* **上下文**:字串

   （可選）預設值為空字串

* **最大長度**:數字

   （可選）預設值是上下文的長度。

* **最大字數**:數字

   （可選）預設值是修剪字串中的字數。

* **safeString**:布爾型

   （可選）如果為true，則返回Handlebars.SafeString()。 預設值為false。

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

## 內容載入更多 {#content-loadmore}

在div下添加兩個跨度的幫助程式，一個用於全文，另一個用於較少的文本，能夠在兩個視圖之間切換。

### 參數 {#parameters-1}

* **上下文**:字串

   （可選）預設值為空字串。

* **數字字元**:數字

   （可選）不顯示全文時要顯示的字元數。 預設值為100。

* **更多文本**:字串

   （可選）要顯示的文本，指示要顯示的文本更多。 預設值為「更多」。

* **橢圓文本**:字串

   （可選）要顯示的文本，指示存在隱藏文本。 預設值為「……」。

* **safeString**:布爾型

   （可選）布爾值，指示是否在返回結果之前應用Handlebars.SafeString()。 預設值為false。

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

返回格式化日期字串的幫助程式。

### 參數 {#parameters-2}

* **上下文**:數字

   （可選）從1970年1月1日（新紀元）起的毫秒值偏移。 預設值是當前日期。

* **格式**:字串

   （可選）要應用的日期格式。 預設值為「YYYY-MM-DDTHH」:mm:ss.sssZ」，結果顯示為「2015-03-18T18」:17:13-07:00英吋

### 範例 {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## 等於 {#equals}

根據等式條件返回內容的幫助器。

### 參數 {#parameters-3}

* **值**:字串

   要比較的左手值。

* **值**:字串

   要比較的右邊值。

### 範例 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm模式 {#if-wcm-mode}

test當前值的塊幫助程式 [WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 以字串分隔的模式清單。

### 參數 {#parameters-4}

* **上下文**:字串

   （可選）要轉換的字串。 如果未提供預設值，則為必需。

* **模式**:字串

   （可選）逗號分隔的清單 [WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) test。

### 範例 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

此幫助程式覆蓋Handlebars幫助程式「i18n」。

另請參閱 [在JavaScript代碼中國際化字串](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)。

### 參數 {#parameters-5}

* **上下文**:字串

   （可選）要轉換的字串。 如果未提供預設值，則為必需。

* **預設**:字串

   （可選）要轉換的預設字串。 如果未提供上下文，則為必需欄位。

* **注釋**:字串

   （可選）翻譯提示

### 範例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 包括 {#include}

一種幫助器，用於將元件作為模板中的非現有資源包括。

這允許比作為JCR節點添加的資源更容易地以寫程式方式定制資源。 請參閱 [添加或包括社區元件](scf.md#add-or-include-a-communities-component)。

只包括少數幾個「社區」元件。 對於AEM6.1，可包含的 [評論](essentials-comments.md)。 [評級](rating-basics.md)。 [回顧](reviews-basics.md), [投票](essentials-voting.md)。

此幫助程式僅適用於伺服器端，提供類似於 [cq：包括](../../help/sites-developing/taglib.md) JSP指令碼。

### 參數 {#parameters-6}

* **上下文**:字串或對象

   （可選，除非提供相對路徑）

   使用 `this` 來修改標籤元素的屬性。

   使用 `this.id` 在 `id` 請求的resourceType。

* **資源類型**:字串

   （可選）資源類型將預設為上下文中的資源類型。

* **模板**:字串

   元件指令碼的路徑。

* **路徑**:字串

   （必需）資源路徑。 如果路徑是相對的，則必須提供上下文，否則返回空字串。

* **創作已禁用**:布爾型

   （可選）預設值為false。 僅供內部使用。

### 範例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

這將包括位於 `this.id` + /注釋。

## 包括客戶端庫 {#includeclientlib}

一種幫助程式，AEM包括html客戶端庫，該庫可以是js、css或主題庫。 對於多個不同類型的inclusion，例如js和css，需要在Handlebars指令碼中多次使用此標籤。

此幫助程式僅適用於伺服器端，提供類似於 [ui:includeClientLib](../../help/sites-developing/taglib.md) JSP指令碼。

### 參數 {#parameters-7}

* **類別**:字串

   （可選）以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有Javascript和CSS庫。 主題名稱從請求中提取。

* **主題**:字串

   （可選）以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有主題相關庫（CSS和JS）。 主題名稱從請求中提取。

* **j**:字串

   （可選）以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有Javascript庫。

* **cs**:字串

   （可選）以逗號分隔的客戶端庫類別清單。 這將包括給定類別的所有CSS庫。

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

## 《美麗時光》 {#pretty-time}

一種幫助器，用於顯示已經過到截止點的時間，在截止點之後顯示常規日期格式。

例如：

* 12小時前
* 7天前

### 參數 {#parameters-8}

* **上下文**:數字

   過去與「現在」比較的時間。 時間表示為1970年1月1日（新紀元）起的毫秒值偏移量。

* **天截止**:數字

   切換到實際日期前的天數。 預設值為60。

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

一種幫助程式，其對用於HTML元素內容的源字串進行編碼以幫助防止XSS。

注：這不是驗證程式，不用於寫入屬性值。

### 參數 {#parameters-9}

* **上下文**:對象

   要編碼的HTML。

### 範例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

一種幫助器，其編碼用於寫入到HTML屬性值以幫助防止XSS的源字串。

注：這不是驗證程式，不用於寫入actionalable屬性（href、src、事件處理程式）。

### 參數 {#parameters-10}

* **上下文**:對象

   要編碼的HTML。

### 範例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-js字串 {#xss-jsstring}

一種幫助程式，它編碼用於寫入JavaScript字串內容的源字串，以幫助防止XSS。

注：這不是驗證程式，不用於寫入任意JavaScript。

### 參數 {#parameters-11}

* **上下文**:對象

   要編碼的HTML。

### 範例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

清除URL以作為HTMLhref或srce屬性值寫入以幫助防止XSS的幫助程式。

注：這可能返回空字串

### 參數 {#parameters-12}

* **上下文**:對象

   要清理的URL。

### 範例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js基本概述 {#handlebars-js-basic-overview}

* Handlebars幫助調用是一個簡單的標識符( *名稱* )，後跟零個或多個空分參數。
* 參數可以是簡單的String、number、boolean或JSON對象，以及作為最後一個參數的鍵值對（散列參數）的可選序列。
* 哈希參數中的鍵必須是簡單標識符。
* 哈希參數中的值是Handlebars表達式：簡單標識符、路徑或字串。
* 當前上下文， `this`，始終可用於Handlebar幫助程式。
* 上下文可以是String、number、Boolean或JSON資料對象。
* 可以將嵌套在當前上下文中的對象作為上下文傳遞，例如 `this.url` 或 `this.id` （請參見以下簡單和塊幫助程式示例）。

* 塊幫助程式是可以從模板中任何位置調用的函式。 它們每次都可以調用模板塊零次或多次，並且具有不同的上下文。 它們包含一個上下文 {{#*name*}} and {{/*name*}}。

* Handlebars為名為「options」的幫助程式提供最終參數。 特殊對象「options」包括

   * 可選專用資料(options.data)
   * 調用的可選鍵值屬性(options.hash)
   * 能夠調用自身(options.fn())
   * 能夠調用其本身的逆(options.inverse())

* 建議從幫助程式返回的HTML字串內容是SafeString。

### Handlebars.js文檔中的簡單幫助程式示例： {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

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

將呈現：

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>貼！&lt;/a>&lt;/li>
&lt;/ul>

### Handlebars.js文檔中的塊幫助程式示例： {#an-example-of-a-block-helper-from-handlebars-js-documentation}

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

將呈現：
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>艾倫&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>耶胡達&lt;/a>&lt;/li>
&lt;/ul>

## 自定義SCF幫助程式 {#custom-scf-helpers}

必須在伺服器端和客戶端上實現自定義幫助程式，尤其是在傳遞資料時。 對於SCF，當伺服器在請求頁面時為給定元件生成HTML時，大多數模板都在伺服器端編譯和呈現。

### 伺服器端自定義幫助程式 {#server-side-custom-helpers}

要在伺服器端實現和註冊自定義SCF幫助程式，只需實現Java介面 [模板幫助程式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)，使其 [OSGi服務](../../help/sites-developing/the-basics.md#osgi) 並作為OSGi捆綁包的一部分安裝。

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
>還必須為客戶端建立為伺服器端建立的幫助程式。
>
>元件在登錄用戶的客戶端上重新呈現，如果找不到客戶端幫助程式，則元件將消失。

### 客戶端自定義幫助程式 {#client-side-custom-helpers}

客戶端幫助程式是通過調用 `Handlebars.registerHelper()`。
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

必須將自定義客戶端幫助程式添加到自定義客戶端庫。
客戶端庫必須：

* 包括依賴項 `cq.social.scf`。
* 載入Handlebar後載入。
* 是 [包括](clientlibs.md)。

注：SCF幫助程式在 `/etc/clientlibs/social/commons/scf/helpers.js`。

| **[⇐功能要點](essentials.md)** | **[伺服器端定制⇒](server-customize.md)** |
|---|---|
|  | **[客戶端定制⇒](client-customize.md)** |
