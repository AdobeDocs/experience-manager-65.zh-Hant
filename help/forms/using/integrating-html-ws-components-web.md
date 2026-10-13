---
title: 在網頁應用程式中整合AEM Forms工作區元件
description: 如何在您自己的網頁應用程式中重複使用AEM Forms工作區元件，以使用功能並提供緊密整合。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%
---
# 在網頁應用程式中整合AEM Forms工作區元件 {#integrating-aem-forms-workspace-components-in-web-applications}

您可以在自己的網頁應用程式中使用AEM Forms工作區[元件](/help/forms/using/description-reusable-components.md)。 以下實作範例使用安裝在™執行個體上的AEM Forms工作區開發套件中的元件來建立網站應用程式。 自訂以下解決方案以符合您的特定需求。 範例實作在入口網站內重複使用`UserInfo`、`FilterList`和`TaskList`元件。

1. 在`https://'[server]:[port]'/lc/crx/de/`登入CRXDE Lite環境。 確保您已安裝AEM Forms workspace dev套件。
1. 建立路徑`/apps/sampleApplication/wscomponents`。
1. 複製css、影像、js/libs、js/runtime和js/registry.js

   * 從 `/libs/ws`
   * 至`/apps/sampleApplication/wscomponents`。

1. 在/apps/sampleApplication/wscomponents/js資料夾中建立demomain.js檔案。 將程式碼從/libs/ws/js/main.js複製到demomain.js中。
1. 在demomain.js中，移除程式碼以初始化路由器，並新增下列程式碼：

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

1. 在/content下建立名稱為`sampleApplication`且型別為`nt:unstructured`的節點。 在此節點的屬性中，加入字串型別及值`sampleApplication`的`sling:resourceType`。 在此節點的存取控制清單中，新增允許jcr:read許可權的`PERM_WORKSPACE_USER`專案。 此外，在`/apps/sampleApplication`的存取控制清單中，新增允許jcr:read許可權的`PERM_WORKSPACE_USER`專案。
1. 在`/apps/sampleApplication/wscomponents/js/registry.js`中，將範本值的路徑從`/lc/libs/ws/`更新為`/lc/apps/sampleApplication/wscomponents/`。
1. 在位於`/apps/sampleApplication/GET.jsp`的入口網站首頁JSP檔案中，新增下列程式碼以在入口網站中包含必要元件。

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   也包含AEM Forms工作區元件所需的CSS檔案。

   >[!NOTE]
   >
   >呈現時，每個元件都會新增至元件標籤（具有類別元件）。 確定您的首頁包含這些標籤。 請參閱AEM Forms工作區的`html.jsp`檔案，深入瞭解這些基本控制項標籤。

1. 若要自訂元件，您可以依照以下方式擴充所需元件的現有檢視：

   ```javascript
   define([
       'jquery',
       'underscore',
       'backbone',
       'runtime/views/userinfo'],
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

1. 修改入口網站CSS以設定入口網站上所需元件的版面、定位和樣式。 例如，您想要讓此入口網站的背景顏色保持為黑色，以便順利檢視userInfo元件。 您可以透過變更`/apps/sampleApplication/wscomponents/css/style.css`中的背景顏色來完成此操作，如下所示：

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
