---
title: 以程式設計方式組合PDF檔案
seo-title: 以程式設計方式組合PDF檔案
description: 使用Assembler服務API，使用Java API和Web Service API，將多個PDF檔案組合為單一PDF檔案。
seo-description: 使用Assembler服務API，使用Java API和Web Service API，將多個PDF檔案組合為單一PDF檔案。
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---


# 以程式設計方式組合PDF檔案{#programmatically-assembling-pdf-documents}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

您可以使用Assembler Service API將多個PDF檔案組合為單一PDF檔案。 下圖顯示三個PDF檔案合併為單一PDF檔案。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

若要將兩份或多份PDF檔案整合為單一PDF檔案，您需要DDX檔案。 DDX文檔描述了Assembler服務生成的PDF文檔。 即，DDX文檔指示Assembler服務執行哪些操作。

在本討論中，假設使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

此DDX檔案將名為&#x200B;*map.pdf*&#x200B;和&#x200B;*directions.pdf*&#x200B;的兩份PDF檔案合併為一份PDF檔案。

>[!NOTE]
>
>要查看拆解PDF文檔的DDX文檔，請參閱[Programmaly Desprication PDF Documents](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)。

>[!NOTE]
>
>有關Assembler服務的詳細資訊，請參見[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 使用web services {#considerations-when-invoking-assembler-service-using-web-services}調用Assembler服務時的注意事項

在組裝大型檔案時，當您新增頁首和頁尾時，可能會遇到`OutOfMemory`錯誤，檔案將無法組裝。 若要降低發生此問題的機率，請新增`DDXProcessorSetting`元素至DDX檔案，如下列範例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

您可以將此元素新增為`DDX`元素的子系，或作為`PDF result`元素的子系。 此設定的預設值為0（零），會關閉核取點，而DDX的運作就像`DDXProcessorSetting`元素不存在一樣。 如果您遇到`OutOfMemory`錯誤，可能需要將值設為整數，通常介於500和5000之間。 小查核點值會導致檢查點更頻繁。

## 步驟{#summary-of-steps}摘要

若要從多份PDF檔案組合單一PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考輸入PDF檔案。
1. 設定執行時期選項。
1. 組合輸入的PDF檔案。
1. 擷取結果。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合PDF檔案。 例如，請考慮本節中介紹的DDX文檔。 此DDX檔案指示Assembler服務將兩個PDF檔案合併為單一PDF檔案。

**參考輸入PDF檔案**

參考要傳遞至Assembler服務的輸入PDF檔案。 例如，如果要傳遞兩個名為「地圖」和「方向」的輸入PDF檔案，則必須傳遞對應的PDF檔案。

map.pdf檔案和directions.pdf檔案都必須放在系列物件中。 索引鍵的名稱必須與DDX檔案中PDF來源屬性的值相符。 如果DDX檔案中的索引鍵和來源屬性相符，則PDF檔案的名稱無關緊要。

>[!NOTE]
>
>如果調用`invokeDDX`操作，則返回包含集合對象的`AssemblerResult`對象。 當您將兩個或兩個以上的輸入PDF檔案傳遞至Assembler服務時，就會使用此操作。 但是，如果只將一個輸入的PDF傳遞給Assembler服務，而且只需要一個返回文檔，請調用`invokeOneDocument`操作。 調用此操作時，將返回單個文檔。 有關使用此操作的資訊，請參閱[組合加密的PDF文檔](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。 有關可設定的運行時選項的資訊，請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類參考。

**匯整輸入的PDF檔案**

在您建立服務用戶端、參考DDX檔案、建立儲存輸入PDF檔案的系列物件，以及設定執行時期選項後，您就可以叫用DDX作業。 使用本節中指定的DDX檔案時，map.pdf和direction.pdf檔案會合併為一個PDF檔案。

**擷取結果**

Assembler服務返回一個`java.util.Map`對象，該對象可從`AssemblerResult`對象中獲得，並包含操作結果。 傳回的`java.util.Map`物件包含產生的檔案和任何例外。

下表匯總了返回的`java.util.Map`對象中可以找到的一些鍵值和對象類型。

<table>
 <thead>
  <tr>
   <th><p>關鍵值</p></th>
   <th><p>物件類型</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>包含在DDX合成元素中指定的合成文檔</p></td>
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

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式解譯PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API {#assemble-pdf-documents-using-the-java-api}組合PDF檔案

使用Assembler Service API(Java)來組合PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 參考現有的DDX檔案。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 參考輸入PDF檔案。

   * 使用`HashMap`建構函式建立`java.util.Map`物件，用來儲存輸入的PDF檔案。
   * 對於每個輸入的PDF檔案，請使用其建構函式並傳遞輸入的PDF檔案位置來建立`java.io.FileInputStream`物件。
   * 對於每個輸入的PDF文檔，請建立`com.adobe.idp.Document`對象並傳遞包含PDF文檔的`java.io.FileInputStream`對象。
   * 對於每個輸入文檔，通過調用`put`方法並傳遞以下參數，向`java.util.Map`對象添加一個條目：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
      * 包含源PDF文檔的`com.adobe.idp.Document`對象（或`java.util.List`對象，指定多個文檔）。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法，設定運行時選項以滿足您的業務要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法並傳遞`false`。

1. 組合輸入的PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列必要值：

   * `com.adobe.idp.Document`物件，代表要使用的DDX檔案
   * 包含要組合的輸入PDF檔案的`java.util.Map`對象
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件，指定執行時間選項，包括預設字型和工作記錄層級

   `invokeDDX`方法返回一個`com.adobe.livecycle.assembler.client.AssemblerResult`對象，該對象包含作業的結果和發生的任何例外。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 這會傳回`java.util.Map`物件。
   * 重複`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件。 （您可以使用DDX檔案中指定的PDF結果元素來取得檔案。）
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

   >[!NOTE]
   >
   >如果`LOG_LEVEL`設定為生成日誌，則可以使用`AssemblerResult`對象的`getJobLog`方法提取日誌。

**另請參閱**

[快速入門（SOAP模式）:使用Java API組合PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#assemble-pdf-documents-using-the-web-service-api}組合PDF檔案

使用Assembler Service API(web service)來組合PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存DDX檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立對象，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 參考輸入PDF檔案。

   * 對於每個輸入的PDF檔案，請使用其建構函式建立`BLOB`物件。 `BLOB`物件用來儲存輸入的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`對象。 此收集物件用於儲存輸入的PDF檔案。
   * 對於每個輸入的PDF檔案，請建立`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。 例如，如果使用兩個輸入的PDF檔案，請建立兩個`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配代表鍵名的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。 （請對每個輸入的PDF檔案執行此工作。）
   * 將儲存PDF文檔的`BLOB`對象指定給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。 （請對每個輸入的PDF檔案執行此工作。）
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`對象添加到`MyMapOf_xsd_string_To_xsd_anyType`對象。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （請對每個輸入的PDF檔案執行此工作。）

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的資料成員分配值，設定運行時選項以滿足您的業務要求。 例如，要指示Assembler服務在出現錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合輸入的PDF檔案。

   叫用`AssemblerServiceClient`物件的`invoke`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象。
   * 包含輸入PDF檔案的`mapItem`陣列。 其鍵必須與PDF源檔案的名稱匹配，其值必須是與這些檔案對應的`BLOB`對象。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invoke`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和可能發生的任何例外。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是包含結果PDF檔案的`Map`物件。
   * 重複`Map`物件，直到找到與結果檔案名稱相符的索引鍵。 然後將該陣列成員的`value`轉換為`BLOB`。
   * 存取PDF檔案的`BLOB`物件的`MTOM`屬性，擷取代表PDF檔案的二進位資料。 這會傳回可寫出至PDF檔案的位元組陣列。

   >[!NOTE]
   >
   >如果`LOG_LEVEL`設定為生成日誌，則可以通過獲取`AssemblerResult`對象的`jobLog`資料成員的值來提取日誌。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
