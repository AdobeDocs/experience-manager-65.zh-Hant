---
title: 活動趨勢
seo-title: Activity Trends
description: 新增社群活動清單元件至頁面
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%

---

# 活動趨勢 {#activity-trends}

## 簡介 {#introduction}

此 `Community Activity List` 「元件」可新增與貼文和檢視相關的趨勢資訊，此資訊可依成員以及貼文和內容檢視。

文檔描述：

* 新增 `Community Activity List` 元件 [社群網站](/help/communities/overview.md#community-sites).

* 的組態設定 `Community Activity List` 元件。

### 需求 {#requirement}

資料 `Community Activity List` 只有在Adobe Analytics已授權並已針對社群網站進行設定時，才可使用。

請參閱 [Communities功能的Analytics設定](/help/communities/analytics.md).

### 將社群活動清單新增至頁面 {#adding-a-community-activity-list-to-a-page}

新增 `Community Activity List` 在製作模式中，找到元件至頁面

* `Communities / Community Activity List`

並將其拖曳到頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

首次放置在社群網站的頁面時，元件的顯示方式如下：

![社群活動](assets/community-activity.png)

### 配置社區活動清單  {#configuring-community-activity-list}

選取已放置的 `Community Activity List` 要存取的元件並選取 `Configure` 表徵圖，開啟「編輯」對話框。

![設定](assets/configure-new.png)

在 **註解** 索引標籤，指定上傳檔案的註解是否及顯示方式：

![屬性](assets/activity-list-properties.png)

* **類型**

   指定要顯示社群成員或使用者產生內容(UGC)的相關資料。

   選擇：

   * `Members`
   * `Content`

   預設為 `Members`.

* **顯示標題**

   要在資料上方顯示的描述性標題，例如 `Trending Content`.
預設為無標題。

* **顯示計數**

   要列出的項目數。
預設為10。

* **活動類型**

   選擇以下選項之一：

   * `Views`（頁面瀏覽次數）
   * `Posts`（建立UGC）
   * `Follows`
   * `Likes`

   預設為檢視。

* **時間段**

   選擇以下選項之一：

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   預設為 `Total`.

* **內容路徑**

   提供將活動範圍限定為網站子集（如特定部落格）的能力。
預設值是整個社群網站。

* **成員人數彙總**

   取消選取（關閉）時，只會計算最上層貼文。 例如，如果內容是根頁面（預設值），則 `Activity Type` of `Posts` 不會顯示任何活動，因為無法將內容張貼至根頁面。 若勾選此選項，則會包含所有子系頁面上的計數。
已勾選預設值。

### 包含4個元件的範例頁面 {#example-page-with-components}

**排名在前的訪客** 設定：類型=成員，活動類型=檢視

**排名最前的貢獻者** 設定：類型=成員，活動類型=貼文

**排名在前的內容** 設定：類型=內容，活動類型=檢視，

**趨勢內容** 設定：類型=內容，活動類型=貼文

![元件](assets/activity-list-components.png)
