---
title: 報表主控台
description: 瞭解如何使用各種可從Adobe Experience Manager作者環境以數種方式存取的報告。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 6%

---

# 報表主控台 {#reports-console}

## 概觀 {#overview}

對於AEM Communities，有多種報表可從作者環境以數種方式存取。

一般而言，各種報表包括：

* [檢視報告](#views-report)

  提供社群成員和網站訪客針對任何社群網站檢視內容的圖表。

* [貼文報表](#posts-report)

  提供社群成員在任何社群網站的各種型別貼文的圖表。

表格式報表可以匯出為.csv格式，以供後續處理。

## 報告主控台 {#reporting-consoles}

### 社群網站報表 {#reports-for-community-sites}

* 從全域導覽： **[!UICONTROL 導覽]** > **[!UICONTROL Communities]** >  **[!UICONTROL 報表]**

* 選擇來源：

   * **[!UICONTROL 指定任務報表]**

      * 為選取的社群網站、使用者或群組以及指派專案產生報告。

   * **[!UICONTROL 貼文報表]**

      * 針對選取的社群網站、內容型別和時段產生報表。

   * **[!UICONTROL 檢視報告]**

      * 針對選取的社群網站、內容型別和時段產生報表。

![報表](assets/reports1.png)

## 檢視報表 {#views-report}

檢視控制檯可讓社群功能在指定時段內針對頁面檢視產生報表。

![檢視報告](assets/view-report.png)

選取報告的條件：

* **[!UICONTROL 網站]**

  選取社群網站。

* **[!UICONTROL 內容型別]**

  可以選擇「所有內容」或選取網站上存在的其中一個功能。

* **[!UICONTROL 時間段]**

  選取下列其中一項：

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選取 **[!UICONTROL 產生]** 以建立報表。

![產生檢視](assets/generate-views.png)

## 貼文報表 {#posts-report}

「貼文」主控台可讓您針對指定時段內社群功能的貼文數量產生報表。

![posts-report](assets/posts-report.png)

選取報告的條件：

* **[!UICONTROL 網站]**

  選取社群網站。

* **[!UICONTROL 內容型別]**

  可以選擇「所有內容」或選取網站上存在的其中一個功能。

* **[!UICONTROL 時間段]**

  選取下列其中一項：

   * 過去 7 天
   * 過去 30 天
   * 過去 90 天
   * 去年

選取 **[!UICONTROL 產生]** 以建立報表。

![generate-report](assets/generate-posts-report.png)

## 疑難排解 {#troubleshooting}

### 未列出任何社群網站 {#no-community-sites-listed}

如果未列出任何社群網站，請確定已針對網站啟用Adobe Analytics。 如果選擇工作分派報表，請確定工作分派功能在社群網站的結構中。

### 報告未顯示在AEM編寫執行個體中 {#reports-do-not-show-in-aem-author-instance}

如果報表未顯示在AEM編寫執行個體中，請檢查自訂，例如發佈執行個體上的URL對應。 如果URL對應僅在Communities網站的AEM Publish例項上完成，請確保已在的AEM Author例項中設定相同的專案。 **網站趨勢報表社交元件工廠** 設定。

![AEM作者上的URL對應](assets/sitetrend.png)
