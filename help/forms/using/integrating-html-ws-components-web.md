---
title: 將AEM Forms工作區元件整合至網頁應用程式
seo-title: 將AEM Forms工作區元件整合至網頁應用程式
description: 如何在您自己的網頁應用程式中重複使用AEM Forms工作區元件，以運用功能並提供緊密整合。
seo-description: 如何在您自己的網頁應用程式中重複使用AEM Forms工作區元件，以運用功能並提供緊密整合。
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 將AEM Forms工作區元件整合至Web應用程式{#integrating-aem-forms-workspace-components-in-web-applications}

您可以在自己的Web應用程式中使用AEM Forms工作區[元件](/help/forms/using/description-reusable-components.md)。 下列範例實作使用CRX™例項上安裝之AEM Forms工作區開發套件中的元件來建立Web應用程式。 根據您的特定需求自訂下列解決方案。 範例實作會在網站入口內重新使用`UserInfo`、`FilterList`和`TaskList`元件。

1. 在`https://'[server]:[port]'/lc/crx/de/`登入CRXDE Lite環境。 確認已安裝AEM Forms Workpace開發套件。
1. 建立路徑`/apps/sampleApplication/wscomponents`。
1. 複製css、影像、js/libs、js/runtime和js/registry.js

   * 從 `/libs/ws`
   * 至 `/apps/sampleApplication/wscomponents`.

1. 在/apps/sampleApplication/wscomponents/js資料夾內建立demomain.js檔案。 將程式碼從/libs/ws/js/main.js複製至demomain.js。
1. 在demomain.js中，移除要初始化Router的程式碼，並新增下列程式碼：

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. 按名稱`sampleApplication`在/content下建立節點，並鍵入`nt:unstructured`。 在此節點的屬性中，添加類型為String的`sling:resourceType`和值`sampleApplication`。 在此節點的「訪問控制清單」中，為`PERM_WORKSPACE_USER`添加一個條目，允許jcr:read權限。 此外，在`/apps/sampleApplication`的「訪問控制清單」中，為`PERM_WORKSPACE_USER`添加允許jcr:read權限的條目。
1. 在`/apps/sampleApplication/wscomponents/js/registry.js`中，針對範本值將路徑從`/lc/libs/ws/`更新至`/lc/apps/sampleApplication/wscomponents/`。
1. 在`/apps/sampleApplication/GET.jsp`的入口首頁JSP檔案中，添加以下代碼以在入口內包括所需的元件。

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   也包含AEM Forms工作區元件所需的CSS檔案。

   >[!NOTE]
   >
   >呈現時，每個元件都會新增至元件標籤（具有類別元件）。 請確定您的首頁包含這些標籤。 請參閱AEM Forms工作區的`html.jsp`檔案，深入了解這些基本控制標籤。

1. 要自定義元件，可以按如下方式擴展所需元件的現有視圖：

   ```javascript
   define([
       ‘jquery’,
       ‘underscore’,
       ‘backbone’,
       ‘runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. 修改入口網站CSS，以設定入口網站上所需元件的版面、定位和樣式。 例如，您想要讓此入口網站的背景顏色保持黑色，以便順利檢視userInfo元件。 您可以依照以下方式變更`/apps/sampleApplication/wscomponents/css/style.css`中的背景顏色，以執行此操作：

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
