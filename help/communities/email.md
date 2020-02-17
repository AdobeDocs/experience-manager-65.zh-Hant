---
title: 設定電子郵件
seo-title: 設定電子郵件
description: 社群的電子郵件設定
seo-description: 社群的電子郵件設定
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 設定電子郵件 {#configuring-email}

AEM Communities使用電子郵件

* [社群通知](notifications.md)
* [社群訂閱](subscriptions.md)

預設情況下，電子郵件功能不起作用，因為它需要指定SMTP伺服器和SMTP用戶。

>[!CAUTION]
>
>電子郵件通知和訂閱必須僅在主要發行者 [上設定](deploy-communities.md#primary-publisher)。

## 預設郵件服務配置 {#default-mail-service-configuration}

通知和訂閱都需要預設的郵件服務。

* 在主要發行者上
* 以管理員權限登入
* 存取 [Web Console](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到 `Day CQ Mail Service`
* 選取編輯圖示

這是以「設定電子郵件通 [知](../../help/sites-administering/notification.md)」的檔案為基礎，但有區別的是，此欄位不 `"From" address` 是必 *要欄位* ，而且應留空。

例如（填入值僅供說明之用）:

![chlimage_1-98](assets/chlimage_1-98.png)

* **[!UICONTROL SMTP伺服器主機名]**:(必 *要)* ，要使用的SMTP伺服器。

* **[!UICONTROL SMTP伺服器端]** 口 *（必需）* SMTP伺服器埠必須是25或更高。

* **[!UICONTROL SMTP用戶]**: *（必需）* SMTP用戶。

* **[!UICONTROL SMTP密碼]**: *（必需）* SMTP用戶的口令。

* **[!UICONTROL 「寄件者」地址]**:留空
* **[!UICONTROL SMTP使用SSL]**:如果勾選，將傳送安全的電子郵件。 確保埠設定為465或SMTP伺服器需要。
* **[!UICONTROL 除錯電子郵件]**:如果選中此選項，則啟用SMTP伺服器交互的日誌記錄。

## AEM Communities電子郵件設定 {#aem-communities-email-configuration}

配置了 [預設郵件服務](#default-mail-service-configuration) ，發行中包含的 `AEM Communities Email Reply Configuration` OSGi配置的兩個現有實例將變為可用。

允許透過電子郵件回覆時，只需進一步設定訂閱的例項。

1. ` [email](#configuration-for-notifications)` 例項

   不支援回覆電子郵件且不應變更的通知

1. ` [subscriptions-email](#configuration-for-subscriptions)` 例項

   需要設定以完全啟用從回覆電子郵件建立貼文

要訪問Communities電子郵件配置實例：

* 在主要發行者上
* 以管理員權限登入
* 存取 [Web Console](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 尋找 `AEM Communities Email Reply Configuration`

![chlimage_1-99](assets/chlimage_1-99.png)

### 通知的設定 {#configuration-for-notifications}

OSGi組態與 `AEM Communities Email Reply Configuration` 名稱電子郵件的例項為立即功能。 此功能不包含電子郵件回覆。

不應更改此配置。

* 找到 `AEM Communities Email Reply Configuration`
* 選取編輯圖示
* 驗證 **名稱**`email`

* 驗證 **從回覆電子郵件建立貼文**`unchecked`

![chlimage_1-100](assets/chlimage_1-100.png)

### 訂閱的設定 {#configuration-for-subscriptions}

對於社群訂閱，可以啟用或停用會員回覆電子郵件以張貼內容的功能。

* 找到 `AEM Communities Email Reply Configuration`
* 選取編輯圖示
* 驗證 **名稱**`subscriptions-email`

![chlimage_1-101](assets/chlimage_1-101.png)

* **[!UICONTROL 名稱]** : *（必要）*`subscriptions-email`。 請勿編輯。

* **[!UICONTROL 從回覆電子郵件建立貼文]**:如果勾選，訂閱電子郵件的收件者可能會透過傳送回覆來張貼內容。 已勾選預設值。
* **[!UICONTROL 新增追蹤ID至標題]**:預設為 `Reply-To`。

* **[!UICONTROL 主旨的最大長度]**:如果追蹤器ID新增至主旨行，則此為主旨的最大長度（不包括追蹤ID），之後會加以修剪。 請注意，這應盡可能小，以免遺失追蹤的ID資訊。 預設值為200。
* **[!UICONTROL 電子郵件「寄件者」地址]**:(必 *要)* ，寄送通知電子郵件的地址。 可能與為默 **認郵件服務指定** 的 [SMTP](#configuredefaultmailservice)用戶相同。 預設為 `no-reply@example.com`。

* **[!UICONTROL 回覆分隔字元]**:如果追蹤器ID已新增至回覆標題，則會使用此分隔字元。 預設值 `+` 為（加號）。

* **[!UICONTROL 主旨中的追蹤器Id首碼]**:如果追蹤器ID已新增至主旨行，則會使用此首碼。 預設為 `post#`。

* **[!UICONTROL 訊息內文中的追蹤器ID首碼]**:如果將追蹤器ID新增至訊息內文，則會使用此首碼。 預設為 `Please do not remove this:`。

* **[!UICONTROL 以HTML形式傳送電子郵件]**:如果勾選，則電子郵件的「內容類型」會設為 `"text/html;charset=utf-8"`。 已勾選預設值。

* **[!UICONTROL 預設用戶名]**:此名稱將用於無名稱用戶。 預設為 `no-reply@example.com`。

* **[!UICONTROL 範本根路徑]**:電子郵件是使用此根路徑中儲存的模板構建的。 預設為 `/etc/community/templates/subscriptions-email`。

## 設定輪詢匯入工具 {#configure-polling-importer}

要將電子郵件導入儲存庫，必須配置輪詢導入程式並手動配置其在儲存庫中的屬性。

### 新增Polling Importer {#add-new-polling-importer}

* 在主要發行者上
* 以管理員權限登入
* 瀏覽至輪詢導入程式控制台例如， [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)
* 選擇「添 **[!UICONTROL 加」]**

![chlimage_1-102](assets/chlimage_1-102.png)

* **[!UICONTROL 類型]**: *（必要）* 下拉式選擇 `POP3 (over SSL).`

* **[!UICONTROL URL]**:(必 *要)* ，出站郵件伺服器。 例如， `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`

* **[!UICONTROL 導入到Path]**&amp;ast;:(必 *要)* ，瀏 `/content/usergenerated/mailFolder/postEmails`覽至資料夾並選 `postEmails`取「確 **定」**

* **[!UICONTROL 更新間隔（秒）]**:(可 *選)* ，為預設郵件服務配置的郵件伺服器可能需要更新時間間隔值。 例如，Gmail可能需要間隔時間 `300`。

* **[!UICONTROL 登入]**: *（可選）*

* **[!UICONTROL 密碼]**: *（可選）*

* 選擇「確 **[!UICONTROL 定」]**

### 調整新輪詢導入程式的協定 {#adjust-protocol-for-new-polling-importer}

儲存新的輪詢設定後，必須進一步修改訂閱電子郵件匯入工具的屬性，才能將通訊協定從變更 `POP3` 為 `emailreply`

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 在主要發行者上
* 以管理員權限登入
* 瀏覽至 [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)
* 選擇新建立的配置
* 修改下列屬性

   * **feedType**:取代 `pop3s` 為 **`emailreply`**
   * **來源**:將源協定替換為 `pop3s://`**`emailreply://`**

![chlimage_1-103](assets/chlimage_1-103.png)

紅色三角形表示已修改的屬性。 請務必儲存變更：

* 選擇「 **[!UICONTROL 全部保存」]**

