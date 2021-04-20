---
title: 以程式設計方式解譯PDF檔案
seo-title: 以程式設計方式解譯PDF檔案
description: 使用Assembler服務，使用Java API和Web Service API，將單一PDF檔案反匯編為多個PDF檔案。
seo-description: 使用Assembler服務，使用Java API和Web Service API，將單一PDF檔案反匯編為多個PDF檔案。
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 0%

---


# 以程式設計方式解譯PDF檔案{#programmatically-disassembling-pdf-documents}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

您可以將PDF檔案傳遞至Assembler服務，以反匯編檔案。 通常，當PDF檔案最初是由許多個別檔案（例如陳述式集合）建立時，這項工作很有用。 在下圖中，DocA被分成多個結果文檔，其中頁面上的第一級書籤標識新結果文檔的開始。

![pd_pd_pdf來自書籤](assets/pd_pd_pdfsfrombookmarks.png)

若要拆解PDF檔案，請確定`PDFsFromBookmarks`元素位於DDX檔案中。 `PDFsFromBookmarks`元素是合成元素，只能是`DDX`元素的子元素。 它沒有`result`屬性，因為它可導致生成多個文檔。

`PDFsFromBookmarks`元素會針對來源檔案中的每個1級書籤產生單一檔案。

在本討論中，假設使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用Assembler服務來組合PDF檔案。 （請參閱[程式設計匯整PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)。）

>[!NOTE]
>
>將單一PDF文檔傳遞至Assembler服務並返回單一文檔時，可以調用`invokeOneDocument`操作。 但是，要反匯編PDF文檔，請使用`invokeDDX`操作，因為雖然一個輸入的PDF文檔被傳遞到Assembler服務，但Assembler服務返回包含一個或多個文檔的集合對象。

>[!NOTE]
>
>有關Assembler服務的詳細資訊，請參見[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}摘要

要拆解PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考要反匯編的PDF文檔。
1. 設定執行時期選項。
1. 反匯編PDF檔案。
1. 儲存已拆解的PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar替換為特定於部署了AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案，才能反匯編PDF檔案。 此DDX文檔必須包含`PDFsFromBookmarks`元素。

**參考PDF檔案以反匯編**

要反匯編PDF文檔，請參考表示要反匯編的PDF文檔的PDF檔案。 傳遞至Assembler服務時，會針對檔案中的每個第1級書籤傳回個別的PDF檔案。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。

**反匯編PDF檔案**

在您建立Assembler服務用戶端、參考DDX檔案、參考要反匯編的PDF檔案，並設定執行時期選項後，您就可以叫用`invokeDDX`方法來反匯編PDF檔案。 如果DDX檔案包含反匯編PDF檔案的指示，Assembler服務會在收集物件中傳回已拆解的PDF檔案。

**儲存已拆解的PDF檔案**

所有已拆解的PDF檔案都會傳回至系列物件中。 逐步處理系列物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#disassemble-a-pdf-document-using-the-java-api}解譯PDF檔案

使用Assembler Service API(Java)拆解PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 參考現有的DDX檔案。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 參考要反匯編的PDF文檔。

   * 使用`HashMap`建構函式建立`java.util.Map`物件，用來儲存輸入的PDF檔案。
   * 使用其建構函式建立`java.io.FileInputStream`物件，並將PDF檔案的位置傳遞至反匯編。
   * 建立`com.adobe.idp.Document`物件，並傳遞包含要反匯編之PDF檔案的`java.io.FileInputStream`物件。
   * 通過調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
      * 包含要反匯編的PDF文檔的`com.adobe.idp.Document`對象。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法，設定運行時選項以滿足您的業務要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法並傳遞`false`。

1. 反匯編PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列必要值：

   * `com.adobe.idp.Document`物件，代表要使用的DDX檔案
   * 包含要反匯編的PDF文檔的`java.util.Map`對象
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件，指定執行時間選項，包括預設字型和工作記錄層級

   `invokeDDX`方法會傳回`com.adobe.livecycle.assembler.client.AssemblerResult`物件，其中包含已拆解的PDF檔案和發生的任何例外。

1. 儲存已拆解的PDF檔案。

   要獲取已拆解的PDF文檔，請執行以下操作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 重複`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

**另請參閱**

[以程式設計方式解譯PDF檔案](#programmatically-disassembling-pdf-documents)

[快速入門（SOAP模式）:使用Java API解譯PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#disassemble-a-pdf-document-using-the-web-service-api}解譯PDF檔案

使用Assembler Service API(web service)拆解PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

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
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，該值代表DDX檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 參考要反匯編的PDF文檔。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存輸入的PDF檔案。 此`BLOB`對象作為參數傳遞給`invokeOneDocument`。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容，填充`BLOB`對象。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`對象。 此收集物件用來儲存要反匯編的PDF。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`key`欄位指派代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
   * 將儲存PDF檔案的`BLOB`物件指派至`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`欄位。
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`對象添加到`MyMapOf_xsd_string_To_xsd_anyType`對象。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的資料成員分配值，設定運行時選項以滿足您的業務要求。 例如，要指示Assembler服務在出現錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`欄位。

1. 反匯編PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * `BLOB`物件，代表DDX檔案，該檔案會分解PDF檔案
   * 包含要反匯編的PDF文檔的`MyMapOf_xsd_string_To_xsd_anyType`對象
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業結果和發生的任何例外。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是包含已拆解PDF檔案的`Map`物件。
   * 重複`Map`物件，以取得每個結果檔案。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 存取PDF檔案的`BLOB`物件的`MTOM`屬性，擷取代表PDF檔案的二進位資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[以程式設計方式解譯PDF檔案](#programmatically-disassembling-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
