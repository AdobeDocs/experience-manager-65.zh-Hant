---
title: 配置共用隊列
seo-title: 配置共用隊列
description: 共用隊列允許您有效地配置和管理用戶隊列。 瞭解如何設定共用佇列。
seo-description: 共用隊列允許您有效地配置和管理用戶隊列。 瞭解如何設定共用佇列。
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# 配置共用隊列{#configuring-shared-queues}

共用隊列允許您有效地配置和管理用戶隊列。 用戶隊列只是指派給用戶的所有任務，有關詳細資訊，請參見[ To Do Lists](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html)。 您可以根據組織需求來指派、取消指派和重新指派使用者佇列。 可以通過兩種方式管理共用隊列：

**管理對使用者的存取權**

您可以使用此選項管理對選定用戶隊列的訪問。

**管理使用者的存取權**

您可以使用此選項管理指派給選定用戶的共用隊列。

## 管理對選定用戶隊列{#managing-access-to-a-selected-user-queue}的訪問

「管理對用戶的訪問」功能允許您管理對選定用戶隊列的訪問。 您可以將所選使用者佇列的存取權授予或撤銷給組織中的其他使用者。 比如，卡拉·鮑曼不在辦公室。 使用「管理使用者存取權」功能，您可以將她的佇列與Akira Tanaka和John Jacobs共用，以完成工作。 稍後，當卡拉·鮑曼回到辦公室時，你可以撤銷對田中明和約翰·雅各布斯排隊的存取權。

共用後，使用者可使用工作區，以存取佇列，即可完成這些工作。

>[!NOTE]
>
>AEM表單版本不建議使用Flex Workspace。

### 配置對選定用戶隊列{#configuring-access-to-a-selected-user-queue}的訪問

1. 使用管理員帳戶登入管理控制台。
1. 選擇&#x200B;**服務** > **表單工作流** > **共用隊列**。

1. 在「管理對用戶的訪問」頁籤上，查找並選擇要共用其隊列的用戶。 右下方窗格會隨時顯示有權存取所選使用者佇列的使用者清單。
1. 在左下窗格中，尋找並選取使用者。 按一下「共用」。
1. 按一下「儲存」以完成。

### 撤消對選定用戶隊列{#revoking-access-to-a-selected-user-queue}的訪問

1. 使用管理員帳戶登入管理控制台。
1. 選擇&#x200B;**服務** > **表單工作流** > **共用隊列**。

1. 在「管理對用戶的訪問」頁籤上，查找並選擇要管理其隊列的用戶。
1. 右下窗格顯示有權訪問所選用戶隊列的用戶清單。 選取使用者，然後按一下「廢止」。
1. 按一下「儲存」以完成。

## 管理分配給用戶{#managing-queues-assigned-to-a-user}的隊列

「按用戶管理訪問」功能允許您管理分配給選定用戶的隊列。 您可以個別授予或撤銷對所選使用者佇列的存取權。 例如，您希望將Akira Tanaka和John Jacobs的使用者佇列給Kara Bowman。 使用「Manage Access By A User」（按用戶管理訪問）功能，您可以搜索Kara Bowman並授予對Akira Tanaka和John Jacobs的任務訪問權限。 稍後，您可以撤銷Kara Bowman對這些使用者佇列的存取權。

指派後，使用者可使用工作區完成這些工作。

>[!NOTE]
>
>AEM表單版本不建議使用Flex Workspace。

### 授予對選定用戶隊列{#granting-access-to-a-selected-user-queue}的訪問權

1. 使用管理員帳戶登入管理控制台。
1. 選擇&#x200B;**服務** > **表單工作流** > **共用隊列**。

1. 在「管理對用戶的訪問」頁籤上，查找並選擇要共用其隊列的用戶。 右下方窗格會隨時顯示有權存取所選使用者佇列的使用者清單。
1. 在左下窗格中，尋找並選取您要與所選使用者共用的使用者佇列。 按一下「共用」。
1. 按一下「儲存」以完成。

### 撤消對選定用戶隊列{#revoking_access_to_a_selected_user_queue-1}的訪問

1. 使用管理員帳戶登入管理控制台。
1. 選擇&#x200B;**服務** > **表單工作流** > **共用隊列**。

1. 在「按用戶管理訪問」頁籤上，查找並選擇要管理其隊列的用戶。
1. 右下窗格顯示分配給選定用戶的用戶隊列清單。 選取使用者佇列，然後按一下「廢止」。
1. 按一下「儲存」以完成。

