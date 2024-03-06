---
title: 瞭解中繼資料概念
description: 瞭解中繼資料的需求和型別，讓資產更輕鬆分類及組織。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: abd3fbb5abb339d5b019fd2d7cf325404fb079e8
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 7%

---

# 瞭解中繼資料概念 {#why-we-need-metadata}

中繼資料是指資料的相關資料。 就此而言，資料是指您的數位資產，例如影像。 中繼資料是進行高效率資產管理的關鍵所在。

中繼資料是資產所有可用資料的集合，但不一定包含在該影像中。 中繼資料的一些範例包括：

* 資產名稱。
* 上次修改的時間和日期。
* 資產儲存在存放庫中的大小。
* 包含在其中的資料夾名稱。
* 相關資產或套用的標籤。

以上是基本的中繼資料屬性， [!DNL Experience Manager] 可管理資產，讓使用者檢視所有資產。 例如，嘗試探索最近新增的資產時，依上次修改日期排序資產會很有用。

例如，您可以將高階資料新增至數位資產：

* 資產型別（影像、視訊、音訊剪輯或檔案）。
* 資產擁有者。
* 資產標題。
* 資產的說明。
* 指派給資產的標籤。

更多中繼資料可協助您進一步將資產分類，且隨著數位資訊量成長，將有所幫助。 您可以僅根據檔案名稱管理數百個檔案。 然而，此方法並不能調整規模。隨著相關人數和管理的資產數量增加，此方法尚嫌不足。

隨著中繼資料增加，數位資產的價值也會成長，這是因為資產會變得

* 更易於存取 - 系統和使用者可以更輕鬆找到資產。
* 更易於管理 - 您可以更容易找到具有同一組屬性的資產，並將變更套用到這些資產。
* 完整 - 資產攜帶更多資訊和包含更多中繼資料的內容。

基於這些原因， [!DNL Assets] 提供建立、管理和交換數位資產中繼資料的合適方式。

## 中繼資料的型別 {#types-of-metadata}

兩種基本的中繼資料型別是技術中繼資料和描述性中繼資料。

技術中繼資料適用於處理數位資產的軟體應用程式，且不應手動維護。 [!DNL Experience Manager Assets] 和其他軟體會自動決定技術中繼資料，而中繼資料可能會在資產修改時變更。 資產可用的技術中繼資料主要取決於資產的檔案型別。 技術中繼資料的一些範例包括：

* 檔案的大小。
* 影像的Dimension（高度和寬度）。
* 音訊或視訊檔案的位元速率。
* 影像的解析度（詳細程度）。

描述性中繼資料是與應用程式網域相關的中繼資料，例如資產來自的業務。 描述性中繼資料無法自動判斷。 它是手動或半自動建立的。 例如，啟用GPS的相機可以自動追蹤經緯度，並在影像中新增地理標籤。

手動建立描述性中繼資料資訊的成本很高。 因此，我們建立了各種標準，以便於在軟體系統和組織之間交換中繼資料。 [!DNL Experience Manager Assets] 支援中繼資料管理的所有相關標準。

## 編碼標準 {#encoding-standards}

有多種方式可將中繼資料內嵌在檔案中。 支援一系列編碼標準：

* XMP：使用者 [!DNL Assets] 將擷取的中繼資料儲存在存放庫中。
* ID3：適用於音訊和視訊檔案。
* Exif：適用於影像檔案。
* 其他/舊版：從 [!DNL Microsoft Word]， [!DNL PowerPoint]， [!DNL Excel]、等等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是一種開放標準，用於 [!DNL Experience Manager Assets] 用於所有中繼資料管理。 此標準提供通用中繼資料編碼，可嵌入至所有檔案格式。 Adobe和其他公司支援XMP標準，因為它提供豐富的內容模型。 XMP標準的使用者和 [!DNL Experience Manager Assets] 擁有強大的平台作為建置基礎。 如需詳細資訊，請參閱 [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

當您在電腦或可攜式MP3播放器上播放數位音訊檔案時，會顯示儲存在這些ID3標籤中的資料。

ID3標籤是專為MP3檔案格式所設計。 格式的其他資訊：

* ID3標籤可用於MP3和mp3PRO檔案。
* WAV沒有標籤。
* WMA擁有不允許開放原始碼實作的專屬標籤。
* Ogg Vorbis使用內嵌於Ogg容器中的Xiph註解。
* AAC使用專屬標籤格式。

### Exif {#exif}

可交換影像檔案格式(Exif)是數位攝影中最常用的中繼資料格式。 它提供一種以多種檔案格式(例如JPEG、TIFF、RIFF和WAV)內嵌中繼資料屬性的固定辭彙的方法。 Exif會將中繼資料儲存為中繼資料名稱和中繼資料值的配對。 這些中繼資料名稱 — 值組也稱為標籤，切勿與中的標籤混淆 [!DNL Experience Manager]. 現代數位相機可建立Exif中繼資料，而現代圖形軟體則支援這些中繼資料。 Exif格式是中繼資料管理（尤其是影像）的最低通用分母。

Exif的一個主要限制是一些常見的影像檔案格式(例如BMP、GIF或PNG)不支援它。

Exif定義的中繼資料欄位通常屬於技術性質，在描述性中繼資料管理中的用途有限。 基於這個原因， [!DNL Experience Manager Assets] 提供Exif屬性對映至 [常見中繼資料結構](metadata-schemas.md) 和 [XMP](xmp-writeback.md).

### 其他中繼資料 {#other-metadata}

其他可從檔案嵌入的中繼資料包括 [!DNL Microsoft Word]， [!DNL PowerPoint]， [!DNL Excel]、等等。

## 瞭解中繼資料結構 {#metadata-schemata}

中繼資料結構是一組預先定義的中繼資料屬性定義，可用於各種應用程式。 屬性一律與資產相關聯，這表示屬性與資源「相關」。

如果沒有符合您需求的中繼資料結構，您也可以自行設計中繼資料結構。 不要複製現有的資訊。 在組織內，分隔結構描述可讓您更輕鬆地共用中繼資料。 [!DNL Experience Manager] 為您提供最受歡迎中繼資料結構的預設清單。 清單可協助您快速啟動中繼資料策略，並快速挑選所需的中繼資料屬性。

支援的中繼資料結構描述如下所列。

### 標準中繼資料 {#standard-metadata}

* DC - [!DNL Dublin Core] 是一組重要且廣泛使用的中繼資料。
* DICOM — 醫學的數位影像與通訊。
* `Iptc4xmpCore` 和 `iptc4xmpExt`  — 國際新聞通訊標準包含許多特定主題的中繼資料。
* RDF — 資源說明架構 — 用於一般語意Web中繼資料。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ`  — 基本工作票證。

### 應用程式專屬中繼資料 {#application-specific-metadata}

應用程式專屬中繼資料包括技術和描述性中繼資料。 如果您使用這類中繼資料，其他應用程式可能無法使用中繼資料。 例如，不同的影像演算應用程式可能無法存取 [!DNL Adobe Photoshop] 中繼資料。 您可以建立工作流程步驟，將應用程式特定屬性變更為標準屬性。

* ACDSee — 由管理的中繼資料 [!DNL ACDSee] 程式。 另請參閱 [www.acdsee.com/](https://www.acdsee.com/).
* 相簿 —  [!DNL Adobe Photoshop Album].
* CQ — 使用者 [!DNL Experience Manager Assets].
* DAM — 使用者 [!DNL Experience Manager Assets].
* DEX - [!DNL Optima SC Description explorer] 是Windows作業系統中繼資料和檔案管理的工具集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto和MP - Microsoft像片。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop].

### Digital Rights Management(DRM)中繼資料 {#digital-rights-management-metadata}

* 副本 —  [!DNL Creative Commons].
* [!DNL XMPRights]。
* 加 —  [圖片授權通用系統](https://www.useplus.com).
* 稜鏡 —  [發佈產業標準中繼資料的需求](https://www.w3.org/submissions/2020/SUBM-prism-20200910/Image_Guide.pdf).
* PRL — 稜鏡許可權語言。
* PUR - PRISM使用許可權。
* `xmpPlus` - PLUS與XMP整合。

### 攝影專用中繼資料 {#photography-specific-metadata}

* Exif — 攝影機的技術資訊，包括GPS位置。
* CRS - [!DNL Camera Raw] 綱要。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF — 影像中繼資料(不僅適用於TIFF影像)。

### 列印特定中繼資料 {#print-specific-metadata}

* PDF與PDF/X - Adobe PDF和協力廠商應用程式。
* 稜鏡 —  [發佈產業標準中繼資料的需求](https://www.w3.org/submissions/2020/SUBM-prism-20200910/Image_Guide.pdf).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG`  — 分頁文字的XMP中繼資料。

### 多媒體專屬中繼資料 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — 媒體管理。

## 中繼資料結構描述參考 {#metadata-schemata-reference}

下列參考資料包含特定中繼資料結構描述（按字母順序）的相關資訊，以及屬性及其定義的清單。

### 都柏林核心 {#dublin-core}

Dublin核心中繼資料提供一組標準化的慣例，用於說明資產，以便輕鬆找到。 在 [!DNL Assets]都柏林核心說明數位資產，包括視訊、音效、影像和檔案。

簡單Dublin核心中繼資料元素集(DCMES)包含15個中繼資料元素，如下表所示。 每個Dublin Core元素都是選用的，可以重複。 您可以新增或刪除Dublin核心中繼資料資訊，就像新增或刪除媒體型別專屬中繼資料一樣。

除了DCMES，還有由Dublin核心方案建立的其他中繼資料元素。 請參閱 [都柏林核心計畫](https://dublincore.org/) 以取得詳細資訊。

| 屬性 | 說明 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| 投稿人 | 負責貢獻內容的人或公司。 |
| 涵蓋範圍 | 資產涵蓋的地理位置或時段。 |
| 建立者 | 負責建立內容的人或公司。 |
| 日期 | 與資產相關聯的日期或時間期間。 |
| 說明 | 有關資產的詳細資訊。 |
| 格式 | 資產的檔案格式、實體媒體或維度。 [!DNL Experience Manager] 使用 `dc:format` 表示資產的MIME型別。 |
| 識別碼 | 資產的唯一參考。 |
| 語言 | 資產的語言(例如 `en` （適用於英文）。 |
| 發佈者 | 負責提供資產的使用者或公司。 |
| 關係 | 相關資產。 |
| 權利 | 關於誰擁有此資產之許可權的資訊。 |
| 來源 | 衍生資產的相關資產。 |
| 主體 | 資產的主題。 |
| 標題 | 資產的名稱。 |
| 類型 | 資產的性質或型別。 |

### IPTC {#iptc}

國際新聞通訊協會(IPTC)是由全球各地的新聞機構組成的聯盟，其目標之一是開發並維護技術標準。 IPTC定義了一組影像的像片中繼資料標準，這些標準幾乎為攝影師所普遍接受。 這些中繼資料標準是1990年代建立的IPTC Information Interchange Model (IIM)標準的一部分。

雖然IPTC標頭資訊已大部分被XMP取代，但XMP可以使用IPTC核心結構描述和擴充功能結構描述。 在影像程式中，XMP和IPTC屬性都會同步。

## 中繼資料導向的工作流程 {#metadata-driven-workflows}

建立中繼資料導向工作流程可協助您自動化部分流程，進而提高效率。 在中繼資料驅動的工作流程中，工作流程管理系統會讀取工作流程，並因此執行一些預先定義的動作。 例如，部分使用中繼資料導向工作流程的方式：

* 工作流程可檢查影像是否具有標題。 如果不適用，系統會通知以新增標題。
* 工作流程可檢查資產上的版權宣告是否允許發佈。 因此，系統會將資產傳送至一台或多台伺服器。
* 工作流程可以檢查沒有預先定義、強制中繼資料的資產，或具有 *無效* 中繼資料。

## XMP 中繼資料 {#xmp-metadata}

XMP （可延伸中繼資料平台）是使用的中繼資料標準 [!DNL Adobe Experience Manager Assets] 用於所有中繼資料管理。 XMP為各種應用程式的中繼資料的建立、處理和交換提供標準格式。

除了提供可嵌入到所有檔案格式的通用中繼資料編碼之外，XMP還提供豐富的 [內容模型](#xmp-core-concepts) 和 [受Adobe支援](#advantages-of-xmp) 和其他公司，以便XMP的使用者能夠與 [!DNL Assets] 擁有強大的平台作為建置基礎。

此 [XMP規格](https://www.adobe.com/devnet/xmp.html) 可透過Adobe使用。

### 什麼是XMP？ {#what-is-xmp}

Adobe首先推出XMP標準作為Adobe Acrobat軟體產品的一部分。 從那時起，XMP標準就被廣泛採用。 [!DNL Assets] 原生支援XMP — 以Adobe為首的可延伸中繼資料平台。 XMP是在數位資產中處理和儲存標準化和專屬中繼資料的標準。 XMP是共同標準，可讓多個應用程式有效處理中繼資料。

例如，生產專業人員可使用Adobe應用程式內建的XMP支援，以跨多種檔案格式傳遞資訊。 [!DNL Assets] 存放庫會擷取XMP中繼資料，並使用它來管理內容生命週期，並提供建立自動化工作流程的功能。

XMP透過提供資料模型、儲存模型和結構描述，將中繼資料的定義、建立和處理標準化。 本章節將介紹所有這些概念。

來自EXIF、ID3或Microsoft Office的所有舊版中繼資料會自動轉譯為XMP，可延伸以支援客戶特定的中繼資料結構，例如產品目錄。

XMP中的中繼資料包含一組屬性。 這些屬性一律與稱為資源的特定實體相關聯；也就是說，屬性是「關於」資源的。 如果有XMP，則資源一律為資產。

### XMP生態系統 {#xmp-ecosystem}

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### XMP的優點 {#advantages-of-xmp}

XMP具有下列優於其他編碼標準和結構描述：

* XMP中繼資料功能非常強大，而且相當精細化。
* XMP可讓您一個屬性有多個值。
* XMP已標準化編碼，讓您輕鬆交換中繼資料。
* XMP是可擴充的。 您可以將其他資訊新增至資產。

XMP標準設計為可擴充，可讓您將自訂型別的中繼資料新增到XMP資料中。 另一方面，EXIF則不會 — 它具有無法擴充的固定屬性清單。

>[!NOTE]
>
>XMP通常不允許內嵌二進位資料型別。 若要在XMP中攜帶二進位資料（例如縮圖影像），這些資料必須以XML易記格式編碼，例如 `Base64`.

### XMP概念 {#xmp-core-concepts}

以下章節說明XMP的核心概念，包括名稱空間和結構描述、屬性和值，以及語言替代方案。

#### 名稱空間和結構描述 {#namespaces-and-schemata}

XMP結構描述是通用XML名稱空間中的一組屬性名稱，包括資料型別和描述性資訊。 XMP結構描述是由其XML名稱空間URI識別。 使用名稱空間可防止不同結構描述中名稱相同但含義不同的屬性之間發生衝突。

例如， `Creator` 兩個獨立設計結構描述中的屬性可能代表建立資產的人，也可能代表建立資產的應用程式(例如Adobe Photoshop)。

#### 屬性和值 {#properties-and-values}

XMP可能包含一或多個結構描述的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括以下內容：

* 都柏林核心結構描述： `dc:title`， `dc:creator`， `dc:subject`， `dc:format`， `dc:rights`.
* XMP基本結構描述： `xmp:CreateDate`， `xmp:CreatorTool`， `xmp:ModifyDate`， `xmp:metadataDate`.
* XMP許可權管理綱要： `xmpRights:WebStatement`， `xmpRights:Marked`.
* XMP媒體管理結構： `xmpMM:DocumentID`.

#### 替代語言 {#language-alternatives}

XMP可讓您新增 `xml:lang` 屬性以指定文字的語言。

## 使用IPTC中繼資料 {#support-for-iptc-metadata}

瞭解如何 [!DNL Adobe Experience Manager Assets] 透過支援新增至資產的IPTC中繼資料、創意評分和關鍵字 [!DNL Adobe Bridge] 和其他 [!DNL Adobe Creative Cloud] 應用程式。

[!DNL Adobe Experience Manager Assets] 支援廣泛用來描述資產的IPTC中繼資料標準。 這邊， [!DNL Assets] 提升影像在各方面（包括攝影師、創意公司、圖書館、博物館等）的接受度。

資產的預設中繼資料結構現在納入IPTC核心和IPTC擴充功能中繼資料結構，以定義完整的中繼資料屬性，讓使用者新增有關影像中所顯示的人員、位置和產品的精確且可靠的資料。 它也支援有關建立影像的日期、名稱和識別碼，以及表達權利資訊的靈活方式。

資產的「屬性」頁面現在包含個別標籤，以便在可編輯的欄位中顯示IPTC核心和IPTC擴充功能中繼資料。

1. 從 [!DNL Assets] 使用者介面，選取影像。
1. 按一下 **[!UICONTROL 屬性]** 工具列中的。
1. 按一下 **[!UICONTROL IPTC]** 標籤以檢視資產的IPTC中繼資料。
1. 視需要編輯IPTC中繼資料屬性。

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. 按一下 **[!UICONTROL IPTC延伸]** 標籤以檢視資產的IPTC擴充功能中繼資料。
1. 視需要編輯IPTC擴充功能中繼資料屬性。
1. 按一下 **[!UICONTROL 儲存並關閉]** 以儲存變更。

### 創意評等支援 {#creative-rating-support}

除了顯示個別使用者評分和彙總評分之外，「屬性」頁面現在還會顯示透過Adobe Bridge和其他創意應用程式指派給資產的評分

這些評等可在「進階」標 **[!UICONTROL 簽的「創作評分]** 」區段 **[!UICONTROL 下取得]** 。

此評等是唯讀屬性，範圍為1至5。 您可以從搜尋面板根據資產的創意評等來搜尋資產。

但是，此屬性目前未編列索引，以避免與使用者進行的自訂變更發生任何衝突。

### 關鍵字支援 {#keyword-support}

此 **[!UICONTROL IPTC]** 的標籤 [!UICONTROL 屬性] 頁面也會顯示透過Adobe Bridge和其他Adobe Creative Cloud應用程式新增至資產的關鍵字。 您也可以編輯這些關鍵字，並從 **[!UICONTROL IPTC]** 標籤。

![關鍵字](assets/keywords-in-iptc-tab.png)
