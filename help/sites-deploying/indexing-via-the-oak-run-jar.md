---
title: 通過Oak-run Jar索引
seo-title: Indexing via the Oak-run Jar
description: 瞭解如何通過Oak-run Jar執行索引。
seo-description: Learn how to perform indexing via the Oak-run Jar.
uuid: 09a83ab9-92ec-4b55-8d24-2302f28fc2e4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c8a505ab-a075-47da-8007-43645a8c3ce5
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
source-git-commit: c61bf629e35db848c3f2f88c6c7e1dd3b7074b1c
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# 通過Oak-run Jar索引 {#indexing-via-the-oak-run-jar}

Oak-run支援命令行上的所有索引使用案例，而無需從JMX級別操作。 Oak-run方法的優點是：

1. 它是用於6.4的AEM新索引工具集
1. 它減少了重新編製索引的時間，這有利地影響了對大型儲存庫重新編製索引的時間
1. 它減少了重新索引期間的資源消耗，AEM從而為其他活動帶來更好的系統AEM效能
1. Oak-run提供帶外支援：如果生產條件不允許對生產實例運行重新索引，則可以使用克隆的環境進行重新索引，以避免對效能產生關鍵影響。

在下面，您將找到在通過 `oak-run` 工具欄。

## 索引一致性檢查 {#indexconsistencychecks}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [用例1 — 索引一致性檢查](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck)。

* `oak-run.jar`快速確定Lucene橡樹索引是否已損壞。
* 在使用中實例上運行一致性檢查AEM級別1和2是安全的。

![索引一致性檢查](assets/screen_shot_2017-12-14at135758.png)

## 索引統計資訊 {#indexstatistics}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [用例2 — 索引統計](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` 轉儲離線分析的所有索引定義、重要索引統計資訊和索引內容。
* 在使用中實例上執行AEM安全。

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## 重標引方法決策樹 {#reindexingapproachdecisiontree}

此圖是一個決策樹，用於確定何時使用各種重新索引方法。

![橡樹_ — 駝鹿興和橡樹跑](assets/oak_-_reindexingwithoak-run.png)

## 重新索引MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [用例3 — 重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)。

### SegmentNodeStore和DocumentNodeStore的文本預提取 {#textpre-extraction}

[文本預提取](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (6.3中存在的AEM功能)可用於減少重新索引的時間。 文本預提取可以與所有重新索引方法結合使用。

取決於 `oak-run.jar` 索引方法在下圖的「執行重新索引」步驟的兩側都有各種步驟。

![SegmentNodeStore和DocumentNodeStore的文本預提取](assets/4.png)

>[!NOTE]
>
>橙色表示必須AEM位於維護窗口中的活動。

### 使用oak-run.jar為MongoMK或RDBMK線上重新索引 {#onlinere-indexingformongomk}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [重新索引 — DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore)。

這是重新索引MongoMK（和RDBMK）安裝的推薦方AEM法。 不應使用其他方法。

只需對群集中的單個實例AEM執行此進程。

![使用oak-run.jar為MongoMK或RDBMK線上重新索引](assets/5.png)

## 重新索引TarMK {#re-indexingtarmk}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore)。

* **冷備用注意事項(TarMK)**

   * Cold Standby沒有特別考慮；冷備用實例將像往常一樣同步更改。

* **AEM發佈場（AE發佈場應始終為TarMK）**

   * 對於發佈場，需要為所有伺服器執行步驟，或者在單個發佈上執行步驟，然後為其他伺服器克隆安裝程式(在克隆實例時執行所有常AEM規步驟；sling.id — 應連結到此處的內容

### TarMK的線上索引 {#onlinere-indexingfortarmk}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [聯機重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore)。

這是在引入oak-run.jar的新索引功能之前使用的方法。 可以通過設定 `reindex=true` Oak指數上的房產。

如果索引的時間和效能影響為客戶可接受，則可使用此方法。 中小型安裝通常是這AEM種情況。

![TarMK的線上索引](assets/6.png)

### 使用oak-run.jar線上重新索引TarMK {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [聯機重新索引 — SegmentNodeStore — 實AEM例正在運行](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning)。

使用oak-run.jar對TarMK進行線上重新索引比 [TarMK的線上索引](#onlinere-indexingfortarmk) 如上所述。 但是，在維護窗口期間也需要執行；提到窗口將更短，需要執行更多步驟才能重新編製索引。

>[!NOTE]
>
>橙色表示必須AEM在維護期間執行的操作。

![使用oak-run.jar線上重新索引TarMK](assets/7.png)

### 使用oak-run.jar離線重新索引TarMK {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [聯機重新索引 — SegmentNodeStore — 實AEM例已關閉](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown)。

TarMK的離線重新索引是最簡單的 `oak-run.jar` 基於索引的TarMK方法，因為它需要 `oak-run.jar` 注釋。 但是，它要AEM求關閉實例。

>[!NOTE]
>
>紅色表示必須AEM關閉的操作。

![使用oak-run.jar離線重新索引TarMK](assets/8.png)

### 使用oak-run.jar的帶外重新索引TarMK  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [帶外重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore)。

帶外重新索引可最大限度地減少重新索引對使用中實例的影AEM響。

>[!NOTE]
>
>紅色表示可AEM能關閉的操作。

![使用oak-run.jar的帶外重新索引TarMK](assets/9.png)

## 更新索引定義 {#updatingindexingdefinitions}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見 [用例4 — 更新索引定義](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions)。

### 使用ACS確保索引在TarMK上建立和更新索引定義 {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Ensure Index是社區支援的項目，不受Adobe支援。

這允許通過內容包發送索引定義，這些內容包稍後會通過將重新索引標誌設定為 `true`。 這適用於重新編製索引不需要很長時間的較小設定。

有關詳細資訊，請參閱 [ACS確保索引文檔](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 的雙曲餘切值。

### 使用oak-run.jar在TarMK上建立和更新索引定義 {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

如果使用非索引重新索引的時間或效能影響 `oak-run.jar` 方法太高，如下所示 `oak-run.jar` 基於TarMK的安裝可用於導入和重新索引Lucene索引定AEM義。

![使用oak-run.jar在TarMK上建立和更新索引定義](assets/10.png)

### 使用oak-run.jar在MonogMK上建立和更新索引定義 {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

如果使用非索引重新索引的時間或效能影響 `oak-run.jar` 方法太高，如下所示 `oak-run.jar` 基於MongoMK的安裝可用於導入和重新索引Lucene索引定AEM義。

![使用oak-run.jar在MonogMK上建立和更新索引定義](assets/11.png)
