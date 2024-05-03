---
title: 在工作摘要窗格中顯示資訊
description: 在AEM Forms工作區中，「工作摘要」窗格可設定為摘要工作或顯示任何其他網頁。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 在工作摘要窗格中顯示資訊 {#displaying-information-in-the-task-summary-pane}

當您在AEM Forms工作區中開啟任務時，「任務摘要」窗格會顯示任務的摘要。 這項工作的相關額外資訊為AEM Forms工作區的一般使用者增加了更多價值。

AEM Forms工作區可讓您在「工作摘要」窗格中顯示您所選擇的網頁。 您可以使用Workbench建立處理以顯示「工作摘要」窗格。

1. 在Workbench中建立「指定作業」處理。 如需有關「指派工作」作業的詳細資訊，請參閱下列主題中的服務參考： [Workbench說明](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >如果TaskSummary URL存在，預設會開啟Task Summary檢視，而不是表單檢視。 在這種情況下，即使使用者在指派任務中啟用了「以最大化模式開啟表單」選項，表單也不會以最大化模式開啟。

1. 設定[工作摘要URL]欄位。 您可以指定常值、範本、變數或XPath運算式。
1. 以下是「工作摘要」頁面上顯示資訊的範例。

   * 登入CRXDE Lite環境： `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**範例摘要** ` under `/content` with type `nt：unstructured`. In the properties of this node, add `sling：resourceType` of type String and value `範例摘要`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr：read` privileges.`
   * `Create a folder`**範例摘要** 在 `/apps`. 在存取控制清單中 `/apps/SampleSummary`，新增專案 `PERM_WORKSPACE_USER` 允許 `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * 將任務摘要URL的值設為 `/lc/content/SampleSummary.html` 在指派工作步驟中。
   * 在AEM Forms工作區中開啟與此指派工作步驟相關聯的工作時， `html.esp` 在 `/apps/SampleSummary` 會在工作摘要窗格中呈現。
