---
title: 建立文檔輸出流
seo-title: Creating Document Output Streams
description: 使用輸出服務將文檔轉換為PDF（包括PDF/A文檔）、PostScript、打印機控制語言(PCL)和Zebra - ZPL、Intermec - IPL、Datamax - DPL和TecToshiba - TPCL標籤格式。
seo-description: Use the Output service to convert documents as PDF (including PDF/A documents), PostScript, Printer Control Language (PCL), and Zebra - ZPL, Intermec - IPL, Datamax - DPL, and TecToshiba - TPCL label formats.
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 74882ccf78a62d543f1598f12ee009f9922c18a4
workflow-type: tm+mt
source-wordcount: '19016'
ht-degree: 0%

---

# 建立文檔輸出流  {#creating-document-output-streams}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於輸出服務**

輸出服務可讓您將文檔輸出為PDF（包括PDF/A文檔）、PostScript、打印機控制語言(PCL)，以及以下標籤格式：

* 澤布拉 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用輸出服務，可以將XML表單資料與表單設計合併，並將文檔輸出到網路打印機或檔案。

有兩種方式可將表單設計（XDP檔案）傳遞至輸出服務。 您可以將包含表單設計的`com.adobe.idp.Document`例項傳遞至輸出服務。 或者，您可以傳遞指定表單設計位置的URI值。 在&#x200B;*使用AEM表單寫程式*&#x200B;中討論了這兩種方法。

>[!NOTE]
>
>輸出服務不支援包含應用程式對象特定指令碼的Acroform PDF文檔。 不會呈現包含應用程式對象特定指令碼的Acroform PDF文檔。

以下各節說明如何使用URI值將表單設計傳遞至輸出服務：

* [建立PDF文檔](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A文檔](creating-document-output-streams.md#creating-pdf-a-documents)

以下各節說明如何在`com.adobe.idp.Document`例項內傳遞表單設計：

* [將內容服務中的檔案（已過時）傳遞至輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

在決定要使用哪種技術時，考量之一是，如果您要從其他AEM Forms服務取得表單設計，然後在`com.adobe.idp.Document`例項內傳遞。 *將檔案傳遞至輸出服務*&#x200B;和&#x200B;*使用片段建立PDF檔案*&#x200B;兩節都會說明如何從其他AEM Forms服務取得表單設計。 第一個區段會從「內容服務」擷取表單設計（已淘汰）。 第二個部分從組合器服務中檢索表單設計。

如果從固定位置（如檔案系統）獲取表單設計，則可以使用其中一種技術。 也就是說，您可以為XDP檔案指定URI值或使用`com.adobe.idp.Document`實例。

要在建立PDF文檔時傳遞指定表單設計位置的URI值，請使用`generatePDFOutput`方法。 同樣地，要在建立PDF文檔時將`com.adobe.idp.Document`實例傳遞到輸出服務，請使用`generatePDFOutput2`方法。

在將輸出流發送到網路打印機時，您也可以使用其中一種技術。 要通過傳遞包含表單設計的`com.adobe.idp.Document`實例將輸出流發送到打印機，請使用`sendToPrinter2`方法。 要通過傳遞URI值向打印機發送輸出流，請使用`sendToPrinter`方法。 *向打印機發送打印流*&#x200B;部分使用`sendToPrinter`方法。

您可以使用輸出服務來完成下列工作：

* [建立PDF文檔](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A文檔](creating-document-output-streams.md#creating-pdf-a-documents)
* [將內容服務中的檔案（已過時）傳遞至輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [打印到檔案](creating-document-output-streams.md#printing-to-files)
* [發送打印流到打印機](creating-document-output-streams.md#sending-print-streams-to-printers)
* [建立多個輸出檔案](creating-document-output-streams.md#creating-multiple-output-files)
* [建立搜尋規則](creating-document-output-streams.md#creating-search-rules)
* [拼合PDF文檔](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立PDF文檔 {#creating-pdf-documents}

您可以使用輸出服務來建立基於表單設計和您提供的XML表單資料的PDF文檔。 由輸出服務建立的PDF檔案不是互動式PDF檔案；用戶無法輸入或修改表單資料。

如果要建立用於長期儲存的PDF文檔，建議您建立PDF/A文檔。 （請參閱[建立PDF/A文檔](creating-document-output-streams.md#creating-pdf-a-documents)。）

若要建立可讓使用者輸入資料的互動式PDF表單，請使用Forms服務。 (請參閱[轉譯互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)。)

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要建立PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料源。
1. 設定PDF運行時選項。
1. 設定呈現運行時選項。
1. 生成PDF文檔。
1. 檢索操作的結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`對象。

**參考XML資料源**

要將資料與表單設計合併，必須引用包含資料的XML資料源。 您計畫填入資料的每個表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

請考量下列貸款申請表範例。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

要將資料合併到此表單設計中，必須建立與表單對應的XML資料源。 以下XML表示與抵押申請表示例對應的XDP XML資料源。

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

**設定PDF運行時選項**

建立PDF文檔時設定檔案URI選項。 此選項指定輸出服務生成的PDF檔案的名稱和位置。

>[!NOTE]
>
>您可以用寫程式方式從輸出服務返回的複雜資料類型中檢索PDF文檔，而不設定檔案URI運行時選項。 但是，通過設定檔案URI運行時選項，您不需要建立應用程式邏輯，以寫程式方式檢索PDF文檔。

**設定呈現運行時選項**

建立PDF文檔時，可以設定渲染運行時選項。 雖然這些選項不是必需的（與所需的PDF運行時選項不同），但您可以執行諸如提高輸出服務的效能之類的任務。 例如，您可以快取輸出服務用來改善其效能的表單設計。

如果您使用標籤的Acrobat表單作為輸入，則無法使用輸出服務Java或Web服務API來關閉標籤的設定。 如果嘗試以寫程式方式將此選項設定為`false`，則結果PDF文檔仍被標籤。

>[!NOTE]
>
>如果未指定呈現運行時選項，則使用預設值。 有關呈現運行時選項的資訊，請參見`RenderOptionsSpec`類引用。 (請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**生成PDF文檔**

參考包含表單資料的有效XML資料源並設定運行時選項後，可以調用輸出服務，從而生成PDF文檔。

生成PDF文檔時，可以指定輸出服務建立PDF文檔所需的URI值。 表單設計可儲存在伺服器檔案系統等位置，或儲存為AEM Forms應用程式的一部分。 作為Forms應用程式一部分而存在的表單設計（或其他資源，例如影像檔案），可使用內容根URI值`repository:///`來參照。 例如，請考慮以下名為&#x200B;*Loan.xdp*&#x200B;的表單設計，該表單設計位於名為&#x200B;*Applications/FormsApplication*&#x200B;的Forms應用程式中：

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

若要存取上圖所示的Loan.xdp檔案，請指定`repository:///Applications/FormsApplication/1.0/FormsFolder/`作為傳遞至`OutputClient`物件的`generatePDFOutput`方法的第三個參數。 指定表單名稱(*Loan.xdp*)作為傳遞至`OutputClient`物件的`generatePDFOutput`方法的第二個參數。

如果XDP檔案包含影像（或其他資源，例如片段），請將資源放置在與XDP檔案相同的應用程式資料夾中。 AEM Forms使用內容根URI作為解析影像參考的基礎路徑。 例如，如果Loan.xdp檔案包含影像，請確定您將影像放置在`Applications/FormsApplication/1.0/FormsFolder/`中。

>[!NOTE]
>
>調用`OutputClient`對象的`generatePDFOutput`或`generatePrintedOutput`方法時，可以引用Forms應用程式URI。

>[!NOTE]
>
>要查看通過引用位於Forms應用程式中的XDP來建立PDF文檔的完整快速入門，請參閱[快速入門（EJB模式）:使用Java API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)根據應用程式XDP檔案建立PDF檔案。

**檢索操作的結果**

在輸出服務執行操作後，它將返回各種資料項，如指定操作是否成功的狀態XML資料。

**另請參閱**

[使用Java API建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[使用Web服務API建立PDF文檔](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立PDF檔案 {#create-a-pdf-document-using-the-java-api}

使用輸出API(Java)建立PDF文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。

1. 參考XML資料源。

   * 建立`java.io.FileInputStream`對象，該對象表示用於通過使用其建構子並傳遞指定XML檔案位置的字串值來填充PDF文檔的XML資料源。
   * 使用其建構子建立`com.adobe.idp.Document`物件。 傳遞`java.io.FileInputStream`物件。

1. 設定PDF運行時選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`物件。
   * 調用`PDFOutputOptionsSpec`對象的`setFileURI`方法，設定檔案URI選項。 傳遞一個字串值，該字串值指定輸出服務生成的PDF檔案的位置。 「檔案URI」選項相對於托管AEM Forms的J2EE應用程式伺服器，而不是客戶端電腦。

1. 設定呈現運行時選項。

   * 使用其建構子建立`RenderOptionsSpec`物件。
   * 調用`RenderOptionsSpec`對象的`setCacheEnabled`並傳遞`true`，快取表單設計以改進輸出服務的效能。

   >[!NOTE]
   >
   >如果輸入文檔是Acrobat表單(在Acrobat中建立的表單)或已簽名或認證的XFA文檔，則不能使用`RenderOptionsSpec`對象的`setPdfVersion`方法來設定PDF文檔的版本。 輸出PDF文檔保留原始PDF版本。 同樣，如果輸入文檔是Acrobat表單或已簽名或認證的XFA文檔，則不能通過調用`RenderOptionsSpec`對象的`setTaggedPDF`方法來設定帶標籤的Adobe PDF選項。

   >[!NOTE]
   >
   >如果輸入PDF文檔經過認證或數字簽名，則不能使用`RenderOptionsSpec`對象的`setLinearizedPDF`方法來設定線性化的PDF選項。 （請參閱[數位簽署PDF檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。）*

1. 生成PDF文檔。

   叫用`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定表單設計所在的內容根。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `com.adobe.idp.Document`對象，該對象包含要與表單設計合併的資料的XML資料源。

   `generatePDFOutput`方法返回包含操作結果的`OutputResult`對象。

   >[!NOTE]
   >
   >叫用`generatePDFOutput`方法產生PDF檔案時，請注意，您無法將資料與已簽署或認證的XFA PDF表單合併。 （請參閱[數字簽名和認證文檔&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。）*

   >[!NOTE]
   >
   >`OutputResult`對象的`getRecordLevelMetaDataList`方法返回&#x200B;`null`*。*

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput2`方法，以建立PDF檔案。 (請參閱[將內容服務中的文檔（已廢止）傳遞到輸出服務&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 檢索操作的結果。

   * 調用`OutputResult`對象的`getStatusDoc`方法，檢索表示`generatePDFOutput`操作狀態的`com.adobe.idp.Document`對象。 此方法會傳回狀態XML資料，指定操作是否成功。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為.xml。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案（確保使用`getStatusDoc`方法返回的`com.adobe.idp.Document`對象）。

   儘管輸出服務將PDF文檔寫入由傳遞到`PDFOutputOptionsSpec`對象的`setFileURI`方法的參數指定的位置，但通過調用`OutputResult`對象的`getGeneratedDoc`方法，您可以以寫程式方式檢索PDF/A文檔。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）:使用Java API建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立PDF文檔 {#create-a-pdf-document-using-the-web-service-api}

使用輸出API（Web服務）建立PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料源。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存將與PDF文檔合併的XML資料。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示包含表單資料的XML檔案的檔案位置。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 設定PDF運行時選項

   * 使用其建構子建立`PDFOutputOptionsSpec`物件。
   * 通過分配字串值來設定檔案URI選項，該字串值指定輸出服務為`PDFOutputOptionsSpec`對象的`fileURI`資料成員生成的PDF檔案的位置。 「檔案URI」選項相對於托管AEM Forms的J2EE應用程式伺服器，而不是客戶端電腦。

1. 設定呈現運行時選項。

   * 使用其建構子建立`RenderOptionsSpec`物件。
   * 將值`true`分配給`RenderOptionsSpec`對象的`cacheEnabled`資料成員，快取表單設計以改進輸出服務的效能。

   >[!NOTE]
   >
   >如果輸入文檔是Acrobat表單(在Acrobat中建立的表單)或已簽名或認證的XFA文檔，則不能使用`RenderOptionsSpec`對象的`setPdfVersion`方法來設定PDF文檔的版本。 輸出PDF文檔保留原始PDF版本。 同樣，如果輸入文檔是Acrobat表單或已簽名或認證的XFA文檔，則不能通過調用`RenderOptionsSpec`對象的`setTaggedPDF`*方法來設定標籤的Adobe PDF選項。*

   >[!NOTE]
   >
   >如果輸入PDF文檔經過認證或數字簽名，則不能使用`RenderOptionsSpec`對象的`linearizedPDF`成員來設定線性化的PDF選項。 （請參閱[數位簽署PDF檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。）*

1. 生成PDF文檔。

   叫用`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定表單設計所在的內容根。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `BLOB`對象，該對象包含要與表單設計合併的資料的XML資料源。
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以描述文檔的生成元資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。 （此參數值僅對於Web服務調用是必需的）。
   * 包含操作結果的`OutputResult`對象。 （此參數值僅對於Web服務調用是必需的）。

   >[!NOTE]
   >
   >叫用`generatePDFOutput`方法產生PDF檔案時，請注意，您無法將資料與已簽署或認證的XFA PDF表單合併。 （請參閱[數字簽名和認證文檔&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。）*

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput2`方法，以建立PDF檔案。 (請參閱[將內容服務中的文檔（已廢止）傳遞到輸出服務&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 檢索操作的結果。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為.xml。
   * 建立位元組陣列，用於儲存`OutputServiceService`對象的`generatePDFOutput`方法（第八個參數）填入結果資料的`BLOB`對象的資料內容。 獲取`BLOB`對象`MTOM` `field`的值，填入位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

   另請參閱

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >不建議使用`OutputServiceService`物件的`generateOutput`方法。

## 建立PDF/A文檔 {#creating-pdf-a-documents}

您可以使用輸出服務來建立PDF/A文檔。 由於PDF/A是用於長期保存文檔內容的存檔格式，因此所有字型都會嵌入並解壓縮檔案。 因此，PDF/A文檔通常比標準PDF文檔大。 此外，PDF/A檔案不包含音訊和視訊內容。 與其他輸出服務任務一樣，您提供表單設計和資料以與表單設計合併，以建立PDF/A文檔。

PDF/A-1規範包含兩個一致性級別，即a和b。兩者的主要差異在於邏輯結構（協助工具）支援，這不是一致性層級b的必要條件。無論一致性級別如何，PDF/A-1都規定所有字型都嵌入生成的PDF/A文檔中。

雖然PDF/A是封存PDF檔案的標準，但如果標準PDF檔案符合您公司的需求，則使用PDF/A進行封存並非強制性。 PDF/A標準的目的是建立可長時間儲存的PDF檔案，並符合檔案保存需求。 例如，URL無法嵌入到PDF/A中，因為隨著時間的推移，該URL可能變為無效。

您的組織必須評估自己的需求、您要保留文檔的時間長度、檔案大小考量事項，並確定您自己的歸檔戰略。 通過使用DocConverter服務，可以以寫程式方式確定PDF文檔是否符合PDF/A。 （請參閱[以程式設計方式決定PDF/A相容性](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)。）

PDF/A文檔必須使用在表單設計中指定的字型，且字型不能替換。 因此，如果位於PDF檔案中的字型在主機作業系統(OS)上不可用，則會發生例外狀況。

在Acrobat中開啟PDF/A檔案時，會顯示訊息，確認該檔案為PDF/A檔案，如下圖所示。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM網站有PDF/A常見問題集區段，您可以從[https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml)存取。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_65)。

### 步驟摘要 {#summary_of_steps-1}

要建立PDF/A文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料源。
1. 設定PDF/A執行階段選項。
1. 設定呈現運行時選項。
1. 生成PDF/A文檔。
1. 檢索操作的結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立自訂應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`對象。

**參考XML資料源**

要將資料與表單設計合併，必須引用包含資料的XML資料源。 要填入資料的每個表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

**設定PDF/A運行時選項**

建立PDF/A文檔時，可以設定「檔案URI」選項。 URI相對於托管AEM Forms的J2EE應用程式伺服器。 也就是說，如果您設定C:\Adobe ，則檔案會寫入伺服器上的資料夾，而非用戶端電腦。 URI指定輸出服務生成的PDF/A檔案的名稱和位置。

**設定呈現運行時選項**

建立PDF/A文檔時，可以設定渲染運行時選項。 您可以設定的兩個PDF/A相關選項是`PDFAConformance`和`PDFARevisionNumber`值。 `PDFAConformance`值表示PDF檔案如何遵守指定如何保留長期電子檔案的要求。 此選項的有效值為`A`和`B`。 有關a級和b級一致性的資訊，請參閱標題為&#x200B;*ISO 19005-1 Document management*&#x200B;的PDF/A-1 ISO規範。

`PDFARevisionNumber`值指的是PDF/A文檔的修訂號。 有關PDF/A文檔的修訂號的資訊，請參閱標題為&#x200B;*ISO 19005-1文檔管理*&#x200B;的PDF/A-1 ISO規範。

>[!NOTE]
>
>建立PDF/A 1A文檔時，無法將標籤的Adobe PDF選項設定為`false`。 PDF/A 1A將始終是帶標籤的PDF文檔。 另外，建立PDF/A 1B文檔時，不能將標籤的Adobe PDF選項設定為`true`。 PDF/A 1B將始終是未標籤的PDF文檔。

**生成PDF/A文檔**

參考包含表單資料的有效XML資料源並設定運行時選項後，可以調用輸出服務，使其生成PDF/A文檔。

**檢索操作的結果**

在輸出服務執行操作後，它返回各種資料項，如指定操作是否成功的XML資料。

**另請參閱**

[使用Java API建立PDF/A檔案](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[使用Web服務API建立PDF/A文檔](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立PDF/A檔案 {#create-a-pdf-a-document-using-the-java-api}

使用輸出API(Java)建立PDF/A文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。

1. 參考XML資料源。

   * 建立`java.io.FileInputStream`對象，該對象表示用於填充PDF/A文檔的XML資料源，方法是使用其建構子並傳遞一個指定XML檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定PDF/A執行階段選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`物件。
   * 調用`PDFOutputOptionsSpec`對象的`setFileURI`方法，設定檔案URI選項。 傳遞一個字串值，該字串值指定輸出服務生成的PDF檔案的位置。 「檔案URI」選項相對於托管AEM Forms的J2EE應用程式伺服器，而不是客戶端電腦。

1. 設定呈現運行時選項。

   * 使用其建構子建立`RenderOptionsSpec`物件。
   * 調用`RenderOptionsSpec`對象的`setPDFAConformance`方法並傳遞指定一致性級別的`PDFAConformance`枚舉值，以設定`PDFAConformance`值。 例如，要指定一致性級別A，請傳遞`PDFAConformance.A`。
   * 調用`RenderOptionsSpec`對象的`setPDFARevisionNumber`方法並傳遞`PDFARevisionNumber.Revision_1`來設定`PDFARevisionNumber`值。

   >[!NOTE]
   >
   >PDF/A文檔的PDF版本為1.4，無論您為`RenderOptionsSpec`對象的&#x200B;`setPdfVersion`*方法指定哪個值。*

1. 生成PDF/A文檔。

   調用`OutputClient`對象的`generatePDFOutput`方法並傳遞以下值，建立PDF/A文檔：

   * `TransformationFormat`枚舉值。 要生成PDF/A文檔，請指定`TransformationFormat.PDFA`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定表單設計所在的內容根。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `com.adobe.idp.Document`對象，該對象包含要與表單設計合併的資料的XML資料源。

   `generatePDFOutput`方法返回包含操作結果的`OutputResult`對象。

   >[!NOTE]
   >
   >`OutputResult`物件的`getRecordLevelMetaDataList`方法會傳回`null`。

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput`2方法，以建立PDF /A檔案。 (請參閱[將內容服務中的檔案（已過時）傳遞至輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 檢索操作的結果。

   * 通過調用`OutputResult`對象的`getStatusDoc`方法，建立表示`generatePDFOutput`方法狀態的`com.adobe.idp.Document`對象。
   * 建立將包含操作結果的`java.io.File`對象。 請確定副檔名為.xml。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案（確保使用`getStatusDoc`方法返回的`com.adobe.idp.Document`對象）。

   >[!NOTE]
   >
   >儘管輸出服務將PDF/A文檔寫入到由傳遞給`PDFOutputOptionsSpec`對象的`setFileURI`方法的參數指定的位置，但通過調用`OutputResult`對象的`getGeneratedDoc`方法，您可以以寫程式方式檢索PDF/A文檔。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API建立PDF/A檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[正在設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服務API建立PDF/A文檔 {#create-a-pdf-a-document-using-the-web-service-api}

使用輸出API（Web服務）建立PDF/A文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料源。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存將與PDF/A文檔合併的資料。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列內容，以填入`BLOB`物件。

1. 設定PDF/A執行階段選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`物件。
   * 通過分配字串值來設定檔案URI選項，該字串值指定輸出服務為`PDFOutputOptionsSpec`對象的`fileURI`資料成員生成的PDF檔案的位置。 「檔案URI」選項相對於托管AEM Forms的J2EE應用程式伺服器，而不是客戶端電腦

1. 設定呈現運行時選項。

   * 使用其建構子建立`RenderOptionsSpec`物件。
   * 將`PDFAConformance`枚舉值分配給`RenderOptionsSpec`對象的`PDFAConformance`資料成員，以設定`PDFAConformance`值。 例如，要指定一致性級別A，請將`PDFAConformance.A`分配給此資料成員。
   * 將`PDFARevisionNumber`枚舉值分配給`RenderOptionsSpec`對象的`PDFARevisionNumber`資料成員，以設定`PDFARevisionNumber`值。 將`PDFARevisionNumber.Revision_1`分配給此資料成員。

   >[!NOTE]
   >
   >PDF/A文檔的PDF版本為1.4，無論您指定哪個值。

1. 生成PDF/A文檔。

   叫用`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * TransformationFormat枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDFA`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定表單設計所在的內容根。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `BLOB`對象，該對象包含要與表單設計合併的資料的XML資料源。
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以描述文檔的生成元資料填充此對象。 （此參數值僅在Web服務調用時是必需的。）
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。 （此參數值僅在Web服務調用時是必需的。）
   * 包含操作結果的`OutputResult`對象。 （此參數值僅在Web服務調用時是必需的。）

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput`2方法，以建立PDF /A檔案。 (請參閱[將內容服務中的檔案（已過時）傳遞至輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 檢索操作的結果。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為.xml。
   * 建立位元組陣列，用於儲存`OutputServiceService`對象的`generatePDFOutput`方法（第八個參數）填入結果資料的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`欄位的值，填入位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將內容服務中的檔案（已過時）傳遞至輸出服務 {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

輸出服務會轉譯非互動式PDF表單，此表單以表單設計為基礎，通常會儲存為XDP檔案，並在Designer中建立。 您可以將包含表單設計的`com.adobe.idp.Document`物件傳遞至輸出服務。 然後，輸出服務將呈現位於`com.adobe.idp.Document`對象中的表單設計。

將`com.adobe.idp.Document`物件傳遞至輸出服務的好處，是其他AEM Forms服務操作會傳回`com.adobe.idp.Document`例項。 也就是說，可以從其他服務操作獲取`com.adobe.idp.Document`實例並呈現它。 例如，假設XDP檔案儲存在名為`/Company Home/Form Designs`的內容服務（已廢止）節點中，如下圖所示。

您可以以程式設計方式從內容服務擷取Loan.xdp（已淘汰），並將XDP檔案傳遞至`com.adobe.idp.Document`物件內的輸出服務。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

若要將從內容服務取得的檔案（已淘汰）傳遞至輸出服務，請執行下列工作：

1. 包含專案檔案。
1. 建立輸出和文檔管理客戶端API對象。
1. 從內容服務擷取表單設計（已淘汰）。
1. 轉譯非互動式PDF表單。
1. 對資料流執行動作。

**包含項目檔案**

將必要的檔案加入您的開發專案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立輸出和文檔管理客戶端API對象**

在以程式設計方式執行輸出服務API操作之前，請建立輸出客戶端API對象。 此外，由於此工作流程會從內容服務擷取XDP檔案（已淘汰），因此請建立檔案管理API物件。

**從內容服務擷取表單設計（已淘汰）**

使用Java或Web服務API從「內容服務」擷取XDP檔案（已淘汰）。 在`com.adobe.idp.Document`實例(或`BLOB`實例（如果您使用Web服務）中返回XDP檔案。 然後，您可以將`com.adobe.idp.Document`實例傳遞到Output服務。

**轉譯非互動式PDF表單**

若要呈現非互動式表單，請將從內容服務傳回的`com.adobe.idp.Document`例項（已過時）傳遞至輸出服務。

>[!NOTE]
>
>名為`generatePDFOutput2`和g `eneratePrintedOutput2`的兩種新方法接受包含表單設計的`com.adobe.idp.Document`對象。 在向網路打印機發送打印流時，還可以將包含表單設計的`com.adobe.idp.Document`傳遞到輸出服務。

**使用表單資料流執行動作**

您可以將非互動式表單儲存為PDF檔案。 您可在Adobe Reader或Acrobat中檢視表單。

**另請參閱**

[使用Java API將檔案傳遞至輸出服務](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[使用網站服務API將檔案傳遞至輸出服務](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### 使用Java API將檔案傳遞至輸出服務 {#pass-documents-to-the-output-service-using-the-java-api}

使用輸出服務與內容服務（已過時）API(Java)，傳遞從內容服務擷取的檔案（已過時）:

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立輸出和文檔管理客戶端API對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`DocumentManagementServiceClientImpl`物件。

1. 從內容服務擷取表單設計（已淘汰）。

   調用`DocumentManagementServiceClientImpl`對象的`retrieveContent`方法並傳遞以下值：

   * 一個字串值，它指定添加內容的儲存區。 預設儲存為`SpacesStore`。 此值是必要參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值是必要參數。
   * 指定版本的字串值。 此值是選用參數，您可以傳遞空白字串。 在此情況下，會擷取最新版本。

   `retrieveContent`方法返回包含XDP檔案的`CRCResult`對象。 調用`CRCResult`對象的`getDocument`方法來檢索`com.adobe.idp.Document`實例。

1. 轉譯非互動式PDF表單。

   調用`OutputClient`對象的`generatePDFOutput2`方法並傳遞以下值：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 一個字串值，它指定影像等其他資源所在的內容根。
   * 代表表單設計的`com.adobe.idp.Document`物件（使用`CRCResult`物件的`getDocument`方法傳回的例項）。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `com.adobe.idp.Document`對象，該對象包含要與表單設計合併的資料的XML資料源。

   `generatePDFOutput2`方法返回包含操作結果的`OutputResult`對象。

1. 對表單資料流執行動作。

   * 調用`OutputResult`對象的`getGeneratedDoc`方法，檢索表示非交互表單的`com.adobe.idp.Document`對象。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案（確保使用`getGeneratedDoc`方法返回的`com.adobe.idp.Document`對象）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）:使用Java API將檔案傳遞至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[快速入門（SOAP模式）:使用Java API將檔案傳遞至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將檔案傳遞至輸出服務 {#pass-documents-to-the-output-service-using-the-web-service-api}

使用輸出服務與內容服務（已過時）API（網站服務），傳遞從內容服務擷取的檔案（已過時）:

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 由於此客戶端應用程式調用了兩個AEM Forms服務，因此請建立兩個服務引用。 為與輸出服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   為與文檔管理服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   因為`BLOB`資料類型對兩個服務引用都是通用的，因此在使用`BLOB`資料類型時，請完全限定該資料類型。 在相應的Web服務快速入門中，所有`BLOB`實例都完全限定。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立輸出和文檔管理客戶端API對象。

   * 使用其預設建構子建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對`DocumentManagementServiceClient`服務客戶端重複這些步驟。

1. 從內容服務擷取表單設計（已淘汰）。

   叫用`DocumentManagementServiceClient`物件的`retrieveContent`方法並傳遞下列值，以擷取內容：

   * 一個字串值，它指定添加內容的儲存區。 預設儲存為`SpacesStore`。 此值是必要參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值是必要參數。
   * 指定版本的字串值。 此值是選用參數，您可以傳遞空白字串。 在此情況下，會擷取最新版本。
   * 儲存瀏覽連結值的字串輸出參數。
   * 儲存內容的`BLOB`輸出參數。 您可以使用此輸出參數來擷取內容。
   * 儲存內容屬性的`ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType`輸出參數。
   * `CRCResult`輸出參數。 您可以使用`BLOB`輸出參數來擷取內容，而不使用此物件。

1. 轉譯非互動式PDF表單。

   調用`OutputServiceClient`對象的`generatePDFOutput2`方法並傳遞以下值：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 一個字串值，它指定影像等其他資源所在的內容根。
   * 代表表單設計的`BLOB`物件(使用內容服務傳回的`BLOB`例項（已廢止）)。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `BLOB`對象，該對象包含要與表單設計合併的資料的XML資料源。
   * 由`generatePDFOutput2`方法填入的輸出`BLOB`對象。 `generatePDFOutput2`方法會以描述文檔的生成元資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * 包含操作結果的輸出`OutputResult`對象。 （此參數值僅對於Web服務調用是必需的）。

   `generatePDFOutput2`方法返回包含非互動式PDF表單的`BLOB`對象。

1. 對表單資料流執行動作。

   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示互動式PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存從`generatePDFOutput2`方法檢索到的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 將儲存庫中的文檔傳遞到輸出服務 {#passing-documents-located-in-the-repository-to-the-output-service}

輸出服務會轉譯非互動式PDF表單，此表單以表單設計為基礎，通常會儲存為XDP檔案，並在Designer中建立。 您可以將包含表單設計的`com.adobe.idp.Document`物件傳遞至輸出服務。 然後，輸出服務將呈現位於`com.adobe.idp.Document`對象中的表單設計。

將`com.adobe.idp.Document`物件傳遞至輸出服務的好處，是其他AEM Forms服務操作會傳回`com.adobe.idp.Document`例項。 也就是說，可以從其他服務操作獲取`com.adobe.idp.Document`實例並呈現它。 例如，假設XDP檔案儲存在AEM Forms存放庫中，如下圖所示。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

*FormsFolder*&#x200B;資料夾是AEM Forms儲存庫中用戶定義的位置（此位置是示例，預設不存在）。 在此示例中，此資料夾中存在名為Loan.xdp的表單設計。 除了表單設計外，其他表單輔助資料（如影像）也可以儲存在此位置。 位於AEM Forms存放庫中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

您可以以程式設計方式從AEM Forms存放庫擷取Loan.xdp，並傳遞至`com.adobe.idp.Document`物件內的輸出服務。

您可以使用兩種方式之一，根據存放庫中的XDP檔案建立PDF。 您可以參照傳遞XDP位置，或以程式設計方式從存放庫擷取XDP，並傳遞至XDP檔案內的輸出服務。

[快速入門（EJB模式）:使用Java API根據應用程式XDP檔案建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （顯示如何參考傳遞XDP檔案的位置）。

[快速入門（EJB模式）:使用Java API將AEM Forms存放庫中的檔案傳遞至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (說明如何以程式設計方式從AEM Forms存放庫擷取XDP檔案，並傳遞至執行個體內的輸出 `com.adobe.idp.Document` 服務)。（本節討論如何執行此任務）

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

要將從AEM Forms儲存庫獲取的文檔傳遞到輸出服務，請執行以下任務：

1. 包含專案檔案。
1. 建立輸出和文檔管理客戶端API對象。
1. 從AEM Forms存放庫擷取表單設計。
1. 轉譯非互動式PDF表單。
1. 對資料流執行動作。

**包含項目檔案**

將必要的檔案加入您的開發專案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立輸出和文檔管理客戶端API對象**

在以程式設計方式執行輸出服務API操作之前，請建立輸出客戶端API對象。 此外，由於此工作流程會從內容服務擷取XDP檔案（已淘汰），因此請建立檔案管理API物件。

**從AEM Forms存放庫擷取表單設計**

使用存放庫API從AEM Forms存放庫擷取XDP檔案。 （請參閱[讀取資源](/help/forms/developing/aem-forms-repository.md#reading-resources)。）

在`com.adobe.idp.Document`實例(或`BLOB`實例（如果您使用Web服務）中返回XDP檔案。 然後，您可以將`com.adobe.idp.Document`實例傳遞到輸出服務。

**轉譯非互動式PDF表單**

若要呈現非互動式表單，請傳遞使用AEM Forms存放庫API傳回的`com.adobe.idp.Document`例項。

>[!NOTE]
>
>名為`generatePDFOutput2`和`generatePrintedOutput2`的兩種新方法接受包含表單設計的`com.adobe.idp.Document`物件。 在向網路打印機發送打印流時，還可以將包含表單設計的`com.adobe.idp.Document`傳遞到輸出服務。

**使用表單資料流執行動作**

您可以將非互動式表單儲存為PDF檔案。 您可在Adobe Reader或Acrobat中檢視表單。

**另請參閱**

[使用Java API將存放庫中的檔案傳遞至輸出服務](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### 使用Java API將存放庫中的檔案傳遞至輸出服務 {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

使用輸出服務和儲存庫API(Java)傳遞從儲存庫檢索到的文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar和adobe-repository-client.jar。

1. 建立輸出和文檔管理客戶端API對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`DocumentManagementServiceClientImpl`物件。

1. 從AEM Forms存放庫擷取表單設計。

   調用`ResourceRepositoryClient`對象的`readResourceContent`方法，並將指定URI位置的字串值傳遞到XDP檔案。 例如， `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。 此值是必填的。 此方法會傳回代表XDP檔案的`com.adobe.idp.Document`例項。

1. 轉譯非互動式PDF表單。

   調用`OutputClient`對象的`generatePDFOutput2`方法並傳遞以下值：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 一個字串值，它指定影像等其他資源所在的內容根。 例如， `repository:///Applications/FormsApplication/1.0/FormsFolder/`。
   * 代表表單設計的`com.adobe.idp.Document`物件（使用`ResourceRepositoryClient`物件的`readResourceContent`方法傳回的例項）。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `com.adobe.idp.Document`對象，該對象包含要與表單設計合併的資料的XML資料源。

   `generatePDFOutput2`方法返回包含操作結果的`OutputResult`對象。

1. 對表單資料流執行動作。

   * 調用`OutputResult`對象的`getGeneratedDoc`方法，檢索表示非交互表單的`com.adobe.idp.Document`對象。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案（確保使用`getGeneratedDoc`方法返回的`com.adobe.idp.Document`對象）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）:使用Java API將AEM Forms存放庫中的檔案傳遞至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用片段建立PDF檔案 {#creating-pdf-documents-using-fragments}

您可以使用輸出和組合器服務來建立基於片段的輸出流，如PDF文檔。 組合器服務組合基於位於多個XDP檔案中的片段的XDP文檔。 已裝配的XDP文檔將傳遞至輸出服務，該服務將建立PDF文檔。 儘管此工作流顯示正在生成的PDF文檔，但輸出服務可為此工作流生成其他輸出類型，如ZPL。 PDF檔案僅用於討論用途。

下圖顯示此工作流程。

![cp_cp_outputsamsemble片段](assets/cp_cp_outputassemblefragments.png)

在閱讀&#x200B;*使用片段建立PDF文檔*&#x200B;之前，建議您熟悉使用組合器服務來組合多個XDP文檔。 （請參閱[組裝多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)。）

>[!NOTE]
>
>您也可以將組合器服務組合的表單設計傳遞至Forms服務，而非輸出服務。 輸出服務與Forms服務的主要差異在於Forms服務會產生互動式PDF檔案，而輸出服務會產生非互動式PDF檔案。 此外，Forms服務無法產生ZPL等基於打印機的輸出流。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

要根據片段建立PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出和組合器客戶端對象。
1. 使用組合器服務生成表單設計。
1. 使用輸出服務生成PDF文檔。
1. 將PDF文檔另存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立輸出和組合器客戶端對象**

在以程式設計方式執行輸出服務API操作之前，請建立輸出客戶端API對象。 另外，由於此工作流調用組合器服務來建立表單設計，因此請建立組合器客戶端API對象。

**使用組合器服務生成表單設計**

使用組合器服務使用片段生成表單設計。 組合器服務返回包含表單設計的`com.adobe.idp.Document`實例。

**使用輸出服務生成PDF文檔**

您可以使用輸出服務使用組合器服務建立的窗體設計生成PDF文檔。 傳遞組合器服務返回到輸出服務的`com.adobe.idp.Document`實例。

**將PDF檔案另存為PDF檔案**

輸出服務生成PDF文檔後，您可以將其另存為PDF檔案。

**另請參閱**

[使用Java API根據片段建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[使用網站服務API根據片段建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[組裝多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[建立PDF文檔](creating-document-output-streams.md#creating-pdf-documents)

### 使用Java API根據片段建立PDF檔案 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

使用輸出服務API和組合器服務API(Java)，根據片段建立PDF文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出和組合器客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 使用組合器服務生成表單設計。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下必需值：

   * 表示要使用的DDX文檔的`com.adobe.idp.Document`對象。
   * 包含輸入XDP檔案的`java.util.Map`對象。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別。

   `invokeDDX`方法返回包含已裝配XDP文檔的`com.adobe.livecycle.assembler.client.AssemblerResult`對象。 要檢索已裝配的XDP文檔，請執行以下操作：

   * 調用`AssemblerResult`對象的`getDocuments`方法。 此方法會傳回`java.util.Map`物件。
   * 對`java.util.Map`對象進行迭代，直到找到結果`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取已裝配的XDP文檔。


1. 使用輸出服務生成PDF文檔。

   調用`OutputClient`對象的`generatePDFOutput2`方法並傳遞以下值：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`
   * 一個字串值，它指定其他資源（如影像）所在的內容根
   * 表示表單設計的`com.adobe.idp.Document`對象（使用匯編器服務返回的實例）
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象
   * 包含呈現運行時選項的`RenderOptionsSpec`對象
   * `com.adobe.idp.Document`對象，該對象包含要與表單設計合併的資料的XML資料源

   `generatePDFOutput2`方法返回包含操作結果的`OutputResult`對象

1. 將PDF文檔另存為PDF檔案。

   * 調用`OutputResult`對象的`getGeneratedDoc`方法，檢索表示PDF文檔的`com.adobe.idp.Document`對象。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案。 （請務必使用`getGeneratedDoc`方法傳回的`com.adobe.idp.Document`物件。）

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）:使用Java API根據片段建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[快速入門（SOAP模式）:使用Java API根據片段建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[正在設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用網站服務API根據片段建立PDF檔案 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

使用輸出服務API和組合器服務API（Web服務），根據片段建立PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 為與輸出服務關聯的服務引用使用以下WSDL定義：

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   為與組合器服務關聯的服務引用使用以下WSDL定義：

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   因為`BLOB`資料類型對兩個服務引用都是通用的，因此在使用`BLOB`資料類型時，請完全限定該資料類型。 在相應的Web服務快速入門中，所有`BLOB`實例都完全限定。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立輸出和組合器客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派至`OutputServiceClient.ClientCredentials.UserName.UserName`欄位。
      * 將相應的密碼值分配給`OutputServiceClient.ClientCredentials.UserName.Password`欄位。
      * 將常數值`HttpClientCredentialType.Basic`指派至`BasicHttpBindingSecurity.Transport.ClientCredentialType`欄位。
   * 將`BasicHttpSecurityMode.TransportCredentialOnly`常數值指派給`BasicHttpBindingSecurity.Security.Mode`欄位。

   >[!NOTE]
   >
   >對`AssemblerServiceClient`對象重複這些步驟。

1. 使用組合器服務生成表單設計。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象
   * 包含所需檔案的`MyMapOf_xsd_string_To_xsd_anyType`對象
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何異常。 要獲取新建立的XDP文檔，請執行以下操作：

   * 訪問`AssemblerResult`對象的`documents`欄位，該欄位是包含結果PDF文檔的`Map`對象。
   * 逐一查看`Map`對象以檢索裝配的表單設計。 將陣列成員的`value`轉換為`BLOB`。 將此`BLOB`實例傳遞至輸出服務。


1. 使用輸出服務生成PDF文檔。

   調用`OutputServiceClient`對象的`generatePDFOutput2`方法並傳遞以下值：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 一個字串值，它指定其他資源（如影像）所在的內容根。
   * 表示表單設計的`BLOB`對象（使用組合器服務返回的`BLOB`實例）。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `BLOB`對象，該對象包含要與表單設計合併的資料的XML資料源。
   * `generatePDFOutput2`方法填入的輸出`BLOB`物件。 `generatePDFOutput2`方法會以描述文檔的生成元資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * 包含操作結果的輸出`OutputResult`對象。 （此參數值僅對於Web服務調用是必需的）。

   `generatePDFOutput2`方法返回包含非互動式PDF表單的`BLOB`對象。

1. 將PDF文檔另存為PDF檔案。

   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示互動式PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存從`generatePDFOutput2`方法檢索到的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 打印到檔案 {#printing-to-files}

您可以使用輸出服務將資料流(如PostScript、打印機控制語言(PCL))或以下標籤格式打印到檔案中：

* 澤布拉 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用輸出服務，可以將XML資料與表單設計合併，並將表單打印到檔案中。 下圖顯示了Output服務建立雷射和標籤檔案。

>[!NOTE]
>
>有關向打印機發送打印流的資訊，請參閱[向打印機發送打印流](creating-document-output-streams.md#sending-print-streams-to-printers)。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

要打印到檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料源。
1. 設定打印到檔案所需的打印運行時選項。
1. 將打印流打印到檔案。
1. 檢索操作的結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。 (請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`對象。

**參考XML資料源**

要打印包含資料的文檔，必須為要填充資料的每個表單欄位引用包含XML元素的XML資料源。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

**設定打印到檔案所需的打印運行時選項**

要打印到檔案，必須通過指定輸出服務要打印到的檔案的位置和名稱來設定檔案URI運行時選項。 例如，要指示輸出服務將名為&#x200B;*MortgageForm.ps*&#x200B;的PostScript檔案打印到C:\Adobe ，請指定C:\Adobe\MortgageForm.ps。

>[!NOTE]
>
>您可以定義選用的執行時選項。 如需可設定的所有選項的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`PrintedOutputOptionsSpec`類參考。

**將打印流打印到檔案**

參考包含表單資料的有效XML資料源並設定打印運行時選項後，可以調用輸出服務，該服務將使其打印檔案。

**檢索操作的結果**

在輸出服務執行操作後，它返回指定操作是否成功的各種資料項，如XML資料。

**另請參閱**

[使用Java API列印至檔案](creating-document-output-streams.md#print-to-files-using-the-java-api)

[使用Web服務API打印到檔案](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API列印至檔案 {#print-to-files-using-the-java-api}

使用輸出API(Java)打印到檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。

1. 參考XML資料源。

   * 建立一個`java.io.FileInputStream`對象，該對象表示用於使用文檔的建構子填充文檔的XML資料源，並傳遞一個指定XML檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定打印到檔案所需的打印運行時選項。

   * 使用其建構子建立`PrintedOutputOptionsSpec`物件。
   * 通過調用PrintedOutputOptionsSpec對象的`setFileURI`方法並傳遞表示檔案名稱和位置的字串值來指定檔案。 例如，如果希望輸出服務打印到位於C:\Adobe的名為MortgageForm.ps的PostScript檔案，請指定C:\\Adobe\MortgageForm.ps。
   * 通過調用`PrintedOutputOptionsSpec`對象的`setCopies`方法並傳遞表示副本數的整數值，指定要打印的副本數。

1. 將打印流打印到檔案。

   調用`OutputClient`對象的`generatePrintedOutput`方法並傳遞以下值，以打印到檔案：

   * `PrintFormat`枚舉值，指定要建立的打印流格式。 例如，要建立PostScript打印流，請傳遞`PrintFormat.PostScript`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定相關宣傳資料檔案（如影像檔案）的位置。
   * 一個字串值，它指定要使用的XDC檔案的位置（如果指定了要使用的XDC檔案，則可以通過`PrintedOutputOptionsSpec`對象來傳遞`null`）。
   * `PrintedOutputOptionsSpec`物件，包含列印至檔案所需的執行階段選項。
   * 包含表單資料的XML資料源的`com.adobe.idp.Document`對象。

   `generatePrintedOutput`方法返回包含操作結果的`OutputResult`對象。

   >[!NOTE]
   >
   >`OutputResult`物件的`getRecordLevelMetaDataList`方法會傳回`null`。

1. 檢索操作的結果。

   * 通過調用`OutputResult`對象的`getStatusDoc`方法（`generatePrintedOutput`方法返回了`OutputResult`對象），建立表示`generatePrintedOutput`方法狀態的`com.adobe.idp.Document`對象。
   * 建立將包含操作結果的`java.io.File`對象。 請確定副檔名為XML。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案（確保使用`getStatusDoc`方法返回的`com.adobe.idp.Document`對象）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API列印至檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[正在設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服務API打印到檔案 {#print-to-files-using-the-web-service-api}

使用輸出API（web服務）打印到檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料源。

   * 使用其建構子建立`BLOB`物件。 `BLOB`物件用於儲存表單資料。
   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值指定包含表單資料的XML檔案的位置。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`binaryData`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 設定打印到檔案所需的打印運行時選項。

   * 使用其建構子建立`PrintedOutputOptionsSpec`物件。
   * 為`PrintedOutputOptionsSpec`對象的`fileURI`資料成員指定一個字串值，該字串值表示檔案的位置和名稱。 例如，如果希望輸出服務打印到位於C:\Adobe的名為&#x200B;*MortgageForm.ps*&#x200B;的PostScript檔案，請指定C:\\Adobe\MortgageForm.ps。
   * 通過為`PrintedOutputOptionsSpec`對象的`copies`資料成員指定表示副本數的整數值，指定要打印的副本數。

1. 將打印流打印到檔案。

   調用`OutputServiceService`對象的`generatePrintedOutput`方法並傳遞以下值，以打印到檔案：

   * `PrintFormat`枚舉值，指定要建立的打印流格式。 例如，要建立PostScript打印流，請傳遞`PrintFormat.PostScript`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定相關宣傳資料檔案（如影像檔案）的位置。
   * 一個字串值，它指定要使用的XDC檔案的位置（如果指定了要使用的XDC檔案，則可以通過`PrintedOutputOptionsSpec`對象來傳遞`null`）。
   * `PrintedOutputOptionsSpec`對象，包含打印到檔案所需的打印運行時選項。
   * `BLOB`物件，包含表單資料的XML資料來源。
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以描述文檔的生成元資料填充此對象。 （此參數值僅在Web服務調用時是必需的。）
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。 （此參數值僅在Web服務調用時是必需的。）
   * 包含操作結果的`OutputResult`對象。 （此參數值僅在Web服務調用時是必需的。）

1. 檢索操作的結果。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為XML。
   * 建立位元組陣列，用於儲存`OutputServiceService`對象的`generatePDFOutput`方法（第八個參數）填入結果資料的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 發送打印流到打印機 {#sending-print-streams-to-printers}

您可以使用輸出服務將打印流(如PostScript、打印機控制語言(PCL))或以下標籤格式發送到網路打印機：

* 澤布拉 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用「輸出」服務，您可以將XML資料與表單設計合併，並將表單輸出為打印流。 例如，您可以建立PostScript打印流並將其發送到網路打印機。 下圖顯示了將打印流發送到網路打印機的輸出服務。

>[!NOTE]
>
>為了演示如何向網路打印機發送打印流，本部分使用SharedPrinter打印機協定向網路打印機發送PostScript打印流。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

要向網路打印機發送打印流，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料源。
1. 設定打印運行時選項
1. 檢索要打印的文檔。
1. 將文檔發送到網路打印機。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，請建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceClient`對象。

**參考XML資料源**

要打印包含資料的文檔，必須為要填充資料的每個表單欄位引用包含XML元素的XML資料源。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

**設定打印運行時選項**

將打印流發送到打印機時，可以設定運行時選項，包括以下選項：

* **副本**:指定要發送到打印機的副本數。預設值為 1。
* **訂書**:使用訂書機時，會設定XCI選項。此選項可在配置模型中由訂書釘元素指定，並且僅用於PS和PCL打印機。
* **OutputJog**:當應合併輸出頁時（在輸出托盤中物理移動），會設定XCI選項。此選項僅適用於PS和PCL打印機。
* **OutputBin**:用於使打印驅動程式能夠選擇相應輸出盒的XCI值。

>[!NOTE]
>
>有關可設定的所有運行時選項的資訊，請參閱`PrintedOutputOptionsSpec`類引用。

**檢索要打印的文檔**

檢索要發送到打印機的打印流。 例如，您可以擷取PostScript檔案並將其傳送至印表機。

如果打印機支援PDF，則可以選擇發送PDF檔案。 但是，將PDF文檔發送到打印機時的一個問題是，每個打印機製造商都有不同的PDF解釋器實現。 也就是說，一些印刷廠使用Adobe PDF解釋，但它取決於打印機。 其他打印機有自己的PDF解釋器。 因此，打印結果可能不同。

將PDF文檔發送到打印機的另一個限制是它只打印；除了打印機上的設定外，它無法訪問雙工、紙盒選擇和裝訂。

要檢索要打印的文檔，請使用`generatePrintedOutput`方法。 下表指定使用`generatePrintedOutput`方法時為指定打印流設定的內容類型。

<table>
 <thead>
  <tr>
   <th><p>打印格式 </p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>預設情況下建立dpl203.xdc或自訂xdc輸出流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>建立DPL 300 DPI輸出流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>建立DPL 400 DPI輸出流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>建立DPL 600 DPI輸出流。</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>建立通用顏色PCL(5c)輸出流。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>建立一般PostScript第3級輸出流。</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>建立自定義IPL輸出流。</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>建立IPL 300 DPI輸出流。</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>建立IPL 400 DPI輸出流。</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>建立通用單色PCL(5e)輸出流。</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>建立一般PostScript第2級輸出流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>建立自定義TPCL輸出流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 DPI </p></td>
   <td><p>建立TPCL 305 DPI輸出流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 DPI </p></td>
   <td><p>建立TPCL 600 DPI輸出流。</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>建立ZPL 203 DPI輸出流。</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>建立ZPL 300 DPI輸出流。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您也可以使用`generatePrintedOutput2`方法將打印流發送到打印機。 但是，與「向打印機發送打印流」部分關聯的快速啟動使用`generatePrintedOutput`方法。

**將打印流發送到網路打印機**

檢索要打印的文檔後，可以調用輸出服務，該服務使其將打印流發送到網路打印機。 要使輸出服務成功找到打印機，必須同時指定打印伺服器和打印機名稱。 此外，還必須指定打印協定。

>[!NOTE]
>
>如果表單伺服器上安裝了PDFG，且伺服器在Windows Server 2008上運行，則無法使用SharedPrinter屬性。 在此情況下，請使用不同的打印機協定。

>[!NOTE]
>
>如果您使用網路打印機且訪問機制為SharedPrinter，則需要指定打印機的完整網路路徑。使用Java API將打印流發送到網路打印機

使用輸出API(Java)將打印流發送到網路打印機：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。

1. 參考XML資料源

   * 建立一個`java.io.FileInputStream`對象，該對象表示用於使用文檔的建構子填充文檔的XML資料源，並傳遞一個指定XML檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定打印運行時選項

   建立代表打印運行時選項的`PrintedOutputOptionsSpec`對象。 例如，可以通過調用`PrintedOutputOptionsSpec`對象的`setCopies`方法來指定要打印的副本數。

   >[!NOTE]
   >
   >如果要生成ZPL打印流，則不能使用`PrintedOutputOptionsSpec`對象的`setPagination`方法來設定分頁值。 同樣，不能為ZPL打印流設定以下選項：OutputJog、PageOffset和Stapler。 `setPagination`方法對於PostScript生成無效。 它僅對PCL生成有效。

1. 檢索要打印的文檔

   * 調用`OutputClient`對象的`generatePrintedOutput`方法並傳遞以下值，檢索要打印的文檔：

      * 指定打印流的`PrintFormat`枚舉值。 例如，要建立PostScript打印流，請傳遞`PrintFormat.PostScript`。
      * 指定表單設計名稱的字串值。
      * 一個字串值，它指定相關宣傳資料檔案（如影像檔案）的位置。
      * 指定要使用的XDC檔案位置的字串值。
      * `PrintedOutputOptionsSpec`物件，包含列印至檔案所需的執行階段選項。
      * `com.adobe.idp.Document`物件，代表包含要與表單設計合併的表單資料的XML資料來源。

      此方法會傳回包含操作結果的`OutputResult`物件。

   * 調用`OutputResult`對象s `getGeneratedDoc`方法，建立要發送到打印機的`com.adobe.idp.Document`對象。 此方法會傳回`com.adobe.idp.Document`物件。


1. 將打印流發送到網路打印機

   調用`OutputClient`對象的`sendToPrinter`方法並傳遞以下值，將打印流發送到網路打印機：

   * 表示要發送到打印機的打印流的`com.adobe.idp.Document`對象。
   * `PrinterProtocol`枚舉值，指定要使用的打印機協定。 例如，要指定SharedPrinter協定，請傳遞`PrinterProtocol.SharedPrinter`。
   * 指定打印伺服器名稱的字串值。 例如，假設打印伺服器的名稱為PrintSever1，請傳遞`\\\PrintSever1`。
   * 指定打印機名稱的字串值。 例如，假設打印機的名稱為Printer1，請傳遞`\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >已將`sendToPrinter`方法新增至8.2.1版的AEM Forms API。

### 使用Web服務API將打印流發送到打印機 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

使用輸出API（web服務）將打印流發送到網路打印機：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料源。

   * 使用其建構子建立`BLOB`物件。 `BLOB`物件用於儲存表單資料。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值指定包含表單資料的XML檔案的位置。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性來確定位元組陣列長度。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 設定打印運行時選項。

   使用其建構子建立`PrintedOutputOptionsSpec`物件。 例如，可以通過為`PrintedOutputOptionsSpec`對象的`copies`資料成員分配一個表示副本數的整數值來指定要打印的副本數。

   >[!NOTE]
   >
   >如果要生成ZPL打印流，則不能使用`PrintedOutputOptionsSpec`對象的`pagination`資料成員來設定分頁值。 同樣，不能為ZPL打印流設定以下選項：OutputJog、PageOffset和Stapler。 `pagination`資料成員對PostScript生成無效。 它僅對PCL生成有效。

1. 檢索要打印的文檔。

   * 調用`OutputServiceService`對象的`generatePrintedOutput`方法並傳遞以下值，檢索要打印的文檔：

      * 指定打印流的`PrintFormat`枚舉值。 例如，要建立PostScript打印流，請傳遞`PrintFormat.PostScript`。
      * 指定表單設計名稱的字串值。
      * 一個字串值，它指定相關宣傳資料檔案（如影像檔案）的位置。
      * 指定要使用的XDC檔案位置的字串值。
      * `PrintedOutputOptionsSpec`對象包含在向網路打印機發送打印流時使用的打印運行時選項。
      * `BLOB`物件，包含表單資料的XML資料來源。
      * 由`generatePrintedOutput`方法填入的`BLOB`對象。 `generatePrintedOutput`方法會以描述文檔的生成元資料填充此對象。 （此參數值僅在Web服務調用時是必需的。）
      * 由`generatePrintedOutput`方法填入的`BLOB`對象。 `generatePrintedOutput`方法會以結果資料填入此物件。 （此參數值僅在Web服務調用時是必需的。）
      * 包含操作結果的`OutputResult`對象。 （此參數值僅在Web服務調用時是必需的。）
   * 獲取`OutputResult`對象&#39;s `generatedDoc`方法的值，建立要發送到打印機的`BLOB`對象。 此方法會傳回`BLOB`物件，其中包含`generatePrintedOutput`方法傳回的PostScript資料。


1. 將打印流發送到網路打印機。

   調用`OutputClient`對象的`sendToPrinter`方法並傳遞以下值，將打印流發送到網路打印機：

   * 表示要發送到打印機的打印流的`BLOB`對象。
   * `PrinterProtocol`枚舉值，指定要使用的打印機協定。 例如，要指定SharedPrinter協定，請傳遞`PrinterProtocol.SharedPrinter`。
   * 一個`bool`值，它指定是否使用前一個參數值。 傳遞值`true`。 （此參數值僅在Web服務調用時是必需的。）
   * 指定打印伺服器名稱的字串值。 例如，假設打印伺服器的名稱為PrintSever1，請傳遞`\\\PrintSever1`。
   * 指定打印機名稱的字串值。 例如，假設打印機的名稱為Printer1，請傳遞`\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >已將`sendToPrinter`方法新增至8.2.1版的AEM Forms API。

## 建立多個輸出檔案 {#creating-multiple-output-files}

輸出服務可以為XML資料源內的每個記錄或包含所有記錄的單個檔案（預設功能為此功能）建立單獨的文檔。 例如，假設有10條記錄位於XML資料源中，並且您指示輸出服務使用輸出服務API為每個記錄建立單獨的PDF文檔（或其他類型的輸出）。 因此，輸出服務會產生10個PDF檔案。 （您可以將多個打印流發送到打印機，而不是建立文檔。）

下圖還顯示了Output服務處理包含多個記錄的XML資料檔案。 不過，假設您指示輸出服務建立包含所有資料記錄的單一PDF檔案。 在這種情況下，輸出服務將生成一個包含所有記錄的文檔。

下圖顯示了Output服務處理包含多個記錄的XML資料檔案。 假設您指示輸出服務為每個資料記錄建立個別的PDF檔案。 在此情況下，輸出服務會為每個資料記錄產生個別的PDF檔案。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

以下XML資料顯示包含三個資料記錄的資料檔案示例。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <batch>
 <LoanRecord>
     <mortgageAmount>500000</mortgageAmount>
     <lastName>Blue</lastName>
     <firstName>Tony</firstName>
     <SSN>555666777</SSN>
     <PositionTitle>Product Manager</PositionTitle>
     <Address>555 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>TBlue@NoMailServer.com</Email>
     <PhoneNum>555-7418</PhoneNum>
     <FaxNum>555-9981</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>300000</mortgageAmount>
     <lastName>White</lastName>
     <firstName>Sam</firstName>
     <SSN>555666222</SSN>
     <PositionTitle>Program Manager</PositionTitle>
     <Address>557 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SWhite@NoMailServer.com</Email>
     <PhoneNum>555-7445</PhoneNum>
     <FaxNum>555-9986</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>700000</mortgageAmount>
     <lastName>Green</lastName>
     <firstName>Steve</firstName>
     <SSN>55566688</SSN>
     <PositionTitle>Project Manager</PositionTitle>
     <Address>445 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SGreeb@NoMailServer.com</Email>
     <PhoneNum>555-2211</PhoneNum>
     <FaxNum>555-2221</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 </batch>
```

請注意，每個資料記錄開始和結束的XML元素為`LoanRecord`。 此XML元素由生成多個檔案的應用程式邏輯引用。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

要根據XML資料源建立多個PDF檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料源。
1. 設定PDF運行時選項。
1. 設定呈現運行時選項。
1. 產生多個PDF檔案。
1. 檢索操作的結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`對象。

**參考XML資料源**

引用包含多個記錄的XML資料源。 必須使用XML元素來分隔資料記錄。 例如，在本節前面顯示的示例XML資料源中，分隔資料記錄的XML元素名為`LoanRecord`。

要填入資料的每個表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

**設定PDF運行時選項**

必須為輸出服務設定以下運行時選項，才能根據XML資料源成功建立多個檔案：

* **許多檔案**:指定輸出服務是建立單個文檔還是建立多個文檔。您可以指定true或false。 要為XML資料源中的每個資料記錄建立單獨的文檔，請指定true。
* **檔案URI**:指定輸出服務生成的檔案的位置。例如，假設您指定C:\\Adobe\forms\Loan.pdf。 在此情況下，輸出服務會建立名為Loan.pdf的檔案，並將該檔案放在C:\\Adobe\forms folder目錄中。 當有多個檔案時，檔案名為Loan0001.pdf、Loan0002.pdf、Loan0003.pdf等。 如果指定檔案位置，則檔案會放在伺服器上，而不是客戶端電腦上。
* **記錄名稱**:在資料源中指定分隔資料記錄的XML元素名稱。例如，在本節前面顯示的示例XML資料源中，分隔資料記錄的XML元素稱為`LoanRecord`。 (您可以為記錄級別分配一個數值，指示包含資料記錄的元素級別，而不設定「記錄名稱」運行時間選項。 但是，您只能設定記錄名稱或記錄層。 您不能同時設定兩個值。)

**設定呈現運行時選項**

建立多個檔案時，可以設定呈現運行時選項。 雖然這些選項不是必需的（與輸出運行時選項不同，這些選項是必需的），但您可以執行諸如提高輸出服務的效能之類的任務。 例如，您可以快取輸出服務用來改善效能的表單設計。

當輸出服務處理批處理記錄時，它以增量方式讀取包含多個記錄的資料。 也就是說，輸出服務會將資料讀入記憶體，並在處理記錄批次時釋放資料。 設定兩個執行時選項之一時，輸出服務會以增量方式載入資料。 如果設定了「記錄名」運行時選項，則輸出服務將以增量方式讀取資料。 同樣，如果將「記錄級運行時間」選項設定為2或更大，則輸出服務將以增量方式讀取資料。

您可以使用`PDFOutputOptionsSpec`或`PrintedOutputOptionSpec`對象的`setLazyLoading`方法控制輸出服務是否執行增量載入。 您可以將值`false`傳遞至此方法，以關閉增量載入。

**產生多個PDF檔案**

參考包含多個資料記錄和設定運行時選項的有效XML資料源後，可以調用輸出服務，該服務將導致其生成多個檔案。 生成多個記錄時，`OutputResult`對象的`getGeneratedDoc`方法返回`null`。

**檢索操作的結果**

輸出服務執行操作後，它返回指定操作是否成功的XML資料。 輸出服務返回以下XML。 在這種情況下，輸出服務生成了42份檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <printResult>
 <status>0</status>
 <requestId>4ad85f9e2</requestId>
 <context/>
 <messages>
 <message>Printed all 42 records successfully.</message>
 </messages>
 <printSpec>
 <input>
 <validated>true</validated>
 <dataFile recordIdField="" recordLevel="0" recordName="LoanRecord"/>
 <sniffRules lookAhead="300"/>
 <formDesign>Loan.xdp</formDesign>
 <contentRoot>C:\Adobe</contentRoot>
 <metadata-spec record="false"/>
 </input>
 <output>
 <format>PDF</format>
 <fileURI>C:\Adobe\forms\Loan.pdf</fileURI>
 <optionString>cacheenabled=true&padebug=false&linearpdf=false&pdfarevisionnumber=1&pdfaconformance=A&taggedpdf=false&TransactionTimeOut=180</optionString>
 <waitForResponse>true</waitForResponse>
 <outputStream>multiple</outputStream>
 </output>
 </printSpec>
 </printResult>
```

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立多個PDF檔案 {#create-multiple-pdf-files-using-the-java-api}

使用輸出API(Java)建立多個PDF檔案：

1. 包含項目檔案」

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。.

1. 建立輸出客戶端對象

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。

1. 參考XML資料源

   * 建立`java.io.FileInputStream`對象，該對象表示包含多個記錄的XML資料源，方法是使用其建構子並傳遞一個字串值，該字串值指定XML檔案的位置。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定PDF運行時選項

   * 使用其建構子建立`PDFOutputOptionsSpec`物件。
   * 調用`PDFOutputOptionsSpec`對象的`setGenerateManyFiles`方法，設定「多檔案」選項。 例如，傳遞值`true`指示輸出服務為XML資料源中的每條記錄建立單獨的PDF檔案。 （如果您傳遞`false`，輸出服務會產生包含所有記錄的單一PDF檔案）。
   * 調用`PDFOutputOptionsSpec`對象的`setFileUri`方法並傳遞一個字串值，該字串值指定輸出服務生成的檔案的位置，從而設定檔案URI選項。 「檔案URI」選項相對於托管AEM Forms的J2EE應用程式伺服器，而不是客戶端電腦。
   * 調用`OutputOptionsSpec`對象的`setRecordName`方法並傳遞字串值，該字串值指定分隔資料記錄的資料源中的XML元素名稱，從而設定「記錄名稱」選項。 (例如，請考量本節前面顯示的XML資料來源。 分隔資料記錄的XML元素的名稱為LoanRecord)。

1. 設定呈現運行時選項

   * 使用其建構子建立`RenderOptionsSpec`物件。
   * 調用`RenderOptionsSpec`對象的`setCacheEnabled`並傳遞`true`的`Boolean`值，快取表單設計以改進輸出服務的效能。

1. 產生多個PDF檔案

   叫用`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以產生多個PDF檔案：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定表單設計所在的內容根。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `com.adobe.idp.Document`對象，該對象包含要與表單設計合併的資料的XML資料源。

   `generatePDFOutput`方法返回包含操作結果的`OutputResult`對象。

1. 檢索操作的結果

   * 建立`java.io.File`對象，該對象表示將包含`generatePDFOutput`方法結果的XML檔案。 請確定副檔名為.xml。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案（確保使用`applyUsageRights`方法返回的`com.adobe.idp.Document`對象）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）:使用Java API建立多個PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立多個PDF檔案 {#create-multiple-pdf-files-using-the-web-service-api}

使用輸出API（Web服務）建立多個PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料源。

   * 使用其建構子建立`BLOB`物件。 `BLOB`物件可用來儲存包含多個記錄的表單資料。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示包含多個記錄的XML檔案的檔案位置。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 設定PDF運行時選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`物件。
   * 通過為`OutputOptionsSpec`對象的`generateManyFiles`資料成員分配布爾值來設定「多檔案」選項。 例如，將值`true`分配給此資料成員，以指示輸出服務為XML資料源中的每條記錄建立單獨的PDF檔案。 （如果您將`false`分配給此資料成員，則輸出服務將生成包含所有記錄的單個PDF。）
   * 通過分配字串值來設定檔案URI選項，該字串值指定輸出服務生成的檔案到`OutputOptionsSpec`對象的`fileURI`資料成員的位置。 「檔案URI」選項相對於托管AEM Forms的J2EE應用程式伺服器，而不是客戶端電腦。
   * 通過指定字串值來設定記錄名稱選項，該字串值在將資料記錄分隔到`OutputOptionsSpec`對象的`recordName`資料成員的資料源中指定XML元素名稱。
   * 通過分配一個整數值來設定副本選項，該整數值指定輸出服務為`OutputOptionsSpec`對象的`copies`資料成員生成的副本數。

1. 設定呈現運行時選項。

   * 使用其建構子建立`RenderOptionsSpec`物件。
   * 將值`true`分配給`RenderOptionsSpec`對象的`cacheEnabled`資料成員，快取表單設計以改進輸出服務的效能。

1. 產生多個PDF檔案。

   叫用`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立多個PDF檔案：

   * TransformationFormat枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定表單設計所在的內容根。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `BLOB`對象，該對象包含要與表單設計合併的資料的XML資料源。
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以描述文檔的生成元資料填充此對象。
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。
   * 包含操作結果的`OutputResult`對象。

1. 檢索操作的結果

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為.xml。
   * 建立位元組陣列，用於儲存`OutputServiceService`對象的`generatePDFOutput`方法（第八個參數）填入結果資料的`BLOB`對象的資料內容。 獲取`BLOB`對象的`binaryData`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立搜尋規則 {#creating-search-rules}

您可以建立搜索規則，使輸出服務檢查輸入資料，並根據資料內容使用不同的表單設計來生成輸出。 例如，如果文本&#x200B;*mortgage*&#x200B;位於輸入資料中，則輸出服務可以使用名為Mortgage.xdp的表單設計。 同樣，如果文本&#x200B;*autobile*&#x200B;位於輸入資料中，則輸出服務可以使用另存為AutobileLoan.xdp的表單設計。 雖然輸出服務可產生不同的輸出類型，但本節假設輸出服務產生PDF檔案。 下圖顯示了通過處理XML資料檔案並使用許多表單設計之一生成PDF檔案的輸出服務。

此外，輸出服務能夠生成文檔包，其中在資料集中提供多個記錄，並且每個記錄與表單設計匹配，並且由多個表單設計生成單個文檔。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

要指示輸出服務在生成文檔時使用搜索規則，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料源。
1. 定義搜尋規則。
1. 設定PDF運行時選項。
1. 設定呈現運行時選項。
1. 生成PDF文檔。
1. 檢索操作的結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，則您需要將adobe-utilities.jar和jbossall-client.jar取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。

**參考XML資料源**

要填入資料的每個表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 只要指定了所有XML元素，就不需要匹配XML元素的顯示順序。

**定義搜尋規則**

要定義搜索規則，可定義輸出服務在輸入資料中搜索的一個或多個文本模式。 對於您定義的每個文本模式，可以指定在找到文本模式時使用的相應表單設計。 如果找到文字模式，則輸出服務會使用對應的表單設計來產生輸出。 文本模式的示例為&#x200B;*mortgage*。

>[!NOTE]
>
>如果找不到文本模式，則使用預設表單。 請確定您使用的所有表單設計都位於內容根目錄中。

**設定PDF運行時選項**

設定以下PDF運行時選項，以便輸出服務成功建立基於多個表單設計的PDF文檔：

* **檔案URI**:指定輸出服務生成的PDF檔案的名稱和位置。
* **規則**:指定您定義的規則。
* **LookAHead**:指定從輸入資料檔案的開頭開始要掃描定義文本模式的位元組數。預設為500個位元組。

**設定呈現運行時選項**

您可以在建立PDF檔案時設定呈現運行時選項。 雖然這些選項不是必要選項（與PDF運行時選項不同），但您可以執行諸如提高輸出服務的效能之類的任務。 例如，您可以快取輸出服務用來改善效能的表單設計。

**生成PDF文檔**

參考有效的XML資料源並設定運行時選項後，可以調用輸出服務，從而生成PDF文檔。 如果輸出服務在輸入資料中找到指定的文本模式，則使用相應的表單設計。 如果未使用文字模式，則輸出服務會使用預設的表單設計。

**檢索操作的結果**

輸出服務執行操作後，它返回指定操作是否成功的XML資料。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立搜尋規則 {#create-search-rules-using-the-java-api}

使用輸出API(Java)建立搜尋規則：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。

1. 參考XML資料源。

   * 建立`java.io.FileInputStream`對象，該對象表示用於通過使用其建構子並傳遞指定XML檔案位置的字串值來填充PDF文檔的XML資料源。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 定義搜尋規則。

   * 使用其建構子建立`Rule`物件。
   * 通過調用`Rule`對象的`setPattern`方法並傳遞指定文本模式的字串值來定義文本模式。
   * 叫用`Rule`物件的`setForm`方法，定義對應的表單設計。 傳遞指定表單設計名稱的字串值。

   >[!NOTE]
   >
   >對於要定義的每個文本模式，重複前三個子步驟。

   * 使用`java.util.ArrayList`建構子建立`java.util.List`物件。
   * 對於您建立的每個`Rule`對象，調用`java.util.List`對象的`add`方法，並傳遞`Rule`對象。


1. 設定PDF運行時選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`物件。
   * 指定輸出服務通過調用`PDFOutputOptionsSpec`對象的`setFileURI`方法生成的PDF檔案的名稱和位置。 傳遞指定PDF檔案位置的字串值。 「檔案URI」選項相對於托管AEM Forms的J2EE應用程式伺服器，而不是客戶端電腦。
   * 通過調用`PDFOutputOptionsSpec`對象的`setRules`方法來設定您定義的規則。 傳遞包含`Rule`對象的`java.util.List`對象。
   * 調用`PDFOutputOptionsSpec`對象的`setLookAhead`方法，設定要掃描定義文本模式的位元組數。 傳遞一個整數值，該值表示位元組數。

1. 設定呈現運行時選項。

   * 使用其建構子建立`RenderOptionsSpec`物件。
   * 快取表單設計，以通過調用`RenderOptionsSpec`對象的`setCacheEnabled`並傳遞`true`來改進輸出服務的效能。

1. 生成PDF文檔。

   通過調用`OutputClient`對象的`generatePDFOutput`方法並傳遞以下值，生成基於多個表單設計的PDF文檔：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 指定預設表單設計名稱的字串值。 也就是說，在未找到文本模式時使用的表單設計。
   * 一個字串值，它指定表單設計所在的內容根。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `com.adobe.idp.Document`物件，包含輸出服務針對已定義的文字模式所搜尋的表單資料。

   `generatePDFOutput`方法返回包含操作結果的`OutputResult`對象。

1. 檢索操作的結果。

   * 通過調用`OutputResult`對象的`getStatusDoc`方法，建立表示`generatePDFOutput`方法狀態的`com.adobe.idp.Document`對象。
   * 建立將包含操作結果的`java.io.File`對象。 請確定副檔名為.xml。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案（確保使用`getStatusDoc`方法返回的`com.adobe.idp.Document`對象）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）:使用Java API建立搜尋規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[快速入門（SOAP模式）:使用Java API建立搜尋規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API建立搜尋規則 {#create-search-rules-using-the-web-service-api}

使用輸出API（網站服務）建立搜尋規則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料源。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存將與PDF文檔合併的資料。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 定義搜尋規則。

   * 使用其建構子建立`Rule`物件。
   * 通過為`Rule`對象的`pattern`資料成員指定指定文本模式的字串值來定義文本模式。
   * 通過為`Rule`對象的`form`資料成員指定表單設計的字串值，定義相應的表單設計。

   >[!NOTE]
   >
   >對於要定義的每個文本模式，重複前三個子步驟。

   * 建立儲存規則的`MyArrayOf_xsd_anyType`物件。
   * 將每個`Rule`物件指派給`MyArrayOf_xsd_anyType`陣列的元素。 為每個`Rule`對象調用`MyArrayOf_xsd_anyType`對象的`Add`方法。


1. 設定PDF運行時選項

   * 使用其建構子建立`PDFOutputOptionsSpec`物件。
   * 通過分配字串值來設定檔案URI選項，該字串值指定輸出服務為`PDFOutputOptionsSpec`對象的`fileURI`資料成員生成的PDF檔案的位置。 「檔案URI」選項相對於托管AEM Forms的J2EE應用程式伺服器，而不是客戶端電腦。
   * 通過分配一個整數值來設定副本選項，該整數值指定輸出服務為`PDFOutputOptionsSpec`對象的`copies`資料成員生成的副本數。
   * 通過為`PDFOutputOptionsSpec`對象的`rules`資料成員分配將規則儲存的`MyArrayOf_xsd_anyType`對象來設定您定義的規則。
   * 通過指定一個整數值來設定要掃描定義文本模式的位元組數，該整數值表示要掃描到`PDFOutputOptionsSpec`對象的`lookAhead`資料方法的位元組數。

1. 設定呈現運行時選項

   * 使用其建構子建立`RenderOptionsSpec`物件。
   * 快取表單設計，以通過將值`true`分配給`RenderOptionsSpec`對象的`cacheEnabled`資料成員來改進輸出服務的效能。

   >[!NOTE]
   >
   >如果輸入文檔是Acrobat表單，則不能使用`RenderOptionsSpec`對象的`pdfVersion`成員來設定PDF文檔的版本。 輸出PDF檔案會保留Acrobat表單的PDF版本。 同樣，如果輸入文檔為Acrobat表單，則不能使用`RenderOptionsSpec`對象的`taggedPDF`方法來設定帶標籤的PDF選項。

   >[!NOTE]
   >
   >如果輸入PDF文檔經過認證或數字簽名，則不能使用`RenderOptionsSpec`對象的`linearizedPDF`成員來設定線性化的PDF選項。 如需詳細資訊，請參閱[數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。

1. 生成PDF文檔

   叫用`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`枚舉值。 要生成PDF文檔，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定表單設計所在的內容根。
   * 包含PDF運行時選項的`PDFOutputOptionsSpec`對象。
   * 包含呈現運行時選項的`RenderOptionsSpec`對象。
   * `BLOB`對象，該對象包含要與表單設計合併的資料的XML資料源。
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以描述文檔的生成元資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * 由`generatePDFOutput`方法填入的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。 （此參數值僅對於Web服務調用是必需的）。
   * 包含操作結果的`OutputResult`對象。 （此參數值僅對於Web服務調用是必需的）。

   >[!NOTE]
   >
   >叫用`generatePDFOutput`方法產生PDF檔案時，請注意，您無法將資料與已簽署、認證或包含使用權限的XFA PDF表單合併。 有關使用權限的資訊，請參閱[將使用權限應用於PDF文檔](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。

1. 檢索操作的結果

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為XML。
   * 建立位元組陣列，用於儲存`OutputServiceService`對象的`generatePDFOutput`方法（第八個參數）填入結果資料的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 拼合PDF文檔 {#flattening-pdf-documents}

您可以使用輸出服務將互動式PDF檔案轉換為非互動式PDF。 互動式PDF檔案可讓使用者輸入或修改PDF檔案欄位中的資料。 將互動式PDF檔案轉換為非互動式PDF檔案的程式稱為&#x200B;*拼合*。 平面化PDF文檔時，用戶無法修改文檔欄位中的資料。 平面化PDF檔案的一個原因是為了確保資料無法修改。

您可以平面化下列類型的PDF檔案：

* 互動式XFA PDF檔案
* AcrobatForms

嘗試平面化非互動式PDF檔案的PDF會造成例外狀況。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-9}

要將互動式PDF文檔平面化為非互動式PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 擷取互動式PDF檔案。
1. 轉換PDF檔案。
1. 將非互動式PDF檔案儲存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您是使用網站服務，請確定您包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。 有關所有AEM Forms JAR檔案的位置資訊，請參閱[包含AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`對象。

**擷取互動式PDF檔案**

檢索要轉換為非互動式PDF文檔的互動式PDF文檔。 嘗試轉換非互動式PDF檔案會造成例外狀況。

**轉換PDF檔案**

擷取互動式PDF檔案後，您可將其轉換為非互動式PDF檔案。 輸出服務返回非互動式PDF文檔。

**將非互動式PDF檔案儲存為PDF檔案**

您可以將非互動式PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API平面化PDF檔案](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[使用Web服務API平面化PDF檔案](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API平面化PDF檔案 {#flatten-a-pdf-document-using-the-java-api}

使用Output API(Java)將互動式PDF檔案平面化為非互動式PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`OutputClient`物件。

1. 擷取互動式PDF檔案。

   * 建立`java.io.FileInputStream`對象，該對象表示要轉換的互動式PDF文檔，方法是使用其建構子並傳遞一個字串值，該字串值指定互動式PDF檔案的位置。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 轉換PDF檔案。

   調用`OutputServiceService`對象的`transformPDF`方法並傳遞以下值，將互動式PDF文檔轉換為非互動式PDF文檔：

   * 包含互動式PDF文檔的`com.adobe.idp.Document`對象。
   * `TransformationFormat`枚舉值。 要生成非互動式PDF文檔，請指定`TransformationFormat.PDF`。
   * 指定修訂編號的`PDFARevisionNumber`枚舉值。 因為此參數是用於PDF/A文檔，所以可以指定`null`。
   * 代表修訂編號和年份的字串值，以冒號分隔。 因為此參數是用於PDF/A文檔，所以可以指定`null`。
   * 代表PDF/A一致性級別的`PDFAConformance`枚舉值。 因為此參數是用於PDF/A文檔，所以可以指定`null`。

   `transformPDF`方法返回包含非互動式PDF文檔的`com.adobe.idp.Document`對象。

1. 將非互動式PDF檔案儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 調用`Document`對象的`copyToFile`方法，將`Document`對象的內容複製到檔案（確保使用`transformPDF`方法返回的`Document`對象）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）:使用Java API轉換PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API轉換PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API平面化PDF檔案 {#flatten-a-pdf-document-using-the-web-service-api}

使用輸出API（網站服務）將互動式PDF檔案平面化為非互動式PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取互動式PDF檔案。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存互動式PDF文檔。
   * 叫用`System.IO.FileStream`物件的建構函式並傳遞代表互動式PDF檔案的檔案位置的字串值，以建立物件。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 轉換PDF檔案。

   調用`OutputClient`對象的`transformPDF`方法並傳遞以下值，將互動式PDF文檔轉換為非互動式PDF文檔：

   * 包含互動式PDF檔案的`BLOB`物件。
   * `TransformationFormat`枚舉值。 要生成非互動式PDF文檔，請指定`TransformationFormat.PDF`。
   * 指定修訂編號的`PDFARevisionNumber`枚舉值。
   * 一個布爾值，它指定是否使用`PDFARevisionNumber`枚舉值。 因為此參數是用於PDF/A文檔，所以可以指定`false`。
   * 代表修訂編號和年份的字串值，以冒號分隔。 因為此參數是用於PDF/A文檔，所以可以指定`null`。
   * 代表PDF/A一致性級別的`PDFAConformance`枚舉值。
   * 指定是否使用`PDFAConformance`枚舉值的布爾值。 因為此參數是用於PDF/A文檔，所以可以指定`false`。

   `transformPDF`方法返回包含非互動式PDF文檔的`BLOB`對象。

1. 將非互動式PDF檔案儲存為PDF檔案。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示非互動式PDF文檔的檔案位置。
   * 建立位元組陣列，用於儲存`transformPDF`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
