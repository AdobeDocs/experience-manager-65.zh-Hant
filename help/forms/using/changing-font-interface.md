---
title: 變更介面上的字型
seo-title: 變更介面上的字型
description: 如何選擇性地變更使用者介面上的字型。
seo-description: 如何選擇性地變更使用者介面上的字型。
uuid: 421fdd24-441a-4092-8c52-f3ed3d5d5671
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 9fcb80b4-cbc2-48a5-afd1-4f3bc50bc503
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 變更介面上的字型{#changing-the-font-on-the-interface}

您可以變更AEM Forms工作區中顯示的字型。 用戶介面的特定部分中使用的字型在樣式表的相應部分中定義。 您可以選擇性地變更使用者介面上的字型。

依照 [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md) ，並視您的需求，依循自訂CSS、HTML或兩者的步驟。

1. 以現有樣式變更或新增字型系列。
1. 變更或新增HTML元素的字型系列內嵌。
1. 新增樣式並用於HTML元素。

例如，若要將頂端導覽列錨點文字的字型變更為Courier New，請依照下列步驟進行：

1. 存取以登入CRXDE Lite `https://[server]:[port]/lc/crx/de/index.jsp`。
1. 執行下列任一項作業：

   1. 若要以現有樣式變更font-family，請在newStyle.css檔案中新增下列項目： /apps/ws/css。

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. 要為HTML元素添加font-family行內，請將檔案復 `/libs/ws/js/runtime/templates/appnavigation.html` 制到 `/apps/ws/js/runtime/templates/appnavigation.html`。

      按如下方式更新/apps/ws/js/runtime/templates/appnavigation.html檔案：

      ```
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      開啟/apps/ws/js/registry.js檔案以進行編輯，並取代 `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` 為 `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`。

   1. 若要新增定義font-family的樣式，請在新的Style.css檔案中新增下列項目：/apps/ws/css。

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      若要新增HTML元素的font-family內嵌，請在appnavigation.html檔案中新增下列項目：/apps/ws/js/runtime/templates。

      ```css
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. 重新啟動工作區並清除瀏覽器快取，以便顯示變更。

![change_font_before](assets/change_font_before.png)

字型自訂前的頂端導覽列

![change_font_after](assets/change_font_after.png)

自訂第一個標籤的字型後的頂端導覽列

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
