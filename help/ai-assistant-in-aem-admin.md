---
title: 在AEM中設定AI助理
description: 瞭解如何使用Adobe Experience Manager中的Admin Console來設定人工智慧助理。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
source-git-commit: 11be37d5a96dd7236f2011b6df3e39bf0b1904b7
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 3%

---

# 在AEM中設定AI助理 {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

若要在AEM (Adobe Experience Manager)中使用AI助理，您的組織必須選擇Admin Console層級的加入。 產品管理員會建立（或選擇）使用者群組，並授予其新的「AI助理」許可權。 新增到該群組的所有人都能立即在整個AEM中存取AI Assistant。 如果目標是讓整個公司都可使用，管理員只需將所有使用者指派給該群組即可。

從員工的角度來看，程式簡單明瞭：識別組織中Adobe Experience Manager的產品管理員，並請求將其新增至啟用AI的使用者群組。 一旦您出現在群組中，「助理員」圖示就會在您下次登入時自動顯示。

管理員應牢記正常的Cloud Manager控管。 在Admin Console中保留產品管理員許可權，以建立設定檔、管理使用者群組或編輯許可權。 如果使用者還需要助理的內建&#x200B;**建立支援票證**&#x200B;功能，請將標準&#x200B;**支援管理員**&#x200B;角色(標準Admin Console角色)新增至相同的個人或群組。

AEM中AI助理的設定程式包含下列步驟：

1. [在Adobe Admin Console中建立新的產品設定檔](#create-profile)。
1. [啟用AI助理產品知識許可權](#enable-permission)。
1. [建立新的使用者群組（或使用現有的使用者群組）](#create-user-group)。
1. [新增使用者至使用者群組](#add-users)。
1. [將產品設定檔指派給使用者群組](#assign-product-profile)。

**先決條件**

開始之前，請確定您已符合下列必要條件：

* 您在Adobe Admin Console中必須至少具有產品管理員許可權。
* 您瞭解組織的使用者管理結構。

**組態考量**

* 處理時間：在Cloud Manager中建立的資源可能需要最多2分鐘的時間才能在Admin Console中顯示許可權設定。
* 多個設定檔：使用者可以成為多個設定檔的一部分，並且所有指派的設定檔中的許可權會合併。
* 組織範圍：某些許可權可能適用於所有計畫的組織層級。
* 預先定義的設定檔：請勿從Admin Console刪除預先定義的許可權設定檔。


## 1 — 在Adobe Admin Console中建立新的產品設定檔{#create-profile}

1. 依照[在Experience Platform檔案中找到的Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile)中建立新產品設定檔中的詳細指示操作。

1. 建立新產品設定檔時，您可以對AI助理使用下列建議值。

   | 文字欄位 | 建議值 |
   | --- | --- |
   | 產品設定檔名稱 | `AI Assistant in AEM` （或您偏好的描述性名稱） |
   | 顯示名稱（選擇性） | `AI Assistant` |
   | 說明 (選填) | `Product profile for managing AI Assistant in AEM access` |
   | 通知 | 根據您組織的偏好設定進行設定 |


## 2 — 啟用AI助理產品知識許可權{#enable-permission}

指派自訂許可權給產品設定檔的程式遵循標準Adobe Cloud Manager自訂許可權工作流程。

參考文章： [將自訂許可權指派給新的產品設定檔](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. 在Admin Console中，按一下您新建立的產品設定檔名稱(`AI Assistant in AEM`)

   ![螢幕擷圖](/help/assets/assets-ai/ai-assistant-console.png)

1. 若要檢視可編輯許可權的清單，請按一下&#x200B;**許可權**&#x200B;索引標籤。

1. 在表格清單中，找出`AI Assistant Product Knowledge`許可權。

   Admin Console中的![AI助理許可權索引標籤](/help/assets/assets-ai/ai-assistant-permission.png)

1. 在許可權名稱的右側，按一下![鉛筆圖示或「編輯」圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)。

1. 在&#x200B;**編輯AI助理的許可權**&#x200B;頁面上，開啟&#x200B;**AI助理產品知識**&#x200B;切換開關。

   ![ AI助理產品知識切換選項的編輯許可權頁面](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. 在頁面的右下角，按一下[儲存]。**&#x200B;**

   您的產品設定檔現在已啟用AI助理產品知識許可權。


## 3 — 建立新的使用者群組（或使用現有的使用者群組）{#create-user-group}

1. 執行下列任一項作業：

>[!BEGINTABS]

>[!TAB 建立新的使用者群組]

1. 在Admin Console中，按一下&#x200B;**使用者** > **使用者群組**。

   ![使用者群組](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. 在&#x200B;**使用者群組**&#x200B;頁面上按一下&#x200B;**新增使用者群組**。

   ![使用者群組頁面上的[新增使用者群組]按鈕](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. 在&#x200B;**建立新使用者群組**&#x200B;頁面上，提供下列資訊：

   | 選項 | 建議值 |
   | --- | --- |
   | 使用者群組名稱 | `AI Assistant in AEM` （或您偏好的名稱） |
   | 說明 (選填) | `User group for managing AI Assistant in AEM access` |

   ![建立新的使用者群組頁面](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. 在頁面的右下角，按一下[儲存]。**&#x200B;**

>[!TAB 使用現有的使用者群組]

如果現有AEM使用者群組符合AI Assistant存取要求，您就可以使用該使用者群組，而不需要建立新群組。

>[!ENDTABS]

## 4 — 將使用者新增至使用者群組{#add-users}

1. 執行下列任一項作業：

>[!BEGINTABS]

>[!TAB 新增個別使用者]

1. 在&#x200B;**使用者群組**&#x200B;頁面的&#x200B;**群組名稱**&#x200B;表格中，按一下您新建立的使用者群組名稱或現有的使用者群組名稱。

   ![使用者群組頁面，在資料表](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)中顯示AEM使用者群組名稱中的AI助理

1. 在AEM **中** AI助理的&#x200B;**使用者群組**&#x200B;頁面中，按一下&#x200B;**使用者**&#x200B;索引標籤，然後按一下&#x200B;**新增使用者**。

   在AEM使用者群組頁面中的![AI助理顯示[使用者]索引標籤和[新增使用者]按鈕](/help/assets/assets-ai/ai-assistant-add-users.png)

1. 在&#x200B;**`Add users to this user group`**&#x200B;頁面上，搜尋並選取需要存取AEM中AI助理的使用者。

   ![新增使用者至此使用者群組頁面](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. 在頁面的右下角，按一下[儲存]。**&#x200B;**
1. 現在，[將產品設定檔指派給使用者群組](#assign-product-profile)。

>[!TAB 大量新增使用者]

您可以在Admin Console中使用大量上傳功能。

1. 準備包含使用者資訊的CSV檔案。
1. 使用&#x200B;**`Add users by CSV`**&#x200B;選項進行有效的大量新增。
1. 現在，[將產品設定檔指派給使用者群組](#assign-product-profile)。

>[!ENDTABS]


## 5 — 將產品設定檔指派給使用者群組{#assign-product-profile}

此步驟遵循將產品設定檔指派給使用者群組的標準Adobe Admin Console工作流程。

參考文章： [管理企業使用者的產品設定檔](https://helpx.adobe.com/tw/enterprise/using/manage-product-profiles.html)

1. 當您仍在AEM使用者群組的AI助理中時，從[4 — 將使用者新增到使用者群組](#add-users)，按一下&#x200B;**已指派的產品設定檔**&#x200B;索引標籤。
1. 按一下&#x200B;**指派設定檔**。

   ![AEM使用者群組頁面中的AI助理已選取指派的產品設定檔索引標籤](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. 在&#x200B;**指派產品和設定檔**&#x200B;頁面的&#x200B;**選取產品設定檔**&#x200B;對話方塊中，搜尋並選取您的&#x200B;**AI助理**&#x200B;產品設定檔。

   ![「指派產品和設定檔」頁面，顯示「選取產品設定檔」對話方塊和選取的「AI助理」產品設定檔](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. 在對話方塊的右下角附近，按一下&#x200B;**套用**。
1. 在&#x200B;**指派產品和設定檔**&#x200B;頁面的右下角附近，按一下&#x200B;**儲存**。

   ![顯示指派給AEM使用者群組中AI助理的AI助理產品設定檔](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## 驗證設定

* 檢查您的產品設定檔顯示指派的使用者群組數量是否正確。
* 驗證使用者群組是否顯示正確數量的使用者。
* 確認已啟用並正確設定AI助理產品知識許可權。


## 測試設定

讓指派群組中的使用者執行下列動作：

1. 登入AEM。
2. 確認AI助理功能可供存取。
3. 測試AI Assistant的功能以確保正確啟用。

## 另請參閱

* [AEM 中的 AI 助理](/help/ai-assistant-in-aem.md)
* [Adobe Experience Platform存取控制](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
