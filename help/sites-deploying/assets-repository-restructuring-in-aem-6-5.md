---
title: 6.5中的資AEM產庫重組
seo-title: Assets Repository Restructuring in AEM 6.5
description: 瞭解如何進行必要的更改，以便遷移到6.5版中的AEMAssets新儲存庫結構。
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

# 6.5中的資AEM產庫重組 {#assets-repository-restructuring-in-aem}

如父代中所述 [6.5中的AEM儲存庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級到AEM6.5的客戶應使用此頁面評估與影響AEM Assets解決方案的儲存庫更改相關的工作量。 某些更改需要在6.5升AEM級過程中進行工作，而其他更改則可以推遲到以後升級。

**使用6.5升級**

* [雜項](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**未來升級前**

* [資產/收集事件電子郵件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [經典資產份額設計](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [下載資產電子郵件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [DRM許可證示例](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [連結共用電子郵件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign工作流指令碼](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [視頻轉碼配置](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [雜項](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 使用6.5升級 {#with-upgrade}

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
   <td><strong>重組指導</strong></td>
   <td><p>如果任何自定義代碼依賴於此位置(即 代碼顯式依賴於此路徑)，則必須更新該代碼以在升級前使用新位置；理想情況下，Java API可用於減少JCR中任何特定路徑的依賴項。</p> <p>保存ZIP檔案以供客戶端下載的臨時位置。 自客戶端請求下載資產後，無需更新。 它將在新位置生成檔案。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

## 未來升級前 {#prior-to-upgrade}

### 資產/收集事件電子郵件通知模板 {#asset-collection-event-e-mail-notification-template}

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
   <td><p>如果客戶修改了電子郵件模板，則執行以下操作以與新儲存庫結構對齊：</p>
    <ol>
     <li>的 <code>/libs/settings/dam/notification</code> 電子郵件模板應從 <strong><code>/etc/notification/email/default</code></strong> 至 <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>因為目標在<strong> <code>/apps</code></strong> 此更改應在SCM中持續。</li>
      </ol> </li>
     <li>刪除資料夾： <strong><code>/etc/dam/notification/email/default</code></strong> 郵件模板被移動之後。<br />
      <ol>
       <li>如果未對下面的電子郵件模板進行更新<strong> <code>/etc/notification/email/default</code></strong>，由於原始電子郵件模板位於 <strong><code>/libs/settings/notification/email/default</code></strong> 作為4安裝AEM的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 經典資產份額設計 {#classic-asset-share-designs}

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
   <td><p>對於在SCM中管理且未通過「設計對話框」在運行時寫入的任何設計，請執行以下操作以與最新型號對齊：</p>
    <ol>
     <li>將設計從「上一個位置」(Previous Location)複製到「新位置」(New Location)下 <code>/apps</code>。</li>
     <li>將設計中的任何CSS、JavaScript和靜態資源轉換為 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客戶端庫</a> 與 <code>allowProxy = true</code>。</li>
     <li>更新對中上一個位置的引用 <code>cq:designPath</code> 屬性 <strong>&gt;AEM DAM管理&gt;資產共用頁&gt;頁屬性&gt;高級頁籤&gt;設計欄位</strong>。</li>
     <li>更新引用上一個位置的任何頁面以使用新的客戶端庫類別。 這需要更新頁面實現代碼。</li>
     <li>更新Dispatcher規則以允許通過 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>對於任何未在SCM中管理的設計，以及通過設計對話框修改的運行時，請勿將可授權的設計移出 <code>/etc</code>。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 下載資產電子郵件通知模板 {#download-asset-e-mail-notification-template}

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
   <td><p>如果電子郵件模板(<strong>下載資產</strong> 或 <strong>過渡工程已完成</strong>)已修改，然後按照以下步驟對齊新結構：</p>
    <ol>
     <li>更新的電子郵件模板應從 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> 至 <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>因為目標在<strong> <code>/apps</code></strong> 此更改應在SCM中持續。</li>
      </ol> </li>
     <li>刪除資料夾： <code>/etc/dam/workflow/notification/email/downloadasset </code>郵件模板被移動之後。<br />
      <ol>
       <li>如果未對下面的電子郵件模板進行更新<strong> <code>/etc</code></strong>，由於原始電子郵件模板位於 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> 作為6.AEM4安裝的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>同時 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> 在技術上支援查找(優先於/app，通過常規Sling CAConfig查找，但在 <code>/etc</code>)模板可以放入 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>。 但是，不建議這樣做，因為沒有運行時UI可方便編輯電子郵件模板。</td>
  </tr>
 </tbody>
</table>

### DRM許可證示例 {#example-drm-licenses}

| **上一個位置** | `/etc/dam/drm/licenses/` |
|---|---|
| **新位置** | `/libs/settings/dam/drm` |
| **重組指導** | N/A |
| **附註** | N/A |

### 連結共用電子郵件通知模板 {#link-share-e-mail-notification-template}

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
   <td><p>如果客戶修改了電子郵件模板，則要與新儲存庫結構對齊：</p>
    <ol>
     <li>更新的電子郵件模板應從 <strong><code>/etc/dam/adhocassetshare</code></strong> 至 <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>因為目標在<strong> <code>/apps</code></strong> 此更改應在SCM中持續。</li>
      </ol> </li>
     <li>刪除資料夾： <strong><code>/etc/dam/adhocassetshare</code></strong> 郵件模板被移動之後。<br />
      <ol>
       <li>如果未對下面的電子郵件模板進行更新<strong> <code>/etc</code></strong>，由於原始電子郵件模板位於 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> 作為6.AEM4安裝的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>同時 <code>/conf/global/settings/dam/adhocassetshare</code> 在技術上支援查找(優先於 <code>/apps</code> 通常使用Sling CAConfig查找，但在 <code>/etc</code>)，模板可以放入 <code>/conf/global/settings/dam/adhocassetshare</code>。 但是，不建議這樣做，因為沒有運行時UI可方便編輯電子郵件模板</td>
  </tr>
 </tbody>
</table>

### InDesign工作流指令碼 {#indesign-workflow-scripts}

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
     <li>從複製所有自定義或修改的指令碼 <strong><code>/etc/dam/indesign/scripts</code></strong> 至 <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>只有將新指令碼或修改的指令碼複製為由提供的未修AEM改指令碼才可通過 <strong><code>/libs/settings</code></strong> 在AEM6.5中</li>
      </ol> </li>
     <li>查找使用「介質提取流程」WF步驟和
      <ol>
       <li>對於「工作流步驟」的每個實例，更新配置中的路徑，以明確指向下的正確指令碼<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> 或 <strong><code>/libs/settings/dam/indesign/scripts</code></strong> 視情況而定。</li>
      </ol> </li>
     <li>刪除<strong> <code>/etc/dam/indesign/scripts</code></strong> 完全。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>建議將自定義指令碼儲存在 <code>/apps</code>，因為這是應儲存代碼的位置。</td>
  </tr>
 </tbody>
</table>

### 視頻轉碼配置 {#video-transcoding-configurations}

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
   <td><p>項目級別自定義項需要剪切並貼上到對等項下 <code>/apps</code> 或 <code>/conf</code> 路徑（如果適用）。</p> <p>要與6.4儲存AEM庫結構對齊：</p>
    <ol>
     <li>從中複製任何修改的視頻配置 <code>/etc/dam/video</code> 至 <code>/apps/settings/dam/video</code></li>
     <li>移除 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 查看器預設配置 {#viewer-preset-configurations}

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
   <td><p>對於現成的「查看器預設」，它將僅在新位置中可用。</p> <p>對於「自定義查看器」預設：</p>
    <ul>
     <li>您必須運行遷移指令碼才能從 <code>/etc</code> 至 <code>/conf</code>。 指令碼位於 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>或者，您可以編輯配置，並將其自動保存到新位置。</li>
    </ul> <p>請注意，您不必調整其copyURL/embed代碼以指向 <code>/conf</code>。 現有請求 <code>/etc</code> 將被重新路由到 <code>/conf</code>。</p> </td>
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
   <td><strong>上一個位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>調整所有參照以指向下的新資源 <code>/libs</code> 使用 <code>/etc.clientlibs/</code> 允許代理前置詞。</p> <p>最後，通過從中刪除遷移的客戶端的資料夾來清除 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>
