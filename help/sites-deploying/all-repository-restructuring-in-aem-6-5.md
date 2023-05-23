---
title: 6.5版中的通AEM用儲存庫重組
seo-title: Common Repository Restructuring in AEM 6.5
description: 瞭解如何進行必要的更改，以便遷移到6.5版中AEM的新儲存庫結構，該結構適用於所有區AEM域。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 that are common for all areas of AEM.
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
source-git-commit: 3f64bd7f5b4eb43aeefb9277a94e10ef1f0df59c
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 2%

---

# 6.5版中的通AEM用儲存庫重組 {#common-repository-restructuring-in-aem}

如父代中所述 [6.5中的AEM儲存庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級到AEM6.5的客戶應使用此頁面評估與儲存庫更改相關的工作量，這些更改可能會影響所有解決方案。 某些更改需要在6.5升AEM級過程中進行工作，而其他更改則可以推遲到以後升級。

**使用6.5升級**

* [ContextHub 組態](#contexthub-6.5)
* [工作流程例項](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [工作流程模型](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [工作流程啟動器](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [工作流指令碼](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**未來升級前**

* [ContextHub 組態](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [經典Cloud Services設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [經典儀表板設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [經典報表設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [預設設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [AdobeDTM JavaScript終結點](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [AdobeDTM Web掛接終結點](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [收件箱任務](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [多站點管理器藍圖配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [項AEM目儀表板小工具配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [複製通知電子郵件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [標記](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [翻譯雲端服務](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [翻譯語言](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [翻譯規則](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [翻譯小部件客戶端庫](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [樹激活Web控制台](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [供應商轉換連接器Cloud Services](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [工作流通知電子郵件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 使用6.5升級 {#with-upgrade}

### ContextHub 組態 {#contexthub-6.5}

從AEM6.4開始，沒有預設的ContextHub配置。 因此，在站點的根級別a `cq:contextHubPathproperty` 應設定為指示應使用哪種配置。

1. 導航到站點的根。
1. 開啟根頁的頁屬性，然後選擇「個性化」頁籤。
1. 在「上下文路徑」欄位中，輸入您自己的ContextHub配置路徑。

此外，在ContextHub配置中， `sling:resourceType` 需要更新為相對而不是絕對。

1. 在CRX DE Lite中開啟ContextHub配置節點的屬性，例如 `/apps/settings/cloudsettings/legacy/contexthub`
1. 更改 `sling:resourceType` 從 `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` 至 `granite/contexthub/cloudsettings/components/baseconfiguration`

即 `sling:resourceType` ContextHub配置必須是相對的，而不是絕對的。

### 工作流程模型 {#workflow-models}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的工作流模型都必須遷移到/conf/global/workflow/models。</p>
    <ol>
     <li>將修改的工作流模型部署到本AEM地6.5開發實例中，以便它們存在於「上一個」位置。</li>
     <li>使用「工作流模型編輯AEM器」(Workflow Model Editor)AEM &gt;「工具」(Tools)&gt;「工作流」(Workflow)&gt;「模型」(Models)編輯「工作流模型」。</li>
     <li>遷移修改的AEM提供的工作流模型時
      <ol>
       <li>開啟「工作流模型編輯器」後，修改瀏覽器的地址URL，並將路徑段/libs/settings/workflow/models替換為/etc/workflow/models。
        <ul>
         <li>例如，更改： <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> 至 <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>在工作流模型編輯器中啟用「編輯」模式，該模式會將工作流模型定義複製到/conf/global/workflow/models。</li>
     <li>按一下「同步」按鈕，將更改同步到/var/workflow/models下的「運行時工作流模型」。</li>
     <li>導出工作流模型(/conf/global/workflow/models/&lt;workflow-model&gt;)和運行時工作流模型(/var/workflow/models/&lt;workflow-model&gt;並融入到項AEM目中。
      <ol>
       <li>例如，導出：
        <ul>
         <li><code>/conf/global/settings/workflow/models/dam/my_workflow_model</code> 和 </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>工作流模型解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>因此，如果要保留AEM，則保留在「上一個」位置中的提供的工作流模型的任何自定義項都必須移動到/conf/global/settings/workflow/models，否則，它們將被/libs/settings/workflow/models中AEM提供的工作流模型定義取代。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流程例項 {#workflow-instances}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>無需執行任何操作即可與新位置對齊。</p> <p>歷史工作流實例可以安全地繼續駐留在上一個位置，並且新工作流實例將在新位置建立。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>中的任何顯式路徑引用
    <code>
     custom
    </code> 「上一個位置」的代碼也應考慮「新建位置」。 建議重新構造此代碼以使用工AEM作流API。</td>
  </tr>
 </tbody>
</table>

### 工作流程啟動器 {#workflow-launchers}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>必須將任何新的或修改的工作流啟動程式遷移到 <code>/conf/global/workflow/launcher/config</code>。</p>
    <ol>
     <li>將任何新的或修改的工作流啟動程式配置從上一位置複製到新位置(<code>/conf/global</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>工作流啟動程式解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>因此，必須將AEM保留在上一個位置的所提供工作流啟動程式的任何自定義內容移動到新位置(<code>/conf/global/settings/workflow/launcher</code> 如果要保留，否則將被中提供的AEM工作流啟動程式定義取代 <code>/libs/settings/workflow/launcher</code>。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流指令碼 {#workflow-scripts}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的工作流指令碼都必須遷移到新位置，並且引用的工作流模型將更新以反映新位置。</p>
    <ol>
     <li>將任何新的或修改的工作流指令碼從上一位置複製到新位置。<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> 應在供應鏈中維護。</li>
      </ul> </li>
     <li>更新對工作流模型中上一個位置的工作流指令碼的任何引用，以指向新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>AEM 6.4 SP1在發佈時，使此重組可推遲到6.5
     <code>
      upgrade
     </code>。</p> <p>如果在6AEM.4 SP1發佈AEM之前升級到6.4，則此重組應作為升級項目的一部分執行。 如果不這樣做，編輯和保存引用「上一位置」中指令碼的工作流步驟將完全從「工作流步驟」中刪除「工作流指令碼」引用，並且只有「新位置」中的「工作流指令碼」才可在指令碼選擇下拉清單中使用。</p> </td>
  </tr>
 </tbody>
</table>

## 未來升級前 {#prior-to-upgrade}

### ContextHub 組態 {#contexthub-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的ContextHub配置都必須遷移到新位置，並且必須更新引用的AEM Sites頁以反映新位置。</p>
    <ol>
     <li>將任何新的或已修改的ContextHub配置從上一個位置複製到新位置。</li>
     <li>將適用的AEM配置與內AEM容層次關聯。
      <ol>
       <li><strong>AEM Sites頁面層次結構(通過AEM Sites&gt;頁面&gt;頁面屬性&gt;高級頁籤&gt;雲配置</strong>。</li>
      </ol> </li>
     <li>將所有遷移的舊版ContextHub配置與上述內容層AEM次取消關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 經典Cloud Services設計 {#classic-cloud-services-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理且未通過設計對話框在運行時寫入的任何設計。</p>
    <ol>
     <li>將設計從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶端庫</a> 與 <code>allowProxy = true</code>。</li>
     <li>更新對中上一個位置的引用 <span class="code">
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span> 屬性。</li>
     <li>更新引用上一個位置的任何頁面以使用新的客戶端庫類別（這需要更新頁面實施代碼）。</li>
     <li>更新AEMDispatcher規則，以允許通過/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改的運行時。</p>
    <ul>
     <li>不要將可創作的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 經典儀表板設計 {#classic-dashboards-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理且未通過設計對話框在運行時寫入的任何設計。</p>
    <ol>
     <li>將設計從「上一位置」複製到「新位置」(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶端庫</a> 與 <code>allowProxy = true</code>。</li>
     <li>更新對中上一個位置的引用
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 屬性。</li>
     <li>更新引用上一個位置的任何頁面以使用新的客戶端庫類別（這需要更新頁面實施代碼）。</li>
     <li>更新AEMDispatcher規則，以允許通過/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改的運行時。</p>
    <ul>
     <li>不要將可創作的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 經典報表設計 {#classic-reports-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理且未通過設計對話框在運行時寫入的任何設計。</p>
    <ol>
     <li>將設計從「上一位置」複製到「新位置」(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶端庫</a> 與 <code>allowProxy = true</code>。</li>
     <li>更新對中上一個位置的引用
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 屬性。</li>
     <li>更新引用上一個位置的任何頁面以使用新的客戶端庫類別（這需要更新頁面實施代碼）。</li>
     <li>更新AEMDispatcher規則，以允許通過/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改的運行時。</p>
    <ul>
     <li>不要將可創作的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 預設設計 {#default-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理且未通過設計對話框在運行時寫入的任何設計。</p>
    <ol>
     <li>將設計從「上一位置」複製到「新位置」(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶端庫</a> 與 <code>allowProxy = true</code>。</li>
     <li>更新對中上一個位置的引用
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 屬性。</li>
     <li>更新引用上一個位置的任何頁面以使用新的客戶端庫類別（這需要更新頁面實施代碼）。</li>
     <li>更新AEMDispatcher規則，以允許通過/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改的運行時。</p>
    <ul>
     <li>不要將可創作的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### AdobeDTM JavaScript終結點 {#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>不需要任何操作。</p> <p>公共先前位置用作專用新位置的代理終結點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### AdobeDTM Web掛接終結點 {#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>不需要任何操作。</p> <p>公共先前位置用作專用新位置的代理終結點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 收件箱任務 {#inbox-tasks}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>使用 <strong>收件箱清除維護任務</strong> 以根據需要從上一個位置刪除舊任務。</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>將任務遷移到新位置不需要任何操作。</p>
    <ul>
     <li>「上一個位置」(Previous Location)中存在的任務繼續可用，並且正常工作。</li>
     <li>在「新建位置」(New Location)中建立「新任務」(New Tasks)。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 多站點管理器藍圖配置 {#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong><em></em>上一個位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>
    <ol>
     <li>從中複製自定義配置 <code>/etc/blueprints</code> 至 <code>/apps/msm</code>。</li>
     <li>移除 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 項AEM目儀表板小工具配置 {#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或已修AEM改的項目儀表板小工具配置都必須遷移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>將任何新的或已修AEM改的項目儀表板小工具配置從上一個位置複製到新位置(<code>/apps</code>)。
      <ol>
       <li>不複製未修改AEM的項目儀表板小工具配置，因為新位置中現在存在這些配置(<code>/libs</code>)。</li>
      </ol> </li>
     <li>更新引AEM用「上一個位置」的任何「項目」模板以指向相應的新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>如果應AEM用了6.4相容性包，則在刪除相容性包時必須執行儲存庫對齊活動。</td>
  </tr>
 </tbody>
</table>

### 複製通知電子郵件模板 {#replication-notification-e-mail-template}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的複製通知電子郵件模板都必須遷移到新位置(<code>/apps</code>)</p>
    <ol>
     <li>將任何新的或修改的複製通知電子郵件模板從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>從上一個位置刪除任何遷移的複製通知電子郵件模板。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>唯一支援的新複製通知電子郵件模板是支援新語言環境。</p> <p>複製通知電子郵件模板解析按以下順序進行：</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.replication</code></li>
     <li><code class="code">/apps/settings/notification-templates/com.day.cq.replication
        </code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.replication</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 標記 {#tags}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>必須將所有標籤遷移到 <code>/content/cq:tags</code>。</p>
    <ol>
     <li>將所有標籤從上一個位置複製到新位置。</li>
     <li>從上一個位置刪除所有標籤。</li>
     <li>通過Web控AEM制台，在以下位置重新啟動Day Compules 5 Tagging OSGi捆綁包 <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> 用於AEM識別「新建位置」包含內容，應使用。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>重新啟動日公報標籤OSGi捆綁包將僅在上一個位置為空時將新位置註冊為標籤根。</p> <p>遷移到新位置後，對上一個位置的引用將繼續工作，以獲得利用AEMTagManager API進行標籤解析的所有功能。</p> <p>顯式引用路徑的任何自定義代碼 <code>/etc/tags</code> 必須更新為 <span class="code">/內容/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>，或最好重寫以與此遷移一起利用TagManager Java API。</p> </td>
  </tr>
 </tbody>
</table>

### 翻譯雲端服務 {#translation-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的翻譯Cloud Services必須遷移到新位置(<code>/apps</code>。 <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>將上一個位置的現有配置遷移到新位置。
      <ul>
       <li>通過創作UI手動重新建立新的翻譯Cloud ServicesAEM配置，位於 <strong>工具&gt;Cloud Services&gt;翻譯Cloud Services</strong>。<br /> 或 </li>
       <li>將任何新的翻譯Cloud Services配置從上一個位置複製到新位置(<code>/apps</code>。 <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</li>
      </ul> </li>
     <li>將適用的AEM配置與內AEM容層次關聯。
      <ol>
       <li>AEM Sites頁層次 <strong>AEM Sites&gt;頁面&gt;頁面屬性&gt;高級頁籤&gt;雲配置</strong>。</li>
       <li>體驗AEM片段層次結構 <strong>體驗AEM片段&gt;體驗片段&gt;屬性&gt;Cloud Services頁籤&gt;雲配置</strong>。</li>
       <li>體驗AEM片段資料夾層次結構 <strong>體驗AEM片段&gt;資料夾&gt;屬性&gt;Cloud Services頁籤&gt;雲配置</strong>。<br /> </li>
       <li>AEM Assets資料夾層次結構 <strong>AEM Assets&gt;資料夾&gt;資料夾屬性&gt;Cloud Services頁籤&gt;配置</strong>。</li>
       <li>項AEM目 <strong>AEM項目&gt;項目&gt;項目屬性&gt;高級頁籤&gt;雲配置</strong>。</li>
      </ol> </li>
     <li>將所有遷移的舊版翻譯Cloud Services與上述內容層AEM次取消關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯Cloud Services解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>遷移的翻譯Cloud Services必須AEM與6.4相容。</p> </td>
  </tr>
 </tbody>
</table>

### 翻譯語言 {#translation-languages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的翻譯語言定義都要求將所有翻譯語言定義遷移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>如果對翻譯語言定義進行了任何添加或修改，則將所有翻譯語言定義從上一個位置複製到新位置(<code>/apps</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯語言路徑解析按以下順序進行：</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>此解析不支援合併覆蓋，這意味著解析的路徑必須包含所有支援的語言，並且不會從更高級的解析繼承支援的語言。</p> </td>
  </tr>
 </tbody>
</table>

### 翻譯規則 {#translation-rules}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>必須將修改的翻譯規則XML檔案遷移到新位置(<code>/apps</code>或 <code>/conf/global</code>)。</p> <p>1。將修改的「翻譯規則」XML檔案從上一個位置複製到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>複製轉換規則XML解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/global/settings/translation/rules/translation_rules.xml</code></li>
     <li><code class="code">/apps/settings/translation/rules/translation_rules.xml
        </code></li>
     <li><code class="code">/etc/workflow/models/translation/translation_rules.xml
        </code></li>
     <li><code>/libs/settings/translation/rules/translation_rules.xml</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 翻譯小部件客戶端庫 {#translation-widget-client-library}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理且未通過設計對話框在運行時寫入的任何設計。</p>
    <ol>
     <li>將設計從「上一位置」複製到「新位置」(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶端庫</a> 與 <code>allowProxy = true</code>。</li>
     <li>更新對中上一個位置的引用
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> 屬性。</li>
     <li>更新引用上一個位置的任何頁面以使用新的客戶端庫類別（這需要更新頁面實施代碼）。</li>
     <li>更新AEMDispatcher規則，以允許通過/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改的運行時。</p>
    <ul>
     <li>不要將可創作的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 樹激活Web控制台 {#tree-activation-web-console}

| **上一個位置** | `/etc/replication/treeactivation` |
|---|---|
| **新位置** | `/libs/replication/treeactivation` |
| **重組指導** | 不需要任何操作。 |
| **附註** | 樹激活Web控制台現在可通過 **工具>部署>複製>激活樹**。 |

{style="table-layout:auto"}

### 供應商轉換連接器Cloud Services {#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的供應商轉換連接器Cloud Services都必須遷移到新位置(<code>/apps</code>。 <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>將上一個位置中的現有配置遷移到新位置。
      <ul>
       <li>通過以下方式手動建立新的供應商翻譯連接器Cloud Services配置： <strong>在AEM「工具」&gt;「Cloud Services」&gt;「翻譯Cloud Services」中創作UI</strong>。<br /> 或 </li>
       <li>將任何新的供應商轉換連接器Cloud Services配置從上一個位置複製到新位置(<code>/apps</code>。 <code>/conf/global </code>或 <code>/conf/&lt;tenant&gt;</code>)。</li>
      </ul> </li>
     <li>將適用的AEM配置與內AEM容層次關聯。
      <ol>
       <li>AEM Sites頁層次 <strong>AEM Sites&gt;頁面&gt;頁面屬性&gt;高級頁籤&gt;雲配置</strong>。</li>
       <li>體驗AEM片段層次結構 <strong>體驗AEM片段&gt;體驗片段&gt;屬性&gt;Cloud Services頁籤&gt;雲配置</strong>。</li>
       <li>體驗AEM片段資料夾層次結構 <strong>體驗AEM片段&gt;資料夾&gt;屬性&gt;Cloud Services頁籤&gt;雲配置</strong>。</li>
       <li>AEM Assets資料夾層次結構 <strong>AEM Assets&gt;資料夾&gt;資料夾屬性&gt;Cloud Services頁籤&gt;配置</strong>。</li>
       <li>項AEM目 <strong>AEM項目&gt;項目&gt;項目屬性&gt;高級頁籤&gt;雲配置</strong>。</li>
      </ol> </li>
     <li>將所有遷移的舊版翻譯Cloud Services與上述內容層AEM次取消關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯Cloud Services解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流通知電子郵件模板 {#workflow-notification-email-templates}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何修改的工作流通知電子郵件模板必須遷移到新位置(<code>/conf/global</code>)。</p>
    <ol>
     <li>將任何修改的工作流通知電子郵件模板從上一個位置複製到新位置。</li>
     <li>從上一個位置刪除遷移的工作流通知電子郵件模板。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>工作流通知電子郵件模板解析按以下順序進行：</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流包 {#workflow-packages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>應將上一位置中的現有工作流包遷移到新位置。</p>
    <ol>
     <li>刪除上一個位置中未被其他內容引用且不需要的任何工作流包。</li>
     <li>在上一個位置移動未被其他內容引用但新位置中需要的任何工作流包。</li>
     <li>保留上一個位置中其他內容引用的任何工作流包。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>通過「經典UI Miscadmin」控制台建立的工作流包會保留在上一個位置，而其他所有包會保留到新位置。</p> <p>儲存在先前或未位置的工作流包可以通過Classic UI Miscadmin控制台進行管理。</p> </td>
  </tr>
 </tbody>
</table>
