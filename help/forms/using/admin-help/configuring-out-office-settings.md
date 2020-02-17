---
title: 設定不在辦公室的設定
seo-title: 設定不在辦公室的設定
description: 「不在辦公室」功能可讓您指定使用者何時離開辦公室，且無法完成AEM表格指派的工作。
seo-description: 「不在辦公室」功能可讓您指定使用者何時離開辦公室，且無法完成AEM表格指派的工作。
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定不在辦公室的設定 {#configuring-out-of-office-settings}

使用者或管理員可使用「不在辦公室」功能來指定使用者何時離開辦公室，以及無法完成AEM表格指派的工作。 當用戶設定為「不在辦公室」時，其任務將分配給一個或多個指定用戶。 使用者可以在工作區中變更其「外出辦公室」設定，或管理員可以代表使用者在表單工作流程中變更設定。

建立流程時，Workbench使用者可以指定是否因為「不在辦公室」設定而重新導向工作。

## 檢視使用者的「外出」資訊 {#view-a-user-s-out-of-office-information}

1. 在管理主控台中，按一下「服務>表單工作流程> Out office」。
1. 在「Out of Office（不在辦公室）」頁面頂部附近的框中，您可以執行下列操作之一：

   **依名稱搜尋**

   選擇「依名稱搜尋」選項。 鍵入全部或部分用戶名，然後按一下「查找」(Find)。 如果將欄位留空，Forms工作流將返回所有用戶的清單

   **依日期範圍搜尋**

   選擇「依日期範圍搜尋」選項。 指定起始和終止日期以及所需的時間戳記，以縮小搜尋結果。 按一下「尋找」。

1. 按一下使用者名稱，在使用者清單下方顯示使用者的「外出」資訊。

## 變更使用者的離職狀態 {#change-a-user-s-out-of-office-status}

1. 如「檢視使用者的 [Out office」資訊中所述，尋找使用者](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)。
1. 按一下您要變更的使用者名稱。
1. 從「 *用戶名* 」當前清單中，選擇「在辦公室中」或「在辦公室外」。
1. 按一下「儲存」。

## 新增使用者的「不在辦公室」日期範圍 {#add-an-out-of-office-date-range-for-a-user}

1. 如「檢視使用者的 [Out office」資訊中所述，尋找使用者](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)。
1. 按一下您要變更的使用者名稱。
1. 按一下「新增日期範圍」。
1. 輸入開始時間和結束時間。 您可以按一下「日曆」圖示來選取日期。 如果您未指定結束時間，使用者將會無限期地設為不在辦公室。
1. 按一下「儲存」。

## 為Out office任務分配用戶 {#assign-a-user-for-out-of-office-tasks}

當使用者不在辦公室時，您可以指派一或多位使用者為使用者執行任何新工作。 您可以設定下列組態：

* 將所有新任務分配給指定的預設用戶。
* 不要重新指派任何工作。 新任務仍分配給不在辦公室的用戶。
* 指派將接收大部分使用者工作的預設使用者，但指定某些程式的工作會重新指派給其他使用者，或仍指派給不在辦公室的使用者。
* 不要指派預設使用者，而是將特定程式的特定工作指派給特定使用者。

   1. 如「檢視使用者的 [Out office」資訊中所述，尋找使用者](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)。
   1. 按一下您要變更的使用者名稱。
   1. 在「Default User For Out office Tasks」（預設用戶退出辦公室任務）清單中，從清單中選擇用戶。 如果您不想指定要接收重新指派項目的預設使用者，請選取「不指派」。

      如果清單中未顯示相應的用戶名，請按一下「查找用戶」，然後使用「查找用戶」對話框搜索用戶。 從清單中選擇適當的用戶，然後按一下「選擇用戶」。 您也可以按一下「尋找使用者」對話方塊中的「檢視使用者排程」，以查看選取的使用者不在辦公室的排程。

   1. 如果有任何進程不應發送給預設用戶，請按一下「添加例外」，然後選擇該進程並從清單中選擇其他用戶。 您也可以選擇「不指派」，讓離開辦公室的使用者仍能指派工作。
   1. 按一下「儲存」。

