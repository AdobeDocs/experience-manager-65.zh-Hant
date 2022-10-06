---
title: 交易報表計費API
seo-title: Transaction Reports Billable APIs
description: 以交易方式入賬的所有API清單
seo-description: List of all the APIs that are accounted as transactions
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
exl-id: 1bc99f3b-3f28-4e74-b259-6ebddc11ffc5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 7%

---

# 交易報表計費API{#transaction-reports-billable-apis}

AEM Forms提供數個API，可提交表單、處理檔案及轉譯檔案。 有些API會記為交易，有些則可免費使用。 本文檔提供在事務處理報告中作為事務處理入帳的所有API的清單。 以下是使用計費API的一些常見案例：

* 提交最適化表單、HTML5表單和表單集
* 呈現互動式通信的打印或網路版本
* 將文檔從一種格式轉換為另一種格式
* 拼合動態PDF文檔
* 生成記錄文檔
* 將互動式PDF文檔與其他PDF文檔合併
* 使用AEM工作流程的指派任務步驟和檔案服務步驟
* 在最適化表單中使用最適化表單

計費API不會計入頁數、檔案或表單的長度，或轉譯檔案的最終格式。 事務處理報表將事務處理分為兩個類別：已呈現的檔案和Forms已提交。

* **Forms已提交：** 從使用AEM Forms建立的任何類型表單提交資料，並將資料提交至任何資料儲存存放庫或資料庫時，即視為表單提交。 例如，提交最適化表單、HTML5表單、PDF forms和表單集會計為提交的表單。 表單集中的每個表單都視為提交。 例如，如果表單集有5個表單，則提交表單集時，交易報告服務會將其計為5個提交。

* **已呈現的文檔：** 通過組合模板和資料、數字簽名或認證文檔、使用可計費文檔服務API來提供文檔服務，或將文檔從一種格式轉換到另一種格式來生成文檔，被記為所呈現的文檔。

>[!NOTE]
>
>交易報表UI會顯示三個類別：Forms已提交、已呈現的檔案和已處理的檔案。 所呈現的文檔和所處理的文檔均作為所呈現的文檔入帳。

## 計費文檔服務API {#billable-document-services-apis}

### 產生PDF服務 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>從支援的檔案類型建立Adobe PDF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>從支援的檔案類型建立Adobe PDF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>將Adobe PDF轉換為支援的檔案類型。 </td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>將Adobe PDF轉換為支援的檔案類型。 </td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>將Adobe PDF轉換為支援的檔案類型。 </td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>從PDF頁面建立HTML。</p> </td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>從指向PDF頁面的URL建立HTML。</td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>從指向PDF頁面的URL建立HTML。</td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>最佳化PDF，借由移除不必要的中繼資料來縮小檔案大小，而不會影響品質。</td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Distiller服務 {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>從支援的檔案類型建立Adobe PDF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>從支援的檔案類型建立Adobe PDF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 記錄服務文檔（DoR服務） {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">轉譯</a></td>
   <td>調用指定的渲染方法以使用提供的參數生成記錄文檔。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 輸出服務 {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>合併資料和模板以建立PDF文檔。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>合併資料和模板以建立PDF文檔。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>合併資料和模板以建立一組PDF文檔。</td>
   <td>已處理的文件</td>
   <td> generatePDFOutputBatch API將表單模板與記錄結合，並生成PDF。 處理一批記錄時，事務報告服務會將每個記錄計為單獨的PDF格式副本。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> 標幟，將多個轉譯結合為單一PDF檔案。 無論標幟的狀態為何，服務都會將每個記錄計為個別的PDF轉譯。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>將XDP和PDF文檔轉換為PostScript(PS)、打印機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>將XDP和PDF文檔轉換為PostScript(PS)、打印機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>將一組XDP和PDF文檔轉換為一組PostScript(PS)、打印機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> generatePDFOutputBatch API將表單模板與記錄結合，並生成PDF。 處理一批記錄時，事務報告服務會將每個記錄計為單獨的PDF格式副本。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> 標幟，將多個轉譯結合為單一PDF檔案。 無論標幟的狀態為何，服務都會將每個記錄計為個別的PDF轉譯。 </td>
  </tr>
 </tbody>
</table>

### Forms 服務 {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>從XDP範本轉譯PDF表單。 XP範本是在Forms Designer中建立。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>從PDF表單或XDP範本中擷取資料</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 轉換PDF服務 {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>將PDF文檔轉換為影像文檔清單。 支援的影像格式包括JPEG、JPEG2K、PNG和TIFF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>使用選項規範中指定的選項，將平面PDF檔案轉換為PostScript格式。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 條碼式Forms服務 {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">解碼</a></td>
   <td>解碼Document對象中的所有條形碼，並返回一個org.w3c.dom.Document對象，該對象包含從條碼中檢索的資料。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 組合器服務 {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">調用</a></td>
   <td>執行指定的DDX文檔並返回 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">組合器結果</a> 包含結果文檔的對象。 </td>
   <td>已處理的文件</td>
   <td>下列業務不會作為交易入賬：
    <ul>
     <li>建立套件或產品組合</li>
     <li>拼接多個XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">調用</a></td>
   <td>執行指定的DDX文檔並返回 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">組合器結果</a> 包含結果文檔的對象。 </td>
   <td>已處理的文件</td>
   <td>PDF生成器、Forms和輸出服務支援的所有輸入檔案格式，組合器服務支援所有這些格式作為輸出檔案格式。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>使用指定的選項將指定的文檔轉換為PDF/A。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 組合器服務的調用API可以根據輸入從內部調用另一服務的計費API。 因此，叫用API可以計為無、單或多個交易。 計算的交易數取決於輸入和叫用的內部API。
>* 使用組合器服務生成的單個PDF文檔可以記為無、單個或多個事務。 計算的交易數取決於提供的DDX代碼。
>


### PDF實用程式服務  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>將PDF檔案轉換為XDP檔案。 為了將PDF檔案成功轉換為XDP檔案，PDF檔案必須在AcroForm字典中包含XFA資料流。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 計費資料捕獲API {#billable-data-capture-apis}

最適化表單、HTML5 Forms和表單集的所有提交事件都計為交易。 預設情況下，提交PDF表單不會計為交易。 使用提供的 [交易記錄器API](record-transaction-custom-implementation.md) 將PDF forms提交記錄為交易記錄。

### 調適型表單 {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交最適化表單</td>
   <td>提交最適化表單以配置提交操作。 </td>
   <td>已提交的表單</td>
   <td>
    <ul>
     <li>成功的提交會計入單筆或兩筆交易。 計算的交易數取決於用於提交的提交操作的類型。 例如，透過電子郵件提交動作傳送PDF會計入兩個交易計數。 用於提交表單的事務處理和用於使用記錄文檔(DOR)服務生成的PDF的事務處理。 </li>
     <li>在最適化表單（最適化表單集）中使用最適化表單只會計入單一交易。 在最適化表單中可以有任意數量的最適化表單。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>說明 </td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交HTML5表</td>
   <td>提交HTML5表單以提交表單中配置的URL。</td>
   <td>已提交的表單</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 表單集 {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交表單集</td>
   <td>將表單集提交到在表單集中配置的提交URL。</td>
   <td>已提交的表單</td>
   <td>
    <ul>
     <li>在最適化表單（最適化表單集）中使用最適化表單只會計入單一交易。 在最適化表單中可以有任意數量的最適化表單。</li>
     <li>HTML中的每個表單5 Forms表單會將帳戶設為個別交易。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi API上的計費互動式通訊和表單導向AEM工作流程 {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

在OSGi上指派以表單為中心的AEM工作流程的任務和檔案服務步驟，以及互動式通訊的所有轉譯，並以交易記帳。 在製作執行個體上預覽互動式通訊和使用代理程式UI在發佈執行個體上預覽沒有計為交易。 如果工作流步驟將事務處理入帳，且工作流無法完成，則事務處理計數不會被撤消。

### 互動式通訊 - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>轉譯Web通道</td>
   <td>開啟互動式通訊的網頁版本。</td>
   <td>已呈交的文件</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### 互動式通信 — 打印通道 {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">轉譯</a> (轉換為PDF)</td>
   <td>生成互動式通信的PDF版本。</td>
   <td>已呈交的文件</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### OSGi上以表單為中心的AEM工作流程  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交分配任務步驟</td>
   <td>已提交的表單</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>提交工作流應用程式起始點 </td>
   <td>已提交的表單</td>
   <td> </td>
  </tr>
  <tr>
   <td>從代理UI提交互動式通訊（列印通道）至工作流程</td>
   <td>已呈交的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 將計費API記錄為自訂代碼的交易 {#recording-billable-apis-as-transactions-for-custom-code}

提交PDF表單、使用代理UI預覽互動式通訊、使用非標準表單提交和自訂實作等動作，不會計為交易記錄。 AEM Forms提供API來記錄這類動作，例如交易。 您可以從自訂實作將API呼叫至 [記錄交易記錄](/help/forms/using/record-transaction-custom-implementation.md).

## 相關文章 {#related-articles}

* [交易報表概述](../../forms/using/transaction-reports-overview.md)
* [查看和了解交易報表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [記錄自訂實施的交易](/help/forms/using/record-transaction-custom-implementation.md)
