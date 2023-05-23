---
title: 活動趨勢
seo-title: Activity Trends
description: 將社區活動清單元件添加到頁面
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

的 `Community Activity List` 元件提供了添加有關成員的帖子和視圖以及內容帖子和視圖的趨勢資訊的能力。

文檔描述：

* 添加 `Community Activity List` 元件 [社區站點](/help/communities/overview.md#community-sites)。

* 的配置設定 `Community Activity List` 元件。

### 需求 {#requirement}

資料 `Community Activity List` 僅在Adobe Analytics獲得社區站點的許可和配置時才可用。

請參閱 [社區功能的分析配置](/help/communities/analytics.md)。

### 將社區活動清單添加到頁面 {#adding-a-community-activity-list-to-a-page}

添加 `Community Activity List` 在作者模式下將元件定位到頁面

* `Communities / Community Activity List`

然後拖到頁面上。

如需必要資訊，請訪問 [社區元件基礎](/help/communities/basics.md)。

首次放置在社區站點的頁面上時，元件的顯示方式如下：

![社區活動](assets/community-activity.png)

### 配置社區活動清單  {#configuring-community-activity-list}

選取已放置的 `Community Activity List` 要訪問和選擇的元件 `Configure` 表徵圖。

![配置](assets/configure-new.png)

在 **注釋** 頁籤，指定上載檔案的注釋的顯示方式和顯示方式：

![屬性](assets/activity-list-properties.png)

* **類型**

   指定是顯示有關社區成員或用戶生成內容(UGC)的資料。

   從以下位置選擇：

   * `Members`
   * `Content`

   預設值為 `Members`。

* **顯示標題**

   顯示在資料上方的描述性標題，如 `Trending Content`。
預設為無標題。

* **顯示計數**

   要列出的項數。
預設值為10。

* **活動類型**

   選擇以下選項之一：

   * `Views`（頁面訪問）
   * `Posts`（建立UGC）
   * `Follows`
   * `Likes`

   預設為視圖。

* **時間段**

   選擇以下選項之一：

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   預設值為 `Total`。

* **內容路徑**

   提供將活動範圍限定到站點子集（如特定部落格）的能力。
預設值是整個社區站點。

* **成員人數彙總**

   取消選擇（關閉）時，只計算頂級員額。 例如，如果上下文是根頁（預設），則 `Activity Type` 共 `Posts` 不會顯示任何活動，因為無法將內容發佈到根頁面。 選中後，將包括所有子體頁面上的計數。
選中預設值。

### 包含4個元件的示例頁 {#example-page-with-components}

**頂級訪問者** 配置：類型=成員，活動類型=視圖

**最佳參與者** 配置：類型=成員，活動類型=帖子

**頂級內容** 配置：類型=內容，活動類型=視圖，

**趨勢內容** 配置：類型=內容，活動類型=帖子

![元件](assets/activity-list-components.png)
