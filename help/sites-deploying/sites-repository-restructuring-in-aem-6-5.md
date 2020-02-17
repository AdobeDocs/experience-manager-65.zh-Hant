---
title: AEM 6.5中的Sites Repository Restructing
seo-title: AEM 6.5中的Sites Repository Restructing
description: 瞭解如何進行必要的變更，以移轉至AEM 6.5 for Sites中的新儲存庫結構。
seo-description: 瞭解如何進行必要的變更，以移轉至AEM 6.5 for Sites中的新儲存庫結構。
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5中的Sites Repository Restructing {#sites-repository-restructuring-in-aem}

如「AEM 6.5 [](/help/sites-deploying/repository-restructuring.md) 」中的父資料庫重組頁面所述，升級至AEM 6.5的客戶應使用此頁面來評估與影響AEM Sites Solution的資料庫變更相關的工作成果。 有些變更需要在AEM 6.5升級程式中努力工作，而其他變更則可延後至日後升級。

**使用6.5升級**

* [ContextHub 區段](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**未來升級前**

* [Adobe Analytics用戶端程式庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [傳統的Microsoft word網頁設計](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [行動裝置模擬器組態](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [多站點管理器Blueprint配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [多站點管理器推廣配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [頁面事件通知電子郵件範本](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [頁面支架](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [互動式格線](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [靜態範本設計](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [Adobe Search and Promote整合用戶端程式庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [Adobe Target整合用戶端程式庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [WCM Foundation用戶端程式庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

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
   <td><p>如果任何新的或修改的ContextHub區段是要在來源控制項中編輯，而非在AEM中編輯，則必須將它們移轉至新位置：</p>
    <ol>
     <li>將任何新的或已修改的ContextHub區段從先前位置複製到適當的新位置(/<code>apps</code>、 <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>將先前位置中ContextHub區段的參考更新為新位置(、、)中已移轉的ContextHub<code>/apps</code>區 <code>/conf/global</code>段 <code>/conf/&lt;tenant&gt;</code>的參考。</li>
    </ol> <p>下列QueryBuilder查詢會在先前位置中找到ContextHub區段的所有參考。<br /> 這 <br /><code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> 可 <br /> 以透過 <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM queryBuilder除錯程式UI執行</a>。 請注意，這是遍歷查詢，因此不要針對生產運行它，並確保根據需要調整遍歷限制。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>ContextHub區段持續存在至先前位置，在 <strong>AEM &gt;個人化&gt;觀眾中顯示為唯讀</strong>。</p> <p>若要在AEM中編輯ContextHub區段，則必須將它們移轉至新<code>/conf/global</code> 位置( <code>/conf/&lt;tenant&gt;</code>或)。 在AEM中建立的任何新ContentHub區段都會持續存留至新<code>/conf/global</code> 位置( <code>/conf/&lt;tenant&gt;</code>或)。</p> <p>AEM網站頁面屬性僅允許選取「上一個位置」(<code>/etc</code>)或單一新位置(<code>/apps</code><code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)，因此ContextHub區段必須相應移轉。</p> <p>AEM參考網站中任何未使用的ContextHub區段都可以移除，而不會移轉至新位置：</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>注意：如果使用ClientContext，建議轉換為ContextHub。</p> </td>
  </tr>
 </tbody>
</table>

## 未來升級前 {#prior-to-upgrade}

### Adobe Analytics用戶端程式庫 {#adobe-analytics-client-libraries}

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
   <td><p>對這些客戶端庫的任何自定義使用都應按類別引用客戶端庫，而不是按路徑引用：</p>
    <ol>
     <li>依「上一個位置」的路徑對「用戶端程式庫」的任何參照都應更新，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的「用戶端程式庫」參照架構</a>。</li>
     <li>如果無法使用AEM的用戶端程式庫參考架構，則可透過AEM的用戶端程式庫Proxy Servlet參考用戶端程式庫的絕對路徑。
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
   <td><p>不支援編輯這些用戶端程式庫。</p> <p>若要取得「用戶端程式庫」類別，請透過CRXDELite <code>cq:ClientLIbraryFolder</code> 造訪每個節點，並檢查類別屬性。</p>
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

### 傳統的Microsoft word網頁設計 {#classic-microsoft-word-to-web-page-designs}

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
   <td><p>適用於任何以SCM管理且不在執行時期透過設計對話方塊寫入的設計。</p>
    <ol>
     <li>將設計從「上一個位置」複製到「新位置」(<code>/apps</code>)。</li>
     <li>將「設計」中的任何CSS、JavaScript和靜態資源轉換為用戶 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">端程式庫</a> , <code>allowProxy = true</code>包含</li>
     <li>在cq:designPath屬性中更新對「上一個位置」的參照。</li>
     <li>更新參照「上一位置」的任何頁面，以使用新的「用戶端程式庫」類別（這需要更新「頁面」實作代碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過Proxy servlet提供用戶端 <code>/etc.clientlibs/</code> 程式庫。</li>
    </ol> <p>對於未在SCM中管理且透過設計對話方塊修改執行時期的任何設計：</p>
    <ul>
     <li>請勿將可編寫的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 行動裝置模擬器組態 {#mobile-device-emulator-configurations}

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
   <td>任何新的行動裝置模擬器組態都必須移轉至新位置。
    <ol>
     <li>將任何新的行動裝置模擬器組態從「上一個位置」複製到新<code>/apps</code>位置( <code>/conf/global</code>、 <code>/conf/&lt;tenant&gt;</code>)。</li>
     <li>對於依賴這些行動裝置模擬器設定的任何AEM網站頁面，請更新頁面的節 <span class="code">點 <code>
        jcr
       </code><code>
        :content
       </code></span> : <br /> [ <span class="code">cq:Page]/jcr:content@cq:       <code>
        deviceGroups
       </code> =字串[ mobile/groups/responsive ]</span></li>
     <li>對於依賴於這些移動設備模擬器配置的任何可編輯模板，請更新可編輯模板，指 <span class="code"><code>
        cq
       </code>向：       到 <code>
        deviceGroups
       </code></span> 新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>行動裝置模擬器組態解析度依下列順序產生：</p>
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

### 多站點管理器Blueprint配置 {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/msm</code> （客戶藍圖配置）</p> <p><code>/libs/msm</code> （適用於螢幕、商務的Blueprint設定立即可用）</p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的多站點管理器Blueprint配置都必須遷移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>將任何新的或修改的多站點管理器Blueprint配置從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>從上一個位置移除所有遷移的多站點管理器Blueprint配置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>所有AEM提供的「多網站管理員Blueprint設定」都存在於的「新位置」中 <code>/libs</code>。</p> <p>內容不參考多站點管理器藍色配置，因此沒有要調整的內容引用。</p> </td>
  </tr>
 </tbody>
</table>

### 多站點管理器推廣配置 {#multi-site-manager-rollout-configurations}

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
   <td><p>任何新的或修改的多站點管理器轉出配置都必須遷移到新位置。</p>
    <ol>
     <li>將任何新的或修改的多站點管理器轉出配置從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>將「AEM頁面」上的任何參照更新為「上一個位置」中的「多網站管理員轉出設定」，以指向「新位置」(或<code>/libs</code> )中的對 <code>/apps</code>應者。</li>
    </ol> <p>從上一個位置移除移轉的多網站管理員轉出組態。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>無法從「上一個位置」移除移轉的「多網站管理員轉出設定」，會導致重複轉出選項顯示給AEM作者。</td>
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
   <td><strong>重組指導</strong></td>
   <td><p>唯一支援的新頁面事件通知電子郵件範本是支援新地區設定。</p> <p>頁面事件電子郵件範本解析依下列順序發生：</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>任何新的或修改的頁面事件通知電子郵件模板都必須遷移到以下位置： <code>/apps</code></p>
    <ol>
     <li>將任何新的或修改的頁面事件通知電子郵件模板從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>從上一個位置移除任何已移轉的頁面事件通知電子郵件範本。</li>
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
   <td><p><span class="code">/libs/settings/ <code>
       wcm
      </code>/template-types/shawblers/swablers</span></p> <p><span class="code">/apps/settings/ <code>
       wcm
      </code>/template-types/shawblers/swablers</span></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>在「上一個位置」下建立的腳手架使用舊版「腳手架」架構，無法移轉至「新位置」。 要與新位置保持一致，任何舊式腳手架都必須使用支援的腳手架架構重新開發。</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 互動式格線 {#responsive-grid-less}

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
   <td><p>對自定義LESS檔案中「上一個位置」(Previous Location)的任何引用都必須更新為從「新位置」(New Location)導入。</p>
    <ul>
     <li>更新在「上一個位置」中引用grid_base.less的任何引用自定義LESS檔案以引用新位置。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>參照非現有檔案 <code>grid_base.less</code> 會導致頁面和範本編輯器的「版面模式」無法運作，並中斷頁面版面配置。</td>
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
   <td><strong>重組指導</strong></td>
   <td><p>適用於任何以SCM管理且不在執行時期透過設計對話方塊寫入的設計。</p>
    <ol>
     <li>將設計從「上一個位置」複製到「新位置」(<code>/apps</code>)。</li>
     <li>將「設計」中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">用戶端程式庫</a><code>allowProxy = true</code>。</li>
     <li>透過 <code>cq:designPath</code> AEM &gt;網站&gt;自訂網站頁面&gt;頁面屬性&gt;進階標籤&gt;設計欄位，更新屬性中「上一個位置」的參考 <strong></strong>。</li>
     <li>更新參照「上一位置」的任何頁面，以使用新的「用戶端程式庫」類別（這需要更新「頁面」實作代碼）。</li>
     <li>更新AEM Dispatcher規則，允許透過Proxy servlet提供用戶端 <code>/etc.clientlibs/</code> 程式庫。</li>
    </ol> <p>對於未在SCM中管理且透過設計對話方塊修改執行時期的任何設計：</p>
    <ul>
     <li>請勿將可編寫的設計移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>建議的方法是使用可編輯範本來建立AEM網站和頁面，這些範本使用結構內容和原則來取代設計。</td>
  </tr>
 </tbody>
</table>

### Adobe Search and Promote整合用戶端程式庫 {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對這些客戶機庫的任何自定義使用都應按類別引用客戶機庫，而不是按路徑引用。</p>
    <ol>
     <li>依「上一個位置」的路徑對「用戶端程式庫」的任何參照都應更新，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的「用戶端程式庫」參照架構</a>。</li>
     <li>如果無法使用AEM的用戶端程式庫參考架構，則可透過AEM的用戶端程式庫Proxy servlet參考用戶端程式庫的絕對路徑：</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>不支援編輯這些用戶端程式庫。</p> <p>要獲取「客戶端庫」類別，請通過CRXDELite訪問每個cq:ClientLibraryFolder節點並檢查類別屬性：</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Adobe Target整合用戶端程式庫 {#adobe-target-integration-client-libraries}

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
   <td><p>對這些客戶機庫的任何自定義使用都應按類別引用客戶機庫，而不是按路徑引用。</p>
    <ol>
     <li>依「上一個位置」的路徑對「用戶端程式庫」的任何參照都應更新，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的「用戶端程式庫」參照架構</a>。</li>
     <li>如果無法使用AEM的用戶端程式庫參考架構，則可透過AEM的用戶端程式庫Proxy servlet參考用戶端程式庫的絕對路徑：</li>
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
   <td><p>不支援編輯這些用戶端程式庫。</p> <p>要獲取「客戶端庫」類別，請通過CRXDELite訪問每個cq:ClientLibraryFolder節點並檢查類別屬性：</p>
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

### WCM Foundation用戶端程式庫 {#wcm-foundation-client-libraries}

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
   <td><p>對這些客戶機庫的任何自定義使用都應按類別引用客戶機庫，而不是按路徑引用。</p>
    <ol>
     <li>依「上一個位置」的路徑對「用戶端程式庫」的任何參照都應更新，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的「用戶端程式庫」參照架構</a>。</li>
     <li>如果無法使用AEM的用戶端程式庫參考架構，則可透過AEM的用戶端程式庫Proxy Servlet參考用戶端程式庫的絕對路徑。</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>不支援編輯這些用戶端程式庫。</p> <p>若要取得「用戶端程式庫」類別，請透過CRXDELite <code>cq:ClientLIbraryFolder</code> 造訪每個節點，並檢查類別屬性：</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

