---
title: 驗證DDX文檔
seo-title: Validating DDX Documents
description: 使用Java API和Web服務API以寫程式方式驗證DDX文檔。
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 0%

---

# 驗證DDX文檔 {#validating-ddx-documents}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

可以以寫程式方式驗證匯編器服務使用的DDX文檔。 即，使用匯編程式服務API，可以確定DDX文檔是否有效。 例如，如果您從以前的AEM Forms版本升級，並且希望確保DDX文檔有效，則可以使用匯編程式服務API驗證它。

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要驗證DDX文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立匯編器客戶端。
1. 引用現有DDX文檔。
1. 設定運行時選項以驗證DDX文檔。
1. 執行驗證。
1. 將驗證結果保存到日誌檔案中。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援的J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於AEM Forms部署在其上的J2EE應用程式伺服器的JAR檔案。

**建立PDF匯編器客戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**引用現有DDX文檔**

要驗證DDX文檔，必須引用現有DDX文檔。

**設定運行時選項以驗證DDX文檔**

驗證DDX文檔時，必須設定指示匯編程式服務驗證DDX文檔的特定運行時選項，而不是執行它。 此外，還可以增加匯編程式服務寫入日誌檔案的資訊量。

**執行驗證**

建立匯編程式服務客戶端、引用DDX文檔並設定運行時選項後，可以調用 `invokeDDX` 驗證DDX文檔的操作。 驗證DDX文檔時，可以通過 `null` 映射參數(此參數通常儲存匯編程式執行在DDX文檔中指定的操作所需的PDF文檔)。

如果驗證失敗，則會引發異常，並且日誌檔案包含詳細資訊，解釋DDX文檔無效的原因。 `OperationException` 實例。 經過基本XML分析和模式檢查後，將執行對DDX規範的驗證。 DDX文檔中的所有錯誤都在日誌中指定。

**將驗證結果保存到日誌檔案中**

匯編器服務返回可寫入XML日誌檔案的驗證結果。 匯編程式服務寫入日誌檔案的詳細資訊量取決於您設定的運行時選項。

**另請參閱**

[使用Java API驗證DDX文檔](#validate-a-ddx-document-using-the-java-api)

[使用Web服務API驗證DDX文檔](#validate-a-ddx-document-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API驗證DDX文檔 {#validate-a-ddx-document-using-the-java-api}

使用匯編器服務API(Java)驗證DDX文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用現有DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定DDX檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 設定運行時選項以驗證DDX文檔。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 設定運行時選項，該選項指示匯編器服務通過調用 `AssemblerOptionSpec` 對象的setValidateOnly方法和傳遞 `true`。
   * 通過調用匯編程式服務寫入日誌檔案的資訊量 `AssemblerOptionSpec` 對象 `getLogLevel` 方法和傳遞字串值符合您的要求。 驗證DDX文檔時，您需要將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以傳遞該值 `FINE` 或 `FINER`。

1. 執行驗證。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示DDX文檔的對象。
   * 值 `null` 用於通常儲存PDF文檔的java.io.Map對象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象。

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含指定DDX文檔是否有效的資訊的對象。

1. 將驗證結果保存到日誌檔案中。

   * 建立 `java.io.File` 對象，並確保檔案副檔名為.xml。
   * 調用 `AssemblerResult` 對象 `getJobLog` 的雙曲餘切值。 此方法返回 `com.adobe.idp.Document` 包含驗證資訊的實例。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象。

   >[!NOTE]
   >
   >如果DDX文檔無效，則 `OperationException` 。 在catch語句中，可以調用 `OperationException` 對象 `getJobLog` 的雙曲餘切值。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[快速啟動（SOAP模式）:使用Java API驗證DDX文檔](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP模式）

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API驗證DDX文檔 {#validate-a-ddx-document-using-the-web-service-api}

使用匯編器服務API（Web服務）驗證DDX文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將localhost替換為表單伺服器的IP地址。

1. 建立PDF匯編器客戶端。

   * 建立 `AssemblerServiceClient` 對象。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。
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
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 設定運行時選項以驗證DDX文檔。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 設定運行時選項，該選項指示匯編器服務通過將值true賦給 `AssemblerOptionSpec` 對象 `validateOnly` 資料成員。
   * 通過為匯編程式服務指定字串值，設定匯編程式服務寫入日誌檔案的資訊量 `AssemblerOptionSpec` 對象 `logLevel` 資料成員。 方法驗證DDX文檔時，希望將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，可以指定值 `FINE` 或 `FINER`。 有關可設定的運行時選項的資訊，請參見 `AssemblerOptionSpec` 類引用 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 執行驗證。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象。
   * 值 `null` 為 `Map` 通常儲存PDF文檔的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含指定DDX文檔是否有效的資訊的對象。

1. 將驗證結果保存到日誌檔案中。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示日誌檔案的檔案位置以及在中開啟檔案的模式。 確保檔案副檔名為.xml。
   * 建立 `BLOB` 通過獲取日誌資訊 `AssemblerResult` 對象 `jobLog` 資料成員。
   * 建立一個位元組陣列，用於儲存 `BLOB` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 的子菜單。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

   >[!NOTE]
   >
   >如果DDX文檔無效，則 `OperationException` 。 在catch語句中，可以獲取 `OperationException` 對象 `jobLog` 成員。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
