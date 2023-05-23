---
title: 參與工作流程
description: 工作流通常包括要求人員在頁面或資產上執行活動的步驟。 工作流選擇一個用戶或組以執行該活動，並為該人員或組分配一個工作項目。
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 4%

---

# 參與工作流程{#participating-in-workflows}

工作流通常包括要求人員在頁面或資產上執行活動的步驟。 工作流選擇一個用戶或組以執行該活動，並為該人員或組分配一個工作項目。

## 處理工作項 {#processing-your-work-items}

您可以執行以下操作來處理工作項：

* **完成**

   您可以完成項目，以允許工作流進入下一步。

* **委派**

   如果已為您分配了步驟，但由於任何原因您無法採取操作，則您可以將該步驟委派給其他用戶或組。

   可用於委派的用戶取決於為誰分配了工作項：

   * 如果工作項已分配給組，則組成員可用。
   * 如果工作項已分配給組，然後委託給用戶，則組成員和組可用。
   * 如果工作項已分配給單個用戶，則無法委派該工作項。

* **後退**

   如果您發現需要重複某個步驟或一系列步驟，則可以退一步。 這允許您選擇在工作流中較早發生的步驟進行重新處理。 工作流將返回到您指定的步驟，然後從那裡繼續。

## 參與工作流 {#participating-in-a-workflow}

### 已分配工作流操作的通知 {#notifications-of-assigned-workflow-actions}

當您被指派工作項目時(例如「核准內 **容**」)，會出現各種警報和/或通知：

* 的 **狀態** 「網站」控制台的列指示頁面在工作流中的時間：

   ![工作流狀態1](assets/workflowstatus-1.png)

* 當您或您所屬的組被分配作為工作流的一部分的工作項目時，該工作項目將出現在您的工作流收件箱AEM中。

   ![工作流收件箱](assets/workflowinbox.png)

### 完成參與者步驟 {#completing-a-participant-step}

在您採取指示的操作後，您可以完成工作項，從而允許工作流繼續。 請按下列步驟完成工作項。

1. 選擇工作流步驟，然後按一下 **完成** 按鈕。
1. 在生成的對話框中，選擇 **下一步**;就是下一步要執行的步驟。 下拉清單顯示所有適當的目標。 A **注釋** 的子菜單。

   ![工作流完成](assets/workflowcomplete.png)

   列出的步驟數取決於工作流模型的設計。

1. 按一下 **確定** 確認操作。

### 委派參與者步驟 {#delegating-a-participant-step}

請按下列步驟委派工作項。

1. 按一下 **委託** 按鈕。
1. 在對話框中，使用下拉清單選擇 **用戶** 將工作項委託給。 也可以添加 **注釋**。

   ![工作流委託](assets/workflowdelegate.png)

1. 按一下 **確定** 確認操作。

### 在參與者步驟上執行後退步驟 {#performing-step-back-on-a-participant-step}

請按下列步驟後退。

1. 按一下頂部導航欄中的「後退」按鈕。
1. 在生成的對話框中，選擇「上一步」(Previous Step);即，下一步執行的步驟，即使這是在工作流早期執行的步驟。 下拉清單顯示所有適當的目標。

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. 按一下「確定」(OK)確認操作。
