---
title: 確定文檔是否符合PDF/A
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: 使用組合器服務來確定PDF文檔是否與使用Java API和Web服務API的PDF/A相容。
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
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
source-wordcount: '2082'
ht-degree: 0%

---

# 確定文檔是否符合PDF/A {#determining-whether-documents-are-pdf-a-compliant}

通過使用組合器服務，可以確定PDF文檔是否PDF/A相容。 PDF/檔案是存檔格式，用於長期保存檔案的內容。 這些字型嵌入到文檔中，並且該檔案被解壓縮。 因此，PDF/A文檔通常比標準PDF文檔大。 此外，PDF/檔案不包含音訊和視訊內容。

PDF/A-1規範由兩個符合級別組成，即A和B。這兩個級別之間的主要差異是邏輯結構（可訪問性）支援，這對於符合級別B不是必需的。無論符合級別如何，PDF/A-1都規定所有字型都嵌入生成的PDF/A文檔中。 目前驗證（和轉換）僅支援PDF/A-1b。

在本討論中，假定使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

在此DDX文檔中， `DocumentInformation` 元素指示組合器服務返回有關輸入PDF文檔的資訊。 在 `DocumentInformation` 元素、 `PDFAValidation` 元素指示組合器服務指示輸入PDF文檔是否PDF/A相容。

組合器服務返回指定輸入PDF文檔在包含的XML文檔中是否PDF/A相容的資訊 `PDFAConformance` 元素。 如果輸入PDF文檔與PDF/A相容，則 `PDFAConformance` 元素 `isCompliant` 屬性為 `true`. 如果PDF文檔不符合PDF/A，則 `PDFAConformance` 元素 `isCompliant` 屬性為 `false`.

>[!NOTE]
>
>因為此部分中指定的DDX文檔包含 `DocumentInformation` 元素，組合器服務返回XML資料而非PDF文檔。 也就是說，組合器服務不會組合或拆解PDF文檔；它返回有關XML文檔中輸入PDF文檔的資訊。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

要確定PDF文檔是否符合PDF/A，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考用於判斷PDF/符合性的PDF檔案。
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

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為AEM Forms所部署之J2EE應用程式伺服器專屬的JAR檔案。 如需所有AEM Forms JAR檔案位置的相關資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

必須引用DDX文檔才能執行組合器服務操作。 要確定輸入PDF文檔是否PDF/A相容，請確保DDX文檔包含 `PDFAValidation` 元素內 `DocumentInformation` 元素。 此 `PDFAValidation` 元素指示組合器服務返回指定輸入PDF文檔是否PDF/A相容的XML文檔。

**參考用於確定PDF/符合性的PDF檔案**

必須引用PDF文檔並將其傳遞到組合器服務，以確定PDF文檔是否與PDF/A相容。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。 如需可設定的執行階段選項相關資訊，請參閱 `AssemblerOptionSpec` 類引用 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**檢索有關PDF文檔的資訊**

建立組合器服務客戶端、引用DDX文檔、引用交互PDF文檔和設定運行時選項後，可以調用 `invokeDDX` 操作。 因為DDX文檔包含 `DocumentInformation` 元素，組合器服務返回XML資料而非PDF文檔。

**保存返回的XML文檔**

組合器服務返回的XML文檔指定輸入PDF文檔是否PDF/A相容。 例如，如果輸入PDF文檔不符合PDF/A，則組合器服務返回包含以下元素的XML文檔：

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

將XML文檔另存為XML檔案，以便可以開啟該檔案並查看結果。

**另請參閱**

[使用Java API確定文檔是否PDF/符合](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[使用Web服務API確定文檔是否PDF/符合](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API確定文檔是否PDF/符合 {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

使用組合器服務API(Java)確定PDF文檔是否PDF/A相容：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞指定DDX檔案位置的字串值。 要確定PDF文檔是否符合PDF/A，請確保DDX文檔包含 `PDFAValidation` 包含在 `DocumentInformation` 元素。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 參考用於判斷PDF/符合性的PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，方法是使用其建構函式並傳遞用於判斷PDF/A符合性的PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。
   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象，方法是使用 `HashMap` 建構子。
   * 將項目新增至 `java.util.Map` 對象 `put` 方法，並傳遞下列引數：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的源元素的值匹配。 例如，本節中引入的DDX文檔中的源元素的值為Loan.pdf。
      * A `com.adobe.idp.Document` 包含輸入PDF文檔的對象。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 通過調用屬於的方法來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 物件 `setFailOnError` 方法和傳遞 `false`.

1. 檢索有關PDF文檔的資訊。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列必要值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含用於確定PDF/符合性的輸入PDF檔案的對象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含XML資料的對象，該資料指定輸入PDF文檔是否PDF/A相容。

1. 保存返回的XML文檔。

   要獲取指定輸入PDF文檔是否為PDF/A文檔的XML資料，請執行以下操作：

   * 叫用 `AssemblerResult` 物件 `getDocuments` 方法。 這會傳回 `java.util.Map` 物件。
   * 重複 `java.util.Map` 對象，直到找到結果 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取XML檔案。 確保將XML資料另存為XML檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API判斷檔案是否PDF/符合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) （SOAP模式）

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API確定文檔是否PDF/符合 {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

使用組合器服務API（Web服務）確定PDF文檔是否PDF/A相容：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立PDF組合器客戶端。

   * 建立 `AssemblerServiceClient` 物件，使用其預設建構函式。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `AssemblerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參考現有的DDX文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存DDX文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置以及在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 參考用於判斷PDF/符合性的PDF檔案。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存輸入PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此集合對象用於儲存PDF文檔。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `key` 欄位。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
   * 指派 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `value` 欄位。
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 為屬於的資料成員指定值，以設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 物件 `failOnError` 資料成員。

1. 檢索有關PDF文檔的資訊。

   叫用 `AssemblerServiceService` 物件 `invoke` 方法，並傳遞下列值：

   * A `BLOB` 表示DDX文檔的對象。
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含輸入PDF文檔的對象。 其鍵必須與PDF源檔案的名稱匹配，且其值必須為 `BLOB` 對應於輸入PDF檔案的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   此 `invoke` 方法傳回 `AssemblerResult` 包含XML資料的對象，該資料指定輸入PDF文檔是否為PDF/A文檔。

1. 保存返回的XML文檔。

   要獲取指定輸入PDF文檔是否為PDF/A文檔的XML資料，請執行以下操作：

   * 存取 `AssemblerResult` 物件 `documents` 欄位，即 `Map` 包含XML資料的對象，該資料指定輸入PDF文檔是否為PDF/A文檔。
   * 重複 `Map` 對象，以獲得每個生成的文檔。 然後，將該陣列成員的值轉換為 `BLOB`.
   * 通過訪問XML資料來提取表示XML資料的二進位資料 `BLOB` 物件 `MTOM` 欄位。 此欄位儲存一個位元組陣列，您可將其寫出為XML檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
