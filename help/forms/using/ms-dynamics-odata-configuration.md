---
title: Microsoft Dynamics OData配置
seo-title: Microsoft Dynamics ODtata配置
description: 通過表單資料模型利用、整合和使用線上和本地Microsoft Dynamics服務。
seo-description: 了解如何通過表單資料模型利用整合和與線上和內部部署的Microsoft Dynamics服務。
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: 表單資料模型
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 0%

---

# Microsoft Dynamics OData配置{#microsoft-dynamics-odata-configuration}

![資料整合](assets/data-integeration.png)

Microsoft Dynamics是一種客戶關係管理(CRM)和企業資源規劃(ERP)軟體，它提供企業解決方案，用於建立和管理客戶帳戶、聯繫人、銷售機會、銷售機會和案例。 [AEM Forms Data ](../../forms/using/data-integration.md) Integration提供OData雲服務配置，以將Forms與線上和內部部署的Microsoft Dynamics伺服器整合。它可讓您根據Microsoft Dynamics服務中定義的實體、屬性和服務來建立表單資料模型。 表單資料模型可用於建立與Microsoft Dynamics伺服器互動的最適化表單，以啟用業務工作流程。 例如：

* 查詢Microsoft Dynamics伺服器以取得資料並預先填入最適化表單
* 在最適化表單提交時將資料寫入Microsoft Dynamics
* 透過表單資料模型中定義的自訂實體在Microsoft Dynamics中寫入資料，反之亦然

AEM Forms附加元件套件也包含參考OData設定，您可利用此設定來快速整合Microsoft Dynamics與AEM Forms。

安裝套件時，您的AEM Forms執行個體上會提供下列實體和服務：

* MS Dynamics ODataCloud Service（OData服務）
* 表單資料模型，帶有預配置的Microsoft Dynamics實體和服務。

只有在AEM執行個體的執行模式設為`samplecontent`（預設）時，表單資料模型中預先設定的Microsoft Dynamics實體和服務才可在您的AEM Forms執行個體上使用。 MS Dynamics ODataCloud Service（OData服務）也可與其他運行模式一起使用。 有關為AEM實例配置運行模式的詳細資訊，請參閱[運行模式](/help/sites-deploying/configure-runmodes.md)。

## 必備條件 {#prerequisites}

開始設定和配置Microsoft Dynamics之前，請確保您具備：

* 已安裝[AEM Forms附加元件套件](../../forms/using/installing-configuring-aem-forms-osgi.md)
* 已聯機配置Microsoft Dynamics 365，或安裝以下Microsoft Dynamics版本之一的實例：

   * 內部部署的Microsoft Dynamics 365
   * 內部部署的Microsoft Dynamics 2016

* [已使用Microsoft Azure Active Directory註冊Microsoft Dynamics聯機服務應用程式](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)。記下註冊服務的用戶端ID（也稱為應用程式ID）和用戶端密碼的值。 這些值在[為您的Microsoft Dynamics服務](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service)配置雲服務時使用。

## 為已註冊的Microsoft Dynamics應用程式{#set-reply-url-for-registered-microsoft-dynamics-application}設定回復URL

請執行以下操作來設定已註冊的Microsoft Dynamics應用程式的回復URL:

>[!NOTE]
>
>只有在將AEM Forms與線上Microsoft Dynamics伺服器整合時，才使用此程式。

1. 轉到Microsoft Azure Active Directory帳戶，並在註冊應用程式的&#x200B;**回復URL**&#x200B;設定中添加以下雲服務配置URL:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目錄](assets/azure_directory_new.png)

1. 儲存設定。

## 配置IFD的Microsoft Dynamics {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics使用基於聲明的身份驗證，向外部用戶提供對Microsoft Dynamics CRM伺服器上資料的訪問。 要啟用此功能，請執行以下操作來配置面向Internet的部署(IFD)的Microsoft Dynamics並配置聲明設定。

>[!NOTE]
>
>只有在將AEM Forms與內部部署的Microsoft Dynamics伺服器整合時，才使用此程式。

1. 如[為Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx)配置IFD中所述，配置IFD的Microsoft Dynamics內部實例。
1. 使用Windows PowerShell運行以下命令，在啟用IFD的Microsoft Dynamics上配置聲明設定：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   如需詳細資訊，請參閱[內部部署CRM(IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd)的應用程式註冊。

## 在AD FS電腦{#configure-oauth-client-on-ad-fs-machine}上配置OAuth客戶端

執行以下操作以在Active Directory聯合身份驗證服務(AD FS)電腦上註冊OAuth客戶端，並在AD FS電腦上授予訪問權：

>[!NOTE]
>
>只有在將AEM Forms與內部部署的Microsoft Dynamics伺服器整合時，才使用此程式。

1. 執行下列命令：

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是可使用任何GUID產生器產生的用戶端ID。
   * `redirect-uri` 是AEM Forms上Microsoft Dynamics OData雲端服務的URL。隨AEM Forms套件安裝的預設雲端服務會部署在下列URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 運行以下命令以授予AD FS電腦上的訪問權：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是Microsoft Dynamics組織URL。

1. Microsoft Dynamics使用HTTPS通訊協定。 要從Forms伺服器調用AD FS終結點，請使用運行AEM Forms的電腦上的`keytool`命令將Microsoft Dynamics站點證書安裝到Java證書儲存。

## 為您的Microsoft Dynamics服務配置雲服務{#configure-cloud-service-for-your-microsoft-dynamics-service}

**MS Dynamics ODataCloud Service（OData服務）**&#x200B;配置隨預設OData配置一起提供。 要將其配置為與Microsoft Dynamics服務連接，請執行以下操作。

1. 導覽至「**[!UICONTROL 工具>Cloud Services>資料來源]**」，然後點選「`global`設定」資料夾。
1. 選擇&#x200B;**MS Dynamics ODataCloud Service（OData服務）**&#x200B;配置，然後點選&#x200B;**[!UICONTROL 屬性]**。 雲端服務設定屬性對話方塊隨即開啟。

   在&#x200B;**Authentication Settings**&#x200B;頁簽中：

   1. 輸入&#x200B;**服務根**&#x200B;欄位的值。 轉到Dynamics實例，並導航至&#x200B;**開發人員資源**&#x200B;以查看「服務根」欄位的值。 例如， https://&lt;tenant-name>/api/data/v9.1/

   1. 將&#x200B;**客戶端ID**（也稱為&#x200B;**應用程式ID**）、**客戶端密碼**、**OAuth URL**、**刷新令牌URL**、**訪問令牌URL**&#x200B;和&lt;a12/**中的預設值替換為Microsoft服務配置欄位中的值。**&#x200B;必須在&#x200B;**Resource**&#x200B;欄位中指定dynamics實例URL，才能使用表單資料模型配置Microsoft Dynamics。 使用服務根URL來衍生Dynamics實例URL。 例如， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/)。

   1. 在&#x200B;**授權範圍**&#x200B;欄位中指定&#x200B;**openid**，以便在Microsoft Dynamics上執行授權過程。

   ![驗證設定](assets/dynamics_authentication_settings_new.png)

1. 按一下「**[!UICONTROL 連線至OAuth]**」。 系統會將您重新導向至Microsoft Dynamics登入頁面。
1. 使用您的Microsoft Dynamics憑證登入，並接受，以允許雲端服務設定連線至Microsoft Dynamics服務。 在雲服務與服務之間建立連接是一項一次性任務。

   接著，系統會將您重新導向至雲端服務設定頁面，此頁面會顯示已成功儲存OData設定的訊息。

MS Dynamics ODataCloud Service（OData服務）雲服務已配置並與Dynamics服務連接。

## 建立表單資料模型{#create-form-data-model}

安裝AEM Forms套件時，AEM執行個體上會部署表單資料模型&#x200B;**Microsoft Dynamics FDM**。 依預設，表單資料模型使用在MS Dynamics ODataCloud Service（OData服務）中配置的Microsoft Dynamics服務作為其資料源。

首次開啟表單資料模型時，它會連接到已配置的Microsoft Dynamics服務，並從Microsoft Dynamics實例中提取實體。 表單資料模型中已新增來自Microsoft Dynamics的「連絡人」和「銷售機會」實體。

若要檢閱表單資料模型，請前往&#x200B;**[!UICONTROL Forms >資料整合]**。 選擇&#x200B;**Microsoft Dynamics FDM**，然後按一下&#x200B;**Edit**&#x200B;以在編輯模式中開啟表單資料模型。 或者，您也可以直接從下列URL開啟表單資料模型：

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

接下來，您可以根據表單資料模型建立最適化表單，並在各種最適化表單使用案例中使用，例如：

* 從Microsoft Dynamics實體和服務查詢資訊以預填最適化表單
* 使用最適化表單規則調用表單資料模型中定義的Microsoft Dynamics伺服器操作
* 將提交的表單資料寫入Microsoft Dynamics實體

建議您建立隨AEM Forms套件提供的表單資料模型復本，並設定資料模型和服務以符合您的需求。 這可確保未來套件的任何更新不會覆寫您的表單資料模型。

如需在業務工作流程中建立和使用表單資料模型的詳細資訊，請參閱[資料整合](../../forms/using/data-integration.md)。
