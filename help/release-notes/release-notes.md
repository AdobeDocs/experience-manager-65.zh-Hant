---
title: ' [!DNL Adobe Experience Manager] 6.5的一般發行說明'
description: '[!DNL Adobe Experience Manager] 6.5說明，概述發行資訊、新增功能、安裝方式，以及詳細的變更清單。'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: f8fcfa9e09167cd4dbaafe938bcbe3ee6ece270f
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5的一般發行說明{#general-release-notes-for-adobe-experience-manager}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 |
| 類型 | 主要版本 |
| 正式發行日期 | 2019 年 4 月 8 日 |
| 建議的更新 | 請參閱[AEM最近更新](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)。 |

### Trivia {#trivia}

此版本[!DNL Adobe Experience Manager]的發行週期從2018年4月4日開始，經過23次反覆品質保證和錯誤修正，並於2019年3月28日結束。 這一版發行中修正的客戶相關問題，包括加強與新功能，總共有 1345 個。

[!DNL Adobe Experience Manager] 6.5自2019年4月8日起全面推出。

![AEM 6.5登入畫面](/help/assets/assets/aem65-login-v4.png)

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5是6.4程式碼基底 [!DNL Adobe Experience Manager] 的升級版本。此版本提供全新的增強功能、重要客戶修正、高優先順序的客戶增強功能，以及針對產品穩定化的一般錯誤修正。此外也包含最多SP4的[!DNL Adobe Experience Manager] 6.4 Service Pack版本。

以下清單提供概觀，而後續頁面則列出完整詳細資訊。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[AEM Foundation](/help/release-notes/wcm-platform.md)中的更改的完整清單。

[!DNL Adobe Experience Manager] 6.5平台以更新版本的OSGi型架構（Apache Sling和Apache Felix）和Java Content Repository為基礎而建置：阿帕奇·傑克拉布特奧克1.10.2。

快速入門使用Eclipse Jetty 9.4.15作為servlet引擎。

#### Java支援  {#java-support}

* Java 11的新支援，以及已支援的Java 8。
* 為獲得最佳效能，請用其他值覆蓋預設GC值。 有關詳細資訊，請參閱[install and update](/help/sites-deploying/custom-standalone-install.md)部分。
* Java 11和Java 8維護更新會由Adobe發佈，供AEM相關專案的客戶使用，但不可從Oracle公開取得。

#### Java開發 {#java-development}

* 現在有[兩個版本的Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)，一個帶有未標籤為要淘汰的公用介面的推薦版本，以及一個包含標籤為要淘汰的介面的版本。

#### 使用者介面 {#user-interface}

UI已經過多種增強功能，讓工作效率更高，使用更輕鬆。

* 新的使用者和群組權限管理UI。
* 欄檢視現在也只會載入畫面上可見的項目，且只會在使用者開始捲動時載入更多。 自6.0以來（在6.4中改善），清單和卡片檢視便已執行此動作。
* 欄檢視現在包含頁面/資產的工作流程狀態（若適用）。
* [全選](/help/sites-authoring/basic-handling.md#select-all)動作是快速執行同一資料夾中所有頁面/資產之動作的方式。
* [全選](/help/sites-authoring/basic-handling.md#select-all)動作會嘗試對所有頁面/資產執行動作，而不只是載入的內容。 如果動作未升級為處理大量動作，則會顯示警告對話方塊。

>[!CAUTION]
>
>Adobe不打算對傳統UI進行進一步的增強。 AEM 6.5已包含傳統UI，而從舊版升級的客戶可繼續依原樣使用。 請注意，舊版UI仍完全受支援。 [了解詳情](/help/sites-deploying/ui-recommendations.md)。

#### 搜尋和索引 {#indexing-and-search}

* 在Oak中搜尋現在支援動態Facet。 例如，資產搜尋中的篩選邊欄會顯示預估的結果量。
* QueryBuilder已擴充，以提供含有動態Facet的結果。

#### 升級 {#upgrade}

* 執行AEM 6.2、6.3和6.4的客戶支援直接就地升級至AEM 6.5。使用5.x或6.0/6.1的客戶若想使用就地升級，需先升級至6.4，然後升級至6.5，或透過將執行個體之間的內容直接傳輸至AEM 6.5來升級。

#### 專案和工作流程 {#projects-and-workflows}

* 6.4版中推出的新工作流程模型編輯器已經過改良，現在包含更多操作，例如複製和發佈、工作流程步驟中的變數支援，以及增強的OR和AND分割。

### [!DNL Experience Manager] 網站 {#experience-manager-sites}

[AEM Sites和Add-ons](/help/release-notes/sites.md)中變更的完整清單。

#### 托管單頁應用程式 {#managed-single-page-apps}

頁面編輯器新增了在用戶端轉譯體驗內內容編輯內容及撰寫/配置的功能(亦稱為[ SPA Editor](/help/sites-developing/spa-architecture.md))。 使用JavaScript架構建立的現有單頁應用程式React或Angular可透過AEM SJ SDK擴充，讓從業人員可編輯。

首次隨附於AEM 6.4 SP2，隨著AEM 6.5,SPA支援的功能如下：

* 使用「模板編輯器」編輯和配置AEM的可編輯部分
* 使用多網站管理來建立國家/地區、特許經營或白色標籤的SPA體驗

#### 無頭式內容管理 {#headless-content-management}

AEM能以各種格式和從堆疊的不同層級提供內容。 自2008年起，部分SlingGET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)和[POSTServlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)便已推出。 [AEM 6.3中導入了內容服務([Sling Model Exporter](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html))，且是AEM SJ SDK用來水合物化單頁應用程式的方法。 [Assets適用的HTTP API](/help/assets/mac-api-assets.md)是CRUD API，已針對AEM 6.5擴充。

新HTTP API功能：

* 新增[內容片段支援至Assets的HTTP API](/help/assets/assets-api-content-fragments.md)以建立、更新、讀取和刪除片段。
* 透過內容服務公開內容片段清單，內容片段清單核心元件](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html)。[
* [顯示每](https://opensource.adobe.com/aem-core-wcm-components/library.html) 個元件之預設內容服務JSON輸出的核心元件庫

#### Screens附加元件 {#screens-add-on}

在從互動式資訊站到數位看板的所有數位顯示器上，有效率地設計、提供和最佳化體驗。

**設計**

* 透過改善的內容重複使用，在數位和店內統一體驗和內容
* 透過對Launch的支援，簡化製作和核准/發佈工作流程
* 使用SPA Editor編輯和提供豐富互動式體驗

**傳遞**

* 擴充的媒體播放器支援，提供強大的線上和離線操作（智慧同步），可擴展至甚至最大的看板網路。

**最佳化**

* 使用動態預留位置，依資料觸發內容的位置或設定進行個人化。
* Adobe Analytics與AEM Screens Player整合所推動的統一分析

如需AEM Screens變更的詳細資訊 — 請參閱[AEM Screens使用手冊](https://docs.adobe.com/content/help/zh-Hant/experience-manager-screens/user-guide/aem-screens-introduction.html)中的發行說明。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

[AEM 6.5 Assets發行說明](/help/release-notes/assets.md)中的變更完整清單。

AEM 6.5導入了下列功能和增強功能，以提升AEM使用者、DAM角色以及相關創意和行銷角色的生產力。

#### 與Adobe Creative Cloud整合 {#integration-with-adobe-creative-cloud}

推出[Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)，這是適用於在Adobe Creative Cloud應用程式(包括Photoshop、Illustrator和InDesign)中工作的創意使用者的應用程式內體驗，可簡化創意人員與行銷人員在內容建立程式中的協作。 AEM案頭應用程式持續支援使用者在案頭上使用AEM資產（使用任何檔案類型和任何案頭應用程式）的需求。

此外，AEM與Adobe Stock整合，可協助直接從AEM Web UI尋找、預覽、授權和儲存Adobe Stock資產。

![Photoshop中的Asset Link面板](/help/assets/assets/aem65-assetlink-photoshop.png)

#### 連線資產 {#connected-assets}

「連線資產」功能可針對大型部署使用許多AEM Sites部署，而這些部署需要運用中央AEM Assets DAM部署的資產。 它可改善集中管理資產的控管，同時為各種Sites部署提供高效率的資產。

### Dynamic Media {#dynamic-media}

Dynamic Media在AEM Assets中提供增強的多媒體製作和傳遞功能，提供身臨其境且個人化的尖端體驗。 透過單一高品質主資產，您可以善用我們進階的雲端轉譯、智慧型裁切和同級最佳的檢視器，以業界領先的效能提供最吸引人的體驗。

新功能包括：

* 支援360視訊和VR耳機
* 自訂影片縮圖
* 增強的協助工具支援
* 熱連結保護

#### 使用者體驗與搜尋 {#user-experience-and-search}

重要的增強功能可提供動態搜尋刻面，協助您更快找到合適的資產，並能從任何資料夾或搜尋結果中選取所有資產，以更有效率地管理多個資產。

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms提供數項新功能和增強功能。 重點包括：

* 跟蹤提交的表單、已處理文檔和已呈現文檔數的事務處理報告
* 互動式通訊的可用性改善
* 最適化表單中的雲端數位簽名
* 在AEM Sites單頁應用程式(SPA)中內嵌最適化表單和互動式通訊。
* 支援AEM工作流程中的變數
* 交互通信中的資料顯示模式支援
* 排序最適化表單和互動式通訊表格
* 表單資料模型中輸入資料的自動驗證

如需新功能和改善功能及檔案資源的相關資訊，請參閱AEM 6.5 Forms的[新功能和增強功能摘要](/help/forms/using/whats-new.md)。

### [!DNL Experience Manager Communities] {#communitiesreleasenotes}

AEM 6.5為Communities新增功能和增強功能。 此版本的重點為：

* 編寫使用者產生的內容時支援已註冊的成員標籤(@mention)。
* 現在支援將大量訊息直接傳送至成員群組。
* 在大量協調UI中開發並新增自訂篩選器。 說明依標籤篩選的[範例專案](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)可作為開發類似自訂篩選器的基礎。
* 新增「清單檢視」，並改善「大量協調」的UI。
* 可以為不同的社群網站和巢狀群組指派不同的管理員，而非單一社群管理員。
* AEM 6.5 Communities的啟用功能支援[(SCORM)2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/)引擎。
* 啟用元件的鍵盤導覽支援可改善協助工具。
* 設定MSRP和DSRP時支援Apache Solr 7.0。

如需變更的詳細清單，請參閱[AEM 6.5 Communities發行說明](/help/release-notes/communities-release-notes.md)。

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

您可以將Livefyre與AEM 6.5執行個體整合。 請參閱[如何整合Livefyre與AEM](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html)。

### 利用以客戶為中心的開發 {#leverage-customer-focused-development}

Adobe使用以客戶為中心的開發模型，允許客戶在規格、開發和測試期間為開發流程的所有階段作出貢獻。 在此過程中，我們感謝所有貢獻客戶和合作夥伴。

Adobe已制定程式和程式，以收集、排定優先順序及追蹤以客戶為重點的錯誤解決方法和增強功能要求開發。 [Experience Manager支援門戶](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support)與Adobe增強和缺陷跟蹤系統整合。 客戶問題會盡可能由客戶支援團隊識別和解決。 呈報至研發時，會擷取所有客戶資訊，並用於優先順序和報告用途。 在開發中，優先考慮付費支援、保證問題和客戶付費的增強功能。

此優先順序排列程式已產生750多項以客戶為重點的變更，已在AEM 6.5中修正。

## 屬於此版本的檔案清單 {#list-of-files-that-are-part-of-the-release}

**Foundation**

* 獨立快速入門：`cq-quickstart-6.5.0.jar`。
* 應用程式伺服器快速入門：`cq-quickstart-6.5.0.war`。
* Dispatcher 4.3.2或更新版本，適用於各種Web伺服器和平台。 請參閱[下載連結](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Eclipse IDE的外掛程式（[了解詳情並下載](/help/sites-developing/aem-eclipse.md)）

* 方括弧程式碼編輯器的擴充功能（[了解詳情並下載](/help/sites-developing/aem-brackets.md)）
* Maven/Gradle相依性（[下載連結](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/)）

**網站**

* 核心元件（[GitHub專案](https://github.com/adobe/aem-core-wcm-components)）
* We.Retail參考實作（[了解詳情](/help/sites-developing/we-retail.md)）
* Maven專案原型：

   * 對於完整堆棧站點：[GitHub專案](https://github.com/adobe/aem-project-archetype)
   * 針對具有React/Angular的單頁應用程式：[GitHub專案](https://github.com/adobe/aem-spa-project-archetype)

* AEM Screens播放器([download](https://download.macromedia.com/screens/))

* 智慧內容語言模型。 已預先安裝英文 — 可下載更多語言

   * [德文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [義大利文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM最新化工具套裝，例如對話方塊轉換工具。 （[GitHub專案](https://github.com/adobe/aem-modernize-tools)）

**資產**

* 新增增強PDF模擬轉譯器的套件（[了解詳情](/help/assets/aem-pdf-rasterizer.md)）
* 添加擴展RAW影像支援的包（[了解詳情](/help/assets/camera-raw.md)）

**Forms**

* [AEM Forms功能的套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Forms OSGi用戶端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 語言 {#languages}

使用者介面提供下列語言：

* 英文
* 德文
* 法文
* 西班牙文
* 義大利文
* 巴西葡萄牙文
* 日文
* 簡體中文
* 繁體中文（有限支援）
* 韓文

[!DNL Experience Manager] 6.5已通過GB18030-2005 CITS認證，可使用中文編碼標準。

## 安裝和更新 {#install-update}

有關安裝要求，請參閱[安裝說明](/help/sites-deploying/custom-standalone-install.md)。

有關詳細說明，請參閱[升級文檔](/help/sites-deploying/upgrade.md)。

## 支援平台 {#supported-platforms}

找到支援平台的完整清單，包括[AEM 6.5技術要求](/help/sites-deploying/technical-requirements.md)上的支援級別。

>[!NOTE]
>
>Oracle已移至OracleJava SE產品的長期支援(LTS)模型。 Java 9和10是依Oracle分類的非LTS版本。 請參閱[OracleJava SE支援路線圖](https://www.oracle.com/technetwork/java/eol-135779.html)。 Adobe支援LTS版的Java，僅在生產環境中執行AEM。 Java 11是搭配AEM 6.5使用的建議版本。

## 過時和移除的功能 {#deprecated-and-removed-features}

Adobe不斷評估產品中的功能，並隨著時間的推移計畫用更強大的版本替換功能，或者決定重新實施選定的部件，以便更好地為將來的期望或擴展做好準備。

對於[!DNL Adobe Experience Manager] 6.5, [請閱讀已棄用和已移除功能的清單](/help/release-notes/deprecated-removed-features.md)。 此頁面也包含近期變更的預先公告，以及客戶從舊版更新的重要通知。

## 已知問題 {#known-issues}

[已知問題清單](/help/release-notes/known-issues.md)

### 產品下載與支援（受限網站） {#product-download-and-support-restricted-sites}

以下網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [請前往licensing.adobe.com下載產品](https://licensing.adobe.com/)。

* [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上其他功能的產品更新、修補程式和套件。

* [透過Admin Console提供客戶支援](https://adminconsole.adobe.com/)。如需詳細資訊，請參閱[新Adobe客戶支援體驗](https://docs.adobe.com/content/help/en/customer-one/using/home.html)。
