---
title: 配置Dynamic Media一般設定
description: 了解如何在Dynamic Media中管理一般設定。 您可以在此處設定發佈伺服器名稱和來源伺服器名稱，並設定影像覆寫選項。 還有預設的影像遮色片銳利化上傳選項，以及要如何處理PostScript、Adobe Photoshop、PDF和Adobe Illustrator檔案的上傳選項。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: null
source-git-commit: 1b853936760daf7ee8d16ba926e612dadec40788
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 4%

---


# 配置Dynamic Media一般設定

設定 **[!UICONTROL Dynamic Media一般設定]** 僅適用於：

* 您以Scene7模式執行Dynamic Media。 請參閱 [在Scene7模式中啟用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* 您有 *現有* **[!UICONTROL Dynamic Media設定]** (在 **[!UICONTROL Cloud Services]**)(在Adobe Experience Manager 6.5.11或更新版本中)。 請參閱 [在Cloud Services中建立Dynamic Media設定](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* 您是具有管理員權限的Experience Manager系統管理員。

Dynamic Media一般設定適用於經驗豐富的網站開發人員和程式設計人員。 Adobe Dynamic Media建議變更這些發佈設定的使用者熟悉Adobe Experience Manager上的Dynamic Media和基本影像技術。

在建立帳戶時，AdobeDynamic Media會自動為您的公司提供指派的伺服器。 這些伺服器可用來建構您網站和應用程式的URL字串。 這些URL呼叫是您的帳戶專屬的。

「Dynamic Media發佈設定」頁面會建立預設設定，決定如何將AdobeDynamic Media伺服器傳遞至網站或應用程式。 如果未指定任何設定，AdobeDynamic Media伺服器會根據Dynamic Media發佈設定頁面上設定的預設設定來傳送資產。

另請參閱 [選用 — Dynamic Media的設定和設定 — Scene7模式設定](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) 以了解更多可選配置任務。

>[!NOTE]
>
>在Adobe Experience Manager上從Dynamic Media Classic升級至Dynamic Media? 「一般設定」頁面和 [發佈設定](/help/assets/dm-publish-settings.md) Dynamic Media中的頁面會預先填入來自Dynamic Media Classic帳戶的值。 例外是列於 **[!UICONTROL 預設上傳選項]** 「一般設定」頁面的區域。 這些值已處於Experience Manager。 因此，您在 **[!UICONTROL 預設上傳選項]**，則會透過Experience Manager使用者介面，反映在Dynamic Media中，而非Dynamic Media Classic中。 「一般設定」頁面和 [發佈設定](/help/assets/dm-publish-settings.md) 頁面會在Dynamic Media Classic和Dynamic Media之間Experience Manager時進行維護。

**設定Dynamic Media一般設定：**

1. 在「Experience Manager作者」模式中，選取Experience Manager標誌以存取全域導覽主控台。
1. 在左側邊欄中，選取「工具」圖示，然後前往 **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media一般設定]**.
1. 在「伺服器」頁面中，設定 **[!UICONTROL 已發佈的伺服器名稱]** 和 **[!UICONTROL 源伺服器名稱]**，然後使用五個標籤來設定「影像編輯」和「Postscript」、「Photoshop」、「PDF」和「Illustrator」檔案的預設上傳選項。

   * [伺服器](#server-general-setting)
   * [上傳至應用程式](#upload-to-application)
   * [影像編輯](#image-editing-tab) 標籤
   * [PostScript](#postscript-tab) 標籤
   * [Photoshop](#photoshop-tab) 標籤
   * [PDF](#pdf-tab) 標籤
   * [Illustrator](#illustrator-tab) 標籤

   ![Dynamic Media一般設定頁面](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media一般設定頁面，**[!UICONTROL 影像編輯]**頁簽。*<br><br>

1. 完成後，在頁面右上角附近選取 **[!UICONTROL 儲存]**.

## 伺服器 {#server-general-setting}

在建立帳戶時，AdobeDynamic Media會自動為您的公司提供指派的伺服器。 這些伺服器可用來建構您網站和應用程式的URL字串。 這些URL呼叫是您的帳戶專屬的。

| 選項 | 說明 |
| --- | --- |
| **[!UICONTROL 已發佈的伺服器名稱]** | 必要.<br>名稱必須使用 `https://` 在路徑中。<br>此伺服器是即時CDN（內容傳遞網路）伺服器，用於您帳戶專屬的所有系統產生URL呼叫。 除非Adobe技術支援指示您更改此伺服器名稱，否則請勿更改此伺服器名稱。 |
| **[!UICONTROL 原始伺服器名稱]** | 必要.<br>此伺服器僅用於質量保證測試。 除非Adobe技術支援指示更改此伺服器名稱，否則請勿更改此伺服器名稱。 |

## 上傳至應用程式 {#upload-to-application}

* **[!UICONTROL 覆寫影像]**

   AdobeDynamic Media不允許兩個檔案具有相同名稱。 每個項目的AdobeDynamic Media ID（影像名稱減去副檔名）必須是唯一的。 因為這個規則， **[!UICONTROL 上傳至應用程式]** 有覆寫。 此選項的確切效果取決於您選擇的指定「覆寫影像」選項。 這些選項指定替換影像的上傳方式：是替換原始影像，還是變成重複影像。 重複影像會以 `-1`. 例如， `chair.tif` 已重新命名 `chair-1.tif`. 這些選項會影響上傳到與原始資料夾不同的資料夾的影像，或具有與原始資料夾不同副檔名的影像，例如JPG、TIF或PNG。

   | 覆寫影像選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 在目前檔案夾中有基底名稱/副檔名相同者時予以覆寫]** | 僅新Dynamic Media帳戶的預設值。<br>此選項是最嚴格的取代規則。 它要求您將取代影像上傳至與原始影像相同的資料夾，且取代影像的副檔名與原始影像相同。 若不符合這些要求，則會建立重複項目。 |
   | **[!UICONTROL 在目前檔案夾中有基本名稱相同者 (無論副檔名為何) 時予以覆寫]** | 需要您將取代影像上傳至與原始檔案相同的資料夾，但副檔名可能與原始檔案不同。 例如， chair.tif會取代chair.jpg。 |
   | **[!UICONTROL 任何檔案夾內若有基本資產名稱/副檔名相同者，將予以覆寫]** | 需要替換影像的副檔名與原始影像相同（例如chair.jpg必須替換chair.jpg，而不是chair.tif）。 不過，您可以將取代影像上傳至與原始影像不同的資料夾。 更新後的影像位於新資料夾中；在檔案的原始位置找不到該檔案。 |
   | **[!UICONTROL 任何檔案夾內若有基本資產名稱相同者 (無論副檔名為何)，將予以覆寫]** | 此選項是最包容的取代規則。 您可以將取代影像上傳至與原始檔案不同的資料夾、以不同副檔名上傳檔案，然後取代原始檔案。 如果原始檔案位於不同的資料夾中，則替換影像位於上載到的新資料夾中。 |

* **[!UICONTROL 保留裁切]**

   控制任何現有手動裁切定義的保留。

   另請參閱 `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) 和 [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)，兩者皆在Dynamic Media檢視器參考指南中。

## 預設上傳選項 {#default-upload-options}

### 影像編輯標籤 {#image-editing-tab}

此篩選器可讓您微調最終縮減取樣影像的銳利化濾鏡效果。 它可協助您控制效果的強度、效果半徑（如以像素計量），以及忽略的對比度臨界值。

「遮色片銳利化」效果使用的選項與Photoshop的「遮色片銳利化」濾鏡相同。 與名稱相反，「遮色片銳利化」是銳利化濾鏡。

| 遮色片不銳利化選項 | 說明 |
| --- | --- |
| **[!UICONTROL 數量]** | 必要.<br>控制套用至邊緣像素的對比度。<br>把它想成效果的強度。 在「AdobeDynamic Media」中，「遮色片銳利化」的量值與在「Adobe Photoshop」中的量值之間的主要差異，是Photoshop的量範圍介於1%到500%之間。 而在AdobeDynamic Media中，值範圍為 `0.0` to `5.0`. AdobeDynamic Media中的5.0值大致等於Photoshop中的500%;值0.9等於90%，以此類推。 |
| **[!UICONTROL 半徑]** | 必要.<br>控制效果的半徑。<br>值範圍是 `0` to `250`. 此效果在影像中的所有像素上運行，並從所有方向的所有像素輻射出來。 半徑以像素計量。 例如，若要獲得類似於2000 x 2000像素影像和500 x 500像素影像的銳利化效果，您可以在2000 x 2000像素影像上設定兩個像素的半徑。 然後在500 x 500像素影像上設定一個像素的半徑值。 較大的值用於具有較多像素的影像。 |
| **[!UICONTROL 臨界值]** | 必要.<br>臨界值是套用遮色片銳利化濾鏡時會忽略的對比範圍。 這種效果非常重要，這樣在使用此濾波器時，影像就不會引入「雜訊」。 值範圍是 `0` - `255`，即灰度影像中的亮度步驟數。 `0`=黑色， `128`=50%灰色， `255`=white。<br>閾值為 `12` 忽略稍微變化的是膚色亮度以避免加噪，但仍然會為對比區域增加邊緣對比度，例如睫毛與皮膚相遇的區域。<br>如果您有某人的臉部照片，「銳利化遮色片」會影響影像的對位部分。 例如，睫毛和皮膚會聚形成明顯的對比區域，皮膚本身也是光滑的。 即使最平滑的皮膚也表現出亮度值的細微變化。 如果您未使用臨界值，濾鏡會強調外觀像素中的這些細微變化。 然後，產生噪音和不期望的效果，同時增加對睫毛的對比度，增強銳度。<br>為避免此問題，會引入臨界值，告知篩選器忽略不會大幅改變對比度的像素，例如平滑外觀。<br>在前面顯示的拉鍊圖中，注意拉鍊旁邊的紋理。 由於閾值太低，無法抑制雜訊，因此會產生影像雜訊。 |
| **[!UICONTROL 單色]** | 選擇以取消銳利化遮色片影像亮度（強度）。<br>取消選取「 」，將每個顏色元件分別遮色片銳利化。 |

另請參閱 [在AdobeDynamic Media和影像伺服器上銳化影像](/help/assets/assets/sharpening_images.pdf).

### PostScript索引標籤 {#postscript-tab}

您可以柵格化Adobe PostScript®檔案、維護透明背景、選擇解析度，以及選擇顏色空間。

您可以在AdobeDynamic Media中使用Adobe PostScript®(EPS)檔案。 AdobeDynamic Media會在您上傳這些檔案時提供設定這些檔案的命令。

上傳PostScript(EPS)影像檔案時，可以以多種方式格式化它們。 您可以柵格化檔案、維護透明背景、選擇解析度和選擇顏色空間。

| PostScript選項 | 說明 |
| --- | --- |
| **[!UICONTROL 處理]** | 選擇柵格化將檔案中的向量圖形轉換為點陣圖格式。 |
| **[!UICONTROL 在演算後的影像中保留透明背景]** | 保留檔案的背景透明度。 |
| **[!UICONTROL 解析度 (像素/英吋)]** | 確定解析度設定。 此設定決定檔案中每英吋顯示的像素數。 |
| **[!UICONTROL 色域]** | · **[!UICONTROL 自動檢測]**  — 保留檔案的顏色空間。<br>· **[!UICONTROL 強制為RGB]**  — 轉換為RGB顏色空間。<br>· **[!UICONTROL 強制為CMYK]**  — 轉換為CMYK顏色空間。<br>· **[!UICONTROL 強制為灰度]**  — 轉換為灰度顏色空間。 |

### Photoshop標籤 {#photoshop-tab}

您可以從Adobe® Photoshop®檔案建立範本、維護圖層、指定圖層的命名方式、擷取文字，以及指定如何將影像錨定到範本中。

| Photoshop選項 | 說明 |
| --- | --- |
| **[!UICONTROL 保留圖層]** | 將PSD中的圖層（如果有的話）分割為個別資產。 資產層仍與PSD相關聯。 您可以在「詳細資訊視圖」中開啟PSD檔案並選取圖層面板來查看它們。 請參閱在PSD檔案中查看和編輯圖層。 |
| **[!UICONTROL 建立範本]** | 從PSD檔案中的圖層建立模板。 |
| **[!UICONTROL 擷取文字]** | 擷取文字，讓使用者能在檢視器中搜尋文字。 |
| **[!UICONTROL 延伸圖層以符合背景大小]** | 將撕開的影像層的大小擴展到背景層的大小。 |
| **[!UICONTROL 圖層命名]** | 將撕開的影像層的大小擴展到背景層的大小。<br>· **[!UICONTROL 圖層名稱]**  — 在影像的圖層名稱后面命名PSD檔案。 例如，原始PSD檔案中名為「價格標籤」的圖層會變成名為「價格標籤」的影像。 但是，如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱（背景、第1層、第2層等），則影像的名稱將以PSD檔案中的圖層號命名。 <br>· **[!UICONTROL Photoshop和圖層編號]**  — 在PSD檔案中的圖層編號後命名影像，忽略原始圖層名稱。 影像的名稱為Photoshop檔案名稱及附加的圖層編號。 例如，檔案的第二層稱為 `Spring Ad.psd` 已命名 `Spring Ad_2` 即使在Photoshop中有非預設名稱。<br>· **[!UICONTROL Photoshop和圖層名稱]**  — 在PSD檔案後面加上圖層名稱或圖層編號的影像名稱。 如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱，則使用圖層號。 例如，名為 `Price Tag` 在名為的PSD檔案中 `SpringAd` 已命名 `Spring Ad_Price Tag`. 名為「第2層」的預設名稱為 `Spring Ad_2`. |
| **[!UICONTROL 錨點]** | 指定如何將影像錨定在從PSD檔案生成的分層合成生成的模板中。 預設情況下，錨點為中心。 中心錨點允許替換影像最好地填充相同的空間，而不管替換影像的長寬比如何。 當參考範本並使用參數替代時，具有替代此影像的不同方面的影像會有效佔據相同的空間。 如果您的應用程式需要替換影像以填充模板中已分配的空間，請更改為其他設定。 |

### PDF標籤 {#pdf-tab}

您可以選擇柵格化檔案、提取搜索詞和連結、設定解析度，以及選擇顏色空間。

| PDF選項 | 說明 |
| --- | --- |
| **[!UICONTROL 處理]** | · **[!UICONTROL 無]**  — 不會處理PDF。<br>· **[!UICONTROL 縮圖]**  — 將PDF檔案中的每個頁面翻轉為縮圖影像。<br> · **[!UICONTROL 光柵化]**  — 拆分PDF檔案中的頁面，並將向量圖形轉換為點陣圖影像。 若要建立eCatalog，請選擇此選項。 |
| **[!UICONTROL 提取]** | · **[!UICONTROL 無]**  — 不會從PDF中擷取搜尋字詞或連結。<br>· **[!UICONTROL 搜尋字詞]**  — 從PDF檔案中提取搜索詞，以便在eCatalog查看器中按關鍵字搜索該檔案。<br>· **[!UICONTROL 連結]**  — 從PDF檔案中提取連結，並將其轉換為eCatalog檢視器中使用的影像地圖。<br>· **[!UICONTROL 搜尋字詞和連結]**  — 擷取搜尋字詞和連結，以用於eCatalog檢視器。 |
| **[!UICONTROL 解析度 (像素/英吋)]** | 確定解析度設定。 此設定決定每英吋顯示的PDF檔案像素數。 預設為150。 |
| **[!UICONTROL 色域]** | · **[!UICONTROL 自動檢測]**  — 維護PDF檔案的顏色空間。<br>· **[!UICONTROL 強制為RGB]**  — 轉換為RGB顏色空間。<br>· **[!UICONTROL 強制為CMYK]**  — 轉換為CMYK顏色空間。<br>· **[!UICONTROL 強制為灰度]**  — 轉換為灰度顏色空間。 |

### Illustrator標籤 {#illustrator-tab}

您可以柵格化Adobe Illustrator®檔案、維護透明背景、選擇解析度，以及選擇顏色空間。

您可以在AdobeDynamic Media中使用Adobe® Illustrator®(AI)檔案。 AdobeDynamic Media會在您上傳這些檔案時提供設定這些檔案的命令。

上傳Illustrator(AI)影像檔案時，可以使用各種方式來格式化它們。 您可以柵格化檔案、維護透明背景、選擇解析度和選擇顏色空間。 在「上傳工作選項」方塊的「PostScript選項」和「Illustrator選項」下的「上傳」畫面上，可使用格式化PostScript和Illustrator檔案的選項。


| Illustrator選項 | 說明 |
| --- | --- |
| **[!UICONTROL 處理]** | 選擇柵格化將檔案中的向量圖形轉換為點陣圖格式。 |
| **[!UICONTROL 在演算後的影像中保留透明背景]** | 保留檔案的背景透明度。 |
| **[!UICONTROL 解析度 (像素/英吋)]** | 確定解析度設定。 此設定決定檔案中每英吋顯示的像素數。 |
| **[!UICONTROL 色域]** | · **[!UICONTROL 自動檢測]**  — 保留檔案的顏色空間。<br>· **[!UICONTROL 強制為RGB]**  — 轉換為RGB顏色空間。<br>· **[!UICONTROL 強制為CMYK]**  — 轉換為CMYK顏色空間。<br>· **[!UICONTROL 強制為灰度]**  — 轉換為灰度顏色空間。 |
