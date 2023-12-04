---
title: Microsoft Dynamics OData設定
description: 瞭解如何透過表單資料模型使用、整合及使用線上和內部部署Microsoft Dynamics服務。
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# Microsoft Dynamics OData設定{#microsoft-dynamics-odata-configuration}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/ms-dynamics-odata-configuration.html) |
| AEM 6.5 | 本文章 |

![資料整合](assets/data-integeration.png)

Microsoft Dynamics是一款客戶關係管理(CRM)和企業資源規劃(ERP)軟體，提供企業解決方案，用於建立和管理客戶帳戶、聯絡人、銷售機會、機會和案例。 [AEM Forms資料整合](../../forms/using/data-integration.md) 提供OData雲端服務設定，以將Forms與線上和內部部署Microsoft Dynamics伺服器整合。 它可讓您根據Microsoft Dynamics服務中定義的實體、屬性和服務來建立表單資料模型。 表單資料模型可用來建立與Microsoft Dynamics伺服器互動的最適化表單，以啟用業務工作流程。 例如：

* 查詢Microsoft Dynamics伺服器以取得資料並預先填入最適化表單
* 提交最適化表單時將資料寫入Microsoft Dynamics
* 透過表單資料模型中定義的自訂實體在Microsoft Dynamics中寫入資料，反之亦然

AEM Forms附加元件套件也包含參考OData設定，可用來快速將Microsoft Dynamics與AEM Forms整合。

安裝套件後，您的AEM Forms執行個體上有以下實體和服務可用：

* MS Dynamics ODataCloud Service（OData服務）
* 具有預先設定之Microsoft Dynamics實體和服務的表單資料模型。

您必須將Microsoft執行個體的執行模式設為，才能在您的AEM Forms執行個體上使用表單資料模型中預先設定的AEM Dynamics實體和服務 `samplecontent` （預設）。 MS Dynamics ODataCloud Service（OData服務）也可用於其他執行模式。 如需為AEM執行個體設定執行模式的詳細資訊，請參閱 [執行模式](/help/sites-deploying/configure-runmodes.md).

## 先決條件 {#prerequisites}

在開始設定和設定Microsoft Dynamics之前，請確定您擁有：

* 已安裝 [AEM Forms附加元件套件](../../forms/using/installing-configuring-aem-forms-osgi.md)
* 已線上上設定Microsoft Dynamics 365，或已安裝下列其中一個Microsoft Dynamics版本的執行個體：

   * Microsoft Dynamics 365內部部署
   * Microsoft Dynamics 2016內部部署

* [已在Microsoft Azure Active Directory註冊Microsoft Dynamics線上服務的應用程式](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). 記下註冊服務的使用者端ID （也稱為應用程式ID）和使用者端密碼的值。 這些值用於 [為您的Microsoft Dynamics服務設定雲端服務](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## 設定已註冊Microsoft Dynamics應用程式的回覆URL {#set-reply-url-for-registered-microsoft-dynamics-application}

執行下列動作，為已註冊的Microsoft Dynamics應用程式設定回覆URL：

>[!NOTE]
>
>只有在將AEM Forms與線上Microsoft Dynamics伺服器整合時，才使用此程式。

1. 前往Microsoft Azure Active Directory帳戶，並在中新增下列雲端服務設定URL **回覆URL** 註冊應用程式的設定：

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目錄](assets/azure_directory_new.png)

1. 儲存設定。

## 設定Microsoft Dynamics以使用IFD {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics使用宣告式驗證，為外部使用者提供對Microsoft Dynamics CRM伺服器上資料的存取權。 若要啟用此功能，請執行以下動作來設定Microsoft Dynamics的網際網路對向部署(IFD)並設定宣告設定。

>[!NOTE]
>
>只有在將AEM Forms與內部部署Microsoft Dynamics伺服器整合時，才使用此程式。

1. 依照中的說明，設定IFD的Microsoft Dynamics內部部署執行個體 [設定Microsoft Dynamics的IFD](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. 使用Windows PowerShell執行以下命令，在啟用IFD的Microsoft Dynamics上設定宣告設定：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   另請參閱 [CRM內部部署(IFD)的應用程式註冊](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 以取得詳細資訊。

## 在AD FS電腦上設定OAuth使用者端 {#configure-oauth-client-on-ad-fs-machine}

執行下列動作，在Active Directory Federation Services (AD FS)電腦上註冊OAuth使用者端並授與AD FS電腦上的存取權：

>[!NOTE]
>
>只有在將AEM Forms與內部部署Microsoft Dynamics伺服器整合時，才使用此程式。

1. 執行以下命令：

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是您可以使用任何GUID產生器產生的使用者端ID。
   * `redirect-uri` 是AEM Forms上Microsoft Dynamics OData雲端服務的URL。 與AEM Forms套件一起安裝的預設雲端服務會部署在以下URL：
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 執行以下命令來授予AD FS電腦上的存取權：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是Microsoft Dynamics組織URL。

1. Microsoft Dynamics使用HTTPS通訊協定。 若要從Forms伺服器叫用AD FS端點，請使用將Microsoft Dynamics網站憑證安裝到Java憑證存放區 `keytool` 執行AEM Forms的電腦上的命令。

## 為您的Microsoft Dynamics服務設定雲端服務 {#configure-cloud-service-for-your-microsoft-dynamics-service}

此 **MS Dynamics ODataCloud Service（OData服務）** 設定隨附預設的OData設定。 若要將其設定為連線至您的Microsoft Dynamics服務，請執行下列動作。

1. 瀏覽至 **[!UICONTROL 「工具>Cloud Service>資料來源」]**，然後選取 `global` 設定資料夾。
1. 選取 **MS Dynamics ODataCloud Service（OData服務）** 設定並選取 **[!UICONTROL 屬性]**. 雲端服務設定屬性對話方塊隨即開啟。

   在 **驗證設定** 標籤：

   1. 輸入值 **服務根目錄** 欄位。 前往Dynamics執行個體並導覽至 **開發人員資源** 以檢視「服務根」欄位的值。 例如， https://&lt;tenant-name>/api/data/v9.1/

   1. 取代 **使用者端ID**(也稱為 **應用程式ID**)， **使用者端密碼**， **OAuth URL**， **重新整理記號URL**， **存取記號URL**、和 **資源** 包含來自您的Microsoft Dynamics服務設定的值的欄位。 您必須在「 」中指定動態執行個體URL **資源** 欄位以使用表單資料模型設定Microsoft Dynamics。 使用服務根URL衍生動態執行個體URL。 例如， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. 指定 **openid** 在 **授權範圍** Microsoft Dynamics上授權程式的欄位。

   ![驗證設定](assets/dynamics_authentication_settings_new.png)

1. 按一下 **[!UICONTROL 連線至OAuth]**. 系統會將您重新導向至Microsoft Dynamics登入頁面。
1. 使用您的Microsoft Dynamics憑證登入，並接受以允許雲端服務設定連線到Microsoft Dynamics服務。 在雲端服務和服務之間建立連線是一項單次性的工作。

   系統會將您重新導向至雲端服務設定頁面，其中顯示OData設定已成功儲存的訊息。

MS Dynamics ODataCloud Service（OData服務）雲端服務已設定，並已與您的Dynamics服務連線。

## 建立表單資料模型 {#create-form-data-model}

安裝AEM Forms套件時，表單資料模型會&#x200B;**Microsoft Dynamics FDM**，即部署在您的AEM執行個體上。 依預設，表單資料模型會使用MS Dynamics ODataCloud Service（OData服務）中設定的Microsoft Dynamics服務作為其資料來源。

首次開啟表單資料模型時，它會連線至已設定的Microsoft Dynamics服務，並從Microsoft Dynamics例項中擷取實體。 Microsoft Dynamics中的「聯絡人」和「銷售機會」實體已新增至表單資料模型。

若要檢閱表單資料模型，請前往 **[!UICONTROL Forms >資料整合]**. 選取 **Microsoft Dynamics FDM** 並按一下 **編輯** 以於編輯模式中開啟表單資料模型。 或者，您也可以直接從下列URL開啟表單資料模型：

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

接著，您可以根據表單資料模型建立最適化表單，並在各種最適化表單使用案例中使用，例如：

* 從Microsoft Dynamics實體和服務查詢資訊，預先填寫最適化表單
* 使用最適化表單規則叫用表單資料模型中定義的Microsoft Dynamics伺服器作業
* 將提交的表單資料寫入Microsoft Dynamics實體

建議您建立AEM Forms套件隨附的表單資料模型副本，並設定資料模型和服務以符合您的需求。 它將確保封裝的任何未來更新都不會覆蓋您的表單資料模型。

如需在業務工作流程中建立和使用表單資料模型的詳細資訊，請參閱 [資料整合](../../forms/using/data-integration.md).
