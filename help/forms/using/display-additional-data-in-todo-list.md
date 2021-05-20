---
title: 在ToDo清單中顯示其他資料
seo-title: 在ToDo清單中顯示其他資料
description: 自訂LiveCycleAEM Forms工作區待辦事項清單的顯示方式，以顯示預設值以外的詳細資訊。
seo-description: 自訂LiveCycleAEM Forms工作區待辦事項清單的顯示方式，以顯示預設值以外的詳細資訊。
uuid: 9467c655-dce2-43ce-8e8f-54542fe81279
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fed3b562-bcc2-4fb7-8fd2-35b1ac621e16
docset: aem65
exl-id: f8b84f13-02d3-4787-95e1-25fd684e6d3b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 在ToDo清單{#displaying-additional-data-in-todo-list}中顯示其他資料

依預設，AEM Forms工作區待辦事項清單會顯示任務顯示名稱和說明。 不過，您可以新增其他資訊，例如建立日期、截止日期。 您也可以新增圖示並變更顯示的樣式。

![查看顯示預設設定的HTML工作區待辦事項標籤](assets/html-todo-list.png)

本文詳細說明了為「待辦事項」清單中的每個任務添加顯示資訊的步驟。

## 可新增的內容{#what-can-be-added}

可以添加伺服器發送的`task.json`中可用的資訊。 資訊可以以純文字檔案形式添加，也可以使用樣式來格式化資訊。

如需JSON物件說明的詳細資訊，請參閱[this](/help/forms/using/html-workspace-json-object-description.md)文章。

## 顯示任務{#displaying-information-on-a-task}的資訊

1. 請依照[AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md)操作。
1. 要顯示任務的其他資訊，必須在`translation.json`的任務塊中添加相應的鍵值值對。

   例如，英文的`/apps/ws/locales/en-US/translation.json`變更：

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
   >為所有支援的語言新增對應的索引鍵值配對。

1. 例如，在任務塊內添加資訊：

   ```json
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## 定義新屬性{#defining-css-for-the-new-property}的CSS

1. 您可以將樣式套用至新增至任務的資訊（屬性）。 為此，需要為添加到`/apps/ws/css/newStyle.css`的新屬性添加樣式資訊。

   例如，新增：

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## 在HTML範本{#adding-entry-in-the-html-template}中新增項目

最後，您需要在開發套件中加入要新增至任務之每個屬性的項目。 若要建立，請參閱建立AEM Forms工作區程式碼。

1. 複製 `task.html`:

   * 從: `/libs/ws/js/runtime/templates/`
   * 至: `/apps/ws/js/runtime/templates/`

1. 將新資訊添加到`/apps/ws/js/runtime/templates/task.html`。

   例如，在`div class="taskProperties"`下新增：

   ```jsp
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
