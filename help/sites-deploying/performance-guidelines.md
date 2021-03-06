---
title: 效能准則
seo-title: 效能准則
description: 本文提供如何最佳化AEM部署效能的一般准則。
seo-description: 本文提供如何最佳化AEM部署效能的一般准則。
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
feature: 設定
exl-id: 5a305a5b-0c3d-413b-88c1-1f5abf7e1579
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2994'
ht-degree: 4%

---

# 效能指南{#performance-guidelines}

本頁提供如何最佳化AEM部署效能的一般准則。 如果您是初次使用AEM，請先瀏覽下列頁面，再開始閱讀效能准則：

* [AEM基本概念](/help/sites-deploying/deploy.md#basic-concepts)
* [AEM中的儲存概觀](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [建議的部署](/help/sites-deploying/recommended-deploys.md)
* [技術需求](/help/sites-deploying/technical-requirements.md)

下圖是AEM可用的部署選項（捲動以檢視所有選項）:

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
   <td><p><strong>資料存放區</strong></p> </td>
   <td><p><strong>索引</strong></p> </td>
   <td><p><strong>Web伺服器</strong></p> </td>
   <td><p><strong>瀏覽器</strong></p> </td>
   <td><p><strong>Marketing Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>網站</p> </td>
   <td><p>非HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>區段</p> </td>
   <td><p>屬性</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>目標</p> </td>
  </tr>
  <tr>
   <td><p>資產</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>檔案</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>分析</p> </td>
  </tr>
  <tr>
   <td><p>社群</p> </td>
   <td><p>Author-CS</p> </td>
   <td><p>紅帽</p> </td>
   <td><p>WebSphere</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>FireFox</p> </td>
   <td><p>行銷活動</p> </td>
  </tr>
  <tr>
   <td><p>表單</p> </td>
   <td><p>作者卸載</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>鉻黃</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>行動</p> </td>
   <td><p>作者叢集</p> </td>
   <td><p>IBM AIX</p> </td>
   <td><p>JBoss</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>對象</p> </td>
  </tr>
  <tr>
   <td><p>多網站</p> </td>
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
   <td><p>Apple OS</p> </td>
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
   <td><p>品牌入口網站</p> </td>
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
   <td><p>AoD</p> </td>
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
   <td><p>LiveFyre</p> </td>
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
   <td><p>Doc安全性</p> </td>
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
   <td><p>程式管理</p> </td>
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
>效能指引主要適用於AEM Sites。

## 何時使用效能指南{#when-to-use-the-performance-guidelines}

您應在下列情況下使用效能准則：

* **首次部署**:規劃首次部署AEM Sites或資產時，請務必了解在配置微內核、節點儲存和資料儲存時可用的選項（與預設設定相比）。例如，將TarMK的資料存放區預設設定變更為檔案資料存放區。
* **升級至新版本**:升級至新版本時，請務必了解與執行中環境相較的效能差異。例如，從AEM 6.1升級至6.2，或從AEM 6.0 CRX2升級至6.2 OAK。
* **回應時間緩慢**:當選定的Nodestore體系結構不滿足您的要求時，必須了解與其他拓撲選項相比的效能差異。例如，部署TarMK而非MongoMK，或使用檔案資料存放區而非Amazon S3或Microsoft Azure Data Store。
* **新增更多作者**:當建議的TarMK拓撲不符合效能需求，且上調製作節點已達到可用的最大容量時，請務必了解與搭配三個或更多製作節點使用MongoMK相比的效能差異。例如，部署MongoMK而非TarMK。
* **新增更多內容**:當建議的資料儲存體系結構不符合您的要求時，請務必了解與其他資料儲存選項相比的效能差異。範例：使用Amazon S3或Microsoft Azure資料存放區，而非檔案資料存放區。

## 簡介 {#introduction}

本章提供AEM架構及其最重要元件的一般概述。 此外，也提供開發准則，並說明TarMK和MongoMK基準測試中使用的測試案例。

### AEM平台{#the-aem-platform}

AEM平台包含下列元件：

![chlimage_1](assets/chlimage_1a.png)

如需AEM平台的詳細資訊，請參閱[什麼是AEM](/help/sites-deploying/deploy.md#what-is-aem)。

### AEM架構{#the-aem-architecture}

AEM部署有三個重要的組成要素。 內容作者、編輯者和核准者用來建立和檢閱內容的&#x200B;**製作例項**。 核准內容後，內容會發佈至名為&#x200B;**發佈例項**&#x200B;的第二個例項類型，使用者可從該類型存取內容。 第三個建置區塊是&#x200B;**Dispatcher**，此模組用於處理快取和URL篩選，並安裝在Web伺服器上。 有關AEM架構的其他資訊，請參閱[典型部署方案](/help/sites-deploying/deploy.md#typical-deployment-scenarios)。

![chlimage_1-1](assets/chlimage_1-1a.png)

### 微核{#micro-kernels}

微內核在AEM中充當持續性管理器。 與AEM一起使用的微內核有三種類型：TarMK、MongoDB和關係資料庫（受限制支援）。 根據執行個體的用途和您考慮的部署類型，選擇符合您需求的部署。 有關微內核的其他資訊，請參閱[建議部署](/help/sites-deploying/recommended-deploys.md)頁。

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

在AEM中，二進位資料可與內容節點分開儲存。 儲存二進位資料的位置稱為&#x200B;**資料儲存**，而內容節點和屬性的位置稱為&#x200B;**節點儲存**。

>[!NOTE]
>
>Adobe建議將TarMK設為客戶用於AEM製作和發佈執行個體的預設持續性技術。

>[!CAUTION]
>
>關係資料庫微內核受限制支援。 使用此類型的微內核之前，請聯繫[Adobe客戶服務](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)。

![chlimage_1-3](assets/chlimage_1-3a.png)

### 資料儲存{#data-store}

處理大量二進位檔時，建議使用外部資料存放區，而非預設節點存放區，以發揮最大效能。 例如，如果您的專案需要大量媒體資產，將其儲存在檔案或Azure/S3資料存放區下，將比直接儲存在MongoDB中更快地存取。

有關可用配置選項的詳細資訊，請參閱[配置節點和資料儲存](/help/sites-deploying/data-store-config.md)。

>[!NOTE]
>
>Adobe建議選擇使用Adobe Managed Services在Azure或Amazon Web Services(AWS)上部署AEM的選項，讓具備在這些雲端運算環境中部署和操作AEM經驗與技能的團隊從中受益。 請參閱我們有關Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)的[其他檔案。
>
>如需有關如何在Azure或AWS上部署AEM的建議，強烈建議您直接與雲端提供者或我們其中一位合作夥伴合作，支援在您選擇的雲端環境中部署AEM。 選定的雲提供商或合作夥伴負責規模規格、設計和實施他們將支援的體系結構，以滿足您的特定效能、負載、可擴充性和安全要求。
>
>如需其他詳細資訊，另請參閱[技術需求](/help/sites-deploying/technical-requirements.md#supported-platforms)頁面。

### 搜尋 {#search-features}

本節中列出的是與AEM搭配使用的自訂索引提供者。 若要深入了解索引，請參閱[Oak查詢與索引](/help/sites-deploying/queries-and-indexing.md)。

>[!NOTE]
>
>對於大部分部署，Adobe建議使用Lucene索引。 您只應將Solr用於特殊和複雜部署中的可擴充性。

![chlimage_1-4](assets/chlimage_1-4a.png)

### 開發指南{#development-guidelines}

您應針對AEM開發以&#x200B;**效能和可擴充性為目標**。 以下呈現您可遵循的一些最佳實務：

**DO**

* 分離呈現、邏輯和內容
* 使用現有AEM API(例如：Sling)和工具(例如：復寫)
* 根據實際內容進行開發
* 優化快取性
* 將保存次數最小化(例如：使用暫時性工作流程
* 確定所有HTTP端點都為RESTful
* 限制JCR觀測範圍
* 注意非同步線程

**不要**

* 如果您可以，請勿直接使用JCR API
* 請勿變更/libs，而是使用覆蓋
* 盡可能不要使用查詢
* 請勿使用Sling系結來取得Java程式碼中的OSGi服務，而應使用：

   * @Reference在DS元件中
   * @Inject在Sling模型中
   * sling.getService()（在Sightly使用類別中）
   * JSP中的sling.getService()
   * 服務追蹤器
   * 直接存取OSGi服務註冊表

如需有關在AEM上開發的詳細資訊，請參閱[Developing - The Basics](/help/sites-developing/the-basics.md)。 如需其他最佳實務，請參閱[開發最佳實務](/help/sites-developing/best-practices.md)。

### 基準方案{#benchmark-scenarios}

>[!NOTE]
>
>此頁面上顯示的所有基準測試都已在實驗室設定中執行。

以下詳述的測試案例會用於TarMK、MongoMk和TarMK與MongoMk章節的基準區段。 要查看特定基準測試使用的方案，請閱讀[技術規範](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark)表中的方案欄位。

**單一產品案例**

AEM Assets:

* 使用者互動：瀏覽資產/搜尋資產/下載資產/讀取資產中繼資料/更新資產中繼資料/上傳資產/執行上傳資產工作流程
* 執行模式：同時使用者，每位使用者進行單次互動

**混合產品案例**

AEM Sites +資產：

* 網站使用者互動：閱讀文章頁面/閱讀頁面/建立段落/編輯段落/建立內容頁面/啟用內容頁面/作者搜尋
* Assets使用者互動：瀏覽資產/搜尋資產/下載資產/讀取資產中繼資料/更新資產中繼資料/上傳資產/執行上傳資產工作流程
* 執行模式：同時使用者，每位使用者的混合互動

**垂直使用案例情境**

媒體:

* 閱讀文章頁面(27.4%)、閱讀頁面(10.9%)、建立工作階段(2.6%)、啟用內容頁面(1.7%)、建立內容頁面(0.4%)、建立段落(4.3%)、編輯段落(0.9%)、影像元件(0.9%)、瀏覽資產(20%)、讀取資產中繼資料(8.5%)、下載資產(4.2%)、搜尋資產(0.2%)、更新資產(2%)(2.4%)、上傳資產(1.2%)、瀏覽專案(4.9%)、讀取專案(6.6%)、專案新增資產(1.2%)、專案新增網站(1.2%)、建立專案(0.1%)、作者搜尋(0.4%)
* 執行模式：同時使用者，每位使用者的混合互動

## TarMK {#tarmk}

本章介紹TarMK的一般效能指南，指定最低架構需求和設定配置。 也提供了基準測試，以進一步說明。

Adobe建議將TarMK設為客戶在所有部署案例（針對AEM製作和發佈例項）中使用的預設持續性技術。

有關TarMK的詳細資訊，請參閱[部署方案](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)和[Tar Storage](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage)。

### TarMK最低架構指南{#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>以下提供的最低架構指引適用於生產環境和高流量網站。 這些是運行AEM所需的&#x200B;**not**[最小規範](/help/sites-deploying/technical-requirements.md#prerequisites)。

若要在使用TarMK時建立良好的效能，您應從下列架構開始：

* 一個Author例項
* 兩個發佈例項
* 兩個Dispatcher

下圖是AEM網站和AEM Assets的架構指引。

>[!NOTE]
>
>如果共用檔案資料儲存區，則應將&#x200B;**ON**&#x200B;開啟無二進位復寫。

**AEM Sites的Tar架構指引**

![chlimage_1-5](assets/chlimage_1-5a.png)

**AEM Assets的Tar架構指引**

![chlimage_1-6](assets/chlimage_1-6a.png)

### TarMK設定指引{#tarmk-settings-guideline}

為獲得良好效能，您應遵循下列設定准則。 有關如何更改設定的說明，請[參閱本頁](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

<table>
 <tbody>
  <tr>
   <td><strong>設定</strong></td>
   <td><strong>參數</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>Sling作業佇列</td>
   <td><code>queue.maxparallel</code></td>
   <td>將值設定為CPU內核數的一半。 </td>
   <td>預設情況下，每個作業隊列的併發線程數等於CPU核心數。</td>
  </tr>
  <tr>
   <td>Granite暫時工作流程佇列</td>
   <td><code>Max Parallel</code></td>
   <td>將值設定為CPU內核數的一半</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM參數</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> </td>
   <td>在AEM啟動指令碼中添加這些JVM參數，以防止擴展查詢超出系統負載。</td>
  </tr>
  <tr>
   <td>Lucene索引配置</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>已啟用</p> <p>已啟用</p> <p>已啟用</p> </td>
   <td>有關可用參數的詳細資訊，請參見<a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">此頁</a>。</td>
  </tr>
  <tr>
   <td>資料存放區= S3資料存放區</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576(1MB)或更小</p> <p>最大堆大小的2-10%</p> </td>
   <td>另請參閱<a href="/help/sites-deploying/data-store-config.md#data-store-configurations">資料儲存配置</a>。</td>
  </tr>
  <tr>
   <td>DAM更新資產工作流程</td>
   <td><code>Transient Workflow</code></td>
   <td>已勾選</td>
   <td>此工作流程會管理資產的更新。</td>
  </tr>
  <tr>
   <td>DAM中繼資料回寫</td>
   <td><code>Transient Workflow</code></td>
   <td>已勾選</td>
   <td>此工作流程會管理XMP回寫至原始二進位檔，並在JCR中設定上次修改的日期。</td>
  </tr>
 </tbody>
</table>

### TarMK效能基準{#tarmk-performance-benchmark}

#### 技術規範{#technical-specifications}

基準測試是按以下規格執行的：

|  | **製作節點** |
|---|---|
| 伺服器 | 裸機硬體(HP) |
| 作業系統 | RedHat Linux |
| CPU/內核 | 英特爾(R)至強(R)CPU E5-2407 @2.40GHz,8核 |
| RAM | 32GB |
| 磁碟 | 磁性 |
| Java | OracleJRE第8版 |
| JVM堆 | 16GB |
| 產品 | AEM 6.2 |
| Nodestore | TarMK |
| 資料存放區 | 檔案DS |
| 藍本 | 單一產品：資產/ 30個並行執行緒 |

#### 效能基準結果{#performance-benchmark-results}

>[!NOTE]
>
>以下數字已標準化為1作為基準，而不是實際吞吐量數字。

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

選擇MongoMK永續性後端而不選擇TarMK的主要原因是橫向縮放執行個體。 這表示有兩個或多個活動的作者實例始終運行，並使用MongoDB作為持久性儲存系統。 執行多個製作執行個體的需求，一般是因為單一伺服器的CPU和記憶體容量（支援所有同時編寫活動）已無法持續。

有關TarMK的詳細資訊，請參閱[部署方案](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)和[Mongo儲存](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage)。

### MongoMK最低體系結構指南{#mongomk-minimum-architecture-guidelines}

若要在使用MongoMK時建立良好的效能，您應從下列架構開始：

* 三個製作例項
* 兩個發佈例項
* 三個MongoDB實例
* 兩個Dispatcher

>[!NOTE]
>
>在生產環境中， MongoDB將始終用作具有主節點和兩個輔助節點的複製副本集。 讀取和寫入會轉到主節點，而讀取會轉到輔助節點。 如果儲存不可用，則可以用仲裁程式替換其中一個輔助程式，但MongoDB副本集必須始終由奇數個實例組成。

>[!NOTE]
>
>如果共用檔案資料儲存區，則應將&#x200B;**ON**&#x200B;開啟無二進位復寫。

![chlimage_1-9](assets/chlimage_1-9a.png)

### MongoMK設定指南{#mongomk-settings-guidelines}

為獲得良好效能，您應遵循下列設定准則。 有關如何更改設定的說明，請[參閱本頁](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

<table>
 <tbody>
  <tr>
   <td><strong>設定</strong></td>
   <td><strong>參數</strong></td>
   <td><strong>值（預設值）</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>Sling作業佇列</td>
   <td><code>queue.maxparallel</code></td>
   <td>將值設定為CPU內核數的一半。 </td>
   <td>預設情況下，每個作業隊列的併發線程數等於CPU核心數。</td>
  </tr>
  <tr>
   <td>Granite暫時工作流程佇列</td>
   <td><code>Max Parallel</code></td>
   <td>將值設定為CPU內核數的一半。</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM參數</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> <p>60000</p> </td>
   <td>在AEM啟動指令碼中添加這些JVM參數，以防止擴展查詢超出系統負載。</td>
  </tr>
  <tr>
   <td>Lucene索引配置</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>已啟用</p> <p>已啟用</p> <p>已啟用</p> </td>
   <td>有關可用參數的詳細資訊，請參見<a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">此頁</a>。</td>
  </tr>
  <tr>
   <td>資料存放區= S3資料存放區</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576(1MB)或更小</p> <p>最大堆大小的2-10%</p> </td>
   <td>另請參閱<a href="/help/sites-deploying/data-store-config.md#data-store-configurations">資料儲存配置</a>。</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048年</p> <p>35(25)</p> <p>20(10)</p> <p>30(5)</p> <p>10(3)</p> <p>4(4)</p> <p>。/cache,size=2048，二進位=0,-compact,-compress</p> </td>
   <td><p>快取的預設大小設定為256 MB。</p> <p>會影響執行快取失效所花費的時間。</p> </td>
  </tr>
  <tr>
   <td>oak-overation</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>最小值和最大值= 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### MongoMK效能基準{#mongomk-performance-benchmark}

### 技術規範{#technical-specifications-1}

基準測試是按以下規格執行的：

|  | **製作節點** | **MongoDB節點** |
|---|---|---|
| 伺服器 | 裸機硬體(HP) | 裸機硬體(HP) |
| 作業系統 | RedHat Linux | RedHat Linux |
| CPU/內核 | 英特爾(R)至強(R)CPU E5-2407 @2.40GHz,8核 | 英特爾(R)至強(R)CPU E5-2407 @2.40GHz,8核 |
| RAM | 32GB | 32GB |
| 磁碟 | 磁性 — 超過1k IOPS | 磁性 — 超過1k IOPS |
| Java | OracleJRE第8版 | N/A |
| JVM堆 | 16GB | 不適用 |
| 產品 | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | 不適用 |
| 資料存放區 | 檔案DS | 不適用 |
| 藍本 | 單一產品：資產/ 30個並行執行緒 | 單一產品：資產/ 30個並行執行緒 |

### 效能基準結果{#performance-benchmark-results-1}

>[!NOTE]
>
>以下數字已標準化為1作為基準，而不是實際吞吐量數字。

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK與MongoMK {#tarmk-vs-mongomk}

在兩者之間進行選擇時，需要考慮的基本規則是TarMK是為效能而設計，而MongoMK是為了擴充性。 Adobe建議將TarMK設為客戶在所有部署案例（針對AEM製作和發佈例項）中使用的預設持續性技術。

選擇MongoMK永續性後端而不選擇TarMK的主要原因是橫向縮放執行個體。 這表示有兩個或多個活動的作者實例始終運行，並使用MongoDB作為持久性儲存系統。 需要執行多個製作執行個體通常是因為單一伺服器的CPU和記憶體容量（支援所有同時編寫活動）已無法持續。

如需TarMK與MongoMK的詳細資訊，請參閱[建議部署](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use)。

### TarMK與MongoMk指南{#tarmk-vs-mongomk-guidelines}

**TarMK的優點**

* 專為內容管理應用程式而構建
* 檔案始終一致，可以使用任何基於檔案的備份工具進行備份
* 提供故障轉移機制 — 有關詳細資訊，請參閱[冷備用](/help/sites-deploying/tarmk-cold-standby.md)
* 提供高效能和可靠的資料儲存，並且操作開銷最小
* 降低TCO（總擁有成本）

**選擇MongoMK的條件**

* 一天內連接的指定用戶數：以千計甚至更多
* 同時使用者人數：數百個以上
* 每日資產擷取量：幾十萬甚至更多
* 每天編輯頁面的數量：幾十萬甚至更多
* 每天的搜索量：幾萬甚至更多

### TarMK與MongoMK基準{#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>以下數字已標準化為1作為基準，而不是實際吞吐量數字。

### 方案1技術規範{#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>製作OAK節點</strong></td>
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
   <td>32GB</td>
   <td>32GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>磁碟</td>
   <td>磁性 — 超過1k IOPS</td>
   <td>磁性 — 超過1k IOPS</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java</td>
   <td>OracleJRE第8版</td>
   <td>不適用</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM堆16GB</td>
   <td>16GB</td>
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
   <td>Nodestore</td>
   <td>TarMK或MongoMK</td>
   <td>不適用</td>
   <td> </td>
  </tr>
  <tr>
   <td>資料存放區</td>
   <td>檔案DS </td>
   <td>不適用</td>
   <td> </td>
  </tr>
  <tr>
   <td>藍本</td>
   <td><p><br /> 單一產品：資產/每次執行30個同時執行緒</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 方案1效能基準結果{#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### 方案2技術規範{#scenario-technical-specifications-1}

>[!NOTE]
>
>若要啟用與使用一個TarMK系統時相同數量的MongoDB作者，您需要具有兩個AEM節點的叢集。 四個節點的MongoDB群集可處理1.8倍於一個TarMK實例的作者數。 八個節點的MongoDB群集可處理的作者數是一個TarMK實例的2.3倍。

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>製作TarMK節點</strong></td>
   <td><strong>製作MongoMK節點</strong></td>
   <td><strong>MongoDB節點</strong></td>
  </tr>
  <tr>
   <td>伺服器</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
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
   <td>Java</td>
   <td>OracleJRE第8版</td>
   <td><br /> OracleJRE第8版</td>
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
   <td>Nodestore</td>
   <td>TarMK </td>
   <td>MongoMK</td>
   <td><br /> 不適用</td>
  </tr>
  <tr>
   <td>資料存放區</td>
   <td>檔案DS </td>
   <td><br /> 檔案DS</td>
   <td><br /> 不適用</td>
  </tr>
  <tr>
   <td>藍本</td>
   <td><p><br /> <br /> 垂直使用案例：媒體/ 2000個併發線程</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### 方案2效能基準結果{#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### AEM Sites和Assets的架構可擴充性准則{#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## 效能指南摘要{#summary-of-performance-guidelines}

本頁所列准則概述如下：

* **TarMK與檔案資** 料集是大多數客戶建議的架構：

   * 最小拓撲：一個製作例項、兩個發佈例項、兩個Dispatcher
   * 如果共用檔案資料儲存，則開啟無二進位複製

* **MongoMK with File Datastore** 是建議的架構，可擴充至作者階層的水準：

   * 最小拓撲：三個製作例項、三個MongoDB例項、兩個發佈例項、兩個Dispatcher
   * 如果共用檔案資料儲存，則開啟無二進位複製

* **** Nodestore應儲存在本地磁碟上，而不是網路連接儲存(NAS)上
* 使用&#x200B;**Amazon S3**&#x200B;時：

   * Amazon S3資料存放區在製作和發佈層級之間共用
   * 必須開啟無二進位複製
   * 「資料存放區垃圾收集」需要先在所有「製作」和「發佈」節點上執行，然後在「製作」上執行第二次

* **除了根據最常見的搜尋建立現成可用的索** 引外，還應建立自訂索引

   * Lucene索引應用於自訂索引

* **自訂工作流程可大幅改善效能**，例如移除「更新資產」工作流程中的視訊步驟、停用未使用的接聽程式等。

如需詳細資訊，請另閱[建議部署](/help/sites-deploying/recommended-deploys.md)頁面。
