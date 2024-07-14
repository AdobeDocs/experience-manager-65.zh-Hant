---
title: 建立檔案輸出資料流
description: 使用「輸出」服務將檔案轉換成PDF(包括PDF/A檔案)、PostScript、印表機控制語言(PCL)和Zebra - ZPL、Intermec - IPL、Datamax - DPL和TecToshiba - TPCL標籤格式。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '18860'
ht-degree: 0%

---

# 建立檔案輸出資料流  {#creating-document-output-streams}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於輸出服務**

「輸出」服務可讓您將檔案輸出為PDF(包括PDF/A檔案)、PostScript、印表機控制語言(PCL)和下列標籤格式：

* 斑馬 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用「輸出」服務，您可以將XML表單資料與表單設計合併，並將檔案輸出至網路印表機或檔案。

有兩種方式可以將表單設計（XDP檔案）傳遞到Output服務。 您可以將包含表單設計的`com.adobe.idp.Document`執行個體傳遞至Output服務。 或者，您可以傳遞一個指定表單設計位置的URI值。 這兩種方式都在&#x200B;*使用AEM表單*&#x200B;進行程式設計時進行了討論。

>[!NOTE]
>
>Output服務不支援包含應用程式物件特定指令碼的AcroformPDF檔案。 包含應用程式物件特定指令碼的AcroformPDF檔案不會轉譯。

以下小節說明如何使用URI值將表單設計傳遞給Output服務：

* [建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A檔案](creating-document-output-streams.md#creating-pdf-a-documents)

以下小節說明如何在`com.adobe.idp.Document`執行個體中傳遞表單設計：

* [將Content Services中的檔案傳遞（已棄用）至Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

決定使用哪種技術時的一個考量是，如果您從其他AEM Forms服務取得表單設計，然後將其傳遞到`com.adobe.idp.Document`執行個體。 *傳遞檔案至輸出服務*&#x200B;和&#x200B;*使用片段建立PDF檔案*&#x200B;區段都會顯示如何從另一個AEM Forms服務取得表單設計。 第一節　從內容服務擷取表單設計（已棄用）。 第二節　從組合器服務擷取表單設計。

如果您要從固定位置（例如檔案系統）取得表單設計，則可以使用任一技術。 也就是說，您可以指定XDP檔案的URI值或使用`com.adobe.idp.Document`執行個體。

若要在建立PDF檔案時，傳遞指定表單設計位置的URI值，請使用`generatePDFOutput`方法。 同樣地，若要在建立PDF檔案時將`com.adobe.idp.Document`執行個體傳遞至輸出服務，請使用`generatePDFOutput2`方法。

將輸出資料流傳送至網路印表機時，您也可以使用其中一種技術。 若要透過傳遞包含表單設計的`com.adobe.idp.Document`執行個體來傳送輸出資料流至印表機，請使用`sendToPrinter2`方法。 若要傳遞URI值來傳送輸出資料流至印表機，請使用`sendToPrinter`方法。 *傳送列印資料流至印表機*&#x200B;區段使用`sendToPrinter`方法。

您可以使用「輸出」服務完成這些工作：

* [建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A檔案](creating-document-output-streams.md#creating-pdf-a-documents)
* [將Content Services中的檔案傳遞（已棄用）至Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [列印至檔案](creating-document-output-streams.md#printing-to-files)
* [傳送列印資料流至印表機](creating-document-output-streams.md#sending-print-streams-to-printers)
* [建立多個輸出檔案](creating-document-output-streams.md#creating-multiple-output-files)
* [建立搜尋規則](creating-document-output-streams.md#creating-search-rules)
* [平面化PDF檔案](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>如需有關Output服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立PDF檔案 {#creating-pdf-documents}

您可以使用Output服務來建立以您提供的表單設計和XML表單資料為基礎的PDF檔案。 Output服務建立的PDF檔案不是互動式PDF檔案；使用者無法輸入或修改表單資料。

如果要建立用於長期儲存的PDF檔案，建議您建立PDF/A檔案。 (請參閱[建立PDF/A檔案](creating-document-output-streams.md#creating-pdf-a-documents)。)

若要建立可讓使用者輸入資料的互動式PDF表單，請使用Forms服務。 (請參閱[呈現互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)。)

>[!NOTE]
>
>如需有關Output服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要建立PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參考XML資料來源。
1. 設定PDF執行階段選項。
1. 設定演算執行階段選項。
1. 產生PDF檔案。
1. 擷取作業的結果。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在受支援的J2EE應用程式伺服器（不是JBoss）上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在之J2EE應用程式伺服器的JAR檔案。

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`物件。

**參考XML資料來源**

若要將資料與表單設計合併，您必須參照包含資料的XML資料來源。 您計畫填入資料的每個表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

請考量下列貸款申請表範例。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

若要將資料合併至此表單設計，您必須建立與表單相對應的XML資料來源。 下列XML代表與範例抵押應用程式表單相對應的XDP XML資料來源。

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

**設定PDF執行階段選項**

建立PDF檔案時，請設定檔案URI選項。 此選項指定輸出服務產生的PDF檔案的名稱和位置。

>[!NOTE]
>
>您不必設定檔案URI執行階段選項，而是可以程式設計方式從輸出服務傳回的複雜資料型別中擷取PDF檔案。 但是，透過設定檔案URI執行時間選項，您不需要建立以程式擷取PDF檔案的應用程式邏輯。

**設定演算執行階段選項**

建立PDF檔案時，您可以設定演算執行階段選項。 雖然這些選項並非必要專案(不同於必要專案的PDF執行階段選項)，但您可以執行工作，例如改善Output服務的效能。 例如，您可以快取Output服務用來改善其效能的表單設計。

如果您使用已標籤的Acrobat表單作為輸入，則無法使用輸出服務Java或Web服務API來關閉已標籤的設定。 如果您嘗試以程式設計方式將此選項設定為`false`，則仍會標籤結果PDF檔案。

>[!NOTE]
>
>如果您未指定呈現執行階段選項，則會使用預設值。 如需有關演算執行階段選項的資訊，請參閱`RenderOptionsSpec`類別參考。 (請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**產生PDF檔案**

在參照包含表單資料的有效XML資料來源並設定執行階段選項後，您可以叫用Output服務，使其產生PDF檔案。

產生PDF檔案時，您可以指定Output服務建立PDF檔案所需的URI值。 表單設計可儲存在伺服器檔案系統等位置或作為AEM Forms應用程式的一部分。 使用內容根URI值`repository:///`，可參考存在於Forms應用程式一部分的表單設計（或其他資源，例如影像檔案）。 例如，假設下列名為&#x200B;*Loan.xdp*&#x200B;的表單設計位於名為&#x200B;*Applications/FormsApplication*&#x200B;的Forms應用程式中：

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

若要存取上圖所示的Loan.xdp檔案，請將`repository:///Applications/FormsApplication/1.0/FormsFolder/`指定為傳遞至`OutputClient`物件之`generatePDFOutput`方法的第三個引數。 將表單名稱(*Loan.xdp*)指定為傳遞至`OutputClient`物件之`generatePDFOutput`方法的第二個引數。

如果XDP檔案包含影像（或其他資源，例如片段），請將資源放在與XDP檔案相同的應用程式資料夾中。 AEM Forms使用內容根URI作為基礎路徑來解析對影像的參照。 例如，如果Loan.xdp檔案包含影像，請確定您將該影像放在`Applications/FormsApplication/1.0/FormsFolder/`中。

>[!NOTE]
>
>叫用`OutputClient`物件的`generatePDFOutput`或`generatePrintedOutput`方法時，您可以參考Forms應用程式URI。

>[!NOTE]
>
>若要檢視透過參考Forms應用程式中的XDP來建立PDF檔案的完整快速入門，請參閱[快速入門（EJB模式）：使用Java API根據應用程式XDP檔案建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)。

**擷取作業的結果**

Output服務執行作業之後，會傳回各種資料專案，例如指定作業是否成功的狀態XML資料。

**另請參閱**

[使用Java API建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[使用Web服務API建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立PDF檔案 {#create-a-pdf-document-using-the-java-api}

使用Output API (Java)建立PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。

1. 參考XML資料來源。

   * 建立`java.io.FileInputStream`物件，代表用來填入PDF檔案的XML資料來源，使用它的建構函式，並傳遞指定XML檔案位置的字串值。
   * 使用物件的建構函式建立`com.adobe.idp.Document`物件。 傳遞`java.io.FileInputStream`物件。

1. 設定PDF執行階段選項。

   * 使用物件的建構函式建立`PDFOutputOptionsSpec`物件。
   * 呼叫`PDFOutputOptionsSpec`物件的`setFileURI`方法來設定檔案URI選項。 傳遞字串值，指定輸出服務產生的PDF檔案位置。 檔案URI選項是相對於主控AEM Forms的J2EE應用程式伺服器，而非使用者端電腦。

1. 設定演算執行階段選項。

   * 使用物件的建構函式建立`RenderOptionsSpec`物件。
   * 快取表單設計以透過叫用`RenderOptionsSpec`物件的`setCacheEnabled`並傳遞`true`來改善輸出服務的效能。

   >[!NOTE]
   >
   >如果輸入檔案是Acrobat表單(在Acrobat中建立的表單)或已簽署或認證的XFA檔案，則您無法使用`RenderOptionsSpec`物件的`setPdfVersion`方法設定PDF檔案的版本。 輸出PDF檔案會保留原始PDF版本。 同樣地，如果輸入檔案是Adobe PDF表單或已簽署或認證的XFA檔案，則您無法透過叫用`RenderOptionsSpec`物件的`setTaggedPDF`方法來設定已標籤的Acrobat選項。

   >[!NOTE]
   >
   >如果輸入PDF檔案是經過認證或數位簽署的，則您無法使用`RenderOptionsSpec`物件的`setLinearizedPDF`方法來設定線性PDF選項。 (請參閱[數位簽署PDF檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。)*

1. 產生PDF檔案。

   呼叫`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`com.adobe.idp.Document`物件。

   `generatePDFOutput`方法傳回包含作業結果的`OutputResult`物件。

   >[!NOTE]
   >
   >當透過叫用`generatePDFOutput`方法產生PDF檔案時，您無法將資料與已簽署或認證的XFAPDF表單合併。 （請參閱[數位簽署和認證檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。）*

   >[!NOTE]
   >
   >`OutputResult`物件的`getRecordLevelMetaDataList`方法傳回&#x200B;`null`*.*

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput2`方法來建立PDF檔案。 (請參閱[將Content Services （已過時）中的檔案傳遞至輸出服務&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 擷取作業的結果。

   * 透過叫用`OutputResult`物件的`getStatusDoc`方法，擷取代表`generatePDFOutput`作業狀態的`com.adobe.idp.Document`物件。 此方法會傳回指定作業是否成功的狀態XML資料。
   * 建立包含作業結果的`java.io.File`物件。 確認副檔名為.xml。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案（請確定您使用的是`getStatusDoc`方法傳回的`com.adobe.idp.Document`物件）。

   雖然Output服務會將PDF檔案寫入傳遞至`PDFOutputOptionsSpec`物件之`setFileURI`方法的引數所指定的位置，但您可以透過叫用`OutputResult`物件的`getGeneratedDoc`方法，以程式設計方式擷取PDF/A檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[快速入門(SOAP模式)：使用Java API建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立PDF檔案 {#create-a-pdf-document-using-the-web-service-api}

使用輸出API （Web服務）建立PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 使用預設建構函式建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`OutputServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存將與PDF檔案合併的XML資料。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表包含表單資料之XML檔案的檔案位置的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 設定PDF執行階段選項

   * 使用物件的建構函式建立`PDFOutputOptionsSpec`物件。
   * 透過指派字串值來設定File URI選項，該字串值指定輸出服務產生給`PDFOutputOptionsSpec`物件的`fileURI`資料成員的PDF檔案位置。 檔案URI選項是相對於主控AEM Forms的J2EE應用程式伺服器，而非使用者端電腦。

1. 設定演算執行階段選項。

   * 使用物件的建構函式建立`RenderOptionsSpec`物件。
   * 快取表單設計以透過將值`true`指派給`RenderOptionsSpec`物件的`cacheEnabled`資料成員來改善Output服務的效能。

   >[!NOTE]
   >
   >如果輸入檔案是Acrobat表單(在Acrobat中建立的表單)或已簽署或認證的XFA檔案，則您無法使用`RenderOptionsSpec`物件的`setPdfVersion`方法設定PDF檔案的版本。 輸出PDF檔案會保留原始PDF版本。 同樣地，如果輸入檔案是Adobe PDF表單或已簽署或認證的XFA檔案，您就無法透過叫用`RenderOptionsSpec`物件的`setTaggedPDF`*方法來設定已標籤的Acrobat選項。*

   >[!NOTE]
   >
   >如果輸入PDF檔案是經認證或數位簽署的，則您無法使用`RenderOptionsSpec`物件的`linearizedPDF`成員來設定線性PDF選項。 (請參閱[數位簽署PDF檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。)*

1. 產生PDF檔案。

   呼叫`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`BLOB`物件。
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將描述檔案的產生中繼資料填入此物件。 （只有Web服務呼叫才需要此引數值）。
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將結果資料填入此物件中。 （只有Web服務呼叫才需要此引數值）。
   * 包含作業結果的`OutputResult`物件。 （只有Web服務呼叫才需要此引數值）。

   >[!NOTE]
   >
   >當透過叫用`generatePDFOutput`方法產生PDF檔案時，您無法將資料與已簽署或認證的XFAPDF表單合併。 （請參閱[數位簽署和認證檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。）*

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput2`方法來建立PDF檔案。 (請參閱[將Content Services （已過時）中的檔案傳遞至輸出服務&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 擷取作業的結果。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確認副檔名為.xml。
   * 建立位元組陣列，以儲存`BLOB`物件的資料內容，該物件是以`OutputServiceService`物件的`generatePDFOutput`方法（第八個引數）填入的結果資料。 取得`BLOB`物件的`MTOM` `field`的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

   另請參閱

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >已棄用`OutputServiceService`物件的`generateOutput`方法。

## 建立PDF/A檔案 {#creating-pdf-a-documents}

您可以使用Output服務來建立PDF/A檔案。 由於PDF/A是用於長期儲存檔案內容的封存格式，因此所有字型全都內嵌且檔案都未壓縮。 因此，PDF/A 文件通常比標準 PDF 文件大。此外，PDF/檔案不包含音訊和視訊內容。 如同其他輸出服務工作，您提供表單設計和資料以與表單設計合併，以建立PDF/A檔案。

PDF/A-1規格包含兩個一致性層次，即a和b。兩者之間的主要差異在於邏輯結構（協助工具）支援，這並非一致性層級b所需。無論一致性層級為何，PDF/A-1會指定所有字型都內嵌在產生的PDF/A檔案中。

雖然PDF/A是封存PDF檔案的標準，但如果標準PDF檔案符合貴公司的需求，則不強制使用PDF/A進行封存。 PDF/A標準的目的是建立可長期儲存的PDF檔案，並符合檔案儲存要求。 例如，URL無法內嵌於PDF/A中，因為該URL可能會隨著時間變得無效。

您的組織必須評估自己的需求、您打算保留檔案的時間長度、檔案大小考量，並決定自己的封存策略。 您可以使用DocConverter服務，以程式設計方式判斷PDF檔案是否符合PDF/A規範。 (請參閱[以程式設計方式決定PDF/相容性](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)。)

PDF/檔案必須使用在表單設計中指定的字型，且字型不能被取代。 因此，如果位於PDF檔案中的字型在主機作業系統(OS)上無法使用，則會發生例外狀況。

在Acrobat中開啟PDF/A檔案時，會顯示訊息，確認檔案為PDF/A檔案，如下圖所示。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM網站有PDF/常見問題集區段，您可以在[https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml)存取。

>[!NOTE]
>
>如需有關Output服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_65)。

### 步驟摘要 {#summary_of_steps-1}

若要建立PDF/檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參考XML資料來源。
1. 設定PDF/執行階段選項。
1. 設定演算執行階段選項。
1. 產生PDF/檔案。
1. 擷取作業的結果。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立自訂應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在受支援的J2EE應用程式伺服器（不是JBoss）上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在之J2EE應用程式伺服器的JAR檔案。

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`物件。

**參考XML資料來源**

若要將資料與表單設計合併，您必須參照包含資料的XML資料來源。 每個要填入資料的表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

**設定PDF/A執行階段選項**

建立PDF/A檔案時，您可以設定「檔案URI」選項。 URI是相對於主控AEM Forms的J2EE應用程式伺服器。 也就是說，如果您設定C:\Adobe，檔案會寫入伺服器上的資料夾，而非使用者端電腦。 URI會指定輸出服務產生的PDF/A檔案的名稱和位置。

**設定演算執行階段選項**

建立PDF/A檔案時，您可以設定演算執行階段選項。 您可以設定的兩個PDF/A相關選項是`PDFAConformance`和`PDFARevisionNumber`值。 `PDFAConformance`值是指PDF檔案如何遵守指定長期保留電子檔案的要求。 此選項的有效值為`A`和`B`。 如需有關等級a和b相容性的資訊，請參閱標題為&#x200B;*ISO 19005-1檔案管理*&#x200B;的PDF/A-1 ISO規格。

`PDFARevisionNumber`值是指PDF/A檔案的修訂版本號碼。 如需PDF/A檔案修訂版本的資訊，請參閱標題為&#x200B;*ISO 19005-1檔案管理*&#x200B;的PDF/A-1 ISO規格。

>[!NOTE]
>
>建立PDF/A 1A檔案時，您無法將已標籤的Adobe PDF選項設為`false`。 PDF/A 1A將永遠是標籤的PDF檔案。 此外，建立PDF/A 1B檔案時，您無法將已標籤的Adobe PDF選項設為`true`。 PDF/A 1B將永遠是未標籤的PDF檔案。

**產生PDF/檔案**

在您參照包含表單資料的有效XML資料來源並設定執行階段選項後，可以叫用Output服務，使其產生PDF/A檔案。

**擷取作業的結果**

Output服務執行作業之後，會傳回各種資料專案，例如指定作業是否成功的XML資料。

**另請參閱**

[使用Java API建立PDF/檔案](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[使用網站服務API建立PDF/檔案](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立PDF/檔案 {#create-a-pdf-a-document-using-the-java-api}

使用Output API (Java)建立PDF/檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。

1. 參考XML資料來源。

   * 使用建構函式並傳遞指定XML檔案位置的字串值，建立代表用來填入PDF/A檔案的XML資料來源的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定PDF/執行階段選項。

   * 使用物件的建構函式建立`PDFOutputOptionsSpec`物件。
   * 呼叫`PDFOutputOptionsSpec`物件的`setFileURI`方法來設定檔案URI選項。 傳遞字串值，指定輸出服務產生的PDF檔案位置。 檔案URI選項是相對於主控AEM Forms的J2EE應用程式伺服器，而非使用者端電腦。

1. 設定演算執行階段選項。

   * 使用物件的建構函式建立`RenderOptionsSpec`物件。
   * 透過叫用`RenderOptionsSpec`物件的`setPDFAConformance`方法並傳遞指定一致性層級的`PDFAConformance`列舉值來設定`PDFAConformance`值。 例如，若要指定一致性層級A，請傳遞`PDFAConformance.A`。
   * 呼叫`RenderOptionsSpec`物件的`setPDFARevisionNumber`方法並傳遞`PDFARevisionNumber.Revision_1`，以設定`PDFARevisionNumber`值。

   >[!NOTE]
   >
   >PDF/A檔案的PDF版本是1.4，無論您為`RenderOptionsSpec`物件的&#x200B;`setPdfVersion`*方法指定哪個值。*

1. 產生PDF/檔案。

   呼叫`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF/A檔案：

   * `TransformationFormat`列舉值。 若要產生PDF/A檔案，請指定`TransformationFormat.PDFA`。
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`com.adobe.idp.Document`物件。

   `generatePDFOutput`方法傳回包含作業結果的`OutputResult`物件。

   >[!NOTE]
   >
   >`OutputResult`物件的`getRecordLevelMetaDataList`方法傳回`null`。

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput`2方法來建立PDF/A檔案。 (請參閱[將Content Services （已過時）中的檔案傳遞至輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 擷取作業的結果。

   * 呼叫`OutputResult`物件的`getStatusDoc`方法，建立代表`generatePDFOutput`方法狀態的`com.adobe.idp.Document`物件。
   * 建立將包含作業結果的`java.io.File`物件。 確認副檔名為.xml。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案（請確定您使用的是`getStatusDoc`方法傳回的`com.adobe.idp.Document`物件）。

   >[!NOTE]
   >
   >雖然Output服務會將PDF/A檔案寫入傳遞至`PDFOutputOptionsSpec`物件之`setFileURI`方法的引數所指定的位置，但您可以透過叫用`OutputResult`物件的`getGeneratedDoc`方法，以程式設計方式擷取PDF/A檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API建立PDF/A檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[正在設定連線內容](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用網站服務API建立PDF/檔案 {#create-a-pdf-a-document-using-the-web-service-api}

使用輸出API （Web服務）建立PDF/A檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 使用預設建構函式建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`OutputServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存將與PDF/A檔案合併的資料。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表要加密之PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列內容指派其`MTOM`欄位來填入`BLOB`物件。

1. 設定PDF/執行階段選項。

   * 使用物件的建構函式建立`PDFOutputOptionsSpec`物件。
   * 透過指派字串值來設定File URI選項，該字串值指定輸出服務產生給`PDFOutputOptionsSpec`物件的`fileURI`資料成員的PDF檔案位置。 檔案URI選項是相對於主控AEM Forms的J2EE應用程式伺服器，而非使用者端電腦

1. 設定演算執行階段選項。

   * 使用物件的建構函式建立`RenderOptionsSpec`物件。
   * 將`PDFAConformance`列舉值指派給`RenderOptionsSpec`物件的`PDFAConformance`資料成員，以設定`PDFAConformance`值。 例如，若要指定一致性層級A，請將`PDFAConformance.A`指派給此資料成員。
   * 將`PDFARevisionNumber`列舉值指派給`RenderOptionsSpec`物件的`PDFARevisionNumber`資料成員，以設定`PDFARevisionNumber`值。 將`PDFARevisionNumber.Revision_1`指派給此資料成員。

   >[!NOTE]
   >
   >PDF/A檔案的PDF版本是1.4，無論您指定哪個值。

1. 產生PDF/檔案。

   呼叫`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * TransformationFormat列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDFA`。
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`BLOB`物件。
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將描述檔案的產生中繼資料填入此物件。 （只有Web服務呼叫需要此引數值。）
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將結果資料填入此物件中。 （只有Web服務呼叫需要此引數值。）
   * 包含作業結果的`OutputResult`物件。 （只有Web服務呼叫需要此引數值。）

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput`2方法來建立PDF/A檔案。 (請參閱[將Content Services （已過時）中的檔案傳遞至輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 擷取作業的結果。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確認副檔名為.xml。
   * 建立位元組陣列，以儲存`BLOB`物件的資料內容，該物件是以`OutputServiceService`物件的`generatePDFOutput`方法（第八個引數）填入的結果資料。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將Content Services中的檔案傳遞（已棄用）至Output Service {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Output服務會根據通常儲存為XDP檔案並在Designer中建立的表單設計，轉譯非互動式PDF表單。 您可以將包含表單設計的`com.adobe.idp.Document`物件傳遞至Output服務。 然後Output服務會轉譯`com.adobe.idp.Document`物件中的表單設計。

將`com.adobe.idp.Document`物件傳遞至輸出服務的好處是，其他AEM Forms服務作業會傳回`com.adobe.idp.Document`執行個體。 也就是說，您可以從另一個服務作業取得`com.adobe.idp.Document`執行個體並加以轉譯。 例如，假設XDP檔案儲存在名為`/Company Home/Form Designs`的Content Services （已過時）節點中，如下圖所示。

您可以程式設計方式從Content Services （已棄用）擷取Loan.xdp，並將XDP檔案傳遞至`com.adobe.idp.Document`物件中的Output服務。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

若要將從Content Services取得的檔案（已棄用）傳遞至Output服務，請執行下列工作：

1. 包含專案檔案。
1. 建立輸出和Document Management Client API物件。
1. 從內容服務擷取表單設計（已棄用）。
1. 轉譯非互動式PDF表單。
1. 對資料流執行動作。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立輸出和Document Management Client API物件**

在您以程式設計方式執行輸出服務API作業之前，請先建立輸出使用者端API物件。 此外，由於此工作流程會從內容服務中擷取XDP檔案（已棄用），請建立檔案管理API物件。

**從內容服務擷取表單設計（已棄用）**

使用Java或網站服務API從內容服務擷取XDP檔案（已棄用）。 XDP檔案是在`com.adobe.idp.Document`執行個體中傳回（如果您使用Web服務，則是`BLOB`執行個體）。 然後您可以將`com.adobe.idp.Document`執行個體傳遞至輸出服務。

**轉譯非互動式PDF表單**

若要呈現非互動式表單，請將從Content Services （已棄用）傳回的`com.adobe.idp.Document`執行個體傳遞至Output服務。

>[!NOTE]
>
>名為`generatePDFOutput2`和g `eneratePrintedOutput2`的兩個新方法接受包含表單設計的`com.adobe.idp.Document`物件。 您也可以在傳送列印資料流至網路印表機時，將包含表單設計的`com.adobe.idp.Document`傳送至Output服務。

**使用表單資料流執行動作**

您可以將非互動式表單儲存為PDF檔案。 您可以在Adobe Reader或Acrobat中檢視表單。

**另請參閱**

[使用Java API將檔案傳遞至Output Service](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[使用網站服務API將檔案傳遞至輸出服務](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### 使用Java API將檔案傳遞至Output Service {#pass-documents-to-the-output-service-using-the-java-api}

使用輸出服務與內容服務（已棄用） API (Java)，傳遞從內容服務（已棄用）擷取的檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立輸出和Document Management Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。 （請參閱[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentManagementServiceClientImpl`物件。

1. 從內容服務擷取表單設計（已棄用）。

   叫用`DocumentManagementServiceClientImpl`物件的`retrieveContent`方法，並傳遞下列值：

   * 字串值，指定新增內容的存放區。 預設存放區為`SpacesStore`。 此值為必要引數。
   * 字串值，指定要擷取之內容的完整路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值為必要引數。
   * 字串值，指定版本。 此值是選用引數，您可以傳遞空字串。 在此情況下，會擷取最新版本。

   `retrieveContent`方法傳回包含XDP檔案的`CRCResult`物件。 透過叫用`CRCResult`物件的`getDocument`方法擷取`com.adobe.idp.Document`執行個體。

1. 轉譯非互動式PDF表單。

   叫用`OutputClient`物件的`generatePDFOutput2`方法，並傳遞下列值：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定影像等其他資源所在的內容根目錄。
   * 代表表單設計的`com.adobe.idp.Document`物件（使用`CRCResult`物件的`getDocument`方法傳回的執行個體）。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`com.adobe.idp.Document`物件。

   `generatePDFOutput2`方法傳回包含作業結果的`OutputResult`物件。

1. 使用表單資料流執行動作。

   * 叫用`OutputResult`物件的`getGeneratedDoc`方法，擷取代表非互動式表單的`com.adobe.idp.Document`物件。
   * 建立包含作業結果的`java.io.File`物件。 確認副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案（請確定您使用的是`getGeneratedDoc`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API將檔案傳遞至「輸出服務」](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[快速入門(SOAP模式)：使用Java API將檔案傳遞至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將檔案傳遞至輸出服務 {#pass-documents-to-the-output-service-using-the-web-service-api}

使用輸出服務與內容服務（已棄用） API （網頁服務），傳遞從內容服務（已棄用）擷取的檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 由於此使用者端應用程式會叫用兩個AEM Forms服務，請建立兩個服務參考。 使用下列WSDL定義作為與輸出服務相關聯的服務參考： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   使用下列WSDL定義作為與Document Management服務相關聯的服務參考： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   因為`BLOB`資料型別是兩個服務參考的共同型別，使用它時，請完全限定`BLOB`資料型別。 在對應的Web服務快速入門中，所有`BLOB`執行個體都是完全合格的。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立輸出和Document Management Client API物件。

   * 使用預設建構函式建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至Forms服務（例如，`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`OutputServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對`DocumentManagementServiceClient`服務使用者端重複這些步驟。

1. 從內容服務擷取表單設計（已棄用）。

   叫用`DocumentManagementServiceClient`物件的`retrieveContent`方法並傳遞下列值以擷取內容：

   * 字串值，指定新增內容的存放區。 預設存放區為`SpacesStore`。 此值為必要引數。
   * 字串值，指定要擷取之內容的完整路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值為必要引數。
   * 字串值，指定版本。 此值是選用引數，您可以傳遞空字串。 在此情況下，會擷取最新版本。
   * 儲存瀏覽連結值的字串輸出引數。
   * 儲存內容的`BLOB`輸出引數。 您可以使用此輸出引數來擷取內容。
   * 儲存內容屬性的`ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType`輸出引數。
   * `CRCResult`輸出引數。 您可以使用`BLOB`輸出引數來擷取內容，而不使用此物件。

1. 轉譯非互動式PDF表單。

   叫用`OutputServiceClient`物件的`generatePDFOutput2`方法，並傳遞下列值：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定影像等其他資源所在的內容根目錄。
   * 代表表單設計的`BLOB`物件(使用內容服務傳回的`BLOB`執行個體（已棄用）。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`BLOB`物件。
   * 由`generatePDFOutput2`方法填入的輸出`BLOB`物件。 `generatePDFOutput2`方法會將描述檔案的產生中繼資料填入此物件。 （只有Web服務呼叫才需要此引數值）。
   * 包含作業結果的輸出`OutputResult`物件。 （只有Web服務呼叫才需要此引數值）。

   `generatePDFOutput2`方法傳回包含非互動式PDF表單的`BLOB`物件。

1. 使用表單資料流執行動作。

   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表互動式PDF檔案檔案位置及開啟檔案模式的字串值。
   * 建立位元組陣列，儲存從`generatePDFOutput2`方法擷取的`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 將存放庫中的檔案傳遞至輸出服務 {#passing-documents-located-in-the-repository-to-the-output-service}

Output服務會根據通常儲存為XDP檔案並在Designer中建立的表單設計，轉譯非互動式PDF表單。 您可以將包含表單設計的`com.adobe.idp.Document`物件傳遞至Output服務。 然後Output服務會轉譯`com.adobe.idp.Document`物件中的表單設計。

將`com.adobe.idp.Document`物件傳遞至輸出服務的好處是，其他AEM Forms服務作業會傳回`com.adobe.idp.Document`執行個體。 也就是說，您可以從另一個服務作業取得`com.adobe.idp.Document`執行個體並加以轉譯。 例如，假設XDP檔案儲存在AEM Forms存放庫中，如下圖所示。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

*FormsFolder*&#x200B;資料夾是AEM Forms存放庫中的使用者定義位置（此位置為範例，預設不存在）。 在此範例中，名為Loan.xdp的表單設計位於此資料夾中。 除了表單設計之外，其他表單附屬資料（例如影像）也可以儲存在此位置。 AEM Forms存放庫中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

您可以程式設計方式從AEM Forms存放庫擷取Loan.xdp，並將其傳遞至`com.adobe.idp.Document`物件中的輸出服務。

您可以使用兩種方式之一，根據存放庫中的XDP檔案建立PDF。 您可以傳遞參考的XDP位置，或以程式設計方式從存放庫擷取XDP，並將其傳遞到XDP檔案中的輸出服務。

[快速入門（EJB模式）：使用Java API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)根據應用程式XDP檔案建立PDF檔案（顯示如何傳遞XDP檔案的位置，以供參考）。

[快速入門（EJB模式）：使用Java API將AEM Forms存放庫中的檔案傳遞至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (顯示如何以程式設計方式從AEM Forms存放庫擷取XDP檔案，並將其傳遞至`com.adobe.idp.Document`執行個體中的輸出服務)。 （本節將討論如何執行此工作）

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

若要將從AEM Forms存放庫取得的檔案傳遞至輸出服務，請執行以下工作：

1. 包含專案檔案。
1. 建立輸出和Document Management Client API物件。
1. 從AEM Forms存放庫擷取表單設計。
1. 轉譯非互動式PDF表單。
1. 對資料流執行動作。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立輸出和Document Management Client API物件**

在您以程式設計方式執行輸出服務API作業之前，請先建立輸出使用者端API物件。 此外，由於此工作流程會從內容服務中擷取XDP檔案（已棄用），請建立檔案管理API物件。

**從AEM Forms存放庫擷取表單設計**

使用存放庫API從AEM Forms存放庫擷取XDP檔案。 （請參閱[讀取資源](/help/forms/developing/aem-forms-repository.md#reading-resources)。）

XDP檔案是在`com.adobe.idp.Document`執行個體中傳回（如果您使用Web服務，則是`BLOB`執行個體）。 然後您可以將`com.adobe.idp.Document`執行個體傳遞至Output服務。

**轉譯非互動式PDF表單**

若要呈現非互動式表單，請傳遞使用AEM Forms存放庫API傳回的`com.adobe.idp.Document`執行個體。

>[!NOTE]
>
>名為`generatePDFOutput2`和`generatePrintedOutput2`的兩個新方法接受包含表單設計的`com.adobe.idp.Document`物件。 您也可以在傳送列印資料流至網路印表機時，將包含表單設計的`com.adobe.idp.Document`傳送至輸出服務。

**使用表單資料流執行動作**

您可以將非互動式表單儲存為PDF檔案。 您可以在Adobe Reader或Acrobat中檢視表單。

**另請參閱**

[使用Java API將存放庫中的檔案傳遞至輸出服務](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### 使用Java API將存放庫中的檔案傳遞至輸出服務 {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

使用輸出服務和存放庫API (Java)傳遞從存放庫擷取的檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar和adobe-repository-client.jar。

1. 建立輸出和Document Management Client API物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。 （請參閱[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentManagementServiceClientImpl`物件。

1. 從AEM Forms存放庫擷取表單設計。

   叫用`ResourceRepositoryClient`物件的`readResourceContent`方法，並將指定URI位置的字串值傳遞給XDP檔案。 例如 `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。此值為必填。 此方法會傳回代表XDP檔案的`com.adobe.idp.Document`執行個體。

1. 轉譯非互動式PDF表單。

   叫用`OutputClient`物件的`generatePDFOutput2`方法，並傳遞下列值：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定影像等其他資源所在的內容根目錄。 例如，`repository:///Applications/FormsApplication/1.0/FormsFolder/`。
   * 代表表單設計的`com.adobe.idp.Document`物件（使用`ResourceRepositoryClient`物件的`readResourceContent`方法傳回的執行個體）。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`com.adobe.idp.Document`物件。

   `generatePDFOutput2`方法傳回包含作業結果的`OutputResult`物件。

1. 使用表單資料流執行動作。

   * 叫用`OutputResult`物件的`getGeneratedDoc`方法，擷取代表非互動式表單的`com.adobe.idp.Document`物件。
   * 建立包含作業結果的`java.io.File`物件。 確認副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案（請確定您使用的是`getGeneratedDoc`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API將AEM Forms儲存庫中的檔案傳遞至Output服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用片段建立PDF檔案 {#creating-pdf-documents-using-fragments}

您可以使用輸出和組合器服務來建立以片段為基礎的輸出資料流，例如PDF檔案。 組合器服務會根據多個XDP檔案中的片段來組合XDP檔案。 組裝的XDP檔案會傳遞給Output服務，該服務會建立PDF檔案。 雖然此工作流程會顯示正在產生的PDF檔案，但「輸出」服務可以為此工作流程產生其他輸出型別，例如ZPL。 PDF檔案僅供討論之用。

下圖顯示此工作流程。

![cp_cp_outputassemblegrations](assets/cp_cp_outputassemblefragments.png)

在讀取&#x200B;*使用片段*&#x200B;建立PDF檔案之前，建議您熟悉使用組合器服務來組合多個XDP檔案。 （請參閱[組合多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)。）

>[!NOTE]
>
>您也可以將由組合器服務組裝的表單設計傳遞至Forms服務，而非輸出服務。 Output服務與Forms服務的主要差異在於Forms服務會產生互動式PDF檔案，而Output服務會產生非互動式PDF檔案。 此外，Forms服務無法產生ZPL等印表機輸出資料流。

>[!NOTE]
>
>如需有關Output服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

若要根據片段建立PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Output and Assembler Client物件。
1. 使用Assembler服務產生表單設計。
1. 使用Output服務產生PDF檔案。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立輸出和組合器使用者端物件**

在您以程式設計方式執行輸出服務API作業之前，請先建立輸出使用者端API物件。 此外，由於此工作流程會叫用Assembler服務來建立表單設計，因此請建立Assembler使用者端API物件。

**使用Assembler服務產生表單設計**

使用Assembler服務產生使用片段的表單設計。 組合器服務傳回包含表單設計的`com.adobe.idp.Document`執行個體。

**使用Output服務產生PDF檔案**

您可以使用Output服務，使用Assembler服務建立的表單設計來產生PDF檔案。 傳遞組合器服務傳回至輸出服務的`com.adobe.idp.Document`執行個體。

**將PDF檔案儲存為PDF檔案**

在Output服務產生PDF檔案後，您可以將其儲存為PDF檔案。

**另請參閱**

[使用Java API根據片段建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[使用Web服務API根據片段建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[組合多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents)

### 使用Java API根據片段建立PDF檔案 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

使用輸出服務API和組合器服務API (Java)，根據片段建立PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立Output and Assembler Client物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`AssemblerServiceClient`物件。

1. 使用Assembler服務產生表單設計。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列必要值：

   * 代表要使用的DDX檔案的`com.adobe.idp.Document`物件。
   * 包含輸入XDP檔案的`java.util.Map`物件。
   * 指定執行階段選項（包括預設字型和作業記錄層級）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件。

   `invokeDDX`方法傳回包含組合XDP檔案的`com.adobe.livecycle.assembler.client.AssemblerResult`物件。 若要擷取組裝的XDP檔案，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 此方法會傳回`java.util.Map`物件。
   * 逐一檢視`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件為止。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法以擷取組合的XDP檔案。

1. 使用Output服務產生PDF檔案。

   叫用`OutputClient`物件的`generatePDFOutput2`方法，並傳遞下列值：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`
   * 字串值，指定其他資源（例如影像）所在的內容根
   * 代表表單設計的`com.adobe.idp.Document`物件（使用Assembler服務傳回的執行個體）
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件
   * 包含演算執行階段選項的`RenderOptionsSpec`物件
   * 包含要與表單設計合併之資料的XML資料來源的`com.adobe.idp.Document`物件

   `generatePDFOutput2`方法傳回包含作業結果的`OutputResult`物件

1. 將PDF檔案儲存為PDF檔案。

   * 透過叫用`OutputResult`物件的`getGeneratedDoc`方法，擷取代表PDF檔案的`com.adobe.idp.Document`物件。
   * 建立包含作業結果的`java.io.File`物件。 請確認副檔名為.pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案。 （請確定您使用的是`getGeneratedDoc`方法傳回的`com.adobe.idp.Document`物件。）

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API根據片段建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[快速入門(SOAP模式)：使用Java API根據片段建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[正在設定連線內容](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服務API根據片段建立PDF檔案 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

使用輸出服務API和組合器服務API （Web服務），根據片段建立PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 針對與Output服務相關的服務參考，使用下列WSDL定義：

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   針對與Assembler服務相關的服務參考，使用下列WSDL定義：

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   因為`BLOB`資料型別是兩個服務參考的共同型別，使用它時，請完全限定`BLOB`資料型別。 在對應的Web服務快速入門中，所有`BLOB`執行個體都是完全合格的。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Output and Assembler Client物件。

   * 使用預設建構函式建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`OutputServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給`OutputServiceClient.ClientCredentials.UserName.UserName`欄位。
      * 將對應的密碼值指派給`OutputServiceClient.ClientCredentials.UserName.Password`欄位。
      * 將常數值`HttpClientCredentialType.Basic`指派給`BasicHttpBindingSecurity.Transport.ClientCredentialType`欄位。

   * 將`BasicHttpSecurityMode.TransportCredentialOnly`常數值指派給`BasicHttpBindingSecurity.Security.Mode`欄位。

   >[!NOTE]
   >
   >對`AssemblerServiceClient`物件重複這些步驟。

1. 使用Assembler服務產生表單設計。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列值：

   * 代表DDX檔案的`BLOB`物件
   * 包含必要檔案的`MyMapOf_xsd_string_To_xsd_anyType`物件
   * 指定執行階段選項的`AssemblerOptionSpec`物件

   `invokeDDX`方法傳回`AssemblerResult`物件，其中包含工作的結果和發生的任何例外狀況。 若要取得新建立的XDP檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，這是包含結果PDF檔案的`Map`物件。
   * 反複檢查`Map`物件以擷取組合表單設計。 將該陣列成員的`value`轉換為`BLOB`。 將此`BLOB`執行個體傳遞至輸出服務。

1. 使用Output服務產生PDF檔案。

   叫用`OutputServiceClient`物件的`generatePDFOutput2`方法，並傳遞下列值：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定其他資源（例如影像）所在的內容根目錄。
   * 代表表單設計的`BLOB`物件（使用組合器服務傳回的`BLOB`執行個體）。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`BLOB`物件。
   * `generatePDFOutput2`方法填入的輸出`BLOB`物件。 `generatePDFOutput2`方法會將描述檔案的產生中繼資料填入此物件。 （只有Web服務呼叫才需要此引數值）。
   * 包含作業結果的輸出`OutputResult`物件。 （只有Web服務呼叫才需要此引數值）。

   `generatePDFOutput2`方法傳回包含非互動式PDF表單的`BLOB`物件。

1. 將PDF檔案儲存為PDF檔案。

   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表互動式PDF檔案檔案位置及開啟檔案模式的字串值。
   * 建立位元組陣列，儲存從`generatePDFOutput2`方法擷取的`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 列印至檔案 {#printing-to-files}

您可以使用Output服務將如PostScript、印表機控制語言(PCL)或下列標籤格式等串流列印到檔案中：

* 斑馬 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用Output服務，您可以將XML資料與表單設計合併，並將表單列印到檔案中。 下圖顯示建立雷射和標籤檔案的「輸出」服務。

>[!NOTE]
>
>如需有關傳送列印資料流到印表機的資訊，請參閱[傳送列印資料流到印表機](creating-document-output-streams.md#sending-print-streams-to-printers)。

>[!NOTE]
>
>如需有關Output服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

若要列印至檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參考XML資料來源。
1. 設定列印至檔案所需的列印執行階段選項。
1. 將列印資料流列印到檔案。
1. 擷取作業的結果。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在受支援的J2EE應用程式伺服器（不是JBoss）上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在之J2EE應用程式伺服器的JAR檔案。 (請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`物件。

**參考XML資料來源**

若要列印包含資料的檔案，您必須針對每個要填入資料的表單欄位，參考包含XML元素的XML資料來源。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

**設定列印至檔案所需的列印執行階段選項**

若要列印至檔案，您必須指定輸出服務列印之檔案的位置和名稱，以設定檔案URI執行時間選項。 例如，若要指示輸出服務將名為&#x200B;*MortgageForm.ps*&#x200B;的PostScript檔案列印至C:\Adobe，請指定C:\Adobe\MortgageForm.ps。

>[!NOTE]
>
>您可以選擇定義執行階段選項。 如需您可以設定的所有選項的相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`PrintedOutputOptionsSpec`類別參考。

**將列印資料流列印到檔案**

在參照包含表單資料的有效XML資料來源並設定列印執行階段選項後，您可以叫用Output服務，使其列印檔案。

**擷取作業的結果**

Output服務執行作業之後，會傳回指定作業是否成功的各種資料專案，例如XML資料。

**另請參閱**

[使用Java API列印至檔案](creating-document-output-streams.md#print-to-files-using-the-java-api)

[使用Web服務API列印至檔案](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API列印至檔案 {#print-to-files-using-the-java-api}

使用Output API (Java)列印至檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。

1. 參考XML資料來源。

   * 使用檔案的建構函式，並傳遞指定XML檔案位置的字串值，建立代表用來填入檔案的XML資料來源的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定列印至檔案所需的列印執行階段選項。

   * 使用物件的建構函式建立`PrintedOutputOptionsSpec`物件。
   * 透過叫用PrintedOutputOptionsSpec物件的`setFileURI`方法並傳遞代表檔案名稱和位置的字串值來指定檔案。 例如，如果您希望輸出服務列印至C:\Adobe中名為MortgageForm.ps的PostScript檔案，請指定C:\\Adobe\MortgageForm.ps。
   * 透過叫用`PrintedOutputOptionsSpec`物件的`setCopies`方法並傳遞代表復本數的整數值來指定要列印的復本數。

1. 將列印資料流列印到檔案。

   透過叫用`OutputClient`物件的`generatePrintedOutput`方法並傳遞下列值來列印至檔案：

   * 指定要建立之列印資料流格式的`PrintFormat`列舉值。 例如，若要建立PostScript列印資料流，請傳遞`PrintFormat.PostScript`。
   * 字串值，指定表單設計的名稱。
   * 字串值，指定相關附屬檔案（例如影像檔案）的位置。
   * 字串值，指定要使用的XDC檔案位置（如果您使用`PrintedOutputOptionsSpec`物件指定要使用的XDC檔案，則可以傳遞`null`）。
   * 包含列印至檔案所需的執行階段選項的`PrintedOutputOptionsSpec`物件。
   * 包含包含表單資料之XML資料來源的`com.adobe.idp.Document`物件。

   `generatePrintedOutput`方法傳回包含作業結果的`OutputResult`物件。

   >[!NOTE]
   >
   >`OutputResult`物件的`getRecordLevelMetaDataList`方法傳回`null`。

1. 擷取作業的結果。

   * 呼叫`OutputResult`物件的`getStatusDoc`方法，建立代表`generatePrintedOutput`方法狀態的`com.adobe.idp.Document`物件（`generatePrintedOutput`方法傳回`OutputResult`物件）。
   * 建立將包含作業結果的`java.io.File`物件。 確認副檔名為XML。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案（請確定您使用的是`getStatusDoc`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API列印至檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[正在設定連線內容](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服務API列印至檔案 {#print-to-files-using-the-web-service-api}

使用Output API （Web服務）列印至檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 使用預設建構函式建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`OutputServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存表單資料。
   * 建立`System.IO.FileStream`物件，方法是叫用其建構函式，並傳遞字串值，指定包含表單資料的XML檔案位置。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`binaryData`屬性，填入`BLOB`物件。

1. 設定列印至檔案所需的列印執行階段選項。

   * 使用物件的建構函式建立`PrintedOutputOptionsSpec`物件。
   * 指定字串值來指定檔案，該字串值代表`PrintedOutputOptionsSpec`物件之`fileURI`資料成員的檔案位置和名稱。 例如，如果您希望輸出服務列印至C:\Adobe中名為&#x200B;*MortgageForm.ps*&#x200B;的PostScript檔案，請指定C:\\Adobe\MortgageForm.ps。
   * 指定整數值來指定要列印的份數，整數值代表`PrintedOutputOptionsSpec`物件的`copies`個資料成員的份數。

1. 將列印資料流列印到檔案。

   透過叫用`OutputServiceService`物件的`generatePrintedOutput`方法並傳遞下列值來列印至檔案：

   * 指定要建立之列印資料流格式的`PrintFormat`列舉值。 例如，若要建立PostScript列印資料流，請傳遞`PrintFormat.PostScript`。
   * 字串值，指定表單設計的名稱。
   * 字串值，指定相關附屬檔案（例如影像檔案）的位置。
   * 字串值，指定要使用的XDC檔案位置（如果您使用`PrintedOutputOptionsSpec`物件指定要使用的XDC檔案，則可以傳遞`null`）。
   * 包含列印至檔案所需的列印執行階段選項的`PrintedOutputOptionsSpec`物件。
   * 包含包含表單資料之XML資料來源的`BLOB`物件。
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將描述檔案的產生中繼資料填入此物件。 （只有Web服務呼叫需要此引數值。）
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將結果資料填入此物件中。 （只有Web服務呼叫需要此引數值。）
   * 包含作業結果的`OutputResult`物件。 （只有Web服務呼叫需要此引數值。）

1. 擷取作業的結果。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確認副檔名為XML。
   * 建立位元組陣列，以儲存`BLOB`物件的資料內容，該物件是以`OutputServiceService`物件的`generatePDFOutput`方法（第八個引數）填入的結果資料。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 傳送列印資料流至印表機 {#sending-print-streams-to-printers}

您可以使用Output服務將列印資料流(例如PostScript、印表機控制語言(PCL)或下列標籤格式)傳送至網路印表機：

* 斑馬 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用Output服務，您可以將XML資料與表單設計合併，並將表單輸出為列印資料流。 例如，您可以建立PostScript列印資料流，並將其傳送至網路印表機。 下圖顯示Output服務傳送列印資料流至網路印表機。

>[!NOTE]
>
>為了示範如何傳送列印資料流至網路印表機，本節會使用SharedPrinter印表機通訊協定，將PostScript列印資料流傳送至網路印表機。

>[!NOTE]
>
>如需有關Output服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

若要將列印資料流傳送至網路印表機，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參考XML資料來源。
1. 設定列印執行階段選項
1. 擷取要列印的檔案。
1. 將檔案傳送至網路印表機。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在受支援的J2EE應用程式伺服器（不是JBoss）上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在之J2EE應用程式伺服器的JAR檔案。

**建立輸出使用者端物件**

在您以程式設計方式執行輸出服務作業之前，請先建立輸出服務使用者端物件。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceClient`物件。

**參考XML資料來源**

若要列印包含資料的檔案，您必須針對每個要填入資料的表單欄位，參考包含XML元素的XML資料來源。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

**設定列印執行階段選項**

當傳送列印資料流至印表機時，您可以設定執行階段選項，包括下列選項：

* **份數**：指定要傳送至印表機的份數。 預設值為 1。
* **裝訂**：使用裝訂器時會設定XCI選項。 此選項可由裝訂元素在組態模型中指定，並且僅用於PS和PCL印表機。
* **OutputJog**：當輸出頁面應該以角拐方式移動（實際在輸出匣中移動）時，會設定XCI選項。 此選項僅適用於PS和PCL印表機。
* **OutputBin**：用來啟用列印驅動程式以選取適當輸出紙匣的XCI值。

>[!NOTE]
>
>如需您可以設定的所有執行階段選項的相關資訊，請參閱`PrintedOutputOptionsSpec`類別參考。

**擷取要列印的檔案**

擷取列印資料流以傳送至印表機。 例如，您可以擷取PostScript檔案，並將其傳送至印表機。

如果您的印表機支援PDF，您可以選擇傳送PDF檔案。 但是，將PDF檔案傳送至印表機的問題是每個印表機製造商都有不同的PDF解譯器實作。 也就是說，有些列印製造商會使用Adobe PDF的解讀，但這取決於印表機。 其他印表機有自己的PDF解譯器。 因此，列印結果可能會有所不同。

傳送PDF檔案至印表機的另一個限制是它只會列印；它無法存取雙面列印、紙匣選擇和裝訂，除非透過印表機的設定。

若要擷取要列印的檔案，請使用`generatePrintedOutput`方法。 下表指定在使用`generatePrintedOutput`方法時，為指定列印資料流設定的內容型別。

<table>
 <thead>
  <tr>
   <th><p>列印格式 </p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>依預設或自訂xdc輸出資料流建立dpl203.xdc。</p></td>
  </tr>
  <tr>
   <td><p>DPL300DPI </p></td>
   <td><p>建立DPL 300 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>DPL406DPI </p></td>
   <td><p>建立DPL 400 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>DPL600DPI </p></td>
   <td><p>建立DPL 600 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>建立一般色彩PCL (5c)輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>建立一般PostScript Level 3輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>建立自訂IPL輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>IPL300DPI </p></td>
   <td><p>建立IPL 300 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>IPL400DPI </p></td>
   <td><p>建立IPL 400 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>建立一般單色PCL (5e)輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>建立一般PostScript Level 2輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>建立自訂TPCL輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL305DPI </p></td>
   <td><p>建立TPCL 305 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL600DPI </p></td>
   <td><p>建立TPCL 600 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>建立ZPL 203 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>ZPL300DPI </p></td>
   <td><p>建立ZPL 300 DPI輸出資料流。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您也可以使用`generatePrintedOutput2`方法將列印資料流傳送至印表機。 不過，與「傳送列印資料流至印表機」區段相關的快速啟動會使用`generatePrintedOutput`方法。

**傳送列印資料流至網路印表機**

擷取要列印的檔案後，您可以叫用「輸出」服務，使其將列印資料流傳送至網路印表機。 若要讓「輸出」服務成功找到印表機，您必須同時指定列印伺服器和印表機名稱。 此外，您也必須指定列印通訊協定。

>[!NOTE]
>
>如果PDFG已安裝在Forms伺服器上，且伺服器在Windows Server 2008上執行，則無法使用SharedPrinter屬性。 在此情況下，請使用不同的印表機通訊協定。

>[!NOTE]
>
>如果您使用網路印表機，且存取機製為SharedPrinter，則需要指定印表機的完整網路路徑。使用Java API將列印資料流傳送至網路印表機

使用輸出API (Java)將列印資料流傳送至網路印表機：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。

1. 參考XML資料來源

   * 使用檔案的建構函式，並傳遞指定XML檔案位置的字串值，建立代表用來填入檔案的XML資料來源的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定列印執行階段選項

   建立代表列印執行階段選項的`PrintedOutputOptionsSpec`物件。 例如，您可以透過叫用`PrintedOutputOptionsSpec`物件的`setCopies`方法來指定要列印的份數。

   >[!NOTE]
   >
   >如果您正在產生ZPL列印資料流，就無法使用`PrintedOutputOptionsSpec`物件的`setPagination`方法來設定分頁值。 同樣地，您無法為ZPL列印資料流設定下列選項：OutputJog、PageOffset和Staple。 `setPagination`方法對於PostScript產生無效。 它只適用於PCL產生。

1. 擷取要列印的檔案

   * 叫用`OutputClient`物件的`generatePrintedOutput`方法並傳遞下列值，以擷取要列印的檔案：

      * 指定列印資料流的`PrintFormat`列舉值。 例如，若要建立PostScript列印資料流，請傳遞`PrintFormat.PostScript`。
      * 字串值，指定表單設計的名稱。
      * 字串值，指定相關附屬檔案（例如影像檔案）的位置。
      * 字串值，指定要使用的XDC檔案位置。
      * 包含列印至檔案所需之執行階段選項的`PrintedOutputOptionsSpec`物件。
      * `com.adobe.idp.Document`物件，代表包含要與表單設計合併之表單資料的XML資料來源。

     此方法會傳回包含作業結果的`OutputResult`物件。

   * 呼叫`OutputResult`物件的`getGeneratedDoc`方法，建立要傳送到印表機的`com.adobe.idp.Document`物件。 此方法會傳回`com.adobe.idp.Document`物件。

1. 傳送列印資料流至網路印表機

   透過叫用`OutputClient`物件的`sendToPrinter`方法並傳遞下列值，將列印資料流傳送至網路印表機：

   * 代表要傳送至印表機之列印資料流的`com.adobe.idp.Document`物件。
   * 指定要使用的印表機通訊協定的`PrinterProtocol`列舉值。 例如，若要指定SharedPrinter通訊協定，請傳遞`PrinterProtocol.SharedPrinter`。
   * 指定列印伺服器名稱的字串值。 例如，假設列印伺服器的名稱為PrintSever1，請傳遞`\\\PrintSever1`。
   * 字串值，指定印表機的名稱。 例如，假設印表機的名稱為Printer1，請傳遞`\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >已在8.2.1版中將`sendToPrinter`方法新增至AEM Forms API。

### 使用網站服務API傳送列印資料流至印表機 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

使用輸出API （網頁服務）將列印資料流傳送至網路印表機：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 使用預設建構函式建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`OutputServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存表單資料。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞字串值，指定包含表單資料之XML檔案的位置。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 取得`System.IO.FileStream`物件的`Length`屬性以決定位元組陣列長度。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 設定列印執行階段選項。

   使用物件的建構函式建立`PrintedOutputOptionsSpec`物件。 例如，您可以指定整數值來指定要列印的份數，該值代表`PrintedOutputOptionsSpec`物件的`copies`資料成員的份數。

   >[!NOTE]
   >
   >如果您正在產生ZPL列印資料流，則無法使用`PrintedOutputOptionsSpec`物件的`pagination`資料成員來設定分頁值。 同樣地，您無法為ZPL列印資料流設定下列選項：OutputJog、PageOffset和Staple。 `pagination`資料成員對於PostScript產生無效。 它只適用於PCL產生。

1. 擷取要列印的檔案。

   * 叫用`OutputServiceService`物件的`generatePrintedOutput`方法並傳遞下列值，以擷取要列印的檔案：

      * 指定列印資料流的`PrintFormat`列舉值。 例如，若要建立PostScript列印資料流，請傳遞`PrintFormat.PostScript`。
      * 字串值，指定表單設計的名稱。
      * 字串值，指定相關附屬檔案（例如影像檔案）的位置。
      * 字串值，指定要使用的XDC檔案位置。
      * `PrintedOutputOptionsSpec`物件，其中包含傳送列印資料流至網路印表機時使用的列印執行時間選項。
      * 包含包含表單資料之XML資料來源的`BLOB`物件。
      * 由`generatePrintedOutput`方法填入的`BLOB`物件。 `generatePrintedOutput`方法會將描述檔案的產生中繼資料填入此物件。 （只有Web服務呼叫需要此引數值。）
      * 由`generatePrintedOutput`方法填入的`BLOB`物件。 `generatePrintedOutput`方法會將結果資料填入此物件中。 （只有Web服務呼叫需要此引數值。）
      * 包含作業結果的`OutputResult`物件。 （只有Web服務呼叫需要此引數值。）

   * 取得`OutputResult`物件的`generatedDoc`方法的值，建立要傳送至印表機的`BLOB`物件。 此方法傳回的`BLOB`物件包含`generatePrintedOutput`方法傳回的PostScript資料。

1. 傳送列印資料流至網路印表機。

   透過叫用`OutputClient`物件的`sendToPrinter`方法並傳遞下列值，將列印資料流傳送至網路印表機：

   * 代表要傳送至印表機之列印資料流的`BLOB`物件。
   * 指定要使用的印表機通訊協定的`PrinterProtocol`列舉值。 例如，若要指定SharedPrinter通訊協定，請傳遞`PrinterProtocol.SharedPrinter`。
   * 指定是否要使用先前引數值的`bool`值。 傳遞值`true`。 （只有Web服務呼叫需要此引數值。）
   * 指定列印伺服器名稱的字串值。 例如，假設列印伺服器的名稱為PrintSever1，請傳遞`\\\PrintSever1`。
   * 字串值，指定印表機的名稱。 例如，假設印表機的名稱為Printer1，請傳遞`\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >已在8.2.1版中將`sendToPrinter`方法新增至AEM Forms API。

## 建立多個輸出檔案 {#creating-multiple-output-files}

Output服務可以為XML資料來源內的每個記錄建立個別的檔案，或是包含所有記錄的單一檔案（此功能為預設值）。 例如，假設有10筆記錄位於XML資料來源中，您指示輸出服務使用輸出服務API為每個記錄建立個別的PDF檔案（或其他型別的輸出）。 因此，Output服務會產生十份PDF檔案。 （您可以傳送多個列印資料流至印表機，而不建立檔案。）

下圖也顯示處理包含多個記錄之XML資料檔案的輸出服務。 不過，假設您指示輸出服務建立包含所有資料記錄的單一PDF檔案。 在這種情況下，Output服務會產生一個包含所有記錄的檔案。

下圖顯示處理包含多個記錄之XML資料檔案的輸出服務。 假設您指示輸出服務為每個資料記錄建立個別的PDF檔案。 在這種情況下，Output服務會為每個資料記錄產生個別的PDF檔案。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

下列XML資料顯示包含三個資料記錄的資料檔案範例。

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

請注意，每個資料記錄開始和結束的XML元素是`LoanRecord`。 產生多個檔案的應用程式邏輯會參考此XML元素。

>[!NOTE]
>
>如需有關Output服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

若要根據XML資料來源建立多個PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參考XML資料來源。
1. 設定PDF執行階段選項。
1. 設定演算執行階段選項。
1. 產生多個PDF檔案。
1. 擷取作業的結果。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在受支援的J2EE應用程式伺服器（不是JBoss）上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在之J2EE應用程式伺服器的JAR檔案。

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`物件。

**參考XML資料來源**

參考包含多個記錄的XML資料來源。 必須使用XML元素來分隔資料記錄。 例如，在本節前面顯示的範例XML資料來源中，分隔資料記錄的XML元素名為`LoanRecord`。

每個要填入資料的表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

**設定PDF執行階段選項**

設定Output服務的下列執行階段選項，以根據XML資料來源成功建立多個檔案：

* **許多檔案**：指定輸出服務是建立單一檔案，還是建立多個檔案。 您可以指定true或false。 若要為XML資料來源中的每個資料記錄建立個別的檔案，請指定true。
* **檔案URI**：指定輸出服務產生的檔案位置。 例如，假設您指定C:\\Adobe\forms\Loan.pdf。 在此情況下，Output服務會建立名為Loan.pdf的檔案，並將該檔案放在C:\\Adobe\forms資料夾中。 如果有多個檔案，檔案名稱為Loan0001.pdf、Loan0002.pdf、Loan0003.pdf等。 如果您指定檔案位置，檔案會放置在伺服器上，而非使用者端電腦上。
* **記錄名稱**：指定資料來源中用來分隔資料記錄的XML元素名稱。 例如，在本節前面顯示的範例XML資料來源中，分隔資料記錄的XML元素稱為`LoanRecord`。 (您不必設定「記錄名稱」執行時間選項，而是可以將「記錄層次」指定為一個數值，表示包含資料記錄的元素層次，以設定「記錄層次」。 不過，您只能設定「記錄名稱」或「記錄層次」。 您無法同時設定這兩個值。)

**設定演算執行階段選項**

您可以在建立多個檔案時設定演算執行階段選項。 雖然這些選項並非必要（不同於必要的輸出執行階段選項），但您可以執行工作，例如改善「輸出」服務的效能。 例如，您可以快取Output服務用來改善效能的表單設計。

Output服務處理批次記錄時，會以累加方式讀取包含多個記錄的資料。 也就是說，Output服務會將資料讀入記憶體，並在批次記錄處理時釋出資料。 設定兩個執行階段選項之一時，輸出服務會以累加方式載入資料。 如果您設定[記錄名稱]執行階段選項，Output服務會以累加方式讀取資料。 同樣地，如果您將「記錄層級」執行時間選項設為2或更大，Output服務會以累加方式讀取資料。

您可以使用`PDFOutputOptionsSpec`或`PrintedOutputOptionSpec`物件的`setLazyLoading`方法控制輸出服務是否執行增量載入。 您可以將值`false`傳遞至此方法，此方法會關閉累加式載入。

**產生多個PDF檔案**

在參照包含多個資料記錄並設定執行階段選項的有效XML資料來源後，您可以叫用Output服務，使其產生多個檔案。 產生多個記錄時，`OutputResult`物件的`getGeneratedDoc`方法會傳回`null`。

**擷取作業的結果**

Output服務執行作業之後，會傳回指定作業是否成功的XML資料。 Output服務會傳回下列XML。 在此情況下，Output服務會產生42份檔案。

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

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立多個PDF檔案 {#create-multiple-pdf-files-using-the-java-api}

使用Output API (Java)建立多個PDF檔案：

1. 包含專案檔案」

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。

1. 參考XML資料來源

   * 使用它的建構函式並傳遞指定XML檔案位置的字串值，建立代表包含多個記錄的XML資料來源的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定PDF執行階段選項

   * 使用物件的建構函式建立`PDFOutputOptionsSpec`物件。
   * 透過叫用`PDFOutputOptionsSpec`物件的`setGenerateManyFiles`方法來設定[許多檔案]選項。 例如，傳遞值`true`以指示輸出服務為XML資料來源中的每個記錄建立個別的PDF檔案。 (如果您傳遞`false`，Output服務會產生包含所有記錄的單一PDF檔案)。
   * 透過叫用`PDFOutputOptionsSpec`物件的`setFileUri`方法並傳遞字串值來設定檔案URI選項，該字串值指定輸出服務產生的檔案位置。 檔案URI選項是相對於主控AEM Forms的J2EE應用程式伺服器，而非使用者端電腦。
   * 透過叫用`OutputOptionsSpec`物件的`setRecordName`方法並傳遞字串值來設定「記錄名稱」選項，該字串值指定資料來源中用於分隔資料記錄的XML元素名稱。 (例如，請考量本節前面顯示的XML資料來源。 分隔資料記錄的XML元素名稱為LoanRecord)。

1. 設定演算執行階段選項

   * 使用物件的建構函式建立`RenderOptionsSpec`物件。
   * 快取表單設計以透過叫用`RenderOptionsSpec`物件的`setCacheEnabled`並傳遞`true`的`Boolean`值來改善輸出服務的效能。

1. 產生多個PDF檔案

   叫用`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以產生多個PDF檔案：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`com.adobe.idp.Document`物件。

   `generatePDFOutput`方法傳回包含作業結果的`OutputResult`物件。

1. 擷取作業的結果

   * 建立代表將包含`generatePDFOutput`方法結果的XML檔案的`java.io.File`物件。 確認副檔名為.xml。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案（請確定您使用的是`applyUsageRights`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API建立多個PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API建立多個PDF檔案 {#create-multiple-pdf-files-using-the-web-service-api}

使用輸出API （Web服務）建立多個PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 使用預設建構函式建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`OutputServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存包含多個記錄的表單資料。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表包含多個記錄之XML檔案的檔案位置的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 設定PDF執行階段選項。

   * 使用物件的建構函式建立`PDFOutputOptionsSpec`物件。
   * 為`OutputOptionsSpec`物件的`generateManyFiles`資料成員指派布林值，以設定[許多檔案]選項。 例如，將值`true`指派給此資料成員，以指示輸出服務為XML資料來源中的每個記錄建立個別的PDF檔案。 (如果您將`false`指派給此資料成員，則Output服務會產生包含所有記錄的單一PDF)。
   * 指定字串值來設定檔案URI選項，該字串值指定輸出服務產生給`OutputOptionsSpec`物件的`fileURI`資料成員的檔案位置。 檔案URI選項是相對於主控AEM Forms的J2EE應用程式伺服器，而非使用者端電腦。
   * 指定字串值來設定記錄名稱選項，該字串值指定資料來源中的XML元素名稱，該資料來源可將資料記錄分隔至`OutputOptionsSpec`物件的`recordName`資料成員。
   * 指定整數值，指定輸出服務產生給`OutputOptionsSpec`物件的`copies`資料成員的復本數目，以設定復本選項。

1. 設定演算執行階段選項。

   * 使用物件的建構函式建立`RenderOptionsSpec`物件。
   * 快取表單設計以透過將值`true`指派給`RenderOptionsSpec`物件的`cacheEnabled`資料成員來改善Output服務的效能。

1. 產生多個PDF檔案。

   叫用`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立多個PDF檔案：

   * TransformationFormat列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`BLOB`物件。
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將描述檔案的產生中繼資料填入此物件。
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將結果資料填入此物件中。
   * 包含作業結果的`OutputResult`物件。

1. 擷取作業的結果

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確認副檔名為.xml。
   * 建立位元組陣列，以儲存`BLOB`物件的資料內容，該物件是以`OutputServiceService`物件的`generatePDFOutput`方法（第八個引數）填入的結果資料。 取得`BLOB`物件的`binaryData`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立搜尋規則 {#creating-search-rules}

您可以建立搜尋規則，讓輸出服務檢查輸入資料，並根據資料內容使用不同的表單設計來產生輸出。 例如，如果文字&#x200B;*mortgage*&#x200B;位於輸入資料中，則輸出服務可以使用名為Mortgage.xdp的表單設計。 同樣地，如果輸入資料中有文字&#x200B;*automobile*，則輸出服務可以使用儲存為AutomobileLoan.xdp的表單設計。 雖然Output服務可以產生不同的輸出型別，但本節假設了Output服務會產生PDF檔案。 下圖顯示透過處理XML資料檔案並使用許多表單設計之一來產生PDF檔案的Output服務。

此外，Output服務能夠產生檔案套件，其中資料集中提供了多個記錄，每個記錄都與一個表單設計相符，並且由多個表單設計產生單個檔案。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>如需有關Output服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

若要指示Output服務在產生檔案時使用搜尋規則，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參考XML資料來源。
1. 定義搜尋規則。
1. 設定PDF執行階段選項。
1. 設定演算執行階段選項。
1. 產生PDF檔案。
1. 擷取作業的結果。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在受支援的J2EE應用程式伺服器（不是JBoss）上，則您必須將adobe-utilities.jar和jbossall-client.jar取代為特定於已部署AEM Forms之J2EE應用程式伺服器的JAR檔案。

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。

**參考XML資料來源**

每個要填入資料的表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 只要指定所有XML元素，就不需要比對XML元素的顯示順序。

**定義搜尋規則**

若要定義搜尋規則，您可以定義「輸出」服務在輸入資料中搜尋的一或多個文字模式。 針對您定義的每個文字模式，指定在文字模式所在位置所使用的對應表單設計。 如果找到文字模式，則Output服務會使用對應的表單設計產生輸出。 文字模式的範例為&#x200B;*按揭*。

>[!NOTE]
>
>如果找不到文字圖樣，則會使用預設的表單。 請確定您使用的所有表單設計都位於內容根目錄中。

**設定PDF執行階段選項**

設定下列PDF執行階段選項，讓Output服務根據多個表單設計成功建立PDF檔案：

* **檔案URI**：指定輸出服務產生的PDF檔案的名稱和位置。
* **規則**：指定您定義的規則。
* **LookAHead**：指定從輸入資料檔案的開頭開始要用來掃描已定義文字模式的位元組數。 預設值為500位元組。

**設定演算執行階段選項**

您可以在建立PDF檔案時設定演算執行階段選項。 雖然這些選項並非必要專案(不同於PDF執行階段選項)，但您可以執行工作，例如改善Output服務的效能。 例如，您可以快取Output服務用來改善效能的表單設計。

**產生PDF檔案**

參照有效的XML資料來源並設定執行階段選項後，您可以叫用Output服務，使其產生PDF檔案。 如果Output服務在輸入資料中找到指定的文字模式，則會使用對應的表單設計。 如果未使用文字模式，則Output服務會使用預設的表單設計。

**擷取作業的結果**

Output服務執行作業之後，會傳回指定作業是否成功的XML資料。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立搜尋規則 {#create-search-rules-using-the-java-api}

使用Output API (Java)建立搜尋規則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。

1. 參考XML資料來源。

   * 建立`java.io.FileInputStream`物件，代表用來填入PDF檔案的XML資料來源，使用它的建構函式，並傳遞指定XML檔案位置的字串值。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 定義搜尋規則。

   * 使用物件的建構函式建立`Rule`物件。
   * 透過叫用`Rule`物件的`setPattern`方法並傳遞指定文字模式的字串值來定義文字模式。
   * 透過叫用`Rule`物件的`setForm`方法定義對應的表單設計。 傳遞指定表單設計名稱的字串值。

   >[!NOTE]
   >
   >針對您要定義的每個文字模式，重複前三個子步驟。

   * 使用`java.util.ArrayList`建構函式建立`java.util.List`物件。
   * 針對您建立的每個`Rule`物件，叫用`java.util.List`物件的`add`方法，並傳遞`Rule`物件。

1. 設定PDF執行階段選項。

   * 使用物件的建構函式建立`PDFOutputOptionsSpec`物件。
   * 指定輸出服務透過叫用`PDFOutputOptionsSpec`物件的`setFileURI`方法所產生PDF檔案的名稱和位置。 傳遞字串值，指定PDF檔案的位置。 檔案URI選項是相對於主控AEM Forms的J2EE應用程式伺服器，而非使用者端電腦。
   * 透過叫用`PDFOutputOptionsSpec`物件的`setRules`方法設定您定義的規則。 傳遞包含`Rule`物件的`java.util.List`物件。
   * 透過叫用`PDFOutputOptionsSpec`物件的`setLookAhead`方法，設定要掃描已定義文字模式的位元組數。 傳遞代表位元組數的整數值。

1. 設定演算執行階段選項。

   * 使用物件的建構函式建立`RenderOptionsSpec`物件。
   * 快取表單設計以透過叫用`RenderOptionsSpec`物件的`setCacheEnabled`並傳遞`true`來改善輸出服務的效能。

1. 產生PDF檔案。

   叫用`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，產生以多個表單設計為基礎的PDF檔案：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定預設表單設計的名稱。 亦即，當找不到文字圖樣時，所使用的表單設計。
   * 字串值，指定表單設計所在的內容根。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * `com.adobe.idp.Document`物件，其中包含由Output服務針對定義的文字模式所搜尋的表單資料。

   `generatePDFOutput`方法傳回包含作業結果的`OutputResult`物件。

1. 擷取作業的結果。

   * 呼叫`OutputResult`物件的`getStatusDoc`方法，建立代表`generatePDFOutput`方法狀態的`com.adobe.idp.Document`物件。
   * 建立將包含作業結果的`java.io.File`物件。 確認副檔名為.xml。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案（請確定您使用的是`getStatusDoc`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API建立搜尋規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[快速入門(SOAP模式)：使用Java API建立搜尋規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立搜尋規則 {#create-search-rules-using-the-web-service-api}

使用輸出API （Web服務）建立搜尋規則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 使用預設建構函式建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`OutputServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存將與PDF檔案合併的資料。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表要加密之PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 定義搜尋規則。

   * 使用物件的建構函式建立`Rule`物件。
   * 藉由指派字串值來定義文字模式，該字串值會指定文字模式給`Rule`物件的`pattern`資料成員。
   * 藉由指派字串值來定義對應的表單設計，該字串值指定表單設計給`Rule`物件的`form`資料成員。

   >[!NOTE]
   >
   >針對您要定義的每個文字模式，重複前三個子步驟。

   * 建立儲存規則的`MyArrayOf_xsd_anyType`物件。
   * 將每個`Rule`物件指派給`MyArrayOf_xsd_anyType`陣列的元素。 為每個`Rule`物件叫用`MyArrayOf_xsd_anyType`物件的`Add`方法。

1. 設定PDF執行階段選項

   * 使用物件的建構函式建立`PDFOutputOptionsSpec`物件。
   * 指定字串值來設定檔案URI選項，該字串值指定輸出服務產生給`PDFOutputOptionsSpec`物件的`fileURI`資料成員的PDF檔案位置。 檔案URI選項是相對於主控AEM Forms的J2EE應用程式伺服器，而非使用者端電腦。
   * 指定整數值，指定輸出服務產生給`PDFOutputOptionsSpec`物件的`copies`資料成員的復本數目，以設定復本選項。
   * 將儲存規則的`MyArrayOf_xsd_anyType`物件指派給`PDFOutputOptionsSpec`物件的`rules`資料成員，以設定您定義的規則。
   * 將代表要掃描位元組數的整數值指派給`PDFOutputOptionsSpec`物件的`lookAhead`資料方法，以設定要掃描已定義文字模式的位元組數。

1. 設定演算執行階段選項

   * 使用物件的建構函式建立`RenderOptionsSpec`物件。
   * 快取表單設計以透過將值`true`指派給`RenderOptionsSpec`物件的`cacheEnabled`資料成員來改善Output服務的效能。

   >[!NOTE]
   >
   >如果輸入檔案是Acrobat表單，則您無法使用`RenderOptionsSpec`物件的`pdfVersion`成員來設定PDF檔案的版本。 輸出PDF檔案會保留Acrobat表單的PDF版本。 同樣地，如果輸入檔案是Acrobat表單，則您無法使用`RenderOptionsSpec`物件的`taggedPDF`方法來設定標籤的PDF選項。

   >[!NOTE]
   >
   >如果輸入PDF檔案是經認證或數位簽署的，則您無法使用`RenderOptionsSpec`物件的`linearizedPDF`成員來設定線性PDF選項。 如需詳細資訊，請參閱[數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。

1. 產生PDF檔案

   呼叫`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * 包含PDF執行階段選項的`PDFOutputOptionsSpec`物件。
   * 包含轉譯執行階段選項的`RenderOptionsSpec`物件。
   * 包含要與表單設計合併之資料的XML資料來源的`BLOB`物件。
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將描述檔案的產生中繼資料填入此物件。 （只有Web服務呼叫才需要此引數值）。
   * 由`generatePDFOutput`方法填入的`BLOB`物件。 `generatePDFOutput`方法會將結果資料填入此物件中。 （只有Web服務呼叫才需要此引數值）。
   * 包含作業結果的`OutputResult`物件。 （只有Web服務呼叫才需要此引數值）。

   >[!NOTE]
   >
   >當透過叫用`generatePDFOutput`方法產生PDF檔案時，您無法將資料與已簽署、已驗證或包含使用許可權的XFAPDF表單合併。 如需使用許可權的相關資訊，請參閱[將使用許可權套用至PDF檔案](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。

1. 擷取作業的結果

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確認副檔名為XML。
   * 建立位元組陣列，以儲存`BLOB`物件的資料內容，該物件是以`OutputServiceService`物件的`generatePDFOutput`方法（第八個引數）填入的結果資料。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 平面化PDF檔案 {#flattening-pdf-documents}

您可以使用Output服務將互動式PDF檔案轉換為非互動式PDF。 互動式PDF檔案可讓使用者輸入或修改PDF檔案欄位中的資料。 將互動PDF檔案轉換為非互動PDF檔案的程式稱為&#x200B;*平面化*。 將PDF檔案平面化時，使用者無法修改檔案欄位中的資料。 平面化PDF檔案的一個原因是為了確保無法修改資料。

您可以平面化下列PDF檔案型別：

* 互動式XFAPDF檔案
* Acrobat Forms

嘗試平面化非互動式PDF檔案的PDF會產生例外狀況。

>[!NOTE]
>
>如需有關Output服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-9}

若要將互動式PDF檔案平面化為非互動式PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 擷取互動式PDF檔案。
1. 轉換PDF檔案。
1. 將非互動式PDF檔案儲存為PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您是使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在受支援的J2EE應用程式伺服器（不是JBoss）上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在之J2EE應用程式伺服器的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用輸出Web服務API，請建立`OutputServiceService`物件。

**擷取互動式PDF檔案**

擷取您要轉換成非互動式PDF檔案的互動式PDF檔案。 嘗試轉換非互動式PDF檔案會產生例外狀況。

**轉換PDF檔案**

擷取互動式PDF檔案後，可將其轉換成非互動式PDF檔案。 Output服務會傳回非互動式PDF檔案。

**將非互動式PDF檔案儲存為PDF檔案**

您可以將非互動式PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API平面化PDF檔案](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[使用網站服務API平面化PDF檔案](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API平面化PDF檔案 {#flatten-a-pdf-document-using-the-java-api}

使用Output API (Java)將互動式PDF檔案平面化為非互動式PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`OutputClient`物件。

1. 擷取互動式PDF檔案。

   * 建立代表互動式PDF檔案的`java.io.FileInputStream`物件，使用它的建構函式並傳遞字串值(指定互動式PDF檔案的位置)來進行轉換。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 轉換PDF檔案。

   呼叫`OutputServiceService`物件的`transformPDF`方法並傳遞下列值，將互動式PDF檔案轉換為非互動式PDF檔案：

   * 包含互動式PDF檔案的`com.adobe.idp.Document`物件。
   * `TransformationFormat`列舉值。 若要產生非互動式PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定修訂編號的`PDFARevisionNumber`列舉值。 由於此引數適用於PDF/檔案，因此您可以指定`null`。
   * 代表修訂編號和年份的字串值，以冒號分隔。 由於此引數適用於PDF/檔案，因此您可以指定`null`。
   * 代表PDF/A一致性層級的`PDFAConformance`列舉值。 由於此引數適用於PDF/檔案，因此您可以指定`null`。

   `transformPDF`方法傳回包含非互動式PDF檔案的`com.adobe.idp.Document`物件。

1. 將非互動式PDF檔案儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案（請確定您使用的是`transformPDF`方法傳回的`Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API轉換PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[快速入門(SOAP模式)：使用Java API轉換PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API平面化PDF檔案 {#flatten-a-pdf-document-using-the-web-service-api}

使用Output API （Web服務）將互動式PDF檔案平面化為非互動式PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 使用預設建構函式建立`OutputServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`OutputServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取互動式PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存互動式PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表互動式PDF檔案檔案位置的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。

1. 轉換PDF檔案。

   呼叫`OutputClient`物件的`transformPDF`方法並傳遞下列值，將互動式PDF檔案轉換為非互動式PDF檔案：

   * 包含互動式PDF檔案的`BLOB`物件。
   * `TransformationFormat`列舉值。 若要產生非互動式PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定修訂編號的`PDFARevisionNumber`列舉值。
   * Boolean值，指定是否使用`PDFARevisionNumber`列舉值。 由於此引數適用於PDF/檔案，因此您可以指定`false`。
   * 代表修訂編號和年份的字串值，以冒號分隔。 由於此引數適用於PDF/檔案，因此您可以指定`null`。
   * 代表PDF/A一致性層級的`PDFAConformance`列舉值。
   * 指定是否使用`PDFAConformance`列舉值的布林值。 由於此引數適用於PDF/檔案，因此您可以指定`false`。

   `transformPDF`方法傳回包含非互動式PDF檔案的`BLOB`物件。

1. 將非互動式PDF檔案儲存為PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表非互動式PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存`transformPDF`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
