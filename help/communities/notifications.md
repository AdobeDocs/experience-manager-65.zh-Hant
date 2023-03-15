---
title: Communities通知
seo-title: Communities Notifications
description: AEM Communities會通知顯示已登入社群成員感興趣的事件
seo-description: AEM Communities has notifications that display events of interest to the signed-in community member
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 1%

---

# Communities通知 {#communities-notifications}

## 概觀 {#overview}

AEM Communities提供通知區段，顯示已登入社群成員感興趣的事件。

通知類似 [活動](/help/communities/essentials-activities.md) 和 [訂閱](/help/communities/subscriptions.md) 因此：

* 成員發佈內容。
* 選擇跟隨另一成員的成員。
* 成員選擇遵循特定主題、文章和其他內容主題。
* 成員標籤(@mention)用戶生成內容中的另一個社區成員。

活動和訂閱的通知的區別為：

* 通知區段的連結一律會顯示在社群網站的標題中：

   * 活動需要 [活動流函式](/help/communities/functions.md#activity-stream-function) 包含在社群網站的結構中。
   * 訂閱需要 [電子郵件設定](/help/communities/email.md).

* 通知的實施是通過可擴展和可插拔的通道：

   * 活動僅可在Web上使用。
   * 訂閱僅限使用電子郵件。

As of Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack)，可用的通知通道包括：

* 網路通道，使用 `Notifications` 連結。
* 電子郵件通道，正確設定電子郵件時可用。

未來的通道包括行動裝置和案頭裝置。

### 要求 {#requirements}

**設定電子郵件**

必須設定電子郵件，電子郵件通道才能運作通知。

如需設定電子郵件的指示，請參閱 [設定電子郵件](/help/communities/analytics.md).

**啟用跟蹤**

必須配置元件以啟用以下功能。 允許下列項目的功能 [部落格](/help/communities/blog-feature.md), [論壇](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [日曆](/help/communities/calendar.md), [檔案庫](/help/communities/file-library.md)，和 [評論](/help/communities/comments.md).

**注意**:

* 社群中使用的元件 [網站範本](/help/communities/sites.md) 和 [群組範本](/help/communities/tools-groups.md) 可能已設定為遵循。

* 成員配置檔案已配置為允許其他成員遵循。

## 來自下列的通知 {#notifications-from-following}

![通知](assets/notifications.png)

此 **[!UICONTROL 追隨]** 按鈕提供可在活動、訂閱和/或通知後跟隨項目的方法。 每次 **[!UICONTROL 追隨]** 按鈕，則可以開啟或關閉選取項。 此 `Email Subscriptions` 只有在配置後才會顯示選擇。

如果選取下列任何方法，按鈕的文字會變更為 **[!UICONTROL 追隨]**. 為方便起見，您可以選擇 `Unfollow All` 切換所有方法。

此 **[!UICONTROL 追隨]** 按鈕隨即出現：

* 查看其他成員的配置檔案時。
* 在主功能頁面（如論壇、QnA和部落格）上：

   * 遵循該一般功能的所有活動。

* 對於特定條目，如論壇主題、QnA問題或部落格文章：

   * 遵循該特定項目的所有活動。

## 管理通知設定 {#managing-notification-settings}

通過從「通知」頁中選擇「通知設定」連結，每個成員都可以管理接收通知的方式。

一律會啟用Web通道。

![notifications14](assets/notifications1.png)

依賴適當 [電子郵件設定](/help/communities/email.md)，提供與網頁頻道相同的設定。

電子郵件通道預設為關閉。

![notifications2](assets/notifications2.png)

成員可以開啟它，但仍取決於所配置的電子郵件。

![notifications3](assets/notifications3.png)

## 檢視通知 {#viewing-notifications}

### Web通知 {#web-notifications}

A [嚮導建立的社群站點](/help/communities/sites-console.md) 現在包含連結至 `Notifications` 功能。 與訊息不同，會為每個社群網站建立通知，而訊息必須在網站建立程式期間啟用。

造訪已發佈的網站時，請選取 `Notifications` 連結將顯示成員的所有通知。

![notifications4](assets/notifications4.png)

### 電子郵件通知 {#email-notifications}

啟用電子郵件通道時，成員會收到包含指向Web上內容的連結的電子郵件。

![notifications5](assets/notifications5.png)

## 自訂電子郵件通知 {#customize-email-notifications}

組織可依 [覆蓋](/help/communities/client-customize.md#overlays) 範本位於 **/libs/settings/community/templates/email/html**.

例如，若要修改提及電子郵件通知（針對Communities元件），請新增 **if** 動詞條件 **提及** 在元件的範本中啟用 **@mentions** 支援。

若要修改部落格註解中@mention的電子郵件通知範本，請放置於： **/libs/settings/community/templates/email/html/social.journal**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
