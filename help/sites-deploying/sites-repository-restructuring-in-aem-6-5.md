---
title: AEM 6.5中的網站存放庫重組
description: 瞭解如何進行必要的變更，以移轉至AEM 6.5中適用於Sites的新存放庫結構。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: b4531792-06dd-4545-9dbb-57224be20dc7
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 1%

---

# AEM 6.5中的網站存放庫重組 {#sites-repository-restructuring-in-aem}

如AEM 6.5[&#128279;](/help/sites-deploying/repository-restructuring.md)頁面的上層存放庫重新調整中所述，升級至AEM 6.5的客戶應使用此頁面來評估與影響AEM Sites解決方案的存放庫變更相關的工作量。 在AEM 6.5升級程式期間，有些變更需要投入大量精力，而其他變更則可能延遲到未來升級。

**升級為6.5**

* [ContextHub 區段](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**未來升級之前**

* [Adobe Analytics使用者端資料庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [從傳統Microsoft Word轉換為網頁設計](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [行動裝置模擬器設定](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [多站點管理員藍圖設定](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [多網站管理員轉出設定](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [頁面事件通知電子郵件範本](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [頁面支架](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [回應式格線較少](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [靜態範本設計](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
<!-- Search&Promote is end-of-life September 1, 2022 * [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries) -->
* [Adobe Target整合使用者端程式庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [WCM Foundation使用者端程式庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## 6.5版升級 {#with-upgrade}

### ContextHub 區段 {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code><br /> </p> <p><code>/conf/settings/settings/wcm/segments</code><br /> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>如果有任何新或修改過的ContextHub區段是在原始檔控制中編輯，而非在AEM中編輯，則必須將其移轉至新位置：</p>
    <ol>
     <li>將先前位置的任何新或修改ContextHub區段複製到適當的新位置（/<code>apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）</li>
     <li>將先前位置中ContextHub區段的參考更新為新位置(<code>/apps</code>、<code>/conf/global</code>、<code>/conf/&lt;tenant&gt;</code>)中已移轉的ContextHub區段。</li>
    </ol> <p>下列QueryBuilder查詢會找出先前位置中ContextHub區段的所有參考。<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br />這可透過<a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM QueryBuilder Debugger UI</a>執行。 請注意，這是周遊查詢，因此請勿對生產執行它，並確保視需要調整周遊限制。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>儲存至先前位置的ContextHub區段，在<strong>AEM &gt; Personalization &gt; Audiences</strong>中顯示為唯讀。</p> <p>如果要在AEM中編輯ContextHub區段，必須將其移轉至新位置（<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。 任何在AEM中建立的新ContentHub區段都會保留至新位置（<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。</p> <p>AEM Sites頁面屬性僅允許選取先前位置(<code>/etc</code>)或單一新位置（<code>/apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>），因此必須據此移轉ContextHub區段。</p> <p>可以從AEM參考網站移除任何未使用的ContextHub區段，且不會移轉到新位置：</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segment/geometrixx-outdoors</li>
    </ul> <p>注意：如果ClientContext正在使用中，建議將其轉換為ContextHub。</p> </td>
  </tr>
 </tbody>
</table>

## 未來升級之前 {#prior-to-upgrade}

### Adobe Analytics使用者端資料庫 {#adobe-analytics-client-libraries}

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
   <td><strong>重組指南</strong></td>
   <td><p>這些使用者端資料庫的任何自訂使用都應依類別而非路徑參照使用者端資料庫：</p>
    <ol>
     <li>應更新先前位置依路徑對使用者端程式庫的任何參考，以使用<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的使用者端程式庫參考架構</a>。</li>
     <li>如果無法使用AEM使用者端程式庫參考架構，則可透過AEM的使用者端程式庫Proxy servlet參考使用者端程式庫的絕對路徑。
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
   <td><p>不支援編輯這些使用者端資料庫。</p> <p>若要取得使用者端資料庫類別，請透過CRXDELite造訪每個<code>cq:ClientLIbraryFolder</code>節點，並檢查類別屬性。</p>
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

### 從傳統Microsoft Word轉換為網頁設計 {#classic-microsoft-word-to-web-page-designs}

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
   <td><strong>重組指南</strong></td>
   <td><p>對於任何在SCM中管理，且未透過設計對話方塊在執行階段寫入的設計。</p>
    <ol>
     <li>將設計從先前位置複製到新位置(<code>/apps</code>)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">使用者端資料庫</a>。</li>
     <li>更新對cq：designPath屬性中「先前位置」的參照。</li>
     <li>更新任何參考先前位置的頁面，以使用新的使用者端程式庫類別（這需要更新頁面實施程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過<code>/etc.clientlibs/</code> Proxy Servlet提供使用者端資料庫。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及透過「設計」對話方塊修改的執行時間：</p>
    <ul>
     <li>請勿將可編寫的設計移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### 行動裝置模擬器設定 {#mobile-device-emulator-configurations}

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
   <td><strong>重組指南</strong></td>
   <td>任何新的行動裝置模擬器設定都必須移轉至新位置。
    <ol>
     <li>將任何新的行動裝置模擬器設定從先前位置複製到新位置(<code>/apps</code>、<code>/conf/global</code>、<code>/conf/&lt;tenant&gt;</code>)。</li>
     <li>對於依賴這些行動裝置模擬器設定的任何AEM Sites頁面，請更新頁面的<span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span>節點： <br /> <span class="code">[cq：Page]/jcr：content@cq：
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>對於相依於這些行動裝置模擬器設定的任何可編輯範本，請更新指向<span class="code">的可編輯範本
       <code>
        cq
       </code>：
       <code>
        deviceGroups
       </code></span>至新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>行動裝置模擬器設定的解析度會依下列順序發生：</p>
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

### 多站點管理員藍圖設定 {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/msm</code> （客戶Blueprint設定）</p> <p><code>/libs/msm</code> (Screens、Commerce的現成藍圖設定)</p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>任何新的或修改過的多站台管理員藍圖設定都必須移轉到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>將任何新的或修改過的多站點管理員Blueprint設定從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>從先前的位置移除所有已移轉的多站點管理員藍圖設定。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>所有AEM提供的多網站管理員藍圖設定都存在於<code>/libs</code>中的新位置。</p> <p>內容未參照多站點管理員藍色設定，因此沒有要調整的內容參照。</p> </td>
  </tr>
 </tbody>
</table>

### 多網站管理員轉出設定 {#multi-site-manager-rollout-configurations}

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
   <td><strong>重組指南</strong></td>
   <td><p>任何新的或修改過的「多網站管理員轉出設定」都必須移轉到新位置。</p>
    <ol>
     <li>將任何新的或修改過的多站點管理員轉出設定從先前位置複製到新位置(<code>/apps</code>)。</li>
     <li>將AEM頁面上任何參考更新至先前位置的多網站管理員轉出設定，以指向新位置（<code>/libs</code>或<code>/apps</code>）中的對應專案。</li>
    </ol> <p>從先前的位置移除已移轉的多站台管理員轉出設定。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>如果無法從先前位置移除已移轉的多網站管理員轉出設定，會導致向AEM作者顯示重複的轉出選項。</td>
  </tr>
 </tbody>
</table>

### 頁面事件通知電子郵件範本 {#page-event-notification-e-mail-template}

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
   <td><strong>重組指南</strong></td>
   <td><p>唯一支援的新頁面事件通知電子郵件範本是支援新地區設定。</p> <p>頁面事件電子郵件範本解析度的發生順序如下：</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>任何新的或修改過的頁面事件通知電子郵件範本都必須移轉至<code>/apps</code>下的新位置：</p>
    <ol>
     <li>將任何新的或修改過的頁面事件通知電子郵件範本從先前位置複製到新位置(<code>/apps</code>)。</li>
     <li>移除先前位置的任何已移轉頁面事件通知電子郵件範本。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 頁面支架 {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><span class="code">/libs/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td>在「先前位置」下建立的支架會使用舊版支架架構，且無法移轉至新位置。 為了與新位置保持一致，必須使用支援的支架框架重新開發任何舊式支架。</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### 回應式格線較少 {#responsive-grid-less}

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
   <td><strong>重組指南</strong></td>
   <td><p>必須更新自訂LESS檔案中對「先前位置」的任何參照，才能從「新位置」匯入。</p>
    <ul>
     <li>更新任何參照自訂LESS檔案，該檔案參照了「先前位置」中的grid_base.less，以參照新位置。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>參考不存在的<code>grid_base.less</code>檔案會導致頁面和範本編輯器的版面配置模式無法運作，並中斷頁面版面配置。</td>
  </tr>
 </tbody>
</table>

### 靜態範本設計 {#static-template-designs}

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
   <td><strong>重組指南</strong></td>
   <td><p>對於任何在SCM中管理，且未透過設計對話方塊在執行階段寫入的設計。</p>
    <ol>
     <li>將設計從先前位置複製到新位置(<code>/apps</code>)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">使用者端資料庫</a>。</li>
     <li>透過<strong>AEM &gt;網站&gt;自訂網站頁面&gt;頁面屬性&gt;進階標籤&gt;設計欄位</strong>，更新對<code>cq:designPath</code>屬性中先前位置的參考。</li>
     <li>更新任何參考先前位置的頁面，以使用新的使用者端程式庫類別（這需要更新頁面實施程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過<code>/etc.clientlibs/</code> Proxy servlet提供使用者端資料庫。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及透過「設計」對話方塊修改的執行時間：</p>
    <ul>
     <li>請勿將可編寫的設計移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>建議的方法是使用可編輯範本來建立AEM Sites和頁面，這些範本使用結構內容和原則來取代設計。</td>
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

### Adobe Target整合使用者端程式庫 {#adobe-target-integration-client-libraries}

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
   <td><strong>重組指南</strong></td>
   <td><p>這些使用者端資料庫的任何自訂使用都應依類別而非路徑參照使用者端資料庫。</p>
    <ol>
     <li>應更新先前位置依路徑對使用者端程式庫的任何參考，以使用<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的使用者端程式庫參考架構</a>。</li>
     <li>如果無法使用AEM使用者端程式庫參考架構，則可透過AEM的使用者端程式庫Proxy servlet參考使用者端程式庫的絕對路徑：</li>
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
   <td><p>不支援編輯這些使用者端資料庫。</p> <p>若要取得使用者端資料庫類別，請透過CRXDELite造訪每個cq：ClientLIbraryFolder節點，並檢查類別屬性：</p>
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

### WCM Foundation使用者端程式庫 {#wcm-foundation-client-libraries}

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
   <td><strong>重組指南</strong></td>
   <td><p>這些使用者端資料庫的任何自訂使用都應依類別而非路徑參照使用者端資料庫。</p>
    <ol>
     <li>應更新先前位置依路徑對使用者端程式庫的任何參考，以使用<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的使用者端程式庫參考架構</a>。</li>
     <li>如果無法使用AEM使用者端程式庫參考架構，則可透過AEM的使用者端程式庫Proxy servlet參考使用者端程式庫的絕對路徑。</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>不支援編輯這些使用者端資料庫。</p> <p>若要取得使用者端資料庫類別，請透過CRXDELite造訪每個<code>cq:ClientLIbraryFolder</code>節點，並檢查類別屬性：</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>
