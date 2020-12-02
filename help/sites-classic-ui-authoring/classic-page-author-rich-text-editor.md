---
title: RTF 編輯器
description: Rich Text Editor是將文字內容輸入AEM的基本建置區塊。
uuid: 4bcce45a-e14f-41b7-8c6f-89d1e1bb595c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ccc0e434-8847-4e12-8a18-84b55fb2964b
docset: aem65
translation-type: tm+mt
source-git-commit: 7bf6657a8fd7677ab15e0f91324a065b684e2f92
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 1%

---


# RTF 編輯器 {#rich-text-editor}

Rich Text Editor是將文字內容輸入AEM的基本建置區塊。 它構成了各個組成部分的基礎，包括：

* 文字
* 文字影像
* 表格

## RTF 編輯器 {#rich-text-editor-1}

WYSIWYG編輯對話方塊提供多種功能：

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>可用的功能可針對個別專案進行設定，因此可能會因您的安裝而有所不同。

## 就地編輯{#in-place-editing}

除了以對話方塊為基礎的「豐富式文字編輯」模式外，AEM也提供就地編輯模式，可直接編輯顯示在頁面版面中的文字。

在段落上按兩下（慢速按兩下），以進入就地編輯模式（元件邊框現在為橙色）。

您可以直接編輯頁面上的文字，而不是在對話方塊視窗內。 只要進行變更，就會自動儲存。

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>如果開啟了內容查找器，則頁籤頂部將顯示一個帶有RTE格式設定選項的工具欄（如上所示）。
>
>如果內容搜尋器未開啟，工具列將不會顯示。

目前，「就地編輯」模式已針對&#x200B;**Text**&#x200B;和&#x200B;**Title**&#x200B;元件產生的頁面元素啟用。

>[!NOTE]
>
>[!UICONTROL Title]元件設計為包含沒有換行符的短文本。 在「就地編輯模式」中編輯標題時，輸入換行符將開啟標題下方的新&#x200B;**Text**&#x200B;元件。

## 富格文本編輯器的功能{#features-of-the-rich-text-editor}

Rich Text Editor提供一系列功能，這些[取決於個別元件的組態](/help/sites-administering/rich-text-editor.md)。 這些功能適用於最佳化觸控和傳統的UI。

### 基本字元格式{#basic-character-formats}

![](do-not-localize/cq55_rte_basicchars.png)

您可以在這裡將格式套用至選取（反白顯示）的字元；一些選項還有短鍵：

* 粗體(Ctrl-B)
* 斜體(Ctrl-I)
* 下划線(Ctrl-U)
* 下標
* 上標

![cq55_rte_basicchars_use](assets/cq55_rte_basicchars_use.png)

所有項目都會以切換方式運作，因此重新選取會移除格式。

### 預先定義的樣式和格式{#predefined-styles-and-formats}

![cq55_rte_stylesparagraph](assets/cq55_rte_stylesparagraph.png)

您的安裝可包含預先定義的樣式和格式。 這些選項可用於&#x200B;**[!UICONTROL Style]**&#x200B;和&#x200B;**[!UICONTROL Format]**&#x200B;下拉清單，並可應用於已選擇的文本。

樣式可套用至特定字串（與CSS相關的樣式）:

![cq55_rte_styles_use](assets/cq55_rte_styles_use.png)

雖然格式會套用至整個文欄位落（格式是以HTML為基礎的）:

![cq55_rte_paragraph_use](assets/cq55_rte_paragraph_use.png)

特定格式只能更改（預設值為&#x200B;**[!UICONTROL Paragraph]**）。

可以移除樣式；將游標置於已應用樣式的文本中，然後按一下刪除表徵圖：

>[!CAUTION]
>
>請勿實際重新選取已套用樣式或將停用圖示的任何文字。

### 剪下、複製、貼上{#cut-copy-paste}

![](do-not-localize/cq55_rte_cutcopypaste.png)

**[!UICONTROL Cut]**&#x200B;和&#x200B;**[!UICONTROL Copy]**&#x200B;的標準函式可用。 提供多種類型的&#x200B;**[!UICONTROL 糊狀]**&#x200B;以適應不同的格式。

* 剪下(Ctrl-X)
* 複製(Ctrl-C)
* 貼上
這是元件的預設貼上機制(Ctrl-V);當安裝在出廠時，此配置為從Word[!UICONTROL 貼上。]

* 貼上為文字：移除所有樣式和格式，只貼上純文字。

* 從Word貼上：這會將內容貼為HTML（含一些必要的重新格式化）。

### 撤消，重做{#undo-redo}

![](do-not-localize/cq55_rte_undoredo.png)

AEM會記錄您目前元件中最近50個動作的記錄，依時間順序保留。 如有需要，這些動作可以嚴格依序還原（然後重做）。

>[!CAUTION]
>
>歷史記錄僅保存在當前編輯會話中。 每次開啟要編輯的元件時，它都會重新啟動。

>[!NOTE]
>
>預設任務數為50。 這可能與您的安裝不同。

### 對齊方式 {#alignment}

![](do-not-localize/cq55_rte_alignment.png)

您的文字可以向左、向中或向右對齊。

![cq55_rte_alignment_use](assets/cq55_rte_alignment_use.png)

### 縮排 {#indentation}

![](do-not-localize/cq55_rte_indent.png)

段落的縮進可以增加或減少。 選定段落將進行縮進，所輸入的任何新文本都將保留當前縮進級別。

![cq55_rte_indent_use](assets/cq55_rte_indent_use.png)

### 清單 {#lists}

![](do-not-localize/cq55_rte_lists.png)

項目清單和編號清單都可在文字中建立。 選擇清單類型並開始鍵入或突出顯示要轉換的文本。 在這兩種情況下，行動態消息都會啟動新的清單項目。

嵌套清單可通過縮進一個或多個清單項來實現。

只要將游標放在清單中，然後選擇其他樣式，即可更改清單的樣式。 子清單也可以與包含清單具有不同的樣式。 建立子清單後（透過縮排），即可套用此項。

![cq55_rte_lists_use](assets/cq55_rte_lists_use.png)

### 連結 {#links}

![](do-not-localize/cq55_rte_links.png)

URL的連結（在您的網站或外部位置）是透過反白標示所需文字，然後按一下超連結圖示來產生：

![](do-not-localize/chlimage_1-9.png)

對話方塊可讓您指定目標URL;還有是否應在新視窗中開啟。

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

您可以：

* 直接輸入URI
* 使用網站地圖在您的網站中選取頁面
* 輸入URI，然後附加目標錨點；例如，`www.TargetUri.org#AnchorName`
* 僅輸入錨點（以參考「目前頁面」）;例如，`#anchor`
* 在內容搜尋器中搜尋頁面，然後將頁面圖示拖放至「超連結」對話方塊

>[!NOTE]
>
>URI可以前置任何為安裝配置的協定。 在標準安裝中，這些是`https://`、`ftp://`和`mailto:`。 為安裝配置的協定將被拒絕並標籤為無效。

要斷開連結位置游標在連結文本中的任意位置，然後按一下[!UICONTROL  Unlink]表徵圖：

![](do-not-localize/chlimage_1-10.png)

### 錨點 {#anchors}

![](do-not-localize/cq55_rte_anchor.png)

可以通過定位游標或選擇某些文本在文本中的任意位置建立錨點。 然後，按一下&#x200B;**錨點**&#x200B;表徵圖以開啟該對話框。

輸入錨點的名稱，然後按一下&#x200B;**OK**&#x200B;保存。

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

錨點會在編輯元件時顯示，現在可用於連結的目標中。

![chlimage_1-104](assets/chlimage_1-104.png)

### 查找並替換{#find-and-replace}

![](do-not-localize/cq55_rte_findreplace.png)

AEM提供&#x200B;**Find**&#x200B;和&#x200B;**Replace**(find and replace)函式。

兩者都有一個&#x200B;**「查找next**」按鈕，用於搜索開啟的元件以查找指定的文本。 您也可以指定是否需要比對大小寫（上／下）。

搜索始終從文本中當前游標位置開始。 當到達元件結尾時，會出現訊息通知您下一個搜尋作業將從頂端開始。

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

**Replace**&#x200B;選項允許您查找&#x200B;****，然後&#x200B;**以指定文本替換**&#x200B;單個實例，或&#x200B;**替換當前元件中的所有**&#x200B;實例。

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### 影像 {#images}

您可從內容搜尋器拖曳影像，將影像新增至文字。

![cq55_rte_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>AEM也提供專用元件，以取得更詳細的影像設定。 例如，**Image**&#x200B;和&#x200B;**Text Image**&#x200B;元件可用。

### 拼字檢查器{#spelling-checker}

![](do-not-localize/cq55_rte_spellchecker.png)

拼字檢查器將檢查當前元件中的所有文本。

會反白顯示任何不正確的拼字：

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>拼字檢查器將使用網站的語言操作，方法是獲取子樹的語言屬性或從URL中提取語言。 例如，`en`分支將被檢查為英文，而`de`分支則為德文。

### 表{#tables}

表格可供使用：

* 作為&#x200B;**Table**&#x200B;元件

   ![chlimage_1-105](assets/chlimage_1-105.png)

* 從&#x200B;**Text**&#x200B;元件內

   ![](do-not-localize/chlimage_1-11.png)

   >[!NOTE]
   >
   >雖然表在RTE中可用，但在建立表時建議使用&#x200B;**Table**&#x200B;元件。

在&#x200B;**Text**&#x200B;和&#x200B;**Table**&#x200B;元件表格功能中，都可透過表格中點按的內容功能表（通常是滑鼠右鍵）;例如：

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>在&#x200B;**Table**&#x200B;元件中，還有專用的工具欄，包括各種標準富格文本編輯器函式以及表特定函式的子集。

表格特定的函式包括：

* [表屬性](#table-properties)
* [儲存格屬性](#cell-properties)
* [添加或刪除行](#add-or-delete-rows)
* [添加或刪除列](#add-or-delete-columns)
* [選擇整個行或列](#selecting-entire-rows-or-columns)
* [合併儲存格](#merge-cells)
* [分割儲存格](#split-cells)
* [巢狀表格](#creating-nested-tables)
* [移除表格](#remove-table)

#### 表屬性{#table-properties}

![cq55_rte_tableproperties_icon](assets/cq55_rte_tableproperties_icon.png)

可以在按一下&#x200B;**OK**&#x200B;保存之前配置表的基本屬性：

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **寬度**:表的總寬度。

* **高度**:桌子的總高度。

* **邊框**:表格邊框的大小。

* **單元格間距**:這會定義儲存格內容與其邊框之間的空格。

* **儲存格間距**:這會定義儲存格之間的距離。

>[!NOTE]
>
>「寬度」和「高度」等少數儲存格屬性可定義為像素或百分比。

>[!CAUTION]
>
>Adobe建議您為表格定義寬度。

#### 單元格屬性{#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

可以配置特定單元格或一系列單元格的屬性：

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **寬度**
* **高度**
* **水準對齊** -左、中或右
* **垂直對齊** -頂部、中間、底部或基線
* **儲存格類型**-資料或標題
* **套用至：單** 一儲存格、整列、整欄

#### 添加或刪除行{#add-or-delete-rows}

![cq55_rte_rows](assets/cq55_rte_rows.png)

可在當前行的上方或下方添加行。

也可以刪除當前行。

#### 添加或刪除列{#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

欄可以新增至目前欄的左側或右側。

也可以刪除當前列。

#### 選擇整個行或列{#selecting-entire-rows-or-columns}

![chlimage_1-105](assets/chlimage_1-106.png)

選擇整個當前行或列。 然後可使用特定動作（例如合併）。

#### 合併儲存格{#merge-cells}

![cq55_rte_](assets/cq55_rte_cellmerge.png) ![cellmergecq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* 如果您已選取一組儲存格，您可將這些儲存格合併為一。
* 如果您只選取一個儲存格，則可將它與儲存格合併至右側或下方。

#### 分割儲存格 {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

選取單一儲存格來分割：

* 水準分割儲存格會在目前欄內，在目前儲存格的右側產生新儲存格。
* 垂直分割儲存格會在目前儲存格下方，但在目前列內產生新儲存格。

#### 建立嵌套表{#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

建立巢狀表格會在目前儲存格中建立新的自含表格。

>[!NOTE]
>
>某些其他行為與瀏覽器相關：
>
>* Windows IE:使用Ctrl+primary-mouse-button-click（通常為左側）來選取多個儲存格。
>* Firefox:拖曳指標以選取儲存格範圍。


#### 刪除表{#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

使用選項從&#x200B;**[!UICONTROL Text]**&#x200B;元件中刪除表。

### 特殊字元 {#special-characters}

![](do-not-localize/cq55_rte_specialchars.png)

您的豐富式文字編輯器可以使用特殊字元；這些視您的安裝而定。

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

使用滑鼠移至檢視字元的放大版本，然後按一下以將其包含在文字的目前位置。

### 源編輯模式{#source-editing-mode}

![](do-not-localize/cq55_rte_sourceedit.png)

來源編輯模式可讓您查看和編輯元件的基礎HTML。

因此，文字：

![cq55_rte_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

在源模式下，Will的外觀如下（通常源模式比較長，因此您必須滾動）:

![cq55_rte_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>離開來源模式時，AEM會進行某些驗證檢查（例如，確保文字正確包含／巢狀內嵌在區塊中）。 這會導致您的編輯變更。
