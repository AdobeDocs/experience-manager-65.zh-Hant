---
title: 驗證DDX文檔
seo-title: 驗證DDX文檔
description: 使用Java API和網站服務API以程式設計方式驗證DDX檔案。
seo-description: 使用Java API和網站服務API以程式設計方式驗證DDX檔案。
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
source-wordcount: '1543'
ht-degree: 0%

---

# 驗證DDX文檔{#validating-ddx-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

可以用寫程式方式驗證組合器服務使用的DDX文檔。 也就是說，使用組合器服務API，可以確定DDX文檔是否有效。 例如，如果您從以前的AEM Forms版本升級，並且希望確保DDX文檔有效，則可以使用組合器服務API來驗證它。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}的摘要

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

建立組合器服務客戶端、引用DDX文檔並設定運行時選項後，可以調用`invokeDDX`操作來驗證DDX文檔。 驗證DDX文檔時，可以傳遞`null`作為映射參數（此參數通常儲存匯編器執行DDX文檔中指定的操作所需的PDF文檔）。

如果驗證失敗，則會引發異常，並且日誌檔案包含詳細資訊，說明為何DDX文檔無效，可從`OperationException`實例獲取。 一旦通過基本XML解析和架構檢查，就會執行對DDX規範的驗證。 DDX文檔中的所有錯誤都在日誌中指定。

**將驗證結果保存在日誌檔案中**

組合器服務返回可寫入XML日誌檔案的驗證結果。 組合器服務寫入日誌檔案的詳細程度取決於您設定的運行時選項。

**另請參閱**

[使用Java API驗證DDX檔案](#validate-a-ddx-document-using-the-java-api)

[使用網站服務API驗證DDX檔案](#validate-a-ddx-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#validate-a-ddx-document-using-the-java-api}驗證DDX文檔

使用組合器服務API(Java)驗證DDX文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 參考現有的DDX文檔。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 設定運行時選項以驗證DDX文檔。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 設定運行時間選項，該選項指示組合器服務通過調用`AssemblerOptionSpec`對象的setValidateOnly方法並傳遞`true`來驗證DDX文檔。
   * 通過調用`AssemblerOptionSpec`對象的`getLogLevel`方法並傳遞字串值來設定組合器服務寫入日誌檔案的資訊量，該資訊量滿足您的要求。 驗證DDX文檔時，需要將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以傳遞值`FINE`或`FINER`。

1. 執行驗證。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * 代表DDX文檔的`com.adobe.idp.Document`對象。
   * 通常儲存PDF文檔的java.io.Map對象的值`null`。
   * 指定運行時選項的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象。

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含指定DDX文檔是否有效的資訊。

1. 將驗證結果保存在日誌檔案中。

   * 建立`java.io.File`物件，並確定副檔名為.xml。
   * 調用`AssemblerResult`對象的`getJobLog`方法。 此方法會傳回包含驗證資訊的`com.adobe.idp.Document`例項。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案。

   >[!NOTE]
   >
   >如果DDX文檔無效，則擲回`OperationException`。 在catch陳述式中，可以調用`OperationException`對象的`getJobLog`方法。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP模式）驗證DDX檔案

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#validate-a-ddx-document-using-the-web-service-api}驗證DDX文檔

使用組合器服務API（Web服務）驗證DDX文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >用表單伺服器的IP地址替換localhost。

1. 建立PDF組合器客戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。
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
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 設定運行時選項以驗證DDX文檔。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 設定運行時間選項，該選項指示組合器服務通過將值true分配給`AssemblerOptionSpec`對象的`validateOnly`資料成員來驗證DDX文檔。
   * 通過將字串值分配給`AssemblerOptionSpec`對象的`logLevel`資料成員，設定組合器服務寫入日誌檔案的資訊量。 方法驗證DDX文檔時，您希望將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以指定值`FINE`或`FINER`。 如需可設定的執行階段選項相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

1. 執行驗證。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象。
   * 通常儲存PDF文檔的`Map`對象的值`null`。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含指定DDX文檔是否有效的資訊。

1. 將驗證結果保存在日誌檔案中。

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示日誌檔案的檔案位置以及在中開啟檔案的模式。 請確定副檔名為.xml。
   * 通過獲取`AssemblerResult`對象的`jobLog`資料成員的值，建立儲存日誌資訊的`BLOB`對象。
   * 建立儲存`BLOB`對象內容的位元組陣列。 獲取`BLOB`對象的`MTOM`欄位的值，填入位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

   >[!NOTE]
   >
   >如果DDX文檔無效，則擲回`OperationException`。 在catch語句中，可以獲取`OperationException`對象的`jobLog`成員的值。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
