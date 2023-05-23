---
title: 查看頁面分析資料以評估頁面內容的有效性
description: 使用頁面分析資料來評估其頁面內容的有效性
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 4%

---

# 查看頁面分析資料{#seeing-page-analytics-data}

使用頁面分析資料來評估頁面內容的有效性。

## 從控制台可見的分析 {#analytics-visible-from-the-console}

![a-10](assets/aa-10.png)

頁面分析資料顯示在 [清單視圖](/help/sites-authoring/basic-handling.md#list-view) 的子菜單。 當頁面以清單格式顯示時，預設情況下以下列可用：

* 頁面檢視
* 不重複訪客
* 頁面逗留時間

每列都顯示當前報告期的值，並指示值自上一個報告期以來是增加還是減少。 您看到的資料每12小時更新一次。

>[!NOTE]
>
>要更改更新期間， [配置導入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)。

1. 開啟 **站點** 控制台；例如 [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. 在工具欄的最右側（右上角），按一下或點擊表徵圖以選擇 **清單視圖** (所顯示的表徵圖將取決於 [當前視圖](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources))。

1. 同樣，在工具欄的最右側（右上角），按一下或點擊表徵圖，然後選擇 **查看設定**。 的 **配置列** 對話框。 進行任何必需的更改並確認 **更新**。

   ![aa-04](assets/aa-04.png)

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

   ![aa-15](assets/aa-15.png)

1. 選擇要在站點控制台中向作者公開的度量，然後按一下 **添加**。

   顯示的列從Adobe Analytics檢索。

   ![aa-16](assets/aa-16.png)

### 從站點開啟內容透視 {#opening-content-insights-from-sites}

開啟 [內容透視](/help/sites-authoring/content-insights.md) 從「站點」控制台進一步調查頁面有效性。

1. 在「站點」控制台中，選擇要查看其內容透視的頁面。
1. 在工具欄上，按一下「分析」和「Recommendations」表徵圖。

   ![](do-not-localize/chlimage_1-16a.png)

## 從頁面編輯器中可見的分析(Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>如果 [Activity Map已配置](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) 的子菜單。

>[!NOTE]
>
>Activity Map資料取自Adobe Analytics。

當您的網站 [配置為Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md)，可以使用 [模式Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 查看相關資料。 例如：

![aa-07](assets/aa-07.png)

### 訪問Activity Map {#accessing-the-activity-map}

選擇 [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 模式，系統將要求您輸入Adobe Analytics憑據。

![aa-03](assets/aa-03.png)

的 **分析** 顯示浮動工具欄；您可以在此處：

* 使用雙箭頭更改工具欄格式(**>**)
* 切換頁面詳細資訊（眼睛表徵圖）
* 配置Activity Map設定（cog表徵圖）
* 選擇要顯示的分析（各種下拉選擇器）
* 退出Activity Map，然後關閉工具欄(x)

![aa-09](assets/aa-09.png)

### 選擇要顯示的分析 {#selecting-the-analytics-to-show}

可以使用各種標準選擇要顯示的分析資料以及顯示方式：

* **標準**/**實況**

* 事件類型
* 用戶組
* **氣泡**/**漸變**/**上升股與下跌股**/**關閉**

* 顯示的期間

![aa-13](assets/aa-13.png)

### 配置Activity Map {#configuring-the-activity-map}

使用 **顯示設定** 表徵圖以開啟 **Activity Map設定** 對話框。

![aa-04-1](assets/aa-04-1.png)

的 **Activity Map設定** 對話框提供了三個頁籤上的一系列選項：

![aa-06](assets/aa-06.png)

* 一般

   * 報表套裝
   * 頁面名稱
   * 語言
   * 標籤覆蓋
   * 標籤字型大小
   * 漸變顏色
   * 氣泡顏色
   * 基於的顏色漸變
   * 漸變透明度

* 標準

   * 顯示（連結類型和數量）
   * 隱藏未接收任何點擊的連結的疊加

* 即時

   * 顯示頂部（上升股或下跌股）
   * 排除底部%
   * 自動更新（資料和期間）
