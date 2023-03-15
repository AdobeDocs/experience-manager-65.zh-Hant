---
title: 為Microsoft® Office 365郵件伺服器通訊協定配置OAuth2型驗證
description: 為Microsoft® Office 365郵件伺服器通訊協定配置OAuth2型驗證
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: d19de2955adef56570378a6d62ec0015718f9039
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---

# 與Microsoft® Office 365郵件伺服器協定整合 {#oauth2-support-for-the-microsoft-mail-server-protocols}

為了讓組織遵守安全的電子郵件要求，AEM Forms提供OAuth 2.0支援，以與Microsoft® Office 365郵件伺服器通訊協定整合。 您可以使用Azure Active Directory(Azure AD)OAuth 2.0身份驗證服務，與各種協定（如IMAP、POP或SMTP）連接，並訪問Office 365用戶的電子郵件資料。 以下是配置Microsoft® Office 365郵件伺服器協定以通過OAuth 2.0服務進行身份驗證的逐步說明：

1. 登入 [https://portal.azure.com/](https://portal.azure.com/) 和搜索 **Azure Active Directory** 在搜尋列中，按一下結果。
或者，您可以直接瀏覽到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下 **新增** > **應用程式註冊** > **新註冊**

   ![應用程式註冊](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 根據您的需求填寫資訊，然後按一下 **註冊**.
   ![支援的帳戶](/help/forms/using/assets/azure_suuportedaccountype.png)
在上述情況中， 
**任何組織目錄（任何Azure AD目錄 — 多租用戶）中的帳戶和個人Microsoft®帳戶（例如Skype、Xbox）** 選項。

   >[!NOTE]
   >
   > * 針對 **任何組織目錄（任何Azure AD目錄 — 多租用戶）中的帳戶** 應用程式時，建議使用工作帳戶，而非個人電子郵件帳戶。
   > * **僅限個人Microsoft®賬戶** 不支援應用程式。
   > * 建議使用 **多租用戶和個人Microsoft®帳戶** 應用程式。


1. 接下來，轉到 **憑證和機密**，按一下 **新用戶端密碼** 並依照畫面上的步驟建立密碼。 請務必記下此機密值以供日後使用。

   ![機密金鑰](/help/forms/using/assets/azure_secretkey.png)

1. 若要新增權限，請前往新建立的應用程式，然後選取 **API權限** > **新增權限** > **Microsoft®圖** > **委派權限**
1. 選取應用程式下列權限的核取方塊，然後按一下 **新增權限**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API權限](/help/forms/using/assets/azure_apipermission.png)

1. 選擇 **驗證** > **新增平台** > **Web**，和 **重新導向Url** 部分，將以下任何URI（通用資源標識符）添加為：
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   在這種情況下， `https://login.microsoftonline.com/common/oauth2/nativeclient` 用作重定向URI。

1. 按一下 **設定** 新增每個URL，並根據您的需求進行設定後，才會執行此動作。
   ![重新導向 URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > 必須選取 **存取權杖** 和 **ID Token** 複選框。

1. 按一下 **概述** 並複製 **應用程式（客戶端）ID**, **目錄（租用戶）ID**，和 **用戶端密碼** 供稍後使用。

   ![概觀](/help/forms/using/assets/azure_overview.png)

## 產生授權代碼 {#generating-the-authorization-code}

接下來，您需要產生授權代碼，如下列步驟所述：

1. 取代後，在瀏覽器中開啟下列URL `clientID` 和 `<client_id>` 和 `redirect_uri` 使用應用程式的重新導向URI:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > 若為單一租用戶應用程式，請取代 `common` 與 `[tenantid]` 在以下URL中，用於產生授權代碼： `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. 當您輸入上述URL時，系統會將您重新導向至登入畫面：
   ![登入畫面](/help/forms/using/assets/azure_loginscreen.png)

1. 輸入電子郵件，按一下 **下一個** 和應用程式權限畫面隨即顯示：

   ![允許權限](/help/forms/using/assets/azure_permission.png)

1. 一旦您允許權限，系統會將您重新導向至新URL，如下所示： `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 複製 `<code>` 從上述URL從 `0.ASY...` to `&session_state` 填入。

## 產生重新整理權杖 {#generating-the-refresh-token}

接下來，您需要產生重新整理Token，如下列步驟所述：

1. 開啟命令提示字元，然後使用下列cURL命令來取得refreshToken。

1. 取代 `clientID`, `client_secret` 和 `redirect_uri` 與應用程式的值，以及 `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > 在單一租用戶應用程式中，若要產生重新整理Token，請使用下列cURL命令並取代 `common` 和 `[tenantid]` 在：
   >`curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. 記下重新整理Token。

## 使用OAuth 2.0支援設定電子郵件服務 {#configureemailservice}

現在，您必須透過管理員UI中的登入，在最新的JEE伺服器設定電子郵件服務：

1. 前往 **首頁** > **服務** > **應用程式和服務** > **服務管理** > **電子郵件服務**, **設定電子郵件服務** 窗口，配置基本身份驗證。

   >[!NOTE]
   >
   > 若要啟用oAuth 2.0驗證服務，必須選取 **SMTP伺服器是否需要身份驗證（SMTP身份驗證）** 核取方塊。

1. 設定 **oAuth 2.0驗證設定** as `True`.
1. 複製 **用戶端ID** 和 **用戶端密碼** 從Azure門戶。
1. 複製所產生的值 **重新整理Token**.
1. 登入 **Workbench** 搜尋 **電子郵件1.0** 從 **活動選擇器**.
1. 電子郵件1.0下提供下列三個選項：
   * **隨文檔一起發送**:傳送包含單一附件的電子郵件。
   * **隨附附件地圖傳送**:傳送包含多個附件的電子郵件。
   * **接收**:從IMAP接收電子郵件。

   >[!NOTE]
   >
   >* 傳輸安全協定的有效值為：&#39;blank&#39;、&#39;SSL&#39;或&#39;TLS&#39;。 您必須設定 **SMTP傳輸安全性** 和 **接收傳輸安全性** to **TLS** 啟用oAuth驗證服務。
   >* **POP3協定** 使用電子郵件端點時不支援OAuth。


   ![連線設定](/help/forms/using/assets/oauth_connectionsettings.png)

1. 選取 **隨文檔一起發送**.
1. 提供 **結束日期** 和 **從** 地址。
1. 叫用應用程式，並使用0Auth 2.0驗證傳送電子郵件。

   >[!NOTE]
   >
   >如果您想要將驗證2.0驗證設定變更為工作台中特定程式的基本驗證，您可以設定 **OAuth 2.0驗證** 值為「False」 **使用全域設定** 在 **連線設定** 標籤。

## 啟用oAuth任務通知的方式 {#enable_oauth_task}

1. 前往 **首頁** > **服務** > **表單工作流程** > **伺服器設定** > **電子郵件設定**
1. 若要啟用oAuth任務通知，請選取 **啟用oAuth** 核取方塊。
1. 複製 **用戶端ID** 和 **用戶端密碼** 從Azure門戶。
1. 複製所產生的值 **重新整理Token**.
1. 按一下 **儲存** 以儲存詳細資訊。

   ![任務通知](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > 要了解與任務通知相關的更多資訊， [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## 設定電子郵件端點 {#configure_email_endpoint}

1. 前往 **首頁** > **服務** > **應用程式和服務** > **端點管理**
1. 若要設定電子郵件端點，請設定 **oAuth 2.0驗證設定** as `True`.
1. 複製 **用戶端ID** 和 **用戶端密碼** 從Azure門戶。
1. 複製所產生的值 **重新整理Token**.
1. 按一下 **儲存** 以儲存詳細資訊。

   ![連線設定](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > 若要了解有關設定電子郵件端點的詳細資訊，請按一下 [設定電子郵件端點](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## 疑難排解 {#troubleshooting}

* 如果電子郵件服務無法正常運作。 嘗試重新產生 `Refresh Token` 如上所述。 部署新值需要幾分鐘的時間。

* 使用Workbench在電子郵件端點中設定電子郵件伺服器詳細資訊時發生錯誤。請嘗試透過管理員UI（而非Workbench）來設定端點。
