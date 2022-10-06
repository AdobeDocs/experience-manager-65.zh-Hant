---
title: Microsoft Dynamics OData設定
seo-title: Microsoft Dynamics ODtata configuration
description: 透過表單資料模型，運用、整合和使用線上和內部部署的Microsoft Dynamics服務。
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

# Microsoft Dynamics OData設定{#microsoft-dynamics-odata-configuration}

![資料整合](assets/data-integeration.png)

Microsoft Dynamics是客戶關係管理(CRM)和企業資源規劃(ERP)軟體，提供企業解決方案，用於建立和管理客戶帳戶、聯繫人、銷售機會、銷售機會和案例。 [AEM Forms資料整合](../../forms/using/data-integration.md) 提供OData雲服務配置，以將Forms與聯機和內部部署的Microsoft Dynamics伺服器整合。 它可讓您根據Microsoft Dynamics服務中定義的實體、屬性和服務來建立表單資料模型。 表單資料模型可用來建立與Microsoft Dynamics伺服器互動的最適化表單，以啟用業務工作流程。 例如：

* 查詢Microsoft Dynamics伺服器以取得資料並預先填入最適化表單
* 在最適化表單提交時將資料寫入Microsoft Dynamics
* 透過表單資料模型中定義的自訂實體在Microsoft Dynamics中寫入資料，反之亦然

AEM Forms附加元件套件也包含參考OData設定，您可運用此設定來快速整合Microsoft Dynamics與AEM Forms。

安裝套件時，您的AEM Forms執行個體上會提供下列實體和服務：

* MS Dynamics ODataCloud Service（OData服務）
* 表單資料模型已預先設定Microsoft Dynamics實體和服務。

只有在AEM例項的執行模式設為時，表單資料模型中預先設定的Microsoft Dynamics實體和服務才可在您的AEM Forms例項上使用 `samplecontent` （預設）。 MS Dynamics ODataCloud Service（OData服務）也可與其他運行模式一起使用。 如需設定AEM例項執行模式的詳細資訊，請參閱 [執行模式](/help/sites-deploying/configure-runmodes.md).

## 必備條件 {#prerequisites}

開始設定和設定Microsoft Dynamics之前，請確定您有：

* 已安裝 [AEM Forms附加元件套件](../../forms/using/installing-configuring-aem-forms-osgi.md)
* 已線上設定Microsoft Dynamics 365，或安裝下列其中一個Microsoft Dynamics版本的例項：

   * Microsoft Dynamics 365內部部署
   * Microsoft Dynamics 2016內部部署

* [已使用Microsoft Azure Active Directory註冊Microsoft Dynamics線上服務的應用程式](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). 記下註冊服務的用戶端ID（也稱為應用程式ID）和用戶端密碼的值。 這些值會在 [為您的Microsoft Dynamics服務設定雲端服務](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## 為已註冊的Microsoft Dynamics應用程式設定回覆URL {#set-reply-url-for-registered-microsoft-dynamics-application}

請執行下列操作，為已註冊的Microsoft Dynamics應用程式設定回覆URL:

>[!NOTE]
>
>只有在將AEM Forms與線上Microsoft Dynamics伺服器整合時，才使用此程式。

1. 前往Microsoft Azure Active Directory帳戶，並在 **回覆URL** 註冊應用程式的設定：

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目錄](assets/azure_directory_new.png)

1. 儲存設定。

## 配置IFD的Microsoft Dynamics {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics使用以聲明為基礎的驗證，為外部使用者提供對Microsoft Dynamics CRM伺服器上資料的存取。 要啟用此功能，請執行以下操作來配置面向Internet的部署(IFD)的Microsoft Dynamics並配置聲明設定。

>[!NOTE]
>
>只有在將AEM Forms與內部部署的Microsoft Dynamics伺服器整合時，才使用此程式。

1. 配置IFD的Microsoft Dynamics內部部署實例，如 [為Microsoft Dynamics配置IFD](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. 使用Windows PowerShell運行以下命令，在啟用IFD的Microsoft Dynamics上配置聲明設定：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   請參閱 [CRM內部部署(IFD)的應用程式註冊](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 以取得詳細資訊。

## 在AD FS電腦上配置OAuth客戶端 {#configure-oauth-client-on-ad-fs-machine}

執行以下操作以在Active Directory聯合身份驗證服務(AD FS)電腦上註冊OAuth客戶端，並在AD FS電腦上授予訪問權：

>[!NOTE]
>
>只有在將AEM Forms與內部部署的Microsoft Dynamics伺服器整合時，才使用此程式。

1. 執行下列命令：

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是可使用任何GUID產生器產生的用戶端ID。
   * `redirect-uri` 是AEM Forms上Microsoft Dynamics OData雲端服務的URL。 隨AEM Forms套件安裝的預設雲端服務會部署在下列URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 運行以下命令以授予AD FS電腦上的訪問權：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是Microsoft Dynamics組織URL。

1. Microsoft Dynamics使用HTTPS通訊協定。 若要從Forms伺服器叫用AD FS端點，請使用安裝Microsoft Dynamics網站憑證至Java憑證存放區 `keytool` 命令。

## 為您的Microsoft Dynamics服務設定雲端服務 {#configure-cloud-service-for-your-microsoft-dynamics-service}

此 **MS Dynamics ODataCloud Service（OData服務）** 配置隨預設OData配置一起提供。 若要將其設定為連線至您的Microsoft Dynamics服務，請執行下列動作。

1. 導覽至 **[!UICONTROL 工具>Cloud Services>資料來源]**，然後點選 `global` 設定資料夾。
1. 選擇 **MS Dynamics ODataCloud Service（OData服務）** 設定與點選 **[!UICONTROL 屬性]**. 雲端服務設定屬性對話方塊隨即開啟。

   在 **驗證設定** 標籤：

   1. 輸入 **服務根** 欄位。 前往Dynamics例項，並導覽至 **開發人員資源** 查看「服務根」欄位的值。 例如， https://&lt;tenant-name>/api/data/v9.1/

   1. 取代 **用戶端ID**(又稱為 **應用程式ID**), **用戶端密碼**, **OAuth URL**, **重新整理Token URL**, **存取權杖URL**，和 **資源** 欄位，其值來自您的Microsoft Dynamics服務設定。 必須在 **資源** 欄位來使用表單資料模型設定Microsoft Dynamics。 使用服務根URL來衍生Dynamics實例URL。 例如， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. 指定 **openid** 在 **授權範圍** 欄位，用於Microsoft Dynamics上的授權程式。

   ![驗證設定](assets/dynamics_authentication_settings_new.png)

1. 按一下 **[!UICONTROL 連線至OAuth]**. 系統會將您重新導向至Microsoft Dynamics登入頁面。
1. 使用您的Microsoft Dynamics憑證登入，並接受以允許雲端服務設定連線至Microsoft Dynamics服務。 在雲服務與服務之間建立連接是一項一次性任務。

   接著，系統會將您重新導向至雲端服務設定頁面，此頁面會顯示已成功儲存OData設定的訊息。

MS Dynamics ODataCloud Service（OData服務）雲服務已配置並與Dynamics服務連接。

## 建立表單資料模型 {#create-form-data-model}

安裝AEM Forms套件時，表單資料模型，**Microsoft Dynamics FDM**，會部署在您的AEM例項上。 依預設，表單資料模型使用MS Dynamics ODataCloud Service（OData服務）中設定的Microsoft Dynamics服務作為其資料來源。

首次開啟表單資料模型時，它會連線至已設定的Microsoft Dynamics服務，並從您的Microsoft Dynamics例項擷取實體。 Microsoft Dynamics的「連絡人」和「銷售機會」實體已新增至表單資料模型中。

若要檢閱表單資料模型，請前往 **[!UICONTROL Forms >資料整合]**. 選擇 **Microsoft Dynamics FDM** 按一下 **編輯** 以在編輯模式中開啟表單資料模型。 或者，您也可以直接從下列URL開啟表單資料模型：

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

接下來，您可以根據表單資料模型建立最適化表單，並在各種最適化表單使用案例中使用，例如：

* 從Microsoft Dynamics實體和服務查詢資訊，預填最適化表單
* 使用適用性表單規則叫用表單資料模型中定義的Microsoft Dynamics伺服器作業
* 將提交的表單資料寫入Microsoft Dynamics實體

建議您建立隨AEM Forms套件提供的表單資料模型復本，並設定資料模型和服務以符合您的需求。 這可確保未來套件的任何更新不會覆寫您的表單資料模型。

如需在業務工作流程中建立和使用表單資料模型的詳細資訊，請參閱 [資料整合](../../forms/using/data-integration.md).
