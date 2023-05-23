---
title: 高級評分和徽章
seo-title: Advanced Scoring and Badges
description: 設定高級計分
seo-description: Setting up advanced scoring
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# 高級評分和徽章{#advanced-scoring-and-badges}

## 概觀 {#overview}

高級評分允許授予徽章，將成員標識為專家。 高級計分根據數量分配分數 *和* 由成員建立的內容質量，而基本評分則僅根據建立的內容數量來分配點。

此差異是由於用於計算得分的得分引擎。 基本評分引擎採用簡單的數學方法。 高級評分引擎是一種自適應算法，它獎勵通過主題的自然語言處理(NLP)推導的貢獻有價值內容和相關內容的活動成員。

除了內容相關性，評分算法還考慮了成員活動，如投票和回答百分比。 雖然基本評分包括定量評分，但高級評分使用算法。

因此，先進的評分引擎需要足夠的資料來進行有意義的分析。 隨著算法不斷根據所建立內容的體積和質量進行調整，不斷重新評估成為專家的成就閾值。 還有一個概念 *衰* 會員的較老職位。 如果一名專家成員停止參與獲得專家地位的主題事項，則在某個預定點(見 [計分引擎配置](#configurable-scoring-engine))可能失去專家的地位。

設定高級評分與基本評分幾乎相同：

* 基本和高級評分和標籤規則 [應用於內容](/help/communities/implementing-scoring.md#apply-rules-to-content) 以同樣的方式。

   * 基本和高級評分規則和標籤規則可應用於相同內容。

* [為元件啟用徽章](/help/communities/implementing-scoring.md#enable-badges-for-component) 為泛型。

在設定評分規則和標籤規則方面的區別是：

* 可配置的高級評分引擎
* 高級計分規則：

   * `scoringType` 設定為 `advanced`
   * 需要 `stopwords`

* 高級標籤規則：

   * `badgingType` 設定為 `advanced`
   * `badgingLevels` 設定為 **要授予的專家級數**
   * 需要 `badgingPaths` 標籤陣列，而不是閾值陣列映射點到標籤。

>[!NOTE]
>
>要使用高級評分和標籤功能，請安裝 [專家識別包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg)。

## 可配置評分引擎 {#configurable-scoring-engine}

高級評分引擎提供具有影響高級評分算法的參數的OSGi配置。

![高級評分引擎](assets/advanced-scoring-engine.png)

* **評分權重**

   對於主題，指定計算分數時應給予最高優先順序的動詞。 可以輸入一個或多個主題，但僅限於 **每個主題**。 請參閱 [主題和動詞](/help/communities/implementing-scoring.md#topics-and-verbs)。
輸入方式 `topic,verb` 用逗號轉義。 例如：
   `/social/forum/hbs/social/forum\,ADD`
預設設定為QnA和論壇元件的ADD謂詞。

* **評分範圍**

   高級分數的範圍由此值（最大可能分數）和0（最低可能分數）定義。

   預設值為100，因此評分範圍為0-100。

* **實體衰減時間間隔**

   此參數表示所有實體得分被延遲後的小時數。 這要求不再將舊內容包含在社區站點的分數中。

   預設值為216000小時（~24年）。

* **評分增長率**
它指定0和評分範圍之間的分數，超過此範圍後，增長將放緩以限制專家數。

   預設值為 50。

## 高級計分規則 {#advanced-scoring-rules}

在基本評分中，獲得徽章所需的數量是已知的。

在高級評分中，需要的數量根據系統內的質量資料量不斷調整。 記分以類似鐘形曲線的方式持續計算。

如果成員在不再活躍的主題上獲得專家徽章，則他們可能會因時間流逝而失去徽章。

### 計分類型 {#scoringtype}

評分規則是一組評分子規則，每個子規則聲明 `scoringType`。

要調用高級計分引擎，請 `scoringType`應設定為 `advanced`。

請參閱 [計分子規則](/help/communities/implementing-scoring.md#scoring-sub-rules)。

![高級評分類型](assets/advanced-scoring-type.png)

### 停詞 {#stopwords}

高級計分包會安裝包含非索引字檔案的配置資料夾：

* `/libs/settings/community/scoring/configuration/stopwords`

該高級評分算法使用在止詞檔案中包含的單詞清單來標識在內容處理期間被忽略的通用英語單詞。

不期望修改此檔案。

如果停止字檔案丟失，高級計分引擎將引發錯誤。

## 高級標籤規則 {#advanced-badging-rules}

高級標籤規則屬性與 [基本標籤規則屬性](/help/communities/implementing-scoring.md#badging-rules)。

與將點與徽章影像關聯不同，只需標識允許的專家數量和要獎勵的徽章影像。

![高級簽名規則](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>類型</th>
   <th>值 說明</th>
  </tr>
  <tr>
   <td>標籤路徑</td>
   <td>字串[]</td>
   <td><em>（必需）</em> 標籤影像的多值字串，直到badgingLevels的數量。 必須對標籤影像路徑進行排序，以便將第一個路徑授予最高專家。 如果徽章數少於badgingLevels所指示的標籤數，則陣列中的最後一個徽章會填充陣列的其餘部分。 示例條目：<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>標籤級別</td>
   <td>長整數</td>
   <td><em>（可選）</em> 指定要授予的專業知識級別。 例如，如果 <code>expert </code>和 <code>almost expert</code> （兩個徽章），則值應設定為2。 badgingLevel應與badgingPath屬性所列的專家相關標籤影像的數量相對應。 預設值為1。</td>
  </tr>
  <tr>
   <td>標籤類型</td>
   <td>字串</td>
   <td><em>（必需）</em> 將評分引擎標識為「basic」或「advanced」。 設定為「高級」，否則預設為「基本」。</td>
  </tr>
  <tr>
   <td>計分規則</td>
   <td>字串[]</td>
   <td><em>（可選）</em> 一個多值字串，用於將標籤規則限制為由列出的評分規則標識的評分事件。<br /> 示例條目：<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> 預設值為無限制。</td>
  </tr>
 </tbody>
</table>

## 包括的規則和徽章 {#included-rules-and-badge}

### 包括的徽章 {#included-badge}

本測試版包含一個基於獎勵的專家徽章：

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![專家徽章](assets/included-badge.png)

要將專家徽章顯示為活動獎勵，請確保：

* `Badges` 為功能（如論壇或QnA元件）啟用。

* 高級評分規則和標籤規則將應用於元件所在的頁面（或祖先）

請參閱以下資訊的基本資訊：

* [為元件啟用標籤](/help/communities/implementing-scoring.md#enableforcomponent)
* [應用規則](/help/communities/implementing-scoring.md#applytopage)

### 包括計分規則和子規則 {#included-scoring-rules-and-sub-rules}

測試版中包括兩個高級評分規則 [論壇功能](/help/communities/functions.md#forum-function) （每個論壇和論壇功能的評論部分各一個）:

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

**附註:**

* 兩者 `rules` 和 `sub-rules` 節點的類型 `cq:Page`。
* `subRules` 是字串類型的屬性`[]` 規則 `jcr:content` 的下界。
* `sub-rules` 可以在各種評分規則之間共用。
* `rules` 應位於儲存庫位置中，並具有每個人的讀取權限。
* 規則名稱必須唯一，不管位置如何。

### 包括標籤規則 {#included-badging-rules}

發行版中包括兩個與 [高級論壇和評論評分規則](#included-scoring-rules-and-sub-rules)。

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**附註:**

* `rules` 節點的類型為cq:Page。
* `rules` 應位於儲存庫位置中，並具有每個人的讀取權限。
* 規則名稱必須唯一，不管位置如何。
