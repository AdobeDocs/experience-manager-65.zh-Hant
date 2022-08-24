---
title: 效能指南
seo-title: Performance Guidelines
description: 本文提供有關如何優化部署效能的一般指AEM南。
seo-description: This article provides general guidelines on how to optimize the performance of your AEM deployment.
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
feature: Configuring
exl-id: 5a305a5b-0c3d-413b-88c1-1f5abf7e1579
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2976'
ht-degree: 5%

---

# 效能指南{#performance-guidelines}

此頁提供有關如何優化部署效能的一般指AEM南。 如果您是新入職者AEM，請先瀏覽以下頁面，然後再開始閱讀效能指南：

* [基AEM本概念](/help/sites-deploying/deploy.md#basic-concepts)
* [儲存概AEM述](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [技術要求](/help/sites-deploying/technical-requirements.md)

下面所示為可用的部署選AEM項（滾動以查看所有選項）:

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>產品</strong></p> </td>
   <td><p><strong>拓撲</strong></p> </td>
   <td><p><strong>作業系統</strong></p> </td>
   <td><p><strong>應用程式伺服器</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>安全性</strong></p> </td>
   <td><p><strong>微內核</strong></p> </td>
   <td><p><strong>資料儲存</strong></p> </td>
   <td><p><strong>索引</strong></p> </td>
   <td><p><strong>網頁伺服器</strong></p> </td>
   <td><p><strong>瀏覽器</strong></p> </td>
   <td><p><strong>Marketing Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>非HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>塔爾</p> </td>
   <td><p>區段</p> </td>
   <td><p>屬性</p> </td>
   <td><p>Apache</p> </td>
   <td><p>邊緣</p> </td>
   <td><p>目標</p> </td>
  </tr>
  <tr>
   <td><p>Assets</p> </td>
   <td><p>發佈 — HA</p> </td>
   <td><p>Solaris</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM</p> </td>
   <td><p>SAML</p> </td>
   <td><p>蒙戈DB</p> </td>
   <td><p>檔案</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>分析</p> </td>
  </tr>
  <tr>
   <td><p>社群</p> </td>
   <td><p>作者 — CS</p> </td>
   <td><p>紅帽</p> </td>
   <td><p>WebSphere</p> </td>
   <td><p>惠普</p> </td>
   <td><p>奧奧特</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>火狐</p> </td>
   <td><p>行銷活動</p> </td>
  </tr>
  <tr>
   <td><p>Forms</p> </td>
   <td><p>作者卸載</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>雄貓</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>蒙戈DB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>鉻</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>行動</p> </td>
   <td><p>作者群集</p> </td>
   <td><p>IBM艾克斯</p> </td>
   <td><p>JBoss</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>薩法里</p> </td>
   <td><p>對象</p> </td>
  </tr>
  <tr>
   <td><p>多站點</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>資產</p> </td>
  </tr>
  <tr>
   <td><p>商務</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>AppleOS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>啟動</p> </td>
  </tr>
  <tr>
   <td><p>Dynamic Media</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>行動</p> </td>
  </tr>
  <tr>
   <td><p>Brand Portal</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>奧德</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>利夫爾</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>畫面</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>文檔安全性</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>流程管理</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>桌面應用程式</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>業績指引主要適用於AEM Sites。

## 何時使用效能指南 {#when-to-use-the-performance-guidelines}

在以下情況下，應使用效能指南：

* **首次部署**:在首次計畫部署AEM Sites或資產時，瞭解配置微內核、節點儲存和資料儲存時可用的選項（與預設設定相比）非常重要。 例如，將TarMK的資料儲存的預設設定更改為檔案資料儲存。
* **升級到新版本**:升級到新版本時，瞭解與運行環境相比的效能差異非常重要。 例如，從AEM6.1升級到6.2，或AEM從6.0 CRX2升級到6.2 OAK。
* **響應時間慢**:當選定的Nodestore體系結構不滿足您的要求時，瞭解與其他拓撲選項相比的效能差異非常重要。 例如，部署TarMK而不是MongoMK，或使用檔案資料儲存而不是AmazonS3或MicrosoftAzure資料儲存。
* **添加更多作者**:當推薦的TarMK拓撲不滿足效能要求且Author節點的升級已達到可用的最大容量時，瞭解與使用MongoMK和三個或更多Author節點相比的效能差異非常重要。 例如，部署MongoMK而不是TarMK。
* **添加更多內容**:當建議的資料儲存體系結構不滿足您的要求時，瞭解與其他資料儲存選項相比的效能差異非常重要。 示例：使用AmazonS3或MicrosoftAzure資料儲存而不是檔案資料儲存。

## 簡介 {#introduction}

本章概括介紹了體系結構AEM及其最重要的元件。 它還提供了開發指南，並描述了TarMK和MongoMK基準test中使用的測試方案。

### 平台AEM {#the-aem-platform}

平AEM台由以下元件組成：

![chlimage_1](assets/chlimage_1a.png)

有關平台的詳細信AEM息，請參見 [什AEM麼](/help/sites-deploying/deploy.md#what-is-aem)。

### 建築AEM {#the-aem-architecture}

部署有三個重要的構AEM成塊。 的 **作者實例** 內容作者、編輯器和批准者用於建立和審閱內容。 當內容被批准時，它將發佈到名為 **發佈實例** 從最終用戶訪問該檔案的位置。 第三塊建築是 **調度程式** 它是一個模組，用於處理快取和URL過濾，並安裝在webserver上。 有關體系結構的其AEM他資訊，請參見 [典型部署方案](/help/sites-deploying/deploy.md#typical-deployment-scenarios)。

![chlimage_1-1](assets/chlimage_1-1a.png)

### 微核 {#micro-kernels}

Micro Kernels充當中的持久性管理AEM器。 使用的微內核有三種類型AEM:TarMK、MongoDB和關係資料庫（受限制支援）。 根據實例的用途和您考慮的部署類型來選擇適合您需要的部署類型。 有關微內核的其他資訊，請參見 [建議的部署](/help/sites-deploying/recommended-deploys.md) 的子菜單。

![chlimage_1-2](assets/chlimage_1-2a.png)

### 諾德斯托雷 {#nodestore}

在中AEM，二進位資料可以獨立於內容節點儲存。 儲存二進位資料的位置稱為 **資料儲存**，而內容節點和屬性的位置稱為 **節點儲存**。

>[!NOTE]
>
>Adobe建議將TarMK作為客戶為AEM作者和發佈實例使用的預設持久性技術。

>[!CAUTION]
>
>關係資料庫微內核受到限制支援。 聯繫人 [Adobe客戶關懷](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html) 之後再使用此類型的微內核。

![chlimage_1-3](assets/chlimage_1-3a.png)

### 資料儲存 {#data-store}

在處理大量二進位檔案時，建議使用外部資料儲存而不是預設節點儲存，以最大化效能。 例如，如果您的項目需要大量媒體資產，則將它們儲存在檔案或Azure/S3資料儲存下將使訪問這些資產比直接儲存在MongoDB中更快。

有關可用配置選項的詳細資訊，請參見 [配置節點和資料儲存](/help/sites-deploying/data-store-config.md)。

>[!NOTE]
>
>Adobe建議選擇在AEMAzure或Amazon Web Services(AWS)上使用Adobe托管服務部署的選項，客戶將從具備在這些雲計算環境中部署和操作的經驗和AEM技能的團隊中獲益。 請看我們的 [有關Adobe Managed Services的其他文檔](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)。
>
>有關如何在AEMAzure或AWS上部署（在Adobe托管服務之外）的建議，我們強烈建議直接與雲提供商或我們的合作夥伴之一合作，支援在您選擇的雲環境AEM中部署。 選定的雲提供商或合作夥伴負責規模規格、設計和實施他們將支援的體系結構，以滿足您的特定效能、負載、可擴充性和安全性要求。
>
>有關其他詳細資訊，另請參見 [技術要求](/help/sites-deploying/technical-requirements.md#supported-platforms) 的子菜單。

### 搜尋 {#search-features}

本節列出的是與一起使用的自定義索引提供AEM程式。 要瞭解有關索引的更多資訊，請參見 [Oak查詢和索引](/help/sites-deploying/queries-and-indexing.md)。

>[!NOTE]
>
>對於大多數部署，Adobe建議使用Lucene索引。 您應僅將Solr用於專業化和複雜部署中的可擴充性。

![chlimage-1-4](assets/chlimage_1-4a.png)

### 開發指導方針 {#development-guidelines}

你應該為AEM了 **效能和可擴充性**。 下面介紹了一些最佳實踐，您可以遵循這些實踐：

**執行**

* 應用演示、邏輯和內容的分離
* 使用現AEM有API(例如：吊具)和工具(例如：複製)
* 根據實際內容進行開發
* 開發最佳可快取性
* 最大限度地減少儲存數(例如：使用臨時工作流)
* 確保所有HTTP端點都為REST風格
* 限制JCR觀測範圍
* 注意非同步線程

**不要**

* 如果可以，請不要直接使用JCR API
* 不更改/libs，而是使用重疊
* 不要盡可能使用查詢
* 不要使用Sling綁定在Java代碼中獲取OSGi服務，而是使用：

   * @Reference在DS元件中
   * @Inject吊具
   * sling.getService()，在輕巧使用類中
   * sling.getService()在JSP中
   * 服務跟蹤器
   * 直接訪問OSGi服務註冊表

有關開發的詳細信AEM息，請閱讀 [開發 — 基本](/help/sites-developing/the-basics.md)。 有關其他最佳做法，請參見 [開發最佳做法](/help/sites-developing/best-practices.md)。

### 基準方案 {#benchmark-scenarios}

>[!NOTE]
>
>此頁上顯示的所有基準test都已在實驗室設定中執行。

下面詳述的測試方案用於TarMK、MongoMk和TarMK與MongoMk章節的基準部分。 要查看特定基準test使用的方案，請閱讀 [技術規格](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark) 的子菜單。

**單一產品方案**

AEM Assets:

* 用戶交互：瀏覽資產/搜索資產/下載資產/讀取資產元資料/更新資產元資料/上載資產/運行上載資產工作流
* 執行模式：併發用戶，每個用戶一次交互

**混合產品方案**

AEM Sites+資產：

* 站點用戶交互：閱讀文章頁/閱讀頁/建立段落/編輯段落/建立內容頁/激活內容頁/作者搜索
* 資產用戶交互：瀏覽資產/搜索資產/下載資產/讀取資產元資料/更新資產元資料/上載資產/運行上載資產工作流
* 執行模式：併發用戶，每個用戶混合交互

**垂直用例方案**

媒體:

* 閱讀文章頁(27.4%)、閱讀頁(10.9%)、建立會話(2.6%)、激活內容頁(1.7%)、建立內容頁(0.4%)、建立段落(4.3%)、編輯段落(0.9%)、影像元件(0.9%)、瀏覽資產(20%)、讀取資產元資料(8.5%)、下載資產(4.2%)、搜索資產(0.2%)、更新資產元資料(2.4%)、上載資產(1.2%)、瀏覽項目(4.9%)、讀取項目(6.6%)、項目添加資產(1.2%)%)、項目添加站點(1.2%)、建立項目(0.1%)、作者搜索(0.4%)
* 執行模式：併發用戶，每個用戶混合交互

## TarMK {#tarmk}

本章提供TarMK的一般效能指南，指定最低體系結構要求和設定配置。 基準test亦已提供以作進一步澄清。

Adobe建議將TarMK作為所有部署方案中客戶使用的預設持久性技術，適用於AEM作者和發佈實例。

有關TarMK的詳細資訊，請參見 [部署方案](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 和 [焦油儲存](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage)。

### TarMK最低體系結構指南 {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>下面介紹的最低體系結構指南針對生產環境和高流量站點。 這些 **不** 這樣 [最小規格](/help/sites-deploying/technical-requirements.md#prerequisites) 需要AEM。

要在使用TarMK時建立良好的效能，您應從以下體系結構開始：

* 一個作者實例
* 兩個發佈實例
* 兩個調度程式

下面是站點和AEM AssetsAEM的架構指南。

>[!NOTE]
>
>應轉換無二進位複製 **開啟** 檔案資料儲存區。

**《AEM SitesTar體系結構指南》**

![chlimage-1-5](assets/chlimage_1-5a.png)

**《AEM AssetsTar體系結構指南》**

![chlimage-1-6](assets/chlimage_1-6a.png)

### TarMK設定指南 {#tarmk-settings-guideline}

為獲得良好效能，您應遵循下面介紹的設定准則。 有關如何更改設定的說明， [查看此頁](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

<table>
 <tbody>
  <tr>
   <td><strong>設定</strong></td>
   <td><strong>參數</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>Sling作業隊列</td>
   <td><code>queue.maxparallel</code></td>
   <td>將值設定為CPU內核數的一半。 </td>
   <td>預設情況下，每個作業隊列的併發線程數等於CPU核心數。</td>
  </tr>
  <tr>
   <td>花崗岩瞬態工作流隊列</td>
   <td><code>Max Parallel</code></td>
   <td>將值設定為CPU內核數的一半</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM參數</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> </td>
   <td>在啟動指令碼中添加這AEM些JVM參數，以防止擴展查詢使系統過載。</td>
  </tr>
  <tr>
   <td>Lucene索引配置</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>已啟用</p> <p>已啟用</p> <p>已啟用</p> </td>
   <td>有關可用參數的詳細資訊，請參閱 <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">此頁</a>。</td>
  </tr>
  <tr>
   <td>資料儲存= S3資料儲存</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576(1MB)或更小</p> <p>最大堆大小的2-10%</p> </td>
   <td>另請參閱 <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">資料儲存配置</a>。</td>
  </tr>
  <tr>
   <td>DAM更新資產工作流</td>
   <td><code>Transient Workflow</code></td>
   <td>已勾選</td>
   <td>此工作流管理資產的更新。</td>
  </tr>
  <tr>
   <td>DAM元資料寫回</td>
   <td><code>Transient Workflow</code></td>
   <td>已勾選</td>
   <td>此工作流XMP管理對原始二進位檔案的回寫，並在JCR中設定上次修改日期。</td>
  </tr>
 </tbody>
</table>

### TarMK效能基準 {#tarmk-performance-benchmark}

#### 技術規格 {#technical-specifications}

基準test是按以下規格執行的：

|  | **作者節點** |
|---|---|
| 伺服器 | 裸機硬體(HP) |
| 作業系統 | RedHat Linux |
| CPU/內核 | 英特爾(R)至強(R)CPU E5-2407 @2.40GHz,8核 |
| RAM | 32 GB |
| 磁碟 | 磁性 |
| Java | OracleJRE 8版 |
| JVM堆 | 16 GB |
| 產品 | AEM 6.2 |
| 諾德斯托雷 | TarMK |
| 資料儲存 | 檔案DS |
| 方案 | 單一產品：資產/30個併發線程 |

#### 效能基準結果 {#performance-benchmark-results}

>[!NOTE]
>
>下面顯示的數字已標準化為1作為基線，而不是實際吞吐量數字。

![chlimage-1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## 蒙戈MK {#mongomk}

選擇MongoMK持久性後端(TarMK)的主要原因是橫向縮放實例。 這意味著有兩個或兩個以上活動的作者實例始終運行，並將MongoDB用作持久性儲存系統。 需要運行多個作者實例通常是因為單個伺服器的CPU和記憶體容量（支援所有併發創作活動）不再可持續。

有關TarMK的詳細資訊，請參見 [部署方案](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 和 [Mongo儲存](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage)。

### MongoMK最低體系結構指南 {#mongomk-minimum-architecture-guidelines}

要在使用MongoMK時建立良好的效能，您應從以下體系結構開始：

* 三個作者實例
* 兩個發佈實例
* 三個MongoDB實例
* 兩個調度程式

>[!NOTE]
>
>在生產環境中， MongoDB將始終用作具有主節點和兩個輔助節點的複製副本集。 讀取和寫入操作將轉至主資料庫，讀取操作可轉至輔助資料庫。 如果儲存不可用，可以將其中一個輔助節點替換為仲裁伺服器，但MongoDB複製副本集必須始終由奇數個實例組成。

>[!NOTE]
>
>應轉換無二進位複製 **開啟** 檔案資料儲存區。

![chlimage-1-9](assets/chlimage_1-9a.png)

### MongoMK設定准則 {#mongomk-settings-guidelines}

為獲得良好效能，您應遵循下面介紹的設定准則。 有關如何更改設定的說明， [查看此頁](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

<table>
 <tbody>
  <tr>
   <td><strong>設定</strong></td>
   <td><strong>參數</strong></td>
   <td><strong>值（預設值）</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>Sling作業隊列</td>
   <td><code>queue.maxparallel</code></td>
   <td>將值設定為CPU內核數的一半。 </td>
   <td>預設情況下，每個作業隊列的併發線程數等於CPU核心數。</td>
  </tr>
  <tr>
   <td>花崗岩瞬態工作流隊列</td>
   <td><code>Max Parallel</code></td>
   <td>將值設定為CPU內核數的一半。</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM參數</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>真</p> <p>60000</p> </td>
   <td>在啟動指令碼中添加這AEM些JVM參數，以防止擴展查詢使系統過載。</td>
  </tr>
  <tr>
   <td>Lucene索引配置</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>已啟用</p> <p>已啟用</p> <p>已啟用</p> </td>
   <td>有關可用參數的詳細資訊，請參閱 <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">此頁</a>。</td>
  </tr>
  <tr>
   <td>資料儲存= S3資料儲存</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576(1MB)或更小</p> <p>最大堆大小的2-10%</p> </td>
   <td>另請參閱 <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">資料儲存配置</a>。</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35(25)</p> <p>20(10)</p> <p>30(5)</p> <p>10(3)</p> <p>4(4)</p> <p>./cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>快取的預設大小設定為256 MB。</p> <p>對執行快取無效所花費的時間有影響。</p> </td>
  </tr>
  <tr>
   <td>橡木觀察</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>最小和最大= 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### MongoMK效能基準 {#mongomk-performance-benchmark}

### 技術規格 {#technical-specifications-1}

基準test是按以下規格執行的：

|  | **「作者」節點** | **MongoDB節點** |
|---|---|---|
| 伺服器 | 裸機硬體(HP) | 裸機硬體(HP) |
| 作業系統 | RedHat Linux | RedHat Linux |
| CPU/內核 | 英特爾(R)至強(R)CPU E5-2407 @2.40GHz,8核 | 英特爾(R)至強(R)CPU E5-2407 @2.40GHz,8核 |
| RAM | 32 GB | 32 GB |
| 磁碟 | 磁性 — 超過1k IOPS | 磁性 — 超過1k IOPS |
| 爪哇 | OracleJRE 8版 | N/A |
| JVM堆 | 16 GB | 不適用 |
| 產品 | AEM 6.2 | MongoDB 3.2 WiredTiger |
| 諾德斯托雷 | 蒙戈MK | 不適用 |
| 資料儲存 | 檔案DS | 不適用 |
| 方案 | 單一產品：資產/30個併發線程 | 單一產品：資產/30個併發線程 |

### 效能基準結果 {#performance-benchmark-results-1}

>[!NOTE]
>
>下面顯示的數字已標準化為1作為基線，而不是實際吞吐量數字。

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK與MongoMK {#tarmk-vs-mongomk}

在兩者之間進行選擇時，需要考慮的基本規則是TarMK是為效能而設計的，而MongoMK是為可擴充性而設計的。 Adobe建議將TarMK作為所有部署方案中客戶使用的預設持久性技術，適用於AEM作者和發佈實例。

選擇MongoMK持久性後端(TarMK)的主要原因是橫向縮放實例。 這意味著有兩個或兩個以上活動的作者實例始終運行，並將MongoDB用作持久性儲存系統。 需要運行多個作者實例通常是因為單個伺服器的CPU和記憶體容量（支援所有併發創作活動）不再可持續。

有關TarMK與MongoMK的進一步詳細資訊，請參見 [建議的部署](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use)。

### TarMK與MongoMk准則 {#tarmk-vs-mongomk-guidelines}

**TarMK的優勢**

* 專為內容管理應用程式構建
* 檔案始終一致，可以使用任何基於檔案的備份工具進行備份
* 提供故障轉移機制 — 請參見 [冷備用](/help/sites-deploying/tarmk-cold-standby.md) 更多詳細資訊
* 提供高效能、可靠的資料儲存，並將操作開銷降至最低
* 降低TCO（總體擁有成本）

**選擇MongoMK的標準**

* 一天中連接的指定用戶數：以千計甚至更多
* 併發用戶數：數以百計甚至更多
* 每天資產接收量：數十萬甚至更多
* 每天編輯的頁數：數十萬甚至更多
* 每天的搜索量：數以萬計甚至更多

### TarMK與MongoMK基準 {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>下面顯示的數字已標準化為1作為基線，而不是實際吞吐量數字。

### 方案1技術規格 {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>作者OAK節點</strong></td>
   <td><strong>MongoDB節點</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>伺服器</td>
   <td>裸機硬體(HP)</td>
   <td>裸機硬體(HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>作業系統</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU/內核</td>
   <td>英特爾(R)至強(R)CPU E5-2407 @2.40GHz,8核</td>
   <td>英特爾(R)至強(R)CPU E5-2407 @2.40GHz,8核</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32 GB</td>
   <td>32 GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>磁碟</td>
   <td>磁性 — 超過1k IOPS</td>
   <td>磁性 — 超過1k IOPS</td>
   <td> </td>
  </tr>
  <tr>
   <td>爪哇</td>
   <td>OracleJRE 8版</td>
   <td>不適用</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM堆16GB</td>
   <td>16 GB</td>
   <td>不適用</td>
   <td> </td>
  </tr>
  <tr>
   <td>產品 </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>諾德斯托雷</td>
   <td>TarMK或MongoMK</td>
   <td>不適用</td>
   <td> </td>
  </tr>
  <tr>
   <td>資料儲存</td>
   <td>檔案DS </td>
   <td>不適用</td>
   <td> </td>
  </tr>
  <tr>
   <td>方案</td>
   <td><p><br /> 單一產品：每次運行資產/30個併發線程</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 方案1效能基準結果 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### 方案2技術規格 {#scenario-technical-specifications-1}

>[!NOTE]
>
>要使用MongoDB和使用一個TarMK系統的作者數量相同，您需要使用兩個節點的群AEM集。 四節點MongoDB群集可處理的作者數是一個TarMK實例的1.8倍。 一個八節點MongoDB群集可處理的作者數是一個TarMK實例的2.3倍。

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>作者TarMK節點</strong></td>
   <td><strong>作者MongoMK節點</strong></td>
   <td><strong>MongoDB節點</strong></td>
  </tr>
  <tr>
   <td>伺服器</td>
   <td>AWSC3.8x大</td>
   <td>AWSC3.8x大</td>
   <td>AWSC3.8x大</td>
  </tr>
  <tr>
   <td>作業系統</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
  </tr>
  <tr>
   <td>CPU/內核</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>60GB</td>
   <td>60GB</td>
   <td>60GB</td>
  </tr>
  <tr>
   <td>磁碟</td>
   <td>固態硬碟 — 10k IOPS</td>
   <td>固態硬碟 — 10k IOPS</td>
   <td>固態硬碟 — 10k IOPS</td>
  </tr>
  <tr>
   <td>爪哇</td>
   <td>OracleJRE 8版</td>
   <td><br /> OracleJRE 8版</td>
   <td>不適用</td>
  </tr>
  <tr>
   <td>JVM堆16GB</td>
   <td>30GB</td>
   <td>30GB</td>
   <td>不適用</td>
  </tr>
  <tr>
   <td>產品 </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>諾德斯托雷</td>
   <td>TarMK </td>
   <td>蒙戈MK</td>
   <td><br /> 不適用</td>
  </tr>
  <tr>
   <td>資料儲存</td>
   <td>檔案DS </td>
   <td><br /> 檔案DS</td>
   <td><br /> 不適用</td>
  </tr>
  <tr>
   <td>方案</td>
   <td><p><br /> <br /> 垂直使用案例：介質/ 2000併發線程</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### 方案2效能基準結果 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### 針對AEM Sites和資產的體系結構可擴充性指南 {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## 業績指南摘要  {#summary-of-performance-guidelines}

本頁介紹的指導原則可概括如下：

* **TarMK和檔案資料儲存** 是大多數客戶推薦的體系結構：

   * 最小拓撲：一個作者實例、兩個發佈實例、兩個調度程式
   * 如果共用檔案資料儲存區，則啟用無二進位複製

* **MongoMK和檔案資料儲存** 是推薦的用於作者層橫向可擴充性的體系結構：

   * 最小拓撲：三個作者實例、三個MongoDB實例、兩個發佈實例、兩個調度程式
   * 如果共用檔案資料儲存區，則啟用無二進位複製

* **諾德斯托雷** 應儲存在本地磁碟上，而不是網路連接儲存(NAS)
* 使用時 **AmazonS3**:

   * AmazonS3資料儲存區在作者層和發佈層之間共用
   * 必須啟用無二進位複製
   * 資料儲存垃圾收集要求在所有「作者」和「發佈」節點上先運行一次，然後在「作者」上再運行一次

* **除了開箱索引外，還應建立自定義索引** 基於最常見的搜索

   * Lucene索引應用於自定義索引

* **定制工作流可以顯著提高效能**&#x200B;例如，在「更新資產」工作流中刪除視頻步驟，禁用未使用的監聽程式等。

有關詳細資訊，請閱讀 [建議的部署](/help/sites-deploying/recommended-deploys.md) 的子菜單。
