---
title: 動態建立DDX文檔
seo-title: 動態建立DDX文檔
description: 使用Java API和網站服務API以動態方式建立DDX檔案。 動態建立DDX文檔使您能夠使用在運行時獲取的DDX文檔中的值。
seo-description: 使用Java API和網站服務API以動態方式建立DDX檔案。 動態建立DDX文檔使您能夠使用在運行時獲取的DDX文檔中的值。
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
source-wordcount: '2199'
ht-degree: 0%

---

# 動態建立DDX文檔{#dynamically-creating-ddx-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以動態建立DDX文檔，該文檔可用於執行組合器操作。 動態建立DDX文檔使您能夠使用在運行時獲取的DDX文檔中的值。 要動態建立DDX文檔，請使用屬於您所使用的寫程式語言的類。 例如，如果您使用Java開發客戶端應用程式，請使用屬於`org.w3c.dom.*`包的類。 同樣，如果使用Microsoft .NET，請使用屬於`System.Xml`命名空間的類。

在將DDX文檔傳遞到組合器服務之前，請將XML從`org.w3c.dom.Document`實例轉換為`com.adobe.idp.Document`實例。 如果您使用Web服務，請將XML從用於建立XML的資料類型（例如`XmlDocument`）轉換為`BLOB`實例。

對於此討論，假設動態建立了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX文檔將PDF文檔拆分。 建議您先熟悉PDF檔案的解體。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}的摘要

要使用動態建立的DDX文檔來拆解PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 建立DDX文檔。
1. 轉換DDX文檔。
1. 設定運行時選項。
1. 反匯編PDF文檔。
1. 儲存已拆解的PDF檔案。

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

使用您使用的寫程式語言建立DDX文檔。 要建立分解PDF文檔的DDX文檔，請確保它包含`PDFsFromBookmarks`元素。 如果您使用Java API，請將用於建立DDX文檔的資料類型轉換為`com.adobe.idp.Document`實例。 如果您使用Web服務，請將資料類型轉換為`BLOB`實例。

**轉換DDX文檔**

使用`org.w3c.dom`類建立的DDX文檔必須轉換為`com.adobe.idp.Document`對象。 要在使用Java API時執行此任務，請使用Java XML轉換類。 如果您使用Web服務，請將DDX文檔轉換為`BLOB`對象。

**參考要拆卸的PDF文檔**

要拆解PDF文檔，請參照表示要拆解的PDF文檔的PDF檔案。 當傳遞到組合器服務時，將為文檔中的每個級別1書籤返回一個單獨的PDF文檔。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。 要設定運行時選項，請使用`AssemblerOptionSpec`對象。

**反匯編PDF文檔**

叫用`invokeDDX`操作，拆解PDF文檔。 傳遞動態建立的DDX檔案。 組合器服務返回集合對象內已拆解的PDF文檔。

**儲存已拆解的PDF檔案**

所有已拆解的PDF文檔都在收集對象中返回。 逐一查看集合物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用Web服務API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式解譯PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API {#dynamically-create-a-ddx-document-using-the-java-api}動態建立DDX文檔

使用組合器服務API(Java)動態建立DDX文檔和拆解PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 建立DDX文檔。

   * 通過調用`DocumentBuilderFactory`類`newInstance`方法建立Java `DocumentBuilderFactory`對象。
   * 通過調用`DocumentBuilderFactory`對象的`newDocumentBuilder`方法建立Java `DocumentBuilder`對象。
   * 呼叫`DocumentBuilder`物件的`newDocument`方法以實例化`org.w3c.dom.Document`物件。
   * 調用`org.w3c.dom.Document`對象的`createElement`方法，建立DDX文檔的根元素。 此方法會建立代表根元素的`Element`物件。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 接下來，通過調用其`setAttribute`方法來設定子元素的值。 最後，呼叫標頭元素的`appendChild`方法，將元素附加至標頭元素，並將子元素物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 呼叫`Document`物件的`createElement`方法，以建立`PDFsFromBookmarks`元素。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 呼叫`setAttribute`方法，以設定`PDFsFromBookmarks`元素的值。 呼叫DDX元素的`appendChild`方法，將`PDFsFromBookmarks`元素附加至`DDX`元素。 將`PDFsFromBookmarks`元素物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 呼叫`Document`物件的`createElement`方法，以建立`PDF`元素。 傳遞代表元素名稱的字串值。 將傳回值轉換為`Element`。 呼叫`setAttribute`方法，以設定`PDF`元素的值。 呼叫`PDFsFromBookmarks`元素的`appendChild`方法，將`PDF`元素附加至`PDFsFromBookmarks`元素。 將`PDF`元素物件作為引數傳遞。 以下幾行代碼顯示此應用程式邏輯：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 轉換DDX文檔。

   * 調用`javax.xml.transform.Transformer`對象的靜態`newInstance`方法，建立`javax.xml.transform.Transformer`對象。
   * 調用`TransformerFactory`對象的`newTransformer`方法，建立`Transformer`對象。
   * 使用其建構子建立`ByteArrayOutputStream`物件。
   * 使用其建構子建立`javax.xml.transform.dom.DOMSource`物件。 傳遞代表DDX文檔的`org.w3c.dom.Document`對象。
   * 使用其建構子並傳遞`ByteArrayOutputStream`物件，以建立`javax.xml.transform.dom.DOMSource`物件。
   * 叫用`javax.xml.transform.Transformer`物件的`transform`方法，填入Java `ByteArrayOutputStream`物件。 傳遞`javax.xml.transform.dom.DOMSource`和`javax.xml.transform.stream.StreamResult`物件。
   * 建立位元組陣列，並將`ByteArrayOutputStream`對象的大小分配給位元組陣列。
   * 叫用`ByteArrayOutputStream`物件的`toByteArray`方法，填入位元組陣列。
   * 使用其建構子並傳遞位元組陣列，建立`com.adobe.idp.Document`物件。

1. 參考要拆卸的PDF文檔。

   * 使用`HashMap`建構子建立用於儲存輸入PDF文檔的`java.util.Map`對象。
   * 使用其建構子並將PDF檔案的位置傳遞至反匯編，以建立`java.io.FileInputStream`物件。
   * 建立`com.adobe.idp.Document`物件。 將包含PDF文檔的`java.io.FileInputStream`對象傳遞至反匯編。
   * 調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象中：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 （在動態建立的DDX文檔中，值為`AssemblerResultPDF.pdf`。）
      * `com.adobe.idp.Document`物件，包含要拆解的PDF檔案。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法來設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用`AssemblerOptionSpec`對象的`setFailOnError`方法並傳遞`false`。

1. 反匯編PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * `com.adobe.idp.Document`對象，表示動態建立的DDX文檔
   * 包含要拆解的PDF文檔的`java.util.Map`對象
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別

   `invokeDDX`方法返回一個`com.adobe.livecycle.assembler.client.AssemblerResult`對象，該對象包含已拆解的PDF文檔以及發生的任何異常。

1. 儲存已拆解的PDF檔案。

   要獲取已拆解的PDF文檔，請執行以下操作：

   * 調用`AssemblerResult`對象的`getDocuments`方法。 此方法會傳回`java.util.Map`物件。
   * 對`java.util.Map`對象進行迭代，直到找到結果`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取PDF文檔。

**另請參閱**

[快速入門（SOAP模式）:使用Java API動態建立DDX檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#dynamically-create-a-ddx-document-using-the-web-service-api}動態建立DDX文檔

使用組合器服務API（Web服務）動態建立DDX文檔並拆解PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 在設定服務引用時，請確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

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

1. 建立DDX文檔。

   * 使用其建構子建立`System.Xml.XmlElement`物件。
   * 調用`XmlElement`對象的`CreateElement`方法，建立DDX文檔的根元素。 此方法會建立代表根元素的`Element`物件。 將代表元素名稱的字串值傳遞至`CreateElement`方法。 通過調用其`SetAttribute`方法來設定DDX元素的值。 最後，通過調用`XmlElement`對象的`AppendChild`方法將元素附加到DDX文檔。 將DDX物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 通過調用`XmlElement`對象的`CreateElement`方法，建立DDX文檔的`PDFsFromBookmarks`元素。 將代表元素名稱的字串值傳遞至`CreateElement`方法。 接下來，呼叫元素的`SetAttribute`方法，以設定元素的值。 呼叫`DDX`元素的`AppendChild`方法，將`PDFsFromBookmarks`元素附加至根元素。 將`PDFsFromBookmarks`元素物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 通過調用`XmlElement`對象的`CreateElement`方法，建立DDX文檔的`PDF`元素。 將代表元素名稱的字串值傳遞至`CreateElement`方法。 接下來，通過調用其`SetAttribute`方法來設定子元素的值。 呼叫`PDFsFromBookmarks`元素的`AppendChild`方法，將`PDF`元素附加至`PDFsFromBookmarks`元素。 將`PDF`元素物件作為引數傳遞。 以下幾行代碼顯示此應用程式邏輯：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 轉換DDX文檔。

   * 使用其建構子建立`System.IO.MemoryStream`物件。
   * 使用代表DDX文檔的`XmlElement`對象，用DDX文檔填充`MemoryStream`對象。 調用`XmlElement`對象的`Save`方法並傳遞`MemoryStream`對象。
   * 建立位元組陣列，並將位於`MemoryStream`物件中的資料填入其中。 下列程式碼會顯示此應用程式邏輯：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 建立`BLOB`物件。 將位元組陣列分配給`BLOB`對象的`MTOM`欄位。

1. 參考要拆卸的PDF文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存輸入的PDF文檔。 此`BLOB`物件會以引數的形式傳遞至`invokeOneDocument`。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為位元組陣列的內容指派其`MTOM`屬性，以填入`BLOB`物件。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 為屬於`AssemblerOptionSpec`對象的資料成員分配值，以設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 反匯編PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * `BLOB`對象，表示動態建立的DDX文檔
   * 包含輸入PDF文檔的`mapItem`陣列
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何異常。

1. 儲存已拆解的PDF檔案。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問`AssemblerResult`對象的`documents`欄位，該欄位是包含已拆解的PDF文檔的`Map`對象。
   * 逐一查看`Map`對象，以獲取每個結果文檔。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 通過訪問其`BLOB`對象的`MTOM`屬性來提取表示PDF文檔的二進位資料。 這會傳回可寫出為PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
