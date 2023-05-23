---
title: 自定義跟蹤表
seo-title: Customize tracking tables
description: How-to自定義在AEM Forms工作區的跟蹤頁籤中顯示的任務表中顯示用戶進程詳細資訊。
seo-description: How-to customize the display of the details of user processes in the task table displayed in the tracking tab of AEM Forms workspace.
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
exl-id: 9ab657cc-fa8e-4168-8a68-e38ac5c51b29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# 自定義跟蹤表{#customize-tracking-tables}

AEM Forms工作區中的跟蹤頁籤用於顯示與登錄用戶相關的進程實例的詳細資訊。 要查看跟蹤表，請首先在左窗格中選擇一個進程名稱，以在中間窗格中查看其實例清單。 選擇一個流程實例，查看右窗格中由此實例生成的任務表。 預設情況下，表列顯示以下任務屬性（任務模型中的相應屬性在括弧中給出）:

* ID ( `taskId`)
* 名稱 ( `stepName`)
* 指示 ( `instructions`)
* 選取的動作 ( `selectedRoute`)
* 建立時間( `createTime`)
* 完成時間( `completeTime`)
* 所有者 ( `currentAssignment.queueOwner`)

任務模型中可用於在任務表中顯示的其餘屬性包括：

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>是OpenFullScreen</p> </td>
   <td><p>提醒計數</p> </td>
  </tr>
  <tr>
   <td><p>類任務</p> </td>
   <td><p>是所有者</p> </td>
   <td><p>路由清單</p> </td>
  </tr>
  <tr>
   <td><p>consultGroupId</p> </td>
   <td><p>是RouteSelectionRequired</p> </td>
   <td><p>已保存的FormCount</p> </td>
  </tr>
  <tr>
   <td><p>內容類型</p> </td>
   <td><p>是ShowAttachments</p> </td>
   <td><p>序列化ImageTicket</p> </td>
  </tr>
  <tr>
   <td><p>建立時間</p> </td>
   <td><p>是StartTask</p> </td>
   <td><p>服務名稱</p> </td>
  </tr>
  <tr>
   <td><p>建立ID</p> </td>
   <td><p>可見</p> </td>
   <td><p>服務標題</p> </td>
  </tr>
  <tr>
   <td><p>當前分配</p> </td>
   <td><p>下一提醒</p> </td>
   <td><p>showACLAactions</p> </td>
  </tr>
  <tr>
   <td><p>截止</p> </td>
   <td><p>數字表單</p> </td>
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
   <td><p>摘要URL</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfOffice用戶名</p> </td>
   <td><p>支援保存</p> </td>
  </tr>
  <tr>
   <td><p>是ApprovalUI</p> </td>
   <td><p>優先順序</p> </td>
   <td><p>任務ACL</p> </td>
  </tr>
  <tr>
   <td><p>是自定義UI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>taskFormType</p> </td>
  </tr>
  <tr>
   <td><p>是DefaultImage</p> </td>
   <td><p>processInstanceStatus</p> </td>
   <td><p>taskUserInfo</p> </td>
  </tr>
  <tr>
   <td><p>已鎖定</p> </td>
   <td><p>processVariables</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p>是MustOpenToComplete</p> </td>
   <td><p>readerSubmitOptions</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

對於任務表中的以下自定義項，需要在原始碼中進行語義更改。 請參閱 [自定義AEM Forms工作區簡介](/help/forms/using/introduction-customizing-html-workspace.md) 有關如何使用workspace SDK進行語義更改，以及如何從更改的源生成精簡包。

## 更改表列及其順序 {#changing-table-columns-and-their-order}

1. 要修改表中顯示的任務屬性及其順序，請配置檔案/ws/js/runtime/templates/processinstancehistory.html :

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

## 對跟蹤表排序 {#sorting-a-tracking-table}

要在按一下列標題時對任務清單表進行排序：

1. 註冊按一下處理程式 `.fixedTaskTableHeader th` 檔案 `js/runtime/views/processinstancehistory.js`。

   ```javascript
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   在處理程式中，調用 `onTaskTableHeaderClick` 函式 `js/runtime/util/history.js`。

   ```javascript
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. 公開 `TaskTableHeaderClick` 方法 `js/runtime/util/history.js`。

   該方法從按一下事件中查找任務屬性，對該屬性上的任務清單進行排序，並使用排序的任務清單呈現任務表。

   通過提供比較器功能，使用任務清單集合上的Backbone排序函式進行排序。

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
