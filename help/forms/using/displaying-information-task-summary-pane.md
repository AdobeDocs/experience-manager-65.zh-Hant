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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在「任務摘要」窗格中顯示資訊 {#displaying-information-in-the-task-summary-pane}

當您在AEM Forms工作區中開啟工作時，「工作摘要」窗格會顯示工作摘要。 這項額外的相關工作資訊為AEM Forms工作區的使用者增加了更多價值。

AEM Forms工作區可讓您在「任務摘要」窗格中顯示您選擇的網頁。 可以建立一個流程，以使用「工作台」顯示「任務匯總」窗格。

1. 在工作台中建立分配任務流程。 有關「分配任務」操作的詳細資訊，請參閱「工作台幫助」中的「服 [務參考」主題](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)。

   >[!NOTE]
   >
   >如果TaskSummary URL存在，則預設情況下會開啟Task Summary視圖，而不開啟Form視圖。 在這種情況下，即使用戶在「分配任務」中啟用「以最大模式開啟表單」選項，表單也不會以最大模式開啟。

1. 配置任務摘要URL欄位。 您可以指定常值、範本、變數或XPath運算式。
1. 下面是顯示「任務摘要」頁上資訊的示例。

   * 請登錄到CRXDE Lite環境，網址為 `https://[server]:[port]/lc/crx/de`。
   * `Create a node`**SampleSummary **/` under `contentnt:` with type `unstructredsling:`. In the properties of this node, add `resourceTypeSampleSummaryPERM_WORKSPACE_` of type String and value ``. In the Access Control List of this node, add an entry for `` allowing `USERjcr:read` privileges.`
   * `Create a folder`**SampleSummary **，在`/apps`下。 在的「訪問控制列`/apps/SampleSummary`表」中，添加允許的`PERM_WORKSPACE_USER`條目`jcr:readprivileges`。
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummaryhtml.esp`.`

   ```
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

   * 設定任務摘要URL的值，如「分配任 `/lc/content/SampleSummary.html` 務」步驟中。
   * 當在AEM Forms工作區中開啟與此「指派任務」步驟相關聯的工作時， `html.esp` at會 `/apps/SampleSummary` 在任務摘要窗格中呈現。


[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
