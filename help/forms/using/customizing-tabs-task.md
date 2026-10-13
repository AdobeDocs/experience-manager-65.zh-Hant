---
title: 自訂任務的標籤
description: 如何在LiveCycle AEM Forms Workspace中自訂您工作的標簽名稱。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '104'
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
