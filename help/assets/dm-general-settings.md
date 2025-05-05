---
title: 配置Dynamic Media一般設定
description: 瞭解如何在Dynamic Media中管理一般設定。 您可以在此處設定您的發佈伺服器名稱和原始伺服器名稱，並設定影像覆寫選項。 此外，還有預設的上傳選項可讓您對影像進行遮色片銳利化調整，以及上傳選項讓您以何種方式處理PostScript、Adobe Photoshop、PDF和Adobe Illustrator檔案。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 0%

---

# 配置Dynamic Media一般設定

設定&#x200B;**[!UICONTROL Dynamic Media一般設定]**&#x200B;僅適用於下列情況：

* 您正在以Scene7模式執行Dynamic Media。 請參閱[在Scene7模式中啟用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode)。
* 您在Adobe Experience Manager 6.5.11或更新版本中有&#x200B;*現有* **[!UICONTROL Dynamic Media設定]** (在&#x200B;**[!UICONTROL 個Cloud Service]**&#x200B;中)。 請參閱[在Cloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)中建立Dynamic Media設定。
* 您是具有管理員許可權的Experience Manager系統管理員。

Dynamic Media一般設定適用於有經驗的網站開發人員和程式設計人員。 Adobe Dynamic Media建議變更這些發佈設定的使用者熟悉Adobe Experience Manager上的Dynamic Media和基本影像技術。

建立帳戶時，AdobeDynamic Media會自動提供指派給貴公司的伺服器。 這些伺服器可用來建構您網站和應用程式的URL字串。 這些URL呼叫特定於您的帳戶。

Dynamic Media Publish設定頁面會建立預設設定，用來決定如何從AdobeDynamic Media伺服器將資產傳送至網站或應用程式。 如果未指定設定，AdobeDynamic Media伺服器會根據Dynamic Media Publish設定頁面上設定的預設設定傳送資產。

另請參閱[選擇性 — Dynamic Media的設定和組態 — Scene7模式設定](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)，以取得更多選擇性組態工作。

>[!NOTE]
>
>在Adobe Experience Manager上從Dynamic Media Classic升級為Dynamic Media？ Dynamic Media中的「一般設定」頁面和[Publish設定](/help/assets/dm-publish-settings.md)頁面已預先填入從您的Dynamic Media Classic帳戶中取得的值。 例外情況是「一般設定」頁面的&#x200B;**[!UICONTROL 預設上傳選項]**&#x200B;區域下列出的所有值。 這些值已在Experience Manager中。 因此，您透過Experience Manager使用者介面在5個標籤中的任一個標籤上，於&#x200B;**[!UICONTROL 預設上傳選項]**&#x200B;下所做的任何變更都會反映在Dynamic Media中，而非Dynamic Media Classic中。 Experience Manager時，「一般設定」頁面和[Publish設定](/help/assets/dm-publish-settings.md)頁面中的所有其他設定和值都會在Dynamic Media Classic和Dynamic Media之間維護。

**若要設定Dynamic Media一般設定：**

1. 在Experience Manager作者模式中，選取Experience Manager標誌以存取全域導覽主控台。
1. 在左側邊欄中，選取「工具」圖示，然後前往&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media一般設定]**。
1. 在「伺服器」頁面中，設定您的&#x200B;**[!UICONTROL 已發佈的伺服器名稱]**&#x200B;和&#x200B;**[!UICONTROL 原始伺服器名稱]**，然後使用這五個索引標籤來設定「影像編輯」以及Postscript、Photoshop、PDF和Illustrator檔案的預設上傳選項。

   * [伺服器](#server-general-setting)
   * [上傳至應用程式](#upload-to-application)
   * [影像編輯](#image-editing-tab)索引標籤
   * [PostScript](#postscript-tab)索引標籤
   * [Photoshop](#photoshop-tab)索引標籤
   * [PDF](#pdf-tab)索引標籤
   * [Illustrator](#illustrator-tab)索引標籤

   ![Dynamic Media一般設定頁面](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media一般設定頁面，已選取&#x200B;**[!UICONTROL 影像編輯]**&#x200B;索引標籤。*<br><br>

1. 完成後，在頁面的右上角附近，選取&#x200B;**[!UICONTROL 儲存]**。

## 伺服器 {#server-general-setting}

建立帳戶時，AdobeDynamic Media會自動提供指派給貴公司的伺服器。 這些伺服器可用來建構您網站和應用程式的URL字串。 這些URL呼叫特定於您的帳戶。

| 選項 | 說明 |
| --- | --- |
| **[!UICONTROL 已發佈的伺服器名稱]** | 必填。<br>名稱在路徑中必須使用`https://`。<br>此伺服器是所有系統產生、特定於您帳戶的URL呼叫中所使用的即時CDN （內容傳遞網路）伺服器。 請勿變更此伺服器名稱，除非Adobe技術支援指示您這麼做。 |
| **[!UICONTROL 原始伺服器名稱]** | 必填。<br>此伺服器僅用於品質保證測試。 除非得到Adobe技術支援的指示，否則請勿變更此伺服器名稱。 |

## 上傳至應用程式 {#upload-to-application}

* **[!UICONTROL 覆寫影像]**

  Adobe Dynamic Media不允許兩個檔案具有相同名稱。 每個專案的AdobeDynamic Media ID （影像名稱減去副檔名）必須是唯一的。 因為此規則，**[!UICONTROL 上載至應用程式]**&#x200B;發生覆寫。 此選項的確切效果取決於您選擇的指定「覆寫影像」選項。 這些選項會指定取代影像的上傳方式：取代原始影像，還是成為重複影像。 重複的影像會以`-1`重新命名。 例如，`chair.tif`已重新命名為`chair-1.tif`。 這些選項會影響上傳至與原始檔案夾不同的影像，或是副檔名與原始檔案夾不同的影像，例如JPG、TIF或PNG。

  >[!NOTE]
  >
  >若要維持與Experience Manager的一致性，請選取[覆寫影像]選項&#x200B;**[!UICONTROL 在目前檔案夾中以相同的基本名稱/副檔名]**&#x200B;覆寫。

  | 覆寫影像選項 | 說明 |
  | --- | --- |
  | **[!UICONTROL 在目前資料夾中有相同的基本名稱/副檔名時覆寫]** | *僅針對新Dynamic Media帳戶預設*。<br>此選項是最嚴格的取代規則。 您需要將取代影像上傳到與原始影像相同的資料夾，而且取代影像的副檔名必須與原始影像相同。 如果不符合這些要求，則會建立副本。<br>*若要與Experience Manager保持一致，請選取此選項*。 |
  | **[!UICONTROL 在目前檔案夾中覆寫相同的基本名稱，無論副檔名是否相同]** | 需要您將取代影像上傳到與原始影像相同的資料夾，但副檔名可能與原始影像不同。 例如，chair.tif會取代chair.jpg。 |
  | **[!UICONTROL 在任何資料夾中以相同的基本資產名稱/副檔名覆寫]** | 取代影像的副檔名必須與原始影像相同（例如，chair.jpg必須取代chair.jpg，而非chair.tif）。 不過，您可以將取代影像上傳到與原始影像不同的資料夾。 更新後的影像位於新資料夾中；檔案無法再在其原始位置找到。 |
  | **[!UICONTROL 在任何資料夾中覆寫相同的基本資產名稱（無論副檔名為何）]** | 此選項是最具包容性的取代規則。 您可以將取代影像上傳到與原始檔案不同的資料夾、上傳副檔名不同的檔案，以及取代原始檔案。 如果原始檔案位於不同的資料夾中，則取代影像會位於其上載至的新資料夾中。 |

* **[!UICONTROL 保留裁切]**

  控制任何現有手動裁切定義的保留。

  另請參閱Dynamic Media檢視器參考指南中的[UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html?lang=zh-Hant)和[ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html?lang=zh-Hant)中的`preserveCrop`。

## 預設上傳選項 {#default-upload-options}

### 影像編輯索引標籤 {#image-editing-tab}

此濾鏡可讓您微調最終縮減取樣影像的銳利化濾鏡效果。 它可協助您控制效果的強度、效果的半徑（以畫素測量），以及被忽略的對比度臨界值。

「遮色片銳利化調整」效果使用與Photoshop的「遮色片銳利化調整」濾鏡相同的選項。 與名稱所建議的相反，「不銳利化遮色片」是一種銳利化濾鏡。

| 「不銳利化遮色片」選項 | 說明 |
| --- | --- |
| **[!UICONTROL 金額]** | 必填。<br>控制套用至邊緣畫素的對比量。<br>將其視為效果的強度。 Adobe Dynamic Media中「遮色片銳利化」的量值與Adobe Photoshop中的量值的主要差異在於，Photoshop的量範圍是1%到500%。 而在Adobe Dynamic Media中，值範圍為`0.0`到`5.0`。 Adobe Dynamic Media中的5.0值約略等同於Photoshop中的500%；0.9值等同於90%，以此類推。 |
| **[!UICONTROL 半徑]** | 必填。<br>控制效果的半徑。<br>值範圍為`0`到`250`。 此效果會在影像中的所有畫素上執行，並從所有方向的所有畫素向外輻射。 半徑是以畫素來測量。 例如，若要針對2000 x 2000畫素影像和500 x 500畫素影像取得類似的銳利化效果，您可以在2000 x 2000畫素影像上設定兩個畫素的半徑。 然後在500 x 500畫素影像上設定一個畫素的半徑值。 較大的值適用於畫素較多的影像。 |
| **[!UICONTROL 閾值]** | 必填。<br>臨界值是套用「遮色片銳利化調整」濾鏡時忽略的對比範圍。 此效果很重要，因此使用此濾鏡時，影像不會引入「雜訊」。 值範圍是`0` - `255`，這是灰階影像中的亮度階數。 `0`=黑色，`128`=50%灰色和`255`=白色。<br>閾值為`12`時，會忽略膚色亮度的細微變化，以避免增加雜訊，但還是會增加邊緣對比度，讓相異區域如睫毛與皮膚相遇的區域。<br>如果您有某個人的臉部像片，「遮色片銳利化調整」會影響影像的反差部分。 例如，睫毛和皮膚會合，以建立明顯的對比區域，以及平滑的皮膚本身。 即使最平滑的皮膚也會顯示亮度值的細微變化。 如果您不使用臨界值，濾鏡會強調外觀畫素中的這些細微變化。 反過來，會建立雜訊和不想要的效果，同時增加睫毛的對比，增強銳利度。<br>為了避免此問題，系統引入臨界值，告訴濾鏡忽略不會大幅改變對比度的畫素，例如平滑外觀。<br>在先前顯示的拉鍊圖形中，請注意拉鍊旁的紋理。 因為臨界值太低，無法抑制雜訊，所以會顯示影像雜訊。 |
| **[!UICONTROL 單色]** | 選取「 」以取消遮色片影像亮度（強度）的銳利化。<br>取消選取以分別取消銳利化遮色片每個色彩元件。 |

另請參閱[在Adobe Dynamic Media和影像伺服器](/help/assets/assets/sharpening_images.pdf)上銳利化影像。

### PostScript索引標籤 {#postscript-tab}

您可以點陣化Adobe PostScript®檔案、維持透明背景、選擇解析度，以及選擇色域。

您可以在Adobe Dynamic Media中使用Adobe PostScript® (EPS)檔案。 AdobeDynamic Media提供可在您上傳這些檔案時加以設定的命令。

上傳PostScript (EPS)影像檔案時，您可以透過各種方式格式化檔案。 您可以點陣化檔案、維持透明背景、選擇解析度，以及選擇色域。

| PostScript選項 | 說明 |
| --- | --- |
| **[!UICONTROL 正在處理]** | 選擇「點陣化」，將檔案中的向量圖形轉換為點陣圖格式。 |
| **[!UICONTROL 在演算後的影像中保留透明背景]** | 保留檔案的背景透明度。 |
| **[!UICONTROL 解析度（畫素/英吋）]** | 決定解析度設定。 此設定決定檔案中每英吋顯示的畫素數目。 |
| **[!UICONTROL 色域]** | · **[!UICONTROL 自動偵測]** — 保留檔案的色域。<br>· **[!UICONTROL 強製為RGB]** — 轉換為RGB色域。<br>· **[!UICONTROL 強製為CMYK]** — 轉換為CMYK色域。<br>· **[!UICONTROL 強製為灰階]** — 轉換為灰階色域。 |

### Photoshop索引標籤 {#photoshop-tab}

您可以從Adobe® Photoshop®檔案建立範本、維護圖層、指定圖層的命名方式、擷取文字，以及指定影像錨定到範本中的方式。

| Photoshop選項 | 說明 |
| --- | --- |
| **[!UICONTROL 保留圖層]** | 將PSD中的圖層（如果有的話）擷取至個別資產。 資產圖層會維持與PSD相關聯。 您可以在「詳細資料檢視」中開啟PSD檔案，並選取圖層面板來檢視它們。 請參閱在PSD檔案中檢視和編輯圖層。 |
| **[!UICONTROL 建立範本]** | 從PSD檔案中的圖層建立範本。 |
| **[!UICONTROL 擷取文字]** | 擷取文字，讓使用者能在檢視器中搜尋文字。 |
| **[!UICONTROL 將圖層延伸至背景大小]** | 將擷取的影像圖層大小延伸至背景圖層大小。 |
| **[!UICONTROL 圖層命名]** | 將擷取的影像圖層大小延伸至背景圖層大小。<br>· **[!UICONTROL 圖層名稱]** — 將影像命名為PSD檔案中的圖層名稱。 例如，原始PSD檔案中名為「價格標籤」的圖層會變成名為「價格標籤」的影像。 不過，如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱（「背景」、「圖層1」、「圖層2」等等），則會以影像在PSD檔案中的圖層編號來命名影像。 <br>· **[!UICONTROL Photoshop和圖層編號]** — 將影像命名為PSD檔案中的圖層編號，略過原始圖層名稱。 影像的命名方式為Photoshop檔案名稱及附加的圖層編號。 例如，名為`Spring Ad.psd`之檔案的第二個層名為`Spring Ad_2`，即使它在Photoshop中有非預設名稱。<br>· **[!UICONTROL Photoshop和圖層名稱]** — 在PSD檔案後面加上圖層名稱或圖層編號來命名影像。 如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱，則會使用圖層編號。 例如，名為`SpringAd`的PSD檔案中名為`Price Tag`的圖層名為`Spring Ad_Price Tag`。 預設名稱為「圖層2」的圖層稱為`Spring Ad_2`。 |
| **[!UICONTROL 錨點]** | 指定如何在範本中錨定影像，範本是從PSD檔案產生的圖層構成產生的。 依預設，錨點是中心。 無論取代影像的外觀比例為何，置中錨點都可讓取代影像以最佳方式填滿相同的空間。 以不同外觀取代此影像的影像，在參照範本並使用引數替代時，實際上會佔據相同的空間。 如果您的應用程式需要替代影像來填滿範本中配置的空間，請變更為其他設定。 |

### PDF標籤 {#pdf-tab}

您可以選擇點陣化檔案、擷取搜尋字詞和連結、設定解析度，以及選擇色域。

| PDF選項 | 說明 |
| --- | --- |
| **[!UICONTROL 正在處理]** | · **[!UICONTROL 無]** — 未完成任何PDF處理。<br>· **[!UICONTROL 縮圖]** — 擷取PDF檔案中的每個頁面，並將其轉換為縮圖影像。<br> · **[!UICONTROL 點陣化]** — 擷取PDF檔案中的頁面，並將向量影象轉換為點陣圖影像。 若要建立eCatalog，請選擇此選項。 |
| **[!UICONTROL 擷取]** | · **[!UICONTROL 無]** — 未從PDF中擷取任何搜尋字詞或連結。<br>· **[!UICONTROL 搜尋字詞]** — 從PDF檔案中擷取搜尋字詞，以便在eCatalog檢視器中依關鍵字搜尋檔案。<br>· **[!UICONTROL 連結]** — 從PDF檔案中擷取連結，並將其轉換成eCatalog檢視器中使用的影像地圖。<br>· **[!UICONTROL 搜尋字詞和連結]** — 擷取搜尋字詞和連結，以用於eCatalog檢視器。 |
| **[!UICONTROL 解析度（畫素/英吋）]** | 決定解析度設定。 此設定決定PDF檔案中每英吋顯示的畫素數目。 預設值為150。 |
| **[!UICONTROL 色域]** | · **[!UICONTROL 自動偵測]** — 保留PDF檔案的色域。<br>· **[!UICONTROL 強製為RGB]** — 轉換為RGB色域。<br>· **[!UICONTROL 強製為CMYK]** — 轉換為CMYK色域。<br>· **[!UICONTROL 強製為灰階]** — 轉換為灰階色域。 |

### Illustrator索引標籤 {#illustrator-tab}

您可以點陣化Adobe Illustrator®檔案、維持透明背景、選擇解析度，以及選擇色域。

您可以在Adobe Dynamic Media中使用® Illustrator® (AI)Adobe。 AdobeDynamic Media提供可在您上傳這些檔案時加以設定的命令。

上傳Illustrator (AI)影像檔案時，您可以透過各種方式格式化檔案。 您可以點陣化檔案、維持透明背景、選擇解析度，以及選擇色域。 在「上傳工作選項」方塊的「PostScript選項」和「Illustrator選項」下，上傳畫面上有可用於格式化PostScript和Illustrator檔案的選項。


| Illustrator選項 | 說明 |
| --- | --- |
| **[!UICONTROL 正在處理]** | 選擇「點陣化」，將檔案中的向量圖形轉換為點陣圖格式。 |
| **[!UICONTROL 在演算後的影像中保留透明背景]** | 保留檔案的背景透明度。 |
| **[!UICONTROL 解析度（畫素/英吋）]** | 決定解析度設定。 此設定決定檔案中每英吋顯示的畫素數目。 |
| **[!UICONTROL 色域]** | · **[!UICONTROL 自動偵測]** — 保留檔案的色域。<br>· **[!UICONTROL 強製為RGB]** — 轉換為RGB色域。<br>· **[!UICONTROL 強製為CMYK]** — 轉換為CMYK色域。<br>· **[!UICONTROL 強製為灰階]** — 轉換為灰階色域。 |
