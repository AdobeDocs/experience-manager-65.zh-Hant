---
title: PDF產生無法使用WorkBench列印大量PDF
description: 當客戶透過WorkBench實作的服務產生大量PDF時，列印服務會失敗。
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# PDF產生無法透過WorkBench列印大量PDF {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## 問題 {#issue}

當客戶透過WorkBench實作的服務產生大量PDF時。 服務因記憶體不足而失敗。 錯誤顯示為：

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!-- Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.-->

這是因為在Windows上，列印請求的最大頁數限製為大約1000頁。 產生列印輸出時，範本和資料必須載入記憶體，產生的版面配置會建置在記憶體中。 這表示最終輸出的大小有限制。 產生列印輸出的程式是32位元工作，這表示在Windows上限製為2 GB的RAM <!--and 4 GB on UNIX-->.

## 套用至 {#applies-to}

解決方案適用於AEM Forms <!--JEE Server and AEM Forms on OSGi Server--> 用於x86_win32 XMLFM。

## 解決方案 {#solution}

影響記憶體使用量最大的因素是表單上的資料量。 不過，在表單設計中有其他因素會對記憶體使用造成較小的影響。 當您瞭解這些因素時，您可以設計表單以輸出較大的列印。 以下區段會依優先順序指出影響記憶體足跡的因素：

### 影響因子 {#impact-factor}

**高**

1. **選擇子表單**  — 選擇子表單集是子表單集物件的變體，可讓您使用條件陳述式從集內自訂特定子表單的顯示。
1. **使用靜態文字取代註解**  — 幾乎所有欄位內都會提供標題，使用者應使用它，而非將額外的靜態文字當作標題。
1. 使用 **Rtf格式(RTF)** 儘可能使用。

**平均**

設計表單範本時，為協助改善記憶體使用量，應考慮其他因素：

1. 避免使用靜態文字來標示欄位。 請改用文字欄位中的標題。
2. 請勿過度使用矩形、直線、物件和表格。
3. 儘可能避免使用RichText和Choice子表單。
4. 避免過度使用子表單和巢狀子表單。

### 資料大小限制 {#data-size-limitations}

由於我們受到最大處理序記憶體的限制，而且處理序耗用的記憶體不僅取決於資料檔案的大小。 它與表單設計密切相關，在某種程度上也與表單中合併的實際資料量密切相關。

如果表單中有許多小節點且資料量小，該程式會消耗較多的記憶體（因此會更快地用盡記憶體），而不是節點數較少（甚至）且資料量大的表單。

閱讀 [以下附錄](#appendix) 如需詳細資訊，其中測試結果是根據列印表單(非標籤PDF)。 使用標籤的PDF程式記憶體需求會增加。 這也取決於表單中的欄位數量 — 大約程式記憶體需求會比非標籤PDF的1.5倍稍多。

### 互動式Forms {#interactive-forms}

由於互動式欄位會再次呈現，互動式表單會耗用比列印Forms更多的記憶體。 在執行的測試中，記憶體消耗大約比列印表單增加1.5倍，而且這些是靜態互動表單。

### 影像格式 {#image-formats}

Adobe不建議任何特定的影像格式。 但最好有較小的影像大小，例如PNG （可攜式網路圖形）。 也不建議使用高解析度影像，其大小有數百兆位元組不等。 此外，不建議使用壓縮影像，因為解壓縮後影像的大小會擴充至數百MB的資料。

### 附錄 {#appendix}

**表格範例**

表格的不同變體顯示於下方，比較簡單表格和複雜表格的轉譯頁數與資料大小。

1. 含有單一欄的表格，其中產生5000頁PDF，資料檔案大小為24 MB且30-K記錄。

   ![table_single_column](/help/forms/using/assets/table_single_column.png)

1. 含有許多小欄的表格，其中產生800頁的PDF，資料檔案大小為4.6 MB和20-K記錄。
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. 含有許多小欄的表格，但因為使用較大的xmlTag名稱而造成較大的資料檔案。
在此，所有內容都和上一個相同，但xml標籤名稱已變大（因此資料檔案大小會增加，而不會增加實際有效資料），最終結果（上限）幾乎相同。 雖然資料檔案大小從4.6 MB增加為44.6 MB。 在此產生800頁的PDF，資料檔案大小為44.6 MB和20-K記錄。

   ![table_bigger_xml_tagname](/help/forms/using/assets/table_bigger_xml_tagname.png)

因此，很難對資料檔案大小設定一般上限。 每個表單都是獨一無二的，因此各表單的記憶體耗用量會有所不同。