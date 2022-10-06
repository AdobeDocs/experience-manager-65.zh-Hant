---
title: 自定義任務的頁簽
seo-title: Customizing tabs for a task
description: 在LiveCycleAEM Forms工作區中，自訂工作之索引標籤的名稱。
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

# 自定義任務的頁簽 {#customizing-tabs-for-a-task}

您可以自訂 `Start Process` 元件(位於 `Start Process` Uber視圖和 `Task Details` 元件(位於 `ToDo` Uber的觀點。

1. 關注 [AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md).
1. 變更 `tabname`在 `translation.json` 檔案。

   例如，變更 `/apps/ws/locales/en-US/translation.json` 對下列內容進行修改。

   * 對於在啟動過程中啟動的任務，請使用 `"startprocess" : {}` 封鎖。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 若為待辦事項中的工作，請從 `"todo" : {}` 封鎖。

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
   >為所有支援的語言新增對應的索引鍵值組。
