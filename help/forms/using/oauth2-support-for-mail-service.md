---
title: 設定Microsoft&reg (Forms JEE OAuth)的OAuth2驗證；Office 365郵件伺服器通訊協定
description: 設定Microsoft&reg (Forms JEE OAuth)的OAuth2驗證；Office 365郵件伺服器通訊協定
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# 將AEM Forms與Microsoft® Office 365郵件伺服器通訊協定整合 {#oauth2-support-for-the-microsoft-mail-server-protocols}

為了讓組織遵守安全電子郵件要求，AEM Forms提供OAuth 2.0支援，以便與Microsoft® Office 365郵件伺服器通訊協定整合。 您可以使用Azure Active Directory (Azure AD) OAuth 2.0驗證服務來連線各種通訊協定（例如IMAP、POP或SMTP），並存取Office 365使用者的電子郵件資料。 以下是設定Microsoft® Office 365郵件伺服器通訊協定以透過OAuth 2.0服務進行驗證的逐步指示：

1. 登入[https://portal.azure.com/](https://portal.azure.com/)並在搜尋列中搜尋&#x200B;**Azure Active Directory**，然後按一下結果。
或者，您可以直接瀏覽到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下&#x200B;**新增** > **應用程式註冊** > **新註冊**。

   ![應用程式註冊](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 根據您的要求填寫資訊，然後按一下「**註冊**」。
   ![支援的帳戶](/help/forms/using/assets/azure_suuportedaccountype.png)
在上述案例中，已選取任何組織目錄（任何Azure AD目錄 — 多租使用者）中的**帳戶和個人Microsoft®帳戶（例如Skype、Xbox）**&#x200B;選項。

   >[!NOTE]
   >
   > * 對於任何組織目錄（任何Azure AD目錄 — 多租使用者）**應用程式中的**&#x200B;帳戶，Adobe建議您使用工作帳戶，而不是個人電子郵件帳戶。
   > * 不支援&#x200B;**僅個人Microsoft®帳戶**&#x200B;應用程式。
   > * Adobe建議您使用&#x200B;**多租使用者和個人Microsoft®帳戶**&#x200B;應用程式。

1. 接下來，移至「**憑證和密碼**」，按一下「**新增用戶端密碼**」，並按照畫面上的步驟建立密碼。請務必記下此secret值以供稍後使用。

   ![秘密金鑰](/help/forms/using/assets/azure_secretkey.png)

1. 若要新增許可權，請前往新建立的應用程式，然後選取&#x200B;**API許可權** > **新增許可權** > **Microsoft® Graph** > **委派許可權**。
1. 選取以下應用程式許可權的核取方塊，然後按一下&#x200B;**新增許可權**：

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API許可權](/help/forms/using/assets/azure_apipermission.png)

1. 選取「**驗證**」>「**新增平台**」>「**網頁**」，並在「**重新導向URL**」區段中，新增下列任一URI （通用資源識別碼）為：
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   在此情況下，`https://login.microsoftonline.com/common/oauth2/nativeclient`會作為重新導向URI使用。

1. 新增每個URL後按一下「設定&#x200B;**」**，並根據您的需求進行設定。
   ![重新導向URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > 必須選取&#x200B;**存取權杖**&#x200B;和&#x200B;**ID權杖**&#x200B;核取方塊。

1. 按一下左窗格中的&#x200B;**總覽**，並複製&#x200B;**應用程式（使用者端） ID**、**目錄（租使用者） ID**&#x200B;和&#x200B;**使用者端密碼**&#x200B;的值以供稍後使用。

   ![概觀](/help/forms/using/assets/azure_overview.png)

## 產生授權代碼 {#generating-the-authorization-code}

接下來，您必須產生授權代碼，如以下步驟所述：

1. 將`clientID`取代為`<client_id>`，並將`redirect_uri`取代為您的應用程式的重新導向URI，然後在瀏覽器中開啟下列URL：

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > 如果存在單一租使用者應用程式，請在下列URL中將`common`取代為您的`[tenantid]`，以產生授權代碼： `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. 當您輸入上述URL時，您會被重新導向至登入畫面：
   ![登入畫面](/help/forms/using/assets/azure_loginscreen.png)

1. 輸入電子郵件，按一下&#x200B;**下一步**，就會顯示[應用程式]許可權畫面：

   ![允許許可權](/help/forms/using/assets/azure_permission.png)

1. 當您允許許可權時，您會被重新導向至新的URL，如下所示： `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 將上述URL中`<code>`的值從`0.ASY...`複製到上述URL中的`&session_state`。

## 產生重新整理權杖 {#generating-the-refresh-token}

接下來，您必須產生重新整理權杖，如下列步驟所述：

1. 開啟命令提示字元並使用下列cURL命令取得refreshToken。

1. 將`clientID`、`client_secret`和`redirect_uri`取代為您應用程式的值以及`<code>`的值：

   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > 在單一租使用者應用程式中，若要產生重新整理權杖，請使用下列cURL命令並將`common`取代為中的`[tenantid]`：
   >`curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. 記下重新整理權杖。

## 設定電子郵件服務與OAuth 2.0支援 {#configureemailservice}

現在，請登入管理員UI，在最新的JEE伺服器上設定電子郵件服務：

1. 移至&#x200B;**首頁** > **服務** > **應用程式與服務** > **服務管理** > **電子郵件服務**，會出現&#x200B;**設定電子郵件服務**&#x200B;視窗，設定為進行基本驗證。

   >[!NOTE]
   >
   > 若要啟用oAuth 2.0驗證服務，必須選取&#x200B;**SMTP伺服器是否需要驗證（SMTP驗證）**&#x200B;核取方塊。

1. 將&#x200B;**oAuth 2.0驗證設定**&#x200B;設為`True`。
1. 從Azure入口網站複製&#x200B;**使用者端識別碼**&#x200B;和&#x200B;**使用者端密碼**&#x200B;的值。
1. 複製產生的&#x200B;**重新整理Token**&#x200B;的值。
1. 登入&#x200B;**Workbench**&#x200B;並從&#x200B;**活動選擇器**&#x200B;搜尋&#x200B;**電子郵件1.0**。
1. 電子郵件1.0下有三個選項：
   * **隨檔案傳送**：傳送包含單一附件的電子郵件。
   * **使用附件地圖傳送**：傳送包含多個附件的電子郵件。
   * **接收**：接收來自IMAP的電子郵件。

   >[!NOTE]
   >
   >* 傳輸安全性通訊協定有下列有效值： &#39;blank&#39;、&#39;SSL&#39;或&#39;TLS&#39;。 將&#x200B;**SMTP Transport Security**&#x200B;和&#x200B;**Receive Transport Security**&#x200B;的值設定為&#x200B;**TLS**，以啟用oAuth驗證服務。
   >* 使用電子郵件端點時，OAuth不支援&#x200B;**POP3通訊協定**。

   ![連線設定](/help/forms/using/assets/oauth_connectionsettings.png)

1. 選取&#x200B;**隨檔案**&#x200B;傳送，以測試應用程式。
1. 提供&#x200B;**TO**&#x200B;和&#x200B;**From**&#x200B;位址。
1. 叫用應用程式，並使用0Auth 2.0驗證傳送電子郵件。

   >[!NOTE]
   >
   >如有需要，您可以將Workbench中特定程式的Auth 2.0驗證設定變更為基本驗證。 若要這麼做，請在&#x200B;**連線設定**&#x200B;索引標籤中的&#x200B;**使用全域設定**&#x200B;下，將&#x200B;**OAuth 2.0驗證**&#x200B;值設為&#39;False&#39;。

## 啟用oAuth任務通知的方式 {#enable_oauth_task}

1. 移至&#x200B;**首頁** > **服務** > **表單工作流程** > **伺服器設定** > **電子郵件設定**
1. 若要啟用oAuth工作通知，請選取&#x200B;**啟用oAuth**&#x200B;核取方塊。
1. 從Azure入口網站複製&#x200B;**使用者端識別碼**&#x200B;和&#x200B;**使用者端密碼**&#x200B;的值。
1. 複製產生的&#x200B;**重新整理Token**&#x200B;的值。
1. 按一下[儲存]儲存詳細資料。****

   ![工作通知](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > 若要瞭解更多與工作通知相關的資訊，[請按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service)。

## 設定電子郵件端點 {#configure_email_endpoint}

1. 移至&#x200B;**首頁** > **服務** > **應用程式與服務** > **端點管理**
1. 若要設定電子郵件端點，請將&#x200B;**oAuth 2.0驗證設定**&#x200B;設為`True`。
1. 從Azure入口網站複製&#x200B;**使用者端識別碼**&#x200B;和&#x200B;**使用者端密碼**&#x200B;的值。
1. 複製產生的&#x200B;**重新整理Token**&#x200B;的值。
1. 按一下[儲存]儲存詳細資料。****

   ![連線設定](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > 若要瞭解有關設定電子郵件端點的詳細資訊，請按一下[設定電子郵件端點]。[](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html)

## 疑難排解 {#troubleshooting}

* 如果電子郵件服務無法正常運作，請嘗試重新產生`Refresh Token`，如上所述。 部署新值需要幾分鐘的時間。

* 使用Workbench在電子郵件端點中設定電子郵件伺服器詳細資料時發生錯誤。 嘗試透過Admin UI （而非Workbench）設定端點。
