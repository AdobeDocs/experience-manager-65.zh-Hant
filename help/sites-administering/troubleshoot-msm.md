---
title: 疑難排解MSM問題和常見問題
description: 瞭解如何疑難排解最常見的MSM相關問題，並獲得最常見的MSM相關問題解答。
feature: Multi Site Manager
role: Admin
exl-id: 23f3391b-5ce3-48e1-ab27-a37737778089
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# 疑難排解MSM問題和常見問題 {#troubleshooting-msm}

## 疑難排解首要步驟 {#first-steps}

如果您在MSM中遇到您認為不正確的行為或錯誤，在開始和詳細的疑難排解之前，請確定：

* 檢查 [MSM常見問題集](#faq) 因為您的問題或疑問可能已經在該處解決。
* 檢查 [MSM最佳實務文章](msm-best-practices.md) 因為其中提供許多秘訣，並澄清一些誤解。

## 尋找有關您的Blueprint和即時副本狀態的進階資訊 {#advanced-info}

MSM會在資源URL上向選取器註冊數個可請求的servlet。 這些供UI使用，也可以直接請求以直接檢視頁面的其他進階計算MSM狀態：

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 在Blueprint頁面上使用這個專案來擷取連結到它的所有即時副本清單，連同其他即時副本狀態資訊。
   * 例如：
     `http://localhost:4502/content/wknd/language-masters/en.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`


1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * 在即時副本頁面上使用它可擷取關於其與其Blueprint頁面之連線的進階資訊。 如果頁面不是即時副本，則不會傳回任何內容。
   * 例如：
     `http://localhost:4502/content/wknd/ca/en.msm.json`

這些servlet會透過產生DEBUG記錄訊息 `com.day.cq.wcm.msm` 記錄器，也會有所幫助。

## 檢查存放庫中的MSM特定資訊 {#checking-repo}

先前的servlet會根據MSM特定的節點和mixin傳回計算資訊。 資訊會以下列方式儲存在存放庫中。

* `cq:LiveSync` mixin型別
   * 此設定於 `jcr:content` 節點和定義根Live Copy頁面。
   * 這些頁面將具有 `cq:LiveSyncConfig` 型別的子節點 `cq:LiveCopy` 透過下列屬性，將包含即時副本的基本和強制性資訊：
      * `cq:master` 指向即時副本的Blueprint頁面。
      * `cq:rolloutConfigs` 表示套用至即時副本的使用中轉出設定。
      * `cq:isDeep` 如果此根即時副本頁面的子頁面包含在即時副本中，則為true。
* `cq:LiveRelationship` mixin型別
   * 任何即時副本頁面上都有此類mixin型別 `jcr:content` 節點。
   * 如果沒有，頁面在某個時間點已分離或透過即時副本動作（建立或轉出）之外的編寫介面手動建立。
* `cq:LiveSyncCancelled` mixin型別
   * 新增至 `jcr:content` 已暫停之即時副本頁面的節點。
   * 如果暫停對子頁面也有效，則 `cq:isCancelledForChildren` 屬性會設定為相同節點上的true。

這些屬性中顯示的資訊應反映在UI中，不過進行疑難排解時，在MSM動作發生時直接在存放庫中觀察MSM行為可能會有所幫助。

瞭解這些屬性對於查詢您的存放庫並找出處於特定狀態的頁面集也很有用。 例如：

* `select * from cq:LiveSync` 傳回所有即時副本根頁面。

## 常見問題集 {#faq}

以下是與MSM和即時副本相關的一些常見問題。

### 為什麼有些屬性（例如標題、註解）在MSM轉出期間未更新？ {#missing-properties}

MSM同步動作是高度可設定的。 轉出時修改的屬性或元件會直接取決於這些設定的屬性。

請參閱 [本文](msm-best-practices.md) 以取得有關本主題的詳細資訊。

### 如何移除一組作者的轉出許可權？ {#remove-rollout-permissions}

沒有 **轉出** 可為AEM主體（使用者或群組）設定或移除的許可權。

或者，您可以：

* 自訂產品UI以隱藏給定主體的轉出動作。
* 從即時副本樹狀結構中移除不允許轉出之作者的寫入許可權。

### 為什麼我會看到尾碼為「_msm_moved」的即時副本頁面？ {#moved-pages}

如果轉出Blueprint頁面，它將更新其即時副本頁面或建立新的即時副本頁面（如果它不存在）（例如，首次轉出或手動刪除即時副本頁面時）。

但在後一種情況下，如果頁面沒有 `cq:LiveRelationship` 屬性以相同名稱存在，建立即時副本頁面之前，此頁面會相應重新命名。

依預設，轉出需要一個連結的即時副本頁面（藍圖的更新將轉出到該頁面），或是沒有頁面（在建立即時副本頁面時）。

如果找到「獨立」頁面，MSM會選擇重新命名此頁面，並建立個別的連結即時副本頁面。

即時副本子樹狀結構中的這類獨立頁面通常是以下專案的結果： **分離** 作業，或前一個即時副本頁面已由作者手動刪除，然後以相同名稱重新建立。

為避免此情況，請使用即時副本 **暫停** 功能而非 **分離**. 更多詳細資訊，請參閱 **分離** 中的動作 [本文章。](msm-livecopy.md)
