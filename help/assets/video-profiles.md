---
title: 視訊設定檔
description: Dynamic Media已隨附預先定義的最適化視訊編碼設定檔。 此現成可用設定檔中的設定已最佳化，可為客戶提供最佳的檢視體驗。 您也可以將智慧型裁切新增至影片。
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
source-git-commit: dacbfbc8b4677ac7b63b92c45602e030031de3a1
workflow-type: tm+mt
source-wordcount: '3727'
ht-degree: 9%

---

# 視訊設定檔 {#video-profiles}

Dynamic Media已隨附預先定義的最適化視訊編碼設定檔。 此現成可用設定檔中的設定已最佳化，可為客戶提供最佳的檢視體驗。 當您使用「最適化視訊編碼」設定檔為主要來源視訊編碼時，在播放期間，視訊播放器會根據客戶的網際網路連線速度自動調整視訊資料流的品質。 此功能稱為最適化串流。

以下是決定視訊品質的其他因素：

* **上傳的主要來源影片解析度**

   如果MP4視頻以低解析度（如240p或360p）記錄，則不能以高清流式傳輸。

* **視訊播放器大小**

   依預設，適用性視訊編碼設定檔中的「寬度」會設為「自動」。 同樣地，在播放期間會根據播放器的大小來使用最佳品質。

請參閱 [視訊編碼最佳作法](/help/assets/video.md#best-practices-for-encoding-videos).

另請參閱 [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md).

>[!NOTE]
>
>若要產生視訊的中繼資料和相關的視訊影像縮圖，視訊本身必須完成Dynamic Media中的編碼程式。 在Adobe Experience Manager, **[!UICONTROL Dynamic Media編碼視訊]** 如果您已啟用Dynamic Media並設定視訊雲端服務，工作流程會對視訊進行編碼。 此工作流程會擷取工作流程處理歷程記錄和失敗資訊。請參閱 [監視視訊編碼和YouTube發佈進度](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). 如果您已啟用Dynamic Media並設定視訊雲端服務，則 **[!UICONTROL Dynamic Media編碼視訊]** 上傳視訊時，工作流程會自動生效。 (如果您未使用Dynamic Media, **[!UICONTROL DAM更新資產]** 工作流程生效。)
>
>搜尋資產時，中繼資料很實用。 縮圖是編碼期間產生的靜態視訊影像。 Experience Manager系統需要這些視訊，並用於使用者介面，協助您在「卡片」檢視、「搜尋結果」檢視和「資產清單」檢視中以視覺化方式識別視訊。 選取已編碼視訊的「轉譯」圖示（上色盤）時，您可以看到產生的縮圖。

建立完視訊描述檔後，可將其套用至資料夾或多個資料夾。 請參閱 [將視訊描述檔套用至資料夾](#applying-a-video-profile-to-folders).

若要定義其他資產類型的進階處理參數，請參閱 [設定資產處理](/help/assets/config-dms7.md#configuring-asset-processing).

另請參閱 [處理中繼資料、影像和視訊的設定檔](processing-profiles.md).

## 最適化視訊編碼預設集 {#adaptive-video-encoding-presets}

下表列出將設定檔編碼為行動裝置、平板電腦裝置和桌上型電腦的最適化視訊串流的最佳實務。 您可以將這些預設集用於任何外觀比例視訊。

<table>
 <tbody>
  <tr>
   <td><strong>視訊格式轉碼器</strong></td>
   <td><strong>視訊大小 — 寬度(px)</strong></td>
   <td><strong>視訊大小 — 高度(px)</strong></td>
   <td><strong>保持長寬比？</strong></td>
   <td><strong>視訊位元速率(Kbps)</strong></td>
   <td><strong>視訊影格速率(Fps)</strong></td>
   <td><strong>音訊轉碼器</strong></td>
   <td><strong>音頻位元速率(Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264(mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>是</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264(mp4)</p> </td>
   <td>auto</td>
   <td>540</td>
   <td>是</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264(mp4)</p> </td>
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

## 關於在視訊設定檔中使用智慧型裁切 {#about-smart-crop-video}

智慧型裁切視訊 — 視訊描述檔中提供的選用功能 — 是運用Adobe Sensei人工智慧功能的工具。 它會自動偵測並裁切您所上傳之任何最適化視訊或漸進式視訊中的焦點（不論大小）。

智慧裁切的支援視訊格式包括MP4、MKV、MOV、AVI、FLV和WMV。

智慧型裁切支援的最大視訊檔案大小如下：

* 持續5分鐘。
* 每秒30幀(FPS)。
* 300-MB檔案大小。

Adobe Sensei限制為9000幀。 即，以30 FPS為單位，5分鐘。 如果您的視訊的FPS較高，則支援的視訊持續時間上限會降低。 例如， 60 FPS視訊的長度必須為2.5分鐘，才能獲得Adobe Sensei和智慧型裁切支援。

![智慧型裁切視訊](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>若要讓視訊智慧型裁切運作，您必須包含一或多個視訊編碼預設集與您的視訊設定檔。

若要使用視訊的智慧型裁切，請建立最適化或漸進式視訊編碼設定檔。 作為設定檔的一部分，請使用 **[!UICONTROL 智慧型裁切比例]** 工具來選取預先定義的外觀比例。 例如，在定義視訊編碼預設集後，您可以新增長寬比為16x9的「行動橫向」定義，以及長寬比為9x16的「行動縱向」定義。 您可選擇的其他外觀或裁切比例包括1x1、4x3和4x5。

![使用智慧型裁切功能編輯視訊編碼設定檔](assets/edit-smart-crop-video2.png)

您可以使用 **[!UICONTROL 智慧型裁切比例]** 在使用者介面中。

建立並儲存視訊設定檔後，即可將其套用至您想要的資料夾。

請參閱 [將視訊設定檔套用至特定資料夾](#applying-video-profiles-to-specific-folders) 或 [全域套用視訊設定檔](#applying-a-video-profile-globally).

另請參閱 [影像智慧型裁切](image-profiles.md).

## 建立最適化串流的視訊設定檔 {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media已隨附預先定義的適用性視訊編碼設定檔，此設定檔為一組適用於MP4 H.264的視訊上傳設定，並針對最佳的檢視體驗進行最佳化。 上傳影片時，您可以使用此設定檔。

不過，如果此預先定義的設定檔不符合您的需求，您可以選取建立自己的最適化視訊編碼設定檔。 使用設定時 **[!UICONTROL 用於自適應流的編碼]**  — 最佳實務 — 您新增至設定檔的所有編碼預設集都會經過驗證，以確保所有視訊具有相同的外觀比例。 此外，編碼視訊被視為串流的多位元速率集。

當您建立視訊編碼設定檔時，請注意大部分的編碼選項都已預先填入建議的預設設定，以協助您。 不過，如果您選取的值不是建議的預設值，可能會在播放期間和其他效能問題導致視訊品質不佳。

因此，對於設定檔中的所有MP4 H.264視訊編碼預設集，會驗證下列值，以確保它們在設定檔中的各個編碼預設集之間相同，進而實現最適化串流：

* 視頻格式編解碼器 — MP4 H.264(.mp4)
* 音訊轉碼器
* 音訊位元速率
* 保持長寬比
* 兩遍編碼
* 固定位元速率
* H264 設定檔
* 音訊取樣速率

如果值不同，您可以繼續依原樣建立設定檔。 不過，無法進行最適化串流。 而是讓使用者體驗單位元速率串流。 建議您編輯編碼設定，以便在設定檔中的各個編碼預設集之間使用相同的值。 (如果 **[!UICONTROL 用於自適應流的編碼]** 已啟用。)

另請參閱 [為漸進式串流建立視訊編碼設定檔](#creating-a-video-encoding-profile-for-progressive-streaming).

另請參閱 [視訊編碼最佳作法](/help/assets/video.md#best-practices-for-encoding-videos).

若要定義其他資產類型的進階處理參數，請參閱 [設定資產處理](/help/assets/config-dms7.md#configuring-asset-processing).

**為最適化串流建立視訊設定檔的方式**,

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 選擇 **[!UICONTROL 建立]** 新增視訊設定檔。

1. 輸入設定檔的名稱和說明。
1. 在「建立/編輯視頻編碼預設集」頁上，選擇 **[!UICONTROL 新增視訊編碼預設集]**.
1. 在 **[!UICONTROL 基本]** 頁簽，設定視頻和音頻選項。
選擇每個選項旁的資訊表徵圖，以獲取其他說明或根據所選視頻格式編解碼器推薦的設定。
1. 在「視訊大小」標題下，確定 **[!UICONTROL 保持長寬比]** 已勾選。
1. 設定視頻幀大小解析度（像素）。 使用 **[!UICONTROL 自動]** 值來自動縮放以符合來源長寬比（寬高比）。 例如「自動x 480」或「640」。

1. 執行下列任一項作業：

   * 在 **[!UICONTROL 寬度]** 欄位，輸入 **[!UICONTROL 自動]**. 在 **[!UICONTROL 高度]** 欄位中，輸入像素值。

   * 若要協助您視覺化視訊的大小，請選取右側的「資訊」圖示(i) **[!UICONTROL 高度]** 開啟「大小計算器」頁。 使用 **[!UICONTROL 大小電腦]** 設定您想要的視訊尺寸（以藍色方塊表示）。 選擇 **[!UICONTROL X]** 在右上角。

1. （選用）選取 **[!UICONTROL 進階]** 標籤，並確保 **[!UICONTROL 使用預設值]** 核取方塊（建議）。 或者，修改進階視訊和音訊設定。
1. 在頁面的右上角，選取 **[!UICONTROL 儲存]** 來儲存預設集。
1. 執行下列任一項作業：
   * 重複步驟4-10以建立其他編碼預設集。 （最適化視訊串流需要多個視訊預設集。）
   * 繼續下一步。

1. （可選）若要將視訊智慧型裁切新增至套用此設定檔的視訊，請執行下列動作：
   * 在「編輯視訊描述檔」頁面的「智慧型裁切比例」標題右側，選取 **[!UICONTROL 新增]**.
   * 在「名稱」欄位中，輸入裁切比例的名稱，以協助您輕鬆識別。
   * 從 **[!UICONTROL 裁切比例]** 下拉式清單中，選取您要使用的比率。

1. 執行下列任一項作業：

   * 視需要繼續新增裁切比例。
   * 繼續下一步。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]** 來儲存設定檔。

您現在可以將設定檔套用至包含視訊的資料夾。 請參閱 [將視訊描述檔套用至資料夾](#applying-a-video-profile-to-folders) 或 [全域套用視訊設定檔](#applying-a-video-profile-globally).

## 建立視訊設定檔以進行漸進式串流 {#creating-a-video-encoding-profile-for-progressive-streaming}

如果您選擇不使用選項 **[!UICONTROL 用於自適應流的編碼]**，您新增至設定檔的所有編碼預設集都會視為個別視訊轉譯，以用於單位元速率串流或漸進式視訊傳送。 此外，沒有驗證可確保所有視訊轉譯具有相同的外觀比例。

視您執行的模式而定，支援的視訊格式轉碼器如下：

* Dynamic Media-Scene7模式：H.264(.mp4)
* Dynamic Media — 混合模式：H.264(.mp4), WebM

另請參閱 [建立最適化串流的視訊編碼設定檔](#creating-a-video-encoding-profile-for-adaptive-streaming).

另請參閱 [視訊編碼最佳作法](/help/assets/video.md#best-practices-for-encoding-videos).

若要定義其他資產類型的進階處理參數，請參閱 [設定資產處理](/help/assets/config-dms7.md#configuring-asset-processing).

**若要建立漸進式串流的視訊設定檔：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 選擇 **[!UICONTROL 建立]** 新增視訊設定檔。
1. 輸入設定檔的名稱和說明。
1. 在「建立/編輯視頻編碼預設集」頁上，選擇 **[!UICONTROL 新增視訊編碼預設集]**.
1. 在 **[!UICONTROL 基本]** 頁簽，設定視頻和音頻選項。
選擇每個選項旁的資訊表徵圖，以獲取其他說明或根據所選視頻格式編解碼器推薦的設定。
1. （可選）在「Video Size（視頻大小）」標題下，取消選中 **[!UICONTROL 保持長寬比]**.
1. 請執行下列動作：
   * 在 **[!UICONTROL 寬度]** 欄位，輸入 **[!UICONTROL 自動]**.
   * 在 **[!UICONTROL 高度]** 欄位中，輸入像素值。
若要協助您視覺化視訊的大小，請選取「高度」的資訊圖示以開啟 **[!UICONTROL 大小電腦]** 頁面。 使用 **[!UICONTROL 大小電腦]** 頁面，以進一步設定您想要的視訊維度（藍方塊）。 完成後，在對話框的右上角，選擇 **[!UICONTROL X]**.
1. （選用）執行下列其中一項作業：

   * 選取 **[!UICONTROL 進階]** 標籤，並確認 **[!UICONTROL 使用預設值]** 核取方塊（建議）。

   * 清除 **[!UICONTROL 使用預設值]** 核取方塊，並指定您想要的視訊設定和音訊設定。
選擇每個選項旁的資訊表徵圖，以獲取其他說明或根據所選視頻格式編解碼器推薦的設定。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]** 來儲存預設集。
1. 執行下列任一項作業：

   * 重複步驟4-9以建立其他編碼預設集。
   * 繼續下一步。

1. （可選）若要將視訊智慧型裁切新增至套用此設定檔的視訊，請執行下列動作：

   * 在「編輯視訊描述檔」頁面的「智慧型裁切比例」標題右側，選取 **[!UICONTROL 新增]**.
   * 在「名稱」欄位中，輸入裁切比例的名稱，以協助您輕鬆識別。
   * 從 **[!UICONTROL 裁切比例]** 下拉式清單中，選取您要使用的比率。

1. 執行下列任一項作業：

   * 視需要繼續新增裁切比例。
   * 繼續下一步。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]** 以儲存設定檔。

您現在可以將設定檔套用至包含視訊的資料夾。 請參閱 [將視訊描述檔套用至資料夾](#applying-a-video-profile-to-folders) 或 [全域套用視訊設定檔](#applying-a-video-profile-globally).

## 使用自訂新增的視訊編碼參數 {#using-custom-added-video-encoding-parameters}

您可以編輯現有的視訊編碼設定檔，以利用進階視訊編碼參數；當您在Experience Manager中建立或編輯視訊設定檔時，無法在使用者介面中找到這些參數。 將一或多個進階參數（例如minBitrate和maxBitrate）新增至您現有的設定檔。

**若要使用自訂新增的視訊編碼參數：**

1. 選取Experience Manager標誌，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 從「CRXDE Lite」頁面，在左側的「瀏覽器」面板中，導覽至下列項目：

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. 在頁面右下方的面板中，從「屬性」標籤中，指定您要使用之參 **[!UICONTROL 數的「名稱]**」、「類型」和「 **[!UICONTROL 值]****** 」。

   可使用下列進階參數：

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
   <td>要用於編碼的H.264級。 這個參數通常會根據您使用的編碼設定自動決定。</td>
   <td><code>String</code></td>
   <td><p>10 * h264</p> <p>例如3.0 = 30,1.3 = 13)</p> <p>無預設值。</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>關鍵幀之間的幀的目標數量。 計算此值，以便每2-10秒生成一個關鍵幀。 例如，在每秒30幀時，關鍵幀間隔應為60-300。<br /> <br /> 較低的關鍵幀間隔可改善最適化視頻編碼的流搜索和流切換行為，還可能改善具有大量運動的視頻的質量。 但是，由於關鍵幀會增加檔案的大小，因此較低的關鍵幀間隔通常會導致以指定位元速率顯示的整體視頻質量較低。</td>
   <td><code>String</code></td>
   <td><p>正數。</p> <p>預設為300。</p> <p>DASH或HLS的建議值為60-90。 (若要對影片使用DASH，必須先在您的帳戶啟用。 請參閱 <a href="/help/assets/video.md#enable-dash">在您的帳戶上啟用DASH</a>.)</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>允許可變位元速率編碼的最小位元速率，單位為每秒千位元組數。</p> <p>此參數僅適用於<strong> 使用常數位元速率</strong> 在您建立或編輯視訊編碼設定檔時，會在「進階」標籤中取消選取此選項。</p> <p>另請參閱 <a href="/help/assets/video.md#bitrate">位元速率</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>正數，以每秒位數為單位。</p> <p>無預設值。</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>允許可變位元速率編碼的最大位元速率（以每秒位元組數為單位）。</p> <p>此參數僅適用於<strong> 使用常數位元速率</strong> 在您建立或編輯視訊編碼設定檔時，會在「進階」標籤中取消選取此選項。</p> <p>另請參閱 <a href="/help/assets/video.md#bitrate">位元速率</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>正數，以每秒位數為單位。</p> <p>無預設值。 不過，建議的值最多是編碼位元速率的兩倍。</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>將值設定為 <code>true</code> 強制音頻流的恆定位元速率（如果受音頻編解碼器支援）。</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>預設為 <code>false</code>.</p> <p>DASH或HLS的建議值為 <code>false</code>. (若要對影片使用DASH，必須先在您的帳戶啟用。 請參閱 <a href="/help/assets/video.md#enable-dash">在您的帳戶上啟用DASH</a>.)</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. 在頁面的右下角附近，選取 **[!UICONTROL 新增]**.
1. 執行下列任一項作業：

   * 重複步驟3和4，將其他參數新增至您的視訊編碼設定檔。
   * 在頁面左上角附近，選取 **[!UICONTROL 全部儲存]**.

1. 在CRXDE Lite頁面的左上角，選取 **[!UICONTROL 回家]** 表徵圖返回Experience Manager。

### 編輯視訊設定檔 {#editing-a-video-encoding-profile}

您可以編輯已建立的任何視訊設定檔，以新增、編輯或刪除該設定檔中的視訊預設集。

依預設，您無法編輯預先定義的現成可用功能 **[!UICONTROL 最適化視訊編碼]** 隨Dynamic Media而來的。 相反地，您可以輕鬆複製設定檔並以新名稱儲存。 然後，您可以在複製的設定檔中編輯所需的預設集。

另請參閱 [視訊編碼最佳作法](/help/assets/video.md#best-practices-for-encoding-videos).

若要定義其他資產類型的進階處理參數，請參閱 [設定資產處理](/help/assets/config-dms7.md#configuring-asset-processing).

**若要編輯視訊設定檔：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 在視訊描述檔頁面上，檢查一個視訊描述檔名稱。
1. 在工具列上，選取 **[!UICONTROL 編輯]**.
1. 在「視訊編碼描述檔」頁面上，視需要編輯名稱和說明。
1. 最佳實務是，請確定已選取「 **[!UICONTROL 最適化串流編碼]** 」核取方塊。選取資訊圖示，以取得最適化串流的說明。 （如果您正在編輯漸進式視訊設定檔，請勿選取此核取方塊。）
1. 在「視訊編碼預設集」標題下，新增、編輯或刪除組成設定檔的視訊編碼預設集。

   選取 **[!UICONTROL 基本]** 和 **[!UICONTROL 進階]** 標籤，以取得其他說明或根據所選視訊格式codec建議的設定。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]**.

### 複製視訊設定檔 {#copying-a-video-encoding-profile}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 在視訊描述檔頁面上，檢查一個視訊描述檔名稱。
1. 在工具列上，選取 **[!UICONTROL 複製]**.
1. 在「視訊編碼描述檔」頁面上，輸入描述檔的新名稱。
1. 最佳實務是，請確定已選取「 **[!UICONTROL 最適化串流編碼]** 」核取方塊。選取資訊圖示，以取得最適化串流的說明。  (如果您要複製漸進式視訊設定檔，請勿選取核取方塊。) 

   在Dynamic Media — 混合模式中，如果WebM視訊預設集是視訊設定檔的一部分，則 **[!UICONTROL 用於自適應流的編碼]** 不可能，因為所有預設集必須是MP4。
1. 在「視訊編碼預設集」標題下，新增、編輯或刪除組成設定檔的視訊編碼預設集。

   選取「基本」和「進階」標籤上每個選項旁的資訊圖示，以取得建議的設定和說明。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]**.

### 刪除視訊設定檔 {#deleting-a-video-encoding-profile}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 在視訊描述檔頁面上，檢查一或多個視訊描述檔名稱。
1. 在工具列上，選取 **[!UICONTROL 刪除]**.
1. 選擇 **[!UICONTROL 確定]**.

## 將視訊描述檔套用至資料夾 {#applying-a-video-profile-to-folders}

將視訊描述檔指派給資料夾時，任何子資料夾都會自動從其父資料夾繼承描述檔。 此規則表示您只能將一個視訊描述檔指派給資料夾。 因此，請仔細考慮上傳、儲存、使用和封存資產的資料夾結構。

如果您將不同的視訊描述檔指派給資料夾，新的描述檔會覆寫先前的描述檔。 先前的資料夾資產維持不變。 新設定檔會套用至稍後新增至資料夾的資產。

在用戶介面中，會以卡片名稱中配置檔案名稱的外觀來指示為其分配配置檔案的資料夾。

![chlimage_1-517](assets/chlimage_1-517.png)

您可以將視訊設定檔套用至特定資料夾，或全域套用至所有資產。

若資料夾中已有您之後已變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 請參閱 [編輯資料夾中的資產處理設定檔後，重新處理該資料夾中的資產](processing-profiles.md#reprocessing-assets).

### 將視訊設定檔套用至特定資料夾 {#applying-video-profiles-to-specific-folders}

您可以從「工具」菜單或在資料夾中從「屬性」將視頻配置檔案應 **[!UICONTROL 用到資料夾]******。本節說明如何以兩種方式將視訊描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

另請參閱 [編輯資料夾中的資產處理設定檔後，重新處理該資料夾中的資產](processing-profiles.md#reprocessing-assets).

#### 透過設定檔使用者介面，將視訊設定檔套用至資料夾 {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 選取您要套用至資料夾或多個資料夾的視訊設定檔。
1. 選擇 **[!UICONTROL 將配置檔案應用於資料夾]** ，然後選取您要用來接收新上傳資產的資料夾或多個資料夾，並選取 **[!UICONTROL 套用]**. 在「卡片檢視」中，資料夾名稱正下方會顯示資料夾名稱，以指出已指派給資料夾的 **[!UICONTROL 資料夾]**。您可以 [監視視訊設定檔處理作業的進度](#monitoring-the-progress-of-an-encoding-job).

#### 從屬性將視訊描述檔套用至資料夾 {#applying-video-profiles-to-folders-from-properties}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]** 然後，再套用至您要套用視訊描述檔的資料夾。
1. 在資料夾中，選取要選取的核取記號，然後選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL 視訊設定檔]** ，然後從下拉式選單中選取設定檔，然後選取 **[!UICONTROL 儲存並關閉]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

   ![chlimage_1-518](assets/chlimage_1-518.png)
您可以 [監視視訊設定檔處理作業的進度](#monitoring-the-progress-of-an-encoding-job).

### 全域套用視訊設定檔 {#applying-a-video-profile-globally}

除了將設定檔套用至資料夾之外，您也可以全域套用一個設定檔，讓任何資料夾中上傳至Experience Manager Assets的任何內容都已套用選取的設定檔。

另請參閱 [編輯資料夾中的資產處理設定檔後，重新處理該資料夾中的資產](processing-profiles.md#reprocessing-assets).

**若要全域套用視訊設定檔：**

* 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`. 新增屬性 `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` 選取 **[!UICONTROL 全部儲存]**.

   ![chlimage_1-519](assets/chlimage_1-519.png)
* 您可以 [監視視訊設定檔處理作業的進度](#monitoring-the-progress-of-an-encoding-job).

## 監視視訊設定檔處理工作的進度 {#monitoring-the-progress-of-an-encoding-job}

會顯示處理指標（或進度列），以便您以視覺化方式監控視訊設定檔處理工作的進度。

您也可以檢視 `error.log` 檔案，監視編碼作業的進度、查看編碼是否已完成，或查看任何作業錯誤。 此 `error.log` 在中找到 `logs` 安裝Experience Manager例項的資料夾。

## 從資料夾移除視訊描述檔 {#removing-a-video-profile-from-folders}

從資料夾移除視訊描述檔時，任何子資料夾都會自動從其父資料夾移除描述檔。 不過，資料夾內發生的檔案處理仍維持不變。

您可以從「工具」功能表內的資料夾或在資料夾內的「資料夾設定」中移除視訊描述檔 ********。本節說明如何以兩種方式從資料夾移除視訊描述檔。

### 透過「描述檔」使用者介面，從資料夾中移除視訊描述檔 {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 選取您要從資料夾或多個資料夾中移除的視訊設定檔。
1. 選擇 **[!UICONTROL 從資料夾中刪除配置檔案]** ，然後選擇要用於從中刪除配置檔案的資料夾或多個資料夾，並選擇 **[!UICONTROL 移除]**.

   您可以確認視訊描述檔不再套用至資料夾，因為資料夾名稱下方不再顯示該名稱。

### 透過「屬性」從資料夾中移除視訊描述檔 {#removing-video-profiles-from-folders-by-way-of-properties}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]** 然後，移至您要從中移除視訊描述檔的資料夾。
1. 在資料夾中，選取核取記號，然後選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL 視訊設定檔]** 索引標籤和選取 **[!UICONTROL 無]** 從下拉式選單中選取 **[!UICONTROL 儲存並關閉]**. 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
