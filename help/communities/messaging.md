---
title: 配置消息
seo-title: 配置消息
description: 社群訊息
seo-description: 社群訊息
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---


# 配置消息 {#configure-messaging}

## 概覽 {#overview}

AEM Communities的訊息功能可讓登入網站訪客（成員）彼此傳送訊息，當登入網站時，這些訊息可供存取。

在社群網站建立期間核取方塊，即可啟用社群 [網站的訊息](/help/communities/sites-console.md)。

此頁包含有關預設配置和可能調整的資訊。

如需開發人員的詳細資訊，請參 [閱Messaging Essentials](/help/communities/essentials-messaging.md)。

## 消息傳遞操作服務 {#messaging-operations-service}

配置 [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) ，可識別處理訊息相關要求的端點、服務應用來儲存訊息的檔案夾，以及如果訊息可能包含檔案附件，允許使用哪些檔案類型。

對於使用建立的社 `Communities Sites console`區站點，服務實例已存在，收件箱設定為 `/mail/inbox`。

### 社群訊息運作服務 {#community-messaging-operations-service}

如下所示，對於使用站點建立嚮導建立的站點，服務 [的配置存在](/help/communities/sites-console.md)。 選取設定旁的鉛筆圖示，即可檢視或編輯設定。

![消息傳遞操作](assets/messaging-operations.png)

### 新增設定 {#add-new-configuration}

要添加新配置，請選擇服務名稱旁邊的加號&#x200B;**&#39;+**&#39;表徵圖：

* **消息欄位允許清單**

   指定合成消息元件用戶可以編輯和保存的屬性。 如果新增了表單元素，則需要新增元素ID，才能儲存在SRP中。 預設為兩個項目： *主題* 和 *內容*。

* **訊息方塊大小限制**

   每個用戶消息框中的最大位元組數。 預設 *為1073741824* (1 GB)。

* **消息計數限制**

   每個用戶允許的消息總數。 值-1表示允許的消息數不限，但須受消息框大小限制。 預設值 *為1000* (10k)。

* **通知傳送失敗**

   如果勾選此選項，則在某些收件者無法傳送訊息時通知傳送者。 已勾選預 *設值*。

* **傳送傳送者ID失敗**

   顯示在傳送失敗訊息中的傳送者名稱。 預設值為 *failureNotifier*。

* **失敗消息模板路徑**

   傳送失敗訊息範本根目錄的絕對路徑。 預設值 *為/etc/notification/messaging/default*。

* **重試次數**

   嘗試重新傳送失敗訊息的次數。 預設值 *為3*。

* **重試間等待**

   嘗試在無法傳送時重新傳送訊息之間等待的秒數。 預設值 *為* 100（秒）。

* **計算更新池大小**

   用於計數更新的併發線程數。 預設值 *為10*。

* **收件箱路徑**

   (必&#x200B;*要*)用於資料夾的路徑，相對於用戶節點(/home/users/*username*) `inbox` 。 路徑不能以尾隨正斜線&#39;/&#39;結束。 預設值 *為/mail/inbox*。

* **已傳送項目路徑**

   (必&#x200B;*要*)用於資料夾的路徑，相對於用戶節點(/home/users/*username*) `sent items` 。 路徑不能以尾隨正斜線&#39;/&#39;結束。 預設值 *為/mail/sentitems* 。

* **支援附件**

   如果選中此選項，用戶可以將附件添加到其郵件中。 已勾選預 *設值*。

* **啟用群組訊息**

   如果選取此選項，註冊的使用者可以傳送大量訊息給成員群組。 預設為 *取消選取*。

* **最大值。 收件者總數**

   如果啟用群組訊息，請指定一次可傳送群組訊息給的收件者數目上限。 預設值 *為100*。

* **批次大小**

   傳送給大量收件者群組時，要一起批次傳送的訊息數。 預設值 *為100*。

* **附件大小總計**

   如果選中了supportAttachments，此值將指定所有附件的允許總大小（以位元組為單位）上限。 預設值 *為104857600* (100 MB)。

* **附件類型塊清單**

   副檔名的區塊清單，前置詞為&#39;**。**&#x200B;被制度拒絕。 如果未列出阻止，則允許擴展。 可使用「**+**」和「**-**」圖示新增或移除延伸模組。

* **允許的附件類型**

   **(需&#x200B;*要操作*** )副檔名的允許清單，與塊清單相反。 若要允許除列出的區塊以外的所有副檔名，請使用「**-**」圖示來移除單一空白項目。

* **服務選擇器**

   (必&#x200B;*要*)呼叫服務的絕對路徑（端點）（虛擬資源）。 所選路徑的根必須包含在OSGi配置的「 *Execution Paths* （執行路徑）」配 [ 置設定中， `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)如 `/bin/`、 `/apps/`和中 `/services/`。 要為站點的消息功能選擇此配置，此端點將作為 **`Service selector`** 的值提 `Message List and Compose Message components` 供(請 [參閱消息功能](/help/communities/configure-messaging.md))。

   預設值為 */bin/messaging* 。

* **欄位允許清單**

   使用 **消息欄位允許清單**。

>[!CAUTION]
>
>每次開啟 `Messaging Operations Service` 配置進行編輯時，如果已刪 `allowedAttachmentTypes.name` 除，則會重新添加一個空條目，使屬性可配置。 單個空條目有效地禁用檔案附件。
>
>要允許除列出的塊外的所有檔案副檔名，請使用「**-**」表徵圖刪除單個空條目（再次），然後按一下「 **保存」**。

## 群組訊息 {#group-messaging}

要允許註冊用戶批量向用戶組發送直接消息，請確保在以下兩個 **Messaging Operation Services配置實例中啟用組消息** 傳遞 **** :

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**消息傳遞操作服務：社交主控台**

![social-console-op-service](assets/social-console-op-service.png)

**消息傳遞操作服務：社交訊息**

![social-message-op-service](assets/social-message-op-service.png)

## 疑難排解 {#troubleshooting}

疑難排解問題的一種方式是啟用 [記錄檔中的除錯訊息。](/help/sites-administering/troubleshooting.md)

另請參閱 [個別服務的記錄者和撰寫者](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)。

要監視的包是 `com.adobe.cq.social.messaging`。
