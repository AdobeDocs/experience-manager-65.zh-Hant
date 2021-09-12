---
title: 管理Dynamic Media影像預設集
description: 了解Dynamic Media影像預設集，並了解如何建立、修改和管理影像預設集。
uuid: 3e9a7af6-bf49-4cff-b516-0a3ee9765391
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cc1111c4-6e24-4570-9ac7-97c25cf24ede
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/image-presets
feature: Image Presets
role: User, Admin
exl-id: 556b99fe-91c3-441f-ba81-22cb8c10ef7f
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '3839'
ht-degree: 8%

---

# 管理Dynamic Media影像預設集{#managing-image-presets}

影像預設集可讓Adobe Experience Manager Assets以不同大小、不同格式，或透過動態產生的其他影像屬性來動態傳送影像。 每個影像預設集代表用於顯示影像的大小調整和格式設定命令的預定義集合。 建立影像預設集時，您會選擇影像傳送的大小。 您也可以選擇格式設定命令，以便在傳送影像以供查看時優化影像的外觀。

管理員可以建立匯出資產的預設集。 用戶在導出映像時可以選擇預設集，該預設集還會按照管理員指定的規範重新格式化映像。

您也可以建立回應式的影像預設集。 如果您將回應式影像預設集套用至資產，則會根據所檢視的裝置或螢幕大小而變更。 除了RGB或灰色之外，還可以配置影像預設集以在顏色空間中使用CMYK。

本節說明如何建立、修改和一般管理影像預設集。 您可以隨時預覽影像，將影像預設集套用至影像。 請參閱[套用影像預設集](/help/assets/image-presets.md)。

>[!NOTE]
>
>智慧型影像處理可與您現有的影像預設集搭配使用，並會在傳送時的最後毫秒內運用智慧，根據瀏覽器或網路連線速度進一步縮小影像檔案大小。 如需詳細資訊，請參閱[智慧影像](/help/assets/imaging-faq.md)。

## 了解Dynamic Media影像預設集 {#understanding-image-presets}

像宏一樣，「影像預設集」是儲存在名稱下的大小調整和格式設定命令的預定義集合。 若要了解「影像預設集」的運作方式，假設您的網站要求每個產品影像以不同大小、不同格式以及案頭和行動傳送的壓縮率顯示。

>[!NOTE]
>
>在Dynamic Media - Scene7模式中，影像預設集僅支援影像資產。

您可以建立兩個影像預設集：案頭版為500 x 500像素，行動版為150 x 150像素。 您可以建立兩個「影像預設集」，一個稱為`Enlarge`，以500x500像素顯示影像，另一個稱為`Thumbnail`，以150x150像素顯示影像。 要以`Enlarge`和`Thumbnail`大小傳送影像，Experience Manager將查找放大影像預設集和縮圖影像預設集的定義。 然後，Experience Manager會動態地根據每個影像預設集的大小和格式規格產生影像。

動態傳送時大小縮小的影像可能會失去清晰度和細節。 因此，每個影像預設集都包含格式控制項，用於在以特定大小傳送影像時對其進行最佳化。 這些控制項可確保影像在傳送至您的網站或應用程式時清晰清晰銳利。

管理員可以建立影像預設集。 若要建立影像預設集，您可以從草稿開始，也可以從現有的預設集開始，並以新名稱儲存。

## 管理Dynamic Media影像預設集 {#managing-image-presets-1}

您可以點選或按一下Experience Manager標誌以存取全域導覽主控台，然後點選或按一下「工具」圖示，並導覽至&#x200B;**[!UICONTROL 「資產>影像預設集」]**，以管理Experience Manager中的影像預設集。

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>您建立的任何影像預設集在您預覽或傳送資產時，也可以以動態轉譯的形式使用。
>
>在&#x200B;*Dynamic Media - Scene7模式*&#x200B;中，您需要&#x200B;*not*&#x200B;發佈影像預設集，因為影像預設集會自動發佈。
>
>在&#x200B;*Dynamic Media — 混合模式*&#x200B;中，您必須手動發佈影像預設集。
>
>請參閱[發佈影像預設集](#publishing-image-presets)。

>[!NOTE]
>
>當您在資產的「詳細資料檢視」中選取「**[!UICONTROL 轉譯]**」時，系統會顯示各種轉譯。 您可以增加或減少顯示的影像預設集數目。 請參閱[增加顯示](#increasing-or-decreasing-the-number-of-image-presets-that-display)的影像預設集數目。

### 智慧型裁切、Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式 {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

>[!NOTE]
>
>本主題僅適用於Dynamic Media — 混合模式。

如果要支援擷取AI、EPS和PDF檔案，以便生成這些檔案格式的動態格式副本，請在建立影像預設集之前查看以下資訊。

Adobe Illustrator的檔案格式是PDF的變體。 在Experience Manager資產方面，主要差異如下：

* Adobe Illustrator檔案包含單一頁面及多個層。 每個圖層都會擷取為主要Illustrator資產下的PNG子資產。
* PDF文檔由一頁或多頁組成。 每個頁面都會擷取為主多頁PDF檔案下的單一頁面PDF子資產。

整體`DAM Update Asset`工作流程中由`Create Sub Asset process`元件建立的子資產。 若要在工作流程中查看此程式元件，請點選「**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]** > **[!UICONTROL DAM更新資產]** > **[!UICONTROL 編輯]**」。

另請參閱[檢視多頁檔案的頁面](/help/assets/managing-linked-subassets.md#view-pages-of-a-multi-page-file)。

開啟資產時，您可以檢視子資產或頁面，點選「內容」功能表，然後選取&#x200B;**[!UICONTROL 子資產]**&#x200B;或&#x200B;**[!UICONTROL 頁面]**。 子資產。 也就是說，PDF頁面由`Create Sub Asset`工作流程元件擷取。 接著會儲存為主要資產下方的`page1.pdf`、`page2.pdf`等項目。 儲存後， `DAM Update Asset`工作流程會處理它們。

若要使用Dynamic Media來預覽和產生AI、EPS或PDF檔案的動態轉譯，需要下列處理步驟：

1. 在`DAM Update Asset`工作流程中，`Rasterize PDF/AI Image Preview Rendition`處理元件會使用設定的解析度將原始資產的第一頁柵格化為`cqdam.preview.png`轉譯。

1. 然後， `cqdam.preview.png`轉譯會由工作流程內的`Dynamic Media Process Image Assets`處理元件最佳化為PTIFF。

>[!NOTE]
>
>在[!UICONTROL DAM更新資產]工作流程中， **[!UICONTROL EPS縮圖]**&#x200B;步驟會為EPS檔案生成縮圖。

#### PDF/AI/EPS資產中繼資料屬性 {#pdf-ai-eps-asset-metadata-properties}

| **中繼資料屬性** | **說明** |
|---|---|
| `dam:Physicalwidthininches` | 文檔寬度（英吋）。 |
| `dam:Physicalheightininches` | 文檔高度（英吋）。 |

您可以通過`DAM Update Asset`工作流訪問`Rasterize PDF/AI Image Preview Rendition`進程元件選項。

點選左上角的Adobe Experience Manager，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。 在「工作流模型」頁面上，選擇「**[!UICONTROL DAM更新資產]**」，然後在工具欄點選「**[!UICONTROL 編輯]**」。 在[!UICONTROL DAM更新資產]工作流程頁面上，點選兩下`Rasterize PDF/AI Image Preview Rendition`處理元件以開啟其「步驟屬性」對話方塊。

#### 柵格化PDF/AI影像預覽轉譯選項 {#rasterize-pdf-ai-image-preview-rendition-options}

![柵格化PDF或AI工作流的參數](assets/rasterize_pdf_ai_image_preview.png)

柵格化PDF或AI工作流的參數

<table>
 <tbody>
  <tr>
   <td><strong>進程參數</strong></td>
   <td><strong>預設設定</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>Mime 類型</td>
   <td><p>application/pdf</p> <p>application/postscript</p> <p>application/illustrator<br /> </p> </td>
   <td>被視為PDF或Illustrator文檔的文檔mime類型清單。<br /> </td>
  </tr>
  <tr>
   <td>寬度上限</td>
   <td>2048年</td>
   <td>生成的預覽格式副本的最大寬度（像素）。<br /> </td>
  </tr>
  <tr>
   <td>高度上限</td>
   <td>2048年</td>
   <td>生成的預覽格式副本的最大高度（像素）。<br /> </td>
  </tr>
  <tr>
   <td>解析度</td>
   <td>72</td>
   <td>以ppi（每英吋像素）顯示第一頁的解析度。</td>
  </tr>
 </tbody>
</table>

使用預設進程參數，PDF/AI文檔的第一頁柵格化為72 ppi，生成的預覽影像的大小為2048 x 2048像素。 對於一般部署，您可能希望將解析度提高至至少150 ppi或更高。 例如，300 ppi的美國字母大小文檔要求最大寬度和高度分別為2550 x 3300像素。

「最大寬度」和「最大高度」限制柵格化的解析度。 例如，如果最大值未變更，且「解析度」設為300 ppi，則美國信函檔案的光柵化為186 ppi。 也就是說，文檔為1581 x 2046像素。

`Rasterize PDF/AI Image Preview Rendition`進程元件已定義最大值，以確保它不會在記憶體中建立過大的映像。 此類大型映像可能會使提供給JVM(Java™虛擬機)的記憶體溢出。 請務必注意，為JVM提供足夠的記憶體，以管理已配置的並行工作流數，每個工作流都有可能以最大配置的大小建立映像。

### InDesign(INDD)檔案格式 {#indesign-indd-file-format}

如果要支援導入INDD檔案，以便生成此檔案格式的動態格式副本，則在建立影像預設集之前，可能需要查看以下資訊。

對於InDesign檔案，只有在Adobe InDesign Server與Experience Manager整合時，才會擷取子資產。 參考的資產會根據其中繼資料進行連結。 InDesign Server不是連結的必要項目。 不過，在處理InDesign檔案之前，Experience Manager內必須有參考的資產，才會在InDesign檔案與參考的資產之間建立連結。

請參閱[整合Experience Manager資產與InDesign Server](/help/assets/indesign.md)。

`DAM Update Asset`工作流程中的媒體擷取程式元件會執行數個預先設定的擴充指令碼，以處理InDesign檔案。

![媒體擷取程式引數中的ExtendScript路徑](assets/6_5_mediaextractionprocess.png)

ExtendScript會在[!UICONTROL DAM更新資產]工作流程中，路徑為「媒體擷取」程式元件的引數。

下列指令碼供Dynamic Media整合使用：

<table>
 <tbody>
  <tr>
   <td><strong>ExtendScript名稱</strong></td>
   <td><strong>預設</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>ThumbnailExport.jsx</td>
   <td>是</td>
   <td>生成300-ppi <code>thumbnail.jpg</code>轉譯，該轉譯經過優化並由<code>Dynamic Media Process Image Assets</code>進程元件轉換為PTIFF轉譯。<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>是</td>
   <td>為每個頁面產生300 PPI JPEG子資產。 JPEG子資產是儲存在InDesign資產下的實際資產。 此外，還通過<code>DAM Update Asset</code>工作流優化並轉換為PTIFF。<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>否</td>
   <td>為每個頁面產生一個PDF子資產。 PDF子資產會依照先前所述進行處理。 由於PDF僅包含單頁，因此不會產生任何子資產。<br /> </td>
  </tr>
 </tbody>
</table>

## 設定影像縮圖大小 {#configuring-image-thumbnail-size}

您可以在&#x200B;**[!UICONTROL DAM更新資產]**&#x200B;工作流程中配置這些設定，以配置縮圖的大小。 工作流程中有兩個步驟可讓您設定影像資產的縮圖大小。 雖然(**[!UICONTROL Dynamic Media處理影像資產]**)用於動態影像資產，而（**[!UICONTROL 處理縮圖]**）用於靜態縮圖產生，或當所有其他處理無法產生縮圖時，*兩個*&#x200B;必須有相同的設定。

在「動 **[!UICONTROL 態媒體處理影像資產」步驟中]** ，影像伺服器會產生縮圖，此組態與套用至「處理縮圖」步驟的組態無關 **** 。透過「處理縮圖 **[!UICONTROL 」步驟產生縮圖]** ，是建立縮圖的最慢且記憶體最耗用的方式。

縮圖大小定義為下列格式：**[!UICONTROL width:height:center]**，例如`80:80:false`。 寬度和高度會以像素為單位決定縮圖的大小。 中心值為false或true，若設為true，表示縮圖影像的大小與設定中指定的大小完全相同。 如果調整大小的影像較小，則會置於縮圖中。

>[!NOTE]
>
>* EPS檔案的縮圖大小是在「縮圖」下的&#x200B;**[!UICONTROL EPS縮圖]**&#x200B;步驟的&#x200B;**[!UICONTROL 參數]**&#x200B;頁簽中配置的。
>
>* 視訊的縮圖大小是在&#x200B;**[!UICONTROL FFmpeg縮圖]**&#x200B;步驟中，在&#x200B;**[!UICONTROL Process]**&#x200B;標籤的&#x200B;**[!UICONTROL Arguments]**&#x200B;下配置。

>


**若要設定影像縮圖大小：**

1. 點選&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]** > **[!UICONTROL DAM更新資產]** > **[!UICONTROL 編輯]**。
1. 點選&#x200B;**[!UICONTROL Dynamic Media處理影像資產]**&#x200B;步驟，然後點選或按一下&#x200B;**[!UICONTROL 縮圖]**&#x200B;標籤。 視需要變更縮圖大小，然後點選「 **[!UICONTROL 確定]**」。

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. 點選「處 **[!UICONTROL 理縮圖]** 」步驟，然後點選「縮 **[!UICONTROL 圖]** 」標籤。視需要變更縮圖大小，然後點選「 **[!UICONTROL 確定]**」。

   >[!NOTE]
   >
   >「處理縮圖」步驟中縮圖引數中 **[!UICONTROL 的值必須與「動態媒體處理影像資產」]** 步驟中的縮圖引數相符 **** 。

1. 點選&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存對工作流程的變更。

### 增加或減少顯示的Dynamic Media影像預設集數目 {#increasing-or-decreasing-the-number-of-image-presets-that-display}

您建立的影像預設集在您預覽資產時可以動態轉譯。 Experience Manager從&#x200B;**[!UICONTROL 詳細資料檢視>轉譯]**&#x200B;檢視資產時，會顯示各種動態轉譯。 您可以增加或減少顯示的轉譯限制。

**增加或減少顯示的Dynamic Media影像預設集數目：**

1. 導覽至CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 導覽至`/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`處的影像預設集清單節點

   ![increase_deximentenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. 在 **[!UICONTROL limit]** 屬性中，將預設設 ****&#x200B;定為15的值變更為所要的數字。
1. 導航到`/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`的影像預設集資料源

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. 在limit屬性中，將數字變更為所需數字，例如`{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 點選「**[!UICONTROL 儲存全部]**」。

## 建立Dynamic Media影像預設集 {#creating-image-presets}

建立Dynamic Media影像預設集可讓您在預覽或發佈時將這些設定套用至任何影像。

>[!NOTE]
>
>如果使用Internet Explorer 9，建立預設集在儲存後不會立即出現在預設集清單中。 若要解決此問題，請停用IE9的快取。

如果要支援AI、PDF和EPS檔案的獲取，以便生成這些檔案格式的動態格式副本，請在建立影像預設集之前查看以下資訊。
請參閱[Adobe Illustrator(AI)、Postscript(EPS)和PDF檔案格式](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)。

如果要支援導入INDD檔案，以便生成此檔案格式的動態格式副本，則在建立影像預設集之前，可能需要查看以下資訊。
請參閱[InDesign(INDD)檔案格式](#indesign-indd-file-format)。

>[!NOTE]
>
>若要建立Dynamic Media影像預設集，您必須以Experience Manager管理員或Admin Console管理員的身分擁有管理員權限。

**若要建立Dynamic Media影像預設集：**

1. 在Experience Manager中，點選Experience Manager標誌以存取全域導覽主控台，然後點選&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**。
1. 按一下&#x200B;**[!UICONTROL 建立]**。將開啟「**[!UICONTROL 編輯影像預設集]**」窗口。

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >若要讓此影像預設變得自適應，請擦除 **[!UICONTROL 寬度]****[!UICONTROL 和高度欄]** 位中的值，並保留空白。

1. 視需要在「基 **[!UICONTROL 本]** 」和「 **[!UICONTROL 進階]** 」標籤中輸入值，包括名稱。這些選項在「影像預設 [集選項」中概述](#image-preset-options)。預設集會出現在左窗格中，並可與其他資產一起即時使用。

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. 按一下「**[!UICONTROL 儲存]**」。

## 建立回應式影像預設集 {#creating-a-responsive-image-preset}

若要建立回應式影像預設集，請執行[建立影像預設集](#creating-image-presets)中的步驟。 在&#x200B;**[!UICONTROL 編輯影像預設集]**&#x200B;窗口中輸入高度和寬度時，請擦除值並將其留空。

將它們留空會告訴Experience Manager此影像預設集是回應式的。 您可以視需要調整其他值。



>[!NOTE]
>
>若要在套用影像預設集至資產時查看&#x200B;**[!UICONTROL URL]**&#x200B;和&#x200B;**[!UICONTROL RESS]**&#x200B;按鈕，必須發佈資產。
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>在Dynamic Media - Scene7模式中，會自動發佈影像預設集和影像資產。
>
>在Dynamic Media — 混合模式中，您必須手動發佈影像預設集和影像資產。

### 影像預設集選項 {#image-preset-options}

建立或編輯影像預設集時，您有本節所述的選項。 此外，Adobe建議以下「最佳做法」選項作為開始：

* **[!UICONTROL 格式]** (基本&#x200B;**** 頁簽) — 選擇 **** JPEG或其它符合您要求的格式。所有網頁瀏覽器都支援JPEG影像格式；它在小檔案大小和影像品質之間提供良好的平衡。但是，JPEG格式影像使用有損壓縮方案，如果壓縮設定太低，則該壓縮方案會引入不想要的影像偽影。因此，Adobe建議將壓縮品質設為75。此設定在影像品質和檔案大小之間取得良好的平衡。

* **[!UICONTROL 啟用簡單銳利化]** -請勿選取「啟用簡 **** 單銳利化」 (此銳利化濾鏡提供的控制力比「非銳利化遮色片」設定少)。

* **[!UICONTROL 銳利化：重新取樣模]** 式 — 選 **[!UICONTROL 取雙三次]**。

#### 基本索引標籤選項 {#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>欄位</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><strong>名稱</strong></td>
   <td>輸入描述性名稱，不含任何空格。 在名稱中加入影像大小規格，協助使用者識別此影像預設集。</td>
  </tr>
  <tr>
   <td><strong>寬度和高度</strong></td>
   <td>以像素輸入影像傳送的大小。 寬度和高度必須大於0像素。 如果其中一個值為0，則不會建立任何預設集。 如果兩個值皆空白，則會建立回應式影像預設集。</td>
  </tr>
  <tr>
   <td><strong>格式</strong></td>
   <td><p>從功能表中選擇格式。</p> <p>選擇<strong>JPEG</strong>提供以下附加選項：</p>
    <ul>
     <li><strong>品質</strong>  — 控制JPEG壓縮級別。此設定會同時影響檔案大小和影像品質。 JPEG質量比例為1-100。 拖曳滑桿時，比例會顯示。</li>
     <li><strong>啟用JPG色度下採樣</strong>  — 由於眼睛對高頻顏色資訊的敏感度比高頻亮度低，因此JPEG影像將影像資訊劃分為亮度和顏色分量。當壓縮JPEG影像時，亮度分量以全解析度保持，而顏色分量通過平均一組像素來縮減採樣。 縮減取樣會將資料量減少一半或三分之一，幾乎不會影響感知的品質。 縮減採樣不適用於灰度影像。 此技術可減少對具有高對比度的影像（例如具有重疊文字的影像）有用的壓縮量。</li>
    </ul>
    <div>
      選擇
     <strong>GIF</strong>或
     <strong>含alpha</strong>的GIF提供以下額外功能
     <strong>GIF顏色量化</strong>選項：
    </div>
    <ul>
     <li><strong>類 </strong>型 — 選 <strong>取「適應性」</strong> （預設值）、 <strong>「Web」</strong>或「 <strong>Macintosh」</strong>。如果選擇<strong>Alpha</strong>的GIF，則Macintosh選項不可用。</li>
     <li><strong>Dither</strong>  — 選取「 <strong></strong> 差 <strong>異」或「關閉」</strong>。</li>
     <li><strong>顏色數 </strong>量 — 輸入從2到256的數字。</li>
     <li><strong>顏色清單</strong>  — 輸入逗號分隔的清單。例如，對於白色、灰色和黑色，請輸入<code>000000,888888,ffffff</code>。</li>
    </ul>
    <div>
      選擇
     <strong>PDF</strong>,
     <strong>TIFF</strong>，或
     <strong>含Alpha</strong>的TIFF提供以下額外選項：
    </div>
    <ul>
     <li><strong>壓縮</strong>  — 選取壓縮演算法。PDF的演算法選項為<strong>None</strong>、<strong>Zip</strong>和<strong>Jpeg</strong>;對於TIFF，選項為<strong>None</strong>、<strong>LZW</strong>、<strong>Jpeg</strong>和<strong>Zip</strong>;而Alpha的TIFF為<strong>None</strong>、<strong>LZW</strong>和<strong>Zip</strong>。</li>
    </ul> <p>選擇<strong>PNG</strong>、<strong>帶Alpha的PNG、</strong>或<strong>EPS</strong>不提供其他選項。</p> </td>
  </tr>
  <tr>
   <td><strong>銳利化</strong></td>
   <td>選擇<strong>「啟用簡單銳利化」</strong>選項，以便在所有縮放發生後將基本銳利化濾鏡應用到影像。銳利化有助於補償以不同大小顯示影像時可能產生的模糊性。 </td>
  </tr>
 </tbody>
</table>

#### 進階索引標籤選項 {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>欄位</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><strong>色域</strong></td>
   <td>為顏色空間選擇<strong>RGB、CMYK、</strong>或<strong>灰度</strong>。</td>
  </tr>
  <tr>
   <td><strong>色彩設定檔</strong></td>
   <td>如果資產與工作設定檔不同，請選取應轉換為的輸出色域設定檔。</td>
  </tr>
  <tr>
   <td><strong>渲染方法</strong></td>
   <td>您可以覆寫預設的呈現方式。 渲染意圖確定目標顏色配置檔案中無法再現的顏色（超出色域）的結果。 如果「渲染目的」與ICC配置檔案不相容，則將忽略它。
    <ul>
     <li>選擇<strong>感知</strong>以當原始影像中的一個或多個顏色超出目標顏色空間的色域時，將總色域從一個顏色空間壓縮到另一個顏色空間。</li>
     <li>當當前顏色空間中的顏色在目標顏色空間中超出色域時，選擇<strong>相對比色</strong>。 而且，您希望將其映射到目標顏色空間的色域內最接近的可能顏色，而不影響任何其他顏色。 </li>
     <li>如果要在轉換為目標顏色空間時重現原始影像顏色飽和度，請選擇<strong>飽和度</strong>。 </li>
     <li>選擇「<strong>絕對比色</strong>」以完全匹配顏色，而不調整會改變影像亮度的白點或黑點。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>黑點補償</strong></td>
   <td>如果輸出配置檔案支援此功能，請選擇此選項。 如果黑點補償與指定的ICC配置檔案不相容，則會忽略它。</td>
  </tr>
  <tr>
   <td><strong>正在遞色</strong></td>
   <td>選擇此選項以可能避免或減少色帶偽影。 </td>
  </tr>
  <tr>
   <td><strong>銳利化類型</strong></td>
   <td><p>選擇「<strong>無</strong>」、「<strong>銳利化</strong>」或「<strong>銳利化遮色片</strong>」。 </p>
    <ul>
     <li>如果要禁用銳利化，請選擇<strong>無</strong>。</li>
     <li>如果要在所有縮放發生後將基本銳利化濾鏡應用到影像，請選擇<strong>銳利化</strong>。 銳利化有助於補償以不同大小顯示影像時可能產生的模糊性。 </li>
     <li>如果要對最終縮減採樣影像微調銳利化濾鏡效果，請選擇「銳利化遮色片」</strong>。 <strong>您可以控制效果的強度、效果半徑（以像素計量），以及忽略的對比度臨界值。 此效果使用的選項與 Photoshop的「遮色片銳利化」濾鏡相同。</strong></li>
    </ul> <p>在<strong>銳利化遮色片</strong>中，您有下列選項：</p>
    <ul>
     <li><strong>量</strong>  — 控制套用至邊緣像素的對比度量。預設的實數值為1.0。對於高解析度影像，您可以將其增加到高達5.0。請將「量」想像為濾鏡強度的度量。</li>
     <li><strong>半徑</strong>  — 決定影響銳利化的邊緣像素周圍的像素數。對於高解析度影像，請輸入從1到2的實數。 低值只會銳化邊緣像素；高值銳化較寬的像素帶。 正確值取決於影像的大小。</li>
     <li><strong>臨界值</strong>  — 決定套用遮色片銳利化濾鏡時要忽略的對比度範圍。換句話說，此選項可決定銳化像素與周圍區域的差異程度，之後才會被視為邊緣像素且銳化。 為避免引入雜訊，請使用2到20的整數值進行實驗。 </li>
     <li><strong>套用至</strong>  — 判斷未銳利化套用至每種顏色或亮度。</li>
    </ul>
    <div>
      銳利化在
     <a href="https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf">銳利化影像</a>。
    </div> </td>
  </tr>
  <tr>
   <td><strong>重新取樣模式</strong></td>
   <td>選擇<strong>重新採樣模式</strong>選項。 這些選項會在縮減取樣時銳化影像：
    <ul>
     <li><strong>雙線性</strong>  — 最快的重新取樣方法。某些鋸齒偽影是可以注意到的。</li>
     <li><strong>雙立方體</strong>  — 增加CPU使用量，但產生更銳利的影像，並產生較少明顯的鋸齒偽影。</li>
     <li><strong>Sharp2</strong>  — 產生的結果比雙立方體稍銳，但CPU成本更高。</li>
     <li><strong>Bi-Sharp</strong>  — 選取Photoshop預設重新取樣器以縮小影像大小，稱為 <strong>雙</strong> 立方體Adobe Photoshop。</li>
     <li><strong>每</strong> 種色彩 <strong>和亮度</strong>  — 每種方法皆可依據顏色或亮度。預設情況下，選擇<strong>每個顏色</strong>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>打印解析度</strong></td>
   <td>選擇用於打印此影像的解析度；預設為72像素。</td>
  </tr>
  <tr>
   <td><strong>影像修飾元</strong></td>
   <td><p>除了UI中可用的通用影像設定，Dynamic Media支援許多進階影像修改，您可以在<strong>影像修飾元</strong>欄位中指定。 這些參數在<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api">Image Server協定命令引用</a>中定義。</p> <p>重要：不支援API中列出的下列功能：</p>
    <ul>
     <li>基本模板和文本呈現命令：<code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code>和 <code>textPs=</code></li>
     <li>本地化命令：<code>locale=</code>和 <code>req=xlate</code></li>
     <li><code>req=set</code> 無法用於一般用途。</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>非核心Dynamic Media服務：SVG、影像呈現和Web-to-Print</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 使用影像修飾元定義影像預設集選項 {#defining-image-preset-options-with-image-modifiers}

除了「基本」和「進階」索引標籤中可用的選項外，您還可以定義影像修飾元，以在定義影像預設集時提供更多選項。 影像呈現仰賴於[HTTP通訊協定參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api)中詳細定義的影像呈現API。

以下是一些您可以使用影像修飾元的基本範例。

>[!NOTE]
>
>某些影像修飾元[無法用於Experience Manager](#advanced-tab-options)。

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html#image-serving-api)  — 反轉每個顏色分量以獲得負影像效果。

   ```xml
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html#image-serving-api)  — 對影像套用模糊篩選。

   ```xml
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* 組合命令 — op_blur和op-invert

   ```xml
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html#image-serving-api)  — 降低或增加亮度。

   ```xml
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html#image-serving-api)  — 調整影像不透明度。可讓您降低前景不透明度。

   ```xml
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

## 編輯影像預設集 {#modifying-image-presets}

1. 在Experience Manager中，點選Experience Manager標誌以存取全域導覽主控台，然後點選&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**。

   ![6_5_imagepreset_editpreset](assets/6_5_imagepreset-editpreset.png)

1. 選取預設集，然後按一下「**[!UICONTROL 編輯]**」。 將開啟「**[!UICONTROL 編輯影像預設集]**」窗口。
1. 進行更改，然後按一下「保存&#x200B;****」以保存更改，或按一下「取消&#x200B;****」以取消更改。

## 發佈Dynamic Media影像預設集 {#publishing-image-presets}

如果您執行的是Dynamic Media — 混合模式，您必須手動發佈影像預設集。

(如果您執行的是Dynamic Media - Scene7模式，則會自動發佈影像預設集；您不需要完成這些步驟。)

**若要在Dynamic Media — 混合模式中發佈影像預設集：**

1. 在Experience Manager中，點選或按一下Experience Manager標誌以存取全域導覽主控台，點選或按一下「工具」圖示，並導覽至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Image Presets]**。
1. 從影像預設集清單中選取影像預設集或多個影像預設集，然後按一下或點選&#x200B;**[!UICONTROL Publish]**。
1. 影像預設集發佈後，狀態會從未發佈變更為已發佈。

   ![chlimage_1-81](assets/chlimage_1-505.png)

## 刪除Dynamic Media影像預設集 {#deleting-image-presets}

1. 在Experience Manager中，點選或按一下Experience Manager標誌以存取全域導覽主控台。
1. 點選&#x200B;**[!UICONTROL 工具]**&#x200B;圖示，然後導覽至&#x200B;**[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**。
1. 選取預設集，然後按一下&#x200B;**[!UICONTROL Delete]**。 Dynamic Media會確認您要刪除它。 點選&#x200B;**[!UICONTROL 刪除]**&#x200B;以刪除，或點選&#x200B;**[!UICONTROL 取消]**&#x200B;以中止。
