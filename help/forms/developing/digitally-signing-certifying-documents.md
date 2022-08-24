---
title: 數字簽名和驗證文檔
seo-title: Digitally Signing and Certifying Documents
description: 使用簽名服務向PDF文檔添加和刪除數字簽名欄位，檢索位於PDF文檔中的簽名欄位的名稱，修改簽名欄位，對PDF文檔進行數字簽名，驗證PDF文檔，驗證PDF文檔中的數字簽名，驗證PDF文檔中的所有數字簽名，以及從簽名欄位中刪除數字簽名。
seo-description: Use the Signature service to add and delete digital signature fields to a PDF document, retrieve the names of signature fields located in a PDF document, modify signature fields, digitally sign PDF documents, certify PDF documents, validate digital signatures located in a PDF document, validate all digital signatures located in a PDF document, and remove a digital signature from a signature field.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '17046'
ht-degree: 0%

---

# 數字簽名和驗證文檔 {#digitally-signing-and-certifying-documents}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於簽名服務**

簽名服務使您的組織能夠保護其分發和接收的Adobe PDF文檔的安全和隱私。 此服務使用數字簽名和認證來確保只有預期的收件人才能更改文檔。 由於安全功能應用於文檔本身，因此文檔在整個生命週期內都保持安全並受到控制。 文檔在防火牆之外保持安全，在離線下載時，在將其提交回您的組織時。

>[!NOTE]
>
>您可以為簽名服務建立自定義簽名處理程式，該處理程式在調用某些操作時被調用，如對PDF文檔進行簽名。

**簽名欄位名**

某些簽名服務操作要求您指定在其上執行操作的簽名欄位的名稱。 例如，在簽名PDF文檔時，指定要簽名的簽名欄位的名稱。 假設簽名欄位的全名為 `form1[0].Form1[0].SignatureField1[0]`。 可以指定 `SignatureField1[0]` 而不是 `form1[0].Form1[0].SignatureField1[0]`。

有時，衝突會導致簽名服務將錯誤的欄位簽名（或執行另一個需要簽名欄位名稱的操作）。 此衝突是名稱的結果 `SignatureField1[0]` 出現在同一PDF文檔中的兩個或多個位置。 例如，請考慮包含兩個名為的簽名欄位的PDF文檔 `form1[0].Form1[0].SignatureField1[0]` 和 `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` 指定 `SignatureField1[0]`。 在這種情況下，簽名服務在迭代文檔中的所有簽名欄位時，會簽名它找到的第一個簽名欄位。

如果PDF文檔中有多個簽名欄位，建議您指定簽名欄位的全名。 即，指定 `form1[0].Form1[0].SignatureField1[0]`而不是 `SignatureField1[0]`。

您可以使用簽名服務完成以下任務：

* 向PDF文檔添加和刪除數字簽名欄位。 (請參閱 [添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。)
* 檢索位於PDF文檔中的簽名欄位的名稱。 (請參閱 [正在檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)。)
* 修改簽名欄位。 (請參閱 [修改簽名欄位](digitally-signing-certifying-documents.md#modifying-signature-fields)。)
* 對PDF文檔進行數字簽名。 (請參閱 [數字簽名PDF文檔](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)
* 驗證PDF文檔。 (請參閱 [驗證PDF文檔](digitally-signing-certifying-documents.md#certifying-pdf-documents)。)
* 驗證位於PDF文檔中的數字簽名。 (請參閱 [驗證數字簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。)
* 驗證位於PDF文檔中的所有數字簽名。 (請參閱 [驗證多個數字簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。)
* 從簽名欄位中刪除數字簽名。 (請參閱 [刪除數字簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)。)

>[!NOTE]
>
>有關簽名服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)..

## 添加簽名欄位 {#adding-signature-fields}

數字簽名顯示在簽名欄位中，這些欄位是包含簽名的圖形表示的表單域。 簽名欄位可以是可見的或不可見的。 簽名者可以使用預先存在的簽名欄位，或者可以以寫程式方式添加簽名欄位。 在兩種情況下，簽名欄位都必須存在，才能簽名PDF文檔。

可以使用簽名服務Java API或簽名Web服務API以寫程式方式添加簽名欄位。 您可以向一個PDF文檔添加多個簽名欄位；但是，每個簽名欄位名稱必須唯一。

>[!NOTE]
>
>某些PDF文檔類型不允許以寫程式方式添加簽名欄位。 有關簽名服務和添加簽名欄位的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要向PDF文檔添加簽名欄位，請執行以下任務：

1. 包括項目檔案。
1. 建立簽名客戶端。
1. 獲取添加簽名域的PDF文檔。
1. 添加簽名欄位。
1. 將PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取添加簽名域的PDF文檔**

必須獲取添加簽名欄位的PDF文檔。

**添加簽名欄位**

要成功將簽名欄位添加到PDF文檔，請指定標識簽名欄位位置的坐標值。 （如果添加了不可見的簽名欄位，則不需要這些值。） 此外，您還可以指定在將簽名應用到簽名欄位後，PDF文檔中的哪些欄位被鎖定。

**將PDF文檔另存為PDF檔案**

在簽名服務向PDF文檔添加簽名欄位後，您可以將文檔另存為PDF檔案，以便用戶可以在Acrobat或Adobe Reader開啟該文檔。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數字簽名PDF文檔](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API添加簽名欄位 {#add-signature-fields-using-the-java-api}

使用簽名API(Java)添加簽名欄位：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取添加簽名域的PDF文檔

   * 建立 `java.io.FileInputStream` 表示PDF文檔的對象，通過使用其建構子並傳遞一個字串值來添加簽名欄位，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 添加簽名欄位

   * 建立 `PositionRectangle` 使用其建構子指定簽名欄位位置的對象。 在建構子中，指定坐標值。
   * 如果需要，請建立 `FieldMDPOptions` 對象，該對象指定在將數字簽名應用於簽名欄位時鎖定的欄位。
   * 通過調用PDF文檔 `SignatureServiceClient` 對象 `addSignatureField` 方法並傳遞以下值：

      * A `com.adobe.idp`. `Document` 表示添加簽名域的PDF文檔的對象。
      * 一個字串值，它指定簽名欄位的名稱。
      * A `java.lang.Integer` 表示添加簽名欄位的頁碼的值。
      * A `PositionRectangle` 指定簽名欄位位置的對象。
      * A `FieldMDPOptions` 對象，該對象指定在將數字簽名應用到簽名欄位後鎖定的PDF文檔中的欄位。 此參數值是可選的，您可以通過 `null`。
   * A `PDFSeedValueOptions` 指定各種運行時值的對象。 此參數值是可選的，您可以通過 `null`。

      的 `addSignatureField` 方法返回 `com.adobe.idp`。 `Document` 表示包含簽名欄位的PDF文檔的對象。
   >[!NOTE]
   >
   >您可以調用 `SignatureServiceClient` 對象 `addInvisibleSignatureField` 方法，添加不可見簽名欄位。

1. 將PDF文檔另存為PDF檔案

   * 建立 `java.io.File` 並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp`。 `Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象。 確保使用 `com.adobe.idp`。 `Document` 返回的對象 `addSignatureField` 的雙曲餘切值。

**另請參閱**

[簽名服務API快速啟動](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用Web服務API添加簽名欄位 {#add-signature-fields-using-the-web-service-api}

要使用簽名API（Web服務）添加簽名欄位：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 對象。
   * 建立 `SignatureServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `SignatureServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取添加簽名域的PDF文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存將包含簽名欄位的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 添加簽名欄位

   通過調用PDF文檔 `SignatureServiceClient` 對象 `addSignatureField` 方法並傳遞以下值：

   * A `BLOB` 表示添加簽名域的PDF文檔的對象。
   * 指定簽名欄位名稱的字串值。
   * 一個整數值，它表示要向其中添加簽名欄位的頁碼。
   * A `PositionRect` 指定簽名欄位位置的對象。
   * A `FieldMDPOptions` 對象，該對象指定在將數字簽名應用到簽名欄位後鎖定的PDF文檔中的欄位。 此參數值是可選的，您可以通過 `null`。
   * A `PDFSeedValueOptions` 指定各種運行時值的對象。 此參數值是可選的，您可以通過 `null`。

   的 `addSignatureField` 方法返回 `BLOB` 表示包含簽名欄位的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示將包含簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `addSignatureField` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 正在檢索簽名欄位名稱 {#retrieving-signature-field-names}

您可以檢索位於要簽名或認證的PDF文檔中的所有簽名欄位的名稱。 如果您不確定位於PDF文檔中的簽名欄位名稱或要驗證這些名稱，可以以寫程式方式檢索它們。 簽名服務返回簽名欄位的完全限定名稱，如 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

>[!NOTE]
>
>有關簽名服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟摘要 {#summary_of_steps-1}

要檢索簽名域名，請執行以下任務：

1. 包括項目檔案。
1. 建立簽名客戶端。
1. 獲取包含簽名欄位的PDF文檔。
1. 檢索簽名欄位名稱。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取包含簽名欄位的PDF文檔**

檢索包含簽名欄位的PDF文檔。

**檢索簽名欄位名稱**

在檢索包含一個或多個簽名域的PDF文檔後，可以檢索簽名域名。

**另請參閱**

[使用Java API檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用Web服務API檢索簽名欄位](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API檢索簽名欄位名稱 {#retrieve-signature-field-names-using-the-java-api}

使用簽名API(Java)檢索簽名欄位名稱：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案（如adobe-signatures-client.jar）。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取包含簽名欄位的PDF文檔

   * 建立 `java.io.FileInputStream` 表示PDF文檔的對象，該文檔通過使用其建構子並傳遞一個字串值來包含簽名欄位，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 檢索簽名欄位名稱

   * 通過調用 `SignatureServiceClient` 對象 `getSignatureFieldList` 方法和傳遞 `com.adobe.idp.Document` 包含包含簽名欄位的PDF文檔的對象。 此方法返回 `java.util.List` 對象，其中每個元素都包含 `PDFSignatureField` 的雙曲餘切值。 使用此對象，可以獲取有關簽名欄位的其他資訊，如簽名欄位是否可見。
   * 迭代 `java.util.List` 用於確定是否存在簽名欄位名稱的對象。 對於PDF文檔中的每個簽名欄位，可以獲取一個 `PDFSignatureField` 的雙曲餘切值。 要獲取簽名欄位的名稱，請調用 `PDFSignatureField` 對象 `getName` 的雙曲餘切值。 此方法返回一個字串值，該字串值指定簽名欄位名稱。

**另請參閱**

[正在檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速啟動（SOAP模式）:使用Java API檢索簽名欄位名稱](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API檢索簽名欄位 {#retrieve-signature-field-using-the-web-service-api}

使用簽名API（Web服務）檢索簽名欄位名稱：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 對象。
   * 建立 `SignatureServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `SignatureServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取包含簽名欄位的PDF文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存包含簽名欄位的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位位元組陣列內容。

1. 檢索簽名欄位名稱

   * 通過調用來檢索簽名欄位名稱 `SignatureServiceClient` 對象 `getSignatureFieldList` 方法和傳遞 `BLOB` 包含包含簽名欄位的PDF文檔的對象。 此方法返回 `MyArrayOfPDFSignatureField` 集合對象，其中每個元素都包含 `PDFSignatureField` 的雙曲餘切值。
   * 迭代 `MyArrayOfPDFSignatureField` 用於確定是否存在簽名欄位名稱的對象。 對於PDF文檔中的每個簽名欄位，您可以 `PDFSignatureField` 的雙曲餘切值。 要獲取簽名欄位的名稱，請調用 `PDFSignatureField` 對象 `getName` 的雙曲餘切值。 此方法返回一個字串值，該字串值指定簽名欄位名稱。

**另請參閱**

[正在檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改簽名欄位 {#modifying-signature-fields}

可以使用Java API和Web服務API修改PDF文檔中的簽名欄位。 修改簽名欄位涉及操作其簽名欄位鎖定字典值或種子值字典值。

A *欄位鎖詞典* 指定簽名域時鎖定的域的清單。 鎖定的欄位防止用戶對欄位進行更改。 A *種子值字典* 包含應用簽名時使用的約束資訊。 例如，您可以更改權限，以控制在不使簽名無效的情況下可能發生的操作。

通過修改現有簽名欄位，您可以對PDF文檔進行更改，以反映不斷變化的業務要求。 例如，新業務要求可能要求在文檔簽名後鎖定所有文檔欄位。

本節說明如何通過修改欄位鎖定字典和種子值字典值來修改簽名欄位。 對簽名域鎖定字典所做的更改將導致簽名域簽名時鎖定PDF文檔中的所有欄位。 對種子值字典所做的更改會禁止對文檔進行特定類型的更改。

>[!NOTE]
>
>有關簽名服務和修改簽名欄位的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要修改PDF文檔中的簽名欄位，請執行以下任務：

1. 包括項目檔案。
1. 建立簽名客戶端。
1. 獲取包含要修改的簽名欄位的PDF文檔。
1. 設定字典值。
1. 修改簽名欄位。
1. 將PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括LiveCycleJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取包含要修改的簽名欄位的PDF文檔**

檢索包含要修改的簽名欄位的PDF文檔。

**設定字典值**

要修改簽名欄位，請將值分配給其欄位鎖定字典或種子值字典。 指定簽名域鎖定字典值涉及指定簽名域時鎖定的PDF文檔欄位。 （本節討論如何鎖定所有欄位。）

可以設定以下種子值字典值：

* **修訂檢查**:指定在將簽名應用於簽名欄位時是否執行吊銷檢查。
* **證書選項**:為證書種子值字典分配值。 在指定證書選項之前，建議您熟悉證書種子值字典。 (請參閱 [PDF引用](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。)
* **摘要選項**:分配用於簽名的摘要算法。 有效值為SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **篩選**:指定與簽名欄位一起使用的篩選器。 例如，可以使用Adobe.PPKLite篩選器。 (請參閱 [PDF引用](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。)
* **標籤選項**:指定與此簽名欄位關聯的標籤值。 值1表示簽名者只能使用指定的條目值。 值0表示允許其他值。 下面是位位置：

   * **1（篩選器）:** 用於簽名欄位的簽名處理程式
   * **2（子篩選器）:** 表示簽名時使用的可接受編碼的名稱陣列
   * **3(V)**:用於簽名欄位的簽名處理程式的最低所需版本號
   * **4（原因）:** 指定文檔簽名可能原因的字串陣列
   * **5(PDFLegalWarnings):** 指定可能的合法證明的字串陣列

* **法律證明**:當文檔被認證時，將自動掃描它以查找特定類型的內容，這些內容會使文檔的可見內容模糊或具有誤導性。 例如，注釋可以遮蔽對瞭解正在認證的內容非常重要的文本。 掃描過程生成指示存在此類內容的警告。 它還提供了可能生成警告的內容的附加說明。
* **權限**:指定可在PDF文檔上使用而不使簽名無效的權限。
* **原因**:指定必須簽名此文檔的原因。
* **時間戳**:指定時間戳選項。 例如，可以設定所使用的時間戳伺服器的URL。
* **版本**:指定用於簽名欄位的簽名處理程式的最小版本號。

**修改簽名欄位**

建立簽名服務客戶端後，檢索包含要修改的簽名欄位的PDF文檔，並設定字典值，您可以指示簽名服務修改簽名欄位。 然後，簽名服務返回包含已修改簽名欄位的PDF文檔。 原始PDF文檔不受影響。

**將PDF文檔另存為PDF檔案**

將包含已修改簽名欄位的PDF文檔另存為PDF檔案，以便用戶可以在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[簽名服務API快速啟動](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[數字簽名PDF文檔](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API修改簽名欄位 {#modify-signature-fields-using-the-java-api}

使用簽名API(Java)修改簽名欄位：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取包含要修改的簽名欄位的PDF文檔

   * 建立 `java.io.FileInputStream` 表示包含要修改的簽名欄位的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定字典值

   * 建立 `PDFSignatureFieldProperties` 對象。 A `PDFSignatureFieldProperties` 對象儲存簽名欄位鎖定字典和種子值字典資訊。
   * 建立 `PDFSeedValueOptionSpec` 對象。 此對象允許您設定種子值字典值。
   * 通過調用PDF文檔禁止更改 `PDFSeedValueOptionSpec` 對象 `setMdpValue` 方法和傳遞 `MDPPermissions.NoChanges` 枚舉值。
   * 建立 `FieldMDPOptionSpec` 對象。 此對象允許您設定簽名域鎖定字典值。
   * 通過調用PDF文檔中的 `FieldMDPOptionSpec` 對象 `setMdpValue` 方法和傳遞 `FieldMDPAction.ALL` 枚舉值。
   * 通過調用 `PDFSignatureFieldProperties` 對象 `setSeedValue` 方法和傳遞 `PDFSeedValueOptionSpec` 的雙曲餘切值。
   * 通過調用 `PDFSignatureFieldProperties`對象 `setFieldMDP` 方法和傳遞 `FieldMDPOptionSpec` 的雙曲餘切值。

   >[!NOTE]
   >
   >要查看可設定的所有種子值字典值，請參閱 `PDFSeedValueOptionSpec` 類引用。 (請參閱 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

1. 修改簽名欄位

   通過調用 `SignatureServiceClient` 對象 `modifySignatureField` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 儲存包含要修改的簽名欄位的PDF文檔的對象
   * 指定簽名欄位名稱的字串值
   * 的 `PDFSignatureFieldProperties` 儲存簽名域鎖定字典和種子值字典資訊的對象

   的 `modifySignatureField` 方法返回 `com.adobe.idp.Document` 儲存包含已修改簽名欄位的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `java.io.File` 對象，並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象。 確保使用 `com.adobe.idp.Document` 對象 `modifySignatureField` 返回。

### 使用Web服務API修改簽名欄位 {#modify-signature-fields-using-the-web-service-api}

使用簽名API（Web服務）修改簽名欄位：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 對象。
   * 建立 `SignatureServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `SignatureServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取包含要修改的簽名欄位的PDF文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存包含要修改的簽名欄位的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性位元組陣列的內容。

1. 設定字典值

   * 建立 `PDFSignatureFieldProperties` 對象。 此對象儲存簽名域鎖定字典和種子值字典資訊。
   * 建立 `PDFSeedValueOptionSpec` 對象。 此對象允許您設定種子值字典值。
   * 通過分配PDF文檔，禁止更改 `MDPPermissions.NoChanges` 枚舉值 `PDFSeedValueOptionSpec` 對象 `mdpValue` 資料成員。
   * 建立 `FieldMDPOptionSpec` 對象。 此對象允許您設定簽名域鎖定字典值。
   * 通過分配PDF文檔中的 `FieldMDPAction.ALL` 枚舉值 `FieldMDPOptionSpec` 對象 `mdpValue` 資料成員。
   * 通過分配種子值字典資訊 `PDFSeedValueOptionSpec` 對象 `PDFSignatureFieldProperties` 對象 `seedValue` 資料成員。
   * 通過分配簽名欄位鎖定字典資訊 `FieldMDPOptionSpec` 對象 `PDFSignatureFieldProperties` 對象 `fieldMDP` 資料成員。

   >[!NOTE]
   >
   >要查看可設定的所有種子值字典值，請參閱 `PDFSeedValueOptionSpec` 類引用。 (請參閱 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 修改簽名欄位

   通過調用 `SignatureServiceClient` 對象 `modifySignatureField` 方法並傳遞以下值：

   * 的 `BLOB` 儲存包含要修改的簽名欄位的PDF文檔的對象
   * 指定簽名欄位名稱的字串值
   * 的 `PDFSignatureFieldProperties` 儲存簽名域鎖定字典和種子值字典資訊的對象

   的 `modifySignatureField` 方法返回 `BLOB` 儲存包含已修改簽名欄位的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值(該字串值表示將包含簽名欄位的PDF文檔的檔案位置)以及開啟檔案的模式來對對象。
   * 建立一個位元組陣列，用於儲存 `BLOB` 對象 `addSignatureField` 方法返回。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數字簽名PDF文檔 {#digitally-signing-pdf-documents}

數字簽名可以應用於PDF文檔以提供安全級別。 數字簽名與手寫簽名一樣，提供了一種手段，使簽名者能夠識別自己並就文檔發表聲明。 用於對文檔進行數字簽名的技術有助於確保簽名者和收件人都清楚簽名的內容，並確信文檔自簽名後沒有更改。

PDF檔案採用公鑰技術簽署。 簽名者有兩個密鑰：公鑰和私鑰。 私鑰儲存在用戶憑據中，簽名時必須可用。 公鑰儲存在用戶的證書中，收件人必須可以使用該證書來驗證簽名。 有關已吊銷證書的資訊可在由證書頒發機構(CA)分發的證書吊銷清單(CRL)和線上證書狀態協定(OCSP)響應中找到。 簽名時間可以從稱為時間戳頒發機構的可信源獲得。

>[!NOTE]
>
>在對PDF文檔進行數字簽名之前，必須確保將證書添加到AEM Forms。 證書是使用管理控制台或使用Trust Manager API以寫程式方式添加的。 (請參閱 [使用Trust Manager API導入憑據](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。)

可以以寫程式方式對PDF文檔進行數字簽名。 對PDF文檔進行數字簽名時，必須引用AEM Forms中存在的安全憑據。 憑據是用於簽名的私鑰。

簽名服務在簽名PDF文檔時執行以下步驟：

1. 簽名服務通過傳遞請求中指定的別名從信任儲存中檢索憑據。
1. 信任儲存會搜索指定的憑據。
1. 憑據將返回到簽名服務，並用於對文檔進行簽名。 還根據別名快取該憑據以備將來請求。

有關處理安全憑據的資訊，請參見 *安裝和部署AEM Forms* 指南。

>[!NOTE]
>
>簽名文檔和驗證文檔之間存在差異。 (請參閱 [驗證PDF文檔](digitally-signing-certifying-documents.md#certifying-pdf-documents)。)

>[!NOTE]
>
>並非所有PDF文檔都支援簽名。 有關簽名服務和數字簽名文檔的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>簽名服務不支援將嵌入的PDF資料作為操作（如驗證文檔）的輸入的XDP檔案。 此操作導致簽名服務引發 `PDFOperationException`。 要解決此問題，請使用PDF實用程式服務將XDP檔案轉換為PDF檔案，然後將轉換後的PDF檔案傳遞給簽名服務操作。 (請參閱 [使用PDF實用程式](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)。)

**nCipher nShield HSM憑據**

當使用nCypher nShield HSM憑據對PDF文檔進行簽名或認證時，只有在重新啟動AEM Forms所部署的J2EE應用程式伺服器之後，才能使用新憑據。 但是，您可以設定配置值，這樣，在不重新啟動J2EE應用程式伺服器的情況下，可以對操作進行簽名或驗證。

可以在位於/opt/nfast/cknfastrc(或c:\nfast\cknfastrc)的cknfastrc檔案中添加以下配置值：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此配置值添加到cknfastrc檔案後，可以在不重新啟動J2EE應用程式伺服器的情況下使用新憑據。

**簽名不受信任**

在對同一PDF文檔進行認證和簽名時，如果不信任認證簽名，則在Acrobat或Adobe Reader開啟PDF文檔時，將針對第一個簽名顯示一個黃色三角形。 為避免這種情況，必須信任驗證簽名。

**對基於XFA的表單的文檔進行簽名**

如果您嘗試使用簽名服務API對基於XFA的表單進行簽名，則可能會在 `View` `Signed` `Version` 位於Acrobat。 例如，請考慮以下工作流：

* 使用使用設計器建立的XDP檔案，可以合併包含簽名欄位的表單設計和包含表單資料的XML資料。 您使用Forms服務生成互動式PDF文檔。
* 您使用簽名服務API對PDF文檔進行簽名。

### 步驟摘要 {#summary_of_steps-3}

要對PDF文檔進行數字簽名，請執行以下任務：

1. 包括項目檔案。
1. 建立簽名服務客戶端。
1. 獲取要簽名的PDF文檔。
1. 簽署PDF文檔。
1. 將簽名的PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取要簽名的PDF文檔**

要簽名PDF文檔，必須獲取包含簽名欄位的PDF文檔。 如果PDF文檔不包含簽名欄位，則無法對其簽名。 可以使用設計器或寫程式方式添加簽名欄位。

**簽署PDF文檔**

在簽名PDF文檔時，可以設定簽名服務使用的運行時選項。 可以設定以下選項：

* 外觀選項
* 吊銷檢查
* 時間戳值

使用 `PDFSignatureAppearanceOptionSpec` 的雙曲餘切值。 例如，通過調用 `PDFSignatureAppearanceOptionSpec` 對象 `setShowDate` 方法 `true`。

您還可以指定是否執行撤消檢查以確定用於對PDF文檔進行數字簽名的證書是否已被撤消。 要執行吊銷檢查，可以指定以下值之一：

* **無檢查**:不執行吊銷檢查。
* **盡力**:始終嘗試檢查是否吊銷鏈中的所有證書。 如果檢查中出現任何問題，則假定吊銷有效。 如果發生任何故障，請假定未吊銷證書。
* **CheckIfAvailable（檢查可用）:** 如果吊銷資訊可用，請檢查鏈中所有證書的吊銷。 如果檢查中出現任何問題，則假定吊銷無效。 如果發生任何故障，則假定證書已吊銷且無效。 （這是預設值。）
* **始終檢查**:檢查是否吊銷鏈中的所有證書。 如果任何證書中都不存在吊銷資訊，則假定吊銷無效。

要對證書執行吊銷檢查，可以使用 `CRLOptionSpec` 的雙曲餘切值。 但是，如果要執行吊銷檢查，並且您沒有指定CRL伺服器的URL，則簽名服務將從證書中獲取該URL。

在執行吊銷檢查時，可以使用聯機證書狀態協定(OCSP)伺服器，而不是使用CRL伺服器。 通常，當使用OCSP伺服器而不是CRL伺服器時，執行吊銷檢查的速度會更快。 (請參閱「聯機證書狀態協定」，地址為 [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560)。)

您可以使用Adobe應用程式和服務設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是在「Adobe應用程式和服務」中首先設定的，則會檢查OCSP伺服器，然後檢查CRL伺服器。 （請參閱AAC幫助中的「使用信任儲存管理證書和憑據」）。

如果指定不執行吊銷檢查，則簽名服務不會檢查用於簽名或證明文檔已被吊銷的證書。 即，忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>雖然CRL或OCSP伺服器可以在證書中指定，但您可以使用 `CRLOptionSpec` 和 `OCSPOptionSpec` 的雙曲餘切值。 例如，要覆蓋CRL伺服器，可以調用 `CRLOptionSpec` 對象 `setLocalURI` 的雙曲餘切值。

時間標籤是指跟蹤修改已簽名或經認證的文檔的時間的過程。 文檔簽名後，即使文檔所有者也不應修改它。 時間標籤有助於強制使用已簽名或經認證的文檔。 可以使用 `TSPOptionSpec` 的雙曲餘切值。 例如，可以指定時間戳提供程式(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務中，通過各個部分和相應的快速啟動，使用撤銷檢查。 由於未指定CRL或OCSP伺服器資訊，因此伺服器資訊是從用於對PDF文檔進行數字簽名的證書中獲取的。

要成功簽署PDF文檔，可以指定包含數字簽名的簽名欄位的完全限定名稱，如 `form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單域時，還可以使用簽名域的部分名稱： `SignatureField3[3]`。

您還必須引用安全憑據以對PDF文檔進行數字簽名。 要引用安全憑據，請指定別名。 別名是對PKCS#12檔案（副檔名為.pfx）或硬體安全模組(HSM)中實際憑據的引用。 有關安全憑據的資訊，請參見 *安裝和部署AEM Forms* 指南。

**保存已簽名的PDF文檔**

簽名服務對PDF文檔進行數字簽名後，您可以將其另存為PDF檔案，以便用戶可以在Acrobat或Adobe Reader開啟它。

**另請參閱**

[使用Java API對PDF文檔進行數字簽名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用Web服務API對PDF文檔進行數字簽名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

[正在檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API對PDF文檔進行數字簽名 {#digitally-sign-pdf-documents-using-the-java-api}

使用簽名API(Java)對PDF文檔進行數字簽名：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取要簽名的PDF文檔

   * 建立 `java.io.FileInputStream` 表示要通過使用其建構子進行數字簽名的PDF文檔的對象，並傳遞指定PDF文檔位置的字串值。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 簽署PDF文檔

   通過調用PDF文檔 `SignatureServiceClient` 對象 `sign` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示要簽名的PDF文檔的對象。
   * 一個字串值，它表示包含數字簽名的簽名欄位的名稱。
   * A `Credential` 表示用於對PDF文檔進行數字簽名的憑據的對象。 建立 `Credential` 通過調用 `Credential` 對象的靜態 `getInstance` 方法並傳遞一個字串值，該字串值指定與安全憑據對應的別名值。
   * A `HashAlgorithm` 對象，該對象指定表示用於摘要PDF文檔的哈希算法的靜態資料成員。 例如，可以指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一個字串值，它表示PDF文檔被數字簽名的原因。
   * 表示簽名者聯繫資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數字簽名外觀的對象。 例如，您可以使用此對象將自定義徽標添加到數字簽名中。
   * A `java.lang.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。
   * 安 `OCSPOptionSpec` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援的首選項的對象。 此參數是可選的，可以 `null`。 有關詳細資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   的 `sign` 方法返回 `com.adobe.idp.Document` 表示簽名PDF文檔的對象。

1. 保存已簽名的PDF文檔

   * 建立 `java.io.File` 並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法 `java.io.File`複製 `Document` 對象。 確保使用 `com.adobe.idp.Document` 返回的對象 `sign` 的雙曲餘切值。

**另請參閱**

[數字簽名PDF文檔](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速啟動（SOAP模式）:使用Java API對PDF文檔進行數字簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API對PDF文檔進行數字簽名 {#digitally-signing-pdf-documents-using-the-web-service-api}

要使用簽名API（Web服務）對PDF文檔進行數字簽名：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 對象。
   * 建立 `SignatureServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `SignatureServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取要簽名的PDF文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存已簽名的PDF文檔。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值(該字串值表示要簽名的PDF文檔的檔案位置和開啟檔案的模式)來對對象。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性位元組陣列的內容。

1. 簽署PDF文檔

   通過調用PDF文檔 `SignatureServiceClient` 對象 `sign` 方法並傳遞以下值：

   * A `BLOB` 表示要簽名的PDF文檔的對象。
   * 一個字串值，它表示包含數字簽名的簽名欄位的名稱。
   * A `Credential` 表示用於對PDF文檔進行數字簽名的憑據的對象。 建立 `Credential` 對象，並通過為 `Credential` 對象 `alias` 屬性。
   * A `HashAlgorithm` 對象，該對象指定表示用於摘要PDF文檔的哈希算法的靜態資料成員。 例如，可以指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一個布爾值，指定是否使用哈希算法。
   * 一個字串值，它表示PDF文檔被數字簽名的原因。
   * 表示簽名者位置的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數字簽名外觀的對象。 例如，您可以使用此對象將自定義徽標添加到數字簽名中。
   * A `System.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。 如果完成了此吊銷檢查，則將其嵌入簽名中。 預設為 `false`。
   * 安 `OCSPOptionSpec` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。 有關此對象的資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援的首選項的對象。 此參數是可選的，可以 `null`。

   的 `sign` 方法返回 `BLOB` 表示簽名PDF文檔的對象。

1. 保存已簽名的PDF文檔

   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `sign` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[數字簽名PDF文檔](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數字簽名互動式Forms {#digitally-signing-interactive-forms}

您可以簽署Forms服務建立的互動式表單。 例如，請考慮以下工作流：

* 您可以合併使用設計器建立的基於XFA的PDF表單，以及使用Forms服務在XML文檔中的表單資料。 Forms伺服器呈現互動式窗體。
* 使用簽名服務API對交互表單進行簽名。

結果是數字簽名的互動式PDF表單。 在簽名基於XFA表單的PDF表單時，請確保將PDF檔案另存為Adobe靜態PDF表單。 如果嘗試簽名保存為PDF動態Adobe表單的PDF表單，則會出現異常。 由於您正在對從Forms服務返回的表單進行簽名，因此請確保該表單包含簽名欄位。

>[!NOTE]
>
>在對互動式表單進行數字簽名之前，必須確保將證書添加到AEM Forms。 證書是使用管理控制台或使用Trust Manager API以寫程式方式添加的。 (請參閱 [使用Trust Manager API導入憑據](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。)

使用Forms服務API時，設定 `GenerateServerAppearance` 運行時選項到 `true`。 此運行時選項可確保在Acrobat或Adobe Reader開啟時，伺服器上生成的表單的外觀仍然有效。 建議在使用FormsAPI生成要簽名的互動式表單時設定此運行時選項。

>[!NOTE]
>
>在閱讀數字簽名互動式Forms之前，建議您熟悉簽名PDF文檔。 (請參閱 [數字簽名PDF文檔](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)

### 步驟摘要 {#summary_of_steps-4}

要對Forms服務返回的交互表單進行數字簽名，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms和簽名客戶端。
1. 使用Forms服務獲取互動式表單。
1. 簽署互動式表單。
1. 將簽名的PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立Forms和簽名客戶端**

由於此工作流同時調用Forms和簽名服務，因此請同時建立Forms服務客戶端和簽名服務客戶端。

**使用Forms服務獲取互動式表單**

您可以使用Forms服務獲取要簽名的互動式PDF表。 在AEM Forms，你可以通過 `com.adobe.idp.Document` 對象到包含要呈現的表單的Forms服務。 此方法的名稱為 `renderPDFForm2`。 此方法返回 `com.adobe.idp.Document` 包含要簽名的窗體的對象。 你可以通過 `com.adobe.idp.Document` 實例。

同樣，如果您使用Web服務，則可以 `BLOB` Forms服務返回簽名服務的實例。

>[!NOTE]
>
>與「數字簽名互動式Forms」部分關聯的快速啟動調用 `renderPDFForm2` 的雙曲餘切值。

**簽署互動式窗體**

在簽名PDF文檔時，可以設定簽名服務使用的運行時選項。 可以設定以下選項：

* 外觀選項
* 吊銷檢查
* 時間戳值

使用 `PDFSignatureAppearanceOptionSpec` 的雙曲餘切值。 例如，通過調用 `PDFSignatureAppearanceOptionSpec` 對象 `setShowDate` 方法 `true`。

**保存已簽名的PDF文檔**

簽名服務對PDF文檔進行數字簽名後，可將其另存為PDF檔案。 PDF檔案可在Acrobat或Adobe Reader開啟。

**另請參閱**

[使用Java API對互動式表單進行數字簽名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用Web服務API對交互表單進行數字簽名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數字簽名PDF文檔](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[呈現互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API對互動式表單進行數字簽名 {#digitally-sign-an-interactive-form-using-the-java-api}

使用Forms和簽名API(Java)對互動式表單進行數字簽名：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-signatures-client.jar和adobe-forms-client.jar。

1. 建立Forms和簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 使用Forms服務獲取互動式表單

   * 建立 `java.io.FileInputStream` 表示要通過使用其建構子傳遞給Forms服務的PDF文檔的對象。 傳遞一個字串值，指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。
   * 建立 `java.io.FileInputStream` 表示XML文檔的對象，該文檔包含要通過使用其建構子傳遞給Forms服務的表單資料。 傳遞一個指定XML檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。
   * 建立 `PDFFormRenderSpec` 用於設定運行時選項的對象。 調用 `PDFFormRenderSpec` 對象 `setGenerateServerAppearance` 方法 `true`。
   * 調用 `FormsServiceClient` 對象 `renderPDFForm2` 方法並傳遞以下值：

      * A `com.adobe.idp.Document` 包含要呈現的PDF窗體的對象。
      * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。
      * A `PDFFormRenderSpec` 儲存運行時選項的對象。
      * A `URLSpec` 包含Forms服務所需的URI值的對象。 可以指定 `null` 值。
      * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

      的 `renderPDFForm2` 方法返回 `FormsResult` 包含表單資料流的對象

   * 通過調用PDF表單 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。 此方法返回 `com.adobe.idp.Document` 表示互動式窗體的對象。


1. 簽署互動式窗體

   通過調用PDF文檔 `SignatureServiceClient` 對象 `sign` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示要簽名的PDF文檔的對象。 確保此對象為 `com.adobe.idp.Document` 從Forms服務獲取的對象。
   * 一個字串值，它表示簽名的簽名欄位的名稱。
   * A `Credential` 表示用於對PDF文檔進行數字簽名的憑據的對象。 建立 `Credential` 通過調用 `Credential` 對象的靜態 `getInstance` 的雙曲餘切值。 傳遞一個字串值，該字串值指定與安全憑據對應的別名值。
   * A `HashAlgorithm` 對象，該對象指定表示用於摘要PDF文檔的哈希算法的靜態資料成員。 例如，可以指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一個字串值，它表示PDF文檔被數字簽名的原因。
   * 表示簽名者聯繫資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數字簽名外觀的對象。 例如，您可以使用此對象將自定義徽標添加到數字簽名中。
   * A `java.lang.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。
   * 安 `OCSPPreferences` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援的首選項的對象。 此參數是可選的，可以 `null`。

   的 `sign` 方法返回 `com.adobe.idp.Document` 表示簽名PDF文檔的對象。

1. 保存已簽名的PDF文檔

   * 建立 `java.io.File` 對象，並確保檔案名副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法 `java.io.File`複製 `Document` 對象。 確保使用 `com.adobe.idp.Document` 對象 `sign` 返回。

**另請參閱**

[數字簽名互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速啟動（SOAP模式）:使用Java API對PDF文檔進行數字簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API對交互表單進行數字簽名 {#digitally-sign-an-interactive-form-using-the-web-service-api}

使用Forms和簽名API（Web服務）對互動式表單進行數字簽名：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 由於此客戶端應用程式調用兩個AEM Forms服務，因此建立兩個服務引用。 對與簽名服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   對與Forms服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   因為 `BLOB` 資料類型是兩種服務引用的公用類型，完全限定 `BLOB` 資料類型。 在相應的Web服務快速啟動中， `BLOB` 實例完全限定。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立Forms和簽名客戶端

   * 建立 `SignatureServiceClient` 對象。
   * 建立 `SignatureServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `SignatureServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對Forms服務客戶端重複這些步驟。

1. 使用Forms服務獲取互動式表單

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存已簽名的PDF文檔。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值(該字串值表示要簽名的PDF文檔的檔案位置和開啟檔案的模式)來對對象。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性位元組陣列的內容。
   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存表單資料。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示包含表單資料的XML檔案的檔案位置，以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性位元組陣列的內容。
   * 建立 `PDFFormRenderSpec` 用於設定運行時選項的對象。 分配值 `true` 到 `PDFFormRenderSpec` 對象 `generateServerAppearance` 的子菜單。
   * 調用 `FormsServiceClient` 對象 `renderPDFForm2` 方法並傳遞以下值：

      * A `BLOB` 包含要呈現的PDF窗體的對象。
      * A `BLOB` 包含要與窗體合併的資料的對象。
      * A `PDFFormRenderSpec` 儲存運行時選項的對象。
      * A `URLSpec` 包含Forms服務所需的URI值的對象。 可以指定 `null` 值。
      * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。
      * 用於儲存窗體中頁數的長輸出參數。
      * 用於區域設定值的字串輸出參數。
      * A `FormResult` 用於儲存互動式窗體的輸出參數的值。
   * 通過調用PDF表單 `FormsResult` 對象 `outputContent` 的子菜單。 此欄位儲存 `BLOB` 表示互動式窗體的對象。


1. 簽署互動式窗體

   通過調用PDF文檔 `SignatureServiceClient` 對象 `sign` 方法並傳遞以下值：

   * A `BLOB` 表示要簽名的PDF文檔的對象。 使用 `BLOB` Forms局返回的實例。
   * 一個字串值，它表示簽名的簽名欄位的名稱。
   * A `Credential` 表示用於對PDF文檔進行數字簽名的憑據的對象。 建立 `Credential` 對象，並通過為 `Credential` 對象 `alias` 屬性。
   * A `HashAlgorithm` 對象，該對象指定表示用於摘要PDF文檔的哈希算法的靜態資料成員。 例如，可以指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一個布爾值，指定是否使用哈希算法。
   * 一個字串值，它表示PDF文檔被數字簽名的原因。
   * 表示簽名者位置的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數字簽名外觀的對象。 例如，您可以使用此對象將自定義徽標添加到數字簽名中。
   * A `System.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。 如果完成了此吊銷檢查，則將其嵌入簽名中。 預設為 `false`。
   * 安 `OCSPPreferences` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。 有關此對象的資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援的首選項的對象。 此參數是可選的，可以 `null`。

   的 `sign` 方法返回 `BLOB` 表示簽名PDF文檔的對象。

1. 保存已簽名的PDF文檔

   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `sign` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[數字簽名互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 驗證PDF文檔 {#certifying-pdf-documents}

您可以通過使用稱為認證簽名的特定類型的簽名來驗證PDF文檔，從而保護文檔的安全。 通過以下方式將經認證的簽名與數字簽名區別：

* 它必須是應用於PDF檔案的第一個簽名；即，在應用經認證的簽名時，文檔中的任何其他簽名欄位都必須未簽名。 在PDF文檔中只允許一個經認證的簽名。 如果要簽名和認證PDF文檔，則必須在簽名前對其進行認證。 驗證PDF文檔後，可以對其他簽名欄位進行數字簽名。
* 文檔的作者或發起者可以指定文檔可以以某些方式進行修改，而不會使經認證的簽名失效。 例如，文檔可允許填寫表單或注釋。 如果作者指定不允許某種修改，Acrobat將限制用戶以這種方式修改文檔。 如果進行此類修改，例如使用其他應用程式，則經認證的簽名無效，並且當用戶開啟文檔時，Acrobat發出警告。 （使用未經認證的簽名，不會阻止修改，並且正常的編輯操作不會使原始簽名無效。）
* 在簽名時，將掃描文檔中特定類型的內容，這些內容可能使文檔的內容模糊或具有誤導性。 例如，批注可能會使頁面上的某些文本模糊，這些文本對於瞭解正在認證的內容非常重要。 可以提供關於此類內容的解釋（法律證明）。

可以使用簽名服務Java API或簽名Web服務API以寫程式方式驗證PDF文檔。 驗證PDF文檔時，必須引用憑據服務中存在的安全憑據。 有關安全憑據的資訊，請參見 *安裝和部署AEM Forms* 指南。

>[!NOTE]
>
>在對同一PDF文檔進行認證和簽名時，如果不信任認證簽名，則在Acrobat或Adobe Reader開啟PDF文檔時，第一個簽名旁邊會出現一個黃色三角形。 必須信任驗證簽名才能避免這種情況。

>[!NOTE]
>
>當使用nCypher nShield HSM憑據對PDF文檔進行簽名或認證時，只有在重新啟動部署了AEM Forms的J2EE應用程式伺服器之後，才能使用新憑據。 但是，您可以設定配置值，這樣，在不重新啟動J2EE應用程式伺服器的情況下，可以對操作進行簽名或驗證。

可以在位於/opt/nfast/cknfastrc(或c:\nfast\cknfastrc)的cknfastrc檔案中添加以下配置值：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此配置值添加到cknfastrc檔案後，可以在不重新啟動J2EE應用程式伺服器的情況下使用新憑據。

>[!NOTE]
>
>有關簽名服務和驗證文檔的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

要驗證PDF文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立簽名客戶端。
1. 獲取PDF文檔以進行認證。
1. 驗證PDF文檔。
1. 將認證PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名操作之前，必須建立簽名客戶端。

**獲取PDF文檔以驗證**

要驗證PDF文檔，必須獲取包含簽名欄位的PDF文檔。 如果PDF文檔不包含簽名欄位，則無法對其進行認證。 可以使用設計器或寫程式方式添加簽名欄位。 有關以寫程式方式添加簽名欄位的資訊，請參見 [添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。

**驗證PDF文檔**

要成功驗證PDF文檔，您需要簽名服務使用以下輸入值來驗證PDF文檔：

* **PDF文檔**:包含簽名欄位的PDF文檔，該簽名欄位是包含經認證簽名的圖形表示的表單欄位。 PDF文檔必須包含簽名欄位，才能對其進行認證。 可以使用設計器或寫程式方式添加簽名欄位。 (請參閱 [添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。)
* **簽名欄位名**:經認證的簽名欄位的完全限定名稱。 以下值是一個示例： `form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單域時，還可以使用簽名域的部分名稱： `SignatureField3[3]`。 如果為欄位名稱傳遞了空值，則動態建立並驗證不可見的簽名欄位。
* **安全憑據**:用於驗證PDF文檔的憑據。 此安全憑據包含密碼和別名，它們必須與憑據服務中憑據中顯示的別名相匹配。 別名是對PKCS#12檔案（帶.pfx副檔名）或硬體安全模組(HSM)中實際憑據的引用。
* **哈希算法**:用於摘要PDF文檔的哈希算法。
* **簽名原因**:顯示在Acrobat或Adobe Reader的值，以便其他用戶知道PDF文檔被認證的原因。
* **簽名人的位置**:憑據指定的簽名者的位置。
* **聯繫資訊**:簽名人的聯繫資訊，如地址和電話號碼。
* **權限資訊**:控制最終用戶可以對文檔執行的操作而不導致認證簽名無效的權限。 例如，您可以設定權限，以便對PDF文檔的任何更改都會導致認證的簽名無效。
* **法律解釋**:當文檔經過認證時，將自動掃描文檔中特定類型的內容，這些內容可能會使文檔的內容模糊或具有誤導性。 例如，批注可能會使頁面上的某些文本模糊，這些文本對於瞭解正在認證的內容非常重要。 掃描過程生成有關這些類型內容的警告。 此值提供了可能生成警告的內容的附加說明。
* **外觀選項**:控制認證簽名外觀的選項。 例如，認證簽名可以顯示日期資訊。
* **吊銷檢查**:此值指定是否對簽名者的證書執行吊銷檢查。 預設設定 `false` 表示未執行吊銷檢查。
* **OCSP設定**:聯機證書狀態協定(OCSP)支援的設定，提供有關用於驗證PDF文檔的憑據狀態的資訊。 例如，您可以指定伺服器的URL，該URL提供有關您用於登錄到PDF文檔的憑據的資訊。
* **CRL設定**:完成吊銷檢查時證書吊銷清單(CRL)首選項的設定。 例如，您可以指定始終檢查是否吊銷了憑據。
* **時間戳**:定義應用於認證簽名的時間戳資訊的設定。 時間戳表示在特定時間之前已建立特定資料。 此知識有助於在簽名者和驗證者之間建立信任關係。

**將認證PDF文檔另存為PDF檔案**

簽名服務認證PDF文檔後，您可以將其另存為PDF檔案，以便用戶可以在Acrobat或Adobe Reader開啟它。

**另請參閱**

[使用Java API驗證PDF文檔](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用Web服務API驗證PDF文檔](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API驗證PDF文檔 {#certify-pdf-documents-using-the-java-api}

使用簽名API(Java)驗證PDF文檔：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取PDF文檔以驗證

   * 建立 `java.io.FileInputStream` 表示要驗證的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 驗證PDF文檔

   通過調用PDF文檔 `SignatureServiceClient` 對象 `certify` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 表示要認證的PDF文檔的對象。
   * 一個字串值，它表示包含簽名的簽名欄位的名稱。
   * A `Credential` 表示用於驗證PDF文檔的憑據的對象。 建立 `Credential` 通過調用 `Credential` 對象的靜態 `getInstance` 方法並傳遞一個字串值，該字串值指定與安全憑據對應的別名值。
   * A `HashAlgorithm` 對象，該對象指定表示用於摘要PDF文檔的哈希算法的靜態資料成員。 例如，可以指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一個字串值，它表示PDF文檔被認證的原因。
   * 表示簽名者聯繫資訊的字串值。
   * A `MDPPermissions` 對象，該對象指定可對使簽名無效的PDF文檔執行的操作。
   * A `PDFSignatureAppearanceOptions` 控制認證簽名外觀的對象。 如果需要，請通過調用方法(如 `setShowDate`。
   * 一個字串值，它解釋了哪些操作使簽名無效。
   * A `java.lang.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。 如果完成了此吊銷檢查，則將其嵌入簽名中。 預設為 `false`。
   * A `java.lang.Boolean` 指定是否鎖定正在認證的簽名欄位的對象。 如果欄位被鎖定，則簽名欄位被標籤為只讀，其屬性無法修改，並且沒有所需權限的任何人都無法清除該欄位。 預設為 `false`。
   * 安 `OCSPPreferences` 儲存線上證書狀態協定(OCSP)支援首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。 有關此對象的資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援的首選項的對象。 例如，在建立 `TSPPreferences` 對象，通過調用 `TSPPreferences` 對象 `setTspServerURL` 的雙曲餘切值。 此參數是可選的，可以 `null`。 有關詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

   的 `certify` 方法返回 `com.adobe.idp.Document` 表示認證PDF文檔的對象。

1. 將認證PDF文檔另存為PDF檔案

   * 建立 `java.io.File` 並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象。

**另請參閱**

[驗證PDF文檔](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速啟動（SOAP模式）:使用Java API驗證PDF文檔](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API驗證PDF文檔 {#certify-pdf-documents-using-the-web-service-api}

使用簽名API（Web服務）驗證PDF文檔：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 對象。
   * 建立 `SignatureServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `SignatureServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取PDF文檔以驗證

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存經認證的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示要驗證的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 資料成員位元組陣列的內容。

1. 驗證PDF文檔

   通過調用PDF文檔 `SignatureServiceClient` 對象 `certify` 方法並傳遞以下值：

   * 的 `BLOB` 表示要認證的PDF文檔的對象。
   * 一個字串值，它表示包含簽名的簽名欄位的名稱。
   * A `Credential` 表示用於驗證PDF文檔的憑據的對象。 建立 `Credential` 對象，並通過為 `Credential` 對象 `alias` 屬性。
   * A `HashAlgorithm` 對象，該對象指定表示用於摘要PDF文檔的哈希算法的靜態資料成員。 例如，可以指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一個布爾值，指定是否使用哈希算法。
   * 一個字串值，它表示PDF文檔被認證的原因。
   * 表示簽名者位置的字串值。
   * 表示簽名者聯繫資訊的字串值。
   * 安 `MDPPermissions` 對象的靜態資料成員，該成員指定可對PDF文檔執行使簽名無效的操作。
   * 一個布爾值，它指定是否使用 `MDPPermissions` 作為上一個參數值傳遞的對象。
   * 一個字串值，它解釋使簽名失效的操作。
   * A `PDFSignatureAppearanceOptions` 控制認證簽名外觀的對象。 建立 `PDFSignatureAppearanceOptions` 對象。 可以通過設定簽名的一個資料成員來修改簽名的外觀。
   * A `System.Boolean` 指定是否對簽名者的證書執行吊銷檢查的對象。 如果完成了此吊銷檢查，則將其嵌入簽名中。 預設為 `false`。
   * A `System.Boolean` 指定是否鎖定正在認證的簽名欄位的對象。 如果欄位被鎖定，則簽名欄位被標籤為只讀，其屬性無法修改，並且沒有所需權限的任何人都無法清除該欄位。 預設為 `false`。
   * A `System.Boolean` 指定是否鎖定簽名欄位的對象。 就是說，如果你通過 `true` 到上一個參數，然後傳遞 `true` 到此參數。
   * 安 `OCSPPreferences` 儲存線上證書狀態協定(OCSP)支援首選項的對象，該對象提供有關用於驗證PDF文檔的憑據狀態的資訊。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。
   * A `CRLPreferences` 儲存證書吊銷清單(CRL)首選項的對象。 如果未執行吊銷檢查，則不使用此參數，您可以指定 `null`。
   * A `TSPPreferences` 儲存時間戳提供程式(TSP)支援的首選項的對象。 例如，在建立 `TSPPreferences` 對象，可通過設定 `TSPPreferences` 對象 `tspServerURL` 資料成員。 此參數是可選的，可以 `null`。

   的 `certify` 方法返回 `BLOB` 表示認證PDF文檔的對象。

1. 將認證PDF文檔另存為PDF檔案

   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示將包含經認證的PDF文檔的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `certify` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[驗證PDF文檔](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證數字簽名 {#verifying-digital-signatures}

可以驗證數字簽名，以確保簽名的PDF文檔未被修改，並且數字簽名有效。 驗證數字簽名時，可以檢查簽名的狀態和簽名的屬性，如簽名者的身份。 在信任數字簽名之前，建議您驗證它。 驗證數字簽名時，請參考包含數字簽名的PDF文檔。

假設簽名者的身份未知。 在Acrobat開啟PDF文檔時，會出現一條警告消息，指出簽名者的身份未知，如下圖所示。

![vd_vd_verifsig](assets/vd_vd_verifysig.png)

同樣，當以寫程式方式驗證數字簽名時，可確定簽名者身份的狀態。 例如，如果驗證上圖所示文檔中的數字簽名，則結果將是簽名者的身份未知。

>[!NOTE]
>
>有關簽名服務和驗證數字簽名的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

要驗證數字簽名，請執行以下任務：

1. 包括項目檔案。
1. 建立簽名客戶端。
1. 獲取包含要驗證的簽名的PDF文檔。
1. 設定PKI運行時選項。
1. 驗證數字簽名。
1. 確定簽名的狀態。
1. 確定簽名者的身份。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，請建立簽名服務客戶端。

**獲取包含要驗證的簽名的PDF文檔**

要驗證用於對PDF文檔進行數字簽名或認證的簽名，請獲取包含簽名的PDF文檔。

**設定PKI運行時選項**

設定簽名服務在驗證PDF文檔中的簽名時使用的以下PKI運行時選項：

* 驗證時間
* 吊銷檢查
* 時間戳值

作為設定這些選項的一部分，可以指定驗證時間。 例如，您可以選擇當前時間（驗證程式電腦上的時間），該時間表示使用當前時間。 有關不同時間值的資訊，請參見 `VerificationTime` 枚舉值 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

您還可以指定是否作為驗證過程的一部分執行吊銷檢查。 例如，您可以執行吊銷檢查以確定證書是否被吊銷。 有關吊銷檢查選項的資訊，請參見 `RevocationCheckStyle` 枚舉值 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

要對證書執行吊銷檢查，請使用 `CRLOptionSpec` 的雙曲餘切值。 但是，如果未指定URL到CRL伺服器，簽名服務將從證書獲取該URL。

在執行吊銷檢查時，可以使用聯機證書狀態協定(OCSP)伺服器，而不是使用CRL伺服器。 通常，當使用OCSP伺服器而不是CRL伺服器時，執行吊銷檢查的速度會更快。 (請參閱 [聯機證書狀態協定](https://tools.ietf.org/html/rfc2560)。)

您可以使用Adobe應用程式和服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是在「Adobe應用程式和服務」中首先設定的，則會檢查OCSP伺服器，然後檢查CRL伺服器。

如果不執行吊銷檢查，簽名服務將不檢查證書是否已吊銷。 即，忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>可以使用 `CRLOptionSpec` 和 `OCSPOptionSpec` 的雙曲餘切值。 例如，要覆蓋CRL伺服器，可以調用 `CRLOptionSpec` 對象 `setLocalURI` 的雙曲餘切值。

時間標籤是跟蹤修改已簽名或已認證文檔的時間的過程。 文檔簽名後，任何人都無法修改它。 時間標籤有助於強制使用已簽名或經認證的文檔。 可以使用 `TSPOptionSpec` 的雙曲餘切值。 例如，可以指定時間戳提供程式(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間設定為 `VerificationTime.CURRENT_TIME` 並且吊銷檢查設定為 `RevocationCheckStyle.BestEffort`。 由於未指定CRL或OCSP伺服器資訊，因此從證書獲取伺服器資訊。

**驗證數字簽名**

要成功驗證簽名，請指定包含簽名的簽名欄位的完全限定名稱，如 `form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單域時，還可以使用簽名域的部分名稱： `SignatureField3`。

預設情況下，簽名服務將文檔在驗證時間後可以簽名的時間限制為65分鐘。 如果用戶嘗試在當前時間驗證簽名，且簽名時間晚於當前時間且在65分鐘內，則簽名服務不會建立驗證錯誤。

>[!NOTE]
>
>有關驗證簽名時需要的其他值，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**確定簽名的狀態**

作為驗證數字簽名的一部分，您可以檢查簽名的狀態。

**確定簽名者的身份**

您可以確定簽名者的身份，該身份可以是以下值之一：

* **未知**:此簽名者未知，因為無法執行簽名者驗證。
* **受信任**:此簽名者受信任。
* **不信任**:此簽名者不受信任。

**另請參閱**

[使用Java API驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[使用Web服務API驗證數字簽名](#verify-digital-signatures-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證數字簽名 {#verify-digital-signatures-using-the-java-api}

使用簽名服務API(Java)驗證數字簽名：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取包含要驗證的簽名的PDF文檔

   * 建立 `java.io.FileInputStream` 表示包含要使用其建構子驗證的簽名的PDF文檔的對象。 傳遞一個字串值，指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定PKI運行時選項

   * 建立 `PKIOptions` 對象。
   * 通過調用 `PKIOptions` 對象 `setVerificationTime` 方法和通過 `VerificationTime` 指定驗證時間的枚舉值。
   * 通過調用設定吊銷檢查選項 `PKIOptions` 對象 `setRevocationCheckStyle` 方法和通過 `RevocationCheckStyle` 指定是否執行吊銷檢查的枚舉值。

1. 驗證數字簽名

   通過調用 `SignatureServiceClient` 對象 `verify2` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 包含數字簽名或認證PDF文檔的對象。
   * 表示包含要驗證的簽名的簽名欄位名稱的字串值。
   * A `PKIOptions` 包含PKI運行時選項的對象。
   * A `VerifySPIOptions` 包含SPI資訊的實例。 可以指定 `null` 的子菜單。

   的 `verify2` 方法返回 `PDFSignatureVerificationInfo` 包含可用於驗證數字簽名的資訊的對象。

1. 確定簽名的狀態

   * 通過調用 `PDFSignatureVerificationInfo` 對象 `getStatus` 的雙曲餘切值。 此方法返回 `SignatureStatus` 指定簽名狀態的對象。 例如，如果未修改簽名的PDF文檔，此方法將返回 `SignatureStatus.DocumentSigNoChanges`。

1. 確定簽名者的身份

   * 通過調用 `PDFSignatureVerificationInfo` 對象 `getSigner` 的雙曲餘切值。 此方法返回 `IdentityInformation` 的雙曲餘切值。
   * 調用 `IdentityInformation` 對象 `getStatus` 確定簽名者身份的方法。 此方法返回 `IdentityStatus` 指定標識的枚舉值。 例如，如果簽名者是受信任的，則此方法將返回 `IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[快速啟動（SOAP模式）:使用Java API驗證數字簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API驗證數字簽名 {#verify-digital-signatures-using-the-web-service-api}

使用簽名服務API（Web服務）驗證數字簽名：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 對象。
   * 建立 `SignatureServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `SignatureServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取包含要驗證的簽名的PDF文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存包含要驗證的數字簽名或認證簽名的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性位元組陣列的內容。

1. 設定PKI運行時選項

   * 建立 `PKIOptions` 對象。
   * 通過分配 `PKIOptions` 對象 `verificationTime` 資料成員 `VerificationTime` 指定驗證時間的枚舉值。
   * 通過分配 `PKIOptions` 對象 `revocationCheckStyle` 資料成員 `RevocationCheckStyle` 指定是否執行吊銷檢查的枚舉值。

1. 驗證數字簽名

   通過調用 `SignatureServiceClient` 對象 `verify2` 方法並傳遞以下值：

   * 的 `BLOB` 包含數字簽名或認證PDF文檔的對象。
   * 表示包含要驗證的簽名的簽名欄位名稱的字串值。
   * A `PKIOptions` 包含PKI運行時選項的對象。
   * A `VerifySPIOptions` 包含SPI資訊的實例。 可以指定 `null` 的子菜單。

   的 `verify2` 方法返回 `PDFSignatureVerificationInfo` 包含可用於驗證數字簽名的資訊的對象。

1. 確定簽名的狀態

   通過獲取簽名的 `PDFSignatureVerificationInfo` 對象 `status` 資料成員。 此資料成員儲存 `SignatureStatus` 指定簽名狀態的對象。 例如，如果修改了簽名的PDF文檔， `status` 資料成員儲存值 `SignatureStatus.DocumentSigNoChanges`。

1. 確定簽名者的身份

   * 通過檢索簽名者的 `PDFSignatureVerificationInfo` 對象 `signer` 資料成員。 此成員返回 `IdentityInformation` 的雙曲餘切值。
   * 檢索 `IdentityInformation` 對象 `status` 確定簽名者身份的資料成員。 此資料成員返回 `IdentityStatus` 指定標識的枚舉值。 例如，如果簽名者受信任，則此成員將返回 `IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證多個數字簽名 {#verifying-multiple-digital-signatures}

AEM Forms提供了驗證位於PDF文檔中的所有數字簽名的方法。 假定PDF文檔包含多個數字簽名，因為業務流程需要多個簽名者的簽名。 例如，請考慮要求貸款官員和經理簽名的財務交易。 可以使用簽名服務Java API或Web服務API來驗證PDF文檔中的所有簽名。 驗證多個數字簽名時，可以檢查每個簽名的狀態和屬性。 在信任數字簽名之前，建議您驗證它。 建議您熟悉驗證單個數字簽名。

>[!NOTE]
>
>有關簽名服務和驗證數字簽名的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

要驗證多個數字簽名，請執行以下任務：

1. 包括項目檔案。
1. 建立簽名客戶端。
1. 獲取包含要驗證的簽名的PDF文檔。
1. 設定PKI運行時選項。
1. 檢索所有數字簽名。
1. 循環訪問所有簽名。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，請建立簽名服務客戶端。

**獲取包含要驗證的簽名的PDF文檔**

要驗證用於對PDF文檔進行數字簽名或認證的簽名，請獲取包含簽名的PDF文檔。

**設定PKI運行時選項**

設定簽名服務在驗證PDF文檔中的所有簽名時使用的以下PKI運行時選項：

* 驗證時間
* 吊銷檢查
* 時間戳值

作為設定這些選項的一部分，可以指定驗證時間。 例如，您可以選擇當前時間（驗證程式電腦上的時間），該時間表示使用當前時間。 有關不同時間值的資訊，請參見 `VerificationTime` 枚舉值 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

您還可以指定是否作為驗證過程的一部分執行吊銷檢查。 例如，您可以執行吊銷檢查以確定證書是否被吊銷。 有關吊銷檢查選項的資訊，請參見 `RevocationCheckStyle` 枚舉值 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

要對證書執行吊銷檢查，請使用 `CRLOptionSpec` 的雙曲餘切值。 但是，如果未指定CRL伺服器的URL，簽名服務將從證書獲取該URL。

在執行吊銷檢查時，可以使用聯機證書狀態協定(OCSP)伺服器，而不是使用CRL伺服器。 通常，當使用OCSP伺服器而不是CRL伺服器時，執行吊銷檢查的速度會更快。 (請參閱 [聯機證書狀態協定](https://tools.ietf.org/html/rfc2560)。)

您可以使用Adobe應用程式和服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果在「Adobe應用程式和服務」中首先設定OCSP伺服器，則會檢查OCSP伺服器，然後檢查CRL伺服器。

如果不執行吊銷檢查，簽名服務將不檢查證書是否已吊銷。 即，忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>可以使用 `CRLOptionSpec` 和 `OCSPOptionSpec` 的雙曲餘切值。 例如，要覆蓋CRL伺服器，可以調用 `CRLOptionSpec` 對象 `setLocalURI` 的雙曲餘切值。

時間標籤是跟蹤修改已簽名或已認證文檔的時間的過程。 文檔簽名後，任何人都無法修改它。 時間標籤有助於強制使用已簽名或經認證的文檔。 可以使用 `TSPOptionSpec` 的雙曲餘切值。 例如，可以指定時間戳提供程式(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間設定為 `VerificationTime.CURRENT_TIME` 並且吊銷檢查設定為 `RevocationCheckStyle.BestEffort`。 由於未指定CRL或OCSP伺服器資訊，因此從證書獲取伺服器資訊。

**檢索所有數字簽名**

要驗證位於PDF文檔中的所有數字簽名，請從PDF文檔中檢索數字簽名。 所有簽名都在清單中返回。 作為驗證數字簽名的一部分，請檢查簽名的狀態。

>[!NOTE]
>
>與驗證單個數字簽名不同，驗證多個簽名時，不需要指定簽名欄位名稱。

**循環訪問所有簽名**

循環訪問每個簽名。 即，對於每個簽名，驗證數字簽名，並檢查簽名者的身份和每個簽名的狀態。 (請參閱 [驗證數字簽名](#verify-digital-signatures-using-the-java-api)。)

>[!NOTE]
>
>如果要求是整個文檔，則無需迭代所有簽名。

**另請參閱**

[使用Java API驗證多個數字簽名](#verify-digital-signatures-using-the-java-api)

[使用Web服務API驗證多個數字簽名](#verify-digital-signatures-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證多個數字簽名 {#verify-multiple-digital-signatures-using-the-java-api}

使用簽名服務API(Java)驗證多個數字簽名：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取包含要驗證的簽名的PDF文檔

   * 建立 `java.io.FileInputStream` 表示包含多個數字簽名的PDF文檔的對象，可使用其建構子進行驗證。 傳遞一個字串值，指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定PKI運行時選項

   * 建立 `PKIOptions` 對象。
   * 通過調用 `PKIOptions` 對象 `setVerificationTime` 方法和通過 `VerificationTime` 指定驗證時間的枚舉值。
   * 通過調用設定吊銷檢查選項 `PKIOptions` 對象 `setRevocationCheckStyle` 方法和通過 `RevocationCheckStyle` 指定是否執行吊銷檢查的枚舉值。

1. 檢索所有數字簽名

   調用 `SignatureServiceClient` 對象 `verifyPDFDocument` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 包含包含多個數字簽名的PDF文檔的對象。
   * A `PKIOptions` 包含PKI運行時選項的對象。
   * A `VerifySPIOptions` 包含SPI資訊的實例。 可以指定 `null` 的子菜單。

   的 `verifyPDFDocument` 方法返回 `PDFDocumentVerificationInfo` 包含有關位於PDF文檔中的所有數字簽名的資訊的對象。

1. 循環訪問所有簽名

   * 通過調用 `PDFDocumentVerificationInfo` 對象 `getVerificationInfos` 的雙曲餘切值。 此方法返回 `java.util.List` 其中每個元素為 `PDFSignatureVerificationInfo` 的雙曲餘切值。 使用 `java.util.Iterator` 要在簽名清單中迭代的對象。
   * 使用 `PDFSignatureVerificationInfo` 對象，通過調用 `PDFSignatureVerificationInfo` 對象 `getStatus` 的雙曲餘切值。 此方法返回 `SignatureStatus` 其靜態資料成員通知您簽名的狀態的對象。 例如，如果簽名未知，則此方法返回 `SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數字簽名](#verifying-multiple-digital-signatures)

[快速啟動（SOAP模式）:使用Java API驗證多個數字簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[驗證數字簽名](#verify-digital-signatures-using-the-java-api)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API驗證多個數字簽名 {#verifying-multiple-digital-signatures-using-the-web-service-api}

使用簽名服務API（Web服務）驗證多個數字簽名：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 對象。
   * 建立 `SignatureServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `SignatureServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取包含要驗證的簽名的PDF文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象儲存包含多個數字簽名以驗證的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性位元組陣列的內容。

1. 設定PKI運行時選項

   * 建立 `PKIOptions` 對象。
   * 通過分配 `PKIOptions` 對象 `verificationTime` 資料成員 `VerificationTime` 指定驗證時間的枚舉值。
   * 通過分配 `PKIOptions` 對象 `revocationCheckStyle` 資料成員 `RevocationCheckStyle` 指定是否執行吊銷檢查的枚舉值。

1. 檢索所有數字簽名

   調用 `SignatureServiceClient` 對象 `verifyPDFDocument` 方法並傳遞以下值：

   * A `BLOB` 包含包含多個數字簽名的PDF文檔的對象。
   * A `PKIOptions` 包含PKI運行時選項的對象。
   * A `VerifySPIOptions` 包含SPI資訊的實例。 可以為此參數指定空值。

   的 `verifyPDFDocument` 方法返回 `PDFDocumentVerificationInfo` 包含有關位於PDF文檔中的所有數字簽名的資訊的對象。

1. 循環訪問所有簽名

   * 通過獲取 `PDFDocumentVerificationInfo` 對象 `verificationInfos` 資料成員。 此資料成員返回 `Object` 陣列，其中每個元素是 `PDFSignatureVerificationInfo` 的雙曲餘切值。
   * 使用 `PDFSignatureVerificationInfo` 對象，通過獲取 `PDFSignatureVerificationInfo` 對象 `status` 資料成員。 此資料成員返回 `SignatureStatus` 其靜態資料成員通知您簽名的狀態的對象。 例如，如果簽名未知，則此方法返回 `SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數字簽名](#verifying-multiple-digital-signatures)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 刪除數字簽名 {#removing-digital-signatures}

必須先從簽名欄位中刪除數字簽名，然後才能應用較新的數字簽名。 無法覆蓋數字簽名。 如果嘗試將數字簽名應用於包含簽名的簽名欄位，則會發生異常。

>[!NOTE]
>
>有關簽名服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

要從簽名欄位中刪除數字簽名，請執行以下任務：

1. 包括項目檔案。
1. 建立簽名客戶端。
1. 獲取包含要刪除的簽名的PDF文檔。
1. 從簽名欄位中刪除數字簽名。
1. 將PDF文檔另存為PDF檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名客戶端**

在以寫程式方式執行簽名服務操作之前，必須建立簽名服務客戶端。

**獲取包含要刪除的簽名的PDF文檔**

要從PDF文檔中刪除簽名，必須獲取包含簽名的PDF文檔。

**從簽名欄位中刪除數字簽名**

要成功從PDF文檔中刪除數字簽名，必須指定包含數字簽名的簽名欄位的名稱。 此外，您必須具有刪除數字簽名的權限；否則，會發生異常。

**將PDF文檔另存為PDF檔案**

簽名服務從簽名欄位刪除數字簽名後，您可以將PDF文檔另存為PDF檔案，以便用戶可以在Acrobat或Adobe Reader開啟該文檔。

**另請參閱**

[使用Java API刪除數字簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用Web服務API刪除數字簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API刪除數字簽名 {#remove-digital-signatures-using-the-java-api}

使用簽名API(Java)刪除數字簽名：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-signatures-client.jar。

1. 建立簽名客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `SignatureServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 獲取包含要刪除的簽名的PDF文檔

   * 建立 `java.io.FileInputStream` 表示包含要刪除的簽名的PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 從簽名欄位中刪除數字簽名

   通過調用 `SignatureServiceClient` 對象 `clearSignatureField` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示包含要刪除的簽名的PDF文檔的對象。
   * 一個字串值，它指定包含數字簽名的簽名欄位的名稱。

   的 `clearSignatureField` 方法返回 `com.adobe.idp.Document` 表示從中刪除數字簽名的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `java.io.File` 並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 的雙曲餘切值。 通過 `java.io.File` 對象，以複製 `com.adobe.idp.Document` 對象。 確保使用 `Document` 返回的對象 `clearSignatureField` 的雙曲餘切值。

**另請參閱**

[刪除數字簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速啟動（SOAP模式）:使用Java API刪除數字簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API刪除數字簽名 {#remove-digital-signatures-using-the-web-service-api}

使用簽名API（Web服務）刪除數字簽名：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立簽名客戶端

   * 建立 `SignatureServiceClient` 對象。
   * 建立 `SignatureServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `SignatureServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 獲取包含要刪除的簽名的PDF文檔

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存包含要刪除的數字簽名的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 從簽名欄位中刪除數字簽名

   通過調用 `SignatureServiceClient` 對象 `clearSignatureField` 方法並傳遞以下值：

   * A `BLOB` 包含簽名PDF文檔的對象。
   * 一個字串值，它表示包含要刪除的數字簽名的簽名欄位的名稱。

   的 `clearSignatureField` 方法返回 `BLOB` 表示從中刪除數字簽名的PDF文檔的對象。

1. 將PDF文檔另存為PDF檔案

   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示包含空簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `sign` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用PDF檔案，將位元組陣列的內容寫入 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[刪除數字簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
