---
title: 配置檔案類型設定
seo-title: 配置檔案類型設定
description: 瞭解如何設定檔案類型設定。
seo-description: 瞭解如何設定檔案類型設定。
uuid: 58a05500-ffbb-4fa2-8ae1-8ac80ab2d099
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89f4d3cf-eb2e-4d55-8209-16ecbba03792
translation-type: tm+mt
source-git-commit: 01c93d2ef344b1ce36fddd21b634b8fa4e7aebe0

---


# 配置檔案類型設定 {#configuring-file-type-settings}

在PDF產生器中，您可以針對支援的檔案類型設定應用程式設定。 在Windows上，您可以針對每個支援的檔案類型設定應用程式設定。 在UNIX和Linux上，您可以設定HTML轉PDF和OpenOffice的應用程式設定。

在「檔案類型設定」頁上，您可以執行以下任務：

* [建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)
* 指定預設要使用的檔案類型設定(請參 [閱匯入和匯出PDF產生器組態檔](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html))
* [變更預設設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#change-the-default-settings)
* [啟用PDF/A支援](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [刪除檔案類型設定](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>檔案類型設定不適用於備援轉換器，例如Acrobat for HTML轉換為PDF、Microsoft powerPoint、Microsoft word和Microsoft Excel。

## 建立或編輯檔案類型設定 {#create-or-edit-file-type-settings}

建立或編輯檔案類型設定，以指定應用程式如何處理支援的檔案類型轉換。 在Windows上，您可以針對每個支援的檔案類型設定應用程式設定。 在UNIX和Linux上，您可以設定HTML轉PDF和OpenOffice的應用程式設定。

1. 在管理控制台中，按一 **[!UICONTROL 下「服務]** > **[!UICONTROL PDF產生器]** >檔案 **[!UICONTROL 類型設定」]**。
1. 按一下「新增」或按一下設定名稱。
1. 在「副檔名」方塊中，為此應用程式接受的檔案類型輸入副檔名（以逗號分隔）。 請勿在擴充功能之前加入句號或間隔。 預設值為 `bmp,gif,jpeg,jpg,tif,tiff,png`。
1. （可選）若要在圖形或影像中使用文字的光學程式碼識別(OCR)，請選取「使用OCR」並設定下列選項：

**** 主要OCRL語言：OCR引擎用來識別字元的語言。 預設值為英文（美國）。

**** PDF輸出樣式：選取「可搜尋的影像」，將頁面的點陣圖影像置於前景中，並將掃描的文字置於下方的不可見圖層上。 頁面的外觀不會變更，但文字會變成可選及可讀。 選取「格式化的文字與圖形」，使用已辨識的文字、字型、圖片和其他圖形元素來重建原始頁面。 預設為可搜尋影像（完全）。

**** 縮減影像取樣：減少彩色、灰階和單色影像的像素數。 在OCR完成後，執行掃描影像的縮減取樣。 預設值為「最低」(600 dpi)。 如果您將PDF輸出樣式設為「可搜尋影像」（完全），則此選項不可用。

1. 請填妥下列章節中的必要資訊：

   [匯入和匯出PDF產生器組態檔](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

   [Adobe PDF匯出設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-2)

   [HTML至PDF設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-3)

   [將Flash視訊轉換為PDF設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-9)

   [XPS到PDF設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-10)

   [PDF最佳化程式設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-11)

   [Microsoft excel設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-excel-settings-windows-only)

   [Microsoft powerPoint設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-powerpoint-settings-windows-only)

   [Microsoft project設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-project-settings-windows-only)

   [Microsoft word設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-word-settings-windows-only)

   [Microsoft Visio設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-header-1354428557)

   [Microsoft Publisher設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-publisher-settings-windows-only)

   [AutoCAD設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings1.md#autocad-settings-windows-only)

   [OpenOffice設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#openoffice-settings)

   [其他應用程式的設定（僅限Windows）](#other-applications-settings-windows-only)

   若要前往其他區段，請按一下其網頁上的連結，或使用「下一[!UICONTROL 步]」或「上一 **[!UICONTROL 步]** 」按鈕。

1. 完成所有章節後，按一下「 **[!UICONTROL 儲存]****[!UICONTROL 」或「另存新檔]** 」，並提供設定名稱。

可自訂各種檔案類型的支援。 (請參閱「使 [用AEM表單進行程式設計」中的「新增對其他原生檔案格式的支援](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)」 [](https://www.adobe.com/go/learn_lc_programming_11))。

## 變更預設設定 {#change-the-default-settings}

您可以變更Adobe PDF設定、安全性設定和檔案類型設定的預設值，這些設定都會套用至新建立的來源。 更改預設值不會影響現有源的設定。

1. 在「管理控制台」中，按一 **[!UICONTROL 下「服務> PDF產生器]**」。
1. 在「 **[!UICONTROL Adobe PDF設定]**」、「檔案類型設定 **[!UICONTROL 」或「安全性設定」頁面上，按一]**********&#x200B;下「設定預設設定」。
1. 選擇您偏好的預設設定。 「設定預設設定」頁面上提供下列一或多個設定：

   **[!UICONTROL Adobe PDF設定]**:原始預設值為Standard(Acrobat 6)。

   **[!UICONTROL 安全性設定]**:原始預設值為「無安全性」(Acrobat 5)。

   **[!UICONTROL 檔案類型設定]**:原始預設值為「標準」。

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

## 刪除檔案類型設定 {#delete-a-file-type-setting}

您可以刪除不再使用的檔案類型設定。

1. 在管理控制台中，按一 **[!UICONTROL 下「服務> PDF Generator>檔案類型設定」]**。
1. 選中要刪除的設定旁邊的複選框。 您可以選取多個來源。 沒有核取方塊的設定一律會隨附於PDF產生器中，且無法刪除。
1. 按一下 **[!UICONTROL 刪除]** ，然後在「刪除確認」頁上按一下 **[!UICONTROL 刪除]**。

## 影像至PDF設定 {#image-to-pdf-settings}

下列選項可決定如何將影像檔案轉換為PDF。 有關訪問這些設定的說明，請參 [閱建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**** 副檔名：以逗號分隔的可轉換副檔名清單。

**** 試用備援轉換器：PDF產生器可使用Java™或Acrobat將影像檔案轉換為PDF。 當選取此選項，而轉換失敗或達到指定的逾時限制時，PDF產生器會使用替代方法來嘗試轉換。 如果替代方法失敗或達到指定的逾時限制，則會將異常寫入日誌檔案。

***注意&#x200B;**:JPEG 2000檔案只能使用Acrobat進行轉換。*

**** 使用OCR:指定是否將OCR（光學字元辨識）套用至PDF。 OCR軟體可讓您搜尋、修正和複製PDF中的文字。

***注意&#x200B;**:OCR PDF（可搜尋的PDF）功能僅在Microsoft windows上受支援。*

**** 主要OCR語言：指定OCR引擎用於識別字元的語言。

**** PDF輸出樣式：決定要產生的PDF類型。 所有格式都會將OCR和字型及頁面識別套用至文字影像，並將它們轉換為一般文字。

**** 可搜尋的影像：確保文字可供搜尋和選取。 這個選項會保留原始影像、視需要設定影像，並在其上放置不可見的文字圖層。 「縮減取樣影像」選項會決定影像是否已縮減取樣，以及縮減取樣的程度。

**** 可搜尋影像（完全）:確保文字可供搜尋和選取。 此選項會保留原始影像，並在其上放置不可見的文字圖層。 建議在需要原始影像最精確的情況下使用。

**** ClearScan:合成與原始字型相近的新Type 3字型，並使用低解析度的副本保留頁面背景。

**** 縮減影像取樣：在OCR完成後，減少彩色、灰階和單色影像的像素數。 選擇要套用的縮減取樣程度。 編號較高的選項可減少縮減取樣，產生解析度較高的PDF。

## Adobe PDF匯出設定（僅限Windows） {#adobe-pdf-export-settings-windows-only}

Adobe PDF匯出設定區段中的「匯出檔案類型」設定可用來將PDF檔案轉換為其他格式。 預設為HTML 4.01，內含階層式樣式表(CSS)1.0(&amp;ast;.htm, &amp;ast;.html)。

有關訪問此設定的說明，請參 [閱建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

## HTML至PDF設定 {#html-to-pdf-settings}

下列選項可決定HTML檔案轉換為PDF的方式。 有關訪問這些選項的說明，請參 [閱建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**** 試用備援轉換器：PDF產生器可使用Java™或Acrobat將HTML檔案轉換為PDF。 當選取此選項，而轉換失敗或達到指定的逾時限制時，PDF產生器會使用替代方法來嘗試轉換。 如果替代方法失敗或達到指定的逾時限制，則會將異常寫入日誌檔案。

**** 預設編碼：從作業系統和字母菜單設定檔案文本的輸入編碼。 只有當HTML來源檔案未指定編碼類型時，才使用「預設編碼」選項中顯示的選取範圍。

**** 強制選擇的編碼：忽略HTML來源檔案中指定的任何編碼，並使用「預設編碼」選項中顯示的選取範圍。

### 色階設定 {#spidering-settings}

*Spidring* 會掃描網頁，以尋找其他網頁的連結。 當遇到到其他網頁的連結時，會擷取目標頁面並包含在產生的PDF檔案中。 啟用這些選項，以設定要擷取並轉換為PDF的層級數：

**** 僅取得X級：從基本頁面URL將頁面編目並轉換至指定層級的深度。 值1隻會轉換提供的URL。

**** 取得整個網站：從提供的URL開始轉換整個網站。

**** 保持同一條路：指向與基本URL不位於相同相對路徑之頁面的任何連結，都不會在尖峰期間轉換。

**** 保持在同一台伺服器上：指向不同伺服器上頁面的任何連結，都不會在串頁期間進行轉換。 只會轉換指向與指定URL相同伺服器的連結。

### 頁面轉換設定 {#page-conversion-settings}

啟用這些選項，以指定HTML頁面的轉換方式。 根據頁面大小，寬度、高度和邊界值會隨之調整。

**** 頁面大小：選擇自訂並指定寬度和高度，或選取預先定義的尺寸。

**** 方向：為轉換的PDF檔案選擇縱向或橫向。

**** 邊界：指定所產生PDF檔案中的邊界（頂端、底部、左側和右側）。

**** 新增書籤至PDF:將書籤新增至PDF檔案。

**** 啟用標籤的PDF:在PDF檔案中內嵌標籤。

**** 設定初始檢視設定：可讓您設定「檔案選項」、「視窗選項」和「使用者介面選項」。 這些設定會決定內容的初始顯示方式。

### 檔案選項 {#document-options}

啟用這些選項，以指定如何顯示內容、如何在PDF檔案中顯示頁面，以及如何指定放大等級：

**** 顯示：選取開啟PDF檔案時要在Acrobat中開啟的窗格。

**** 頁面配置：為PDF文檔選擇頁面佈局類型。

**** 放大比例：選擇PDF檔案初始檢視的預設放大比例，或選擇自訂值。 選擇預設設定表示將使用預設的Acrobat放大比例。

**** 開啟至頁碼：指定PDF開啟至的頁碼。

### 視窗選項 {#window-options}

啟用這些選項以指定視窗的大小和顯示方式。

**** 將視窗調整為初始頁面：將Acrobat視窗調整為初始頁面的大小。

**** 畫面中央視窗：在螢幕中央開啟窗口。

**** 以全螢幕模式開啟：以全螢幕模式開啟視窗。

**** 顯示：在窗口中顯示文檔標題或檔案名。

### 使用者介面選項 {#user-interface-options}

啟用這些選項以指定窗口外觀：

**** 隱藏選單列：隱藏PDF檔案中的選單列。

**** 隱藏工具列：隱藏PDF檔案中的工具列。

**** 隱藏視窗控制項：隱藏PDF檔案中的視窗控制項。

## 將Flash視訊轉換為PDF設定 {#flash-videos-to-pdf-settings}

PDF Generator支援提交Adobe Flash影片（SWF或FLV檔案），並建立內嵌Adobe Flash影片的PDF檔案。 此轉換不需要將Adobe Flash Player安裝在表單伺服器上。 有關訪問此選項的說明，請參 [閱建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**** 副檔名：以逗號分隔的可轉換副檔名清單。

## XPS到PDF設定 {#xps-to-pdf-settings}

XML紙張規格(XPS)在Windows打印機中使用。 此為Microsoft格式，可從任何Microsoft office應用程式建立。 AEM表單提供轉換XPS檔案PDF的功能。

**** 副檔名：以逗號分隔的清單，列出所有可轉換的XPS檔案副檔名。 目前有一種格式：.xps.

## PDF最佳化程式設定 {#pdf-optimizer-settings}

PDF產生器支援減少PDF檔案大小的功能。 您是使用這些設定，還是只使用少數設定，取決於您要如何使用檔案，以及檔案必須具備的基本屬性。 在大多數情況下，預設設定最適合發揮最大效率——移除內嵌字型、壓縮影像，以及移除不再需要的檔案項目，以節省空間。

>[!NOTE]
>
>最佳化數位簽章檔案會移除數位簽章，並使其無效。

有關訪問此設定的說明，請參 [閱建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**** 目標PDF版本：指定PDF相容的Acrobat版本。

### 字型 {#fonts}

1. 選取「 **字型」。**
1. 選擇下列選項之一：

   **** 取消內嵌所有字型：解除內嵌所有內嵌字型。

   **** 請勿取消內嵌任何字型：不取消內嵌任何字型。

   **** 取消內嵌某些字型：僅解除內嵌指定字型。 請依照下列步驟來指定您要取消內嵌的字型：

   * 如有必要，請從「字型來源」下拉式選單 **中選取其** 他字型目錄。 此下拉式選單列出在「首頁>設定>核心繫 **統>核心組態」中指定的字型目錄**。
   * 從「可用字型」清單中選取一或多 **個字型** ，然後按一下「 **新增」**。 這些字型會新增至「要取消 **內嵌的字型** 」清單。
   * 如果您想要取消內嵌某些表格伺服器上不存在的字型，請在「新增字型至取消內嵌」方塊中輸入這些字型的名稱 **** 。 按一下&#x200B;**「新增」**。
   >[!NOTE]
   >
   >*如果您想要取消內嵌部分子集已內嵌在檔案中的字型，請在字型名稱前加上+號。 例如，&quot;+Helvetica&quot;。*

1. 如果您只想內嵌使用中字型的子集，請選取「子集所有內嵌字 **型」**。

   >[!NOTE]
   >
   >*如果您搭配使用這個選項與「取消內嵌」**部分字型**,「將字型新增至取消內嵌」清單中的字型仍&#x200B;****然完全取消內嵌。*

   >[!NOTE]
   >
   >*字型子設定是只內嵌部分字型的技巧。 字型子集僅包含檔案中使用的字元。*

### 透明度 {#transparency}

如果您的PDF檔案包含包含透明度的圖稿，您可以使用PDF最佳化程式設定來平面化透明度並減少檔案大小。

>[!NOTE]
>
>如果選取Acrobat 4.0和更新版本做為Target PDF版本，所有透明物件都會平面化。 對於其他Target PDF版本，支援透明度，您可以設定透明度設定。

選取「 **透明度** 」，在最佳化PDF檔案時設定透明度設定。

**透明度** ：指定要保留的向量資訊量。 較高的設定會保留更多的向量物件，而較低的設定則會點陣化更多的向量物件；中介設定會保留向量格式的簡單區域，並點陣化複雜的區域。 選取最低的設定，點陣化所有圖稿。

>[!NOTE]
>
>產生的點陣化量取決於頁面的複雜性和重疊物件的類型。

**線條圖和文字解析度** ，所有物件（包括影像、向量圖稿、文字和漸層）都會點陣化到這些物件。 支援的值是1像素／英吋(ppi)至9600 ppi。

>[!NOTE]
>
>線條圖和文字解析度一般應設為600-1200 ppi，以提供高品質點陣化，尤其是針對有襯線或小型點數字型。

**漸層和網格** ：漸層和網格的柵格化解析度。 支援的值為1 ppi至1200 ppi。

>[!NOTE]
>
>漸層和網格解析度一般應設為150-300 ppi，因為漸層、陰影和羽化的品質不會隨著解析度的提高而改善，但列印時間和檔案大小會增加。

**將所有文本轉換為輪廓** 將所有類型對象（點類型、區域類型和路徑類型）轉換為輪廓並丟棄包含透明度的頁面上的所有類型字元資訊。 此選項可確保文字寬度在平面化期間維持一致。 請注意，啟用此選項會在Acrobat中檢視或在低解析度的桌上型印表機上列印時，使小字型看起來稍微粗些。 它不會影響列印在高解析度印表機或影像機上的文字品質。

**將所有筆畫轉換為輪廓** 將包含透明度的頁面上的所有筆畫轉換為簡單的填色路徑。 此選項可確保在平面化期間筆畫的寬度保持一致。 請注意，啟用此選項會使細筆畫看起來稍微粗一些，並會降低平面化效能。

**剪輯複雜區域** —確保向量圖稿和點陣化圖稿之間的邊界沿物件路徑落下。 此選項可減少在日誌的一部分時導致的拼接工件

>[!NOTE]
>
>有些列印驅動程式會以不同的方式處理點陣圖和向量圖，有時會產生色彩拼接。 通過禁用某些打印驅動程式特定的色彩管理設定，您可以將拼接問題降到最低。 這些設定隨每台打印機而異，因此，有關詳細資訊，請參閱打印機附帶的文檔。

保留疊印：混合透明圖稿的顏色和背景顏色，以建立疊印效果。

下表顯示一般的印表機類型及其解析度（以dpi測量）、預設螢幕尺規(以每英吋行數(lpi)測量)，以及以每英吋像素數(ppi)測量的影像重新取樣解析度。 例如，如果要打印到600 dpi雷射打印機，則要重新取樣影像的解析度應輸入170。

**「影像** 」選取「影像」，以指定彩色、灰階和單色影像的壓縮和重新取樣選項。 您可能想要嘗試這些選項，以在檔案大小和影像品質之間找到適當的平衡。彩色和灰階影像的解析度設定應是列印檔案時的1.5到2倍。 單色影像的解析度應該與輸出裝置相同，但請注意，將單色影像儲存為高於1500 dpi的解析度會增加檔案大小，而不會明顯改善影像品質。 將放大的影像（例如地圖）可能需要更高的解析度。

>[!NOTE]
>
>重新取樣單色影像可能會產生非預期的檢視結果，例如無影像顯示。 如果發生此情況，請關閉重新取樣並重新轉換檔案。 這個問題最有可能發生在亞採樣中，而最不可能發生在雙立方體縮減採樣中。

<table>
 <tbody>
  <tr>
   <th><p><strong>打印機解析度</strong></p> </th>
   <th><p><strong>預設行畫面</strong></p> </th>
   <th><p><strong>影像解析度</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 dpi（雷射打印機）</p> </td>
   <td><p>60 lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi（雷射打印機）</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 dpi（照排機）</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi（照排機）</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

#### 捨棄物件 {#discard-objects}

* 選擇「 **捨棄對象** 」(Discard Objects)，指定要從PDF中移除的對象，並優化CAD繪圖中的曲線。
* **放棄所有表單提交、匯入和重設動作**:停用與提交或匯入表單資料相關的所有動作，並重設表單欄位。 此選項會保留動作連結到的表單物件。
* **捨棄所有JavaScript動作**:從PDF移除任何使用JavaScript的動作。
* **捨棄內嵌的頁面縮圖**:移除內嵌的頁面縮圖。 此選項對於大型檔案很有用，在您按一下「頁面」按鈕後，可能需要很長時間才能繪製頁面縮圖。
* **將平滑線轉換為曲線**:減少在CAD繪圖中建立曲線時所使用的控制點數，如此可縮小PDF檔案並加快螢幕上的轉換速度。
* **捨棄嵌入的打印設定**:從文檔中刪除嵌入的打印設定，如頁面縮放和雙工模式。
* **捨棄書籤**:從檔案中移除所有書籤。
* **平面化表單欄位**:使表單欄位無法使用，而且外觀不會變更。 表單資料會與頁面合併，成為頁面內容。
* **捨棄所有替代影像**:移除影像的所有版本，但目的是在螢幕上檢視的版本除外。 有些PDF包含多個版本的相同影像，以用於不同用途，例如螢幕上低解析度檢視和高解析度列印。
* **捨棄檔案標籤**:從檔案中移除標籤，也會移除文字的協助功能和重排功能。
* **偵測並合併影像片段**:尋找分割為薄片的影像或遮色片，並嘗試將切片合併為單一影像或遮色片。
* **捨棄內嵌搜尋索引**:移除內嵌的搜尋索引，以減少檔案大小。

#### 捨棄使用者資料 {#discard-user-data}

選 **擇捨棄用戶資料** ，以刪除您不想分發或與其他用戶共用的任何個人資訊。

* **捨棄所有注釋、表單和多媒體**:從PDF移除所有注釋、表格、表格欄位和多媒體。
* **捨棄所有物件資料**:從PDF移除所有物件。
* **捨棄外部交互參照**:移除其他檔案的連結。 跳至PDF中其他位置的連結不會移除。
* **捨棄隱藏圖層內容並平面化可見圖層**:減少檔案大小。 最佳化檔案看起來與原始PDF相同，但不包含圖層資訊。
* **捨棄檔案資訊和中繼資料**:移除檔案資訊字典和所有中繼資料串流中的資訊。 （使用「另存新檔」命令，將中繼資料串流還原為PDF的副本）。
* **放棄檔案附件**:移除所有檔案附件，包括新增至PDF的附件作為注釋。 （PDF Optimizer不會最佳化附加的檔案。）
* **捨棄其他應用程式的私用資料**:從PDF檔案中移除資訊，這些資訊只對建立檔案的應用程式有用。 此設定不會影響PDF的功能，但會降低檔案大小。

### 清理 {#clean-up}

選擇 **「清理** 」，從文檔中刪除不必要的項目。
這些項目包括過時或不必用於文檔用途的元素。 移除某些元素會嚴重影響PDF的功能。 依預設，僅選取不影響功能的元素。 如果您不確定移除其他選項的含意，請使用預設選項。

**壓縮**

從下拉式選單中選取下列其中一個「篩選壓縮」選項：

* 壓縮整個檔案
* 壓縮檔案結構
* 移除壓縮
* 保留壓縮不變

**使用Flate來編碼未編碼的串流**:將Flate壓縮套用至所有未編碼的串流。

**捨棄無效書籤**:移除指向已刪除檔案中頁面的書籤。

**放棄未引用的命名目標**:從PDF檔案移除未在內部參考的已命名目標。 此選項不會檢查其他PDF檔案或網站的連結。

**最佳化PDF以快速檢視網頁**:重新架構PDF檔案，以便從網頁伺服器進行逐頁下載（位元組伺服）。

**在使用LZW編碼的串流中，請改用Flate**:將Flate壓縮套用至所有使用LZW編碼的內容串流和影像。

**捨棄無效連結**:移除跳至無效目的地的連結。

**最佳化頁面內容**:將所有行尾字元轉換為空格字元，以改善Flate壓縮。

## Microsoft excel設定（僅限Windows） {#microsoft-excel-settings-windows-only}

這些選項決定如何轉換Microsoft excel檔案。 有關訪問這些選項的說明，請參 [閱建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)。

**試用OpenOffice做為備援轉換器**:當選取此選項，而使用Microsoft excel的轉換失敗或達到指定的逾時限制時，PDF產生器會使用OpenOffice來嘗試轉換。 如果使用OpenOffice的轉換失敗或達到指定的逾時限制，則會將例外寫入日誌檔案。

**副檔名**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設值為 `xls,xlsx`。 請勿在擴充功能之前加入句號或之間加入空格。

**建立PDF/A-1a相容檔案**:強制使用PDF/A-1b:2005 RGB Adobe PDF設定。

**新增書籤至Adobe PDF**:將Excel工作表名稱轉換為書籤。 預設會選取此選項。

**將工作表調整為單一頁面**:縮小文字大小，以符合單一頁面上的工作表大小。

**轉換整個活頁簿**:轉換Excel檔案中的所有工作表。 如果未選取此選項，則僅轉換目前的頁面。

**自動運行宏**:在轉換檔案之前，先執行Excel檔案中的任何巨集（例如插入目前時間的巨集）。

**轉換檔案資訊**:根據來源檔案中的檔案資訊新增PDF檔案屬性。 這包括檔案標題、作者、主旨和關鍵字等資訊。

**新增Adobe PDF的連結**:將來源檔案中的超連結轉換為PDF檔案中的超連結。

**將來源檔案附加至Adobe PDF**:選取此選項時，原始Excel試算表會插入為產生之PDF檔案內的附件。

**使用標籤的Adobe PDF啟用協助工具和重排**:在PDF檔案內內嵌標籤，以啟用協助功能和重排。

**要載入的Excel增益集清單**:依預設（基於安全性原因），當Excel檔案轉換為PDF時，不會執行Excel增益集。 若要允許在轉換期間執行某些Excel增益集，請提供以逗號分隔的增益集名稱清單。

**要轉換的工作表清單**:當此方塊為空白時，Excel試算表中的所有工作表都會包含在產生的PDF中。 若要選擇性轉換工作表的子集，請提供以逗號分隔的工作表名稱清單。

## Microsoft powerPoint設定（僅限Windows） {#microsoft-powerpoint-settings-windows-only}

這些選項決定了Microsoft powerPoint檔案的轉換方式。 有關訪問這些選項的說明，請參 [閱建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings)。

**[!UICONTROL 試用OpenOffice做為備援轉換器]**:當選取此選項，而使用Microsoft powerPoint的轉換失敗或達到指定的逾時限制時，PDF產生器會使用OpenOffice來嘗試轉換。 如果使用OpenOffice的轉換失敗或達到指定的逾時限制，則會將例外寫入日誌檔案。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設值為ppt,pptx。 請勿在擴充功能之前加入句號或之間加入空格。

**[!UICONTROL 轉換檔案資訊]**:從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。

**[!UICONTROL 新增書籤至Adobe PDF]**:將PowerPoint標題轉換為書籤。 預設會選取此選項。

**[!UICONTROL 將來源檔案附加至Adobe PDF]**:將來源檔案新增至PDF檔案做為附件。 預設會取消選取此選項。

**[!UICONTROL 使用標籤的Adobe PDF啟用協助工具和重排]**:將標籤嵌入PDF檔案。 預設會取消選取此選項。

**[!UICONTROL 將多媒體轉換為PDF多媒體]**:盡可能將多媒體轉換為PDF多媒體。 預設會選取此選項。

**[!UICONTROL 轉換主講人附註]**:將主講人附註轉換為PDF。

**[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行PowerPoint文檔中的任何宏（如插入當前時間的宏）。

**[!UICONTROL 基於PowerPoint印表機設定的PDF版面配置]**:使用PowerPoint印表機設定來配置PDF檔案的版面。

**[!UICONTROL 新增Adobe PDF的連結]**:在轉換檔案時保留現有的連結。 連結的外觀一般不會改變。 只有在同時選取「啟用協助工具」選項時，才可建立連結。 預設會取消選取此選項。

**[!UICONTROL 將投影片轉場效果儲存在Adobe PDF中]**:轉換投影片轉場效果。 預設會選取此選項。

**[!UICONTROL 將動畫儲存在Adobe PDF中]**:將轉換的動畫儲存在PDF檔案中。

**[!UICONTROL 將隱藏的投影片轉換為PDF頁面]**:轉換隱藏的投影片。

**[!UICONTROL 建立PDF/A-1a相容檔案]**:強制使用PDF/A-1b:2005 RGB Adobe PDF設定。 當您產生PDF檔案時，不會轉換一些PowerPoint功能。 如果Acrobat中的PowerPoint轉場沒有相同的轉場，則會取代類似的轉場。 如果多個動畫效果位於同一張投影片中，則會使用單一效果。 頁面切換效果和項目符號跳轉效果會進行轉換。

## Microsoft project設定（僅限Windows） {#microsoft-project-settings-windows-only}

這些選項決定了Microsoft project檔案的轉換方式。 有關訪問這些選項的說明，請參 [閱建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)。

1. **** 副檔名：指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設值為 `mpp`。 請勿在擴充功能之前加入句號或之間加入空格。

1. **[!UICONTROL 轉換檔案資訊]**:從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。
1. **[!UICONTROL 將來源檔案附加至Adobe PDF]**:將來源檔案新增至PDF檔案做為附件。
1. **[!UICONTROL 建立PDF/A-1a相容檔案]**:強制使用PDF/A-1b:2005 RGB Adobe PDF設定。
1. **[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行Microsoft project文檔中的任何宏（如插入當前時間的宏）。

## Microsoft word設定（僅限Windows） {#microsoft-word-settings-windows-only}

這些選項決定如何轉換Microsoft word檔案。 有關訪問這些選項的說明，請參 [閱建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)。

**[!UICONTROL 試用OpenOffice做為備援轉換器]**:當選取此選項，而使用Microsoft word的轉換失敗或達到指定的逾時限制時，PDF產生器會使用OpenOffice來嘗試轉換。 如果使用OpenOffice的轉換失敗或達到指定的逾時限制，則會將例外寫入日誌檔案。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設值為 `doc,docx,rtf,txt`。 請勿在擴充功能之前加入句號或之間加入空格。

**[!UICONTROL 轉換檔案資訊]**:從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。

**[!UICONTROL 新增書籤至Adobe PDF]**:將標題轉換為書籤。 預設會選取此選項。

**[!UICONTROL 將來源檔案附加至Adobe PDF]**:將來源檔案新增至PDF檔案做為附件。

**[!UICONTROL 將交互參照和目錄轉換為連結]**:將所有交叉引用和目錄條目轉換為連結。 預設會選取此選項。

**[!UICONTROL 使用標籤的Adobe PDF啟用協助工具和重排]**:將標籤嵌入PDF檔案。 預設會選取此選項。

**[!UICONTROL 建立PDF/A-1a相容檔案]**:如果選取此選項，強制使用PDF/A-1b:2005 RGB Adobe PDF設定。

**[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行Word文檔中的任何宏（如插入當前時間的宏）。

**[!UICONTROL 保留Adobe PDF中的檔案標籤]**:將Word檔案中的標籤轉換為PDF檔案中的註解。

**[!UICONTROL 新增Adobe PDF的連結]**:將來源檔案中的超連結轉換為PDF檔案中的超連結。

**[!UICONTROL 轉換注腳和章節附註連結]**:從注腳和附註引文建立連結至PDF檔案中的附註。

**[!UICONTROL 在Adobe PDF中將顯示的注釋轉換為附註]**:將Word檔案中的注釋轉換為PDF檔案中的文字注釋。

**[!UICONTROL 啟用進階標籤]**:新增進階標籤以增強協助功能。

**[!UICONTROL 將所有樣式轉換為書籤]**:將Word檔案中的所有樣式轉換為PDF檔案中的書籤。

**[!UICONTROL 含色階的樣式]**:指定Word檔案中哪些樣式會轉換為PDF檔案中的書籤。 也指定書籤的層級。 若要使用此功能，請取消選取「 **[!UICONTROL 將所有樣式轉換為書籤]** 」選項，並以下列格式指定樣式名稱：

styleName1=level1[,styleName2=level2...]

如果Microsoft word樣式名稱包含逗號(,)或等號(=)，請在特殊字元前加上轉義字元(&quot;\_)。 例如，指定名為&quot;Heading, 1&quot;的樣式為Heading\, 1。

## Microsoft Visio設定（僅限Windows） {#visio}

**轉換檔案資訊**:從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。 預設會啟用此選項。

**新增Adobe PDF的連結**:保留所有連結。 預設會選取此選項。

**新增書籤至Adobe PDF**:將標題轉換為書籤。 預設會選取此選項。

**將來源檔案附加至Adobe PDF**:將來源檔案新增至PDF檔案做為附件。

**一律平面化Adobe PDF中的圖層**:平面化所有Visio圖層。

**轉換所有頁面**:轉換Visio檔案的所有頁面。

**在Adobe acrobat中檢視時開啟圖層面板**:如果Visio圖層未平面化，則會開啟一個視窗，您可以在其中指定當使用Acrobat開啟時，PDF檔案中保留的圖層。 預設會選取此選項。

**建立PDF/A-1b相容檔案**:強制使用Adobe PDF設定PDF/A-1b:2005(RGB)。

**將注釋轉換為Adobe PDF注釋**:將Visio注釋轉換為PDF注釋。

## Microsoft Publisher設定（僅限Windows） {#microsoft-publisher-settings-windows-only}

這些選項決定如何轉換Microsoft Publisher檔案。 有關訪問這些選項的說明，請參 [閱建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設值為 `pub`。 請勿在擴充功能之前加入句號或之間加入空格。

## AutoCAD設定（僅限Windows） {#autocad-settings-windows-only}

這些選項決定如何轉換AutoCAD檔案。 有關訪問這些選項的說明，請參 [閱建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings)。

**[!UICONTROL 副檔名]**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設值為 `dwg`。 請勿在擴充功能之前加入句號或之間加入空格。

**[!UICONTROL 轉換檔案資訊]**:從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和注釋。 預設會選取此選項。

**[!UICONTROL 新增書籤至Adobe PDF]**:將標題轉換為書籤。

**[!UICONTROL 一律平面化Adobe PDF中的圖層]**:平面化所有AutoCAD圖層。

**[!UICONTROL 在Adobe Acrobat中檢視時開啟圖層窗格]**:在Acrobat中開啟PDF時顯示圖層結構。

**[!UICONTROL 建立PDF/E-1相容檔案]**:建立符合PDF/E-1規範的檔案。 PDF/E是交換工程與技術檔案的ISO標準。 如需PDF/E-1的詳細資訊，請參閱 [Adobe和業界標準](https://www.adobe.com/enterprise/standards/index.html)。

**[!UICONTROL 轉換所有版面]**:在PDF中包含所有版面。

**[!UICONTROL 將模型空間轉換為3D]**:選中後，模型空間佈局將轉換為PDF中的3D注釋。

**[!UICONTROL 新增Adobe PDF的連結]**:如果選取此選項，則保留所有連結。

**[!UICONTROL 將來源檔案附加至Adobe PDF]**:將來源檔案新增至PDF檔案做為附件。

**[!UICONTROL 建立PDF/A-1b相容檔案]**:強制使用PDF/A-1b Adobe PDF設定。

**[!UICONTROL 轉換所有圖層]**:根據預設，PDF產生器僅將AutoCAD檔案的預設圖層轉換為PDF，而非檔案中的所有圖層。 選擇此選項可轉換檔案的所有圖層。

**[!UICONTROL 內嵌比例資訊]**:保留繪圖比例資訊。

**[!UICONTROL 轉換目前的版面]**:在PDF中只包含目前的版面。

**[!UICONTROL 要轉換的AutoCAD版面清單]**:AutoCAD繪圖可以有多個版面。 當此框為空時，AutoCAD繪圖中的所有佈局都將包含在生成的PDF文檔中。 若要選擇性轉換版面的子集，請提供版面名稱的逗號分隔清單。

## OpenOffice設定 {#openoffice-settings}

這些選項決定如何轉換OpenOffice檔案。 有關訪問這些選項的說明，請參 [閱建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings)。

**嘗試將PDFMaker作為備援轉換器**:當選取此選項，而使用OpenOffice的轉換失敗或達到指定的逾時限制時，PDF產生器會使用PDFMaker來嘗試轉換。 如果使用PDFMaker的轉換失敗或達到指定的逾時限制，則會將異常寫入日誌檔案。

**副檔名**:指定此應用程式所接受之檔案類型的副檔名（以逗號分隔）。 預設值為 `odt,odp,ods,odg,odf,sxw,sxi,sxd`。 請勿在擴充功能之前加入句號或之間加入空格。

**範圍**:轉換所有頁面或指定特定頁面或頁面範圍。 如果未定義頁面範圍，則會轉換所有頁面。 若要匯出一系列頁面，請使用格式3-6。 要導出單頁，請使用格式7;9;11。 可以使用3-6;8;10;12等格式導出頁面範圍和單頁的組合。

**頁面方向**:僅適用於純文字檔案，請為轉換的PDF檔案選取縱向或橫向。

**影像**:設定影像轉換的方式。 具有內嵌預覽的EPS影像只會匯出為預覽。 未嵌入預覽的EPS影像將導出為空佔位符。 使用影像的無損壓縮，會保留所有像素。 由於影像的JPEG壓縮和高品質等級，幾乎所有像素都會保留。 在低品質的層級中，有些像素會遺失，而且會產生偽影，但檔案大小會減少。

**一般**:啟用選項，將標籤的PDF轉換或將Writer和FormCalc檔案註解、Impress投影片轉換效果或空白頁面匯出為PDF。 匯出標籤時，檔案大小可能會大幅增加。 某些匯出的標籤是目錄、超連結和控制項。

您也可以指定表單的提交方式。 選項包括XML、FDF、PDF或HTML。 此設定會覆寫您在檔案中設定的控制項URL屬性。 PDF檔案只能選取一個常用設定：

* PDF（傳送整份檔案）
* FDF（傳送控制內容）
* HTML
* XML

**標籤的PDF**:允許從OpenOffice檔案建立標籤的PDF。 標籤的PDF包含有關文檔內容結構的資訊。 這有助於在不同螢幕的裝置上顯示檔案，以及使用螢幕閱讀程式軟體時。 此外，它還可協助協助協助工具軟體對PDF檔案執行各種有用的作業，例如朗讀PDF檔案的內容。

**匯出附註**:將OpenOffice檔案中的附註轉換為產生的PDF檔案中的附註。

**使用轉場效果**:將OpenOffice簡報中的投影片轉場效果轉換為對應的PDF轉場效果。

**以格式提交表單**:建立可由PDF檔案使用者填寫及列印的PDF表格。

**自動匯出插入的空白頁面**:選取此選項時，自動插入的空白頁面會包含在產生的PDF檔案中。 如果您要雙面列印PDF檔案，這個功能就很實用。 例如，可以配置書籍，使章節的第一頁始終從奇數頁開始。 如果上一章在奇數頁面結尾，OpenOffice會在空白偶數頁面中插入。 此選項控制是否在產生的PDF中包含該偶數編號的頁面。

## 其他應用程式設定（僅限Windows） {#other-applications-settings-windows-only}

您無法透過管理控制台來變更其他應用程式的設定；它們顯示支援檔案類型的檔案副檔名。 有關訪問這些設定的說明，請參 [閱建立或編輯檔案類型設定](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html)。

* Corel wordPerfect: `wpd`
* Adobe pageMaker: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

可能需要自訂這些檔案類型的支援。 如需詳細資訊，請參閱「使用AEM表單進行程式設計」中的「新增對其他原 [生檔案格式的支援」](https://www.adobe.com/go/learn_aemforms_programming_62)。

有關配置PDFG網路打印機的幫助，請參 [閱設定PDFG網路打印機（僅限Windows）](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md)。
