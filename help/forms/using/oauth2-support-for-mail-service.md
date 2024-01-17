---
title: 設定Microsoft&reg； Office 365郵件伺服器通訊協定的OAuth2驗證
description: 設定Microsoft&reg； Office 365郵件伺服器通訊協定的OAuth2驗證
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: 020b92463371294706e9873e0d8962583d19ac52
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 5%

---

# 與Microsoft® Office 365郵件伺服器通訊協定整合 {#oauth2-support-for-the-microsoft-mail-server-protocols}

為了讓組織遵守安全電子郵件要求，AEM Forms提供OAuth 2.0支援，以便與Microsoft® Office 365郵件伺服器通訊協定整合。 您可以使用Azure Active Directory (Azure AD) OAuth 2.0驗證服務來連線各種通訊協定（例如IMAP、POP或SMTP），並存取Office 365使用者的電子郵件資料。 以下是設定Microsoft® Office 365郵件伺服器通訊協定以透過OAuth 2.0服務進行驗證的逐步指示：

1. 登入 [https://portal.azure.com/](https://portal.azure.com/) 並搜尋 **Azure Active Directory** ，然後按一下結果。
或者，您可以直接瀏覽到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下 **新增** > **應用程式註冊** > **新註冊**.

   ![應用程式註冊](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 根據您的要求填寫資訊，然後按一下「**註冊**」。
   ![支援的帳戶](/help/forms/using/assets/azure_suuportedaccountype.png)
在上述案例中， **任何組織目錄（任何Azure AD目錄 — 多租使用者）中的帳戶和個人Microsoft®帳戶（例如，Skype、Xbox）** 已選取選項。

   >[!NOTE]
   >
   > * 的 **任何組織目錄（任何Azure AD目錄 — 多租使用者）中的帳戶** 應用程式，Adobe建議您使用工作帳戶，而非個人電子郵件帳戶。
   > * **僅限個人Microsoft®帳戶** 應用程式不受支援。
   * Adobe建議您使用 **多租使用者和個人Microsoft®帳戶** 應用程式。

1. 接下來，移至「**憑證和密碼**」，按一下「**新增用戶端密碼**」，並按照畫面上的步驟建立密碼。請務必記下此secret值以供稍後使用。

   ![秘密金鑰](/help/forms/using/assets/azure_secretkey.png)

1. 若要新增許可權，請前往新建的應用程式，然後選取「 」 **API許可權** > **新增許可權** > **Microsoft® Graph** > **委派許可權**.
1. 選取以下應用程式許可權的核取方塊，然後按一下 **新增許可權**：

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API許可權](/help/forms/using/assets/azure_apipermission.png)

1. 選取 **驗證** > **新增平台** > **Web**，以及 **重新導向Url** 區段，將以下任一URI （通用資源識別碼）新增為：
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   在這種情況下， `https://login.microsoftonline.com/common/oauth2/nativeclient` 會作為重新導向URI使用。

1. 按一下 **設定** 新增每個URL並根據您的要求進行設定後。
   ![重新導向URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   必須選取 **存取權杖** 和 **ID權杖** 核取方塊。

1. 按一下 **概觀** 並複製下列專案的值： **應用程式（使用者端） ID**， **目錄（租使用者） ID**、和 **使用者端密碼** 以供日後使用。

   ![概觀](/help/forms/using/assets/azure_overview.png)

## 產生授權代碼 {#generating-the-authorization-code}

接下來，您必須產生授權代碼，如以下步驟所述：

1. 取代之後，在瀏覽器中開啟下列URL `clientID` 使用 `<client_id>` 和 `redirect_uri` 使用應用程式的重新導向URI：

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   如果存在單一租使用者應用程式，請取代 `common` 與您的 `[tenantid]` 在下列產生授權代碼的URL中： `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. 當您輸入上述URL時，您會被重新導向至登入畫面：
   ![登入畫面](/help/forms/using/assets/azure_loginscreen.png)

1. 輸入電子郵件，按一下 **下一個** 「應用程式」許可權畫面隨即顯示：

   ![允許許可權](/help/forms/using/assets/azure_permission.png)

1. 當您允許許可權時，您會重新導向至新的URL，如下所示： `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 複製值 `<code>` 從上面的URL從 `0.ASY...` 至 `&session_state` 在上述URL中。

## 產生重新整理權杖 {#generating-the-refresh-token}

接下來，您必須產生重新整理權杖，如下列步驟所述：

1. 開啟命令提示字元並使用下列cURL命令取得refreshToken。

1. 取代 `clientID`， `client_secret`、和 `redirect_uri` 以及您應用程式的值 `<code>`：

   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   在單一租使用者應用程式中，若要產生重新整理權杖，請使用以下cURL命令並取代 `common` 使用 `[tenantid]` 在：
   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. 記下重新整理權杖。

## 設定電子郵件服務與OAuth 2.0支援 {#configureemailservice}

現在，請登入管理員UI，在最新的JEE伺服器上設定電子郵件服務：

1. 前往 **首頁** > **服務** > **應用程式和服務** > **服務管理** > **電子郵件服務**，則 **設定電子郵件服務** 視窗會出現，針對基本驗證進行設定。

   >[!NOTE]
   >
   若要啟用oAuth 2.0驗證服務，必須選取 **SMTP伺服器是否需要驗證（SMTP驗證）** 核取方塊。

1. 設定 **oAuth 2.0驗證設定** 作為 `True`.
1. 複製下列專案的值： **使用者端ID** 和 **使用者端密碼** 從Azure入口網站。
1. 複製產生的值 **重新整理Token**.
1. 登入 **Workbench** 和搜尋 **電子郵件1.0** 從 **活動選取器**.
1. 電子郵件1.0下有三個選項：
   * **隨檔案傳送**：傳送包含單一附件的電子郵件。
   * **隨附件地圖傳送**：傳送包含多個附件的電子郵件。
   * **接收**：從IMAP接收電子郵件。

   >[!NOTE]
   >
   * 傳輸安全性通訊協定有下列有效值： &#39;blank&#39;、&#39;SSL&#39;或&#39;TLS&#39;。 設定值 **SMTP傳輸安全性** 和 **接收傳輸安全性** 至 **TLS** 以啟用oAuth驗證服務。
   * **pop3通訊協定** 使用電子郵件端點時，不支援OAuth使用。

   ![連線設定](/help/forms/using/assets/oauth_connectionsettings.png)

1. 選取以測試應用程式 **隨檔案傳送**.
1. 提供 **到** 和 **從** 位址。
1. 叫用應用程式，並使用0Auth 2.0驗證傳送電子郵件。

   >[!NOTE]
   >
   如有需要，您可以將Workbench中特定程式的Auth 2.0驗證設定變更為基本驗證。 若要這麼做，請設定 **OAuth 2.0驗證** 值為&#39;False&#39;，在 **使用全域設定** 在 **連線設定** 標籤。

## 啟用oAuth任務通知的方式 {#enable_oauth_task}

1. 前往 **首頁** > **服務** > **表單工作流程** > **伺服器設定** > **電子郵件設定**
1. 若要啟用oAuth工作通知，請選取 **啟用oAuth** 核取方塊。
1. 複製下列專案的值： **使用者端ID** 和 **使用者端密碼** 從Azure入口網站。
1. 複製產生的值 **重新整理Token**.
1. 按一下 **儲存** 以儲存詳細資訊。

   ![任務通知](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   若要瞭解更多與工作通知相關的資訊， [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## 設定電子郵件端點 {#configure_email_endpoint}

1. 前往 **首頁** > **服務** > **應用程式和服務** > **端點管理**
1. 若要設定電子郵件端點，請設定 **oAuth 2.0驗證設定** 作為 `True`.
1. 複製下列專案的值： **使用者端ID** 和 **使用者端密碼** 從Azure入口網站。
1. 複製產生的值 **重新整理Token**.
1. 按一下 **儲存** 以儲存詳細資訊。

   ![連線設定](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   若要瞭解有關設定電子郵件端點的詳細資訊，請按一下 [設定電子郵件端點](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html).

## 疑難排解 {#troubleshooting}

* 如果電子郵件服務無法正常運作，請嘗試重新產生 `Refresh Token` 如上所述。 部署新值需要幾分鐘的時間。

* 使用Workbench在電子郵件端點中設定電子郵件伺服器詳細資料時發生錯誤。 嘗試透過Admin UI （而非Workbench）設定端點。
