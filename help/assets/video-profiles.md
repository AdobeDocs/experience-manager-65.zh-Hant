---
title: 視訊設定檔
description: 動態媒體已隨附預先定義的最適化視訊編碼設定檔。 此現成可用的設定檔中的設定已最佳化，讓客戶獲得最佳的檢視體驗。 您也可以將智慧裁切新增至影片。
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
translation-type: tm+mt
source-git-commit: 569c552686e6312ecae0d500147a8b65354c303d

---


# Video profiles {#video-profiles}

動態媒體已隨附預先定義的最適化視訊編碼設定檔。 此現成可用的設定檔中的設定已最佳化，讓客戶獲得最佳的檢視體驗。 當您使用「最適化視訊編碼」設定檔來編碼主視訊時，視訊播放器會在播放期間根據客戶的網際網路連線速度自動調整視訊串流的品質。 這稱為可調式串流。

以下是決定影片品質的其他因素：

* **已上傳主影片的解析度**

   如果MP4視訊是以較低的解析度（例如240p或360p）錄制，就無法以高解析度串流。

* **視訊播放器大小**

   依預設，「最適化視訊編碼」描述檔中的「寬度」會設為「自動」。同樣地，在播放期間，會根據播放器的大小來使用最佳品質。

請參 [閱視訊編碼的最佳實務](/help/assets/video.md#best-practices-for-encoding-videos)。

另請參閱 [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md)。

>[!NOTE]
>
>若要產生視訊的中繼資料和相關的視訊影像縮圖，視訊本身需要在動態媒體中執行編碼程式。 在AEM中，如果您已啟用動態媒 **** 體並設定視訊雲端服務，「動態媒體編碼視訊」工作流程會對視訊進行編碼。 此工作流程會擷取工作流程處理歷程記錄和失敗資訊。 請參閱 [監控視訊編碼和YouTube發佈進度](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress)。 如果您已啟用動態媒體並設定視訊雲端服務，當您上傳視訊時，「動態媒體編碼視訊 **** 」工作流程會自動生效。 (如果您未使用動態媒體， **[!UICONTROL DAM更新資產工作流程將生效]** 。)
>
>在搜尋資產時，中繼資料很實用。 縮圖是編碼期間產生的靜態視訊影像。 AEM系統需要這些視訊，並用於使用者介面，以協助您在「卡片」檢視、「搜尋結果」檢視和「資產清單」檢視中以視覺化方式識別視訊。 當您點選編碼視訊的「轉譯」圖示（畫家的浮動視窗）時，可看到產生的縮圖。

完成視訊描述檔的建立後，即可將它套用至資料夾或多個資料夾。 請參 [閱將視訊描述檔套用至資料夾。](#applying-a-video-profile-to-folders)

要定義其他資產類型的高級處理參數，請參 [閱配置資產處理](/help/assets/config-dms7.md#configuring-asset-processing)。

另請參閱 [處理中繼資料、影像和視訊的設定檔](processing-profiles.md)。

## 最適化視訊編碼預設集 {#adaptive-video-encoding-presets}

下表列出最佳實務編碼設定檔，以針對行動與平板電腦裝置以及桌上型電腦進行最適化視訊串流。 您可將這些預設集用於任何外觀比例視訊。

<table>
 <tbody>
  <tr>
   <td><strong>視訊格式轉碼器</strong></td>
   <td><strong>視訊大小——寬度(px)</strong></td>
   <td><strong>視訊大小——高度(px)</strong></td>
   <td><strong>保持長寬比？</strong></td>
   <td><strong>視訊位元速率(Kbps)</strong></td>
   <td><strong>視訊影格速率(Fps)</strong></td>
   <td><strong>音訊轉碼器</strong></td>
   <td><strong>音訊位元速率(Kbps)</strong></td>
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

## 關於在視訊描述檔中使用智慧裁切 {#about-smart-crop-video}

智慧型裁切視訊（視訊描述檔中的選用功能）是一種工具，可運用Adobe Sensei中的人工智慧功能，自動偵測並裁切您上傳的任何最適化視訊或漸進式視訊中的焦點，不論其大小。

智慧型裁切支援的視訊格式包括MP4、MKV、MOV、AVI、FLV和WMV。

智慧型裁切支援的視訊檔案大小上限如下：

* 持續5分鐘。
* 每秒30幀(FPS)。
* 300 MB檔案大小。

請注意，Adobe Sensei目前限制為9000個影格。 也就是說，在30 FPS時5分鐘。 如果您的視訊的FPS較高，則支援的視訊持續時間上限會降低。 例如，60 FPS視訊的長度必須為2.5分鐘，Adobe Sensai和智慧型裁切才能支援。

![智慧型裁切視訊](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>若要智慧型視訊裁切，您必須在視訊描述檔中加入一或多個視訊編碼預設集。

若要使用智慧型裁切來進行視訊，請建立最適化或漸進式視訊編碼設定檔。 在描述檔中，使用智慧型裁 **[!UICONTROL 切比例工具]** ，選取預先定義的外觀比例。 例如，在定義視訊編碼預設集後，您可以新增「行動橫向」定義（外觀比例為16x9）和「行動縱向」定義（外觀比例為9x16）。 您可選擇的其他外觀或裁切比例包括1x1、4x3和4x5。

![使用智慧裁切編輯視訊編碼設定檔](assets/edit-smart-crop-video2.png)

請注意，您可以使用使用者介面中「智慧型裁切比例」最右側的滑桿，將視訊描述檔中的視訊智慧型裁切切換為開啟或關閉 **** 。

建立並儲存視訊描述檔後，您可以將它套用至所需的資料夾。

請參 [閱將視訊描述檔套用至特定資料夾](#applying-video-profiles-to-specific-folders) ，或 [全域套用視訊描述檔](#applying-a-video-profile-globally)。

另請參閱 [智慧型影像裁切](image-profiles.md)。

## 建立視訊描述檔以進行最適化串流 {#creating-a-video-encoding-profile-for-adaptive-streaming}

動態媒體已隨附預先定義的最適化視訊編碼設定檔- MP4 H.264的視訊上傳設定群組——已最佳化，以提供最佳的檢視體驗。 您可以在上傳影片時使用此設定檔。

不過，如果此預先定義的描述檔不符合您的需求，您可以選擇建立自己的最適化視訊編碼描述檔。 當您使用最適化串流的 **[!UICONTROL Encode（編碼）設定]**-作為最佳實務——您新增至描述檔的所有編碼預設集都會經過驗證，以確保所有視訊都有相同的外觀比例。 此外，編碼視訊會視為串流的多位元速率集。

當您建立視訊編碼設定檔時，會注意到大部分的編碼選項都已預先填入建議的預設設定，以協助您。 不過，如果您選取的值不是建議的預設值，請注意，這可能會在播放時造成視訊品質不佳，以及其他效能問題。

因此，針對描述檔中的所有MP4 H.264視訊編碼預設集，會驗證下列值，以確保這些值在描述檔中的個別編碼預設集上都相同，進而提供最適化串流功能：

* 視訊格式轉碼器- MP4 H.264(.mp4)
* 音訊轉碼器
* 音訊位元速率
* 保持高寬比
* 兩遍編碼
* 固定位元速率
* H264 設定檔
* 音訊取樣速率

如果值不相同，則可以繼續按原樣建立配置檔案。 不過，請注意，不可能進行自適應串流。 使用者將可體驗單位元速率串流。 建議您編輯編碼設定，以便在描述檔中的個別編碼預設集間使用相同的值。 （請注意，如果已啟用「最適化串流編碼」，視訊設定檔／預設集編輯器應強制同等使用最適化視訊編碼設定。）

另請參閱 [建立漸進式串流的視訊編碼設定檔](#creating-a-video-encoding-profile-for-progressive-streaming)。

另請參閱 [視訊編碼的最佳實務](/help/assets/video.md#best-practices-for-encoding-videos)。

要定義其他資產類型的高級處理參數，請參 [閱配置資產處理](/help/assets/config-dms7.md#configuring-asset-processing)。

**若要建立視訊描述檔以進行最適化串流**,

1. 點選AEM標誌並導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL 資產]** >視 **[!UICONTROL 訊設定檔]**」。
1. 按一下或點選「 **[!UICONTROL 建立]** 」以新增視訊設定檔。

1. 輸入配置檔案的名稱和說明。
1. 在「建立／編輯視訊編碼預設集」頁面上，點選「 **[!UICONTROL 新增視訊編碼預設集」]**。
1. 在「基 **[!UICONTROL 本]** 」標籤上，設定視訊和音訊選項。
請點選每個選項旁的資訊圖示，以根據選取的視訊格式codec取得其他說明或建議的設定。
1. 在「Video Size（視訊大小）」標題下，確保已 **[!UICONTROL 勾選「Keep aspect]** ratio（保持外觀比例）」。
1. 設定視訊影格大小解析度（以像素為單位）。 使用「 **[!UICONTROL 自動]** 」值可自動縮放以符合來源長寬比（寬高比）。 例如，「自動x 480」或「640 x自動」。

1. 執行下列任一項作業：

   * 在「寬 **[!UICONTROL 度]** 」欄位中輸 **[!UICONTROL 入auto]**。 在「高 **[!UICONTROL 度]** 」欄位中，輸入像素值。

   * 若要協助您視覺化視訊的大小，請點選 **[!UICONTROL Height右側的資訊圖示(i)]** ，以開啟「大小計算器」頁面。 使用 **[!UICONTROL 大小計算器]** ，設定您想要的視訊尺寸（由藍色方塊表示）。 完成 **[!UICONTROL 時]** ，點選右上角的X。

1. （可選）點選「進階 **[!UICONTROL 」標籤]** ，並確定已選 **[!UICONTROL 取「使用預設值]** 」核取方塊（建議）。 或者，修改進階的視訊和音訊設定。
1. 在頁面的右上角，點選「儲 **[!UICONTROL 存]** 」以儲存預設集。
1. 執行下列任一項作業：
   * 重複步驟4-10以建立其他編碼預設集。 （最適化視訊串流需要多個視訊預設集。）
   * 繼續下一步。

1. （可選）若要將視訊智慧型裁切新增至將套用此設定檔的視訊，請執行下列動作：
   * 在「編輯視訊描述檔」頁面的「智慧型裁切比例」標題右側，點選「新增 **[!UICONTROL 」]**。
   * 在「名稱」欄位中，輸入裁切比例的名稱，以協助您輕鬆識別。
   * 從「裁 **[!UICONTROL 切比例]** 」下拉式清單中，選取您要使用的比例。

1. 執行下列任一項作業：

   * 視需要繼續新增裁切比例。
   * 繼續下一步。

1. 在頁面的右上角，再點選「 **[!UICONTROL Save]** 」以儲存描述檔。

您現在可以將描述檔套用至包含影片的檔案夾。 請參 [閱將視訊描述檔套用至資料夾](#applying-a-video-profile-to-folders) , [或全域套用視訊描述檔](#applying-a-video-profile-globally)。

## 建立漸進式串流的視訊設定檔 {#creating-a-video-encoding-profile-for-progressive-streaming}

如果您選擇不使用「編碼」選項進行最適化串流 ****，請注意，您新增至描述檔的所有編碼預設集都會被視為個別視訊轉譯，以用於單位元速率串流或漸進式視訊傳送。 此外，沒有驗證可確保所有視訊轉譯具有相同的外觀比例。

視您執行的模式而定，支援的視訊格式轉碼器如下：

* 動態媒體——場景7模式：H.264(.mp4)
* 動態媒體——混合模式：H.264(.mp4)、WebM

另請參閱 [建立適應性串流的視訊編碼設定檔](#creating-a-video-encoding-profile-for-adaptive-streaming)。

另請參閱 [視訊編碼的最佳實務](/help/assets/video.md#best-practices-for-encoding-videos)。

要定義其他資產類型的高級處理參數，請參 [閱配置資產處理](/help/assets/config-dms7.md#configuring-asset-processing)。

**若要建立漸進式串流的視訊設定檔：**

1. 點選AEM標誌並導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL 資產]** >視 **[!UICONTROL 訊設定檔]**」。
1. 點選「 **[!UICONTROL 建立]** 」以新增視訊設定檔。
1. 輸入配置檔案的名稱和說明。
1. 在「建立／編輯視訊編碼預設集」頁面上，點選「 **[!UICONTROL 新增視訊編碼預設集」]**。
1. 在「基 **[!UICONTROL 本]** 」標籤上，設定視訊和音訊選項。
請點選每個選項旁的資訊圖示，以根據選取的視訊格式codec取得其他說明或建議的設定。
1. （可選）在「Video Size（視訊大小）」標題下，取消勾選「 **[!UICONTROL Keep aspect ratio（保留外觀比例）]**」。
1. 執行下列動作：
   * 在「寬 **[!UICONTROL 度]** 」欄位中輸 **[!UICONTROL 入auto]**。
   * 在「高 **[!UICONTROL 度]** 」欄位中，輸入像素值。
若要協助您視覺化視訊的大小，請點選「高度」的資訊圖示以開啟「大小計 **[!UICONTROL 算器]** 」頁面。 使用「 **[!UICONTROL 大小計算器]** 」頁可以進一步設定視頻尺寸（藍色框）。 完成後，在對話框的右上角點選 **[!UICONTROL X]**。
1. （可選）執行下列任一項作業：

   * 點選「 **[!UICONTROL 進階]** 」標籤，並確定已選 **[!UICONTROL 取「使用預設值]** 」核取方塊（建議）。

   * 清除「 **[!UICONTROL 使用預設值]** 」核取方塊，並指定您要的視訊設定和音訊設定。
請點選每個選項旁的資訊圖示，以根據選取的視訊格式codec取得其他說明或建議的設定。

1. 在頁面的右上角，點選「儲 **[!UICONTROL 存]** 」以儲存預設集。
1. 執行下列任一項作業：

   * 重複步驟4-9以建立其他編碼預設集。
   * 繼續下一步。

1. （可選）若要將視訊智慧型裁切新增至將套用此設定檔的視訊，請執行下列動作：

   * 在「編輯視訊描述檔」頁面的「智慧型裁切比例」標題右側，點選「新增 **[!UICONTROL 」]**。
   * 在「名稱」欄位中，輸入裁切比例的名稱，以協助您輕鬆識別。
   * 從「裁 **[!UICONTROL 切比例]** 」下拉式清單中，選取您要使用的比例。

1. 執行下列任一項作業：

   * 視需要繼續新增裁切比例。
   * 繼續下一步。

1. 在頁面的右上角，點選「儲存 **** 」以儲存描述檔。

您現在可以將描述檔套用至包含影片的檔案夾。 請參 [閱將視訊描述檔套用至資料夾](#applying-a-video-profile-to-folders) , [或全域套用視訊描述檔](#applying-a-video-profile-globally)。

## 使用自訂新增的視訊編碼參數 {#using-custom-added-video-encoding-parameters}

您可以編輯現有的視訊編碼設定檔，以利用在AEM中建立或編輯視訊設定檔時，使用者介面中找不到的進階視訊編碼參數。 您可自訂將一或多個進階參數（例如minBitrate和maxBitrate）新增至現有的描述檔。

**若要使用自訂新增的視訊編碼參數**:

1. 點選AEM標誌，然後導覽至「工 **[!UICONTROL 具]** >一 **[!UICONTROL 般]** > **[!UICONTROL CRXDE Lite]**」。
1. 從CRXDE Lite頁面，在左側的「檔案總管」面板中，導覽至下列：

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
   <td>用於編碼的H.264層級。 這通常會根據您使用的編碼設定自動決定。</td>
   <td><code>String</code></td>
   <td><p>10 * h264級</p> <p>例如，3.0 = 30,1.3 = 13)</p> <p>無預設值。</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>關鍵影格之間的影格目標數目。 計算此值，每2-10秒產生一個關鍵影格。 例如，每秒30幀，關鍵幀間隔應為60-300。<br /> 較低 <br /> 的關鍵影格間隔可改善最適化視訊編碼的串流搜尋和串流切換行為，也可改善具有大量動作的視訊品質。 不過，由於關鍵影格會增加檔案大小，因此較低的關鍵影格間隔通常會導致特定位元速率的整體視訊品質較低。</td>
   <td><code>String</code></td>
   <td><p>正數。</p> <p>預設值為300。</p> <p>HLS（HTTP即時串流）的建議值為60-90。</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>允許可變位元速率編碼的最小位元速率，以Kbps（每秒千位）為單位。</p> <p>只有在您建立或編輯視訊編碼描述檔時<strong></strong> ，在「進階」索引標籤中取消選取「使用常數位元速率」時，才會套用此參數。</p> <p>另請參閱 <a href="/help/assets/video.md#bitrate">位元速率</a>。</p> </td>
   <td><code>String</code></td>
   <td><p>正數，以Kbps為單位。</p> <p>無預設值。</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>允許以Kbps為單位的可變位元速率編碼的最大位元速率。</p> <p>只有在您建立或編輯視訊編碼描述檔時<strong></strong> ，在「進階」索引標籤中取消選取「使用常數位元速率」時，才會套用此參數。</p> <p>另請參閱 <a href="/help/assets/video.md#bitrate">位元速率</a>。</p> </td>
   <td><code>String</code></td>
   <td><p>正數，以Kbps為單位。</p> <p>無預設值。 不過，建議的值是編碼位元速率的兩倍。</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>如果音訊轉 <code>true</code> 碼器支援，請將值設為強制音訊串流的恆定位元速率。</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>預設為 <code>false</code>。</p> <p>HLS（HTTP即時串流）的建議值為 <code>false</code>。</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. 在頁面的右下角附近，點選「新增 **[!UICONTROL 」]**。
1. 執行下列任一項作業：

   * 重複步驟3和4，將另一個參數新增至視訊編碼設定檔。
   * 在頁面左上角附近，點選「全 **[!UICONTROL 部儲存」]**。

1. 在CRXDE Lite頁面的左上角，點選「 **[!UICONTROL Back Home]** 」（返回首頁）圖示以返回AEM。

### 編輯視訊設定檔 {#editing-a-video-encoding-profile}

您可以編輯您建立的任何視訊設定檔，以新增、編輯或刪除該設定檔中的視訊預設集。

依預設，您無法編輯動態媒體隨附的預先定 **[!UICONTROL 義、立即可用的最適化視訊編碼]** 。 您可以輕鬆地複製描述檔，並使用新名稱加以儲存。 然後，您可以在複製的描述檔中編輯所需的預設集。

另請參閱 [視訊編碼的最佳實務](/help/assets/video.md#best-practices-for-encoding-videos)。

要定義其他資產類型的高級處理參數，請參 [閱配置資產處理](/help/assets/config-dms7.md#configuring-asset-processing)。

**要編輯視頻配置檔案**:

1. 點選AEM標誌並導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL 資產]** >視 **[!UICONTROL 訊設定檔]**」。
1. 在「視訊描述檔」頁面上，勾選一個視訊描述檔名稱。
1. 在工具列上，點選「 **[!UICONTROL 編輯」]**。
1. 在「視訊編碼描述檔」頁面上，視需要編輯名稱和說明。
1. 最佳實務是，請確定已選取「 **[!UICONTROL 最適化串流編碼]** 」核取方塊。
點選資訊圖示以取得最適化串流的說明。 （如果您正在編輯漸進式視訊設定檔，請勿選取此核取方塊）。
1. 在「視訊編碼預設集」標題下，新增、編輯或刪除構成描述檔的視訊編碼預設集。

   請點選「基本」和「進階」標籤上每個選項旁的資訊圖示，以取得其他說明或根據選取的視訊格式codec建議的設定。 ********

1. 在頁面的右上角，點選「儲存 **[!UICONTROL 」]**。

### 複製視訊設定檔 {#copying-a-video-encoding-profile}

1. 點選AEM標誌並導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL 資產]** >視 **[!UICONTROL 訊設定檔]**」。
1. 在「視訊描述檔」頁面上，勾選一個視訊描述檔名稱。
1. 在工具列上，點選「 **[!UICONTROL 複製」]**。
1. 在「視訊編碼描述檔」頁面上，輸入描述檔的新名稱。
1. 最佳實務是，請確定已選取「 **[!UICONTROL 最適化串流編碼]** 」核取方塊。 點選資訊圖示以取得最適化串流的說明。 （如果您要複製漸進式視訊設定檔，請勿選取核取方塊。）

   在「動態媒體——混合」模式中，如果WebM視訊預設集是視訊設定檔的一部分，則無法進行「 **[!UICONTROL Encode for adaptive streaming]** 」，因為所有預設集都必須是MP4。
1. 在「視訊編碼預設集」標題下，新增、編輯或刪除構成描述檔的視訊編碼預設集。

   點選「基本」和「進階」標籤上每個選項旁的資訊圖示，以取得建議的設定和說明。

1. 在頁面的右上角，點選「儲存 **[!UICONTROL 」]**。

### 刪除視訊設定檔 {#deleting-a-video-encoding-profile}

1. 點選AEM標誌並導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL 資產]** >視 **[!UICONTROL 訊設定檔]**」。
1. 在「視訊描述檔」頁面上，勾選一或多個視訊描述檔名稱。
1. 在工具列上，點選「 **[!UICONTROL 刪除」]**。
1. 點選「 **[!UICONTROL 確定]**」。

## 將視訊描述檔套用至資料夾 {#applying-a-video-profile-to-folders}

將視訊描述檔指派給檔案夾時，任何子檔案夾都會自動從其父檔案夾繼承描述檔。 這表示您只能將一個視訊描述檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的檔案夾結構。

如果您指派不同的視訊描述檔給資料夾，新的描述檔會覆寫先前的描述檔。 舊有的資料夾資產仍維持不變。 新的描述檔會套用至稍後新增至資料夾的資產。

在用戶介面中，配置了配置檔案的資料夾將通過卡名稱中顯示的配置檔案的名稱來表示。

![chlimage_1-517](assets/chlimage_1-517.png)

您可以將視訊描述檔套用至特定資料夾，或全域套用至所有資產。

您可以重新處理已有現有視訊設定檔的資料夾中的資產，您稍後會加以變更。 請參 [閱編輯資料夾的處理設定檔後，重新處理資產](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile)。

### 將視訊描述檔套用至特定資料夾 {#applying-video-profiles-to-specific-folders}

您可以從「工具」菜單或在資料夾中從「屬性」將視頻配置檔案應 **[!UICONTROL 用到資料夾]******。 本節說明如何以兩種方式將視訊描述檔套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

另請參閱 [編輯資料夾的處理設定檔後重新處理資產](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile)。

#### 透過描述檔使用者介面，將視訊描述檔套用至資料夾 {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. 點選AEM標誌並導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL 資產]** >視 **[!UICONTROL 訊設定檔]**」。
1. 選擇要應用於資料夾或多個資料夾的視頻配置檔案。
1. 點選 **[!UICONTROL 「將描述檔套用至檔案夾」]** ，然後選取您要用來接收新上傳資產的檔案夾或多個檔案夾，並點選「套 **[!UICONTROL 用」]**。 在「卡片檢視」中，資料夾名稱正下方會顯示資料夾名稱，以指出已指派給資料夾的 **[!UICONTROL 資料夾]**。
您可以 [監控視訊描述檔處理工作的進度](#monitoring-the-progress-of-an-encoding-job)。

#### 從「屬性」將視訊描述檔套用至資料夾 {#applying-video-profiles-to-folders-from-properties}

1. 點選或按一下AEM標誌，並導覽至 **[!UICONTROL Assets]** ，然後導覽至您要套用視訊描述檔的檔案夾。
1. 在資料夾上，點選核取標籤以選取它，然後點選「 **[!UICONTROL 屬性]**」。
1. 選擇「 **[!UICONTROL 視訊描述檔]** 」標籤，然後從下拉式選單中選取描述檔，然後按一下「 **[!UICONTROL 儲存並關閉」]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

   ![chlimage_1-518您](assets/chlimage_1-518.png)可以 [監控視訊描述檔處理工作的進度](#monitoring-the-progress-of-an-encoding-job)。

### 全域套用視訊設定檔 {#applying-a-video-profile-globally}

除了將描述檔套用至檔案夾外，您也可以全域套用一個，如此任何檔案夾中上傳至AEM資產的內容都會套用選取的描述檔。

另請參閱 [編輯資料夾的處理設定檔後重新處理資產](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile)。

**若要全域套用視訊設定檔**,

* 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`。 新增屬性並 `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` 點選「 **[!UICONTROL 全部儲存」]**。

   ![chlimage_1-519](assets/chlimage_1-519.png)
* 您可以 [監控視訊描述檔處理工作的進度](#monitoring-the-progress-of-an-encoding-job)。

## 監控視訊描述檔處理工作的進度 {#monitoring-the-progress-of-an-encoding-job}

顯示處理指示器（或進度列），以便您能夠直觀地監視視頻配置檔案處理作業的進度。

您也可以檢視檔 `error.log` 案，以監控編碼工作的進度、查看編碼是否完成，或查看任何工作錯誤。 您 `error.log` 可在安裝AEM `logs` 實例的資料夾中找到。

## 從資料夾移除視訊描述檔 {#removing-a-video-profile-from-folders}

從資料夾中刪除視頻配置檔案時，任何子資料夾都會自動繼承從其父資料夾中刪除的配置檔案。 不過，對檔案夾中發生的檔案處理仍維持不變。

您可以從「工具」功能表內的資料夾或在資料夾內的「資料夾設定」中移除視訊描述檔 ********。 本節說明如何以兩種方式從資料夾移除視訊描述檔。

### 透過描述檔使用者介面，從資料夾移除視訊描述檔 {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. 點選AEM標誌並導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL 資產]** >視 **[!UICONTROL 訊設定檔]**」。
1. 選擇要從資料夾或多個資料夾中刪除的視頻配置檔案。
1. 點選 **[!UICONTROL 「從檔案夾移除描述檔]** 」，然後選取您要用來從中移除描述檔的檔案夾或多個檔案夾，並點選「 **[!UICONTROL 移除」]**。

   您可以確認視訊描述檔不再套用至資料夾，因為檔案夾名稱下方不會再顯示該名稱。

### 透過「屬性」從資料夾移除視訊描述檔 {#removing-video-profiles-from-folders-by-way-of-properties}

1. 點選或按一下AEM標誌，並導覽至 **[!UICONTROL Assets]** ，然後導覽至您要從中移除視訊描述檔的檔案夾。
1. 在資料夾上點選或按一下核取標籤以選取它，然後點選或按一下「 **屬性」**。
1. 選擇「 **[!UICONTROL 視訊描述檔]** 」標籤，並從下拉式選單中選 **[!UICONTROL 取「無]** 」，然後按一下「 **[!UICONTROL 儲存並關閉」]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

