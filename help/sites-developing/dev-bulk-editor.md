---
title: 開發大量編輯器
seo-title: Developing the Bulk Editor
description: 標籤可讓內容分類和組織
seo-description: Tagging allows content to be categorized and organized
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 2%

---

# 開發大量編輯器{#developing-the-bulk-editor}

本節說明如何開發大量編輯器工具，以及如何擴充以大量編輯器為基礎的產品清單元件。

## 大量編輯器查詢參數 {#bulk-editor-query-parameters}

使用大量編輯器時，有數個查詢參數可新增至URL，以使用特定設定呼叫大量編輯器。 如果您希望批量編輯器始終與特定配置一起使用（例如在「產品清單」元件中），則需要修改bulkeditor.jsp（位於/libs/wcm/core/components/bulkeditor中）或建立具有特定配置的元件。 使用查詢參數所做的變更不是永久性的。

例如，如果您在瀏覽器的URL中輸入下列內容：

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

大量編輯器顯示時未顯示 **根路徑** 欄位(hrp=true)會隱藏欄位。 參數hrp=false時，會顯示欄位（預設值）。

以下是批量編輯器查詢參數的清單：

>[!NOTE]
>
>每個參數都可以有長名和短名。 例如，搜索根路徑的長名稱為 `rootPath`，短的是 `rp`. 如果未定義長名稱，則會從請求讀取短名稱。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> 參數</p> <p>（長名/短名）<br /> </p> </td>
   <td> 類型 <br /> </td>
   <td> 說明 <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> 字串 </td>
   <td> 搜尋根路徑</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> 字串</td>
   <td> 搜尋查詢</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> 布林值</td>
   <td> 若為true，則會啟用內容模式<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> 字串[]</td>
   <td> 搜索的屬性（選中的colsSelection中的值顯示為複選框）</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> 字串[]</td>
   <td> 搜尋的額外屬性（以逗號分隔的文字欄位顯示）</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> 布林值</td>
   <td> 若為true，則會在頁面載入時執行查詢<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> 字串[]</td>
   <td> 搜索的屬性選擇（顯示為複選框）</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> 布林值</td>
   <td> 若為true，則只顯示網格，而不顯示搜索面板 <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollaped / spc</td>
   <td> 布林值</td>
   <td> 為true時，載入時會收合搜尋面板</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> 布林值</td>
   <td> 若為true，則隱藏根路徑欄位</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> 布林值</td>
   <td> 若為true，則隱藏查詢欄位</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> 布林值</td>
   <td> 若為true，則會隱藏內容模式欄位</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> 布林值</td>
   <td> 若為true，則隱藏「欄選取」欄位</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> 布林值</td>
   <td> 若為true，則會隱藏額外的欄位</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> 布林值</td>
   <td> 若為true，則隱藏搜尋按鈕</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> 布林值</td>
   <td> 若為true，則會隱藏「儲存」按鈕</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> 布林值</td>
   <td> 若為true，則會隱藏匯出按鈕</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> 布林值</td>
   <td> 若為true，則會隱藏匯入按鈕</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> 布林值</td>
   <td> 若為true，則隱藏網格搜索結果編號文本</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> 布林值</td>
   <td> 為true時，隱藏網格插入按鈕</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> 布林值</td>
   <td> true時，隱藏網格刪除按鈕</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> 布林值</td>
   <td> 若為true，則會隱藏格線「path」欄</td>
  </tr>
 </tbody>
</table>

### 開發基於批量編輯器的元件：產品清單元件 {#developing-a-bulk-editor-based-component-the-product-list-component}

本節概述如何使用大量編輯器，並根據大量編輯器說明現有的Geometrixx元件：產品清單元件。

產品清單元件可讓使用者顯示和編輯資料表。 例如，您可以使用產品清單元件來表示目錄中的產品。 資訊會在標準HTML表中顯示，而任何編輯都會在 **編輯** 對話框，其中包含BulkEditor介面工具集。 (此大量編輯器與可從/etc/importers/bulkeditor.html或「工具」功能表存取的編輯器完全相同)。 產品清單元件已針對特定、有限的大量編輯器功能進行設定。 批量編輯器的每個部分（或從批量編輯器派生的元件）都可以配置。

使用批量編輯器，您可以新增、修改、刪除、篩選和匯出列、儲存修改和匯入一組列。 每一行都儲存為「產品清單」元件實例本身下的節點。 每個儲存格都是每個節點的屬性。 這是一種設計選擇，可以輕鬆更改，例如，您可以將節點儲存在儲存庫中的其他位置。 查詢servlet的角色是返回要顯示的節點清單；搜索路徑定義為「產品清單」實例。

產品清單元件的原始碼可在/apps/geometrixx/components/productlist存放庫中取得，且由多個部分組成，如所有AEM元件：

* HTML呈現：渲染在JSP檔案(/apps/geometrixx/components/productlist/productlist.jsp)中完成。 JSP讀取當前產品清單元件的子節點，並將每個子節點顯示為HTML表的行。
* 編輯對話方塊，您可在此定義批量編輯器配置。 設定對話方塊以符合元件的需求：列在網格或搜索上執行的可用操作和可能操作。 請參閱 [批量編輯器配置屬性](#bulk-editor-configuration-properties) 以取得所有設定屬性的資訊。

以下是對話子節點的XML表示：

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### 批量編輯器配置屬性 {#bulk-editor-configuration-properties}

批量編輯器的每個部分都可進行配置。 下表列出批量編輯器的所有配置屬性。

<table>
 <tbody>
  <tr>
   <td>屬性名稱</td>
   <td>定義</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>搜索根路徑</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>搜尋查詢</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>啟用內容模式為true:屬性在jcr:content節點上讀取，而非在搜尋結果節點上讀取</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>搜索的屬性（colsSelection中的選定值顯示為複選框）</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>搜尋的額外屬性（以文字欄位逗號分隔顯示）</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>若要在頁面載入上執行查詢，則為True</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>搜索的屬性選擇（顯示為複選框）</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>為True ，只顯示格線而不顯示搜尋面板（請別忘記將initialSearch設為true）</td>
  </tr>
  <tr>
   <td>searchPanelCollaped</td>
   <td>預設折疊搜索面板為True</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>隱藏根路徑欄位</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>隱藏查詢欄位</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>隱藏內容模式欄位</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>隱藏協定選擇欄位</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>隱藏額外的cols欄位</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>隱藏搜索按鈕</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>隱藏保存按鈕</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>隱藏導出按鈕</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>隱藏導入按鈕</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>隱藏網格搜索結果編號文本</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>隱藏網格插入按鈕</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>隱藏網格刪除按鈕</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>隱藏網格「路徑」列</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>查詢Servlet的路徑</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>匯出servlet的路徑</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>匯入servlet的路徑</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>插入行時添加到節點的資源類型</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>儲存按鈕Widget設定</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>搜尋按鈕Widget設定</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>匯出按鈕Widget設定</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>匯入按鈕Widget設定</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>搜尋面板Widget設定</td>
  </tr>
  <tr>
   <td>網格</td>
   <td>格線介面工具集配置</td>
  </tr>
  <tr>
   <td>商店</td>
   <td>儲存設定</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>網格列模型配置</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>rootPath widget設定</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>queryParams widget設定</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>contentMode widget設定</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>colsSelection widget配置</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>extraCols widget設定</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>欄中繼資料設定。 可能的屬性包括（應用於列的所有單元格）: <br />
    <ul>
     <li>cellStyle:html樣式 </li>
     <li>cellCls:css類 </li>
     <li>readOnly:為true，而無法變更值 </li>
     <li>核取方塊：true ，將欄的所有儲存格定義為核取方塊（true/false值） </li>
     <li>forcedPosition:要指定列必須置於網格中的位置的整數值（介於0和列數之間）<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 欄中繼資料設定 {#columns-metadata-configuration}

您可以為每欄進行設定：

* 顯示屬性：html樣式、CSS類和只讀

* 核取方塊
* 強迫職位

CSS和唯讀欄

批量編輯器有三列配置：

* 單元格CSS類名(cellCls):新增至已設定欄之每個儲存格的CSS類別名稱。
* 單元格樣式(cellStyle):HTML樣式，會新增至已設定欄的每個儲存格。
* 只讀（只讀）:為已配置列的每個單元格設定只讀。

設定必須定義為下列設定：

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

您可在productlist元件(/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata)中找到下列範例：

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**核取方塊**

如果核取方塊配置屬性設為true，則列的所有儲存格都會呈現為核取方塊。 核取方塊會傳送 **true** 儲存servlet, **false** 否則。 在頁首功能表中，您也可以 **全部選擇** 或 **選擇無**. 如果所選標題是複選框列的標題，則啟用這些選項。

在前一個範例中，選取欄僅包含核取方塊，作為核取方塊=&quot;true&quot;。

**強迫位置**

強制位置元資料forcedPosition可讓您指定欄在格線中的位置：0是第一位，而 &lt;number of=&quot;&quot; columns=&quot;&quot;>-1是最後一個位置。 任何其他值會受到忽略。

在前一個範例中，選取欄是forcedPosition=&quot;0&quot;的第一欄。

### 查詢Servlet {#query-servlet}

依預設，查詢Servlet可在 `/libs/wcm/core/components/bulkeditor/json.java`. 您可以設定其他路徑以擷取資料。

查詢Servlet的運作方式如下：它會接收GQL查詢並傳回欄、計算結果，並將結果以JSON資料流的形式傳回至大量編輯器。

在產品清單元件案例中，傳送至查詢servlet的兩個參數如下：

* 查詢：&quot;path:/content/geometrixx/en/customers/jcr:content/par/productlist Cube&quot;
* cols:&quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

而傳回的JSON資料流如下：

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

每個點擊都對應一個節點及其屬性，並在格線中顯示為一列。

您可以擴展查詢Servlet以返回複雜的繼承模型或返回儲存在特定邏輯位置的節點。 查詢Servlet可用於執行任何類型的複雜計算。 然後，網格可顯示儲存庫中多個節點的聚合行。 在這種情況下，這些行的修改和保存必須由「保存Servlet」管理。

### 儲存Servlet {#save-servlet}

在批量編輯器的預設配置中，每行都是一個節點，該節點的路徑儲存在行記錄中。 批量編輯器會透過jcr路徑保留列與節點之間的連結。 當使用者編輯格線時，會建立所有修改的清單。 使用者點按 **儲存**，則會將POST查詢傳送至具有更新屬性值的每個路徑。 這是Sling概念的基礎，如果每個儲存格都是節點的屬性，就可正常運作。 但是，如果實現查詢Servlet以進行繼承計算，則此模型不能作為查詢Servlet返回的屬性從另一個節點繼承。

「儲存servlet」概念是修改不會直接張貼至每個節點，而是張貼至執行儲存作業的一個servlet。 這可讓此servlet分析修改並將屬性儲存在正確節點上。

每個更新的屬性都會以下列格式傳送至servlet:

* 參數名稱： &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

   範例：/content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* 值： &lt;value>

   例如: 12123

Servlet需要知道catalogCode屬性的儲存位置。

預設的「儲存Servlet」實作可在/libs/wcm/bulkeditor/save/POST.jsp取得，且用於「產品清單」元件。 會採用請求中的所有參數(搭配 &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> 格式)，並使用JCR API在節點上寫入屬性。 如果節點不存在（網格插入的行），它也會建立節點。

預設程式碼不應如原樣使用，因為它會重新實作伺服器原生功能(上的POST &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>)，因此只是建立將管理屬性繼承模型的儲存servlet的好起點。
