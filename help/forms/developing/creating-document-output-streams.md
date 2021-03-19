---
title: 建立檔案輸出串流
seo-title: 建立檔案輸出串流
description: 使用「輸出」服務將檔案轉換為PDF（包括PDF/A檔案）、PostScript、印表機控制語言(PCL)和Zebra - ZPL、Intermec - IPL、Datamax - DPL和TecToshiba - TPCL標籤格式。
seo-description: 使用「輸出」服務將檔案轉換為PDF（包括PDF/A檔案）、PostScript、印表機控制語言(PCL)和Zebra - ZPL、Intermec - IPL、Datamax - DPL和TecToshiba - TPCL標籤格式。
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '19045'
ht-degree: 0%

---


# 建立文檔輸出流{#creating-document-output-streams}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

**關於輸出服務**

「輸出」服務可讓您將檔案輸出為PDF（包括PDF/A檔案）、PostScript、印表機控制語言(PCL)，以及下列標籤格式：

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用「輸出」服務，您可以將XML表單資料與表單設計合併，並將檔案輸出至網路印表機或檔案。

有兩種方式可讓您將表單設計（XDP檔案）傳遞至輸出服務。 您可以將包含表單設計的`com.adobe.idp.Document`實例傳遞至Output服務。 或者，您可以傳遞指定表單設計位置的URI值。 在&#x200B;*Programming with forms*&#x200B;中，對這兩種方AEM法進行了討論。

>[!NOTE]
>
>輸出服務不支援包含應用程式物件特定指令碼的Acroform PDF檔案。 不會轉譯包含應用程式物件特定指令碼的Acrobat PDF檔案。

以下各節說明如何使用URI值將表單設計傳遞至輸出服務：

* [建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A檔案](creating-document-output-streams.md#creating-pdf-a-documents)

以下各節說明如何在`com.adobe.idp.Document`實例中傳遞表單設計：

* [將位於Content Services中的檔案（不建議使用）傳送至輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

在決定使用哪種技巧時，一個考慮因素是，如果您要從另一個AEM Forms服務取得表單設計，然後在`com.adobe.idp.Document`實例中傳遞它。 *將檔案傳遞至輸出服務*&#x200B;和&#x200B;*使用片段建立PDF檔案兩節都說明如何從其他AEM Forms服務取得表單設計。*&#x200B;第一個區段會從Content Services擷取表單設計（已過時）。 第二部分從Assembler服務檢索表單設計。

如果從固定位置（如檔案系統）獲取表單設計，則可以使用其中一種技術。 也就是說，可以為XDP檔案指定URI值，或使用`com.adobe.idp.Document`實例。

要在建立PDF文檔時傳遞指定表單設計位置的URI值，請使用`generatePDFOutput`方法。 同樣地，要在建立PDF文檔時將`com.adobe.idp.Document`實例傳遞到Output服務，請使用`generatePDFOutput2`方法。

將輸出流發送到網路打印機時，您也可以使用其中一種技術。 要通過傳遞包含表單設計的`com.adobe.idp.Document`實例將輸出流發送到打印機，請使用`sendToPrinter2`方法。 要通過傳遞URI值向打印機發送輸出流，請使用`sendToPrinter`方法。 *向打印機發送打印流*&#x200B;部分使用`sendToPrinter`方法。

您可以使用輸出服務完成以下任務：

* [建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A檔案](creating-document-output-streams.md#creating-pdf-a-documents)
* [將位於Content Services中的檔案（不建議使用）傳送至輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [列印至檔案](creating-document-output-streams.md#printing-to-files)
* [傳送列印串流至印表機](creating-document-output-streams.md#sending-print-streams-to-printers)
* [建立多個輸出檔案](creating-document-output-streams.md#creating-multiple-output-files)
* [建立搜尋規則](creating-document-output-streams.md#creating-search-rules)
* [平面化PDF檔案](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立PDF檔案{#creating-pdf-documents}

您可以使用「輸出」服務來建立以您提供的表單設計和XML表單資料為基礎的PDF檔案。 由輸出服務建立的PDF檔案不是互動式PDF檔案；用戶不能輸入或修改表單資料。

如果您想要建立適用於長期儲存的PDF檔案，建議您建立PDF/A檔案。 （請參閱[建立PDF/A檔案](creating-document-output-streams.md#creating-pdf-a-documents)）。

若要建立可讓使用者輸入資料的互動式PDF表單，請使用Forms服務。 (請參閱[演算互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)。)

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

要建立PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料來源。
1. 設定PDF執行時期選項。
1. 設定演算執行時期選項。
1. 產生PDF檔案。
1. 檢索操作的結果。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要項)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用Output web service API，請建立`OutputServiceService`物件。

**參考XML資料來源**

若要將資料與表單設計合併，您必須參考包含資料的XML資料來源。 您計畫填入資料的每個表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不符，則會忽略它。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

請考慮以下貸款申請表示例。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

要將資料合併到此表單設計中，必須建立與表單對應的XML資料源。 以下XML代表與範例抵押申請表格對應的XDP XML資料來源。

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

**設定PDF執行時期選項**

在建立PDF文檔時設定檔案URI選項。 此選項指定輸出服務所生成的PDF檔案的名稱和位置。

>[!NOTE]
>
>您不必設定檔案URI執行時期選項，而是可以程式設計方式從Output服務傳回的複雜資料類型擷取PDF檔案。 不過，透過設定檔案URI執行時期選項，您不需要建立以程式設計方式擷取PDF檔案的應用程式邏輯。

**設定渲染運行時選項**

建立PDF檔案時，您可以設定演算執行時期選項。 雖然這些選項不是必要的（與PDF執行時期選項不同），但您可以執行例如改善輸出服務的效能等工作。 例如，您可以快取輸出服務使用的表單設計，以提升其效能。

如果您使用標籤的Acrobat表單作為輸入，則無法使用Output服務Java或web服務API來關閉標籤設定。 如果您嘗試以程式設計方式將此選項設為`false`，則結果PDF檔案仍會加上標籤。

>[!NOTE]
>
>如果您未指定演算執行時期選項，則會使用預設值。 有關渲染運行時選項的資訊，請參見`RenderOptionsSpec`類參考。 (請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**產生PDF檔案**

在您參考包含表單資料的有效XML資料來源並設定執行時期選項後，就可以叫用「輸出」服務，以產生PDF檔案。

當產生PDF檔案時，您會指定「輸出」服務建立PDF檔案所需的URI值。 表單設計可儲存在伺服器檔案系統等位置或作為AEM Forms應用程式的一部分。 使用內容根URI值`repository:///`可以參考作為Forms應用程式一部分存在的表單設計（或其他資源，如影像檔案）。 例如，請考慮以下名為&#x200B;*Loan.xdp*&#x200B;的表單設計，它位於名為&#x200B;*Applications/FormsApplication*&#x200B;的Forms應用程式中：

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

若要存取上圖中所示的Loan.xdp檔案，請指定`repository:///Applications/FormsApplication/1.0/FormsFolder/`作為傳遞至`OutputClient`物件`generatePDFOutput`方法的第三個參數。 指定表單名稱(*Loan.xdp*)作為傳遞至`OutputClient`物件`generatePDFOutput`方法的第二個參數。

如果XDP檔案包含影像（或其他資源，例如片段），請將資源放置在與XDP檔案相同的應用程式資料夾中。 AEM Forms使用內容根URI作為解析影像參照的基本路徑。 例如，如果Loan.xdp檔案包含影像，請確定您將影像置入`Applications/FormsApplication/1.0/FormsFolder/`。

>[!NOTE]
>
>在調用`OutputClient`物件的`generatePDFOutput`或`generatePrintedOutput`方法時，您可以參考Forms應用程式URI。

>[!NOTE]
>
>要查看通過引用位於Forms應用程式中的XDP建立PDF文檔的完整快速入門，請參閱[快速入門（EJB模式）:使用Java API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)根據應用程式XDP檔案建立PDF檔案。

**檢索操作的結果**

輸出服務執行操作後，它返回各種資料項，如指定操作是否成功的狀態XML資料。

**另請參閱**

[使用Java API建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[使用web service API建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API {#create-a-pdf-document-using-the-java-api}建立PDF檔案

使用輸出API(Java)建立PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。

1. 參考XML資料來源。

   * 建立`java.io.FileInputStream`對象，該對象表示XML資料源，該資料源使用其建構子並傳遞一個字串值，該字串值指定XML檔案的位置。
   * 使用其建構子建立`com.adobe.idp.Document`對象。 傳遞`java.io.FileInputStream`物件。

1. 設定PDF執行時期選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`對象。
   * 調用`PDFOutputOptionsSpec`物件的`setFileURI`方法，以設定「檔案URI」選項。 傳遞一個字串值，指定輸出服務所產生PDF檔案的位置。 「檔案URI」選項是相對於代管AEM Forms的J2EE應用程式伺服器，而非用戶端電腦。

1. 設定演算執行時期選項。

   * 使用其建構子建立`RenderOptionsSpec`對象。
   * 快取表單設計，以叫用`RenderOptionsSpec`物件的`setCacheEnabled`並傳遞`true`來改善輸出服務的效能。

   >[!NOTE]
   >
   >如果輸入檔案是Acrobat表單(在Acrobat建立的表單)或已簽署或認證的XFA檔案，則無法使用`RenderOptionsSpec`物件的`setPdfVersion`方法來設定PDF檔案版本。 輸出PDF檔案會保留原始PDF版本。 同樣地，如果輸入檔案是Acrobat表單或已簽署或認證的XFA檔案，則無法透過叫用`RenderOptionsSpec`物件的`setTaggedPDF`方法來設定標籤的Adobe PDF選項。

   >[!NOTE]
   >
   >如果輸入的PDF檔案經過認證或數位簽署，則無法使用`RenderOptionsSpec`物件的`setLinearizedPDF`方法來設定線性化的PDF選項。 （請參閱[數位簽署PDF檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。）*

1. 產生PDF檔案。

   呼叫`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 指定表單設計所在內容根目錄的字串值。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `com.adobe.idp.Document`物件，包含XML資料來源，其中包含要與表單設計合併的資料。

   `generatePDFOutput`方法返回包含操作結果的`OutputResult`對象。

   >[!NOTE]
   >
   >當呼叫`generatePDFOutput`方法產生PDF檔案時，請注意，您無法將資料與已簽署或認證的XFA PDF表單合併。 （請參閱[數位簽署和認證檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。）*

   >[!NOTE]
   >
   >`OutputResult`物件的`getRecordLevelMetaDataList`方法傳回&#x200B;`null`*。*

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput2`方法來建立PDF檔案。 (請參閱[將位於Content Services中的檔案（已過時）傳遞至Output Service ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 檢索操作的結果。

   * 通過調用`OutputResult`對象的`getStatusDoc`方法來檢索表示`generatePDFOutput`操作狀態的`com.adobe.idp.Document`對象。 此方法返回指定操作是否成功的狀態XML資料。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為。xml。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案（請確定您使用`getStatusDoc`方法傳回的`com.adobe.idp.Document`物件）。

   雖然「輸出」服務會將PDF檔案寫入由傳遞至`PDFOutputOptionsSpec`物件`setFileURI`方法的引數所指定的位置，但您仍可以叫用`OutputResult`物件的`getGeneratedDoc`方法，以程式設計方式擷取PDF/A檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#create-a-pdf-document-using-the-web-service-api}建立PDF檔案

使用輸出API(web service)建立PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存將與PDF檔案合併的XML資料。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含表單資料的XML檔案的檔案位置。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 設定PDF執行時期選項

   * 使用其建構子建立`PDFOutputOptionsSpec`對象。
   * 指定字串值來設定「檔案URI」選項，該字串值會指定「輸出」服務產生的PDF檔案在`PDFOutputOptionsSpec`物件的`fileURI`資料成員上的位置。 「檔案URI」選項是相對於代管AEM Forms的J2EE應用程式伺服器，而非用戶端電腦。

1. 設定演算執行時期選項。

   * 使用其建構子建立`RenderOptionsSpec`對象。
   * 快取表單設計，將值`true`指派給`RenderOptionsSpec`物件的`cacheEnabled`資料成員，以改善輸出服務的效能。

   >[!NOTE]
   >
   >如果輸入檔案是Acrobat表單(在Acrobat建立的表單)或已簽署或認證的XFA檔案，則無法使用`RenderOptionsSpec`物件的`setPdfVersion`方法來設定PDF檔案版本。 輸出PDF檔案會保留原始PDF版本。 同樣地，如果輸入檔案是Acrobat表單或已簽署或認證的XFA檔案，則無法透過叫用`RenderOptionsSpec`物件的`setTaggedPDF`*方法來設定標籤的Adobe PDF選項。*

   >[!NOTE]
   >
   >如果輸入的PDF檔案經過認證或數位簽章，則無法使用`RenderOptionsSpec`物件的`linearizedPDF`成員來設定線性化的PDF選項。 （請參閱[數位簽署PDF檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。）*

1. 產生PDF檔案。

   呼叫`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 指定表單設計所在內容根目錄的字串值。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `BLOB`物件，包含XML資料來源，其中包含要與表單設計合併的資料。
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以描述檔案的產生中繼資料填入此物件。 （此參數值僅適用於Web服務調用）。
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。 （此參數值僅適用於Web服務調用）。
   * 包含操作結果的`OutputResult`對象。 （此參數值僅適用於Web服務調用）。

   >[!NOTE]
   >
   >當呼叫`generatePDFOutput`方法產生PDF檔案時，請注意，您無法將資料與已簽署或認證的XFA PDF表單合併。 （請參閱[數位簽署和認證檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。）*

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput2`方法來建立PDF檔案。 (請參閱[將位於Content Services中的檔案（已過時）傳遞至Output Service ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 檢索操作的結果。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為。xml。
   * 建立位元組陣列，儲存由`OutputServiceService`物件的`generatePDFOutput`方法（第8個參數）填入結果資料之`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM` `field`值，以填入位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

   另請參閱

   [步驟摘要](creating-document-output-streams.md#summary-of-steps)

   [使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

   [使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >`OutputServiceService`物件的`generateOutput`方法已過時。

## 建立PDF/A檔案{#creating-pdf-a-documents}

您可以使用「輸出」服務來建立PDF/A檔案。 由於PDF/A是長期保存檔案內容的封存格式，所以所有字型都已內嵌，檔案也未壓縮。 因此，PDF/A檔案通常比標準PDF檔案大。 此外，PDF/A檔案不包含音訊和視訊內容。 如同其他「輸出」服務工作，您提供表單設計和資料，以便與表單設計合併以建立PDF/A檔案。

PDF/A-1規格包含兩個符合等級，即a和b。兩者之間的主要區別在於邏輯結構（可訪問性）支援，而邏輯結構（可訪問性）支援對於符合性級別b不是必需的。無論符合程度如何，PDF/A-1都規定所有字型都內嵌在產生的PDF/A檔案中。

雖然PDF/A是封存PDF檔案的標準，但是如果標準PDF檔案符合您公司的需求，就不必使用PDF/A進行封存。 PDF/A標準的目的，在於建立可長期儲存的PDF檔案，並符合檔案保存要求。 例如，URL無法內嵌在PDF/A中，因為URL可能會隨著時間變成無效。

您的組織必須評估自己的需求、您希望保存文檔的時間長度、檔案大小考慮因素，並確定自己的歸檔策略。 您可以使用DocConverter服務，以程式設計方式判斷PDF檔案是否符合PDF/A規範。 （請參閱[程式設計決定PDF/A相容性](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)）。

PDF/A檔案必須使用在表單設計中指定的字型，且字型無法取代。 因此，如果位於PDF檔案中的字型無法在主機作業系統(OS)上使用，則會發生例外情況。

當PDF/A檔案在Acrobat開啟時，會顯示一則訊息，確認檔案為PDF/A檔案，如下圖所示。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM網站有PDF/A常見問答區段，您可從[https://www.aiim.org/documents/standards/19005-1_FAQ.pdf](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf)存取。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}摘要

要建立PDF/A文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料來源。
1. 設定PDF/A執行時期選項。
1. 設定演算執行時期選項。
1. 產生PDF/A檔案。
1. 檢索操作的結果。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立自定義應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要項)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用Output web service API，請建立`OutputServiceService`物件。

**參考XML資料來源**

若要將資料與表單設計合併，您必須參考包含資料的XML資料來源。 每個要填入資料的表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不符，則會忽略它。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

**設定PDF/A執行時期選項**

在建立PDF/A文檔時，可以設定「檔案URI」選項。 URI是相對於代管AEM Forms的J2EE應用程式伺服器。 也就是說，如果設定C:\Adobe，則檔案將寫入到伺服器上的資料夾，而不是客戶端電腦。 URI指定輸出服務所生成的PDF/A檔案的名稱和位置。

**設定渲染運行時選項**

您可以在建立PDF/A檔案時設定演算執行時期選項。 您可以設定的兩個PDF/A相關選項是`PDFAConformance`和`PDFARevisionNumber`值。 `PDFAConformance`值是指PDF檔案如何符合指定長期電子檔案保留的要求。 此選項的有效值為`A`和`B`。 有關a級和b級符合性的資訊，請參閱標題為&#x200B;*ISO 19005-1檔案管理*&#x200B;的PDF/A-1 ISO規格。

`PDFARevisionNumber`值是指PDF/A檔案的修訂號。 有關PDF/A文檔修訂號的資訊，請參閱標題為&#x200B;*ISO 19005-1文檔管理*&#x200B;的PDF/A-1 ISO規範。

>[!NOTE]
>
>建立PDF/A 1A文檔時，不能將標籤的Adobe PDF選項設定為`false`。 PDF/A 1A永遠是標籤的PDF檔案。 此外，在建立PDF/A 1B文檔時，不能將標籤的Adobe PDF選項設定為`true`。 PDF/A 1B永遠是未標籤的PDF檔案。

**產生PDF/A檔案**

參考包含表單資料的有效XML資料來源並設定執行時期選項後，您可以叫用「輸出」服務，使其產生PDF/A檔案。

**檢索操作的結果**

輸出服務執行操作後，它返回各種資料項，如指定操作是否成功的XML資料。

**另請參閱**

[使用Java API建立PDF/A檔案](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[使用web service API建立PDF/A檔案](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API {#create-a-pdf-a-document-using-the-java-api}建立PDF/A檔案

使用輸出API(Java)建立PDF/A檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。

1. 參考XML資料來源。

   * 建立`java.io.FileInputStream`對象，該對象表示XML資料源，該資料源使用其建構子並傳遞指定XML檔案位置的字串值來填充PDF/A文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定PDF/A執行時期選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`對象。
   * 調用`PDFOutputOptionsSpec`物件的`setFileURI`方法，以設定「檔案URI」選項。 傳遞一個字串值，指定輸出服務所產生PDF檔案的位置。 「檔案URI」選項是相對於代管AEM Forms的J2EE應用程式伺服器，而非用戶端電腦。

1. 設定演算執行時期選項。

   * 使用其建構子建立`RenderOptionsSpec`對象。
   * 通過調用`RenderOptionsSpec`對象的`setPDFAConformance`方法並傳遞指定一致性級別的`PDFAConformance`枚舉值來設定`PDFAConformance`值。 例如，要指定符合性級別A，請傳遞`PDFAConformance.A`。
   * 調用`RenderOptionsSpec`物件的`setPDFARevisionNumber`方法並傳遞`PDFARevisionNumber.Revision_1`，以設定`PDFARevisionNumber`值。

   >[!NOTE]
   >
   >PDF/A檔案的PDF版本為1.4，不論您為`RenderOptionsSpec`物件的&#x200B;`setPdfVersion`*方法指定哪個值。*

1. 產生PDF/A檔案。

   叫用`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF/A檔案：

   * `TransformationFormat`枚舉值。 若要產生PDF/A檔案，請指定`TransformationFormat.PDFA`。
   * 指定表單設計名稱的字串值。
   * 指定表單設計所在內容根目錄的字串值。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * 包含XML資料來源的`com.adobe.idp.Document`物件，其中包含要與表單設計合併的資料。

   `generatePDFOutput`方法返回包含操作結果的`OutputResult`對象。

   >[!NOTE]
   >
   >`OutputResult`物件的`getRecordLevelMetaDataList`方法會傳回`null`。

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput`2方法，以建立PDF/A檔案。 (請參閱[將位於Content Services中的檔案（已過時）傳遞至Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 檢索操作的結果。

   * 通過調用`OutputResult`對象的`getStatusDoc`方法，建立表示`generatePDFOutput`方法狀態的`com.adobe.idp.Document`對象。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為。xml。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案（請確定您使用`getStatusDoc`方法傳回的`com.adobe.idp.Document`物件）。

   >[!NOTE]
   >
   >雖然「輸出」服務會將PDF/A檔案寫入至傳遞至`PDFOutputOptionsSpec`物件`setFileURI`方法之引數所指定的位置，但您仍可以呼叫`OutputResult`物件的`getGeneratedDoc`方法，以程式設計方式擷取PDF/A檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API建立PDF/A檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用web service API {#create-a-pdf-a-document-using-the-web-service-api}建立PDF/A檔案

使用輸出API(web service)建立PDF/A檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存將與PDF/A檔案合併的資料。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列內容來填充`BLOB`對象。

1. 設定PDF/A執行時期選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`對象。
   * 指定字串值來設定「檔案URI」選項，該字串值會指定「輸出」服務產生的PDF檔案在`PDFOutputOptionsSpec`物件的`fileURI`資料成員上的位置。 「檔案URI」選項是相對於代管AEM Forms的J2EE應用程式伺服器，而非用戶端電腦

1. 設定演算執行時期選項。

   * 使用其建構子建立`RenderOptionsSpec`對象。
   * 將`PDFAConformance`列舉值指派給`RenderOptionsSpec`物件的`PDFAConformance`資料成員，以設定`PDFAConformance`值。 例如，要指定符合性級別A，請為此資料成員分配`PDFAConformance.A`。
   * 將`PDFARevisionNumber`列舉值指派給`RenderOptionsSpec`物件的`PDFARevisionNumber`資料成員，以設定`PDFARevisionNumber`值。 將`PDFARevisionNumber.Revision_1`分配給此資料成員。

   >[!NOTE]
   >
   >PDF/A檔案的PDF版本為1.4，不論您指定的值為何。

1. 產生PDF/A檔案。

   呼叫`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * TransformationFormat枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDFA`。
   * 指定表單設計名稱的字串值。
   * 指定表單設計所在內容根目錄的字串值。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `BLOB`物件，包含XML資料來源，其中包含要與表單設計合併的資料。
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以描述檔案的產生中繼資料填入此物件。 （此參數值僅適用於Web服務調用。）
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。 （此參數值僅適用於Web服務調用。）
   * 包含操作結果的`OutputResult`對象。 （此參數值僅適用於Web服務調用。）

   >[!NOTE]
   >
   >您也可以叫用`OutputClient`物件的`generatePDFOutput`2方法，以建立PDF/A檔案。 (請參閱[將位於Content Services中的檔案（已過時）傳遞至Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 檢索操作的結果。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為。xml。
   * 建立位元組陣列，儲存由`OutputServiceService`物件的`generatePDFOutput`方法（第8個參數）填入結果資料之`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將位於Content Services中的檔案（已過時）傳遞至Output Service {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

「輸出」服務會轉譯非互動式PDF表單，該表單以通常儲存為XDP檔案並在Designer中建立的表單設計為基礎。 您可以將包含表單設計的`com.adobe.idp.Document`物件傳遞至Output服務。 然後，輸出服務將呈現位於`com.adobe.idp.Document`對象中的表單設計。

將`com.adobe.idp.Document`對象傳遞到輸出服務的一個好處是，其他AEM Forms服務操作返回`com.adobe.idp.Document`實例。 也就是說，您可以從其他服務操作中獲取一個`com.adobe.idp.Document`實例並進行渲染。 例如，假設XDP檔案儲存在名為`/Company Home/Form Designs`的Content Services（已過時）節點中，如下圖所示。

您可以以程式設計方式從Content Services（不建議使用）擷取Loan.xdp，並將XDP檔案傳遞至`com.adobe.idp.Document`物件內的Output服務。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-2}摘要

要將從Content Services（不建議使用）獲取的文檔傳遞到Output服務，請執行以下任務：

1. 包含專案檔案。
1. 建立輸出和檔案管理用戶端API物件。
1. 從Content Services擷取表單設計（已過時）。
1. 轉換非互動式PDF表單。
1. 對資料流執行動作。

**包含專案檔案**

將必要的檔案加入您的開發專案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立輸出和文檔管理客戶端API對象**

在以程式設計方式執行輸出服務API操作之前，請先建立輸出用戶端API物件。 此外，由於此工作流程會從Content Services擷取XDP檔案（已停用），因此請建立Document Management API物件。

**從Content Services擷取表單設計（已過時）**

使用Java或web service API從Content Services（已過時）擷取XDP檔案。 在`com.adobe.idp.Document`實例（或在使用web services時為`BLOB`實例）中返回XDP檔案。 然後，可以將`com.adobe.idp.Document`實例傳遞到Output服務。

**轉換非互動式PDF表單**

若要轉換非互動式表單，請將從Content Services（不建議使用）傳回的`com.adobe.idp.Document`例項傳遞至Output服務。

>[!NOTE]
>
>名為`generatePDFOutput2`和g `eneratePrintedOutput2`的兩種新方法接受包含表單設計的`com.adobe.idp.Document`物件。 在將打印流發送到網路打印機時，還可以將包含表單設計的`com.adobe.idp.Document`傳遞到Output服務。

**使用表單資料流執行動作**

您可以將非互動式表單儲存為PDF檔案。 您可在Adobe Reader或Acrobat檢視表格。

**另請參閱**

[使用Java API將檔案傳送至輸出服務](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[使用web service API將檔案傳遞至Output Service](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### 使用Java API {#pass-documents-to-the-output-service-using-the-java-api}將檔案傳遞至輸出服務

使用輸出服務和內容服務（已過時）API(Java)傳遞從Content Services（已過時）擷取的檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立「輸出」和「檔案管理用戶端API」物件。

   * 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`DocumentManagementServiceClientImpl`對象。

1. 從Content Services擷取表單設計（已過時）。

   叫用`DocumentManagementServiceClientImpl`物件的`retrieveContent`方法並傳遞下列值：

   * 一個字串值，它指定添加內容的儲存。 預設商店為`SpacesStore`。 此值為必要參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值為必要參數。
   * 指定版本的字串值。 此值為可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。

   `retrieveContent`方法返回包含XDP檔案的`CRCResult`對象。 調用`CRCResult`物件的`getDocument`方法，擷取`com.adobe.idp.Document`例項。

1. 轉換非互動式PDF表單。

   叫用`OutputClient`物件的`generatePDFOutput2`方法並傳遞下列值：

   * `TransformationFormat`枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 一個字串值，它指定附加資源（如影像）所在的內容根目錄。
   * 代表表單設計的`com.adobe.idp.Document`物件（使用`CRCResult`物件的`getDocument`方法傳回的例項）。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `com.adobe.idp.Document`物件，包含XML資料來源，其中包含要與表單設計合併的資料。

   `generatePDFOutput2`方法返回包含操作結果的`OutputResult`對象。

1. 對表單資料流執行動作。

   * 調用`OutputResult`物件的`getGeneratedDoc`方法，擷取代表非互動式表單的`com.adobe.idp.Document`物件。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為。pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案（請確定您使用`getGeneratedDoc`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API將檔案傳送至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[快速入門（SOAP模式）:使用Java API將檔案傳送至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#pass-documents-to-the-output-service-using-the-web-service-api}將檔案傳遞至Output Service

使用輸出服務和內容服務（已過時）API(web service)傳遞從Content Services（已過時）檢索的文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 由於此客戶端應用程式調用兩個AEM Forms服務，因此建立兩個服務引用。 對與「輸出」服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   對與「文檔管理」服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   由於`BLOB`資料類型對於兩個服務引用都很常見，因此使用`BLOB`資料類型時可完全限定資料類型。 在相應的Web服務快速啟動中，所有`BLOB`實例都完全限定。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立「輸出」和「檔案管理用戶端API」物件。

   * 使用其預設建構子建立`OutputServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對`DocumentManagementServiceClient`服務客戶端重複這些步驟。

1. 從Content Services擷取表單設計（已過時）。

   叫用`DocumentManagementServiceClient`物件的`retrieveContent`方法並傳遞下列值，以擷取內容：

   * 一個字串值，它指定添加內容的儲存。 預設商店為`SpacesStore`。 此值為必要參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值為必要參數。
   * 指定版本的字串值。 此值為可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。
   * 儲存瀏覽連結值的字串輸出參數。
   * 儲存內容的`BLOB`輸出參數。 您可以使用此輸出參數來擷取內容。
   * 儲存內容屬性的`ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType`輸出參數。
   * `CRCResult`輸出參數。 您可以使用`BLOB`輸出參數來擷取內容，而不是使用此物件。

1. 轉換非互動式PDF表單。

   叫用`OutputServiceClient`物件的`generatePDFOutput2`方法並傳遞下列值：

   * `TransformationFormat`枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 一個字串值，它指定附加資源（如影像）所在的內容根目錄。
   * 代表表單設計的`BLOB`物件(使用Content Services傳回的`BLOB`例項（已過時）)。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `BLOB`物件，包含XML資料來源，其中包含要與表單設計合併的資料。
   * 由`generatePDFOutput2`方法填充的輸出`BLOB`對象。 `generatePDFOutput2`方法會以描述檔案的產生中繼資料填入此物件。 （此參數值僅適用於Web服務調用）。
   * 包含操作結果的輸出`OutputResult`對象。 （此參數值僅適用於Web服務調用）。

   `generatePDFOutput2`方法會傳回包含非互動式PDF表單的`BLOB`物件。

1. 對表單資料流執行動作。

   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表互動式PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存從`generatePDFOutput2`方法檢索到的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 將儲存庫中的文檔傳遞到輸出服務{#passing-documents-located-in-the-repository-to-the-output-service}

「輸出」服務會轉譯非互動式PDF表單，該表單以通常儲存為XDP檔案並在Designer中建立的表單設計為基礎。 您可以將包含表單設計的`com.adobe.idp.Document`物件傳遞至Output服務。 然後，輸出服務將呈現位於`com.adobe.idp.Document`對象中的表單設計。

將`com.adobe.idp.Document`對象傳遞到輸出服務的一個好處是，其他AEM Forms服務操作返回`com.adobe.idp.Document`實例。 也就是說，您可以從其他服務操作中獲取一個`com.adobe.idp.Document`實例並進行渲染。 例如，假設XDP檔案儲存在AEM Forms儲存庫中，如下圖所示。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

*FormsFolder*&#x200B;資料夾是AEM Forms儲存庫中用戶定義的位置（此位置是示例，預設情況下不存在）。 在此示例中，名為Loan.xdp的表單設計位於此資料夾中。 除了表單設計外，其他表單文宣（例如影像）也可以儲存在此位置。 位於AEM Forms儲存庫中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

您可以通過寫程式方式從AEM Forms儲存庫中檢索Loan.xdp，並將其傳遞到`com.adobe.idp.Document`對象內的Output服務。

您可以使用兩種方式之一，根據位於儲存庫中的XDP檔案建立PDF。 您可以通過引用傳遞XDP位置，也可以通過寫程式方式從儲存庫中檢索XDP並將其傳遞到XDP檔案中的Output服務。

[快速啟動（EJB模式）:使用Java API根據應用程式XDP檔案建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （顯示如何參考傳遞XDP檔案的位置）。

[快速啟動（EJB模式）:使用Java API將位於AEM Forms資料檔案庫中的文檔傳遞到輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (說明如何以寫程式方式從AEM Forms資料檔案庫中檢索XDP檔案並將其傳遞到實例中的輸出 `com.adobe.idp.Document` 服務)。（本節討論如何執行此任務）

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-3}摘要

要將從AEM Forms儲存庫獲取的文檔傳遞到輸出服務，請執行以下任務：

1. 包含專案檔案。
1. 建立輸出和檔案管理用戶端API物件。
1. 從AEM Forms儲存庫檢索表單設計。
1. 轉換非互動式PDF表單。
1. 對資料流執行動作。

**包含專案檔案**

將必要的檔案加入您的開發專案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立輸出和文檔管理客戶端API對象**

在以程式設計方式執行輸出服務API操作之前，請先建立輸出用戶端API物件。 此外，由於此工作流程會從Content Services擷取XDP檔案（已停用），因此請建立Document Management API物件。

**從AEM Forms儲存庫檢索表單設計**

使用儲存庫API從AEM Forms儲存庫檢索XDP檔案。 （請參閱[閱讀資源](/help/forms/developing/aem-forms-repository.md#reading-resources)。）

在`com.adobe.idp.Document`實例（或在使用web services時為`BLOB`實例）中返回XDP檔案。 然後，可以將`com.adobe.idp.Document`實例傳遞到Output服務。

**轉換非互動式PDF表單**

要呈現非互動式表單，請傳遞使用AEM Forms資料庫API傳回的`com.adobe.idp.Document`實例。

>[!NOTE]
>
>名為`generatePDFOutput2`和`generatePrintedOutput2`的兩種新方法接受包含表單設計的`com.adobe.idp.Document`物件。 在將打印流發送到網路打印機時，還可以將包含表單設計的`com.adobe.idp.Document`傳遞到Output服務。

**使用表單資料流執行動作**

您可以將非互動式表單儲存為PDF檔案。 您可在Adobe Reader或Acrobat檢視表格。

**另請參閱**

[使用Java API將儲存庫中的文檔傳遞到輸出服務](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### 使用Java API {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}將儲存庫中的文檔傳遞到輸出服務

使用輸出服務和儲存庫API(Java)傳遞從儲存庫檢索到的文檔：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar和adobe-repository-client.jar。

1. 建立「輸出」和「檔案管理用戶端API」物件。

   * 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`DocumentManagementServiceClientImpl`對象。

1. 從「AEM Forms儲存庫」檢索表單設計。

   叫用`ResourceRepositoryClient`物件的`readResourceContent`方法，並將指定URI位置的字串值傳遞至XDP檔案。 例如，`/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。 此值為必填值。 此方法傳回代表XDP檔案的`com.adobe.idp.Document`例項。

1. 轉換非互動式PDF表單。

   叫用`OutputClient`物件的`generatePDFOutput2`方法並傳遞下列值：

   * `TransformationFormat`枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 一個字串值，它指定附加資源（如影像）所在的內容根目錄。 例如，`repository:///Applications/FormsApplication/1.0/FormsFolder/`。
   * 代表表單設計的`com.adobe.idp.Document`物件（使用`ResourceRepositoryClient`物件的`readResourceContent`方法傳回的例項）。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `com.adobe.idp.Document`物件，包含XML資料來源，其中包含要與表單設計合併的資料。

   `generatePDFOutput2`方法返回包含操作結果的`OutputResult`對象。

1. 對表單資料流執行動作。

   * 調用`OutputResult`物件的`getGeneratedDoc`方法，擷取代表非互動式表單的`com.adobe.idp.Document`物件。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為。pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案（請確定您使用`getGeneratedDoc`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API將位於AEM Forms儲存庫中的文檔傳遞到輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用片段{#creating-pdf-documents-using-fragments}建立PDF檔案

您可以使用「輸出」和「匯編器」服務來建立基於片段的輸出流，如PDF文檔。 Assembler服務會根據位於多個XDP檔案中的片段來組合XDP檔案。 組合的XDP檔案會傳遞至Output服務，此服務會建立PDF檔案。 雖然此工作流程顯示正在生成的PDF文檔，但「輸出」服務可以為此工作流生成其他輸出類型，如ZPL。 PDF檔案僅用於討論用途。

下圖顯示此工作流程。

![cp_cp_outputsemble片段](assets/cp_cp_outputassemblefragments.png)

在閱讀「使用片段建立PDF檔案」*之前，建議您熟悉使用Assembler服務來組合多份XDP檔案。*（請參閱[組合多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)）。

>[!NOTE]
>
>您也可以將由Assembler服務組合的表單設計傳遞給Forms服務，而不是輸出服務。 輸出服務與Forms服務的主要區別在於，Forms服務會產生互動式PDF檔案，而輸出服務則會產生非互動式PDF檔案。 此外，Forms服務無法生成基於打印機的輸出流，如ZPL。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-4}摘要

若要根據片段建立PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Output和Assembler客戶端對象。
1. 使用Assembler服務生成表單設計。
1. 使用「輸出」服務來產生PDF檔案。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立輸出和匯編客戶端對象**

在以程式設計方式執行輸出服務API操作之前，請先建立輸出用戶端API物件。 此外，由於此工作流調用Assembler服務來建立表單設計，因此建立Assembler Client API對象。

**使用Assembler服務生成表單設計**

使用Assembler服務使用片段來產生表單設計。 Assembler服務返回包含表單設計的`com.adobe.idp.Document`實例。

**使用「輸出」服務來產生PDF檔案**

您可以使用「輸出」服務，使用Assembler服務建立的表單設計生成PDF文檔。 將Assembler服務返回的`com.adobe.idp.Document`實例傳遞到Output服務。

**將PDF檔案儲存為PDF檔案**

在「輸出」服務產生PDF檔案後，您可將它儲存為PDF檔案。

**另請參閱**

[使用Java API根據片段建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[使用web service API，根據片段建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[組合多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents)

### 使用Java API {#create-a-pdf-document-based-on-fragments-using-the-java-api}根據片段建立PDF檔案

使用Output Service API和Assembler Service API(Java)，根據片段建立PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立Output和Assembler客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 使用Assembler服務生成表單設計。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列必要值：

   * `com.adobe.idp.Document`物件，代表要使用的DDX檔案。
   * 包含輸入XDP檔案的`java.util.Map`對象。
   * 一個`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別。

   `invokeDDX`方法返回包含已裝配的XDP文檔的`com.adobe.livecycle.assembler.client.AssemblerResult`對象。 要檢索已裝配的XDP文檔，請執行以下操作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 此方法返回`java.util.Map`對象。
   * 重複`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，擷取已組合的XDP檔案。


1. 使用「輸出」服務來產生PDF檔案。

   叫用`OutputClient`物件的`generatePDFOutput2`方法並傳遞下列值：

   * `TransformationFormat`枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`
   * 一個字串值，它指定附加資源（如影像）所在的內容根目錄
   * 代表表單設計的`com.adobe.idp.Document`對象（使用Assembler服務返回的實例）
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件
   * 包含演算執行時期選項的`RenderOptionsSpec`物件
   * 包含XML資料來源的`com.adobe.idp.Document`物件，其中包含要與表單設計合併的資料

   `generatePDFOutput2`方法返回包含操作結果的`OutputResult`對象

1. 將PDF檔案儲存為PDF檔案。

   * 叫用`OutputResult`物件的`getGeneratedDoc`方法，擷取代表PDF檔案的`com.adobe.idp.Document`物件。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為。pdf。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案。 （請確定您使用`getGeneratedDoc`方法傳回的`com.adobe.idp.Document`物件。）

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API根據片段建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[快速入門（SOAP模式）:使用Java API根據片段建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用web service API {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}根據片段建立PDF檔案

使用Output Service API和Assembler Service API(web service)，以片段為基礎建立PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 對與「輸出」服務關聯的服務引用使用以下WSDL定義：

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   對與Assembler服務關聯的服務引用使用以下WSDL定義：

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   由於`BLOB`資料類型對於兩個服務引用都很常見，因此使用`BLOB`資料類型時可完全限定資料類型。 在相應的Web服務快速啟動中，所有`BLOB`實例都完全限定。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立Output和Assembler客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給`OutputServiceClient.ClientCredentials.UserName.UserName`欄位。
      * 為`OutputServiceClient.ClientCredentials.UserName.Password`欄位分配相應的口令值。
      * 將常數值`HttpClientCredentialType.Basic`分配給`BasicHttpBindingSecurity.Transport.ClientCredentialType`欄位。
   * 將`BasicHttpSecurityMode.TransportCredentialOnly`常數值指派給`BasicHttpBindingSecurity.Security.Mode`欄位。

   >[!NOTE]
   >
   >對`AssemblerServiceClient`對象重複這些步驟。

1. 使用Assembler服務生成表單設計。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象
   * 包含所需檔案的`MyMapOf_xsd_string_To_xsd_anyType`對象
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何例外。 要獲取新建立的XDP文檔，請執行以下操作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是`Map`物件，包含產生的PDF檔案。
   * 重複`Map`物件，以擷取已組合的表單設計。 將該陣列成員的`value`轉換為`BLOB`。 將此`BLOB`實例傳遞到Output服務。


1. 使用「輸出」服務來產生PDF檔案。

   叫用`OutputServiceClient`物件的`generatePDFOutput2`方法並傳遞下列值：

   * `TransformationFormat`枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 一個字串值，它指定附加資源（如影像）所在的內容根目錄。
   * 代表表單設計的`BLOB`對象（使用Assembler服務返回的`BLOB`實例）。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `BLOB`物件，包含XML資料來源，其中包含要與表單設計合併的資料。
   * `generatePDFOutput2`方法所填充的輸出`BLOB`對象。 `generatePDFOutput2`方法會以描述檔案的產生中繼資料填入此物件。 （此參數值僅適用於Web服務調用）。
   * 包含操作結果的輸出`OutputResult`對象。 （此參數值僅適用於Web服務調用）。

   `generatePDFOutput2`方法會傳回包含非互動式PDF表單的`BLOB`物件。

1. 將PDF檔案儲存為PDF檔案。

   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表互動式PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存從`generatePDFOutput2`方法檢索到的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 打印到檔案{#printing-to-files}

您可以使用「輸出」服務將PostScript、打印機控制語言(PCL)或以下標籤格式等流打印到檔案：

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用「輸出」服務，您可以將XML資料與表單設計合併，並將表單列印至檔案。 下圖顯示了建立雷射和標籤檔案的輸出服務。

>[!NOTE]
>
>有關向打印機發送打印流的資訊，請參閱[向打印機發送打印流](creating-document-output-streams.md#sending-print-streams-to-printers)。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-5}摘要

要打印到檔案，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料來源。
1. 設定列印至檔案所需的列印執行時間選項。
1. 將列印串流列印至檔案。
1. 檢索操作的結果。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。 (請參閱[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用Output web service API，請建立`OutputServiceService`物件。

**參考XML資料來源**

要打印包含資料的文檔，您必須為要填入資料的每個表單欄位引用包含XML元素的XML資料源。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不符，則會忽略它。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

**將打印所需的打印運行時選項設定為檔案**

要打印到檔案，必須通過指定輸出服務打印到的檔案的位置和名稱來設定檔案URI運行時選項。 例如，若要指示「輸出」服務將名為&#x200B;*MortgageForm.ps*&#x200B;的PostScript檔案列印為C:\Adobe，請指定C:\Adobe\MortgageForm.ps。

>[!NOTE]
>
>您可以定義選用的執行時期選項。 有關可設定的所有選項的資訊，請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`PrintedOutputOptionsSpec`類參考。

**將列印串流列印至檔案**

在參考包含表單資料的有效XML資料來源並設定列印執行時期選項後，您就可以叫用「輸出」服務，讓它列印檔案。

**檢索操作的結果**

在Output服務執行操作後，它會返回各種資料項，如XML資料，以指定操作是否成功。

**另請參閱**

[使用Java API列印至檔案](creating-document-output-streams.md#print-to-files-using-the-java-api)

[使用web service API列印至檔案](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API {#print-to-files-using-the-java-api}列印至檔案

使用輸出API(Java)列印至檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。

1. 參考XML資料來源。

   * 建立`java.io.FileInputStream`對象，該對象表示XML資料源，該資料源使用其建構子並傳遞指定XML檔案位置的字串值來填充文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定列印至檔案所需的列印執行時間選項。

   * 使用其建構子建立`PrintedOutputOptionsSpec`對象。
   * 調用PrintedOutputOptionsSpec對象的`setFileURI`方法並傳遞代表檔案名稱和位置的字串值，以指定檔案。 例如，如果您想要將「輸出」服務列印為位於C:\Adobe的名為MortgageForm.ps的PostScript檔案，請指定C:\\Adobe\MortgageForm.ps。
   * 調用`PrintedOutputOptionsSpec`物件的`setCopies`方法並傳遞代表份數的整數值，以指定要列印的份數。

1. 將列印串流列印至檔案。

   調用`OutputClient`物件的`generatePrintedOutput`方法並傳遞下列值，以列印至檔案：

   * `PrintFormat`列舉值，指定要建立的列印串流格式。 例如，若要建立PostScript列印串流，請傳遞`PrintFormat.PostScript`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定相關輔助檔案（如影像檔案）的位置。
   * 一個字串值，它指定要使用的XDC檔案的位置（如果指定了要使用`PrintedOutputOptionsSpec`對象的XDC檔案，則可以傳遞`null`）。
   * `PrintedOutputOptionsSpec`物件，包含列印至檔案所需的執行時期選項。
   * 包含表單資料的XML資料源的`com.adobe.idp.Document`對象。

   `generatePrintedOutput`方法返回包含操作結果的`OutputResult`對象。

   >[!NOTE]
   >
   >`OutputResult`物件的`getRecordLevelMetaDataList`方法會傳回`null`。

1. 檢索操作的結果。

   * 通過調用`OutputResult`對象的`getStatusDoc`方法（`generatePrintedOutput`方法返回`OutputResult`對象），建立表示`generatePrintedOutput`方法狀態的`com.adobe.idp.Document`對象。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為XML。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案（請確定您使用`getStatusDoc`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API列印至檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用web service API {#print-to-files-using-the-web-service-api}列印至檔案

使用輸出API(web service)列印至檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存表單資料。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值指定包含表單資料的XML檔案的位置。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`binaryData`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 設定列印至檔案所需的列印執行時間選項。

   * 使用其建構子建立`PrintedOutputOptionsSpec`對象。
   * 指定檔案的方式為：將代表檔案位置和名稱的字串值指派給`PrintedOutputOptionsSpec`物件的`fileURI`資料成員。 例如，如果您希望輸出服務列印至位於C:\Adobe的名為&#x200B;*MortgageForm.ps*&#x200B;的PostScript檔案，請指定C:\\Adobe\MortgageForm.ps。
   * 通過為`PrintedOutputOptionsSpec`對象的`copies`資料成員指定表示副本數的整數值，指定要打印的副本數。

1. 將列印串流列印至檔案。

   調用`OutputServiceService`物件的`generatePrintedOutput`方法並傳遞下列值，以列印至檔案：

   * `PrintFormat`列舉值，指定要建立的列印串流格式。 例如，若要建立PostScript列印串流，請傳遞`PrintFormat.PostScript`。
   * 指定表單設計名稱的字串值。
   * 一個字串值，它指定相關輔助檔案（如影像檔案）的位置。
   * 一個字串值，它指定要使用的XDC檔案的位置（如果指定了要使用`PrintedOutputOptionsSpec`對象的XDC檔案，則可以傳遞`null`）。
   * `PrintedOutputOptionsSpec`物件，包含列印至檔案所需的列印執行時間選項。
   * 包含表單資料的XML資料源的`BLOB`對象。
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以描述檔案的產生中繼資料填入此物件。 （此參數值僅適用於Web服務調用。）
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。 （此參數值僅適用於Web服務調用。）
   * 包含操作結果的`OutputResult`對象。 （此參數值僅適用於Web服務調用。）

1. 檢索操作的結果。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為XML。
   * 建立位元組陣列，儲存由`OutputServiceService`物件的`generatePDFOutput`方法（第8個參數）填入結果資料之`BLOB`物件的資料內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 向打印機發送打印流{#sending-print-streams-to-printers}

您可以使用「輸出」服務將打印流(如PostScript、打印機控制語言(PCL)或以下標籤格式)發送到網路打印機：

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用「輸出」服務，您可以將XML資料與表單設計合併，並將表單輸出為列印串流。 例如，您可以建立PostScript列印串流，並將它傳送至網路印表機。 下圖顯示Output服務將打印流發送到網路打印機。

>[!NOTE]
>
>為了演示如何向網路打印機發送打印流，本節使用SharedPrinter打印機協定向網路打印機發送PostScript打印流。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-6}摘要

要向網路打印機發送打印流，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料來源。
1. 設定列印執行時期選項
1. 擷取要列印的檔案。
1. 將文檔發送到網路打印機。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要項)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，請建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用Output web service API，請建立`OutputServiceClient`物件。

**參考XML資料來源**

要打印包含資料的文檔，您必須為要填入資料的每個表單欄位引用包含XML元素的XML資料源。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不符，則會忽略它。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

**設定列印執行時期選項**

將打印流發送到打印機時，可以設定運行時選項，包括以下選項：

* **副本**:指定要發送到打印機的副本數。預設值為 1。
* **訂書**:當使用訂書機時，設定XCI選項。此選項可在配置模型中由Staple元素指定，僅用於PS和PCL打印機。
* **OutputJog**:當輸出頁面應進行慢動作（在輸出托盤中實際移動）時，會設定XCI選項。此選項僅適用於PS和PCL打印機。
* **OutputBin**:用於使打印驅動程式選擇適當輸出站的XCI值。

>[!NOTE]
>
>有關可設定的所有運行時選項的資訊，請參見`PrintedOutputOptionsSpec`類參考。

**擷取要列印的檔案**

擷取要傳送至印表機的列印串流。 例如，您可以擷取PostScript檔案並將它傳送至印表機。

如果您的印表機支援PDF，您可以選擇傳送PDF檔案。 但是，將PDF檔案傳送至印表機的問題是，每家印表機製造商都有不同的PDF解譯器實作。 就是說，有些印刷廠是用Adobe PDF詮釋的，但是它要靠印刷。 其他印表機則有其專屬的PDF解譯器。 因此，列印結果可能會有所不同。

傳送PDF檔案至印表機的另一個限制是，它只會列印；它無法訪問雙面打印器、紙盒選擇和裝訂，除非通過打印機上的設定。

要檢索要打印的文檔，請使用`generatePrintedOutput`方法。 下表指定使用`generatePrintedOutput`方法時為指定打印流設定的內容類型。

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
   <td><p>依預設建立dpl203.xdc或自訂xdc輸出串流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>建立DPL 300 DPI輸出串流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>建立DPL 400 DPI輸出串流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>建立DPL 600 DPI輸出串流。</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>建立通用顏色PCL(5c)輸出流。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>建立一般PostScript Level 3輸出串流。</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>建立自訂IPL輸出串流。</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>建立IPL 300 DPI輸出串流。</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>建立IPL 400 DPI輸出串流。</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>建立通用單色PCL(5e)輸出流。</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>建立一般PostScript Level 2輸出串流。</p></td>
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
>您也可以使用`generatePrintedOutput2`方法，將打印流發送到打印機。 但是，與「向打印機發送打印流」部分關聯的快速啟動使用`generatePrintedOutput`方法。

**將打印流發送到網路打印機**

擷取要列印的檔案後，您可以叫用「輸出」服務，以便傳送列印串流至網路印表機。 要使「輸出」服務成功找到打印機，必須同時指定打印伺服器和打印機名稱。 此外，您還必須指定打印協定。

>[!NOTE]
>
>如果PDFG已安裝在forms伺服器上，且伺服器在Windows Server 2008上執行，則無法使用SharedPrinter屬性。 在這種情況下，請使用不同的打印機協定。

>[!NOTE]
>
>如果您使用網路打印機且訪問機制是SharedPrinter，則需要指定打印機的完整網路路徑。使用Java API將打印流發送到網路打印機

使用輸出API(Java)將打印流發送到網路打印機：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。

1. 參考XML資料來源

   * 建立`java.io.FileInputStream`對象，該對象表示XML資料源，該資料源使用其建構子並傳遞指定XML檔案位置的字串值來填充文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定列印執行時期選項

   建立`PrintedOutputOptionsSpec`對象，該對象表示打印運行時選項。 例如，您可以叫用`PrintedOutputOptionsSpec`物件的`setCopies`方法，以指定要列印的份數。

   >[!NOTE]
   >
   >如果您要產生ZPL列印串流，則無法使用`PrintedOutputOptionsSpec`物件的`setPagination`方法來設定分頁值。 同樣地，您無法為ZPL打印流設定以下選項：OutputJog、PageOffset和Stapler。 `setPagination`方法對於PostScript產生無效。 它僅適用於PCL生成。

1. 擷取要列印的檔案

   * 調用`OutputClient`物件的`generatePrintedOutput`方法並傳遞下列值，以擷取要列印的檔案：

      * 指定打印流的`PrintFormat`枚舉值。 例如，若要建立PostScript列印串流，請傳遞`PrintFormat.PostScript`。
      * 指定表單設計名稱的字串值。
      * 一個字串值，它指定相關輔助檔案（如影像檔案）的位置。
      * 一個字串值，它指定要使用的XDC檔案的位置。
      * `PrintedOutputOptionsSpec`物件，包含列印至檔案所需的執行時期選項。
      * `com.adobe.idp.Document`物件，代表包含表單資料的XML資料來源，以便與表單設計合併。

      此方法返回包含操作結果的`OutputResult`對象。

   * 通過調用`OutputResult`對象「s `getGeneratedDoc`」方法建立要發送到打印機的`com.adobe.idp.Document`對象。 此方法返回`com.adobe.idp.Document`對象。


1. 將打印流發送到網路打印機

   調用`OutputClient`物件的`sendToPrinter`方法並傳遞下列值，將列印串流傳送至網路印表機：

   * `com.adobe.idp.Document`物件，代表要傳送至印表機的列印串流。
   * `PrinterProtocol`枚舉值，它指定要使用的打印機協定。 例如，要指定SharedPrinter協定，請傳遞`PrinterProtocol.SharedPrinter`。
   * 指定打印伺服器名稱的字串值。 例如，假設打印伺服器的名稱為PrintSever1，則傳遞`\\\PrintSever1`。
   * 指定打印機名稱的字串值。 例如，假設打印機的名稱為Printer1，則傳遞`\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >`sendToPrinter`方法已新增至8.2.1版的AEM FormsAPI。

### 使用web service API {#send-a-print-stream-to-a-printer-using-the-web-service-api}將打印流發送到打印機

使用Output API(web service)將打印流發送到網路打印機：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存表單資料。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞指定包含表單資料之XML檔案位置的字串值。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列長度。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 設定列印執行時期選項。

   使用其建構子建立`PrintedOutputOptionsSpec`對象。 例如，您可以指定要列印的份數，方法是指派一個整數值，代表`PrintedOutputOptionsSpec`物件的`copies`資料成員的份數。

   >[!NOTE]
   >
   >如果您要產生ZPL列印串流，則無法使用`PrintedOutputOptionsSpec`物件的`pagination`資料成員來設定分頁值。 同樣地，您無法為ZPL打印流設定以下選項：OutputJog、PageOffset和Stapler。 `pagination`資料成員對於PostScript產生無效。 它僅適用於PCL生成。

1. 擷取要列印的檔案。

   * 調用`OutputServiceService`物件的`generatePrintedOutput`方法並傳遞下列值，以擷取要列印的檔案：

      * 指定打印流的`PrintFormat`枚舉值。 例如，若要建立PostScript列印串流，請傳遞`PrintFormat.PostScript`。
      * 指定表單設計名稱的字串值。
      * 一個字串值，它指定相關輔助檔案（如影像檔案）的位置。
      * 一個字串值，它指定要使用的XDC檔案的位置。
      * `PrintedOutputOptionsSpec`對象包含在向網路打印機發送打印流時使用的打印運行時選項。
      * 包含表單資料的XML資料源的`BLOB`對象。
      * 由`generatePrintedOutput`方法填充的`BLOB`對象。 `generatePrintedOutput`方法會以描述檔案的產生中繼資料填入此物件。 （此參數值僅適用於Web服務調用。）
      * 由`generatePrintedOutput`方法填充的`BLOB`對象。 `generatePrintedOutput`方法會以結果資料填入此物件。 （此參數值僅適用於Web服務調用。）
      * 包含操作結果的`OutputResult`對象。 （此參數值僅適用於Web服務調用。）
   * 通過獲取`OutputResult`對象「s `generatedDoc`」方法的值，建立要發送到打印機的`BLOB`對象。 此方法傳回包含`generatePrintedOutput`方法傳回之PostScript資料的`BLOB`物件。


1. 將打印流發送到網路打印機。

   調用`OutputClient`物件的`sendToPrinter`方法並傳遞下列值，將列印串流傳送至網路印表機：

   * `BLOB`物件，代表要傳送至印表機的列印串流。
   * `PrinterProtocol`枚舉值，它指定要使用的打印機協定。 例如，要指定SharedPrinter協定，請傳遞`PrinterProtocol.SharedPrinter`。
   * 一個`bool`值，它指定是否使用前一個參數值。 傳遞值`true`。 （此參數值僅適用於Web服務調用。）
   * 指定打印伺服器名稱的字串值。 例如，假設打印伺服器的名稱為PrintSever1，請傳遞`\\\PrintSever1`。
   * 指定打印機名稱的字串值。 例如，假設打印機的名稱為Printer1，請傳遞`\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >`sendToPrinter`方法已新增至8.2.1版的AEM FormsAPI。

## 建立多個輸出檔案{#creating-multiple-output-files}

Output服務可以為XML資料源中的每個記錄或包含所有記錄的單個檔案（預設功能為此功能）建立單獨的文檔。 例如，假設有10個記錄位於XML資料來源中，您會指示「輸出」服務使用「輸出服務API」為每個記錄建立個別的PDF檔案（或其他輸出類型）。 因此，輸出服務會產生十份PDF檔案。 （您可以傳送多個列印串流至印表機，而不是建立檔案。）

下圖還顯示了處理包含多個記錄的XML資料檔案的輸出服務。 不過，假設您指示「輸出」服務建立包含所有資料記錄的單一PDF檔案。 在這種情況下，輸出服務將生成一個包含所有記錄的文檔。

下圖顯示Output服務處理包含多個記錄的XML資料檔案。 假設您指示輸出服務為每個資料記錄建立個別的PDF檔案。 在這種情況下，「輸出」服務會為每個資料記錄產生個別的PDF檔案。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

以下XML資料顯示包含三個資料記錄的資料檔案範例。

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

請注意，啟動和結束每個資料記錄的XML元素為`LoanRecord`。 此XML元素由產生多個檔案的應用程式邏輯參考。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-7}摘要

若要根據XML資料來源建立多個PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料來源。
1. 設定PDF執行時期選項。
1. 設定演算執行時期選項。
1. 產生多個PDF檔案。
1. 檢索操作的結果。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用Output web service API，請建立`OutputServiceService`物件。

**參考XML資料來源**

參考包含多個記錄的XML資料來源。 必須使用XML元素來分隔資料記錄。 例如，在本節稍早顯示的範例XML資料來源中，分隔資料記錄的XML元素名為`LoanRecord`。

每個要填入資料的表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不符，則會忽略它。 如果指定了所有XML元素，則不需要匹配XML元素的顯示順序。

**設定PDF執行時期選項**

您必須為Output服務設定以下運行時選項，才能基於XML資料源成功建立多個檔案：

* **許多檔案**:指定輸出服務是建立單個文檔還是建立多個文檔。您可以指定true或false。 要為XML資料源中的每個資料記錄建立單獨的文檔，請指定true。
* **檔案URI**:指定輸出服務生成的檔案的位置。例如，假設您指定C:\\Adobe\forms\Loan.pdf。 在這種情況下，輸出服務會建立名為Loan.pdf的檔案，並將檔案放在C:\\Adobe\forms folder檔案夾中。 當有多個檔案時，檔案名稱為Loan0001.pdf、Loan0002.pdf、Loan0003.pdf等。 如果您指定檔案位置，則檔案會放在伺服器上，而非用戶端電腦上。
* **記錄名稱**:指定在資料來源中分隔資料記錄的XML元素名稱。例如，在本節稍早顯示的範例XML資料來源中，分隔資料記錄的XML元素稱為`LoanRecord`。 (您可以為記錄級別指定數值，以指示包含資料記錄的元素級別，而不是設定「記錄名稱」運行時選項。 不過，您只能設定「記錄名稱」或「記錄層級」。 您不能同時設定這兩個值。)

**設定渲染運行時選項**

您可以在建立多個檔案時，設定轉譯執行時期選項。 雖然這些選項不是必需的（與輸出運行時選項不同，這些選項是必需的），但您可以執行諸如提高輸出服務的效能之類的任務。 例如，您可以快取Output服務使用的表單設計，以提升效能。

當輸出服務處理批處理記錄時，它以增量方式讀取包含多個記錄的資料。 即，輸出服務將資料讀取到記憶體中，並在處理記錄批時釋放資料。 當設定兩個執行時期選項中的一個時，「輸出」服務會以遞增方式載入資料。 如果設定「記錄名稱」運行時選項，則「輸出」服務以增量方式讀取資料。 同樣地，如果將「記錄級別」運行時間選項設定為2或更大，則「輸出」服務以增量方式讀取資料。

您可以使用`PDFOutputOptionsSpec`或`PrintedOutputOptionSpec`物件的`setLazyLoading`方法來控制輸出服務是否執行遞增載入。 您可以將值`false`傳遞至此方法，以關閉遞增載入。

**產生多個PDF檔案**

在參考包含多個資料記錄並設定執行時期選項的有效XML資料來源後，您就可以叫用「輸出」服務，以產生多個檔案。 當產生多個記錄時，`OutputResult`物件的`getGeneratedDoc`方法會傳回`null`。

**檢索操作的結果**

輸出服務執行操作後，它返回指定操作是否成功的XML資料。 輸出服務會傳回下列XML。 在這種情況下，輸出服務生成了42個文檔。

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

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API {#create-multiple-pdf-files-using-the-java-api}建立多個PDF檔案

使用輸出API(Java)建立多個PDF檔案：

1. 包含專案檔案」

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。.

1. 建立輸出客戶端對象

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。

1. 參考XML資料來源

   * 使用`java.io.FileInputStream`物件的建構函式並傳遞指定XML檔案位置的字串值，以建立代表包含多個記錄之XML資料來源的物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定PDF執行時期選項

   * 使用其建構子建立`PDFOutputOptionsSpec`對象。
   * 調用`PDFOutputOptionsSpec`物件的`setGenerateManyFiles`方法，以設定「多個檔案」選項。 例如，請傳遞值`true`，以指示Output服務為XML資料來源中的每個記錄建立個別的PDF檔案。 （如果您通過`false`，輸出服務將生成包含所有記錄的單個PDF文檔）。
   * 調用`PDFOutputOptionsSpec`物件的`setFileUri`方法並傳遞字串值，指定輸出服務所產生檔案的位置，以設定檔案URI選項。 「檔案URI」選項是相對於代管AEM Forms的J2EE應用程式伺服器，而非用戶端電腦。
   * 調用`OutputOptionsSpec`物件的`setRecordName`方法，並傳遞字串值，指定分隔資料記錄的資料來源中的XML元素名稱，以設定「記錄名稱」選項。 (例如，請考慮本節稍早說明的XML資料來源。 分隔資料記錄的XML元素名稱為LoanRecord)。

1. 設定渲染運行時選項

   * 使用其建構子建立`RenderOptionsSpec`對象。
   * 快取表單設計，以調用`RenderOptionsSpec`物件的`setCacheEnabled`並傳遞`true`的`Boolean`值，以改善輸出服務的效能。

1. 產生多個PDF檔案

   叫用`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以產生多個PDF檔案：

   * `TransformationFormat`列舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 指定表單設計所在內容根目錄的字串值。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `com.adobe.idp.Document`物件，包含XML資料來源，其中包含要與表單設計合併的資料。

   `generatePDFOutput`方法返回包含操作結果的`OutputResult`對象。

1. 檢索操作的結果

   * 建立`java.io.File`對象，該對象表示將包含`generatePDFOutput`方法結果的XML檔案。 請確定副檔名為。xml。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案（請確定您使用`applyUsageRights`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API建立多個PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#create-multiple-pdf-files-using-the-web-service-api}建立多個PDF檔案

使用輸出API(web service)建立多個PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存包含多個記錄的表單資料。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，該值代表包含多個記錄之XML檔案的檔案位置。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 設定PDF執行時期選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`對象。
   * 為`OutputOptionsSpec`物件的`generateManyFiles`資料成員指派布林值，以設定「多個檔案」選項。 例如，將`true`值指派給此資料成員，以指示「輸出」服務為XML資料來源中的每項記錄建立個別的PDF檔案。 （如果您指派`false`給此資料成員，則輸出服務會產生包含所有記錄的單一PDF）。
   * 通過為`OutputOptionsSpec`對象的`fileURI`資料成員指定指定輸出服務生成的檔案位置的字串值來設定檔案URI選項。 「檔案URI」選項是相對於代管AEM Forms的J2EE應用程式伺服器，而非用戶端電腦。
   * 通過為資料源中指定XML元素名稱的字串值（該字串值將資料記錄分隔到`OutputOptionsSpec`對象的`recordName`資料成員）來設定記錄名稱選項。
   * 通過為`OutputOptionsSpec`對象的`copies`資料成員分配一個整數值，該整數值指定輸出服務生成的副本數。

1. 設定演算執行時期選項。

   * 使用其建構子建立`RenderOptionsSpec`對象。
   * 快取表單設計，將值`true`指派給`RenderOptionsSpec`物件的`cacheEnabled`資料成員，以改善輸出服務的效能。

1. 產生多個PDF檔案。

   叫用`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立多個PDF檔案：

   * TransformationFormat枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 指定表單設計所在內容根目錄的字串值。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `BLOB`物件，包含XML資料來源，其中包含要與表單設計合併的資料。
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以描述檔案的產生中繼資料填入此物件。
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。
   * 包含操作結果的`OutputResult`對象。

1. 檢索操作的結果

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為。xml。
   * 建立位元組陣列，儲存由`OutputServiceService`物件的`generatePDFOutput`方法（第8個參數）填入結果資料之`BLOB`物件的資料內容。 獲取`BLOB`對象`binaryData`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立搜索規則{#creating-search-rules}

您可以建立搜尋規則，讓「輸出」服務檢查輸入資料，並根據資料內容使用不同的表單設計來產生輸出。 例如，如果文字&#x200B;*mortgage*&#x200B;位於輸入資料中，則輸出服務可以使用名為Mortgage.xdp的表單設計。 同樣地，如果文本&#x200B;*automobile*&#x200B;位於輸入資料中，則輸出服務可以使用保存為AutomobileLoan.xdp的表單設計。 雖然Output服務可以生成不同的輸出類型，但本節假定Output服務生成PDF檔案。 下圖顯示「輸出」服務，它可處理XML資料檔案並使用許多表格設計之一來產生PDF檔案。

此外，輸出服務還能產生檔案封裝，其中在資料集中提供多個記錄，且每個記錄都與表單設計相符，而單一檔案則由多個表單設計組成。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-8}摘要

要指示輸出服務在生成文檔時使用搜索規則，請執行以下步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 參考XML資料來源。
1. 定義搜尋規則。
1. 設定PDF執行時期選項。
1. 設定演算執行時期選項。
1. 產生PDF檔案。
1. 檢索操作的結果。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要項)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援J2EE應用程式伺服器上，則您將需要以部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案來取代adobe-utilities.jar和jbossall-client.jar。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。

**參考XML資料來源**

每個要填入資料的表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不符，則會忽略它。 只要指定了所有XML元素，就不需要與XML元素的顯示順序匹配。

**定義搜尋規則**

要定義搜索規則，您可以定義「輸出」服務在輸入資料中搜索的一個或多個文本模式。 對於您定義的每個文本模式，您指定在文本模式所在時使用的相應表單設計。 如果找到文字模式，則輸出服務會使用對應的表單設計來產生輸出。 文本模式的示例是&#x200B;*mortgage*。

>[!NOTE]
>
>如果未找到文字圖樣，則會使用預設表格。 請確定您使用的所有表單設計都位於內容根目錄中。

**設定PDF執行時期選項**

設定下列PDF執行時期選項，讓「輸出」服務能夠根據多種表單設計成功建立PDF檔案：

* **檔案URI**:指定輸出服務所生成的PDF檔案的名稱和位置。
* **規則**:指定您定義的規則。
* **LookAHead**:指定從輸入資料檔案開始掃描定義的文本模式時要使用的位元組數。預設值為500位元組。

**設定渲染運行時選項**

您可以在建立PDF檔案時設定演算執行時期選項。 雖然這些選項不是必要的（與PDF執行時期選項不同），但您可以執行例如改善輸出服務的效能等工作。 例如，您可以快取Output服務使用的表單設計，以提升效能。

**產生PDF檔案**

參考有效的XML資料來源並設定執行時期選項後，您可以叫用「輸出」服務，以產生PDF檔案。 如果Output服務在輸入資料中找到指定的文本模式，則使用相應的表單設計。 如果未使用文字模式，則輸出服務會使用預設的表單設計。

**檢索操作的結果**

輸出服務執行操作後，它返回指定操作是否成功的XML資料。

**另請參閱**

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API {#create-search-rules-using-the-java-api}建立搜尋規則

使用輸出API(Java)建立搜尋規則：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。

1. 參考XML資料來源。

   * 建立`java.io.FileInputStream`對象，該對象表示XML資料源，該資料源使用其建構子並傳遞一個字串值，該字串值指定XML檔案的位置。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 定義搜尋規則。

   * 使用其建構子建立`Rule`對象。
   * 調用`Rule`物件的`setPattern`方法並傳遞指定文字模式的字串值，以定義文字模式。
   * 調用`Rule`物件的`setForm`方法，以定義對應的表單設計。 傳遞指定表單設計名稱的字串值。

   >[!NOTE]
   >
   >對於要定義的每個文本模式，重複前三個子步驟。

   * 使用`java.util.ArrayList`建構函式建立`java.util.List`物件。
   * 對於您建立的每個`Rule`對象，調用`java.util.List`對象的`add`方法並傳遞`Rule`對象。


1. 設定PDF執行時期選項。

   * 使用其建構子建立`PDFOutputOptionsSpec`對象。
   * 指定輸出服務透過叫用`PDFOutputOptionsSpec`物件的`setFileURI`方法所產生的PDF檔案名稱和位置。 傳遞指定PDF檔案位置的字串值。 「檔案URI」選項是相對於代管AEM Forms的J2EE應用程式伺服器，而非用戶端電腦。
   * 設定您透過叫用`PDFOutputOptionsSpec`物件的`setRules`方法所定義的規則。 傳遞包含`Rule`物件的`java.util.List`物件。
   * 調用`PDFOutputOptionsSpec`物件的`setLookAhead`方法，設定要掃描已定義文字模式的位元組數。 傳遞一個整數值，代表位元組數。

1. 設定演算執行時期選項。

   * 使用其建構子建立`RenderOptionsSpec`對象。
   * 快取表單設計，以調用`RenderOptionsSpec`物件的`setCacheEnabled`並傳遞`true`，以改善輸出服務的效能。

1. 產生PDF檔案。

   調用`OutputClient`物件的`generatePDFOutput`方法並傳遞下列值，以產生以多種表單設計為基礎的PDF檔案：

   * `TransformationFormat`枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定預設表單設計名稱的字串值。 也就是說，在未找到文字圖樣時使用的表格設計。
   * 一個字串值，它指定表單設計所在的內容根目錄。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `com.adobe.idp.Document`物件，包含Output服務在定義的文字模式中搜尋的表單資料。

   `generatePDFOutput`方法返回包含操作結果的`OutputResult`對象。

1. 檢索操作的結果。

   * 通過調用`OutputResult`對象的`getStatusDoc`方法，建立表示`generatePDFOutput`方法狀態的`com.adobe.idp.Document`對象。
   * 建立包含操作結果的`java.io.File`對象。 請確定副檔名為。xml。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案（請確定您使用`getStatusDoc`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API建立搜尋規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[快速入門（SOAP模式）:使用Java API建立搜尋規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#create-search-rules-using-the-web-service-api}建立搜尋規則

使用輸出API(web service)建立搜尋規則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考XML資料來源。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存將與PDF檔案合併的資料。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 定義搜尋規則。

   * 使用其建構子建立`Rule`對象。
   * 通過為`Rule`對象的`pattern`資料成員指定指定文本模式的字串值來定義文本模式。
   * 為`Rule`物件的`form`資料成員指派指定表單設計的字串值，以定義對應的表單設計。

   >[!NOTE]
   >
   >對於要定義的每個文本模式，重複前三個子步驟。

   * 建立儲存規則的`MyArrayOf_xsd_anyType`物件。
   * 將每個`Rule`對象分配給`MyArrayOf_xsd_anyType`陣列的元素。 為每個`Rule`對象調用`MyArrayOf_xsd_anyType`對象的`Add`方法。


1. 設定PDF執行時期選項

   * 使用其建構子建立`PDFOutputOptionsSpec`對象。
   * 指定字串值來設定檔案URI選項，該字串值會指定輸出服務所產生的PDF檔案在`PDFOutputOptionsSpec`物件的`fileURI`資料成員上的位置。 「檔案URI」選項是相對於代管AEM Forms的J2EE應用程式伺服器，而非用戶端電腦。
   * 通過為`PDFOutputOptionsSpec`對象的`copies`資料成員分配一個整數值，該整數值指定輸出服務生成的副本數。
   * 將儲存規則的`MyArrayOf_xsd_anyType`對象分配給`PDFOutputOptionsSpec`對象的`rules`資料成員，以設定您定義的規則。
   * 通過為`PDFOutputOptionsSpec`對象的`lookAhead`資料方法指定表示要掃描的位元組數的整數值，設定要掃描已定義文本模式的位元組數。

1. 設定渲染運行時選項

   * 使用其建構子建立`RenderOptionsSpec`對象。
   * 將值`true`指派給`RenderOptionsSpec`物件的`cacheEnabled`資料成員，以快取表單設計，以改善輸出服務的效能。

   >[!NOTE]
   >
   >如果輸入檔案是Acrobat表單，則無法使用`RenderOptionsSpec`物件的`pdfVersion`成員來設定PDF檔案版本。 輸出PDF檔案會保留PDF版本的Acrobat表單。 同樣地，如果輸入檔案是Acrobat表單，則無法使用`RenderOptionsSpec`物件的`taggedPDF`方法來設定標籤的PDF選項。

   >[!NOTE]
   >
   >如果輸入的PDF檔案經過認證或數位簽章，則無法使用`RenderOptionsSpec`物件的`linearizedPDF`成員來設定線性化的PDF選項。 如需詳細資訊，請參閱[數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。

1. 產生PDF檔案

   呼叫`OutputServiceService`物件的`generatePDFOutput`方法並傳遞下列值，以建立PDF檔案：

   * `TransformationFormat`枚舉值。 若要產生PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定表單設計名稱的字串值。
   * 指定表單設計所在內容根目錄的字串值。
   * 包含PDF執行時期選項的`PDFOutputOptionsSpec`物件。
   * `RenderOptionsSpec`物件，包含轉譯執行時期選項。
   * `BLOB`物件，包含XML資料來源，其中包含要與表單設計合併的資料。
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以描述檔案的產生中繼資料填入此物件。 （此參數值僅適用於Web服務調用）。
   * 由`generatePDFOutput`方法填充的`BLOB`對象。 `generatePDFOutput`方法會以結果資料填入此物件。 （此參數值僅適用於Web服務調用）。
   * 包含操作結果的`OutputResult`對象。 （此參數值僅適用於Web服務調用）。

   >[!NOTE]
   >
   >當透過叫用`generatePDFOutput`方法產生PDF檔案時，請注意，您無法將資料與已簽署、認證或包含使用權限的XFA PDF表單合併。 如需使用權的詳細資訊，請參閱[將使用權套用至PDF檔案](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。

1. 檢索操作的結果

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 請確定副檔名為XML。
   * 建立位元組陣列，儲存由`OutputServiceService`物件的`generatePDFOutput`方法（第8個參數）填入結果資料之`BLOB`物件的資料內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 平面化PDF檔案{#flattening-pdf-documents}

您可以使用「輸出」服務，將互動式PDF檔案轉換為非互動式PDF。 互動式PDF檔案可讓使用者輸入或修改PDF檔案欄位中的資料。 將互動式PDF檔案轉換為非互動式PDF檔案的程式稱為&#x200B;*平面化*。 當PDF檔案平面化時，使用者無法修改檔案欄位中的資料。 平面化PDF檔案的一個原因是為了確保資料無法修改。

您可以平面化下列類型的PDF檔案：

* 互動式XFA PDF檔案
* AcrobatForms

嘗試平面化非互動式PDF檔案的PDF會造成例外。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-9}摘要

若要將互動式PDF檔案平面化為非互動式PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出客戶端對象。
1. 擷取互動式PDF檔案。
1. 轉換PDF檔案。
1. 將非互動式PDF檔案儲存為PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您是使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。 有關所有AEM FormsJAR檔案的位置資訊，請參見[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果您使用Java API，請建立`OutputClient`物件。 如果您使用Output web service API，請建立`OutputServiceService`物件。

**擷取互動式PDF檔案**

擷取您要轉換為非互動式PDF檔案的互動式PDF檔案。 嘗試轉換非互動式PDF檔案時，會造成例外。

**轉換PDF檔案**

擷取互動式PDF檔案後，您可將它轉換為非互動式PDF檔案。 Output服務會傳回非互動式PDF檔案。

**將非互動式PDF檔案儲存為PDF檔案**

您可以將非互動式PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API平面化PDF檔案](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[使用web service API平面化PDF檔案](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API {#flatten-a-pdf-document-using-the-java-api}平面化PDF檔案

使用Output API(Java)將互動式PDF檔案平面化為非互動式PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`OutputClient`對象。

1. 擷取互動式PDF檔案。

   * 建立`java.io.FileInputStream`物件，以代表互動式PDF檔案，使用其建構函式並傳遞指定互動式PDF檔案位置的字串值。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 轉換PDF檔案。

   調用`OutputServiceService`物件的`transformPDF`方法並傳遞下列值，將互動式PDF檔案轉換為非互動式PDF檔案：

   * 包含互動式PDF檔案的`com.adobe.idp.Document`物件。
   * `TransformationFormat`列舉值。 若要產生非互動式PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定修訂號的`PDFARevisionNumber`列舉值。 由於此參數適用於PDF/A文檔，因此您可以指定`null`。
   * 一個字串值，代表修訂編號和年份，以冒號分隔。 由於此參數適用於PDF/A文檔，因此您可以指定`null`。
   * `PDFAConformance`列舉值，代表PDF/A符合性等級。 由於此參數適用於PDF/A文檔，因此您可以指定`null`。

   `transformPDF`方法會傳回包含非互動式PDF檔案的`com.adobe.idp.Document`物件。

1. 將非互動式PDF檔案儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製至檔案（請確定您使用`transformPDF`方法傳回的`Document`物件）。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API轉換PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）:使用Java API轉換PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#flatten-a-pdf-document-using-the-web-service-api}平面化PDF檔案

使用Output API(web service)將互動式PDF檔案平面化為非互動式PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立輸出客戶端對象。

   * 使用其預設建構子建立`OutputServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`OutputServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`OutputServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`OutputServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取互動式PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存互動式PDF檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立對象，該字串值表示互動式PDF文檔的檔案位置。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 轉換PDF檔案。

   調用`OutputClient`物件的`transformPDF`方法並傳遞下列值，將互動式PDF檔案轉換為非互動式PDF檔案：

   * 包含互動式PDF檔案的`BLOB`物件。
   * `TransformationFormat`枚舉值。 若要產生非互動式PDF檔案，請指定`TransformationFormat.PDF`。
   * 指定修訂號的`PDFARevisionNumber`列舉值。
   * 一個布爾值，它指定是否使用`PDFARevisionNumber`枚舉值。 由於此參數適用於PDF/A文檔，因此您可以指定`false`。
   * 一個字串值，代表修訂編號和年份，以冒號分隔。 由於此參數適用於PDF/A文檔，因此您可以指定`null`。
   * `PDFAConformance`列舉值，代表PDF/A符合性等級。
   * 指定是否使用`PDFAConformance`列舉值的布林值。 由於此參數適用於PDF/A文檔，因此您可以指定`false`。

   `transformPDF`方法會傳回包含非互動式PDF檔案的`BLOB`物件。

1. 將非互動式PDF檔案儲存為PDF檔案。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示非互動PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存`transformPDF`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
