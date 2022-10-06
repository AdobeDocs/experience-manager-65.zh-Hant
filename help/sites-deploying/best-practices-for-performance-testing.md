---
title: 效能測試最佳實務
seo-title: Best Practices for Performance Testing
description: 本文概述用於效能測試的總體戰略和方法，以及一些可用於協助該過程的工具。
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

# 效能測試最佳實務{#best-practices-for-performance-testing}

## 簡介 {#introduction}

效能測試是任何AEM部署的重要部分。 效能測試可能會根據客戶需求，對發佈例項、製作例項或兩者執行。

本檔案將概述執行效能測試的總體戰略和方法，以及Adobe提供的一些工具，以協助執行該過程。 最後，我們將從代碼分析和系統配置角度分析AEM 6提供的一些工具，以幫助進行效能調整。

### 模擬現實 {#simulating-reality}

執行效能測試時，最重要的是確保您盡可能模擬生產環境。 雖然這通常很困難，但必須確保這些測試的準確性。 在設計效能測試時，必須考慮以下幾點：

* 類似生產的內容

AEM中的許多效能測量（例如查詢回應時間）可能會受到系統上內容的大小影響。 請務必確保測試環境盡可能接近生產資料的副本。

* 生產程式碼

生產環境中部署的AEM版本和Hotfix應與測試環境相同。 此外，還必須測試部署至生產環境的程式碼版本。

* 生產類硬體和網路配置

如果沒有盡可能接近生產環境，這些測試就毫無意義。 理想情況下，硬體規格、網路介面、負載平衡器和CDN應與測試環境中的生產環境相同。

* 生產負載

在系統負載過重之前，系統不會出現許多效能問題。 良好的效能測試應模擬生產系統在其峰值時所受的負載。

### 設定目標 {#setting-goals}

開始進行效能測試之前，必須設定非功能需求，以指定負載和回應時間。 如果您要從現有系統移轉，請確定回應時間與目前的生產值類似。 對於負載，最好採用當前峰值負載，將其加倍。 這可確保網站在成長時仍可繼續正常運作。

### 工具 {#tools}

市場上有許多市面上可用的效能測試工具。 運行負載生成工具時，必須確保執行測試的電腦具有足夠的網路頻寬。 否則，一旦測試機達到其連接極限，就不會在被測試的環境中產生額外負載。

#### 測試工具 {#testing-tools}

* Adobe **艱難的一天** 工具可用來在AEM例項產生負載並收集效能資料。 Adobe的AEM工程團隊實際上會使用此工具來測試AEM產品本身。 在艱難時刻執行的指令碼是通過屬性檔案和JMX XML檔案配置的。 如需詳細資訊，請參閱 [艱難的一天檔案](/help/sites-developing/tough-day.md).

* AEM提供現成可用的工具，可快速查看有問題的查詢、要求和錯誤訊息。 如需詳細資訊，請參閱 [診斷工具](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 操作控制面板檔案的區段。
* Apache提供以下產品： **JMeter** 可用於效能和負載測試以及功能行為。 它是開源軟體，可免費使用，但功能集比企業產品小，學習曲線也更陡。 JMeter可在Apache的網站上找到，網址為 [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **載入運行器** 是企業級負載測試產品。 提供免費評估版本。 如需詳細資訊，請參閱 [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* 雲端負載測試工具，例如 [諾伊斯塔](https://www.neustar.biz/services/web-performance/load-testing) 也可使用。
* 若是測試行動或回應式網站，則需使用個別的工具集。 它們通過調節網路頻寬，模擬慢速移動連接（如3G或EDGE）來工作。 使用範圍更廣的工具包括：

   * **[網路鏈路調節器](https://nshipster.com/network-link-conditioner/)**  — 它提供易於使用的UI，並且在網路堆棧中處於相當低的級別工作。 包含OS X和iOS的版本；
   * [**Charles**](https://www.charlesproxy.com/)  — 除了其他幾種用途外，還提供網路節流的Web調試代理應用程式。 提供Windows、OS X和Linux版本。

#### 最佳化工具 {#optimization-tools}

**監控**

此 [監控效能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) 說明檔案是工具和方法的好資源，可用來診斷問題和找出調整的區域。

**觸控式UI中的開發人員模式**

AEM 6的觸控式UI中，有一項新功能是開發人員模式。 就像作者可在編輯和預覽模式之間切換一樣，開發人員可在製作UI中切換至開發人員模式，以查看頁面上每個元件的轉譯時間，以及查看任何錯誤的堆疊追蹤。 如需開發人員模式的詳細資訊，請參閱 [CQ Gems簡報](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

**使用rlog.jar讀取請求日誌**

如需更全面分析AEM系統上的要求記錄， `rlog.jar` 可用來搜尋和排序 `request.log` AEM產生的檔案。 此jar檔案會隨AEM安裝一起包含在 `/crx-quickstart/opt/helpers` 檔案夾。 如需記錄工具和要求記錄的詳細資訊，請參閱 [監控與維護](/help/sites-deploying/monitoring-and-maintaining.md) 檔案。

**說明查詢工具**

此 [說明查詢工具](/help/sites-administering/operations-dashboard.md#explain-query) 在ACS AEM工具中，可用於查看運行查詢時使用的索引。 這在優化慢速運行查詢時非常有用。

**PageSpeed Tools**

Google的PageSpeed工具提供網站分析，以符合頁面效能最佳實務，以及可與Apache執行個體上的dispatcher一併安裝的外掛程式，以做出其他最佳化。 如需詳細資訊，請參閱 [PageSpeed工具網站](https://developers.google.com/speed/pagespeed/).

## 製作環境 {#author-environment}

### 執行測試 {#performing-tests}

若要對製作環境進行效能測試，您必須模擬生產製作者的體驗。 這表示製作安裝必須包含所有元件、OSGi套件組合、UI自訂、自訂索引，以及您為生產製作例項準備的任何其他新增項目。

有許多自動化框架是專為效能和負載測試而設計的。 您可以在這些工具中記錄自訂指令碼，然後加以播放，以模擬同時執行類似內容建立和啟動活動的作者人數高峰。 建議您使用「艱難日」工具來模擬活動，例如上傳數千個資產或啟用大量頁面。

對於需要大量資產載入或頁面編寫的環境類型，必須使用Tough Day等工具，以確保環境在峰值負載下能有效運作。 [WebDAV](/help/sites-administering/webdav-access.md) 是不需要指令碼的工具，也可用來載入大量資產。

#### MongoDB特定步驟 {#mongodb-specific-steps}

在後端有MongoDB的系統上，AEM提供數個 [JMX](/help/sites-administering/jmx-console.md) 執行負載或效能測試時需要監控的MBeans:

* 此 **整合快取統計資訊** MBean。 您可以前往：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

對於名為的快取 **Document-Diff**，點擊率應該會結束 `.90`. 如果點擊率低於90%，您可能需要修改 `DocumentNodeStoreService` 設定。 Adobe產品支援可建議您的環境最佳設定。

* 此 **Oak存放庫統計資料** Mbean。 您可以前往：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

此 **ObservationQueueMaxLength** 區段會顯示Oak的觀察佇列中過去幾小時、分鐘、秒和周的事件數。 在「每小時」區段中找出最大的事件數。 此數字需要與 `oak.observation.queue-length` 設定。 如果觀察佇列顯示的最高數量超過 `queue-length` 設定：

1. 建立名為的檔案： `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` 包含參數 `oak.observation.queue‐length=50000`
1. 將其置於/crx-quickstart/install資料夾下。

>[!NOTE]
>另請參閱 [AEM 6.x |效能調整提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

預設設定為10,000，但大部分部署通常需要將其提高至20,000或50,000。

## 發佈環境 {#publish-environment}

### 執行測試 {#performing-tests-1}

部署中最需要接受載入測試的部分，是面對發佈或調度程式環境的一般使用者。

第三方自動化測試工具可用來測試網站的效能。 這些工具可讓您記錄使用者在網站上執行的步驟，並同時執行其中許多工作階段，以模擬生產網站的典型負載。

大部分的生產網站都已最佳化，例如Dispatcher快取和內容傳送網路。 測試時，您必須確定這些最佳化也適用於測試環境。 除了監控一般使用者的回應時間外，您也需監控發佈伺服器和調度程式上的系統量度，以確保系統不受硬體資源限制。

在不需要高層級個人化的系統上，Dispatcher應快取大部分的請求。 因此，發佈例項的負載應維持相對平坦。 如果需要高層級的個人化，建議對個人化內容使用iFrame或AJAX要求等技術，以便允許盡可能多的Dispatcher快取。

對於基本測試，Apache Bench可用於測量Web伺服器響應時間，並幫助建立用於測量記憶體洩漏等內容的負載。 如需詳細資訊，請參閱 [監控檔案](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## 疑難排解效能問題 {#troubleshooting-performance-issues}

在製作執行個體上執行效能測試後，任何問題都需要調查、診斷和解決。 在執行分析和解決問題時，您可以使用數種工具和技術：

* 您可以檢查 [請求效能日誌](/help/sites-administering/operations-dashboard.md#request-performance) （在操作控制面板中）。 此工具可用來識別緩慢的頁面請求
* 使用分析慢速運行的查詢 [查詢效能工具](/help/sites-administering/operations-dashboard.md#query-performance)

* 查看錯誤清單，了解錯誤或警告。 如需詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md)
* 監視系統硬體資源，如記憶體和CPU利用率、磁碟I/O或網路I/O。這些資源往往是效能瓶頸的原因
* 最佳化頁面架構及其處理方式，以盡量減少URL參數的使用，以允許盡可能多的快取
* 關注 [效能最佳化](/help/sites-deploying/configuring-performance.md) 和 [效能調校提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 檔案

* 如果在製作執行個體上編輯某些頁面或元件時發生問題，請使用觸控式UI開發人員模式來檢查相關頁面。 這可提供頁面上每個內容區域的劃分及其載入時間
* 縮制網站上的所有JS和CSS。 如需如何執行此動作的詳細資訊，請參閱 [部落格貼文](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* 從元件中消除內嵌的CSS和JS。 這些請求應隨用戶端程式庫一併縮制，以盡量減少呈現頁面所需的請求數
* 使用瀏覽器工具（例如Chrome的「網路」標籤）來檢查伺服器請求，並查看哪些請求花費的時間最長。

確定問題區域後，可檢查應用程式代碼以優化效能。 任何現成可用的AEM功能若未正確執行，可透過Adobe支援處理。
