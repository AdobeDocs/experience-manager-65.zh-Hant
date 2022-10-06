---
title: 驗證DDX文檔
seo-title: Validating DDX Documents
description: 使用Java API和網站服務API以程式設計方式驗證DDX檔案。
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

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

可以用寫程式方式驗證組合器服務使用的DDX文檔。 也就是說，使用組合器服務API，可以確定DDX文檔是否有效。 例如，如果您從以前的AEM Forms版本升級，並且希望確保DDX文檔有效，則可以使用組合器服務API來驗證它。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

要驗證DDX文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立組合器客戶端。
1. 參考現有的DDX文檔。
1. 設定運行時選項以驗證DDX文檔。
1. 執行驗證。
1. 將驗證結果保存在日誌檔案中。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為AEM Forms所部署之J2EE應用程式伺服器專屬的JAR檔案。

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

要驗證DDX文檔，必須參考現有DDX文檔。

**設定運行時選項以驗證DDX文檔**

驗證DDX文檔時，必須設定特定的運行時選項，這些選項指示組合器服務驗證DDX文檔，而不執行它。 此外，您還可以增加組合器服務寫入日誌檔案的資訊量。

**執行驗證**

建立組合器服務客戶端、引用DDX文檔並設定運行時選項後，可以調用 `invokeDDX` 驗證DDX文檔的操作。 驗證DDX文檔時，可以傳遞 `null` 作為映射參數(此參數通常儲存PDF文檔，組合器需要這些文檔執行在DDX文檔中指定的操作)。

如果驗證失敗，則會擲回例外，且記錄檔包含詳細資訊，說明為何DDX檔案無效，可從 `OperationException` 例項。 一旦通過基本XML解析和架構檢查，就會執行對DDX規範的驗證。 DDX文檔中的所有錯誤都在日誌中指定。

**將驗證結果保存在日誌檔案中**

組合器服務返回可寫入XML日誌檔案的驗證結果。 組合器服務寫入日誌檔案的詳細程度取決於您設定的運行時選項。

**另請參閱**

[使用Java API驗證DDX檔案](#validate-a-ddx-document-using-the-java-api)

[使用網站服務API驗證DDX檔案](#validate-a-ddx-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API驗證DDX檔案 {#validate-a-ddx-document-using-the-java-api}

使用組合器服務API(Java)驗證DDX文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞指定DDX檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 設定運行時選項以驗證DDX文檔。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 設定運行時間選項，該選項指示組合器服務通過調用 `AssemblerOptionSpec` 對象的setValidateOnly方法和傳遞 `true`.
   * 通過調用 `AssemblerOptionSpec` 物件 `getLogLevel` 方法和傳遞字串值符合您的需求。 驗證DDX文檔時，需要將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以傳遞值 `FINE` 或 `FINER`.

1. 執行驗證。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 表示DDX文檔的對象。
   * 值 `null` 用於通常儲存PDF檔案的java.io.Map物件。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象。

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含指定DDX文檔是否有效的資訊的對象。

1. 將驗證結果保存在日誌檔案中。

   * 建立 `java.io.File` 物件，並確定副檔名為.xml。
   * 叫用 `AssemblerResult` 物件 `getJobLog` 方法。 此方法會傳回 `com.adobe.idp.Document` 包含驗證資訊的例項。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 物件。

   >[!NOTE]
   >
   >如果DDX檔案無效，則 `OperationException` 被擲回。 在catch陳述式中，您可以叫用 `OperationException` 物件 `getJobLog` 方法。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[快速入門（SOAP模式）:使用Java API驗證DDX檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP模式）

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API驗證DDX檔案 {#validate-a-ddx-document-using-the-web-service-api}

使用組合器服務API（Web服務）驗證DDX文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >用表單伺服器的IP地址替換localhost。

1. 建立PDF組合器客戶端。

   * 建立 `AssemblerServiceClient` 物件，使用其預設建構函式。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時，會使用此屬性。
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
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。

1. 設定運行時選項以驗證DDX文檔。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 設定運行時間選項，該選項指示組合器服務通過將值true指定給 `AssemblerOptionSpec` 物件 `validateOnly` 資料成員。
   * 通過為 `AssemblerOptionSpec` 物件 `logLevel` 資料成員。 方法驗證DDX文檔時，您希望將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以指定值 `FINE` 或 `FINER`. 如需可設定的執行階段選項相關資訊，請參閱 `AssemblerOptionSpec` 類引用 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 執行驗證。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列值：

   * A `BLOB` 表示DDX文檔的對象。
   * 值 `null` 針對 `Map` 通常儲存PDF文檔的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含指定DDX文檔是否有效的資訊的對象。

1. 將驗證結果保存在日誌檔案中。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子，並傳遞一個字串值，該字串值表示日誌檔案的檔案位置，以及在中開啟檔案的模式。 請確定副檔名為.xml。
   * 建立 `BLOB` 透過取得 `AssemblerResult` 物件 `jobLog` 資料成員。
   * 建立位元組陣列，用於儲存 `BLOB` 物件。 取得 `BLOB` 物件 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

   >[!NOTE]
   >
   >如果DDX檔案無效，則 `OperationException` 被擲回。 在catch陳述式中，您可以取得 `OperationException` 物件 `jobLog` 成員。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
