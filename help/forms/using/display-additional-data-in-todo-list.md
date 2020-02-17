---
title: 在ToDo清單中顯示其他資料
seo-title: 在ToDo清單中顯示其他資料
description: How-to自訂LiveCycle AEM Forms工作區「待辦事項」清單的顯示，以顯示除預設值外的更多資訊。
seo-description: How-to自訂LiveCycle AEM Forms工作區「待辦事項」清單的顯示，以顯示除預設值外的更多資訊。
uuid: 9467c655-dce2-43ce-8e8f-54542fe81279
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fed3b562-bcc2-4fb7-8fd2-35b1ac621e16
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 在ToDo清單中顯示其他資料{#displaying-additional-data-in-todo-list}

依預設，AEM Forms工作區待辦項目清單會顯示工作顯示名稱和說明。 不過，您可以新增其他資訊，例如建立日期、截止日期。 您也可以新增圖示並變更顯示的樣式。

![查看顯示預設配置的「HTML工作區待辦事項」頁籤](assets/html-todo-list.png)

本文詳細說明在「待辦事項」清單中新增要顯示每個工作資訊的步驟。

## 可新增的功能 {#what-can-be-added}

您可以新增伺服器所傳送 `task.json` 的可用資訊。 這些資訊可以新增為純文字，或您可使用樣式來設定資訊的格式。

如需JSON物件說明的詳細資訊，請參閱 [本](/help/forms/using/html-workspace-json-object-description.md) 文。

## 顯示任務資訊 {#displaying-information-on-a-task}

1. 請遵循「 [AEM Forms工作區自訂的一般步驟」](../../forms/using/generic-steps-html-workspace-customization.md)。
1. 要顯示任務的附加資訊，必須在的任務塊中添加相應的鍵值對 `translation.json`。

   例如，英文 `/apps/ws/locales/en-US/translation.json` 的變更：

   ```
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
   >為所有支援的語言新增對應的金鑰值配對。

1. 例如，在任務塊中添加資訊：

   ```
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## 定義新屬性的CSS {#defining-css-for-the-new-property}

1. 您可以將樣式應用於添加到任務中的資訊（屬性）。 若要這麼做，您必須新增新增至的新屬性的樣式資訊 `/apps/ws/css/newStyle.css`。

   例如，新增：

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## 在HTML範本中新增項目 {#adding-entry-in-the-html-template}

最後，您需要在dev套件中包含您要新增至工作的每個屬性的項目。 若要建立AEM Forms工作區代碼，請參閱「建立AEM Forms工作區代碼」。

1. 複製 `task.html`:

   * 從: `/libs/ws/js/runtime/templates/`
   * 至: `/apps/ws/js/runtime/templates/`

1. 將新資訊添加到 `/apps/ws/js/runtime/templates/task.html`。

   例如，在 `div class="taskProperties"`:

   ```
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
