---
title: 配置共用隊列
seo-title: Configuring Shared Queues
description: 共用隊列允許您有效地配置和管理用戶隊列。 了解如何配置共用隊列。
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

共用隊列允許您有效地配置和管理用戶隊列。 用戶隊列只是指派給用戶的所有任務，請參閱 [執行清單](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) 以取得更多資訊。 您可以根據您的組織需求來分配、取消分配和重新分配用戶隊列。 可以通過兩種方式管理共用隊列：

**管理對使用者的存取**

您可以使用此選項管理對選定用戶隊列的訪問。

**管理使用者的存取權**

您可以使用此選項管理分配給選定用戶的共用隊列。

## 管理對選定用戶隊列的訪問 {#managing-access-to-a-selected-user-queue}

「管理對用戶的訪問」功能允許您管理對選定用戶隊列的訪問。 您可以授予或撤銷對所選使用者佇列的存取權給組織中的其他使用者。 比如，卡拉·鮑曼已經不在辦公室了。 使用「管理使用者存取權」功能，可與田中明和John Jacobs共用佇列以完成作業。 之後，當卡拉·鮑曼回到辦公室時，你可以取消對田中明和約翰·雅可布隊伍的訪問。

共用後，使用者即可使用工作區完成這些工作，並擁有佇列的存取權。

>[!NOTE]
>
>AEM Forms版本已不再使用Flex Workspace。

### 配置對選定用戶隊列的訪問 {#configuring-access-to-a-selected-user-queue}

1. 使用管理員帳戶登入管理控制台。
1. 選擇 **服務** > **表單工作流程** > **共用佇列**.

1. 在「管理對用戶的訪問」頁簽上，查找並選擇要共用其隊列的用戶。 無論如何，右下窗格都會顯示可存取所選使用者佇列的使用者清單。
1. 在左下窗格中，查找並選擇用戶。 按一下「共用」。
1. 按一下「儲存」以完成。

### 撤消對選定用戶隊列的訪問 {#revoking-access-to-a-selected-user-queue}

1. 使用管理員帳戶登入管理控制台。
1. 選擇 **服務** > **表單工作流程** > **共用佇列**.

1. 在「管理對用戶的訪問」頁簽上，查找並選擇要管理其隊列的用戶。
1. 右下窗格顯示有權訪問所選用戶隊列的用戶清單。 選擇用戶，然後按一下撤消。
1. 按一下「儲存」以完成。

## 管理分配給用戶的隊列 {#managing-queues-assigned-to-a-user}

「按用戶管理訪問」功能允許您管理分配給選定用戶的隊列。 您可以將對用戶隊列的訪問權限單獨授予或撤消給選定用戶。 例如，您希望將Akira Tanaka和John Jacobs用戶隊列分配給Kara Bowman。 使用「按用戶管理訪問」功能，您可以搜索Kara Bowman並授予對分配給Akira Tanaka和John Jacobs的任務的訪問權。 稍後，您可以撤銷Kara Bowman對這些用戶隊列的訪問權限。

指派後，使用者即可使用工作區完成這些工作。

>[!NOTE]
>
>AEM Forms版本已不再使用Flex Workspace。

### 授予對選定用戶隊列的訪問權 {#granting-access-to-a-selected-user-queue}

1. 使用管理員帳戶登入管理控制台。
1. 選擇 **服務** > **表單工作流程** > **共用佇列**.

1. 在「管理對用戶的訪問」頁簽上，查找並選擇要共用其隊列的用戶。 無論如何，右下窗格都會顯示可存取所選使用者佇列的使用者清單。
1. 在左下窗格中，查找並選擇要與所選用戶共用的用戶隊列。 按一下「共用」。
1. 按一下「儲存」以完成。

### 撤消對選定用戶隊列的訪問 {#revoking_access_to_a_selected_user_queue-1}

1. 使用管理員帳戶登入管理控制台。
1. 選擇 **服務** > **表單工作流程** > **共用佇列**.

1. 在「按用戶管理訪問」頁簽上，查找並選擇要管理其隊列的用戶。
1. 右下窗格顯示分配給所選用戶的用戶隊列清單。 選擇用戶隊列，然後按一下撤消。
1. 按一下「儲存」以完成。
