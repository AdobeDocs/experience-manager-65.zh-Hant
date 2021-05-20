---
title: 自定義任務詳細資訊頁
seo-title: 自定義任務詳細資訊頁
description: 如何自訂AEM Forms工作區中的任務詳細資訊頁面，以修改顯示的任務預設資訊。
seo-description: 如何自訂AEM Forms工作區中的任務詳細資訊頁面，以修改顯示的任務預設資訊。
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 自定義任務詳細資訊頁{#customizing-the-task-details-page}

任務詳細資訊頁包含有關任務及其進程的資訊。 但是，您可以自定義任務詳細資訊頁以添加或刪除資訊。

您可以將下列資訊添加到任務詳細資訊頁：

* 任務的JSON物件中可用的資訊([AEM Forms工作區JSON物件說明](/help/forms/using/html-workspace-json-object-description.md)中的任務區段)
* 處理例項的JSON物件中可用的資訊([AEM Forms工作區JSON物件說明](/help/forms/using/html-workspace-json-object-description.md)中的處理例項區段)

要自定義任務詳細資訊頁，請執行以下操作：

1. 請遵循[AEM Forms工作區自訂的一般步驟。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 若要顯示任何其他資訊，請在`todo`block > `details`block > `app`block > [ `required`block ]向`translation.json`檔案中添加相應的鍵值對。

   [ `required`block]引用了可用塊，如任務資訊的任務塊、進程資訊的進程塊和待定任務資訊的當前待定任務塊。

   例如，要在任務詳細資訊頁中添加有關「所需工藝路線選擇」的資訊，可以在任務塊中添加以下鍵值對：

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
   >為所有支援的語言新增對應的索引鍵值配對。

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
>要使用在AEM Forms工作區的&#x200B;**Start Process**&#x200B;頁簽中建立的任務自定義任務詳細資訊頁，請將新資訊添加到`/apps/ws/js/runtime/templates/startprocess.html`。
>
>若要為詳細資訊頁面中新增的資訊新增樣式，請使用[Workspace自訂](changing-locale-user-interface.md)中的&#x200B;*使用者介面changes*&#x200B;區段來修改CSS檔案。
