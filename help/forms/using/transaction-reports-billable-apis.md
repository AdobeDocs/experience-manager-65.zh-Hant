---
title: 事務處理報表可開單API
seo-title: Transaction Reports Billable APIs
description: 作為事務處理入賬的所有API的清單
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

# 事務處理報表可開單API{#transaction-reports-billable-apis}

AEM Forms提供多個API來提交表單、處理文檔和呈現文檔。 某些API被記為事務，而其他API則可免費使用。 此文檔提供在事務報表中作為事務處理入帳的所有API的清單。 以下是使用可計費API的幾種常見方案：

* 提交自適應表單、HTML5表單和表單集
* 呈現互動式通信的打印或網路版本
* 將文檔從一種格式轉換為另一種格式
* 拼合動態PDF文檔
* 生成記錄文檔
* 將互動式PDF文檔與另一PDF文檔合併
* 使用工作流的分配任務步驟和文檔服務AEM步驟
* 在自適應形式內使用自適應形式

計費API不包括頁數、文檔或表單的長度或所呈現文檔的最終格式。 事務報表將事務分為兩類：已提交的檔案和Forms已提交。

* **Forms提交：** 當從與AEM Forms合作建立的任何類型的表單提交資料並將資料提交到任何資料儲存儲存庫或資料庫時，將視為表單提交。 例如，提交自適應表單、HTML5表單、PDF forms和表單集將作為提交的表單入賬。 表單集中的每個表單都被視為提交。 例如，如果表單集有5個表單，則提交表單集時，事務報告服務會將其計為5個提交。

* **已呈現的文檔：** 通過組合模板和資料、對文檔進行數字簽名或認證、使用文檔服務的可開單文檔服務API或將文檔從一種格式轉換到另一種格式來生成文檔，作為所呈現的文檔入賬。

>[!NOTE]
>
>事務處理報表用戶介面顯示三個類別：Forms已提交、已呈現的文檔和已處理的文檔。 已呈現的文檔和已處理的文檔均作為已呈現的文檔入賬。

## 可開單文檔服務API {#billable-document-services-apis}

### 生成PDF服務 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">建立PDF</a></td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">導出PDF</a></td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">html檔案到PDF</a></td>
   <td><p>從PDF頁建立HTML。</p> </td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>從指向PDF頁的URL建立HTML。</td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>從指向PDF頁的URL建立HTML。</td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">優化PDF</a></td>
   <td>優化PDF，通過刪除不必要的元資料來減小檔案大小，而不影響質量。</td>
   <td>已處理的文件<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Distiller {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">建立PDF</a><br /> </td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">呈現</a></td>
   <td>調用指定的呈現方法以使用提供的參數生成記錄文檔。</td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">生成PDFOutput</a></td>
   <td>合併資料和模板以建立PDF文檔。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">生成PDFOutput</a></td>
   <td>合併資料和模板以建立PDF文檔。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>合併資料和模板以建立一組PDF文檔。</td>
   <td>已處理的文件</td>
   <td> generatePDFOutputBatch API將表單模板與記錄組合，並生成PDF。 處理一批記錄時，事務處理報告服務會將每個記錄計算為單獨的PDF格式副本。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> 標籤以將多個格式副本合併到單個PDF檔案。 無論標誌的狀態如何，服務都會將每個記錄計為單獨的PDF格式副本。 </td>
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
   <td> generatePDFOutputBatch API將表單模板與記錄組合，並生成PDF。 處理一批記錄時，事務處理報告服務會將每個記錄計算為單獨的PDF格式副本。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> 標籤以將多個格式副本合併到單個PDF檔案。 無論標誌的狀態如何，服務都會將每個記錄計為單獨的PDF格式副本。 </td>
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
   <td>從XDP模板呈現PDF窗體。 XP模板是在Forms設計器中建立的。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">導出資料</a></td>
   <td>從PDF表單或XDP模板中提取資料</td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">到影像</a></td>
   <td>將PDF文檔轉換為影像文檔清單。 支援的影像格式為JPEG、JPEG2K、PNG和TIFF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">到PS</a></td>
   <td>使用選項規範中指定的選項將平面PDF檔案轉換為PostScript格式。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 巴克德Forms局 {#barcoded-forms-service}

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
   <td>對Document對象中的所有條形碼進行解碼並返回一個org.w3c.dom.Document對象，該對象包含從條形碼檢索到的資料。</td>
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
   <td>執行指定的DDX文檔並返回 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">匯編結果</a> 包含結果文檔的對象。 </td>
   <td>已處理的文件</td>
   <td>下列業務不作為交易入賬：
    <ul>
     <li>建立包或包</li>
     <li>拼接多個XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">調用</a></td>
   <td>執行指定的DDX文檔並返回 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">匯編結果</a> 包含結果文檔的對象。 </td>
   <td>已處理的文件</td>
   <td>PDF生成器、Forms和輸出服務支援的所有輸入檔案格式，匯編器服務支援所有這些格式作為輸出檔案格式。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">到PDFA</a></td>
   <td>使用指定的選項將指定的文檔轉換為PDF/A。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 匯編器服務的調用API可以根據輸入在內部調用另一服務的可計費API。 因此，調用API可以作為無、單或多個事務處理來處理。 計數的事務數取決於輸入和調用的內部API。
>* 使用匯編程式服務生成的單個PDF文檔可以作為無、單個或多個事務處理入賬。 計數的事務數取決於提供的DDX代碼。
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">將PDF轉換為XDP</a></td>
   <td>將PDF文檔轉換為XDP檔案。 為了使PDF文檔成功轉換為XDP檔案，PDF文檔必須在AcroForm字典中包含XFA流。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 計費資料捕獲API {#billable-data-capture-apis}

自適應表單、FormsHTML和表單集的所有提交事件均作為事務處理入賬。 預設情況下，提交PDF表單不會作為交易記錄入賬。 使用提供的 [事務記錄器API](record-transaction-custom-implementation.md) 將PDF forms提交記錄為交易記錄。

### 最適化表單 {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>說明</td>
   <td>交易記錄報表類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交自適應表單</td>
   <td>提交一個自適應表單以配置提交操作。 </td>
   <td>已提交的表單</td>
   <td>
    <ul>
     <li>成功提交可用於單個或兩個事務。 計數的事務處理數取決於用於提交的提交操作類型。 例如，通過電子郵件提交操作帳戶發送PDF，以處理兩個事務。 使用記錄文檔(DOR)服務生成的一個用於提交表單的事務處理和另一個用於PDF的事務處理。 </li>
     <li>在自適應表單（自適應表單表單集）中使用自適應表單只計算單個事務。 可以在自適應窗體中擁有任意數量的自適應窗體。</li>
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
   <td>提交HTML5表單</td>
   <td>提交HTML5表單以提交在表單中配置的URL。</td>
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
     <li>在自適應表單（自適應表單表單集）中使用自適應表單只計算單個事務。 可以在自適應窗體中擁有任意數量的自適應窗體。</li>
     <li>HTML5Forms窗體中的每個窗體都將帳戶設定為單獨的事務。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 基於OSGi API的可計費交互AEM通信和以表單為中心的工作流 {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

在OSGi上分配以表單為中心的工作流的任務和文檔服務AEM步驟以及互動式通信的所有格式副本，並作為事務處理入賬。 在作者實例上預覽互動式通信以及使用代理用戶介面在發佈實例上預覽不會作為事務處理入賬。 如果工作流步驟將事務處理入帳，而工作流無法完成，則不會衝銷事務處理計數。

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
   <td>呈現Web通道</td>
   <td>開啟互動式通信的Web版本。</td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">呈現</a> (轉換為PDF)</td>
   <td>生成互動式通信的PDF版本。</td>
   <td>已呈交的文件</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### OSGi上以表AEM格為中心的工作流  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>用例</p> </td>
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
   <td>將交互通信（打印通道）從代理UI提交到工作流</td>
   <td>已呈交的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 將可開單API記錄為自定義代碼的事務 {#recording-billable-apis-as-transactions-for-custom-code}

諸如提交PDF表單、使用代理UI預覽互動式通信、使用非標準表單提交和自定義實現等操作不會作為事務處理入賬。 AEM Forms提供API來記錄這些操作，如事務。 您可以從自定義實現調用API [記錄交易記錄](/help/forms/using/record-transaction-custom-implementation.md)。

## 相關文章 {#related-articles}

* [事務處理報表概覽](../../forms/using/transaction-reports-overview.md)
* [查看和瞭解事務處理報表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [記錄自定義實現的事務](/help/forms/using/record-transaction-custom-implementation.md)
