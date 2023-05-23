---
title: 在「任務摘要」窗格中顯示資訊
seo-title: Displaying information in the Task Summary pane
description: 在AEM Forms工作區中，可以配置「任務摘要」窗格來匯總任務或顯示任何其他網頁。
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 在「任務摘要」窗格中顯示資訊 {#displaying-information-in-the-task-summary-pane}

在AEM Forms工作區中開啟任務時，「任務摘要」窗格可顯示任務摘要。 任務的這些附加和相關資訊為AEM Forms工作區的最終用戶增加了更多價值。

AEM Forms工作區允許您在「任務摘要」窗格中顯示您選擇的網頁。 可以建立一個流程，以使用Workbench顯示「任務匯總」窗格。

1. 在工作台中建立分配任務流程。 有關分配任務操作的詳細資訊，請參閱中的「服務參考」主題 [工作台幫助](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)。

   >[!NOTE]
   >
   >如果存在TaskSummary URL，則預設情況下會開啟Task Summary（任務摘要）視圖，而不是Form（表單）視圖。 在這種情況下，即使用戶在分配任務中啟用「以最大化模式開啟表單」選項，表單也不會以最大化模式開啟。

1. 配置「任務摘要URL」欄位。 可以指定文本值、模板、變數或XPath表達式。
1. 下面是在「任務摘要」頁上顯示資訊的示例。

   * 登錄到CRXDE Lite環境，位於 `https://'[server]:[port]'/lc/crx/de`。
   * `Create a node`**示例摘要** ` under `/內容` with type `nt：非結構化`. In the properties of this node, add `sling:resourceType` of type String and value `示例摘要`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr：讀取` privileges.`
   * `Create a folder`**示例摘要** 在 `/apps`。 在的訪問控制清單中 `/apps/SampleSummary`，為 `PERM_WORKSPACE_USER` 允許 `jcr:readprivileges`。
   * `Create a file `html.esp` at `/apps/示例摘要`. For example, add the following lines in `html.esp`.`

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

   * 將任務摘要URL的值設定為 `/lc/content/SampleSummary.html` 在分配任務步驟中。
   * 在AEM Forms工作區中開啟與此分配任務步驟關聯的任務時， `html.esp` 在 `/apps/SampleSummary` 在任務摘要窗格中呈現。
