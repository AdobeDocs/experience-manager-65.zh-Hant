---
title: 進階計分和徽章
seo-title: 進階計分和徽章
description: 設定進階計分
seo-description: 設定進階計分
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 1%

---


# 進階計分與徽章{#advanced-scoring-and-badges}

## 概覽 {#overview}

進階評分可授予徽章，以識別會員為專家。 進階計分會根據成員建立之內容的數量&#x200B;*和*&#x200B;品質來指派點數，而基本計分則只會根據建立之內容的數量來指派點數。

此差異是由於用來計算分數的計分引擎所致。 基本計分引擎採用簡單數學。 進階計分引擎是一種自適應算法，可獎勵通過主題的自然語言處理(NLP)推導而貢獻有價值和相關內容的主動成員。

除了內容相關性外，計分演算法也會考量成員活動，例如投票和答案百分比。 雖然基本計分包括了定量計分，但進階計分則採用演算法。

因此，先進的計分引擎需要足夠的資料，使分析具有意義。 隨著演算法不斷調整所建立內容的量與品質，成為專家的成就臨界值會不斷重新評估。 成員的較舊員額也有&#x200B;*decay*&#x200B;的概念。 如果專家成員停止參與獲得專家地位的主題，在某個預先確定的點（見[計分引擎配置](#configurable-scoring-engine)），他們可能失去其專家地位。

設定進階計分與基本計分幾乎相同：

* 基本和進階計分和標籤規則以相同方式套用至內容](/help/communities/implementing-scoring.md#apply-rules-to-content)。[

   * 基本和進階計分和標籤規則可套用至相同內容。

* [為元件啟用標](/help/communities/implementing-scoring.md#enable-badges-for-component) 章，通用。

在設定計分和標籤規則方面的差異為：

* 可設定的進階計分引擎
* 進階計分規則：

   * `scoringType` 設定為  `advanced`
   * 需要 `stopwords`

* 進階標籤規則：

   * `badgingType` 設定為  `advanced`
   * `badgingLevels` 設定為 **要授予的專家級數**
   * 需要`badgingPaths`陣列標籤，而不是閾值陣列映射點到標籤。

>[!NOTE]
>
>若要使用進階計分和標籤功能，請安裝[Expert Identification套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)。

## 可配置計分引擎{#configurable-scoring-engine}

進階計分引擎提供OSGi組態，其參數會影響進階計分演算法。

![進階計分引擎](assets/advanced-scoring-engine.png)

* **評分權重**

   對於主題，請指定計算分數時應給予最高優先順序的動詞。 可以輸入一個或多個主題，但限制為每個主題&#x200B;**一個動詞**。 請參閱[主題和動詞](/help/communities/implementing-scoring.md#topics-and-verbs)。
輸入為`topic,verb`，逗號已逸出。 例如：
   `/social/forum/hbs/social/forum\,ADD`
對於QnA和論壇元件，預設設定為ADD動詞。

* **計分範圍**

   進階分數的範圍由此值（最大可能分數）和0（最低可能分數）定義。

   預設值為100，因此計分範圍為0-100。

* **實體衰減時間間隔**

   此參數代表所有實體分數在其後延遲的小時數。 您必須在社群網站的分數中不再包含舊內容。

   預設值為216000小時（~24年）。

* **評分增**
長率這會指定0與評分範圍之間的分數，超過此分數，增長會放緩，以限制專家人數。

   預設值為 50。

## 進階計分規則{#advanced-scoring-rules}

在基本評分中，獲得徽章所需的數量是已知的。

在進階計分中，需要的量是根據系統內的質量資料量不斷調整。 計分會以類似鐘形曲線的方式持續計算。

如果會員在已不活躍的主題上獲得專家徽章，他們可能會因為時間的流逝而失去徽章。

### scoringType {#scoringtype}

計分規則是一組計分子規則，每個子規則都聲明`scoringType`。

要調用高級計分引擎，`scoringType`應設定為`advanced`。

請參閱[計分子規則](/help/communities/implementing-scoring.md#scoring-sub-rules)。

![進階計分類型](assets/advanced-scoring-type.png)

### 秒字{#stopwords}

進階計分套件會安裝組態資料夾，其中包含秒數檔案：

* `/libs/settings/community/scoring/configuration/stopwords`

進階計分演算法使用秒字檔案中包含的字詞清單，以識別在內容處理期間忽略的常見英文字詞。

您不希望修改此檔案。

如果秒數檔案遺失，進階計分引擎將會擲回錯誤。

## 進階標籤規則{#advanced-badging-rules}

高級標籤規則屬性與[基本標籤規則屬性](/help/communities/implementing-scoring.md#badging-rules)不同。

與其將點與徽章影像建立關聯，您只需識別允許的專家人數和要授予的徽章影像。

![advanced-badging-rules](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>類型</th>
   <th>值說明</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>String[]</td>
   <td><em>（必要）</em> 徽章影像的多值字串，最多可達badgingLevels的數目。標章影像路徑必須依順序排列，因此第一個路徑會授與最高專家。 如果標籤數少於badgingLevels所指示的標籤數，則陣列中的最後一個標籤將填充陣列的其餘部分。 範例項目：<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>長整數</td>
   <td><em>（可選）指</em> 定要授予的專業知識級別。例如，如果應該有<code>expert </code>和<code>almost expert</code>（兩個標章），則值應設為2。 badgingLevel應與badgingPath屬性所列的專家相關標章影像數目相對應。 預設值為1。</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>字串</td>
   <td><em>（必要）</em> 將計分引擎識別為「基本」或「進階」。設為「進階」，則預設為「基本」。</td>
  </tr>
  <tr>
   <td>計分規則</td>
   <td>字串[]</td>
   <td><em>（可選）</em> 多值字串，將標籤規則限制為由列出的分數規則所識別的分數事件。<br /> 範例項目：<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> 預設值不受限制。</td>
  </tr>
 </tbody>
</table>

## 包含的規則和徽章{#included-rules-and-badge}

### 包含的徽章{#included-badge}

本測試版包含一個獎勵型專家徽章：

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![專家徽章](assets/included-badge.png)

要讓專家徽章顯示為活動的獎勵，請確定：

* `Badges` 已針對功能啟用，例如論壇或QnA元件。

* 進階計分和標籤規則會套用至放置元件的頁面（或上階）

請參閱以下內容的基本資訊：

* [啟用元件徽章](/help/communities/implementing-scoring.md#enableforcomponent)
* [套用規則](/help/communities/implementing-scoring.md#applytopage)

### 包含計分規則和子規則{#included-scoring-rules-and-sub-rules}

測試版包含[論壇函式](/help/communities/functions.md#forum-function)的兩個進階計分規則（每個用於論壇和論壇功能的注釋元件）:

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**附註:**

* `rules`和`sub-rules`節點都屬於`cq:Page`類型。

* `subRules` 是規則節點類[] 型「字串」的屬 `jcr:content` 性。

* `sub-rules` 可能會在各種計分規則之間共用。

* `rules` 應位於具有每個人讀取權限的儲存庫位置。

* 規則名稱必須是唯一的，無論位置為何。

### 包含的標籤規則{#included-badging-rules}

此發行包含兩個與[進階論壇和留言計分規則](#included-scoring-rules-and-sub-rules)對應的進階標籤規則。

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**附註:**

* `rules` 節點的類型為cq:Page。
* `rules` 應位於具有每個人讀取權限的儲存庫位置。
* 規則名稱必須是唯一的，無論位置為何。

