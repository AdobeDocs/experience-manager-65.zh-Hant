---
title: MSM問題故障排除和常見問題
description: 瞭解如何排除與MSM相關的最常見問題，並獲得與MSM相關的最常見問題的答案。
feature: Multi Site Manager
role: Admin
exl-id: 23f3391b-5ce3-48e1-ab27-a37737778089
source-git-commit: a323e6c30bf2c226f6613d1b9b037a0beedbfc0d
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---

# MSM問題故障排除和常見問題 {#troubleshooting-msm}

## 故障排除第一步 {#first-steps}

如果您遇到MSM中的錯誤行為或錯誤，請在開始和詳細故障排除之前確保：

* 檢查 [MSM常見問題](#faq) 因為你的問題或問題可能已經在那裡解決了。
* 檢查 [MSM最佳做法文章](msm-best-practices.md) 因為提供了一些提示，並澄清了一些誤解。

## 查找有關您的藍圖和即時拷貝狀態的高級資訊 {#advanced-info}

MSM在資源URL上註冊多個可以通過選擇器請求的Servlet。 這些功能由UI使用，但也可以直接請求查看頁面的其他高級計算MSM狀態：

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 在藍圖頁上使用此選項可檢索連結到它的所有即時副本的清單，以及其他即時副本狀態資訊。
   * 例如：
      `http://localhost:4502/content/wknd/language-masters/en.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`


1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * 在Live Copy頁面上使用此選項可檢索有關其與藍圖頁面連接的高級資訊。 如果頁面不是即時副本，則不返回任何內容。
   * 例如：
      `http://localhost:4502/content/wknd/ca/en.msm.json`

這些servlet通過 `com.day.cq.wcm.msm` 記錄器也會有所幫助。

## 在儲存庫中檢查特定於MSM的資訊 {#checking-repo}

先前的Servlet基於MSM特定節點和混合返回計算資訊。 資訊以下列方式儲存在儲存庫中。

* `cq:LiveSync` 混音類型
   * 已設定 `jcr:content` 並定義根Live Copy頁。
   * 那些頁面 `cq:LiveSyncConfig` 類型的子節點 `cq:LiveCopy` 包含有關Live Copy的基本和必需資訊，可通過以下屬性進行：
      * `cq:master` 指向「即時拷貝」的藍圖頁面。
      * `cq:rolloutConfigs` 指示應用於即時拷貝的活動部署配置。
      * `cq:isDeep` 如果此根Live Copy頁的子頁包含在Live Copy中，則為true。
* `cq:LiveRelationship` 混音類型
   * 任何Live Copy頁面的混合類型都在其上 `jcr:content` 的下界。
   * 如果不是，則某個時點的頁面已經分離或通過Live Copy操作（建立或展開）外的創作介面手動建立。
* `cq:LiveSyncCancelled` 混音類型
   * 添加到 `jcr:content` 已掛起的Live Copy頁面的節點。
   * 如果暫停對子頁也有效，則 `cq:isCancelledForChildren` 屬性在同一節點上設定為true。

這些屬性中的資訊應反映在UI中，但在進行故障排除時，在MSM操作發生時直接在儲存庫中觀察MSM行為可能會有所幫助。

瞭解這些屬性對於查詢儲存庫和查找處於特定狀態的頁面集也非常有用。 例如：

* `select * from cq:LiveSync` 返回所有Live Copy根頁。

## 常見問題集 {#faq}

以下是一些與MSM和Live Copy相關的常見問題。

### 為什麼在MSM部署期間不更新某些屬性（如標題、注釋）? {#missing-properties}

MSM同步操作是高度可配置的。 在展開期間修改哪些屬性或元件直接取決於這些配置的屬性。

請參閱 [這篇文章](msm-best-practices.md) 的子菜單。

### 如何刪除一組作者的轉出權限？ {#remove-rollout-permissions}

沒有 **推廣** 可以為承擔者（用戶或組）AEM設定或刪除的權限。

作為替代方法，您可以：

* 自定義產品UI以隱藏給定承擔者的「展示」操作。
* 從Live Copy樹中為不允許展開的作者刪除寫權限。

### 為什麼我看到帶有尾碼「_msm_moved」的Live Copy頁面？ {#moved-pages}

如果展開藍圖頁，則它將更新其「即時複製」頁或建立新的「即時複製」頁（如首次展開或手動刪除「即時複製」頁）。

但是，在後一種情況下，如果沒有 `cq:LiveRelationship` 屬性存在且名稱相同，在建立Live Copy頁之前，將相應地更名此頁。

預設情況下，部署需要一個連結的即時拷貝頁面，在該頁面上將展開藍圖的更新，或者在建立即時拷貝頁面時沒有頁面。

如果找到「獨立」頁，MSM將選擇更名此頁，並建立單獨的連結Live Copy頁。

Live Copy子樹中的此類獨立頁面通常是 **分離** 操作，或前一個Live Copy頁面已由作者手動刪除，然後以相同名稱重新建立。

為避免此情況，請使用即時拷貝 **掛起** 特徵 **分離**。 有關 **分離** 操作 [這篇文章。](msm-livecopy.md)
