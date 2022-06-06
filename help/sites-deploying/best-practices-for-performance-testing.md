---
title: 效能測試的最佳做法
seo-title: Best Practices for Performance Testing
description: 本文概述了用於效能測試的總體戰略和方法，以及可用於協助該過程的一些工具。
seo-description: This article outlines the overall strategies and methodologies used for performance testing as well as some of the tools that are available to assist in the process.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: e8320b1dac681fd2c9e749344e8c126487d840ba
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 0%

---

# 效能測試的最佳做法{#best-practices-for-performance-testing}

## 簡介 {#introduction}

效能測試是任何部署的重要AEM部分。 根據客戶要求，可對發佈實例、作者實例或兩者執行效能測試。

本文檔將概述執行業績test的總體戰略和方法，以及Adobe為協助執行該過程而提供的一些工具。 最後，我們將從代碼分析和系統配置角度分析AEM6中提供的一些工具，以幫助進行效能調整。

### 模擬現實 {#simulating-reality}

執行效能test時，最重要的是確保盡可能地模仿生產環境。 雖然這往往很困難，但必須確保這些test的準確性。 在設計效能test時，必須考慮以下幾點：

* 類似生產的內容

系統中的許AEM多效能度量（如查詢響應時間）都可能受系統內容大小的影響。 必須確保test環境盡可能接近生產資料的副本。

* 生產代碼

在生AEM產環境中部署的版本和修補程式應相同。 test部署到生產環境的代碼版本也很重要。

* 類似於生產的硬體和網路配置

如果沒有與生產盡可能相似的環境，test將毫無意義。 理想情況下，硬體規格、網路介面、負載平衡器和CDN應與test環境中的生產相同。

* 生產負荷

許多效能問題只有在系統負載過重時才會出現。 良好的效能test應模擬生產系統在其高峰時所受的負載。

### 設定目標 {#setting-goals}

在開始效能測試之前，必須設定非功能要求以指定負載和響應時間。 如果要從現有系統遷移，請確保響應時間與當前生產值類似。 對於負載，最好將當前峰值負載加倍。 這將確保網站在增長時繼續表現良好。

### 工具 {#tools}

市場上有許多市售的效能測試工具。 運行負載生成工具時，必須確保正在執行test的電腦具有足夠的網路頻寬。 否則，一旦test機達到其連接的限制，在test下的環境上將不會產生附加負載。

#### 測試工具 {#testing-tools}

* Adobe **艱難的一天** 工具可用於生成實例上AEM的負載並收集效能資料。 AdobeAEM的工程團隊實際使用該工具對產品本身進AEM行負載測試。 在「艱難日」中執行的指令碼是通過屬性檔案和JMX XML檔案配置的。 有關詳細資訊，請參見 [艱難的日期文檔](/help/sites-developing/tough-day.md)。

* 提AEM供現成的工具，可快速查看有問題的查詢、請求和錯誤消息。 有關詳細資訊，請參見 [診斷工具](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 的子目錄。
* Apache提供名為 **JMeter** 可用於效能和負載測試以及功能行為。 它是開源軟體，可免費使用，但其特徵集比企業產品小，學習曲線也比較陡。 JMeter可在Apache的網站上找到，網址為： [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **載入運行器** 是企業級負載測試產品。 提供免費評估版本。 有關詳細資訊，請參閱 [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* 基於雲的負載測試工具，如 [新星](https://www.neustar.biz/services/web-performance/load-testing) 也可用。
* 在測試移動網站或響應網站時，需要使用一套單獨的工具。 它們通過限制網路頻寬、模擬速度較慢的移動連接（如3G或EDGE）來工作。 使用範圍更廣的工具包括：

   * **[網路鏈路調節器](https://nshipster.com/network-link-conditioner/)**  — 它提供易於使用的UI，在網路堆棧上工作的級別相當低。 它包括OS X和iOS版；
   * [**查爾斯**](https://www.charlesproxy.com/)  — 除了其他幾種用途外，還提供網路限制的Web調試代理應用程式。 Windows、OS X和Linux提供版本。

#### 優化工具 {#optimization-tools}

**監控**

的 [監視效能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) 文檔是工具和方法的好資源，可用於診斷問題和確定調整區域。

**Touch UI中的開發人員模式**

6的觸摸UI中的一AEM項新功能是開發人員模式。 正如作者可以在編輯和預覽模式之間切換一樣，開發人員也可以在作者UI中切換到開發者模式，以查看頁面上每個元件的呈現時間以及查看任何錯誤的堆棧跟蹤。 有關開發人員模式的詳細資訊，請參閱 [CQ Gems演示文稿](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)。

**使用rlog.jar讀取請求日誌**

要更全面地分析系統上的請求日AEM志， `rlog.jar` 可用於搜索和排序 `request.log` 生成的AEM檔案。 此jar檔案隨安裝一起AEM包含在 `/crx-quickstart/opt/helpers` 的子菜單。 有關日誌工具和一般請求日誌的詳細資訊，請參見 [監視和維護](/help/sites-deploying/monitoring-and-maintaining.md) 文檔。

**解釋查詢工具**

的 [解釋查詢工具](/help/sites-administering/operations-dashboard.md#explain-query) 在ACS AEM Tools中可用於查看運行查詢時使用的索引。 這在優化運行緩慢的查詢時非常有用。

**PageSpeed工具**

Google的PageSpeed工具提供了站點分析，以符合頁面效能的最佳做法，並提供了一個插件，可以與Apache實例上的調度程式一起安裝，以進行其他優化。 有關詳細資訊，請參見 [PageSpeed工具網站](https://developers.google.com/speed/pagespeed/)。

## 作者環境 {#author-environment}

### 執行Test {#performing-tests}

為了在作者環境中進行效能測試，必須模擬生產作者的體驗。 這意味著作者安裝必須包含您為生產作者實例準備的所有元件、OSGi捆綁包、UI自定義、自定義索引和任何其他添加。

有許多自動化框架可用於效能和負載測試。 可以在這些工具中記錄自定義指令碼，然後回放以模擬同時執行類似內容建立和激活活動的作者人數的峰值。 建議您使用Tough Day工具來模擬諸如上載數千個資產或激活大量頁面等活動。

對於需要大量資產載入或頁面創作的環境類型，必須使用「艱難日」等工具，以確保環境在峰值負載下能夠高效運行。 [WebDAV](/help/sites-administering/webdav-access.md) 是一種不需要指令碼編寫的工具，也可用於載入大量資產。

#### MongoDB特定步驟 {#mongodb-specific-steps}

在具有MongoDB後端的系統上，AEM提供 [JMX](/help/sites-administering/jmx-console.md) 執行負載或效能test時需要監視的MBean:

* 的 **合併的快取統計資訊** MBean。 可通過以下方式直接訪問：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

對於名為 **文檔比較**，命中率應該結束 `.90`。 如果命中率低於90%，您可能需要修改 `DocumentNodeStoreService` 配置。 Adobe產品支援可為您的環境推薦最佳設定。

* 的 **Oak儲存庫統計資訊** 豆。 可通過以下方式直接訪問：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

的 **ObservationQueueMaxLength** 部分將顯示Oak觀察隊列中過去幾小時、分、秒和周的事件數。 在「每小時」部分中查找事件的最大數量。 需要將此數字與 `oak.observation.queue-length` 的子菜單。 如果為觀察隊列顯示的最高數目超過 `queue-length` 設定：

1. 建立名為： `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` 包含參數 `oak.observation.queue‐length=50000`
1. 將其置於/crx-quickstart/install資料夾下。

>[!NOTE]
>另請參見上的知識文庫文章 [AEM 6.x |效能優化提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

預設設定為10,000，但大多數部署通常需要將其提高到20,000或50,000。

## 發佈環境 {#publish-environment}

### 執行Test {#performing-tests-1}

部署中最重要的部分是面向最終用戶的發佈test或調度程式環境。

第三方自動測試工具可用於test網站的效能。 這些工具允許您記錄用戶將在站點上執行的步驟，並同時運行其中的許多會話，以模擬生產網站的典型負載。

大多數生產網站都進行了優化，如調度程式快取和內容傳遞網路。 在測試時，您需要確保這些優化也適用於test環境。 除了監視最終用戶的響應時間之外，您還需要監視發佈伺服器和調度程式上的系統度量，以確保系統不受硬體資源的限制。

在不需要高度個性化的系統上，調度程式應快取大多數請求。 因此，發佈實例上的負載應保持相對平坦。 如果需要高級別的個性化，建議使用諸如iFrames或對個性化內容的AJAX請求等技術，以便允許盡可能多的調度程式快取。

對於基本test,Apache Bench可用於測量Web伺服器響應時間，並幫助建立用於測量記憶體洩漏之類的負載。 有關詳細資訊，請參閱 [監控文檔](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)。

## 效能問題疑難解答 {#troubleshooting-performance-issues}

在對作者實例運行效能test後，需要調查、診斷和解決任何問題。 在執行分析和解決問題時，可以使用多種工具和技術：

* 您可以檢查 [請求效能日誌](/help/sites-administering/operations-dashboard.md#request-performance) 中。 此工具可用於標識慢速頁面請求
* 使用 [查詢效能工具](/help/sites-administering/operations-dashboard.md#query-performance)

* 查看錯誤清單中的錯誤或警告。 有關詳細資訊，請參見 [記錄](/help/sites-deploying/configure-logging.md)
* 監視系統硬體資源，如記憶體和CPU利用率、磁碟I/O或網路I/O。這些資源通常是效能瓶頸的原因
* 優化頁面的體系結構以及如何定址這些頁面，以最小化URL參數的使用，以允許盡可能多地進行快取
* 關注 [效能優化](/help/sites-deploying/configuring-performance.md) 和 [效能調整提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 文檔

* 如果在作者實例上編輯某些頁面或元件時出現問題，請使用TouchUI開發人員模式來檢查有關頁面。 這將提供頁面上每個內容區域的細分及其載入時間
* 精簡站點上的所有JS和CSS。 有關如何執行此操作的詳細資訊，請參閱 [部落格帖子](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)。
* 從元件中刪除嵌入的CSS和JS。 應將它們包括在客戶端庫中並與其進行精簡，以最大限度地減少呈現頁面所需的請求數
* 使用瀏覽器工具（如Chrome的「網路」頁籤）檢查伺服器請求，並查看哪些請求花費的時間最長。

一旦確定了問題區域，就可以檢查應用程式碼以進行效能優化。 任何未正AEM常執行的開箱功能都可以通過Adobe支援解決。
