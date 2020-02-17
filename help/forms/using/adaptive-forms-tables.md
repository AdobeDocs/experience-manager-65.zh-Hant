---
title: 最適化表格
seo-title: 最適化表格
description: AEM Forms中的Table元件可讓您在可回應行動版面的最適化表單中建立表格，也允許使用XDP表格元件。
seo-description: AEM Forms中的Table元件可讓您在可回應行動版面的最適化表單中建立表格，也允許使用XDP表格元件。
uuid: 03436c81-42f0-430f-9e52-14a4ab0e877d
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc418da9-496f-4a2b-bfe4-2add3ac4f468
docset: aem65
translation-type: tm+mt
source-git-commit: d12d35bf8355d3069071523427a7794b88c09b13

---


# 最適化表格{#tables-in-adaptive-forms}

使用表格是呈現複雜資料的有效、簡化且有組織的方式。 它幫助用戶輕鬆地識別資訊並以行和列的有序排列提供輸入。 金融服務和政府機構的大多數表格都需要大型資料表，才能填入數字並執行計算。

AEM Forms在元件瀏覽器的邊欄中提供「表格」元件，可讓您在最適化表格中建立表格。 它提供的一些關鍵功能包括：

* 行動裝置上的互動式版面
* 可配置的行和列
* 在執行時期動態新增和刪除列
* 合併或合併及分割儲存格
* 螢幕閱讀程式可存取
* 使用CSS自訂版面
* 與XDP表元件相容並映射
* 支援使用XSD複雜類型元素新增列或儲存格
* 從XML檔案合併資料

## 建立表 {#create-a-table}

若要建立表格，請從最適化表單的sidekick中，從元件瀏覽器拖放表格元件。 依預設，表格包含兩欄和三列，包括標題列。

![AEM側欄中的表格元件](assets/sidebar-tables.png)

### 關於標題和內文儲存格 {#about-header-and-body-cells}

標題儲存格是文字欄位。 若要變更頁首的標籤，請在頁首儲存格上按一下滑鼠右鍵，然後按一下「編 **輯」**。 在「編輯」對話方塊中，更新「值」欄位中的標 **簽** ，然後按一下「 **確定」**。

依預設，內文儲存格是文字方塊。 您可以使用sidekick中可用的任何其他最適化表單元件來取代主體儲存格，例如數值方塊、日期選擇器或下拉式清單。

例如，下表中的第一個內文列包含文字方塊、日期選擇器和下拉式清單元件做為儲存格。

![行——單元格類型](assets/row-cell-types.png)

通過選擇要合併的單元格，按一下右鍵並選擇合併，可以合併兩個或多個主體單元 **格**。 此外，您也可以將合併的儲存格分割，方法是按一下滑鼠右鍵並選取「分割 **儲存格」**。

### 添加、刪除、移動行和列 {#add-delete-move-rows-and-columns}

您可以新增和刪除行或列，以及在表格中上下移動行。

要添加或刪除行或列或移動行，請按一下行或列中的任何單元格。 下拉式功能表會出現在欄的頂端和列的左側。 頂部的菜單提供添加或刪除列的選項，而左側的菜單允許添加、刪除或移動行。

* 「添加」操作將在選定行或列的右側添加一行或列。
* 「刪除」操作將刪除選定的行或列。
* 「上移和下移」操作將上移和下移選定行。

行的下拉菜單還提供了「編輯」操作，以編輯行屬性、設定和樣式選項。

![add-delete-move-row-column](assets/add-delete-move-row-column.png)

>[!NOTE]
>
>雖然您可以在表格中新增任意數量的列，但可新增的欄數上限為6。 此外，您也無法從表格中刪除標題列。

### 添加表說明 {#add-table-description}

您可以新增表格說明如何組織資訊，讓螢幕閱讀程式解譯及讀出。 要添加說明：

1. 選取表格並點選 ![cmppr](assets/cmppr.png) ，在側欄中查看其屬性。
1. 在「協助工具」標籤中指定摘要。
1. 按一 **下完成**。

### 對表中的列進行排序 {#sortcolumnstable}

您可以根據表格中任何欄在最適化表單中排序資料。 列中的值可以按升序或降序排序。

排序可套用至包含：

* 靜態文字
* 資料模型對象屬性
* 靜態文字與資料模型物件屬性的組合

要對表列應用排序，表列單元格必須包含以下任何元件：數值方塊、數值步進器、日期輸入欄位、日期選擇器、文字或文字方塊。

要啟用排序：

1. 選取表格並點選 ![](assets/configure_icon.png) （設定）。 您也可以使用互動式通訊的側 **邊** ，使用內容瀏覽器選取表格。
1. 選擇 **啟用排序**。
1. 點選 ![](assets/done_icon.png) 以儲存表格屬性。 欄標題中的排序圖示（向上和向下箭頭）表示已啟用排序。

   ![啟用排序](assets/enable_sorting_new.png)

1. 切換至「 **預覽** 」模式以檢視輸出。 表格會根據表格的第一欄自動排序。
1. 按一下欄標題，以根據欄排序值。

   帶有向上箭頭的列標題表示表基於該列進行排序。 此外，欄中的值會以升序顯示。

   ![按升序排序](assets/sorting_ascending_new.png)

   同樣地，帶有向下箭頭的列標題表示列中的值以降序顯示。

   您也可以在「預覽」模式中對表格進行變 **更** ，然後再按一下欄標題，以排序欄值。

## 配置表樣式 {#configure}

可使用頁面工具欄中的「樣式」(Style)模式定義表的樣式。 執行以下步驟以切換到樣式模式並編輯表樣式

1. 在頁面工具列的「預覽」之前，點 ![選畫布下拉式清單](assets/canvas-drop-down.png) > **樣式**。

1. 在側欄中，選取表格並點選編輯按鈕 ![edit-button](assets/edit-button.png)。
您可以在側欄中看到樣式屬性。

![表的樣式屬性](assets/style-table.png)

>[!NOTE]
>
>您可以變更LESS變數的值，以變更標題列和內文列的色彩主題。 如需詳細資訊，請參 [閱「AEM Forms中的主題](/help/forms/using/themes.md) 」 [](/help/forms/using/creating-custom-adaptive-form-themes.md)。

## 動態新增或刪除列 {#add-or-delete-a-row-dynamically}

表格提供立即可用的支援，可在執行時期動態新增或刪除列。

1. 選取表格列並點選 ![cmppr](assets/cmppr.png)。
1. 在「重複設定」索引標籤中，指定表格中限制列數的最小和最大計數。
1. 按一 **下完成**。

在執行時期，您會看到 **+***和-* -按鈕來新增或刪除列。

![add-delete-rows-dynamically](assets/add-delete-rows-dynamically.png)

>[!NOTE]
>
>表格左側行動版面的「標題」不支援動態新增或刪除列。

## 表中的表達式 {#expressions-in-a-table}

使用最適化表單的表格，您可以在JavaScript中編寫運算式來引發行為，例如顯示或隱藏表格或列、加總所有數字並顯示儲存格中的總數、啟用或停用儲存格、驗證使用者輸入等。 這些運算式使用最適化表單指令碼模型API。

雖然表和行僅支援可見性表達式，以便根據表達式返回的值控制其可見性，但單元格支援以下表達式：

* **** 初始化指令碼：以對欄位的初始化執行操作。
* **** 值提交指令碼：變更欄位值後的表單元件。

>[!NOTE]
>
>如果XFA變更／退出指令碼也套用至相同欄位，XFA變更／退出指令碼會在「值提交」指令碼之前執行。

* **計算表達式**:自動計算欄位的值。
* **驗證運算式**:來驗證欄位。
* **存取運算式**:啟用／停用欄位。
* **可見度運算式**:以控制欄位和面板的可見度。

表或行的可見性表達式可在其對應的「編輯」元件對話框的「面板屬性」(Panel properties)頁籤中定義。 儲存格的運算式可在其「編輯」元件對話方塊的「指令碼」索引標籤中定義。

如需最適化表單類別、事件、物件和公用API的完整清單，請參閱適 [化表單的JavaScript程式庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/index.html)。

## 行動版面 {#mobile-layouts}

自適應表單的表格提供無與倫比的體驗行動裝置，因為它的版面流暢且回應速度快。 AEM Forms為表格提供兩種行動版面——左側的標題和可收合的欄。

您可以從表格的「編輯」元件對話方塊的「樣式」索引標籤，為表格設定行動版面。

### Headers on left {#headers-on-left}

在左側版面的「標題」中，表格中的標題會在左側轉置，只有一個儲存格會出現在標題上。 此版面中的每一行都會以不同區段顯示。 以下影像會比較桌上型電腦和行動裝置上的表格。

![案頭檢視](assets/desktopview_new.png)

左側版面具有標題的表格案頭檢視

![左側的標題](assets/headersontheleft_new.png)

左側版面具有標題的表格的行動檢視

### 可收合的欄位版面 {#collapsible-columns-layout}

在「可折疊」欄版面中，表格中的欄會收合，以顯示一或兩欄（視裝置大小而定），而其他欄則會收合。 可以按一下折疊／展開表徵圖來查看表格中的其他列。

**注意**:雖然「可收合」欄版面已針對行動裝置最佳化，但如果可用的寬度不足以顯示表格中的所有欄位，則也可在桌上型電腦上運作。

以下影像會比較表格在具有收合和展開欄的裝置上的外觀。

![collabess-column](assets/collapsed-column.png)

表格的收合欄，行動裝置上只顯示兩欄

![collable_column](assets/collapsible_column.png)

行動裝置上表格的擴充欄

## 合併表格中的資料 {#merge-data-in-a-table}

使用可調式表單中的表格，您可以在執行時期使用XML檔案的資料填入表格。 資料XML檔案可以駐留在執行AEM Forms伺服器的機器的本機檔案系統或CRX儲存庫中。

讓我們舉下列銀行交易摘要表為例，其中我們要填入XML檔案中的資料。

![資料合併表](assets/data-merge-table.png)

在此示例中，Element name屬性用於：

* 行是 **Row1**
* 事務日期下的正文單元格 **是tableItem1**
* 「說明」(Description)下的主體儲存格 **為tableItem2**
* 「事務類型」(Transaction type)下的主體單元格為 **類型**
* 「以USD表示的金額」下方的內文儲存格 **是tableItem3**

包含下列格式資料的XML檔案：

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
 <typeSelect>0</typeSelect>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Purchase laptop</tableItem2>
      <type>0</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Transport expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-01-08</tableItem1>
      <tableItem2>Laser printer</tableItem2>
      <type>0</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-12-08</tableItem1>
      <tableItem2>Credit card payment</tableItem2>
      <type>0</type>
      <tableItem3>300</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-06</tableItem1>
      <tableItem2>Interest earnings</tableItem2>
      <type>1</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Payment from a client</tableItem2>
      <type>1</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Food expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 </data>
  </afUnboundData>
  <afBoundData>
    <data/>
  </afBoundData>
  <afBoundData/>
</afData>
```

在示例XML中，行的資料由標籤定義，該標籤是表 `<Row1>` 中行的元素名稱。 在標籤 `<Row1>` 中，每個儲存格的資料都會在標籤中定義其元素名稱， `<tableItem1>``<tableItem2>`例如、 `<tableItem3>`和 `<type>`。

要在運行時將這些資料與表合併，我們需要將包含表的自適應表單指向禁用wcmmode的絕對XML位置。 例如，如果最適化表單位於 *https://localhost:4502/myForms/bankTransaction.html* ，而資料XML檔案儲存在 *C:/myTransactions/bankSummary.xml*，則可以在下列URL中檢視含有資料的表格：

*https://localhost:4502/myForms/bankTransaction.html?dataRef=file:/// C:/myTransactions/bankSummary.xml&amp;wcmmode=disabled*

![資料——合併表](assets/data-merged-table.png)

## 使用XDP元件和XSD複雜類型 {#use-xdp-components-and-xsd-complex-types}

如果您根據XFA表單範本建立最適化表單，XFA元素可在AEM Content Finder的「資料模型」索引標籤中使用。 您可以以最適化形式拖放這些XFA元素，包括表格。

XFA表元素會映射至Table元件，並在最適化表單中立即使用。 XDP表的所有屬性和功能在移動到自適應表單時都會保留，而且您可以像使用本地自適應表單表一樣對其執行任何操作。 例如，如果XDP表中的行被標籤為可重複，則在自適應表單中刪除時也會重複該行。

此外，還可以拖放XDP子表單，在表中添加新行。 不過，請注意，刪除巢狀子表單並不有效。

>[!NOTE]
>
>沒有標題行的XDP表將不映射到自適應表單表元件。 它會改為以流暢的版面對應至最適化表單面板元件。 此外，當從XDP將嵌套表添加到自適應表單時，外表將轉換為面板，同時保留內表。

此外，您還可以拖放一組XSD複雜類型元素以建立表格列。 在您放置元素的列正下方建立新列。 使用XSD複雜類型元素建立的儲存格會維護XSD的系結參考。 您也可以將元素拖放至儲存格，以XSD複雜類型元素取代主體儲存格。

>[!NOTE]
>
>XDP表元件、子表單或XSD複雜類型中的元素數不能超過一行中的單元格數。 例如，您不能將四個元素拖放到只有三個儲存格的列上。 這會導致錯誤。
>
>如果元素數少於一列中的儲存格數，新列會先根據元素新增儲存格，然後新增預設儲存格以填入該列中其餘的儲存格。 例如，如果您將三個元素群組拖放至含有四個儲存格的列中，前三個儲存格會以您所放置的元素為基礎，其餘一個儲存格將是預設表格儲存格。

## 主要考量事項 {#key-considerations}

* 如果您在製作以XSD為基礎的表格時上下移動列，表格列中會出現一些資料遺失的情況，會顯示在提交表格時產生的資料XML中。
* 預設表中的每個主體單元格都具有與其相關聯的預定義元素名稱。 如果在最適化表單中添加另一個表，則新表中的預設主體單元格將具有與第一個表中相同的元素名稱。 在這種情況下，提交表單時產生的資料將僅包含其中一個表格的預設內文儲存格中的資料。 因此，請確保更名預設主體單元格的元素名稱，以使它們在各表中保持唯一，並避免資料丟失。

   請注意，這僅適用於預設的內文儲存格。 如果向表中添加更多行或列，將自動為非預設主體單元格生成唯一的元素名稱。

