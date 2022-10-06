---
title: 國際化UI字串
seo-title: Internationalizing UI Strings
description: Java和Javascript API可讓您將字串國際化
seo-description: Java and Javascript APIs enable you to internationalize strings
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---

# 國際化UI字串 {#internationalizing-ui-strings}

Java和Javascript API可讓您將下列資源類型中的字串國際化：

* Java源檔案。
* JSP指令碼。
* 用戶端程式庫或頁面來源中的Javascript。
* 對話框和元件配置屬性中使用的JCR節點屬性值。

如需國際化和本地化流程的概述，請參閱 [國際化元件](/help/sites-developing/i18n.md).

## 以Java和JSP程式碼將字串國際化 {#internationalizing-strings-in-java-and-jsp-code}

此 `com.day.cq.i18n` Java套件可讓您在UI中顯示本地化字串。 此 `I18n` 類別提供 `get` 從AEM字典中擷取本地化字串的方法。 唯一需要的參數為 `get` 方法是英文中的字串常值。 英文是UI的預設語言。 以下示例將單詞本地化 `Search`:

`i18n.get("Search");`

以英文識別字串，與ID識別字串且在執行階段用於參考字串的一般國際化架構不同。 使用英文字串常值可提供下列優點：

* 程式碼容易理解。
* 預設語言的字串一律可用。

### 決定使用者語言 {#determining-the-user-s-language}

有兩種方式可判斷使用者偏好的語言：

* 對於已驗證的使用者，請從使用者帳戶的偏好設定中決定語言。
* 請求的頁的地區。

使用者帳戶的語言屬性是偏好的方法，因為它更可靠。 不過，使用者必須登入才能使用此方法。

#### 建立I18n Java對象 {#creating-the-i-n-java-object}

I18n類提供兩個建構子。 您如何確定用戶的首選語言決定了要使用的建構子。

若要以使用者帳戶中指定的語言呈現字串，請使用下列建構函式（匯入後） `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

建構函式使用 `SlingHTTPRequest` 以擷取使用者的語言設定。

要使用頁面區域設定來確定語言，首先需要獲取所請求頁面語言的ResourceBundle :

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### 字串國際化 {#internationalizing-a-string}

使用 `get` 方法 `I18n` 對象，以國際化字串。 唯一需要的參數為 `get` 方法是要國際化的字串。 該字串與Translator字典中的字串對應。 get方法會在字典中查找字串，並傳回目前語言的翻譯。

第一個引數 `get` 方法必須符合下列規則：

* 值必須是字串常值。 類型的變數 `String` 無法接受。
* 字串常值必須在一行上表示。
* 字串區分大小寫。

```xml
i18n.get("Enter a search keyword");
```

#### 使用翻譯提示 {#using-translation-hints}

指定 [翻譯提示](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) ，以區分字典中的重複字串。 使用 `get` 提供翻譯提示的方法。 翻譯提示必須與字典中項目的Comment屬性完全相符。

例如，字典包含字串 `Request` 兩次：一次是動詞，一次是名詞。 下列程式碼包含翻譯提示，作為 `get` 方法：

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### 在本地化的句子中包含變數 {#including-variables-in-localized-sentences}

在本地化字串中加入變數，將內容含義建置至句子中。 例如，登入Web應用程式後，首頁會顯示訊息「歡迎返回管理員」。 收件箱中有2條郵件。」 頁面內容會決定使用者名稱和訊息數量。

[在字典里](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)，變數在字串中會以括弧內的索引表示。 指定變數的值作為 `get` 方法。 引數會放置在轉換提示之後，而索引會與引數的順序對應：

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

國際化字串和翻譯提示必須與字典中的字串和注釋完全匹配。 您可以提供 `null` 值做為第二個引數。

#### 使用靜態Get方法 {#using-the-static-get-method}

此 `I18N` 類定義靜態 `get` 當您需要將少量字串本地化時，此方法相當實用。 除了物件的 `get` 方法，靜態方法需要 `SlingHttpRequest` 物件或 `ResourceBundle` 使用的語言（根據您決定使用者偏好語言的方式）:

* 使用用戶的語言首選項：提供SlingHttpRequest作為第一個參數。

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* 使用頁面語言：提供ResourceBundle作為第一個參數。

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### 在Javascript程式碼中將字串國際化 {#internationalizing-strings-in-javascript-code}

Javascript API可讓您將用戶端上的字串當地化。 與 [Java和JSP](#internationalizing-strings-in-java-and-jsp-code) 程式碼中，Javascript API可讓您識別要本地化的字串、提供本地化提示，以及在本地化的字串中加入變數。

此 `granite.utils` [用戶庫資料夾](/help/sites-developing/clientlibs.md) 提供Javascript API。 若要使用API，請在頁面上包含此用戶端程式庫資料夾。 本地化函式使用 `Granite.I18n` 命名空間。

在顯示本地化字串之前，您需要使用 `Granite.I18n.setLocale` 函式。 此函式需要區域設定的語言代碼作為參數：

```
Granite.I18n.setLocale("fr");
```

若要呈現本地化字串，請使用 `Granite.I18n.get` 函式：

```
Granite.I18n.get("string to localize");
```

下列範例會國際化字串&quot;Welcome back&quot;:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

函式參數與Java I18n.get方法不同：

* 第一個參數是要本地化的字串常值。
* 第二個參數是要插入至字串常值的陣列。
* 第三個參數是本地化提示。

以下範例使用Javascript將「歡迎返回管理員」當地化。 收件箱中有2條郵件。」 句子：

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### 從JCR節點將字串國際化 {#internationalizing-strings-from-jcr-nodes}

UI字串通常以JCR節點屬性為基礎。 例如， `jcr:title` 頁面的屬性通常用作 `h1` 元素。 此 `I18n` 類別提供 `getVar` 將這些字串本地化的方法。

以下示例JSP指令碼將檢索 `jcr:title` 屬性，並在頁面上顯示本地化字串：

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### 為JCR節點指定翻譯提示 {#specifying-translation-hints-for-jcr-nodes}

類似 [Java API中的翻譯提示](#using-translation-hints)，您可以提供翻譯提示來區分字典中的重複字串。 提供翻譯提示作為包含國際化屬性的節點的屬性。 提示屬性的名稱由國際化屬性名稱的名稱和 `_commentI18n` 尾碼：

`${prop}_commentI18n`

例如， `cq:page` 節點包含正在本地化的jcr:title屬性。 提供提示作為名為jcr:title_commentI18n的屬性的值。

### 測試國際化覆蓋 {#testing-internationalization-coverage}

測試您是否已將UI中的所有字串國際化。 若要查看涵蓋哪些字串，請將使用者語言設為zz_ZZ，然後在網頁瀏覽器中開啟UI。 國際化字串將以以下格式顯示存根轉換：

`USR_*Default-String*_尠`

下圖顯示了AEM首頁的存根翻譯：

![chlimage_1](assets/chlimage_1a.jpeg)

要設定用戶的語言，請為用戶帳戶配置首選項節點的語言屬性。

用戶的首選項節點的路徑如下：

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)
