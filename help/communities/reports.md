---
title: 報表主控台
seo-title: 報表主控台
description: 瞭解如何存取報表
seo-description: 瞭解如何存取報表
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 報表主控台{#reports-console}

## 概覽 {#overview}

對於AEM Communities，有多種報表可透過數種方式從作者環境存取。

一般而言，各種報表包括：

* [工作報表](#assignments-report) -針對啟用 [社群](/help/communities/overview.md#enablement-community)，提供學員在其工作上的進度概觀，包括在實作SCORM標準時的相關分數
* [檢視報表](#views-report) -提供任何社群網站的社群成員和網站訪客的內容檢視圖表
* [貼文報表](#posts-report) -提供社群成員張貼至任何社群網站的各種貼文類型圖表

啟用 [Adobe Analytics後](/help/communities/sites-console.md#analytics)，報表將包含一段時間內每個啟用資源的檢視次數、播放次數、留言和評分

表格報表可匯出為。csv格式，以供後續處理。

## 報告控制台 {#reporting-consoles}

### 社群網站的報表 {#reports-for-community-sites}

* 從全域導覽：導 **覽**、社 **群、報表**

* 選擇

   * **指定任務報表**

      * 為選定的社區站點、用戶或組和分配生成報告

      * **貼文報表**

         * 為所選社群網站、內容類型和時段產生報表
      * **檢視報表**

         * 為所選社群網站、內容類型和時段產生報表


![chlimage_1-236](assets/chlimage_1-236.png)

### 啟用資源和學習路徑的報表 {#reports-for-enablement-resources-and-learning-paths}

* 從全局導航：導 **覽**、社 **群、資源**

* 選取現有的啟用社群網站

   * 選擇**報表**圖示以產生涵蓋所有啟用資源的報表
   * 選擇啟用學習路徑
   * 選擇**報表**圖示，以產生

      * 隨附的啟用資源
      * 指派給學習路徑的學員

* 這些報表提供：

   * 表格資料，可下載為CSV

      * 識別學員
      * 他們的地位
      * 是否通過目錄分配或訪問
      * 評論的次數
      * 星級

如需詳細資訊，請參 [閱「資源](/help/communities/resources.md#report) 」主控台的「報表」區段。

## 指定任務報表 {#assignments-report}

「工作總管」可讓報表依啟用社群網站、使用者或群組以及工作來篩選。

報告提供有關其進度的資訊，以及所提供的任何意見或評分。

![chlimage_1-237](assets/chlimage_1-237.png)

選取報表的條件：

* **網站**

   選擇啟用社群網站

* **使用者或群組**
   * 選擇使用者以產生一個學員的報表
   * 選取群組以產生學員群組的報表
   隧道服務將從發佈環境訪問成員和成員組

* **指定任務**

   從指派給所選學員的啟用資源中選擇

選擇 **產生** ，以建立報表：

![chlimage_1-238](assets/chlimage_1-238.png)

## 檢視報表 {#views-report}

「檢視」控制台可讓報表在指定時段內，依社群功能在頁面檢視時產生。

![chlimage_1-239](assets/chlimage_1-239.png)

選取報表的條件：

* **網站**

   選擇社區站點

* **內容類型**

   可以選擇「全部內容」，或選擇網站上的其中一個功能

* 時間幀

   選擇其中一個

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選擇 **產生** ，以建立報表：

![chlimage_1-240](assets/chlimage_1-240.png)

## 貼文報表 {#posts-report}

「貼文」控制台可讓您針對特定時段內社群功能的貼文數產生報表。

![chlimage_1-241](assets/chlimage_1-241.png)

選取報表的條件：

* **網站**

   選擇社區站點

* **內容類型**

   可以選擇「全部內容」，或選擇網站上的其中一個功能

* 時間幀

   選擇其中一個

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選擇 **產生** ，以建立報表：

![chlimage_1-242](assets/chlimage_1-242.png)

## 疑難排解 {#troubleshooting}

### 未列出社群網站 {#no-community-sites-listed}

如果未列出社群網站，請確定已為網站啟用Adobe Analytics。 如果選擇分配報告，請確保分配功能位於社區站點的結構中。

### 報表不會顯示在AEM Author例項中 {#reports-do-not-show-in-aem-author-instance}

如果報表未顯示在「AEM作者」例項中，請檢查自訂項目，例如「發佈」例項上的URL對應。 如果URL對應僅在社群網站的AEM Publish例項上完成，請確定已在**Site Trend Report Social元件工廠**組態的AEM Author例項中設定過相同的對應。

![AEM作者的URL對應](assets/sitetrend.png)