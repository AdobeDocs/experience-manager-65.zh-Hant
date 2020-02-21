---
title: 以程式設計方式組合PDF檔案
seo-title: 以程式設計方式組合PDF檔案
description: 'null'
seo-description: 'null'
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
translation-type: tm+mt
source-git-commit: 868936e0fd20d3867e31f0351d7b388149472fd2

---


# 以程式設計方式組合PDF檔案 {#programmatically-assembling-pdf-documents}

您可以使用Assembler Service API將多個PDF檔案組合為單一PDF檔案。 下圖顯示三個PDF檔案合併為單一PDF檔案。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

若要將兩份或多份PDF檔案整合為單一PDF檔案，您需要DDX檔案。 DDX文檔描述了Assembler服務生成的PDF文檔。 即，DDX文檔指示Assembler服務執行哪些操作。

在本討論中，假設使用了以下DDX文檔。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

此DDX檔案將兩份名為 *map.pdf* 和 ** directions.pdf的PDF檔案合併為單一PDF檔案。

>[!NOTE]
>
>若要查看拆解PDF檔案的DDX檔案，請參閱以程式設 [計方式解譯PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)。

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參 [閱Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 使用web services調用Assembler服務時的注意事項 {#considerations-when-invoking-assembler-service-using-web-services}

在組裝大型檔案時，當您新增頁首和頁尾時，可能會發 `OutOfMemory` 生錯誤，而且不會組裝檔案。 若要降低發生此問題的機率，請新增 `DDXProcessorSetting` 元素至DDX檔案，如下列範例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

您可以將此元素新增為元素的 `DDX` 子系或元素的子 `PDF result` 系。 此設定的預設值為0（零），會關閉勾選點，而DDX的運作就像元素 `DDXProcessorSetting` 不存在一樣。 如果您遇到錯 `OutOfMemory` 誤，可能需要將值設為整數，通常介於500到5000之間。 小查核點值會導致檢查點更頻繁。

## 步驟摘要 {#summary-of-steps}

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
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如果AEM Forms部署在JBoss以外的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為JAR檔案，而JAR檔案是部署AEM Forms的J2EE應用程式伺服器專用的檔案。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合PDF檔案。 例如，請考慮本節中介紹的DDX文檔。 此DDX檔案指示Assembler服務將兩個PDF檔案合併為單一PDF檔案。

**參考輸入PDF檔案**

參考要傳遞至Assembler服務的輸入PDF檔案。 例如，如果要傳遞兩個名為「地圖」和「方向」的輸入PDF檔案，則必須傳遞對應的PDF檔案。

map.pdf檔案和directions.pdf檔案都必須放在系列物件中。 索引鍵的名稱必須與DDX檔案中PDF來源屬性的值相符。 如果DDX檔案中的索引鍵和來源屬性相符，則PDF檔案的名稱無關緊要。

>[!NOTE]
>
>如果 `AssemblerResult` 您叫用此操作，則會傳回包含系列物件的物 `invokeDDX` 件。 當您將兩個或兩個以上的輸入PDF檔案傳遞至Assembler服務時，就會使用此操作。 但是，如果只將一個輸入PDF傳遞給Assembler服務，而且只需要一個返回文檔，請調用該操 `invokeOneDocument` 作。 調用此操作時，將返回單個文檔。 如需使用此作業的詳細資訊，請參 [閱組合加密的PDF檔案](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。 如需您可設定之執行時期選項的詳細資訊，請參閱 `AssemblerOptionSpec`[AEM Forms API參考中的類別參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**匯整輸入的PDF檔案**

在您建立服務用戶端、參考DDX檔案、建立儲存輸入PDF檔案的系列物件，以及設定執行時期選項後，您就可以叫用DDX作業。 使用本節中指定的DDX檔案時，map.pdf和direction.pdf檔案會合併為一個PDF檔案。

**擷取結果**

Assembler服務返回一 `java.util.Map` 個對象，該對象可從該對象中獲 `AssemblerResult` 得，並包含操作結果。 返回的對 `java.util.Map` 像包含生成的文檔和任何例外。

下表匯總了返回對象中可以找到的一些鍵值和對象類型 `java.util.Map` 。

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

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式解譯PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API匯整PDF檔案 {#assemble-pdf-documents-using-the-java-api}

使用Assembler Service API(Java)來組合PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `AssemblerServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考現有的DDX檔案。

   * 使用 `java.io.FileInputStream` 其建構子並傳遞指定DDX檔案位置的字串值，建立表示DDX文檔的對象。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 參考輸入PDF檔案。

   * 使用 `java.util.Map` 建構函式建立用來儲存輸入PDF檔案的物 `HashMap` 件。
   * 對於每個輸入的PDF檔案，請使 `java.io.FileInputStream` 用其建構函式並傳遞輸入的PDF檔案位置來建立物件。
   * 對於每個輸入的PDF檔案，請建 `com.adobe.idp.Document` 立物件並傳遞包 `java.io.FileInputStream` 含PDF檔案的物件。
   * 對於每個輸入文檔，通過調用其方法 `java.util.Map` 並傳遞以下引 `put` 數，向對象添加條目：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
      * 包 `com.adobe.idp.Document` 含來源PDF `java.util.List` 檔案的物件（或指定多份檔案的物件）。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 調用屬於該對象的方法，以設定運行時選項以滿足您的業務 `AssemblerOptionSpec` 要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用 `AssemblerOptionSpec` 物件的方 `setFailOnError` 法並傳遞 `false`。

1. 組合輸入的PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列必要值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文檔的對象
   * 包 `java.util.Map` 含要組合的輸入PDF檔案的對象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 運行時選項（包括預設字型和作業日誌級別）的對象
   該方 `invokeDDX` 法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 一個對象，該對象包含作業結果和所發生的任何異常。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的方 `getDocuments` 法。 這會傳回 `java.util.Map` 物件。
   * 重複該對 `java.util.Map` 像，直到找到結果對 `com.adobe.idp.Document` 像。 （您可以使用DDX檔案中指定的PDF結果元素來取得檔案。）
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法以擷取PDF檔案。
   >[!NOTE]
   >
   >如果 `LOG_LEVEL` 設定為生成日誌，則可使用對象的方法 `AssemblerResult` 提取日 `getJobLog` 志。

**另請參閱**

[快速入門（SOAP模式）:使用Java API組合PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API匯整PDF檔案 {#assemble-pdf-documents-using-the-web-service-api}

使用Assembler Service API(web service)來組合PDF檔案：

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
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 參考輸入PDF檔案。

   * 對於每個輸入的PDF檔案，請使用 `BLOB` 其建構函式來建立物件。 物件 `BLOB` 用來儲存輸入的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。
   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 此收集物件用於儲存輸入的PDF檔案。
   * 對於每個輸入的PDF檔案，請建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。 例如，如果使用兩個輸入的PDF檔案，請建立兩個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 為對象欄位指定代表鍵名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字串 `key` 值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。 （請對每個輸入的PDF檔案執行此工作。）
   * 將存 `BLOB` 儲PDF文檔的對象指 `MyMapOf_xsd_string_To_xsd_anyType_Item` 派到對 `value` 像欄位。 （請對每個輸入的PDF檔案執行此工作。）
   * 將對象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 添加到對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 調用對 `MyMapOf_xsd_string_To_xsd_anyType` 像的方 `Add` 法並傳遞對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 （請對每個輸入的PDF檔案執行此工作。）

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 通過為屬於該對象的資料成員分配值，設定運行時選項以滿足您的業務需 `AssemblerOptionSpec` 求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請指 `false` 派給 `AssemblerOptionSpec` 物件的資料 `failOnError` 成員。

1. 組合輸入的PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invoke` 法並傳遞下列值：

   * 表 `BLOB` 示DDX文檔的對象。
   * 包含 `mapItem` 輸入PDF檔案的陣列。 其鍵必須與PDF源檔案的名稱匹配，其值必須是對應 `BLOB` 於這些檔案的對象。
   * 指定 `AssemblerOptionSpec` 運行時選項的對象。
   該方 `invoke` 法返回 `AssemblerResult` 一個對象，該對象包含作業的結果和可能發生的任何例外。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取物 `AssemblerResult` 件的欄 `documents` 位，此欄位是包含 `Map` 結果PDF檔案的物件。
   * 重複該對 `Map` 像，直到找到與生成文檔的名稱匹配的鍵。 然後將該陣列成員轉 `value` 換為 `BLOB`。
   * 存取PDF檔案的物件屬性，以擷取代表PDF文 `BLOB` 件的二進位 `MTOM` 資料。 這會傳回可寫出至PDF檔案的位元組陣列。
   >[!NOTE]
   >
   >如果 `LOG_LEVEL` 設定為生成日誌，則可以通過獲取對象資料成員的值來 `AssemblerResult` 提取日 `jobLog` 志。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
