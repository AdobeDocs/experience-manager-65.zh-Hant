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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 自定義任務詳細資訊頁{#customizing-the-task-details-page}

任務詳細資訊頁面包含有關任務及其進程的資訊。 不過，您可以自訂任務詳細資訊頁面，以新增或刪除資訊。

您可以將以下資訊添加到任務詳細資訊頁中：

* 工作的JSON物件中可用的資訊（[AEM Forms工作區中的「工作」區段JSON物件說明](/help/forms/using/html-workspace-json-object-description.md)）
* 進程例項的JSON物件（[AEM Forms工作區中的「處理例項」區段JSON物件說明](/help/forms/using/html-workspace-json-object-description.md)）中的可用資訊

要自定義任務詳細資訊頁，請執行以下操作：

1. 遵循[AEM Forms工作區自訂的一般步驟。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 要顯示其他資訊，請將相應的鍵值對添加到`todo`塊> `details`塊> `app`塊> [塊`required`塊]的`translation.json`檔案。

   [ `required`塊]引用可用塊，如任務資訊的任務塊、進程資訊的進程塊和待定任務資訊的當前待定任務塊。

   例如，要在任務詳細資訊頁中添加有關「需要路由選擇」的資訊，可以在任務塊中添加以下鍵值對：

   ```json
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

1. 將`/libs/ws/js/runtime/templates/taskdetails.html`複製到`/apps/ws/js/runtime/templates/taskdetails.html`。

   將新資訊添加到`/apps/ws/js/runtime/templates/taskdetails.html`。 例如：

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

   搜尋並將`text!/lc/libs/ws/js/runtime/templates/taskdetails.html`取代為`text!/lc/apps/ws/js/runtime/templates/taskdetails.html`。

>[!NOTE]
>
>若要使用在AEM Forms工作區的&#x200B;**啟動程式**&#x200B;標籤中建立的工作來自訂工作詳細資訊頁面，請將新資訊新增至`/apps/ws/js/runtime/templates/startprocess.html`。
>
>要為詳細資訊頁面中添加的資訊添加新樣式，請使用[ Workspace Customization](changing-locale-user-interface.md)中的&#x200B;*User interface changes*&#x200B;部分修改CSS檔案。
