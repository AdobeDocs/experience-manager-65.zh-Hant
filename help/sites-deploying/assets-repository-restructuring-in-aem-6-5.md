---
title: AEM 6.5中的資產存放庫重組
description: 瞭解如何進行必要的變更，以移轉至資產的Adobe Experience Manager (AEM) 6.5中的新存放庫結構。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---

# AEM 6.5中的資產存放庫重組 {#assets-repository-restructuring-in-aem}

如父項所述 [AEM 6.5中的存放庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級至Adobe Experience Manager (AEM) 6.5的客戶應使用此頁面評估與影響AEM Assets解決方案的存放庫變更相關的工作量。 在AEM 6.5升級程式期間，有些變更需要投入大量精力，而其他變更則可能延遲到未來升級。

**6.5版升級**

* [雜項](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**在日後升級之前**

* [資產/集合事件電子郵件通知範本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [傳統資產共用設計](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [下載資產電子郵件通知範本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [範例DRM授權](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [連結共用電子郵件通知範本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign工作流程指令碼](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [視訊轉碼設定](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [雜項](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 6.5版升級 {#with-upgrade}

### 雜項 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>如果任何自訂程式碼依賴此位置，也就是說，程式碼明確依賴此路徑，則必須更新程式碼以使用新位置，才能進行升級。 理想情況下，當可用時使用Java™ API，以減少對JCR中任何特定路徑的相依性。</p> <p>用於儲存使用者端下載的ZIP檔案的臨時位置。 使用者端要求下載資產後，就不需要更新。 它會在新位置產生檔案。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

## 在日後升級之前 {#prior-to-upgrade}

### 資產/集合事件電子郵件通知範本 {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>如果客戶修改了電子郵件範本，則請執行下列動作以符合新的存放庫結構：</p>
    <ol>
     <li>此 <code>/libs/settings/dam/notification</code> 電子郵件範本應複製自 <strong><code>/etc/notification/email/default</code></strong> 至 <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>因為目的地位於<strong> <code>/apps</code></strong>，此變更應儲存在SCM中。</li>
      </ol> </li>
     <li>移除資料夾： <strong><code>/etc/dam/notification/email/default</code></strong> 內的電子郵件範本移動後。<br />
      <ol>
       <li>如果未更新下的電子郵件範本<strong> <code>/etc/notification/email/default</code></strong>，資料夾可以移除，因為原始電子郵件範本存在於 <strong><code>/libs/settings/notification/email/default</code></strong> 作為AEM 4安裝的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### 傳統資產共用設計 {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>對於在SCM中管理，且未透過「設計」對話方塊在執行階段寫入的任何設計，請執行下列動作以對齊最新模型：</p>
    <ol>
     <li>將設計從先前位置複製到下的新位置 <code>/apps</code>.</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶庫</a> 替換為 <code>allowProxy = true</code>.</li>
     <li>更新中先前位置的參照 <code>cq:designPath</code> 屬性，方式 <strong>AEM &gt; DAM管理員&gt;資產共用頁面&gt;頁面屬性&gt;進階標籤&gt;設計欄位</strong>.</li>
     <li>若要使用新的「使用者端資源庫」類別，請更新任何參照先前位置的頁面。 這需要更新頁面實施程式碼。</li>
     <li>更新Dispatcher規則，以允許透過以下方式提供使用者端資料庫： <code>/etc.clientlibs/</code> Proxy servlet。</li>
    </ol> <p>對於任何未在SCM中管理，且透過「設計」對話方塊修改執行時間的設計，請勿將可編寫的設計移出 <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### 下載資產電子郵件通知範本 {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>如果電子郵件範本(<strong>下載adasset</strong> 或 <strong>transientworkflowcompleted</strong>)，然後依照以下程式來對齊新結構：</p>
    <ol>
     <li>更新的電子郵件範本應複製自 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> 至 <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>因為目的地位於<strong> <code>/apps</code></strong>，此變更應儲存在SCM中。</li>
      </ol> </li>
     <li>移除資料夾： <code>/etc/dam/workflow/notification/email/downloadasset </code>內的電子郵件範本移動後。<br />
      <ol>
       <li>如果未更新下的電子郵件範本<strong> <code>/etc</code></strong>，資料夾可以移除，因為原始電子郵件範本存在於 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> 作為AEM 6.4安裝的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>當 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> 技術上支援的查詢(透過一般的Sling CAConfig查詢方式在/apps之前優先，但在之後 <code>/etc</code>)範本可以放在 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. 但是，不建議這麼做，因為沒有執行階段UI可方便編輯電子郵件範本。</td>
  </tr>
 </tbody>
</table>

### 範例DRM授權 {#example-drm-licenses}

| **上一個位置** | `/etc/dam/drm/licenses/` |
|---|---|
| **新位置** | `/libs/settings/dam/drm` |
| **重組指南** | 不適用 |
| **附註** | 不適用 |

### 連結共用電子郵件通知範本 {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>如果客戶修改了電子郵件範本，則必須符合新的存放庫結構：</p>
    <ol>
     <li>更新的電子郵件範本應複製自 <strong><code>/etc/dam/adhocassetshare</code></strong> 至 <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>因為目的地位於<strong><code>/apps</code></strong>，此變更應儲存在SCM中。</li>
      </ol> </li>
     <li>移除資料夾： <strong><code>/etc/dam/adhocassetshare</code></strong> 內的電子郵件範本移動後。<br />
      <ol>
       <li>如果未更新下的電子郵件範本<strong> <code>/etc</code></strong>，資料夾可以移除，因為原始電子郵件範本存在於 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> 作為AEM 6.4安裝的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>當 <code>/conf/global/settings/dam/adhocassetshare</code> 技術上支援查詢(優先於 <code>/apps</code> 透過一般的Sling CacOnfig查閱，但在 <code>/etc</code>)，則範本可放在 <code>/conf/global/settings/dam/adhocassetshare</code>. 但是，不建議這麼做，因為沒有執行階段UI來方便編輯電子郵件範本</td>
  </tr>
 </tbody>
</table>

### InDesign工作流程指令碼 {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>若要與新的存放庫結構對齊：</p>
    <ol>
     <li>複製所有自訂或修改的指令碼來源 <strong><code>/etc/dam/indesign/scripts</code></strong> 至 <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>只有複製新的或修改過的指令碼，才能作為AEM未修改的指令碼使用，其方式為 <strong><code>/libs/settings</code></strong> 在AEM 6.5中</li>
      </ol> </li>
     <li>找到所有使用媒體提取程式WF步驟的工作流程模型，並
      <ol>
       <li>針對「工作流程步驟」的每個例項，更新config中的路徑，以明確指向下的適當指令碼<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> 或 <strong><code>/libs/settings/dam/indesign/scripts</code></strong> 視情況而定。</li>
      </ol> </li>
     <li>移除<strong> <code>/etc/dam/indesign/scripts</code></strong> 全部。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>建議將自訂指令碼儲存在 <code>/apps</code>，因為這是應儲存程式碼的位置。</td>
  </tr>
 </tbody>
</table>

### 視訊轉碼設定 {#video-transcoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>專案層級自訂必須剪下並貼在等效專案下 <code>/apps</code> 或 <code>/conf</code> 路徑是否適用。</p> <p>若要與AEM 6.4存放庫結構一致：</p>
    <ol>
     <li>複製任何修改的視訊設定，從 <code>/etc/dam/video</code> 至 <code>/apps/settings/dam/video</code></li>
     <li>移除 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 檢視器預設集設定 {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>對於現成的檢視器預設集，它僅適用於新位置。</p> <p>對於自訂檢視器預設集：</p>
    <ul>
     <li>執行移轉指令碼，讓您可以將節點從 <code>/etc</code> 至 <code>/conf</code>. 指令碼位於 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>或者，您可以編輯組態，它們會自動儲存到新位置。</li>
    </ul> <p>您不必調整其copyURL/內嵌程式碼以指向 <code>/conf</code>. 現有要求至 <code>/etc</code> 被重新路由到正確的內容，從 <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 雜項 {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>調整任何參照以指向下的新資源 <code>/libs</code> 使用 <code>/etc.clientlibs/</code> 允許Proxy前置詞。</p> <p>最後，透過從移除已移轉的clientlibs的資料夾來清理 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>
