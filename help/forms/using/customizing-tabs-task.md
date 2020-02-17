---
title: 自定義任務的頁籤
seo-title: 自定義任務的頁籤
description: How-to自訂LiveCycle AEM Forms工作區中各標籤的名稱。
seo-description: How-to自訂LiveCycle AEM Forms工作區中各標籤的名稱。
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 自定義任務的頁籤 {#customizing-tabs-for-a-task}

您可以在Uber檢視中自訂 `Start Process` 元件的標籤名稱， `Start Process` 在 `Task Details` Uber檢視中自訂元件 `ToDo` 的標籤名稱。

1. 請遵循「 [AEM Forms工作區自訂的一般步驟」](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 更改檔案 `tabname`中的 `translation.json` 值。

   例如，將英 `/apps/ws/locales/en-US/translation.json` 文變更為下列。

   * 對於在啟動進程中啟動的任務，請使用塊中的以下代碼 `"startprocess" : {}` 段。

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 對於To-do中的任務，請使用塊中的以下代碼 `"todo" : {}` 片段。

   ```
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
   >為所有支援的語言新增對應的金鑰值對。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
