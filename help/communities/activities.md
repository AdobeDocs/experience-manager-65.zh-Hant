---
title: 活動資料流功能
seo-title: 活動資料流功能
description: 已登錄社區成員的活動
seo-description: 已登錄社區成員的活動
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---

# 活動資料流功能{#activity-streams-feature}

## 簡介 {#introduction}

已登錄社區成員的活動，例如發佈到論壇或部落格，被收集到流中，該流可以通過`Activity Streams`元件的配置以各種方式被過濾和顯示。

當社群成員關注感興趣的帖子或關注其他社區成員的活動時，跟隨的能力將添加另一個活動視圖。

文檔描述：

* 新增活動資料流元件至AEM網站
* 活動資料流元件的組態設定

### 新增活動資料流至頁面{#adding-activity-streams-to-a-page}

如果想在製作模式中將`Activity Streams`元件新增至頁面，請使用元件瀏覽器來找出

* `Communities / Activity Streams`

並將其拖曳至應該顯示活動資料流的頁面上。

如需必要資訊，請造訪[Communities Components Basics](/help/communities/basics.md)。

包含[必要的用戶端程式庫](/help/communities/essentials-activities.md#essentials-for-client-side)時，以下是`Activity Streams`元件的顯示方式：

![活動資料流](assets/activity-component.png)

### 配置活動流{#configuring-activity-streams}

選取要存取的放置`Activity Streams`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![設定](assets/configure-new.png)

在&#x200B;**使用者活動**&#x200B;標籤下，指定要顯示的活動：

![使用者活動](assets/user-activities.png)

* **活動最大數量**

   要顯示的活動數

* **資料流資源路徑**

   保留為空白，以預設為社群網站或社群群組。 資料流資源路徑標識活動源。 預設為空白。

* **顯示使用者活動視圖**

   如果勾選此選項，活動頁面將包含一個索引標籤，該索引標籤會根據目前成員在社群內產生的活動來篩選活動。 已勾選預設值。

* **顯示所有活動視圖**

   如果勾選此選項，活動頁面將包含索引標籤，該索引標籤包含在目前成員有權存取的社群內產生的所有活動。 已勾選預設值。

* **顯示以下檢視**

   如果選中，則活動頁將包含一個頁簽，該頁簽將根據當前成員正在跟蹤的活動來篩選活動。 已勾選預設值。

### 正在查看{#following-view}

必須配置元件以啟用以下功能。 允許下列功能：[blog](/help/communities/blog-feature.md)、[forum](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[日曆](/help/communities/calendar.md)、[filelibrary](/help/communities/file-library.md)和[注釋](/help/communities/comments.md)。

![後視](assets/following-activities.png)

**Follow**&#x200B;按鈕提供了一種方法，可以將條目作為活動跟蹤，[notifications](/help/communities/notifications.md)或[訂閱](/help/communities/subscriptions.md)。 每次選擇&#x200B;**Follow**&#x200B;按鈕時，都可以開啟或關閉選擇。 `Email Subscriptions`選項僅在配置時存在。

如果選擇了下列任何方法，則按鈕的文本將更改為&#x200B;**Following**。 為方便起見，可以選取`Unfollow All`來關閉所有方法。

將顯示&#x200B;**Follow**&#x200B;按鈕：

* 查看其他成員的配置檔案時。
* 在主功能頁面上，如論壇、QnA和部落格。

   * 遵循該一般功能的所有活動。

* 用於特定條目，如論壇主題、QnA問題或部落格文章。

   * 遵循該特定項目的所有活動。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[Activity Streams Essentials](/help/communities/essentials-activities.md)頁面。
