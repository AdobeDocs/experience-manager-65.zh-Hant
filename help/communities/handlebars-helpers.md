---
title: SCF Handlebars協助程式
description: Handlebars Helper方法可加快處理SCF的速度
topic-tags: developing
content-type: reference
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 2%

---

# SCF Handlebars協助程式 {#scf-handlebars-helpers}

| **[⇐功能要點](essentials.md)** | **[伺服器端自訂⇒](server-customize.md)** |
|---|---|
|   | **[使用者端自訂⇒](client-customize.md)** |

Handlebars Helpers （協助程式）是可從Handlebars指令碼呼叫的方法，以方便使用SCF元件。

實施包含使用者端和伺服器端定義。 開發人員也可以建立自訂協助程式。

AEM Communities提供的自訂SCF協助程式定義於 [使用者端資料庫](../../help/sites-developing/clientlibs.md)：

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>請務必安裝 [最新Communities Feature Pack](deploy-communities.md#latestfeaturepack).

## 縮寫 {#abbreviate}

協助程式傳回符合maxWords和maxLength屬性的縮寫字串。

提供要縮寫的字串作為內容。 如果未提供任何內容，則會傳回空字串。

首先，將前後關聯裁剪為maxLength，然後將前後關聯分割為單字並縮小為maxWords。

如果safeString設為true，則傳回的字串為SafeString。

### 參數 {#parameters}

* **內容**：字串

  （選用）預設為空字串

* **maxLength**：數字

  （選用）預設值是前後關聯的長度。

* **maxWords**：數字

  （選用）預設值是裁剪字串中的字數。

* **safeString**：布林值

  （選用）如果為true，則傳回Handlebars.SafeString()。 預設值為false。

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

協助程式可在div下新增兩個跨頁，一個用於全文，另一個用於較少文字，並能在兩個檢視之間切換。

### 參數 {#parameters-1}

* **內容**：字串

  （選用）預設為空字串。

* **numChars**：數字

  （選用）不顯示全文時顯示的字元數。 預設值為100。

* **更多文字**：字串

  （選用）要顯示的文字，表示還有更多文字要顯示。 預設值為「更多」。

* **省略文字**：字串

  （選用）要顯示的文字，表示有隱藏的文字。 預設值為「……」。

* **safeString**：布林值

  （選用）布林值，指出在傳回結果之前是否要套用Handlebars.SafeString()。 預設值為false。

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

協助程式可傳回格式化的日期字串。

### 參數 {#parameters-2}

* **內容**：數字

  （選用）從1970年1月1日起位移的毫秒值（紀元）。 預設值為目前日期。

* **格式**：字串

  （選用）要套用的日期格式。 預設為&quot;`YYYY-MM-DDTHH:mm:ss.sssZ`&quot;，結果將顯示為&quot;`2015-03-18T18:17:13-07:00`&quot;

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

根據等式條件傳回內容的協助程式。

### 參數 {#parameters-3}

* **值**：字串

  要比較的左側值。

* **值**：字串

  要比較的右側值。

### 範例 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
`{{else}}`
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

區塊協助程式會測試目前的值， [WCM模式](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 針對以字串分隔的模式清單。

### 參數 {#parameters-4}

* **內容**：字串

  （選用）要翻譯的字串。 若未提供預設值，則為必要。

* **模式**：字串

  （選用）逗號分隔清單 [WCM模式](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 以測試是否設定。

### 範例 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{else}}
 ...
`{{/if-wcm-mode}}`
```

## i18n {#i-n}

此協助程式會覆寫Handlebars協助程式&#39;i18n&#39;。

另請參閱 [在JavaScript程式碼中國際化字串](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### 參數 {#parameters-5}

* **內容**：字串

  （選用）要翻譯的字串。 若未提供預設值，則為必要。

* **預設**：字串

  （選用）要翻譯的預設字串。 如果未提供內容，則為必要。

* **評論**：字串

  （選用）翻譯提示

### 範例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 包含 {#include}

將元件加入為範本中不存在資源的協助程式。

與新增為JCR節點的資源相比，此方法讓資源更容易以程式設計方式自訂。 另請參閱 [新增或包含Communities元件](scf.md#add-or-include-a-communities-component).

只有少數幾個社群元件可供包含。 <!-- OBSOLETE/OLD  NEED TO UPDATE FOR 6.5  For AEM 6.1, those that are includable are [comments](essentials-comments.md), [rating](rating-basics.md), [reviews](reviews-basics.md), and [voting](essentials-voting.md). -->

此協助程式僅適用於伺服器端，可提供類似以下的功能 [cq：include](../../help/sites-developing/taglib.md) 用於JSP指令碼。

### 參數 {#parameters-6}

* **內容**：字串或物件

  （選擇性，除非提供相對路徑）

  使用 `this` 以傳遞目前內容。

  使用 `this.id` 若要取得資源，請前往 `id` 用於呈現請求的resourceType。

* **resourceType**：字串

  （選擇性）資源型別預設為來自前後關聯的資源型別。

* **範本**：字串

  元件指令碼的路徑。

* **路徑**：字串

  （必要）資源的路徑。 如果路徑是相對路徑，則必須提供上下文，否則會傳回空字串。

* **authoringDisabled**：布林值

  （選用）預設為false。 僅供內部使用。

### 範例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

在包含新的註釋元件 `this.id` + /comments。

## IncludeClientLib {#includeclientlib}

包含AEM html使用者端程式庫的協助程式，可以是js、css或主題程式庫。 對於不同型別的多個包含專案（例如js和css），此標籤必須在Handlebars指令碼中多次使用。

此協助程式僅適用於伺服器端，可提供類似以下的功能 [ui：includeClientLib](../../help/sites-developing/taglib.md) 用於JSP指令碼。

### 參數 {#parameters-7}

* **類別**：字串

  （選用）以逗號分隔的使用者端程式庫類別清單。 納入指定類別的所有JavaScript和CSS資料庫。 主題名稱會從請求中擷取。

* **主題**：字串

  （選用）以逗號分隔的使用者端程式庫類別清單。 包含指定類別的所有主題相關資料庫（CSS和JS）。 主題名稱會從請求中擷取。

* **js**：字串

  （選用）以逗號分隔的使用者端程式庫類別清單。 包含指定類別的所有JavaScript程式庫。

* **css**：字串

  （選用）以逗號分隔的使用者端程式庫類別清單。 包含指定類別的所有CSS資料庫。

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

## 美化時間 {#pretty-time}

協助程式會顯示到達截止點之前經過的時間，之後會顯示一般日期格式。

例如：

* 12小時前
* 7天前

### 參數 {#parameters-8}

* **內容**：數字

  與「現在」進行比較的過去時間。 時間以自1970年1月1日起位移的毫秒值表示（紀元）。

* **daysCutoff**：數字

  切換到實際日期之前的天數。 預設值為60。

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

協助程式會為HTML元素內容編碼來源字串，以協助抵禦XSS。

注意：此協助程式不是驗證器，且不可用於寫入屬性值。

### 參數 {#parameters-9}

* **內容**：物件

  要編碼的HTML。

### 範例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

協助程式會編碼來源字串，以寫入HTML屬性值，協助防範XSS。

注意：此協助程式不是驗證器，且不可用於撰寫可操作的屬性（href、src、事件處理常式）。

### 參數 {#parameters-10}

* **內容**：物件

  要編碼的HTML。

### 範例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

協助程式會編碼來源字串，以寫入JavaScript字串內容來協助防範XSS。

注意：此協助程式不是驗證器，且不可用來寫入任意JavaScript。

### 參數 {#parameters-11}

* **內容**：物件

  要編碼的HTML。

### 範例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

協助程式會清理要當作HTMLhref或srce屬性值寫入的URL，以協助防範XSS。

注意：此協助程式可能會傳回空字串。

### 參數 {#parameters-12}

* **內容**：物件

  要清理的URL。

### 範例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js基本概述 {#handlebars-js-basic-overview}

* Handlebars協助程式呼叫是簡單的識別碼(識別碼 *名稱* 後接零個或多個以空格分隔的引數。
* 引數可以是簡單字串、數字、布林值或JSON物件，以及作為最後一個引數的鍵值值配對（雜湊引數）選用序列。
* 雜湊引數中的索引鍵必須是簡單識別碼。
* 雜湊引數中的值是Handlebars運算式：簡單識別碼、路徑或字串。
* 目前的內容， `this`，Handlebars協助程式一律可使用。
* 內容可以是字串、數字、布林值或JSON資料物件。
* 可以將目前前後關聯內的巢狀物件作為前後關聯傳遞，例如 `this.url` 或 `this.id` （請參閱下列簡單和區塊協助程式的範例）。

* 區塊協助程式是可從範本中任何位置呼叫的函式。 他們每次可使用不同的內容呼叫範本區塊零次或多次。 它們包含介於以下兩者之間的內容： `{{#*name*}}` 和 `{{/*name*}}`.

* Handlebars為名為&#39;options&#39;的協助程式提供最終引數。 特殊物件&#39;options&#39;包括

   * 選擇性私人資料(options.data)
   * 呼叫的選用機碼值屬性(options.hash)
   * 啟動本身的功能(options.fn())
   * 可叫用本身的反函式(options.inverse())

* 建議從協助程式傳回的HTML字串內容為SafeString。

### Handlebars.js檔案中的簡單協助程式範例： {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>`{{#posts}}`<li>{{{link_to "Post"}}}</li>`{{/posts}}`</ul>'

var template = Handlebars.compile(source);

template(context);
```

會呈現：

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>發佈！&lt;/a>&lt;/li>
&lt;/ul>

### Handlebars.js檔案中的區塊協助程式範例： {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>`{{#people}}`<li>`{{#link}}``{{name}}``{{/link}}`</li>`{{/people}}`</ul>";

var template = Handlebars.compile(source);

template(data);
```

會呈現：
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>耶胡達&lt;/a>&lt;/li>
&lt;/ul>

## 自訂SCF協助程式 {#custom-scf-helpers}

必須在伺服器端和使用者端實作自訂協助程式，尤其是在傳遞資料時。 對於SCF，大多數範本會在伺服器端編譯並轉譯，因為伺服器會在要求頁面時產生指定元件的HTML。

### 伺服器端自訂協助程式 {#server-side-custom-helpers}

若要在伺服器端實作並註冊自訂SCF Helper，只需實作Java™介面即可 [TemplateHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)，使其成為 [OSGi服務](../../help/sites-developing/the-basics.md#osgi) 並將其安裝為OSGi套件組合的一部分。

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
>也必須為使用者端建立為伺服器端建立的協助程式。
>
>元件會在登入使用者的使用者端重新呈現，如果找不到使用者端協助程式，元件會消失。

### 使用者端自訂協助程式 {#client-side-custom-helpers}

使用者端協助程式是透過叫用註冊的Handlebars指令碼 `Handlebars.registerHelper()`.
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

自訂使用者端協助程式必須新增至自訂使用者端資料庫。
clientlib必須：

* 包含相依於 `cq.social.scf`.
* 載入Handlebars之後載入。
* 是 [已包含](clientlibs.md).

注意：SCF協助程式定義於 `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐功能要點](essentials.md)** | **[伺服器端自訂⇒](server-customize.md)** |
|---|---|
|   | **[使用者端自訂⇒](client-customize.md)** |
