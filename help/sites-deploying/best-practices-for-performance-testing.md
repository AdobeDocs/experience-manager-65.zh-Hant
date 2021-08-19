---
title: 效能測試最佳實務
seo-title: 效能測試最佳實務
description: 本文概述用於效能測試的總體戰略和方法，以及一些可用於協助該過程的工具。
seo-description: 本文概述用於效能測試的總體戰略和方法，以及一些可用於協助該過程的工具。
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '1920'
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

* Adobe的&#x200B;**Tough Day**&#x200B;工具可用來在AEM例項上產生負載並收集效能資料。 Adobe的AEM工程團隊實際上會使用此工具來測試AEM產品本身。 在艱難時刻執行的指令碼是通過屬性檔案和JMX XML檔案配置的。 如需詳細資訊，請參閱[Tough Day documentation](/help/sites-developing/tough-day.md)。

* AEM提供現成可用的工具，可快速查看有問題的查詢、要求和錯誤訊息。 如需詳細資訊，請參閱Operations Dashboard檔案的[診斷工具](/help/sites-administering/operations-dashboard.md#diagnosis-tools)區段。
* Apache提供名為&#x200B;**JMeter**&#x200B;的產品，可用於效能和負載測試以及功能行為。 它是開源軟體，可免費使用，但功能集比企業產品小，學習曲線也更陡。 您可以在Apache的網站[https://jmeter.apache.org/](https://jmeter.apache.org/)找到JMeter

* **Load Runner** 是企業級負載測試產品。提供免費評估版本。 如需詳細資訊，請參閱[https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* 也可使用雲端負載測試工具，例如[Neustar](https://www.neustar.biz/services/web-performance/load-testing)。
* 若是測試行動或回應式網站，則需使用個別的工具集。 它們通過調節網路頻寬，模擬慢速移動連接（如3G或EDGE）來工作。 使用範圍更廣的工具包括：

   * **[網路連結調節器](https://nshipster.com/network-link-conditioner/)**  — 它提供易於使用的UI，並且在網路堆疊上工作的級別相當低。其中包含OS X和iOS的版本；
   * [**Charles**](https://www.charlesproxy.com/)  — 除了數個其他用途外，還提供網路節流功能的網頁除錯代理應用程式。提供Windows、OS X和Linux版本。

#### 最佳化工具 {#optimization-tools}

**監控**

[監視效能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)文檔是可用於診斷問題和查找調整區域的工具和方法的良好資源。

**觸控式UI中的開發人員模式**

AEM 6的觸控式UI中，有一項新功能是開發人員模式。 就像作者可在編輯和預覽模式之間切換一樣，開發人員可在製作UI中切換至開發人員模式，以查看頁面上每個元件的轉譯時間，以及查看任何錯誤的堆疊追蹤。 如需開發人員模式的詳細資訊，請參閱此[CQ Gems簡報](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)。

**使用rlog.jar讀取請求日誌**

要更全面地分析AEM系統上的請求日誌，可以使用`rlog.jar`搜索AEM生成的`request.log`檔案並對其進行排序。 `/crx-quickstart/opt/helpers`資料夾中的AEM安裝包含此jar檔案。 有關日誌工具和請求日誌的詳細資訊，請參閱[監視和維護](/help/sites-deploying/monitoring-and-maintaining.md)文檔。

**說明查詢工具**

ACS AEM工具中的[Explain Query Tool](/help/sites-administering/operations-dashboard.md#explain-query)可用於查看運行查詢時使用的索引。 這在優化慢速運行查詢時非常有用。

**PageSpeed Tools**

Google的PageSpeed工具提供網站分析，以符合頁面效能最佳實務，並提供外掛程式，可與Apache執行個體上的Dispatcher一併安裝，以作出其他最佳化。 如需詳細資訊，請參閱[PageSpeed工具網站](https://developers.google.com/speed/pagespeed/)。

## 製作環境 {#author-environment}

### 執行測試 {#performing-tests}

若要對製作環境進行效能測試，您必須模擬製作作者的體驗。 這表示製作安裝必須包含所有元件、OSGi套件組合、UI自訂、自訂索引，以及您為生產製作例項準備的任何其他新增項目。

有許多自動化框架是專為效能和負載測試而設計的。 您可以在這些工具中記錄自訂指令碼，然後加以播放，以模擬同時執行類似內容建立和啟動活動的作者人數高峰。 建議您使用「艱難日」工具來模擬活動，例如上傳數千個資產或啟用大量頁面。

對於需要大量資產載入或頁面編寫的環境類型，必須使用Tough Day等工具，以確保環境在峰值負載下能有效運作。 [](/help/sites-administering/webdav-access.md) WebDAV是不需要指令碼的工具，也可用於載入大量資產。

#### MongoDB特定步驟 {#mongodb-specific-steps}

在有MongoDB後端的系統上，AEM提供了幾個[JMX](/help/sites-administering/jmx-console.md) MBean，在執行負載或效能測試時需要監控：

* **統一快取統計資訊** MBean。 您可以前往：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

對於名為&#x200B;**Document-Diff**&#x200B;的快取，點擊率應大於`.90`。 如果點擊率低於90%，您可能需要修改`DocumentNodeStoreService`設定。 Adobe產品支援可建議您的環境最佳設定。

* **Oak Repository Statistics** Mbean。 您可以前往：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

**ObservationQueueMaxLength**&#x200B;區段將顯示Oak觀察佇列中過去幾小時、分鐘、秒和周的事件數。 在「每小時」區段中找出最大的事件數。 需要將此數字與`oak.observation.queue-length`設定進行比較，該設定可在[OSGi控制台](/help/sites-deploying/web-console.md)的&#x200B;**SlingRepositoryManager**&#x200B;元件中找到。 如果觀察佇列顯示的最高數量超過`queue-length`設定，請聯絡Adobe支援以取得提升設定的協助。 預設設定為1,000，但大部分部署通常需要將其提高至20,000或50,000。

## 發佈環境 {#publish-environment}

### 執行測試 {#performing-tests-1}

部署中最需要接受載入測試的部分，是面對發佈或調度程式環境的一般使用者。

第三方自動化測試工具可用來測試網站的效能。 這些工具可讓您記錄使用者在網站上執行的步驟，並同時執行其中許多工作階段，以模擬生產網站的典型負載。

大部分的生產網站都已最佳化，例如Dispatcher快取和內容傳送網路。 測試時，您必須確定這些最佳化也適用於測試環境。 除了監控一般使用者的回應時間外，您也需監控發佈伺服器和調度程式上的系統量度，以確保系統不受硬體資源限制。

在不需要高層級個人化的系統上，Dispatcher應快取大部分的請求。 因此，發佈例項的負載應維持相對平坦。 如果需要高層級的個人化，建議對個人化內容使用iFrame或AJAX要求等技術，以便允許盡可能多的Dispatcher快取。

對於基本測試，Apache Bench可用於測量Web伺服器響應時間，並幫助建立用於測量記憶體洩漏等內容的負載。 如需詳細資訊，請參閱[監控檔案](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)中的範例。

## 疑難排解效能問題 {#troubleshooting-performance-issues}

在製作執行個體上執行效能測試後，任何問題都需要調查、診斷和解決。 在執行分析和解決問題時，您可以使用數種工具和技術：

* 您可以在「操作控制面板」中檢查[請求效能日誌](/help/sites-administering/operations-dashboard.md#request-performance)。 此工具可用來識別緩慢的頁面請求
* 使用[查詢效能工具](/help/sites-administering/operations-dashboard.md#query-performance)分析慢速運行的查詢

* 查看錯誤清單，了解錯誤或警告。 如需詳細資訊，請參閱[記錄](/help/sites-deploying/configure-logging.md)
* 監視系統硬體資源，如記憶體和CPU利用率、磁碟I/O或網路I/O。這些資源往往是效能瓶頸的原因
* 最佳化頁面架構及其處理方式，以盡量減少URL參數的使用，以允許盡可能多的快取
* 請參閱[效能最佳化](/help/sites-deploying/configuring-performance.md)和[效能調整提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)檔案

* 如果在製作執行個體上編輯某些頁面或元件時發生問題，請使用觸控式UI開發人員模式來檢查相關頁面。 這可提供頁面上每個內容區域的劃分及其載入時間
* 縮制網站上的所有JS和CSS。 有關如何執行此操作的詳細資訊，請參閱此[部落格文章](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)。
* 從元件中消除內嵌的CSS和JS。 這些請求應隨用戶端程式庫一併縮制，以盡量減少呈現頁面所需的請求數
* 使用瀏覽器工具（例如Chrome的「網路」標籤）來檢查伺服器請求，並查看哪些請求花費的時間最長。

確定問題區域後，可檢查應用程式代碼以優化效能。 任何現成可用的AEM功能若未正確執行，可透過Adobe支援處理。
