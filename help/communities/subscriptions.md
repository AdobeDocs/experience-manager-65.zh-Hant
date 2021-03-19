---
title: Communities 訂閱
seo-title: Communities 訂閱
description: 社群成員透過電子郵件與其他成員互動
seo-description: 社群成員透過電子郵件與其他成員互動
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 2%

---


# Communities 訂閱 {#communities-subscriptions}

## 概覽 {#overview}

從社群[FP1](deploy-communities.md#latestfeaturepack)開始，社群成員可以使用稱為訂閱的功能，透過電子郵件與社群互動。

訂閱類似於[notifications](notifications.md)，因為當關注部落格文章、論壇主題或QnA問題時，成員可以訂閱。

訂閱與通知的區別在於：

* 成員在追隨其他成員時不得訂閱。
* 成員唯一要執行的操作是選擇`Email Subscriptions` ，如果遵循下列操作。
* 當設定電子郵件回覆時，會員只要回覆收到的電子郵件，就可以有效地張貼內容。

### 要求{#requirements}

**設定電子郵件**

必須設定電子郵件，才能讓訂閱發揮功能，讓成員以電子郵件回覆。

有關設定電子郵件的說明，請參閱[配置電子郵件](email.md)。

**啟用訂閱並追蹤**

必須配置元件以啟用訂閱&#x200B;*和*。 允許訂閱的功能有[blog](blog-feature.md)、[論壇](forum.md)和[QnA](working-with-qna.md)。

## {#subscriptions-from-following}之後的訂閱

![訂閱追蹤](assets/subscription-following.png)

**Follow**&#x200B;按鈕提供了跟蹤條目作為活動、訂閱和／或通知的方法。 每次選擇&#x200B;**Follow**&#x200B;按鈕時，都可以開啟或關閉選擇。

如果選擇了任何下列方法，則按鈕的文本將更改為&#x200B;**Following**。 為方便起見，您可以選取`Unfollow All`來關閉所有方法。

**Follow**&#x200B;按鈕只有在將論壇、QnA或部落格設定為啟用電子郵件訂閱時，才會包含`Email Subscriptions`選項。 此按鈕將會出現：

* 在啟用論壇的主功能頁面上，QnA或部落格將針對該功能下的所有活動傳送電子郵件。

* 對於特定項目，如論壇主題、QnA問題或部落格，當該特定項目有活動時，將發送電子郵件。

## 電子郵件回覆{#reply-by-email}

當電子郵件設定為[以透過電子郵件](email.md#configure-polling-importer)回覆時，訂閱的會員將會收到電子郵件，內含已張貼的內容和線上內容的連結。

如果回覆電子郵件，則回覆中輸入的內容會顯示為線上內容。

![電子郵件回覆](assets/email-reply.png)

回覆張貼所花費的時間量由[輪詢匯入工具的更新間隔](email.md#configure-polling-importer)控制。

![QA](assets/qa.png)

