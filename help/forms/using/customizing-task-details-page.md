---
title: 自定義任務詳細資訊頁
seo-title: 自定義任務詳細資訊頁
description: How-to customize the task details page in AEM Forms workspace to modify the default information displayed about a task.
seo-description: How-to customize the task details page in AEM Forms workspace to modify the default information displayed about a task.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# 自定義任務詳細資訊頁 {#customizing-the-task-details-page}

任務詳細資訊頁面包含有關任務及其進程的資訊。 不過，您可以自訂任務詳細資訊頁面，以新增或刪除資訊。

您可以將以下資訊添加到任務詳細資訊頁中：

* 任務的JSON物件中可用的資訊( [AEM Forms工作區中的「工作」區段「JSON物件說明](/help/forms/using/html-workspace-json-object-description.md)」)
* 流程例項的JSON物件中可用的資訊( [AEM Forms工作區中的「流程例項」區段「JSON物件說明](/help/forms/using/html-workspace-json-object-description.md)」)

要自定義任務詳細資訊頁，請執行以下操作：

1. 依循 [AEM Forms工作區自訂的一般步驟。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 若要顯示其他資訊，請在「區塊>區塊>區塊> `translation.json` 區塊」的檔 `todo`案中新 `details`增對應的鍵值 `app`對 [`required`]。

   該 [ 塊 `required`是指可用塊] ，如任務資訊的任務塊、進程資訊的進程塊，以及暫掛任務資訊的當前暫掛任務塊。

   例如，要在任務詳細資訊頁中添加有關「需要路由選擇」的資訊，可以在任務塊中添加以下鍵值對：

   ```
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >為所有支援的語言新增對應的金鑰值配對。

1. 複製 `/libs/ws/js/runtime/templates/taskdetails.html` 至 `/apps/ws/js/runtime/templates/taskdetails.html`。

   將新資訊添加到 `/apps/ws/js/runtime/templates/taskdetails.html`。 例如：

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. 開啟/apps/ws/js/registry.js進行編輯。

   搜尋並取代 `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` 為 `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`。

>[!NOTE]
>
>若要使用在AEM Forms工作區的「開始處理」標籤中建立的工作來自訂工作詳細資訊頁面，請將新資訊新增至 ****`/apps/ws/js/runtime/templates/startprocess.html`。
>
>若要為在詳細資料頁面中新增的資訊新增樣式，請使用「工作區自訂」中的「使用者介面變更」區段來修 *改CSS*[檔案](/help/forms/using/changing-locale-user-interface.md#main-pars-header-3)。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
