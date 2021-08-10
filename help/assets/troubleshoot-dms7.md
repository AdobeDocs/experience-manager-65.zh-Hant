---
title: 疑難排解Dynamic Media - Scene7模式
description: 疑難排解Dynamic Media以Scene7模式執行時。
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
role: User, Admin
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: 疑難排解
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 1%

---

# 疑難排解Dynamic Media - Scene7模式{#troubleshooting-dynamic-media-scene-mode}

以下檔案說明Dynamic Media執行&#x200B;**dynamicmedia_scene7**&#x200B;執行模式的疑難排解。

## 設定與設定 {#setup-and-configuration}

請執行下列動作，確認Dynamic Media已正確設定：

* 啟動命令包含`-r dynamicmedia_scene7`運行模式參數。
* 任何Adobe Experience Manager 6.4 Cumulative Fix Pack(CFP)，都已先於&#x200B;*再安裝於*&#x200B;任何可用的Dynamic Media Feature Pack。
* 已安裝選用的Feature Pack 18912。

   此選用功能套件適用於FTP支援，或從Dynamic Media Classic將資產移轉至Dynamic Media。

* 導覽至「Cloud Services」使用者介面，並確認布建的帳戶顯示在&#x200B;**[!UICONTROL 可用配置]**&#x200B;下。
* 確保已啟用`Dynamic Media Asset Activation (scene7)`復寫代理。

   此復寫代理位於「作者上的代理」下。

## 一般（所有資產） {#general-all-assets}

以下是所有資產的一些一般提示和秘訣。

### 資產同步狀態屬性 {#asset-synchronization-status-properties}

您可以在CRXDE Lite中檢閱下列資產屬性，以確認資產是否從Experience Manager同步至Dynamic Media:

| **屬性** | **範例** | **說明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 節點連結至Dynamic Media的一般指標。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **** PublishCompleteor錯誤文字 | 資產上傳至Dynamic Media的狀態。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必須填入，才能產生URL至Dynamic Media的遠端資產。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **** 後繼 **失敗：`<error text>`** | 集（回轉集、影像集等）、影像預設集、檢視器預設集、資產的影像地圖更新或已編輯影像的同步狀態。 |

### 同步記錄 {#synchronization-logging}

同步錯誤和問題記錄在`error.log`(Experience Manager伺服器目錄`/crx-quickstart/logs/`)中。 有足夠的記錄可供判斷大部分問題的根本原因，但您可以透過Sling主控台([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))增加`com.adobe.cq.dam.ips`套件上的DEBUG記錄，以收集詳細資訊。

### 移動、複製、刪除 {#move-copy-delete}

執行「移動」、「複製」或「刪除」操作之前，請執行以下操作：

* 對於影像和視訊，在執行移動、複製或刪除操作之前，請確認`<object_node>/jcr:content/metadata/dam:scene7ID`值存在。
* 對於影像和檢視器預設集，在執行移動、複製或刪除操作之前，請確認`https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata`值存在。
* 如果缺少上述中繼資料值，您必須在移動、複製或刪除作業前重新上傳資產。

### 版本控制 {#version-control}

取代現有的Dynamic Media資產（相同名稱和位置）時，您可以保留兩個資產或取代/建立版本：

* 同時保留會為已發佈的資產URL建立一個唯一名稱的資產。 例如， `image.jpg`是原始資產，而`image1.jpg`是新上傳的資產。

* Dynamic Media - Scene7模式傳送不支援建立版本。 新版本會取代傳送中的現有資產。

## 影像和集 {#images-and-sets}

如果您對影像和集有問題，請參閱下列疑難排解指南。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何偵錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法存取資產詳細資料檢視中的複製URL/內嵌按鈕</td>
   <td>
    <ol>
     <li><p>前往CRX/DE:</p>
      <ul>
       <li>檢查JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code>中是否已定義預設集。 如果您從Experience Manager6.x升級至6.4，並選擇退出移轉，則此位置適用。 否則，位置為<code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>檢查以確定JCR中的資產在「中繼資料顯示為<code>PublishComplete</code>」下有<code>dam:scene7FileStatus</code><strong> </strong>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>重新整理頁面/導覽至其他頁面並返回（必須重新編譯側欄JSP）</p> <p>如果沒有用：</p>
    <ul>
     <li>發佈資產。</li>
     <li>重新上傳資產並發佈。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>集合編輯器中的資產選擇器停滯於永久載入中</td>
   <td><p>6.4中需修正的已知問題</p> </td>
   <td><p>關閉選取器並將其重新開啟。</p> </td>
  </tr>
  <tr>
   <td><strong></strong> 在編輯資產集時選取資產後，「選取」按鈕沒有作用中</td>
   <td><p> </p> <p>6.4中需修正的已知問題</p> <p> </p> </td>
   <td><p>先在「資產選擇器」的其他資料夾中選取，然後返回選取資產。</p> </td>
  </tr>
  <tr>
   <td>切換投影片後，輪播熱點會四處移動</td>
   <td><p>檢查所有幻燈片的大小是否相同。</p> </td>
   <td><p>僅對輪播使用大小相同的影像。</p> </td>
  </tr>
  <tr>
   <td>影像未以Dynamic Media檢視器預覽</td>
   <td><p>檢查中繼資料屬性(CRXDE Lite)中的資產是否包含<code>dam:scene7File</code></p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>上傳的資產不會顯示在資產選取器中</td>
   <td><p>檢查資產的屬性<code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code>(CRXDE Lite)</p> </td>
   <td><p>檢查所有資產是否已完成處理。</p> </td>
  </tr>
  <tr>
   <td>當資產尚未開始處理時，卡片檢視上的橫幅會顯示<strong>新增</strong></td>
   <td>檢查工作流程未擷取的資產<code>jcr:content</code> &gt; <code>dam:assetState</code> = <code>unprocessed</code>。</td>
   <td>等待工作流程擷取資產。</td>
  </tr>
  <tr>
   <td>影像或集不會顯示檢視器URL或內嵌程式碼</td>
   <td>檢查檢視器預設集是否已發佈。</td>
   <td><p>前往「<strong>工具</strong> &gt; <strong>資產</strong> &gt; <strong>檢視器預設集</strong>」並發佈檢視器預設集。</p> </td>
  </tr>
 </tbody>
</table>

## 影片 {#video}

如果您對視訊有問題，請參閱下列疑難排解指引。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何偵錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>無法預覽視訊</td>
   <td>
    <ul>
     <li>檢查資料夾是否已指派視訊描述檔（如果不支援檔案格式）。 如果不支援，則只會顯示影像。</li>
     <li>視頻配置檔案必須包含多個編碼預設集才能生成AVS集(單個編碼被視為MP4檔案的視頻內容；對於不支援的檔案，則視為與未處理的檔案相同)。</li>
     <li>確認中繼資料中<code>dam:scene7File</code>的<code>dam:scene7FileAvs</code>，以檢查視訊是否已完成處理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊描述檔指派給資料夾。</li>
     <li>編輯視訊設定檔以包含多個編碼預設集。</li>
     <li>等待視頻完成處理。</li>
     <li>重新載入視訊，確定Dynamic Media編碼視訊工作流程未執行。<br /> </li>
     <li>重新上傳影片。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊未編碼</td>
   <td>
    <ul>
     <li>檢查運行模式是否為<code>dynamicmedia_scene7</code>。</li>
     <li>檢查是否已設定Dynamic Media雲端服務。</li>
     <li>檢查視訊設定檔是否與上傳資料夾相關聯。</li>
    </ul> </td>
   <td>
    <ol>
     <li>使用檢查您的Experience Manager例項 <code>-r dynamicmedia_scene7</code></li>
     <li>檢查「Cloud Services」下的Dynamic Media設定是否已正確設定。</li>
     <li>檢查資料夾是否有視訊設定檔。 此外，檢查視訊設定檔。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>視訊處理需要太長時間</td>
   <td><p>要確定視頻編碼是否仍在進行中，或是否已進入故障狀態：</p>
    <ul>
     <li>檢查視訊狀態<code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>從工作流控制台<code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt;實例、存檔、失敗頁簽監視視頻。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>視訊轉譯遺失</td>
   <td><p>上傳視訊時，但沒有編碼的轉譯：</p>
    <ul>
     <li>檢查資料夾是否已指派視訊設定檔。</li>
     <li>確認中繼資料中的<code>dam:scene7FileAvs</code>以檢查視訊已完成處理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>將視訊描述檔指派給資料夾。</li>
     <li>等待視頻完成處理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 檢視器 {#viewers}

如果您在檢視器上有問題，請參閱下列疑難排解指南。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>如何偵錯</strong></td>
   <td><strong>解決方案</strong></td>
  </tr>
  <tr>
   <td>未發佈查看器預設集</td>
   <td><p>繼續到示例管理器診斷頁： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>觀察計算值。 正確運作時，您會看到下列內容：</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注意</strong>:配置檢視器資產的Dynamic Media雲端設定後，可能需要約10分鐘的時間才能同步。</p> <p>如果未啟動的資產仍保留，請選取<strong>列出所有未啟動的資產</strong>按鈕中的任一個，以查看詳細資訊。</p> </td>
   <td>
    <ol>
     <li>導覽至管理工具中的檢視器預設集清單： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>選擇所有查看器預設集，然後選擇<strong>Publish</strong>。</li>
     <li>導覽回範例管理員，並觀察未啟動的資產計數現在為零。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>檢視器預設集圖稿會從資產詳細資料中的預覽或複製URL/內嵌程式碼中傳回404</td>
   <td><p>在CRXDE Lite中執行下列操作：</p>
    <ol>
     <li>導覽至Dynamic Media同步資料夾內的<code>&lt;sync-folder&gt;/_CSS/_OOTB</code>資料夾（例如<code>/content/dam/_CSS/_OOTB</code>）,</li>
     <li>尋找有問題資產的中繼資料節點（例如<code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>）。</li>
     <li>檢查是否存在<code>dam:scene7*</code>屬性。 如果資產已成功同步和發佈，您會看到<code>dam:scene7FileStatus</code>集設為<strong>PublishComplete</strong>。</li>
     <li>嘗試串連下列屬性和字串文字的值，以直接從Dynamic Media請求圖稿
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>範例: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>如果範例資產或檢視器預設集圖稿尚未同步或發佈，請重新啟動整個複製/同步程式：</p>
    <ol>
     <li>導覽至CRXDE Lite。
      <ul>
       <li>刪除 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>導覽至CRX套件管理器：<code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>在清單中搜索查看器包（以<code>cq-dam-scene7-viewers-content</code>開頭）</li>
       <li>選擇<strong>重新安裝</strong>。</li>
      </ol> </li>
     <li>在「Cloud Services」下，導覽至「Dynamic Media設定」頁面，然後開啟Dynamic Media - S7設定的設定對話方塊。
      <ul>
       <li>不進行更改，請選擇<strong>保存</strong>。 此動作會再次觸發邏輯，以建立和同步範例資產、檢視器預設集CSS和圖稿。<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
