---
title: Communities 訂閱
description: 社群成員透過電子郵件與其他成員互動
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Communities 訂閱 {#communities-subscriptions}

## 概觀 {#overview}

在社群[FP1](deploy-communities.md#latestfeaturepack)中，社群成員可使用稱為訂閱的功能，透過電子郵件與社群互動。

訂閱類似於[通知](notifications.md)，因為成員在關注部落格、論壇主題或問題清單問題時可能會訂閱。

訂閱與通知的區別在於：

* 成員在下列其他成員時不得訂閱。
* 成員唯一要採取的動作是在執行動作時選取`Email Subscriptions`。
* 設定電子郵件回覆時，成員只需回覆收到的電子郵件，即可有效張貼內容。

### 要求 {#requirements}

**設定電子郵件**

您必須設定電子郵件，才能讓訂閱正常運作，並讓成員透過電子郵件回覆。

如需設定電子郵件的說明，請參閱[設定電子郵件](email.md)。

**啟用訂閱並關注**

元件必須設定為啟用後續的訂閱&#x200B;*和*。 允許訂閱的功能為[部落格](blog-feature.md)、[論壇](forum.md)和[QnA](working-with-qna.md)。

## 來自下列的訂閱 {#subscriptions-from-following}

![訂閱正在關注](assets/subscription-following.png)

**追隨**&#x200B;按鈕提供將專案作為活動、訂閱和/或通知進行追蹤的方法。 每次選取&#x200B;**追隨**&#x200B;按鈕時，都可以開啟或關閉選取專案。

如果選取任何追蹤方法，按鈕的文字會變更為&#x200B;**追蹤**。 為方便起見，可以選取`Unfollow All`以關閉所有方法。

**關注**&#x200B;按鈕只有在論壇、QnA或部落格設定為啟用電子郵件訂閱時才包含`Email Subscriptions`選項。 此按鈕將會出現：

* 在啟用的論壇、QnA或部落格的主要功能頁面上，將針對該功能下的所有活動傳送電子郵件。

* 針對特定專案，例如論壇主題、QnA問題或部落格。當該特定專案有活動時，將傳送電子郵件。

## 透過電子郵件回覆 {#reply-by-email}

當電子郵件[設定為要透過電子郵件](email.md#configure-polling-importer)回覆時，訂閱的成員將會收到包含張貼內容及線上內容連結的電子郵件。

如果他們回覆電子郵件，他們在回覆中輸入的內容將顯示為線上內容。

![電子郵件回覆](assets/email-reply.png)

張貼回覆所需的時間由[輪詢匯入工具的更新間隔](email.md#configure-polling-importer)控制。

![QA](assets/qa.png)
