---
title: 建立新的登入畫面
seo-title: 建立新的登入畫面
description: 如何修改LiveCycle模組的登入頁面，例如AEM Forms工作區或Forms Manager。
seo-description: 如何修改LiveCycle模組的登入頁面，例如AEM Forms工作區或Forms Manager。
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
translation-type: tm+mt
source-git-commit: 9fcfd1c2c63d9a32f2d68f5b0c974bc5b5d22b40
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 4%

---


# 建立新登錄螢幕{#creating-a-new-login-screen}

您可以修改使用AEM Forms登入畫面的所有AEM Forms模組的登入畫面。 例如，這些修改會影響Forms Manager和AEM Forms工作區的登入畫面。

## 先決條件{#prerequisite}

1. 以管理員權限登入`/lc/crx/de`。
1. 執行下列動作：

   1. 複製分層結構：`/libs/livecycle/core/content`，位於`/apps/livecycle/core/content`。

      維護相同的（節點／資料夾）屬性和訪問控制。

   1. 複製內容資料夾：

      從: `/libs/livecycle/core`

      至: `/apps/livecycle/core`.

   1. 刪除`/apps/livecycle/core`資料夾的內容。

1. 執行下列動作：

   1. 複製分層結構：`/libs/livecycle/core/components/login`，位於`/apps/livecycle/core/components/login`。 維護相同的（節點／資料夾）屬性和訪問控制。

   1. 複製元件資料夾：從`/libs/livecycle/core`到`/apps/livecycle/core`。

   1. 刪除資料夾的內容：`/apps/livecycle/core/components/login`。

### 添加新區域設定{#adding-a-new-locale}

1. 複製`i18n`資料夾：

   * 從 `/libs/livecycle/core/components/login`
   * 至 `/apps/livecycle/core/components/login`

1. 刪除`i18n`內除一個資料夾外的所有資料夾，例如`en`。

1. 在資料夾`en`上，執行以下操作：

   1. 將資料夾更名為要支援的區域設定名稱。 例如，`ar`。

   1. 將屬性`jcr:language`值更改為`ar`（用於`ar`資料夾）。
   >[!NOTE]
   >
   >如果locale是語言——國家代碼組合，例如`ar-DZ`，則將資料夾名稱和屬性值更改為`ar-DZ`。

1. 複製 `login.jsp`:

   * 從 `/libs/livecycle/core/components/login`
   * 至 `/apps/livecycle/core/components/login`

1. 修改`/apps/livecycle/core/components/login/login.jsp`的下列程式碼片段：

***地區是語言代碼***

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

***若要變更預設地區設定***

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### 添加新文本或修改現有文本{#adding-new-text-or-modifying-existing-text}

1. 複製`i18n`資料夾：

   * 從 `/libs/livecycle/core/components/login`
   * 至 `/apps/livecycle/core/components/login`

1. 現在，修改要更改其文本的節點屬性`sling:message`的值（位於所需的區域設定代碼資料夾下）。 轉換是通過節點`sling:key`屬性值中提及的鍵完成的。

1. 要添加新的鍵值對，請執行以下操作。 請查看後續螢幕擷取中的範例。

   1. 建立類型`sling:MessageEntry`的節點，或複製現有節點，然後在所有區域設定資料夾下對其進行更名。
   1. 複製 `login.jsp` :

      * 從 `/libs/livecycle/core/components/login`

      * 至 `/apps/livecycle/core/components/login`
   1. 修改`/apps/livecycle/core/components/login/login.jsp`以合併新添加的文本。

   ![新增鍵值配對](assets/capture_new.png)

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

### 添加新樣式或修改現有樣式{#adding-new-style-or-modifying-existing-style}

1. 複製`login`節點：

   * 從 `/libs/livecycle/core/content`
   * 至 `/apps/livecycle/core/content`

1. 從節點`/apps/livecycle/core/content/login.`刪除檔案`login.js`和`jquery-1.8.0.min.js`
1. 修改CSS檔案中的樣式。
1. 若要新增樣式：

   1. 新增樣式至`/apps/livecycle/core/content/login/login.css`
   1. 複製 `login.jsp`

      * 從 `/libs/livecycle/core/components/login`

      * 至 `/apps/livecycle/core/components/login`
   1. 修改`/apps/livecycle/core/components/login/login.jsp`以合併新添加的樣式。



例如：

* 將下列內容新增至`/apps/livecycle/core/content/login/login.css`。

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* 在`/apps/livecycle/core/components/login.jsp`中修改以下內容。


   ```jsp
   <div class="loginContentArea">
   ```

   至

   ```jsp
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>如果`/apps/livecycle/core/content/login`（從`/libs/livecycle/core/content/login`複製）中的現有影像已移除，則移除CSS中的對應參照。

### 新增影像{#add-new-images}

1. 請遵循「新增樣式」或修改現有樣式（如上所述）的步驟。
1. 在`/apps/livecycle/core/content/login`中新增影像。 若要新增影像：

   1. 安裝WebDAV用戶端。
   1. 使用webDAV客戶端導航到`/apps/livecycle/core/content/login`資料夾。 如需詳細資訊，請參閱：[https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

   1. 新增影像。

1. 在`/apps/livecycle/core/content/login/login.css,`中新增與`/apps/livecycle/core/content/login`中新增影像對應的樣式。
1. 使用`login.jsp`中`/apps/livecycle/core/components`的新樣式。

例如：


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    *在/apps/livecycle/core/components/login.jsp中修改下列內容。

```jsp
<div class="loginContainerBkg">
```

至

```jsp
<div class="newLginContainerBkg">
```
