---
title: 配置消息
seo-title: Configuring Messaging
description: 社區消息
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

AEM Communities的消息傳遞功能提供了登錄站點訪問者（成員）向彼此發送在登錄站點時可訪問的消息的能力。

通過選中框為社區站點啟用消息 [社區網站建立](/help/communities/sites-console.md)。

此頁提供有關預設配置和可能調整的資訊。

有關開發人員的其他資訊，請參見 [消息傳送軟體包](/help/communities/essentials-messaging.md)。

## 消息傳遞操作服務 {#messaging-operations-service}

配置 [AEM Communities消息服務](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) 標識處理與消息相關的請求的終結點、服務應用於儲存消息的資料夾，以及如果消息可能包含檔案附件，則允許使用哪些檔案類型。

對於使用 `Communities Sites console`，服務實例已存在，收件箱設定為 `/mail/inbox`。

### 社區消息傳遞操作服務 {#community-messaging-operations-service}

如下所示，對於使用 [站點建立嚮導](/help/communities/sites-console.md)。 通過選擇配置旁邊的鉛筆表徵圖，可以查看或編輯配置。

![消息傳遞操作](assets/messaging-operations.png)

### 新增設定 {#add-new-configuration}

要添加新配置，請選擇加號「**+**「 」表徵圖（位於服務名稱旁）:

* **消息欄位允許清單**

   指定合成消息元件用戶可以編輯和保留的屬性。 如果添加了新的表單元素，則如果需要將元素ID儲存在SRP中，則需要添加。 預設值為兩個條目： *主題* 和 *內容*。

* **消息框大小限制**

   每個用戶消息框中的最大位元組數。 預設值為 *1073741824* (1 GB)。

* **消息計數限制**

   每個用戶允許的消息總數。 值為–1表示允許的消息數不限，但受消息框大小限制的限制。 預設值為 *10000* (10k)。

* **通知傳遞失敗**

   如果選中，則在某些收件人的郵件傳遞失敗時通知發件人。 預設值為 *已檢查*。

* **傳遞發件人ID失敗**

   傳遞失敗消息中顯示的發件人名稱。 預設值為 *失敗通告程式*。

* **失敗消息模板路徑**

   傳遞失敗消息模板根的絕對路徑。 預設值為 */etc/notification/messaging/default*。

* **重試次數**

   嘗試重新發送未能傳遞的消息的次數。 預設值為 *3*。

* **重試之間等待**

   在發送失敗時嘗試重新發送消息之間等待的秒數。 預設值為 *100* （秒）。

* **計數更新池大小**

   用於計數更新的併發線程數。 預設值為 *10*。

* **收件箱路徑**

   (*必需*)相對於用戶節點的路徑(/home/users/*用戶名*)，用於 `inbox` 的子菜單。 路徑不能以尾隨正斜槓「/」結束。 預設值為 */mail/inbox*。

* **已發送項路徑**

   (*必需*)相對於用戶節點的路徑(/home/users/*用戶名*)，用於 `sent items` 的子菜單。 路徑不能以尾隨正斜槓「/」結束。 預設值為 */mail/sentitems* 。

* **支援附件**

   如果選中，則用戶可以將附件添加到其郵件中。 預設值為 *已檢查*。

* **啟用組消息**

   如果選中，則註冊用戶可以向一組成員發送批量消息。 預設值為 *已取消*。

* **最大數。 總收件人數**

   如果啟用了組消息傳遞，請指定每次可以向其發送組消息的最大收件人數。 預設值為 *100*。

* **批次大小**

   發送到大組收件人時要一起批處理的發送郵件數。 預設值為 *100*。

* **附件總大小**

   如果選中supportAttachments，則此值指定所有附件的最大允許總大小（以位元組為單位）。 預設值為 *104857600* (100 MB)。

* **附件類型塊清單**

   檔案副檔名的塊清單，前置詞為「**。**&#x200B;被系統拒絕。 如果未列出阻止，則允許擴展。 可以使用「 」添加或刪除擴展&#x200B;**+**&#39;和&#39;**-**&#39;表徵圖。

* **允許的附件類型**

   **(*需要操作*)** 檔案名擴展的允許清單，與塊清單相反。 要允許除列出的塊之外的所有檔案副檔名，請使用「**-**「表徵圖，刪除單個空條目。

* **服務選擇器**

   (*必需*)調用服務的絕對路徑（端點）（虛擬資源）。 所選路徑的根必須包含在 *執行路徑* OSGi配置的配置設定 [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)，例如 `/bin/`。 `/apps/`, `/services/`。 要為站點的消息傳遞功能選擇此配置，將提供此終結點作為 **`Service selector`** 值 `Message List and Compose Message components` （請參見） [消息功能](/help/communities/configure-messaging.md))。

   預設值為 */bin/消息* 。

* **欄位允許清單**

   使用 **消息欄位允許清單**。

>[!CAUTION]
>
>每次 `Messaging Operations Service` 如果開啟了要編輯的配置 `allowedAttachmentTypes.name` 刪除後，將重新添加一個空條目，以使屬性可配置。 單個空條目會有效禁用檔案附件。
>
>要允許除列出的塊之外的所有檔案副檔名，請使用「**-**「表徵圖：在按一下 **保存**。

## 組消息 {#group-messaging}

要允許註冊用戶批量向用戶組發送直接消息，請確保 **啟用組消息** 在以下兩個實例中 **消息傳遞操作服務** 配置：

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**消息傳遞操作服務：社交控制台**

![社交控制台操作服務](assets/social-console-op-service.png)

**消息傳遞操作服務：社交資訊**

![社交消息業務](assets/social-message-op-service.png)

## 疑難排解 {#troubleshooting}

解決問題的一種方法是啟用 [調試日誌中的消息。](/help/sites-administering/troubleshooting.md)

另請參閱 [個人服務的伐木者和作家](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)。

要監視的包是 `com.adobe.cq.social.messaging`。
