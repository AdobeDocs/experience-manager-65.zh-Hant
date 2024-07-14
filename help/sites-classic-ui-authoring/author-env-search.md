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
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# 搜尋{#searching}

AEM的製作環境提供多種搜尋內容的機制，視資源型別而定。

>[!NOTE]
>
>在作者環境之外，也可以使用其他機制來搜尋，例如[查詢產生器](/help/sites-developing/querybuilder-api.md)和[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。

## 搜尋基本資訊 {#search-basics}

若要存取搜尋面板，請按一下適當主控台左窗格頂端的&#x200B;**搜尋**&#x200B;標籤。

![chlimage_1-101](assets/chlimage_1-101.png)

搜尋面板可讓您搜尋所有網站頁面。 它包含下列欄位和Widget：

* **全文**：搜尋指定的文字
* **修改於**&#x200B;之後/之前：僅搜尋在特定日期之間變更的頁面
* **範本**：僅搜尋那些以指定範本為基礎的頁面
* **標籤**：僅搜尋具有指定標籤的頁面

>[!NOTE]
>
>當您的執行個體設定為[Lucene搜尋](/help/sites-deploying/queries-and-indexing.md)時，您可以在&#x200B;**全文**&#x200B;中使用下列專案：
>
>* [萬用字元](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [布林運運算元](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [規則運算式](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [欄位分組](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [提升](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>

按一下窗格底部的&#x200B;**搜尋**&#x200B;以執行搜尋。 按一下&#x200B;**重設**&#x200B;以清除搜尋條件。

## 篩選條件 {#filter}

您可以在不同的位置設定（和清除）篩選器，以向下鑽研並調整您的檢視：

![chlimage_1-102](assets/chlimage_1-102.png)

## 尋找並取代 {#find-and-replace}

在&#x200B;**網站**&#x200B;主控台中，**尋找和取代**&#x200B;功能表選項可讓您搜尋和取代網站某區段中字串的多個執行個體。

1. 選取您要執行尋找和取代動作的根頁面或資料夾。
1. 選取&#x200B;**工具**&#x200B;然後&#x200B;**尋找與取代**：

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. **尋找和取代**&#x200B;對話方塊會執行下列動作：

   * 確認尋找動作應該開始的根路徑
   * 定義要找到的字詞
   * 定義應取代它的字詞
   * 指出搜尋是否應區分大小寫
   * 指示是否只應找到全字（否則也會找到子字串）

   按一下&#x200B;**預覽**&#x200B;列出找到辭彙的清單。 您可以選取/清除要取代的特定執行個體：

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. 按一下[取代]以實際取代所有執行個體。 ****&#x200B;系統會要求您確認此動作。

尋找和取代servlet的預設範圍涵蓋下列屬性：

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

可以使用Apache Felix Web管理主控台（例如，`https://localhost:4502/system/console/configMgr`）變更範圍。 選取`CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)`並視需要設定範圍。

>[!NOTE]
>
>在標準AEM安裝中，「尋找和取代」會使用Lucene來搜尋功能。
>
>Lucene索引長度最多16k的字串屬性。 超出此範圍的字串將不會被搜尋。
