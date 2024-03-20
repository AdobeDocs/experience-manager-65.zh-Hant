---
title: 搜尋
description: AEM的製作環境提供多種搜尋內容的機制，視資源型別而定。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# 搜尋{#searching}

AEM的製作環境提供多種搜尋內容的機制，視資源型別而定。

>[!NOTE]
>
>在製作環境之外，也提供其他機制可供搜尋，例如 [查詢產生器](/help/sites-developing/querybuilder-api.md) 和 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## 搜尋基本資訊 {#search-basics}

若要存取搜尋面板，請按一下 **搜尋** 標籤顯示在適當主控台的左窗格頂端。

![chlimage_1-101](assets/chlimage_1-101.png)

搜尋面板可讓您搜尋所有網站頁面。 它包含下列欄位和Widget：

* **全文**：搜尋指定的文字
* **修改於以下日期之後/之前**：僅搜尋在特定日期之間變更的頁面
* **範本**：僅根據指定的範本搜尋這些頁面
* **標籤**：僅搜尋具有指定標籤的頁面

>[!NOTE]
>
>當您的執行個體設定為 [Lucene搜尋](/help/sites-deploying/queries-and-indexing.md) 您可在以下中使用 **全文**：
>
>* [萬用字元](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [布林運運算元](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [規則運算式](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [欄位分組](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [提升](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>

按一下以執行搜尋 **搜尋** 位於窗格底部。 按一下 **重設** 以清除搜尋條件。

## 篩選條件 {#filter}

您可以在不同的位置設定（和清除）篩選器，以向下鑽研並調整您的檢視：

![chlimage_1-102](assets/chlimage_1-102.png)

## 尋找並取代 {#find-and-replace}

在 **網站** 主控台a **尋找和取代** 功能表選項可讓您在網站的某個區段中搜尋及取代字串的多個執行個體。

1. 選取您要執行尋找和取代動作的根頁面或資料夾。
1. 選取 **工具** 則 **尋找和取代**：

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. 此 **尋找和取代** 對話方塊會執行下列動作：

   * 確認尋找動作應該開始的根路徑
   * 定義要找到的字詞
   * 定義應取代它的字詞
   * 指出搜尋是否應區分大小寫
   * 指示是否只應找到全字（否則也會找到子字串）

   按一下 **預覽** 列出辭彙的發現位置。 您可以選取/清除要取代的特定執行個體：

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. 按一下 **取代** 以實際取代所有例項。 系統會要求您確認此動作。

尋找和取代servlet的預設範圍涵蓋下列屬性：

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

可使用Apache Felix Web管理主控台(例如 `https://localhost:4502/system/console/configMgr`)。 選取 `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` 並視需要設定範圍。

>[!NOTE]
>
>在標準AEM安裝中，「尋找和取代」會使用Lucene來搜尋功能。
>
>Lucene索引長度最多16k的字串屬性。 超出此範圍的字串將不會被搜尋。
