---
title: 6.5中的站AEM點儲存庫重組
seo-title: Sites Repository Restructuring in AEM 6.5
description: 瞭解如何進行必要的更改，以便遷移到6.5版中的AEM新站點儲存庫結構。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for Sites.
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
feature: Upgrading
exl-id: b4531792-06dd-4545-9dbb-57224be20dc7
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 1%

---

# 6.5中的站AEM點儲存庫重組 {#sites-repository-restructuring-in-aem}

如父代中所述 [6.5中的AEM儲存庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級到AEM6.5的客戶應使用此頁面評估與影響AEM Sites解決方案的儲存庫更改相關的工作量。 某些更改需要在6.5升AEM級過程中進行工作，而其他更改則可以推遲到以後升級。

**使用6.5升級**

* [ContextHub 區段](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**未來升級前**

* [Adobe Analytics客戶端庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [經典Microsoft詞到網頁設計](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [移動設備模擬器配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [多站點管理器藍圖配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [多站點管理器部署配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [頁面事件通知電子郵件模板](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [頁腳手架](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [響應性網格](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [靜態模板設計](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)

<!-- Search&Promote is end-of-life September 1, 2022 * [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries) -->
* [Adobe Target整合客戶端庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [WCM Foundation客戶端庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## 使用6.5升級 {#with-upgrade}

### ContextHub 區段 {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果任何新的或修改的ContextHub網段都打算在原始碼管理中編輯，而不是在中編輯，AEM則必須將它們遷移到新位置：</p>
    <ol>
     <li>將任何新的或已修改的ContextHub段從上一個位置複製到相應的新位置(/<code>apps</code>。 <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>將上一個位置中對ContextHub段的引用更新到新位置中遷移的ContextHub段(<code>/apps</code>。 <code>/conf/global</code>。 <code>/conf/&lt;tenant&gt;</code>)。</li>
    </ol> <p>以下QueryBuilder查詢將查找前一位置中對ContextHub段的所有引用。<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> 可通過 <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEMQueryBuilder調試器UI</a>。 請注意，這是遍歷查詢，因此不要針對生產運行它，並確保根據需要調整遍歷限制。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>ContextHub段保留到上一個位置，顯示為只讀 <strong>AEM&gt;個性化&gt;受眾</strong>。</p> <p>如果要在中可編輯ContextHub網AEM段，則必須將其遷移到新位置(<code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。 在中建立的任何新ContentHub網段AEM都會保留到新位置(<code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p> <p>AEM Sites頁屬性僅允許上一個位置(<code>/etc</code>)或單個新位置(<code>/apps</code>。 <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)，因此必須相應遷移ContextHub段。</p> <p>可以從引用站點中AEM刪除任何未使用的ContextHub段，但不能將其遷移到新位置：</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx outdoors</li>
    </ul> <p>注：如果正在使用ClientContext，建議轉換為ContextHub。</p> </td>
  </tr>
 </tbody>
</table>

## 未來升級前 {#prior-to-upgrade}

### Adobe Analytics客戶端庫 {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>這些客戶端庫的任何自定義使用都應按類別引用客戶端庫，而不是按路徑引用：</p>
    <ol>
     <li>應更新「上一個位置」上按路徑對客戶端庫的任何引用以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">客AEM戶端庫引用框架</a>。</li>
     <li>如AEM果無法使用客戶端庫引用框架，則可以通過客戶端庫代理Servlet引AEM用客戶端庫的絕對路徑。
      <ul>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/appmeasurement.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/plugins.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/tracking.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/util.js</code></li>
      </ul> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>從不支援編輯這些客戶端庫。</p> <p>要獲取客戶端庫類別，請訪問 <code>cq:ClientLIbraryFolder</code> 節點，並檢查categories屬性。</p>
    <ul>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/appmeasurement</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/plugins</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/tracking</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 經典Microsoft詞到網頁設計 {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理且未通過設計對話框在運行時寫入的任何設計。</p>
    <ol>
     <li>將設計從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶端庫</a> 與 <code>allowProxy = true</code>。</li>
     <li>更新cq:designPath屬性中對「上一個位置」的引用。</li>
     <li>更新引用上一個位置的任何頁面以使用新的客戶端庫類別（這需要更新頁面實施代碼）。</li>
     <li>更新AEMDispatcher規則以允許通過 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改的運行時：</p>
    <ul>
     <li>不要將可創作的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 移動設備模擬器配置 {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>任何新的移動設備模擬器配置都必須遷移到新位置。
    <ol>
     <li>將任何新的移動設備模擬器配置從上一位置複製到新位置(<code>/apps</code>。 <code>/conf/global</code>。 <code>/conf/&lt;tenant&gt;</code>)。</li>
     <li>對於依賴於這些移動設備模擬器配置的任何AEM Sites頁，請更新該頁的 <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> 節點： <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> =字串[移動/組/響應]</span></li>
     <li>對於依賴於這些移動設備模擬器配置的任何可編輯模板，請更新可編輯模板，並指向 <span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span> 到新建位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>移動設備模擬器配置解析按以下順序進行：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li><code>/conf/global/settings/mobile</code></li>
     <li><code>/apps/settings/mobile</code></li>
     <li><code>/libs/settings/mobile</code></li>
     <li><code>/etc/mobile</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 多站點管理器藍圖配置 {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/msm</code> （客戶藍圖配置）</p> <p><code>/libs/msm</code> （螢幕、商業的現成藍圖配置）</p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的多站點管理器藍圖配置都必須遷移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>將任何新的或修改的多站點管理器藍圖配置從上一位置複製到新位置(<code>/apps</code>)。</li>
     <li>從上一個位置刪除所有遷移的多站點管理器藍圖配置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>所AEM有提供的多站點管理器藍圖配置都位於 <code>/libs</code>。</p> <p>內容不引用多站點管理器藍色配置，因此沒有要調整的內容引用。</p> </td>
  </tr>
 </tbody>
</table>

### 多站點管理器部署配置 {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的多站點管理器部署配置都必須遷移到新位置。</p>
    <ol>
     <li>將任何新的或修改的多站點管理器部署配置從上一位置複製到新位置(<code>/apps</code>)。</li>
     <li>將頁面上的AEM任何引用更新到上一個位置中的多站點管理器部署配置，以指向新位置中的對應位置(<code>/libs</code> 或 <code>/apps</code>)。</li>
    </ol> <p>從上一個位置刪除遷移的多站點管理器部署配置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>未能從「上一個位置」中刪除遷移的多站點管理器部署配置將導致向作者顯示重複的部署AEM選項。</td>
  </tr>
 </tbody>
</table>

### 頁面事件通知電子郵件模板 {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>唯一支援的新頁面事件通知電子郵件模板是支援新語言環境。</p> <p>頁面事件電子郵件模板解析按以下順序進行：</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>任何新的或修改的頁面事件通知電子郵件模板必須遷移到以下位置 <code>/apps</code>:</p>
    <ol>
     <li>將任何新的或修改的頁面事件通知電子郵件模板從上一位置複製到新位置(<code>/apps</code>)。</li>
     <li>從上一個位置刪除任何遷移的頁面事件通知電子郵件模板。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 頁腳手架 {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><span class="code">/libs/settings//
      <code>
       wcm
      </code>/模板類型/腳手架/腳手架</span></p> <p><span class="code">/apps/settings//
      <code>
       wcm
      </code>/模板類型/腳手架/腳手架</span></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>在上一個位置下建立的腳手架使用傳統腳手架，無法遷移到新位置。 為了與新地點保持一致，任何舊腳手架必須使用支撐腳手架重新開發。</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 響應性網格 {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>必須更新對自定義LESS檔案中「上一個位置」(Previous Location)的任何引用，以從「新建位置」(New Location)導入。</p>
    <ul>
     <li>更新引用「上一位置」中引用grid_base.less的任何引用自定義LESS檔案以引用新位置。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>引用非現有 <code>grid_base.less</code> 檔案導致頁面和模板編輯器的佈局模式無法工作，並導致頁面佈局中斷。</td>
  </tr>
 </tbody>
</table>

### 靜態模板設計 {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理且未通過設計對話框在運行時寫入的任何設計。</p>
    <ol>
     <li>將設計從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶端庫</a> 與 <code>allowProxy = true</code>。</li>
     <li>更新對中上一個位置的引用 <code>cq:designPath</code> 屬性 <strong>&gt;站AEM點&gt;自定義站點頁&gt;頁面屬性&gt;高級頁籤&gt;設計欄位</strong>。</li>
     <li>更新引用上一個位置的任何頁面以使用新的客戶端庫類別（這需要更新頁面實施代碼）。</li>
     <li>更新AEMDispatcher規則以允許通過 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改的運行時：</p>
    <ul>
     <li>不要將可創作的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>建議的方法是使用可編輯模板構建AEM Sites和頁面，這些模板使用結構內容和策略代替設計。</td>
  </tr>
 </tbody>
</table>

<!-- Search&Promote is end of life as of September 1, 2022 ### Adobe Search and Promote Integration Client Libraries {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Previous location</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>New location(s)</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Restructuring guidance</strong></td>
   <td><p>Any custom use of these Client Libraries should reference the Client Library by category, and not by path.</p>
    <ol>
     <li>Any references to the Client Library by path at the Previous Location should be updated to use <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM's Client Library referencing framework</a>.</li>
     <li>If AEM's Client Library referencing framework cannot be used, the absolute path of the Client Libraries can be referenced via AEM's Client Library Proxy servlet:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td><p>Editing of these Client Libraries was never supported.</p> <p>To obtain the Client Library categories, visit each cq:ClientLIbraryFolder node via CRXDELite and inspect the categories property:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table> -->

### Adobe Target整合客戶端庫 {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>這些客戶端庫的任何自定義使用都應按類別引用客戶端庫，而不是按路徑引用。</p>
    <ol>
     <li>應更新「上一個位置」上按路徑對客戶端庫的任何引用以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">客AEM戶端庫引用框架</a>。</li>
     <li>如果AEM無法使用客戶端庫引用框架，則可以通過客戶端庫代理Servlet引用客戶端庫AEM的絕對路徑：</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/testandtarget.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs-integration.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/init.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/mbox.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/parameters.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/util.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>從不支援編輯這些客戶端庫。</p> <p>要獲取客戶端庫類別，請通過CRXDELite訪問每個cq:ClientLIbraryFolder節點並檢查categies屬性：</p>
    <ul>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/testandtarget</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs-integration</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/init</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/mbox</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/parameters</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### WCM Foundation客戶端庫 {#wcm-foundation-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>這些客戶端庫的任何自定義使用都應按類別引用客戶端庫，而不是按路徑引用。</p>
    <ol>
     <li>應更新「上一個位置」上按路徑對客戶端庫的任何引用以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">客AEM戶端庫引用框架</a>。</li>
     <li>如AEM果無法使用客戶端庫引用框架，則可以通過客戶端庫代理Servlet引AEM用客戶端庫的絕對路徑。</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>從不支援編輯這些客戶端庫。</p> <p>要獲取客戶端庫類別，請訪問 <code>cq:ClientLIbraryFolder</code> 節點，並檢查categories屬性：</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>
