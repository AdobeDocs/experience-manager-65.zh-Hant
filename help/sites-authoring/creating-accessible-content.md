---
title: 為Adobe Experience Manager建立無障礙內容（符合WCAG 2.1）
description: 使用AEM協助讓身心障礙人士存取及使用網路內容
exl-id: 2145d761-f51d-482b-a0e7-ef7500c4872f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '13636'
ht-degree: 2%

---

# 建立可存取的內容 (符合 WCAG 2.1) {#creating-accessible-content-wcag-conformance}

此 [網頁內容可及性指引(WCAG) 2.1](https://www.w3.org/TR/WCAG/)，由下列人員撰寫： [全球資訊網協會的工作小組](https://www.w3.org/groups/#Accessibility_Guidelines_Working_Group)，包含一系列技術獨立指引和成功標準，協助身心障礙人士存取及使用網路內容。

作為介紹，聯盟提供了一系列區段和支援檔案：

* [WCAG 2.1的新功能](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [如何滿足WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [瞭解WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [適用於WCAG 2.1的技術](https://www.w3.org/WAI/WCAG21/Techniques/)
* [WCAG檔案](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

此外，請參閱：
* 此 [WCAG 2.1快速指南](/help/managing/qg-wcag.md).
* 此 [Adobe解決方案的無障礙合規報告](https://www.adobe.com/accessibility/compliance.html).
* [設定RTF編輯器以產生無障礙內容](/help/sites-administering/rte-accessible-content.md)

指引會根據三個一致性層級進行分級：A級（最低）、AA級和AAA級（最高）。 簡而言之，層級的定義如下：

* **** A級：您的網站達到基本的最低協助功能等級。要達到此級別，將滿足所有A級成功標準。
* **AA級：** 這是您努力追求的最佳無障礙環境支援等級，其中您的網站可達到基本無障礙環境支援等級，因此大部分使用者都可使用大部分的技術。 要達到此級別，將滿足所有A級和A級成功標準。
* **AAA級：** 您的網站可達到高水準的協助工具。 要達到此級別，將滿足所有A級、AA級和AAA級成功標準。

建立網站時，您必須決定要讓網站遵循的整體等級。

以下小節會顯示 [WCAG 2.1指引圖層](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) 具有A級和AA級的相關成功標準 [一致性層級](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1).

>[!NOTE]
>
>本檔案將使用下列專案：
>
>* 此 [WCAG 2.1指引的簡稱](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* 此 [WCAG 2.1指引中使用的編號](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) 以便與WCAG網站進行交叉參照。

## 准則1：可感知 {#principle-perceivable}

[准則1：可感知 — 資訊和使用者介面元件必須以使用者可感知的方式呈現給使用者。](https://www.w3.org/TR/WCAG/#perceivable)

### 替代文字(1.1) {#text-alternatives}

[指引1.1替代文字：為任何非文字內容提供替代文字，以便可以變更為人們需要的其他形式，例如大字型、盲文、語音、符號或更簡單的語言。](https://www.w3.org/TR/WCAG/#text-alternatives)

### 非文字內容(1.1.1) {#non-text-content}

* 成功標準1.1.1
* A級
* 非文字內容：除了下列情況外，所有呈現給使用者的非文字內容都有相同用途的替代文字。

#### 用途 — 非文字內容(1.1.1) {#purpose-non-text-content}

網頁上的資訊可以用許多不同的非文字格式提供，例如圖片、影片、動畫、圖表和圖形。 失明或嚴重視力障礙的人無法看到非文字內容。 但他們可以透過熒幕閱讀器讀取文字內容，或透過點字顯示裝置以觸覺形式呈現文字內容。 因此，透過以圖形格式提供文字替代內容，看不到圖形內容的人可以存取內容所提供的資訊的同等版本。

另一個有用的優點是，替代文字可讓搜尋引擎技術為非文字內容編制索引。

#### 如何達到標準 — 非文字內容(1.1.1) {#how-to-meet-non-text-content}

對於靜態圖形，基本要求是為圖形提供對等文字替代文字。 這可以在以下位置完成： **替代文字** 欄位。 例如，請參閱核心元件 **[影像](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html)**.

>[!NOTE]
>
>部分現成可用的核心元件，例如 **[輪播](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html)** 不提供 **替代文字** 用於新增替代文字說明至個別影像的欄位，不過 **標籤** 欄位(**[協助工具](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html#accessibility-tab)** 標籤)。
>
>當針對您的AEM例項實作這些版本時，您的開發團隊必須設定這些元件以支援 `alt` 屬性，讓作者可以將其新增至內容(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

AEM需要 **替代文字** 預設要填寫的欄位。 如果影像是純粹的裝飾且不需要替代文字，則 **影像為裝飾性** 選項時可核取。

#### 建立良好的替代文字 {#creating-good-text-alternatives}

有多種形式的非文字內容，因此替代文字的值取決於圖形在網頁中所扮演的角色。 一些要遵循的經驗法則包括：

* 替代文字應簡潔明瞭，但能清楚擷取非文字內容所提供的基本資訊。
* 應避免過長的說明（超過100個字元）。 如果替代文字需要更多細節：
   * 在替代文字中提供簡短說明
   * 並在相同頁面其他位置或不同網頁中有更長的說明。 將影像設為連結，或是在影像旁邊放置文字連結，即可連結至此個別說明。
* 替代文字不應復寫相同頁面上附近文字表單中提供的內容。 請記住，許多影像都是已涵蓋在頁面文字中的點插圖，因此可能有詳細的替代文字。
* 如果非文字內容是另一個頁面或檔案的連結，且沒有其他文字構成相同連結的一部分，則影像的替代文字必須指出連結的目的地。 它不能描述影像。
* 如果非文字內容包含在按鈕元素中，且沒有文字構成相同按鈕的一部分，則影像的替代文字必須表示按鈕的功能。 它不能描述影像。
* 指定空白(null)替代文字是影像完全可以接受的作法，但前提是影像不需要替代文字。 例如，它是純粹的裝飾圖形，或頁面文字中存在對等文字。

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

需要替代文字的特定非文字內容型別可能包括：

* 說明性像片：指人物、物件或地點的影像。 請務必思考像片在頁面中的角色，並描述影像內容，因為輔助技術將會朗讀元素型別(例如 `graphic` 或 `image`)；使用可增加清晰度 `screenshot` 或 `illustration` 以替代文字說明，但這取決於內容。 一致性是一個重要因素，整個撰寫團隊都必須做出決定，且此決定應套用至整個使用者體驗。
* 圖示：這些是傳達特定資訊的小圖形符號（圖形）。 每個頁面和網站都必須使用一致的量度。 圖示在頁面或網站上的所有例項都應使用相同的簡短替代文字，除非這樣做會造成相鄰文字不必要的重複。
* 圖表和圖形：這些通常表示數值資料。 因此，提供替代文字的一個選項可能是包含圖表或圖形中顯示的主要趨勢的簡短摘要。 如有需要，也可在文字中使用 **說明** 中的欄位 **進階** 影像屬性索引標籤。 此外，您也可以在頁面或網站的其他位置，以表格形式提供來源資料。
* 地圖、圖表、流程圖：對於提供空間資料的圖形（例如，支援描述物件或程式之間的關係），請確定關鍵訊息是以文字格式提供，並且此文字資訊位於每個關聯資料點附近。 對於地圖，提供等同全文的地圖可能不切實際，但如果提供地圖以幫助人們找到特定位置的方式，則地圖影像的替代文字可以簡短地指出 *X的地圖*，接著在頁面其他位置的文字中或透過 **說明** 中的欄位 **進階** 的標籤 **影像** 元件。
* 驗證碼：驗證碼是 *完全自動化的公用圖靈測試，將電腦和人類區分開來*. 這是用於網頁的安全性檢查，可區分人類與惡意軟體，但可能會造成協助工具障礙。 這些影像會要求使用者描述他們所看到的內容，以便通過安全性測試。 無法提供影像的替代文字，因此您必須考慮替代非圖形解決方案。 W3C提供一些建議，例如：
   * 邏輯謎題
   * 使用聲音輸出而非影像
   * 限制使用帳戶和垃圾郵件篩選器。
* 背景影像：這些是使用階層式樣式表(CSS)而不是HTML來達成。 這表示無法指定替代文字值。 因此，背景影像不應提供重要的文字資訊，即使提供，頁面文字中也必須提供此資訊。 不過，當影像無法顯示時，請務必顯示替代背景。

>[!NOTE]
>
>背景和前景文字之間應該有適當等級的對比；這部分將詳加討論 [對比（最小） (1.4.3)](#contrast-minimum).

#### 更多資訊 — 非文字內容(1.1.1) {#more-information-non-text-content}

* [瞭解成功標準1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [如何達到成功標準1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [驗證碼的W3C說明和替代方案](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### 時間型媒體(1.2) {#time-based-media}

[准則1.2以時間為主的媒體：提供以時間為主的媒體替代方案。](https://www.w3.org/TR/WCAG/#time-based-media)

此准則所處理的網路內容為 *基於時間*. 這涵蓋使用者可播放的內容（例如視訊、音訊和動畫內容），並可預先錄製或即時資料流。

### 純音訊和純視訊（預先錄製）(1.2.1) {#audio-only-and-video-only-prerecorded}

* 成功標準1.2.1
* A級
* 純音訊和純視訊（預先錄製）：對於預先錄製的純音訊和預先錄製的純視訊媒體，除非音訊或視訊是文字的替代媒體，且標示清楚如下，否則情況如下：
   * 僅限預先錄製的音訊：時間型媒體的替代方案，為預先錄製的僅限音訊內容提供同等資訊。
   * 僅限預先錄製的視訊：這是以時間為基礎的媒體的替代選擇，或是提供的音訊曲目，可提供與預先錄製的僅限視訊內容相同的資訊。

#### 用途 — 純音訊和純視訊（預先錄製）(1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

下列使用者可能會遇到視訊與音訊的無障礙問題：

* 沒有音軌或音軌不足以通知視訊或動畫中正在發生的事情時，患有視覺障礙的人；
* 有聽力障礙或耳聾且聽不到音軌的人；
* 聽得見音軌但不瞭解說話內容的人（例如，因為這是他們不懂的語言）。

使用不支援以特定媒體格式(例如AdobeFlash)播放內容之瀏覽器或裝置的使用者，也可能無法播放視訊或音訊。

以不同的格式提供這項資訊，例如文字（或沒有音訊的視訊），可以讓無法存取原始內容的人存取這些資訊。

#### 如何達到標準 — 純音訊和純視訊（預先錄製）(1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* 如果內容是預先錄製不含視訊的音訊（例如播客）：
   * 在緊接內容之前或之後的位置提供音訊內容文字記錄的連結。 成績單應該是一個HTML頁面，其中包含所有口語和重要非口語內容的對等文字，以及說話者的指示、設定說明、聲音表情以及任何其他重要音訊的說明。
* 如果內容是無音訊的動畫或預先錄製的視訊：
   * 提供緊接在內容之前或之後的連結，以提供視訊所提供的資訊對等文字說明
   * 或是常用的音訊格式（例如MP3）中的對等音訊描述。

>[!NOTE]
>
>如果音訊或視訊內容是作為相同網頁上其他格式內容的替代內容提供，則可能不需要額外的替代內容。
>
>准則， [瞭解WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)，提供進一步資訊。

在AEM網頁中插入多媒體的方式與插入影像類似。 不過，由於多媒體內容遠不止是靜態影像，因此控制多媒體播放的方式有各種不同的設定和選項。

>[!NOTE]
>
>將多媒體與資訊性內容搭配使用時，您也必須建立替代內容的連結。 例如，若要包含文字記錄，請建立HTML頁面以顯示記錄，然後在音訊內容旁邊或下方新增連結。

#### 更多資訊 — 純音訊和純視訊（預先錄製）(1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [瞭解成功標準1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [如何達到成功標準1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### 註解（預先錄製） (1.2.2) {#captions-prerecorded}

* 成功標準1.2.2
* A級
* 註解（預先錄製）：除了媒體是文字的替代媒體，且明確標示為文字外，同步媒體中的所有預先錄製的音訊內容都會提供註解。

#### 用途 — 字幕（預先錄製）(1.2.2) {#purpose-captions-prerecorded}

耳聾或聽力缺佳的人將無法或很難存取音訊內容。 註解是口語和非口語音訊的對等文字，會在視訊期間的適當時間顯示在熒幕上。 它們可讓無法聽到音訊的人瞭解正在發生的事情。

#### 如何達到標準 — 字幕（預先錄製）(1.2.2) {#how-to-meet-captions-prerecorded}

註解可以是：

* 開啟：播放視訊時一律可見
* 隱藏式：註解可以由使用者開啟或關閉

儘可能使用隱藏式字幕，因為使用者可以選擇是否檢視字幕。

對於隱藏式字幕，請以適當的格式建立並提供同步化的字幕檔案(例如 [SMIL](https://www.w3.org/AudioVideo/))以及視訊檔案(如何操作的詳細資訊不在本指南的涵蓋範圍內，但我們提供了一些教學課程的連結，位於 [更多資訊 — 字幕（預先錄製）(1.2.2)](#more-information-captions-prerecorded))。 請務必提供註解或在視訊播放器中啟用註解功能，讓使用者知道視訊有註解可以使用。

如果您必須使用開啟的註解，請將文字內嵌到視訊曲目中。 您可以使用視訊編輯應用程式來達到此目的，該應用程式允許將標題重疊在視訊上。

#### 更多資訊 — 字幕（預先錄製）(1.2.2) {#more-information-captions-prerecorded}

* [瞭解成功標準1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [如何達到成功標準1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### 音訊描述或替代媒體（預先錄製） (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* 成功標準1.2.3
* A級
* 音訊說明或替代媒體（預先錄製）：除了媒體是文字的替代媒體，且明確標示為文字的替代媒體外，系統會為同步媒體提供時間型媒體或預先錄製的視訊內容的替代媒體。

#### 用途 — 音訊說明或替代媒體（預先錄製） (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

如果影片或動畫中的資訊僅以視覺效果呈現，或是音軌提供的資訊不足以讓使用者瞭解正在發生的視覺效果，失明或患有視覺障礙的使用者將會遇到協助工具障礙。

#### 如何達到標準 — 音訊說明或替代媒體（預先錄製） (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

您可採取兩種方法來達到此成功標準。 任一專案皆可接受：

1. 為視訊內容加入其他音訊說明。 有三種方法可達成此目的：
   * 在現有對話方塊中暫停期間，提供未顯示在現有音軌中的場景變更資訊；
   * 提供包含原始音軌的全新、額外和選購音軌，但也包含有關場景變更的額外音訊資訊。
      * 使用者可以在現有的音軌之間切換(這項 *不會* 包含音訊說明)和新的音軌(可 *會* 包含音訊說明)。
      * 這可防止不需要額外說明的使用者中斷。
   * 建立視訊內容的第二個版本，以允許擴充音訊說明。 這可藉由在適當位置暫時暫停音訊和視訊，減少在現有對話方塊之間提供詳細音訊說明的困難。 因此，在動作再次開始之前，可以輸入更長的音訊說明。 如同上一個範例，最好將此作為選用的額外音訊曲目提供，以防止對不需要額外說明的使用者造成中斷。
1. 提供文字稿，其為視訊或動畫的音訊與視覺元素的適當對等文字。 這應包括（在適當情況下）指出講話者、設定說明、任何事件，或視覺上顯示的資訊和語音表述內容。 視其長度而定，您可以將文字記錄放在與視訊或動畫相同的頁面上，或放在另一個頁面上；如果您選擇後一個選項，請在視訊或動畫旁提供文字記錄的連結。

本指南不涵蓋如何建立音訊描述視訊的確切細節。 建立視訊和音訊說明可能相當耗時，但其他Adobe產品可協助您完成這些工作。

#### 更多資訊 — 音訊說明或替代媒體（預先錄製） (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [瞭解成功標準1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [如何達到成功標準1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### 註解（即時） (1.2.4)  {#captions-live}

* 成功標準1.2.4
* AA級
* 註解（即時）：為同步媒體中的所有即時音訊內容提供註解。

#### 用途 — 註解（即時） (1.2.4) {#purpose-captions-live}

此成功標準與 [註解（預先錄製）](#captions-prerecorded) 因為除了此成功標準需要處理網路直播等即時簡報之外，此標準還能解決耳聾或聽力缺佳使用者遇到的協助工具問題。

#### 如何達到標準 — 字幕（即時）(1.2.4) {#how-to-meet-captions-live}

遵循提供的指引 [註解（預先錄製）](#captions-prerecorded) 以上。 然而，由於媒體的即時性質，提供註解必須儘快建立，並對正在發生的事情做出回應。 因此，您應該考慮使用即時字幕或語音轉文字工具。

詳細指示不在本檔案的涵蓋範圍內，但下列資源提供有用的資訊：

* [WebAIM：即時字幕](https://webaim.org/techniques/captions/realtime)

* [AccessComputing專案（華盛頓大學）：能否使用語音辨識自動產生字幕？](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### 更多資訊 — 字幕（即時） (1.2.4) {#more-information-captions-live}

* [瞭解成功標準1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [如何達到成功標準1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### 音訊說明（預先錄製） (1.2.5)  {#audio-description-prerecorded}

* 成功標準1.2.5
* AA級
* 音訊說明（預先錄製）：提供同步媒體中所有預先錄製的視訊內容的音訊說明。

#### 用途 — 音訊說明（預先錄製） (1.2.5) {#purpose-audio-description-prerecorded}

此成功標準與 [音訊說明或替代媒體（預先錄製）](#audio-description-or-media-alternative-prerecorded)但作者必須提供更詳細的音訊說明才能符合AA級標準。

#### 如何達到標準 — 音訊說明（預先錄製） (1.2.5) {#how-to-meet-audio-description-prerecorded}

遵循提供的指引 [音訊說明或替代媒體（預先錄製）](#audio-description-or-media-alternative-prerecorded).

#### 更多資訊 — 音訊說明（預先錄製） (1.2.5) {#more-information-audio-description-prerecorded}

* [瞭解成功標準1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [如何達到成功標準1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### 可調整(1.3) {#adaptable}

[指南1.3可調整：建立能以不同方式呈現的內容（例如更簡單的版面），而不會遺失資訊或結構。](https://www.w3.org/TR/WCAG/#adaptable)

本指引涵蓋支援以下人員所需的需求：

* 可能無法存取作者以該內容預設呈現方式呈現的資訊（例如，多欄版面或大量使用顏色和/或影像的頁面）。

* 可能使用純音訊或替代視覺顯示，例如大型文字或高對比度。

### 資訊和關係(1.3.1)  {#info-and-relationships}

* 成功標準1.3.1
* A級
* 資訊和關係：透過表示法傳遞的資訊、結構和關係可以程式化方式決定，或是可在文字中使用。

#### 用途 — 資訊和關係(1.3.1) {#purpose-info-and-relationships}

殘障人士使用的許多輔助技術都仰賴結構性資訊來有效顯示或 *瞭解* 內容。 此結構資訊可以採用頁面標題、表格列與欄標題，以及清單型別的形式。 例如，熒幕助讀程式可讓使用者在頁面中從標題導覽至標題。 但是，當頁面內容似乎只有透過視覺樣式而非基礎HTML的結構時，則沒有可用於輔助技術的結構資訊，限制其支援更輕鬆瀏覽的能力。

此成功標準旨在確保透過HTML或其他編碼技術以程式設計方式提供此類結構資訊，以便瀏覽器和輔助技術可存取並利用這些資訊。

#### 如何達到標準 — 資訊和關係(1.3.1) {#how-to-meet-info-and-relationships}

AEM可讓您使用適當的HTML元素，輕鬆建構語義上有意義的網頁內容。 在RTE （文字元件）中開啟頁面內容，並使用 **引數格式** 選單（段落符號），指定適當的結構元素（例如，段落和標題）。

在適用的情況下，您可以使用下列元素，確定您的網頁指定了適當的結構：

* **標題：** 只要您已啟用RTE的協助工具功能，AEM就會提供三個層級的頁面標題。 您可以使用這些項目來識別內容的區段和子區段。標題1是標題的最高級別，標題3是最低級別。系統管理員可以配置系統以允許使用更多標題級別。

* **清單**：您可以使用HTML來指定三種不同型別的清單：
   * 元素 `<ul>` 用於無序 *列*  (項目符號) 清單。識別個別清單專案時會使用 `<li>` 元素。 在RTE中，使用 **專案符號清單** 圖示。
   * 此 `<ol>` 元素用於 *編號* 清單。 識別個別清單專案時會使用 `<li>` 元素。 在RTE中，使用 **編號清單** 圖示。

  如果要將現有內容變更為特定清單型別，請反白適當的文字並選取適當的清單型別。 如前一個顯示段落文字輸入方式的範例一樣，適當的清單元素會自動新增至您的HTML。

  在全螢幕模式中，會顯示個別 **的「項目符號清單** 」和「 **** 編號清單」圖示。當未處於全螢幕模式時，單一「清單」圖示後面會提供這兩個 **選項** 。

* **表格**：資料表格必須使用HTML表格元素來識別：
   * 一 `<table>` 元素
   * a `<tr>` 表格每一列的元素
   * a `<th>` 每個列和欄標題的元素
   * a `<td>` 每個資料儲存格的元素

  此外，可存取的表格會使用下列元素和屬性：

   * 此 `<caption>` 元素可用來提供表格的可見標題。 字幕預設會顯示在表格上方，但可以使用CSS適當地放置字幕。 註解會以程式設計方式與表格相關聯，因此是一種提供內容簡介的實用方法。
   * 此 `<summary>` 元素透過提供視力正常使用者看見的摘要，協助失明使用者更輕鬆地瞭解表格中呈現的資訊。 這在使用了複雜或非常規表格佈局的情況下很有用（此屬性不會顯示在瀏覽器中，只會由輔助型技術讀取）。
   * 此 `scope` 的屬性 `<th>` 元素是用來指出儲存格是否代表特定列的標題，或代表特定欄的標題。 在複雜的表格中使用標題和id屬性也是類似的方法，其中資料儲存格可能會與一個或多個標題相關聯。

  >[!NOTE]
  >
  >依預設，這些元素和屬性不直接可用，但系統管理員可以在以下位置新增對這些值的支援： **表格屬性** 對話方塊(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes).

  若要開啟 **表格** 對話方塊，您可在其中選取 **表格屬性** 標籤：

   * 定義適當的 **註解**.
   * 理想情況下，請移除「寬 **度」、「邊框高度」、「邊框高度」、「邊框高度**」、「單元格間距」、「單元格間距 **」、「單元格**************&#x200B;間距」的預設值。因為這些屬性可以在全局樣式表中設定。

  然後，您可以使用 **儲存格屬性** 若要選擇儲存格是資料或標題儲存格：

* **強調**：使用 `<strong>` 或 `<em>` 表示強調的元素。 請勿使用標題來反白標示段落中的文字。
   * 反白您要強調的文字；
   * 按一下 **B** 圖示(for `<strong>`)或 **I** 圖示(for `<em>`)中顯示 **屬性** 面板(請確定已選取HTML)。

     >[!NOTE]
     >
     >標準AEM安裝中的RTE設定為使用：
     >
     >* `<b>` 代表 `<strong>`
     >* `<i>` 代表 `<em>`
     >
     >實際上相同，但 `<strong>` 和 `<em>` 偏好使用，因為它們的語意正確html。 您的開發團隊可以設定要使用的RTE `<strong>` 和 `<em>` (而非 `<b>` 和 `<i>`)時，退出連結逾時。

* **複雜資料表**：有時候，如果有具有兩個或多個標題級別的複雜表格，則基本表格屬性可能不足以提供所有必要的結構資訊。 對於這些型別的複雜表格，必須使用標題與其相關儲存格建立直接關係 **頁首** 和 **id** 屬性。

  >[!NOTE]
  >
  >ID屬性無法在現成安裝中使用。 可透過在RTE中設定HTML規則和序列化程式來啟用它。

  例如，在下表的標題和ID中，會對輔助技術使用者進行程式化關聯。

  ```xml
    <table>
      <tr>
        <th rowspan="2" id="h">Homework</th>
        <th colspan="3" id="e">Exams</th>
        <th colspan="3" id="p">Projects</th>
      </tr>
      <tr>
        <th id="e1" headers="e">1</th>
        <th id="e2" headers="e">2</th>
        <th id="ef" headers="e">Final</th>
        <th id="p1" headers="p">1</th>
        <th id="p2" headers="p">2</th>
        <th id="pf" headers="p">Final</th>
      </tr>
      <tr>
        <td headers="h">15%</td>
        <td headers="e e1">15%</td>
        <td headers="e e2">15%</td>
        <td headers="e ef">20%</td>
        <td headers="p p1">10%</td>
        <td headers="p p2">10%</td>
        <td headers="p pf">15%</td>
      </tr>
    </table>
  ```

  若要在AEM中達成此目的，請使用來源編輯模式直接新增標籤。

  >[!NOTE]
  >
  >在標準安裝中，此功能無法立即使用。 它需要設定RTE、HTML規則和序列化程式。

#### 更多資訊 — 資訊和關係(1.3.1) {#more-information-info-and-relationships}

* [瞭解成功標準1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [如何達到成功標準1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### 有意義的順序(1.3.2)  {#meaningful-sequence}

* 成功標準1.3.2
* A級
* 有意義的順序：當內容的顯示順序會影響內容含義時，能以程式設計方式決定正確的閱讀順序。

#### 用途 — 有意義的順序(1.3.2) {#purpose-meaningful-sequence}

此成功標準旨在讓使用者代理能提供內容的替代簡報，同時保留理解內容含義所需的閱讀順序。 請務必儘可能以程式設計方式決定至少一個有意義的內容順序。 當輔助技術以錯誤的順序讀取內容，或在套用替代樣式表或其他格式變更時，不符合此成功標準的內容可能會讓使用者感到困惑或是不知所措。

#### 如何達到標準 — 有意義的順序(1.3.2) {#how-to-meet-meaningful-sequence}

請遵循以下准則： [如何達到成功標準1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### 更多資訊 — 有意義的順序(1.3.2) {#more-information-meaningful-sequence}

* [瞭解成功標準1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [如何達到成功標準1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### 感官特性(1.3.3)  {#sensory-characteristics}

* 成功標準1.3.3
* A級
* 感官特性：提供用於理解和操作內容的指示，不會僅依賴元件的感官特性，例如形狀、大小、視覺位置、方向或聲音。

#### 用途 — 感官特性(1.3.3) {#purpose-sensory-characteristics}

設計者通常專注於視覺設計特徵，例如顏色、形狀、文字樣式，或內容在展示資訊時的絕對或相對位置。 這些可能是傳達資訊的強大設計技術（並且可以改善具有認知協助工具需求的視力正常使用者的整體協助工具），但盲人或視力受損者可能無法存取需要視覺識別屬性（例如位置、顏色或形狀）的資訊。

同樣地，需要區分不同聲音的資訊（例如，男性或女性口語內容），如果音訊內容沒有反映在任何替代文字中，對於聽覺障礙的人來說，會造成協助工具障礙。

>[!NOTE]
>
>如需有關替代色彩的需求，請參閱 [使用顏色](#use-of-color).

#### 如何達到標準 — 感官特性(1.3.3) {#how-to-meet-sensory-characteristics}

請確定任何依賴頁面內容視覺特性的資訊也會以替代格式呈現。

* 不要依賴視覺位置來提供資訊。 例如，如果您想讓使用者參閱頁面右側的功能表以存取進一步資訊，請勿參閱 *右側的功能表*；請改為命名選單（例如，透過標題），並在文字中參照該名稱。
* 請勿依賴文字樣式（例如粗體或斜體文字）作為傳達資訊的唯一方式。

>[!NOTE]
>
>如果在非視覺內容中理解描述性字詞的含義，則可以使用描述性字詞。 例如，使用 *以上* 和 *以下* 通常可以接受，因為它們分別表示特定內容專案之前和之後的內容；當朗讀內容時，這仍然是合理的。

#### 更多資訊 — 感官特性(1.3.3) {#more-information-sensory-characteristics}

* [瞭解成功標準1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [如何達到成功標準1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### 可區分(1.4) {#distinguishable}

[准則1.4可區分：讓使用者更容易檢視和聆聽內容，包括將前景與背景分開。](https://www.w3.org/TR/WCAG/#distinguishable)

### 使用顏色(1.4.1)  {#use-of-color}

* 成功標準1.4.1
* A級
* 使用顏色：顏色並非唯一用於傳達資訊（表示動作、提示回應或區分視覺元素）的視覺方式。

>[!NOTE]
>
>此成功標準特別針對色彩感知。 其他形式的認知包含在 [可調整(1.3)](#adaptable)；包括程式化存取色彩和其他視覺簡報編碼。

#### 用途 — 使用顏色(1.4.1) {#purpose-use-of-color}

色彩是增強網頁審美吸引力的有效方式，在傳達資訊方面也很有用。 然而，視覺障礙有很多種，從失明到色覺缺陷，這表示有些人無法分辨某些顏色。 這使得色彩編碼成為提供資訊的不可靠方式。

例如，有紅 — 綠色覺缺陷的人將無法區分綠色陰影和紅色陰影。 他們可能會將這兩種顏色視為第三種顏色（例如，棕色），在這種情況下，他們無法區分紅色、綠色和棕色。

此外，使用純文字瀏覽器、單色顯示裝置或檢視頁面黑白列印成品的人無法察覺顏色。

進一步考慮因素為 *已選取* 介面元素的狀態（例如索引標籤、切換按鈕等），這些元素必須以顏色和視覺呈現方式以外的其他某種方式傳遞。 對於這類元素，當建立不依賴特定感官的全包容式使用者體驗時，額外使用圖案、形狀和程式化資訊會很有幫助。

#### 如何達到標準 — 使用顏色(1.4.1) {#how-to-meet-use-of-color}

無論在何處使用顏色來傳達資訊，請務必提供資訊，而不需要看到顏色。

例如，請確定色彩提供的資訊也明確地以文字提供。

如果使用顏色作為提供資訊的提示，您應該提供額外的視覺提示，例如變更樣式（例如粗體、斜體）或字型。 這有助於視力缺佳或色覺辨認障礙的人識別資訊。 然而，這並不能完全依賴，因為這對於完全看不到頁面的使用者而言並無助益。 因此，提供隱藏文字或使用程式化解決方案(例如 [可存取的網頁標準多樣化網際網路應用程式(ARIA)套件](https://www.w3.org/WAI/standards-guidelines/aria/)，將此資訊傳達給失明的使用者。

#### 更多資訊 — 使用顏色(1.4.1) {#more-information-use-of-color}

* [瞭解成功標準1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [如何達到成功標準1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### 音訊控制(1.4.2)  {#audio-control}

* 成功標準1.4.2
* A級
* 音訊控制：如果網頁上的任何音訊自動播放超過3秒，則要麼有一種機制可用來暫停或停止音訊，要麼有一種獨立於整體系統音量控制音量的機制。

#### 用途 — 音訊控制(1.4.2) {#purpose-audio-control}

如果同時有其他音訊播放，使用熒幕閱讀軟體的個人可能會難以聽到語音輸出。 如果熒幕助讀程式的語音輸出是軟體式的（現今大多數都是如此），而且是透過與音效相同的音量控制來控制，這種困難就會加劇。 此外，有些認知障礙人士和神經系統障礙人士可能對聲音敏感。 這些人認為無法變更音訊內容的音量會造成干擾。

因此，使用者必須能夠關閉背景聲音。

>[!NOTE]
>
>控制音量包括能夠將音量減少到零。

#### 如何達到標準 — 音訊控制(1.4.2) {#how-to-meet-audio-control}

請遵循以下准則： [如何達到成功標準1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### 更多資訊 — 音訊控制(1.4.2) {#more-information-audio-control}

* [瞭解成功標準1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [如何達到成功標準1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### 對比（最小） (1.4.3) {#contrast-minimum}

* 成功標準1.4.3
* AA級
* 對比度（最小）：文字的視覺呈現和影像的對比度至少為4.5:1，以下除外：
   * 大型文字：大型文字和影像的對比率至少為3:1。
   * 附帶：文字或文字的影像，屬於非使用中使用者介面元件的一部分， [純裝飾](https://www.w3.org/TR/WCAG/#dfn-pure-decoration)，任何人都看不到，或是包含其他重要視覺內容的圖片的一部分，不需要對比度。
   * 圖志型別：屬於圖志或品牌名稱的文字沒有最低對比要求。

  >[!NOTE]
  >
  >另請參閱 [瞭解非文字對比](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) 如需詳細資訊，以協助確保內容作者瞭解非文字元素（包括圖示、介面元素等）的其他需求。

#### 用途 — 對比（最小） (1.4.3) {#purpose-contrast-minimum}

某些視力障礙的人可能無法分辨某些低對比顏色配對。 如果發生下列任一情況，這些人員可能會發生協助工具問題：

* 文字與背景顏色對比較差。
* 文字（例如連結文字和非連結文字）的色彩編碼對於區分資訊很重要。

>[!NOTE]
>
>純粹用於裝飾目的的文字會從此成功標準中排除。

#### 如何達到標準 — 對比（最小） (1.4.3) {#how-to-meet-contrast-minimum}

請確定文字與其背景的對比度已足夠。 對比率視相關文字的大小和樣式而定：

* 對於大小小於18點（或粗體小於14點）的文字，文字的文字/影像與背景之間的對比率應至少為4.5:1。
* 對於大小至少為18點（或粗體為14點）的文字，對比率應至少為3:1。
* 如果陣列化背景，則任何文字周圍的背景都應著色，以維持4.5:1或3:1的比例。

>[!NOTE]
>
>請記住，字型在呈現等同的PT/PX/EM大小的方式上可能有所不同。
>
>為網頁內容選擇適當的字型與大小時，請務必判斷並正確使用可讀性和可用性。

>[!NOTE]
>
>下列網站可協助您轉換至其他單位：
>
>* [Px到Em電腦 — Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* 請參閱「Font size conversion： pixel-point-em-rem-percent」，網址為 `https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/`
>* 請參閱PMtoEM.com：PX到EM的簡單轉換，網址為 `http://pxtoem.com/`

若要檢查對比率，請使用色彩對比工具，例如 [Paciello Group色彩對比分析器](https://www.paciellogroup.com/resources/contrast-analyser.html) 或 [WebAIM色彩對比檢查程式](https://webaim.org/resources/contrastchecker/). 這些工具可讓您檢查顏色配對，並報告任何對比問題。

或者，如果您不太在意頁面外觀的指定，則可以選擇不指定背景和前景文字顏色。 不需要檢查對比，因為使用者的瀏覽器會決定文字和背景的顏色。

如果無法滿足建議的對比等級，請提供替代對等頁面版本的連結（沒有色彩對比問題）。 或者，讓使用者根據自己的需求調整頁面色彩配置的對比。

#### 更多資訊 — 對比（最小） (1.4.3) {#more-information-contrast-minimum}

* [瞭解成功標準1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [如何達到成功標準1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### 調整文字大小(1.4.4)  {#resize-text}

* 成功標準1.4.4
* A級
* 調整文字大小：除了文字的註解和影像之外，在不使用輔助技術的情況下，最多可調整文字大小200%，而不會失去內容或功能。

#### 用途 — 調整文字大小(1.4.4) {#purpose-resize-text}

此成功標準旨在確保視覺呈現的文字，包括文字型控制項（已顯示以便顯示的文字字元） [與仍在資料表單（例如ASCII）中的文字字元比較])可成功縮放，因此具有輕微視覺障礙的人士可直接讀取，而不需要使用熒幕放大鏡等輔助技術。 縮放網頁上的所有內容可能會讓使用者受益，但文字是最關鍵的。

#### 如何達到標準 — 調整文字大小(1.4.4) {#how-to-meet-resize-text}

除了遵循底下的指引 [如何達到成功標準1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) 您可以鼓勵內容作者在其頁面設計和字型大小（例如回應式網頁設計）中使用不固定、彈性的寬度和高度，讓讀者可以調整文字大小。

#### 更多資訊 — 調整文字大小(1.4.4) {#more-information-resize-text}

* [瞭解成功標準1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [如何達到成功標準1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### 文字的影像(1.4.5) {#images-of-text}

* 成功標準1.4.5
* AA級
* 文字的影像：如果使用的技術可以達到視覺呈現效果，文字會用來傳遞資訊，而非文字的影像，但下列專案除外：
   * 可自訂：可視地根據使用者的需求自訂文字影像；
   * 必要：文字的特定呈現方式對於傳達的資訊至關重要。

>[!NOTE]
>
>標誌型別（屬於標誌或品牌名稱一部分的文字）被認為是必要的。

#### 用途 — 文字影像(1.4.5) {#purpose-images-of-text}

當偏好文字的特定樣式時，通常會使用文字的影像；例如，商標標誌或從其他來源產生的文字（例如，紙質檔案的掃描）。 然而，與使用CSS以HTML呈現和樣式化的文字相比，文字影像在變更大小或外觀方面缺乏靈活性，而這對於有視覺障礙或閱讀困難的人可能是必要的。

#### 如何達到標準 — 文字影像(1.4.5) {#how-to-meet-images-of-text}

如果必須使用文字的影像，請使用CSS將文字的影像取代為HTML的對等文字，以便可自訂文字使用。 如需範例，請參閱 [C30：使用CSS將文字取代為文字的影像，並提供使用者介面控制項以進行切換](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### 更多資訊 — 文字影像(1.4.5) {#more-information-images-of-text}

* [瞭解成功標準1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [如何達到成功標準1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## 准則2：可操作 {#principle-operable}

[准則2：可操作 — 使用者介面元件和導覽必須可操作。](https://www.w3.org/TR/WCAG/#operable)

### 無障礙鍵盤(2.1) {#keyboard-accessible}

[Guidelinate 2.1無障礙鍵盤：讓所有功能都可使用鍵盤。](https://www.w3.org/TR/WCAG/#keyboard-accessible)

此准則涉及的是，確保使用者可以使用鍵盤存取所有功能。

### 鍵盤(2.1.1)  {#keyboard}

* 成功標準2.1.1
* A級
* 鍵盤：內容的所有功能都可透過鍵盤介面操作，不需要個別擊鍵的特定時間，除非基礎功能需要取決於使用者移動路徑的輸入，而不僅僅是端點。

#### 用途 — 鍵盤(2.1.1) {#purpose-keyboard}

此成功標準旨在儘可能確保內容可透過鍵盤或鍵盤介面操作（以便使用替代鍵盤）。 如果內容可以透過鍵盤或替代鍵盤操作，則無法視力的人（無法使用需要手眼合作的裝置，例如滑鼠）和必須使用替代鍵盤或充當鍵盤模擬器的輸入裝置的人可以操作。 鍵盤模擬器包括語音輸入軟體、呼吸軟體、熒幕鍵盤、掃描軟體，以及各種輔助技術和備用鍵盤。 視力缺佳的人也可能難以追蹤指標，而且如果能透過鍵盤控制指標，他們會發現使用軟體更容易（或只有可能）。

#### 如何達到標準 — 鍵盤(2.1.1) {#how-to-meet-keyboard}

請遵循以下准則： [如何達到成功標準2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard).

#### 更多資訊 — 鍵盤(2.1.1) {#more-information-keyboard}

* [瞭解成功標準2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何達到成功標準2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### 無鍵盤陷阱(2.1.2)  {#no-keyboard-trap}

* 成功標準2.1.2
* A級
* 無鍵盤陷阱：如果可以使用鍵盤介面將鍵盤焦點移至頁面的元件，則焦點只需使用鍵盤介面即可從該元件移開，如果除了使用未修改的箭頭、Tab鍵或其他標準退出方法外，該移開功能還需使用其他工具，系統會告知使用者將焦點移開的方法。

#### 用途 — 無鍵盤陷阱(2.1.2) {#purpose-no-keyboard-trap}

此成功標準旨在確保內容不會 *補漏白* 網頁內容子區段中的鍵盤焦點。 當一個頁面結合了多種格式並使用外掛程式或內嵌應用程式呈現時，這是一個常見問題。

有時候，網頁的功能會將焦點限制在內容的子區段（例如強制回應對話方塊）。 在這種情況下，您應該提供讓使用者能夠退出該內容子區段的方法（例如，按ESC鍵關閉模組對話方塊，或按「關閉」按鈕關閉模組對話方塊）。

#### 如何達到標準 — 無鍵盤陷阱(2.1.2) {#how-to-meet-no-keyboard-trap}

請遵循以下准則： [如何達到成功標準2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap).

#### 更多資訊 — 無鍵盤陷阱(2.1.2) {#more-information-no-keyboard-trap}

* [瞭解成功標準2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何達到成功標準2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### 充足的時間(2.2) {#enough-time}

[指引2.2充足時間：為使用者提供充足的時間來閱讀及使用內容。](https://www.w3.org/TR/WCAG/#enough-time)

此准則涉及的是，確保使用者有足夠的時間來閱讀內容並採取動作。

### 計時可調(2.2.1)  {#timing-adjustable}

* 成功標準2.2.1
* A級
* 鍵盤：為使用者提供充足的時間來閱讀及使用內容。

#### 用途 — 計時可調(2.2.1) {#purpose-timing-adjustable}

此成功標準旨在確保身心障礙使用者有儘可能充足的時間與網路內容互動。 失明、視力缺佳、行動不便以及認知困難等殘障人士，可能需要更多時間閱讀內容或執行線上表單填寫等功能。 如果Web功能是時間相依的，則某些使用者在時間限制發生之前將很難執行所需的動作。 這可能會導致他們無法存取服務。 設計不限時間的功能可協助殘障人士成功完成這些功能。 提供停用時間限制、自訂時間限制長度或在時間限制發生前要求更多時間的選項，有助於需要超過預期時間的使用者成功完成工作。 這些選項會以最有利於使用者的順序列出。 停用時間限制比自訂時間限制長度好，這比在時間限制發生之前請求更多時間好。

#### 如何達到標準 — 計時可調(2.2.1) {#how-to-meet-timing-adjustable}

請遵循以下准則： [如何達到成功標準2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### 更多資訊 — 計時可調(2.2.1) {#more-information-timing-adjustable}

* [瞭解成功標準2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [如何達到成功標準2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### 暫停、停止、隱藏(2.2.2)  {#pause-stop-hide}

* 成功標準2.2.2
* A級
* 暫停、停止、隱藏：對於移動、閃爍、捲動或自動更新的資訊，符合下列情況：
   * 移動、閃爍、捲動：適用於任何移動、閃爍或捲動資訊，
      * (a)自動啟動，
      * (b)持續超過五秒，而
      * (C)與其他內容同時呈現，使用者有一個機制可暫停、停止或隱藏內容，除非移動、閃爍或捲動屬於必要活動的一部分；
   * 自動更新：適用於任何自動更新資訊，
      * (a)自動啟動，並且
      * (b)與其他內容同時顯示，除非自動更新是重要活動的一部分，否則使用者會有暫停、停止或隱藏內容的機制，或控制更新的頻率。

需要注意的要點包括：

1. 如需與閃爍或閃爍內容相關的需求，請參閱請勿設計會導致癲癇發作的內容(2.3)。
1. 由於任何不符合此成功標準的內容都可能干擾使用者使用整個頁面的能力，網頁上的所有內容（無論是否用於滿足其他成功標準）都必須符合此成功標準。 另請參閱 [一致性需求5：不干擾](https://www.w3.org/TR/WCAG20/#cc5).
1. 軟體定期更新或串流至使用者代理程式的內容，不必保留或呈現暫停起始與繼續簡報之間產生或接收的資訊，因為這在技術上可能行不通，且在許多情況下這麼做可能會產生誤導。
1. 如果在此階段中無法對所有使用者進行互動，而且如果未指出進度，可能會讓使用者感到困惑或導致他們認為內容已凍結或中斷，則作為預先載入階段的一部分或類似情況發生的動畫可視為必要。

#### 用途 — 暫停、停止、隱藏(2.2.2) {#purpose-pause-stop-hide}

某些使用者可能會發現移動的內容會讓人分心，甚至讓人覺得難受，因此難以將注意力集中在頁面的其他部分。 此外，對於無法跟上移動文字進度的人來說，這類內容可能很難閱讀。

#### 如何達到標準 — 暫停、停止、隱藏(2.2.2) {#how-to-meet-pause-stop-hide}

根據內容的性質，您可以在建立包含移動、閃爍或閃爍內容的網頁時，套用下列一或多個建議：

* 提供暫停捲動內容的方法，讓使用者有充足的時間閱讀。 例如，新聞捲軸、自動更新的文字，以及自動推進的影像輪播。
* 請確定閃爍的內容會在5秒後停止閃爍。
* 使用適當的技術來顯示可由瀏覽器停用的移動或閃爍內容。 例如，Graphics Interchange Format (GIF)或Animated Portable Network Graphics (APNG)檔案。
* 在網頁上提供表單控制項，讓使用者可停用頁面上的所有移動或閃爍內容。
* 如果以上建議均不可行，請提供包含所有內容但不含任何移動或閃爍之頁面的連結。

#### 更多資訊 — 暫停、停止、隱藏(2.2.2) {#more-information-pause-stop-hide}

* [瞭解成功標準2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [如何達到成功標準2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### 癲癇發作和生理反應(2.3) {#seizures-and-physcial-reactions}

[指南2.3癲癇發作：請勿設計會導致癲癇發作或生理反應的內容。](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### 三個Flash或低於臨界值(2.3.1) {#three-flashes-or-below-threshold}

* 成功標準2.3.1
* A級
* 三次Flash或低於臨界值：網頁在任何一秒的期間內，都不包含閃光超過三次的任何專案，或是閃光低於一般閃光燈和紅色閃光燈臨界值。

>[!NOTE]
>
>由於任何不符合此成功標準的內容都可能干擾使用者使用整個頁面的能力，因此網頁上的所有內容（無論是否用於符合其他成功標準）都必須符合此成功標準。 另請參閱 [一致性需求5：不干擾](https://www.w3.org/TR/WCAG/#cc5).

#### 用途 — 三個Flash或低於臨界值(2.3.1) {#purpose-three-flashes-or-below-threshold}

在某些情況下，閃爍的內容會導致光敏性癲癇發作。 此成功標準可讓這類使用者存取及體驗所有內容，而不需擔心內容閃爍問題。

#### 如何達到標準 — 三個Flash或低於臨界值(2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

採取步驟以確保套用下列技術：

* 請確定在任何一秒的時間段內，元件的閃爍次數不會超過三次；
* 如果無法滿足上述條件，則會在內顯示閃爍的內容 *小安全區域* 以畫面的畫素為單位。 此區域是使用複雜的公式來計算，詳見 [G176：讓閃爍區域保持足夠小](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)，因此只有在需要*閃爍的內容時，才應使用此技巧。

#### 更多資訊 — 三個Flash或低於臨界值(2.3.1) {#more-information-three-flashes-or-below-threshold}

* [瞭解成功標準2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [如何達到成功標準2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### 可導覽(2.4) {#navigable}

[指引2.4可導覽：提供可協助使用者導覽、尋找內容及判斷其所在位置的方法。](https://www.w3.org/TR/WCAG/#navigable)

此准則涉及的是，確保內容簡單明瞭，讓使用者導覽。

### 略過區塊(2.4.1)  {#bypass-blocks}

* 成功標準2.4.1
* A級
* 略過區塊：提供的機制可略過多個網頁上重複的內容區塊。

#### 用途 — 略過區塊(2.4.1) {#purpose-bypass-blocks}

此成功標準旨在讓依序瀏覽內容的人更直接地存取網頁的主要內容。 網頁和應用程式通常會有出現在其他頁面或熒幕上的內容。 重複出現的內容區塊範例包括但不限於導覽連結、標題圖形、功能表及廣告框架。 就本規範而言，個別字詞、短語或單一連結等小型重複區段不會被視為區塊。

#### 如何達到標準 — 略過區塊(2.4.1) {#how-to-meet-bypass-blocks}

請遵循以下准則： [如何達到成功標準2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### 更多資訊 — 略過區塊(2.4.1) {#more-information-bypass-blocks}

* [瞭解成功標準2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [如何達到成功標準2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### 頁面帶有標題(2.4.2)  {#page-titled}

* 成功標準2.4.2
* A級
* 頁面標題：網頁具有說明主題或目的的標題。

#### 用途 — 頁面帶有標題(2.4.2) {#purpose-page-titled}

此成功標準可協助每個人（無論是否有任何損傷）快速識別網頁內容，而不需完整閱讀頁面。 這在瀏覽器標籤中開啟數個網頁時非常有用，因為頁面標題會顯示在標籤中，因此可以快速找到。

#### 如何達到標準 — 頁面有標題(2.4.2) {#how-to-meet-page-titled}

在AEM中建立新HTML頁面時，您可以指定頁面標題。 請確定標題足以描述頁面內容和用途，尤其是任何不重複方面，讓訪客可快速找出內容是否符合其需求。

編輯頁面時，您也可以編輯頁面標題，頁面資訊——屬 **性可****存取。**

#### 更多資訊 — 頁面帶有標題(2.4.2) {#more-information-page-titled}

* [瞭解成功標準2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [如何達到成功標準2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### 焦點順序(2.4.3)  {#focus-order}

* 成功標準2.4.3
* A級
* 焦點順序：如果網頁可以循序導覽，且導覽順序會影響含義或作業，可聚焦元件會以保留含義和可操作性的順序接收焦點。

#### 用途 — 焦點順序(2.4.3) {#purpose-focus-order}

此成功標準旨在確保使用者依序導覽內容時，會依與內容含義一致的順序遇到資訊，而且可使用鍵盤操作。 這可讓使用者形成內容的一致心智模型，以減少混淆。 可反映內容中邏輯關係的順序可能不同。 例如，在由多個欄位和/或步驟組成的線上表單中移動元件會反映內容中的邏輯關係。

#### 如何達到標準 — 焦點順序(2.4.3) {#how-to-meet-focus-order}

請遵循以下准則： [如何達到成功標準2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### 更多資訊 — 焦點順序(2.4.3) {#more-information-focus-order}

* [瞭解成功標準2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [如何達到成功標準2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### 連結目的（在內容中） (2.4.4)  {#link-purpose-in-context}

* 成功標準2.4.4
* A級
* 連結目的（在內容中）：每個連結的目的都可以單獨從連結文字中決定，或是從連結文字及其程式化決定的連結內容中決定，除非連結目的通常對使用者來說模稜兩可。

#### 用途 — 連結用途（在內容中） (2.4.4) {#purpose-link-purpose-in-context}

不論使用狀況為何，透過適當的連結文字清楚指出連結的方向至關重要。 這可協助使用者決定他們是否實際想要追蹤連結。 對於視力正常的使用者，當頁面上有多個連結時（尤其是頁面含有大量文字時），有意義的連結文字會很有用，因為有意義的連結文字可更清楚指出目標頁面的功能。 使用某些輔助技術的使用者可以在單一頁面上產生所有連結的清單，如果該連結文字是唯一的且資訊豐富，使用者就可以更輕鬆地脫離上下文理解連結文字。 然而，如果連結無法提供足夠資訊來準確描述連結前往何處，則患有認知障礙的視力正常人士可能會感到困惑。

#### 如何達到標準 — 連結目的（在內容中） (2.4.4) {#how-to-meet-link-purpose-in-context}

首先，請確定連結的文字中已清楚說明連結的用途。

* 錯誤範例：
   * 文字：如需2010年秋季晚間課程的詳細資訊，請按一下這裡。
   * 原因：它沒有清楚且明確地指出其目的地。
* 好範例：
   * 文字：2010年秋季晚間課程 — 詳細資料。
   * 原因：只要稍微調整文字和連結元素的位置，就能改善連結文字：

連結的用語在各個頁面中應保持一致，尤其是導覽列。 例如，如果特定頁面的連結已命名為 **出版物** 請在一個頁面上使用其他頁面上的文字，以確保一致性。

在撰寫時，在使用標題屬性以確保頁面上呈現的類似連結提供有關目的地的唯一資訊方面還存在一些問題（例如，「閱讀更多」通常是指一系列的不同目的地）：

* 標題屬性中包含的文字僅供滑鼠使用者作為工具提示快顯視窗使用，而無法透過鍵盤或行動使用者一致地存取。
* 熒幕助讀程式可以讀取標題屬性，但預設可能不會啟用此功能；因此使用者可能不知道存在標題屬性。
* 變更標題文字的外觀很困難，這表示有些人可能難以或無法閱讀。

因此，雖然title屬性可用於為連結提供額外內容，請注意其限制，且請勿將其用作適當連結文字的替代方案。

如果連結是由影像所組成，請確定影像的替代文字描述了連結的目的地。 例如，如果書架影像設定為個人出版物的連結，則替代文字應該寫成 **約翰·史密斯的出版物** 而非 **書架**.

或者，如果連結錨點包含描述連結用途以及影像元素的文字（因此文字會出現在影像旁），請為影像使用空的alt屬性：

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith's publications
</a>
```

>[!NOTE]
>
>以上程式碼片段僅供說明之用，建議您使用 **影像** 元件。

雖然建議您直接提供連結文字來識別連結目的，而不需要其他內容，但您不一定要承認這一點。 與內容無關的連結可用於下列情況，其HTML範例可在下列位置找到： [如何達到成功標準2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* 連結文字是緊密相關連結清單的一部分，當連結周圍的清單專案提供了足夠的內容時。
* 連結的用途可由 *之前* （非下列）段落文字。
* 連結包含在資料表中，因此可從相關標題中清楚識別用途。
* 連結清單包含在一組標題中，標題本身會提供適當的上下文。
* 連結清單包含在巢狀連結中，且巢狀連結上方的父清單專案會提供適當的內容。

有時候，當一個頁面上有數個連結（每個連結都會提供複雜但必要的詳細資訊中的連結方向）時，最好提供其他版本的網頁，此網頁會顯示完全相同的內容，但連結文字的詳細資訊並不多。

或者，使用指令碼，讓連結本身提供的文字量最小。 在啟動位於頁面頂端的適當控制項時，連結文字會 *已展開* 以取得更詳細的資料。 類似的方法是使用CSS來 *隱藏* 視力正常的使用者提供的完整連結，但還是會以全熒幕方式輸出給熒幕助讀程式使用者。 這不屬於本檔案的範圍，但如需如何達成此目標的詳細資訊，請參閱 [更多資訊 — 連結目的（在內容中） (2.4.4)](#more-information-link-purpose-in-context) 區段。

#### 更多資訊 — 連結目的（在內容中） (2.4.4) {#more-information-link-purpose-in-context}

* [瞭解成功標準2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [如何達到成功標準2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### 多種方式(2.4.5)  {#multiple-ways}

* 成功標準2.4.5
* AA級
* 多種方式：除了當網頁是程式的結果或步驟外，還有其他方法可用於在一組網頁中找出網頁。

#### 用途 — 多種方式(2.4.5) {#purpose-multiple-ways}

此成功標準旨在讓使用者能夠以最符合其需求的方式找到內容。 使用者可能會發現一種技術比另一種技術更易於使用或理解。

即使是小型網站，也應為使用者提供一些方向方法。 如果是三或四頁的網站，且所有頁面都是從首頁連結，只提供首頁的連結（首頁上的連結也可做為網站地圖）就足夠了。

#### 如何達到標準 — 多種方式(2.4.5) {#how-to-meet-multiple-ways}

請遵循以下准則： [如何達到成功標準2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways).

#### 更多資訊 — 多種方式(2.4.5) {#more-information-multiple-ways}

* [瞭解成功標準2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [如何達到成功標準2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### 標題和標籤(2.4.6)  {#headings-and-labels}

* 成功標準2.4.6
* AA級
* 標題和標籤：標題和標籤會說明主題或用途。

#### 用途 — 標題和標籤(2.4.6) {#purpose-headings-and-labels}

此成功標準旨在協助使用者瞭解網頁中包含哪些資訊，以及這些資訊的組織方式。 當標題清晰且具有描述性時，使用者可以更輕鬆地找到他們尋找的資訊，並且可以更輕鬆地瞭解內容不同部分之間的關係。 描述性標籤可協助使用者識別內容中的特定元件。

#### 如何達到標準 — 標題和標籤(2.4.6) {#how-to-meet-headings-and-labels}

請遵循以下准則： [如何達到成功標準2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels).

#### 更多資訊 — 標題和標籤(2.4.6) {#more-information-headings-and-labels}

* [瞭解成功標準2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [如何達到成功標準2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### 焦點可見(2.4.7)  {#focus-visible}

* 成功標準2.4.7
* AA級
* 焦點可見：任何鍵盤可操作的使用者介面都有可看到鍵盤焦點指示器的操作模式。

#### 用途 — 焦點可見(2.4.7) {#purpose-focus-visible}

此成功標準旨在協助使用者瞭解鍵盤焦點在哪個元素。

使用者必須可能知道在多個元素中，哪一個元素具有鍵盤焦點。 如果熒幕上只有一個鍵盤可操作控制項，則會符合成功標準，因為視覺設計只會呈現一個鍵盤可操作專案。

成功標準中說的「作業模式」，則是考慮平台可能無法始終顯示焦點指標的問題。 通常只有一種作業模式，因此此成功標準適用。

#### 如何達到標準 — 焦點可見(2.4.7) {#how-to-meet-focus-visible}

請遵循以下准則： [如何達到成功標準2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### 更多資訊 — 焦點可見(2.4.7) {#more-information-focus-visible}

* [瞭解成功標準2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [如何達到成功標準2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## 准則3：可理解 {#principle-understandable}

[准則3：可理解 — 使用者介面的資訊和操作必須是可理解的。](https://www.w3.org/TR/WCAG/#understandable)

### 讓文字內容可讀取及理解(3.1) {#make-text-content-readable-and-understandable}

[准則3.1可讀取：讓文字內容可讀取且可理解。](https://www.w3.org/TR/WCAG/#readable)

### 頁面語言(3.1.1) {#language-of-page}

* 成功標準3.1.1
* A級
* 頁面語言：每個網頁的預設人類語言均可由程式決定。

#### 用途 — 頁面語言(3.1.1) {#purpose-language-of-page}

此成功標準旨在確保文字和其他語言內容正確呈現。 對於熒幕助讀程式使用者，這可確保內容正確發音，而視覺瀏覽器則更有可能正確顯示特定字元集。

#### 如何達到標準 — 頁面語言(3.1.1) {#how-to-meet-language-of-page}

為達到此成功標準，可使用以下識別網頁的預設語言 `lang` 中的屬性 `<html>` 頁面頂端的元素。 例如：

* 如果頁面以英文撰寫，則 `<html>` 元素應為：
  `<html lang = "en">`

* 而要以西班牙文轉譯的頁面應採用下列標準：
  `<html lang = "es">`

在AEM中，您的頁面預設語言是在建立頁面時設定，但在編輯時也可以變更 [頁面屬性](/help/sites-authoring/editing-page-properties.md).

>[!NOTE]
>
>AEM針對根語言的變體提供進一步的微調，例如，美式英文 — en-us、英式英文 — en-gb和加拿大英文 — en-ca。 這種詳細程度對輔助型技術來說通常是多餘的，不過可用於頁面內容中的區域變化。

#### 更多資訊 — 頁面語言(3.1.1) {#more-information-language-of-page}

* [瞭解成功標準3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [如何達到成功標準3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* 這些程式碼以ISO 639-1為基礎。 如需每種語言的程式碼清單，請參閱 [W3學校網站](https://www.w3schools.com/tags/ref_language_codes.asp).

### 區域性語言(3.1.2)  {#language-of-parts}

* 成功標準3.1.2
* AA級
* 部分語言：內容中每個段落或片語的人類語言能以程式設計方式決定。 唯一例外的是正確的名稱、技術術語、不定語言的單詞，以及已變成緊鄰文字的白語中的單詞或短語。

#### 用途 — 區域性語言(3.1.2) {#purpose-language-of-parts}

此成功標準的用途與成功標準類似 [頁面語言](#language-of-page)，但適用於單一頁面上包含多種語言內容的網頁（例如，由於引號或不常見的借出文字）。

套用此成功標準的頁面允許：

* 使用盲文轉換軟體插入重音字元。
* 熒幕助讀程式，可朗讀那些具有特殊字元或未使用在頁面層級識別的預設語言的單字。
* 翻譯工具(例如Google Translate)可正確將內容從一種語言翻譯成另一種語言。

#### 如何達到標準 — 零件語言(3.1.2) {#how-to-meet-language-of-parts}

此 `lang` attribute可用來識別內容語言的變更。 例如，德文引號（ISO 639-1程式碼「de」）可顯示如下：

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>現成可用的執行個體不支援區塊引號。 可開發自訂元件以支援此功能。

同樣地，如果 `span` 元素的使用方式如下：

```xml
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>納入不同語言的人名或城市時，不必遵循此成功標準。 或者，使用預設語言中常見的借出字詞或短語時，例如 *幸災樂禍* 英文版。

若要使用適當的語言新增span元素，您可以在RTE的來源編輯模式中手動編輯HTML標示，使其顯示如上。 或者 `lang` 屬性可由系統管理員包含在RTE中(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

#### 更多資訊 — 區域性語言(3.1.2) {#more-information-language-of-parts}

* [瞭解成功標準3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [如何達到成功標準3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### 可預測(3.2) {#predictable}

[指引3.2可預測：讓網頁以可預見的方式顯示和運作。](https://www.w3.org/TR/WCAG/#predictable)

此准則涉及的是，確保網頁的外觀和運作方式一致。

### 聚焦(3.2.1)  {#on-focus}

* 成功標準3.2.1
* A級
* 聚焦：當任何使用者介面元件收到焦點時，它不會起始內容的變更。

#### 用途 — 聚焦(3.2.1) {#purpose-on-focus}

此成功標準旨在確保訪客在檔案中導覽時，功能是可預測的。 任何能夠在收到焦點時觸發事件的元件，均不得變更內容。 元件收到焦點時變更上下文的範例包括但不限於：

* 元件收到焦點時自動提交表單；
* 元件收到焦點時會啟動新視窗；
* 當元件收到焦點時，焦點會變更為另一個元件；

焦點可以透過鍵盤（例如，以Tab鍵移至控制項）或滑鼠（例如，按一下文字欄位）移至控制項。 將滑鼠移到控制項上不會移動焦點，除非指令碼會實作此行為。 對於某些型別的控制項，按一下控制項也可能會啟動控制項（例如按鈕），這反過來又會啟動前後關聯中的變更。

#### 如何達到標準 — 焦點(3.2.1) {#how-to-meet-on-focus}

請遵循以下准則： [如何達到成功標準3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus).

#### 更多資訊 — 聚焦(3.2.1) {#more-information-on-focus}

* [瞭解成功標準3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [如何達到成功標準3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### 輸入(3.2.2)  {#on-input}

* 成功標準3.2.2
* A級
* 輸入：變更任何使用者介面元件的設定不會自動導致內容變更，除非使用者在使用元件之前已被告知該行為。

#### 用途 — 輸入(3.2.2) {#purpose-on-input}

此成功標準旨在確保輸入資料或選取表單控制項具有可預見的效果。 變更任何使用者介面元件的設定將會變更控制項中某些持續存在的方面（當使用者不再與控制項互動時）。 因此，核取核取方塊、在文字欄位中輸入文字，或變更清單控制項中的選取選項會變更其設定，但啟用連結或按鈕則不會變更。 前後關聯的變更可能會讓不容易察覺變更或容易被變更分散注意力的使用者感到困惑。 只有當明確指出這類變更是因應使用者的動作而發生時，才適合變更內容。

#### 如何達到標準 — 輸入(3.2.2) {#how-to-meet-on-input}

請遵循以下准則： [如何達到成功標準3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input).

#### 更多資訊 — 輸入(3.2.2) {#more-information-on-input}

* [瞭解成功標準3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [如何達到成功標準3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### 一致的導覽(3.2.3)  {#consistent-navigation}

* 成功標準3.2.3
* AA級
* 一致的導覽：在一組網頁內的多個網頁上重複執行的導覽機制，每次都以相同的相對順序發生，除非使用者已起始變更。

#### 用途 — 一致的導覽(3.2.3) {#purpose-consistent-navigation}

此成功標準旨在鼓勵使用一致的呈現和版面配置，讓使用者與一組網頁內的重複內容互動，且必須找到特定資訊或功能超過一次。 視力缺佳的使用熒幕放大功能一次顯示一小部分熒幕的個人，通常會使用視覺提示和頁面邊界來快速找到重複的內容。 對於使用空間記憶體或設計中的視覺提示來尋找重複內容的視覺使用者，以相同順序呈現重複內容也很重要。

本節中使用「相同順序」這個片語，並非表示無法使用子導覽功能表，或無法使用次要導覽區塊或頁面結構。 反之，此成功標準旨在協助與網頁上重複內容互動的使用者，以便預測其所尋找內容的位置。 而且，當他們再次遇到時，可以更快速地找到它。

使用者可使用最適化使用者代理程式或設定偏好設定，以對他們最有用的方式呈現資訊，藉此啟動順序變更。

#### 如何達到標準 — 一致的導覽(3.2.3) {#how-to-meet-consistent-navigation}

請遵循以下准則： [如何達到成功標準3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation).

#### 更多資訊 — 一致的導覽(3.2.3) {#more-information-consistent-navigation}

* [瞭解成功標準3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [如何達到成功標準3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### 一致的識別(3.2.4)  {#consistent-identification}

* 成功標準3.2.4
* A級
* 一致的識別：一組網頁內具有相同功能的元件，都會以一致的方式識別。

#### 用途 — 一致的識別(3.2.4) {#purpose-consistent-identification}

此成功標準旨在確保一組網頁內重複出現的功能元件能有一致的識別。 使用熒幕助讀程式的人員在操作網站時，所使用的策略是依賴他們對可能出現在不同網頁上的功能的熟悉度。 如果相同的功能在不同網頁上具有不同的標籤（或更一般而言，具有不同的存取名稱），則網站的使用難度會大幅增加。 這也可能會令人困惑，並增加認知困難人士的認知負擔。 因此，一致的標籤會有所幫助。

此一致性要求的適用範圍也包括替代文字。 如果圖示或其他非文字專案具有相同的功能，則其替代文字也應保持一致。

如果某個網頁上有兩個元件的功能與一組網頁內另一個頁面上的元件功能相同，則所有這3個元件都必須保持一致。 因此，相同頁面上的兩個專案將保持一致。

雖然在單一網頁內總是保持一致是理想的最佳做法，但3.2.4僅解決一組網頁內的一致性問題（該組網頁內的多個頁面上會重複某些內容）。

#### 如何達到標準 — 一致的身分識別(3.2.4) {#how-to-meet-consistent-identification}

請遵循以下准則： [如何達到成功標準3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification).

#### 更多資訊 — 一致的識別(3.2.4) {#more-information-consistent-identification}

* [瞭解成功標準3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [如何達到成功標準3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### 輸入協助(3.3) {#input-assistance}

[准則3.3輸入協助：協助使用者避免和更正錯誤。](https://www.w3.org/TR/WCAG/#input-assistance)

### 錯誤識別(3.3.1)  {#error-identification}

* 成功標準3.3.1
* A級
* 錯誤識別：如果自動偵測到輸入錯誤，則會識別發生錯誤的專案，並以文字向使用者說明錯誤。

#### 用途 — 錯誤識別(3.3.1) {#purpose-error-identification}

此成功標準旨在確保使用者知道已發生錯誤，並可判斷錯誤內容。 錯誤訊息應儘可能具體。 如果表單提交失敗，則重新顯示表單並指示錯誤欄位不足以讓某些使用者感知已發生錯誤。 例如，熒幕助讀程式的使用者在遇到其中一個指標之前，不會知道有錯誤發生。 他們可能會在遇到錯誤指標之前完全放棄表單，認為頁面根本無法運作。 根據WCAG中的定義， [輸入錯誤](https://www.w3.org/TR/WCAG/#dfn-input-error) 是使用者提供的資訊，但不被接受。 這包含下列專案。

網頁需要但使用者忽略的資訊，或使用者提供但超出所需資料格式或允許值的資訊。
例如：

* 使用者無法在州、省或地區欄位中輸入適當的縮寫；
* 使用者輸入的州縮寫不是有效的州；
* 使用者輸入的郵遞區號不存在；
* 使用者輸入未來2年的出生日期；
* 使用者在只接受數字的電話號碼欄位中輸入字母字元或括弧；
* 使用者輸入的競標低於上一個競標或最低競標增幅。

#### 如何達到標準 — 錯誤識別(3.3.1) {#how-to-meet-error-identification}

請遵循以下准則： [如何達到成功標準3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### 更多資訊 — 錯誤識別(3.3.1) {#more-information-error-identification}

* [瞭解成功標準3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [如何達到成功標準3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### 標籤或指示(3.3.2) {#labels-or-instructions}

* 成功標準3.3.2
* A級
* 標籤或指示：內容需要使用者輸入時，會提供標籤或指示。

#### 用途 — 標籤或指示(3.3.2) {#purpose-labels-or-instructions}

提供指示以幫助人們完成表單是介面可用性良好實務的基本部分。 這麼做有助於視障或認知障礙人士瞭解表單的版面以及在特定表單欄位中要提供的資料類別，否則他們可能會有困難。

##### 表單

在AEM WKND示範專案中，當您新增表單元件(例如 **文字欄位**，移至頁面。 此預設標題取決於元件型別。 您可在下列欄位新增自己的標題： **標題與文字** 該欄位之「編輯」對話方塊的「 」索引標籤。 請務必確保標籤可協助使用者瞭解與每個表單元件相關聯的資料。

這個 **標題** 欄位必須用於欄位元素，因為它提供了可用於輔助技術的標籤。 僅在該欄位旁的文字中寫入標籤是不夠的。

對於某些表單元件，您也可以使用 **隱藏標題** 核取方塊。 以此方式隱藏的標籤仍適用於輔助技術，但無法顯示在螢幕上。雖然這在某些情況下是個好方法，但最好儘可能加入視覺標籤，因為有些使用者可能會看到畫面的一小部分（一次看一個欄位），並需要標籤才能正確識別欄位。

###### 影像按鈕 {#image-buttons}

其中使用影像按鈕(例如 **影像按鈕** 元件)、 **標題** 中的欄位 **標題與文字** 「編輯」對話方塊的標籤實際上會提供影像的替代文字，而非標籤。 因此，在以下範例中，包含文字的影像 `Submit` 的alt文字為 `Submit`，使用編輯對話方塊中的 **Title** 欄位新增。

###### 表單欄位群組 {#groups-of-form-fields}

在WKND專案中，有一組相關控制項，例如 **選項按鈕群組**，群組和個別控制項可能需要標題。 在AEM中新增一組選項按鈕時，「標題 **」欄位會提供此群組標題，而個別標題會指定為選項按鈕(** Items ****)。

不過，群組標題和選項按鈕本身之間沒有程式化關聯。範本編輯器必須將標題包住必要 `fieldset` 和 `legend` 標籤來建立此關聯，而這只能透過編輯頁面原始碼來完成。 或者，系統管理員可以新增對這些元素的支援，使這些元素顯示在 **欄位屬性** 對話方塊(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

###### Forms的其他注意事項 {#additional-considerations-for-forms}

如果要以特定格式輸入資料，請在標籤文字中清楚說明。 例如，如果日期必須輸入在 `DD-MM-YYYY` 格式，請在標籤中特別指明這一點。 這表示當熒幕助讀程式的使用者遇到該欄位時，會自動公告標籤，以及關於格式的其他資訊。

如果表單欄位的輸入是必填的，請使用標籤中的必要字詞來清楚說明。AEM在需要欄位時新增星號，但最好將字詞加入標 `required`簽本身(在編輯對話方塊的「 **Title** 」欄位中)。

標籤的位置也很重要，因為它有助於他們找到適當的欄位。 當使用者面對複雜表單時，這尤其重要。 遵循以下慣例：

* 核取方塊或選項按鈕：標籤會放置在緊鄰欄位右側的位置。
* 所有其他表單元件（例如文字方塊、下拉式方塊）：標籤會放置在欄位上方或左側。

在功能有限的簡單表單中，適當地標示 `Submit` 按鈕可作為相鄰欄位的標籤(例如， `Search`)。 當尋找標籤文字的空間可能困難時，這個用法很有用。

#### 更多資訊 — 標籤或指示(3.3.2) {#more-information-labels-or-instructions}

* [瞭解成功標準3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [如何達到成功標準3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### 錯誤建議(3.3.3)  {#error-suggestion}

* 成功標準3.3.3
* AA級
* 鍵盤：如果自動偵測到輸入錯誤且知道有關更正的建議，則會向使用者提供建議，除非這會危及內容的安全性或用途。

#### 用途 — 錯誤建議(3.3.3) {#purpose-error-suggestion}

此成功標準旨在儘可能確保使用者收到更正輸入錯誤的適當建議。 WCAG定義 [輸入錯誤](https://www.w3.org/TR/WCAG/#dfn-input-error) 表示這是「系統不接受的使用者提供的資訊」。 部分不被接受的資訊範例包括使用者需要但省略的資訊，以及使用者提供但超出所需資料格式或允許值的資訊。

成功標準3.3.1會提供錯誤通知。 然而，認知困難的人士可能很難理解如何更正錯誤。 視障人士可能無法明白到底該如何更正錯誤。 如果表單提交失敗，使用者可能會放棄表單，因為他們可能不確定如何更正錯誤，即使他們知道已經發生錯誤。

內容作者可以提供錯誤說明，或者使用者代理可以根據技術專屬、以程式設計方式決定的資訊提供錯誤說明。

#### 如何達到標準 — 錯誤建議(3.3.3) {#how-to-meet-error-suggestion}

請遵循以下准則： [如何達到成功標準3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion).

#### 更多資訊 — 錯誤建議(3.3.3) {#more-information-error-suggestion}

* [瞭解成功標準3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [如何達到成功標準3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### 錯誤預防（法律、金融、資料） (3.3.4)  {#error-prevention-legal-financial-data}

* 成功標準3.3.4
* AA級
* 錯誤預防（法律、財務、資料）：對於造成使用者發生法律承諾或財務交易的網頁、在資料儲存系統中修改或刪除使用者可控資料的網頁，或提交使用者測試回應的網頁，以下至少一項為真：

   * 可還原的提交內容。
   * 已檢查檢查使用者輸入的資料是否有輸入錯誤，並為使用者提供更正錯誤的機會。
   * 已確認提供一種機制，可在完成提交前複查、確認及更正資訊。

#### 用途 — 錯誤預防（法律、金融、資料） (3.3.4) {#purpose-error-prevention-legal-financial-data}

此成功標準旨在協助身心障礙使用者在執行無法回覆的動作時，避免因錯誤而導致嚴重後果。 例如，購買不可退款的機票，或提交訂單在經紀帳戶中購買股票，都是可能產生嚴重後果的金融交易。 如果使用者在航空旅行日期上出錯，他們最終可能會拿到一張無法交換的錯誤日期的機票。 如果使用者在要購買的股票數量上發生錯誤，他們最終可能會購買超出預期數量的股票。 這兩種代價高昂的錯誤都會涉及立即發生且事後無法變更的交易。 同樣地，如果使用者無意中修改或刪除了儲存在資料庫中但日後必須存取的資料（例如旅行服務網站中自己的整個旅行檔案），也可能是無法復原的錯誤。 當提及修改或刪除「使用者可控」資料時，目的是防止大量資料遺失，例如刪除檔案或記錄。 並非要求每個儲存命令都需確認，也不是要簡單建立或編輯檔案、記錄或其他資料。

身心障礙使用者可能更容易犯錯。 患有閱讀障礙的人可能會顛倒數字和字母，而患有運動障礙的人則可能會意外按錯按鍵。 提供還原動作的功能，讓使用者更正可能導致嚴重後果的錯誤。 提供檢閱和更正資訊的功能，讓使用者在採取造成嚴重後果的行動之前，有機會偵測錯誤。

使用者可控制的資料是指使用者可檢視的資料，使用者可透過有意的動作變更和/或刪除這些資料。 使用者控制此類資料的範例是更新使用者帳戶的電話號碼和地址，或從網站刪除過去發票的記錄。 它不是指使用者無法直接檢視或互動的網際網路記錄和搜尋引擎監控資料。

#### 如何達到標準 — 錯誤預防（法律、金融、資料） (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

請遵循以下准則： [如何達到成功標準3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### 更多資訊 — 錯誤預防（法律、金融、資料） (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [瞭解成功標準3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [如何達到成功標準3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## 原則4：強健 {#principle-robust}

[原則4：強健 — 內容必須足夠強健，以供包括輔助技術在內的各種使用者代理程式解讀。](https://www.w3.org/TR/WCAG/#robust)

### 相容(4.1) {#compatible}

[准則4.1相容：儘可能與目前和未來的使用者代理程式（包括輔助技術）相容。](https://www.w3.org/TR/WCAG/#compatible)

儘可能與目前和未來的使用者代理程式相容，包括輔助技術。

### 剖析(4.1.1)  {#parsing}

* 成功標準4.1.1
* A級
* 剖析：在使用標籤語言實作的內容中，元素具有完整的開始和結束標籤，元素根據其規格進行巢狀，元素不包含重複屬性，並且任何ID都是唯一的，除非規格允許這些功能。

#### 用途 — 剖析(4.1.1) {#purpose-parsing}

此成功標準旨在確保使用者代理（包括輔助技術）可準確解讀和分析內容。 如果內容無法剖析為資料結構，則不同的使用者代理程式可能會以不同的方式呈現內容，或無法剖析內容。 有些使用者代理會使用「修復技術」來轉譯編碼缺佳的內容。

由於修復技術因使用者代理而異，因此作者無法假設內容已正確剖析為資料結構，或內容將由專業使用者代理（包括輔助技術）正確呈現，除非內容是根據該技術的正式文法中定義的規則所建立。 在標籤語言中，元素和屬性語法中的錯誤，以及無法提供正確巢狀的開頭/結束標籤，會導致使用者代理程式無法可靠地剖析內容的錯誤。 因此，成功標準要求只能使用正式文法的規則來剖析內容。

#### 如何達到標準 — 剖析(4.1.1) {#how-to-meet-parsing}

請遵循以下准則： [如何達到成功標準4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### 更多資訊 — 剖析(4.1.1) {#more-information-parsing}

* [瞭解成功標準4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [如何達到成功標準4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### 名稱、角色、值(4.1.2)  {#name-role-value}

* 成功標準4.1.2
* A級
* 名稱、角色、值：對於所有使用者介面元件（包含但不限於：表單元素、連結和指令碼產生的元件），名稱和角色能以程式設計方式決定；使用者可設定的狀態、屬性和值能以程式設計方式設定；使用者代理程式可收到這些專案的變更通知，包括輔助技術。

#### 用途 — 名稱、角色、值(4.1.2) {#purpose-ame-role-value}

此成功標準旨在確保輔助技術(AT)可以收集關於內容中使用者介面控制項狀態的資訊，加以啟用（或設定）並保持在最新狀態。

若使用來自無障礙技術的標準控制項，此過程相當簡單明瞭。 如果根據規格使用使用者介面元素，則符合此提供的條件。 （請參閱底下的成功標準4.1.2範例）

但是，如果建立了自訂控制項，或介面元素被程式設計（使用程式碼或指令碼）為具有不同於平常的角色和/或功能，則必須採取其他措施以確保控制項為輔助技術提供重要資訊，並允許輔助技術控制這些資訊。

使用者介面控制項的重要狀態是其是否具有焦點。 控制項的焦點狀態能以程式設計方式決定，且會傳送有關焦點變更的通知給使用者代理程式和輔助技術。 使用者介面控制項狀態的其他範例包括是否已選取核取方塊或選項按鈕。 或是展開或收合可收合的樹狀結構或清單節點。

#### 如何達到標準 — 名稱、角色、值(4.1.2) {#how-to-meet-ame-role-value}

請遵循以下准則： [如何達到成功標準4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### 更多資訊 — 名稱、角色、值(4.1.2) {#more-information-ame-role-value}

* [瞭解成功標準4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [如何達到成功標準4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
