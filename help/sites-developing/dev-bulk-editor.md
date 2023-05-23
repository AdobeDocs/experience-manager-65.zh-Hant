---
title: 開發批量編輯器
seo-title: Developing the Bulk Editor
description: 標籤允許對內容進行分類和組織
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

# 開發批量編輯器{#developing-the-bulk-editor}

本節介紹如何開發批量編輯器工具以及如何擴展基於批量編輯器的「產品清單」元件。

## 批量編輯器查詢參數 {#bulk-editor-query-parameters}

使用批量編輯器時，可以向URL添加多個查詢參數，以使用特定配置調用批量編輯器。 如果希望批量編輯器始終與特定配置一起使用，則需要修改bulkeditor.jsp（位於/libs/wcm/core/components/bulkeditor中）或建立具有特定配置的元件。 使用查詢參數所做的更改不是永久的。

例如，如果在瀏覽器的URL中鍵入以下內容：

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

顯示批量編輯器，但 **根路徑** 欄位as hrp=true隱藏該欄位。 當參數hrp=false時，將顯示欄位（預設值）。

以下是批量編輯器查詢參數的清單：

>[!NOTE]
>
>每個參數都可以有長名和短名。 例如，搜索根路徑的長名稱為 `rootPath`，短的是 `rp`。 如果未定義長名稱，則從請求中讀取短名稱。

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
   <td> 根路徑/ rp<br /> </td>
   <td> 字串 </td>
   <td> 搜索根路徑</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> 字串</td>
   <td> 搜索查詢</td>
  </tr>
  <tr>
   <td> 內容模式/公分<br /> </td>
   <td> 布林值</td>
   <td> 如果為true，則啟用內容模式<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> 字串[]</td>
   <td> 搜索的屬性（cols中的選中值顯示為複選框的選擇）</td>
  </tr>
  <tr>
   <td> extraCols/ec<br /> </td>
   <td> 字串[]</td>
   <td> 額外搜索的屬性（顯示在逗號分隔的文本欄位中）</td>
  </tr>
  <tr>
   <td> 初始搜索/是<br /> </td>
   <td> 布林值</td>
   <td> 如果為true，則在頁面載入時執行查詢<br /> </td>
  </tr>
  <tr>
   <td> cols選擇/cs<br /> </td>
   <td> 字串[]</td>
   <td> 搜索屬性選擇（顯示為複選框）</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> 布林值</td>
   <td> 如果為true，則僅顯示網格而不顯示搜索面板 <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollaped / spc</td>
   <td> 布林值</td>
   <td> 如果為true，則在載入時折疊搜索面板</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏根路徑欄位</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏查詢欄位</td>
  </tr>
  <tr>
   <td> 隱藏內容模式/hcm</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏內容模式欄位</td>
  </tr>
  <tr>
   <td> 隱藏ColsSelection / hcs</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏列選擇欄位</td>
  </tr>
  <tr>
   <td> hideExtraCols/hec</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏附加列欄位</td>
  </tr>
  <tr>
   <td> 隱藏搜索按鈕</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏搜索按鈕</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏「保存」按鈕</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏導出按鈕</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏導入按鈕</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏網格搜索結果編號文本</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> 布林值</td>
   <td> 當為true時，隱藏網格插入按鈕</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> 布林值</td>
   <td> 當為true時，隱藏網格刪除按鈕</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> 布林值</td>
   <td> 如果為true，則隱藏網格「path」列</td>
  </tr>
 </tbody>
</table>

### 開發基於批量編輯器的元件：產品清單元件 {#developing-a-bulk-editor-based-component-the-product-list-component}

本節概述了如何使用批量編輯器，並基於批量編輯器對現有Geometrixx元件進行了說明：產品清單元件。

「產品清單」元件允許用戶顯示和編輯資料表。 例如，您可以使用「產品清單」元件來表示目錄中的產品。 該資訊在標準HTML表中顯示，任何編輯都在 **編輯** 對話框，其中包含BulkEditor小部件。 (此批量編輯器與/etc/importers/bulkeditor.html或通過「工具」菜單可訪問的編輯器完全相同)。 產品清單元件已針對特定的有限批量編輯器功能進行了配置。 可以配置批量編輯器的每個部分（或從批量編輯器派生的元件）。

使用批量編輯器，可以添加、修改、刪除、篩選和導出行、保存修改並導入一組行。 每行都作為節點儲存在「產品清單」元件實例本身下。 每個單元格是每個節點的屬性。 這是一種設計選擇，可以很容易地更改它，例如，您可以將節點儲存在儲存庫中的其他位置。 查詢servlet的作用是返回要顯示的節點清單；搜索路徑定義為「產品清單」實例。

「產品清單」元件的原始碼可在/apps/geometrixx/components/productlist的儲存庫中找到，它由幾個部件組成，如所有AEM元件：

* HTML呈現：渲染在JSP檔案(/apps/geometrixx/components/productlist/productlist.jsp)中完成。 JSP讀取當前「產品清單」元件的子節點，並將每個子節點顯示為HTML表的行。
* 「編輯」(Edit)對話框，在其中定義「批量編輯器」配置。 配置對話框以滿足元件的需要：列以及在網格或搜索中執行的可能操作。 請參閱 [批量編輯器配置屬性](#bulk-editor-configuration-properties) 的子菜單。

以下是對話框子節點的XML表示形式：

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

可以配置批量編輯器的每個部分。 下表列出了批量編輯器的所有配置屬性。

<table>
 <tbody>
  <tr>
   <td>屬性名稱</td>
   <td>定義</td>
  </tr>
  <tr>
   <td>根路徑</td>
   <td>搜索根路徑</td>
  </tr>
  <tr>
   <td>查詢參數</td>
   <td>搜尋查詢</td>
  </tr>
  <tr>
   <td>內容模式</td>
   <td>啟用內容模式為True:屬性在jcr:content節點上讀取，而不在搜索結果節點上讀取</td>
  </tr>
  <tr>
   <td>cols值</td>
   <td>搜索的屬性（cols中的選中值顯示為複選框的選擇）</td>
  </tr>
  <tr>
   <td>額外協定</td>
   <td>額外搜索的屬性（以文本欄位逗號分隔顯示）</td>
  </tr>
  <tr>
   <td>初始搜索</td>
   <td>為True，在頁載入時執行查詢</td>
  </tr>
  <tr>
   <td>cols選擇</td>
   <td>搜索的屬性選擇（顯示為複選框）</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True僅顯示網格而不顯示搜索面板（不要忘記將initialSearch設定為true）</td>
  </tr>
  <tr>
   <td>searchPanelCollaped</td>
   <td>預設情況下為True可折疊搜索面板</td>
  </tr>
  <tr>
   <td>隱藏根路徑</td>
   <td>隱藏根路徑欄位</td>
  </tr>
  <tr>
   <td>隱藏查詢參數</td>
   <td>隱藏查詢欄位</td>
  </tr>
  <tr>
   <td>隱藏內容模式</td>
   <td>隱藏內容模式欄位</td>
  </tr>
  <tr>
   <td>隱藏選擇</td>
   <td>隱藏列選擇欄位</td>
  </tr>
  <tr>
   <td>隱藏ExtraCols</td>
   <td>隱藏附加協定欄位</td>
  </tr>
  <tr>
   <td>隱藏搜索按鈕</td>
   <td>隱藏搜索按鈕</td>
  </tr>
  <tr>
   <td>隱藏保存按鈕</td>
   <td>隱藏保存按鈕</td>
  </tr>
  <tr>
   <td>隱藏導出按鈕</td>
   <td>隱藏導出按鈕</td>
  </tr>
  <tr>
   <td>隱藏導入按鈕</td>
   <td>隱藏導入按鈕</td>
  </tr>
  <tr>
   <td>隱藏結果編號</td>
   <td>隱藏網格搜索結果編號文本</td>
  </tr>
  <tr>
   <td>隱藏插入按鈕</td>
   <td>隱藏網格插入按鈕</td>
  </tr>
  <tr>
   <td>隱藏刪除按鈕</td>
   <td>隱藏網格刪除按鈕</td>
  </tr>
  <tr>
   <td>隱藏路徑列</td>
   <td>隱藏網格「路徑」列</td>
  </tr>
  <tr>
   <td>查詢URL</td>
   <td>查詢Servlet的路徑</td>
  </tr>
  <tr>
   <td>導出URL</td>
   <td>導出Servlet的路徑</td>
  </tr>
  <tr>
   <td>導入URL</td>
   <td>導入Servlet的路徑</td>
  </tr>
  <tr>
   <td>插入的資源類型</td>
   <td>插入行時添加到節點的資源類型</td>
  </tr>
  <tr>
   <td>保存按鈕</td>
   <td>保存按鈕小部件配置</td>
  </tr>
  <tr>
   <td>搜索按鈕</td>
   <td>搜索按鈕小部件配置</td>
  </tr>
  <tr>
   <td>導出按鈕</td>
   <td>導出按鈕小部件配置</td>
  </tr>
  <tr>
   <td>導入按鈕</td>
   <td>導入按鈕小部件配置</td>
  </tr>
  <tr>
   <td>搜索面板</td>
   <td>搜索面板小部件配置</td>
  </tr>
  <tr>
   <td>網格</td>
   <td>網格小部件配置</td>
  </tr>
  <tr>
   <td>商店</td>
   <td>儲存配置</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>網格列模型配置</td>
  </tr>
  <tr>
   <td>根路徑輸入</td>
   <td>根路徑小部件配置</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>queryParams小部件配置</td>
  </tr>
  <tr>
   <td>內容模式輸入</td>
   <td>內容模式小部件配置</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>colsSelection小部件配置</td>
  </tr>
  <tr>
   <td>額外Cols輸入</td>
   <td>extraCols小部件配置</td>
  </tr>
  <tr>
   <td>cols元資料</td>
   <td>列元資料配置。 可能的屬性（應用於列的所有單元格）: <br />
    <ul>
     <li>單元格樣式：html樣式 </li>
     <li>cellCls:css類 </li>
     <li>只讀：不能更改值 </li>
     <li>複選框：true，將列的所有單元格定義為複選框（true/false值） </li>
     <li>forcedPosition:用於指定列必須放在網格中的位置的整數值（介於0和列數–1之間）<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 列元資料配置 {#columns-metadata-configuration}

可以為每列配置：

* 顯示屬性：html樣式、CSS類和只讀

* 複選框
* 強迫的位置

CSS和只讀列

批量編輯器有三個列配置：

* 單元格CSS類名(cellCls):添加到已配置列的每個單元格的CSS類名。
* 單元格樣式(cellStyle):添加到已配置列的每個單元格的HTML樣式。
* 只讀（只讀）:為配置列的每個單元格設定只讀。

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

在productlist元件(/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata)中可以找到以下示例：

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

如果複選框配置屬性設定為true，則列的所有單元格將呈現為複選框。 複選框發送 **真** 保存Servlet, **假** 否則。 在標題菜單中，您還可以 **全選** 或 **選擇無**。 如果選定的標題是複選框列的標題，則會啟用這些選項。

在前例中，選擇列僅包含複選框，如checkbox=&quot;true&quot;。

**強制位置**

強制位置元資料forcedPosition允許您指定列在網格中的位置：0是第一位 &lt;number of=&quot;&quot; columns=&quot;&quot;>-1是最後一個位置。 任何其他值會受到忽略。

在前例中，選擇列是作為forcedPosition=&quot;0&quot;的第一列。

### 查詢Servlet {#query-servlet}

預設情況下，可在以下位置找到查詢Servlet: `/libs/wcm/core/components/bulkeditor/json.java`。 可以配置其他路徑以檢索資料。

查詢Servlet的工作方式如下：它接收GQL查詢和要返回的列，計算結果，並將結果作為JSON流發回到批量編輯器。

在「產品清單」元件案例中，發送到Query Servlet的兩個參數如下：

* 查詢：&quot;路徑：/content/geometrixx/en/customers/jcr:content/par/productlist多維資料集&quot;
* cols:&quot;選擇，ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

返回的JSON流如下所示：

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

每個命中都對應一個節點及其屬性，並在網格中顯示為一行。

可以擴展Query Servlet以返回複雜繼承模型或返回儲存在特定邏輯位置的節點。 查詢Servlet可用於執行任何類型的複雜計算。 然後，網格可以顯示作為儲存庫中多個節點聚合的行。 在這種情況下，這些行的修改和保存必須由保存Servlet管理。

### 保存Servlet {#save-servlet}

在批量編輯器的預設配置中，每行都是一個節點，並且此節點的路徑儲存在行記錄中。 批量編輯器通過jcr路徑保留行和節點之間的連結。 當用戶編輯網格時，將生成所有修改的清單。 當用戶按一下 **保存**，將POST查詢發送到具有更新的屬性值的每個路徑。 這是Sling概念的基礎，如果每個單元是節點的屬性，則其工作良好。 但是，如果實現Query Servlet進行繼承計算，則此模型不能作為Query Servlet返回的屬性從另一個節點繼承。

「保存Servlet」概念是，這些修改不會直接發佈到每個節點，而是發佈到執行保存作業的一個Servlet。 這使此Servlet能夠分析修改並將屬性保存在正確的節點上。

每個更新的屬性都以下列格式發送到servlet:

* 參數名稱： &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

   示例：/content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* 值： &lt;value>

   例如: 12123

Servlet需要知道catalogCode屬性的儲存位置。

預設的Save Servlet實現可在/libs/wcm/bulkeditor/save/POST.jsp上找到，並用於「產品清單」元件。 它從請求中獲取所有參數( &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> 格式)，並使用JCR API在節點上寫入屬性。 如果節點不存在（網格插入的行），它還會建立節點。

預設代碼不應像重新實施伺服器本機操作那樣使用(POST &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>)，因此只是構建管理屬性繼承模型的Save Servlet的一個好起點。
