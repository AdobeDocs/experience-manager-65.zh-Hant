---
title: 建立Adobe Experience Manager的無障礙內容（符合WCAG 2.1）
description: 使用AEM協助讓身心障礙人士可存取及使用網頁內容
exl-id: 2145d761-f51d-482b-a0e7-ef7500c4872f
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '13950'
ht-degree: 4%

---

# 建立可存取的內容 (符合 WCAG 2.1) {#creating-accessible-content-wcag-conformance}

此 [網頁內容可及性指引(WCAG)2.1](https://www.w3.org/TR/WCAG/)，由 [萬維網聯盟的一個工作組](https://www.w3.org/Consortium/activities#Accessibility_Guidelines_Working_Group)，包含一套與技術無關的指引和成功標準，可協助身心障礙人士存取及使用網路內容。

作為介紹，該聯合會提供了一系列章節和支援檔案：

* [WCAG 2.1的新功能](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [How to Meet WCAG 2.1 (如何達成 WCAG 2.1) ](https://www.w3.org/WAI/WCAG21/quickref/)
* [Understanding WCAG 2.1 (了解 WCAG 2.1) ](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Techniques for WCAG 2.1 (WCAG 2.1 的專用技術) ](https://www.w3.org/WAI/WCAG21/Techniques/)
* [WCAG檔案](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

此外，請參閱：
* 我們的 [WCAG 2.1快速指南](/help/managing/qg-wcag.md).
* 此 [Adobe解決方案的協助工具合規報告](https://www.adobe.com/accessibility/compliance.html).
* [設定RTF編輯器以產生無障礙內容](/help/sites-administering/rte-accessible-content.md)

指南分為三個符合級別：A級（最低）、AA級和AAA級（最高）。 簡要地說，這些級別的定義如下：

* **** A級：您的網站達到基本的最低協助功能等級。要達到此級別，將滿足所有A級成功標準。
* **AA級：** 這是您努力追求的理想無障礙環境等級，其中您的網站可達到基本無障礙環境等級，因此大部分使用者都能使用大部分技術來存取。 要達到此級別，將滿足所有A級和A級成功標準。
* **** AAA級：您的網站可達到非常高的協助功能。要達到此級別，將滿足所有A級、AA級和AAA級成功標準。

建立網站時，您必須決定要讓網站遵循的整體等級。

以下部分介紹 [WCAG 2.1指引的層](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) 與A級和AA級的相關成功標準 [合格級別](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1).

>[!NOTE]
>
>在本檔案中，我們使用：
>
>* 此 [WCAG 2.1指引的簡短名稱](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* 此 [WCAG 2.1指引中使用的編號](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) 以輔助與WCAG網站的交叉參照。


## 原則1:可感知 {#principle-perceivable}

[原則1:可感知(Perceivable) — 資訊和用戶介面元件必須以用戶能夠感知的方式顯示給用戶。](https://www.w3.org/TR/WCAG/#perceivable)

### 替代文字(1.1) {#text-alternatives}

[准則1.1文本替代：為任何非文字內容提供替代文字的內容，以便將其變更為人們需要的其他形式，例如大型印刷品、盲文、語音、符號或更簡單的語言。](https://www.w3.org/TR/WCAG/#text-alternatives)

### 非文字內容(1.1.1) {#non-text-content}

* 成功標準1.1.1
* A級
* 非文字內容：呈現給使用者的所有非文字內容都有可達到同等目的的替代文字，但下列情形除外。

#### 用途 — 非文字內容(1.1.1) {#purpose-non-text-content}

網頁上的資訊可以以許多不同的非文本格式提供，如圖片、視頻、動畫、圖表和圖形。 盲人或視力嚴重受損的人無法看到非文本內容，但他們可以通過螢幕閱讀器讀取文本內容或通過盲文顯示設備以觸覺形式顯示文本內容來訪問文本內容。 因此，通過以圖形格式提供內容的文本替代項，看不到圖形內容的人可以訪問內容提供的資訊的同等版本。

另一個有用的好處是，文本替代項使得非文本內容能夠根據搜索引擎技術編製索引。

#### 如何達成 — 非文字內容(1.1.1) {#how-to-meet-non-text-content}

對於靜態圖形，基本要求是為圖形提供等效文本替代。 您可以在 **替代文字** 欄位；如需核心元件的相關資訊，請參閱 **[影像](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)**.

>[!NOTE]
>
>部分現成可用的核心元件，例如 **[輪播](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/carousel.html)** 不提供 **替代文字** 欄位，將替代文字說明新增至個別影像，但有 **標籤** 欄位()**[協助工具](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/carousel.html#accessibility-tab)** 標籤)，以取得Advertising Cloud的說明。
>
>當針對您的AEM例項實作這些版本時，您的開發團隊將需要設定這些元件以支援 `alt` 屬性，讓作者可將其新增至內容(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

AEM需要 **替代文字** 欄位以預設填入。 如果影像純粹是裝飾性的，而替代文字是不必要的， **影像是裝飾** 選項。

#### 建立良好的文字替代項目 {#creating-good-text-alternatives}

非文字內容有多種形式，因此替代文字的值取決於圖形在網頁中扮演的角色。 以下是一些一般經驗法則：

* 替代案文應簡明扼要，但應清楚掌握非文本內容提供的基本資訊。
* 應避免過長的說明（超過100個字元）。 如果替代文字需要更詳細的資訊：
   * 在替代文字中提供簡短說明
   * 和在相同頁面或個別網頁其他地方的文字中有較長的說明。 將影像設為連結，或將文字連結放置在影像旁，以連結至此個別說明。
* 替代文字不應複製相同頁面附近文字表單中提供的內容。 請記住，許多影像都是頁面文字中已涵蓋點的圖解，因此可能已存在詳細的文字替代項目。
* 如果非文本內容是指向其他頁面或文檔的連結，並且沒有其他文本構成同一連結的一部分，則影像的替代文本必須指示連結的目的地，而不是描述影像。
* 如果非文字內容包含在按鈕元素中，並且沒有構成相同按鈕一部分的文字，則影像的替代文字必須指示按鈕的功能，而不是描述影像。
* 為影像指定空白(null)替代文字是完全可接受的，但前提是影像不需要替代文字（例如，純粹是裝飾圖形），或頁面文字中已存在相等文字。

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

需要替代文字的特定非文字內容類型可能包括：

* 說明性照片：這些是人、物體或地方的影像。 請務必思考像片在頁面中的角色，並且一般建議說明影像內容，因為輔助技術會宣佈元素類型(例如， `graphic` 或 `image`);可提高使用的清晰度 `screenshot` 或 `illustration` 在替代文字說明中，但這取決於內容。 一致性是重要因素，應為整個製作團隊做出決策，並套用至整個使用者體驗。
* 表徵圖：這些是傳送特定資訊的小型像形圖（圖形）。 必須在頁面和網站間一致地使用。 頁面或網站上的圖示所有例項都應有相同的簡短文字替代項目，除非這麼做會造成相鄰文字的不必要重複。
* 圖表和圖形：這些通常代表數值資料。 因此，提供文本替代的一個選項可能是包含圖表或圖形中顯示的主要趨勢的簡要摘要。 如有必要，也可使用 **說明** 欄位 **進階** 「影像屬性」頁簽。 此外，您可以在頁面或網站其他地方以表格形式提供來源資料。
* 地圖、圖表、流程圖：對於提供空間資料的圖形（例如，用於支援描述對象或進程之間的關係），請確保以文本格式提供密鑰消息，並且此文本資訊位於每個關聯資料點附近。 對於地圖，提供等同全文的地圖可能不切實際，但如果提供地圖以幫助人們找到特定位置的方式，則地圖影像的替代文字可以簡短地標示 *X*，然後在頁面其他地方的文字或透過 **Image元件的「** Advanced **」 (進階) 索引標籤中的「** Description **** 」 (說明) 欄位，提供指向該位置的指示。
* 驗證碼：驗證碼是 *完全自動化的公共圖靈測試*. 這是一種用於網頁上的安全檢查，用於區分人類和惡意軟體，但可能造成無障礙障礙。 這些影像需要使用者描述他們看到的內容，才能通過安全性測試。 顯然無法為影像提供替代文字，因此您需要考慮替代的非圖形解決方案。 W3C提供了一些建議，例如：每種方法都有各自的優點和缺點。
   * 邏輯拼圖
   * 使用聲音輸出而非影像
   * 有限使用帳戶和垃圾郵件篩選器。
* 背景影像：這些是使用階層式樣式表(CSS)而非HTML來達成。 這表示無法指定替代文字值。 因此，背景影像不應提供重要的文字資訊 — 如果提供了，這些資訊也必須在頁面的文字中提供。 但是，當無法顯示影像時，必須顯示替代背景。

>[!NOTE]
>
>背景文字與前景文字之間應有適當的對比度；詳細討論 [對比度（最低）(1.4.3)](#contrast-minimum).

#### 詳細資訊 — 非文字內容(1.1.1) {#more-information-non-text-content}

* [了解成功標準1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [如何符合成功標準1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [驗證碼的W3C說明和替代方案](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### 時間型媒體(1.2) {#time-based-media}

[准則1.2以時間為基礎的媒體：提供以時間為基礎的媒體的替代方案。](https://www.w3.org/TR/WCAG/#time-based-media)

這涉及 *時間型*. 這涵蓋使用者可播放的內容（例如視訊、音訊和動畫內容），且可以預先錄制或即時資料流。

### 僅限音訊和僅限視訊（預錄）(1.2.1) {#audio-only-and-video-only-prerecorded}

* 成功標準1.2.1
* A級
* 僅限音訊和僅限視訊（預錄）:對於預錄的純音頻和預錄的純視頻媒體，以下是真的，但音頻或視頻是文本的替代媒體且明確標籤為這樣的媒體除外：
   * 僅預錄音頻：提供了用於基於時間的媒體的替代，該替代提供用於預錄的僅音頻內容的等效資訊。
   * 僅預錄視頻：提供了用於基於時間的媒體的替代媒體或音頻軌道，該音頻軌道為預錄的僅視頻內容呈現等同資訊。

#### 用途 — 僅限音訊和僅限視訊（預錄）(1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

視訊和音訊的協助工具問題可能會發生：

* 沒有音軌或音軌時，視覺受損的人無法告知影片或動畫中發生的情況；
* 聽力受損或失聰的人，聽不到音軌；
* 那些能聽到背景音樂，但不理解人們說什麼的人（例如，因為他們所說的語言是他們不懂的）。

使用不支援以特定媒體格式播放內容(例如AdobeFlash)的瀏覽器或裝置的使用者，也可能無法使用視訊或音訊。

以不同格式提供此資訊，例如文字（或無音訊的視訊音訊），可讓無法存取原始內容的使用者存取。

#### 如何達成 — 僅限音訊和僅限視訊（預錄）(1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* 如果內容預錄的音訊沒有視訊（例如播客）:
   * 在內容之前或之後立即提供連結至音訊內容的文字記錄。 文字記錄應是HTML頁面，其文字等同於所有口語和非口語重要內容，還應包含說話者的指示、設定的描述、聲音表達以及任何其他重要音頻的描述。
* 如果內容是動畫或預錄的無音頻視頻：
   * 在內容之前或之後，提供連結給視訊所提供資訊的同等文字說明
   * 或MP3等常用音訊格式的等效音訊說明。

>[!NOTE]
>
>如果提供音頻或視頻內容作為已存在於相同網頁上的另一種格式內容的替代內容，則可能不需要另外的替代內容。
>
>准則， [了解WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)，請提供詳細資訊。

在AEM網頁中插入多媒體與插入影像類似。 然而，由於多媒體內容遠不止是靜止的影像，所以在控制多媒體的播放方式方面存在多種不同的設定和選項。

>[!NOTE]
>
>當您將多媒體與資訊內容搭配使用時，您還必須建立替代內容的連結。 例如，要包括文本記錄，請建立一個HTML頁以顯示該記錄，然後在音頻內容旁或下面添加一個連結。

#### 詳細資訊 — 僅限音訊和僅限視訊（預錄）(1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [了解成功標準1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [如何符合成功標準1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### 字幕（預錄）(1.2.2) {#captions-prerecorded}

* 成功標準1.2.2
* A級
* 字幕（預錄）:為同步媒體中所有預錄音頻內容提供字幕，除非該媒體是文本的媒體替代品，並且清楚地標籤為這樣。

#### 用途 — 字幕（預錄）(1.2.2) {#purpose-captions-prerecorded}

失聰或聽力障礙的人無法或很難存取音訊內容。 字幕是口語和非口語音頻的等效文本，在視頻中的適當時間顯示在螢幕上。 它們讓聽不到音訊的人了解正在發生的情況。

#### 如何符合 — 字幕（預錄）(1.2.2) {#how-to-meet-captions-prerecorded}

字幕可以是：

* 開啟：播放視訊時一律顯示
* 已關閉：字幕可由用戶開啟或關閉

盡可能使用隱藏式字幕，因為這可讓使用者選擇是否檢視字幕。

對於隱藏式字幕，您需要以適當的格式建立並提供同步的字幕檔案(例如 [SMIL](https://www.w3.org/AudioVideo/))和影片檔案(有關如何執行此作業的詳細資訊，不在本指南的討論範圍內，但我們已提供下列教學課程的連結 [更多資訊 — 字幕（預錄）(1.2.2)](#more-information-captions-prerecorded). 請務必提供附註或啟用視訊播放器的註解功能，讓使用者知道視訊有可用的註解。

如果必須使用開啟字幕，請將文本嵌入視頻軌道。 這可以使用允許將標題覆蓋到視頻上的視頻編輯應用程式來實現。

#### 更多資訊 — 字幕（預錄）(1.2.2) {#more-information-captions-prerecorded}

* [了解成功標準1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [如何符合成功標準1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### 音訊說明或替代媒體（預錄）(1.2.3) {#audio-description-or-media-alternative-prerecorded}

* 成功標準1.2.3
* A級
* 音訊說明或替代媒體（預錄）:為同步媒體提供基於時間的媒體或音頻描述的預錄視頻內容的替代物，除非該媒體是文本的媒體替代物並且清楚地標籤為這樣。

#### 用途 — 音訊說明或替代媒體（預錄）(1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

如果僅以視覺方式提供視頻或動畫中的資訊，或如果音軌未提供足夠的資訊，以便了解視覺上正在發生的情況，盲人或視力障礙者將會遇到無障礙障礙。

#### 如何達成 — 音訊說明或替代媒體（預錄）(1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

有兩種方法可滿足此成功標準。 兩者皆可接受：

1. 包含視訊內容的其他音訊說明。 這可以通過以下三種方式之一實現：
   * 在現有對話方塊中暫停期間，提供場景中未作為現有音頻軌道一部分顯示的更改的相關資訊；
   * 提供新的、附加的和可選的音軌，其中包含原始音軌，但也包含有關場景更改的額外音頻資訊。
      * 這可讓使用者在現有的音訊軌道( *不* 包含音訊說明)和新的音訊軌道( *does* 包含音訊說明)。
      * 這可防止不需要額外說明的使用者中斷。
   * 建立視訊內容的第二版，以允許擴充音訊說明。 這可借由在適當點暫停音訊和視訊，減少在現有對話方塊之間的間隙內提供詳細音訊說明的相關困難。 因此，在動作再次開始之前，可以提供更長的音訊說明。 如上一個範例，最好以選用的額外音訊追蹤提供，以免中斷不需要其他說明的使用者。
1. 提供與視頻或動畫的音頻和視覺元素相當的適當文本文本記錄。 這應當包括，在適當情況下，指示說話的人、設定的說明、視覺上呈現的任何事件或資訊，以及聲音表達。 視其長度而定，可以將記錄放在與視頻或動畫相同的頁面上，或放在單獨的頁面上；如果選擇後一個選項，請提供視頻或動畫旁邊的轉錄的連結。

有關如何建立音訊描述視訊的確切詳細資訊，不在本指南的討論範圍內。 建立視訊和音訊說明可能很耗時，但其他Adobe產品可協助您完成這些工作。

#### 詳細資訊 — 音訊說明或替代媒體（預錄）(1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [了解成功標準1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [如何符合成功標準1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### 字幕（正常）(1.2.4)  {#captions-live}

* 成功標準1.2.4
* AA級
* 字幕（即時）:為同步媒體中的所有即時音頻內容提供字幕。

#### 用途 — 字幕（正式啟用）(1.2.4) {#purpose-captions-live}

此成功標準與 [字幕（預錄）](#captions-prerecorded) 它解決了聾人或聽力障礙者所遇到的無障礙障礙障礙，但此成功標準涉及即時演示，如網播。

#### 如何符合 — 字幕（正式啟用）(1.2.4) {#how-to-meet-captions-live}

遵循 [字幕（預錄）](#captions-prerecorded) 上。 但是，由於媒體的即時性，必須盡快建立字幕提供，以響應正在發生的情況。 因此，您應考慮使用即時字幕或語音轉文字工具。

本檔案不提供詳細說明，但下列資源提供實用資訊：

* [WebAIM:即時字幕](https://www.webaim.org/techniques/captions/realtime.php)

* [AccessComputing項目（華盛頓大學）:字幕是否可以使用語音識別自動生成？](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### 更多資訊 — 字幕（正式啟用）(1.2.4) {#more-information-captions-live}

* [了解成功標準1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [如何符合成功標準1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### 音訊說明（預錄）(1.2.5)  {#audio-description-prerecorded}

* 成功標準1.2.5
* AA級
* 音頻描述（預錄）:提供同步媒體中所有預錄視頻內容的音頻描述。

#### 用途 — 音訊說明（預錄）(1.2.5) {#purpose-audio-description-prerecorded}

此成功標準與 [音訊說明或替代媒體（預錄）](#audio-description-or-media-alternative-prerecorded)，但作者必須提供更詳細的音訊說明才能符合AA級。

#### 如何滿足 — 音頻說明（預錄）(1.2.5) {#how-to-meet-audio-description-prerecorded}

遵循 [音訊說明或替代媒體（預錄）](#audio-description-or-media-alternative-prerecorded).

#### 詳細資訊 — 音訊說明（預錄）(1.2.5) {#more-information-audio-description-prerecorded}

* [了解成功標準1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [如何符合成功標準1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### 適應性(1.3) {#adaptable}

[准則1.3適應性：建立可以以不同方式呈現的內容（例如更簡單的版面），而不會遺失資訊或結構。](https://www.w3.org/TR/WCAG/#adaptable)

此指引涵蓋支援以下人員的必要需求：

* 可能無法存取作者在該內容的預設呈現中所呈現的資訊（例如多欄版面或大量使用顏色和/或影像的頁面）。

* 可使用純音，或替代的視覺顯示，例如大文字或高對比。

### 資訊和關係(1.3.1)  {#info-and-relationships}

* 成功標準1.3.1
* A級
* 資訊和關係：通過展示傳遞的資訊、結構和關係可以寫程式地確定或在文本中可用。

#### 用途 — 資訊和關係(1.3.1) {#purpose-info-and-relationships}

許多殘疾人使用的輔助技術依靠結構資訊來有效顯示或 *了解* 內容。 此結構資訊可以採用頁標題、表行和列標題及清單類型的形式。 例如，螢幕助讀程式可讓使用者從標題瀏覽至標題的頁面。 不過，當頁面內容看起來只是透過視覺樣式(而非基礎HTML)有結構時，輔助技術就無法使用結構資訊，限制了其支援更輕鬆瀏覽的能力。

此成功標準的存在，是為了確保以程式設計方式透過HTML或其他編碼技術提供此類結構資訊，讓瀏覽器和輔助技術能夠存取及利用這些資訊。

#### 如何達成 — 資訊和關係(1.3.1) {#how-to-meet-info-and-relationships}

AEM可讓您使用適當的HTML元素，輕鬆建構具語義意義的網頁內容。 在RTE中開啟頁面內容（文字元件），然後使用 **Paraformat** （段落符號），以指定適當的結構元素（例如段落、標題等）。

您可以視情況使用下列元素，確保網頁已獲得適當的結構：

* **標題：** 只要您已啟用RTE的協助工具功能，AEM就會提供3層頁面標題。 您可以使用這些項目來識別內容的區段和子區段。標題1是標題的最高級別，標題3是最低級別。系統管理員可以配置系統以允許使用更多標題級別。

* **清單**:您可以使用HTML來指定三種不同的清單類型：
   * 元素 `<ul>` 用於無序 *列*  (項目符號) 清單。使用元素來識別個別清 `<li>` 單項目。在RTE中，使用「項目符號列 **表」表徵圖** 。
   * 此 `<ol>` 元素用於 *編號* 清單。 個別清單項目的識別方式為 `<li>` 元素。 在RTE中，使用 **編號清單** 表徵圖。

   如果要將現有內容更改為特定清單類型，請突出顯示相應的文本並選擇相應的清單類型。 如先前顯示如何輸入段落文字的範例所示，適當的清單元素會自動新增至您的HTML。

   在全螢幕模式中，會顯示個別 **的「項目符號清單** 」和「 **** 編號清單」圖示。當未處於全螢幕模式時，單一「清單」圖示後面會提供這兩個 **選項** 。

* **表格**:必須使用HTML表元素來標識資料表：
   * one `<table>` 元素
   * a `<tr>` 表格每一列的元素
   * a `<th>` 元素
   * a `<td>` 元素

   此外，可訪問的表還使用以下元素和屬性：

   * 此 `<caption>` 元素可用來提供表格的可見標題。 字幕預設會出現在表格的正中，但可使用CSS適當定位。 註解以寫程式方式與表格相關聯，因此它是提供內容介紹的有用方法。
   * 此 `<summary>` 元素可協助無視的使用者提供視力不佳的使用者看得到的概要，以更輕鬆地了解表格中顯示的資訊。 若使用複雜或非常規的表格配置，此屬性特別實用（此屬性不會顯示在瀏覽器中，而只會讀出至輔助技術）。
   * 此 `scope` 屬性 `<th>` 元素用於指示儲存格代表特定列或特定欄的標題。 類似的方法是在複雜表格中使用標題和id屬性，其中資料儲存格可與一或多個標題相關聯。

   >[!NOTE]
   >
   >預設情況下，這些元素和屬性不直接可用，但系統管理員可以在 **表屬性** 對話框(請參見 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes).

   若要開啟 **表格** 對話方塊中選取 **表屬性** 標籤：

   * 定義適當 **註解**.
   * 理想情況下，請移除「寬 **度」、「邊框高度」、「邊框高度」、「邊框高度**」、「單元格間距」、「單元格間距 **」、「單元格**************&#x200B;間距」的預設值。因為這些屬性可以在全局樣式表中設定。

   然後，您就可以使用 **儲存格屬性** 若要選擇儲存格是資料儲存格還是標題儲存格：

* **強調**:使用 `<strong>` 或 `<em>` 指示強調的元素。 請勿使用標題來反白標示段落中的文字。
   * 突出顯示要強調的文本；
   * 按一下「屬性」面板中顯示的 **B** 表徵圖( `<strong>`for)或「屬性」面板中顯示 **的「I** 」表徵圖(for `<em>`)(請確定已選 **** 中HTML)。

      >[!NOTE]
      >
      >標準AEM安裝中的RTE已設定為使用：
      >
      >* `<b>` 代表 `<strong>`
      >* `<i>` 代表 `<em>`

      >
      >實際上是一樣的，但 `<strong>` 和 `<em>` 較好，因為它們在語義上正確。 您的開發團隊可以設定RTE以使用 `<strong>` 和 `<em>` (而非 `<b>` 和 `<i>`)，以開發您的專案例項。

* **複雜的資料表**:在某些情況下，如果有具有兩個或多個標題級別的複雜表，則基本表屬性可能不足以提供所有必要的結構資訊。對於這些類型的複雜表格，需要使用header和 **id屬性在標題及其相關儲存格之間建** 立直 **接** 關係。

   >[!NOTE]
   >
   >id屬性在現成可用的安裝中無法使用。 可透過在RTE中設定HTML規則和序列化程式來啟用。

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

   要在AEM中實現此目標，必須使用源編輯模式直接添加標籤。

   >[!NOTE]
   >
   >標準安裝中不立即提供此功能。 它需要RTE、HTML規則和序列化程式的配置。

#### 更多資訊 — 資訊和關係(1.3.1) {#more-information-info-and-relationships}

* [了解成功標準1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [如何符合成功標準1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### 有意義的序列(1.3.2)  {#meaningful-sequence}

* 成功標準1.3.2
* A級
* 有意義的序列：當呈現內容的序列影響其含義時，可以以寫程式方式確定正確的讀取序列。

#### 用途 — 有意義的序列(1.3.2) {#purpose-meaningful-sequence}

此成功標準的目的在於讓使用者代理提供內容的替代呈現，同時保留了解含義所需的閱讀順序。 必須能夠以寫程式方式確定至少一個有意義的內容序列。 當輔助技術以錯誤順序讀取內容，或套用替代樣式表或其他格式變更時，不符合此成功標準的內容可能會混淆或取消使用者方向。

#### 如何相遇 — 有意義的序列(1.3.2) {#how-to-meet-meaningful-sequence}

遵循 [如何符合成功標準1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### 更多資訊 — 有意義的序列(1.3.2) {#more-information-meaningful-sequence}

* [了解成功標準1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [如何符合成功標準1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### 感官特性(1.3.3)  {#sensory-characteristics}

* 成功標準1.3.3
* A級
* 感官特徵：為了解和操作內容而提供的指令不僅依賴於部件的感官特性，如形狀、大小、視覺位置、方向或聲音。

#### 目的 — 感官特性(1.3.3) {#purpose-sensory-characteristics}

設計人員在展示資訊時，往往關注視覺設計特徵，如顏色、形狀、文本樣式或內容的絕對或相對位置。 這些設計技術在傳達資訊方面可能非常強大（而且可以改善視力障礙使用者對認知障礙需求的整體無障礙性），但盲人或視力障礙者可能無法存取需要視覺識別位置、顏色或形狀等屬性的資訊。

同樣，需要區分不同聲音（例如男性或女性口語內容）的資訊，如果沒有反映在音頻內容的任何替代文本中，則會對聽力受損的人造成無障礙障礙。

>[!NOTE]
>
>有關顏色替代品的相關需求，請參閱 [顏色的使用](#use-of-color).

#### 如何滿足 — 感官特性(1.3.3) {#how-to-meet-sensory-characteristics}

請確定任何仰賴頁面內容視覺特性的資訊也會以替代格式顯示。

* 不要依賴視覺位置提供資訊。 例如，如果您想要將使用者引導至頁面右側的功能表，以存取詳細資訊，請勿參閱 *右邊的菜單*;請改為命名功能表（例如透過標題），並在文字中參照該名稱。
* 請勿以文字樣式（例如粗體或斜體文字）作為傳達資訊的唯一方式。

>[!NOTE]
>
>如果明白描述性詞語在非視覺內容中有意義，則可接受使用。 例如，使用 *abos* 和 *low* 通常是可接受的值，因為它們分別暗示特定內容之前和之後的內容；當內容被朗讀時，這仍然有意義。

#### 更多資訊 — 感官特性(1.3.3) {#more-information-sensory-characteristics}

* [了解成功標準1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [如何符合成功標準1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### 可區分(1.4) {#distinguishable}

[准則1.4可區分：讓使用者更輕鬆查看和聽取內容，包括將前景與背景分開。](https://www.w3.org/TR/WCAG/#distinguishable)

### 顏色的使用(1.4.1)  {#use-of-color}

* 成功標準1.4.1
* A級
* 顏色的使用：顏色不是唯一用於傳遞資訊、指示動作、提示響應或區分視覺元素的視覺手段。

>[!NOTE]
>
>此成功標準專門處理色彩感知。 其他形式的感知涵蓋於 [適應性(1.3)](#adaptable);包括對顏色的可寫程式訪問和其他可視演示編碼。

#### 用途 — 顏色的使用(1.4.1) {#purpose-use-of-color}

顏色是增強網頁審美吸引力的一種明顯有效的方法，也是資訊傳遞的有用手段。 然而，從失明到彩色視覺缺乏，都存在著一系列視覺缺陷，這意味著有些人無法區分某些顏色。 這使得顏色編碼成為提供資訊的不可靠方式。

例如，有紅綠色視覺缺陷的人將無法區分綠色的陰影和紅色的陰影。 他們可能會將這兩種顏色視為第三種顏色（例如棕色），在這種情況下，他們將無法區分紅色、綠色和棕色。

此外，使用純文字瀏覽器、單色顯示裝置或檢視頁面黑白打印輸出的使用者無法察覺顏色。

進一步的考量是 *已選取* 介面元素的狀態（例如，制表符、切換按鈕等），除了僅以顏色傳達外，還需要以其他方式傳達，而不只是以視覺呈現。 對於這些元素，額外使用模式、形狀和程式化資訊對於建立不依賴特定意義的完全包容性用戶體驗很有幫助。

#### 如何達成 — 色彩的使用(1.4.1) {#how-to-meet-use-of-color}

無論使用何種顏色來傳達資訊，都要確保資訊可用，而無需查看顏色。

例如，請確定文字中也明確提供顏色提供的資訊。

如果使用顏色作為提供資訊的提示，則應提供其他視覺提示，如更改樣式（如粗體、斜體字）或字型。 這有助於視力不足或彩色視力不足的人識別資訊。 不過，這無法完全依賴，因為這對根本看不到頁面的人沒有幫助。 因此，提供隱藏文字或使用程式化解決方案(例如 [無障礙的Rich Internet Applications(ARIA)Web標準套件](https://www.w3.org/WAI/standards-guidelines/aria/)，向無視的使用者傳達此資訊。

#### 更多資訊 — 顏色的使用(1.4.1) {#more-information-use-of-color}

* [了解成功標準1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [如何符合成功標準1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### 音頻控制(1.4.2)  {#audio-control}

* 成功標準1.4.2
* A級
* 音頻控制：如果網頁上的任何音頻自動播放超過3秒，則可以使用暫停或停止音頻的機制，或者可以使用獨立於整體系統音量級別的控制音頻音量的機制。

#### 用途 — 音訊控制(1.4.2) {#purpose-audio-control}

使用螢幕閱讀軟體的人，如果同時有其他音頻播放，就很難聽到語音輸出。 當螢幕助讀程式的語音輸出是基於軟體（如今大多數），並且通過與聲音相同的音量控制來控制時，這一困難就更加嚴重。 此外，一些認知殘疾人和神經發散的人可能具有聲音敏感性。 這些人會發現無法更改音頻內容的音量級別會造成很大干擾。

因此，用戶必須能夠關閉背景音。

>[!NOTE]
>
>對音量的控制包括能夠將其音量減小到零。

#### 如何達成 — 音訊控制(1.4.2) {#how-to-meet-audio-control}

遵循 [如何符合成功標準1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### 詳細資訊 — 音訊控制(1.4.2) {#more-information-audio-control}

* [了解成功標準1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [如何符合成功標準1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### 對比度（最低）(1.4.3) {#contrast-minimum}

* 成功標準1.4.3
* AA級
* 對比度（最小值）:文本和影像的視覺呈現具有至少4.5:1的對比度，但以下除外：
   * 大文本：大型文本和影像的對比度至少為3:1。
   * 附帶：屬於非活動用戶介面元件(即 [純裝飾](https://www.w3.org/TR/WCAG/#dfn-pure-decoration)，任何人都看不到，或是包含重要其他視覺內容之圖片的一部分，則沒有對比需求。
   * Logotype:屬於標誌或品牌名稱的文字沒有最低的對比要求。

   >[!NOTE]
   >
   >請參閱 [了解非文字對比](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) 如需詳細資訊，可協助確保內容作者了解非文字元素（包括圖示、介面元素等）的其他需求。

#### 用途 — 對比（最低）(1.4.3) {#purpose-contrast-minimum}

某些視覺障礙的人可能無法區分某些低對比度顏色對。 如果以下情況之一，這些人可能會遇到無障礙問題：

* 文字與背景顏色對比較差。
* 文本（如連結文本和非連結文本）的顏色編碼在識別資訊方面具有重要意義。

>[!NOTE]
>
>純粹用於裝飾目的的文字會排除在此成功標準之外。

#### 如何達成 — 對比（最低）(1.4.3) {#how-to-meet-contrast-minimum}

請確定文字與背景對比充分。 對比度取決於相關文本的大小和樣式：

* 對於大小小於18點（或14點粗體）的文本，文本/影像與背景的對比度應至少為4.5:1。
* 對於大小至少為18點（或14點粗體）的文本，對比度應至少為3:1。
* 如果已構圖背景，則應對所有文本週圍的背景進行著色，以保持4.5:1或3:1的比例。

>[!NOTE]
>
>請記住，字型在呈現等同PT/PX/EM大小時可能有所不同。
>
>建議您在選取適當字型和調整網頁內容大小時，善用可讀性和易用性的判斷力，以利錯誤。

>[!NOTE]
>
>下列網站可協助您轉換至其他單位：
>
>* [Px至Em計算器 — Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* [字型大小轉換：pixel-point-em-rem-percent](https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/)
>* [PMtoEM.com:將PX轉換為EM變更為簡單](https://pxtoem.com)


若要檢查對比度，請使用顏色對比工具，例如 [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) 或 [WebAIM顏色對比檢查程式](https://www.webaim.org/resources/contrastchecker/). 這些工具可讓您檢查色彩配對，並報告任何對比問題。

或者，如果您不太在意指定頁面的外觀，可以選擇不指定背景和前景文字顏色。 不需要對比度檢查，因為用戶的瀏覽器將確定文本和背景的顏色。

如果無法達到建議的對比層級，您需要提供頁面替代版本的連結（沒有顏色對比問題），或讓使用者根據自己的需求調整頁面色彩配置的對比。

#### 更多資訊 — 對比（最低）(1.4.3) {#more-information-contrast-minimum}

* [了解成功標準1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [如何符合成功標準1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### 調整文本大小(1.4.4)  {#resize-text}

* 成功標準1.4.4
* A級
* 調整文本大小：除了文字的標題和影像外，在沒有輔助技術的情況下，文字可調整大小，高達200%，而不會失去內容或功能。

#### 用途 — 調整文字大小(1.4.4) {#purpose-resize-text}

此成功標準的目的在於確保以視覺化方式呈現的文字，包括以文字為基礎的控制項（已顯示以便可看見的文字字元） [與仍以ASCII等資料形式顯示的文字字元])可成功縮放，讓視力有輕度障礙的人直接閱讀，而不需使用輔助技術，例如螢幕放大鏡。 使用者可從調整網頁上所有內容的比例中獲益，但文字是最重要的。

#### 如何相遇 — 調整文本大小(1.4.4) {#how-to-meet-resize-text}

並遵循以下准則： [如何符合成功標準1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) 您可以鼓勵內容作者在其頁面設計和字型大小（例如，回應式網頁設計）中使用流暢、彈性的寬度和高度，讓讀者能夠調整文字大小。

#### 更多資訊 — 調整文字大小(1.4.4) {#more-information-resize-text}

* [了解成功標準1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [如何符合成功標準1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### 文字影像(1.4.5) {#images-of-text}

* 成功標準1.4.5
* AA級
* 文字影像：如果所使用的技術能夠實現視覺呈現，則使用文本來傳達資訊，而不是文本的影像，但以下除外：
   * 可自訂：文本的影像可以根據用戶的需求進行可視化定製；
   * 基本：對所傳送的資訊而言，特定的文本表述是必不可少的。

>[!NOTE]
>
>Logotype（屬於標誌或品牌名稱的文字）被視為必要項目。

#### 用途 — 文字影像(1.4.5) {#purpose-images-of-text}

當偏好特定文字樣式時，通常會使用文字影像；例如，logotype或如果文本是從其他源（例如掃描紙文檔）生成的。 然而，與以HTML呈現和使用CSS設定樣式的文字相比，文字的影像缺乏變更大小或外觀的彈性，這對於視覺障礙或閱讀困難的人來說可能是必要的。

#### 如何相遇 — 文字影像(1.4.5) {#how-to-meet-images-of-text}

如果必須使用文字影像，請使用CSS將文字影像取代為HTML中的等同文字，讓文字能以可自訂的方式提供。 如需如何達成此目標的範例，請參閱 [C30:使用CSS將文本替換為文本的影像，並提供用戶介面控制項以切換](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### 詳細資訊 — 文字影像(1.4.5) {#more-information-images-of-text}

* [了解成功標準1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [如何符合成功標準1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## 原則2:可操作 {#principle-operable}

[原則2:可操作 — 用戶介面元件和導航必須可操作。](https://www.w3.org/TR/WCAG/#operable)

### 鍵盤(2.1) {#keyboard-accessible}

[建議2.1鍵盤（可訪問）:使所有功能都可通過鍵盤使用。](https://www.w3.org/TR/WCAG/#keyboard-accessible)

這涉及確保用戶可以使用鍵盤訪問所有功能。

### 鍵盤(2.1.1)  {#keyboard}

* 成功標準2.1.1
* A級
* 鍵盤：內容的所有功能通過鍵盤介面可操作，而不要求對個別鍵擊的特定定時，除了其基礎功能需要取決於用戶移動的路徑的輸入，而不僅僅是端點。

#### 用途 — 鍵盤(2.1.1) {#purpose-keyboard}

此成功標準旨在確保內容可在可能的情況下透過鍵盤或鍵盤介面操作（以便使用替代鍵盤）。 當內容可以通過鍵盤或替代鍵盤操作時，它可由無視覺的人（無法使用需要眼睛協調的滑鼠等設備）以及必須使用替代鍵盤或輸入設備作為鍵盤模擬器的人操作。 鍵盤模擬器包括語音輸入軟體、SIP和Puff軟體、螢幕鍵盤、掃描軟體以及各種輔助技術和備用鍵盤。 視力不佳的個人也可能難以追蹤指標，如果能從鍵盤控制指標，就會發現使用軟體更容易（或者只可能）。

#### 如何相遇 — 鍵盤(2.1.1) {#how-to-meet-keyboard}

遵循 [如何符合成功標準2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard).

#### 更多資訊 — 鍵盤(2.1.1) {#more-information-keyboard}

* [了解成功標準2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何符合成功標準2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### 無鍵盤陷阱(2.1.2)  {#no-keyboard-trap}

* 成功標準2.1.2
* A級
* 無鍵盤陷阱：如果可以使用鍵盤介面將鍵盤焦點移動到頁面的元件，則僅使用鍵盤介面可將焦點移離該元件，並且，如果它需要超過未修改的箭頭鍵或標籤鍵或其他標準退出方法，則建議用戶使用將焦點移離的方法。

#### 用途 — 無鍵盤陷阱(2.1.2) {#purpose-no-keyboard-trap}

此成功標準的目的是確保內容不會 *陷阱* 鍵盤焦點位於網頁上內容的子區段內。 在頁面中結合多種格式並使用外掛程式或內嵌應用程式轉譯時，這是常見的問題。

有時網頁的功能會將焦點限制在內容的子區段（例如，強制回應對話）。 在這種情況下，您應提供讓使用者能夠退出該內容區段的方法（例如，ESC鍵會關閉強制回應對話方塊，或是Close按鈕會關閉強制回應對話方塊）。

#### 如何相遇 — 無鍵盤陷阱(2.1.2) {#how-to-meet-no-keyboard-trap}

遵循 [如何符合成功標準2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap).

#### 更多資訊 — 無鍵盤陷阱(2.1.2) {#more-information-no-keyboard-trap}

* [了解成功標準2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何符合成功標準2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### 足夠的時間(2.2) {#enough-time}

[准則2.2足夠的時間：為使用者提供足夠的時間來閱讀和使用內容。](https://www.w3.org/TR/WCAG/#enough-time)

這關係到確保用戶有足夠的時間閱讀並採取行動。

### 可調時(2.2.1)  {#timing-adjustable}

* 成功標準2.2.1
* A級
* 鍵盤：為使用者提供足夠的時間來閱讀和使用內容。

#### 用途 — 可調時(2.2.1) {#purpose-timing-adjustable}

此成功標準旨在確保為身心障礙的使用者提供充足的時間，以便盡可能與網頁內容互動。 失明、低視力、靈巧性缺陷和認知限制等殘疾人可能需要更多時間閱讀內容或執行功能，如填寫線上表單。 如果Web功能與時間相關，則某些使用者在時間限制發生之前將很難執行所需的動作。 這可能會使他們無法存取服務。 設計不依賴時間的功能將幫助殘疾人成功完成這些功能。 提供禁用時間限制、自定義時間限制長度或在時間限制發生之前請求更多時間的選項，可幫助那些需要超出預期時間才能成功完成任務的用戶。 這些選項會依對使用者最有幫助的順序列出。 禁用時間限制比自定義時間限制長度更好，這比在時間限制發生之前請求更多時間要好。

#### 如何達成 — 可調時(2.2.1) {#how-to-meet-timing-adjustable}

遵循 [如何符合成功標準2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### 更多資訊 — 可調時(2.2.1) {#more-information-timing-adjustable}

* [了解成功標準2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [如何符合成功標準2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### 暫停、停止、隱藏(2.2.2)  {#pause-stop-hide}

* 成功標準2.2.2
* A級
* 暫停、停止、隱藏：對於移動、閃爍、滾動或自動更新資訊，以下是true:
   * 移動、閃爍、滾動：對於(a)自動啟動、(b)持續超過五秒、(c)與其他內容並行顯示的任何移動、閃爍或滾動資訊，有一種機制供用戶暫停、停止或隱藏，除非移動、閃爍或滾動是活動必不可少的一部分；
   * 自動更新：對於(a)自動啟動和(b)與其他內容並行顯示的任何自動更新資訊，有一種機制可讓使用者暫停、停止或隱藏更新，或控制更新的頻率，除非自動更新是活動的一部分，而其至關重要。

備注點有：

1. 有關閃爍或閃爍內容的要求，請參閱「Do Not Design Content in a Way that Know to Couse Quantured(2.3)(Do Not Design Content in a Way the Known to Cauges Quatted(2.3))」。
1. 由於任何不符合此成功標準的內容都可能干擾使用者使用整個頁面的能力，因此網頁上的所有內容（無論是否用於符合其他成功標準）都必須符合此成功標準。 請參閱 [合規要求5:無干擾](https://www.w3.org/TR/WCAG20/#cc5).
1. 由軟體定期更新或流向用戶代理的內容不需要保留或呈現在暫停啟動和恢復呈現之間產生或接收的資訊，因為這在技術上可能不可能，並且在許多情況下可能誤導用戶。
1. 如果在預載入階段或類似情況中不能對所有用戶進行交互，並且如果不指示進度，則可能會混淆用戶或導致他們認為內容已凍結或損壞，則可以認為動畫是必不可少的。

#### 用途 — 暫停、停止、隱藏(2.2.2) {#purpose-pause-stop-hide}

某些使用者可能會發現移動的內容會分散注意力，甚至會讓人感到身體痛苦，使得您很難專注在頁面的其他部分。 此外，對於無法跟上移動文字的人，這類內容可能很難閱讀。

#### 如何相遇 — 暫停、停止、隱藏(2.2.2) {#how-to-meet-pause-stop-hide}

根據內容的性質，在建立包含移動、閃爍或閃爍內容的網頁時，可以應用以下一個或多個建議：

* 提供暫停捲動內容的方法，讓使用者有足夠的時間閱讀內容。 例如，自動前進的新聞提示、自動更新的文字和影像輪播。
* 請確定連結的內容在5秒後停止閃爍。
* 使用適當的技術來顯示可由瀏覽器停用的移動或閃爍內容。 例如，圖形交換格式(GIF)或動畫可移植網路圖形(APNG)檔案。
* 在網頁上提供表單控制項，以允許使用者停用頁面上所有移動或閃爍的內容。
* 如果無法執行上述任何操作，請提供包含所有內容的頁面連結，但不要移動或閃爍。

#### 詳細資訊 — 暫停、停止、隱藏(2.2.2) {#more-information-pause-stop-hide}

* [了解成功標準2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [如何符合成功標準2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### 癲癇和身體反應(2.3) {#seizures-and-physcial-reactions}

[准則2.3緝獲量：請勿以已知導致癲癇或身體反應的方式設計內容。](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### 三個Flash或低於臨界值(2.3.1) {#three-flashes-or-below-threshold}

* 成功標準2.3.1
* A級
* 三個Flash或低於臨界值：網頁不包含任何在任何一秒內閃爍超過三次，或閃爍低於一般閃爍閾值和紅色閃爍閾值。

>[!NOTE]
>
>由於任何不符合此成功標準的內容都可能干擾使用者使用整個頁面的能力，因此網頁上的所有內容（無論是否用於符合其他成功標準）都必須符合此成功標準。 請參閱 [合規要求5:無干擾](https://www.w3.org/TR/WCAG/#cc5).

#### 用途 — 三個Flash或低於臨界值(2.3.1) {#purpose-three-flashes-or-below-threshold}

在某些情況下，閃爍的內容可能導致感光性癲癇。 此成功標準可讓這類使用者存取和體驗所有內容，而不必擔心內容閃爍的問題。

#### 如何達成 — 三個Flash或低於臨界值(2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

您應採取步驟，確認已套用下列技術：

* 在任何一秒的時間內，元件不會閃爍超過三次；
* 如果無法符合上述條件，則在 *小安全區* 畫面上的像素。 此區域是使用複雜公式計算，涵蓋於 [G176:保持閃光區足夠小](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)，因此只有在閃爍內容時才應遵循此技術 *絕對* 必要。

#### 詳細資訊 — 三個Flash或低於臨界值(2.3.1) {#more-information-three-flashes-or-below-threshold}

* [了解成功標準2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [如何符合成功標準2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### 可導覽(2.4) {#navigable}

[准則2.4可導覽：提供可協助使用者導覽、尋找內容及判斷其所在位置的方式。](https://www.w3.org/TR/WCAG/#navigable)

這涉及確保內容簡單明瞭，供使用者導覽。

### 略過區塊(2.4.1)  {#bypass-blocks}

* 成功標準2.4.1
* A級
* 旁路塊：機制可用來略過在多個網頁上重複的內容區塊。

#### 用途 — 略過區塊(2.4.1) {#purpose-bypass-blocks}

此成功標準的目的在於讓循序導覽內容的使用者，能更直接存取網頁的主要內容。 網頁和應用程式通常具有顯示在其他頁面或螢幕上的內容。 重複的內容區塊範例包括但不限於導覽連結、標題圖形、功能表和廣告影格。 為本規定的目的，不將個別字詞、片語或單個連結等重複的小部分視為區塊。

#### 如何達成 — 略過區塊(2.4.1) {#how-to-meet-bypass-blocks}

遵循 [如何符合成功標準2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### 更多資訊 — 略過區塊(2.4.1) {#more-information-bypass-blocks}

* [了解成功標準2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [如何符合成功標準2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### 標題為(2.4.2)的頁面  {#page-titled}

* 成功標準2.4.2
* A級
* 標題為：網頁的標題可描述主題或用途。

#### 用途 — 標題為(2.4.2)的頁面 {#purpose-page-titled}

此成功標準可協助所有人（不論是否有任何特定障礙）快速識別網頁內容，而無須完整閱讀頁面。 若在瀏覽器標籤中開啟數個網頁，這特別實用，因為頁面標題會顯示在標籤中，因此可快速找到。

#### 如何相遇 — 標題為(2.4.2)的頁面 {#how-to-meet-page-titled}

在AEM中建立新HTML頁面時，您可以指定頁面標題。 請確定標題能充分說明頁面的內容和用途，尤其是任何不重複的方面，讓訪客能快速識別內容是否實際與其需求相關。

編輯頁面時，您也可以編輯頁面標題，頁面資訊——屬 **性可****存取。**

#### 更多資訊 — 標題為(2.4.2)的頁面 {#more-information-page-titled}

* [了解成功標準2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [如何符合成功標準2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### 焦點順序(2.4.3)  {#focus-order}

* 成功標準2.4.3
* A級
* 焦點順序：如果網頁可以按順序導航，並且導航順序影響意義或操作，則可聚焦元件以保持意義和操作性的順序接收焦點。

#### 用途 — 焦點順序(2.4.3) {#purpose-focus-order}

此成功標準旨在確保當使用者依序導覽內容時，會遇到與內容含義一致且可由鍵盤操作的資訊。 這可讓使用者對內容建立一致的心理模型，以減少混淆。 內容中可能會有不同的順序反映邏輯關係。 例如，以由多個欄位和/或步驟組成的線上形式在元件之間移動會反映內容中的邏輯關係。

#### 如何達成 — 焦點訂單(2.4.3) {#how-to-meet-focus-order}

遵循 [如何符合成功標準2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### 更多資訊 — 焦點順序(2.4.3) {#more-information-focus-order}

* [了解成功標準2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [如何符合成功標準2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### 連結用途（內容中）(2.4.4)  {#link-purpose-in-context}

* 成功標準2.4.4
* A級
* 連結用途（在內容中）:每個連結的用途可以單獨從連結文本中確定，或者從連結文本連同其以程式設計方式確定的連結上下文一起確定，除非在通常情況下連結的目的對用戶是不明確的。

#### 用途 — 連結用途（內容中）(2.4.4) {#purpose-link-purpose-in-context}

對所有使用者而言，無論是否受到損害，透過適當連結文字清楚指出連結的方向至關重要。 這可協助使用者決定是否確實要追蹤連結。 對有視力的使用者而言，有意義的連結文字在頁面上有數個連結時（尤其是如果頁面是文字密集型的話）非常有用，因為有意義的連結文字可更清楚地指出目標頁面的功能。 某些輔助技術的使用者可產生單一頁面上所有連結的清單，如果該連結文字既獨特又能提供資訊，則可更輕鬆地了解內容外的連結文字。 然而，如果一個連結沒有提供足夠的資訊來準確描述該連結將帶往何處，則弱視的認知殘疾人可能會變得困惑。

#### 如何達成 — 連結用途（在內容中）(2.4.4) {#how-to-meet-link-purpose-in-context}

最重要的是，請確定連結的文字中已清楚說明連結的用途。

* 錯誤範例：
   * 文字：如需2010年秋天的晚間課程詳細資訊，請按一下這裡。
   * 原因：它沒有明確、明確地指明其目的地。
* 範例：
   * 文字：2010年秋季的夜班 — 細節。
   * 原因：稍微調整連結元素的文字和位置，即可改善連結文字：

連結的措辭應在各頁面上一致，尤其是導覽列。 例如，若特定頁面的連結已命名為 **出版物** 在單一頁面上，使用其他頁面上的該文字以確保一致性。

撰寫時，使用標題屬性會有一些問題，以確保頁面上呈現的類似連結提供關於目的地的唯一資訊（例如，「了解詳情」通常會指一系列不同的目的地）:

* 標題屬性中包含的文字通常僅作為工具提示彈出式視窗供滑鼠使用者使用，且無法使用鍵盤或行動使用者一致地存取。
* 螢幕助讀程式可讀取標題屬性，但此功能預設可能未啟用；因此，使用者可能不知道標題屬性存在。
* 很難改變標題文本的外觀，這意味著有些人可能很難或不可能閱讀。

因此，雖然title屬性可用來提供連結的額外內容，請注意其限制，請勿將其用作適當連結文字的替代項目。

當連結由影像組成時，請確定影像的替代文字說明連結的目的地。 例如，如果將書架的影像設為個人出版物的連結，則應閱讀替代文字 **約翰·史密斯的出版物** 和 **書架**.

或者，如果連結錨點除了影像元素外還包含描述連結用途的文字（因此文字會出現在影像旁邊），請為影像使用空白的alt屬性：

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>上述程式碼片段為圖例，建議您使用 **影像** 元件。

雖然建議您提供可識別連結目的的連結文字而不需要額外內容，但您可以認識到，這並非總是可行的。 無內容連結可用於下列情況，其HTML範例可在 [如何符合成功標準2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* 連結文字屬於密切相關連結清單的一部分，以及包含連結的清單項目提供足夠的內容時。
* 若連結的目的可從 *前置* （非以下）段文本。
* 若連結包含在資料表中，因此可從相關標題中清楚識別目的。
* 如果連結清單包含在一組標題中，而標題本身提供了適當的上下文。
* 其中，連結清單包含在巢狀連結中，而巢狀連結上方的父清單項目提供適當的內容。

在某些情況下，頁面上會有數個連結（每個連結以複雜但必要的詳細資訊提供連結的方向），因此提供可顯示完全相同內容但連結文字未如詳細的替代版網頁可能是適當的。

或者，可以使用指令碼，使得在連結本身內提供最少量的文本，但在激活定位到頁面頂部的適當控制項時，連結文本是 *擴充* 進一步細節。 使用CSS是類似的方法 *隱藏* 目視使用者的完整連結，但仍會以全螢幕輸出給螢幕助讀程式使用者。 這不在本檔案的範圍內，但有關如何達成此目標的詳細資訊，請參閱 [詳細資訊 — 連結用途（內容中）(2.4.4)](#more-information-link-purpose-in-context) 區段。

#### 詳細資訊 — 連結用途（內容中）(2.4.4) {#more-information-link-purpose-in-context}

* [了解成功標準2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [如何符合成功標準2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### 多種方式(2.4.5)  {#multiple-ways}

* 成功標準2.4.5
* AA級
* 多種方式：在一組網頁中，可以找到多種方法來查找網頁，除了該網頁是某個進程的結果或步驟之外。

#### 用途 — 多種方式(2.4.5) {#purpose-multiple-ways}

此成功標準的目的，是讓使用者能夠以最符合其需求的方式找到內容。 用戶可以發現一種技術比另一種更容易理解或更易理解。

即使是小型網站，也應為使用者提供一些定位方式。 若為三或四個頁面網站，且所有頁面皆從首頁連結，則只要提供來自和至首頁的連結即可，其中首頁上的連結也可作為網站地圖。

#### 如何達成 — 多種方式(2.4.5) {#how-to-meet-multiple-ways}

遵循 [如何符合成功標準2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways).

#### 更多資訊 — 多種方式(2.4.5) {#more-information-multiple-ways}

* [了解成功標準2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [如何符合成功標準2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### 標題和標籤(2.4.6)  {#headings-and-labels}

* 成功標準2.4.6
* AA級
* 標題和標籤：標題和標籤描述主題或目的。

#### 用途 — 標題和標籤(2.4.6) {#purpose-headings-and-labels}

此成功標準旨在協助使用者了解網頁中包含哪些資訊，以及該資訊的組織方式。 當標題清晰且描述性強時，使用者可更輕鬆找到所搜尋的資訊，並更輕鬆了解內容不同部分之間的關係。 描述性標籤可協助使用者識別內容中的特定元件。

#### 如何符合 — 標題和標籤(2.4.6) {#how-to-meet-headings-and-labels}

遵循 [如何符合成功標準2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels).

#### 詳細資訊 — 標題和標籤(2.4.6) {#more-information-headings-and-labels}

* [了解成功標準2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [如何符合成功標準2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### 焦點可見(2.4.7)  {#focus-visible}

* 成功標準2.4.7
* AA級
* 焦點可見：任何可操作鍵盤的用戶介面都具有操作模式，其中鍵盤焦點指示器是可見的。

#### 用途 — 焦點可見(2.4.7) {#purpose-focus-visible}

此成功標準的目的在於協助使用者知道哪個元素具有鍵盤焦點。

人員必須知道多個元素中的哪個元素具有鍵盤焦點。 如果畫面上只有一個鍵盤可操作的控制項，則會符合成功標準，因為視覺設計只顯示一個鍵盤可操作的項目。

如果成功標準顯示為「操作模式」，這表示平台不一定會顯示焦點指標。 在大多數情況下，只有一種操作模式，因此此成功標準適用。

#### 如何開會 — 焦點可見(2.4.7) {#how-to-meet-focus-visible}

遵循 [如何符合成功標準2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### 更多資訊 — 可見焦點(2.4.7) {#more-information-focus-visible}

* [了解成功標準2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [如何符合成功標準2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## 原則3:可理解 {#principle-understandable}

[原則3:可理解 — 資訊和用戶介面的操作必須可理解。](https://www.w3.org/TR/WCAG/#understandable)

### 讓文字內容可讀且可理解(3.1) {#make-text-content-readable-and-understandable}

[准則3.1可讀：讓文字內容可讀且可理解。](https://www.w3.org/TR/WCAG/#readable)

### 頁面語言(3.1.1) {#language-of-page}

* 成功標準3.1.1
* A級
* 頁面語言：每個網頁的預設人類語言可以程式設計地決定。

#### 用途 — 頁面語言(3.1.1) {#purpose-language-of-page}

此成功標準的目的在於確保文字和其他語言內容正確轉譯。 若是螢幕助讀程式使用者，這可確保內容正確發音，而視覺瀏覽器更可能正確顯示特定字元集。

#### 如何相遇 — 頁面語言(3.1.1) {#how-to-meet-language-of-page}

為符合此成功標準，可使用 `lang` 屬性 `<html>` 元素。 例如：

* 若以英文撰寫， `<html>` 元素應該讀取：
   `<html lang = "en">`

* 以西班牙文轉譯的頁面應採用下列標準：
   `<html lang = "es">`

在AEM中，頁面的預設語言是在建立頁面時設定，但在編輯時也可能變更 [頁面屬性](/help/sites-authoring/editing-page-properties.md).

>[!NOTE]
>
>AEM可進一步微調根語言的變化；例如，美國英語 — en-us、英語 — en-gb和加拿大英語 — en-ca。 對於輔助技術，此詳細程度通常是多餘的，不過可用於頁面內容中的區域變異。

#### 更多資訊 — 頁面語言(3.1.1) {#more-information-language-of-page}

* [了解成功標準3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [如何符合成功標準3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* 代碼基於ISO 639-1。 您可以在 [W3學校站點](https://www.w3schools.com/tags/ref_language_codes.asp).

### 部件語言(3.1.2)  {#language-of-parts}

* 成功標準3.1.2
* AA級
* 部件語言：可以以寫程式方式確定內容中每個段落或短語的人類語言，但是，適當的名稱、技術術語、不確定語言的單詞以及作為立即圍繞文本的白話的一部分的單詞或短語除外。

#### 目的 — 部件的語言(3.1.2) {#purpose-language-of-parts}

此成功標準的用途與成功標準類似 [頁面語言](#language-of-page)，但適用於單一頁面上包含多種語言內容的網頁（例如，由於引號或不常見的借記字詞）除外。

套用此成功標準的頁面允許：

* 盲文轉換軟體，以插入帶重音字元。
* 螢幕助讀程式可朗讀那些有特殊字元或未使用頁面層級所識別之預設語言的字詞。
* Google翻譯工具等翻譯工具可將內容從一種語言正確翻譯為另一種語言。

#### 如何交集 — 部件語言(3.1.2) {#how-to-meet-language-of-parts}

此 `lang` 屬性可用來識別內容語言中的變更。 例如，德文引號（ISO 639-1代碼&quot;de&quot;）如下所示：

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>現成可用的執行個體不支援區塊引號。 可開發自訂元件以支援此功能。

同樣地，若 `span` 元素的使用方式如下：

```xml
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>在包含不同語言的名稱或城市，或使用在預設語言中已司空見慣的借詞或片語時(例如 *幸福* 英文)。

若要新增跨度元素（使用適當的語言），您可以在RTE的來源編輯模式中手動編輯HTML標籤，使其如上所示。 或者， `lang` 屬性可由系統管理員包含在RTE中(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

#### 更多資訊 — 部件語言(3.1.2) {#more-information-language-of-parts}

* [了解成功標準3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [如何符合成功標準3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### 可預測(3.2) {#predictable}

[准則3.2可預測：讓網頁以可預測的方式顯示和運作。](https://www.w3.org/TR/WCAG/#predictable)

這涉及確保網頁的外觀和操作方式一致。

### 聚焦(3.2.1)  {#on-focus}

* 成功標準3.2.1
* A級
* 聚焦：任何使用者介面元件收到焦點時，都不會起始內容變更。

#### 用途 — 觀看(3.2.1) {#purpose-on-focus}

此成功標準的目的，是在訪客瀏覽檔案時，確保功能可預測。 任何元件若能在收到焦點時觸發事件，則不得變更內容。 元件收到焦點時變更內容的範例包括，但不限於：

* 元件收到焦點時自動提交的表單；
* 元件受到關注時啟動的新窗口；
* 當該元件接收焦點時，焦點會變更為另一個元件；

焦點可以通過鍵盤（例如對控制項進行Tab鍵操作）或滑鼠（例如按一下文本欄位）移動到控制項。 將滑鼠移到控制項上不會移動焦點，除非指令碼實施此行為。 請注意，對於某些類型的控制項，按一下控制項也可以激活控制項（例如按鈕），這反過來又可以啟動上下文中的更改。

#### 如何開會 — 觀看(3.2.1) {#how-to-meet-on-focus}

遵循 [如何符合成功標準3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus).

#### 更多資訊 — 觀看(3.2.1) {#more-information-on-focus}

* [了解成功標準3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [如何符合成功標準3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### 輸入(3.2.2)  {#on-input}

* 成功標準3.2.2
* A級
* 輸入時：更改任何用戶介面元件的設定不會自動導致上下文更改，除非在使用該元件之前已告知用戶該行為。

#### 用途 — 輸入(3.2.2) {#purpose-on-input}

此成功標準的目的是確保輸入資料或選取表單控制項具有可預測的效果。 變更任何使用者介面元件的設定，會變更控制項中某些方面，而這些方面會在使用者不再與其互動時持續存在。 因此，勾選核取方塊、在文字欄位中輸入文字，或變更清單控制項中選取的選項，都會變更其設定，但啟動連結或按鈕則否。 內容變更可能會混淆無法輕鬆感知變更或容易因變更而分心的使用者。 唯有當使用者的動作顯然會發生這類變更時，才適合變更內容。

#### 如何符合 — 輸入(3.2.2) {#how-to-meet-on-input}

遵循 [如何符合成功標準3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input).

#### 更多資訊 — 輸入(3.2.2) {#more-information-on-input}

* [了解成功標準3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [如何符合成功標準3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### 一致導航(3.2.3)  {#consistent-navigation}

* 成功標準3.2.3
* AA級
* 一致導航：在一組網頁內，在多個網頁上重複的導航機制在每次重複時都以相同的相對順序發生，除非用戶啟動了更改。

#### 用途 — 一致導覽(3.2.3) {#purpose-consistent-navigation}

此成功標準旨在鼓勵使用者在一組網頁內與重複內容互動，且需要多次尋找特定資訊或功能時，使用一致的呈現和版面。 視覺低的個人若同時使用螢幕放大率來顯示一小部分螢幕，通常會使用視覺提示和頁面邊界來快速找出重複的內容。 對於在設計中使用空間記憶或視覺提示來定位重複內容的視覺使用者而言，以相同順序呈現重複內容也很重要。

請務必注意，本節中使用「相同順序」一詞並不代表無法使用子導覽功能表，或無法使用次導覽區塊或頁面結構。 相反地，此成功標準旨在協助使用者在網頁上與重複內容互動，以便預測所尋找內容的位置，並在再次遇到時更快速找到。

用戶可以通過使用自適應用戶代理或設定首選項來啟動順序的更改，以便以對他們最有用的方式顯示資訊。

#### 如何達成 — 一致的導覽(3.2.3) {#how-to-meet-consistent-navigation}

遵循 [如何符合成功標準3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation).

#### 更多資訊 — 一致導覽(3.2.3) {#more-information-consistent-navigation}

* [了解成功標準3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [如何符合成功標準3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### 一致識別(3.2.4)  {#consistent-identification}

* 成功標準3.2.4
* A級
* 一致的標識：在一組網頁內具有相同功能的元件會一致識別。

#### 用途 — 一致標識(3.2.4) {#purpose-consistent-identification}

此成功標準旨在確保一致識別一組網頁中重複出現的功能元件。 操作網站時使用螢幕助讀程式的人採用的策略是，他們非常依賴於對可能出現在不同網頁的功能的熟悉。 如果相同的函式在不同的網頁上具有不同標籤（或更一般地說，不同的可存取名稱），則網站的使用難度會大得多。 這也可能令人困惑，並增加了認知局限性人群的認知負荷。 因此，一致的標籤將有所幫助。

這種一致性延伸到了文本替代項。 如果圖示或其他非文字項目具有相同的功能，則其替代文字也應一致。

如果網頁上有兩個元件，且兩者的功能與一組網頁中其他頁面上的元件相同，則這三個元件必須一致。 因此，同一頁上的兩者將保持一致。

雖然理想且最佳實務一律在單一網頁內保持一致，但3.2.4僅處理一組網頁內的一致性，該組網頁中的多個頁面上重複某項目。

#### 如何達成 — 一致的識別(3.2.4) {#how-to-meet-consistent-identification}

遵循 [如何符合成功標準3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification).

#### 更多資訊 — 一致身份識別(3.2.4) {#more-information-consistent-identification}

* [了解成功標準3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [如何符合成功標準3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### 投入援助(3.3) {#input-assistance}

[准則3.3投入援助：協助使用者避免和修正錯誤。](https://www.w3.org/TR/WCAG/#input-assistance)

### 錯誤標識(3.3.1)  {#error-identification}

* 成功標準3.3.1
* A級
* 錯誤標識：如果自動檢測到輸入錯誤，則識別出錯誤的項，並以文本向用戶描述該錯誤。

#### 用途 — 錯誤識別(3.3.1) {#purpose-error-identification}

此成功標準旨在確保使用者知道發生錯誤，並可判斷錯誤。 錯誤訊息應盡可能具體。 在表單提交失敗的情況下，重新顯示表單並指出錯誤中的欄位，不足以讓部分使用者察覺發生錯誤。 例如，螢幕助讀程式的使用者在遇到其中一個指標前，將不會知道有錯誤。 他們可能會在遇到錯誤指標前完全放棄表單，認為頁面無法運作。 根據WCAG中的定義， [輸入錯誤](https://www.w3.org/TR/WCAG/#dfn-input-error) 是使用者提供的未接受的資訊。 這包括：

網頁所需但用戶所省略的資訊，或用戶所提供但不符合所需資料格式或允許值的資訊。
例如：

* 使用者無法在中輸入正確的縮寫，如州、省、地區等。 欄位;
* 用戶輸入非有效狀態的狀態縮寫；
* 用戶輸入的郵遞區號不存在；
* 用戶在未來2年內輸入出生日期；
* 用戶在只接受號碼的電話號碼欄位中輸入字母字元或括弧；
* 使用者輸入的競標低於先前的競標或最低競標增量。

#### 如何滿足 — 錯誤標識(3.3.1) {#how-to-meet-error-identification}

遵循 [如何符合成功標準3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### 更多資訊 — 錯誤識別(3.3.1) {#more-information-error-identification}

* [了解成功標準3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [如何符合成功標準3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### 標籤或說明(3.3.2) {#labels-or-instructions}

* 成功標準3.3.2
* A級
* 標籤或指示：當內容需要用戶輸入時，提供標籤或指示。

#### 用途 — 標籤或指示(3.3.2) {#purpose-labels-or-instructions}

提供說明以協助使用者填寫表單是介面可用性良好實務的基本部分。 這麼做對於視覺或認知功能障礙的人特別有幫助，因為他們原本可能很難理解表單的版面配置，以及要在特定表單欄位中提供的資料類型。

##### Forms

在AEM WKND示範專案中，新增表單元件時(例如 **文字欄位**，前往頁面。 此預設標題取決於元件類型。您可以在 **標題和文字** 頁簽。 務必確保標籤可協助使用者了解與每個表單元件相關聯的資料。

此 **標題** 欄位必須用於欄位元素，因為它提供可用於輔助技術的標籤。 僅在欄位旁的文字中寫標籤是不夠的。

對於某些表單元件，您也可以使用「隱藏標題」核取方塊以視覺化方式 **隱藏標籤** 。以此方式隱藏的標籤仍適用於輔助技術，但無法顯示在螢幕上。雖然這在某些情況下是個好方法，但通常最好盡可能加入視覺標籤，因為有些使用者可能會看到畫面的一小部分 (一次看一個欄位)，並需要標籤來正確識別欄位。

###### 影像按鈕 {#image-buttons}

其中使用影像按鈕(例如 **影像按鈕** WKND專案的元件) **標題** 欄位 **標題和文字** 編輯對話方塊的索引標籤實際上會提供影像的替代文字，而非標籤。 因此，在以下範例中，包含文字的影像 `Submit` 的alt文字為 `Submit`，使用編輯對話方塊中的 **Title** 欄位新增。

###### 表單欄位群組 {#groups-of-form-fields}

在WKND專案中，有一組相關控制項，例如 **無線電組**，群組以及個別控制項可能需要標題。 在AEM中新增一組選項按鈕時，「標題 **」欄位會提供此群組標題，而個別標題會指定為選項按鈕(** Items ****)。

不過，群組標題和選項按鈕本身之間沒有程式化關聯。範本編輯人員必須將標題包住必要 `fieldset` 和 `legend` 標籤，才能建立此關聯，而這只能透過編輯頁面原始碼來完成。或者，系統管理員可以新增對這些元素的支援，使這些元素顯示在 **欄位屬性** 對話方塊(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

###### 其他Forms考量事項 {#additional-considerations-for-forms}

如果要以特定格式輸入資料，請在標籤文字中清楚說明。 例如，如果必須在 `DD-MM-YYYY` 格式，具體說明這是標籤的一部分。 這表示當螢幕助讀程式的使用者遇到欄位時，會自動宣佈標籤，以及格式的其他資訊。

如果表單欄位的輸入是必填的，請使用標籤中的必要字詞來清楚說明。AEM在需要欄位時新增星號，但最好將字詞加入標 `required`簽本身(在編輯對話方塊的「 **Title** 」欄位中)。

標籤的定位也很重要，因為這有助於他們找到適當的欄位。 當使用者面臨複雜表單時，這尤其重要。 請遵守以下公約：

* 複選框或單選按鈕：標籤會立即放置在欄位的右側。
* 所有其他表單元件（例如文字方塊、下拉式方塊）:標籤會緊接在欄位的上方或緊鄰左側。

以功能非常有限的簡單形式，適當標示 `Submit` 按鈕可作為相鄰欄位的標籤(例如 `Search`)。 這在尋找標籤文字的空格可能很困難的情況下很有用。

#### 更多資訊 — 標籤或說明(3.3.2) {#more-information-labels-or-instructions}

* [了解成功標準3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [如何符合成功標準3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### 錯誤建議(3.3.3)  {#error-suggestion}

* 成功標準3.3.3
* AA級
* 鍵盤：如果自動檢測輸入錯誤並知道用於校正的建議，則向用戶提供建議，除非它會危及內容的安全或目的。

#### 用途 — 錯誤建議(3.3.3) {#purpose-error-suggestion}

此成功標準的目的在於確保使用者收到適當建議以更正輸入錯誤（如果可能）。 WCAG的定義 [輸入錯誤](https://www.w3.org/TR/WCAG/#dfn-input-error) 說系統「不接受用戶提供的資訊」。 未被接受的資訊的一些示例包括用戶需要但省略的資訊和用戶提供但不符合所需資料格式或允許值的資訊。

成功標準3.3.1提供錯誤通知。 然而，認知有限的人可能很難理解如何糾正錯誤。 視覺殘疾的人可能無法確切了解如何更正錯誤。 如果表單提交失敗，使用者可能會因為不知道如何更正錯誤而放棄表單，即使他們知道錯誤已發生。

內容作者可以提供錯誤的描述，或者用戶代理可以基於特定於技術的、以寫程式方式確定的資訊提供錯誤的描述。

#### 如何達成 — 錯誤建議(3.3.3) {#how-to-meet-error-suggestion}

遵循 [如何符合成功標準3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion).

#### 詳細資訊 — 錯誤建議(3.3.3) {#more-information-error-suggestion}

* [了解成功標準3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [如何符合成功標準3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### 錯誤預防（法律、財務、資料）(3.3.4)  {#error-prevention-legal-financial-data}

* 成功標準3.3.4
* AA級
* 錯誤預防（法律、財務、資料）:對於導致用戶發生法律承諾或財務交易、修改或刪除資料儲存系統中用戶可控資料或提交用戶測試響應的網頁，至少以下情況之一為真：

   * 可逆提交是可逆的。
   * 檢查用戶輸入的已檢查資料是否有輸入錯誤，並向用戶提供糾正這些錯誤的機會。
   * 已確認在提交完成之前，有機制可供審閱、確認和更正資訊。

#### 用途 — 錯誤預防（法律、財務、資料）(3.3.4) {#purpose-error-prevention-legal-financial-data}

本成功標準旨在協助身心障礙的使用者避免執行無法還原的動作時發生錯誤而導致的嚴重後果。 例如，購買不可退還的機票或提交訂購單以在經紀帳戶中購買股票，是具有嚴重後果的金融交易。 如果用戶在航空旅行日期犯了錯誤，他或她最終可能會在無法交換的錯誤日期獲得機票。 如果用戶在要購買的股票數量上犯了錯誤，他或她最終可能購買的股票會超出預期。 這兩種錯誤都涉及立即發生的交易，且以後不能更改，而且代價非常高。 同樣，如果用戶無意修改或刪除儲存在資料庫中的資料（如他們在旅行服務網站中的整個旅行配置檔案），則可能是一個不可恢復的錯誤。 當提及修改或刪除「用戶可控」資料時，其目的是防止大量丟失資料，如刪除檔案或記錄。 不是為了每次保存命令或文檔、記錄或其他資料的簡單建立或編輯而需要確認。

殘疾使用者更可能犯錯。 閱讀障礙者可以轉換數字和字母，運動障礙者可以錯擊鍵。 提供反轉動作的功能，可讓使用者修正可能導致嚴重後果的錯誤。 提供審查和糾正資訊的能力使用戶在採取具有嚴重後果的行動之前能夠檢測錯誤。

用戶可控資料是用戶可查看的資料，用戶可以通過故意操作來更改和/或刪除這些資料。 控制此類資料的用戶的示例將更新用戶帳戶的電話號碼和地址，或從網站刪除過去發票的記錄。 它不會參照使用者無法直接檢視或與之互動的網際網路記錄和搜尋引擎監控資料等項目。

#### 如何達成 — 錯誤預防（法律、財務、資料）(3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

遵循 [如何符合成功標準3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### 更多資訊 — 錯誤預防（法律、財務、資料）(3.3.4) {#more-information-error-prevention-legal-financial-data}

* [了解成功標準3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [如何符合成功標準3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## 原則4:強大 {#principle-robust}

[原則4:強大 — 內容必須足夠強大，以供各種使用者代理（包括輔助技術）解譯。](https://www.w3.org/TR/WCAG/#robust)

### 相容(4.1) {#compatible}

[准則4.1相容：盡量提高與目前和未來使用者代理的相容性，包括輔助技術。](https://www.w3.org/TR/WCAG/#compatible)

盡量提高與目前和未來使用者代理的相容性，包括輔助技術。

### 解析(4.1.1)  {#parsing}

* 成功標準4.1.1
* A級
* 解析：在使用標籤語言實作的內容中，元素具有完整的開始和結束標籤，元素根據其規範進行嵌套，元素不包含重複屬性，且除了規範允許這些功能外，任何ID都是唯一的。

#### 用途 — 解析(4.1.1) {#purpose-parsing}

此成功標準的目的在於確保使用者代理（包括輔助技術）可準確解譯和剖析內容。 如果無法將內容剖析為資料結構，則不同的使用者代理可能會以不同方式呈現內容，或完全無法剖析內容。 有些使用者代理使用「修復技術」來轉譯編碼不良的內容。

由於修復技術在用戶代理之間各不相同，因此作者不能假設內容將準確剖析為資料結構，或者內容將由專門的用戶代理（包括輔助技術）正確呈現，除非內容是根據該技術的正式語法中定義的規則建立。 在標籤語言中，元素和屬性語法中的錯誤以及未提供正確巢狀的開始/結束標籤會導致錯誤，使用者代理無法可靠地剖析內容。 因此，成功標準要求只能使用正規語法的規則來剖析內容。

#### 如何符合 — 剖析(4.1.1) {#how-to-meet-parsing}

遵循 [如何符合成功標準4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### 更多資訊 — 解析(4.1.1) {#more-information-parsing}

* [了解成功標準4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [如何符合成功標準4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### 名稱、角色、值(4.1.2)  {#name-role-value}

* 成功標準4.1.2
* A級
* 名稱、角色、值：針對所有使用者介面元件(包括但不限於：表單元素、連結和指令碼產生的元件)，可以以程式設計方式確定名稱和角色；可由使用者設定的狀態、屬性和值，可以以程式設計方式設定；使用者代理可取得這些項目的變更通知，包括輔助技術。

#### 用途 — 名稱、角色、值(4.1.2) {#purpose-ame-role-value}

此成功標準的目的在於確保輔助技術(AT)可以收集、啟用（或設定）相關資訊，並隨時掌握內容中使用者介面控制項的最新狀態。

使用無障礙技術的標準控制時，此程式就相當簡單明瞭。 如果用戶介面元素根據規格使用，則滿足此設定的條件。 （請參閱下方的成功標準4.1.2範例）

但是，如果已建立自訂控制項，或介面元素已程式化（在程式碼或指令碼中）以具有與往常不同的角色和/或功能，則需要採取其他措施，以確保控制項提供重要資訊給輔助技術，並允許這些控制項由輔助技術控制。

用戶介面控制項的一個特別重要的狀態是它是否具有焦點。 控制項的焦點狀態可以以程式設計方式確定，並且關於焦點改變的通知會傳送給使用者代理和輔助技術。 用戶介面控制狀態的其他示例包括是否已選擇複選框或單選按鈕，或者是否展開或折疊可折疊的樹或清單節點。

#### 如何達成 — 名稱、角色、值(4.1.2) {#how-to-meet-ame-role-value}

遵循 [如何符合成功標準4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### 詳細資訊 — 名稱、角色、值(4.1.2) {#more-information-ame-role-value}

* [了解成功標準4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [如何符合成功標準4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
