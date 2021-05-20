---
title: 以程式設計方式解譯PDF檔案
seo-title: 以程式設計方式解譯PDF檔案
description: 使用組合器服務，使用Java API和Web服務API將單個PDF文檔拆解為多個PDF文檔。
seo-description: 使用組合器服務，使用Java API和Web服務API將單個PDF文檔拆解為多個PDF文檔。
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 0%

---

# 以寫程式方式分解PDF文檔{#programmatically-disassembling-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

通過將PDF文檔傳遞到組合器服務，可以拆解該文檔。 通常，當PDF文檔最初從許多單獨文檔（如語句集合）建立時，此任務非常有用。 在下圖中，DocA被分為多個結果文檔，其中頁面上的第一級書籤標識新結果文檔的開始。

![pd_pd_pdf從書籤](assets/pd_pd_pdfsfrombookmarks.png)

要拆解PDF文檔，請確保`PDFsFromBookmarks`元素位於DDX文檔中。 `PDFsFromBookmarks`元素是結果元素，只能是`DDX`元素的子元素。 它沒有`result`屬性，因為它可能導致生成多個文檔。

`PDFsFromBookmarks`元素會為源文檔中的每個1級書籤生成單個文檔。

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
>閱讀本節之前，建議您熟悉使用組合器服務來組合PDF文檔。 （請參閱[以程式設計方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)。）

>[!NOTE]
>
>將單個PDF文檔傳遞到組合器服務並返回單個文檔時，可以調用`invokeOneDocument`操作。 但是，要拆解PDF文檔，請使用`invokeDDX`操作，因為雖然一個輸入的PDF文檔被傳遞到組合器服務，但組合器服務返回一個包含一個或多個文檔的集合對象。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}的摘要

要拆解PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考要拆卸的PDF文檔。
1. 設定運行時選項。
1. 反匯編PDF文檔。
1. 儲存已拆解的PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

必須參考DDX文檔才能拆解PDF文檔。 此DDX文檔必須包含`PDFsFromBookmarks`元素。

**參考要拆卸的PDF文檔**

要拆解PDF文檔，請參照表示要拆解的PDF文檔的PDF檔案。 當傳遞到組合器服務時，將為文檔中的每個級別1書籤返回一個單獨的PDF文檔。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。

**反匯編PDF文檔**

建立組合器服務客戶端後，參考DDX文檔，參考要拆解的PDF文檔，並設定運行時選項，可以通過調用`invokeDDX`方法來拆解PDF文檔。 如果DDX文檔包含拆解PDF文檔的說明，則組合器服務會在收集對象中返回已拆解的PDF文檔。

**儲存已拆解的PDF檔案**

所有已拆解的PDF文檔都在收集對象中返回。 逐一查看集合物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#disassemble-a-pdf-document-using-the-java-api}拆解PDF文檔

使用組合器服務API(Java)拆解PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 參考現有的DDX文檔。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 參考要拆卸的PDF文檔。

   * 使用`HashMap`建構子建立用於儲存輸入PDF文檔的`java.util.Map`對象。
   * 使用其建構子並將PDF檔案的位置傳遞至反匯編，以建立`java.io.FileInputStream`物件。
   * 建立`com.adobe.idp.Document`對象，並傳遞包含要拆解的PDF文檔的`java.io.FileInputStream`對象。
   * 調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象中：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
      * `com.adobe.idp.Document`物件，包含要拆解的PDF檔案。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法來設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用`AssemblerOptionSpec`對象的`setFailOnError`方法並傳遞`false`。

1. 反匯編PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下必需值：

   * 表示要使用的DDX文檔的`com.adobe.idp.Document`對象
   * 包含要拆解的PDF文檔的`java.util.Map`對象
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別

   `invokeDDX`方法返回一個`com.adobe.livecycle.assembler.client.AssemblerResult`對象，該對象包含已拆解的PDF文檔以及發生的任何異常。

1. 儲存已拆解的PDF檔案。

   要獲取已拆解的PDF文檔，請執行以下操作：

   * 調用`AssemblerResult`對象的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 對`java.util.Map`對象進行迭代，直到找到結果`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取PDF文檔。

**另請參閱**

[以程式設計方式解譯PDF檔案](#programmatically-disassembling-pdf-documents)

[快速入門（SOAP模式）:使用Java API解譯PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#disassemble-a-pdf-document-using-the-web-service-api}拆解PDF文檔

使用組合器服務API（web服務）拆解PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 在設定服務引用時，請確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

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
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示DDX文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 參考要拆卸的PDF文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存輸入的PDF文檔。 此`BLOB`物件會以引數的形式傳遞至`invokeOneDocument`。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此集合對象用於儲存要拆解的PDF。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配表示鍵名的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
   * 將儲存PDF文檔的`BLOB`對象指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象&#39; `Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 為屬於`AssemblerOptionSpec`對象的資料成員分配值，以設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`欄位。

1. 反匯編PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * `BLOB`對象，表示拆分PDF文檔的DDX文檔
   * 包含要反匯編的PDF文檔的`MyMapOf_xsd_string_To_xsd_anyType`對象
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業結果和發生的任何異常。

1. 儲存已拆解的PDF檔案。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問`AssemblerResult`對象的`documents`欄位，該欄位是包含已拆解的PDF文檔的`Map`對象。
   * 逐一查看`Map`對象，以獲取每個結果文檔。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 通過訪問其`BLOB`對象的`MTOM`屬性來提取表示PDF文檔的二進位資料。 這會傳回可寫出為PDF檔案的位元組陣列。

**另請參閱**

[以程式設計方式解譯PDF檔案](#programmatically-disassembling-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
