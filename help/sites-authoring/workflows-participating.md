---
title: 參與工作流程
seo-title: 參與工作流程
description: 工作流程通常包含要求人員在頁面或資產上執行活動的步驟。
seo-description: 工作流程通常包含要求人員在頁面或資產上執行活動的步驟。
uuid: 15d56bcc-1e84-4cc0-8b71-7fb906cd7ff7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: f170613c-329e-446b-9ac3-350615f1bfb6
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 1%

---


# 參與工作流程{#participating-in-workflows}

工作流程通常包含要求人員在頁面或資產上執行活動的步驟。 工作流選擇要執行活動的用戶或組，並將工作項目分配給該人員或組。 使用者會收到通知，然後可採取適當的動作：

* [檢視通知](#notifications-of-available-workflow-actions)
* [完成參與者步驟](#completing-a-participant-step)
* [委派參與者步驟](#delegating-a-participant-step)
* [對參與者步驟執行退一步](#performing-step-back-on-a-participant-step)
* [開啟工作流程項目以檢視詳細資訊（並採取動作）](#opening-a-workflow-item-to-view-details-and-take-actions)
* [檢視工作流程裝載（多個資源）](#viewing-the-workflow-payload-multiple-resources)

## 可用工作流操作通知{#notifications-of-available-workflow-actions}

當您被指派工作項目時(例如「核准內 **容**」)，會出現各種警報和/或通知：

* 您的[通知](/help/sites-authoring/inbox.md)指示符（工具列）將遞增：

   ![](do-not-localize/wf-57.png)

* 項目將列在通知[收件箱](/help/sites-authoring/inbox.md)中：

   ![wf-58](assets/wf-58.png)

* 當您使用頁面編輯器時，狀態列會顯示：

   * 應用於頁面的工作流的名稱；例如，要求啟動。
   * 當前用戶在工作流的當前步驟中可以執行的任何操作；例如，「完成」(Complete)、「委派」(Delegate)、「查看」(View)詳細資訊。
   * 頁面所受的工作流程數。 您可以：

      * 使用向左／向右箭頭來導覽各種工作流程的狀態資訊。
      * 按一下／點選實際數字，以開啟所有適用工作流程的下拉式清單，然後選取您要顯示在狀態列中的工作流程。

   ![wf-59](assets/wf-59.png)

   >[!NOTE]
   >
   >狀態列僅對具有工作流權限的用戶可見；例如，`workflow-users`群組的成員。
   >
   >
   >當目前的使用者直接參與工作流程的目前步驟時，會顯示動作。

* 當為資源開啟&#x200B;**時間軸**&#x200B;時，將顯示工作流步驟。 當您按一下／點選警報橫幅時，也會顯示可用的動作：

   ![screen-shot_2019-03-05at120453](assets/screen-shot_2019-03-05at120453.png)

### 完成參與者步驟{#completing-a-participant-step}

您可以完成項目，讓工作流程繼續下一個步驟。

在此操作中，您可以指明：

* **下一步**:下一步；您可以從提供的清單中選擇
* **評論**:if freed

您可以從以下任一步驟中完成參與者步驟：

* [收件箱](#completing-a-participant-step-inbox)
* [頁面編輯器](#completing-a-participant-step-page-editor)
* [時間軸](#completing-a-participant-step-timeline)
* [開啟工作流程項目以檢視詳細資訊](#opening-a-workflow-item-to-view-details-and-take-actions)時。

#### 完成參與者步驟——收件箱{#completing-a-participant-step-inbox}

請按下列步驟完成工作項目：

1. 開啟&#x200B;**[AEM Inbox](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 從工具欄中選擇&#x200B;**Complete**。
1. 將會開啟&#x200B;**完整工作項目**&#x200B;對話框。 從下拉式選擇器中選取「下一步」**，並視需要新增「注釋」****。**
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止動作）。

#### 完成參與者步驟——頁面編輯器{#completing-a-participant-step-page-editor}

請按下列步驟完成工作項目：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從頂部的狀態欄中選擇&#x200B;**Complete**。
1. 將會開啟&#x200B;**完整工作項目**&#x200B;對話框。 從下拉式選擇器中選取「下一步」**，並視需要新增「注釋」****。**
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止動作）。

#### 完成參與者步驟——時間軸{#completing-a-participant-step-timeline}

您也可以使用時間軸來完成並進行步驟：

1. 選擇所需頁面並開啟&#x200B;**時間軸**（或開啟&#x200B;**時間軸**&#x200B;並選擇頁面）:

   ![screen-shot_2019-03-05at120744](assets/screen-shot_2019-03-05at120744.png)

1. 按一下／點選警報橫幅以顯示可用動作。 選擇&#x200B;**高級**:

   ![screen-shot_2019-03-05at120453-1](assets/screen-shot_2019-03-05at120453-1.png)

1. 您可以根據工作流程來選擇下一個步驟：

   ![screen-shot_2019-03-05at120905](assets/screen-shot_2019-03-05at120905.png)

1. 選擇&#x200B;**Advance**&#x200B;以確認操作。

### 委派參與者步驟{#delegating-a-participant-step}

如果已指派步驟給您，但由於任何原因您無法採取動作，您可以將步驟委派給其他使用者或群組。

可進行委派的用戶取決於分配了工作項目的人員：

* 如果工作項目已指派給群組，則可使用群組成員。
* 如果工作項目已指派給某個組，然後委託給用戶，則可以使用組成員和組。
* 如果工作項目已指派給單一使用者，則無法委派工作項目。

在此操作中，您可以指明：

* **使用者**:要委派給的用戶；您可以從提供的清單中選擇
* **評論**:if freed

您可以從以下任一位置委派參與者步驟：

* [收件箱](#delegating-a-participant-step-inbox)
* [頁面編輯器](#delegating-a-participant-step-page-editor)
* [時間軸](#delegating-a-participant-step-timeline)
* [開啟工作流程項目以檢視詳細資訊](#opening-a-workflow-item-to-view-details-and-take-actions)時。

#### 委派參與者步驟——收件箱{#delegating-a-participant-step-inbox}

使用以下過程來委派工作項目：

1. 開啟&#x200B;**[AEM Inbox](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 從工具欄中選擇&#x200B;**委派**。
1. 對話方塊將會開啟。 從下拉式選擇器中指定&#x200B;**User**（這也可以是群組），並視需要新增&#x200B;**Comment**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止動作）。

#### 委派參與者步驟——頁面編輯器{#delegating-a-participant-step-page-editor}

使用以下過程來委派工作項目：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從頂部的狀態欄中選擇&#x200B;**委派**。
1. 對話方塊將會開啟。 從下拉式選擇器中指定&#x200B;**User**（這也可以是群組），並視需要新增&#x200B;**Comment**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止動作）。

#### 委派參與者步驟——時間軸{#delegating-a-participant-step-timeline}

您也可以使用時間軸來委派和／或指派步驟：

1. 選擇所需頁面並開啟&#x200B;**時間軸**（或開啟&#x200B;**時間軸**&#x200B;並選擇頁面）。
1. 按一下／點選警報橫幅以顯示可用動作。 選擇&#x200B;**變更受託人**:

   ![screen-shot_2019-03-05at120453-2](assets/screen-shot_2019-03-05at120453-2.png)

1. 指定新的受託人：

   ![screen-shot_2019-03-05at121025](assets/screen-shot_2019-03-05at121025.png)

1. 選擇&#x200B;**Assign**&#x200B;以確認操作。

### 對參與者執行退一步步驟{#performing-step-back-on-a-participant-step}

如果您發現需要重複某個步驟或一系列步驟，則可退後一步。 這可讓您選取在工作流程中較早發生的步驟，以進行重新處理。 工作流程會返回您指定的步驟，然後繼續進行。

在此操作中，您可以指明：

* **上一步**:返回的步驟；您可以從提供的清單中選擇
* **評論**:if freed

您可以從以下任一位置對參與者執行退一步：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)
* [時間軸](#performing-step-back-on-a-participant-step-timeline)
* [開啟工作流程項目以檢視詳細資訊](#opening-a-workflow-item-to-view-details-and-take-actions)時。

#### 對參與者步驟執行退一步——收件箱{#performing-step-back-on-a-participant-step-inbox}

請按下列步驟退一步：

1. 開啟&#x200B;**[AEM Inbox](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 選擇&#x200B;**後退**&#x200B;以開啟對話框。

1. 指定&#x200B;**上一步**，並視需要新增&#x200B;**評論**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止動作）。

#### 對參與者步驟執行退一步——頁面編輯器{#performing-step-back-on-a-participant-step-page-editor}

請按下列步驟退一步：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從頂部的狀態欄中選擇「後退」。****
1. 指定&#x200B;**上一步**，並視需要新增&#x200B;**評論**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止動作）。

#### 對參與者步驟執行後退——時間軸{#performing-step-back-on-a-participant-step-timeline}

您也可以使用時間軸來回滾（步驟）回到上一個步驟：

1. 選擇所需頁面並開啟&#x200B;**時間軸**（或開啟&#x200B;**時間軸**&#x200B;並選擇頁面）。
1. 按一下／點選警報橫幅以顯示可用動作。 選擇&#x200B;**回滾**:

   ![screen-shot_2019-03-05at121131](assets/screen-shot_2019-03-05at121131.png)

1. 指定工作流應返回的步驟：

   ![screen-shot_2019-03-05at121158](assets/screen-shot_2019-03-05at121158.png)

1. 選擇&#x200B;**回滾**&#x200B;以確認操作。

### 開啟工作流項以查看詳細資訊（並採取操作）{#opening-a-workflow-item-to-view-details-and-take-actions}

查看工作流工作項目的詳細資訊並採取相應的操作。

工作流詳細資訊顯示在頁籤中，工具欄中提供了相應的操作：

* **「工** 作項目」頁籤：

   ![wf-72](assets/wf-72.png)

* **工作流** 資訊頁籤：

   ![wf-73](assets/wf-73.png)

   如果已為模型配置了[工作流階段](/help/sites-developing/workflows.md#workflow-stages)，則可以根據以下內容查看進度：

   ![wf-107](assets/wf-107.png)

* **「注** 釋」頁籤：

   ![wf-75](assets/wf-75.png)

您可以從以下任一位置開啟工作項目詳細資訊：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)

#### 開啟工作流詳細資訊——收件箱{#opening-workflow-details-inbox}

要開啟工作流項並查看詳細資訊，請執行以下操作：

1. 開啟&#x200B;**[AEM Inbox](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 選擇&#x200B;**開啟**&#x200B;以開啟資訊頁籤。

1. 如果需要，請選擇相應的操作，提供任何詳細資訊並使用&#x200B;**OK**（或&#x200B;**Cancel**）進行確認。
1. 使用&#x200B;**Save**&#x200B;或&#x200B;**Cancel**&#x200B;退出。

#### 開啟工作流詳細資訊——頁面編輯器{#opening-workflow-details-page-editor}

要開啟工作流項並查看詳細資訊，請執行以下操作：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從狀態欄選擇「查看詳細資訊」以開啟資訊頁籤。****

1. 如果需要，請選擇相應的操作，提供任何詳細資訊並使用&#x200B;**OK**（或&#x200B;**Cancel**）進行確認。
1. 使用&#x200B;**Save**&#x200B;或&#x200B;**Cancel**&#x200B;退出。

### 查看工作流負載（多資源）{#viewing-the-workflow-payload-multiple-resources}

您可以檢視與工作流程例項相關聯之裝載的詳細資料。 一開始會顯示套件中的資源，然後您可以下鑽以顯示個別頁面。

要查看工作流實例的裝載和資源，請執行以下操作：

1. 開啟&#x200B;**[AEM Inbox](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選／按一下縮圖）。
1. 從工具欄中選擇「查看裝載」(View Payload)**以開啟對話框。**

   由於工作流包只是儲存庫中路徑的指針的集合，因此您可以在此處添加／刪除／修改條目以調整工作流包引用的內容。 使用&#x200B;**資源定義**&#x200B;元件添加新條目。

   ![wf-78](assets/wf-78.png)

1. 這些連結可用來開啟個別頁面。
