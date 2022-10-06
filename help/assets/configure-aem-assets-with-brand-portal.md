---
title: 使用 Brand Portal 設定 AEM Assets
seo-title: Configure AEM Assets with Brand Portal
description: 了解如何使用Brand Portal設定AEM Assets，以將資產和集合發佈至Brand Portal。
seo-description: Learn how to configure AEM Assets with Brand Portal for publishing assets and Collections to Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 8%

---

# 使用 Brand Portal 設定 AEM Assets {#configure-integration-65}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=zh-Hant) |

Adobe Experience Manager Assets Brand Portal可讓您將已核准的品牌資產從Adobe Experience Manager Assets發佈至Brand Portal，並分發給Brand Portal使用者。

AEM Assets是透過Adobe Developer Console使用Brand Portal來設定，其會擷取AdobeIdentity Management服務(IMS)帳戶代號，以便授權Brand Portal租用戶。

>[!NOTE]
>
>AEM 6.5.4.0及更新版本支援透過Adobe Developer Console使用Brand Portal設定AEM Assets。
>
>過去，Brand Portal是透過舊版OAuth閘道設定，該閘道使用JSON網頁代號(JWT)交換來取得IMS存取代號以進行授權。
>
>2020年4月6日起，不再支援透過舊版OAuth閘道進行設定，且已變更為Adobe Developer Console。

>[!TIP]
>
>***僅適用於現有客戶***
>
>建議您繼續使用現有的舊版OAuth閘道設定。 如果您遇到舊版OAuth閘道設定的問題，請刪除現有設定，並透過Adobe Developer Console建立新設定。

本說明說明下列兩個使用案例：

* [新配置](#configure-new-integration-65):如果您是新的Brand Portal使用者，且想使用Brand Portal設定您的AEM Assets製作例項，可以透過Adobe Developer Console建立設定。
* [升級配置](#upgrade-integration-65):如果您是現有Brand Portal使用者，且在舊版OAuth閘道上設定，請刪除現有設定，並透過Adobe Developer主控台建立新設定。

提供的資訊基於以下假設：閱讀本幫助的任何人都熟悉以下技術：

* 安裝、設定和管理Adobe Experience Manager和AEM套件。

* 使用Linux和Microsoft Windows作業系統。

## 必備條件 {#prerequisites}

您需要下列項目才能使用 Brand Portal 設定 AEM Assets：

* 具有最新Service Pack且正在執行的AEM Assets作者例項
* Brand Portal租用戶URL
* 在Brand Portal租用戶的IMS組織上具有系統管理員權限的使用者

[下載並安裝AEM 6.5](#aemquickstart)

[下載並安裝最新的AEM Service Pack](#servicepack)

### 下載並安裝AEM 6.5 {#aemquickstart}

建議您讓AEM 6.5設定AEM製作例項。 如果您沒有AEM啟動並執行，請從下列位置下載：

* 如果您是現有AEM客戶，請從下載AEM 6.5 [Adobe授權網站](https://licensing.adobe.com).

* 如果您是Adobe合作夥伴，請使用 [Adobe合作夥伴培訓計畫](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) 請求AEM 6.5。

下載AEM後，如需設定AEM製作例項的指示，請參閱 [部署和維護](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### 下載及安裝AEM最新Service Pack {#servicepack}

有關詳細說明，請參閱

* [AEM 6.5 Service Pack發行說明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**聯絡支援** 如果您找不到最新的AEM套件或Service Pack。

## 建立設定 {#configure-new-integration-65}

使用Brand Portal設定AEM Assets需要在AEM Assets製作執行個體和Adobe Developer主控台中進行設定。

1. 在AEM Assets中，建立IMS帳戶並產生公開憑證（公開金鑰）。
1. 在Adobe Developer Console中，為您的Brand Portal租用戶（組織）建立專案。
1. 在專案下，使用公開金鑰設定API以建立服務帳戶(JWT)連線。
1. 取得服務帳戶憑證和JWT裝載資訊。
1. 在AEM Assets中，使用服務帳戶憑證和JWT裝載來設定IMS帳戶。
1. 在AEM Assets中，使用IMS帳戶和Brand Portal端點（組織URL）來設定Brand Portal雲端服務。
1. 將資產從AEM Assets發佈至Brand Portal，以測試您的設定。

>[!NOTE]
>
>AEM Assets製作例項只能設定一個Brand Portal租用戶。

如果您是第一次使用Brand Portal設定AEM Assets，請依所列順序執行下列步驟：
1. [取得公開憑證](#public-certificate)
1. [建立服務帳戶(JWT)連線](#createnewintegration)
1. [設定IMS帳戶](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)
1. [測試設定](#test-integration)

### 建立 IMS 設定 {#create-ims-configuration}

IMS設定會以Brand Portal租用戶驗證您的AEM Assets製作例項。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [設定IMS帳戶](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開金鑰（憑證）在Adobe Developer Console上驗證您的設定檔。

1. 登入您的AEM Assets製作例項。 預設URL為 `http://localhost:4502/aem/start.html`.

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導覽至 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**.

1. 在Adobe IMS設定頁面中，按一下 **[!UICONTROL 建立]**. 它會重新導向至 **[!UICONTROL Adobe IMS技術帳戶設定]** 頁面。 依預設， **憑證** 標籤。

1. 選擇 **[!UICONTROL AdobeBrand Portal]** 在 **[!UICONTROL 雲端解決方案]** 下拉式清單。

1. 選取 **[!UICONTROL 建立新憑證]** 核取方塊並指定 **別名** 公開金鑰。 別名用作公鑰的名稱。

1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。然後，按一下 **[!UICONTROL 確定]** 來產生公開金鑰。

   ![建立憑證](assets/ims-config2.png)

1. 按一下 **[!UICONTROL 下載公開金鑰]** 圖示並將公開金鑰(.crt)檔案儲存在電腦上。

   公開金鑰稍後將用於設定Brand Portal租用戶的API，以及在Adobe Developer Console中產生服務帳戶憑證。

   ![下載憑證](assets/ims-config3.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   在 **帳戶** 標籤，系統會建立Adobe IMS帳戶，而此帳戶需要在Adobe Developer Console中產生的服務帳戶憑證。 暫時保持此頁面開啟。

   開啟新標籤，然後 [在Adobe Developer主控台中建立服務帳戶(JWT)連線](#createnewintegration) 取得用於設定IMS帳戶的憑證和JWT裝載。

### 建立服務帳戶(JWT)連線 {#createnewintegration}

在Adobe Developer Console中，專案和API是在Brand Portal租用戶（組織）層級設定。 設定API會建立服務帳戶(JWT)連線。 有兩種方法可用來設定API，方法是產生金鑰組（私密和公開金鑰）或上傳公開金鑰。 若要使用Brand Portal設定AEM Assets，您必須在AEM Assets中產生公開金鑰（憑證），並透過上傳公開金鑰在Adobe Developer Console中建立憑證。 您必須具備這些憑證才能在AEM Assets中設定IMS帳戶。 設定IMS帳戶後，您就可以在AEM Assets中設定Brand Portal雲端服務。

執行下列步驟以產生服務帳戶憑證和JWT裝載：

1. 以IMS組織(Brand Portal租用戶)的系統管理員權限登入Adobe Developer Console。 預設URL為 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >確認您已從右上角的下拉式清單（組織）中選取正確的IMS組織(Brand Portal租用戶)。

1. 按一下 **[!UICONTROL 建立新專案]**. 系統會為您的組織建立一個空白專案，其名稱為系統產生。

   按一下 **[!UICONTROL 編輯專案]** 更新 **[!UICONTROL 專案標題]** 和 **[!UICONTROL 說明]**，然後按一下 **[!UICONTROL 儲存]**.

1. 在 **[!UICONTROL 專案概述]** 按一下 **[!UICONTROL 新增API]**.

1. 在 **[!UICONTROL 新增API視窗]**，選取 **[!UICONTROL AEM Brand Portal]** 按一下 **[!UICONTROL 下一個]**.

   確定您擁有AEM Brand Portal服務的存取權。

1. 在 **[!UICONTROL 設定API]** 按一下 **[!UICONTROL 上傳您的公開金鑰]**. 然後，按一下 **[!UICONTROL 選取檔案]** 並上傳您在 [取得公開憑證](#public-certificate) 區段。

   按一下&#x200B;**[!UICONTROL 下一步]**。

   ![上傳公開金鑰](assets/service-account3.png)

1. 驗證公開金鑰並按一下 **[!UICONTROL 下一個]**.

1. 選擇 **[!UICONTROL Assets Brand Portal]** 作為預設產品設定檔，然後按一下 **[!UICONTROL 儲存已設定的API]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![選取產品設定檔](assets/service-account4.png)

1. 設定API後，系統會將您重新導向至API概觀頁面。 從下方的左側導覽 **[!UICONTROL 憑證]**，按一下 **[!UICONTROL 服務帳戶(JWT)]** 選項。

   >[!NOTE]
   >
   >您可以檢視憑證並執行下列動作：產生JWT代號、複製憑證詳細資訊、擷取用戶端密碼等。

1. 從 **[!UICONTROL 客戶端憑據]** 頁簽，複製 **[!UICONTROL 用戶端ID]**.

   按一下 **[!UICONTROL 擷取用戶端密碼]** 並複製 **[!UICONTROL 用戶密碼]**.

   ![服務帳戶憑據](assets/service-account5.png)

1. 導覽至 **[!UICONTROL 產生JWT]** 標籤並複製 **[!UICONTROL JWT裝載]** 資訊。

您現在可以將用戶端ID（API金鑰）、用戶端密碼和JWT裝載，用於 [設定IMS帳戶](#create-ims-account-configuration) 在AEM Assets。

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe I/O Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.
-->

### 設定IMS帳戶 {#create-ims-account-configuration}

請確認您已執行下列步驟：

* [取得公開憑證](#public-certificate)
* [建立服務帳戶(JWT)連線](#createnewintegration)

執行下列步驟來設定IMS帳戶。

1. 開啟IMS設定並導覽至 **[!UICONTROL 帳戶]** 標籤。 您在 [取得公開憑證](#public-certificate).

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在 **[!UICONTROL 授權伺服器]** 欄位，指定URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   在 **[!UICONTROL API金鑰]** 欄位， **[!UICONTROL 用戶端密碼]**，和 **[!UICONTROL 裝載]** （JWT裝載），而您 [建立服務帳戶(JWT)連線](#createnewintegration).

   按一下&#x200B;**[!UICONTROL 建立]**。

   已設定IMS帳戶。

   ![IMS 帳戶設定](assets/create-new-integration6.png)

1. 選取IMS帳戶設定，然後按一下 **[!UICONTROL 檢查運行狀況]**.

   按一下 **[!UICONTROL 檢查]** 框中輸入URL。 成功設定時，畫面會顯示訊息，指出 *已成功檢索令牌*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一個IMS設定。
>
>確認IMS設定通過健康狀況檢查。 如果配置未通過運行狀況檢查，則無效。 您必須刪除它，然後建立新的有效配置。

### 設定雲端服務 {#configure-the-cloud-service}

執行下列步驟以設定Brand Portal雲端服務：

1. 登入您的AEM Assets製作例項。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導覽至 **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. 在Brand Portal設定頁面中，按一下 **[!UICONTROL 建立]**.

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選取您在 [設定IMS帳戶](#create-ims-account-configuration).

   在 **[!UICONTROL 服務URL]** 欄位中，指定您的Brand Portal租用戶（組織）URL。

   ![](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。雲端設定此時已建立。

   您的AEM Assets作者例項現在已以Brand Portal租用戶設定。

### 測試設定 {#test-integration}

執行下列步驟驗證設定：

1. 登入您的AEM Assets雲端例項。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導覽至 **[!UICONTROL 部署]** > **[!UICONTROL 復寫]**.

   ![](assets/test-integration1.png)

1. 在「復寫」頁面中，按一下 **[!UICONTROL 作者代理]**.

   ![](assets/test-integration2.png)

   您可以看到為您的Brand Portal租用戶建立的四個復寫代理。

   找出Brand Portal租用戶的復寫代理，然後按一下復寫代理URL。

   ![](assets/test-integration3.png)

   >[!NOTE]
   >
   >復寫代理並行工作，並平等共用作業分配，從而將發佈速度提高了原始速度的四倍。 設定雲端服務後，若要啟用依預設啟動的復寫代理，以啟用多個資產的平行發佈，則不需要額外設定。

1. 若要驗證AEM Assets與Brand Portal之間的連線，請按一下 **[!UICONTROL 測試連線]** 表徵圖。

   ![](assets/test-integration4.png)

   系統會顯示訊息，指出您的 *已成功傳遞測試包*.

   ![](assets/test-integration5.png)

1. 驗證所有四個複製代理上的測試結果。


   >[!NOTE]
   >
   >請避免停用任何復寫代理，因為這可能導致資產復寫（在佇列中執行）失敗。
   >
   >請確定所有四個復寫代理均已設定，以避免逾時錯誤。 請參閱 [疑難排解平行發佈至Brand Portal的問題](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).
   >
   >請勿修改任何自動產生的設定。

您現在可以：

* [從 AEM Assets 發佈資產到 Brand Portal](../assets/brand-portal-publish-assets.md)
* [從Brand Portal發佈資產至AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) -Brand Portal的Asset Sourcing
* [從 AEM Assets 發佈資料夾到 Brand Portal](../assets/brand-portal-publish-folder.md)
* [從 AEM Assets 發佈集合到 Brand Portal](../assets/brand-portal-publish-collection.md)
* [將預設集、結構和 Facet 發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

請參閱 [Brand Portal檔案](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 以取得更多資訊。


## 升級配置 {#upgrade-integration-65}

依所列順序執行下列步驟，將現有設定升級至Adobe Developer Console:
1. [驗證正在運行的作業](#verify-jobs)
1. [刪除現有配置](#delete-existing-configuration)
1. [建立設定](#configure-new-integration-65)

### 驗證正在運行的作業 {#verify-jobs}

進行任何修改之前，請確定您的AEM Assets製作執行個體上未執行任何發佈工作。 為此，您可以驗證所有四個複製代理上活動作業的狀態，並確保隊列處於空閒狀態。

1. 登入您的AEM Assets製作例項。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導覽至 **[!UICONTROL 部署]** > **[!UICONTROL 部署複製]**.

1. 在「復寫」頁面中，按一下 **[!UICONTROL 作者代理]**.

   ![](assets/test-integration2.png)

1. 找出您Brand Portal租用戶的復寫代理。

   確保 **隊列空閒** 對於所有復寫代理，沒有任何發佈作業處於活動狀態。

   ![](assets/test-integration3.png)

### 刪除現有配置 {#delete-existing-configuration}

刪除現有配置時，必須運行以下檢查清單：
* 刪除所有四個複製代理
* 刪除Brand Portal雲端服務
* 刪除MAC使用者

1. 登入您的AEM Assets製作執行個體，並以管理員身分開啟CRX Lite。 預設URL為 `http://localhost:4502/crx/de/index.jsp`.

1. 導覽至 `/etc/replications/agents.author` 並刪除您Brand Portal租用戶的所有四個復寫代理。

   ![](assets/delete-replication-agent.png)

1. 導覽至 `/etc/cloudservices/mediaportal` 和刪除Brand Portal雲端服務設定。

   ![](assets/delete-cloud-service.png)

1. 導覽至 `/home/users/mac` 和刪除 **Mac使用者** 你的Brand Portal租戶。

   ![](assets/delete-mac-user.png)


您現在可以 [建立配置](#configure-new-integration-65) 透過Adobe Developer Console在AEM 6.5製作例項上執行。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
