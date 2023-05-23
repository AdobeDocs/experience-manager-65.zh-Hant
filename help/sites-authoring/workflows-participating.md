---
title: 工作流參與
description: 工作流通常包括要求人員在頁面或資產上執行活動的步驟。
uuid: 15d56bcc-1e84-4cc0-8b71-7fb906cd7ff7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: f170613c-329e-446b-9ac3-350615f1bfb6
docset: aem65
exl-id: e47270e8-bace-4d0f-a088-7269b6356315
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 1%

---

# 參與工作流程{#participating-in-workflows}

工作流通常包括要求人員在頁面或資產上執行活動的步驟。 工作流選擇一個用戶或組以執行該活動，並為該人員或組分配一個工作項目。 用戶收到通知，然後可以採取相應的操作：

* [查看通知](#notifications-of-available-workflow-actions)
* [完成參與者步驟](#completing-a-participant-step)
* [委派參與者步驟](#delegating-a-participant-step)
* [對參與者步驟執行後退步驟](#performing-step-back-on-a-participant-step)
* [開啟工作流項以查看詳細資訊（並採取操作）](#opening-a-workflow-item-to-view-details-and-take-actions)
* [查看工作流負載（多個資源）](#viewing-the-workflow-payload-multiple-resources)

## 可用工作流操作的通知 {#notifications-of-available-workflow-actions}

當您被指派工作項目時(例如「核准內 **容**」)，會出現各種警報和/或通知：

* 您 [通知](/help/sites-authoring/inbox.md) 指示符（工具欄）將遞增：

   ![](do-not-localize/wf-57.png)

* 該項目將列在您的通知中 [收件箱](/help/sites-authoring/inbox.md):

   ![wf-58](assets/wf-58.png)

* 使用頁面編輯器時，狀態欄將顯示：

   * 應用到頁面的工作流的名稱；例如請求激活。
   * 當前用戶在工作流的當前步驟中可執行的操作；例如，「完成」(Complete)、「委託」(Delegate)、「查看詳細資訊」(View details)。
   * 該頁面所受的工作流數。 您可以：

      * 使用左箭頭/右箭頭瀏覽各種工作流的狀態資訊。
      * 按一下/點按實際數字開啟所有適用工作流的下拉清單，然後選擇要在狀態欄中顯示的工作流。

   ![wf-59](assets/wf-59.png)

   >[!NOTE]
   >
   >狀態欄僅對具有工作流權限的用戶可見；例如， `workflow-users` 組。
   >
   >
   >當當前用戶直接參與工作流的當前步驟時，將顯示操作。

* 當 **時間軸** 為資源開啟，將顯示工作流步驟。 按一下/點擊警報標語時，還會顯示可用操作：

   ![螢幕抓拍_2019-03-05at120453](assets/screen-shot_2019-03-05at120453.png)

### 完成參與者步驟 {#completing-a-participant-step}

您可以完成項目，以允許工作流進入下一步。

在此操作中，您可以指明：

* **下一步**:下一步，可以從提供的清單中進行選擇
* **注釋**:如果需要

您可以從以下任一步驟完成參與者步驟：

* [收件箱](#completing-a-participant-step-inbox)
* [頁面編輯器](#completing-a-participant-step-page-editor)
* [時間軸](#completing-a-participant-step-timeline)
* 何時 [開啟工作流項以查看詳細資訊](#opening-a-workflow-item-to-view-details-and-take-actions)。

#### 完成參與者步驟 — 收件箱 {#completing-a-participant-step-inbox}

請按下列步驟完成工作項：

1. 開啟 **[收件箱AEM](/help/sites-authoring/inbox.md)**。
1. 選擇要對其執行操作的工作流項（點擊/按一下縮略圖）。
1. 選擇 **完成** 的子菜單。
1. 的 **完成工作項** 對話框。 選擇 **下一步** 從下拉選擇器添加 **注釋** 的子菜單。
1. 使用 **確定** 完成步驟(或 **取消** 中止操作)。

#### 完成參與者步驟 — 頁面編輯器 {#completing-a-participant-step-page-editor}

請按下列步驟完成工作項：

1. 開啟 [編輯頁面](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 選擇 **完成** 的下界。
1. 的 **完成工作項** 對話框。 選擇 **下一步** 從下拉選擇器添加 **注釋** 的子菜單。
1. 使用 **確定** 完成步驟(或 **取消** 中止操作)。

#### 完成參與者步驟 — 時間表 {#completing-a-participant-step-timeline}

您還可以使用時間線完成並推進步驟：

1. 選擇所需頁面並開啟 **時間軸** （開啟） **時間軸** 並選擇頁面):

   ![螢幕抓拍_2019-03-05at120744](assets/screen-shot_2019-03-05at120744.png)

1. 按一下/點擊警報標語以顯示可用操作。 選擇 **先進**:

   ![screen-shot_2019-03-05at120453-1](assets/screen-shot_2019-03-05at120453-1.png)

1. 根據工作流，您可以選擇下一步：

   ![螢幕抓拍_2019-03-05at120905](assets/screen-shot_2019-03-05at120905.png)

1. 選擇 **先進** 確認操作。

### 委派參與者步驟 {#delegating-a-participant-step}

如果已為您分配了步驟，但由於任何原因您無法採取操作，則您可以將該步驟委派給其他用戶或組。

可用於委派的用戶取決於為誰分配了工作項：

* 如果工作項已分配給組，則組成員可用。
* 如果工作項已分配給組，然後委託給用戶，則組成員和組可用。
* 如果工作項已分配給單個用戶，則無法委派該工作項。

在此操作中，您可以指明：

* **用戶**:要委託給的用戶；可以從提供的清單中進行選擇
* **注釋**:如果需要

您可以從以下任一位置委託參與者步驟：

* [收件箱](#delegating-a-participant-step-inbox)
* [頁面編輯器](#delegating-a-participant-step-page-editor)
* [時間軸](#delegating-a-participant-step-timeline)
* 何時 [開啟工作流項以查看詳細資訊](#opening-a-workflow-item-to-view-details-and-take-actions)。

#### 委派參與者步驟 — 收件箱 {#delegating-a-participant-step-inbox}

請按下列步驟委派工作項：

1. 開啟 **[收件箱AEM](/help/sites-authoring/inbox.md)**。
1. 選擇要對其執行操作的工作流項（點擊/按一下縮略圖）。
1. 選擇 **委託** 的子菜單。
1. 對話框將開啟。 指定 **用戶** 從下拉選擇器（這也可以是組）中添加 **注釋** 的子菜單。
1. 使用 **確定** 完成步驟(或 **取消** 中止操作)。

#### 委派參與者步驟 — 頁面編輯器 {#delegating-a-participant-step-page-editor}

請按下列步驟委派工作項：

1. 開啟 [編輯頁面](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 選擇 **委託** 的下界。
1. 對話框將開啟。 指定 **用戶** 從下拉選擇器（這也可以是組）中添加 **注釋** 的子菜單。
1. 使用 **確定** 完成步驟(或 **取消** 中止操作)。

#### 委託參與者步驟 — 時間表 {#delegating-a-participant-step-timeline}

您還可以使用時間線來委派和/或分配步驟：

1. 選擇所需頁面並開啟 **時間軸** （開啟） **時間軸** 並選擇頁面)。
1. 按一下/點擊警報標語以顯示可用操作。 選擇 **更改受分配人**:

   ![screen-shot_2019-03-05at120453-2](assets/screen-shot_2019-03-05at120453-2.png)

1. 指定新的受分配人：

   ![螢幕抓拍_2019-03-05at121025](assets/screen-shot_2019-03-05at121025.png)

1. 選擇 **分配** 確認操作。

### 在參與者步驟上執行後退步驟 {#performing-step-back-on-a-participant-step}

如果您發現需要重複某個步驟或一系列步驟，則可以退一步。 這允許您選擇在工作流中較早發生的步驟進行重新處理。 工作流將返回到您指定的步驟，然後從那裡繼續。

在此操作中，您可以指明：

* **上一步**:返回的步驟；可以從提供的清單中進行選擇
* **注釋**:如果需要

您可以從以下任一步驟對參與者步驟執行後退：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)
* [時間軸](#performing-step-back-on-a-participant-step-timeline)
* 何時 [開啟工作流項以查看詳細資訊](#opening-a-workflow-item-to-view-details-and-take-actions)。

#### 在參與者步驟上執行後退步驟 — 收件箱 {#performing-step-back-on-a-participant-step-inbox}

請按下列步驟後退：

1. 開啟 **[收件箱AEM](/help/sites-authoring/inbox.md)**。
1. 選擇要對其執行操作的工作流項（點擊/按一下縮略圖）。
1. 選擇 **後退** 的子菜單。

1. 指定 **上一步** 並添加 **注釋** 的子菜單。
1. 使用 **確定** 完成步驟(或 **取消** 中止操作)。

#### 在參與者步驟 — 頁面編輯器上執行後退步驟 {#performing-step-back-on-a-participant-step-page-editor}

請按下列步驟後退：

1. 開啟 [編輯頁面](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 選擇 **後退** 的下界。
1. 指定 **上一步** 並添加 **注釋** 的子菜單。
1. 使用 **確定** 完成步驟(或 **取消** 中止操作)。

#### 對參與者步驟執行後退步驟 — 時間軸 {#performing-step-back-on-a-participant-step-timeline}

還可以使用時間軸將（步驟）回滾到上一步：

1. 選擇所需頁面並開啟 **時間軸** （開啟） **時間軸** 並選擇頁面)。
1. 按一下/點擊警報標語以顯示可用操作。 選擇 **回滾**:

   ![screen-shot_2019-03-05at121131](assets/screen-shot_2019-03-05at121131.png)

1. 指定工作流應返回到的步驟：

   ![screen-shot_2019-03-05at121158](assets/screen-shot_2019-03-05at121158.png)

1. 選擇 **回滾** 確認操作。

### 開啟工作流項以查看詳細資訊（並採取操作） {#opening-a-workflow-item-to-view-details-and-take-actions}

查看工作流工作項的詳細資訊並採取相應的操作。

工作流詳細資訊顯示在頁籤中，工具欄中提供了相應的操作：

* **工件** 頁籤：

   ![wf-72](assets/wf-72.png)

* **工作流資訊** 頁籤：

   ![wf-73](assets/wf-73.png)

   如果 [工作流階段](/help/sites-developing/workflows.md#workflow-stages) 已為模型配置，您可以根據以下內容查看進度：

   ![wf-107](assets/wf-107.png)

* **注釋** 頁籤：

   ![wf-75](assets/wf-75.png)

您可以從以下任一位置開啟工作項詳細資訊：

* [收件箱](#performing-step-back-on-a-participant-step-inbox)
* [頁面編輯器](#performing-step-back-on-a-participant-step-page-editor)

#### 開啟工作流詳細資訊 — 收件箱 {#opening-workflow-details-inbox}

要開啟工作流項並查看詳細資訊，請執行以下操作：

1. 開啟 **[收件箱AEM](/help/sites-authoring/inbox.md)**。
1. 選擇要對其執行操作的工作流項（點擊/按一下縮略圖）。
1. 選擇 **開啟** 的子菜單。

1. 如果需要，請選擇相應的操作，提供任何詳細資訊並與 **確定** 或 **取消**)。
1. 使用 **保存** 或 **取消** 按鈕。

#### 開啟工作流詳細資訊 — 頁面編輯器 {#opening-workflow-details-page-editor}

要開啟工作流項並查看詳細資訊，請執行以下操作：

1. 開啟 [編輯頁面](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing)。
1. 選擇 **查看詳細資訊** 的子菜單。

1. 如果需要，請選擇相應的操作，提供任何詳細資訊並與 **確定** 或 **取消**)。
1. 使用 **保存** 或 **取消** 按鈕。

### 查看工作流負載（多個資源） {#viewing-the-workflow-payload-multiple-resources}

您可以查看與工作流實例關聯的負載的詳細資訊。 最初顯示包中的資源，然後您可以細化以顯示各個頁面。

要查看工作流實例的負載和資源，請執行以下操作：

1. 開啟 **[收件箱AEM](/help/sites-authoring/inbox.md)**。
1. 選擇要對其執行操作的工作流項（點擊/按一下縮略圖）。
1. 選擇 **查看負載** 對話框。

   由於工作流包只是指向儲存庫中路徑的指針的集合，因此您可以在此處添加/刪除/修改條目，以調整工作流包引用的內容。 使用 **資源定義** 元件以添加新條目。

   ![wf-78](assets/wf-78.png)

1. 這些連結可用於開啟各個頁面。
