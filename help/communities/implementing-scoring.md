---
title: 社群評分和預算
description: AEM Communities評分和徽章可讓您識別及獎勵社群成員
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2851'
ht-degree: 2%

---

# 社群評分和預算 {#communities-scoring-and-badges}

## 概觀 {#overview}

AEM Communities評分和徽章功能提供識別及獎勵社群成員的能力。

評分和徽章的主要方面包括：

* [指派徽章](#assign-and-revoke-badges) 以識別社群中成員的角色。

* [徽章的基本獎勵](#enable-scoring) 鼓勵成員參與（建立的內容數量）。

* [進階獎勵徽章](/help/communities/advanced.md) 將成員識別為專家（建立的內容品質）。

**注意** 獎勵徽章是 [預設為未啟用](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>UI可供使用時，CRXDE Lite中顯示的實作結構可能會有所變更。

## 徽章 {#badges}

徽章會放置在成員的名稱下，以表示其在社群中的角色或地位。 徽章可以顯示為影像或名稱。 當顯示為影像時，名稱會包含為協助工具的替代文字。

依預設，徽章位於以下位置的存放庫中：

* `/libs/settings/community/badging/images`

若儲存在其他位置，應讓每個人都可讀取這些檔案。

在UGC中會區分徽章，不論它們是依照規則指派或贏取。 目前，指派的徽章會顯示為文字，而贏取的徽章會顯示為影像。

### 徽章管理UI {#badge-management-ui}

社群 [徽章主控台](/help/communities/badges.md) 可讓您新增自訂徽章，當成員贏取（授予）或在社群中擔任特定角色（已指派）時，徽章會針對該成員顯示。

### 指派的徽章 {#assigned-badges}

管理員會根據社群成員在社群中的角色，為其指派角色型徽章。

指派（和授予）徽章會儲存在選取的 [SRP](/help/communities/srp.md) 和無法直接存取。 在GUI可用之前，指派角色型徽章的唯一方法是使用程式碼或cURL。 如需cURL指示，請參閱標題為 [指派和撤銷徽章](#assign-and-revoke-badges).

此版本包含三個角色型徽章：

* **版主**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **群組管理員**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **有特殊許可權的成員**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![已指派的徽章](assets/assigned-badges.png)

### 獎勵徽章 {#awarded-badges}

評分服務會根據社群成員活動中套用的規則，將獎勵型徽章授予社群成員。

若要讓徽章顯示為活動的獎勵，必須發生以下兩個情況：

* 徽章必須為 [已啟用](#enableforcomponent) 用於特徵元件。
* 評分和徽章規則必須 [已套用](#applytopage) 到放置元件的頁面（或上階）。

此版本包含三個獎勵型徽章：

* **金級**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **銀級**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **銅級**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![獎章徽章](assets/awarded-badges.png)

>[!NOTE]
>
>評分規則可設定為針對標籤為不適當的貼文指派負分，進而影響評分值。 不過，獲得徽章後，由於評分點減少或評分規則變更，該徽章將不會自動移除。
>
>獎勵徽章的撤銷方式與指派徽章相同。 請參閱 [指派和撤銷徽章](#assign-and-revoke-badges) 區段。 未來的改善專案將包括管理成員徽章的UI。

### 自訂徽章 {#custom-badges}

自訂徽章可使用進行安裝 [徽章主控台](/help/communities/badges.md) 並在徽章規則中指派或指定。

從「徽章」控制檯安裝後，自訂徽章會自動複製到發佈環境。

## 啟用評分 {#enable-scoring}

預設不會啟用評分。 設定及啟用徽章評分和獎勵的基本步驟為：

* 識別學習點數規則([評分規則](#scoring-rules))。
* 針對每個評分規則所累積的點數，指派 [徽章](#badges) ([徽章規則](#badging-rules))。

* [套用評分和徽章規則至社群網站](#apply-rules-to-content).
* [為社群功能啟用徽章](#enable-badges-for-component).

請參閱 [快速測試](#quick-test) 區段，使用論壇和評論的預設評分和徽章規則，為社群網站啟用評分。

### 套用規則至內容 {#apply-rules-to-content}

若要啟用評分和徽章，請新增屬性 `scoringRules` 和 `badgingRules` 至網站內容樹狀結構中的任何節點。

如果網站已發佈，請在套用所有規則並啟用元件後，重新發佈網站。

套用至已啟用徽章的元件的規則為目前節點或其上階的規則。

如果節點的型別 `cq:Page` （建議），然後使用CRXDE|Lite，將屬性新增至其 `jcr:content` 節點。

| **屬性** | **類型** | **說明** |
|---|---|---|
| badgingrules | 字串 | 的陣列清單 [徽章規則](#badging-rules) |
| scoringRules | 字串 | 的陣列清單 [評分規則](#scoring-rules) |

>[!NOTE]
>
>如果評分規則似乎對獎勵徽章沒有影響，請確保該評分規則並未被徽章規則的scoringRules屬性封鎖。 請參閱標題為的一節 [徽章規則](#badging-rules).

### 啟用元件的預算 {#enable-badges-for-component}

評分和徽章規則僅適用於已透過編輯元件設定來啟用徽章的元件例項。 [製作模式](/help/communities/author-communities.md).

布林值屬性， `allowBadges`，啟用/停用元件例項的徽章顯示。 它可在以下位置設定： [元件編輯對話方塊](/help/communities/author-communities.md) 用於論壇、QnA和評論元件，透過標籤為的核取方塊 **顯示徽章**.

#### 範例：論壇元件例項的allowBadges {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>以論壇、QnA和評論中的HBS程式碼為例，任何元件都可以重疊以顯示徽章。

## 評分規則 {#scoring-rules}

評分規則是獎勵徽章評分的基礎。

每個評分規則都是一或多個子規則的清單。 評分規則會套用至社群網站內容，以識別啟用徽章時要套用的規則。

評分規則是繼承的，但不會累加。 例如：

* 如果頁面2包含評分規則2，且其上階page1包含評分規則1。
* page2元件上的動作會同時叫用rule1和rule2。
* 如果兩個規則包含相同專案的適用子規則 `topic/verb`：

   * 只有規則2的子規則會影響分數。
   * 不會新增兩個子規則的分數。

有多個評分規則時，系統會分別維護每個規則的分數。

評分規則是型別的節點 `cq:Page` 具有屬性 `jcr:content` 指定定義其之子規則清單的節點。

分數會儲存在SRP中。

>[!NOTE]
>
>最佳實務：為各個評分規則指定唯一名稱。
>
>評分規則名稱應為全域唯一名稱，且不得以相同名稱結尾。
>
>的範例 *非* 待辦事項：
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### 評分子規則 {#scoring-sub-rules}

評分子規則包含詳細說明參與社群之值的屬性。

每個評分子規則都會識別：

* 正在追蹤哪些活動？
* 涉及哪些特定的社群功能？
* 系統會給予多少點數？

依預設，點數會授予採取動作的成員，除非子規則將內容的所有者指定為接收點數( `forOwner`)。

每個子規則可包含在一或多個評分規則中。

子規則的名稱通常會遵循使用的模式 *主旨*， *物件*、和 *動詞*. 例如：

* member-comment-create
* 會員 — 接收 — 投票

子規則是型別的節點 `cq:Page` 具有屬性 `jcr:content`指定下列專案的節點： [動詞和主題](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>類型</th>
   <th> 值說明</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>長整數</td>
   <td>
    <ul>
     <li>必要；動詞會對應至事件動作</li>
     <li>至少必須有一個動詞屬性</li>
     <li>動詞必須全部大寫輸入</li>
     <li>可能有多個動詞屬性，但無重複專案</li>
     <li>值是要套用至此事件的分數</li>
     <li>值可為正數或負數</li>
     <li>此版本支援的動詞清單位於 <a href="#topics-and-verbs">主題和動詞</a> 區段</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>字串</td>
   <td>
    <ul>
     <li>選用；將子規則限製為事件主題所識別的社群元件</li>
     <li>若指定：值是事件主題的多值字串</li>
     <li>此版本中的主題清單位於 <a href="#topics-and-verbs">主題和動詞</a> 區段</li>
     <li>預設為套用至與動詞相關的所有主題</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>布林值</td>
   <td>
    <ul>
     <li>選擇性；當成員對其擁有的內容進行操作時並不相關</li>
     <li>如果為true，則將分數套用至所執行內容的擁有者</li>
     <li>如果為false，則對成員執行動作套用分數</li>
     <li>預設為false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>字串</td>
   <td>
    <ul>
     <li>選用；識別評分引擎</li>
     <li>若設為「基本」，會根據數量指定評分引擎
      <ul>
       <li>包含在發行版本中</li>
      </ul> </li>
     <li>若設為「進階」，會根據品質與數量指定評分引擎
      <ul>
       <li>需要 <a href="/help/communities/advanced.md">額外套件</a></li>
      </ul> </li>
     <li>預設為「basic」</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 包含評分規則和子規則 {#included-scoring-rules-and-sub-rules}

此版本包含的兩個評分規則： [論壇功能](/help/communities/functions.md#forum-function) （論壇功能的「論壇」和「評論」元件各一個） ：

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-comment-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-give-vote /member/give-vote /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-forum-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-note-vote /member/settings/community/scoring/rules/sub-rules/member-is-modered

**附註:**

* 兩者 `rules` 和 `sub-rules` 節點的型別為cq：Page。

* `subRules` 是String型別的屬性[] 在規則的 `jcr:content` 節點。

* `sub-rules` 可以在各種評分規則之間共用。
* `rules` 應該位在儲存庫位置，且每個人都有讀取許可權。

   * 無論位置為何，規則名稱必須是唯一的。

### 啟用自訂評分規則 {#activating-custom-scoring-rules}

在製作環境中對評分規則或子規則所做的任何變更或新增都必須安裝在發佈上。

## 徽章規則 {#badging-rules}

徽章規則透過指定以下內容，將評分規則連結至徽章：

* 評分規則
* 要授與特定徽章所需的分數

徽章規則是型別的節點 `cq:Page` 具有屬性 `jcr:content` 將評分規則與分數和徽章建立關聯的節點。

徽章的規則包含必要 `thresholds` 對應至徽章的分數有序清單屬性。 分數必須依遞增值排序。 例如：

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * 榮獲銅級徽章者可獲得1分。

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * 當累積60分時，會授予銀級徽章。

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * 當累積80分時，會授予金級徽章。

徽章規則會與評分規則配對，這會決定如何累積分數。 請參閱標題為的一節 [套用規則至內容](#apply-rules-to-content).

此 `scoringRules` 徽章規則的屬性只會限制哪些評分規則可以與該特定徽章規則配對。

>[!NOTE]
>
>最佳做法：建立每個AEM網站專屬的徽章影像。

![badging-rule-configuration](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>類型</th>
   <th>值說明</th>
  </tr>
  <tr>
   <td>臨界值</td>
   <td>字串</td>
   <td><em>（必要）</em> 「數字|路徑」形式的多值字串
    <ul>
     <li>數字=分數</li>
     <li>| =垂直線字元(U+007C)</li>
     <li>路徑=徽章影像資源的完整路徑</li>
    </ul> 這些字串必須排序，數字的值才會增加，數字與路徑之間不應出現空格。<br /> 範例專案：<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingtype</td>
   <td>字串</td>
   <td><em>（選擇性）</em> 將評分引擎識別為「基本」或「進階」。 如果需要進階評分引擎，請參閱 <a href="/help/communities/advanced.md">進階評分和徽章</a>. 預設值為「basic」。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>字串</td>
   <td>(<em>可選</em>)多值字串，可將徽章規則限製為評分規則所識別的評分事件</td>
  </tr>
 </tbody>
</table>

### 包含的徽章規則 {#included-badging-rules}

發行版本中包含兩個徽章規則，分別對應至 [論壇和評論評分規則](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**附註:**

* `rules` 節點的型別為cq：Page。
* `rules` 應該位在儲存庫位置，且每個人都有讀取許可權。

   * 無論位置為何，規則名稱必須是唯一的。

### 啟用自訂徽章規則 {#activating-custom-badging-rules}

在製作環境中對徽章規則或影像所做的任何變更或新增都必須安裝在發佈上。

## 指派和撤銷徽章 {#assign-and-revoke-badges}

您可以使用以下任一專案將徽章指派給成員： [成員主控台](/help/communities/members.md#badges-tab) 或使用cURL命令以程式設計方式執行。

以下cURL命令顯示指派和撤銷徽章的HTTP要求所需的專案。 基本格式為：

cURL -i -XPOST-H *頁首* -u *登入* -F *操作* -F *徽章* *member-profile-url*

*頁首* = &quot;Accept：application/json&quot;自訂標題以傳遞至伺服器（必填）

*登入* = administrator-id：password，例如admin：admin

*操作* = &quot;：operation=social：assignBadge&quot;或&quot;：operation=social：deleteBadge&quot;

*徽章* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* =徽章影像檔案在存放庫中的位置，例如/libs/settings/community/badging/images/moderator/jcr：content/moderator.png

*member-profile-url* =發佈時成員設定檔的端點，例如https://&lt;server>：&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>此 *member-profile-url*：
>
>* 如果符合以下條件，可參考作者例項： [通道服務](/help/communities/users.md#tunnel-service) 已啟用。
>* 可能是一個模糊的隨機名稱 — 請參閱 [安全性檢查清單](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) 關於可授權ID。

### 範例： {#examples}

#### 指派版主徽章 {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### 撤銷指定的銀級徽章 {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>使用cURL來指派和撤銷徽章適用於任何徽章影像，但是當指派而不是贏取時，會將其標籤為已指派徽章並進行相應處理。

## 自訂元件的評分和預算 {#scoring-and-badges-for-custom-components}

將針對自訂元件建立的事件主題與動詞建立關聯，可為其建立評分和徽章規則。

## 主題和動詞 {#topics-and-verbs}

當成員與社群功能互動時，會傳送可觸發非同步接聽程式的事件，例如通知和評分。

元件的SocialEvent例項會將事件記錄為 `actions` 發生於 `topic`. SocialEvent包含傳回 `verb` 與動作相關聯。 有一個 *n-1* 關係介於 `actions` 和 `verbs`.

針對已傳送的communities元件，下表說明 `verbs` 已針對每個專案定義 `topic` 可在以下位置使用： [評分子規則](#scoring-sub-rules).

>[!NOTE]
>
>新的布林值屬性， `allowBadges`，啟用/停用元件例項的徽章顯示。 可在更新後設定 [元件編輯對話方塊](/help/communities/author-communities.md) 透過標籤為的核取方塊 **顯示徽章**.

**[行事曆元件](/help/communities/calendar.md)**
社交事件 `topic`= com/adobe/cq/social/calendar

| **動詞** | **說明** |
|---|---|
| POST | 成員建立行事曆事件 |
| 新增 | 行事曆事件的成員註解 |
| 更新 | 成員的行事曆事件或註解已編輯 |
| 刪除 | 成員的行事曆事件或註解已刪除 |

**[註解元件](/help/communities/comments.md)**
社交事件 `topic`= com/adobe/cq/social/comment

| **動詞** | **說明** |
|---|---|
| POST | 成員建立註解 |
| 新增 | 成員回複評論 |
| 更新 | 成員的註解已編輯 |
| 刪除 | 已刪除成員的註解 |

**[檔案庫元件](/help/communities/file-library.md)**
社交事件 `topic`= com/adobe/cq/social/fileLibrary

| **動詞** | **說明** |
|---|---|
| POST | 成員建立資料夾 |
| 附加 | 成員上傳檔案 |
| 更新 | 成員更新資料夾或檔案 |
| 刪除 | 成員刪除資料夾或檔案 |

**[論壇元件](/help/communities/forum.md)**
社交事件 `topic`= com/adobe/cq/social/forum

| **動詞** | **說明** |
|---|---|
| POST | 成員建立論壇主題 |
| 新增 | 成員對論壇主題的回覆 |
| 更新 | 成員的論壇主題或回覆已編輯 |
| 刪除 | 已刪除成員的論壇主題或回覆 |

**[日誌元件](/help/communities/blog-feature.md)**
社交事件 `topic`= com/adobe/cq/social/journal

| **動詞** | **說明** |
|---|---|
| POST | 成員建立部落格 |
| 新增 | 部落格上的成員評論 |
| 更新 | 已編輯成員的部落格或評論 |
| 刪除 | 已刪除成員的部落格或評論 |

**[QnA元件](/help/communities/working-with-qna.md)**
社交事件 `topic` = com/adobe/cq/social/qna

| **動詞** | **說明** |
|---|---|
| POST | 成員建立QnA問題 |
| 新增 | 成員建立QnA答案 |
| 更新 | 編輯成員的QnA問題或答案 |
| 選取 | 已選取成員的答案 |
| 取消選取 | 已取消選取成員的答案 |
| 刪除 | 已刪除成員的QnA問題或答案 |

**[稽核元件](/help/communities/reviews.md)**
社交事件 `topic`= com/adobe/cq/social/review

| **動詞** | **說明** |
|---|---|
| POST | 成員建立稽核 |
| 更新 | 成員的稽核已編輯 |
| 刪除 | 已刪除成員的評論 |

**[評等元件](/help/communities/rating.md)**
社交事件 `topic`= com/adobe/cq/social/tally/rating

| **動詞** | **說明** |
|---|---|
| 新增評等 | 已對成員的內容進行升級 |
| 移除評等 | 成員的內容已降級 |

**[投票元件](/help/communities/voting.md)**
社交事件 `topic`= com/adobe/cq/social/tally/voting

| **動詞** | **說明** |
|---|---|
| 新增投票 | 成員內容已投贊成票 |
| 移除投票 | 成員內容已被投票否決 |

**啟用稽核的元件**
社交事件 `topic`= com/adobe/cq/social/moderation

| **動詞** | **說明** |
|---|---|
| 拒絕 | 成員內容遭拒 |
| 如有不當情形，加註旗標 | 已標幟成員的內容 |
| 如有不當情形，取消標幟 | 成員的內容未標幟 |
| ACCEPT | 仲裁者已核准成員的內容 |
| 關閉 | 成員關閉評論以進行編輯和回覆 |
| 開啟 | 成員重新開啟註解 |

### 自訂元件事件 {#custom-component-events}

對於自訂元件，會例項化SocialEvent以將元件的事件記錄為 `actions` 發生於 `topic`.

若要支援評分，SocialEvent需要覆寫方法 `getVerb()` 因此適當的 `verb` 針對每個屬性傳回 `action`. 此 `verb` 針對動作傳回的可能是常用的(例如 `POST`)或專用於元件的元件(例如 `ADD RATING`)。 有一個 *n-1* 關係介於 `actions` 和 `verbs`.

## 疑難排解 {#troubleshooting}

### 徽章未出現 {#badges-are-not-appearing}

如果評分和徽章規則已套用至網站的內容，但未針對任何活動授與徽章，請確定已為該元件的執行個體啟用徽章。

另請參閱 [啟用元件的預算](#enable-badges-for-component).

### 評分規則無效 {#scoring-rule-has-no-effect}

如果評分和徽章規則已套用至網站的內容，且已針對某些動作（而非其他動作）授與徽章，請檢查徽章規則是否未限制其套用的評分規則。

請參閱 `scoringRules` 屬性 [徽章規則](#badging-rules).

### 區分大小寫的拼寫錯誤 {#case-sensitive-typo}

大部分的屬性和值（尤其是動詞）都區分大小寫。 在評分子規則中使用動詞時，動詞必須全部大寫。

如果功能無法如預期運作，請確認資料已正確輸入。

## 快速測試 {#quick-test}

您可以使用快速嘗試評分和徽章 [快速入門教學課程](/help/communities/getting-started.md) （參與）網站：

* 存取作者的CRXDE Lite。
* 瀏覽至基本頁面：

   * /content/sites/engage/en/jcr：content

* 新增badgingRules屬性：

   * **名稱**：`badgingRules`
   * **類型**：`String`
   * 選取 **多個**
   * 選取 **新增**
   * 輸入 `/libs/settings/community/badging/rules/forums-badging`
   * 選取 **+**
   * 輸入 `/libs/settings/community/badging/rules/comments-badging`
   * 選取 **確定**

* 新增scoringRules屬性：

   * **名稱**：`scoringRules`
   * **類型**：`String`
   * 選取 **多個**
   * 選取 **新增**
   * 輸入 `/libs/settings/community/scoring/rules/forums-scoring`
   * 選取 **+**
   * 輸入 `/libs/settings/community/scoring/rules/comments-scoring`
   * 選取 **確定**

* 選取 **全部儲存**.

![test-scoring-badging](assets/test-scoring-badging.png)

接下來，確定論壇和評論元件允許顯示徽章：

* 再次使用CRXDE Lite。
* 瀏覽至論壇元件

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* 如有必要，請新增allowBadges布林值屬性，並確保其為true。

   * **名稱**：`allowBadges`
   * **類型**：`Boolean`
   * **值**：`true`

![test-forum-component](assets/test-forum-component.png)

下一個， [重新發佈](/help/communities/sites-console.md#publishing-the-site) 社群網站。

最後，

* 瀏覽至發佈執行個體上的元件。
* 以社群成員身分登入(例如，weston.mccall@dodgit.com /密碼)。
* 發表新論壇主題。
* 頁面必須重新整理才能顯示徽章。

   * 登出並以其他社群成員身分登入(例如：aaron.mcdonald@mailinator.com/password)。

* 選取論壇。

由於第一個論壇徽章規則的第一個臨界值是1分，這應該會為社群成員贏取可透過其論壇貼文看到的銅級徽章。

![bronzebadge](assets/bronzebadge.png)

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [評分和徽章要點](/help/communities/configure-scoring.md) 開發人員頁面。

如需進階評分引擎的詳細資訊，請參閱 [進階評分和徽章](/help/communities/advanced.md).

可設定的排行榜 [元件](/help/communities/enabling-leaderboard.md) 和 [函式](/help/communities/functions.md#leaderboard-function) 簡化社群網站上顯示成員及其分數的程式。
