---
title: 驗證DDX檔案
description: 使用Java API和網站服務API，以程式設計方式驗證DDX檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 0%

---

# 驗證DDX檔案 {#validating-ddx-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以程式化方式驗證組合器服務所使用的DDX檔案。 也就是說，您可以使用組合器服務API來判斷DDX檔案是否有效。 例如，如果您從舊版AEM Forms升級，並且想確保DDX檔案有效，則可使用組合器服務API來驗證。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱[組合器服務與DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

若要驗證DDX檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立組合器使用者端。
1. 參考現有的DDX檔案。
1. 設定執行階段選項以驗證DDX檔案。
1. 執行驗證。
1. 將驗證結果儲存在記錄檔中。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在J2EE應用程式伺服器的JAR檔案。

**建立PDF組合器使用者端**

您必須先建立組合器服務使用者端，才能以程式設計方式執行組合器作業。

**參考現有的DDX檔案**

若要驗證DDX檔案，您必須參考現有的DDX檔案。

**設定執行階段選項以驗證DDX檔案**

驗證DDX檔案時，您必須設定特定的執行階段選項，以指示Assembler服務驗證DDX檔案，而不是執行。 此外，您也可以增加Assembler服務寫入記錄檔的資訊量。

**執行驗證**

建立Assembler服務使用者端、參考DDX檔案並設定執行階段選項之後，您可以叫用`invokeDDX`作業來驗證DDX檔案。 驗證DDX檔案時，您可以傳遞`null`作為對應引數(此引數通常會儲存組合器執行DDX檔案中指定之作業所需的PDF檔案)。

如果驗證失敗，則會擲回例外狀況，而記錄檔會包含詳細資訊，說明為何可從`OperationException`執行個體取得DDX檔案無效。 一旦通過基本的XML剖析和結構描述檢查，就會根據DDX規格執行驗證。 DDX檔案中的所有錯誤都在記錄中指定。

**將驗證結果儲存在記錄檔中**

組合器服務會傳回您可以寫入XML記錄檔的驗證結果。 Assembler服務寫入記錄檔的詳細資訊量，取決於您設定的執行階段選項。

**另請參閱**

[使用Java API驗證DDX檔案](#validate-a-ddx-document-using-the-java-api)

[使用網站服務API驗證DDX檔案](#validate-a-ddx-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API驗證DDX檔案 {#validate-a-ddx-document-using-the-java-api}

使用組合器服務API (Java)驗證DDX檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`AssemblerServiceClient`物件。

1. 參考現有的DDX檔案。

   * 使用它的建構函式並傳遞指定DDX檔案位置的字串值，建立代表DDX檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 設定執行階段選項以驗證DDX檔案。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 透過叫用`AssemblerOptionSpec`物件的setValidateOnly方法並傳遞`true`，設定執行階段選項，指示Assembler服務驗證DDX檔案。
   * 透過叫用`AssemblerOptionSpec`物件的`getLogLevel`方法並傳遞符合您要求的字串值，設定Assembler服務寫入記錄檔的資訊量。 驗證DDX檔案時，您想要將更多資訊寫入記錄檔，以協助進行驗證程式。 因此，您可以傳遞值`FINE`或`FINER`。

1. 執行驗證。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列值：

   * 代表DDX檔案的`com.adobe.idp.Document`物件。
   * 通常儲存PDF檔案的java.io.Map物件的值`null`。
   * 指定執行階段選項的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件。

   `invokeDDX`方法傳回`AssemblerResult`物件，其中包含指定DDX檔案是否有效的資訊。

1. 將驗證結果儲存在記錄檔中。

   * 建立`java.io.File`物件，並確定副檔名為.xml。
   * 叫用`AssemblerResult`物件的`getJobLog`方法。 此方法會傳回包含驗證資訊的`com.adobe.idp.Document`執行個體。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案。

   >[!NOTE]
   >
   >如果DDX檔案無效，則會擲回`OperationException`。 在catch陳述式中，您可以叫用`OperationException`物件的`getJobLog`方法。

**另請參閱**

[驗證DDX檔案](#validating-ddx-documents)

[快速入門(SOAP模式)：使用Java API驗證DDX檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (SOAP模式)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API驗證DDX檔案 {#validate-a-ddx-document-using-the-web-service-api}

使用組合器服務API （Web服務）驗證DDX檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以Forms伺服器的IP位址取代localhost。

1. 建立PDF組合器使用者端。

   * 使用預設建構函式建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。
   * 取得`AssemblerServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存DDX檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表DDX檔案檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。

1. 設定執行階段選項以驗證DDX檔案。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 將值true指派給`AssemblerOptionSpec`物件的`validateOnly`資料成員，以設定執行階段選項，指示Assembler服務驗證DDX檔案。
   * 將字串值指派給`AssemblerOptionSpec`物件的`logLevel`資料成員，以設定Assembler服務寫入記錄檔的資訊量。 方法驗證DDX檔案時，您想要將更多資訊寫入記錄檔，以協助進行驗證程式。 因此，您可以指定值`FINE`或`FINER`。 如需您可以設定的執行階段選項相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

1. 執行驗證。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列值：

   * 代表DDX檔案的`BLOB`物件。
   * 通常儲存PDF檔案的`Map`物件的值`null`。
   * 指定執行階段選項的`AssemblerOptionSpec`物件。

   `invokeDDX`方法傳回`AssemblerResult`物件，其中包含指定DDX檔案是否有效的資訊。

1. 將驗證結果儲存在記錄檔中。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表記錄檔之檔案位置的字串值，以及開啟檔案的模式。 確認副檔名為.xml。
   * 取得`AssemblerResult`物件的`jobLog`資料成員的值，建立儲存記錄資訊的`BLOB`物件。
   * 建立位元組陣列以儲存`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

   >[!NOTE]
   >
   >如果DDX檔案無效，則會擲回`OperationException`。 在catch陳述式中，您可以取得`OperationException`物件的`jobLog`成員的值。

**另請參閱**

[驗證DDX檔案](#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
