---
title: 支援AEM Assets中的XMP中繼資料
description: 瞭解AEM Assets用於中繼資料管理的XMP（可擴充中繼資料平台）中繼資料標準。 XMP提供標準格式，讓您針對多種應用程式建立、處理和交換中繼資料。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# XMP中繼資料 {#xmp-metadata}

XMP（可擴充中繼資料平台）是AEM Assets用於所有中繼資料管理的中繼資料標準。 XMP提供標準格式，讓您針對多種應用程式建立、處理和交換中繼資料。

除了提供可嵌入所有檔案格式的通用中繼資料編碼外，XMP還提供多樣化的 [內容模型](xmp.md#xmp-core-concepts) ，並受 [Adobe](xmp.md#advantages-of-xmp) 和其他公司的支援，讓XMP與AEM Assets的使用者擁有強大的平台可以建立。

XMP規 [格可從](https://www.adobe.com/devnet/xmp.html) Adobe取得。

## 什麼是XMP? {#what-is-xmp}

AEM Assets本身支援XMP —— 由Adobe牽頭的可擴充中繼資料平台。 XMP是處理和儲存數位資產中標準化和專屬中繼資料的標準。 XMP是通用的標準，可讓多個應用程式有效地處理中繼資料。

例如，生產專業人員可使用Adobe應用程式內建的XMP支援，跨多種檔案格式傳遞資訊。 AEM Assets儲存庫會擷取XMP中繼資料，並使用它來管理內容生命週期，並提供建立自動化工作流程的功能。

XMP透過提供資料模型、儲存模型和結構描述，標準化中繼資料的定義、建立和處理方式。 本節將介紹這些概念。

EXIF、ID3或Microsoft office的所有舊式中繼資料都會自動轉譯為XMP,XMP可加以擴充，以支援客戶特定的中繼資料架構，例如產品型錄。

XMP中的中繼資料由一組屬性組成。 這些屬性始終與稱為資源的特定實體相關聯；即，屬性是關於資源的。 對於XMP，資源永遠是資產。

### Adobe {#adobe}

Adobe率先將XMP標準納入Adobe acrobat軟體產品。 自此，XMP標準得到廣泛採用。

### XMP生態系統 {#xmp-ecosystem}

XMP定義了 [中繼資料](https://en.wikipedia.org/wiki/Metadata) 模型，可與任何已定義的中繼資料項目集搭配使用。 XMP也定義了基本屬性的特定結構 [](https://en.wikipedia.org/wiki/XML_schema) ，這些基本屬性可用於記錄資源在經過多個處理步驟（從被拍攝、掃描或創作為文字）、通過照片編輯步驟(如 [](https://en.wikipedia.org/wiki/Image_scanner)[](https://en.wikipedia.org/wiki/Cropping_%28image%29) or color adjustment)到組合成最終影像時的歷史記錄。 XMP可讓每個軟體程式或裝置在過程中，將自己的資訊新增至數位資源，並保留在最終的數位檔案中。

XMP最常是使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium)[Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF)的子集進行序列化和儲存，該子集又以 [XML表示](https://en.wikipedia.org/wiki/XML)。

## XMP的優點 {#advantages-of-xmp}

XMP比其他編碼標準和圖式具有以下優點：

* 以XMP為基礎的中繼資料功能強大，而且具備細緻的功能。
* XMP可讓您針對一個屬性擁有多個值。
* XMP具備標準化編碼，可讓您輕鬆交換中繼資料。
* XMP具有可擴充性。 您可以新增其他資訊至資產。

### 可擴充 {#extensible}

XMP標準可擴充，讓您在XMP資料中新增自訂的中繼資料類型。 而EXIF則否——它有固定的屬性清單，無法延伸。

>[!NOTE]
>
>XMP通常不允許嵌入二進位資料類型。 若要以XMP格式傳送二進位資料（例如縮圖影像），它們必須以XML友好格式編碼，例如 `Base64`。

## XMP Core Concepts {#xmp-core-concepts}

以下各節介紹XMP的核心概念，包括名稱空間和圖式、屬性和值，以及語言替代。

### 命名空間和圖式 {#namespaces-and-schemata}

XMP架構是一組通用XML命名空間中的屬性名稱，其中包含資料類型和描述性資訊。 XMP架構由其XML命名空間URI來識別。 使用名稱空間可防止名稱相同但含義不同之不同結構中屬性之間的衝突。

例如，兩個 `Creator` 獨立設計結構中的屬性可能代表建立資產的人員，也可能代表建立資產的應用程式（例如Adobe Photoshop）。

### 屬性與值 {#properties-and-values}

XMP可以包括來自一個或多個方案的屬性。

例如，許多Adobe應用程式使用的典型子集可能包括：

* 都柏林核心架構：dc:title, dc:creator, dc:subject, dc:format, dc:rights
* XMP基本架構：xmp:CreateDate, xmp:CreatorTool, xmp:ModifyDate, xmp:metadataDate
* XMP權限管理架構：xmpRights:WebStatement, xmpRights:Marked
* XMP媒體管理架構：xmpMM:DocumentID

### 語言替代 {#language-alternatives}

XMP可讓您將屬性新增至 `xml:lang` 文字屬性，以指定文字的語言。
