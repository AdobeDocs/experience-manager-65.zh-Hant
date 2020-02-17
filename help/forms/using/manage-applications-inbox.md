---
title: 在AEM收件匣中管理表單應用程式和工作
seo-title: 在AEM收件匣中管理表單應用程式和工作
description: AEM Inbox可讓您透過提交應用程式和管理工作，來啟動以表單為中心的工作流程。
seo-description: AEM Inbox可讓您透過提交應用程式和管理工作，來啟動以表單為中心的工作流程。
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 在AEM收件匣中管理表單應用程式和工作{#manage-forms-applications-and-tasks-in-aem-inbox}

啟動或觸發表單導向工作流程的眾多方式之一，就是透過AEM收件匣中的應用程式。 您需要建立工作流應用程式，使表單工作流作為「收件箱」中的應用程式可用。 如需工作流程應用程式和其他啟動表單工作流程方式的詳細資訊，請參 [閱「在OSGi上啟動表單導向的工作流程」](../../forms/using/aem-forms-workflow.md#launch)。

此外，AEM Inbox會整合來自各種AEM元件（包括表單工作流程）的通知和工作。 當觸發包含「指派」任務步驟的表單工作流時，相關應用程式將作為任務列在受託人的收件箱中。 如果受託人是群組，則任務會出現在所有群組成員的「收件匣」中，直到個別要求或委派該任務為止。

「收件箱」用戶介面提供清單和日曆視圖以查看任務。 您也可以設定檢視設定。 您可以根據各種參數來篩選任務。 有關查看和篩選器的詳細資訊，請參 [閱收件箱](/help/sites-authoring/inbox.md)。

總之，「收件箱」允許您建立新應用程式並管理分配的任務。

>[!NOTE] {graybox=&quot;true&quot;}
>
>您必須是工作流程使用者群組的成員，才能使用AEM Inbox。

## 建立應用程式 {#create-application}

1. 前往https://[server]:[port]/aem/inbox的「AEM Inbox」。
1. 在「收件匣」UI中，點選「 **[!UICONTROL 建立>應用程式」]**。 此時將顯示「選擇應用程式」頁。
1. 選取應用程式，然後按一下「 **[!UICONTROL 建立]**」。 與應用程式相關聯的最適化表單隨即開啟。 在最適化表單中填寫資訊，然後點選「提 **[!UICONTROL 交」]**。 它會啟動關聯的工作流程，並在受託人的「收件匣」中建立工作。

## 管理任務 {#manage-tasks}

當Forms工作流程觸發而您是受託人或受託人群組的一部分時，您的收件匣中就會出現工作。 您可以在收件箱中查看任務詳細資訊並對任務執行可用操作。

### 報銷或委派任務 {#claim-or-delegate-tasks}

指派給群組的任務會出現在所有群組成員的收件箱中。 任何群組成員都可以宣稱該任務或將其委派給另一個群組成員。 若要這麼做：

1. 點選以選取工作的縮圖。 開啟或委派任務的選項會顯示在頂部。

   ![選擇任務](assets/select-task.png)

1. 執行下列任一項作業：

   * 若要委派任務，請點選「委 **[!UICONTROL 派」]**。 「委派項目」(Delegate Item)對話框開啟。 選取使用者、選擇性地新增註解，然後點選「 **[!UICONTROL 確定]**」。
   ![委派](assets/delegate.png)

   * 要聲明任務，請按一下「打 **[!UICONTROL 開」]**。 將開啟「指定給自身」對話框。 點選「 **[!UICONTROL 繼續]** 」以宣告此工作。 聲明的任務將以您作為收件箱中的受託人的身份顯示。
   ![索賠](assets/claim.png)

### 查看詳細資訊並對任務執行操作 {#view-details-and-perform-actions-on-tasks}

開啟任務時，可以查看任務詳細資訊並執行可用操作。 任務可用的操作是在關聯的Forms工作流的「分配」任務步驟中定義的。

1. 點選以選取工作的縮圖。 開啟或委派選定任務的選項將顯示在頂部。
1. 點選「 **開啟** 」以檢視工作詳細資訊並採取動作。 將開啟詳細的任務視圖。 在此視圖中，您可以查看任務詳細資訊並對任務採取操作。

   >[!NOTE]
   >
   >如果任務已分配給組，則必須聲明它能夠在詳細視圖中開啟它。

![task-details](assets/task-details.png)

詳細的任務視圖包括以下幾節：

* 任務詳細資訊
* 表單
* 工作流程詳細資訊
* 動作工具列

#### Task details {#task-details}

「任務詳細資訊」部分顯示有關該任務的資訊。 顯示的資訊取決於工作流中「分配」任 [務步驟的配置](/help/sites-developing/workflows-step-ref.md) 設定。 上例顯示任務的說明、狀態、開始日期和工作流。 它還允許將檔案附加到任務。

#### 表單 {#form}

主要內容區域中的「表單」標籤會顯示已提交的表單和欄位層級附件（如果有的話）。

#### Workflow details {#workflow-details}

頂部的「工作流詳細資訊」頁籤顯示了工作流中各個階段的任務進度。 它顯示任務的已完成、當前和待定階段。 工作流的階段是在關聯工作流的「指 [定任務」(Assign](/help/sites-developing/workflows-step-ref.md) task)步驟中定義的。

此外，該頁籤還顯示工作流中每個已完成階段的任務歷史記錄。 您可以點選「 **[!UICONTROL 檢視詳細資訊]** 」以取得已完成的階段，以瞭解該階段的詳細資訊。 它顯示關於任務的注釋、表單和任務附件、狀態、開始和結束日期等。

![workflow-details](assets/workflow-details.png)

#### 動作工具列 {#actions-toolbar}

「操作」(Actions)工具欄顯示任務的所有可用選項。 雖然「保存」(Save)、「重置」(Reset)和「委派」(Delegate)是預設操作，但「分配」( [Assign)任務步驟中配置了其他可用操作](/help/sites-developing/workflows-step-ref.md)。 在上述範例中，工作流程中已設定「核准」和「拒絕」。

在您對任務採取操作時，該任務將在工作流中進一步執行。

### 檢視完成的工作 {#view-completed-tasks}

AEM收件匣只會顯示作用中的工作。 完成的任務不會顯示在清單中。 但是，您可以使用「收件箱」篩選器根據多個參數（如任務類型、狀態、開始和結束日期等）來篩選任務。 要查看已完成的任務，請執行以下操作：

1. 在「AEM收件匣」中，點 ![選「切換側面板1」](assets/toggle-side-panel1.png) ，以開啟篩選選取器。
1. 點選「 **[!UICONTROL Task Status]** accordion」(任務狀態 **[!UICONTROL )，然後選擇「]** Complete」。 您完成的所有工作都會出現。

   ![濾鏡](assets/filter.png)

1. 點選以選取工作，然後按一下「 **[!UICONTROL 開啟]**」。

此任務將開啟以顯示與任務相關聯的文檔或自適應表單。 對於最適化表單，任務會顯示唯讀最適化表單或其記錄的PDF文檔，如「指派任務」工作流程步驟的「表單／文檔」選 [項卡中所配置](/help/sites-developing/workflows-step-ref.md)。

任務詳細資訊部分顯示已執行的操作、任務狀態、開始日期和結束日期等資訊。

![已完成任務](assets/completed-task.png)

「工 **[!UICONTROL 作流詳細資料]** 」標籤會顯示工作流程的每個步驟。 點選 **[!UICONTROL 檢視詳細資訊]** ，以取得詳細資訊。

![completed-task-workflow](assets/completed-task-workflow.png)

