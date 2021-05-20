---
title: 配置檔案類型設定
seo-title: 配置檔案類型設定
description: 了解如何配置檔案類型設定。
seo-description: 了解如何配置檔案類型設定。
uuid: ab037659-c6ff-4de9-9417-f5a6fc8122cb
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ab19b248-8931-4cf6-b6a5-fb7b067c4a49
feature: PDF 產生器
source-git-commit: 3bb12f6323398971ec315f49611a39977bd548a2
workflow-type: tm+mt
source-wordcount: '6171'
ht-degree: 0%

---


# 配置檔案類型設定{#configuring-file-type-settings}

在PDF產生器中，您可以為支援的檔案類型設定應用程式設定。 在Windows上，您可以為每個支援的檔案類型設定應用程式設定。 在UNIX和Linux上，您可以為HTML到PDF和OpenOffice設定應用程式設定。

在「檔案類型設定」頁上，您可以執行以下任務：

* [建立或編輯檔案類型設定](#create-or-edit-file-type-settings)
* 指定預設要使用的檔案類型設定（請參閱[匯入和匯出PDF產生器組態檔](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)）
* [變更預設設定](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [啟用PDF/A支援](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [刪除檔案類型設定](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>檔案類型設定不適用於後援轉換器，例如Acrobat for HTML轉換為PDF、Microsoft PowerPoint、Microsoft Word和Microsoft Excel。

## 建立或編輯檔案類型設定{#create-or-edit-file-type-settings}

建立或編輯檔案類型設定，以指定應用程式如何處理支援的檔案類型轉換。 在Windows上，您可以為每個支援的檔案類型設定應用程式設定。 在UNIX和Linux上，您可以為HTML到PDF和OpenOffice設定應用程式設定。

1. 在管理控制台中，按一下「**[!UICONTROL 服務]** > **[!UICONTROL PDF生成器]** > **[!UICONTROL 檔案類型設定]**」。
1. 按一下「新增」或按一下設定的名稱。
1. 在「檔案名副檔名」框中，鍵入為此應用程式接受的檔案類型的檔案名副檔名（以逗號分隔）。 請勿包含擴充功能之前的句號或之間的空格。 預設值為`bmp,gif,jpeg,jpg,tif,tiff,png`。
1. （可選）要在圖形或影像中使用文本的光學代碼識別(OCR)，請選擇「使用OCR」並設定以下選項：

**主要OCR語言：** 用於識別字元的OCR引擎語言。預設為英文（美國）。

**PDF輸出樣式：** 選取「可搜尋影像」，在前景中具有頁面的點陣圖影像，並在下方的不可見圖層上顯示掃描的文字。頁面外觀不會變更，但文字可供選取及讀取。 選擇「格式化文本和圖形」(Formatted Text &amp; Graphics)，使用已識別的文本、字型、圖片和其他圖形元素重構原始頁面。 預設為可搜尋影像（完全）。

**下採樣影像：** 減少彩色、灰度和單色影像中的像素數。完成OCR後，會執行掃描影像的下採樣。 預設值為最低(600 dpi)。 如果您將PDF輸出樣式設為「可搜尋影像」（完全），則無法使用此選項。

1. 填妥以下小節中的必要資訊：

[匯入和匯出PDF產生器組態檔](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

[Adobe PDF匯出設定（僅限Windows）](#adobe-pdf-export-settings-windows-only)

[HTML至PDF設定](#html-to-pdf-settings)

[Flash影片至PDF設定](#flash-videos-to-pdf-settings)

[XPS到PDF設定](#xps-to-pdf-settings)

[PDF優化程式設定](/help/forms/using/admin-help/configuring-file-type-settings.md)

[Microsoft Excel設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-excel-settings-windows-only)

[Microsoft PowerPoint設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-powerpoint-settings-windows-only)

[Microsoft Project設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-project-settings-windows-only)

[Microsoft Word設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-word-settings-windows-only)

[Microsoft Visio設定（僅Windows）](#visio)

[Microsoft Publisher設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-publisher-settings-windows-only)

[AutoCAD設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#autocad-settings-windows-only)

[OpenOffice設定](/help/forms/using/admin-help/configuring-file-type-settings.md#openoffice-settings)

[其他應用程式的設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#other-applications-settings-windows-only)

   要轉到其他部分，請按一下其網頁上的連結，或使用&#x200B;**[!UICONTROL Next]**&#x200B;或&#x200B;**[!UICONTROL Previous]**&#x200B;按鈕。

1. 完成所有部分後，按一下&#x200B;**[!UICONTROL Save]**&#x200B;或&#x200B;**[!UICONTROL Save As]**&#x200B;並提供設定的名稱。

可自訂各種檔案類型的支援。 (請參閱[使用AEM表單寫程式](https://www.adobe.com/go/learn_lc_programming_11)中的「[新增對其他原生檔案格式的支援](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)」。)

## 更改預設設定{#change-the-default-settings}

您可以變更套用至新建立來源之Adobe PDF設定、安全設定及檔案類型設定的預設值。 更改預設值不會影響現有源的設定。

1. 在管理控制台中，按一下「**[!UICONTROL 服務> PDF生成器]**」。
1. 在&#x200B;**[!UICONTROL Adobe PDF設定]**、**[!UICONTROL 檔案類型設定]**&#x200B;或&#x200B;**[!UICONTROL 安全設定]**&#x200B;頁面上，按一下&#x200B;**[!UICONTROL 設定預設設定]**。
1. 選取您偏好的預設設定。 「設定預設設定」頁面提供下列一或多個設定：

   **[!UICONTROL Adobe PDF設定]**:原始預設值為Standard(Acrobat 6)。

   **[!UICONTROL 安全設定]**:原始預設值為無安全性(Acrobat 5)。

   **[!UICONTROL 檔案類型設定]**:原始預設值為「標準」。

1. 按一下「**[!UICONTROL 儲存]**」。

## 刪除檔案類型設定{#delete-a-file-type-setting}

您可以刪除不再使用的檔案類型設定。

1. 在管理控制台中，按一下「**[!UICONTROL 服務> PDF生成器>檔案類型設定]**」。
1. 選取要刪除之設定旁的核取方塊。 您可以選擇多個源。 PDF產生器一律會包含旁邊沒有核取方塊的設定，且無法刪除。
1. 按一下&#x200B;**[!UICONTROL Delete]**，然後在「刪除確認」頁上按一下&#x200B;**[!UICONTROL Delete]**。

## 影像到PDF設定{#image-to-pdf-settings}

下列選項決定如何將影像檔案轉換為PDF。 有關訪問這些設定的說明，請參閱[建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**副檔名：** 以逗號分隔的副檔名清單，可供轉換。

**嘗試後援轉換工具：** PDF產生器可使用Java™或Acrobat將影像檔案轉換為PDF。當選取此選項且轉換失敗或達到指定的逾時限制時，PDF產生器會使用替代方法來嘗試轉換。 如果替代方法失敗或達到指定的逾時限制，則會將例外寫入日誌檔案。

>[!NOTE]
>
>JPEG 2000檔案只能使用Acrobat進行轉換。

**使用OCR:** 指定是否要將OCR（光學字元識別）套用至PDF。OCR軟體可讓您搜索、更正和複製PDF中的文本。

***注意&#x200B;**:只有Microsoft Windows才支援OCR PDF（可搜尋的PDF）功能。*

**主要OCR語言：** 指定OCR引擎用於識別字元的語言。

**PDF輸出樣式：** 決定要產生的PDF類型。所有格式都會將OCR、字型和頁面識別應用於文本影像，並將它們轉換為普通文本。

**可搜尋的影像：** 確保文字可供搜尋及選取。此選項可保留原始影像，視需要對其進行描述，並在其上放置隱藏的文本層。 「縮減取樣影像」選項可決定影像是否縮減取樣以及縮減取樣的程度。

**可搜尋的影像（完全）:** 確保文字可供搜尋及選取。此選項可保留原始影像，並將不可見的文本層置於其上。 建議用於要求原始影像保真度最高的情況。

**ClearScan:** 合成與原始字型接近的新類型3字型，並使用低解析度副本保留頁面背景。

**縮減影像範例：** 完成OCR後，減少彩色、灰階和單色影像的像素數。選擇要應用的縮減取樣程度。 編號較高的選項可減少縮減取樣，因而產生解析度較高的PDF。

## Adobe PDF匯出設定（僅限Windows）{#adobe-pdf-export-settings-windows-only}

Adobe PDF匯出設定區段中的「匯出檔案類型」設定，用於將PDF檔案轉換為其他格式。 預設為HTML 4.01，含階層式樣式表(CSS)1.0(*.htm、*.html)。

有關訪問此設定的說明，請參閱[建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

## HTML-to-PDF設定{#html-to-pdf-settings}

下列選項決定HTML檔案轉換為PDF的方式。 有關訪問這些選項的說明，請參閱[建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**嘗試後援轉換工具：** PDF產生器可使用Java™或Acrobat，將HTML檔案轉換為PDF。當選取此選項且轉換失敗或達到指定的逾時限制時，PDF產生器會使用替代方法來嘗試轉換。 如果替代方法失敗或達到指定的逾時限制，則會將例外寫入日誌檔案。

**預設編碼：** 從作業系統和字母的功能表設定檔案文字的輸入編碼。僅當HTML源檔案未指定編碼類型時，才使用「預設編碼」選項中顯示的選項。

**強制選取的編碼：** 忽略HTML來源檔案中指定的任何編碼，並使用預設編碼選項中顯示的選取內容。

### 尖峰設定{#spidering-settings}

** Spidering會掃描網頁，以尋找其他網頁的連結。遇到到其他網頁的連結時，目標頁面會被擷取並包含在所產生的PDF檔案中。 啟用以下選項可設定要擷取並轉換為PDF的層級數：

**僅取得X層：** 從基礎頁面URL編目並轉換頁面至指定層級深度。值1隻會轉換提供的URL。

**取得整個網站：** 從提供的URL開始轉換整個網站。

**保持在相同路徑上：** 呈現期間，任何指向與基本URL不在相同相對路徑上之頁面的連結都不會轉換。

**保留在相同伺服器上：** 呈現期間，任何指向不同伺服器上頁面的連結都不會轉換。只會轉換指向與指定URL相同之伺服器的連結。

### 頁面轉換設定{#page-conversion-settings}

啟用這些選項可指定HTML頁面的轉換方式。 根據頁面大小，寬度、高度和邊界值會相應調整。

**頁面大小：** 選擇自訂並指定寬度和高度，或選取預先定義的維度。

**方向：** 為轉換的PDF檔案選取直向或橫向。

**邊距：** 指定生成的PDF文檔中的邊距（上、下、左和右）。

**將書籤新增為PDF:** 將書籤新增至PDF檔案。

**啟用標籤的PDF:** 在PDF檔案中嵌入標籤。

**設定初始視圖設定：** 用於配置文檔選項、窗口選項和用戶介面選項。這些設定會決定內容最初的顯示方式。

### 文檔選項{#document-options}

啟用這些選項可指定如何顯示內容、如何顯示PDF文檔中的頁面，以及如何指定放大級別：

**顯示：** 選取當PDF檔案開啟時要在Acrobat中開啟的窗格。

**頁面佈局：** 選擇PDF文檔的頁面佈局類型。

**放大率：** 為PDF文檔的初始視圖選擇預設的放大率，或選擇自定義值。選擇預設設定表示將使用預設的Acrobat放大率。

**開啟至頁碼：** 指定PDF開啟至的頁碼。

### 窗口選項{#window-options}

啟用這些選項可指定窗口的大小和顯示方式。

**將視窗調整為初始頁面大小：** 將Acrobat視窗調整為初始頁面的大小。

**在螢幕上居中窗口：** 開啟螢幕中央的窗口。

**以全螢幕模式開啟：** 以全螢幕模式開啟視窗。

**顯示：** 在窗口中顯示文檔標題或檔案名。

### 用戶介面選項{#user-interface-options}

啟用以下選項以指定窗口外觀：

**隱藏菜單欄：** 隱藏PDF文檔中的菜單欄。

**隱藏工具欄：** 隱藏PDF文檔中的工具欄。

**隱藏窗口控制項：** 隱藏PDF文檔中的窗口控制項。

## Flash視訊為PDF設定{#flash-videos-to-pdf-settings}

PDF產生器支援提交視訊以供AdobeFlash（SWF或FLV檔案），以及建立含有視訊的PDF檔案以供內嵌AdobeFlash。 此轉換不需要在表單伺服器上安裝AdobeFlash Player。 有關訪問此選項的說明，請參閱[建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**副檔名：** 以逗號分隔的副檔名清單，可供轉換。

## XPS到PDF設定{#xps-to-pdf-settings}

XML紙張規範(XPS)在Windows打印機中使用。 此格式為Microsoft格式，可從任何Microsoft Office應用程式中建立。 AEM forms提供轉換XPS檔案PDF的功能。

**副檔名：** 以逗號分隔的清單，列出所有可轉換的XPS副檔名。目前有一種格式：.xps。

## PDF優化程式設定{#pdf-optimizer-settings}

PDF產生器支援縮減PDF檔案大小的功能。 使用所有這些設定還是僅使用一些設定取決於您要如何使用檔案以及檔案必須具有的基本屬性。 在大多數情況下，預設設定都是最有效率的：通過刪除嵌入的字型、壓縮影像以及從不再需要的檔案中刪除項來節省空間。

>[!NOTE]
>
>優化數字簽名的文檔會刪除並使數字簽名失效。

有關訪問此設定的說明，請參閱[建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**Target PDF版本：** 指定與PDF相容的Acrobat版本。

### 字型 {#fonts}

1. 選擇&#x200B;**字型。**
1. 選取下列其中一個選項：

   **取消嵌入所有字型：** 取消嵌入所有嵌入字型。

   **不要取消嵌入任何字型：** 不取消嵌入任何字型。

   **取消嵌入某些字型：** 僅取消嵌入指定的字型。請按照下列步驟指定要取消嵌入的字型：

   * 如有必要，請從&#x200B;**字型源**&#x200B;下拉菜單中選擇其他字型目錄。 此下拉菜單列出&#x200B;**首頁>設定>核心繫統>核心配置**&#x200B;中指定的字型目錄。
   * 從&#x200B;**可用字型**&#x200B;清單中選擇一個或多個字型，然後按一下&#x200B;**添加**。 這些字型將添加到&#x200B;**Fonts to Unembed**&#x200B;清單中。
   * 如果要取消嵌入表單伺服器上不存在的某些字型，請在&#x200B;**Add fonts to unembed**&#x200B;框中輸入這些字型的名稱。 按一下&#x200B;**「新增」**。

   >[!NOTE]
   >
   >*如果要取消嵌入子集嵌入文檔中的某些字型，請在字型名前加上+號。例如， &quot;+Helvetica&quot;。*

1. 如果只想嵌入嵌入字型的在用子集，請選擇&#x200B;**Subset all embedded fonts**。

   >[!NOTE]
   >
   >*如果您搭配「取消內嵌某些字型」使用此選&#x200B;**項**，「將字型新增至取消內嵌」**清單中的字**型仍會完全取消內嵌。*

   >[!NOTE]
   >
   >*字型子設定是僅嵌入部分字型的技術。字型子集僅包含文檔中使用的字元。*

### 透明度 {#transparency}

如果您的PDF文檔包含包含透明度的圖稿，則可以使用PDF優化程式設定來平面化透明度並減小檔案大小。

>[!NOTE]
>
>如果選取Acrobat 4.0和更新版本作為Target PDF版本，所有透明物件都會平面化。 對於其他Target PDF版本，支援透明度，並且您可以配置透明度設定。

選擇&#x200B;**透明度**&#x200B;以在優化PDF文檔時配置透明度設定。

**透** 明級別指定要保留的向量資訊量。較高的設定會保留更多向量對象，而較低的設定會柵格化更多向量對象；中間設定會保留向量形式的簡單區域，並柵格化複雜區域。 選擇最低設定以柵格化所有圖稿。

>[!NOTE]
>
>發生的光柵化量取決於頁面的複雜性和重疊對象的類型。

**線條圖和文** 本解析度，所有對象（包括影像、向量圖稿、文本和漸變）都柵格化到這些對象。支援的值為1像素/英吋(ppi)至9600 ppi。

>[!NOTE]
>
>線條圖和文字解析度一般應設為600-1200 ppi，以提供高品質的光柵化效果，尤其是襯線或小點大小的類型。

**漸變和網格** 解析度，漸變和網格柵格化到此解析度。支援的值為1 ppi至1200 ppi。

>[!NOTE]
>
>漸變和網格解析度通常應設定為150-300 ppi，因為漸變、陰影和羽化的質量不會隨著解析度的提高而提高，但打印時間和檔案大小會增加。

**將所有文本轉換** 為輪廓將所有類型對象（點類型、區域類型和路徑類型）轉換為輪廓並丟棄包含透明度的頁面上的所有類型字形資訊。此選項可確保拼合期間文字的寬度保持一致。 請注意，啟用此選項將使小字型在Acrobat中查看時或在低解析度的台式打印機上打印時看起來稍微粗一些。 它不會影響打印在高解析度打印機或影像集上的類型的質量。

**將所有描邊轉換為** 輪廓將所有描邊轉換為包含透明度的頁面上的簡單填充路徑。此選項可確保拼合期間筆畫的寬度保持一致。 請注意，啟用此選項會導致薄筆划顯示為稍粗，並可能降低拼合效能。

**按一下復** 雜區域確保向量圖稿和柵格化圖稿之間的邊界沿對象路徑下降。此選項可減少記錄部分時產生的拼接成品

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>某些打印驅動程式對光柵和向量圖的處理方式不同，有時會導致顏色拼接。 通過禁用某些打印驅動程式特定的顏色管理設定，您可以最大限度地減少拼接問題。 這些設定因每台打印機而異，因此有關詳細資訊，請參閱打印機隨附的文檔。

保留疊印：將透明圖稿的顏色與背景顏色混合，以建立疊印效果。

下表顯示了常見的打印機類型及其以dpi測量的解析度、以每英吋行(lpi)測量的預設螢幕規則，以及以每英吋像素(ppi)測量的影像的重採樣解析度。 例如，如果要打印到600 dpi雷射打印機，則輸入170作為要重新取樣影像的解析度。

**** 影像選擇影像以指定顏色、灰度和單色影像的壓縮和重採樣選項。您可能希望嘗試使用這些選項來在檔案大小和影像質量之間找到適當的平衡。彩色和灰度影像的解析度設定應是打印檔案的線螢幕的1.5到2倍。 單色影像的解析度應與輸出設備相同，但請注意，以高於1500 dpi的解析度保存單色影像會增加檔案大小，而不會顯著改善影像質量。 將被放大的影像，如地圖，可能需要更高的解析度。

>[!NOTE]
>
>重新採樣單色影像可能具有意外的查看結果，例如沒有影像顯示。 如果發生此情況，請關閉重新取樣並重新轉換檔案。 子採樣最有可能出現此問題，而雙立方縮減採樣最不可能出現此問題。

<table>
 <tbody>
  <tr>
   <th><p><strong>打印機解析度</strong></p> </th>
   <th><p><strong>預設行螢幕</strong></p> </th>
   <th><p><strong>影像解析度</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 dpi（雷射打印機）</p> </td>
   <td><p>60lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi（雷射打印機）</p> </td>
   <td><p>85磅</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 dpi（照排機）</p> </td>
   <td><p>120lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi（照排機）</p> </td>
   <td><p>150lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

#### 放棄對象{#discard-objects}

* 選擇&#x200B;**放棄對象**&#x200B;以指定要從PDF中刪除的對象並優化CAD繪圖中的曲線。
* **捨棄所有表單提交、匯入和重設動作**:停用與提交或匯入表單資料相關的所有動作，並重設表單欄位。此選項會保留動作連結到的表單物件。
* **捨棄所有JavaScript動作**:從PDF中移除任何使用JavaScript的動作。
* **捨棄內嵌的頁面縮圖**:移除內嵌的頁面縮圖。此選項對於大型文檔非常有用，在按一下「頁面」按鈕後，可能需要花很長時間繪製頁面縮略圖。
* **將平滑線轉換為曲線**:減少用於在CAD繪圖中建立曲線的控制點數，從而縮小PDF檔案並加快螢幕繪製。
* **放棄嵌入的打印設定**:從文檔中刪除嵌入的打印設定，如頁面縮放和雙工模式。
* **捨棄書籤**:從文檔中刪除所有書籤。
* **平面化表單欄位**:使表單欄位無法使用，而外觀不會變更。表單資料會與頁面合併，成為頁面內容。
* **捨棄所有替代影像**:移除除了用於螢幕檢視的版本以外的所有影像版本。有些PDF包含多個版本的相同影像，以用於不同用途，例如螢幕上低解析度檢視和高解析度列印。
* **放棄文檔標籤**:從文檔中刪除標籤，這也會刪除文本的輔助功能和重排功能。
* **偵測及合併影像片段**:查找碎片為薄切片並嘗試將切片合併為單個影像或蒙版的影像或蒙版。
* **放棄嵌入的搜索索引**:刪除嵌入的搜索索引，從而減小檔案大小。

#### 放棄用戶資料{#discard-user-data}

選擇&#x200B;**放棄用戶資料**&#x200B;以刪除您不想分發或與其他用戶共用的任何個人資訊。

* **捨棄所有注釋、Forms和多媒體**:從PDF中移除所有注釋、表單、表單欄位和多媒體。
* **放棄所有對象資料**:從PDF中刪除所有對象。
* **捨棄外部交叉引用**:刪除指向其他文檔的連結。跳至PDF內其他位置的連結不會移除。
* **捨棄隱藏圖層內容並平面化可見圖層**:減小檔案大小。最佳化的檔案看起來像原始PDF，但不包含圖層資訊。
* **放棄文檔資訊和元資料**:刪除文檔資訊字典和所有元資料流中的資訊。（使用「另存新檔」命令，將中繼資料資料流還原為PDF的副本。）
* **放棄檔案附件**:刪除所有檔案附件，包括作為注釋添加到PDF的附件。（PDF Optimizer不會最佳化附加的檔案。）
* **捨棄其他應用程式的專用資料**:從PDF文檔中去除僅對建立文檔的應用程式有用的資訊。此設定不會影響PDF的功能，但會減小檔案大小。

### 清理{#clean-up}

選擇&#x200B;**清除**以從文檔中刪除不必要的項。
這些項目包括對您預定使用文檔而言過時或不必要的元素。 移除某些元素可能會嚴重影響PDF的功能。 依預設，僅選取不影響功能的元素。 如果您不確定移除其他選項的可能影響，請使用預設選取項目。

**壓縮**

從下拉式選單中選取下列其中一個「完全壓縮」選項：

* 壓縮整個檔案
* 壓縮文檔結構
* 移除壓縮
* 保持壓縮不變

**使用Flate來編碼未編碼的資料流**:將全部壓縮套用至所有未編碼的資料流。

**捨棄無效書籤**:刪除指向文檔中要刪除的頁面的書籤。

**放棄未引用的命名目標**:從PDF檔案內移除未在內部參照的已命名目的地。此選項不會檢查其他PDF檔案或網站的連結。

**最佳化PDF以快速進行Web檢視**:重新建構PDF檔案，以便從Web伺服器一次性下載頁面（位元組服務）。

**在使用LZW編碼的資料流中，請改用Flate**:對使用LZW編碼的所有內容流和影像應用全壓縮。

**放棄無效連結**:移除跳至無效目的地的連結。

**最佳化頁面內容**:將所有行尾字元轉換為空格字元，這可改善Flate壓縮。

## Microsoft Excel設定（僅限Windows）{#microsoft-excel-settings-windows-only}

這些選項決定了Microsoft Excel檔案的轉換方式。 有關訪問這些選項的說明，請參閱[建立或編輯檔案類型設定](#create-or-edit-file-type-settings)。

**請嘗試使用OpenOffice作為備援轉換工具**:當選取此選項，且使用Microsoft Excel的轉換失敗或達到指定的逾時限制時，PDF產生器會使用OpenOffice來嘗試轉換。如果使用OpenOffice的轉換失敗或達到指定的超時限制，則會將異常寫入日誌檔案。

**副檔名**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。預設值為`xls,xlsx`。 請勿在擴充功能之前加上句號或之間加上空格。

**建立PDF/A-1a相容檔案**:強制使用PDF/A-1b:2005 RGB Adobe PDF設定。

**將書籤新增至Adobe PDF**:將Excel工作表名稱轉換為書籤。預設會選取此選項。

**將工作表調整為單一頁面**:縮小文字大小，以符合單一頁面上的工作表大小。

**轉換整個活頁簿**:轉換Excel檔案中的所有工作表。如果未選取此選項，則只會轉換目前的頁面。

**自動運行宏**:在轉換文檔之前，運行Excel文檔中的任何宏（如插入當前時間的宏）。

**轉換文檔資訊**:根據源檔案中的文檔資訊添加PDF文檔屬性。這包括檔案標題、作者、主旨和關鍵字等資訊。

**新增連結至Adobe PDF**:將源檔案中的超連結轉換為PDF文檔中的超連結。

**將來源檔案附加至Adobe PDF**:選取此選項時，原始Excel電子錶格將作為附件插入生成的PDF文檔中。

**啟用無障礙和帶有標籤Adobe PDF的Reflow**:將標籤內嵌在PDF檔案中，以啟用協助工具和重排。

**要載入的Excel增益集清單**:依預設（基於安全考量），將Excel檔案轉換為PDF時，不會執行Excel增益集。若要允許在轉換期間執行某些Excel增益集，請提供增益集名稱的逗號分隔清單。

**要轉換的工作表清單**:當此方塊為空時，Excel試算表中的所有工作表都會包含在產生的PDF中。要選擇性地轉換工作表的子集，請提供以逗號分隔的工作表名稱清單。

## Microsoft PowerPoint設定（僅限Windows）{#microsoft-powerpoint-settings-windows-only}

這些選項決定了Microsoft PowerPoint檔案的轉換方式。 有關訪問這些選項的說明，請參閱[建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**[!UICONTROL 請嘗試使用OpenOffice作為備援轉換工具]**:當選中此選項且使用Microsoft PowerPoint的轉換失敗或達到指定的逾時限制時，PDF生成器將嘗試使用OpenOffice進行轉換。如果使用OpenOffice的轉換失敗或達到指定的超時限制，則會將異常寫入日誌檔案。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。預設值為ppt,pptx。 請勿在擴充功能之前加上句號或之間加上空格。

**[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。預設會選取此選項。

**[!UICONTROL 將書籤新增至Adobe PDF]**:將PowerPoint標題轉換為書籤。預設會選取此選項。

**[!UICONTROL 將來源檔案附加至Adobe PDF]**:將源檔案作為附件添加到PDF檔案中。預設會取消選取此選項。

**[!UICONTROL 啟用無障礙和帶有標籤Adobe PDF的Reflow]**:將標籤內嵌至PDF檔案。預設會取消選取此選項。

**[!UICONTROL 將多媒體轉換為PDF多媒體]**:盡可能將多媒體轉換為PDF多媒體。預設會選取此選項。

**[!UICONTROL 轉換揚聲器注釋]**:將揚聲器注釋轉換為PDF。

**[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行PowerPoint文檔中的任何宏（如插入當前時間的宏）。

**[!UICONTROL 基於PowerPoint打印機設定的PDF佈局]**:使用PowerPoint打印機設定來佈局PDF文檔。

**[!UICONTROL 新增連結至Adobe PDF]**:轉換檔案時保留現有連結。連結的外觀基本不變。 只有選取了「啟用協助工具」選項，才能建立連結。 預設會取消選取此選項。

**[!UICONTROL 在Adobe PDF中儲存投影片轉變]**:轉換幻燈片過渡。預設會選取此選項。

**[!UICONTROL 在Adobe PDF中儲存動畫]**:將轉換的動畫保存在PDF檔案中。

**[!UICONTROL 將隱藏的投影片轉換為PDF頁面]**:轉換隱藏的幻燈片。

**[!UICONTROL 建立PDF/A-1a相容檔案]**:強制使用PDF/A-1b:2005 RGB Adobe PDF設定。生成PDF檔案時，不會轉換一些PowerPoint功能。 如果PowerPoint轉變在Acrobat中沒有等效轉變，則會替換類似的轉變。 如果同一幻燈片中有多個動畫效果，則使用一個效果。 頁面轉變和項目符號調整項目會經過轉換。

## Microsoft Project設定（僅限Windows）{#microsoft-project-settings-windows-only}

這些選項決定了Microsoft Project檔案的轉換方式。 有關訪問這些選項的說明，請參閱[建立或編輯檔案類型設定](#create-or-edit-file-type-settings)。

1. **[!UICONTROL 副檔名：]** 指定此應用程式接受的檔案類型副檔名，並以逗號分隔。預設值為`mpp`。 請勿在擴充功能之前加上句號或之間加上空格。

1. **[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。預設會選取此選項。
1. **[!UICONTROL 將來源檔案附加至Adobe PDF]**:將源檔案作為附件添加到PDF檔案中。
1. **[!UICONTROL 建立PDF/A-1a相容檔案]**:強制使用PDF/A-1b:2005 RGB Adobe PDF設定。
1. **[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行Microsoft Project文檔中的任何宏（如插入當前時間的宏）。

## Microsoft Word設定（僅限Windows）{#microsoft-word-settings-windows-only}

這些選項決定了Microsoft Word檔案的轉換方式。 有關訪問這些選項的說明，請參閱[建立或編輯檔案類型設定](#create-or-edit-file-type-settings)。

**[!UICONTROL 請嘗試使用OpenOffice作為備援轉換工具]**:當選擇此選項且使用Microsoft Word的轉換失敗或達到指定的逾時限制時，PDF生成器將嘗試使用OpenOffice進行轉換。如果使用OpenOffice的轉換失敗或達到指定的超時限制，則會將異常寫入日誌檔案。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。預設值為`doc,docx,rtf,txt`。 請勿在擴充功能之前加上句號或之間加上空格。

**[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。預設會選取此選項。

**[!UICONTROL 將書籤新增至Adobe PDF]**:將標題轉換為書籤。預設會選取此選項。

**[!UICONTROL 將來源檔案附加至Adobe PDF]**:將源檔案作為附件添加到PDF檔案中。

**[!UICONTROL 將交叉參照和目錄轉換為連結]**:將所有交叉引用和目錄條目轉換為連結。預設會選取此選項。

**[!UICONTROL 啟用無障礙和帶有標籤Adobe PDF的Reflow]**:將標籤內嵌至PDF檔案。預設會選取此選項。

**[!UICONTROL 建立PDF/A-1a相容檔案]**:如果選取，會強制使用PDF/A-1b:2005 RGB Adobe PDF設定。

**[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行Word文檔中的任何宏（如插入當前時間的宏）。

**[!UICONTROL 在Adobe PDF中保留文檔標籤]**:將Word文檔中的標注轉換為PDF檔案中的注釋。

**[!UICONTROL 新增連結至Adobe PDF]**:將源檔案中的超連結轉換為PDF文檔中的超連結。

**[!UICONTROL 轉換腳注和章節附註連結]**:建立從腳注和注釋引用到PDF文檔中注釋的連結。

**[!UICONTROL 在Adobe PDF中將顯示的註解轉換為附註]**:將Word文檔中的注釋轉換為PDF文檔中的文本注釋。

**[!UICONTROL 啟用進階標籤]**:新增進階標籤以增強協助工具。

**[!UICONTROL 將所有樣式轉換為書籤]**:將Word文檔中的所有樣式轉換為PDF文檔中的書籤。

**[!UICONTROL 將指定的樣式轉換為書籤]**:將您在具有級別欄位的樣式中定 **[!UICONTROL 義的樣]** 式轉換為PDF文檔中的書籤。

**[!UICONTROL 具有層級的樣式]**:指定Word文檔中的哪些樣式將轉換為PDF文檔中的書籤。也會指定書籤的層級。 要使用此功能，請取消選擇&#x200B;**[!UICONTROL 將所有樣式轉換為書籤]**&#x200B;選項，並以下列格式指定樣式名稱：

**styleName1=level1[,styleName2=level2...]**

如果Microsoft Word樣式名稱包含逗號(,)或等號(=)，請在特殊字元前面加上逸出字元(&quot;\_)。 例如，指定名為&quot;Heading, 1&quot;的樣式作為Heading\, 1。

**Acrobat PDFMaker編碼：** 指定Acrobat PDFMaker的輸入純文字檔案的編碼類型。例如，如果您使用UTF-8編碼檔案，請選取UTF-8以獲得最佳結果。

## Microsoft Visio設定（僅Windows） {#visio}

**轉換文檔資訊**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。預設會選取此選項。 預設會啟用此選項。

**新增連結至Adobe PDF**:保留所有連結。預設會選取此選項。

**將書籤新增至Adobe PDF**:將標題轉換為書籤。預設會選取此選項。

**將來源檔案附加至Adobe PDF**:將源檔案作為附件添加到PDF檔案中。

**在Adobe PDF中一律平面化圖層**:拼合所有Visio圖層。

**轉換所有頁面**:轉換Visio檔案的所有頁面。

**在Adobe Acrobat中檢視時，開啟「圖層」面板**:如果Visio圖層未平面化，則開啟一個窗口，在該窗口中，可以指定使用Acrobat開啟時PDF檔案中保留的圖層。預設會選取此選項。

**建立PDF/A-1b相容檔案**:強制使用Adobe PDF設定PDF/A-1b:2005(RGB)。

**將注釋轉換為Adobe PDF注釋**:將Visio注釋轉換為PDF注釋。

## Microsoft Publisher設定（僅限Windows）{#microsoft-publisher-settings-windows-only}

這些選項決定了Microsoft Publisher檔案的轉換方式。 有關訪問這些選項的說明，請參閱[建立或編輯檔案類型設定](#create-or-edit-file-type-settings)。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。預設值為`pub`。 請勿在擴充功能之前加上句號或之間加上空格。

## AutoCAD設定（僅限Windows）{#autocad-settings-windows-only}

這些選項決定了AutoCAD檔案的轉換方式。 有關訪問這些選項的說明，請參閱[建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。預設值為`dwg`。 請勿在擴充功能之前加上句號或之間加上空格。

**[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。預設會選取此選項。

**[!UICONTROL 將書籤新增至Adobe PDF]**:將標題轉換為書籤。

**[!UICONTROL 在Adobe PDF中一律平面化圖層]**:拼合所有AutoCAD層。

**[!UICONTROL 在Adobe Acrobat中檢視時開啟「圖層」窗格]**:在Acrobat中開啟PDF時顯示圖層結構。

**[!UICONTROL 轉換所有版面]**:包括PDF中的所有佈局。

**[!UICONTROL 將模型空間轉換為3D]**:選中後，模型空間佈局將轉換為PDF中的3D注釋。

**[!UICONTROL 新增連結至Adobe PDF]**:如果選取，會保留所有連結。

**[!UICONTROL 將來源檔案附加至Adobe PDF]**:將源檔案作為附件添加到PDF檔案中。

**[!UICONTROL 建立PDF/A-1b相容檔案]**:強制使用PDF/A-1b Adobe PDF設定。

**[!UICONTROL 轉換所有圖層]**:預設情況下，PDF生成器僅將AutoCAD檔案的預設層轉換為PDF，而不是檔案內的所有層。選擇此選項可轉換檔案的所有圖層。

**[!UICONTROL 內嵌縮放資訊]**:保留繪圖比例資訊。

**[!UICONTROL 轉換當前佈局]**:僅包括PDF中的當前佈局。

**[!UICONTROL 要轉換的AutoCAD佈局清單]**:AutoCAD繪圖可以具有多個佈局。當此框為空時，AutoCAD繪圖中的所有佈局都包含在生成的PDF文檔中。 要選擇性地轉換佈局的子集，請提供佈局名稱的逗號分隔清單。

## OpenOffice設定{#openoffice-settings}

這些選項決定了如何轉換OpenOffice檔案。 有關訪問這些選項的說明，請參閱[建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**嘗試將PDFMaker作為備援轉換器**:當選擇此選項，且使用OpenOffice的轉換失敗或達到指定的超時限制時，PDF生成器將嘗試使用PDFMaker進行轉換。如果使用PDFMaker的轉換失敗或達到指定的逾時限制，則會將例外寫入日誌檔案。

**副檔名**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。預設值為`odt,odp,ods,odg,odf,sxw,sxi,sxd`。 請勿在擴充功能之前加上句號或之間加上空格。

**範圍**:轉換所有頁面，或指定特定頁面或頁面範圍。如果未定義頁面範圍，則會轉換所有頁面。 若要匯出一系列頁面，請使用3-6格式。 若要匯出單頁，請使用7;9;11格式。 您可以使用3-6;8;10;12等格式，匯出頁面範圍和單頁的組合。

**頁面方向**:僅對於純文字檔案檔案，請為轉換的PDF文檔選擇直向或橫向。

**影像**:配置影像的轉換方式。含有內嵌預覽的EPS影像只會匯出為預覽。 未嵌入預覽的EPS影像會導出為空佔位符。 通過無損壓縮影像，保留所有像素。 由於影像的JPEG壓縮和高質量級別，幾乎所有像素都被保留。 在低品質層級中，有些像素會遺失，並引入偽影，但檔案大小會降低。

**一般**:啟用將標籤的PDF轉換或將Writer和FormCalc文檔注釋、Impress幻燈片轉換效果或空白頁導出為PDF的選項。匯出標籤時，檔案大小可能會大幅增加。 有些匯出的標籤是目錄、超連結和控制項。

您也可以指定表單的提交方式。 選項有XML、FDF、PDF或HTML。 此設定會覆寫您在檔案中設定的控制項URL屬性。 只能為PDF文檔選擇一個通用設定：

* PDF（發送整個文檔）
* FDF（傳送控制內容）
* HTML
* XML

**標籤的PDF**:允許從OpenOffice文檔建立帶標籤的PDF。標籤的PDF包含有關文檔內容結構的資訊。 這對於在具有不同螢幕的設備上顯示文檔以及使用螢幕閱讀器軟體時都很有幫助。 它還幫助輔助工具軟體對PDF文檔執行各種有用的操作，例如朗讀PDF文檔的內容。

**匯出附註**:將OpenOffice文檔中的注釋轉換為生成的PDF文檔中的注釋。

**使用轉變效果**:將OpenOffice演示文稿中的幻燈片轉換效果轉換為相應的PDF轉換效果。

**以格式提交Forms**:建立PDF表單，該表單可由PDF文檔的用戶填寫和打印。

**導出自動插入的空白頁**:選取此選項時，自動插入的空白頁面會包含在產生的PDF檔案中。如果要雙面打印PDF文檔，則此功能非常有用。 例如，可以配置書籍，使章節的第一頁始於奇數頁。 如果上一章的結尾是奇數頁，OpenOffice會插入一個空的偶數頁。 此選項可控制是否將該偶數編號的頁面包含在產生的PDF中。

## 其他應用程式設定（僅限Windows）{#other-applications-settings-windows-only}

無法通過管理控制台更改其他應用程式的設定；它們會顯示所支援檔案類型的副檔名。 有關訪問這些設定的說明，請參閱[建立或編輯檔案類型設定](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html)。

* Corel WordPerfect:`wpd`
* AdobePageMaker:`pmd, pm6, p65, pm`
* Adobe FrameMaker:`fm`
* Adobe Photoshop: `psd`

可能需要自訂對這些檔案類型的支援。 如需詳細資訊，請參閱[使用AEM表單寫程式](https://www.adobe.com/go/learn_aemforms_programming_62)中的「新增對其他原生檔案格式的支援」。

有關配置PDFG網路打印機的幫助，請參閱[設定PDFG網路打印機（僅Windows）](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md)。
