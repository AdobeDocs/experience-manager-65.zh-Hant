---
title: 操作控制面板
seo-title: Operations Dashboard
description: 瞭解如何使用Adobe Experience Manager中的操作控制面板。
seo-description: Learn how to use the Operations Dashboard.
uuid: ef24813f-a7a8-4b26-a496-6f2a0d9efef6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: b210f5d7-1d68-49ee-ade7-667c6ab11d2b
docset: aem65
exl-id: f9a88156-91a2-4c85-9bc9-8f23700c2cbd
feature: Operations
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '6057'
ht-degree: 2%

---

# 操作控制面板 {#operations-dashboard}

## 簡介 {#introduction}

AEM 6中的操作儀表板可協助系統操作員快速監視AEM系統健康狀況。 此外，還能提供AEM相關方面自動產生的診斷資訊，並讓您設定和執行完整的維護自動化，大幅減少專案操作和支援案例。 操作控制面板可以透過自訂健康情況檢查和維護任務進行擴展。 此外，您也可透過JMX從外部監視工具存取操作控制面板資料。

**操作控制面板：**

* 是一鍵式系統狀態，可協助營運部門提高效率
* 在單一集中位置提供系統健康概觀
* 縮短尋找、分析和修正問題的時間
* 提供獨立的維護自動化，協助大幅降低專案營運成本

您可以前往「 」存取 **工具** - **作業** 從AEM歡迎畫面。

>[!NOTE]
>
>若要存取操作控制面板，登入使用者必須屬於「操作員」使用者群組。 如需詳細資訊，請參閱以下說明檔案： [使用者、群組和存取權管理](/help/sites-administering/user-group-ac-admin.md).

## 健全狀態報表 {#health-reports}

健康狀態報告系統透過Sling健康狀態檢查提供AEM執行個體的健康狀態資訊。 您可以透過OSGI、JMX、HTTP請求（透過JSON）或透過Touch UI完成此操作。 它提供某些可設定計數器的測量值和臨界值，有時也提供如何解決問題的資訊。

它有幾項功能，如下所述。

## 健康狀態檢查 {#health-checks}

此 **健康狀態報表** 是一套卡片系統，可指出特定產品區域的健康情況好或壞。 這些卡片是Sling健康情況檢查的視覺效果，其會彙總來自JMX和其他來源的資料，並再次以MBean公開處理的資訊。 這些MBean也可以在以下位置檢查： [JMX Web主控台](/help/sites-administering/jmx-console.md)，位於 **org.apache.sling.healthcheck** 網域。

健康狀態報告介面可透過以下方式存取： **工具** - **作業** - **健康狀態報表** 「AEM歡迎」畫面上的功能表，或直接透過下列URL進行：

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

卡片系統會顯示三種可能的狀態： **確定**， **警告** 和 **關鍵**. 狀態是規則和臨界值的結果，您可以將滑鼠移至卡片上，然後按一下動作列中的齒輪圖示即可設定這些規則和臨界值：

![chlimage_1-117](assets/chlimage_1-117.png)

### 健康情況檢查型別 {#health-check-types}

AEM 6中有兩種健康狀態檢查型別：

1. 個別健康情況檢查
1. 複合健康狀態檢查

一個 **個人健康情況檢查** 是與狀態卡相對應的單一健康情況檢查。 個別健康情況檢查可以使用規則或臨界值來設定，而且它們可以提供一或多個提示和連結來解決已識別的健康情況問題。 以「記錄錯誤」檢查為例：如果執行個體記錄中存在ERROR專案，請在健康狀態檢查的詳細資訊頁面中找到。 在頁面頂端，您可以在診斷工具區段中看到「記錄訊息」分析器的連結，讓您更詳細地分析這些錯誤，並重新設定記錄器。

A **複合健康狀態檢查** 是彙總來自數個個別檢查的資訊的檢查。

複合健康狀態檢查的設定是使用 **篩選標籤**. 本質上，具有相同篩選器標籤的所有單一檢查都會分組為複合健康狀態檢查。 只有當所有要彙總的單一檢查的狀態都為OK時，複合健康狀態檢查的狀態才會為OK。

### 如何建立健康情況檢查 {#how-to-create-health-checks}

在「操作控制面板」中，您可以顯示個別和複合健康情況檢查的結果。

### 建立個人健康狀態檢查 {#creating-an-individual-health-check}

建立個別健康情況檢查涉及兩個步驟：實作Sling健康情況檢查和在控制面板的設定節點中新增健康情況檢查專案。

1. 若要建立Sling健康情況檢查，請建立實作Sling健康情況檢查介面的OSGI元件。 將此元件新增至套件組合中。 元件的屬性可完整識別健康狀態檢查。 安裝元件後，系統會自動建立JMX MBean以進行健康狀態檢查。 請參閱 [Sling健康情況檢查檔案](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html) 以取得詳細資訊。

   使用OSGI服務元件附註編寫的Sling健康情況檢查元件範例：

   ```java
   @Component(service = HealthCheck.class,
   property = {
       HealthCheck.NAME + "=Example Check",
       HealthCheck.TAGS + "=example",
       HealthCheck.TAGS + "=test",
       HealthCheck.MBEAN_NAME + "=exampleHealthCheckMBean"
   })
    public class ExampleHealthCheck implements HealthCheck {
       @Override
       public Result execute() {
           // health check code
       }
    }
   ```

   >[!NOTE]
   >
   >此 `MBEAN_NAME` 屬性定義為此健康狀態檢查產生的mbean的名稱。

1. 建立健康狀態檢查之後，必須建立新的設定節點，才能在操作儀表板介面中存取它。 對於此步驟，必須知道健康狀態檢查的JMX Mbean名稱( `MBEAN_NAME` 屬性)。 若要建立健康狀態檢查的設定，請開啟CRXDE並新增節點(型別 **nt：unstructured**)，路徑如下： `/apps/settings/granite/operations/hc`

   應在新節點上設定下列屬性：

   * **名稱:** `sling:resourceType`

      * **類型：**`String`
      * **值:** `granite/operations/components/mbean`

   * **名稱:** `resource`

      * **類型：**`String`
      * **值:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`

   >[!NOTE]
   >
   >上述資源路徑的建立如下所示：如果健康情況檢查的mbean名稱為「test」，請在路徑結尾新增「test」 `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`
   >
   >所以最終路徑如下：
   >
   >`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/test`

   >[!NOTE]
   >
   >確定 `/apps/settings/granite/operations/hc` path的下列屬性設定為true：
   >
   >
   >`sling:configCollectionInherit`
   >
   >`sling:configPropertyInherit`
   >
   >
   >此程式會告知設定管理員要將新設定與中的現有設定合併 `/libs`.

### 建立複合健康狀態檢查 {#creating-a-composite-health-check}

複合健康狀態檢查的作用是彙總共用一組通用功能的數個個別健康狀態檢查。 例如，「安全性複合健康情況檢查」會將執行安全性相關驗證的所有個別健康情況檢查分組。 建立複合檢查的第一步是新增OSGI設定。 若要將其顯示在操作儀表板中，必須以簡單檢查相同的方式新增新的配置節點。

1. 前往OSGI主控台中的Web Configuration Manager。 存取 `https://serveraddress:port/system/console/configMgr`
1. 搜尋以下名稱的專案： **Apache Sling複合健康狀態檢查**. 找到之後，請注意已有兩個組態可供使用：一個用於「系統檢查」，另一個用於「安全性檢查」。
1. 按組態右側的「+」按鈕來建立組態。 新視窗隨即顯示，如下所示：

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. 建立設定並儲存。 Mbean會以新組態建立。

   每個設定屬性的用途如下：

   * **名稱(hc.name)：** 複合健康狀態檢查的名稱。 建議使用有意義的名稱。
   * **標籤(hc.tags)：** 此健康狀態檢查的標籤。 如果此複合健康狀態檢查要成為另一個複合健康狀態檢查（例如在健康狀態檢查的階層中）的一部分，請新增此複合相關的標籤。
   * **MBean名稱(hc.mbean.name)：** 為此複合健康狀態檢查的JMX MBean指定的Mbean名稱。
   * **篩選標籤(filter.tags)：** 複合健康情況檢查專屬的屬性。 這些標籤會由複合專案彙總。 複合健康狀態檢查會在其群組下彙總所有具有符合此複合之任何篩選標籤的健康狀態檢查。 例如，含有篩選標籤的複合健康情況檢查 **測試** 和 **check**，彙總具有下列任何一項的所有個別和複合健康情況檢查： **測試** 和 **check** 標籤屬性中的標籤( `hc.tags`)。

   >[!NOTE]
   >
   >系統會為Apache Sling複合健康狀態檢查的每個新設定建立新的JMX Mbean。**

1. 最後，已建立的複合健康狀態檢查專案必須新增至「操作控制面板」組態節點。 此程式與個別健康情況檢查的程式相同：型別的節點 **nt：unstructured** 必須建立於 `/apps/settings/granite/operations/hc`. 節點的資源屬性是由的值所定義 **hc.mean.name** 在OSGI設定中。

   例如，如果您建立了組態並設定 **hc.mbean.name** 值至 **磁碟使用情況**，設定節點如下：

   * **名稱:** `Composite Health Check`

      * **類型：**`nt:unstructured`

   具有以下屬性：

   * **名稱:** `sling:resourceType`

      * **類型：**`String`
      * **值:** `granite/operations/components/mbean`

   * **名稱:** `resource`

      * **類型：**`String`
      * **值:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`

   >[!NOTE]
   >
   >如果您建立邏輯上屬於複合檢查的個別健康情況檢查（預設情況下已存在於儀表板中），則會自動擷取這些檢查，並將其分組在個別複合檢查下。 因此，不需要為這些檢查建立設定節點。
   >
   >例如，如果您建立個別安全性健康情況檢查，請將其指派給「**安全性**「 」標籤完成，並已安裝。 它會自動顯示在「操作圖示板」的「安全性檢查」複合檢查下。

### AEM提供的健康情況檢查 {#health-checks-provided-with-aem}

<table>
 <tbody>
  <tr>
   <td><strong>運行狀況檢查名稱</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>查詢效能</td>
   <td><p>此健康情況檢查已簡化 <strong>在AEM 6.4中</strong>，現在會檢查最近重構的 <code>Oak QueryStats</code> MBean，更具體地說 <code>SlowQueries </code>屬性。 如果統計資料包含任何緩慢查詢，則健康狀態檢查會傳回警告。 否則，會傳回OK狀態。<br /> </p> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=queriesStatus，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>觀測佇列長度</td>
   <td><p>「觀察佇列長度」會反複執行所有事件接聽程式和背景觀察程式，並比較其 <code>queueSize </code>至其 <code>maxQueueSize</code> 和：</p>
    <ul>
     <li>若符合下列條件，則會傳回「嚴重」狀態： <code>queueSize</code> 值超過 <code>maxQueueSize</code> 值（即事件會被捨棄的時間）</li>
     <li>如果符合下列條件，則傳回Warn <code>queueSize</code> 值超過 <code>maxQueueSize * WARN_THRESHOLD</code> （預設值為0.75） </li>
    </ul> <p>每個佇列的長度上限分別來自不同的設定(Oak和AEM)，且無法透過此健康狀態檢查設定。 此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=ObservationQueueLengthHealthCheck，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>查詢周遊限制</td>
   <td><p>查詢周遊限制檢查 <code>QueryEngineSettings</code> MBean，更具體地說 <code>LimitInMemory</code> 和 <code>LimitReads</code> 屬性，並傳回下列狀態：</p>
    <ul>
     <li>如果其中一個限制等於或大於 <code>Integer.MAX_VALUE</code></li>
     <li>如果其中一個限制低於10000 （Oak的建議設定），則傳回「警告」狀態</li>
     <li>若符合下列條件，則會傳回「嚴重」狀態： <code>QueryEngineSettings</code> 或無法擷取任何限制</li>
    </ul> <p>此健康狀態檢查的Mbean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=queryTraversalLimitsBundle，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>已同步時鐘</td>
   <td><p>此檢查僅適用於 <a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">檔案節點存放區叢集</a>. 它會傳回以下狀態：</p>
    <ul>
     <li>當執行個體時鐘不同步並超過預先定義的低臨界值時，會傳回警告狀態</li>
     <li>當執行個體時鐘不同步並超過預先定義的高臨界值時，會傳回「嚴重」狀態</li>
    </ul> <p>此健康狀態檢查的Mbean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=slingDiscoveryOakSynchronizedClocks，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>非同步處理索引</td>
   <td><p>非同步索引檢查：</p>
    <ul>
     <li>如果至少一個索引通道失敗，則傳回「嚴重」狀態</li>
     <li>檢查 <code>lastIndexedTime</code> 對於所有索引通道和：
      <ul>
       <li>如果超過2小時前，則傳回「嚴重」狀態 </li>
       <li>如果時間介於2小時到45分鐘之間，則傳回警告狀態 </li>
       <li>如果時間少於45分鐘前，則傳回「正常」狀態 </li>
      </ul> </li>
     <li>如果不符合這些條件，則會傳回OK狀態</li>
    </ul> <p>「嚴重」和「警告」狀態臨界值均可設定。 此健康狀態檢查的Mbean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=asyncIndexHealthCheck，type=HealthCheck</a>.</p> <p><strong>注意： </strong>此健康情況檢查可與AEM 6.4搭配使用，且已反向移植至AEM 6.3.0.1。</p> </td>
  </tr>
  <tr>
   <td>大型 Lucene 索引</td>
   <td><p>此檢查使用下列專案公開的資料： <code>Lucene Index Statistics</code> 識別大型索引和傳回的MBean：</p>
    <ul>
     <li>如果索引中有超過10億份檔案，則為警告狀態</li>
     <li>a如果索引中有超過15億份檔案，則為嚴重狀態</li>
    </ul> <p>臨界值是可設定的，健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=largeIndexHealthCheck，type=HealthCheck。</a></p> <p><strong>注意： </strong>此檢查適用於AEM 6.4，並已反向移植至AEM 6.3.2.0。</p> </td>
  </tr>
  <tr>
   <td>系統維護</td>
   <td><p>「系統維護」是一種複合檢查，如果所有維護工作都按設定執行，則會傳回「確定」。 請記住：</p>
    <ul>
     <li>每個維護任務都會隨附相關的健康狀態檢查</li>
     <li>如果未將任務新增至維護期間，其健康狀態檢查會傳回「嚴重」</li>
     <li>設定「稽核記錄」和「工作流程清除」維護作業，或將其從維護視窗中移除。 如果未進行設定，這些工作會在第一次嘗試執行時失敗，因此「系統維護」檢查會傳回「嚴重」狀態。</li>
     <li><strong>使用AEM 6.4</strong>，另外也會檢查 <a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">Lucene二進位檔維護</a> 任務</li>
     <li>在AEM 6.2和更低版本上，系統維護檢查會在啟動後立即傳回「警告」狀態，因為工作永遠不會執行。 從6.3開始，如果尚未到達第一個維護時段，則會傳回「確定」。</li>
    </ul> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">org.apache.sling.healthcheck：name=systemchecks，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>復寫佇列</td>
   <td><p>此檢查會反複執行復寫代理程式並檢視其佇列。 對於佇列頂端的專案，檢查會檢視代理程式重試復寫的次數。 如果代理程式重試的復寫超過的值， <code>numberOfRetriesAllowed</code> 引數，則會傳回警告。 此 <code>numberOfRetriesAllowed</code> 引數是可設定的。 </p> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=replicationQueue，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Sling 工作</td>
   <td>
    <div>
      「Sling工作」會檢查JobManager中佇列的作業數目，並將其與
     <code>maxNumQueueJobs</code> 臨界值，以及：
    </div>
    <ul>
     <li>若超過 <code>maxNumQueueJobs</code> 在佇列中</li>
     <li>如果長期執行中的作用中工作超過1小時，則傳回Critical</li>
     <li>如果有佇列的工作，而且最後完成的工作時間超過1小時，則傳回Critical</li>
    </ul> <p>僅可設定佇列作業的最大數量引數，其預設值為1000。</p> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=slingJobs，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>要求效能</td>
   <td><p>此檢查會檢視 <code>granite.request.metrics.timer</code> <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">Sling量度 </a>和：</p>
    <ul>
     <li>如果第75個百分位值超過嚴重臨界值（預設值為500毫秒），則傳回Critical</li>
     <li>如果第75個百分位值超過警告臨界值（預設值為200毫秒），則傳回Warn</li>
    </ul> <p>此健康狀態檢查的MBean為<em> </em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=requestsStatus，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>日誌錯誤</td>
   <td><p>如果記錄中有錯誤，此檢查會傳回「警告」狀態。</p> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=logErrorHealthCheck，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>磁碟空間</td>
   <td><p>磁碟空間檢查會檢視 <code>FileStoreStats</code> MBean，會擷取節點存放區的大小以及節點存放區分割區上可用的磁碟空間量，並且：</p>
    <ul>
     <li>如果可用磁碟空間與存放庫大小的比率小於警告臨界值（預設值為10），則傳回Warn</li>
     <li>如果可用磁碟空間與存放庫大小的比率小於嚴重臨界值（預設值為2），則傳回「嚴重」</li>
    </ul> <p>這兩個臨界值都是可設定的。 此檢查僅適用於具有區段存放區的執行個體。</p> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=DiskSpaceHealthCheck，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>排程器健康情況檢查</td>
   <td><p>如果執行個體有執行超過60秒的Quartz工作，此檢查會傳回警告。 可設定可接受的持續時間臨界值。</p> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=slingCommonsSchedulerHealthCheck，type=HealthCheck</a><em>.</em></p> </td>
  </tr>
  <tr>
   <td>安全性檢查</td>
   <td><p>安全性檢查是一種複合檢查，可彙總多個安全性相關檢查的結果。 這些個別健康情況檢查可解決 <a href="/help/sites-administering/security-checklist.md">安全性檢查清單檔案頁面。</a> 此檢查在執行個體啟動時，可作為安全冒煙測試使用。 </p> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=securitychecks，type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>作用中組合</td>
   <td><p>使用中的組合會檢查所有組合的狀態，並且：</p>
    <ul>
     <li>如果有任何套件組合未作用中或（從延遲啟動開始），則傳回「警告」狀態</li>
     <li>它會忽略忽略清單中的套件組合狀態</li>
    </ul> <p>忽略清單引數是可設定的。</p> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=inactiveBundles，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>程式碼快取檢查</td>
   <td><p>健康情況檢查會驗證可能觸發Java™ 7中出現CodeCache錯誤的多個JVM條件：</p>
    <ul>
     <li>如果執行個體在Java™ 7上執行，並啟用程式碼快取排清，則傳回Warn</li>
     <li>如果執行個體在Java™ 7上執行，且保留的程式碼快取大小小於最小臨界值（預設值為90 MB），則傳回Warn</li>
    </ul> <p>此 <code>minimum.code.cache.size</code> 臨界值是可設定的。 如需有關錯誤的詳細資訊，請參閱 <a href="https://bugs.java.com/bugdatabase/"> 然後搜尋Bug ID 8012547</a>.</p> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=codeCacheHealthCheck，type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>資源搜尋路徑錯誤</td>
   <td><p>檢查路徑中是否有任何資源 <code>/apps/foundation/components/primary</code> 和：</p>
    <ul>
     <li>如果下有子節點，則傳回警告 <code>/apps/foundation/components/primary</code></li>
    </ul> <p>此健康狀態檢查的MBean為 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck：name=resourceSearchPathErrorHealthCheck，type=HealthCheck</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 健康狀態檢查設定 {#health-check-configuration}

根據預設，對於現成可用的AEM執行個體，健康情況檢查每60秒執行一次。

您可以設定 **期間** 使用 [OSGi設定](/help/sites-deploying/configuring-osgi.md) **查詢健康狀態檢查設定** (com.adobe.granite.queries.impl.hc.QueryHealthCheckMetrics)。

## 使用Nagios進行監視 {#monitoring-with-nagios}

健康情況檢查儀表板可以透過Granite JMX Mbeans與Nagios整合。 以下範例說明如何新增一項檢查，顯示執行AEM之伺服器上已使用的記憶體。

1. 在監視伺服器上設定並安裝Nagios。
1. 接著，安裝Nagios遠端外掛程式執行程式(NRPE)。

   >[!NOTE]
   >
   >如需如何在系統上安裝Nagios和NRPE的詳細資訊，請參閱 [Nagios檔案](https://library.nagios.com/library/products/nagios-core/manuals//).

1. 新增AEM伺服器的主機定義。 您可以透過Nagios XI Web Interface，使用Configuration Manager來完成這項工作：

   1. 開啟瀏覽器並指向Nagios伺服器。
   1. 按下 **設定** 上方功能表中的按鈕。
   1. 在左窗格中，按下 **核心設定管理員** 在 **進階設定**.
   1. 按下 **主機** 連結至 **監視** 區段。
   1. 新增主機定義：

   ![chlimage_1-118](assets/chlimage_1-118.png)

   以下是主機設定檔案的範例，以備您使用Nagios Core時使用：

   ```xml
   define host {
      address 192.168.0.5
      max_check_attempts 3
      check_period 24x7
      check-command check-host-alive
      contacts admin
      notification_interval 60
      notification_period 24x7
   }
   ```

1. 在AEM伺服器上安裝Nagios和NRPE。
1. 安裝 [check_http_json](https://github.com/phrawzty/check_http_json) 外掛程式。
1. 在兩個伺服器上定義一般JSON檢查命令：

   ```xml
   define command{
   
       command_name    check_http_json-int
   
       command_line    /usr/lib/nagios/plugins/check_http_json --user "$ARG1$" --pass "$ARG2$" -u 'https://$HOSTNAME$:$ARG3$/$ARG4$' -e '$ARG5$' -w '$ARG6$' -c '$ARG7$'
   
   }
   ```

1. 新增AEM伺服器上已使用記憶體的服務：

   ```xml
   define service {
   
       use generic-service
   
       host_name my.remote.host
   
       service_description AEM Author Used Memory
   
       check_command  check_http_json-int!<cq-user>!<cq-password>!<cq-port>!system/sling/monitoring/mbeans/java/lang/Memory.infinity.json!{noname}.mbean:attributes.HeapMemoryUsage.mbean:attributes.used.mbean:value!<warn-threshold-in-bytes>!<critical-threshold-in-bytes>
   
       }
   ```

1. 檢查您的Nagios儀表板是否有新建立的服務：

   ![chlimage_1-119](assets/chlimage_1-119.png)

## 診斷工具 {#diagnosis-tools}

「操作控制面板」也提供診斷工具的存取權，這些工具可協助尋找和疑難排解健康情況檢查控制面板所產生警告的根本原因，並提供系統操作員的重要除錯資訊。

其最重要的功能包括：

* 記錄訊息分析器
* 存取棧積和執行緒傾印的功能
* 請求和查詢效能分析器

您可以前往「 」，存取「診斷工具」畫面 **工具 — 作業 — 診斷** 從AEM歡迎畫面。 您也可以直接存取下列URL來存取畫面： `https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### 記錄訊息 {#log-messages}

記錄訊息使用者介面預設會顯示所有ERROR訊息。 如果您想要顯示更多日誌訊息，請以適當的日誌層級設定日誌程式。

記錄訊息使用記憶體中的記錄附加器，因此與記錄檔無關。 另一個後果是變更此UI中的記錄層級不會變更記錄到傳統記錄檔案中的資訊。 在此UI中新增和移除記錄器只會影響記憶體記錄器。 此外，變更記錄器設定會反映在記憶體記錄器的未來。 已記錄且不再相關的專案不會刪除，但日後不會再記錄類似的專案。

您可以從UI的左上角齒輪按鈕提供記錄器設定，以設定要記錄的內容。 在那裡，您可以新增、移除或更新記錄器設定。 記錄器設定是由 **記錄層級** （警告/資訊/偵錯）及 **篩選器名稱**. 此 **篩選器名稱** 具有篩選記錄日誌訊息來源的角色。 或者，如果記錄器應擷取指定層級的所有記錄訊息，則篩選器名稱應為&quot;**根**「。 設定記錄器的層級，會觸發擷取層級等於或高於指定層級的所有訊息。

範例：

* 如果您計畫擷取所有 **錯誤** 訊息 — 不需要設定。 預設會擷取所有ERROR訊息。
* 如果您計畫擷取所有 **錯誤**， **警告** 和 **資訊** messages — 記錄器名稱應設為： &quot;**根**&quot;，而記錄器層級為： **資訊**.

* 如果您打算擷取來自特定套件（例如com.adobe.granite）的所有訊息，記錄器名稱應設為： &quot;com.adobe.granite&quot;。 而且，記錄器層級設定為： **偵錯** (這麼做會擷取所有 **錯誤**， **警告**， **資訊**、和 **偵錯** 訊息)，如下圖所示。

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>您不能設定記錄器名稱，以透過指定的篩選器僅擷取錯誤訊息。 依預設，會擷取所有ERROR訊息。

>[!NOTE]
>
>記錄訊息使用者介面未反映實際的錯誤記錄。 除非您在UI中設定其他型別的記錄訊息，否則您只會看到錯誤訊息。 如需如何顯示特定記錄訊息，請參閱上述指示。

>[!NOTE]
>
>診斷頁面中的設定不會影響記錄到記錄檔的內容，反之亦然。 因此，雖然錯誤記錄可能會擷取INFO訊息，但您可能會在記錄訊息UI中看不到。 此外，透過UI也可以從特定套件擷取DEBUG訊息，而不會影響錯誤記錄。 如需如何設定記錄檔的詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md).

>[!NOTE]
>
>**使用AEM 6.4**，維護任務會立即從INFO層級以詳細資訊豐富的格式登出。 此工作流程可讓您更清楚地瞭解維護任務的狀態。
>
>如果您使用協力廠商工具（例如Splunk）來監控和回應維護任務活動，您可以使用以下記錄陳述式：

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### 要求效能 {#request-performance}

「要求效能」頁面可讓您分析處理的最慢的頁面要求。 此頁面上只會註冊內容要求。 更具體來說，會擷取下列請求：

1. 要求存取下的資源 `/content`
1. 要求存取下的資源 `/etc/design`
1. 具有下列專案的請求： `".html"` 副檔名

![chlimage_1-122](assets/chlimage_1-122.png)

頁面隨即顯示：

* 提出要求的時間
* URL和要求方法
* 持續時間（毫秒）

依預設，會擷取最慢的20個頁面請求，但可以在Configuration Manager中修改限制。

### 查詢效能 {#query-performance}

「查詢效能」頁面可讓您分析系統執行的最慢查詢。 此資訊由JMX Mbean中的存放庫提供。 在Jackrabbit中， `com.adobe.granite.QueryStat` JMX Mbean提供此資訊，而在Oak存放庫中，此資訊由提供 `org.apache.jackrabbit.oak.QueryStats.`

頁面隨即顯示：

* 進行查詢的時間
* 查詢的語言
* 查詢的發出次數
* 查詢的陳述式
* 持續時間（毫秒）

![chlimage_1-123](assets/chlimage_1-123.png)

### 說明查詢 {#explain-query}

對於任何特定查詢，Oak會嘗試根據下方的存放庫中定義的Oak索引，找出最佳執行方式 **oak：index** 節點。 根據查詢的不同，Oak可能會選擇不同的索引。 瞭解Oak如何執行查詢是最佳化查詢的第一步。

Explain Query是一種說明Oak如何執行查詢的工具。 您可以前往「 」存取 **工具 — 作業 — 診斷** 從AEM歡迎畫面。 然後，按一下 **查詢效能** 並切換至 **說明查詢** 標籤。

**功能**

* 支援Xpath、JCR-SQL和JCR-SQL2查詢語言
* 報告所提供查詢的實際執行時間
* 偵測緩慢的查詢，並就可能緩慢的查詢發出警告
* 報告用於執行查詢的Oak索引
* 顯示實際Oak查詢引擎說明
* 提供慢速和熱門查詢的點按載入清單

進入Explain查詢UI後，輸入查詢，然後按 **說明** 按鈕：

![chlimage_1-124](assets/chlimage_1-124.png)

「查詢說明」區段中的第一個專案是實際說明。 說明會顯示用來執行查詢的索引型別。

第二個專案是執行計畫。

勾選 **包含執行時間** 方塊中也會顯示執行查詢的時間。 此 **包含節點計數** 選項會報告節點計數。 該報告會提供詳細資訊，可用於為您的應用程式或部署最佳化索引。

![chlimage_1-125](assets/chlimage_1-125.png)

### 索引管理員 {#the-index-manager}

Index Manager的目的是方便索引管理，例如維護索引或檢視其狀態。

從「歡迎畫面」前往**工具 — 作業 — 診斷**，然後按一下 **索引管理員** 按鈕。

您也可以從以下URL直接存取： `https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![index_manager](assets/index_manager.png)

UI可用來篩選表格中的索引，方法是在畫面左上角的搜尋方塊中輸入篩選條件。

### 下載狀態ZIP {#download-status-zip}

這個動作會觸發下載壓縮檔，其中包含有關系統狀態和設定的實用資訊。 封存包含執行個體設定、套件組合清單、OSGI、Sling量度和統計資料，可能會產生大型檔案。 您可以使用來減少大型狀態檔案的影響 **下載狀態ZIP**&#x200B;視窗。 視窗可從下列位置存取：**AEM >工具>作業>診斷>下載狀態ZIP。**

在此視窗中，您可以選取要匯出的專案（記錄檔和/或對話串傾印），以及相對於目前日期包含在下載中的記錄天數。

![download_status_zip](assets/download_status_zip.png)

### 下載執行緒傾印 {#download-thread-dump}

此動作會觸發下載zip ，其中包含系統中存在的對話串的相關資訊。 會提供每個執行緒的相關資訊，例如其狀態、類別載入器以及棧疊追蹤。

### 下載棧積傾印 {#download-heap-dump}

您可以下載棧積的快照以便稍後分析。 此動作會觸發下載大型（數百MB）檔案。

## 自動維護任務 {#automated-maintenance-tasks}

「自動維護任務」頁面可供您檢視及追蹤排定定期執行的建議維護任務。 這些工作已與「健康情況檢查」系統整合。 任務也可以從介面手動執行。

若要前往操作控制面板中的「維護」頁面，請從AEM歡迎畫面，前往 **工具 — 作業 — 控制面板 — 維護**，或直接追蹤此連結：

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

「操作儀表板」中有以下工作：

1. 此 **修訂清除**&#x200B;任務，位於 **每日維護期間** 功能表。
1. 此 **Lucene二進位清理** 任務，位於 **每日維護期間** 功能表。
1. 此 **工作流程清除** 任務，位於 **每週維護期間** 功能表。
1. 此 **資料存放區記憶體回收** 任務，位於 **每週維護期間** 功能表。
1. 此 **稽核記錄維護** 任務，位於 **每週維護期間** 功能表。
1. 此 **版本清除維護** 任務，位於 **每週維護期間** 功能表。

每日維護期間的預設時間為凌晨2:00至下午5:00。設定在每週維護期間執行的工作，會在星期六上午1:00到凌晨2:00之間執行。

您也可以按兩個維護卡片上的齒輪圖示來設定計時：

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>自AEM 6.1起，現有的維護時段也可設定為每月執行。

### 修訂清理 {#revision-clean-up}

如需有關執行修訂清除的詳細資訊， [請參閱此專屬文章](/help/sites-deploying/revision-cleanup.md).

### Lucene 二進位清理 {#lucene-binaries-cleanup}

使用Lucene二進位檔案清理工作，您可以清除Lucene二進位檔案並降低執行中的資料存放區大小要求。 Lucene的二進位流失率會每天回收，而非先前依賴成功的專案 [資料存放區記憶體回收](/help/sites-administering/data-store-garbage-collection.md) 執行。

雖然開發維護任務是為了減少與Lucene相關的修訂垃圾，但在執行任務時普遍提高了效率：

* 每週執行資料存放區記憶體回收工作可以更快完成。
* 它也可能稍微改善整體AEM效能。

您可存取Lucene二進位清理工作，位置如下： **AEM >工具>作業>維護>每日維護視窗> Lucene二進位清理**.

### 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

如需資料存放區記憶體回收的詳細資訊，請參閱專用 [檔案頁面](/help/sites-administering/data-store-garbage-collection.md).

### 工作流程清除 {#workflow-purge}

您也可以從維護控制面板中清除工作流程。 若要執行「工作流程永久刪除」作業，請執行下列步驟：

1. 按一下 **每週維護期間** 頁面。
1. 在下一頁中，按一下 **播放** 在 **工作流程清除** 卡片。

>[!NOTE]
>
>如需有關工作流程維護的詳細資訊，請參閱 [此頁面](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances).

### 稽核記錄維護 {#audit-log-maintenance}

有關稽核記錄維護，請參閱 [個別的檔案頁面。](/help/sites-administering/operations-audit-log.md)

### 版本清除 {#version-purge}

您可以排定「版本永久刪除」維護作業，以自動刪除舊版本。 此動作將手動使用 [版本清除工具](/help/sites-deploying/version-purging.md). 您可以存取「 」，以排程並設定「版本永久刪除」工作 **工具>作業>維護>每週維護視窗** 並依照下列步驟進行：

1. 按一下&#x200B;**「新增」**。
1. 選擇 **版本清除** （從下拉式功能表）。

   ![version_purge_maintenancetask](assets/version_purge_maintenancetask.png)

1. 若要設定「版本清除」工作，請按一下 **齒輪** 圖示新建立的「版本清除」維護卡片上。

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**使用AEM 6.4**，您可以停止「版本清除」維護任務，如下所示：

* 自動 — 如果排程的維護視窗在任務完成之前關閉，任務會自動停止。 當下一個維護視窗開啟時，它會繼續。
* 手動 — 若要手動停止工作，請在「版本清除」維護卡上，按一下 **停止** 圖示。 在下次執行時，工作將會安全地繼續。

>[!NOTE]
>
>停止維護工作表示暫停其執行而不會失去已進行中工作的追蹤。

>[!CAUTION]
>
>最佳化您應經常執行版本清除工作的存放庫大小。 當流量有限時，應該將任務排程在營業時間以外。

## 自訂維護任務 {#custom-maintenance-tasks}

自訂維護任務可以實作為OSGi服務。 由於維護任務基礎架構以Apache Sling的作業處理為基礎，因此維護任務必須實施Java™介面 ` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`. 此外，它必須宣告數個服務註冊屬性以偵測為維護任務，如下所示：

<table>
 <tbody>
  <tr>
   <td><strong>服務屬性名稱</strong><br /> </td>
   <td><strong>說明</strong></td>
   <td><strong>範例</strong><br /> </td>
   <td><strong>類型</strong></td>
  </tr>
  <tr>
   <td>granite.maintenance.isStoppable</td>
   <td>定義使用者是否可以停止工作的布林值屬性。 如果任務宣告它可停止，它必須在執行期間檢查它是否停止，然後相應地採取行動。 預設值為false。</td>
   <td>true</td>
   <td>選用</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>定義工作是否為必要且必須定期執行的布林值屬性。 如果任務為必要任務，但目前不在任何使用中的排程視窗中，則健康狀態檢查會報告此錯誤。 預設值為false。</td>
   <td>true</td>
   <td>選用</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>任務的唯一名稱 — 該名稱用於引用任務，只是簡單名稱。</td>
   <td>MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>granite.maintenance.title</td>
   <td>為此任務顯示的標題</td>
   <td>我的特殊維護任務</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>job.topics</td>
   <td>維護任務的唯一主題。<br /> Apache Sling作業處理會啟動具有此主題的作業，以執行維護任務，而當任務針對此主題註冊時，就會開始執行。<br /> 主題的開頭必須是 <i>com/adobe/granite/maintenance/job/</i></td>
   <td>com/adobe/granite/maintenance/job/MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
 </tbody>
</table>

除了上述服務屬性外， `process()` 方法 `JobConsumer` 介面必須透過新增應為維護任務執行的程式碼來實作。 提供的 `JobExecutionContext` 可用來輸出狀態資訊、檢查工作是否由使用者停止並建立結果（成功或失敗）。

如果維護任務不應該在所有安裝上執行（例如，只應在發佈執行個體上執行），您可以透過新增來讓服務需要設定為作用中 `@Component(policy=ConfigurationPolicy.REQUIRE)`. 然後，您可以根據設定將設定標籤為從屬於存放庫中的執行模式。 如需詳細資訊，請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository).

以下是自訂維護任務的範例，該任務會從過去24小時內修改過的可設定暫存目錄中刪除檔案：

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experiencemanager-java-maintenancetask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample)- [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

部署服務後，它會公開至操作控制面板UI。 您可以將其新增到其中一個可用的維護排程：

![chlimage_1-127](assets/chlimage_1-127.png)

此動作會在/apps/granite/operations/config/maintenance/新增對應的資源`schedule`/`taskname`. 如果工作依執行模式而定，必須使用該維護工作必須啟動的執行模式值在該節點上設定屬性granite.operations.conditions.runmode。

## 系統綜覽 {#system-overview}

此 **系統總覽儀表板** 顯示AEM執行個體的組態、硬體及健康情況的高階概觀。 系統健康狀態是透明的，所有資訊都會彙總在單一儀表板中。

>[!NOTE]
>
>您也可以 [觀看此影片](https://video.tv.adobe.com/v/21340) 以瞭解「系統總覽儀表板」的簡介。

### 如何存取 {#how-to-access}

若要存取系統總覽儀表板，請導覽至 **「工具」>「作業」>「系統概述」**.

![system_overview_dashboard](assets/system_overview_dashboard.png)

### 說明系統總覽儀表板 {#system-overview-dashboard-explained}

下表說明「系統總覽儀表板」中顯示的所有資訊。 當沒有可顯示的相關資訊（例如，備份未進行中，沒有重要的健康情況檢查）時，個別區段會顯示「沒有專案」訊息。

您也可以下載 `JSON` 按一下「 」以摘要儀表板資訊 **下載** 按鈕來顯示控制板右上角的按鈕。 此 `JSON` 端點為 `/libs/granite/operations/content/systemoverview/export.json` 並且可用於 `curl` 外部監視指令碼。

<table>
 <tbody>
  <tr>
   <td><strong>區段</strong></td>
   <td><strong>顯示哪些資訊</strong></td>
   <td><strong>何時重要</strong></td>
   <td><strong>連結至</strong></td>
  </tr>
  <tr>
   <td>健康狀態檢查</td>
   <td>
    <ul>
     <li>處於嚴重狀態的檢查清單</li>
     <li>處於警告狀態的檢查清單</li>
    </ul> </td>
   <td>以視覺顯示：<br />
    <ul>
     <li>嚴重檢查的紅色標籤</li>
     <li>用於警告檢查的橙色標籤</li>
    </ul> </td>
   <td>
    <ul>
     <li>健康狀態報表頁面</li>
    </ul> </td>
  </tr>
  <tr>
   <td>維護任務</td>
   <td>
    <ul>
     <li>失敗的任務清單</li>
     <li>目前正在執行的工作清單</li>
     <li>上次執行成功的作業清單</li>
     <li>從未執行過的作業清單</li>
     <li>未排程的工作清單</li>
    </ul> </td>
   <td><p>以視覺顯示：</p>
    <ul>
     <li>失敗任務的紅色標籤</li>
     <li>用於執行任務的橘色標籤（因為這些可能會影響效能）</li>
     <li>每個其他狀態的灰色標籤</li>
    </ul> </td>
   <td>
    <ul>
     <li>維護作業頁面</li>
    </ul> </td>
  </tr>
  <tr>
   <td>系統</td>
   <td>
    <ul>
     <li>作業系統和作業系統版本(例如macOS X)</li>
     <li>系統平均負載，擷取自 <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">OperatingSystemMXBeanusable</a></li>
     <li>磁碟空間（位於主目錄所在的分割區）</li>
     <li>棧積上限，由傳回 <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">MemoryMXBean</a></li>
    </ul> </td>
   <td>N/A</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>執行個體</td>
   <td>
    <ul>
     <li>AEM版本</li>
     <li>執行模式清單</li>
     <li>執行個體開始的日期</li>
    </ul> </td>
   <td>N/A</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>存放庫</td>
   <td>
    <ul>
     <li>Oak版本</li>
     <li>節點存放區型別（區段Tar或檔案）
      <ul>
       <li>如果型別是document，則會顯示檔案存放區的型別（RDB或Mongo）</li>
      </ul> </li>
     <li>如果有自訂資料存放區：
      <ul>
       <li>若為檔案資料存放區，則會顯示路徑</li>
       <li>若為S3資料存放區，會顯示S3儲存貯體的名稱</li>
       <li>如果是共用的S3資料存放區，則會顯示S3儲存貯體的名稱</li>
       <li>對於Azure資料存放區，會顯示容器</li>
      </ul> </li>
     <li>如果沒有自訂外部資料存放區，則會顯示一則訊息，指出此事實</li>
    </ul> </td>
   <td>N/A</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>發佈代理程式</td>
   <td>
    <ul>
     <li>具有封鎖佇列的代理程式清單</li>
     <li>設定錯誤的代理程式清單（「設定錯誤」）</li>
     <li>佇列處理暫停的代理程式清單</li>
     <li>閒置代理程式清單</li>
     <li>執行中代理程式（目前正在處理專案）的清單</li>
    </ul> </td>
   <td><p>以視覺顯示：</p>
    <ul>
     <li>封鎖的代理程式或設定錯誤的紅色標籤</li>
     <li>暫停代理的橘色標籤</li>
     <li>用於暫停、閒置或執行中的代理程式的灰色標籤<br /> </li>
    </ul> </td>
   <td>發佈頁面<br /> </td>
  </tr>
  <tr>
   <td>複寫代理程式</td>
   <td>
    <ul>
     <li>具有封鎖佇列的代理程式清單</li>
     <li>閒置代理程式清單</li>
     <li>執行中代理程式（目前正在處理專案）的清單</li>
    </ul> </td>
   <td><p>以視覺顯示：<br /> </p>
    <ul>
     <li>已封鎖代理程式的紅色標籤</li>
     <li>暫停代理程式的灰色標籤</li>
    </ul> </td>
   <td>復寫頁面</td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td>
    <ul>
     <li>工作流程工作：
      <ul>
       <li>失敗的工作流程工作數目（如果有的話）</li>
       <li>已取消的工作流程工作數目（如果有的話）</li>
      </ul> </li>
    </ul>
    <ul>
     <li>工作流程計數 — 指定狀態的工作流程數量（如果有的話）：
      <ul>
       <li>執行中</li>
       <li>失敗</li>
       <li>已暫停</li>
       <li>已中止</li>
      </ul> </li>
    </ul> <p>會針對上方呈現的每個狀態執行查詢，限製為400毫秒。 在400毫秒時，會顯示截至該時間所取得的專案數。</p> </td>
   <td><p>未解譯：</p>
    <ul>
     <li>當有工作流程和工作處於非預期狀態時，使用者應進行調查。</li>
    </ul> </td>
   <td>工作流程失敗頁面</td>
  </tr>
  <tr>
   <td>Sling 工作</td>
   <td><p>Sling工作計數 — 指定狀態的工作數（如果有的話）：</p>
    <ul>
     <li>失敗</li>
     <li>已排入佇列</li>
     <li>已取消</li>
     <li>作用中</li>
    </ul> </td>
   <td><p>未解譯：</p>
    <ul>
     <li>當有工作處於非預期狀態或具有高計數時，使用者應進行調查。</li>
    </ul> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>預估節點計數</td>
   <td><p>預估數量：</p>
    <ul>
     <li>頁面</li>
     <li>資產</li>
     <li>標記</li>
     <li>可授權專案</li>
     <li>節點總數<br /> </li>
    </ul> <p>節點總數是從nodeCounterMBean取得，其餘的統計資料是從IndexInfoService取得。</p> </td>
   <td>N/A</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>備份</td>
   <td>顯示「線上備份進行中」（如果有的話）。</td>
   <td>N/A</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>索引</td>
   <td><p>顯示:</p>
    <ul>
     <li>"正在編制索引"</li>
     <li>"正在進行查詢"</li>
    </ul> <p>如果索引或查詢對話串存在於對話串傾印中。</p> </td>
   <td>N/A</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>
