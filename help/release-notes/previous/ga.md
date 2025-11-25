---
title: ' [!DNL Adobe Experience Manager] 6.5的一般發行說明'
description: '[!DNL Adobe Experience Manager] 6.5說明列出發行資訊、新增功能、安裝方法以及詳細的變更清單。'
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '4477'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5的一般發行說明{#general-release-notes-for-adobe-experience-manager}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 |
| 類型 | 主要版本 |
| 正式發佈日期 | 2019 年 4 月 8 日 |
| 建議的更新 | 檢視[AEM最近更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)。 |

### Trivia {#trivia}

此版本[!DNL Adobe Experience Manager]的發行週期從2018年4月4日開始，經過23次品質保證和錯誤修正的反複，並於2019年3月28日結束。 此版本修正的增強功能和新功能等客戶相關問題總數為1345個。

[!DNL Adobe Experience Manager] 6.5自2019年4月8日起已正式推出。

![AEM 6.5登入畫面](/help/assets/assets/aem65-login-v4.png)

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5是[!DNL Adobe Experience Manager] 6.4程式碼基底的升級版本。 此版本提供全新的增強功能、重要客戶修正、高優先順序的客戶增強功能，以及針對產品穩定化的一般錯誤修正。其中也包含[!DNL Adobe Experience Manager]個6.4 Service Pack發行版本，最高至SP4。

下列清單為概觀內容，而後續頁面列出完整的詳細資訊。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5平台建置在OSGi架構的更新版本（Apache Sling和Apache Felix）和Java™內容存放庫： Apache Jackrabbit Oak 1.10.2.

快速入門使用Eclipse Jetty 9.4.15作為servlet引擎。

#### Java™ 支援  {#java-support}

* 新增對Java™ 11和已支援的Java™ 8的支援。
* 為獲得最佳效能，請以其他值覆寫預設GC值。 如需詳細資訊，請參閱[安裝與更新](/help/sites-deploying/custom-standalone-install.md)區段。
* Adobe會發佈Java™ 11和Java™ 8維護更新，以供客戶在AEM相關專案中使用(若未從Oracle公開提供)。

#### Java™開發 {#java-development}

* Uberjar[目前有](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)兩個版本，建議使用未標示為過時的公用介面版本，以及包含標示為過時的介面的版本。

#### 使用者介面 {#user-interface}

UI已進行各種增強功能，使其更有效率且更易於使用。

* 使用者和群組適用的新許可權管理UI。
* 欄檢視現在也只會載入畫面上可見的專案，並在使用者開始捲動時載入更多專案。 清單和卡片檢視從6.0開始就這樣做了（在6.4中進行了改進）。
* 欄檢視現在包含頁面/資產的工作流程狀態（如適用）。
* [全選](/help/sites-authoring/basic-handling.md#select-all)動作是將所有頁面/資產置於相同資料夾中的動作快速執行的方法。
* [全選](/help/sites-authoring/basic-handling.md#select-all)動作會嘗試對所有頁面/資產執行動作，而不只是已載入的專案。 如果動作未升級為處理大量動作，則會顯示警告對話方塊。

>[!CAUTION]
>
>Adobe不打算進一步增強傳統UI。 AEM 6.5包含傳統UI，而從舊版升級的客戶可繼續依原樣使用。 傳統UI在被取代時仍完全支援。 [閱讀更多](/help/sites-deploying/ui-recommendations.md)。

#### 搜尋和索引 {#indexing-and-search}

* Oak中的搜尋現在支援動態Facet。 例如，資產搜尋中的篩選邊欄會顯示預估的結果數量。
* 已擴充QueryBuilder以提供具有動態Facet的結果。

#### 升級 {#upgrade}

* 執行AEM 6.2、6.3和6.4的客戶可支援直接就地升級至AEM 6.5。使用5.x或6.0/6.1的客戶若想使用就地升級，必須先升級至6.4。 然後，升級至6.5，或透過在執行個體之間直接將內容轉移到AEM 6.5的方式進行升級。
* 6.5中的升級程式大致相同。
* 我們持續支援6.4中推出的回溯相容性、升級複雜性評估及可持續升級功能。如有需要，這些區域已進行版本專屬更新。
* 模式偵測器封裝現已簡化。 有一個套件會針對可用的來源版本評估升級至6.5。
* 如需有關升級程式的詳細資訊，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。

#### 專案和工作流程 {#projects-and-workflows}

* 6.4中推出的新工作流程模型編輯器已改善，以包含更多作業，例如複製和發佈、工作流程步驟中的變數支援，以及增強的`OR`和`AND`分割。

#### 存放庫 {#repository}

* Adobe Experience Manager 6.5的基礎建置在OSGi型架構（Apache Sling和Apache Felix）和Java™內容存放庫： Apache Jackrabbit Oak 1.10.2的更新版本之上。
* 如需已修正問題的概觀，請參閱[Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)、[Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt)和[Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)。

>[!CAUTION]
>
>自AEM 6.3以來出現的新版Oak區段Tar需要存放庫移轉。 如果您要從舊版TarMK升級，或想從其他型別的持續性切換新的Segment Tar，則必須執行此步驟。 如需新的區段Tar優點詳細資訊，請參閱[移轉至Oak區段Tar常見問題集](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar)。

#### OSGI {#osgi}

* 新增OSGi Promise和Converter公用程式庫。

#### 安全性 {#security}

* 新增管理員使用者的密碼過期時間。

#### 網頁伺服器 {#web-server}

* 快速入門發行版本使用Eclipse Jetty 9.4.15作為servlet引擎(AEM 6.4隨9.3.22提供)。

### [!DNL Experience Manager]個網站 {#experience-manager-sites}

#### 受管理的單頁應用程式 {#managed-single-page-apps}

頁面編輯器新增了在使用者端轉譯體驗（也稱為[SPA編輯器](/help/sites-developing/spa-architecture.md)）中的內容編輯和撰寫/配置功能。 使用JavaScript框架React或Angular建置的現有單頁應用程式可透過AEM SJ SDK進行擴充，讓從業人員可編輯。

首次隨附AEM 6.4 SP2，搭配AEM 6.5的SPA支援將獲得下列功能：

* 使用範本編輯器來編輯及設定SPA的AEM可編輯部分
* 使用多網站管理建立國家/地區、特許經營或白色標籤的SPA體驗

#### Headless內容管理 {#headless-content-management}

AEM能以各種格式和從各種棧疊層級提供內容。 自2008年以來，已有部分產品使用[Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)和[POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)。 內容服務（[Sling模型匯出程式](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)）是在AEM 6.3中匯入的，是AEM SJ SDK用來合併單頁應用程式的方法。 適用於Assets[的](/help/assets/mac-api-assets.md)HTTP API是針對AEM 6.5擴充的CRUD API。

新HTTP API功能：

* 新增[內容片段支援至Assets](/help/assets/assets-api-content-fragments.md)的HTTP API，以建立、更新、讀取和刪除片段。
* 透過[內容片段清單核心元件](https://www.aemcomponents.dev)的內容服務公開內容片段清單。
* 顯示每個元件的預設Content Services JSON輸出的[核心元件庫](https://www.aemcomponents.dev)

#### Screens附加元件 {#screens-add-on}

有效率地設計、提供和最佳化所有數位顯示器（從互動式資訊站到數位看板）上的體驗。

* 透過改善內容重複使用，跨數位和店內整合體驗和內容
* 透過支援Launch簡化製作和核准/發佈工作流程
* 使用SPA編輯器編輯及提供豐富的互動式體驗
* 使用Launches規劃招牌內容的未來內容變更
* 循序頻道中計量的播放
* 使用來源檔案（例如Excel工作表）自動建立專案結構
* 透過強大的線上和離線作業(Smart Sync)擴充媒體播放器支援，甚至可擴充至最大的看板網路。
* 使用動態預留位置，依位置或資料觸發內容的設定進行個人化。
* Adobe Analytics整合至AEM Screens Player所驅動的統一深入分析

如需AEM Screens變更的詳細資訊，請參閱[AEM Screens使用手冊](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html)中的發行說明。

#### 元件與範本開發 {#component-amp-template-development}

* Maven專案原型18+如需新專案，請參閱[GitHub的發行說明](https://github.com/adobe/aem-project-archetype/releases)。
* 單頁應用程式Maven專案原型1.0.6+適用於新專案，請參閱[GitHub版本注意事項](https://github.com/adobe/aem-spa-project-archetype/releases)。
* HTL 1.4版，請參閱發行說明[GitHub ](https://github.com/adobe/htl-spec/releases/tag/1.4)。

   * 字串、陣列和物件的「in」運運算元：

     ```html
     ${'a' in 'abc'}
     ${100 in myArray}
     ${'a' in myObject}
     ```

   * 具有data-sly-set的變數宣告：
     `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 列出和重複控制引數：開始、步驟、結束：
     `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap的識別碼：

     ```html
     <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
     text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
     </div>
     ```

   * 支援負數

* 核心元件2.3.2+請參閱[GitHub版本注意事項](https://github.com/adobe/aem-core-wcm-components/releases)。
* 配置容器的格線系統，請參閱[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)。
* Clientlib Manager：將Google Closure Compiler預設為JavaScript clientlibs的縮制（舊預設為Yahoo YUI），並將Google Closure Compiler更新為v版20190121
* 範本編輯器和原則

   * 為使用JS SDK （也稱為SPA編輯器）的單頁應用程式建立和編輯範本

* 參考網站We.Retail 4.0，請參閱發行說明[GitHub ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)。
* 升級現有網站以使用最新編輯器功能的工具組，請參閱[GitHub存放庫](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM包含1.12.4版的jQuery程式庫，可提供與現有自訂程式碼的最大相容性。 Adobe已進行修改，以解決已知的安全性問題。

#### 網站管理 {#site-administration}

* [Reference](/help/sites-authoring/author-environment-tools.md#references)邊欄有新區段，列出指向所選頁面的內部連結。 在打算將頁面離線或刪除時，這項功能相當實用，可檢視哪些頁面需要在離線前進行調整。
* [清單檢視](/help/sites-authoring/basic-handling.md#list-view)有一個新的工作流程欄，當頁面在工作流程中時會顯示狀態。
* 在[頁面屬性](/help/sites-authoring/editing-page-properties.md)中，現在可以在指派縮圖至頁面時瀏覽現有資產（縮圖示籤）。

#### 頁面編輯器 {#page-editor}

* 允許使用JS SDK （也稱為SPA編輯器）的React和Angular使用者端元件建置單頁應用程式體驗的內容內編輯和組成
* 只有在頁面已設定支架頁面時，才會顯示「支架模式」。

#### 內容片段與編輯器 {#content-fragments-amp-editor}

* 在內容片段編輯器中新增[註解](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations)邊欄，以提供一般評論並檢視文字中所做的評論（也會顯示在時間軸邊欄中）
* 將[內容片段模式](/help/assets/content-fragments/content-fragments-models.md)中多行文字元素的預設內容型別設定為簡單文字、RTF或Markdown的功能
* 在RTE （全熒幕檢視）中選取文字，以新增[註解/註解](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [透過參考邊欄並排比較內容片段的版本](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)
* 資產下載報表現在會顯示相應的內容片段
* 透過/api.json新增[內容片段支援至Assets HTTP API](/help/assets/assets-api-content-fragments.md)。 有可用於建立、更新、讀取和刪除內容片段的API。

#### 體驗片段 {#experience-fragments}

* 已改善[體驗片段](/help/sites-authoring/experience-fragments.md)的索引，因此可在搜尋使用這些體驗片段的頁面中找到其內容。
* [匯出至Target](/help/sites-administering/experience-fragments-target.md)選項現在可讓您以JSON (預設為HTML)或兩者來傳送體驗片段。

#### 翻譯 {#translation}

* 使用主要專案簡化建立翻譯專案的流程。
* 將翻譯工作設定為預設的已核准狀態，以簡化執行翻譯專案。
* 允許使用第三方翻譯記憶庫中的變更來更新翻譯頁面。
* 允許匯出JSON格式的翻譯工作。
* 更新Microsoft®翻譯整合以使用V3 API。

#### 多網站管理(MSM) {#multi-site-management-msm}

* 對於使用PushOnModify的轉出設定，更妥善地處理頁面移動操作以避免不一致狀態。
* 根據預設，在LiveCopy結構內建立頁面會建立獨立頁面。
* 在使用JS SDK （也稱為SPA編輯器）的單頁應用程式中使用MSM功能

#### 啟動 {#launches}

* 新的啟動檢閱和核准工作流程，以及僅提升已核准啟動頁面的功能
* 在UI中新增[選項，以選擇在促銷活動步驟](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)後立即刪除啟動項

#### 內容目標定位與模擬 {#content-targeting-simulation}

* ContextHub資料層和使用者端規則引擎JavaScript已更新，預設為使用jQuery 3。

#### AEM和Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>目前：
>
>* 如果您在AEM的「活動」主控台中使用Adobe Target作為目標定位引擎，則僅支援`at.js 1.x`。
>
>* 如果您使用體驗片段匯出至Target並在Target主控台內執行活動，則同時支援`at.js. 1.x`和`at.js 2.x`。

* Adobe Target整合現在使用Target Standard API。 舊版AEM使用Target Classic HTTP API，此API現已棄用。
* 包含Adobe Target `mbox.js`版本63。 Adobe強烈建議您將實作切換至`at.js` v1.x。
* 現已包含`at.js`版本1.5.0。 Adobe建議您使用[Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html)將`at.js` v1.x布建至網站。

#### AEM和Adobe Analytics {#aem-amp-adobe-analytics}

* 已包含`s_code.js` H.27.5。 Adobe建議您切換實作至`AppMeasurement.js`
* 已包含`AppMeasurement.js` v1.8.0。 Adobe建議您使用[Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html)將AppMeasurement.js布建至網站。

#### AEM和Commerce {#aem-commerce}

Commerce integration framework的改良功能發行週期比AEM 6.4更快。使用Commerce integration framework[從](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html)AEM和Adobe Commerce整合瞭解更多資訊。

#### Communities附加元件 {#communities-add-on}

若要取得最新版本，請參閱檔案的[部署Communities](/help/communities/deploy-communities.md)區段。

##### 社群參與增強功能 {#enhancements-to-community-engagement}

**@Mentions支援**
AEM Communities現在可讓註冊使用者在使用者產生的內容中標籤（提及）其他註冊會員，以吸引他們的注意。 接著會通知已標籤（已提及）的成員，並包含對應之使用者產生內容的深層連結。 但是，使用者可以選擇停用/啟用網頁和電子郵件通知。

![At提及支援](/help/release-notes/assets/at-mentions.png)

社群使用者不需要搜尋其名字、姓氏或使用者名稱，即可檢視是否有任何使用者聯絡過他們或需要他們注意。 此外，它可讓UGC作者向最能解決問題並新增輸入內容的特定註冊使用者尋求回應。

社群管理員需要在社群元件上&#x200B;**啟用提及功能**，才能讓註冊的使用者使用這些元件的功能。

**群組訊息**

註冊的社群成員現在可以透過單一電子郵件組合將直接訊息大量傳送給群組，而不是個別將相同的訊息傳送給群組成員。 若要允許[群組傳訊](/help/communities/configure-messaging.md)，請同時啟用[傳訊操作服務](/help/communities/messaging.md#group-messaging)的執行個體。

![群組訊息](/help/release-notes/assets/group-messaging.png)

##### 大量仲裁的增強功能 {#enhancements-to-bulk-moderation}

大量稽核中的自訂篩選器

[現在可以開發自訂篩選器](/help/communities/moderation.md#custom-filters)並新增到大量仲裁UI。

在[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)中有示範篩選標籤的[範例專案](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)可供使用。 此專案可作為開發類似自訂篩選器的基礎。

![自訂篩選器](/help/release-notes/assets/custom-tag-filter.png)

**大量稽核中的清單檢視**

具有已改良UI的新清單檢視已提供大量仲裁，以顯示使用者產生的內容專案。

![在清單檢視中進行大量仲裁](/help/release-notes/assets/list-view-moderation.png)

##### 網站與群組管理的增強功能 {#enhancements-to-site-and-group-management}

**作者端網站與群組管理員**

Communities (從AEM 6.5開始)允許分散管理（和管理）不同的社群網站和群組/巢狀群組。 託管多個社群網站和巢狀群組的組織現在可以在建立網站（和群組）時，在作者端選取管理員角色的成員。

![網站管理員](/help/release-notes/assets/site-admin.png)

場地管理員可以在任何階層建立群組，並成為預設管理員。 這些管理員稍後可由其他群組管理員移除。 群組管理員可以管理群組G1，並在G1下建立巢狀的子群組。

##### 啟用的增強功能 {#enhancements-to-enablement}

**SCORM 2017.1支援**

AEM 6.5 Communities的啟用功能支援可共用的內容物件參考模型[ (SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/)引擎。

* 啟用元件的鍵盤導覽支援
* AEM Communities中的啟用元件（例如目錄和課程播放、指派、檔案庫）可支援鍵盤導覽，以提升協助工具。

##### 其他增強功能 {#other-enhancements}

* Solr 7支援
* 設定MSRP和DSRP時，AEM 6.5社群可支援Apache Solr 7.0版本的搜尋平台。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5引進以下功能和增強功能，以提高AEM使用者、DAM角色和相關創意和行銷角色的生產力。

#### 與[!DNL Adobe Creative Cloud]和創意工作流程整合 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager]提供多種方法來與[!DNL Adobe Creative Cloud]整合及共用資產，以用於創意和行銷或業務團隊密切合作的工作流程。 [!DNL Experience Manager] 6.5持續改善整合，並進一步簡化整合，以發掘更多商機並簡化現有方法。

請閱讀下文，瞭解您可用來最有效支援您的Content Velocity使用案例的[!DNL Experience Manager] 6.5的特定功能和整合。

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link]在內容建立過程中加強創意人員與行銷人員之間的協同合作。 創意人員可以存取儲存在[!DNL Experience Manager Assets]中的內容，無需離開他們最熟悉的應用程式。 創意人員可以使用[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]和[!DNL Adobe InDesign]應用程式中的應用程式內面板，順暢地瀏覽、搜尋、簽出和簽入資產。

[!DNL Adobe Asset Link]是適用於企業的[Creative Cloud](https://www.adobe.com/tw/creativecloud/business/enterprise.html)產品的一部分。 如需詳細資訊，包括[!DNL Experience Manager]部署的必要設定，請參閱[Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)。

![在Adobe Photoshop中搜尋資產](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock]整合 {#stock}

您的組織可以在[!DNL Adobe Stock]內使用其[!DNL Experience Manager Assets]企業計畫，以確保您的創意和行銷專案可廣泛使用授權資產。 您可以使用[!DNL Adobe Stock]的強大DAM功能，快速尋找、預覽及授權Experience Manager中儲存的[!DNL Experience Manager]資產。

[!DNL Adobe Stock]服務可讓設計師和企業存取數百萬張高品質、精選且免版稅的像片、向量、插圖、影片、範本和3D資產，以供其所有創意專案使用。

如需詳細資訊，請參閱[在Experience Manager Assets中使用Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md)。

從Experience Manager Assets![預覽Adobe Stock影像和授權](/help/release-notes/assets/stock_image_preview_license_options.png)

*圖：從[!DNL Adobe Stock]預覽[!DNL Experience Manager Assets]影像和授權。*

![在Experience Manager中搜尋及篩選授權的Adobe Stock影像](/help/release-notes/assets/aem-search-filters2.jpg)

*圖：搜尋並篩選[!DNL Adobe Stock].[!DNL Experience Manager]中授權的*&#x200B;影像

##### [!DNL Adobe InDesign]中的動態參考 {#dynamic-references-in-indesign}

在[!DNL Experience Manager Assets]個檔案中使用的[!DNL Adobe InDesign]是動態的。 如果參照的資產在存放庫中移動，參照會自動更新。 如需詳細資訊，請參閱[如何管理複合資產](/help/assets/managing-linked-subassets.md)。

#### Brand Portal功能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal]可協助您輕鬆取得、有效控制並安全地散佈核准的資產，給跨裝置的外部廠商/代理商及內部業務使用者。 它有助於提高資產共用的效率、加快資產上市時間，並消除不合規使用和未經授權存取的風險。

如需詳細資訊，請參閱[Brand Portal的新功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html)。

#### 已連線資產 {#connectedassets}

在大型企業中，可以分發建立網站所需的基礎架構。 有時，網站建立功能和所需的數位資產位於不同的獨立單位。

[!DNL Experience Manager Sites]提供建立網頁的功能，[!DNL Experience Manager Assets]是提供網站所需資產的數位資產管理(DAM)系統。 [!DNL Experience Manager]現在整合[!DNL Sites]和[!DNL Assets]，以支援上述使用案例。 請參閱[如何設定及使用連線Assets功能](/help/assets/use-assets-across-connected-assets-instances.md)。

![從其他[!DNL Experience Manager]部署的[!DNL Sites]頁面上的[!DNL Experience Manager]部署拖曳資產](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*圖：從其他[!DNL Experience Manager]部署上的[!DNL Sites]頁面上的[!DNL Experience Manager]部署拖曳資產。*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media]在[!DNL Experience Manager Assets]中提供增強的豐富媒體製作與傳遞，以推動具沈浸式與個人化的尖端體驗。 透過上傳單一高品質的主要資產，並使用Adobe的進階雲端轉譯和檢視器，您可以即時提供轉譯的任何組合，以支援組織的媒體策略。

如需新[!DNL Dynamic Media]功能的詳細資訊，請參閱[Dynamic Media發行說明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html)。

##### 360視訊支援 {#video-support}

使用先進的檢視器，直接在[!DNL Experience Manager]中管理您的360視訊檔案，為桌上型電腦、行動裝置和VR耳機提供VR體驗。 如需詳細資訊，請參閱[使用360視訊](/help/assets/360-video.md)。

##### 自訂影片縮圖 {#custom-video-thumbnails}

您現在可以使用視訊本身的影格或儲存在DAM中的其他內容，來自訂視訊資產的縮圖。 如需其他指示，請參閱[關於視訊縮圖](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)。

##### 協助工具增強功能 {#accessibility-enhancements}

[!DNL Dynamic Media]檢視器現在支援增強的協助工具功能，例如Aria支援、熒幕閱讀程式和Alt文字。 如需詳細資訊，請參閱[檢視者參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html)。

#### 搜尋體驗增強功能 {#experience-enhancement-for-searching}

從[!DNL Experience Manager] 6.5開始，行銷人員可以從搜尋結果頁面更快找到所需資產。 甚至在套用搜尋篩選條件之前，搜尋Facet就會以資產數量更新。 檢視篩選的預期計數，有助於使用者有效瀏覽搜尋結果。 如需詳細資訊，請參閱[在Experience Manager中搜尋資產](/help/assets/search-assets.md)。

![檢視搜尋Facet中未篩選搜尋結果的資產數目](/help/assets/assets/asset_search_results_in_facets_filters.png)

*圖：檢視搜尋Facet中未篩選搜尋結果的資產數量。*

#### 可用性增強功能 {#usability-enhancement}

您現在可以選取資料夾中的所有已載入資產，或一次從搜尋結果中選取資產。 它有助於您快速管理多個資產。 核取方塊會選取所有符合情境的資產，例如搜尋結果，而不僅僅是[!DNL Experience Manager]介面中顯示的資產。

![使用「全選」選項，按一下即可選取所有載入的資產。](/help/release-notes/assets/select-all-in-aem-assets.gif)

*圖：使用[全選]選項只要按一下即可選取所有載入的資產。*

#### 中繼資料增強功能 {#metadata-enhancements}

[!DNL Assets]可讓您建立資產資料夾的中繼資料結構，定義資料夾屬性頁面中顯示的版面和中繼資料。 您現在可以將資料夾中繼資料結構指派給現有資料夾，或是在建立資料夾時。 如需詳細資訊，請參閱[資料夾中繼資料結構描述](/help/assets/metadata-config.md#folder-metadata-schema)。

指定階層式中繼資料時，可在執行階段從JSON檔案載入選項，而不是在表單中手動輸入。 如需詳細資訊，請參閱[階層式中繼資料](/help/assets/metadata-schemas.md#cascading-metadata)。

#### 報告增強功能 {#reporting-enhancements}

內容片段和連結共用現在包含在下載的報表中。 如需詳細資訊，請參閱[Assets報表](/help/assets/asset-reports.md)。

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms提供數項新功能和增強功能。 重點包括：

* 追蹤已提交表單、已處理檔案和已轉譯檔案數量的交易報表
* 互動式通訊的可用性改善
* 調適型表單中的雲端數位簽名
* 將調適型表單和互動式通訊內嵌到AEM Sites單頁應用程式(SPA)中。
* 支援AEM工作流程中的變數
* 互動式通訊中的資料顯示模式支援
* 排序最適化表單和互動式通訊表格
* 自動驗證表單資料模型中的輸入資料

請參閱[AEM 6.5 Forms中的新功能和增強功能摘要](/help/forms/using/whats-new.md)，以取得有關新功能和改進功能及檔案資源的資訊。

### 使用以客戶為中心的開發 {#use-customer-focused-development}

Adobe使用以客戶為中心的開發模型，允許客戶在規格、開發和測試期間對開發流程的所有階段作出貢獻。 在此感謝所有貢獻的客戶和合作夥伴。

Adobe已具備程式和流程，可讓您收集、區分優先順序和追蹤以客戶為中心的錯誤解決和增強功能請求開發。 [Experience Manager支援入口網站](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support)已與Adobe增強功能與瑕疵追蹤系統整合。 客戶支援團隊會儘可能找出客戶問題並加以解決。 當升級至研發時，會擷取所有客戶資訊，並用於優先順序和報告。 在開發中，會優先處理付費支援、保證問題和客戶付費的增強功能。

此優先順序處理程式產生超過750項在AEM 6.5中修正的以客戶為中心的變更。

## 屬於發行版本一部分的檔案清單 {#list-of-files-that-are-part-of-the-release}

**Foundation**

* 獨立快速入門： `cq-quickstart-6.5.0.jar`。
* 應用程式伺服器快速入門： `cq-quickstart-6.5.0.war`。
* 適用於各種Web伺服器和平台的Dispatcher 4.3.2或更新版本。 檢視[下載連結](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Eclipse IDE的外掛程式（[閱讀更多資訊並下載](/help/sites-developing/aem-eclipse.md)）

* Brackets程式碼編輯器的延伸模組（[閱讀更多資訊並下載](/help/sites-developing/aem-brackets.md)）
* Maven/Gradle相依性（[下載連結](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/)）

**Sites**

* 核心元件（[GitHub專案](https://github.com/adobe/aem-core-wcm-components)）
* We.Retail參考實作（[瞭解詳情](/help/sites-developing/we-retail.md)）
* Maven專案原型：

   * 完整棧疊網站： [GitHub專案](https://github.com/adobe/aem-project-archetype)
   * 若為具有React/Angular的單頁應用程式： [GitHub專案](https://github.com/adobe/aem-spa-project-archetype)

* 適用於各種目標平台的AEM Screens Player （[下載](https://download.macromedia.com/screens/)）

* 智慧內容語言模型。 已預先安裝英文 — 可以下載更多語言

   * [德文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [義大利文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法文](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM現代化工具套裝，例如對話方塊轉換工具。 （[GitHub專案](https://github.com/adobe/aem-modernize-tools)）

**資產**

* 封裝以新增增強型PDF模擬轉譯器（[瞭解詳情](/help/assets/aem-pdf-rasterizer.md)）
* 新增延伸RAW影像支援的封裝（[瞭解詳情](/help/assets/camera-raw.md)）

**表單**

* 用於AEM Forms功能的[封裝](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Forms OSGi使用者端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 語言 {#languages}

使用者介面提供下列語言版本：

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

[!DNL Experience Manager] 6.5已通過GB18030-2005 CITS使用中文編碼標準的認證。

## 安裝與更新 {#install-update}

如需設定需求，請參閱[安裝指示](/help/sites-deploying/custom-standalone-install.md)。

如需詳細指示，請參閱[升級檔案](/help/sites-deploying/upgrade.md)。

## 受支援平台 {#supported-platforms}

尋找支援平台的完整矩陣，包括[AEM 6.5技術需求](/help/sites-deploying/technical-requirements.md)的支援層級。

>[!NOTE]
>
>Oracle已改用Oracle Java™ SE產品的長期支援(LTS)模型。 Java™ 9和10是Oracle的非LTS版本。 請參閱[Oracle Java™ SE支援藍圖](https://www.oracle.com/technetwork/java/eol-135779.html)。 Adobe支援LTS版本的Java™，僅能在生產環境中執行AEM。 AEM 6.5建議使用Java™ 11版本。

## 已棄用和移除的功能 {#deprecated-and-removed-features}

Adobe會持續評估產品功能，不斷使用更強大的版本進行替換，也可能決定重新推出部分元件，以滿足未來期望或外掛程式。

若為[!DNL Adobe Experience Manager] 6.5，[請閱讀已過時和已移除功能的清單](/help/release-notes/deprecated-removed-features.md)。 此頁面也包含未來變更的預先公告，以及適用於先前版本更新之客戶的重要通知。

## 已知問題 {#known-issues}

### Platform {#platform}

* 已報告刪除CRX-Quickstart及其內容的問題。

  在這些動作中，確定屬性`htmllibmanager.fileSystemOutputCacheLocation`不是空字串：

   1. 正在呼叫`/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`。
   2. 升級至AEM 6.5。
   3. 在AEM 6.5上執行「延遲內容移轉」。

* 如果您搭配使用JDK 11與AEM 6.5執行個體，部署部分套件後，部分頁面可能會顯示為空白。 記錄檔中會顯示下列錯誤訊息：

  ```java
  *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
  java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
  ```

若要解決此錯誤：

1. 停止AEM執行個體。 移至`<aem_server_path_on_server>crx-quickstart\conf`並開啟`sling.properties`檔案。 Adobe建議對此檔案進行備份。

1. 搜尋`org.osgi.framework.bootdelegation=`。 新增`jdk.internal.reflect,jdk.internal.reflect.*`屬性以顯示結果為。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 儲存檔案並重新啟動AEM執行個體。

### Sites {#sites}

* **使用頁面版本**： [如果頁面已移動，您將無法再對移動前所做的任何版本執行預覽](/help/sites-authoring/working-with-page-versions.md#previewing-a-version)。

### Assets {#assets}

* **搜尋：**&#x200B;如果搜尋字串包含前置空格([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))，則搜尋不會傳回任何內容
* **資料夾中繼資料結構描述**：新增選擇按鈕後，ID和Value欄位未如預期般呈現，且刪除功能無法運作。 (CQ-4261144)
* 重新命名資產時，資產名稱中不可使用空白字元。 (CQ-4266403)

### Forms {#forms}

* 在Linux®作業系統上安裝AEM Forms時，使用硬體安全性模組的數位簽名無法運作。 (CQ-4266721)
* (僅適用於WebSphere上的AEM Forms®)如果您搜尋以&#x200B;**使用者名稱**&#x200B;作為搜尋條件的&#x200B;**管理員**，則&#x200B;**Forms Workflow** > **任務搜尋**&#x200B;選項不會傳回任何結果。 (CQ-4266457)

* AEM Forms無法將使用JPEG壓縮的TIF和TIFF檔案轉換為PDF檔案。 (CQ-4265972)
* **AEM Forms Assets掃描器**&#x200B;和&#x200B;**Letter to Interactive Communication移轉**&#x200B;選項在&#x200B;**AEM Forms移轉**&#x200B;頁面上無法運作。 (CQ-4266572)

* (僅適用於JBoss® 7)當您從舊版升級至AEM 6.5 Forms，且舊版具有建立並使用預設提交或預設轉譯程式副本的程式(.lca)時，使用這類程式(.lca)的HTML5 Forms無法執行所需動作。 (CQ-4243928)
* 在調適型來源中，從規則編輯器叫用表單資料模型服務以動態更新影像選擇元件值時，不會更新影像選擇元件的值。 (CQ-4254754)
* AEM Forms Designer安裝程式需要32位元版本的[Visual C++可轉散發執行階段套件2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170)和[Visual C++可轉散發執行階段套件2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1)。 在開始安裝之前，請確定已安裝前述的可轉散發執行階段套件。 (CQ-4265668)

* PDF Generator不支援智慧卡式驗證。 當管理員在Windows伺服器上啟用群組原則`Interactive Logon: Require Smart card`時，所有現有的PDF Generator使用者都會失效。

* 當調適型表單設定為動態更新元件值，且透過Dispatcher存取託管表單的發佈執行個體時，動態更新欄位值的功能會停止運作。 若要解決此問題，請在發佈執行個體上，開啟CRXDE，導覽至`/libs/fd/af/runtime/clientlibs/guideChartReducer`，然後建立下列屬性。

   * 名稱： allowProxy
   * 型別：布林值
   * 值： true
   * Protected： False
   * 必要： False
   * 多個：False
   * 自動建立： False

  屬性可讓執行階段資料夾下的使用者端程式庫存取代理。 (CQ-4268679)

* AEM Forms啟動時，會出現`SAX Security Manager could not be setup`警告。
* 當您在執行20.10.00版Adobe Acrobat Reader的Apple iOS或iPadOS上開啟受AEM Forms Document Security保護的PDF時
* 從 Apple iOS 裝置提交包含標準 HTML 上傳欄位的表單時，有時不會傳送檔案內容並在另一端收到 0 位元組檔案。Apple iOS 15.1 提供此問題的修正。

## 產品下載與支援（受限制的網站） {#product-download-and-support-restricted-sites}

以下網站僅供客戶使用。 若您是客戶並且需要存取權，請聯絡您的 Adobe 客戶經理。

* [產品下載位於licensing.adobe.com](https://licensing.adobe.com/)。

* [軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上其他功能的產品更新、修補程式及套件。

* 透過Admin Console[客戶支援](https://adminconsole.adobe.com/)。 如需詳細資訊，請參閱[新的Adobe客戶支援體驗](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。
