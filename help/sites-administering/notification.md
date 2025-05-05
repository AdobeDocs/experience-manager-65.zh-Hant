---
title: 設定電子郵件通知
description: 瞭解如何在Adobe Experience Manager中設定電子郵件通知。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: efaff4557aba3557a355ed385a5358cf1108c159
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 8%

---


# 設定電子郵件通知{#configuring-email-notification}

AEM傳送電子郵件通知給使用者，符合以下條件：

* 已訂閱頁面事件，例如，修改或復寫。 [通知收件匣](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications)區段說明如何訂閱這類事件。

* 已訂閱論壇活動。
* 必須在工作流程中執行步驟。 [參與者步驟](/help/sites-developing/workflows-step-ref.md#participant-step)區段說明如何在工作流程中觸發電子郵件通知。

先決條件：

* 使用者需要在其設定檔中定義有效的電子郵件地址。
* **天CQ郵件服務**&#x200B;需要正確設定。

當使用者收到通知時，他將會收到在其設定檔中定義之語言的電子郵件。 每種語言都有各自的範本可供自訂。 可以為新語言新增新的電子郵件範本。

>[!NOTE]
>
>使用AEM時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得詳細資訊和建議的作法。

## 設定郵件服務 {#configuring-the-mail-service}

若要讓AEM能夠傳送電子郵件，必須正確設定&#x200B;**Day CQ郵件服務**。 您可以在Web主控台中檢視組態。 使用AEM時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得詳細資訊和建議的作法。

下列限制適用：

* **SMTP伺服器連線埠**&#x200B;必須為25或更高。

* **SMTP伺服器主機名稱**&#x200B;不得為空白。
* **「寄件者」位址**&#x200B;不可為空白，且您必須變更預設值&quot;<noreply@day.com>&quot;。

為協助您針對&#x200B;**Day CQ Mail Service**&#x200B;的問題進行偵錯，您可以觀看此服務的記錄檔：

`com.day.cq.mailer.DefaultMailService`

在Web主控台中的設定如下所示：

![Day CQ Mail Service OSGi設定視窗](assets/chlimage_1-276.png)

## 設定電子郵件通知通道 {#configuring-the-email-notification-channel}

當您訂閱頁面或論壇事件通知時，寄件者電子郵件地址會依預設設為`no-reply@acme.com`。 您可以在Web主控台中設定&#x200B;**通知電子郵件通道**&#x200B;服務來變更此值。

若要設定寄件者電子郵件地址，請新增`sling:OsgiConfig`節點至存放庫。 使用以下程式，直接使用CRXDE Lite新增節點：

1. 在CRXDE Lite中，在應用程式資料夾下方新增名為`config`的資料夾。
1. 在設定資料夾中，新增名為的節點：

   `sling:OsgiConfig`型別的`com.day.cq.wcm.notification.email.impl.EmailChannel`

1. 將`String`屬性新增至名為`email.from`的節點。 針對值，指定您要使用的電子郵件地址。

1. 按一下&#x200B;**「儲存全部」**。

請使用下列程式來定義內容封裝來源資料夾中的節點：

1. 在您的`jcr_root/apps/*app_name*/config folder`中，建立名為`com.day.cq.wcm.notification.email.impl.EmailChannel.xml`的檔案

1. 新增下列XML來代表節點：

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 將`email.from`屬性( `name@server.com`)的值取代為您的電子郵件地址。

1. 儲存檔案。

## 設定工作流程電子郵件通知服務 {#configuring-the-workflow-email-notification-service}

當您收到工作流程電子郵件通知時，寄件者電子郵件地址和主機URL首碼都會設定為預設值。 您可以在Web主控台中設定&#x200B;**Day CQ工作流程電子郵件通知服務**，以變更這些值。 如果這樣做，您必須將變更保留在存放庫中。

在Web主控台中，預設設定如下所示：

![Day CQ工作流程電子郵件通知服務設定視窗](assets/chlimage_1-277.png)

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

1. 建立[頁面通知](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)的覆蓋

1. 開啟檔案：

   `en.txt`

1. 視需要修改檔案。
1. 儲存變更。

範本的格式必須如下：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

其中&lt;text_x>可以是靜態文字和動態字串變數的混合。 下列變數可用於頁面通知的電子郵件範本中：

* `${time}`，事件日期和時間。

* `${userFullName}`，觸發事件的使用者全名。

* `${userId}`，觸發事件的使用者識別碼。
* `${modifications}`，以格式說明頁面事件的型別和頁面路徑：

  &lt;頁面事件型別> => &lt;頁面路徑>

  例如：

  PageModified => /content/geometrixx/en/products

### 工作流程通知的電子郵件範本 {#email-templates-for-workflow-notification}

工作流程通知的電子郵件範本（英文）位於：

`/libs/settings/workflow/notification/email/default/en.txt`

其定義如下：

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

1. 建立[工作流程通知](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)的覆蓋

1. 開啟檔案：

   `en.txt`

1. 視需要修改檔案。
1. 儲存變更。

範本的格式必須如下：

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>其中`<text_x>`可以是靜態文字和動態字串變數的混合。 `<text_x>`專案的每一行都必須以反斜線( `\`)結尾，但最後一個執行個體除外，因為反斜線的缺位代表`<text_x>`字串變數的結尾。
>
>您可以在Properties.load() [&#128279;](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-)方法的javadocs中找到範本格式的詳細資訊。

方法`${payload.path.open}`會顯示工作專案裝載的路徑。 例如，若為Sites中的頁面，則`payload.path.open`會類似於`/bin/wcmcommand?cmd=open&path=…`。；這沒有伺服器名稱，因此範本會在它前面加上`${host.prefix}`。

下列變數可用於電子郵件範本中：

* `${event.EventType}`，事件的型別
* `${event.TimeStamp}`，事件的日期和時間
* `${event.User}`，觸發事件的使用者
* `${initiator.home}`，啟動器節點路徑

* `${initiator.name}`，啟動器名稱

* `${initiator.email}`，發起人的電子郵件地址
* `${item.id}`，工作專案的識別碼
* `${item.node.id}`，與此工作專案相關聯之工作流程模型中的節點識別碼
* `${item.node.title}`，工作專案的標題
* `${participant.email}`，參與者的電子郵件地址
* `${participant.name}`，參與者的名稱
* `${participant.familyName}`，參與者的姓氏
* `${participant.id}`，參與者識別碼
* `${participant.language}`，參與者語言
* `${instance.id}`，工作流程識別碼
* `${instance.state}`，工作流程狀態
* `${model.title}`，工作流程模型的標題
* `${model.id}`，工作流程模型的識別碼

* `${model.version}`，工作流程模型的版本
* `${payload.data}`，承載

* `${payload.type}`，裝載型別
* `${payload.path}`，承載的路徑
* `${host.prefix}`，主機首碼，例如： `http://localhost:4502`

### 新增新語言的電子郵件範本 {#adding-an-email-template-for-a-new-language}

新增新語言的範本：

1. 視需要建立[覆蓋](/help/sites-developing/overlays.md)。

   * [頁面通知](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
   * [工作流程通知](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

1. 新增檔案`<language-code>.txt`。
1. 將檔案調整成語言。
1. 儲存變更。

>[!NOTE]
>
>用作電子郵件範本檔案名稱的`<language-code>`必須是AEM可辨識的雙字母小寫語言代碼。 對於語言程式碼，AEM依賴ISO-639-1。

## 設定AEM Assets電子郵件通知 {#assetsconfig}

共用或取消共用AEM Assets中的集合時，使用者可以從AEM接收電子郵件通知。 若要設定電子郵件通知，請依照下列步驟執行。

1. 設定電子郵件服務，如[設定郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service)中所述。
1. 以管理員身分登入AEM。 按一下&#x200B;**工具** > **作業** > **網頁主控台**&#x200B;以開啟Web主控台設定。
1. 編輯&#x200B;**Day CQ DAM資源集合Servlet**。 選取&#x200B;**傳送電子郵件**。 按一下「**儲存**」。

## 設定OAuth {#setting-up-oauth}

AEM為其整合的郵件程式服務提供OAuth2支援，以允許組織遵守安全電子郵件要求。

您可以為多個電子郵件提供者設定OAuth，如下所述。

>[!NOTE]
>
>此程式是發佈執行個體的範例。 如果您想在作者執行個體上啟用電子郵件通知，您需要對作者執行相同的步驟。

### Gmail {#gmail}

1. 在`https://console.developers.google.com/projectcreate`建立您的專案
1. 選取您的專案，然後前往&#x200B;**API與服務** - **儀表板 — 認證**
1. 根據您的要求設定OAuth同意畫面
1. 在隨後的「更新畫面」中，新增這兩個範圍：
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. 新增領域後，請回到左側功能表中的&#x200B;**認證**，然後前往&#x200B;**建立認證** - **OAuth使用者端ID** - **案頭應用程式**
1. 隨即開啟新視窗，其中包含「使用者端ID」和「使用者端密碼」。
1. 儲存這些認證。

**AEM端組態**

>[!NOTE]
>
>Adobe Managed Service客戶可與他們的客戶服務工程師合作，對生產環境進行這些變更。

首先，設定郵件服務：

1. 前往`http://serveraddress:serverport/system/console/configMgr`開啟AEM Web Console
1. 尋找，然後按一下&#x200B;**Day CQ郵件服務**
1. 新增下列設定：
   * SMTP伺服器主機名稱： `smtp.gmail.com`
   * SMTP伺服器連線埠： `25`或`587`，視需求而定
   * 勾選&#x200B;**SMPT使用StarTLS**&#x200B;以及&#x200B;**SMTP需要StarTLS**&#x200B;的勾選方塊
   * 檢查&#x200B;**OAuth流程**&#x200B;並按一下&#x200B;**儲存**。

接下來，請依照下列程式設定您的SMTP OAuth提供者：

>[!WARNING]
>
>完成此設定後，如果您曾變更OSGi設定&#x200B;**CQ Mailer SMTP OAuth2 Provide**&#x200B;中的&#x200B;*任何*&#x200B;值，則您必須依照這些步驟再次重新授權。
>
>如果未執行這些動作，則儲存在`/conf/global/settings/mailer/oauth`的存取權杖將會無效，且OAuth2與SMTP伺服器的連線將會失敗。

1. 前往`http://serveraddress:serverport/system/console/configMgr`開啟AEM Web Console
1. 尋找，然後按一下&#x200B;**CQ Mailer SMTP OAuth2 Provider**

1. 請依照以下說明填寫必要資訊：
   * 授權URL： `https://accounts.google.com/o/oauth2/auth`
   * 權杖URL： `https://accounts.google.com/o/oauth2/token`
   * 範圍： `https://www.googleapis.com/auth/gmail.send`和`https://mail.google.com/`。 您可以按每個已設定範圍右側的&#x200B;**+**&#x200B;按鈕，以新增多個範圍。
   * 使用者端ID和使用者端密碼：使用您擷取的值（如上段所述）設定這些欄位。
   * 重新整理權杖URL： `https://accounts.google.com/o/oauth2/token`
   * 重新整理Token到期日：永不
1. 按一下「**儲存**」。

<!-- clarify refresh token expiry, currently not present in the UI -->

設定完成後，設定應該如下所示：

![CQ Mailer SMTP Oauth2提供者設定視窗](assets/oauth-smtpprov2.png)

現在啟動OAuth元件。 您可以透過以下方式進行：

1. 造訪此URL以移至[元件主控台]： `http://serveraddress:serverport/system/console/components`
1. 尋找下列元件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按元件左側的「播放」圖示

   ![顯示OAuthCodeGenerateServlet和OAuthCodeAccessTokenGenerator的元件清單](assets/oauth-components-play.png)

最後，透過以下方式確認設定：

1. 前往發佈執行個體的位址，並以管理員身分登入。
1. 在瀏覽器中開啟新索引標籤，並移至`http://serveraddress:serverport/services/mailer/oauth2/authorize`。 這會將您重新導向至SMTP提供者的頁面，在此案例中是Gmail。
1. 登入並同意提供必要許可權
1. 在同意後，權杖將會儲存在存放庫中。 您可以直接存取發佈執行個體上的此URL，以在`accessToken`下存取它： `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. 對每個發佈執行個體重複上述步驟

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. 前往 [https://portal.azure.com/](https://portal.azure.com/) 並登入。
1. 在搜尋列中搜尋 **Azure Active Directory**，然後按一下結果。或者，您可以直接瀏覽到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下「**應用程式註冊** - **新註冊**」

   ![設定Microsoft Outlook時的新註冊按鈕](assets/oauth-outlook1.png)

1. 根據您的要求填寫資訊，然後按一下&#x200B;**註冊**
1. 前往新建的應用程式，然後選取「**API 權限**」
1. 移至「**新增權限** - **Graph 權限** - **委派的權限**」
1. 為您的應用程式選取以下權限，然後按一下「**新增權限**」：
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 移至&#x200B;**驗證** - **新增平台** - **Web**，並在&#x200B;**重新導向URL**&#x200B;區段中，新增下列URL以重新導向OAuth程式碼，然後按&#x200B;**設定**：
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 對每個發佈執行個體重複上述步驟
1. 根據您的需求進行設定
1. 接下來，移至&#x200B;**憑證和密碼**，按一下&#x200B;**新增使用者端密碼**，然後依照熒幕上的步驟建立密碼。 請務必記下此密碼以備稍後使用
1. 在左側窗格中按「**概觀**」並複製「**應用程式 (用戶端) ID**」和「**目錄 (租用戶) ID**」的值以供稍後使用

回顧一下，您必須擁有下列資訊才能在AEM端為郵件程式服務設定OAuth2：

* 驗證 URL，將使用租用戶 ID 建構。 它將具有此形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 權杖 URL，將使用租用戶 ID 建構。 它將具有此形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 重新整理 URL，將使用租用戶 ID 建構。 它將具有此形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 用戶端 ID
* 用戶端密碼

**AEM端組態**

接下來，將您的OAuth2設定與AEM整合：

>[!WARNING]
>
>完成此設定後，如果您曾變更OSGi設定&#x200B;**CQ Mailer SMTP OAuth2 Provide**&#x200B;中的&#x200B;*任何*&#x200B;值，則您必須依照這些步驟再次重新授權。
>
>如果未執行這些動作，則儲存在`/conf/global/settings/mailer/oauth`的存取權杖將會無效，且OAuth2與SMTP伺服器的連線將會失敗。

1. 瀏覽至`http://serveraddress:serverport/system/console/configMgr`，移至您本機執行個體的Web主控台
1. 尋找並按一下&#x200B;**Day CQ郵件服務**
1. 新增下列設定：
   * SMTP伺服器主機名稱： `smtp.office365.com`
   * SMTP使用者：您的使用者名稱（電子郵件格式）
   * 「寄件者」地址：郵件程式所傳送訊息的「寄件者：」欄位中使用的電子郵件地址
   * SMTP伺服器連線埠： `25`或`587` （視需求而定）
   * 勾選&#x200B;**SMPT使用StarTLS**&#x200B;以及&#x200B;**SMTP需要StarTLS**&#x200B;的勾選方塊
   * 檢查&#x200B;**OAuth流程**&#x200B;並按一下&#x200B;**儲存**。
1. 尋找，然後按一下&#x200B;**CQ Mailer SMTP OAuth2 Provider**
1. 請依照以下說明填寫必要資訊：
   * 填入授權URL、權杖URL和重新整理權杖URL，方法為依照此程式結尾[的說明](#microsoft-outlook)建構它們
   * 使用者端ID和使用者端密碼：使用上述擷取的值來設定這些欄位。
   * 將以下範圍新增到設定中：
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode重新導向Url： `http://localhost:4503/services/mailer/oauth2/token`
   * 重新整理記號URL：這應該與上述記號URL的值相同
1. 按一下「**儲存**」。

設定完成後，設定應該如下所示：

![完成的CQ Mailer SMTP OAuth2組態](assets/oauth-outlook-smptconfig.png)

現在啟動OAuth元件。 您可以透過以下方式進行：

1. 造訪此URL以移至[元件主控台]： `http://serveraddress:serverport/system/console/components`
1. 尋找下列元件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按元件左側的「播放」圖示

![包含OAuthCodeGenerateServlet和OAuthCodeAccessTokenGenerator的元件清單片段](assets/oauth-components-play.png)

最後，透過以下方式確認設定：

1. 前往發佈執行個體的位址，並以管理員身分登入。
1. 在瀏覽器中開啟新索引標籤，並移至`http://serveraddress:serverport/services/mailer/oauth2/authorize`。 這會將您重新導向至SMTP提供者的頁面，在此案例中是Outlook。
1. 登入並同意提供必要許可權
1. 在同意後，權杖將會儲存在存放庫中。 您可以直接存取發佈執行個體上的此URL，以在`accessToken`下存取它： `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
