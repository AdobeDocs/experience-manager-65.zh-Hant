---
title: 參與工作流程
seo-title: 參與工作流程
description: 工作流程通常包括要求人員在頁面或資產上執行活動的步驟。
seo-description: 工作流程通常包括要求人員在頁面或資產上執行活動的步驟。
uuid: 15d56bcc-1e84-4cc0-8b71-7fb906cd7ff7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: f170613c-329e-446b-9ac3-350615f1bfb6
docset: aem65
exl-id: e47270e8-bace-4d0f-a088-7269b6356315
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 1%

---

# 參與工作流程{#participating-in-workflows}

工作流程通常包括要求人員在頁面或資產上執行活動的步驟。 工作流選擇要執行活動的用戶或組，並將工作項指派給該人員或組。 使用者會收到通知，然後可以採取適當的動作：

* [檢視通知](#notifications-of-available-workflow-actions)
* [完成參與者步驟](#completing-a-participant-step)
* [委派參與者步驟](#delegating-a-participant-step)
* [在參與者步驟上執行退步](#performing-step-back-on-a-participant-step)
* [開啟工作流項以查看詳細資訊（並執行操作）](#opening-a-workflow-item-to-view-details-and-take-actions)
* [檢視工作流程裝載（多個資源）](#viewing-the-workflow-payload-multiple-resources)

## 可用工作流操作通知{#notifications-of-available-workflow-actions}

當您被指派工作項目時(例如「核准內 **容**」)，會出現各種警報和/或通知：

* 您的[notification](/help/sites-authoring/inbox.md)指示器（工具欄）將增加：

   ![](do-not-localize/wf-57.png)

* 項目將列在通知[收件箱](/help/sites-authoring/inbox.md)中：

   ![wf-58](assets/wf-58.png)

* 使用頁面編輯器時，狀態列會顯示：

   * 要套用至頁面的工作流程名稱；例如Request for Activation。
   * 工作流當前步驟的當前用戶可用的任何操作；例如，完成、委派、檢視詳細資訊。
   * 頁面要遵循的工作流程數。 您可以：

      * 使用向左/向右箭頭瀏覽各種工作流程的狀態資訊。
      * 按一下/點選實際數字，開啟所有適用工作流程的下拉式清單，然後選取您要顯示在狀態列中的工作流程。

   ![wf-59](assets/wf-59.png)

   >[!NOTE]
   >
   >狀態欄僅對具有工作流權限的用戶可見；例如，`workflow-users`組的成員。
   >
   >
   >當目前使用者直接參與工作流程的目前步驟時，就會顯示動作。

* 為資源開啟&#x200B;**時間軸**&#x200B;時，將顯示工作流步驟。 當您按一下/點選警報橫幅時，也會顯示可用的動作：

   ![screen-shot_2019-03-05at120453](assets/screen-shot_2019-03-05at120453.png)

### 完成參與者步驟{#completing-a-participant-step}

您可以完成項目，讓工作流程繼續進行下一個步驟。

在此動作上，您可以指出：

* **下一步**:下一步要採取；您可以從提供的清單中選取
* **評論**:必要

您可以從以下任一步驟完成參與者步驟：

* [收件匣](#completing-a-participant-step-inbox)
* [頁面編輯器](#completing-a-participant-step-page-editor)
* [時間軸](#completing-a-participant-step-timeline)
* [開啟工作流項以查看詳細資訊時](#opening-a-workflow-item-to-view-details-and-take-actions)。

#### 完成參與者步驟 — 收件箱{#completing-a-participant-step-inbox}

使用以下過程完成工作項：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選/按一下縮圖）。
1. 從工具欄中選擇&#x200B;**Complete**。
1. 將開啟&#x200B;**完成工作項**&#x200B;對話框。 從下拉式選取器中選取&#x200B;**下一步**，並視需要新增&#x200B;**註解**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止操作）。

#### 完成參與者步驟 — 頁面編輯器{#completing-a-participant-step-page-editor}

使用以下過程完成工作項：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從頂部的狀態欄中選擇&#x200B;**Complete**。
1. 將開啟&#x200B;**完成工作項**&#x200B;對話框。 從下拉式選取器中選取&#x200B;**下一步**，並視需要新增&#x200B;**註解**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止操作）。

#### 完成參與者步驟 — 時間表{#completing-a-participant-step-timeline}

您也可以使用時間軸來完成和推進步驟：

1. 選擇所需的頁並開啟&#x200B;**時間軸**（或開啟&#x200B;**時間軸**&#x200B;並選擇該頁）:

   ![screen-shot_2019-03-05at120744](assets/screen-shot_2019-03-05at120744.png)

1. 按一下/點選警報橫幅以顯示可用動作。 選擇&#x200B;**Advance**:

   ![screen-shot_2019-03-05at120453-1](assets/screen-shot_2019-03-05at120453-1.png)

1. 您可以根據工作流程選取下一個步驟：

   ![screen-shot_2019-03-05at120905](assets/screen-shot_2019-03-05at120905.png)

1. 選擇&#x200B;**Advance**&#x200B;以確認操作。

### 委派參與者步驟{#delegating-a-participant-step}

如果已指派步驟給您，但由於任何原因您無法採取動作，您可以將步驟委派給其他使用者或群組。

可用於委派的用戶取決於為誰分配了工作項：

* 如果工作項已分配給組，則組成員可用。
* 如果工作項目被指派給某個組，然後被委派給某個用戶，則可使用組成員和組。
* 如果工作項已分配給單個用戶，則無法委派工作項。

在此動作上，您可以指出：

* **使用者**:要委派給的用戶；您可以從提供的清單中選取
* **評論**:必要

您可以從以下任一位置委派參與者步驟：

* [收件匣](#delegating-a-participant-step-inbox)
* [頁面編輯器](#delegating-a-participant-step-page-editor)
* [時間軸](#delegating-a-participant-step-timeline)
* [開啟工作流項以查看詳細資訊時](#opening-a-workflow-item-to-view-details-and-take-actions)。

#### 委派參與者步驟 — 收件箱{#delegating-a-participant-step-inbox}

使用以下過程來委派工作項：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選/按一下縮圖）。
1. 從工具欄中選擇&#x200B;**委派**。
1. 對話方塊將會開啟。 從下拉式選取器（這也可以是群組）中指定&#x200B;**User**，並視需要新增&#x200B;**Comment**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止操作）。

#### 委派參與者步驟 — 頁面編輯器{#delegating-a-participant-step-page-editor}

使用以下過程來委派工作項：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從頂部的狀態欄中選擇&#x200B;**委派**。
1. 對話方塊將會開啟。 從下拉式選取器（這也可以是群組）中指定&#x200B;**User**，並視需要新增&#x200B;**Comment**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止操作）。

#### 委派參與者步驟 — 時間軸{#delegating-a-participant-step-timeline}

您也可以使用時間軸來委派和/或指派步驟：

1. 選擇所需的頁，然後開啟&#x200B;**時間軸**（或開啟&#x200B;**時間軸**&#x200B;並選擇該頁）。
1. 按一下/點選警報橫幅以顯示可用動作。 選擇&#x200B;**更改受託人**:

   ![screen-shot_2019-03-05at120453-2](assets/screen-shot_2019-03-05at120453-2.png)

1. 指定新的受託人：

   ![screen-shot_2019-03-05at121025](assets/screen-shot_2019-03-05at121025.png)

1. 選擇&#x200B;**Assign**&#x200B;以確認操作。

### 對參與者步驟{#performing-step-back-on-a-participant-step}執行退步

如果您發現需要重複某個步驟或一系列步驟，您可以退後一步。 這可讓您選取先前在工作流程中發生的步驟，以進行重新處理。 工作流程會回到您指定的步驟，然後從那裡繼續。

在此動作上，您可以指出：

* **上一步**:要返回的步驟；您可以從提供的清單中選取
* **評論**:必要

您可以從以下任一步驟中對參與者步驟執行後退：

* [收件匣](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)
* [時間軸](#performing-step-back-on-a-participant-step-timeline)
* [開啟工作流項以查看詳細資訊時](#opening-a-workflow-item-to-view-details-and-take-actions)。

#### 在參與者步驟上執行步驟 — 收件箱{#performing-step-back-on-a-participant-step-inbox}

請依照下列程式進行退步：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選/按一下縮圖）。
1. 選擇&#x200B;**後退**&#x200B;以開啟對話框。

1. 指定&#x200B;**上一步**，並根據需要添加&#x200B;**注釋**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止操作）。

#### 在參與者步驟上執行步驟 — 頁面編輯器{#performing-step-back-on-a-participant-step-page-editor}

請依照下列程式進行退步：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從頂部的狀態欄中選擇&#x200B;**後退**。
1. 指定&#x200B;**上一步**，並根據需要添加&#x200B;**注釋**。
1. 使用&#x200B;**OK**&#x200B;完成步驟（或使用&#x200B;**Cancel**&#x200B;中止操作）。

#### 對參與者步驟執行退步 — 時間軸{#performing-step-back-on-a-participant-step-timeline}

您也可以使用時間軸來回復到上一個步驟：

1. 選擇所需的頁，然後開啟&#x200B;**時間軸**（或開啟&#x200B;**時間軸**&#x200B;並選擇該頁）。
1. 按一下/點選警報橫幅以顯示可用動作。 選擇&#x200B;**回滾**:

   ![screen-shot_2019-03-05at121131](assets/screen-shot_2019-03-05at121131.png)

1. 指定工作流程應返回的步驟：

   ![screen-shot_2019-03-05at121158](assets/screen-shot_2019-03-05at121158.png)

1. 選擇&#x200B;**回滾**&#x200B;以確認操作。

### 開啟工作流項以查看詳細資訊（並執行操作）{#opening-a-workflow-item-to-view-details-and-take-actions}

查看工作流工作項的詳細資訊並採取相應操作。

工作流程詳細資訊會顯示在標籤中，而工具列中會提供適當的動作：

* **** WORKITEM頁簽：

   ![wf-72](assets/wf-72.png)

* **工作流** 資訊頁簽：

   ![wf-73](assets/wf-73.png)

   如果已為模型配置了[工作流階段](/help/sites-developing/workflows.md#workflow-stages)，則可以根據以下內容查看進度：

   ![wf-107](assets/wf-107.png)

* **** COMMENTS索引標籤：

   ![wf-75](assets/wf-75.png)

您可以從以下任一位置開啟工作項詳細資訊：

* [收件匣](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)

#### 開啟工作流詳細資訊 — 收件箱{#opening-workflow-details-inbox}

要開啟工作流項並查看詳細資訊，請執行以下操作：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選/按一下縮圖）。
1. 選擇&#x200B;**開啟**&#x200B;以開啟資訊頁簽。

1. 如果需要，請選擇相應的操作，提供任何詳細資訊並使用&#x200B;**OK**（或&#x200B;**Cancel**）進行確認。
1. 使用&#x200B;**Save**&#x200B;或&#x200B;**Cancel**&#x200B;退出。

#### 開啟工作流詳細資訊 — 頁面編輯器{#opening-workflow-details-page-editor}

要開啟工作流項並查看詳細資訊，請執行以下操作：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從狀態欄中選擇&#x200B;**查看詳細資訊**&#x200B;以開啟資訊頁簽。

1. 如果需要，請選擇相應的操作，提供任何詳細資訊並使用&#x200B;**OK**（或&#x200B;**Cancel**）進行確認。
1. 使用&#x200B;**Save**&#x200B;或&#x200B;**Cancel**&#x200B;退出。

### 檢視工作流程裝載（多個資源）{#viewing-the-workflow-payload-multiple-resources}

您可以檢視與工作流程例項相關聯的裝載的詳細資訊。 一開始會顯示套件中的資源，然後您可以向下切入以顯示個別頁面。

若要檢視工作流程例項的裝載和資源：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其採取動作的工作流程項目（點選/按一下縮圖）。
1. 從工具欄中選擇&#x200B;**查看裝載**&#x200B;以開啟對話框。

   由於工作流包只是指向儲存庫內路徑的指針的集合，因此您可以在此處添加/刪除/修改條目，以調整工作流包引用的內容。 使用&#x200B;**資源定義**&#x200B;元件添加新條目。

   ![wf-78](assets/wf-78.png)

1. 連結可用來開啟個別頁面。
