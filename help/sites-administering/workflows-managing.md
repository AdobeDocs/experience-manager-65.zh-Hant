---
title: 管理工作流程存取權
seo-title: 管理工作流程存取權
description: 了解如何管理工作流程的存取權。
seo-description: 了解如何管理工作流程的存取權。
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# 管理工作流程存取權{#managing-access-to-workflows}

根據使用者帳戶設定ACL以允許（或停用）啟動和參與工作流程。

## 工作流{#required-user-permissions-for-workflows}所需的用戶權限

若符合以下條件，可對工作流程採取動作：

* 您正在使用`admin`帳戶
* 帳戶已分配給預設組`workflow-users`:

   * 此組保留用戶執行工作流操作所需的所有權限。
   * 帳戶在此群組中時，它只能存取其啟動的工作流程。

* 帳戶已分配給預設組`workflow-administrators`:

   * 此群組擁有特權使用者監控及管理工作流程所需的所有權限。
   * 帳戶在此群組中時，它可以存取所有工作流程。

>[!NOTE]
>
>這些是最低要求。 您的帳戶也必須是指派的參與者或指派群組的成員，才能執行特定步驟。

## 配置對工作流的訪問{#configuring-access-to-workflows}

工作流模型繼承預設訪問控制清單(ACL)，以控制用戶與工作流交互的方式。 要自定義工作流的用戶訪問，請修改包含工作流模型節點的資料夾的儲存庫中的訪問控制清單(ACL):

* [將特定工作流模型的ACL應用於/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [在/var/workflow/models中建立子資料夾，並將ACL套用至該資料夾](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>有關使用CRXDE Lite配置ACL的資訊，請參閱[訪問權限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

### 將特定工作流模型的ACL應用於/var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

如果工作流模型儲存在`/var/workflow/models`中，則可以在資料夾中指定與該工作流相關的特定ACL:

1. 在網頁瀏覽器中開啟CRXDE Lite(例如[http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在節點樹中，選擇工作流模型資料夾的節點：

   `/var/workflow/models`

1. 按一下&#x200B;**Access Control**&#x200B;頁簽。
1. 在&#x200B;**本地訪問控制策略**（**訪問控制清單**）表中，按一下&#x200B;**添加條目**&#x200B;的加號表徵圖。
1. 在&#x200B;**添加新條目**&#x200B;對話框中，添加具有以下屬性的新ACE:

   * **主要**:  `content-authors`
   * **類型**:  `Deny`
   * **權限**:  `jcr:read`
   * **rep:glob**:特定工作流程的參考

   ![wf-108](assets/wf-108.png)

   **存取控制清單**&#x200B;表格現在包含`prototype-wfm-01`工作流程模型上`content-authors`的限制。

   ![wf-109](assets/wf-109.png)

1. 按一下「**全部保存**」。

   `prototype-wfm-01`工作流不再適用於`content-authors`組的成員。

### 在/var/workflow/models中建立子資料夾，並將ACL套用至該{#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

您的[開發團隊可以在的子資料夾](/help/sites-developing/workflows-models.md#creating-a-new-workflow)中建立工作流程

`/var/workflow/models`

可比較儲存在

`/var/workflow/models/dam/`

然後，您可以將ACL添加到資料夾本身。

1. 在網頁瀏覽器中開啟CRXDE Lite(例如[http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在節點樹中，為工作流模型資料夾中的單個資料夾選擇節點；例如：

   `/var/workflow/models/prototypes`

1. 按一下&#x200B;**Access Control**&#x200B;頁簽。
1. 在&#x200B;**適用的訪問控制策略**&#x200B;表中，按一下&#x200B;**添加**&#x200B;條目的加號表徵圖。
1. 在&#x200B;**本地訪問控制策略**（**訪問控制清單**）表中，按一下&#x200B;**添加條目**&#x200B;的加號表徵圖。
1. 在&#x200B;**添加新條目**&#x200B;對話框中，添加具有以下屬性的新ACE:

   * **主要**:  `content-authors`
   * **類型**:  `Deny`
   * **權限**:  `jcr:read`

   >[!NOTE]
   >
   >與[將特定工作流模型的ACL應用到/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)一樣，您可以包括rep:glob以限制對特定工作流的訪問。

   ![wf-110](assets/wf-110.png)

   **存取控制清單**&#x200B;表格現在包含`prototypes`資料夾上`content-authors`的限制。

   ![wf-111](assets/wf-111.png)

1. 按一下「**全部保存**」。

   `prototypes`資料夾中的模型不再可供`content-authors`組的成員使用。
