---
title: 動態建立DDX文檔
seo-title: Dynamically Creating DDX Documents
description: 使用Java API和網站服務API以動態方式建立DDX檔案。 動態建立DDX文檔使您能夠使用在運行時獲取的DDX文檔中的值。
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# 動態建立DDX文檔 {#dynamically-creating-ddx-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以動態建立DDX文檔，該文檔可用於執行組合器操作。 動態建立DDX文檔使您能夠使用在運行時獲取的DDX文檔中的值。 要動態建立DDX文檔，請使用屬於您所使用的寫程式語言的類。 例如，如果您使用Java開發客戶端應用程式，請使用屬於 `org.w3c.dom.*`包。 同樣地，如果您使用Microsoft .NET，請使用屬於 `System.Xml` 命名空間。

在將DDX文檔傳遞到組合器服務之前，請將XML從 `org.w3c.dom.Document` 例項 `com.adobe.idp.Document` 例項。 如果您使用Web服務，請從用於建立XML的資料類型中轉換XML(例如， `XmlDocument`) `BLOB` 例項。

對於此討論，假設動態建立了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX文檔拆分PDF文檔。 建議您熟悉拆解PDF文檔。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

要使用動態建立的DDX文檔來拆解PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 建立DDX文檔。
1. 轉換DDX文檔。
1. 設定運行時選項。
1. 拆解PDF文檔。
1. 保存已拆解的PDF文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，請建立組合器服務客戶端。

**建立DDX文檔**

使用您使用的寫程式語言建立DDX文檔。 要建立分解PDF文檔的DDX文檔，請確保它包含 `PDFsFromBookmarks` 元素。 將用於建立DDX文檔的資料類型轉換為 `com.adobe.idp.Document` 例項。 如果您使用網站服務，請將資料類型轉換為 `BLOB` 例項。

**轉換DDX文檔**

使用 `org.w3c.dom` 類別必須轉換為 `com.adobe.idp.Document` 物件。 要在使用Java API時執行此任務，請使用Java XML轉換類。 如果您使用Web服務，請將DDX文檔轉換為 `BLOB` 物件。

**參考要拆解的PDF文檔**

要拆解PDF文檔，請參考表示要拆解的PDF文檔的PDF檔案。 當傳遞到組合器服務時，將為文檔中的每個級別1書籤返回一個單獨的PDF文檔。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。 若要設定執行時選項，請使用 `AssemblerOptionSpec` 物件。

**拆解PDF文檔**

通過調用 `invokeDDX` 操作。 傳遞動態建立的DDX檔案。 組合器服務返回集合對象中已拆解的PDF文檔。

**保存已拆解的PDF文檔**

所有已拆解的PDF文檔都返回在收集對象中。 逐一查看集合物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用Web服務API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式分解PDF文檔](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API動態建立DDX檔案 {#dynamically-create-a-ddx-document-using-the-java-api}

使用組合器服務API(Java)動態建立DDX文檔和拆解PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 建立DDX文檔。

   * 建立Java `DocumentBuilderFactory` 物件，方法是呼叫 `DocumentBuilderFactory` class `newInstance` 方法。
   * 建立Java `DocumentBuilder` 物件，方法是呼叫 `DocumentBuilderFactory` 物件 `newDocumentBuilder` 方法。
   * 呼叫 `DocumentBuilder` 物件 `newDocument` 實例化方法 `org.w3c.dom.Document` 物件。
   * 叫用 `org.w3c.dom.Document` 物件 `createElement` 方法。 此方法會建立 `Element` 代表根元素的物件。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，呼叫子元素，以設定子元素的值 `setAttribute` 方法。 最後，呼叫標頭元素的 `appendChild` 方法，並將子元素物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 建立 `PDFsFromBookmarks` 元素 `Document` 物件 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 為 `PDFsFromBookmarks` 元素 `setAttribute` 方法。 附加 `PDFsFromBookmarks` 元素 `DDX` 元素，方法是呼叫 `appendChild` 方法。 傳遞 `PDFsFromBookmarks` 元素物件作為引數。 下列幾行程式碼會顯示此應用程式邏輯：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 建立 `PDF` 元素 `Document` 物件 `createElement` 方法。 傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 為 `PDF` 元素 `setAttribute` 方法。 附加 `PDF` 元素 `PDFsFromBookmarks` 元素 `PDFsFromBookmarks` 元素 `appendChild` 方法。 傳遞 `PDF` 元素物件作為引數。 以下幾行代碼顯示此應用程式邏輯：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 轉換DDX文檔。

   * 建立 `javax.xml.transform.Transformer` 對象，方法是調用 `javax.xml.transform.Transformer` 對象的靜態 `newInstance` 方法。
   * 建立 `Transformer` 對象，方法是調用 `TransformerFactory` 物件 `newTransformer` 方法。
   * 建立 `ByteArrayOutputStream` 物件，使用其建構子。
   * 建立 `javax.xml.transform.dom.DOMSource` 物件，使用其建構子。 傳遞 `org.w3c.dom.Document` 表示DDX文檔的對象。
   * 建立 `javax.xml.transform.dom.DOMSource` 對象，使用其建構子並傳遞 `ByteArrayOutputStream` 物件。
   * 填入Java `ByteArrayOutputStream` 對象，方法是調用 `javax.xml.transform.Transformer` 物件 `transform` 方法。 傳遞 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 對象。
   * 建立位元組陣列，並分配 `ByteArrayOutputStream` 位元組陣列的物件。
   * 叫用 `ByteArrayOutputStream` 物件 `toByteArray` 方法。
   * 建立 `com.adobe.idp.Document` 物件，方法是使用其建構子並傳遞位元組陣列。

1. 參考要拆卸的PDF文檔。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象，方法是使用 `HashMap` 建構子。
   * 建立 `java.io.FileInputStream` 對象，使用其建構子，並將PDF文檔的位置傳遞到反匯編。
   * 建立 `com.adobe.idp.Document` 物件。 傳遞 `java.io.FileInputStream` 包含要拆解的PDF文檔的對象。
   * 將項目新增至 `java.util.Map` 對象 `put` 方法，並傳遞下列引數：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 (在動態建立的DDX檔案中，值為 `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` 包含要拆解的PDF文檔的對象。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 通過調用屬於的方法來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 物件 `setFailOnError` 方法和傳遞 `false`.

1. 拆解PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 表示動態建立的DDX文檔的對象
   * A `java.util.Map` 包含要拆解的PDF文檔的對象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象，包括預設字型和作業日誌級別

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已拆解的PDF文檔和發生的任何例外的對象。

1. 保存已拆解的PDF文檔。

   要獲取已拆解的PDF文檔，請執行以下操作：

   * 叫用 `AssemblerResult` 物件 `getDocuments` 方法。 此方法會傳回 `java.util.Map` 物件。
   * 重複 `java.util.Map` 對象，直到找到結果 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取PDF檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API動態建立DDX檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API動態建立DDX檔案 {#dynamically-create-a-ddx-document-using-the-web-service-api}

使用組合器服務API（Web服務）動態建立DDX文檔並拆解PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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

1. 建立DDX文檔。

   * 建立 `System.Xml.XmlElement` 物件，使用其建構子。
   * 叫用 `XmlElement` 物件 `CreateElement` 方法。 此方法會建立 `Element` 代表根元素的物件。 將代表元素名稱的字串值傳遞至 `CreateElement` 方法。 呼叫DDX元素，以設定其值 `SetAttribute` 方法。 最後，呼叫 `XmlElement` 物件 `AppendChild` 方法。 將DDX物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 建立DDX文檔的 `PDFsFromBookmarks` 元素 `XmlElement` 物件 `CreateElement` 方法。 將代表元素名稱的字串值傳遞至 `CreateElement` 方法。 接下來，呼叫元素的 `SetAttribute` 方法。 附加 `PDFsFromBookmarks` 元素，借由呼叫 `DDX` 元素 `AppendChild` 方法。 傳遞 `PDFsFromBookmarks` 元素物件作為引數。 下列幾行程式碼會顯示此應用程式邏輯：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 建立DDX文檔的 `PDF` 元素 `XmlElement` 物件 `CreateElement` 方法。 將代表元素名稱的字串值傳遞至 `CreateElement` 方法。 接下來，呼叫子元素，以設定子元素的值 `SetAttribute` 方法。 附加 `PDF` 元素 `PDFsFromBookmarks` 元素 `PDFsFromBookmarks` 元素 `AppendChild` 方法。 傳遞 `PDF` 元素物件作為引數。 以下幾行代碼顯示此應用程式邏輯：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 轉換DDX文檔。

   * 建立 `System.IO.MemoryStream` 物件，使用其建構子。
   * 填入 `MemoryStream` 對象，使用 `XmlElement` 表示DDX文檔的對象。 叫用 `XmlElement` 物件 `Save` 方法並傳遞 `MemoryStream` 物件。
   * 建立位元組陣列，並在 `MemoryStream` 物件。 下列程式碼會顯示此應用程式邏輯：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 建立 `BLOB` 物件。 將位元組陣列指派給 `BLOB` 物件 `MTOM` 欄位。

1. 參考要拆卸的PDF文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存輸入PDF文檔。 此 `BLOB` 物件會傳遞至 `invokeOneDocument` 作為引數。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性位元組陣列的內容。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 為屬於的資料成員指定值，以設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 物件 `failOnError` 資料成員。

1. 拆解PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列值：

   * A `BLOB` 表示動態建立的DDX文檔的對象
   * 此 `mapItem` 包含輸入PDF文檔的陣列
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含作業結果的對象以及發生的任何例外。

1. 保存已拆解的PDF文檔。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 存取 `AssemblerResult` 物件 `documents` 欄位，即 `Map` 包含已拆解PDF文檔的對象。
   * 重複 `Map` 對象，以獲得每個生成的文檔。 然後，將陣列成員的 `value` 到 `BLOB`.
   * 通過訪問PDF文檔來提取代表文檔的二進位資料 `BLOB` 物件 `MTOM` 屬性。 這會傳回一個位元組陣列，您可將其寫出至PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
