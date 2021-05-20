---
title: 活動趨勢
seo-title: 活動趨勢
description: 新增社群活動清單元件至頁面
seo-description: 新增社群活動清單元件至頁面
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
source-wordcount: '357'
ht-degree: 4%

---

# 活動趨勢{#activity-trends}

## 簡介 {#introduction}

`Community Activity List`元件可新增關於依成員及貼文和內容檢視之貼文和檢視的趨勢資訊。

文檔描述：

* 將`Community Activity List`元件新增至[社群網站](/help/communities/overview.md#community-sites)。

* `Community Activity List`元件的組態設定。

### 需求 {#requirement}

`Community Activity List`的資料僅在為社群網站授權並配置Adobe Analytics時可用。

請參閱[Analytics For Communities](/help/communities/analytics.md)。

### 將社群活動清單新增至頁面{#adding-a-community-activity-list-to-a-page}

若要在製作模式中將`Community Activity List`元件新增至頁面，請找出元件

* `Communities / Community Activity List`

並將其拖曳到頁面上。

如需必要資訊，請造訪[Communities Components Basics](/help/communities/basics.md)。

首次放置在社群網站的頁面時，元件的顯示方式如下：

![社群活動](assets/community-activity.png)

### 配置社區活動清單{#configuring-community-activity-list}

選取要存取的放置`Community Activity List`元件，並選取開啟編輯對話方塊的`Configure`圖示。

![設定](assets/configure-new.png)

在&#x200B;**Comments**&#x200B;標籤下，指定上傳檔案的備注是否及顯示方式：

![屬性](assets/activity-list-properties.png)

* **類型**

   指定要顯示社群成員或使用者產生內容(UGC)的相關資料。

   選擇：

   * `Members`
   * `Content`

   預設值為`Members`。

* **顯示標題**

   要在資料上方顯示的描述性標題，例如`Trending Content`。
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

   預設值為`Total`。

* **內容路徑**

   提供將活動範圍限定為網站子集（如特定部落格）的能力。
預設值是整個社群網站。

* **成員人數彙總**

   取消選取（關閉）時，只會計算最上層貼文。 例如，如果內容是根頁面（預設值），則`Posts`的`Activity Type`將不會顯示任何活動，因為無法將內容張貼至根頁面。 若勾選此選項，則會包含所有子系頁面上的計數。
已勾選預設值。

### 4個元件的範例頁面{#example-page-with-components}

**頂** 級Visitorsconfig:類型=成員，活動類型=檢視

**排名在** 前的貢獻者設定：類型=成員，活動類型=貼文

**排名在** 前的Contentconfig:類型=內容，活動類型=檢視，

**趨勢** 內容設定：類型=內容，活動類型=貼文

![元件](assets/activity-list-components.png)
