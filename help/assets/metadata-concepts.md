---
title: 瞭解元資料概念
description: 瞭解元資料的需求和類型，以便更輕鬆地對資產進行分類和組織。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2720'
ht-degree: 9%

---

# 瞭解元資料概念 {#why-we-need-metadata}

元資料是指有關資料的資料。 在這方面，資料是指數字資產，比如影像。 中繼資料是進行高效率資產管理的關鍵所在。

元資料是資產可用的所有資料的集合，但不一定包含在該映像中。 元資料的一些示例包括：

* 資產的名稱。
* 上次修改的時間和日期。
* 儲存在儲存庫中的資產大小。
* 包含在中的資料夾的名稱。
* 相關資產或應用的標籤。

以上是基本元資料屬性 [!DNL Experience Manager] 可以管理資產，這允許用戶查看所有資產。 例如，在嘗試發現最近添加的資產時，按上次修改日期對資產進行排序非常有用。

您可以向數字資產添加更多高級資料，例如：

* 資產類型（影像、視頻、音頻剪輯或文檔）。
* 資產所有者。
* 資產的標題。
* 資產說明。
* 分配給資產的標籤。

更多元資料有助於您進一步對資產進行分類，並有助於隨著數字資訊量的增長。 僅根據檔案名可以管理幾百個檔案。 然而，此方法並不能調整規模。當涉案人數和受管理資產數量增加時，這個數字就不足。

隨著中繼資料增加，數位資產的價值也會成長，這是因為資產會變得

* 更易於存取 - 系統和使用者可以更輕鬆找到資產。
* 更易於管理 - 您可以更容易找到具有同一組屬性的資產，並將變更套用到這些資產。
* 完整 - 資產攜帶更多資訊和包含更多中繼資料的內容。

出於這些原因， [!DNL Assets] 為您提供了建立、管理和交換數字資產的元資料的正確方法。

## 元資料的類型 {#types-of-metadata}

元資料的兩種基本類型是技術元資料和描述元資料。

技術元資料對於處理數字資產且不應手動維護的軟體應用程式非常有用。 [!DNL Experience Manager Assets] 而其他軟體則自動確定技術元資料，當資產被修改時，元資料可能會改變。 資產的可用技術元資料在很大程度上取決於資產的檔案類型。 技術元資料的一些示例包括：

* 檔案大小。
* 影像的Dimension（高度和寬度）。
* 音頻或視頻檔案的比特率。
* 影像的解析度（詳細程度）。

描述性元資料是與應用程式域相關的元資料，例如資產來自的業務。 無法自動確定描述性元資料。 它是手動或半自動建立的。 例如，GPS攝像頭可以自動跟蹤經緯度，並添加地理標籤。

手動建立描述性元資料資訊的成本很高。 因此，制定標準以簡化跨軟體系統和組織的元資料交換。 [!DNL Experience Manager Assets] 支援元資料管理的所有相關標準。

## 編碼標準 {#encoding-standards}

在檔案中嵌入元資料有多種方法。 支援編碼標準的選擇：

* XMP:使用 [!DNL Assets] 將提取的元資料儲存在儲存庫中。
* ID3:檔案。
* Exif:的子菜單。
* 其他/舊版：從 [!DNL Microsoft Word]。 [!DNL PowerPoint]。 [!DNL Excel]等等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP為一個公開標準，由 [!DNL Experience Manager Assets] 所有元資料管理。 該標準提供可嵌入所有檔案格式的通用元資料編碼。 Adobe和其他公司XMP支援標準，因為它提供了豐富的內容模型。 標準和XMP的用戶 [!DNL Experience Manager Assets] 有一個強大的平台可以構建。 有關詳細資訊，請參見 [XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

在電腦或攜帶型MP3播放器上回放數字音頻檔案時，這些ID3標籤中儲存的資料會顯示。

ID3標籤是為MP3檔案格式設計的。 有關格式的其他資訊：

* ID3標籤在MP3和mp3PRO檔案中工作。
* WAV沒有標籤。
* WMA具有不允許開源實現的專有標籤。
* Ogg Vorbis使用Ogg容器中嵌入的Xiph注釋。
* AAC使用專有標籤格式。

### 艾希夫 {#exif}

可交換影像檔案格式(Exif)是數字攝影中最常用的元資料格式。 它提供了一種以多種檔案格式(如JPEG、TIFF、RIFF和WAV)嵌入固定的元資料屬性辭彙的方法。 Exif將元資料儲存為元資料名稱和元資料值的對。 這些元資料名稱 — 值對也稱為標籤，不要與中的標籤混淆 [!DNL Experience Manager]。 現代數位相機建立了Exif元資料，現代圖形軟體支援它。 Exif格式是元資料管理的最低公分母，尤其是映像。

Exif的一個主要限制是，一些常用的影像檔案格式(如BMP、GIF或PNG)不支援它。

Exif定義的元資料欄位通常是技術性的，在描述性元資料管理中使用有限。 因此， [!DNL Experience Manager Assets] 提供將Exif屬性映射到 [通用元資料架構](metadata-schemas.md) 進入 [XMP](xmp-writeback.md)。

### 其他元資料 {#other-metadata}

可以從檔案中嵌入的其他元資料包括 [!DNL Microsoft Word]。 [!DNL PowerPoint]。 [!DNL Excel]等等。

## 瞭解元資料架構 {#metadata-schemata}

元資料方案是可在各種應用程式中使用的預定義元資料屬性定義集。 屬性始終與資產關聯，這意味著屬性是資源的「關於」。

如果不存在滿足您需要的元資料架構，您也可以設計自己的元資料架構。 不要複製現有資訊。 在組織內，分離模式使共用元資料更加容易。 [!DNL Experience Manager] 為您提供了最流行的元資料架構的預設清單。 該清單可幫助您快速啟動元資料策略並快速選擇所需的元資料屬性。

下面列出了支援的元資料架構。

### 標準元資料 {#standard-metadata}

* DC - [!DNL Dublin Core] 是一組重要且廣泛使用的元資料。
* DICOM — 醫學數字成像和通信。
* `Iptc4xmpCore` 和 `iptc4xmpExt`  — 國際新聞通訊標準包含許多特定主題的元資料。
* RDF — 資源說明框架 — 用於通用語義Web元資料。
* XMP [!DNL Extensible Metadata Platform]。
* `xmpBJ`  — 基本作業票務。

### 特定於應用程式的元資料 {#application-specific-metadata}

特定於應用程式的元資料包括技術和描述性元資料。 如果使用此類元資料，則其他應用程式可能無法使用元資料。 例如，其他影像呈現應用程式可能無法訪問 [!DNL Adobe Photoshop] 元資料。 您可以建立將特定於應用程式的屬性更改為標準屬性的工作流步驟。

* ACDSee — 由 [!DNL ACDSee] 的子菜單。 請參閱 [www.acdsee.com](https://www.acdsee.com/)。
* 相冊 —  [!DNL Adobe Photoshop Album]。
* CQ — 使用者 [!DNL Experience Manager Assets]。
* DAM — 使用者 [!DNL Experience Manager Assets]。
* DEX - [!DNL Optima SC Description explorer] 是用於Windows作業系統元資料和檔案管理的工具的集合。
* CRS - [Adobe Photoshop Camera·勞](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom]。
* MediaPro - [iView媒體專業版](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto和MP -MicrosoftPhoto。
* PDF和PDF/X。
* Photoshop和普索。 [!DNL Adobe Photoshop]。

### Digital Rights Management(DRM)元資料 {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* 加 —  [圖片許可通用系統](https://www.useplus.com)。
* 稜鏡 —  [發佈行業標準元資料要求](https://www.idealliance.org/prism-metadata)。
* PRL - PRISM權利語言。
* PUR - PRISM使用權。
* `xmpPlus`  — 將PLUS與整合XMP。

### 特定於攝影的元資料 {#photography-specific-metadata}

* Exif — 來自相機的技術資訊，包括GPS位置。
* CRS - [!DNL Camera Raw] 架構。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF — 映像元資料(不僅用於TIFF映像)。

### 特定於打印的元資料 {#print-specific-metadata}

* PDF和PDF/X -Adobe PDF和第三方應用程式。
* 稜鏡 —  [發佈行業標準元資料要求](https://www.idealliance.org/prism-metadata)。
* XMP [!DNL Extensible Metadata Platform]。
* `xmpPG`  — 頁面XMP文本的元資料。

### 多媒體特定元資料 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — 介質管理。

## 元資料架構引用 {#metadata-schemata-reference}

以下引用包括有關特定元資料架構的資訊（按字母順序）以及屬性清單及其定義。

### 都柏林核心 {#dublin-core}

都柏林核心元資料提供了一套標準化的約定，用於描述資產，以便更容易找到資產。 在 [!DNL Assets], Dublin Core描述數字資產，包括視頻、聲音、影像和文檔。

簡單的都柏林核心元資料元素集(DCMES)包含下表中列出的15個元資料元素。 每個都柏林核心元素都是可選的，可以重複。 您可以添加或刪除特定於媒體類型的元資料的都柏林核心元資料資訊。

除了DCMES之外，都柏林核心計畫還建立了其他元資料元素。 查看 [都柏林核心計畫](https://dublincore.org/) 的子菜單。

| 屬性 | 說明 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| 貢獻者 | 負責對內容作出貢獻的人或公司。 |
| 覆蓋 | 資產所覆蓋的地理位置或時間期。 |
| 創造者 | 負責建立內容的人員或公司。 |
| 日期 | 與資產關聯的日期或時間段。 |
| 說明 | 有關資產的詳細資訊。 |
| 格式 | 資產的檔案格式、物理介質或維。 [!DNL Experience Manager] 使用 `dc:format` 表示資產的MIME類型。 |
| 標識符 | 資產的唯一引用。 |
| 語言 | 資產的語言(例如， `en` )。 |
| 發佈者 | 負責使資產可用的人員或公司。 |
| 關係 | 相關資產。 |
| 權利 | 有關誰有權訪問此資產的資訊。 |
| source | 資產所衍生之相關資產。 |
| 主題 | 資產的主題。 |
| 標題 | 資產的名稱。 |
| 類型 | 資產的性質或類別。 |

### IPTC {#iptc}

國際新聞電信委員會(IPTC)是全球新聞機構的聯合體 — 其目標之一是制定和維持技術標準。 IPTC為影像定義了一套幾乎被攝影師普遍接受的照片元資料標準。 這些元資料標準是20世紀90年代建立的被稱為IPTC資訊交換模型(IIM)的更廣泛標準的一部分。

雖然IPTC頭資訊已被大多數替XMP代，但IPTC核心架構和擴展架構可供XMP使用。 在映像程式中，同XMP步和IPTC屬性。

## 元資料驅動的工作流 {#metadata-driven-workflows}

建立元資料驅動的工作流有助於您自動執行某些流程，從而提高效率。 在元資料驅動的工作流中，工作流管理系統讀取該工作流，並因此執行一些預定義的操作。 例如，您可以使用元資料驅動的工作流的一些方法：

* 工作流可以檢查影像是否具有標題。 如果沒有，系統會通知添加標題。
* 工作流可以檢查資產上的版權聲明是否允許分發。 因此，系統將資產發送到一台或另一台伺服器。
* 工作流可以檢查沒有預定義的強制元資料或具有 *無效* 元資料。

## XMP 中繼資料 {#xmp-metadata}

XMP（可擴展元資料平台）是 [!DNL Adobe Experience Manager Assets] 所有元資料管理。 為XMP各種應用程式建立、處理和交換元資料提供了標準格式。

除了提供可嵌入到所有檔案格式的通用元資料編碼之外，還XMP提供了豐富的 [內容模型](#xmp-core-concepts) 和 [由Adobe支援](#advantages-of-xmp) 以及其他公司的用戶XMP, [!DNL Assets] 有一個強大的平台可以構建。

的 [XMP規格](https://www.adobe.com/devnet/xmp.html) 的子菜單。

### 什麼XMP? {#what-is-xmp}

Adobe首先將XMP標準作為Adobe Acrobat軟體產品的一部分。 自此，該標XMP準被廣泛採用。 [!DNL Assets] 本機支XMP持由Adobe牽頭的可擴展元資料平台。 XMP是處理和儲存數字資產中標準化和專有元資料的標準。 設計XMP為允許多個應用程式有效地使用元資料的通用標準。

例如，生產專業人員使用Adobe應用程式內XMP的內置支援跨多種檔案格式傳遞資訊。 [!DNL Assets] 儲存庫提取XMP元資料並使用它來管理內容生命週期，並提供了建立自動化工作流的能力。

通XMP過提供資料模型、儲存模型和模式來標準化元資料的定義、建立和處理方式。 本節將介紹所有這些概念。

EXIF、ID3或Microsoft辦事處的所有舊元資料都會自動轉換為XMP，可以擴展為支援特定於客戶的元資料架構，如產品目錄。

中的元XMP資料由一組屬性組成。 這些屬性始終與稱為資源的特定實體相關聯；即，屬性是「關於」資源。 在這種情況XMP下，資源始終是資產。

### XMP生態系統 {#xmp-ecosystem}

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟 (從被拍攝、掃描或創作為文字) 、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。XMP可讓每個軟體程式或裝置沿途將其資訊新增至數位資源，然後再保留在最終數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

### 優XMP勢 {#advantages-of-xmp}

與其XMP他編碼標準和方案相比具有以下優點：

* 基XMP於元資料功能強大且細粒度。
* 可XMP以為一個屬性設定多個值。
* XMP具有標準化編碼，可輕鬆交換元資料。
* XMP可擴展。 您可以在資產中添加其他資訊。

該標XMP準設計為可擴展，允許您向資料中添加自定義類型的元XMP資料。 而EXIF則不是 — 它有一個無法擴展的固定屬性清單。

>[!NOTE]
>
>通XMP常不允許嵌入二進位資料類型。 要以縮略圖XMP像等形式傳送二進位資料，必須以XML友好格式(如 `Base64`。

### XMP概念 {#xmp-core-concepts}

以下各節介紹了命名空間XMP和架構、屬性和值以及語言替代方案的核心概念。

#### 命名空間和架構 {#namespaces-and-schemata}

架XMP構是包含資料類型和描述性資訊的公共XML命名空間中的一組屬性名稱。 架XMP構由其XML命名空間URI標識。 使用命名空間可防止名稱相同但含義不同的不同架構中的屬性之間發生衝突。

例如， `Creator` 兩個獨立設計方案中的屬性可能是指建立資產的人員，也可能是指建立資產的應用程式(例如，Adobe Photoshop)。

#### 屬性和值 {#properties-and-values}

可XMP以包括來自一個或多個架構的屬性。 例如，許多Adobe應用程式使用的典型子集可能包括以下內容：

* 都柏林核心架構： `dc:title`。 `dc:creator`。 `dc:subject`。 `dc:format`。 `dc:rights`。
* XMP基本架構 `xmp:CreateDate`。 `xmp:CreatorTool`。 `xmp:ModifyDate`。 `xmp:metadataDate`。
* XMP權限管理架構 `xmpRights:WebStatement`。 `xmpRights:Marked`。
* XMP媒體管理架構 `xmpMM:DocumentID`。

#### 語言替代 {#language-alternatives}

可XMP以添加 `xml:lang` 屬性到文本屬性以指定文本的語言。

## 使用IPTC元資料 {#support-for-iptc-metadata}

瞭解如何 [!DNL Adobe Experience Manager Assets] 支援IPTC元資料、Creative評級和通過 [!DNL Adobe Bridge] 其他 [!DNL Adobe Creative Cloud] 。

[!DNL Adobe Experience Manager Assets] 支援廣泛用於描述資產的IPTC元資料標準。 這邊， [!DNL Assets] 加強攝影師、創意機構、圖書館、博物館等各方對其形象的接受。

資產的預設元資料模式現在結合了IPTC核心和IPTC擴展元資料模式來定義全面的元資料屬性，這些屬性允許用戶添加有關影像中顯示的人員、位置和產品的精確可靠資料。 它還支援有關建立影像的日期、名稱和標識符，以及表達權限資訊的靈活方法。

資產的「屬性」頁現在包含單獨的頁籤，以在可編輯欄位中顯示IPTC核心和IPTC擴展元資料。

1. 從 [!DNL Assets] 用戶介面，選擇影像。
1. 按一下 **[!UICONTROL 屬性]** 的子菜單。
1. 按一下 **[!UICONTROL IPTC]** 頁籤，查看資產的IPTC元資料。
1. 根據需要編輯IPTC元資料屬性。

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. 按一下 **[!UICONTROL IPTC擴展]** 頁籤，查看資產的IPTC擴展元資料。
1. 根據需要編輯IPTC擴展元資料屬性。
1. 按一下 **[!UICONTROL 保存並關閉]** 的子菜單。

### 創意評級支援 {#creative-rating-support}

除了顯示單個用戶評級和聚合評級外，「屬性」頁現在還顯示通過Adobe Bridge和其他Creative Apps為資產分配的評級

這些評等可在「進階」標 **[!UICONTROL 簽的「創作評分]** 」區段 **[!UICONTROL 下取得]** 。

此評級為只讀屬性，範圍在1-5之間。 您可以根據資產的「創意評級」從「搜索面板」中搜索資產。

但是，當前未對此屬性編製索引，以避免與用戶所做的自定義更改發生任何衝突。

### 關鍵字支援 {#keyword-support}

的 **[!UICONTROL IPTC]** 頁籤 [!UICONTROL 屬性] 頁面還顯示通過Adobe Bridge和其他Adobe Creative Cloud應用添加到資產中的關鍵字。 您也可以編輯這些關鍵字，並從 **[!UICONTROL IPTC]** 頁籤。

![關鍵字](assets/keywords-in-iptc-tab.png)
