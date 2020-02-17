---
title: 疑難排解動態媒體- Scene7模式
description: 疑難排解Scene7執行模式中的動態媒體。
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 疑難排解動態媒體- Scene7模式{#troubleshooting-dynamic-media-scene-mode}

以下檔案說明執行dynamicmedia_scene7執行模 **式之Dynamic media的疑難排解** 。

## 設定與設定 {#setup-and-configuration}

請執行下列動作，以確保已正確設定動態媒體：

* 啟動命令包含runmode `-r dynamicmedia_scene7` 參數。
* 任何AEM 6.4累積修補程式套件(CFP)都已先安裝，再安裝 *任何* 「動態媒體功能套件」。
* 已安裝可選功能包18912。

   此選用功能套件可用於FTP支援，或是從Dynamic Media Classic(Scene7)將資產移轉至Dynamic Media。

* 導覽至雲端服務使用者介面，並確認已布建的帳戶會顯示在「可用 **[!UICONTROL 設定」下]**。
* 確保已啟 `Dynamic Media Asset Activation (scene7)` 用複製代理。

   此複製代理位於Author上的Agent下。

## 一般（所有資產） {#general-all-assets}

以下是所有資產的一些一般提示和秘訣。

### 資產同步狀態屬性 {#asset-synchronization-status-properties}

以下資產屬性可在CRXDE Lite中檢閱，以確認資產從AEM成功同步至動態媒體：

| **屬性** | **範例** | **說明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 節點已連結至動態媒體的常規指示符。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** 或錯誤文字 | 資產上傳至動態媒體的狀態。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必須填入，才能產生Dynamic media遠端資產的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **成功** 或 **失敗：`<error text>`** | 集（回轉集、影像集等）、影像預設集、檢視器預設集、資產的影像地圖更新，或已編輯的影像的同步狀態。 |

### 同步記錄 {#synchronization-logging}

同步錯誤和問題已記錄在 `error.log` 中(AEM伺服器目 `/crx-quickstart/logs/`錄)。 您可使用充份的記錄功能來判斷大多數問題的根本原因，不過您可以透過Sling Console( `com.adobe.cq.dam.ips` https://localhost:4502/system/console/slinglog[](https://localhost:4502/system/console/slinglog))，將記錄功能增加至套件上的DEBUG，以收集更多資訊。

### 移動、複製、刪除 {#move-copy-delete}

執行移動、複製或刪除操作之前，請執行以下操作：

* 對於影像和視訊，請在執行移 `<object_node>/jcr:content/metadata/dam:scene7ID` 動、複製或刪除操作之前先確認有值。
* 對於影像和檢視器預設集，請在執行移 `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` 動、複製或刪除作業之前先確認有值。
* 如果遺失上述中繼資料值，您必須在移動、複製或刪除作業之前重新上傳資產。

### 版本控制 {#version-control}

取代現有的動態媒體資產（相同名稱和位置）時，您可以選擇保留兩個資產或取代／建立版本：

* 保留兩者皆可建立具有已發佈資產URL唯一名稱的新資產。 例如，是 `image.jpg` 原始資產， `image1.jpg` 是新上傳的資產。

* 動態媒體- Scene7模式傳送不支援建立版本。 新版本將取代傳送中的現有資產。

## 影像和集合 {#images-and-sets}

如果您對影像和設定有任何問題，請參閱下列疑難排解指引。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何除錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法在資產詳細資料檢視中存取複製URL/內嵌按鈕</td>
   <td>
    <ol>
     <li><p>前往CRX/DE:</p>
      <ul>
       <li>檢查JCR中是否定義了預 <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> 設。 請注意，如果您從AEM 6.x升級至6.4，並選擇退出移轉，則此位置適用。 否則，地點就是 <code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>檢查以確定JCR中的資產在「中繼資料」 <code>dam:scene7FileStatus</code><strong> 下方 </strong>顯示為 <code>PublishComplete</code>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>重新整理頁面／導覽至另一頁並返回（需重新編譯側欄JSP）</p> <p>如果這不管用：</p>
    <ul>
     <li>發佈資產。</li>
     <li>重新上傳資產並發佈。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>集合編輯器中的資產選擇器卡在永久載入中</td>
   <td><p>6.4版中已知問題已修正</p> </td>
   <td><p>關閉選取器並重新開啟。</p> </td>
  </tr>
  <tr>
   <td><strong>選取</strong> (Select)按鈕在選取資產做為編輯集的一部分後，不會作用中</td>
   <td><p> </p> <p>6.4版中已知問題已修正</p> <p> </p> </td>
   <td><p>先按一下「資產選擇器」中的其他資料夾，然後返回以選取資產。</p> </td>
  </tr>
  <tr>
   <td>切換投影片後，轉盤熱點會四處移動</td>
   <td><p>檢查所有投影片的大小是否相同。</p> </td>
   <td><p>僅對轉盤使用相同大小的影像。</p> </td>
  </tr>
  <tr>
   <td>影像不會使用動態媒體檢視器預覽</td>
   <td><p>檢查資產是否包 <code>dam:scene7File</code> 含在中繼資料屬性(CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>已上傳的資產不會顯示在資產選擇器中</td>
   <td><p>Check Asset has property <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>卡片檢視上的橫幅 <strong>顯示</strong> 「新增」資產尚未開始處理</td>
   <td>檢查資 <code>jcr:content</code> 產&gt; <code>dam:assetState</code> =如果 <code>unprocessed</code> 工作流未拾取資產。</td>
   <td>等待工作流程擷取資產。</td>
  </tr>
  <tr>
   <td>影像或影像集不會顯示檢視器URL或內嵌代碼</td>
   <td>檢查檢視器預設集是否已發佈。</td>
   <td><p>前往「工 <strong>具</strong> &gt;資產 <strong>&gt;檢視</strong> 器預設集 <strong></strong> 」並發佈檢視器預設集。</p> </td>
  </tr>
 </tbody>
</table>

## Video {#video}

如果您對視訊有任何問題，請參閱下列疑難排解指引。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何除錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法預覽視訊</td>
   <td>
    <ul>
     <li>檢查資料夾是否已指派視訊描述檔（如果不支援檔案格式）。 如果不支援，則只會顯示影像。</li>
     <li>視訊設定檔必須包含多個編碼預設集，才能產生AVS集(單一編碼視為MP4檔案的視訊內容；對於不支援的檔案，會視為與未處理的檔案相同)。</li>
     <li>確認中繼資料中的內容，以檢查視訊是否 <code>dam:scene7FileAvs</code> 已完 <code>dam:scene7File</code> 成處理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊描述檔指派給資料夾。</li>
     <li>編輯視訊設定檔以包含多個編碼預設集。</li>
     <li>等待視訊完成處理。</li>
     <li>如果您重新載入視訊，請確定「動態媒體編碼視訊」工作流程未執行。<br /> </li>
     <li>重新上傳視訊。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊未編碼</td>
   <td>
    <ul>
     <li>檢查runmode是否為 <code>dynamicmedia_scene7</code>。</li>
     <li>檢查是否已設定Dynamic Media cloud服務。</li>
     <li>檢查視訊描述檔是否與上傳資料夾相關聯。</li>
    </ul> </td>
   <td>
    <ol>
     <li>使用 <code>-r dynamicmedia_scene7</code></li>
     <li>檢查「雲端服務」下的「動態媒體設定」是否已正確設定。</li>
     <li>檢查資料夾是否有視訊描述檔。 此外，檢查視訊設定檔。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊處理需要太長時間</td>
   <td><p>若要判斷視訊編碼是否仍在進行中，或已進入失敗狀態：</p>
    <ul>
     <li>檢查視訊狀態 <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>從工作流程控制台&gt;例項、封存、 <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> 失敗標籤監控視訊。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>影片轉譯遺失</td>
   <td><p>上傳視訊時，但沒有編碼轉譯：</p>
    <ul>
     <li>檢查資料夾是否已指派視訊描述檔。</li>
     <li>在中繼資料中確認，以檢查視訊是否已完成 <code>dam:scene7FileAvs</code> 處理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊描述檔指派給資料夾。</li>
     <li>等待視訊完成處理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 檢視器 {#viewers}

如果您對檢視器有任何問題，請參閱下列疑難排解指引。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何除錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>檢視器預設集未發佈</td>
   <td><p>繼續到示例管理器診斷頁： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>觀察計算值。 當正確運作時，您應看到：</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注意</strong>:在設定Dynamic Media cloud設定後，檢視器資產同步大約需要10分鐘。</p> <p>如果未啟動的資產仍保留，請按一下「列出所有 <strong>未啟動的資產</strong> 」按鈕以檢視詳細資訊。</p> </td>
   <td>
    <ol>
     <li>導覽至管理工具中的檢視器預設集清單： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>選取所有檢視器預設集，然後按一下「 <strong>發佈」</strong>。</li>
     <li>返回範例管理員，並觀察未啟動的資產計數現在為零。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>檢視器預設集圖稿會從資產詳細資料的預覽或複製URL/內嵌代碼傳回404</td>
   <td><p>在CRXDE Lite中，請執行下列動作：</p>
    <ol>
     <li>導覽至 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> 動態媒體同步資料夾中的資料夾(例如 <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>尋找有問題資產的中繼資料節點(例如 <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>)。</li>
     <li>檢查是否存在屬 <code>dam:scene7*</code> 性。 如果資產已成功同步並發佈，您會看到 <code>dam:scene7FileStatus</code> 設定為 <strong>PublishComplete</strong>。</li>
     <li>嘗試串連下列屬性和字串文字的值，直接從Dynamic media要求圖稿
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>範例: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>如果範例資產或檢視器預設圖稿尚未同步或發佈，請重新啟動整個複製／同步程式：</p>
    <ol>
     <li>導覽至CRXDE Lite。
      <ul>
       <li>刪除 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>導覽至CRX套件管理器： <code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>在清單中搜尋檢視器套件(開頭為 <code>cq-dam-scene7-viewers-content</code>)</li>
       <li>按一下「 <strong>重新安裝</strong>」。</li>
      </ol> </li>
     <li>在「雲端服務」下，導覽至「動態媒體設定」頁面，然後開啟您的「動態媒體- S7」設定的設定對話方塊。
      <ul>
       <li>不進行任何變更，請按一下「 <strong>儲存</strong>」。 這會再次觸發邏輯，以建立並同步範例資產、檢視器預設CSS和圖稿。<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

