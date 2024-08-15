---
title: 疑難排解MSM問題和常見問題
description: 瞭解如何疑難排解最常見的MSM相關問題，並取得最常見的MSM相關問題解答。
feature: Multi Site Manager
role: Admin
exl-id: 23f3391b-5ce3-48e1-ab27-a37737778089
solution: Experience Manager, Experience Manager Sites
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---

# 疑難排解MSM問題和常見問題 {#troubleshooting-msm}

## 疑難排解首要步驟 {#first-steps}

如果您在MSM中遇到您認為不正確的行為或錯誤，在開始和詳細的疑難排解之前，請務必：

* 請檢視[MSM常見問題集](#faq)，因為您的問題或疑問可能已在該處解決。
* 請檢視[MSM最佳實務文章](msm-best-practices.md)，因為其中提供了一些秘訣，以及一些錯誤概念的澄清。

## 尋找有關您的Blueprint和即時副本狀態的進階資訊 {#advanced-info}

MSM會在資源URL上向選取器註冊數個可請求的servlet。 這些可供UI使用，也可以直接請求以直接檢視頁面的其他進階計算MSM狀態：

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 在Blueprint頁面上使用這個專案來擷取連結到它的所有即時副本清單，連同其他即時副本狀態資訊。
   * 例如：
     `http://localhost:4502/content/wknd/language-masters/en.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`


1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * 在即時副本頁面上使用它可擷取有關其與Blueprint頁面連線的進階資訊。 如果頁面不是即時副本，則不會傳回任何專案。
   * 例如：
     `http://localhost:4502/content/wknd/ca/en.msm.json`

這些servlet會透過`com.day.cq.wcm.msm`記錄器產生DEBUG記錄訊息，這些訊息也可能會有所幫助。

## 檢查存放庫中的MSM特定資訊 {#checking-repo}

先前的servlet會根據MSM特定節點和mixin傳回計算資訊。 資訊會以下列方式儲存在存放庫中。

* `cq:LiveSync` mixin型別
   * 這是在`jcr:content`節點上設定，並定義根即時副本頁面。
   * 這些頁面具有型別為`cq:LiveCopy`的`cq:LiveSyncConfig`子節點，其中包含透過下列屬性在即時副本上的基本和必要資訊：
      * `cq:master`指向即時副本的Blueprint頁面。
      * `cq:rolloutConfigs`表示套用至即時副本的有效轉出設定。
      * 如果此根即時副本頁面的子頁面包含在即時副本中，`cq:isDeep`為true。
* `cq:LiveRelationship` mixin型別
   * 任何即時副本頁面的`jcr:content`節點都有此類mixin型別。
   * 如果沒有，頁面在某個時間點已被分離或透過即時副本動作（建立或轉出）之外的編寫介面手動建立。
* `cq:LiveSyncCancelled` mixin型別
   * 已新增至已暫停之即時副本頁面的`jcr:content`個節點。
   * 如果暫停對子頁面也有效，則相同節點上的`cq:isCancelledForChildren`屬性會設為true。

這些屬性中存在的資訊應反映在UI中，但是在進行疑難排解時，當MSM動作發生時直接在存放庫中觀察MSM行為可能會有所幫助。

瞭解這些屬性也有助於查詢您的存放庫並找出處於特定狀態的頁面集。 例如：

* `select * from cq:LiveSync`會傳回所有即時副本根頁面。

## 常見問題集 {#faq}

以下是與MSM和即時副本相關的一些常見問題。

### 為什麼有些屬性（例如標題、註解）在MSM轉出期間沒有更新？ {#missing-properties}

MSM同步動作是高度可設定的。 轉出期間會修改哪些屬性或元件，直接取決於這些設定的屬性。

請參閱[MSM最佳實務](msm-best-practices.md)以取得此主題的詳細資訊。

### 如何移除一組作者的轉出許可權？ {#remove-rollout-permissions}

沒有可以為AEM主體（使用者或群組）設定或移除的&#x200B;**轉出**&#x200B;許可權。

或者，您可以：

* 自訂產品UI以隱藏指定主體的轉出動作。
* 針對不允許轉出的作者，從即時副本樹狀結構中移除寫入許可權。

### 為什麼我會看到尾碼為「_msm_moved」的即時副本頁面？ {#moved-pages}

如果轉出Blueprint頁面，它會更新其即時副本頁面或建立新的即時副本頁面（如果尚未存在）。 例如，首次轉出或手動刪除即時副本頁面時。

但在後一種情況下，如果存在不含`cq:LiveRelationship`屬性的同名頁面，則會在建立即時副本頁面之前重新命名此頁面。

依預設，轉出需要一個連結的即時副本頁面，藍圖的更新會轉出到該頁面。 或者，建立即時副本頁面時，完全沒有頁面。

如果找到「獨立」頁面，MSM會選擇重新命名此頁面，並建立個別的連結即時副本頁面。

即時副本子樹狀結構中的這類獨立頁面通常是&#x200B;**分離**&#x200B;作業的結果，或之前的即時副本頁面已由作者手動刪除，然後以相同名稱重新建立。

若要避免此問題，請使用即時副本&#x200B;**暫停**&#x200B;功能，而非&#x200B;**分離**。 有關&#x200B;**分離**&#x200B;動作的詳細資訊，請參閱[本文章。](msm-livecopy.md)
