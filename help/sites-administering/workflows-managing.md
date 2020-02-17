---
title: 管理對工作流程的存取
seo-title: 管理對工作流程的存取
description: 瞭解如何管理對工作流程的存取。
seo-description: 瞭解如何管理對工作流程的存取。
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理對工作流程的存取{#managing-access-to-workflows}

根據用戶帳戶配置ACL以允許（或禁用）啟動和參與工作流。

## 工作流程的必要使用者權限 {#required-user-permissions-for-workflows}

在下列情況下，可對工作流程採取行動：

* 您正在使用帳 `admin` 戶
* 帳戶已指派給預設群組 `workflow-users`:

   * 此群組擁有使用者執行工作流程動作所需的所有權限。
   * 當帳戶在此群組中時，它只能存取其啟動的工作流程。

* 帳戶已指派給預設群組 `workflow-administrators`:

   * 此群組擁有您的特權使用者監控和管理工作流程所需的所有權限。
   * 當帳戶在此群組中時，它可存取所有工作流程。

>[!NOTE]
>
>這些是最低要求。 您的帳戶也必須是已指派的參與者或已指派群組的成員，才能採取特定步驟。

## 設定對工作流程的存取權 {#configuring-access-to-workflows}

工作流模型繼承了預設訪問控制清單(ACL)，用於控制用戶與工作流交互的方式。 要自定義工作流的用戶訪問權，請修改包含工作流模型節點的資料夾的儲存庫中的訪問控制清單(ACL):

* [將特定工作流模型的ACL應用到/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [在/var/workflow/models中建立子資料夾，並將ACL應用到](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>有關使用CRXDE Lite配置ACL的資訊，請參見 [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

### 將特定工作流模型的ACL應用到/var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

如果工作流模型儲存在檔案 `/var/workflow/models` 夾中，則可以在資料夾中指定與該工作流相關的特定ACL:

1. 在您的網頁瀏覽器中開啟CRXDE Lite(例如 [http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在節點樹中，選擇工作流模型資料夾的節點：

   `/var/workflow/models`

1. 按一下「 **存取控制** 」標籤。
1. 在「本 **地訪問控制策略** (**訪問控制清單**)」表中，按一下加號表徵圖添加 **條目**。
1. 在「添 **加新條目** 」對話框中，添加具有以下屬性的新ACE:

   * **負責人**: `content-authors`
   * **類型**: `Deny`
   * **權限**: `jcr:read`
   * **rep:glob**:參考特定工作流程
   ![wf-108](assets/wf-108.png)

   「存 **取控制清單** 」(Access Control List `content-authors` )表格現在包含對工作 `prototype-wfm-01` 流程模型的限制。

   ![wf-109](assets/wf-109.png)

1. 按一下「 **全部儲存**」。

   群 `prototype-wfm-01` 組成員無法再使用工作 `content-authors` 流程。

### 在/var/workflow/models中建立子資料夾，並將ACL應用到 {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

您的 [開發團隊可以在](/help/sites-developing/workflows-models.md#creating-a-new-workflow)

`/var/workflow/models`

與儲存在

`/var/workflow/models/dam/`

然後，可以將ACL添加到資料夾本身。

1. 在您的網頁瀏覽器中開啟CRXDE Lite(例如 [http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在節點樹中，選擇工作流模型資料夾中單個資料夾的節點；例如：

   `/var/workflow/models/prototypes`

1. 按一下「 **存取控制** 」標籤。
1. 在「適 **用的訪問控制策略** 」(Appliable Access Control Policy **)表格中，按一下加號圖** 標添加條目。
1. 在「本 **地訪問控制策略** (**訪問控制清單**)」表中，按一下加號表徵圖添加 **條目**。
1. 在「添 **加新條目** 」對話框中，添加具有以下屬性的新ACE:

   * **負責人**: `content-authors`
   * **類型**: `Deny`
   * **權限**: `jcr:read`
   >[!NOTE]
   >
   >與將特 [定工作流模型的ACL應用到/var/workflow/models一樣](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) ，您可以包括rep:glob以限制對特定工作流的訪問。

   ![wf-110](assets/wf-110.png)

   「訪 **問控制清單** 」(Access Control List `content-authors` )表格現在包含對資料夾 `prototypes` 的限制。

   ![wf-111](assets/wf-111.png)

1. 按一下「 **全部儲存**」。

   資料夾中的 `prototypes` 模型不再適用於組的成 `content-authors` 員。

