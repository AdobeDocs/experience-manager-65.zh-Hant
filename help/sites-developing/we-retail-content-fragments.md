---
title: 在We.Retail中試用內容片段
description: 瞭解如何使用We.Retail在Adobe Experience Manager中試用內容片段。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments,Developing
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---

# 在We.Retail中試用內容片段{#trying-out-content-fragments-in-we-retail}

內容片段可讓您建立頻道中性內容，以及各種（頻道特定的）變化。 **We.Retail** (可在Adobe Experience Manager的現成執行個體中使用)提供Lofoten中的&#x200B;**Arctic Surfing**&#x200B;片段作為基本範例。 這說明：

* Adobe Experience Manager (AEM)內容片段是[建立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。 它們可讓您建立管道中性內容，連同（可能特定於管道）變數。

   * 檢視[在We.Retail中尋找內容片段資產的位置](#where-to-find-content-fragments-in-we-retail)

* 然後，您就可以[在編寫內容頁面時](/help/sites-authoring/content-fragments.md)使用這些片段及其變數。

   * 檢視[在We.Retail中使用內容片段的位置](#where-content-fragments-are-used-in-we-retail)

如需建立、管理、使用和開發內容片段的完整檔案：

* 檢視[進一步資訊](#further-information)

>[!NOTE]
>
>**內容片段**&#x200B;和&#x200B;**[體驗片段](/help/sites-authoring/experience-fragments.md)**&#x200B;是AEM中的不同功能：
>
>* **內容片段**&#x200B;是可編輯內容，主要為文字和相關影像。 它們是純內容，沒有設計和配置。
>* **體驗片段**&#x200B;是完整佈局的內容；網頁的片段。
>
>體驗片段可以包含內容片段形式的內容，反之則不行。

## 在We.Retail中尋找內容片段的位置 {#where-to-find-content-fragments-in-we-retail}

We.Retail中有數個範例內容片段；透過&#x200B;**Assets**、**檔案**、**We.Retail**、**英文**、**體驗**&#x200B;導覽。

其中包括&#x200B;**Lofoten的Arctic Surfing**，片段以及相關視覺資產：

* 透過&#x200B;**Assets**，**檔案**，**We.Retail**，**英文**，**體驗**，**在Lofoten的北極衝浪**：

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

您可以選取並編輯Lofoten **片段中的**&#x200B;北極衝浪：

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

在這裡，您可以使用標籤（左側面板） [編輯和管理](/help/assets/content-fragments/content-fragments.md)您的片段：

<!--![cf-45-aa](do-not-localize/cf-45-aa.png) ![cf-45-a](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[變數](/help/assets/content-fragments/content-fragments-variations.md)**&#x200B;包含[Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[相關聯的內容](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[中繼資料](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## 在We.Retail中使用內容片段的位置 {#where-content-fragments-are-used-in-we-retail}

為了說明使用內容片段[&#128279;](/help/sites-authoring/content-fragments.md)進行頁面製作，下面提供了幾個範例頁面，例如：

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

例如，Lofoten **中的** Arctic Surfing內容片段已在Sites頁面中參照：

* 透過&#x200B;**網站**、**We.Retail**、**語言主版**、**英文**、**體驗**&#x200B;進行瀏覽。 接著在Lofoten **開啟** Arctic Surfing進行編輯：

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 更多資訊 {#further-information}

如需詳細資訊，請參閱：

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)

   * 瞭解如何建立、編輯及管理您的內容片段資產。

* [使用內容片段編寫頁面](/help/sites-authoring/content-fragments.md)

   * 編寫頁面時使用您的內容片段。

* [開發AEM — 內容片段的元件](/help/sites-developing/components-content-fragments.md)

   * 內容片段元件的概觀。

* [開發和擴充內容片段](/help/sites-developing/customizing-content-fragments.md)

   * 可協助您開發及擴充內容片段的資訊。
