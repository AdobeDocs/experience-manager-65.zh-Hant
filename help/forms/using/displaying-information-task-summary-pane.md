---
title: 在「任務摘要」窗格中顯示資訊
seo-title: 在「任務摘要」窗格中顯示資訊
description: 在AEM Forms工作區中，可以設定「工作摘要」窗格來摘要工作或顯示任何其他網頁。
seo-description: 在AEM Forms工作區中，可以設定「工作摘要」窗格來摘要工作或顯示任何其他網頁。
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# 在「任務摘要」窗格中顯示資訊{#displaying-information-in-the-task-summary-pane}

當您在AEM Forms工作區中開啟工作時，「工作摘要」窗格會顯示工作摘要。 這項額外的相關工作資訊為AEM Forms工作區的使用者增加了更多價值。

AEM Forms工作區可讓您在「任務摘要」窗格中顯示您選擇的網頁。 可以建立一個流程，以使用「工作台」顯示「任務匯總」窗格。

1. 在工作台中建立分配任務流程。 有關「分配任務」操作的詳細資訊，請參閱[Workbench Help](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)中的「服務參考」主題。

   >[!NOTE]
   >
   >如果TaskSummary URL存在，則預設情況下會開啟Task Summary視圖，而不開啟Form視圖。 在這種情況下，即使用戶在「分配任務」中啟用「以最大模式開啟表單」選項，表單也不會以最大模式開啟。

1. 配置任務摘要URL欄位。 您可以指定常值、範本、變數或XPath運算式。
1. 下面是顯示「任務摘要」頁上資訊的示例。

   * 在`https://'[server]:[port]'/lc/crx/de`登錄到CRXDE Lite環境。
   * `Create a node`**SampleSummary** ` under `/` with type `contentnt:`. In the properties of this node, add `unstructredsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**范** 例摘要 `/apps`。在`/apps/SampleSummary`的「訪問控制清單」中，為`PERM_WORKSPACE_USER`添加允許`jcr:readprivileges`的條目。
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummaryhtml.esp`.`

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

   * 在「分配任務」步驟中，將任務摘要url的值設定為`/lc/content/SampleSummary.html`。
   * 當在AEM Forms工作區中開啟與此「指派任務」步驟相關聯的任務時，`/apps/SampleSummary`的`html.esp`會呈現在任務摘要窗格中。
