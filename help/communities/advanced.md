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
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf

---


# 進階計分和徽章{#advanced-scoring-and-badges}

## 概覽 {#overview}

進階評分可授予徽章，以識別會員為專家。 進階計分會根據成員建立的 *內容數量* 和品質來指派點數，而基本計分則只會根據建立的內容數量來指派點數。

此差異是由於用來計算分數的計分引擎所致。 基本計分引擎採用簡單數學。 進階計分引擎是一種自適應算法，可獎勵通過主題的自然語言處理(NLP)推導而貢獻有價值和相關內容的主動成員。

除了內容相關性外，計分演算法也會考量成員活動，例如投票和答案百分比。 雖然基本計分包括了量化分數，但進階計分則採用演算法。

因此，先進的計分引擎需要足夠的資料，使分析具有意義。 隨著演算法不斷調整所建立內容的量與品質，成為專家的成就臨界值會不斷重新評估。 還有一個概念 *是* ，成員的舊職位會衰落。 如果專家成員停止參與獲得專家地位的主題，在某個預先確定的點(請參閱計分引擎配置 [](#configurable-scoring-engine))，他們可能失去專家的地位。

設定進階計分與基本計分幾乎相同：

* 基本和進階計分與標籤規則 [會以相同方式套用](/help/communities/implementing-scoring.md#apply-rules-to-content) 至內容

   * 基本和進階計分與標籤規則可套用至相同內容

* [為元件啟用標章](/help/communities/implementing-scoring.md#enable-badges-for-component) ，是通用的

在設定計分和標籤規則方面的差異為：

* 可設定的進階計分引擎
* 進階計分規則：

   * `scoringType` 設定為 `advanced`
   * requires `stopwords`

* 進階標籤規則：

   * `badgingType` 設定為 `advanced`
   * `badgingLevels` 設定為 **要授予的專家級數**
   * 需要 `badgingPaths` 標籤陣列，而不是閾值陣列映射點到標籤

>[!NOTE]
>
>若要使用進階的計分和標籤功能，請安裝「專 [家識別」套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)。

## 可配置計分引擎 {#configurable-scoring-engine}

進階計分引擎提供OSGi組態，其參數會影響進階計分演算法。

![chlimage_1-139](assets/chlimage_1-139.png)

* **評分權重**

   對於主題，請指定計算分數時應給予最高優先順序的動詞。 可以輸入一個或多個主題，但每個主題限 **定一個動詞**。 請參 [閱主題和動詞](/help/communities/implementing-scoring.md#topics-and-verbs)。
以逗號逸 `topic,verb` 出方式輸入。 例如：
   `/social/forum/hbs/social/forum\,ADD`
對於QnA和論壇元件，預設設定為ADD動詞。

* **計分範圍**

   進階分數的範圍由此值（最大可能分數）和0（最低可能分數）定義。

   預設值為100，因此計分範圍為0-100。

* **實體衰減時間間隔**

   此參數代表所有實體分數在其後延遲的小時數。 您必須在社群網站的分數中不再包含舊內容。

   預設值為216000小時（~24年）。

* **評分增長率**：這會指定0與評分範圍之間的分數，超過此分數，增長會放緩，以限制專家人數。

   預設值為 50。

## 進階計分規則 {#advanced-scoring-rules}

在基本評分中，獲得徽章所需的數量是已知的。

在進階計分中，需要的量是根據系統內的質量資料量不斷調整。 計分會以類似鐘形曲線的方式持續計算。

如果會員在已不活躍的主題上獲得專家徽章，他們可能會因為時間的流逝而失去徽章。

### scoringType {#scoringtype}

計分規則是一組計分子規則，每個子規則都聲明 `scoringType`。

若要叫用進階計分引擎， `scoringType`應將設為 `advanced`。

請參 [閱計分子規則](/help/communities/implementing-scoring.md#scoring-sub-rules)。

![chlimage_1-140](assets/chlimage_1-140.png)

### 秒詞 {#stopwords}

進階計分套件會安裝組態資料夾，其中包含秒數檔案：

* `/etc/community/scoring/configuration/stopwords`

進階計分演算法使用秒字檔案中包含的字詞清單，以識別在內容處理期間忽略的常見英文字詞。

您不希望修改此檔案。

如果秒數檔案遺失，進階計分引擎將會擲回錯誤。

## 進階標籤規則 {#advanced-badging-rules}

進階標籤規則屬性與基本標籤 [規則屬性不同](/help/communities/implementing-scoring.md#badging-rules)。

與其將點與徽章影像建立關聯，您只需識別允許的專家人數和要授予的徽章影像。

![chlimage_1-141](assets/chlimage_1-141.png)

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
   <td><em>（必要）</em> ，標籤影像的多值字串，最多為badgingLevels數目。 標章影像路徑必須依順序排列，因此第一個路徑會授與最高專家。 如果標籤數少於badgingLevels所指示的標籤數，則陣列中的最後一個標籤將填充陣列的其餘部分。 範例項目：<br /> <code>/etc/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>長整數</td>
   <td><em>（可選）</em> ，指定要授予的專業知識級別。 例如，如果應該有一個 <code>expert </code>和( <code>almost expert</code> 兩個標章)，則值應設定為2。 badgingLevel應與badgingPath屬性所列的專家相關標章影像數目相對應。 預設值為1。</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>字串</td>
   <td><em>（必要）</em> ，將計分引擎識別為「基本」或「進階」。 設為「進階」，則預設為「基本」。</td>
  </tr>
  <tr>
   <td>計分規則</td>
   <td>String[]</td>
   <td><em>（可選）</em> ，多值字串，將標籤規則限制為由列出的分數規則識別的分數事件。<br /> 範例項目：<br /> 預 <code>/etc/community/scoring/rules/adv-comments-scoring</code><br /> 設為無限制。</td>
  </tr>
 </tbody>
</table>

## 包含的規則和徽章 {#included-rules-and-badge}

### 隨附徽章 {#included-badge}

本測試版包含一個獎勵型專家徽章：

* `expert`

   `/etc/community/badging/images/expert-badge/jcr:content/expert.png`

![chlimage_1-142](assets/chlimage_1-142.png)

要讓專家徽章顯示為活動的獎勵，請確定：

* `Badges` 已針對功能啟用，例如論壇或QnA元件。

* 進階計分和標籤規則會套用至放置元件的頁面（或上階）

請參閱以下內容的基本資訊：

* [啟用元件徽章](/help/communities/implementing-scoring.md#enableforcomponent)
* [套用規則](/help/communities/implementing-scoring.md#applytopage)

### 包含計分規則和子規則 {#included-scoring-rules-and-sub-rules}

測試版包含兩個論壇功能的進階計分 [規則](/help/communities/functions.md#forum-function) （每個用於論壇，而論壇功能的注釋元件則各一個）:

1. `/etc/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/etc/community/scoring/rules/sub-rules/adv-comments-rule
/etc/community/scoring/rules/sub-rules/adv-voting-rule-owner
/etc/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/etc/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/etc/community/scoring/rules/sub-rules/adv-forums-rule
/etc/community/scoring/rules/sub-rules/adv-comments-rule
/etc/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**附註:**

* 節 `rules`點和 `sub-rules` 節點都屬於 `cq:Page`

* `subRules`是規則節點上類型[] 「字串」的屬 `jcr:content` 性

* `sub-rules` 可能與各種計分規則共用

* `rules`應位於具有每個人的讀取權限的儲存庫位置

   * 規則名稱必須是唯一的，無論位置為何

### 包含的標籤規則 {#included-badging-rules}

此發行包含兩個與進階論壇和留言計分規則對 [應的進階標籤規則](#included-scoring-rules-and-sub-rules)。

* `/etc/community/badging/rules/adv-comments-badging`
* `/etc/community/badging/rules/adv-forums-badging`

**附註:**

* `rules` 節點的類型cq:Page
* `rules` 應位於具有每個人的讀取權限的儲存庫位置

   * 規則名稱必須是唯一的，無論位置為何

