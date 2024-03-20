---
title: 檢視頁面分析資料，以評估頁面內容的成效
description: 使用頁面分析資料來評估其頁面內容的成效
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
exl-id: 2e406512-47fb-451d-b837-0a3898ae1f08
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 4%

---

# 檢視頁面分析資料{#seeing-page-analytics-data}

使用頁面分析資料來評估頁面內容的成效。

## 從主控台可見的Analytics {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

頁面分析資料顯示於 [清單檢視](/help/sites-authoring/basic-handling.md#list-view) Sites主控台的。 當頁面以清單格式顯示時，預設會提供下列欄：

* 頁面檢視
* 獨特訪客
* 頁面逗留時間

每一欄會顯示目前報告期間的值，也會指出值自上一個報告期間以來是否有所增減。 您看到的資料每12小時更新一次。

>[!NOTE]
>
>若要變更更新期間， [設定匯入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. 開啟 **網站** 主控台；例如， [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. 在工具列的最右側（右上角），按一下圖示以選取 **清單檢視** (顯示的圖示取決於 [目前檢視](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources))。

1. 再次按一下工具列最右側（右上角）的圖示，然後選取 **檢視設定**. 此 **設定欄** 對話方塊開啟。 進行任何必要的變更，並確認： **更新**.

   ![spad-02](assets/spad-02.png)

### 選取報告期間 {#selecting-the-reporting-period}

選取Analytics資料出現在Sites Console上的報告期間：

* 最近 30 天的資料
* 最近 90 天的資料
* 今年的資料

目前的報告期間會顯示在網站主控台的工具列上（在頂端工具列的右側）。 使用下拉式清單來選取所需的報表期間。

![aa-05](assets/aa-05.png)

### 設定可用的資料欄 {#configuring-available-data-columns}

analytics-administrators使用者群組的成員可以設定Sites主控台，讓作者檢視額外的Analytics欄。

>[!NOTE]
>
>當頁面的樹狀結構包含與不同Adobe Analytics雲端設定相關聯的子項時，您無法為頁面設定可用的資料欄。

1. 在清單檢視中，使用檢視選取器（工具列右側），選取 **檢視設定** 然後 **新增自訂Analytics資料**.

   ![spad-03](assets/spad-03.png)

1. 選取您要在Sites主控台中向作者公開的量度，然後按一下 **新增**.

   顯示的欄是從Adobe Analytics中擷取的。

   ![aa-16](assets/aa-16.png)

### 從Sites開啟內容分析 {#opening-content-insights-from-sites}

開啟 [內容分析](/help/sites-authoring/content-insights.md) ，以進一步調查頁面的成效。

1. 在Sites主控台中，選取您要檢視其內容深入分析的頁面。
1. 在工具列上，按一下Analytics和Recommendations圖示。

   ![Analytics和Recommendations圖示](do-not-localize/chlimage_1-14.png)

## 從頁面編輯器可見的Analytics (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>由於Adobe Analytics API中的安全性變更，AEM中包含的Activity Map版本已無法再使用。
>
>此 [Adobe Analytics提供的ActivityMap外掛程式](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 現在應該使用。
