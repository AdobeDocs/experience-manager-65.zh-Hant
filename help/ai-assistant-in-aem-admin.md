---
title: 設定 AEM 中的 AI 助理
description: 了解如何使用 Adobe Experience Manager 中的 Admin Console 來設定 AI 助理。
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
autotag-review: '2026-05-18T18:35:37.980Z'
TQID: 'https://experienceleague.adobe.com/5YTQUJbJPlJuxToS6AVhJww1KQ20tuOlRoCVquyfSng'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1202
ht-degree: 98%

---

# 設定 AEM 中的 AI 助理 {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

若要在 AEM (Adobe Experience Manager) 中使用 AI 助理，必須擁有透過 AI 助理存取產品知識的權限。 此權限預設為「開啟」。

如果您想要控制誰可以存取產品知識，請從與您的 Adobe ID 關聯之電子郵件地址寄送電子郵件到 [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com)。 Adobe 可啟用使用者層級存取控制。 啟用後，您的管理員可以依照下列步驟授予使用者層級存取權。

如果您已要求使用者層級存取控制，您的組織必須透過 Adobe Admin Console 選擇加入。 產品管理員會建立 (或選擇) 使用者群組，並授予其新的「AI 助理」權限。 新增到該群組的所有人都能立即在整個 AEM 中存取 AI 助理。 如果目標是讓整個公司都可使用，管理員只需將所有使用者指派給該群組即可。

從員工的角度來看，程序簡單明瞭：識別組織中的 Adobe Experience Manager 產品管理員，並請求將其新增至具有 AI 功能的使用者群組。 當您出現在該群組時，「助理」圖示便會在您下次登入時自動顯示。

管理員應記住正常的 Cloud Manager 治理。 在 Admin Console 中保留產品管理員權限，以建立輪廓、管理使用者群組或編輯權限。 如果使用者還需要助理的內建&#x200B;**建立支援票證**&#x200B;功能，請將標準&#x200B;**支援管理員**&#x200B;角色 (標準 Admin Console 角色) 新增至相同的個體或群組。

AEM 中的 AI 助理之設定程序包含下列步驟：

1. [在 Adobe Admin Console 中建立新的產品輪廓](#create-profile)。
1. [啟用 AI 助理產品知識權限](#enable-permission)。
1. [建立新的使用者群組 (或使用現有的使用者群組)](#create-user-group)。
1. [新增使用者至使用者群組](#add-users)。
1. [將產品輪廓指派給使用者群組](#assign-product-profile)。

**先決條件**

開始之前，請確定您已符合下列先決條件：

* 您在 Adobe Admin Console 中必須至少具有產品管理員權限。
* 您對組織的使用者管理結構有所了解。

**設定考量**

* 處理時間：在 Cloud Manager 中建立的資源可能需要最多 2 分鐘才會出現在 Admin Console 以進行權限設定。
* 多個輪廓：使用者可以成為多個輪廓的一部分，並且權限會從所有指派的輪廓中合併。
* 組織範圍：某些權限可能適用於所有方案的組織層級。
* 預先定義的輪廓：請勿從 Admin Console 刪除預先定義的權限輪廓。


## &#x200B;1. - 在 Adobe Admin Console 中建立新的產品輪廓{#create-profile}

1. 在 Experience Platform 文件中找到[在 Adobe Admin Console 中建立新的產品輪廓](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/access-control/ui/create-profile)的詳細說明，並依循其指示進行操作。

1. 建立新產品輪廓時，您可以對 AI 助理使用下列建議值。

   | 文字欄位 | 建議值 |
   | --- | --- |
   | 產品輪廓名稱 | `AI Assistant in AEM` (或您偏好的說明性名稱) |
   | 顯示名稱 (選用) | `AI Assistant` |
   | 說明 (選填) | `Product profile for managing AI Assistant in AEM access` |
   | 通知 | 根據您組織的偏好進行設定 |


## &#x200B;2. - 啟用 AI 助理產品知識權限{#enable-permission}

指派自訂權限給產品輪廓的程序遵循標準 Adobe Cloud Manager 自訂權限工作流程。

參考文章：[將自訂權限指派到新的產品輪廓](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. 在 Admin Console 中，按一下您剛建立的新產品輪廓名稱 (`AI Assistant in AEM`)

   ![螢幕擷圖](/help/assets/assets-ai/ai-assistant-console.png)

1. 若要檢視可編輯權限的清單，請按一下&#x200B;**「權限」**&#x200B;索引標籤。

1. 在表格清單中，找到 `AI Assistant Product Knowledge` 權限。

   ![Admin Console 中的 AI 助理權限索引標籤](/help/assets/assets-ai/ai-assistant-permission.png)

1. 在權限名稱的右側，按一下![「鉛筆」圖示或「編輯」圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)。

1. 在&#x200B;**「編輯 AI 助理的權限」**&#x200B;頁面上，開啟&#x200B;**「AI 助理產品知識」**&#x200B;切換開關。

   ![AI 助理產品知識切換選項的編輯權限頁面](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. 在頁面的右下角，按一下&#x200B;**「儲存」**。

   您的產品輪廓現在已啟用 AI 助理產品知識權限。


## &#x200B;3. - 建立新的使用者群組 (或使用現有的使用者群組){#create-user-group}

1. 執行下列任一項作業：

>[!BEGINTABS]

>[!TAB 建立新的使用者群組]

1. 在 Admin Console 中，按一下&#x200B;**「使用者」**>**「使用者群組」**。

   ![使用者群組](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. 在&#x200B;**「使用者群組」**&#x200B;頁面上按一下&#x200B;**「新增使用者群組」**。

   ![「使用者群組」頁面上的「新增使用者群組」按鈕](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. 在&#x200B;**「建立新的使用者群組」**&#x200B;頁面上，提供下列資訊：

   | 選項 | 建議值 |
   | --- | --- |
   | 使用者群組名稱 | `AI Assistant in AEM` (或您偏好的名稱) |
   | 說明 (選填) | `User group for managing AI Assistant in AEM access` |

   ![「建立新的使用者群組」頁面](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. 在頁面的右下角，按一下&#x200B;**「儲存」**。

>[!TAB 使用現有的使用者群組]

如果現有 AEM 使用者群組符合 AI 助理的存取要求，您就可以使用該群組，而不需要建立新群組。

>[!ENDTABS]

## &#x200B;4. - 新增使用者至使用者群組{#add-users}

1. 執行下列任一項作業：

>[!BEGINTABS]

>[!TAB 新增個別使用者]

1. 在&#x200B;**「使用者群組」**&#x200B;頁面的&#x200B;**「群組名稱」**&#x200B;表格中，按一下您新建立的使用者群組名稱或現有的使用者群組名稱。

   ![「使用者群組」頁面在表格中顯示 AEM 使用者群組名稱中的 AI 助理](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. 在 **AEM 中的 AI 助理之**「使用者群組」**頁面上，**&#x200B;按一下&#x200B;**「使用者」**&#x200B;索引標籤，然後按一下&#x200B;**「新增使用者」**。

   在AEM使用者群組頁面中的![AI助理顯示[使用者]索引標籤和[新增使用者]按鈕](/help/assets/assets-ai/ai-assistant-add-users.png)

1. 在 **`Add users to this user group`** 頁面上，搜尋並選取需要存取 AEM 中的AI助理之使用者。

   ![新增使用者至此使用者群組頁面](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. 在頁面的右下角，按一下&#x200B;**「儲存」**。
1. 現在，[將產品輪廓指派給使用者群組](#assign-product-profile)。

>[!TAB 大量新增使用者]

您可以在 Admin Console 中使用大量上傳功能。

1. 準備包含使用者資訊的 CSV 檔案。
1. 使用&#x200B;**`Add users by CSV`**&#x200B;選項進行有效的大量新增。
1. 現在，[將產品輪廓指派給使用者群組](#assign-product-profile)。

>[!ENDTABS]


## &#x200B;5. - 將產品輪廓指派給使用者群組{#assign-product-profile}

此步驟遵循將產品輪廓指派給使用者群組的標準 Adobe Admin Console 工作流程。

參考文章：[管理企業使用者的產品輪廓](https://helpx.adobe.com/tw/enterprise/using/manage-product-profiles.html)

1. 當您仍在 AEM 使用者群組的 AI 助理中時，從 [4 - 新增使用者至使用者群組](#add-users)，按一下&#x200B;**「已指派的產品輪廓」**&#x200B;索引標籤。
1. 按一下&#x200B;**「指派輪廓」**。

   ![AEM 使用者群組頁面中的 AI 助理已選取「指派的產品輪廓」索引標籤](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. 在&#x200B;**「指派產品和輪廓」**&#x200B;頁面的&#x200B;**「選取產品輪廓」**&#x200B;對話框中，搜尋並選取您的 **AI 助理**&#x200B;產品輪廓。

   ![在「指派產品和輪廓」頁面，顯示「選取產品輪廓」對話框和選取的「AI助理」產品輪廓](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. 在對話框接近右下角，按一下&#x200B;**「套用」**。
1. 在&#x200B;**「指派產品和輪廓」**&#x200B;頁面右下角附近，按一下&#x200B;**「儲存」**。

   ![AI 助理產品輪廓顯示已指派給 AEM 使用者群組中的 AI 助理](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## 驗證設定

* 檢查您的產品輪廓是否顯示正確數量的已指派使用者群組。
* 驗證使用者群組是否顯示正確數量的使用者。
* 確認已啟用並正確設定 AI 助理產品知識權限。


## 測試設定

讓指派群組中的一名使用者執行下列動作：

1. 登入 AEM。
2. 確認 AI 助理功能可供存取。
3. 測試 AI 助理的功能以確保正確啟用。

## 另請參閱

* [AEM 中的 AI 助理](/help/ai-assistant-in-aem.md)
* [Adobe Experience Platform 中的存取控制](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
