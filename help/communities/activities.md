---
title: 活動資料流功能
seo-title: Activity Streams Feature
description: 已登錄社區成員的活動
seo-description: Activities of a signed-in community member
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
source-wordcount: '455'
ht-degree: 4%

---

# 活動資料流功能 {#activity-streams-feature}

## 簡介 {#introduction}

已登錄社區成員的活動，例如發佈到論壇或部落格，被收集到流中，該流可以通過配置以各種方式被過濾和顯示 `Activity Streams` 元件。

當社群成員關注感興趣的帖子或關注其他社區成員的活動時，跟隨的能力將添加另一個活動視圖。

文檔描述：

* 新增活動資料流元件至AEM網站
* 活動資料流元件的組態設定

### 新增活動資料流至頁面 {#adding-activity-streams-to-a-page}

如果需要新增 `Activity Streams` 在製作模式中，使用元件瀏覽器來尋找

* `Communities / Activity Streams`

並將其拖曳至應該顯示活動資料流的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的用戶端程式庫](/help/communities/essentials-activities.md#essentials-for-client-side) 包含在內，以下為方式 `Activity Streams` 元件隨即顯示：

![活動資料流](assets/activity-component.png)

### 設定活動資料流 {#configuring-activity-streams}

選取已放置的 `Activity Streams` 要存取的元件並選取 `Configure` 表徵圖，開啟「編輯」對話框。

![設定](assets/configure-new.png)

在 **使用者活動** 索引標籤，指定要顯示的活動：

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

### 後續檢視 {#following-view}

必須配置元件以啟用以下功能。 允許下列項目的功能 [部落格](/help/communities/blog-feature.md), [論壇](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [日曆](/help/communities/calendar.md), [檔案庫](/help/communities/file-library.md)，和 [評論](/help/communities/comments.md).

![後視](assets/following-activities.png)

此 **追隨** 按鈕提供將條目作為活動跟蹤的方法， [通知](/help/communities/notifications.md)，或 [訂閱](/help/communities/subscriptions.md). 每次 **追隨** 按鈕，則可以開啟或關閉選取項。 此 `Email Subscriptions` 只有在配置後才會顯示選擇。

如果選取下列任何方法，按鈕的文字會變更為 **追隨**. 為方便起見，您可以選擇 `Unfollow All` 切換所有方法。

此 **追隨** 按鈕隨即出現：

* 查看其他成員的配置檔案時。
* 在主功能頁面上，如論壇、QnA和部落格。

   * 遵循該一般功能的所有活動。

* 用於特定條目，如論壇主題、QnA問題或部落格文章。

   * 遵循該特定項目的所有活動。

### 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [活動資料流基本資訊](/help/communities/essentials-activities.md) 頁面。
