---
title: 在We.Retail中試用內容片段
seo-title: 在We.Retail中試用內容片段
description: 'null'
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: 759d2dd8d12861757bf7f54b77d8d3ca170887fe
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 4%

---


# 在We.Retail中試用內容片段{#trying-out-content-fragments-in-we-retail}

內容片段可讓您建立不受通道影響的內容，以及（可能是特定通道的）變化。 **We.Retail** （如AEM的現成可用例項所提供）提供了Lofotenas的殘片 **Arctic Surfing** （北極衝浪）。這說明：

* Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。它們可讓您建立不受頻道影響的內容，以及（可能是特定頻道的）變化。

   * 請參閱We.Retail](#where-to-find-content-fragments-in-we-retail)中的[尋找內容片段資產的位置

* 然後，在編寫內容頁面時，您可以[使用這些片段及其變化。](/help/sites-authoring/content-fragments.md)

   * 請參閱[Where Content Fragments are Used in We.Retail](#where-content-fragments-are-used-in-we-retail)

有關建立、管理、使用和開發內容片段的完整檔案：

* 請參閱[詳細資訊](#further-information)

>[!NOTE]
>
>**內容** 片段和 **[體驗](/help/sites-authoring/experience-fragments.md)** 片段是AEM中的不同功能：
>
>* **內容** 片段是編輯內容，主要是文字和相關影像。它們是純粹的內容，不需要設計和版面配置。
>* **體驗** 片段內容已完整排版；網頁的片段。

>
>
「體驗片段」可以包含內容片段的形式，但不能以相反的方式包含。

## 在We.Retail {#where-to-find-content-fragments-in-we-retail}中尋找內容片段的位置

We.Retail中有數個範例內容片段；透過&#x200B;**Assets**、**Files**、**We.Retail**、**English**、**Experiences**&#x200B;導覽。

這包括Lofoten的&#x200B;**北極衝浪片段以及相關的視覺資產：**

* 透過&#x200B;**Assets**、**Files**、**We.Retail**、**English**、**Experiences**、**Lofoten的Artic Surfing瀏覽導覽：**

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

您可以選擇並編輯&#x200B;**Ractic Surfing in Lofoten**&#x200B;片段：

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

在這裡，您可以使用標籤（左側面板）來編輯和管理片段：[](/help/assets/content-fragments/content-fragments.md)

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[變](/help/assets/content-fragments/content-fragments-variations.md)** 數，包括 [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[相關聯的內容](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[中繼資料](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## We.Retail {#where-content-fragments-are-used-in-we-retail}中使用內容片段的位置

為了說明使用內容片段[製作頁面的方式，以下列幾個範例頁面提供：](/help/sites-authoring/content-fragments.md)

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

例如，Lofoten **中的** Arctic Surfing內容片段在「網站」頁面中參考：

* 透過&#x200B;**Sites**、**We.Retail**、**語言碩士**、**英文**、**Experience**&#x200B;導覽。 然後開啟&#x200B;**Ractic Surfing in Lofoten**&#x200B;進行編輯：

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 更多資訊 {#further-information}

如需詳細資訊，請參閱：

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)

   * 瞭解如何建立、編輯和管理您的內容片段資產。

* [使用內容片段製作頁面](/help/sites-authoring/content-fragments.md)

   * 在編寫頁面時使用您的內容片段。

* [開發AEM —— 內容片段的元件](/help/sites-developing/components-content-fragments.md)

   * 內容片段的元件概觀。

* [開發和擴充內容片段](/help/sites-developing/customizing-content-fragments.md)

   * 協助您開發和擴充內容片段的資訊。

