---
title: 查看頁面分析資料以評估頁面內容的有效性
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
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 11%

---

# 查看頁面分析資料{#seeing-page-analytics-data}

使用頁面分析資料來評估頁面內容的有效性。

## 從控制台可見的分析 {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

頁面分析資料顯示在 [清單視圖](/help/sites-authoring/basic-handling.md#list-view) 的子菜單。 當頁面以清單格式顯示時，預設情況下以下列可用：

* 頁面檢視
* 不重複訪客
* 頁面逗留時間

每列都顯示當前報告期的值，並指示值自上一個報告期以來是增加還是減少。 您看到的資料每12小時更新一次。

>[!NOTE]
>
>要更改更新期間， [配置導入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)。

1. 開啟 **站點** 控制台；例如 [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. 在工具欄的最右側（右上角），按一下或點擊表徵圖以選擇 **清單視圖** (所顯示的表徵圖將取決於 [當前視圖](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources))。

1. 同樣，在工具欄的最右側（右上角），按一下或點擊表徵圖，然後選擇 **查看設定**。 的 **配置列** 對話框。 進行任何必需的更改並確認 **更新**。

   ![spad-02](assets/spad-02.png)

### 選擇報告期 {#selecting-the-reporting-period}

選擇在「站點」控制台上顯示分析資料的報告期：

* 最近 30 天的資料
* 最近 90 天的資料
* 今年的資料

當前報告期出現在「站點」控制台的工具欄（頂部工具欄的右側）上。 使用下拉框選擇所需的報告期間。

![aa-05](assets/aa-05.png)

### 配置可用資料列 {#configuring-available-data-columns}

analytics-administrators用戶組的成員可以配置「站點」控制台，使作者能夠查看額外的「分析」列。

>[!NOTE]
>
>如果頁面樹包含與不同的Adobe Analytics雲配置關聯的子級，則無法配置頁面的可用資料列。

1. 在「清單視圖」中，使用視圖選擇器（工具欄右側），選擇 **查看設定** 然後 **添加自定義分析資料**。

   ![spad-03](assets/spad-03.png)

1. 選擇要在站點控制台中向作者公開的度量，然後按一下 **添加**。

   顯示的列從Adobe Analytics檢索。

   ![aa-16](assets/aa-16.png)

### 從站點開啟內容透視 {#opening-content-insights-from-sites}

開啟 [內容透視](/help/sites-authoring/content-insights.md) 從「站點」控制台進一步調查頁面有效性。

1. 在「站點」控制台中，選擇要查看其內容透視的頁面。
1. 在工具欄上，按一下「分析」和「Recommendations」表徵圖。

   ![](do-not-localize/chlimage_1-14.png)

## 從頁面編輯器中可見的分析(Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。
>
>的 [由Adobe Analytics提供的ActivityMap插件](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 應該被使用。
