---
title: 檢視頁面分析資料
seo-title: 檢視頁面分析資料
description: 使用頁面分析資料來評估其頁面內容的有效性
seo-description: 使用頁面分析資料來評估其頁面內容的有效性
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e

---


# 檢視頁面分析資料{#seeing-page-analytics-data}

使用頁面分析資料來評估頁面內容的有效性。

## 從主控台顯示的分析 {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

頁面分析資料會顯示在 [網站主控台的](/help/sites-authoring/basic-handling.md#list-view) 「清單檢視」中。 當頁面以清單格式顯示時，預設情況下可使用以下列：

* 頁面檢視
* 獨特訪客
* 頁面逗留時間

每個欄會顯示目前報告期間的值，並指出該值自上一個報告期間以來是否增加或減少。 您看到的資料每12小時更新一次。

>[!NOTE]
>
>若要變更更新期間，請 [設定匯入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)。

1. 開啟 **Sites** Console;例如 [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. 在工具列的最右側（右上角），按一下或點選圖示以選取「清單檢視」( **List View** )(顯示的圖示將視目前 [的檢視而定](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources))。

1. 同樣地，在工具列的最右側（右上角），按一下或點選圖示，然後選取「檢視 **設定」**。 將會 **開啟「配置列** 」對話框。 進行任何必要的變更，並使用「更新」 **進行確認**。

   ![aa-04](assets/aa-04.png)

### 選擇報告期 {#selecting-the-reporting-period}

選取Analytics資料會顯示在Sites主控台上的報表時段：

* 最近 30 天的資料
* 最近 90 天的資料
* 今年的資料

目前的報告時段會顯示在Sites主控台的工具列（頂端工具列的右側）上。 使用下拉式清單來選擇所需的報表時段。
![aa-05](assets/aa-05.png)

### 配置可用資料列 {#configuring-available-data-columns}

分析管理員使用者群組的成員可以設定「網站」主控台，讓作者可以查看額外的Analytics欄。

>[!NOTE]
>
>當頁面樹狀結構包含與不同Adobe Analytics雲端設定相關聯的子系時，您無法設定頁面的可用資料欄。

1. 在清單檢視中，使用檢視選擇器（工具列右側），選取檢 **視設定** , **然後新增自訂分析資料**。

   ![aa-15](assets/aa-15.png)

1. 在「網站」主控台中，選取您要向作者公開的量度，然後按一下「新 **增」**。

   顯示的欄會從Adobe Analytics擷取。

   ![aa-16](assets/aa-16.png)

### 從網站開啟內容見解 {#opening-content-insights-from-sites}

從 [Sites主控台開啟Content Insight](/help/sites-authoring/content-insights.md) ，以進一步調查頁面效能。

1. 在「網站」主控台中，選取您要查看其內容分析的頁面。
1. 在工具列上，按一下「Analytics and Recommendations」圖示。

   ![](do-not-localize/chlimage_1-16a.png)

## 從頁面編輯器(Activity Map)可見的分析 {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>如果已為您的網站設 [定Activity Map](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) ，則會顯示此資訊。

>[!NOTE]
>
>Activity map的資料取自Adobe Analytics。

當您的網站已設 [定為Adobe Analytics時](/help/sites-administering/adobeanalytics-connect.md)，您可以使用 [模式Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 來檢視相關資料。 例如：

![aa-07](assets/aa-07.png)

### 存取Activity Map {#accessing-the-activity-map}

在選取 [Activity Map模式後](/help/sites-authoring/author-environment-tools.md#page-modes) ，系統會要求您輸入Adobe Analytics認證。

![aa-03](assets/aa-03.png)

顯示 **了Analytics** 浮動工具列；您可以在這裡：

* 使用雙箭頭(**>>**)更改工具欄格式
* 切換頁面詳細資訊（眼睛圖示）
* 設定Activity map設定（cog圖示）
* 選取要顯示的分析（各種下拉式選擇器）
* 結束Activity Map，並關閉工具列(x)

![aa-09](assets/aa-09.png)

### 選取要顯示的分析 {#selecting-the-analytics-to-show}

您可以使用各種標準，選擇要顯示的分析資料以及顯示方式：

* **Standard**/**Live**

* 事件類型
* 使用者群組
* **泡泡**/**漸層**/獲益&#x200B;**者與損失者**/**關閉**

* 顯示期間

![aa-13](assets/aa-13.png)

### 設定Activity Map {#configuring-the-activity-map}

使用「顯 **示設定** 」圖示開啟「 **Activity Map設定」對話方塊** 。

![aa-04-1](assets/aa-04-1.png)

「 **Activity map設定** 」對話方塊提供三個標籤上的選項範圍：

![aa-06](assets/aa-06.png)

* 一般

   * 報表套裝
   * 頁面名稱
   * 語言
   * 標籤覆蓋與
   * 標籤字型大小
   * 漸層顏色
   * 泡泡顏色
   * 根據
   * 漸層透明度

* 標準

   * 顯示（連結類型和數目）
   * 隱藏未收到點擊之連結的覆蓋圖

* 即時

   * 顯示頂端（獲益者或損失者）
   * 排除底部%
   * 自動更新（資料和期間）

