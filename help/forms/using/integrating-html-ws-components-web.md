---
title: 將AEM Forms工作區元件整合在Web應用程式中
seo-title: 將AEM Forms工作區元件整合在Web應用程式中
description: 如何在您自己的網頁應用程式中重複使用AEM Forms工作區元件，以運用功能並提供緊密的整合。
seo-description: 如何在您自己的網頁應用程式中重複使用AEM Forms工作區元件，以運用功能並提供緊密的整合。
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 將AEM Forms工作區元件整合在Web應用程式中 {#integrating-aem-forms-workspace-components-in-web-applications}

您可以在自己的Web應用程式 [中使用](/help/forms/using/description-reusable-components.md) AEM Forms工作區元件。 下列範例實作使用CRX™例項上安裝的AEM Forms工作區開發套件中的元件來建立Web應用程式。 自訂下列解決方案，以符合您的特定需求。 範例實作會重 `UserInfo`新使用 `FilterList`Web Portal `TaskList`內的元件。

1. 在登錄CRXDE Lite環境 `https://[server]:[port]/lc/crx/de/`。 請確定您已安裝AEM Forms Workpace dev套件。
1. 建立路徑 `/apps/sampleApplication/wscomponents`。
1. 複製css、影像、js/libs、js/runtime和js/registry.js

   * 從 `/libs/ws`
   * 至 `/apps/sampleApplication/wscomponents`.

1. 在/apps/sampleApplication/wscomponents/js資料夾內建立demomain.js檔案。 將程式碼從/libs/ws/js/main.js複製至demomain.js。
1. 在demomain.js中，刪除要初始化路由器的代碼並添加以下代碼：

   ```
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. 在/content下按名稱建立節 `sampleApplication` 點並鍵入 `nt:unstructured`。 在此節點的屬性中，添加類 `sling:resourceType` 型為String和值 `sampleApplication`。 在此節點的「訪問控制清單」中添加允許jcr:read權 `PERM_WORKSPACE_USER` 限的條目。 此外，在「存取控制清單」中 `/apps/sampleApplication` 新增允許jcr:read權 `PERM_WORKSPACE_USER` 限的項目。
1. 在范 `/apps/sampleApplication/wscomponents/js/registry.js` 本值的更 `/lc/libs/ws/` 新 `/lc/apps/sampleApplication/wscomponents/` 路徑中。
1. 在您的入口網站首頁JSP檔案( `/apps/sampleApplication/GET.jsp`)中，新增下列程式碼，以在入口網站內包含必要的元件。

   ```as3
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   也包含AEM Forms工作區元件所需的CSS檔案。

   >[!NOTE]
   >
   >在演算時，每個元件都會新增至元件標籤（具有類別元件）。 請確定您的首頁包含這些標籤。 請參閱AEM `html.jsp` Forms工作區的檔案，進一步瞭解這些基本控制標籤。

1. 要定制元件，可以按如下方式擴展所需元件的現有視圖：

   ```as3
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

1. 修改入口網站CSS，以設定您入口網站上所需元件的版面、位置和樣式。 例如，您想要將此入口網站的背景顏色維持為黑色，以便檢視userInfo元件。 您可以依下列方式變更背景顏色來 `/apps/sampleApplication/wscomponents/css/style.css` 執行此動作：

   ```as3
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
