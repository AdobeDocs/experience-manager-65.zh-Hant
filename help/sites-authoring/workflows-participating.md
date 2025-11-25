---
title: 工作流程參與率
description: 工作流程通常包括需要人員在頁面或資產上執行活動的步驟。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: e47270e8-bace-4d0f-a088-7269b6356315
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 1%

---

# 參與工作流程{#participating-in-workflows}

工作流程通常包括需要人員在頁面或資產上執行活動的步驟。 工作流程會選取執行活動的使用者或群組，並將工作專案指派給該人員或群組。 使用者會收到通知，然後可以採取適當的動作：

* [檢視通知](#notifications-of-available-workflow-actions)
* [完成參與者步驟](#completing-a-participant-step)
* [委派參與者步驟](#delegating-a-participant-step)
* [對參與者步驟執行後退](#performing-step-back-on-a-participant-step)
* [開啟工作流程專案以檢視詳細資訊（並執行動作）](#opening-a-workflow-item-to-view-details-and-take-actions)
* [檢視工作流程裝載（多個資源）](#viewing-the-workflow-payload-multiple-resources)

## 可用工作流程動作的通知 {#notifications-of-available-workflow-actions}

當您被指派工作項目時(例如「核准內 **容**」)，會出現各種警報和/或通知：

* 您的[通知](/help/sites-authoring/inbox.md)指標（工具列）將會增加：

  ![通知指示器](do-not-localize/wf-57.png)

* 此專案將列在您的通知[收件匣](/help/sites-authoring/inbox.md)中：

  ![wf-58](assets/wf-58.png)

* 使用頁面編輯器時，狀態列將會顯示：

   * 套用至頁面的工作流程名稱，例如「請求啟用」。
   * 目前使用者在工作流程目前步驟中可用的任何動作；例如，完成、委派、檢視詳細資訊。
   * 頁面須遵守的工作流程數量。 您可以：

      * 使用左/右箭頭，導覽各種工作流程的狀態資訊。
      * 按一下實際數字，以開啟所有適用工作流程的下拉式清單，然後選取您要在狀態列中顯示的工作流程。

  ![wf-59](assets/wf-59.png)

  >[!NOTE]
  >
  >只有具有工作流程許可權的使用者才能看到狀態列；例如，`workflow-users`群組的成員。
  >
  >
  >當目前使用者直接參與工作流程的目前步驟時，會顯示動作。

* 當資源的&#x200B;**時間表**&#x200B;開啟時，會顯示工作流程步驟。 當您按一下警示橫幅時，畫面也會顯示可用的動作：

  ![screen-shot_2019-03-05at120453](assets/screen-shot_2019-03-05at120453.png)

### 完成參與者步驟 {#completing-a-participant-step}

您可以完成專案以允許工作流程進行到下一個步驟。

在此動作中，您可以指出：

* **下一步**：下一個要採取的步驟；您可以從提供的清單中選取
* **註解**：如有必要

您可以透過下列任一方式完成參與者步驟：

* [收件匣](#completing-a-participant-step-inbox)
* [頁面編輯器](#completing-a-participant-step-page-editor)
* [時間軸](#completing-a-participant-step-timeline)
* [開啟工作流程專案以檢視詳細資料](#opening-a-workflow-item-to-view-details-and-take-actions)時。

#### 完成參與者步驟 — 收件匣 {#completing-a-participant-step-inbox}

請使用下列步驟完成工作專案：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（按一下縮圖）。
1. 從工具列選取&#x200B;**完成**。
1. **完成工作專案**&#x200B;對話方塊開啟。 從下拉式選取器中選取&#x200B;**下一步**，並視需要新增&#x200B;**註解**。
1. 使用&#x200B;**確定**&#x200B;完成步驟（或使用&#x200B;**取消**&#x200B;中止動作）。

#### 完成參與者步驟 — 頁面編輯器 {#completing-a-participant-step-page-editor}

請使用下列步驟完成工作專案：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從頂端的狀態列選取&#x200B;**完成**。
1. **完成工作專案**&#x200B;對話方塊開啟。 從下拉式選取器中選取&#x200B;**下一步**，並視需要新增&#x200B;**註解**。
1. 使用&#x200B;**確定**&#x200B;完成步驟（或使用&#x200B;**取消**&#x200B;中止動作）。

#### 完成參與者步驟 — 時間表 {#completing-a-participant-step-timeline}

您也可以使用時間表來完成並推進步驟：

1. 選取必要頁面並開啟&#x200B;**時間表** （或開啟&#x200B;**時間表**&#x200B;並選取頁面）：

   ![screen-shot_2019-03-05at120744](assets/screen-shot_2019-03-05at120744.png)

1. 按一下警報橫幅以顯示可用動作。 選取&#x200B;**前進**：

   ![screen-shot_2019-03-05at120453-1](assets/screen-shot_2019-03-05at120453-1.png)

1. 根據工作流程，您可以選取下一個步驟：

   ![screen-shot_2019-03-05at120905](assets/screen-shot_2019-03-05at120905.png)

1. 選取&#x200B;**前進**&#x200B;以確認動作。

### 委派參與者步驟 {#delegating-a-participant-step}

如果已將步驟指派給您，但由於任何原因您無法採取動作，則可以將步驟委派給其他使用者或群組。

可委派的使用者取決於工作專案的指派者：

* 如果工作專案已指派給群組，則群組成員可供使用。
* 如果工作專案已指派給群組，然後又委派給使用者，則群組成員和群組可供使用。
* 如果工作專案已指派給單一使用者，則無法委派工作專案。

在此動作中，您可以指出：

* **使用者**：您要委派給的使用者；您可以從提供的清單中選取
* **註解**：如有必要

您可從下列任一項委派參與者步驟：

* [收件匣](#delegating-a-participant-step-inbox)
* [頁面編輯器](#delegating-a-participant-step-page-editor)
* [時間軸](#delegating-a-participant-step-timeline)
* [開啟工作流程專案以檢視詳細資料](#opening-a-workflow-item-to-view-details-and-take-actions)時。

#### 委派參與者步驟 — 收件匣 {#delegating-a-participant-step-inbox}

請使用下列步驟委派工作專案：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（按一下縮圖）。
1. 從工具列選取&#x200B;**委派**。
1. 對話方塊開啟。 從下拉式選取器中指定&#x200B;**使用者** （也可以是群組），並視需要新增&#x200B;**註解**。
1. 使用&#x200B;**確定**&#x200B;完成步驟（或使用&#x200B;**取消**&#x200B;中止動作）。

#### 委派參與者步驟 — 頁面編輯器 {#delegating-a-participant-step-page-editor}

請使用下列步驟委派工作專案：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從頂端的狀態列選取&#x200B;**委派**。
1. 對話方塊開啟。 從下拉式選取器中指定&#x200B;**使用者** （也可以是群組），並視需要新增&#x200B;**註解**。
1. 使用&#x200B;**確定**&#x200B;完成步驟（或使用&#x200B;**取消**&#x200B;中止動作）。

#### 委派參與者步驟 — 時間表 {#delegating-a-participant-step-timeline}

您也可以使用時間表來委派及/或指派步驟：

1. 選取必要頁面，然後開啟&#x200B;**時間表** （或開啟&#x200B;**時間表**&#x200B;並選取頁面）。
1. 按一下警報橫幅以顯示可用動作。 選取&#x200B;**變更被指定者**：

   ![screen-shot_2019-03-05at120453-2](assets/screen-shot_2019-03-05at120453-2.png)

1. 指定新的被指定者：

   ![screen-shot_2019-03-05at121025](assets/screen-shot_2019-03-05at121025.png)

1. 選取&#x200B;**指派**&#x200B;以確認動作。

### 對參與者步驟執行後退 {#performing-step-back-on-a-participant-step}

如果您發現某個步驟或一系列步驟需要重複，您可以後退。 這可讓您選取工作流程中先前發生的步驟，以便重新處理。 工作流程會回到您指定的步驟，然後從那裡繼續。

在此動作中，您可以指出：

* **上一步**：要傳回到的步驟；您可以從提供的清單中選取
* **註解**：如有必要

您可以透過下列其中一種方式，對參與者步驟執行後退：

* [收件匣](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)
* [時間軸](#performing-step-back-on-a-participant-step-timeline)
* [開啟工作流程專案以檢視詳細資料](#opening-a-workflow-item-to-view-details-and-take-actions)時。

#### 對參與者步驟執行後退 — 收件匣 {#performing-step-back-on-a-participant-step-inbox}

請使用下列步驟來後退：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（按一下縮圖）。
1. 選取&#x200B;**後退**&#x200B;以開啟對話方塊。

1. 指定&#x200B;**上一步**，並視需要新增&#x200B;**註解**。
1. 使用&#x200B;**確定**&#x200B;完成步驟（或使用&#x200B;**取消**&#x200B;中止動作）。

#### 對參與者步驟執行後退 — 頁面編輯器 {#performing-step-back-on-a-participant-step-page-editor}

請使用下列步驟來後退：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從頂端的狀態列選取&#x200B;**後退**。
1. 指定&#x200B;**上一步**，並視需要新增&#x200B;**註解**。
1. 使用&#x200B;**確定**&#x200B;完成步驟（或使用&#x200B;**取消**&#x200B;中止動作）。

#### 對參與者步驟執行後退 — 時間表 {#performing-step-back-on-a-participant-step-timeline}

您也可以使用時間軸來回滾（回退）至上一步：

1. 選取必要頁面，然後開啟&#x200B;**時間表** （或開啟&#x200B;**時間表**&#x200B;並選取頁面）。
1. 按一下警報橫幅以顯示可用動作。 選取&#x200B;**回覆**：

   ![screen-shot_2019-03-05at121131](assets/screen-shot_2019-03-05at121131.png)

1. 指定工作流程應傳回到的步驟：

   ![screen-shot_2019-03-05at121158](assets/screen-shot_2019-03-05at121158.png)

1. 選取&#x200B;**回覆**&#x200B;以確認動作。

### 開啟工作流程專案以檢視詳細資訊（並執行動作） {#opening-a-workflow-item-to-view-details-and-take-actions}

檢視工作流程工作專案的詳細資訊，並採取適當的動作。

工作流程詳細資訊會顯示在標籤中，而工具列中有適當的動作：

* **工作專案**&#x200B;索引標籤：

  ![wf-72](assets/wf-72.png)

* **工作流程資訊**&#x200B;標籤：

  ![wf-73](assets/wf-73.png)

  如果已經為模型設定了[工作流程階段](/help/sites-developing/workflows.md#workflow-stages)，您可以根據下列專案檢視進度：

  ![wf-107](assets/wf-107.png)

* **評論**&#x200B;標籤：

  ![wf-75](assets/wf-75.png)

您可以透過以下其中一種方式來開啟工作專案詳細資料：

* [收件匣](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)

#### 開啟工作流程詳細資料 — 收件匣 {#opening-workflow-details-inbox}

若要開啟工作流程專案並檢視詳細資訊，請執行下列動作：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（按一下縮圖）。
1. 選取&#x200B;**開啟**&#x200B;以開啟資訊標籤。

1. 如有必要，請選取適當的動作，提供任何詳細資料，並透過&#x200B;**確定** （或&#x200B;**取消**）確認。
1. 使用&#x200B;**儲存**&#x200B;或&#x200B;**取消**&#x200B;結束。

#### 開啟工作流程詳細資料 — 頁面編輯器 {#opening-workflow-details-page-editor}

若要開啟工作流程專案並檢視詳細資訊，請執行下列動作：

1. 開啟[頁面進行編輯](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 從狀態列選取&#x200B;**檢視詳細資料**&#x200B;以開啟資訊標籤。

1. 如有必要，請選取適當的動作，提供任何詳細資料，並透過&#x200B;**確定** （或&#x200B;**取消**）確認。
1. 使用&#x200B;**儲存**&#x200B;或&#x200B;**取消**&#x200B;結束。

### 檢視工作流程裝載（多個資源） {#viewing-the-workflow-payload-multiple-resources}

您可以檢視與工作流程例項相關聯的裝載詳細資料。 一開始會顯示封裝中的資源，然後您可以向下展開以顯示個別頁面。

若要檢視工作流程例項的裝載和資源：

1. 開啟&#x200B;**[AEM收件匣](/help/sites-authoring/inbox.md)**。
1. 選取您要對其執行動作的工作流程專案（按一下縮圖）。
1. 從工具列選取&#x200B;**檢視裝載**&#x200B;以開啟對話方塊。

   由於Workflow封裝只是存放庫內路徑的指標集合，因此您可以在此處新增/移除/修改專案，以調整Workflow封裝所參照的專案。 使用&#x200B;**資源定義**&#x200B;元件來新增專案。

   ![wf-78](assets/wf-78.png)

1. 這些連結可用來開啟個別頁面。
