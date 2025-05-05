---
title: 仲裁社群內容
description: 瞭解如何稽核使用者產生的內容，以便您識別正面貢獻並限制負面貢獻，例如垃圾郵件和辱罵性語言。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 2%

---

# 仲裁社群內容 {#moderating-community-content}

## 概觀 {#overview}

社群內容(也稱為使用者產生的內容(UGC))是在成員（登入網站訪客）透過與下列社群元件之一的互動從已發佈的社群網站張貼內容時建立的：

* [部落格](/help/communities/blog-feature.md)：會員發表部落格或評論。
* [行事曆](/help/communities/calendar.md)：成員張貼行事曆事件或註解。
* [註解](/help/communities/comments.md)：成員張貼註解或回覆註解。

* [論壇](/help/communities/forum.md)：成員張貼新主題或回覆主題。
* [創意力](/help/communities/ideation-feature.md)：成員發表創意或評論。
* [QnA](/help/communities/working-with-qna.md)：成員建立問題或回答問題。
* [評論](/help/communities/reviews.md)：成員在評等專案時發表評論。

UGC的稽核對於識別正面貢獻和限制負面貢獻很有用（例如垃圾郵件和辱罵語言）。 UGC可從數個環境中稽核：

* [社群內容儲存](working-with-srp.md)

* [大量仲裁主控台](moderation.md)

  公共環境中的管理員和[社群版主](/help/communities/users.md)以及作者環境中的管理員可存取版主主控台。 當社群內容儲存在[公用存放區](/help/communities/working-with-srp.md)中時，便可以執行此作業。

* [內容中稽核](in-context.md)

  管理員和社群版主可直接在發佈內容的頁面上執行Publish環境中的版主。

## 稽核動作 {#moderation-actions}

可以對發佈內容(UGC)執行的動作會因使用者身分和環境而異。 下表使用下列術語，根據使用者身分說明各種角色：

* `Admin`

  [社群管理員](users.md)群組成員的使用者。

* `Moderator`

  [社群版主](users.md#publishenvironmentusersandgroups)群組的成員（具有[版主許可權](in-context.md#moderatorpermissions)）。

* `Creator`

  發佈內容的使用者。

* `Member`

  沒有特殊許可權的登入使用者。

* `Visitor`

  匿名使用者。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>管理員</strong></td>
   <td><strong>版主</strong></td>
   <td><strong>建立者</strong></td>
   <td><strong>成員</strong></td>
   <td><strong>訪客</strong></td>
   <td><strong>事件<br />已觸發</strong></td>
   <td><strong>已預先稽核</strong></td>
  </tr>
  <tr>
   <td><strong>編輯/<br />刪除</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>剪切</strong></td>
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
   <td><strong>關閉/<br />重新開啟</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>標幟/<br />取消標幟</strong></td>
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

貼文發表後，建立者、管理員或社群版主可能會編輯或刪除貼文。

刪除UGC時，它會從存放庫中移除，並且可能無法復原。

### 剪切 {#cut}

管理員或社群版主可以將一個或多個論壇主題或QnA問題從一個位置移動到另一個位置。 這包括從一個社群網站到另一個社群網站，前提是相同的成員在兩個網站上都有仲裁許可權。

透過選取「剪下」動作，內容會複製到剪貼簿。 可以複製多個貼文，並將其作為一個群組移動到新位置。

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

在另一個位置，當內容顯示在剪貼簿中時，新Post旁會顯示「貼上」按鈕，其中數字可識別將貼上的貼文數量。 「貼上」按鈕包含清除剪貼簿而非貼上的選項。

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### 拒絕 {#deny}

版主可不允許UGC在已發佈的網站上保持可見。 對於管理員和社群版主，該貼文仍可用，並標籤為垃圾訊息。

### 關閉/重新開啟 {#close-reopen}

「關閉」動作會作用於對話的整個對話串（論壇主題或初始評論），並包含所有後續的貼文或回覆。

關閉後，不僅無法進一步回覆，也不允許協調動作。

若要執行任何操作，必須重新開啟主題或註解。

管理員或社群版主可能會執行「關閉/重新開啟」動作。

### 標幟/取消標幟 {#flag-unflag}

標幟是任何登入成員（內容建立者除外）表示貼文內容存在問題的一種方式。 標幟後，取消標幟圖示就會顯示，允許同一成員取消標幟內容。

內容內稽核可設定為允許成員在標幟貼文時選取原因。 可選擇的旗標原因清單是可設定的，包括是否可以輸入自訂原因。 標幟原因會與UGC一併儲存，但原因不會觸發任何特定動作。 僅觸發通知的旗標數。 已標幟的內容會依此進行註解，以便版主可對其採取行動。

系統會追蹤所有標幟及標幟原因，並在達到臨界值時傳送事件。 如果社群版主允許UGC，則會封存這些標幟。 允許並封存之後，如果有後續標幟，則會封存這些標幟，就像之前沒有標幟一樣。

### 允許 {#allow}

對於已標幟、已拒絕或未在預先稽核系統中核准的UGC，允許動作是一個選項。 允許動作會清除任何存在的已標幟或已拒絕/垃圾郵件狀態，並封存任何已標幟的資料。

## 常見的稽核概念 {#common-moderation-concepts}

### 預先稽核 {#premoderation}

UGC預先稽核時，帖子要等到稽核動作核准後才會出現在已發佈的網站上。 建立[社群網站](/help/communities/sites-console.md)期間，勾選[內容已預先稽核](sites-console.md#moderation)方塊可啟用整個網站的預先稽核。 將元件放置在頁面上時，可使用編輯對話方塊中的設定，將支援稽核的元件設定為可預先稽核：

* [評論](comments.md)和[評論](reviews.md)
在&#x200B;**[!UICONTROL 使用者稽核]** > **[!UICONTROL 預先稽核]**&#x200B;中。

* [論壇](/help/communities/forum.md)、[構思](/help/communities/ideation-feature.md)、[QnA](/help/communities/working-with-qna.md)和[行事曆](/help/communities/calendar.md)
在&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 已稽核]**&#x200B;中。

### 垃圾郵件偵測 {#spam-detection}

垃圾郵件偵測是一種自動稽核功能，會透過將提交的使用者產生的內容標籤為垃圾郵件來篩選掉不需要的片段。 一旦啟用，它會根據預先設定的垃圾郵件字詞集合來識別使用者產生的內容是否為垃圾郵件。 預設垃圾訊息字詞提供於

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`。

但是，若要自訂或延伸預設垃圾郵件，請在/apps目錄中建立一組文字並遵循具有[覆蓋](/help/communities/overlay-comments.md)的預設垃圾郵件的字結構。

使用者產生的貼文（涵蓋所有內容型別，例如部落格、論壇和評論）若包含垃圾訊息，會在貼文上方標示「此貼文被分類為垃圾訊息」文字。

版主可以看到這類貼文，並加以標示，以允許或拒絕出現在網站上。 這些貼文上的稽核動作可在內容中或透過大量稽核UI執行。

![垃圾郵件偵測](assets/spamdetection.png)

若要啟用垃圾郵件偵測引擎，請執行下列步驟：

1. 前往`/system/console/configMgr`開啟[網頁主控台](https://localhost:4502/system/console/configMgr)。

1. 找到&#x200B;**AEM Communities自動調節**&#x200B;設定並加以編輯。
1. 新增&#x200B;**[!UICONTROL SpamProcess]**&#x200B;專案。

![spamprocess](assets/spamprocess.png)

>[!NOTE]
>
>垃圾郵件偵測僅針對英文地區設定實施。

### 情緒 {#sentiment}

情緒是根據貼文(UGC)中出現的正面和負面關鍵字（[關注字詞](#configuringwatchwords)）數目計算的。

情緒分析使用一組預先設定的規則，並計算UGC的情緒。 預設規則為`/libs/cq/workflow/components/workflow/social/sentiments/rules`。

規則產生的值介於1 （全是負值，沒有正字）到10 （全是正值，沒有負值）之間。 情緒值5是中性情緒，且為預設值。

/libs元件中定義的規則為：

* 規則1：如果沒有正面字詞和至少一個負面字詞，則將值設為1。
* 規則2：如果沒有負面字詞和至少一個正面字詞，則將值設為10。
* 規則3：如果負面字數多於正面字數，則將值設為3。
* 規則4：如果正面字數多於負面字數，則將值設為8。

若要覆寫或新增規則，請依照預設規則的結構在/apps目錄中建立一組規則。 編輯情緒設定，以便識別規則的位置。

分析後，該情緒會與UGC一併儲存。

在[大量仲裁主控台](/help/communities/moderation.md)中，可以根據情緒是負面、中性或正面來篩選和檢視UGC。

#### 關注字詞 {#watchwords}

AEM Communities提供&#x200B;*關注字分析器*，作為評估[情緒](#sentiment)的程式中的步驟。 關注字詞對人氣值的貢獻來自於對張貼內容中使用的負面和正面關注字詞與禁止字詞的比較。

#### 設定情緒和關注字詞 {#configure-sentiment-and-watchwords}

正面和負面標語清單可自訂，如同情緒規則一樣。

預設的關注字清單可以輸入為存放庫中節點的屬性，類似於預設值，或透過使用字清單設定OSGi服務`sentimentprocess.name`來覆寫預設值。

**sentimentprocess.name**&#x200B;也可以修改為參考自訂情緒規則集的位置。

若要設定情緒和關注字詞：

* 以管理員身分登入您的作者執行個體。
* 開啟[網頁主控台](https://localhost:4502/system/console/configMgr)。
* 找到`sentimentprocess.name`。
* 選取設定，以便您可以在編輯模式中開啟它。

![sentimentprocess](assets/sentimentprocess.png)

* **正面標語**

  以逗號分隔的單詞清單，可形成正面情緒，並覆寫預設值。 預設為空白清單。

* **負面關注字詞**

  以逗號分隔的單詞清單，構成覆寫預設值的負面情緒。 預設為空白清單。

* **Watchwords節點的明確路徑**

  包含指定預設關注字的預設`positive`和`negative`屬性的節點的存放庫位置。 預設值為`/libs/settings/community/watchwords/default`。

* **情緒規則**

  根據正面和負面關注字詞計算情緒的規則的存放庫位置。 預設值為`/libs/cq/workflow/components/workflow/social/sentiments/rules` （不過，不再涉及任何工作流程）。

下列是預設關注字詞的自訂專案範例，當`Explicit Path to Watchwords Node`設定為`/libs/settings/community/watchwords/default`時。

![crxde](assets/crxde.png)

### 版主許可權 {#moderator-permissions}

下列許可權在指派給相同資源時，統稱為`moderator permissions`：

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
