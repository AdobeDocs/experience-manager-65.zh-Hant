---
title: 建立適用於Adobe Experience Manager的可存取內容（WCAG 2.1符合性）
description: 使用AEM協助讓殘障人士存取和使用網頁內容
translation-type: tm+mt
source-git-commit: cb7df7301364eb1ce3a1ca376256d2cd5afcb2c8
workflow-type: tm+mt
source-wordcount: '13956'
ht-degree: 4%

---


# Creating Accessible Content (WCAG 2.1 Conformance) {#creating-accessible-content-wcag-conformance}

World Wide Wec Consortium [(World Wide Wec Consortium](https://www.w3.org/TR/WCAG/))的一個工作組起草的《Web內容無障礙環境准則》(WCAG)2.1 [](https://www.w3.org/Consortium/activity#Accessibility_Guidelines_Working_Group)，由一套技術獨立的准則和成功標準組成，以幫助殘疾人能夠訪問和使用Web內容。

作為介紹，該聯合組織提供了一系列章節和支援檔案：

* [WCAG 2.1的新功能](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [How to Meet WCAG 2.1 (如何達成 WCAG 2.1) ](https://www.w3.org/WAI/WCAG21/quickref/)
* [Understanding WCAG 2.1 (瞭解 WCAG 2.1) ](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Techniques for WCAG 2.1 (WCAG 2.1 的專用技術) ](https://www.w3.org/WAI/WCAG21/Techniques/)
* [WCAG檔案](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

此外，請參閱：
* Our [Quick Guide to WCAG 2.1](/help/managing/qg-wcag.md).
* Adobe解決 [方案的「協助工具符合性」報表](https://www.adobe.com/accessibility/compliance.html)。
* [設定Rich Text Editor，以產生可存取的內容](/help/sites-administering/rte-accessible-content.md)

該准則按三個一致性級別分級： A級（最低）、AA級和AAA級（最高）。 簡單地說，這些級別的定義如下：

* **** A級：您的網站達到基本的最低協助功能等級。要達到此級別，將滿足所有A級成功標準。
* **AA級：** 這是您致力追求的最佳無障礙環境支援，其中您的網站達到基本無障礙環境支援的程度，因此在大多數情況下，大多數人都可使用大部分技術。 要達到此級別，將滿足所有A級和A級成功標準。
* **** AAA級：您的網站可達到非常高的協助功能。要達到此級別，將滿足所有A級、AA級和AAA級成功標準。

建立網站時，您必須決定要讓網站遵循的整體等級。

以下部分介 [紹了WCAG 2.1准則的各層](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) ，以及A級和A級符合性級別的相關 [成功標準](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1)。

>[!NOTE]
>
>在本檔案中，我們使用：
>
>* 《 [WCAG 2.1准則》的簡稱](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance)。
>* WCAG 2. [1准則中用於協助與WCAG網站交互參照的編號](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) 。


## 原則1: 可感知 {#principle-perceivable}

[原則1: 可感知——資訊和使用者介面元件必須以使用者可感知的方式呈現給使用者。](https://www.w3.org/TR/WCAG/#perceivable)

### 替代文字(1.1) {#text-alternatives}

[准則1.1備選案文： 為任何非文字內容提供替代文字，以便將其變更為人們需要的其他形式，例如大型印刷、盲文、語音、符號或更簡單的語言。](https://www.w3.org/TR/WCAG/#text-alternatives)

### 非文字內容(1.1.1) {#non-text-content}

* 成功標準1.1.1
* A級
* 非文字內容： 除下列情況外，提供給使用者的所有非文字內容都有提供同等目的的文字替代項目。

#### 用途——非文字內容(1.1.1) {#purpose-non-text-content}

網頁上的資訊可以提供許多不同的非文字格式，例如圖片、視訊、動畫、圖表和圖形。 盲人或視力嚴重受損的人無法看到非文本內容，但他們可以通過螢幕閱讀器讀取文本內容或通過盲文顯示設備以觸覺形式顯示文本內容。 因此，提供圖形格式的內容替代文字，讓無法看見圖形內容的使用者可以存取內容所提供的相同版本資訊。

另一個有用的好處是，替代文字可讓非文字內容依搜尋引擎技術建立索引。

#### 如何開會——非文字內容(1.1.1) {#how-to-meet-non-text-content}

對於靜態圖形，基本要求是為圖形提供等效的文本替代。 這可在「替代文字」欄 **位中完成** ; 請參閱核心元件影 **[像](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/components/image.translate.html)**。

>[!NOTE]
>
>有些現成可用的核心元件(例如 **[Carousel](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html)**)不提供將替代文字說明新增至個別影像的**Alternative Text **（替代文字）欄位，不過整個元件有**Label **field(**[](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html#accessibility-tab)** AccessibilityTab)。
>
>When implementing versions of these for your AEM instance, your development team will need to configure such components to support the `alt` attribute so that authors can add it to the content (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

AEM需要依預 **設填入「替代文字** 」欄位。 如果影像純粹是裝飾性的，而不需要替代文字，則可以 **檢查「影像是裝飾** 」選項。

#### 建立好的替代文字 {#creating-good-text-alternatives}

非文字內容有多種形式，因此文字替代項目的價值取決於圖形在網頁中所扮演的角色。 以下是一些一般經驗法則：

* 文字替代項目應簡明扼要，但應清楚地擷取非文字內容所提供之基本資訊。
* 應避免過長的說明（超過100個字元）。 如果替代文字需要更詳細的資訊：
   * 在替代文字中提供簡短說明
   * 並在相同頁面的其他位置或個別網頁的文字中有較長的說明。 將影像設為連結，或將文字連結置於影像旁，以連結至此個別的說明。
* 替代文字不應複製相同頁面附近文字表單中提供的內容。 請記住，許多影像是頁面文字中已涵蓋的點的插圖，因此可能已有詳細的文字替代項目。
* 如果非文字內容是指向其他頁面或檔案的連結，而沒有其他文字構成相同連結的一部分，則影像的替代文字必須指出連結的目的地，而非描述影像。
* 如果非文字內容包含在按鈕元素中，且沒有文字組成相同按鈕的一部分，則影像的替代文字必須指出按鈕的功能，而非描述影像。
* 對於給予空白(null)替代文字的影像，完全可以接受，但前提是影像不需要替代文字（例如，純粹是裝飾性圖形），或是頁面文字中已存在等同文字。

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

需要替代文字的特定非文字內容類型可能包括：

* 說明性像片： 這些是人物、物件或地點的影像。 請務必考慮像片在頁面中的角色，並且通常建議描述影像內容，因為輔助技術會宣佈元素類型(例如 `graphic` 或 `image`); 它可提高替代文字說 `screenshot` 明的使 `illustration` 用清晰度，但這取決於內容。 一致性是一個重要因素，因此應針對整個製作團隊做出決策，並套用至使用者體驗。
* 圖示： 這些是傳達特定資訊的小型圖片（圖形）。 必須在頁面和網站上一致使用這些變數。 頁面或網站上的圖示所有例項都應有相同的簡短文字替代項目，除非這麼做會造成相鄰文字的不必要複製。
* 圖表和圖形： 這些通常代表數值資料。 因此，提供文字替代選擇的一個選項可能是包含圖表或圖形中主要趨勢的簡短摘要。 如有必要，也可使用「進階影像屬性」索引標籤中的「說 **明** 」欄位，在文字中提供更詳 **細的說明** 。 此外，您也可以在頁面或網站的其他地方以表格形式提供來源資料。
* 地圖、圖表、流程圖： 對於提供空間資料的圖形（例如，支援描述對象或進程之間的關係），請確保關鍵消息以文本格式提供，並且該文本資訊位於每個相關資料點附近。 對於地圖，提供等同全文的地圖可能不切實際，但如果提供地圖以幫助人們找到特定位置的方式，則地圖影像的替代文字可以簡短地標示 *X*，然後在頁面其他地方的文字或透過 **Image元件的「** Advanced **」 (進階) 索引標籤中的「** Description **** 」 (說明) 欄位，提供指向該位置的指示。
* 驗證碼： 驗證碼是完全自 *動化的公共圖靈測試，可區分電腦和人*。 它是用於網頁上的安全檢查，用於區分人類和惡意軟體，但會造成無障礙環境支援。 這些影像需要使用者描述他們所看到的內容，才能通過安全性測試。 為影像提供替代文字顯然不可能，因此您需要考慮其他非圖形解決方案。 W3C提供了一些建議，如：
   * 邏輯謎題
   * 使用音效輸出而非影像
   * 使用帳戶和垃圾訊息篩選的限制。
* 背景影像： 這些功能是使用階層式樣式表(CSS)而非HTML來達成。 這表示無法指定替代文字值。 因此，背景影像不應提供重要的文字資訊——如果有的話，這項資訊也必須提供在頁面的文字中。 但是，當無法顯示影像時，必須顯示替代背景。

>[!NOTE]
>
>背景文字和前景文字之間應有適當的對比度； 這在對比度（最小值）(1.4.3) [中會有更詳細的討論](#contrast-minimum)。

#### 詳細資訊——非文字內容(1.1.1) {#more-information-non-text-content}

* [瞭解成功標準1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [如何符合成功標準1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [W3C說明及驗證碼的替代方案](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### 時間型媒體(1.2) {#time-based-media}

[准則1.2基於時間的媒體： 為時間型媒體提供替代選擇。](https://www.w3.org/TR/WCAG/#time-based-media)

這是針對以時間為基礎的 *網頁內容*。 這涵蓋使用者可播放的內容（例如視訊、音訊和動畫內容），並可預先錄制或即時串流。

### 純音訊和純視訊（預錄）(1.2.1) {#audio-only-and-video-only-prerecorded}

* 成功標準1.2.1
* A級
* 僅限音訊和僅限視訊（預錄）: 對於預錄的純音訊和純視訊媒體，除非音訊或視訊是文字的替代媒體，並明確標示為：
   * 僅預錄音效： 提供了用於基於時間的媒體的替代方案，該替代方案為預錄的僅音頻內容呈現等同資訊。
   * 僅預錄視訊： 提供了用於基於時間的媒體的替代選擇或音頻軌道，該音頻軌道顯示用於預錄的僅視頻內容的等效資訊。

#### 用途——僅限音訊和僅限視訊（預錄）(1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

視訊和音訊的協助功能問題可能會透過下列方式發生：

* 沒有配樂或配樂時，視覺受損者無法告知視訊或動畫中的情況；
* 聽障者，聾者，聽不到配樂；
* 聽得見配樂但不懂的人（例如，因為配樂是他們不懂的語言）。

使用不支援以特定媒體格式（例如Adobe Flash）播放內容的瀏覽器或裝置的使用者，也可能無法使用視訊或音訊。

以不同格式提供此資訊，例如文字（或無音訊的視訊音訊），可讓無法存取原始內容的使用者存取。

#### 如何開會——僅限音訊和僅限視訊（預錄）(1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* 如果內容是預先錄制的音訊，但沒有視訊（例如播客）:
   * 在內容之前或之後，提供連結至音訊內容的文字記錄。 成績單應是HTML頁面，其文字等同於所有口語和重要的非口語內容，另外還包括說話者的指示、設定的描述、聲音表達以及任何其他重要音效的描述。
* 如果內容是動畫或預錄的視訊，且沒有音效：
   * 在內容之前或之後，提供視訊所提供資訊的等同文字說明連結
   * 或是常用音訊格式（例如MP3）的等效音訊描述。

>[!NOTE]
>
>如果音訊或視訊內容是提供給已存在於相同網頁上其他格式之內容的替代內容，則可能不需要其他替代內容。
>
>《瞭解 [WCAG 1.2.1》准則](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)，提供了進一步的資訊。

將多媒體插入AEM網頁類似於插入影像。 然而，由於多媒體內容遠非靜態影像，因此有多種不同的設定和選項來控制多媒體的播放方式。

>[!NOTE]
>
>當您將多媒體與資訊性內容搭配使用時，您也必須建立替代內容的連結。 例如，若要包含文字成績單，請建立HTML頁面以顯示成績單，然後在音訊內容旁或下方新增連結。

#### 詳細資訊——僅限音訊和僅限視訊（預錄）(1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [瞭解成功標準1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [如何符合成功標準1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### 標題（預錄）(1.2.2) {#captions-prerecorded}

* 成功標準1.2.2
* A級
* 標題（預錄）: 除了媒體是文字的替代媒體，而且已清楚標示為同步媒體外，所有預先錄制的音訊內容都會提供標題。

#### 目的——標題（預錄）(1.2.2) {#purpose-captions-prerecorded}

聾人或聽障者將無法或很難存取音訊內容。 標題是語音和非語音音訊的文字等效，在視訊中的適當時間在螢幕上顯示。 它們讓聽不到音效的人，瞭解現在的情況。

#### 如何符合——標題（預錄）(1.2.2) {#how-to-meet-captions-prerecorded}

標題可以是：

* 開啟： 播放視訊時一律顯示
* 已關閉： 字幕可由使用者開啟或關閉

盡可能使用隱藏字幕，因為這可讓使用者選擇是否檢視字幕。

對於隱藏字幕，您需要在視訊檔案旁建立並提供適當格式(例如 [SMIL](https://www.w3.org/AudioVideo/))的同步化字幕檔案(如如何執行此動作的詳細資訊不在本指南中，但我們提供了 [More Information - Captions(Prerecorded)(1.2.2)下的教學課程連結](#more-information-captions-prerecorded)。 請確定您提供附註或啟用視訊播放器中的標題功能，讓使用者知道標題可用於視訊。

如果您必須使用開放標題，請將文字內嵌至視訊軌。 這可以使用影片編輯應用程式來實現，讓標題可以覆蓋在影片上。

#### 詳細資訊——標題（預錄）(1.2.2) {#more-information-captions-prerecorded}

* [瞭解成功標準1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [如何符合成功標準1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### 音訊描述或替代媒體（預錄）(1.2.3) {#audio-description-or-media-alternative-prerecorded}

* 成功標準1.2.3
* A級
* 音訊描述或媒體替代（預錄）: 為同步媒體提供基於時間的媒體或預錄視頻內容的音頻描述的替代物，除非媒體是文本的媒體替代物，並且被明確標示為這樣。

#### 用途——音訊說明或媒體替代（預錄）(1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

如果視障或視障人士僅以視覺化方式提供視訊或動畫中的資訊，或者配樂無法提供足夠的資訊，以視覺化方式瞭解發生的情況，將會遇到無障礙環境支援。

#### 如何開會——音訊說明或替代媒體（預錄）(1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

為滿足此成功標準，可採用兩種方法。 兩者皆可接受：

1. 加入視訊內容的其他音訊描述。 這可以通過以下三種方式之一實現：
   * 在現有對話方塊的暫停期間，提供場景中未呈現為現有音軌一部分的變更資訊；
   * 提供新的、額外的和選用的音軌，其中包含原始音軌，但也包含場景變更的額外音訊資訊。
      * 這可讓使用者在現有的音軌(其中 *不包含音訊* )和新的音軌(其中 *包含音訊說明* )之間切換。
      * 如此可避免中斷不需要其他說明的使用者。
   * 建立視訊內容的第二版本，以允許擴充音訊說明。 這可借由在適當的點暫停音訊和視訊，減少在現有對話方塊之間的間隙中提供詳細音訊描述的相關困難。 因此，在動作再次開始之前，可以提供更長的音訊描述。 如上例所示，這最好是選用的額外音軌，以防止不需要額外說明的使用者中斷。
1. 提供與視訊或動畫的音訊和視覺元素相當的適當文字記錄。 這應當包括，在適當情況下，指示說話者、設定說明、任何以視覺方式呈現的事件或資訊，以及聲音表達。 視其長度而定，您可以將成績單放在視訊或動畫的相同頁面，或放在個別頁面上； 如果您選擇後一個選項，請提供視訊或動畫旁的轉錄本連結。

如何建立音訊描述視訊的確切詳細資訊，不在本指南中。 建立視訊和音訊描述可能很耗時，但其他Adobe產品可協助您完成這些工作。

#### 詳細資訊——音訊說明或替代媒體（預錄）(1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [瞭解成功標準1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [如何符合成功標準1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### 標題(Live)(1.2.4)  {#captions-live}

* 成功標準1.2.4
* AA級
* 標題（即時）: 同步化媒體中所有即時音訊內容都提供標題。

#### 用途——標題（即時）(1.2.4) {#purpose-captions-live}

此成功標準與標題（預錄） [(](#captions-prerecorded) Captions)相同，因為它可解決失聰或聽障人士所遭遇的無障礙環境支援障礙，但此成功標准則處理即時簡報，例如網路廣播。

#### How to Meet - Captions(Live)(1.2.4) {#how-to-meet-captions-live}

請遵循上述標題(預 [錄)的指引](#captions-prerecorded) 。 但是，由於媒體的即時性質，必須盡快建立字幕布建，以因應目前的情況。 因此，您應考慮使用即時字幕或語音轉文字工具。

詳細說明超出本檔案的範圍，但下列資源可提供有用資訊：

* [WebAIM: 即時字幕](https://www.webaim.org/techniques/captions/realtime.php)

* [AccessComputing專案（華盛頓大學）: 是否可以使用語音識別自動產生字幕？](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### 詳細資訊——標題（即時）(1.2.4) {#more-information-captions-live}

* [瞭解成功標準1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [如何符合成功標準1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### 音訊說明（預錄）(1.2.5)  {#audio-description-prerecorded}

* 成功標準1.2.5
* AA級
* 音訊說明（預錄）: 提供同步媒體中所有預先錄制的視訊內容的音訊描述。

#### 用途——音訊說明（預錄）(1.2.5) {#purpose-audio-description-prerecorded}

此成功標準與「音訊說明」或「媒體替代項目（預錄） [](#audio-description-or-media-alternative-prerecorded)」相同，但作者必須提供更詳細的音訊說明，以符合「等級AA」。

#### 如何開會——音訊說明（預錄）(1.2.5) {#how-to-meet-audio-description-prerecorded}

依照「音訊描述」或「媒 [體替代項目（預先錄制）」的指引](#audio-description-or-media-alternative-prerecorded)。

#### 詳細資訊——音訊說明（預錄）(1.2.5) {#more-information-audio-description-prerecorded}

* [瞭解成功標準1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [如何符合成功標準1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### 適應性(1.3) {#adaptable}

[准則1.3適應性： 建立可以以不同方式呈現的內容（例如更簡單的版面），而不會遺失資訊或結構。](https://www.w3.org/TR/WCAG/#adaptable)

本准則涵蓋支援以下人員的必要要求：

* 可能無法存取作者在預設內容呈現中所呈現的資訊（例如，多欄版面或大量使用色彩和／或影像的頁面）。

* 可能會使用純音效，或是其他視覺顯示，例如大型文字或高對比度。

### 資訊與關係(1.3.1)  {#info-and-relationships}

* 成功標準1.3.1
* A級
* 資訊與關係： 通過表現傳遞的資訊、結構和關係可以通過寫程式方式確定，或在文本中可用。

#### 用途——資訊與關係(1.3.1) {#purpose-info-and-relationships}

許多殘障人士使用的輔助技術都仰賴結構資訊，以有效顯示或瞭解 *內容* 。 此結構資訊可以採用頁標題、表行和列標題以及清單類型的形式。 例如，螢幕閱讀程式可讓使用者從標題到標題瀏覽頁面。 但是，當頁面內容只看起來是透過視覺樣式而非基礎HTML來呈現結構時，輔助技術就無法使用結構資訊，限制了其支援更輕鬆瀏覽的能力。

此成功標準的存在是為了確保此類結構資訊是透過HTML或其他編碼技術以程式設計方式提供，讓瀏覽器和輔助技術可存取並運用這些資訊。

#### 如何認識——資訊與關係(1.3.1) {#how-to-meet-info-and-relationships}

AEM可讓您使用適當的HTML元素，輕鬆建構具有語義意義的網頁內容。 在RTE（文本元件）中開啟頁面內容，並使用 **Paraformat** （段落符號）菜單指定適當的結構元素（例如段落、標題等）。

您可以使用下列適用的元素，確保您的網頁已獲得適當的結構：

* **標題：** 只要您已啟用RTE的協助功能，AEM就會提供3層頁面標題。 您可以使用這些項目來識別內容的區段和子區段。標題1是標題的最高級別，標題3是最低級別。系統管理員可以配置系統以允許使用更多標題級別。

* **清單**: 您可以使用HTML來指定三種不同的清單類型：
   * 元素 `<ul>` 用於無序 *列*  (項目符號) 清單。使用元素來識別個別清 `<li>` 單項目。在RTE中，使用「項目符號列 **表」表徵圖** 。
   * The `<ol>` element is used for *numbered* lists. 使用元素來識別個別清單 `<li>` 項目。 在RTE中，使用「編號列 **表」表徵圖** 。
   如果要將現有內容變更為特定的清單類型，請反白標示適當的文字並選取適當的清單類型。 如先前顯示如何輸入段落文字的範例，適當的清單元素會自動新增至您的HTML。

   在全螢幕模式中，會顯示個別 **的「項目符號清單** 」和「 **** 編號清單」圖示。當未處於全螢幕模式時，單一「清單」圖示後面會提供這兩個 **選項** 。

* **表格**: 必須使用HTML表格元素來識別資料表格：
   * 一個元 `<table>` 素
   * 表 `<tr>` 中每一行的元素
   * 每 `<th>` 行和列標題的元素
   * 每個 `<td>` 資料儲存格的元素
   此外，可存取的表格還使用下列元素和屬性：

   * 元 `<caption>` 素用於提供表格的可見標題。 字幕預設會出現在表格的正中，但可使用CSS適當定位。 標題以寫程式方式與表關聯，因此它是提供內容介紹的有用方法。
   * 元 `<summary>` 素提供有視覺的使用者可看到的摘要，協助無視的使用者更輕鬆地瞭解表格中顯示的資訊。 在使用複雜或非常規表格版面時（此屬性不會顯示在瀏覽器中，只會讀出至輔助技術），此功能特別有用。
   * 元 `scope` 素的屬性用 `<th>` 於指示儲存格代表特定列或特定欄的標題。 類似的方法是在複雜表格中使用標題和id屬性，其中資料儲存格可與一或多個標題相關聯。
   >[!NOTE]
   >
   >By default, these elements and attributes are not directly available, though it is possible for the system administrator to add support for these values in the **Table properties** dialog box (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes).

   要開啟「表 **」(Table** )對話框 **，可以在其中選擇「表** 屬性」(Table Properties)頁籤：

   * 定義適當的 **標題**。
   * 理想情況下，請移除「寬 **度」、「邊框高度」、「邊框高度」、「邊框高度**」、「單元格間距」、「單元格間距 **」、「單元格**************&#x200B;間距」的預設值。因為這些屬性可以在全局樣式表中設定。
   然後，您可以使用 **儲存格屬性** ，選擇儲存格是資料或標題儲存格：

* **重點**: 使用或 `<strong>` 元素 `<em>` 來指示強調。 請勿使用標題來反白標示段落中的文字。
   * 反白標示您要強調的文字；
   * 按一下「屬性」面板中顯示的 **B** 表徵圖( `<strong>`for)或「屬性」面板中顯示 **的「I** 」表徵圖(for `<em>`)(請確定已選 **** 中HTML)。

      >[!NOTE]
      >
      >標準AEM安裝中的RTE已設定為使用：
      >
      >* `<b>` 的 `<strong>`
      >* `<i>` 的 `<em>`
      >
      >它們實際上是相同的，但 `<strong>` 是 `<em>` 更可取，因為它們在語義上正確。 您的開發團隊可以設定RTE，以在開 `<strong>` 發您的專 `<em>` 案例項時使 `<b>` 用和(而非和 `<i>`)。


* **複雜的資料表**:在某些情況下，如果有具有兩個或多個標題級別的複雜表，則基本表屬性可能不足以提供所有必要的結構資訊。對於這些類型的複雜表格，需要使用header和 **id屬性在標題及其相關儲存格之間建** 立直 **接** 關係。

   >[!NOTE]
   >
   >id屬性不適用於現成可用的安裝。 它可以通過配置HTML規則和RTE中的串列化函式來啟用。

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

   若要在AEM中達成此目的，您必須使用來源編輯模式直接新增標籤。

   >[!NOTE]
   >
   >標準安裝中不會立即使用此功能。 它需要配置RTE、HTML規則和串列化器。

#### 詳細資訊——資訊與關係(1.3.1) {#more-information-info-and-relationships}

* [瞭解成功標準1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [如何符合成功標準1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### 有意義的序列(1.3.2)  {#meaningful-sequence}

* 成功標準1.3.2
* A級
* 有意義的序列： 當內容呈現的序列影響其含義時，可以寫程式地確定正確的讀取序列。

#### 目的——有意義的序列(1.3.2) {#purpose-meaningful-sequence}

本「成功准則」的目的是讓使用者代理提供內容的替代呈現方式，同時保留理解其含義所需的閱讀順序。 必須能夠以程式設計方式確定至少一個有意義的內容序列。 當輔助技術以錯誤的順序讀取內容，或套用替代樣式表或其他格式變更時，不符合此成功准則的內容可能會混淆或誤導使用者。

#### 如何相遇——有意義的序列(1.3.2) {#how-to-meet-meaningful-sequence}

請遵循「如 [何符合成功准則1.3.2」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)。

#### 詳細資訊——有意義的序列(1.3.2) {#more-information-meaningful-sequence}

* [瞭解成功標準1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [如何符合成功標準1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### 感官特性(1.3.3)  {#sensory-characteristics}

* 成功標準1.3.3
* A級
* 感官特徵： 提供的理解和操作內容的指示不僅依賴於部件的感官特性，如形狀、大小、視覺位置、方向或聲音。

#### 目的——感官特性(1.3.3) {#purpose-sensory-characteristics}

設計人員通常會專注在視覺設計功能上，例如顏色、形狀、文字樣式，或內容在呈現資訊時的絕對或相對位置。 這些設計技術在傳遞資訊方面非常強大（並且可以改善有認知無障礙需求的有視力的用戶的總體無障礙性），但盲人或視覺障礙的人可能無法訪問需要視覺識別屬性（如位置、顏色或形狀）的資訊。

同樣地，如果需要區分不同聲音（例如男性或女性口語內容）的資訊沒有反映在音頻內容的任何文本替代中，則對聽力有障礙的人會造成無障礙。

>[!NOTE]
>
>有關顏色替代項的相關要求，請參閱 [使用顏色](#use-of-color)。

#### 如何滿足感官特性(1.3.3) {#how-to-meet-sensory-characteristics}

請確定任何依賴頁面內容視覺特性的資訊，也會以替代格式顯示。

* 不要依賴視覺位置提供資訊。 例如，若您想將使用者引至頁面右側的功能表，以取得詳細資訊，請勿參 *閱右側的功能表*; 請改為命名功能表（例如透過標題），並在文字中參照該名稱。
* 切勿依賴文字樣式（例如粗體或斜體文字）來傳達資訊。

>[!NOTE]
>
>如果明白描述性詞語在非視覺化內容中有意義，則可接受使用。 例如，使用 *上述**和下* 述內容通常是可接受的，因為它們分別表示特定內容項目前後的內容； 當內容被大聲朗讀時，這仍然有意義。

#### 更多資訊——感官特性(1.3.3) {#more-information-sensory-characteristics}

* [瞭解成功標準1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [如何符合成功標準1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### 可區分(1.4) {#distinguishable}

[准則1.4可區分： 讓使用者更輕鬆地檢視和聽取內容，包括將前景與背景分開。](https://www.w3.org/TR/WCAG/#distinguishable)

### 色彩的使用(1.4.1)  {#use-of-color}

* 成功標準1.4.1
* A級
* 色彩的使用： 顏色不是傳送資訊、指示動作、提示響應或區分視覺元素的唯一視覺手段。

>[!NOTE]
>
>此成功標準可特別處理色彩感知。 其他形式的觀感皆涵蓋在 [Appative(1.3)中](#adaptable); 包括程式化存取色彩和其他視覺化簡報編碼。

#### 用途——色彩的使用(1.4.1) {#purpose-use-of-color}

顏色是增強網頁美感的一種明顯有效的方式，在資訊傳遞方面也有很大的幫助。 但是，從失明到彩色視覺缺陷，都存在著一系列的視覺缺陷，這意味著有些人無法區分某些顏色。 這使得色彩編碼成為提供資訊的不可靠方式。

例如，有紅綠色視覺缺陷的人，將無法區分綠色和紅色。 他們可能會將這兩種顏色視為第三種顏色（例如，棕色），在這種情況下，他們將無法區分紅色、綠色和棕色。

此外，使用純文字瀏覽器、單色顯示裝置或檢視頁面黑白列印成品的使用者無法察覺色彩。

另一個考量是介面 *元素* （例如，標籤、切換按鈕等）的選取狀態，它需要以非僅使用顏色和超出視覺呈現的方式傳達。 對於這些元素，額外使用圖樣、形狀和程式化資訊對於建立完全包容且不依賴特定意義的使用者體驗非常有用。

#### 如何符合——色彩的使用(1.4.1) {#how-to-meet-use-of-color}

無論使用何種顏色來傳達資訊，請確定這些資訊是可用的，而不需要查看顏色。

例如，請確定文字中也明確提供由顏色提供的資訊。

如果使用顏色做為提供資訊的提示，您應提供額外的視覺提示，例如變更樣式（例如粗體、斜體）或字型。 這可協助視力低下或色彩視覺缺乏者識別資訊。 但是，它不能完全依賴，因為它不會幫助根本看不到頁面的人。 因此，（有時）提供隱藏文字或使用程式化解決方案(例如 [Accessible Rich Internet Applications(ARIA)Web標準套件](https://www.w3.org/WAI/standards-guidelines/aria/))，將此資訊傳達給無目光的使用者是很有用的。

#### 更多資訊——色彩的使用(1.4.1) {#more-information-use-of-color}

* [瞭解成功標準1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [如何符合成功標準1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### 音訊控制(1.4.2)  {#audio-control}

* 成功標準1.4.2
* A級
* 音訊控制： 如果網頁上的任何音訊自動播放超過3秒，則可使用暫停或停止音訊的機制，或使用獨立於整體系統音量等級的機制來控制音訊音量。

#### 用途——音訊控制(1.4.2) {#purpose-audio-control}

使用螢幕閱讀軟體的使用者若同時播放其他音訊，就很難聽到語音輸出。 當螢幕閱讀器的語音輸出是以軟體為基礎（如今大多數），並透過與音效相同的音量控制來控制時，這一困難就會加劇。 此外，一些認知障礙者和神經發散者可能具有聽覺敏感性。 這些人會發現，無法變更音訊內容的音量等級會造成相當的中斷。

因此，使用者必須能夠關閉背景音效。

>[!NOTE]
>
>對音量的控制包括能夠將音量減小到零。

#### 如何符合——音訊控制(1.4.2) {#how-to-meet-audio-control}

請遵循「如 [何符合成功准則1.4.2」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)。

#### 詳細資訊——音訊控制(1.4.2) {#more-information-audio-control}

* [瞭解成功標準1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [如何符合成功標準1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### 對比度（最低）(1.4.3) {#contrast-minimum}

* 成功標準1.4.3
* AA級
* 對比度（最小值）: 文字和影像的視覺呈現至少有4.5:1的對比率，但下列除外：
   * 大型文字： 大型文字和大型文字影像的對比度至少為3:1。
   * 附帶： 屬於非作用中使用者介面元件的文字或影像、純粹的裝飾、任何人看不到的文字或影像 [](https://www.w3.org/TR/WCAG/#dfn-pure-decoration)，或是包含重要其他視覺內容之圖片的一部分，則無對比需求。
   * Logotypes: 屬於標誌或品牌名稱的文字沒有最低對比要求。
   >[!NOTE]
   >
   >如需詳 [細資訊，請參閱瞭解非文字對比](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) ，以協助內容作者瞭解非文字元素（包括圖示、介面元素等）的其他需求。

#### 用途——對比（最低）(1.4.3) {#purpose-contrast-minimum}

某些視覺障礙的人可能無法區分某些低對比色彩對。 如果以下情況，這些人可能會遇到無障礙環境支援問題：

* 文字與背景顏色對比較差。
* 文本（如連結文本和非連結文本）的顏色編碼在區分資訊方面具有重要意義。

>[!NOTE]
>
>純用於裝飾目的的文字會排除在此成功標準之外。

#### 如何符合——對比（最低）(1.4.3) {#how-to-meet-contrast-minimum}

請確定文字與其背景對比充分。 對比率取決於相關文本的大小和樣式：

* 對於大小小於18點（或14點粗體）的文字，文字的文字／影像與背景的對比率應至少為4.5:1。
* 對於大小至少為18點（或14點粗體）的文字，對比率應至少為3:1。
* 如果對背景進行圖案化，則任何文字周圍的背景都應該著色，以保持4.5:1或3:1比例。

>[!NOTE]
>
>請記住，字型在轉換等同PT/PX/EM大小時可能會有所不同。
>
>建議您在選擇適當的字型和網頁內容調整大小時，在可讀性和可用性方面運用良好的判斷力和錯誤。

>[!NOTE]
>
>以下網站可協助轉換至其他單位：
>
>* [Px到Em Calcuter - Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* [字型大小轉換： pixel-point-em-rem-percent](https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/)
>* [PMtoEM.com: 將PX轉換為EM變得簡單](http://pxtoem.com)


若要檢查對比度，請使用顏色對比工具，例如 [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) 或 [WebAIM顏色對比檢查器](https://www.webaim.org/resources/contrastchecker/)。 這些工具可讓您檢查顏色對，並報告任何對比問題。

或者，如果您不太在意指定頁面的外觀，可以選擇不指定背景和前景文字顏色。 不需要進行對比檢查，因為使用者的瀏覽器會決定文字和背景的顏色。

如果無法達到建議的對比度等級，您將需要提供頁面的替代等同版本（沒有顏色對比問題）的連結，或讓使用者根據自己的需求調整頁面色彩配置的對比度。

#### 詳細資訊——對比度（最低）(1.4.3) {#more-information-contrast-minimum}

* [瞭解成功標準1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [如何符合成功標準1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### 調整文字大小(1.4.4)  {#resize-text}

* 成功標準1.4.4
* A級
* 調整文字大小： 除了文字的標題和影像外，不需使用輔助技術就可調整文字大小，最高200%不會遺失內容或功能。

#### 用途——調整文字大小(1.4.4) {#purpose-resize-text}

本「成功准則」的目的是確保能夠成功縮放視覺化轉譯文字，包括以文字顯示的控制項(與仍以資料形式(例如ASCII [])顯示的文字字元)，讓視覺障礙輕微的人直接讀取文字，而不需使用輔助技術（例如螢幕放大鏡）。 使用者可從縮放網頁上所有內容中獲益，但文字最重要。

#### 如何開會——調整文字大小(1.4.4) {#how-to-meet-resize-text}

除了遵循「如何符合成功准則1.4.4 [」(](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) How to Meet Success Criteria 1.4.4)下的准則，您還可以鼓勵內容作者在其頁面設計和字型大小（例如，互動式網頁設計）中使用流暢、有彈性的寬度和高度，讓讀者能夠調整文字大小。

#### 詳細資訊——調整文字大小(1.4.4) {#more-information-resize-text}

* [瞭解成功標準1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [如何符合成功標準1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### 文字影像(1.4.5) {#images-of-text}

* 成功標準1.4.5
* AA級
* 文字影像： 如果所使用的技術可以實現視覺呈現，則除了下列項目外，文字會用來傳達資訊，而非文字影像：
   * 可自訂： 文本影像可以根據用戶的需求進行可視化定製；
   * 基本： 對所傳達的資訊而言，文本的具體呈現至關重要。

>[!NOTE]
>
>Logotypes（屬於標誌或品牌名稱的文字）被視為必要項目。

#### 用途——文字影像(1.4.5) {#purpose-images-of-text}

當偏好特定文字樣式時，通常會使用文字影像； 例如，logotype或如果文字是從其他來源產生（例如，掃描紙張檔案）。 但是，與使用HTML呈現的文字和使用CSS建立樣式的文字相比，文字的影像缺乏彈性來變更尺寸或外觀，這對於有視覺障礙或閱讀困難的人而言可能是必要的。

#### 如何開會——文字影像(1.4.5) {#how-to-meet-images-of-text}

如果必須使用文字影像，請使用CSS將文字影像取代為HTML中的等同文字，讓文字以可自訂的方式使用。 如需如何達成此目的的範例，請參閱 [C30: 使用CSS將文字取代為文字影像，並提供使用者介面控制項來切換](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30)。

#### 詳細資訊——文字影像(1.4.5) {#more-information-images-of-text}

* [瞭解成功標準1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [如何符合成功標準1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## 原則2: 可操作 {#principle-operable}

[原則2: 可操作——用戶介面元件和導航必須可操作。](https://www.w3.org/TR/WCAG/#operable)

### 可存取鍵盤(2.1) {#keyboard-accessible}

[准則2.1可存取鍵盤： 從鍵盤使用所有功能。](https://www.w3.org/TR/WCAG/#keyboard-accessible)

這就是為了確保使用者可以使用鍵盤存取所有功能。

### 鍵盤(2.1.1)  {#keyboard}

* 成功標準2.1.1
* A級
* 鍵盤： 所述內容的所有功能可通過鍵盤介面操作而不需要個別按鍵的特定定時，除非所述基礎功能需要取決於用戶移動的路徑而不是僅僅取決於端點的輸入。

#### 用途——鍵盤(2.1.1) {#purpose-keyboard}

本「成功准則」的目的在於確保內容可透過鍵盤或鍵盤介面（以便使用替代鍵盤）運作。 當內容可透過鍵盤或替代鍵盤操作時，無視力的人（無法使用例如需要眼睛協調的老鼠等裝置），以及必須使用替代鍵盤或輸入裝置作為鍵盤模擬器的人，都可進行操作。 鍵盤模擬器包括語音輸入軟體、Sip-and-puff軟體、螢幕上鍵盤、掃描軟體以及各種輔助技術和替代鍵盤。 視力低的個人也可能無法追蹤指標，如果能夠從鍵盤控制，就會發現軟體的使用更輕鬆（或僅限可能）。

#### 如何開會——鍵盤(2.1.1) {#how-to-meet-keyboard}

請遵循「如 [何符合成功准則2.1.1」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)。

#### 更多資訊——鍵盤(2.1.1) {#more-information-keyboard}

* [瞭解成功標準2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何符合成功標準2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### 無鍵盤陷印(2.1.2)  {#no-keyboard-trap}

* 成功標準2.1.2
* A級
* 無鍵盤陷阱： 如果鍵盤焦點可以使用鍵盤介面移動到頁面的元件，則焦點可以僅使用鍵盤介面從該元件移開，並且，如果它需要的不是未修改的箭頭鍵或Tab鍵或其他標準退出方法，則建議用戶使用將焦點移開的方法。

#### 用途——無鍵盤陷印(2.1.2) {#purpose-no-keyboard-trap}

本「成功准則」的目的是確保內容不會陷 *入* 「網頁」內容子區段內的鍵盤焦點。 當頁面內結合多種格式並使用外掛程式或內嵌應用程式來轉換時，這是常見的問題。

有時網頁的功能會將焦點限制在內容的子部分（例如，模式對話）。 在這種情況下，您應提供一種方法，讓使用者能夠退出該內容的子部分（例如，ESC鍵關閉模態對話框，或「關閉」按鈕關閉模態對話框）。

#### 如何開會——無鍵盤陷阱(2.1.2) {#how-to-meet-no-keyboard-trap}

請遵循「如 [何符合成功准則2.1.2」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)。

#### 詳細資訊——無鍵盤陷印(2.1.2) {#more-information-no-keyboard-trap}

* [瞭解成功標準2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何符合成功標準2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### 足夠的時間(2.2) {#enough-time}

[准則2.2足夠時間： 為使用者提供足夠的時間閱讀和使用內容。](https://www.w3.org/TR/WCAG/#enough-time)

這就是為了確保使用者有足夠的時間閱讀並採取行動。

### 可調整時間(2.2.1)  {#timing-adjustable}

* 成功標準2.2.1
* A級
* 鍵盤： 為使用者提供足夠的時間閱讀和使用內容。

#### 用途——可調整時間(2.2.1) {#purpose-timing-adjustable}

本「成功准則」的目的在於確保為殘障人士提供適當的時間，讓他們盡可能與網頁內容互動。 失明、低視力、靈活度障礙和認知限制等殘障人士可能需要更多時間閱讀內容或執行功能，例如填寫線上表格。 如果Web函式與時間相關，某些用戶將難以在時間限制出現之前執行所需的操作。 這可能會使他們無法存取服務。 設計不依賴時間的功能將幫助殘障人士成功完成這些功能。 提供選項來停用時限、自訂時限長度或在時間限制發生之前請求更多時間，可協助那些需要超過預期時間的使用者順利完成工作。 這些選項會依對使用者最有幫助的順序列出。 停用時間限制比自訂時間限制長度好，這比在時間限制出現之前請求更多時間好。

#### 如何符合——可調整時間(2.2.1) {#how-to-meet-timing-adjustable}

請遵循「如 [何符合成功標準2.2.1」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)。

#### 更多資訊——可調整計時(2.2.1) {#more-information-timing-adjustable}

* [瞭解成功標準2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [如何符合成功標準2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### 暫停、停止、隱藏(2.2.2)  {#pause-stop-hide}

* 成功標準2.2.2
* A級
* 暫停、停止、隱藏： 對於移動、閃爍、捲動或自動更新資訊，以下是正確的：
   * 移動、閃爍、滾動： 對於(a)自動啟動、(b)持續超過五秒，且(c)與其他內容並行顯示的任何移動、閃爍或捲動資訊，使用者有暫停、停止或隱藏的機制，除非動作、閃爍或捲動是活動不可或缺的一部分；
   * 自動更新： 對於任何(a)自動啟動且(b)與其他內容並行顯示的自動更新資訊，使用者有暫停、停止或隱藏更新或控制更新頻率的機制，除非自動更新是其必要活動的一部分。

注意事項有：

1. 有關閃爍或閃爍內容的要求，請參閱「Do not Design Content in a Way that is Know to Cause Countude(2.3)（以已知導致癲癇的方式設計內容）」。
1. 由於任何不符合此成功標準的內容都可能干擾使用者使用整個頁面的能力，因此網頁上的所有內容（無論是否用於符合其他成功標準）都必須符合此成功標準。 請參 [閱符合性要求5: 不干涉](https://www.w3.org/TR/WCAG20/#cc5)。
1. 由軟體定期更新或流向用戶代理的內容不需要保留或呈現在暫停開始和恢復演示之間生成或接收的資訊，因為這在技術上可能不可能，在許多情況下可能會誤導。
1. 如果在預先載入階段或類似情況中發生的動畫，對於所有使用者而言，在該階段無法進行互動，且若未指出進度，可能會混淆使用者，或導致使用者認為內容已凍結或中斷，則視為必要。

#### 用途——暫停、停止、隱藏(2.2.2) {#purpose-pause-stop-hide}

某些使用者可能會發現移動的內容會分散注意力，甚至是讓身體很痛苦，因此很難將注意力集中在頁面的其他部分。 此外，對於無法跟上動態文字腳步的人而言，這些內容可能很難閱讀。

#### 如何開會——暫停、停止、隱藏(2.2.2) {#how-to-meet-pause-stop-hide}

根據內容的性質，在建立包含移動、閃爍或閃爍內容的網頁時，您可以套用下列一或多個建議：

* 提供暫停捲動內容的方式，讓使用者有足夠的時間閱讀內容。 例如，新聞提示器、自動更新的文字，以及自動前進的影像轉盤。
* 請確定眨眼的內容在5秒後停止閃爍。
* 使用適當的技術來顯示可由瀏覽器停用的移動或閃爍內容。 例如，圖形交換格式(GIF)或可移植網路圖形(APNG)動畫檔案。
* 在網頁上提供表單控制項，讓使用者停用頁面上所有移動或閃爍的內容。
* 如果無法使用上述任一功能，請提供包含所有內容的頁面連結，但不會移動或閃爍。

#### 詳細資訊——暫停、停止、隱藏(2.2.2) {#more-information-pause-stop-hide}

* [瞭解成功標準2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [如何符合成功標準2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### 癲癇與身體反應(2.3) {#seizures-and-physcial-reactions}

[准則2.3緝獲： 切勿以已知會導致癲癇或身體反應的方式設計內容。](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### 閃爍三次或低於閾值(2.3.1) {#three-flashes-or-below-threshold}

* 成功標準2.3.1
* A級
* 閃爍三次或低於閾值： 網頁不包含任何在任一秒內閃爍超過三次的內容，或flash低於一般flash和紅色flash臨界值。

>[!NOTE]
>
>由於任何不符合此成功標準的內容都可能干擾使用者使用整個頁面的能力，因此網頁上的所有內容（無論是否用於符合其他成功標準）都必須符合此成功標準。 請參 [閱符合性要求5: 不干涉](https://www.w3.org/TR/WCAG/#cc5)。

#### 用途——三個閃爍或低於閾值(2.3.1) {#purpose-three-flashes-or-below-threshold}

在某些情況下，閃爍的內容可能導致感光性癲癇。 此成功標準可讓這些使用者存取並體驗所有內容，而不需擔心內容閃爍。

#### 如何符合——三個閃爍或低於閾值(2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

您應採取步驟，以確保套用下列技術：

* 確保元件在一秒內不會閃爍超過三次；
* 如果無法符合上述條件，則在螢幕上以像素為單位，在小 *的安全區域內* ，顯示閃爍的內容。 此區域是使用 [G176中涵蓋的複雜公式計算： 保持閃爍區域足夠小](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)，因此只有在絕對需要閃爍內容時才應 *該* 。

#### 更多資訊——閃爍三次或低於臨界值(2.3.1) {#more-information-three-flashes-or-below-threshold}

* [瞭解成功標準2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [如何符合成功標準2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### 可導覽(2.4) {#navigable}

[准則2.4可導航： 提供協助使用者導覽、尋找內容及判斷其所在位置的方式。](https://www.w3.org/TR/WCAG/#navigable)

這可確保內容簡單易用，讓使用者輕鬆導覽。

### 略過區塊(2.4.1)  {#bypass-blocks}

* 成功標準2.4.1
* A級
* 略過區塊： 一種機制可略過多個網頁上重複的內容區塊。

#### 用途——略過區塊(2.4.1) {#purpose-bypass-blocks}

本「成功准則」的目的，在於讓依序導覽內容的使用者更直接存取網頁的主要內容。 網頁和應用程式通常會有內容出現在其他頁面或螢幕上。 重複的內容區塊範例包括但不限於導覽連結、頁首圖形、選單和廣告影格。 就本規定而言，個別字詞、片語或單一連結等重複的小段不視為區塊。

#### 如何相遇——繞過塊(2.4.1) {#how-to-meet-bypass-blocks}

請遵循「如 [何符合成功標準2.4.1」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)。

#### 詳細資訊——略過區塊(2.4.1) {#more-information-bypass-blocks}

* [瞭解成功標準2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [如何符合成功標準2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### 標題為(2.4.2)的頁面  {#page-titled}

* 成功標準2.4.2
* A級
* 標題為： 網頁標題可說明主題或目的。

#### 用途——標題為(2.4.2)的頁面 {#purpose-page-titled}

此成功標準可協助每個人（不論是否有任何特定的損害）快速識別網頁內容，而不需完整閱讀網頁。 當在瀏覽器標籤中開啟多個網頁時，這特別有用，因為頁面標題會顯示在標籤中，因此可快速找到。

#### 如何開會——標題為(2.4.2)的頁面 {#how-to-meet-page-titled}

在AEM中建立新的HTML頁面時，您可以指定頁面標題。 請確定標題已充分說明頁面的內容和用途，尤其是任何獨特的方面，讓訪客可以快速識別內容是否與其需求實際相關。

編輯頁面時，您也可以編輯頁面標題，頁面資訊——屬 **性可****存取。**

#### 更多資訊——標題為(2.4.2)的頁面 {#more-information-page-titled}

* [瞭解成功標準2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [如何符合成功標準2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### 焦點順序(2.4.3)  {#focus-order}

* 成功標準2.4.3
* A級
* 焦點順序： 如果網頁可依序導覽，而導覽順序會影響意義或操作，則可聚焦元件會依保留意義和操作性的順序接收焦點。

#### 用途——焦點訂單(2.4.3) {#purpose-focus-order}

本「成功准則」的目的是確保當使用者依序瀏覽內容時，會以符合內容含義的順序遇到資訊，並可從鍵盤操作。 這可讓使用者對內容建立一致的心理模型，以減少混淆。 內容中可能會有不同順序反映邏輯關係。 例如，在由多個欄位和／或步驟組成的線上表單中移動元件，會反映內容中的邏輯關係。

#### 如何滿足——焦點訂單(2.4.3) {#how-to-meet-focus-order}

請遵循「如 [何符合成功標準2.4.3」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)。

#### 更多資訊——焦點訂單(2.4.3) {#more-information-focus-order}

* [瞭解成功標準2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [如何符合成功標準2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### 連結用途（在內容中）(2.4.4)  {#link-purpose-in-context}

* 成功標準2.4.4
* A級
* 連結用途（在內容中）: 每個連結的目的可以單獨地從連結文本確定，也可以從連結文本連同其寫程式確定的連結上下文一起確定，除非連結的目的一般對用戶來說是模糊的。

#### 目的——連結目的（在內容中）(2.4.4) {#purpose-link-purpose-in-context}

對所有使用者而言，無論是否受到損害，透過適當的連結文字清楚指出連結的方向至關重要。 這可協助使用者決定是否實際要追蹤連結。 對有目光的使用者而言，當頁面上有數個連結時（尤其是頁面文字較多時），有意義的連結文字非常有用，因為有意義的連結文字可更清楚地指出目標頁面的功能。 某些輔助技術的使用者可以在單一頁面上產生所有連結的清單，如果連結文字既獨特又具資訊性，就可以更輕鬆地瞭解不符合上下文的連結文字。 然而，如果連結無法提供足夠的資訊，以準確描述連結將帶往何處，則有認知障礙的有視者可能會感到困惑。

#### 如何符合——連結目的（在內容中）(2.4.4) {#how-to-meet-link-purpose-in-context}

首先，請確定連結的目的在連結的文字中已清楚說明。

* 錯誤示例：
   * 文字： 如需2010年秋季晚間課程的詳細資訊，請按一下這裡。
   * 原因： 它沒有明確，明確地指出其目的地。
* 好例子：
   * 文字： 2010年秋季夜校課程——詳細內容。
   * 原因： 只要稍微調整文字和連結元素的位置，連結文字就可以改善：

連結應在各頁面上使用一致的措辭，尤其是導覽列。 例如，如果某個頁面上的特定頁面連結名為 **Publications** ，請在其他頁面上使用該文字以確保一致性。

在編寫時，使用標題屬性會有一些問題，以確保頁面上顯示的類似連結提供有關目的地的唯一資訊（例如，「閱讀更多」通常會指一系列不同的目的地）:

* 標題屬性中包含的文字通常僅供滑鼠使用者使用，做為工具提示快顯視窗，而且無法使用鍵盤或行動使用者一致地存取。
* 螢幕閱讀程式可讀出標題屬性，但此功能可能未依預設啟用； 因此，使用者可能不知道標題屬性存在。
* 很難改變標題文本的外觀，這意味著有些人可能很難或不可能閱讀。

因此，雖然title屬性可用來提供連結的額外內容，但請注意其限制，請勿將它當做適當連結文字的替代項目。

當連結由影像組成時，請確定影像的替代文字說明連結的目的地。 例如，如果將書架的影像設為人物出版物的連結，則替代文字應閱讀 **John Smith的出版物** ，而非 **Bookshelf**。

或者，如果連結錨點除了影像元素以外還包含說明連結用途的文字（因此文字會出現在影像旁邊），請為影像使用空白alt屬性：

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>上述程式碼片段是圖示，建議您使用 **Image** 元件。

雖然建議提供識別連結目的的連結文字，而不需要額外的內容，但是可以認識到，這並非總是可能。 下列情況可使用內容自由連結，其HTML範例可在 [How to Meet Success Criterion 2.4.4中找到](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)。

* 其中連結文字是緊密相關連結清單的一部分，而包含連結的清單項目則提供足夠的內容。
* 從前款（非下款）項文 *本中* ，可以明確連結目的的。
* 如果連結包含在資料表中，因此可以從關聯的標題中清楚地確定目的。
* 其中，連結清單包含在一組標題中，標題本身提供了合適的上下文。
* 其中，連結清單包含在巢狀連結中，而巢狀連結上方的上層清單項目則提供適當的內容。

在某些情況下，如果頁面上有數個連結（其中每個連結以複雜但必要的詳細資訊提供連結的方向），則可以提供網頁的替代版本，以顯示完全相同的內容，但連結文字未如此詳細。

或者，可以使用指令碼，使得在連結本身內提供最少數量的文本，但在激活定位在頁面頂部的適當控制項時，連結文本被擴展 ** 。 類似的方法是使用CSS來隱藏 *完整連結* ，以免有目光的使用者看到，但仍會將它完整輸出給螢幕閱讀程式使用者。 這不屬於本檔案的範圍，但有關如何達成此目的的更多資訊，請參閱「更多資訊——連結用途（在內容中）」(2.4.4)一節 [](#more-information-link-purpose-in-context) 。

#### 詳細資訊——連結用途（在內容中）(2.4.4) {#more-information-link-purpose-in-context}

* [瞭解成功標準2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [如何符合成功標準2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### 多種方式(2.4.5)  {#multiple-ways}

* 成功標準2.4.5
* AA級
* 多種方式： 在一組網頁中，除了網頁是某個程式的結果或步驟之外，還有多種方法可用來尋找網頁。

#### 用途——多種方式(2.4.5) {#purpose-multiple-ways}

本「成功准則」的目的，在於讓使用者能以最符合其需求的方式來尋找內容。 使用者會發現，一種技術比另一種技術更容易使用或更容易理解。

即使是小型網站，也應該為使用者提供一些方向。 對於三、四個頁面網站（所有頁面皆從首頁連結），僅提供來自首頁和來自首頁的連結（首頁上的連結也可當成網站地圖）就足夠了。

#### 如何開會——多種方式(2.4.5) {#how-to-meet-multiple-ways}

請遵循「如 [何符合成功標準2.4.5」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)。

#### 更多資訊——多種方式(2.4.5) {#more-information-multiple-ways}

* [瞭解成功標準2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [如何符合成功標準2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### 標題和標籤(2.4.6)  {#headings-and-labels}

* 成功標準2.4.6
* AA級
* 標題和標籤： 標題和標籤描述主題或目的。

#### 用途——標題和標籤(2.4.6) {#purpose-headings-and-labels}

本「成功准則」旨在協助使用者瞭解網頁中包含哪些資訊以及該資訊的組織方式。 當標題清晰且描述性強時，使用者可以更輕鬆地找到他們所尋找的資訊，並更輕鬆地瞭解內容不同部分之間的關係。 描述性標籤可協助使用者識別內容中的特定元件。

#### 如何符合——標題和標籤(2.4.6) {#how-to-meet-headings-and-labels}

請遵循「如 [何符合成功標準2.4.6」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)。

#### 詳細資訊——標題和標籤(2.4.6) {#more-information-headings-and-labels}

* [瞭解成功標準2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [如何符合成功標準2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### 焦點可見(2.4.7)  {#focus-visible}

* 成功標準2.4.7
* AA級
* 焦點可見： 任何鍵盤可操作的用戶介面具有操作模式，其中鍵盤焦點指示器是可見的。

#### 用途——焦點可見(2.4.7) {#purpose-focus-visible}

此成功標準的目的是協助使用者瞭解哪個元素具有鍵盤焦點。

人必須能夠知道多個元素中哪個元素具有鍵盤焦點。 如果螢幕上只有一個鍵盤可操作的控制項，則會符合成功標準，因為視覺設計只顯示一個鍵盤可操作的項目。

當成功標準顯示「操作模式」時，這是為了說明不一定總是顯示焦點指標的平台。 在大多數情況下，只有一種操作模式，因此會套用此成功准則。

#### 如何開會——焦點可見(2.4.7) {#how-to-meet-focus-visible}

請遵循「如 [何符合成功標準2.4.7」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)。

#### 詳細資訊——可見焦點(2.4.7) {#more-information-focus-visible}

* [瞭解成功標準2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [如何符合成功標準2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## 原則3: 可理解 {#principle-understandable}

[原則3: 可理解——資訊和用戶介面的操作必須可理解。](https://www.w3.org/TR/WCAG/#understandable)

### 讓文字內容可讀且可理解(3.1) {#make-text-content-readable-and-understandable}

[准則3.1可讀： 讓文字內容可讀且易於理解。](https://www.w3.org/TR/WCAG/#readable)

### 頁面語言(3.1.1) {#language-of-page}

* 成功標準3.1.1
* A級
* 頁面語言： 每個網頁的預設人文語言可依程式設計決定。

#### 用途——頁面語言(3.1.1) {#purpose-language-of-page}

此成功標準的目的是確保文字和其他語言內容正確呈現。 對於螢幕閱讀器使用者，這可確保內容正確發音，而視覺瀏覽器更可能正確顯示特定字元集。

#### How to Meet - Language of Page(3.1.1) {#how-to-meet-language-of-page}

為符合此成功標準，可使用頁面頂端的元素內 `lang` 的屬性來 `<html>` 識別網頁的預設語言。 例如：

* 如果頁面以英文寫入，元 `<html>` 素應為：
   `<html lang = “en”>`

* 而以西班牙文轉譯的頁面，則應採用下列標準：
   `<html lang = “es”>`

在AEM中，您的頁面預設語言是在建立頁面時設定，但在編輯「頁面屬性」時也可 [以變更](/help/sites-authoring/editing-page-properties.md)。

>[!NOTE]
>
>AEM可進一步微調根語言的變化； 例如，美國英語- en-us、英語- en-gb和加拿大英語- en-ca。 對於輔助技術而言，這種詳細程度通常是多餘的，不過可用於頁面內容的區域變化。

#### 詳細資訊——頁面語言(3.1.1) {#more-information-language-of-page}

* [瞭解成功標準3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [如何符合成功標準3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* 代碼基於ISO 639-1。 W3 Schools網站提供更詳盡的每種語言程式碼清 [單](https://www.w3schools.com/tags/ref_language_codes.asp)。

### 部件語言(3.1.2)  {#language-of-parts}

* 成功標準3.1.2
* AA級
* 部件語言： 除了正確的名稱、技術術語、不確定語言的字詞和已成為立即周圍文本的白話部分的字詞或短語外，內容中每個段落或短語的人文語言可以寫程式確定。

#### 用途——部件語言(3.1.2) {#purpose-language-of-parts}

此成功准則的目的與「頁面語言」的成功准則類似，但適用於單一頁面上包含多種語言內容的網頁（例如，由於引文或不常見的借記字詞）。 [](#language-of-page)

套用此成功准則的頁面允許：

* 盲文轉換軟體以插入帶重音字元。
* 螢幕閱讀程式可讀出那些具有特殊字元的字詞，或不是在頁面層級識別的預設語言。
* 翻譯工具（例如Google Translate），可將內容從一種語言正確翻譯為另一種語言。

#### How to Meet - Language of Parts(3.1.2) {#how-to-meet-language-of-parts}

該 `lang` 屬性可用來識別內容語言的變更。 例如，德文引號（ISO 639-1代碼&quot;de&quot;）如下所示：

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>現成可用的實例不支援區塊引號。 可開發自訂元件以支援此功能。

同樣地，如果元素的使用方式如下，瀏覽器也可以正確呈現不常見 `span` 的借記字詞或片語：

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>在包含不同語言的名稱或城市，或在使用預設語言中已司空見慣的借詞或片語(例如英文中的 *幸災樂禍* )時，不必遵循此成功標準。

要使用適當的語言添加span元素，可以在RTE的源編輯模式中手動編輯HTML標籤，以便其讀取如上。 或者， `lang` 系統管理員可將屬性包含在RTE中(請參 [閱Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes))。

#### 詳細資訊——部件語言(3.1.2) {#more-information-language-of-parts}

* [瞭解成功標準3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [如何符合成功標準3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### 可預測(3.2) {#predictable}

[准則3.2可預測： 讓網頁以可預測的方式顯示和運作。](https://www.w3.org/TR/WCAG/#predictable)

這就是要確保網頁的外觀和運作方式一致。

### 焦點(3.2.1)  {#on-focus}

* 成功標準3.2.1
* A級
* 焦點： 當任何使用者介面元件收到焦點時，它不會起始內容變更。

#### 目的——重點(3.2.1) {#purpose-on-focus}

此成功標準的目的是確保在訪客瀏覽檔案時，功能可預測。 任何在接收焦點時能夠觸發事件的元件，都不得變更內容。 元件接收焦點時更改上下文的示例包括，但不限於：

* 元件獲得焦點時自動提交的表單；
* 當元件收到焦點時，就會啟動新視窗；
* 當該元件接收焦點時，焦點會變更為另一個元件；

焦點可以通過鍵盤（例如與控制項對開）或滑鼠（例如在文本欄位上按一下）移動到控制項。 將滑鼠移至控制項上時，除非指令碼實作此行為，否則不會移動焦點。 請注意，對於某些類型的控制項，按一下控制項也可能會啟動控制項（例如按鈕），而此控制項可能會啟動內容變更。

#### 如何開會——焦點(3.2.1) {#how-to-meet-on-focus}

請遵循「如 [何符合成功准則3.2.1」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)。

#### 更多資訊——焦點(3.2.1) {#more-information-on-focus}

* [瞭解成功標準3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [如何符合成功標準3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### 輸入(3.2.2)  {#on-input}

* 成功標準3.2.2
* A級
* 輸入時： 變更任何使用者介面元件的設定並不會自動造成內容變更，除非使用者在使用元件之前已被告知該行為。

#### 用途——輸入(3.2.2) {#purpose-on-input}

本「成功准則」的目的是確保輸入資料或選取表單控制項具有可預測的效果。 變更任何使用者介面元件的設定，會變更控制項中在使用者不再與其互動時會持續存在的某些方面。 因此，勾選核取方塊、在文字欄位中輸入文字或變更清單控制項中選取的選項會變更其設定，但啟動連結或按鈕則不會變更。 情境的變更會迷惑不解的使用者，讓他們不容易察覺變更，或容易被變更分心。 只有當使用者的動作顯然會發生這類變更時，才適合變更內容。

#### 如何符合——輸入時(3.2.2) {#how-to-meet-on-input}

請遵循「如 [何符合成功准則3.2.2」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#on-input)。

#### 詳細資訊——輸入(3.2.2) {#more-information-on-input}

* [瞭解成功標準3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [如何符合成功標準3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### 一致導覽(3.2.3)  {#consistent-navigation}

* 成功標準3.2.3
* AA級
* 一致導覽： 在一組網頁內的多個網頁上重複的導覽機制，在每次重複時都以相同的相對順序發生，除非使用者啟動變更。

#### 用途——一致導覽(3.2.3) {#purpose-consistent-navigation}

本「成功准則」旨在鼓勵使用者在一組網頁內與重複內容互動且需要多次找出特定資訊或功能的情況下，使用一致的簡報和版面。 低視覺的個人使用螢幕放大率，一次顯示螢幕的一小部分時，通常會使用視覺提示和頁面邊界來快速找出重複的內容。 對於視覺使用者而言，以相同順序呈現重複內容也很重要，因為視覺使用者在設計中使用空間記憶體或視覺提示來定位重複內容。

請務必注意，本節中使用「相同順序」一詞並非暗示無法使用子導覽功能表，或無法使用次導覽或頁面結構區塊。 相反地，此成功准則旨在協助使用者透過網頁與重複內容互動，以預測所尋找內容的位置，並在再次遇到時更快速找到。

用戶可以通過使用自適應用戶代理或通過設定首選項來啟動按順序的更改，以便以對他們最有用的方式呈現資訊。

#### 如何開會——一致導覽(3.2.3) {#how-to-meet-consistent-navigation}

請遵循「如 [何符合成功准則3.2.3」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)。

#### 詳細資訊——一致導覽(3.2.3) {#more-information-consistent-navigation}

* [瞭解成功標準3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [如何符合成功標準3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### 一致識別(3.2.4)  {#consistent-identification}

* 成功標準3.2.4
* A級
* 一致的識別： 在一組網頁中具有相同功能的元件會一致識別。

#### 用途——一致識別(3.2.4) {#purpose-consistent-identification}

本「成功准則」的目的，在於確保一致識別在一組網頁中重複出現的功能元件。 使用螢幕閱讀程式的使用者在操作網站時採用的策略，是高度依賴使用者熟悉可能出現在不同網頁的功能。 如果相同的功能在不同的網頁上有不同的標籤（或更一般地說，是不同的可存取名稱），則網站的使用難度會大大增加。 這也可能令人困惑，並增加了對認知有限的人的認知負荷。 因此，一致的標籤將有所幫助。

這種一致性延伸到了文本替代項。 如果圖示或其他非文字項目具有相同的功能，則其文字替代項目也應保持一致。

如果網頁上有兩個元件，其功能都與一組網頁中其他頁面上的元件相同，則這3個元件必須保持一致。 因此，同一頁上的兩者將保持一致。

雖然在單一網頁內始終保持一致是最理想且最佳的作法，但3.2.4隻解決一組網頁內的一致性問題，而該組網頁中的多個網頁會重複某些內容。

#### 如何滿足——一致的標識(3.2.4) {#how-to-meet-consistent-identification}

請遵循「如 [何符合成功准則3.2.4」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)。

#### 更多資訊——一致識別(3.2.4) {#more-information-consistent-identification}

* [瞭解成功標準3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [如何符合成功標準3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### 輸入協助(3.3) {#input-assistance}

[准則3.3投入援助： 協助使用者避免並修正錯誤。](https://www.w3.org/TR/WCAG/#input-assistance)

### 錯誤識別(3.3.1)  {#error-identification}

* 成功標準3.3.1
* A級
* 錯誤標識： 如果自動檢測到輸入錯誤，則識別出錯誤的項目，並以文本向用戶說明錯誤。

#### 用途——錯誤識別(3.3.1) {#purpose-error-identification}

本成功准則的目的是確保使用者知道發生錯誤，並可判斷錯誤的內容。 錯誤訊息應盡可能具體。 如果表單提交失敗，重新顯示表單並指出有錯誤的欄位不足以讓部分使用者察覺到發生錯誤。 例如，螢幕閱讀程式使用者在遇到其中一個指示器之前，不會知道有錯誤。 他們可能會在遇到錯誤指示器之前完全放棄表單，認為頁面無法運作。 根據WCAG中的定義，輸 [入錯誤](https://www.w3.org/TR/WCAG/#dfn-input-error) ，是由用戶提供的未接受的資訊。 這包括：

網頁要求但使用者省略的資訊，或使用者提供但不符合要求資料格式或允許值的資訊。
例如：

* 用戶未能在州、省、地區等地輸入正確的縮寫。 欄位;
* 用戶輸入非有效狀態的狀態縮寫；
* 用戶輸入的郵遞區號不存在；
* 用戶在未來2年內進入出生日期；
* 用戶在只接受數字的電話號碼欄位中輸入字母或括弧；
* 使用者輸入低於先前出價或最低出價增量的出價。

#### 如何符合——錯誤識別(3.3.1) {#how-to-meet-error-identification}

請遵循「如 [何符合成功准則3.3.1」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)。

#### 詳細資訊——錯誤識別(3.3.1) {#more-information-error-identification}

* [瞭解成功標準3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [如何符合成功標準3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### 標籤或指示(3.3.2) {#labels-or-instructions}

* 成功標準3.3.2
* A級
* 標籤或指示： 當內容需要使用者輸入時，會提供標籤或指示。

#### 用途——標籤或說明(3.3.2) {#purpose-labels-or-instructions}

提供說明以協助人們填寫表單是介面可用性的基本實務。 這樣做對於視覺或認知障礙的人特別有幫助，因為如果不是這樣，他們可能難以理解表單的佈局以及在特定表單域中提供的資料類型。

##### 表單

在AEM WKND展示專案中，當您將表單元件（例如文字欄位）新增至頁面時，會新增預設標籤。 ****&#x200B;此預設標題取決於元件類型，您可以在該欄位的編輯對話框的「標題」( **Title)和「文本」(Text** )頁籤中添加自己的標題。 請務必確保標籤有助於使用者瞭解與每個表單元件相關聯的資料。

此「 **標題** 」欄位必須用於欄位元素，因為它提供可用於輔助技術的標籤。 僅僅在欄位旁的文字中加上標籤是不夠的。

對於某些表單元件，您也可以使用「隱藏標題」核取方塊以視覺化方式 **隱藏標籤** 。以此方式隱藏的標籤仍適用於輔助技術，但無法顯示在螢幕上。雖然這在某些情況下是個好方法，但通常最好盡可能加入視覺標籤，因為有些使用者可能會看到畫面的一小部分 (一次看一個欄位)，並需要標籤來正確識別欄位。

###### 影像按鈕 {#image-buttons}

Where image buttons are used (for example, the **Image Button** component of the WKND project) the **Title** field in the **Title and Text** tab of the edit dialog actually provides the alt text for the image, rather than the label. 因此，在以下範例中，包含文字的影像 `Submit` 的alt文字為 `Submit`，使用編輯對話方塊中的 **Title** 欄位新增。

###### 表單欄位群組 {#groups-of-form-fields}

In the WKND project, where there is a group of related controls, such as **Radio Group**, a title may be needed for the group, as well as individual controls. 在AEM中新增一組選項按鈕時，「標題 **」欄位會提供此群組標題，而個別標題會指定為選項按鈕(** Items ****)。

不過，群組標題和選項按鈕本身之間沒有程式化關聯。範本編輯人員必須將標題包住必要 `fieldset` 和 `legend` 標籤，才能建立此關聯，而這只能透過編輯頁面原始碼來完成。Alternatively, a system administrator can add support for these elements so that they appear in the **Field Properties** dialog (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

###### 表單的其他考量事項 {#additional-considerations-for-forms}

如果要以特定格式輸入資料，請在標籤文本中明確說明這一點。 例如，如果必須以格式輸入日期，請特 `DD-MM-YYYY` 別指出這是標籤的一部分。 這表示當螢幕閱讀程式使用者遇到欄位時，標籤會自動宣佈，以及格式的其他資訊。

如果表單欄位的輸入是必填的，請使用標籤中的必要字詞來清楚說明。AEM在需要欄位時新增星號，但最好將字詞加入標 `required`簽本身(在編輯對話方塊的「 **Title** 」欄位中)。

標籤的定位也很重要，因為它可協助標籤找到適當的欄位。 當使用者面對複雜的表單時，這尤其重要。 遵守以下公約：

* 核取方塊或選項按鈕：
標籤會立即置於欄位右側。
* 所有其他表單元件（例如文字方塊、組合方塊）:
標籤會立即置於欄位的上方或左側。

在功能非常有限的簡單表單中，適當標 `Submit` 記按鈕可當成相鄰欄位的標籤(例如 `Search`)。 在尋找標籤文字的空間可能比較困難的情況下，此功能很實用。

#### 詳細資訊——標籤或指示(3.3.2) {#more-information-labels-or-instructions}

* [瞭解成功標準3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [如何符合成功標準3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### 錯誤建議(3.3.3)  {#error-suggestion}

* 成功標準3.3.3
* AA級
* 鍵盤： 如果自動檢測到輸入錯誤並且已知要更正的建議，則向用戶提供建議，除非該建議會危及內容的安全性或目的。

#### 目的——錯誤建議(3.3.3) {#purpose-error-suggestion}

本「成功准則」的目的，在於確保使用者在可能的情況下收到適當的建議，以修正輸入錯誤。 輸入錯誤的WCAG [定義](https://www.w3.org/TR/WCAG/#dfn-input-error) ，表示系統「不接受用戶提供的資訊」。 未被接受的資訊的一些示例包括用戶需要但省略的資訊以及用戶提供但不屬於所需資料格式或允許值的資訊。

成功准則3.3.1提供錯誤通知。 然而，認知有限的人可能很難理解如何糾正錯誤。 視覺殘障人士可能無法確切瞭解如何修正錯誤。 如果提交表單失敗，使用者可能會放棄表單，因為他們可能不確定如何更正錯誤，即使他們知道錯誤已發生。

內容作者可以提供錯誤的描述，或者用戶代理可以根據特定於技術的、以寫程式方式確定的資訊提供錯誤的描述。

#### 如何符合——錯誤建議(3.3.3) {#how-to-meet-error-suggestion}

請遵循「如 [何符合成功准則3.3.3」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)。

#### 詳細資訊——錯誤建議(3.3.3) {#more-information-error-suggestion}

* [瞭解成功標準3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [如何符合成功標準3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### 錯誤預防（法律、財務、資料）(3.3.4)  {#error-prevention-legal-financial-data}

* 成功標準3.3.4
* AA級
* 錯誤預防（法律、財務、資料）: 對於導致用戶發生法律承諾或財務交易、修改或刪除資料儲存系統中用戶可控制資料或提交用戶測試響應的網頁，至少以下情況之一是正確的：

   * 可逆提交是可逆的。
   * 檢查用戶輸入的CheckedData是否有輸入錯誤，並為用戶提供糾正錯誤的機會。
   * ConfirmedA機制可用於在提交定稿之前審查、確認和更正資訊。

#### 目的——錯誤預防（法律、財務、資料）(3.3.4) {#purpose-error-prevention-legal-financial-data}

本「成功准則」的目的是協助殘障人士避免在執行無法反轉的動作時，因為發生錯誤而造成嚴重後果。 例如，購買不可退還的機票或提交訂單以在經紀帳戶中購買股票，是具有嚴重後果的財務交易。 如果使用者在航空旅行日期犯了錯誤，他／她最終可能會得到一張無法交換的錯日機票。 如果使用者在要購買的股票數量上發生錯誤，他或她最終可能會購買比預期更多的股票。 這兩種錯誤都涉及立即發生且事後無法更改的事務，而且代價非常高昂。 同樣地，如果用戶無意中修改或刪除了儲存在資料庫中的資料（如旅行服務網站中的整個旅行配置檔案），則可能是一個不可恢復的錯誤。 當提及修改或刪除「用戶可控」資料時，其目的是防止大量丟失資料，如刪除檔案或記錄。 不是為了要求確認每個保存命令，或是建立或編輯文檔、記錄或其他資料。

殘障人士更可能犯錯。 閱讀障礙者可以轉寄數字和信件，而機動障礙者可以誤按鍵。 提供反向動作的功能可讓使用者修正可能導致嚴重後果的錯誤。 提供檢閱和修正資訊的能力，讓使用者有機會在採取具有嚴重後果的動作之前，先偵測錯誤。

用戶可控資料是用戶可觀察的資料，用戶可以通過故意操作來更改和／或刪除。 控制此類資料的用戶的例子包括更新用戶帳戶的電話號碼和地址，或從網站上刪除過去發票的記錄。 它不指使用者無法直接檢視或互動的網際網路記錄檔和搜尋引擎監控資料。

#### 如何滿足——錯誤預防（法律、財務、資料）(3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

請遵循「如 [何符合成功准則3.3.4」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)。

#### 詳細資訊——錯誤預防（法律、財務、資料）(3.3.4) {#more-information-error-prevention-legal-financial-data}

* [瞭解成功標準3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [如何符合成功標準3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## 原則4: 強穩 {#principle-robust}

[原則4: 強穩——內容必須足夠強穩，以供各種使用者代理程式（包括輔助技術）解讀。](https://www.w3.org/TR/WCAG/#robust)

### 相容(4.1) {#compatible}

[准則4.1相容： 將與目前和未來使用者代理程式的相容性提升到最大，包括輔助技術。](https://www.w3.org/TR/WCAG/#compatible)

將與目前和未來使用者代理程式的相容性提升到最大，包括輔助技術。

### 剖析(4.1.1)  {#parsing}

* 成功標準4.1.1
* A級
* 剖析： 在使用標籤語言實施的內容中，元素具有完整的開始和結束標籤，元素根據其規範進行巢狀化，元素不包含重複屬性，而且除了規範允許這些功能外，所有ID都是唯一的。

#### 用途——剖析(4.1.1) {#purpose-parsing}

本「成功准則」的目的在於確保使用者代理（包括輔助技術）能夠正確解譯和剖析內容。 如果無法將內容解析為資料結構，則不同的用戶代理可能以不同的方式呈現內容，或完全無法解析內容。 有些使用者代理會使用「修復技術」來產生編碼不良的內容。

由於修復技術在各用戶代理之間各不相同，因此作者不能假設內容將被精確解析為資料結構，或者內容將被包括輔助技術在內的專業用戶代理正確呈現，除非內容是根據該技術的正式語法中定義的規則建立的。 在標籤語言中，元素和屬性語法中的錯誤以及未能提供正確巢狀的開始／結束標籤會導致錯誤，使用者代理無法可靠地剖析內容。 因此，成功准則要求僅使用形式語法的規則來剖析內容。

#### 如何符合——剖析(4.1.1) {#how-to-meet-parsing}

請遵循「如 [何符合成功標準4.1.1」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#parsing)。

#### 詳細資訊——剖析(4.1.1) {#more-information-parsing}

* [瞭解成功標準4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [如何符合成功標準4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### 名稱、角色、值(4.1.2)  {#name-role-value}

* 成功標準4.1.2
* A級
* 名稱、角色、值： 對於所有用戶介面元件(包括但不限於： 表單元素、連結和指令碼生成的元件)，可以通過寫程式方式確定名稱和角色； 用戶可以設定的狀態、屬性和值可以通過寫程式方式設定； 使用者代理可取得這些項目變更的通知，包括輔助技術。

#### 用途——名稱、角色、值(4.1.2) {#purpose-ame-role-value}

本「成功准則」的目的是確保「輔助技術」(AT)可收集、啟用（或設定）內容中使用者介面控制項的狀態，並隨時掌握最新資訊。

當使用可存取技術的標準控制時，此程式就十分簡單。 如果用戶介面元素根據規格使用，則滿足此設定的條件。 （請參閱下方的成功准則4.1.2範例）

但是，如果建立了自定義控制項，或者將介面元素寫程式（在代碼或指令碼中）以具有與通常不同的角色和／或功能，則需要採取額外措施，以確保控制項向輔助技術提供重要資訊並允許輔助技術控制它們。

用戶介面控制項的一個特別重要的狀態是是否具有焦點。 可以寫程式地確定控制的焦點狀態，並且將關於焦點改變的通知發送給用戶代理和輔助技術。 用戶介面控制狀態的其他示例包括是否選中了複選框或單選按鈕，或是展開或折疊可折疊的樹或清單節點。

#### 如何符合——名稱、角色、值(4.1.2) {#how-to-meet-ame-role-value}

請遵循「如 [何符合成功標準4.1.2」下的准則](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)。

#### 詳細資訊——名稱、角色、值(4.1.2) {#more-information-ame-role-value}

* [瞭解成功標準4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [如何符合成功標準4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
