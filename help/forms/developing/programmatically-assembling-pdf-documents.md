---
title: 以程式設計方式組合PDF檔案
seo-title: 以程式設計方式組合PDF檔案
description: 使用組合器服務API，使用Java API和Web服務API將多個PDF文檔組合為單個PDF文檔。
seo-description: 使用組合器服務API，使用Java API和Web服務API將多個PDF文檔組合為單個PDF文檔。
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
source-wordcount: '2152'
ht-degree: 0%

---

# 以寫程式方式組合PDF文檔{#programmatically-assembling-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以使用組合器服務API將多個PDF文檔組合為單個PDF文檔。 下圖顯示三個PDF檔案合併為單一PDF檔案。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

要將兩個或多個PDF文檔組合為單個PDF文檔，需要DDX文檔。 DDX文檔描述組合器服務生成的PDF文檔。 也就是說，DDX文檔指示組合器服務執行哪些操作。

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

此DDX文檔將名為&#x200B;*map.pdf*&#x200B;和&#x200B;*directions.pdf*&#x200B;的兩個PDF文檔合併為單個PDF文檔。

>[!NOTE]
>
>要查看分解PDF文檔的DDX文檔，請參閱[以寫程式方式分解PDF文檔](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 使用Web服務調用組合器服務時的注意事項{#considerations-when-invoking-assembler-service-using-web-services}

在裝配大型文檔期間添加頁眉和頁腳時，可能會遇到`OutOfMemory`錯誤，檔案將不會裝配。 若要降低發生此問題的機率，請新增`DDXProcessorSetting`元素至您的DDX檔案，如下列範例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

您可以將此元素新增為`DDX`元素的子項，或新增為`PDF result`元素的子項。 此設定的預設值為0（零），這會關閉勾選點，而DDX的行為就像`DDXProcessorSetting`元素不存在一樣。 如果您遇到`OutOfMemory`錯誤，則可能需要將值設定為整數，通常介於500和5000之間。 小的查核點值會導致查核點更頻繁。

## 步驟{#summary-of-steps}的摘要

要從多個PDF文檔組合單個PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考輸入的PDF文檔。
1. 設定運行時選項。
1. 組合輸入的PDF文檔。
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

必須參考DDX文檔才能組合PDF文檔。 例如，請考量本節中引入的DDX檔案。 此DDX文檔指示組合器服務將兩個PDF文檔合併為單個PDF文檔。

**參考輸入PDF文檔**

參考要傳遞至組合器服務的輸入PDF文檔。 例如，如果要傳遞名為「地圖」和「方向」的兩個輸入PDF文檔，則必須傳遞相應的PDF檔案。

map.pdf檔案和directions.pdf檔案都必須放置在集合物件中。 鍵的名稱必須與DDX文檔中PDF源屬性的值匹配。 如果DDX文檔中的鍵和源屬性匹配，則PDF檔案的名稱不重要。

>[!NOTE]
>
>如果調用`invokeDDX`操作，則返回`AssemblerResult`對象，該對象包含集合對象。 將兩個或兩個以上輸入的PDF文檔傳遞到組合器服務時，將使用此操作。 但是，如果只將一個輸入PDF傳遞到組合器服務，並且只需要一個返回文檔，請調用`invokeOneDocument`操作。 調用此操作時，將返回單個文檔。 有關使用此操作的資訊，請參閱[組合加密的PDF文檔](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。 如需可設定的執行階段選項相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

**組合輸入的PDF文檔**

建立服務客戶端、引用DDX檔案、建立儲存輸入PDF文檔的集合對象和設定運行時選項後，可以調用DDX操作。 使用本節中指定的DDX文檔時，map.pdf和direction.pdf檔案合併為一個PDF文檔。

**擷取結果**

組合器服務返回一個`java.util.Map`對象，該對象可從`AssemblerResult`對象中獲取，並且包含操作結果。 傳回的`java.util.Map`物件包含產生的檔案和任何例外。

下表匯總了可以位於返回的`java.util.Map`對象中的一些鍵值和對象類型。

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

[以程式設計方式解譯PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API {#assemble-pdf-documents-using-the-java-api}組合PDF文檔

使用組合器服務API(Java)組合PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 參考現有的DDX文檔。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 參考輸入的PDF文檔。

   * 使用`HashMap`建構子建立用於儲存輸入PDF文檔的`java.util.Map`對象。
   * 對於每個輸入PDF文檔，使用其建構子並傳遞輸入PDF文檔的位置來建立`java.io.FileInputStream`對象。
   * 對於每個輸入的PDF文檔，建立`com.adobe.idp.Document`對象，並傳遞包含PDF文檔的`java.io.FileInputStream`對象。
   * 對於每個輸入文檔，通過調用`put`方法並傳遞以下參數將條目添加到`java.util.Map`對象中：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
      * 包含源PDF文檔的`com.adobe.idp.Document`對象（或指定多個文檔的`java.util.List`對象）。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法來設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用`AssemblerOptionSpec`對象的`setFailOnError`方法並傳遞`false`。

1. 組合輸入的PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下必需值：

   * 表示要使用的DDX文檔的`com.adobe.idp.Document`對象
   * `java.util.Map`對象，包含要組合的輸入PDF檔案
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，指定運行時選項，包括預設字型和作業日誌級別

   `invokeDDX`方法返回一個`com.adobe.livecycle.assembler.client.AssemblerResult`對象，該對象包含作業的結果和發生的任何異常。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 調用`AssemblerResult`對象的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 對`java.util.Map`對象進行迭代，直到找到結果`com.adobe.idp.Document`對象。 （您可以使用DDX文檔中指定的PDF結果元素來獲取文檔。）
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取PDF文檔。

   >[!NOTE]
   >
   >如果`LOG_LEVEL`被設定為生成日誌，則可以使用`AssemblerResult`對象的`getJobLog`方法提取日誌。

**另請參閱**

[快速入門（SOAP模式）:使用Java API組裝PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#assemble-pdf-documents-using-the-web-service-api}組合PDF文檔

使用組合器服務API（Web服務）組合PDF文檔：

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
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 參考輸入的PDF文檔。

   * 對於每個輸入的PDF文檔，使用其建構子建立`BLOB`對象。 `BLOB`對象用於儲存輸入的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此收集對象用於儲存輸入的PDF文檔。
   * 對於每個輸入的PDF文檔，建立`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。 例如，如果使用兩個輸入的PDF文檔，請建立兩個`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配表示鍵名的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 （對每個輸入的PDF文檔執行此任務。）
   * 將儲存PDF文檔的`BLOB`對象指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。 （對每個輸入的PDF文檔執行此任務。）
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （對每個輸入的PDF文檔執行此任務。）

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 為屬於`AssemblerOptionSpec`對象的資料成員分配值，以設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合輸入的PDF文檔。

   調用`AssemblerServiceClient`對象的`invoke`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象。
   * 包含輸入PDF文檔的`mapItem`陣列。 其鍵必須與PDF源檔案的名稱匹配，其值必須是與這些檔案對應的`BLOB`對象。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invoke`方法返回一個`AssemblerResult`對象，該對象包含作業的結果以及可能發生的任何異常。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問`AssemblerResult`對象的`documents`欄位，該欄位是包含結果PDF文檔的`Map`對象。
   * 逐一查看`Map`對象，直到找到與結果文檔的名稱匹配的鍵。 然後將該陣列成員的`value`轉換為`BLOB`。
   * 通過訪問其`BLOB`對象的`MTOM`屬性來提取表示PDF文檔的二進位資料。 這會傳回可寫出為PDF檔案的位元組陣列。

   >[!NOTE]
   >
   >如果`LOG_LEVEL`被設定為生成日誌，則可以通過獲取`AssemblerResult`對象的`jobLog`資料成員的值來提取日誌。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
