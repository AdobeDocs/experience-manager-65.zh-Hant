---
title: 為Adobe Experience Manager建立可訪問內容（WCAG 2.1一致性）
description: 用AEM於幫助使殘疾人能夠訪問和使用Web內容
exl-id: 2145d761-f51d-482b-a0e7-ef7500c4872f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '13956'
ht-degree: 5%

---

# 建立可存取的內容 (符合 WCAG 2.1) {#creating-accessible-content-wcag-conformance}

的 [Web內容輔助功能指南(WCAG)2.1](https://www.w3.org/TR/WCAG/)，由 [World Wide Wec Consortium工作組](https://www.w3.org/Consortium/activities#Accessibility_Guilenes_Working_Group)包括一套與技術無關的准則和成功標準，以幫助殘疾人訪問和使用網路內容。

作為介紹，該聯盟提供了一系列章節和支援檔案：

* [WCAG 2.1中的新功能](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [How to Meet WCAG 2.1 (如何達成 WCAG 2.1) ](https://www.w3.org/WAI/WCAG21/quickref/)
* [Understanding WCAG 2.1 (了解 WCAG 2.1) ](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Techniques for WCAG 2.1 (WCAG 2.1 的專用技術) ](https://www.w3.org/WAI/WCAG21/Techniques/)
* [WCAG文檔](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

此外，請參閱：
* 我們的 [WCAG 2.1快速指南](/help/managing/qg-wcag.md)。
* 的 [Adobe解決方案的輔助功能符合性報告](https://www.adobe.com/accessibility/compliance.html)。
* [配置富格文本編輯器以生成可訪問內容](/help/sites-administering/rte-accessible-content.md)

本指南按三個一致性級別分級：A級（最低）、A級和AAA級（最高）。 簡而言之，這些級別定義如下：

* **** A級：您的網站達到基本的最低協助功能等級。要達到此級別，將滿足所有A級成功標準。
* **AA級：** 這是您努力實現的理想的可訪問性級別，在此級別，您的站點達到了基本的可訪問性級別，因此在大多數情況下使用大多數技術的大多數人都可以訪問。 要達到此級別，將滿足所有A級和A級成功標準。
* **** AAA級：您的網站可達到非常高的協助功能。要達到此級別，將滿足所有A級、AA級和AAA級成功標準。

建立網站時，您必須決定要讓網站遵循的整體等級。

以下部分顯示 [WCAG 2.1指南的層](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) A級和AA級的相關成功標準 [一致性級別](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1)。

>[!NOTE]
>
>在本文檔中，我們使用：
>
>* 的 [WCAG 2.1准則的短名稱](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance)。
>* 的 [WCAG 2.1指南中使用的編號](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) 以便與WCAG網站交叉引用。


## 原則1:可感知 {#principle-perceivable}

[原則1:可感知 — 資訊和用戶介面元件必須以用戶能夠感知的方式顯示給用戶。](https://www.w3.org/TR/WCAG/#perceivable)

### 文本替代(1.1) {#text-alternatives}

[准則1.1案文備選方案：為任何非文本內容提供文本替代，以便將其轉換為人們需要的其他形式，如大型打印、盲文、語音、符號或更簡單的語言。](https://www.w3.org/TR/WCAG/#text-alternatives)

### 非文本內容(1.1.1) {#non-text-content}

* 成功標準1.1.1
* A級
* 非文本內容：呈現給用戶的所有非文本內容都有一個文本替代項，該文本替代項服務於相同目的，下面列出的情況除外。

#### 目的 — 非文本內容(1.1.1) {#purpose-non-text-content}

網頁上的資訊可以以多種不同的非文本格式提供，如圖片、視頻、動畫、圖表和圖形。 失明或視力嚴重受損的人無法看到非文本內容，但他們可以通過讓螢幕閱讀器讀取文本內容或通過盲文顯示設備以觸覺形式呈現來訪問文本內容。 因此，通過提供圖形格式內容的文本替代選項，無法查看圖形內容的人可以訪問內容所提供的資訊的等效版本。

一個有用的附加好處是，文本替代方案使非文本內容能夠通過搜索引擎技術進行索引。

#### 如何見面 — 非文本內容(1.1.1) {#how-to-meet-non-text-content}

對於靜態圖形，基本要求是為圖形提供等效的文本替換。 可以在 **備選文本** 欄位；例如， **[影像](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/components/image.translate.html)**。

>[!NOTE]
>
>一些現成的核心元件，如 **[旋轉木馬](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/components/carousel.html)** 不提供 **備選文本** 用於向單個影像添加替代文本說明的欄位，但 **標籤** 欄位(D)**[輔助功能](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html#accessibility-tab)** )。
>
>為實例實施這些版本AEM時，您的開發團隊需要配置這些元件以支援 `alt` 屬性，以便作者可以將其添加到內容(請參見 [添加對附加HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

AEM要求 **備選文本** 預設情況下要填充的欄位。 如果影像純粹是裝飾性的，並且不需要替代文字， **影像是裝飾性的** 選項。

#### 建立好文本選項 {#creating-good-text-alternatives}

非文本內容有多種形式，因此文本替換的價值取決於圖形在網頁中所扮演的角色。 以下是一些一般經驗法則：

* 案文備選案文應簡潔明瞭，但應清楚地掌握非文本內容提供的基本資訊。
* 應避免過長的描述（超過100個字元）。 如果文本替代項需要更多詳細資訊：
   * 在備選文本中提供簡短說明
   * 在同一頁或單獨網頁的其他位置的文本中有較長的說明。 通過使影像成為連結或將文本連結置於影像旁邊來連結到此單獨的說明。
* 備選文本不應複製同一頁面上附近文本表單中提供的內容。 請記住，許多影像是頁面文本中已涵蓋的點的插圖，因此可能已存在詳細的文本替代選項。
* 如果非文本內容是指向另一頁或文檔的連結，並且沒有其他文本構成同一連結的一部分，則影像的替代文本必須指示連結的目的地，而不是描述影像。
* 如果非文本內容包含在按鈕元素中，並且沒有文本構成同一按鈕的一部分，則影像的替代文本必須指示按鈕的功能，而不是描述影像。
* 為影像指定空（空）替代文本是完全可接受的，但前提是該影像不需要替代文本（例如，它是純裝飾圖形），或者頁面文本中已存在等效文本。

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

需要文本替代的特定類型的非文本內容可能包括：

* 說明性照片：這些是人、物體或地方的影像。 考慮照片在頁面中的作用非常重要，並且通常建議描述影像內容，因為輔助技術會宣佈元素類型(例如， `graphic` 或 `image`);可以提高使用的清晰度 `screenshot` 或 `illustration` 在替代文字說明中，但這取決於上下文。 一致性是一個重要因素，應該為整個創作團隊做出決策，並且這應用於整個用戶體驗。
* 表徵圖：這些是傳輸特定資訊的小像形圖（圖形）。 必須在頁面和站點上始終使用它們。 頁面或站點上表徵圖的所有實例都應具有相同的簡短文本選項，除非這樣做會導致相鄰文本的不必要的重複。
* 圖表和圖形：這些通常表示數值資料。 因此，提供文本替代選項的一個選項可能是包含圖表或圖形中顯示的主要趨勢的簡短摘要。 如有必要，還可使用 **說明** 的 **高級** 影像屬性頁籤。 此外，您還可以以表格形式在頁面或站點的其他位置提供源資料。
* 映射、圖、流程圖：對於提供空間資料的圖形（例如，支援描述對象或進程之間的關係），請確保以文本格式提供關鍵消息，並確保此文本資訊位於每個關聯資料點附近。 對於地圖，提供等同全文的地圖可能不切實際，但如果提供地圖以幫助人們找到特定位置的方式，則地圖影像的替代文字可以簡短地標示 *X*，然後在頁面其他地方的文字或透過 **Image元件的「** Advanced **」 (進階) 索引標籤中的「** Description **** 」 (說明) 欄位，提供指向該位置的指示。
* 驗證碼：驗證碼是 *完全自動化的公共圖靈test將電腦和人區分開來*。 它是用於網頁上的安全檢查，用於區分人和惡意軟體，但會造成訪問障礙。 這些映像需要用戶描述他們看到的內容，以便通過安全test。 為影像提供文本替代顯然是不可能的，因此您需要考慮其他非圖形解決方案。 W3C提出了一些建議，如：
   * 邏輯謎題
   * 使用聲音輸出而不是影像
   * 帳戶和垃圾郵件過濾器使用有限。
* 背景影像：這些是使用層疊樣式表(CSS)而不是在HTML中實現的。 這意味著無法指定替代文本值。 因此，背景影像不應提供重要的文本資訊 — 如果提供了，則還必須在頁面文本中提供此資訊。 但是，當無法顯示影像時，必須顯示替代背景。

>[!NOTE]
>
>背景和前景文本之間應有適當的對比度；在 [對比度（最小值）(1.4.3)](#contrast-minimum)。

#### 詳細資訊 — 非文本內容(1.1.1) {#more-information-non-text-content}

* [瞭解成功標準1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [如何滿足成功標1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [驗證碼的W3C解釋和替代](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### 基於時間的介質(1.2) {#time-based-media}

[准則1.2基於時間的介質：為基於時間的介質提供替代方案。](https://www.w3.org/TR/WCAG/#time-based-media)

這涉及的Web內容 *基於時間*。 這包括用戶可以播放的內容（例如視頻、音頻和動畫內容），並且可以預先錄制或即時流。

### 僅音頻和僅視頻（預錄）(1.2.1) {#audio-only-and-video-only-prerecorded}

* 成功標準1.2.1
* A級
* 僅音頻和僅視頻（預錄）:對於預錄的純音頻和純視頻媒體，除非音頻或視頻是文本的替代介質，並且明確標籤為：
   * 僅預錄音頻：提供了用於基於時間的媒體的替代方案，其提供用於預錄的僅音頻內容的等效資訊。
   * 僅預錄視頻：提供了用於基於時間的媒體或音頻軌道的替代方案，其提供用於預錄的僅視頻內容的等效資訊。

#### 用途 — 僅音頻和僅視頻（預錄）(1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

視頻和音頻的可訪問性問題可能會通過以下方式出現：

* 沒有原聲帶或原聲帶時，視覺受損者不足以告知視頻或動畫中的情況；
* 聽障者，聾者，聽不到配樂；
* 能聽到原聲帶但不理解正在說什麼的人（例如，因為他們聽不懂的語言）。

使用瀏覽器或設備的用戶也可能無法使用視頻或音頻，這些瀏覽器或設備不支援以特定媒體格式播放內容，如AdobeFlash。

以不同格式提供此資訊(如文本（或無音頻的視頻的音頻）可使無法訪問原始內容的人能夠訪問此資訊。

#### How to Meet — 僅音頻和僅視頻（預錄）(1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* 如果內容是預錄音頻且沒有視頻（如播客）:
   * 在內容之前或之後提供指向音頻內容的文本記錄的連結。 筆錄應是HTML頁面，其文本相當於所有口語和重要的非口語內容，並應包括說話者的指示、設定描述、聲音表達以及任何其他重要音頻的描述。
* 如果內容是動畫或預錄的無音頻視頻：
   * 在內容之前或之後提供連結，以表示視頻所提供資訊的等效文本描述
   * 或者使用常用音頻格式（如MP3）的等效音頻描述。

>[!NOTE]
>
>如果所述音頻或視頻內容被提供為已經存在於同一網頁上的另一種格式的內容的替代，則可能不需要附加的替代。
>
>指南， [瞭解WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)，提供詳細資訊。

將多媒體插AEM入網頁與插入影像類似。 然而，由於多媒體內容遠不止是靜止影像，因此有各種不同的設定和選項來控制多媒體的播放方式。

>[!NOTE]
>
>在將多媒體與資訊內容一起使用時，還必須建立到替代選項的連結。 例如，要包括文本記錄，請建立HTML頁以顯示記錄，然後在音頻內容旁或下添加連結。

#### 詳細資訊 — 僅音頻和僅視頻（預錄）(1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [瞭解成功標準1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [如何滿足成功標1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### 字幕（預錄）(1.2.2) {#captions-prerecorded}

* 成功標準1.2.2
* A級
* 字幕（預錄）:為同步媒體中所有預先錄制的音頻內容提供字幕，除非該媒體是文本的替代媒體並且被清楚地標籤為這樣。

#### 目的 — 字幕（預錄）(1.2.2) {#purpose-captions-prerecorded}

聾人或聽力障礙者無法或難以獲取音頻內容。 字幕是在視頻期間的適當時間在螢幕上顯示的口語和非口語音頻的文本等效項。 它們讓聽不到音頻的人理解正在發生的事情。

#### How to Meet - Captions（預錄）(1.2.2) {#how-to-meet-captions-prerecorded}

字幕可以是：

* 開啟：播放視頻時始終可見
* 關閉：字幕可由用戶開啟或關閉

盡可能使用隱藏字幕，因為這樣用戶就可以選擇是否查看字幕。

對於隱藏字幕，您需要以適當的格式建立並提供同步字幕檔案(如 [SMIL](https://www.w3.org/AudioVideo/))旁邊(有關如何執行此操作的詳細資訊超出本指南的範圍，但我們提供了指向以下部分教程的連結 [詳細資訊 — 字幕（預錄）(1.2.2)](#more-information-captions-prerecorded)。 確保在視頻播放器中提供注釋或啟用字幕功能，以便讓用戶知道字幕可用於視頻。

如果必須使用開放字幕，請將文本嵌入視頻軌道。 這可以通過使用允許將標題疊置到視頻上的視頻編輯應用程式來實現。

#### 詳細資訊 — 字幕（預錄）(1.2.2) {#more-information-captions-prerecorded}

* [瞭解成功標準1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [如何滿足成功標1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### 音頻說明或介質替代（預錄）(1.2.3) {#audio-description-or-media-alternative-prerecorded}

* 成功標準1.2.3
* A級
* 音頻說明或介質替代（預錄）:為同步媒體提供基於時間的媒體或預錄視頻內容的音頻描述的替代方案，除非媒體是文本的替代媒體並且被清楚地標籤為這樣。

#### 用途 — 音頻說明或媒體替代（預錄）(1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

如果視頻或動畫中的資訊僅以視覺方式提供，或者如果背景音樂沒有提供足夠的資訊來讓人們瞭解視覺上正在發生的事情，則盲人或視覺障礙者將體驗無障礙。

#### How to Meet - Audio Description或Media Alternation（預錄）(1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

為了達到這一成功標準，可以採用兩種方法。 兩者皆可接受：

1. 包括視頻內容的其他音頻說明。 這可以通過以下三種方式之一實現：
   * 在現有對話框中暫停期間，提供有關未作為現有音頻軌道一部分呈現的場景更改的資訊；
   * 提供新的、附加的和可選的音頻軌道，其中包含原始音軌，但還包括有關場景更改的附加音頻資訊。
      * 這允許用戶在現有音頻軌道之間切換( *不* 包含音頻說明)和新音頻軌道( *是* 包含音頻說明)。
      * 這防止了不需要附加說明的用戶中斷。
   * 建立視頻內容的第二版本，以允許擴展音頻說明。 這通過在適當點暫停音頻和視頻，減少了在現有對話之間的間隙中提供詳細音頻描述的困難。 因此，在再次開始操作之前，可以給出更長的音頻描述。 如上例所示，最好將其作為可選的附加音頻軌道提供，以防止對不需要附加說明的用戶造成中斷。
1. 提供與視頻或動畫的音頻和視覺元素等價的適當文本文字記錄。 這應當包括，在適當情況下，說明說話者、對設定的描述、視覺上呈現的任何事件或資訊以及聲音表達。 視其長度而定，可以將文字記錄放在視頻或動畫的同一頁面，或放在單獨的頁面上；如果選擇後一個選項，請提供視頻或動畫旁邊的文字記錄的連結。

有關如何建立音頻描述視頻的詳細資訊超出本指南的範圍。 建立視頻和音頻說明可能非常耗時，但其他Adobe產品可幫助完成這些任務。

#### 詳細資訊 — 音頻說明或媒體替代（預錄）(1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [瞭解成功標準1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [如何滿足成功標1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### 字幕（即時）(1.2.4)  {#captions-live}

* 成功標準1.2.4
* AA級
* 字幕（即時）:為同步媒體中的所有即時音頻內容提供字幕。

#### 目的 — 字幕（即時）(1.2.4) {#purpose-captions-live}

此成功標準與 [字幕（預錄）](#captions-prerecorded) 因為它解決了聾人或聽力受損者所經歷的無障礙障礙障礙，但這一成功標準涉及網路廣播等即時演示。

#### How to Meet - Captions(Live)(1.2.4) {#how-to-meet-captions-live}

遵循為 [字幕（預錄）](#captions-prerecorded) 上。 但是，由於媒體的現場性質，必須盡快建立字幕設定，並應對正在發生的情況。 因此，您應考慮使用即時字幕或語音到文本工具。

詳細說明超出了本文檔的範圍，但以下資源提供了有用的資訊：

* [WebAIM:即時字幕](https://www.webaim.org/techniques/captions/realtime.php)

* [AccessComputing項目（華盛頓大學）:能否使用語音識別自動生成字幕？](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### 詳細資訊 — 字幕（即時）(1.2.4) {#more-information-captions-live}

* [瞭解成功標準1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [如何滿足成功標1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### 音頻說明（預錄）(1.2.5)  {#audio-description-prerecorded}

* 成功標準1.2.5
* AA級
* 音頻說明（預錄）:為同步媒體中的所有預錄視頻內容提供音頻描述。

#### 用途 — 音頻說明（預錄）(1.2.5) {#purpose-audio-description-prerecorded}

此成功標準與 [音頻說明或介質替代（預錄）](#audio-description-or-media-alternative-prerecorded)，但作者必須提供更詳細的音頻說明才能符合AA級。

#### How to Meet - Audio Description（預錄）(1.2.5) {#how-to-meet-audio-description-prerecorded}

遵循為 [音頻說明或介質替代（預錄）](#audio-description-or-media-alternative-prerecorded)。

#### 詳細資訊 — 音頻說明（預錄）(1.2.5) {#more-information-audio-description-prerecorded}

* [瞭解成功標準1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [如何滿足成功標1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### 適應性(1.3) {#adaptable}

[准則1.3適應性：建立可以以不同方式（例如更簡單的佈局）呈現的內容，而不會丟失資訊或結構。](https://www.w3.org/TR/WCAG/#adaptable)

本准則涵蓋支援以下人員所需的要求：

* 可能無法訪問作者在該內容的預設演示中展示的資訊（例如，多列佈局或大量使用顏色和/或影像的頁面）。

* 可以使用純音或可選的視覺顯示，如大文本或高對比度。

### 資訊和關係(1.3.1)  {#info-and-relationships}

* 成功標準1.3.1
* A級
* 資訊和關係：通過演示所傳達的資訊、結構和關係可以以寫程式方式確定或以文本形式提供。

#### 目的 — 資訊和關係(1.3.1) {#purpose-info-and-relationships}

殘疾人使用的許多輔助技術依靠結構資訊來有效地顯示或顯示 *瞭解* 內容。 此結構資訊可以採用頁面標題、表行和列標題以及清單類型的形式。 例如，螢幕閱讀器允許用戶在從標題到標題的頁面中導航。 然而，當頁面內容似乎只通過視覺造型而非底層HTML具有結構時，則輔助技術沒有可用的結構資訊，限制了它們支援更方便瀏覽的能力。

這種成功標準的存在是為了確保通過HTML或其他編碼技術以寫程式方式提供這種結構資訊，以便瀏覽器和輔助技術能夠訪問和利用這些資訊。

#### 如何會面 — 資訊和關係(1.3.1) {#how-to-meet-info-and-relationships}

使用AEM適當的HTML元素可輕鬆構建語義上有意義的Web內容。 在RTE（文本元件）中開啟頁面內容，然後使用 **參數格式** 菜單（段落符號），以指定相應的結構元素（例如段落、標題等）。

在適用情況下，可使用下列元素確保為網頁指定適當的結構：

* **標題：** 只要您啟用了RTE的輔助功能，就會提AEM供3級頁面標題。 您可以使用這些項目來識別內容的區段和子區段。標題1是標題的最高級別，標題3是最低級別。系統管理員可以配置系統以允許使用更多標題級別。

* **清單**:可以使用HTML指定三種不同的清單類型：
   * 元素 `<ul>` 用於無序 *列*  (項目符號) 清單。使用元素來識別個別清 `<li>` 單項目。在RTE中，使用「項目符號列 **表」表徵圖** 。
   * 的 `<ol>` 元素用於 *編號* 清單。 使用 `<li>` 的子菜單。 在RTE中，使用 **編號清單** 表徵圖

   如果要將現有內容更改為特定清單類型，請突出顯示相應的文本並選擇相應的清單類型。 如前面顯示如何輸入段落文本的示例所示，相應的清單元素將自動添加到您的HTML中。

   在全螢幕模式中，會顯示個別 **的「項目符號清單** 」和「 **** 編號清單」圖示。當未處於全螢幕模式時，單一「清單」圖示後面會提供這兩個 **選項** 。

* **表**:必須使用HTML表元素標識資料表：
   * 一個 `<table>` 元素
   * a `<tr>` 表中每行的元素
   * a `<th>` 每行和列標題的元素
   * a `<td>` 每個資料單元格的元素

   此外，可訪問的表還使用以下元素和屬性：

   * 的 `<caption>` 元素用於為表提供可見的標題。 預設情況下，字幕顯示在表格的中心位置，但可以使用CSS進行適當定位。 字幕以寫程式方式與表相關聯，因此它是提供內容介紹的有用方法。
   * 的 `<summary>` 元素通過提供有視力的用戶能夠看到的內容的概要，幫助無視的用戶更輕鬆地理解表中顯示的資訊。 在使用複雜或非常規表佈局時，這特別有用（此屬性不顯示在瀏覽器中，它只讀於輔助技術）。
   * 的 `scope` 屬性 `<th>` 元素用於指示單元格是否代表特定行的標題或特定列的標題。 類似的方法是在複雜表中使用頭和id屬性，其中資料單元可與一個或多個頭相關聯。

   >[!NOTE]
   >
   >預設情況下，這些元素和屬性不直接可用，儘管系統管理員可以在 **表屬性** 對話框，請參閱 [添加對附加HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)。

   開啟 **表格** 對話框，您可以在其中選擇 **表屬性** 頁籤：

   * 定義適當的 **標題**。
   * 理想情況下，請移除「寬 **度」、「邊框高度」、「邊框高度」、「邊框高度**」、「單元格間距」、「單元格間距 **」、「單元格**************&#x200B;間距」的預設值。因為這些屬性可以在全局樣式表中設定。

   然後，您可以使用 **單元格屬性** 要選擇單元格是資料單元格還是標題單元格：

* **強調**:使用 `<strong>` 或 `<em>` 指示強調的元素。 請勿使用標題來反白標示段落中的文字。
   * 突出顯示要強調的文本；
   * 按一下「屬性」面板中顯示的 **B** 表徵圖( `<strong>`for)或「屬性」面板中顯示 **的「I** 」表徵圖(for `<em>`)(請確定已選 **** 中HTML)。

      >[!NOTE]
      >
      >標準安裝中AEM的RTE設定為使用：
      >
      >* `<b>` 代表 `<strong>`
      >* `<i>` 代表 `<em>`

      >
      >它們實際上是一樣的，但 `<strong>` 和 `<em>` 是最好的，因為它們在語義上是正確的html。 您的開發團隊可以配置RTE以使用 `<strong>` 和 `<em>` (而不是 `<b>` 和 `<i>`)。

* **複雜的資料表**:在某些情況下，如果有具有兩個或多個標題級別的複雜表，則基本表屬性可能不足以提供所有必要的結構資訊。對於這些類型的複雜表格，需要使用header和 **id屬性在標題及其相關儲存格之間建** 立直 **接** 關係。

   >[!NOTE]
   >
   >id屬性在出廠安裝中不可用。 可以通過在RTE中配置HTML規則和序列化程式來啟用它。

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

   要在中實現AEM此目的，必須使用源編輯模式直接添加標注。

   >[!NOTE]
   >
   >此功能在標準安裝中不能立即使用。 它需要配置RTE、HTML規則和序列化程式。

#### 詳細資訊 — 資訊和關係(1.3.1) {#more-information-info-and-relationships}

* [瞭解成功標準1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [如何滿足成功標1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### 有意義的序列(1.3.2)  {#meaningful-sequence}

* 成功標準1.3.2
* A級
* 有意義的序列：當呈現內容的序列影響其含義時，可以寫程式地確定正確的讀取序列。

#### 目的 — 有意義的序列(1.3.2) {#purpose-meaningful-sequence}

此成功標準的目的是使用戶代理能夠提供內容的替代呈現，同時保留理解含義所需的閱讀順序。 必須能夠以寫程式方式確定至少一個有意義的內容序列。 當輔助技術以錯誤的順序讀取內容或當應用替代樣式表或其他格式更改時，不符合此成功標準的內容可能會迷惑用戶或使用戶不定向。

#### 如何相遇 — 有意義的序列(1.3.2) {#how-to-meet-meaningful-sequence}

遵循以下指南 [如何滿足成功標1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)。

#### 詳細資訊 — 有意義的序列(1.3.2) {#more-information-meaningful-sequence}

* [瞭解成功標準1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [如何滿足成功標1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### 感官特徵(1.3.3)  {#sensory-characteristics}

* 成功標準1.3.3
* A級
* 感官特徵：為理解和操作內容而提供的說明不僅依賴於部件的感官特徵，如形狀、大小、視覺位置、方向或聲音。

#### 目的 — 感官特性(1.3.3) {#purpose-sensory-characteristics}

設計人員在展示資訊時通常關注視覺設計特徵，如顏色、形狀、文本樣式或內容的絕對或相對位置。 這些設計技術在傳遞資訊方面可以非常強大（並且可以改善有認知可達性需求的有視力用戶的總體可訪問性），但是盲人或視力受損者可能無法訪問需要視覺識別位置、顏色或形狀等屬性的資訊。

同樣，需要區分不同聲音（例如，男性或女性口語內容）的資訊，如果沒有反映在音頻內容的任何文本替代中，將給聽力受損者帶來無障礙障礙。

>[!NOTE]
>
>有關顏色替代品的要求，請參閱 [顏色的使用](#use-of-color)。

#### 如何滿足 — 感官特性(1.3.3) {#how-to-meet-sensory-characteristics}

確保還以替代格式顯示依賴於頁面內容視覺特徵的任何資訊。

* 不要依靠視覺定位來提供資訊。 例如，如果要將用戶引導到頁面右側的菜單，以便訪問更多資訊，請不要引用 *右邊的菜單*;而是將菜單命名（例如，通過標題）並在文本中引用該名稱。
* 不要依賴文本樣式（例如，粗體或斜體文本）作為傳遞資訊的唯一方式。

>[!NOTE]
>
>如果理解描述性術語在非視覺上下文中具有含義，則使用描述性術語將是可接受的。 例如，使用 *上* 和 *下* 通常可以接受，因為它們分別暗示某一內容項之前和之後的內容；當內容被大聲說出來時，這仍然有意義。

#### 更多資訊 — 感官特性(1.3.3) {#more-information-sensory-characteristics}

* [瞭解成功標準1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [如何滿足成功標1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### 可區分(1.4) {#distinguishable}

[准則1.4可區分：使用戶更容易查看和聽取內容，包括將前景與背景分開。](https://www.w3.org/TR/WCAG/#distinguishable)

### 顏色的使用(1.4.1)  {#use-of-color}

* 成功標準1.4.1
* A級
* 顏色的使用：顏色不是傳遞資訊、指示動作、提示響應或區分可視元素的唯一視覺手段。

>[!NOTE]
>
>此成功標準特別針對顏色感知。 其他形式的感知 [適應性(1.3)](#adaptable);包括對顏色的寫程式訪問和其他視覺呈現編碼。

#### 用途 — 顏色的使用(1.4.1) {#purpose-use-of-color}

顏色是提高網頁審美感的一種有效途徑，在資訊傳遞方面也是有用的。 但是，從盲目性到彩色視覺缺陷，都存在著一系列視覺缺陷，這意味著有些人無法分辨出某些顏色。 這使得顏色編碼成為提供資訊的不可靠方式。

例如，有紅綠色視覺缺陷的人，將無法區分綠色和紅色。 他們可能將這兩種顏色都視為第三種顏色（例如，棕色），在這種情況下，他們將無法區分紅色、綠色和棕色。

此外，使用純文字檔案瀏覽器、單色顯示設備或查看頁面黑白打印輸出的人無法感知顏色。

進一步考慮是 *選定* 介面元素的狀態（例如，制表符、切換按鈕等），它需要以某種方式傳達，而不僅僅是使用顏色，而且不僅僅是視覺呈現。 對於這些元素，當建立不依賴特定感知的完全包容的用戶體驗時，對模式、形狀和寫程式資訊的額外使用會有所幫助。

#### 如何相遇 — 顏色的使用(1.4.1) {#how-to-meet-use-of-color}

無論使用顏色來傳遞資訊，都要確保資訊可用而無需查看顏色。

例如，確保在文本中也明確提供由顏色提供的資訊。

如果顏色用作提供資訊的提示，則應提供附加的視覺提示，如更改樣式（如粗體、斜體）或字型。 這有助於視力低或視力不足的人識別資訊。 但是，它不能完全靠得住，因為它根本無助於看不到頁面的人。 因此，（有時）提供隱藏的文本或使用寫程式解決方案是有用的，例如 [可訪問的富Internet應用程式(ARIA)Web標準套件](https://www.w3.org/WAI/standards-guidelines/aria/)，將此資訊傳達給無視的用戶。

#### 詳細資訊 — 顏色的使用(1.4.1) {#more-information-use-of-color}

* [瞭解成功標準1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [如何滿足成功標1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### 音頻控制(1.4.2)  {#audio-control}

* 成功標準1.4.2
* A級
* 音頻控制：如果網頁上的任何音頻自動播放超過3秒，則可以使用機制來暫停或停止音頻，或者可以使用機制來獨立於整個系統音量級別控制音頻音量。

#### 用途 — 音頻控制(1.4.2) {#purpose-audio-control}

使用螢幕閱讀軟體的個人如果同時有其他音頻播放，則很難聽到語音輸出。 當螢幕閱讀器的語音輸出是基於軟體（如今大多數情況一樣）並通過與聲音相同的音量控制來控制時，這一困難就會加劇。 此外，一些認知障礙者和神經發散者可能具有聲音敏感性。 這些人將發現無法更改音頻內容的音量級別會造成很大干擾。

因此，用戶能夠關閉背景聲音是非常重要的。

>[!NOTE]
>
>控制音量包括能夠將其音量減小到零。

#### 如何見面 — 音頻控制(1.4.2) {#how-to-meet-audio-control}

遵循以下指南 [如何滿足成功標1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)。

#### 詳細資訊 — 音頻控制(1.4.2) {#more-information-audio-control}

* [瞭解成功標準1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [如何滿足成功標1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### 對比度（最小值）(1.4.3) {#contrast-minimum}

* 成功標準1.4.3
* AA級
* 對比度（最小值）:文本和文本影像的視覺呈現具有至少4.5:1的對比度，以下除外：
   * 大文本：大規模文本和大規模文本的影像具有至少3:1的對比度。
   * 附帶：作為非活動用戶介面元件的一部分的文本或影像， [純裝](https://www.w3.org/TR/WCAG/#dfn-pure-decoration)，對於任何人都不可見，或者是包含顯著其他視覺內容的圖片的一部分，沒有對比度要求。
   * 邏輯類型：作為徽標或品牌名稱一部分的文本沒有最低對比度要求。

   >[!NOTE]
   >
   >請參閱 [瞭解非文本對比度](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) 有關詳細資訊，請幫助確保內容作者瞭解非文本元素（包括表徵圖、介面元素等）的附加要求。

#### 用途 — 對比度（最小值）(1.4.3) {#purpose-contrast-minimum}

某些視覺缺陷的人可能無法區分某些低對比度顏色對。 如果出現以下情況，則這些人員可能會出現可訪問性問題：

* 文字與背景顏色對比較差。
* 文本（如連結文本和非連結文本）的顏色編碼在識別資訊中是很重要的。

>[!NOTE]
>
>純用於裝飾目的的文本不在此成功標準中。

#### 如何碰合 — 對比度（最小值）(1.4.3) {#how-to-meet-contrast-minimum}

確保文本與其背景充分對比。 對比度取決於所討論文本的大小和樣式：

* 對於大小小於18點（或14點粗體）的文本，文本/影像與背景之間的對比度應至少為4.5:1。
* 對於大小至少為18點（或14點粗體）的文本，對比度應至少為3:1。
* 如果對背景進行陣列，則應對任何文本週圍的背景進行著色，以保持4.5:1或3:1比例。

>[!NOTE]
>
>請記住，字型在呈現等效PT/PX/EM大小時可能有所不同。
>
>建議在為Web內容選擇適當字型和調整大小時，在可讀性和可用性方面使用良好的判斷和錯誤。

>[!NOTE]
>
>以下站點可幫助轉換到其他單位：
>
>* [Px到Em計算器 — Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* [字型大小轉換：像素點 — em-rem百分比](https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/)
>* [PMtoEM.com:PX到EM的轉換變得簡單](http://pxtoem.com)


要檢查對比度，請使用顏色對比度工具，如 [Paciello組顏色對比分析儀](https://www.paciellogroup.com/resources/contrast-analyser.html) 或 [WebAIM顏色對比度檢查器](https://www.webaim.org/resources/contrastchecker/)。 這些工具允許您檢查顏色對並報告任何對比度問題。

或者，如果您不太關心指定頁面的外觀，則可以選擇不指定背景和前景文本顏色。 無需進行對比度檢查，因為用戶的瀏覽器將確定文本和背景的顏色。

如果無法滿足建議的對比度級別，則需要提供指向頁面的替代等效版本（沒有顏色對比度問題）的連結，或允許用戶根據自己的要求調整頁面顏色方案的對比度。

#### 詳細資訊 — 對比度（最小值）(1.4.3) {#more-information-contrast-minimum}

* [瞭解成功標準1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [如何滿足成功標1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### 調整文本大小(1.4.4)  {#resize-text}

* 成功標準1.4.4
* A級
* 調整文本大小：除了文本的字幕和影像外，在不使用輔助技術的情況下，文本的大小可調整200%，而不會丟失內容或功能。

#### 用途 — 調整文本大小(1.4.4) {#purpose-resize-text}

此成功標準的目的是確保以可視方式呈現文本，包括基於文本的控制項(已顯示的文本字元，以便可以看到它們 [與仍以資料格式（如ASCII）顯示的文本字元])可以成功地縮放，以便具有輕微視覺殘疾的人可以直接閱讀，而不需要使用輔助技術，如螢幕放大鏡。 用戶可以從擴展網頁上的所有內容中獲益，但文本是最關鍵的。

#### 如何會面 — 調整文本大小(1.4.4) {#how-to-meet-resize-text}

並遵循以下准則： [如何滿足成功標1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) 您可以鼓勵內容作者在其頁面設計和字型大小（例如，響應性Web設計）中使用流暢、靈活的寬度和高度，使讀者能夠調整文本的大小。

#### 詳細資訊 — 調整文本大小(1.4.4) {#more-information-resize-text}

* [瞭解成功標準1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [如何滿足成功標1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### 文本影像(1.4.5) {#images-of-text}

* 成功標準1.4.5
* AA級
* 文本影像：如果所使用的技術能夠實現視覺呈現，則文本用於傳遞資訊而不是文本的影像，以下除外：
   * 可自定義：文本影像可以根據用戶的需求進行可視化定製；
   * 基本：對所傳達的資訊而言，文本的具體呈現至關重要。

>[!NOTE]
>
>Logotypes（屬於徽標或品牌名稱的文本）被認為是必不可少的。

#### 目的 — 文本影像(1.4.5) {#purpose-images-of-text}

當選擇特定文本樣式時，通常使用文本影像；例如，logotype或如果文本是從另一個源生成的（例如，掃描紙面文檔）。 但是，與使用HTML和CSS樣式顯示的文本相比，文本影像缺乏更改視覺障礙或閱讀困難者可能需要的大小或外觀的靈活性。

#### 如何碰面 — 文本影像(1.4.5) {#how-to-meet-images-of-text}

如果必須使用文本影像，則使用CSS將文本影像替換為HTML中的等效文本，以便文本能夠以可自定義的方式可用。 有關如何實現此目標的示例，請參閱 [C30:使用CSS將文本替換為文本影像並提供用戶介面控制項以切換](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30)。

#### 詳細資訊 — 文本影像(1.4.5) {#more-information-images-of-text}

* [瞭解成功標準1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [如何滿足成功標1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## 原則2:可操作 {#principle-operable}

[原則2:可操作 — 用戶介面元件和導航必須可操作。](https://www.w3.org/TR/WCAG/#operable)

### 鍵盤可訪問(2.1) {#keyboard-accessible}

[指南2.1鍵盤可訪問：使所有功能都可從鍵盤獲得。](https://www.w3.org/TR/WCAG/#keyboard-accessible)

這涉及確保用戶可以使用鍵盤訪問所有功能。

### 鍵盤(2.1.1)  {#keyboard}

* 成功標準2.1.1
* A級
* 鍵盤：所述內容的所有功能可通過鍵盤介面操作而不需要用於單個擊鍵的特定定時，除非其基礎功能需要取決於用戶移動的路徑而不是僅僅取決於端點的輸入。

#### 用途 — 鍵盤(2.1.1) {#purpose-keyboard}

此成功標準的目的是確保盡可能通過鍵盤或鍵盤介面來操作內容（以便使用備用鍵盤）。 當內容可以通過鍵盤或備用鍵盤操作時，無視力的人（不能使用需要手形協調的滑鼠等設備的人），以及必須使用備用鍵盤或作為鍵盤模擬器的輸入設備的人，都可操作內容。 鍵盤模擬器包括語音輸入軟體、吸音軟體、螢幕鍵盤、掃描軟體以及各種輔助技術和備用鍵盤。 視力低的個體在跟蹤指針時可能也會遇到困難，如果能夠從鍵盤控制指針，則發現使用軟體會容易得多（或只可能）。

#### 如何碰頭 — 鍵盤(2.1.1) {#how-to-meet-keyboard}

遵循以下指南 [如何滿足成功標2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)。

#### 詳細資訊 — 鍵盤(2.1.1) {#more-information-keyboard}

* [瞭解成功標準2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何滿足成功標2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### 無鍵盤陷印(2.1.2)  {#no-keyboard-trap}

* 成功標準2.1.2
* A級
* 無鍵盤陷印：如果可以使用鍵盤介面將鍵盤焦點移動到頁面的元件，則只使用鍵盤介面就可以將焦點移離該元件，並且如果它需要多於未修改的箭頭鍵或制表鍵或其他標準退出方法，則建議用戶使用將焦點移離的方法。

#### 用途 — 無鍵盤陷印(2.1.2) {#purpose-no-keyboard-trap}

此成功標準的目的是確保內容不 *陷阱* 鍵盤焦點位於網頁內容的子部分內。 當在頁面中組合多種格式並使用插件或嵌入式應用程式呈現時，這是一個常見問題。

有時網頁的功能將焦點限制在內容的子節（例如，模式對話）。 在這種情況下，您應提供一種方法，讓用戶能夠退出該內容子部分（例如，ESC鍵關閉模式對話框，或關閉按鈕關閉模式對話框）。

#### 如何碰頭 — 無鍵盤陷印(2.1.2) {#how-to-meet-no-keyboard-trap}

遵循以下指南 [如何滿足成功標2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)。

#### 詳細資訊 — 無鍵盤陷印(2.1.2) {#more-information-no-keyboard-trap}

* [瞭解成功標準2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何滿足成功標2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### 足夠的時間(2.2) {#enough-time}

[准則2.2足夠時間：為用戶提供足夠的時間來閱讀和使用內容。](https://www.w3.org/TR/WCAG/#enough-time)

這涉及確保用戶有足夠的時間閱讀並採取行動。

### 時序可調(2.2.1)  {#timing-adjustable}

* 成功標準2.2.1
* A級
* 鍵盤：為用戶提供足夠的時間來閱讀和使用內容。

#### 目的 — 時序可調(2.2.1) {#purpose-timing-adjustable}

本成功標準旨在確保為殘疾用戶提供足夠的時間，盡可能與Web內容進行交互。 失明、低視力、靈巧性缺陷和認知限制等殘疾人可能需要更多時間閱讀內容或執行填寫線上表格等功能。 如果Web功能與時間相關，則某些用戶在出現時間限制之前將很難執行所需的操作。 這可能使服務無法訪問。 設計不依賴於時間的功能將有助於殘疾人成功完成這些功能。 提供選項以禁用時間限制、自定義時間限制的長度或請求在時間限制發生之前的更多時間，有助於那些需要比預期時間更長的用戶成功完成任務。 這些選項按對用戶最有幫助的順序列出。 禁用時間限制比自定義時間限制的長度要好，這比在時間限制出現之前請求更多時間要好。

#### 如何滿足 — 時序可調(2.2.1) {#how-to-meet-timing-adjustable}

遵循以下指南 [如何滿足成功標2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)。

#### 詳細資訊 — 可調整計時(2.2.1) {#more-information-timing-adjustable}

* [瞭解成功標準2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [如何滿足成功標2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### 暫停、停止、隱藏(2.2.2)  {#pause-stop-hide}

* 成功標準2.2.2
* A級
* 暫停、停止、隱藏：對於移動、閃爍、滾動或自動更新資訊，以下是真的：
   * 移動、閃爍、滾動：對於(a)自動啟動的任何移動、閃爍或滾動資訊，(b)持續超過五秒，(c)與其他內容並行顯示，有一種機制供用戶暫停、停止或隱藏資訊，除非移動、閃爍或滾動是必要活動的一部分；
   * 自動更新：對於(a)自動啟動和(b)與其他內容並行顯示的任何自動更新資訊，用戶有暫停、停止或隱藏更新或控制更新頻率的機制，除非自動更新是必要活動的一部分。

注意事項有：

1. 有關閃爍或閃爍內容的要求，請參閱「Don Design Content in a What is Knowd to Cause Contures(2.3)(不以已知導致檢獲的方式設計內容(2.3))」。
1. 由於任何不符合此成功標準的內容都可能干擾用戶使用整個頁面的能力，因此網頁上的所有內容（無論是否用於滿足其他成功標準）都必須符合此成功標準。 請參閱 [符合性要求5:無干擾](https://www.w3.org/TR/WCAG20/#cc5)。
1. 不需要由軟體定期更新或被流式傳輸到用戶代理的內容來保留或呈現在暫停開始和恢復演示之間生成或接收的資訊，因為這在技術上可能不可能，並且在許多情況下可能誤導這樣做。
1. 如果在預載入階段或類似情況中不能發生交互，並且如果不指示進度，可能會迷惑用戶或導致他們認為內容已凍結或斷開，則可以認為動畫是必不可少的。

#### 目的 — 暫停、停止、隱藏(2.2.2) {#purpose-pause-stop-hide}

某些用戶可能會發現移動內容會分散注意力，甚至會讓人感到痛苦，這使得他們很難集中精力處理頁面的其他部分。 此外，對於那些無法跟上移動文本的人來說，這些內容可能很難閱讀。

#### 如何見面 — 暫停、停止、隱藏(2.2.2) {#how-to-meet-pause-stop-hide}

根據內容的性質，在建立包含移動、閃爍或閃爍內容的網頁時，可以應用以下一個或多個建議：

* 提供暫停滾動內容的方法，以給用戶足夠的時間來讀取內容。 例如，新聞標題欄、自動更新的文本和自動升級的影像線。
* 確保連結內容在五秒後停止閃爍。
* 使用適當的技術來顯示可由瀏覽器禁用的移動或閃爍內容。 例如，圖形交換格式(GIF)或動畫可移植網路圖形(APNG)檔案。
* 在網頁上提供表單控制項，允許用戶禁用頁面上的所有移動或閃爍內容。
* 如果上述任一項不可能，請提供指向包含所有內容但不移動或閃爍的頁面的連結。

#### 詳細資訊 — 暫停、停止、隱藏(2.2.2) {#more-information-pause-stop-hide}

* [瞭解成功標準2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [如何滿足成功標2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### 癲癇和生理反應(2.3) {#seizures-and-physcial-reactions}

[准則2.3緝獲量：不要以已知會引起癲癇或身體反應的方式設計內容。](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### 三個Flash或低於閾值(2.3.1) {#three-flashes-or-below-threshold}

* 成功標準2.3.1
* A級
* 三個Flash或低於閾值：網頁中不包含在任何一秒週期內閃爍三次以上的內容，或者閃爍低於一般閃爍閾值和紅色閃爍閾值。

>[!NOTE]
>
>由於任何不符合此成功標準的內容都可能干擾用戶使用整個頁面的能力，因此網頁上的所有內容（無論是否用於滿足其他成功標準）都必須符合此成功標準。 請參閱 [符合性要求5:無干擾](https://www.w3.org/TR/WCAG/#cc5)。

#### 目的 — 三個Flash或低於閾值(2.3.1) {#purpose-three-flashes-or-below-threshold}

在某些情況下，閃爍的內容可能導致感光性癲癇。 此成功標準允許這些用戶訪問和體驗所有內容，而無需擔心內容閃爍。

#### 如何碰頭 — 三個Flash或低於閾值(2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

應採取步驟確保應用以下技術：

* 確保元件在任何一秒鐘內閃爍不超過三次；
* 如果無法滿足上述條件，則在 *小安全區* 像素。 此區域使用複雜公式計算，覆蓋於 [G176:保持閃蒸區足夠小](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)因此，只有在閃爍內容為 *絕對* 必要。

#### 更多資訊 — 三個Flash或低於閾值(2.3.1) {#more-information-three-flashes-or-below-threshold}

* [瞭解成功標準2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [如何滿足成功標2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### 可導航(2.4) {#navigable}

[准則2.4可導航：提供幫助用戶導航、查找內容和確定其位置的方法。](https://www.w3.org/TR/WCAG/#navigable)

這涉及確保內容易於用戶瀏覽且簡單易用。

### 旁路塊(2.4.1)  {#bypass-blocks}

* 成功標準2.4.1
* A級
* 繞過塊：一種機制可用於繞過在多個網頁上重複的內容塊。

#### 用途 — 旁路塊(2.4.1) {#purpose-bypass-blocks}

此成功標準的目的是允許順序瀏覽內容的人員更直接地訪問網頁的主要內容。 網頁和應用程式通常包含顯示在其他頁面或螢幕上的內容。 重複內容塊的示例包括但不限於導航連結、標題圖形、菜單和廣告幀。 為本規定的目的，諸如單個單詞、短語或單個連結等重複的小節不被視為塊。

#### 如何碰頭 — 繞過塊(2.4.1) {#how-to-meet-bypass-blocks}

遵循以下指南 [如何滿足成功標2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)。

#### 詳細資訊 — 旁路塊(2.4.1) {#more-information-bypass-blocks}

* [瞭解成功標準2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [如何滿足成功標2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### 標題為(2.4.2)的頁  {#page-titled}

* 成功標準2.4.2
* A級
* 標題為：網頁的標題描述主題或目的。

#### 目的 — 標題為(2.4.2)的頁 {#purpose-page-titled}

此成功標準可幫助每個人快速識別網頁內容，而不必閱讀該頁面。 當在瀏覽器頁籤中開啟多個網頁時，這特別有用，因為該頁籤中顯示了頁面標題，因此可以快速定位。

#### 如何見面 — 標題為(2.4.2)的頁 {#how-to-meet-page-titled}

在中建立新HTML頁AEM時，可以指定頁標題。 確保標題充分描述了頁面的內容和用途，特別是所有獨特的方面，以便訪問者能夠快速確定內容是否與其需求實際相關。

編輯頁面時，您也可以編輯頁面標題，頁面資訊——屬 **性可****存取。**

#### 詳細資訊 — 標題為(2.4.2)的頁 {#more-information-page-titled}

* [瞭解成功標準2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [如何滿足成功標2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### 焦點順序(2.4.3)  {#focus-order}

* 成功標準2.4.3
* A級
* 焦點順序：如果網頁可以按順序導航並且導航序列影響意義或操作，則可聚焦元件以保持含義和可操作性的順序接收焦點。

#### 目的 — 焦點順序(2.4.3) {#purpose-focus-order}

此成功標準的目的是確保當用戶按順序瀏覽內容時，他們會按與內容含義一致的順序遇到資訊，並且可以從鍵盤操作。 這通過讓用戶形成內容的一致心理模型來減少混淆。 可能有不同的順序反映內容中的邏輯關係。 例如，在由多個欄位和/或步驟組成的聯機表單中移動元件反映內容中的邏輯關係。

#### 如何見面 — 焦點順序(2.4.3) {#how-to-meet-focus-order}

遵循以下指南 [如何滿足成功標2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)。

#### 詳細資訊 — 焦點順序(2.4.3) {#more-information-focus-order}

* [瞭解成功標準2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [如何滿足成功標2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### 連結用途（上下文）(2.4.4)  {#link-purpose-in-context}

* 成功標準2.4.4
* A級
* 連結用途（在上下文中）:每個連結的目的可以單獨從連結文本中確定，也可以從連結文本連同其以寫程式方式確定的連結上下文一起確定，除非在通常情況下連結的目的對用戶是不明確的。

#### 目的 — 連結目的（在上下文中）(2.4.4) {#purpose-link-purpose-in-context}

對所有用戶來說，無論有何損害，通過適當的連結文本明確指示連結的方向至關重要。 這有助於用戶確定他們是否真的想跟隨連結。 對於有目光的用戶，當頁面上有多個連結時（尤其是當頁面上有大量文本時），有意義的連結文本非常有用，因為有意義的連結文本可以更清楚地顯示目標頁面的功能。 一些輔助技術的用戶可以在一個頁面上生成所有連結的清單，如果連結文本既獨特又資訊豐富，則可以更容易地從上下文中理解連結文本。 然而，如果一個連結無法提供足夠的資訊來準確描述連結將帶給他們的位置，那麼有視力的認知障礙個體可能會變得困惑。

#### How to Meet — 連結目的（在上下文中）(2.4.4) {#how-to-meet-link-purpose-in-context}

最重要的是，確保連結的目的在連結的文本中已明確說明。

* 錯誤示例：
   * 文本：有關2010年秋季晚間課程的詳細資訊，請按一下這裡。
   * 原因：它沒有明確無誤地指明目的地。
* 好示例：
   * 文本：2010年秋季的晚間課程 — 詳情。
   * 原因：通過略微調整文本和連結元素的位置，可以改進連結文本：

連結應在各頁上使用一致的措辭，尤其是對於導航欄。 例如，如果指定了指向特定頁的連結 **出版物** 在一頁上，使用其他頁上的文本來確保一致性。

在編寫本文時，在使用標題屬性時存在一些問題，以確保頁面上顯示的類似連結提供有關目標的唯一資訊（例如，「閱讀更多內容」通常指一系列不同的目標）:

* 標題屬性中包含的文本通常僅作為工具提示彈出窗口供滑鼠用戶使用，並且不能使用鍵盤或移動用戶一致地訪問。
* 螢幕閱讀器可以讀出標題屬性，但預設情況下可能無法啟用此功能；因此用戶可能不知道標題屬性存在。
* 很難改變標題文本的外觀，這意味著有些人可能很難或無法閱讀。

因此，雖然標題屬性可用於為連結提供額外的上下文，但要瞭解其局限性，不要將其用作適當的連結文本的替代項。

如果連結由影像組成，請確保該影像的替代文本描述了連結的目標。 例如，如果將書架的影像設定為指向個人出版物的連結，則應閱讀替代文本 **約翰·史密斯的出版物** 不 **書架**。

或者，如果連結錨點除了影像元素之外還包含描述連結用途的文本（因此文本會顯示在影像旁邊），請為影像使用空alt屬性：

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>上面的代碼段是圖，建議使用 **影像** 元件。

雖然建議提供標識連結目的的連結文本而不需要額外的上下文，但人們認識到這並非總是可能的。 上下文自由連結可用於以下情況，其HTML示例可在 [如何滿足成功標2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)。

* 其中連結文本是緊密相關連結清單的一部分，並且包含連結的清單項提供了足夠的上下文。
* 當連結的目的可以從 *前* （非下文）段文本。
* 如果連結包含在資料表中，因此可以從相關標題中明確地識別目的。
* 如果連結清單包含在一組標題中，則標題本身提供了合適的上下文。
* 其中，連結清單包含在嵌套連結中，而嵌套連結上方的父清單項提供了合適的上下文。

在某些情況下，如果頁面上有多個連結（每個連結都以複雜但必要的詳細資訊提供連結的方向），則最好提供顯示完全相同內容但連結文本不如此詳細的網頁替代版本。

或者，可以使用指令碼，使得在連結本身內提供最少量的文本，但是當激活定位在頁面頂部的適當控制項時，連結文本是 *擴展* 進一步細節。 類似的方法是使用CSS *隱藏* 可視用戶的完整連結，但仍將其全部輸出給螢幕閱讀器用戶。 這不屬於本文檔的範圍，但有關如何實現此目標的詳細資訊，請參閱 [更多資訊 — 連結目的（在上下文中）(2.4.4)](#more-information-link-purpose-in-context) 的子菜單。

#### 更多資訊 — 連結目的（在上下文中）(2.4.4) {#more-information-link-purpose-in-context}

* [瞭解成功標準2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [如何滿足成功標2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### 多路(2.4.5)  {#multiple-ways}

* 成功標準2.4.5
* AA級
* 多種方式：除了網頁是進程的結果或步驟之外，在一組網頁中可以找到多個網頁。

#### 目的 — 多種方式(2.4.5) {#purpose-multiple-ways}

此成功標準的目的是使用戶能夠以最能滿足其需要的方式查找內容。 用戶可能發現一種技術比另一種技術更容易或更容易理解。

即使是小型網站，也應該為用戶提供一些定位手段。 對於三、四頁的網站，如果所有頁面都從首頁連結起來，則只需提供從首頁到首頁的連結即可，其中首頁上的連結也可以用作網站地圖。

#### How to Meet - Multiple Ways(2.4.5) {#how-to-meet-multiple-ways}

遵循以下指南 [如何滿足成功標2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)。

#### 詳細資訊 — 多種方式(2.4.5) {#more-information-multiple-ways}

* [瞭解成功標準2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [如何滿足成功標2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### 標題和標籤(2.4.6)  {#headings-and-labels}

* 成功標準2.4.6
* AA級
* 標題和標籤：標題和標籤描述主題或用途。

#### 用途 — 標題和標籤(2.4.6) {#purpose-headings-and-labels}

此成功標準旨在幫助用戶瞭解網頁中包含哪些資訊以及這些資訊是如何組織的。 當標題清晰、描述性強時，用戶可以更輕鬆地找到自己想要的資訊，並且更容易理解內容不同部分之間的關係。 描述性標籤可幫助用戶識別內容中的特定元件。

#### 如何會合 — 標題和標籤(2.4.6) {#how-to-meet-headings-and-labels}

遵循以下指南 [如何滿足成功標2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)。

#### 詳細資訊 — 標題和標籤(2.4.6) {#more-information-headings-and-labels}

* [瞭解成功標準2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [如何滿足成功標2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### 焦點可見(2.4.7)  {#focus-visible}

* 成功標準2.4.7
* AA級
* 焦點可見：任何可操作鍵盤的用戶介面具有操作模式，其中鍵盤焦點指示器是可見的。

#### 目的 — 焦點可見(2.4.7) {#purpose-focus-visible}

此成功標準的目的是幫助人們知道哪個元素具有鍵盤焦點。

人必須能夠知道多個元素中的哪個元素具有鍵盤焦點。 如果螢幕上只有一個鍵盤可操作控制項，則會滿足成功標準，因為可視設計只顯示一個鍵盤可操作項。

如果成功標準上寫有「操作模式」，則說明了可能並不總是顯示焦點指示器的平台。 在大多數情況下，只有一種操作模式，因此此成功標準適用。

#### 如何見面 — 焦點可見(2.4.7) {#how-to-meet-focus-visible}

遵循以下指南 [如何滿足成功標2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)。

#### 詳細資訊 — 焦點可見(2.4.7) {#more-information-focus-visible}

* [瞭解成功標準2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [如何滿足成功標2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## 原則3:可以理解 {#principle-understandable}

[原則3:可理解 — 資訊和用戶介面的操作必須可理解。](https://www.w3.org/TR/WCAG/#understandable)

### 使文本內容可讀且可理解(3.1) {#make-text-content-readable-and-understandable}

[准則3.1可讀：使文本內容可讀且易於理解。](https://www.w3.org/TR/WCAG/#readable)

### 頁面語言(3.1.1) {#language-of-page}

* 成功標準3.1.1
* A級
* 頁面語言：每個網頁的預設人工語言可以寫程式確定。

#### 目的 — 頁面語言(3.1.1) {#purpose-language-of-page}

此成功標準的目的是確保正確呈現文本和其他語言內容。 對於螢幕閱讀器用戶，這可確保內容被正確讀取，而視覺瀏覽器更有可能正確顯示某些字元集。

#### How to Meet - Language of Page(3.1.1) {#how-to-meet-language-of-page}

為滿足此成功標準，可以使用 `lang` 屬性 `<html>` 元素。 例如：

* 如果用英文書寫頁面， `<html>` 元素應讀取：
   `<html lang = "en">`

* 以西班牙文呈現的頁面應採用以下標準：
   `<html lang = "es">`

在AEM中，在建立頁面時設定頁面的預設語言，但在編輯時也可能更改 [頁面屬性](/help/sites-authoring/editing-page-properties.md)。

>[!NOTE]
>
>為根AEM語言的變體提供進一步的微調；例如，美國英語 — en-us、英國英語 — en-gb和加拿大英語 — en-ca。 這種詳細程度通常對輔助技術來說是多餘的，但可用於頁面內容的區域差異。

#### 詳細資訊 — 頁面語言(3.1.1) {#more-information-language-of-page}

* [瞭解成功標準3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [如何滿足成功標3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* 這些代碼基於ISO 639-1。 可在 [W3學校網站](https://www.w3schools.com/tags/ref_language_codes.asp)。

### 部件語言(3.1.2)  {#language-of-parts}

* 成功標準3.1.2
* AA級
* 部件語言：內容中每個段落或短語的人文語言可以以寫程式方式確定，但適當的名稱、技術術語、不確定語言的單詞以及已成為立即環繞文本的本地語言的一部分的單詞或短語除外。

#### 目的 — 部件語言(3.1.2) {#purpose-language-of-parts}

此成功標準的目的與成功標準相似 [頁面語言](#language-of-page)，但適用於單個頁面上包含多種語言內容的網頁（例如，由於引用或不常見的借詞）。

應用此成功標準的頁面允許：

* 盲文轉換軟體，用於插入帶重音字元。
* 螢幕閱讀器可讀出那些具有特殊字元或不使用在頁面級別標識的預設語言的單詞。
* 翻譯工具(如Google翻譯)可將內容從一種語言正確翻譯到另一種語言。

#### How to Meet — 部件語言(3.1.2) {#how-to-meet-language-of-parts}

的 `lang` 屬性可用於標識內容語言中的更改。 例如，德語（ISO 639-1代碼&quot;de&quot;）中的引號如下所示：

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>開箱實例中不支援塊引號。 可以開發自定義元件以支援該功能。

同樣，如果 `span` 元素的使用方式如下：

```xml
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>在包含不同語言的名稱或城市，或使用預設語言中已司空見慣的借詞或短語(如 *幸災樂禍* 英文)。

若要使用適當的語言添加HTML元素，可以在RTE的源編輯模式下手動編輯區域標籤，以便其讀取如上。 或者， `lang` 屬性可由系統管理員包括在RTE中(請參閱 [添加對附加HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

#### 詳細資訊 — 部件語言(3.1.2) {#more-information-language-of-parts}

* [瞭解成功標準3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [如何滿足成功標3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### 可預測(3.2) {#predictable}

[准則3.2可預測：使網頁以可預知的方式顯示和運行。](https://www.w3.org/TR/WCAG/#predictable)

這涉及確保網頁在外觀和操作上保持一致。

### 聚焦(3.2.1)  {#on-focus}

* 成功標準3.2.1
* A級
* 聚焦：當任何用戶介面元件接收到焦點時，它不會啟動上下文的更改。

#### 目的 — 聚焦(3.2.1) {#purpose-on-focus}

此成功標準的目的是確保訪問者在文檔中導航時功能可預測。 任何能夠在接收焦點時觸發事件的元件不得更改上下文。 元件接收焦點時更改上下文的示例包括但不限於：

* 元件收到焦點時自動提交的表單；
* 元件收到焦點時啟動的新窗口；
* 當該元件接收到焦點時，焦點會改變到另一元件；

焦點可以通過鍵盤（例如，打印到控制項）或滑鼠（例如，按一下文本欄位）移動到控制項。 將滑鼠移到控制項上不會移動焦點，除非指令碼實現此行為。 請注意，對於某些類型的控制項，按一下某個控制項也可以激活該控制項（如按鈕），這反過來又可以啟動上下文中的更改。

#### 如何見面 — 聚焦(3.2.1) {#how-to-meet-on-focus}

遵循以下指南 [如何滿足成功標3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)。

#### 更多資訊 — 焦點(3.2.1) {#more-information-on-focus}

* [瞭解成功標準3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [如何滿足成功標3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### 輸入(3.2.2)  {#on-input}

* 成功標準3.2.2
* A級
* 輸入：更改任何用戶介面元件的設定不會自動導致上下文的更改，除非在使用該元件之前已告知用戶該行為。

#### 用途 — 輸入(3.2.2) {#purpose-on-input}

此成功標準的目的是確保輸入資料或選擇表單控制項具有可預測的效果。 更改任何用戶介面元件的設定正在更改控制項中的某些方面，當用戶不再與其交互時，這些方面將一直存在。 因此，選中複選框、將文本輸入文本欄位或更改清單控制項中的選定選項會更改其設定，但激活連結或按鈕則不會更改。 上下文中的更改可能會迷惑那些不容易察覺更改或容易被更改分心的用戶。 只有當明確將響應用戶的操作而發生此類更改時，上下文的更改才適用。

#### 如何碰頭 — 輸入時(3.2.2) {#how-to-meet-on-input}

遵循以下指南 [如何滿足成功標3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)。

#### 詳細資訊 — 輸入(3.2.2) {#more-information-on-input}

* [瞭解成功標準3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [如何滿足成功標3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### 一致導航(3.2.3)  {#consistent-navigation}

* 成功標準3.2.3
* AA級
* 一致導航：在一組網頁內的多個網頁上重複的導航機制在每次重複時都以相同的相對順序發生，除非由用戶發起更改。

#### 用途 — 一致導航(3.2.3) {#purpose-consistent-navigation}

此成功標準的目的是鼓勵用戶使用一致的演示和佈局，這些用戶與一組網頁中重複的內容進行交互，需要多次查找特定資訊或功能。 使用螢幕放大率一次顯示螢幕一小部分的具有低視覺的個體通常使用視覺提示和頁面邊界快速定位重複內容。 以相同順序呈現重複內容對於視覺用戶也很重要，這些視覺用戶在設計中使用空間儲存或視覺提示來定位重複內容。

必須指出，本節中使用短語&quot;相同順序&quot;並不意味著不能使用子導航菜單或不能使用輔助導航或頁面結構塊。 相反，此成功標準旨在幫助跨網頁與重複內容交互的用戶能夠預測他們正在查找的內容的位置，並在再次遇到內容時更快地找到它。

用戶可以通過使用自適應用戶代理或通過設定首選項來啟動按順序的更改，以便以對他們最有用的方式顯示資訊。

#### 如何見面 — 一致導航(3.2.3) {#how-to-meet-consistent-navigation}

遵循以下指南 [如何滿足成功標3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)。

#### 詳細資訊 — 一致導航(3.2.3) {#more-information-consistent-navigation}

* [瞭解成功標準3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [如何滿足成功標3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### 一致標識(3.2.4)  {#consistent-identification}

* 成功標準3.2.4
* A級
* 一致標識：一致地標識一組網頁中具有相同功能的元件。

#### 目的 — 一致標識(3.2.4) {#purpose-consistent-identification}

此成功標準的目的是確保對一組網頁中重複出現的功能元件進行一致識別。 使用螢幕閱讀器的用戶在操作網站時使用的策略是嚴重依賴於他們對可能出現在不同網頁上的功能的熟悉。 如果相同的功能在不同的網頁上具有不同的標籤（或更一般地說，不同的可訪問名稱），則網站的使用難度將大大增加。 它可能還會讓認知局限的人感到困惑，並增加他們的認知負荷。 因此，一致的標籤將有所幫助。

這種一致性延伸到了文本替代。 如果表徵圖或其他非文本項目具有相同的功能，則它們的文本選項也應一致。

如果網頁上有兩個元件，它們的功能與一組網頁中另一個頁面上的元件相同，則所有這三個元件必須一致。 因此，同一頁上的兩者將保持一致。

儘管理想和最佳做法是始終在單個網頁內保持一致，但3.2.4只處理一組網頁內的一致性，其中在該組網頁的多個頁面上重複某些內容。

#### 如何滿足 — 一致標識(3.2.4) {#how-to-meet-consistent-identification}

遵循以下指南 [如何滿足成功標3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)。

#### 更多資訊 — 一致標識(3.2.4) {#more-information-consistent-identification}

* [瞭解成功標準3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [如何滿足成功標3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### 投入幫助(3.3) {#input-assistance}

[准則3.3投入援助：幫助用戶避免和糾正錯誤。](https://www.w3.org/TR/WCAG/#input-assistance)

### 錯誤標識(3.3.1)  {#error-identification}

* 成功標準3.3.1
* A級
* 錯誤標識：如果自動檢測到輸入錯誤，則識別出錯誤的項，並以文本形式向用戶描述該錯誤。

#### 目的 — 錯誤標識(3.3.1) {#purpose-error-identification}

此成功標準的目的是確保用戶知道發生了錯誤，並能夠確定錯誤。 錯誤消息應盡可能具體。 在提交表單失敗的情況下，重新顯示表單並指示出錯的欄位對於一些用戶來說不足以感知到出現錯誤。 例如，螢幕閱讀器用戶在遇到一個指示器之前不會知道有錯誤。 他們可能會在遇到錯誤指示器之前完全放棄表格，認為頁面根本不起作用。 根據WCAG中的定義， [輸入錯誤](https://www.w3.org/TR/WCAG/#dfn-input-error) 是用戶提供的未接受的資訊。 這包括：

網頁需要但用戶省略的資訊，或用戶提供但不屬於所需資料格式或允許值的資訊。
例如：

* 用戶未能在州、省、地區等中輸入相應的縮寫。 欄位;
* 用戶輸入的州/省/自治區縮寫無效；
* 用戶輸入不存在的郵遞區號；
* 用戶將來輸入出生日期2年；
* 用戶在只接受號碼的電話號碼欄位中輸入字母字元或括弧；
* 用戶輸入低於上一個投標或最小投標增量的投標。

#### How to Meet — 錯誤標識(3.3.1) {#how-to-meet-error-identification}

遵循以下指南 [如何滿足成功標3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)。

#### 詳細資訊 — 錯誤標識(3.3.1) {#more-information-error-identification}

* [瞭解成功標準3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [如何滿足成功標3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### 標籤或說明(3.3.2) {#labels-or-instructions}

* 成功標準3.3.2
* A級
* 標籤或說明：當內容需要用戶輸入時提供標籤或說明。

#### 用途 — 標籤或說明(3.3.2) {#purpose-labels-or-instructions}

提供幫助人們完成表單的說明是介面可用性方面良好實踐的基本部分。 這樣做對於視覺或認知障礙患者特別有幫助，否則他們可能很難理解表單的佈局以及在特定表單域中提供的資料類型。

##### Forms

在AEMWKND演示項目中，添加表單元件時會添加預設標籤，如 **文本欄位**&#x200B;的雙曲餘切值。 此預設標題取決於元件類型。您可以在 **標題和文本** 對話框。 必須確保標籤有助於用戶瞭解與每個表單元件關聯的資料。

此 **標題** 欄位元素必須用於欄位元素，因為它提供了可用於輔助技術的標籤。 僅在欄位旁邊的文本中寫入標籤是不夠的。

對於某些表單元件，您也可以使用「隱藏標題」核取方塊以視覺化方式 **隱藏標籤** 。以此方式隱藏的標籤仍適用於輔助技術，但無法顯示在螢幕上。雖然這在某些情況下是個好方法，但通常最好盡可能加入視覺標籤，因為有些使用者可能會看到畫面的一小部分 (一次看一個欄位)，並需要標籤來正確識別欄位。

###### 影像按鈕 {#image-buttons}

使用影像按鈕的位置(例如， **影像按鈕** WKND項目的元件) **標題** 的 **標題和文本** 頁籤實際上提供了影像的alt文本，而不是標籤。 因此，在以下範例中，包含文字的影像 `Submit` 的alt文字為 `Submit`，使用編輯對話方塊中的 **Title** 欄位新增。

###### 表單域組 {#groups-of-form-fields}

在WKND項目中，有一組相關控制項，如 **無線電組**，組以及個別控制項可能需要標題。 在AEM中新增一組選項按鈕時，「標題 **」欄位會提供此群組標題，而個別標題會指定為選項按鈕(** Items ****)。

不過，群組標題和選項按鈕本身之間沒有程式化關聯。範本編輯人員必須將標題包住必要 `fieldset` 和 `legend` 標籤，才能建立此關聯，而這只能透過編輯頁面原始碼來完成。或者，系統管理員可以添加對這些元素的支援，以便這些元素出現在 **欄位屬性** 對話框（請參見） [添加對附加HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

###### Forms的其他注意事項 {#additional-considerations-for-forms}

如果要以特定格式輸入資料，請在標籤文本中明確這一點。 例如，如果必須在 `DD-MM-YYYY` 格式，具體將其指定為標籤的一部分。 這意味著當螢幕閱讀器用戶遇到該欄位時，標籤將自動被宣佈，並附加有關格式的附加資訊。

如果表單欄位的輸入是必填的，請使用標籤中的必要字詞來清楚說明。AEM在需要欄位時新增星號，但最好將字詞加入標 `required`簽本身(在編輯對話方塊的「 **Title** 」欄位中)。

標籤的定位也很重要，因為它有助於標籤找到相應的欄位。 當用戶面對複雜的表單時，這尤其重要。 按照以下公約執行：

* 複選框或單選按鈕：標籤將立即定位在欄位的右側。
* 所有其它表單元件（如文本框、組合框）:標籤位於欄位的正上方或正左側。

以功能非常有限的簡單形式，適當標籤 `Submit` 按鈕可用作相鄰欄位的標籤(例如 `Search`)。 在為標籤文本查找空間可能很困難時，此選項非常有用。

#### 詳細資訊 — 標籤或說明(3.3.2) {#more-information-labels-or-instructions}

* [瞭解成功標準3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [如何滿足成功標3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### 錯誤建議(3.3.3)  {#error-suggestion}

* 成功標準3.3.3
* AA級
* 鍵盤：如果自動檢測到輸入錯誤並且已知用於更正的建議，則向用戶提供建議，除非它會危及內容的安全或目的。

#### 目的 — 錯誤建議(3.3.3) {#purpose-error-suggestion}

此成功標準的目的是確保用戶在可能的情況下收到糾正輸入錯誤的適當建議。 WCAG定義 [輸入錯誤](https://www.w3.org/TR/WCAG/#dfn-input-error) 說是&quot;用戶提供的資訊不被系統接受&quot;。 不被接受的資訊的一些示例包括用戶需要但省略的資訊和用戶提供但不屬於所需資料格式或允許值的資訊。

成功標準3.3.1提供錯誤通知。 但是，具有認知限制的人可能很難理解如何糾正錯誤。 視覺殘疾者可能無法確切地找出如何糾正錯誤。 在提交表單失敗的情況下，用戶可能會放棄表單，因為他們可能不知道如何更正錯誤，即使他們知道錯誤已經發生。

內容作者可以提供錯誤的描述，或者用戶代理可以基於特定於技術的、以寫程式方式確定的資訊提供錯誤的描述。

#### 如何滿足 — 錯誤建議(3.3.3) {#how-to-meet-error-suggestion}

遵循以下指南 [如何滿足成功標3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)。

#### 詳細資訊 — 錯誤建議(3.3.3) {#more-information-error-suggestion}

* [瞭解成功標準3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [如何滿足成功標3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### 錯誤預防（法律、財務、資料）(3.3.4)  {#error-prevention-legal-financial-data}

* 成功標準3.3.4
* AA級
* 錯誤預防（法律、財務、資料）:對於導致用戶發生法律承諾或財務交易、修改或刪除資料儲存系統中的用戶可控資料或提交用戶test響應的網頁，至少以下情況之一為：

   * 可逆提交是可逆的。
   * 檢查用戶輸入的資料是否有輸入錯誤，並為用戶提供糾正錯誤的機會。
   * 已確認在提交完成之前，可以使用一種機制來查看、確認和更正資訊。

#### 目的 — 錯誤預防（法律、財務、資料）(3.3.4) {#purpose-error-prevention-legal-financial-data}

本成功標準旨在幫助殘疾用戶在執行無法逆轉的操作時避免由於錯誤而造成的嚴重後果。 例如，購買不可退還的機票或在經紀賬戶中提交購買股票的訂單是具有嚴重後果的金融交易。 如果用戶在航空旅行日期犯了錯誤，他或她最終可能拿到一張無法兌換的錯日機票。 如果用戶在購買的股票數量上犯了錯誤，他或她最終可能會購買比預期更多的股票。 這兩種錯誤都涉及立即發生且以後無法更改的交易，並且代價非常高昂。 同樣，如果用戶無意中修改或刪除儲存在資料庫中的資料（如旅行服務網站中的整個旅行檔案），則可能是不可恢復的錯誤。 當涉及修改或刪除「用戶可控」資料時，其目的是防止諸如刪除檔案或記錄之類的大量資料丟失。 不是要求確認每個保存命令或簡單建立或編輯文檔、記錄或其他資料。

有殘疾的用戶可能更容易犯錯。 閱讀障礙者可以轉換數字、字母，而汽車障礙者可以錯擊鍵。 通過提供反向操作的功能，用戶可以更正可能導致嚴重後果的錯誤。 提供查看和更正資訊的能力使用戶有機會在採取具有嚴重後果的行動之前檢測錯誤。

用戶可控資料是用戶可查看的資料，用戶可以通過有意的操作來更改和/或刪除。 控制此類資料的用戶的例子是更新用戶帳戶的電話號碼和地址，或從網站刪除過去發票的記錄。 它不引用用戶無法直接查看或與之交互的網際網路日誌和搜索引擎監控資料。

#### How to Meet - Error Prevention(Legal、Financial、Data)(3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

遵循以下指南 [如何滿足成功標3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)。

#### 詳細資訊 — 錯誤預防（法律、財務、資料）(3.3.4) {#more-information-error-prevention-legal-financial-data}

* [瞭解成功標準3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [如何滿足成功標3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## 原則4:穩健 {#principle-robust}

[原則4:強健 — 內容必須足夠強健，以便由各種用戶代理進行解釋，包括輔助技術。](https://www.w3.org/TR/WCAG/#robust)

### 相容(4.1) {#compatible}

[准則4.1相容：最大限度地提高與當前和未來用戶代理的相容性，包括輔助技術。](https://www.w3.org/TR/WCAG/#compatible)

最大限度地提高與當前和未來用戶代理的相容性，包括輔助技術。

### 分析(4.1.1)  {#parsing}

* 成功標準4.1.1
* A級
* 分析：在使用標籤語言實現的內容中，元素具有完整的開始和結束標籤，元素根據其規範進行嵌套，元素不包含重複的屬性，除非規範允許這些功能，否則任何ID都是唯一的。

#### 目的 — 分析(4.1.1) {#purpose-parsing}

此成功標準的目的是確保用戶代理能夠準確解釋和分析內容。 如果無法將內容解析為資料結構，則不同的用戶代理可能會以不同方式呈現內容，或者完全無法分析內容。 一些用戶代理使用「修復技術」來呈現編碼不良的內容。

由於修復技術在用戶代理中不同，因此作者不能假設內容將被準確解析為資料結構或將由包括輔助技術在內的專門用戶代理正確呈現，除非內容是根據該技術的正式語法中定義的規則建立的。 在標籤語言中，元素和屬性語法中的錯誤以及未能提供正確嵌套的開始/結束標籤會導致錯誤，從而阻止用戶代理可靠地分析內容。 因此，成功標準要求只能使用形式語法的規則來分析內容。

#### How to Meet — 分析(4.1.1) {#how-to-meet-parsing}

遵循以下指南 [如何滿足成功標4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)。

#### 詳細資訊 — 分析(4.1.1) {#more-information-parsing}

* [瞭解成功標準4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [如何滿足成功標4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### 名稱、角色、值(4.1.2)  {#name-role-value}

* 成功標準4.1.2
* A級
* 名稱、角色、值：對於所有用戶介面元件(包括但不限於：表單元素、連結和指令碼生成的元件)，名稱和角色可以通過寫程式方式確定；可以以寫程式方式設定用戶可以設定的狀態、屬性和值；用戶代理可以獲得對這些物品的更改通知，包括輔助技術。

#### 用途 — 名稱、角色、值(4.1.2) {#purpose-ame-role-value}

此成功標準的目的是確保輔助技術(AT)能夠收集有關、激活（或設定）內容中用戶介面控制項狀態的資訊並保持最新。

當使用可訪問技術的標準控制時，此過程非常簡單。 如果用戶介面元素按照說明使用，則滿足此設定的條件。 (請參閱下面的成功標準4.1.2示例)

但是，如果建立了自定義控制項，或者將介面元素（在代碼或指令碼中）寫程式為具有與通常不同的角色和/或功能，則需要採取額外措施以確保控制項向輔助技術提供重要資訊並允許它們由輔助技術控制。

用戶介面控制項的一個特別重要的狀態是它是否具有焦點。 控制的焦點狀態可以寫程式地確定，並且關於焦點改變的通知被發送到用戶代理和輔助技術。 用戶介面控制狀態的其它示例包括是否選中了複選框或單選按鈕，或是否展開或折疊可折疊樹或清單節點。

#### How to Meet - Name、Role、Value(4.1.2) {#how-to-meet-ame-role-value}

遵循以下指南 [如何滿足成功標4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)。

#### 詳細資訊 — 名稱、角色、值(4.1.2) {#more-information-ame-role-value}

* [瞭解成功標準4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [如何滿足成功標4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
