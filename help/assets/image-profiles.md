---
title: Dynamic Media影像設定檔
description: 建立包含遮色片銳利化設定和/或智慧型裁切或智慧型色票設定的影像設定檔，然後將設定檔套用至影像資產的資料夾。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
solution: Experience Manager, Experience Manager Assets
source-git-commit: a4c95d604e63c4fd00f17d2fb99a9e46f823ca10
workflow-type: tm+mt
source-wordcount: '3063'
ht-degree: 4%

---

# Dynamic Media影像設定檔 {#image-profiles}

上傳影像時，您可以套用影像設定檔至資料夾，在上傳時自動裁切影像。

>[!IMPORTANT]
>
>* 智慧型裁切僅適用於Dynamic Media - Scene7模式。
>* 「影像設定檔」不適用於PDF、動畫GIF或INDD (Adobe InDesign)檔案。

## 裁切選項 {#crop-options}

當您對影像實作智慧型裁切時，Adobe會建議下列最佳作法並強制進行下列限制：

| 限制型別 | 最佳實務 | 強加的限制 |
| --- | --- | --- |
| 每個影像的智慧型裁切數目 | 5 | 100 |

另請參閱[Dynamic Media限制](/help/assets/limitations.md)。

<!-- CQDOC-16069 for paragraph directly below -->

智慧型裁切座標會根據外觀比例而定。 針對影像設定檔中的各種智慧型裁切設定，如果影像設定檔中新增維度的外觀比例相同，則會將相同的外觀比例傳送至Dynamic Media。 Adobe建議您使用相同的裁切區域。 這麼做可確保不會對「影像設定檔」中使用的不同維度造成影響。

您建立的每個智慧型裁切產生都需要額外的處理。 例如，新增五個以上的智慧型裁切外觀比例可能會導致資產擷取速度緩慢。 它也會造成系統負載增加。 由於您可以在資料夾層級套用智慧型裁切，Adobe建議您僅在需要的資料夾&#x200B;*使用*。

**定義影像設定檔中智慧型裁切的准則**
為了控制智慧型裁切使用量，並最佳化裁切的處理時間和儲存空間，Adobe建議下列准則和提示：

* 即將套用智慧型裁切的影像資產必須至少為50 x 50畫素或更大。
* 理想情況下，每個影像可裁切10至15顆智慧型影像，以最佳化熒幕比例和處理時間。
* 根據裁切維度而非最終使用狀況來命名智慧型裁切。 這麼做有助於最佳化在多個頁面上使用單一維度的重複專案。
* 為特定資料夾和子資料夾建立頁面/資產型別的影像設定檔，而非套用至所有資料夾或所有資產的通用智慧型裁切設定檔。
* 套用至子資料夾的影像設定檔會覆寫套用至資料夾的影像設定檔。
* 不允許包含重複智慧型裁切尺寸的影像設定檔。
* 不允許設定有智慧型裁切選項的重複已命名影像設定檔。

您有兩個影像裁切選項可供選擇：「畫素裁切」或「智慧型裁切」。 您也可以選擇自動建立顏色和影像色票。

>[!IMPORTANT]
>
>* Adobe建議您檢閱任何產生的裁切和色票，確保它們適當且與您的品牌和價值相關。
>* 智慧型裁切不支援CMYK影像格式。

| 選項 | 使用時機 | 說明 |
| --- | --- | --- |
| 像素裁切 | 僅根據尺寸大量裁切影像。 | 若要使用此選項，請從[裁切選項]下拉式清單中選取&#x200B;**[!UICONTROL 畫素裁切]**。<br><br>若要從影像側面裁切，請輸入影像任何側面或每一側面要裁切的畫素數。 裁切多少影像取決於影像檔案中的ppi （每英吋畫素）設定。<br><br>影像設定檔畫素裁切會以下列方式呈現：<br>·值為上、下、左和右。<br>·左上方會視為`0,0`，而畫素裁切是從此處計算的。<br>·裁切起點：左邊是X，上邊是Y<br>·水準計算：原始影像的水準畫素尺寸減去「左」，然後減去「右」。<br>·垂直計算：垂直畫素高度減去「頂端」，然後減去「底部」。<br><br>例如，假設您有4000 x 3000畫素影像。 您使用下列值：Top=250、Bottom=500、Left=300、Right=700。<br><br>從左上方(300,250)裁切，使用（4000-300-700、3000-250-500或3000,2250）的填色空間。 |
| 智慧型裁切 | 根據視覺焦點批次裁切影像。 | 智慧型裁切利用Adobe Sensei中人工智慧的強大功能，快速大量自動裁切影像。 智慧型裁切會自動偵測並裁切至任何影像中的焦點，以擷取預期的目標點，無論熒幕大小為何。</p> <p>若要使用智慧型裁切，請從「裁切選項」下拉式清單中選取&#x200B;**[!UICONTROL 智慧型裁切]**，然後在回應式影像裁切的右側，啟用（開啟）此功能。</p> <p>「大」、「Medium」和「小」的預設中斷點大小通常涵蓋行動裝置和平板電腦裝置、桌上型電腦和橫幅上大部分影像使用的完整大小範圍。 如有需要，您可以編輯「大」、「Medium」和「小」的預設名稱。</p> <p>若要新增更多中斷點，請選取&#x200B;**[!UICONTROL 新增裁切]**&#x200B;以刪除裁切，並選取「垃圾桶」圖示。 |
| 顏色及影像樣本 | 大量產生每個影像的影像色票。 | **注意**： Dynamic Media Classic不支援智慧型色票。<br><br>從顯示顏色或紋理的產品影像自動尋找並產生高品質色票。<br><br>若要使用「顏色和影像色票」，請從「裁切選項」下拉式清單中選取「**[!UICONTROL 智慧型裁切]**」，然後在「顏色和影像色票」的右側，啟用（開啟）此功能。 在「寬度」和「高度」文字方塊中輸入畫素值。<br><br>雖然所有影像裁切都可從「轉譯」邊欄取得，但色票只能透過「複製URL」功能使用。 使用您自己的檢視元件來呈現網站上的色票。 (此規則的例外是輪播橫幅。 Dynamic Media為輪播橫幅中使用的色票提供檢視元件。)<br><br>**使用影像色票**<br>&#x200B;影像色票的URL很簡單。 它是：<br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>，其中`:Swatch`已附加至資產要求。<br><br>**使用色票**<br>&#x200B;若要使用色票，您需提出包含下列內容的`req=userdata`要求：<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例如，下列是Dynamic Media Classic中的色票資產：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>以下是色票資產對應的`req=userdata` URL：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br> `req=userdata`回應如下：<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>您也可以要求XML或JSON格式的`req=userdata`回應，如下列個別URL範例所示：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**注意：**&#x200B;建立您自己的WCM元件以要求色票並剖析`SmartSwatchColor`屬性，以24位RGB的十六進位制值表示。<br><br>另請參閱檢視器參考指南[&#128279;](https://experienceleague.adobe.com/zh-hant/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata)中的`userdata`。 |

## 不銳利化遮色片 {#unsharp-mask}

使用&#x200B;**[!UICONTROL 不銳利化遮色片]**&#x200B;來微調最終縮減取樣影像的銳利化濾鏡效果。 您可以控制效果的強度、效果的半徑（以畫素測量），以及被忽略的對比度臨界值。 此效果使用與Adobe Photoshop的&#x200B;*遮色片銳利化*&#x200B;濾鏡相同的選項。

>[!NOTE]
>
>不銳利化遮色片只會套用至PTIFF （金字塔tiff）中縮減取樣超過50%的縮減比例轉譯。 這表示ptiff中最大大小的轉譯不會受到不銳利化遮色片的影響，而較小大小的轉譯（例如縮圖）會遭到更改（並顯示不銳利化遮色片）。

在&#x200B;**[!UICONTROL 不銳利化遮色片]**&#x200B;中，您有下列篩選選項：

| 選項 | 說明 |
| --- | --- |
| 數量 | 控制套用至邊緣畫素的對比量。 預設值為1.75。若是高解析度的影像，最高可增加至5。 將「數量」視為濾鏡強度的量度。 範圍為0到5。 |
| 半徑 | 決定邊緣畫素周圍影響銳利化的畫素數量。對於高解析度的影像，請輸入1到2。低值只會銳利化邊緣畫素；高值會銳利化較寬的畫素範圍。 正確的值取決於影像的大小。 預設值為0.2。範圍為0到250。 |
| 臨界值 | 決定套用遮色片銳利化調整濾鏡時要忽略的對比範圍。換言之，此選項決定銳化畫素與周圍區域的差異程度，才會被視為邊緣畫素並予以銳化。 為避免引入雜訊，請嘗試使用0到255之間的值。 |

在[銳利化影像](/help/assets/assets/sharpening_images.pdf)中說明銳利化。

## 建立Dynamic Media影像設定檔 {#creating-image-profiles}

若要定義其他資產型別的進階處理引數，請參閱[設定資產處理](config-dms7.md#configuring-asset-processing)。

檢視[處理中繼資料、影像和影片的設定檔](processing-profiles.md)。

另請參閱[組織數位Assets以使用處理設定檔的最佳實務](/help/assets/organize-assets.md)。

**若要建立Dynamic Media影像設定檔：**

1. 選取Adobe Experience Manager標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 影像設定檔]**。
1. 選取「**[!UICONTROL 建立]**」以新增影像設定檔。
1. 輸入輪廓名稱，以及遮色片、裁切或色票（或兩者）的銳利化調整值。

   使用專屬於其預定用途的設定檔名稱。 例如，如果您想建立只產生色票的設定檔(即智慧型裁切已停用（關閉），而顏色和影像色票已啟用（開啟）)，請使用設定檔名稱「智慧型色票」。

   另請參 [閱智慧型裁切和智慧型色票選項](#crop-options) [和遮色片銳利化](#unsharp-mask)。

   ![裁切](assets/crop.png)

1. 選取&#x200B;**[!UICONTROL 儲存]**。新建立的設定檔會顯示在可用設定檔清單中。

## 編輯或刪除Dynamic Media影像設定檔 {#editing-or-deleting-image-profiles}

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 影像設定檔]**。
1. 選取您要編輯或移除的影像設定檔。 若要編輯它，請選取&#x200B;**[!UICONTROL 編輯影像設定檔]**。 若要移除它，請選取&#x200B;**[!UICONTROL 刪除影像設定檔]**。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果編輯，請儲存變更。 如果刪除，請確認您要移除設定檔。

## 將Dynamic Media影像設定檔套用至資料夾 {#applying-an-image-profile-to-folders}

當您將「影像描述檔」指派給資料夾時，任何子資料夾都會自動從其父資料夾繼承描述檔。 此工作流程表示您只能將一個影像設定檔指派至資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的資料夾結構。

如果您將不同的影像設定檔指派給資料夾，則新的設定檔會覆寫先前的設定檔。 先前現有的資料夾資產保持不變。 新設定檔會套用至稍後新增至資料夾的資產。

已指派設定檔的資料夾會使用卡片中顯示的設定檔名稱在使用者介面中指明。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以將影像設定檔套用至特定資料夾，或全域套用至所有資產。

若資料夾中已有您後來加以變更的現有影像設定檔，您可以重新處理該資料夾中的資產。 檢視在您編輯資料夾中資產的處理設定檔後，[重新處理資料夾中的資產](processing-profiles.md#reprocessing-assets)。

### 將Dynamic Media影像設定檔套用至特定資料夾 {#applying-image-profiles-to-specific-folders}

您可以從&#x200B;**[!UICONTROL 工具]**&#x200B;功能表或在資料夾內的&#x200B;**[!UICONTROL 屬性]**&#x200B;中，將影像設定檔套用至資料夾。 本節說明如何以兩種方式將「影像設定檔」套用至資料夾。

已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

若資料夾中已有您後來加以變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 檢視在您編輯資料夾中資產的處理設定檔後，[重新處理資料夾中的資產](processing-profiles.md#reprocessing-assets)。

#### 從「設定檔」使用者介面將Dynamic Media影像設定檔套用至資料夾 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 影像設定檔]**。
1. 選取您要套用至一或多個資料夾的影像設定檔。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 選取&#x200B;**[!UICONTROL 將處理設定檔套用至資料夾]**，然後選取您要用來接收新上傳資產的資料夾或多個資料夾，並選取&#x200B;**[!UICONTROL 套用]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

#### 從「屬性」將Dynamic Media影像設定檔套用至資料夾 {#applying-image-profiles-to-folders-from-properties}

1. 選取Experience League標誌並導覽至&#x200B;**[!UICONTROL Assets]**。 然後導覽至您要套用影像設定檔之資料夾的父資料夾。
1. 在資料夾中，選取核取記號以選取資料夾，然後選取&#x200B;**[!UICONTROL 屬性]**。
1. 選取&#x200B;**[!UICONTROL 影像設定檔]**&#x200B;標籤。 從&#x200B;**[!UICONTROL 設定檔名稱]**&#x200B;下拉式清單中，選取設定檔，然後選取&#x200B;**[!UICONTROL 儲存並關閉]**。 已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全域套用Dynamic Media影像設定檔 {#applying-an-image-profile-globally}

除了將設定檔套用至資料夾外，您還可以全域套用設定檔，以便任何資料夾中上傳至Experience Manager資產的任何內容都會套用選取的設定檔。

若資料夾中已有您後來加以變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 請參閱[在您編輯資料夾中資產的處理設定檔](processing-profiles.md#reprocessing-assets)之後，重新處理該資料夾中的資產。

**全域套用Dynamic Media影像設定檔：**

1. 執行下列任一項作業：

   * 瀏覽至`https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam`並套用適當的設定檔，然後選取&#x200B;**[!UICONTROL 儲存]**。

     ![chlimage_1-257](assets/chlimage_1-257.png)

   * 瀏覽至CRXDE Lite到下列節點： `/content/dam/jcr:content`。

     新增屬性`imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>`並選取&#x200B;**[!UICONTROL 全部儲存]**。

     ![configure_image_profiles](assets/configure_image_profiles.png)

## 編輯單一影像的智慧型裁切或智慧型色票 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>* 智慧型裁切僅適用於Dynamic Media - Scene7模式。

您可以手動重新對齊影像的智慧型裁切視窗或調整其大小，以進一步調整其焦點。

在您編輯智慧型裁切並儲存之後，此變更會傳播到您針對特定影像使用裁切的任何地方。

如有必要，請重新執行智慧型裁切以再次產生其他裁切。

另請參閱[編輯多張影像的智慧型裁切或智慧型色票](#editing-the-smart-crop-or-smart-swatch-of-multiple-images)。

**若要編輯單一影像的智慧型裁切或智慧型色票：**

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL Assets]**，然後導覽至已套用智慧型裁切或智慧型色票影像設定檔的資料夾。
1. 選取資料夾以開啟其內容。
1. 選取您要調整其智慧型裁切或智慧型色票的影像。
1. 在工具列中選取&#x200B;**[!UICONTROL 智慧型裁切]**。

   >[!TIP]
   >
   >使用快速鍵`s`來編輯智慧型裁切或智慧型色票。

1. 執行下列任一項作業：

   * 在頁面的右上角附近，向左或向右拖曳滑桿可分別增加或減少影像顯示。
   * 在影像上，拖曳角落控點來調整裁切或色票的可檢視區域大小。
   * 在影像上，將方塊/色票拖曳到新位置。 您只能編輯影像色票；色票為靜態。
   * 在影像上方，選取&#x200B;**[!UICONTROL 回覆]**&#x200B;以復原所有編輯並還原原始裁切或色票。

1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 儲存]**，然後選取&#x200B;**[!UICONTROL 關閉]**&#x200B;以返回資產的資料夾。

## 編輯多個影像的智慧型裁切或智慧型色票 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>* 智慧型裁切僅適用於Dynamic Media - Scene7模式。

將包含智慧型裁切的「影像設定檔」套用至資料夾後，該資料夾中的所有影像都會套用裁切。 如果需要，您可以&#x200B;*手動*&#x200B;重新對齊多個影像中的智慧型裁切視窗或調整其大小，以進一步調整其焦點。

在您編輯智慧型裁切並儲存之後，此變更會傳播到您針對特定影像使用裁切的任何地方。

如有必要，請重新執行智慧型裁切以再次產生其他裁切。

**若要編輯多重影像的智慧型裁切或智慧型色票：**

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL Assets]**，然後移至已套用智慧型裁切或智慧型色票影像設定檔的資料夾。
1. 在資料夾中，選取&#x200B;**[!UICONTROL 其他動作]** (...)圖示，然後選取&#x200B;**[!UICONTROL 智慧型裁切]**。

1. 在&#x200B;**[!UICONTROL 編輯智慧型裁切]**&#x200B;頁面上，執行下列任一項作業：

   * 調整頁面上影像的檢視大小。

     在中斷點名稱下拉式清單的右側，向左或向右拖曳滑桿以變更可檢視影像顯示的大小。

     ![edit_smart_rances-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根據中斷點名稱篩選可檢視影像清單。 在以下範例中，影像是以中斷點名稱「Medium」進行篩選。

     在頁面的右上角，從下拉式清單中選取中斷點名稱，以篩選您看到的影像。 （請參閱上圖。）

     ![edit_smart_rances-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 調整智慧型裁切方塊的大小。 執行下列任一項作業：

      * 如果影像隻有智慧型裁切或智慧型色票，請在影像上拖曳裁切方塊的邊角控點，以調整裁切可檢視區域的大小。
      * 如果影像同時具有智慧型裁切和智慧型色票，請在影像上拖曳裁切方塊的邊角控點，以調整裁切的可檢視區域大小。 或者，選取影像下方的智慧型色票（色票為靜態），然後拖曳裁切方塊的邊角控點，以調整色票可檢視區域的大小。

     ![調整影像的智慧型裁切大小](assets/edit_smart_crops-resize.png)

   * 移動智慧型裁切方塊。 執行下列任一項作業：

      * 如果影像隻有智慧型裁切或智慧型色票，請在影像上，將裁切方塊拖曳到新位置。
      * 如果影像同時具有智慧型裁切和智慧型色票，請在影像上，將智慧型裁切方塊拖曳到新位置。 或者，選取影像下方的智慧型色票（色票為靜態），然後將智慧型色票裁切方塊拖曳至新位置。

     ![edit_smart_rances-move](assets/edit_smart_crops-move.png)

   * 復原所有編輯並還原原始的智慧型裁切或智慧型色票（僅適用於目前的編輯作業階段）。

     選取影像上方的&#x200B;**[!UICONTROL 回覆]**。

     ![edit_smart_crops-revert](assets/edit_smart_crops-revert.png)

1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 儲存]**，然後選取&#x200B;**[!UICONTROL 關閉]**&#x200B;以返回資產的資料夾。

## 從資料夾中移除Dynamic Media影像設定檔 {#removing-an-image-profile-from-folders}

當您從資料夾中移除「影像描述檔」時，任何子資料夾都會自動繼承從其父資料夾中移除的描述檔。 不過，在資料夾內發生的任何檔案處理作業都會維持不變。

您可以從&#x200B;**[!UICONTROL 工具]**&#x200B;功能表內的資料夾中移除影像設定檔，或者如果您在資料夾中，則可以從&#x200B;**[!UICONTROL 屬性]**&#x200B;中移除影像設定檔。 本節說明如何以兩種方式從資料夾中移除「影像設定檔」。

### 透過設定檔使用者介面，從資料夾中移除Dynamic Media影像設定檔 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 影像設定檔]**。
1. 選取您要從資料夾或多個資料夾移除的影像設定檔。
1. 選取&#x200B;**[!UICONTROL 從資料夾移除處理設定檔]**，然後選取您要用來從中移除設定檔的資料夾或多個資料夾，並選取&#x200B;**[!UICONTROL 移除]**。

   您可以確認「影像設定檔」不再套用至資料夾，因為資料夾名稱下方不再有該名稱。

### 透過「屬性」從資料夾中移除Dynamic Media影像設定檔 {#removing-image-profiles-from-folders-via-properties}

1. 選取Experience Manager標誌並導覽&#x200B;**[!UICONTROL Assets]**，然後移至您要移除其中之影像設定檔的資料夾。
1. 在資料夾中，選取核取記號以選取資料夾，然後選取&#x200B;**[!UICONTROL 屬性]**。
1. 選取&#x200B;**[!UICONTROL 影像設定檔]**&#x200B;標籤。
1. 從&#x200B;**[!UICONTROL 設定檔名稱]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 無]**，然後選取&#x200B;**[!UICONTROL 儲存並關閉]**。

   已為其分配配置檔案的資料夾將通過資料夾名稱正下方的配置檔案名稱顯示來指示。
