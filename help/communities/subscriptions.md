---
title: 社群訂閱
seo-title: 社群訂閱
description: 社群成員透過電子郵件與其他成員互動
seo-description: 社群成員透過電子郵件與其他成員互動
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 社群訂閱 {#communities-subscriptions}

## 概覽 {#overview}

自Communities [FP1起](deploy-communities.md#latestfeaturepack)，社群成員可以使用稱為訂閱的功能，透過電子郵件與社群互動。

訂閱與通知類 [似](notifications.md) ，因為會員在關注部落格文章、論壇主題或QnA問題時可能會訂閱。

訂閱與通知的區別在於：

* 當追隨其他成員時，成員不得訂閱
* 成員唯一要執行的操作是選擇以 `Email Subscriptions` 下操作
* 當設定電子郵件回覆時，會員只要回覆收到的電子郵件，就可以有效地張貼內容

### 需求 {#requirements}

**設定電子郵件**

必須設定電子郵件，才能讓訂閱發揮功能，讓成員以電子郵件回覆。

如需設定電子郵件的指示，請參閱 [設定電子郵件](email.md)。

**啟用訂閱並追蹤**

必須設定元件，才能啟用訂閱 *和* 遵循。 允許訂閱的功能 [包括部落格](blog-feature.md)、 [論壇](forum.md)[和](working-with-qna.md)QnA。

## 下列訂閱 {#subscriptions-from-following}

![chlimage_1-5](assets/chlimage_1-5.png)

「跟 **蹤** 」按鈕提供了一種方法，可以跟蹤條目作為活動、訂閱和／或通知。 每次選取「 **跟隨** 」按鈕時，都可以開啟或關閉選取範圍。

如果選取任何下列方法，按鈕的文字會變更為「下 **列」**。 為方便起見，您可以選取以 `Unfollow All` 關閉所有方法。

只有在 **將論壇、QnA或部**`Email Subscriptions` 落格設定為啟用電子郵件訂閱時，「關注」按鈕才會包含此選項。 此按鈕將會出現

* 在啟用論壇、QnA或部落格的主要功能頁面上

   * 會針對該功能下的所有活動傳送電子郵件

* 針對特定項目，例如論壇主題、QnA問題或部落格文章

   * 當該特定項目有活動時，將會傳送電子郵件

## 電子郵件回覆 {#reply-by-email}

當電子郵件設 [定為以電子郵件回覆](email.md#configure-polling-importer)，訂閱的會員將會收到電子郵件，內含已張貼的內容和線上內容的連結。

如果回覆電子郵件，則回覆中輸入的內容會顯示為線上內容。

![chlimage_1-6](assets/chlimage_1-6.png)

回覆張貼的時間量由輪詢匯入工具的更 [新間隔控制](email.md#configure-polling-importer)。

![chlimage_1-7](assets/chlimage_1-7.png)

