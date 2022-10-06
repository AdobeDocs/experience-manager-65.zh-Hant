---
title: 使用書籤組合PDF文檔
seo-title: Assembling PDF Documents with Bookmarks
description: 使用組合器服務修改包含書籤的PDF文檔，以包括使用Java API和Web服務API的書籤。
seo-description: Use the Assembler service to modify a PDF document that does contain bookmarks to include bookmarks using the Java API and the Web Service API.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 0%

---

# 使用書籤組合PDF文檔 {#assembling-pdf-documents-with-bookmarks}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以組合包含書籤的PDF文檔。 例如，假設您的PDF檔案不包含書籤，且您想借由提供書籤來修改該檔案。 使用組合器服務，可以將不包含書籤的PDF文檔傳遞給它，並返回包含書籤的PDF文檔。

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

在此DDX文檔中，請注意源屬性被分配了值 `Loan.pdf`. 此DDX文檔指定將單個PDF文檔傳遞到組合器服務。 使用書籤組裝PDF文檔時，必須指定描述結果文檔中書籤的書籤XML文檔。 要指定書籤XML文檔，請確保 `Bookmarks` 元素。

在此示例DDX文檔中， `Bookmarks` 元素指定 `doc2` 作為值。 此值表示傳遞到組合器服務的輸入映射包含名為的鍵 `doc2`. 的值 `doc2` key是 `com.adobe.idp.Document` 表示書籤XML文檔的值。 (請參閱以下主題中的「書籤語言」： [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).)

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

在此書籤XML文檔中，請注意「操作」元素，該元素定義用戶按一下書籤時執行的操作。 在「動作」元素下方是Launch元素，可啟動應用程式（例如NotePad）並開啟檔案(例如PDF檔案)。 要開啟PDF檔案，必須使用指定要開啟的檔案的「檔案」元素。 例如，在此部分指定的書籤XML檔案中，開啟的檔案名稱為LoanDetails.pdf。

>[!NOTE]
>
>如需支援動作的完整詳細資訊，請參閱「 `Action` 元素」 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

給定本節中指定的DDX文檔，並將XML檔案作為輸入加入書籤，組合器服務將組合包含以下書籤的PDF文檔。

![aw_aw_bmark](assets/aw_aw_bmark.png)

當使用者點按 *開啟貸款詳細資訊* 書籤中， LoanDetails.pdf即會開啟。 同樣地，當使用者點按 *啟動NotePad* 書籤，則啟動NotePad。

>[!NOTE]
>
>閱讀本節之前，建議您熟悉使用組合器服務來組合PDF文檔。 本節不討論概念，例如建立包含輸入文檔的集合對象，或了解如何從返回的集合對象中提取結果。 (請參閱 [以寫程式方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

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

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為AEM Forms所部署之J2EE應用程式伺服器專屬的JAR檔案。 如需所有AEM Forms JAR檔案位置的相關資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

必須引用DDX文檔來組合PDF文檔。 此DDX文檔必須包含 `Bookmarks` 元素，指示組合器服務組合包含書籤的PDF。 （如需範例，請參閱本節前面所示的DDX檔案。）

**參考要新增書籤的PDF檔案**

參考要新增書籤的PDF檔案。 引用的PDF文檔是否已包含書籤並不重要。 若 `Bookmarks` 元素是PDF來源元素的子項，則書籤會取代PDF來源中已存在的元素。 不過，如果您想要保留現有書籤，請確定 `Bookmarks` 是PDF源元素的同級。 例如，請考量下列範例：

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
>請參閱以下主題中的「書籤語言」： [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

**將PDF文檔和書籤XML文檔添加到映射集合**

必須將添加書籤的PDF文檔和書籤XML文檔添加到映射集合。 因此，地圖集合物件包含兩個元素：PDF文檔和書籤XML文檔。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。 如需可設定的執行階段選項相關資訊，請參閱 `AssemblerOptionSpec` 類引用 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**組合PDF文檔**

要組合包含新書籤的PDF文檔，請使用組合器服務的 `invokeDDX` 操作。 您必須使用 `invokeDDX` 操作，而不是其它組合器服務操作，例如 `invokeOneDocument` 是因為組合器服務需要在映射集合對象內傳遞的書籤XML文檔。 此物件是 `invokeDDX` 操作。

**保存包含書籤的PDF文檔**

必須從返回的映射對象中提取結果並保存相應的PDF文檔。 (請參閱以下主題中的「提取結果」： [以寫程式方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API使用書籤組合PDF檔案 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

使用組合器服務API(Java)使用書籤組合PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 建立 `AssemblerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞指定DDX檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 參考要新增書籤的PDF檔案。

   * 建立 `java.io.FileInputStream` 對象，方法是使用其建構子並傳遞PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用其建構子並傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。

1. 參考書籤XML文檔。

   * 建立 `java.io.FileInputStream` 對象，方法是使用其建構子並傳遞表示書籤XML文檔的XML檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，並傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。

1. 將PDF文檔和書籤XML文檔添加到映射集合。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔和書籤XML文檔的對象。
   * 通過調用 `java.util.Map` 物件 `put` 方法，並傳遞下列引數：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
      * A `com.adobe.idp.Document` 包含輸入PDF文檔的對象。
   * 叫用 `java.util.Map` 物件 `put` 方法，並傳遞下列引數：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的書籤源元素的值匹配。
      * A `com.adobe.idp.Document` 包含書籤XML文檔的對象。


1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 通過調用屬於的方法來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 物件 `setFailOnError` 方法和傳遞 `false`.

1. 組合PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列必要值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含輸入PDF文檔和書籤XML文檔的對象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項（包括預設字型和作業日誌級別）的對象

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含作業結果的對象以及發生的任何例外。

1. 儲存包含書籤的PDF檔案。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 叫用 `AssemblerResult` 物件 `getDocuments` 方法。 這會傳回 `java.util.Map` 物件。
   * 重複 `java.util.Map` 對象，直到找到結果 `com.adobe.idp.Document` 物件。 (您可以使用DDX文檔中指定的PDF結果元素來獲取文檔。)
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取PDF檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF檔案與書籤組裝](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API使用書籤組合PDF文檔 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

使用組合器服務API（Web服務）將PDF文檔與書籤組合：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立PDF組合器客戶端。

   * 建立 `AssemblerServiceClient` 物件，使用其預設建構函式。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時，會使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `AssemblerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參考現有的DDX文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存DDX文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 參考要新增書籤的PDF檔案。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 物件可用來儲存輸入PDF。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 參考書籤XML文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存書籤XML文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 將PDF文檔和書籤XML文檔添加到映射集合。

   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此收集對象用於儲存輸入PDF文檔和書籤XML文檔。
   * 對於每個輸入PDF文檔和書籤XML文檔，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `key` 欄位。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
   * 指派 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `value` 欄位。
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` 物件 `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 (對每個輸入PDF文檔和書籤XML文檔執行此任務。)

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 為屬於的資料成員指定值，以設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 物件 `failOnError` 資料成員。

1. 組合PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列值：

   * A `BLOB` 表示DDX文檔的對象
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含輸入文檔的陣列
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含作業結果的對象以及可能發生的任何例外。

1. 儲存包含書籤的PDF檔案。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 存取 `AssemblerResult` 物件 `documents` 欄位，即 `Map` 包含結果PDF文檔的對象。
   * 重複 `Map` 對象，直到找到與生成文檔的名稱匹配的鍵。 然後將該陣列成員的 `value` 到 `BLOB`.
   * 通過訪問PDF文檔來提取代表文檔的二進位資料 `BLOB` 物件 `MTOM` 欄位。 這會傳回一個位元組陣列，您可將其寫出至PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
