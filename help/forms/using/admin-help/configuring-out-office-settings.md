---
title: 配置外出設定
seo-title: Configuring Out of Office Settings
description: 「外出」功能可讓您指定使用者何時離開辦公室，且無法完成AEM表單指派的工作。
seo-description: The Out of Office feature enables you to specify when a user will be out of the office and unable to complete tasks assigned by AEM forms.
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 配置外出設定 {#configuring-out-of-office-settings}

「外出」功能可讓使用者或管理員指定使用者何時離開辦公室，且無法完成AEM表單指派的工作。 當用戶設定為「外出」時，其任務將分配給一個或多個指定用戶。 使用者可以在工作區中變更其「外出」設定，或管理員可以在表單工作流程中代表使用者變更設定。

建立程式時，Workbench使用者可指定是否因「不在辦公室」設定而可將任務重新導向。

## 查看用戶的外出資訊 {#view-a-user-s-out-of-office-information}

1. 在管理控制台中，按一下「服務>表單工作流程>外出」。
1. 在「外出」頁面頂端附近的方塊中，您可以執行下列其中一項操作：

   **按名稱搜索**

   選擇「按名稱搜索」選項。 鍵入用戶名的全部或部分，然後按一下「查找」。 如果將欄位留空，Forms工作流程會傳回所有使用者的清單

   **依日期範圍搜尋**

   選取「依日期範圍搜尋」選項。 指定開始日期和結束日期，以及所需的時間戳記，以縮小搜尋結果。 按一下「查找」。

1. 按一下用戶名，在用戶清單下面顯示用戶的「Out of Office」資訊。

## 更改用戶的外出狀態 {#change-a-user-s-out-of-office-status}

1. 查找用戶，如 [查看用戶的外出資訊](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 按一下您要變更的使用者名稱。
1. 從 *使用者名稱* 當前清單中，選擇「在辦公室中」或「不在辦公室中」。
1. 按一下「儲存」。

## 為使用者新增「不在辦公室」日期範圍 {#add-an-out-of-office-date-range-for-a-user}

1. 查找用戶，如 [查看用戶的外出資訊](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 按一下您要變更的使用者名稱。
1. 按一下「新增日期範圍」 。
1. 輸入開始時間和結束時間。 您可以按一下「日曆」圖示來選取日期。 如果您未指定結束時間，系統會無限期將使用者設為不在辦公室。
1. 按一下「儲存」。

## 為外出任務分配用戶 {#assign-a-user-for-out-of-office-tasks}

當用戶不在辦公室時，您可以分配一個或多個用戶，以為用戶執行任何新任務。 您可以設定下列設定：

* 將所有新任務分配給指定的預設用戶。
* 不重新分配任何任務。 新任務仍分配給不在辦公室的用戶。
* 分配預設用戶，該用戶將接收用戶的大部分任務，但指定某些進程中的任務被重新分配給其他用戶，或者繼續分配給不在辦公室的用戶。
* 不要指派預設使用者，而是將特定程式中的特定任務指派給特定使用者。

   1. 查找用戶，如 [查看用戶的外出資訊](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. 按一下您要變更的使用者名稱。
   1. 在「Default User For Out Office Tasks」（預設用戶外出任務）清單中，從清單中選擇一個用戶。 如果您不想指定預設用戶來接收重新分配的項目，請選擇「不分配」。

      如果清單中未出現相應的用戶名，請按一下「查找用戶」，然後使用「查找用戶」對話框搜索該用戶。 從清單中選擇適當的用戶，然後按一下「選擇用戶」。 您也可以按一下「查找用戶」對話框中的「查看用戶的計畫」，查看所選用戶的不在辦公時間表。

   1. 如果有任何進程不應發送給預設用戶，請按一下「添加異常」，然後選擇該進程並從清單中選擇其他用戶。 您也可以選擇「不分配」，將任務繼續分配給不在辦公室的用戶。
   1. 按一下「儲存」。
