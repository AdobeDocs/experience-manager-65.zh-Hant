---
title: 配置共用隊列
seo-title: Configuring Shared Queues
description: 共用隊列允許您有效配置和管理用戶隊列。 瞭解如何配置共用隊列。
seo-description: Shared Queues allow you to configure and manage user queues effectively. Learn how to configure shared queues.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# 配置共用隊列{#configuring-shared-queues}

共用隊列允許您有效配置和管理用戶隊列。 用戶隊列只是分配給用戶的所有任務，請參閱 [要執行清單](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) 的子菜單。 您可以根據組織需要分配、取消分配和重新分配用戶隊列。 可以通過兩種方式管理共用隊列：

**管理對用戶的訪問**

您可以使用此選項管理對選定用戶隊列的訪問。

**管理用戶訪問**

您可以使用此選項管理分配給選定用戶的共用隊列。

## 管理對選定用戶隊列的訪問 {#managing-access-to-a-selected-user-queue}

管理對用戶的訪問功能允許您管理對選定用戶隊列的訪問。 您可以向組織中的其他用戶授予或撤消對選定用戶隊列的訪問權限。 比如，卡拉·鮑曼不在辦公室。 使用「管理對用戶的訪問」功能，她的隊列可以與Akira Tanaka和John Jacobs共用，以完成。 之後，當卡拉·鮑曼回到辦公室時，你可以取消她在田中明和約翰·雅各布斯的排隊權。

共用後，用戶可以使用Workspace完成這些任務，並訪問隊列。

>[!NOTE]
>
>不建議使用Flex工AEM作空間。

### 配置對選定用戶隊列的訪問 {#configuring-access-to-a-selected-user-queue}

1. 使用管理員帳戶登錄到管理控制台。
1. 選擇 **服務** > **表單工作流** > **共用隊列**。

1. 在「管理對用戶的訪問」頁籤上，查找並選擇要共用其隊列的用戶。 在任何時候，右下窗格都顯示有權訪問選定用戶隊列的用戶清單。
1. 在左下窗格中，查找並選擇用戶。 按一下「共用」。
1. 按一下「保存」完成。

### 撤消對所選用戶隊列的訪問 {#revoking-access-to-a-selected-user-queue}

1. 使用管理員帳戶登錄到管理控制台。
1. 選擇 **服務** > **表單工作流** > **共用隊列**。

1. 在「管理對用戶的訪問」頁籤上，查找並選擇要管理其隊列的用戶。
1. 右下窗格顯示有權訪問選定用戶隊列的用戶清單。 選擇用戶，然後按一下「撤消」。
1. 按一下「保存」完成。

## 管理分配給用戶的隊列 {#managing-queues-assigned-to-a-user}

管理用戶訪問功能允許您管理分配給選定用戶的隊列。 您可以單獨向選定用戶授予或撤消對用戶隊列的訪問權限。 例如，您希望將Akira Tanaka和John Jacobs用戶隊列分配給Kara Bowman。 使用「按用戶管理訪問」功能，您可以搜索Kara Bowman並授予對分配給Akira Tanaka和John Jacobs的任務的訪問權限。 稍後，您可以取消Kara Bowman對這些用戶隊列的訪問。

分配完這些任務後，用戶可以使用Workspace完成。

>[!NOTE]
>
>不建議使用Flex工AEM作空間。

### 授予對所選用戶隊列的訪問權限 {#granting-access-to-a-selected-user-queue}

1. 使用管理員帳戶登錄到管理控制台。
1. 選擇 **服務** > **表單工作流** > **共用隊列**。

1. 在「管理對用戶的訪問」頁籤上，查找並選擇要共用其隊列的用戶。 在任何時候，右下窗格都顯示有權訪問選定用戶隊列的用戶清單。
1. 在左下窗格中，查找並選擇要與選定用戶共用的用戶隊列。 按一下「共用」。
1. 按一下「保存」完成。

### 撤消對所選用戶隊列的訪問 {#revoking_access_to_a_selected_user_queue-1}

1. 使用管理員帳戶登錄到管理控制台。
1. 選擇 **服務** > **表單工作流** > **共用隊列**。

1. 在「按用戶管理訪問」頁籤上，查找並選擇要管理其隊列的用戶。
1. 右下窗格顯示分配給選定用戶的用戶隊列清單。 選擇用戶隊列，然後按一下「撤消」。
1. 按一下「保存」完成。
