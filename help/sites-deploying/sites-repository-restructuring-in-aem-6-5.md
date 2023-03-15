---
title: AEM 6.5中的Sites存放庫重新調整
seo-title: Sites Repository Restructuring in AEM 6.5
description: 了解如何進行必要的變更，以移轉至AEM 6.5 for Sites中的新存放庫結構。
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

# AEM 6.5中的Sites存放庫重新調整 {#sites-repository-restructuring-in-aem}

如父項所述 [AEM 6.5中的存放庫重新調整架構](/help/sites-deploying/repository-restructuring.md) 頁面中，升級至AEM 6.5的客戶應使用此頁面評估與影響AEM Sites解決方案的存放庫變更相關的工作量。 有些變更需要AEM 6.5升級程式中的工作量，而有些變更可能會延遲至日後升級。

**使用6.5升級**

* [ContextHub 區段](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**未來升級前**

* [Adobe Analytics用戶端程式庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [傳統Microsoft Word至網頁設計](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [行動裝置模擬器設定](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [多站點管理器Blueprint配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [多網站管理員轉出設定](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [頁面事件通知電子郵件範本](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [頁面支架](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [響應網格較少](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [靜態範本設計](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)

<!-- Search&Promote is end-of-life September 1, 2022 * [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries) -->
* [Adobe Target整合用戶端程式庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [WCM Foundation用戶端程式庫](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## 使用6.5升級 {#with-upgrade}

### ContextHub 區段 {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果要在原始碼控制項中編輯任何新的或修改的ContextHub區段，而不是在AEM中編輯，則必須將其遷移到新位置：</p>
    <ol>
     <li>將任何新的或修改的ContextHub區段從上一個位置複製到適當的新位置(/<code>apps</code>, <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>將先前位置中ContextHub區段的參考更新為新位置中移轉的ContextHub區段(<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>)。</li>
    </ol> <p>以下QueryBuilder查詢會在先前位置找到ContextHub區段的所有參考。<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> 這可透過 <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM QueryBuilder Debugger UI</a>. 請注意，這是遍歷查詢，因此請勿針對生產環境運行它，並確保根據需要調整遍歷限制。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>保存至上一個位置的ContextHub區段在 <strong>AEM &gt;個人化&gt;對象</strong>.</p> <p>若要在AEM中編輯ContextHub區段，必須移轉至新位置(<code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。 在AEM中建立的任何新ContentHub區段都會保留到新位置(<code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p> <p>AEM Sites頁面屬性僅允許上一個位置(<code>/etc</code>)或單一新位置(<code>/apps</code>, <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)，因此ContextHub區段必須據以移轉。</p> <p>任何未使用之AEM參考網站的ContextHub區段都可移除，且不會移轉至新位置：</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>注意：如果ClientContext正在使用中，建議轉換為ContextHub。</p> </td>
  </tr>
 </tbody>
</table>

## 未來升級前 {#prior-to-upgrade}

### Adobe Analytics用戶端程式庫 {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
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
     <li>應更新「上一個位置」上依路徑對用戶端程式庫的任何參考，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM用戶端程式庫參考架構</a>.</li>
     <li>如果無法使用AEM用戶端程式庫參考架構，則可透過AEM用戶端程式庫代理servlet參考用戶端程式庫的絕對路徑。
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
   <td><p>從不支援編輯這些客戶端庫。</p> <p>若要取得用戶端程式庫類別，請瀏覽 <code>cq:ClientLIbraryFolder</code> 節點，並檢查類別屬性。</p>
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

### 傳統Microsoft Word至網頁設計 {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理、而不是在運行時通過設計對話框寫入的任何設計。</p>
    <ol>
     <li>將設計從上一位置複製到新位置(<code>/apps</code>)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">用戶端程式庫</a> with <code>allowProxy = true</code>.</li>
     <li>更新cq:designPath屬性中上一個位置的引用。</li>
     <li>更新任何參考上一個位置的頁面，以使用新的用戶端程式庫類別（這需要更新頁面實作程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改運行時：</p>
    <ul>
     <li>請勿將可製作的設計移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 行動裝置模擬器設定 {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>任何新的行動裝置模擬器設定都必須移轉至新位置。
    <ol>
     <li>將任何新的行動裝置模擬器配置從上一個位置複製到新位置(<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>)。</li>
     <li>對於依賴這些行動裝置模擬器設定的任何AEM Sites頁面，請更新頁面的 <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> 節點： <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> =字串[行動/群組/回應式]</span></li>
     <li>對於依賴於這些移動設備模擬器配置的任何可編輯模板，請更新可編輯的模板，並指向 <span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span> 新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>行動裝置模擬器組態解析度依下列順序進行：</p>
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
   <td><strong>上一位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/msm</code> （客戶Blueprint設定）</p> <p><code>/libs/msm</code> （適用於Screens、Commerce的Blueprint設定現成可用）</p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的多站點管理器Blueprint配置都必須遷移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>將任何新的或修改的多站點管理器Blueprint配置從上一位置複製到新位置(<code>/apps</code>)。</li>
     <li>從上一個位置刪除所有遷移的多站點管理器Blueprint配置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>所有AEM提供的多網站管理員Blueprint設定均位於 <code>/libs</code>.</p> <p>內容不會參考多網站管理員藍色設定，因此沒有內容參考需要調整。</p> </td>
  </tr>
 </tbody>
</table>

### 多網站管理員轉出設定 {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>任何新的或修改的多網站管理員轉出設定都必須移轉至新位置。</p>
    <ol>
     <li>將任何新的或修改的多網站管理員轉出設定從上一個位置複製到新位置(<code>/apps</code>)。</li>
     <li>將AEM頁面上的任何參考更新為先前位置中的多網站管理員轉出設定，以指向新位置中的對應位置(<code>/libs</code> 或 <code>/apps</code>)。</li>
    </ol> <p>從上一個位置移除移轉的多網站管理員轉出設定。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>無法從「上一個位置」移除移轉的多網站管理員轉出設定，導致向AEM作者顯示重複轉出選項。</td>
  </tr>
 </tbody>
</table>

### 頁面事件通知電子郵件範本 {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>唯一支援的新「頁面事件通知電子郵件模板」是支援新語言環境。</p> <p>頁面事件電子郵件範本解析按以下順序發生：</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>任何新的或修改的頁面事件通知電子郵件範本都必須移轉至 <code>/apps</code>:</p>
    <ol>
     <li>將任何新的或修改的頁面事件通知電子郵件模板從上一位置複製到新位置(<code>/apps</code>)。</li>
     <li>從上一個位置刪除任何遷移的頁面事件通知電子郵件模板。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 頁面支架 {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><span class="code">/libs/settings/
      <code>
       wcm
      </code>/template-types/swargers/swabrers</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/swargers/swabrers</span></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td>在「上一位置」下建立的架構使用舊版架構，且無法移轉至新位置。 若要與新位置一致，必須使用支援的架構架構重新開發任何舊版架構。</td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 響應網格較少 {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>必須更新自定義LESS檔案中對「上一個位置」的任何引用，以從「新位置」導入。</p>
    <ul>
     <li>更新在「上一位置」中引用grid_base.less的任何引用自定義LESS檔案以引用新位置。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>參考非現有 <code>grid_base.less</code> 檔案會導致頁面和範本編輯器的「配置模式」無法運作，以及頁面配置中斷。</td>
  </tr>
 </tbody>
</table>

### 靜態範本設計 {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理、而不是在運行時通過設計對話框寫入的任何設計。</p>
    <ol>
     <li>將設計從上一位置複製到新位置(<code>/apps</code>)。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">用戶端程式庫</a> with <code>allowProxy = true</code>.</li>
     <li>更新上一個位置的參考，位於 <code>cq:designPath</code> 透過 <strong>AEM &gt;網站&gt;自訂網站頁面&gt;頁面屬性&gt;進階標籤&gt;設計欄位</strong>.</li>
     <li>更新任何參考上一個位置的頁面，以使用新的用戶端程式庫類別（這需要更新頁面實作程式碼）。</li>
     <li>更新AEM Dispatcher規則，以允許透過 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的任何設計，以及通過設計對話框修改運行時：</p>
    <ul>
     <li>請勿將可製作的設計移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>建議的方法是使用可編輯的範本來建立AEM Sites和頁面，這些範本使用結構內容和原則來取代設計。</td>
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

### Adobe Target整合用戶端程式庫 {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
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
     <li>應更新「上一個位置」上依路徑對用戶端程式庫的任何參考，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM用戶端程式庫參考架構</a>.</li>
     <li>如果無法使用AEM用戶端程式庫參考架構，則可透過AEM用戶端程式庫代理servlet參考用戶端程式庫的絕對路徑：</li>
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
   <td><p>從不支援編輯這些客戶端庫。</p> <p>若要取得「用戶端程式庫」類別，請透過CRXDELite造訪每個cq:ClientLibraryFolder節點，並檢查類別屬性：</p>
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
   <td><strong>上一位置</strong></td>
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
     <li>應更新「上一個位置」上依路徑對用戶端程式庫的任何參考，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM用戶端程式庫參考架構</a>.</li>
     <li>如果無法使用AEM用戶端程式庫參考架構，則可透過AEM用戶端程式庫代理servlet參考用戶端程式庫的絕對路徑。</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td><p>從不支援編輯這些客戶端庫。</p> <p>若要取得用戶端程式庫類別，請瀏覽 <code>cq:ClientLIbraryFolder</code> 節點，並檢查類別屬性：</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>
