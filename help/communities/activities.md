---
title: 活動流功能
seo-title: Activity Streams Feature
description: 已簽署社區成員的活動
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

# 活動流功能 {#activity-streams-feature}

## 簡介 {#introduction}

已登錄社區成員的活動，例如發佈到論壇或部落格，被收集到流中，該流可以通過配置以各種方式被過濾和顯示 `Activity Streams` 元件。

當社區成員跟蹤感興趣的帖子或跟蹤其他社區成員的活動時，跟蹤功能會添加另一個活動視圖。

文檔描述：

* 將活動流元件添加到站AEM點
* 活動流元件的配置設定

### 將活動流添加到頁 {#adding-activity-streams-to-a-page}

如果希望添加 `Activity Streams` 在作者模式下對頁面的元件，使用元件瀏覽器查找

* `Communities / Activity Streams`

並將其拖到活動流應出現的頁面上。

如需必要資訊，請訪問 [社區元件基礎](/help/communities/basics.md)。

當 [所需的客戶端庫](/help/communities/essentials-activities.md#essentials-for-client-side) 包括，這是 `Activity Streams` 元件將出現：

![活動流](assets/activity-component.png)

### 配置活動流 {#configuring-activity-streams}

選取已放置的 `Activity Streams` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置](assets/configure-new.png)

在 **用戶活動** 頁籤，指定要顯示的活動：

![用戶活動](assets/user-activities.png)

* **活動最大數量**

   要顯示的活動數

* **資料流資源路徑**

   留空以預設到社區站點或社區組。 流資源路徑標識活動源。 預設值為空。

* **顯示使用者活動視圖**

   如果選中，則活動頁面將包含一個頁籤，該頁籤根據當前成員在社區中生成的活動篩選活動。 選中預設值。

* **顯示所有活動視圖**

   如果選中，則活動頁面將包含一個頁籤，其中包含當前成員有權訪問的社區中生成的所有活動。 選中預設值。

* **顯示以下檢視**

   如果選中，則活動頁面將包含一個頁籤，該頁籤根據當前成員正在跟蹤的活動篩選活動。 選中預設值。

### 以下視圖 {#following-view}

必須配置元件以啟用以下功能。 允許以下功能包括 [部落格](/help/communities/blog-feature.md)。 [論壇](/help/communities/forum.md)。 [QnA](/help/communities/working-with-qna.md)。 [日曆](/help/communities/calendar.md)。 [檔案庫](/help/communities/file-library.md), [評論](/help/communities/comments.md)。

![後視圖](assets/following-activities.png)

的 **關注** 按鈕可以將條目作為活動跟蹤， [通知](/help/communities/notifications.md)或 [訂閱](/help/communities/subscriptions.md)。 每次 **關注** 按鈕，可以開啟或關閉選定內容。 的 `Email Subscriptions` 僅當配置時才存在選擇。

如果選擇了以下任何方法，則按鈕的文本將更改為 **跟蹤**。 為方便起見，可以選擇 `Unfollow All` 關閉所有方法。

的 **關注** 按鈕：

* 查看其他成員的配置檔案時。
* 在主功能頁面上，如論壇、QnA和部落格。

   * 遵循該常規功能的所有活動。

* 有關特定條目，如論壇主題、QnA問題或部落格。

   * 跟蹤該特定條目的所有活動。

### 其他資訊 {#additional-information}

有關 [活動流軟體包](/help/communities/essentials-activities.md) 頁面。
