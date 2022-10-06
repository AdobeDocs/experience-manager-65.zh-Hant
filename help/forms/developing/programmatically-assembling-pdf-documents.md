---
title: 以寫程式方式組合PDF文檔
seo-title: Programmatically Assembling PDF Documents
description: 使用組合器服務API，使用Java API和Web服務API將多個PDF文檔組合為單個PDF文檔。
seo-description: Use the Assembler service API to assemble multiple PDF documents into a single PDF document using the Java API and the Web Service API.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 0%

---

# 以寫程式方式組合PDF文檔 {#programmatically-assembling-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以使用組合器服務API將多個PDF文檔組合為單個PDF文檔。 下圖顯示三個PDF文檔合併到單個PDF文檔中。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

要將兩個或多個PDF文檔組合為單個PDF文檔，需要DDX文檔。 DDX文檔描述了組合器服務生成的PDF文檔。 也就是說，DDX文檔指示組合器服務執行哪些操作。

在本討論中，假定使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

此DDX文檔將合併兩個PDF文檔，命名為 *map.pdf* 和 *directions.pdf* 整合到單一PDF檔案中。

>[!NOTE]
>
>要查看分解PDF文檔的DDX文檔，請參閱 [以寫程式方式分解PDF文檔](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 使用Web服務調用組合器服務時的注意事項 {#considerations-when-invoking-assembler-service-using-web-services}

在組裝大型文檔期間添加頁眉和頁腳時，您可能會遇到 `OutOfMemory` 錯誤，且檔案將不會組裝。 若要降低發生此問題的機率，請新增 `DDXProcessorSetting` 元素，如下列範例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

您可以將此元素新增為 `DDX` 元素或作為 `PDF result` 元素。 此設定的預設值為0（零），這會關閉勾選點，而DDX的運作方式就像 `DDXProcessorSetting` 元素不存在。 如果您遇到 `OutOfMemory` 錯誤，您可能需要將值設為整數，通常介於500和5000之間。 小的查核點值會導致查核點更頻繁。

## 步驟摘要 {#summary-of-steps}

要從多個PDF文檔組合單個PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考輸入PDF文檔。
1. 設定運行時選項。
1. 組合輸入PDF文檔。
1. 提取結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器客戶端。

**參考現有的DDX文檔**

必須引用DDX文檔來組合PDF文檔。 例如，請考量本節中引入的DDX檔案。 此DDX文檔指示組合器服務將兩個PDF文檔合併為單個PDF文檔。

**參考輸入PDF文檔**

參考要傳遞至組合器服務的輸入PDF文檔。 例如，如果要傳遞名為Map and Directions的兩個輸入PDF文檔，則必須傳遞相應的PDF檔案。

map.pdf檔案和directions.pdf檔案都必須放置在集合物件中。 鍵的名稱必須與DDX文檔中PDF源屬性的值匹配。 如果DDX文檔中的鍵和源屬性匹配，則PDF檔案的名稱不重要。

>[!NOTE]
>
>安 `AssemblerResult` 如果您叫用 `invokeDDX` 操作。 當將兩個或兩個以上輸入PDF文檔傳遞到組合器服務時，將使用此操作。 但是，如果只將一個輸入PDF傳遞到組合器服務，並且只需要一個返回文檔，請調用 `invokeOneDocument` 操作。 調用此操作時，將返回單個文檔。 如需使用此操作的詳細資訊，請參閱 [組裝加密的PDF文檔](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。 如需可設定的執行階段選項相關資訊，請參閱 `AssemblerOptionSpec` 類引用 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**組合輸入PDF文檔**

建立服務客戶端、引用DDX檔案、建立儲存輸入PDF文檔的集合對象和設定運行時選項後，可以調用DDX操作。 使用本節中指定的DDX文檔時，map.pdf和direction.pdf檔案將合併到一個PDF文檔中。

**擷取結果**

組合器服務返回 `java.util.Map` 物件，可從 `AssemblerResult` 對象，且包含操作結果。 傳回 `java.util.Map` 對象包含生成的文檔和任何例外。

下表匯總了返回的中可以找到的一些鍵值和對象類型 `java.util.Map` 物件。

<table>
 <thead>
  <tr>
   <th><p>索引鍵值</p></th>
   <th><p>物件類型</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>包含在DDX結果元素中指定的結果文檔</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>包含文檔的任何例外</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>包含作業日誌</p></td>
  </tr>
 </tbody>
</table>

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式分解PDF文檔](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API組合PDF檔案 {#assemble-pdf-documents-using-the-java-api}

使用組合器服務API(Java)組合PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞指定DDX檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 參考輸入PDF文檔。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象，方法是使用 `HashMap` 建構子。
   * 對於每個輸入PDF文檔，建立 `java.io.FileInputStream` 對象，使用其建構子並傳遞輸入PDF文檔的位置。
   * 對於每個輸入PDF文檔，建立 `com.adobe.idp.Document` 物件，並傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。
   * 對於每個輸入文檔，向 `java.util.Map` 對象 `put` 方法，並傳遞下列引數：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
      * A `com.adobe.idp.Document` 物件(或 `java.util.List` 指定多個文檔的對象)，包含源PDF文檔。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 通過調用屬於的方法來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 物件 `setFailOnError` 方法和傳遞 `false`.

1. 組合輸入PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列必要值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含要組合的輸入PDF檔案的對象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項（包括預設字型和作業日誌級別）的對象

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含作業結果的對象以及發生的任何例外。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 叫用 `AssemblerResult` 物件 `getDocuments` 方法。 這會傳回 `java.util.Map` 物件。
   * 重複 `java.util.Map` 對象，直到找到結果 `com.adobe.idp.Document` 物件。 (您可以使用DDX文檔中指定的PDF結果元素來獲取文檔。)
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取PDF檔案。

   >[!NOTE]
   >
   >若 `LOG_LEVEL` 設為產生記錄檔，您可使用 `AssemblerResult` 物件 `getJobLog` 方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API組裝PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API組合PDF文檔 {#assemble-pdf-documents-using-the-web-service-api}

使用組合器服務API（web服務）組合PDF文檔：

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
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。

1. 參考輸入PDF文檔。

   * 對於每個輸入PDF文檔，建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存輸入PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此收集對象用於儲存輸入PDF文檔。
   * 對於每個輸入PDF文檔，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。 例如，如果使用兩個輸入PDF檔案，請建立兩個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `key` 欄位。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 (對每個輸入PDF文檔執行此任務。)
   * 指派 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `value` 欄位。 (對每個輸入PDF文檔執行此任務。)
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` 物件 `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 (對每個輸入PDF文檔執行此任務。)

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 為屬於的資料成員指定值，以設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 物件 `failOnError` 資料成員。

1. 組合輸入PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invoke` 方法，並傳遞下列值：

   * A `BLOB` 表示DDX文檔的對象。
   * 此 `mapItem` 包含輸入PDF文檔的陣列。 其鍵必須與PDF源檔案的名稱匹配，且其值必須為 `BLOB` 對應於那些檔案的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   此 `invoke` 方法傳回 `AssemblerResult` 包含作業結果的對象以及可能發生的任何例外。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 存取 `AssemblerResult` 物件 `documents` 欄位，即 `Map` 包含結果PDF文檔的對象。
   * 重複 `Map` 對象，直到找到與生成文檔的名稱匹配的鍵。 然後將該陣列成員的 `value` 到 `BLOB`.
   * 通過訪問PDF文檔來提取代表文檔的二進位資料 `BLOB` 物件 `MTOM` 屬性。 這會傳回一個位元組陣列，您可將其寫出至PDF檔案。

   >[!NOTE]
   >
   >若 `LOG_LEVEL` 設為產生記錄檔，您可以透過取得 `AssemblerResult` 物件 `jobLog` 資料成員。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
