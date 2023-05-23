---
title: 確定文檔是否符合PDF/A
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: 使用PDF程式服務可以使用Java API和Web服務API確定PDF文檔是否與A相容。
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
ht-degree: 2%

---

# 確定文檔是否符合PDF/A {#determining-whether-documents-are-pdf-a-compliant}

您可以使用PDF程式服務確定PDF文檔是否與A相容。 PDF/文檔作為存檔格式存在，用於長期保存文檔的內容。 字體內嵌在文件中，檔案未壓縮。因此，PDF/A 文件通常比標準 PDF 文件大。此外，PDF/A 文件不包含音訊和視訊內容。

PDF/A-1規格由兩個一致性級別組成，即A和B。兩個級別之間的主要區別是邏輯結構（可訪問性）支援，這對於一致性級別B來說不是必需的。無論符合級別如何，PDF/A-1都指示所有字型都嵌入到生成的PDF/A文檔中。 此時，驗證（和轉換）中僅支援PDF/A-1b。

在本討論中，假定使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

在此DDX文檔中， `DocumentInformation` 元素指示匯編器服務返回有關輸入PDF文檔的資訊。 在 `DocumentInformation` 元素 `PDFAValidation` 元素指示匯編器服務指示輸入PDF文檔是否符合PDF/A。

匯編器服務返回資訊，該資訊指定輸入PDF文檔在包含PDF的XML文檔中是否與匯編/A相容 `PDFAConformance` 的子菜單。 如果輸入PDF文檔符合PDF/A，則 `PDFAConformance` 元素 `isCompliant` 屬性 `true`。 如果PDF文檔不符合PDF/A，則 `PDFAConformance` 元素 `isCompliant` 屬性 `false`。

>[!NOTE]
>
>因為在本節中指定的DDX文檔包含 `DocumentInformation` 元素，匯編器服務將返回XML資料，而不是PDF文檔。 即匯編服務不匯編或拆解PDF文檔；它返回有關XML文檔中輸入PDF文檔的資訊。

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要確定PDF文檔是否符合PDF/A，請執行以下任務：

1. 包括項目檔案。
1. 建立PDF匯編器客戶端。
1. 引用現有DDX文檔。
1. 引用用於確定PDF/符合性的PDF文檔。
1. 設定運行時選項。
1. 檢索有關PDF文檔的資訊。
1. 保存返回的XML文檔。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援的J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於AEM Forms部署在其上的J2EE應用程式伺服器的JAR檔案。 有關所有AEM FormsJAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF匯編器客戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**引用現有DDX文檔**

必須引用DDX文檔才能執行匯編程式服務操作。 要確定輸入PDF文檔是否符合PDF/A，請確保DDX文檔包含 `PDFAValidation` 元素 `DocumentInformation` 的子菜單。 的 `PDFAValidation` 元素指示匯編器服務返回XML文檔，該文檔指定輸入PDF文檔是否與PDF/A相容。

**引用用於確定PDF/符合性的PDF文檔**

必須引用PDF文檔並將其傳遞給匯編器服務，以確定PDF文檔是否符合PDF/A。

**設定運行時選項**

您可以設定運行時選項，這些選項在匯編程式服務執行作業時控制其行為。 例如，您可以設定一個選項，指示匯編程式服務在遇到錯誤時繼續處理作業。 有關可設定的運行時選項的資訊，請參見 `AssemblerOptionSpec` 類引用 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**檢索有關PDF文檔的資訊**

在建立匯編器服務客戶端、引用DDX文檔、引用互動式PDF文檔和設定運行時選項後，可以調用 `invokeDDX` 的下界。 因為DDX文檔包含 `DocumentInformation` 元素，匯編器服務將返回XML資料，而不是PDF文檔。

**保存返回的XML文檔**

匯編器服務返回的XML文檔指定輸入PDF文檔是否與PDF/A相容。 例如，如果輸入PDF文檔不符合PDF/A，則匯編器服務將返回包含以下元素的XML文檔：

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

將XML文檔另存為XML檔案，以便開啟檔案並查看結果。

**另請參閱**

[使用Java API確定文檔是否符合PDF/A標準](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[使用Web服務API確定文檔是否符合PDF/A標準](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API確定文檔是否符合PDF/A標準 {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

使用PDF程式服務API(Java)確定PDF文檔是否符合/A:

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用現有DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定DDX檔案的位置。 要確定PDF文檔是否符合PDF/A，請確保DDX文檔包含 `PDFAValidation` 包含在 `DocumentInformation` 的子菜單。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 引用用於確定PDF/符合性的PDF文檔。

   * 建立 `java.io.FileInputStream` 使用其建構子並傳遞用於確定PDF/符合性的PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 包含PDF文檔的對象。
   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象 `HashMap` 建構子。
   * 向 `java.util.Map` 通過調用對象 `put` 方法並傳遞以下參數：

      * 表示鍵名稱的字串值。 此值必須與DDX文檔中指定的源元素的值匹配。 例如，本節介紹的DDX文檔中的源元素的值為Loan.pdf。
      * A `com.adobe.idp.Document` 包含輸入PDF文檔的對象。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過調用屬於的方法來設定運行時選項以滿足業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 對象 `setFailOnError` 方法 `false`。

1. 檢索有關PDF文檔的資訊。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下所需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含用於確定PDF/符合性的輸入PDF檔案的對象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含XML資料的對象，該資料指定輸入PDF文檔是否與PDF/A相容。

1. 保存返回的XML文檔。

   要獲取指定輸入PDF文檔是否是PDF/A文檔的XML資料，請執行以下操作：

   * 調用 `AssemblerResult` 對象 `getDocuments` 的雙曲餘切值。 這返回 `java.util.Map` 的雙曲餘切值。
   * 迭代 `java.util.Map` 直到找到結果 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取XML文檔。 確保將XML資料另存為XML檔案。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API確定文檔是否PDF/A相容](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) （SOAP模式）

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API確定文檔是否符合PDF/A標準 {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

通過使用匯編器服務API（Web服務）確定PDF文檔是否符合PDF/A:

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立PDF匯編器客戶端。

   * 建立 `AssemblerServiceClient` 對象。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `AssemblerServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用現有DDX文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存DDX文檔。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值（該字串值表示DDX文檔的檔案位置和開啟檔案的模式）來對對象。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 引用用於確定PDF/符合性的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存輸入PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 此集合對象用於儲存PDF文檔。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。
   * 為指定表示鍵名的字串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `key` 的子菜單。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
   * 分配 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `value` 的子菜單。
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 調用 `MyMapOf_xsd_string_To_xsd_anyType` 對象 `Add` 方法和通過 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過將值分配給屬於的資料成員來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編程式服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 對象 `failOnError` 資料成員。

1. 檢索有關PDF文檔的資訊。

   調用 `AssemblerServiceService` 對象 `invoke` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象。
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含輸入PDF文檔的對象。 其鍵必須與PDF源檔案的名稱匹配，其值必須為 `BLOB` 與輸入PDF檔案對應的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   的 `invoke` 方法返回 `AssemblerResult` 包含XML資料的對象，該資料指定輸入PDF文檔是否是PDF/A文檔。

1. 保存返回的XML文檔。

   要獲取指定輸入PDF文檔是否是PDF/A文檔的XML資料，請執行以下操作：

   * 訪問 `AssemblerResult` 對象 `documents` 欄位， `Map` 包含XML資料的對象，該XML資料指定輸入PDF文檔是否是PDF/A文檔。
   * 迭代 `Map` 對象，以獲取每個結果文檔。 然後，將該陣列成員的值轉換為 `BLOB`。
   * 通過訪問XML資料提取表示XML資料的二進位資料 `BLOB` 對象 `MTOM` 的子菜單。 此欄位儲存可以作為XML檔案寫入的位元組陣列。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
