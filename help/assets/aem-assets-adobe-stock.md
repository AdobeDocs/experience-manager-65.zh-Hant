---
title: 管理 [!DNL Adobe Stock] 資產
description: 搜索、獲取、許可和管理 [!DNL Adobe Stock] 資產 [!DNL Adobe Experience Manager]。 將授權資產用作任何其他數字資產。
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 7%

---

# 使用 [!DNL Adobe Stock] 資產 [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-assets-adobe-stock.html?lang=en) |
| AEM 6.5 | 本文 |

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

[!DNL Adobe Stock] 服務為設計師和企業提供了對其所有創造性項目的數百萬高質量、可策劃的免版稅照片、向量、插圖、視頻、模板和3D資產的訪問權。

[!DNL Adobe Stock] 預設情況下，企業產品包括整個組織的共用權。 資產一旦獲得組織用戶的許可，組織的其他用戶就可以識別、下載和使用此資產，而無需再次許可。 資產一旦獲得組織的許可，使用權就是永久的。

組織可以整合其企業 [!DNL Adobe Stock] 計畫 [!DNL Experience Manager Assets] 確保獲得許可的資產能夠廣泛用於其創造性和市場營銷項目，同時具備強大的資產管理能力 [!DNL Experience Manager]。 [!DNL Experience Manager] 用戶可以快速查找、預覽和許可保存在中的Adobe Stock資產 [!DNL Experience Manager]，不離開 [!DNL Experience Manager] 。

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## 整合 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] 為用戶提供搜索、預覽、保存和許可的功能 [!DNL Adobe Stock] 資產 [!DNL Experience Manager]。

**必備條件**

整合需要：

* 安 [企業 [!DNL Adobe Stock] 計畫](https://stockenterprise.adobe.com/)
* 具有Admin Console到預設Stock產品配置檔案的權限的用戶
* 具有在Adobe Developer控制台中建立整合的開發人員訪問配置檔案權限的用戶

企業 [!DNL Adobe Stock] 計畫，

* 提供產品權利 [!DNL Adobe Stock] (與Experience Manager有關的股票)
* 已購買到 [!DNL Adobe Admin Console] 你的股票
* 在中啟用服務帳戶(JWT)驗證 [!DNL Adobe Developer Console] 你的股票
* 允許從內部全局管理信用和許可 [!DNL Adobe Admin Console]

在權利檔案中， [!DNL Adobe Stock] 存在於 [!DNL Admin Console]。 可以建立多個配置檔案，這些配置檔案確定哪些人可以授權Stock資產。 具有直接訪問產品配置檔案的用戶可以訪問 [https://stock.adobe.com/](https://stock.adobe.com/) 以及證券資產。 但是，還有另一種方法使用開發人員訪問建立整合(API)來驗證之間的通信 [!DNL Experience Manager] 和 [!DNL Adobe Stock]。

>[!NOTE]
>
>股票服務帳戶(JWT)驗證隨企業股票權利一起提供。
>
>整合不支援企業股票權利的Oauth身份驗證。

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## 整合步驟 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integration-steps}

整合 [!DNL Experience Manager] 和 [!DNL Adobe Stock]，按列出的順序執行以下步驟：

1. [取得公開憑證](#public-certificate)

   在 [!DNL Experience Manager]，建立IMS帳戶並生成公共證書（公鑰）。

1. [建立服務帳戶(JWT)連接](#createnewintegration)

   在 [!DNL Adobe Developer Console]，為 [!DNL Adobe Stock] 組織。 在項目下，使用公鑰配置API以建立服務帳戶(JWT)連接。 獲取服務帳戶憑據和JWT負載資訊。

1. [配置IMS帳戶](#create-ims-account-configuration)

   在 [!DNL Experience Manager]，使用服務帳戶憑據和JWT負載配置IMS帳戶。

1. [設定雲端服務](#configure-the-cloud-service)

   在 [!DNL Experience Manager]，配置 [!DNL Adobe Stock] 使用IMS帳戶的雲服務。


### 建立IMS配置 {#create-an-ims-configuration}

IMS配置驗證您的 [!DNL Experience Manager Assets] 作者實例 [!DNL Adobe Stock] 權利。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [配置IMS帳戶](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公鑰（證書）在Adobe Developer控制台中驗證您的產品配置檔案。

1. 登錄到 [!DNL Experience Manager Assets] 作者實例。 預設URL為 `http://localhost:4502/aem/start.html`。

1. 從 **[!UICONTROL 工具]** 面板，導航至 **[!UICONTROL 安全]** > **[!UICONTROL Adobe IMS配置]**。

1. 在「Adobe IMS配置」頁中，按一下 **[!UICONTROL 建立]**。 的 **[!UICONTROL Adobe IMS技術帳戶配置]** 的上界。

1. 在 **[!UICONTROL 證書]** 頁籤 **[!UICONTROL Adobe Stock]** 從 **[!UICONTROL 雲解決方案]** 下拉清單。

1. 您可以建立證書或為配置重用現有證書。

   要建立證書，請選擇 **[!UICONTROL 建立新證書]** 複選框並指定 **別名** 公鑰。 別名用作公鑰的名稱。

1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。然後，按一下 **[!UICONTROL 確定]** 生成公鑰。

1. 按一下 **[!UICONTROL 下載公鑰]** 表徵圖並將公鑰(.crt)檔案保存在電腦上。 稍後將使用公鑰為您的Brand Portal租戶配置API並在Adobe Developer控制台中生成服務帳戶憑據。

   按一下&#x200B;**[!UICONTROL 下一步]**。

   ![生成證書](assets/stock-integration-ims-account.png)

1. 在 **帳戶** 頁籤，建立需要服務帳戶憑據的Adobe IMS帳戶。

   開啟新頁籤並 [在Adobe Developer控制台中建立服務帳戶(JWT)連接](#createnewintegration)。

### 建立服務帳戶(JWT)連接 {#createnewintegration}

在Adobe Developer控制台中，項目和API在組織級別進行配置。 配置API可建立服務帳戶(JWT)連接。 通過生成密鑰對（私鑰和公鑰）或上載公鑰來配置API有兩種方法。 在此示例中，服務帳戶憑據是通過上載公鑰來生成的。

要生成服務帳戶憑據和JWT負載，請執行以下操作：

1. 以系統管理員權限登錄到Adobe Developer控制台。 預設URL為 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   確保您從下拉清單（組織）中選擇了正確的IMS組織（股票權利）。

1. 按一下 **[!UICONTROL 建立新項目]**。 系統會為您的組織建立一個空項目，其名稱為系統生成。

   按一下 **[!UICONTROL 編輯項目]**。 更新 **[!UICONTROL 項目標題]** 和 **[!UICONTROL 說明]**，然後按一下 **[!UICONTROL 保存]**。

1. 在 **[!UICONTROL 項目概述]** 按鈕 **[!UICONTROL 添加API]**。

1. 在 **[!UICONTROL 添加API窗口]**&#x200B;選中 **[!UICONTROL Adobe Stock]**。 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 在 **[!UICONTROL 配置API]** 窗口，選擇 **[!UICONTROL 服務帳戶(JWT)]** 驗證。 按一下&#x200B;**[!UICONTROL 下一步]**。

   ![建立 — jwt — 憑據](assets/aem-stock-jwt.png)

1. 按一下 **[!UICONTROL 上載公鑰]**。 按一下 **[!UICONTROL 選擇檔案]** 並上載您已在 [獲取公共證書](#public-certificate) 的子菜單。 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 驗證公鑰並按一下 **[!UICONTROL 下一個]**。

1. 選擇預設 **[!UICONTROL Adobe Stock]** 產品配置檔案，按一下 **[!UICONTROL 保存已配置的API]**。

1. 配置API後，您將重定向到「API概述」頁。 從左導航下 **[!UICONTROL 憑據]**，按一下 **[!UICONTROL 服務帳戶(JWT)]** 的雙曲餘切值。 在此，您可以查看憑據並執行操作，如生成JWT令牌、複製憑據詳細資訊和檢索客戶端密鑰。

1. 從 **[!UICONTROL 客戶端憑據]** 頁籤，複製 **[!UICONTROL 客戶端ID]**。

   按一下 **[!UICONTROL 檢索客戶端密鑰]** 複製 **[!UICONTROL 客戶端機密]**。

   ![generate-jwt憑據](assets/aem-stock-jwt-credential.png)

1. 導航到 **[!UICONTROL 生成JWT]** 頁籤並複製 **[!UICONTROL JWT負載]** 的下界。

現在，您可以使用客戶端ID（API密鑰）、客戶端密鑰和JWT負載 [配置IMS帳戶](#create-ims-account-configuration) 在 [!DNL Experience Manager Assets]。

### 配置IMS帳戶 {#create-ims-account-configuration}

您必須 [證書](#public-certificate) 和 [服務帳戶(JWT)憑據](#createnewintegration) 配置IMS帳戶。

配置IMS帳戶：

1. 開啟IMS配置並導航到 **[!UICONTROL 帳戶]** 頁籤。 你一直開啟這頁 [獲取公共證書](#public-certificate)。

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在 **[!UICONTROL 授權伺服器]** 欄位，輸入URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)。

   在 **[!UICONTROL API密鑰]** 欄位， **[!UICONTROL 客戶端密碼]**, **[!UICONTROL 負載]** （JWT負載） [建立服務帳戶(JWT)連接](#createnewintegration)。

1. 按一下&#x200B;**[!UICONTROL 建立]**。建立IMS帳戶配置。

   ![配置IMS帳戶](assets/aem-stock-ims-config.png)

1. 選擇IMS帳戶配置，然後按一下 **[!UICONTROL 檢查運行狀況]**。

   按一下 **[!UICONTROL 檢查]** 的子菜單。 成功配置時，將顯示一條消息， *已成功檢索令牌*。

   ![健康檢查](assets/aem-stock-healthcheck.png)


### 設定雲端服務 {#configure-the-cloud-service}

配置 [!DNL Adobe Stock] 雲服務：

1. 在 [!DNL Experience Manager] 用戶介面，導航 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**。

1. 在 [!DNL Adobe Stock Configurations] 的 **[!UICONTROL 建立]**。

1. 指定 **[!UICONTROL 標題]** 為雲配置。

   選擇在建立時建立的IMS配置 [配置IMS帳戶](#create-ims-account-configuration)。

   從下拉清單中選擇區域設定。

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   您 [!DNL Experience Manager Assets] 作者實例現在與 [!DNL Adobe Stock]。 可以建立多個 [!DNL Adobe Stock] 配置（例如，基於區域設定的配置）。 您現在可以訪問、搜索和許可 [!DNL Adobe Stock] 內的資產 [!DNL Experience Manager] 用戶介面。

   ![搜索庫存資產](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >在整合階段，只有管理員才能訪問 [!DNL Adobe Stock] 資產、搜索股票資產（使用全新搜索）和許可證 [!DNL Adobe Stock] 資產。
   >
   >管理員可以進一步將用戶或組添加到 [!DNL Adobe Stock] 雲服務，並授予這些非管理員用戶 [!DNL Experience Manager] 訪問「Stock（庫）」配置。

1. 要添加用戶或組，請選擇 [!DNL Adobe Stock] 雲配置，按一下 **[!UICONTROL 屬性]**。

1. 搜索以添加您已為其分配訪問Adobe Stock配置權限的用戶或組。 請參閱 [將權限分配給用戶組](#assign-permissions-to-group)。


## 為用戶組分配權限 {#assign-permissions-to-group}

管理員可以建立用戶組，並授予某些用戶或組訪問 [!DNL Adobe Stock] 雲服務。

以下是用戶搜索和許可Adobe Stock資產所需的權限：

* 配置路徑： `/conf/global/settings/stock`
* 權限: `jcr:read`
* 權限類型: `Allow`

您可以建立用戶組或將權限分配給現有用戶組。 可以從 [!DNL Experience Manager Assets] 介面或 [!DNL User Admin] 控制台。

**提供對用戶組的訪問權限 [!DNL Experience Manager]:**

1. 在 [!DNL Experience Manager] 用戶介面，導航 **[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 組]**。 建立用戶組 [!DNL Adobe Stock]。

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 權限]**。

1. 在左面板中搜索用戶組並添加新 **[!UICONTROL 訪問控制項(ACE)]** Adobe Stock。

   * 配置路徑： `/conf/global/settings/stock`
   * 權限: `jcr:read`
   * 權限類型: `Allow`

   按一下 **[!UICONTROL 添加]**。

   ![用戶權限](assets/aem-stock-user-permissions.png)

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**。 選擇 [!DNL Adobe Stock] 雲配置，按一下 **[!UICONTROL 屬性]**。

1. 將新建立的用戶組添加到 [!DNL Adobe Stock] 配置。 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   ![分配用戶](assets/aem-stock-adduser.png)

**提供對用戶的訪問 [!DNL User Admin Console]:**

1. 開啟 [!DNL Experience Manager] 用戶Admin Console。 預設URL為 `http://localhost:4502/userdamin`。

1. 在左面板中，輸入 `user_id` 或 `name`。 按兩下以開啟用戶屬性。

1. 導航到 **[!UICONTROL 權限]** 頁籤 `read` 權限 [!DNL Adobe Stock] 雲配置： `/conf/global/settings/stock`。

   >[!CAUTION]
   >
   >如果不允許雲配置，則用戶只能訪問 **[!UICONTROL 資產]** 的 [!DNL Experience Manager] 。
   >
   >允許訪問 [!UICONTROL 資產] 和 [!DNL Adobe Stock] 資產，確保允許用戶進行雲配置。

1. 按一下 **[!UICONTROL 保存]** 更新權限。

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. 將用戶或組添加到 [!DNL Adobe Stock] 雲配置。


## 訪問Adobe Stock資產 {#access-stock-assets}

具有對 [!DNL Adobe Stock] 雲配置可以搜索和許可 [!DNL Adobe Stock] 資產 [!DNL Experience Manager] 。

用戶必須執行激活該 [!DNL Adobe Stock] 訪問前配置雲 [!DNL Adobe Stock] 資產。 這是一次性活動。 如果為用戶分配了多個權限 [!DNL Adobe Stock] 雲配置，用戶可以從 **[!UICONTROL 用戶首選項]**。

激活 [!DNL Adobe Stock] 雲配置：

1. 登錄到 [!DNL Experience Manager]。

1. 按一下右上角的用戶表徵圖，然後按一下 **[!UICONTROL 我的首選項]**。 的 **[!UICONTROL 用戶首選項]** 的下界。

1. 選擇所需 **[!UICONTROL 庫存配置]** 從下拉清單中按一下 **[!UICONTROL 接受]** 來激活配置。

   ![用戶首選項](assets/aem-stock-preferences.png)

1. 導航到 **[!UICONTROL 資產]** > **[!UICONTROL Adobe Stock]**。 您現在可以查看、搜索和許可 [!DNL Adobe Stock] 資產。

下表說明了用戶權限在訪問 [!DNL Adobe Stock] 資產：

| 使用者 | 群組 | 權限 | 在用戶首選項中接受庫存配置 | 訪問資產 | 訪問Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| 管理員 | N/A | 全部 | N/A | 是 | 是 |
| test-doc1 | DAM 使用者 | /conf/global /settings/stock/cloud/config | 是 | 是 | 是 |
| test-doc1 | DAM 使用者 | /conf/global /settings/stock/cloud/config | 否 | 錯誤：無法載入資料 | 否 |
| test-doc1 | DAM 使用者 | **允許**:/conf/global /settings/stock     **拒絕**:/cloud-config | 庫存配置不可見 | 是 | 否 |


## 使用和管理 [!DNL Adobe Stock] 資產 [!DNL Experience Manager] {#usemanage}

使用此功能，組織可以允許其用戶使用 [!DNL Adobe Stock] 資產 [!DNL Experience Manager Assets]。 從 [!DNL Experience Manager] 用戶介面，用戶可搜索 [!DNL Adobe Stock] 資產和許可所需資產。

一次 [!DNL Adobe Stock] 資產在 [!DNL Experience Manager]它可以像一種典型資產那樣使用和管理。 在 [!DNL Experience Manager]用戶可以搜索和預覽資產；複製並公佈資產；分佔投資 [!DNL Brand Portal];通過 [!DNL Experience Manager] 案頭應用；等等。

![搜索 [!DNL Adobe Stock] 對您的 [!DNL Adobe Experience Manager] 工作區](assets/adobe-stock-search-results-workspace.png)

**A.**[!DNL Adobe Stock] 搜尋與已提供 ID 之資產的類似資產。**B.** 搜尋與您選取的型態或方向相符的資產。**C.** 搜尋一或多個支援的資產類型 **D.** 開啟或收合篩選器窗格 **E.** 在 中為選取的資產授權並加以儲存 [!DNL Experience Manager]**F.**[!DNL Experience Manager] 將資產儲存在 中並加上浮水印 **G.**[!DNL Adobe Stock] 在 網站上探索與選取的資產類似的資產 **H.**[!DNL Adobe Stock] 在 網站上檢視選取的資產 **I.** 搜尋結果中選取的資產數目 **J.** 在卡片檢視與清單檢視之間切換

### 查找資產 {#find-assets}

您 [!DNL Experience Manager] 用戶，可以在兩者中搜索資產， [!DNL Experience Manager] 和 [!DNL Adobe Stock]。 當搜索位置不限於 [!DNL Adobe Stock]，搜索結果 [!DNL Experience Manager] 和 [!DNL Adobe Stock] 的上界。

* 搜索 [!DNL Adobe Stock] 資產，按一下 **[!UICONTROL 導航]** > **[!UICONTROL 資產]** > **[!UICONTROL 搜索Adobe Stock]**。

* 要跨 [!DNL Adobe Stock] 和 [!DNL Experience Manager Assets]按一下「搜索」 ![搜索](assets/do-not-localize/search_icon.png)。

或者，開始鍵入 `Location: Adobe Stock` 的子菜單。 [!DNL Adobe Stock] 資產。 [!DNL Experience Manager] 提供了對搜索的資產的高級篩選功能，允許用戶使用篩選器快速零入所需的資產，如受支援資產類型、影像方向和許可狀態。

>[!NOTE]
>
>搜索的資產 [!DNL Adobe Stock] 顯示 [!DNL Experience Manager]。 [!DNL Adobe Stock] 資產被提取並儲存在 [!DNL Experience Manager] 僅在用戶 [保存資產](/help/assets/aem-assets-adobe-stock.md#saveassets) 或 [許可證和保存資產](/help/assets/aem-assets-adobe-stock.md#licenseassets)。 已儲存在 [!DNL Experience Manager] 顯示並突出顯示，以便參考和訪問。 另外， [!DNL Stock] 將資產與一些附加元資料一起保存，以將源指示為 [!DNL Stock]。

![在中搜索篩選器 [!DNL Experience Manager] 突出顯示 [!DNL Adobe Stock] 搜索結果中的資產](assets/aem-search-filters2.jpg)

### 保存並查看所需資產 {#saveassets}

選擇要保存的資產 [!DNL Experience Manager]。 按一下 [!UICONTROL 保存] 的子菜單。 未經許可的資產以水線本地保存。

下次搜索資產時，保存的資產會加亮顯示標籤，以指示此類資產在 [!DNL Experience Manager Assets]。

>[!NOTE]
>
>最近添加的資產顯示「新」徽章，而不顯示「授權」徽章。

### 許可證資產 {#licenseassets}

用戶可以許可 [!DNL Adobe Stock] 資產的額度 [!DNL Adobe Stock] 企業計畫。 當您許可某個資產時，它將不帶水印而被保存，並且可用於搜索和使用 [!DNL Experience Manager Assets]。

![用於許可和保存的對話框 [!DNL Adobe Stock] 資產 [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### 訪問元資料和資產屬性 {#access-metadata-and-asset-properties}

用戶可以訪問和預覽元資料，包括 [!DNL Adobe Stock] 在中保存的資產的元資料屬性 [!DNL Experience Manager]，然後添加 **[!UICONTROL 許可證引用]** 的下界。 但是，對許可證引用的更新未在 [!DNL Experience Manager] 和 [!DNL Adobe Stock] 的子菜單。

用戶可以查看許可和未授權資產的屬性。

![查看和訪問已保存資產的元資料和許可證引用](assets/metadata_properties.jpg)


## 已知限制 {#known-limitations}

* **與 [!DNL Experience Manager] Service Pack 6.5.7.0及更高版本**:在與整合期間發現意外問題 [!DNL Experience Manager] 6.5.7.0及以上。 該問題正在測試中，預計將在 [!DNL Experience Manager] 6.5.11.0。聯繫人 [!DNL Customer Support] 立即修復。

* **限制用戶許可的功能無法正常工作**:所有用戶 `read` 允許對庫存配置的權限搜索和許可 [!DNL Adobe Stock] 資產。

* **非管理員用戶必須手動激活 [!DNL Adobe Stock] 雲配置**:在 **[!UICONTROL 用戶首選項]** 的 **[!UICONTROL 庫存配置]** 顯示 [!DNL Adobe Stock] 雲配置已啟用，但它對非管理員用戶不起作用。 用戶必須按一下 **[!UICONTROL 接受]** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。 如果沒有此步驟，系統將在訪問時反映錯誤消息 **[!UICONTROL 資產]**。

* **未顯示編輯影像警告**:授權映像時，用戶無法檢查映像是否為「僅編輯使用」。 為防止可能的誤用，管理員可以關閉對Admin Console的編輯資產訪問。

* **顯示了錯誤的許可證類型**:可能在中顯示不正確的許可證類型 [!DNL Experience Manager] 的下界。 用戶可以登錄 [!DNL Adobe Stock] 的子菜單。

* **未同步引用欄位和元資料**:當用戶更新許可證參考欄位時，在中更新許可證參考資訊 [!DNL Experience Manager] 但不在 [!DNL Adobe Stock] 的子菜單。 同樣，如果用戶更新 [!DNL Adobe Stock] 網站，更新未同步 [!DNL Experience Manager]。

>[!MORELIKETHIS]
>
>* [使用視頻教程 [!DNL Adobe Stock] 資產 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] 企業計畫幫助](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] 常見問題集](https://helpx.adobe.com/stock/faq.html)



<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

