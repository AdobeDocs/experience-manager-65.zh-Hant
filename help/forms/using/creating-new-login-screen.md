---
title: 建立新登錄螢幕
seo-title: Creating a new login screen
description: 如何修改LiveCycle模組的登錄頁，例如AEM Forms工作區或Forms管理器。
seo-description: How-to modify the login page of LiveCycle modules, for example of AEM Forms workspace or Forms Manager.
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 7%

---

# 建立新登錄螢幕{#creating-a-new-login-screen}

您可以修改使用AEM Forms登錄螢幕的所有AEM Forms模組的登錄螢幕。 例如，修改會影響Forms管理器和AEM Forms工作區的登錄螢幕。

## 必備條件 {#prerequisite}

1. 登錄時間： `/lc/crx/de` 具有管理員權限。
1. 執行以下操作：

   1. 複製分層結構：共 `/libs/livecycle/core/content` 在 `/apps/livecycle/core/content`。

      維護相同的（節點/資料夾）屬性和訪問控制。

   1. 複製內容資料夾：

      從: `/libs/livecycle/core`

      至: `/apps/livecycle/core`.

   1. 刪除 `/apps/livecycle/core` 的子菜單。

1. 執行以下操作：

   1. 複製分層結構：共 `/libs/livecycle/core/components/login` 在 `/apps/livecycle/core/components/login`。 維護相同的（節點/資料夾）屬性和訪問控制。

   1. 複製元件資料夾：從 `/libs/livecycle/core` 至 `/apps/livecycle/core`。

   1. 刪除資料夾的內容： `/apps/livecycle/core/components/login`。

### 添加新區域設定 {#adding-a-new-locale}

1. 複製 `i18n` 資料夾：

   * 從 `/libs/livecycle/core/components/login`
   * 至 `/apps/livecycle/core/components/login`

1. 刪除內部的所有資料夾 `i18n` 除了一個 `en`。

1. 在資料夾上 `en`，執行以下操作：

   1. 將資料夾更名為要支援的區域設定名稱。 比如說， `ar`。

   1. 更改屬性 `jcr:language` 值 `ar`(對於 `ar` 資料夾)。
   >[!NOTE]
   >
   >如果區域設定是語言 — 國家/地區代碼組合， `ar-DZ`，然後將資料夾名稱和屬性值更改為 `ar-DZ`。

1. 複製 `login.jsp`:

   * 從 `/libs/livecycle/core/components/login`
   * 至 `/apps/livecycle/core/components/login`

1. 修改以下代碼段 `/apps/livecycle/core/components/login/login.jsp`:

***區域設定是語言代碼***

```jsp
String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

至

```jsp
String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("ar")) {
            browserLocale = "ar";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

```jsp
String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

至

```jsp
String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
            browserLocale = "ar-DZ";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

***更改預設區域設定***

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### 添加新文本或修改現有文本 {#adding-new-text-or-modifying-existing-text}

1. 複製 `i18n` 資料夾：

   * 從 `/libs/livecycle/core/components/login`
   * 至 `/apps/livecycle/core/components/login`

1. 現在修改屬性的值 `sling:message` 要更改其文本的節點（位於所需的區域設定代碼資料夾下）。 翻譯通過 `sling:key` 節點的屬性。

1. 要添加新的鍵值對，請執行以下操作。 在螢幕快照中檢查下面的示例。

   1. 建立類型的節點 `sling:MessageEntry`，或複製現有節點，然後在所有區域設定資料夾下對其進行更名。
   1. 複製 `login.jsp` :

      * 從 `/libs/livecycle/core/components/login`

      * 至 `/apps/livecycle/core/components/login`
   1. 修改 `/apps/livecycle/core/components/login/login.jsp` 合併新添加的文本。

   ![添加新鍵值對](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   至

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### 添加新樣式或修改現有樣式 {#adding-new-style-or-modifying-existing-style}

1. 複製 `login` 節點：

   * 從 `/libs/livecycle/core/content`
   * 至 `/apps/livecycle/core/content`

1. 刪除檔案 `login.js` 和 `jquery-1.8.0.min.js`，從節點 `/apps/livecycle/core/content/login.`
1. 修改CSS檔案中的樣式。
1. 要添加新樣式：

   1. 將新樣式添加到 `/apps/livecycle/core/content/login/login.css`
   1. 複製 `login.jsp`

      * 從 `/libs/livecycle/core/components/login`

      * 至 `/apps/livecycle/core/components/login`
   1. 修改 `/apps/livecycle/core/components/login/login.jsp` 來修改標籤元素的屬性。



例如：

* 將以下內容添加到 `/apps/livecycle/core/content/login/login.css`。

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* 修改以下內容 `/apps/livecycle/core/components/login.jsp`。


   ```jsp
   <div class="loginContentArea">
   ```

   至

   ```jsp
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>如果中的現有映像 `/apps/livecycle/core/content/login` （複製自） `/libs/livecycle/core/content/login`)，然後刪除CSS中的相應引用。

### 添加新映像 {#add-new-images}

1. 按照添加新樣式或修改現有樣式的步驟（上面有說明）。
1. 在中添加新映像 `/apps/livecycle/core/content/login`。 要添加影像：

   1. 安裝WebDAV客戶端。
   1. 導航到 `/apps/livecycle/core/content/login` 資料夾，使用webDAV客戶端。 有關詳細資訊，請參閱： [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant)。

   1. 添加新映像。

1. 在中添加新樣式 `/apps/livecycle/core/content/login/login.css,` 對應添加到 `/apps/livecycle/core/content/login`。
1. 在中使用新樣式 `login.jsp` 在 `/apps/livecycle/core/components`。

例如：


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    *在/apps/livecycle/core/components/login.jsp中修改以下內容。

```jsp
<div class="loginContainerBkg">
```

至

```jsp
<div class="newLginContainerBkg">
```
