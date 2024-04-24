---
title: 設定電子郵件
description: 瞭解如何設定Adobe Experience Manager社群的電子郵件通知和訂閱。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 設定電子郵件 {#configuring-email}

AEM Communities將電子郵件用於：

* [社群通知](notifications.md)
* [Communities 訂閱](subscriptions.md)

依預設，電子郵件功能無法運作，因為它需要SMTP伺服器和SMTP使用者的規格。

>[!CAUTION]
>
>通知和訂閱的電子郵件只能在 [主要發行者](deploy-communities.md#primary-publisher).

## 預設郵件服務設定 {#default-mail-service-configuration}

通知和訂閱都需要預設郵件服務。

* 以系統管理員許可權登入主要發行者並存取 [網頁主控台](../../help/sites-deploying/configuring-osgi.md)：

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到 `Day CQ Mail Service`.
* 選取編輯圖示。

這是根據以下專案的檔案： [設定電子郵件通知](../../help/sites-administering/notification.md)，但不同之處在於此欄位 `"From" address` 是 *非* 必填，且應留空。

例如（填入的值僅供說明用途）：

![email-config](assets/email-config.png)

* **[!UICONTROL smtp伺服器主機名稱]**

  *（必要）* 要使用的SMTP伺服器。

* **[!UICONTROL SMTP伺服器連線埠]**

  *（必要）* SMTP伺服器連線埠必須為25或更高。

* **[!UICONTROL SMTP使用者]**

  *（必要）* smtp使用者。

* **[!UICONTROL SMTP密碼]**

  *（必要）* SMTP使用者的密碼。

* **[!UICONTROL 「寄件者」地址]**

  留空
* **[!UICONTROL SMTP使用SSL]**

  如果勾選，它會傳送安全電子郵件。 請確定連線埠已設為465，或是SMTP伺服器所需的連線埠。
* **[!UICONTROL 除錯電子郵件]**

  如果勾選，就會啟用SMTP伺服器互動的記錄。

## AEM Communities電子郵件設定 {#aem-communities-email-configuration}

一旦 [預設郵件服務](#default-mail-service-configuration) 已設定，則的兩個現有執行個體 `AEM Communities Email Reply Configuration` 此發行版本中包含的OSGi設定開始正常運作。

僅訂閱的執行個體在允許電子郵件回覆時必須進一步設定。

1. [電子郵件](#configuration-for-notifications) 例項：

   對於不支援回覆電子郵件的通知，不應加以變更。

1. [訂閱 — 電子郵件](#configuration-for-subscriptions) 例項：

   需要設定才能完全啟用從回覆電子郵件建立貼文。

若要存取Communities電子郵件設定例項：

* 以系統管理員許可權登入主要發行者並存取 [網頁主控台](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 尋找 `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### 通知的設定 {#configuration-for-notifications}

的例項 `AEM Communities Email Reply Configuration` 使用Name email is forthenotifications功能進行OSGi設定。 此功能不包含電子郵件回覆。

請勿變更此設定。

* 找到 `AEM Communities Email Reply Configuration`.
* 選取編輯圖示。
* 確認 **名稱** 是 `email`.

* 確認 **從回覆電子郵件建立貼文** 是 `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### 訂閱的設定 {#configuration-for-subscriptions}

若為Communities訂閱，可透過回覆電子郵件來啟用或停用成員張貼內容的能力。

* 找到 `AEM Communities Email Reply Configuration`.
* 選取編輯圖示。
* 確認 **名稱** 是 `subscriptions-email`.

  ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL 名稱]**

  *（必要）* `subscriptions-email`. 請勿編輯。

* **[!UICONTROL 從回覆電子郵件建立貼文]**

  如果勾選，訂閱電子郵件的收件者可以透過傳送回覆來張貼內容。 預設為已核取。
* **[!UICONTROL 將追蹤的ID新增至標頭]**

  預設為 `Reply-To`.

* **[!UICONTROL 主旨的長度上限]**

  如果將追蹤器ID新增至主旨行，這是主旨的長度上限（不包括追蹤的ID），之後會加以裁剪。 該值應儘可能小，以避免追蹤的ID資訊遺失。 預設值為200。

* **[!UICONTROL 「回覆」電子郵件地址]**

  用作「回覆」電子郵件地址的地址。 預設為 `no-reply@example.com`.

* **[!UICONTROL 回覆分隔符號]**

  如果將追蹤器ID新增至回覆標題，請使用此分隔符號。 預設為 `+` （加號）。

* **[!UICONTROL 主旨中的追蹤器ID首碼]**

  如果將追蹤器ID新增至主旨行，則會使用此首碼。 預設為 `post#`.

* **[!UICONTROL 訊息本文中的追蹤器ID首碼]**

  如果將追蹤器ID新增至訊息本文，則會使用此首碼。 預設為 `Please do not remove this:`.

* **[!UICONTROL 以HTML傳送電子郵件]**：如果勾選，則會將電子郵件的「內容型別」設為 `"text/html;charset=utf-8"`. 預設為已核取。

* **[!UICONTROL 預設使用者名稱]**

  此名稱不用於名稱使用者。 預設為 `no-reply@example.com`.

* **[!UICONTROL 範本根路徑]**

  電子郵件是使用儲存在此根路徑中的範本所建置。 預設為 `/etc/community/templates/subscriptions-email`.

## 設定輪詢匯入工具 {#configure-polling-importer}

若要將電子郵件匯入存放庫，必須手動設定輪詢匯入工具並在存放庫中設定其屬性。

### 新增輪詢匯入工具 {#add-new-polling-importer}

* 以系統管理員許可權登入主要發行者，並瀏覽至輪詢匯入工具主控台：

  例如， [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* 選取 **[!UICONTROL 新增]**

  ![輪詢匯入工具](assets/polling-importer.png)

* **[!UICONTROL 類型]**

  *（必要）* 下拉以選取 `POP3 (over SSL)`.

* **[!UICONTROL URL]**

  *（必要）* 輸出郵件伺服器。 例如，`pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`。

* **[!UICONTROL 匯入至路徑]**&amp;ast；

  *（必要）* 將設為 `/content/usergenerated/mailFolder/postEmails`
瀏覽至 `postEmails`資料夾並選取 **確定**.

* **[!UICONTROL 以秒為單位的更新間隔]**

  *（可選）* 為預設郵件服務設定的郵件伺服器可能有與更新間隔值相關的要求。 例如，Gmail可能需要 `300`.

* **[!UICONTROL 登入]**

  *（可選）*

* **[!UICONTROL 密碼]**

  *（可選）*

* 選取 **[!UICONTROL 確定]**.

### 調整新輪詢匯入工具的通訊協定 {#adjust-protocol-for-new-polling-importer}

儲存新的輪詢設定後，需要進一步修改訂閱電子郵件匯入工具的屬性，以從變更通訊協定 `POP3` 至 `emailreply`.

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)：

* 以系統管理員許可權登入主要發行者並瀏覽至 [https://&lt;server>：&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* 選取新建立的組態並修改下列屬性：

   * **feedType**：取代 `pop3s` 替換為 **`emailreply`**
   * **來源**：取代來源的通訊協定 `pop3s://` 替換為 **`emailreply://`**

![輪詢通訊協定](assets/polling-protocol.png)

紅色三角形表示修改的屬性。 請務必儲存變更：

* 選取 **[!UICONTROL 全部儲存]**.
