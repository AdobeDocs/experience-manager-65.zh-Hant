---
title: 使用書籤組裝PDF文檔
seo-title: Assembling PDF Documents with Bookmarks
description: 使用匯編器服務修改包含書籤的PDF文檔，以使用Java API和Web服務API包括書籤。
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

# 使用書籤組裝PDF文檔 {#assembling-pdf-documents-with-bookmarks}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

可以裝配包含書籤的PDF文檔。 例如，假定您的PDF文檔不包含書籤，並且您想通過提供書籤來修改它。 使用匯編器服務，可以將不包含書籤的PDF文檔傳遞給它，並返回包含書籤的PDF文檔。

書籤包含以下屬性：

* 在螢幕上顯示為文本的標題。
* 一個操作，它指定當用戶按一下書籤時發生的情況。 書籤的典型操作是移動到當前文檔中的另一個位置或開啟另一個PDF文檔，儘管可以指定其他操作。

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

在此DDX文檔中，請注意已為源屬性分配了值 `Loan.pdf`。 此DDX文檔指定將單個PDF文檔傳遞到匯編器服務。 在將PDF文檔與書籤組合時，必須指定描述結果文檔中書籤的書籤XML文檔。 要指定書籤XML文檔，請確保 `Bookmarks` 元素在DDX文檔中指定。

在此示例DDX文檔中， `Bookmarks` 元素指定 `doc2` 值。 此值表示傳遞給匯編器服務的輸入映射包含名為 `doc2`。 的值 `doc2` 鍵是 `com.adobe.idp.Document` 表示書籤XML文檔的值。 (請參閱 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。)

本主題使用以下XML書籤語言來匯編包含書籤的PDF文檔。

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

在此書籤XML文檔中，請注意定義用戶按一下書籤時執行的操作的「操作」元素。 「操作」元素下是啟動應用程式（如NotePad）並開啟檔案(如PDF檔案)的「啟動」元素。 要開啟PDF檔案，必須使用指定要開啟的檔案的「檔案」元素。 例如，在本節中指定的書籤XML檔案中，開啟的檔案的名稱為LoanDetails.pdf。

>[!NOTE]
>
>有關支援操作的完整詳細資訊，請參閱 `Action` 元素」 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

給定本節中指定的DDX文檔，並將XML檔案書籤作為輸入，匯編器服務將匯編包含以下書籤的PDF文檔。

![aw_aw_bmark](assets/aw_aw_bmark.png)

當用戶按一下 *開啟貸款詳細資訊* 書籤，將開啟LoanDetails.pdf。 同樣，當用戶按一下 *啟動NotePad* 書籤，NotePad已啟動。

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用匯編器服務PDF文檔。 本節不討論概念，如建立包含輸入文檔的集合對象或學習如何從返回的集合對象中提取結果。 (請參閱 [以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)。)

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要匯編包含書籤的PDF文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立PDF匯編器客戶端。
1. 引用現有DDX文檔。
1. 引用添加書籤的PDF文檔。
1. 引用書籤XML文檔。
1. 將PDF文檔和書籤XML文檔添加到映射集合。
1. 設定運行時選項。
1. 匯編PDF文檔。
1. 保存包含書籤的PDF文檔。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援的J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於AEM Forms部署在其上的J2EE應用程式伺服器的JAR檔案。 有關所有AEM FormsJAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF匯編器客戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**引用現有DDX文檔**

必須引用DDX文檔來匯編PDF文檔。 此DDX文檔必須包含 `Bookmarks` 元素，指示匯編器服務匯編包含書籤的PDF。 （有關示例，請參閱本節前面顯示的DDX文檔。）

**引用添加書籤的PDF文檔**

引用添加書籤的PDF文檔。 引用的PDF文檔是否已包含書籤並不重要。 如果 `Bookmarks` 元素是PDF源元素的子元素，則書籤將替換PDF源中已存在的元素。 但是，如果要保留現有書籤，請確保 `Bookmarks` 是PDF源元素的同級。 例如，請考慮以下示例：

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**引用書籤XML文檔**

要裝配包含新書籤的PDF，必須引用書籤XML文檔。 書籤XML文檔將傳遞給映射集合對象內的匯編器服務。 （例如，請參閱本節前面顯示的書籤XML文檔。）

>[!NOTE]
>
>請參閱中的「書籤語言」 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

**將PDF文檔和書籤XML文檔添加到映射集合**

必須將書籤添加到的PDF文檔和書籤XML文檔都添加到映射集合中。 因此，Map集合對象包含兩個元素：PDF文檔和書籤XML文檔。

**設定運行時選項**

您可以設定運行時選項，這些選項在匯編程式服務執行作業時控制其行為。 例如，您可以設定一個選項，指示匯編程式服務在遇到錯誤時繼續處理作業。 有關可設定的運行時選項的資訊，請參見 `AssemblerOptionSpec` 類引用 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**匯編PDF文檔**

要匯編包含新書籤的PDF文檔，請使用匯編器服務的 `invokeDDX` 的下界。 您必須使用 `invokeDDX` 與其他匯編程式服務操作(如 `invokeOneDocument` 是因為匯編器服務需要在映射集合對象內傳遞的書籤XML文檔。 此對象是 `invokeDDX` 的下界。

**保存包含書籤的PDF文檔**

必須從返回的映射對象中提取結果並保存相應的PDF文檔。 (請參閱中的「提取結果」 [以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API將PDF文檔與書籤組合起來 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

使用匯編器服務API(Java)使用書籤匯編PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用現有DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定DDX檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 引用添加書籤的PDF文檔。

   * 建立 `java.io.FileInputStream` 使用其建構子並傳遞PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子傳遞對象 `java.io.FileInputStream` 包含PDF文檔的對象。

1. 引用書籤XML文檔。

   * 建立 `java.io.FileInputStream` 使用其建構子並傳遞表示書籤XML文檔的XML檔案的位置。
   * 建立 `com.adobe.idp.Document` 並傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。

1. 將PDF文檔和書籤XML文檔添加到映射集合。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔和書籤XML文檔的對象。
   * 通過調用輸入PDF文檔 `java.util.Map` 對象 `put` 方法並傳遞以下參數：

      * 表示鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
      * A `com.adobe.idp.Document` 包含輸入PDF文檔的對象。
   * 通過調用 `java.util.Map` 對象 `put` 方法並傳遞以下參數：

      * 表示鍵名稱的字串值。 此值必須與DDX文檔中指定的書籤源元素的值匹配。
      * A `com.adobe.idp.Document` 包含書籤XML文檔的對象。


1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過調用屬於的方法來設定運行時選項以滿足業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 對象 `setFailOnError` 方法 `false`。

1. 匯編PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下所需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含輸入PDF文檔和書籤XML文檔的對象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象，包括預設字型和作業日誌級別

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含作業結果和所發生的任何異常的對象。

1. 保存包含書籤的PDF文檔。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 調用 `AssemblerResult` 對象 `getDocuments` 的雙曲餘切值。 這返回 `java.util.Map` 的雙曲餘切值。
   * 迭代 `java.util.Map` 直到找到結果 `com.adobe.idp.Document` 的雙曲餘切值。 (可以使用DDX文檔中指定的PDF結果元素獲取文檔。)
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取PDF文檔。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API將PDF文檔與書籤組合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API將PDF文檔與書籤組合起來 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

使用匯編器服務API（Web服務）將帶有書籤的PDF文檔匯編：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立PDF匯編器客戶端。

   * 建立 `AssemblerServiceClient` 對象。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `AssemblerServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用現有DDX文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存DDX文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 引用添加書籤的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存輸入PDF。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 引用書籤XML文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存書籤XML文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 將PDF文檔和書籤XML文檔添加到映射集合。

   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 此集合對象用於儲存輸入PDF文檔和書籤XML文檔。
   * 對於每個輸入PDF文檔和書籤XML文檔，建立一個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。
   * 為指定表示鍵名的字串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `key` 的子菜單。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
   * 分配 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `value` 的子菜單。
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 調用 `MyMapOf_xsd_string_To_xsd_anyType` 對象 `Add` 方法和通過 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 (對每個輸入PDF文檔和書籤XML文檔執行此任務。)

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過將值分配給屬於的資料成員來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編程式服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 對象 `failOnError` 資料成員。

1. 匯編PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含輸入文檔的陣列
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作業結果的對象以及可能發生的任何異常。

1. 保存包含書籤的PDF文檔。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問 `AssemblerResult` 對象 `documents` 欄位， `Map` 包含結果PDF文檔的對象。
   * 迭代 `Map` 對象，直到找到與結果文檔的名稱匹配的鍵。 然後轉換該陣列成員 `value` 到 `BLOB`。
   * 通過訪問PDF文檔來提取表示該文檔的二進位資料 `BLOB` 對象 `MTOM` 的子菜單。 這將返回可以寫入PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
