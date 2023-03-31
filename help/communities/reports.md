---
title: 報表主控台
seo-title: Reports Console
description: 了解如何存取報表
seo-description: Learn how to access reports
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# 報表主控台 {#reports-console}

## 概觀 {#overview}

針對AEM Communities，有多種報表可從製作環境以數種方式存取。

一般而言，各種報告包括：

* [檢視報表](#views-report)

   提供任何社群網站的社群成員和網站訪客的內容檢視圖表。

* [貼文報表](#posts-report)

   提供依社群成員到任何社群網站的各種貼文類型的圖表。

表格報表可匯出為.csv格式，以供後續處理。

## 報表主控台 {#reporting-consoles}

### 社群網站報表 {#reports-for-community-sites}

* 從全局導航： **[!UICONTROL 導覽]** > **[!UICONTROL 社群]** >  **[!UICONTROL 報表]**

* 選擇：

   * **[!UICONTROL 指定任務報表]**

      * 為所選社區站點、用戶或組和分配生成報告。
   * **[!UICONTROL 貼文報表]**

      * 為所選社區站點、內容類型和時段生成報告。
   * **[!UICONTROL 檢視報表]**

      * 為選定的社區站點、內容類型和時段生成報告。



![報告](assets/reports1.png)

## 檢視報表 {#views-report}

「檢視」主控台可讓您在指定時段內，依社群功能在頁面檢視時產生報表。

![檢視報表](assets/view-report.png)

選取報表的條件：

* **[!UICONTROL 網站]**

   選擇社區站點。

* **[!UICONTROL 內容類型]**

   可以選擇「全部內容」或選擇站點上存在的功能之一。

* **[!UICONTROL 時間範圍]**

   選擇以下選項之一：

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選擇 **[!UICONTROL 產生]** 來建立報表。

![generate-views](assets/generate-views.png)

## 貼文報表 {#posts-report}

「貼文」主控台可針對特定時段內社群功能的貼文數產生報表。

![貼文 — 報表](assets/posts-report.png)

選取報表的條件：

* **[!UICONTROL 網站]**

   選擇社區站點。

* **[!UICONTROL 內容類型]**

   可以選擇「全部內容」或選擇站點上存在的功能之一。

* **[!UICONTROL 時間範圍]**

   選擇以下選項之一：

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選擇 **[!UICONTROL 產生]** 來建立報表。

![generate-report](assets/generate-posts-report.png)

## 疑難排解 {#troubleshooting}

### 未列出社區站點 {#no-community-sites-listed}

如果未列出社群網站，請確定已為網站啟用Adobe Analytics。 如果選擇分配的報表，請確保分配函式位於社區站點的結構中。

### 報表未顯示在AEM製作例項中 {#reports-do-not-show-in-aem-author-instance}

如果報表未顯示在AEM製作例項中，請檢查是否有自訂項目，例如「發佈」例項上的URL對應。 如果僅在社群網站的AEM Publish例項上完成URL對應，請確定已在中的AEM Author例項中設定相同的URL對應 **網站趨勢報表社交元件工廠** 設定。

![AEM作者上的URL對應](assets/sitetrend.png)
