---
title: 瞭解中繼資料概念
description: 瞭解中繼資料的需求和類型，以便更輕鬆地分類和組織資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '2732'
ht-degree: 6%

---


# 瞭解中繼資料概念 {#why-we-need-metadata}

中繼資料是指有關資料的資料。 在這方面，資料是指您的數位資產，例如影像。 中繼資料對於有效率的資產管理至關重要。

中繼資料是資產所有可用資料的集合，但不一定包含在該影像中。 中繼資料的一些範例包括：

* 資產的名稱。
* 上次修改的時間和日期。
* 資產儲存在儲存庫中時的大小。
* 包含在中的資料夾的名稱。
* 相關資產或套用的標籤。

以上是可管理資產的基本中繼資 [!DNL Experience Manager] 料屬性，可讓使用者查看所有資產。 例如，在嘗試尋找最近新增的資產時，可使用上次修改日期來排序資產。

您可以新增更多高階資料至數位資產，例如：

* 資產類型（是影像、視訊、音訊剪輯或檔案？）。
* 資產的擁有者。
* 資產的標題。
* 資產的說明。
* 指派給資產的標籤。

更多中繼資料可協助您進一步分類資產，並隨著數位資訊的增加而有所幫助。 僅根據檔名管理幾百個檔案是可能的。 但是，這種方法不具可擴充性。 當涉案人數和管理的資產數量增加時，這個數字就不夠。

隨著中繼資料的增加，數位資產的價值會增加，因為資產會變成，

* 更容易存取——系統和使用者可輕鬆找到。
* 管理起來更輕鬆——您可以更輕鬆地尋找具有相同屬性集的資產，並套用變更。
* 完整——資產包含更多資訊和內容，以及更多中繼資料。

基於這些原因， [!DNL Assets] 您可以為數位資產提供建立、管理和交換中繼資料的適當方式。

## 中繼資料類型 {#types-of-metadata}

兩種基本的中繼資料類型是技術中繼資料和描述性中繼資料。

技術中繼資料對於處理數位資產且不應手動維護的軟體應用程式非常有用。 [!DNL Experience Manager Assets] 而其他軟體會自動決定技術中繼資料，而當資產修改時，中繼資料可能會變更。 資產的可用技術中繼資料主要取決於資產的檔案類型。 技術中繼資料的一些範例包括：

* 檔案大小。
* 影像的尺寸（高度和寬度）。
* 音訊或視訊檔案的位元速率。
* 影像的解析度（詳細程度）。

描述性中繼資料是與應用程式網域相關的中繼資料，例如資產來自的業務。 無法自動確定描述性中繼資料。 系統會手動或半自動建立。 例如，可使用GPS的相機可自動追蹤經緯度，並新增地理標籤影像。

手動建立描述性中繼資料資訊的成本很高。 因此，建立標準是為了簡化跨軟體系統和組織的中繼資料交換。 [!DNL Experience Manager Assets] 支援中繼資料管理的所有相關標準。

## 編碼標準 {#encoding-standards}

在檔案中內嵌中繼資料有多種方式。 支援多種編碼標準：

* XMP:用於將提 [!DNL Assets] 取的元資料儲存在儲存庫中。
* ID3:音訊和視訊檔案。
* 例如：的雙曲餘切值。
* 其他／舊版：從 [!DNL Microsoft Word]、 [!DNL PowerPoint][!DNL Excel]等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是開放標準，供所有中繼資料 [!DNL Experience Manager Assets] 管理使用。 此標準提供通用中繼資料編碼，可嵌入所有檔案格式。 Adobe和其他公司支援XMP標準，因為它提供多樣化內容模型。 使用XMP標準和XMP標準的 [!DNL Experience Manager Assets] 使用者擁有強大的平台。 如需詳細資訊，請參 [閱XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

當您在電腦或可攜式MP3播放器上播放數位音訊檔案時，會顯示儲存在這些ID3標籤中的資料。

ID3標籤是針對MP3檔案格式而設計。 有關格式的其他資訊：

* ID3標籤適用於MP3和mp3PRO檔案。
* WAV沒有標籤。
* WMA有不允許開放原始碼實作的專屬標籤。
* Ogg Vorbis使用內嵌在Ogg容器中的Xiph Comments。
* AAC使用專屬的標籤格式。

### Exif {#exif}

可交換的影像檔案格式(Exif)是數位攝影中最常用的中繼資料格式。 它提供以多種檔案格式（例如JPEG、TIFF、RIFF和WAV）嵌入固定的中繼資料屬性辭彙的方式。 Exif將中繼資料儲存為中繼資料名稱與中繼資料值的配對。 這些中繼資料名稱——值配對也稱為標籤，不要與中的標籤混淆 [!DNL Experience Manager]。 現代數位相機可建立Exif中繼資料，而現代圖形軟體也支援它。 Exif格式是中繼資料管理的最低公分母，尤其是影像。

Exif的主要限制是不支援一些常用的影像檔案格式，例如BMP、GIF或PNG。

Exif定義的中繼資料欄位通常具有技術性，在描述性中繼資料管理中使用有限。 因此，提供 [!DNL Experience Manager Assets] Exif屬性對應至常用中 [繼資料架構](metadata-schemas.md) ，以及 [XMP](xmp-writeback.md)。

### 其他中繼資料 {#other-metadata}

可從檔案內嵌的其他中繼資 [!DNL Microsoft Word]料 [!DNL PowerPoint]包括 [!DNL Excel]、、等等。

## 瞭解中繼資料圖式 {#metadata-schemata}

中繼資料結構是一組預先定義的中繼資料屬性定義，可用於各種應用程式。 屬性始終與資產相關聯，這表示屬性與資源「相關」。

如果沒有符合您需求的中繼資料架構，您也可以設計您自己的中繼資料架構。 請勿複製現有資訊。 在組織內，分離圖式資料可讓共用中繼資料更輕鬆。 [!DNL Experience Manager] 提供您最常用中繼資料架構的預設清單。 此清單可協助您快速開始中繼資料策略，並快速挑選您需要的中繼資料屬性。

支援的中繼資料架構列於下方。

### 標準中繼資料 {#standard-metadata}

* DC —— 是 [!DNL Dublin Core] 一組重要且廣泛使用的元資料。
* DICOM —— 數位影像與醫學通訊。
* `Iptc4xmpCore` 和 `iptc4xmpExt` - International Press Communications Standard包含許多特定主題的中繼資料。
* RDF —— 資源描述框架——通用語義Web元資料。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` -基本工作訂票。

### 應用程式專用的中繼資料 {#application-specific-metadata}

應用程式專用的中繼資料包含技術和描述性中繼資料。 如果您使用此類中繼資料，其他應用程式可能無法使用中繼資料。 例如，不同的影像轉換應用程式可能無法存取中繼 [!DNL Adobe Photoshop] 資料。 您可以建立工作流程步驟，將應用程式特定屬性變更為標準屬性。

* ACDSee —— 由程式管理的元 [!DNL ACDSee] 資料。 請參 [閱www.acdsee.com/](https://www.acdsee.com/)。
* 相簿- [!DNL Adobe Photoshop Album].
* CQ —— 使用者 [!DNL Experience Manager Assets]。
* DAM —— 用於 [!DNL Experience Manager Assets]。
* DEX - [Optima SC描述檔案總管](http://www.optimasc.com/products/dex/index.html) ，是Windows作業系統中中繼資料和檔案管理工具的集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto和MP - Microsoft Photo。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop].

### 數位版權管理(DRM)中繼資料 {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* PLUS —— 圖 [片授權通用系統](https://www.useplus.com)。
* PRISM —— 發佈 [業界標準中繼資料的需求](https://www.idealliance.org/prism-metadata)。
* PRL —— 稜鏡版權語言。
* PUR —— 稜鏡使用權。
* `xmpPlus` -將PLUS與XMP整合。

### 攝影專用中繼資料 {#photography-specific-metadata}

* Exif —— 相機的技術資訊，包括GPS位置。
* CRS —— 方 [!DNL Camera Raw] 案。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF —— 影像中繼資料（不僅適用於TIFF影像）。

### 列印專用的中繼資料 {#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和協力廠商應用程式。
* PRISM —— 發佈 [業界標準中繼資料的需求](https://www.idealliance.org/prism-metadata)。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` -分頁文字的XMP中繼資料。

### 多媒體特定中繼資料 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` -媒體管理。

## 中繼資料圖式參考 {#metadata-schemata-reference}

以下參考包括關於特定元資料方案的資訊（按字母順序）以及屬性清單及其定義。

### Dublin Core {#dublin-core}

Dublin Core中繼資料提供一組標準化的慣例，用於描述資產，以便更容易找到。 在 [!DNL Assets]中，Dublin Core說明數位資產，包括視訊、音效、影像和檔案。

簡單的Dublin Core Metadata Element Set(DCMES)包含15個中繼資料元素，如下表所列。 每個Dublin Core元素都是選用的，可重複。 您可以像新增或刪除媒體類型特定中繼資料一樣，新增或刪除Dublin Core中繼資料資訊。

除了DCMES之外，還有Dublin Core Initiative（都柏林核心計畫）建立的其他元資料元素。 如需詳細 [資訊，請參閱Dublin Core](https://dublincore.org/) initiative。

| 屬性 | 說明 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| contributor | 負責對內容作出貢獻的人士或公司。 |
| 覆蓋率 | 資產涵蓋的地理位置或時段。 |
| 製造者 | 負責建立內容的人員或公司。 |
| 日期 | 與資產相關的日期或期間。 |
| 說明 | 資產的詳細資訊。 |
| 格式 | 資產的檔案格式、實體媒體或尺寸。 [!DNL Experience Manager] 用 `dc:format` 來表示資產的MIME類型。 |
| 識別碼 | 資產的唯一參考。 |
| 語言 | 資產的語言（例如，英文為en）。 |
| publisher | 負責使資產可供使用的人員或公司。 |
| 關係 | 相關資產。 |
| 權利 | 關於誰有權使用此資產的資訊。 |
| source | 資產衍生自之相關資產。 |
| 主旨 | 資產的主題。 |
| 標題 | 資產的名稱。 |
| 類型 | 資產的性質或類別。 |

### IPTC {#iptc}

國際新聞通訊委員會(IPTC)是由全球新聞機構組成的聯合體，其目標之一是制定和維護技術標準。 IPTC為影像定義了一套像片中繼資料標準，在攝影師中幾乎被普遍接受。 這些元資料標準是20世紀90年代建立的更廣泛標準的一部分，即IPTC資訊交換模型(IIM)。

雖然IPTC標題資訊已大部份被XMP取代，但XMP可使用IPTC核心架構和擴充架構。 在影像程式中，XMP和IPTC屬性都會同步。

## 中繼資料導向的工作流程 {#metadata-driven-workflows}

建立中繼資料導向的工作流程可協助您自動化某些程式，進而提高效率。 在元資料驅動的工作流中，工作流管理系統讀取該工作流並因此執行一些預定義的操作。 例如，您可使用中繼資料導向工作流程的一些方式：

* 工作流程可以檢查影像是否有標題。 如果沒有，系統會通知您新增標題。
* 工作流程可以檢查資產上的版權聲明是否允許散發。 因此，系統會將資產傳送至一或另一伺服器。
* 工作流程可以檢查資產是否沒有預先定義的強制中繼資料，或是包含無效中繼資料 *的資* 產。

## XMP 中繼資料 {#xmp-metadata}

XMP（可擴充中繼資料平台）是所有中繼資料管理所 [!DNL Adobe Experience Manager Assets] 使用的中繼資料標準。 XMP提供標準格式，讓您針對多種應用程式建立、處理和交換中繼資料。

XMP除了提供可嵌入所有檔案格式的通用中繼資料編碼外，還提供多樣化的 [內容模型](#xmp-core-concepts) ，並受 [Adobe](#advantages-of-xmp)[!DNL Assets] 和其他公司的支援，讓XMP的使用者結合使用者擁有強大的平台來建立內容。

XMP規 [格](https://www.adobe.com/devnet/xmp.html) ，可從Adobe取得。

### 什麼是XMP? {#what-is-xmp}

Adobe率先將XMP標準納入Adobe Acrobat軟體產品。 自此，XMP標準得到廣泛採用。 [!DNL Assets] 原生支援XMP —— 由Adobe牽頭的可擴充中繼資料平台。 XMP是處理和儲存數位資產中標準化和專屬中繼資料的標準。 XMP是通用的標準，可讓多個應用程式有效地處理中繼資料。

例如，生產專業人員可使用Adobe應用程式內建的XMP支援，跨多種檔案格式傳遞資訊。 [!DNL Assets] 資料庫會擷取XMP中繼資料，並使用它來管理內容生命週期，並提供建立自動化工作流程的能力。

XMP透過提供資料模型、儲存模型和結構描述，標準化中繼資料的定義、建立和處理方式。 本節將介紹這些概念。

EXIF、ID3或Microsoft Office的所有舊式中繼資料都會自動轉譯為XMP,XMP可加以擴充，以支援客戶特定的中繼資料架構，例如產品型錄。

XMP中的中繼資料由一組屬性組成。 這些屬性始終與稱為資源的特定實體相關聯；即，屬性是關於資源的。 對於XMP，資源永遠是資產。

### XMP生態系統 {#xmp-ecosystem}

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### XMP的優點 {#advantages-of-xmp}

XMP比其他編碼標準和圖式具有以下優點：

* 以XMP為基礎的中繼資料功能強大，而且具備細緻的功能。
* XMP可讓您針對一個屬性擁有多個值。
* XMP具備標準化編碼，可讓您輕鬆交換中繼資料。
* XMP具有可擴充性。 您可以新增其他資訊至資產。

XMP標準可擴充，讓您在XMP資料中新增自訂的中繼資料類型。 而EXIF則否——它有固定的屬性清單，無法延伸。

>[!NOTE]
>
>XMP通常不允許嵌入二進位資料類型。 若要以XMP格式傳送二進位資料（例如縮圖影像），它們必須以XML友好格式編碼，例如 `Base64`。

### XMP概念 {#xmp-core-concepts}

以下各節介紹XMP的核心概念，包括名稱空間和圖式、屬性和值，以及語言替代。

#### 命名空間和圖式 {#namespaces-and-schemata}

XMP架構是一組通用XML命名空間中的屬性名稱，其中包含資料類型和描述性資訊。 XMP架構由其XML命名空間URI來識別。 使用名稱空間可防止名稱相同但含義不同之不同結構中屬性之間的衝突。

例如，兩個 `Creator` 獨立設計結構中的屬性可能代表建立資產的人員，也可能代表建立資產的應用程式（例如Adobe Photoshop）。

#### 屬性與值 {#properties-and-values}

XMP可以包括來自一個或多個方案的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括：

* 都柏林核心架構： `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP基本架構： `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`。
* XMP權限管理架構： `xmpRights:WebStatement`, `xmpRights:Marked`ý?
* XMP媒體管理架構： `xmpMM:DocumentID`.

#### 替代語言 {#language-alternatives}

XMP可讓您將屬 `xml:lang` 性新增至文字屬性，以指定文字的語言。

## 使用IPTC中繼資料 {#support-for-iptc-metadata}

瞭解如何 [!DNL Adobe Experience Manager Assets] 支援透過和其他應用程式新增至資產的IPTC中繼資料、創意評 [!DNL Adobe Bridge] 分和關 [!DNL Adobe Creative Cloud] 鍵字。

[!DNL Adobe Experience Manager Assets] 支援廣泛用於描述資產的IPTC中繼資料標準。 如此， [!DNL Assets] 就可提高攝影師、創意廣告公司、圖書館、博物館等各方對影像的接受度。

資產的預設中繼資料結構現在整合了IPTC核心和IPTC擴充功能中繼資料結構，以定義完整的中繼資料屬性，讓使用者新增有關影像中顯示之人物、位置和產品的精確可靠資料。 它也支援建立影像的日期、名稱和識別碼，並提供彈性的方式來表達權限資訊。

資產的「屬性」頁面現在包含個別的標籤，可在可編輯欄位中顯示「IPTC核心」和「IPTC擴充功能」中繼資料。

1. 從使用者 [!DNL Assets] 介面中，選取影像。
1. Click **[!UICONTROL Properties]** from the toolbar.
1. 按一下 **[!UICONTROL IPTC]** 標籤，以檢視資產的IPTC中繼資料。
1. 視需要編輯IPTC中繼資料屬性。

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Click the **[!UICONTROL IPTC Extension]** tab to view IPTC Extension metadata for the asset.
1. 視需要編輯IPTC Extension中繼資料屬性。
1. Click **[!UICONTROL Save &amp; Close]** to save the changes.

### 創意評分支援 {#creative-rating-support}

除了顯示個別使用者分級和匯總分級外，「屬性」頁面現在還會顯示透過Adobe Bridge和其他Creative Apps指派給資產的分級

這些評等可在「進階」標 **[!UICONTROL 簽的「創作評分]** 」區段 **[!UICONTROL 下取得]** 。

此分級是唯讀屬性，範圍介於1-5之間。 您可以從「搜尋面板」根據資產的「創意評分」來搜尋資產。

不過，此屬性目前未建立索引，以避免與使用者所做的自訂變更產生任何衝突。

### 關鍵字支援 {#keyword-support}

「屬 **[!UICONTROL 性」頁面的]** 「IPTC  」索引標籤也會顯示透過Adobe Bridge和其他Adobe Creative Cloud應用程式新增至資產的關鍵字。 您也可以編輯這些關鍵字，並從「 **[!UICONTROL IPTC」索引標籤新增更多關]** 鍵字。

![關鍵字](assets/keywords-in-iptc-tab.png)
