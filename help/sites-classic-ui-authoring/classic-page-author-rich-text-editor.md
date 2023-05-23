---
title: RTF 編輯器
description: 富格文本編輯器是用於將文本內容輸入的基本構造塊AEM。
uuid: 4bcce45a-e14f-41b7-8c6f-89d1e1bb595c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ccc0e434-8847-4e12-8a18-84b55fb2964b
docset: aem65
exl-id: 5623dcf4-bda9-4dee-ace3-5a1f6057e96c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 1%

---

# RTF 編輯器 {#rich-text-editor}

富格文本編輯器是用於將文本內容輸入的基本構造塊AEM。 它構成了各個組成部分的基礎，包括：

* 文字
* 文字影像
* 表格

## RTF 編輯器 {#rich-text-editor-1}

WYSIWYG編輯對話框提供了多種功能：

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>可用功能可針對單個項目進行配置，因此安裝時可能會有所不同。

## 就地編輯 {#in-place-editing}

除了基於對話框的富格文本編輯模式AEM外，還提供了就地編輯模式，該模式允許在文本顯示在頁面佈局中時直接編輯文本。

在段落上按一下兩次（慢速按兩下）以進入就地編輯模式（元件邊框現在將變為橙色）。

您將能夠直接編輯頁面上的文本，而不是在對話框窗口內。 只需進行更改，即可自動保存。

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>如果開啟了內容查找器，則帶有RTE格式設定選項的工具欄將顯示在頁籤的頂部（如上所示）。
>
>如果內容查找器未開啟，則不會顯示工具欄。

當前，已為由 **文本** 和 **標題** 元件。

>[!NOTE]
>
>的 [!UICONTROL 標題] 元件設計為包含不帶換行符的短文本。 在「就地編輯」模式下編輯標題時，輸入換行符將開啟新標題 **文本** 下的元件。

## 富格文本編輯器的功能 {#features-of-the-rich-text-editor}

富格文本編輯器提供了一系列功能，這些功能 [取決於配置](/help/sites-administering/rich-text-editor.md) 的下界。 這些功能可用於觸摸優化和經典用戶介面。

### 基本字元格式 {#basic-character-formats}

![](do-not-localize/cq55_rte_basicchars.png)

在此，您可以將格式設定應用於選定（突出顯示）的字元；一些選項還有短鍵：

* 粗體(Ctrl-B)
* 斜體(Ctrl-I)
* 下划線(Ctrl-U)
* 下標
* 上標

![cq55_rte_basicchars_use](assets/cq55_rte_basicchars_use.png)

所有操作都以切換方式進行，因此重新選擇將刪除格式。

### 預定義樣式和格式 {#predefined-styles-and-formats}

![cq55_rte_stylesparaph](assets/cq55_rte_stylesparagraph.png)

您的安裝可包括預定義的樣式和格式。 這些可用於 **[!UICONTROL 樣式]** 和 **[!UICONTROL 格式]** 下拉清單，並可應用於您選擇的文本。

樣式可應用於特定字串（與CSS相關的樣式）:

![cq55_rte_styles_use](assets/cq55_rte_styles_use.png)

雖然格式應用於整個文本段落(格式基於HTML):

![cq55_rte_paragraph_use](assets/cq55_rte_paragraph_use.png)

只能更改特定格式(預設值為 **[!UICONTROL 段落]**)。

可以刪除樣式；將游標置於已應用樣式的文本中，然後按一下「刪除」表徵圖：

>[!CAUTION]
>
>不要實際重新選擇已應用樣式或表徵圖將被停用的任何文本。

### 剪切、複製、貼上 {#cut-copy-paste}

![](do-not-localize/cq55_rte_cutcopypaste.png)

標準函式 **[!UICONTROL 剪切]** 和 **[!UICONTROL 複製]** 的雙曲餘切值。 幾種 **[!UICONTROL 貼上]** 以迎合不同格式。

* 剪切(Ctrl-X)
* 複製(Ctrl-C)
* 貼上這是元件的預設貼上機制(Ctrl-V);當出廠時，此配置將 [!UICONTROL 從Word貼上]。

* 貼上為文本：刪除所有樣式和格式以僅貼上純文字檔案。

* 從Word貼上：此操作將內容貼上為HTML（帶有一些必要的重新格式化）。

### 撤消，重做 {#undo-redo}

![](do-not-localize/cq55_rte_undoredo.png)

AEM按時間順序保存當前元件中最後50個操作的記錄。 如果需要，這些操作可以嚴格按順序撤消（然後重做）。

>[!CAUTION]
>
>該歷史記錄僅保存為當前編輯會話。 每次開啟元件進行編輯時，都會重新啟動它。

>[!NOTE]
>
>50是預設的任務數。 這可能與您的安裝不同。

### 對齊方式 {#alignment}

![](do-not-localize/cq55_rte_alignment.png)

文本可以左對齊、居中對齊或右對齊。

![cq55_rte_alignment_use](assets/cq55_rte_alignment_use.png)

### 縮排 {#indentation}

![](do-not-localize/cq55_rte_indent.png)

可以增加或減少段落的縮進。 選定段落將進行縮進，輸入的任何新文本將保留當前縮進級別。

![cq55_rte_indent_use](assets/cq55_rte_indent_use.png)

### 清單 {#lists}

![](do-not-localize/cq55_rte_lists.png)

可以在文本中建立項目符號清單和編號清單。 選擇清單類型並開始鍵入或突出顯示要轉換的文本。 在這兩種情況下，行源都將啟動新清單項。

嵌套清單可通過縮進一個或多個清單項來實現。

只需將游標定位在清單中，然後選擇其它樣式，即可更改清單的樣式。 子清單也可具有與包含清單不同的樣式。 建立子清單後（通過縮排）即可應用此選項。

![cq55_rte_lists_use](assets/cq55_rte_lists_use.png)

### 連結 {#links}

![](do-not-localize/cq55_rte_links.png)

通過突出顯示所需文本，然後按一下超連結表徵圖，可生成指向URL的連結（位於網站或外部位置）:

![](do-not-localize/chlimage_1-9.png)

通過對話框可以指定目標URL;還有是否應該在新窗口中開啟。

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

您可以：

* 直接鍵入URI
* 使用網站圖選擇網站內的頁面
* 輸入URI，然後追加目標錨點；例如 `www.TargetUri.org#AnchorName`
* 僅輸入錨點（以引用「當前頁」）;比如說， `#anchor`
* 在內容查找器中搜索頁面，然後將頁面表徵圖拖放到「超連結」對話框中

>[!NOTE]
>
>URI可以優先於為安裝配置的任何協定。 在標準安裝中， `https://`。 `ftp://`, `mailto:`。 未為安裝配置的協定將被拒絕，並標籤為無效。

要斷開連結位置，請在連結文本中的任意位置按一下 [!UICONTROL 取消連結] 表徵圖：

![](do-not-localize/chlimage_1-10.png)

### 錨點 {#anchors}

![](do-not-localize/cq55_rte_anchor.png)

通過定位游標或選擇某些文本，可以在文本中的任意位置建立錨點。 然後按一下 **錨點** 表徵圖開啟對話框。

輸入錨點的名稱，然後按一下 **確定** 來保存。

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

在編輯元件時顯示錨點，現在可在目標內用於連結。

![chlimage_1-104](assets/chlimage_1-104.png)

### 查找和替換 {#find-and-replace}

![](do-not-localize/cq55_rte_findreplace.png)

AEM提供 **查找** 和 **替換** （查找和替換）函式。

都有 **查找下一個** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。 還可以指定是否需要匹配大小寫（上/下）。

搜索將始終從文本中的當前游標位置開始。 當到達元件的結尾時，將顯示一條消息，通知您下一個搜索操作將從頂部開始。

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

的 **替換** 選項 **查找**，則 **替換** 具有指定文本的單個實例，或 **全部替換** 當前元件中的實例。

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### 影像 {#images}

可以從內容查找器中拖動影像，以將其添加到文本中。

![cq55_rte_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>還提AEM供專用元件，用於更詳細的映像配置。 例如 **影像** 和 **文本影像** 元件可用。

### 拼寫檢查 {#spelling-checker}

![](do-not-localize/cq55_rte_spellchecker.png)

拼寫檢查器將檢查當前元件中的所有文本。

將突出顯示任何不正確的拼寫：

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>拼寫檢查器將通過獲取子樹的語言屬性或從URL中提取語言來使用網站的語言。 例如 `en` 分支將被檢查， `de` 德語分店。

### 表 {#tables}

兩個表均可用：

* 作為 **表格** 元件

   ![chlimage_1-105](assets/chlimage_1-105.png)

* 從 **文本** 元件

   ![](do-not-localize/chlimage_1-11.png)

   >[!NOTE]
   >
   >儘管RTE中提供了表，但建議使用 **表格** 元件。

在 **文本** 和 **表格** 元件表功能可通過在表內按一下的上下文菜單（通常是滑鼠右鍵）獲得；例如：

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>在 **表格** 此外，還可使用專用工具欄，包括各種標準的富格文本編輯器函式，以及表特定函式的子集。

表的特定函式包括：

* [表屬性](#table-properties)
* [單元格屬性](#cell-properties)
* [添加或刪除行](#add-or-delete-rows)
* [添加或刪除列](#add-or-delete-columns)
* [選擇整行或列](#selecting-entire-rows-or-columns)
* [合併單元格](#merge-cells)
* [分割儲存格](#split-cells)
* [嵌套表](#creating-nested-tables)
* [刪除表](#remove-table)

#### 表屬性 {#table-properties}

![cq55_rte_tableproperties_icon](assets/cq55_rte_tableproperties_icon.png)

在按一下 **確定** 保存：

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **寬度**:表的總寬度。

* **高度**:表的總高度。

* **邊框**:表邊框的大小。

* **單元格填充**:這將定義單元格內容與其邊框之間的空白。

* **單元格間距**:這定義了單元格之間的距離。

>[!NOTE]
>
>「寬度」和「高度」等少數單元格屬性可定義為像素或百分比。

>[!CAUTION]
>
>Adobe建議您為表定義寬度。

#### 單元格屬性 {#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

可以配置特定單元格或一系列單元格的屬性：

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **寬度**
* **高度**
* **水準對齊**  — 左、中或右
* **垂直對齊**  — 上、中、下或基線
* **單元格類型** — 資料或標題
* **應用於：** 單個單元格，整行，整列

#### 添加或刪除行 {#add-or-delete-rows}

![cq55_rte_rows](assets/cq55_rte_rows.png)

行可以在當前行的上方或下方添加。

也可以刪除當前行。

#### 添加或刪除列 {#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

列可以添加到當前列的左側或右側。

也可以刪除當前列。

#### 選擇整行或列 {#selecting-entire-rows-or-columns}

![chlimage_1-106](assets/chlimage_1-106.png)

選擇整個當前行或列。 然後可以使用特定操作（例如合併）。

#### 合併單元格 {#merge-cells}

![cq55_rte_cellmerge](assets/cq55_rte_cellmerge.png) ![cq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* 如果選擇了一組單元格，則可以將這些單元格合併為一個單元格。
* 如果只選擇了一個單元格，則可以將其與單元格合併到右側或下方。

#### 分割儲存格 {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

選擇單個單元格將其拆分：

* 水準拆分單元格將在當前列中生成當前單元格右側的新單元格。
* 垂直拆分單元格將在當前單元格下面生成新單元格，但在當前行內。

#### 建立嵌套表 {#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

建立嵌套表將在當前單元格中建立新的自包含表。

>[!NOTE]
>
>某些附加行為與瀏覽器相關：
>
>* Windows IE:使用Ctrl+主滑鼠按鈕按一下（通常向左）可選擇多個單元格。
>* Firefox:拖動指針以選擇單元格區域。


#### 刪除表 {#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

使用選項從 **[!UICONTROL 文本]** 元件。

### 特殊字元 {#special-characters}

![](do-not-localize/cq55_rte_specialchars.png)

您的富文本編輯器可以使用特殊字元；這些可能因安裝而異。

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

使用滑鼠可查看字元的放大版本，然後按一下滑鼠可將其包含在文本的當前位置。

### 源編輯模式 {#source-editing-mode}

![](do-not-localize/cq55_rte_sourceedit.png)

源編輯模式允許您查看和編輯元件的基礎HTML。

因此，文字是：

![cq55_rte_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

在源模式下，將如下所示（通常源較長，因此您必須滾動）:

![cq55_rte_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>離開源模式時，AEM會進行某些驗證檢查（例如，確保文本正確包含/嵌套在塊中）。 這可能導致對編輯內容進行更改。
