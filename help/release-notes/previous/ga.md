---
title: 的一般發行說明 [!DNL Adobe Experience Manager] 6.5
description: '[!DNL Adobe Experience Manager] 6.5說明，概述發行資訊、新增功能、安裝方式，以及詳細的變更清單。'
source-git-commit: 9b15215a68495a800e94a58b523e1b7baa0c0203
workflow-type: tm+mt
source-wordcount: '4696'
ht-degree: 4%

---

# 的一般發行說明 [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 |
| 類型 | 主要版本 |
| 正式發行日期 | 2019 年 4 月 8 日 |
| 建議的更新 | 請參閱 [AEM近期更新](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html). |

### Trivia {#trivia}

此版本的 [!DNL Adobe Experience Manager] 從2018年4月4日開始，經過23次反覆品質保證和錯誤修正，並於2019年3月28日結束。 這一版發行中修正的客戶相關問題，包括加強與新功能，總共有 1345 個。

[!DNL Adobe Experience Manager] 6.5自2019年4月8日起全面推出。

![AEM 6.5登入畫面](/help/assets/assets/aem65-login-v4.png)

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5是 [!DNL Adobe Experience Manager] 6.4代碼庫。 此版本提供全新的增強功能、重要客戶修正、高優先順序的客戶增強功能，以及針對產品穩定化的一般錯誤修正。也包含 [!DNL Adobe Experience Manager] 6.4 Service Pack最多發行SP4。

以下清單提供概觀，而後續頁面則列出完整詳細資訊。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

平台 [!DNL Adobe Experience Manager] 6.5以更新版本的OSGi型架構（Apache Sling和Apache Felix）和Java Content Repository為基礎而建置：阿帕奇·傑克拉布特奧克1.10.2。

快速入門使用Eclipse Jetty 9.4.15作為servlet引擎。

#### Java支援  {#java-support}

* Java 11的新支援，以及已支援的Java 8。
* 為獲得最佳效能，請用其他值覆蓋預設GC值。 如需詳細資訊，請參閱 [安裝和更新](/help/sites-deploying/custom-standalone-install.md) 區段。
* Java 11和Java 8維護更新會由Adobe發佈，供AEM相關專案的客戶使用，但不可公開透過Oracle取得。

#### Java開發 {#java-development}

* 現在有 [Uberjar的兩個版本](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)，此版本建議使用未標示為淘汰的公用介面，以及包含標示為淘汰的介面的版本。

#### 使用者介面 {#user-interface}

UI已經過多種增強功能，讓工作效率更高，使用更輕鬆。

* 新的使用者和群組權限管理UI。
* 欄檢視現在也只會載入畫面上可見的項目，且只會在使用者開始捲動時載入更多。 自6.0以來（在6.4中改善），清單和卡片檢視便已執行此動作。
* 欄檢視現在包含頁面/資產的工作流程狀態（若適用）。
* 此 [全選](/help/sites-authoring/basic-handling.md#select-all) 動作是對相同資料夾中的所有頁面/資產執行動作的快速方式。
* 此 [全選](/help/sites-authoring/basic-handling.md#select-all) 動作會嘗試對所有頁面/資產執行動作，而不只是載入的內容。 如果動作未升級為處理大量動作，則會顯示警告對話方塊。

>[!CAUTION]
>
>Adobe不打算對傳統UI進行進一步的增強。 AEM 6.5已包含傳統UI，而從舊版升級的客戶可繼續依原樣使用。 請注意，舊版UI仍完全受支援。 [了解詳情](/help/sites-deploying/ui-recommendations.md).

#### 搜尋和索引 {#indexing-and-search}

* 在Oak中搜尋現在支援動態Facet。 例如，資產搜尋中的篩選邊欄會顯示預估的結果量。
* QueryBuilder已擴充，以提供含有動態Facet的結果。

#### 升級 {#upgrade}

* 執行AEM 6.2、6.3和6.4的客戶支援直接就地升級至AEM 6.5。使用5.x或6.0/6.1的客戶若想使用就地升級，需先升級至6.4，然後升級至6.5，或透過將執行個體之間的內容直接傳輸至AEM 6.5來升級。
* 6.5中的升級程式基本相同。
* 我們繼續支援6.4中推出的「向後相容性」、「升級複雜性評估」和「可持續升級」功能。根據需要對這些領域進行了版本特定的更新。
* 模式偵測器封裝已簡化，且將有一個套件評估可用來源版本的6.5升級。
* 如需升級程式的詳細資訊，請參閱 [升級檔案](/help/sites-deploying/upgrade.md).

#### 專案和工作流程 {#projects-and-workflows}

* 6.4版推出的全新工作流程模型編輯器經過改良，加入更多操作，例如複製和發佈、工作流程步驟中的變數支援，以及增強功能 `OR` 和 `AND` 分割。

#### 存放庫 {#repository}

* Adobe Experience Manager 6.5的基礎以更新版本的OSGi型架構（Apache Sling和Apache Felix）和Java Content Repository為基礎而構建：阿帕奇·傑克拉布特奧克1.10.2。
* 如需已修正問題的概觀，請參閱 [阿帕奇·傑克拉布特·奧克·吉拉訴1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [阿帕奇·傑克拉布特·奧克·吉拉訴1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 和 [阿帕奇·傑克拉布特·奧克·吉拉訴1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>自AEM 6.3以來出現的新版Oak Segment Tar需要移轉存放庫。 如果您從舊版TarMK升級，或想從其他類型的永續性切換新的區段Tar，此步驟為必要步驟。 如需新區段Tar的優點的詳細資訊，請參閱 [移轉至Oak Segment Tar常見問題集](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* 新增OSGi Promises和Converter公用程式程式庫。

#### 安全性 {#security}

* 新增管理員使用者的密碼過期。

#### Web伺服器 {#web-server}

* 快速入門發佈使用Eclipse Jetty 9.4.15作為servlet引擎(AEM 6.4隨9.3.22提供)。

### [!DNL Experience Manager] 網站 {#experience-manager-sites}

#### 托管單頁應用程式 {#managed-single-page-apps}

頁面編輯器新增了在用戶端轉譯體驗（亦已知）中內容內編輯內容及撰寫/配置的功能 [作為SPA編輯器](/help/sites-developing/spa-architecture.md))。 使用JavaScript架構建立的現有單頁應用程式React或Angular可透過AEM SJ SDK擴充，讓從業人員可編輯。

首次隨附於AEM 6.4 SP2，隨著AEM 6.5,SPA支援的功能如下：

* 使用「模板編輯器」編輯和配置AEM的可編輯部分
* 使用多網站管理來建立國家/地區、特許經營或白色標籤的SPA體驗

#### 無頭式內容管理 {#headless-content-management}

AEM能以各種格式和從堆疊的不同層級提供內容。 自2008年以來，有些公司一直使用 [SlingGET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 和 [POSTServlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). 內容服務([Sling模型導出器](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html))於AEM 6.3中推出，且為AEM SJ SDK用來水合物法單頁應用程式。 此 [適用於資產的HTTP API](/help/assets/mac-api-assets.md) 是已針對AEM 6.5擴充的CRUD API。

新HTTP API功能：

* 新增 [支援HTTP API for Assets的內容片段](/help/assets/assets-api-content-fragments.md) 建立、更新、讀取和刪除片段。
* 透過Content Services與 [內容片段清單核心元件](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [核心元件程式庫](https://opensource.adobe.com/aem-core-wcm-components/library.html) 顯示每個元件的預設「內容服務」JSON輸出

#### Screens附加元件 {#screens-add-on}

在從互動式資訊站到數位看板的所有數位顯示器上，有效率地設計、提供和最佳化體驗。

* 透過改善的內容重複使用，在數位和店內統一體驗和內容
* 透過對Launch的支援，簡化製作和核准/發佈工作流程
* 使用SPA Editor編輯和提供豐富互動式體驗
* 使用啟動來規劃看板內容的未來內容變更
* 序列通道中的計量播放
* 使用源檔案（如Excel工作表）自動建立項目結構
* 擴充的媒體播放器支援，提供強大的線上和離線操作（智慧同步），可擴展至甚至最大的看板網路。
* 使用動態預留位置，依資料觸發內容的位置或設定進行個人化。
* Adobe Analytics與AEM Screens Player整合所推動的統一分析

如需AEM Screens變更的詳細資訊 — 請參閱 [AEM Screens使用手冊](https://docs.adobe.com/content/help/zh-Hant/experience-manager-screens/user-guide/aem-screens-introduction.html).

#### 元件和範本開發 {#component-amp-template-development}

* 如需新專案的Maven專案原型18+，請參閱 [Github以取得發行說明](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* 如需新專案的單頁應用程式Maven專案原型1.0.6+，請參閱 [Github以取得發行說明](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL 1.4版，請參閱 [Github以取得發行說明](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * 字串、陣列和對象的「in」運算子：

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * 具有data-sly-set的變數宣告：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 清單和重複控制參數：開始、步驟、結束：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap的識別碼：

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 支援負數

* 核心元件2.3.2+，請參閱 [Github以取得發行說明](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases).
* 佈局容器的網格系統，請參閱 [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib管理器：將Google關閉編譯器預設為縮制JavaScript clientlibs（舊預設為Yahoo UI），並將Google關閉編譯器更新為v20190121版
* 範本編輯器和原則

   * 為使用JS SDK的單頁應用程式建立和編輯範本(又稱為SPA編輯器)

* 參考網站We.Retail 4.0，請參閱 [Github以取得發行說明](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* 若要升級現有網站以運用最新編輯器功能，請參閱 [Github存放庫](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM包含jQuery程式庫1.12.4版，可提供與現有自訂程式碼的最大相容性。 Adobe已修改以解決已知的安全問題。

#### 網站管理 {#site-administration}

* 此 [參考](/help/sites-authoring/author-environment-tools.md#references) 邊欄有一個新區段，可列出指向所選頁面的內部連結。 當計畫將頁面離線或刪除時，此功能相當實用，可讓您查看哪些頁面需要在離線前加以調整。
* 此 [清單檢視](/help/sites-authoring/basic-handling.md#list-view) 有一個新的工作流程欄，會顯示頁面目前處於工作流程中的狀態。
* 在 [頁面屬性](/help/sites-authoring/editing-page-properties.md)，現在可以在將縮圖指派給頁面時瀏覽現有資產（縮圖索引標籤）。

#### 頁面編輯器 {#page-editor}

* 允許使用運用JS SDK的React和Angular用戶端元件(也稱為SPA編輯器)來建立單頁應用程式體驗，並進行內容內編輯和組合
* 只有在頁面已設定支架頁面時，才會顯示支架模式。

#### 內容片段與編輯器 {#content-fragments-amp-editor}

* 新增 [註解](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) 內容片段編輯器中的邊欄，以產生一般注釋並查看文字中的注釋（也顯示在時間軸邊欄中）
* 可在 [內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 簡單文字、RTF或標籤下拉式清單
* 新增 [註解/註解](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) 在RTE中選取文字（全螢幕檢視）
* [比較版本](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) 透過參考邊欄並排顯示內容片段
* 「資產下載報表」現在會據以顯示內容片段
* 新增 [資產HTTP API的內容片段支援](/help/assets/assets-api-content-fragments.md) 通過/api.json。 有可建立、更新、讀取和刪除內容片段的API。

#### 體驗片段 {#experience-fragments}

* 改進 [體驗片段](/help/sites-authoring/experience-fragments.md)，則會在搜尋其使用中的頁面時找到其內容
* 此 [匯出至Target](/help/sites-administering/experience-fragments-target.md) 選項現在允許以JSON傳送體驗片段(預設為HTML)，或兩者皆有

#### 轉換 {#translation}

* 使用專案主版簡化建立翻譯專案
* 預設情況下，將翻譯作業設定為批准狀態，簡化翻譯項目的執行
* 允許使用第三方翻譯記憶庫中的更改更新翻譯的頁面
* 允許以JSON格式匯出翻譯工作
* 更新Microsoft翻譯整合以使用V3 API

#### 多站點管理(MSM) {#multi-site-management-msm}

* 針對使用PushOnModify的轉出設定，請更妥善處理頁面移動操作，以避免狀態不一致
* 依預設，現在會在Live Copy結構內建立新頁面時，會建立獨立頁面
* 在使用JS SDK的單頁應用程式中使用MSM功能(又稱為SPA Editor)

#### 啟動 {#launches}

* 啟動的新審核和核准工作流程，以及僅可提升已核准啟動頁面的功能
* 新增 [選項，以選擇在促銷步驟後立即刪除Launch](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### 內容鎖定與模擬 {#content-targeting-simulation}

* ContextHub資料層和用戶端規則引擎JavaScript已更新，依預設會使用jQuery 3。

#### AEM和Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>目前：
>
>* 僅 `at.js 1.x` 如果您在AEM Activities Console中使用Adobe Target作為目標引擎，則支援此功能。
>
>* 兩者 `at.js. 1.x` 和 `at.js 2.x` 如果您使用體驗片段匯出至Target，以及在Target的主控台內執行活動，則支援此功能。


* Adobe Target整合現在可以使用Target Standard API。 舊版AEM會使用Target Classic HTTP API，現已淘汰。
* Adobe Target `mbox.js` 包含63版。 Adobe強烈建議將實作切換為 `at.js` v1.x。
* `at.js` 現已包含1.5.0版。 Adobe建議您使用 [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 準備 `at.js` v1.x。

#### AEM和Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` 包含H.27.5。 Adobe建議您將實作切換為 `AppMeasurement.js`
* `AppMeasurement.js` 包含1.8.0版。 Adobe建議使用 [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 將AppMeasurement.js布建至網站。

#### AEM與商務 {#aem-commerce}

自AEM 6.4起，Commerce Integration Framework的改良速度更快。 [如需詳細資訊，請前往這裡](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

#### Communities附加元件 {#communities-add-on}

若要取得最新版本，請參閱 [部署社群](/help/communities/deploy-communities.md) 一節。

##### 增強社群參與 {#enhancements-to-community-engagement}

**@Mentions支援**
AEM Communities現在可讓註冊使用者在「使用者產生的內容」中標籤（提及）其他已註冊成員，以吸引其注意。 接著會通知標籤（提及的）成員，並附上對應使用者產生內容的深層連結。 不過，使用者可以選擇停用/啟用網路和電子郵件通知。

![提及次數支援](/help/release-notes/assets/at-mentions.png)

社群使用者不需要搜尋其名字、姓氏或使用者名稱，即可查看是否有任何人與他們取得聯繫或需要他們注意。 此外，它允許UGC作者尋求特定註冊用戶的回應，這些註冊用戶能夠最好地解決問題並添加輸入。

社群管理員需 **啟用提及次數** 在社群元件上，讓已註冊的使用者能夠在這些元件上使用功能。

**群組訊息**

已註冊的社群成員現在可以透過單一電子郵件組合大量傳送直接訊息給群組，而非個別傳送相同的訊息給群組成員。 若要允許 [群組訊息](/help/communities/configure-messaging.md)，請啟用 [報文傳送操作服務](/help/communities/messaging.md#group-messaging).

![群組訊息](/help/release-notes/assets/group-messaging.png)

##### 大量協調的增強功能 {#enhancements-to-bulk-moderation}

大量協調中的自訂篩選器

[自訂篩選器](/help/communities/moderation.md#custom-filters) 現在可開發並新增至「大量協調」UI。

A [範例專案](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) 說明可透過標籤篩選，於 [Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). 此專案可作為開發類似自訂篩選器的基礎。

![自訂篩選器](/help/release-notes/assets/custom-tag-filter.png)

**大量協調中的清單檢視**

已提供新的「清單檢視」，並改善UI，以大量協調顯示「使用者產生的內容」項目。

![清單檢視中的大量協調](/help/release-notes/assets/list-view-moderation.png)

##### 增強網站和群組管理 {#enhancements-to-site-and-group-management}

**作者端網站和群組管理員**

AEM 6.5以後的Communities允許對不同的社群網站和群組/巢狀群組進行分散管理（和管理）。 托管多個社群網站和巢狀群組的組織現在可以在建立網站（和群組）時，為作者端的管理員角色選取成員。

![站點管理員](/help/release-notes/assets/site-admin.png)

網站管理員可以在任何階層層級建立群組，並成為預設管理員。 其他群組管理員稍後可移除這些管理員。 群組管理員可以管理其群組G1，並在G1下建立巢狀子群組。

##### 啟用的增強功能 {#enhancements-to-enablement}

**SCORM 2017.1支援**

AEM 6.5 Communities的啟用功能支援可共用內容物件參考模型 [(SCORM)2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。

* 啟用元件的鍵盤導覽支援
* AEM Communities中的啟用元件（例如目錄和課程播放、工作總攬、檔案程式庫）支援鍵盤導覽，以改善協助工具。

##### 其他增強功能 {#other-enhancements}

* Solr 7支援
* AEM 6.5社群在設定MSRP和DSRP時，支援Apache Solr 7.0版的搜尋平台。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5導入了下列功能和增強功能，以提升AEM使用者、DAM角色以及相關創意和行銷角色的生產力。

#### 與整合 [!DNL Adobe Creative Cloud] 和創意工作流程 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] 提供多種整合方式，與 [!DNL Adobe Creative Cloud] 和共用資產，以便在創意與行銷或業務團隊密切合作的工作流程中使用。 [!DNL Experience Manager] 6.5繼續改進整合工作，並進一步精簡整合工作，以揭示更多機會和精簡現有方法。

深入了解 [!DNL Experience Manager] 6.5，以最佳方式支援您的內容速度使用案例。

##### Adobe資產連結 {#aal}

[!DNL Adobe Asset Link] 加強創意人員與行銷人員在內容建立程式中的協作。 創作者可存取儲存在 [!DNL Experience Manager Assets]，而不需離開他們最熟悉的應用程式。 創意人員可使用 [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]，和 [!DNL Adobe InDesign] 應用程式。

[!DNL Adobe Asset Link] 是 [企業Creative Cloud](https://www.adobe.com/creativecloud/business/enterprise.html) 提供。 如需詳細資訊，包括 [!DNL Experience Manager] 部署，請參閱 [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html).

![在Adobe Photoshop中搜尋資產](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] 整合 {#stock}

貴組織可使用 [!DNL Adobe Stock] 企業計畫 [!DNL Experience Manager Assets] 確保授權資產可廣泛用於您的創意和行銷專案。 您可以快速找到、預覽和授權 [!DNL Adobe Stock] 以Experience Manager儲存的資產，使用 [!DNL Experience Manager].

[!DNL Adobe Stock] 該服務為設計人員和企業提供數百萬張高質量、精心策劃、免版稅的照片、向量圖、插圖、視頻、模板和3D資產，供其所有創意項目使用。

如需詳細資訊，請參閱 [在Experience Manager Assets中使用Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md).

![從Experience Manager Assets預覽Adobe Stock影像和授權](/help/release-notes/assets/stock_image_preview_license_options.png)

*圖：預覽 [!DNL Adobe Stock] 映像和許可 [!DNL Experience Manager Assets].*

![在Experience Manager中搜尋及篩選授權的Adobe Stock影像](/help/release-notes/assets/aem-search-filters2.jpg)

*圖：搜尋及篩選已授權 [!DNL Adobe Stock] 影像 [!DNL Experience Manager].*

##### 中的動態參考 [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] 用於 [!DNL Adobe InDesign] 檔案為動態。 如果參考的資產在存放庫中移動，則參考會自動更新。 如需詳細資訊，請參閱 [如何管理複合資產](/help/assets/managing-linked-subassets.md).

#### Brand Portal功能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] 可協助您輕鬆取得、有效控制並安全地將經核准的資產分散給外部廠商/代理，以及跨裝置將內部業務使用者。 它有助於提高資產共用的效率，加快資產上市時間，並消除不合規使用和未經授權的訪問的風險。

如需詳細資訊，請參閱 [Brand Portal的新功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hant).

#### 連線資產 {#connectedassets}

在大型企業中，建立網站所需的基礎架構可以分散。 有時，網站建立功能和所需的數位資產會分散在不同的孤立環境中。

[!DNL Experience Manager Sites] 提供建立網頁的功能，而 是可為網站提供必要資產的數位資產管理 (DAM) 系統。[!DNL Experience Manager Assets][!DNL Experience Manager] 現在透過整合支援上述使用案例 [!DNL Sites] 和 [!DNL Assets]. 請參閱 [如何設定及使用連線資產功能](/help/assets/use-assets-across-connected-assets-instances.md).

![從 [!DNL Experience Manager] 在 [!DNL Sites] 不同頁面 [!DNL Experience Manager] 部署](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*圖：從 [!DNL Experience Manager] 在 [!DNL Sites] 頁面 [!DNL Experience Manager] 部署。*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] 在 [!DNL Experience Manager Assets] 提供身臨其境且個人化的尖端體驗。 透過上傳單一高品質主要資產並使用Adobe的進階雲端轉譯和檢視器，您可以即時提供任何轉譯組合，以支援貴組織的媒體策略。

如需新增功能的詳細資訊， [!DNL Dynamic Media] 功能，請參閱 [Dynamic Media發行說明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### 360視訊支援 {#video-support}

直接在 [!DNL Experience Manager] 使用尖端的檢視器，將VR體驗提供至桌上型電腦、行動裝置和VR頭戴式裝置。 如需詳細資訊，請參閱 [使用360影片](/help/assets/360-video.md).

##### 自訂影片縮圖 {#custom-video-thumbnails}

您現在可以使用視訊本身或DAM中儲存的其他內容的影格，自訂視訊資產的縮圖。 如需其他指示，請參閱 [關於視訊縮圖](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### 協助工具增強功能 {#accessibility-enhancements}

[!DNL Dynamic Media] 檢視器現在支援增強的協助工具功能，例如Aria支援、螢幕閱讀器和Alt-text。 如需其他詳細資訊，請參閱 [檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### 搜尋體驗增強功能 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5之後，行銷人員可以從搜尋結果頁面更快找到所需資產。 甚至在套用搜尋篩選器之前，搜尋刻面也會以資產數量更新。 透過篩選器查看預期的計數，可協助使用者有效率地導覽搜尋結果。 如需詳細資訊，請參閱 [在Experience Manager中搜尋資產](/help/assets/search-assets.md).

![查看未篩選搜尋Facet中搜尋結果的資產數量](/help/assets/assets/asset_search_results_in_facets_filters.png)

*圖：在搜尋Facet中查看未篩選搜尋結果的資產數量。*

#### 可用性增強 {#usability-enhancement}

您現在可以選取資料夾內或搜尋結果中所有已載入的資產。 可協助您快速管理多個資產。 核取方塊會選取符合案例的所有資產（例如搜尋結果），而不只是顯示在 [!DNL Experience Manager] 介面。

![使用「全部選取」選項，只要按一下即可選取所有載入的資產。](/help/release-notes/assets/select-all-in-aem-assets.gif)

*圖：使用「全部選取」選項，只要按一下即可選取所有載入的資產。*

#### 中繼資料增強功能 {#metadata-enhancements}

[!DNL Assets] 可讓您建立資產資料夾的中繼資料結構，定義資料夾屬性頁面中顯示的配置和中繼資料。 現在，您可以在建立資料夾時，將資料夾中繼資料結構指派給現有資料夾。 如需詳細資訊，請參閱 [資料夾中繼資料結構](/help/assets/metadata-config.md#folder-metadata-schema).

指定階層式中繼資料時，可在執行階段從JSON檔案載入選項，例如，不必在表單中手動輸入。 如需詳細資訊，請參閱 [階層中繼資料](/help/assets/metadata-schemas.md#cascading-metadata).

#### 報表增強功能 {#reporting-enhancements}

內容片段和連結分享現在會包含在下載的報表中。 如需詳細資訊，請參閱 [Assets報表](/help/assets/asset-reports.md).

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

請參閱 [AEM 6.5 Forms的新功能和增強功能摘要](/help/forms/using/whats-new.md) 以取得新功能和改善功能與檔案資源的相關資訊。

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

您可以將Livefyre與AEM 6.5執行個體整合。 請參閱 [如何整合Livefyre與AEM](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html).

### 利用以客戶為中心的開發 {#leverage-customer-focused-development}

Adobe使用以客戶為中心的開發模型，允許客戶在規格、開發和測試期間為開發流程的所有階段作出貢獻。 在此過程中，我們感謝所有貢獻客戶和合作夥伴。

Adobe已制定程式和程式，以便收集、排定優先順序及追蹤以客戶為中心的錯誤解決方法，以及開發增強功能要求。 此 [Experience Manager支援入口網站](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 整合了Adobe增強和缺陷跟蹤系統。 客戶問題會盡可能由客戶支援團隊識別和解決。 呈報至研發時，會擷取所有客戶資訊，並用於優先順序和報告用途。 在開發中，優先考慮付費支援、保證問題和客戶付費的增強功能。

此優先順序排列程式已產生750多項以客戶為重點的變更，已在AEM 6.5中修正。

## 屬於此版本的檔案清單 {#list-of-files-that-are-part-of-the-release}

**Foundation**

* 獨立快速入門： `cq-quickstart-6.5.0.jar`.
* 應用程式伺服器快速入門： `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2或更新版本，適用於各種Web伺服器和平台。 請參閱 [下載連結](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Eclipse IDE外掛程式([了解詳情及下載](/help/sites-developing/aem-eclipse.md))

* 方括弧程式碼編輯器的擴充功能([了解詳情及下載](/help/sites-developing/aem-brackets.md))
* Maven/Gradle相依性([下載連結](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**網站**

* 核心元件([GitHub專案](https://github.com/adobe/aem-core-wcm-components))
* We.Retail參考實作([閱讀更多資訊](/help/sites-developing/we-retail.md))
* Maven專案原型：

   * 對於完整堆棧站點： [GitHub專案](https://github.com/adobe/aem-project-archetype)
   * 針對具有React/Angular的單頁應用程式： [GitHub專案](https://github.com/adobe/aem-spa-project-archetype)

* AEM Screens播放器([下載](https://download.macromedia.com/screens/))

* 智慧內容語言模型。 已預先安裝英文 — 可下載更多語言

   * [德文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [義大利文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM最新化工具套裝，例如對話方塊轉換工具。 ([GitHub專案](https://github.com/adobe/aem-modernize-tools))

**資產**

* 新增增強PDF模擬轉譯器([閱讀更多資訊](/help/assets/aem-pdf-rasterizer.md))
* 要添加擴展RAW映像支援的包([閱讀更多資訊](/help/assets/camera-raw.md))

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

如需設定需求，請參閱 [安裝指示](/help/sites-deploying/custom-standalone-install.md).

如需詳細指示，請參閱 [升級檔案](/help/sites-deploying/upgrade.md).

## 支援平台 {#supported-platforms}

查找支援平台的完整清單，包括支援級別 [AEM 6.5技術要求](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle已移至OracleJava SE產品的長期支援(LTS)模型。 Java 9和10是依Oracle分類的非LTS版本。 請參閱 [OracleJava SE支援藍圖](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe支援LTS版的Java，僅在生產環境中執行AEM。 Java 11是搭配AEM 6.5使用的建議版本。

## 過時和移除的功能 {#deprecated-and-removed-features}

Adobe不斷評估產品中的功能，並隨著時間的推移計畫用更強大的版本替換功能，或者決定重新實施選定的部件，以便更好地為將來的期望或擴展做好準備。

針對 [!DNL Adobe Experience Manager] 6.5, [閱讀已棄用和已移除功能的清單](/help/release-notes/deprecated-removed-features.md). 此頁面也包含近期變更的預先公告，以及客戶從舊版更新的重要通知。

## 已知問題 {#known-issues}

### 平台 {#platform}

* 系統回報CRX快速入門及其內容遭刪除的問題。

   在這些動作上，請確定屬性 `htmllibmanager.fileSystemOutputCacheLocation` 不是空字串：

   1. 呼叫 `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. 升級至AEM 6.5。
   3. 在AEM 6.5上執行「延遲內容移轉」。

   A [知識庫](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) 文章已提供詳細資訊，並提供此問題的因應措施。

* 如果您使用AEM 6.5執行個體的JDK 11，部署某些套件後，某些頁面可能會顯示為空白。 記錄檔中會顯示下列錯誤訊息：

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

若要解決此錯誤：

1. 停止AEM例項。 前往 `<aem_server_path_on_server>crx-quickstart\conf` 然後開啟 `sling.properties` 檔案。 Adobe建議備份此檔案。

1. 搜尋 `org.osgi.framework.bootdelegation=`. 新增 `jdk.internal.reflect,jdk.internal.reflect.*` 屬性，將結果顯示為。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 儲存檔案並重新啟動AEM執行個體。

## 網站 {#sites}

* **使用頁面版本**:如果頁面已移動，則您無法再對移動前進行的任何版本執行預覽。

### 資產 {#assets}

* **搜尋：** 如果搜尋字串包含前導空格([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **資料夾中繼資料結構**:新增選擇按鈕後，ID和值欄位無法如預期呈現，且刪除功能無法運作。 (CQ-4261144)
* 重新命名資產時，無法在資產名稱中使用空白字元。 (CQ-4266403)

### Forms {#forms}

* 當AEM Forms安裝在Linux作業系統上時，具有硬體安全模組的數位簽名無法運作。 (CQ-4266721)
* (僅限WebSphere上的AEM Forms) **Forms Workflow** > **任務搜索** 如果您搜尋 **管理員** with **使用者名稱** 作為搜尋條件。 (CQ-4266457)

* AEM Forms無法將具有JPEG壓縮的TIF和TIFF檔案轉換為PDF檔案。 (CQ-4265972)
* 此 **AEM Forms Assets掃描器** 和 **信函到互動式通訊移轉** 選項在 **AEM Forms移轉** 頁面。 (CQ-4266572)

* （僅限JBoss 7）從舊版升級至AEM 6.5 Forms，且舊版有建立並使用預設提交或預設呈現程式副本的程式(.lca)時，使用此類程式(.lca)的HTML5 Forms無法執行所需動作。 (CQ-4243928)
* 在自適應自中，當從規則編輯器調用表單資料模型服務以動態更新影像選擇元件的值時，不更新影像選擇元件的值。 (CQ-4254754)
* AEM Forms Designer安裝程式需要32位元版本 [Visual C++可再分發運行時包2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) 和 [Visual C++可再分發運行時包2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). 在開始安裝之前，請確保已安裝上述可重新分發的運行時包。 (CQ-4265668)

* PDF產生器不支援基於智慧卡的身份驗證。  當管理員啟用組策略時 `Interactive Logon: Require Smart card` 在Windows伺服器上，所有現有PDF生成器用戶都將失效。

* 將適用性表單設定為動態更新元件的值，並透過Dispatcher存取托管表單的發佈例項時，動態更新欄位值的功能將停止運作。 若要解決此問題，請在發佈執行個體上開啟CRXDE，導覽至 `/libs/fd/af/runtime/clientlibs/guideChartReducer`，並建立下方所列的屬性。

   * 名稱：allowProxy
   * 類型：布林值
   * 值：true
   * 受保護：False
   * 強制：False
   * 多個：False
   * 自動建立：False

   此屬性可讓執行階段資料夾下的用戶端程式庫存取Proxy。 (CQ-4268679)

* AEM Forms啟動時， `SAX Security Manager could not be setup` 警告出現。
* 在執行Adobe Acrobat Reader 20.10.00版的Apple iOS或iPadOS上開啟受AEM Forms檔案安全性保護的PDF時。
* 從 Apple iOS 裝置提交包含標準 HTML 上傳欄位的表單時，有時不會傳送檔案內容並在另一端收到 0 位元組檔案。Apple iOS 15.1 提供此問題的修正。

## 產品下載與支援（受限網站） {#product-download-and-support-restricted-sites}

以下網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [請前往licensing.adobe.com下載產品](https://licensing.adobe.com/).

* 產品更新、修補程式和包，以獲得 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

* [透過Admin Console提供客戶支援](https://adminconsole.adobe.com/). 如需詳細資訊，請參閱 [全新Adobe客戶支援體驗](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
