---
title: 組合非互動式PDF檔案
seo-title: 組合非互動式PDF檔案
description: 使用非互動式PDF表單作為輸入，使用Java API和Web Service API來組合非互動式PDF檔案。
seo-description: 使用非互動式PDF表單作為輸入，使用Java API和Web Service API來組合非互動式PDF檔案。
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 0%

---


# 組合非互動式PDF檔案{#assembling-non-interactive-pdf-documents}

當使用互動式PDF表單做為輸入時，您可以組合非互動式PDF檔案。 也就是說，假設您有一個表單，使用者可以使用它在其欄位中輸入資料。 您可以將該表單傳遞至Assembler服務，導致Assembler服務傳回PDF檔案，防止使用者將資料輸入其欄位。 本檔案是非互動式PDF表單。 例如，下圖顯示代表互動式表單的抵押申請。

在本討論中，假設使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

在此DDX文檔中，請注意源屬性被分配了值`inDoc`。 在僅將一個輸入的PDF文檔傳遞給Assembler服務並返回一個PDF文檔，並調用`invokeOneDocument`操作的情況下，請將值`inDoc`分配給PDF源屬性。 調用`invokeOneDocument`操作時，`inDoc`值是必須在DDX文檔中指定的預定義鍵。

相反地，將兩個或兩個以上輸入的PDF文檔傳遞到Assembler服務時，可以調用`invokeDDX`操作。 在這種情況下，請將輸入PDF文檔的檔案名指定給`source`屬性。

此DDX文檔包含`NoXFA`元素，該元素指示Assembler服務返回非互動式PDF文檔。

如果輸入的PDF檔案是以Acrobat表單或靜態XFA表單為基礎，Assembler服務就可以組合非互動式PDF檔案，而AEM輸出服務不會成為表單安裝的一部分。 但是，如果輸入的PDF檔案是動態XFA表單，則輸出服務必須是表單安裝的一AEM部分。 如果在組裝動態XFA表單時，AEM輸出服務不是表單安裝的一部分，則會拋出異常。 請參閱[建立檔案輸出串流](/help/forms/developing/creating-document-output-streams.md)。

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用Assembler服務來組合PDF檔案。 本節不討論概念，例如建立包含輸入檔案的系列物件，或學習如何從傳回的系列物件擷取結果。 （請參閱[程式設計匯整PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)。）

>[!NOTE]
>
>有關Assembler服務的詳細資訊，請參見[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}摘要

若要組合非互動式PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考互動式PDF檔案。
1. 設定執行時期選項。
1. 組合PDF檔案。
1. 儲存非互動式PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為AEM Forms部署在的J2EE應用程式伺服器專用的JAR檔案。

**建立Assembler客戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合PDF檔案。 此DDX文檔必須包含`NoXFA`元素，該元素指示Assembler服務返回非互動式PDF文檔。

**參考互動式PDF檔案**

互動式PDF檔案必須參考並傳遞至Assembler服務，才能取回非互動式PDF檔案。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。

**組合PDF檔案**

建立Assembler服務客戶端後，請參考DDX文檔，參考互動式PDF文檔，並設定運行時選項，您可以調用`invokeOneDocument`操作。 由於只有一個輸入的PDF文檔會傳遞給Assembler服務並返回一個文檔，因此您可以使用`invokeOneDocument`操作，而不使用`invokeDDX`操作。

**儲存非互動式PDF檔案**

如果僅將單一PDF文檔傳遞到Assembler服務，Assembler服務將返回單一文檔，而不是集合對象。 也就是說，調用`invokeOneDocument`操作時，將返回單個文檔。 由於本節中引用的DDX文檔包含建立非互動式PDF文檔的說明，因此Assembler服務返回可另存為PDF檔案的非互動式PDF文檔。

**另請參閱**

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-a-non-interactive-pdf-document-using-the-java-api}組合非互動式PDF檔案

使用Assembler Service API(Java)來組合非互動式PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立Assembler客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 參考現有的DDX檔案。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 參考互動式PDF檔案。

   * 使用其建構函式並傳遞互動式PDF檔案的位置，以建立`java.io.FileInputStream`物件。
   * 建立`com.adobe.idp.Document`物件並傳遞包含PDF檔案的`java.io.FileInputStream`物件。 此`com.adobe.idp.Document`物件會傳遞至`invokeOneDocument`方法。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法，設定運行時選項以滿足您的業務要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法並傳遞`false`。

1. 組合PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeOneDocument`方法並傳遞下列值：

   * 代表DDX文檔的`com.adobe.idp.Document`對象。 請確定此DDX檔案包含PDF來源元素的`inDoc`值。
   * 包含互動式PDF檔案的`com.adobe.idp.Document`物件。
   * 一個`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別。

   `invokeOneDocument`方法會傳回包含非互動式PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存非互動式PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 調用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製至檔案。 請確定您使用`invokeOneDocument`方法傳回的`Document`物件。

* &quot;快速啟動（SOAP模式）:使用Java API組合非互動式PDF檔案」

## 使用web service API {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}組合非互動式PDF檔案

使用Assembler Service API(web service)來組合非互動式PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立Assembler客戶端。

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
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 參考互動式PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存輸入的PDF檔案。 此`BLOB`對象作為參數傳遞給`invokeOneDocument`。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的資料成員分配值，設定運行時選項以滿足您的業務要求。 例如，要指示Assembler服務在出現錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeOneDocument`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象
   * 代表互動式PDF檔案的`BLOB`物件
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeOneDocument`方法會傳回包含非互動式PDF檔案的`BLOB`物件。

1. 儲存非互動式PDF檔案。

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示非互動PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存`invokeOneDocument`方法返回的`BLOB`對象的內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

* 「快速入門(MTOM):使用web service API組合非互動式PDF檔案」。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
