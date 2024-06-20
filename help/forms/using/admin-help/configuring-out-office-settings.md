---
title: 正在設定[外出]設定
description: 「不在辦公室」功能可讓您指定使用者何時不在辦公室，且無法完成AEM表單所指派的工作。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 正在設定[外出]設定 {#configuring-out-of-office-settings}

「不在辦公室」功能可讓使用者或管理員指定使用者何時不在辦公室，且無法完成AEM表單所指派的工作。 當使用者設定為「不在辦公室」時，其任務會指派給一個或多個指定使用者。 使用者可以在Workspace中變更其「外出」設定，或管理員可以代表使用者在Forms Workflow中變更設定。

建立處理作業時，Workbench使用者可以指定是否可因「外出」設定而重新導向作業。

## 檢視使用者的休假資訊 {#view-a-user-s-out-of-office-information}

1. 在管理控制檯中，按一下「服務>表單工作流程>外出」。
1. 在「郵件答錄機」頁面頂端附近的方塊中，您可以執行下列任一項作業：

   **依名稱搜尋**

   選取「依名稱搜尋」選項。 輸入全部或部分使用者名稱，然後按一下「尋找」。 如果將此欄位留空，Forms工作流程會傳回所有使用者的清單。

   **依日期範圍搜尋**

   選取依日期範圍搜尋選項。 指定開始和結束日期以及所需的時間戳記，以縮小搜尋結果的範圍。 按一下「尋找」。

1. 按一下使用者名稱，即可在使用者清單下方顯示使用者的「外出」資訊。

## 變更使用者的休假狀態 {#change-a-user-s-out-of-office-status}

1. 尋找使用者，如所述 [檢視使用者的休假資訊](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 按一下您要變更的使用者名稱。
1. 從 *使用者名稱* 目前為清單，請選取[在辦公室中]或[不在辦公室]。
1. 按一下「儲存」。

## 新增使用者的「不在辦公室」日期範圍 {#add-an-out-of-office-date-range-for-a-user}

1. 尋找使用者，如所述 [檢視使用者的休假資訊](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 按一下您要變更的使用者名稱。
1. 按一下「新增日期範圍」。
1. 輸入開始時間和結束時間。 您可以按一下「行事曆」圖示以選取日期。 如果您未指定結束時間，使用者將會無限期設為不在辦公室。
1. 按一下「儲存」。

## 為休假任務指派使用者 {#assign-a-user-for-out-of-office-tasks}

當使用者不在辦公室時，您可以指派一或多個使用者為該使用者執行任何新工作。 您可以設定下列設定：

* 將所有新任務指派給指定的預設使用者。
* 請勿重新指派任何工作。 新任務仍會指派給不在辦公室的使用者。
* 指派將接收大部分使用者任務的預設使用者，但指定將來自特定流程的任務重新指派給其他使用者，或繼續指派給不在辦公室的使用者。
* 不要指派預設使用者，而是將特定程式中的特定工作指派給特定使用者。

   1. 尋找使用者，如所述 [檢視使用者的休假資訊](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. 按一下您要變更的使用者名稱。
   1. 在「外出工作的預設使用者」清單中，從清單中選取使用者。 如果您不想指定預設使用者來接收重新指派的專案，請選取「不要指派」。

      如果清單中未出現適當的使用者名稱，請按一下「尋找使用者」，然後使用「尋找使用者」對話方塊來搜尋使用者。 從清單中選取適當的使用者，然後按一下「選取使用者」。 您也可以按一下「尋找使用者」對話方塊中的「檢視使用者排程」，以檢視所選使用者的休假排程。

   1. 如果有任何不應傳送給預設使用者的程式，請按一下「新增例外」，然後選取該程式，再從清單中選取其他使用者。 您也可以選取「不要指派」 ，讓工作保持指派給不在辦公室的使用者。
   1. 按一下「儲存」。
