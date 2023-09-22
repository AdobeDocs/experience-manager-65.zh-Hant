---
title: 透過Oak-run Jar編制索引
description: 瞭解如何透過Oak-run Jar執行索引。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# 透過Oak-run Jar編制索引 {#indexing-via-the-oak-run-jar}

Oak-run支援命令列上的所有索引使用案例，不必從JMX層級操作。 Oak-run方法的優點包括：

1. 這是適用於AEM 6.4的新的索引工具集
1. 這能縮短重新編列索引的時間，而有利於影響大型存放庫的重新編列索引時間
1. 這減少了在AEM中重新索引時的資源消耗，導致其他AEM活動獲得更好的系統效能
1. Oak-run提供頻外支援：如果生產條件不允許您在生產執行個體上執行重新索引，則可以使用複製的環境來重新索引，以避免對效能產生嚴重影響。

以下是透過以下方式執行索引作業時可使用的使用案例清單 `oak-run` 工具。

## 索引一致性檢查 {#indexconsistencychecks}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [使用案例1 — 索引一致性檢查](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar`快速判斷Lucene Oak索引是否損毀。
* 針對一致性檢查層級1和2而在使用中的AEM執行個體上執行是安全的。

![索引一致性檢查](assets/screen_shot_2017-12-14at135758.png)

## 索引統計資料 {#indexstatistics}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [使用案例2 — 索引統計資料](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` 會傾印所有索引定義、重要索引統計資料，以及離線分析的索引內容。
* 可在使用中的AEM例項上安全執行。

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## 重新索引方法決策樹 {#reindexingapproachdecisiontree}

此圖表是決定何時使用各種重新索引方法的決策樹。

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## 重新索引MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [使用案例3 — 重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### SegmentNodeStore和DocumentNodeStore的文字預先擷取 {#textpre-extraction}

[文字預先擷取](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (AEM 6.3已有的功能)可用來減少重新編列索引的時間。 文字預先擷取可用於所有重新索引方法。

依據 `oak-run.jar` 索引方法，在下圖中「執行重新索引」步驟的兩側都有各種步驟。

![SegmentNodeStore和DocumentNodeStore的文字預先擷取](assets/4.png)

>[!NOTE]
>
>橘色表示AEM必須在維護期間進行的活動。

### 使用oak-run.jar為MongoMK或RDBMK線上重新索引 {#onlinere-indexingformongomk}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [重新索引 — 檔案節點存放區](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

這是重新索引MongoMK （和RDBMK） AEM安裝的建議方法。 不應使用其他方法。

僅針對叢集中的單一AEM執行個體執行此程式。

![使用oak-run.jar為MongoMK或RDBMK線上重新索引](assets/5.png)

## 重新索引TarMK {#re-indexingtarmk}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **冷待命考量事項(TarMK)**

   * 冷待命沒有特殊考量；冷待命執行個體會照常同步變更。

* **AEM發佈陣列（AE發佈陣列應一律為TarMK）**

   * 對於發佈陣列，必須為全部完成或在單一發佈上執行步驟。 接著，複製其他人的設定(複製AEM執行個體時採用所有常用的預先處理方式；sling.id — 應該在這裡連結到某個專案)。

### TarMK的線上重新索引 {#onlinere-indexingfortarmk}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [線上重新索引 — 區段節點存放區](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

這是oak-run.jar引進新索引功能之前使用的方法。 這可透過設定 `reindex=true` 屬性。

如果客戶可接受索引的時間和效能影響，則可使用此方法。 中小型的AEM安裝通常就是這種情況。

![TarMK的線上重新索引](assets/6.png)

### 使用oak-run.jar線上重新索引TarMK {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [線上重新索引 — SegmentNodeStore - AEM執行個體正在執行](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

使用oak-run.jar線上重新索引TarMK比 [TarMK的線上重新索引](#onlinere-indexingfortarmk) 如上所述。 但是，它需要在維護時段內執行；其中提到時段較短，並且需要更多步驟來執行重新索引。

>[!NOTE]
>
>橘色表示在維護期間必須執行AEM的作業。

![使用oak-run.jar線上重新索引TarMK](assets/7.png)

### 使用oak-run.jar離線重新索引TarMK {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [線上重新索引 — SegmentNodeStore - AEM執行個體已關閉](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

離線重新索引TarMK是最簡單的方法 `oak-run.jar` 針對TarMK的重新索引方法，因為它需要單一 `oak-run.jar` 評論。 但是，它需要關閉AEM執行個體。

>[!NOTE]
>
>紅色表示必須關閉AEM的作業。

![使用oak-run.jar離線重新索引TarMK](assets/8.png)

### 使用oak-run.jar的頻外重新索引TarMK  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [頻外重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

頻外重新索引可將重新索引對使用中AEM執行個體造成的影響降至最低。

>[!NOTE]
>
>紅色表示可能關閉AEM的作業。

![使用oak-run.jar的頻外重新索引TarMK](assets/9.png)

## 更新索引定義 {#updatingindexingdefinitions}

>[!NOTE]
>
>如需此情境的詳細資訊，請參閱 [使用案例4 — 更新索引定義](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### 使用ACS在TarMK上建立和更新索引定義確保索引 {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS確認索引是社群支援的專案，不受Adobe支援的支援。

這允許透過內容包來傳送索引定義，這稍後會透過將重新索引標幟設定為來導致重新索引 `true`. 這適用於重新索引不需要很長的時間的較小設定。

如需詳細資訊，請參閱 [ACS確認索引檔案](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 以取得詳細資訊。

### 使用oak-run.jar在TarMK上建立和更新索引定義 {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

如果使用重新索引的時間或效能影響`oak-run.jar` 方法太高，請遵循下列步驟 `oak-run.jar` 在基於TarMK的AEM安裝中，基於的方法可用於匯入和重新索引Lucene索引定義。

![使用oak-run.jar在TarMK上建立和更新索引定義](assets/10.png)

### 使用oak-run.jar在MonogMK上建立和更新索引定義 {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

如果使用重新索引的時間或效能影響`oak-run.jar` 方法太高，請遵循下列步驟 `oak-run.jar` 在基於MongoMK的AEM安裝中，基於的方法可用於匯入和重新索引Lucene索引定義。

![使用oak-run.jar在MonogMK上建立和更新索引定義](assets/11.png)
