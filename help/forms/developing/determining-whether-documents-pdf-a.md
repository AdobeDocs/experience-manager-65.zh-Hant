---
title: 判斷檔案是否與PDF/A相容
seo-title: 判斷檔案是否與PDF/A相容
description: 'null'
seo-description: 'null'
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 判斷檔案是否與PDF/A相容 {#determining-whether-documents-are-pdf-a-compliant}

您可以使用Assembler服務來判斷PDF檔案是否與PDF/A相容。 PDF/A檔案以封存格式存在，以長期保存檔案的內容。 字型會內嵌在檔案中，檔案會解壓縮。 因此，PDF/A檔案通常比標準PDF檔案大。 此外，PDF/A檔案不包含音訊和視訊內容。

PDF/A-1規格包含兩個符合等級，即A和B。兩個級別之間的主要區別是邏輯結構（可訪問性）支援，這是符合性級別B不需要的。無論符合程度如何，PDF/A-1都規定所有字型都內嵌在產生的PDF/A檔案中。 目前，驗證（和轉換）只支援PDF/A-1b。

在本討論中，假設使用了以下DDX文檔。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

在此DDX文檔中，元素 `DocumentInformation` 指示Assembler服務返回有關輸入PDF文檔的資訊。 在元 `DocumentInformation` 素中，元 `PDFAValidation` 素會指示Assembler服務指出輸入的PDF檔案是否與PDF/A相容。

Assembler服務返回指定輸入的PDF文檔在包含元素的XML文檔中是否與PDF/A相容的 `PDFAConformance` 資訊。 如果輸入的PDF檔案與PDF/A相容，元素 `PDFAConformance` 屬性的 `isCompliant` 值就是 `true`。 如果PDF檔案不符合PDF/A規範，元素 `PDFAConformance` 屬性的 `isCompliant` 值就是 `false`。

>[!NOTE]
>
>由於本節中指定的DDX文檔包含元 `DocumentInformation` 素，因此Assembler服務會傳回XML資料，而非PDF文檔。 即Assembler服務不匯編或反匯編PDF文檔；它會傳回有關XML檔案中輸入PDF檔案的資訊。

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參 [閱Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

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
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如果AEM Forms部署在JBoss以外的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為JAR檔案，而AEM Forms部署在該J2EE應用程式伺服器上。 如需所有AEM Forms JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須引用DDX文檔才能執行Assembler服務操作。 若要判斷輸入的PDF檔案是否與PDF/A相容，請確定DDX檔案包含元 `PDFAValidation` 素中的元 `DocumentInformation` 素。 元 `PDFAValidation` 素指示Assembler服務返回指定輸入PDF文檔是否與PDF/A相容的XML文檔。

**參考用來判斷PDF/A相容性的PDF檔案**

必須參考PDF檔案並將其傳遞至Assembler服務，以判斷PDF檔案是否與PDF/A相容。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。 如需您可設定之執行時期選項的詳細資訊，請參閱 `AssemblerOptionSpec`[AEM Forms API參考中的類別參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**擷取PDF檔案的相關資訊**

建立Assembler服務客戶端後，請參考DDX文檔、參考互動式PDF文檔並設定運行時選項，您可以調用該操 `invokeDDX` 作。 由於DDX文檔包含該元 `DocumentInformation` 素，因此Assembler服務會傳回XML資料，而非PDF檔案。

**儲存傳回的XML檔案**

Assembler服務返回的XML文檔指定輸入的PDF文檔是否與PDF/A相容。 例如，如果輸入的PDF檔案與PDF/A不相容，Assembler服務會傳回包含下列元素的XML檔案：

```as3
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

將XML檔案儲存為XML檔案，以便開啟檔案並檢視結果。

**另請參閱**

[使用Java API判斷檔案是否與PDF/A相容](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[使用web service API判斷檔案是否符合PDF/A規範](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API判斷檔案是否與PDF/A相容 {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

使用Assembler Service API(Java)判斷PDF檔案是否與PDF/A相容：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `AssemblerServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考現有的DDX檔案。

   * 使用 `java.io.FileInputStream` 其建構子並傳遞指定DDX檔案位置的字串值，建立表示DDX文檔的對象。 若要判斷PDF檔案是否與PDF/A相容，請確定DDX檔案包含元 `PDFAValidation` 素內的元 `DocumentInformation` 素。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 參考用來判斷PDF/A相容性的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞用來判斷PDF/A相容性之PDF檔案的位置，以建立物件。
   * 使用 `com.adobe.idp.Document` 其建構函式並傳遞包含PDF文 `java.io.FileInputStream` 件的物件，以建立物件。
   * 使用 `java.util.Map` 建構函式建立用來儲存輸入PDF檔案的物 `HashMap` 件。
   * 通過調用對象的方 `java.util.Map` 法並傳遞以 `put` 下參數，向對象添加條目：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的源元素的值匹配。 例如，本節中引入的DDX檔案中的來源元素值為Loan.pdf。
      * 包 `com.adobe.idp.Document` 含輸入PDF檔案的物件。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 調用屬於該對象的方法，以設定運行時選項以滿足您的業務 `AssemblerOptionSpec` 要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用 `AssemblerOptionSpec` 物件的方 `setFailOnError` 法並傳遞 `false`。

1. 擷取PDF檔案的相關資訊。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列必要值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文檔的對象
   * 包 `java.util.Map` 含輸入PDF檔案的物件，用於判斷PDF/A相容性
   * 指 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 定運行時選項的對象
   此方 `invokeDDX` 法會傳回包 `com.adobe.livecycle.assembler.client.AssemblerResult` 含XML資料的物件，指定輸入的PDF檔案是否與PDF/A相容。

1. 儲存傳回的XML檔案。

   若要取得指定輸入PDF檔案是否為PDF/A檔案的XML資料，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的方 `getDocuments` 法。 這會傳回 `java.util.Map` 物件。
   * 重複該對 `java.util.Map` 像，直到找到結果對 `com.adobe.idp.Document` 像。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法以擷取XML檔案。 確保將XML資料儲存為XML檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) （SOAP模式）判斷檔案是否與PDF/A相容

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API判斷檔案是否符合PDF/A規範 {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

使用Assembler Service API(web service)確定PDF檔案是否與PDF/A相容：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立PDF匯寫程式式用戶端。

   * 使用其 `AssemblerServiceClient` 預設建構函式建立物件。
   * 使用建 `AssemblerServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `AssemblerServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存DDX文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示DDX文檔的檔案位置以及在中開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 參考用來判斷PDF/A相容性的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 物件 `BLOB` 用來儲存輸入的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。
   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 此收集物件用來儲存PDF檔案。
   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType_Item` 像。
   * 為對象欄位指定代表鍵名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字串 `key` 值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
   * 將存 `BLOB` 儲PDF文檔的對象指 `MyMapOf_xsd_string_To_xsd_anyType_Item` 派到對 `value` 像欄位。
   * 將對象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 添加到對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 調用對 `MyMapOf_xsd_string_To_xsd_anyType` 像的方 `Add` 法並傳遞對 `MyMapOf_xsd_string_To_xsd_anyType` 像。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 通過為屬於該對象的資料成員分配值，設定運行時選項以滿足您的業務需 `AssemblerOptionSpec` 求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請指 `false` 派給 `AssemblerOptionSpec` 物件的資料 `failOnError` 成員。

1. 擷取PDF檔案的相關資訊。

   叫用物 `AssemblerServiceService` 件的方 `invoke` 法並傳遞下列值：

   * 表 `BLOB` 示DDX文檔的對象。
   * 包 `MyMapOf_xsd_string_To_xsd_anyType` 含輸入PDF檔案的物件。 其鍵必須與PDF源檔案的名稱匹配，其值必須是與輸 `BLOB` 入的PDF檔案對應的對象。
   * 指定 `AssemblerOptionSpec` 運行時選項的對象。
   此方 `invoke` 法傳回包 `AssemblerResult` 含XML資料的物件，指定輸入的PDF檔案是否為PDF/A檔案。

1. 儲存傳回的XML檔案。

   若要取得指定輸入PDF檔案是否為PDF/A檔案的XML資料，請執行下列動作：

   * 存取物 `AssemblerResult` 件的欄 `documents` 位，此物件是包含XML資料的 `Map` 物件，指定輸入的PDF檔案是否為PDF/A檔案。
   * 重複該對 `Map` 像，以獲得每個結果文檔。 然後，將該陣列成員的值轉換為 `BLOB`。
   * 存取XML資料物件的欄位，以擷取代表XML資 `BLOB` 料的二進位 `MTOM` 資料。 此欄位儲存可以寫出為XML檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
