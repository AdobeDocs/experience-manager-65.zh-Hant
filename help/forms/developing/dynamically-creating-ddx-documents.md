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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 0%

---


# 動態建立DDX文檔{#dynamically-creating-ddx-documents}

您可以動態建立DDX文檔，該文檔可用於執行Assembler操作。 動態建立DDX檔案可讓您在執行時期取得的DDX檔案中使用值。 若要動態建立DDX檔案，請使用屬於您所使用之程式設計語言的類別。 例如，如果您使用Java開發客戶端應用程式，請使用屬於`org.w3c.dom.*`包的類。 同樣地，如果您使用Microsoft .NET，請使用屬於`System.Xml`命名空間的類。

在將DDX文檔傳遞到Assembler服務之前，請將XML從`org.w3c.dom.Document`實例轉換為`com.adobe.idp.Document`實例。 如果您使用web services，請將XML從用於建立XML的資料類型（例如`XmlDocument`）轉換為`BLOB`實例。

在此討論中，假設以下DDX文檔是動態建立的。

```xml
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
>如需Assembler服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}摘要

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

使用您使用的程式設計語言建立DDX檔案。 要建立拆解PDF文檔的DDX文檔，請確保該文檔包含`PDFsFromBookmarks`元素。 如果您使用Java API，請將用於建立DDX檔案的資料類型轉換為`com.adobe.idp.Document`例項。 如果您使用web services，請將資料類型轉換為`BLOB`例項。

**轉換DDX檔案**

使用`org.w3c.dom`類建立的DDX文檔必須轉換為`com.adobe.idp.Document`對象。 要在使用Java API時執行此任務，請使用Java XML轉換類。 如果您使用web services，請將DDX檔案轉換為`BLOB`物件。

**參考PDF檔案以進行反匯編**

要反匯編PDF文檔，請參考表示要反匯編的PDF文檔的PDF檔案。 傳遞至Assembler服務時，會針對檔案中的每個第1級書籤傳回個別的PDF檔案。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。 要設定運行時選項，請使用`AssemblerOptionSpec`對象。

**反匯編PDF檔案**

調用`invokeDDX`操作，反匯編PDF文檔。 傳遞動態建立的DDX檔案。 Assembler服務會在收集物件中傳回已拆解的PDF檔案。

**儲存已拆解的PDF檔案**

所有已拆解的PDF檔案都會傳回至系列物件中。 逐步處理系列物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用web service API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式解譯PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API {#dynamically-create-a-ddx-document-using-the-java-api}動態建立DDX檔案

使用Assembler Service API(Java)動態建立DDX檔案並反匯編PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 建立DDX檔案。

   * 通過調用`DocumentBuilderFactory`類`newInstance`方法建立Java `DocumentBuilderFactory`對象。
   * 呼叫`DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立Java `DocumentBuilder`物件。
   * 呼叫`DocumentBuilder`物件的`newDocument`方法，以實例化`org.w3c.dom.Document`物件。
   * 呼叫`org.w3c.dom.Document`物件的`createElement`方法，以建立DDX檔案的根元素。 此方法會建立一個`Element`物件，代表根元素。 將表示元素名稱的字串值傳遞至`createElement`方法。 將返回值轉換為`Element`。 接著，呼叫其`setAttribute`方法，以設定子元素的值。 最後，呼叫標題元素的`appendChild`方法，將元素附加至標題元素，並將子項元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 呼叫`Document`物件的`createElement`方法，以建立`PDFsFromBookmarks`元素。 將表示元素名稱的字串值傳遞至`createElement`方法。 將返回值轉換為`Element`。 通過調用`setAttribute`方法來設定`PDFsFromBookmarks`元素的值。 呼叫DDX元素的`appendChild`方法，將`PDFsFromBookmarks`元素附加至`DDX`元素。 將`PDFsFromBookmarks`元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 呼叫`Document`物件的`createElement`方法，以建立`PDF`元素。 傳遞代表元素名稱的字串值。 將返回值轉換為`Element`。 通過調用`setAttribute`方法來設定`PDF`元素的值。 呼叫`PDFsFromBookmarks`元素的`appendChild`方法，將`PDF`元素附加至`PDFsFromBookmarks`元素。 將`PDF`元素物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 轉換DDX檔案。

   * 通過調用`javax.xml.transform.Transformer`對象的靜態`newInstance`方法建立`javax.xml.transform.Transformer`對象。
   * 調用`TransformerFactory`物件的`newTransformer`方法，以建立`Transformer`物件。
   * 使用其建構子建立`ByteArrayOutputStream`對象。
   * 使用其建構子建立`javax.xml.transform.dom.DOMSource`對象。 傳遞代表DDX文檔的`org.w3c.dom.Document`對象。
   * 使用其建構子並傳遞`ByteArrayOutputStream`對象，建立`javax.xml.transform.dom.DOMSource`對象。
   * 調用`javax.xml.transform.Transformer`物件的`transform`方法，以填入Java `ByteArrayOutputStream`物件。 傳遞`javax.xml.transform.dom.DOMSource`和`javax.xml.transform.stream.StreamResult`物件。
   * 建立位元組陣列，並將`ByteArrayOutputStream`對象的大小分配給位元組陣列。
   * 調用`ByteArrayOutputStream`物件的`toByteArray`方法，以填入位元組陣列。
   * 使用`com.adobe.idp.Document`物件的建構函式並傳遞位元組陣列，以建立&lt;a0/>物件。

1. 參考要反匯編的PDF文檔。

   * 使用`HashMap`建構函式建立`java.util.Map`物件，用來儲存輸入的PDF檔案。
   * 使用其建構函式建立`java.io.FileInputStream`物件，並將PDF檔案的位置傳遞至反匯編。
   * 建立`com.adobe.idp.Document`對象。 將包含PDF文檔的`java.io.FileInputStream`對象傳遞至反匯編。
   * 通過調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。 （在動態建立的DDX檔案中，值為`AssemblerResultPDF.pdf`。）
      * 包含要反匯編的PDF文檔的`com.adobe.idp.Document`對象。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法，設定運行時選項以滿足您的業務要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法並傳遞`false`。

1. 反匯編PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * `com.adobe.idp.Document`物件，代表動態建立的DDX檔案
   * 包含要反匯編的PDF文檔的`java.util.Map`對象
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件，指定執行時間選項，包括預設字型和工作記錄層級

   `invokeDDX`方法會傳回`com.adobe.livecycle.assembler.client.AssemblerResult`物件，其中包含已拆解的PDF檔案和發生的任何例外。

1. 儲存已拆解的PDF檔案。

   要獲取已拆解的PDF文檔，請執行以下操作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 此方法返回`java.util.Map`對象。
   * 重複`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API動態建立DDX檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#dynamically-create-a-ddx-document-using-the-web-service-api}動態建立DDX檔案

使用Assembler Service API(web service)動態建立DDX檔案並反匯編PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 建立DDX檔案。

   * 使用其建構子建立`System.Xml.XmlElement`對象。
   * 呼叫`XmlElement`物件的`CreateElement`方法，以建立DDX檔案的根元素。 此方法會建立一個`Element`物件，代表根元素。 將表示元素名稱的字串值傳遞至`CreateElement`方法。 調用DDX元素的`SetAttribute`方法，為其設定值。 最後，呼叫`XmlElement`物件的`AppendChild`方法，將元素附加至DDX檔案。 將DDX物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 呼叫`XmlElement`物件的`CreateElement`方法，以建立DDX檔案的`PDFsFromBookmarks`元素。 將表示元素名稱的字串值傳遞至`CreateElement`方法。 接著，呼叫元素的`SetAttribute`方法，以設定元素的值。 呼叫`DDX`元素的`AppendChild`方法，將`PDFsFromBookmarks`元素附加至根元素。 將`PDFsFromBookmarks`元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 呼叫`XmlElement`物件的`CreateElement`方法，以建立DDX檔案的`PDF`元素。 將表示元素名稱的字串值傳遞至`CreateElement`方法。 接著，呼叫其`SetAttribute`方法，以設定子元素的值。 呼叫`PDFsFromBookmarks`元素的`AppendChild`方法，將`PDF`元素附加至`PDFsFromBookmarks`元素。 將`PDF`元素物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 轉換DDX檔案。

   * 使用其建構子建立`System.IO.MemoryStream`對象。
   * 使用代表DDX文檔的`XmlElement`對象，將`MemoryStream`對象填入DDX文檔。 叫用`XmlElement`物件的`Save`方法並傳遞`MemoryStream`物件。
   * 建立位元組陣列，並將位於`MemoryStream`物件中的資料填入該陣列。 下列程式碼顯示此應用程式邏輯：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 建立`BLOB`對象。 將位元組陣列指派給`BLOB`物件的`MTOM`欄位。

1. 參考要反匯編的PDF文檔。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存輸入的PDF檔案。 此`BLOB`對象作為參數傳遞給`invokeOneDocument`。
   * 通過調用`System.IO.FileStream`對象的建構子建立&lt;a0/>對象。 傳遞一個字串值，代表輸入PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的資料成員分配值，設定運行時選項以滿足您的業務要求。 例如，要指示Assembler服務在出現錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 反匯編PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * `BLOB`物件，代表動態建立的DDX檔案
   * 包含輸入PDF檔案的`mapItem`陣列
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何例外。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是包含已拆解PDF檔案的`Map`物件。
   * 重複`Map`物件，以取得每個結果檔案。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 存取PDF檔案的`BLOB`物件的`MTOM`屬性，擷取代表PDF檔案的二進位資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
