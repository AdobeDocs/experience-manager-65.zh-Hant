---
title: 6.5中的資產AEM儲存庫重組
seo-title: 6.5中的資產AEM儲存庫重組
description: 瞭解如何進行必要的更改，以便遷移到6.5中的AEM Assets新儲存庫結構。
seo-description: 瞭解如何進行必要的更改，以便遷移到6.5中的AEM Assets新儲存庫結構。
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
feature: 升級
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 2%

---


# 6.5 &lt;AEMa0/>中的資產資料庫重組{#assets-repository-restructuring-in-aem}

如[父6.5](/help/sites-deploying/repository-restructuring.md)頁中的「資料庫重組」頁中所述，升級至AEM6.5的客戶應使用此頁評估與影響AEM Assets解決方案的資料庫更改相關的工作成果。 有些變更需要在6.5升級程AEM序中努力工作，而有些則會延遲至日後升級。

**使用6.5升級**

* [其他](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**未來升級前**

* [資產／收集事件電子郵件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [傳統資產共用設計](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [下載資產電子郵件通知範本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [DRM授權範例](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [連結共用電子郵件通知範本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign工作流指令碼](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [視訊轉碼設定](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [其他](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 使用6.5升級{#with-upgrade}

### Misc {#misc}

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
   <td><strong>重組指導</strong></td>
   <td><p>如果任何自訂代碼都與此位置相關(即 程式碼明確依賴此路徑)，則程式碼必須更新，才能在升級前使用新位置；最理想的情況是，當Java API可用來減少對JCR中任何特定路徑的依賴性時。</p> <p>暫存位置，以儲存ZIP檔供用戶端下載。 由於用戶端要求下載資產，因此不需要更新。 它將在新位置生成檔案。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

## 未來升級前{#prior-to-upgrade}

### 資產／收集事件電子郵件通知模板{#asset-collection-event-e-mail-notification-template}

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
   <td><strong>重組指導</strong></td>
   <td><p>如果客戶修改了電子郵件模板，請執行以下操作以便與新儲存庫結構保持一致：</p>
    <ol>
     <li><code>/libs/settings/dam/notification</code>電子郵件範本應從<strong><code>/etc/notification/email/default</code></strong>複製至<strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>由於目標位於<strong> <code>/apps</code></strong>中，因此應將此更改保存在SCM中。</li>
      </ol> </li>
     <li>刪除資料夾：<strong><code>/etc/dam/notification/email/default</code></strong>。<br />
      <ol>
       <li>如果<strong> <code>/etc/notification/email/default</code></strong>下未對電子郵件模板進行更新，則可以刪除該資料夾，因為在安裝4時，<strong><code>/libs/settings/notification/email/default</code></strong>下存在原始電子郵件模板AEM。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 傳統資產共用設計{#classic-asset-share-designs}

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
   <td><strong>重組指導</strong></td>
   <td><p>對於任何在SCM中管理且未在執行時期透過設計對話方塊寫入的設計，請執行下列動作以與最新型號對齊：</p>
    <ol>
     <li>將設計從「上一個位置」複製到<code>/apps</code>下的「新位置」。</li>
     <li>將「設計」中的任何CSS、JavaScript和靜態資源轉換為<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">具有<code>allowProxy = true</code>的「用戶端程式庫」。</a></li>
     <li>透過<strong> &gt; DAM管理員&gt;資產共用頁面&gt;頁面屬性&gt;進階標籤&gt;設計欄位</strong>，更新<code>cq:designPath</code>屬性中「上一個位置」的參考。</li>
     <li>更新參照上一個位置的任何頁面，以使用新的「用戶端程式庫」類別。 這需要更新頁面實施程式碼。</li>
     <li>更新Dispatcher規則，允許通過<code>/etc.clientlibs/</code>代理Servlet提供客戶端庫。</li>
    </ol> <p>對於未在SCM中管理且透過設計對話方塊修改執行時期的任何設計，請勿將可授權的設計移出<code>/etc</code>。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 下載資產電子郵件通知範本{#download-asset-e-mail-notification-template}

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
   <td><strong>重組指導</strong></td>
   <td><p>如果電子郵件範本（<strong>downloadasset</strong>或<strong>transentworkflowcompleted</strong>）已修改，請遵循下列步驟以符合新結構：</p>
    <ol>
     <li>更新的電子郵件範本應從<strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong>複製至<strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>由於目標位於<strong> <code>/apps</code></strong>中，因此應將此更改保存在SCM中。</li>
      </ol> </li>
     <li>刪除資料夾：<code>/etc/dam/workflow/notification/email/downloadasset </code>移動電子郵件範本後。<br />
      <ol>
       <li>如果<strong> <code>/etc</code></strong>下未對電子郵件模板進行更新，則可以刪除該資料夾，因為在安裝6.4時，<strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong>下存在原始電子郵件模板AEM。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>雖然在技術上支援<code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>尋找（優先於/apps之前，透過一般的Sling CAConfig查閱，但是在<code>/etc</code>之後），範本可以放在<code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>中。 不過，不建議這麼做，因為沒有執行時期UI可協助編輯電子郵件範本。</td>
  </tr>
 </tbody>
</table>

### DRM授權範例{#example-drm-licenses}

| **上一個位置** | `/etc/dam/drm/licenses/` |
|---|---|
| **新位置** | `/libs/settings/dam/drm` |
| **重組指導** | 不適用 |
| **附註** | 不適用 |

### 連結共用電子郵件通知模板{#link-share-e-mail-notification-template}

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
   <td><strong>重組指導</strong></td>
   <td><p>如果客戶修改了電子郵件模板，則要與新儲存庫結構一致：</p>
    <ol>
     <li>更新的電子郵件範本應從<strong><code>/etc/dam/adhocassetshare</code></strong>複製至<strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>由於目標位於<strong> <code>/apps</code></strong>中，因此應將此更改保存在SCM中。</li>
      </ol> </li>
     <li>刪除資料夾：<strong><code>/etc/dam/adhocassetshare</code></strong>。<br />
      <ol>
       <li>如果<strong> <code>/etc</code></strong>下未對電子郵件模板進行更新，則可以刪除該資料夾，因為在安裝6.4時，<strong><code>/libs/settings/dam/adhocassetshare</code></strong>下存在原始電子郵件模板AEM。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>雖然在技術上支援<code>/conf/global/settings/dam/adhocassetshare</code>尋找（透過一般的Sling CAConfig查閱優先於<code>/apps</code>之前，但在<code>/etc</code>之後），範本可以放在<code>/conf/global/settings/dam/adhocassetshare</code>中。 不過，不建議這麼做，因為沒有執行階段UI可協助編輯電子郵件範本</td>
  </tr>
 </tbody>
</table>

### InDesign工作流指令碼{#indesign-workflow-scripts}

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
   <td><strong>重組指導</strong></td>
   <td><p>要與新儲存庫結構對齊：</p>
    <ol>
     <li>將所有自定義或修改的指令碼從<strong><code>/etc/dam/indesign/scripts</code></strong>複製到<strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>只有將新的或修改的指令碼複製為由提供的未AEM修改的指令碼，才能通過AEM6.5中的<strong><code>/libs/settings</code></strong>使用</li>
      </ol> </li>
     <li>找到所有使用媒體抽取流程WF步驟的工作流模型，並
      <ol>
       <li>對於工作流步驟的每個實例，請根據需要更新配置中的路徑，以明確指向<strong> <code>/apps/settings/dam/indesign/scripts</code></strong>或<strong><code>/libs/settings/dam/indesign/scripts</code></strong>下的相應指令碼。</li>
      </ol> </li>
     <li>完全刪除<strong> <code>/etc/dam/indesign/scripts</code></strong>。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>建議將自訂指令碼儲存在<code>/apps</code>下，因為這是應儲存程式碼的位置。</td>
  </tr>
 </tbody>
</table>

### 視頻轉碼配置{#video-transcoding-configurations}

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
   <td><strong>重組指導</strong></td>
   <td><p>專案層級自訂必須視需要剪下並貼在等效的<code>/apps</code>或<code>/conf</code>路徑下。</p> <p>要與6.AEM4儲存庫結構一致：</p>
    <ol>
     <li>將任何修改的視頻配置從<code>/etc/dam/video</code>複製到 <code>/apps/settings/dam/video</code></li>
     <li>移除 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### 檢視器預設集組態{#viewer-preset-configurations}

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
   <td><strong>重組指導</strong></td>
   <td><p>對於現成可用的檢視器預設集，它只能在新位置使用。</p> <p>對於自訂檢視器預設集：</p>
    <ul>
     <li>您必須運行遷移指令碼才能將節點從<code>/etc</code>移動到<code>/conf</code>。 該指令碼位於<em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>或者，您可以編輯配置，並將其自動保存到新位置。</li>
    </ul> <p>請注意，您不必調整其copyURL/embed程式碼，即可指向<code>/conf</code>。 對<code>/etc</code>的現有請求將從<code>/conf</code>重新路由至正確的內容。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### Misc {#misc2}

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
   <td><strong>重組指導</strong></td>
   <td><p>使用<code>/etc.clientlibs/</code>允許代理前置詞調整指向<code>/libs</code>下的新資源的任何引用。</p> <p>最後，將已遷移客戶端的資料夾從 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

