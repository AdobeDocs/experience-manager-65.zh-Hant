---
title: 自訂追蹤表格
description: 如何在AEM Forms工作區的「追蹤」標籤中顯示的工作表格中，自訂顯示使用者程式詳細資訊的方式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 9ab657cc-fa8e-4168-8a68-e38ac5c51b29
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# 自訂追蹤表格{#customize-tracking-tables}

AEM Forms工作區中的追蹤索引標籤是用來顯示登入使用者涉及之程式執行個體的詳細資訊。 若要檢視追蹤表格，請先在左窗格中選取處理名稱，以在中間窗格中檢視其執行處理清單。 選取程式執行處理，在右窗格中檢視此執行處理產生的任務表格。 依照預設，表格欄會顯示下列工作屬性（工作模型中的對應屬性會以括弧指定）：

* ID ( `taskId`)
* 名稱( `stepName`)
* 指示( `instructions`)
* 選取的動作( `selectedRoute`)
* 建立時間( `createTime`)
* 完成時間( `completeTime`)
* 所有者( `currentAssignment.queueOwner`)

任務模型中可顯示在任務表格中的其餘屬性包括：

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>reminderCount</p> </td>
  </tr>
  <tr>
   <td><p>classOfTask</p> </td>
   <td><p>isOwner</p> </td>
   <td><p>routeList</p> </td>
  </tr>
  <tr>
   <td><p>consultGroupId</p> </td>
   <td><p>isRouteSelectionRequired</p> </td>
   <td><p>savedFormCount</p> </td>
  </tr>
  <tr>
   <td><p>contenttype</p> </td>
   <td><p>isShowAttachments</p> </td>
   <td><p>serializedImageTicket</p> </td>
  </tr>
  <tr>
   <td><p>createTime</p> </td>
   <td><p>isStartTask</p> </td>
   <td><p>serviceName</p> </td>
  </tr>
  <tr>
   <td><p>creationId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextReminder</p> </td>
   <td><p>showACLActions</p> </td>
  </tr>
  <tr>
   <td><p>期限</p> </td>
   <td><p>numForms</p> </td>
   <td><p>showDirectActions</p> </td>
  </tr>
  <tr>
   <td><p>說明</p> </td>
   <td><p>numFormsToBeSaved</p> </td>
   <td><p>狀態</p> </td>
  </tr>
  <tr>
   <td><p>顯示名稱</p> </td>
   <td><p>outOfOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfOfficeUserName</p> </td>
   <td><p>supportssave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovalUI</p> </td>
   <td><p>優先順序</p> </td>
   <td><p>taskACL</p> </td>
  </tr>
  <tr>
   <td><p>isCustomUI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>taskFormType</p> </td>
  </tr>
  <tr>
   <td><p>isDefaultImage</p> </td>
   <td><p>processinstancestatus</p> </td>
   <td><p>taskUserInfo</p> </td>
  </tr>
  <tr>
   <td><p>isLocked</p> </td>
   <td><p>processVariables</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p>isMustOpenToComplete</p> </td>
   <td><p>readerSubmitOptions</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

對於工作表中的下列自訂，您需要在原始程式碼中進行語意變更。 另請參閱 [自訂AEM Forms工作區簡介](/help/forms/using/introduction-customizing-html-workspace.md) 瞭解如何使用Workspace SDK進行語意變更，以及從變更的來源建立縮制的套件。

## 變更表格欄及其順序 {#changing-table-columns-and-their-order}

1. 若要修改表格中顯示的工作屬性及其順序，請設定檔案/ws/js/runtime/templates/processinstancehistory.html ：

   ```html
   <table>
       <thead>
           <tr>
               <!-- put the column headings in order here, for example-->
               <th><%= $.t('history.fixedTaskTableHeader.taskName')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskInstructions')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskRoute')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCreateTime')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCompleteTime')%></th>
           </tr>
       </thead>
   </table>
   ```

   ```html
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example, -->
               <td><%= task.stepName %></td>
               <td><%= task.instructions %></td>
               <td><%= !task.selectedRoute?'':(task.selectedRoute=='null'?'Default':task.selectedRoute) %></td>
               <td><%= task.createTime?task.formattedCreateTime:'' %></td>
               <td><%= task.completeTime? task.formattedCompleteTime:'' %></td>
           </tr>
           <%});%>
       </tbody>
   </table>
   ```

## 排序追蹤表格 {#sorting-a-tracking-table}

若要在按一下欄標題時排序工作清單表格：

1. 登入的點選處理常式 `.fixedTaskTableHeader th` 在檔案中 `js/runtime/views/processinstancehistory.js`.

   ```javascript
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   在處理常式中，呼叫 `onTaskTableHeaderClick` 函式 `js/runtime/util/history.js`.

   ```javascript
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. 公開 `TaskTableHeaderClick` 中的方法 `js/runtime/util/history.js`.

   此方法會從按一下事件尋找工作屬性、排序該屬性上的工作清單，並呈現工作表格與排序的工作清單。

   藉由提供比較器函式，使用工作清單集合上的骨幹排序函式完成排序。

   ```javascript
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```javascript
   onTaskTableHeaderClick = function (event) {
           var target = $(event.target),
            comparator,
               attribute;
           if(target.hasClass('taskName')){
            attribute = 'stepName';
           } else if(target.hasClass('taskInstructions')){
               attribute = 'instructions';
           } else if(target.hasClass('taskRoute')){
               attribute = 'selectedRoute';
           } else if(target.hasClass('taskCreateTime')){
               attribute = 'createTime';
           } else if(target.hasClass('taskCompleteTime')){
               attribute = 'completeTime';
           }
           taskList.comparator = function (task) {
            return task.get(attribute);
           };
           taskList.sort();
           render();
       };
   ```
