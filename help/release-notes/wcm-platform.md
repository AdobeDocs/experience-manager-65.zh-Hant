---
title: AEM Foundation和存放庫
description: Adobe Experience Manager平台和存放庫發行說明。
exl-id: 06938419-392b-432d-ba0c-ba444b3e141c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# AEM Foundation和存放庫{#aem-foundation-repository}

## 更改清單{#list-of-changes}

### 存放庫 {#repository}

* Adobe Experience Manager 6.5的基礎以更新版本的OSGi型架構（Apache Sling和Apache Felix）和Java Content Repository為基礎而構建：阿帕奇·傑克拉布特奧克1.10.2。
* 如需已修正問題的概觀，請參閱[Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)、[Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt)及[Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)。

>[!CAUTION]
>
>自AEM 6.3以來出現的新版Oak Segment Tar需要移轉存放庫。 如果您從舊版TarMK升級，或想從其他類型的永續性切換新的區段Tar，此步驟為必要步驟。 如需新區段Tar有何優點的詳細資訊，請參閱[移轉至Oak區段Tar常見問題集](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar)。

### Java支援{#java-support}

* Java 11的新支援，以及已支援的Java 8。
* 為獲得最佳效能，請用其他值覆蓋預設GC值。 有關詳細資訊，請參閱[安裝和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* Java 11和Java 8維護更新會由Adobe發佈，供AEM相關專案的客戶使用，但不可從Oracle公開取得。

### OSGI {#osgi}

* 新增OSGi Promises和Converter公用程式程式庫。

### 專案和工作流程{#projects-and-workflows}

* 6.4版中推出的新工作流程模型編輯器已經過改良，現在包含更多操作，例如複製和發佈、工作流程步驟中的變數支援，以及增強的`OR`和`AND`分割。

### 搜尋 {#searching}

* 在Oak中搜尋現在支援動態Facet。 例如，資產搜尋中的篩選邊欄會顯示預估的結果量。
* QueryBuilder已擴充，以提供含有動態Facet的結果。

### 安全性 {#security}

* 新增管理員使用者的密碼過期。

### 使用者介面{#user-interface}

UI已經過多種增強功能，讓工作效率更高，使用更輕鬆。

* AEM 6.5推出適用於使用者和群組的全新權限管理UI，讓您更輕鬆地檢視和設定整組權限和限制，而無需前往CRXDE。
* 欄檢視現在也只會載入畫面上可見的項目，且只會在使用者開始捲動時載入更多。 自6.0以來（在6.4中改善），清單和卡片檢視便已執行此動作。
* 欄檢視現在包含頁面/資產的工作流程狀態（若適用）。
* 「全部選取」動作是對相同資料夾中所有頁面/資產執行動作的快速方式。
* 「全部選取」動作會嘗試對所有頁面/資產執行動作，而不只是載入的內容。 如果動作未升級為處理大量動作，則會顯示警告。

>[!CAUTION]
>
>Adobe將不會對傳統UI進行進一步的增強。 Experience Manager6.5包含傳統UI，以便回溯相容。 過時的傳統UI仍完全支援[了解詳情](/help/sites-deploying/ui-recommendations.md)。

### 升級 {#upgrade}

* 6.5中的升級程式基本相同。
* 我們繼續支援6.4中推出的「向後相容性」、「升級複雜性評估」和「可持續升級」功能。根據需要對這些領域進行了版本特定的更新。
* 模式偵測器封裝已簡化，且將有一個套件評估可用來源版本的6.5升級。
* 有關升級過程的詳細資訊，請參閱[升級文檔](/help/sites-deploying/upgrade.md)。

### Web伺服器{#web-server}

* 快速入門發佈使用Eclipse Jetty 9.4.15作為servlet引擎(AEM 6.4隨9.3.22提供)。
