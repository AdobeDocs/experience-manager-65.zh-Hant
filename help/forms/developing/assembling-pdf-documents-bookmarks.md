---
title: 使用書籤組合PDF檔案
seo-title: 使用書籤組合PDF檔案
description: 'null'
seo-description: 'null'
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用書籤組合PDF檔案 {#assembling-pdf-documents-with-bookmarks}

您可以組合包含書籤的PDF檔案。 例如，假設您的PDF檔案不包含書籤，而您想要透過提供書籤來修改它。 使用Assembler服務，您可以傳遞不含書籤的PDF檔案，並傳回包含書籤的PDF檔案。

書籤包含下列屬性：

* 在畫面上顯示為文字的標題。
* 一種動作，指定當使用者點按書籤時會發生什麼。 書籤的典型動作是移至目前檔案中的其他位置，或開啟其他PDF檔案，但可指定其他動作。

在本討論中，假設使用了以下DDX文檔。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

在此DDX文檔中，請注意源屬性已分配值 `Loan.pdf`。 此DDX文檔指定將單個PDF文檔傳遞到Assembler服務。 當將PDF檔案與書籤組合時，您必須指定書籤XML檔案，以說明結果檔案中的書籤。 若要指定書籤XML檔案，請確 `Bookmarks` 定元素已在DDX檔案中指定。

在此示例中，DDX文檔中 `Bookmarks` 元素指 `doc2` 定為值。 此值表示傳遞給Assembler服務的輸入映射包含名為的鍵 `doc2`。 索引鍵的值 `doc2` 是代表書 `com.adobe.idp.Document` 簽XML檔案的值。 (請參閱「匯編器服務」和「DDX參考」中 [的「書籤語言」](https://www.adobe.com/go/learn_aemforms_ddx_63)。)

本主題使用下列XML書籤語言來組合包含書籤的PDF檔案。

```as3
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

在此書籤XML檔案中，請注意「動作」元素，該元素定義當使用者按一下書籤時所執行的動作。 在「動作」元素下方是「啟動」元素，可啟動應用程式（例如NotePad）並開啟檔案（例如PDF檔案）。 要開啟PDF檔案，必須使用指定要開啟的檔案的「檔案」元素。 例如，在本節中指定的書籤XML檔案中，開啟的檔案名稱為LoanDetails.pdf。

>[!NOTE]
>
>有關支援的操作的完整詳細資訊，請參 `Action` 閱「匯編器服務」和「 [DDX參考」中的「元素」](https://www.adobe.com/go/learn_aemforms_ddx_63)。

給定本節中指定的DDX文檔，並將XML檔案作為書籤輸入，Assembler服務會匯編包含以下書籤的PDF文檔。

![aw_aw_bmark](assets/aw_aw_bmark.png)

當使用者按一下「開 *啟貸款詳細資訊」書籤* ,LoanDetails.pdf就會開啟。 同樣地，當使用者按一下「啟動 *NotePad」書籤* ,NotePad也會啟動。

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用Assembler服務來組合PDF檔案。 本節不討論概念，例如建立包含輸入檔案的系列物件，或學習如何從傳回的系列物件擷取結果。 (請參 [閱「程式設計方式組裝PDF檔案」](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)。

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參 [閱Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

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

如果AEM Forms部署在JBoss以外的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為JAR檔案，而AEM Forms部署在該J2EE應用程式伺服器上。 如需所有AEM Forms JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合PDF檔案。 此DDX檔案必須包含元 `Bookmarks` 素，元素會指示Assembler服務組合包含書籤的PDF。 （如需範例，請參閱本節稍早說明的DDX檔案）。

**參考新增書籤的PDF檔案**

參考新增書籤的PDF檔案。 參考的PDF檔案是否已包含書籤並不重要。 如果元 `Bookmarks` 素是PDF來源元素的子系，則書籤會取代PDF來源中已存在的子系。 不過，如果您想要保留現有的書籤，請確 `Bookmarks` 定這是PDF來源元素的同級。 例如，請考慮以下範例：

```as3
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**參考書籤XML檔案**

若要組合包含新書籤的PDF，您必須參考書籤XML檔案。 書籤XML文檔會傳遞到Map收集對象內的Assembler服務。 （如需範例，請參閱本節稍早說明的書籤XML檔案。）

>[!NOTE]
>
>請參閱匯編器服務和DDX參考 [中的「書籤語言」](https://www.adobe.com/go/learn_aemforms_ddx_63)。

**將PDF檔案和書籤XML檔案新增至Map系列**

您必須同時新增書籤的PDF檔案和書籤XML檔案至Map集合。 因此，Map收集物件包含兩個元素：PDF檔案與書籤XML檔案。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。 如需您可設定之執行時期選項的詳細資訊，請參閱 `AssemblerOptionSpec`[AEM Forms API參考中的類別參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**組合PDF檔案**

若要組合包含新書籤的PDF檔案，請使用Assembler服務的作 `invokeDDX` 業。 您必須使用該操作而非其他 `invokeDDX` Assembler服務操作(如 `invokeOneDocument` Assembler服務)的原因是，Assembler服務需要在Map收集對象中傳遞書籤XML文檔。 此對象是操作的參 `invokeDDX` 數。

**儲存包含書籤的PDF檔案**

您必須從傳回的地圖物件擷取結果，並儲存對應的PDF檔案。 (請參閱「以程式設計方式組 [合PDF檔案」中的「摘取結果](/help/forms/developing/programmatically-assembling-pdf-documents.md)」)。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API使用書籤組合PDF檔案 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

使用Assembler Service API(Java)將PDF檔案與書籤組合：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。 (請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用其 `AssemblerServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考現有的DDX檔案。

   * 使用 `java.io.FileInputStream` 其建構子並傳遞指定DDX檔案位置的字串值，建立表示DDX文檔的對象。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 參考新增書籤的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞PDF檔案的位置來建立物件。
   * 使用 `com.adobe.idp.Document` 其建構函式建立物件，並傳 `java.io.FileInputStream` 遞包含PDF檔案的物件。

1. 參考書籤XML檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞代表書籤XML檔案的XML檔案位置，以建立物件。
   * 建立物 `com.adobe.idp.Document` 件並傳遞包 `java.io.FileInputStream` 含PDF檔案的物件。

1. 將PDF檔案和書籤XML檔案新增至Map系列。

   * 建立 `java.util.Map` 用來儲存輸入PDF檔案和書籤XML檔案的物件。
   * 叫用物件的方法並傳遞下 `java.util.Map` 列引數，以 `put` 新增輸入的PDF檔案：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
      * 包 `com.adobe.idp.Document` 含輸入PDF檔案的物件。
   * 調用物件的方法並傳遞下列引 `java.util.Map` 數，以新 `put` 增書籤XML檔案：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之書籤來源元素的值相符。
      * 包 `com.adobe.idp.Document` 含書籤XML文檔的對象。


1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 調用屬於該對象的方法，以設定運行時選項以滿足您的業務 `AssemblerOptionSpec` 要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用 `AssemblerOptionSpec` 物件的方 `setFailOnError` 法並傳遞 `false`。

1. 組合PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列必要值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文檔的對象
   * 包 `java.util.Map` 含輸入PDF檔案和書籤XML檔案的物件。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 運行時選項（包括預設字型和作業日誌級別）的對象
   該方 `invokeDDX` 法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 一個對象，該對象包含作業結果和所發生的任何異常。

1. 儲存包含書籤的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的方 `getDocuments` 法。 這會傳回 `java.util.Map` 物件。
   * 重複該對 `java.util.Map` 像，直到找到結果對 `com.adobe.idp.Document` 像。 （您可以使用DDX檔案中指定的PDF結果元素來取得檔案。）
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法以擷取PDF檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF檔案與書籤組合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API，以書籤組合PDF檔案 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

使用Assembler Service API(web service)，使用書籤組合PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立PDF匯寫程式式用戶端。

   * 使用其 `AssemblerServiceClient` 預設建構函式建立物件。
   * 使用建 `AssemblerServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `AssemblerServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存DDX文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示DDX文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 參考新增書籤的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 物 `BLOB` 件用於儲存輸入的PDF。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 參考書籤XML檔案。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存書籤XML文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 將PDF檔案和書籤XML檔案新增至Map系列。

   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 此收集物件用來儲存輸入的PDF檔案和書籤的XML檔案。
   * 對於每個輸入的PDF檔案和書籤XML檔案，請建立物 `MyMapOf_xsd_string_To_xsd_anyType_Item` 件。
   * 為對象欄位指定代表鍵名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字串 `key` 值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
   * 將存 `BLOB` 儲PDF文檔的對象指 `MyMapOf_xsd_string_To_xsd_anyType_Item` 派到對 `value` 像欄位。
   * 將對象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 添加到對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 調用對 `MyMapOf_xsd_string_To_xsd_anyType` 像的方 `Add` 法並傳遞對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 （請對每個輸入的PDF檔案和書籤XML檔案執行此工作）。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 通過為屬於該對象的資料成員分配值，設定運行時選項以滿足您的業務需 `AssemblerOptionSpec` 求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請指 `false` 派給 `AssemblerOptionSpec` 物件的資料 `failOnError` 成員。

1. 組合PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列值：

   * 代 `BLOB` 表DDX文檔的對象
   * 包含 `MyMapOf_xsd_string_To_xsd_anyType` 輸入文檔的陣列
   * 指定 `AssemblerOptionSpec` 運行時選項的對象
   該方 `invokeDDX` 法返回 `AssemblerResult` 一個對象，該對象包含作業的結果和可能發生的任何例外。

1. 儲存包含書籤的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取物 `AssemblerResult` 件的欄 `documents` 位，此欄位是包含 `Map` 結果PDF檔案的物件。
   * 重複該對 `Map` 像，直到找到與生成文檔的名稱匹配的鍵。 然後將該陣列成員轉 `value` 換為 `BLOB`。
   * 存取PDF檔案物件的欄位，擷取代表PDF文 `BLOB` 件的二進位 `MTOM` 資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
