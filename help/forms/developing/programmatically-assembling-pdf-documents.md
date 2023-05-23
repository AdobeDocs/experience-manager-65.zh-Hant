---
title: 以寫程式方式裝配PDF文檔
seo-title: Programmatically Assembling PDF Documents
description: 使用匯編器服務API可使用Java API和Web服務API將多個PDF文檔匯編為單個PDF文檔。
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

# 以寫程式方式裝配PDF文檔 {#programmatically-assembling-pdf-documents}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

您可以使用匯編器服務API將多個PDF文檔匯編為單個PDF文檔。 下圖顯示三個PDF文檔正在合併到單個PDF文檔中。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

要將兩個或多個PDF文檔組合為單個PDF文檔，需要DDX文檔。 DDX文檔描述匯編器服務生成的PDF文檔。 即，DDX文檔指示匯編程式執行哪些操作。

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

此DDX文檔合併兩個名為 *地圖.pdf* 和 *方向.pdf* 一個PDF文檔。

>[!NOTE]
>
>要查看分解PDF文檔的DDX文檔，請參閱 [以寫程式方式分解PDF文檔](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)。

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 使用Web服務調用匯編器服務時的注意事項 {#considerations-when-invoking-assembler-service-using-web-services}

在組裝大型文檔期間添加頁眉和頁腳時，可能會遇到 `OutOfMemory` 錯誤，檔案將不會裝配。 要降低出現此問題的可能性，請添加 `DDXProcessorSetting` 元素，如下例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

可以將此元素添加為 `DDX` 元素或作為 `PDF result` 的子菜單。 此設定的預設值為0（零），它關閉複選點，DDX的行為與 `DDXProcessorSetting` 元素不存在。 如果你遇到 `OutOfMemory` 錯誤，您可能需要將值設定為整數，通常介於500和5000之間。 小的檢查點值導致檢查點更頻繁。

## 步驟摘要 {#summary-of-steps}

要從多個PDF文檔匯編單個PDF文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立PDF匯編器客戶端。
1. 引用現有DDX文檔。
1. 引用輸入PDF文檔。
1. 設定運行時選項。
1. 匯編輸入PDF文檔。
1. 提取結果。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援的J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立PDF匯編器客戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器客戶端。

**引用現有DDX文檔**

必須引用DDX文檔來匯編PDF文檔。 例如，請考慮本節中介紹的DDX文檔。 此DDX文檔指示匯編程式服務將兩個PDF文檔合併到單個PDF文檔中。

**引用輸入PDF文檔**

引用要傳遞到匯編器服務的輸入PDF文檔。 例如，如果要傳遞名為「映射」(Map)和「方向」(Directions)的兩個輸入PDF文檔，則必須傳遞相應的PDF檔案。

map.pdf檔案和directions.pdf檔案都必須放在集合對象中。 鍵的名稱必須與DDX文檔中PDF源屬性的值匹配。 如果DDX文檔中的鍵和源屬性匹配，則PDF檔案的名稱是什麼並不重要。

>[!NOTE]
>
>安 `AssemblerResult` 如果調用集合對象，則返回該對象 `invokeDDX` 的下界。 將兩個或多個輸入PDF文檔傳遞到匯編器服務時，將使用此操作。 但是，如果您只將一個輸入PDF傳遞給匯編器服務，並且只期望有一個返回文檔，請調用 `invokeOneDocument` 的下界。 調用此操作時，將返回單個文檔。 有關使用此操作的資訊，請參見 [組裝加密的PDF文檔](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)。

**設定運行時選項**

您可以設定運行時選項，這些選項在匯編程式服務執行作業時控制其行為。 例如，您可以設定一個選項，指示匯編程式服務在遇到錯誤時繼續處理作業。 有關可設定的運行時選項的資訊，請參見 `AssemblerOptionSpec` 類引用 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**匯編輸入PDF文檔**

在建立服務客戶端、引用DDX檔案、建立儲存輸入PDF文檔的集合對象和設定運行時選項後，可以調用DDX操作。 使用本節中指定的DDX文檔時，map.pdf和direction.pdf檔案將合併到一個PDF文檔中。

**提取結果**

匯編器服務返回 `java.util.Map` 對象，可從 `AssemblerResult` 對象，其中包含操作結果。 返回 `java.util.Map` 對象包含結果文檔和任何異常。

下表匯總了返回的 `java.util.Map` 的雙曲餘切值。

<table>
 <thead>
  <tr>
   <th><p>鍵值</p></th>
   <th><p>對象類型</p></th>
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

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式分解PDF文檔](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API匯編PDF文檔 {#assemble-pdf-documents-using-the-java-api}

使用匯編器服務API(Java)匯編PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用現有DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定DDX檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 引用輸入PDF文檔。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象 `HashMap` 建構子。
   * 對於每個輸入PDF文檔，建立 `java.io.FileInputStream` 使用其建構子並傳遞輸入PDF文檔的位置。
   * 對於每個輸入PDF文檔，建立 `com.adobe.idp.Document` 並傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。
   * 對於每個輸入文檔，向 `java.util.Map` 通過調用對象 `put` 方法並傳遞以下參數：

      * 表示鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
      * A `com.adobe.idp.Document` 對象 `java.util.List` 指定多個文檔的對象)。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過調用屬於的方法來設定運行時選項以滿足業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 對象 `setFailOnError` 方法 `false`。

1. 匯編輸入PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下所需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含要裝配的輸入PDF檔案的對象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象，包括預設字型和作業日誌級別

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含作業結果和所發生的任何異常的對象。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 調用 `AssemblerResult` 對象 `getDocuments` 的雙曲餘切值。 這返回 `java.util.Map` 的雙曲餘切值。
   * 迭代 `java.util.Map` 直到找到結果 `com.adobe.idp.Document` 的雙曲餘切值。 (可以使用DDX文檔中指定的PDF結果元素獲取文檔。)
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取PDF文檔。

   >[!NOTE]
   >
   >如果 `LOG_LEVEL` 設定為生成日誌，可使用 `AssemblerResult` 對象 `getJobLog` 的雙曲餘切值。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API組裝PDF文檔](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API匯編PDF文檔 {#assemble-pdf-documents-using-the-web-service-api}

使用匯編器服務API（Web服務）匯編PDF文檔：

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
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 引用輸入PDF文檔。

   * 對於每個輸入PDF文檔，建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存輸入PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 此集合對象用於儲存輸入PDF文檔。
   * 對於每個輸入PDF文檔，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。 例如，如果使用兩個輸入PDF文檔，則建立兩個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象。
   * 為指定表示鍵名的字串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `key` 的子菜單。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 (為每個輸入PDF文檔執行此任務。)
   * 分配 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `value` 的子菜單。 (為每個輸入PDF文檔執行此任務。)
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 調用 `MyMapOf_xsd_string_To_xsd_anyType` 對象 `Add` 方法和通過 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 (為每個輸入PDF文檔執行此任務。)

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過將值分配給屬於的資料成員來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編程式服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 對象 `failOnError` 資料成員。

1. 匯編輸入PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invoke` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象。
   * 的 `mapItem` 包含輸入PDF文檔的陣列。 其鍵必須與PDF源檔案的名稱匹配，其值必須為 `BLOB` 對應於這些檔案的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   的 `invoke` 方法返回 `AssemblerResult` 包含作業結果的對象以及可能發生的任何異常。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問 `AssemblerResult` 對象 `documents` 欄位， `Map` 包含結果PDF文檔的對象。
   * 迭代 `Map` 對象，直到找到與結果文檔的名稱匹配的鍵。 然後轉換該陣列成員 `value` 到 `BLOB`。
   * 通過訪問PDF文檔來提取表示該文檔的二進位資料 `BLOB` 對象 `MTOM` 屬性。 這將返回可以寫入PDF檔案的位元組陣列。

   >[!NOTE]
   >
   >如果 `LOG_LEVEL` 設定為生成日誌，通過獲取日誌的 `AssemblerResult` 對象 `jobLog` 資料成員。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
