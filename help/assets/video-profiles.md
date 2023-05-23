---
title: 視頻配置檔案
description: Dynamic Media已經提供了預定義的自適應視頻編碼配置檔案。 此現成配置檔案中的設定經過優化，為您的客戶提供最佳的觀看體驗。 您還可以將智慧裁剪添加到視頻中。
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
feature: Video Profiles
role: User, Admin
mini-toc-levels: 3
exl-id: b290fac2-7259-45d7-b733-70419d632b07
source-git-commit: 78aa7aac838dabc1c4f0329520092e4755541322
workflow-type: tm+mt
source-wordcount: '3736'
ht-degree: 8%

---

# 視頻配置檔案 {#video-profiles}

Dynamic Media已經提供了預定義的自適應視頻編碼配置檔案。 此現成配置檔案中的設定經過優化，為您的客戶提供最佳的觀看體驗。 使用自適應視頻編碼配置檔案對主源視頻進行編碼時，在回放期間，視頻播放器會根據客戶的Internet連接速度自動調整視頻流的質量。 此功能稱為自適應比特率流。

以下是決定視頻質量的其他因素：

* **上載的主源視頻的解析度**

   如果MP4視頻以較低解析度（如240p或360p）錄制，則無法以高清流式傳輸。

* **視頻播放器大小**

   預設情況下，自適應視頻編碼配置檔案中的「寬度」設定為「自動」。 同樣，在回放期間，根據播放器的大小使用最佳質量。

請參閱 [視頻編碼的最佳做法](/help/assets/video.md#best-practices-for-encoding-videos)。

另請參閱 [組織使用處理配置檔案的數字資產的最佳做法](/help/assets/organize-assets.md)。

>[!NOTE]
>
>要生成視頻的元資料和相關視頻影像縮略圖，視頻本身必須經過Dynamic Media的編碼過程。 在Adobe Experience Manager, **[!UICONTROL Dynamic Media編碼視頻]** 如果您啟用了Dynamic Media並設定了視頻雲服務，則工作流會對視頻進行編碼。 此工作流程會擷取工作流程處理歷程記錄和失敗資訊。請參閱 [監視視頻編碼和YouTube發佈進度](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress)。 如果您已啟用Dynamic Media並設定視頻雲服務， **[!UICONTROL Dynamic Media編碼視頻]** 當您上載視頻時，工作流將自動生效。 (如果你不用Dynamic Media, **[!UICONTROL DAM更新資產]** 工作流生效。)
>
>在搜索資產時，元資料非常有用。 縮略圖是編碼過程中生成的靜態視頻影像。 Experience Manager系統需要這些視頻，並在用戶介面中使用，以幫助您在「卡」視圖、「搜索結果」視圖和「資產清單」視圖中直觀地標識視頻。 選擇編碼視頻的「格式副本」表徵圖（上色調色板）時，可以看到生成的縮略圖。

建立完視頻配置檔案後，將其應用於資料夾或多個資料夾。 請參閱 [將視頻配置檔案應用於資料夾](#applying-a-video-profile-to-folders)。

要為其它資產類型定義高級處理參數，請參閱 [配置資產處理](/help/assets/config-dms7.md#configuring-asset-processing)。

另請參閱 [用於處理元資料、影像和視頻的配置檔案](processing-profiles.md)。

## 自適應視頻編碼預設 {#adaptive-video-encoding-presets}

下表列出了適用於移動和平板電腦設備以及台式電腦的自適應視頻流的最佳編碼配置檔案。 可以將這些預設用於任何縱橫比視頻。

<table>
 <tbody>
  <tr>
   <td><strong>視訊格式轉碼器</strong></td>
   <td><strong>視頻大小 — 寬度(px)</strong></td>
   <td><strong>視頻大小 — 高度(px)</strong></td>
   <td><strong>保持長寬比？</strong></td>
   <td><strong>視頻比特率(Kbps)</strong></td>
   <td><strong>視頻幀速率(FPS)</strong></td>
   <td><strong>音訊轉碼器</strong></td>
   <td><strong>音頻比特率(Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264(MP4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>是</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264(MP4)</p> </td>
   <td>auto</td>
   <td>540</td>
   <td>是</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264(MP4)</p> </td>
   <td>auto</td>
   <td>720<br /> </td>
   <td>是</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## 關於在視頻配置檔案中使用智慧裁剪 {#about-smart-crop-video}

視頻智慧裁剪是「視頻配置檔案」中的一項可選功能，它利用了Adobe Sensei人工智慧的力量。 它會自動檢測並裁剪您上傳的任何自適應視頻或漸進視頻中的焦點，而不管其大小。

支援的智慧裁剪視頻格式包括MP4、MKV、MOV、AVI、FLV和WMV。

智慧裁剪支援的最大視頻檔案大小為以下條件：

* 五分鐘。
* 每秒30幀(FPS)。
* 300-MB檔案大小。

Adobe Sensei限制為9000幀。 也就是，在30 FPS時，5分鐘。 如果視頻的FPS較高，則支援的最大視頻持續時間將減少。 例如，60 FPS視頻的長度必須為2.5分鐘，才能得到Adobe Sensei和智慧裁剪的支援。

![視頻智慧裁剪](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>要使視頻智慧裁剪工作，必須將一個或多個視頻編碼預設與視頻配置檔案一起使用。

要將智慧裁剪用於視頻，請建立自適應或漸進視頻編碼配置檔案。 作為配置檔案的一部分，使用 **[!UICONTROL 智慧裁剪比率]** 工具來選擇預定義的寬高比。 例如，在定義視頻編碼預設後，可以添加長寬比為16x9的「移動橫向」定義和長寬比為9x16的「移動縱向」定義。 您可以從中選擇的其它方面或裁剪比包括1x1、4x3和4x5。

![使用智慧裁剪編輯視頻編碼配置檔案](assets/edit-smart-crop-video2.png)

可以使用位於最右側的滑塊將視頻配置檔案中的視頻智慧裁剪切換為開啟或關閉 **[!UICONTROL 智慧裁剪比率]** 的子菜單。

建立和保存視頻配置檔案後，可以將其應用於所需的資料夾。

請參閱 [將視頻配置檔案應用到特定資料夾](#applying-video-profiles-to-specific-folders) 或 [全局應用視頻配置檔案](#applying-a-video-profile-globally)。

另請參閱 [影像智慧裁剪](image-profiles.md)。

## 為自適應比特率流建立視頻配置檔案 {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media已經提供了預定義的自適應視頻編碼配置檔案，該配置檔案是一組MP4 H.264視頻上傳設定，經過優化，可獲得最佳的觀看體驗。 您可以在上傳視頻時使用此配置檔案。

但是，如果此預定義配置檔案不滿足您的需要，您可以選擇建立自己的自適應視頻編碼配置檔案。 使用設定時 **[!UICONTROL 用於自適應流的編碼]**  — 作為最佳實踐，您添加到配置檔案中的所有編碼預設都經過驗證，以確保所有視頻具有相同的寬高比。 此外，將編碼視頻視為流的多比特率集。

建立視頻編碼配置檔案時，請注意大多數編碼選項都預先填充了建議的預設設定，以幫助您。 但是，如果您選擇的值不是建議的預設值，則會在回放期間和其他效能問題導致視頻質量下降。

因此，對於配置檔案中的所有MP4 H.264視頻編碼預設，將驗證以下值以確保它們在配置檔案中的各個編碼預設之間相同，從而使自適應比特率流化成為可能：

* 視頻格式編解碼器 — MP4 H.264(.mp4)
* 音訊轉碼器
* 音訊位元速率
* 保持長寬比
* 兩遍編碼
* 固定位元速率
* H264 設定檔
* 音訊取樣速率

如果值不相同，則可以繼續按原樣建立配置檔案。 但是，不可能進行自適應比特率流。 相反，用戶會體驗單比特率流。 建議編輯編碼設定，以便在配置檔案中的各個編碼預設之間使用相同的值。 (視頻簡檔/預設編輯器強制自適應視頻編碼設定的奇偶校驗 **[!UICONTROL 用於自適應流的編碼]** 啟用)。

另請參閱 [建立用於逐行流的視頻編碼配置檔案](#creating-a-video-encoding-profile-for-progressive-streaming)。

另請參閱 [視頻編碼的最佳做法](/help/assets/video.md#best-practices-for-encoding-videos)。

要為其它資產類型定義高級處理參數，請參閱 [配置資產處理](/help/assets/config-dms7.md#configuring-asset-processing)。

**為自適應比特率流建立視頻配置檔案**。

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視頻配置檔案]**。
1. 選擇 **[!UICONTROL 建立]** 添加視頻配置檔案。

1. 輸入配置檔案的名稱和說明。
1. 在「建立/編輯視頻編碼預設」頁上，選擇 **[!UICONTROL 添加視頻編碼預設]**。
1. 在 **[!UICONTROL 基本]** 頁籤。
根據所選視頻格式編解碼器，選擇每個選項旁邊的資訊表徵圖以獲取其他說明或建議的設定。
1. 在「視頻大小」標題下，確保 **[!UICONTROL 保持縱橫比]** 的子菜單。
1. 設定視頻幀大小解析度（以像素為單位）。 使用 **[!UICONTROL 自動]** 值以自動縮放以匹配源縱橫比（寬高比）。 例如，「自動x 480」或「640 x自動」。

1. 執行下列任一項作業：

   * 在 **[!UICONTROL 寬度]** 欄位，輸入 **[!UICONTROL 自動]**。 在 **[!UICONTROL 高度]** 欄位，以像素為單位輸入值。

   * 要幫助您可視化視頻的大小，請選擇右側的「資訊」表徵圖(i) **[!UICONTROL 高度]** 開啟「大小計算器」頁。 使用 **[!UICONTROL 大小計算器]** 以設定所需的視頻尺寸（用藍色框表示）。 選擇 **[!UICONTROL X]** 在右上角。

1. （可選）選擇 **[!UICONTROL 高級]** 並確保 **[!UICONTROL 使用預設值]** 複選框（推薦）。 或者，修改高級視頻和音頻設定。
1. 在頁面的右上角，選擇 **[!UICONTROL 保存]** 來保存預設。
1. 執行下列任一項作業：
   * 重複步驟4-10以建立附加編碼預設。 （自適應視頻流需要多個視頻預設。）
   * 繼續下一步。

1. （可選）要將視頻智慧裁剪添加到此配置檔案應用到的視頻中，請執行以下操作：
   * 在「編輯視頻配置檔案」頁上，選擇「智慧裁剪比率」標題右側的 **[!UICONTROL 添加新]**。
   * 在「名稱」欄位中，為裁剪比率鍵入一個名稱，以幫助您輕鬆識別它。
   * 從 **[!UICONTROL 作物比率]** 下拉清單中，選擇要使用的比率。

1. 執行下列任一項作業：

   * 根據需要繼續添加新的作物比率。
   * 繼續下一步。

1. 在頁面的右上角，選擇 **[!UICONTROL 保存]** 的子菜單。

現在，您可以將配置檔案應用於包含視頻的資料夾。 請參閱 [將視頻配置檔案應用於資料夾](#applying-a-video-profile-to-folders) 或 [全局應用視頻配置檔案](#applying-a-video-profile-globally)。

## 建立視頻配置檔案以進行逐行流式處理 {#creating-a-video-encoding-profile-for-progressive-streaming}

如果您選擇不使用該選項 **[!UICONTROL 用於自適應流的編碼]**，添加到配置檔案的所有編碼預設都被視為單比特率流或逐行視頻傳送的單個視頻格式副本。 此外，沒有驗證可確保所有視訊轉譯具有相同的外觀比例。

根據您正在運行的模式，支援的視頻格式編解碼器如下所示：

* Dynamic Media-Scene7模式：H.264(.mp4)
* Dynamic Media — 混合模式：H.264(.mp4),WebM

另請參閱 [建立用於自適應比特率流的視頻編碼配置檔案](#creating-a-video-encoding-profile-for-adaptive-streaming)。

另請參閱 [視頻編碼的最佳做法](/help/assets/video.md#best-practices-for-encoding-videos)。

要為其它資產類型定義高級處理參數，請參閱 [配置資產處理](/help/assets/config-dms7.md#configuring-asset-processing)。

**要為逐行流式處理建立視頻配置檔案，請執行以下操作：**

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視頻配置檔案]**。
1. 選擇 **[!UICONTROL 建立]** 添加視頻配置檔案。
1. 輸入配置檔案的名稱和說明。
1. 在「建立/編輯視頻編碼預設」頁上，選擇 **[!UICONTROL 添加視頻編碼預設]**。
1. 在 **[!UICONTROL 基本]** 頁籤。
根據所選視頻格式編解碼器，選擇每個選項旁邊的資訊表徵圖以獲取其他說明或建議的設定。
1. （可選）在「Video Size（視頻大小）」標題下，取消選中 **[!UICONTROL 保持縱橫比]**。
1. 請執行下列動作：
   * 在 **[!UICONTROL 寬度]** 欄位，輸入 **[!UICONTROL 自動]**。
   * 在 **[!UICONTROL 高度]** 欄位，以像素為單位輸入值。
要幫助您可視化視頻的大小，請選擇「高度」的資訊表徵圖以開啟 **[!UICONTROL 大小計算器]** 的子菜單。 使用 **[!UICONTROL 大小計算器]** 框，以進一步設定視頻維度（藍色框）。 完成後，在對話框的右上角，選擇 **[!UICONTROL X]**。
1. （可選）執行下列操作之一：

   * 選擇 **[!UICONTROL 高級]** ，並確保 **[!UICONTROL 使用預設值]** 複選框（推薦）。

   * 清除 **[!UICONTROL 使用預設值]** 複選框，然後指定所需的視頻設定和音頻設定。
根據所選視頻格式編解碼器，選擇每個選項旁邊的資訊表徵圖以獲取其他說明或建議的設定。

1. 在頁面的右上角，選擇 **[!UICONTROL 保存]** 來保存預設。
1. 執行下列任一項作業：

   * 重複步驟4-9以建立附加編碼預設。
   * 繼續下一步。

1. （可選）要將視頻智慧裁剪添加到此配置檔案應用到的視頻中，請執行以下操作：

   * 在「編輯視頻配置檔案」頁上，選擇「智慧裁剪比率」標題右側的 **[!UICONTROL 添加新]**。
   * 在「名稱」欄位中，為裁剪比率鍵入一個名稱，以幫助您輕鬆識別它。
   * 從 **[!UICONTROL 作物比率]** 下拉清單中，選擇要使用的比率。

1. 執行下列任一項作業：

   * 根據需要繼續添加新的作物比率。
   * 繼續下一步。

1. 在頁面的右上角，選擇 **[!UICONTROL 保存]** 的子菜單。

現在，您可以將配置檔案應用於包含視頻的資料夾。 請參閱 [將視頻配置檔案應用到資料夾](#applying-a-video-profile-to-folders) 或 [全局應用視頻配置檔案](#applying-a-video-profile-globally)。

## 使用自定義添加的視頻編碼參數 {#using-custom-added-video-encoding-parameters}

在Experience Manager中建立或編輯視頻配置檔案時，可以編輯現有視頻編碼配置檔案以利用用戶介面中找不到的高級視頻編碼參數。 將一個或多個高級參數（如minBitrate和maxBitrate）添加到現有配置檔案。

**要使用自定義添加的視頻編碼參數：**

1. 選擇Experience Manager徽標，然後導航至 **[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL CRXDE Lite]**。
1. 從CRXDE Lite頁，在左側的「瀏覽器」面板中，導航至以下內容：

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. 在頁面右下方的面板中，從「屬性」標籤中，指定您要使用之參 **[!UICONTROL 數的「名稱]**」、「類型」和「 **[!UICONTROL 值]****** 」。

   以下高級參數可供使用：

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>說明</strong><br /> </td>
   <td><strong>類型</strong><br /> </td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>用於編碼的H.264級。 通常，此參數會根據您使用的編碼設定自動確定。</td>
   <td><code>String</code></td>
   <td><p>10 * h264級</p> <p>例如，3.0 = 30,1.3 = 13)</p> <p>無預設值。</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>關鍵幀之間的目標幀數。 計算此值，以便每2-10秒生成一個關鍵幀。 例如，在每秒30幀時，關鍵幀間隔應為60-300。<br /> <br /> 較低的關鍵幀間隔改善了自適應視頻編碼的流查找和流切換行為，並且還可以改善具有大量運動的視頻的質量。 但是，由於關鍵幀會增大檔案的大小，因此較低的關鍵幀間隔通常會導致給定比特率下的整體視頻質量降低。</td>
   <td><code>String</code></td>
   <td><p>正數。</p> <p>預設值為300。</p> <p>DASH或HLS的建議值為60-90。 (若要將DASH用於視頻，必須先在您的帳戶中啟用它。 請參閱 <a href="/help/assets/video.md#enable-dash">啟用帳戶上的DASH</a>。)</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>允許以Kbps（千比特/秒）為單位的可變比特率編碼的最小比特率。</p> <p>此參數僅在<strong> 使用常數比特率</strong> 在建立或編輯視頻編碼配置檔案時，在「高級」頁籤中取消選擇。</p> <p>另請參閱 <a href="/help/assets/video.md#bitrate">比特率</a>。</p> </td>
   <td><code>String</code></td>
   <td><p>正數，以Kbps為單位。</p> <p>無預設值。</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>允許可變比特率編碼的最大比特率(Kbps)。</p> <p>此參數僅在<strong> 使用常數比特率</strong> 在建立或編輯視頻編碼配置檔案時，在「高級」頁籤中取消選擇。</p> <p>另請參閱 <a href="/help/assets/video.md#bitrate">比特率</a>。</p> </td>
   <td><code>String</code></td>
   <td><p>正數，以Kbps為單位。</p> <p>無預設值。 但是，建議的值是編碼比特率的兩倍。</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>將值設定為 <code>true</code> 強制音頻流的恆定比特率（如果受音頻編解碼器支援）。</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>預設值為 <code>false</code>。</p> <p>DASH或HLS的建議值為 <code>false</code>。 (若要將DASH用於視頻，必須先在您的帳戶中啟用它。 請參閱 <a href="/help/assets/video.md#enable-dash">啟用帳戶上的DASH</a>。)</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. 在頁面右下角附近，選擇 **[!UICONTROL 添加]**。
1. 執行下列任一項作業：

   * 重複步驟3和4，將另一個參數添加到視頻編碼配置檔案中。
   * 在頁面左上角附近，選擇 **[!UICONTROL 全部保存]**。

1. 在CRXDE Lite頁的左上角，選擇 **[!UICONTROL 返回首頁]** 表徵圖以返回Experience Manager。

### 編輯視頻配置檔案 {#editing-a-video-encoding-profile}

您可以編輯已建立的用於添加、編輯或刪除該配置檔案中的視頻預設的任何視頻配置檔案。

預設情況下，不能編輯預定義的現成版本 **[!UICONTROL 自適應視頻編碼]** Dynamic Media的檔案。 相反，您可以輕鬆複製配置檔案並使用新名稱保存它。 然後，可以在複製的配置檔案中編輯所需的預設。

另請參閱 [視頻編碼的最佳做法](/help/assets/video.md#best-practices-for-encoding-videos)。

要為其它資產類型定義高級處理參數，請參閱 [配置資產處理](/help/assets/config-dms7.md#configuring-asset-processing)。

**編輯視頻配置檔案：**

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視頻配置檔案]**。
1. 在「視頻配置檔案」頁面上，檢查一個視頻配置檔案名稱。
1. 在工具欄上，選擇 **[!UICONTROL 編輯]**。
1. 在「視頻編碼概要檔案」頁上，根據需要編輯名稱和說明。
1. 作為最佳做法，確保 **[!UICONTROL 用於自適應比特率流的編碼]** 的雙曲餘切值。
選擇資訊表徵圖以描述自適應比特率流。 （如果正在編輯漸進視頻配置檔案，請不要選中此複選框。）
1. 在「視頻編碼預設」標題下，添加、編輯或刪除構成配置檔案的視頻編碼預設。

   選擇上每個選項旁邊的資訊表徵圖 **[!UICONTROL 基本]** 和 **[!UICONTROL 高級]** 頁籤，用於根據所選視頻格式編解碼器進行其他說明或推薦設定。

1. 在頁面的右上角，選擇 **[!UICONTROL 保存]**。

### 複製視頻配置檔案 {#copying-a-video-encoding-profile}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視頻配置檔案]**。
1. 在「視頻配置檔案」頁面上，檢查一個視頻配置檔案名稱。
1. 在工具欄上，選擇 **[!UICONTROL 複製]**。
1. 在「視頻編碼概要檔案」頁上，輸入概要檔案的新名稱。
1. 最佳實務是，請確定已選取「 **[!UICONTROL 最適化串流編碼]** 」核取方塊。選擇資訊表徵圖以描述自適應比特率流。  (如果您要複製漸進式視訊設定檔，請勿選取核取方塊。) 

   在Dynamic Media — 混合模式下，如果WebM視頻預設是視頻配置檔案的一部分，則 **[!UICONTROL 用於自適應流的編碼]** 不可能，因為所有預設都必須是MP4。
1. 在「視頻編碼預設」標題下，添加、編輯或刪除構成配置檔案的視頻編碼預設。

   選擇「基本」(Basic)和「高級」(Advanced)頁籤上每個選項旁邊的資訊表徵圖，以瞭解建議的設定和說明。

1. 在頁面的右上角，選擇 **[!UICONTROL 保存]**。

### 刪除視頻配置檔案 {#deleting-a-video-encoding-profile}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視頻配置檔案]**。
1. 在「視頻配置檔案」頁面上，檢查一個或多個視頻配置檔案名稱。
1. 在工具欄上，選擇 **[!UICONTROL 刪除]**。
1. 選擇 **[!UICONTROL 確定]**。

## 將視頻配置檔案應用於資料夾 {#applying-a-video-profile-to-folders}

將視頻配置檔案分配給資料夾時，任何子資料夾都會自動從其父資料夾繼承配置檔案。 此規則表示只能將一個視頻配置檔案分配給資料夾。 因此，請仔細考慮上載、儲存、使用和存檔資產所在的資料夾結構。

如果為資料夾分配了不同的視頻配置檔案，則新配置檔案將覆蓋以前的配置檔案。 以前現有的資料夾資產保持不變。 新配置檔案將應用於稍後添加到資料夾的資產。

在用戶介面中，將配置檔案分配給它的資料夾通過配置檔案名稱在卡名稱中的外觀來指示。

![chlimage_1-517](assets/chlimage_1-517.png)

您可以將視頻配置檔案應用於特定資料夾或全局應用於所有資產。

您可以重新處理資料夾中的資產，該資料夾中已有您稍後更改的現有視頻配置檔案。 請參閱 [編輯資料夾的處理配置檔案後，重新處理資料夾中的資產](processing-profiles.md#reprocessing-assets)。

### 將視頻配置檔案應用到特定資料夾 {#applying-video-profiles-to-specific-folders}

您可以從「工具」菜單或在資料夾中從「屬性」將視頻配置檔案應 **[!UICONTROL 用到資料夾]******。本節說明如何以兩種方式將視訊描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

另請參閱 [編輯資料夾的處理配置檔案後，重新處理資料夾中的資產](processing-profiles.md#reprocessing-assets)。

#### 通過配置檔案用戶介面將視頻配置檔案應用到資料夾 {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視頻配置檔案]**。
1. 選擇要應用於資料夾或多個資料夾的視頻配置檔案。
1. 選擇 **[!UICONTROL 將配置檔案應用於資料夾]** 並選擇要用於接收新上載資產的資料夾或多個資料夾，然後選擇 **[!UICONTROL 應用]**。 在「卡片檢視」中，資料夾名稱正下方會顯示資料夾名稱，以指出已指派給資料夾的 **[!UICONTROL 資料夾]**。你可以 [監視視頻配置檔案處理作業的進度](#monitoring-the-progress-of-an-encoding-job)。

#### 將視頻配置檔案應用到「屬性」中的資料夾 {#applying-video-profiles-to-folders-from-properties}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 資產]** 然後，將視頻配置檔案應用到的資料夾。
1. 在資料夾上，選擇複選標籤以選擇它，然後選擇 **[!UICONTROL 屬性]**。
1. 選擇 **[!UICONTROL 視頻配置檔案]** ，然後從下拉菜單中選擇配置檔案，然後選擇 **[!UICONTROL 保存並關閉]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

   ![chlimage_1-518](assets/chlimage_1-518.png)
你可以 [監視視頻配置檔案處理作業的進度](#monitoring-the-progress-of-an-encoding-job)。

### 全局應用視頻配置檔案 {#applying-a-video-profile-globally}

除了將配置檔案應用到資料夾外，您還可以全局應用一個配置檔案，以便任何資料夾中上載到Experience Manager Assets的任何內容都應用了選定的配置檔案。

另請參閱 [編輯資料夾的處理配置檔案後，重新處理資料夾中的資產](processing-profiles.md#reprocessing-assets)。

**要全局應用視頻配置檔案，請執行以下操作：**

* 導航到CRXDE Lite到以下節點： `/content/dam/jcr:content`。 添加屬性 `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` 選擇 **[!UICONTROL 全部保存]**。

   ![chlimage_1-519](assets/chlimage_1-519.png)
* 你可以 [監視視頻配置檔案處理作業的進度](#monitoring-the-progress-of-an-encoding-job)。

## 監視視頻配置檔案處理作業的進度 {#monitoring-the-progress-of-an-encoding-job}

顯示一個處理指示器（或進度條），以便您可以直觀地監視視頻配置檔案處理作業的進度。

您還可以查看 `error.log` 檔案，監視編碼作業的進度，查看編碼是否完成，或查看任何作業錯誤。 的 `error.log` 的 `logs` 安裝Experience Manager實例的資料夾。

## 從資料夾中刪除視頻配置檔案 {#removing-a-video-profile-from-folders}

從資料夾中刪除視頻配置檔案時，任何子資料夾都會自動從其父資料夾中繼承刪除配置檔案。 但是，對資料夾中已發生的檔案的任何處理都保持不變。

您可以從「工具」功能表內的資料夾或在資料夾內的「資料夾設定」中移除視訊描述檔 ********。本節說明如何以兩種方式從資料夾移除視訊描述檔。

### 通過「配置式」用戶介面從資料夾中刪除視頻配置檔案 {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視頻配置檔案]**。
1. 選擇要從資料夾或多個資料夾中刪除的視頻配置檔案。
1. 選擇 **[!UICONTROL 從資料夾中刪除配置檔案]** 並選擇要用於從中刪除配置檔案的資料夾或多個資料夾，然後選擇 **[!UICONTROL 刪除]**。

   您可以確認視頻配置檔案不再應用於資料夾，因為該名稱不再出現在資料夾名稱下。

### 通過「屬性」從資料夾中刪除視頻配置檔案 {#removing-video-profiles-from-folders-by-way-of-properties}

1. 選擇Experience Manager徽標並導航至 **[!UICONTROL 資產]** 然後轉到要從中刪除視頻配置檔案的資料夾。
1. 在資料夾上，選擇複選標籤，然後選擇 **[!UICONTROL 屬性]**。
1. 選擇 **[!UICONTROL 視頻配置檔案]** 頁籤 **[!UICONTROL 無]** 從下拉菜單中選擇 **[!UICONTROL 保存並關閉]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
