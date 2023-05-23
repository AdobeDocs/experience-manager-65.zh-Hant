---
title: 在ToDo清單中顯示其他資料
seo-title: Displaying additional data in ToDo list
description: How-to自定義LiveCycleAEM Forms工作區的待辦事項清單的顯示，以顯示除預設值之外的更多資訊。
seo-description: How-to customize the display of the To-do list of LiveCycle AEM Forms workspace to show more information besides the default.
uuid: 9467c655-dce2-43ce-8e8f-54542fe81279
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fed3b562-bcc2-4fb7-8fd2-35b1ac621e16
docset: aem65
exl-id: f8b84f13-02d3-4787-95e1-25fd684e6d3b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# 在ToDo清單中顯示其他資料{#displaying-additional-data-in-todo-list}

預設情況下，AEM Forms工作區待辦事項清單顯示任務顯示名稱和說明。 但是，您可以添加其他資訊，如建立日期、截止日期。 您還可以添加表徵圖並更改顯示的樣式。

![查看顯示預設配置的HTML工作區待辦事項頁籤](assets/html-todo-list.png)

本文詳細介紹了添加要在「待辦事項」清單中顯示的每個任務資訊的步驟。

## 可添加的內容 {#what-can-be-added}

您可以在中添加可用資訊 `task.json` 由伺服器發送。 資訊可以作為純文字檔案添加，也可以使用樣式來設定資訊的格式。

有關JSON對象說明的詳細資訊，請參見 [這個](/help/forms/using/html-workspace-json-object-description.md) 文章。

## 顯示任務資訊 {#displaying-information-on-a-task}

1. 關注 [AEM Forms工作區定製的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md)。
1. 要顯示任務的附加資訊，必須在任務塊中添加相應的鍵值對 `translation.json`。

   例如更改 `/apps/ws/locales/en-US/translation.json` 英文：

   ```json
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >為所有支援的語言添加相應的鍵值對。

1. 例如，在任務塊內添加資訊：

   ```json
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## 為新屬性定義CSS {#defining-css-for-the-new-property}

1. 您可以將樣式應用於添加到任務中的資訊（屬性）。 為此，需要為添加到的新屬性添加樣式資訊 `/apps/ws/css/newStyle.css`。

   例如，添加：

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## 在HTML模板中添加條目 {#adding-entry-in-the-html-template}

最後，您需要在dev包中為要添加到任務的每個屬性包含一個條目。 要建立一個，請參閱構建AEM Forms工作區代碼。

1. 複製 `task.html`:

   * 從: `/libs/ws/js/runtime/templates/`
   * 至: `/apps/ws/js/runtime/templates/`

1. 將新資訊添加到 `/apps/ws/js/runtime/templates/task.html`。

   例如，在下面添加 `div class="taskProperties"`:

   ```jsp
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
