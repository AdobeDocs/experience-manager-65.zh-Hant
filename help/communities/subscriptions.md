---
title: Communities 訂閱
seo-title: Communities Subscriptions
description: 社區成員通過電子郵件與其他成員交互
seo-description: Community members interact with other members through email
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Communities 訂閱 {#communities-subscriptions}

## 概觀 {#overview}

截至社區 [FP1](deploy-communities.md#latestfeaturepack)，社區成員可以使用稱為訂閱的功能通過電子郵件與社區進行交互。

訂閱與 [通知](notifications.md) 成員在關注部落格、論壇主題或QnA問題時可以訂閱。

將訂閱與通知區分的是：

* 成員在跟蹤其他成員時不能訂閱。
* 成員唯一要執行的操作是選擇 `Email Subscriptions` 下。
* 當配置電子郵件回復時，成員可以通過簡單地回復接收的電子郵件來有效地發佈內容。

### 要求 {#requirements}

**配置電子郵件**

必須配置電子郵件，使訂閱功能正常，並使成員通過電子郵件進行回復。

有關設定電子郵件的說明，請參見 [配置電子郵件](email.md)。

**啟用訂閱並遵循**

必須配置元件以啟用訂閱 *和* 。 允許訂閱的功能是 [部落格](blog-feature.md)。 [論壇](forum.md) 和 [QnA](working-with-qna.md)。

## 以下訂閱 {#subscriptions-from-following}

![訂閱跟蹤](assets/subscription-following.png)

的 **關注** 按鈕提供了將條目作為活動、訂閱和/或通知跟蹤的方法。 每次 **關注** 按鈕，可以開啟或關閉選定內容。

如果選擇了以下任何方法，則按鈕的文本將更改為 **跟蹤**。 為方便起見，可以選擇 `Unfollow All` 關閉所有方法。

的 **關注** 按鈕將包括 `Email Subscriptions` 選項，僅在將論壇、QnA或部落格配置為啟用電子郵件訂閱時。 此按鈕將出現：

* 在啟用的論壇的主功能頁面上，QnA或部落格將針對該功能下的所有活動發送電子郵件。

* 對於特定條目，如論壇主題、QnA問題或部落格，當該特定條目有活動時將發送電子郵件。

## 通過電子郵件答復 {#reply-by-email}

當電子郵件 [已配置為通過電子郵件回復](email.md#configure-polling-importer)，訂閱的成員將收到一封包含已發佈內容和指向線上內容的連結的電子郵件。

如果他們回復電子郵件，他們在回復中輸入的內容將作為內容線上顯示。

![電子郵件回復](assets/email-reply.png)

回復發佈所花費的時間由 [輪詢導入程式的更新間隔](email.md#configure-polling-importer)。

![QA](assets/qa.png)
