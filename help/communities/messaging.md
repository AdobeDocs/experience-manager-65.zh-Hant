---
title: 配置消息
seo-title: 設定傳訊
description: Communities傳訊
seo-description: Communities傳訊
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: Administrator
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---

# 配置消息{#configure-messaging}

## 概覽 {#overview}

AEM Communities的傳訊功能可讓登入的網站訪客（成員）相互傳送訊息，這些訊息在登入網站時便可存取。

在[社群網站建立](/help/communities/sites-console.md)期間勾選方塊，即可為社群網站啟用傳訊功能。

此頁面提供預設配置和可能調整的資訊。

如需開發人員的其他資訊，請參閱[Messaging Essentials](/help/communities/essentials-messaging.md)。

## 報文傳送操作服務{#messaging-operations-service}

配置[AEM Communities報文傳送操作服務](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl)標識了處理報文傳送相關請求的端點、服務應用於儲存報文的資料夾，以及如果報文可能包含檔案附件，則允許哪些檔案類型。

對於使用`Communities Sites console`建立的社群網站，服務的例項已存在，收件箱設定為`/mail/inbox`。

### 社區消息傳送操作服務{#community-messaging-operations-service}

如下所示，使用[站點建立嚮導](/help/communities/sites-console.md)建立的站點存在服務的配置。 選取設定旁的鉛筆圖示，即可檢視或編輯設定。

![報文傳送操作](assets/messaging-operations.png)

### 新增設定 {#add-new-configuration}

若要新增新設定，請選取服務名稱旁的加號「**+**」圖示：

* **訊息欄位允許清單**

   指定撰寫訊息元件使用者可編輯及保留的屬性。 如果新增了新的表單元素，則需要新增元素ID，才能儲存在SRP中。 預設值為兩個項目：*subject*&#x200B;和&#x200B;*content*。

* **訊息方塊大小限制**

   每個用戶消息框中的最大位元組數。 預設值為&#x200B;*1073741824*(1 GB)。

* **消息計數限制**

   每個使用者允許的訊息總數。 值為–1表示允許的消息數量不限，但以消息框大小限制為前提。 預設值為&#x200B;*10000*(10k)。

* **通知傳送失敗**

   如果已勾選此選項，則在某些收件者無法傳送訊息時通知寄件者。 預設值為&#x200B;*checked*。

* **失敗傳送寄件者ID**

   傳送失敗訊息中顯示的寄件者名稱。 預設值為&#x200B;*failureNotifier*。

* **失敗消息模板路徑**

   傳送失敗的訊息範本根的絕對路徑。 預設值為&#x200B;*/etc/notification/messaging/default*。

* **重試次數**

   嘗試重新傳送失敗訊息的次數。 預設值為&#x200B;*3*。

* **在重試之間等待**

   嘗試在無法發送時重新發送消息之間等待的秒數。 預設值為&#x200B;*100*（秒）。

* **計數更新池大小**

   用於計數更新的併發線程數。 預設值為&#x200B;*10*。

* **收件匣路徑**

   （*必要*）相對於使用者節點(/home/users/*username*)的路徑，用於`inbox`資料夾。 路徑不得以尾隨正斜線「/」結尾。 預設值為&#x200B;*/mail/inbox*。

* **已傳送項目路徑**

   （*必要*）相對於使用者節點(/home/users/*username*)的路徑，用於`sent items`資料夾。 路徑不得以尾隨正斜線「/」結尾。 預設值為&#x200B;*/mail/sentitems* 。

* **支援附件**

   如果勾選此選項，使用者就能將附件新增至其訊息。 預設值為&#x200B;*checked*。

* **啟用組消息**

   如果選中，註冊用戶可以向一組成員發送大量消息。 預設值為&#x200B;*取消選取*。

* **最大值否。收件者總數**

   如果已啟用組消息，請指定一次可發送到的組消息的最大收件人數。 預設值為&#x200B;*100*。

* **批次大小**

   傳送給大群收件者時，要一起批次傳送的訊息數。 預設值為&#x200B;*100*。

* **總附件大小**

   如果選中了supportAttachments，此值將指定所有附件的最大允許總大小（以位元組為單位）。 預設值為&#x200B;*104857600*(100 MB)。

* **附件類型封鎖清單**

   副檔名為的封鎖清單，首碼為「**」。**&#39;，系統將拒絕此選項。如果未列入封鎖名單，則允許擴充功能。 可以使用「**+**」和「**-**」表徵圖添加或刪除擴展。

* **允許的附件類型**

   **(*需要動作*)** 副檔名的允許清單，與封鎖清單相反。若要允許所有副檔名，但列入封鎖名單的除外，請使用「**-**」圖示來移除單一空白項目。

* **服務選擇器**

   （*必要*）呼叫服務的絕對路徑（端點）（虛擬資源）。 所選路徑的根必須包含在OSGi配置[ `Apache Sling Servlet/Script Resolver and Error Handler` ](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)的&#x200B;*執行路徑*&#x200B;配置設定中，如`/bin/`、`/apps/`和`/services/`。 要為站點的消息功能選擇此配置，此端點將作為`Message List and Compose Message components`的&#x200B;**`Service selector`**&#x200B;值提供（請參閱[消息功能](/help/communities/configure-messaging.md)）。

   預設值為&#x200B;*/bin/messaging* 。

* **欄位允許清單**

   使用&#x200B;**消息欄位允許清單**。

>[!CAUTION]
>
>每次開啟`Messaging Operations Service`配置進行編輯時，如果已刪除`allowedAttachmentTypes.name`，則會重新添加一個空條目，以使屬性可配置。 單個空條目有效地禁用了檔案附件。
>
>若要允許所有副檔名，除那些已列入封鎖名單的副檔名外，請使用「**-**」圖示以（再次）在按一下&#x200B;**Save**&#x200B;前移除單一空白項目。

## 組消息{#group-messaging}

若要允許註冊用戶向用戶組批量發送直接消息，請確保在以下兩個實例中&#x200B;**消息操作服務**&#x200B;配置中啟用組消息&#x200B;**:**

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**報文傳送操作服務：社交主控台**

![social-console-op-service](assets/social-console-op-service.png)

**報文傳送操作服務：社交訊息**

![social-message-op-service](assets/social-message-op-service.png)

## 疑難排解 {#troubleshooting}

疑難排解問題的一種方式是啟用日誌中的[調試消息。](/help/sites-administering/troubleshooting.md)

另請參閱[個別服務的記錄器和寫入器](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)。

要監視的包為`com.adobe.cq.social.messaging`。
