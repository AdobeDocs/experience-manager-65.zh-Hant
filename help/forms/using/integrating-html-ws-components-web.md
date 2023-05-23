---
title: 在Web應用程式中整合AEM Forms工作區元件
seo-title: Integrating AEM Forms workspace components in web applications
description: 如何在您自己的Web應用中重新使用AEM Forms工作區元件，以利用功能並提供緊密整合。
seo-description: How to reuse AEM Forms workspace components in your own webapps to leverage functionality and provide tight integration.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 在Web應用程式中整合AEM Forms工作區元件 {#integrating-aem-forms-workspace-components-in-web-applications}

可以使用AEM Forms工作區 [元件](/help/forms/using/description-reusable-components.md) 在您自己的Web應用程式中。 以下示例實現使用CRX™實例上安裝的AEM Forms工作區開發包中的元件來建立Web應用程式。 根據您的特定需要定制以下解決方案。 示例實現重用 `UserInfo`。 `FilterList`, `TaskList`Web門戶中的元件。

1. 登錄到CRXDE Lite環境，位於 `https://'[server]:[port]'/lc/crx/de/`。 確保已安裝AEM FormsWorkPace Dev軟體包。
1. 建立路徑 `/apps/sampleApplication/wscomponents`。
1. 複製css、images、js/libs、js/runtime和js/registry.js

   * 從 `/libs/ws`
   * 至 `/apps/sampleApplication/wscomponents`.

1. 在/apps/sampleApplication/wscomponents/js資料夾內建立demomain.js檔案。 將代碼從/libs/ws/js/main.js複製到demomain.js。
1. 在demomain.js中，刪除要初始化Router的代碼，並添加以下代碼：

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

1. 按名稱在/content下建立節點 `sampleApplication` 和類型 `nt:unstructured`。 在此節點的屬性中添加 `sling:resourceType` 字串和值類型 `sampleApplication`。 在此節點的「訪問控制清單」中，為 `PERM_WORKSPACE_USER` 允許jcr:read權限。 另外，在 `/apps/sampleApplication` 添加條目 `PERM_WORKSPACE_USER` 允許jcr:read權限。
1. 在 `/apps/sampleApplication/wscomponents/js/registry.js` 更新路徑 `/lc/libs/ws/` 至 `/lc/apps/sampleApplication/wscomponents/` 的下界。
1. 在門戶首頁的JSP檔案中，位於 `/apps/sampleApplication/GET.jsp`，添加以下代碼以包括入口中所需的元件。

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   還包括AEM Forms工作區元件所需的CSS檔案。

   >[!NOTE]
   >
   >在呈現時，每個元件被添加到元件標籤（具有類元件）。 確保首頁包含這些標籤。 查看 `html.jsp` AEM Forms工作區的檔案，以瞭解有關這些基本控制項標籤的詳細資訊。

1. 要定制元件，可以按如下方式擴展所需元件的現有視圖：

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

1. 修改門戶CSS以配置門戶上所需元件的佈局、定位和樣式。 例如，您希望將背景顏色保留為黑色，以便此門戶能夠正確查看userInfo元件。 可以通過更改中的背景顏色來執行此操作 `/apps/sampleApplication/wscomponents/css/style.css` 如下：

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
