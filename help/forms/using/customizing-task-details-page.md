---
title: 自定義任務詳細資訊頁
seo-title: Customizing the task details page
description: How-to在AEM Forms工作區中自定義任務詳細資訊頁面以修改顯示的有關任務的預設資訊。
seo-description: How-to customize the task details page in AEM Forms workspace to modify the default information displayed about a task.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 自定義任務詳細資訊頁 {#customizing-the-task-details-page}

任務詳細資訊頁面包含有關任務及其進程的資訊。 但是，您可以自定義任務詳細資訊頁面以添加或刪除資訊。

您可以將以下資訊添加到任務詳細資訊頁面：

* 任務的JSON對象中可用的資訊(中的「任務」部分 [AEM Forms工作區JSON對象說明](/help/forms/using/html-workspace-json-object-description.md))
* 進程實例的JSON對象中可用的資訊(中的「進程實例」部分 [AEM Forms工作區JSON對象說明](/help/forms/using/html-workspace-json-object-description.md))

要自定義任務詳細資訊頁，請執行以下操作：

1. 關注 [AEM Forms工作區定製的一般步驟。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 要顯示任何附加資訊，請向 `translation.json` 檔案 `todo`塊> `details`塊> `app`塊> [ `required`塊]。

   的 [ `required`塊] 引用可用塊，如任務資訊的任務塊、流程資訊的流程塊和待定任務資訊的當前待處理任務塊。

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
   >為所有支援的語言添加相應的鍵值對。

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

   搜索和替換 `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` 與 `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`。

>[!NOTE]
>
>使用在 **啟動進程** 頁籤，將新資訊添加到 `/apps/ws/js/runtime/templates/startprocess.html`。
>
>要為在詳細資訊頁面中添加的資訊添加新樣式，請使用 *用戶介面更改* 部分 [工作區自定義](changing-locale-user-interface.md)。
