---
title: 使用可排程的版面預先填入表單
seo-title: 使用可排程的版面預先填入表單
description: 'null'
seo-description: 'null'
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用可排程的版面預先填入表單 {#prepopulating-forms-with-flowable-layouts1}

## 使用可排程的版面預先填入表單 {#prepopulating-forms-with-flowable-layouts2}

預先填入表單會在轉譯的表單中向使用者顯示資料。 例如，假設使用者使用使用者名稱和密碼登入網站。 如果驗證成功，客戶端應用程式將查詢資料庫以獲取用戶資訊。 資料會合併到表單中，然後再將表單轉譯給使用者。 因此，用戶能夠在表單中查看個性化資料。

預先填入表單具有以下優點：

* 可讓使用者檢視表單中的自訂資料。
* 減少使用者填寫表單時的輸入量。
* 控制資料的放置位置，以確保資料的完整性。

下列兩個XML資料來源可預先填入表單：

* XDP資料來源，是符合XFA語法的XML（或XFDF資料，以預先填入使用Acrobat建立的表格）。
* 任意XML資料來源，包含與表單欄位名稱相符的名稱／值配對（本節中的範例使用任意XML資料來源）。

您要預先填入的每個表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不符，則會忽略它。 只要指定了所有XML元素，就不需要與XML元素的顯示順序匹配。

當您預先填入已包含資料的表單時，必須指定XML資料來源中已顯示的資料。 假設一個包含10個欄位的表單有4個欄位中的資料。 接下來，假設您要預先填入其餘6個欄位。 在這種情況下，您必須在用於預先填入表單的XML資料來源中指定10個XML元素。 如果您只指定6個元素，原始的4個欄位會是空的。

例如，您可以預先填入表單，例如範例確認表單。 (請參閱轉譯互動式PDF表單 [](/help/forms/developing/rendering-forms-rendering-forms-rendering-interactive-pdf-forms-rendering.md#rendering-interactive-pdf-forms-rendering)中的「確認表單」。)

若要預先填入範例確認表單，您必須建立一個XML資料來源，其中包含三個XML元素，這些元素會符合表單中的三個欄位。 此表單包含下列三個欄位： `FirstName`、 `LastName`和 `Amount`。 第一步是建立XML資料來源，其中包含與表單設計欄位相符的XML元素。 下一步是為XML元素指派資料值，如下列XML程式碼所示。

```as3
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

使用此XML資料來源預先填入確認表單，然後轉譯表單後，就會顯示您指派給XML元素的資料值，如下圖所示。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 使用可排列的版面預先填入表單 {#prepopulating_forms_with_flowable_layouts-1}

具有可排列版面的表單對於向使用者顯示未確定數量的資料非常有用。 由於表單的版面會自動調整為合併的資料量，因此您不需要預先決定表單的固定版面或頁數，就像使用固定版面的表單一樣。

表單通常會填入在執行時期取得的資料。 因此，您可以建立記憶體中的XML資料來源，並將資料直接放入記憶體中的XML資料來源，以預先填入表格。

考慮使用網路應用程式，例如線上商店。 線上購物者完成購買項目後，所有購買的項目都會放入記憶體內的XML資料來源中，以便預先填入表單。 下圖顯示了此過程，如圖後的表中所述。

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
   <td><p>使用者從線上商店購買商品。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>當使用者完成購買項目並按一下「提交」按鈕後，就會建立記憶體中的XML資料來源。 購買的項目和使用者資訊會放入記憶體中的XML資料來源。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML資料來源用於預先填入採購單表單（下表列出此表單的範例）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>採購訂單表單會轉譯至用戶端網頁瀏覽器。 </p></td>
  </tr>
 </tbody>
</table>

下圖顯示了採購訂單表單的示例。 表格中的資訊可以根據XML資料中的記錄數來調整。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>表單可以預先填入來自其他來源的資料，例如企業資料庫或外部應用程式。

### 表單設計考量 {#form-design-considerations}

具有可排列版面的表單，是以在設計人員中建立的表單設計為基礎。 表單設計指定一組版面配置、呈現和資料擷取規則，包括根據使用者輸入計算值。 當資料輸入表單時，就會套用規則。 新增至表單的欄位是表單設計中的子表單。 例如，在上圖中顯示的採購訂單表單中，每行都是子表單。 有關建立包含子表單的表單設計的資訊，請 [參閱建立具有可流式佈局的採購訂單表單](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9)。

### 瞭解資料子群組 {#understanding-data-subgroups}

XML資料來源可用來預先填入固定版面和可排列版面的表單。 但是，區別在於，使用可排程版面預先填入表單的XML資料來源包含重複的XML元素，這些元素會用來預先填入表單中重複的子表單。 這些重複的XML元素稱為資料子群組。

用於預填上圖中所示採購訂單表單的XML資料源包含四個重複資料子組。 每個資料子群組都對應於購買的項目。 購買的物品包括顯示器、台燈、電話和地址簿。

以下XML資料來源用於預先填入採購單表單。

```as3
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

請注意，每個資料子群組包含四個與此資訊對應的XML元素：

* 項目部件號
* 項目說明
* 項目數量
* 單價

資料子群組的父XML元素名稱必須與表單設計中的子表單名稱相符。 例如，在上圖中，請注意資料子群組的父XML元素名稱 `detail`。 這對應於採購訂單表單所基於的表單設計中的子表單的名稱。 如果資料子群組的父XML元素名稱與子表單不符，則不會預先填入伺服器端表單。

每個資料子群組都必須包含符合子表單欄位名稱的XML元素。 表 `detail` 單設計中的子表單包含下列欄位：

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>如果您嘗試使用包含重複XML元素的資料來源預先填入表單，並將選 `RenderAtClient` 項設 `No`為，則只會將第一個資料記錄合併到表單中。 為確保所有資料記錄都合併到表單中，請將設定 `RenderAtClient` 為 `Yes`。 如需選項的詳 `RenderAtClient` 細資訊，請 [參閱用戶端上的轉換表單](/help/forms/developing/rendering-forms-client.md)。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要預先填入可排程版面的表單，請執行下列工作：

1. 包含專案檔案。
1. 建立記憶體中的XML資料來源。
1. 轉換XML資料來源。
1. 演算預先填入的表單。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立記憶體中的XML資料來源**

您可以使用 `org.w3c.dom` 類別來建立記憶體內的XML資料來源，以預先填入具有可排列版面的表單。 您必須將資料放入符合表單的XML資料來源。 如需有可排列版面的表單與XML資料來源之間關係的詳細資訊，請參閱 [Understanding data sibroums](/help/forms/developing/rendering-forms-rendering-forms preming-forms-flowable-layouts-preming preming-forms-flowable-layouts-premipluepleuting.md#underpling.md#understanding-data-subroums.d.d.d-subroums)。

**轉換XML資料來源**

使用類建立的記憶體中XML資料源 `org.w3c.dom` 可以在用於預 `com.adobe.idp.Document` 填表單之前轉換為對象。 記憶體中的XML資料源可以使用Java XML轉換類進行轉換。

>[!NOTE]
>
>如果您使用Forms服務的WSDL來預先填入表單，則必須將物件 `org.w3c.dom.Document` 轉換為物 `BLOB` 件。

**演算預先填入的表單**

您會像轉換其他表格一樣，轉換預先填入的表格。 唯一的區別是，您使用包 `com.adobe.idp.Document` 含XML資料來源的物件來預先填入表單。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API預填表單 {#prepopulating-forms-using-the-java-api}

若要使用Forms API(Java)以可排程的版面預先填入表單，請執行下列步驟：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。 如需這些檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立記憶體中的XML資料來源

   * 通過調用類 `DocumentBuilderFactory` 的方法建立Java `DocumentBuilderFactory` 對 `newInstance` 像。
   * 呼叫物件 `DocumentBuilder` 的方法，以建 `DocumentBuilderFactory` 立Java物 `newDocumentBuilder` 件。
   * 呼叫物 `DocumentBuilder` 件的方 `newDocument` 法以實例化 `org.w3c.dom.Document` 物件。
   * 叫用物件的方法，以建立XML資料 `org.w3c.dom.Document` 來源的根元 `createElement` 素。 這會建立 `Element` 代表根元素的物件。 將表示元素名稱的字串值傳遞至方 `createElement` 法。 將返回值轉換為 `Element`。 接著，呼叫物件的方法，將根元素附 `Document` 加至文 `appendChild` 件，並將根元素物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫物件的方法，以建立XML資料 `Document` 來源的標題元 `createElement` 素。 將表示元素名稱的字串值傳遞至方 `createElement` 法。 將返回值轉換為 `Element`。 接著，呼叫物件的方法，將標題元素附加 `root` 至根元素 `appendChild` ，並將標題元素物件傳遞為引數。 附加到標題元素的XML元素對應於表單的靜態部分。 下列程式碼行會顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 呼叫物件的方法，以建立屬於標題元素的 `Document` 子項元 `createElement` 素，並傳遞代表元素名稱的字串值。 將返回值轉換為 `Element`。 接著，呼叫子項元素的方法來設定 `appendChild` 其值，並將物 `Document` 件的方法 `createTextNode` 傳遞為引數。 指定顯示為子元素值的字串值。 最後，呼叫標題元素的方法，將子項元素附加至標題元素， `appendChild` 並將子項元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 重複表格靜態部分（在XML資料來源圖中，這些欄位如A節所示）中每個欄位的最後一個子步驟，將所有剩餘的元素新增至標題元素。(請參 [閱瞭解資料子群組](#understanding-data-subgroups)。)
   * 呼叫物件的方法，以建立XML資料來源 `Document` 的詳細資 `createElement` 料。 將表示元素名稱的字串值傳遞至方 `createElement` 法。 將返回值轉換為 `Element`。 接著，呼叫物件的方法，將詳細資料元素附加 `root` 至根元素 `appendChild` ，並將詳細資料元素物件傳遞為引數。 附加到細節元素的XML元素對應於表單的動態部分。 下列程式碼行會顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫物件的方法，以建立屬於詳細資料元素的 `Document` 子項元 `createElement` 素，並傳遞代表元素名稱的字串值。 將返回值轉換為 `Element`。 接著，呼叫子項元素的方法來設定 `appendChild` 其值，並將物 `Document` 件的方法 `createTextNode` 傳遞為引數。 指定顯示為子元素值的字串值。 最後，呼叫詳細資料元素的方法，將子項元素附加至詳細資料元素， `appendChild` 並將子項元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加至詳細資料元素。 要正確建立用於填充採購訂單表單的XML資料源，您必須將以下XML元素附加到詳細資訊元素： `txtDescription`、 `numQty`和 `numUnitPrice`。
   * 對用於預先填入表單的所有資料項目，重複最後兩個子步驟。

1. 轉換XML資料來源

   * 調用 `javax.xml.transform.Transformer` 物件的靜態方 `javax.xml.transform.Transformer` 法來建立物 `newInstance` 件。
   * 調用 `Transformer` 物件的方 `TransformerFactory` 法以建立物 `newTransformer` 件。
   * 使用其 `ByteArrayOutputStream` 建構函式建立物件。
   * 使用 `javax.xml.transform.dom.DOMSource` 其建構函式並傳遞步驟1中建 `org.w3c.dom.Document` 立的物件，以建立物件。
   * 使用其 `javax.xml.transform.dom.DOMSource` 建構函式並傳遞物件，以建立物 `ByteArrayOutputStream` 件。
   * 調用物 `ByteArrayOutputStream` 件的方法並傳 `javax.xml.transform.Transformer` 遞物件和物件，以填 `transform` 入Java物 `javax.xml.transform.dom.DOMSource``javax.xml.transform.stream.StreamResult` 件。
   * 建立位元組陣列並將對象的大 `ByteArrayOutputStream` 小分配給位元組陣列。
   * 調用物件的方法，以填 `ByteArrayOutputStream` 入位元組 `toByteArray` 陣列。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞位元組陣列，以建立物件。

1. 演算預先填入的表單

   叫用物 `FormsServiceClient` 件的方 `renderPDFForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。
   * 包 `com.adobe.idp.Document` 含要與表單合併的資料的對象。 請確定您使用步驟 `com.adobe.idp.Document` 一和步驟二中建立的物件。
   * 存 `PDFFormRenderSpec` 儲運行時選項的對象。
   * 包 `URLSpec` 含Forms服務所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
   該方 `renderPDFForm` 法返回包 `FormsResult` 含必須寫入客戶端Web瀏覽器的表單資料流的對象。

   * 建立用 `javax.servlet.ServletOutputStream` 於傳送表單資料串流至用戶端網頁瀏覽器的物件。
   * 通過調 `com.adobe.idp.Document` 用對象的方法 `FormsResult` 建立對 `getOutputContent` 像。
   * 調用 `java.io.InputStream` 物件的方 `com.adobe.idp.Document` 法以建立物 `getInputStream` 件。
   * 呼叫物件的方法，並將位元組陣列傳 `InputStream` 入為引數， `read` 以表格資料流的方式建立位元組陣列。
   * 叫用物 `javax.servlet.ServletOutputStream` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。


**另請參閱**

[快速入門（SOAP模式）:使用Java API將可排程的版面預先填入表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API預填表單 {#prepopulating-forms-using-the-web-service-api}

若要使用Forms API(web service)以可排程的版面預先填入表單，請執行下列步驟：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。 (請參 [閱使用Apache Axis建立Java代理類](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)。)
   * 將Java代理類包含到類路徑中。

1. 建立記憶體中的XML資料來源

   * 通過調用類 `DocumentBuilderFactory` 的方法建立Java `DocumentBuilderFactory` 對 `newInstance` 像。
   * 呼叫物件 `DocumentBuilder` 的方法，以建 `DocumentBuilderFactory` 立Java物 `newDocumentBuilder` 件。
   * 呼叫物 `DocumentBuilder` 件的方 `newDocument` 法以實例化 `org.w3c.dom.Document` 物件。
   * 叫用物件的方法，以建立XML資料 `org.w3c.dom.Document` 來源的根元 `createElement` 素。 這會建立 `Element` 代表根元素的物件。 將表示元素名稱的字串值傳遞至方 `createElement` 法。 將返回值轉換為 `Element`。 接著，呼叫物件的方法，將根元素附 `Document` 加至文 `appendChild` 件，並將根元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫物件的方法，以建立XML資料 `Document` 來源的標題元 `createElement` 素。 將表示元素名稱的字串值傳遞至方 `createElement` 法。 將返回值轉換為 `Element`。 接著，呼叫物件的方法，將標題元素附加 `root` 至根元素 `appendChild` ，並將標題元素物件傳遞為引數。 附加到標題元素的XML元素對應於表單的靜態部分。 下列程式碼行會顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 呼叫物件的方法，以建立屬於標題元素的 `Document` 子項元 `createElement` 素，並傳遞代表元素名稱的字串值。 將返回值轉換為 `Element`。 接著，呼叫子項元素的方法來設定 `appendChild` 其值，並將物 `Document` 件的方法 `createTextNode` 傳遞為引數。 指定顯示為子元素值的字串值。 最後，呼叫標題元素的方法，將子項元素附加至標題元素， `appendChild` 並將子項元素物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 重複表格靜態部分（在XML資料來源圖中，這些欄位如A節所示）中每個欄位的最後一個子步驟，將所有剩餘的元素新增至標題元素。(請參 [閱瞭解資料子群組](#understanding-data-subgroups)。)
   * 呼叫物件的方法，以建立XML資料來源 `Document` 的詳細資 `createElement` 料。 將表示元素名稱的字串值傳遞至方 `createElement` 法。 將返回值轉換為 `Element`。 接著，呼叫物件的方法，將詳細資料元素附加 `root` 至根元素 `appendChild` ，並將詳細資料元素物件傳遞為引數。 附加到細節元素的XML元素對應於表單的動態部分。 下列程式碼行顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫物件的方法，以建立屬於詳細資料元素的 `Document` 子項元 `createElement` 素，並傳遞代表元素名稱的字串值。 將返回值轉換為 `Element`。 接著，呼叫子項元素的方法來設定 `appendChild` 其值，並將物 `Document` 件的方法 `createTextNode` 傳遞為引數。 指定顯示為子元素值的字串值。 最後，呼叫詳細資料元素的方法，將子項元素附加至詳細資料元素， `appendChild` 並將子項元素物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加至詳細資料元素。 要正確建立用於填充採購訂單表單的XML資料源，您必須將以下XML元素附加到詳細資訊元素： `txtDescription`、 `numQty`和 `numUnitPrice`。
   * 對用於預先填入表單的所有資料項目，重複最後兩個子步驟。

1. 轉換XML資料來源

   * 調用 `javax.xml.transform.Transformer` 物件的靜態方 `javax.xml.transform.Transformer` 法來建立物 `newInstance` 件。
   * 調用 `Transformer` 物件的方 `TransformerFactory` 法以建立物 `newTransformer` 件。
   * 使用其 `ByteArrayOutputStream` 建構函式建立物件。
   * 使用 `javax.xml.transform.dom.DOMSource` 其建構函式並傳遞步驟1中建 `org.w3c.dom.Document` 立的物件，以建立物件。
   * 使用其 `javax.xml.transform.dom.DOMSource` 建構函式並傳遞物件，以建立物 `ByteArrayOutputStream` 件。
   * 調用物 `ByteArrayOutputStream` 件的方法並傳 `javax.xml.transform.Transformer` 遞物件和物件，以填 `transform` 入Java物 `javax.xml.transform.dom.DOMSource``javax.xml.transform.stream.StreamResult` 件。
   * 建立位元組陣列並將對象的大 `ByteArrayOutputStream` 小分配給位元組陣列。
   * 調用物件的方法，以填 `ByteArrayOutputStream` 入位元組 `toByteArray` 陣列。
   * 使用其 `BLOB` 建構函式建立物件，並叫用其方 `setBinaryData` 法並傳遞位元組陣列。

1. 演算預先填入的表單

   叫用物 `FormsService` 件的方 `renderPDFForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。
   * 包 `BLOB` 含要與表單合併的資料的對象。 請確定您使用 `BLOB` 在步驟1和步驟2中建立的物件。
   * 存 `PDFFormRenderSpecc` 儲運行時選項的對象。 如需詳細資訊，請參 [閱「AEM Forms API參考」](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 包 `URLSpec` 含Forms服務所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空對象。 這可用來儲存轉譯的PDF表單。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空對象。 （此引數將儲存表單中的頁數）。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空對象。 （此引數將儲存地區值）。
   * 包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作結果的空對象。
   該方 `renderPDFForm` 法用必 `com.adobe.idp.services.holders.FormsResultHolder` 須寫入客戶端Web瀏覽器的表單資料流填充作為最後一個參數值傳遞的對象。

   * 獲取 `FormResult` 對象資料成員的 `com.adobe.idp.services.holders.FormsResultHolder` 值以建立 `value` 對象。
   * 呼叫 `BLOB` 物件的方法，以建立包含表 `FormsResult` 單資料的物 `getOutputContent` 件。
   * 通過調用對象的方 `BLOB` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `BLOB` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 建立位元組陣列，並透過叫用物件的方 `BLOB` 法來填入該 `getBinaryData` 陣列。 此任務將對象的內 `FormsResult` 容分配給位元組陣列。
   * 叫用物 `javax.servlet.http.HttpServletResponse` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。
   >[!NOTE]
   >
   >該方 `renderPDFForm` 法用必 `com.adobe.idp.services.holders.FormsResultHolder` 須寫入客戶端Web瀏覽器的表單資料流填充作為最後一個參數值傳遞的對象。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

