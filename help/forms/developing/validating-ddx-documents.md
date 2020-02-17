---
title: 驗證DDX文檔
seo-title: 驗證DDX文檔
description: 'null'
seo-description: 'null'
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 驗證DDX文檔 {#validating-ddx-documents}

可以通過寫程式方式驗證Assembler服務使用的DDX文檔。 也就是說，使用Assembler服務API，可以確定DDX文檔是否有效。 例如，如果您從舊版AEM Forms升級，而您想要確保DDX檔案有效，則可使用Assembler服務API來驗證它。

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參 [閱Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要驗證DDX文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立Assembler客戶端。
1. 參考現有的DDX檔案。
1. 設定執行時期選項以驗證DDX檔案。
1. 執行驗證。
1. 將驗證結果保存到日誌檔案中。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如果AEM Forms部署在JBoss以外的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為JAR檔案，而AEM Forms部署在該J2EE應用程式伺服器上。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

要驗證DDX文檔，必須引用現有DDX文檔。

**設定執行時期選項以驗證DDX檔案**

驗證DDX文檔時，必須設定特定的運行時選項，這些選項指示Assembler服務驗證DDX文檔，而不是執行它。 此外，還可以增加Assembler服務寫入日誌檔案的資訊量。

**執行驗證**

建立Assembler服務客戶端、引用DDX文檔並設定運行時選項後，可以調用操 `invokeDDX` 作來驗證DDX文檔。 驗證DDX文檔時，可以作為映射參 `null` 數傳遞（此參數通常儲存匯編器需要執行DDX文檔中指定的操作的PDF文檔）。

如果驗證失敗，則會拋出異常，而日誌檔案包含詳細資訊，說明DDX文檔無效的原因，可以從實例中獲 `OperationException` 取。 一旦通過基本的XML解析和模式檢查，就會執行對DDX規範的驗證。 DDX文檔中的所有錯誤都在日誌中指定。

**將驗證結果保存到日誌檔案中**

Assembler服務返回可寫入XML日誌檔案的驗證結果。 匯編器服務寫入日誌檔案的詳細程度取決於您設定的運行時選項。

**另請參閱**

[使用Java API驗證DDX檔案](#validate-a-ddx-document-using-the-java-api)

[使用web service API驗證DDX檔案](#validate-a-ddx-document-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API驗證DDX檔案 {#validate-a-ddx-document-using-the-java-api}

使用Assembler Service API(Java)驗證DDX檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `AssemblerServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考現有的DDX檔案。

   * 使用 `java.io.FileInputStream` 其建構子並傳遞指定DDX檔案位置的字串值，建立表示DDX文檔的對象。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 設定執行時期選項以驗證DDX檔案。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 設定執行時選項，指示Assembler服務透過叫用物件的setValidateOnly方法並傳 `AssemblerOptionSpec` 遞來驗證DDX檔案 `true`。
   * 調用物件的方法並傳遞符合您需求的字串值，以設定Assembler服務 `AssemblerOptionSpec` 寫入 `getLogLevel` 記錄檔的資訊量。 驗證DDX文檔時，需要將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以傳遞值 `FINE` 或 `FINER`。

1. 執行驗證。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列值：

   * 表 `com.adobe.idp.Document` 示DDX文檔的對象。
   * 通常 `null` 儲存PDF檔案的java.io.Map物件值。
   * 指 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 定運行時選項的對象。
   該方 `invokeDDX` 法返回一 `AssemblerResult` 個包含指定DDX文檔是否有效的資訊的對象。

1. 將驗證結果保存到日誌檔案中。

   * 建立物 `java.io.File` 件，並確定副檔名為。xml。
   * 叫用 `AssemblerResult` 物件的方 `getJobLog` 法。 此方法會傳回包 `com.adobe.idp.Document` 含驗證資訊的例項。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容 `com.adobe.idp.Document` 複製至檔案。
   >[!NOTE]
   >
   >如果DDX文檔無效，則拋 `OperationException` 出一個。 在catch語句中，可以調用對 `OperationException` 像的方 `getJobLog` 法。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP模式）驗證DDX檔案

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API驗證DDX檔案 {#validate-a-ddx-document-using-the-web-service-api}

使用Assembler Service API(web service)驗證DDX文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將localhost替換為表單伺服器的IP地址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其 `AssemblerServiceClient` 預設建構函式建立物件。
   * 使用建 `AssemblerServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。
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
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 設定執行時期選項以驗證DDX檔案。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 設定執行時選項，指示Assembler服務將值true指派給物件的資料成員，以驗證DDX `AssemblerOptionSpec` 文 `validateOnly` 件。
   * 通過為對象的資料成員分配字串值，設定Assembler服務寫入日誌檔案 `AssemblerOptionSpec` 的信 `logLevel` 息量。 方法驗證DDX文檔時，需要將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以指定值 `FINE` 或 `FINER`。 如需您可設定之執行時期選項的詳細資訊，請參閱 `AssemblerOptionSpec`[AEM Forms API參考中的類別參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 執行驗證。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列值：

   * 表 `BLOB` 示DDX文檔的對象。
   * 通常 `null` 儲存PDF文 `Map` 檔的對象的值。
   * 指定 `AssemblerOptionSpec` 運行時選項的對象。
   該方 `invokeDDX` 法返回一 `AssemblerResult` 個包含指定DDX文檔是否有效的資訊的對象。

1. 將驗證結果保存到日誌檔案中。

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示日誌檔案的檔案位置以及開啟檔案的模式。 請確定副檔名為。xml。
   * 透過 `BLOB` 取得物件資料成員的值，建立儲存記錄 `AssemblerResult` 資訊的 `jobLog` 物件。
   * 建立儲存物件內容的位元組 `BLOB` 陣列。 取得物件欄位的值，以填入 `BLOB` 位元組陣 `MTOM` 列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。
   >[!NOTE]
   >
   >如果DDX文檔無效，則拋 `OperationException` 出一個。 在catch語句中，可以獲取對象成 `OperationException` 員的值 `jobLog` 。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
