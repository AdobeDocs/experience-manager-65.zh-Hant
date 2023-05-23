---
title: 動態建立DDX文檔
seo-title: Dynamically Creating DDX Documents
description: 使用Java API和Web服務API動態建立DDX文檔。 動態建立DDX文檔使您能夠在DDX文檔中使用在運行時獲得的值。
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

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

可以動態建立可用於執行匯編器操作的DDX文檔。 動態建立DDX文檔使您能夠在DDX文檔中使用在運行時獲得的值。 要動態建立DDX文檔，請使用屬於您所使用的寫程式語言的類。 例如，如果您使用Java開發客戶端應用程式，則使用屬於 `org.w3c.dom.*`檔案。 同樣，如果您使用的是Microsoft.NET，則使用屬於 `System.Xml` 命名空間。

在將DDX文檔傳遞到匯編器服務之前，請將XML從 `org.w3c.dom.Document` 實例 `com.adobe.idp.Document` 實例。 如果使用Web服務，請從用於建立XML的資料類型轉換XML(例如， `XmlDocument`) `BLOB` 實例。

對於此討論，假定動態建立了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX文檔拆分PDF文檔。 建議您熟悉拆卸PDF文檔。

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要使用動態建立的DDX文檔拆解PDF文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立PDF匯編器客戶端。
1. 建立DDX文檔。
1. 轉換DDX文檔。
1. 設定運行時選項。
1. 分解PDF文檔。
1. 保存已拆卸的PDF文檔。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

**建立PDF匯編器客戶端**

在以寫程式方式執行匯編器操作之前，請建立匯編器服務客戶端。

**建立DDX文檔**

使用您正在使用的寫程式語言建立DDX文檔。 要建立拆分PDF文檔的DDX文檔，請確保它包含 `PDFsFromBookmarks` 的子菜單。 將用於建立DDX文檔的資料類型轉換為 `com.adobe.idp.Document` 實例。 如果使用Web服務，請將資料類型轉換為 `BLOB` 實例。

**轉換DDX文檔**

使用 `org.w3c.dom` 類必須轉換為 `com.adobe.idp.Document` 的雙曲餘切值。 要使用Java API時執行此任務，請使用Java XML轉換類。 如果使用Web服務，請將DDX文檔轉換為 `BLOB` 的雙曲餘切值。

**引用要拆卸的PDF文檔**

要拆卸PDF文檔，請參照表示要拆卸的PDF文檔的PDF檔案。 傳遞到匯編程式服務時，將為文檔中的每個1級書籤返回單獨的PDF文檔。

**設定運行時選項**

您可以設定運行時選項，這些選項在匯編程式服務執行作業時控制其行為。 例如，您可以設定一個選項，指示匯編程式服務在遇到錯誤時繼續處理作業。 要設定運行時選項，請使用 `AssemblerOptionSpec` 的雙曲餘切值。

**分解PDF文檔**

通過調用PDF文檔 `invokeDDX` 的下界。 傳遞動態建立的DDX文檔。 匯編器服務返回集合對象內的已拆卸PDF文檔。

**保存已拆卸的PDF文檔**

所有已拆卸的PDF文檔都在收集對象中返回。 循環訪問集合對象並將每個PDF文檔另存為PDF檔案。

**另請參閱**

[使用Java API動態建立DDX文檔](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用Web服務API動態建立DDX文檔](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式分解PDF文檔](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API動態建立DDX文檔 {#dynamically-create-a-ddx-document-using-the-java-api}

使用匯編器服務API(Java)動態建立DDX文檔並拆解PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 建立DDX文檔。

   * 建立Java `DocumentBuilderFactory` 通過調用 `DocumentBuilderFactory` 類 `newInstance` 的雙曲餘切值。
   * 建立Java `DocumentBuilder` 通過調用 `DocumentBuilderFactory` 對象 `newDocumentBuilder` 的雙曲餘切值。
   * 呼叫 `DocumentBuilder` 對象 `newDocument` 實例化方法 `org.w3c.dom.Document` 的雙曲餘切值。
   * 通過調用 `org.w3c.dom.Document` 對象 `createElement` 的雙曲餘切值。 此方法建立 `Element` 表示根元素的對象。 將表示元素名稱的字串值傳遞到 `createElement` 的雙曲餘切值。 將返回值強制轉換為 `Element`。 接下來，通過調用子元素的值來設定其值 `setAttribute` 的雙曲餘切值。 最後，通過調用標題元素的 `appendChild` 方法，並將子元素對象作為參數傳遞。 以下代碼行顯示此應用程式邏輯：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 建立 `PDFsFromBookmarks` 通過調用 `Document` 對象 `createElement` 的雙曲餘切值。 將表示元素名稱的字串值傳遞到 `createElement` 的雙曲餘切值。 將返回值強制轉換為 `Element`。 為 `PDFsFromBookmarks` 調用元素 `setAttribute` 的雙曲餘切值。 追加 `PDFsFromBookmarks` 元素 `DDX` 調用DDX元素 `appendChild` 的雙曲餘切值。 通過 `PDFsFromBookmarks` 元素對象作為參數。 以下代碼行顯示此應用程式邏輯：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 建立 `PDF` 通過調用 `Document` 對象 `createElement` 的雙曲餘切值。 傳遞表示元素名稱的字串值。 將返回值強制轉換為 `Element`。 為 `PDF` 調用元素 `setAttribute` 的雙曲餘切值。 追加 `PDF` 元素 `PDFsFromBookmarks` 通過調用 `PDFsFromBookmarks` 元素 `appendChild` 的雙曲餘切值。 通過 `PDF` 元素對象作為參數。 以下代碼行顯示此應用程式邏輯：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 轉換DDX文檔。

   * 建立 `javax.xml.transform.Transformer` 通過調用 `javax.xml.transform.Transformer` 對象的靜態 `newInstance` 的雙曲餘切值。
   * 建立 `Transformer` 通過調用 `TransformerFactory` 對象 `newTransformer` 的雙曲餘切值。
   * 建立 `ByteArrayOutputStream` 對象。
   * 建立 `javax.xml.transform.dom.DOMSource` 對象。 通過 `org.w3c.dom.Document` 表示DDX文檔的對象。
   * 建立 `javax.xml.transform.dom.DOMSource` 使用其建構子並傳遞對象 `ByteArrayOutputStream` 的雙曲餘切值。
   * 填充Java `ByteArrayOutputStream` 通過調用 `javax.xml.transform.Transformer` 對象 `transform` 的雙曲餘切值。 通過 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 對象。
   * 建立位元組陣列並分配 `ByteArrayOutputStream` 對象。
   * 通過調用 `ByteArrayOutputStream` 對象 `toByteArray` 的雙曲餘切值。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞位元組陣列。

1. 參照要拆卸的PDF文檔。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象 `HashMap` 建構子。
   * 建立 `java.io.FileInputStream` 對象，使用其建構子，並將PDF文檔的位置傳遞到反匯編。
   * 建立 `com.adobe.idp.Document` 的雙曲餘切值。 通過 `java.io.FileInputStream` 包含要拆卸的PDF文檔的對象。
   * 向 `java.util.Map` 通過調用對象 `put` 方法並傳遞以下參數：

      * 表示鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 (在動態建立的DDX文檔中，值為 `AssemblerResultPDF.pdf`。)
      * A `com.adobe.idp.Document` 包含要拆卸的PDF文檔的對象。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過調用屬於的方法來設定運行時選項以滿足業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 對象 `setFailOnError` 方法 `false`。

1. 分解PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示動態建立的DDX文檔的對象
   * A `java.util.Map` 包含要拆卸的PDF文檔的對象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象，包括預設字型和作業日誌級別

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已拆卸的PDF文檔和發生的任何異常的對象。

1. 保存已拆卸的PDF文檔。

   要獲取已拆卸的PDF文檔，請執行以下操作：

   * 調用 `AssemblerResult` 對象 `getDocuments` 的雙曲餘切值。 此方法返回 `java.util.Map` 的雙曲餘切值。
   * 迭代 `java.util.Map` 直到找到結果 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取PDF文檔。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API動態建立DDX文檔](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API動態建立DDX文檔 {#dynamically-create-a-ddx-document-using-the-web-service-api}

使用匯編器服務API（Web服務）動態建立DDX文檔並拆解PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 請確保在設定服務引用時使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

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

1. 建立DDX文檔。

   * 建立 `System.Xml.XmlElement` 對象。
   * 通過調用 `XmlElement` 對象 `CreateElement` 的雙曲餘切值。 此方法建立 `Element` 表示根元素的對象。 將表示元素名稱的字串值傳遞到 `CreateElement` 的雙曲餘切值。 通過調用DDX元素的值 `SetAttribute` 的雙曲餘切值。 最後，通過調用 `XmlElement` 對象 `AppendChild` 的雙曲餘切值。 將DDX對象作為參數傳遞。 以下代碼行顯示此應用程式邏輯：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 建立DDX文檔 `PDFsFromBookmarks` 通過調用 `XmlElement` 對象 `CreateElement` 的雙曲餘切值。 將表示元素名稱的字串值傳遞到 `CreateElement` 的雙曲餘切值。 接下來，通過調用元素的值 `SetAttribute` 的雙曲餘切值。 追加 `PDFsFromBookmarks` 調用 `DDX` 元素 `AppendChild` 的雙曲餘切值。 通過 `PDFsFromBookmarks` 元素對象作為參數。 以下代碼行顯示此應用程式邏輯：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 建立DDX文檔 `PDF` 通過調用 `XmlElement` 對象 `CreateElement` 的雙曲餘切值。 將表示元素名稱的字串值傳遞到 `CreateElement` 的雙曲餘切值。 接下來，通過調用子元素的值來設定其值 `SetAttribute` 的雙曲餘切值。 追加 `PDF` 元素 `PDFsFromBookmarks` 通過調用 `PDFsFromBookmarks` 元素 `AppendChild` 的雙曲餘切值。 通過 `PDF` 元素對象作為參數。 以下代碼行顯示此應用程式邏輯：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 轉換DDX文檔。

   * 建立 `System.IO.MemoryStream` 對象。
   * 填充 `MemoryStream` DDX文檔中的對象 `XmlElement` 表示DDX文檔的對象。 調用 `XmlElement` 對象 `Save` 方法和通過 `MemoryStream` 的雙曲餘切值。
   * 建立位元組陣列，並使用位於 `MemoryStream` 的雙曲餘切值。 以下代碼顯示此應用程式邏輯：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 建立 `BLOB` 的雙曲餘切值。 將位元組陣列分配給 `BLOB` 對象 `MTOM` 的子菜單。

1. 參照要拆卸的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存輸入PDF文檔。 此 `BLOB` 對象被傳遞到 `invokeOneDocument` 作為論據。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性位元組陣列的內容。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過將值分配給屬於的資料成員來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編程式服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 對象 `failOnError` 資料成員。

1. 分解PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `BLOB` 表示動態建立的DDX文檔的對象
   * 的 `mapItem` 包含輸入PDF文檔的陣列
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作業結果和所發生的任何異常的對象。

1. 保存已拆卸的PDF文檔。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問 `AssemblerResult` 對象 `documents` 欄位， `Map` 包含已拆卸的PDF文檔的對象。
   * 迭代 `Map` 對象，以獲取每個結果文檔。 然後，將該陣列成員 `value` 到 `BLOB`。
   * 通過訪問PDF文檔來提取表示該文檔的二進位資料 `BLOB` 對象 `MTOM` 屬性。 這將返回可以寫入PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
