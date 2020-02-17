---
title: 中繼資料圖式參考
description: '瞭解描述資產中繼資料的標準慣例，包括Dublin Core、IPTC和其他中繼資料結構。 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 中繼資料圖式參考 {#metadata-schemata-reference}

以下參考包括關於特定元資料方案的資訊（按字母順序）以及屬性清單及其定義。

## Dublin Core {#dublin-core}

Dublin Core中繼資料提供一組標準化的慣例，用於描述資產，以便更容易找到。 在AEM Assets中，Dublin Core說明數位資產，包括視訊、音效、影像和檔案。

簡單的Dublin Core Metadata Element Set(DCMES)包含15個中繼資料元素，如下表所列。 每個Dublin core元素都是選用的，可重複。 您可以像新增或刪除媒體類型特定中繼資料一樣，新增或刪除Dublin Core中繼資料資訊。

除了DCMES之外，還有Dublin Core Initiative（都柏林核心計畫）建立的其他元資料元素。 如需詳細 [資訊，請參閱Dublin Core](https://dublincore.org/) Initiative。

| 屬性 | 說明 |
|---|---|
| contributor | 負責對內容作出貢獻的人士或公司。 |
| 覆蓋率 | 資產涵蓋的地理位置或時段。 |
| 製造者 | 負責建立內容的人員或公司。 |
| 日期 | 與資產相關的日期或期間。 |
| 說明 | 資產的詳細資訊。 |
| 格式 | 資產的檔案格式、實體媒體或尺寸。 AEM使用dc:format來表示資產的mime類型。 |
| 識別碼 | 資產的唯一參考。 |
| 語言 | 資產的語言（例如，英文為en）。 |
| publisher | 負責使資產可供使用的人員或公司。 |
| 關係 | 相關資產。 |
| 權利 | 關於誰有權使用此資產的資訊。 |
| source | 資產衍生自之相關資產。 |
| 主旨 | 資產的主題。 |
| 標題 | 資產的名稱。 |
| 類型 | 資產的性質或類別。 |

## IPTC {#iptc}

國際新聞通訊委員會(IPTC)是由全球新聞機構組成的聯合體，其目標之一是制定和維護技術標準。 IPTC為影像定義了一套像片中繼資料標準，在攝影師中幾乎被普遍接受。 這些元資料標準是20世紀90年代建立的更廣泛標準的一部分，即IPTC資訊交換模型(IIM)。

雖然IPTC標題資訊已大部份被XMP取代，但XMP可使用IPTC核心架構和擴充架構。 在影像程式中，XMP和IPTC屬性都會同步。
