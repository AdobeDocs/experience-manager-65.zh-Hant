---
title: 設定電子郵件通知
seo-title: Configuring Email Notification
description: 了解如何在AEM中設定電子郵件通知。
seo-description: Learn how to configure Email Notification in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
source-git-commit: 676299c741684708d420ac208f44b0c7a285de0c
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 1%

---

# 設定電子郵件通知{#configuring-email-notification}

AEM會傳送電子郵件通知給下列使用者：

* 已訂閱頁面事件，例如修改或復寫。 此 [通知收件匣](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) 一節說明如何訂閱此類事件。

* 已訂閱論壇活動。
* 必須在工作流程中執行步驟。 此 [參與者步驟](/help/sites-developing/workflows-step-ref.md#participant-step) 一節說明如何在工作流程中觸發電子郵件通知。

先決條件：

* 使用者的設定檔中必須定義有效的電子郵件地址。
* 此 **Day CQ Mail Service** 必須正確設定。

收到通知時，使用者會收到其設定檔中定義的語言電子郵件。 每種語言都有各自的範本，可供自訂。 可針對新語言新增新的電子郵件範本。

>[!NOTE]
>
>使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議的實務。

## 設定郵件服務 {#configuring-the-mail-service}

若要讓AEM能夠傳送電子郵件， **Day CQ Mail Service** 必須正確設定。 您可以在Web主控台中檢視設定。 使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議的實務。

下列限制適用：

* 此 **SMTP伺服器埠** 必須是25或更高。

* 此 **SMTP伺服器主機名** 不得空白。
* 此 **「寄件者」地址** 不得空白。

協助您對 **Day CQ Mail Service**，您可以觀看服務記錄：

`com.day.cq.mailer.DefaultMailService`

在Web控制台中，配置如下所示：

![chlimage_1-276](assets/chlimage_1-276.png)

## 設定電子郵件通知通道 {#configuring-the-email-notification-channel}

當您訂閱頁面或論壇事件通知時，寄件者電子郵件地址會設為 `no-reply@acme.com` 預設值。 您可以借由設定 **通知電子郵件通道** 服務。

若要設定寄件者電子郵件地址，請新增 `sling:OsgiConfig` 節點到儲存庫。 使用以下過程直接使用CRXDE Lite添加節點：

1. 在CRXDE Lite中，新增名為 `config` 應用程式資料夾下方。
1. 在設定資料夾中，新增節點：

   `com.day.cq.wcm.notification.email.impl.EmailChannel` 類型 `sling:OsgiConfig`

1. 新增 `String` 屬性至名為的節點 `email.from`. 對於值，指定您要使用的電子郵件地址。

1. 按一下 **全部儲存**.

使用以下過程來定義內容包源資料夾中的節點：

1. 在 `jcr_root/apps/*app_name*/config folder`，建立名為的檔案 `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. 添加以下XML以表示節點：

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 取代 `email.from` 屬性( `name@server.com`)和您的電子郵件地址。

1. 儲存檔案。

## 設定工作流程電子郵件通知服務 {#configuring-the-workflow-email-notification-service}

當您收到工作流程電子郵件通知時，寄件者電子郵件地址和主機URL首碼都會設為預設值。 您可以透過設定 **Day CQ工作流程電子郵件通知服務** 中。 若您這麼做，建議您將變更保留在存放庫中。

預設配置在Web控制台中如下所示：

![chlimage_1-277](assets/chlimage_1-277.png)

### 頁面通知的電子郵件範本 {#email-templates-for-page-notification}

頁面通知的電子郵件範本位於下方：

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

預設英文範本( `en.txt`)的定義如下：

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 自訂頁面通知的電子郵件範本 {#customizing-email-templates-for-page-notification}

若要自訂頁面通知的英文電子郵件範本：

1. 在CRXDE中，開啟檔案：

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. 根據您的需求修改檔案。
1. 儲存變更。

範本必須具備下列格式：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

其中 &lt;text_x> 可以是靜態文字和動態字串變數的混合。 可在電子郵件範本內使用下列變數以取得頁面通知：

* `${time}`，事件日期和時間。

* `${userFullName}`，觸發事件的使用者完整名稱。

* `${userId}`，即觸發事件的使用者ID。
* `${modifications}`，以下列格式說明頁面事件類型和頁面路徑：

   &lt;page event=&quot;&quot; type=&quot;&quot;> => &lt;page path=&quot;&quot;>

   例如：

   PageModified => /content/geometrixx/en/products

### 論壇通知的電子郵件範本 {#email-templates-for-forum-notification}

論壇通知的電子郵件範本位於：

`/etc/notification/email/default/com.day.cq.collab.forum`

預設英文範本( `en.txt`)的定義如下：

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 為論壇通知自訂電子郵件範本 {#customizing-email-templates-for-forum-notification}

若要自訂論壇通知的英文電子郵件範本：

1. 在CRXDE中，開啟檔案：

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. 根據您的需求修改檔案。
1. 儲存變更。

範本必須具備下列格式：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

其中 `<text_x>` 可以是靜態文字和動態字串變數的混合。

下列變數可在電子郵件範本中用於論壇通知：

* `${time}`，事件日期和時間。

* `${forum.path}`，即論壇頁面的路徑。

### 工作流通知的電子郵件範本 {#email-templates-for-workflow-notification}

工作流程通知的電子郵件範本（英文）位於：

`/libs/settings/workflow/notification/email/default/en.txt`

定義如下：

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 自訂工作流程通知的電子郵件範本 {#customizing-email-templates-for-workflow-notification}

若要自訂工作流程事件通知的英文電子郵件範本：

1. 在CRXDE中，開啟檔案：

   `/libs/settings/workflow/notification/email/default/en.txt`

1. 根據您的需求修改檔案。
1. 儲存變更。

範本必須具備下列格式：

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>其中 `<text_x>` 可以是靜態文字和動態字串變數的混合。 每行 `<text_x>` 項目需要以反斜線( `\`)，但最後一個例項除外，因為沒有反斜線表示結尾 `<text_x>` 字串變數。
>
>如需範本格式的詳細資訊，請參閱 [Properties.load()的javadoc](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) 方法。

方法 `${payload.path.open}` 會顯示工作項目裝載的路徑。 例如，接著，針對Sites中的頁面 `payload.path.open` 會類似於 `/bin/wcmcommand?cmd=open&path=…`.;這沒有伺服器名稱，因此範本會在前置加上 `${host.prefix}`.

可在電子郵件範本內使用下列變數：

* `${event.EventType}`，事件類型
* `${event.TimeStamp}`、事件的日期和時間
* `${event.User}`，觸發事件的使用者
* `${initiator.home}`，啟動器節點路徑

* `${initiator.name}`，啟動器名稱

* `${initiator.email}`，發起人的電子郵件地址
* `${item.id}`，工作項的id
* `${item.node.id}`，此工作項目關聯的工作流模型中節點的id
* `${item.node.title}`，工作項的標題
* `${participant.email}`，參與者的電子郵件地址
* `${participant.name}`，參與者姓名
* `${participant.familyName}`，參與者的姓氏
* `${participant.id}`，參與者的id
* `${participant.language}`，參與者語言
* `${instance.id}`，工作流程id
* `${instance.state}`，工作流程狀態
* `${model.title}`，工作流程模型的標題
* `${model.id}`，工作流程模型的id

* `${model.version}`，工作流程模型的版本
* `${payload.data}`，裝載

* `${payload.type}`，裝載類型
* `${payload.path}`，裝載的路徑
* `${host.prefix}`，主機首碼，例如：http://localhost:4502

### 新增新語言的電子郵件範本 {#adding-an-email-template-for-a-new-language}

為新語言添加模板：

1. 在CRXDE中，新增檔案 `<language-code>.txt` 如下：

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` :頁面通知
   * `/etc/notification/email/default/com.day.cq.collab.forum` :論壇通知
   * `/libs/settings/workflow/notification/email/default` :工作流通知

1. 使檔案適應語言。
1. 儲存變更。

>[!NOTE]
>
>此 `<language-code>` 作為電子郵件範本的檔案名稱必須是AEM可辨識的小寫字母語言代碼。 對於語言代碼，AEM需依賴ISO-639-1。

## 設定AEM Assets電子郵件通知 {#assetsconfig}

AEM Assets中的集合為共用或非共用時，使用者會收到AEM的電子郵件通知。 若要設定電子郵件通知，請遵循下列步驟。

1. 依照上文所述，設定電子郵件服務 [設定郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service).
1. 以管理員身分登入AEM。 按一下 **工具** >  **操作** >  **Web主控台** 開啟Web控制台配置。
1. 編輯 **日CQ DAM資源收集Servlet**. 選擇 **傳送電子郵件**. 按一下「**儲存**」。

## 設定OAuth {#setting-up-oauth}

AEM提供OAuth2的整合式Mailer服務支援，讓組織能夠遵守安全的電子郵件需求。

您可以為多個電子郵件提供者設定OAuth，如下所述。

>[!NOTE]
>
>以下概述的程式是Publish例項的範例。 若您想這麼做，也可以對Author例項執行此程式。

### Gmail {#gmail}

1. 在 `https://console.developers.google.com/projectcreate`
1. 選取您的專案，然後前往 **API與服務** - **控制面板 — 憑證**
1. 根據您的需求設定OAuth同意畫面
1. 在下面的更新螢幕中，添加以下兩個作用域：
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. 添加範圍後，返回 **憑證** 在左側功能表中，然後前往 **建立憑證** - **OAuth用戶端ID** - **案頭應用程式**
1. 將會開啟一個新視窗，其中包含用戶端ID和用戶端密碼。
1. 保存這些憑據。

**AEM端組態**

>[!NOTE]
>
>Adobe管理服務客戶可與其客戶服務工程師合作，對生產環境進行這些變更。

首先，配置郵件服務：

1. 開啟AEM Web Console，方法是前往 `http://serveraddress:serverport/system/console/configMgr`
1. 尋找，然後按一下 **Day CQ Mail Service**
1. 新增下列設定：
   * SMTP 伺服器主機名稱: `smtp.gmail.com`
   * SMTP伺服器埠： `25` 或 `587`，視需求而定
   * 勾選 **SMPT使用StarTLS** 和 **SMTP需要StarTLS**
   * 檢查 **OAuth流量** 按一下 **儲存**.

接下來，請依照下列程式來設定您的SMTP OAuth提供者：

1. 開啟AEM Web Console，方法是前往 `http://serveraddress:serverport/system/console/configMgr`
1. 尋找，然後按一下 **CQ郵件程式SMTP OAuth2提供程式**
1. 填寫所需資訊如下：
   * 授權URL: `https://accounts.google.com/o/oauth2/auth`
   * 代號URL: `https://accounts.google.com/o/oauth2/token`
   * 範圍： `https://www.googleapis.com/auth/gmail.send` 和 `https://mail.google.com/`. 您可以按 **+** 按鈕（位於每個已配置作用域的右側）。
   * 用戶端ID和用戶端密碼：使用您依上段所述擷取的值來設定這些欄位。
   * 重新整理記號 URL: `https://accounts.google.com/o/oauth2/token`
   * 重新整理代號過期：從不
1. 按一下「**儲存**」。

<!-- clarify refresh token expiry, currrently not present in the UI -->

設定後，設定應如下所示：

![oauth smtp提供程式](assets/oauth-smtpprov2.png)

現在，啟動OAuth元件。 您可以透過下列方式執行此作業：

1. 請造訪此URL，前往元件主控台： `http://serveraddress:serverport/system/console/components`
1. 尋找下列元件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按元件左側的「播放」圖示

   ![元件](assets/oauth-components-play.png)

最後，請依下列方式確認設定：

1. 前往Publish例項的位址，並以管理員身分登入。
1. 在瀏覽器中開啟新標籤，然後前往 `http://serveraddress:serverport/services/mailer/oauth2/authorize`. 這會將您重新導向至SMTP提供者的頁面，在此例中為Gmail。
1. 登入並同意授予必要的權限
1. 同意後，Token會儲存在存放庫中。 您可以在 `accessToken` 直接在您的發佈執行個體上存取此URL: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. 對每個發佈例項重複上述步驟

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. 前往 [https://portal.azure.com/](https://portal.azure.com/) 並登入。
1. 搜尋 **Azure Active Directory** 在搜尋列中，按一下結果。 或者，您可以直接瀏覽至 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下 **應用程式註冊** - **新註冊**

   ![](assets/oauth-outlook1.png)

1. 根據您的需求填寫資訊，然後按一下 **註冊**
1. 前往新建立的應用程式，然後選取 **API權限**
1. 前往 **新增權限** - **圖表權限** - **委派權限**
1. 選取您應用程式的下列權限，然後按一下 **新增權限**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 前往 **驗證** - **新增平台** - **Web**，和 **重新導向Url** 區段中，新增下列URL以重新導向OAuth程式碼，然後按 **設定**:
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 對每個發佈例項重複上述步驟
1. 根據您的需求配置設定
1. 接下來，轉到 **憑證和機密**，按一下 **新用戶端密碼** 並依照畫面上的步驟建立密碼。 請務必注意此機密以供日後使用
1. Press **概述** 並複製 **應用程式（客戶端）ID** 和 **目錄（租用戶）ID** 供稍後使用

若要重述，您需要下列資訊才能為AEM端的Mailer服務設定OAuth2:

* 驗證URL，將以租用戶ID建構。 它會有此表格： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 代號URL，將以租用戶ID建構。 它會有此表格： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 將以租用戶ID建構的重新整理URL。 它會有此表格： `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 用戶端ID
* 用戶端密碼

**AEM端組態**

接下來，整合您的OAuth2設定與AEM:

1. 瀏覽至，前往本機執行個體的Web主控台 `http://serveraddress:serverport/system/console/configMgr`
1. 尋找並按一下 **Day CQ Mail Service**
1. 新增下列設定：
   * SMTP 伺服器主機名稱: `smtp.office365.com`
   * SMTP用戶：電子郵件格式中的用戶名
   * 「寄件者」地址：要在郵件者所傳送訊息的「寄件者：」欄位中使用的電子郵件地址
   * SMTP伺服器埠： `25` 或 `587` 視需求而定
   * 勾選 **SMPT使用StarTLS** 和 **SMTP需要StarTLS**
   * 檢查 **OAuth流量** 按一下 **儲存**.
1. 尋找，然後按一下 **CQ郵件程式SMTP OAuth2提供程式**
1. 填寫所需資訊如下：
   * 建構授權URL、代號URL和重新整理代號URL，如下所述： [本程式的結尾](#microsoft-outlook)
   * 用戶端ID和用戶端密碼：使用您依上述方式擷取的值來設定這些欄位。
   * 將以下作用域添加到配置中：
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode重新導向Url: `http://localhost:4503/services/mailer/oauth2/token`
   * 重新整理Token URL:此值應與上方的代號URL相同
1. 按一下「**儲存**」。

設定後，設定應如下所示：

![](assets/oauth-outlook-smptconfig.png)

現在，啟動OAuth元件。 您可以透過下列方式執行此作業：

1. 請造訪此URL，前往元件主控台： `http://serveraddress:serverport/system/console/components`
1. 尋找下列元件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按元件左側的「播放」圖示

![元件2](assets/oauth-components-play.png)

最後，請依下列方式確認設定：

1. 前往Publish例項的位址，並以管理員身分登入。
1. 在瀏覽器中開啟新標籤，然後前往 `http://serveraddress:serverport/services/mailer/oauth2/authorize`. 這會將您重新導向至SMTP提供者的頁面，在此例中為Gmail。
1. 登入並同意授予必要的權限
1. 同意後，Token會儲存在存放庫中。 您可以在 `accessToken` 直接在您的發佈執行個體上存取此URL: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`