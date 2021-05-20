---
title: 組合非互動式PDF檔案
seo-title: 組合非互動式PDF檔案
description: 使用非互動式PDF表單作為輸入，使用Java API和Web服務API來組合非互動式PDF檔案。
seo-description: 使用非互動式PDF表單作為輸入，使用Java API和Web服務API來組合非互動式PDF檔案。
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 0%

---

# 組合非互動式PDF文檔{#assembling-non-interactive-pdf-documents}

使用互動式PDF表單作為輸入時，您可以組合非互動式PDF檔案。 也就是說，假設您有一個表單，使用者可使用該表單在其欄位中輸入資料。 您可以將表單傳遞至組合器服務，導致組合器服務返回PDF文檔，該文檔阻止用戶將資料輸入到其欄位中。 此文檔是非互動式PDF表單。 例如，下圖顯示代表互動式表單的抵押申請。

在本討論中，假定使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

在此DDX文檔中，請注意源屬性被分配了值`inDoc`。 在僅將一個輸入的PDF文檔傳遞到組合器服務並返回一個PDF文檔，並調用`invokeOneDocument`操作的情況下，將值`inDoc`分配給PDF源屬性。 調用`invokeOneDocument`操作時，`inDoc`值是必須在DDX文檔中指定的預定義鍵。

相反，將兩個或兩個以上輸入的PDF文檔傳遞到組合器服務時，可以調用`invokeDDX`操作。 在此情況下，將輸入PDF文檔的檔案名分配給`source`屬性。

此DDX文檔包含`NoXFA`元素，該元素指示組合器服務返回非互動式PDF文檔。

如果輸入的PDF檔案是以Acrobat表單或靜態XFA表單為基礎，則組合器服務可以組合非互動式PDF檔案，而輸出服務不是AEM表單安裝的一部分。 不過，如果輸入的PDF檔案是動態XFA表單，則輸出服務必須是AEM表單安裝的一部分。 如果組裝動態XFA表單時，輸出服務不屬於AEM表單安裝的一部分，則會擲回例外狀況。 請參閱[建立文檔輸出流](/help/forms/developing/creating-document-output-streams.md)。

>[!NOTE]
>
>閱讀本節之前，建議您先熟悉使用組合器服務組合PDF文檔。 本節不討論概念，例如建立包含輸入文檔的集合對象，或了解如何從返回的集合對象中提取結果。 （請參閱[以程式設計方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)。）

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}的摘要

要組合非互動式PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考互動式PDF檔案。
1. 設定運行時選項。
1. 組合PDF文檔。
1. 儲存非互動式PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為AEM Forms所部署之J2EE應用程式伺服器專屬的JAR檔案。

**建立組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

必須參考DDX文檔才能組合PDF文檔。 此DDX文檔必須包含`NoXFA`元素，該元素指示組合器服務返回非互動式PDF文檔。

**參考互動式PDF檔案**

必須引用互動式PDF文檔並將其傳遞到組合器服務，才能返回非互動式PDF文檔。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。

**組合PDF檔案**

建立組合器服務客戶端、引用DDX文檔、引用互動式PDF文檔和設定運行時選項後，可以調用`invokeOneDocument`操作。 因為只有一個輸入的PDF文檔會傳遞到組合器服務，並且返回了單個文檔，所以可以使用`invokeOneDocument`操作，而不是使用`invokeDDX`操作。

**儲存非互動式PDF檔案**

如果僅將單個PDF文檔傳遞到組合器服務，組合器服務將返回單個文檔，而不是集合對象。 也就是說，調用`invokeOneDocument`操作時，返回單個文檔。 由於本節中引用的DDX文檔包含建立非互動式PDF文檔的說明，因此組合器服務返回可另存為PDF檔案的非互動式PDF文檔。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-a-non-interactive-pdf-document-using-the-java-api}組合非互動式PDF檔案

使用組合器服務API(Java)組合非互動式PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 參考現有的DDX文檔。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 參考互動式PDF檔案。

   * 使用其建構子並傳遞互動式PDF檔案的位置，以建立`java.io.FileInputStream`物件。
   * 建立`com.adobe.idp.Document`物件並傳遞包含PDF檔案的`java.io.FileInputStream`物件。 此`com.adobe.idp.Document`物件會傳遞至`invokeOneDocument`方法。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法來設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用`AssemblerOptionSpec`對象的`setFailOnError`方法並傳遞`false`。

1. 組合PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeOneDocument`方法並傳遞以下值：

   * 代表DDX文檔的`com.adobe.idp.Document`對象。 確保此DDX文檔包含PDF源元素的`inDoc`值。
   * 包含互動式PDF檔案的`com.adobe.idp.Document`物件。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別。

   `invokeOneDocument`方法返回包含非互動式PDF文檔的`com.adobe.idp.Document`對象。

1. 儲存非互動式PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 調用`Document`對象的`copyToFile`方法，將`Document`對象的內容複製到檔案。 請確定您使用`invokeOneDocument`方法傳回的`Document`物件。

* &quot;快速入門（SOAP模式）:使用Java API組裝非互動式PDF檔案」

## 使用Web服務API {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}組合非互動式PDF文檔

使用組合器服務API（Web服務）組合非互動式PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立組合器客戶端。

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
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 參考互動式PDF檔案。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存輸入的PDF文檔。 此`BLOB`物件會以引數的形式傳遞至`invokeOneDocument`。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 為屬於`AssemblerOptionSpec`對象的資料成員分配值，以設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeOneDocument`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象
   * 代表互動式PDF檔案的`BLOB`物件
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeOneDocument`方法返回包含非互動式PDF文檔的`BLOB`對象。

1. 儲存非互動式PDF檔案。

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示非互動式PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存`invokeOneDocument`方法返回的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`欄位的值，填入位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

* 「快速入門(MTOM):使用Web服務API組裝非互動式PDF檔案」。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
