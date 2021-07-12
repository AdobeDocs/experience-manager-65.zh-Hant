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
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# Communities 訂閱 {#communities-subscriptions}

## 概覽 {#overview}

自社群[FP1](deploy-communities.md#latestfeaturepack)起，社群成員可透過電子郵件使用稱為訂閱的功能與社群互動。

訂閱類似於[notifications](notifications.md)，因為成員在遵循部落格文章、論壇主題或QnA問題時可以訂閱。

訂閱與通知的區別在於：

* 成員在以下成員時不能訂閱。
* 成員執行的唯一操作是選擇`Email Subscriptions`。
* 設定電子郵件回覆時，成員只要回覆收到的電子郵件，即可有效張貼內容。

### 需求 {#requirements}

**設定電子郵件**

必須設定電子郵件，訂閱才能正常運作，成員才能透過電子郵件回覆。

有關設定電子郵件的說明，請參閱[配置電子郵件](email.md)。

**啟用訂閱與追蹤**

必須配置元件，以啟用以下訂閱&#x200B;*和*。 允許訂閱的功能包括[blog](blog-feature.md)、[forum](forum.md)和[QnA](working-with-qna.md)。

## 來自下列項目的訂閱 {#subscriptions-from-following}

![subscription-following](assets/subscription-following.png)

**Follow**&#x200B;按鈕提供了一種方法，可以將條目作為活動、訂閱和/或通知跟蹤。 每次選擇&#x200B;**Follow**&#x200B;按鈕時，都可以開啟或關閉選擇。

如果選擇了下列任何方法，則按鈕的文本將更改為&#x200B;**Following**。 為方便起見，可以選取`Unfollow All`來關閉所有方法。

只有當論壇、QnA或部落格配置為啟用電子郵件訂閱時，**Follow**&#x200B;按鈕才會包含`Email Subscriptions`選項。 此按鈕隨即出現：

* 在已啟用論壇的主功能頁面上，QnA或部落格將為該功能下的所有活動發送電子郵件。

* 對於特定條目（如論壇主題、QnA問題或部落格文章），當有特定條目的活動時將發送電子郵件。

## 透過電子郵件回覆 {#reply-by-email}

當電子郵件設定為[以通過電子郵件](email.md#configure-polling-importer)回復時，訂閱的成員將收到一封包含已發佈內容的電子郵件和指向線上內容的連結。

如果他們回覆電子郵件，他們在回覆中輸入的內容將顯示為線上內容。

![電子郵件回覆](assets/email-reply.png)

發佈回覆所需的時間由[輪詢匯入工具的更新間隔](email.md#configure-polling-importer)控制。

![QA](assets/qa.png)
