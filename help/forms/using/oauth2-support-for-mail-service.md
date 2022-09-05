---
title: OAuth2對郵件服務的支援
description: 'Oauth2對郵件服務的支援  '
source-git-commit: 081b0c70ceca0502cb84d7e1b68b0b12dc45a4e7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# OAuth2對郵件服務的支援 {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service為其整合式Mail Service提供OAuth2支援，讓組織能遵守安全的電子郵件需求。

您可以為多個電子郵件提供者設定OAuth。 以下是設定AEM Mail Service以透過OAuth2使用Microsoft Office 365 Outlook進行驗證的逐步指示。 其他廠商也能以類似方式進行設定。

## Microsoft Outlook {#microsoft-outlook}

1. 前往 [https://portal.azure.com/](https://portal.azure.com/) 並登入。
1. 搜尋 **Azure Active Directory** 在搜尋列中，按一下結果。 或者，您可以直接瀏覽至 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下 **應用程式註冊** - **新註冊**

   ![](/help/forms/using/assets/outh_outlook.PNG)

1. 根據您的需求填寫資訊，然後按一下 **註冊**
1. 前往新建立的應用程式，然後選取 **API權限**
1. 前往 **新增權限** - **圖表權限** - **委派權限**
1. 選取您應用程式的下列權限，然後按一下 **新增權限**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 前往 **驗證** - **新增平台** - **Web**，和 **重新導向Url** 區段中，新增下列URL — 一個含有，一個不含正斜線：
   * `http://localhost/`
   * `http://localhost`
1. Press **設定** 新增每個URL，並根據您的需求進行設定
1. 接下來，轉到 **憑證和機密**，按一下 **新用戶端密碼** 並依照畫面上的步驟建立密碼。 請務必注意此機密以供日後使用
1. Press **概述** 並複製 **應用程式（客戶端）ID** 供稍後使用。

若要重述，您需要下列資訊才能為AEM端的Mail服務設定OAuth2:

* 驗證URL的格式為： `https://login.microsoftonline.com/<ID>/oauth2/v2.0/authorize`
* 表單中的代號URL: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* 以下形式顯示「刷新URL」： `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* 用戶端ID
* 用戶端密碼

### 產生重新整理代號 {#generating-the-refresh-token}

接下來，您需要產生重新整理代號，如後續步驟所示。

您可以依照下列步驟來執行此操作：

1. 取代後，在瀏覽器中開啟下列URL `clientID` 以及您帳戶的特定值：

   ```https://login.microsoftonline.com/common/oauth2/v2/authorize?client_id=<client_id>&scope=IMAP.AccessAsUser.A;;%20POP.AccessAsUser.All%20SMTP.Send%20User.Read&response_type=code&redirect-uri=http://loginmicrosoftonline.com/common/outh2/nativeclient&prompt=login```

1. 允許權限，無論何時需要。
1. URL會重新導向至以此格式建構的新位置： `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 複製 `<code>` 在上述範例中
1. 使用下列cURL命令來取得refreshToken。 將clientID、clientSecret取代為您帳戶的值，並取代 `<code>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client-id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=M.R3_BAY.1bf609bf-25b3-2fcd-d910-02e02c53bc
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=~1E8Q~cz-m6vgOb9m~SI.eF9jSVTbFUiP5f0” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. 記下refreshToken和accessToken。

### 驗證Token {#validating-the-tokens}

在AEM端繼續設定OAuth之前，請務必透過下列程式驗證accessToken和refreshToken:

1. 使用先前程式中產生的refreshToken來產生accessToken。 您可以透過下列curl和取代 `<client_id>`,`<client_secret>` 以及 `<refreshToken>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client_id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=<code>
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=<client_secret>
   &refresh_token=<refresh_token” 
   -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. 使用accessToken傳送郵件，以查看其是否正常運作。

>[!NOTE]
>
> 您可以從以下位置取得Postman API集合： [此位置](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### 使用Auth2.0支援配置電子郵件服務 {#configureemailservice}

現在，您必須透過管理員UI中的登入，在最新的JEE伺服器設定電子郵件服務：

1. 前往 **首頁** - **服務** - **應用程式和服務** - **服務管理** - **電子郵件服務**
1. **設定電子郵件服務** 窗口，配置 **SMPT** 和 **IMP** 用於基本驗證的伺服器。
1. 要啟用Outlook郵件身份驗證服務，請選擇 **oAuth 2.0驗證設定** 核取方塊。
1. 複製 **用戶端ID** 和 **用戶端密碼** 從Azure門戶。
1. 複製所產生的值 **重新整理Token**.
1. 按一下 **儲存** 以儲存詳細資訊。
1. 登入Workbench並搜尋 **電子郵件1.0** 從 **活動選擇器**.
1. 電子郵件1.0下提供下列三個選項：
   * **隨文檔一起發送**:傳送包含單一附件的電子郵件。
   * **隨附附件地圖傳送**:傳送包含多個附件的電子郵件。
   * **接收**:從POP3或IMAP接收電子郵件。
1. 選取 **隨文檔一起發送**
1. 提供 **結束日期** 和 **從** 地址。
1. 叫用應用程式，並使用oAuth2.0驗證傳送電子郵件。

>[!NOTE]
>
> 如果您想要將Auth 2.0驗證設定變更為工作台中特定程式的基本驗證，可取消勾選 **oAuth2.0驗證** 核取方塊 **使用全域設定** 在 **連線設定** 標籤。

### 疑難排解 {#troubleshooting}

如果郵件服務無法正常運作，請重新產生 `refreshToken` 如上所述。 部署新值需要幾分鐘的時間。


