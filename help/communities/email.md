---
title: 設定電子郵件
seo-title: Configuring Email
description: 社群的電子郵件設定
seo-description: Email configuration for Communities
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 3%

---

# 設定電子郵件 {#configuring-email}

AEM Communities使用電子郵件：

* [Communities通知](notifications.md)
* [Communities 訂閱](subscriptions.md)

依預設，電子郵件功能無法運作，因為它需要指定SMTP伺服器和SMTP使用者。

>[!CAUTION]
>
>通知和訂閱的電子郵件必須僅在 [主要發佈者](deploy-communities.md#primary-publisher).

## 預設郵件服務配置 {#default-mail-service-configuration}

通知和訂閱均需要預設郵件服務。

* 以管理員權限登入主發佈者並存取 [Web主控台](../../help/sites-deploying/configuring-osgi.md):

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找出 `Day CQ Mail Service`.
* 選取編輯圖示。

這是根據 [設定電子郵件通知](../../help/sites-administering/notification.md)但是，在這個領域 `"From" address` is *not* 必要，且應保留空白。

例如（填入僅供說明之用的值）:

![email-config](assets/email-config.png)

* **[!UICONTROL SMTP伺服器主機名]**

   *（必要）* 要使用的SMTP伺服器。

* **[!UICONTROL SMTP伺服器埠]**

   *（必要）* SMTP伺服器埠必須是25或更高。

* **[!UICONTROL SMTP用戶]**

   *（必要）* SMTP用戶。

* **[!UICONTROL SMTP密碼]**

   *（必要）* SMTP用戶的密碼。

* **[!UICONTROL 「寄件者」地址]**

   保留空白
* **[!UICONTROL SMTP使用SSL]**

   若勾選此選項，將會傳送安全電子郵件。 請確保埠已設定為465或SMTP伺服器所需的埠。
* **[!UICONTROL 偵錯電子郵件]**

   如果選中此選項，則啟用SMTP伺服器交互的記錄。

## AEM Communities電子郵件設定 {#aem-communities-email-configuration}

一旦 [預設郵件服務](#default-mail-service-configuration) 已設定，則 `AEM Communities Email Reply Configuration` 發行包含的OSGi設定可正常運作。

允許透過電子郵件回覆時，只需進一步設定訂閱的例項。

1. [電子郵件](#configuration-for-notifications) 例項：

   若為不支援回覆電子郵件的通知，則不應加以變更。

1. [訂閱 — 電子郵件](#configuration-for-subscriptions) 例項：

   需要設定才能完全啟用從回覆電子郵件建立貼文的功能。

要訪問Communities電子郵件配置實例：

* 以管理員權限登入主發佈者並存取 [Web主控台](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找出 `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### 通知的設定 {#configuration-for-notifications}

的例項 `AEM Communities Email Reply Configuration` 使用「名稱」電子郵件設定的OSGi為立即功能。 此功能不包含電子郵件回覆。

不應更改此配置。

* 找出 `AEM Communities Email Reply Configuration`.
* 選取編輯圖示。
* 驗證 **名稱** is `email`.

* 驗證 **從回覆電子郵件建立貼文** is `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### 訂閱的設定 {#configuration-for-subscriptions}

對於「社群」訂閱，可以透過回覆電子郵件來啟用或停用成員張貼內容的能力。

* 找出 `AEM Communities Email Reply Configuration`.
* 選取編輯圖示。
* 驗證 **名稱** is `subscriptions-email`.

   ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL 名稱]**

   *（必要）* `subscriptions-email`. 請勿編輯。

* **[!UICONTROL 從回覆電子郵件建立貼文]**

   如果選中，訂閱電子郵件的收件人可以通過發送回復來發佈內容。 已勾選預設值。
* **[!UICONTROL 將追蹤ID新增至標題]**

   預設為 `Reply-To`.

* **[!UICONTROL 主旨的長度上限]**

   如果將追蹤器ID新增至主旨行，則此為除了追蹤ID以外的主旨最大長度，之後會加以裁剪。 請注意，這應盡可能小，以免追蹤的ID資訊遺失。 預設為200。

* **[!UICONTROL 「回復」電子郵件地址]**

   用作「回覆」電子郵件地址的地址。 預設為 `no-reply@example.com`.

* **[!UICONTROL 回覆分隔字元]**

   如果追蹤器ID新增至回覆標題，將會使用此分隔字元。 預設為 `+` （加號）。

* **[!UICONTROL 主旨中的追蹤器ID前置詞]**

   如果追蹤器ID新增至主旨行，將會使用此首碼。 預設為 `post#`.

* **[!UICONTROL 訊息內文中的追蹤器ID首碼]**

   如果將追蹤器ID新增至訊息內文，將會使用此首碼。 預設為 `Please do not remove this:`.

* **[!UICONTROL 以電子郵件方式HTML]**:若勾選此選項，電子郵件的「內容類型」將設為 `"text/html;charset=utf-8"`. 已勾選預設值。

* **[!UICONTROL 預設用戶名]**

   此名稱將不用於姓名用戶。 預設為 `no-reply@example.com`.

* **[!UICONTROL 範本根路徑]**

   使用儲存於此根路徑之範本所建立的電子郵件. 預設為 `/etc/community/templates/subscriptions-email`.

## 設定輪詢匯入工具 {#configure-polling-importer}

若要將電子郵件帶入存放庫，您必須設定輪詢匯入工具，並手動在存放庫中設定其屬性。

### 新增輪詢匯入工具 {#add-new-polling-importer}

* 以管理員權限登入主要發佈者，並瀏覽至輪詢匯入工具主控台：

   例如， [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* 選擇 **[!UICONTROL 新增]**

   ![polling-importer](assets/polling-importer.png)

* **[!UICONTROL 類型]**

   *（必要）* 下拉以選取 `POP3 (over SSL)`.

* **[!UICONTROL URL]**

   *（必要）* 出站郵件伺服器。 例如, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL 匯入至路徑]**&amp;ast;

   *（必要）* 設為 `/content/usergenerated/mailFolder/postEmails`
瀏覽至 `postEmails`資料夾和選取 **確定**.

* **[!UICONTROL 以秒為單位的更新間隔]**

   *（可選）* 為預設郵件服務配置的郵件伺服器可能有關於更新時間間隔值的要求。 例如，Gmail可能需要間隔 `300`.

* **[!UICONTROL 登入]**

   *(選用)*

* **[!UICONTROL 密碼]**

   *(選用)*

* 選擇 **[!UICONTROL 確定]**.

### 調整新輪詢導入程式的協定 {#adjust-protocol-for-new-polling-importer}

儲存新輪詢設定後，必須進一步修改訂閱電子郵件匯入工具的屬性，才能將通訊協定從 `POP3` to `emailreply`.

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 以管理員權限登錄到主發佈伺服器並瀏覽到 [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* 選取新建立的設定並修改下列屬性：

   * **feedType**:取代 `pop3s` with **`emailreply`**
   * **來源**:替換源的協定 `pop3s://` with **`emailreply://`**

![輪詢協定](assets/polling-protocol.png)

紅色三角形表示修改的屬性。 請務必儲存變更：

* 選擇 **[!UICONTROL 全部儲存]**.
