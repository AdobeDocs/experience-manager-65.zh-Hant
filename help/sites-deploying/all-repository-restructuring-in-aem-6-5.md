---
title: AEM 6.5中的通用資料庫重組
seo-title: AEM 6.5中的通用資料庫重組
description: 瞭解如何進行必要的變更，以移轉至AEM 6.5中所有AEM區域都常用的新儲存庫結構。
seo-description: 瞭解如何進行必要的變更，以移轉至AEM 6.5中所有AEM區域都常用的新儲存庫結構。
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5中的通用資料庫重組 {#common-repository-restructuring-in-aem}

如「AEM 6.5 [](/help/sites-deploying/repository-restructuring.md) 」中的父資料庫重組頁面所述，升級至AEM 6.5的客戶應使用此頁面來評估與資料庫變更相關的工作成果，這些變更可能會影響所有解決方案。 有些變更需要在AEM 6.5升級程式中努力工作，而其他變更則可延後至日後升級。

**使用6.5升級**

* [工作流程例項](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [工作流程模型](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [工作流程啟動器](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [工作流程指令碼](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**未來升級前**

* [ContextHub 組態](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Classic Cloud services設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [傳統儀表板設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [傳統報表設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [預設設計](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Adobe DTM javaScript端點](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Adobe DTM Web-Hook端點](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [收件箱任務](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [多站點管理器Blueprint配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [AEM Projects Dashboard Gadget設定](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [複製通知電子郵件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [標記](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [翻譯雲端服務](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [翻譯語言](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [翻譯規則](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [翻譯介面工具集用戶端程式庫](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [樹狀結構啟動Web主控台](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [廠商轉譯連接器雲端服務](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [工作流程通知電子郵件範本](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 使用6.5升級 {#with-upgrade}

### 工作流程模型 {#workflow-models}

<table>
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
     <li>將修改的「工作流程模型」部署至本機AEM 6.4開發例項，如此就會存在於「上一個」位置。</li>
     <li>使用AEM的「工作流程模型編輯器」(Workflow Model Editor)，在「AEM &gt;工具&gt;工作流程&gt;模型」(AEM &gt; Workflow &gt; Models)編輯「工作流程模型」(Workflow Model)。</li>
     <li>移轉修改的AEM提供的工作流程模型時
      <ol>
       <li>在「工作流模型編輯器」開啟時，修改瀏覽器的位址URL，並將路徑區段/libs/settings/workflow/models取代為/etc/workflow/models。
        <ul>
         <li>例如，變更： <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html至</em> http://localhost:4502/editor.html <em>/etc/workflow/models<strong></strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>在工作流模型編輯器中啟用「編輯」模式，該模式將工作流模型定義複製到/conf/global/workflow/models。</li>
     <li>點選「同步」按鈕，將變更同步至/var/workflow/models下的「執行階段工作流程模型」。</li>
     <li>匯出「工作流程模型」(/conf/global/workflow/models/&lt;workflow-model&gt;)和「執行時期工作流程模型」(/var/workflow/models/&lt;workflow-model&gt;)，並整合至AEM專案。
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
   <td><p>「工作流模型」解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>因此，如果要保留AEM提供的「工作流程模型」，則「上一個」位置中保留的任何自訂都必須移至/conf/global/settings/workflow/models，否則將被/libs/settings/workflow/models中AEM提供的「工作流程模型」定義所取代。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流程例項 {#workflow-instances}

<table>
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
   <td><p>不需要執行任何動作來與新位置對齊。</p> <p>歷史工作流程例項可安全地繼續駐留在先前位置，而新的工作流程例項則會在新位置中建立。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>程式碼中任何明確 <code>
     custom
    </code> 的「上一個位置」路徑參考，也應考量「新位置」。 建議將此程式碼重構為使用AEM Workflow API。</td>
  </tr>
 </tbody>
</table>

### 工作流程啟動器 {#workflow-launchers}

<table>
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
   <td><p>必須將任何新的或修改的Workflow Rachilters遷移到 <code>/conf/global/workflow/launcher/config</code>。</p>
    <ol>
     <li>將任何新的或修改的工作流啟動程式配置從「上一個位置」複製到「新位置」(<code>/conf/global</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>Workflow Launcher解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>因此，「上一個」位置中保留的AEM提供的「工作流程啟動程式」的任何自訂項目都必須移至「新位置」(<code>/conf/global/settings/workflow/launcher</code> 如果要保留，則會由中的AEM提供的「工作流程啟動程式」定義取代 <code>/libs/settings/workflow/launcher</code>。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流程指令碼 {#workflow-scripts}

<table>
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
   <td><p>任何新的或修改的工作流指令碼都必須遷移到「新位置」(New Location)，並且引用的工作流模型已更新，以反映「新位置」(New Location)。</p>
    <ol>
     <li>將任何新的或修改的工作流指令碼從上一個位置複製到新位置。<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> 應在SCM中維護。</li>
      </ul> </li>
     <li>更新工作流模型中先前位置對工作流指令碼的任何引用，以指向新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>AEM 6.4 SP1在發行時，會讓它延遲至6.5 <code>
      upgrade
     </code>。</p> <p>如果在AEM 6.4 SP1發行之前升級至AEM 6.4，此重組應視為升級專案的一部分來執行。 如果不這樣做，編輯和保存引用「上一個位置」中指令碼的「工作流指令碼」將完全從「工作流步驟」中刪除「工作流指令碼」引用，並且只有「新位置」中的「工作流指令碼」將在指令碼選擇下拉式清單中可用。</p> </td>
  </tr>
 </tbody>
</table>

## 未來升級前 {#prior-to-upgrade}

### ContextHub 組態 {#contexthub-configurations}

<table>
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
   <td><p>任何新的或修改的ContextHub設定都必須移轉至新位置，且必須更新參照的AEM Sites頁面以反映新位置。</p>
    <ol>
     <li>將任何新的或修改的ContextHub配置從上一個位置複製到新位置。</li>
     <li>將適用的AEM設定與AEM內容階層建立關聯。
      <ol>
       <li><strong>透過「AEM網站&gt;頁面&gt;頁面屬性&gt;進階標籤&gt;雲端設定」的AEM網站頁面階層</strong>。</li>
      </ol> </li>
     <li>將任何移轉的舊版ContextHub組態與前述的AEM內容階層分離。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Classic Cloud services設計 {#classic-cloud-services-designs}

<table>
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
   <td><p>適用於任何以SCM管理且不在執行時期透過設計對話方塊寫入的設計。</p>
    <ol>
     <li>將設計從「上一個位置」複製到「新位置」(<code>/apps</code>)。</li>
     <li>將「設計」中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">用戶端程式庫</a><code>allowProxy = true</code>。</li>
     <li>在以下位置更新「上一個位置」的參 <span class="code"><code>
        cq
       </code>考：       屬 <code>
        designPath
       </code></span> 性。</li>
     <li>更新參照「上一位置」的任何頁面，以使用新的「用戶端程式庫」類別（這需要更新「頁面」實作代碼）。</li>
     <li>更新AEM Dispatcher規則，允許透過/etc.clientlibs/... 代理servlet。</li>
    </ol> <p>對於任何未在SCM中管理的設計，以及透過設計對話方塊修改執行時期的設計。</p>
    <ul>
     <li>請勿將可編寫的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 傳統儀表板設計 {#classic-dashboards-designs}

<table>
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
   <td><p>適用於任何以SCM管理且不在執行時期透過設計對話方塊寫入的設計。</p>
    <ol>
     <li>將設計從「上一個位置」複製到「新位置」(/apps)。</li>
     <li>將「設計」中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">用戶端程式庫</a><code>allowProxy = true</code>。</li>
     <li>在以下位置更新對上一個位置的引用： <code>
       cq
      </code>     屬 <code>
       designPath
      </code> 性。</li>
     <li>更新參照「上一位置」的任何頁面，以使用新的「用戶端程式庫」類別（這需要更新「頁面」實作代碼）。</li>
     <li>更新AEM Dispatcher規則，允許透過/etc.clientlibs/... 代理servlet。</li>
    </ol> <p>對於任何未在SCM中管理的設計，以及透過設計對話方塊修改執行時期的設計。</p>
    <ul>
     <li>請勿將可編寫的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 傳統報表設計 {#classic-reports-designs}

<table>
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
   <td><p>適用於任何以SCM管理且不在執行時期透過設計對話方塊寫入的設計。</p>
    <ol>
     <li>將設計從「上一個位置」複製到「新位置」(/apps)。</li>
     <li>將「設計」中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">用戶端程式庫</a><code>allowProxy = true</code>。</li>
     <li>在以下位置更新對上一個位置的引用： <code>
       cq
      </code>     屬 <code>
       designPath
      </code> 性。</li>
     <li>更新參照「上一位置」的任何頁面，以使用新的「用戶端程式庫」類別（這需要更新「頁面」實作代碼）。</li>
     <li>更新AEM Dispatcher規則，允許透過/etc.clientlibs/... 代理servlet。</li>
    </ol> <p>對於任何未在SCM中管理的設計，以及透過設計對話方塊修改執行時期的設計。</p>
    <ul>
     <li>請勿將可編寫的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 預設設計 {#default-designs}

<table>
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
   <td><p>適用於任何以SCM管理且不在執行時期透過設計對話方塊寫入的設計。</p>
    <ol>
     <li>將設計從「上一個位置」複製到「新位置」(/apps)。</li>
     <li>將「設計」中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">用戶端程式庫</a><code>allowProxy = true</code>。</li>
     <li>在以下位置更新對上一個位置的引用： <code>
       cq
      </code>     屬 <code>
       designPath
      </code> 性。</li>
     <li>更新參照「上一位置」的任何頁面，以使用新的「用戶端程式庫」類別（這需要更新「頁面」實作代碼）。</li>
     <li>更新AEM Dispatcher規則，允許透過/etc.clientlibs/... 代理servlet。</li>
    </ol> <p>對於任何未在SCM中管理的設計，以及透過設計對話方塊修改執行時期的設計。</p>
    <ul>
     <li>請勿將可編寫的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Adobe DTM javaScript端點 {#adobe-dtm-javascript-endpoint}

<table>
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
   <td><p>不需執行任何動作。</p> <p>公共先前位置用作專用新位置的代理端點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Adobe DTM Web-Hook端點 {#adobe-dtm-web-hook-endpoint}

<table>
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
   <td><p>不需執行任何動作。</p> <p>公共先前位置用作專用新位置的代理端點。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 收件箱任務 {#inbox-tasks}

<table>
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
   <td>使用「收 <strong>件箱清除維護任務</strong> 」，根據需要從上一個位置刪除舊任務。</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>將Task遷移到新位置不需要任何操作。</p>
    <ul>
     <li>「上一個位置」中顯示的任務仍可繼續使用並正常運作。</li>
     <li>新任務在新位置中建立。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 多站點管理器Blueprint配置 {#multi-site-manager-blueprint-configurations}

<table>
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
     <li>將自訂組態從複製 <code>/etc/blueprints</code> 到 <code>/apps/msm</code>。</li>
     <li>移除 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### AEM Projects Dashboard Gadget設定 {#aem-projects-dashboard-gadget-configurations}

<table>
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
   <td><p>任何新的或修改的AEM Projects Dashboard Gadget設定都必須移轉至新位置(<code>/apps</code>)。</p>
    <ol>
     <li>將任何新的或已修改的AEM Projects Dashboard Gadget設定從先前位置複製到新位置(<code>/apps</code>)。
      <ol>
       <li>請勿複製未修改的AEM Projects Dashboard Gadget設定，因為這些設定現在已存在於新位置(<code>/libs</code>)中。</li>
      </ol> </li>
     <li>更新任何參照「上一個位置」的AEM projects範本，以指向適當的新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>如果已套用AEM 6.4相容性套件，在移除相容性套件時，就必須執行儲存庫對齊活動。</td>
  </tr>
 </tbody>
</table>

### 複製通知電子郵件模板 {#replication-notification-e-mail-template}

<table>
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

<table>
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
   <td><p>所有標籤都必須移轉至 <code>/content/cq:tags</code>。</p>
    <ol>
     <li>將所有標籤從上一個位置複製到新位置。</li>
     <li>從上一個位置移除所有標籤。</li>
     <li>透過AEM Web Console，在 <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> for AEM重新啟動Day Communate 5 Tagging OSGi bundle，以辨識「新位置」包含內容且應使用。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>重新啟動Day Commute標籤OSGi捆綁包將僅在「上一個位置」為空時將「新位置」註冊為標籤根目錄。</p> <p>針對所有運用AEM TagManager API進行標籤解析的功能，移轉至「新位置」後，「上一個位置」的參考仍將繼續運作。</p> <p>任何明確參照路徑的自訂程 <code>/etc/tags</code> 式碼都必須更新為 <span class="code">/content/ <code>
       cq
      </code><code>
       :tags
      </code></span>，或最好改寫，以搭配此移轉運用TagManager Java API。</p> </td>
  </tr>
 </tbody>
</table>

### 翻譯雲端服務 {#translation-cloud-services}

<table>
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
   <td><p>任何新的翻譯雲端服務都必須移轉至新<code>/apps</code>位置( <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>將上一個位置的現有配置遷移到新位置。
      <ul>
       <li>透過「工具&gt;雲端服務&gt;轉譯雲端服務」的AEM製作UI, <strong>手動重新建立新的Translation Cloud服務設定</strong>。<br /> 或 </li>
       <li>將任何新的Translation cloud服務配置從「上一個位置」複製到「新<code>/apps</code>位置」( <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</li>
      </ul> </li>
     <li>將適用的AEM設定與AEM內容階層建立關聯。
      <ol>
       <li>透過 <strong>AEM Sites &gt;頁面&gt;頁面屬性&gt;進階標籤&gt;雲端設定的AEM Sites頁面階層</strong>。</li>
       <li>透過 <strong>AEM體驗片段&gt;體驗片段&gt;屬性&gt;雲端服務標籤&gt;雲端設定的AEM體驗片段階層</strong>。</li>
       <li>透過 <strong>AEM Experience Fragments &gt;資料夾&gt;屬性&gt;雲端服務標籤&gt;雲端設定的AEM Experience Fragment資料夾階層</strong>。<br /> </li>
       <li>透過「 <strong>AEM Assets &gt;資料夾&gt;資料夾屬性&gt;雲端服務標籤&gt;設定」的AEM Assets資料夾階層</strong>。</li>
       <li>透過 <strong>AEM Projects &gt;專案&gt;專案屬性&gt;進階標籤&gt;雲端設定的AEM專案</strong>。</li>
      </ol> </li>
     <li>將任何移轉的舊版Translation cloud服務與前述的AEM內容階層分離。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯雲服務解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>移轉的Translation cloud服務必須與AEM 6.4相容。</p> </td>
  </tr>
 </tbody>
</table>

### 翻譯語言 {#translation-languages}

<table>
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
   <td><p>任何新的或修改的翻譯語言定義都需要將所有翻譯語言定義遷移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>如果對翻譯語言定義進行了任何添加或修改，則將所有翻譯語言定義從先前位置複製到新位置(<code>/apps</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯語言路徑解析按以下順序進行：</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>此解析度不支援合併覆蓋，這表示已解析的路徑必須包含所有支援的語言，且不會繼承高階解析度的支援語言。</p> </td>
  </tr>
 </tbody>
</table>

### 翻譯規則 {#translation-rules}

<table>
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
   <td><p>修改的翻譯規則XML檔案必須遷移到新位置(<code>/apps</code>或 <code>/conf/global</code>)。</p> <p>1.將修改過的翻譯規則XML檔案從上一個位置複製到新位置。</p> </td>
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

### 翻譯介面工具集用戶端程式庫 {#translation-widget-client-library}

<table>
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
   <td><p>適用於任何以SCM管理且不在執行時期透過設計對話方塊寫入的設計。</p>
    <ol>
     <li>將設計從「上一個位置」複製到「新位置」(/apps)。</li>
     <li>將「設計」中的任何CSS、JavaScript和靜態資源轉換為用戶 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">端程式庫</a> , <code>allowProxy = true</code>包含</li>
     <li>在以下位置更新對上一個位置的引用： <code>
       cq
      </code>     屬 <code>
       designPath
      </code> 性。</li>
     <li>更新參照「上一位置」的任何頁面，以使用新的「用戶端程式庫」類別（這需要更新「頁面」實作代碼）。</li>
     <li>更新AEM Dispatcher規則，允許透過/etc.clientlibs/... 代理servlet。</li>
    </ol> <p>對於任何未在SCM中管理的設計，以及透過設計對話方塊修改執行時期的設計。</p>
    <ul>
     <li>請勿將可編寫的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 樹狀結構啟動Web主控台 {#tree-activation-web-console}

| **上一個位置** | `/etc/replication/treeactivation` |
|---|---|
| **新位置** | `/libs/replication/treeactivation` |
| **重組指導** | 不需執行任何動作。 |
| **附註** | 樹激活Web控制台現在可通過「工具」>「部 **署」>「複製」>「激活樹**」。 |

### 廠商轉譯連接器雲端服務 {#vendor-translation-connector-cloud-services}

<table>
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
   <td><p>任何新的廠商翻譯連接器雲端服務都必須移轉至新<code>/apps</code>位置( <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>將「上一個位置」中的現有配置遷移到「新位置」。
      <ul>
       <li>透過 <strong>AEM製作UI（位於「工具&gt;雲端服務&gt;轉譯雲端服務」）手動建立新廠商轉譯連接器雲端服務設定</strong>。<br /> 或 </li>
       <li>將任何新的供應商翻譯連接器雲端服務配置從先前位置複製到新<code>/apps</code>位置( <code>/conf/global </code>或 <code>/conf/&lt;tenant&gt;</code>)。</li>
      </ul> </li>
     <li>將適用的AEM設定與AEM內容階層建立關聯。
      <ol>
       <li>透過 <strong>AEM Sites &gt;頁面&gt;頁面屬性&gt;進階標籤&gt;雲端設定的AEM Sites頁面階層</strong>。</li>
       <li>透過 <strong>AEM體驗片段&gt;體驗片段&gt;屬性&gt;雲端服務標籤&gt;雲端設定的AEM體驗片段階層</strong>。</li>
       <li>透過 <strong>AEM Experience Fragments &gt;資料夾&gt;屬性&gt;雲端服務標籤&gt;雲端設定的AEM Experience Fragment資料夾階層</strong>。</li>
       <li>透過「 <strong>AEM Assets &gt;資料夾&gt;資料夾屬性&gt;雲端服務標籤&gt;設定」的AEM Assets資料夾階層</strong>。</li>
       <li>透過 <strong>AEM Projects &gt;專案&gt;專案屬性&gt;進階標籤&gt;雲端設定的AEM專案</strong>。</li>
      </ol> </li>
     <li>將任何移轉的舊版Translation cloud服務與前述的AEM內容階層分離。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>翻譯雲服務解析按以下順序進行：</p>
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

<table>
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
   <td><p>任何修改的工作流通知電子郵件模板都必須遷移到新位置(<code>/conf/global</code>)。</p>
    <ol>
     <li>將任何修改的工作流通知電子郵件模板從上一個位置複製到新位置。</li>
     <li>從上一個位置移除移轉的工作流程通知電子郵件範本。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>工作流程通知電子郵件範本解析依下列順序進行：</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流程套件 {#workflow-packages}

<table>
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
   <td><p>應將先前位置中的現有工作流包遷移到新位置。</p>
    <ol>
     <li>移除先前位置中未被其他內容參考且不需要的其他工作流程套件。</li>
     <li>移動先前位置中未被其他內容引用，但新位置中其他必要位置的任何工作流程套件。</li>
     <li>保留先前位置中其他內容所參照的任何工作流程套件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>透過Classic UI Miscadmin主控台建立的工作流程套件會保留在先前的位置，而其他所有套件則會保留在新位置。</p> <p>可以通過Classic UI Miscadmin控制台管理儲存在先前位置或當前位置中的工作流程式包。</p> </td>
  </tr>
 </tbody>
</table>

