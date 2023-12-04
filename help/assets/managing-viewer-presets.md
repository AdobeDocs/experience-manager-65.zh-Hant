---
title: 管理檢視器預設集
description: 如何在Dynamic Media中建立、編輯及管理檢視器預設集。
uuid: 64fcf16a-7c4a-435b-bf1a-f27b8b39a715
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cf7823f4-82c2-4e36-9b65-3c58359b8104
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
feature: Viewer Presets
role: User, Admin
exl-id: 0899e497-88e9-4fc3-a6be-b3a149fb5b32
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '4422'
ht-degree: 8%

---

# 管理檢視器預設集{#managing-viewer-presets}

檢視器預設集是一組設定，可決定使用者如何在電腦熒幕和行動裝置上檢視多媒體資產。 如果您是管理員，可以建立檢視器預設集。 設定可供一系列檢視器組態選項使用。 例如，您可以變更檢視器的顯示大小或縮放行為。

如需建立和自訂HTML5檢視器預設集的指示，請參閱AdobeDynamic Media *HTML5檢視器SDK API檔案*. SDK可在內嵌於SDK本身的IS發佈伺服器上使用。 每個程式庫版本都有各自的SDK檔案。

路徑： `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.\
例如，3.10 SDK： [https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)

另請參閱 [Adobe Dynamic Media檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

本節說明如何建立、編輯及管理檢視器預設集。 您可以隨時將檢視器預設集套用至資產，進行預覽。 另請參閱 [套用檢視器預設集](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>編輯任何 *預先定義的現成檢視器預設集* 不支援的情況。 如果您嘗試編輯現成的檢視器預設集，系統會提示您使用新名稱儲存檢視器預設集。

## 檢視器的鍵盤協助工具 {#keyboard-accessibility-for-viewers}

所有現成的檢視器都支援鍵盤協助工具。

另請參閱 [鍵盤協助工具和導覽](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html).

## 管理檢視器預設集 {#managing-viewer-presets-1}

您可以點選，在Adobe Experience Manager中新增、編輯、刪除、發佈、取消發佈和預覽檢視器預設集 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>依預設，當您在資產的詳細資料檢視中選取「檢視器」時，系統會顯示15個檢視器預設集。 您可以提高此限制。請參 [閱增加顯示的檢視器預設集數目](#increasing-the-number-of-viewer-presets-that-display)。

### 檢視器支援回應式設計網頁 {#viewer-support-for-responsive-designed-web-pages}

不同的網頁有不同的需求。 例如，有時您會想要網頁提供連結，在個別瀏覽器視窗中開啟HTML5檢視器。 在其他情況下，您可能需要直接將HTML5檢視器內嵌在託管頁面上。 在後一種情況下，網頁可能會有靜態配置。 或是「回應式」的網頁，在不同裝置或不同瀏覽器視窗大小上的顯示會有所不同。 為因應這些需求，Dynamic Media隨附的所有預先定義、現成可用的HTML5檢視器都支援靜態網頁和回應式設計網頁。

另請參閱 [Responsive影像資料庫](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html) 以取得有關如何將回應式檢視器內嵌至網頁的詳細資訊。

>[!NOTE]
>
>首次使用現成可用的檢視器之前，請先發佈這些檢視器。
>另請參閱 [發佈檢視器預設集].(#publishing-viewer-presets)

### 檢視器預設集系統相容性 {#viewer-preset-system-compatibility}

Dynamic Media隨附的所有現成可用的檢視器預設集都與下列系統完全相容：

* 桌上型
* Apple iPhone
* Apple iPad
* Android™智慧型手機
* Android™平板電腦
* 視訊額外支援MP4播放 [BlackBerry®](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) 和 [Windows Phone](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs).

### 檢視器預設集的豐富媒體型別 {#rich-media-types-for-viewer-presets}

管理員可在建立檢視器預設集時新增及自訂下列多媒體型別。

<table>
 <tbody>
  <tr>
   <td><strong>傳送集</strong><br /> </td>
   <td><p>將熱點或影像地圖（或兩者）新增到兩個或多個影像的序列。 客戶可以將影像向左或向右平移，然後在影像上選取熱點，以取得其他詳細資訊或直接從網站的類別、首頁或登陸頁面購買。</p> </td>
  </tr>
  <tr>
   <td><strong>維度</strong><br /> </td>
   <td><p>顯示可讓您旋轉、平移、縮放或重新置入相機的3D場景。</p> </td>
  </tr>
  <tr>
   <td><strong>彈出式縮放</strong></td>
   <td><p>在原始影像旁顯示縮放區域的第二個影像。 沒有要使用的控制項 — 使用者將選取範圍移動到他們想要檢視的區域。</p> <p>判斷此檢視器的完整頻寬使用量時，請考量檢視器中會提供主要影像和彈出式影像。 主要影像大小（「舞台寬度」和「高度」）和「縮放因數」決定彈出式影像大小。 若要防止彈出式檔案變得太大，請平衡這兩個值：如果主要影像大小很大，請降低「縮放因數」值。 （「彈出式寬度」和「彈出式高度」決定彈出式視窗的大小，但不是提供給檢視器的彈出式影像大小。）</p> <p>例如，如果您的主要影像大小是350 x 350畫素，而「縮放因數」為3，則產生的彈出式影像是1050 x 1050畫素。 如果您的主要影像大小是300 x 300畫素，縮放因數為4，則彈出式影像是1200 x 1200畫素。 根據JPEG品質設定（建議的設定介於80到90之間），您可以大幅減少檔案大小。 建議的縮放因數為2.5至4，視您的主影像大小而定。</p> </td>
  </tr>
  <tr>
   <td><strong>內嵌縮放</strong></td>
   <td>在原始檢視器中顯示縮放區域的影像。 沒有要使用的控制項。 也就是說，使用者將選取範圍移至要檢視的區域。</td>
  </tr>
  <tr>
   <td><strong>影像集</strong></td>
   <td>在「影像集」檢視器中，使用者可以透過選取縮圖影像來檢視專案的不同檢視或色彩變化。 此檢視器也提供縮放工具，以便更密切地檢查影像。</td>
  </tr>
  <tr>
   <td><strong>互動影像</strong></td>
   <td>熱點會新增至影像部分，然後客戶可選取這些部分以取得其他詳細資訊，或直接從網站的類別、首頁或登入頁面購買。</td>
  </tr>
  <tr>
   <td><strong>互動視訊</strong></td>
   <td>縮圖會新增至影片中的時間軸區段，然後客戶可選取該區段以取得其他詳細資訊，或直接從網站的類別、首頁或登入頁面購買。</td>
  </tr>
  <tr>
   <td><strong>混合媒體</strong></td>
   <td>在一個檢視器中顯示不同型別的媒體。 您可以包含迴轉集、影像集、影像和視訊。</td>
  </tr>
  <tr>
   <td><strong>全景影像</strong></td>
   <td><p>「全景影像」和「全景VR」檢視器可呈現球狀全景影像，讓使用者沈浸在房間、屬性、位置或橫向的360度檢視體驗中。</p> <p>若要讓上傳的影像符合球面全景的條件，該影像必須具備下列其中一項或兩項：</p>
    <ul>
     <li>外觀比例為2:1。</li>
     <li>以關鍵字標籤 <code>equirectangular</code>，或 <code>spherical</code> 和 <code>panorama</code>，或 <code>spherical </code>和 <code>panoramic</code>. 另請參閱 <a href="/help/sites-authoring/tags.md">使用標籤</a>.</li>
    </ul> <p>外觀比例和關鍵字條件都適用於資產詳細資料頁面和「全景媒體」WCM元件的全景資產。</p> <p><strong>重要</strong>：此檢視器僅適用於Dynamic Media - Scene7模式。</p> </td>
  </tr>
  <tr>
   <td><strong>智慧型裁切視訊</strong><br /> </td>
   <td><p>使用此檢視器自動偵測並裁切至任何視訊中的焦點。</p> </td>
  </tr>
  <tr>
   <td><strong>迴轉集</strong></td>
   <td>提供影像的多個檢視，讓使用者可以轉動物件來檢查不同的側邊和角度。</td>
  </tr>
  <tr>
   <td><strong>360度影片</strong></td>
   <td><p>使用360/VR視訊檢視器可呈現等矩形的視訊，呈現房間、屬性、位置、橫向或醫療程式的沈浸式檢視體驗。</p> <p>在平面顯示器上播放期間，使用者可以控制視角；在行動裝置上播放通常會套用其內建的陀螺儀控制項。</p> <p>檢視器包含原生支援，可傳送360個視訊資產。 依預設，檢視或播放時不需要額外的設定。 您可使用標準視訊副檔名（例如.mp4、.mkv和.mov）來傳送360視訊。 最常見的轉碼器是H.264。</p> <p><strong>重要</strong>：此檢視器僅適用於Dynamic Media - Scene7模式。</p> </td>
  </tr>
  <tr>
   <td><strong>影片</strong></td>
   <td><p>使用漸進式或自我調整位元速率串流播放視訊。 最適化位元速率串流會自動執行裝置和頻寬偵測，以正確格式提供正確品質的視訊。</p> </td>
  </tr>
  <tr>
   <td><strong>垂直縮放</strong></td>
   <td><p>垂直縮放檢視器可讓您最大化產品影像檢視體驗，讓使用者獲得產品的最佳表示方式。 色票的垂直位置會執行下列動作：</p>
    <ul>
     <li>確保色票「高於摺頁」。<br/> 使用水準色票時，除非使用者向下捲動頁面，否則不會顯示水準色票（視使用者的案頭熒幕大小而定）。 將色票垂直放置在檢視器中，可確保無論使用者的熒幕大小如何，都能看見色票。</li>
     <li>將主要影像大小最大化。<br /> 使用水準色票時，必須在頁面上保留空間，以確保可看見色票。 此定位縮小了主要影像的大小。 然而，若是垂直色票版面配置，您就不需要配置此空間。 因此，您可以將主要影像大小最大化。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>縮放</strong></td>
   <td>可讓使用者透過選取區域來放大該區域。 使用者可以選取控制項來放大、縮小影像，以及將影像重設為預設大小。</td>
  </tr>
 </tbody>
</table>

### 現成可用的檢視器預設集清單 {#list-of-out-of-the-box-viewer-presets}

下表列出Dynamic Media隨附的所有預先定義、現成可用的檢視器預設集。

另請參閱 [即時示範](https://landing.adobe.com/tw/na/dynamic-media/ctir-2755/live-demos.html).

如需有關檢視器支援的網頁瀏覽器和作業系統版本的資訊，您可以檢閱「檢視器發行說明」。

請參閱目錄中的「檢視器發行說明」。 [檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

>[!NOTE]
>
>Dynamic Media中的所有現成可用的檢視器預設集都已啟動（開啟），但您必須發佈它們。
>另請參閱 [發佈檢視器預設集](#publishing-viewer-presets).
>
>您建立和新增的任何新檢視器預設集都必須同時啟動*和*已發佈。
>另請參閱 [啟用或停用檢視器預設集](#activating-or-deactivating-viewer-presets) 和 [發佈檢視器預設集](#publishing-viewer-presets).

<table>
 <tbody>
  <tr>
   <td><strong>檢視器預設集標題</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>CSS檔案名稱</strong><br /> </td>
  </tr>
  <tr>
   <td>Carousel_Dotted_dark</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Dotted_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_dark</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>維度</td>
   <td>維度</td>
   <td><code>html5_dimensionalviewer.css</code></td>
  </tr>
  <tr>
   <td>彈出</td>
   <td>彈出式縮放</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>影像集_深色</td>
   <td>影像集</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>影像集光</td>
   <td>影像集</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_dark</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>彈出式縮放</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>全景影像</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImageVR</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>Interactive_Image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>互動視訊</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>互動視訊</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>smartcropvideo</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewer.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo_social</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>迴轉集_深色</td>
   <td>迴轉集</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>迴轉集_光線</td>
   <td>迴轉集</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>影片</p> <p>（包含隱藏式字幕支援）</p> </td>
   <td>影片</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>（包括基本視訊播放控制、視訊演算在立體聲模式下完成、手動視點控制關閉但陀螺儀控制開啟，以及無社群媒體功能）</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(專為使用虛擬現實眼鏡的使用者所設計。 包含基本視訊播放控制項和社群媒體功能)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>（包括支援隱藏式字幕和社群媒體）</p> </td>
   <td>影片</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_dark<br /> </td>
   <td>縮放<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>縮放</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### 支援的行動檢視器手勢矩陣 {#supported-mobile-viewers-gestures-matrix}

下表識別iOS、Android™ 2.x和Android™ 3.x裝置支援的行動檢視器手勢。

<table>
 <tbody>
  <tr>
   <td><strong>手勢</strong></td>
   <td><strong>彈出式縮放</strong></td>
   <td><strong>縮放</strong></td>
   <td><strong>迴轉</strong></td>
  </tr>
  <tr>
   <td><p><strong>拖曳</strong></p> </td>
   <td><p>Pans</p> </td>
   <td><p>Pans</p> </td>
   <td><p>Pans</p> </td>
  </tr>
  <tr>
   <td><p><strong>選擇</strong></p> </td>
   <td><p>顯示彈出式視窗</p> </td>
   <td><p>顯示或隱藏使用者介面</p> </td>
   <td><p>顯示或隱藏使用者介面</p> </td>
  </tr>
  <tr>
   <td><p><strong>雙選</strong></p> </td>
   <td><p>不適用</p> </td>
   <td><p>放大或重設</p> </td>
   <td><p>放大或重設</p> </td>
  </tr>
  <tr>
   <td><p><strong>捏緊開啟</strong></p> </td>
   <td><p>不適用</p> </td>
   <td><p>放大(僅限iOS和Android™ 3x)</p> </td>
   <td><p>放大(僅限iOS和Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>捏合關閉</strong></p> </td>
   <td><p>不適用</p> </td>
   <td><p>縮小(僅限iOS和Android™ 3x)</p> </td>
   <td><p>縮小(僅限iOS和Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>撥動</strong></p> </td>
   <td><p>捲動色票列</p> </td>
   <td><p>捲動影像</p> </td>
   <td><p>旋轉</p> </td>
  </tr>
  <tr>
   <td><p><strong>輕觸</strong></p> </td>
   <td><p>捲動色票列</p> </td>
   <td><p>捲動影像</p> </td>
   <td><p>旋轉</p> </td>
  </tr>
 </tbody>
</table>

## 增加顯示的檢視器預設集數目 {#increasing-the-number-of-viewer-presets-that-display}

Experience Manager在檢視資產時會顯示各種檢視器預設集 **[!UICONTROL 詳細資料檢視]** > **[!UICONTROL 檢視者]**. 您可以增加或減少顯示的檢視器數目。

**增加顯示的檢視器預設集數目：**

1. 導覽至CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 導覽至檢視器預設集清單節點，該節點位於下列位置：

   `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. 在 **[!UICONTROL limit]** 屬性中，將預設設 ****&#x200B;定為15的值變更為所要的數字。
1. 導覽至檢視器預設集資料來源，網址為 `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. 在limit屬性中，將數字變更為所需的數字，例如 `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 選取 **[!UICONTROL 全部儲存]**.

## 建立檢視器預設集 {#creating-a-new-viewer-preset}

建立檢視器預設集可讓您套用各種設定來檢視資產並與之互動。 不過，您不需要建立檢視器預設集。 您也可以選擇使用AEM Assets隨附的預設現成檢視器預設集。

如果您選擇建立檢視器預設集，儲存後會自動啟動檢視器狀態(設為 **[!UICONTROL 開啟]**)，位於「檢視器預設集」頁面。 此狀態表示只要您預覽影像或視訊，都可在Dynamic Media元件和互動媒體元件中看到。

有些檢視器預設集具有可影響檢視器使用和整體行為的獨佔設定。 根據您建立的檢視器預設集，您可能會想要瞭解這些特殊考量事項。

另請參閱 [建立互動式檢視器預設集的特殊考量事項](#special-considerations-for-creating-an-interactive-viewer-preset).

另請參閱 [建立轉盤橫幅檢視器預設集的特殊考量事項](#special-considerations-for-creating-a-carousel-banner-viewer-preset).

**若要建立檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產] > [!UICONTROL 檢視器預設集]**.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. 在「檢視器預設集」頁面的工具列上，選取「 」 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 新增檢視器預設集]** 對話方塊，在 **[!UICONTROL 預設集名稱]** 欄位，輸入新預設集的名稱。 請謹慎選擇名稱 — 在您選取後，這些名稱將無法編輯 **[!UICONTROL 建立]**.

   當您稍後在這些步驟中儲存預設集時，該名稱會顯示在「預設集標題」欄標題下的「檢視器預設集」頁面上。

1. 在「豐富型媒體型別」下拉式功能表中，選取您要建立的檢視器預設集型別，然後在頁面的右上角選取 **[!UICONTROL 建立]**.

   另請參閱 [檢視器預設集的豐富媒體型別](#rich-media-types-for-viewer-presets).

1. 在「檢視器預設集編輯器」頁面上，選擇 **[!UICONTROL 外觀]** 標籤。
1. 執行下列任一項作業：

   * 在 **[!UICONTROL 選取的型別]** 從下拉式選單中，選取您要自訂其視覺設計的元件。 或者，您可以在檢視器中選取任何視覺元素，以選取它進行設定。

     視覺化編輯器可讓您檢視特定屬性對樣式有何影響。 使用編輯器左側的範例來設定或調整任何屬性，以立即看到其對檢視器產生的影響。

     每種檢視器預設集型別的CSS樣式屬性都在「自訂」一節中說明 *`<viewer name>`* 檢視器」中的說明主題 [檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). 例如，如果您要建立的檢視器預設集型別為 `Mixed_Media`，請參閱 [自訂混合媒體檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html) 以取得每個屬性的清單和說明。

   * 如果您已在個別的CSS檔案中定義樣式設定，則可將CSS檔案上傳至AEM Assets。 選取 **[!UICONTROL 匯入CSS]** 在 **[!UICONTROL 選取的型別]** 下拉式選單（如有必要，請向上捲動視覺編輯器以檢視它）以便您可以找到上傳的CSS檔案並將其與檢視器預設集相關聯。

     匯入CSS檔案時，視覺編輯器會檢查CSS是否使用正確的檢視器標籤。 例如，如果您正在建立縮放檢視器，所有您匯入的CSS規則都必須使用其檢視器類別名稱來定義 `.s7mixedmediaviewer` 定義於父檢視器元素上。

     只要為指定檢視器正確定義CSS標籤，您就可以匯入任意的手工製作CSS。 (CSS標籤會在任何「自訂」一節中說明， *&lt;viewer name=&quot;&quot;>* 檢視器」中的說明主題 [檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). 例如，如果您想閱讀有關縮放檢視器的CSS標籤，請參閱 [自訂縮放檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html).) 不過，視覺化編輯器可能並不瞭解某些CSS值。 在這種情況下，視覺化編輯器會嘗試覆寫錯誤，讓CSS仍可運作。

   >[!NOTE]
   >
   >如果您偏好直接以原始格式編輯CSS，請選取「 」 **[!UICONTROL 顯示/隱藏CSS]** 在「選取型別」(Selected Type)下拉式選單下方（如有必要，請向上捲動視覺編輯器以檢視它）。
   >就像視覺化編輯器一樣，當您直接在CSS中變更屬性時，立刻就能看到這對檢視器範例有何影響。 同時，該屬性也會在視覺化編輯器中自動更新。 因此，您可以使用原始CSS編輯器或視覺化編輯器，或可互換使用兩者。

   >[!NOTE]
   >
   >對於按鈕圖稿，請選擇2x影像並上傳高解析度圖稿。 使用互動式影像和可購物橫幅時，您也可以選取各種現成的熱點按鈕。

1. （可選）在「編輯檢視器預設集」頁面頂端附近，選取「 」 **[!UICONTROL 案頭]**， **[!UICONTROL 平板電腦]**，或 **[!UICONTROL 電話]** 為不同的裝置和熒幕型別唯一定義視覺樣式。
1. 在「檢視器預設集編輯器」頁面上，選擇 **[!UICONTROL 行為]** 標籤。 或者，您可以在檢視器中選取任何視覺元素，以選取它進行設定。
例如，對於 *videoplayer* 文字，在 **[!UICONTROL 修飾元]** > **[!UICONTROL 播放]**，您可從下列三個最適化位元速率串流選項中選取：

   * **[!UICONTROL 虛線]**  — 視訊資料流僅以短劃線顯示。 不過，在Safari/iOS裝置上，您必須選取 **[!UICONTROL hls]** 做為型別。
   * **[!UICONTROL hls]**  — 視訊資料流僅以HLS形式。
   * **[!UICONTROL 自動]**  — 最佳做法。 建立DASH和HLS串流已最佳化儲存。 因此，Adobe建議您一律選取 **[!UICONTROL 自動]** 做為播放型別。 視訊串流採用虛線、hls或漸進式，如下列播放順序所示：
      * 如果瀏覽器支援DASH，則會先使用DASH串流。
      * 如果瀏覽器不支援DASH，則會使用HLS資料流（第二）。
      * 如果瀏覽器不支援DASH或HLS，最後會使用漸進式播放。

   >[!NOTE]
   >
   >若要檢視並使用 **[!UICONTROL 虛線]** 選項，必須先由您帳戶上的Adobe技術支援啟用。 另請參閱 [在您的帳戶上啟用DASH](/help/assets/video.md#enable-dash).

1. 從「選 **[!UICONTROL 定類型]** 」(Selected Type)下拉菜單中，選擇要更改其行為的元件。

   視覺化編輯器中的許多元件都有與之相關的詳細說明。 展開元件以顯示其相關引數時，這些說明會顯示在藍色方塊中。

   有些檢視器類型具有可讓您在「 **[!UICONTROL IS Command」 (IS命令) 文字欄位中指定「Image Serving]** 」 (影像伺服) 命令的元件。如需您可使用的指令清單，請參 [閱影像伺服API參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html)。

   >[!NOTE]
   >
   >**如果您使用觸控裝置，例如手機或平板電腦……**
   >
   >
   >在文字欄位中輸入值後，選取使用者介面中的其他位置以提交變更並關閉虛擬鍵盤。 如果您選取Enter，則不會發生任何動作。

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**.
1. 發佈新的檢視器預設集，以便用於您的網站。

   另請參閱 [發佈檢視器預設集](#publishing-viewer-presets).

   >[!IMPORTANT]
   >
   >針對使用最適化位元速率串流設定檔的舊影片，URL會隨著HLS串流繼續如常播放，直到您恢復正常播放 [重新處理視訊資產](/help/assets/processing-profiles.md#reprocessing-assets). 重新處理之後，相同的URL會繼續運作，不過現在有 *兩者* DASH和HLS串流已啟用。

### 建立互動式檢視器預設集的特殊考量事項 {#special-considerations-for-creating-an-interactive-viewer-preset}

**關於面板中影像縮圖的顯示模式**

當您建立或編輯互動式視訊檢視器預設集時，可以選擇在選取時要使用的顯示模式設定 `InteractiveSwatches` 從 **[!UICONTROL 選取的元件]** 選單下的 **[!UICONTROL 行為]** 標籤。 您選擇的顯示模式會影響縮圖在視訊播放時的顯示方式和時間。 您可以選擇 `segment`顯示模式（預設）或 `continuous` 顯示模式。

<table>
 <tbody>
  <tr>
   <td><strong>顯示模式</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>區段</td>
   <td><p><code>Segment </code>是現成互動視訊檢視器預設集的預設顯示模式 <code>Shoppable_Video_light</code> 和 <code>Shoppable_Video_dark</code> 以及您自行建立的任何互動式視訊檢視器預設集。</p> <p>在此模式中，當指派給視訊區段的縮圖數目少於顯示面板中的可見點數時。 此外，下一個或上一個子區段的縮圖為 <i>非 </i>拉入以填滿面板中的任何空白點。 也就是說，它可以保留指定給特定視訊區段的色票顯示。</p> </td>
  </tr>
  <tr>
   <td>連續</td>
   <td><p>在 <code>continuous </code>顯示模式：如果區段中的縮圖數目少於面板中顯示的數目，則檢視器會自動包含顯示下一個區段的縮圖。 或者，檢視器會自動包含先前區段縮圖的顯示（若顯示的是最後一個縮圖）。</p> <p>此 <a href="/help/assets/interactive-videos.md">此主題中的影片</a> 是 <code>continuous </code>顯示模式。</p> </td>
  </tr>
 </tbody>
</table>

**關於互動式視訊檢視器中的自動捲動行為**

互動式視訊檢視器中的縮圖自動捲動行為不受您選擇之顯示模式影響。

當您建立或編輯互動式視訊檢視器預設集時，可從「行為」標籤存取「自動捲動」。在行為標籤中，從 **[!UICONTROL 選取的元件]** 下拉式功能表，選取 **[!UICONTROL 互動色票]**. 「自動捲動」(Auto Scroll)複選框列在「IS命令」(IS Command)文本欄位下。

如果您在檢視器預設集中停用「自動捲動 **** 」 (清除核取方塊)，當使用者播放視訊時，面板只會顯示整個視訊長度的第一個縮圖影像。不過，使用者可視需要使用向上和向下箭頭圖示手動捲動縮圖。

當您在檢視器預設集中啟用 (選取) 「自動捲動 **** 」時，在視訊播放期間，指派給視訊區段的縮圖影像會在區段開始時捲動至檢視中。但是，有些例項會顯示區段中某些縮圖的長度，是其前後縮圖的兩倍。發生此行為是因為區段中的縮圖數目大於面板中顯示的數目，且不可平均分割。

舉例說明，假設您有一個30秒的視訊區段。 此外，30秒內總共會顯示九張縮圖。 您瀏覽器的大小調整方式，使顯示面板中有四個可見的縮圖位置。 30秒的視訊時間區段分為三個子區段。 下表顯示指定時間子區段顯示之縮圖的劃分：

| **視訊子區段** | **子區段時間（以秒為單位）** | **面板中可見的縮圖** |
|---|---|---|
| 1 | 0-10 | 1、2、3、4 |
| 2 | 10-20 | 4， 5， 6， 7 |
| 3 | 20-30 | 6、7、8、9 |

視訊子區段3的延伸範圍不會超出指派給它的縮圖。 也請注意，在面板中顯示的縮圖4、6和7比其他縮圖長兩倍。

檢視器根據可用位置數量，用於面板中顯示縮圖的邏輯如下：

* 子區段數=四捨五入至下一個子區段（縮圖數/縮圖面板中的可見位置數，根據瀏覽器視窗大小而定）。
以上表為例，9個縮圖/ 4個槽= 2.25；檢視器邏輯將其四捨五入為三個子區段。

* 縮圖數=四捨五入至下一個縮圖（縮圖數/視訊子區段數）。
以上表為例，9個縮圖/ 3個視訊子區段= 3個縮圖。

* 子區段持續時間=影片總持續時間/影片子區段數。
以上表範例為例，30秒/ 3視訊子區段=每個視訊子區段顯示10秒。

#### 建立轉盤橫幅檢視器預設集的特殊考量事項 {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

建立「轉盤橫幅」檢視器預設集時，變更熱點樣式的存取方式如下：

| | **說明** | **動作** |
|---|---|---|
| **[!UICONTROL 熱點圖示]** | 變更用於熱點的圖示 | 若要變更熱點圖示影像，請在 **[!UICONTROL 外觀]** 標籤，在 **[!UICONTROL 選取的元件]**，選取 **[!UICONTROL ImageMapEffect]**. 在 **[!UICONTROL 圖示]**，選取 **[!UICONTROL 背景]** 和 **[!UICONTROL 影像]** 欄位導覽至您想要的背景影像。 |

## 啟用或停用檢視器預設集 {#activating-or-deactivating-viewer-presets}

使用者介面中可用的檢視器預設集取決於作者模式中處於作用中的檢視器預設集。 依預設，建立檢視器預設集後設為「開啟」。 如果您關閉預設集，在「作者」模式中看不到預設集。 如果預設集已發佈，則無論其是否切換，都會發佈預設集。 如果清單太笨拙，或者您不想讓檢視器預設集可供使用，您可能會想要停用檢視器預設集。

**若要啟用或停用檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 在「檢視器預設集」頁面的 **[!UICONTROL 狀態]** 欄標題，選取切換即可啟用或停用檢視器預設集。

   已啟動的檢視器預設集會在右側顯示切換，並位於藍色方塊內；已停用的檢視器預設集會在左側顯示切換，並位於淺灰色方塊內。

## 發佈檢視器預設集 {#publishing-viewer-presets}

啟用（或開啟）檢視器預設集狀態表示檢視器預設集會顯示在Dynamic Media元件、互動媒體元件中，以及您檢視資產的任何時間。

但是，到 *deliver* 如果資產具有檢視器預設集，檢視器預設集也必須發佈。 必須啟動所有檢視器預設集 *和* 已發佈，以取得資產的URL或內嵌程式碼。 請務必啟動並發佈Dynamic Media隨附的所有現成可用的檢視器預設集。 您建立和新增的自訂檢視器預設集會自動啟動，但也必須發佈。

另請參閱 [啟用或停用檢視器預設集](#activating-or-deactivating-viewer-presets).

另請參閱 [預覽資產](/help/assets/previewing-assets.md).

**若要發佈檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 選取一或多個您要發佈的檢視器預設集。
1. 在工具列上，選取 **[!UICONTROL 發佈]** 圖示。

## 排序檢視器預設集 {#sorting-viewer-presets}

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 選取 **[!UICONTROL 預設集標題]**， **[!UICONTROL 型別]**， **[!UICONTROL 已發佈]**，或 **[!UICONTROL 狀態]** 以依該欄標題排序。 例如，選取 **[!UICONTROL 型別]**  依字母或反向字母順序排序檢視器預設集型別。

## 編輯檢視器預設集 {#editing-viewer-presets}

編輯任何 *預先定義的現成檢視器預設集* 不支援的情況。 如果您編輯現成的檢視器預設集，系統會提示您以新名稱儲存該預設集。

**若要編輯檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 勾選檢視器預設集標題左側的方塊，選取預設集。
1. 在工具列上，選取 **[!UICONTROL 編輯]**.
1. 在 **[!UICONTROL 檢視器預設集編輯器]** 頁面上，使用「 」選單中的選項，對檢視器預設集進行您想要的變更 **[!UICONTROL 外觀]** 和 **[!UICONTROL 行為]** 索引標籤。

   從 **[!UICONTROL 外觀]** 索引標籤中，在「檢視器預設集編輯器」頁面的左上角附近，選取 **[!UICONTROL 案頭]**， **[!UICONTROL 平板電腦]**，或 **[!UICONTROL 電話]** 以變更資產的簡報模式。

1. 在頁面的右上角附近，執行下列任一項作業：

   * 選取 **[!UICONTROL 儲存]** 以儲存您的變更並返回「檢視器預設集」頁面。
   * 選取 **[!UICONTROL 取消]** 使所做的任何變更失效，並返回「檢視器預設集」頁面。

## 刪除自訂檢視器預設集 {#deleting-custom-viewer-presets}

您可以刪除已建立並新增至Dynamic Media的檢視器預設集。

**若要刪除自訂檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 在「檢視器預設集」頁面上，核取「預設集標題」，然後選取 **[!UICONTROL 垃圾桶]** 圖示。
1. 選取&#x200B;**[!UICONTROL 刪除]**。

## 將檢視器預設集套用至資產 {#applying-a-viewer-preset-to-an-asset}

如果您已發佈資產和選取的檢視器， **[!UICONTROL URL]** 和 **[!UICONTROL Embed]**  (內嵌) 按鈕會在您選取檢視器預設集後顯示。

**若要將檢視器預設集套用至資產：**

1. 開啟資產，並在頁面左上角附近選取下拉式功能表，然後選取「 」 **[!UICONTROL 檢視者]**.

   >[!NOTE]
   >
   >如果您已發佈資產和選取的檢視器， **[!UICONTROL URL]** 和 **[!UICONTROL Embed]**  (內嵌) 按鈕會在您選取檢視器預設集後顯示。

1. 從左窗格選取檢視器預設集，以便將其套用至資產。

   您可以 [複製要共用的URL](/help/assets/linking-urls-to-yourwebapplication.md) 與其他使用者整合。

## 使用檢視器預設集傳送資產 {#delivering-assets-with-viewer-presets}

若要取得檢視器預設集的URL，請參閱 [將URL連結至您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md). 另請參閱 [將視訊檢視器內嵌在網頁上](/help/assets/embed-code.md).

如果您使用Experience Manager做為WCM，您可以直接在頁面上使用檢視器預設集新增資產。 另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).
