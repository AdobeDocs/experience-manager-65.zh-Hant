---
title: AEM Foundation & Repository
description: Adobe Experience Manager 6.3 AEM Platform和Repository的發行說明。
uuid: 70626eda-c514-44bd-9f28-ff7abdc22f53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 66ecf4c5-6d0f-4586-880d-7d1c8a5a5614
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# AEM Foundation &amp; Repository{#aem-foundation-repository}

## 變更清單 {#list-of-changes}

### 存放庫 {#repository}

* Adobe Experience Manager 6.5的基礎建立在OSGi架構（Apache Sling和Apache Felix）和Java內容存放庫的更新版本之上：Apache Jackrabbit Oak 1.10.2.
* 如需修 [正問題的完整概觀，請參閱Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)、 [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 和 [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) 。

>[!CAUTION]
>
>* 自AEM 6.3以來，Oak Segment Tar的新版本需要儲存庫移轉。 如果您要從舊版TarMK升級，或想要從其他永續性類型切換新的區段Tar，此步驟為必要步驟。 如需新區段Tar的優點的詳細資訊，請參閱移轉至 [Oak區段Tar常見問答](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar)。
>



### Java支援 {#java-support}

* Java 11的新支援，以及已支援的Java 8
* 為獲得最佳效能，請用其他值覆蓋預設GC值。 如需詳細資訊，請參閱「安 [裝與更新](/help/sites-deploying/custom-standalone-install.md) 」一節。
* Java 11和Java 8維護更新將由Adobe分發，以便客戶在AEM相關專案中使用，但Oracle未公開提供

### OSGI {#osgi}

* 已新增OSGi承諾和轉換器公用程式庫

### 專案和工作流程 {#projects-and-workflows}

* 6.4版中引進的全新工作流程模型編輯器已經過改良，加入更多作業，例如複製和發佈、工作流程步驟中的變數支援，以及增強的OR和AND分割。

### 搜尋 {#searching}

* 在Oak中搜尋現在支援動態Facet。 例如，資產搜尋中的篩選邊欄會顯示估計的結果量。
* QueryBuilder已擴充，可提供動態刻面結果

### 安全性 {#security}

* 已新增管理員使用者的密碼到期。

### 使用者介面{#user-interface}

UI已做了各種增強功能，讓它更有生產力，也更容易使用。

* AEM 6.5推出新的「使用者和群組的權限管理UI」，讓您更輕鬆地檢視和設定整個權限和限制集，而不需前往CRXDE。
* 欄檢視現在也只會載入螢幕上可見的項目，而且只會在使用者開始捲動時載入更多項目。 清單和卡片檢視自6.0起就已執行此動作（在6.4中改良）
* 欄檢視現在包含頁面／資產的工作流程狀態（如果適用）
* 「全選」動作是快速執行動作的方式，可將所有頁面／資產置於同一資料夾中
* 「全選」動作會嘗試對所有頁面／資產執行動作，而不只是載入的內容。 如果動作尚未升級以處理大量動作，則會顯示警告對話方塊

>[!CAUTION]
>
>* Adobe不打算對Classic UI做進一步的增強。 AEM 6.5包含Classic UI，而從舊版升級的客戶可依現狀繼續使用。 請注意，Classic UI在遭淘汰時仍完全受支援，請 [閱讀詳細內容](/help/sites-deploying/ui-recommendations.md)。
>



### 升級 {#upgrade}

* 升級程式在6.5中基本保持不變。
* 我們繼續支援6.4版中推出的回溯相容性、升級複雜性評估和持續升級功能。在需要時，已對這些區域進行了特定版本的更新。
* Pattern Detector封裝已經簡化，而且將有一個封裝評估可用來源版本的6.5升級。
* 如需升級程式 [的詳細資訊](/help/sites-deploying/upgrade.md) ，請參閱升級檔案。

### Web伺服器 {#web-server}

* Quickstart散發使用Eclipse Jetty 9.4.15做為servlet引擎（AEM 6.4隨附9.3.22）

