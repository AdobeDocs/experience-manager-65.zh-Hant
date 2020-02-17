---
title: 效能測試的最佳實務
seo-title: 效能測試的最佳實務
description: 本文概述用於效能測試的整體策略和方法，以及可協助執行此程式的部分工具。
seo-description: 本文概述用於效能測試的整體策略和方法，以及可協助執行此程式的部分工具。
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 效能測試的最佳實務{#best-practices-for-performance-testing}

## 簡介 {#introduction}

效能測試是任何AEM部署的重要部分。 視客戶需求而定，可對發佈例項、作者例項或兩者執行效能測試。

本檔案將概述執行效能測試的整體策略和方法，以及Adobe提供的一些工具，以協助執行此程式。 最後，我們將從程式碼分析和系統組態角度分析AEM 6中提供的一些工具，以協助進行效能調整。

### 模擬現實 {#simulating-reality}

執行效能測試時，最重要的是確保您盡可能地模仿生產環境。 雖然這通常很困難，但必須確保這些測試的準確性。 在設計效能測試時，必須考慮以下幾點：

* 類似生產的內容

AEM中的許多效能度量（例如查詢回應時間）可能會受到系統內容大小的影響。 請務必確保測試環境盡可能接近生產資料的副本。

* 生產程式碼

部署在生產環境中的AEM版本和修補程式在測試環境中應相同。 測試部署至生產環境的程式碼版本也很重要。

* 類似生產的硬體和網路配置

如果沒有盡可能接近生產環境，這些測試將毫無意義。 理想情況下，硬體規格、網路介面、負載平衡器和CDN應與測試環境中的製作相同。

* 生產負載

許多效能問題都要等到系統負載過重時才會出現。 良好的效能測試應模擬生產系統在高峰時的負載。

### 設定目標 {#setting-goals}

在開始進行效能測試之前，必須設定非功能性需求以指定負載和回應時間。 如果您要從現有系統移轉，請確定回應時間與目前的生產值類似。 對於負載，最好將當前峰值負載加倍。 這可確保網站在成長時仍能繼續良好運作。

### 工具 {#tools}

市場上有許多市面上可用的效能測試工具。 在運行負載生成工具時，必須確保執行測試的電腦具有足夠的網路頻寬。 否則，一旦測試機達到其連接極限，將不會在測試環境中產生額外負載。

#### 測試工具 {#testing-tools}

* Adobe的 **Tough Day** tool can be used to generate load on AEM instances and collect performance data. Adobe的AEM工程團隊實際上使用此工具來測試AEM產品本身。 在Tough Day中執行的指令碼是透過屬性檔案和JMX XML檔案來設定。 如需詳細資訊，請參閱 [Tough Day檔案](/help/sites-developing/tough-day.md)。

* AEM提供立即可用的工具，讓您快速查看有問題的查詢、要求和錯誤訊息。 如需詳細資訊，請參 [閱Operations Dashboard檔案的Diagnosis Tools](/help/sites-administering/operations-dashboard.md#diagnosis-tools) （診斷工具）一節。
* Apache提供了名為 **JMeter** 的產品，可用於效能和負載測試以及功能行為。 它是開放原始碼軟體，可免費使用，但其功能比企業產品要小，學習曲線也更陡。 JMeter可在Apache的網站上找到，網址為 [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** 是企業級負載測試產品。 提供免費試用版。 如需詳細資訊，請造訪 [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* 也可使用雲端負載測 [試工具](https://www.neustar.biz/services/web-performance/load-testing) ，例如Neustar。
* 在測試行動或互動式網站時，需要使用個別的工具集。 它們可以調節網路頻寬，模擬慢速的行動連線，例如3G或EDGE。 使用範圍更廣的工具包括：

   * **[Network Link Condition](https://nshipster.com/network-link-conditioner/)**—— 它提供易於使用的UI，在網路堆棧上工作級別較低。 它包含OS x和iOS的版本；[](https://nshipster.com/network-link-conditioner/)
   * [**Charles **](https://www.charlesproxy.com/)—— 除了其他幾種用途外，還提供網路調節的Web調試代理應用程式。 提供Windows、OS x和Linux版本。[](https://www.charlesproxy.com/)

#### 最佳化工具 {#optimization-tools}

**監控**

「監 [控效能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) 」文檔是工具和方法的一個好資源，可用於診斷問題並查找要調整的區域。

**Touch UI中的開發人員模式**

AEM 6觸控UI的其中一項新功能是「開發人員模式」。 如同作者可在編輯和預覽模式之間切換，開發人員可在作者UI中切換至開發人員模式，以檢視頁面上每個元件的演算時間，並檢視任何錯誤的堆疊追蹤。 如需開發人員模式的詳細資訊，請參 [閱此CQ Gems簡報](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)。

**使用rlog.jar讀取請求日誌**

若要更全面地分析AEM系統上的請求記錄檔， `rlog.jar` 可用來搜尋AEM產生的檔 `request.log` 案並排序。 此jar檔案隨附於資料夾中的AEM安 `/crx-quickstart/opt/helpers` 裝。 如需記錄工具和一般要求記錄的詳細資訊，請參閱監 [控與維護檔案](/help/sites-deploying/monitoring-and-maintaining.md) 。

**Explain Query Tool**

ACS AEM Tools [中的Explain Query](/help/sites-administering/operations-dashboard.md#explain-query) （解釋查詢）工具可用於查看運行查詢時使用的索引。 在優化慢速運行查詢時，這非常有用。

**PageSpeed工具**

Google的PageSpeed工具提供網站分析，以符合最佳頁面效能實務，以及可與Apache執行個體之分派程式一起安裝的外掛程式，以進行其他最佳化。 如需詳細資訊，請參 [閱PageSpeed工具網站](https://developers.google.com/speed/pagespeed/)。

## 作者環境 {#author-environment}

### 執行測試 {#performing-tests}

為了對作者環境進行效能測試，必須模擬生產作者的經驗。 這表示作者安裝必須包含所有元件、OSGi組合、UI自訂、自訂索引，以及您為生產作者實例所準備的任何其他新增功能。

目前有許多自動化架構都是針對效能和負載測試而設計。 您可在這些工具中記錄自訂指令碼，然後播放以模擬同時執行類似內容建立和啟動活動的作者人數尖峰。 建議您使用「艱難日」工具來模擬上傳數千個資產或啟動大量頁面等活動。

對於需要大量資產載入或製作頁面的環境類型，必須使用Tough Day等工具，以確保環境在高峰負載下能有效運作。 [WebDAV](/help/sites-administering/webdav-access.md) 是不需要編寫指令碼的工具，也可用來載入大量資產。

#### MongoDB特定步驟 {#mongodb-specific-steps}

在具有MongoDB後端的系統上，AEM提供數個 [JMX](/help/sites-administering/jmx-console.md) MBean，當執行負載或效能測試時需要監控：

* 統一 **快取統計** MBean。 您可以直接前往：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

對於名為 **Document-Diff的快取**，點擊率應該已結束 `.90`。 如果點擊率低於90%，您可能需要修改您的設 `DocumentNodeStoreService` 定。 Adobe產品支援可以建議您的環境最佳設定。

* Oak Repository **統計資料** Mbean。 您可以直接前往：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

「 **ObservationQueueMaxLength** 」區段將顯示Oak在過去數小時、數分鐘、數秒和數週內的觀察佇列事件數。 在「每小時」區段中尋找最大的事件數。 此數字需要與 `oak.observation.queue-length` OSGi **主控台中** SlingRepositoryManager元件中的設定進行比較 [](/help/sites-deploying/web-console.md)。 如果觀察佇列顯示的最高數目超過設定值，請 `queue-length` 聯絡Adobe支援以取得提升設定的協助。 預設設定為1,000，但大部分的部署通常需要將它提高至20,000或50,000。

## 發佈環境 {#publish-environment}

### 執行測試 {#performing-tests-1}

部署中需要接受負載測試的最重要部分是面向最終用戶的發佈或分發程式環境。

協力廠商自動化測試工具可用來測試網站的效能。 這些工具可讓您記錄使用者在網站上執行的步驟，並同時執行其中許多作業，以模擬生產網站的典型負載。

大部份的生產網站都有最佳化功能，例如Dispatcher快取和內容傳送網路。 在測試時，您需要確定這些最佳化也適用於測試環境。 除了監控使用者的回應時間外，您還需要監控發佈伺服器和調度程式上的系統度量，以確保系統不受硬體資源的限制。

在不需要高度個人化的系統上，調度程式應快取大多數請求。 因此，發佈例項的載入應維持相對平坦。 如果需要高度個人化，建議使用iFrames或AJAX要求等技術來處理個人化內容，以便盡可能多地進行分派程式快取。

在基本測試中，Apache Bench可用來測量Web伺服器回應時間，並協助建立負載以測量記憶體洩漏等項目。 如需詳細資訊，請參閱「監控」文 [件中的範例](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)。

## 疑難排解效能問題 {#troubleshooting-performance-issues}

在作者實例上運行效能測試後，需要調查、診斷和解決任何問題。 在執行分析和解決問題時，可以使用幾種工具和技術：

* 您可以檢查「操 [作儀表板](/help/sites-administering/operations-dashboard.md#request-performance) 」中的「請求效能」日誌。 此工具可用來識別緩慢的頁面請求
* 使用查詢效能工具分析慢 [速運行的查詢](/help/sites-administering/operations-dashboard.md#query-performance)

* 觀看錯誤或警告的錯誤清單。 如需詳細資訊，請參閱記 [錄](/help/sites-deploying/configure-logging.md)
* 監控系統硬體資源，如記憶體和CPU利用率、磁碟I/O或網路I/O。這些資源通常是導致效能瓶頸的原因
* 最佳化頁面的架構及其處理方式，將URL參數的使用降至最低，以允許盡可能多的快取
* 遵循「效 [能最佳化](/help/sites-deploying/configuring-performance.md) 」和「效 [能調整」提示檔案](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

* 如果編輯作者例項上的特定頁面或元件時發生問題，請使用TouchUI開發人員模式來檢查相關頁面。 這將提供頁面上每個內容區域的劃分以及載入時間
* 精簡網站上的所有JS和CSS。 如需如何執行此動作的詳細資訊，請參閱此部 [落格文章](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)。
* 毋需從元件中內嵌CSS和JS。 應隨用戶端程式庫一起加入和調整這些程式庫，以盡量減少轉譯頁面所需的請求數
* 使用瀏覽器工具（例如Chrome的「網路」索引標籤）來檢查伺服器要求，並查看哪些要求耗時最長。

一旦發現問題區域，就可檢查應用程式碼以進行效能最佳化。 Adobe支援可解決任何無法正確執行的現成可用AEM功能。
