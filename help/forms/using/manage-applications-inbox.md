---
title: 管理AEM收件匣中的Forms應用程式和工作
description: AEM收件匣可讓您透過提交應用程式和管理工作來啟動以Forms為中心的工作流程。
contentOwner: vishgupt
topic-tags: document_services, publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 8d17194b-8baf-4878-b3ae-d351a056aebf
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 2%

---

# 管理AEM收件匣中的Forms應用程式和工作{#manage-forms-applications-and-tasks-in-aem-inbox}

啟動或觸發以Forms為中心的工作流程的多種方式之一，就是透過AEM收件匣中的應用程式。 若要讓Forms工作流程在收件匣中成為應用程式，請建立工作流程應用程式。 如需工作流程應用程式和啟動Forms工作流程其他方法的詳細資訊，請參閱 [在OSGi上啟動以Forms為中心的工作流程](../../forms/using/aem-forms-workflow.md#launch).

此外，AEM收件匣會整合來自各種AEM元件(包括Forms工作流程)的通知和工作。 當觸發包含「指派」任務步驟的表單工作流程時，相關聯的應用程式會在受指派人的收件匣中列為任務。 如果受指派人是群組，則該任務會出現在所有群組成員的「收件匣」中，直到個別人員宣告或委派該任務為止。

收件匣使用者介面提供清單和行事曆檢視以檢視工作。 您也可以配置檢視設定。 您可以根據各種引數篩選任務。 如需有關檢視和篩選的詳細資訊，請參閱 [您的收件匣](/help/sites-authoring/inbox.md).

簡而言之，「收件匣」可讓您建立應用程式及管理指派的工作。

>[!NOTE]
>
>您必須是工作流程 — 使用者群組的成員，才能使用AEM收件匣。

## 建立應用程式 {#create-application}

1. 前往AEM收件匣，網址為https://&#39;[伺服器]：[連線埠]&#39;/aem/inbox.
1. 在收件匣UI中，選取 **[!UICONTROL 建立>應用程式]**. 便會顯示「選取應用程式」頁面。
1. 選取應用程式並按一下 **[!UICONTROL 建立]**. 與應用程式關聯的最適化表單隨即開啟。 在最適化表單中填寫資訊，然後選取 **[!UICONTROL 提交]**. 它會啟動關聯的工作流程，並在受指派人的收件匣中建立任務。

## 管理任務 {#manage-tasks}

當Forms工作流程觸發時，而您是受指派人或受指派人群組的一部分，任務會出現在您的收件匣中。 您可以在「收件匣」中檢視任務詳細資訊，並對任務執行可用的動作。

### 申請或委派任務 {#claim-or-delegate-tasks}

指派給群組的任務會出現在所有群組成員的收件匣中。 任何群組成員都可以要求該任務或將其委派給其他群組成員。 若要這麼做：

1. 選取以選取任務的縮圖。 用於開啟或委派任務的選項會顯示在頂端。

   ![選擇任務](assets/select-task.png)

1. 執行下列任一項作業：

   * 若要委派任務，請選取 **[!UICONTROL 委派]**. 「委派專案」對話方塊開啟。 選取使用者，並選擇性地新增註解，然後選取 **[!UICONTROL 確定]**.

   ![委派](assets/delegate.png)

   * 若要宣告工作，請選取 **[!UICONTROL 開啟]**. 「指派給自己」對話方塊開啟。 選取 **[!UICONTROL 繼續]** 以宣告任務。 您作為受指派人會出現在您的收件匣中。

   ![索賠](assets/claim.png)

### 檢視詳細資料並對任務執行動作 {#view-details-and-perform-actions-on-tasks}

當您開啟任務時，可以檢視任務詳細資訊並執行可用的動作。 任務可用的動作會在相關Forms工作流程的指派任務步驟中定義。

1. 選取以選取任務的縮圖。 頂端會顯示開啟或委派所選任務的選項。
1. 選取 **開啟** 以檢視工作詳細資訊。 詳細任務檢視隨即開啟。 在此檢視中，您可以檢視任務詳細資訊並處理任務。

   >[!NOTE]
   >
   >如果將任務指派給群組，您必須宣告它能在詳細檢視中開啟。

![task-details](assets/task-details.png)

詳細的工作檢視包含下列區段：

* 任務詳細資訊
* 表單
* 工作流程資訊
* 動作工具列

#### 任務詳細資訊 {#task-details}

「工作詳細資訊」段落顯示工作的相關資訊。 顯示的資訊取決於 [指派任務步驟](/help/sites-developing/workflows-step-ref.md) 在工作流程中。 上述範例顯示用於工作的說明、狀態、開始日期和工作流程。 它還允許將檔案附加到任務。

#### 表單 {#form}

主要內容區域中的「表單」標籤會顯示已提交的表單和欄位層級附件（如果有）。

#### 工作流程資訊 {#workflow-details}

頂端的「工作流程詳細資訊」標籤會顯示工作流程中各個階段的任務進度。 它會顯示任務的已完成階段、目前階段及擱置階段。 工作流程的階段定義於 [指派任務步驟](/help/sites-developing/workflows-step-ref.md) 相關聯工作流程的。

此外，索引標籤會顯示工作流程中每個已完成階段的任務歷史記錄。 您可以選取 **[!UICONTROL 檢視詳細資料]** 完成階段的相關資訊。 它會顯示有關任務的註解、表單及工作附件、狀態、開始與結束日期等。

![workflow-details](assets/workflow-details.png)

#### 動作工具列 {#actions-toolbar}

「動作」工具列會顯示任務的所有可用選項。 「儲存」、「重設」和「委派」是預設動作，其他可用動作則配置於 [指派任務步驟](/help/sites-developing/workflows-step-ref.md). 在上述範例中，核准和拒絕是在工作流程中設定。

當您處理任務時，它會在工作流程中繼續進行。

### 檢視完成的任務 {#view-completed-tasks}

AEM收件匣只會顯示作用中的任務。 已完成的任務未出現在清單中。 不過，您可以使用收件匣篩選器根據數個引數來篩選任務，例如任務型別、狀態以及開始和結束日期。 若要檢視已完成的工作，請執行下列動作：

1. 在AEM收件匣中，選取 ![toggle-side-panel1](assets/toggle-side-panel1.png) 以開啟篩選選擇器。
1. 選取 **[!UICONTROL 任務狀態]** 摺疊式功能表及選取 **[!UICONTROL 完成]**. 所有已完成的任務都會出現。

   ![篩選](assets/filter.png)

1. 選取以選取工作並按一下 **[!UICONTROL 開啟]**.

任務會開啟以顯示與任務相關聯的檔案或最適化表單。 針對最適化表單，任務會顯示在的「表單/檔案」索引標籤中設定的唯讀最適化表單或其PDF記錄檔案 [指派任務工作流程步驟](/help/sites-developing/workflows-step-ref.md).

任務詳細資訊區段會顯示已執行動作、任務狀態、開始日期和結束日期等資訊。

![completed-task](assets/completed-task.png)

此 **[!UICONTROL 工作流程詳細資訊]** 標籤會顯示工作流程的每個步驟。 選取 **[!UICONTROL 檢視詳細資料]** 以取得詳細資訊。

![completed-task-workflow](assets/completed-task-workflow.png)

## 疑難排解 {#troubleshooting-workflows}

### 無法在AEM收件匣中檢視與AEM工作流程相關的專案 {#unable-to-see-aem-worklow-items}

工作流程模型所有者無法在AEM收件匣中檢視與AEM工作流程相關的專案。 若要解決此問題，請將下列索引新增至您的AEM存放庫並重新建立索引。

1. 使用下列其中一種方法來新增索引：

   * 在CRX DE中的建立以下節點： `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` 各自屬性，如下表所指定：

     | 節點 | 屬性 | 類型 |
     |---|---|---|
     | sharedwith | sharedwith | 字串 |
     | 鎖定 | 鎖定 | 布林值 |
     | 已傳回 | 已傳回 | 布林值 |
     | allowInboxShare | allowInboxShare | 布林值 |
     | allowExplicitSharing | allowExplicitSharing | 布林值 |


   * 透過AEM套件部署索引。 您可以使用 [AEM原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en) 專案以建立可部署的AEM套件。 使用以下範常式式碼，將索引新增至AEM Archetype專案：

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [建立屬性索引並將其設定為true](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html#the-property-index).

1. 在CRX DE中設定索引或透過套件部署後， [重新索引存放庫](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex).

https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html
