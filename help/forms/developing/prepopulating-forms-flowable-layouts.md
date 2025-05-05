---
title: 使用可流程配置預先填入Forms
description: 將表單預先填入為可流動佈局，以便使用Java API和網站服務API在轉譯的表單內向使用者顯示資料。
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '3478'
ht-degree: 0%

---

# 使用可流程配置預先填入Forms {#prepopulating-forms-with-flowable-layouts1}

## 使用可流程配置預先填入Forms {#prepopulating-forms-with-flowable-layouts2}

預先填入表單會在轉譯的表單中向使用者顯示資料。 例如，假設使用者使用使用者名稱和密碼登入網站。 如果驗證成功，使用者端應用程式會查詢資料庫以取得使用者資訊。 資料會合併至表單，然後表單會呈現給使用者。 因此，使用者可以在表單中檢視個人化資料。

預先填入表單具有以下優點：

* 讓使用者能在表單中檢視自訂資料。
* 減少使用者在表單中輸入的次數。
* 控制資料放置的位置，確保資料完整性。

以下兩個XML資料來源可以預先填入表單：

* XDP資料來源是符合XFA語法的XML (或是預先填入使用Acrobat建立的表單的XFDF資料)。
* 任意XML資料來源，包含符合表單欄位名稱的名稱/值組（本節中的範例使用任意XML資料來源）。

要預先填入的每個表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 只要指定所有XML元素，就不需要比對XML元素的顯示順序。

預先填入已包含資料的表單時，您必須指定已在XML資料來源中顯示的資料。 假設包含10個欄位的表單有4個欄位中的資料。 接下來，假設您要預先填入其餘六個欄位。 在此情況下，您必須在XML資料來源中指定10個XML元素，用於預先填入表單。 如果您只指定六個元素，則原始的四個欄位為空白。

例如，您可以預先填入表單，如範例確認表單。 (請參閱[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)中的「確認表單」。)

若要預先填入範例確認表單，您必須建立包含三個XML元素（符合表單中的三個欄位）的XML資料來源。 此表單包含下列三個欄位： `FirstName`、`LastName`和`Amount`。 第一步是建立包含符合表單設計中欄位的XML元素的XML資料來源。 下一步是將資料值指派給XML元素，如下列XML程式碼所示。

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

使用此XML資料來源預先填入確認表單，然後轉譯表單後，您指派給XML元素的資料值會顯示出來，如下圖所示。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 使用可流動版面配置預先填入表單 {#prepopulating_forms_with_flowable_layouts-1}

具有可流動版面的Forms對於向使用者顯示未確定的資料量很有用。 由於表單的版面配置會自動調整為符合合併的資料量，因此您不需要像處理具有固定版面的表單那樣預先決定表單的固定版面配置或頁數。

表單通常會填入執行階段取得的資料。 因此，您可以建立記憶體內XML資料來源，並將資料直接放入記憶體內XML資料來源，預先填入表單。

考慮使用網路型應用程式，例如線上商店。 線上購物者完成購買專案後，所有購買的專案都會放入記憶體中XML資料來源，用於預先填入表單。 下圖顯示此程式，圖後的表格對此程式進行了說明。

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

下表說明此圖表中的步驟。

<table>
 <thead>
  <tr>
   <th><p>步驟</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>使用者從網路型線上商店購買專案。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>使用者完成採購料號並按一下「提交」按鈕後，即會建立記憶體中的XML資料來源。 購買的專案和使用者資訊會放入記憶體中的XML資料來源中。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML資料來源可用來預先填入採購單表單（此表單的範例顯示於此表格下方）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>採購單表單會呈現給使用者端網頁瀏覽器。 </p></td>
  </tr>
 </tbody>
</table>

下圖顯示採購單表單的範例。 表格中的資訊可以調整為XML資料中的記錄數。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>表單可以預先填入來自其他來源（例如企業資料庫或外部應用程式）的資料。

### 表單設計考量事項 {#form-design-considerations}

具有可流動版面的Forms是根據在Designer中建立的表單設計。 表單設計會指定一組配置、顯示和資料擷取規則，包括根據使用者輸入計算值。 將資料輸入表單時會套用規則。 新增至表單的欄位是表單設計內的子表單。 例如，在上圖所示的採購單表單中，每一行都是子表單。 如需建立包含子表單的表單設計相關資訊，請參閱[建立具有流程配置之採購單表單](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9_tw)。

### 瞭解資料子群組 {#understanding-data-subgroups}

XML資料來源可用來預先填入具有固定版面配置和可流動版面的表單。 不過，不同之處在於，以可流程配置預先填入表單的XML資料來源包含重複的XML元素，這些元素用於預先填入表單內重複的子表單。 這些重複的XML元素稱為資料子群組。

用來預先填入上圖所示之採購單表單的XML資料來源包含四個重複的資料子群組。 每個資料子群組都對應至已購買的專案。 購買的專案包括顯示器、檯燈、電話和通訊錄。

下列XML資料來源可用來預先填入採購單表單。

```xml
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

請注意，每個資料子群組都包含四個XML元素，這些元素對應至下列資訊：

* 專案部分編號
* 專案說明
* 專案數量
* 單價

資料子群組的父XML元素名稱必須符合表單設計中的子表單名稱。 例如，在上一個圖表中，請注意資料子群組的父XML元素名稱為`detail`。 這對應於採購單表單所依據之表單設計中的子表單名稱。 如果資料子群組的父XML元素名稱與子表單不符，則不會預先填入伺服器端表單。

每個資料子群組都必須包含符合子表單中欄位名稱的XML元素。 表單設計中的`detail`子表單包含下列欄位：

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>如果您嘗試使用包含重複XML元素的資料來源預先填入表單，並且將`RenderAtClient`選項設定為`No`，則只有第一個資料記錄會合併到表單中。 為確保所有資料記錄都合併到表單中，請將`RenderAtClient`設定為`Yes`。 如需`RenderAtClient`選項的詳細資訊，請參閱[在使用者端轉譯Forms](/help/forms/developing/rendering-forms-client.md)。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要以可流動版面配置預先填入表單，請執行下列工作：

1. 包含專案檔案。
1. 建立記憶體中的XML資料來源。
1. 轉換XML資料來源。
1. 呈現預先填入的表單。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立記憶體中的XML資料來源**

您可以使用`org.w3c.dom`類別來建立記憶體中的XML資料來源，以預先填入具有流程配置的表單。 將資料放入符合表單的XML資料來源中。 如需有關具有流程配置之表單與XML資料來源之間關係的資訊，請參閱[瞭解資料子群組](#understanding-data-subgroups)。

**轉換XML資料來源**

使用`org.w3c.dom`類別建立的記憶體內XML資料來源可以轉換為`com.adobe.idp.Document`物件，然後才可用來預先填入表單。 您可以使用Java XML轉換類別來轉換記憶體中的XML資料來源。

>[!NOTE]
>
>如果您使用Forms服務的WSDL預先填入表單，您必須將`org.w3c.dom.Document`物件轉換為`BLOB`物件。

**呈現預先填入的表單**

呈現預先填入的表單的方式與其他表單類似。 唯一的差異是您使用包含XML資料來源的`com.adobe.idp.Document`物件來預先填入表單。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API預先填入表單 {#prepopulating-forms-using-the-java-api}

若要使用Forms API (Java)預先填入具有流程配置的表單，請執行以下步驟：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。 如需這些檔案位置的相關資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立記憶體中的XML資料來源

   * 呼叫`DocumentBuilderFactory`類別的`newInstance`方法，以建立Java `DocumentBuilderFactory`物件。
   * 呼叫`DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立Java `DocumentBuilder`物件。
   * 呼叫`DocumentBuilder`物件的`newDocument`方法以例項化`org.w3c.dom.Document`物件。
   * 呼叫`org.w3c.dom.Document`物件的`createElement`方法，以建立XML資料來源的根專案。 這會建立代表根專案的`Element`物件。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 接著，呼叫`Document`物件的`appendChild`方法，將根元素附加至檔案，然後傳遞根元素物件做為引數。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫`Document`物件的`createElement`方法，以建立XML資料來源的標頭專案。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 接著，呼叫`root`物件的`appendChild`方法，將標頭專案附加至根專案，然後將標頭專案物件作為引數傳遞。 附加至標頭元素的XML元素會對應至表單的靜態部分。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 呼叫`Document`物件的`createElement`方法，建立屬於標頭專案的子專案，並傳遞代表專案名稱的字串值。 將傳回值轉換為`Element`。 接著，呼叫子專案的`appendChild`方法以設定其值，並將`Document`物件的`createTextNode`方法傳遞為引數。 指定顯示為子專案值的字串值。 最後，呼叫標頭專案的`appendChild`方法，將子專案附加至標頭專案，並將子專案物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 重複表單靜態部分中顯示之每個欄位的最後一個子步驟（在XML資料來源圖表中，這些欄位顯示在A節中），將所有剩餘的元素新增至標頭元素。（請參閱[瞭解資料子群組](#understanding-data-subgroups)。）
   * 呼叫`Document`物件的`createElement`方法，以建立XML資料來源的詳細資料專案。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 接著，呼叫`root`物件的`appendChild`方法，將詳細專案附加至根專案，然後將詳細專案物件作為引數傳遞。 附加至詳細資訊元素的XML元素會對應至表單的動態部分。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫`Document`物件的`createElement`方法，建立屬於詳細資料專案的子專案，並傳遞代表專案名稱的字串值。 將傳回值轉換為`Element`。 接著，呼叫子專案的`appendChild`方法以設定其值，並將`Document`物件的`createTextNode`方法傳遞為引數。 指定顯示為子專案值的字串值。 最後，呼叫細節專案的`appendChild`方法，將子專案附加至細節專案，並將子專案物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加至詳細資料元素。 若要正確建立用於填入採購單表單的XML資料來源，您必須將下列XML元素附加至詳細資料元素： `txtDescription`、`numQty`和`numUnitPrice`。
   * 針對用於預先填入表單的所有資料專案，重複前兩個子步驟。

1. 轉換XML資料來源

   * 呼叫`javax.xml.transform.Transformer`物件的靜態`newInstance`方法，以建立`javax.xml.transform.Transformer`物件。
   * 呼叫`TransformerFactory`物件的`newTransformer`方法，以建立`Transformer`物件。
   * 使用物件的建構函式建立`ByteArrayOutputStream`物件。
   * 使用它的建構函式並傳遞在步驟1中建立的`org.w3c.dom.Document`物件來建立`javax.xml.transform.dom.DOMSource`物件。
   * 使用它的建構函式並傳遞`ByteArrayOutputStream`物件來建立`javax.xml.transform.dom.DOMSource`物件。
   * 呼叫`javax.xml.transform.Transformer`物件的`transform`方法並傳遞`javax.xml.transform.dom.DOMSource`和`javax.xml.transform.stream.StreamResult`物件以填入Java `ByteArrayOutputStream`物件。
   * 建立位元組陣列，並將`ByteArrayOutputStream`物件的大小配置給位元組陣列。
   * 叫用`ByteArrayOutputStream`物件的`toByteArray`方法來填入位元組陣列。
   * 使用它的建構函式並傳遞位元組陣列，來建立`com.adobe.idp.Document`物件。

1. 呈現預先填入的表單

   叫用`FormsServiceClient`物件的`renderPDFForm`方法，並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。
   * 包含要與表單合併之資料的`com.adobe.idp.Document`物件。 請確定您使用在步驟一和步驟二中建立的`com.adobe.idp.Document`物件。
   * 儲存執行階段選項的`PDFFormRenderSpec`物件。
   * 包含Forms服務所需URI值的`URLSpec`物件。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。

   `renderPDFForm`方法傳回`FormsResult`物件，其中包含必須寫入使用者端網頁瀏覽器的表單資料流。

   * 建立用來傳送表單資料流至使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件。
   * 呼叫`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 呼叫`InputStream`物件的`read`方法，並將位元組陣列作為引數傳遞，以表單資料流填入位元組陣列。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[快速入門(SOAP模式)：使用Java API以可流動的版面配置預先填入Forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API預先填入表單 {#prepopulating-forms-using-the-web-service-api}

若要使用Forms API （Web服務）預先填入具有流動版面的表單，請執行以下步驟：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。 （請參閱[使用Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)建立Java Proxy類別。）
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立記憶體中的XML資料來源

   * 呼叫`DocumentBuilderFactory`類別的`newInstance`方法，以建立Java `DocumentBuilderFactory`物件。
   * 呼叫`DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立Java `DocumentBuilder`物件。
   * 呼叫`DocumentBuilder`物件的`newDocument`方法以例項化`org.w3c.dom.Document`物件。
   * 呼叫`org.w3c.dom.Document`物件的`createElement`方法，以建立XML資料來源的根專案。 這會建立代表根專案的`Element`物件。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 接著，呼叫`Document`物件的`appendChild`方法，將根元素附加至檔案，然後傳遞根元素物件做為引數。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫`Document`物件的`createElement`方法，以建立XML資料來源的標頭專案。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 接著，呼叫`root`物件的`appendChild`方法，將標頭專案附加至根專案，然後將標頭專案物件作為引數傳遞。 附加至標頭元素的XML元素會對應至表單的靜態部分。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 呼叫`Document`物件的`createElement`方法，建立屬於標頭專案的子專案，並傳遞代表專案名稱的字串值。 將傳回值轉換為`Element`。 接著，呼叫子專案的`appendChild`方法以設定其值，並將`Document`物件的`createTextNode`方法傳遞為引數。 指定顯示為子專案值的字串值。 最後，呼叫標頭專案的`appendChild`方法，將子專案附加至標頭專案，並將子專案物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 重複表單靜態部分中顯示之每個欄位的最後一個子步驟（在XML資料來源圖表中，這些欄位顯示在A節中），將所有剩餘的元素新增至標頭元素。（請參閱[瞭解資料子群組](#understanding-data-subgroups)。）
   * 呼叫`Document`物件的`createElement`方法，以建立XML資料來源的詳細資料專案。 將代表元素名稱的字串值傳遞至`createElement`方法。 將傳回值轉換為`Element`。 接著，呼叫`root`物件的`appendChild`方法，將詳細專案附加至根專案，然後將詳細專案物件作為引數傳遞。 附加至詳細資訊元素的XML元素會對應至表單的動態部分。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫`Document`物件的`createElement`方法，建立屬於詳細資料專案的子專案，並傳遞代表專案名稱的字串值。 將傳回值轉換為`Element`。 接著，呼叫子專案的`appendChild`方法以設定其值，並將`Document`物件的`createTextNode`方法傳遞為引數。 指定顯示為子專案值的字串值。 最後，呼叫細節專案的`appendChild`方法，將子專案附加至細節專案，並將子專案物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加至詳細資料元素。 若要正確建立用於填入採購單表單的XML資料來源，您必須將下列XML元素附加至詳細資料元素： `txtDescription`、`numQty`和`numUnitPrice`。
   * 針對用於預先填入表單的所有資料專案，重複前兩個子步驟。

1. 轉換XML資料來源

   * 呼叫`javax.xml.transform.Transformer`物件的靜態`newInstance`方法，以建立`javax.xml.transform.Transformer`物件。
   * 呼叫`TransformerFactory`物件的`newTransformer`方法，以建立`Transformer`物件。
   * 使用物件的建構函式建立`ByteArrayOutputStream`物件。
   * 使用它的建構函式並傳遞在步驟1中建立的`org.w3c.dom.Document`物件來建立`javax.xml.transform.dom.DOMSource`物件。
   * 使用它的建構函式並傳遞`ByteArrayOutputStream`物件來建立`javax.xml.transform.dom.DOMSource`物件。
   * 呼叫`javax.xml.transform.Transformer`物件的`transform`方法並傳遞`javax.xml.transform.dom.DOMSource`和`javax.xml.transform.stream.StreamResult`物件以填入Java `ByteArrayOutputStream`物件。
   * 建立位元組陣列，並將`ByteArrayOutputStream`物件的大小配置給位元組陣列。
   * 叫用`ByteArrayOutputStream`物件的`toByteArray`方法來填入位元組陣列。
   * 使用它的建構函式建立`BLOB`物件，叫用它的`setBinaryData`方法並傳遞位元組陣列。

1. 呈現預先填入的表單

   叫用`FormsService`物件的`renderPDFForm`方法，並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。
   * 包含要與表單合併之資料的`BLOB`物件。 請確定您使用在步驟一和步驟二中建立的`BLOB`物件。
   * 儲存執行階段選項的`PDFFormRenderSpecc`物件。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 包含Forms服務所需URI值的`URLSpec`物件。
   * 儲存檔案附件的`java.util.HashMap`物件。 這是選用引數，如果您不想將檔案附加至表單，可以指定`null`。
   * 方法填入的空白`com.adobe.idp.services.holders.BLOBHolder`物件。 這可用來儲存轉譯的PDF表單。
   * 方法填入的空白`javax.xml.rpc.holders.LongHolder`物件。 （此引數會儲存表單中的頁數）。
   * 方法填入的空白`javax.xml.rpc.holders.StringHolder`物件。 （此引數將會儲存地區設定值）。
   * 包含此作業結果的空白`com.adobe.idp.services.holders.FormsResultHolder`物件。

   `renderPDFForm`方法會將必須寫入使用者端網頁瀏覽器的表單資料流，填入作為最後一個引數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

   * 取得`com.adobe.idp.services.holders.FormsResultHolder`物件之`value`資料成員的值，以建立`FormResult`物件。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 透過叫用物件的`getContentType`方法，取得`BLOB`物件的內容型別。
   * 透過叫用其`setContentType`方法並傳遞`BLOB`物件的內容型別來設定`javax.servlet.http.HttpServletResponse`物件的內容型別。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立用來將表單資料流寫入使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 建立位元組陣列，並透過叫用`BLOB`物件的`getBinaryData`方法來填入該陣列。 此工作會將`FormsResult`物件的內容指派給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

   >[!NOTE]
   >
   >`renderPDFForm`方法會將必須寫入使用者端網頁瀏覽器的表單資料流，填入作為最後一個引數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
