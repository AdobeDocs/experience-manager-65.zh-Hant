---
title: 常規發行說明 [!DNL Adobe Experience Manager] 6.5
description: '"[!DNL Adobe Experience Manager] 6.5說明，概述發行資訊、新增功能、安裝方式和詳細的更改清單。」'
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '4696'
ht-degree: 4%

---

# 常規發行說明 [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 |
| 類型 | 主要版本 |
| 一般可用性日期 | 2019 年 4 月 8 日 |
| 建議的更新 | 請參閱 [AEM最近更新](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)。 |

### Trivia {#trivia}

此版本的 [!DNL Adobe Experience Manager] 自2018年4月4日起，經過23次質量保證和缺陷修復，於2019年3月28日終止。 這一版發行中修正的客戶相關問題，包括加強與新功能，總共有 1345 個。

[!DNL Adobe Experience Manager] 6.5自2019年4月8日起正式提供。

![AEM 6.5登錄螢幕](/help/assets/assets/aem65-login-v4.png)

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5是升級版 [!DNL Adobe Experience Manager] 6.4代碼庫。 此版本提供全新的增強功能、重要客戶修正、高優先順序的客戶增強功能，以及針對產品穩定化的一般錯誤修正。它還包括 [!DNL Adobe Experience Manager] 6.4 Service Pack最多可發行SP4。

下面的清單提供了概述 — 而後續頁面則列出了全部詳細資訊。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

平台 [!DNL Adobe Experience Manager] 6.5在基於OSGi的框架（Apache Sling和Apache Felix）和Java內容儲存庫的更新版本之上構建：阿帕奇·傑克拉比·橡1.10.2。

Quickstart將Eclipse Jetty 9.4.15用作Servlet引擎。

#### Java支援  {#java-support}

* 對Java 11以及已支援的Java 8的新支援。
* 為獲得最佳效能，請用其他值覆蓋預設GC值。 有關詳細資訊，請參見 [安裝和更新](/help/sites-deploying/custom-standalone-install.md) 的子菜單。
* 當未從Adobe公開時，Java 11和Java 8維護更新會通過Oracle分AEM發，以便客戶在相關項目中使用。

#### Java開發 {#java-development}

* 現在 [烏貝爾哈的兩個版本](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)、建議的版本，其中包含未標籤為棄用的公共介面，以及包含標籤為棄用的介面的版本。

#### 使用者介面 {#user-interface}

對用戶介面進行了各種增強，使其更高效，更易於使用。

* 用戶和組的新權限管理UI。
* 列視圖現在也只載入螢幕上可見的條目，並且僅在用戶開始滾動時載入更多條目。 清單和卡視圖自6.0（在6.4中改進）以來就已經執行了此操作。
* 列視圖現在包括頁面/資產的工作流狀態（如果適用）。
* 的 [全選](/help/sites-authoring/basic-handling.md#select-all) action是執行同一資料夾中所有頁面/資產的操作的快速方法。
* 的 [全選](/help/sites-authoring/basic-handling.md#select-all) 操作嘗試對所有頁面/資產執行操作，而不只是載入了什麼。 如果未將操作升級為處理批量操作，則將顯示警告對話框。

>[!CAUTION]
>
>Adobe不打算對經典用戶介面進行進一步的增強。 AEM6.5包含經典UI，從早期版本升級的客戶可以繼續按原樣使用它。 請注意，不建議使用時，Classic UI仍完全受支援。 [閱讀更多內容](/help/sites-deploying/ui-recommendations.md)。

#### 搜索和索引 {#indexing-and-search}

* 在Oak中搜索現在支援動態小平面。 例如，資產搜索中的過濾欄顯示估計的結果量。
* 擴展了QueryBuilder，以提供具有動態小平面的結果。

#### 升級 {#upgrade}

* 運行6.2 、 AEM 6.3和6.4的客AEM戶支援直接就地升級到6.5。使用5.x或6.0/6.1的客戶若想使用就地升級，需要先升級到6.4 — 然後升級到6.5 ，或通過將實例之間的內容直接傳輸到AEM6.5來升級。
* 升級程式在6.5中基本保持不變。
* 我們繼續支援6.4中引入的向後相容性、升級複雜性評估和可持續升級功能。在需要時對這些區域進行了特定版本的更新。
* 陣列檢測器封裝已簡化，並且將有一個軟體包評估可用源版本升級到6.5。
* 有關升級過程的詳細資訊，請參閱 [升級文檔](/help/sites-deploying/upgrade.md)。

#### 項目和工作流 {#projects-and-workflows}

* 在6.4中引入的新工作流模型編輯器已得到改進，包括了更多操作，如「複製和發佈」、「工作流」步驟中的「變數」支援以及增強 `OR` 和 `AND` 拆分。

#### 存放庫 {#repository}

* Adobe Experience Manager6.5的基礎是基於OSGi的框架（Apache Sling和Apache Felix）和Java內容儲存庫的更新版本：阿帕奇·傑克拉比·橡1.10.2。
* 有關已修復問題的概覽，請參閱 [Apache Jackrabbit Oak Jira訴1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)。 [Apache Jackrabbit Oak Jira訴1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 和 [Apache Jackrabbit Oak Jira訴1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)。

>[!CAUTION]
>
>自6.3以來新版本的Oak Segment TarAEM需要遷移儲存庫。 如果要從較舊版本的TarMK升級，或希望從另一類型的持久性中切換新的Segment Tar，則此步驟是必需的。 有關新Segment Tar的優勢的詳細資訊，請參見 [遷移到Oak Segment Tar常見問題](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar)。

#### 奧斯吉 {#osgi}

* 已添加OSGi Poriments和Converter實用程式庫。

#### 安全性 {#security}

* 已為管理員用戶添加密碼到期。

#### Web伺服器 {#web-server}

* Quickstart分發將Eclipse Jetty 9.4.15用作Servlet引擎(隨附AEM於9.3.22的6.4)。

### [!DNL Experience Manager] 網站 {#experience-manager-sites}

#### 托管單頁應用 {#managed-single-page-apps}

頁面編輯器添加了在上下文中編輯內容和在客戶端呈現體驗內合成/佈局的功能（也已知） [作為編SPA輯器](/help/sites-developing/spa-architecture.md))。 使用JavaScript框架構建的現有單頁應用可以使用AEMSJ SDK擴展React或Angular，使從業人員可編輯。

第一次作為AEM6.4 SP2的一部分發AEM貨，具有SPA以下功能：

* 使用模板編輯器編輯和配AEM置可編輯部SPA分
* 使用多站點管理建立國家/地區、特許經營或白色標SPA記體驗

#### 無頭內容管理 {#headless-content-management}

AEM能夠以各種格式和堆棧的不同級別為內容提供服務。 有些從2008年開始就開始使用 [吊帶GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 和 [POSTServlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)。 內容服務([Sling模型導出器](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html))在AEM6.3中引入，是AEMSJ SDK用於水合單頁應用的方法。 的 [資產的HTTP API](/help/assets/mac-api-assets.md) 是CRUD API，擴展為AEM6.5。

新的HTTP API功能：

* 已添加 [對資產的HTTP API的內容片段支援](/help/assets/assets-api-content-fragments.md) 建立、更新、讀取和刪除片段。
* 通過Content Services公開內容片段清單 [內容片段清單核心元件](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html)。
* [核心元件庫](https://opensource.adobe.com/aem-core-wcm-components/library.html) 顯示每個元件的預設Content Services JSON輸出

#### 螢幕載入項 {#screens-add-on}

在從互動式亭子到數字標牌的所有數字顯示器上高效設計、交付和優化體驗。

* 通過改進的內容重用，跨數字和儲存中統一體驗和內容
* 簡化的創作和批准/發佈工作流，支援啟動
* 使用編輯器編輯和提供豐富的交互SPA體驗
* 使用「發佈」計畫標牌內容的未來內容更改
* 在序列通道中計量重放
* 使用源檔案（如Excel工作表）自動建立項目結構
* 擴展的媒體播放器支援，具有強大的線上和離線操作(Smart Sync)，可擴展到甚至最大的標牌網路。
* 使用動態佔位符按資料觸發的內容的位置或配置進行個性化設定。
* Adobe Analytics與AEM Screens玩家的整合帶動的統一見解

有關對AEM Screens的更改的詳細資訊 — 請參閱 [AEM Screens使用手冊](https://docs.adobe.com/content/help/zh-Hant/experience-manager-screens/user-guide/aem-screens-introduction.html)。

#### 元件和模板開發 {#component-amp-template-development}

* 有關新項目的Maven項目原型18+，請參見 [發行說明的Github](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases)。
* 新項目的單頁App Maven項目原型1.0.6+，請參見 [發行說明的Github](https://github.com/adobe/aem-spa-project-archetype/releases)。
* HTL 1.4版，請參見 [發行說明的Github](https://github.com/adobe/htl-spec/releases/tag/1.4)。

   * 字串、陣列和對象的「in」運算子：

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * 具有資料漏洞集的變數聲明：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 列出和重複控制參數：開始，步驟，結束：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * 資料洩漏解包的標識符：

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 支援負數

* 核心元件2.3.2+，請參見 [發行說明的Github](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases)。
* 用於佈局容器的網格系統，請參閱 [吉圖布](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)。
* 客戶端庫管理器：使「Google關閉編譯器」預設為JavaScript客戶端的小型化（舊預設值為Yahoo UYI），並將「Google關閉編譯器」更新為v20190121版
* 模板編輯器和策略

   * 為使用JS SDK的單頁應用建立和編輯模板(也稱為編SPA輯器)

* 參考網站We.Retail 4.0，請參閱 [發行說明的Github](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)。
* 用於升級現有站點以利用最新編輯器功能的工具包，請參見 [Github儲存庫](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>包AEM括版本1.12.4的jQuery庫，以提供與現有自定義代碼的最大相容性。 已通過Adobe進行了修改，以解決已知的安全問題。

#### 站點管理 {#site-administration}

* 的 [引用](/help/sites-authoring/author-environment-tools.md#references) rail有一個新部分，列出指向選定頁面的內部連結。 這在計畫使頁面離線或刪除時非常有用 — 查看哪些頁面需要在離線之前進行調整。
* 的 [清單視圖](/help/sites-authoring/basic-handling.md#list-view) 有一個新的工作流列，該列顯示頁面當前處於工作流中時的狀態。
* 在 [頁屬性](/help/sites-authoring/editing-page-properties.md)，現在可以在為頁面分配縮略圖（縮略圖頁籤）時瀏覽現有資產。

#### 頁面編輯器 {#page-editor}

* 允許在上下文內編輯和合成單頁應用程式體驗，該體驗使用利用JS SDK的React和React和ReactAngular客戶端元件(也稱為SPAEditor)構建
* 僅當頁面配置了腳手架頁面時，才顯示「腳手架模式」。

#### 內容片段和編輯器 {#content-fragments-amp-editor}

* 新建 [注釋](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) 在「內容片段編輯器」中導軌，以在文本中作出一般注釋並查看注釋（也顯示在時間軸導軌中）
* 能夠在 [內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 到簡單文本、富格文本或標籤
* 添加 [注釋/注釋](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) 通過選擇RTE（全屏視圖）中的文本
* [比較版本](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) 通過參考軌並排顯示內容片段
* 「資產下載報告」現在相應地顯示內容片段
* 添加 [對資產HTTP API的內容片段支援](/help/assets/assets-api-content-fragments.md) 通過/api.json。 有用於建立、更新、讀取和刪除內容片段的API。

#### 體驗片段 {#experience-fragments}

* 改進了 [體驗片段](/help/sites-authoring/experience-fragments.md)因此，在搜索使用它們的頁面時會找到它們的內容
* 的 [導出到目標](/help/sites-administering/experience-fragments-target.md) 選項現在允許將體驗片段作為JSON發送(預設為HTML)，或同時發送兩者

#### 轉換 {#translation}

* 使用項目主體簡化翻譯項目的建立
* 通過將翻譯作業設定為預設批准狀態，簡化執行翻譯項目
* 允許使用第三方翻譯記憶庫中的更改更新已翻譯的頁面
* 允許以JSON格式導出翻譯作業
* 更新Microsoft翻譯整合以使用V3 API

#### 多站點管理(MSM) {#multi-site-management-msm}

* 對於使用PushOnModify的展開配置，可以更好地處理頁面移動操作以避免狀態不一致
* 現在，在livecopy結構內建立新頁預設情況下將建立獨立頁
* 在使用JS SDK的單頁應用中使用MSM功能(也稱為SPA編輯器)

#### 啟動 {#launches}

* 啟動的新審閱和批准工作流，以及僅升級已批准的啟動頁面的功能
* 已添加 [選項，以選擇在升級步驟後立即刪除啟動](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### 內容目標和模擬 {#content-targeting-simulation}

* ContextHub資料層和客戶端規則引擎JavaScript已更新為預設使用jQuery 3。

#### AEMAdobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>當前：
>
>* 僅 `at.js 1.x` 如果在「活動」控制台中將Adobe Target用作目標引AEM擎，則支援此選項。
>
>* 兩者 `at.js. 1.x` 和 `at.js 2.x` 如果使用Experience Fragment導出到目標並在目標的控制台內運行Activities，則支援。


* Adobe Target整合現在可以使用目標標準API。 早期版本AEM使用目標經典HTTP API，現在已棄用。
* Adobe Target `mbox.js` 包含63版。 Adobe強烈建議將實施切換到 `at.js` v1.x
* `at.js` 1.5.0版現已包括。 Adobe建議您使用 [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 提供 `at.js` 1.x版。

#### AEMAdobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` 包括H.27.5。 Adobe建議您將實施切換到 `AppMeasurement.js`
* `AppMeasurement.js` 包含v1.8.0。 Adobe建議使用 [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 將AppMeasurement.js置備到站點。

#### 和AEM商業 {#aem-commerce}

自6.4以來，對Commerce Integration Framework的改進已進入更快的AEM發佈週期。 [在此處瞭解更多資訊](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html)。

#### 社區載入項 {#communities-add-on}

要獲取最新版本，請參閱 [部署社區](/help/communities/deploy-communities.md) 的雙曲餘切值。

##### 增強社區參與 {#enhancements-to-community-engagement}

**@Mentions支援**
AEM Communities現在允許註冊用戶在用戶生成的內容中標籤（提及）其他註冊成員以引起他們的注意。 然後通知標籤（提及的）成員，其具有到相應用戶生成內容的深度連結。 但是，用戶可以選擇禁用/啟用Web和電子郵件通知。

![提及支援](/help/release-notes/assets/at-mentions.png)

社區用戶無需搜索其名、姓或用戶名，即可查看是否有人聯繫過他們或需要他們的注意。 此外，它還允許UGC的作者尋求能夠最好地解決該問題並添加輸入的特定註冊用戶的響應。

社區管理員需要 **啟用提及** 在社區元件上允許註冊用戶使用這些元件上的功能。

**組消息**

註冊的社區成員現在可以通過單個電子郵件組合將直接郵件批量發送到組，而不是單獨將同一郵件發送到組成員。 允許 [組消息](/help/communities/configure-messaging.md)，啟用兩個實例 [消息傳遞操作服務](/help/communities/messaging.md#group-messaging)。

![組消息](/help/release-notes/assets/group-messaging.png)

##### 批量審核功能增強 {#enhancements-to-bulk-moderation}

批量審核中的自定義篩選器

[自定義篩選器](/help/communities/moderation.md#custom-filters) 現在可以開發並添加到批量審核UI中。

A [示例項目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) 在中演示通過標籤過濾 [吉圖布](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)。 此項目可用作開發類似自定義篩選器的基礎。

![自定義篩選器](/help/release-notes/assets/custom-tag-filter.png)

**批量審核中的清單視圖**

已以批量審核方式提供具有改進UI的新清單視圖，以顯示用戶生成的內容條目。

![清單視圖中的批量審核](/help/release-notes/assets/list-view-moderation.png)

##### 對站點和組管理的增強 {#enhancements-to-site-and-group-management}

**作者端站點和組管理員**

6.AEM5以後的社區允許對不同的社區站點和組/嵌套組進行分散管理（和管理）。 托管多個社區站點和嵌套組的組織現在可以在建立站點（和組）時為「作者」端的管理員角色選擇成員。

![站點管理員](/help/release-notes/assets/site-admin.png)

站點管理員可以在任何層次結構級別建立組，並成為預設管理員。 這些管理員稍後可由其他組管理員刪除。 組管理員可以管理其組G1並建立嵌套在G1下的子組。

##### 增強支援 {#enhancements-to-enablement}

**SCORM 2017.1支援**

6.5社區的啟AEM用功能支援可共用內容對象參考模型 [(SCORM)2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。

* 支援元件的鍵盤導航支援
* AEM Communities的啟用元件（例如目錄和課程播放、作業、檔案庫）支援鍵盤導航，以改進輔助功能。

##### 其他增強功能 {#other-enhancements}

* Solr 7支援
* 6AEM.5社區在設定MSRP和DSRP時支援Apache Solr 7.0版本的搜索平台。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM6.5引入了以下功能和增強功能，以提高用戶AEM的生產力、DAM角色以及相關的創意和營銷角色。

#### 與 [!DNL Adobe Creative Cloud] 創意工作流 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] 提供了多種與 [!DNL Adobe Creative Cloud] 並共用資產以用於創意和營銷或業務團隊緊密協作的工作流。 [!DNL Experience Manager] 6.5繼續改進整合工作，並進一步精簡整合工作，以揭示更多機會和簡化現有方法。

閱讀以瞭解 [!DNL Experience Manager] 6.5，您可以使用它來最好地支援內容速度使用案例。

##### Adobe資產連結 {#aal}

[!DNL Adobe Asset Link] 在內容建立過程中加強創意人員和營銷人員的協作。 創意可以訪問儲存在 [!DNL Experience Manager Assets]不留下他們最熟悉的應用。 創意人員可以使用應用程式內面板無縫瀏覽、搜索、簽出和簽入資產 [!DNL Adobe Photoshop]。 [!DNL Adobe Illustrator], [!DNL Adobe InDesign] 。

[!DNL Adobe Asset Link] 是 [企業Creative Cloud](https://www.adobe.com/creativecloud/business/enterprise.html) 提供。 有關它的詳細資訊，包括 [!DNL Experience Manager] 部署，請參閱 [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。

![搜索Adobe Photoshop資產](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] 整合 {#stock}

您的組織可以使用 [!DNL Adobe Stock] 企業計畫 [!DNL Experience Manager Assets] 確保許可資產廣泛適用於您的創意和營銷項目。 您可以快速查找、預覽和許可證 [!DNL Adobe Stock] 使用強大的DAM功能保存在Experience Manager中的資產 [!DNL Experience Manager]。

[!DNL Adobe Stock] 服務為設計師和企業提供了對其所有創造性項目的數百萬高質量、可策劃的免版稅照片、向量、插圖、視頻、模板和3D資產的訪問權。

有關詳細資訊，請參見 [在Experience Manager Assets使用Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md)。

![從Experience Manager Assets預覽Adobe Stock影像和許可證](/help/release-notes/assets/stock_image_preview_license_options.png)

*圖：預覽 [!DNL Adobe Stock] 映像和許可 [!DNL Experience Manager Assets]。*

![在Experience Manager中搜索和篩選許可的Adobe Stock影像](/help/release-notes/assets/aem-search-filters2.jpg)

*圖：搜索和篩選許可證 [!DNL Adobe Stock] 影像 [!DNL Experience Manager]。*

##### 中的動態引用 [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] 用於 [!DNL Adobe InDesign] 檔案是動態的。 如果被引用的資產在儲存庫中移動，則引用將自動更新。 有關詳細資訊，請參見 [如何管理複合資產](/help/assets/managing-linked-subassets.md)。

#### Brand Portal能力 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] 幫助您輕鬆獲得、有效控制和安全地將批准的資產分佈到外部供應商/代理和跨設備的內部業務用戶。 它有助於提高資產共用的效率，加快資產的上市時間，並消除違規使用和未授權訪問的風險。

有關詳細資訊，請參見 [Brand Portal有什麼新聞嗎](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hant)。

#### 連線資產 {#connectedassets}

在大型企業中，建立網站所需的基礎架構可以分發。 有時，網站建立功能和所需的數字資產位於不同的庫中。

[!DNL Experience Manager Sites] 提供建立網頁的功能，而 是可為網站提供必要資產的數位資產管理 (DAM) 系統。[!DNL Experience Manager Assets][!DNL Experience Manager] 現在通過整合支援上述使用案例 [!DNL Sites] 和 [!DNL Assets]。 請參閱 [如何配置和使用連接的資產功能](/help/assets/use-assets-across-connected-assets-instances.md)。

![從 [!DNL Experience Manager] 部署 [!DNL Sites] 另一頁 [!DNL Experience Manager] 部署](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*圖：從 [!DNL Experience Manager] 部署 [!DNL Sites] 頁 [!DNL Experience Manager] 部署。*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] 提供增強的富媒體創作和交付 [!DNL Experience Manager Assets] 推動身臨其境且個性化的尖端體驗。 通過上載單個高質量主資產並使用Adobe的高級雲呈現和查看器，您可以即時提供任何格式副本組合以支援您組織的媒體策略。

有關新建的詳細資訊 [!DNL Dynamic Media] 功能，請參閱 [Dynamic Media發行說明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html)。

##### 360視頻支援 {#video-support}

直接在中管理360視頻檔案 [!DNL Experience Manager] 使用最先進的查看器將VR體驗交付到台式機、移動設備和VR頭戴式設備。 有關詳細資訊，請參見 [使用360視頻](/help/assets/360-video.md)。

##### 自定義視頻縮略圖 {#custom-video-thumbnails}

現在，您可以使用視頻本身或DAM中儲存的其他內容的幀來自定義視頻資產的縮略圖。 有關其他說明，請參見 [關於視頻縮略圖](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)。

##### 協助工具增強功能 {#accessibility-enhancements}

[!DNL Dynamic Media] 查看器現在支援增強的輔助功能，如Aria-support、螢幕閱讀器和Alt-text。 有關其他詳細資訊，請參閱 [查看器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html)。

#### 搜索體驗增強 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5之後，營銷人員可以從搜索結果頁面更快地發現所需的資產。 即使在應用搜索過濾器之前，搜索小平面也會隨資產數量而更新。 查看過濾器的預期計數有助於用戶高效地瀏覽搜索結果。 有關詳細資訊，請參見 [在Experience Manager中搜索資產](/help/assets/search-assets.md)。

![查看未篩選搜索小平面中搜索結果的資產數](/help/assets/assets/asset_search_results_in_facets_filters.png)

*圖：查看不篩選搜索方面搜索結果的資產數。*

#### 可用性增強 {#usability-enhancement}

現在，您可以在資料夾內或從搜索結果中一次性選擇所有載入的資產。 它幫助您快速管理多個資產。 此複選框將選擇符合方案的所有資產，例如搜索結果，而不僅選擇在 [!DNL Experience Manager] 。

![使用「全選」(Select All)選項，一次按一下即可選擇所有已載入的資產。](/help/release-notes/assets/select-all-in-aem-assets.gif)

*圖：使用「全選」(Select All)選項，一次按一下即可選擇所有已載入的資產。*

#### 元資料增強 {#metadata-enhancements}

[!DNL Assets] 允許您為資產資料夾建立元資料架構，這些架構定義了資料夾屬性頁中顯示的佈局和元資料。 現在，您可以將資料夾元資料架構分配給現有資料夾或建立資料夾時。 有關詳細資訊，請參見 [資料夾元資料架構](/help/assets/metadata-config.md#folder-metadata-schema)。

指定級聯元資料時，可以在運行時從JSON檔案載入選項，例如，不必在表單中手動鍵入。 有關詳細資訊，請參見 [級聯元資料](/help/assets/metadata-schemas.md#cascading-metadata)。

#### 報告增強 {#reporting-enhancements}

內容片段和連結共用現在包含在下載的報告中。 有關詳細資訊，請參見 [資產報表](/help/assets/asset-reports.md)。

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM6.5Forms提供了一些新功能和增強功能。 重點包括：

* 跟蹤已提交表單、已處理文檔和已呈現文檔數的事務處理報表
* 對互動式通信的可用性改進
* 基於雲的自適應數字簽名
* 在AEM Sites單頁應用程式中嵌入自適應表單和互動式SPA通信。
* 支援工作流中的AEM變數
* 互動式通信中的資料顯示模式支援
* 對自適應表單和互動式通信表進行排序
* 表單資料模型中輸入資料的自動驗證

查看 [6.5Forms的新功能AEM和增強概述](/help/forms/using/whats-new.md) 獲取有關新增和改進的功能和文檔資源的資訊。

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

您可以將Livefyre與AEM6.5實例整合。 請參閱 [如何將livefyre與](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html)。

### 利用以客戶為中心的開發 {#leverage-customer-focused-development}

Adobe正在使用以客戶為中心的開發模型，該模型允許客戶在規範、開發和測試期間為開發過程的所有階段作出貢獻。 在此過程中，我們將向所有有貢獻的客戶和合作夥伴致謝。

Adobe已制定相應的流程和流程，以便收集、排定優先順序並跟蹤以客戶為中心的錯誤解決和增強請求開發。 的 [Experience Manager支援門戶](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 與Adobe增強和缺陷跟蹤系統相整合。 客戶問題由客戶支援團隊在可能的情況下確定和解決。 升級到R&amp;D後，將捕獲所有客戶資訊，並用於優先順序和報告目的。 在開發中，優先考慮有償支援、擔保問題和客戶付費的增強。

這一優先順序排列過程在6.5中完成了750多項以客戶為AEM重點的更改。

## 作為版本一部分的檔案清單 {#list-of-files-that-are-part-of-the-release}

**Foundation**

* 獨立快速入門： `cq-quickstart-6.5.0.jar`。
* 應用程式伺服器快速啟動： `cq-quickstart-6.5.0.war`。
* 用於各種Web伺服器和平台的Dispatcher 4.3.2或更高版本。 請參閱 [下載連結](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* 用於Eclipse IDE的插件([閱讀更多內容並下載](/help/sites-developing/aem-eclipse.md))

* 括弧代碼編輯器的擴展([閱讀更多內容並下載](/help/sites-developing/aem-brackets.md))
* Maven/Gradle依賴項([下載連結](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**網站**

* 核心元件([GitHub項目](https://github.com/adobe/aem-core-wcm-components))
* We.Retail Reference實施([閱讀更多](/help/sites-developing/we-retail.md))
* Maven項目原型：

   * 對於完整堆棧站點： [GitHub項目](https://github.com/adobe/aem-project-archetype)
   * 對於具有React/Angular的單頁應用： [GitHub項目](https://github.com/adobe/aem-spa-project-archetype)

* AEM Screens各目標平台玩家([下載](https://download.macromedia.com/screens/))

* 智慧內容語言模型。 預裝英語 — 可下載更多語言

   * [德文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [義大利文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* 現AEM代化工具套件，例如對話框轉換工具。 ([GitHub項目](https://github.com/adobe/aem-modernize-tools))

**資產**

* 要添加增強的PDF光柵化器([閱讀更多](/help/assets/aem-pdf-rasterizer.md))
* 要添加擴展RAW映像支援的包([閱讀更多](/help/assets/camera-raw.md))

**Forms**

* [用於AEM Forms功能的包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM FormsOSGi客戶端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 語言 {#languages}

用戶介面可以使用以下語言：

* 英文
* 德文
* 法文
* 西班牙文
* 義大利文
* 巴西葡萄牙語
* 日文
* 簡體中文
* 繁體中文（有限支援）
* 韓文

[!DNL Experience Manager] 6.5已通過GB18030-2005 CITS中文編碼標準的認證。

## 安裝和更新 {#install-update}

有關設定要求，請參閱 [安裝說明](/help/sites-deploying/custom-standalone-install.md)。

有關詳細說明，請參見 [升級文檔](/help/sites-deploying/upgrade.md)。

## 支援的平台 {#supported-platforms}

查找支援的平台的完整清單，包括支援級別 [AEM六點五技術要求](/help/sites-deploying/technical-requirements.md)。

>[!NOTE]
>
>Oracle已轉向OracleJava SE產品的長期支援(LTS)模型。 Java 9和10是非LTS版本，按Oracle。 請參閱 [OracleJava SE支援路線圖](https://www.oracle.com/technetwork/java/eol-135779.html)。 Adobe支援Java的LTS版本，只在生產AEM中運行。 建議將Java 11與AEM6.5一起使用。

## 過時和移除的功能 {#deprecated-and-removed-features}

Adobe不斷評估產品中的功能，並隨著時間推移，計畫用更強大的版本替換功能，或者決定重新實施選定的部件，以便更好地為將來的期望或擴展做好準備。

對於 [!DNL Adobe Experience Manager] 6.5, [讀取已棄用和已刪除權能的清單](/help/release-notes/deprecated-removed-features.md)。 該頁還包含對近期變化的預先公告，以及對從先前版本更新的客戶的重要通知。

## 已知問題 {#known-issues}

### 平台 {#platform}

* 將報告刪除CRX-Quickstart及其內容的問題。

   在這些操作中，確保 `htmllibmanager.fileSystemOutputCacheLocation` 不是空字串：

   1. 呼叫 `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`。
   2. 升級到AEM6.5。
   3. 在6.5上執行「懶AEM散內容遷移」。

   A [知識庫](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) 文章提供了更多詳細資訊和解決此問題的方法。

* 如果將JDK 11與AEM6.5實例一起使用，則部署某些包後，某些頁面可能顯示為空白。 日誌檔案中顯示以下錯誤消息：

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

要解決此錯誤：

1. 停止實AEM例。 轉到 `<aem_server_path_on_server>crx-quickstart\conf` 開啟 `sling.properties` 的子菜單。 Adobe建議備份此檔案。

1. 搜尋 `org.osgi.framework.bootdelegation=`. 添加 `jdk.internal.reflect,jdk.internal.reflect.*` 顯示結果的屬性。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 保存檔案並重新啟AEM動實例。

### 網站 {#sites}

* **使用頁面版本**: [如果已移動頁面，則無法再對移動之前建立的任何版本執行預覽](/help/sites-authoring/working-with-page-versions.md#previewing-a-version)。

### 資產 {#assets}

* **搜索：** 如果搜索字串包含前導空格()，則搜索不會生成任何返回[OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **資料夾元資料架構**:添加選擇按鈕後，ID和值欄位不會按預期方式呈現，刪除功能將不起作用。 (CQ-4261144)
* 更名資產時，不能在資產名稱中使用空格。 (CQ-4266403)

### Forms {#forms}

* 當AEM Forms安裝在Linux作業系統上時，帶硬體安全模組的數字簽名無法正常工作。 (CQ-4266721)
* (僅AEM Forms在WebSphere上) **Forms Workflow** > **任務搜索** 的子菜單。 **管理員** 與 **用戶名** 的子菜單。 (CQ-4266457)

* AEM Forms無法將具有JPEG壓縮的TIF和TIFF檔案轉換為PDF文檔。 (CQ-4265972)
* 的 **AEM Forms資產掃描程式** 和 **信函到互動式通信遷移** 選項不適用 **AEM Forms移民** 的子菜單。 (CQ-4266572)

* （僅限JBoss 7）從早期版本升級到AEM6.5Forms，且早期版本具有建立並使用預設提交或預設呈現流程副本的流程(.lca)時，使用此類流程(.lca)的FormsHTML無法執行所需操作。 (CQ-4243928)
* 在自適應中，當從規則編輯器調用表單資料模型服務以動態地更新影像選擇元件的值時，不更新影像選擇元件的值。 (CQ-4254754)
* AEM Forms設計器安裝程式需要32位版本 [Visual C++可再發行運行時包2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) 和 [Visual C++可再發行運行時包2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package)。 在開始安裝之前，請確保已安裝上述可再分發運行時包。 (CQ-4265668)

* PDF生成器不支援基於智慧卡的身份驗證。  當管理員啟用組策略時 `Interactive Logon: Require Smart card` 在Windows伺服器上，所有現有PDF生成器用戶都無效。

* 當自適應表單被配置為動態更新元件的值並且承載表單的發佈實例通過調度程式被訪問時，動態更新欄位值的功能停止工作。 要解決此問題，請在發佈實例上開啟CRXDE，導航到 `/libs/fd/af/runtime/clientlibs/guideChartReducer`，並建立下面列出的屬性。

   * 名稱：allowProxy
   * 類型：布爾型
   * 值：真
   * 受保護：假
   * 必需：假
   * 多個：假
   * 自動建立：假

   該屬性使運行時資料夾下的客戶端庫能夠訪問代理。 (CQ-4268679)

* 當AEM Forms開始時， `SAX Security Manager could not be setup` 警告。
* 當您在運行Adobe Acrobat Reader版本20.10.00的AppleiOS或iPadOS上開啟受AEM Forms文檔安全保護的PDF時。
* 從 Apple iOS 裝置提交包含標準 HTML 上傳欄位的表單時，有時不會傳送檔案內容並在另一端收到 0 位元組檔案。Apple iOS 15.1 提供此問題的修正。

## 產品下載和支援（受限站點） {#product-download-and-support-restricted-sites}

以下站點僅可供客戶使用。 如果您是客戶，需要訪問，請與Adobe客戶經理聯繫。

* [產品下載，網址為licensing.adobe.com](https://licensing.adobe.com/)。

* 產品更新、修補程式和包，以獲得 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。

* [客戶支援(通過Admin Console)](https://adminconsole.adobe.com/)。 有關詳細資訊，請參見 [新Adobe客戶支援體驗](https://docs.adobe.com/content/help/en/customer-one/using/home.html)。
