---
title: 組合非互動式PDF檔案
seo-title: Assembling Non-Interactive PDF Documents
description: 使用非互動式PDF表單作為輸入，透過Java API和Web服務API來組合非互動式PDF檔案。
seo-description: Use a non-interactive PDF form as input to assemble a non-interactive PDF document using the Java API and Web Service API.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# 組合非互動式PDF檔案 {#assembling-non-interactive-pdf-documents}

使用互動式PDF表單作為輸入時，您可以組合非互動式PDF檔案。 也就是說，假設您有一個表單，使用者可使用該表單在欄位中輸入資料。 您可以將該表單傳遞給Assembler服務，導致Assembler服務傳回PDF檔案，以防止使用者在其欄位中輸入資料。 本檔案為非互動式PDF表單。 例如，下圖顯示代表互動式表單的貸款應用程式。

為了進行此討論，假設使用下列DDX檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

在此DDX檔案中，請注意已將值指派給來源屬性 `inDoc`. 在只有一個輸入PDF檔案傳遞至Assembler服務且傳回一個PDF檔案的情況下，您呼叫 `invokeOneDocument` 作業，指派值 `inDoc` 至PDF來源屬性。 叫用 `invokeOneDocument` 作業， `inDoc` value是預先定義的索引鍵，必須在DDX檔案中指定。

相反地，將兩個或多個輸入PDF檔案傳遞至組合器服務時，您可以叫用 `invokeDDX` 作業。 在此情況下，將輸入PDF檔案的檔案名稱指派給 `source` 屬性。

此DDX檔案包含 `NoXFA` 元素，指示Assembler服務傳回非互動式PDF檔案。

如果輸入PDF檔案是以Acrobat表單或靜態XFA表單為基礎，則組合器服務可組合非互動式PDF檔案，而輸出服務不會成為AEM表單安裝的一部分。 不過，如果輸入PDF檔案是動態XFA表單，則輸出服務必須是AEM表單安裝的一部分。 組裝動態XFA表單時，如果輸出服務不是AEM表單安裝的一部分，則會擲回例外狀況。 另請參閱 [建立檔案輸出資料流](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>閱讀本節之前，建議您先熟悉使用Assembler服務組合PDF檔案。 本節不討論概念，例如建立包含輸入檔案的集合物件，或學習如何從傳回的集合物件中擷取結果。 (請參閱 [以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

若要組合非互動式PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考互動式PDF檔案。
1. 設定執行階段選項。
1. 組合PDF檔案。
1. 儲存非互動式PDF檔案。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在J2EE應用程式伺服器的JAR檔案。

**建立組合器使用者端**

您必須先建立組合器服務使用者端，才能以程式設計方式執行組合器作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDF檔案。 此DDX檔案必須包含 `NoXFA` 元素，指示Assembler服務傳回非互動式PDF檔案。

**參考互動式PDF檔案**

必須參考互動式PDF檔案並將其傳遞至Assembler服務，才能取回非互動式PDF檔案。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。

**組合PDF檔案**

建立Assembler服務使用者端、參考DDX檔案、參考互動式PDF檔案以及設定執行階段選項之後，您可以叫用 `invokeOneDocument` 作業。 由於只有一個輸入PDF檔案會傳遞至Assembler服務並傳回單一檔案，因此您可以使用 `invokeOneDocument` 作業而非 `invokeDDX` 作業。

**儲存非互動式PDF檔案**

如果只有單一PDF檔案傳遞至Assembler服務，Assembler服務會傳回單一檔案，而非集合物件。 也就是說，叫用 `invokeOneDocument` 作業時，會傳回單一檔案。 由於此區段中所參照的DDX檔案包含建立非互動式PDF檔案的指示，因此Assembler服務會傳回可儲存為PDF檔案的非互動式PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API組合非互動式PDF檔案 {#assemble-a-non-interactive-pdf-document-using-the-java-api}

使用組合器服務API (Java)組合非互動式PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立組合器使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值（指定DDX檔案的位置）來代表DDX檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 參考互動式PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞互動式PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件並傳遞 `java.io.FileInputStream` 包含PDF檔案的物件。 這個 `com.adobe.idp.Document` 物件傳遞至 `invokeOneDocument` 方法。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 使用建構函式來儲存執行階段選項的物件。
   * 透過叫用屬於下列專案的方法，設定執行階段選項以符合您的業務需求 `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用 `AssemblerOptionSpec` 物件的 `setFailOnError` 方法與傳遞 `false`.

1. 組合PDF檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeOneDocument` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 代表DDX檔案的物件。 確定此DDX檔案包含值 `inDoc` (PDF來源元素)。
   * A `com.adobe.idp.Document` 包含互動式PDF檔案的物件。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定執行階段選項（包括預設字型和作業記錄層級）的物件。

   此 `invokeOneDocument` 方法傳回 `com.adobe.idp.Document` 包含非互動式PDF檔案的物件。

1. 儲存非互動式PDF檔案。

   * 建立 `java.io.File` 物件，並確認副檔名為.pdf。
   * 叫用 `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件至檔案。 確定您使用 `Document` 物件， `invokeOneDocument` 方法已傳回。

* 「快速入門（SOAP模式）：使用Java API組合非互動式PDF檔案」

## 使用網站服務API組合非互動式PDF檔案 {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

使用組合器服務API （Web服務）組合非互動式PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 搭配託管AEM Forms之伺服器的IP位址。

1. 建立組合器使用者端。

   * 建立 `AssemblerServiceClient` 物件，使用它的預設建構函式。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `AssemblerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參考現有的DDX檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存DDX檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表DDX檔案檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 透過叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 參考互動式PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存輸入PDF檔案。 這個 `BLOB` 物件傳遞至 `invokeOneDocument` 作為引數。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 透過叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 使用建構函式來儲存執行階段選項的物件。
   * 將值指派給屬於下列專案的資料成員，以設定執行階段選項以符合您的業務需求 `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請指派 `false` 至 `AssemblerOptionSpec` 物件的 `failOnError` 資料成員。

1. 組合PDF檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeOneDocument` 方法並傳遞下列值：

   * A `BLOB` 代表DDX檔案的物件
   * A `BLOB` 代表互動式PDF檔案的物件
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件

   此 `invokeOneDocument` 方法傳回 `BLOB` 包含非互動式PDF檔案的物件。

1. 儲存非互動式PDF檔案。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表非互動式PDF檔案檔案位置的字串值，以及用來開啟檔案的模式。
   * 建立位元組陣列，儲存 `BLOB` 物件， `invokeOneDocument` 方法已傳回。 透過取得 `BLOB` 物件的 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式，然後傳遞 `System.IO.FileStream` 物件。
   * 透過叫用將位元組陣列的內容寫入PDF檔案 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

* 「快速入門(MTOM)：使用網站服務API組合非互動式PDF檔案」。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
