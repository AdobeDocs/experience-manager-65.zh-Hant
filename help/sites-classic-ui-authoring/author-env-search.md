---
title: 搜尋
seo-title: 搜尋
description: AEM的作者環境提供多種搜尋內容的機制，視資源類型而定。
seo-description: AEM的作者環境提供多種搜尋內容的機制，視資源類型而定。
uuid: 6dd3df4d-6040-4230-8373-fc028687b675
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8d32960c-47c3-4e92-b02e-ad4d8fea7b2d
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---


# 搜尋{#searching}

AEM的作者環境提供多種搜尋內容的機制，視資源類型而定。

>[!NOTE]
>
>在作者環境之外，也有其他機制可供搜尋，例如[查詢產生器](/help/sites-developing/querybuilder-api.md)和[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。

## 搜索基礎{#search-basics}

要訪問搜索面板，請按一下相應控制台左側窗格頂部的&#x200B;**Search**&#x200B;頁籤。

![chlimage_1-101](assets/chlimage_1-101.png)

搜尋面板可讓您搜尋所有網站頁面。 它包含下列欄位和Widget:

* **全文**:搜尋指定的文字
* **修改後／之前**:僅搜尋在特定日期之間變更的頁面
* **範本**:僅根據指定的範本搜尋這些頁面
* **標籤**:僅搜尋具有指定標籤的頁面

>[!NOTE]
>
>為[Lucene search](/help/sites-deploying/queries-and-indexing.md)配置實例時，您可以在&#x200B;**Fulltext**&#x200B;中使用以下內容：
>
>* [萬用字元](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [布林運算子](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)

   >
   >
* [規則運算式](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [欄位分組](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [Boosting](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)

>



按一下窗格底部的&#x200B;**Search**&#x200B;執行搜索。 按一下&#x200B;**Reset**&#x200B;以清除搜索標準。

## 篩選 {#filter}

您可以在不同位置設定（並清除）篩選器，以下列方式深入檢視並細化檢視：

![chlimage_1-102](assets/chlimage_1-102.png)

## 查找並替換{#find-and-replace}

在&#x200B;**Websites**&#x200B;主控台中，**尋找與取代**&#x200B;功能表選項可讓您在網站的某個區段內搜尋和取代字串的多個例項。

1. 選擇根頁面或資料夾，您希望在其中執行查找和替換操作。
1. 選擇&#x200B;**工具**，然後選擇&#x200B;**查找和替換**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. **尋找與取代**&#x200B;對話方塊執行下列動作：

   * 確認尋找動作應該開始的根路徑
   * 定義要找到的詞語
   * 定義應替換的詞語
   * 指出搜尋是否應區分大小寫
   * 指出是否只應找到整個字詞（否則也找到子字串）

   按一下&#x200B;**預覽**&#x200B;會列出找到詞語的位置。 您可以選擇／清除要替換的特定實例：

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. 按一下&#x200B;**Replace**&#x200B;以實際替換所有實例。 系統會要求您確認動作。

查找和替換servlet的預設範圍涵蓋以下屬性：

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

可使用Apache Felix Web Management Console（例如，在`https://localhost:4502/system/console/configMgr`）變更範圍。 選擇`CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)`並根據需要配置範圍。

>[!NOTE]
>
>在標準AEM安裝中，「尋找和取代」會使用Lucene來提供搜尋功能。
>
>Lucene索引長度高達16k的字串屬性。 超過此值的字串將不會被搜尋。
