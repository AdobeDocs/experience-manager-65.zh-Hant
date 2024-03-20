---
title: 內容分析
description: 內容分析會使用網頁分析和SEO建議來提供頁面效能的相關資訊
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 3%

---

# 內容分析{#content-insight}

「內容分析」會使用網頁分析和SEO建議來提供頁面效能的相關資訊。 使用內容深入分析來決定如何修改頁面，或瞭解先前的變更如何變更效能。 對於您編寫的每個頁面，都可以開啟「內容分析」來分析頁面。

![chlimage_1-311](assets/chlimage_1-311.png)

「內容分析」頁面的版面配置會隨著您使用之裝置的熒幕維度和方向而改變。

## 報表資料

「內容分析」頁面包含使用Adobe SiteCatalyst、Adobe Target、Adobe Social和BrightEdge資料的報表：

* SiteCatalyst：下列量度的報表可供使用：

   * 頁面檢視
   * 頁面平均逗留時間
   * 來源

* Target：頁面包含選件的促銷活動報表。
* BrightEdge：報告可改善搜尋引擎頁面可見度的頁面功能，並建議應實作的功能。

另請參閱 [開啟頁面的Analytics和Recommendations](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page).

## 報告期間

報表會顯示您所控制的一段時間的資料。 當您調整報表時段時，報表會自動重新整理該時段的資料。 視覺提示會指出頁面版本變更的時間，讓您能夠比較每個版本的效能。

>[!NOTE]
>
>內容深入分析控制面板的時間表位於 `GMT`.

您也可以指定報告資料的詳細程度，例如，您可以檢視每日、每週、每月或每年資料。

另請參閱 [變更報告期間](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period).

>[!NOTE]
>
>內容深入分析報表要求您的管理員已將AEM與SiteCatalyst、Target和BrightEdge整合。 另請參閱 [與SightCatalyst整合](/help/sites-administering/adobeanalytics.md)， [與Adobe Target整合](/help/sites-administering/target.md)、和 [與BrightEdge整合](/help/sites-administering/brightedge.md).

## 檢視報表 {#the-views-report}

「檢視」報表包含下列用於評估頁面流量的功能：

* 在報告期間，某個頁面的檢視總數。
* 報告期間檢視次數的圖表：

   * 檢視總數。
   * 不重複訪客。

![chlimage_1-312](assets/chlimage_1-312.png)

## 頁面平均參與報表 {#the-page-average-engaged-report}

「頁面平均參與次數」報表包含下列評估頁面成效的功能：

* 整個報告期間頁面保持開啟的平均時間。
* 整個報告期間頁面檢視平均長度的圖表。

![chlimage_1-313](assets/chlimage_1-313.png)

## 來源報表 {#the-sources-report}

「來源」報表指出使用者如何導覽至頁面，例如從搜尋引擎結果或使用已知URL。

![chlimage_1-314](assets/chlimage_1-314.png)

## 彈回報表 {#the-bounces-report}

「跳出數」報表所包含的圖形，可顯示某個頁面在選定報表期間發生的跳出次數。

![chlimage_1-315](assets/chlimage_1-315.png)

## 行銷活動報表 {#the-campaign-activity-report}

針對頁面有效的每個行銷活動，都會顯示一份報表，名為 *行銷活動名稱* 活動。 報表會顯示提供選件的每個區段的頁面曝光次數和轉換次數。

![chlimage_1-316](assets/chlimage_1-316.png)

## SEO Recommendations報表 {#the-seo-recommendations-report}

SEO Recommendations報表包含頁面的BrightEdge分析結果。 此報表是頁面功能的檢查清單，指出頁面包含和不包含哪些功能，以使用搜尋引擎最大化尋找能力。

報表可讓您建立任務，以便進行改善以改進頁面可查詢性。 Recommendations會指出已建立實施建議的工作。 另請參閱 [指派SEO Recommendations的任務](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations).

![chlimage_1-317](assets/chlimage_1-317.png)
