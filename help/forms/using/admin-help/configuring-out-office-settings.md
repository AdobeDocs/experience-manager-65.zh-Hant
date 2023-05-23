---
title: 配置外出設定
seo-title: Configuring Out of Office Settings
description: 「外出」功能允許您指定用戶何時離開辦公室，以及無法完成表單分配的任AEM務。
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

「外出」功能使用戶或管理員能夠指定用戶何時離開辦公室，以及無法完成表單分配的AEM任務。 當用戶設定為「外出」時，其任務將分配給一個或多個指定用戶。 用戶可以在Workspace中更改其「外出」設定，或者管理員可以在表單工作流中代表用戶更改設定。

建立流程時，Workbench用戶可以指定是否可以由於「外出」設定而重定向任務。

## 查看用戶的Out Office資訊 {#view-a-user-s-out-of-office-information}

1. 在管理控制台中，按一下「服務」>「表單工作流」>「外出」。
1. 在「外出」頁面頂部附近的框中，可以執行以下操作之一：

   **按名稱搜索**

   選擇「按名稱搜索」選項。 鍵入全部或部分用戶名，然後按一下「查找」。 如果將欄位留空，Forms工作流將返回所有用戶的清單

   **按日期範圍搜索**

   選擇「按日期範圍搜索」選項。 指定起始日期和終止日期以及所需的時間戳，以縮小搜索結果。 按一下「查找」。

1. 按一下用戶名，在用戶清單下顯示用戶的「外出」資訊。

## 更改用戶的外出狀態 {#change-a-user-s-out-of-office-status}

1. 查找用戶，如中所述 [查看用戶的Out Office資訊](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)。
1. 按一下要更改的用戶的名稱。
1. 從 *用戶名* 為當前清單，選擇「在Office中」或「在Office之外」。
1. 按一下「儲存」。

## 為用戶添加「外出」日期範圍 {#add-an-out-of-office-date-range-for-a-user}

1. 查找用戶，如中所述 [查看用戶的Out Office資訊](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)。
1. 按一下要更改的用戶的名稱。
1. 按一下添加日期範圍。
1. 輸入開始時間和結束時間。 您可以按一下「日曆」表徵圖選擇日期。 如果不指定結束時間，則用戶將被無限期設定為離職。
1. 按一下「儲存」。

## 為外出任務分配用戶 {#assign-a-user-for-out-of-office-tasks}

當用戶不在辦公室時，您可以分配一個或多個用戶來為用戶執行任何新任務。 可以設定以下配置：

* 將所有新任務分配給指定的預設用戶。
* 不重新分配任何任務。 新任務仍分配給不在辦公室的用戶。
* 分配將接收用戶大部分任務的預設用戶，但指定將某些進程中的任務重新分配給其他用戶或保留分配給不在辦公室的用戶。
* 不分配預設用戶，而是將特定進程中的某些任務分配給特定用戶。

   1. 查找用戶，如中所述 [查看用戶的Out Office資訊](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)。
   1. 按一下要更改的用戶的名稱。
   1. 在「Default User For Out Office Tasks」清單中，從清單中選擇用戶。 如果不想指定預設用戶來接收重新分配的項目，請選擇「不分配」。

      如果清單中未顯示相應的用戶名，請按一下「查找用戶」，然後使用「查找用戶」對話框搜索用戶。 從清單中選擇相應的用戶，然後按一下「選擇用戶」。 也可以按一下「查找用戶」對話框中的「查看用戶的調度」，以查看所選用戶的外出調度。

   1. 如果有任何進程不應發送給預設用戶，請按一下「添加例外」，然後選擇該進程並從清單中選擇其他用戶。 您也可以選擇「不分配」，將任務保留分配給不在辦公室的用戶。
   1. 按一下「儲存」。
