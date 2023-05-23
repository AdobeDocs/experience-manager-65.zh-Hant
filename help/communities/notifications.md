---
title: 社區通知
seo-title: Communities Notifications
description: AEM Communities有通知，顯示登錄社區成員感興趣的事件
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

# 社區通知 {#communities-notifications}

## 概觀 {#overview}

AEM Communities提供通知部分，顯示已登錄社區成員感興趣的事件。

通知與 [活動](/help/communities/essentials-activities.md) 和 [訂閱](/help/communities/subscriptions.md) 因為：

* 成員發佈內容。
* 選擇跟隨另一個成員的成員。
* 選擇遵循特定主題、文章和其他內容線程的成員。
* 成員標籤(@mention)用戶生成的內容中的另一個社區成員。

將通知與活動和訂閱區分開的是：

* 通知部分的連結始終出現在社區站點的標題中：

   * 活動要求 [活動流函式](/help/communities/functions.md#activity-stream-function) 被納入社區網站的結構。
   * 訂閱需要 [電子郵件配置](/help/communities/email.md)。

* 通知的實現是通過可擴展和可插拔的渠道：

   * 活動僅在Web上可用。
   * 訂閱僅使用電子郵件可用。

截至社區 [FP1](/help/communities/deploy-communities.md#latestfeaturepack)，可用的通知通道有：

* Web通道，使用 `Notifications` 的子菜單。
* 電子郵件通道，在正確配置電子郵件時可用。

未來的渠道是移動和台式機。

### 要求 {#requirements}

**配置電子郵件**

必須配置電子郵件，以使通知能夠正常運行。

有關設定電子郵件的說明，請參見 [配置電子郵件](/help/communities/analytics.md)。

**啟用跟蹤**

必須配置元件以啟用以下功能。 允許以下功能包括 [部落格](/help/communities/blog-feature.md)。 [論壇](/help/communities/forum.md)。 [QnA](/help/communities/working-with-qna.md)。 [日曆](/help/communities/calendar.md)。 [檔案庫](/help/communities/file-library.md), [評論](/help/communities/comments.md)。

**注意**:

* 社區中使用的元件 [站點模板](/help/communities/sites.md) 和 [組模板](/help/communities/tools-groups.md) 可能已配置為遵循。

* 成員配置檔案已配置為允許其他成員跟隨。

## 來自以下內容的通知 {#notifications-from-following}

![通知](assets/notifications.png)

的 **[!UICONTROL 關注]** 按鈕提供了將條目作為活動、訂閱和/或通知跟蹤的方法。 每次 **[!UICONTROL 關注]** 按鈕，可以開啟或關閉選定內容。 的 `Email Subscriptions` 僅當配置時才存在選擇。

如果選擇了以下任何方法，則按鈕的文本將更改為 **[!UICONTROL 跟蹤]**。 為方便起見，可以選擇 `Unfollow All` 關閉所有方法。

的 **[!UICONTROL 關注]** 按鈕：

* 查看其他成員的配置檔案時。
* 在主功能頁面上，如論壇、QnA和部落格：

   * 遵循該常規功能的所有活動。

* 對於特定條目，如論壇主題、QnA問題或部落格：

   * 跟蹤該特定條目的所有活動。

## 管理通知設定 {#managing-notification-settings}

通過從「通知」頁中選擇「通知設定」連結，每個成員都可以管理通知的接收方式。

Web通道始終處於啟用狀態。

![notifications14](assets/notifications1.png)

電子郵件通道，它依賴於適當 [電子郵件配置](/help/communities/email.md)，提供的設定與Web頻道的設定相同。

預設情況下，電子郵件通道處於關閉狀態。

![notifications2](assets/notifications2.png)

成員可能會開啟它，但仍取決於配置的電子郵件。

![notifications3](assets/notifications3.png)

## 查看通知 {#viewing-notifications}

### Web通知 {#web-notifications}

A [嚮導已建立社區網站](/help/communities/sites-console.md) 現在包括到 `Notifications` 標題欄上的「Fice」。 與消息不同，系統會為每個社區站點建立通知，而在站點建立過程中必須啟用消息。

訪問已發佈站點時，選擇 `Notifications` 連結將顯示成員的所有通知。

![notifications4](assets/notifications4.png)

### 電子郵件通知 {#email-notifications}

啟用電子郵件通道後，成員將接收包含指向Web上內容的連結的電子郵件。

![notifications5](assets/notifications5.png)

## 自定義電子郵件通知 {#customize-email-notifications}

組織可以通過 [疊](/help/communities/client-customize.md#overlays) 位於 **/libs/settings/community/templates/email/html**。

例如，要修改提及的電子郵件通知（針對社區元件），請添加 **如果** 動詞條件 **提及** 在為其啟用 **@mentions** 支援。

要修改部落格注釋中@mention的電子郵件通知模板，請將模板置於： **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
