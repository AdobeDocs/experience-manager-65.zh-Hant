---
title: 動態建立DDX檔案
seo-title: 動態建立DDX檔案
description: 'null'
seo-description: 'null'
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 動態建立DDX檔案 {#dynamically-creating-ddx-documents}

您可以動態建立DDX文檔，該文檔可用於執行Assembler操作。 動態建立DDX檔案可讓您在執行時期取得的DDX檔案中使用值。 若要動態建立DDX檔案，請使用屬於您所使用之程式設計語言的類別。 例如，如果您使用Java開發用戶端應用程式，請使用屬於套件的 `org.w3c.dom.*`類別。 同樣地，如果您使用Microsoft .NET，請使用屬於命名空間的 `System.Xml` 類。

在將DDX文檔傳遞至Assembler服務之前，請將XML從實例 `org.w3c.dom.Document` 轉換為實 `com.adobe.idp.Document` 例。 如果您使用web services，請將XML從用來建立XML(例如 `XmlDocument`)的資料類型轉換為例 `BLOB` 項。

在此討論中，假設以下DDX文檔是動態建立的。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX檔案會拆解PDF檔案。 建議您熟悉解譯PDF檔案。

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參 [閱Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

若要使用動態建立的DDX檔案來拆解PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 建立DDX檔案。
1. 轉換DDX檔案。
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

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，請建立匯編器服務客戶端。

**建立DDX檔案**

使用您使用的程式設計語言建立DDX檔案。 若要建立會拆解PDF檔案的DDX檔案，請確定檔案包含元 `PDFsFromBookmarks` 素。 如果您使用Java API，請將用於建立DDX文 `com.adobe.idp.Document` 件的資料類型轉換為例項。 如果您使用web services，請將資料類型轉換為例 `BLOB` 項。

**轉換DDX檔案**

使用類建立的DDX文 `org.w3c.dom` 檔必須轉換為對 `com.adobe.idp.Document` 像。 要在使用Java API時執行此任務，請使用Java XML轉換類。 如果您使用web services，請將DDX檔案轉換為物 `BLOB` 件。

**參考PDF檔案以反匯編**

要反匯編PDF文檔，請參考表示要反匯編的PDF文檔的PDF檔案。 傳遞至Assembler服務時，會針對檔案中的每個第1級書籤傳回個別的PDF檔案。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。 要設定運行時選項，請使用對 `AssemblerOptionSpec` 像。

**反匯編PDF檔案**

調用操作，可反匯編PDF `invokeDDX` 文檔。 傳遞動態建立的DDX檔案。 Assembler服務會在收集物件中傳回已拆解的PDF檔案。

**儲存已拆解的PDF檔案**

所有已拆解的PDF檔案都會傳回至系列物件中。 逐步處理系列物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用web service API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式解譯PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API動態建立DDX檔案 {#dynamically-create-a-ddx-document-using-the-java-api}

使用Assembler Service API(Java)動態建立DDX檔案並反匯編PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `AssemblerServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 建立DDX檔案。

   * 通過調用類 `DocumentBuilderFactory` 的方法建立Java `DocumentBuilderFactory` 對 `newInstance` 像。
   * 呼叫物件 `DocumentBuilder` 的方法，以建 `DocumentBuilderFactory` 立Java物 `newDocumentBuilder` 件。
   * 呼叫物 `DocumentBuilder` 件的方 `newDocument` 法以實例化 `org.w3c.dom.Document` 物件。
   * 叫用物件的方法，以建立DDX文 `org.w3c.dom.Document` 件的根元 `createElement` 素。 此方法會建立 `Element` 代表根元素的物件。 將表示元素名稱的字串值傳遞至方 `createElement` 法。 將返回值轉換為 `Element`。 接著，呼叫子元素的方法，以設定子元素的 `setAttribute` 值。 最後，呼叫標題元素的方法，將元素附加至標題元素， `appendChild` 並將子項元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 呼叫 `PDFsFromBookmarks` 物件的方 `Document` 法以建立元 `createElement` 素。 將表示元素名稱的字串值傳遞至方 `createElement` 法。 將返回值轉換為 `Element`。 呼叫元素的方 `PDFsFromBookmarks` 法，以設定元素 `setAttribute` 值。 呼叫 `PDFsFromBookmarks` DDX元素的 `DDX` 方法，將元素附加至元 `appendChild` 素。 將元素 `PDFsFromBookmarks` 物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 呼叫 `PDF` 物件的方 `Document` 法以建立元 `createElement` 素。 傳遞代表元素名稱的字串值。 將返回值轉換為 `Element`。 呼叫元素的方 `PDF` 法，以設定元素 `setAttribute` 值。 呼叫 `PDF` 元素的方 `PDFsFromBookmarks` 法，將元素 `PDFsFromBookmarks` 附加至元 `appendChild` 素。 將元素 `PDF` 物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 轉換DDX檔案。

   * 調用 `javax.xml.transform.Transformer` 物件的靜態方 `javax.xml.transform.Transformer` 法來建立物 `newInstance` 件。
   * 調用 `Transformer` 物件的方 `TransformerFactory` 法以建立物 `newTransformer` 件。
   * 使用其 `ByteArrayOutputStream` 建構函式建立物件。
   * 使用其 `javax.xml.transform.dom.DOMSource` 建構函式建立物件。 傳遞 `org.w3c.dom.Document` 代表DDX檔案的物件。
   * 使用其 `javax.xml.transform.dom.DOMSource` 建構函式並傳遞物件，以建立物 `ByteArrayOutputStream` 件。
   * 調用物件 `ByteArrayOutputStream` 的方法，以填 `javax.xml.transform.Transformer` 入Java物 `transform` 件。 傳遞 `javax.xml.transform.dom.DOMSource` 和物 `javax.xml.transform.stream.StreamResult` 件。
   * 建立位元組陣列並將對象的大 `ByteArrayOutputStream` 小分配給位元組陣列。
   * 調用物件的方法，以填 `ByteArrayOutputStream` 入位元組 `toByteArray` 陣列。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞位元組陣列，以建立物件。

1. 參考要反匯編的PDF文檔。

   * 使用 `java.util.Map` 建構函式建立用來儲存輸入PDF檔案的物 `HashMap` 件。
   * 使用 `java.io.FileInputStream` 其建構函式建立物件，並將PDF檔案的位置傳遞至反匯編。
   * 建立對 `com.adobe.idp.Document` 像。 將包含 `java.io.FileInputStream` PDF檔案的物件傳遞至反匯編。
   * 通過調用對象的方 `java.util.Map` 法並傳遞以 `put` 下參數，向對象添加條目：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。 (在動態建立的DDX檔案中，值是 `AssemblerResultPDF.pdf`。)
      * 包含 `com.adobe.idp.Document` 要反匯編的PDF文檔的對象。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 調用屬於該對象的方法，以設定運行時選項以滿足您的業務 `AssemblerOptionSpec` 要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用 `AssemblerOptionSpec` 物件的方 `setFailOnError` 法並傳遞 `false`。

1. 反匯編PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列值：

   * 代表 `com.adobe.idp.Document` 動態建立的DDX檔案的物件
   * 包含 `java.util.Map` 要反匯編的PDF文檔的對象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 運行時選項（包括預設字型和作業日誌級別）的對象
   此方 `invokeDDX` 法會傳回包 `com.adobe.livecycle.assembler.client.AssemblerResult` 含已拆解PDF檔案的物件，以及發生的任何例外。

1. 儲存已拆解的PDF檔案。

   要獲取已拆解的PDF文檔，請執行以下操作：

   * 叫用 `AssemblerResult` 物件的方 `getDocuments` 法。 此方法返回對 `java.util.Map` 像。
   * 重複該對 `java.util.Map` 像，直到找到結果對 `com.adobe.idp.Document` 像。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法以擷取PDF檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API動態建立DDX檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API動態建立DDX檔案 {#dynamically-create-a-ddx-document-using-the-web-service-api}

使用Assembler Service API(web service)動態建立DDX檔案並反匯編PDF檔案：

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

1. 建立DDX檔案。

   * 使用其 `System.Xml.XmlElement` 建構函式建立物件。
   * 叫用物件的方法，以建立DDX文 `XmlElement` 件的根元 `CreateElement` 素。 此方法會建立 `Element` 代表根元素的物件。 將表示元素名稱的字串值傳遞至方 `CreateElement` 法。 呼叫DDX元素的方法，以設定其 `SetAttribute` 值。 最後，呼叫物件的方法，將元素附 `XmlElement` 加至DDX文 `AppendChild` 件。 將DDX物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 呼叫物件的方 `PDFsFromBookmarks` 法，以建立DDX `XmlElement` 檔案的元 `CreateElement` 素。 將表示元素名稱的字串值傳遞至方 `CreateElement` 法。 接著，呼叫元素的方法，以設定元素的 `SetAttribute` 值。 呼叫 `PDFsFromBookmarks` 元素的方法，將元素附 `DDX` 加至根元 `AppendChild` 素。 將元素 `PDFsFromBookmarks` 物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 呼叫物件的方 `PDF` 法，以建立DDX `XmlElement` 檔案的元 `CreateElement` 素。 將表示元素名稱的字串值傳遞至方 `CreateElement` 法。 接著，呼叫子元素的方法，以設定子元素的 `SetAttribute` 值。 呼叫 `PDF` 元素的方 `PDFsFromBookmarks` 法，將元素 `PDFsFromBookmarks` 附加至元 `AppendChild` 素。 將元素 `PDF` 物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 轉換DDX檔案。

   * 使用其 `System.IO.MemoryStream` 建構函式建立物件。
   * 使用 `MemoryStream` 代表DDX文檔的對象，將 `XmlElement` 對象填入DDX文檔。 叫用物 `XmlElement` 件的方 `Save` 法並傳遞物 `MemoryStream` 件。
   * 建立位元組陣列，並將位於物件中的資料填入該 `MemoryStream` 陣列。 下列程式碼顯示此應用程式邏輯：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 建立對 `BLOB` 像。 將位元組陣列指派 `BLOB` 至物件的欄 `MTOM` 位。

1. 參考要反匯編的PDF文檔。

   * 使用其 `BLOB` 建構函式建立物件。 物件 `BLOB` 用來儲存輸入的PDF檔案。 此 `BLOB` 對象作為引數 `invokeOneDocument` 傳遞給。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表輸入PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 對象的屬性指 `MTOM` 定位元組陣列的內容來填充對象。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 通過為屬於該對象的資料成員分配值，設定運行時選項以滿足您的業務需 `AssemblerOptionSpec` 求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請指 `false` 派給 `AssemblerOptionSpec` 物件的資料 `failOnError` 成員。

1. 反匯編PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列值：

   * 代表 `BLOB` 動態建立的DDX檔案的物件
   * 包含 `mapItem` 輸入PDF檔案的陣列
   * 指定 `AssemblerOptionSpec` 運行時選項的對象
   該方 `invokeDDX` 法返回 `AssemblerResult` 一個對象，該對象包含作業結果和所發生的任何異常。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取物 `AssemblerResult` 件的欄 `documents` 位，此欄位是包含 `Map` 已拆解PDF檔案的物件。
   * 重複該對 `Map` 像，以獲得每個結果文檔。 然後，將該陣列成員轉 `value` 換為 `BLOB`。
   * 存取PDF檔案的物件屬性，以擷取代表PDF文 `BLOB` 件的二進位 `MTOM` 資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
