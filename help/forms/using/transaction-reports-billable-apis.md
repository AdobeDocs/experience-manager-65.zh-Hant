---
title: 事務處理報表可開單API
seo-title: 事務處理報表可開單API
description: 列出所有作為事務處理的API
seo-description: 列出所有作為事務處理的API
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# 事務處理報表可開單API{#transaction-reports-billable-apis}

AEM Forms提供數個API來提交表單、處理檔案和演算檔案。 有些API會以交易方式入賬，而有些則可免費使用。 本檔案提供在交易報表中以交易方式入賬的所有API的清單。 以下是使用計費API的一些常見方案：

* 提交最適化表單、HTML5表單和表單集
* 呈現互動式通訊的平面或網頁版本
* 將文檔從一種格式轉換為另一種格式
* 平面化動態PDF檔案
* 生成記錄文檔
* 將互動式PDF檔案與其他PDF檔案合併
* 使用AEM工作流程的指派工作步驟和檔案服務步驟
* 在自適應表單中使用自適應表單

帳單API不會計入頁數、檔案或表單的長度，或轉譯檔案的最終格式。 事務報表將事務分為兩類：已轉譯的檔案和已提交的表單。

* **** 提交的表單：當從使用AEM Forms建立的任何類型表單提交資料，且資料會提交至任何資料儲存存放庫或資料庫時，即視為表單提交。 例如，提交最適化表單、HTML5表單、PDF表單和表單集都會視為提交的表單。 表單集中的每個表單都被視為提交。 例如，如果表單集有5個表單，提交表單集時，事務報告服務會將其計為5個提交。

* **** 轉譯的檔案：通過組合模板和資料、數字地簽名或認證文檔、使用文檔服務的可計費文檔服務API或將文檔從一種格式轉換為另一種格式來生成文檔，被視為所呈現的文檔。

>[!NOTE]
>
>交易報表UI會顯示三個類別：已提交的表單、已轉譯的檔案和已處理的檔案。 所呈現的文檔和所處理的文檔均作為所呈現的文檔入賬。

## 可計費的檔案服務API {#billable-document-services-apis}

### 產生PDF服務 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
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
   <td><p>從HTML頁面建立PDF。</p> </td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>從指向HTML頁面的URL建立PDF。</td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>從指向HTML頁面的URL建立PDF。</td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">最佳化PDF</a></td>
   <td>最佳化PDF，借由移除不必要的中繼資料來減少檔案大小，而不會影響品質。</td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
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

### 記錄服務檔案（DoR服務） {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">渲染</a></td>
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
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>合併資料和範本以建立PDF檔案。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>合併資料和範本以建立PDF檔案。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>合併資料和範本以建立一組PDF檔案。</td>
   <td>已處理的文件</td>
   <td> generatePDFOutputBatch API將表單範本與記錄結合，並產生PDF。 當您處理一批記錄時，交易報告服務會將每個記錄計為個別的PDF轉譯。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles旗標</a> ，將多個轉譯合併為單一PDF檔案。 不論旗標狀態為何，服務都會將每個記錄計為個別的PDF轉譯。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>將XDP和PDF檔案轉換為PostScript(PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>將XDP和PDF檔案轉換為PostScript(PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>將一組XDP和PDF檔案轉換為一組PostScript(PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> generatePDFOutputBatch API將表單範本與記錄結合，並產生PDF。 當您處理一批記錄時，交易報告服務會將每個記錄計為個別的PDF轉譯。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles旗標</a> ，將多個轉譯合併為單一PDF檔案。 不論旗標狀態為何，服務都會將每個記錄計為個別的PDF轉譯。 </td>
  </tr>
 </tbody>
</table>

### 表單服務 {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>從XDP範本轉譯PDF表單。 XP範本是在Forms Designer中建立的。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>從PDF表單或XDP範本擷取資料</td>
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
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>將PDF檔案轉換為影像檔案清單。 支援的影像格式包括JPEG、JPEG2K、PNG和TIFF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>使用選項規範中指定的選項將平面PDF檔案轉換為PostScript格式。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Barcoded Forms服務 {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">解碼</a></td>
   <td>解碼Document物件中的所有條碼，並傳回包含從條碼擷取之資料的org.w3c.dom.Document物件。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Assembler Service {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">調用</a></td>
   <td>執行指定的DDX文檔並返回包 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">含結果文檔的AssemblerResult</a> 對象。 </td>
   <td>已處理的文件</td>
   <td>下列業務不會作為交易入賬：
    <ul>
     <li>建立套件或作品集</li>
     <li>拼接多個XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">調用</a></td>
   <td>執行指定的DDX文檔並返回包 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">含結果文檔的AssemblerResult</a> 對象。 </td>
   <td>已處理的文件</td>
   <td>Assembler服務支援PDF產生器、表單和輸出服務支援的所有輸入檔案格式，支援所有這些格式做為輸出檔案格式。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>使用指定的選項，將指定的檔案轉換為PDF/A。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 匯編器服務的調用API可以根據輸入在內部調用另一服務的計費API。 因此，調用API可以作為無、單個或多個事務處理來處理。 計算的交易數量取決於輸入和呼叫的內部API。
>* 使用匯編器服務生成的單個PDF文檔可以作為無、單個或多個事務處理來處理。 計算的交易數量取決於提供的DDX代碼。
>



### PDF公用程式服務 {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>將PDF檔案轉換為XDP檔案。 為了讓PDF檔案成功轉換為XDP檔案，PDF檔案必須在AcroForm字典中包含XFA串流。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 計費資料擷取API {#billable-data-capture-apis}

最適化表單、HTML5表單和表單集的所有提交事件都視為交易。 依預設，提交PDF表單不會算作交易。 使用提供的 [交易記錄API](transaction-reports-billable-apis.md#recordingbillableapisastransactionsforcustomcode) ，將PDF表單提交記錄為交易。

### 適用性表單 {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交最適化表單</td>
   <td>提交最適化表單以設定提交動作。 </td>
   <td>已提交的表單</td>
   <td>
    <ul>
     <li>成功的提交包含單筆或兩筆交易。 計算的事務處理數取決於用於提交的提交操作類型。 例如，透過電子郵件提交動作帳戶傳送PDF，可計算兩筆交易。 使用記錄檔案(DOR)服務產生的一筆表單提交交易和另一筆PDF交易。 </li>
     <li>在最適化表單（最適化表單集）中使用最適化表單只會計入單一交易。 您可以在最適化表單中擁有任意數量的最適化表單。</li>
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
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>送出HTML5表格</td>
   <td>提交HTML5表單以提交表單中設定的URL。</td>
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
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交表單集</td>
   <td>將表單集提交到表單集中配置的提交URL。</td>
   <td>已提交的表單</td>
   <td>
    <ul>
     <li>在最適化表單（最適化表單集）中使用最適化表單只會計入單一交易。 您可以在最適化表單中擁有任意數量的最適化表單。</li>
     <li>HTML5 Forms表單中的每個表單都會將帳戶設定為個別交易。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi API上的計費互動式通訊和表單導向AEM工作流程 {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

在OSGi上指派表單導向AEM工作流程的工作和檔案服務步驟，以及互動式通訊的所有轉譯，並視為交易處理。 在作者例項上預覽互動式通訊，並使用Agent UI在發佈例項上預覽，不會算作交易。 如果工作流步驟將事務處理入帳，而工作流無法完成，則不會撤消事務處理計數。

### 互動式通訊 - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>呈現網路頻道</td>
   <td>開啟互動式通訊的網頁版本。</td>
   <td>已呈交的文件</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>事務處理報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">轉換</a> （轉換為PDF）</td>
   <td>產生互動式通訊的PDF版本。</td>
   <td>已呈交的文件</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### OSGi上的表單導向AEM工作流程 {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>事務處理報告類別</td>
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
   <td>提交工作流程應用程式起點 </td>
   <td>已提交的表單</td>
   <td> </td>
  </tr>
  <tr>
   <td>將互動式通訊（列印頻道）從代理UI送出至工作流程</td>
   <td>已呈交的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 將可計費API記錄為自訂代碼的交易 {#recording-billable-apis-as-transactions-for-custom-code}

諸如提交PDF表單、使用代理UI預覽互動式通訊、使用非標準表單提交和自訂實作等動作，不會算作交易。 AEM Forms提供API來記錄這類動作，例如交易。 您可以從自訂實作呼叫API以記 [錄交易](/help/forms/using/record-transaction-custom-implementation.md)。

## 相關文章 {#related-articles}

* [事務處理報表概覽](../../forms/using/transaction-reports-overview.md)
* [查看和瞭解事務處理報表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [記錄自訂實作的交易](/help/forms/using/record-transaction-custom-implementation.md)

