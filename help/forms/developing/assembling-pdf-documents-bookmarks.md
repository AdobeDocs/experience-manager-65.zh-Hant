---
title: 使用書籤組合PDF檔案
seo-title: 使用書籤組合PDF檔案
description: 使用Assembler服務可修改包含書籤的PDF檔案，使用Java API和Web Service API加入書籤。
seo-description: 使用Assembler服務可修改包含書籤的PDF檔案，使用Java API和Web Service API加入書籤。
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '2588'
ht-degree: 0%

---


# 使用書籤{#assembling-pdf-documents-with-bookmarks}組合PDF檔案

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以組合包含書籤的PDF檔案。 例如，假設您的PDF檔案不包含書籤，而您想要透過提供書籤來修改它。 使用Assembler服務，您可以傳遞不含書籤的PDF檔案，並傳回包含書籤的PDF檔案。

書籤包含下列屬性：

* 在畫面上顯示為文字的標題。
* 一種動作，指定當使用者點按書籤時會發生什麼。 書籤的典型動作是移至目前檔案中的其他位置，或開啟其他PDF檔案，但可指定其他動作。

在本討論中，假設使用了以下DDX文檔。

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

在此DDX文檔中，請注意源屬性被分配了值`Loan.pdf`。 此DDX文檔指定將單個PDF文檔傳遞到Assembler服務。 當將PDF檔案與書籤組合時，您必須指定書籤XML檔案，以說明結果檔案中的書籤。 若要指定書籤XML檔案，請確定`Bookmarks`元素已在DDX檔案中指定。

在此示例中，`Bookmarks`元素指定`doc2`作為值。 此值表示傳遞給Assembler服務的輸入映射包含名為`doc2`的鍵。 `doc2`鍵的值是`com.adobe.idp.Document`值，代表書籤XML檔案。 （請參閱[Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)中的「書籤語言」。）

本主題使用下列XML書籤語言來組合包含書籤的PDF檔案。

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

在此書籤XML檔案中，請注意「動作」元素，該元素定義當使用者按一下書籤時執行的動作。 在「動作」元素下方是「啟動」元素，可啟動應用程式（例如NotePad）並開啟檔案（例如PDF檔案）。 要開啟PDF檔案，必須使用指定要開啟的檔案的「檔案」元素。 例如，在本節中指定的書籤XML檔案中，開啟的檔案名稱為LoanDetails.pdf。

>[!NOTE]
>
>有關支援操作的完整詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)中的「 `Action`元素」。

給定本節中指定的DDX文檔，並將XML檔案作為書籤輸入，Assembler服務會匯編包含以下書籤的PDF文檔。

![aw_aw_bmark](assets/aw_aw_bmark.png)

當使用者按一下「開啟貸款詳細資訊&#x200B;*」書籤時，LoanDetails.pdf便會開啟。*&#x200B;同樣地，當使用者按一下&#x200B;*啟動NotePad*&#x200B;書籤時，NotePad就會啟動。

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用Assembler服務來組合PDF檔案。 本節不討論概念，例如建立包含輸入檔案的系列物件，或學習如何從傳回的系列物件擷取結果。 （請參閱[程式設計匯整PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)。）

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}摘要

若要組合包含書籤的PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考新增書籤的PDF檔案。
1. 參考書籤XML檔案。
1. 將PDF檔案和書籤XML檔案新增至Map系列。
1. 設定執行時期選項。
1. 組合PDF檔案。
1. 儲存包含書籤的PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如果AEM Forms部署在JBoss以外的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為JAR檔案，而AEM Forms部署在該J2EE應用程式伺服器上。 如需所有AEM Forms JAR檔案位置的詳細資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合PDF檔案。 此DDX檔案必須包含`Bookmarks`元素，以指示Assembler服務組合包含書籤的PDF。 （如需範例，請參閱本節稍早說明的DDX檔案）。

**參考新增書籤的PDF檔案**

參考新增書籤的PDF檔案。 參考的PDF檔案是否已包含書籤並不重要。 如果`Bookmarks`元素是PDF來源元素的子系，則書籤會取代PDF來源中已存在的元素。 不過，如果您想要保留現有書籤，請確定`Bookmarks`是PDF來源元素的同級。 例如，請考慮以下範例：

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**參考書籤XML檔案**

若要組合包含新書籤的PDF，您必須參考書籤XML檔案。 書籤XML文檔會傳遞到Map收集對象內的Assembler服務。 （如需範例，請參閱本節稍早說明的書籤XML檔案。）

>[!NOTE]
>
>請參閱[Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)中的「書籤語言」。

**將PDF檔案和書籤XML檔案新增至Map系列**

您必須同時新增書籤的PDF檔案和書籤XML檔案至Map集合。 因此，Map收集物件包含兩個元素：PDF檔案與書籤XML檔案。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。 如需您可設定之執行時期選項的詳細資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

**組合PDF檔案**

若要組合包含新書籤的PDF檔案，請使用Assembler服務的`invokeDDX`操作。 您必須使用`invokeDDX`操作而非其他Assembler服務操作（如`invokeOneDocument`）的原因是，Assembler服務需要在Map收集對象中傳遞的書籤XML文檔。 此對象是`invokeDDX`操作的參數。

**儲存包含書籤的PDF檔案**

您必須從傳回的地圖物件擷取結果，並儲存對應的PDF檔案。 （請參閱[Programmaly Assembling PDF Documents](/help/forms/developing/programmatically-assembling-pdf-documents.md)中的「擷取結果」。）

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-pdf-documents-with-bookmarks-using-the-java-api}使用書籤組合PDF檔案

使用Assembler Service API(Java)將PDF檔案與書籤組合：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 參考現有的DDX檔案。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 參考新增書籤的PDF檔案。

   * 使用其建構函式並傳遞PDF檔案的位置，以建立`java.io.FileInputStream`物件。
   * 使用其建構函式建立`com.adobe.idp.Document`物件，並傳遞包含PDF檔案的`java.io.FileInputStream`物件。

1. 參考書籤XML檔案。

   * 使用其建構函式並傳遞代表書籤XML檔案的XML檔案位置，以建立`java.io.FileInputStream`物件。
   * 建立`com.adobe.idp.Document`物件並傳遞包含PDF檔案的`java.io.FileInputStream`物件。

1. 將PDF檔案和書籤XML檔案新增至Map系列。

   * 建立`java.util.Map`物件，用來儲存輸入的PDF檔案和書籤的XML檔案。
   * 叫用`java.util.Map`物件的`put`方法並傳遞下列引數，以新增輸入的PDF檔案：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
      * 包含輸入PDF文檔的`com.adobe.idp.Document`對象。
   * 調用`java.util.Map`物件的`put`方法並傳遞下列引數，以新增書籤XML檔案：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之書籤來源元素的值相符。
      * `com.adobe.idp.Document`物件，其中包含書籤XML檔案。


1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法，設定運行時選項以滿足您的業務要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法並傳遞`false`。

1. 組合PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列必要值：

   * `com.adobe.idp.Document`物件，代表要使用的DDX檔案
   * `java.util.Map`物件，其中包含輸入的PDF檔案和書籤的XML檔案。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件，指定執行時間選項，包括預設字型和工作記錄層級

   `invokeDDX`方法返回一個`com.adobe.livecycle.assembler.client.AssemblerResult`對象，該對象包含作業的結果和發生的任何例外。

1. 儲存包含書籤的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 重複`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件。 （您可以使用DDX檔案中指定的PDF結果元素來取得檔案。）
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF檔案與書籤組合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}使用書籤來組合PDF檔案

使用Assembler Service API(web service)，使用書籤組合PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存DDX檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立對象，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 參考新增書籤的PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存輸入的PDF。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 參考書籤XML檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存書籤XML檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 將PDF檔案和書籤XML檔案新增至Map系列。

   * 建立`MyMapOf_xsd_string_To_xsd_anyType`對象。 此收集物件用來儲存輸入的PDF檔案和書籤的XML檔案。
   * 對於每個輸入的PDF檔案和書籤XML檔案，請建立`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配代表鍵名的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
   * 將儲存PDF文檔的`BLOB`對象指定給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`對象添加到`MyMapOf_xsd_string_To_xsd_anyType`對象。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （請對每個輸入的PDF檔案和書籤XML檔案執行此工作）。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的資料成員分配值，設定運行時選項以滿足您的業務要求。 例如，要指示Assembler服務在出現錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象
   * 包含輸入文檔的`MyMapOf_xsd_string_To_xsd_anyType`陣列
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和可能發生的任何例外。

1. 儲存包含書籤的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是包含結果PDF檔案的`Map`物件。
   * 重複`Map`物件，直到找到與結果檔案名稱相符的索引鍵。 然後將該陣列成員的`value`轉換為`BLOB`。
   * 存取PDF檔案的`BLOB`物件的`MTOM`欄位，擷取代表PDF檔案的二進位資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
