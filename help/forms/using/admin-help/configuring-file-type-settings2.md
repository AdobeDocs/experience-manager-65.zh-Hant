---
title: 配置檔案類型設定
seo-title: Configuring file type settings
description: 了解如何配置檔案類型設定。
seo-description: Learn how to configure file type settings.
uuid: d01f430b-9637-4a5f-b3a7-d5ef3e5ecbc5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: adbe8416-c8d7-4581-940b-df62eadf0e26
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6167'
ht-degree: 0%

---


# 配置檔案類型設定 {#configuring-file-type-settings}

在「PDF產生器」中，您可以為支援的檔案類型設定應用程式設定。 在Windows上，您可以為每個支援的檔案類型設定應用程式設定。 在UNIX和Linux上，可以為HTML到PDF和OpenOffice設定應用程式設定。

在「檔案類型設定」頁上，您可以執行以下任務：

* [建立或編輯檔案類型設定](#create-or-edit-file-type-settings)
* 指定預設使用的檔案類型設定(請參閱 [匯入和匯出PDF產生器組態檔](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html))
* [變更預設設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#change-the-default-settings)
* [啟用PDF/A支援](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [刪除檔案類型設定](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>檔案類型設定不適用於後援轉換器，例如Acrobat，以HTML轉換至PDF、Microsoft PowerPoint、Microsoft Word和Microsoft Excel。

## 建立或編輯檔案類型設定 {#create-or-edit-file-type-settings}

建立或編輯檔案類型設定，以指定應用程式如何處理支援的檔案類型轉換。 在Windows上，您可以為每個支援的檔案類型設定應用程式設定。 在UNIX和Linux上，可以為HTML到PDF和OpenOffice設定應用程式設定。

1. 在管理控制台中，按一下 **[!UICONTROL 服務]** > **[!UICONTROL PDF產生器]** > **[!UICONTROL 檔案類型設定]**.
1. 按一下「新增」或按一下設定的名稱。
1. 在「檔案名副檔名」框中，鍵入為此應用程式接受的檔案類型的檔案名副檔名（以逗號分隔）。 請勿包含擴充功能之前的句號或之間的空格。 預設為 `bmp,gif,jpeg,jpg,tif,tiff,png`。
1. （可選）要在圖形或影像中使用文本的光學代碼識別(OCR)，請選擇「使用OCR」並設定以下選項：

**主要OCR語言：** 用於識別字元的OCR引擎語言。 預設為英文（美國）。

**PDF輸出樣式：** 選擇「可搜索影像」，在前景中具有頁面的點陣圖影像，並在下方的不可見圖層上具有掃描的文本。 頁面外觀不會變更，但文字可供選取及讀取。 選擇「格式化文本和圖形」(Formatted Text &amp; Graphics)，使用已識別的文本、字型、圖片和其他圖形元素重構原始頁面。 預設為可搜尋影像（完全）。

**下載影像：** 減少彩色、灰度和單色影像中的像素數。 完成OCR後，會執行掃描影像的下採樣。 預設值為最低(600 dpi)。 如果您將PDF輸出樣式設為「可搜尋影像」（完全），則此選項無法使用。

1. 填妥以下小節中的必要資訊：

   [匯入和匯出PDF產生器組態檔](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

[Adobe PDF匯出設定（僅限Windows）](#adobe-pdf-export-settings-windows-only)

[HTML對PDF設定](#html-to-pdf-settings)

[Flash影片以PDF設定](#flash-videos-to-pdf-settings)

[XPS到PDF設定](#xps-to-pdf-settings)

[PDF優化程式設定](#pdf-optimizer-settings)

[Microsoft Excel設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-excel-settings-windows-only)

[Microsoft PowerPoint設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-powerpoint-settings-windows-only)

[Microsoft專案設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-project-settings-windows-only)

[Microsoft Word設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-word-settings-windows-only)

[Microsoft Visio設定（僅限Windows）](#visio)

[Microsoft Publisher設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-publisher-settings-windows-only)

[AutoCAD設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#autocad-settings-windows-only)

[OpenOffice設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#openoffice-settings)

[其他應用程式的設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#other-applications-settings-windows-only)

   若要前往其他區段，請按一下其網頁上的連結，或使用**[!UICONTROL 下一個]**或 **[!UICONTROL 上一個]** 按鈕。

1. 完成所有區段後，按一下 **[!UICONTROL 儲存]** 或 **[!UICONTROL 另存新檔]** 並提供設定的名稱。

可自訂各種檔案類型的支援。 (請參閱「 [新增對其他原生檔案格式的支援](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)在 [使用AEM表單進行程式設計](https://www.adobe.com/go/learn_lc_programming_11).)

## 變更預設設定 {#change-the-default-settings}

您可以變更套用至新建立來源之Adobe PDF設定、安全設定及檔案類型設定的預設值。 更改預設值不會影響現有源的設定。

1. 在管理控制台中，按一下 **[!UICONTROL 服務>PDF產生器]**.
1. 在 **[!UICONTROL Adobe PDF設定]**, **[!UICONTROL 檔案類型設定]**，或 **[!UICONTROL 安全設定]** 頁面，按一下 **[!UICONTROL 設定預設設定]**.
1. 選取您偏好的預設設定。 「設定預設設定」頁面提供下列一或多個設定：

   **[!UICONTROL Adobe PDF設定]**:原始預設值為Standard(Acrobat 6)。

   **[!UICONTROL 安全設定]**:原始預設值為無安全性(Acrobat 5)。

   **[!UICONTROL 檔案類型設定]**:原始預設值為「標準」。

1. 按一下「**[!UICONTROL 儲存]**」。

## 刪除檔案類型設定 {#delete-a-file-type-setting}

您可以刪除不再使用的檔案類型設定。

1. 在管理控制台中，按一下 **[!UICONTROL 服務>PDF生成器>檔案類型設定]**.
1. 選取要刪除之設定旁的核取方塊。 您可以選擇多個源。 PDF產生器一律會包含旁邊沒有核取方塊的設定，且無法刪除。
1. 按一下 **[!UICONTROL 刪除]** 在「刪除確認」頁面上，按一下 **[!UICONTROL 刪除]**.

## 影像到PDF設定 {#image-to-pdf-settings}

下列選項決定如何將影像檔案轉換為PDF。 如需存取這些設定的相關指示，請參閱 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**副檔名：** 可轉換的副檔名清單（以逗號分隔）。

**嘗試回退轉換器：** PDF產生器可使用Java™或Acrobat將影像檔案轉換為PDF。 選取此選項，當轉換失敗或達到指定的逾時限制時，PDF產生器會使用替代方法來嘗試轉換。 如果替代方法失敗或達到指定的逾時限制，則會將例外寫入日誌檔案。

>[!NOTE]
>
>JPEG2000檔案只能使用Acrobat進行轉換。

**使用OCR:** 指定是否將OCR（光學字元識別）應用到PDF。 OCR軟體允許您搜索、更正和複製PDF中的文本。

***附註&#x200B;**:只有Microsoft Windows才支援OCRPDF(可搜尋PDF)功能。*

**主要OCR語言：** 指定OCR引擎用於標識字元的語言。

**PDF輸出樣式：** 決定要產生的PDF類型。 所有格式都會將OCR、字型和頁面識別應用於文本影像，並將它們轉換為普通文本。

**可搜索影像：** 確保文字可供搜尋和選取。 此選項可保留原始影像，視需要對其進行描述，並在其上放置隱藏的文本層。 「縮減取樣影像」選項可決定影像是否縮減取樣以及縮減取樣的程度。

**可搜索影像（完全）:** 確保文字可供搜尋和選取。 此選項可保留原始影像，並將不可見的文本層置於其上。 建議用於要求原始影像保真度最高的情況。

**ClearScan:** 合成與原始字型接近的新類型3字型，並使用低解析度副本保留頁面背景。

**下載影像：** 在OCR完成後，減少彩色、灰度和單色影像的像素數。 選擇要應用的縮減取樣程度。 編號較高的選項的縮減取樣較少，這會產生較高解析度的PDF。

## Adobe PDF匯出設定（僅限Windows） {#adobe-pdf-export-settings-windows-only}

「Adobe PDF匯出設定」區段中的「匯出檔案類型」設定，用於將PDF檔案轉換為其他格式。 預設為HTML4.01，包含階層式樣式表(CSS)1.0(*.htm、*.html)。

有關訪問此設定的說明，請參閱 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## HTML對PDF設定 {#html-to-pdf-settings}

下列選項決定如何將HTML檔案轉換為PDF。 如需存取這些選項的指示，請參閱 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**嘗試回退轉換器：** PDF產生器可使用Java™或Acrobat，將HTML檔案轉換為PDF。 選取此選項，當轉換失敗或達到指定的逾時限制時，PDF產生器會使用替代方法來嘗試轉換。 如果替代方法失敗或達到指定的逾時限制，則會將例外寫入日誌檔案。

**預設編碼：** 從作業系統和字母的功能表設定檔案文字的輸入編碼。 僅當HTML源檔案未指定編碼類型時，才使用預設編碼選項中顯示的選項。

**強制選定編碼：** 忽略在HTML源檔案中指定的任何編碼，並使用預設編碼選項中顯示的選項。

### 尖峰設定 {#spidering-settings}

*窺視* 掃描網頁以查找指向其他網頁的連結。 遇到到其他網頁的連結時，將提取目標頁面並包含在所生成的PDF文檔中。 啟用以下選項可設定要提取並轉換為PDF的級別數：

**僅獲取X級：** 從基礎頁面URL編目並將頁面轉換至指定層級的深度。 值1隻會轉換提供的URL。

**取得整個網站：** 從提供的URL開始轉換整個網站。

**保持同一路徑：** 任何指向與基本URL不在相同相對路徑上的頁面的連結，在尖峰期間都不會轉換。

**保持在同一伺服器上：** 在尖峰期間，指向不同伺服器上頁面的任何連結都不會轉換。 只會轉換指向與指定URL相同之伺服器的連結。

### 頁面轉換設定 {#page-conversion-settings}

啟用這些選項可指定轉換HTML頁面的方式。 根據頁面大小，寬度、高度和邊界值會相應調整。

**頁面大小：** 選擇「自訂」並指定寬度和高度，或選取預先定義的尺寸。

**方向：** 為轉換的PDF文檔選擇直向或橫向。

**邊距：** 指定生成的PDF文檔中的邊距（頂部、底部、左側和右側）。

**新增書籤至PDF:** 將書籤添加到PDF文檔。

**啟用標籤PDF:** 在PDF檔案中嵌入標籤。

**設定初始視圖設定：** 用於配置文檔選項、窗口選項和用戶介面選項。 這些設定會決定內容最初的顯示方式。

### 文檔選項 {#document-options}

啟用這些選項可指定如何顯示內容、如何顯示PDF文檔中的頁面，以及如何指定放大級別：

**顯示：** 選擇開啟PDF文檔時要在Acrobat中開啟的窗格。

**頁面配置：** 為PDF文檔選擇頁面佈局類型。

**放大：** 為PDF文檔的初始視圖選擇預設的放大率，或選擇自定義值。 選擇預設設定表示將使用預設的Acrobat放大率。

**開啟至頁碼：** 指定PDF開啟的頁碼。

### 視窗選項 {#window-options}

啟用這些選項可指定窗口的大小和顯示方式。

**將窗口調整為初始頁：** 將Acrobat視窗調整為初始頁面的大小。

**螢幕上的中心窗口：** 開啟螢幕中央的視窗。

**以全螢幕模式開啟：** 以全螢幕模式開啟視窗。

**顯示：** 在窗口中顯示文檔標題或檔案名。

### 使用者介面選項 {#user-interface-options}

啟用以下選項以指定窗口外觀：

**隱藏菜單欄：** 隱藏PDF文檔中的菜單欄。

**隱藏工具欄：** 隱藏PDF文檔中的工具欄。

**隱藏窗口控制項：** 隱藏PDF文檔中的窗口控制項。

## Flash影片以PDF設定 {#flash-videos-to-pdf-settings}

PDF產生器支援提交視訊以進行AdobeFlash(SWF或FLV檔案)，以及建立PDF檔案並內嵌視訊以進行AdobeFlash。 此轉換不需要在表單伺服器上安裝AdobeFlash Player。 如需存取此選項的指示，請參閱 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**副檔名：** 可轉換的副檔名清單（以逗號分隔）。

## XPS到PDF設定 {#xps-to-pdf-settings}

XML紙張規範(XPS)在Windows打印機中使用。 此格式為Microsoft格式，可從任何Microsoft Office應用程式中建立。 AEM forms提供轉換XPS檔案的PDF。

**副檔名：** 可轉換的所有XPS副檔名的逗號分隔清單。 目前有一種格式：.xps。

## PDF優化程式設定 {#pdf-optimizer-settings}

PDF產生器支援縮減PDF檔案大小的功能。 使用所有這些設定還是僅使用一些設定取決於您要如何使用檔案以及檔案必須具有的基本屬性。 在大多數情況下，預設設定都是最有效率的：通過刪除嵌入的字型、壓縮影像以及從不再需要的檔案中刪除項來節省空間。

>[!NOTE]
>
>優化數字簽名的文檔會刪除並使數字簽名失效。

有關訪問此設定的說明，請參閱 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**目標PDF版本：** 指定與PDF相容的Acrobat版本。

### 字型 {#fonts}

1. 選擇 **字型。**
1. 選取下列其中一個選項：

   **取消嵌入所有字型：** 將所有嵌入字型解除嵌入。

   **不要取消嵌入任何字型：** 不會取消嵌入任何字型。

   **取消嵌入某些字型：** 僅嵌入指定的字型。 請按照下列步驟指定要取消嵌入的字型：

   * 如有必要，請從 **字型源** 下拉式功能表。 此下拉菜單列出了在 **首頁>設定>核心繫統>核心組態**.
   * 從 **可用字型** 清單和按一下 **新增**. 這些字型會新增至 **要取消嵌入的字型** 清單。
   * 如果要取消嵌入表單伺服器上不存在的字型，請在 **為取消嵌入添加字型** 框。 按一下&#x200B;**「新增」**。

   >[!NOTE]
   >
   >*如果要取消嵌入子集嵌入文檔中的某些字型，請在字型名前加上+號。 例如，「+Helvetica」。*

1. 如果只要嵌入嵌入字型的在用子集，請選擇 **對所有嵌入字型進行子集**.

   >[!NOTE]
   >
   >*如果您搭配使用此選項&#x200B;**取消嵌入某些字型**,**為取消嵌入添加字型**清單仍完全未嵌入。*

   >[!NOTE]
   >
   >*字型子設定是僅嵌入部分字型的技術。 字型子集僅包含文檔中使用的字元。*

### 透明度 {#transparency}

如果PDF文檔包含包含透明度的圖稿，則可以使用PDF優化程式設定來平面化透明度並減小檔案大小。

>[!NOTE]
>
>如果選取Acrobat 4.0和更新版本作為TargetPDF版本，則所有透明對象都會平面化。 對於其他TargetPDF版本，支援透明度，並且您可以配置透明度設定。

選擇 **透明度** 配置透明度設定，同時優化PDF文檔。

**透明度** 指定要保留的向量資訊量。 較高的設定會保留更多向量對象，而較低的設定會柵格化更多向量對象；中間設定會保留向量形式的簡單區域，並柵格化複雜區域。 選擇最低設定以柵格化所有圖稿。

>[!NOTE]
>
>發生的光柵化量取決於頁面的複雜性和重疊對象的類型。

**線條圖和文字** 將所有對象（包括影像、向量圖稿、文本和漸變）柵格化到的解析度。 支援的值為1像素/英吋(ppi)至9600 ppi。

>[!NOTE]
>
>線條圖和文字解析度一般應設為600-1200 ppi，以提供高品質的光柵化效果，尤其是襯線或小點大小的類型。

**漸層和網格** 柵格化漸變和網格的解析度。 支援的值為1 ppi至1200 ppi。

>[!NOTE]
>
>漸變和網格解析度通常應設定為150-300 ppi，因為漸變、陰影和羽化的質量不會隨著解析度的提高而提高，但打印時間和檔案大小會增加。

**將所有文本轉換為輪廓** 將所有類型對象（點類型、區域類型和路徑類型）轉換為輪廓並丟棄包含透明度的頁面上的所有類型字形資訊。 此選項可確保拼合期間文字的寬度保持一致。 請注意，啟用此選項將使小字型在Acrobat中查看時或在低解析度的台式打印機上打印時看起來稍微粗一些。 它不會影響打印在高解析度打印機或影像集上的類型的質量。

**將所有描邊轉換為輪廓** 將包含透明度的頁面上的所有筆畫轉換為簡單的填充路徑。 此選項可確保拼合期間筆畫的寬度保持一致。 請注意，啟用此選項會導致薄筆划顯示為稍粗，並可能降低拼合效能。

**剪輯複雜區域** 確保向量圖稿和柵格化圖稿之間的邊界沿對象路徑下降。 此選項可減少記錄部分時產生的拼接成品

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>某些打印驅動程式對光柵和向量圖的處理方式不同，有時會導致顏色拼接。 通過禁用某些打印驅動程式特定的顏色管理設定，您可以最大限度地減少拼接問題。 這些設定因每台打印機而異，因此有關詳細資訊，請參閱打印機隨附的文檔。

保留疊印：將透明圖稿的顏色與背景顏色混合，以建立疊印效果。

下表顯示了常見的打印機類型及其以dpi測量的解析度、以每英吋行(lpi)測量的預設螢幕規則，以及以每英吋像素(ppi)測量的影像的重採樣解析度。 例如，如果要打印到600 dpi雷射打印機，則輸入170作為要重新取樣影像的解析度。

**影像** 選擇「影像」以指定顏色、灰度和單色影像的壓縮和重採樣選項。 您可能希望嘗試使用這些選項來在檔案大小和影像質量之間找到適當的平衡。彩色和灰度影像的解析度設定應是打印檔案的線螢幕的1.5到2倍。 單色影像的解析度應與輸出設備相同，但請注意，以高於1500 dpi的解析度保存單色影像會增加檔案大小，而不會顯著改善影像質量。 將被放大的影像，如地圖，可能需要更高的解析度。

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

#### 放棄對象 {#discard-objects}

* 選擇 **放棄對象** 指定要從PDF中移除的對象，並優化CAD繪圖中的曲線。
* **放棄所有表單提交、導入和重置操作**:停用與提交或匯入表單資料相關的所有動作，並重設表單欄位。 此選項會保留動作連結到的表單物件。
* **捨棄所有JavaScript動作**:從PDF中移除任何使用JavaScript的動作。
* **放棄嵌入的頁縮圖**:移除內嵌的頁面縮圖。 此選項對於大型文檔非常有用，在按一下「頁面」按鈕後，可能需要花很長時間繪製頁面縮略圖。
* **將平滑線轉換為曲線**:減少用於在CAD繪圖中建立曲線的控制點數，這將導致較小的PDF檔案和更快的螢幕繪製。
* **放棄嵌入的打印設定**:從文檔中刪除嵌入的打印設定，如頁面縮放和雙工模式。
* **捨棄書籤**:從文檔中刪除所有書籤。
* **平面化表單欄位**:使表單欄位無法使用，而外觀不會變更。 表單資料會與頁面合併，成為頁面內容。
* **捨棄所有替代影像**:移除除了用於螢幕檢視的版本以外的所有影像版本。 某些PDF包含多個版本的相同影像，以用於不同用途，例如低解析度的螢幕檢視和高解析度列印。
* **放棄文檔標籤**:從文檔中刪除標籤，這也會刪除文本的輔助功能和重排功能。
* **偵測及合併影像片段**:查找碎片為薄切片並嘗試將切片合併為單個影像或蒙版的影像或蒙版。
* **放棄嵌入的搜索索引**:刪除嵌入的搜索索引，從而減小檔案大小。

#### 放棄用戶資料 {#discard-user-data}

選擇 **放棄用戶資料** 移除您不想分發或與其他使用者共用的任何個人資訊。

* **捨棄所有注釋、Forms和多媒體**:從PDF中刪除所有注釋、表單、表單欄位和多媒體。
* **放棄所有對象資料**:從PDF中刪除所有對象。
* **捨棄外部交叉引用**:刪除指向其他文檔的連結。 跳至PDF內其他位置的連結不會移除。
* **捨棄隱藏圖層內容並平面化可見圖層**:減小檔案大小。 最佳化的檔案看起來像原始PDF，但不包含圖層資訊。
* **放棄文檔資訊和元資料**:刪除文檔資訊字典和所有元資料流中的資訊。 (使用「另存新檔」命令，將中繼資料串流還原為PDF的復本。)
* **放棄檔案附件**:刪除所有檔案附件，包括作為注釋添加到PDF的附件。 (PDF優化程式不優化附加的檔案。)
* **放棄其他應用程式的專用資料**:從PDF文檔中刪除僅對建立文檔的應用程式有用的資訊。 此設定不會影響PDF的功能，但會降低檔案大小。

### 清理 {#clean-up}

選擇 **清理** 從文檔中刪除不必要的項。
這些項目包括對您預定使用文檔而言過時或不必要的元素。 移除某些元素可能會嚴重影響PDF的功能。 依預設，僅選取不影響功能的元素。 如果您不確定移除其他選項的可能影響，請使用預設選取項目。

**壓縮**

從下拉式選單中選取下列其中一個「完全壓縮」選項：

* 壓縮整個檔案
* 壓縮文檔結構
* 移除壓縮
* 保持壓縮不變

**使用Flate對未編碼的流進行編碼**:將全部壓縮套用至所有未編碼的資料流。

**捨棄無效書籤**:刪除指向文檔中要刪除的頁面的書籤。

**放棄未引用的命名目標**:從PDF文檔中刪除未在內部引用的已命名目標。 此選項不會檢查其他PDF檔案或網站的連結。

**最佳化PDF以快速進行Web檢視**:重新建構PDF檔案，以便從Web伺服器進行一次性頁面下載（位元組服務）。

**在使用LZW編碼的資料流中，請改用Flate**:對使用LZW編碼的所有內容流和影像應用全壓縮。

**放棄無效連結**:移除跳至無效目的地的連結。

**最佳化頁面內容**:將所有行尾字元轉換為空格字元，這可改善Flate壓縮。

## Microsoft Excel設定（僅限Windows） {#microsoft-excel-settings-windows-only}

這些選項決定了轉換Microsoft Excel檔案的方式。 如需存取這些選項的指示，請參閱 [建立或編輯檔案類型設定](#create-or-edit-file-type-settings).

**嘗試使用OpenOffice作為備援轉換器**:當選取此選項，且使用Microsoft Excel的轉換失敗或達到指定的逾時限制時，PDF產生器會使用OpenOffice來嘗試轉換。 如果使用OpenOffice的轉換失敗或達到指定的超時限制，則會將異常寫入日誌檔案。

**副檔名**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。 預設為 `xls,xlsx`。請勿在擴充功能之前加上句號或之間加上空格。

**建立PDF/A-1a相容檔案**:強制使用PDF/A-1b:2005RGBAdobe PDF設定。

**新增書籤至Adobe PDF**:將Excel工作表名稱轉換為書籤。 預設會選取此選項。

**調整工作表以符合單一頁面**:縮小文字大小，以符合單一頁面上的工作表大小。

**轉換整個活頁簿**:轉換Excel檔案中的所有工作表。 如果未選取此選項，則只會轉換目前的頁面。

**自動運行宏**:在轉換文檔之前，運行Excel文檔中的任何宏（如插入當前時間的宏）。

**轉換文檔資訊**:根據源檔案中的文檔資訊添加PDF文檔屬性。 這包括檔案標題、作者、主旨和關鍵字等資訊。

**新增連結至Adobe PDF**:將源檔案中的超連結轉換為PDF文檔中的超連結。

**將源檔案附加到Adobe PDF**:選取此選項時，原始Excel試算表會插入為所產生PDF檔案中的附件。

**啟用協助工具，並使用標籤的Adobe PDF啟用Reflow**:將標籤內嵌在PDF檔案中，以啟用協助工具和重排。

**要載入的Excel增益集清單**:依預設（基於安全考量），當Excel檔案轉換為PDF時，不會執行Excel增益集。 若要允許在轉換期間執行某些Excel增益集，請提供增益集名稱的逗號分隔清單。

**要轉換的工作表清單**:當此方塊為空時，Excel試算表中的所有工作表都會納入產生的PDF。 要選擇性地轉換工作表的子集，請提供以逗號分隔的工作表名稱清單。

## Microsoft PowerPoint設定（僅限Windows） {#microsoft-powerpoint-settings-windows-only}

這些選項決定了如何轉換Microsoft PowerPoint檔案。 如需存取這些選項的指示，請參閱 [建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings).

**[!UICONTROL 嘗試使用OpenOffice作為備援轉換器]**:當選中此選項且使用Microsoft PowerPoint的轉換失敗或達到指定的逾時限制時，PDF生成器將嘗試使用OpenOffice進行轉換。 如果使用OpenOffice的轉換失敗或達到指定的超時限制，則會將異常寫入日誌檔案。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。 預設值為ppt,pptx。 請勿在擴充功能之前加上句號或之間加上空格。

**[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。

**[!UICONTROL 新增書籤至Adobe PDF]**:將PowerPoint標題轉換為書籤。 預設會選取此選項。

**[!UICONTROL 將源檔案附加到Adobe PDF]**:將源檔案作為附件添加到PDF檔案中。 預設會取消選取此選項。

**[!UICONTROL 啟用協助工具，並使用標籤的Adobe PDF啟用Reflow]**:將標籤內嵌至PDF檔案。 預設會取消選取此選項。

**[!UICONTROL 將多媒體轉換為PDF多媒體]**:盡可能將多媒體轉換為PDF多媒體。 預設會選取此選項。

**[!UICONTROL 轉換揚聲器注釋]**:將揚聲器注釋轉換為PDF。

**[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行PowerPoint文檔中的任何宏（如插入當前時間的宏）。

**[!UICONTROL 基於PowerPoint打印機設定的PDF佈局]**:使用PowerPoint打印機設定來佈局PDF文檔。

**[!UICONTROL 新增連結至Adobe PDF]**:轉換檔案時保留現有連結。 連結的外觀基本不變。 只有選取了「啟用協助工具」選項，才能建立連結。 預設會取消選取此選項。

**[!UICONTROL 在Adobe PDF中儲存投影片轉變]**:轉換幻燈片過渡。 預設會選取此選項。

**[!UICONTROL 在Adobe PDF中儲存動畫]**:將轉換的動畫保存在PDF檔案中。

**[!UICONTROL 將隱藏的投影片轉換為PDF頁面]**:轉換隱藏的幻燈片。

**[!UICONTROL 建立PDF/A-1a相容檔案]**:強制使用PDF/A-1b:2005RGBAdobe PDF設定。 生成PDF檔案時，不會轉換一些PowerPoint功能。 如果PowerPoint轉變在Acrobat中沒有等效轉變，則會替換類似的轉變。 如果同一幻燈片中有多個動畫效果，則使用一個效果。 頁面轉變和項目符號調整項目會經過轉換。

## Microsoft專案設定（僅限Windows） {#microsoft-project-settings-windows-only}

這些選項決定如何轉換Microsoft專案檔案。 如需存取這些選項的指示，請參閱 [建立或編輯檔案類型設定](#create-or-edit-file-type-settings).

1. **[!UICONTROL 副檔名：]** 指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。 預設為 `mpp`。請勿在擴充功能之前加上句號或之間加上空格。

1. **[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。
1. **[!UICONTROL 將源檔案附加到Adobe PDF]**:將源檔案作為附件添加到PDF檔案中。
1. **[!UICONTROL 建立PDF/A-1a相容檔案]**:強制使用PDF/A-1b:2005RGBAdobe PDF設定。
1. **[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行Microsoft項目文檔中的任何宏（如插入當前時間的宏）。

## Microsoft Word設定（僅限Windows） {#microsoft-word-settings-windows-only}

這些選項決定如何轉換Microsoft Word檔案。 如需存取這些選項的指示，請參閱 [建立或編輯檔案類型設定](#create-or-edit-file-type-settings).

**[!UICONTROL 嘗試使用OpenOffice作為備援轉換器]**:當選取此選項，且使用Microsoft Word的轉換失敗或達到指定的逾時限制時，PDF產生器會使用OpenOffice來嘗試轉換。 如果使用OpenOffice的轉換失敗或達到指定的超時限制，則會將異常寫入日誌檔案。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。 預設為 `doc,docx,rtf,txt`。請勿在擴充功能之前加上句號或之間加上空格。

**[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。

**[!UICONTROL 新增書籤至Adobe PDF]**:將標題轉換為書籤。 預設會選取此選項。

**[!UICONTROL 將源檔案附加到Adobe PDF]**:將源檔案作為附件添加到PDF檔案中。

**[!UICONTROL 將交叉引用和目錄轉換為連結]**:將所有交叉引用和目錄條目轉換為連結。 預設會選取此選項。

**[!UICONTROL 啟用協助工具，並使用標籤的Adobe PDF啟用Reflow]**:將標籤內嵌至PDF檔案。 預設會選取此選項。

**[!UICONTROL 建立PDF/A-1a相容檔案]**:若已選取，會強制使用PDF/A-1b:2005RGBAdobe PDF設定。

**[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行Word文檔中的任何宏（如插入當前時間的宏）。

**[!UICONTROL 在Adobe PDF中保留文檔標籤]**:將Word文檔中的標籤轉換為PDF檔案中的注釋。

**[!UICONTROL 新增連結至Adobe PDF]**:將源檔案中的超連結轉換為PDF文檔中的超連結。

**[!UICONTROL 轉換腳注和章節附註連結]**:建立從腳注和注釋引用到PDF文檔中注釋的連結。

**[!UICONTROL 在Adobe PDF中將顯示的註解轉換為附註]**:將Word文檔中的注釋轉換為PDF文檔中的文本注釋。

**[!UICONTROL 啟用進階標籤]**:新增進階標籤以增強協助工具。

**[!UICONTROL 將所有樣式轉換為書籤]**:將Word文檔中的所有樣式轉換為PDF文檔中的書籤。

**[!UICONTROL 具有層級的樣式]**:指定Word文檔中的哪些樣式將轉換為PDF文檔中的書籤。 也會指定書籤的層級。 若要使用此功能，請取消選取 **[!UICONTROL 將所有樣式轉換為書籤]** ，並以下列格式指定樣式名稱：

styleName1=level1[,styleName2=level2...]

如果Microsoft Word樣式名稱包含逗號(,)或等號(=)，請在特殊字元前面加上逸出字元(&quot;\_)。 例如，指定名為&quot;Heading, 1&quot;的樣式作為Heading\, 1。

## Microsoft Visio設定（僅限Windows） {#visio}

**轉換文檔資訊**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。 預設會啟用此選項。

**新增連結至Adobe PDF**:保留所有連結。 預設會選取此選項。

**新增書籤至Adobe PDF**:將標題轉換為書籤。 預設會選取此選項。

**將源檔案附加到Adobe PDF**:將源檔案作為附件添加到PDF檔案中。

**在Adobe PDF中一律平面化圖層**:拼合所有Visio圖層。

**轉換所有頁面**:轉換Visio檔案的所有頁面。

**在Adobe Acrobat中檢視時開啟圖層面板**:如果Visio圖層未平面化，則開啟一個窗口，在該窗口中，可以指定使用Acrobat開啟時保留在PDF檔案中的圖層。 預設會選取此選項。

**建立PDF/A-1b相容檔案**:強制使用Adobe PDF設定PDF/A-1b:2005(RGB)。

**將注釋轉換為Adobe PDF注釋**:將Visio注釋轉換為PDF注釋。

## Microsoft Publisher設定（僅限Windows） {#microsoft-publisher-settings-windows-only}

這些選項決定如何轉換Microsoft Publisher檔案。 如需存取這些選項的指示，請參閱 [建立或編輯檔案類型設定](#create-or-edit-file-type-settings).

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。 預設為 `pub`。請勿在擴充功能之前加上句號或之間加上空格。

## AutoCAD設定（僅限Windows） {#autocad-settings-windows-only}

這些選項決定了AutoCAD檔案的轉換方式。 如需存取這些選項的指示，請參閱 [建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings).

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。 預設為 `dwg`。請勿在擴充功能之前加上句號或之間加上空格。

**[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。

**[!UICONTROL 新增書籤至Adobe PDF]**:將標題轉換為書籤。

**[!UICONTROL 在Adobe PDF中一律平面化圖層]**:拼合所有AutoCAD層。

**[!UICONTROL 在Adobe Acrobat中檢視時開啟圖層窗格]**:在Acrobat中開啟PDF時顯示圖層結構。

**[!UICONTROL 建立PDF/E-1相容檔案]**:建立符合PDF/E-1的檔案。 PDF/E是用於交換工程和技術文檔的ISO標準。 如需PDF/E-1的詳細資訊，請參閱 [Adobe和行業標準](https://www.adobe.com/enterprise/standards/index.html).

**[!UICONTROL 轉換所有佈局]**:包括PDF中的所有佈局。

**[!UICONTROL 將模型空間轉換為3D]**:選中後，模型空間佈局將轉換為PDF中的3D注釋。

**[!UICONTROL 新增連結至Adobe PDF]**:如果選取，會保留所有連結。

**[!UICONTROL 將源檔案附加到Adobe PDF]**:將源檔案作為附件添加到PDF檔案中。

**[!UICONTROL 建立PDF/A-1b相容檔案]**:強制使用PDF/A-1b Adobe PDF設定。

**[!UICONTROL 轉換所有圖層]**:預設情況下，「PDF生成器」(AutoCad)僅將AutoCAD檔案的預設層轉換為PDF，而不是檔案內的所有層。 選擇此選項可轉換檔案的所有圖層。

**[!UICONTROL 內嵌縮放資訊]**:保留繪圖比例資訊。

**[!UICONTROL 轉換當前佈局]**:僅包含PDF中的目前配置。

**[!UICONTROL 要轉換的AutoCAD佈局清單]**:AutoCAD繪圖可以具有多個佈局。 當此框為空時，AutoCAD繪圖中的所有佈局都包括在生成的PDF文檔中。 要選擇性地轉換佈局的子集，請提供佈局名稱的逗號分隔清單。

## OpenOffice設定 {#openoffice-settings}

這些選項決定了如何轉換OpenOffice檔案。 如需存取這些選項的指示，請參閱 [建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings).

**嘗試將PDFMaker作為後備轉換器**:當選擇此選項，且使用OpenOffice的轉換失敗或達到指定的超時限制時，PDF生成器將嘗試使用PDFMaker進行轉換。 如果使用PDFMaker的轉換失敗或達到指定的逾時限制，則會將例外寫入日誌檔案。

**副檔名**:指定此應用程式接受的檔案類型的副檔名（以逗號分隔）。 預設為 `odt,odp,ods,odg,odf,sxw,sxi,sxd`。請勿在擴充功能之前加上句號或之間加上空格。

**範圍**:轉換所有頁面，或指定特定頁面或頁面範圍。 如果未定義頁面範圍，則會轉換所有頁面。 若要匯出一系列頁面，請使用3-6格式。 若要匯出單頁，請使用7;9;11格式。 您可以使用3-6;8;10;12等格式，匯出頁面範圍和單頁的組合。

**頁面方向**:僅對於純文字檔案檔案，請為轉換的PDF文檔選擇直向或橫向。

**影像**:配置影像的轉換方式。 具有內嵌預覽的EPS影像只會匯出為預覽。 沒有內嵌預覽的EPS影像會匯出為空白預留位置。 通過無損壓縮影像，保留所有像素。 由於影像的JPEG壓縮和高品質等級，幾乎所有像素都會保留。 在低品質層級中，有些像素會遺失，並引入偽影，但檔案大小會降低。

**一般**:啟用將標籤PDF轉換的選項，或將Writer和FormCalc文檔注釋、Impress幻燈片轉換效果或空白頁導出到PDF。 匯出標籤時，檔案大小可能會大幅增加。 有些匯出的標籤是目錄、超連結和控制項。

您也可以指定表單的提交方式。 選項包括XML、FDF、PDF或HTML。 此設定會覆寫您在檔案中設定的控制項URL屬性。 只能為PDF文檔選擇一個通用設定：

* PDF（發送整個文檔）
* FDF（傳送控制內容）
* HTML
* XML

**標籤PDF**:啟用從OpenOffice文檔建立標籤PDF。 標籤的PDF包含有關文檔內容結構的資訊。 這對於在具有不同螢幕的設備上顯示文檔以及使用螢幕閱讀器軟體時都很有幫助。 它還有助於輔助工具軟體對PDF文檔執行各種有用的操作，例如朗讀PDF文檔的內容。

**匯出附註**:將OpenOffice文檔中的注釋轉換為生成的PDF文檔中的注釋。

**使用轉變效果**:將OpenOffice演示文稿中的幻燈片轉換效果轉換為相應的PDF轉換效果。

**以格式提交Forms**:建立PDF表單，該表單可由PDF文檔的用戶填寫和打印。

**導出自動插入的空白頁**:選取此選項時，自動插入的空白頁面將包含在生成的PDF文檔中。 如果要雙面打印PDF文檔，則此選項非常有用。 例如，可以配置書籍，使章節的第一頁始於奇數頁。 如果上一章的結尾是奇數頁，OpenOffice會插入一個空的偶數頁。 此選項會控制是否要將該偶數編號的頁面包含在產生的PDF中。

## 其他應用程式設定（僅限Windows） {#other-applications-settings-windows-only}

無法通過管理控制台更改其他應用程式的設定；它們會顯示所支援檔案類型的副檔名。 如需存取這些設定的相關指示，請參閱 [建立或編輯檔案類型設定](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* AdobePageMaker: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

可能需要自訂對這些檔案類型的支援。 如需詳細資訊，請參閱 [使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_62).

有關配置PDFG網路打印機的幫助，請參見 [設定PDFG網路打印機（僅限Windows）](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
