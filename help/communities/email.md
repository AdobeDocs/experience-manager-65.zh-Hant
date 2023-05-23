---
title: 配置電子郵件
seo-title: Configuring Email
description: 社區的電子郵件配置
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

# 配置電子郵件 {#configuring-email}

AEM Communities使用電子郵件：

* [社區通知](notifications.md)
* [Communities 訂閱](subscriptions.md)

預設情況下，電子郵件功能不起作用，因為它需要SMTP伺服器和SMTP用戶的規範。

>[!CAUTION]
>
>只有在 [主發佈者](deploy-communities.md#primary-publisher)。

## 預設郵件服務配置 {#default-mail-service-configuration}

通知和訂閱都需要預設郵件服務。

* 使用管理員權限登錄到主發佈伺服器並訪問 [Web控制台](../../help/sites-deploying/configuring-osgi.md):

   * 比如說， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 查找 `Day CQ Mail Service`。
* 選擇編輯表徵圖。

這基於 [配置電子郵件通知](../../help/sites-administering/notification.md)但在這個領域里 `"From" address` 是 *不* 必需，應留空。

例如（僅為說明目的用值填充）:

![電子郵件配置](assets/email-config.png)

* **[!UICONTROL SMTP伺服器主機名]**

   *（必需）* 要使用的SMTP伺服器。

* **[!UICONTROL SMTP伺服器埠]**

   *（必需）* SMTP伺服器埠必須是25或更高。

* **[!UICONTROL SMTP用戶]**

   *（必需）* SMTP用戶。

* **[!UICONTROL SMTP密碼]**

   *（必需）* SMTP用戶的密碼。

* **[!UICONTROL &quot;發件人&quot;地址]**

   留空
* **[!UICONTROL SMTP使用SSL]**

   如果選中，將發送安全電子郵件。 確保埠設定為465或SMTP伺服器所需的埠。
* **[!UICONTROL 調試電子郵件]**

   如果選中，則啟用SMTP伺服器交互的日誌記錄。

## AEM Communities電子郵件配置 {#aem-communities-email-configuration}

一旦 [預設郵件服務](#default-mail-service-configuration) 已配置， `AEM Communities Email Reply Configuration` OSGi配置（包括在發行版中）可正常工作。

在允許通過電子郵件回復時，只需進一步配置訂閱實例。

1. [電子郵件](#configuration-for-notifications) 實例：

   對於不支援回復電子郵件且不應更改的通知。

1. [訂閱 — 電子郵件](#configuration-for-subscriptions) 實例：

   需要配置才能完全啟用通過回復電子郵件建立帖子。

要訪問社區電子郵件配置實例：

* 使用管理員權限登錄到主發佈伺服器並訪問 [Web控制台](../../help/sites-deploying/configuring-osgi.md)

   * 比如說， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 定位 `AEM Communities Email Reply Configuration`。

![電子郵件回復配置](assets/email-reply-config.png)

### 通知配置 {#configuration-for-notifications}

實例 `AEM Communities Email Reply Configuration` OSGi配置和「名稱」電子郵件是立即啟用功能。 此功能不包括電子郵件回復。

不應更改此配置。

* 查找 `AEM Communities Email Reply Configuration`。
* 選擇編輯表徵圖。
* 驗證 **名稱** 是 `email`。

* 驗證 **通過回復電子郵件建立帖子** 是 `unchecked`。

![配置 — 電子郵件 — 回復](assets/configure-email-reply.png)

### 訂閱配置 {#configuration-for-subscriptions}

對於社區訂閱，可以啟用或禁用成員通過回復電子郵件來發佈內容的功能。

* 查找 `AEM Communities Email Reply Configuration`。
* 選擇編輯表徵圖。
* 驗證 **名稱** 是 `subscriptions-email`。

   ![配置電子郵件訂閱](assets/configure-email-subscriptions.png)

* **[!UICONTROL 名稱]**

   *（必需）* `subscriptions-email`。 不編輯。

* **[!UICONTROL 通過回復電子郵件建立帖子]**

   如果選中，訂閱電子郵件的收件人可以通過發送回復來發佈內容。 選中預設值。
* **[!UICONTROL 將跟蹤的ID添加到標題]**

   預設值為 `Reply-To`。

* **[!UICONTROL 主旨的長度上限]**

   如果跟蹤器ID添加到主題行，則這是主題的最大長度（不包括跟蹤的ID），在此長度之後將裁切它。 請注意，應盡可能小，以避免丟失跟蹤的ID資訊。 預設值為200。

* **[!UICONTROL 「回復」電子郵件地址]**

   用作「回復」電子郵件地址的地址。 預設值為 `no-reply@example.com`。

* **[!UICONTROL 回復分隔符]**

   如果將跟蹤器ID添加到回復頭，則將使用此分隔符。 預設值為 `+` （加號）。

* **[!UICONTROL 主題中的跟蹤器ID前置詞]**

   如果將跟蹤器ID添加到主題行，則將使用此前置詞。 預設值為 `post#`。

* **[!UICONTROL 消息正文中的跟蹤器ID前置詞]**

   如果將跟蹤器ID添加到消息正文，則將使用此前置詞。 預設值為 `Please do not remove this:`。

* **[!UICONTROL 電子郵件作為HTML]**:如果選中，則電子郵件的「內容類型」將設定為 `"text/html;charset=utf-8"`。 選中預設值。

* **[!UICONTROL 預設用戶名]**

   此名稱將不用於任何名稱用戶。 預設值為 `no-reply@example.com`。

* **[!UICONTROL 模板根路徑]**

   使用儲存於此根路徑之範本所建立的電子郵件. 預設值為 `/etc/community/templates/subscriptions-email`。

## 配置輪詢導入程式 {#configure-polling-importer}

為了將電子郵件帶入儲存庫，必須配置輪詢導入程式並手動在儲存庫中配置其屬性。

### 添加新輪詢導入程式 {#add-new-polling-importer}

* 使用管理員權限登錄到主發佈伺服器並瀏覽到輪詢導入程式控制台：

   比如說， [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* 選擇 **[!UICONTROL 添加]**

   ![輪詢導入器](assets/polling-importer.png)

* **[!UICONTROL 類型]**

   *（必需）* 下拉以選擇 `POP3 (over SSL)`。

* **[!UICONTROL URL]**

   *（必需）* 出站郵件伺服器。 比如說， `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`。

* **[!UICONTROL 導入到路徑]**&amp;ast;

   *（必需）* 設定為 `/content/usergenerated/mailFolder/postEmails`
瀏覽到 `postEmails`資料夾和 **確定**。

* **[!UICONTROL 以秒為單位的更新間隔]**

   *（可選）* 為預設郵件服務配置的郵件伺服器可能對更新間隔值有要求。 例如，Gmail可能需要間隔 `300`。

* **[!UICONTROL 登入]**

   *(選用)*

* **[!UICONTROL 密碼]**

   *(選用)*

* 選擇 **[!UICONTROL 確定]**。

### 調整新輪詢導入程式的協定 {#adjust-protocol-for-new-polling-importer}

保存新輪詢配置後，必須進一步修改訂閱電子郵件導入程式的屬性，以便將協定從 `POP3` 至 `emailreply`。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 使用管理員權限登錄到主發佈伺服器並瀏覽到 [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)。
* 選擇新建立的配置並修改以下屬性：

   * **feedType**:替換 `pop3s` 與 **`emailreply`**
   * **源**:替換源的協定 `pop3s://` 與 **`emailreply://`**

![輪詢協定](assets/polling-protocol.png)

紅色三角形表示已修改的屬性。 確保保存更改：

* 選擇 **[!UICONTROL 全部保存]**。
