---
title: 使用 Brand Portal 設定 AEM Assets
seo-title: 使用 Brand Portal 設定 AEM Assets
description: 瞭解如何使用品牌入口網站設定AEM資產，以便將資產和系列發佈至品牌入口網站。
seo-description: 瞭解如何使用品牌入口網站設定AEM資產，以便將資產和系列發佈至品牌入口網站。
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 8%

---


# 使用 Brand Portal 設定 AEM Assets {#configure-integration-65}

Adobe Experience Manager Assets Brand Portal可讓您從Adobe Experience Manager Assets將經核准的品牌資產發佈至品牌入口網站，並將其分發給品牌入口網站使用者。

AEM Assets已透過Adobe Developer Console設定品牌入口網站，該網站會購買Adobe Identity Management Services(IMS)帳戶Token以授權品牌入口網站租用戶。

>[!NOTE]
>
>AEM 6.5.4.0及更新版本支援透過Adobe Developer Console以品牌入口網站設定AEM資產。
>
>之前，品牌入口網站是透過舊版OAuth閘道來設定，該閘道使用JSON Web Token(JWT)交換來取得IMS存取Token以進行授權。
>
>從2020年4月6日起，不再支援透過舊版OAuth閘道進行的設定，並變更為Adobe Developer Console。

>[!TIP]
>
>***僅限現有客戶***
>
>建議您繼續使用現有的舊版OAuth閘道設定。 萬一您遇到舊版OAuth閘道設定的問題，請刪除現有的設定，並透過Adobe Developer Console建立新的設定。

本說明說明下列兩個使用案例：

* [新配置](#configure-new-integration-65):如果您是新的品牌入口網站使用者，並想要使用品牌入口網站設定您的AEM Assets作者例項，您可以透過Adobe Developer Console建立設定。
* [升級配置](#upgrade-integration-65):如果您是現有的品牌入口網站使用者，在舊版OAuth閘道上有設定，請刪除現有的設定，並透過Adobe Developer Console建立新的設定。

提供的資訊基於以下假設：閱讀本「說明」的人熟悉下列技術：

* 安裝、設定和管理Adobe Experience Manager和AEM套件。

* 使用Linux和Microsoft Windows作業系統。

## 必備條件 {#prerequisites}

您需要下列項目才能使用 Brand Portal 設定 AEM Assets：

* 具有最新Service Pack的啟動和執行AEM Assets作者實例
* 品牌入口網站租用戶URL
* 對品牌入口網站的IMS組織具有系統管理員權限的使用者

[下載並安裝AEM 6.5](#aemquickstart)

[下載並安裝最新的AEM Service Pack](#servicepack)

### 下載並安裝AEM 6.5 {#aemquickstart}

建議您讓AEM 6.5來設定AEM作者例項。 如果您沒有啟動並執行AEM，請從下列位置下載：

* 如果您是現有的AEM客戶，請從[Adobe授權網站](http://licensing.adobe.com)下載AEM 6.5。

* 如果您是Adobe合作夥伴，請使用[Adobe合作夥伴培訓計畫](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q)來申請AEM 6.5。

下載AEM後，如需設定AEM作者例項的指示，請參閱[部署與維護](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/deploy.html#default-local-install)。

### 下載並安裝AEM最新的Service Pack {#servicepack}

如需詳細指示，請參閱

* [AEM 6.5 Service Pack發行說明](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**若您** 找不到最新的AEM套件或Service Pack，請聯絡「支援」。

## 建立設定 {#configure-new-integration-65}

使用品牌入口網站設定AEM資產需要同時在AEM Assets作者實例和Adobe Developer Console中進行設定。

1. 在AEM Assets中，建立IMS帳戶並產生公用憑證（公用金鑰）。
1. 在Adobe Developer Console中，為您的品牌入口網站租用戶（組織）建立專案。
1. 在專案下，使用公開金鑰來設定API，以建立服務帳戶(JWT)連線。
1. 獲取服務帳戶憑據和JWT裝載資訊。
1. 在AEM Assets中，使用服務帳戶認證和JWT裝載來設定IMS帳戶。
1. 在AEM Assets中，使用IMS帳戶和品牌入口端端點（組織URL）來設定品牌入口網站雲端服務。
1. 將資產從AEM Assets發佈至品牌入口網站，以測試您的設定。

>[!NOTE]
>
>AEM Assets作者實例僅應設定一個品牌入口網站租戶。

如果您是第一次使用品牌入口網站設定AEM資產，請在所列順序中執行下列步驟：
1. [取得公開憑證](#public-certificate)
1. [建立服務帳戶(JWT)連接](#createnewintegration)
1. [設定IMS帳戶](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)
1. [測試設定](#test-integration)

### 建立 IMS 設定 {#create-ims-configuration}

IMS設定會向品牌入口網站租用戶驗證您的AEM Assets作者實例。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [設定IMS帳戶](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開金鑰（憑證）會在Adobe Developer Console上驗證您的個人檔案。

1. 登入您的AEM Assets作者實例。 預設URL為`http://localhost:4502/aem/start.html`。

1. 從&#x200B;**工具**![工具](assets/do-not-localize/tools.png)面板，導覽至&#x200B;**[!UICONTROL 安全]** > **[!UICONTROL Adobe IMS設定]**。

1. 在「Adobe IMS設定」頁面中，按一下「**[!UICONTROL 建立]**」。 它會重新導向至&#x200B;**[!UICONTROL Adobe IMS技術帳戶設定]**&#x200B;頁面。 預設情況下，**Certificate**&#x200B;頁籤開啟。

1. 在&#x200B;**[!UICONTROL 雲端解決方案]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL Adobe品牌入口網站]**。

1. 選擇「建立新證書」複選框，並為公鑰指定&#x200B;**[!UICONTROL 別名]**。 ****&#x200B;別名用作公共密鑰的名稱。

1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。然後，按一下&#x200B;**[!UICONTROL OK]**&#x200B;以生成公鑰。

   ![建立憑證](assets/ims-config2.png)

1. 按一下「下載公開金鑰」圖示，並將公開金鑰(.crt)檔案儲存在您的電腦上。****

   公開金鑰稍後將用於為您的品牌入口網站租用戶設定API，並在Adobe Developer Console中產生服務帳戶認證。

   ![下載憑證](assets/ims-config3.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**Account**&#x200B;標籤中，會建立Adobe IMS帳戶，此帳戶需要Adobe Developer Console中產生的服務帳戶認證。 暫時保持此頁面開啟。

   在Adobe Developer Console[中開啟新標籤並建立服務帳戶(JWT)連線，以取得用於設定IMS帳戶的認證和JWT裝載。](#createnewintegration)

### 建立服務帳戶(JWT)連接{#createnewintegration}

在Adobe Developer Console中，專案和API是在品牌入口網站租用戶（組織）層級設定。 配置API會建立服務帳戶(JWT)連接。 有兩種方法可用來設定API：產生金鑰對（私用和公開金鑰）或上傳公開金鑰。 若要使用品牌入口網站設定AEM資產，您必須在AEM資產中產生公開金鑰（憑證），並透過上傳公開金鑰在Adobe Developer Console中建立認證。 在AEM資產中設定IMS帳戶時，需要這些認證。 在設定IMS帳戶後，您就可以在AEM Assets中設定品牌入口網站雲端服務。

執行以下步驟以生成服務帳戶憑據和JWT裝載：

1. 以IMS組織（品牌入口網站租用戶）的系統管理員權限登入Adobe Developer Console。 預設URL為[https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   >[!NOTE]
   >
   >請確定您已從右上角的下拉式（組織）清單中選取正確的IMS組織（品牌入口網站租用戶）。

1. 按一下&#x200B;**[!UICONTROL 建立新項目]**。 系統會為您的組織建立空白專案，其名稱由系統產生。

   按一下&#x200B;**[!UICONTROL 編輯項目]**&#x200B;以更新&#x200B;**[!UICONTROL 項目標題]**&#x200B;和&#x200B;**[!UICONTROL 說明]**，然後按一下&#x200B;**[!UICONTROL 保存]**。

1. 在&#x200B;**[!UICONTROL Project overview]**&#x200B;標籤中，按一下&#x200B;**[!UICONTROL Add API]**。

1. 在&#x200B;**[!UICONTROL 新增API視窗]**&#x200B;中，選取&#x200B;**[!UICONTROL AEM品牌入口網站]**，然後按一下&#x200B;**[!UICONTROL Next]**。

   請確定您擁有AEM品牌入口網站服務的存取權。

1. 在&#x200B;**[!UICONTROL 配置API]**&#x200B;窗口中，按一下&#x200B;**[!UICONTROL 上傳公開密鑰]**。 然後，按一下「**[!UICONTROL 選擇檔案]**」並上傳您在[獲取公共證書](#public-certificate)部分中下載的公開密鑰（.crt檔案）。

   按一下&#x200B;**[!UICONTROL 下一步]**。

   ![上傳公開金鑰](assets/service-account3.png)

1. 驗證公鑰，然後按一下&#x200B;**[!UICONTROL Next]**。

1. 選擇&#x200B;**[!UICONTROL Assets Brand Portal]**&#x200B;作為預設產品配置檔案，然後按一下&#x200B;**[!UICONTROL Save configured API]**。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![選擇產品設定檔](assets/service-account4.png)

1. 一旦設定API後，就會將您重新導向至API概觀頁面。 在&#x200B;**[!UICONTROL Credentials]**&#x200B;下的左側導航中，按一下&#x200B;**[!UICONTROL 服務帳戶(JWT)]**&#x200B;選項。

   >[!NOTE]
   >
   >您可以查看憑據並執行諸如生成JWT Token、複製憑據詳細資訊、檢索客戶機密碼等操作。

1. 從&#x200B;**[!UICONTROL 客戶端憑據]**&#x200B;頁籤複製&#x200B;**[!UICONTROL 客戶端ID]**。

   按一下「檢索客戶機密碼」**[!UICONTROL 並複製**[!UICONTROL &#x200B;客戶機密碼&#x200B;]**。]**

   ![服務帳戶認證](assets/service-account5.png)

1. 導航至「生成JWT ]**」頁籤並複製**[!UICONTROL  JWT Payload ]**資訊。**[!UICONTROL 

您現在可以使用用戶端ID（API金鑰）、用戶端密碼和JWT裝載至[，在AEM資產中設定IMS帳戶](#create-ims-account-configuration)。

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

### 設定IMS帳戶{#create-ims-account-configuration}

請確認您已執行下列步驟：

* [取得公開憑證](#public-certificate)
* [建立服務帳戶(JWT)連接](#createnewintegration)

執行下列步驟以設定IMS帳戶。

1. 開啟IMS設定並導覽至&#x200B;**[!UICONTROL Account]**&#x200B;標籤。 在[取得公共憑證時，您會保持頁面開啟。](#public-certificate)

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在&#x200B;**[!UICONTROL 授權伺服器]**&#x200B;欄位中，指定URL:[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)。

   在[建立服務帳戶(JWT)連線](#createnewintegration)時，在&#x200B;**[!UICONTROL API金鑰]**&#x200B;欄位、**[!UICONTROL 客戶機密碼]**&#x200B;和&#x200B;**[!UICONTROL Payload]**（JWT有效載荷）中指定您複製的用戶端ID。

   按一下&#x200B;**[!UICONTROL 建立]**。

   已設定IMS帳戶。

   ![IMS 帳戶設定](assets/create-new-integration6.png)

1. 選擇IMS帳戶配置，然後按一下&#x200B;**[!UICONTROL 檢查運行狀況]**。

   在對話框中按一下「**[!UICONTROL 檢查]**」。 成功配置時，將顯示一條消息，表示&#x200B;*Token已成功檢索*。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一個IMS設定。
>
>確保IMS配置通過健康檢查。 如果配置未通過健康檢查，則無效。 您必須刪除它並建立新的有效設定。

### 設定雲端服務 {#configure-the-cloud-service}

執行下列步驟以設定品牌入口網站雲端服務：

1. 登入您的AEM Assets作者實例。

1. 從&#x200B;**工具** ![工具](assets/do-not-localize/tools.png)面板，導覽至&#x200B;**[!UICONTROL 雲端服務]** > **[!UICONTROL AEM品牌入口網站]**。

1. 在「品牌入口網站設定」頁面中，按一下「建立&#x200B;**[!UICONTROL 」。]**

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選擇您在[設定IMS帳戶](#create-ims-account-configuration)時建立的IMS設定。

   在&#x200B;**[!UICONTROL 服務URL]**&#x200B;欄位中，指定您的品牌入口網站租用戶（組織）URL。

   ![](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。雲端設定此時已建立。

   您的AEM Assets作者例項現在已設定為品牌入口網站租用戶。

### 測試設定 {#test-integration}

執行以下步驟以驗證配置：

1. 登入您的AEM Assets雲端例項。

1. 從&#x200B;**工具**![工具](assets/do-not-localize/tools.png)面板，導航至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 複製]**。

   ![](assets/test-integration1.png)

1. 在「複製」頁中，按一下&#x200B;**[!UICONTROL 作者上的代理]**。

   ![](assets/test-integration2.png)

   您可以看到為您的品牌門戶租用戶建立的四個複製代理。

   找到您的Brand Portal租用戶的複製代理，然後按一下複製代理URL。

   ![](assets/test-integration3.png)

   >[!NOTE]
   >
   >複製代理並行工作，共用作業分配，使發佈速度提高了原始速度的四倍。 在設定雲端服務後，不需要額外的設定，就可啟用依預設啟用的複製代理，以啟用多個資產的並行發佈。

1. 若要驗證AEM Assets和品牌入口網站之間的連線，請按一下&#x200B;**[!UICONTROL Test Connection]**&#x200B;圖示。

   ![](assets/test-integration4.png)

   出現一條消息，表示&#x200B;*測試包已成功交付*。

   ![](assets/test-integration5.png)

1. 驗證所有四個複製代理上的測試結果。


   >[!NOTE]
   >
   >請避免禁用任何複製代理，因為它可能導致資產的複製（在隊列中運行）失敗。
   >
   >確保所有4個複製代理都配置為避免超時錯誤。 請參閱[疑難排解並行發佈至品牌入口網站的問題。](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout)

您現在可以：

* [從 AEM Assets 發佈資產到 Brand Portal](../assets/brand-portal-publish-assets.md)
* [將資產從品牌入口網站發佈至AEM資產](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) -品牌入口網站中的資產來源補充
* [從 AEM Assets 發佈資料夾到 Brand Portal](../assets/brand-portal-publish-folder.md)
* [從 AEM Assets 發佈集合到 Brand Portal](../assets/brand-portal-publish-collection.md)
* [將預設集、結構和 Facet 發佈至 Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [將標記發佈至 Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

如需詳細資訊，請參閱[品牌入口網站檔案](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html)。


## 升級配置{#upgrade-integration-65}

請依所列順序執行下列步驟，將您現有的組態升級至Adobe Developer Console:
1. [驗證正在運行的作業](#verify-jobs)
1. [刪除現有配置](#delete-existing-configuration)
1. [建立設定](#configure-new-integration-65)

### 驗證正在運行的作業{#verify-jobs}

在您進行任何修改之前，請確定您的AEM Assets作者實例上沒有執行任何發佈工作。 為此，您可以驗證所有四個複製代理上活動作業的狀態，並確保隊列處於空閒狀態。

1. 登入您的AEM Assets作者實例。

1. 從&#x200B;**工具**![工具](assets/do-not-localize/tools.png)面板，導航至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 部署複製]**。

1. 在「複製」頁中，按一下&#x200B;**[!UICONTROL 作者上的代理]**。

   ![](assets/test-integration2.png)

1. 找到您品牌門戶租用戶的複製代理。

   確保所有複製代理的&#x200B;**隊列都為Idle** ，則未激活發佈作業。

   ![](assets/test-integration3.png)

### 刪除現有配置{#delete-existing-configuration}

刪除現有配置時，必須運行以下檢查清單：
* 刪除所有四個複製代理
* 刪除品牌入口網站雲端服務
* 刪除MAC用戶

1. 登入您的AEM Assets作者例項，並以管理員身分開啟CRX Lite。 預設URL為`http://localhost:4502/crx/de/index.jsp`。

1. 導覽至`/etc/replications/agents.author`並刪除您品牌入口網站租用戶的所有4個複製代理。

   ![](assets/delete-replication-agent.png)

1. 導覽至`/etc/cloudservices/mediaportal`並刪除品牌入口網站雲端服務設定。

   ![](assets/delete-cloud-service.png)

1. 導覽至`/home/users/mac`並刪除您品牌入口網站的&#x200B;**MAC使用者**。

   ![](assets/delete-mac-user.png)


您現在可以透過AEM 6.5作者例項上的Adobe Developer Console,[建立configuration](#configure-new-integration-65)。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


