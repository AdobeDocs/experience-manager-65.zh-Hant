---
title: 搜索表單和資產
seo-title: Searching for forms and assets
description: 您可以使用搜索搜索實例中AEM的表單AEM和資產。 基本和高級搜索允許您快速查找資產。
seo-description: You can search forms and assets in your AEM instance using AEM search. Basic and advanced search allows you to quickly locate your assets.
uuid: 0928a453-3dc4-448b-9320-dcbf20606dd9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: e65925ff-1fbf-4da6-bf09-0cf056c86e5a
docset: aem65
role: Admin
exl-id: 1f4f49b7-5f32-47dd-9dc7-a6974faf2bdf
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 3%

---

# 搜索表單和資產{#searching-for-forms-and-assets}

您可以使用文本字串或文本字串以及通配符搜索表單或表單資產。 您還可以使用「搜索」面板中各種類別中提供的條件縮小搜索範圍。

選擇一個或多個條件並指定文本字串時，文本和條件的交集將作為搜索結果返回。 搜索結果與提供的表單和資產元資料一樣好。

按一下 ![aem6forms搜索](assets/aem6forms_search.png)，顯示或隱藏搜索面板。

## 基本搜索 {#basic-search}

基本搜索是預設搜索，運行時不指定任何篩選器。 元資料屬性全文搜索由AEM Forms進行。

要運行基本搜索，請在文本欄位中輸入搜索查詢並按回車鍵。 也可以輸入通配符(&#42;)匹配任意數字元。

Adobe Experience Manager在元資料屬性中搜索輸入的文本並返回相應的結果。 如果鍵入多個單詞，則搜索操作將匹配要搜索的完整文本。

請注意以下有關基本搜索的要點：

* 使用表單和資產元資料屬性執行搜索。
* 如果鍵入多個單詞，則搜索操作將匹配要搜索的完整文本。
* 搜索不區分大小寫。 例如，當鍵入 `geometrixx`，標題為的資產 `Geometrixx`。 `GEOMETRIXX`, `GeoMetRixx` 的子菜單。

* 不支援單詞的部分匹配。 要使用部分字串進行搜索，請使用 &#42; 通配符。 但是，如果搜索查詢與完整單詞匹配，則顯示相應的表單或資產。
* 在搜索過程中，會尊重並且不修剪額外的空格。 比如說， `My form` 與 `My form`。

* 如果元資料屬性中欄位的資料和顯示值不同，則不能將顯示值用作搜索參數。 例如，不能基於狀態（如「已修改」或「已發佈」）進行搜索，因為這些屬性以不同的格式儲存。

## 高級搜索 {#advanced-search}

在搜索條件中，除了查詢外，還可以指定一些搜索參數，使基本搜索更加高效和集中。

![用於表單和資產搜索的搜索欄位AEM和參數或篩選器](assets/search_forms_assets.png)

用於表單和資產搜索的搜索欄位AEM和參數或篩選器

### 資產路徑 {#asset-path}

通過使用資產路徑篩選器，可以將搜索結果限制為當前目錄。 如果未選擇「在當前目錄中搜索」選項，則搜索結果將包含基目錄中的資產。 如果當前頁不是目錄，並且選擇了「在當前目錄中搜索」選項，則搜索將返回父目錄中存在的資產。

### 資產修改 {#asset-modification}

選擇以下選項之一，以搜索在特定時間段內修改的所有資產。

| **選項** | **說明** |
|---|---|
| 2 小時前 | 搜索過去兩小時內修改的所有資產。 |
| 1 週前 | 搜索在最近一週內修改的所有資產。 |
| 1 個月前 | 搜索在過去一個月內修改的所有資產。 |
| 1 年前 | 搜索在過去一年內修改的所有資產。 |

### 資產狀態 {#asset-status}

您可以使用以下狀態之一搜索資產：

* **已發佈**:搜索發佈後已發佈且未修改的所有資產。

* **未發佈**:搜索從未發佈的所有資產。

* **已修改**:搜索發佈後修改或未發佈的所有資產。

### 資產類型 {#asset-type}

您可以選擇任意數量的資產類型。 搜索返回所有選定資產類型的合併。

<table>
 <tbody>
  <tr>
   <th>選項</th> 
   <th>說明</th> 
  </tr>
  <tr>
   <td>表單模板<br /> </td> 
   <td>搜索所有表單模板。<br /> </td> 
  </tr>
  <tr>
   <td>PDF窗體</td> 
   <td>搜索所有PDF文檔。</td> 
  </tr>
  <tr>
   <td>文件</td> 
   <td>搜索所有文檔。</td> 
  </tr>
  <tr>
   <td>自適應窗體<br /> </td> 
   <td>搜索所有自適應表單。</td> 
  </tr>
  <tr>
   <td>資源</td> 
   <td>搜索所有資源。<br /> </td> 
  </tr>
 </tbody>
</table>

### 標記 {#tags}

標籤是附加到資產以進行標識的標籤。 搜索時，從下拉清單中選擇任意數量的標籤或添加自定義標籤（如有必要）。 搜索結果包含所選標籤的交集。
