---
title: 管理工作流程存取權
seo-title: Managing Access to Workflows
description: 瞭解如何管理對工作流的訪問。
seo-description: Learn how to manage access to Workflows.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---

# 管理工作流程存取權{#managing-access-to-workflows}

根據用戶帳戶配置ACL以允許（或禁用）啟動和參與工作流。

## 工作流所需的用戶權限 {#required-user-permissions-for-workflows}

在以下情況下，可對工作流執行操作：

* 你在工作 `admin` 帳戶
* 帳戶已分配給預設組 `workflow-users`:

   * 此組包含用戶執行工作流操作所需的所有權限。
   * 當帳戶在此組中時，它只有權訪問它已啟動的工作流。

* 帳戶已分配給預設組 `workflow-administrators`:

   * 此組包含特權用戶監視和管理工作流所需的所有權限。
   * 當帳戶在此組中時，它有權訪問所有工作流。

>[!NOTE]
>
>這是最低要求。 您的帳戶還必須是已分配的參與者或已分配組的成員，才能採取特定步驟。

## 配置對工作流的訪問 {#configuring-access-to-workflows}

工作流模型繼承一個預設訪問控制清單(ACL)，用於控制用戶如何與工作流交互。 要自定義工作流的用戶訪問，請修改包含工作流模型節點的資料夾的儲存庫中的訪問控制清單(ACL):

* [將特定工作流模型的ACL應用於/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [在/var/workflow/models中建立子資料夾，並將ACL應用於](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>有關使用CRXDE Lite配置ACL的資訊，請參見 [訪問權限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

### 將特定工作流模型的ACL應用於/var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

如果工作流模型儲存在 `/var/workflow/models` 然後，您可以在資料夾中指定與該工作流相關的特定ACL:

1. 在Web瀏覽器中開啟CRXDE Lite(例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在節點樹中，為工作流模型資料夾選擇節點：

   `/var/workflow/models`

1. 按一下 **訪問控制** 頁籤。
1. 在 **本地訪問控制策略** (**訪問控制清單**)表格，按一下加號表徵圖 **添加條目**。
1. 在 **添加新條目** 對話框添加具有以下屬性的新ACE:

   * **主**: `content-authors`
   * **類型**: `Deny`
   * **權限**: `jcr:read`
   * **rep:glob**:引用特定工作流

   ![wf-108](assets/wf-108.png)

   的 **訪問控制清單** 表現在包括對 `content-authors` 的 `prototype-wfm-01` 工作流模型。

   ![wf-109](assets/wf-109.png)

1. 按一下 **全部保存**。

   的 `prototype-wfm-01` 工作流不再可用於 `content-authors` 組。

### 在/var/workflow/models中建立子資料夾，並將ACL應用於 {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

您 [開發團隊可以在子資料夾中建立工作流](/help/sites-developing/workflows-models.md#creating-a-new-workflow) 共

`/var/workflow/models`

與儲存在

`/var/workflow/models/dam/`

然後，可以向資料夾本身添加ACL。

1. 在Web瀏覽器中開啟CRXDE Lite(例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在節點樹中，為工作流模型資料夾中的單個資料夾選擇節點；例如：

   `/var/workflow/models/prototypes`

1. 按一下 **訪問控制** 頁籤。
1. 在 **適用的訪問控制策略** 表徵圖 **添加** 的下界。
1. 在 **本地訪問控制策略** (**訪問控制清單**)表格，按一下加號表徵圖 **添加條目**。
1. 在 **添加新條目** 對話框添加具有以下屬性的新ACE:

   * **主**: `content-authors`
   * **類型**: `Deny`
   * **權限**: `jcr:read`

   >[!NOTE]
   >
   >與 [將特定工作流模型的ACL應用於/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) 您可以包括rep:glob以限制對特定工作流的訪問。

   ![wf-110](assets/wf-110.png)

   的 **訪問控制清單** 表現在包括對 `content-authors` 的 `prototypes` 的子菜單。

   ![wf-111](assets/wf-111.png)

1. 按一下 **全部保存**。

   中的模型 `prototypes` 資料夾不再可供 `content-authors` 組。
