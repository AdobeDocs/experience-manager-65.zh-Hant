---
title: 配置消息
seo-title: Configuring Messaging
description: Communities傳訊
seo-description: Communities messaging
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---

# 配置消息 {#configure-messaging}

## 概觀 {#overview}

AEM Communities的傳訊功能可讓登入的網站訪客（成員）相互傳送訊息，這些訊息在登入網站時便可存取。

在 [社群網站建立](/help/communities/sites-console.md).

此頁面提供預設配置和可能調整的資訊。

如需開發人員的其他資訊，請參閱 [Messaging Essentials](/help/communities/essentials-messaging.md).

## 報文傳送操作服務 {#messaging-operations-service}

設定 [AEM Communities傳訊作業服務](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) 標識處理郵件相關請求的端點、服務應用於儲存郵件的資料夾，以及如果郵件中可能包含檔案附件，則允許哪些檔案類型。

針對使用 `Communities Sites console`，服務的例項已存在，而收件匣設為 `/mail/inbox`.

### 社區消息傳送操作服務 {#community-messaging-operations-service}

如下所示，使用建立的網站已具備服務的設定 [網站建立精靈](/help/communities/sites-console.md). 選取設定旁的鉛筆圖示，即可檢視或編輯設定。

![報文傳送操作](assets/messaging-operations.png)

### 新增設定 {#add-new-configuration}

要添加新配置，請選擇加號「**+**&#x200B;服務名稱旁的「 」圖示：

* **訊息欄位允許清單**

   指定撰寫訊息元件使用者可編輯及保留的屬性。 如果新增了新的表單元素，則需要新增元素ID，才能儲存在SRP中。 預設值為兩個項目： *主旨* 和 *內容*.

* **訊息方塊大小限制**

   每個用戶消息框中的最大位元組數。 預設為 *1073741824* (1 GB)。

* **消息計數限制**

   每個使用者允許的訊息總數。 值為–1表示允許的消息數量不限，但以消息框大小限制為前提。 預設為 *10000* (10k)。

* **通知傳送失敗**

   如果已勾選此選項，則在某些收件者無法傳送訊息時通知寄件者。 預設為 *已勾選*.

* **失敗傳送寄件者ID**

   傳送失敗訊息中顯示的寄件者名稱。 預設為 *failureNotifier*.

* **失敗消息模板路徑**

   傳送失敗的訊息範本根的絕對路徑。 預設為 */etc/notification/messaging/default*.

* **重試次數**

   嘗試重新傳送失敗訊息的次數。 預設為 *3*.

* **在重試之間等待**

   嘗試在無法發送時重新發送消息之間等待的秒數。 預設為 *100* （秒）。

* **計數更新池大小**

   用於計數更新的併發線程數。 預設為 *10*.

* **收件匣路徑**

   (*必填*)相對於使用者節點(/home/users/*用戶名*)，以用於 `inbox` 檔案夾。 路徑不得以尾隨正斜線「/」結尾。 預設為 */mail/inbox*.

* **已傳送項目路徑**

   (*必填*)相對於使用者節點(/home/users/*用戶名*)，以用於 `sent items` 檔案夾。 路徑不得以尾隨正斜線「/」結尾。 預設為 */mail/sentitems* .

* **支援附件**

   如果勾選此選項，使用者就能將附件新增至其訊息。 預設為 *已勾選*.

* **啟用組消息**

   如果選中，註冊用戶可以向一組成員發送大量消息。 預設為 *已選取*.

* **最大值否。 收件者總數**

   如果已啟用組消息，請指定一次可發送到的組消息的最大收件人數。 預設為 *100*.

* **批次大小**

   傳送給大群收件者時，要一起批次傳送的訊息數。 預設為 *100*.

* **總附件大小**

   如果選中了supportAttachments，此值將指定所有附件的最大允許總大小（以位元組為單位）。 預設為 *104857600* (100 MB)。

* **附件類型封鎖清單**

   副檔名為的封鎖清單，首碼為「**.**&#39;，系統將拒絕此選項。 如果未列入封鎖名單，則允許擴充功能。 可使用&#x200B;**+**&#39;和&#39;**-**」表徵圖。

* **允許的附件類型**

   **(*需要的操作*)** 副檔名的允許清單，與封鎖清單相反。 若要允許所有副檔名，但列入封鎖名單者除外，請使用「**-**「 」表徵圖，刪除單個空條目。

* **服務選擇器**

   (*必填*)呼叫服務的絕對路徑（端點）（虛擬資源）。 所選路徑的根必須包含在 *執行路徑* OSGi配置的配置設定 [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)，例如 `/bin/`, `/apps/`，和 `/services/`. 要為站點的消息傳送功能選擇此配置，將提供此端點作為 **`Service selector`** 值 `Message List and Compose Message components` (請參閱 [訊息功能](/help/communities/configure-messaging.md))。

   預設為 */bin/messaging* .

* **欄位允許清單**

   使用 **訊息欄位允許清單**.

>[!CAUTION]
>
>每次a `Messaging Operations Service` 若要編輯，請開啟設定 `allowedAttachmentTypes.name` 已移除，則會重新新增空白項目，以讓屬性可設定。 單個空條目有效地禁用了檔案附件。
>
>若要允許所有副檔名，但列入封鎖名單者除外，請使用「**-**「 」表徵圖，在按一下 **儲存**.

## 群組訊息 {#group-messaging}

若要允許註冊的使用者大量傳送直接訊息給使用者群組，請務必 **啟用組消息** 在以下兩個例項中 **報文傳送操作服務** 配置：

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**報文傳送操作服務：社交主控台**

![social-console-op-service](assets/social-console-op-service.png)

**報文傳送操作服務：社交訊息**

![social-message-op-service](assets/social-message-op-service.png)

## 疑難排解 {#troubleshooting}

疑難排解的一種方式是啟用 [在日誌中調試消息。](/help/sites-administering/troubleshooting.md)

另請參閱 [個人服務的記錄器和撰寫器](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

要監視的包是 `com.adobe.cq.social.messaging`.
