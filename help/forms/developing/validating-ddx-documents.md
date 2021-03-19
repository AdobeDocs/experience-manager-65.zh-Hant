---
title: 驗證DDX文檔
seo-title: 驗證DDX文檔
description: 使用Java API和Web Service API以程式設計方式驗證DDX檔案。
seo-description: 使用Java API和Web Service API以程式設計方式驗證DDX檔案。
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---


# 驗證DDX文檔{#validating-ddx-documents}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

可以通過寫程式方式驗證Assembler服務使用的DDX文檔。 也就是說，使用Assembler服務API，可以確定DDX文檔是否有效。 例如，如果您從先前的AEM Forms版本升級，而您想要確保DDX文檔有效，則可以使用Assembler服務API來驗證它。

>[!NOTE]
>
>有關Assembler服務的詳細資訊，請參見[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}摘要

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
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為AEM Forms部署在的J2EE應用程式伺服器專用的JAR檔案。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

要驗證DDX文檔，必須引用現有DDX文檔。

**設定執行時期選項以驗證DDX檔案**

驗證DDX文檔時，必須設定特定的運行時選項，這些選項指示Assembler服務驗證DDX文檔，而不是執行它。 此外，還可以增加Assembler服務寫入日誌檔案的資訊量。

**執行驗證**

建立Assembler服務客戶端、引用DDX文檔並設定運行時選項後，可以調用`invokeDDX`操作來驗證DDX文檔。 驗證DDX文檔時，可以將`null`作為映射參數傳遞（此參數通常儲存匯編程式要求執行DDX文檔中指定的操作的PDF文檔）。

如果驗證失敗，則會拋出異常，而且日誌檔案包含詳細資訊，說明DDX文檔無效的原因，可從`OperationException`實例獲取。 一旦通過基本的XML解析和模式檢查，就會執行對DDX規範的驗證。 DDX文檔中的所有錯誤都在日誌中指定。

**將驗證結果保存到日誌檔案中**

Assembler服務返回可寫入XML日誌檔案的驗證結果。 匯編器服務寫入日誌檔案的詳細程度取決於您設定的運行時選項。

**另請參閱**

[使用Java API驗證DDX檔案](#validate-a-ddx-document-using-the-java-api)

[使用web service API驗證DDX檔案](#validate-a-ddx-document-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#validate-a-ddx-document-using-the-java-api}驗證DDX檔案

使用Assembler Service API(Java)驗證DDX檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 參考現有的DDX檔案。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 設定執行時期選項以驗證DDX檔案。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 設定執行時選項，指示Assembler服務調用`AssemblerOptionSpec`物件的setValidateOnly方法並傳遞`true`來驗證DDX檔案。
   * 調用`AssemblerOptionSpec`物件的`getLogLevel`方法，並傳遞符合您需求的字串值，以設定Assembler服務寫入記錄檔的資訊量。 驗證DDX文檔時，需要將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以傳遞值`FINE`或`FINER`。

1. 執行驗證。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * 代表DDX文檔的`com.adobe.idp.Document`對象。
   * 通常儲存PDF檔案的java.io.Map物件的`null`值。
   * 指定運行時選項的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象。

   `invokeDDX`方法返回`AssemblerResult`對象，該對象包含指定DDX文檔是否有效的資訊。

1. 將驗證結果保存到日誌檔案中。

   * 建立`java.io.File`物件，並確定副檔名為。xml。
   * 叫用`AssemblerResult`物件的`getJobLog`方法。 此方法會傳回包含驗證資訊的`com.adobe.idp.Document`例項。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案。

   >[!NOTE]
   >
   >如果DDX文檔無效，則拋出`OperationException`。 在catch語句中，可以調用`OperationException`對象的`getJobLog`方法。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[快速入門（SOAP模式）:使用Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP模式）驗證DDX檔案

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#validate-a-ddx-document-using-the-web-service-api}驗證DDX檔案

使用Assembler Service API(web service)驗證DDX文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將localhost替換為表單伺服器的IP地址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。
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
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 設定執行時期選項以驗證DDX檔案。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 設定執行時選項，指示Assembler服務將值true指派給`AssemblerOptionSpec`物件的`validateOnly`資料成員，以驗證DDX檔案。
   * 通過為`AssemblerOptionSpec`對象的`logLevel`資料成員分配字串值，設定Assembler服務寫入日誌檔案的資訊量。 方法驗證DDX文檔時，需要將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以指定值`FINE`或`FINER`。 有關可設定的運行時選項的資訊，請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類參考。

1. 執行驗證。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象。
   * 通常儲存PDF文檔的`Map`對象的`null`值。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invokeDDX`方法返回`AssemblerResult`對象，該對象包含指定DDX文檔是否有效的資訊。

1. 將驗證結果保存到日誌檔案中。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示日誌檔案的檔案位置和開啟檔案的模式。 請確定副檔名為。xml。
   * 通過獲取`AssemblerResult`對象的`jobLog`資料成員的值，建立儲存日誌資訊的`BLOB`對象。
   * 建立儲存`BLOB`對象內容的位元組陣列。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

   >[!NOTE]
   >
   >如果DDX文檔無效，則拋出`OperationException`。 在catch語句中，可以獲取`OperationException`對象`jobLog`成員的值。

**另請參閱**

[驗證DDX文檔](#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
