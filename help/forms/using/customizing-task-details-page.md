---
title: 自訂工作詳細資訊頁面
description: 如何在AEM Forms工作區中自訂任務詳細資訊頁面，以修改顯示的有關任務的預設資訊。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 自訂工作詳細資訊頁面 {#customizing-the-task-details-page}

作業詳細資訊頁面包含作業及其流程的資訊。 不過，您可以自訂工作詳細資訊頁面來新增或刪除資訊。

您可以將下列資訊新增至工作詳細資訊頁面：

* 任務的JSON物件中可用的資訊(任務區段位於 [AEM Forms工作區JSON物件說明](/help/forms/using/html-workspace-json-object-description.md))
* 程式執行個體的JSON物件中可用的資訊（中的程式執行個體區段） [AEM Forms工作區JSON物件說明](/help/forms/using/html-workspace-json-object-description.md))

若要自訂工作詳細資訊頁面，請執行下列動作：

1. 追隨 [AEM Forms工作區自訂的一般步驟。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 若要顯示任何其他資訊，請將對應的索引鍵/值組新增至 `translation.json` 檔案位於 `todo`區塊> `details`區塊> `app`區塊> [`required`區塊].

   此 [`required`區塊] 參考可用的區塊，例如工作資訊的工作區塊、處理資訊的處理區塊，以及擱置工作資訊的目前擱置工作區塊。

   例如，若要在工作詳細資訊頁面中新增有關「需要路由選擇」的資訊，您可以在工作區塊中新增下列索引鍵/值組：

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
   >為所有支援的語言新增對應的機碼值組。

1. 複製 `/libs/ws/js/runtime/templates/taskdetails.html` 至 `/apps/ws/js/runtime/templates/taskdetails.html`.

   將新資訊新增至 `/apps/ws/js/runtime/templates/taskdetails.html`. 例如：

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

   搜尋和取代 `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` 替換為 `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>若要使用在中建立的任務自訂任務詳細資訊頁面 **開始程式** AEM Forms標籤，將新資訊新增至 `/apps/ws/js/runtime/templates/startprocess.html`.
>
>若要為新增至詳細資訊頁面的資訊新增樣式，請使用 *使用者介面變更* 中的區段 [工作區自訂](changing-locale-user-interface.md).
