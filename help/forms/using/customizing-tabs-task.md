---
title: 自訂任務的標籤
description: 如何在LiveCycleAEM Forms工作區中自訂您工作的標簽名稱。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 自訂任務的標籤 {#customizing-tabs-for-a-task}

您可以在`Start Process` Uber檢視中自訂`Start Process`元件的標簽名稱，並在`ToDo` Uber檢視中自訂`Task Details`元件。

1. 執行[AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 變更`translation.json`檔案中`tabname`的值。

   例如，將英文的`/apps/ws/locales/en-US/translation.json`變更為下列內容。

   * 對於在啟動程式中啟動的工作，請使用`"startprocess" : {}`區塊中的下列程式碼片段。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 對於待辦事項中的工作，請使用`"todo" : {}`區塊中的下列程式碼片段。

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
   >為所有支援的語言新增對應的機碼值組。
