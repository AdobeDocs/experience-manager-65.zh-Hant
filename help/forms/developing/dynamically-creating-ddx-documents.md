---
title: 動態建立DDX檔案
description: 使用Java API和Web服務API動態建立DDX檔案。 動態建立DDX檔案可讓您使用在執行階段取得的DDX檔案中的值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---

# 動態建立DDX檔案 {#dynamically-creating-ddx-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以動態建立可用來執行Assembler作業的DDX檔案。 動態建立DDX檔案可讓您使用在執行階段取得的DDX檔案中的值。 若要動態建立DDX檔案，請使用屬於您使用之程式語言的類別。 例如，如果您使用Java開發使用者端應用程式，請使用屬於`org.w3c.dom.*`封裝的類別。 同樣地，如果您使用Microsoft .NET，請使用屬於`System.Xml`名稱空間的類別。

在您將DDX檔案傳遞至組合器服務之前，請先將XML從`org.w3c.dom.Document`執行個體轉換為`com.adobe.idp.Document`執行個體。 如果您使用Web服務，請將XML從用來建立XML的資料型別（例如`XmlDocument`）轉換為`BLOB`執行個體。

對於此討論，假設已動態建立下列DDX檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX檔案會拆解PDF檔案。 建議您熟悉PDF檔案的解譯作業。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱[組合器服務與DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

若要使用動態建立的DDX檔案來分解PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 建立DDX檔案。
1. 轉換DDX檔案。
1. 設定執行階段選項。
1. 拆解PDF檔案。
1. 儲存已拆解的PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立PDF組合器使用者端**

在您以程式設計方式執行組合器作業之前，請先建立組合器服務使用者端。

**建立DDX檔案**

使用您使用的程式語言建立DDX檔案。 若要建立可解散PDF檔案的DDX檔案，請確定它包含`PDFsFromBookmarks`元素。 如果您使用Java API，請將用來建立DDX檔案的資料型別轉換為`com.adobe.idp.Document`執行個體。 如果您使用網站服務，請將資料型別轉換為`BLOB`執行個體。

**轉換DDX檔案**

使用`org.w3c.dom`類別建立的DDX檔案必須轉換成`com.adobe.idp.Document`物件。 若要在使用Java API時執行此工作，請使用Java XML轉換類別。 如果您使用網站服務，請將DDX檔案轉換為`BLOB`物件。

**參考PDF檔案以拆解**

若要拆解PDF檔案，請參照代表要拆解PDF檔案的PDF檔案。 當傳遞至Assembler服務時，會針對檔案中的每個1級書籤傳回個別的PDF檔案。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。 若要設定執行階段選項，請使用`AssemblerOptionSpec`物件。

**拆解PDF檔案**

透過叫用`invokeDDX`作業來分解PDF檔案。 傳遞動態建立的DDX檔案。 Assembler服務會傳回集合物件中已拆解的PDF檔案。

**儲存已解譯的PDF檔案**

所有已拆解的PDF檔案都會在集合物件中傳回。 逐一檢視集合物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用網站服務API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式分解的PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API動態建立DDX檔案 {#dynamically-create-a-ddx-document-using-the-java-api}

使用組合器服務API (Java)動態建立DDX檔案並分解PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`AssemblerServiceClient`物件。

1. 建立DDX檔案。

   * 呼叫`DocumentBuilderFactory`類別的`newInstance`方法，以建立Java `DocumentBuilderFactory`物件。
   * 呼叫`DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立Java `DocumentBuilder`物件。
   * 呼叫`DocumentBuilder`物件的`newDocument`方法以例項化`org.w3c.dom.Document`物件。
   * 呼叫`org.w3c.dom.Document`物件的`createElement`方法，以建立DDX檔案的根專案。 此方法會建立代表根專案的`Element`物件。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 接著，呼叫子專案的`setAttribute`方法，以設定其值。 最後，呼叫標頭專案的`appendChild`方法，將專案附加至標頭專案，並將子專案物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 呼叫`Document`物件的`createElement`方法，以建立`PDFsFromBookmarks`專案。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 呼叫其`setAttribute`方法，以設定`PDFsFromBookmarks`專案的值。 呼叫DDX專案的`appendChild`方法，將`PDFsFromBookmarks`專案附加至`DDX`專案。 將`PDFsFromBookmarks`專案物件傳遞為引數。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 呼叫`Document`物件的`createElement`方法，以建立`PDF`專案。 傳遞代表元素名稱的字串值。 將傳回值轉換為`Element`。 呼叫其`setAttribute`方法，以設定`PDF`專案的值。 呼叫`PDFsFromBookmarks`專案的`appendChild`方法，將`PDF`專案附加至`PDFsFromBookmarks`專案。 將`PDF`專案物件傳遞為引數。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 轉換DDX檔案。

   * 呼叫`javax.xml.transform.Transformer`物件的靜態`newInstance`方法，以建立`javax.xml.transform.Transformer`物件。
   * 呼叫`TransformerFactory`物件的`newTransformer`方法，以建立`Transformer`物件。
   * 使用物件的建構函式建立`ByteArrayOutputStream`物件。
   * 使用物件的建構函式建立`javax.xml.transform.dom.DOMSource`物件。 傳遞代表DDX檔案的`org.w3c.dom.Document`物件。
   * 使用它的建構函式並傳遞`ByteArrayOutputStream`物件來建立`javax.xml.transform.dom.DOMSource`物件。
   * 叫用`javax.xml.transform.Transformer`物件的`transform`方法填入Java `ByteArrayOutputStream`物件。 傳遞`javax.xml.transform.dom.DOMSource`和`javax.xml.transform.stream.StreamResult`物件。
   * 建立位元組陣列，並將`ByteArrayOutputStream`物件的大小配置給位元組陣列。
   * 叫用`ByteArrayOutputStream`物件的`toByteArray`方法來填入位元組陣列。
   * 使用它的建構函式並傳遞位元組陣列，來建立`com.adobe.idp.Document`物件。

1. 參照要拆解的PDF檔案。

   * 使用`HashMap`建構函式建立用來儲存輸入PDF檔案的`java.util.Map`物件。
   * 使用物件的建構函式並傳遞PDF檔案的位置來建立`java.io.FileInputStream`物件以進行拆解。
   * 建立`com.adobe.idp.Document`物件。 傳遞包含PDF檔案的`java.io.FileInputStream`物件以進行拆解。
   * 透過叫用物件的`put`方法並傳遞下列引數，將專案新增至`java.util.Map`物件：

      * 代表索引鍵名稱的字串值。 此值必須符合DDX檔案中指定的PDF來源元素的值。 （在動態建立的DDX檔案中，值為`AssemblerResultPDF.pdf`。）
      * 包含要拆解之PDF檔案的`com.adobe.idp.Document`物件。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 透過叫用屬於`AssemblerOptionSpec`物件的方法，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法，然後傳遞`false`。

1. 拆解PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列值：

   * 代表動態建立之DDX檔案的`com.adobe.idp.Document`物件
   * 包含要分解之PDF檔案的`java.util.Map`物件
   * 指定執行階段選項（包括預設字型和作業記錄層級）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件

   `invokeDDX`方法傳回`com.adobe.livecycle.assembler.client.AssemblerResult`物件，其中包含已解譯的PDF檔案以及發生的任何例外狀況。

1. 儲存已拆解的PDF檔案。

   若要取得已拆解的PDF檔案，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 此方法會傳回`java.util.Map`物件。
   * 逐一檢視`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件為止。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

**另請參閱**

[快速入門(SOAP模式)：使用Java API動態建立DDX檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API動態建立DDX檔案 {#dynamically-create-a-ddx-document-using-the-web-service-api}

使用Assembler Service API （Web服務）動態建立DDX檔案並分解PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您在設定服務參考時使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立PDF組合器使用者端。

   * 使用預設建構函式建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。
   * 取得`AssemblerServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 建立DDX檔案。

   * 使用物件的建構函式建立`System.Xml.XmlElement`物件。
   * 呼叫`XmlElement`物件的`CreateElement`方法，以建立DDX檔案的根專案。 此方法會建立代表根專案的`Element`物件。 將代表元素名稱的字串值傳遞至`CreateElement`方法。 呼叫DDX專案的`SetAttribute`方法，以設定該專案的值。 最後，呼叫`XmlElement`物件的`AppendChild`方法，將元素附加至DDX檔案。 傳遞DDX物件作為引數。 下列幾行程式碼會顯示此應用程式邏輯：

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 呼叫`XmlElement`物件的`CreateElement`方法，建立DDX檔案的`PDFsFromBookmarks`專案。 將代表元素名稱的字串值傳遞至`CreateElement`方法。 接著，呼叫元素的`SetAttribute`方法，以設定元素的值。 呼叫`DDX`專案的`AppendChild`方法，將`PDFsFromBookmarks`專案附加至根專案。 將`PDFsFromBookmarks`專案物件傳遞為引數。 下列幾行程式碼會顯示此應用程式邏輯：

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 呼叫`XmlElement`物件的`CreateElement`方法，建立DDX檔案的`PDF`專案。 將代表元素名稱的字串值傳遞至`CreateElement`方法。 接著，呼叫子專案的`SetAttribute`方法，以設定其值。 呼叫`PDFsFromBookmarks`專案的`AppendChild`方法，將`PDF`專案附加至`PDFsFromBookmarks`專案。 將`PDF`專案物件傳遞為引數。 下列幾行程式碼會顯示此應用程式邏輯：

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 轉換DDX檔案。

   * 使用物件的建構函式建立`System.IO.MemoryStream`物件。
   * 使用代表DDX檔案的`XmlElement`物件將DDX檔案填入`MemoryStream`物件。 叫用`XmlElement`物件的`Save`方法並傳遞`MemoryStream`物件。
   * 建立位元組陣列，並在`MemoryStream`物件中填入資料。 下列程式碼顯示此應用程式邏輯：

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 建立`BLOB`物件。 將位元組陣列指派給`BLOB`物件的`MTOM`欄位。

1. 參照要拆解的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存輸入PDF檔案。 此`BLOB`物件會以引數的形式傳遞至`invokeOneDocument`。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表輸入PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 將物件的`MTOM`屬性指派給位元組陣列的內容，以填入`BLOB`物件。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 將值指派給屬於`AssemblerOptionSpec`物件的資料成員，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請將`false`指派給`AssemblerOptionSpec`物件的`failOnError`資料成員。

1. 拆解PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列值：

   * 代表動態建立之DDX檔案的`BLOB`物件
   * 包含輸入PDF檔案的`mapItem`陣列
   * 指定執行階段選項的`AssemblerOptionSpec`物件

   `invokeDDX`方法傳回`AssemblerResult`物件，其中包含工作的結果和發生的任何例外狀況。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是包含已解除組裝PDF檔案的`Map`物件。
   * 逐一檢視`Map`物件以取得每個結果檔案。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 存取其`BLOB`物件的`MTOM`屬性，以擷取代表PDF檔案的二進位資料。 這會傳回您可以寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
