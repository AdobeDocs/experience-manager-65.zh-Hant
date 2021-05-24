---
title: 搜尋
seo-title: 搜尋
description: AEM的製作環境提供多種搜尋內容的機制，視資源類型而定。
seo-description: AEM的製作環境提供多種搜尋內容的機制，視資源類型而定。
uuid: 6dd3df4d-6040-4230-8373-fc028687b675
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8d32960c-47c3-4e92-b02e-ad4d8fea7b2d
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# 搜尋{#searching}

AEM的製作環境提供多種搜尋內容的機制，視資源類型而定。

>[!NOTE]
>
>在製作環境之外，也提供其他搜尋機制，例如[查詢產生器](/help/sites-developing/querybuilder-api.md)和[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。

## 搜索基本知識{#search-basics}

要訪問搜索面板，請按一下相應控制台左窗格頂部的&#x200B;**Search**&#x200B;頁簽。

![chlimage_1-101](assets/chlimage_1-101.png)

「搜尋」面板可讓您在所有網站頁面上進行搜尋。 它包含下列項目的欄位和小工具：

* **全文**:搜索指定的文本
* **在**&#x200B;之後/之前修改：僅搜尋在特定日期之間變更的頁面
* **範本**:僅根據指定的範本搜尋那些頁面
* **標籤**:僅搜尋具有指定標籤的頁面

>[!NOTE]
>
>為[Lucene搜尋](/help/sites-deploying/queries-and-indexing.md)設定執行個體時，您可以在&#x200B;**Fulltext**&#x200B;中使用下列內容：
>
>* [萬用字元](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [布林運算子](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)

   >
   >
* [規則運算式](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [欄位分組](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [Boosting](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)

>



按一下窗格底部的&#x200B;**Search**&#x200B;執行搜索。 按一下&#x200B;**重設**&#x200B;以清除搜尋條件。

## 篩選 {#filter}

在各種位置，可設定（並清除）篩選器，以深入鑽研並調整檢視：

![chlimage_1-102](assets/chlimage_1-102.png)

## 查找和替換{#find-and-replace}

在&#x200B;**網站**&#x200B;主控台中， **尋找和取代**&#x200B;功能表選項可讓您在網站的某個區段內搜尋和取代字串的多個例項。

1. 選擇根頁面或資料夾，以在其中執行查找和替換操作。
1. 依次選擇&#x200B;**工具**&#x200B;和&#x200B;**查找和替換**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. **查找和替換**&#x200B;對話框執行以下操作：

   * 確認尋找動作應從哪個根路徑開始
   * 定義要找到的詞
   * 定義應替代該詞的術語
   * 指出搜尋是否應區分大小寫
   * 指示是否只應找到整字（否則也找到子字串）

   按一下&#x200B;**預覽**&#x200B;列出找到詞語的位置。 您可以選取/清除要取代的特定例項：

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. 按一下&#x200B;**Replace**&#x200B;以實際取代所有例項。 系統會要求您確認動作。

查找和替換servlet的預設範圍涵蓋以下屬性：

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

範圍可使用Apache Felix Web Management Console（例如`https://localhost:4502/system/console/configMgr`）來變更。 選擇`CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)`並根據需要配置範圍。

>[!NOTE]
>
>在標準AEM安裝中，「尋找和取代」會使用Lucene來執行搜尋功能。
>
>Lucene索引長度多達16k的字串屬性。 系統不會搜尋超出此範圍的字串。
