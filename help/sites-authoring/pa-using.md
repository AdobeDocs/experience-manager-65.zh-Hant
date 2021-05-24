---
title: 查看頁面分析資料
seo-title: 查看頁面分析資料
description: 使用頁面分析資料來評估其頁面內容的有效性
seo-description: 使用頁面分析資料來評估其頁面內容的有效性
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 4%

---

# 查看頁面分析資料{#seeing-page-analytics-data}

使用頁面分析資料來評估頁面內容的有效性。

## 從控制台{#analytics-visible-from-the-console}可見的分析

![aa-10](assets/aa-10.png)

頁面分析資料會顯示在Sites主控台的[清單檢視](/help/sites-authoring/basic-handling.md#list-view)中。 當頁面以清單格式顯示時，預設會提供下列欄：

* 頁面檢視
* 不重複訪客
* 頁面逗留時間

每欄會顯示目前報告期間的值，也指出值自上一個報告期間以來是否增加或減少。 您看到的資料會每12小時更新一次。

>[!NOTE]
>
>要更改更新期間，請[配置導入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)。

1. 開啟&#x200B;**Sites**&#x200B;主控台；例如[http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. 在工具列的最右側（右上角），按一下或點選圖示以選取&#x200B;**清單檢視**（顯示的圖示取決於[目前檢視](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)）。

1. 同樣地，在工具列的最右側（右上角），按一下或點選圖示，然後選取「**檢視設定**」。 將會開啟&#x200B;**配置列**&#x200B;對話框。 進行任何需要的更改，並使用&#x200B;**Update**&#x200B;確認。

   ![aa-04](assets/aa-04.png)

### 選擇報告期{#selecting-the-reporting-period}

選取Analytics資料會出現在Sites Console的報表時段：

* 最近 30 天的資料
* 最近 90 天的資料
* 今年的資料

目前的報告時段會顯示在Sites Console的工具列上（頂端工具列的右側）。 使用下拉式清單來選取所需的報告期間。
![aa-05](assets/aa-05.png)

### 配置可用資料列{#configuring-available-data-columns}

分析管理員使用者群組的成員可以設定Sites Console，讓作者看到額外的Analytics欄。

>[!NOTE]
>
>當頁面樹狀結構包含與不同Adobe Analytics雲端設定相關聯的子項時，您無法為頁面設定可用的資料欄。

1. 在「清單檢視」中，使用檢視選取器（工具列右側），選取「**檢視設定**」，然後選取「**新增自訂Analytics資料**」。

   ![aa-15](assets/aa-15.png)

1. 在Sites控制台中，選取您要公開給作者的量度，然後按一下&#x200B;**Add**。

   顯示的欄會從Adobe Analytics中擷取。

   ![aa-16](assets/aa-16.png)

### 從網站開啟內容分析{#opening-content-insights-from-sites}

從Sites主控台開啟[內容分析](/help/sites-authoring/content-insights.md)以進一步調查頁面有效性。

1. 在Sites Console中，選取您要查看「內容分析」的頁面。
1. 在工具列上，按一下Analytics和Recommendations圖示。

   ![](do-not-localize/chlimage_1-16a.png)

## 從頁面編輯器(Activity Map){#analytics-visible-from-the-page-editor-activity-map}中可見的分析

>[!NOTE]
>
>如果已為您的網站設定[Activity Map](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map)，則會顯示此資訊。

>[!NOTE]
>
>Activity Map的資料取自Adobe Analytics。

當您的網站已針對Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md)進行[設定時，您可以使用[模式Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes)來檢視相關資料。 例如：

![aa-07](assets/aa-07.png)

### 訪問Activity Map{#accessing-the-activity-map}

選取[Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes)模式後，系統會要求您輸入Adobe Analytics憑證。

![aa-03](assets/aa-03.png)

顯示&#x200B;**Analytics**&#x200B;浮動工具列；您可以在此：

* 使用雙箭頭(**>>**)更改工具欄格式
* 切換頁面詳細資料（眼睛圖示）
* 配置Activity Map設定（齒輪表徵圖）
* 選取要顯示的分析（各種下拉式選取器）
* 結束Activity Map，然後關閉工具列(x)

![aa-09](assets/aa-09.png)

### 選取要顯示{#selecting-the-analytics-to-show}的Analytics

您可以使用各種准則來選取要顯示的分析資料及其顯示方式：

* **標準**/**上線**

* 事件類型
* 使用者群組
* **泡泡**/**漸層**/**獲益者和損失者**/**關閉**

* 顯示的期間

![aa-13](assets/aa-13.png)

### 配置Activity Map{#configuring-the-activity-map}

使用&#x200B;**顯示設定**&#x200B;表徵圖開啟&#x200B;**Activity Map設定**&#x200B;對話框。

![aa-04-1](assets/aa-04-1.png)

**Activity Map設定**&#x200B;對話方塊提供三個標籤上的選項範圍：

![aa-06](assets/aa-06.png)

* 一般

   * 報表套裝
   * 頁面名稱
   * 語言
   * 標籤覆蓋圖
   * 標籤字型大小
   * 漸層顏色
   * 氣泡顏色
   * 顏色漸層根據
   * 漸層透明度

* 標準

   * 顯示（連結類型和數目）
   * 隱藏未收到點擊之連結的覆蓋圖

* 即時

   * 顯示排名最前（獲益者或損失者）
   * 排除最後%
   * 自動更新（資料和期間）
