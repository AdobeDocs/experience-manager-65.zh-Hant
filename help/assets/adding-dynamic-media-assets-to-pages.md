---
title: 新增動態媒體資產至頁面
description: 如何在AEM中將Dynamic media元件新增至頁面
uuid: b5e982f5-fa1c-478a-bcb3-a1ef980df201
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 97a5f018-8255-4b87-9d21-4a0fdf740e4d
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 新增動態媒體資產至頁面{#adding-dynamic-media-assets-to-pages}

若要將動態媒體功能新增至您在網站上使用的資產，您可以直接在頁面上新增 **Dynamic Media**、 **Interactive Media**、 **Media**&#x200B;或 **** Video 360全景媒體元件。 若要這麼做，請進入「版面」模式並啟用「動態媒體」元件。 然後，您可以將這些元件新增至頁面，並新增資產至元件。 動態媒體元件是智慧型的——他們知道您是新增影像還是視訊，而可用的設定選項也會隨之變更。

如果您使用AEM做為WCM，請直接將Dynamic media資產新增至頁面。 如果您使用協力廠商來處理WCM，請連結 [或](/help/assets/linking-urls-to-yourwebapplication.md)[內嵌資](/help/assets/embed-code.md) 產。 如需多方互動網站，請參閱將最佳化 [的影像傳送至多方互動網站](/help/assets/responsive-site.md)。

>[!NOTE]
>
>您必須先發佈資產，才能將資產新增至AEM中的頁面。 請參閱 [發佈動態媒體資產](/help/assets/publishing-dynamicmedia-assets.md)。

## 新增動態媒體元件至頁面 {#adding-a-dynamic-media-component-to-a-page}

將動態媒體、互動式媒體、全景媒體或視訊360媒體元件新增至頁面，與將元件新增至任何頁面相同。 以下各節將介紹動態媒體元件。

1. 在AEM中，開啟您要新增動態媒體元件的頁面。
1. 在左窗格中，點選「元件 **[!UICONTROL 」圖示]** ，然後篩選「動態媒體」。

   如果沒有可用的動態媒體元件，您必須啟用或開啟動態媒體元件。 如需詳 [細資訊，請參閱編輯頁面範本](/help/sites-authoring/templates.md#editing-templates-template-authors) 。

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. 拖曳動 **[!UICONTROL 態媒體元件]** ，並將其拖曳至頁面上所需的位置。

   在以下範例中， **[!UICONTROL 使用Video 360 Media]** （視訊360媒體）元件。

   ![6_5_360video_wcmcomponentdrag](assets/6_5_360video_wcmcomponentdrag.png)

1. 將滑鼠指標直接暫留在元件上。 當元件被藍色方塊包圍時，點選一次即可顯示元件的工具列。 點選「 **[!UICONTROL Configuration(wrench)]** 」圖示。

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. 視您拖放至頁面的動態媒體元件而定，會開啟設定對話方塊。 [視需要設定元件的選項](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) 。

   下列範例顯示「動態媒體 **[!UICONTROL 視訊360媒體]** 」元件對話方塊和「檢視器預設集」下拉式清單中可用的選項。

   ![視訊360媒體元件](assets/6_5_360video_wcmcomponentviewerpreset.png)

   動態媒體視訊360媒體元件。

1. 完成後，在對話框右上角附近點選核取標籤以儲存變更。

## 本地化動態媒體元件 {#localizing-dynamic-media-components}

您可透過下列兩種方式將Dynamic media元件當地語系化：

* 在「網站」的網頁中，開啟「屬 **[!UICONTROL 性]** 」並選 **[!UICONTROL 取「進階]** 」標籤。 選擇所要的本地化語言。

   ![chlimage_1-172](assets/chlimage_1-538.png)

* 從網站選取器中，選取所要的頁面或頁面群組。 點選「 **[!UICONTROL 屬性]** 」並選取「 **[!UICONTROL 進階]** 」標籤。 選擇所要的本地化語言。

   >[!NOTE]
   >
   >請注意，並非「語言」選單中所有可用的 **[!UICONTROL 語言]** ，目前都已指派Token。

## 動態媒體元件 {#dynamic-media-components}

當您點選「元件」圖示，然後在「動態媒體」上篩選時， **[!UICONTROL 就可使用]** 「動態媒 **[!UICONTROL 體」元件]**。

可用的動態媒體元件包括：

* **[!UICONTROL 動態媒體]** -用於影像、視訊、eCatalog和回轉集等資產。
* **[!UICONTROL 互動式媒體]** -用於任何互動式資產，例如互動式視訊、互動式影像或轉盤集。
* **[!UICONTROL 全景媒體]** -用於全景影像或全景VR影像資產。
* **[!UICONTROL 視訊360媒體]** -用於360視訊和360 VR視訊資產。

>[!NOTE]
>
>這些元件預設不可用，在使用之前必須先透過範本編輯器提供。 [在範本編輯器中提](/help/sites-authoring/templates.md#editing-templates-template-authors)供這些元件後，您就可以像新增其他AEM元件一樣，將元件新增至您的頁面。

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Dynamic Media component {#dynamic-media-component}

動態媒體元件是智慧型元件。 視您新增影像或視訊而定，您有各種選項。 此元件支援影像預設集、影像檢視器，例如影像集、回轉集、混合媒體集和視訊。 此外，檢視器具有互動功能——螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

>[!NOTE]
>
>如果您的網頁有下列項目：
>
>* 在相同頁面上使用多個動態媒體元件例項。
>* 每個例項都使用相同的資產類型。
>
>
請注意，不支援為該頁面上的每個動態媒體元件指派不同的檢視器預設集。
>
>不過，您可以對頁面內使用相同類型資產的所有動態媒體元件使用相同的檢視器預設集。

當您新增動態媒體元件，而「動態媒 **[!UICONTROL 體設定]** 」為空白或無法正確新增資產時，請勾選下列項目：

* 您已啟 [用動態媒體](/help/assets/config-dynamic.md)。 動態媒體預設為停用。
* 該影像具有金字塔tiff檔案。 在啟用動態媒體之前匯入的影像沒有金字塔tiff檔案。

#### 使用影像時 {#when-working-with-images}

動態媒體元件可讓您新增動態影像，包括影像集、回轉集和混合媒體集。 您可以放大、縮小，如果適用，則可以在回轉集內旋轉影像，或從其他類型的回轉集選取影像。

您也可以直接在元件中設定檢視器預設集、影像預設集或影像格式。 若要讓影像回應，您可以設定中斷點或套用回應式影像預設集。

您可以點選元件中的「編輯」圖示，然後點選「動態媒體設定」，以編 **[!UICONTROL 輯下列]** 「動態媒體 **[!UICONTROL 設定」]**。

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。 如果要使其成為固定大小，請在「高級」( **[!UICONTROL Advanced]** )頁籤的元件中使用「寬度」( **[!UICONTROL Width)和「高度」(Height]** )設定它 ****。

* **[!UICONTROL 檢視器預設]**-從下拉式選單中選取現有的檢視器預設。 如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 請參閱管理檢視器預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

   如果您要檢視影像集、回轉集或混合媒體集，這是唯一可用的選項。 顯示的檢視器預設集也很聰明——只會顯示相關的檢視器預設集。

* **[!UICONTROL 檢視器修飾元]**-檢視器修飾元採用名稱=值配對與&amp;分隔字元的形式，可讓您變更檢視器，如檢視器參考指南所述。 觀看者修飾詞的示例是為 `posterimage=img.jpg&caption=text.vtt,1` 視頻縮略圖設定不同的影像，並將隱藏字幕／字幕檔案與視頻相關聯。

* **[!UICONTROL 影像預設集]**-從下拉式選單中選取現有的影像預設集。 如果您要尋找的影像預設集不可見，您可能需要將它顯示。 請參閱管理影像預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 影像修飾元]**-您可以提供其他影像指令來套用影像效果。 這些說明在「影像預設集」和「影像伺服命令」參考中。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 中斷點]**-如果您在回應式網站上使用此資產，則需要新增影像中斷點。 影像中斷點必須以逗號(,)分隔。 當影像預設集中未定義高度或寬度時，此選項便可運作。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

   您可以點選元件中的「編輯」，編輯下列 **[!UICONTROL 進階設定]** 。

* **[!UICONTROL 標題]**-更改影像的標題。

* **[!UICONTROL 替代文字]**-為關閉圖形的使用者新增影像標題。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL URL, Open in]**- You can set an asset to open a link. 設定URL，並在「開啟於」中指出您要在相同視窗或新視窗中開啟它。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 寬度]**-如果希望影像為固定大小，請以像素輸入值。 將此值留空可讓資產具有適應性。

* **[!UICONTROL 高度]**-如果希望影像為固定大小，請以像素輸入值。 將此值留空可讓資產具有適應性。


#### 使用視訊時 {#when-working-with-video}

使用動態媒體元件，將動態視訊新增至網頁。 當您編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集來播放頁面上的視訊。

![chlimage_1-173](assets/chlimage_1-540.png)

按一下元件中的「編輯」，即可編輯下列 **[!UICONTROL 動態媒體]** 「設定」。

>[!NOTE]
>
>依預設，動態媒體視訊元件是可調式的。 如果要使其成為固定大小，請在元件中使用「高級」( **[!UICONTROL Advanced]** )頁籤中的「寬度」( **[!UICONTROL Width]** )和「高度」( **[!UICONTROL Height]** )來設定它。

* **[!UICONTROL查看器預設集**-從下拉菜單中選擇現有視頻查看器預設集。 如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 請參閱管理檢視器預設集。

* **[!UICONTROL檢視器修飾元**-檢視器修飾元採用名稱=值配對與&amp;分隔字元的形式，讓您變更檢視器，如Adobe檢視器參考指南所述。 檢視器修飾詞的範例是 `posterimage=img.jpg&caption=text.vtt,1`

   例如，使用檢視器修飾元，您可以執行下列動作：

   * 將標題檔案與視訊關聯： [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_video_viewer_url_caption.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_video_viewer_url_caption.html)
   * 將導覽檔案與視訊建立關聯： [https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_video_viewer_url_navigation.html](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/r_html5_video_viewer_url_navigation.html)
   按一下元件中的「編輯」(Edit **** )可編輯以下「高級設定」(Advanced Settings)。

* **[!UICONCONTROL標題**-更改視頻的標題。

* **[!UICONTROL 寬度]**-如果希望影像為固定大小，請以像素輸入值。 將此值留空可讓資產具有適應性。

* **[!UICONTROL 高度]**-如果希望影像為固定大小，請以像素輸入值。 將此值留空可讓資產具有適應性。

#### 使用Smart Crop時 {#when-working-with-smart-crop}

使用動態媒體元件將智慧型裁切影像資產新增至您的網頁。 當您編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集來播放頁面上的視訊。

另請參閱影 [像描述檔](/help/assets/image-profiles.md)。

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

按一下元件中的「編輯」，即可編輯下列 **[!UICONTROL 動態媒體]** 設定。

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。 如果要使其成為固定大小，請在「高級」( **[!UICONTROL Advanced]** )頁籤的元件中使用「寬度」( **[!UICONTROL Width)和「高度」(Height]** )設定它 ****。

* **[!UICONTROL 影像修飾元]**-您可以提供其他影像指令來套用影像效果。 這些說明在「影像預設集」和「影像伺服命令」參考中。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

   按一下元件中的「編輯」(Edit **** )可編輯以下「高級設定」(Advanced Settings)。

* **[!UICONTROL 標題]**-更改「智慧裁切」影像的標題。

* **[!UICONTROL 替代文字]**-為關閉圖形的使用者新增智慧型裁切影像的標題。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL URL, Open in]**- You can set an asset to open a link. 設定URL，並在「開啟於」中指出您要在相同視窗或新視窗中開啟它。

   如果您正在檢視影像集、回轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 寬度]**-如果希望影像為固定大小，請以像素輸入值。 將此值留空可讓資產具有適應性。

* **[!UICONTROL 高度]**-如果希望影像為固定大小，請以像素輸入值。 將此值留空可讓資產具有適應性。

### 互動式媒體元件 {#interactive-media-component}

互動式媒體元件適用於這些資產上具有互動功能的熱點或影像地圖。 如果您有互動式影像、互動式視訊或轉盤橫幅，請使用互動式 **[!UICONTROL 媒體元件]** 。

互動式媒體元件是智慧型的。 視您新增影像或視訊而定，您有各種選項。 此外，檢視器具有互動功能——螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

>[!NOTE]
>
>如果您的網頁有下列項目：
>
>* 在相同頁面上使用多個互動式媒體元件例項。
>* 每個例項都使用相同的資產類型。
>
>
請注意，不支援為該頁面上的每個互動式媒體元件指派不同的檢視器預設集。
>
>不過，您可以針對頁面內使用相同類型資產的所有互動式媒體元件使用相同的檢視器預設集。

![chlimage_1-174](assets/chlimage_1-541.png)

您可以點選元件中的「編 **[!UICONTROL 輯]** 」( **[!UICONTROL Edit]** )，編輯下列「一般」(General)設定。

* **[!UICONTROL 檢視器預設]**-從下拉式選單中選取現有的檢視器預設。 如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 檢視器預設集必須先發佈，才能使用。 請參閱管理檢視器預設集。

* **[!UICONTROL 標題]**-變更影片標題。

* **[!UICONTROL 寬度]**-如果希望影像為固定大小，請以像素輸入值。 將此值留空可讓資產具有適應性。

* **[!UICONTROL 高度]**-如果希望影像為固定大小，請以像素輸入值。 將此值留空可讓資產具有適應性。

   您可以按一下元件 **[!UICONTROL 中的「編輯」]** ，編輯下列「新 **** 增至購物車」設定。

* **[!UICONTROL 顯示產品資產]**-預設情況下，此值為選定值。 產品資產會依「商務」模組中的定義，顯示產品的影像。 清除核取標籤，不會顯示產品資產。

* **[!UICONTROL 顯示產品價格]**-預設情況下，此值處於選中狀態。 產品價格顯示「商務」模組中定義的項目價格。 清除勾號以不顯示產品價格。

* **[!UICONTROL 顯示產品表單]**-預設情況下，不選擇此值。 「產品表單」包含任何產品變體，例如尺寸和顏色。 清除勾號，不顯示產品變數。

### 全景媒體元件 {#panoramic-media-component}

全景媒體元件適用於球形全景影像的資產。 此類影像可提供360°的房間、房產、位置或風景觀賞體驗。 若要符合球形全景的影像，它必須具備下列其中一個或兩個：

* 寬高比為2:1。
* 使用關鍵字 `equirectangular` 或(`spherical` + `panorama`)或(`spherical` + `panoramic`)標籤。 請參 [閱使用標籤](/help/sites-authoring/tags.md)。

外觀比例和關鍵字條件都適用於資產詳細資料頁面和全景媒體 **** WCM元件的全景資產。

>[!NOTE]
>
>如果您的網頁有下列項目：
>
>* 在相同頁面上 **[!UICONTROL 使用Panoramic Media]** （全景媒體）元件的多個例項。
>* 每個實例都使用相同的資產類型。
>
>
請注意，不支援為該頁面上的每個 **[!UICONTROL Panoramic Media]** （全景媒體）元件指派不同的檢視器預設集。
>
>但是，您可以針對頁面內使用相同類型資產的所有全景媒體元件使用相同的檢視器預設集。

![panoramic-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

您可以點選元件中的「設定」，以編 **[!UICONTROL 輯下列設定]** 。

* **[!UICONTROL 檢視器預設]**(Viewer Preset)-從「檢視器預設」下拉式選單中選取現有的檢視器。

如果您所尋找的檢視器預設集不可見，請勾選以確保已發佈。 您必須先發佈檢視器預設集，才能使用。 請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md)。

### 視訊360媒體元件 {#video-media-component}

使用 **[!UICONTROL Video 360 Media]** （視訊360媒體）元件，在您的網頁上演算等方形視訊，以提供身歷其境的房間、房產、位置、風景或醫療程式檢視體驗。

在平面顯示器上播放時，用戶可以控制視角；在行動裝置上播放時，通常會運用其內建的陀螺控制項。

檢視器包含傳送360個視訊資產的原生支援。 依預設，檢視或播放不需要其他設定。 您可使用標準的視訊副檔名（例如。mp4、.mkv和。mov）來傳送360視訊。 最常見的轉碼器是H.264。

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

您可以點選元件中的「設定」，以編 **[!UICONTROL 輯下列設定]** 。

* **[!UICONTROL 檢視器預設]**(Viewer Preset)-從「檢視器預設」下拉式選單中選取現有的檢視器。 使用Video360VR的使用者可使用虛擬實境眼鏡。 包含基本的視訊播放控制項和社交媒體功能。 使用Video360_social，其中包含基本的視訊播放控制項。 視訊演算是在立體模式下完成。 手動視點控制已關閉，但陀螺儀控制已開啟。 沒有社交媒體功能。

如果您所尋找的檢視器預設集不可見，請勾選以確保已發佈。 您必須先發佈檢視器預設集，才能使用。 請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md)。

### 使用HTTP/2來傳送動態媒體資產 {#using-http-to-delivery-dynamic-media-assets}

HTTP/2是全新、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並降低所需的處理能力。 動態媒體資產的傳送現在可透過HTTP/2，提供更佳的回應和載入時間。

如需 [您的動態媒體帳戶開始使用HTTP/2的完整詳細資訊，請參閱HTTP2內容傳送](/help/assets/http2.md) 。

>[!MORELIKETHIS]
>
>* [在AEM Dynamic media中使用視訊播放器](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-player-feature-video-use.html)
>* [搭配AEM Dynamic media使用互動式視訊](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-interactive-video-feature-video-use.html)
>* [使用AEM Dynamic media瞭解資產檢視器](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-viewer-feature-video-understand.html)
>* [搭配AEM Dynamic media使用自訂視訊縮圖](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-thumbnails-feature-video-use.html)
>* [瞭解使用AEM Dynamic media進行色彩管理](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-color-management-technical-video-setup.html)
>* [搭配AEM Dynamic media使用影像銳利化](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-image-sharpening-feature-video-use.html)

