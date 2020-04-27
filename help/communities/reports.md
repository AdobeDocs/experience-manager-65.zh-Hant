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
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# 報表主控台 {#reports-console}

## 概覽 {#overview}

對於AEM Communities，有多種報表可透過數種方式從作者環境存取。

一般而言，各種報表包括：

* [指定任務報表](#assignments-report)

   對於啟 [用社群](/help/communities/overview.md#enablement-community)，提供學員作業進度的概觀，包括實施SCORM標準時的相關分數。

* [檢視報表](#views-report)

   提供任何社群網站的社群成員和網站訪客的內容檢視圖表。

* [貼文報表](#posts-report)

   提供社群成員對任何社群網站之各類貼文的圖表。

啟用 [Adobe Analytics後](/help/communities/sites-console.md#analytics)，報表將包含一段時間內每個啟用資源的檢視次數、播放次數、留言和評分。

表格報表可匯出為。csv格式，以供後續處理。

## 報告控制台 {#reporting-consoles}

### 社群網站的報表 {#reports-for-community-sites}

* 從全域導覽：導覽 **[!UICONTROL >]** 社群 **[!UICONTROL >報]****[!UICONTROL 表]**

* 選擇：

   * **[!UICONTROL 指定任務報表]**

      * 為選定的社區站點、用戶或組和分配生成報告。
   * **[!UICONTROL 貼文報表]**

      * 為選取的社群網站、內容類型和時段產生報表。
   * **[!UICONTROL 檢視報表]**

      * 為選取的社群網站、內容類型和時段產生報表。



![chlimage_1-236](assets/chlimage_1-236.png)

### 啟用資源和學習路徑的報表 {#reports-for-enablement-resources-and-learning-paths}

* 從全域導覽：導覽 **[!UICONTROL >]** 社群 **[!UICONTROL >資]****[!UICONTROL 源]**

* 選取現有的啟用社群網站：

   * 選取 **報表圖示** ，以產生涵蓋所有啟用資源的報表。
   * 選擇啟用學習路徑。
   * 選擇 **報表圖** 示，以產生報表：

      * 隨附的啟用資源。
      * 指派給學習路徑的學員。

* 這些報告提供：

   * 可下載為CSV的表格資料：

      * 識別學員
      * 他們的狀態
      * 是指派或透過目錄存取
      * 留言數
      * 指定星級

如需詳細資訊，請參 [閱「資源](/help/communities/resources.md#report) 」主控台的「報表」區段。

## 指定任務報表 {#assignments-report}

「工作總管」可讓報表依啟用社群網站、使用者或群組以及工作來篩選。

報告提供有關其進度的資訊，以及所提供的任何意見或評分。

![chlimage_1-237](assets/chlimage_1-237.png)

選取報表的條件：

* **網站**

   選取啟用社群網站。

* **使用者或群組**
   * 選取「使用者」，為一個學員產生報表。
   * 選取「群組」，為學員群組產生報表。
   隧道服務將從發佈環境訪問成員和成員組。

* **指定任務**

   從指派給所選學員的啟用資源中進行選擇。

選擇 **生成** ，建立報表：

![chlimage_1-238](assets/chlimage_1-238.png)

## 檢視報表 {#views-report}

「檢視」控制台可讓報表在指定時段內，依社群功能在頁面檢視時產生。

![chlimage_1-239](assets/chlimage_1-239.png)

選擇報表的標準：

* **[!UICONTROL 網站]**

   選擇社群網站。

* **[!UICONTROL 內容類型]**

   可選擇「所有內容」或選擇網站上的其中一個功能。

* **[!UICONTROL 時間範圍]**

   選擇以下選項之一：

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選擇 **[!UICONTROL 產生]** ，以建立報表。

![chlimage_1-240](assets/chlimage_1-240.png)

## 貼文報表 {#posts-report}

「貼文」控制台可讓您針對特定時段內社群功能的貼文數產生報表。

![chlimage_1-241](assets/chlimage_1-241.png)

選擇報表的標準：

* **[!UICONTROL 網站]**

   選擇社群網站。

* **[!UICONTROL 內容類型]**

   可選擇「所有內容」或選擇網站上的其中一個功能。

* **[!UICONTROL 時間範圍]**

   選擇以下選項之一：

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選擇 **[!UICONTROL 產生]** ，以建立報表。

![chlimage_1-242](assets/chlimage_1-242.png)

## 疑難排解 {#troubleshooting}

### 未列出社群網站 {#no-community-sites-listed}

如果未列出社群網站，請確定已為網站啟用Adobe Analytics。 如果選擇分配報告，請確保分配功能位於社區站點的結構中。

### 報表不會顯示在AEM Author例項中 {#reports-do-not-show-in-aem-author-instance}

如果報表未顯示在「AEM作者」例項中，請檢查自訂項目，例如「發佈」例項上的URL對應。 如果URL對應僅在社群網站的AEM Publish例項上完成，請確定AEM Author例項中已在「網站趨勢報表社交元件工廠」設定中設定 **過相同的對應** 。

![AEM作者的URL對應](assets/sitetrend.png)