---
title: 參與工作流程
seo-title: Participating in Workflows
description: 工作流程通常包括要求人員在頁面或資產上執行活動的步驟。 工作流選擇要執行活動的用戶或組，並將工作項指派給該人員或組。
seo-description: Workflows typically include steps that require a person to perform an activity on a page or asset. The workflow selects a user or group to perform the activity and assigns a work item to that person or group.
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 4%

---

# 參與工作流程{#participating-in-workflows}

工作流程通常包括要求人員在頁面或資產上執行活動的步驟。 工作流選擇要執行活動的用戶或組，並將工作項指派給該人員或組。

## 處理您的工作項 {#processing-your-work-items}

您可以執行以下操作來處理工作項：

* **完成**

   您可以完成項目，讓工作流程繼續進行下一個步驟。

* **委派**

   如果已指派步驟給您，但由於任何原因您無法採取動作，您可以將步驟委派給其他使用者或群組。

   可用於委派的用戶取決於為誰分配了工作項：

   * 如果工作項已分配給組，則組成員可用。
   * 如果工作項目被指派給某個組，然後被委派給某個用戶，則可使用組成員和組。
   * 如果工作項已分配給單個用戶，則無法委派工作項。

* **後退**

   如果您發現需要重複某個步驟或一系列步驟，您可以退後一步。 這可讓您選取先前在工作流程中發生的步驟，以進行重新處理。 工作流程會回到您指定的步驟，然後從那裡繼續。

## 參與工作流程 {#participating-in-a-workflow}

### 已分配工作流操作的通知 {#notifications-of-assigned-workflow-actions}

當您被指派工作項目時(例如「核准內 **容**」)，會出現各種警報和/或通知：

* 此 **狀態** 「網站控制台」的欄會指出頁面何時處於工作流程中：

   ![workflowstatus-1](assets/workflowstatus-1.png)

* 當您或您所屬的組被分配工作項目作為工作流的一部分時，該工作項目將出現在您的AEM工作流收件箱中。

   ![工作流程收件匣](assets/workflowinbox.png)

### 完成參與者步驟 {#completing-a-participant-step}

在您採取此動作後，表示您可以完成工作項目，從而允許工作流程繼續。 請使用以下過程完成工作項。

1. 選取工作流程步驟，然後按一下 **完成** 按鈕。
1. 在產生的對話方塊中，選取 **下一步**;即，下一個執行步驟。 下拉式清單會顯示所有適當的目的地。 A **註解** 也可以輸入。

   ![工作流程完成](assets/workflowcomplete.png)

   列出的步驟數取決於工作流模型的設計。

1. 按一下 **確定** 以確認動作。

### 委派參與者步驟 {#delegating-a-participant-step}

使用以下過程來委派工作項。

1. 按一下 **委派** 按鈕。
1. 在對話方塊中，使用下拉式清單來選取 **使用者** 將工作項委派給。 您也可以新增 **註解**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. 按一下 **確定** 以確認動作。

### 在參與者步驟上執行退步 {#performing-step-back-on-a-participant-step}

請依照下列程式退後。

1. 按一下頂端導覽列中的「上一步」按鈕。
1. 在產生的對話方塊中，選取「上一步」；也就是說，後續執行的步驟，即使這是在工作流程較早時發生的步驟。 下拉式清單會顯示所有適當的目的地。

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. 按一下「確定」以確認動作。
