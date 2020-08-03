---
title: 社群通知
seo-title: 社群通知
description: AEM Communities有通知，可顯示登入社群成員感興趣的事件
seo-description: AEM Communities有通知，可顯示登入社群成員感興趣的事件
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# 社群通知 {#communities-notifications}

## 概覽 {#overview}

AEM Communities提供通知區段，可顯示已登入社群成員感興趣的事件。

通知與活動 [和](/help/communities/essentials-activities.md)[訂閱類](/help/communities/subscriptions.md) 似，可能來自：

* 發佈內容的成員。
* 選擇跟隨另一個成員的成員。
* 選擇遵循特定主題、文章和其他內容主題的成員。
* 成員標籤（@提及）用戶生成的內容中的另一個社區成員。

通知與活動和訂閱的區別在於：

* 通知區段的連結永遠會出現在社群網站的標題中：

   * 活動需 [要將活動串流功能](/help/communities/functions.md#activity-stream-function) ，納入社群網站的結構中。
   * 訂閱需要 [設定電子郵件](/help/communities/email.md)。

* 通知的實作方式是透過可擴充且可插拔的通道：

   * 活動僅在Web上提供。
   * 訂閱僅能使用電子郵件。

自Communities [FP1起](/help/communities/deploy-communities.md#latestfeaturepack)，可用的通知渠道包括：

* 使用連結存取的網路頻 `Notifications` 道。
* 電子郵件渠道，在正確設定電子郵件時可用。

未來的通道包括行動和案頭。

### 需求 {#requirements}

**設定電子郵件**

必須設定電子郵件，才能讓電子郵件通路正常運作。

如需設定電子郵件的指示，請參閱 [設定電子郵件](/help/communities/analytics.md)。

**啟用追蹤**

必須配置元件以啟用以下功能。 允許以下功能：部落格 [、論壇](/help/communities/blog-feature.md)、 [QnQnPn](/help/communities/forum.md)、Filary [brary、elicary行事歷、](/help/communities/working-with-qna.md)[](/help/communities/calendar.md)[](/help/communities/file-library.md)[](/help/communities/comments.md)elicary注釋。

**注意**:

* 社群網站範本 [和群組範本](/help/communities/sites.md)[中使用的元件](/help/communities/tools-groups.md) ，可能已設定為遵循。

* 成員配置檔案已配置為允許其他成員跟隨。

## 來自下列的通知 {#notifications-from-following}

![通知](assets/notifications.png)

「跟 **[!UICONTROL 蹤]** 」按鈕提供了一種方法，可以跟蹤條目作為活動、訂閱和／或通知。 每次選取「 **[!UICONTROL 跟隨]** 」按鈕時，都可以開啟或關閉選取範圍。 只有 `Email Subscriptions` 在配置時，才會顯示選擇。

如果選取任何下列方法，按鈕的文字會變更為「下 **[!UICONTROL 列」]**。 為方便起見，您可以選取以 `Unfollow All` 關閉所有方法。

將出 **[!UICONTROL 現「]** Follow（跟蹤）」按鈕：

* 查看其他成員的配置檔案時。
* 在主要功能頁面上，例如論壇、QnA和部落格：

   * 遵循該一般功能的所有活動。

* 對於特定項目，例如論壇主題、QnA問題或部落格：

   * 跟蹤該特定條目的所有活動。

## 管理通知設定 {#managing-notification-settings}

從「通知」頁面選擇「通知設定」連結，可讓每個成員管理接收通知的方式。

Web頻道一律啟用。

![notifications14](assets/notifications1.png)

電子郵件渠道依賴於電子郵件的 [正確配置](/help/communities/email.md)，它提供與Web渠道相同的設定。

電子郵件頻道預設為關閉。

![notifications2](assets/notifications2.png)

成員可以開啟它，但仍取決於正在配置的電子郵件。

![notifications3](assets/notifications3.png)

## 檢視通知 {#viewing-notifications}

### 網頁通知 {#web-notifications}

建 [立社群網站的精靈](/help/communities/sites-console.md) ，現在會在橫幅上 `Notifications` 方的網站標題列中包含功能的連結。 與訊息不同的是，會為每個社群網站建立通知，而訊息必須在網站建立程式中啟用。

在造訪發佈網站時，選取連結 `Notifications` 會顯示成員的所有通知。

![notifications4](assets/notifications4.png)

### 電子郵件通知 {#email-notifications}

啟用電子郵件頻道後，會員會收到電子郵件，其中包含網路內容的連結。

![notifications5](assets/notifications5.png)

## 自訂電子郵件通知 {#customize-email-notifications}

組織可以自訂電子郵件通 [知](/help/communities/client-customize.md#overlays) ，將範本覆 **蓋在/libs/settings/community/templates/email/html中**。

例如，若要修改提及電子郵件通知（針對社群元件），請在您啟用 **@mentions支援的元件範本中，新增動詞提及的** if **條件****** 。

若要修改部落格注釋中@提及的電子郵件通知範本，請將範本置於： **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/tw**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

