---
title: 診斷Dynamic Media-Scene7模式
description: 在Dynamic Media以Scene7模式運行時排除故障。
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
role: User, Admin
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: Troubleshooting
mini-toc-levels: 3
source-git-commit: 9c3df2491f99fe31e4b64b47442dd583af06974e
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 1%

---

# 診斷Dynamic Media-Scene7模式{#troubleshooting-dynamic-media-scene-mode}

以下文檔介紹Dynamic Media運行的故障排除 **動態媒體_場景7** 運行模式。

## 設定和配置 {#setup-and-configuration}

通過執行以下操作，確保已正確設定Dynamic Media:

* 啟動命令包含 `-r dynamicmedia_scene7` 運行模式參數。
* 已先安裝任何Adobe Experience Manager6.4累積修復包(CFP) *先* 任何可用的Dynamic Media功能包。
* 已安裝可選功能包18912。

   此可選功能包用於FTP支援，或者您要將資產從Dynamic Media Classic遷移到Dynamic Media。

* 導航到Cloud Services用戶介面並確認已設定帳戶顯示在 **[!UICONTROL 可用配置]**。
* 確保 `Dynamic Media Asset Activation (scene7)` 已啟用複製代理。

   此複製代理位於「Agent on Author（作者上的代理）」下。

## 常規（所有資產） {#general-all-assets}

以下是所有資產的一些一般提示和技巧。

### 資產同步狀態屬性 {#asset-synchronization-status-properties}

可以在CRXDE Lite中查看以下資產屬性，以確認資產從Experience Manager到Dynamic Media的成功同步：

| **屬性** | **範例** | **說明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | 節點連結到Dynamic Media的一般指示。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **發佈完成** 錯誤文本 | 資產上載到Dynamic Media的狀態。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必須填充以生成Dynamic Media遠程資產的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **成功** 或 **失敗：`<error text>`** | 集（旋轉集、影像集等）、影像預設、查看器預設、資產的影像映射更新或已編輯的影像的同步狀態。 |

### 同步記錄 {#synchronization-logging}

同步錯誤和問題已登錄 `error.log` (Experience Manager伺服器目錄) `/crx-quickstart/logs/`)。 可以使用足夠的日誌記錄來確定大多數問題的根本原因，但您可以將日誌記錄增加到 `com.adobe.cq.dam.ips` 通過Sling控制台進行打包([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))以收集更多資訊。

### 移動、複製、刪除 {#move-copy-delete}

在執行「移動」(Move)、「複製」(Copy)或「刪除」(Delete)操作之前，請執行以下操作：

* 對於影像和視頻，確認 `<object_node>/jcr:content/metadata/dam:scene7ID` 在執行移動、複製或刪除操作之前存在值。
* 對於影像和查看器預設，確認 `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` 在執行移動、複製或刪除操作之前存在值。
* 如果缺少上面的元資料值，則必須在移動、複製或刪除操作之前重新上載資產。

### 版本控制 {#version-control}

替換現有Dynamic Media資產（同名和地點）時，您可以保留兩個資產或替換/建立版本：

* 保留兩者都會為已發佈資產URL建立具有唯一名稱的資產。 比如說， `image.jpg` 是原始資產 `image1.jpg` 是新上載的資產。

* 在Dynamic Media-Scene7模式傳遞中不支援建立版本。 新版本將替換交付中的現有資產。

## 影像和集 {#images-and-sets}

如果您對映像和集有問題，請參閱以下故障排除指導。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何調試</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法訪問資產詳細資訊視圖中的複製URL/嵌入按鈕</td>
   <td>
    <ol>
     <li><p>轉至CRX/DE:</p>
      <ul>
       <li>檢查JCR中是否有預設 <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> 定義。 如果您從Experience Manager6.x升級到6.4並選擇退出遷移，則此位置適用。 否則，位置 <code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>檢查以確保JCR中的資產 <code>dam:scene7FileStatus</code><strong> </strong>在元資料下顯示為 <code>PublishComplete</code>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>刷新頁面/導航到另一頁並返回（必須重新編譯側軌JSP）</p> <p>如果這行不通：</p>
    <ul>
     <li>發佈資產。</li>
     <li>重新上載資產並發佈。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>設定編輯器中的資產選擇器卡在永久載入中</td>
   <td><p>6.4中要解決的已知問題</p> </td>
   <td><p>關閉選擇器並重新開啟它。</p> </td>
  </tr>
  <tr>
   <td><strong>選擇</strong> 選擇作為編輯集一部分的資產後，按鈕不處於活動狀態</td>
   <td><p> </p> <p>6.4中要解決的已知問題</p> <p> </p> </td>
   <td><p>首先在「資產選擇器」中的另一個資料夾上選擇，然後返回以選擇資產。</p> </td>
  </tr>
  <tr>
   <td>在幻燈片之間切換後，旋轉木馬熱點會移動</td>
   <td><p>檢查所有幻燈片的大小是否相同。</p> </td>
   <td><p>僅對旋轉木馬使用大小相同的影像。</p> </td>
  </tr>
  <tr>
   <td>影像不與Dynamic Media查看器預覽</td>
   <td><p>檢查資產是否包含 <code>dam:scene7File</code> 元資料屬性(CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>上載的資產不顯示在資產選擇器中</td>
   <td><p>檢查資產具有屬性 <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>卡上的橫幅顯示 <strong>新建</strong> 當資產未開始處理時</td>
   <td>檢查資產 <code>jcr:content</code> &gt; <code>dam:assetState</code> =if <code>unprocessed</code> 工作流沒有採集。</td>
   <td>等待工作流提取資產。</td>
  </tr>
  <tr>
   <td>影像或集不顯示查看器URL或嵌入代碼</td>
   <td>檢查查看器預設是否已發佈。</td>
   <td><p>轉到 <strong>工具</strong> &gt; <strong>資產</strong> &gt; <strong>查看器預設</strong> 並發佈查看器預設。</p> </td>
  </tr>
 </tbody>
</table>

## 影片 {#video}

如果您對視頻有問題，請參閱以下故障排除指導。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何調試</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法預覽視頻</td>
   <td>
    <ul>
     <li>檢查資料夾是否已為其分配視頻配置檔案（如果不支援檔案格式）。 如果不支援，則只顯示影像。</li>
     <li>視頻配置檔案必須包含多個編碼預設以生成AVS集(單個編碼被視為MP4檔案的視頻內容；對於不支援的檔案，與未處理檔案相同)。</li>
     <li>通過確認 <code>dam:scene7FileAvs</code> 共 <code>dam:scene7File</code> 元資料。</li>
    </ul> </td>
   <td>
    <ol>
     <li>為資料夾分配視頻配置檔案。</li>
     <li>編輯視頻配置檔案以包括多個編碼預設。</li>
     <li>等待視頻完成處理。</li>
     <li>重新載入視頻，確保Dynamic Media編碼視頻工作流未運行。<br /> </li>
     <li>重新上載視頻。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視頻未編碼</td>
   <td>
    <ul>
     <li>檢查運行模式是否為 <code>dynamicmedia_scene7</code>。</li>
     <li>檢查是否配置了Dynamic Media雲服務。</li>
     <li>檢查視頻配置檔案是否與上載資料夾關聯。</li>
    </ul> </td>
   <td>
    <ol>
     <li>檢查您的Experience Manager實例 <code>-r dynamicmedia_scene7</code></li>
     <li>檢查Cloud Services下的Dynamic Media配置是否已正確設定。</li>
     <li>檢查資料夾是否具有視頻配置檔案。 另外，檢查視頻配置檔案。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視頻處理耗時太長</td>
   <td><p>要確定視頻編碼是否仍在進行中或是否已進入失敗狀態：</p>
    <ul>
     <li>檢查視頻狀態 <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>從工作流控制台監視視頻 <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt;實例、存檔、失敗頁籤。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>缺少視頻格式副本</td>
   <td><p>上載視頻時，但沒有編碼格式副本：</p>
    <ul>
     <li>檢查資料夾是否已分配視頻配置檔案。</li>
     <li>通過確認 <code>dam:scene7FileAvs</code> 元資料。</li>
    </ul> </td>
   <td>
    <ol>
     <li>為資料夾分配視頻配置檔案。</li>
     <li>等待視頻完成處理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 檢視器 {#viewers}

如果與查看者有問題，請參閱以下故障排除指南。

### 問題：未發佈查看器預設 {#viewers-not-published}

**如何調試**

1. 繼續到示例管理器診斷頁： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`。
1. 觀察計算值。 正確操作時，將看到以下內容： `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`。

   >[!NOTE]
   >
   >配置查看器資產的Dynamic Media雲設定後，可能需要大約10分鐘才能同步。

1. 如果未激活的資產仍然存在，請選擇 **列出所有未激活的資產** 按鈕以查看詳細資訊。

**解決方案**

1. 導航到管理工具中的查看器預設清單： `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. 選擇所有查看器預設，然後選擇 **發佈**。
1. 返回至示例經理，並觀察未激活的資產計數現在為零。

### 問題：查看器預設圖稿從資產詳細資訊中的預覽或複製URL/嵌入代碼返回404 {#viewer-preset-404}

**如何調試**

在CRXDE Lite中，執行以下操作：

1. 導航到 `<sync-folder>/_CSS/_OOTB` 資料夾(例如， `/content/dam/_CSS/_OOTB`)。
1. 查找有問題資產的元資料節點(例如， `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`)。
1. 檢查是否存在 `dam:scene7*` 屬性。 如果資產已成功同步並發佈，您將看到 `dam:scene7FileStatus` 設定為 **發佈完成**。
1. 嘗試通過連接以下屬性和字串文本的值直接從動態媒體請求圖稿：

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
範例: 
`https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**解決方案**

如果示例資產或查看器預設圖稿尚未同步或發佈，請重新啟動整個複製/同步過程：

1. 導航到CRXDE Lite。
1. 刪除 `<sync-folder>/_CSS/_OOTB`.
1. 導航到CRX包管理器： `https://localhost:4502/crx/packmgr/`。
1. 在清單中搜索查看器包；開始 `cq-dam-scene7-viewers-content`。
1. 選擇 **重新安裝**。
1. 在Cloud Services下，導航到「Dynamic Media配置」頁，然後開啟Dynamic Media- S7配置的配置對話框。
1. 不更改，選擇 **保存**。
此保存操作將再次觸發邏輯，以建立和同步示例資源、查看器預設的CSS和圖稿。

### 問題：影像預覽未載入到Viewer預設創作中 {#image-preview-not-loading}

**解決方案**

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台，然後導航至 **[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。
1. 在左滑軌中，導航到以下位置的示例內容資料夾：

   `/content/dam/_DMSAMPLE`

1. 刪除 `_DMSAMPLE` 的子菜單。
1. 在左滑軌中，導航到以下位置的預設資料夾：

   `/conf/global/settings/dam/dm/presets/viewer`

1. 刪除 `viewer` 的子菜單。
1. 在CRXDE Lite頁的左上角附近，選擇 **[!UICONTROL 全部保存]**。
1. 在CRXDE Lite頁的左上角，選擇 **返回首頁** 表徵圖
1. 重新建立 [Dynamic MediaCloud Services配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)。
