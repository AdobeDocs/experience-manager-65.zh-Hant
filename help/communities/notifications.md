---
title: Communities通知
seo-title: Communities通知
description: AEM Communities會通知顯示已登入社群成員感興趣的事件
seo-description: AEM Communities會通知顯示已登入社群成員感興趣的事件
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
source-wordcount: '625'
ht-degree: 1%

---

# Communities通知 {#communities-notifications}

## 概覽 {#overview}

AEM Communities提供通知區段，顯示已登入社群成員感興趣的事件。

通知類似於[activities](/help/communities/essentials-activities.md)和[subscriptions](/help/communities/subscriptions.md)，因為它們可能源自：

* 成員發佈內容。
* 選擇跟隨另一成員的成員。
* 成員選擇遵循特定主題、文章和其他內容主題。
* 成員標籤(@mention)用戶生成內容中的另一個社區成員。

活動和訂閱的通知的區別為：

* 通知區段的連結一律會顯示在社群網站的標題中：

   * 活動要求將[活動資料流函式](/help/communities/functions.md#activity-stream-function)包含在社群網站的結構中。
   * 訂閱需要[電子郵件](/help/communities/email.md)的設定。

* 通知的實施是通過可擴展和可插拔的通道：

   * 活動僅可在Web上使用。
   * 訂閱僅限使用電子郵件。

自Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack)起，可用的通知通道為：

* 使用`Notifications`連結存取的Web通道。
* 電子郵件通道，正確設定電子郵件時可用。

未來的通道包括行動裝置和案頭裝置。

### 需求 {#requirements}

**設定電子郵件**

必須設定電子郵件，電子郵件通道才能運作通知。

有關設定電子郵件的說明，請參閱[配置電子郵件](/help/communities/analytics.md)。

**啟用跟蹤**

必須配置元件以啟用以下功能。 允許下列功能：[blog](/help/communities/blog-feature.md)、[forum](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[日曆](/help/communities/calendar.md)、[filelibrary](/help/communities/file-library.md)和[注釋](/help/communities/comments.md)。

**注意**:

* 在社區[站點模板](/help/communities/sites.md)和[組模板](/help/communities/tools-groups.md)中使用的元件可能已配置為遵循。

* 成員配置檔案已配置為允許其他成員遵循。

## 來自下列的通知 {#notifications-from-following}

![通知](assets/notifications.png)

**[!UICONTROL Follow]**&#x200B;按鈕提供了一種方法，可以將條目作為活動、訂閱和/或通知跟蹤。 每次選擇&#x200B;**[!UICONTROL Follow]**&#x200B;按鈕時，都可以開啟或關閉選擇。 `Email Subscriptions`選項僅在配置時存在。

如果選擇了下列任何方法，則按鈕的文本將更改為&#x200B;**[!UICONTROL Following]**。 為方便起見，可以選取`Unfollow All`來關閉所有方法。

將顯示&#x200B;**[!UICONTROL Follow]**&#x200B;按鈕：

* 查看其他成員的配置檔案時。
* 在主功能頁面（如論壇、QnA和部落格）上：

   * 遵循該一般功能的所有活動。

* 對於特定條目，如論壇主題、QnA問題或部落格文章：

   * 遵循該特定項目的所有活動。

## 管理通知設定 {#managing-notification-settings}

通過從「通知」頁中選擇「通知設定」連結，每個成員都可以管理接收通知的方式。

一律會啟用Web通道。

![notifications14](assets/notifications1.png)

電子郵件通道依賴於電子郵件](/help/communities/email.md)的適當[配置，提供與Web通道相同的設定。

電子郵件通道預設為關閉。

![notifications2](assets/notifications2.png)

成員可以開啟它，但仍取決於所配置的電子郵件。

![notifications3](assets/notifications3.png)

## 檢視通知 {#viewing-notifications}

### Web通知 {#web-notifications}

建立的[精靈社群網站](/help/communities/sites-console.md)現在包含橫幅上方網站標題列中`Notifications`功能的連結。 與訊息不同，會為每個社群網站建立通知，而訊息必須在網站建立程式期間啟用。

訪問已發佈的站點時，選擇`Notifications`連結將顯示該成員的所有通知。

![通知4](assets/notifications4.png)

### 電子郵件通知 {#email-notifications}

啟用電子郵件通道時，成員會收到包含指向Web上內容的連結的電子郵件。

![通知5](assets/notifications5.png)

## 自訂電子郵件通知 {#customize-email-notifications}

組織可以透過[覆蓋](/help/communities/client-customize.md#overlays)範本來自訂電子郵件通知，位於&#x200B;**/libs/settings/community/templates/email/html**。

例如，若要修改提及電子郵件通知（針對社群元件），請在您啟用&#x200B;**@mentions**&#x200B;支援的元件範本中，新增動詞&#x200B;**提及**&#x200B;的&#x200B;**條件。**

若要修改部落格註解中@mention的電子郵件通知範本，請放置於：**/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
