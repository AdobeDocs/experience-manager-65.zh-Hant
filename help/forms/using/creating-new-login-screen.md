---
title: 建立登入畫面
description: 如何修改LiveCycle模組的登入頁面，例如AEM Forms工作區或Forms Manager。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 3%

---

# 建立登入畫面{#creating-a-new-login-screen}

您可以修改所有使用AEM Forms登入畫面的AEM Forms模組的登入畫面。 例如，修改會同時影響Forms Manager和AEM Forms工作區的登入畫面。

## 必備條件 {#prerequisite}

1. 登入： `/lc/crx/de` 具有管理員許可權。
1. 執行下列動作：

   1. 複製下列的階層結構： `/libs/livecycle/core/content` 在 `/apps/livecycle/core/content`.

      維護相同的（節點/資料夾）屬性和存取控制。

   1. 複製內容資料夾：

      從： `/libs/livecycle/core`

      至： `/apps/livecycle/core`.

   1. 刪除內容 `/apps/livecycle/core` 資料夾。

1. 執行下列動作：

   1. 複製下列的階層結構： `/libs/livecycle/core/components/login` 在 `/apps/livecycle/core/components/login`. 維護相同的（節點/資料夾）屬性和存取控制。

   1. 複製元件資料夾：從 `/libs/livecycle/core` 至 `/apps/livecycle/core`.

   1. 刪除資料夾的內容： `/apps/livecycle/core/components/login`.

### 新增地區設定 {#adding-a-new-locale}

1. 複製 `i18n` 資料夾：

   * 從 `/libs/livecycle/core/components/login`
   * 至 `/apps/livecycle/core/components/login`

1. 刪除裡面的所有資料夾 `i18n` 除了一項，例如 `en`.

1. 在資料夾上 `en`，請執行下列動作：

   1. 將資料夾重新命名為您要支援的區域設定名稱。 例如，`ar`。

   1. 變更屬性 `jcr:language` 值至 `ar`(適用於 `ar` 資料夾)。

   >[!NOTE]
   >
   >如果locale是語言 — 國家/地區的代碼組合，例如， `ar-DZ`，然後將資料夾名稱和屬性值變更為 `ar-DZ`.

1. 複製 `login.jsp`：

   * 從 `/libs/livecycle/core/components/login`
   * 至 `/apps/livecycle/core/components/login`

1. 修改下列程式碼片段 `/apps/livecycle/core/components/login/login.jsp`：

***地區設定為語言代碼***

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

***變更預設地區設定***

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### 新增文字或修改現有文字 {#adding-new-text-or-modifying-existing-text}

1. 複製 `i18n` 資料夾：

   * 從 `/libs/livecycle/core/components/login`
   * 至 `/apps/livecycle/core/components/login`

1. 現在修改屬性的值 `sling:message` 節點（位於所需的地區設定代碼資料夾下）中，您想要變更其文字的。 翻譯會透過下列值中提及的索引鍵完成： `sling:key` 節點的屬性。

1. 若要新增索引鍵/值組，請執行下列動作。 請檢視下列熒幕擷圖中的範例。

   1. 建立型別節點 `sling:MessageEntry`，或複製現有節點並重新命名（在所有地區設定資料夾下）。
   1. 複製 `login.jsp` ：

      * 從 `/libs/livecycle/core/components/login`

      * 至 `/apps/livecycle/core/components/login`

   1. 修改 `/apps/livecycle/core/components/login/login.jsp` 以合併新加入的文字。

   ![新增索引鍵/值組](assets/capture_new.png)

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

### 新增樣式或修改現有樣式 {#adding-new-style-or-modifying-existing-style}

1. 複製 `login` 節點：

   * 從 `/libs/livecycle/core/content`
   * 至 `/apps/livecycle/core/content`

1. 刪除檔案 `login.js` 和 `jquery-1.8.0.min.js`，從節點 `/apps/livecycle/core/content/login.`
1. 修改CSS檔案中的樣式。
1. 若要新增樣式：

   1. 新增樣式至 `/apps/livecycle/core/content/login/login.css`
   1. 複製 `login.jsp`

      * 從 `/libs/livecycle/core/components/login`

      * 至 `/apps/livecycle/core/components/login`

   1. 修改 `/apps/livecycle/core/components/login/login.jsp` 以合併新加入的樣式。


例如：

* 將下列專案新增至 `/apps/livecycle/core/content/login/login.css`.

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* 在中修改下列專案 `/apps/livecycle/core/components/login.jsp`.


  ```jsp
  <div class="loginContentArea">
  ```

  至

  ```jsp
  <div class="newLoginContentArea">
  ```

>[!NOTE]
>
>如果影像位於 `/apps/livecycle/core/content/login` (複製自 `/libs/livecycle/core/content/login`)，然後在CSS中移除對應的參照。

### 新增影像 {#add-new-images}

1. 請依照新增樣式或修改現有樣式的步驟（如上所述）操作。
1. 在中新增影像 `/apps/livecycle/core/content/login`. 若要新增影像：

   1. 安裝WebDAV使用者端。
   1. 瀏覽至 `/apps/livecycle/core/content/login` 資料夾，使用webDAV使用者端。 如需詳細資訊，請參閱 [WebDAV存取](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en).

   1. 新增影像。

1. 在中新增樣式 `/apps/livecycle/core/content/login/login.css,` 對應至中新增的新影像 `/apps/livecycle/core/content/login`.
1. 在中使用新樣式 `login.jsp` 在 `/apps/livecycle/core/components`.

例如：


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    *在/apps/livecycle/core/components/login.jsp中修改下列專案。

```jsp
<div class="loginContainerBkg">
```

至

```jsp
<div class="newLginContainerBkg">
```
