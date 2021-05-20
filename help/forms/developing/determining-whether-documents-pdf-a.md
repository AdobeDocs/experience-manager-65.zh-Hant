---
title: 確定文檔是否符合PDF/A
seo-title: 確定文檔是否符合PDF/A
description: 使用組合器服務可確定使用Java API和Web服務API的PDF文檔是否與PDF/A相容。
seo-description: 使用組合器服務可確定使用Java API和Web服務API的PDF文檔是否與PDF/A相容。
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2109'
ht-degree: 0%

---

# 確定文檔是否符合PDF/A {#determining-whether-documents-are-pdf-a-compliant}

通過組合器服務，可以確定PDF文檔是否與PDF/A相容。 PDF/A檔案是存檔格式，用於長期保存檔案的內容。 這些字型嵌入到文檔中，並且該檔案被解壓縮。 因此，PDF/A文檔通常比標準PDF文檔大。 此外，PDF/A檔案不包含音訊和視訊內容。

PDF/A-1規範由兩個一致性級別組成，即A和B。這兩個級別之間的主要區別是邏輯結構（輔助功能）支援，對於一致性級別B不是必要的。無論一致性級別如何，PDF/A-1都規定所有字型都嵌入生成的PDF/A文檔中。 目前驗證（和轉換）僅支援PDF/A-1b。

在本討論中，假定使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

在此DDX文檔中，`DocumentInformation`元素指示組合器服務返回有關輸入PDF文檔的資訊。 在`DocumentInformation`元素內，`PDFAValidation`元素指示組合器服務指示輸入的PDF文檔是否與PDF/A相容。

組合器服務返回的資訊指定輸入的PDF文檔在包含`PDFAConformance`元素的XML文檔中是否與PDF/A相容。 如果輸入的PDF文檔與PDF/A相容，`PDFAConformance`元素的`isCompliant`屬性的值為`true`。 如果PDF文檔與PDF/A不相容，`PDFAConformance`元素的`isCompliant`屬性的值為`false`。

>[!NOTE]
>
>由於此節中指定的DDX文檔包含`DocumentInformation`元素，因此組合器服務將返回XML資料而不是PDF文檔。 也就是說，組合器服務不會組合或反匯編PDF文檔；它返回有關XML文檔中輸入的PDF文檔的資訊。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}的摘要

要確定PDF文檔是否與PDF/A相容，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考用來判斷PDF/A相容性的PDF檔案。
1. 設定運行時選項。
1. 檢索有關PDF文檔的資訊。
1. 保存返回的XML文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為AEM Forms所部署之J2EE應用程式伺服器專屬的JAR檔案。 有關所有AEM Forms JAR檔案的位置資訊，請參閱[包含AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

必須引用DDX文檔才能執行組合器服務操作。 要確定輸入的PDF文檔是否與PDF/A相容，請確保DDX文檔包含`DocumentInformation`元素內的`PDFAValidation`元素。 `PDFAValidation`元素指示組合器服務返回指定輸入PDF文檔是否與PDF/A相容的XML文檔。

**參考用於判斷PDF/A相容性的PDF檔案**

必須參考PDF文檔並將其傳遞到組合器服務，以確定PDF文檔是否與PDF/A相容。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。 如需可設定的執行階段選項相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

**檢索有關PDF文檔的資訊**

建立組合器服務客戶端、引用DDX文檔、引用互動式PDF文檔和設定運行時選項後，可以調用`invokeDDX`操作。 由於DDX文檔包含`DocumentInformation`元素，因此組合器服務返回XML資料而不是PDF文檔。

**保存返回的XML文檔**

組合器服務返回的XML文檔指定輸入的PDF文檔是否與PDF/A相容。 例如，如果輸入的PDF文檔與PDF/A不相容，則組合器服務返回包含以下元素的XML文檔：

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

將XML文檔另存為XML檔案，以便可以開啟該檔案並查看結果。

**另請參閱**

[使用Java API確定文檔是否符合PDF/A](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[使用Web服務API確定文檔是否符合PDF/A](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}確定文檔是否與PDF/A相容

使用組合器服務API(Java)確定PDF文檔是否與PDF/A相容：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 參考現有的DDX文檔。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。 要確定PDF文檔是否與PDF/A相容，請確保DDX文檔包含`PDFAValidation`元素內包含的`DocumentInformation`元素。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 參考用來判斷PDF/A相容性的PDF檔案。

   * 使用其建構子並傳遞用於確定PDF/A符合性的PDF檔案的位置，以建立`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞包含PDF檔案的`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。
   * 使用`HashMap`建構子建立用於儲存輸入PDF文檔的`java.util.Map`對象。
   * 調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象中：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的源元素的值匹配。 例如，本節中引入的DDX文檔中的源元素的值為Loan.pdf。
      * 包含輸入PDF文檔的`com.adobe.idp.Document`對象。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法來設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用`AssemblerOptionSpec`對象的`setFailOnError`方法並傳遞`false`。

1. 檢索有關PDF文檔的資訊。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下必需值：

   * 表示要使用的DDX文檔的`com.adobe.idp.Document`對象
   * `java.util.Map`物件，包含用於判斷PDF/A相容性的輸入PDF檔案
   * 指定運行時選項的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`com.adobe.livecycle.assembler.client.AssemblerResult`對象，該對象包含指定輸入PDF文檔是否與PDF/A相容的XML資料。

1. 保存返回的XML文檔。

   要獲取指定輸入PDF文檔是否為PDF/A文檔的XML資料，請執行以下操作：

   * 調用`AssemblerResult`對象的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 對`java.util.Map`對象進行迭代，直到找到結果`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取XML文檔。 確保將XML資料另存為XML檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API（SOAP模式）判斷檔案是否符合PDF](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) /A規範

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}確定文檔是否與PDF/A相容

使用組合器服務API（Web服務）確定PDF文檔是否與PDF/A相容：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立PDF組合器客戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時會使用此屬性。)
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存DDX文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示DDX文檔的檔案位置以及在中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 參考用來判斷PDF/A相容性的PDF檔案。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存輸入的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此集合對象用於儲存PDF文檔。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配表示鍵名的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
   * 將儲存PDF文檔的`BLOB`對象指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象&#39; `Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 為屬於`AssemblerOptionSpec`對象的資料成員分配值，以設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 檢索有關PDF文檔的資訊。

   調用`AssemblerServiceService`對象的`invoke`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象。
   * 包含輸入PDF文檔的`MyMapOf_xsd_string_To_xsd_anyType`對象。 其鍵必須與PDF源檔案的名稱匹配，且其值必須是與輸入PDF檔案對應的`BLOB`對象。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invoke`方法返回一個`AssemblerResult`對象，該對象包含指定輸入PDF文檔是否為PDF/A文檔的XML資料。

1. 保存返回的XML文檔。

   要獲取指定輸入PDF文檔是否為PDF/A文檔的XML資料，請執行以下操作：

   * 訪問`AssemblerResult`對象的`documents`欄位，該欄位是`Map`對象，包含指定輸入PDF文檔是否為PDF/A文檔的XML資料。
   * 逐一查看`Map`對象，以獲取每個結果文檔。 然後，將該陣列成員的值轉換為`BLOB`。
   * 通過訪問其`BLOB`對象的`MTOM`欄位來提取表示XML資料的二進位資料。 此欄位儲存一個位元組陣列，您可將其寫出為XML檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
