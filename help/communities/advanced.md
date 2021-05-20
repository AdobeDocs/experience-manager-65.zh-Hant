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
role: Administrator
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# 高級計分和徽章{#advanced-scoring-and-badges}

## 概覽 {#overview}

高級評分允許授予徽章以將成員標識為專家。 進階計分會根據成員建立的內容數量&#x200B;*和*&#x200B;質量來指派點數，而基本計分則僅根據建立的內容數量來指派點數。

此差異是因為用於計算分數的分數引擎。 基本計分引擎採用簡單的數學。 進階計分引擎是一種自適應算法，用於獎勵通過主題的自然語言處理(NLP)推導而貢獻有價值和相關內容的活躍成員。

除了內容相關性外，評分演算法也會考量成員活動，例如投票和答案的百分比。 雖然基本評分會定量地納入，但進階評分會以演算法方式使用。

因此，進階計分引擎需要足夠的資料，使分析有意義。 隨著演算法持續根據所建立內容的數量和品質進行調整，系統會持續重新評估成為專家的成就臨界值。 成員的較舊員額也有&#x200B;*decay*&#x200B;的概念。 如果專家成員停止參與他們獲得專家身份的主題，在某個預先確定的點（見[計分引擎配置](#configurable-scoring-engine)），他們可能失去其專家身份。

設定進階分數幾乎與基本分數相同：

* 基本和進階計分與徽章規則以相同方式套用至內容](/help/communities/implementing-scoring.md#apply-rules-to-content)。[

   * 基本和進階分數及徽章規則可套用至相同內容。

* [為元件啟用徽](/help/communities/implementing-scoring.md#enable-badges-for-component) 章，通用。

設定計分和徽章規則的差異為：

* 可配置的高級計分引擎
* 進階計分規則：

   * `scoringType` 設為  `advanced`
   * 需要 `stopwords`

* 進階簽章規則：

   * `badgingType` 設為  `advanced`
   * `badgingLevels` 設定為 **要授予的專家級數**
   * 需要`badgingPaths`徽章陣列，而非臨界值陣列映射點到徽章。

>[!NOTE]
>
>要使用高級計分和標籤功能，請安裝[專家身份識別包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)。

## 可配置計分引擎{#configurable-scoring-engine}

進階計分引擎提供OSGi設定，其中包含影響進階計分演算法的參數。

![進階分數引擎](assets/advanced-scoring-engine.png)

* **計分權重**

   對於主題，指定計算分數時應給予最高優先順序的動詞。 可以輸入一個或多個主題，但每個主題&#x200B;**限定為**&#x200B;一個動詞。 請參閱[主題和動詞](/help/communities/implementing-scoring.md#topics-and-verbs)。
以`topic,verb`輸入，逗號逸出。 例如：
   `/social/forum/hbs/social/forum\,ADD`
預設設定為QnA和論壇元件的ADD謂詞。

* **分數範圍**

   進階分數的範圍由此值（最大可能分數）和0（最小可能分數）定義。

   預設值為100，因此分數範圍為0-100。

* **實體耗散時間間隔**

   此參數代表所有實體分數被延遲的小時數。 這必須不再將舊內容納入社群網站的分數中。

   預設值為216000小時（~24年）。

* **計分增**
長率這指定0和計分範圍之間的分數，超過此範圍後增長會放緩以限制專家人數。

   預設值為 50。

## 高級計分規則{#advanced-scoring-rules}

在基本計分中，已知獲得徽章所需的數量。

在進階計分中，需要的數量會根據系統內的品質資料量不斷調整。 計分會以類似鐘形曲線的方式持續計算。

如果成員在已不活躍的主題上獲得了專家徽章，則他們可能會因時間流逝而失去其徽章。

### scoringType {#scoringtype}

計分規則是一組計分子規則，每個規則都聲明`scoringType`。

若要叫用進階計分引擎，`scoringType`應設為`advanced`。

請參閱[計分子規則](/help/communities/implementing-scoring.md#scoring-sub-rules)。

![advanced-scoring-type](assets/advanced-scoring-type.png)

### 停字 {#stopwords}

高級計分包會安裝包含秒數檔案的配置資料夾：

* `/libs/settings/community/scoring/configuration/stopwords`

進階計分演算法使用秒數檔案中包含的字詞清單，以識別內容處理期間會忽略的常見英文字詞。

不希望修改此檔案。

如果秒數檔案遺失，進階計分引擎會擲回錯誤。

## 高級簽名規則{#advanced-badging-rules}

高級簽名規則屬性與[基本簽名規則屬性](/help/communities/implementing-scoring.md#badging-rules)不同。

與其將點與徽章影像關聯，只需識別允許的專家數量和要獎勵的徽章影像即可。

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
   <td><em>（必要）</em> 徽章影像的多值字串，長度為badgingLevels數目。必須排序徽章影像路徑，以便將第一個路徑授予最高專家。 如果徽章數少於badgingLevels所指示的，陣列中的最後一個徽章會填滿陣列的其餘部分。 範例項目：<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>長整數</td>
   <td><em>（可選）</em> 指定要授予的專業水準。例如，如果應該有<code>expert </code>和<code>almost expert</code>（兩個徽章），則值應設為2。 badgingLevel應與為badgingPath屬性列出的專家相關徽章影像的數量相對應。 預設為1。</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>字串</td>
   <td><em>（必要）</em> 將計分引擎識別為「基本」或「進階」。若設為「進階」，則預設值為「basic」。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>字串[]</td>
   <td><em>（選用）</em> 多值字串，用於將標籤規則限制為對列出的分數規則所識別的事件評分。<br /> 範例項目： <br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> 預設為無限制。</td>
  </tr>
 </tbody>
</table>

## 包含的規則和徽章{#included-rules-and-badge}

### 包含的徽章{#included-badge}

此測試版包含一個獎勵型專家徽章：

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![專家徽章](assets/included-badge.png)

若要讓專家徽章顯示為活動的獎勵，請確定：

* `Badges` 為功能（如論壇或QnA元件）啟用。

* 進階計分和徽章規則會套用至放置元件的頁面（或上階）

請參閱以下項目的基本資訊：

* [啟用元件的徽章](/help/communities/implementing-scoring.md#enableforcomponent)
* [套用規則](/help/communities/implementing-scoring.md#applytopage)

### 包含計分規則和子規則{#included-scoring-rules-and-sub-rules}

測試版包含[論壇函式](/help/communities/functions.md#forum-function)的兩個進階計分規則（論壇和論壇功能的註解元件各一個）:

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

* `rules`和`sub-rules`節點都屬於類型`cq:Page`。

* `subRules` 是規則節點類[] 型字串的屬 `jcr:content` 性。

* `sub-rules` 可在各種計分規則之間共用。

* `rules` 應位於具有每個人讀取權限的存放庫位置。

* 規則名稱必須是唯一的，無論位置為何。

### 包含標籤規則{#included-badging-rules}

此發行包含兩個與[進階論壇和留言分數規則](#included-scoring-rules-and-sub-rules)對應的進階標籤規則。

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**附註:**

* `rules` 節點類型為cq:Page。
* `rules` 應位於具有每個人讀取權限的存放庫位置。
* 規則名稱必須是唯一的，無論位置為何。
