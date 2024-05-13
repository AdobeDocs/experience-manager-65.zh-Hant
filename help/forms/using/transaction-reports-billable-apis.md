---
title: 交易報告計費 API
description: 作為交易入帳的所有API清單
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
exl-id: e92f1b59-79ef-40fa-af9a-7380cd701a75
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: acb023caf0a7e64fea9cf5d9198d672ee14c8d88
workflow-type: tm+mt
source-wordcount: '1754'
ht-degree: 8%

---

# 透過OSGi為AEM Forms提供交易報表可記帳API {#transaction-reports-billable-apis}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/transaction-reports-billable-apis) |
| AEM 6.5 | 本文章 |

AEM Forms提供多個API來提交表單、處理檔案和轉譯檔案。 有些API是以交易入帳，其他則可供自由使用。 本檔案提供在交易報表中作為交易入帳的所有API清單。 以下是一些使用計費API的常見案例：

* 提交最適化表單、HTML5表單和表單集
* 呈現互動式通訊的列印或網頁版本
* 將檔案從一種格式轉換為另一種格式
* 平面化動態PDF檔案
* 產生記錄檔案
* 將互動式PDF檔案與另一個PDF檔案合併
* 使用AEM Workflow的指派工作步驟與檔案服務步驟
* 在最適化表單中使用最適化表單

帳單API不考慮頁數、檔案或表單的長度，或轉譯檔案的最終格式。 交易報告將交易分為兩個類別：已呈現的檔案和Forms已提交。

* **Forms已提交：** 若從使用AEM Forms建立的任何型別的表單提交資料，且資料已提交至任何資料儲存庫或資料庫，則視為表單提交。 例如，提交最適化表單、HTML5表單、PDF forms和表單集都會計為已提交的表單。 表單集中的每個表單都視為提交。 例如，如果表單集有5個表單，在提交表單集時，交易報告服務將其計為5個提交。

* **已轉譯的檔案：** 透過結合範本和資料來產生檔案、以數位方式簽署或認證檔案、使用用於檔案服務的計費檔案服務API，或將檔案從一種格式轉換為另一種格式，均被視為檔案已呈現。

>[!NOTE]
>
>交易報表UI會顯示三個類別：已提交的Forms、已轉譯的檔案以及已處理的檔案。 已轉譯的檔案和已處理的檔案都會入帳為已轉譯的檔案。

## 可記帳檔案服務API {#billable-document-services-apis}

### 產生PDF服務 {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>從支援的檔案型別建立Adobe PDF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>從支援的檔案型別建立Adobe PDF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>將Adobe PDF轉換為支援的檔案型別。 </td>
   <td>已處理的檔案<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>將Adobe PDF轉換為支援的檔案型別。 </td>
   <td>已處理的檔案<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>將Adobe PDF轉換為支援的檔案型別。 </td>
   <td>已處理的檔案<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>從HTML頁面建立PDF。</p> </td>
   <td>已處理的檔案<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>從指向PDF頁面的URL建立HTML。</td>
   <td>已處理的檔案<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>從指向PDF頁面的URL建立HTML。</td>
   <td>已處理的檔案<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>最佳化PDF以移除不必要的中繼資料，進而降低檔案大小，而不會影響品質。</td>
   <td>已處理的檔案<br /> </td>
   <td> </td>
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
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/docassurance/client/api/DocAssuranceService.html#secureDocument-com.adobe.aemfd.docmanager.Document-com.adobe.fd.docassurance.client.api.EncryptionOptions-com.adobe.fd.docassurance.client.api.SignatureOptions-com.adobe.fd.docassurance.client.api.ReaderExtensionOptions-com.adobe.fd.signatures.pdf.inputs.UnlockOptions-" target="_blank">secureDocument</a><br /> </td>
   <td>此API可讓您保護檔案的安全。 您可以使用API來簽署、認證、讀取器延伸或加密PDF檔案。</td>
   <td>已處理的文件</td>
   <td>只對secureDocument的簽署和認證操作收費。</td>
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
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>從支援的檔案型別建立Adobe PDF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>從支援的檔案型別建立Adobe PDF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 記錄檔案服務（DoR服務） {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">轉譯</a></td>
   <td>叫用指定的轉譯方法，以使用提供的引數產生記錄檔案。</td>
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
   <td>交易報告類別</td>
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
   <td> generatePDFOutputBatch API將表單範本與記錄結合，並產生PDF。 當您處理記錄批次時，交易報告服務會將每個記錄計為個別的PDF轉譯。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFile</a> 此旗標可結合多個轉譯為單一PDF檔案。 無論標幟的狀態為何，服務都會將每筆記錄計為個別的PDF轉譯。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>將XDP和PDF檔案轉換為PostScript (PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>將XDP和PDF檔案轉換為PostScript (PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>將一組XDP和PDF檔案轉換為一組PostScript (PS)、印表機命令語言(PCL)和ZPL檔案格式。 </td>
   <td>已處理的文件</td>
   <td> generatePDFOutputBatch API將表單範本與記錄結合，並產生PDF。 當您處理記錄批次時，交易報告服務會將每個記錄計為個別的PDF轉譯。 <br> 您可以使用 <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFile</a> 此旗標可結合多個轉譯為單一PDF檔案。 無論標幟的狀態為何，服務都會將每筆記錄計為個別的PDF轉譯。 </td>
  </tr>
 </tbody>
</table>

### Forms 服務 {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
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
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>將PDF檔案轉換為影像檔案清單。 支援的影像格式為JPEG、JPEG2K、PNG和TIFF。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>使用選項規格中指定的選項將FlatPDF檔案轉換為PostScript格式。</td>
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
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">解碼</a></td>
   <td>解碼Document物件中的所有條碼，並傳回org.w3c.dom.Document物件，該物件包含從條碼擷取的資料。</td>
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
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">叫用</a></td>
   <td>執行指定的DDX檔案並傳回 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">組合器結果</a> 包含結果檔案的物件。 </td>
   <td>已處理的文件</td>
   <td>下列作業不會作為交易入帳：
    <ul>
     <li>建立套件或投資組合</li>
     <li>拼接多個XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">叫用</a></td>
   <td>執行指定的DDX檔案並傳回 <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">組合器結果</a> 包含結果檔案的物件。 </td>
   <td>已處理的文件</td>
   <td>PDF Generator、Forms和輸出服務支援的所有輸入檔案格式，組合器服務都支援所有這些格式作為輸出檔案格式。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>使用指定的選項將指定的檔案轉換為PDF/A。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

當您執行下列一或多個作業時，叫用API的使用量會計為交易：
1. 從非PDF格式轉換成PDF格式。 例如，從XDP格式轉換成PDF格式，兼顧互動和非互動的通訊形式，以及從Word轉換成PDF。
1. 從PDF格式轉換為PDF/A格式。
1. 從PDF格式轉換為非PDF格式。 範例包括從PDF到影像格式的轉換或從PDF到文字格式的轉換。

>[!NOTE]
>
>* 組合器服務的叫用API可以在內部根據輸入呼叫另一個服務的計費的API。 因此，叫用API可計為無、單一或多個交易。 計算交易數取決於輸入和叫用的內部API。
>* 使用組合器服務產生的單一PDF檔案可計為無、單一或多個交易。 計算交易數目取決於提供的DDX代碼。

### PDF公用程式服務  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>將PDF檔案轉換為XDP檔案。 若要將PDF檔案成功轉換成XDP檔案，PDF檔案必須在AcroForm字典中包含XFA資料流。</td>
   <td>已處理的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 可記帳資料擷取API {#billable-data-capture-apis}

調適型表單、HTML5 Forms和表單集的所有提交事件都會計為交易。 依預設，PDF表單的提交不會作為交易入帳。 使用提供的 [交易錄製器API](record-transaction-custom-implementation.md) 將PDF forms提交記錄為交易。

### 最適化表單 {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交最適化表單</td>
   <td>提交最適化表單以設定提交動作。 </td>
   <td>已提交的表單</td>
   <td>
    <ul>
     <li>單一或兩個交易的成功提交帳戶。 計算交易數取決於用於提交的提交動作型別。 例如，透過電子郵件傳送PDF時，提交動作會計算兩個交易計數。 一個交易用於表單提交，另一個交易用於使用記錄檔案(DOR)服務產生的PDF。 </li>
     <li>在最適化表單（最適化表單集）中使用最適化表單時，只會計算單一交易。 在最適化表單中可以有任意數量的最適化表單。</li>
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
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交HTML5表單</td>
   <td>提交HTML5表單以提交在表單中設定的URL。</td>
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
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交表單集</td>
   <td>將表單集提交至表單集中設定的提交URL。</td>
   <td>已提交的表單</td>
   <td>
    <ul>
     <li>在最適化表單（最適化表單集）中使用最適化表單時，只會計算單一交易。 在最適化表單中可以有任意數量的最適化表單。</li>
     <li>HTML5 Forms表單中的每個表單都會將帳戶設定為個別交易。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi API上的可計費互動式通訊與表單中心AEM工作流程 {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

在OSGi上指派以表單為中心的AEM Workflow的工作和檔案服務步驟，以及互動式通訊的所有轉譯，並作為交易入帳。 在製作執行個體上預覽互動式通訊，以及使用代理程式UI在發佈執行個體上預覽，不會計為交易。 如果工作流程步驟將交易入帳，但工作流程無法完成，則不會迴轉交易計數。

### 互動式通訊 - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>轉譯Web管道</td>
   <td>開啟互動式通訊的Web版本。</td>
   <td>已呈交的文件</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### 互動式通訊 — Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>說明</td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">轉譯</a> (轉換成PDF)</td>
   <td>產生互動式通訊的PDF版本。</td>
   <td>已呈交的文件</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### OSGi上的表單中心AEM工作流程  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>使用案例</p> </td>
   <td>交易報告類別</td>
   <td>其他資訊</td>
  </tr>
  <tr>
   <td>提交指派工作步驟</td>
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
   <td>從Agent UI提互動動式通訊(Print Channel)至工作流程</td>
   <td>已呈交的文件</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 將可記帳API記錄為自訂程式碼的交易 {#recording-billable-apis-as-transactions-for-custom-code}

提交PDF表單、使用代理程式UI預覽互動式通訊、使用非標準表單提交和自訂實施等動作不會計為交易。 AEM Forms提供API來記錄此類動作，例如交易。 您可以從自訂實施呼叫API至 [記錄交易](/help/forms/using/record-transaction-custom-implementation.md).

## 相關文章 {#related-articles}

* [在OSGi上使用AEM Forms的交易報表概觀](../../forms/using/transaction-reports-overview.md)
* [在OSGi上檢視和瞭解AEM Forms的交易報表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [在OSGi上記錄AEM Forms的自訂實作交易](/help/forms/using/record-transaction-custom-implementation.md)
