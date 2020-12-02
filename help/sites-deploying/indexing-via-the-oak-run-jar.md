---
title: 透過Oak-run Jar建立索引
seo-title: 透過Oak-run Jar建立索引
description: 瞭解如何透過Oak-run Jar執行索引。
seo-description: 瞭解如何透過Oak-run Jar執行索引。
uuid: 09a83ab9-92ec-4b55-8d24-2302f28fc2e4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c8a505ab-a075-47da-8007-43645a8c3ce5
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---


# 透過Oak-run Jar {#indexing-via-the-oak-run-jar}建立索引

Oak-run支援命令列上的所有索引使用案例，而不需從JMX層級操作。 Oak-run方法的優點有：

1. 它是AEM 6.4的全新索引工具集
1. 它縮短了重新索引時間，這有利地影響大型儲存庫的重新索引時間
1. 它可降低AEM中重新索引期間的資源消耗，為其他AEM活動提供更佳的系統效能
1. Oak-run提供帶外支援：如果生產條件不允許對生產實例運行重新索引，則可以使用克隆的環境進行重新索引，以避免對效能產生嚴重影響。

在下面，您將找到一個清單，列出在通過`oak-run`工具執行索引操作時可利用的使用案例。

## 索引一致性檢查{#indexconsistencychecks}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見[使用案例1 —— 索引一致性檢查](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck)。

* `oak-run.jar`快速判斷lucene oak索引是否損毀。
* 在使用中的AEM例項上執行一致性檢查層級1和2是安全的。

![screen_shot_2017-12-14at135758](assets/screen_shot_2017-12-14at135758.png)

## 索引統計資訊{#indexstatistics}

>[!NOTE]
>
>有關此方案的詳細資訊，請參閱[使用案例2 —— 索引統計資訊](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` 轉儲所有索引定義、重要索引統計資訊和索引內容，以便離線分析。
* 可在使用中的AEM例項上執行。

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## 重新索引方法決策樹{#reindexingapproachdecisiontree}

此圖是一種決策樹，用於確定何時使用各種重新索引方法。

![oak_-_riendingwithoak run](assets/oak_-_reindexingwithoak-run.png)

## 重新索引MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>有關此方案的詳細資訊，請參閱[使用案例3 —— 重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)。

### SegmentNodeStore和DocumentNodeStore {#textpre-extraction}的文字預擷取

[文字預擷取](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) （AEM 6.3中已有的功能）可用來縮短重新索引的時間。文本預抽取可與所有重新索引方法結合使用。

根據`oak-run.jar`索引方法，下圖中「執行重新索引」步驟的兩側將有各種步驟。

![4](assets/4.png)

>[!NOTE]
>
>橘色表示AEM必須位於維護視窗中的活動。

### 使用oak-run.jar {#onlinere-indexingformongomk}為MongoMK或RDBMK聯機重新索引

>[!NOTE]
>
>有關此方案的詳細資訊，請參見[ Reindex - DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore)。

這是重新索引MongoMK（和RDBMK）AEM安裝的建議方法。 不應使用其他方法。

此程式只需對叢集中的單一AEM例項執行。

![5](assets/5.png)

## 重新索引TarMK {#re-indexingtarmk}

>[!NOTE]
>
>有關此方案的詳細資訊，請參見[ Reindex - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore)。

* **冷備用注意事項(TarMK)**

   * 冷備無特殊考慮；冷備用實例將照常同步更改。

* **AEM Publish Farms（AE Publish Farms應永遠為TarMK）**

   * 對於發佈群組，它必須針對所有OR執行單一發佈的步驟，然後仿製其他人的設定(在複製AEM例項時採取所有常規的動作；sling.id —— 應連結至此處的項目)

### TarMK {#onlinere-indexingfortarmk}的聯機重新索引

>[!NOTE]
>
>有關此方案的詳細資訊，請參閱[Online Reindex - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore)。

這是在引入oak-run.jar新索引功能之前所使用的方法。 It can by setting the `reindex=true` property on the Oak index.

如果客戶可以接受索引的時間和效能影響，則可使用此方法。 中小型AEM安裝通常是如此。

![6](assets/6.png)

### 使用oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}線上重新索引TarMK

>[!NOTE]
>
>如需此藍本的詳細資訊，請參閱[線上重新索引- SegmentNodeStore - AEM例項正在執行](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning)。

TarMK的線上重新索引比上述線上TarkMK重新索引更快。 但是，它也需要在維護窗口期間執行，方法是窗口將更短，並且需要執行更多步驟來重新編製索引。

>[!NOTE]
>
>橘色表示必須在維護期間執行AEM的作業。

![7](assets/7.png)

### 使用oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}離線重新索引TarMK

>[!NOTE]
>
>如需此案例的詳細資訊，請參閱[線上重新索引- SegmentNodeStore - AEM例項為關閉](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown)。

離線重新索引TarMK是TarMK最簡單的`oak-run.jar`重新索引方法，因為它需要單一`oak-run.jar`注釋。 不過，它需要關閉AEM例項。

>[!NOTE]
>
>紅色表示必須關閉AEM的作業。

![8](assets/8.png)

### 使用oak-run.jar {#out-of-bandre-indexingtarmkusingoak-run-jar}的帶外重新索引TarMK

>[!NOTE]
>
>有關此方案的詳細資訊，請參見[帶外重新索引- SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore)。

帶外重新索引功能可將重新索引功能對使用中AEM例項的影響降至最低。

>[!NOTE]
>
>紅色表示AEM可能關閉的作業。

![9](assets/9.png)

## 更新索引定義{#updatingindexingdefinitions}

>[!NOTE]
>
>有關此方案的詳細資訊，請參閱[使用案例4 —— 更新索引定義](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions)。

### 使用ACS在TarMK上建立和更新索引定義Ensure Index {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Ensure Index是社群支援的專案，Adobe支援不支援。

這允許透過內容封裝來傳送索引定義，而後者會透過將重新索引標幟設定為`true`來重新索引。 這適用於重新建立索引不需要很長時間的較小設定。

有關詳細資訊，請參見[ACS Ensure Index文檔](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)。

### 使用oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}在TarMK上建立和更新索引定義

如果使用非`oak-run.jar`方法重新索引的時間或效能影響太大，則可使用下列以`oak-run.jar`為基礎的方法，在以TarMK為基礎的AEM安裝中匯入和重新索引Lucene索引定義。

![10](assets/10.png)

### 使用oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}在MonogMK上建立和更新索引定義

如果使用非`oak-run.jar`方法重新索引的時間或效能影響太大，則可使用下列`oak-run.jar`方法來匯入和重新索引以MongoMK為基礎的AEM安裝中的Lucene索引定義。

![11](assets/11.png)

