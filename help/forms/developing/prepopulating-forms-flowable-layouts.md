---
title: 使用可流式配置預填Forms
seo-title: Prepopulating Forms with Flowable Layouts
description: 以可流動的版面預先填入表單，以使用Java API和網站服務API向呈現表單中的使用者顯示資料。
seo-description: Prepopulate forms with flowable layout to display data to users within a rendered form using the Java API and the Web Service API.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '3505'
ht-degree: 0%

---

# 使用可流式配置預填Forms {#prepopulating-forms-with-flowable-layouts1}

## 使用可流式配置預填Forms {#prepopulating-forms-with-flowable-layouts2}

預先填入的表單會向呈現表單中的使用者顯示資料。 例如，假設使用者以使用者名稱和密碼登入網站。 如果驗證成功，則客戶端應用程式查詢資料庫以獲取用戶資訊。 資料會合併到表單中，然後將表單轉譯給使用者。 因此，使用者能夠檢視表單中的個人化資料。

預填表單具有以下優點：

* 讓使用者可在表單中檢視自訂資料。
* 減少輸入使用者以填入表單的量。
* 通過控制資料的放置位置，確保資料完整性。

以下兩個XML資料來源可以預先填入表單：

* XDP資料來源，是符合XFA語法的XML(或XFDF資料，以預先填入使用Acrobat建立的表單)。
* 任意XML資料源，包含與表單欄位名稱匹配的名稱/值對（本節中的示例使用任意XML資料源）。

要預填的每個表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不匹配，則會忽略該元素。 只要指定了所有XML元素，就不需要匹配XML元素的顯示順序。

預先填入已包含資料的表單時，必須指定已顯示在XML資料來源中的資料。 假設一個包含10個欄位的表單有4個欄位中的資料。 接下來，假設您要預填其餘六個欄位。 在此情況下，您必須在用於預填表單的XML資料來源中指定10個XML元素。 如果僅指定六個元素，則原始的四個欄位為空。

例如，您可以預先填入表單，例如範例確認表單。 (請參閱 [轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)

要預填示例確認表單，必須建立一個XML資料源，該資料源包含三個與表單中的三個欄位匹配的XML元素。 此表單包含下列三個欄位： `FirstName`, `LastName`，和 `Amount`. 第一步是建立XML資料源，該資料源包含與表單設計中的欄位匹配的XML元素。 下一步是將資料值分配給XML元素，如以下XML代碼所示。

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

使用此XML資料源預填確認表單，然後呈現表單後，將顯示分配給XML元素的資料值，如下圖所示。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 使用可流動版面預填表單 {#prepopulating_forms_with_flowable_layouts-1}

具有可流動配置的Forms對於向使用者顯示數量不定的資料非常有用。 由於表單的版面會自動調整為合併的資料量，因此您不需要預先決定表單的固定版面或頁面數，因為您需要處理具有固定版面的表單。

表單通常會填入在執行階段取得的資料。 因此，您可以建立記憶體內XML資料源，並將資料直接放入記憶體內XML資料源中，以預填表單。

考慮基於Web的應用程式，例如線上商店。 線上購物者完成購買項目後，所有購買項目都會放入記憶體內XML資料來源中，以用於預先填入表單。 下圖顯示了此過程，詳見圖後的表格。

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

下表說明此圖中的步驟。

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
   <td><p>使用者從網頁型線上商店購買項目。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>當使用者完成購買項目並按一下「提交」按鈕後，就會建立記憶體內的XML資料來源。 購買的項目和用戶資訊將放入記憶體中的XML資料源中。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML資料源用於預填採購訂單表單（下表顯示了此表單的示例）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>採購訂單表單將呈現給客戶端Web瀏覽器。 </p></td>
  </tr>
 </tbody>
</table>

下圖顯示採購訂單表單的示例。 表中的資訊可以根據XML資料中的記錄數進行調整。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>表單可以預先填入來自其他來源的資料，例如企業資料庫或外部應用程式。

### 表單設計考量事項 {#form-design-considerations}

具有可流動版面的Forms以在Designer中建立的表單設計為基礎。 表單設計指定一組佈局、呈現和資料捕獲規則，包括基於用戶輸入的計算值。 在表單中輸入資料時，會套用規則。 新增至表單的欄位是表單設計中的子表單。 例如，在上圖中顯示的採購訂單表單中，每行都是子表單。 如需建立包含子表單的表單設計的相關資訊，請參閱 [建立具有可流式佈局的採購訂單表單](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### 了解資料子組 {#understanding-data-subgroups}

XML資料來源可用來預先填入固定版面和可流動版面的表單。 但是，區別在於，使用可流式佈局預填表單的XML資料源包含用於預填表單中重複的子表單的重複XML元素。 這些重複的XML元素稱為資料子組。

用於預填上圖中所示採購訂單表單的XML資料源包含四個重複資料子組。 每個資料子群組都對應至購買的項目。 購買的物品包括顯示器、台燈、電話和通訊簿。

以下XML資料源用於預填採購訂單表單。

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

請注意，每個資料子組都包含四個與此資訊對應的XML元素：

* 物料部件號
* 項目說明
* 項目數量
* 單價

資料子組的父XML元素的名稱必須與位於表單設計中的子表單的名稱匹配。 例如，在上圖中，請注意資料子組的父XML元素的名稱是 `detail`. 這對應於採購訂單表單所基於的表單設計中的子表單的名稱。 如果資料子組的父XML元素名稱與子表單名稱不匹配，則不會預填伺服器端表單。

每個資料子組必須包含與子表單中的欄位名稱匹配的XML元素。 此 `detail` 表單設計中的子表單包含下列欄位：

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>如果您嘗試使用包含重複XML元素的資料來源預先填入表單，並設定 `RenderAtClient` 選項 `No`，則只會將第一個資料記錄合併至表單中。 為確保所有資料記錄都合併到表單中，請設定 `RenderAtClient` to `Yes`. 如需 `RenderAtClient` 選項，請參閱 [在用戶端呈現Forms](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要使用可流式佈局預填表單，請執行以下任務：

1. 包含專案檔案。
1. 建立記憶體內XML資料源。
1. 轉換XML資料源。
1. 呈現預先填入的表單。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立記憶體內XML資料源**

您可以使用 `org.w3c.dom` 類以建立記憶體內XML資料源，以預填具有可流式佈局的表單。 必須將資料放入符合窗體的XML資料源中。 有關具有可流式佈局的表單與XML資料源之間關係的資訊，請參見 [了解資料子組](#understanding-data-subgroups).

**轉換XML資料源**

記憶體內XML資料源，使用 `org.w3c.dom` 類別可轉換為 `com.adobe.idp.Document` 物件，才能用來預先填入表單。 記憶體中的XML資料源可以使用Java XML轉換類進行轉換。

>[!NOTE]
>
>如果您使用Forms服務的WSDL來預先填入表單，則必須轉換 `org.w3c.dom.Document` 物件 `BLOB` 物件。

**呈現預先填入的表單**

您會呈現預先填入的表單，就像其他表單一樣。 唯一的差異是您使用 `com.adobe.idp.Document` 包含要預填表單之XML資料來源的物件。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API預先填入表單 {#prepopulating-forms-using-the-java-api}

若要使用Forms API(Java)以可流式版面預先填入表單，請執行下列步驟：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。 如需這些檔案的位置資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. 建立記憶體內XML資料源

   * 建立Java `DocumentBuilderFactory` 物件，方法是呼叫 `DocumentBuilderFactory` class `newInstance` 方法。
   * 建立Java `DocumentBuilder` 物件，方法是呼叫 `DocumentBuilderFactory` 物件 `newDocumentBuilder` 方法。
   * 呼叫 `DocumentBuilder` 物件 `newDocument` 實例化方法 `org.w3c.dom.Document` 物件。
   * 叫用 `org.w3c.dom.Document` 物件 `createElement` 方法。 這會建立 `Element` 代表根元素的物件。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，呼叫 `Document` 物件 `appendChild` 方法，並將根元素物件作為引數傳遞。 以下幾行代碼顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫 `Document` 物件 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，呼叫 `root` 物件 `appendChild` 方法，並將header元素物件作為引數傳遞。 附加到標題元素的XML元素對應於表單的靜態部分。 下列幾行程式碼會顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 呼叫 `Document` 物件 `createElement` 方法，並傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 接下來，呼叫子元素，以設定子元素的值 `appendChild` 方法，並傳遞 `Document` 物件 `createTextNode` 方法做為引數。 指定顯示為子元素值的字串值。 最後，呼叫標頭元素的 `appendChild` 方法，並將子元素物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 重複表單靜態部分中每個欄位的最後一個子步驟，將所有剩餘元素新增至標題元素（在XML資料來源圖表中，這些欄位顯示在A節中）。 [了解資料子組](#understanding-data-subgroups).)
   * 呼叫 `Document` 物件 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，呼叫 `root` 物件 `appendChild` 方法，並將detail元素物件作為引數傳遞。 附加到詳細元素的XML元素對應於表單的動態部分。 下列幾行程式碼會顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫 `Document` 物件 `createElement` 方法，並傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 接下來，呼叫子元素，以設定子元素的值 `appendChild` 方法，並傳遞 `Document` 物件 `createTextNode` 方法做為引數。 指定顯示為子元素值的字串值。 最後，呼叫詳細資料元素的 `appendChild` 方法，並將子元素物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加到詳細資訊元素。 要正確建立用於填充採購訂單表單的XML資料源，必須將以下XML元素附加到詳細資訊元素： `txtDescription`, `numQty`，和 `numUnitPrice`.
   * 對用於預先填入表單的所有資料項目，重複最後兩個子步驟。

1. 轉換XML資料源

   * 建立 `javax.xml.transform.Transformer` 對象，方法是調用 `javax.xml.transform.Transformer` 對象的靜態 `newInstance` 方法。
   * 建立 `Transformer` 對象，方法是調用 `TransformerFactory` 物件 `newTransformer` 方法。
   * 建立 `ByteArrayOutputStream` 物件，使用其建構子。
   * 建立 `javax.xml.transform.dom.DOMSource` 對象，使用其建構子並傳遞 `org.w3c.dom.Document` 在步驟1中建立的物件。
   * 建立 `javax.xml.transform.dom.DOMSource` 對象，使用其建構子並傳遞 `ByteArrayOutputStream` 物件。
   * 填入Java `ByteArrayOutputStream` 對象，方法是調用 `javax.xml.transform.Transformer` 物件 `transform` 方法和傳遞 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 對象。
   * 建立位元組陣列，並分配 `ByteArrayOutputStream` 位元組陣列的物件。
   * 叫用 `ByteArrayOutputStream` 物件 `toByteArray` 方法。
   * 建立 `com.adobe.idp.Document` 物件，方法是使用其建構子並傳遞位元組陣列。

1. 呈現預先填入的表單

   叫用 `FormsServiceClient` 物件 `renderPDFForm` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。
   * A `com.adobe.idp.Document` 包含要與表單合併資料的物件。 請確定您使用 `com.adobe.idp.Document` 在步驟一和步驟二中建立的物件。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流發送到客戶端web瀏覽器的對象。
   * 建立 `com.adobe.idp.Document` 對象，方法是調用 `FormsResult` 物件s `getOutputContent` 方法。
   * 建立 `java.io.InputStream` 對象，方法是調用 `com.adobe.idp.Document` 物件 `getInputStream` 方法。
   * 叫用 `InputStream` 物件 `read` 方法，並將位元組陣列傳遞為引數。
   * 叫用 `javax.servlet.ServletOutputStream` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。


**另請參閱**

[快速入門（SOAP模式）:使用Java API以可流式配置預填Forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API預先填入表單 {#prepopulating-forms-using-the-web-service-api}

若要使用Forms API（網站服務），以可流動的版面預先填入表單，請執行下列步驟：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。 (請參閱 [使用Apache Axis建立Java代理類](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * 將Java代理類包含到類路徑中。

1. 建立記憶體內XML資料源

   * 建立Java `DocumentBuilderFactory` 物件，方法是呼叫 `DocumentBuilderFactory` class `newInstance` 方法。
   * 建立Java `DocumentBuilder` 物件，方法是呼叫 `DocumentBuilderFactory` 物件 `newDocumentBuilder` 方法。
   * 呼叫 `DocumentBuilder` 物件 `newDocument` 實例化方法 `org.w3c.dom.Document` 物件。
   * 叫用 `org.w3c.dom.Document` 物件 `createElement` 方法。 這會建立 `Element` 代表根元素的物件。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，呼叫 `Document` 物件 `appendChild` 方法，並將根元素物件作為引數傳遞。 下列幾行程式碼會顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫 `Document` 物件 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，呼叫 `root` 物件 `appendChild` 方法，並將header元素物件作為引數傳遞。 附加到標題元素的XML元素對應於表單的靜態部分。 下列幾行程式碼會顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 呼叫 `Document` 物件 `createElement` 方法，並傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 接下來，呼叫子元素，以設定子元素的值 `appendChild` 方法，並傳遞 `Document` 物件 `createTextNode` 方法做為引數。 指定顯示為子元素值的字串值。 最後，呼叫標頭元素的 `appendChild` 方法，並將子元素物件作為引數傳遞。 以下幾行代碼顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 重複表單靜態部分中每個欄位的最後一個子步驟，將所有剩餘元素新增至標題元素（在XML資料來源圖表中，這些欄位顯示在A節中）。 [了解資料子組](#understanding-data-subgroups).)
   * 呼叫 `Document` 物件 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，呼叫 `root` 物件 `appendChild` 方法，並將detail元素物件作為引數傳遞。 附加到詳細元素的XML元素對應於表單的動態部分。 以下幾行代碼顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫 `Document` 物件 `createElement` 方法，並傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 接下來，呼叫子元素，以設定子元素的值 `appendChild` 方法，並傳遞 `Document` 物件 `createTextNode` 方法做為引數。 指定顯示為子元素值的字串值。 最後，呼叫詳細資料元素的 `appendChild` 方法，並將子元素物件作為引數傳遞。 以下幾行代碼顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加到詳細資訊元素。 要正確建立用於填充採購訂單表單的XML資料源，必須將以下XML元素附加到詳細資訊元素： `txtDescription`, `numQty`，和 `numUnitPrice`.
   * 對用於預先填入表單的所有資料項目，重複最後兩個子步驟。

1. 轉換XML資料源

   * 建立 `javax.xml.transform.Transformer` 對象，方法是調用 `javax.xml.transform.Transformer` 對象的靜態 `newInstance` 方法。
   * 建立 `Transformer` 對象，方法是調用 `TransformerFactory` 物件 `newTransformer` 方法。
   * 建立 `ByteArrayOutputStream` 物件，使用其建構子。
   * 建立 `javax.xml.transform.dom.DOMSource` 對象，使用其建構子並傳遞 `org.w3c.dom.Document` 在步驟1中建立的物件。
   * 建立 `javax.xml.transform.dom.DOMSource` 對象，使用其建構子並傳遞 `ByteArrayOutputStream` 物件。
   * 填入Java `ByteArrayOutputStream` 對象，方法是調用 `javax.xml.transform.Transformer` 物件 `transform` 方法和傳遞 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 對象。
   * 建立位元組陣列，並分配 `ByteArrayOutputStream` 位元組陣列的物件。
   * 叫用 `ByteArrayOutputStream` 物件 `toByteArray` 方法。
   * 建立 `BLOB` 對象，使用其建構子調用其 `setBinaryData` 方法，並傳遞位元組陣列。

1. 呈現預先填入的表單

   叫用 `FormsService` 物件 `renderPDFForm` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。
   * A `BLOB` 包含要與表單合併資料的物件。 請確定您使用 `BLOB` 在步驟1和步驟2中建立的物件。
   * A `PDFFormRenderSpecc` 儲存運行時選項的對象。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 由方法填入的物件。 這可用來儲存呈現的PDF表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 由方法填入的物件。 （此引數會以表單儲存頁數）。
   * 空白 `javax.xml.rpc.holders.StringHolder` 由方法填入的物件。 （此參數將儲存區域設定值）。
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   此 `renderPDFForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個引數值傳遞的物件，具有必須寫入用戶端網頁瀏覽器的表單資料流。

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件 `value` 資料成員。
   * 建立 `BLOB` 包含表單資料的物件，方法是叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得 `BLOB` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立位元組陣列，並叫用 `BLOB` 物件 `getBinaryData` 方法。 此任務分配 `FormsResult` 位元組陣列的物件。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

   >[!NOTE]
   >
   >此 `renderPDFForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個引數值傳遞的物件，具有必須寫入用戶端網頁瀏覽器的表單資料流。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
