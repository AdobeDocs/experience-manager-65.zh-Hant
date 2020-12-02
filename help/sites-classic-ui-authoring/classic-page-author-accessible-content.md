---
title: 建立可存取的內容 (符合 WCAG 2.0)
seo-title: 建立可存取的內容 (符合 WCAG 2.0)
description: WCAG 2.0 包含一系列無需仰賴技術的指引和成功標準，有助身心障礙人士存取與使用網路內容。
seo-description: WCAG 2.0 包含一系列無需仰賴技術的指引和成功標準，有助身心障礙人士存取與使用網路內容。
page-status-flag: de-activated
uuid: c2c0cac0-2a9f-478d-8261-e8cc894aae34
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 378bc33d-ab6c-4651-9688-102c961561fc
translation-type: tm+mt
source-git-commit: df992fc0204519509c4662a7d4315939af2fc92c
workflow-type: tm+mt
source-wordcount: '9241'
ht-degree: 8%

---


# 建立可存取的內容 (符合 WCAG 2.0){#creating-accessible-content-wcag-conformance}

>[!CAUTION]
>
>由於AEM 6.4已淘汰Classic UI，因此WCAG 2.1未更新此頁面上的內容。
>
>如需AEM和WCAG 2.1的詳細資訊，請參閱下列頁面：
>
>* [AEM與網頁協助工具准則](/help/managing/web-accessibility.md)
>* [WCAG 2.1 快速指南](/help/managing/qg-wcag.md)
>* [建立可存取的內容 (符合 WCAG 2.1)](/help/sites-authoring/creating-accessible-content.md)


WCAG 2.0 包含一系列無需仰賴技術的指引和成功標準，有助身心障礙人士存取與使用網路內容。

>[!NOTE]
>
>另請參閱:
>
>* 我們的[WCAG 2.0](/help/managing/qg-wcag.md)快速指南，以取得詳細資訊
>* [設定Rich Text Editor，以製作可存取的內容](/help/sites-administering/rte-accessible-content.md)

>



這些級別按三個一致性級別進行分級：A級（最低）、AA級和AAA級（最高）。 簡單地說，這些級別的定義如下：

* **** A級：您的網站達到基本的最低協助功能等級。要達到此級別，將滿足所有A級成功標準。
* **** AA級：這是您努力追求的最佳無障礙環境支援等級，其中您的網站可達到更高的無障礙環境支援等級，因此大部分使用者都可使用大部分的技術。要達到此級別，將滿足所有A級和A級成功標準。
* **** AAA級：您的網站可達到非常高的協助功能。要達到此級別，將滿足所有A級、AA級和AAA級成功標準。

建立網站時，您必須決定要讓網站遵循的整體等級。

以下部分介紹[WCAG 2.0准則](https://www.w3.org/TR/WCAG20/#guidelines)以及A級和A級符合性級別[的相關成功標準。](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html)

>[!NOTE]
>
>由於無法滿足特定類型內容的所有級別AAA成功標準，因此不建議將此級別符合標準作為一般策略。

>[!NOTE]
>
>在本檔案中，我們使用：
>
>* [WCAG 2.0 Guidelines](https://www.w3.org/TR/WCAG20/#guidelines)的簡稱。
>* [WCAG 2.0 Guidelines](https://www.w3.org/TR/WCAG20/#guidelines)中用於幫助與WCAG網站交互引用的編號。

>



## 原則1:可感知{#principle-perceivable}

[原則1:可感知——資訊和使用者介面元件必須以使用者可感知的方式呈現給使用者。](https://www.w3.org/TR/WCAG20/#perceivable)

### 替代文字(1.1){#text-alternatives}

[准則1.1備選案文：為任何非文字內容提供替代文字，以便將其變更為人們需要的其他形式，例如大型印刷、盲文、語音、符號或更簡單的語言。](https://www.w3.org/TR/WCAG20/#text-equiv)

### 非文字內容(1.1.1){#non-text-content}

* 成功標準1.1.1
* A級
* 非文字內容：除下列情況外，提供給使用者的所有非文字內容都有提供同等目的的文字替代項目。

#### 用途——非文字內容(1.1.1){#purpose-non-text-content}

網頁上的資訊可以提供許多不同的非文字格式，例如圖片、視訊、動畫、圖表和圖形。 盲人或視力嚴重受損的人無法看到非文本內容，但他們可以通過螢幕閱讀器讀取文本內容或通過盲文顯示設備以觸覺形式顯示文本內容。 因此，提供圖形格式的內容替代文字，讓無法看見圖形內容的使用者可以存取內容所提供的相同版本資訊。

另一個有用的好處是，替代文字可讓非文字內容依搜尋引擎技術建立索引。

#### 如何開會——非文字內容(1.1.1){#how-to-meet-non-text-content}

對於靜態圖形，基本要求是為圖形提供等效的文本替代。 這可在&#x200B;**Alt Text**&#x200B;欄位中完成：

>[!NOTE]
>
>有些現成可用的元件(例如 **Carousel** 和 **Slideshow** )不提供將替代文字說明新增至影像的方式。當為您的AEM例項實作這些版本時，您的開發團隊將需要設定這些元件以支援`alt`屬性，讓作者可以將它新增至內容（請參閱[新增支援其他HTML元素和屬性](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

**Alt Text**&#x200B;欄位可在&#x200B;**Image**&#x200B;元件對話框的&#x200B;**Advanced**&#x200B;映像屬性頁籤中使用：

![在傳統UI中編輯影像元件對話方塊；顯示「替代文字」欄位。](assets/chlimage_1-17a.png)

AEM依預設會將&#x200B;**Alt Text**&#x200B;新增至您的影像。 對於傳統UI，預設屬性的建立方式有兩種不同的情況（雖然預設值可能不足以作為替代值，而且很可能需要在&#x200B;**Advanced**&#x200B;影像屬性頁籤中編輯）:

* 個檔案:

   影像是從使用者的硬碟上傳。 如果將影像元件新增至頁面，然後從硬碟或其他來源選擇影像，則&#x200B;**Alt Text**&#x200B;的預設值為`file`。 必須在&#x200B;**Advanced**&#x200B;影像屬性標籤中變更此項。 同樣地，此值不會顯示在&#x200B;**Alt Text**&#x200B;欄位中，但當值變更時，新值會顯示在欄位中。

* 資產:

   從數位資產儲存庫新增影像。 如果您將影像從數位資產存放庫拖曳至網頁，則該影像的&#x200B;**Title**&#x200B;和&#x200B;**Alt Text**&#x200B;值會從該影像的中繼資料擷取。

>[!NOTE]
>
>在上述兩種情況中，**Alt Text**&#x200B;的預設值都不會顯示在&#x200B;**Advanced Image Properties**&#x200B;標籤中。 要更改預設值，只需在&#x200B;**Alt Text**&#x200B;欄位中輸入新值。

>[!NOTE]
>
>如果您的影像純粹是裝飾性的（請參閱[建立好的替代文字](#creating-good-text-alternatives)），您可以使用空格鍵在&#x200B;**Alt Text**&#x200B;欄位中輸入空格。 這會建立空的`alt`屬性，提示螢幕閱讀程式忽略影像。

#### 建立好的替代文字{#creating-good-text-alternatives}

非文字內容有多種形式，因此文字替代項目的價值取決於圖形在網頁中所扮演的角色。 以下是一些一般經驗法則：

* 文字替代項目應簡明扼要，但應清楚地擷取非文字內容所提供之基本資訊。
* 應避免過長的說明（超過100個字元）。 如果替代文字需要更詳細的資訊：

   * 在替代文字中提供簡短說明
   * 並在相同頁面的其他位置或個別網頁的文字中有較長的說明。 將影像設為連結，或將文字連結置於影像旁，以連結至此個別的說明。

* 替代文字不應複製相同頁面附近文字表單中提供的內容。 請記住，許多影像是頁面文字中已涵蓋的點的插圖，因此可能已有詳細的文字替代項目。
* 如果非文字內容是指向其他頁面或檔案的連結，而沒有其他文字構成相同連結的一部分，則影像的替代文字必須指出連結的目的地，而非描述影像。
* 如果非文字內容包含在按鈕元素中，且沒有文字組成相同按鈕的一部分，則影像的替代文字必須指出按鈕的功能，而非描述影像。
* 如果影像是空白(null)的替代文字，但是只有在影像沒有替代文字（例如純裝飾性圖形）或頁面文字中已存在等同文字時，才能完全接受。

[W3C草稿：HTML5提供有用文字替代品的技術](https://dev.w3.org/html5/alt-techniques/)提供了更多細節，並提供了針對不同類型影像的適當替代文字提供範例。

需要替代文字的特定非文字內容類型可能包括：

* 說明性像片：

   這些是人物、物件或地點的影像。 想想像片在頁面中的角色；適當的文字等同項目可能是[object ]*的*&#x200B;像片，但可能取決於周圍的文字。

* 圖示：

   這些是傳達特定資訊的小型圖片（圖形）。 必須在頁面和網站上一致使用這些變數。 頁面或網站上的圖示所有例項都應有相同的簡短文字替代項目，除非這麼做會造成相鄰文字的不必要複製。

* 圖表和圖形：

   這些通常代表數值資料。 因此，提供文字替代選擇的一個選項可能是包含圖表或圖形中主要趨勢的簡短摘要。 如有必要，也可使用&#x200B;**Advanced**&#x200B;影像屬性標籤中的&#x200B;**Description**&#x200B;欄位，在文字中提供更詳細的說明。 此外，您也可以在頁面或網站的其他地方以表格形式提供來源資料。

   ![圖形範例。以下是提供替代方案的最佳方法。](assets/chlimage_1-2a.jpeg)

   若要提供此範例圖表的替代選項，請在影像本身加入簡明的`alt`文字，然後使用全文替代項目跟隨影像。

   ```xml
   <p><img src="figure1.gif" alt="Figure 1" ></p>
   <p> Figure 1. Distribution of Articles by Journal Category.
   Pie chart: Language=68%, Education=14% and Science=18%.</p>
   ```

   >[!NOTE]
   >
   >上述程式碼片段僅用於說明順序。 建議使用&#x200B;**Image**&#x200B;元件（而非上述的`img src`參考）。

   在AEM中，您可使用影像設定對話方塊中的&#x200B;**Alt Text**&#x200B;和&#x200B;**Description**&#x200B;欄位組合來完成此作業——如[How to Meet - Non-text Content(1.1.1)](#how-to-meet-non-text-content)。

* 地圖、圖表、流程圖：

   用於提供空間資料的圖形(例如。 若要支援描述物件或程式之間的關係)，請確定關鍵訊息是以文字格式提供。對於地圖，提供等同全文的地圖可能不切實際，但如果提供地圖以幫助人們找到特定位置的方式，則地圖影像的替代文字可以簡短地標示 *X*，然後在頁面其他地方的文字或透過 **Image元件的「** Advanced **」 (進階) 索引標籤中的「** Description **** 」 (說明) 欄位，提供指向該位置的指示。

* 驗證碼：

   CAPTCHA是&#x200B;*完全自動化的公共圖靈測試，可告訴電腦和人類Apart*。 它是用於網頁上的安全檢查，用於區分人類和惡意軟體，但會造成無障礙環境支援。 這些影像需要使用者描述他們所看到的內容，才能通過安全性測試。 為影像提供替代文字顯然不可能，因此您需要考慮其他非圖形解決方案。

   W3C提供了一些建議，如：

   * 邏輯謎題
   * 使用音效輸出而非影像
   * 使用帳戶和垃圾訊息篩選的限制。

* 背景影像：

   這些功能是使用階層式樣式表(CSS)而非HTML來達成。 這表示無法指定替代文字值。 因此，背景影像不應提供重要的文字資訊——如果有的話，這項資訊也必須提供在頁面的文字中。

   但是，當無法顯示影像時，必須顯示替代背景。

   >[!NOTE]
   >
   >背景文字和前景文字之間應有適當的對比度；這在[Contrapts(Minimum)(1.4.3)](#contrast-minimum)中會有更詳細的討論。

#### 詳細資訊——非文字內容(1.1.1){#more-information-non-text-content}

* [瞭解成功標準1.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)
* [如何符合成功標準1.1.1](https://www.w3.org/WAI/WCAG20/quickref/#text-equiv)
* [W3C:HTML5提供實用文字替代（草稿）的技巧](https://dev.w3.org/html5/alt-techniques/)
* [W3C說明及驗證碼的替代方案](https://www.w3.org/TR/turingtest/)

### 基於時間的介質(1.2){#time-based-media}

[准則1.2基於時間的媒體：為時間型媒體提供替代選擇。](https://www.w3.org/TR/WCAG20/#text-equiv)

這涉及&#x200B;*時間型*&#x200B;的網頁內容。 這包括使用者可播放的內容（例如視訊、音訊和動畫內容），並可預先錄制或即時串流。

### 僅限音訊和僅限視訊（預先錄制）(1.2.1){#audio-only-and-video-only-pre-recorded}

* 成功標準1.2.1
* A級
* 僅限音訊和僅限視訊（預錄）:對於預錄的純音訊和純視訊媒體，除非音訊或視訊是文字的替代媒體，並明確標示為：

   * 僅預錄音效：提供了用於基於時間的媒體的替代方案，該替代方案為預錄的僅音頻內容呈現等同資訊。
   * 僅預錄視訊：提供了用於基於時間的媒體的替代選擇或音頻軌道，該音頻軌道顯示用於預錄的僅視頻內容的等效資訊。

#### 用途——僅限音訊和僅限視訊（預錄）(1.2.1){#purpose-audio-only-and-video-only-pre-recorded}

視訊和音訊的協助功能問題可能會透過下列方式發生：

* 沒有配樂或配樂時，視覺受損者無法告知視訊或動畫中的情況；
* 聽障者，聾者，聽不到配樂；
* 聽得見配樂但不懂的人（例如，因為配樂是他們不懂的語言）。

使用不支援以特定媒體格式（例如Adobe Flash）播放內容的瀏覽器或裝置的使用者，也可能無法使用視訊或音訊。

以不同格式提供此資訊，例如文字（或無音訊的視訊音訊），可讓無法存取原始內容的使用者存取。

#### 如何開會——僅限音訊和僅限視訊（預錄）(1.2.1){#how-to-meet-audio-only-and-video-only-pre-recorded}

* 如果內容是預先錄制的音訊，但沒有視訊（例如播客）:

   * 在內容之前或之後，提供連結至音訊內容的文字記錄。

      成績單應是HTML頁面，其文字等同於所有口語和重要的非口語內容，另外還包括說話者的指示、設定的描述、聲音表達以及任何其他重要音效的描述。

* 如果內容是動畫或預先錄制的視訊，且沒有音效：

   * 在內容之前或之後，提供視訊所提供資訊的等同文字說明連結
   * 或是常用音訊格式（例如MP3）的等效音訊描述。

>[!NOTE]
>
>如果提供音訊或視訊內容作為網頁上已存在其他格式內容的替代內容，則無需遵循上述要求。 例如，如果視訊說明文字指示清單，則此視訊不需要替代項目，因為文字指示已可當成視訊的替代項目。

將多媒體（尤其是Flash內容）插入AEM網頁，就像插入影像一樣。 然而，由於多媒體內容遠非靜態影像，因此有多種不同的設定和選項來控制多媒體的播放方式。

>[!NOTE]
>
>當您將多媒體與資訊性內容搭配使用時，您也必須建立替代內容的連結。 例如，若要包含文字成績單，請建立HTML頁面以顯示成績單，然後在音訊內容旁或下方新增連結。

#### 詳細資訊——僅限音訊和僅限視訊（預錄）(1.2.1){#more-information-audio-only-and-video-only-pre-recorded}

* [瞭解成功標準1.2.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html)
* [如何符合成功標準1.2.1](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)

### 標題（預先錄制）(1.2.2){#captions-pre-recorded}

* 成功標準1.2.2
* A級
* 標題（預錄）:除了媒體是文字的替代媒體，而且已清楚標示為同步媒體外，所有預先錄制的音訊內容都會提供標題。

#### 用途——標題（預先錄制）(1.2.2){#purpose-captions-pre-recorded}

聽障或聽障者將無法或難以存取音訊內容。 標題是語音和非語音音訊的文字等效，在視訊中的適當時間在螢幕上顯示。 它們讓聽不到音效的人，瞭解現在的情況。

>[!NOTE]
>
>在視訊或動畫的相同頁面上提供適當的文字或非文字等同內容（提供直接等同的資訊）時，不需要標題。

#### 如何符合——標題（預先錄制）(1.2.2){#how-to-meet-captions-pre-recorded}

標題可以是：

* 開啟：播放視訊時一律顯示)
* 已關閉：字幕可由使用者開啟或關閉

盡可能使用隱藏字幕，因為這可讓使用者選擇是否檢視字幕。

對於隱藏字幕，您需要在視訊檔案旁建立並提供適當格式（例如[SMIL](https://www.w3.org/AudioVideo/)）的同步化字幕檔案(如如何做到的詳細資訊不在本指南的範圍內，但我們提供了[更多資訊——標題（預先錄制）(1.2.2)](#more-information-captions-pre-recorded)下的教學課程連結)。 請確定您提供附註，讓使用者知道視訊有可用的標題。

如果您必須使用開放標題，請將文字內嵌至視訊軌。 這可以使用影片編輯應用程式來實現，讓標題可以覆蓋在影片上。

#### 詳細資訊——標題（預先錄制）(1.2.2){#more-information-captions-pre-recorded}

* [瞭解成功標準1.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html):
* [如何符合成功標準1.2.2](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)
* [W3C:同步化多媒體](https://www.w3.org/AudioVideo/)
* [字幕、成績單和音訊說明——由WebAIM提供](https://webaim.org/techniques/captions/)

### 音訊描述或媒體替代（預錄）(1.2.3){#audio-description-or-media-alternative-pre-recorded}

* 成功標準1.2.3
* A級
* 音訊描述或媒體替代（預錄）:為同步媒體提供基於時間的媒體或預錄視頻內容的音頻描述的替代物，除非媒體是文本的媒體替代物，並且被明確標示為這樣。

#### 用途——音訊描述或媒體替代（預錄）(1.2.3){#purpose-audio-description-or-media-alternative-pre-recorded}

如果視障或視障人士僅以視覺化方式提供視訊或動畫中的資訊，或者配樂無法提供足夠的資訊，以視覺化方式瞭解發生的情況，將會遇到無障礙環境支援。

#### How to Meet - Audio Description or Media Alternation(Pre-Recorded)(1.2.3){#how-to-meet-audio-description-or-media-alternative-pre-recorded}

為滿足此成功標準，可採用兩種方法。 兩者皆可接受：

1. 加入視訊內容的其他音訊描述。 這可以通過以下三種方式之一實現：

   * 在現有對話方塊的暫停期間，提供場景中未呈現為現有音軌一部分的變更資訊；
   * 提供新的、額外的可選音軌，其中包含原始音軌，但也包含場景變更的額外音訊資訊。

      * 這可讓使用者在現有的音軌（*不包含音訊描述）和新的音軌（*&#x200B;包含音訊描述）之間切換。**
      * 如此可避免中斷不需要其他說明的使用者。
   * 建立視訊內容的第二版本，以允許擴充音訊說明。 這可借由在適當的點暫停音訊和視訊，減少在現有對話方塊之間的間隙中提供詳細音訊描述的相關困難。 因此，在動作再次開始之前，可以提供更長的音訊描述。 如上例所示，這最好是選用的額外音軌，以防止不需要額外說明的使用者中斷。


1. 提供與視訊或動畫的音訊和視覺元素相當的適當文字記錄。 這應當包括，在適當情況下，說話者的指示、設定的描述、聲音表達。 視其長度而定，您可以將成績單放在視訊或動畫的相同頁面，或放在個別頁面上；如果您選擇後一個選項，請提供視訊或動畫旁的轉錄本連結。

如何建立音訊描述視訊的確切詳細資訊，不在本指南中。 建立視訊和音訊描述可能很耗時，但其他Adobe產品可協助您完成這些工作。 如果您在Adobe Flash Professional中建立內容，您也應建立指令碼以提示使用者下載適當的外掛程式，並透過`<noscript>`元素提供文字替代項目。

#### 詳細資訊——音訊描述或媒體替代（預錄）(1.2.3){#more-information-audio-description-or-media-alternative-pre-recorded}

* [瞭解成功標準1.2.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html):
* [如何符合成功標準1.2.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc)
* [Adobe Encore CS5](https://www.adobe.com/products/premiere/encore/)

### 標題(Live)(1.2.4){#captions-live}

* 成功標準1.2.4
* AA級
* 標題（即時）:同步化媒體中所有即時音訊內容都提供標題。

#### 用途——標題(Live)(1.2.4){#purpose-captions-live}

此成功標準與[標題（預先錄制）](#captions-pre-recorded)相同，因為它可解決聾人或聽障人士所經歷的無障礙環境障礙，但此成功標準涉及即時簡報，例如網路廣播。

#### How to Meet - Captions(Live)(1.2.4){#how-to-meet-captions-live}

請遵循上述[標題（預先錄制）](#captions-pre-recorded)的指引。 但是，由於媒體的即時性質，必須盡快建立字幕布建，以因應目前的情況。 因此，您應考慮使用即時字幕或語音轉文字工具。

詳細說明超出本檔案的範圍，但下列資源可提供有用資訊：

* [WebAIM:即時字幕](https://www.webaim.org/techniques/captions/realtime.php)
* [AccessIT（華盛頓大學）:是否可以使用語音識別自動產生字幕？](https://www.washington.edu/accessit/articles?1209)

#### 詳細資訊——標題(Live)(1.2.4){#more-information-captions-live}

* [瞭解成功標準1.2.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html)
* [如何符合成功標準1.2.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-real-time-captions)

### 音訊說明（預先錄制）(1.2.5){#audio-description-pre-recorded}

* 成功標準1.2.5
* AA級
* 音訊說明（預錄）:提供同步媒體中所有預先錄制的視訊內容的音訊描述。

#### 用途——音訊說明（預先錄制）(1.2.5){#purpose-audio-description-pre-recorded}

此成功標準與[音訊描述或媒體替代項目（預先錄制）](#audio-description-or-media-alternative-pre-recorded)相同，但作者必須提供更詳細的音訊描述，以符合等級AA。

#### How to Meet - Audio Description(Pre-Recorded)(1.2.5){#how-to-meet-audio-description-pre-recorded}

遵循[音訊說明或媒體替代項目（預先錄制）](#audio-description-or-media-alternative-pre-recorded)的指引。

#### 詳細資訊——音訊說明（預先錄制）(1.2.5){#more-information-audio-description-pre-recorded}

* [瞭解成功標準1.2.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html)
* [如何符合成功標準1.2.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc-only)

### 適應性(1.3){#adaptable}

[准則1.3適應性：建立可以以不同方式呈現的內容（例如更簡單的版面），而不會遺失資訊或結構。](https://www.w3.org/TR/WCAG20/#content-structure-separation)

本准則涵蓋支援以下人員的必要要求：

* 可能無法存取作者在*標準*二維、多欄、彩色網頁版面中所呈現的資訊

* 可能會使用純音效或替代的視覺顯示，例如大型文字或高對比度。

### 資訊與關係(1.3.1){#info-and-relationships}

* 成功標準1.3.1
* A級
* 資訊與關係：通過表現傳遞的資訊、結構和關係可以通過寫程式方式確定，或在文本中可用。

#### 用途——資訊與關係(1.3.1){#purpose-info-and-relationships}

許多殘障人士使用的輔助技術都依賴結構資訊，以有效顯示或輸出內容。 此結構資訊可以採用頁標題、表行和列標題以及清單類型的形式。 例如，螢幕閱讀程式可讓使用者從標題到標題瀏覽頁面。 但是，當頁面內容只看起來是透過視覺樣式而非基礎HTML來呈現結構時，輔助技術就無法使用結構資訊，限制了其支援更輕鬆瀏覽的能力。

此成功標準的存在，是為了確保此類結構性資訊是透過HTML提供，讓瀏覽器和輔助技術能夠存取並運用這些資訊。

#### 如何認識——資訊與關係(1.3.1){#how-to-meet-info-and-relationships}

AEM可讓您輕鬆使用適當的HTML元素來建構網頁。 在RTE（文本元件）中開啟頁面內容，然後使用&#x200B;**Format**&#x200B;菜單指定適當的結構元素（例如段落、標題等）。

下圖顯示已設定為段落文字的文字；使用的原始碼視圖顯示其具有正確的開啟和關閉&lt;p>和&lt;/p>標籤。

![在來源編輯模式（傳統UI）中顯示的段落元素範例。](assets/chlimage_1-18a.png)

您可以透過下列方式，確保您的網頁具有適當的結構：

* **使用標題：**

   只要您已啟用RTE的協助功能（請參閱[AEM和Accessibility](/help/sites-administering/rte-accessible-content.md)）,AEM就會提供3層頁面標題。 您可以使用這些項目來識別內容的區段和子區段。標題1是標題的最高級別，標題3是最低級別。系統管理員可以配置系統以允許使用更多標題級別。

   下圖顯示不同標題類型的範例。

   ![下拉式選取器（傳統UI）中顯示的標題H1到H3。](assets/chlimage_1-19a.png)

* **強調的文字**:

   使用&lt;strong>或&lt;em>元素指出強調。 請勿使用標題來反白標示段落中的文字。

   * 反白標示您要強調的文字；
   * 按一下&#x200B;**B**&#x200B;圖示（對於&lt;strong>）或&#x200B;**I**&#x200B;圖示（對於&lt;em>）（對於&lt;em>）（對於&#x200B;**Properties**&#x200B;面板顯示）（請確定已選取HTML）。

   >[!NOTE]
   >
   >標準AEM安裝中的RTE已設定為使用：
   >
   >* &lt;b> for&lt;/b> 
   * &lt;i> for&lt;/i> 

   它們實際上是相同的，但&lt;strong>和&lt;em>較好，因為它們是語義正確的html。 您的開發團隊可以設定RTE，以便在開發專案例項時使用&lt;strong>和&lt;em>（而非&lt;b>和&lt;i>）。

* **使用清單**:您可以使用HTML來指定三種不同的清單類型：

   * `<ul>`元素用於&#x200B;*無序*&#x200B;清單（項目符號）。 使用`<li>`元素來識別個別清單項目。

      在RTE中，使用&#x200B;**項目清單**&#x200B;圖示。

   * `<ol>`元素用於&#x200B;*編號*&#x200B;清單。 使用`<li>`元素來識別個別清單項目。

      在RTE中，使用&#x200B;**Numbered List**&#x200B;表徵圖。
   如果要將現有內容變更為特定的清單類型，請反白標示適當的文字並選取適當的清單類型。 如先前顯示如何輸入段落文字的範例所示，適當的清單元素會自動新增至您的HTML，但您可以在來源編輯檢視中檢視此項。

   >[!NOTE]
   `<dl>` 不受RTE支援。

* **使用表格**:

   必須使用HTML表格元素來識別資料表格：

   * 一個`<table>`元素
   * a `<tr>`元素，用於表格的每一列
   * 每個列和列標題的`<th>`元素
   * 每個資料儲存格的`<td>`元素

   >[!NOTE]
   應使用&#x200B;**Table**&#x200B;元件實現表。 雖然表可以在Text元件中建立，但不建議這樣做。

   此外，可存取的表格還使用下列元素和屬性：

   * `<caption>`元素用於為表格提供可見標題。 字幕預設會出現在表格的正中，但可使用CSS適當定位。 標題以寫程式方式與表關聯，因此它是提供內容介紹的有用方法。
   * `<h3 class="summary">`元素提供有視力的使用者可看到的摘要，協助無視力的使用者更輕鬆地瞭解表格中顯示的資訊。 在使用複雜或非常規表格版面時（此屬性不會顯示在瀏覽器中，只會讀出至輔助技術），此功能特別有用。
   * `<th>`元素的`scope`屬性用於指示單元格是代表特定行的標題，還是代表特定列的標題。 類似的方法是在複雜表格中使用標題和id屬性，其中資料儲存格可與一或多個標題相關聯。

   >[!NOTE]
   預設情況下，這些元素和屬性不直接可用，但系統管理員可以在&#x200B;**表屬性**&#x200B;對話框中添加對這些值的支援（請參閱[添加對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

   添加&#x200B;**Table**&#x200B;時，可使用對話框配置&#x200B;**Table properties**。

   * 相應的&#x200B;**標題**。
   * 理想情況下，請移除「寬 **度」、「邊框高度」、「邊框高度」、「邊框高度**」、「單元格間距」、「單元格間距 **」、「單元格**************&#x200B;間距」的預設值。因為這些屬性可以在全局樣式表中設定。

   ![表屬性對話框。](assets/chlimage_1-20a.png)

   然後，您可以使用&#x200B;**儲存格屬性**&#x200B;來選擇儲存格是資料儲存格還是標題儲存格，如果標題儲存格，則選擇它是與列或欄相關，或兩者皆有：

   ![呼叫屬性對話框；將行（通常是第一行）設定為標題行。](assets/chlimage_1-21a.png)

* **複雜的資料表：**

   在某些情況下，如果有具有兩個或多個標題級別的複雜表，則基本表屬性可能不足以提供所有必要的結構資訊。 對於這些類型的複雜表格，需要使用header和 **id屬性在標題及其相關儲存格之間建** 立直 **接** 關係。例如，在下表的標題和ID中，會對輔助技術使用者進行程式化關聯。

   >[!NOTE]
   id屬性不適用於現成可用的安裝。 它可以通過配置HTML規則和RTE中的串列化函式來啟用。

   >[!NOTE]
   應使用&#x200B;**Table**&#x200B;元件實現表。 雖然表可以在Text元件中建立，但不建議這樣做。

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
   標準安裝中不會立即使用此功能。 它需要配置RTE;HTML規則和序列化程式。

#### 詳細資訊——資訊與關係(1.3.1){#more-information-info-and-relationships}

* [瞭解成功標準1.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html)
* [如何符合成功標準1.3.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-programmatic)

### 感官特性(1.3.3){#sensory-characteristics}

* 成功准則1.3.3
* A級
* 感官特徵：提供的理解和操作內容的指示不僅依賴於部件的感官特性，如形狀、大小、視覺位置、方向或聲音。

#### 目的——感官特性(1.3.3){#purpose-sensory-characteristics}

設計人員通常會專注在視覺設計功能上，例如顏色、形狀、文字樣式，或內容在呈現資訊時的絕對或相對位置。 這些設計技巧在傳達資訊時十分強大，但盲人或視障人士可能無法存取需要視覺識別位置、顏色或形狀等屬性的資訊。

同樣地，如果需要區分不同聲音（例如男性或女性口語內容）的資訊沒有反映在音頻內容的任何文本替代內容中，則對聽力有障礙的人會造成無障礙。

>[!NOTE]
有關顏色替代項的要求，請參閱[使用顏色](#use-of-color)。

#### 如何滿足——感官特性(1.3.3){#how-to-meet-sensory-characteristics}

請確定任何依賴頁面內容視覺特性的資訊，也會以替代格式顯示。

* 不要依賴視覺位置提供資訊。 例如，如果您想將使用者引薦至頁面右側的功能表，以取得詳細資訊，請勿參考右側的&#x200B;*功能表；請改為命名功能表（例如透過標題），並在文字中參照該名稱。*
* 切勿依賴文字樣式（例如粗體或斜體文字）來傳達資訊。

>[!NOTE]
如果明白描述性詞語在非視覺化內容中有意義，則可接受使用。 例如，使用&#x200B;*above*&#x200B;和&#x200B;*below*&#x200B;通常是可接受的，因為它們分別表示特定內容項目之前和之後的內容；當內容被大聲朗讀時，這仍然有意義。

#### 更多資訊——感官特性(1.3.3){#more-information-sensory-characteristics}

* [瞭解成功標準1.3.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html)
* [如何符合成功標準1.3.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-understanding)

### 可區分(1.4){#distinguishable}

[准則1.4可區分：讓使用者更輕鬆地檢視和聽取內容，包括將前景與背景分開。](https://www.w3.org/TR/WCAG20/#visual-audio-contrast)

### 色彩的使用(1.4.1){#use-of-color}

* 成功標準1.4.1
* A級
* 色彩的使用：顏色不是傳送資訊、指示動作、提示響應或區分視覺元素的唯一視覺手段。

>[!NOTE]
此成功標準可特別處理色彩感知。 其他形式的感知涵蓋在[適應性(1.3)](#adaptable)中；包括程式化存取色彩和其他視覺化簡報編碼。

#### 用途——色彩的使用(1.4.1){#purpose-use-of-color}

顏色是增強網頁美感的一種明顯有效的方式，在資訊傳遞方面也有很大的幫助。 但是，從失明到彩色視覺缺陷，都存在著一系列的視覺缺陷，這意味著有些人無法區分某些顏色。 這使得色彩編碼成為提供資訊的不可靠方式。

例如，有紅綠色視覺缺陷的人，將無法區分綠色和紅色。 他們可能會將這兩種顏色視為第三種顏色（例如，棕色），在這種情況下，他們將無法區分紅色、綠色和棕色。

此外，使用純文字瀏覽器、單色顯示裝置或檢視頁面黑白列印成品的使用者無法察覺色彩。

#### How to Meet - Use of Color(1.4.1){#how-to-meet-use-of-color}

無論使用何種顏色來傳達資訊，請確定這些資訊是可用的，而不需要查看顏色。

例如，請確定文字中也明確提供由顏色提供的資訊。 下圖顯示顏色和文本如何指示效能的座位可用性：

<table>
 <tbody>
  <tr>
   <td><p><strong>效能</strong></p> </td>
   <td><p><strong>可用性</strong></p> </td>
  </tr>
  <tr>
   <td><p>星期二3月16日<sup>th</sup></p> </td>
   <td><p>可用授權</p> </td>
  </tr>
  <tr>
   <td><p>星期三3月17日</p> </td>
   <td><p>可用授權</p> </td>
  </tr>
  <tr>
   <td><p>星期四3月18日<sup>th</sup></p> </td>
   <td><p>售完</p> </td>
  </tr>
 </tbody>
</table>

如果使用顏色做為提供資訊的提示，您應提供額外的視覺提示，例如變更樣式（例如粗體、斜體）或字型。 這可協助視力低下或色彩視覺缺乏者識別資訊。 但是，它不能完全依賴，因為它不會幫助根本看不到頁面的人。

#### 更多資訊——色彩的使用(1.4.1){#more-information-use-of-color}

* [瞭解成功標準1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [如何符合成功標準1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [符合3:1對比度的指南，包含「網頁安全」色彩清單](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)

### 對比度（最低）(1.4.3){#contrast-minimum}

* 成功標準1.4.3
* AA級
* 對比度（最小值）:文字和影像的視覺呈現至少有4.5:1的對比率，但下列除外：

   * 大型文字：大型文字和大型文字影像的對比度至少為3:1。
   * 附帶：屬於非作用中使用者介面元件的文字或影像，是純粹的裝飾，對任何人不可見，或是包含其他重要視覺內容之圖片的文字或影像，則無對比要求。
   * Logotypes:屬於標誌或品牌名稱的文字沒有最低對比要求。

#### 用途——對比（最低）(1.4.3){#purpose-contrast-minimum}

某些視覺障礙的人可能無法區分某些低對比色彩對。 如果以下情況，這些人可能會遇到無障礙環境支援問題：

* 文字與背景顏色對比較差。
* 文本（如連結文本和非連結文本）的顏色編碼在區分資訊方面具有重要意義。

>[!NOTE]
純用於裝飾目的的文字會排除在此成功標準之外。

#### 如何符合——對比（最低）(1.4.3){#how-to-meet-contrast-minimum}

請確定文字與其背景對比充分。 對比率取決於相關文本的大小和樣式：

* 對於大小小於18點（或14點粗體）的文字，文字的文字／影像與背景的對比率應至少為4.5:1。
* 對於大小至少為18點（或14點粗體）的文字，對比率應至少為3:1。
* 如果對背景進行圖案化，則任何文字周圍的背景都應該著色，以保持4.5:1或3:1比例。

要檢查對比度，請使用顏色對比工具，如[Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html)或[WebAIM顏色對比檢查器](https://www.webaim.org/resources/contrastchecker/)。 這些工具可讓您檢查顏色對，並報告任何對比問題。

或者，如果您不太在意指定頁面的外觀，可以選擇不指定背景和前景文字顏色。 不需要進行對比檢查，因為使用者的瀏覽器會決定文字和背景的顏色。

如果無法達到建議的對比度等級，您將需要提供頁面的替代等同版本（沒有顏色對比問題）的連結，或讓使用者根據自己的需求調整頁面色彩配置的對比度。

#### 詳細資訊——對比度（最低）(1.4.3){#more-information-contrast-minimum}

* [瞭解成功標準1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
* [如何符合成功標準1.4.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-contrast)

### 文字影像(1.4.5){#images-of-text}

* 成功標準1.4.5
* AA級
* 文字影像：如果所使用的技術可以實現視覺呈現，則除了下列項目外，文字會用來傳達資訊，而非文字影像：

   * 可自訂：文本影像可以根據用戶的需求進行可視化定製；
   * 基本：對所傳達的資訊而言，文本的具體呈現至關重要。

>[!NOTE]
Logotypes（屬於標誌或品牌名稱的文字）被視為必要項目。

#### 用途——文字影像(1.4.5){#purpose-images-of-text}

當偏好特定文字樣式時，通常會使用文字影像；例如，logotype或如果文字是從其他來源產生（例如，掃描紙張檔案）。 但是，與使用HTML呈現的文字和使用CSS建立樣式的文字相比，文字的影像缺乏彈性來變更尺寸或外觀，這對於有視覺障礙或閱讀困難的人而言可能是必要的。

#### How to Meet - Images of Text(1.4.5){#how-to-meet-images-of-text}

如果必須使用文字影像，請使用CSS將文字影像取代為HTML中的等同文字，讓文字以可自訂的方式使用。 有關如何實現此目的的示例，請參閱[C30:使用CSS將文字取代為文字影像，並提供使用者介面控制項來切換](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30)。

#### 詳細資訊——文字影像(1.4.5){#more-information-images-of-text}

* [瞭解成功標準1.4.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html)
* [如何符合成功標準1.4.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-text-presentation)

## 原則2:可操作{#principle-operable}

[原則2:可操作——用戶介面元件和導航必須可操作。](https://www.w3.org/TR/WCAG20/#operable)

### 暫停、停止、隱藏(2.2.2){#pause-stop-hide}

* 成功標準2.2.2
* A級
* 暫停、停止、隱藏：對於移動、閃爍、捲動或自動更新資訊，以下是正確的：

   * 移動、閃爍、滾動：對於(a)自動啟動、(b)持續超過五秒，且(c)與其他內容並行顯示的任何移動、閃爍或捲動資訊，使用者有暫停、停止或隱藏的機制，除非動作、閃爍或捲動是活動不可或缺的一部分；
   * 自動更新：對於任何(a)自動啟動且(b)與其他內容並行顯示的自動更新資訊，使用者有暫停、停止或隱藏更新或控制更新頻率的機制，除非自動更新是其必要活動的一部分。

注意事項有：

1. 有關閃爍或閃爍內容的要求，請參閱[「不以已知導致癲癇的方式設計內容(2.3)](#seizures)」。
1. 由於任何不符合此成功標準的內容都可能干擾使用者使用整個頁面的能力，因此網頁上的所有內容（無論是否用於符合其他成功標準）都必須符合此成功標準。 請參閱[符合性要求5:非干擾](https://www.w3.org/TR/WCAG20/#cc5)。
1. 由軟體定期更新或流向用戶代理的內容不需要保留或呈現在暫停開始和恢復演示之間生成或接收的資訊，因為這在技術上可能不可能，在許多情況下可能會誤導。
1. 如果在預先載入階段或類似情況中發生的動畫，對於所有使用者而言，在該階段無法進行互動，且若未指出進度，可能會混淆使用者，或導致使用者認為內容已凍結或中斷，則視為必要。

#### 用途——暫停、停止、隱藏(2.2.2){#purpose-pause-stop-hide}

某些使用者可能會發現移動的內容會分散注意力，並且難以將注意力集中在頁面的其他部分。 此外，對於無法跟上動態文字腳步的人而言，這些內容可能很難閱讀。

#### 如何開會——暫停、停止、隱藏(2.2.2){#how-to-meet-pause-stop-hide}

根據內容的性質，在建立包含移動、閃爍或閃爍內容的網頁時，您可以套用下列一或多個建議：

* 提供暫停捲動內容的方式，讓使用者有足夠的時間閱讀內容。 例如，新聞提示或自動更新的文字。
* 請確定眨眼的內容在5秒後停止閃爍。
* 使用適當的技術來顯示可由瀏覽器停用的閃爍內容。 例如，圖形交換格式(GIF)或可移植網路圖形(APNG)動畫檔案。
* 在網頁上提供表單控制項，讓使用者停用頁面上所有閃爍的內容。
* 如果無法使用上述任一功能，請提供包含所有內容但不眨眼的頁面連結。

#### 詳細資訊——暫停、停止、隱藏(2.2.2){#more-information-pause-stop-hide}

* [瞭解成功標準2.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html)
* [如何符合成功標準2.2.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-time-limits-pause)

### 緝獲量(2.3){#seizures}

[准則2.3緝獲：切勿以已知會導致癲癇的方式設計內容。](https://www.w3.org/TR/WCAG20/#seizure)

### 3個閃爍或低於閾值(2.3.1){#three-flashes-or-below-threshold}

* 成功標準2.3.1
* A級
* 閃爍三次或低於閾值：網頁不包含任何在任一秒內閃爍超過三次的內容，或flash低於一般flash和紅色flash臨界值。

>[!NOTE]
由於任何不符合此成功標準的內容都可能干擾使用者使用整個頁面的能力，因此網頁上的所有內容（無論是否用於符合其他成功標準）都必須符合此成功標準。 請參閱[符合性要求5:非干擾](https://www.w3.org/TR/WCAG20/#cc5)。

#### 用途——三個閃爍或低於閾值(2.3.1){#purpose-three-flashes-or-below-threshold}

在某些情況下，閃爍的內容可能導致感光性癲癇。 此成功標準可讓這些使用者存取並體驗所有內容，而不需擔心內容閃爍。

#### 如何符合——三個閃爍或低於閾值(2.3.1){#how-to-meet-three-flashes-or-below-threshold}

您應採取步驟，以確保套用下列技術：

* 確保元件在一秒內不會閃爍超過三次；
* 如果無法符合上述條件，則在螢幕上以像素顯示&#x200B;*小安全區*&#x200B;內閃爍的內容。 此區域是使用複數公式計算的，該公式在[G176中涵蓋：保持閃爍區域足夠小](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)，因此只有在必要閃爍內容&#x200B;*絕對*&#x200B;時才應採用此技術。

#### 詳細資訊——三個閃爍或低於臨界值(2.3.1){#more-information-three-flashes-or-below-threshold}

* [瞭解成功標準2.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html)
* [如何符合成功標準2.3.1](https://www.w3.org/WAI/WCAG20/quickref/#seizure)

### 標題為(2.4.2){#page-titled}的頁面

* 成功准則2.4.2
* A級
* 標題為：網頁標題可說明主題或目的。

#### 用途——標題為(2.4.2){#purpose-page-titled}的頁面

此成功標準可協助每個人（不論是否有任何特定的損害）快速識別網頁內容，而不需完整閱讀網頁。 當在瀏覽器標籤中開啟多個網頁時，這特別有用，因為頁面標題會顯示在標籤中，因此可快速找到。

#### 如何開會——標題為(2.4.2){#how-to-meet-page-titled}的頁面

在AEM中建立新的HTML頁面時，您可以指定頁面標題。 請確定標題已充分說明頁面內容，讓訪客可以快速識別內容是否與其需求有實際關係。

編輯頁面時，您也可以編輯頁面標題，該頁面可由&#x200B;**Sidekick** - **Page**&#x200B;標籤- **Page Properties...**

#### 更多資訊——標題為(2.4.2){#more-information-page-titled}的頁面

* [瞭解成功標準2.4.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)
* [如何符合成功標準2.4.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-title)

### 連結用途（在內容中）(2.4.4){#link-purpose-in-context}

* 成功准則2.4.4
* A級
* 連結用途（在內容中）:每個連結的目的可以單獨地從連結文本確定，也可以從連結文本連同其寫程式確定的連結上下文一起確定，除非連結的目的一般對用戶來說是模糊的。

#### 用途——連結用途（在內容中）(2.4.4){#purpose-link-purpose-in-context}

對所有使用者而言，無論是否受到損害，透過適當的連結文字清楚指出連結的方向至關重要。 這可協助使用者決定是否實際要追蹤連結。 對有目光的使用者而言，當頁面上有數個連結時（尤其是頁面文字較多時），有意義的連結文字非常有用，因為有意義的連結文字可更清楚地指出目標頁面的功能。 雖然輔助技術的使用者可以在單一頁面上產生所有連結的清單，但更輕鬆地瞭解連結文字與內容無關。

#### How to Meet - Link Purse(In Context)(2.4.4){#how-to-meet-link-purpose-in-context}

首先，請確定連結的目的在連結的文字中已清楚說明。

* 錯誤示例：

   * 文字：如需2010年秋季晚間課程的詳細資訊，請按一下這裡。
   * 原因：它沒有明確，明確地指出其目的地。

* 好例子：

   * 文字：2010年秋季夜校課程——詳細內容。
   * 原因：只要稍微調整文字和連結元素的位置，連結文字就可以改善：

連結應在各頁面上使用一致的措辭，尤其是導覽列。 例如，如果某個頁面上的特定頁面的連結名為&#x200B;**Publications**，請在其他頁面上使用該文字以確保一致性。

然而，在撰寫本文時，標題的使用存在一些問題：

* 標題屬性中包含的文字通常只能以工具提示快顯方式供滑鼠使用者使用，而且無法使用鍵盤存取。
* 螢幕閱讀程式可讀出標題屬性，但此功能可能未依預設啟用；因此，使用者可能不知道標題屬性存在。
* 很難改變標題文本的外觀，這意味著有些人可能很難或不可能閱讀。

因此，雖然title屬性可用來提供連結的額外內容，但請注意其限制，請勿將它當做適當連結文字的替代項目。

當連結由影像組成時，請確定影像的替代文字說明連結的目的地。 例如，如果書架的影像設定為連結至某人的出版品，則替代文字應為&#x200B;**John Smith』的出版物**，而非&#x200B;**Bookshelf**。

或者，如果連結錨點除了影像元素以外還包含說明連結用途的文字（因此文字會出現在影像旁邊），請為影像使用空白alt屬性：

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
上述程式碼片段為圖示，建議使用&#x200B;**Image**&#x200B;元件。

雖然建議您提供可識別連結目的的連結文字，而不需要額外的內容，但是可以認識到，這並非總能做到。 無上下文連結可用於下列情況，其HTML範例可在[如何符合成功准則2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs)中找到。

* 其中連結文字是緊密相關連結清單的一部分，而包含連結的清單項目則提供足夠的內容。
* 從&#x200B;*前面的*（非下）段文本中可清楚識別連結目的的。
* 如果連結包含在資料表中，因此可以從關聯的標題中清楚地確定目的。
* 其中，連結清單包含在一組標題中，標題本身提供了合適的上下文。
* 其中，連結清單包含在巢狀連結中，而巢狀連結上方的父清單項目則提供適當的內容。

在某些情況下，如果頁面上有數個連結（其中每個連結以複雜但必要的詳細資訊提供連結的方向），則可以提供網頁的替代版本，以顯示完全相同的內容，但連結文字未如此詳細。

或者，可以使用指令碼，使得在連結本身內提供最少數量的文本，但在激活定位在頁面頂部的適當控制項時，連結文本被&#x200B;*擴展*&#x200B;進一步詳細。 類似的方法是使用CSS來隱藏完整連結，以免有目光的使用者看到，但仍會將它完整輸出給螢幕閱讀程式使用者。 **&#x200B;這不在本檔案範圍內，但有關如何實現此目標的更多資訊，請參閱[更多資訊——連結用途（在內容中）(2.4.4)](#more-information-link-purpose-in-context)一節。

#### 詳細資訊——連結用途（在內容中）(2.4.4){#more-information-link-purpose-in-context}

* [瞭解成功標準2.4.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html)
* [如何符合成功標準2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs)
* [C7:使用CSS來隱藏連結文字的一部分](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)

## 原則3:可理解{#principle-understandable}

[原則3:可理解——資訊和用戶介面的操作必須可理解。](https://www.w3.org/TR/WCAG20/#understandable)

### 讓文字內容可讀且可理解(3.1){#make-text-content-readable-and-understandable}

[准則3.1可讀：讓文字內容可讀且易於理解。](https://www.w3.org/TR/WCAG20/#meaning)

### 頁面語言(3.1.1){#language-of-page}

* 成功標準3.1.1
* A級
* 頁面語言：每個網頁的預設人文語言可依程式設計決定。

#### 用途——頁面語言(3.1.1){#purpose-language-of-page}

此成功標準的目的是確保文字和其他語言內容正確呈現。 對於螢幕閱讀器使用者，這可確保內容正確發音，而視覺瀏覽器更可能正確顯示特定字元集。

#### How to Meet - Language of Page(3.1.1){#how-to-meet-language-of-page}

為符合此成功標準，可使用頁面頂端的`<html>`元素中的`lang`屬性來識別網頁的預設語言。 例如：

* 如果頁面以英文寫入，`<html>`元素應為：

   `<html lang = “en-gb”>`

* 而要轉換為美文的頁面，則應採用下列標準：

   `<html lang = “en-us”>`

**在AEM中，您的頁面預設語言是在建立頁面時設定，但在編輯頁面時也可以變更，頁面可由** Sidekick **-** Page **標籤-** Page Properties...存取- **Advanced** 頁籤。

#### 詳細資訊——頁面語言(3.1.1){#more-information-language-of-page}

* [瞭解成功標準3.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html)
* [如何符合成功標準3.1.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-doc-lang-id)
* 代碼基於ISO 639-1。 [W3學校網站](https://www.w3schools.com/tags/ref_language_codes.asp)提供更詳盡的每種語言代碼清單。

### 部件語言(3.1.2){#language-of-parts}

* 成功標準3.1.2
* AA級
* 部件語言：除了正確的名稱、技術術語、不確定語言的字詞和已成為立即周圍文本的白話部分的字詞或短語外，內容中每個段落或短語的人文語言可以寫程式確定。

#### 用途——部件語言(3.1.2){#purpose-language-of-parts}

此成功准則的目的類似於「頁面語言」的「成功准則」[，但適用於單一頁面上包含多種語言內容的網頁（例如，由於引文或不常見的借記字詞）。](#language-of-page)

套用此成功准則的頁面允許：

* 盲文轉換軟體以插入帶重音字元。
* 螢幕閱讀程式可正確讀出未使用預設語言的字詞。
* 翻譯工具（例如Google Translate），可將內容從一種語言正確翻譯為另一種語言。

#### How to Meet - Language of Parts(3.1.2){#how-to-meet-language-of-parts}

`lang`屬性可用來識別內容語言的變更。 例如，德文引號（ISO 639-1代碼&quot;de&quot;）如下所示：

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
現成可用的實例不支援區塊引號。 可開發自訂元件以支援此功能。

同樣地，如果`span`元素的使用方式如下，瀏覽器也可正確呈現不常見的借記字詞或片語：

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</span>.</p>
```

>[!NOTE]
在包含不同語言的名稱或城市，或使用預設語言中已司空見慣的借詞或片語（例如英文中的&#x200B;*schadenfreude*）時，您不必遵循此成功標準。

要使用適當的語言添加span元素，可以在RTE的源編輯模式中手動編輯HTML標籤，以便其讀取如上。 或者，系統管理員可將`lang`屬性包含在RTE中（請參閱[添加對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

#### 詳細資訊——部件語言(3.1.2){#more-information-language-of-parts}

* [瞭解成功標準3.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html)
* [如何符合成功標準3.1.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-other-lang-id)

### 幫助用戶避免和更正錯誤(3.3){#help-users-avoid-and-correct-mistakes}

[准則3.3投入援助：協助使用者避免並修正錯誤。](https://www.w3.org/TR/WCAG20/#minimize-error)

### 標籤或說明(3.3.2){#labels-or-instructions}

* 成功標準3.3.2
* A級
* 標籤或指示：當內容需要使用者輸入時，會提供標籤或指示。

#### 用途——標籤或說明(3.3.2){#purpose-labels-or-instructions}

提供說明以協助人們填寫表單是介面可用性的基本實務。 這樣做對於視覺或認知障礙的人特別有幫助，因為如果不是這樣，他們可能難以理解表單的佈局以及在特定表單域中提供的資料類型。

在AEM中，當您將表單元件（例如&#x200B;**文字欄位**）新增至頁面時，會新增預設標籤。 此預設標題取決於元件類型。您可以在該欄位的編輯對話框的&#x200B;**標題和文本**&#x200B;頁籤中添加自己的標題。 請務必確保標籤有助於使用者瞭解與每個表單元件相關聯的資料。

![「標題」和「文字」索引標籤（編輯對話方塊）;已新增標題「說明」。](assets/chlimage_1-22a.png)

此&#x200B;**Title**&#x200B;欄位必須用於欄位元素，因為它提供可用於輔助技術的標籤。 僅僅在欄位旁的文字中加上標籤是不夠的。

對於某些表單元件，您也可以使用「隱藏標題」核取方塊以視覺化方式 **隱藏標籤** 。以此方式隱藏的標籤仍適用於輔助技術，但無法顯示在螢幕上。雖然這在某些情況下是個好方法，但通常最好盡可能加入視覺標籤，因為有些使用者可能會看到畫面的一小部分 (一次看一個欄位)，並需要標籤來正確識別欄位。

#### 影像按鈕{#image-buttons}

其中使用影像按鈕(例如 **Image Button** 元件)時，編輯對話方塊的「標題」和「文字」索引標籤中的「標題 ******** 」欄位實際上會提供影像的替代文字，而非標籤。因此，在以下範例中，包含文字的影像 `Submit` 的alt文字為 `Submit`，使用編輯對話方塊中的 **Title** 欄位新增。

![在「標題」欄位（編輯對話方塊）中設定「替代文字」的影像按鈕。](assets/chlimage_1-23a.png)

#### 表單欄位群組{#groups-of-form-fields}

如果有一組相關控制項，例如 **Radio Group**，則可能需要該群組的標題以及個別控制項。在AEM中新增一組選項按鈕時，「標題 **」欄位會提供此群組標題，而個別標題會指定為選項按鈕(** Items ****)。

![新增項目至選項組。組標題是「聯繫方式」-在「標題」欄位中定義。](assets/chlimage_1-24a.png)

不過，群組標題和選項按鈕本身之間沒有程式化關聯。範本編輯人員必須將標題包住必要 `fieldset` 和 `legend` 標籤，才能建立此關聯，而這只能透過編輯頁面原始碼來完成。或者，系統管理員可以添加對這些元素的支援，使這些元素顯示在&#x200B;**欄位屬性**&#x200B;對話框中（請參閱[添加對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

#### 表單{#additional-considerations-for-forms}的其他注意事項

如果要以特定格式輸入資料，請在標籤文本中明確說明這一點。 例如，如果必須以`DD-MM-YYYY`格式輸入日期，請特別指出這是標籤的一部分。 這表示當螢幕閱讀程式使用者遇到欄位時，標籤會自動宣佈，以及格式的其他資訊。

如果表單欄位的輸入是必填的，請使用標籤中的必要字詞來清楚說明。AEM在需要欄位時新增星號，但最好將字詞加入標 `required`簽本身(在編輯對話方塊的「 **Title** 」欄位中)。

![在「標題」欄位中新增螢幕閱讀器使用者的其他資訊（必填字詞）。](assets/chlimage_1-25a.png)

標籤的定位也很重要，因為它可協助標籤找到適當的欄位。 當使用者面對複雜的表單時，這尤其重要。 遵守以下公約：

* 核取方塊或選項按鈕：

   標籤會立即置於欄位右側。

* 所有其他表單元件（例如文字方塊、組合方塊）:

   標籤會立即置於欄位的上方或左側。

在功能非常有限的簡單表單中，適當標籤`Submit`按鈕可當成相鄰欄位的標籤（例如`Search`）。 當尋找標籤文字的空間時，這項功能會很有用。

#### 詳細資訊——標籤或指示(3.3.2){#more-information-labels-or-instructions}

* [瞭解成功標準3.3.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html)
* [如何符合成功標準3.3.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-minimize-error-cues)

