---
title: 在AEM收件匣中管理Forms應用程式和任務
seo-title: Manage Forms applications and tasks in AEM Inbox
description: AEM收件匣可讓您透過提交應用程式和管理工作來啟動以Forms為中心的工作流程。
seo-description: AEM Inbox allows you to launch Forms-centric workflows through submitting applications and manage tasks.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: document_services, publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
exl-id: 8d17194b-8baf-4878-b3ae-d351a056aebf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 2%

---

# 在AEM收件匣中管理Forms應用程式和任務{#manage-forms-applications-and-tasks-in-aem-inbox}

啟動或觸發以Forms為中心的工作流程的許多方式之一，就是透過AEM收件匣中的應用程式。 您需要建立工作流程應用程式，才能讓Forms工作流程在收件匣中作為應用程式可用。 如需工作流程應用程式和其他啟動Forms工作流程方法的詳細資訊，請參閱 [在OSGi上啟動以Forms為中心的工作流程](../../forms/using/aem-forms-workflow.md#launch).

此外，AEM收件匣整合來自各種AEM元件(包括Forms工作流程)的通知和工作。 觸發包含「分配」任務步驟的表單工作流時，關聯的應用程式將作為任務列在受託人的收件箱中。 如果受託人是組，則任務將出現在所有組成員的收件箱中，直到單個人請求或委託任務為止。

「收件箱」用戶介面提供清單和日曆視圖以查看任務。 您也可以配置檢視設定。 您可以根據各種參數來篩選任務。 如需檢視和篩選器的詳細資訊，請參閱 [您的收件匣](/help/sites-authoring/inbox.md).

總之，收件箱允許您建立新應用程式並管理分配的任務。

>[!NOTE]
>
>您必須是工作流程使用者群組的成員，才能使用AEM收件匣。

## 建立應用程式 {#create-application}

1. 前往AEM收件匣，網址為https://&#39;[伺服器]:[埠]「/aem/inbox」。
1. 在收件匣UI中，點選 **[!UICONTROL 建立>應用程式]**. 此時將出現「選擇應用程式」頁。
1. 選取應用程式並按一下 **[!UICONTROL 建立]**. 與應用程式相關聯的最適化表單隨即開啟。 填寫最適化表單中的資訊，然後點選 **[!UICONTROL 提交]**. 它會啟動關聯的工作流，並在受託人的收件匣中建立任務。

## 管理任務 {#manage-tasks}

當Forms工作流程觸發且您是受託人或受託人群組的一部分時，工作會出現在收件匣中。 您可以從收件箱中查看任務詳細資訊並對任務執行可用操作。

### 聲明或委派任務 {#claim-or-delegate-tasks}

指派給群組的任務會顯示在所有群組成員的收件匣中。 任何組成員都可以聲明該任務或將其委派給另一個組成員。 若要這麼做：

1. 點選以選取工作的縮圖。 開啟或委派任務的選項會顯示在頂端。

   ![選擇任務](assets/select-task.png)

1. 執行下列任一項作業：

   * 若要委派工作，請點選 **[!UICONTROL 委派]**. 「委派項目」(Delegate Item)對話框開啟。 選取使用者、選擇性新增註解，然後點選 **[!UICONTROL 確定]**.

   ![委派](assets/delegate.png)

   * 要聲明任務，請點選 **[!UICONTROL 開啟]**. 將開啟「指派給自身」對話框。 點選 **[!UICONTROL 繼續]** 來申請任務。 聲明的任務將以您作為收件箱中的受託人的身份顯示。

   ![索賠](assets/claim.png)

### 查看詳細資訊並執行任務操作 {#view-details-and-perform-actions-on-tasks}

開啟任務時，可以查看任務詳細資訊並執行可用操作。 在關聯的Forms工作流的「分配任務」步驟中定義了任務可用的操作。

1. 點選以選取工作的縮圖。 開啟或委派所選任務的選項顯示在頂部。
1. 點選 **開啟** 查看任務詳細資訊並採取操作。 將開啟詳細的任務視圖。 在此視圖中，您可以查看任務詳細資訊並對任務執行操作。

   >[!NOTE]
   >
   >如果任務被分配給組，則必須聲明它能夠在詳細視圖中開啟它。

![任務詳細資訊](assets/task-details.png)

詳細的任務視圖包括以下幾節：

* 任務詳細資訊
* 表單
* 工作流程資訊
* 動作工具列

#### 任務詳細資訊 {#task-details}

「任務詳細資訊」部分顯示有關任務的資訊。 顯示的資訊取決於 [分配任務步驟](/help/sites-developing/workflows-step-ref.md) 在工作流程中。 上例顯示用於任務的說明、狀態、開始日期和工作流。 它也允許將檔案附加到任務。

#### 表單 {#form}

主要內容區域中的「表單」索引標籤會顯示已提交的表單和欄位層級附件（如果有）。

#### 工作流程資訊 {#workflow-details}

頂部的「工作流詳細資訊」頁簽顯示任務在工作流中各個階段的進度。 它顯示任務的已完成、當前和待定階段。 工作流程的階段定義於 [分配任務步驟](/help/sites-developing/workflows-step-ref.md) 的子句。

此外，索引標籤會顯示工作流程中每個已完成階段的任務歷史記錄。 您可以點選 **[!UICONTROL 檢視詳細資料]** 以了解該階段的詳細資訊。 它顯示有關任務的備注、表單和任務附件、狀態、開始和結束日期等。

![工作流程詳細資訊](assets/workflow-details.png)

#### 動作工具列 {#actions-toolbar}

「操作」工具欄顯示該任務的所有可用選項。 雖然「儲存」、「重設」和「委派」是預設動作，但其他可用動作則設定於 [分配任務步驟](/help/sites-developing/workflows-step-ref.md). 在上述範例中，工作流程中已設定「核准」和「拒絕」。

當您對任務採取動作時，它會在工作流程中繼續進行。

### 查看已完成的任務 {#view-completed-tasks}

AEM收件匣只會顯示作用中任務。 已完成的任務不會顯示在清單中。 但是，您可以使用收件箱篩選器來根據任務類型、狀態、開始和結束日期等參數來篩選任務。 要查看已完成的任務：

1. 在AEM收件匣中，點選 ![切換側面板1](assets/toggle-side-panel1.png) 來開啟篩選選擇器。
1. 點選 **[!UICONTROL 任務狀態]** 折疊式功能表及選取 **[!UICONTROL 完成]**. 所有已完成的任務都會顯示。

   ![filter](assets/filter.png)

1. 點選以選取任務，然後按一下 **[!UICONTROL 開啟]**.

該任務將開啟，以顯示與任務關聯的文檔或最適化表單。 對於最適化表單，任務將顯示只讀適用性表單或其記錄PDF文檔，如 [分配任務工作流步驟](/help/sites-developing/workflows-step-ref.md).

「任務詳細資訊」部分顯示了已採取的操作、任務狀態、開始日期和結束日期等資訊。

![已完成任務](assets/completed-task.png)

此 **[!UICONTROL 工作流程詳細資訊]** 索引標籤會顯示工作流程的每個步驟。 點選 **[!UICONTROL 查看詳細資訊]** 以取得詳細資訊。

![completed-task-workflow](assets/completed-task-workflow.png)

## 疑難排解 {#troubleshooting-workflows}

### 無法在AEM收件匣中檢視與AEM工作流程相關的項目 {#unable-to-see-aem-worklow-items}

工作流模型擁有者無法在AEM收件匣中檢視與AEM Workflow相關的項目。 若要解決此問題，請將下列索引新增至您的AEM存放庫並重建索引。

1. 使用下列其中一種方法來新增索引：

   * 在CRX DE中於建立下列節點 `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` 下表所指定的個別屬性：

      | 節點 | 屬性 | 類型 |
      |---|---|---|
      | sharedWith | sharedWith | 字串 |
      | 鎖定 | 鎖定 | 布林值 |
      | 傳回 | 傳回 | 布林值 |
      | allowInboxSharing | allowInboxSharing | 布林值 |
      | allowExplicitSharing | allowExplicitSharing | 布林值 |


   * 透過AEM套件部署索引。 您可以使用 [AEM原型](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/developing/archetype) 建立可部署AEM套件的專案。 使用下列范常式式碼，將索引新增至AEM原型專案：

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [建立屬性索引並將其設為true](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/queries-and-indexing.html#the-property-index).

1. 在CRX DE中設定索引或透過套件部署後， [重新索引儲存庫](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex).

https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/queries-and-indexing.html
