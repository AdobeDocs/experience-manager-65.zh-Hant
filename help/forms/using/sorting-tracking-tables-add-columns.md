---
title: 自訂追蹤表格
seo-title: 自訂追蹤表格
description: How-to customize the display of user processes in the task table displayed in the AEM Forms workspace.
seo-description: How-to customize the display of user processes in the task table displayed in the AEM Forms workspace.
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 自訂追蹤表格{#customize-tracking-tables}

AEM Forms工作區中的追蹤標籤可用來顯示涉及登入使用者的程式例項的詳細資料。 若要檢視追蹤表格，請先在左窗格中選取程式名稱，以在中間窗格中查看其例項清單。 選擇一個進程實例，在右窗格中查看由此實例生成的任務表。 預設情況下，表列顯示以下任務屬性（任務模型中的相應屬性在括弧中給出）:

* ID ( `taskId`)
* 名稱 ( `stepName`)
* 說明 ( `instructions`)
* 選取的動作 ( `selectedRoute`)
* 建立時間( `createTime`)
* 完成時間( `completeTime`)
* 所有者 ( `currentAssignment.queueOwner`)

任務模型中可用於顯示在任務表中的其餘屬性為：

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>rementCount</p> </td>
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
   <td><p>contentType</p> </td>
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
   <td><p>nextRements</p> </td>
   <td><p>showACLAactions</p> </td>
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
   <td><p>displayName</p> </td>
   <td><p>outOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfficeUserName</p> </td>
   <td><p>supportsSave</p> </td>
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
   <td><p>processInstanceStatus</p> </td>
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

對於任務表中的以下自定義，您需要在原始碼中進行語義更改。 請參 [閱自訂AEM Forms工作區簡介](/help/forms/using/introduction-customizing-html-workspace.md) ，瞭解如何使用工作區SDK進行語義變更，以及從變更的來源建立精簡的套件。

## 更改表列及其順序 {#changing-table-columns-and-their-order}

1. 要修改表中顯示的任務屬性及其順序，請配置檔案/ws/js/runtime/templates/processinstancehistory.html :

   ```as3
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

   ```as3
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example -->
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

## 對追蹤表格排序 {#sorting-a-tracking-table}

要在按一下列標題時對任務清單表進行排序，請執行以下操作：

1. 在檔案中註冊點按 `.fixedTaskTableHeader th` 處理常式 `js/runtime/views/processinstancehistory.js`。

   ```as3
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   在處理程式中，調用 `onTaskTableHeaderClick` 的函式 `js/runtime/util/history.js`。

   ```as3
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. 在中公 `TaskTableHeaderClick` 開方法 `js/runtime/util/history.js`。

   該方法從click事件中查找任務屬性，對該屬性上的任務清單進行排序，並使用排序的任務清單呈現任務表。

   通過提供比較器功能，使用任務清單集合上的Backbone排序功能進行排序。

   ```as3
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```as3
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

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
