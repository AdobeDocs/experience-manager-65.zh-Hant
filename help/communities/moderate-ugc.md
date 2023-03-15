---
title: 調節社群內容
seo-title: Moderating Community Content
description: 協調概念和動作
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
ht-degree: 1%

---

# 調節社群內容 {#moderating-community-content}

## 概觀 {#overview}

當成員（登入網站訪客）透過與下列其中一個社群元件互動來發佈來自已發佈社群網站的內容時，會建立社群內容(也稱為使用者產生的內容(UGC)):

* [部落格](/help/communities/blog-feature.md):成員發佈部落格文章或評論。
* [日曆](/help/communities/calendar.md):成員發佈日曆事件或留言。
* [註解](/help/communities/comments.md):成員發佈評論或回複評論。

* [論壇](/help/communities/forum.md):成員發佈新主題或回復主題。
* [構思](/help/communities/ideation-feature.md):成員發佈構想或留言。
* [QnA](/help/communities/working-with-qna.md):成員可建立問題或回答問題。
* [評論](/help/communities/reviews.md):成員在評分項目時發佈評論。

UGC的調節有助於識別正面貢獻以及限制負面貢獻（例如垃圾訊息和辱罵性語言）。 UGC可從數個環境中審核：

* [社群內容儲存](working-with-srp.md)

* [大量協調主控台](moderation.md)

   管理員和 [社群協調者](/help/communities/users.md) 以及作者環境中的管理員。 當社群內容儲存在 [公用商店](/help/communities/working-with-srp.md).

* [內容內協調](in-context.md)

   發佈環境中的協調可由管理員和社群協調者直接在發佈內容的頁面上執行。

## 協調動作 {#moderation-actions}

可對發佈內容(UGC)執行的動作會依使用者身分和環境而有所不同。 下表使用下列術語，根據使用者身分說明各種角色：

* `Admin`

   屬於 [社群管理員](users.md) 群組。

* `Moderator`

   成員 [社群協調者](users.md#publishenvironmentusersandgroups) 群組(具有 [版主權限](in-context.md#moderatorpermissions))。

* `Creator`

   發佈內容的使用者。

* `Member`

   沒有特殊權限的登入使用者。

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
   <td><strong>訪客</strong></td>
   <td><strong>事件<br /> 觸發</strong></td>
   <td><strong>已預先審核</strong></td>
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
   <td><strong>標幟/<br /> 取消標幟</strong></td>
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

貼文發表後，建立者、管理員或社群版主可以編輯或刪除貼文。

刪除UGC後，該UGC將從儲存庫中刪除，並且可能無法恢復。

### 剪下 {#cut}

管理員或社區協調者可以將一個或多個論壇主題或QnA問題從一個位置移動到另一個位置。 這包括從一個社群網站到另一個社群網站，前提是同一成員在這兩個網站上都擁有協調權限。

選取「剪下」動作後，內容會複製到剪貼簿。 多則貼文可以複製，並以群組形式移動至新位置。

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

在另一個位置，當剪貼簿中出現內容時，新貼文旁會顯示「貼上」按鈕，其中數字代表將貼上的貼文數量。 「貼上」按鈕包含清除剪貼簿而非貼上的選項。

![貼上](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### 拒絕 {#deny}

版主可能不允許UGC在已發佈的網站上保持可見。 對於管理員和社群協調者，貼文仍可供使用，且會加上垃圾訊息注釋。

### 關閉/重新開啟 {#close-reopen}

「關閉」動作會針對整個對話線程（論壇主題或初始評論）執行，並包含所有後續貼文或回覆。

關閉時，不僅無法進一步回覆，也不允許任何協調動作。

要執行任何操作，主題或注釋必須重新開啟。

管理員或社群協調者可以執行「關閉/重新開啟」動作。

### 標幟/取消標幟 {#flag-unflag}

標幟是任何已登入成員（內容的建立者除外）的方法，用以指出貼文內容有問題。 標籤後，會出現取消標幟圖示，讓相同的成員取消標幟內容。

內容內協調可設定為允許成員在標籤貼文時選取原因。 可配置可選標誌原因清單，包括是否可輸入自定義原因。 標幟原因會以UGC儲存，但原因不會觸發任何特定動作。 只有標幟數會觸發通知。 標幟內容會以此方式加上註解，以便協調者可依此方式行動。

系統會追蹤所有已標幟、已標幟以及標幟原因，並在達到臨界值時傳送事件。 如果社群版主允許UGC，則會封存這些標幟。 在允許和歸檔後，如果有後續的標籤，則會將其歸檔，就像以前沒有標籤一樣。

### 允許 {#allow}

「允許」動作是UGC的選項，其已標籤、拒絕或未在預先審核的系統中核准。 「允許」動作會清除任何已標幟或已拒絕/垃圾訊息狀態，並封存任何已標幟資料。

## 常見的協調概念 {#common-moderation-concepts}

### 預先協調 {#premoderation}

UGC經過預先審核後，貼文在經過協調動作核准後，才會顯示在已發佈的網站上。 建立 [社群網站](/help/communities/sites-console.md)，勾選方塊 [內容已預先審核](sites-console.md#moderation) 會為整個網站啟用預先協調。 將元件放在頁面上後，即可使用其編輯對話方塊中的設定，將支援協調的元件設定為預先協調：

* [註解](comments.md) 和 [評論](reviews.md)
in **[!UICONTROL 使用者協調]** > **[!UICONTROL 預先協調]**.

* [論壇](/help/communities/forum.md), [識別](/help/communities/ideation-feature.md), [QnA](/help/communities/working-with-qna.md)，和 [日曆](/help/communities/calendar.md)
in **[!UICONTROL 設定]** > **[!UICONTROL 已審核]**.

### 垃圾郵件檢測 {#spam-detection}

垃圾訊息偵測是自動協調功能，可將提交的使用者產生的內容標示為垃圾訊息，以篩選掉不想要的片段。 啟用後，它會根據預先設定的垃圾訊息集合來識別使用者產生的內容是否為垃圾訊息。 預設的垃圾郵件字詞提供於

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`。

但是，要自定義或擴展預設垃圾郵件字詞，請通過 [覆蓋](/help/communities/overlay-comments.md).

使用者產生的包含垃圾訊息字詞的貼文（涵蓋所有內容類型，例如部落格、論壇和留言），在貼文上方會標示為「此貼文已分類為垃圾訊息」。

版主可以看到這樣的貼文，並標示相同的貼文，以允許或拒絕出現在網站上。 這些貼文的協調動作可在內容內或透過大量協調UI來執行。

![垃圾郵件檢測](assets/spamdetection.png)

要啟用垃圾郵件檢測引擎，請執行以下步驟：

1. 開啟 [Web主控台](https://localhost:4502/system/console/configMgr)，前往 `/system/console/configMgr`.

1. 找出 **AEM Communities自動協調** 設定，並加以編輯。
1. 新增 **[!UICONTROL SpamProcess]** 的下界。

![垃圾郵件處理](assets/spamprocess.png)

>[!NOTE]
>
>垃圾郵件檢測僅針對英語區域設定實施。

### 情緒 {#sentiment}

情緒是根據正面和負面關鍵字的數量([觀看詞](#configuringwatchwords))存在於貼文(UGC)中。

情緒分析使用一組預先設定的規則，並計算UGC的情緒。 預設規則位於： `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

規則產生的值從1（所有負面，無正面字詞）到10（所有正面，無負面字詞）。 情緒值5為中性情緒，為預設值。

/libs元件中定義的規則為：

* 規則1:如果沒有正面字詞和至少一個負面字詞，請將值設為1。
* 規則2:如果沒有負面字詞和至少一個正面字詞，請將值設為10。
* 規則3:如果負面字詞多於正面字詞，請將值設為3。
* 第4條：如果正面字詞多於負面字詞，請將值設為8。

若要覆寫或新增規則，請依照預設規則的結構，在/apps目錄中建立一組規則。 編輯情緒設定以識別規則的位置。

分析後，情緒會與UGC一起儲存。

從 [大量協調控制台](/help/communities/moderation.md)，您可以根據情緒是負面、中性或正面來篩選及檢視UGC。

#### 口碑 {#watchwords}

AEM communities提供 *watchword分析器* 作為評估 [情緒](#sentiment). 關注字詞對情緒值的貢獻，是因為張貼內容中使用的負面和正面關注字詞，以及禁止字詞的比較。

#### 設定情緒和觀看字詞 {#configure-sentiment-and-watchwords}

正面和負面觀看字清單可自訂，因為可以是情緒規則。

預設的監看字清單可以作為儲存庫中節點的屬性輸入，類似於預設值，或通過配置OSGi服務來覆蓋預設值 `sentimentprocess.name` 用詞清單。

此 **sentimentprocess.name** 也可修改以參考自訂情緒規則集的位置。

若要設定情緒和口號：

* 以管理員身分登入您的製作執行個體。
* 開啟 [Web主控台](https://localhost:4502/system/console/configMgr).
* 找出 `sentimentprocess.name`.
* 選取要在編輯模式中開啟的設定。

![情緒過程](assets/sentimentprocess.png)

* **正面的口號**

   導致正面情緒覆寫預設值的以逗號分隔字詞清單。 預設為空白清單。

* **負面觀看詞**

   導致負面情緒的字詞清單（以逗號分隔）會覆寫預設值。 預設為空白清單。

* **觀看詞節點的明確路徑**

   包含預設值的節點的儲存庫位置 `positive` 和 `negative` 指定預設監看字的屬性。 預設為 `/libs/settings/community/watchwords/default`.

* **情緒規則**

   根據正面和負面關鍵字計算情緒之規則的存放庫位置。 預設為 `/libs/cq/workflow/components/workflow/social/sentiments/rules` （不過，不再涉及任何工作流程）。

以下是預設關注字詞的自訂項目範例，當 `Explicit Path to Watchwords Node` 設為 `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### 版主權限 {#moderator-permissions}

將下列權限指派給相同資源時，統稱為 `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
