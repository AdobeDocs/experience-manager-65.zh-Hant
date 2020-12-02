---
title: AEM Foundation和儲存庫
description: Adobe Experience Manager平台和儲存庫的發行說明。
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# AEM Foundation和Repository {#aem-foundation-repository}

## 變更清單{#list-of-changes}

### 存放庫 {#repository}

* Adobe Experience Manager 6.5的基礎建立在OSGi架構（Apache Sling和Apache Felix）和Java內容存放庫的更新版本之上：Apache Jackrabbit Oak 1.10.2.
* 如需已修正問題的概觀，請參閱[Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)、[Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt)和[Apache Jackrabbit Oak Jira v. 1.1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)。

>[!CAUTION]
>
>自AEM 6.3以來，Oak Segment Tar的新版本需要儲存庫移轉。 如果您要從舊版TarMK升級，或想要從其他永續性類型切換新的區段Tar，此步驟為必要步驟。 如需新區段Tar的優點的詳細資訊，請參閱[移轉至Oak區段Tar常見問答集](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar)。

### Java支援{#java-support}

* Java 11以及已支援的Java 8的新支援。
* 為獲得最佳效能，請用其他值覆蓋預設GC值。 如需詳細資訊，請參閱[安裝與更新](/help/sites-deploying/custom-standalone-install.md)一節。
* Java 11和Java 8維護更新由Adobe分發，以便客戶在AEM相關專案中使用，但Oracle未公開提供。

### OSGI {#osgi}

* 已新增OSGi Promises和Converter公用程式庫。

### 專案和工作流程{#projects-and-workflows}

* 6.4版中新增的「工作流程模型」編輯器已經過改良，加入更多作業，例如「複製」和「發佈」、「工作流程」步驟中的「變數」支援，以及增強的`OR`和`AND`分割。

### 搜尋 {#searching}

* 在Oak中搜尋現在支援動態Facet。 例如，資產搜尋中的篩選邊欄會顯示估計的結果量。
* QueryBuilder已擴充，可提供動態Facet結果。

### 安全性 {#security}

* 已新增管理員使用者的密碼到期。

### 使用者介面{#user-interface}

UI已做了各種增強功能，讓它更有生產力，也更容易使用。

* AEM 6.5推出新的「使用者和群組的權限管理UI」，讓您更輕鬆地檢視和設定整個權限和限制集，而不需前往CRXDE。
* 欄檢視現在也只會載入螢幕上可見的項目，而且只會在使用者開始捲動時載入更多項目。 清單和卡片檢視自6.0起就已執行此動作（在6.4中已改善）。
* 欄檢視現在包含頁面／資產的工作流程狀態（如果適用）。
* 「全選」動作是在相同資料夾中執行所有頁面／資產動作的快速方式。
* 「全選」動作會嘗試對所有頁面／資產執行動作，而不只是載入的內容。 如果動作未升級為處理大量動作，則會顯示警告。

>[!CAUTION]
>
>Adobe不會對Classic UI做進一步的增強。 Experience Manager 6.5包含Classic UI，以提供回溯相容性。 Classic UI仍完全受支援，不再提倡[閱讀更多內容](/help/sites-deploying/ui-recommendations.md)。

### 升級{#upgrade}

* 升級程式在6.5中基本保持不變。
* 我們繼續支援6.4版中推出的回溯相容性、升級複雜性評估和持續升級功能。在需要時，已對這些區域進行了特定版本的更新。
* Pattern Detector封裝已經簡化，而且將有一個封裝評估可用來源版本的6.5升級。
* 有關升級過程的詳細資訊，請參閱[升級文檔](/help/sites-deploying/upgrade.md)。

### Web伺服器{#web-server}

* Quickstart散發使用Eclipse Jetty 9.4.15做為servlet引擎（AEM 6.4隨附9.3.22）。
