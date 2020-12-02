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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 自定義任務{#customizing-tabs-for-a-task}的頁籤

您可以在`Start Process` Uber視圖中為`Start Process`元件自定義頁籤名稱，在`ToDo` Uber視圖中為`Task Details`元件自定義頁籤名稱。

1. 請依照[AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)進行。
1. 變更`translation.json`檔案中的`tabname`值。

   例如，將英文的`/apps/ws/locales/en-US/translation.json`變更為下列。

   * 對於在啟動進程中啟動的任務，請使用`"startprocess" : {}`塊中的以下代碼片段。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 對於To-do中的任務，請使用`"todo" : {}`塊中的以下代碼片段。

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
   >為所有支援的語言新增對應的金鑰值對。
