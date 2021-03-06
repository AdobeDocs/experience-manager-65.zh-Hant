---
title: AEM 6.5中的常見存放庫重新調整架構
seo-title: AEM 6.5中的常見存放庫重新調整架構
description: 了解如何進行必要的變更，以移轉至AEM 6.5中所有AEM區域通用的新存放庫結構。
seo-description: 了解如何進行必要的變更，以移轉至AEM 6.5中所有AEM區域通用的新存放庫結構。
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2724'
ht-degree: 2%

---

# AEM 6.5 {#common-repository-restructuring-in-aem}中的常見存放庫重新調整

如上層[AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的存放庫重組頁面所述，升級至AEM 6.5的客戶應使用此頁面評估與存放庫變更相關的工作成果，這些工作成果可能會對所有解決方案造成影響。 有些變更需要AEM 6.5升級程式中的工作量，而有些變更可能會延遲至日後升級。

**使用6.5升級**

* [ContextHub 組態](#contexthub-6.5)
* [工作流程例項](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [工作流程模型](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [工作流程啟動器](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [工作流程指令碼](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**未來升級前**

* [ContextHub 組態](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [傳統Cloud Services設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [傳統控制面板設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [傳統報表設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [預設設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [AdobeDTM JavaScript端點](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [AdobeDTM Web-Hook端點](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [收件箱任務](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [多站點管理器Blueprint配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [AEM Projects儀表板小工具配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [複製通知電子郵件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [標記](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [翻譯雲端服務](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [翻譯語言](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [翻譯規則](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [翻譯介面工具集用戶端程式庫](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [樹激活Web控制台](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [廠商翻譯連接器Cloud Services](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [工作流程通知電子郵件範本](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 使用6.5升級{#with-upgrade}

### ContextHub 組態 {#contexthub-6.5}

從AEM 6.4開始，沒有預設的ContextHub設定。 因此，應在網站的根層級設定`cq:contextHubPathproperty`，以指出應使用哪個設定。

1. 導覽至網站的根目錄。
1. 開啟根頁面的頁面屬性，然後選取「個人化」索引標籤。
1. 在「Contexthub路徑」欄位中，輸入您自己的ContextHub設定路徑。

此外，在ContextHub設定中，`sling:resourceType`需要更新為相對值而非絕對值。

1. 在CRX DE Lite中開啟ContextHub設定節點的屬性，例如`/apps/settings/cloudsettings/legacy/contexthub`
1. 將`sling:resourceType`從`/libs/granite/contexthub/cloudsettings/components/baseconfiguration`更改為`granite/contexthub/cloudsettings/components/baseconfiguration`

亦即，ContextHub設定的`sling:resourceType`必須是相對的，而非絕對的。

### 工作流程模型 {#workflow-models}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的工作流程模型都必須移轉至/conf/global/workflow/models。</p>
    <ol>
     <li>將修改的工作流模型部署到本地AEM 6.5開發實例中，使它們存在於上一位置。</li>
     <li>使用AEM Workflow Model Editor（工具&gt;工作流&gt;模型）編輯工作流模型。</li>
     <li>移轉修改的AEM提供的工作流程模型時
      <ol>
       <li>開啟「工作流模型編輯器」後，修改瀏覽器的地址URL，並將路徑段/libs/settings/workflow/models替換為/etc/workflow/models。
        <ul>
         <li>例如，變更：<em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em>至<em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>在工作流模型編輯器中啟用「編輯」模式，該編輯器將工作流模型定義複製到/conf/global/workflow/models。</li>
     <li>點選「同步」按鈕，將變更同步至/var/workflow/models底下的「執行階段工作流程模型」。</li>
     <li>匯出「工作流程模型」(/conf/global/workflow/models/&lt;workflow-model&gt;)和「執行階段工作流程模型」(/var/workflow/models/&lt;workflow-model&gt;)，並整合至AEM專案。
      <ol>
       <li>例如，匯出：
        <ul>
         <li><code>/config/settings/workflow/models/dam/my_workflow_model</code> 和 </li>
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
    </ol> <p>因此，如果要保留AEM提供的工作流模型的任何自訂，則必須將其移至/conf/global/settings/workflow/models，否則將由/libs/settings/workflow/models中AEM提供的工作流模型定義所取代。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流程例項 {#workflow-instances}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>無需執行任何動作來與新位置一致。</p> <p>歷史工作流實例可以安全地繼續駐留在「上一位置」中，而新的工作流實例將在「新位置」中建立。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>中的任何明確路徑參考
    <code>
     custom
    </code>前一個位置的代碼也應考慮新位置。 建議您重構此程式碼，以使用AEM工作流程API。</td>
  </tr>
 </tbody>
</table>

### 工作流程啟動器 {#workflow-launchers}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>必須將任何新的或修改的工作流啟動器遷移到<code>/conf/global/workflow/launcher/config</code>。</p>
    <ol>
     <li>將任何新的或修改的工作流啟動器配置從上一位置複製到新位置(<code>/conf/global</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>工作流啟動器解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>因此，如果要保留AEM提供的工作流啟動器定義，則保留在「上一個」位置的任何自定義項都必須移到「新位置」(<code>/conf/global/settings/workflow/launcher</code>)，否則將被<code>/libs/settings/workflow/launcher</code>中AEM提供的工作流啟動器定義取代。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流指令碼{#workflow-scripts}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>必須將任何新的或修改的工作流指令碼遷移到「新位置」，並更新參考的工作流模型以反映「新位置」。</p>
    <ol>
     <li>將任何新的或修改的工作流指令碼從上一位置複製到新位置。<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> 應在SCM中維護。</li>
      </ul> </li>
     <li>更新工作流模型中先前位置的對工作流指令碼的任何引用，以指向新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>AEM 6.4 SP1在發行時，可讓此重組延後至6.5
     <code>
      upgrade
     </code>。</p> <p>如果在AEM 6.4 SP1發行前升級至AEM 6.4，應在升級專案中執行此重新調整。 若不執行此操作，則編輯和保存引用上一個位置中的指令碼的工作流步驟將完全從工作流步驟中刪除工作流指令碼引用，並且指令碼選擇下拉式清單中將僅提供新位置中的工作流指令碼。</p> </td>
  </tr>
 </tbody>
</table>

## 未來升級前{#prior-to-upgrade}

### ContextHub 組態 {#contexthub-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的ContextHub設定都必須移轉至新位置，且必須更新參考的AEM Sites頁面以反映新位置。</p>
    <ol>
     <li>將任何新的或修改的ContextHub配置從上一個位置複製到新位置。</li>
     <li>將適用的AEM設定與AEM內容階層關聯。
      <ol>
       <li><strong>AEM Sites頁面階層，透過AEM Sites &gt;頁面&gt;頁面屬性&gt;進階標籤&gt;雲端設定</strong>。</li>
      </ol> </li>
     <li>將任何移轉的舊版ContextHub設定與上述AEM內容階層分離。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 傳統Cloud Services設計{#classic-cloud-services-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理、而不是在運行時通過設計對話框寫入的任何設計。</p>
    <ol>
     <li>將設計從上一位置複製到新位置(<code>/apps</code>)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">使用<code>allowProxy = true</code>的用戶端程式庫</a>。</li>
     <li>更新<span class="code">中上一個位置的引用
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span>屬性。</li>
     <li>更新任何參考上一個位置的頁面，以使用新的用戶端程式庫類別（這需要更新頁面實作程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供用戶端程式庫。 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改運行時。</p>
    <ul>
     <li>請勿將可作者的設計移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 傳統控制面板設計{#classic-dashboards-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理、而不是在運行時通過設計對話框寫入的任何設計。</p>
    <ol>
     <li>將設計從上一位置複製到新位置(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">使用<code>allowProxy = true</code>的用戶端程式庫</a>。</li>
     <li>更新上一個位置的參考，位於
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>屬性。</li>
     <li>更新任何參考上一個位置的頁面，以使用新的用戶端程式庫類別（這需要更新頁面實作程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供用戶端程式庫。 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改運行時。</p>
    <ul>
     <li>請勿將可作者的設計移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 傳統報表設計{#classic-reports-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理、而不是在運行時通過設計對話框寫入的任何設計。</p>
    <ol>
     <li>將設計從上一位置複製到新位置(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">使用<code>allowProxy = true</code>的用戶端程式庫</a>。</li>
     <li>更新上一個位置的參考，位於
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>屬性。</li>
     <li>更新任何參考上一個位置的頁面，以使用新的用戶端程式庫類別（這需要更新頁面實作程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供用戶端程式庫。 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改運行時。</p>
    <ul>
     <li>請勿將可作者的設計移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 預設設計{#default-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理、而不是在運行時通過設計對話框寫入的任何設計。</p>
    <ol>
     <li>將設計從上一位置複製到新位置(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">使用<code>allowProxy = true</code>的用戶端程式庫</a>。</li>
     <li>更新上一個位置的參考，位於
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>屬性。</li>
     <li>更新任何參考上一個位置的頁面，以使用新的用戶端程式庫類別（這需要更新頁面實作程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供用戶端程式庫。 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改運行時。</p>
    <ul>
     <li>請勿將可作者的設計移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### AdobeDTM JavaScript端點{#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>無需任何動作。</p> <p>公用上一個位置充當專用新位置的代理端點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### AdobeDTM Web-Hook端點{#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>無需任何動作。</p> <p>公用上一個位置充當專用新位置的代理端點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 收件箱任務{#inbox-tasks}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>使用<strong>收件箱清除維護任務</strong>可根據需要從上一個位置刪除舊任務。</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>將任務遷移到新位置無需任何操作。</p>
    <ul>
     <li>「上一位置」中顯示的任務仍可繼續使用，且可正常運作。</li>
     <li>新任務在新位置中建立。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 多站點管理器Blueprint配置{#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong><em></em>上一位置</strong></td>
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
     <li>將自定義配置從<code>/etc/blueprints</code>複製到<code>/apps/msm</code>。</li>
     <li>移除 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### AEM Projects儀表板小工具配置{#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的AEM Projects儀表板小工具配置都必須遷移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>將任何新的或修改的AEM Projects儀表板小工具配置從上一個位置複製到新位置(<code>/apps</code>)。
      <ol>
       <li>請勿複製未修改的AEM Projects儀表板小工具配置，因為新位置(<code>/libs</code>)中現在存在這些配置。</li>
      </ol> </li>
     <li>更新參考「上一個位置」的任何AEM專案範本，以指向適當的新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>如果應用了AEM 6.4相容性包，則在刪除相容性包時必須執行儲存庫對齊活動。</td>
  </tr>
 </tbody>
</table>

### 複製通知電子郵件模板{#replication-notification-e-mail-template}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>必須將任何新的或修改的複製通知電子郵件模板遷移到新位置(<code>/apps</code>)</p>
    <ol>
     <li>將任何新的或修改的複製通知電子郵件模板從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>從上一個位置刪除所有遷移的複製通知電子郵件模板。</li>
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
   <td><strong>上一位置</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>所有標籤都必須移轉至<code>/content/cq:tags</code>。</p>
    <ol>
     <li>將所有標籤從上一位置複製到新位置。</li>
     <li>從上一個位置刪除所有標籤。</li>
     <li>透過AEM Web主控台，在<em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em>重新啟動Day Commulate 5 Tagging OSGi套件組合，讓AEM識別包含內容且應使用的新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>重新啟動Day Commulate標籤OSGi套件組合只會在「上一位置」為空時，將「新位置」註冊為標籤根。</p> <p>針對所有採用AEM TagManager API來解析標籤的功能，移轉至「新位置」後，「上一位置」的參考將會繼續運作。</p> <p>必須將明確參考路徑<code>/etc/tags</code>的任何自訂程式碼更新為<span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>，或最好重寫以搭配此次移轉使用TagManager Java API。</p> </td>
  </tr>
 </tbody>
</table>

### 翻譯雲端服務 {#translation-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的翻譯Cloud Services都必須遷移到新位置（<code>/apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。</p>
    <ol>
     <li>將先前位置的現有設定移轉至新位置。
      <ul>
       <li>在<strong>工具&gt;Cloud Services&gt;翻譯Cloud Services</strong>，透過AEM製作UI手動重新建立新的翻譯Cloud Services設定。<br /> 或 </li>
       <li>將任何新的翻譯Cloud Services配置從上一位置複製到新位置（<code>/apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。</li>
      </ul> </li>
     <li>將適用的AEM設定與AEM內容階層關聯。
      <ol>
       <li>AEM Sites頁面階層，透過<strong>AEM Sites &gt;頁面&gt;頁面屬性&gt;進階標籤&gt;雲端設定</strong>。</li>
       <li>AEM體驗片段階層，透過<strong>AEM體驗片段&gt;體驗片段&gt;屬性&gt;Cloud Services標籤&gt;雲端設定</strong>。</li>
       <li>AEM體驗片段資料夾階層，透過<strong>AEM體驗片段&gt;資料夾&gt;屬性&gt;Cloud Services標籤&gt;雲端設定</strong>。<br /> </li>
       <li>AEM Assets資料夾階層，透過<strong>AEM Assets &gt;資料夾&gt;資料夾屬性&gt;Cloud Services標籤&gt;設定</strong>。</li>
       <li>AEM透過<strong>AEM專案&gt;專案&gt;專案屬性&gt;進階標籤&gt;雲端設定</strong>進行專案。</li>
      </ol> </li>
     <li>將任何已移轉的舊版翻譯Cloud Services與上述AEM內容階層分離。</li>
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
    </ol> <p>移轉的翻譯Cloud Services必須與AEM 6.4相容。</p> </td>
  </tr>
 </tbody>
</table>

### 翻譯語言{#translation-languages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的翻譯語言定義都需要將所有翻譯語言定義遷移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>如果對翻譯語言定義進行了任何添加或修改，則將上一個位置的所有翻譯語言定義複製到新位置(<code>/apps</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯語言路徑解析按以下順序進行：</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>此解析度不支援合併覆蓋，這表示解析的路徑必須包含所有受支援的語言，並且不會繼承高階解析度的受支援語言。</p> </td>
  </tr>
 </tbody>
</table>

### 翻譯規則{#translation-rules}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>修改的翻譯規則XML檔案必須遷移到新位置（<code>/apps</code>或<code>/conf/global</code>）。</p> <p>1.將修改的翻譯規則XML檔案從上一位置複製到新位置。</p> </td>
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

### 翻譯介面工具集客戶端庫{#translation-widget-client-library}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理、而不是在運行時通過設計對話框寫入的任何設計。</p>
    <ol>
     <li>將設計從上一位置複製到新位置(/apps)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">使用<code>allowProxy = true</code>的用戶端程式庫</a>。</li>
     <li>更新上一個位置的參考，位於
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>屬性。</li>
     <li>更新任何參考上一個位置的頁面，以使用新的用戶端程式庫類別（這需要更新頁面實作程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過/etc.clientlibs/提供用戶端程式庫。 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改運行時。</p>
    <ul>
     <li>請勿將可作者的設計移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 樹激活Web控制台{#tree-activation-web-console}

| **上一位置** | `/etc/replication/treeactivation` |
|---|---|
| **新位置** | `/libs/replication/treeactivation` |
| **重組指導** | 無需任何動作。 |
| **附註** | 樹激活Web控制台現在可通過&#x200B;**工具>部署>複製>激活樹**&#x200B;獲得。 |

{style=&quot;table-layout:auto&quot;}

### 供應商翻譯連接器Cloud Services{#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
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
   <td><p>任何新的「供應商翻譯連接器」Cloud Services都必須遷移到新位置（<code>/apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。</p>
    <ol>
     <li>將「上一位置」中的現有配置遷移到「新位置」。
      <ul>
       <li>通過<strong>AEM編寫UI(位於「工具」&gt;「Cloud Services」&gt;「翻譯Cloud Services」</strong>)手動建立新供應商翻譯連接器Cloud Services配置。<br /> 或 </li>
       <li>將任何新的「供應商翻譯連接器」Cloud Services配置從上一位置複製到新位置（<code>/apps</code>、<code>/conf/global </code>或<code>/conf/&lt;tenant&gt;</code>）。</li>
      </ul> </li>
     <li>將適用的AEM設定與AEM內容階層關聯。
      <ol>
       <li>AEM Sites頁面階層，透過<strong>AEM Sites &gt;頁面&gt;頁面屬性&gt;進階標籤&gt;雲端設定</strong>。</li>
       <li>AEM體驗片段階層，透過<strong>AEM體驗片段&gt;體驗片段&gt;屬性&gt;Cloud Services標籤&gt;雲端設定</strong>。</li>
       <li>AEM體驗片段資料夾階層，透過<strong>AEM體驗片段&gt;資料夾&gt;屬性&gt;Cloud Services標籤&gt;雲端設定</strong>。</li>
       <li>AEM Assets資料夾階層，透過<strong>AEM Assets &gt;資料夾&gt;資料夾屬性&gt;Cloud Services標籤&gt;設定</strong>。</li>
       <li>AEM透過<strong>AEM專案&gt;專案&gt;專案屬性&gt;進階標籤&gt;雲端設定</strong>進行專案。</li>
      </ol> </li>
     <li>將任何已移轉的舊版翻譯Cloud Services與上述AEM內容階層分離。</li>
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

### 工作流通知電子郵件模板{#workflow-notification-email-templates}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何修改的工作流通知電子郵件模板都必須遷移到新位置(<code>/conf/global</code>)。</p>
    <ol>
     <li>將任何修改的工作流通知電子郵件模板從上一位置複製到新位置。</li>
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

### 工作流程套件{#workflow-packages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
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
     <li>移除先前位置中未被其他內容參照且不需要的任何工作流程套件。</li>
     <li>移動上一個位置中未被其他內容引用，但在新位置中需要的任何工作流包。</li>
     <li>保留先前位置中其他內容所參考的任何工作流程套件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>透過傳統UI Miscadmin主控台建立的工作流程套件會保留在先前的位置，而其他所有套件則會保留在新的位置。</p> <p>儲存在先前或未位置的工作流程套件可透過傳統UI Miscadmin主控台管理。</p> </td>
  </tr>
 </tbody>
</table>
