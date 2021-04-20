---
title: 判斷檔案是否與PDF/A相容
seo-title: 判斷檔案是否與PDF/A相容
description: 使用Assembler服務，使用Java API和Web Service API來判斷PDF檔案是否與PDF/A相容。
seo-description: 使用Assembler服務，使用Java API和Web Service API來判斷PDF檔案是否與PDF/A相容。
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 0%

---


# 確定文檔是否與PDF/A相容{#determining-whether-documents-are-pdf-a-compliant}

您可以使用Assembler服務來判斷PDF檔案是否與PDF/A相容。 PDF/A檔案以封存格式存在，以長期保存檔案的內容。 字型會內嵌在檔案中，檔案會解壓縮。 因此，PDF/A檔案通常比標準PDF檔案大。 此外，PDF/A檔案不包含音訊和視訊內容。

PDF/A-1規格包含兩個符合等級，即A和B。兩個級別之間的主要區別是邏輯結構（可訪問性）支援，這是符合性級別B不需要的。無論符合程度如何，PDF/A-1都規定所有字型都內嵌在產生的PDF/A檔案中。 目前，驗證（和轉換）只支援PDF/A-1b。

在本討論中，假設使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

在此DDX文檔中，`DocumentInformation`元素指示Assembler服務返回有關輸入PDF文檔的資訊。 在`DocumentInformation`元素中，`PDFAValidation`元素指示Assembler服務指示輸入的PDF文檔是否與PDF/A相容。

Assembler服務返回指定輸入的PDF文檔在包含`PDFAConformance`元素的XML文檔中是否與PDF/A相容的資訊。 如果輸入的PDF檔案與PDF/A相容，則`PDFAConformance`元素的`isCompliant`屬性值為`true`。 如果PDF檔案不符合PDF/A規範，則`PDFAConformance`元素的`isCompliant`屬性值為`false`。

>[!NOTE]
>
>由於本節中指定的DDX文檔包含`DocumentInformation`元素，因此Assembler服務會返回XML資料，而不是PDF文檔。 即Assembler服務不匯編或反匯編PDF文檔；它會傳回有關XML檔案中輸入PDF檔案的資訊。

>[!NOTE]
>
>有關Assembler服務的詳細資訊，請參見[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}摘要

若要判斷PDF檔案是否與PDF/A相容，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考用來判斷PDF/A相容性的PDF檔案。
1. 設定執行時期選項。
1. 擷取PDF檔案的相關資訊。
1. 儲存傳回的XML檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為AEM Forms部署在的J2EE應用程式伺服器專用的JAR檔案。 有關所有AEM FormsJAR檔案的位置資訊，請參見[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須引用DDX文檔才能執行Assembler服務操作。 若要判斷輸入的PDF檔案是否與PDF/A相容，請確定DDX檔案包含`DocumentInformation`元素中的`PDFAValidation`元素。 `PDFAValidation`元素指示Assembler服務返回指定輸入PDF文檔是否與PDF/A相容的XML文檔。

**參考用來判斷PDF/A相容性的PDF檔案**

必須參考PDF檔案並將其傳遞至Assembler服務，以判斷PDF檔案是否與PDF/A相容。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。 有關可設定的運行時選項的資訊，請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類參考。

**擷取PDF檔案的相關資訊**

建立Assembler服務客戶端後，請參考DDX文檔，參考互動式PDF文檔，並設定運行時選項，您可以調用`invokeDDX`操作。 由於DDX文檔包含`DocumentInformation`元素，因此Assembler服務返回XML資料而不是PDF文檔。

**儲存傳回的XML檔案**

Assembler服務返回的XML文檔指定輸入的PDF文檔是否與PDF/A相容。 例如，如果輸入的PDF檔案與PDF/A不相容，Assembler服務會傳回包含下列元素的XML檔案：

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

將XML檔案儲存為XML檔案，以便開啟檔案並檢視結果。

**另請參閱**

[使用Java API判斷檔案是否與PDF/A相容](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[使用web service API判斷檔案是否符合PDF/A規範](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}判斷檔案是否與PDF/A相容

使用Assembler Service API(Java)判斷PDF檔案是否與PDF/A相容：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 參考現有的DDX檔案。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。 若要判斷PDF檔案是否與PDF/A相容，請確定DDX檔案包含`PDFAValidation`元素，該元素包含在`DocumentInformation`元素中。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 參考用來判斷PDF/A相容性的PDF檔案。

   * 使用其建構函式並傳遞用來判斷PDF/A相容性之PDF檔案的位置，以建立`java.io.FileInputStream`物件。
   * 使用其建構函式並傳遞包含PDF檔案的`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。
   * 使用`HashMap`建構函式建立用來儲存輸入PDF檔案的`java.util.Map`物件。
   * 通過調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的源元素的值匹配。 例如，本節中引入的DDX檔案中的來源元素值為Loan.pdf。
      * 包含輸入PDF文檔的`com.adobe.idp.Document`對象。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法，設定運行時選項以滿足您的業務要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法並傳遞`false`。

1. 擷取PDF檔案的相關資訊。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列必要值：

   * `com.adobe.idp.Document`物件，代表要使用的DDX檔案
   * `java.util.Map`物件，包含用來判斷PDF/A相容性的輸入PDF檔案
   * 指定運行時選項的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象

   `invokeDDX`方法返回包含XML資料的`com.adobe.livecycle.assembler.client.AssemblerResult`對象，該XML資料指定輸入PDF文檔是否與PDF/A相容。

1. 儲存傳回的XML檔案。

   若要取得指定輸入PDF檔案是否為PDF/A檔案的XML資料，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 重複`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取XML檔案。 確保將XML資料儲存為XML檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) （SOAP模式）判斷檔案是否與PDF/A相容

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}判斷檔案是否符合PDF/A規範

使用Assembler Service API(web service)確定PDF檔案是否與PDF/A相容：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存DDX檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 參考用來判斷PDF/A相容性的PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存輸入的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`對象。 此收集物件用來儲存PDF檔案。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配代表鍵名的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
   * 將儲存PDF文檔的`BLOB`對象指定給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`對象添加到`MyMapOf_xsd_string_To_xsd_anyType`對象。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象&#39; `Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的資料成員分配值，設定運行時選項以滿足您的業務要求。 例如，要指示Assembler服務在出現錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 擷取PDF檔案的相關資訊。

   叫用`AssemblerServiceService`物件的`invoke`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象。
   * 包含輸入PDF文檔的`MyMapOf_xsd_string_To_xsd_anyType`對象。 其鍵必須與PDF源檔案的名稱匹配，其值必須是與輸入PDF檔案對應的`BLOB`對象。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invoke`方法返回包含XML資料的`AssemblerResult`對象，該XML資料指定輸入的PDF文檔是否為PDF/A文檔。

1. 儲存傳回的XML檔案。

   若要取得指定輸入PDF檔案是否為PDF/A檔案的XML資料，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是`Map`物件，包含指定輸入PDF檔案是否為PDF/A檔案的XML資料。
   * 重複`Map`物件，以取得每個結果檔案。 然後，將該陣列成員的值轉換為`BLOB`。
   * 通過訪問其`BLOB`對象的`MTOM`欄位，提取表示XML資料的二進位資料。 此欄位儲存可以寫出為XML檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
