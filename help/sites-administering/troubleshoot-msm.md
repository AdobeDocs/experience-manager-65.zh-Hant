---
title: 疑難排解MSM問題和常見問題集
description: 了解如何疑難排解最常見的MSM相關問題，並取得最常見的MSM相關問題的解答。
feature: Multi Site Manager
role: Admin
exl-id: 23f3391b-5ce3-48e1-ab27-a37737778089
source-git-commit: 289c4644063504ec3c8e02d930933ad7260600f0
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# 疑難排解MSM問題和常見問題集 {#troubleshooting-msm}

## 疑難排解第一步 {#first-steps}

如果您遇到MSM中的錯誤或行為不正確，請務必在開始和詳細的疑難排解之前：

* 檢查 [MSM常見問題集](#faq) 因為你的問題或問題可能已經在那裡解決了。
* 檢查 [MSM最佳做法文章](msm-best-practices.md) 由於提供了一些建議，並澄清了一些誤解。

## 尋找關於您的Blueprint和Live Copy狀態的進階資訊 {#advanced-info}

MSM會註冊多個可向資源URL上的選取器要求的servlet。 UI會使用這些狀態，但也可以直接請求，以直接查看頁面的其他進階計算MSM狀態：

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 在Blueprint頁面上使用此功能，可擷取連結至該Live Copy的所有Live Copy清單，以及其他Live Copy狀態資訊。
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * 在Live Copy頁面上使用此功能，可擷取其與Blueprint頁面連線的進階資訊。 如果頁面不是即時副本，則不會傳回任何內容。

這些servlet會透過 `com.day.cq.wcm.msm` 記錄器也可能有用。

## 在存放庫中檢查MSM專屬資訊 {#checking-repo}

先前的servlet根據MSM特定節點和mixin返回計算資訊。 資訊將以下方式儲存在儲存庫中。

* `cq:LiveSync` 混合類型
   * 此設定於 `jcr:content` 節點，並定義根即時副本頁面。
   * 這些頁面會有 `cq:LiveSyncConfig` 類型的子節點 `cq:LiveCopy` 包含Live Copy的基本和必要資訊（透過下列屬性）:
      * `cq:master` 指向即時副本的Blueprint頁面。
      * `cq:rolloutConfigs` 指出套用至即時副本的作用中轉出設定。
      * `cq:isDeep` 如果此根即時副本頁面的子頁面包含在即時副本中，則為true。
* `cq:LiveRelationship` 混合類型
   * 任何「即時副本」頁面的其中都有這種混合類型 `jcr:content` 節點。
   * 若未這麼做，則某個時間點的頁面會透過Live Copy動作（建立或轉出）以外的製作介面被分離或手動建立。
* `cq:LiveSyncCancelled` 混合類型
   * 新增至 `jcr:content` 暫停的Live Copy頁面節點。
   * 如果暫停對子頁面也有效，則 `cq:isCancelledForChildren` 在相同節點上，屬性設為true。

這些屬性中顯示的資訊應反映在UI中，但在進行疑難排解時，在發生MSM動作時，直接在存放庫中觀察MSM行為可能會很有幫助。

了解這些屬性對於查詢您的儲存庫並找出特定狀態的頁面集也很有用。 例如：

* `select * from cq:LiveSync` 會傳回所有Live Copy根頁面。

## 常見問題集 {#faq}

以下是一些與MSM和Live Copy相關的常見問題。

### 為何MSM轉出期間沒有更新某些屬性（例如標題、註解）? {#missing-properties}

MSM同步動作可高度設定。 轉出期間修改的屬性或元件直接取決於這些設定的屬性。

請參閱 [這篇文章](msm-best-practices.md) 以取得此主題的詳細資訊。

### 如何移除一組作者的轉出權限？ {#remove-rollout-permissions}

沒有 **轉出** 可為AEM主體（用戶或組）設定或移除的權限。

或者，您可以：

* 自訂產品UI以隱藏指定承擔者的轉出動作。
* 從Live Copy樹中為不允許轉出的作者刪除寫權限。

### 為何會看到尾碼為「_msm_moved」的Live Copy頁面？ {#moved-pages}

如果Blueprint頁面已推出，它會更新其「即時副本」頁面，或在尚未存在時建立新的「即時副本」頁面（例如首次推出或手動刪除「即時副本」頁面）。

但在後一種情況下，如果頁面沒有 `cq:LiveRelationship` 屬性存在且名稱相同，因此在建立Live Copy頁面之前，此頁面會據此重新命名。

依預設，轉出會預期一個連結的即時副本頁面，藍圖的更新將轉出到該頁面，或是當建立即時副本頁面時沒有頁面。

如果找到「獨立」頁面，MSM會選擇重新命名此頁面，並建立個別的連結Live Copy頁面。

Live Copy子樹中的這種獨立頁面通常是 **分離** ，或由作者手動刪除舊版Live Copy頁面，然後以相同名稱重新建立。

為了避免此情況，請使用Live Copy **暫停** 功能而非 **分離**. 更多 **分離** 動作 [這篇文章。](msm-livecopy.md)
