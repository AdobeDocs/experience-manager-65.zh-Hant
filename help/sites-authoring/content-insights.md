---
title: 內容分析
seo-title: Content Insight
description: Content Insight使用Web分析和SEO建議提供有關頁面效能的資訊
seo-description: Content Insight provides information about page performance using web analytics and SEO recommendation
uuid: 32f5b37c-2a82-462a-9f0a-c19bed46e198
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 60f980fd-049e-43c1-8b5d-60a8279b357a
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 2%

---

# 內容分析{#content-insight}

Content Insight使用Web分析和SEO建議提供有關頁面效能的資訊。 使用Content Insight可就如何修改頁面做出決策，或瞭解以前的更改如何更改效能。 對於您所創作的每個頁面，您都可以開啟內容透視來分析該頁面。

![chlimage_1-311](assets/chlimage_1-311.png)

Content Insight頁面的佈局會更改，以適應您所使用設備的螢幕尺寸和方向。

## 報表資料

「內容透視」頁包括使用Adobe SiteCatalyst、Adobe Target、Adobe Social和BrightEdge資料的報告：

* SiteCatalyst:以下指標的報告可用：

   * 頁面視圖
   * 頁上花費的平均時間
   * 來源

* 目標：有關您的頁面包括優惠的促銷活動的報告。
* BrightEdge:頁面上的報告功能可提高頁面對搜索引擎的可見性，並建議應實施的功能。

請參閱 [開啟分析和Recommendations頁](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page)。

## 報告期

報表顯示您控制的一段時間的資料。 在調整報告期間時，報表會自動刷新該期間的資料。 視覺提示指示頁面版本更改的時間，以便您可以比較每個版本的效能。

您還可以指定報告資料的粒度，例如，您可以查看每日、每週、每月或每年的資料。

請參閱 [更改報告期](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period)。

>[!NOTE]
>
>Content Insights報告要求您的管理員已AEM與SiteCatalyst、目標和BrightEdge整合。 請參閱 [與SightCatalyst整合](/help/sites-administering/adobeanalytics.md)。 [與Adobe Target整合](/help/sites-administering/target.md), [與BrightEdge整合](/help/sites-administering/brightedge.md)。

## 視圖報告 {#the-views-report}

「視圖」報告包含以下用於評估頁面流量的功能：

* 報告期間某頁的視圖總數。
* 報告期內視圖數的圖表：

   * 視圖總數。
   * 獨特的儲存器。

![chlimage_1-312](assets/chlimage_1-312.png)

## 頁面平均已參與報告 {#the-page-average-engaged-report}

「Page Average Engabed 」報告包含以下用於評估頁面有效性的功能：

* 整個報告期間頁面保持開啟的平均時間。
* 整個報告期間頁面視圖的平均長度的圖表。

![chlimage_1-313](assets/chlimage_1-313.png)

## 源報告 {#the-sources-report}

「源」報告指示用戶如何從搜索引擎結果或使用已知URL導航到該頁。

![chlimage_1-314](assets/chlimage_1-314.png)

## 跳躍報告 {#the-bounces-report}

「退貨」報表包含一個圖表，該圖表顯示在所選報告期間內某頁發生的退貨數。

![chlimage_1-315](assets/chlimage_1-315.png)

## 市場活動報表 {#the-campaign-activity-report}

對於頁面處於活動狀態的每個市場活動，都會顯示一個名為 *市場活動名稱* 活動。 此報表顯示為其提供優惠的每個段的頁面印象和轉換。

![chlimage_1-316](assets/chlimage_1-316.png)

## 徐Recommendations報導 {#the-seo-recommendations-report}

SEORecommendations報告包含該頁面的BrightEdge分析結果。 報告是頁面功能的核對表，它指示頁面包含哪些功能，但不包括哪些功能，以使用搜索引擎最大化查找性。

報告使您能夠建立任務，以便改進頁面查找能力。 Recommendations指出，已經為執行該建議而制定了任務。 請參閱 [為SEORecommendations分配任務](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations)。

![chlimage_1-317](assets/chlimage_1-317.png)
