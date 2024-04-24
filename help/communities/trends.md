---
title: 活動趨勢
description: 將社群活動清單元件新增至頁面
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 活動趨勢 {#activity-trends}

## 簡介 {#introduction}

此 `Community Activity List` 元件可讓您新增成員貼文和檢視的趨勢資訊，以及內容的貼文和檢視。

本檔案說明：

* 新增 `Community Activity List` 元件至 [社群網站](/help/communities/overview.md#community-sites).

* 的組態設定 `Community Activity List` 元件。

### 需求 {#requirement}

以下專案的資料 `Community Activity List` 只有當Adobe Analytics獲得授權並設定用於社群網站時，才可使用。

另請參閱 [社群功能的Analytics設定](/help/communities/analytics.md).

### 將社群活動清單新增至頁面 {#adding-a-community-activity-list-to-a-page}

若要新增 `Community Activity List` 元件至作者模式下的頁面，找到元件 `Communities / Community Activity List` 並將其拖曳至頁面上的適當位置。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當元件首次置於社群網站頁面時，以下是元件的顯示方式：

![社群活動](assets/community-activity.png)

### 設定社群活動清單  {#configuring-community-activity-list}

選取已放置的 `Community Activity List` 元件，然後選取 `Configure` 圖示以開啟「編輯」對話方塊。

![設定](assets/configure-new.png)

在 **註解** 索引標籤中，指定是否及如何顯示已上傳檔案的註解：

![屬性](assets/activity-list-properties.png)

* **類型**

  指定是否要顯示有關社群成員或使用者產生內容(UGC)的資料。

  選取自：

   * `Members`
   * `Content`

  預設為 `Members`.

* **顯示標題**

  要顯示在資料上方的描述性標題，例如 `Trending Content`.
預設為無標題。

* **顯示計數**

  要列出的專案數。
預設值為10。

* **活動型別**

  選取下列其中一項：

   * `Views`（頁面瀏覽數）
   * `Posts`（建立UGC）
   * `Follows`
   * `Likes`

  預設值為「檢視」。

* **時段**

  選取下列其中一項：

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1)`
   * `Total`

  預設為 `Total`.

* **內容路徑**

  這可讓您將活動範圍設定為網站的子集，例如特定部落格。
預設為整個社群網站。

* **成員人數彙總**

  取消選取（關閉）時，只會計算最上層的貼文。 例如，如果內容是根頁面（預設），則 `Activity Type` 之 `Posts` 絕不顯示任何活動，因為無法將內容張貼至根頁面。 如果勾選，則會包含所有下級頁面上的計數。
預設為已核取。

### 包含四個元件的範例頁面 {#example-page-with-components}

**排名在前的訪客** config：型別=成員，活動型別=檢視

**主要參與者** 設定：型別=成員，活動型別=貼文

**熱門內容** 設定：型別=內容，活動型別=檢視，

**趨勢內容** 設定：型別=內容，活動型別=貼文

![元件](assets/activity-list-components.png)
