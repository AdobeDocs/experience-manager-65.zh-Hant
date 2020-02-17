---
title: 開發批量編輯器
seo-title: 開發批量編輯器
description: 標籤可讓內容分類並組織
seo-description: 標籤可讓內容分類並組織
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 開發批量編輯器{#developing-the-bulk-editor}

本節介紹如何開發批量編輯器工具以及如何擴展基於批量編輯器的產品清單元件。

## 批量編輯器查詢參數 {#bulk-editor-query-parameters}

使用批量編輯器時，有幾個查詢參數可以添加到URL中，以使用特定配置調用批量編輯器。 如果您希望批量編輯器始終與特定配置（例如，在「產品清單」元件中）一起使用，則需要修改bulkeditor.jsp（位於/libs/wcm/core/components/bulkeditor中）或建立具有特定配置的元件。 使用查詢參數進行的更改不是永久的。

例如，如果您在瀏覽器的URL中鍵入以下內容：

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

批量編輯器顯示時不 **帶根路徑欄位** ，因為hrp=true會隱藏該欄位。 參數hrp=false時，會顯示欄位（預設值）。

以下是批量編輯器查詢參數的清單：

>[!NOTE]
>
>每個參數都可以有長名和短名。 例如，搜索根路徑的長名稱是 `rootPath`，短名稱是 `rp`。 如果未定義長名稱，則從請求中讀取短名稱。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> 參數</p> <p>（長名／短名）<br /> </p> </td>
   <td> 類型 <br /> </td>
   <td> 說明 <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> 字串 </td>
   <td> 搜索根路徑</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> 字串</td>
   <td> 搜索查詢</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> 布林值 (Boolean)</td>
   <td> 若為true，則內容模式會啟用<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> String[]</td>
   <td> 已搜索屬性（colsSelection中的選定值顯示為複選框）</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> String[]</td>
   <td> 額外搜尋的屬性（顯示在逗號分隔的文字欄位中）</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，會在頁面載入時執行查詢<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> String[]</td>
   <td> 搜索屬性選擇（顯示為複選框）</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> 布林值 (Boolean)</td>
   <td> 若為true，則只顯示格線，而不顯示搜尋面板 <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> 布林值 (Boolean)</td>
   <td> 若為true，則載入時搜尋面板會收合</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏根路徑欄位</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏查詢欄位</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> 布林值 (Boolean)</td>
   <td> 若為true，則隱藏內容模式欄位</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏列選擇欄位</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏多餘的列欄位</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏搜尋按鈕</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏保存按鈕</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏匯出按鈕</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏匯入按鈕</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏網格搜索結果編號文本</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏網格插入按鈕</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏網格刪除按鈕</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> 布林值 (Boolean)</td>
   <td> 當為true時，隱藏格線「路徑」欄</td>
  </tr>
 </tbody>
</table>

### 開發基於批量編輯器的元件：產品清單元件 {#developing-a-bulk-editor-based-component-the-product-list-component}

本節概述如何使用批量編輯器，並說明現有的Geometrixx元件（以批量編輯器為基礎）:產品清單元件。

「產品清單」元件可讓使用者顯示和編輯資料表。 例如，您可以使用「產品清單」元件來表示目錄中的產品。 這些資訊會顯示在標準HTML表格中，而任何編輯都會在「編輯」對話方塊中執行，而 **「編輯** 」對話方塊中包含BulkEditor介面工具集。 (此批量編輯器與可從/etc/importers/bulkeditor.html或「工具」功能表存取的編輯器完全相同)。 產品清單元件已針對特定、有限的大量編輯器功能進行設定。 批量編輯器的每個部分（或從批量編輯器派生的元件）都可以配置。

使用批量編輯器，您可以添加、修改、刪除、篩選和導出行、保存修改和導入行集。 每一行都儲存為「產品清單」元件實例本身下的節點。 每個單元格都是每個節點的屬性。 這是一種設計選擇，可以輕鬆更改，例如，您可以將節點儲存在儲存庫中的其他位置。 查詢servlet的角色是返回要顯示的節點清單；搜索路徑被定義為「產品清單」實例。

「產品清單」元件的原始碼可在/apps/geometrixx/components/productlist儲存庫中取用，並由多個部分（例如所有AEM元件）組成：

* HTML轉換：演算是在JSP檔案(/apps/geometrixx/components/productlist/productlist.jsp)中完成。 JSP讀取當前產品清單元件的子節點，並將每個子節點顯示為HTML表的行。
* 「編輯」對話框，在該對話框中定義批量編輯器配置。 設定對話方塊以符合元件的需求：欄和可能在網格或搜索上執行的操作。 有關 [所有配置屬性的資訊](#bulk-editor-configuration-properties) ，請參見批量編輯器配置屬性。

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

批量編輯器的每個部分都可以配置。 下表列出了批量編輯器的所有配置屬性。

<table>
 <tbody>
  <tr>
   <td>屬性名稱</td>
   <td>定義</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>搜尋根路徑</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>搜尋查詢</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>啟用內容模式為true:屬性在jcr:content節點上讀取，在搜索結果節點上不讀取</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>已搜尋的屬性（colsSelection中的核取值顯示為核取方塊）</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>額外搜尋的屬性（以逗號分隔的文字欄位顯示）</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>True可在頁面載入時執行查詢</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>搜尋的屬性選擇（顯示為核取方塊）</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True：只顯示格線而不顯示搜尋面板（請勿忘記將initialSearch設為true）</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>預設為True可收合搜尋面板</td>
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
   <td>隱藏選取欄位</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>隱藏額外的cols欄位</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>隱藏搜尋按鈕</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>隱藏儲存按鈕</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>隱藏匯出按鈕</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>隱藏匯入按鈕</td>
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
   <td>隱藏格線「路徑」欄</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>查詢servlet的路徑</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>導出servlet的路徑</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>導入servlet的路徑</td>
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
   <td>匯入按鈕介面工具集設定</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>搜尋面板Widget設定</td>
  </tr>
  <tr>
   <td>網格</td>
   <td>格線介面工具集設定</td>
  </tr>
  <tr>
   <td>商店</td>
   <td>商店設定</td>
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
   <td>queryParams Widget設定</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>contentMode widget設定</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>colsSelection Widget設定</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>extraCols widget設定</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>欄中繼資料設定。 可能的屬性是（套用至欄的所有儲存格）: <br />
    <ul>
     <li>cellStyle:html樣式 </li>
     <li>cellCls:css類 </li>
     <li>readOnly:true to not beaching value </li>
     <li>複選框：true：將列的所有單元格定義為複選框（true/false值） </li>
     <li>forcedPosition:整數值，以指定欄必須置於格線中的位置（介於0和欄數-1之間）<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 欄中繼資料設定 {#columns-metadata-configuration}

您可以為每個欄設定：

* 顯示屬性：html樣式、CSS類別和唯讀

* 複選框
* 強迫職位

CSS和唯讀欄

批量編輯器有三種列配置：

* 儲存格CSS類別名稱(cellCls):添加到已配置列的每個單元格的CSS類名。
* 儲存格樣式(cellStyle):HTML樣式，會新增至已設定欄的每個儲存格。
* 唯讀（唯讀）:為已配置列的每個單元格設定只讀。

配置必須定義為以下配置：

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

以下範例可在產品清單元件(/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata)中找到：

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

如果複選框配置屬性設定為true，則列的所有單元格都將顯示為複選框。 複選框將 **true** 發送到伺服器Save servlet，否 **則為** false。 在頁首功能表中，您也可以選 **取全部** ，或 **選取無**。 如果選定的標題是複選框列的標題，則會啟用這些選項。

在前面的示例中，選擇列只包含複選框作為checkbox=&quot;true&quot;。

**強迫位置**

強制位置中繼資料forcedPosition可讓您指定欄在格線中的位置：0是第一位，&lt;number of columns>-1是最後一位。 會忽略任何其他值。

在前例中，選擇欄是forcedPosition=&quot;0&quot;的第一欄。

### 查詢Servlet {#query-servlet}

預設情況下，可在中找到查詢Servlet `/libs/wcm/core/components/bulkeditor/json.java`。 您可以設定另一個路徑來擷取資料。

查詢Servlet的工作方式如下：它會接收GQL查詢和要返回的列，計算結果，並將結果作為JSON流發送回批量編輯器。

在「產品清單」元件案例中，發送到Query Servlet的兩個參數如下：

* 查詢：&quot;path:/content/geometrixx/tw/customers/jcr:content/par/productlist Cube&quot;
* cols:&quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

而傳回的JSON串流如下：

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

每個點擊都對應一個節點及其屬性，並在網格中顯示為一行。

可以擴展查詢Servlet以返回複雜的繼承模型或返回儲存在特定邏輯位置的節點。 查詢Servlet可用於進行任何類型的複雜計算。 然後，網格可以顯示儲存庫中多個節點的聚合行。 在這種情況下，這些行的修改和保存必須由保存Servlet管理。

### 保存Servlet {#save-servlet}

在批量編輯器的預設配置中，每行都是一個節點，該節點的路徑儲存在行記錄中。 批量編輯器通過jcr路徑保留行和節點之間的連結。 當使用者編輯網格時，會建立所有修改的清單。 當使用者按一 **下「儲存**」時，POST查詢會以更新的屬性值傳送至每個路徑。 這是Sling概念的基礎，如果每個儲存格都是節點的屬性，則其運作良好。 但是，如果實現Query Servlet進行繼承計算，則此模型不能作為Query Servlet返回的屬性從另一個節點繼承。

「保存servlet」概念是，修改不直接發佈到每個節點，而是發佈到執行保存作業的一個servlet。 這使此servlet能夠分析修改並將屬性保存在正確的節點上。

每個更新的屬性都以下列格式發送到servlet:

* 參數名稱：&lt;jcr path>/&lt;property name>

   範例：/content/geometrixx/tw/products/jcr:content/par/productlist/1258674859000/SellingSku

* 值：&lt;value>

   例如: 12123

Servlet需要知道catalogCode屬性的儲存位置。

預設的Save servlet實施可在/libs/wcm/bulkeditor/save/POST.jsp上獲得，並用於「產品清單」元件。 它會從請求中取用所有參數（使用&lt;jcr path>/&lt;property name>格式），並使用JCR API在節點上寫入屬性。 如果節點不存在（網格插入的行），它也會建立節點。

預設代碼不應像重新實施伺服器本機操作那樣使用（&lt;jcr path>/&lt;property name>上的POST），因此，它只是構建將管理屬性繼承模型的保存Servlet的一個好起點。
