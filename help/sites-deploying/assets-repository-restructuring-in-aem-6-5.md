---
title: AEM 6.5中的資產存放庫重新調整
seo-title: Assets Repository Restructuring in AEM 6.5
description: 了解如何進行必要的變更，以移轉至AEM 6.5 for Assets中的新存放庫結構。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 2%

---

# AEM 6.5中的資產存放庫重新調整 {#assets-repository-restructuring-in-aem}

如父項所述 [AEM 6.5中的存放庫重新調整架構](/help/sites-deploying/repository-restructuring.md) 頁面中，升級至AEM 6.5的客戶應使用此頁面評估與影響AEM Assets解決方案的存放庫變更相關的工作量。 有些變更需要AEM 6.5升級程式中的工作量，而有些變更可能會延遲至日後升級。

**使用6.5升級**

* [雜項](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**未來升級前**

* [資產/收集事件電子郵件通知範本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [傳統資產共用設計](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [下載資產電子郵件通知範本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [範例DRM授權](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [連結共用電子郵件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign工作流程指令碼](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [視訊轉碼設定](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [雜項](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 使用6.5升級 {#with-upgrade}

### 雜項 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果任何自訂程式碼相依於此位置(即 程式碼需明確依賴此路徑)，則必須更新程式碼，才能在升級前使用新位置；最好使用Java API（若有）來減少對JCR中任何特定路徑的相依性。</p> <p>存放zip檔案以供用戶端下載的臨時位置。 由於用戶端要求下載資產，因此不需要更新。 它會在新位置產生檔案。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

## 未來升級前 {#prior-to-upgrade}

### 資產/收集事件電子郵件通知範本 {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果客戶修改了電子郵件模板，則執行以下操作以便與新的儲存庫結構保持一致：</p>
    <ol>
     <li>此 <code>/libs/settings/dam/notification</code> 電子郵件範本應從 <strong><code>/etc/notification/email/default</code></strong> to <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>因為目的地在<strong> <code>/apps</code></strong> 此變更應在SCM中持續存在。</li>
      </ol> </li>
     <li>移除資料夾： <strong><code>/etc/dam/notification/email/default</code></strong> 中的電子郵件模板被移動之後。<br />
      <ol>
       <li>若未更新<strong> <code>/etc/notification/email/default</code></strong>，資料夾可移除，因為原始電子郵件範本位於 <strong><code>/libs/settings/notification/email/default</code></strong> 作為AEM 4安裝的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 傳統資產共用設計 {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>對於在SCM中管理、而不是在運行時通過「設計對話框」寫入的任何設計，執行以下操作以與最新模型一致：</p>
    <ol>
     <li>將設計從上一個位置複製到 <code>/apps</code>.</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">用戶端程式庫</a> with <code>allowProxy = true</code>.</li>
     <li>更新上一個位置的參考，位於 <code>cq:designPath</code> 透過 <strong>AEM &gt; DAM管理員&gt;資產共用頁面&gt;頁面屬性&gt;進階標籤&gt;設計欄位</strong>.</li>
     <li>更新任何參考上一個位置的頁面以使用新的「用戶端程式庫」類別。 這需要更新頁面實作程式碼。</li>
     <li>更新Dispatcher規則，以允許透過 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>對於未在SCM中管理的設計，以及透過設計對話方塊修改的執行階段，請勿將可授權的設計移出 <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 下載資產電子郵件通知範本 {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果電子郵件模板(<strong>downloadassets</strong> 或 <strong>transitworkflowcompleted</strong>)，然後依照下列程式來對齊新結構：</p>
    <ol>
     <li>更新的電子郵件範本應從 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> to <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>因為目的地在<strong> <code>/apps</code></strong> 此變更應在SCM中持續存在。</li>
      </ol> </li>
     <li>移除資料夾： <code>/etc/dam/workflow/notification/email/downloadasset </code>中的電子郵件模板被移動之後。<br />
      <ol>
       <li>若未更新<strong> <code>/etc</code></strong>，資料夾可移除，因為原始電子郵件範本位於 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> 作為AEM 6.4安裝的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>同時 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> 技術支援查詢(透過一般的Sling CAConfig查閱優先於/apps，但在 <code>/etc</code>)可將範本放入 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. 但是，不建議這樣做，因為沒有運行時UI來加速電子郵件模板的編輯。</td>
  </tr>
 </tbody>
</table>

### 範例DRM授權 {#example-drm-licenses}

| **上一位置** | `/etc/dam/drm/licenses/` |
|---|---|
| **新位置** | `/libs/settings/dam/drm` |
| **重組指導** | N/A |
| **附註** | N/A |

### 連結共用電子郵件通知模板 {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>如果客戶修改了電子郵件模板，則要與新的儲存庫結構一致：</p>
    <ol>
     <li>更新的電子郵件範本應從 <strong><code>/etc/dam/adhocassetshare</code></strong> to <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>因為目的地在<strong> <code>/apps</code></strong> 此變更應在SCM中持續存在。</li>
      </ol> </li>
     <li>移除資料夾： <strong><code>/etc/dam/adhocassetshare</code></strong> 中的電子郵件模板被移動之後。<br />
      <ol>
       <li>若未更新<strong> <code>/etc</code></strong>，資料夾可移除，因為原始電子郵件範本位於 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> 作為AEM 6.4安裝的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>同時 <code>/conf/global/settings/dam/adhocassetshare</code> 在技術上支援查找(優先於 <code>/apps</code> ，但在 <code>/etc</code>)，則範本可放置於 <code>/conf/global/settings/dam/adhocassetshare</code>. 但是，不建議這樣做，因為沒有運行時UI來加速編輯電子郵件模板</td>
  </tr>
 </tbody>
</table>

### InDesign工作流程指令碼 {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>要與新的儲存庫結構一致：</p>
    <ol>
     <li>從 <strong><code>/etc/dam/indesign/scripts</code></strong> to <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>只有以AEM提供的未修改指令碼形式複製新指令碼或已修改指令碼，才能透過 <strong><code>/libs/settings</code></strong> 在AEM 6.5中</li>
      </ol> </li>
     <li>找出使用「媒體提取流程」WF步驟和
      <ol>
       <li>對於工作流程步驟的每個例項，更新設定中的路徑，以明確指向下方的適當指令碼<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> 或 <strong><code>/libs/settings/dam/indesign/scripts</code></strong> 視情況而定。</li>
      </ol> </li>
     <li>移除<strong> <code>/etc/dam/indesign/scripts</code></strong> 完全。</li>
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
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>專案層級自訂項目必須剪下並貼上至對等項目 <code>/apps</code> 或 <code>/conf</code> 路徑。</p> <p>若要與AEM 6.4存放庫結構一致：</p>
    <ol>
     <li>複製任何修改的視訊配置 <code>/etc/dam/video</code> to <code>/apps/settings/dam/video</code></li>
     <li>移除 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 檢視器預設集組態 {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>若為現成可用的檢視器預設集，則只能在新位置中使用。</p> <p>針對「自訂檢視器」預設集：</p>
    <ul>
     <li>您必須執行移轉指令碼，才能將節點從 <code>/etc</code> to <code>/conf</code>. 指令碼位於 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>或者，您可以編輯配置，並將其自動保存到新位置。</li>
    </ul> <p>請注意，您不必調整其copyURL/embed程式碼以指向 <code>/conf</code>. 的現有請求 <code>/etc</code> 會重新路由至 <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 雜項 {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>調整任何參照以指向下的新資源 <code>/libs</code> 使用 <code>/etc.clientlibs/</code> 允許代理前置詞。</p> <p>最後，將移轉的客戶端資料夾從 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>
