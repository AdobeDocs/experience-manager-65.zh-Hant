---
title: 社群通知
seo-title: 社群通知
description: AEM Communities有通知，顯示已登入社群成員感興趣的事件
seo-description: AEM Communities有通知，顯示已登入社群成員感興趣的事件
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---


# 社群通知{#communities-notifications}

## 概覽 {#overview}

AEM Communities提供通知區段，顯示已登入社群成員的興趣事件。

通知與[活動](/help/communities/essentials-activities.md)和[訂閱](/help/communities/subscriptions.md)類似，因為它們可能來自：

* 發佈內容的成員。
* 選擇跟隨另一個成員的成員。
* 選擇遵循特定主題、文章和其他內容主題的成員。
* 成員標籤（@提及）用戶生成的內容中的另一個社區成員。

通知與活動和訂閱的區別在於：

* 通知區段的連結永遠會出現在社群網站的標題中：

   * 活動要求[活動流函式](/help/communities/functions.md#activity-stream-function)包含在社區站點的結構中。
   * 訂閱需要[電子郵件](/help/communities/email.md)的設定。

* 通知的實作方式是透過可擴充且可插拔的通道：

   * 活動僅在Web上提供。
   * 訂閱僅能使用電子郵件。

從Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack)開始，可用的通知頻道包括：

* 使用`Notifications`連結訪問的Web通道。
* 電子郵件渠道，在正確設定電子郵件時可用。

未來的通道包括行動和案頭。

### 要求{#requirements}

**設定電子郵件**

必須設定電子郵件，才能讓電子郵件通路正常運作。

有關設定電子郵件的說明，請參閱[配置電子郵件](/help/communities/analytics.md)。

**啟用追蹤**

必須配置元件以啟用以下功能。 允許下列功能：[blog](/help/communities/blog-feature.md)、[論壇](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[日曆](/help/communities/calendar.md)、[filebrary](/help/communities/file-library.md)和[注釋](/help/communities/comments.md)。

**注意**:

* 在社區[站點模板](/help/communities/sites.md)和[組模板](/help/communities/tools-groups.md)中使用的元件已配置為遵循。

* 成員配置檔案已配置為允許其他成員跟隨。

## 來自{#notifications-from-following}的通知

![通知](assets/notifications.png)

**[!UICONTROL Follow]**&#x200B;按鈕提供了跟蹤條目作為活動、訂閱和／或通知的方法。 每次選擇&#x200B;**[!UICONTROL Follow]**&#x200B;按鈕時，都可以開啟或關閉選擇。 `Email Subscriptions`選項僅在配置時顯示。

如果選擇了任何下列方法，則按鈕的文本將更改為&#x200B;**[!UICONTROL Following]**。 為方便起見，您可以選取`Unfollow All`來關閉所有方法。

將顯示&#x200B;**[!UICONTROL Follow]**&#x200B;按鈕：

* 查看其他成員的配置檔案時。
* 在主要功能頁面上，例如論壇、QnA和部落格：

   * 遵循該一般功能的所有活動。

* 對於特定項目，例如論壇主題、QnA問題或部落格：

   * 跟蹤該特定條目的所有活動。

## 管理通知設定{#managing-notification-settings}

從「通知」頁面選擇「通知設定」連結，可讓每個成員管理接收通知的方式。

Web頻道一律啟用。

![通知14](assets/notifications1.png)

電子郵件渠道依賴於電子郵件](/help/communities/email.md)的正確[配置，提供與Web渠道相同的設定。

電子郵件頻道預設為關閉。

![通知2](assets/notifications2.png)

成員可以開啟它，但仍取決於正在配置的電子郵件。

![通知3](assets/notifications3.png)

## 查看通知{#viewing-notifications}

### Web通知{#web-notifications}

[精靈建立的社群網站](/help/communities/sites-console.md)現在包含橫幅上方網站標題列中`Notifications`功能的連結。 與訊息不同的是，會為每個社群網站建立通知，而訊息必須在網站建立程式中啟用。

訪問發佈站點時，選擇`Notifications`連結將顯示該成員的所有通知。

![通知4](assets/notifications4.png)

### 電子郵件通知{#email-notifications}

啟用電子郵件頻道後，會員會收到電子郵件，其中包含網路內容的連結。

![通知5](assets/notifications5.png)

## 自訂電子郵件通知{#customize-email-notifications}

組織可以透過[覆蓋](/help/communities/client-customize.md#overlays)**/libs/settings/community/templates/email/html**&#x200B;範本來自訂電子郵件通知。

例如，若要修改提及電子郵件通知（針對社群元件），請在您啟用&#x200B;**@mentions**&#x200B;支援的元件範本中，新增&#x200B;**if**&#x200B;條件，用於動詞&#x200B;**提及**。

若要修改部落格注釋中@提及的電子郵件通知範本，請將範本置於：**/libs/settings/community/templates/email/html/social.journal.components.hbs.comment.en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

