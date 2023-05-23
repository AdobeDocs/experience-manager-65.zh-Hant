---
title: 配置電子郵件通知
seo-title: Configuring Email Notification
description: 瞭解如何在中配置電子郵件通AEM知。
seo-description: Learn how to configure Email Notification in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
source-git-commit: 144fbe2d0efe20d848e9556f8d652a403d1835b2
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 12%

---

# 配置電子郵件通知{#configuring-email-notification}

AEM將電子郵件通知發送給以下用戶：

* 已訂閱頁事件，例如修改或複製。 的 [通知收件箱](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) 節介紹如何訂閱此類事件。

* 已訂閱論壇活動。
* 必須在工作流中執行步驟。 的 [參與者步驟](/help/sites-developing/workflows-step-ref.md#participant-step) 部分介紹如何在工作流中觸發電子郵件通知。

先決條件：

* 用戶需要在其個人資料中定義有效的電子郵件地址。
* 的 **第CQ天郵件服務** 需要正確配置。

當用戶被通知時，他收到一封電子郵件，其語言在其個人資料中定義。 每種語言都有自己的模板，可以自定義。 可以為新語言添加新的電子郵件模板。

>[!NOTE]
>
>使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

## 配置郵件服務 {#configuring-the-mail-service}

為AEM了能發郵件， **第CQ天郵件服務** 需要正確配置。 您可以在Web控制台中查看配置。 使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

應用以下約束：

* 的 **SMTP伺服器埠** 必須是25歲或更高。

* 的 **SMTP伺服器主機名** 不得為空。
* 的 **&quot;發件人&quot;地址** 不得為空。

幫助您調試問題 **第CQ天郵件服務**，您可以監視服務的日誌：

`com.day.cq.mailer.DefaultMailService`

Web控制台中的配置如下所示：

![chlimage_1-276](assets/chlimage_1-276.png)

## 配置電子郵件通知通道 {#configuring-the-email-notification-channel}

訂閱頁面或論壇事件通知時，發件人電子郵件地址將設定為 `no-reply@acme.com` 預設值。 通過配置 **通知電子郵件通道** 的下界。

要配置發件人電子郵件地址，請添加 `sling:OsgiConfig` 節點到儲存庫。 使用以下過程直接使用CRXDE Lite添加節點：

1. 在CRXDE Lite中，添加名為 `config` 應用程式資料夾下。
1. 在配置資料夾中，添加一個名為：

   `com.day.cq.wcm.notification.email.impl.EmailChannel` 類型 `sling:OsgiConfig`

1. 添加 `String` 屬性 `email.from`。 對於值，指定要使用的電子郵件地址。

1. 按一下 **全部保存**。

請按下列步驟定義內容包源資料夾中的節點：

1. 在 `jcr_root/apps/*app_name*/config folder`，建立名為 `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. 添加以下XML以表示節點：

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 替換 `email.from` 屬性(A) `name@server.com`)。

1. 儲存檔案。

## 配置工作流電子郵件通知服務 {#configuring-the-workflow-email-notification-service}

當您收到工作流電子郵件通知時，發件人電子郵件地址和主機URL前置詞均設定為預設值。 通過配置 **第CQ天工作流電子郵件通知服務** 的下界。 如果您這樣做，建議將更改保留在儲存庫中。

預設配置在Web控制台中如下所示：

![chlimage_1-277](assets/chlimage_1-277.png)

### 頁面通知的電子郵件模板 {#email-templates-for-page-notification}

頁面通知的電子郵件模板位於以下位置：

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

預設英語模板( `en.txt`)的定義如下：

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

#### 自定義頁面通知的電子郵件模板 {#customizing-email-templates-for-page-notification}

要自定義頁面通知的英文電子郵件模板，請執行以下操作：

1. 在CRXDE中，開啟檔案：

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. 根據需要修改檔案。
1. 儲存變更。

模板需要具有以下格式：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

位置 &lt;text_x> 可以是靜態文本和動態字串變數的混合。 可以在電子郵件模板中為頁面通知使用以下變數：

* `${time}`，事件日期和時間。

* `${userFullName}`，觸發事件的用戶的全名。

* `${userId}`，觸發事件的用戶的ID。
* `${modifications}`，以下列格式描述頁面事件的類型和頁面路徑：

   &lt;page event=&quot;&quot; type=&quot;&quot;> => &lt;page path=&quot;&quot;>

   例如：

   PageModified => /content/geometrixx/en/products

### 工作流通知的電子郵件模板 {#email-templates-for-workflow-notification}

工作流通知（英語）的電子郵件模板位於：

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

#### 自定義工作流通知的電子郵件模板 {#customizing-email-templates-for-workflow-notification}

要自定義工作流事件通知的英文電子郵件模板，請執行以下操作：

1. 在CRXDE中，開啟檔案：

   `/libs/settings/workflow/notification/email/default/en.txt`

1. 根據需要修改檔案。
1. 儲存變更。

模板需要具有以下格式：

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>位置 `<text_x>` 可以是靜態文本和動態字串變數的混合。 每行 `<text_x>` 項目需要用反斜槓結束( `\`)，但上一個實例除外，因為沒有反斜線表示 `<text_x>` 字串變數。
>
>有關模板格式的詳細資訊，請參閱 [javadocs of Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) 的雙曲餘切值。

方法 `${payload.path.open}` 顯示工作項的有效負載的路徑。 例如，在「站點」中， `payload.path.open` 會類似 `/bin/wcmcommand?cmd=open&path=…`。;這是沒有伺服器名稱的，因此模板會預先使用 `${host.prefix}`。

在電子郵件模板中可以使用以下變數：

* `${event.EventType}`，事件類型
* `${event.TimeStamp}`、事件的日期和時間
* `${event.User}`，觸發事件的用戶
* `${initiator.home}`，啟動器節點路徑

* `${initiator.name}`，啟動器名稱

* `${initiator.email}`，啟動器的電子郵件地址
* `${item.id}`，工作項的ID
* `${item.node.id}`，與此工作項關聯的工作流模型中節點的ID
* `${item.node.title}`，工作項的標題
* `${participant.email}`，參與者的電子郵件地址
* `${participant.name}`，參與者的名稱
* `${participant.familyName}`，參與者的家族名稱
* `${participant.id}`，參與者的id
* `${participant.language}`，參與者語言
* `${instance.id}`，工作流ID
* `${instance.state}`，工作流狀態
* `${model.title}`，工作流模型的標題
* `${model.id}`，工作流模型的ID

* `${model.version}`，工作流模型的版本
* `${payload.data}`，負載

* `${payload.type}`，負載類型
* `${payload.path}`，負載路徑
* `${host.prefix}`，主機前置詞，例如：http://localhost:4502

### 為新語言添加電子郵件模板 {#adding-an-email-template-for-a-new-language}

為新語言添加模板：

1. 在CRXDE中，添加檔案 `<language-code>.txt` 以下：

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` :頁通知
   * `/libs/settings/workflow/notification/email/default` :用於工作流通知

1. 使檔案適應語言。
1. 儲存變更。

>[!NOTE]
>
>的 `<language-code>` 用作電子郵件模板的檔案名需要是由識別的二字母小寫語言代AEM碼。 語言代AEM碼依賴ISO-639-1。

## 配置AEM Assets電子郵件通知 {#assetsconfig}

當AEM Assets的集合被共用或取消共用時，用戶可以從接收電子郵件通AEM知。 要配置電子郵件通知，請執行以下步驟。

1. 按上述說明配置電子郵件服務 [配置郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service)。
1. 以管理AEM員身份登錄。 按一下 **工具** >  **操作** >  **Web控制台** 開啟Web控制台配置。
1. 編輯 **第CQ DAM資源收集Servlet**。 選擇 **發送電子郵件**。 按一下「**儲存**」。

## 設定OAuth {#setting-up-oauth}

為AEM其整合郵件服務提供OAuth2支援，以便組織能夠遵守安全的電子郵件要求。

您可以為多個電子郵件提供程式配置OAuth，如下所述。

>[!NOTE]
>
>此過程是發佈實例的示例。 如果希望在「作者」實例上啟用電子郵件通知，則需要在「作者」上執行相同的步驟。

### Gmail {#gmail}

1. 在以下位置建立項目 `https://console.developers.google.com/projectcreate`
1. 選擇項目，然後轉到 **API和服務** - **儀表板 — 憑據**
1. 根據您的要求配置OAuth同意螢幕
1. 在下面的更新螢幕中，添加以下兩個作用域：
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. 添加作用域後，返回 **憑據** 在左側菜單中，然後轉到 **建立憑據** - **OAuth客戶端ID** - **案頭應用**
1. 將開啟一個包含客戶端ID和客戶端密碼的新窗口。
1. 保存這些憑據。

**側AEM面配置**

>[!NOTE]
>
>Adobe管理服務客戶可以與其客戶服務工程師合作，對生產環境進行這些更改。

首先，配置郵件服務：

1. 通過轉AEM到以下位置開啟Web控制台 `http://serveraddress:serverport/system/console/configMgr`
1. 查找，然後按一下 **第CQ天郵件服務**
1. 添加以下設定：
   * SMTP 伺服器主機名稱: `smtp.gmail.com`
   * SMTP伺服器埠： `25` 或 `587`，取決於要求
   * 選中「 **SMPT使用StarTLS** 和 **SMTP需要StarTLS**
   * 檢查 **OAuth流** 按一下 **保存**。

接下來，按照以下步驟配置SMTP OAuth提供程式：

1. 通過轉AEM到以下位置開啟Web控制台 `http://serveraddress:serverport/system/console/configMgr`
1. 查找，然後按一下 **CQ郵件程式SMTP OAuth2提供程式**
1. 按如下方式填寫所需資訊：
   * 授權URL: `https://accounts.google.com/o/oauth2/auth`
   * 標籤URL: `https://accounts.google.com/o/oauth2/token`
   * 作用域： `https://www.googleapis.com/auth/gmail.send` 和 `https://mail.google.com/`。 通過按 **+** 按鈕。
   * 客戶端ID和客戶端密碼：使用上段所述的檢索值配置這些欄位。
   * 重新整理記號 URL: `https://accounts.google.com/o/oauth2/token`
   * 刷新令牌到期：從不
1. 按一下「**儲存**」。

<!-- clarify refresh token expiry, currrently not present in the UI -->

配置後，設定應如下所示：

![oauth smtp提供程式](assets/oauth-smtpprov2.png)

現在，激活OAuth元件。 您可以透過以下方式進行：

1. 通過訪問以下URL轉到元件控制台： `http://serveraddress:serverport/system/console/components`
1. 查找以下元件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按元件左側的「Play（播放）」表徵圖

   ![元件](assets/oauth-components-play.png)

最後，通過以下方式確認配置：

1. 轉到「發佈」實例的地址，並以管理員身份登錄。
1. 在瀏覽器中開啟一個新頁籤，然後轉到 `http://serveraddress:serverport/services/mailer/oauth2/authorize`。 這將重定向到SMTP提供程式的頁面（在此情況下為Gmail）。
1. 登錄並同意授予所需權限
1. 同意後，令牌將儲存在儲存庫中。 你可以在 `accessToken` 通過直接訪問發佈實例上的此URL: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. 對每個發佈實例重複上述步驟

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. 前往 [https://portal.azure.com/](https://portal.azure.com/) 並登入。
1. 在搜尋列中搜尋 **Azure Active Directory**，然後按一下結果。或者，您可以直接瀏覽到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 按一下「**應用程式註冊** - **新註冊**」

   ![](assets/oauth-outlook1.png)

1. 根據您的要求填寫資訊，然後按一下「**註冊**」
1. 前往新建的應用程式，然後選取「**API 權限**」
1. 移至「**新增權限** - **Graph 權限** - **委派的權限**」
1. 為您的應用程式選取以下權限，然後按一下「**新增權限**」：
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 轉到 **驗證** - **添加平台** - **Web**&#x200B;的 **重定向URL** 部分，添加以下URL以重定向OAuth代碼，然後按 **配置**:
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 對每個發佈實例重複上述步驟
1. 根據您的要求配置設定
1. 接下來，移至「**憑證和密碼**」，按一下「**新增用戶端密碼**」，並按照畫面上的步驟建立密碼。請務必記下此密碼以備稍後使用
1. 在左側窗格中按「**概觀**」並複製「**應用程式 (用戶端) ID**」和「**目錄 (租用戶) ID**」的值以供稍後使用

若要重新訪問，您需要以下資訊來為一側的Mailer服務配置OAuth2AEM :

* 驗證 URL，將使用租用戶 ID 建構。 它將具有此形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 權杖 URL，將使用租用戶 ID 建構。 它將具有此形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 重新整理 URL，將使用租用戶 ID 建構。 它將具有此形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 用戶端 ID
* 用戶端密碼

**側AEM面配置**

接下來，將OAuth2設定與AEM:

1. 通過瀏覽到 `http://serveraddress:serverport/system/console/configMgr`
1. 查找並按一下 **第CQ天郵件服務**
1. 添加以下設定：
   * SMTP 伺服器主機名稱: `smtp.office365.com`
   * SMTP用戶：電子郵件格式的用戶名
   * 「發件人」地址：郵件發送者發送的郵件的「發件人：」欄位中要使用的電子郵件地址
   * SMTP伺服器埠： `25` 或 `587` 取決於要求
   * 選中「 **SMPT使用StarTLS** 和 **SMTP需要StarTLS**
   * 檢查 **OAuth流** 按一下 **保存**。
1. 查找，然後按一下 **CQ郵件程式SMTP OAuth2提供程式**
1. 按如下方式填寫所需資訊：
   * 通過構建授權URL、令牌URL和刷新令牌URL（如所述）來填充 [本程式的結束](#microsoft-outlook)
   * 客戶端ID和客戶端密碼：使用上述檢索到的值配置這些欄位。
   * 將以下範圍新增到設定中：
      * openid
      * 離線訪問
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode重定向URL: `http://localhost:4503/services/mailer/oauth2/token`
   * 刷新標籤URL:此值應與上面的標籤URL的值相同
1. 按一下「**儲存**」。

配置後，設定應如下所示：

![](assets/oauth-outlook-smptconfig.png)

現在，激活OAuth元件。 您可以透過以下方式進行：

1. 通過訪問以下URL轉到元件控制台： `http://serveraddress:serverport/system/console/components`
1. 查找以下元件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按元件左側的「Play（播放）」表徵圖

![components2](assets/oauth-components-play.png)

最後，通過以下方式確認配置：

1. 轉到「發佈」實例的地址，並以管理員身份登錄。
1. 在瀏覽器中開啟一個新頁籤，然後轉到 `http://serveraddress:serverport/services/mailer/oauth2/authorize`。 這將重定向到SMTP提供程式的頁面，在此情況下為Outlook。
1. 登錄並同意授予所需權限
1. 同意後，令牌將儲存在儲存庫中。 你可以在 `accessToken` 通過直接訪問發佈實例上的此URL: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
