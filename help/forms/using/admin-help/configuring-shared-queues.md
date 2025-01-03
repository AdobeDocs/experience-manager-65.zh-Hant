---
title: 設定共用佇列
description: 共用佇列可讓您有效設定和管理使用者佇列。 瞭解如何設定共用佇列。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# 設定共用佇列{#configuring-shared-queues}

共用佇列可讓您有效設定和管理使用者佇列。 使用者佇列只是指派給使用者的所有工作，如需詳細資訊，請參閱[待辦事項清單](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html)。 您可以根據組織需求指派、取消指派和重新指派使用者佇列。 您可以透過兩種方式管理共用佇列：

**管理使用者的存取權**

您可以使用此選項來管理所選使用者佇列的存取權。

**由使用者管理存取權**

您可以使用此選項來管理指派給選定使用者的共用佇列。

## 管理所選使用者佇列的存取權 {#managing-access-to-a-selected-user-queue}

管理對使用者的存取權功能可讓您管理對所選使用者佇列的存取權。 您可以將選取之使用者佇列的存取權授與或撤銷給貴組織中的其他使用者。 例如，卡拉·鮑曼不在辦公室。 使用「管理使用者存取」功能，Kara的佇列可以與Akira Tanaka和John Jacobs共用以完成。 在稍後時間，當Kara回到辦公室時，您可以撤銷田中昭和約翰·雅各布斯對其佇列的存取權。

共用後，這些工作可由具有佇列存取權的使用者使用Workspace來完成。

>[!NOTE]
>
>AEM Forms版本已棄用Flex Workspace。

### 設定選取使用者佇列的存取權 {#configuring-access-to-a-selected-user-queue}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

1. 使用管理員帳戶登入管理主控台。
1. 選取&#x200B;**服務** > **Forms Workflow** > **共用佇列**。

1. 在管理使用者的存取權索引標籤中，尋找並選取您要共用其佇列的使用者。 在任何時候，右下角窗格都會顯示可存取所選使用者佇列的使用者清單。
1. 在左下方的窗格中，尋找並選取使用者。 按一下「共用」。
1. 按一下「儲存」以完成。

### 撤銷對所選使用者佇列的存取權 {#revoking-access-to-a-selected-user-queue}

1. 使用管理員帳戶登入管理主控台。
1. 選取&#x200B;**服務** > **Forms Workflow** > **共用佇列**。

1. 在管理使用者的存取權索引標籤中，尋找並選取您要管理其佇列的使用者。
1. 右下方的窗格會顯示可存取所選使用者佇列的使用者清單。 選取使用者，然後按一下撤銷。
1. 按一下「儲存」以完成。

## 管理指派給使用者的佇列 {#managing-queues-assigned-to-a-user}

「依使用者管理存取」功能可讓您管理指派給選定使用者的佇列。 您可以將使用者佇列的存取權個別授與或撤銷給選取的使用者。 例如，您希望將Akira Tanaka和John Jacobs使用者佇列指派給Kara Bowman。 使用「依使用者管理存取權」功能，您可以搜尋Kara Bowman並授予指派給Akira Tanaka和John Jacobs的工作存取權。 您稍後可以撤銷Kara Bowman對這些使用者佇列的存取權。

指派後，使用者即可使用Workspace完成這些工作。

>[!NOTE]
>
>AEM Forms版本已棄用Flex Workspace。

### 授與所選使用者佇列的存取權 {#granting-access-to-a-selected-user-queue}

1. 使用管理員帳戶登入管理主控台。
1. 選取&#x200B;**服務** > **Forms Workflow** > **共用佇列**。

1. 在管理使用者的存取權索引標籤中，尋找並選取您要共用其佇列的使用者。 在任何時候，右下角窗格都會顯示可存取所選使用者佇列的使用者清單。
1. 在左下方的窗格中，尋找並選取您要與所選使用者共用的使用者佇列。 按一下「共用」。
1. 按一下「儲存」以完成。

### 撤銷對所選使用者佇列的存取權 {#revoking_access_to_a_selected_user_queue-1}

1. 使用管理員帳戶登入管理主控台。
1. 選取&#x200B;**服務** > **Forms Workflow** > **共用佇列**。

1. 在依使用者管理存取權標籤中，尋找並選取您要管理其佇列的使用者。
1. 右下方窗格顯示指派給所選使用者的使用者佇列清單。 選取使用者佇列，然後按一下撤銷。
1. 按一下「儲存」以完成。
