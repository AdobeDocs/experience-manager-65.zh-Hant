---
title: Microsoft Dynamics OData組態
seo-title: Microsoft Dynamics ODtata組態
description: 透過表單資料模型，運用、整合及使用線上和內部Microsoft Dynamics服務。
seo-description: 瞭解如何透過表單資料模型，運用與線上和內部Microsoft Dynamics服務的整合與運作。
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: 表單資料模型
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 0%

---


# Microsoft Dynamics OData組態{#microsoft-dynamics-odata-configuration}

![資料整合](assets/data-integeration.png)

Microsoft Dynamics是客戶關係管理(CRM)和企業資源規劃(ERP)軟體，提供企業解決方案，以建立和管理客戶帳戶、連絡人、潛在客戶、商機和案例。 [AEM Forms資](../../forms/using/data-integration.md) 料整合提供OData雲端服務組態，將Forms與線上和內部Microsoft Dynamics伺服器整合。它可讓您根據Microsoft Dynamics服務中定義的實體、屬性和服務來建立表單資料模型。 表單資料模型可用來建立與Microsoft Dynamics伺服器互動的最適化表單，以啟用商業工作流程。 例如：

* 查詢Microsoft Dynamics Server中的資料和預先填入最適化表單
* 在自適應表單提交時，將資料寫入Microsoft Dynamics
* 透過表單資料模型中定義的自訂實體，在Microsoft Dynamics中寫入資料，反之亦然

AEM Forms附加套件也包含參考OData組態，您可運用此組態來快速整合Microsoft Dynamics與AEM Forms。

安裝軟體包後，您的AEM Forms實例上將提供以下實體和服務：

* MS Dynamics ODataCloud Service（OData服務）
* 使用預先設定的Microsoft Dynamics實體和服務來建立資料模型。

只有在實例的運行模式設定為`samplecontent`（預設）時，在AEM Forms實例上才可AEM以使用表單資料模型中預配置的Microsoft Dynamics實體和服務。 MS Dynamics ODataCloud Service（OData服務）也適用於其他運行模式。 有關為實例配置運行模式的詳AEM細資訊，請參見[運行模式](/help/sites-deploying/configure-runmodes.md)。

## 必備條件 {#prerequisites}

在開始設定和設定Microsoft Dynamics之前，請確定您有：

* 已安裝[AEM Forms附加軟體包](../../forms/using/installing-configuring-aem-forms-osgi.md)
* 已線上設定Microsoft Dynamics 365，或安裝下列其中一個Microsoft Dynamics版本的例項：

   * Microsoft Dynamics 365內部
   * Microsoft Dynamics 2016內部版

* [已在Microsoft Azure Active Directory中註冊Microsoft Dynamics線上服務的應用程式](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)。記下註冊服務的用戶端ID（也稱為應用程式ID）和用戶端密碼的值。 這些值在[為您的Microsoft Dynamics服務](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service)配置雲服務時使用。

## 為已註冊的Microsoft Dynamics應用程式設定回覆URL {#set-reply-url-for-registered-microsoft-dynamics-application}

請執行下列動作，為註冊的Microsoft Dynamics應用程式設定回覆URL:

>[!NOTE]
>
>只有在將AEM Forms與線上Microsoft Dynamics伺服器整合時，才使用此過程。

1. 前往Microsoft Azure Active Directory帳戶，並在您註冊的應用程式的「回覆URL」設定中新增下列雲端服務設定URL:****

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目錄](assets/azure_directory_new.png)

1. 儲存設定。

## 為IFD配置Microsoft Dynamics {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics使用以理賠為基礎的驗證，將Microsoft Dynamics CRM伺服器上的資料存取權提供給外部使用者。 若要啟用此功能，請執行下列動作，以設定Microsoft Dynamics for Internet-facing deployment(IFD)，並設定索賠設定。

>[!NOTE]
>
>僅在將AEM Forms與內部Microsoft Dynamics伺服器整合時使用此過程。

1. 按照[ Configure IFD for Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx)中所述，為IFD配置Microsoft Dynamics內部實例。
1. 使用Windows PowerShell運行以下命令，在啟用IFD的Microsoft Dynamics上配置聲明設定：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   如需詳細資訊，請參閱[內部CRM(IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd)應用程式註冊。

## 在AD FS機器上設定OAuth用戶端{#configure-oauth-client-on-ad-fs-machine}

請執行下列動作，在Active Directory Federation Services(AD FS)機器上註冊OAuth用戶端，並授與AD FS機器的存取權：

>[!NOTE]
>
>僅在將AEM Forms與內部Microsoft Dynamics伺服器整合時使用此過程。

1. 運行以下命令：

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是可使用任何GUID產生器產生的用戶端ID。
   * `redirect-uri` 是AEM FormsMicrosoft Dynamics OData雲端服務的URL。隨AEM Forms軟體包安裝的預設雲服務部署在以下URL中：
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 運行以下命令以授予對AD FS電腦的訪問權：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是Microsoft Dynamics組織URL。

1. Microsoft Dynamics使用HTTPS通訊協定。 要從Forms伺服器調用AD FS端點，請在運行AEM Forms的電腦上使用`keytool`命令將Microsoft Dynamics站點證書安裝到Java證書儲存。

## 為您的Microsoft Dynamics服務配置雲端服務{#configure-cloud-service-for-your-microsoft-dynamics-service}

**MS Dynamics ODataCloud Service（OData服務）**&#x200B;配置隨預設OData配置一起提供。 要將其配置為與Microsoft Dynamics服務連接，請執行以下操作。

1. 導覽至「**[!UICONTROL 工具>Cloud Services> Data Sources]**」，然後點選「`global`組態」資料夾。
1. 選擇&#x200B;**MS Dynamics ODataCloud Service（OData服務）**&#x200B;配置並按一下&#x200B;**[!UICONTROL 屬性]**。 雲端服務設定屬性對話方塊隨即開啟。

   在&#x200B;**驗證設定**&#x200B;頁籤中：

   1. 輸入&#x200B;**服務根**&#x200B;欄位的值。 轉至Dynamics實例並導航至&#x200B;**Developer Resources**&#x200B;以查看「服務根」欄位的值。 例如，https://&lt;tenant-name>/api/data/v9.1/

   1. 取代&#x200B;**用戶端ID**（亦稱&#x200B;**應用程式ID**）、**用戶端密碼**、**OAuth URL**、**重新整理Token URL**、**使用Microsoft Dynamics服務組態的值存取Token URL**&#x200B;和&#x200B;**資源**&#x200B;欄位。 必須在&#x200B;**資源**&#x200B;欄位中指定動態例項URL，才能使用表單資料模型來設定Microsoft Dynamics。 使用「服務根URL」衍生動態例項URL。 例如，[https://org.crm.dynamics.com](https://org.crm.dynamics.com/)。

   1. 在&#x200B;**授權範圍**&#x200B;欄位中指定&#x200B;**openid**，以便在Microsoft Dynamics上進行授權程式。

   ![驗證設定](assets/dynamics_authentication_settings_new.png)

1. 按一下「連線至OAuth ]**」。**[!UICONTROL &#x200B;系統會將您重新導向至Microsoft Dynamics登入頁面。
1. 使用您的Microsoft Dynamics憑證登入，並接受允許雲端服務設定連線至Microsoft Dynamics服務。 建立雲服務與服務之間的連接是一次性的任務。

   然後，您會被重新導向至雲端服務設定頁面，此頁面會顯示訊息，指出OData設定已成功儲存。

MS Dynamics ODataCloud Service（OData服務）雲端服務已設定並與您的Dynamics服務連接。

## 建立表單資料模型{#create-form-data-model}

安裝AEM Forms軟體包時，實例上將部署表單資料模型&#x200B;**Microsoft Dynamics FDM** AEM。 預設情況下，表單資料模型使用在MS Dynamics ODataCloud Service（OData服務）中配置的Microsoft Dynamics服務作為其資料源。

首次開啟表單資料模型時，它將連接到已配置的Microsoft Dynamics服務並從Microsoft Dynamics實例中提取實體。 Microsoft Dynamics的「連絡人」和「潛在客戶」實體已新增至表單資料模型。

若要檢視表單資料模型，請前往&#x200B;**[!UICONTROL Forms>資料整合]**。 選擇&#x200B;**Microsoft Dynamics FDM**&#x200B;並按一下&#x200B;**編輯**&#x200B;以在編輯模式下開啟表單資料模型。 或者，您也可以直接從下列URL開啟表單資料模型：

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

接下來，您可以根據表單資料模型建立自適應表單，並在各種自適應表單使用案例中使用，例如：

* 從Microsoft Dynamics實體和服務查詢資訊以預先填寫最適化表單
* 使用自適應表單規則調用在表單資料模型中定義的Microsoft Dynamics伺服器操作
* 將提交的表單資料寫入Microsoft Dynamics實體

建議您建立隨AEM Forms套件提供的表單資料模型復本，並設定符合您需求的資料模型和服務。 它將確保未來套件的任何更新不會覆寫您的表單資料模型。

如需在商業工作流程中建立和使用表單資料模型的詳細資訊，請參閱[資料整合](../../forms/using/data-integration.md)。
