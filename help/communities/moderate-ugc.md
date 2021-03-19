---
title: 協調社群內容
seo-title: 協調社群內容
description: 協調概念和動作
seo-description: 協調概念和動作
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 1%

---


# 協調社群內容{#moderating-community-content}

## 概覽 {#overview}

當會員（登入網站訪客）透過與下列其中一個社群元件互動，從已發佈的社群網站張貼內容時，就會建立社群內容，也稱為使用者產生的內容(UGC):

* [部落格](/help/communities/blog-feature.md):會員張貼部落格文章或留言。
* [日曆](/help/communities/calendar.md):成員會張貼日曆事件或留言。
* [注釋](/help/communities/comments.md):成員會張貼留言或回覆留言。

* [論壇](/help/communities/forum.md):成員會發佈新主題或回覆主題。
* [概念](/help/communities/ideation-feature.md):會員張貼構想或留言。
* [QnA](/help/communities/working-with-qna.md):成員會建立問題或回答問題。
* [評論](/help/communities/reviews.md):成員在評分項目時張貼評論。

UGC的協調有助於識別正面貢獻以及限制負面貢獻（例如垃圾訊息和辱罵性語言）。 UGC可從以下幾種環境協調：

* [社群內容儲存](working-with-srp.md)

* [大量協調主控台](moderation.md)

   管理員和[社群協調者](/help/communities/users.md)可在公共環境中以及作者環境中的管理員存取協調控制台。 當社群內容儲存在[公用商店](/help/communities/working-with-srp.md)時，就可能發生此情況。

* [內容協調](in-context.md)

   發佈環境中的協調可由管理員和社群協調者直接在發佈內容的頁面上執行。

## 協調動作{#moderation-actions}

可對發佈內容(UGC)執行的動作會視使用者身分和環境而有所不同。 下表使用下列術語，根據用戶身份描述各種角色：

* `Admin`

   [community-administrators](users.md)群組成員的使用者。

* `Moderator`

   [社群協調者](users.md#publishenvironmentusersandgroups)群組的成員（具有[協調者權限](in-context.md#moderatorpermissions)）。

* `Creator`

   張貼內容的使用者。

* `Member`

   不具特殊權限的登入使用者。

* `Visitor`

   匿名使用者。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>管理員</strong></td>
   <td><strong>版主</strong></td>
   <td><strong>產生器</strong></td>
   <td><strong>成員</strong></td>
   <td><strong>訪客</strong></td>
   <td><strong>Event<br />觸發</strong></td>
   <td><strong>預先協調</strong></td>
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

### 編輯／刪除{#edit-delete}

貼文製作完成後，創作者、管理員或社群協調者可以編輯或刪除貼文。

刪除UGC時，它將從儲存庫中刪除，並且可能無法恢復。

### 剪下 {#cut}

管理員或社區協調者可以將一個或多個論壇主題或QnA問題從一個位置移動到另一個位置。 這包括從一個社群網站到另一個社群網站，前提是相同成員在這兩個網站上都擁有協調權限。

選取「剪下」(Cut)動作，內容就會複製到剪貼簿。 多則貼文可以複製，並以群組的形式移至新位置。

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

在另一個位置，當剪貼簿中有內容時，「新貼文」旁會顯示「貼上」按鈕，其編號會識別將貼上的貼文數。 「貼上」按鈕包含清除剪貼簿而非貼上的選項。

![作業範圍](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### 拒絕 {#deny}

協調者可能不允許UGC在發佈的網站上保持可見。 對於管理員和社群協調者，貼文仍可使用，並加上垃圾訊息。

### 關閉／重新開啟{#close-reopen}

「關閉」動作會在整個對話串流（論壇主題或初始留言）上運作，並包含所有後續的貼文或回覆。

關閉時，不僅無法再回覆，也不允許任何協調動作。

要執行任何操作，主題或注釋必須重新開啟。

管理員或社群協調者可以執行「關閉／重新開啟」動作。

### 標籤／取消標籤{#flag-unflag}

標幟是任何登入會員（內容建立者除外）的一種方式，用以指出貼文內容有問題。 標幟後，會出現取消標幟圖示，允許相同成員取消標幟內容。

可設定內容內容協調，讓成員在標籤貼文時選擇原因。 可配置可選標籤原因清單，包括是否可以輸入自定義原因。 標幟原因會與UGC一起儲存，但原因不會觸發任何特定動作。 只有旗標數會觸發通知。 標幟內容會加上註解，如此協調者就可據此行事。

系統會追蹤所有標幟、標幟者和標幟原因，並在達到臨界值時傳送事件。 如果社群協調者允許UGC，則會封存這些標幟。 在允許和封存後，如果有後續的標籤，則會封存這些標籤，就像之前沒有標籤一樣。

### 允許 {#allow}

「允許」動作是UGC的選項，其已標幟、拒絕或未在預先協調的系統中核准。 「允許」動作會清除任何已標幟或拒絕／垃圾訊息狀態，並封存任何已標幟的資料。

## 常見協調概念{#common-moderation-concepts}

### 預先協調{#premoderation}

當UGC預先協調時，貼文在協調動作核准後，才會顯示在發佈的網站上。 在建立[社群網站](/help/communities/sites-console.md)期間，勾選「內容為預先協調」方塊將啟用整個網站的預先協調。 [](sites-console.md#moderation)將元件放在頁面上後，就可設定支援協調的元件，以使用其編輯對話方塊中的設定進行預先協調：

* [在「使](comments.md) 用者 [](reviews.md)
協調 **[!UICONTROL >預先協]** 調」中建 **[!UICONTROL 議和檢閱]**。

* [論壇](/help/communities/forum.md) [理念](/help/communities/ideation-feature.md)、 [QnA](/help/communities/working-with-qna.md)和Settings  [](/help/communities/calendar.md)
 **[!UICONTROL >主持的]**  ****&#x200B;日曆。

### 垃圾郵件檢測{#spam-detection}

垃圾訊息偵測是一種自動協調功能，可將提交的使用者產生的內容標示為垃圾訊息，以篩選不可取的部分。 啟用後，它會根據預先設定的垃圾訊息字詞集合，識別使用者產生的內容是否為垃圾訊息。 預設垃圾訊息字詞提供於

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`。

不過，若要自訂或擴充預設垃圾訊息字詞，請透過[overlay](/help/communities/overlay-comments.md)，在/apps目錄中依預設垃圾訊息字詞結構建立一組字詞。

使用者產生的包含垃圾訊息的貼文（跨所有內容類型，例如部落格、論壇和留言）在貼文上方標有「此貼文已分類為垃圾訊息」文字。

協調者可以看到此類貼文，並加上相同的標籤，以允許或拒絕在網站上顯示。 這些貼文的協調動作可以在內容內或透過大量協調UI來執行。

![垃圾郵件檢測](assets/spamdetection.png)

若要啟用垃圾訊息偵測引擎，請依照下列步驟進行：

1. 轉至`/system/console/configMgr`以開啟[Web主控台](https://localhost:4502/system/console/configMgr)。

1. 找到&#x200B;**AEM Communities自動協調**&#x200B;配置並加以編輯。
1. 添加&#x200B;**[!UICONTROL SpamProcess]**&#x200B;條目。

![垃圾郵件處理](assets/spamprocess.png)

>[!NOTE]
>
>垃圾訊息偵測只會針對英文地區設定實作。

### 情緒 {#sentiment}

情緒是根據貼文(UGC)中顯示的正面和負面關鍵字([watchwords](#configuringwatchwords))數目計算。

情緒分析使用一組預先設定的規則，並計算UGC的情緒。 預設規則位於：`/libs/cq/workflow/components/workflow/social/sentiments/rules.`

規則產生的值從1（所有負面，無正面字詞）到10（所有正面，無負面字詞）。 情緒值5為中性情緒，且為預設值。

/libs元件中定義的規則包括：

* 規則1:如果沒有正面字詞且至少有一個負面字詞，請將值設為1。
* 規則2:如果沒有否定字詞且至少有一個正面字詞，請將值設為10。
* 規則3:如果有比正面字詞更多的負面字詞，請將值設為3。
* 規則4:如果正面字詞多於負面字詞，請將值設為8。

若要覆寫或新增規則，請依照預設規則的結構，在/apps目錄中建立一組規則。 編輯情緒設定，以識別規則的位置。

分析後，情緒會與UGC一起儲存。

從[大量協調控制台](/help/communities/moderation.md)，可以根據情緒是負面、中性或正面來篩選和檢視UGC。

#### 關注字詞{#watchwords}

AEM社群提供&#x200B;*watchword分析器*&#x200B;作為評估[情緒](#sentiment)的程式步驟。 關注字詞對情緒值的貢獻是因為比較已張貼內容中使用的負面和正面關注字詞，以及禁止字詞。

#### 設定情緒和關注字詞{#configure-sentiment-and-watchwords}

可自訂正面和負面監看字詞清單，因為可以是情緒規則。

預設的監視字詞清單可以作為節點的屬性在儲存庫中輸入，類似於預設值，或者通過使用字詞清單配置OSGi服務`sentimentprocess.name`來覆蓋預設值。

**sentimentprocess.name**&#x200B;也可以修改，以參考自訂情緒規則集的位置。

若要設定情緒和關注字詞：

* 以管理員身分登入您的作者例項。
* 開啟[Web控制台](https://localhost:4502/system/console/configMgr)。
* 找到`sentimentprocess.name`。
* 選擇要在編輯模式下開啟的配置。

![感情過程](assets/sentimentprocess.png)

* **正面的關注字詞**

   以逗號分隔的字詞清單，可導致覆寫預設值的正面情緒。 預設為空白清單。

* **負面關注字詞**

   以逗號分隔的字詞清單，會造成覆寫預設值的負面情緒。 預設為空白清單。

* **監視字詞節點的顯式路徑**

   包含預設`positive`和`negative`屬性的節點的儲存庫位置，這些屬性指定預設的監視字。 預設值為`/libs/settings/community/watchwords/default`。

* **情緒規則**

   根據正面和負面關注字詞計算情緒的規則存放庫位置。 預設值為`/libs/cq/workflow/components/workflow/social/sentiments/rules`（不過，不再涉及任何工作流程）。

以下是當`Explicit Path to Watchwords Node`設為`/libs/settings/community/watchwords/default`時，預設監看字詞的自訂項目範例。

![crxde](assets/crxde.png)

### 協調者權限{#moderator-permissions}

以下權限在指派給相同資源時統稱為`moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`

