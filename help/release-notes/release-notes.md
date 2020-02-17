---
title: Adobe Experience Manager 6.5的一般發行說明
description: Adobe Experience Manager 6.5說明，其中概述發行資訊、新增功能、安裝方式和詳細的變更清單。
uuid: b916624e-9486-4391-8c6f-cb4045e78490
contentOwner: chuesler
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 7d3ceccb-4f00-4e11-9c9f-6de46a455e02
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# Adobe Experience Manager 6.5的一般發行說明{#general-release-notes-for-adobe-experience-manager}

## 發行資訊 {#release-information}

<table>
 <tbody>
  <tr>
   <th>產品</th>
   <td>Adobe Experience Manager<br /> </td>
  </tr>
  <tr>
   <th>版本</th>
   <td>6.5</td>
  </tr>
  <tr>
   <th>類型</th>
   <td>主要版本</td>
  </tr>
  <tr>
   <th>正式上市日期</th>
   <td>2019年4月8日<br /> </td>
  </tr>
  <tr>
   <th>建議的更新</th>
   <td>請參閱 <a href="https://helpx.adobe.com/experience-manager/aem-releases-updates.html">AEM發行和更新</a></td>
  </tr>
 </tbody>
</table>

### Trivia {#trivia}

此版Adobe Experience manager的發行週期從2018年4月4日開始，經過23次反複的品質保證與錯誤修正，並於2019年3月28日結束。 這一版發行中修正的客戶相關問題，包括加強與新功能，總共有 1345 個。

Adobe Experience Manager 6.5自2019年4月8日起正式推出。

![AEM 6.5登入畫面](/help/assets/assets/aem65-login-v4.png)

## 新功能 {#what-s-new}

Adobe Experience Manager 6.5是Adobe Experience Manager 6.4程式碼庫的升級版本。 它提供全新和增強的功能、關鍵客戶修正、高優先順序的客戶增強功能，以及針對產品穩定化的一般錯誤修正。 此外，還包含最多SP4的Adobe Experience Manager 6.4 Service Pack版本。

下列清單提供概觀——而後續頁面則列出完整的詳細資訊。

### Experience Manager Foundation {#experience-manager-foundation}

[AEM Foundation變更的完整清單](/help/release-notes/wcm-platform.md)。

Adobe Experience Manager 6.5平台以OSGi架構（Apache Sling和Apache Felix）的更新版本和Java Content Repository為基礎：Apache Jackrabbit Oak 1.10.2.

快速入門使用Eclipse Jetty 9.4.15做為servlet引擎。

#### Java支援 {#java-support}

* Java 11的新支援，以及已支援的Java 8
* 為獲得最佳效能，請用其他值覆蓋預設GC值。 如需詳細資訊，請參閱「安 [裝與更新](/help/sites-deploying/custom-standalone-install.md) 」一節。
* Java 11和Java 8維護更新將由Adobe分發，以便客戶在AEM相關專案中使用，但Oracle未公開提供

#### Java開發 {#java-development}

* 現在有兩 [個版本的Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)，一個建議版本，其中包含未標籤為取代的公用介面，以及一個包含已標籤為取代的介面。

#### 使用者介面{#user-interface}

UI已做了各種增強功能，讓它更有生產力，也更容易使用。

* 使用者和群組的新權限管理UI
* 欄檢視現在也只會載入螢幕上可見的項目，而且只會在使用者開始捲動時載入更多項目。 清單和卡片檢視自6.0起就已執行此動作（在6.4中改良）
* 欄檢視現在包含頁面／資產的工作流程狀態（如果適用）
* 「全 [選](/help/sites-authoring/basic-handling.md#select-all) 」動作是快速執行動作的方式，可將所有頁面／資產置於同一資料夾中
* 「全 [選](/help/sites-authoring/basic-handling.md#select-all) 」動作會嘗試對所有頁面／資產執行動作，而不只是載入的內容。 如果動作尚未升級為處理大量動作，則會顯示警告對話方塊

>[!CAUTION]
>
>Adobe不打算對Classic UI做進一步的增強。 AEM 6.5包含Classic UI，而從舊版升級的客戶可依現狀繼續使用。 請注意，Classic UI在遭淘汰時仍完全受支援。 [閱讀更多資訊](/help/sites-deploying/ui-recommendations.md)。

#### 搜尋與索引 {#search-indexing}

* 在Oak中搜尋現在支援動態Facet。 例如，資產搜尋中的篩選邊欄會顯示估計的結果量。
* QueryBuilder已擴充，可提供動態刻面結果

#### 升級 {#upgrade}

* 執行AEM 6.2、6.3和6.4的客戶支援直接就地升級至AEM 6.5。使用5.x或6.0/6.1的客戶若想使用就地升級，則需先升級至6.4 —— 然後升級至6.5，或透過在執行個體之間傳輸內容直接升級至AEM 6.5。

#### 專案和工作流程 {#projects-and-workflows}

* 6.4版中引進的全新工作流程模型編輯器已經過改良，加入更多作業，例如複製和發佈、工作流程步驟中的變數支援，以及增強的OR和AND分割。

### Experience Manager Sites {#experience-manager-sites}

[AEM Sites和Add-ons中變更的完整清單](/help/release-notes/sites.md)。

#### 受管理的單頁應用程式 {#managed-single-page-apps}

頁面編輯器新增了在用戶端轉譯體驗（亦稱為SPA編輯器）中內容內容編輯及合成／版面 [的功能](/help/sites-developing/spa-architecture.md)。 使用JavaScript架構建立的現有單頁應用程式可使用AEM SJ SDK擴充，讓從業人員可編輯。

AEM 6.4 SP2首次隨附於AEM 6.5,SPA支援可享有下列功能：

* 使用範本編輯器來編輯和設定SPA的AEM可編輯部分
* 使用多網站管理來建立國家、特許經營或白標籤的SPA體驗

#### 無頭內容管理 {#headless-content-management}

AEM能夠以各種格式和堆疊的不同層級來提供內容。 有些自2008年起就使用 [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 和 [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)。 Content Services([Sling Model Exporter](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html))已推出於AEM 6.3，是AEM SJ SDK用來為單頁應用程式加水的方法。 Assets [的HTTP API](/help/assets/mac-api-assets.md) 是CRUD API，已針對AEM 6.5擴充。

新的HTTP API功能：

* 新增 [內容片段支援至HTTP API](/help/assets/assets-api-content-fragments.md) ，以建立、更新、讀取和刪除片段。
* 透過內容服務公開內容片段清單核 [心元件的內容片段清單](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html)。
* [核心元件庫](https://opensource.adobe.com/aem-core-wcm-components/library.html) ，顯示每個元件的預設Content Services JSON輸出

#### 畫面附加元件 {#screens-add-on}

在從互動式資訊站到數位招牌的所有數位展示上，有效率地設計、提供和最佳化體驗。

**設計**

* 透過改善的內容重複使用功能，將體驗和內容統一在數位和店內
* 簡化製作和核准／發佈工作流程，並支援啟動
* 使用SPA編輯器編輯和提供豐富的互動式體驗

**提供**

* 擴充的媒體播放器支援，提供強穩的線上和離線作業(Smart Sync)，可擴充至最大的標牌網路。

**最佳化**

* 使用動態預留位置，依資料觸發內容的位置或設定個人化。
* 由Adobe Analytics與AEM Screens player整合所推動的統一見解

如需AEM畫面變更的詳細資訊——請參閱 [AEM畫面使用指南中的發行說明](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)。

### Experience Manager Assets {#experience-manager-assets}

[AEM 6.5 Assets版本注意事項的完整變更清單](/help/release-notes/assets.md)。

AEM 6.5提供下列功能和增強功能，可大幅提升AEM使用者、DAM角色和相關的創意和行銷角色的生產力。

#### 與Adobe Creative cloud整合 {#integration-with-adobe-creative-cloud}

Adobe Asset Link [](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)是Adobe Creative cloud應用程式（包括Photoshop、Illustrator和InDesign）中的創意使用者在應用程式中的體驗，它可簡化創意人員與行銷人員在內容建立程式中的協作。 AEM案頭應用程式持續支援使用者使用AEM在案頭上的資產、使用任何檔案類型和任何案頭應用程式的需求。

此外，AEM與Adobe Stock整合，可協助直接從AEM Web UI尋找、預覽、授權及儲存Adobe Stock資產。

![Photoshop中的「資產連結」面板](/help/assets/assets/aem65-assetlink-photoshop.png)

#### 連線資產 {#connected-assets}

Connected Assets功能針對較大型的部署，提供許多AEM Sites部署，需要運用中央AEM Assets DAM部署的資產。 它可改善集中管理資產的治理，同時讓資產能夠高效率地供應至各種網站部署。

### 動態媒體 {#dynamic-media}

Dynamic media在AEM Assets中提供增強的豐富型媒體製作和發佈功能，以推動身歷其境且個人化的尖端體驗。 透過單一高品質的主資產，您可以利用我們的進階雲端演算、Smart Crop和同級最佳檢視器，以領先業界的效能提供最引人入勝的體驗。

新功能包括：

* 支援360視訊和VR耳機
* 自訂視訊縮圖
* 增強的協助工具支援
* 熱連結保護

#### 使用者體驗與搜尋 {#user-experience-and-search}

主要增強功能可提供動態搜尋Facet，協助您更快找到正確的資產，並提供從任何資料夾或搜尋結果選取所有資產的功能，以更有效率地管理多個資產。

### Adobe Experience Manager Forms {#experience-manager-forms}

AEM 6.5 Forms提供多項新功能和增強功能。 重點包括：

* 事務處理報表，用於跟蹤提交的表單數、已處理的文檔數和已呈現的文檔數
* 互動式通訊的可用性改進
* 以雲端為基礎的數位簽名，以最適化表單呈現
* 在AEM Sites單頁應用程式(SPA)中內嵌最適化表單和互動式通訊。
* 支援AEM工作流程中的變數
* 互動式通信中的資料顯示模式支援
* 排序最適化表單和互動式通訊表
* 表單資料模型中輸入資料的自動驗證

請參閱 [AEM 6.5 Forms中新功能和增強功能的摘要](/help/forms/using/whats-new.md) ，以取得新功能和增強功能與檔案資源的相關資訊。

### Experience Manager Communities {#communitiesreleasenotes}

AEM 6.5新增功能和增強功能至社群。 此版本的亮點為：

* 編寫使用者產生的內容時，支援已註冊的成員標籤（@提及）。
* 現在支援將大量訊息直接傳送給成員群組。
* 在大量協調UI中開發並新增自訂篩選。 示範 [依標籤篩選的範例專案](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) ，可做為開發類似自訂篩選的基礎。
* 「大量協調」中的UI已改善，提供「新清單檢視」。
* 可以為不同的社群網站和巢狀群組指派不同的管理員，而不是單一社群管理員。
* AEM 6.5 Communities的啟用功能支 [援(SCORM)2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。
* 啟用元件上的鍵盤導覽支援可改善協助工具。
* 設定MSRP和DSRP時支援Apache Solr 7.0。

如需詳細的變更清單，請參 [閱「AEM 6.5社群版本注意事項」](/help/release-notes/communities-release-notes.md)。

### Experience Manager Livefyre {#experience-manager-livefyre}

您可以將Livefyre與AEM 6.5執行個體整合。 有關如何將Livefyre與AEM整合的資訊，請參閱：

* [整合Livefyre](https://helpx.adobe.com/experience-manager/6-4/help/sites-administering/livefyre.html)

### 運用以客戶為中心的開發 {#leverage-customer-focused-development}

Adobe採用以客戶為中心的開發模型，讓客戶在規格、開發和測試期間，對開發流程的所有階段都有貢獻。 在此過程中，我們感謝所有有貢獻的客戶和合作夥伴。

Adobe已制定相關程式和程式，以收集、排定優先順序並追蹤以客戶為中心的錯誤解決方案和增強功能要求開發。 Adobe [Marketing cloud支援入口網站](https://helpx.adobe.com/marketing-cloud/contact-support.html) ，已與Adobe增強與缺陷追蹤系統整合。 客戶問題會盡可能與客戶服務確認並解決。 呈報至研發時，會擷取所有客戶資訊，並用於優先排序和報告用途。 在開發時，優先考慮付費支援和擔保問題以及付費客戶增強功能。

此優先順序排列程式已在AEM 6.5中修正超過750項以客戶為主的變更。

## 屬於「版本」的檔案清單 {#list-of-files-that-are-part-of-the-release}

**基礎**

* 獨立快速入門：cq-quickstart-6.5.0.jar
* 應用程式伺服器快速啟動：cq-quickstart-6.5.0.war
* Dispatcher 4.3.2或更新版本，適用於各種Web伺服器和平台(下[載連結](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html))
* Eclipse IDE增效模組(詳[細內容及下載](/help/sites-developing/aem-eclipse.md))

* Brackets程式碼編輯器的擴充功能([閱讀更多資訊並下載](/help/sites-developing/aem-brackets.md))
* Maven/Gradle相依性(下[載連結](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/aem/uber-jar/6.5.0/))

**網站**

* 核心元件([GitHub專案](https://github.com/adobe/aem-core-wcm-components))
* We.Retail Reference實作(詳[細資訊](/help/sites-developing/we-retail.md))
* Maven Project Archetypes:

   * 對於完整堆棧站點： [GitHub專案](https://github.com/adobe/aem-project-archetype)
   * 針對具有React/Angular的單頁應用程式： [GitHub專案](https://github.com/adobe/aem-spa-project-archetype)

* 適用於各種目標平台的AEM Screens Players([下載](https://download.macromedia.com/screens/))

* 智慧型內容語言模型。 已預先安裝英文——可下載更多語言

   * [德文](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙文](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [義大利文](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法文](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM最新化工具套裝，例如對話轉換工具。 ([GitHub專案](https://github.com/adobe/aem-modernize-tools))

**資產**

* 封裝以新增增強的PDF點陣化器([閱讀詳細資訊](/help/assets/aem-pdf-rasterizer.md))
* 封裝以新增擴充的RAW影像支援(詳[細資訊](/help/assets/camera-raw.md))

**表單**

* [AEM Forms功能的套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)
* [AEM Forms OSGi Client SDK](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/6.0.80/)

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

Experience Manager 6.5已通過GB18030-2005 CITS認證，可使用中文編碼標準。

## 安裝與更新 {#install-update}

請參 [閱安裝指示](/help/sites-deploying/custom-standalone-install.md) ，瞭解安裝需求。

請參閱升 [級檔案](/help/sites-deploying/upgrade.md) ，以取得詳細指示。

## 支援的平台 {#supported-platforms}

請尋找完整的支援平台矩陣，包括[AEM 6.5技術需求的支援層級](/help/sites-deploying/technical-requirements.md)

Oak microKernel forOak microKernel for

>[!NOTE]
>
>Oracle已改為Oracle Java SE產品的「長期支援」(LTS)模型。 Java 9和10是Oracle發行的非LTS版本(請參 [閱Oracle Java SE支援路線圖](https://www.oracle.com/technetwork/java/eol-135779.html))。 Adobe僅提供LTS版Java的支援，以在生產中執行AEM。 因此，建議使用Java 11與AEM 6.5搭配使用。

## 已過時和已移除的功能 {#deprecated-and-removed-features}

Adobe會持續評估產品中的功能，並隨著時間推移，計畫以功能更強大的版本來取代功能，或決定重新建置選取的部件，以便為未來的期望或擴充做好更好的準備。

若是Adobe Experience Manager 6.5，請閱 [讀已過時和已移除的功能清單](/help/release-notes/deprecated-removed-features.md)。 本頁還包含對近期變更的預先公告，以及客戶從舊版更新的重要通知。

## 已知問題 {#known-issues}

[已知問題清單](/help/release-notes/known-issues.md)

### 產品下載與支援（受限制的網站） {#product-download-and-support-restricted-sites}

這些網站僅提供給客戶使用。 如果您是客戶，需要存取權，請聯絡您的Adobe客戶經理。

* [](https://daycare.day.com) 產 [品下載，請造訪licensing.adobe.com](https://licensing.adobe.com/)

* [daycare.day.com的客戶支援](https://daycare.day.com)

