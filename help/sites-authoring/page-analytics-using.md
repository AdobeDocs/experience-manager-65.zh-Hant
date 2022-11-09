---
title: 查看頁面分析資料
seo-title: Seeing Page Analytics Data
description: 使用頁面分析資料來評估其頁面內容的有效性
seo-description: Use page analytics data to gauge the effectiveness of their page content
uuid: 5398a5d5-0239-4194-a403-77f5e6fcd741
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 5d192a48-c86f-4803-bb0d-0411ac7470f5
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
exl-id: 2e406512-47fb-451d-b837-0a3898ae1f08
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 11%

---

# 查看頁面分析資料{#seeing-page-analytics-data}

使用頁面分析資料來評估頁面內容的有效性。

## 從主控台顯示的分析 {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

頁面分析資料顯示於 [清單檢視](/help/sites-authoring/basic-handling.md#list-view) 的下一頁。 當頁面以清單格式顯示時，預設會提供下列欄：

* 頁面檢視
* 不重複訪客
* 頁面逗留時間

每欄會顯示目前報告期間的值，也指出值自上一個報告期間以來是否增加或減少。 您看到的資料會每12小時更新一次。

>[!NOTE]
>
>要更改更新期間， [設定匯入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. 開啟 **網站** 主控台；例如 [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. 在工具列的最右側（右上角），按一下或點選圖示以選取 **清單檢視** (所顯示的圖示取決於 [目前檢視](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources))。

1. 同樣地，在工具列的最右側（右上角），按一下或點選圖示，然後選取 **檢視設定**. 此 **配置列** 對話框將開啟。 進行任何必要的變更，並使用確認 **更新**.

   ![spad-02](assets/spad-02.png)

### 選擇報告期 {#selecting-the-reporting-period}

選取Analytics資料會出現在Sites Console的報表時段：

* 最近 30 天的資料
* 最近 90 天的資料
* 今年的資料

目前的報告時段會顯示在Sites Console的工具列上（頂端工具列的右側）。 使用下拉式清單來選取所需的報告期間。

![aa-05](assets/aa-05.png)

### 配置可用資料列 {#configuring-available-data-columns}

分析管理員使用者群組的成員可以設定Sites Console，讓作者看到額外的Analytics欄。

>[!NOTE]
>
>當頁面樹狀結構包含與不同Adobe Analytics雲端設定相關聯的子項時，您無法為頁面設定可用的資料欄。

1. 在「清單視圖」中，使用視圖選擇器（工具欄右側），選擇 **檢視設定** 然後 **新增自訂Analytics資料**.

   ![spad-03](assets/spad-03.png)

1. 在Sites控制台中選取要公開給作者的量度，然後按一下 **新增**.

   顯示的欄會從Adobe Analytics中擷取。

   ![aa-16](assets/aa-16.png)

### 從網站開啟內容分析 {#opening-content-insights-from-sites}

開啟 [內容分析](/help/sites-authoring/content-insights.md) 從Sites主控台進一步調查頁面有效性。

1. 在Sites Console中，選取您要查看「內容分析」的頁面。
1. 在工具列上，按一下Analytics和Recommendations圖示。

   ![](do-not-localize/chlimage_1-14.png)

## 頁面編輯器中可見的分析(Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。
>
>此 [ActivityMap外掛程式由Adobe Analytics提供](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 現在應該使用。
