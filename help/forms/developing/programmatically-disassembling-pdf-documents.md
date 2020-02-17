---
title: 以程式設計方式解譯PDF檔案
seo-title: 以程式設計方式解譯PDF檔案
description: 'null'
seo-description: 'null'
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 以程式設計方式解譯PDF檔案 {#programmatically-disassembling-pdf-documents}

您可以將PDF檔案傳遞至Assembler服務，以反匯編檔案。 通常，當PDF檔案最初是由許多個別檔案（例如陳述式集合）建立時，這項工作很有用。 在下圖中，DocA被分成多個結果文檔，其中頁面上的第一級書籤標識新結果文檔的開始。

![pd_pd_pdf來自書籤](assets/pd_pd_pdfsfrombookmarks.png)

若要反匯編PDF檔案，請確 `PDFsFromBookmarks` 定元素位於DDX檔案中。 元 `PDFsFromBookmarks` 素是合成元素，只能是元素的子元 `DDX` 素。 它沒有屬性， `result` 因為它可導致生成多個文檔。

元 `PDFsFromBookmarks` 素會針對來源檔案中的每個1級書籤產生單一檔案。

在本討論中，假設使用了以下DDX文檔。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用Assembler服務來組合PDF檔案。 (請參閱 [以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>將單一PDF檔案傳送至Assembler服務並傳回單一檔案時，您可以叫用該 `invokeOneDocument` 操作。 但是，要反匯編PDF文檔，請使用該操作，因為 `invokeDDX` 儘管一個輸入的PDF文檔被傳遞到Assembler服務，Assembler服務仍返回包含一個或多個文檔的集合對象。

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參 [閱Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要拆解PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考要反匯編的PDF文檔。
1. 設定執行時期選項。
1. 反匯編PDF檔案。
1. 儲存已拆解的PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar取代為JAR檔案，而JAR檔案是部署AEM Forms的J2EE應用程式伺服器專用。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案，才能反匯編PDF檔案。 此DDX檔案必須包含 `PDFsFromBookmarks` 元素。

**參考PDF檔案以反匯編**

要反匯編PDF文檔，請參考表示要反匯編的PDF文檔的PDF檔案。 傳遞至Assembler服務時，會針對檔案中的每個第1級書籤傳回個別的PDF檔案。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。

**反匯編PDF檔案**

在您建立Assembler服務用戶端、參考DDX檔案、參考要反匯編的PDF檔案，以及設定執行時期選項後，您就可以叫用方法來反匯編PDF文 `invokeDDX` 件。 如果DDX檔案包含反匯編PDF檔案的指示，Assembler服務會在收集物件中傳回已拆解的PDF檔案。

**儲存已拆解的PDF檔案**

所有已拆解的PDF檔案都會傳回至系列物件中。 逐步處理系列物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API解譯PDF檔案 {#disassemble-a-pdf-document-using-the-java-api}

使用Assembler Service API(Java)拆解PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `AssemblerServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考現有的DDX檔案。

   * 使用 `java.io.FileInputStream` 其建構子並傳遞指定DDX檔案位置的字串值，建立表示DDX文檔的對象。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 參考要反匯編的PDF文檔。

   * 使用 `java.util.Map` 建構函式建立用來儲存輸入PDF檔案的物 `HashMap` 件。
   * 使用 `java.io.FileInputStream` 其建構函式建立物件，並將PDF檔案的位置傳遞至反匯編。
   * 建立物 `com.adobe.idp.Document` 件並將包含PDF `java.io.FileInputStream` 檔案的物件傳遞至反匯編。
   * 通過調用對象的方 `java.util.Map` 法並傳遞以 `put` 下參數，向對象添加條目：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
      * 包含 `com.adobe.idp.Document` 要反匯編的PDF文檔的對象。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 調用屬於該對象的方法，以設定運行時選項以滿足您的業務 `AssemblerOptionSpec` 要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用 `AssemblerOptionSpec` 物件的方 `setFailOnError` 法並傳遞 `false`。

1. 反匯編PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列必要值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文檔的對象
   * 包含 `java.util.Map` 要反匯編的PDF文檔的對象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 運行時選項（包括預設字型和作業日誌級別）的對象
   此方 `invokeDDX` 法會傳回包 `com.adobe.livecycle.assembler.client.AssemblerResult` 含已拆解PDF檔案的物件，以及發生的任何例外。

1. 儲存已拆解的PDF檔案。

   要獲取已拆解的PDF文檔，請執行以下操作：

   * 叫用 `AssemblerResult` 物件的方 `getDocuments` 法。 這會傳回 `java.util.Map` 物件。
   * 重複該對 `java.util.Map` 像，直到找到結果對 `com.adobe.idp.Document` 像。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法以擷取PDF檔案。

**另請參閱**

[以程式設計方式解譯PDF檔案](#programmatically-disassembling-pdf-documents)

[快速入門（SOAP模式）:使用Java API解譯PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API解譯PDF檔案 {#disassemble-a-pdf-document-using-the-web-service-api}

使用Assembler Service API(web service)拆解PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

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
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，該值代表DDX檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 參考要反匯編的PDF文檔。

   * 使用其 `BLOB` 建構函式建立物件。 物件 `BLOB` 用來儲存輸入的PDF檔案。 此 `BLOB` 對象作為引數 `invokeOneDocument` 傳遞給。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 對象的欄位分 `MTOM` 配位元組陣列的內容來填充對象。
   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 此收集物件用來儲存要反匯編的PDF。
   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType_Item` 像。
   * 為物件欄位指派代表索引鍵名稱 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字串 `key` 值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
   * 將儲 `BLOB` 存PDF檔案的物件指派至物 `MyMapOf_xsd_string_To_xsd_anyType_Item` 件的欄 `value` 位。
   * 將對象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 添加到對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 調用對 `MyMapOf_xsd_string_To_xsd_anyType` 像的方 `Add` 法並傳遞對 `MyMapOf_xsd_string_To_xsd_anyType` 像。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 通過為屬於該對象的資料成員分配值，設定運行時選項以滿足您的業務需 `AssemblerOptionSpec` 求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請指 `false` 派給 `AssemblerOptionSpec` 物件的欄 `failOnError` 位。

1. 反匯編PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列值：

   * 代 `BLOB` 表DDX文檔的對象，該PDF文檔會拆分
   * 包含 `MyMapOf_xsd_string_To_xsd_anyType` 要反匯編的PDF文檔的對象
   * 指定 `AssemblerOptionSpec` 運行時選項的對象
   該方 `invokeDDX` 法返回一個對 `AssemblerResult` 像，該對象包含作業結果和所發生的任何異常。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取物 `AssemblerResult` 件的欄 `documents` 位，此欄位是包含 `Map` 已拆解PDF檔案的物件。
   * 重複該對 `Map` 像，以獲得每個結果文檔。 然後，將該陣列成員轉 `value` 換為 `BLOB`。
   * 存取PDF檔案的物件屬性，以擷取代表PDF文 `BLOB` 件的二進位 `MTOM` 資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[以程式設計方式解譯PDF檔案](#programmatically-disassembling-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
