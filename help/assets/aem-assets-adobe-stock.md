---
title: 管理 [!DNL Adobe Stock] 資產
description: 從 [!DNL Adobe Experience Manager]內搜尋、擷取、授權及管理 [!DNL Adobe Stock] 資產。 將授權資產作為任何其他數位資產使用。
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2446'
ht-degree: 3%

---

# 在[!DNL Adobe Experience Manager Assets]中使用[!DNL Adobe Stock]個資產 {#use-adobe-stock-assets-in-aem-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-assets-adobe-stock.html?lang=en) |
| AEM 6.5 | 本文章 |

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

[!DNL Adobe Stock]服務可讓設計師和企業存取數百萬張高品質、精選且免版稅的像片、向量、插圖、影片、範本和3D資產，以供其所有創意專案使用。

根據預設，企業方案的[!DNL Adobe Stock]包含整個組織的共用許可權。 當資產獲得組織使用者的授權後，組織的其他使用者可以識別、下載和使用此資產，而無需再次授權。 一旦您的組織授權資產，其使用權利即永久有效。

組織可以整合其企業[!DNL Adobe Stock]計畫與[!DNL Experience Manager Assets]，以確保授權資產可廣泛用於其創意和行銷專案，並具備[!DNL Experience Manager]的強大資產管理功能。 [!DNL Experience Manager]使用者無需離開[!DNL Experience Manager]介面，即可快速尋找、預覽及授權[!DNL Experience Manager]中儲存的Adobe Stock資產。

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## 整合[!DNL Experience Manager]和[!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets]讓使用者能夠直接從[!DNL Experience Manager]搜尋、預覽、儲存及授權[!DNL Adobe Stock]資產。

**必備條件**

此整合需要：

* [企業 [!DNL Adobe Stock] 計畫](https://stockenterprise.adobe.com/)
* 具有預設Stock產品設定檔Admin Console許可權的使用者
* 具有開發人員存取設定檔許可權的使用者，可在Adobe Developer Console中建立整合

企業[!DNL Adobe Stock]計畫，

* 提供[!DNL Adobe Stock]的產品權益(與Experience Manager相關的庫存)
* 針對您的股票權益購買到[!DNL Adobe Admin Console]的積分
* 在[!DNL Adobe Developer Console]內為您的股票權益啟用服務帳戶(JWT)驗證
* 啟用從[!DNL Adobe Admin Console]內全域管理信用額度與授權

在權益中，[!DNL Adobe Stock]的預設產品設定檔存在於[!DNL Admin Console]中。 可建立多個設定檔，這些設定檔決定誰可以授權Stock資產。 直接存取產品設定檔的使用者可以存取[https://stock.adobe.com/](https://stock.adobe.com/)並授權Stock資產。 然而，有其他方法可使用「開發人員存取權」建立整合(API)，以驗證[!DNL Experience Manager]與[!DNL Adobe Stock]之間的通訊。

>[!NOTE]
>
>Stock服務帳戶(JWT)驗證隨附企業Stock權益。
>
>整合不支援企業股票權益的Oauth驗證。

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## 整合[!DNL Experience Manager]和[!DNL Adobe Stock]的步驟 {#integration-steps}

若要整合[!DNL Experience Manager]與[!DNL Adobe Stock]，請依照列出的順序執行下列步驟：

1. [取得公開憑證](#public-certificate)

   在[!DNL Experience Manager]中，建立IMS帳戶並產生公開憑證（公開金鑰）。

1. [建立服務帳戶(JWT)連線](#createnewintegration)

   在[!DNL Adobe Developer Console]中，為您的[!DNL Adobe Stock]組織建立專案。 在專案下，使用公開金鑰設定API以建立服務帳戶(JWT)連線。 取得服務帳戶憑證和JWT裝載資訊。

1. [設定IMS帳戶](#create-ims-account-configuration)

   在[!DNL Experience Manager]中，使用服務帳戶憑證和JWT承載設定IMS帳戶。

1. [設定雲端服務](#configure-the-cloud-service)

   在[!DNL Experience Manager]中，使用IMS帳戶設定[!DNL Adobe Stock]雲端服務。


### 建立IMS設定 {#create-an-ims-configuration}

IMS設定使用[!DNL Adobe Stock]權益驗證您的[!DNL Experience Manager Assets]作者執行個體。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [設定IMS帳戶](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開金鑰（憑證）會在Adobe Developer Console中驗證您的產品設定檔。

1. 登入您的[!DNL Experience Manager Assets]作者執行個體。 預設URL為`http://localhost:4502/aem/start.html`。

1. 從&#x200B;**[!UICONTROL 工具]**&#x200B;面板，導覽至&#x200B;**[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**。

1. 在「Adobe IMS設定」頁面中，按一下「**[!UICONTROL 建立]**」。 **[!UICONTROL Adobe IMS技術帳戶設定]**&#x200B;頁面隨即開啟。

1. 在&#x200B;**[!UICONTROL 憑證]**&#x200B;標籤中，從&#x200B;**[!UICONTROL 雲端解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Adobe Stock]**。

1. 您可以建立憑證或針對設定重複使用現有憑證。

   若要建立憑證，請選取&#x200B;**[!UICONTROL 建立新憑證]**&#x200B;核取方塊，並指定公開金鑰的&#x200B;**別名**。 別名的作用是公開金鑰的名稱。

1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。然後，按一下&#x200B;**[!UICONTROL 確定]**&#x200B;以產生公開金鑰。

1. 按一下&#x200B;**[!UICONTROL 下載公開金鑰]**&#x200B;圖示，然後將公開金鑰(.crt)檔案儲存在電腦上。 公開金鑰稍後將用於設定Brand Portal租使用者的API，以及在Adobe Developer Console中產生服務帳戶認證。

   按一下「**[!UICONTROL 下一步]**」。

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. 在&#x200B;**帳戶**&#x200B;索引標籤中，已建立需要服務帳戶認證的Adobe IMS帳戶。

   開啟新索引標籤並在Adobe Developer Console](#createnewintegration)中[建立服務帳戶(JWT)連線。

### 建立服務帳戶(JWT)連線 {#createnewintegration}

在Adobe Developer Console中，專案和API是在組織層級設定。 設定API會建立服務帳戶(JWT)連線。 有兩種方式可設定API：產生金鑰組（私密金鑰和公開金鑰）或上傳公開金鑰。 在此範例中，服務帳戶認證是透過上傳公開金鑰所產生。

若要產生服務帳戶憑證和JWT裝載：

1. 以系統管理員許可權登入Adobe Developer Console。 預設URL為[https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   確保您已從下拉式（組織）清單中選取正確的IMS組織（庫存權利）。

1. 按一下&#x200B;**[!UICONTROL 建立新專案]**。 系統會為您的組織建立名稱由系統產生的空白專案。

   按一下&#x200B;**[!UICONTROL 編輯專案]**。 更新&#x200B;**[!UICONTROL 專案標題]**&#x200B;和&#x200B;**[!UICONTROL 描述]**，然後按一下&#x200B;**[!UICONTROL 儲存]**。

1. 在&#x200B;**[!UICONTROL 專案概述]**&#x200B;索引標籤中，按一下&#x200B;**[!UICONTROL 新增API]**。

1. 在&#x200B;**[!UICONTROL 新增API視窗]**&#x200B;中，選取&#x200B;**[!UICONTROL Adobe Stock]**。 按一下「**[!UICONTROL 下一步]**」。

1. 在&#x200B;**[!UICONTROL 設定API]**&#x200B;視窗中，選取&#x200B;**[!UICONTROL 服務帳戶(JWT)]**&#x200B;驗證。 按一下「**[!UICONTROL 下一步]**」。

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. 按一下&#x200B;**[!UICONTROL 上傳您的公開金鑰]**。 按一下&#x200B;**[!UICONTROL 選取檔案]**&#x200B;並上傳您在[取得公開憑證](#public-certificate)區段中下載的公開金鑰（.crt檔案）。 按一下「**[!UICONTROL 下一步]**」。

1. 驗證公開金鑰並按一下&#x200B;**[!UICONTROL 下一步]**。

1. 選取預設&#x200B;**[!UICONTROL Adobe Stock]**&#x200B;產品設定檔，然後按一下&#x200B;**[!UICONTROL 儲存設定的API]**。

1. 設定API後，您會重新導向至API概觀頁面。 從左側導覽列中的&#x200B;**[!UICONTROL 認證]**&#x200B;下，按一下&#x200B;**[!UICONTROL 服務帳戶(JWT)]**&#x200B;選項。 在這裡，您可以檢視認證並執行產生JWT權杖、複製認證詳細資料和擷取使用者端密碼等動作。

1. 從&#x200B;**[!UICONTROL 使用者端認證]**&#x200B;索引標籤，複製&#x200B;**[!UICONTROL 使用者端識別碼]**。

   按一下&#x200B;**[!UICONTROL 擷取使用者端密碼]**&#x200B;並複製&#x200B;**[!UICONTROL 使用者端密碼]**。

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. 導覽至「**[!UICONTROL 產生JWT]**」標籤，並複製&#x200B;**[!UICONTROL JWT裝載]**&#x200B;資訊。

您現在可以使用使用者端ID （API金鑰）、使用者端密碼和JWT裝載在[!DNL Experience Manager Assets]中[設定IMS帳戶](#create-ims-account-configuration)。

### 設定IMS帳戶 {#create-ims-account-configuration}

您必須擁有[憑證](#public-certificate)和[服務帳戶(JWT)認證](#createnewintegration)，才能設定IMS帳戶。

若要設定IMS帳戶：

1. 開啟IMS設定並導覽至「**[!UICONTROL 帳戶]**」標籤。 [取得公開憑證](#public-certificate)時，您保持頁面開啟。

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在&#x200B;**[!UICONTROL 授權伺服器]**&#x200B;欄位中，輸入URL： [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)。

   在&#x200B;**[!UICONTROL API金鑰]**&#x200B;欄位、**[!UICONTROL 使用者端密碼]**&#x200B;以及您在[建立服務帳戶(JWT)連線](#createnewintegration)時所複製的&#x200B;**[!UICONTROL 裝載]** （JWT裝載）中，輸入使用者端識別碼。

1. 按一下「**[!UICONTROL 建立]**」。IMS帳戶設定已建立。

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. 選取IMS帳戶設定，然後按一下&#x200B;**[!UICONTROL 檢查健康狀態]**。

   在對話方塊中按一下&#x200B;**[!UICONTROL 核取]**。 成功設定時，會顯示訊息，顯示&#x200B;*Token已成功擷取*。

   ![健康情況檢查](assets/aem-stock-healthcheck.png)


### 設定雲端服務 {#configure-the-cloud-service}

若要設定[!DNL Adobe Stock]雲端服務：

1. 在[!DNL Experience Manager]使用者介面中，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Stock]**。

1. 在[!DNL Adobe Stock Configurations]頁面中，按一下&#x200B;**[!UICONTROL 建立]**。

1. 指定雲端設定的&#x200B;**[!UICONTROL 標題]**。

   選取您在[設定IMS帳戶](#create-ims-account-configuration)時所建立的IMS設定。

   從下拉式清單中選取您的地區設定。

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   您的[!DNL Experience Manager Assets]作者執行個體現在已與[!DNL Adobe Stock]整合。 您可以建立多個[!DNL Adobe Stock]組態（例如地區設定組態）。 您現在可以從[!DNL Experience Manager]使用者介面存取、搜尋及授權[!DNL Adobe Stock]資產。

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >在此整合階段，只有管理員可以存取[!DNL Adobe Stock]資產、搜尋Stock資產（使用Omnisearch），以及授權[!DNL Adobe Stock]資產。
   >
   >管理員可以進一步將使用者或群組新增至[!DNL Adobe Stock]雲端服務，並在[!DNL Experience Manager]中授予這些非管理員使用者存取Stock設定的許可權。

1. 若要新增使用者或群組，請選取[!DNL Adobe Stock]雲端設定，然後按一下&#x200B;**[!UICONTROL 屬性]**。

1. 搜尋以新增您已指派許可權來存取Adobe Stock設定的使用者或群組。 請參閱[將許可權指派給使用者群組](#assign-permissions-to-group)。


## 指派許可權給使用者群組 {#assign-permissions-to-group}

管理員可以建立使用者群組，並將許可權授予特定使用者或群組以存取[!DNL Adobe Stock]雲端服務。

以下是使用者搜尋和授權Adobe Stock資產所需的許可權：

* 設定路徑： `/conf/global/settings/stock`
* 許可權： `jcr:read`
* 許可權型別： `Allow`

您可以建立使用者群組或指派許可權給現有的使用者群組。 可從[!DNL Experience Manager Assets]介面或[!DNL User Admin]主控台指派許可權。

**若要從[!DNL Experience Manager]提供使用者群組的存取權：**

1. 在[!DNL Experience Manager]使用者介面中，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 群組]**。 建立[!DNL Adobe Stock]的使用者群組。

1. 瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 許可權]**。

1. 在左側面板中搜尋使用者群組，並為Adobe Stock新增新的&#x200B;**[!UICONTROL 存取控制專案(ACE)]**。

   * 設定路徑： `/conf/global/settings/stock`
   * 許可權： `jcr:read`
   * 許可權型別： `Allow`

   按一下&#x200B;**[!UICONTROL 新增]**。

   ![使用者許可權](assets/aem-stock-user-permissions.png)

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Stock]**。 選取[!DNL Adobe Stock]雲端設定，然後按一下&#x200B;**[!UICONTROL 屬性]**。

1. 將新建立的使用者群組新增至[!DNL Adobe Stock]設定。 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。

   ![指派使用者](assets/aem-stock-adduser.png)

**若要提供存取權給來自[!DNL User Admin Console]的使用者：**

1. 開啟[!DNL Experience Manager]使用者Admin Console。 預設URL為`http://localhost:4502/userdamin`。

1. 在左側面板中，輸入`user_id`或`name`來搜尋使用者。 按兩下以開啟使用者屬性。

1. 瀏覽至&#x200B;**[!UICONTROL 許可權]**&#x200B;索引標籤，並允許[!DNL Adobe Stock]雲端設定的`read`許可權： `/conf/global/settings/stock`。

   >[!CAUTION]
   >
   >如果不允許雲端設定，則使用者只能在[!DNL Experience Manager]介面中存取&#x200B;**[!UICONTROL Assets]**。
   >
   >若要允許存取[!UICONTROL Assets]和[!DNL Adobe Stock]資產，請確定使用者允許雲端設定。

1. 按一下[儲存]以更新許可權。****

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. 將使用者或群組新增至[!DNL Adobe Stock]雲端設定。


## 存取Adobe Stock資產 {#access-stock-assets}

擁有[!DNL Adobe Stock]雲端設定許可權的非管理員使用者可以從[!DNL Experience Manager]介面搜尋及授權[!DNL Adobe Stock]資產。

使用者在存取[!DNL Adobe Stock]個資產之前，必須執行啟用[!DNL Adobe Stock]雲端設定的額外步驟。 這是單次活動。 如果使用者在多個[!DNL Adobe Stock]雲端設定上被指派許可權，則使用者可以從&#x200B;**[!UICONTROL 使用者偏好設定]**&#x200B;中選取所需的設定。

若要啟用[!DNL Adobe Stock]雲端設定：

1. 登入[!DNL Experience Manager]。

1. 從右上角按一下使用者圖示，然後按一下&#x200B;**[!UICONTROL 我的偏好設定]**。 **[!UICONTROL 使用者偏好設定]**&#x200B;視窗隨即開啟。

1. 從下拉式清單中選取所需的&#x200B;**[!UICONTROL Stock組態]**，然後按一下&#x200B;**[!UICONTROL 接受]**&#x200B;以啟動組態。

   ![使用者偏好設定](assets/aem-stock-preferences.png)

1. 導覽至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**。 您現在可以檢視、搜尋及授權[!DNL Adobe Stock]資產。

下表說明存取[!DNL Adobe Stock]資產時使用者許可權的運作方式：

| 使用者 | 群組 | 權限 | 接受使用者偏好設定中的Stock設定 | 存取Assets | 存取Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| 管理員 | 不適用 | 全部 | 不適用 | 是 | 是 |
| test-doc1 | DAM 使用者 | /conf/global /settings/stock/cloud-config | 是 | 是 | 是 |
| test-doc1 | DAM 使用者 | /conf/global /settings/stock/cloud-config | 否 | 錯誤：無法載入資料 | 否 |
| test-doc1 | DAM 使用者 | **允許**： /conf/global /settings/stock     **拒絕**： /cloud-config | Stock設定不可見 | 是 | 否 |


## 使用和管理[!DNL Experience Manager]中的[!DNL Adobe Stock]資產 {#usemanage}

使用此功能，組織可以允許其使用者使用[!DNL Experience Manager Assets]中的[!DNL Adobe Stock]個資產進行工作。 在[!DNL Experience Manager]使用者介面中，使用者可以搜尋[!DNL Adobe Stock]資產並授權必要的資產。

在[!DNL Experience Manager]中授權[!DNL Adobe Stock]資產後，就可以像一般資產一樣使用和管理它。 在[!DNL Experience Manager]中，使用者可以搜尋及預覽資產；複製及發佈資產；在[!DNL Brand Portal]上共用資產；透過[!DNL Experience Manager]案頭應用程式存取及使用資產，以此類推。

![搜尋[!DNL Adobe Stock]資產，並從[!DNL Adobe Experience Manager]工作區篩選結果](assets/adobe-stock-search-results-workspace.png)

**A.**&#x200B;搜尋與已提供[!DNL Adobe Stock] ID之資產的類似資產。 **B.** 搜尋與您選取的型態或方向相符的資產。**C.**&#x200B;搜尋一或多個支援的資產型別&#x200B;**D.**&#x200B;開啟或收合篩選器窗格&#x200B;**E.**&#x200B;授權並將選取的資產儲存在[!DNL Experience Manager] **F.**&#x200B;將資產儲存在[!DNL Experience Manager]中（含浮水印&#x200B;**G.**）探索[!DNL Adobe Stock]網站上與選取的資產類似的資產&#x200B;**H.**&#x200B;在[!DNL Adobe Stock]網站&#x200B;**I.**&#x200B;上檢視&#x200B;**網站上選取的資產從搜尋結果選取的資產數目** J。 19}在卡片檢視和清單檢視之間切換

### 尋找資產 {#find-assets}

您的[!DNL Experience Manager]使用者可以在[!DNL Experience Manager]和[!DNL Adobe Stock]中搜尋資產。 當搜尋位置不限於[!DNL Adobe Stock]時，會顯示來自[!DNL Experience Manager]和[!DNL Adobe Stock]的搜尋結果。

* 若要搜尋[!DNL Adobe Stock]資產，請按一下&#x200B;**[!UICONTROL 導覽]** > **[!UICONTROL Assets]** > **[!UICONTROL 搜尋Adobe Stock]**。

* 若要搜尋[!DNL Adobe Stock]與[!DNL Experience Manager Assets]之間的資產，請按一下搜尋![搜尋](assets/do-not-localize/search_icon.png)。

或者，開始在搜尋列中輸入`Location: Adobe Stock`以選取[!DNL Adobe Stock]資產。 [!DNL Experience Manager]針對搜尋的資產提供進階篩選功能，讓使用者能夠使用篩選器快速鎖定所需的資產，例如支援的資產型別、影像方向和授權狀態。

>[!NOTE]
>
>從[!DNL Adobe Stock]搜尋的Assets會顯示在[!DNL Experience Manager]中。 [!DNL Adobe Stock]資產只有在使用者[儲存資產](/help/assets/aem-assets-adobe-stock.md#saveassets)或[授權並儲存資產](/help/assets/aem-assets-adobe-stock.md#licenseassets)之後，才會擷取並儲存在[!DNL Experience Manager]存放庫中。 已儲存在[!DNL Experience Manager]中的Assets會顯示並反白顯示，以方便參考和存取。 此外，[!DNL Stock]資產會與一些額外的中繼資料一起儲存，以將來源指示為[!DNL Stock]。

![在[!DNL Experience Manager]中搜尋篩選器，並在搜尋結果中反白顯示[!DNL Adobe Stock]個資產](assets/aem-search-filters2.jpg)

### 儲存並檢視必要的資產 {#saveassets}

選取您要儲存於[!DNL Experience Manager]的資產。 按一下頂端工具列中的[!UICONTROL 儲存]，並提供資產的名稱和位置。 未授權資產會使用浮水印儲存在本機。

下次當您搜尋資產時，儲存的資產會以徽章強調顯示，以表示這些資產可在[!DNL Experience Manager Assets]中使用。

>[!NOTE]
>
>最近新增的資產會顯示新徽章，而非授權徽章。

### 授權資產 {#licenseassets}

使用者可以使用其[!DNL Adobe Stock]企業計畫的配額來授權[!DNL Adobe Stock]資產。 當您授權資產時，儲存時不會加上浮水印，且可在[!DNL Experience Manager Assets]中搜尋和使用。

![在[!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)中授權及儲存[!DNL Adobe Stock]個資產的對話方塊


### 存取中繼資料和資產屬性 {#access-metadata-and-asset-properties}

使用者可以存取及預覽中繼資料，包括儲存在[!DNL Experience Manager]中之資產的[!DNL Adobe Stock]中繼資料屬性，以及新增資產的&#x200B;**[!UICONTROL 授權參考]**。 但是，[!DNL Experience Manager]與[!DNL Adobe Stock]網站之間未同步授權參考的更新。

使用者可以看到已授權和未授權資產的屬性。

![檢視及存取已儲存資產的中繼資料和授權參考](assets/metadata_properties.jpg)


## 已知限制 {#known-limitations}

* **與[!DNL Experience Manager] Service Pack 6.5.7.0和以上版本整合時發生的問題**：在與[!DNL Experience Manager] 6.5.7.0和以上版本整合期間發現未預期的問題。 此問題正在測試中，預計可在[!DNL Experience Manager] 6.5.11.0中使用。連絡[!DNL Customer Support]以取得立即的Hotfix。

* **限制使用者授權的功能無法正常運作**：所有具有Stock設定`read`許可權的使用者都可以搜尋及授權[!DNL Adobe Stock]資產。

* **非管理員使用者必須手動啟用[!DNL Adobe Stock]雲端設定**：在&#x200B;**[!UICONTROL 使用者偏好設定]**&#x200B;視窗中，**[!UICONTROL Stock設定]**&#x200B;會將[!DNL Adobe Stock]雲端設定顯示為已啟用，但無法用於非管理員使用者。 使用者必須按一下&#x200B;**[!UICONTROL 接受]**&#x200B;按鈕才能啟用Stock設定。 如果沒有此步驟，系統會在存取&#x200B;**[!UICONTROL Assets]**&#x200B;時反映錯誤訊息。

* **未顯示編輯影像警告**：授權影像時，使用者無法檢查影像是否僅限編輯使用。 為防止可能的誤用，管理員可以從Admin Console關閉編輯資產的存取權。

* **顯示的授權型別錯誤**：資產的[!DNL Experience Manager]可能顯示不正確的授權型別。 使用者可以登入[!DNL Adobe Stock]網站以檢視授權型別。

* **參考欄位和中繼資料未同步**：當使用者更新授權參考欄位時，授權參考資訊會在[!DNL Experience Manager]中更新，但不會在[!DNL Adobe Stock]網站上更新。 同樣地，如果使用者更新[!DNL Adobe Stock]網站上的參考欄位，則更新不會在[!DNL Experience Manager]中同步。

>[!MORELIKETHIS]
>
>* [有關搭配使用 [!DNL Adobe Stock] 資產與 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)的教學影片
>* [[!DNL Adobe Stock] 企業計畫說明](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
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

