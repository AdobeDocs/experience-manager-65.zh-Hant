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

`Community Activity List`元件可讓您新增成員貼文和檢視的趨勢資訊，以及內容的貼文和檢視。

本檔案說明：

* 正在將`Community Activity List`元件新增至[社群網站](/help/communities/overview.md#community-sites)。

* `Community Activity List`元件的組態設定。

### 需求 {#requirement}

`Community Activity List`的資料只有在針對社群網站授權並設定Adobe Analytics時才能使用。

請參閱[社群功能的Analytics設定](/help/communities/analytics.md)。

### 將社群活動清單新增至頁面 {#adding-a-community-activity-list-to-a-page}

若要將`Community Activity List`元件新增至作者模式的頁面，請找到元件`Communities / Community Activity List`並將其拖曳至頁面上的適當位置。

如需必要資訊，請造訪[社群元件基本知識](/help/communities/basics.md)。

當元件首次置於社群網站頁面時，以下是元件的顯示方式：

![社群活動](assets/community-activity.png)

### 設定社群活動清單  {#configuring-community-activity-list}

選取置入的`Community Activity List`元件，然後選取`Configure`圖示以開啟「編輯」對話方塊。

![設定](assets/configure-new.png)

在&#x200B;**註解**&#x200B;標籤下，指定是否及如何顯示已上傳檔案的註解：

![屬性](assets/activity-list-properties.png)

* **類型**

  指定是否要顯示有關社群成員或使用者產生內容(UGC)的資料。

  選取自：

   * `Members`
   * `Content`

  預設值為`Members`。

* **顯示標題**

  要在資料上方顯示的描述性標題，例如`Trending Content`。
預設為無標題。

* **顯示計數**

  要列出的專案數。
預設值為10。

* **活動型別**

  選取下列其中一項：

   * `Views`（頁面瀏覽次數）
   * `Posts`（正在建立UGC）
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

  預設值為`Total`。

* **內容路徑**

  這可讓您將活動範圍設定為網站的子集，例如特定部落格。
預設為整個社群網站。

* **成員計數彙總**

  取消選取（關閉）時，只會計算最上層的貼文。 例如，如果內容是根頁面（預設值），則`Posts`的`Activity Type`絕不會顯示任何活動，因為沒有能力將內容發佈到根頁面。 如果勾選，則會包含所有下級頁面上的計數。
預設為已核取。

### 包含四個元件的範例頁面 {#example-page-with-components}

**熱門訪客**&#x200B;設定：型別=成員，活動型別=檢視

**主要參與者**&#x200B;設定：型別=成員，活動型別=貼文

**最上層內容**&#x200B;設定：型別=內容，活動型別=檢視，

**趨勢內容**&#x200B;設定：型別=內容，活動型別=貼文

![元件](assets/activity-list-components.png)
