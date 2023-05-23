---
title: 使用 Brand Portal 設定 AEM Assets
seo-title: Configure AEM Assets with Brand Portal
description: 瞭解如何將AEM Assets與Brand Portal配置為向Brand Portal發佈資產和收藏。
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
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2076'
ht-degree: 8%

---

# 使用 Brand Portal 設定 AEM Assets {#configure-integration-65}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=zh-Hant) |
| AEM 6.5 | 本文 |

Adobe Experience Manager Assets Brand Portal允許您將批准的品牌資產從Adobe Experience Manager資產發佈到Brand Portal，並分發給Brand Portal用戶。

AEM Assets通過Adobe Developer控制台配置Brand Portal，該控制台為Brand Portal租戶的授權採購AdobeIdentity Management服務(IMS)帳戶令牌。

>[!NOTE]
>
>通過AEM Assets控制台在6.5.4.0及更高版本上AEM支援配置Brand Portal。
>
>此前，Brand Portal通過舊式OAuth網關進行配置，該網關使用JSON Web令牌(JWT)交換來獲取IMS訪問令牌以進行授權。
>
>從2020年4月6日起不再支援通過舊式OAuth網關進行配置，並將其更改為Adobe Developer控制台。

>[!TIP]
>
>***僅適用於現有客戶***
>
>建議繼續使用現有的舊式OAuth網關配置。 在舊式OAuth網關配置中遇到問題時，請刪除現有配置並通過Adobe Developer控制台建立新配置。

本幫助描述以下兩種使用情形：

* [新配置](#configure-new-integration-65):如果您是新的Brand Portal用戶，並想在Brand Portal上配置您的AEM Assets作者實例，則可以通過Adobe Developer控制台建立配置。
* [升級配置](#upgrade-integration-65):如果您是現有的Brand Portal用戶，在舊式OAuth網關上進行配置，請刪除現有配置，並通過Adobe Developer控制台建立新配置。

所提供的資訊基於以下假設：任何閱讀本幫助的人都熟悉以下技術：

* 安裝、配置和管理Adobe Experience Manager和AEM包。

* 使用Linux和MicrosoftWindows作業系統。

## 必備條件 {#prerequisites}

您需要下列項目才能使用 Brand Portal 設定 AEM Assets：

* 具有最新Service Pack的正在運行的AEM Assets作者實例
* Brand Portal租戶URL
* 對Brand Portal租戶的IMS組織具有系統管理員權限的用戶

[下載並安裝AEM6.5](#aemquickstart)

[下載並安裝最新AEM的Service Pack](#servicepack)

### 下載並安裝AEM6.5 {#aemquickstart}

建議使AEM用6.5設定作AEM者實例。 如果沒有啟動和AEM運行，請從以下位置下載它：

* 如果您是現有客AEM戶，請從AEM下載6.5 [Adobe許可網站](https://licensing.adobe.com)。

* 如果您是Adobe合作夥伴，請使用 [Adobe合作夥伴培訓計畫](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) 請求AEM6.5

下載後AEM，有關設定作者實例的說AEM明，請參見 [部署和維護](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install)。

### 下載並安裝最AEM新的Service Pack {#servicepack}

有關詳細說明，請參見

* [《 AEM 6.5 Service Pack發行說明》](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**聯繫支援** 找不到最新包或AEMService Pack。

## 建立設定 {#configure-new-integration-65}

將AEM Assets配置為Brand Portal需要兩種配置：AEM Assets作者實例和Adobe Developer控制台。

1. 在AEM Assets，建立IMS帳戶並生成公共證書（公鑰）。
1. 在Adobe Developer控制台中，為您的Brand Portal租戶（組織）建立項目。
1. 在項目下，使用公鑰配置API以建立服務帳戶(JWT)連接。
1. 獲取服務帳戶憑據和JWT負載資訊。
1. 在AEM Assets，使用服務帳戶憑據和JWT負載配置IMS帳戶。
1. 在AEM Assets，使用IMS帳戶和Brand Portal端點（組織URL）配置Brand Portal雲服務。
1. Test配置，將資產從AEM Assets發佈到Brand Portal。

>[!NOTE]
>
>AEM Assets的作者實例只能配置一個Brand Portal租戶。

如果您首次將AEM Assets配置為Brand Portal，請按列出的順序執行以下步驟：
1. [取得公開憑證](#public-certificate)
1. [建立服務帳戶(JWT)連接](#createnewintegration)
1. [配置IMS帳戶](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)
1. [測試設定](#test-integration)

### 建立 IMS 設定 {#create-ims-configuration}

IMS配置向Brand Portal租戶驗證您的AEM Assets作者實例。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [配置IMS帳戶](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公鑰（證書）在Adobe Developer控制台上驗證您的配置檔案。

1. 登錄到您的AEM Assets作者實例。 預設URL為 `http://localhost:4502/aem/start.html`。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導航至 **[!UICONTROL 安全]** > **[!UICONTROL Adobe IMS配置]**。

1. 在「Adobe IMS配置」頁中，按一下 **[!UICONTROL 建立]**。 它將重定向到 **[!UICONTROL Adobe IMS技術帳戶配置]** 的子菜單。 預設情況下， **證書** 的子菜單。

1. 選擇 **[!UICONTROL AdobeBrand Portal]** 的 **[!UICONTROL 雲解決方案]** 下拉清單。

1. 選擇 **[!UICONTROL 建立新證書]** 複選框並指定 **別名** 公鑰。 別名用作公鑰的名稱。

1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。然後，按一下 **[!UICONTROL 確定]** 生成公鑰。

   ![建立憑證](assets/ims-config2.png)

1. 按一下 **[!UICONTROL 下載公鑰]** 表徵圖並將公鑰(.crt)檔案保存在電腦上。

   公鑰稍後將用於為您的Brand Portal租戶配置API並在Adobe Developer控制台中生成服務帳戶憑據。

   ![下載憑證](assets/ims-config3.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   在 **帳戶** 頁籤，建立Adobe IMS帳戶，它需要在Adobe Developer控制台中生成的服務帳戶憑據。 暫時保持此頁面開啟。

   開啟新頁籤並 [在Adobe Developer控制台中建立服務帳戶(JWT)連接](#createnewintegration) 獲取用於配置IMS帳戶的憑據和JWT負載。

### 建立服務帳戶(JWT)連接 {#createnewintegration}

在Adobe Developer控制台中，項目和API在Brand Portal租戶（組織）級別配置。 配置API可建立服務帳戶(JWT)連接。 通過生成密鑰對（私鑰和公鑰）或上載公鑰來配置API有兩種方法。 要將AEM Assets配置為Brand Portal，必須在AEM Assets中生成公鑰（證書），並通過上載公鑰在Adobe Developer控制台中建立憑據。 配置AEM Assets的IMS帳戶需要這些憑據。 一旦配置了IMS帳戶，您就可以在AEM Assets配置Brand Portal雲服務。

執行以下步驟以生成服務帳戶憑據和JWT負載：

1. 使用IMS組織(Brand Portal租戶)的系統管理員權限登錄到Adobe Developer控制台。 預設URL為 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   >[!NOTE]
   >
   >確保從右上角的下拉（組織）清單中選擇了正確的IMS組織(Brand Portal租戶)。

1. 按一下 **[!UICONTROL 建立新項目]**。 系統會為您的組織建立一個空項目，其名稱為系統生成。

   按一下 **[!UICONTROL 編輯項目]** 更新 **[!UICONTROL 項目標題]** 和 **[!UICONTROL 說明]**，然後按一下 **[!UICONTROL 保存]**。

1. 在 **[!UICONTROL 項目概述]** 按鈕 **[!UICONTROL 添加API]**。

1. 在 **[!UICONTROL 添加API窗口]**&#x200B;選中 **[!UICONTROL AEM Brand Portal]** 按一下 **[!UICONTROL 下一個]**。

   確保您有權訪問AEM Brand Portal服務。

1. 在 **[!UICONTROL 配置API]** 窗口，按一下 **[!UICONTROL 上載公鑰]**。 然後，按一下 **[!UICONTROL 選擇檔案]** 並上載您已在 [獲取公共證書](#public-certificate) 的子菜單。

   按一下&#x200B;**[!UICONTROL 下一步]**。

   ![上載公鑰](assets/service-account3.png)

1. 驗證公鑰並按一下 **[!UICONTROL 下一個]**。

1. 選擇 **[!UICONTROL Assets Brand Portal]** 作為預設產品配置檔案，然後按一下 **[!UICONTROL 保存已配置的API]**。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![選擇產品配置檔案](assets/service-account4.png)

1. 配置API後，您將重定向到「API概述」頁。 從左導航下 **[!UICONTROL 憑據]**，按一下 **[!UICONTROL 服務帳戶(JWT)]** 的雙曲餘切值。

   >[!NOTE]
   >
   >您可以查看憑據並執行諸如生成JWT令牌、複製憑據詳細資訊、檢索客戶端機密等操作。

1. 從 **[!UICONTROL 客戶端憑據]** 頁籤，複製 **[!UICONTROL 客戶端ID]**。

   按一下 **[!UICONTROL 檢索客戶端密鑰]** 複製 **[!UICONTROL 客戶端機密]**。

   ![服務帳戶憑據](assets/service-account5.png)

1. 導航到 **[!UICONTROL 生成JWT]** 頁籤並複製 **[!UICONTROL JWT負載]** 的下界。

現在，您可以使用客戶端ID（API密鑰）、客戶端密鑰和JWT負載 [配置IMS帳戶](#create-ims-account-configuration) 在AEM Assets。

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

### 配置IMS帳戶 {#create-ims-account-configuration}

請確認您已執行下列步驟：

* [取得公開憑證](#public-certificate)
* [建立服務帳戶(JWT)連接](#createnewintegration)

執行以下步驟來配置IMS帳戶。

1. 開啟IMS配置並導航到 **[!UICONTROL 帳戶]** 頁籤。 你一直開啟這頁 [獲取公共證書](#public-certificate)。

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在 **[!UICONTROL 授權伺服器]** 欄位，指定URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)。

   在 **[!UICONTROL API密鑰]** 欄位， **[!UICONTROL 客戶端密碼]**, **[!UICONTROL 負載]** （JWT負載） [建立服務帳戶(JWT)連接](#createnewintegration)。

   按一下&#x200B;**[!UICONTROL 建立]**。

   已配置IMS帳戶。

   ![IMS 帳戶設定](assets/create-new-integration6.png)

1. 選擇IMS帳戶配置，然後按一下 **[!UICONTROL 檢查運行狀況]**。

   按一下 **[!UICONTROL 檢查]** 的子菜單。 成功配置時，將顯示一條消息， *已成功檢索令牌*。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您必須只有一個IMS配置。
>
>確保IMS配置通過運行狀況檢查。 如果配置未通過運行狀況檢查，則該配置無效。 必須刪除它並建立新的有效配置。

### 設定雲端服務 {#configure-the-cloud-service}

執行以下步驟來配置Brand Portal雲服務：

1. 登錄到您的AEM Assets作者實例。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導航至 **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**。

1. 在「Brand Portal配置」頁中，按一下 **[!UICONTROL 建立]**。

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選擇在建立時建立的IMS配置 [配置IMS帳戶](#create-ims-account-configuration)。

   在 **[!UICONTROL 服務URL]** 欄位，指定您的Brand Portal租戶（組織）URL。

   ![](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。雲端設定此時已建立。

   您的AEM Assets作者實例現在已與Brand Portal租戶配置。

### 測試設定 {#test-integration}

執行以下步驟驗證配置：

1. 登錄到您的AEM Assets雲實例。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導航至 **[!UICONTROL 部署]** > **[!UICONTROL 複製]**。

   ![](assets/test-integration1.png)

1. 在「複製」頁中，按一下 **[!UICONTROL 作者代理]**。

   ![](assets/test-integration2.png)

   您可以看到為您的Brand Portal租戶建立的四個複製代理。

   找到您的Brand Portal租戶的複製代理，然後按一下複製代理URL。

   ![](assets/test-integration3.png)

   >[!NOTE]
   >
   >複製代理並行工作，並平等共用作業分配，從而將發佈速度提高了原始速度的四倍。 配置雲服務後，無需進行其他配置即可啟用預設激活的複製代理，以啟用多個資產的並行發佈。

1. 要驗證AEM Assets和Brand Portal之間的連接，請按一下 **[!UICONTROL Test連接]** 表徵圖

   ![](assets/test-integration4.png)

   出現一條消息， *test包已成功交付*。

   ![](assets/test-integration5.png)

1. 驗證所有四個複製代理的test結果。


   >[!NOTE]
   >
   >避免禁用任何複製代理，因為它可能導致資產的複製（在隊列中運行）失敗。
   >
   >確保將所有四個複製代理配置為避免超時錯誤。 請參閱 [排除與Brand Portal並行發佈的問題](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout)。
   >
   >不要修改任何自動生成的設定。

您現在可以：

* [從 AEM Assets 發佈資產到 Brand Portal](../assets/brand-portal-publish-assets.md)
* [發佈從Brand Portal到AEM Assets的資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) -Brand Portal資產來源補充
* [從 AEM Assets 發佈資料夾到 Brand Portal](../assets/brand-portal-publish-folder.md)
* [從 AEM Assets 發佈集合到 Brand Portal](../assets/brand-portal-publish-collection.md)
* [將預設集、結構和 Facet 發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

請參閱 [Brand Portal文檔](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 的子菜單。


## 升級配置 {#upgrade-integration-65}

按列出的順序執行以下步驟，將現有配置升級到Adobe Developer控制台：
1. [驗證正在運行的作業](#verify-jobs)
1. [刪除現有配置](#delete-existing-configuration)
1. [建立設定](#configure-new-integration-65)

### 驗證正在運行的作業 {#verify-jobs}

在進行任何修改之前，請確保在您的AEM Assets作者實例上沒有運行發佈作業。 為此，您可以驗證所有四個複製代理上活動作業的狀態，並確保隊列處於空閒狀態。

1. 登錄到您的AEM Assets作者實例。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導航至 **[!UICONTROL 部署]** > **[!UICONTROL 部署複製]**。

1. 在「複製」頁中，按一下 **[!UICONTROL 作者代理]**。

   ![](assets/test-integration2.png)

1. 找到您的Brand Portal租戶的複製代理。

   確保 **隊列空閒** 對於所有複製代理，沒有發佈作業處於活動狀態。

   ![](assets/test-integration3.png)

### 刪除現有配置 {#delete-existing-configuration}

刪除現有配置時，必須運行以下核對清單：
* 刪除所有四個複製代理
* 刪除Brand Portal雲服務
* 刪除MAC用戶

1. 以管理員身份登錄到AEM Assets作者實例並開啟CRX Lite。 預設URL為 `http://localhost:4502/crx/de/index.jsp`。

1. 導航到 `/etc/replications/agents.author` 並刪除您的Brand Portal租戶的所有四個複製代理。

   ![](assets/delete-replication-agent.png)

1. 導航到 `/etc/cloudservices/mediaportal` 刪除Brand Portal雲服務配置。

   ![](assets/delete-cloud-service.png)

1. 導航到 `/home/users/mac` 刪除 **Mac用戶** 你Brand Portal的房客。

   ![](assets/delete-mac-user.png)


你現在可以 [建立配置](#configure-new-integration-65) 通過Adobe Developer控制台AEM的6.5作者實例。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
