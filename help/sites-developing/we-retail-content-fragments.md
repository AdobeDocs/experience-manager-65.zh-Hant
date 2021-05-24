---
title: 在We.Retail中嘗試內容片段
seo-title: 在We.Retail中嘗試內容片段
description: 在We.Retail中嘗試內容片段
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 5%

---

# 在We.Retail{#trying-out-content-fragments-in-we-retail}中嘗試內容片段

內容片段可讓您建立管道中性內容，以及（可能是管道特定的）變化。 **We.Retail** (如AEM的現成可用例項中所示)提供Lofotenas中的 **北極衝** 浪片段作為基本範例。這說明：

* Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。它們可讓您建立管道中性內容，以及（可能是管道特定的）變化。

   * 請參閱[在We.Retail](#where-to-find-content-fragments-in-we-retail)中尋找內容片段資產的位置

* 然後，您可以在編寫內容頁面時](/help/sites-authoring/content-fragments.md)使用這些片段及其變化。[

   * 請參閱[其中We.Retail](#where-content-fragments-are-used-in-we-retail)中使用內容片段

如需建立、管理、使用和開發內容片段的完整檔案：

* 請參閱[更多資訊](#further-information)

>[!NOTE]
>
>**內容** 片段和 **[體驗](/help/sites-authoring/experience-fragments.md)** 片段是AEM內的不同功能：
>
>* **內容** 片段是編輯內容，主要是文字和相關影像。它們是純內容，沒有設計和佈局。
>* **體驗** 片段內容已完整規劃；網頁的片段。

>
>
體驗片段可以包含內容片段形式的內容，但不能以相反的方式。

## 在We.Retail {#where-to-find-content-fragments-in-we-retail}中尋找內容片段的位置

We.Retail中有數個範例內容片段；透過&#x200B;**Assets**、**Files**、**We.Retail**、**English**、**Experiences**&#x200B;導覽。

這些包括Lofoten的&#x200B;**北極衝浪**、片段以及相關的視覺資產：

* 透過&#x200B;**Assets**、**Files**、**We.Retail**、**English**、**Experiences**、**Lofoten**&#x200B;的Artic Surfing導覽：

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

您可以選擇並編輯Lofoten **中的**&#x200B;北極衝浪片段：

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

您可以在此使用標籤（左側面板）編輯和管理](/help/assets/content-fragments/content-fragments.md)您的片段：[

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[](/help/assets/content-fragments/content-fragments-variations.md)** 變數，包括 [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[相關聯的內容](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[中繼資料](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## 其中內容片段用於We.Retail {#where-content-fragments-are-used-in-we-retail}

為了說明使用內容片段](/help/sites-authoring/content-fragments.md)製作[頁面，下方提供數個範例頁面，例如：

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

例如，Lofoten **內容片段的**&#x200B;北極衝浪在「網站」頁面中參考：

* 透過&#x200B;**Sites**、**We.Retail**、**語言主版**、**英文版**、**Experience**&#x200B;導覽。 然後開啟&#x200B;**Lofoten的北極衝浪活動**&#x200B;進行編輯：

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 更多資訊 {#further-information}

如需更多詳細資訊，請參閱：

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)

   * 了解如何建立、編輯及管理您的內容片段資產。

* [使用內容片段進行頁面編寫](/help/sites-authoring/content-fragments.md)

   * 編寫頁面時，請使用您的內容片段。

* [開發AEM — 內容片段的元件](/help/sites-developing/components-content-fragments.md)

   * 內容片段元件的概觀。

* [開發和擴充內容片段](/help/sites-developing/customizing-content-fragments.md)

   * 可協助您開發及擴充內容片段的資訊。
