---
title: 國際化UI字串
seo-title: 國際化UI字串
description: Java和Javascript API可讓您將字串國際化
seo-description: Java和Javascript API可讓您將字串國際化
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 國際化UI字串 {#internationalizing-ui-strings}

Java和Javascript API可讓您將字串國際化為下列類型的資源：

* Java源檔案。
* JSP指令碼。
* 用戶端程式庫或頁面來源中的Javascript。
* 用於對話框和元件配置屬性的JCR節點屬性值。

有關國際化和本地化流程的概述，請參 [閱國際化元件](/help/sites-developing/i18n.md)。

## 在Java和JSP代碼中國際化字串 {#internationalizing-strings-in-java-and-jsp-code}

Java `com.day.cq.i18n` 套件可讓您在UI中顯示本地化字串。 類別 `I18n` 提供從AEM `get` 字典擷取本地化字串的方法。 方法的唯一必 `get` 要參數是英文的字串常值。 英文是UI的預設語言。 以下範例將單字定位 `Search`:

`i18n.get("Search");`

以英文識別字串不同於一般的國際化架構，其中ID可識別字串，並在執行時期用來參考字串。 使用英文字串常值可提供下列優點：

* 程式碼易懂。
* 預設語言的字串永遠可用。

### 確定用戶語言 {#determining-the-user-s-language}

有兩種方式可決定使用者偏好的語言：

* 對於已驗證的使用者，請從使用者帳戶的偏好設定中判斷語言。
* 請求頁面的地區設定。

使用者帳戶的語言屬性是偏好的方法，因為它更可靠。 但是，用戶必須登錄才能使用此方法。

#### 建立I18n java對象 {#creating-the-i-n-java-object}

I18n類提供兩個建構子。 您如何決定使用者偏好的語言，以決定要使用的建構函式。

若要以使用者帳戶中指定的語言呈現字串，請使用下列建構函式(匯入後 `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

建構函式使 `SlingHTTPRequest` 用來擷取使用者的語言設定。

若要使用頁面地區設定來判斷語言，您首先需要取得所請求頁面語言的ResourceBundle:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### 字串國際化 {#internationalizing-a-string}

使用物 `get` 件的方 `I18n` 法來國際化字串。 方法的唯一必要參 `get` 數是要國際化的字串。 該字串與Translator字典中的字串相對應。 get方法會在字典中查找字串並返回當前語言的翻譯。

方法的第一個引 `get` 數必須符合下列規則：

* 值必須是字串常值。 類型變數 `String` 不可接受。
* 字串常值必須在單行上具有表達式。
* 字串區分大小寫。

```xml
i18n.get("Enter a search keyword");
```

#### 使用翻譯提示 {#using-translation-hints}

指定國 [際化字串的轉譯提示](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) ，以區分字典中重複的字串。 使用方法的第二個可選參 `get` 數提供翻譯提示。 翻譯提示必須與字典中項目的「注釋」屬性完全匹配。

例如，字典包含兩 `Request` 次：一次是動詞，一次是名詞。 以下代碼包括翻譯提示作為方法中的引 `get` 數：

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### 在局部化句子中加入變數 {#including-variables-in-localized-sentences}

在本地化字串中加入變數，將內容相關意義建立至句子中。 例如，登入Web應用程式後，首頁會顯示訊息「歡迎返回管理員」。 收件匣中有2條訊息。」 頁面內容會決定使用者名稱和訊息數量。

[在字典中](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)，變數在字串中表示為方括弧內的索引。 指定變數的值作為方法的 `get` 參數。 引數將按照轉換提示放置，索引與引數的順序相對應：

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

國際化字串和翻譯提示必須與字典中的字串和注釋完全匹配。 通過提供值作為第二個引數，可以 `null` 忽略本地化提示。

#### 使用Static Get方法 {#using-the-static-get-method}

類定 `I18N` 義了靜態方 `get` 法，當您需要本地化少量字串時，該方法非常有用。 除了對象方法的參 `get` 數外，靜態方法還要求對象或您正在使用的 `SlingHttpRequest``ResourceBundle` 對象，具體取決於您確定用戶首選語言的方式：

* 使用使用者的語言偏好設定：提供SlingHttpRequest作為第一個參數。

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* 使用頁面語言：提供ResourceBundle作為第一個參數。

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### 在Javascript程式碼中國際化字串 {#internationalizing-strings-in-javascript-code}

Javascript API可讓您在用戶端上本地化字串。 和 [Java和JSP程式碼一樣](#internationalizing-strings-in-java-and-jsp-code) ,Javascript API可讓您識別要本地化的字串、提供本地化提示，以及在本地化的字串中加入變數。

用戶 `granite.utils` 端程 [式庫資料夾](/help/sites-developing/clientlibs.md) ，提供Javascript API。 若要使用API，請在您的頁面上加入此用戶端程式庫資料夾。 本地化函式使用命名 `Granite.I18n` 空間。

在顯示本地化字串之前，您需要使用函式設定語 `Granite.I18n.setLocale` 言環境。 函式需要語言環境的語言代碼作為參數：

```
Granite.I18n.setLocale("fr");
```

若要呈現本地化字串，請使用 `Granite.I18n.get` 函式：

```
Granite.I18n.get("string to localize");
```

下列範例將字串&quot;Welcome back&quot;國際化：

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

函式參數與Java I18n不同。get方法：

* 第一個參數是要本地化的字串常值。
* 第二個參數是要插入字串常值的陣列。
* 第三個參數是定位提示。

下列範例使用Javascript來本地化「歡迎返回管理員」。 收件匣中有2條訊息。」 句子：

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### 從JCR節點國際化字串 {#internationalizing-strings-from-jcr-nodes}

UI字串通常以JCR節點屬性為基礎。 例如，頁面 `jcr:title` 的屬性通常用作頁面代碼中元 `h1` 素的內容。 類提 `I18n` 供了定位這 `getVar` 些字串的方法。

以下示例JSP指令碼從儲存庫 `jcr:title` 中檢索屬性，並在頁面上顯示本地化字串：

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### 為JCR節點指定翻譯提示 {#specifying-translation-hints-for-jcr-nodes}

與Java API [中的翻譯提示類似](#using-translation-hints)，您可以提供翻譯提示來區分字典中的重複字串。 提供翻譯提示作為包含國際化屬性的節點的屬性。 提示屬性的名稱由具有尾碼的國際化屬性名稱 `_commentI18n` 組成：

`${prop}_commentI18n`

例如，節點 `cq:page` 包含正在本地化的jcr:title屬性。 提示是作為名為jcr:title_commentI18n的屬性值提供的。

### 測試國際化覆蓋範圍 {#testing-internationalization-coverage}

測試您的UI中的所有字串是否已國際化。 若要查看涵蓋哪些字串，請將使用者語言設為zz_ZZ，然後在網頁瀏覽器中開啟UI。 國際化字串以下列格式顯示存根轉換：

`USR_*Default-String*_尠`

下圖顯示AEM首頁的存根翻譯：

![chlimage_1](assets/chlimage_1a.jpeg)

要設定用戶的語言，請為用戶帳戶配置首選項節點的語言屬性。

用戶的首選項節點具有如下路徑：

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)

