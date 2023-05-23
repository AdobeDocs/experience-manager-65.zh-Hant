---
title: 為Microsoft® Office 365郵件伺服器協定配置基於OAuth2的身份驗證
description: 為Microsoft® Office 365郵件伺服器協定配置基於OAuth2的身份驗證
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: d19de2955adef56570378a6d62ec0015718f9039
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---

# 與Microsoft® Office 365郵件伺服器協定整合 {#oauth2-support-for-the-microsoft-mail-server-protocols}

為使組織能夠遵守安全電子郵件要求，AEM Forms為與Microsoft® Office 365郵件伺服器協定整合提供OAuth 2.0支援。 您可以使用Azure Active Directory(Azure AD)OAuth 2.0身份驗證服務，以連接IMAP、POP或SMTP等各種協定，並訪問Office 365用戶的電子郵件資料。 以下是配置Microsoft® Office 365郵件伺服器協定以通過OAuth 2.0服務進行身份驗證的逐步說明：

1. 登錄 [https://portal.azure.com/](https://portal.azure.com/) 並搜索 **Azure Active Directory** 的子菜單。
或者，您可以直接瀏覽到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下 **添加** > **應用註冊** > **新建註冊**

   ![應用程式註冊](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 根據您的要求填寫資訊，然後按一下 **註冊**。
   ![支援的帳戶](/help/forms/using/assets/azure_suuportedaccountype.png)
在上述情況下， 
**任何組織目錄（任何Azure AD目錄 — 多租戶）中的帳戶和個人Microsoft®帳戶（例如，Skype、Xbox）** 的雙曲餘切值。

   >[!NOTE]
   >
   > * 對於 **任何組織目錄中的帳戶（任何Azure AD目錄 — 多租戶）** 應用程式，建議使用工作帳戶而不是個人電子郵件帳戶。
   > * **僅限個人Microsoft®帳戶** 不支援應用程式。
   > * 建議使用 **多租戶和個人Microsoft®帳戶** 的子菜單。


1. 下一步，轉到 **證書和機密**&#x200B;按一下 **新客戶機密鑰** 按螢幕上的步驟建立秘密。 請務必注意此機密值，以備以後使用。

   ![機密金鑰](/help/forms/using/assets/azure_secretkey.png)

1. 要添加權限，請轉到新建立的應用，然後選擇 **API權限** > **添加權限** > **Microsoft®圖形** > **授權權限**
1. 選中應用的以下權限的複選框，然後按一下 **添加權限**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API權限](/help/forms/using/assets/azure_apipermission.png)

1. 選擇 **驗證** > **添加平台** > **Web**&#x200B;的 **重定向URL** 部分，將以下任何URI（通用資源標識符）添加為：
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   在這個例子中， `https://login.microsoftonline.com/common/oauth2/nativeclient` 用作重定向URI。

1. 按一下 **配置** 添加每個URL後，根據您的要求配置設定。
   ![重新導向 URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > 必須選擇 **訪問令牌** 和 **ID令牌** 複選框。

1. 按一下 **概述** 在左窗格中，複製 **應用程式（客戶端）ID**。 **目錄（租戶）ID**, **客戶端密碼** 供以後使用。

   ![概觀](/help/forms/using/assets/azure_overview.png)

## 生成授權代碼 {#generating-the-authorization-code}

接下來，您需要生成授權代碼，具體說明如下步驟：

1. 替換後在瀏覽器中開啟以下URL `clientID` 和 `<client_id>` 和 `redirect_uri` 的重定向URI:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > 如果是單租戶應用程式，請替換 `common` 和 `[tenantid]` 的下界： `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. 鍵入上述URL後，將重定向到登錄螢幕：
   ![登錄螢幕](/help/forms/using/assets/azure_loginscreen.png)

1. 輸入電子郵件，按一下 **下一個** 並顯示「App permission（應用程式權限）」螢幕：

   ![允許權限](/help/forms/using/assets/azure_permission.png)

1. 允許權限後，您將被重定向到新URL，其為： `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 複製的值 `<code>` 從以上URL `0.ASY...` 至 `&session_state` 的子菜單。

## 產生重新整理權杖 {#generating-the-refresh-token}

接下來，您需要生成刷新令牌，具體說明如下步驟：

1. 開啟命令提示符，然後使用以下cURL命令獲取refreshToken。

1. 替換 `clientID`。 `client_secret` 和 `redirect_uri` 與應用程式的值以及 `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > 在單個租戶應用程式中，要生成刷新令牌，請使用以下cURL命令並替換 `common` 和 `[tenantid]` 中：
   >`curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. 記下刷新標籤。

## 使用OAuth 2.0支援配置電子郵件服務 {#configureemailservice}

現在，您必須通過登錄管理UI在最新的JEE伺服器上配置電子郵件服務：

1. 轉到 **首頁** > **服務** > **應用程式和服務** > **服務管理** > **電子郵件服務**，也請參見Wiki頁。 **配置電子郵件服務** 的子菜單。

   >[!NOTE]
   >
   > 要啟用oAuth 2.0身份驗證服務，必須選擇 **SMTP伺服器是否需要驗證（SMTP驗證）** 複選框。

1. 設定 **oAuth 2.0身份驗證設定** 如 `True`。
1. 複製的值 **客戶端ID** 和 **客戶端密碼** 從Azure門戶。
1. 複製已生成的值 **刷新令牌**。
1. 登錄到 **工作台** 搜索 **電子郵件1.0** 從 **活動選取器**。
1. 在E-mail 1.0下，有三個選項：
   * **隨文檔一起發送**:發送帶有單個附件的電子郵件。
   * **使用附件映射發送**:發送包含多個附件的電子郵件。
   * **接收**:從IMAP接收電子郵件。

   >[!NOTE]
   >
   >* 傳輸安全協定的有效值為：「blank」、「SSL」或「TLS」。 必須設定 **SMTP傳輸安全** 和 **接收傳輸安全性** 至 **TLS** 用於啟用oAuth身份驗證服務。
   >* **POP3協定** 使用電子郵件終結點時，OAuth不支援。


   ![連接設定](/help/forms/using/assets/oauth_connectionsettings.png)

1. Test應用程式，方法是 **隨文檔一起發送**。
1. 提供 **至** 和 **從** 地址。
1. 調用應用程式並使用0Auth 2.0身份驗證發送電子郵件。

   >[!NOTE]
   >
   >如果要將Auth 2.0身份驗證設定更改為工作台中特定進程的基本身份驗證，可以設定 **OAuth 2.0身份驗證** 值在下 **使用全局設定** 的 **連接設定** 頁籤。

## 啟用身份驗證任務通知 {#enable_oauth_task}

1. 轉到 **首頁** > **服務** > **表單工作流** > **伺服器設定** > **電子郵件設定**
1. 要啟用身份驗證任務通知，請選擇 **啟用身份驗證** 複選框。
1. 複製的值 **客戶端ID** 和 **客戶端密碼** 從Azure門戶。
1. 複製已生成的值 **刷新令牌**。
1. 按一下 **保存** 的子菜單。

   ![任務通知](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > 要瞭解與任務通知相關的詳細資訊， [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service)。

## 配置電子郵件終結點 {#configure_email_endpoint}

1. 轉到 **首頁** > **服務** > **應用程式和服務** > **終結點管理**
1. 要配置電子郵件終結點，請設定 **oAuth 2.0身份驗證設定** 如 `True`。
1. 複製的值 **客戶端ID** 和 **客戶端密碼** 從Azure門戶。
1. 複製已生成的值 **刷新令牌**。
1. 按一下 **保存** 的子菜單。

   ![連接設定](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > 要瞭解有關配置電子郵件終結點的詳細資訊，請按一下 [配置電子郵件終結點](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html)。

## 疑難排解 {#troubleshooting}

* 如果電子郵件服務工作不正常。 嘗試重新生成 `Refresh Token` 如上所述。 部署新值需要幾分鐘。

* 使用Workbench在電子郵件終結點中配置電子郵件伺服器詳細資訊時出錯。請嘗試通過管理UI而不是Workbench配置終結點。
