---
title: 社群評分和標章
seo-title: 社群評分和標章
description: AEM Communities評分和標章可讓您識別和獎勵社群成員
seo-description: AEM Communities評分和標章可讓您識別和獎勵社群成員
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 社群評分和標章{#communities-scoring-and-badges}

## 概覽 {#overview}

AEM Communities計分和標章功能提供識別和獎勵社群成員的能力。

評分和標章主要有：

* [指派標章](#assign-and-revoke-badges) ，以識別社群中成員的角色

* [基本獎章](#enable-scoring) ，以鼓勵會員參與（建立的內容數量）
* [進階授與徽章](/help/communities/advanced.md) ，將會員識別為專家（建立的內容品質）

**請注意** ，預設不會 [啟用標章授予](/help/communities/implementing-scoring.md#main-pars-text-237875536)。

>[!CAUTION]
>
>在CRXDE Lite中可見的實作結構可能會在UI可用時變更。

## 徽章 {#badges}

標章會放在成員名稱下，以指出其角色或在社群中的地位。 標章可以顯示為影像或名稱。 當顯示為影像時，名稱會包含為協助工具的替代文字。

預設情況下，徽章位於

* /etc/community/badging/images

如果儲存在不同的位置，則每個人都應該可以讀取。

在UGC中，徽章會區分為是指派徽章，還是根據規則賺取徽章。 目前，指派的標章會顯示為文字，而免費標章會顯示為影像。

### 徽章管理UI {#badge-management-ui}

Communities [Badges控制台](/help/communities/badges.md) （Communities Badges控制台）提供新增自訂徽章的功能，這些徽章可在獲得（授予）會員或在其擔任社群中特定角色（指派）時顯示。

### 指派的標章 {#assigned-badges}

基於角色的徽章由管理員根據社區成員在社區中的角色指派給社區成員。

指派（和已喚醒）的標章會儲存在選取的 [SRP](/help/communities/srp.md) ，無法直接存取。 在GUI可用之前，指派角色標章的唯一方法就是使用程式碼或cURL。 如需cURL指示，請參閱標題為「指派 [和撤銷標章」的章節](#assign-and-revoke-badges)。

此版本包含3個以角色為基礎的標章：

* 協調者
   `/etc/community/badging/images/moderator/jcr:content/moderator.png`

* 群組管理員
   `/etc/community/badging/images/group-manager/jcr:content/group-manager.png`

* 特權成員
   `/etc/community/badging/images/privileged-member/jcr:content/privileged-member.png`

![chlimage_1-98](assets/chlimage_1-98.png)

### 獎章 {#awarded-badges}

評分服務會根據社區成員在社區活動中適用的規則，向社區成員頒發獎勵標章。

為了讓徽章成為活動的獎勵，必須有兩件事：

* 必須為特 [徵元件](#enableforcomponent) 啟用標籤
* 計分和標籤規則必 [須套用](#applytopage) 至元件所在的頁面（或上階）

本版包含三枚獎勵型徽章：

* 黃金
   `/etc/community/badging/images/gold-badge/jcr:content/gold.png`

* 銀
   `/etc/community/badging/images/silver-badge/jcr:content/silver.png`

* 銅
   `/etc/community/badging/images/bronze-badge/jcr:content/bronze.png`

![chlimage_1-99](assets/chlimage_1-99.png)

>[!NOTE]
>
>評分規則可設定為為標示為不適當之貼文指派負點，進而影響分數值。 不過，一旦獲得徽章，就不會因為計分點減少或計分規則變更而自動移除徽章。
>
>吊銷獎章的方式與吊銷標章相同。 請參閱「 [指派和撤銷標章](#assign-and-revoke-badges) 」一節。 未來的改進將包括管理會員徽章的UI。

### 自訂標章 {#custom-badges}

自訂徽章可以使用「徽章」控 [制台安裝](/help/communities/badges.md) ，並可在徽章規則中指派或指定。

當從Badges控制台安裝時，自訂標章會自動複製至發佈環境。

## 啟用計分 {#enable-scoring}

預設未啟用計分。 標章設定及啟用評分及授予的基本步驟為：

* 識別賺取點數的規則([計分規則](#scoring-rules))
* 針對每個計分規則累積的點數，指派 [標章](#badges) ([標章規則](#badging-rules))

* [將計分和徽章規則套用至社群網站](#apply-rules-to-content)
* [啟用社群功能的標籤](#enable-badges-for-component)

請參閱「 [快速測試](#quick-test) 」區段，使用論壇和留言的預設計分和標籤規則，為社群網站啟用計分。

### 套用規則至內容 {#apply-rules-to-content}

若要啟用計分和標章，請將屬 `scoringRules` 性新 `badgingRules`增至網站內容樹中的任何節點。

如果網站已發佈，在套用所有規則並啟用元件後，請重新發佈網站。

適用於啟用徽章的元件的規則是當前節點或其祖先的規則。

如果節點類型(建 `cq:Page` 議)，則使用CRXDE|Lite將屬性添加到其節 `jcr:content`點。

| **屬性** | **類型** | **說明** |
|---|---|---|
| badgingRules | String[] | 標籤規則的數 [組清單](#badging-rules) |
| 計分規則 | String[] | 計分規則的數 [組清單](#scoring-rules) |

>[!NOTE]
>
>如果評分規則似乎對獎勵徽章沒有影響，請確定評分規則未被評分規則的scoringRules屬性封鎖。 請參閱標籤規 [則一節](#badging-rules)。

### 啟用元件標章 {#enable-badges-for-component}

計分和徽章規則僅適用於在編寫模式中編輯元件組態以啟用徽章的元件 [例項](/help/communities/author-communities.md)。

布爾屬性 `allowBadges`啟用／禁用元件實例的標誌顯示。 它可在論壇、QnA的組 [件編輯對話框中配置](/help/communities/author-communities.md) ，並通過標有「顯示標章」的複選框對元件 **進行注釋**。

#### 範例：「論壇」元件實例的allowBadges {#example-allowbadges-for-forum-component-instance}

![chlimage_1-100](assets/chlimage_1-100.png)

>[!NOTE]
>
>任何元件都可重疊，以顯示標章，例如論壇、QnA和註解中的HBS程式碼。

## 計分規則 {#scoring-rules}

評分規則是評分標誌的基礎。

很簡單，每個計分規則都是一或多個子規則的清單。 計分規則會套用至社群網站內容，以識別在啟用標章時套用的規則。

計分規則是繼承的，但不是加法的。 例如：

* 如果page2包含計分規則2，其上階page1包含計分規則1
* page2元件上的動作將同時叫用規則1和規則2
* 如果兩個規則都包含相同之子規則 `topic/verb` :

   * 只有規則2的子規則會影響分數
   * 兩個子規則的分數不會加在一起

當有多個計分規則時，會針對每個規則分別維護分數。

計分規則是指在其節 `cq:Page` 點上具有屬性的 `jcr:content`節點，這些屬性指定定義規則的子規則清單。

分數會儲存在SRP中。

>[!NOTE]
>
>最佳實務：為每個計分規則指定唯一名稱。
>
>計分規則名稱應全局唯一；他們不應以同名結尾。
>
>*not *to的範例：
>/etc/community/scoring/rules/site1/forums-scoring
>/etc/community/scoring/rules/site2/forums-scorning

### 計分子規則 {#scoring-sub-rules}

計分子規則包含詳細說明參與社群的值的屬性。

每個計分子規則識別

* 追蹤哪些活動
* 其中涉及到特定的社區功能
* 授與多少點數

預設情況下，系統會將點數授予採取動作的成員，除非子規則指定內容擁有者接收點數( `forOwner`)。

每個子規則可以包含在一個或多個計分規則中。

子規則的名稱通常遵循使用*主語、物件*和動詞的 *模式。* 例如：

* member-comment-create
* 會員接收投票

子規則是指在其節點上具有屬 `cq:Page` 性的類型節 `jcr:content`點，可指定動 [詞和主題](#topics-and-verbs) 。

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
     <li>必要；動詞與事件動作相對應</li>
     <li>至少有一個動詞屬性</li>
     <li>動詞必須輸入全部大寫</li>
     <li>有多個動詞屬性，但沒有重複</li>
     <li>值是要套用至此事件的分數</li>
     <li>值可以是正數或負數</li>
     <li>版本中支援的動詞清單位於「主題與動 <a href="#topics-and-verbs">詞」區段</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>String[]</td>
   <td>
    <ul>
     <li>可選；將子規則限制為由事件主題標識的社區元件</li>
     <li>如果已指定：值是事件主題的多值字串</li>
     <li>發行中的主題清單位於「主題和動 <a href="#topics-and-verbs">詞」部分</a></li>
     <li>default is to apply to all topics associated with verb(s)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>布林值 (Boolean)</td>
   <td>
    <ul>
     <li>可選；與會員根據其擁有的內容行事無關</li>
     <li>若為真，則對所處理內容的擁有者套用分數</li>
     <li>如果為false，請將分數套用至執行動作的成員</li>
     <li>default is false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>字串</td>
   <td>
    <ul>
     <li>可選；識別計分引擎</li>
     <li>如果為"basic"，則根據數量指定計分引擎
      <ul>
       <li>包含在發行中</li>
      </ul> </li>
     <li>如果為「進階」，則根據品質和數量指定計分引擎
      <ul>
       <li>需要其 <a href="/help/communities/advanced.md">他套件</a></li>
      </ul> </li>
     <li>預設值為"basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 包含計分規則和子規則 {#included-scoring-rules-and-sub-rules}

此發行包含兩個論壇功能的評 [分規則](/help/communities/functions.md#forum-function) （一個分別用於論壇和論壇功能的「注釋」元件）:

1. /etc/community/scorting/rules/comments-scorting

   * subRules[] =/etc/community/scoring/rules/sub-rules/member-comment-create/etc/community/scomment/scommen-receive-pote/etc/community/scoring/rules/member-give-pote/etc/communere/s/sub-rules/sub-ren-res/men-is/mer-is-is-jon-red

1. /etc/community/scoring/rules/forums-scoring

   * subRules[] =/etc/community/scoring/rules/sub-rules/member-forum-create/etc/community/scommer-receive-vote/etc/community/scoring/rules/member-give-pote/etc/community/scorin/rules/sub-rules/mereres/mer-rules/member-is/is/is-is-is/men-is-is-is-is-is-is-is-is-is-is-is-h-re-is-h-h-h-re-re-th-thed

**附註:**

* both `rules`and `sub-rules` nodes are type cq:Page

* `subRules`是規則節點上類型[] 「字串」的屬 `jcr:content` 性

* `sub-rules` 可能與各種計分規則共用
* `rules`應位於具有每個人的讀取權限的儲存庫位置

   * 規則名稱必須是唯一的，不論位置

### 啟用自訂計分規則 {#activating-custom-scoring-rules}

在作者環境中對計分規則或子規則所做的任何變更或新增，都必須安裝在發佈上。

## 標籤規則 {#badging-rules}

標籤規則會指定：

* 計分規則
* 需要獲得特定徽章的分數

標籤規則是具有屬性的節 `cq:Page` 點類型的節點，屬 `jcr:content`性會將計分規則與分數和標籤建立關聯。

標籤規則由強制屬性組成， `thresholds`此屬性是對應至標章的分數順序清單。 分數必須依增加值排序。 例如：

* `1|/etc/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * 以1分的成績獲得銅牌

* `60|/etc/community/badging/images/silver-badge/jcr:content/silver.png`

   * 當積分60分時，將頒發銀牌

* `80|/etc/community/badging/images/gold-badge/jcr:content/gold.png`

   * 當累積80分時，就會發現金牌

標籤規則與計分規則配對，可決定點數的累積方式。 請參閱「將規則套 [用至內容」一節](#apply-rules-to-content)。

標籤 `scoringRules`規則上的屬性只會限制哪些計分規則可與該特定標籤規則配對。

>[!NOTE]
>
>最佳實務：建立每個AEM網站專屬的徽章影像。

![chlimage_1-101](assets/chlimage_1-101.png)

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>類型</th>
   <th>值說明</th>
  </tr>
  <tr>
   <td>閾值</td>
   <td>String[]</td>
   <td><em>（必要）</em> 「number|path」格式的多值字串
    <ul>
     <li>數字=分數</li>
     <li>| =垂直線字元(U+007C)</li>
     <li>路徑=標籤映像資源的完整路徑</li>
    </ul> 字串必須依序排列，如此數字值就會增加，數字和路徑之間不應出現空格。<br /><br /> 範例項目： <code>80|/etc/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>字串</td>
   <td><em>（可選）</em> ，將計分引擎識別為「基本」或「進階」。 如果需要進階計分引擎，請參閱進階 <a href="/help/communities/advanced.md">計分和標章</a>。 預設值為「basic」。</td>
  </tr>
  <tr>
   <td>計分規則</td>
   <td>String[]</td>
   <td>(可<em>選</em>)多值字串，可將標籤規則限制為由計分規則識別的計分事件</td>
  </tr>
 </tbody>
</table>

### 包含的標籤規則 {#included-badging-rules}

此發行包含兩個與論壇和留言計分規則對 [應的標籤規則](#includedscoringrules)。

* /etc/community/badging/rules/comments-badging
* /etc/community/badging/rules/forums-badging

**附註:**

* `rules` 節點的類型cq:Page
* `rules`應位於具有每個人的讀取權限的儲存庫位置

   * 規則名稱必須是唯一的，不論位置

### 啟用自訂標籤規則 {#activating-custom-badging-rules}

在作者環境中對標籤規則或影像所做的任何變更或新增動作都必須安裝在發佈上。

## 指派和撤銷標章 {#assign-and-revoke-badges}

可以使用成員控制台或使用cURL命令 [以寫程式方式](/help/communities/members.md#badges-tab) ，將標章分配給成員。

下列cURL命令顯示HTTP要求指派和廢止標章的必要項。 基本格式為：

cURL -i -X POST -H標 *題* -u *signin * -F *操作* -F *badge * *member-profile-url*

*header* = &quot;Accept:application/json&quot;自訂標題，以傳遞至伺服器（必要）

*signin* = administrator-id:password，例如：admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = badge映像檔案在儲存庫中的位置，例如：/etc/community/badging/images/coldrator/jcr/content/moderator.png

*member-profile-url* =發佈時成員配置檔案的端點，例如：https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>成 *員-profile-url*
>
>* 如果已啟用「隧道服務」，則 [可參照作者實例](/help/communities/users.md#tunnel-service) 。
>* 可能是模糊的隨機名稱——請參閱安全性檢 [查清單](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) ，瞭解可授權ID
>



### 範例： {#examples}

#### 指派協調者徽章 {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/etc/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### 撤銷指派的銀色徽章 {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/etc/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>使用cURL指派和撤銷標章適用於任何標章影像，但當指派標章（而非獲得）時，它們會標示為已指派的標章並據以處理。

## 自訂元件的計分和標章 {#scoring-and-badges-for-custom-components}

可通過將為元件建立的事件主題與動詞關聯，為自定義元件建立計分和標籤規則。

## 主題和動詞 {#topics-and-verbs}

當成員與社群功能互動時，會傳送可觸發非同步接聽程式的事件，例如通知和計分。

元件的SocialEvent例項會將事件記 `actions`錄為發生的 `topic`。 SocialEvent包含傳回與動作相 `verb`關聯的方法。 和之 *間有* n- `actions`1關係 `verbs`。

對於傳遞的社群元件，下表說明可 `verbs`用於計 `topic`分子規則 [的每個定義](#scoring-sub-rules)。

>[!NOTE]
>
>新的布林屬性 `allowBadges`，可啟用／停用元件例項的標章顯示。 它可透過標示為「顯示標章」的核 [取方塊，在更新的元件編輯](/help/communities/author-communities.md) 對話 **方塊中設定**。

**[行事歷元](/help/communities/calendar.md)**件SocialEvent`topic`= com/adobe/cq/social/calendar

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立日曆事件 |
| 新增 | 日曆事件上的成員注釋 |
| 更新 | 會編輯成員的日曆事件或注釋 |
| 刪除 | 會員的日曆事件或留言已刪除 |

**[Comments Component](/help/communities/comments.md)**SocialEvent`topic`= com/adobe/cq/social/comment

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立注釋 |
| 新增 | 成員回覆評論 |
| 更新 | 已編輯成員的注釋 |
| 刪除 | 會員的注釋已刪除 |

**[檔案庫元件](/help/communities/file-library.md)**SocialEvent`topic`= com/adobe/cq/social/fileLibrary

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立資料夾 |
| 附加 | 成員上傳檔案 |
| 更新 | 成員更新資料夾或檔案 |
| 刪除 | 成員刪除資料夾或檔案 |

**[論壇元件](/help/communities/forum.md)**SocialEvent`topic`= com/adobe/cq/social/forum

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立論壇主題 |
| 新增 | 成員對論壇主題的回覆 |
| 更新 | 編輯成員的論壇主題或回覆 |
| 刪除 | 會員的論壇主題或回覆被刪除 |

**[Journal Component](/help/communities/blog-feature.md)**SocialEvent`topic`= com/adobe/cq/social/journal

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立部落格 |
| 新增 | 部落格文章中的成員注釋 |
| 更新 | 會編輯會員的部落格文章或留言 |
| 刪除 | 會員的部落格文章或留言已刪除 |

**[QnA元件](/help/communities/working-with-qna.md)**SocialEvent`topic`= com/adobe/cq/social/qna

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立QnA問題 |
| 新增 | 成員建立QnA答案 |
| 更新 | 成員的QnA問題或答案已編輯 |
| 選擇 | 已選擇成員的答案 |
| 取消選擇 | 會員的答案為取消選擇 |
| 刪除 | 刪除成員的QnA問題或答案 |

**[Reviews Component](/help/communities/reviews.md)**SocialEvent`topic`= com/adobe/cq/social/review

| **動詞** | **說明** |
|---|---|
| 貼文 | 成員建立審閱 |
| 更新 | 會員的審核已編輯 |
| 刪除 | 會員的審核已刪除 |

**[評分元件](/help/communities/rating.md)**SocialEvent`topic`= com/adobe/cq/social/tally/rating

| **動詞** | **說明** |
|---|---|
| 新增評分 | 會員的內容已被評級 |
| 移除評分 | 會員的內容已降級 |

**[投票元件](/help/communities/voting.md)**SocialEvent`topic`= com/adobe/cq/social/tally/poting

| **動詞** | **說明** |
|---|---|
| 新增投票 | 會員的內容已通過投票 |
| 移除投票 | 會員的內容已被否決 |

**已啟用協調的元**&#x200B;件SocialEvent `topic`= com/adobe/cq/social/協調

| **動詞** | **說明** |
|---|---|
| 拒絕 | 會員的內容被拒絕 |
| 不適當的旗幟 | 會員的內容已標籤 |
| 取消標幟為不當 | 會員的內容已取消標幟 |
| 接受 | 會員的內容由協調者核准 |
| 關閉 | 成員關閉編輯和回覆的注釋 |
| 開啟 | 成員重新開啟注釋 |

### 自訂元件事件 {#custom-component-events}

對於自訂元件，會執行個體化SocialEvent，以記錄元件的事 `actions`件為發生 `topic`。

若要支援計分，SocialEvent需要覆寫方法， `getVerb()` 以便針對每 `verb`個方法傳回適當 `action`。 針 `verb` 對動作傳回的可能是常用(例如 `POST`)或專用於元件(例如 `ADD RATING`)。 和之 *間有* n- `actions`1關係 `verbs`。

## 疑難排解 {#troubleshooting}

### 徽章未顯示 {#badges-are-not-appearing}

如果已將分數和徽章規則套用至網站的內容，但未察覺任何活動的徽章，請確定已為該元件的例項啟用徽章。

請參 [閱啟用元件標章](#enable-badges-for-component)。

### 計分規則無效 {#scoring-rule-has-no-effect}

如果已對網站內容套用計分和徽章規則，且某些動作（但非其他動作）會授與徽章，請檢查徽章規則是否未限制套用的計分規則。

請參閱 `scoringRules`標籤規 [則的屬性](#badging-rules)。

### 區分大小寫錯字 {#case-sensitive-typo}

大部分的屬性和值，尤其是動詞，都會區分大小寫。 在計分子規則中使用動詞時，必須全部為大寫。

如果功能未如預期運作，請確定資料已正確輸入。

## 快速測試 {#quick-test}

使用快速入門教學課程（參與）網站， [快速嘗試計分](/help/communities/getting-started.md) 和標籤：

* 在作者上存取CRXDE Lite
* 瀏覽至基本頁：

   * /content/sites/engage/tw/jcr:content

* 添加badgingRules屬性：

   * **名稱**: `badgingRules`
   * **類型**: `String`
   * 選擇多 **個**
   * 選擇添 **加**
   * enter `/etc/community/badging/rules/forums-badging`
   * select **+**
   * enter `/etc/community/badging/rules/comments-badging`
   * 選擇確 **定**

* 添加scoringRules屬性：

   * **名稱**: `scoringRules`
   * **類型**: `String`
   * 選擇多 **個**
   * 選擇添 **加**
   * enter `/etc/community/scoring/rules/forums-scoring`
   * select **+**
   * enter `/etc/community/scoring/rules/comments-scoring`
   * 選擇確 **定**

* 選擇「 **全部保存」**

![chlimage_1-102](assets/chlimage_1-102.png)

接下來，請確定論壇和注釋元件允許顯示標章：

* 再次使用CRXDE Lite
* 瀏覽至論壇元件

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* 如有必要，請新增allowBadges布林屬性，並確保其為true

   * **名稱**: `allowBadges`
   * **類型**: `Boolean`
   * **值**: `true`

![chlimage_1-103](assets/chlimage_1-103.png)

接著， [重新發佈](/help/communities/sites-console.md#publishing-the-site) 社群網站。

最後，

* 瀏覽至發佈例項上的元件
* 以社群成員身分登入(例如：weston.mccall@dodgit.com /密碼)
* 張貼新論壇主題
* 頁面必須重新整理，才能顯示徽章

   * 註銷並以不同的社區成員身份登錄(例如：aaron.mcdonald@mailinator.com/password)

* 選擇論壇

這應該會為社群成員贏得銅像徽章，其論壇貼文會顯示此徽章，因為第一個論壇徽章規則的第一個臨界值為1。

![鑄幣](assets/bronzebadge.png)

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員 [的「計分與標章](/help/communities/configure-scoring.md) 」頁面。

如需進階計分引擎的詳細資訊，請參 [閱進階計分和徽章](/help/communities/advanced.md)。

可配置的Leerboard組 [件](/help/communities/enabling-leaderboard.md)[和函式](/help/communities/functions.md#leaderboard-function) ，可簡化成員在社區站點上的顯示及其分數。
