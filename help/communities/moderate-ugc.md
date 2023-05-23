---
title: 調節社區內容
seo-title: Moderating Community Content
description: 審核概念和操作
seo-description: Moderation concepts and actions
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 2%

---

# 調節社區內容 {#moderating-community-content}

## 概觀 {#overview}

當成員（登錄站點訪問者）通過與下列社區元件之一進行交互從已發佈社區站點發佈內容時，將建立社區內容(也稱為用戶生成內容(UGC)):

* [部落格](/help/communities/blog-feature.md):成員發佈部落格或評論。
* [日曆](/help/communities/calendar.md):成員會發佈日曆事件或注釋。
* [注釋](/help/communities/comments.md):成員會發佈評論或回複評論。

* [論壇](/help/communities/forum.md):成員會發佈新主題或對主題的回復。
* [想像](/help/communities/ideation-feature.md):成員會發佈想法或評論。
* [QnA](/help/communities/working-with-qna.md):成員會建立問題或回答問題。
* [評論](/help/communities/reviews.md):成員在對項進行評級時發佈評語。

UGC的適當性對於承認積極貢獻和限制消極貢獻（如垃圾郵件和辱罵語言）是有用的。 UGC可以從以下幾個環境中審核：

* [社區內容儲存](working-with-srp.md)

* [批量審核控制台](moderation.md)

   管理員可以訪問「審核」控制台， [社區管理者](/help/communities/users.md) 以及作者環境中的管理員。 當社區內容儲存在 [普通商店](/help/communities/working-with-srp.md)。

* [上下文中的調節](in-context.md)

   發佈環境中的審核可由管理員和社區審核人員直接在發佈內容的頁面上執行。

## 審核操作 {#moderation-actions}

可以對已發佈內容(UGC)執行的操作會因用戶身份和環境而異。 下表使用以下術語根據用戶身份描述各種角色：

* `Admin`

   屬於 [社區管理員](users.md) 組。

* `Moderator`

   成員 [社區管理者](users.md#publishenvironmentusersandgroups) 組 [版權](in-context.md#moderatorpermissions))。

* `Creator`

   發佈內容的用戶。

* `Member`

   沒有特殊權限的登錄用戶。

* `Visitor`

   匿名用戶。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>管理員</strong></td>
   <td><strong>版主</strong></td>
   <td><strong>建立者</strong></td>
   <td><strong>成員</strong></td>
   <td><strong>訪問者</strong></td>
   <td><strong>事件<br /> 已觸發</strong></td>
   <td><strong>預審</strong></td>
  </tr>
  <tr>
   <td><strong>編輯/<br /> 刪除</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>剪下</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>拒絕</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>關閉/<br /> 重新開啟</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>標誌/<br /> 取消標籤</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>允許</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### 編輯/刪除 {#edit-delete}

發佈後，建立者、管理員或社區版主可以編輯或刪除該帖子。

刪除UGC時，它將從儲存庫中刪除，並且可能無法恢復。

### 剪下 {#cut}

管理員或社區主持人可以將一個或多個論壇主題或QnA問題從一個位置移動到另一個位置。 這包括從一個社區站點到另一個社區站點，前提是同一成員在兩個站點上都具有審核權限。

通過選擇「剪切」(Cut)操作，內容將複製到剪貼簿。 可以將多個帖子作為組複製並移動到新位置。

![牙形](assets/cutugc.png)

![putbackug](assets/putbackugc.png)

在另一位置，當剪貼簿中存在內容時，「新建帖子」旁邊將顯示「貼上」按鈕，其編號標識將貼上的帖子數。 「貼上」(Paste)按鈕包含一個選項，用於清除剪貼簿而不是貼上。

![巴斯德](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### 拒絕 {#deny}

版主可能不允許UGC在已發佈的站點上保持可見。 對於管理員和社區版主，帖子仍然可用，並且批注為垃圾郵件。

### 關閉/重新開啟 {#close-reopen}

「關閉」操作在整個對話線程（論壇主題或初始評論）上運行，並包括所有後續帖子或回復。

關閉後，不僅不可能再進行回復，也不允許執行任何審核操作。

要執行任何操作，必須重新開啟主題或注釋。

「關閉/重新開啟」(Close/Reopen)操作可由管理員或社區審閱人執行。

### 標籤/取消標籤 {#flag-unflag}

標籤是任何登錄成員（內容建立者除外）的一種方法，用於指示帖子的內容存在問題。 標籤後，將出現取消標籤表徵圖，允許同一成員取消標籤內容。

可以將上下文內審核配置為允許成員在標籤帖子時選擇原因。 可配置可選標誌原因清單，包括是否可以輸入自定義原因。 標籤原因與UGC一起保存，但該原因不會觸發任何特定操作。 只有標誌數才會觸發通知。 標籤的內容被這樣標注，以便審閱人可以對其採取行動。

系統跟蹤標籤的所有標誌和標誌原因，並在達到閾值時發送事件。 如果社區版主允許UGC，則這些標誌將存檔。 在允許和歸檔後，如果有後續的放大，則會將其歸檔，就像以前沒有放大一樣。

### 允許 {#allow}

「允許」操作是UGC的選項，該選項已標籤、拒絕或未在預審核的系統中獲得批准。 「允許」操作將清除任何已標籤或拒絕/垃圾郵件狀態，並存檔任何已標籤的資料。

## 常見審核概念 {#common-moderation-concepts}

### 預審 {#premoderation}

當UGC被預審核時，該帖子將不會出現在發佈的站點上，直到審核操作批准。 建立期間 [社區站點](/help/communities/sites-console.md)，選中該框 [內容已預審](sites-console.md#moderation) 將啟用整個站點的預審。 一旦將元件放在頁面上，支援審核的元件就可以使用其編輯對話框中的設定配置為預審核：

* [注釋](comments.md) 和 [回顧](reviews.md)
在 **[!UICONTROL 用戶審核]** > **[!UICONTROL 預審核]**。

* [論壇](/help/communities/forum.md)。 [識別](/help/communities/ideation-feature.md)。 [QnA](/help/communities/working-with-qna.md), [日曆](/help/communities/calendar.md)
在 **[!UICONTROL 設定]** > **[!UICONTROL 已審核]**。

### 垃圾郵件檢測 {#spam-detection}

垃圾郵件檢測是一種自動審核功能，它通過將提交的用戶生成的內容標籤為垃圾郵件來過濾掉不可期望的內容。 一旦啟用，它基於預先配置的垃圾郵件詞集合來識別用戶生成的內容是否是垃圾郵件。 預設垃圾郵件詞提供於

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`。

但是，要自定義或擴展預設垃圾郵件詞，請通過以下方式在/apps目錄中建立一組預設垃圾郵件詞的結構 [覆蓋](/help/communities/overlay-comments.md)。

用戶生成的包含垃圾郵件詞的帖子（跨所有內容類型，如部落格、論壇和評論）在帖子上方標有「此帖子被分類為垃圾郵件」。

版主可以查看此類帖子並標籤相同以允許或拒絕在站點上出現。 這些帖子的審核操作可以在上下文中執行，也可以通過批量審核UI執行。

![垃圾檢測](assets/spamdetection.png)

要啟用垃圾郵件檢測引擎，請執行以下步驟：

1. 開啟 [Web控制台](https://localhost:4502/system/console/configMgr)，通過 `/system/console/configMgr`。

1. 定位 **AEM Communities汽車節** 配置，並對其進行編輯。
1. 添加 **[!UICONTROL 垃圾郵件進程]** 的子菜單。

![垃圾郵件](assets/spamprocess.png)

>[!NOTE]
>
>垃圾郵件檢測僅針對英語區域設定實施。

### 情緒 {#sentiment}

情緒根據正和負關鍵字的數目計算([口號](#configuringwatchwords))。

情緒分析使用一組預先配置的規則並計算UGC的情緒。 預設規則位於： `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

規則生成的值從1（所有為負，沒有為正的字）到10（所有為正，沒有為負的字）。 情緒值為5是中性情緒，是違約。

/libs元件中定義的規則有：

* 規則1:如果沒有正詞且至少有一個負詞，則將值設定為1。
* 規則2:如果沒有負詞和至少一個正詞，則將值設定為10。
* 規則3:如果負詞多於正詞，則將值設定為3。
* 規則4:如果正詞多於負詞，則將值設定為8。

要覆蓋或添加規則，請在/apps目錄中按照預設規則的結構建立一組規則。 編輯情緒配置以標識規則的位置。

分析後，情緒與UGC一起儲存。

從 [批量調整控制台](/help/communities/moderation.md)，可以根據情緒是否為負、中性還是正性來過濾和查看UGC。

#### 守望詞 {#watchwords}

AEM社區提供 *監視器* 作為評估 [情緒](#sentiment)。 對表詞所提供的情緒值的貢獻是，對已發佈內容中使用的負面和正面表詞以及禁止的詞語進行比較。

#### 配置情緒和監視詞 {#configure-sentiment-and-watchwords}

可以定制正反的口號清單，也可以定制情感規則。

預設的監視字清單可以作為儲存庫中某個節點的屬性輸入，與預設值類似，或通過配置OSGi服務覆蓋預設值 `sentimentprocess.name` 和單詞表。

的 **sentive process.name** 也可以修改以引用自定義情緒規則集的位置。

要配置情緒和口令：

* 以管理員身份登錄到作者實例。
* 開啟 [Web控制台](https://localhost:4502/system/console/configMgr)。
* 定位 `sentimentprocess.name`。
* 選擇要在編輯模式下開啟的配置。

![感知過程](assets/sentimentprocess.png)

* **正表詞**

   以逗號分隔的詞清單，它會產生覆蓋預設值的正面情緒。 預設為空清單。

* **負值監視詞**

   以逗號分隔的詞清單，它會導致覆蓋預設值的負面情緒。 預設為空清單。

* **監視詞節點的顯式路徑**

   包含預設值的節點的儲存庫位置 `positive` 和 `negative` 指定預設監視字的屬性。 預設值為 `/libs/settings/community/watchwords/default`。

* **情緒規則**

   用於基於正和負的監視詞計算情緒的規則的儲存庫位置。 預設值為 `/libs/cq/workflow/components/workflow/social/sentiments/rules` （但是，不再涉及任何工作流）。

以下是預設監視詞的自定義項示例， `Explicit Path to Watchwords Node` 設定為 `/libs/settings/community/watchwords/default`。

![克克斯德](assets/crxde.png)

### 版主權限 {#moderator-permissions}

當分配給同一資源時，以下權限統稱為 `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
