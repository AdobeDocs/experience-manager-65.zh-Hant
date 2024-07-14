---
title: 在工作摘要窗格中顯示資訊
description: 在AEM Forms工作區中，「工作摘要」窗格可設定為摘要工作或顯示任何其他網頁。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 在工作摘要窗格中顯示資訊 {#displaying-information-in-the-task-summary-pane}

當您在AEM Forms工作區中開啟任務時，「任務摘要」窗格會顯示任務的摘要。 這項工作的相關額外資訊為AEM Forms工作區的一般使用者增加了更多價值。

AEM Forms工作區可讓您在「工作摘要」窗格中顯示您所選擇的網頁。 您可以使用Workbench建立處理以顯示「工作摘要」窗格。

1. 在Workbench中建立「指定作業」處理。 如需指派工作作業的詳細資訊，請參閱[Workbench說明](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)中的服務參考主題。

   >[!NOTE]
   >
   >如果TaskSummary URL存在，預設會開啟Task Summary檢視，而不是表單檢視。 在這種情況下，即使使用者在指派任務中啟用了「以最大化模式開啟表單」選項，表單也不會以最大化模式開啟。

1. 設定[工作摘要URL]欄位。 您可以指定常值、範本、變數或XPath運算式。
1. 以下是「工作摘要」頁面上顯示資訊的範例。

   * 在`https://'[server]:[port]'/lc/crx/de`登入CRXDE Lite環境。
   * `Create a node`**SampleSummary** ` under `/content` with type `nt：unstructured`. In the properties of this node, add `sling：resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr：read` privileges.`
   * `/apps`下的&#x200B;`Create a folder`**SampleSummary**。 在`/apps/SampleSummary`的存取控制清單中，新增允許`jcr:readprivileges`的`PERM_WORKSPACE_USER`專案。
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

   * 在指派工作步驟中將工作摘要URL的值設定為`/lc/content/SampleSummary.html`。
   * 在AEM Forms工作區中開啟與此指派工作步驟相關聯的工作時，`/apps/SampleSummary`的`html.esp`會在工作摘要窗格中呈現。
