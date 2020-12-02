---
title: 活動趨勢
seo-title: 活動趨勢
description: 將社群活動清單元件添加到頁面
seo-description: 將社群活動清單元件添加到頁面
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 4%

---


# 活動趨勢{#activity-trends}

## 簡介 {#introduction}

`Community Activity List`元件可新增成員的貼文和檢視、貼文和內容檢視等趨勢資訊。

本檔案說明：

* 將`Community Activity List`元件添加到[社區站點](/help/communities/overview.md#community-sites)。

* `Community Activity List`元件的配置設定。

### 需求 {#requirement}

`Community Activity List`的資料僅在Adobe Analytics取得社群網站的授權並設定時才可用。

請參閱[社群功能分析設定](/help/communities/analytics.md)。

### 將社群活動清單添加到頁面{#adding-a-community-activity-list-to-a-page}

若要在作者模式下將`Community Activity List`元件新增至頁面，請找出該元件

* `Communities / Community Activity List`

並將它拖曳至頁面上的位置。

如需必要資訊，請造訪[Communities Components Basics](/help/communities/basics.md)。

首次放置在社群網站頁面時，元件的顯示方式如下：

![社群活動](assets/community-activity.png)

### 配置社區活動清單{#configuring-community-activity-list}

選擇要訪問的已放置的`Community Activity List`元件，並選擇`Configure`表徵圖以開啟編輯對話框。

![配置](assets/configure-new.png)

在&#x200B;**Comments**&#x200B;標籤下，指定上傳檔案的注釋是否及顯示方式：

![屬性](assets/activity-list-properties.png)

* **類型**

   指定要顯示社群成員或使用者產生內容(UGC)的相關資料。

   從中選擇：

   * `Members`
   * `Content`

   預設值為`Members`。

* **顯示標題**

   要在資料上方顯示的描述性標題，例如`Trending Content`。
預設為無標題。

* **顯示計數**

   要列出的項目數。
預設值為10。

* **活動類型**

   選擇以下選項之一：

   * `Views`（頁面瀏覽）
   * `Posts`（建立UGC）
   * `Follows`
   * `Likes`

   預設為「檢視」。

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

   提供將活動範圍限定在網站子集的能力，例如特定部落格。
預設為整個社群網站。

* **成員人數彙總**

   取消選取（關閉）時，只會計入頂層貼文。 例如，如果內容是根頁面（預設值），則`Posts`的`Activity Type`將不會顯示任何活動，因為無法將內容張貼至根頁面。 勾選後，會包含所有子系頁面的計數。
已勾選預設值。

### 包含4個元件{#example-page-with-components}的示例頁

**頂級** 訪客組態：類型=成員，活動類型=視圖

**熱門貢** 獻者組態：類型=成員，活動類型=貼文

**主要** 內容組態：類型=內容，活動類型=檢視，

**趨勢** Contentconfig:類型=內容，活動類型=貼文

![元件](assets/activity-list-components.png)

