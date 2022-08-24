---
title: 配置檔案類型設定
seo-title: Configuring file type settings
description: 瞭解如何配置檔案類型設定。
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

在「PDF生成器」中，可以設定受支援檔案類型的應用程式設定。 在Windows上，可以為每個受支援的檔案類型設定應用程式設定。 在UNIX和Linux上，可以設定HTML到PDF和OpenOffice的應用程式設定。

在「檔案類型設定」頁上，可以執行以下任務：

* [建立或編輯檔案類型設定](#create-or-edit-file-type-settings)
* 指定預設使用的檔案類型設定(請參見 [導入和導出PDF生成器配置檔案](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html))
* [更改預設設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#change-the-default-settings)
* [啟用PDF/A支援](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [刪除檔案類型設定](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>檔案類型設定不適用於備用轉換器，如用於HTML到PDF轉換的Acrobat、MicrosoftPowerPoint、MicrosoftWord和MicrosoftExcel。

## 建立或編輯檔案類型設定 {#create-or-edit-file-type-settings}

建立或編輯檔案類型設定，以指定應用程式如何處理受支援檔案類型的轉換。 在Windows上，可以為每個受支援的檔案類型設定應用程式設定。 在UNIX和Linux上，可以設定HTML到PDF和OpenOffice的應用程式設定。

1. 在管理控制台中，按一下 **[!UICONTROL 服務]** > **[!UICONTROL PDF發生器]** > **[!UICONTROL 檔案類型設定]**。
1. 按一下「新建」或按一下設定的名稱。
1. 在「檔案名副檔名」框中，為此應用程式接受的檔案類型鍵入檔案副檔名（以逗號分隔）。 不要包括擴展之前的句點或擴展之間的空格。 預設為 `bmp,gif,jpeg,jpg,tif,tiff,png`。
1. （可選）要在圖形或影像中使用文本的光學代碼識別(OCR)，請選擇「使用OCR」並設定以下選項：

**主要OCR語言：** 用於標識字元的OCR引擎的語言。 預設為英語（美國）。

**PDF輸出樣式：** 選擇「可搜索影像」，將頁面的點陣圖影像置於前景中，並將掃描的文本置於下方的不可見圖層上。 頁面外觀不會更改，但文本將變為可選和可讀。 選擇「格式化文本和圖形」(Formatted Text &amp; Graphics)，使用識別的文本、字型、圖片和其他圖形元素重構原始頁面。 預設為可搜索影像（精確）。

**下採樣影像：** 減少彩色、灰度和單色影像中的像素數。 在完成OCR後執行掃描影像的下採樣。 預設值為「最低」(600 dpi)。 如果將PDF輸出樣式設定為「可搜索影像（精確）」，則此選項不可用。

1. 完成以下各節中的所需資訊：

   [導入和導出PDF生成器配置檔案](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

[Adobe PDF導出設定（僅限Windows）](#adobe-pdf-export-settings-windows-only)

[HTML到PDF設定](#html-to-pdf-settings)

[Flash視頻到PDF設定](#flash-videos-to-pdf-settings)

[XPS到PDF設定](#xps-to-pdf-settings)

[PDF優化程式設定](#pdf-optimizer-settings)

[MicrosoftExcel設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-excel-settings-windows-only)

[MicrosoftPowerPoint設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-powerpoint-settings-windows-only)

[Microsoft項目設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-project-settings-windows-only)

[MicrosoftWord設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-word-settings-windows-only)

[MicrosoftVisio設定（僅限Windows）](#visio)

[Microsoft發佈者設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-publisher-settings-windows-only)

[AutoCAD設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#autocad-settings-windows-only)

[OpenOffice設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#openoffice-settings)

[其他應用程式的設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#other-applications-settings-windows-only)

   要轉到其他部分，請按一下其網頁上的連結或使用**[!UICONTROL 下一個]**或 **[!UICONTROL 上一個]** 按鈕。

1. 完成所有部分後，按一下 **[!UICONTROL 保存]** 或 **[!UICONTROL 另存為]** 並提供設定的名稱。

可以自定義對各種檔案類型的支援。 (請參閱「 [添加對其他本機檔案格式的支援](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; [用表格編AEM程](https://www.adobe.com/go/learn_lc_programming_11)。)

## 更改預設設定 {#change-the-default-settings}

您可以更改應用於新建立源的Adobe PDF設定、安全設定和檔案類型設定的預設值。 更改預設值不會影響現有源的設定。

1. 在管理控制台中，按一下 **[!UICONTROL 服務>PDF生成器]**。
1. 在 **[!UICONTROL Adobe PDF設定]**。 **[!UICONTROL 檔案類型設定]**&#x200B;或 **[!UICONTROL 安全設定]** 的 **[!UICONTROL 設定預設設定]**。
1. 選擇首選預設設定。 「設定預設設定」(Set Default Settings)頁面上提供以下一個或多個設定：

   **[!UICONTROL Adobe PDF設定]**:原始預設值為Standard(Acrobat 6)。

   **[!UICONTROL 安全設定]**:原始預設值為No Security(Acrobat 5)。

   **[!UICONTROL 檔案類型設定]**:原始預設值為「標準」(Standard)。

1. 按一下「**[!UICONTROL 儲存]**」。

## 刪除檔案類型設定 {#delete-a-file-type-setting}

可以刪除不再使用的檔案類型設定。

1. 在管理控制台中，按一下 **[!UICONTROL 服務>PDF生成器>檔案類型設定]**。
1. 選中要刪除的設定旁邊的複選框。 可以選擇多個源。 沒有複選框的設定始終包含在PDF生成器中，無法刪除。
1. 按一下 **[!UICONTROL 刪除]** 並在「刪除確認」頁上，按一下 **[!UICONTROL 刪除]**。

## 影像到PDF設定 {#image-to-pdf-settings}

以下選項確定如何將影像檔案轉換為PDF。 有關訪問這些設定的說明，請參見 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**檔案副檔名：** 可轉換的檔案副檔名的逗號分隔清單。

**嘗試回退轉換器：** PDF生成器可以使用Java™或Acrobat將影像檔案轉換為PDF。 當選中此選項且轉換失敗或達到指定的超時限制時，PDF生成器會嘗試使用替代方法進行轉換。 如果替代方法失敗或達到指定的超時限制，則會將異常寫入日誌檔案。

>[!NOTE]
>
>JPEG2000檔案只能使用Acrobat轉換。

**使用OCR:** 指定是否將OCR（光學字元識別）應用於PDF。 OCR軟體使您能夠搜索、更正和複製PDF中的文本。

***附註&#x200B;**:OCRPDF(可搜索PDF)功能僅在MicrosoftWindows上受支援。*

**主要OCR語言：** 指定OCR引擎用於標識字元的語言。

**PDF輸出樣式：** 確定要生產的PDF類型。 所有格式都將OCR和字型及頁面識別應用於文本影像，並將它們轉換為普通文本。

**可搜索的映像：** 確保文本可搜索和可選。 此選項保留原始影像，根據需要進行描述，並在其上放置一個不可見的文本圖層。 「下採樣影像」選項確定是否對影像進行下採樣以及下採樣到什麼程度。

**可搜索影像（準確）:** 確保文本可搜索和可選。 此選項保留原始影像，並在其上放置不可見的文本圖層。 建議用於對原始影像要求最高保真度的情況。

**ClearScan:** 合成與原始字型接近的新類型3字型，並使用低解析度副本保留頁面背景。

**下採樣影像：** 在完成OCR後，減少彩色、灰度和單色影像中的像素數。 選擇要應用的縮減採樣程度。 編號較高的選項減少了降採樣，從而產生了較高的解析度PDF。

## Adobe PDF導出設定（僅限Windows） {#adobe-pdf-export-settings-windows-only}

「Adobe PDF導出設定」部分中的「導出檔案類型」設定用於將PDF檔案轉換為其他格式。 預設為HTML4.01與級聯樣式表(CSS)1.0(*.htm, *.html)。

有關訪問此設定的說明，請參見 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

## HTML到PDF設定 {#html-to-pdf-settings}

以下選項確定如何將HTML檔案轉換為PDF。 有關訪問這些選項的說明，請參見 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**嘗試回退轉換器：** PDF生成器可以使用Java™或Acrobat將HTML檔案轉換為PDF。 當選中此選項且轉換失敗或達到指定的超時限制時，PDF生成器會嘗試使用替代方法進行轉換。 如果替代方法失敗或達到指定的超時限制，則會將異常寫入日誌檔案。

**預設編碼：** 從作業系統和字母表菜單設定檔案文本的輸入編碼。 僅當HTML源檔案未指定編碼類型時，才使用預設編碼選項中顯示的選擇。

**強制選定編碼：** 忽略在HTML源檔案中指定的任何編碼，並使用預設編碼選項中顯示的選擇。

### 插入設定 {#spidering-settings}

*尖吻* 掃描網頁以查找指向其他網頁的連結。 當遇到到另一個網頁的連結時，將讀取目標頁面並將其包括在所生成的PDF文檔中。 啟用以下選項可設定要讀取並轉換為PDF的級別數：

**僅獲取X級：** 從基頁URL將頁面從基頁URL向上轉換到指定級別的深度。 值1僅轉換提供的URL。

**獲取整個站點：** 從提供的URL開始轉換整個站點。

**保持同一路徑：** 指向與基本URL不位於相對路徑上的頁面的任何連結，都不會在插入過程中轉換。

**保持在同一伺服器上：** 指向不同伺服器上頁面的任何連結在插入期間不會轉換。 只轉換指向與指定URL相同的伺服器的連結。

### 頁面轉換設定 {#page-conversion-settings}

啟用這些選項以指定如何轉換HTML頁。 根據頁面大小，寬度、高度和邊距值會相應調整。

**頁面大小：** 選擇自定義並指定寬度和高度，或選擇預定義尺寸。

**方向：** 為轉換的PDF文檔選擇縱向或橫向。

**邊距：** 指定生成的PDF文檔中的邊距（「上」、「下」、「左」和「右」）。

**將書籤添加到PDF:** 將書籤添加到PDF文檔。

**啟用標籤PDF:** 在PDF文檔中嵌入標籤。

**設定初始視圖設定：** 用於配置文檔選項、窗口選項和用戶介面選項。 這些設定確定內容最初的顯示方式。

### 文檔選項 {#document-options}

啟用這些選項可指定如何顯示內容、如何在PDF文檔中顯示頁面以及如何指定放大率級別：

**顯示：** 選擇開啟Acrobat文檔時要在PDF中開啟的窗格。

**頁面佈局：** 選擇PDF文檔的頁面佈局類型。

**放大率：** 為PDF文檔的初始視圖選擇預設的放大率，或選擇自定義值。 選擇預設設定表示將使用預設的Acrobat放大率。

**開啟至頁碼：** 指定PDF開啟的頁碼。

### 窗口選項 {#window-options}

啟用這些選項以指定窗口的大小和顯示方式。

**將窗口調整為初始頁：** 將Acrobat窗口調整為初始頁面的大小。

**螢幕中心窗口：** 開啟螢幕中央的窗口。

**以全屏模式開啟：** 以全屏模式開啟窗口。

**顯示：** 在窗口中顯示文檔標題或檔案名。

### 用戶介面選項 {#user-interface-options}

啟用以下選項以指定窗口外觀：

**隱藏菜單欄：** 隱藏PDF文檔中的菜單欄。

**隱藏工具欄：** 隱藏PDF文檔中的工具欄。

**隱藏窗口控制項：** 隱藏PDF文檔中的窗口控制項。

## Flash視頻到PDF設定 {#flash-videos-to-pdf-settings}

PDF生成器支援提交視頻以進行AdobeFlash(SWF或FLV檔案)，並建立包含視頻的AdobeFlash檔案。 此轉換不需要在表單伺服器上安裝AdobeFlash Player。 有關訪問此選項的說明，請參見 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**檔案副檔名：** 可轉換的檔案副檔名的逗號分隔清單。

## XPS到PDF設定 {#xps-to-pdf-settings}

XML紙張規範(XPS)在Windows打印機中使用。 這是Microsoft格式，可以從任何Microsoft辦公室應用程式建立。 表AEM單提供了轉換XPS檔案的PDF。

**檔案副檔名：** 可轉換的所有XPS檔案副檔名的逗號分隔清單。 當前有一種格式：.xps。

## PDF優化程式設定 {#pdf-optimizer-settings}

PDF生成器支援減少PDF檔案大小的功能。 是使用所有這些設定還是僅使用少數設定取決於您打算如何使用這些檔案以及檔案必須具有的基本屬性。 在大多數情況下，預設設定適合於實現最高效率 — 通過刪除嵌入字型、壓縮影像以及從不再需要的檔案中刪除項目來節省空間。

>[!NOTE]
>
>優化數字簽名文檔會刪除並使數字簽名失效。

有關訪問此設定的說明，請參見 [建立或編輯檔案類型設定](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**目標PDF版本：** 指定PDF與之相容的Acrobat版本。

### 字型 {#fonts}

1. 選擇 **字型。**
1. 選擇以下選項之一：

   **取消嵌入所有字型：** 解除嵌入所有嵌入字型。

   **不取消嵌入任何字型：** 不取消嵌入任何字型。

   **取消嵌入某些字型：** 只嵌入指定的字型。 按照以下步驟指定要取消嵌入的字型：

   * 如有必要，請從 **字型源** 的下界。 此下拉菜單列出了在中指定的字型目錄 **首頁>設定>核心繫統>核心配置**。
   * 從 **可用字型** 按一下 **添加**。 這些字型將添加到 **要取消嵌入的字型** 清單框。
   * 如果要取消嵌入某些在forms伺服器上不存在的字型，請在 **添加要取消嵌入的字型** 框。 按一下&#x200B;**「新增」**。

   >[!NOTE]
   >
   >*如果要取消嵌入其子集嵌入到文檔中的某些字型，請在字型名稱前加上+號。 例如，「+Helvetica」。*

1. 如果只嵌入嵌入字型的正在使用的子集，請選擇 **子集所有嵌入字型**。

   >[!NOTE]
   >
   >*如果您與&#x200B;**取消嵌入某些字型**，字型&#x200B;**添加要取消嵌入的字型**清單仍未嵌入。*

   >[!NOTE]
   >
   >*字型子設定是僅嵌入字型一部分的技術。 字型子集僅包含文檔中使用的字元。*

### 透明度 {#transparency}

如果PDF文檔包含包含透明度的圖稿，則可以使用PDF優化程式設定來拼合透明度並減小檔案大小。

>[!NOTE]
>
>如果選擇Acrobat 4.0和更高版本作為目標PDF版本，則所有透明對象都會展平。 對於其他目標PDF版本，支援透明度，並且可以配置透明度設定。

選擇 **透明度** 以在優化PDF文檔時配置透明度設定。

**透明度級別** 指定將保留的向量資訊量。 較高的設定保留了更多的向量對象，而較低的設定柵格化了更多的向量對象；中間設定以向量形式保留簡單區域，並柵格化複雜區域。 選擇最低設定以柵格化所有圖稿。

>[!NOTE]
>
>發生的光柵化量取決於頁面的複雜性和重疊對象的類型。

**線條藝術和文本** 將所有對象（包括影像、向量圖稿、文本和漸變）柵格化到的解析度。 支援的值為1像素/英吋(ppi)到9600 ppi。

>[!NOTE]
>
>線條藝術和文本解析度通常應設定為600-1200 ppi，以提供高質量光柵化，特別是在襯線或小點尺寸類型上。

**漸變和網格** 漸變和網格柵格化到的解析度。 支援的值為1 ppi到1200 ppi。

>[!NOTE]
>
>漸變和網格解析度通常應設定為150-300 ppi，因為漸變、陰影和羽毛的質量不會隨著解析度的提高而改善，但打印時間和檔案大小會增加。

**將所有文本轉換為輪廓** 將所有類型對象（點類型、區域類型和路徑類型）轉換為輪廓並丟棄包含透明度的頁面上的所有類型字形資訊。 此選項可確保文本寬度在拼合期間保持一致。 請注意，啟用此選項將導致小字型在Acrobat查看或在低解析度案頭打印機上打印時略顯粗。 它不會影響打印在高解析度打印機或成像機上的類型的質量。

**將所有描邊轉換為輪廓** 將包含透明度的頁面上的所有筆觸轉換為簡單填充路徑。 此選項可確保拼合期間筆畫的寬度保持一致。 請注意，啟用此選項會使細描邊顯得稍粗，並可能降低拼合效能。

**剪輯複雜區域** 確保向量圖稿和柵格化圖稿之間的邊界沿對象路徑下落。 此選項可減少在日誌的一部分時導致的拼接工件

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>某些打印驅動程式會以不同方式處理光柵和向量圖，有時會導致顏色拼接。 通過禁用某些打印驅動程式特定的顏色管理設定，您可能能夠最大限度地減少拼接問題。 這些設定因每台打印機而異，因此請參閱打印機附帶的文檔以瞭解詳細資訊。

保留疊印：將透明圖稿的顏色與背景顏色混合以建立疊印效果。

下表顯示了常用類型的打印機及其解析度（以dpi表示）、其預設螢幕定界(以行/英吋(lpi)表示)，以及以像素/英吋(ppi)表示的影像的重採樣解析度。 例如，如果要打印到600 dpi雷射打印機，則輸入170作為重新取樣影像的解析度。

**影像** 選擇「影像」以為彩色、灰度和單色影像指定壓縮和重採樣選項。 您可能希望嘗試使用這些選項來在檔案大小和影像質量之間找到適當的平衡。彩色和灰度影像的解析度設定應是打印檔案的線屏規則的1.5到2倍。 單色影像的解析度應與輸出設備相同，但請注意，以高於1500 dpi的解析度保存單色影像會增大檔案大小，而不會顯著提高影像質量。 將被放大的影像，例如地圖，可能需要更高的解析度。

>[!NOTE]
>
>重新取樣單色影像可能會產生意外的查看結果，例如沒有影像顯示。 如果發生這種情況，請關閉重新取樣並再次轉換檔案。 這個問題最可能發生在亞採樣中，而最不可能發生在雙三次採樣中。

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
   <td><p>85 LPI</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 dpi（照排機）</p> </td>
   <td><p>120 LPI</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi（照排機）</p> </td>
   <td><p>150 LPI</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

#### 放棄對象 {#discard-objects}

* 選擇 **放棄對象** 指定要從PDF中移除的對象，並優化CAD繪圖中的曲線。
* **放棄所有表單提交、導入和重置操作**:禁用與提交或導入表單資料相關的所有操作，並重置表單域。 此選項保留操作連結到的窗體對象。
* **放棄所有JavaScript操作**:從PDF中刪除使用JavaScript的任何操作。
* **放棄嵌入的頁面縮略圖**:刪除嵌入的頁面縮略圖。 此選項對於大型文檔非常有用，在按一下「頁面」按鈕後，可能需要很長時間才能繪製頁面縮略圖。
* **將平滑線轉換為曲線**:減少在CAD繪圖中用於生成曲線的控制點數，這樣可以減少PDF檔案，並加快螢幕繪製。
* **放棄嵌入式打印設定**:從文檔中刪除嵌入的打印設定，如頁面縮放和雙工模式。
* **放棄書籤**:從文檔中刪除所有書籤。
* **拼合表單域**:使表單域不能使用，而其外觀不會更改。 表單資料與頁面合併，以成為頁面內容。
* **放棄所有備用映像**:刪除映像的所有版本，但目標是在螢幕上查看的版本除外。 某些PDF包括同一影像的多個版本，用於不同目的，例如低解析度的螢幕觀看和高解析度打印。
* **放棄文檔標籤**:從文檔中刪除標籤，這也會刪除文本的輔助功能和重排功能。
* **檢測和合併影像片段**:查找碎片化為薄切片並嘗試將切片合併為單個影像或蒙版的影像或蒙版。
* **放棄嵌入式搜索索引**:刪除嵌入的搜索索引，從而減小檔案大小。

#### 放棄用戶資料 {#discard-user-data}

選擇 **放棄用戶資料** 刪除不想與其他用戶分發或共用的任何個人資訊。

* **放棄所有評論、Forms和多媒體**:從PDF中刪除所有注釋、表單、表單域和多媒體。
* **放棄所有對象資料**:從PDF中刪除所有對象。
* **放棄外部交叉引用**:刪除指向其他文檔的連結。 跳到PDF中其他位置的連結不會刪除。
* **放棄隱藏圖層內容並平整可見圖層**:減小檔案大小。 優化的文檔看起來像原始PDF，但不包含圖層資訊。
* **放棄文檔資訊和元資料**:刪除文檔資訊字典和所有元資料流中的資訊。 (使用「另存為」命令將元資料流還原到PDF的副本。)
* **放棄檔案附件**:刪除所有檔案附件，包括作為注釋添加到PDF的附件。 (PDF優化程式不優化附加檔案。)
* **丟棄其他應用程式的專用資料**:從PDF文檔中刪除僅對建立文檔的應用程式有用的資訊。 此設定不影響PDF的功能，但會減小檔案大小。

### 清除 {#clean-up}

選擇 **清除** 從文檔中刪除不必要的項目。
這些項目包括過時或對文檔的預定用途不必要的元素。 刪除某些元素會嚴重影響PDF的功能。 預設情況下，只選擇不影響功能的元素。 如果您不確定刪除其他選項的含義，請使用預設選擇。

**壓縮**

從下拉菜單中選擇以下「Flate compression（過濾壓縮）」選項之一：

* 壓縮整個檔案
* 壓縮文檔結構
* 刪除壓縮
* 保持壓縮不變

**使用flate對未編碼的流進行編碼**:將Flate壓縮應用於所有未編碼的流。

**放棄無效書籤**:刪除指向文檔中已刪除頁面的書籤。

**放棄未引用的命名目標**:從PDF文檔中刪除未在內部引用的命名目標。 此選項不檢查其他PDF檔案或網站的連結。

**優化快速Web視圖的PDF**:重新構建PDF文檔，以便從Web伺服器進行每次頁面下載（位元組服務）。

**在使用LZW編碼的流中，請改用flate**:對使用LZW編碼的所有內容流和影像應用Flate壓縮。

**放棄無效連結**:刪除跳至無效目標的連結。

**優化頁面內容**:將所有行尾字元轉換為空格字元，從而改進Flate壓縮。

## MicrosoftExcel設定（僅限Windows） {#microsoft-excel-settings-windows-only}

這些選項確定如何轉換MicrosoftExcel檔案。 有關訪問這些選項的說明，請參見 [建立或編輯檔案類型設定](#create-or-edit-file-type-settings)。

**嘗試OpenOffice作為回退轉換器**:當選擇此選項且使用MicrosoftExcel的轉換失敗或達到指定的超時限制時，PDF生成器會嘗試使用OpenOffice進行轉換。 如果使用OpenOffice的轉換失敗或達到指定的超時限制，則會向日誌檔案中寫入異常。

**檔案副檔名**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設為 `xls,xlsx`。不包括擴展之前的句點或擴展之間的空格。

**建立PDF/A-1a相容檔案**:強制使用PDF/A-1b:2005RGBAdobe PDF設定。

**將書籤添加到Adobe PDF**:將Excel工作表名稱轉換為書籤。 預設情況下，此選項處於選中狀態。

**將工作表調整為單頁**:減少文本大小以適合單頁上的工作表。

**轉換整個工作簿**:轉換Excel檔案中的所有工作表。 如果未選擇此選項，則僅轉換當前頁。

**自動運行宏**:在轉換文檔之前，在Excel文檔中運行任何宏（如插入當前時間的宏）。

**轉換文檔資訊**:根據源檔案中的文檔資訊添加PDF文檔屬性。 這包括文檔標題、作者、主題和關鍵字等資訊。

**添加到Adobe PDF的連結**:將源檔案中的超連結轉換為PDF文檔中的超連結。

**將源檔案附加到Adobe PDF**:選擇此選項後，原始Excel電子錶格將作為附件插入生成的PDF文檔中。

**啟用輔助功能和帶有標籤的Reflow**:在PDF文檔中嵌入標籤，以啟用輔助功能和重排。

**要載入的Excel載入項清單**:預設情況下（出於安全原因），當Excel檔案轉換為PDF時，不會運行Excel載入項。 要允許某些Excel載入項在轉換期間運行，請提供以逗號分隔的載入項名稱清單。

**要轉換的工作表清單**:當此框為空時，Excel電子錶格中的所有工作表都包括在生成的PDF中。 要有選擇地轉換工作表的子集，請提供以逗號分隔的工作表名稱清單。

## MicrosoftPowerPoint設定（僅限Windows） {#microsoft-powerpoint-settings-windows-only}

這些選項確定如何轉換MicrosoftPowerPoint檔案。 有關訪問這些選項的說明，請參見 [建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings)。

**[!UICONTROL 嘗試OpenOffice作為回退轉換器]**:當選擇此選項且使用MicrosoftPowerPoint的轉換失敗或達到指定的超時限制時，PDF生成器會嘗試使用OpenOffice進行轉換。 如果使用OpenOffice的轉換失敗或達到指定的超時限制，則會向日誌檔案中寫入異常。

**[!UICONTROL 檔案副檔名]**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設值為ppt,pptx。 不包括擴展之前的句點或擴展之間的空格。

**[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框中添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設情況下，此選項處於選中狀態。

**[!UICONTROL 將書籤添加到Adobe PDF]**:將PowerPoint標題轉換為書籤。 預設情況下，此選項處於選中狀態。

**[!UICONTROL 將源檔案附加到Adobe PDF]**:將源檔案作為附件添加到PDF檔案。 預設情況下，此選項處於取消選中狀態。

**[!UICONTROL 啟用輔助功能和帶有標籤的Reflow]**:將標籤嵌入到PDF檔案中。 預設情況下，此選項處於取消選中狀態。

**[!UICONTROL 將多媒體轉換為PDF多媒體]**:盡可能將多媒體轉換為PDF多媒體。 預設情況下，此選項處於選中狀態。

**[!UICONTROL 轉換揚聲器備注]**:將揚聲器備注轉換為PDF。

**[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行PowerPoint文檔中的任何宏（如插入當前時間的宏）。

**[!UICONTROL 基於PowerPoint打印機設定的PDF佈局]**:使用PowerPoint打印機設定來佈局PDF文檔。

**[!UICONTROL 添加到Adobe PDF的連結]**:轉換檔案時保留現有連結。 連結的外觀一般保持不變。 僅當同時選擇了「啟用輔助功能」選項時，才能建立連結。 預設情況下，此選項處於取消選中狀態。

**[!UICONTROL 保存Adobe PDF的幻燈片過渡]**:轉換幻燈片過渡。 預設情況下，此選項處於選中狀態。

**[!UICONTROL 在Adobe PDF保存動畫]**:將轉換的動畫保存在PDF檔案中。

**[!UICONTROL 將隱藏幻燈片轉換為PDF頁]**:轉換隱藏幻燈片。

**[!UICONTROL 建立PDF/A-1a相容檔案]**:強制使用PDF/A-1b:2005RGBAdobe PDF設定。 生成PDF檔案時，不會轉換一些PowerPoint功能。 如果PowerPoint過渡在Acrobat沒有等效過渡，則替換類似過渡。 如果多個動畫效果位於同一幻燈片中，則使用單個效果。 轉換頁面過渡和項目符號飛行。

## Microsoft項目設定（僅限Windows） {#microsoft-project-settings-windows-only}

這些選項確定如何轉換Microsoft項目檔案。 有關訪問這些選項的說明，請參見 [建立或編輯檔案類型設定](#create-or-edit-file-type-settings)。

1. **[!UICONTROL 檔案副檔名：]** 指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設為 `mpp`。不包括擴展之前的句點或擴展之間的空格。

1. **[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框中添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設情況下，此選項處於選中狀態。
1. **[!UICONTROL 將源檔案附加到Adobe PDF]**:將源檔案作為附件添加到PDF檔案。
1. **[!UICONTROL 建立PDF/A-1a相容檔案]**:強制使用PDF/A-1b:2005RGBAdobe PDF設定。
1. **[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行Microsoft項目文檔中的任何宏（如插入當前時間的宏）。

## MicrosoftWord設定（僅限Windows） {#microsoft-word-settings-windows-only}

這些選項確定如何轉換MicrosoftWord檔案。 有關訪問這些選項的說明，請參見 [建立或編輯檔案類型設定](#create-or-edit-file-type-settings)。

**[!UICONTROL 嘗試OpenOffice作為回退轉換器]**:當選擇此選項且使用MicrosoftWord的轉換失敗或達到指定的超時限制時，PDF生成器會嘗試使用OpenOffice進行轉換。 如果使用OpenOffice的轉換失敗或達到指定的超時限制，則會向日誌檔案中寫入異常。

**[!UICONTROL 檔案副檔名]**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設為 `doc,docx,rtf,txt`。不包括擴展之前的句點或擴展之間的空格。

**[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框中添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設情況下，此選項處於選中狀態。

**[!UICONTROL 將書籤添加到Adobe PDF]**:將標題轉換為書籤。 預設情況下，此選項處於選中狀態。

**[!UICONTROL 將源檔案附加到Adobe PDF]**:將源檔案作為附件添加到PDF檔案。

**[!UICONTROL 將交叉引用和目錄轉換為連結]**:將所有交叉引用和目錄條目轉換為連結。 預設情況下，此選項處於選中狀態。

**[!UICONTROL 啟用輔助功能和帶有標籤的Reflow]**:將標籤嵌入到PDF檔案中。 預設情況下，此選項處於選中狀態。

**[!UICONTROL 建立PDF/A-1a相容檔案]**:如果選中，則強制使用PDF/A-1b:2005RGBAdobe PDF設定。

**[!UICONTROL 自動運行宏]**:在轉換文檔之前，運行Word文檔中的任何宏（如插入當前時間的宏）。

**[!UICONTROL 保留Adobe PDF中的文檔標籤]**:將Word文檔中的標籤轉換為PDF檔案中的注釋。

**[!UICONTROL 添加到Adobe PDF的連結]**:將源檔案中的超連結轉換為PDF文檔中的超連結。

**[!UICONTROL 轉換腳注和章節附註連結]**:從腳注和章節附註引用建立連結到PDF文檔中的注釋。

**[!UICONTROL 在Adobe PDF將顯示的注釋轉換為注釋]**:將Word文檔中的注釋轉換為PDF文檔中的文本注釋。

**[!UICONTROL 啟用高級標籤]**:添加高級標籤以增強輔助功能。

**[!UICONTROL 將所有樣式轉換為書籤]**:將Word文檔中的所有樣式轉換為PDF文檔中的書籤。

**[!UICONTROL 帶級別的樣式]**:指定Word文檔中哪些樣式將轉換為PDF文檔中的書籤。 還指定書籤的級別。 要使用此功能，請取消選擇 **[!UICONTROL 將所有樣式轉換為書籤]** 選項，並按以下格式指定樣式名稱：

styleName1=level1[,styleName2=level2...]

如果MicrosoftWord樣式名稱包含逗號(,)或等號(=)，請在特殊字元前加轉義字元(&quot;\_)。 例如，將名為「標題， 1」的樣式指定為標題\, 1。

## MicrosoftVisio設定（僅限Windows） {#visio}

**轉換文檔資訊**:從源檔案的「屬性」對話框中添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設情況下，此選項處於選中狀態。 預設情況下，此選項處於啟用狀態。

**添加到Adobe PDF的連結**:保留所有連結。 預設情況下，此選項處於選中狀態。

**將書籤添加到Adobe PDF**:將標題轉換為書籤。 預設情況下，此選項處於選中狀態。

**將源檔案附加到Adobe PDF**:將源檔案作為附件添加到PDF檔案。

**在Adobe PDF始終平整圖層**:拼合所有Visio圖層。

**轉換所有頁面**:轉換Visio檔案的所有頁面。

**在Adobe Acrobat查看時開啟圖層面板**:如果Visio圖層未平展，則開啟一個窗口，在該窗口中可以指定當使用Acrobat開啟時保留在PDF檔案中的圖層。 預設情況下，此選項處於選中狀態。

**建立PDF/A-1b相容檔案**:強制使用Adobe PDF設定PDF/A-1b:2005(RGB)。

**將注釋轉換為Adobe PDF注釋**:將Visio備注轉換為PDF備注。

## Microsoft發佈者設定（僅限Windows） {#microsoft-publisher-settings-windows-only}

這些選項確定如何轉換Microsoft發佈器檔案。 有關訪問這些選項的說明，請參見 [建立或編輯檔案類型設定](#create-or-edit-file-type-settings)。

**[!UICONTROL 檔案副檔名]**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設為 `pub`。不包括擴展之前的句點或擴展之間的空格。

## AutoCAD設定（僅限Windows） {#autocad-settings-windows-only}

這些選項確定如何轉換AutoCAD檔案。 有關訪問這些選項的說明，請參見 [建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings)。

**[!UICONTROL 檔案副檔名]**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設為 `dwg`。不包括擴展之前的句點或擴展之間的空格。

**[!UICONTROL 轉換文檔資訊]**:從源檔案的「屬性」對話框中添加文檔資訊，包括標題、主題、作者、關鍵字、經理、公司、類別和注釋。 預設情況下，此選項處於選中狀態。

**[!UICONTROL 將書籤添加到Adobe PDF]**:將標題轉換為書籤。

**[!UICONTROL 在Adobe PDF始終平整圖層]**:拼合所有AutoCAD層。

**[!UICONTROL 在Adobe Acrobat查看時開啟圖層窗格]**:顯示PDF在Acrobat開啟時的層結構。

**[!UICONTROL 建立PDF/E-1相容檔案]**:建立符合PDF/E-1的檔案。 PDF/E是交換工程和技術文檔的ISO標準。 有關PDF/E-1的詳細資訊，請參見 [Adobe和行業標準](https://www.adobe.com/enterprise/standards/index.html)。

**[!UICONTROL 轉換所有佈局]**:包括PDF中的所有佈局。

**[!UICONTROL 將模型空間轉換為3D]**:選中後，模型空間佈局將轉換為PDF中的3D注釋。

**[!UICONTROL 添加到Adobe PDF的連結]**:如果選中，則保留所有連結。

**[!UICONTROL 將源檔案附加到Adobe PDF]**:將源檔案作為附件添加到PDF檔案。

**[!UICONTROL 建立PDF/A-1b相容檔案]**:強制使用PDF/A-1bAdobe PDF設定。

**[!UICONTROL 轉換所有圖層]**:預設情況下，「PDF生成器」(AutoCAD Generator)僅將AutoCAD檔案的預設層轉換為PDF，而不是將檔案中的所有層轉換為。 選擇此選項可轉換檔案的所有層。

**[!UICONTROL 嵌入比例資訊]**:保留繪圖比例資訊。

**[!UICONTROL 轉換當前佈局]**:僅包括PDF中的當前佈局。

**[!UICONTROL 要轉換的AutoCAD佈局清單]**:AutoCAD繪圖可具有多個佈局。 當此框為空時，AutoCAD繪圖中的所有佈局都包括在生成的PDF文檔中。 要選擇性地轉換佈局的子集，請提供以逗號分隔的佈局名稱清單。

## OpenOffice設定 {#openoffice-settings}

這些選項確定如何轉換OpenOffice檔案。 有關訪問這些選項的說明，請參見 [建立或編輯檔案類型設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings)。

**嘗試PDFMaker作為回退轉換器**:當選擇此選項且使用OpenOffice的轉換失敗或達到指定的超時限制時，PDF生成器會嘗試使用PDFMaker進行轉換。 如果使用PDFMaker的轉換失敗或達到指定的超時限制，則會將異常寫入日誌檔案。

**檔案副檔名**:指定此應用程式接受的檔案類型的檔案副檔名（以逗號分隔）。 預設為 `odt,odp,ods,odg,odf,sxw,sxi,sxd`。不包括擴展之前的句點或擴展之間的空格。

**範圍**:轉換所有頁面或指定特定頁面或頁面範圍。 如果未定義頁面範圍，則轉換所有頁面。 要導出一系列頁面，請使用3-6格式。 要導出單頁，請使用格式7;9;11。 可以使用3-6;8;10;12等格式導出頁面範圍和單個頁面的組合。

**頁面方向**:僅對純文字檔案檔案，請為轉換的PDF文檔選擇縱向或橫向。

**影像**:配置轉換影像的方式。 帶有嵌入預覽的EPS影像僅作為預覽導出。 沒有嵌入預覽的EPS影像會導出為空佔位符。 利用影像的無損壓縮，將保留所有像素。 由於影像的JPEG壓縮和高質量級別，幾乎所有像素都得到保留。 在低質量級別下，某些像素會丟失並引入偽像，但檔案大小會減少。

**常規**:啟用選項以轉換帶標籤的PDF，或將Writer和FormCalc文檔注釋、Impress幻燈片轉換效果或空白頁導出到PDF。 導出標籤時，檔案大小可能會大幅增加。 導出的某些標籤是目錄、超連結和控制項。

您還可以指定表單的提交方式。 選項為XML、FDF、PDF或HTML。 此設定將覆蓋在文檔中設定的控制項的URL屬性。 只能為PDF文檔選擇一個公用設定：

* PDF（發送整個文檔）
* FDF（發送控制內容）
* HTML
* XML

**標籤PDF**:允許從OpenOffice文檔建立帶標籤的PDF。 標籤PDF包含有關文檔內容結構的資訊。 在具有不同螢幕的設備上顯示文檔以及使用螢幕閱讀器軟體時，這會有所幫助。 它還幫助輔助輔助軟體對PDF文檔執行各種有用的操作，例如朗讀PDF文檔的內容。

**導出注釋**:將OpenOffice文檔中的注釋轉換為生成的PDF文檔中的注釋。

**使用過渡效果**:將OpenOffice演示文稿中的幻燈片轉換效果轉換為相應的PDF轉換效果。

**以格式提交Forms**:建立PDF表單，該表單可由PDF文檔的用戶填寫和打印。

**導出自動插入的空白頁**:選中此選項後，自動插入的空白頁面將包括在生成的PDF文檔中。 如果要雙面打印PDF文檔，則此功能非常有用。 例如，可以配置書籍，以便章節的第一頁始終在奇數頁上開始。 如果上一章在奇數頁上結束，OpenOffice將插入一個空偶數頁。 此選項控制是否在生成的PDF中包含該偶數頁。

## 其他應用程式設定（僅限Windows） {#other-applications-settings-windows-only}

不能通過管理控制台更改其他應用程式的設定；它們顯示支援的檔案類型的檔案副檔名。 有關訪問這些設定的說明，請參見 [建立或編輯檔案類型設定](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html)。

* Corel WordPerfect: `wpd`
* AdobePageMaker: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

可能需要自定義對這些檔案類型的支援。 有關詳細資訊，請參閱中的「添加對其他本機檔案格式的支援」 [用表格編AEM程](https://www.adobe.com/go/learn_aemforms_programming_62)。

有關配置PDFG網路打印機的幫助，請參見 [設定PDFG網路打印機（僅限Windows）](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md)。
