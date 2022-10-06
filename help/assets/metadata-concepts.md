---
title: 了解中繼資料概念
description: 了解中繼資料的需求和類型，以便更輕鬆地分類和組織資產。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2720'
ht-degree: 9%

---

# 了解中繼資料概念 {#why-we-need-metadata}

中繼資料是指資料的相關資料。 在這方面，資料是指您的數位資產，例如影像。 中繼資料是進行高效率資產管理的關鍵所在。

中繼資料是資產可用之所有資料的集合，但不一定包含在該影像中。 中繼資料的一些範例為：

* 資產名稱。
* 上次修改的時間和日期。
* 儲存在存放庫中的資產大小。
* 資料夾的名稱。
* 相關資產或套用的標籤。

以上是基本中繼資料屬性， [!DNL Experience Manager] 可管理資產，讓使用者可以查看所有資產。 例如，在嘗試探索最近新增的資產時，依上次修改日期排序資產很實用。

您可以新增更多高階資料至數位資產，例如：

* 資產的類型（影像、視訊、音訊剪輯或檔案）。
* 資產擁有者。
* 資產的標題。
* 資產說明。
* 指派給資產的標籤。

更多中繼資料可協助您進一步分類資產，並隨著數位資訊量增加而有所幫助。 僅根據檔案名稱即可管理數百個檔案。 然而，此方法並不能調整規模。當參與人數和管理的資產數量增加時，這個數字就不夠。

隨著中繼資料增加，數位資產的價值也會成長，這是因為資產會變得

* 更易於存取 - 系統和使用者可以更輕鬆找到資產。
* 更易於管理 - 您可以更容易找到具有同一組屬性的資產，並將變更套用到這些資產。
* 完整 - 資產攜帶更多資訊和包含更多中繼資料的內容。

基於這些原因， [!DNL Assets] 為您提供建立、管理和交換數位資產的中繼資料的適當方式。

## 中繼資料的類型 {#types-of-metadata}

兩種基本的中繼資料類型是技術中繼資料和描述性中繼資料。

技術中繼資料對於處理數位資產且不應手動維護的軟體應用程式非常有用。 [!DNL Experience Manager Assets] 而其他軟體則自動確定技術元資料，當資產被修改時，元資料可能會改變。 資產的可用技術中繼資料主要取決於資產的檔案類型。 技術中繼資料的一些範例為：

* 檔案大小。
* Dimension（高度和寬度）。
* 音訊或視訊檔案的位元速率。
* 影像的解析度（詳細程度）。

描述性中繼資料是與應用程式網域相關的中繼資料，例如資產來自的業務。 無法自動確定描述性中繼資料。 系統會手動或半自動建立。 例如，啟用GPS的相機可自動追蹤經緯度，並新增地理標籤影像。

手動建立描述性中繼資料資訊的成本很高。 因此，制定標準是為了方便跨軟體系統和組織交換元資料。 [!DNL Experience Manager Assets] 支援元資料管理的所有相關標準。

## 編碼標準 {#encoding-standards}

在檔案中內嵌中繼資料有多種方式。 支援一系列編碼標準：

* XMP:使用者 [!DNL Assets] 將擷取的中繼資料儲存在存放庫中。
* ID3:用於音頻和視頻檔案。
* 例如：（適用於影像檔案）。
* 其他/舊版：從 [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是開放標準，用於 [!DNL Experience Manager Assets] 用於所有中繼資料管理。 此標準提供通用中繼資料編碼，可嵌入到所有檔案格式中。 Adobe和其他公司支援XMP standard，因為它提供豐富的內容模型。 XMP standard和的使用者 [!DNL Experience Manager Assets] 有一個強大的平台可以建立。 如需詳細資訊，請參閱 [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

當您在電腦或筆記型電腦MP3播放器上播放數位音訊檔案時，儲存在這些ID3標籤中的資料會顯示。

ID3標籤是為MP3檔案格式而設計。 格式的其他資訊：

* ID3標籤適用於MP3和mp3PRO檔案。
* WAV沒有標籤。
* WMA具有不允許開放原始碼實作的專屬標籤。
* Ogg Vorbis使用嵌入在Ogg容器中的Xiph注釋。
* AAC使用專屬標籤格式。

### Exif {#exif}

可交換影像檔案格式(Exif)是數位攝影中最常用的中繼資料格式。 它提供了以多種檔案格式嵌入固定的元資料屬性辭匯的方法，如JPEG、TIFF、RIFF和WAV。 Exif將中繼資料儲存為中繼資料名稱和中繼資料值的配對。 這些中繼資料名稱值配對也稱為標籤，請勿與 [!DNL Experience Manager]. 現代數位相機可建立Exif元資料，現代圖形軟體可支援它。 Exif格式是中繼資料管理的最低公分母，尤其是影像。

Exif的一個主要限制是少數常見的影像檔案格式(例如BMP、GIF或PNG)不支援它。

Exif定義的中繼資料欄位通常屬於技術性質，在描述性中繼資料管理中的使用有限。 因此， [!DNL Experience Manager Assets] 選件將Exif屬性對應至 [公用元資料結構](metadata-schemas.md) 和 [XMP](xmp-writeback.md).

### 其他中繼資料 {#other-metadata}

可從檔案嵌入的其他元資料包括 [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]等。

## 了解中繼資料結構 {#metadata-schemata}

中繼資料結構是可用於各種應用程式的一組預先定義的中繼資料屬性定義。 屬性一律與資產相關聯，這表示屬性是資源的「關於」。

如果沒有符合您需求的中繼資料結構，您也可以設計您自己的中繼資料結構。 請勿複製現有資訊。 在組織內，區隔架構可讓您更輕鬆共用中繼資料。 [!DNL Experience Manager] 提供最受歡迎中繼資料結構的預設清單。 此清單可協助您快速啟動中繼資料策略，並快速挑選您需要的中繼資料屬性。

支援的中繼資料結構列於下方。

### 標準中繼資料 {#standard-metadata}

* DC - [!DNL Dublin Core] 是一組重要且廣泛使用的中繼資料。
* DICOM — 醫學中的數字影像和通信。
* `Iptc4xmpCore` 和 `iptc4xmpExt` - 《國際新聞通訊標準》包含許多特定主題的元資料。
* RDF — 資源描述框架 — 用於通用語義Web元資料。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ`  — 基本工作票證。

### 應用程式專屬中繼資料 {#application-specific-metadata}

應用程式專用中繼資料包含技術和描述性中繼資料。 如果您使用此類中繼資料，其他應用程式可能無法使用中繼資料。 例如，不同的影像呈現應用程式可能無法存取 [!DNL Adobe Photoshop] 中繼資料。 您可以建立將應用程式特定屬性變更為標準屬性的工作流程步驟。

* ACDSee — 由管理的中繼資料 [!DNL ACDSee] 程式。 請參閱 [www.acdsee.com/](https://www.acdsee.com/).
* 專輯 —  [!DNL Adobe Photoshop Album].
* CQ — 使用者 [!DNL Experience Manager Assets].
* DAM — 使用者 [!DNL Experience Manager Assets].
* DEX - [!DNL Optima SC Description explorer] 是Windows作業系統元資料和檔案管理工具的集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto和MP -Microsoft Photo。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop].

### Digital Rights Management(DRM)中繼資料 {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* 加 —  [圖片許可通用系統](https://www.useplus.com).
* 稜鏡 —  [行業標準中繼資料的發佈需求](https://www.idealliance.org/prism-metadata).
* PRL — 稜鏡版權語言。
* PUR — 稜鏡使用權。
* `xmpPlus` - PLUS與XMP整合。

### 攝影專用中繼資料 {#photography-specific-metadata}

* Exif — 相機的技術資訊，包括GPS位置。
* CRS - [!DNL Camera Raw] 綱要。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF — 影像中繼資料(不僅適用於TIFF影像)。

### 特定於打印的元資料 {#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和協力廠商應用程式。
* 稜鏡 —  [行業標準中繼資料的發佈需求](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG`  — 分頁文字的XMP中繼資料。

### 多媒體特定中繼資料 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — 媒體管理。

## 中繼資料結構參考 {#metadata-schemata-reference}

以下引用包括有關特定元資料結構（按字母順序）的資訊，以及屬性及其定義的清單。

### 都柏林核心 {#dublin-core}

都柏林核心中繼資料提供一套標準化的慣例，用於描述資產，以便更容易找到。 在 [!DNL Assets], Dublin Core描述數字資產，包括視頻、聲音、影像和文檔。

簡單的都柏林核心元資料元素集(DCMES)包含下表中列出的15個元資料元素。 每個都柏林核心元素都是選用元素，且可重複。 您可以像新增或刪除媒體類型特定中繼資料一樣，新增或刪除都柏林核心中繼資料資訊。

除了DCMES之外，還有由Dublin Core Initiative建立的其他元資料元素。 請參閱 [都柏林核心計畫](https://dublincore.org/) 以取得更多資訊。

| 屬性 | 說明 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| 貢獻者 | 負責對內容作出貢獻的人員或公司。 |
| 覆蓋 | 資產涵蓋的地理位置或時段。 |
| 建立者 | 負責建立內容的人員或公司。 |
| 日期 | 與資產相關聯的日期或期間。 |
| 說明 | 資產的詳細資訊。 |
| 格式 | 資產的檔案格式、實體媒體或維度。 [!DNL Experience Manager] uses `dc:format` 以表示資產的MIME類型。 |
| 識別碼 | 資產的唯一參考。 |
| 語言 | 資產的語言(例如 `en` 英文版)。 |
| 發佈者 | 負責使資產可用的人員或公司。 |
| 關係 | 相關資產。 |
| 權利 | 關於誰擁有此資產的權限的資訊。 |
| source | 資產衍生自的相關資產。 |
| 主旨 | 資產主題。 |
| 標題 | 資產的名稱。 |
| 類型 | 資產的性質或類型。 |

### IPTC {#iptc}

國際新聞電信理事會(IPTC)是全球新聞機構的聯合體，其目標之一是制定和維護技術標準。 IPTC為影像定義了一套照片元資料標準，這些標準幾乎在攝影師中被普遍接受。 這些元資料標準是20世紀90年代建立的稱為IPTC資訊交換模型(IIM)的更廣泛標準的一部分。

雖然IPTC標頭資訊已被XMP取代，但XMP可使用IPTC核心架構和擴充架構。 在映像程式中，XMP和IPTC屬性都同步。

## 中繼資料導向的工作流程 {#metadata-driven-workflows}

建立中繼資料導向的工作流程可協助您自動執行某些程式，進而提高效率。 在元資料驅動的工作流中，工作流管理系統讀取該工作流，並因此執行一些預定義的操作。 例如，您可以使用中繼資料導向工作流程的一些方式：

* 工作流程可檢查影像是否具有標題。 若未這麼做，系統會通知您新增標題。
* 工作流程可以檢查資產上的版權聲明是否允許發佈。 因此，系統會將資產傳送至一部或另一部伺服器。
* 工作流程可以檢查沒有預先定義、強制中繼資料的資產，或是具有的資產 *無效* 中繼資料。

## XMP 中繼資料 {#xmp-metadata}

XMP（可擴充中繼資料平台）是 [!DNL Adobe Experience Manager Assets] 用於所有中繼資料管理。 XMP提供標準格式，供多種應用程式建立、處理和交換中繼資料。

除了提供可內嵌於所有檔案格式的通用中繼資料編碼外，XMP還提供豐富的 [內容模型](#xmp-core-concepts) 和 [支援Adobe](#advantages-of-xmp) 和其他公司，讓XMP的使用者 [!DNL Assets] 有一個強大的平台可以建立。

此 [XMP規格](https://www.adobe.com/devnet/xmp.html) 可從Adobe取得。

### 什麼是XMP? {#what-is-xmp}

Adobe先在Adobe Acrobat軟體產品中導入XMP標準。 此後，XMP標準被廣泛採用。 [!DNL Assets] 原生支援XMP — 由Adobe牽頭的可擴充中繼資料平台。 XMP是處理和儲存數位資產中標準化和專屬中繼資料的標準。 XMP的設計是通用標準，可讓多個應用程式有效處理中繼資料。

例如，生產專業人員可在Adobe的應用程式中使用內建的XMP支援，以傳遞多種檔案格式的資訊。 [!DNL Assets] 存放庫會擷取XMP中繼資料，並使用它來管理內容生命週期，並提供建立自動化工作流程的功能。

XMP借由提供資料模型、儲存模型和結構，標準化中繼資料的定義、建立和處理方式。 本節將介紹所有這些概念。

來自EXIF、ID3或Microsoft Office的所有舊版中繼資料都會自動轉譯為XMP，以延伸支援客戶專屬的中繼資料結構，例如產品目錄。

XMP中的中繼資料包含一組屬性。 這些屬性始終與稱為資源的特定實體相關聯；也就是說，屬性是關於資源。 在XMP的情況下，資源一律為資產。

### XMP生態系統 {#xmp-ecosystem}

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### XMP的優點 {#advantages-of-xmp}

XMP比其他編碼標準和架構有下列優點：

* XMP型中繼資料功能強大且微調。
* XMP可讓您擁有一個屬性的多個值。
* XMP具有標準化編碼，可讓您輕鬆交換中繼資料。
* XMP可擴充。 您可以新增其他資訊至資產。

XMP標準的設計可擴充，可讓您將自訂中繼資料類型新增至XMP資料。 EXIF則否 — 它有無法擴充的固定屬性清單。

>[!NOTE]
>
>XMP通常不允許嵌入二進位資料類型。 若要在XMP中傳送二進位資料（例如縮圖影像），必須以適合XML的格式編碼，例如 `Base64`.

### XMP概念 {#xmp-core-concepts}

以下各節將說明XMP的核心概念，包括命名空間和架構、屬性和值，以及語言替代項目。

#### 命名空間和架構 {#namespaces-and-schemata}

XMP架構是通用XML命名空間中的一組屬性名稱，包含資料類型和描述性資訊。 XMP架構由其XML命名空間URI標識。 使用命名空間可避免名稱相同但含義不同之不同結構中的屬性之間產生衝突。

例如， `Creator` 兩個獨立設計結構中的屬性可能代表建立資產的人員，或可能代表建立資產的應用程式(例如Adobe Photoshop)。

#### 屬性和值 {#properties-and-values}

XMP可包含一或多個結構中的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括：

* 都柏林核心架構： `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP基本結構： `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* XMP權限管理結構： `xmpRights:WebStatement`, `xmpRights:Marked`.
* XMP媒體管理結構： `xmpMM:DocumentID`.

#### 替代語言 {#language-alternatives}

XMP可讓您新增 `xml:lang` 屬性來指定文字的語言。

## 使用IPTC元資料 {#support-for-iptc-metadata}

了解如何 [!DNL Adobe Experience Manager Assets] 支援IPTC元資料、創意評等和通過 [!DNL Adobe Bridge] 其他 [!DNL Adobe Creative Cloud] 應用程式。

[!DNL Adobe Experience Manager Assets] 支援IPTC元資料標準，該標準被廣泛用於描述資產。 這邊， [!DNL Assets] 增強了攝影師、創意機構、圖書館、博物館等各方對其影像的接受度。

資產的預設中繼資料結構現在整合了IPTC核心和IPTC擴充功能中繼資料結構，以定義完整的中繼資料屬性，讓使用者能新增關於影像中顯示之人員、位置和產品的精確且可靠資料。 此外，也支援建立影像的日期、名稱和識別碼，以及彈性的權限資訊表達方式。

資產的「屬性」頁面現在包含個別的標籤，以在可編輯欄位中顯示IPTC核心和IPTC擴充功能中繼資料。

1. 從 [!DNL Assets] 使用者介面，選取影像。
1. 按一下 **[!UICONTROL 屬性]** 的上界。
1. 按一下 **[!UICONTROL IPTC]** 頁簽，查看資產的IPTC元資料。
1. 視需要編輯IPTC元資料屬性。

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. 按一下 **[!UICONTROL IPTC擴展]** 頁簽，查看資產的IPTC擴展元資料。
1. 視需要編輯IPTC擴展元資料屬性。
1. 按一下 **[!UICONTROL 儲存並關閉]** 以儲存變更。

### 創意評等支援 {#creative-rating-support}

除了顯示個別使用者評等和匯總評等外，「屬性」頁面現在還會顯示透過Adobe Bridge和其他創意應用程式指派給資產的評等

這些評等可在「進階」標 **[!UICONTROL 簽的「創作評分]** 」區段 **[!UICONTROL 下取得]** 。

此評等是唯讀屬性，範圍介於1到5之間。 您可以從「搜尋面板」根據資產的創作評等來搜尋資產。

不過，此屬性目前未編列索引，以避免與使用者所做的自訂變更產生任何衝突。

### 關鍵字支援 {#keyword-support}

此 **[!UICONTROL IPTC]** 的 [!UICONTROL 屬性] 頁面也會顯示透過Adobe Bridge和其他Adobe Creative Cloud應用程式新增至資產的關鍵字。 您也可以編輯這些關鍵字，並從 **[!UICONTROL IPTC]** 標籤。

![關鍵字](assets/keywords-in-iptc-tab.png)
