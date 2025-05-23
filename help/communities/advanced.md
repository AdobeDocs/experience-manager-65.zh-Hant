---
title: 進階評分和徽章
description: 瞭解如何設定進階分數，以便允許獎勵徽章以將成員識別為專家。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 1%

---

# 進階評分和徽章{#advanced-scoring-and-badges}

## 概觀 {#overview}

進階評分可授予徽章，將成員識別為專家。 進階評分會根據成員建立的內容數量&#x200B;*和*&#x200B;品質指派點數，而基本評分則會根據建立的內容數量指派點數。

此差異是因為用於計算分數的評分引擎。 基本的評分引擎會套用簡單的數學。 進階評分引擎是一種自我調整演演算法，可獎勵透過主題的自然語言處理(NLP)推斷出的貢獻有價值和相關內容的活躍成員。

除了內容關聯性之外，評分演演算法也會考慮成員活動，例如投票和回答百分比。 雖然基本評分會以量化方式納入量度，但進階評分會以演演算法方式使用這些量度。

因此，進階評分引擎需要足夠的資料，才能讓分析有意義。 當演演算法持續調整以符合所建立內容的數量和品質時，系統會持續重新評估成為專家的成就門檻。 成員較舊的貼文也有&#x200B;*衰減*&#x200B;的概念。 如果專家成員停止參與他們獲得專家地位的主題，在某個預先確定的時間點（請參閱[評分引擎組態](#configurable-scoring-engine)），他們可能會失去其專家地位。

設定進階評分與基本評分幾乎相同：

* 基本和進階評分與徽章規則是以相同方式套用至內容[&#128279;](/help/communities/implementing-scoring.md#apply-rules-to-content)。

   * 基本和進階評分和徽章規則可套用至相同內容。

* [啟用元件](/help/communities/implementing-scoring.md#enable-badges-for-component)的徽章是通用的。

設定評分和徽章規則的差異如下：

* 可設定的進階評分引擎
* 進階評分規則：

   * `scoringType`已設定為`advanced`
   * 需要`stopwords`

* 進階徽章規則：

   * `badgingType`已設定為`advanced`
   * `badgingLevels`設定為&#x200B;**要獎勵的專家層級數目**
   * 需要`badgingPaths`個徽章陣列，而不是臨界值陣列對應點到徽章。

>[!NOTE]
>
>若要使用進階評分與徽章功能，請安裝[專家識別套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg)。

## 可設定的評分引擎 {#configurable-scoring-engine}

進階評分引擎提供OSGi設定，其中包含影響進階評分演演算法的引數。

![進階評分引擎](assets/advanced-scoring-engine.png)

* **評分權重**

  對於主題，請指定計算分數時，應給予最高優先順序的動詞。 可以輸入一或多個主題，但限製為每個主題&#x200B;**一個**&#x200B;動詞。 檢視[主題和動詞](/help/communities/implementing-scoring.md#topics-and-verbs)。
輸入為`topic,verb`，逗號逸出。 例如：
  `/social/forum/hbs/social/forum\,ADD`
QnA和論壇元件的預設值設為ADD動詞。

* **評分範圍**

  進階分數的範圍是透過此值（最高分數）和0 （最低分數）來定義。

  預設值為100，因此評分範圍為0至100。

* **實體衰減時間間隔**

  此引數代表所有實體分數都經過衰減的小時數。 此為必要操作，不能再將舊內容納入社群網站的分數中。

  預設值為216000小時（~24年）。

* **評分成長率**
這會指定介於0分數範圍之間的分數，超過該分數範圍後，成長速度會減慢，以限制專家數量。

  預設值為 50。

## 進階評分規則 {#advanced-scoring-rules}

在基本評分中，獲得徽章所需的數量是已知的。

在進階評分中，所需的數量會根據系統內的品質資料量持續調整。 評分會以類似鈴鐺曲線的方式持續計算。

如果成員在已不活躍的主題上獲得專家徽章，則他們可能會因為隨著時間衰減而失去徽章。

### scoringType {#scoringtype}

評分規則是一組評分子規則，每個子規則都會宣告`scoringType`。

若要叫用進階評分引擎，`scoringType`應設為`advanced`。

請參閱[評分子規則](/help/communities/implementing-scoring.md#scoring-sub-rules)。

![進階評分型別](assets/advanced-scoring-type.png)

### 停用詞 {#stopwords}

進階評分套件會安裝包含停用字檔案的設定資料夾：

* `/libs/settings/community/scoring/configuration/stopwords`

進階評分演演算法會使用停用字詞檔案中包含的字詞清單，來識別在內容處理期間被忽略的常見英文字詞。

預期不會修改此檔案。

如果遺失停用詞檔案，進階評分引擎會產生錯誤。

## 進階徽章規則 {#advanced-badging-rules}

進階徽章規則屬性與[基本徽章規則屬性](/help/communities/implementing-scoring.md#badging-rules)不同。

不必將點與徽章影像相關聯，只需識別允許的專家人數以及要獎勵的徽章影像。

![advanced-badging-rules](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>類型</th>
   <th>值說明</th>
  </tr>
  <tr>
   <td>badgingpath</td>
   <td>String[]</td>
   <td><em>（必要）</em>徽章影像的多值字串，最多badgingLevels的數目。 徽章影像路徑必須排序，才能將第一個授予最高的專家。 如果徽章數少於badgingLevels所指示的數目，則陣列中的最後一個徽章會填滿陣列的其餘部分。 範例專案：<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>長</td>
   <td><em>（選擇性）</em>指定要授與的專業知識等級。 例如，如果應該有<code>expert </code>和<code>almost expert</code> （兩個徽章），則值應該設定為2。 badgingLevel應該與badgingPath屬性所列的專家相關徽章影像數量相對應。 預設值為1。</td>
  </tr>
  <tr>
   <td>badgingtype</td>
   <td>字串</td>
   <td><em>（必要）</em>將評分引擎識別為「基本」或「進階」。 設為「進階」，否則預設為「基本」。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String[]</td>
   <td><em>（選擇性）</em>多值字串，可將徽章規則限製為由列出的一或多個評分規則所識別的評分事件。<br />範例專案： <br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br />預設為無限制。</td>
  </tr>
 </tbody>
</table>

## 包含的規則和徽章 {#included-rules-and-badge}

### 包含的徽章 {#included-badge}

此Beta版包含一枚獎勵型專家徽章：

* `expert`

  `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![專家徽章](assets/included-badge.png)

若要讓專家徽章顯示為活動的獎勵，請確定：

* 已針對功能（例如論壇或QnA元件）啟用`Badges`。

* 進階評分和徽章規則會套用至放置元件的頁面（或上階）

請參閱下列專案的基本資訊：

* [啟用元件的徽章](/help/communities/implementing-scoring.md#enableforcomponent)
* [套用規則](/help/communities/implementing-scoring.md#applytopage)

### 包含評分規則和子規則 {#included-scoring-rules-and-sub-rules}

測試版包含了[論壇功能](/help/communities/functions.md#forum-function)的兩個進階評分規則（論壇功能的論壇和評論元件各一個）：

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule
   ```

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   ```

**附註：**

* `rules`和`sub-rules`節點都是型別`cq:Page`。
* `subRules`是規則`jcr:content`節點上型別為String`[]`的屬性。
* `sub-rules`可以在各種評分規則之間共用。
* `rules`應該位於儲存庫位置，且每個人都有讀取許可權。
* 無論位置為何，規則名稱必須是唯一的。

### 包含的徽章規則 {#included-badging-rules}

發行中包含兩個進階徽章規則，對應至[進階論壇和評論評分規則](#included-scoring-rules-and-sub-rules)。

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**附註：**

* `rules`節點的型別為cq：Page。
* `rules`應該位於儲存庫位置，且每個人都有讀取許可權。
* 無論位置為何，規則名稱必須是唯一的。
