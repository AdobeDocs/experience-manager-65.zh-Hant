---
title: 在「任務摘要」窗格中顯示資訊
seo-title: 在「任務摘要」窗格中顯示資訊
description: 在AEM Forms工作區中，可以設定「任務摘要」窗格來摘要任務或顯示任何其他網頁。
seo-description: 在AEM Forms工作區中，可以設定「任務摘要」窗格來摘要任務或顯示任何其他網頁。
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 在「任務摘要」窗格{#displaying-information-in-the-task-summary-pane}中顯示資訊

在AEM Forms工作區中開啟任務時，「任務摘要」窗格可以顯示任務的摘要。 此額外的相關任務資訊可為AEM Forms工作區的使用者增加更多價值。

AEM Forms工作區可讓您在「任務摘要」窗格中顯示您選擇的網頁。 可以建立一個流程以使用Workbench顯示「任務摘要」窗格。

1. 在Workbench中建立分配任務流程。 有關「分配任務」操作的詳細資訊，請參閱[Workbench幫助](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)中的服務參考主題。

   >[!NOTE]
   >
   >如果存在TaskSummary URL，則預設會開啟Task Summary視圖，而非Form視圖。 在這種情況下，即使用戶在「分配任務」中啟用「以最大化模式開啟表單」選項，表單也不會以最大化模式開啟。

1. 配置「任務摘要URL」欄位。 您可以指定常值、範本、變數或XPath運算式。
1. 下面是在「任務摘要」頁上顯示資訊的示例。

   * 在`https://'[server]:[port]'/lc/crx/de`登入CRXDE Lite環境。
   * `Create a node`**SampleSummary** ` under `/` with type `contentt:`. In the properties of this node, add `unstructedsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**** 下方的SampleSummary  `/apps`。在`/apps/SampleSummary`的訪問控制清單中，為`PERM_WORKSPACE_USER`添加允許`jcr:readprivileges`的條目。
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
   * 在AEM Forms工作區中開啟與此分配任務步驟關聯的任務時，在`/apps/SampleSummary`處的`html.esp`將呈現在任務摘要窗格中。
