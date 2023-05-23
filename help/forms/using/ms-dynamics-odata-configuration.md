---
title: MicrosoftDynamics OData配置
seo-title: Microsoft Dynamics ODtata configuration
description: 通過表單資料模型利用、整合和與線上和內部部署的MicrosoftDynamics服務進行協作。
seo-description: Learn how to leverage integrate and work with online and on-premises Microsoft Dynamics services through form data model.
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# MicrosoftDynamics OData配置{#microsoft-dynamics-odata-configuration}

![資料整合](assets/data-integeration.png)

Microsoft動態公司是一種客戶關係管理(CRM)和企業資源規劃(ERP)軟體，它為建立和管理客戶帳戶、聯繫人、銷售線索、機會和案例提供企業解決方案。 [AEM Forms資料整合](../../forms/using/data-integration.md) 提供OData雲服務配置，以將Forms與線上和內部部署的MicrosoftDynamics伺服器整合。 它使您能夠基於在MicrosoftDynamics服務中定義的實體、屬性和服務建立表單資料模型。 表單資料模型可用於建立與MicrosoftDynamics伺服器交互的自適應表單以啟用業務工作流。 例如：

* 查詢MicrosoftDynamics伺服器以獲取資料並預填充自適應表單
* 在自適應表單提交上將資料寫入MicrosoftDynamics
* 通過表單資料模型中定義的自定義實體在MicrosoftDynamics中寫入資料，反之亦然

AEM Forms附加產品包還包括參考OData配置，您可以利用這些配置快速將Microsoft動力與AEM Forms整合。

安裝軟體包後，您的AEM Forms實例上可以使用以下實體和服務：

* MS Dynamics ODataCloud Service（OData服務）
* 使用預配置的MicrosoftDynamics實體和服務形成資料模型。

只有將實例的運行模式設定為，預配置的MicrosoftDynamics表單資料模型中的實體和服務才可在AEM Forms實例AEM上使用 `samplecontent` （預設）。 MS Dynamics ODataCloud Service（OData服務）也可用於其他運行模式。 有關為實例配置運行模式的詳細信AEM息，請參見 [運行模式](/help/sites-deploying/configure-runmodes.md)。

## 必備條件 {#prerequisites}

在開始設定和配置Microsoft動態之前，請確保：

* 已安裝 [AEM Forms附加包](../../forms/using/installing-configuring-aem-forms-osgi.md)
* 已聯機配置MicrosoftDynamics 365，或已安裝下列MicrosoftDynamics版本之一的實例：

   * MicrosoftDynamics 365內部裝備
   * Microsoft2016年動力

* [已在MicrosoftAzure Active Directory中註冊MicrosoftDynamics聯機服務的應用程式](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)。 記下註冊服務的客戶端ID（也稱為應用程式ID）和客戶端機密的值。 在 [為您的MicrosoftDynamics服務配置雲服務](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service)。

## 為已註冊的MicrosoftDynamics應用程式設定答復URL {#set-reply-url-for-registered-microsoft-dynamics-application}

請執行以下操作來設定已註冊的MicrosoftDynamics應用程式的回復URL:

>[!NOTE]
>
>僅在將AEM Forms與聯機MicrosoftDynamics伺服器整合時使用此過程。

1. 轉到MicrosoftAzure Active Directory帳戶，並在中添加以下雲服務配置URL **答復URL** 註冊應用程式的設定：

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目錄](assets/azure_directory_new.png)

1. 儲存設定。

## 為IFD配置Microsoft動態 {#configure-microsoft-dynamics-for-ifd}

MicrosoftDynamics使用基於聲明的身份驗證為外部用戶提供對MicrosoftDynamics CRM伺服器上資料的訪問。 要啟用此功能，請執行以下操作來配置面向Internet的部署(IFD)的MicrosoftDynamics並配置聲明設定。

>[!NOTE]
>
>僅在將AEM Forms與內部部署的MicrosoftDynamics伺服器整合時使用此過程。

1. 配置IFD的MicrosoftDynamics內部實例，如中所述 [為Microsoft動態配置IFD](https://technet.microsoft.com/en-us/library/dn609803.aspx)。
1. 使用Windows PowerShell運行以下命令，以配置啟用IFD的MicrosoftDynamics上的聲明設定：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   請參閱 [CRM本地(IFD)的應用程式註冊](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 的雙曲餘切值。

## 在AD FS電腦上配置OAuth客戶端 {#configure-oauth-client-on-ad-fs-machine}

執行以下操作以在Active Directory聯合身份驗證服務(AD FS)電腦上註冊OAuth客戶端並授予對AD FS電腦的訪問權限：

>[!NOTE]
>
>僅在將AEM Forms與內部部署的MicrosoftDynamics伺服器整合時使用此過程。

1. 運行以下命令：

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是可以使用任何GUID生成器生成的客戶端ID。
   * `redirect-uri` 是MicrosoftDynamics OData雲服務在AEM Forms的URL。 隨AEM Forms包一起安裝的預設雲服務部署在以下URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 運行以下命令以授予對AD FS電腦的訪問權限：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是Microsoft動態組織URL。

1. Microsoft動態採用HTTPS協定。 要從Forms伺服器調用AD FS終結點，請使用 `keytool` 命令。

## 為您的MicrosoftDynamics服務配置雲服務 {#configure-cloud-service-for-your-microsoft-dynamics-service}

的 **MS Dynamics ODataCloud Service（OData服務）** 配置附帶預設OData配置。 要將其配置為與MicrosoftDynamics服務連接，請執行以下操作。

1. 導航到 **[!UICONTROL 工具>Cloud Services>資料源]**，然後按一下 `global` 配置資料夾。
1. 選擇 **MS Dynamics ODataCloud Service（OData服務）** 配置和分路 **[!UICONTROL 屬性]**。 將開啟雲服務配置屬性對話框。

   在 **驗證設定** 頁籤：

   1. 輸入 **服務根** 的子菜單。 轉至Dynamics實例並導航至 **開發人員資源** 查看「服務根」欄位的值。 例如，https://&lt;tenant-name>/api/data/v9.1

   1. 替換 **客戶端ID**(亦稱： **應用程式ID**) **客戶端密碼**。 **OAuth URL**。 **刷新標籤URL**。 **訪問令牌URL**, **資源** 包含來自您的MicrosoftDynamics服務配置的值的欄位。 必須在 **資源** 欄位，以使用窗體資料模型配置MicrosoftDynamics。 使用服務根URL可導出動態實例URL。 比如說， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/)。

   1. 指定 **openid** 的 **授權範圍** 用於Microsoft動力的授權過程。

   ![驗證設定](assets/dynamics_authentication_settings_new.png)

1. 按一下 **[!UICONTROL 連接到OAuth]**。 您被重定向到「Microsoft動態」登錄頁。
1. 使用您的MicrosoftDynamics憑據登錄並接受，以允許雲服務配置連接到MicrosoftDynamics服務。 建立雲服務與服務之間的連接是一次性的任務。

   然後，您將重定向到雲服務配置頁，該頁顯示OData配置已成功保存的消息。

MS Dynamics ODataCloud Service（OData服務）雲服務已配置並與您的Dynamics服務連接。

## 建立表單資料模型 {#create-form-data-model}

當你安裝AEM Forms軟體包時，**MicrosoftFDM**，已部署在實例AEM上。 預設情況下，表單資料模型使用在MS Dynamics ODataCloud Service（OData服務）中配置的MicrosoftDynamics服務作為其資料源。

首次開啟表單資料模型時，它會連接到已配置的MicrosoftDynamics服務，並從您的MicrosoftDynamics實例中提取實體。 Microsoft動力的「聯繫人」和「潛在客戶」實體已在表單資料模型中添加。

要查看表單資料模型，請轉到 **[!UICONTROL Forms>資料整合]**。 選擇 **MicrosoftFDM** 按一下 **編輯** 以編輯模式開啟窗體資料模型。 或者，可以直接從以下URL開啟表單資料模型：

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![預設fdm-1](assets/default-fdm-1.png)

接下來，您可以基於表單資料模型建立自適應表單，並在各種自適應表單使用情形中使用它，例如：

* 通過從MicrosoftDynamics實體和服務查詢資訊來預填自適應表單
* 使用自適應表單規則調用在表單資料模型中定義的MicrosoftDynamics伺服器操作
* 將提交的表單資料寫入MicrosoftDynamics實體

建議建立隨AEM Forms軟體包提供的表單資料模型副本，並配置資料模型和服務以滿足您的要求。 它將確保將來對軟體包的任何更新不會覆蓋您的表單資料模型。

有關在業務工作流中建立和使用表單資料模型的詳細資訊，請參閱 [資料整合](../../forms/using/data-integration.md)。
