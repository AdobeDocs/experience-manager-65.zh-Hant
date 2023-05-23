---
title: 報告控制台
seo-title: Reports Console
description: 瞭解如何訪問報告
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

# 報告控制台 {#reports-console}

## 概觀 {#overview}

對於AEM Communities，有各種報告可以從作者環境以多種方式查閱。

總的來說，各種報告是：

* [檢視報表](#views-report)

   為任何社區站點提供按社區成員和站點訪問者列出的內容視圖圖表。

* [貼文報表](#posts-report)

   按社區成員向任何社區站點提供各種類型帖子的圖表。

表格式報告可以以.csv格式導出，以供後續處理。

## 報告控制台 {#reporting-consoles}

### 社區站點報告 {#reports-for-community-sites}

* 從全局導航： **[!UICONTROL 導航]** > **[!UICONTROL 社區]** >  **[!UICONTROL 報告]**

* 從以下選項中選擇：

   * **[!UICONTROL 指定任務報表]**

      * 為所選社區站點、用戶或組和分配生成報告。
   * **[!UICONTROL 貼文報表]**

      * 為所選社區站點、內容類型和時段生成報告。
   * **[!UICONTROL 檢視報表]**

      * 為所選社區站點、內容類型和時段生成報告。



![報告](assets/reports1.png)

## 檢視報表 {#views-report}

「視圖」控制台允許在給定時間段內按社區功能在頁面視圖上生成報告。

![查看報表](assets/view-report.png)

選擇報表的條件：

* **[!UICONTROL 網站]**

   選擇社區站點。

* **[!UICONTROL 內容類型]**

   可以選擇「全部內容」或選擇站點上存在的功能之一。

* **[!UICONTROL 時間框]**

   選擇以下選項之一：

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選擇 **[!UICONTROL 生成]** 的子菜單。

![生成視圖](assets/generate-views.png)

## 貼文報表 {#posts-report}

「帖子」控制台允許在給定時間段內生成針對社區功能帖子數的報告。

![員額報告](assets/posts-report.png)

選擇報表的條件：

* **[!UICONTROL 網站]**

   選擇社區站點。

* **[!UICONTROL 內容類型]**

   可以選擇「全部內容」或選擇站點上存在的功能之一。

* **[!UICONTROL 時間框]**

   選擇以下選項之一：

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選擇 **[!UICONTROL 生成]** 的子菜單。

![生成報告](assets/generate-posts-report.png)

## 疑難排解 {#troubleshooting}

### 未列出社區站點 {#no-community-sites-listed}

如果未列出社區站點，請確保已為站點啟用Adobe Analytics。 如果選擇分配的報告，請確保分配功能位於社區站點的結構中。

### 報告不在AEM作者實例中顯示 {#reports-do-not-show-in-aem-author-instance}

如果報告未在AEM作者實例中顯示，請檢查自定義項，如發佈實例上的URL映射。 如果僅在社區站點的AEM發佈實例上完成URL映射，請確保在中的AEM Author實例中配置了該映射 **地點趨勢報表社會元件工廠** 配置。

![AEM作者上的URL映射](assets/sitetrend.png)
