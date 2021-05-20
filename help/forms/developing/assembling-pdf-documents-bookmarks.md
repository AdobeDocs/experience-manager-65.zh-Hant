---
title: 使用書籤組合PDF檔案
seo-title: 使用書籤組合PDF檔案
description: 使用組合器服務修改包含書籤的PDF文檔，以包括使用Java API和Web服務API的書籤。
seo-description: 使用組合器服務修改包含書籤的PDF文檔，以包括使用Java API和Web服務API的書籤。
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2588'
ht-degree: 0%

---

# 使用書籤{#assembling-pdf-documents-with-bookmarks}組裝PDF文檔

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以組合包含書籤的PDF檔案。 例如，假設您的PDF檔案不含書籤，且您想借由提供書籤來修改該檔案。 使用組合器服務，可以傳遞不包含書籤的PDF文檔，並返回包含書籤的PDF文檔。

書籤包含下列屬性：

* 螢幕上顯示為文字的標題。
* 一種動作，可指定使用者點按書籤時會發生什麼。 書籤的典型操作是移動到當前文檔中的其他位置或開啟另一個PDF文檔，儘管可以指定其他操作。

在本討論中，假定使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

在此DDX文檔中，請注意源屬性被分配了值`Loan.pdf`。 此DDX文檔指定將單個PDF文檔傳遞到組合器服務。 使用書籤組裝PDF文檔時，必須指定描述結果文檔中書籤的書籤XML文檔。 要指定書籤XML文檔，請確保在DDX文檔中指定`Bookmarks`元素。

在此示例DDX文檔中，`Bookmarks`元素將`doc2`指定為值。 此值指示傳遞到組合器服務的輸入映射包含名為`doc2`的鍵。 `doc2`鍵的值是代表書籤XML文檔的`com.adobe.idp.Document`值。 （請參閱[組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)中的「書籤語言」。）

本主題使用以下XML書籤語言來組合包含書籤的PDF文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

在此書籤XML文檔中，請注意「操作」元素，該元素定義用戶按一下書籤時執行的操作。 在「動作」元素底下是Launch元素，可啟動應用程式（例如NotePad）並開啟檔案（例如PDF檔案）。 要開啟PDF檔案，必須使用指定要開啟的檔案的「檔案」元素。 例如，在此部分指定的書籤XML檔案中，開啟的檔案名稱為LoanDetails.pdf。

>[!NOTE]
>
>有關支援操作的完整詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)中的「`Action`元素」。

給定本節中指定的DDX文檔，並將XML檔案作為輸入加入書籤，組合器服務將組合包含以下書籤的PDF文檔。

![aw_aw_bmark](assets/aw_aw_bmark.png)

當用戶按一下&#x200B;*開啟貸款詳細資訊*&#x200B;書籤時，將開啟LoanDetails.pdf。 同樣地，當使用者點按&#x200B;*啟動NotePad*&#x200B;書籤時，NotePad即會啟動。

>[!NOTE]
>
>閱讀本節之前，建議您先熟悉使用組合器服務組合PDF文檔。 本節不討論概念，例如建立包含輸入文檔的集合對象，或了解如何從返回的集合對象中提取結果。 （請參閱[以程式設計方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)。）

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}的摘要

要組合包含書籤的PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考要新增書籤的PDF檔案。
1. 參考書籤XML文檔。
1. 將PDF文檔和書籤XML文檔添加到映射集合。
1. 設定運行時選項。
1. 組合PDF文檔。
1. 儲存包含書籤的PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為AEM Forms所部署之J2EE應用程式伺服器專屬的JAR檔案。 有關所有AEM Forms JAR檔案的位置資訊，請參閱[包含AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

必須參考DDX文檔才能組合PDF文檔。 此DDX文檔必須包含`Bookmarks`元素，該元素指示組合器服務組合包含書籤的PDF。 （如需範例，請參閱本節前面所示的DDX檔案。）

**參考要新增書籤的PDF檔案**

參考要新增書籤的PDF檔案。 參考的PDF檔案是否已包含書籤並不重要。 如果`Bookmarks`元素是PDF來源元素的子項，則書籤會取代PDF來源中已存在的元素。 不過，如果您想保留現有書籤，請確定`Bookmarks`是PDF來源元素的同層級。 例如，請考量下列範例：

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**參考書籤XML文檔**

要組合包含新書籤的PDF，必須引用書籤XML文檔。 書籤XML文檔將傳遞到映射集合對象內的組合器服務。 （如需範例，請參閱本節前面所示的書籤XML檔案。）

>[!NOTE]
>
>請參閱[組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)中的「書籤語言」。

**將PDF文檔和書籤XML文檔添加到映射集合**

您必須將要新增書籤的PDF檔案和書籤XML檔案新增至地圖集合。 因此，地圖集合物件包含兩個元素：PDF文檔和書籤XML文檔。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。 如需可設定的執行階段選項相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

**組合PDF檔案**

要組合包含新書籤的PDF文檔，請使用組合器服務的`invokeDDX`操作。 必須使用`invokeDDX`操作而不是其他組合器服務操作（如`invokeOneDocument`）的原因是組合器服務需要在映射集合對象內傳遞的書籤XML文檔。 此對象是`invokeDDX`操作的參數。

**儲存包含書籤的PDF檔案**

您必須從傳回的地圖物件中擷取結果，並儲存對應的PDF檔案。 （請參閱[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)中的「提取結果」。）

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-pdf-documents-with-bookmarks-using-the-java-api}使用書籤組合PDF檔案

使用組合器服務API(Java)使用書籤組合PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 參考現有的DDX文檔。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 參考要新增書籤的PDF檔案。

   * 使用其建構子並傳遞PDF檔案的位置，建立`java.io.FileInputStream`物件。
   * 使用其建構子建立`com.adobe.idp.Document`物件，並傳遞包含PDF檔案的`java.io.FileInputStream`物件。

1. 參考書籤XML文檔。

   * 使用其建構子並傳遞表示書籤XML文檔的XML檔案的位置，建立`java.io.FileInputStream`對象。
   * 建立`com.adobe.idp.Document`物件並傳遞包含PDF檔案的`java.io.FileInputStream`物件。

1. 將PDF文檔和書籤XML文檔添加到映射集合。

   * 建立`java.util.Map`對象，該對象用於儲存輸入的PDF文檔和書籤的XML文檔。
   * 叫用`java.util.Map`物件的`put`方法並傳遞下列引數，以新增輸入PDF檔案：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
      * 包含輸入PDF文檔的`com.adobe.idp.Document`對象。
   * 調用`java.util.Map`對象的`put`方法並傳遞以下參數，添加書籤XML文檔：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的書籤源元素的值匹配。
      * 包含書籤XML文檔的`com.adobe.idp.Document`對象。


1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法來設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用`AssemblerOptionSpec`對象的`setFailOnError`方法並傳遞`false`。

1. 組合PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下必需值：

   * 表示要使用的DDX文檔的`com.adobe.idp.Document`對象
   * `java.util.Map`對象，包含輸入PDF文檔和書籤XML文檔。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，指定運行時選項，包括預設字型和作業日誌級別

   `invokeDDX`方法返回一個`com.adobe.livecycle.assembler.client.AssemblerResult`對象，該對象包含作業的結果和發生的任何異常。

1. 儲存包含書籤的PDF檔案。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 調用`AssemblerResult`對象的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 對`java.util.Map`對象進行迭代，直到找到結果`com.adobe.idp.Document`對象。 （您可以使用DDX文檔中指定的PDF結果元素來獲取文檔。）
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取PDF文檔。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF檔案與書籤組合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}使用書籤組合PDF文檔

使用組合器服務API（Web服務）將PDF文檔與書籤組合：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

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
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示DDX文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 參考要新增書籤的PDF檔案。

   * 使用其建構子建立`BLOB`物件。 `BLOB`物件用於儲存輸入PDF。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 參考書籤XML文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存書籤XML文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 將PDF文檔和書籤XML文檔添加到映射集合。

   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此收集對象用於儲存輸入的PDF文檔和書籤的XML文檔。
   * 對於每個輸入的PDF文檔和書籤的XML文檔，建立`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配表示鍵名的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
   * 將儲存PDF文檔的`BLOB`對象指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （對每個輸入的PDF文檔和書籤的XML文檔執行此任務。）

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 為屬於`AssemblerOptionSpec`對象的資料成員分配值，以設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象
   * 包含輸入文檔的`MyMapOf_xsd_string_To_xsd_anyType`陣列
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果以及可能發生的任何異常。

1. 儲存包含書籤的PDF檔案。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問`AssemblerResult`對象的`documents`欄位，該欄位是包含結果PDF文檔的`Map`對象。
   * 逐一查看`Map`對象，直到找到與結果文檔的名稱匹配的鍵。 然後將該陣列成員的`value`轉換為`BLOB`。
   * 通過訪問其`BLOB`對象的`MTOM`欄位，提取表示PDF文檔的二進位資料。 這會傳回可寫出為PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
