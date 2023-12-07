---
title: 效能測試的最佳實務
description: 瞭解效能測試使用的整體策略和方法，以及可用於協助該流程的一些工具。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 0%

---

# 效能測試的最佳實務{#best-practices-for-performance-testing}

## 簡介 {#introduction}

效能測試是任何AEM部署的重要一環。 視客戶需求而定，可能會在發佈執行個體、製作執行個體或兩者上執行效能測試。

本檔案概述執行效能測試的整體策略和方法，以及Adobe為協助該過程而提供的一些工具。 最後，從程式碼分析和系統設定的角度，閱讀AEM 6中可用來協助效能調整的工具分析。

### 模擬現實 {#simulating-reality}

進行效能測試時，請務必儘可能模擬生產環境。 雖然這類工作通常很困難，但必須確保這些測試的準確性。 在設計效能測試時，務必要考慮以下幾點：

* 生產樣內容

AEM中的許多效能測量（例如查詢回應時間）都可能受到系統內容大小的影響。 務必確保測試環境儘可能接近生產資料的副本。

* 生產代碼

生產環境中部署的AEM版本和Hotfix在測試環境中應相同。 在部署至生產環境的程式碼版本上進行測試也很重要。

* 類似生產環境的硬體與網路組態

如果沒有儘可能接近生產環境的環境，這些測試就毫無意義。 理想情況下，硬體規格、網路介面、負載平衡器和CDN應與測試環境中的生產環境相同。

* 生產負載

許多效能問題直到系統負載過重才會出現。 良好的效能測試應該會模擬生產系統在其尖峰時的負載。

### 設定目標 {#setting-goals}

開始進行效能測試之前，必須設定非功能需求，以指定載入和回應時間。 如果您要從現有系統移轉，請確定回應時間與您目前的生產值類似。 對於負載，最好取用目前的峰值負載並將其加倍。 這麼做可確保網站在成長過程中能夠繼續表現良好。

### 工具 {#tools}

市面上有許多市售的效能測試工具。 執行負載產生工具時，請務必確保執行測試的電腦具有足夠的網路頻寬。 否則，一旦測試機器達到其連線的限制，則不會在受測試的環境中產生額外的負載。

#### 測試工具 {#testing-tools}

* Adobe的 **艱苦的一天** 工具可用來產生AEM執行個體的負載，以及收集效能資料。 Adobe的AEM工程團隊實際上會使用此工具來執行AEM產品本身的負載測試。 在「艱難日」中執行的指令碼會透過屬性檔案和JMX XML檔案來設定。 如需詳細資訊，請參閱 [艱苦日檔案](/help/sites-developing/tough-day.md).

* AEM提供立即可用的工具，可快速檢視有問題的查詢、請求和錯誤訊息。 如需詳細資訊，請參閱 [診斷工具](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 區段建立模型。
* Apache提供產品，稱為 **Jmeter** 可用於效能和負載測試，以及功能行為的資訊。 它是開放原始碼軟體，可以自由使用，但功能集比企業產品更小，而且學習曲線更陡峭。 您可在Apache的網站上找到JMeter，網址為 [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **載入執行器** 是企業級的負載測試產品。 提供免費的評估版本。 如需詳細資訊，請參閱 [https://www.microfocus.com/en-us/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)

* 網站負載測試工具，例如 [Vercara](https://vercara.com/website-performance-management) 也可使用。
* 測試行動或回應式網站時，必須使用另一組工具。 它們的工作方式是調節網路頻寬，模擬速度較慢的行動連線，如3G或EDGE。 使用範圍較廣的工具包括：

   * **[網路連結調節器](https://nshipster.com/network-link-conditioner/)**  — 它提供簡單易用的UI，在網路棧疊上以相當低的層級運作。 其中包括OS X和iOS的版本；
   * [**Charles**](https://www.charlesproxy.com/)  — 一種Web偵錯Proxy應用程式，除了其他幾種用途外，還提供網路節流。 提供適用於Windows、OS X和Linux®的版本。

#### 最佳化工具 {#optimization-tools}

**監視**

此 [監控效能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) 說明檔案是用來診斷問題並找出調整區域的工具與方法的實用資源。

**觸控式UI中的開發人員模式**

AEM 6觸控式UI的其中一項新功能是開發人員模式。 就像作者可以在編輯和預覽模式之間切換一樣，開發人員可以在作者UI中切換到開發人員模式。 這麼做可讓您檢視頁面上每個元件的轉譯時間，以及檢視任何錯誤的棧疊追蹤。 如需開發人員模式的詳細資訊，請參閱此 [CQ Gems簡報](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en).

**使用rlog.jar讀取請求記錄**

若要更全面地分析AEM系統上的請求記錄， `rlog.jar` 可用來搜尋及排序 `request.log` AEM產生的檔案。 此jar檔案包含在的AEM安裝中 `/crx-quickstart/opt/helpers` 資料夾。 如需有關登入工具和一般請求登入的詳細資訊，請參閱 [監控與維護](/help/sites-deploying/monitoring-and-maintaining.md) 檔案。

**說明查詢工具**

此 [說明查詢工具](/help/sites-administering/operations-dashboard.md#explain-query) 在ACS中，AEM工具可用於檢視執行查詢時使用的索引。 此工具在最佳化執行速度較慢的查詢時相當實用。

**PageSpeed Tools**

Google的PageSpeed工具提供網站分析，以符合頁面效能最佳實務，此外掛程式可與Dispatcher一起安裝在Apache執行個體上，以進行其他最佳化。
請參閱 [PageSpeed Tools網站](https://developers.google.com/speed).

## 作者環境 {#author-environment}

### 執行測試 {#performing-tests}

若要在作者環境中執行效能測試，您必須模擬生產作者的體驗。 也就是說，製作安裝必須包含所有元件、OSGi套件組合、UI自訂、自訂索引，以及您為生產製作執行個體準備的任何其他新增專案。

有許多針對效能和負載測試而設計的自動化架構。 自訂指令碼可以記錄在這些工具中，然後播放以模擬同時執行類似內容建立和啟用活動的作者尖峰數量。 建議您使用「首日」工具來模擬上傳數千個資產或啟用大量頁面等活動。

對於需要大量資產載入或頁面編寫的環境型別，必須使用「工作日」等工具。 如此可確保環境在尖峰負載下有效運作。 [WebDAV](/help/sites-administering/webdav-access.md) 是一種不需要指令碼的工具，也可用來載入大量資產。

#### MongoDB特定步驟 {#mongodb-specific-steps}

在具有MongoDB後端的系統上，AEM提供數個 [JMX](/help/sites-administering/jmx-console.md) 執行負載或效能測試時必須監視的MBean：

* 此 **整合的快取統計資料** MBean。 您可以透過以下位置直接存取該區域：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

針對指定的快取 **Document-Diff**，點選率應已超過 `.90`. 如果點選率降至90%以下，您可能必須編輯 `DocumentNodeStoreService` 設定。 Adobe產品支援可為您的環境建議最佳設定。

* 此 **Oak存放庫統計資料** Mbean。 您可以透過以下位置直接存取該區域：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

此 **ObservationqueueMaxLength** 區段會顯示Oak的觀察佇列中過去小時、分鐘、秒和周的事件數。 在「每小時」區段中找出事件數量最多者。 將此數字與 `oak.observation.queue-length` 設定。 如果為觀察佇列顯示的最高數量超過 `queue-length` 設定：

1. 建立名為的檔案： `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` 包含引數 `oak.observation.queue‐length=50000`
1. 將其放在/crx--quickstart/install資料夾下。

>[!NOTE]
>另請參閱 [AEM 6.x |效能調整秘訣](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en)

預設值為10,000，但大多數部署都必須將其提高至20,000或50,000。

## 發佈環境 {#publish-environment}

### 執行測試 {#performing-tests-1}

部署中必須接受負載測試的最重要部分是面向發佈或Dispatcher環境的一般使用者。

可使用協力廠商自動化測試工具來測試網站的效能。 這些工具可讓您記錄使用者在網站上執行的步驟，以及同時執行其中許多工作階段，以模擬生產網站中的典型負載。

大部分的生產網站都有最佳化功能，例如Dispatcher快取和內容傳遞網路都已準備就緒。 測試時，請確定這些最佳化也適用於測試環境。 除了監控使用者的回應時間之外，還要監控發佈伺服器和Dispatcher上的系統測量結果，以確保系統不受硬體資源的限制。

在不需要高度個人化的系統上，Dispatcher應該快取大部分的請求。 因此，發佈執行個體的負載應保持相對平坦。 如果需要高層的個人化，建議對個人化內容使用iFrame或AJAX請求等技術，以儘可能允許Dispatcher快取。

對於基本測試，Apache Bench可用於測量網頁伺服器回應時間，並幫助建立負載以測量記憶體流失等專案。 請參閱中的範例： [監控檔案](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## 疑難排解效能問題 {#troubleshooting-performance-issues}

在製作執行個體上執行效能測試後，必須調查、診斷並解決任何問題。 在執行分析和解決問題時，您可以使用數種工具和技術：

* 您可以檢查 [要求效能記錄](/help/sites-administering/operations-dashboard.md#request-performance) 在操作控制面板中。 此工具可用來識別緩慢的頁面請求
* 使用分析緩慢執行的查詢 [查詢效能工具](/help/sites-administering/operations-dashboard.md#query-performance)

* 檢視錯誤記錄檔中是否有錯誤或警告。 如需詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md).
* 監視系統硬體資源，例如記憶體和CPU使用率、磁碟I/O或網路I/O。這些資源通常是造成效能瓶頸的原因。
* 最佳化頁面的架構以及處理方式，以儘量減少URL引數的使用，進而允許儘可能多的快取。
* 請遵循 [效能最佳化](/help/sites-deploying/configuring-performance.md) 和 [效能調整秘訣](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en) 檔案。

* 如果編輯作者執行個體上的特定頁面或元件時發生問題，請使用TouchUI開發人員模式來檢查有問題的頁面。 這樣做會提供頁面上每個內容區域的劃分，及其載入時間。
* 將網站上的所有JS和CSS縮制。 檢視此 [部落格貼文](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* 排除元件中的內嵌CSS和JS。 使用者端程式庫應包含並加以縮制，以將轉譯頁面所需的請求數量降至最低。
* 若要檢查伺服器請求並檢視哪些請求的執行時間最長，請使用Chrome的「網路」標籤等瀏覽器工具。

一旦識別出問題區域，即可檢查應用程式程式碼以最佳化效能。 任何無法正常執行的現成AEM功能，都可以透過Adobe支援來處理。
