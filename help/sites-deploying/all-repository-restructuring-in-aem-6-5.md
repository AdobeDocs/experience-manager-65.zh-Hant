---
title: AEM 6.5中的通用存放庫重新架構
description: 瞭解如何進行必要的變更，以移轉至AEM 6.5中適用於AEM所有區域的通用新存放庫結構。
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
solution: Experience Manager, Experience Manager Sites
feature: Upgrading
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2694'
ht-degree: 2%

---

# AEM 6.5中的通用存放庫重新架構 {#common-repository-restructuring-in-aem}

如父項所述 [AEM 6.5中的存放庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級至AEM 6.5的客戶應使用此頁面來評估與可能影響所有解決方案的存放庫變更相關聯的工作量。 在AEM 6.5升級程式期間，有些變更需要投入大量精力，而其他變更則可能延遲到未來升級。

**6.5版升級**

* [ContextHub 組態](#contexthub-6.5)
* [工作流程例項](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [工作流程模型](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [工作流程啟動器](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [工作流程指令碼](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**未來升級之前**

* [ContextHub 組態](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [傳統Cloud Service設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [傳統儀表板設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [傳統報表設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [預設設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [AdobeDTM JavaScript端點](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [AdobeDTM Web-Hook端點](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [收件匣任務](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [多站點管理員藍圖設定](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [AEM專案控制面板小工具設定](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [復寫通知電子郵件範本](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [標記](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [翻譯雲端服務](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [翻譯語言](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [翻譯規則](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [翻譯Widget使用者端資料庫](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [樹啟動Web主控台](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [廠商翻譯聯結器Cloud Service](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [工作流程通知電子郵件範本](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 6.5版升級 {#with-upgrade}

### ContextHub設定 {#contexthub-6.5}

從AEM 6.4開始，沒有預設的ContextHub設定。 因此，在網站的根層級上 `cq:contextHubPathproperty` 應設定以指出應使用哪個設定。

1. 導覽至網站的根目錄。
1. 開啟根頁面的頁面屬性，並選取個人化標籤。
1. 在Contexthub路徑欄位中，輸入您自己的ContextHub設定路徑。

此外，在ContextHub設定上， `sling:resourceType` 需要更新為相對而非絕對。

1. 在CRX DE Lite中開啟ContextHub設定節點的屬性，例如 `/apps/settings/cloudsettings/legacy/contexthub`
1. 變更 `sling:resourceType` 從 `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` 至 `granite/contexthub/cloudsettings/components/baseconfiguration`

即 `sling:resourceType` 的URL必須是相對的，而非絕對的。

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新的或修改過的工作流程模型必須移轉至/conf/global/workflow/models。</p>
    <ol>
     <li>將修改過的工作流程模型部署至本機AEM 6.5開發執行個體，讓這些模型存在於「先前位置」。</li>
     <li>在「AEM &gt;工具&gt;工作流程&gt;模型」中，使用「AEM工作流程模型編輯器」編輯工作流程模型。</li>
     <li>移轉修改的AEM提供的工作流程模型時
      <ol>
       <li>在「工作流程模型編輯器」開啟的狀態下，修改瀏覽器的位址URL，並將路徑區段/libs/settings/workflow/models取代為/etc/workflow/models。
        <ul>
         <li>例如，變更： <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/model</strong>/dam/update_asset.html</em> 至 <em>http://localhost:4502/editor.html<strong>/etc/workflow/model</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>啟用「工作流程模型編輯器」中的「編輯」模式，將工作流程模型定義複製到/conf/global/workflow/models。</li>
     <li>選取「同步」按鈕，將變更同步至/var/workflow/models下的「執行階段工作流程模型」。</li>
     <li>匯出兩個工作流程模型(/conf/global/workflow/models/&lt;workflow-model&gt;)和執行階段工作流程模型(/var/workflow/models/&lt;workflow-model&gt;)並整合至AEM專案。
      <ol>
       <li>例如，匯出：
        <ul>
         <li><code>/conf/global/settings/workflow/models/dam/my_workflow_model</code><br /> 和 </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>工作流程模型解析的順序如下：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>因此，如果想要保留AEM提供之工作流程模型的任何自訂專案，必須將其移至/conf/global/settings/workflow/models （先前位置），否則它們將會由AEM提供之/libs/settings/workflow/models中的工作流程模型定義取代。</p> </td>
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
   <td><strong>重組指南</strong></td>
   <td><p>無需任何動作即可與「新位置」對齊。</p> <p>歷史工作流程例項可以安全地繼續駐留在「先前位置」，而新的「工作流程例項」將會建立在「新位置」。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>中的任何明確路徑參照
    <code>
     custom
    </code> 先前位置的代碼也應說明新位置。 建議將此程式碼重構為使用AEM Workflow API。</td>
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
   <td><strong>重組指南</strong></td>
   <td><p>任何新的或修改過的工作流程啟動器都必須移轉至 <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>將任何新或修改的工作流程啟動器設定從上一個位置複製到新位置(<code>/conf/global</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>工作流程啟動器解析度的發生順序如下：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>因此，AEM提供之工作流程啟動器保留在先前位置的任何自訂都必須移至新位置(<code>/conf/global/settings/workflow/launcher</code> 如果要保留這些引數，否則將由AEM提供的工作流程啟動器定義取代。 <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### 工作流程指令碼 {#workflow-scripts}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新或修改的工作流程指令碼必須移轉到新位置，而且參考工作流程模型必須更新以反映新位置。</p>
    <ol>
     <li>將任何新或修改的工作流程指令碼從先前位置複製到新位置。<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> 應在SCM中維護。</li>
      </ul> </li>
     <li>更新工作流'b5'7b模型中先前位置對「工作流'b5'7b指令碼」的任何參照，以指向「新位置」。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>AEM 6.4 SP1在發行時使其可延遲至6.5
     <code>
      upgrade
     </code>.</p> <p>如果升級至AEM 6.4 SP1發行之前的AEM 6.4，此重組應該作為升級專案的一部分來執行。 如果不這樣做，編輯和儲存參考先前位置中指令碼的工作流程步驟將會從工作流程步驟中完全移除工作流程指令碼參考，而且指令碼選取下拉式清單中只有新位置的工作流程指令碼可用。</p> </td>
  </tr>
 </tbody>
</table>

## 未來升級之前 {#prior-to-upgrade}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新或修改的ContextHub設定都必須移轉至新位置，且參考AEM Sites頁面必須更新以反映新位置。</p>
    <ol>
     <li>將先前位置的任何新設定或修改的ContextHub設定複製到新位置。</li>
     <li>將適用的AEM設定與AEM內容階層建立關聯。
      <ol>
       <li><strong>透過AEM Sites &gt;頁面&gt;頁面屬性&gt;進階標籤&gt;雲端設定的AEM Sites頁面階層</strong>.</li>
      </ol> </li>
     <li>解除所有已移轉的舊版ContextHub設定與上述的AEM內容階層的關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 傳統Cloud Service設計 {#classic-cloud-services-designs}

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
   <td><strong>重組指南</strong></td>
   <td><p>對於任何在SCM中管理，且未透過設計對話方塊在執行階段寫入的設計。</p>
    <ol>
     <li>將設計從先前位置複製到新位置(<code>/apps</code>)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶庫</a> 替換為 <code>allowProxy = true</code>.</li>
     <li>更新中先前位置的參照 <span class="code">
       <code>
        cq
       </code>：
       <code>
        designPath
       </code></span> 屬性。</li>
     <li>更新任何參考先前位置的頁面，以使用新的使用者端程式庫類別（這需要更新頁面實施程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供使用者端資料庫。 Proxy servlet。</li>
    </ol> <p>針對任何未在SCM中管理的設計，以及透過「設計」對話方塊修改的執行時間。</p>
    <ul>
     <li>請勿將可作者設計移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 傳統儀表板設計 {#classic-dashboards-designs}

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
   <td><strong>重組指南</strong></td>
   <td><p>對於任何在SCM中管理，且未透過設計對話方塊在執行階段寫入的設計。</p>
    <ol>
     <li>將設計從先前位置複製到新位置(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶庫</a> 替換為 <code>allowProxy = true</code>.</li>
     <li>更新中先前位置的參照
      <code>
       cq
      </code>：
      <code>
       designPath
      </code> 屬性。</li>
     <li>更新任何參考先前位置的頁面，以使用新的使用者端程式庫類別（這需要更新頁面實施程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供使用者端資料庫。 Proxy servlet。</li>
    </ol> <p>針對任何未在SCM中管理的設計，以及透過「設計」對話方塊修改的執行時間。</p>
    <ul>
     <li>請勿將可作者設計移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 傳統報表設計 {#classic-reports-designs}

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
   <td><strong>重組指南</strong></td>
   <td><p>對於任何在SCM中管理，且未透過設計對話方塊在執行階段寫入的設計。</p>
    <ol>
     <li>將設計從先前位置複製到新位置(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶庫</a> 替換為 <code>allowProxy = true</code>.</li>
     <li>更新中先前位置的參照
      <code>
       cq
      </code>：
      <code>
       designPath
      </code> 屬性。</li>
     <li>更新任何參考先前位置的頁面，以使用新的使用者端程式庫類別（這需要更新頁面實施程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供使用者端資料庫。 Proxy servlet。</li>
    </ol> <p>針對任何未在SCM中管理的設計，以及透過「設計」對話方塊修改的執行時間。</p>
    <ul>
     <li>請勿將可作者設計移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
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
   <td><strong>重組指南</strong></td>
   <td><p>對於任何在SCM中管理，且未透過設計對話方塊在執行階段寫入的設計。</p>
    <ol>
     <li>將設計從先前位置複製到新位置(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶庫</a> 替換為 <code>allowProxy = true</code>.</li>
     <li>更新中先前位置的參照
      <code>
       cq
      </code>：
      <code>
       designPath
      </code> 屬性。</li>
     <li>更新任何參考先前位置的頁面，以使用新的使用者端程式庫類別（這需要更新頁面實施程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供使用者端資料庫。 Proxy servlet。</li>
    </ol> <p>針對任何未在SCM中管理的設計，以及透過「設計」對話方塊修改的執行時間。</p>
    <ul>
     <li>請勿將可作者設計移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### AdobeDTM JavaScript端點 {#adobe-dtm-javascript-endpoint}

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
   <td><strong>重組指南</strong></td>
   <td><p>不需要採取任何動作。</p> <p>先前的公用位置會作為私人新位置的Proxy端點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### AdobeDTM Web-Hook端點 {#adobe-dtm-web-hook-endpoint}

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
   <td><strong>重組指南</strong></td>
   <td><p>不需要採取任何動作。</p> <p>先前的公用位置會作為私人新位置的Proxy端點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 收件匣任務 {#inbox-tasks}

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
   <td><strong>重組指南</strong></td>
   <td>使用 <strong>收件匣清除維護任務</strong> 以視需要從先前位置移除舊任務。</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>將工作移轉至新位置不需要任何動作。</p>
    <ul>
     <li>「先前位置」中的工作仍可使用且正常運作。</li>
     <li>新任務即會在新位置中建立。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 多站點管理員藍圖設定 {#multi-site-manager-blueprint-configurations}

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
   <td><strong>重組指南</strong></td>
   <td>
    <ol>
     <li>自訂組態複製來源 <code>/etc/blueprints</code> 至 <code>/apps/msm</code>.</li>
     <li>移除 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### AEM專案控制面板小工具設定 {#aem-projects-dashboard-gadget-configurations}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新或修改的AEM專案儀表板小工具設定都必須移轉到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>將任何新或修改的AEM專案儀表板小工具設定從先前的位置複製到新位置(<code>/apps</code>)。
      <ol>
       <li>請勿複製未修改的AEM專案儀表板小工具設定，因為這些設定現在存在於新位置(<code>/libs</code>)。</li>
      </ol> </li>
     <li>更新任何參照先前位置的「AEM專案管理系統」範本，以指向適當的新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>如果套用AEM 6.4相容性套件，在移除相容性套件時就必須執行存放庫對齊活動。</td>
  </tr>
 </tbody>
</table>

### 復寫通知電子郵件範本 {#replication-notification-e-mail-template}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新的或修改過的復寫通知電子郵件範本都必須移轉到新位置(<code>/apps</code>)</p>
    <ol>
     <li>將任何新的或修改過的復寫通知電子郵件範本從先前位置複製到新位置(<code>/apps</code>)。</li>
     <li>從先前位置移除所有已移轉的復寫通知電子郵件範本。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>唯一支援的新復寫通知電子郵件範本是支援新的地區設定。</p> <p>復寫通知電子郵件範本解析的順序如下：</p>
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
   <td><strong>重組指南</strong></td>
   <td><p>所有標籤都必須移轉至 <code>/content/cq:tags</code>.</p>
    <ol>
     <li>將先前位置的所有標籤複製到新位置。</li>
     <li>從先前位置移除所有標籤。</li>
     <li>透過AEM網頁主控台，重新啟動Day Communique 5標籤OSGi套件組合位於 <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> 以供AEM識別「新位置」包含內容且應使用。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>重新啟動Day Communique Tagging OSGi套件組合時，如果「先前位置」空白，系統只會將「新位置」註冊為標籤根。</p> <p>針對使用AEM TagManager API進行標籤解析的所有功能，移轉至新位置後，「先前位置」的參照仍會繼續運作。</p> <p>明確參考路徑的任何自訂程式碼 <code>/etc/tags</code> 必須更新至 <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>，或是最好重寫以搭配此移轉使用TagManager Java API。</p> </td>
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
   <td><strong>重組指南</strong></td>
   <td><p>任何新的翻譯Cloud Service都必須移轉到新的位置(<code>/apps</code>， <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>將先前位置中的現有設定移轉到新位置。
      <ul>
       <li>透過AEM編寫UI，在手動重新建立新的翻譯Cloud Service設定 <strong>「工具&gt;Cloud Service&gt;翻譯Cloud Service」</strong>.<br /> 或 </li>
       <li>將任何新的翻譯Cloud Service設定從上一個位置複製到新位置(<code>/apps</code>， <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</li>
      </ul> </li>
     <li>將適用的AEM設定與AEM內容階層建立關聯。
      <ol>
       <li>AEM Sites頁面階層，透過 <strong>AEM Sites &gt;頁面&gt;頁面屬性&gt;進階標籤&gt;雲端設定</strong>.</li>
       <li>AEM體驗片段階層，透過 <strong>AEM體驗片段&gt;體驗片段&gt;屬性&gt;Cloud Service標籤&gt;雲端設定</strong>.</li>
       <li>AEM體驗片段資料夾階層，透過 <strong>AEM體驗片段&gt;資料夾&gt;屬性&gt;Cloud Service標籤&gt;雲端設定</strong>.<br /> </li>
       <li>AEM Assets資料夾階層，透過 <strong>AEM Assets &gt;資料夾&gt;資料夾屬性&gt;Cloud Service標籤&gt;設定</strong>.</li>
       <li>AEM專案管道 <strong>AEM專案&gt;專案&gt;專案屬性&gt;進階標籤&gt;雲端設定</strong>.</li>
      </ol> </li>
     <li>解除所有已移轉的舊版翻譯Cloud ServiceAEM與上述內容階層的關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯Cloud Service解析的順序如下：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>已移轉的翻譯Cloud Service必須與AEM 6.4相容。</p> </td>
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
   <td><strong>重組指南</strong></td>
   <td><p>任何新翻譯語言定義或修改過的翻譯語言定義都需要將所有翻譯語言定義移轉到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>如果對翻譯語言定義進行了任何新增或修改，則將所有翻譯語言定義從先前位置複製到新位置(<code>/apps</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯語言路徑解析的順序如下：</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>此解析度不支援合併覆蓋，這表示解析的路徑必須包含所有支援的語言，並且不會繼承高階解析度支援的語言。</p> </td>
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
   <td><strong>重組指南</strong></td>
   <td><p>修改過的翻譯規則XML檔案必須移轉到新位置(<code>/apps</code>，或 <code>/conf/global</code>)。</p> <p>1.將修改過的「轉譯規則」XML檔案從先前位置複製到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>復寫轉譯規則XML解析的順序如下：</p>
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

### 翻譯Widget使用者端資料庫 {#translation-widget-client-library}

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
   <td><strong>重組指南</strong></td>
   <td><p>對於任何在SCM中管理，且未透過設計對話方塊在執行階段寫入的設計。</p>
    <ol>
     <li>將設計從先前位置複製到新位置(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶庫</a> 替換為 <code>allowProxy = true</code>.</li>
     <li>更新中先前位置的參照
      <code>
       cq
      </code>：
      <code>
       designPath
      </code> 屬性。</li>
     <li>更新任何參考先前位置的頁面，以使用新的使用者端程式庫類別（這需要更新頁面實施程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供使用者端資料庫。 Proxy servlet。</li>
    </ol> <p>針對任何未在SCM中管理的設計，以及透過「設計」對話方塊修改的執行時間。</p>
    <ul>
     <li>請勿將可作者設計移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 樹啟動Web主控台 {#tree-activation-web-console}

| **上一個位置** | `/etc/replication/treeactivation` |
|---|---|
| **新位置** | `/libs/replication/treeactivation` |
| **重組指南** | 不需要採取任何動作。 |
| **附註** | Tree Activation Web Console現在可透過以下方式使用 **「工具」 > 「部署」 > 「復寫」 > 「啟動樹狀結構」**. |

{style="table-layout:auto"}

### 廠商翻譯聯結器Cloud Service {#vendor-translation-connector-cloud-services}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新的廠商翻譯聯結器Cloud Service都必須移轉至新位置(<code>/apps</code>， <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>將先前位置中的現有組態移轉到新位置。
      <ul>
       <li>手動建立全新廠商翻譯聯結器Cloud Service設定，透過 <strong>「工具&gt;Cloud Service&gt;翻譯Cloud Service」中的AEM編寫UI</strong>.<br /> 或 </li>
       <li>將任何新的廠商翻譯聯結器Cloud Service設定從先前的位置複製到新位置(<code>/apps</code>， <code>/conf/global </code>或 <code>/conf/&lt;tenant&gt;</code>)。</li>
      </ul> </li>
     <li>將適用的AEM設定與AEM內容階層建立關聯。
      <ol>
       <li>AEM Sites頁面階層，透過 <strong>AEM Sites &gt;頁面&gt;頁面屬性&gt;進階標籤&gt;雲端設定</strong>.</li>
       <li>AEM體驗片段階層，透過 <strong>AEM體驗片段&gt;體驗片段&gt;屬性&gt;Cloud Service標籤&gt;雲端設定</strong>.</li>
       <li>AEM體驗片段資料夾階層，透過 <strong>AEM體驗片段&gt;資料夾&gt;屬性&gt;Cloud Service標籤&gt;雲端設定</strong>.</li>
       <li>AEM Assets資料夾階層，透過 <strong>AEM Assets &gt;資料夾&gt;資料夾屬性&gt;Cloud Service標籤&gt;設定</strong>.</li>
       <li>AEM專案管道 <strong>AEM專案&gt;專案&gt;專案屬性&gt;進階標籤&gt;雲端設定</strong>.</li>
      </ol> </li>
     <li>解除所有已移轉的舊版翻譯Cloud ServiceAEM與上述內容階層的關聯。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯Cloud Service解析的順序如下：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流程通知電子郵件範本 {#workflow-notification-email-templates}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何修改過的工作流程通知電子郵件範本都必須移轉至新位置(<code>/conf/global</code>)。</p>
    <ol>
     <li>將先前位置的任何已修改工作流程通知電子郵件範本複製到新位置。</li>
     <li>從先前位置移除已移轉的工作流程通知電子郵件範本。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>工作流程通知電子郵件範本解析的順序如下：</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流程封裝 {#workflow-packages}

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
   <td><strong>重組指南</strong></td>
   <td><p>先前位置中的現有Workflow套件應移轉到新位置。</p>
    <ol>
     <li>移除先前位置中未被其他內容參考或不需要的任何Workflow套件。</li>
     <li>將未被其他內容引用、但在新位置有其他需要的任何Workflow套件移至先前位置。</li>
     <li>將其他內容參考的任何Workflow套件保留在先前位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>透過傳統UI Miscadmin主控台建立的工作流程套件會保留在先前的位置，而其他所有套件則會保留在新位置。</p> <p>儲存在之前或以下位置的工作流程套件可以透過傳統UI Miscadmin控制檯進行管理。</p> </td>
  </tr>
 </tbody>
</table>
