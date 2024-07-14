---
title: 針對JEE上的AEM Forms交易報告計費API 。
description: 在JEE上記為AEM Forms交易的所有API清單。
topic-tags: forms-manager
feature: Transaction Reports
exl-id: dbb22369-c0a2-4cf6-b01b-096b4de13a14
role: Admin, User, Developer
solution: "Experience Manager, Experience Manager Forms"
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 3%

---

# 適用於AEM Forms on JEE的交易報告可記帳API {#transaction-reports-billable-apis}

JEE上的AEM Forms提供數個API來提交、處理和轉譯檔案。 有些API是以交易入帳，其他則可供自由使用。 本檔案提供入帳為交易的所有API清單。 以下是一些使用計費API的常見案例：

* 將檔案從一種格式轉換為另一種格式
* 平面化動態PDF檔案
* 將互動式PDF檔案與另一個PDF檔案合併

帳單API不考慮頁數、檔案或表單的長度，或轉譯檔案的最終格式。
<!--

* **Forms Submitted:** When data is submitted from any type of form created with AEM Forms and the data is submitted to any data storage repository or database is considered form submission. For example, submitting an HTML5 Form, PDF Forms are accounted as forms submitted. Each form in a form set is considered a submission. For example, if a form set has 5 forms, when the form set is submitted, transaction reporting service counts it as 5 submissions.

* **Documents Rendered:** Generating a document by combining a template and data, digitally signing or certifying a document, using a billable document services API for document services, or converting a document from one format to another are accounted as documents rendered.

-->

以下是JEE計費API清單。 在OSGi](/help/forms/using/transaction-reports-billable-apis.md)上尋找AEM Forms的[可記帳API清單。

## 可記帳檔案服務API {#billable-document-services-apis}

### 產生PDF服務 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
  </tr>
   <tr>
   <td><a>CreatePDF</a></td>
   <td>為受支援的檔案型別建立Adobe PDF。</td>
   <td>轉換<br /> </td>
  </tr>
  <tr>
   <td><a>CreatePDF3</a></td>
   <td>為受支援的檔案型別建立Adobe PDF。 </td>
   <td>轉換<br /> </td>
  </tr>
  <tr>
   <td><a> HtmlToPDF</a></td>
   <td>將HTML檔案轉換為Adobe PDF。 </td>
   <td>轉換<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF</a></td>
   <td>將PDF匯出至支援的檔案型別。 </td>
   <td>轉換<br /> </td>
  </tr>
  <tr>
   <td><a>EXPORTPDF2</a></td>
   <td><p>將PDF匯出至支援的檔案型別。</p> </td>
   <td>轉換<br /> </td>
  </tr>
  <tr>
   <td><a>EXPORTPDF3</a></td>
   <td>將PDF匯出至支援的檔案型別。</td>
   <td>轉換<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlFileToPDF</a></td>
   <td>將HTML檔案轉換為PDF。</td>
   <td>轉換<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlToPDF2</a></td>
   <td>將HTML檔案轉換為PDF。</td>
   <td>轉換<br /> </td>
  </tr>
  <tr>
   <td><a>OptimizePDF</a></td>
   <td>最佳化PDF以移除不必要的中繼資料，進而降低檔案大小，而不會影響品質。</td>
   <td>轉換<br /> </td>
  </tr>
 </tbody>
</table>

### DocAssurance服務 {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
  </tr>
  <tr>
   <td><a>簽署/認證</a><br /> </td>
   <td>此API可讓您保護檔案的安全。 您可以使用此API來簽署及認證PDF檔案。</td>
   <td>轉換</td>
  </tr>
 </tbody>
</table>


### Distiller服務 {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
  </tr>
  <tr>
  <tr>
   <td><a>CreatePDF</a></td>
   <td>從支援的檔案型別建立Adobe PDF。</td>
   <td>轉換</td>
  </tr>
  <tr>
   <td><a>CreatePDF2</a></td>
   <td>從支援的檔案型別建立Adobe PDF。</td>
   <td>轉換</td>
  </tr>
 </tbody>
</table>

<!--

### Document of Record Service (DoR Service) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### 輸出服務 {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
  </tr>
  <tr>
   <td><a>generateOutput</a></td>
   <td>合併資料和範本以建立PDF檔案。</td>
   <td>已呈交的文件</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput</a></td>
   <td>合併資料和範本以建立PDF檔案。</td>
   <td>已呈交的文件</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput2</a></td>
   <td>合併資料和範本以建立PDF檔案。</td>
   <td>已呈交的文件</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput</a></td>
   <td>將XDP和PDF檔案轉換為PostScript (PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已呈交的文件</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput2</a></td>
   <td>將XDP和PDF檔案轉換為PostScript (PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已呈交的文件</td>
  </tr>
  <tr>
   <td><a>transformPDF</a></td>
   <td>將一組XDP和PDF檔案轉換為一組PostScript (PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>檔案轉換</td>
  </tr>
 </tbody>
</table>

<!-- ### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XDP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### 轉換PDF服務 {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
  </tr>
  <tr>
   <td><a>toImage2</a></td>
   <td>將PDF檔案轉換為影像檔案清單。 支援的影像格式為JPEG、JPEG2K、PNG和TIFF。</td>
   <td>檔案轉換</td>
  </tr>
  <tr>
   <td><a>toPS2</a></td>
   <td>使用選項規格中指定的選項，將「平坦PDF」檔案轉換為PostScript格式。</td>
   <td>檔案轉換</td>
  </tr>
  <tr>
   <td><a>toSWF</a></td>
   <td>使用選項規格中指定的選項將「平坦PDF」檔案轉換為SWF格式。</td>
   <td>檔案轉換</td>
  </tr>
 </tbody>
</table>

### 條碼式Forms服務 {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
  </tr>
  <tr>
   <td><a>解碼</a></td>
   <td>解碼Document物件中的所有條碼，並傳回org.w3c.dom.Document物件，該物件包含從條碼擷取的資料。</td>
   <td>檔案轉換</td>
  </tr>
 </tbody>
</table>

### 組合器服務 {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
  </tr>
  <tr>
   <td><a>叫用</a></td>
   <td>執行指定的DDX檔案並傳回包含結果檔案的AssemblerResult物件。 </td>
   <td>檔案轉換</td>
  </tr>
  <tr>
   <td><a>invokeDDX</a></td>
   <td>執行指定的DDX檔案並傳回包含結果檔案的AssemblerResult物件。 </td>
   <td>檔案轉換</td>
  </tr>
  <tr>
   <td><a>invokeOneDocument</a></td>
   <td>使用指定的選項將指定的檔案轉換為PDF/A。</td>
   <td>檔案轉換</td>
  </tr>
  <tr>
   <td><a>invokeDDXneDocument</a></td>
   <td>使用指定的選項將指定的檔案轉換為PDF/A。</td>
   <td>檔案轉換</td>
  </tr>
  <tr>
   <td><a>toPDFA</a></td>
   <td>使用指定的選項將指定的檔案轉換為PDF/A。</td>
   <td>檔案轉換</td>
  </tr>
 </tbody>
</table>

當您執行下列一或多個作業時，叫用API的使用量會計為交易：
1. 從非PDF格式轉換成PDF格式。 例如，從XDP格式轉換成PDF格式。<!-- catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. 從PDF格式轉換為PDF/A格式。
1. 從PDF格式轉換為非PDF格式。 範例包括從PDF到影像格式的轉換或從PDF到文字格式的轉換。

>[!NOTE]
>
>* 組合器服務的叫用API可以在內部根據輸入呼叫另一個服務的計費的API。 因此，`invoke API`可計為無、單一或多個交易。 計算交易數取決於輸入和叫用的內部API。
>* 使用組合器服務（例如`invoke`和`invokeDDX`）產生的單一PDF檔案可計為無、單一或多個交易。 計算的交易數目取決於提供的<!--DDX-->代碼。

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a>convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Conversion</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

## 可記帳資料擷取API {#billable-data-capture-apis}

<!--All the submission events of Forms, HTML5 Forms, and form set are accounted as transactions. By default, submission of a PDF Form is not accounted as a transaction. Use the provided [transaction recorder API](record-transaction-custom-implementation.md) to record a PDF Forms submission as a transaction.-->

<!--
### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an adaptive form</td>
   <td>Submits an adaptive form to configured submit action. </td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Successful submissions account for single or two transactions. The number of transactions counted depends upon the type of submit action used for submission. For example, sending PDF through email submit action accounts for two counts of transactions. One transaction for form submission and another for PDF generated using the Document of Record (DOR) service. </li>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

<!--### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### 表單 {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
  </tr>
  <tr>
   <td>exportData</td>
   <td>提交表單。</td>
   <td>已提交的表單</td>
  </tr>
  <tr>
   <td>exportData2</td>
   <td>提交表單。</td>
   <td>已提交的表單</td>
  </tr>
  <tr>
   <td>renderForm</td>
   <td>提交表單。</td>
   <td>Forms已呈現</td>
  </tr>
  <tr>
   <td>renderHTMLForm</td>
   <td>提交表單。</td>
   <td>Forms已呈現</td>
  </tr>
  <tr>
   <td>renderHTMLForm2</td>
   <td>提交表單。</td>
   <td>Forms已呈現</td>
  </tr>
  <tr>
   <td>renderPDFForm</td>
   <td>提交表單。</td>
   <td>Forms已呈現</td>
  </tr>
  <tr>
   <td>renderPDFForm2</td>
   <td>提交表單。</td>
   <td>Forms已呈現</td>
  </tr>
  <tr>
   <td>renderPDFFormWithUsageRights</td>
   <td>提交表單。</td>
   <td>Forms已呈現</td>
  </tr>
 </tbody>
</table>

<!-- ## Billable Interactive Communication and Form-centric AEM Workflows on OSGi APIs {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.

<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
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
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Form-centric AEM Workflows on OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Use case</p> </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an Assign Task step</td>
   <td>Forms Submitted</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Submitting a workflow application startpoint </td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
  <tr>
   <td>Submitting an interactive communication (Print Channel) from the Agent UI to a workflow</td>
   <td>Documents Rendered</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--

WILL ADD THIS ONE - 

## Recording billable APIs as transactions for custom code {#recording-billable-apis-as-transactions-for-custom-code}

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, using non-standard form submission, and custom implementations are not accounted as transactions. AEM Forms provides an API to record such actions as transactions. You can call the API from your custom implementations to [record a transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md)
* [Viewing and Understanding a Transaction Reports](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Record a transaction for custom implementations](/help/forms/using/record-transaction-custom-implementation.md)

-->

## 相關文章

* [在JEE上啟用和檢視AEM Forms的交易報告](/help/forms/using/transaction-report-overview-jee.md)
* [為JEE上的AEM Forms記錄自訂元件API的交易](/help/forms/using/record-transaction-custom-component-jee.md)
