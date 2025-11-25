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
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 3%

---

# 建立登入畫面{#creating-a-new-login-screen}

您可以修改所有使用AEM Forms登入畫面的AEM Forms模組的登入畫面。 例如，修改會同時影響Forms Manager和AEM Forms工作區的登入畫面。

## 必備條件 {#prerequisite}

1. 以系統管理員許可權在`/lc/crx/de`登入。
1. 執行下列動作：

   1. 在`/libs/livecycle/core/content`復寫`/apps/livecycle/core/content`的階層結構。

      維護相同的（節點/資料夾）屬性和存取控制。

   1. 複製內容資料夾：

      從： `/libs/livecycle/core`

      至： `/apps/livecycle/core`。

   1. 刪除`/apps/livecycle/core`資料夾的內容。

1. 執行下列動作：

   1. 在`/libs/livecycle/core/components/login`復寫`/apps/livecycle/core/components/login`的階層結構。 維護相同的（節點/資料夾）屬性和存取控制。

   1. 將元件資料夾：從`/libs/livecycle/core`複製到`/apps/livecycle/core`。

   1. 刪除資料夾的內容： `/apps/livecycle/core/components/login`。

### 新增地區設定 {#adding-a-new-locale}

1. 複製`i18n`資料夾：

   * 從 `/libs/livecycle/core/components/login`
   * 至`/apps/livecycle/core/components/login`

1. 刪除`i18n`中的所有資料夾，但其中一個除外，例如`en`。

1. 在資料夾`en`上，執行下列動作：

   1. 將資料夾重新命名為您要支援的區域設定名稱。 例如，`ar`。

   1. 將屬性`jcr:language`值變更為`ar` （針對`ar`資料夾）。

   >[!NOTE]
   >
   >如果地區設定是語言 — 國家/地區代碼組合，例如`ar-DZ`，則將資料夾名稱和屬性值變更為`ar-DZ`。

1. 複製`login.jsp`：

   * 從 `/libs/livecycle/core/components/login`
   * 至`/apps/livecycle/core/components/login`

1. 修改`/apps/livecycle/core/components/login/login.jsp`的下列程式碼片段：

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

   收件者

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

   收件者

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

### 新增文字或修改現有文字 {#adding-new-text-or-modifying-existing-text}

1. 複製`i18n`資料夾：

   * 從 `/libs/livecycle/core/components/login`
   * 至`/apps/livecycle/core/components/login`

1. 現在修改您想要變更文字之節點（在所需的地區設定代碼資料夾下）的屬性`sling:message`的值。 透過在節點的`sling:key`屬性值中提及的索引鍵完成轉譯。

1. 若要新增索引鍵/值組，請執行下列動作。 請檢視下列熒幕擷圖中的範例。

   1. 建立型別`sling:MessageEntry`的節點，或複製現有的節點，並在所有地區設定資料夾下重新命名它。
   1. 複製`login.jsp` ：

      * 從 `/libs/livecycle/core/components/login`

      * 至`/apps/livecycle/core/components/login`

   1. 修改`/apps/livecycle/core/components/login/login.jsp`以合併新加入的文字。

   ![新增索引鍵/值組](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   收件者

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### 新增樣式或修改現有樣式 {#adding-new-style-or-modifying-existing-style}

1. 複製`login`節點：

   * 從 `/libs/livecycle/core/content`
   * 至`/apps/livecycle/core/content`

1. 從節點`login.js`刪除檔案`jquery-1.8.0.min.js`和`/apps/livecycle/core/content/login.`
1. 修改CSS檔案中的樣式。
1. 若要新增樣式：

   1. 新增樣式至`/apps/livecycle/core/content/login/login.css`
   1. 複製`login.jsp`

      * 從 `/libs/livecycle/core/components/login`

      * 至`/apps/livecycle/core/components/login`

   1. 修改`/apps/livecycle/core/components/login/login.jsp`以合併新加入的樣式。


例如：

* 新增下列至`/apps/livecycle/core/content/login/login.css`。

  ```
  css.newLoginContentArea {
      width: 700px;
      padding: 100px 0px 0px 100px;
  }
  ```

* 在`/apps/livecycle/core/components/login.jsp`中修改下列專案。


  ```jsp
  <div class="loginContentArea">
  ```

  收件者

  ```jsp
  <div class="newLoginContentArea">
  ```

>[!NOTE]
>
>如果`/apps/livecycle/core/content/login`中的現有影像（複製自`/libs/livecycle/core/content/login`）已移除，則移除CSS中對應的參考。

### 新增影像 {#add-new-images}

1. 請依照新增樣式或修改現有樣式的步驟（如上所述）操作。
1. 在`/apps/livecycle/core/content/login`中新增影像。 若要新增影像：

   1. 安裝WebDAV使用者端。
   1. 使用webDAV使用者端導覽至`/apps/livecycle/core/content/login`資料夾。 如需詳細資訊，請參閱[WebDAV存取](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=zh-Hant)。

   1. 新增影像。

1. 在`/apps/livecycle/core/content/login/login.css,`中新增與在`/apps/livecycle/core/content/login`中新增的新影像對應的樣式。
1. 在`login.jsp`的`/apps/livecycle/core/components`使用新樣式。

   例如：


   ```css
   .newLoginContainerBkg {
   
    background-image: url(my_Bg.gif);
    background-repeat: no-repeat;
    background-position: left top;
    width: 727px;
   }
   ```


   * 在/apps/livecycle/core/components/login.jsp中修改下列內容。

   ```jsp
   <div class="loginContainerBkg">
   ```

   收件者

   ```jsp
   <div class="newLginContainerBkg">
   ```
