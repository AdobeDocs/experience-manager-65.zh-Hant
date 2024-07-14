---
title: 社群通知
description: AEM Communities有通知可顯示登入社群成員感興趣的事件
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# 社群通知 {#communities-notifications}

## 概觀 {#overview}

AEM Communities提供通知區段，顯示已登入社群成員感興趣的事件。

通知類似於[活動](/help/communities/essentials-activities.md)和[訂閱](/help/communities/subscriptions.md)，因為它們可能來自：

* 成員張貼內容。
* 選擇跟隨其他成員的成員。
* 成員選擇遵循特定主題、文章和其他內容對話串。
* 成員標籤(@mention)使用者產生的內容中的另一個社群成員。

通知與活動和訂閱的區別在於：

* 通知區段的連結一律會顯示在社群網站的標題中：

   * 活動需要將[活動資料流函式](/help/communities/functions.md#activity-stream-function)包含在社群網站的結構中。
   * 訂閱需要[設定電子郵件](/help/communities/email.md)。

* 通知的實作透過可擴充和可插拔的管道進行：

   * 活動只能在Web上使用。
   * 訂閱只能透過電子郵件取得。

截至Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack)，可用的通知通道為：

* 使用`Notifications`連結存取的Web管道。
* 電子郵件頻道，在正確設定電子郵件時可用。

未來的頻道包括行動裝置和桌上型電腦。

### 要求 {#requirements}

**設定電子郵件**

必須設定電子郵件，通知的電子郵件通道才能正常運作。

如需設定電子郵件的說明，請參閱[設定電子郵件](/help/communities/analytics.md)。

**啟用Follow**

元件必須設定為啟用下列專案。 允許追蹤的功能包括[部落格](/help/communities/blog-feature.md)、[論壇](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[行事曆](/help/communities/calendar.md)、[檔案庫](/help/communities/file-library.md)和[註解](/help/communities/comments.md)。

**附註**：

* 社群[網站範本](/help/communities/sites.md)和[群組範本](/help/communities/tools-groups.md)中使用的元件可能已設定為要遵循。

* 成員設定檔已設定為允許其他成員跟隨。

## 來自以下專案的通知 {#notifications-from-following}

![通知](assets/notifications.png)

**[!UICONTROL 追隨]**&#x200B;按鈕提供將專案作為活動、訂閱和/或通知進行追蹤的方法。 每次選取&#x200B;**[!UICONTROL 追隨]**&#x200B;按鈕時，都可以開啟或關閉選取專案。 `Email Subscriptions`選取專案只有在設定後才出現。

如果選取任何追蹤方法，按鈕的文字會變更為&#x200B;**[!UICONTROL 追蹤]**。 為方便起見，可以選取`Unfollow All`以關閉所有方法。

**[!UICONTROL 追隨]**&#x200B;按鈕將會出現：

* 檢視其他成員的設定檔時。
* 在主要功能頁面（例如論壇、QnA和部落格）上：

   * 遵循該一般功能的所有活動。

* 針對特定專案，例如論壇主題、QnA問題或部落格：

   * 追蹤該特定專案的所有活動。

## 管理通知設定 {#managing-notification-settings}

從「通知」頁面選取「通知設定」連結，即可讓每個成員管理接收通知的方式。

Web Channel一律啟用。

![通知14](assets/notifications1.png)

電子郵件通道依賴電子郵件](/help/communities/email.md)的正確[設定，提供與網頁通道相同的設定。

電子郵件通道預設為關閉。

![通知2](assets/notifications2.png)

可由成員開啟，但仍取決於設定的電子郵件。

![通知3](assets/notifications3.png)

## 檢視通知 {#viewing-notifications}

### Web通知 {#web-notifications}

[精靈建立的社群網站](/help/communities/sites-console.md)現在在橫幅上方的網站標題列中包含指向`Notifications`功能的連結。 與訊息不同，會為每個社群網站建立通知，而訊息必須在網站建立過程中啟用。

造訪已發佈的網站時，選取`Notifications`連結將會顯示該成員的所有通知。

![通知4](assets/notifications4.png)

### 電子郵件通知 {#email-notifications}

啟用電子郵件通道時，成員會收到包含網頁內容連結的電子郵件。

![通知5](assets/notifications5.png)

## 自訂電子郵件通知 {#customize-email-notifications}

組織可以透過[覆蓋](/help/communities/client-customize.md#overlays)位於&#x200B;**/libs/settings/community/templates/email/html**&#x200B;的範本來自訂電子郵件通知。

例如，若要修改提及電子郵件通知（適用於社群元件），請在啟用&#x200B;**@mentions**&#x200B;支援之元件的範本中，新增動詞&#x200B;**提及**&#x200B;的&#x200B;**if**&#x200B;條件。

若要修改部落格評論中@mention的電子郵件通知範本，請將現成範本放置於： **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
