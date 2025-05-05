---
title: 設定傳訊
description: 瞭解AEM Communities中的傳訊功能，該功能讓登入的網站訪客（成員）能夠相互傳送訊息。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# 設定傳訊 {#configure-messaging}

## 概觀 {#overview}

AEM Communities的傳訊功能讓登入的網站訪客（成員）能夠傳送訊息給其他人，這些訊息在登入網站時可供存取。

在[社群網站建立](/help/communities/sites-console.md)期間勾選方塊，即可啟用社群網站的傳訊功能。

此頁面包含預設設定和可能調整的相關資訊。

如需開發人員的其他資訊，請參閱[傳訊要點](/help/communities/essentials-messaging.md)。

## 傳訊操作服務 {#messaging-operations-service}

設定[AEM Communities訊息操作服務](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl)會識別處理訊息相關請求的端點、服務應用來儲存訊息的資料夾，以及如果訊息可能包含檔案附件，允許哪些檔案型別。

對於使用`Communities Sites console`建立的社群網站，服務的執行個體已存在，收件匣設為`/mail/inbox`。

### 社群傳訊操作服務 {#community-messaging-operations-service}

如下所示，使用[網站建立精靈](/help/communities/sites-console.md)建立的網站已有服務的組態。 選取組態旁邊的鉛筆圖示，即可檢視或編輯組態。

![傳訊作業](assets/messaging-operations.png)

### 新增設定 {#add-new-configuration}

若要新增設定，請選取服務名稱旁的加號&#39;**+**&#39;圖示：

* **訊息欄位允許清單**

  指定使用者可編輯及儲存的撰寫訊息元件屬性。 如果新增了新表單元素，則必須新增元素ID （如果需要）以儲存在SRP中。 預設為兩個專案： *主旨*&#x200B;和&#x200B;*內容*。

* **訊息方塊大小限制**

  每位使用者訊息方塊中的最大位元組數。 預設值為&#x200B;*1073741824* (1 GB)。

* **訊息計數限制**

  每位使用者允許的訊息總數。 值為–1表示允許無限數量的訊息，受訊息方塊大小限制。 預設值為&#x200B;*10000* (10k)。

* **通知傳送失敗**

  如果勾選，如果郵件無法傳遞給某些收件者，則通知寄件者。 預設為&#x200B;*已核取*。

* **傳送寄件者識別碼**&#x200B;失敗

  顯示在傳送失敗訊息中的寄件者名稱。 預設值為&#x200B;*failureNotifier*。

* **失敗訊息範本路徑**

  傳遞失敗訊息範本根目錄的絕對路徑。 預設值為&#x200B;*/etc/notification/messaging/default*。

* **重試次數**

  嘗試重新傳送無法傳遞之訊息的次數。 預設值為&#x200B;*3*。

* **在重試之間等待**

  傳送失敗時嘗試重新傳送訊息之間等待的秒數。 預設值為&#x200B;*100* （秒）。

* **計數更新集區大小**

  用於計數更新的並行執行緒數目。 預設值為&#x200B;*10*。

* **收件匣路徑**

  （*必要*）使用於`inbox`資料夾的路徑(相對於使用者的節點（/home/users/*使用者名稱*）)。 路徑不能以正斜線&#39;/&#39;結尾。 預設值為&#x200B;*/郵件/收件匣*。

* **傳送的專案路徑**

  （*必要*）使用於`sent items`資料夾的路徑(相對於使用者的節點（/home/users/*使用者名稱*）)。 路徑不能以正斜線&#39;/&#39;結尾。 預設值為&#x200B;*/mail/sentitems* 。

* **支援附件**

  如果勾選，使用者可以將附件新增至其訊息。 預設為&#x200B;*已核取*。

* **啟用群組訊息**

  如果選取，註冊的使用者可以傳送大量訊息給一組成員。 預設為&#x200B;*已取消選取*。

* **最大數量 收件者總數**

  如果已啟用群組訊息，請指定一次可傳送群組訊息的收件者數目上限。 預設值為&#x200B;*100*。

* **批次大小**

  傳送給大量收件者時，要批次處理以供傳送的訊息數。 預設值為&#x200B;*100*。

* **附件大小總計**

  如果核取supportAttachments，此值會指定所有附件允許的總大小上限（位元組）。 預設值為&#x200B;*104857600* (100 MB)。

* **附件型別封鎖清單**

  檔案名稱副檔名的封鎖清單，前置詞為&#39;**。**&#39;，已被系統拒絕。 如果未加入封鎖清單，則允許此擴充功能。 可以使用&#39;**+**&#39;和&#39;**-**&#39;圖示來新增或移除擴充功能。

* **允許的附件型別**

  **（*需要動作*）**&#x200B;副檔名的允許清單，與封鎖清單相反。 若要允許所有副檔名（已加入封鎖清單的副檔名除外），請使用&#39;**-**&#39;圖示來移除單一空白專案。

* **服務選擇器**

  （*必要*）用來呼叫服務的絕對路徑（端點） （虛擬資源）。 選擇的路徑根必須包含在OSGi設定[`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)的&#x200B;*執行路徑*&#x200B;設定中，例如`/bin/`、`/apps/`和`/services/`。 若要為網站的訊息功能選取此設定，此端點會提供為`Message List and Compose Message components`的&#x200B;**`Service selector`**&#x200B;值（請參閱[訊息功能](/help/communities/configure-messaging.md)）。

  預設值為&#x200B;*/bin/傳訊* 。

* **欄位允許清單**

  使用&#x200B;**訊息欄位允許清單**。

>[!CAUTION]
>
>每次開啟`Messaging Operations Service`設定進行編輯時，如果移除了`allowedAttachmentTypes.name`，則會讀取空白專案以使屬性可設定。 單一空白專案會有效停用檔案附件。
>
>若要允許所有副檔名（已加入封鎖清單的副檔名除外），請使用&#39;**-**&#39;圖示來移除單一空白專案，再按一下[儲存]。**&#x200B;**

## 群組訊息 {#group-messaging}

若要允許註冊的使用者大量傳送直接訊息給使用者群組，請確定在下列兩個&#x200B;**傳訊操作服務**&#x200B;組態的執行個體中&#x200B;**啟用群組傳訊**：

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**訊息操作服務：社交主控台**

![social-console-op-service](assets/social-console-op-service.png)

**訊息操作服務：社交訊息**

![social-message-op-service](assets/social-message-op-service.png)

## 疑難排解 {#troubleshooting}

疑難排解問題的一種方式是啟用記錄檔中的[偵錯訊息。](/help/sites-administering/troubleshooting.md)

另請參閱個別服務的[記錄器及寫入器](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)。

要監視的封裝是`com.adobe.cq.social.messaging`。
