---
title: 國際化UI字串
description: Java&trade和JavaScript API可讓您將字串國際化
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# 國際化UI字串 {#internationalizing-ui-strings}

Java™和JavaScript API可讓您國際化下列資源型別中的字串：

* Java™來源檔案。
* JSP指令碼。
* 使用者端資料庫或頁面來源中的JavaScript。
* 對話方塊和元件組態屬性中使用的JCR節點屬性值。

如需國際化和本地化程式的概述，請參閱 [國際化元件](/help/sites-developing/i18n.md).

## 在Java™和JSP程式碼中國際化字串 {#internationalizing-strings-in-java-and-jsp-code}

此 `com.day.cq.i18n` Java™套件可讓您在UI中顯示當地語系化的字串。 此 `I18n` 類別提供 `get` 從Adobe Experience Manager (AEM)字典擷取當地語系化字串的方法。 唯一需要的 `get` 方法是指英文中的字串常值。 英文是UI的預設語言。 下列範例會將單字本地化 `Search`：

`i18n.get("Search");`

識別英文字串與典型的國際化架構不同，後者的ID會識別字串，並在執行階段用來參考字串。 使用英文字串可提供下列優點：

* 程式碼容易理解。
* 預設語言中的字串一律可用。

### 決定使用者的語言 {#determining-the-user-s-language}

判斷使用者偏好語言的方式有兩種：

* 對於已驗證身分的使用者，從使用者帳戶中的偏好設定中決定語言。
* 要求頁面的地區設定。

使用者帳戶的語言屬性是慣用方法，因為較可靠。 但是，使用者必須登入才能使用此方法。

#### 建立I18n Java™物件 {#creating-the-i-n-java-object}

I18n類別提供兩個建構函式。 如何判斷使用者的偏好語言會決定要使用的建構函式。

若要以使用者帳戶中指定的語言呈現字串，請使用下列建構函式（匯入後） `com.day.cq.i18n.I18n)`：

```java
I18n i18n = new I18n(slingRequest);
```

建構函式使用 `SlingHTTPRequest` 以擷取使用者的語言設定。

若要使用頁面地區設定來決定語言，請先取得所要求頁面語言的ResourceBundle：

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### 將字串國際化 {#internationalizing-a-string}

使用 `get` 方法 `I18n` 物件將字串國際化。 唯一需要的 `get` 方法是要國際化的字串。 字串對應至翻譯工具字典中的字串。 get方法會在字典中查詢字串，並傳回目前語言的翻譯。

的第一個引數 `get` 方法必須符合下列規則：

* 值必須是字串常值。 型別變數 `String` 不被接受。
* 字串常值必須用單行表示。
* 字串區分大小寫。

```xml
i18n.get("Enter a search keyword");
```

#### 使用翻譯提示 {#using-translation-hints}

指定 [翻譯提示](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) 國際化字串的字元，以區分字典中的重複字串。 使用的第二個選用引數 `get` 提供翻譯提示的方法。 翻譯提示必須完全符合字典中專案的Comment屬性。

例如，字典包含字串 `Request` 兩次：一次作為動詞，另一次作為名詞。 下列程式碼包含轉譯提示作為中的引數 `get` 方法：

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### 納入當地語系化句子中的變數 {#including-variables-in-localized-sentences}

將變數納入當地語系化字串中，將內容相關含意建置到句子中。 例如，登入Web應用程式後，首頁會顯示訊息「歡迎回到系統管理員」。 您的收件匣中有兩封郵件。」 頁面內容會決定使用者名稱和訊息數。

[在字典中](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)中，變數會以字串形式呈現為括弧內的索引。 將變數的值指定為 `get` 方法。 引數會放置在轉譯提示之後，而索引會與引數的順序相對應：

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

國際化字串和翻譯提示必須與字典中的字串和註解完全相符。 您可以省略本地化提示，提供 `null` 值做為第二個引數。

#### 使用靜態Get方法 {#using-the-static-get-method}

此 `I18N` 類別會定義靜態 `get` 方法，適合在必須將數個字串當地語系化時使用。 除了物件的引數 `get` 方法，靜態方法需要 `SlingHttpRequest` 物件或 `ResourceBundle` 根據您判斷使用者偏好語言的方式，您正在使用的語言：

* 使用使用者的語言偏好設定：提供SlingHttpRequest做為第一個引數。

  `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* 使用頁面語言：提供ResourceBundle做為第一個引數。

  `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### 在JavaScript程式碼中國際化字串 {#internationalizing-strings-in-javascript-code}

JavaScript API可讓您在使用者端上將字串當地語系化。 如同 [Java™和JSP](#internationalizing-strings-in-java-and-jsp-code) 程式碼、JavaScript API可讓您識別要本地化的字串、提供本地化提示，以及在本地化的字串中加入變數。

此 `granite.utils` [使用者端資料庫資料夾](/help/sites-developing/clientlibs.md) 提供JavaScript API。 若要使用API，請在您的頁面上包含此使用者端程式庫資料夾。 本地化函式使用 `Granite.I18n` 名稱空間。

顯示當地語系化字串之前，請先使用 `Granite.I18n.setLocale` 函式。 函式需要地區設定的語言代碼作為引數：

```
Granite.I18n.setLocale("fr");
```

若要呈現當地語系化的字串，請使用 `Granite.I18n.get` 函式：

```
Granite.I18n.get("string to localize");
```

下列範例會將「歡迎回來」字串國際化：

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

函式引數與Java™ I18n.get方法不同：

* 第一個引數是要本地化的字串常值。
* 第二個引數是要插入字串常值中的值陣列。
* 第三個引數是本地化提示。

以下範例使用JavaScript將「歡迎回來管理員」當地語系化。 您的收件匣中有兩封郵件。」 句子：

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### 從JCR節點國際化字串 {#internationalizing-strings-from-jcr-nodes}

UI字串通常以JCR節點屬性為基礎。 例如， `jcr:title` 頁面的屬性通常用作 `h1` 個元素進行識別。 此 `I18n` 類別提供 `getVar` 將這些字串當地語系化的方法。

以下範例JSP指令碼會擷取 `jcr:title` 屬性，並在頁面上顯示本地化的字串：

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### 指定JCR節點的轉譯提示 {#specifying-translation-hints-for-jcr-nodes}

類似於 [Java™ API中的翻譯提示](#using-translation-hints)，您可以提供翻譯提示來區分字典中的重複字串。 提供翻譯提示，作為包含國際化屬性的節點的屬性。 hint屬性的名稱是由國際化屬性的名稱所組成，其中 `_commentI18n` 字尾：

`${prop}_commentI18n`

例如， `cq:page` 節點包含正在本地化的jcr：title屬性。 提示會提供為名為jcr：title_commentI18n的屬性的值。

### 測試國際化涵蓋範圍 {#testing-internationalization-coverage}

測試您是否將UI中的所有字串國際化。 若要檢視涵蓋哪些字串，請將使用者語言設為zz_ZZ，然後在網頁瀏覽器中開啟UI。 國際化字串會以下列格式顯示並帶有存根轉譯：

`USR_*Default-String*_尠`

下圖顯示AEM首頁的存根轉譯：

![chlimage_1](assets/chlimage_1a.jpeg)

若要設定使用者的語言，請為使用者帳戶設定偏好設定節點的語言屬性。

使用者的偏好設定節點的路徑如下：

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)
