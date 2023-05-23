---
title: 建立文檔輸出流
seo-title: Creating Document Output Streams
description: 使用輸出服務將文檔轉換為PDF(包括PDF/A文檔)、PostScript、打印機控制語言(PCL)和Zebra - ZPL、Intermec - IPL、Datamax - DPL和TecToshiba - TPCL標籤格式。
seo-description: Use the Output service to convert documents as PDF (including PDF/A documents), PostScript, Printer Control Language (PCL), and Zebra - ZPL, Intermec - IPL, Datamax - DPL, and TecToshiba - TPCL label formats.
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '19016'
ht-degree: 0%

---

# 建立文檔輸出流  {#creating-document-output-streams}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於輸出服務**

「輸出」服務允許您將文檔作為PDF(包括PDF/A文檔)、PostScript、打印機控制語言(PCL)和以下標籤格式輸出：

* 斑馬 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用「輸出」服務，可以將XML表單資料與表單設計合併，並將文檔輸出到網路打印機或檔案。

有兩種方法可將表單設計（XDP檔案）傳遞到Output服務。 您可以通過 `com.adobe.idp.Document` 包含輸出服務的窗體設計的實例。 或者可以傳遞指定表單設計位置的URI值。 在 *用表格編AEM程*。

>[!NOTE]
>
>Output服務不支援包含應用程式對象特定指令碼的AcroformPDF文檔。 不呈現包含應用程式對象特定指令碼的AcroformPDF文檔。

以下各節說明如何使用URI值將表單設計傳遞給Output服務：

* [建立PDF文檔](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A文檔](creating-document-output-streams.md#creating-pdf-a-documents)

以下各節說明如何在 `com.adobe.idp.Document` 實例：

* [將Content Services中的文檔（不建議使用）傳遞到輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF文檔](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

在決定使用哪種技術時，需要考慮的一點是，如果您是從另一家AEM Forms服務部門獲得表單設計，則在 `com.adobe.idp.Document` 實例。 都 *將文檔傳送到輸出服務* 和 *使用片段建立PDF文檔* 部分顯示如何從另一家AEM Forms服務獲取表單設計。 第一部分從Content Services（不建議使用）檢索表單設計。 第二部分從匯編器服務檢索表單設計。

如果從固定位置（如檔案系統）獲取表單設計，則可以使用兩種技術。 即，可以為XDP檔案指定URI值，或使用 `com.adobe.idp.Document` 實例。

要在建立PDF文檔時傳遞指定窗體設計位置的URI值，請使用 `generatePDFOutput` 的雙曲餘切值。 同樣，要通過 `com.adobe.idp.Document` 在建立PDF文檔時將實例輸入到輸出服務， `generatePDFOutput2` 的雙曲餘切值。

向網路打印機發送輸出流時，也可以使用兩種技術。 通過傳遞 `com.adobe.idp.Document` 包含窗體設計的實例，使用 `sendToPrinter2`的雙曲餘切值。 要通過傳遞URI值將輸出流發送到打印機，請使用 `sendToPrinter`的雙曲餘切值。 的 *將打印流發送到打印機* 節使用 `sendToPrinter` 的雙曲餘切值。

您可以使用輸出服務完成以下任務：

* [建立PDF文檔](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A文檔](creating-document-output-streams.md#creating-pdf-a-documents)
* [將Content Services中的文檔（不建議使用）傳遞到輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF文檔](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [打印到檔案](creating-document-output-streams.md#printing-to-files)
* [將打印流發送到打印機](creating-document-output-streams.md#sending-print-streams-to-printers)
* [建立多個輸出檔案](creating-document-output-streams.md#creating-multiple-output-files)
* [建立搜索規則](creating-document-output-streams.md#creating-search-rules)
* [拼合PDF文檔](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立PDF文檔 {#creating-pdf-documents}

您可以使用「輸出」服務建立基於您提供的表單設計和XML表單資料的PDF文檔。 由輸出服務建立的PDF文檔不是互動式PDF文檔；用戶不能輸入或修改表單資料。

如果要建立用於長期儲存的PDF文檔，建議您建立PDF/文檔。 (請參閱 [建立PDF/A文檔](creating-document-output-streams.md#creating-pdf-a-documents)。)

要建立互動式PDF表單，以便用戶輸入資料，請使用Forms服務。 (請參閱 [呈現互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)。)

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要建立PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立輸出客戶端對象。
1. 引用XML資料源。
1. 設定PDF運行時選項。
1. 設定呈現運行時選項。
1. 生成PDF文檔。
1. 檢索操作的結果。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援的J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果使用Java API，請建立 `OutputClient` 的雙曲餘切值。 如果使用Output Web服務API，請建立 `OutputServiceService` 的雙曲餘切值。

**引用XML資料源**

要將資料與表單設計合併，必須引用包含資料的XML資料源。 您計畫用資料填充的每個表單域都必須存在XML元素。 XML元素名稱必須與欄位名稱匹配。 如果XML元素與表單域不對應，或XML元素名稱與欄位名稱不匹配，則忽略該元素。 如果指定了所有XML元素，則不必與XML元素的顯示順序匹配。

請考慮以下貸款申請表示例。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

要將資料合併到此表單設計中，必須建立與表單對應的XML資料源。 以下XML表示與示例抵押申請表單對應的XDP XML資料源。

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
>您不必設定檔案URI運行時選項，而是可以以寫程式方式從Output服務返回的複雜資料類型中檢索PDF文檔。 但是，通過設定檔案URI運行時選項，您不需要建立以寫程式方式檢索PDF文檔的應用程式邏輯。

**設定呈現運行時選項**

可以在建立PDF文檔時設定渲染運行時選項。 雖然這些選項不是必需的(與必需的PDF運行時選項不同)，但您可以執行諸如提高輸出服務的效能之類的任務。 例如，您可以快取輸出服務使用的表單設計以提高其效能。

如果將帶標籤的Acrobat表單用作輸入，則不能使用Output服務Java或Web服務API來關閉帶標籤的設定。 如果嘗試以寫程式方式將此選項設定為 `false`，結果PDF文檔仍被標籤。

>[!NOTE]
>
>如果未指定渲染運行時選項，則使用預設值。 有關呈現運行時選項的資訊，請參見 `RenderOptionsSpec` 類引用。 (請參閱 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**生成PDF文檔**

在引用包含表單資料的有效XML資料源並設定運行時選項後，可以調用輸出服務，從而生成PDF文檔。

在生成PDF文檔時，指定輸出服務建立PDF文檔所需的URI值。 表單設計可以儲存在諸如伺服器檔案系統或作為AEM Forms應用程式的一部分的位置。 通過使用內容根URI值可以引用作為Forms應用程式一部分存在的表單設計（或其他資源，如影像檔案） `repository:///`。 例如，請考慮以下名為 *Loan.xdp* 位於名為「A.D.A.」的Forms應用程式 *應用程式/表單應用程式*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

要訪問上圖中顯示的Loan.xdp檔案，請指定 `repository:///Applications/FormsApplication/1.0/FormsFolder/` 作為傳遞給 `OutputClient` 對象 `generatePDFOutput` 的雙曲餘切值。 指定表單名稱(*Loan.xdp*)作為傳遞給 `OutputClient` 對象 `generatePDFOutput` 的雙曲餘切值。

如果XDP檔案包含影像（或其他資源，如片段），請將資源放在與XDP檔案相同的應用程式資料夾中。 AEM Forms使用內容根URI作為基路徑來解析對影像的引用。 例如，如果Loan.xdp檔案包含映像，請確保將映像放在 `Applications/FormsApplication/1.0/FormsFolder/`。

>[!NOTE]
>
>在調用URI時，可以引用Forms應用程式URI `OutputClient` 對象 `generatePDFOutput` 或 `generatePrintedOutput` 的雙曲餘切值。

>[!NOTE]
>
>要查看通過引用位於Forms應用程式中的XDP建立PDF文檔的完整快速入門，請參見 [快速啟動（EJB模式）:使用Java API基於應用程式XDP檔案建立PDF文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)。

**檢索操作的結果**

在輸出服務執行操作後，它將返回各種資料項，如指定操作是否成功的狀態XML資料。

**另請參閱**

[使用Java API建立PDF文檔](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[使用Web服務API建立PDF文檔](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立PDF文檔 {#create-a-pdf-document-using-the-java-api}

使用輸出API(Java)建立PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用XML資料源。

   * 建立 `java.io.FileInputStream` 表示XML資料源的對象，該XML資料源用於使用PDF文檔的建構子並傳遞一個字串值來指定XML檔案的位置來填充該對象文檔。
   * 建立 `com.adobe.idp.Document` 對象。 通過 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定PDF運行時選項。

   * 建立 `PDFOutputOptionsSpec` 對象。
   * 通過調用 `PDFOutputOptionsSpec` 對象 `setFileURI` 的雙曲餘切值。 傳遞一個字串值，該字串值指定輸出服務生成的PDF檔案的位置。 「檔案URI」選項是相對於承載AEM Forms的J2EE應用程式伺服器，而不是客戶機。

1. 設定呈現運行時選項。

   * 建立 `RenderOptionsSpec` 對象。
   * 通過調用Cache快取表單設計，提高Output服務的效能 `RenderOptionsSpec` 對象 `setCacheEnabled` 傳 `true`。

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 對象 `setPdfVersion` 方法，如果輸入文檔是Acrobat表單(在Acrobat建立的表單)或已簽名或認證的XFA文檔。 輸出PDF文檔保留原始PDF版本。 同樣，您不能通過調用 `RenderOptionsSpec` 對象 `setTaggedPDF` 方法。

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 對象 `setLinearizedPDF` 方法。 (請參閱 [數字簽名PDF文檔&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。)*

1. 生成PDF文檔。

   通過調用PDF `OutputClient` 對象 `generatePDFOutput` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定窗體設計的名稱。
   * 一個字串值，它指定窗體設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `com.adobe.idp.Document` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。

   的 `generatePDFOutput` 方法返回 `OutputResult` 包含操作結果的對象。

   >[!NOTE]
   >
   >通過調用生成PDF文檔時 `generatePDFOutput` 方法，請注意，您不能將資料與已簽名或已認證的XFAPDF表格合併。 (請參閱 [數字簽名和驗證文檔&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。)*

   >[!NOTE]
   >
   >的 `OutputResult` 對象 `getRecordLevelMetaDataList` 方法返回 `null`*。*

   >[!NOTE]
   >
   >您還可以通過調用 `OutputClient` 對象 `generatePDFOutput2` 的雙曲餘切值。 (請參閱 [將Content Services中的文檔（不建議使用）傳遞到輸出服務&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 檢索操作的結果。

   * 檢索 `com.adobe.idp.Document` 表示 `generatePDFOutput` 通過調用 `OutputResult` 對象 `getStatusDoc` 的雙曲餘切值。 此方法返回指定操作是否成功的狀態XML資料。
   * 建立 `java.io.File` 包含操作結果的對象。 確保檔案副檔名為.xml。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象到檔案(確保 `com.adobe.idp.Document` 返回的對象 `getStatusDoc` )。

   儘管輸出服務會將PDF文檔寫入由傳遞到的參數指定的位置 `PDFOutputOptionsSpec` 對象 `setFileURI` 方法，可通過調用PDF/A文檔以寫程式方式檢索文檔 `OutputResult` 對象 `getGeneratedDoc` 的雙曲餘切值。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API建立PDF文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API建立PDF文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立PDF文檔 {#create-a-pdf-document-using-the-web-service-api}

使用輸出API（Web服務）建立PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立輸出客戶端對象。

   * 建立 `OutputServiceClient` 對象。
   * 建立 `OutputServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `OutputServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML資料源。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存將與PDF文檔合併的XML資料。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示包含表單資料的XML檔案的檔案位置。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 設定PDF運行時選項

   * 建立 `PDFOutputOptionsSpec` 對象。
   * 通過分配一個字串值來設定檔案URI選項，該字串值指定輸出服務生成到的PDF檔案的位置 `PDFOutputOptionsSpec` 對象 `fileURI` 資料成員。 「檔案URI」選項是相對於承載AEM Forms的J2EE應用程式伺服器，而不是客戶機。

1. 設定呈現運行時選項。

   * 建立 `RenderOptionsSpec` 對象。
   * 快取表單設計以通過賦值來提高輸出服務的效能 `true` 到 `RenderOptionsSpec` 對象 `cacheEnabled` 資料成員。

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 對象 `setPdfVersion` 方法，如果輸入文檔是Acrobat表單(在Acrobat建立的表單)或已簽名或認證的XFA文檔。 輸出PDF文檔保留原始PDF版本。 同樣，您不能通過調用 `RenderOptionsSpec` 對象 `setTaggedPDF`*方法，如果輸入文檔是Acrobat表單或經簽名或認證的XFA文檔。*

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 對象 `linearizedPDF` 成員。 (請參閱 [數字簽名PDF文檔&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。)*

1. 生成PDF文檔。

   通過調用PDF `OutputServiceService` 對象 `generatePDFOutput`方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定窗體設計的名稱。
   * 一個字串值，它指定窗體設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `BLOB` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用描述文檔的生成元資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用結果資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * 安 `OutputResult` 包含操作結果的對象。 （此參數值僅對於Web服務調用是必需的）。

   >[!NOTE]
   >
   >通過調用生成PDF文檔時 `generatePDFOutput` 方法，請注意，您不能將資料與已簽名或已認證的XFAPDF表格合併。 (請參閱 [數字簽名和驗證文檔&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。)*

   >[!NOTE]
   >
   >您還可以通過調用 `OutputClient` 對象 `generatePDFOutput2` 的雙曲餘切值。 (請參閱 [將Content Services中的文檔（不建議使用）傳遞到輸出服務&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 檢索操作的結果。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 確保檔案副檔名為.xml。
   * 建立一個位元組陣列，用於儲存 `BLOB` 用結果資料填充的對象 `OutputServiceService` 對象 `generatePDFOutput` 方法（第八個參數）。 通過獲取 `BLOB` 對象 `MTOM` `field`。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

   另請參閱

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >的 `OutputServiceService` 對象 `generateOutput` 方法已棄用。

## 建立PDF/A文檔 {#creating-pdf-a-documents}

您可以使用輸出服務建立PDF/文檔。 由於PDF/A是文檔內容長期保留的存檔格式，因此所有字型都被嵌入，檔案也未壓縮。 因此，PDF/A 文件通常比標準 PDF 文件大。此外，PDF/A文檔不包含音頻和視頻內容。 與其他輸出服務任務一樣，您提供了要與表單設計合併的表單設計和資料，以建立PDF/文檔。

PDF/A-1規格由兩個一致性級別組成，即a和b。兩者之間的主要區別在於邏輯結構（可訪問性）支援，這在一致性級別b中不是必需的。無論符合級別如何，PDF/A-1都指示所有字型都嵌入到生成的PDF/A文檔中。

雖然PDF/A是存檔PDF文檔的標準，但如果標準PDF文檔滿足您公司的需要，則PDF/A不是強制性的。 PDF/A標準的目的是建立一個PDF檔案，該檔案可以長期儲存並滿足文檔保存要求。 例如，URL無法嵌入到PDF/A中，因為隨著時間的推移，URL可能會變為無效。

您的公司必須評估自己的需求、您打算保留文檔的時間長短、檔案大小考慮事項，並確定您自己的歸檔策略。 可以通過使用DocConverter服務以寫程式方式確定PDF文檔是否符合PDF/A。 (請參閱 [以寫程式方式確定PDF/符合性](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)。)

PDF/文檔必須使用在窗體設計中指定的字型，且不能替換字型。 因此，如果位於PDF文檔中的字型在主機作業系統(OS)上不可用，則會發生異常。

在Acrobat開啟PDF/A文檔時，將顯示一條消息，確認該文檔是PDF/A文檔，如下圖所示。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM網站有一個PDF/常見問題部分，您可以在 [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml)。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_65)。

### 步驟摘要 {#summary_of_steps-1}

要建立PDF/文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立輸出客戶端對象。
1. 引用XML資料源。
1. 設定PDF/運行時選項。
1. 設定呈現運行時選項。
1. 生成PDF/文檔。
1. 檢索操作的結果。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立自定義應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援的J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果使用Java API，請建立 `OutputClient` 的雙曲餘切值。 如果使用Output Web服務API，請建立 `OutputServiceService` 的雙曲餘切值。

**引用XML資料源**

要將資料與表單設計合併，必須引用包含資料的XML資料源。 要用資料填充的每個表單域都必須存在XML元素。 XML元素名稱必須與欄位名稱匹配。 如果XML元素與表單域不對應，或XML元素名稱與欄位名稱不匹配，則忽略該元素。 如果指定了所有XML元素，則不必與XML元素的顯示順序匹配。

**設定PDF/運行時選項**

建立PDF/文檔時，可以設定「檔案URI」選項。 URI相對於承載AEM Forms的J2EE應用程式伺服器。 即，如果設定C:\Adobe ，則檔案將寫入伺服器上的資料夾，而不寫入客戶端電腦。 URI指定輸出服務生成的PDF/A檔案的名稱和位置。

**設定呈現運行時選項**

在建立PDF/A文檔時，可以設定渲染運行時選項。 可以設定的兩個PDF/A相關選項是 `PDFAConformance` 和 `PDFARevisionNumber` 值。 的 `PDFAConformance` 值指PDF文檔如何遵守指定長期電子文檔保留方式的要求。 此選項的有效值為 `A` 和 `B`。 有關級別a和b一致性的資訊，請參閱標題為「PDF/A-1 ISO」的規範 *ISO 19005-1文檔管理*。

的 `PDFARevisionNumber` 值指PDF/A文檔的修訂號。 有關PDF/A文檔的修訂號的資訊，請參閱標題為「PDF/A-1 ISO規範」的 *ISO 19005-1文檔管理*。

>[!NOTE]
>
>無法將標籤的Adobe PDF選項設定為 `false` 建立PDF/A 1A文檔時。 PDF/A 1A將始終是帶標籤的PDF文檔。 此外，不能將標籤的Adobe PDF選項設定為 `true` 建立PDF/A 1B文檔時。 PDF/A 1B將始終是未標籤的PDF文檔。

**生成PDF/文檔**

引用包含表單資料的有效XML資料源並設定運行時選項後，可以調用輸出服務，使其生成PDF/A文檔。

**檢索操作的結果**

在輸出服務執行操作後，它返回各種資料項，如指定操作是否成功的XML資料。

**另請參閱**

[使用Java API建立PDF/文檔](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[使用Web服務API建立PDF/文檔](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立PDF/文檔 {#create-a-pdf-a-document-using-the-java-api}

使用輸出API(Java)建立PDF/文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用XML資料源。

   * 建立 `java.io.FileInputStream` 表示XML資料源的對象，該XML資料源使用PDF/A文檔的建構子並傳遞一個字串值來指定XML檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定PDF/運行時選項。

   * 建立 `PDFOutputOptionsSpec` 對象。
   * 通過調用 `PDFOutputOptionsSpec` 對象 `setFileURI` 的雙曲餘切值。 傳遞一個字串值，該字串值指定輸出服務生成的PDF檔案的位置。 「檔案URI」選項是相對於承載AEM Forms的J2EE應用程式伺服器，而不是客戶機。

1. 設定呈現運行時選項。

   * 建立 `RenderOptionsSpec` 對象。
   * 設定 `PDFAConformance` 通過調用 `RenderOptionsSpec` 對象 `setPDFAConformance` 方法和通過 `PDFAConformance` 指定一致性級別的枚舉值。 例如，要指定一致性級別A，請通過 `PDFAConformance.A`。
   * 設定 `PDFARevisionNumber` 通過調用 `RenderOptionsSpec` 對象 `setPDFARevisionNumber` 方法 `PDFARevisionNumber.Revision_1`。

   >[!NOTE]
   >
   >PDF/A文檔的PDF版本為1.4，而不管您為 `RenderOptionsSpec` 對象 `setPdfVersion`*的雙曲餘切值。*

1. 生成PDF/文檔。

   通過調用PDF/文檔 `OutputClient` 對象 `generatePDFOutput` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF/文檔，請指定 `TransformationFormat.PDFA`。
   * 一個字串值，它指定窗體設計的名稱。
   * 一個字串值，它指定窗體設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `com.adobe.idp.Document` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。

   的 `generatePDFOutput` 方法返回 `OutputResult` 包含操作結果的對象。

   >[!NOTE]
   >
   >的 `OutputResult` 對象 `getRecordLevelMetaDataList` 方法返回 `null`。

   >[!NOTE]
   >
   >您還可以通過調用 `OutputClient` 對象 `generatePDFOutput`2方法。 (請參閱 [將Content Services中的文檔（不建議使用）傳遞到輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 檢索操作的結果。

   * 建立 `com.adobe.idp.Document` 表示 `generatePDFOutput` 方法 `OutputResult` 對象 `getStatusDoc` 的雙曲餘切值。
   * 建立 `java.io.File` 包含操作結果的對象。 確保檔案副檔名為.xml。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象到檔案(確保 `com.adobe.idp.Document` 返回的對象 `getStatusDoc` )。

   >[!NOTE]
   >
   >儘管Output服務會將PDF/A文檔寫入到參數指定的位置，該位置將傳遞給 `PDFOutputOptionsSpec` 對象 `setFileURI` 方法，可通過調用PDF/A文檔以寫程式方式檢索文檔 `OutputResult` 對象 `getGeneratedDoc` 的雙曲餘切值。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API建立PDF/文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服務API建立PDF/文檔 {#create-a-pdf-a-document-using-the-web-service-api}

使用輸出API（Web服務）建立PDF/文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立輸出客戶端對象。

   * 建立 `OutputServiceClient` 對象。
   * 建立 `OutputServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `OutputServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML資料源。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存將與PDF/A文檔合併的資料。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 設定PDF/運行時選項。

   * 建立 `PDFOutputOptionsSpec` 對象。
   * 通過分配一個字串值來設定檔案URI選項，該字串值指定輸出服務生成到的PDF檔案的位置 `PDFOutputOptionsSpec` 對象 `fileURI` 資料成員。 「檔案URI」選項是相對於承載AEM Forms的J2EE應用程式伺服器，而不是客戶機

1. 設定呈現運行時選項。

   * 建立 `RenderOptionsSpec` 對象。
   * 設定 `PDFAConformance` 值 `PDFAConformance` 枚舉值到 `RenderOptionsSpec` 對象 `PDFAConformance` 資料成員。 例如，要指定符合性級別A，請分配 `PDFAConformance.A` 到此資料成員。
   * 設定 `PDFARevisionNumber` 值 `PDFARevisionNumber` 枚舉值到 `RenderOptionsSpec` 對象 `PDFARevisionNumber` 資料成員。 分配 `PDFARevisionNumber.Revision_1` 到此資料成員。

   >[!NOTE]
   >
   >PDF/A文檔的PDF版本為1.4，而不管您指定哪個值。

1. 生成PDF/文檔。

   通過調用PDF `OutputServiceService` 對象 `generatePDFOutput`方法並傳遞以下值：

   * TransformationFormat枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDFA`。
   * 一個字串值，它指定窗體設計的名稱。
   * 一個字串值，它指定窗體設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `BLOB` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用描述文檔的生成元資料填充此對象。 （僅Web服務調用需要此參數值。）
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用結果資料填充此對象。 （僅Web服務調用需要此參數值。）
   * 安 `OutputResult` 包含操作結果的對象。 （僅Web服務調用需要此參數值。）

   >[!NOTE]
   >
   >您還可以通過調用 `OutputClient` 對象 `generatePDFOutput`2方法。 (請參閱 [將Content Services中的文檔（不建議使用）傳遞到輸出服務](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 檢索操作的結果。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 確保檔案副檔名為.xml。
   * 建立一個位元組陣列，用於儲存 `BLOB` 用結果資料填充的對象 `OutputServiceService` 對象 `generatePDFOutput` 方法（第八個參數）。 通過獲取 `BLOB` 對象 `MTOM` 的子菜單。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將Content Services中的文檔（不建議使用）傳遞到輸出服務 {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

「輸出」服務將呈現一個非互動式PDF表單，該表單基於通常另存為XDP檔案並在設計器中建立的表單設計。 你可以通過 `com.adobe.idp.Document` 包含輸出服務的窗體設計的對象。 然後，輸出服務將呈現位於 `com.adobe.idp.Document` 的雙曲餘切值。

通過 `com.adobe.idp.Document` 輸出服務的對象是其他AEM Forms服務操作返回 `com.adobe.idp.Document` 實例。 就是說，你可以 `com.adobe.idp.Document` 實例，並呈現它。 例如，假定XDP檔案儲存在名為「Content Services（不建議使用）」的節點中 `/Company Home/Form Designs`，如下圖所示。

您可以以寫程式方式從Content Services中檢索Loan.xdp（已棄用），並將XDP檔案傳遞到 `com.adobe.idp.Document` 的雙曲餘切值。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要將從Content Services（不建議使用）獲取的文檔傳遞到Output服務，請執行以下任務：

1. 包括項目檔案。
1. 建立輸出和文檔管理客戶端API對象。
1. 從Content Services檢索表單設計（不建議使用）。
1. 呈現非互動式PDF窗體。
1. 對資料流執行操作。

**包括項目檔案**

將必要的檔案包括到您的開發項目中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立輸出和文檔管理客戶端API對象**

在以寫程式方式執行輸出服務API操作之前，請建立輸出客戶端API對象。 此外，由於此工作流從Content Services（不建議使用）檢索XDP檔案，因此請建立Document Management API對象。

**從Content Services檢索表單設計（不建議使用）**

使用Java或Web服務API從Content Services（不建議使用）檢索XDP檔案。 在 `com.adobe.idp.Document` 實例(或 `BLOB` 實例)。 然後，您可以 `com.adobe.idp.Document` 實例。

**呈現非互動式PDF窗體**

要呈現非互動式窗體，請傳遞 `com.adobe.idp.Document` 從Content Services（不建議使用）返回到Output服務的實例。

>[!NOTE]
>
>兩種新方法名為 `generatePDFOutput2`和g `eneratePrintedOutput2`接受 `com.adobe.idp.Document` 包含窗體設計的對象。 您還可以通過 `com.adobe.idp.Document`在將打印流發送到網路打印機時包含輸出服務的窗體設計。

**對表單資料流執行操作**

可以將非互動式窗體另存為PDF檔案。 該表格可以在Adobe Reader或Acrobat觀看。

**另請參閱**

[使用Java API將文檔傳遞到輸出服務](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[使用Web服務API將文檔傳遞到輸出服務](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[使用片段建立PDF文檔](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### 使用Java API將文檔傳遞到輸出服務 {#pass-documents-to-the-output-service-using-the-java-api}

使用Output Service和Content Services（不建議使用）API(Java)傳遞從Content Services（不建議使用）檢索的文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立輸出和文檔管理客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。
   * 建立 `DocumentManagementServiceClientImpl` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 從Content Services檢索表單設計（不建議使用）。

   調用 `DocumentManagementServiceClientImpl` 對象 `retrieveContent` 方法並傳遞以下值：

   * 一個字串值，它指定添加內容的儲存。 預設儲存為 `SpacesStore`。 此值是必需參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需參數。
   * 指定版本的字串值。 此值是可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。

   的 `retrieveContent` 方法返回 `CRCResult` 包含XDP檔案的對象。 檢索 `com.adobe.idp.Document` 實例 `CRCResult` 對象 `getDocument` 的雙曲餘切值。

1. 呈現非互動式PDF窗體。

   調用 `OutputClient` 對象 `generatePDFOutput2` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定附加資源（如影像）所在的內容根。
   * A `com.adobe.idp.Document` 表示窗體設計的對象(使用 `CRCResult` 對象 `getDocument` )。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `com.adobe.idp.Document` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。

   的 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作結果的對象。

1. 對表單資料流執行操作。

   * 檢索 `com.adobe.idp.Document` 通過調用 `OutputResult` 對象 `getGeneratedDoc` 的雙曲餘切值。
   * 建立 `java.io.File` 包含操作結果的對象。 確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象到檔案(確保 `com.adobe.idp.Document` 返回的對象 `getGeneratedDoc` )。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API將文檔傳遞到輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API將文檔傳遞到輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將文檔傳遞到輸出服務 {#pass-documents-to-the-output-service-using-the-web-service-api}

使用Output Service和Content Services（棄用）API（Web服務）傳遞從Content Services（棄用）檢索的文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 由於此客戶端應用程式調用兩個AEM Forms服務，因此建立兩個服務引用。 對與輸出服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   對與文檔管理服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   因為 `BLOB` 資料類型是兩種服務引用的公用類型，完全限定 `BLOB` 資料類型。 在相應的Web服務快速啟動中， `BLOB` 實例完全限定。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立輸出和文檔管理客戶端API對象。

   * 建立 `OutputServiceClient` 對象。
   * 建立 `OutputServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `OutputServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對 `DocumentManagementServiceClient`服務客戶端。

1. 從Content Services檢索表單設計（不建議使用）。

   通過調用 `DocumentManagementServiceClient` 對象 `retrieveContent` 方法並傳遞以下值：

   * 一個字串值，它指定添加內容的儲存。 預設儲存為 `SpacesStore`。 此值是必需參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需參數。
   * 指定版本的字串值。 此值是可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。
   * 儲存瀏覽連結值的字串輸出參數。
   * A `BLOB` 儲存內容的輸出參數。 可以使用此輸出參數檢索內容。
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 儲存內容屬性的輸出參數。
   * A `CRCResult` 輸出參數。 您可以使用 `BLOB` 輸出參數以檢索內容。

1. 呈現非互動式PDF窗體。

   調用 `OutputServiceClient` 對象 `generatePDFOutput2` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定附加資源（如影像）所在的內容根。
   * A `BLOB` 表示窗體設計的對象(使用 `BLOB` 由Content Services返回的實例（不建議使用）。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `BLOB` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。
   * 輸出 `BLOB` 填充的對象 `generatePDFOutput2` 的雙曲餘切值。 的 `generatePDFOutput2` 方法使用描述文檔的生成元資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * 輸出 `OutputResult` 包含操作結果的對象。 （此參數值僅對於Web服務調用是必需的）。

   的 `generatePDFOutput2` 方法返回 `BLOB` 包含非互動式PDF窗體的對象。

1. 對表單資料流執行操作。

   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示互動式PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 從 `generatePDFOutput2` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 將儲存庫中的文檔傳遞到輸出服務 {#passing-documents-located-in-the-repository-to-the-output-service}

「輸出」服務將呈現一個非互動式PDF表單，該表單基於通常另存為XDP檔案並在設計器中建立的表單設計。 你可以通過 `com.adobe.idp.Document` 包含輸出服務的窗體設計的對象。 然後，輸出服務將呈現位於 `com.adobe.idp.Document` 的雙曲餘切值。

通過 `com.adobe.idp.Document` 輸出服務的對象是其他AEM Forms服務操作返回 `com.adobe.idp.Document` 實例。 就是說，你可以 `com.adobe.idp.Document` 實例，並呈現它。 例如，假定XDP檔案儲存在AEM Forms儲存庫中，如下圖所示。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

的 *表單資料夾* folder是AEM Forms儲存庫中的用戶定義的位置（此位置是示例，預設情況下不存在）。 在此示例中，名為Loan.xdp的窗體設計位於此資料夾中。 除了表單設計之外，還可以將其他表單輔助材料（如影像）儲存在此位置。 位於AEM Forms儲存庫中的資源的路徑是：

`Applications/Application-name/Application-version/Folder.../Filename`

可以以寫程式方式從AEM Forms儲存庫中檢索Loan.xdp，並將其傳遞到 `com.adobe.idp.Document` 的雙曲餘切值。

可以使用兩種方法之一基於儲存庫中的XDP檔案建立PDF。 可以通過引用傳遞XDP位置，也可以通過寫程式方式從儲存庫中檢索XDP，並將其傳遞到XDP檔案內的「輸出」服務。

[快速啟動（EJB模式）:使用Java API基於應用程式XDP檔案建立PDF文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （顯示如何通過引用傳遞XDP檔案的位置）。

[快速啟動（EJB模式）:使用Java API將位於AEM Forms資料檔案庫中的文檔傳遞到輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (顯示如何以寫程式方式從AEM Forms儲存庫檢索XDP檔案，並將其傳遞到 `com.adobe.idp.Document` 實例)。 （本節討論如何執行此任務）

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

要將從AEM Forms儲存庫獲取的文檔傳遞到輸出服務，請執行以下任務：

1. 包括項目檔案。
1. 建立輸出和文檔管理客戶端API對象。
1. 從AEM Forms儲存庫檢索表單設計。
1. 呈現非互動式PDF窗體。
1. 對資料流執行操作。

**包括項目檔案**

將必要的檔案包括到您的開發項目中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立輸出和文檔管理客戶端API對象**

在以寫程式方式執行輸出服務API操作之前，請建立輸出客戶端API對象。 此外，由於此工作流從Content Services（不建議使用）檢索XDP檔案，因此請建立Document Management API對象。

**從AEM Forms儲存庫檢索表單設計**

使用Repository API從AEM Forms資料檔案庫中檢索XDP檔案。 (請參閱 [讀取資源](/help/forms/developing/aem-forms-repository.md#reading-resources)。)

在 `com.adobe.idp.Document` 實例(或 `BLOB` 實例)。 然後，您可以 `com.adobe.idp.Document` 輸出服務的實例。

**呈現非互動式PDF窗體**

要呈現非互動式窗體，請傳遞 `com.adobe.idp.Document` 使用AEM Forms資料庫API返回的實例。

>[!NOTE]
>
>兩種新方法名為 `generatePDFOutput2`和 `generatePrintedOutput2`接受 `com.adobe.idp.Document`包含窗體設計的對象。 您還可以通過 `com.adobe.idp.Document` 在將打印流發送到網路打印機時包含輸出服務的窗體設計。

**對表單資料流執行操作**

可以將非互動式窗體另存為PDF檔案。 該表格可以在Adobe Reader或Acrobat觀看。

**另請參閱**

[使用Java API將儲存庫中的文檔傳遞到輸出服務](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

資源儲存庫客戶端

### 使用Java API將儲存庫中的文檔傳遞到輸出服務 {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

使用輸出服務和儲存庫API(Java)傳遞從儲存庫檢索的文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar和adobe-repository-client.jar。

1. 建立輸出和文檔管理客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。
   * 建立 `DocumentManagementServiceClientImpl` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 從AEM Forms儲存庫檢索表單設計。

   調用 `ResourceRepositoryClient` 對象 `readResourceContent` 方法，並將指定URI位置的字串值傳遞到XDP檔案。 比如說， `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。 此值是必需的。 此方法返回 `com.adobe.idp.Document` 表示XDP檔案的實例。

1. 呈現非互動式PDF窗體。

   調用 `OutputClient` 對象 `generatePDFOutput2` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定附加資源（如影像）所在的內容根。 比如說， `repository:///Applications/FormsApplication/1.0/FormsFolder/`。
   * A `com.adobe.idp.Document` 表示窗體設計的對象(使用 `ResourceRepositoryClient` 對象 `readResourceContent` )。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `com.adobe.idp.Document` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。

   的 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作結果的對象。

1. 對表單資料流執行操作。

   * 檢索 `com.adobe.idp.Document` 通過調用 `OutputResult` 對象 `getGeneratedDoc` 的雙曲餘切值。
   * 建立 `java.io.File` 包含操作結果的對象。 確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象到檔案(確保 `com.adobe.idp.Document` 返回的對象 `getGeneratedDoc` )。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API將位於AEM Forms資料檔案庫中的文檔傳遞到輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用片段建立PDF文檔 {#creating-pdf-documents-using-fragments}

可以使用「輸出」和「匯編器」服務建立基於片段的輸出流，如PDF文檔。 匯編器服務基於位於多個XDP檔案中的片段來匯編XDP文檔。 已裝配的XDP文檔將傳遞給Output服務，該服務將建立PDF文檔。 儘管此工作流顯示正在生成的PDF文檔，但輸出服務可以為此工作流生成其他輸出類型，如ZPL。 PDF文檔僅用於討論。

下圖顯示了此工作流。

![cp_cp_outputsamblements片段](assets/cp_cp_outputassemblefragments.png)

閱讀前 *使用片段建立PDF文檔*，建議您熟悉使用匯編器服務來匯編多個XDP文檔。 (請參閱 [組裝多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)。)

>[!NOTE]
>
>您還可以將由匯編器服務匯編的表單設計傳遞給Forms服務，而不是輸出服務。 輸出服務和Forms服務的主要區別是Forms服務生成互動式PDF文檔，而輸出服務生成非互動式PDF文檔。 此外，Forms服務無法生成基於打印機的輸出流，如ZPL。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

要基於片段建立PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立輸出和匯編器客戶端對象。
1. 使用匯編器服務生成表單設計。
1. 使用輸出服務生成PDF文檔。
1. 將PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立輸出和匯編器客戶端對象**

在以寫程式方式執行輸出服務API操作之前，請建立輸出客戶端API對象。 此外，由於此工作流調用匯編器服務以建立表單設計，因此建立匯編器客戶端API對象。

**使用匯編器服務生成表單設計**

使用匯編器服務使用片段生成表單設計。 匯編器服務返回 `com.adobe.idp.Document` 包含窗體設計的實例。

**使用輸出服務生成PDF文檔**

可以使用「輸出」服務使用匯編器服務建立的表單設計生成PDF文檔。 通過 `com.adobe.idp.Document` 匯編器服務返回到輸出服務的實例。

**將PDF文檔另存為PDF檔案**

在輸出服務生成PDF文檔後，可以將其另存為PDF檔案。

**另請參閱**

[使用Java API基於片段建立PDF文檔](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[使用Web服務API基於片段建立PDF文檔](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[組裝多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[建立PDF文檔](creating-document-output-streams.md#creating-pdf-documents)

### 使用Java API基於片段建立PDF文檔 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

使用「輸出服務API」和「匯編器服務API」(Java)，基於片段建立PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar。

1. 建立輸出和匯編器客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 使用匯編器服務生成表單設計。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下所需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象。
   * A `java.util.Map` 包含輸入XDP檔案的對象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項（包括預設字型和作業日誌級別）的對象。

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已裝配的XDP文檔的對象。 要檢索已裝配的XDP文檔，請執行以下操作：

   * 調用 `AssemblerResult` 對象 `getDocuments` 的雙曲餘切值。 此方法返回 `java.util.Map` 的雙曲餘切值。
   * 迭代 `java.util.Map` 直到找到結果 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 提取XDP文檔的方法。


1. 使用輸出服務生成PDF文檔。

   調用 `OutputClient` 對象 `generatePDFOutput2` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`
   * 一個字串值，它指定附加資源（如影像）所在的內容根
   * A `com.adobe.idp.Document` 表示窗體設計的對象（使用匯編器服務返回的實例）
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象
   * 的 `com.adobe.idp.Document` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料

   的 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作結果的對象

1. 將PDF文檔另存為PDF檔案。

   * 檢索 `com.adobe.idp.Document` 通過調用PDF文檔 `OutputResult` 對象 `getGeneratedDoc` 的雙曲餘切值。
   * 建立 `java.io.File` 包含操作結果的對象。 確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象。 (確保使用 `com.adobe.idp.Document` 對象 `getGeneratedDoc` 方法返回。)

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API基於片段建立PDF文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API基於片段建立PDF文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服務API基於片段建立PDF文檔 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

使用「輸出服務API」和「匯編器服務API」（Web服務），基於片段建立PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 對與輸出服務關聯的服務引用使用以下WSDL定義：

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   對與匯編器服務關聯的服務引用使用以下WSDL定義：

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   因為 `BLOB` 資料類型是兩種服務引用的公用類型，完全限定 `BLOB` 資料類型。 在相應的Web服務快速啟動中， `BLOB` 實例完全限定。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立輸出和匯編器客戶端對象。

   * 建立 `OutputServiceClient` 對象。
   * 建立 `OutputServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `OutputServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給 `OutputServiceClient.ClientCredentials.UserName.UserName`的子菜單。
      * 將相應的密碼值分配給 `OutputServiceClient.ClientCredentials.UserName.Password`的子菜單。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`的子菜單。
   * 分配 `BasicHttpSecurityMode.TransportCredentialOnly` 常數值 `BasicHttpBindingSecurity.Security.Mode`的子菜單。

   >[!NOTE]
   >
   >對 `AssemblerServiceClient`的雙曲餘切值。

1. 使用匯編器服務生成表單設計。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含所需檔案的對象
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作業結果和所發生的任何異常的對象。 要獲取新建立的XDP文檔，請執行以下操作：

   * 訪問 `AssemblerResult` 對象 `documents` 欄位， `Map` 包含結果PDF文檔的對象。
   * 迭代 `Map` 對象，以檢索已裝配的窗體設計。 強制轉換該陣列成員 `value` 到 `BLOB`。 傳遞此 `BLOB` 實例。


1. 使用輸出服務生成PDF文檔。

   調用 `OutputServiceClient` 對象 `generatePDFOutput2` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定附加資源（如影像）所在的內容根。
   * A `BLOB` 表示窗體設計的對象(使用 `BLOB` 匯編程式服務返回的實例)。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `BLOB` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。
   * 輸出 `BLOB` 對象 `generatePDFOutput2` 方法填充。 的 `generatePDFOutput2` 方法使用描述文檔的生成元資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * 輸出 `OutputResult` 包含操作結果的對象。 （此參數值僅對於Web服務調用是必需的）。

   的 `generatePDFOutput2` 方法返回 `BLOB` 包含非互動式PDF窗體的對象。

1. 將PDF文檔另存為PDF檔案。

   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示互動式PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 從 `generatePDFOutput2` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 打印到檔案 {#printing-to-files}

可以使用輸出服務將流(如PostScript、打印機控制語言(PCL))或以下標籤格式打印到檔案：

* 斑馬 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用「輸出」服務，可以將XML資料與表單設計合併，並將表單打印到檔案。 下圖顯示了Output服務建立雷射和標籤檔案。

>[!NOTE]
>
>有關將打印流發送到打印機的資訊，請參見 [將打印流發送到打印機](creating-document-output-streams.md#sending-print-streams-to-printers)。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

要打印到檔案，請執行以下步驟：

1. 包括項目檔案。
1. 建立輸出客戶端對象。
1. 引用XML資料源。
1. 設定打印到檔案所需的打印運行時選項。
1. 將打印流打印到檔案。
1. 檢索操作的結果。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援的J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。 (請參閱 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果使用Java API，請建立 `OutputClient` 的雙曲餘切值。 如果使用Output Web服務API，請建立 `OutputServiceService` 的雙曲餘切值。

**引用XML資料源**

要打印包含資料的文檔，必須為要用資料填充的每個表單域引用包含XML元素的XML資料源。 XML元素名稱必須與欄位名稱匹配。 如果XML元素與表單域不對應，或XML元素名稱與欄位名稱不匹配，則忽略該元素。 如果指定了所有XML元素，則不必與XML元素的顯示順序匹配。

**設定打印到檔案所需的打印運行時選項**

要打印到檔案，必須通過指定輸出服務打印到的檔案的位置和名稱來設定檔案URI運行時選項。 例如，指示輸出服務打印名為 *MortgageForm.ps* 至C:\Adobe，指定C:\Adobe\MortgageForm.ps。

>[!NOTE]
>
>您可以定義可選的運行時選項。 有關可設定的所有選項的資訊，請參閱 `PrintedOutputOptionsSpec` 類引用 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**將打印流打印到檔案**

引用包含表單資料的有效XML資料源並設定打印運行時選項後，可以調用輸出服務，使其打印檔案。

**檢索操作的結果**

在輸出服務執行操作後，它返回指定操作是否成功的各種資料項，如XML資料。

**另請參閱**

[使用Java API打印到檔案](creating-document-output-streams.md#print-to-files-using-the-java-api)

[使用Web服務API打印到檔案](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API打印到檔案 {#print-to-files-using-the-java-api}

使用輸出API(Java)打印到檔案：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用XML資料源。

   * 建立 `java.io.FileInputStream` 表示XML資料源的對象，該XML資料源用於使用文檔的建構子並傳遞一個字串值來指定XML檔案的位置來填充文檔。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定打印到檔案所需的打印運行時選項。

   * 建立 `PrintedOutputOptionsSpec` 對象。
   * 通過調用PrintedOutputOptionsSpec對象的 `setFileURI` 方法，並傳遞一個字串值，該字串值表示檔案的名稱和位置。 例如，如果希望輸出服務打印到C:\Adobe中名為MortgageForm.ps的PostScript檔案，請指定C:\\Adobe\MortgageForm.ps。
   * 通過調用 `PrintedOutputOptionsSpec` 對象 `setCopies` 方法並傳遞一個表示副本數的整數值。

1. 將打印流打印到檔案。

   通過調用 `OutputClient` 對象 `generatePrintedOutput` 方法並傳遞以下值：

   * A `PrintFormat` 指定要建立的打印流格式的枚舉值。 例如，要建立PostScript打印流，請傳遞 `PrintFormat.PostScript`。
   * 一個字串值，它指定窗體設計的名稱。
   * 一個字串值，它指定相關輔助檔案（如影像檔案）的位置。
   * 一個字串值，它指定要使用的XDC檔案的位置(您可以傳遞 `null` 如果指定了XDC檔案，則 `PrintedOutputOptionsSpec` 對象)。
   * 的 `PrintedOutputOptionsSpec` 包含打印到檔案所需的運行時選項的對象。
   * 的 `com.adobe.idp.Document` 包含包含表單資料的XML資料源的對象。

   的 `generatePrintedOutput` 方法返回 `OutputResult` 包含操作結果的對象。

   >[!NOTE]
   >
   >的 `OutputResult` 對象 `getRecordLevelMetaDataList` 方法返回 `null`。

1. 檢索操作的結果。

   * 建立 `com.adobe.idp.Document` 表示 `generatePrintedOutput` 方法 `OutputResult` 對象 `getStatusDoc` 方法( `OutputResult` 對象由 `generatePrintedOutput` )。
   * 建立 `java.io.File` 包含操作結果的對象。 確保檔案副檔名為XML。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象到檔案(確保 `com.adobe.idp.Document` 返回的對象 `getStatusDoc` )。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API打印到檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服務API打印到檔案 {#print-to-files-using-the-web-service-api}

使用輸出API（Web服務）打印到檔案：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立輸出客戶端對象。

   * 建立 `OutputServiceClient` 對象。
   * 建立 `OutputServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `OutputServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML資料源。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存表單資料。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值指定包含表單資料的XML檔案的位置。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `binaryData` 屬性。

1. 設定打印到檔案所需的打印運行時選項。

   * 建立 `PrintedOutputOptionsSpec` 對象。
   * 通過為指定一個字串值來指定檔案，該字串值表示檔案的位置和名稱 `PrintedOutputOptionsSpec` 對象 `fileURI` 資料成員。 例如，如果希望輸出服務打印到名為 *MortgageForm.ps* 位於C:\Adobe中，指定C:\\Adobe\MortgageForm.ps。
   * 指定要打印的副本數，方法是為 `PrintedOutputOptionsSpec` 對象 `copies` 資料成員。

1. 將打印流打印到檔案。

   通過調用 `OutputServiceService` 對象 `generatePrintedOutput` 方法並傳遞以下值：

   * A `PrintFormat` 指定要建立的打印流格式的枚舉值。 例如，要建立PostScript打印流，請傳遞 `PrintFormat.PostScript`。
   * 一個字串值，它指定窗體設計的名稱。
   * 一個字串值，它指定相關輔助檔案（如影像檔案）的位置。
   * 一個字串值，它指定要使用的XDC檔案的位置(您可以傳遞 `null` 如果指定了XDC檔案，則 `PrintedOutputOptionsSpec` 對象)。
   * 的 `PrintedOutputOptionsSpec` 包含打印到檔案所需的打印運行時選項的對象。
   * 的 `BLOB` 包含包含表單資料的XML資料源的對象。
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用描述文檔的生成元資料填充此對象。 （僅Web服務調用需要此參數值。）
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用結果資料填充此對象。 （僅Web服務調用需要此參數值。）
   * 安 `OutputResult` 包含操作結果的對象。 （僅Web服務調用需要此參數值。）

1. 檢索操作的結果。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 確保檔案副檔名為XML。
   * 建立一個位元組陣列，用於儲存 `BLOB` 用結果資料填充的對象 `OutputServiceService` 對象 `generatePDFOutput` 方法（第八個參數）。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將打印流發送到打印機 {#sending-print-streams-to-printers}

可以使用輸出服務將打印流(如PostScript、打印機控制語言(PCL))或以下標籤格式發送到網路打印機：

* 斑馬 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用「輸出」服務，可以將XML資料與表單設計合併，並將表單輸出為打印流。 例如，您可以建立PostScript打印流並將其發送到網路打印機。 下圖顯示了將打印流發送到網路打印機的輸出服務。

>[!NOTE]
>
>為了演示如何將打印流發送到網路打印機，本節使用SharedPrinter打印機協定將PostScript打印流發送到網路打印機。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

要將打印流發送到網路打印機，請執行以下步驟：

1. 包括項目檔案。
1. 建立輸出客戶端對象。
1. 引用XML資料源。
1. 設定打印運行時選項
1. 檢索要打印的文檔。
1. 將文檔發送到網路打印機。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援的J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，請建立輸出服務客戶端對象。 如果使用Java API，請建立 `OutputClient` 的雙曲餘切值。 如果使用Output Web服務API，請建立 `OutputServiceClient` 的雙曲餘切值。

**引用XML資料源**

要打印包含資料的文檔，必須為要用資料填充的每個表單域引用包含XML元素的XML資料源。 XML元素名稱必須與欄位名稱匹配。 如果XML元素與表單域不對應，或XML元素名稱與欄位名稱不匹配，則忽略該元素。 如果指定了所有XML元素，則不必與XML元素的顯示順序匹配。

**設定打印運行時選項**

將打印流發送到打印機時，可以設定運行時選項，包括以下選項：

* **副本**:指定要發送到打印機的副本數。 預設值為 1。
* **裝訂**:使用訂書機時設定XCI選項。 此選項可在配置模型中由訂書釘元素指定，僅用於PS和PCL打印機。
* **輸出角拐**:當應對輸出頁進行合頁（在輸出托盤中物理移動）時，將設定XCI選項。 此選項僅用於PS和PCL打印機。
* **輸出站**:用於使打印驅動程式選擇相應輸出站的XCI值。

>[!NOTE]
>
>有關可設定的所有運行時選項的資訊，請參閱 `PrintedOutputOptionsSpec` 類引用。

**檢索要打印的文檔**

檢索要發送到打印機的打印流。 例如，可以檢索PostScript檔案並將其發送到打印機。

如果打印機支援PDF，則可以選擇發送PDF檔案。 但是，向打印機發送PDF文檔的問題是每個打印機製造商都有不同的PDF解釋器實現。 就是有的印刷廠用Adobe PDF的解譯，但是它要看打印機。 其他打印機有自己的PDF解釋器。 因此，打印結果可能會有所不同。

將PDF文檔發送到打印機的另一個限制是它只打印；除通過打印機上的設定外，它無法訪問雙工、紙盒選擇和裝訂。

要檢索要打印的文檔，請使用 `generatePrintedOutput` 的雙曲餘切值。 下表指定了使用 `generatePrintedOutput` 的雙曲餘切值。

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
   <td><p>預設情況下建立dpl203.xdc或自定義xdc輸出流。</p></td>
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
   <td><p>通用顏色PCL </p></td>
   <td><p>建立通用顏色PCL(5c)輸出流。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>建立通用PostScript第3級輸出流。</p></td>
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
   <td><p>建立通用PostScript第2級輸出流。</p></td>
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
>您還可以使用 `generatePrintedOutput2` 的雙曲餘切值。 但是，與「將打印流發送到打印機」部分關聯的快速開始使用 `generatePrintedOutput` 的雙曲餘切值。

**將打印流發送到網路打印機**

檢索要打印的文檔後，可以調用輸出服務，使其向網路打印機發送打印流。 要使輸出服務成功找到打印機，必須同時指定打印伺服器和打印機名稱。 此外，還必須指定打印協定。

>[!NOTE]
>
>如果表單伺服器上安裝了PDFG，並且伺服器在Windows Server 2008上運行，則不能使用SharedPrinter屬性。 在這種情況下，請使用其他打印機協定。

>[!NOTE]
>
>如果使用網路打印機，並且訪問機制是SharedPrinter，則需要指定打印機的完整網路路徑。使用Java API將打印流發送到網路打印機

使用Output API(Java)將打印流發送到網路打印機：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar。

1. 建立輸出客戶端對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用XML資料源

   * 建立 `java.io.FileInputStream` 表示XML資料源的對象，該XML資料源用於使用文檔的建構子並傳遞一個字串值來指定XML檔案的位置來填充文檔。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定打印運行時選項

   建立 `PrintedOutputOptionsSpec` 表示打印運行時選項的對象。 例如，可以通過調用 `PrintedOutputOptionsSpec` 對象 `setCopies` 的雙曲餘切值。

   >[!NOTE]
   >
   >不能使用 `PrintedOutputOptionsSpec` 對象 `setPagination` 的子菜單。 同樣，您不能為ZPL打印流設定以下選項：OutputJog、PageOffset和Staple。 的 `setPagination` 方法對於PostScript生成無效。 它僅對PCL生成有效。

1. 檢索要打印的文檔

   * 通過調用 `OutputClient` 對象 `generatePrintedOutput` 方法並傳遞以下值：

      * A `PrintFormat` 指定打印流的枚舉值。 例如，要建立PostScript打印流，請傳遞 `PrintFormat.PostScript`。
      * 一個字串值，它指定窗體設計的名稱。
      * 一個字串值，它指定相關輔助檔案（如影像檔案）的位置。
      * 一個字串值，它指定要使用的XDC檔案的位置。
      * 的 `PrintedOutputOptionsSpec` 包含打印到檔案所需的運行時選項的對象。
      * 的 `com.adobe.idp.Document` 表示包含要與表單設計合併的表單資料的XML資料源的對象。

      此方法返回 `OutputResult` 包含操作結果的對象。

   * 建立 `com.adobe.idp.Document` 通過調用 `OutputResult` 對象s `getGeneratedDoc` 的雙曲餘切值。 此方法返回 `com.adobe.idp.Document` 的雙曲餘切值。


1. 將打印流發送到網路打印機

   通過調用 `OutputClient` 對象 `sendToPrinter` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示要發送到打印機的打印流的對象。
   * A `PrinterProtocol` 指定要使用的打印機協定的枚舉值。 例如，要指定SharedPrinter協定，請傳遞 `PrinterProtocol.SharedPrinter`。
   * 指定打印伺服器名稱的字串值。 例如，假定打印伺服器的名稱為PrintSever1，傳遞 `\\\PrintSever1`。
   * 指定打印機名稱的字串值。 例如，假定打印機的名稱為Printer1 ，則傳遞 `\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >的 `sendToPrinter` 方法已添加到8.2.1版中的AEM FormsAPI。

### 使用Web服務API將打印流發送到打印機 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

使用輸出API（Web服務）將打印流發送到網路打印機：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立輸出客戶端對象。

   * 建立 `OutputServiceClient` 對象。
   * 建立 `OutputServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `OutputServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML資料源。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存表單資料。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值指定包含表單資料的XML檔案的位置。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 設定打印運行時選項。

   建立 `PrintedOutputOptionsSpec` 對象。 例如，可以通過為指定一個整數值來指定要打印的副本數，該整數值表示要打印的副本數 `PrintedOutputOptionsSpec` 對象 `copies` 資料成員。

   >[!NOTE]
   >
   >不能使用 `PrintedOutputOptionsSpec` 對象 `pagination` 資料成員。 同樣，您不能為ZPL打印流設定以下選項：OutputJog、PageOffset和Staple。 的 `pagination` 資料成員對PostScript生成無效。 它僅對PCL生成有效。

1. 檢索要打印的文檔。

   * 通過調用 `OutputServiceService` 對象 `generatePrintedOutput` 方法並傳遞以下值：

      * A `PrintFormat` 指定打印流的枚舉值。 例如，要建立PostScript打印流，請傳遞 `PrintFormat.PostScript`。
      * 一個字串值，它指定窗體設計的名稱。
      * 一個字串值，它指定相關輔助檔案（如影像檔案）的位置。
      * 一個字串值，它指定要使用的XDC檔案的位置。
      * 的 `PrintedOutputOptionsSpec` 包含將打印流發送到網路打印機時使用的打印運行時選項的對象。
      * 的 `BLOB` 包含包含表單資料的XML資料源的對象。
      * A `BLOB` 填充的對象 `generatePrintedOutput` 的雙曲餘切值。 的 `generatePrintedOutput` 方法使用描述文檔的生成元資料填充此對象。 （僅Web服務調用需要此參數值。）
      * A `BLOB` 填充的對象 `generatePrintedOutput` 的雙曲餘切值。 的 `generatePrintedOutput` 方法使用結果資料填充此對象。 （僅Web服務調用需要此參數值。）
      * 安 `OutputResult` 包含操作結果的對象。 （僅Web服務調用需要此參數值。）
   * 建立 `BLOB` 通過獲取 `OutputResult` 對象s `generatedDoc` 的雙曲餘切值。 此方法返回 `BLOB` 包含由 `generatePrintedOutput` 的雙曲餘切值。


1. 將打印流發送到網路打印機。

   通過調用 `OutputClient` 對象 `sendToPrinter` 方法並傳遞以下值：

   * A `BLOB` 表示要發送到打印機的打印流的對象。
   * A `PrinterProtocol` 指定要使用的打印機協定的枚舉值。 例如，要指定SharedPrinter協定，請傳遞 `PrinterProtocol.SharedPrinter`。
   * A `bool` 指定是否使用上一個參數值的值。 傳遞值 `true`。 （僅Web服務調用需要此參數值。）
   * 指定打印伺服器名稱的字串值。 例如，假定打印伺服器的名稱為PrintSever1，則傳遞 `\\\PrintSever1`。
   * 指定打印機名稱的字串值。 例如，假定打印機的名稱為Printer1，則傳遞 `\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >的 `sendToPrinter` 方法已添加到8.2.1版中的AEM FormsAPI。

## 建立多個輸出檔案 {#creating-multiple-output-files}

輸出服務可以為XML資料源中的每個記錄或包含所有記錄的單個檔案建立單獨的文檔（此功能是預設功能）。 例如，假定10條記錄位於XML資料源中，並且您通過使用輸出服務API指示輸出服務為每個記錄建立單獨的PDF文檔（或其他類型的輸出）。 因此，輸出服務生成十個PDF文檔。 （您可以將多個打印流發送到打印機，而不是建立文檔。）

下圖還顯示了Output服務處理包含多個記錄的XML資料檔案。 但是，假定您指示輸出服務建立包含所有資料記錄的單個PDF文檔。 在這種情況下，輸出服務將生成一個包含所有記錄的文檔。

下圖顯示了Output服務處理包含多個記錄的XML資料檔案。 假定您指示輸出服務為每個資料記錄建立單獨的PDF文檔。 在這種情況下，輸出服務會為每個資料記錄生成單獨的PDF文檔。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

以下XML資料顯示了包含三個資料記錄的資料檔案的示例。

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

請注意，啟動和結束每個資料記錄的XML元素是 `LoanRecord`。 此XML元素由生成多個檔案的應用程式邏輯引用。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

要基於XML資料源建立多個PDF檔案，請執行以下步驟：

1. 包括項目檔案。
1. 建立輸出客戶端對象。
1. 引用XML資料源。
1. 設定PDF運行時選項。
1. 設定呈現運行時選項。
1. 生成多個PDF檔案。
1. 檢索操作的結果。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援的J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果使用Java API，請建立 `OutputClient` 的雙曲餘切值。 如果使用Output Web服務API，請建立 `OutputServiceService` 的雙曲餘切值。

**引用XML資料源**

引用包含多個記錄的XML資料源。 必須使用XML元素來分隔資料記錄。 例如，在本節前面顯示的示例XML資料源中，分隔資料記錄的XML元素被命名為 `LoanRecord`。

要用資料填充的每個表單域都必須存在XML元素。 XML元素名稱必須與欄位名稱匹配。 如果XML元素與表單域不對應，或XML元素名稱與欄位名稱不匹配，則忽略該元素。 如果指定了所有XML元素，則不必與XML元素的顯示順序匹配。

**設定PDF運行時選項**

必須為輸出服務設定以下運行時選項，才能基於XML資料源成功建立多個檔案：

* **許多檔案**:指定輸出服務是建立單個文檔還是建立多個文檔。 可以指定true或false。 要為XML資料源中的每個資料記錄建立單獨的文檔，請指定true。
* **檔案URI**:指定輸出服務生成的檔案的位置。 例如，假定您指定C:\\Adobe\forms\Loan.pdf。 在這種情況下，輸出服務將建立一個名為Loan.pdf的檔案，並將該檔案放在C:\\Adobe\forms folder目錄中。 當存在多個檔案時，檔案名為Loan0001.pdf、Loan0002.pdf、Loan003.pdf等。 如果指定檔案位置，則檔案將放在伺服器上，而不放在客戶機上。
* **記錄名稱**:指定分隔資料記錄的資料源中的XML元素名稱。 例如，在本節前面顯示的示例XML資料源中，將調用分隔資料記錄的XML元素 `LoanRecord`。 (您不必設定「記錄名」運行時選項，而是可以通過為記錄級別分配一個數值來設定記錄級別，該值指示包含資料記錄的要素級別。 但是，您只能設定「記錄名稱」或「記錄級別」。 不能同時設定這兩個值。)

**設定呈現運行時選項**

可以在建立多個檔案時設定呈現運行時選項。 雖然這些選項不是必需的（與輸出運行時選項不同，它們是必需的），但您可以執行諸如提高輸出服務的效能之類的任務。 例如，您可以快取輸出服務使用的表單設計以提高效能。

當輸出服務處理批處理記錄時，它以增量方式讀取包含多個記錄的資料。 即，輸出服務將資料讀入記憶體，並在處理記錄批時釋放資料。 設定兩個運行時選項之一時，輸出服務以增量方式載入資料。 如果設定「記錄名稱」運行時選項，則「輸出」服務將以增量方式讀取資料。 同樣，如果將「記錄級別」運行時選項設定為2或更大，則「輸出」服務將以增量方式讀取資料。

您可以使用 `PDFOutputOptionsSpec` 或 `PrintedOutputOptionSpec` 對象 `setLazyLoading` 的雙曲餘切值。 您可以傳遞值 `false` 關閉增量載入的方法。

**生成多個PDF檔案**

在引用包含多個資料記錄和設定運行時選項的有效XML資料源後，可以調用輸出服務，使其生成多個檔案。 生成多個記錄時， `OutputResult` 對象 `getGeneratedDoc` 方法返回 `null`。

**檢索操作的結果**

輸出服務執行操作後，它返回指定操作是否成功的XML資料。 輸出服務返回以下XML。 在這種情況下，輸出服務生成了42個文檔。

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

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立多個PDF檔案 {#create-multiple-pdf-files-using-the-java-api}

使用Output API(Java)建立多個PDF檔案：

1. 包括項目檔案」

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar。。

1. 建立輸出客戶端對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用XML資料源

   * 建立 `java.io.FileInputStream` 表示XML資料源的對象，該XML資料源使用其建構子並傳遞一個字串值，該字串值指定XML檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定PDF運行時選項

   * 建立 `PDFOutputOptionsSpec` 對象。
   * 通過調用 `PDFOutputOptionsSpec` 對象 `setGenerateManyFiles` 的雙曲餘切值。 例如，傳遞值 `true` 指示輸出服務為XML資料源中的每個記錄建立單獨的PDF檔案。 (如果通過 `false`，輸出服務將生成包含所有記錄的單個PDF文檔)。
   * 通過調用 `PDFOutputOptionsSpec` 對象 `setFileUri` 方法並傳遞一個字串值，該字串值指定輸出服務生成的檔案的位置。 「檔案URI」選項是相對於承載AEM Forms的J2EE應用程式伺服器，而不是客戶機。
   * 通過調用 `OutputOptionsSpec` 對象 `setRecordName` 方法，並傳遞一個字串值，該字串值指定分隔資料記錄的資料源中的XML元素名稱。 (例如，請考慮本節前面顯示的XML資料源。 分隔資料記錄的XML元素的名稱為LoanRecord)。

1. 設定呈現運行時選項

   * 建立 `RenderOptionsSpec` 對象。
   * 通過調用Cache快取表單設計，提高Output服務的效能 `RenderOptionsSpec` 對象 `setCacheEnabled` 通過 `Boolean` 值 `true`。

1. 生成多個PDF檔案

   通過調用 `OutputClient` 對象 `generatePDFOutput` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定窗體設計的名稱。
   * 一個字串值，它指定窗體設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `com.adobe.idp.Document` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。

   的 `generatePDFOutput` 方法返回 `OutputResult` 包含操作結果的對象。

1. 檢索操作的結果

   * 建立 `java.io.File` 表示將包含XML檔案的 `generatePDFOutput` 的雙曲餘切值。 確保檔案副檔名為.xml。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象到檔案(確保 `com.adobe.idp.Document` 返回的對象 `applyUsageRights` )。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API建立多個PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立多個PDF檔案 {#create-multiple-pdf-files-using-the-web-service-api}

使用Output API（Web服務）建立多個PDF檔案：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立輸出客戶端對象。

   * 建立 `OutputServiceClient` 對象。
   * 建立 `OutputServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `OutputServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML資料源。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存包含多個記錄的表單資料。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示包含多個記錄的XML檔案的檔案位置。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 設定PDF運行時選項。

   * 建立 `PDFOutputOptionsSpec` 對象。
   * 通過為Many Files指定布爾值來設定 `OutputOptionsSpec` 對象 `generateManyFiles` 資料成員。 例如，分配值 `true` 指示輸出服務為XML資料源中的每個記錄建立單獨的PDF檔案。 (如果分配 `false` 到此資料成員，則輸出服務將生成包含所有記錄的單個PDF)。
   * 通過分配一個字串值來設定檔案URI選項，該字串值指定輸出服務生成到的檔案的位置 `OutputOptionsSpec` 對象 `fileURI` 資料成員。 「檔案URI」選項是相對於承載AEM Forms的J2EE應用程式伺服器，而不是客戶機。
   * 通過分配字串值來設定記錄名稱選項，該字串值指定將資料記錄分離到 `OutputOptionsSpec` 對象 `recordName` 資料成員。
   * 通過分配一個整數值來設定副本選項，該整數值指定輸出服務生成的副本數 `OutputOptionsSpec` 對象 `copies` 資料成員。

1. 設定呈現運行時選項。

   * 建立 `RenderOptionsSpec` 對象。
   * 快取表單設計以通過賦值來提高輸出服務的效能 `true` 到 `RenderOptionsSpec` 對象 `cacheEnabled` 資料成員。

1. 生成多個PDF檔案。

   通過調用以建立多個PDF檔案 `OutputServiceService` 對象 `generatePDFOutput`方法並傳遞以下值：

   * TransformationFormat枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定窗體設計的名稱。
   * 一個字串值，它指定窗體設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `BLOB` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用描述文檔的生成元資料填充此對象。
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用結果資料填充此對象。
   * 安 `OutputResult` 包含操作結果的對象。

1. 檢索操作的結果

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 確保檔案副檔名為.xml。
   * 建立一個位元組陣列，用於儲存 `BLOB` 用結果資料填充的對象 `OutputServiceService` 對象 `generatePDFOutput` 方法（第八個參數）。 通過獲取 `BLOB` 對象 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立搜索規則 {#creating-search-rules}

您可以建立搜索規則，使輸出服務檢查輸入資料並使用基於資料內容的不同表單設計來生成輸出。 例如，如果 *抵押* 位於輸入資料中，則輸出服務可以使用名為Mortgage.xdp的表單設計。 同樣，如果 *汽車* 在輸入資料中，則輸出服務可以使用保存為AutomobileLoan.xdp的表單設計。 儘管輸出服務可以生成不同的輸出類型，但本節假定輸出服務生成PDF檔案。 下圖顯示了通過處理XML資料檔案並使用多種表單設計之一生成PDF檔案的輸出服務。

此外，輸出服務能夠生成文檔包，其中在資料集中提供多個記錄，並且每個記錄與表單設計匹配，並且單個文檔由多個表單設計組成。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

要指示輸出服務在生成文檔時使用搜索規則，請執行以下步驟：

1. 包括項目檔案。
1. 建立輸出客戶端對象。
1. 引用XML資料源。
1. 定義搜索規則。
1. 設定PDF運行時選項。
1. 設定呈現運行時選項。
1. 生成PDF文檔。
1. 檢索操作的結果。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援的J2EE應用程式伺服器上，則您需要用特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案替換adobe-utilities.jar和jbossall-client.jar。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。

**引用XML資料源**

要用資料填充的每個表單域都必須存在XML元素。 XML元素名稱必須與欄位名稱匹配。 如果XML元素與表單域不對應，或XML元素名稱與欄位名稱不匹配，則忽略該元素。 只要指定了所有XML元素，就不必與XML元素的顯示順序匹配。

**定義搜索規則**

要定義搜索規則，您可以定義輸出服務在輸入資料中搜索的一個或多個文本模式。 對於您定義的每個文本圖案，可指定相應的表單設計，該設計在文本圖案位於時使用。 如果找到文本模式，則輸出服務使用相應的表單設計來生成輸出。 文本模式的示例是 *抵押*。

>[!NOTE]
>
>如果未找到文本模式，則使用預設表單。 確保您使用的所有窗體設計都位於內容根目錄中。

**設定PDF運行時選項**

設定以下PDF運行時選項，以便輸出服務基於多個表單設計成功建立PDF文檔：

* **檔案URI**:指定輸出服務生成的PDF檔案的名稱和位置。
* **規則**:指定您定義的規則。
* **LookAHead**:指定要從輸入資料檔案開始掃描定義的文本模式時使用的位元組數。 預設值為500位元組。

**設定呈現運行時選項**

可以在建立PDF檔案時設定渲染運行時選項。 雖然這些選項不是必需的(與PDF運行時選項不同)，但您可以執行諸如提高輸出服務效能之類的任務。 例如，您可以快取輸出服務使用的表單設計以提高效能。

**生成PDF文檔**

在引用有效的XML資料源並設定運行時選項後，可以調用輸出服務，從而生成PDF文檔。 如果輸出服務在輸入資料中定位指定的文本模式，則使用相應的表單設計。 如果未使用文本模式，則輸出服務將使用預設的表單設計。

**檢索操作的結果**

輸出服務執行操作後，它返回指定操作是否成功的XML資料。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立搜索規則 {#create-search-rules-using-the-java-api}

使用Output API(Java)建立搜索規則：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用XML資料源。

   * 建立 `java.io.FileInputStream` 表示XML資料源的對象，該XML資料源用於使用PDF文檔的建構子並傳遞一個字串值來指定XML檔案的位置來填充該對象文檔。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 定義搜索規則。

   * 建立 `Rule` 對象。
   * 通過調用 `Rule` 對象 `setPattern` 方法並傳遞指定文本模式的字串值。
   * 通過調用 `Rule` 對象 `setForm` 的雙曲餘切值。 傳遞一個字串值，指定表單設計的名稱。

   >[!NOTE]
   >
   >對於要定義的每個文本陣列，重複前三個子步驟。

   * 建立 `java.util.List` 對象 `java.util.ArrayList` 建構子。
   * 每個 `Rule` 建立的對象，調用 `java.util.List` 對象 `add` 方法和通過 `Rule` 的雙曲餘切值。


1. 設定PDF運行時選項。

   * 建立 `PDFOutputOptionsSpec` 對象。
   * 指定輸出服務通過調用PDF檔案生成的檔案的名稱和位置 `PDFOutputOptionsSpec` 對象 `setFileURI` 的雙曲餘切值。 傳遞一個字串值，指定PDF檔案的位置。 「檔案URI」選項是相對於承載AEM Forms的J2EE應用程式伺服器，而不是客戶機。
   * 設定通過調用 `PDFOutputOptionsSpec` 對象 `setRules` 的雙曲餘切值。 通過 `java.util.List` 包含 `Rule` 對象。
   * 通過調用 `PDFOutputOptionsSpec` 對象 `setLookAhead` 的雙曲餘切值。 傳遞一個表示位元組數的整數值。

1. 設定呈現運行時選項。

   * 建立 `RenderOptionsSpec` 對象。
   * 通過調用Cache快取表單設計，以提高輸出服務的效能 `RenderOptionsSpec` 對象 `setCacheEnabled` 傳 `true`。

1. 生成PDF文檔。

   通過調用基於多個表單設計的PDF文檔 `OutputClient` 對象 `generatePDFOutput` 方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定預設表單設計的名稱。 即，在未定位文本圖案時使用的窗體設計。
   * 一個字串值，它指定窗體設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `com.adobe.idp.Document` 對象，該對象包含由Output服務搜索的已定義文本模式的表單資料。

   的 `generatePDFOutput` 方法返回 `OutputResult` 包含操作結果的對象。

1. 檢索操作的結果。

   * 建立 `com.adobe.idp.Document` 表示 `generatePDFOutput` 方法 `OutputResult` 對象 `getStatusDoc` 的雙曲餘切值。
   * 建立 `java.io.File` 包含操作結果的對象。 確保檔案副檔名為.xml。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象到檔案(確保 `com.adobe.idp.Document` 返回的對象 `getStatusDoc` )。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API建立搜索規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API建立搜索規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立搜索規則 {#create-search-rules-using-the-web-service-api}

使用Output API（Web服務）建立搜索規則：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立輸出客戶端對象。

   * 建立 `OutputServiceClient` 對象。
   * 建立 `OutputServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `OutputServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML資料源。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存將與PDF文檔合併的資料。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示要加密的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 定義搜索規則。

   * 建立 `Rule` 對象。
   * 通過為指定文本模式的字串值指定文本模式來定義文本模式 `Rule` 對象 `pattern` 資料成員。
   * 通過為指定表單設計的字串值來定義相應的表單設計 `Rule` 對象 `form` 資料成員。

   >[!NOTE]
   >
   >對於要定義的每個文本陣列，重複前三個子步驟。

   * 建立 `MyArrayOf_xsd_anyType` 儲存規則的對象。
   * 分配每個 `Rule` 對象的元素 `MyArrayOf_xsd_anyType` 陣列。 調用 `MyArrayOf_xsd_anyType` 對象 `Add` 方法 `Rule` 的雙曲餘切值。


1. 設定PDF運行時選項

   * 建立 `PDFOutputOptionsSpec` 對象。
   * 通過分配一個字串值來設定檔案URI選項，該字串值指定輸出服務生成到的PDF檔案的位置 `PDFOutputOptionsSpec` 對象 `fileURI` 資料成員。 「檔案URI」選項是相對於承載AEM Forms的J2EE應用程式伺服器，而不是客戶機。
   * 通過分配一個整數值來設定副本選項，該整數值指定輸出服務生成的副本數 `PDFOutputOptionsSpec` 對象 `copies` 資料成員。
   * 設定通過分配 `MyArrayOf_xsd_anyType` 將規則儲存到 `PDFOutputOptionsSpec` 對象 `rules` 資料成員。
   * 通過分配表示要掃描的位元組數的整數值來設定要掃描的已定義文本模式的位元組數 `PDFOutputOptionsSpec` 對象 `lookAhead` 資料方法。

1. 設定呈現運行時選項

   * 建立 `RenderOptionsSpec` 對象。
   * 快取表單設計，通過賦值來提高輸出服務的效能 `true` 到 `RenderOptionsSpec` 對象 `cacheEnabled` 資料成員。

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 對象 `pdfVersion` 成員。 輸出PDF文檔保留Acrobat窗體的PDF版本。 同樣，不能使用 `RenderOptionsSpec` 對象 `taggedPDF` 的下界。

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 對象 `linearizedPDF` 成員。 有關資訊，請參見 [數字簽名PDF文檔](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。

1. 生成PDF文檔

   通過調用PDF `OutputServiceService` 對象 `generatePDFOutput`方法並傳遞以下值：

   * A `TransformationFormat` 枚舉值。 要生成PDF文檔，請指定 `TransformationFormat.PDF`。
   * 一個字串值，它指定窗體設計的名稱。
   * 一個字串值，它指定窗體設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF運行時選項的對象。
   * A `RenderOptionsSpec` 包含呈現運行時選項的對象。
   * 的 `BLOB` 包含XML資料源的對象，該資料源包含要與窗體設計合併的資料。
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用描述文檔的生成元資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * A `BLOB` 填充的對象 `generatePDFOutput` 的雙曲餘切值。 的 `generatePDFOutput` 方法使用結果資料填充此對象。 （此參數值僅對於Web服務調用是必需的）。
   * 安 `OutputResult` 包含操作結果的對象。 （此參數值僅對於Web服務調用是必需的）。

   >[!NOTE]
   >
   >通過調用生成PDF文檔時 `generatePDFOutput` 方法，請注意，您不能將資料與已簽名、已認證或包含使用權限的XFAPDF表單合併。 有關使用權限的資訊，請參見 [將使用權限應用於PDF文檔](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。

1. 檢索操作的結果

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示包含結果資料的XML檔案位置。 確保檔案副檔名為XML。
   * 建立一個位元組陣列，用於儲存 `BLOB` 用結果資料填充的對象 `OutputServiceService` 對象 `generatePDFOutput` 方法（第八個參數）。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 拼合PDF文檔 {#flattening-pdf-documents}

可以使用輸出服務將互動式PDF文檔轉換為非互動式PDF。 互動式PDF文檔允許用戶輸入或修改PDF文檔欄位中的資料。 調用將互動式PDF文檔轉換為非互動式PDF文檔的過程 *平坦*。 當PDF文檔被拼合時，用戶無法修改文檔欄位中的資料。 展平PDF文檔的一個原因是確保資料無法修改。

可以拼合以下類型的PDF文檔：

* 互動式XFAPDF文檔
* AcrobatForms

嘗試拼合非互動式PDF文檔的PDF會導致異常。

>[!NOTE]
>
>有關輸出服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-9}

要將互動式PDF文檔拼合為非互動式PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立輸出客戶端對象。
1. 檢索互動式PDF文檔。
1. 轉換PDF文檔。
1. 將非互動式PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援的J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。 有關所有AEM FormsJAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立輸出客戶端對象**

在以寫程式方式執行輸出服務操作之前，必須建立輸出服務客戶端對象。 如果使用Java API，請建立 `OutputClient` 的雙曲餘切值。 如果使用Output Web服務API，請建立 `OutputServiceService` 的雙曲餘切值。

**檢索互動式PDF文檔**

檢索要轉換為非互動式PDF文檔的互動式PDF文檔。 嘗試轉換非互動式PDF文檔時會導致異常。

**轉換PDF文檔**

檢索互動式PDF文檔後，可將其轉換為非互動式PDF文檔。 輸出服務返回非互動式PDF文檔。

**將非互動式PDF文檔另存為PDF檔案**

可以將非互動式PDF文檔另存為PDF檔案。

**另請參閱**

[使用Java API拼合PDF文檔](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[使用Web服務API拼合PDF文檔](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API拼合PDF文檔 {#flatten-a-pdf-document-using-the-java-api}

使用「輸出API(Java)」將互動式PDF文檔拼合為非互動式PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-output-client.jar。

1. 建立輸出客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `OutputClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索互動式PDF文檔。

   * 建立 `java.io.FileInputStream` 表示要轉換的互動式PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定互動式PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 轉換PDF文檔。

   通過調用互動式PDF文檔將互動式PDF文檔轉換為非互動式 `OutputServiceService` 對象 `transformPDF` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 包含互動式PDF文檔的對象。
   * A `TransformationFormat` 枚舉值。 要生成非互動式PDF文檔，請指定 `TransformationFormat.PDF`。
   * A `PDFARevisionNumber` 指定修訂號的枚舉值。 由於此參數是用於PDF/A文檔，因此可以指定 `null`。
   * 一個字串值，它表示修正數和年份，以冒號分隔。 由於此參數是用於PDF/A文檔，因此可以指定 `null`。
   * A `PDFAConformance` 表示PDF/A一致性級別的枚舉值。 由於此參數是用於PDF/A文檔，因此可以指定 `null`。

   的 `transformPDF` 方法返回 `com.adobe.idp.Document` 包含非互動式PDF文檔的對象。

1. 將非互動式PDF文檔另存為PDF檔案。

   * 建立 `java.io.File` 對象，並確保檔案副檔名為.pdf。
   * 調用 `Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象到檔案(確保 `Document` 返回的對象 `transformPDF` )。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速啟動（EJB模式）:使用Java API轉換PDF文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API轉換PDF文檔](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API拼合PDF文檔 {#flatten-a-pdf-document-using-the-web-service-api}

使用「輸出API（Web服務）」將互動式PDF文檔拼合為非互動式PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立輸出客戶端對象。

   * 建立 `OutputServiceClient` 對象。
   * 建立 `OutputServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `OutputServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 檢索互動式PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存互動式PDF文檔。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示互動式PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 轉換PDF文檔。

   通過調用互動式PDF文檔將互動式PDF文檔轉換為非互動式 `OutputClient` 對象 `transformPDF` 方法並傳遞以下值：

   * A `BLOB` 包含互動式PDF文檔的對象。
   * A `TransformationFormat` 枚舉值。 要生成非互動式PDF文檔，請指定 `TransformationFormat.PDF`。
   * A `PDFARevisionNumber` 指定修訂號的枚舉值。
   * 一個布爾值，它指定 `PDFARevisionNumber` 使用枚舉值。 由於此參數是用於PDF/A文檔，因此可以指定 `false`。
   * 一個字串值，它表示修正數和年份，以冒號分隔。 由於此參數是用於PDF/A文檔，因此可以指定 `null`。
   * A `PDFAConformance` 表示PDF/A一致性級別的枚舉值。
   * 用於指定 `PDFAConformance` 使用枚舉值。 由於此參數是用於PDF/A文檔，因此可以指定 `false`。

   的 `transformPDF` 方法返回 `BLOB` 包含非互動式PDF文檔的對象。

1. 將非互動式PDF文檔另存為PDF檔案。

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示非互動式PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `transformPDF` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
