---
title: 在We.Retail中嘗試內容片段
seo-title: Trying out Content Fragments in We.Retail
description: 在We.Retail中嘗試內容片段
seo-description: null
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 4%

---

# 在We.Retail中嘗試內容片段{#trying-out-content-fragments-in-we-retail}

內容片段允許您建立通道中性內容以及（可能特定於通道）變體。 **We.Retail** (在的出廠預裝實例中可AEM用) **洛福滕北極衝浪** 作為基本樣本。 這說明：

* Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。它們允許您建立通道中性內容以及（可能特定於通道）變體。

   * 請參閱 [在We.Retail中查找內容片段資產的位置](#where-to-find-content-fragments-in-we-retail)

* 你可以 [在創作時使用這些片段及其變體](/help/sites-authoring/content-fragments.md) 內容頁面。

   * 請參閱 [內容片段在We.Retail中的使用位置](#where-content-fragments-are-used-in-we-retail)

有關建立、管理、使用和開發內容片段的完整文檔：

* 請參閱 [詳細資訊](#further-information)

>[!NOTE]
>
>**內容片段** 和 **[體驗片段](/help/sites-authoring/experience-fragments.md)** 是內部的不同功AEM能：
>
>* **內容片段** 是編輯內容，主要是文本和相關影像。 它們是純內容，沒有設計和佈局。
>* **體驗片段** 內容全面，網頁的片段。
>
>體驗片段可以包含內容片段的形式，但不能以相反的方式。

## 在We.Retail中查找內容片段的位置 {#where-to-find-content-fragments-in-we-retail}

We.Retail中有幾個樣本內容片段；導航 **資產**。 **檔案**。 **We.Retail**。 **英語**。 **體驗**。

這些包括 **洛福滕北極衝浪**，片段以及相關的視覺資產：

* 導航 **資產**。 **檔案**。 **We.Retail**。 **英語**。 **體驗**。 **羅福滕的藝術衝浪**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![CF-44](assets/cf-44.png)

可以選擇和編輯 **洛福滕北極衝浪** 片段：

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

你可以 [編輯和管理](/help/assets/content-fragments/content-fragments.md) 使用制表符（左側面板）的片段：

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[變體](/help/assets/content-fragments/content-fragments-variations.md)** 包括 [馬爾克當](/help/assets/content-fragments/content-fragments-markdown.md)
* **[相關聯的內容](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[中繼資料](/help/assets/content-fragments/content-fragments-metadata.md)**

![CF-46](assets/cf-46.png)

## 內容片段在We.Retail中的使用位置 {#where-content-fragments-are-used-in-we-retail}

為了說明 [用內容片段創作頁面](/help/sites-authoring/content-fragments.md) 下面提供了幾個示例頁：

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

例如， **洛福滕北極衝浪** 「站點」頁中引用了內容片段：

* 導航 **站點**。 **We.Retail**。 **語言大師**。 **英語**。 **經驗**。 然後開啟 **洛福滕北極衝浪** 編輯：

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 更多資訊 {#further-information}

有關詳細資訊，請參閱：

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)

   * 瞭解如何建立、編輯和管理內容片段資產。

* [帶內容片段的頁面創作](/help/sites-authoring/content-fragments.md)

   * 創作頁面時使用內容片段。

* [開發AEM — 內容片段的元件](/help/sites-developing/components-content-fragments.md)

   * 內容片段元件概述。

* [內容片段的開發和擴展](/help/sites-developing/customizing-content-fragments.md)

   * 幫助您開發和擴展內容片段的資訊。
