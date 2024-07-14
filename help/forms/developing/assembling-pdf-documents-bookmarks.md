---
title: 組合含書籤的PDF檔案
description: 使用Java API和Web服務API，使用組合器服務來修改包含書籤的PDF檔案，以包含書籤。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 0%

---

# 組合含書籤的PDF檔案 {#assembling-pdf-documents-with-bookmarks}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以組合包含書籤的PDF檔案。 例如，假設您有一份不含書籤的PDF檔案，而且您想提供書籤來修改它。 使用Assembler服務，您可以傳遞不包含書籤的PDF檔案，並取回包含書籤的PDF檔案。

書籤包含以下屬性：

* 在熒幕上顯示為文字的標題。
* 此動作會指定使用者按一下書籤時所執行的動作。 書籤的典型動作是移動到目前檔案中的另一個位置，或開啟另一個PDF檔案，不過也可以指定其他動作。

為了進行此討論，假設使用下列DDX檔案。

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

在此DDX檔案中，請注意來源屬性已指派值`Loan.pdf`。 此DDX檔案指定將單一PDF檔案傳遞至組合器服務。 當組合含有書籤的PDF檔案時，您必須指定書籤XML檔案，以說明結果檔案中的書籤。 若要指定書籤XML檔案，請確定已在DDX檔案中指定`Bookmarks`專案。

在此範例DDX檔案中，`Bookmarks`專案指定`doc2`為值。 此值表示傳遞至組合器服務的輸入對應包含名為`doc2`的索引鍵。 `doc2`索引鍵的值是代表書籤XML檔案的`com.adobe.idp.Document`值。 （請參閱[組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)中的「書籤語言」。）

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

在此書籤XML檔案中，請注意定義使用者按一下書籤時所執行動作的「動作」元素。 在「動作」元素底下是Launch元素，可啟動應用程式（例如NotePad）並開啟檔案(例如PDF檔案)。 若要開啟PDF檔案，您必須使用指定要開啟的檔案的「檔案」元素。 例如，在本節指定的書籤XML檔案中，開啟的檔案名稱為LoanDetails.pdf。

>[!NOTE]
>
>如需支援動作的完整詳細資料，請參閱[組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)中的`Action`專案。

指定此區段中所指定的DDX檔案並將XML檔案加入書籤作為輸入，Assembler服務會組合包含下列書籤的PDF檔案。

![aw_aw_bmark](assets/aw_aw_bmark.png)

當使用者按一下&#x200B;*開啟貸款詳細資料*&#x200B;書籤時，就會開啟LoanDetails.pdf。 同樣地，當使用者按一下&#x200B;*啟動NotePad*&#x200B;書籤時，NotePad就會啟動。

>[!NOTE]
>
>閱讀本節之前，建議您先熟悉使用Assembler服務組合PDF檔案。 本節不討論概念，例如建立包含輸入檔案的集合物件，或學習如何從傳回的集合物件中擷取結果。 (請參閱[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)。)

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱[組合器服務與DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

若要組合包含書籤的PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參照新增書籤的PDF檔案。
1. 參考書籤XML檔案。
1. 將PDF檔案和書籤XML檔案新增至地圖集合。
1. 設定執行階段選項。
1. 組合PDF檔案。
1. 儲存包含書籤的PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在J2EE應用程式伺服器的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF組合器使用者端**

您必須先建立組合器服務使用者端，才能以程式設計方式執行組合器作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDF檔案。 此DDX檔案必須包含`Bookmarks`元素，這會指示組合器服務組合包含書籤的PDF。 （如需範例，請參閱本節前面顯示的DDX檔案）。

**參考加入書籤的PDF檔案**

參照新增書籤的PDF檔案。 參考的PDF檔案是否已包含書籤並不重要。 如果`Bookmarks`元素是PDF來源元素的子項，則書籤將會取代PDF來源中已存在的專案。 不過，如果要保留現有的書籤，請確定`Bookmarks`是PDF來源元素的同層級。 例如，請考量下列範例：

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**參考書籤XML檔案**

若要組合包含新書籤的PDF，您必須參考書籤XML檔案。 書籤XML檔案會傳遞到Map集合物件中的Assembler服務。 （如需範例，請參閱本區段前面顯示的書籤XML檔案。）

>[!NOTE]
>
>請參閱[組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)中的「書籤語言」。

**將PDF檔案和書籤XML檔案新增至地圖集合**

將新增書籤的PDF檔案與書籤XML檔案新增至地圖集合。 因此，Map集合物件包含兩個元素：PDF檔案與書籤XML檔案。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。 如需您可以設定的執行階段選項相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

**組合PDF檔案**

若要組合包含新書籤的PDF檔案，請使用Assembler服務的`invokeDDX`作業。 您必須使用`invokeDDX`作業而非其他Assembler服務作業（例如`invokeOneDocument`）的原因，是因為Assembler服務需要在Map集合物件中傳遞的書籤XML檔案。 此物件是`invokeDDX`作業的引數。

**儲存包含書籤的PDF檔案**

從傳回的地圖物件中擷取結果，並儲存對應的PDF檔案。 (請參閱[以程式設計方式組裝PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)中的「擷取結果」。)

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API彙編PDF檔案及書籤 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

使用組合器服務API (Java)組合帶有書籤的PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。 （請參閱[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`AssemblerServiceClient`物件。

1. 參考現有的DDX檔案。

   * 使用它的建構函式並傳遞指定DDX檔案位置的字串值，建立代表DDX檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 參照新增書籤的PDF檔案。

   * 使用物件的建構函式並傳遞PDF檔案的位置來建立`java.io.FileInputStream`物件。
   * 使用它的建構函式建立`com.adobe.idp.Document`物件，並傳遞包含PDF檔案的`java.io.FileInputStream`物件。

1. 參考書籤XML檔案。

   * 使用物件的建構函式，並傳遞代表書籤XML檔案的XML檔案位置，以建立`java.io.FileInputStream`物件。
   * 建立`com.adobe.idp.Document`物件並傳遞包含PDF檔案的`java.io.FileInputStream`物件。

1. 將PDF檔案和書籤XML檔案新增至地圖集合。

   * 建立用來儲存輸入PDF檔案和書籤XML檔案的`java.util.Map`物件。
   * 呼叫`java.util.Map`物件的`put`方法並傳遞下列引數，以新增輸入PDF檔案：

      * 代表索引鍵名稱的字串值。 此值必須符合DDX檔案中指定的PDF來源元素的值。
      * 包含輸入PDF檔案的`com.adobe.idp.Document`物件。

   * 呼叫`java.util.Map`物件的`put`方法並傳遞下列引數，以新增書籤XML檔案：

      * 代表索引鍵名稱的字串值。 此值必須符合DDX檔案中指定的書籤來源元素值。
      * 包含書籤XML檔案的`com.adobe.idp.Document`物件。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 透過叫用屬於`AssemblerOptionSpec`物件的方法，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法，然後傳遞`false`。

1. 組合PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列必要值：

   * 代表要使用的DDX檔案的`com.adobe.idp.Document`物件
   * 同時包含輸入PDF檔案與書籤XML檔案的`java.util.Map`物件。
   * 指定執行階段選項（包括預設字型和作業記錄層級）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件

   `invokeDDX`方法傳回`com.adobe.livecycle.assembler.client.AssemblerResult`物件，其中包含工作的結果和發生的任何例外狀況。

1. 儲存包含書籤的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 逐一檢視`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件為止。 (您可以使用DDX檔案中指定的PDF結果元素來取得檔案。)
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

**另請參閱**

[快速入門(SOAP模式)：使用Java API以書籤組合PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API彙編PDF檔案及書籤 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

使用Assembler Service API （Web服務）來組合包含書籤的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

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
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 參照新增書籤的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存輸入PDF。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 參考書籤XML檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存書籤XML檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 將PDF檔案和書籤XML檔案新增至地圖集合。

   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此集合物件是用來儲存輸入PDF檔案與書籤XML檔案。
   * 針對每個輸入PDF檔案和書籤XML檔案，建立`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 將代表索引鍵名稱的字串值指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`key`欄位。 此值必須符合DDX檔案中指定的PDF來源元素的值。
   * 將儲存PDF檔案的`BLOB`物件指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`欄位。
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 叫用`MyMapOf_xsd_string_To_xsd_anyType`物件的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`物件。 (針對每個輸入PDF檔案與書籤XML檔案執行此工作。)

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 將值指派給屬於`AssemblerOptionSpec`物件的資料成員，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請將`false`指派給`AssemblerOptionSpec`物件的`failOnError`資料成員。

1. 組合PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列值：

   * 代表DDX檔案的`BLOB`物件
   * 包含輸入檔案的`MyMapOf_xsd_string_To_xsd_anyType`陣列
   * 指定執行階段選項的`AssemblerOptionSpec`物件

   `invokeDDX`方法傳回`AssemblerResult`物件，其中包含工作結果以及可能發生的任何例外狀況。

1. 儲存包含書籤的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，這是包含結果PDF檔案的`Map`物件。
   * 反複檢查`Map`物件，直到找到符合結果檔名稱的金鑰。 然後將該陣列成員的`value`轉換為`BLOB`。
   * 存取其`BLOB`物件的`MTOM`欄位，擷取代表PDF檔案的二進位資料。 這會傳回您可以寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
