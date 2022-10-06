---
title: 搜尋表單和資產
seo-title: Searching for forms and assets
description: 您可以使用AEM搜尋在AEM例項中搜尋表單和資產。 基本和進階搜尋可讓您快速找到資產。
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

# 搜尋表單和資產{#searching-for-forms-and-assets}

您可以使用文字字串或文字字串以及萬用字元來搜尋表單或表單資產。 您也可以使用「搜尋」面板中各種類別可用的條件來縮小搜尋範圍。

選取一或多個條件並指定文字字串時，文字和條件的交集會以搜尋結果傳回。 搜尋結果與提供的表單和資產中繼資料一樣好。

按一下 ![aem6forms_search](assets/aem6forms_search.png)，以顯示或隱藏搜尋面板。

## 基本搜尋 {#basic-search}

基本搜索是預設搜索，運行時不指定任何篩選器。 中繼資料屬性的全文搜尋由AEM Forms執行。

若要執行基本搜尋，請在文字欄位中輸入搜尋查詢，然後點擊傳回。 您也可以輸入萬用字元(&#42;)來比對任何字元數。

Adobe Experience Manager會在中繼資料屬性中搜尋輸入的文字，並傳回對應的結果。 如果鍵入多個單詞，則搜索操作將匹配用於搜索的完整文本。

請注意基本搜尋的下列要點：

* 使用表單和資產中繼資料屬性進行搜尋。
* 如果鍵入多個單詞，則搜索操作將匹配用於搜索的完整文本。
* 搜尋不區分大小寫。 例如，當您輸入 `geometrixx`，標題為資產 `Geometrixx`, `GEOMETRIXX`，和 `GeoMetRixx` 會顯示在搜尋結果中。

* 不支援字詞的部分匹配。 若要使用部分字串進行搜尋，請使用 &#42; 萬用字元。 不過，如果搜尋查詢符合完整的字詞，則會顯示對應的表單或資產。
* 搜尋期間會考慮額外空格，且不會加以修剪。 例如， `My form` 與的搜索查詢不同 `My form`.

* 如果元資料屬性中欄位的資料和顯示值不同，則不能將顯示值用作搜索參數。 例如，您無法根據狀態（如已修改或已發佈）進行搜索，因為這些屬性以不同的格式儲存。

## 進階搜尋 {#advanced-search}

在搜索標準中，除了查詢之外，還可以指定一些搜索參數，使基本搜索更加高效和集中。

![AEM表單和資產搜尋的搜尋欄位和參數或篩選器](assets/search_forms_assets.png)

AEM表單和資產搜尋的搜尋欄位和參數或篩選器

### 資產路徑 {#asset-path}

使用資產路徑篩選器，可將搜尋結果限制為目前目錄。 如果未選擇「在當前目錄中搜索」選項，則搜索結果將包含基目錄中的資產。 如果當前頁不是目錄，且已選取「在當前目錄中搜索」選項，則搜索將返回父目錄中存在的資產。

### 資產修改 {#asset-modification}

選取下列其中一個選項，以搜尋在特定時段內修改的所有資產。

| **選項** | **說明** |
|---|---|
| 2 小時前 | 搜尋過去兩小時內修改的所有資產。 |
| 1 週前 | 搜尋過去一週內修改的所有資產。 |
| 1 個月前 | 搜尋過去一個月內修改的所有資產。 |
| 1 年前 | 搜尋過去一年內修改的所有資產。 |

### 資產狀態 {#asset-status}

您可以使用下列其中一種狀態來搜尋資產：

* **已發佈**:搜尋發佈後已發佈且未修改的所有資產。

* **未發佈**:搜尋所有從未發佈的資產。

* **已修改**:搜尋發佈後修改或取消發佈的所有資產。

### 資產類型 {#asset-type}

您可以選取任何數量的資產類型。 搜尋會傳回所有選取資產類型的聯合。

<table>
 <tbody>
  <tr>
   <th>選項</th> 
   <th>說明</th> 
  </tr>
  <tr>
   <td>表單範本<br /> </td> 
   <td>搜尋所有表單範本。<br /> </td> 
  </tr>
  <tr>
   <td>PDF表單</td> 
   <td>搜索所有PDF文檔。</td> 
  </tr>
  <tr>
   <td>文件</td> 
   <td>搜索所有文檔。</td> 
  </tr>
  <tr>
   <td>適用性表單<br /> </td> 
   <td>搜尋所有最適化表單。</td> 
  </tr>
  <tr>
   <td>資源</td> 
   <td>搜尋所有資源。<br /> </td> 
  </tr>
 </tbody>
</table>

### 標記 {#tags}

標籤是附加至資產以供識別的標籤。 搜尋時，請從下拉式清單中選取任意數量的標籤，或視需要新增自訂標籤。 搜索結果包含選定標籤的交集。
