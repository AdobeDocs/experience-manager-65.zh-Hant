---
title: 自定義任務的頁籤
seo-title: Customizing tabs for a task
description: How-to在LiveCycleAEM Forms工作區中自定義任務的頁籤名稱。
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 自定義任務的頁籤 {#customizing-tabs-for-a-task}

可以自定義 `Start Process` 元件 `Start Process` Uber的觀點 `Task Details` 元件 `ToDo` Uber的觀點。

1. 關注 [AEM Forms工作區定製的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 更改 `tabname`的 `translation.json` 的子菜單。

   例如，更改 `/apps/ws/locales/en-US/translation.json` 中輸入。

   * 對於在啟動過程中啟動的任務，請使用 `"startprocess" : {}` 框。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 對於To-do中的任務，請使用 `"todo" : {}` 框。

   ```json
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >為所有支援的語言添加相應的鍵值對。
