---
title: 用可流式佈局預填充Forms
seo-title: Prepopulating Forms with Flowable Layouts
description: 使用可流式佈局預填充表單，以使用Java API和Web服務API向呈現表單中的用戶顯示資料。
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

# 用可流式佈局預填充Forms {#prepopulating-forms-with-flowable-layouts1}

## 用可流式佈局預填充Forms {#prepopulating-forms-with-flowable-layouts2}

預填充表單將向呈現表單中的用戶顯示資料。 例如，假定用戶使用用戶名和密碼登錄到網站。 如果驗證成功，則客戶端應用程式查詢資料庫以獲取用戶資訊。 將資料合併到表單中，然後將表單呈現給用戶。 結果，用戶能夠查看表單內的個性化資料。

預填充表單具有以下優點：

* 允許用戶查看表單中的自定義資料。
* 減少用戶填寫表單時鍵入的內容量。
* 通過控制資料的放置位置來確保資料完整性。

以下兩個XML資料源可以預填充表單：

* XDP資料源，它是符合XFA語法的XML(或XFDF資料，用於預填充使用Acrobat建立的表單)。
* 一個任意XML資料源，包含與表單的欄位名稱匹配的名稱/值對（本節中的示例使用任意XML資料源）。

要預填充的每個表單域都必須存在XML元素。 XML元素名稱必須與欄位名稱匹配。 如果XML元素與表單域不對應，或XML元素名稱與欄位名稱不匹配，則忽略該元素。 只要指定了所有XML元素，就不必與XML元素的顯示順序匹配。

預填充已包含資料的表單時，必須指定XML資料源中已顯示的資料。 假定包含10個欄位的表單有四個欄位中的資料。 接下來，假定要預填充其餘六個欄位。 在這種情況下，必須在用於預填充表單的XML資料源中指定10個XML元素。 如果僅指定六個元素，則原始的四個欄位為空。

例如，您可以預填充表單，如示例確認表單。 (請參閱中的「確認表」 [呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)。)

要預填充示例確認表單，必須建立一個XML資料源，該資料源包含三個與表單中三個欄位匹配的XML元素。 此表單包含以下三個欄位： `FirstName`。 `LastName`, `Amount`。 第一步是建立一個XML資料源，該資料源包含與表單設計中的欄位匹配的XML元素。 下一步是為XML元素分配資料值，如以下XML代碼所示。

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

使用此XML資料源預填充確認表單並再次呈現表單後，將顯示分配給XML元素的資料值，如下圖所示。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 用可流式佈局預填充表單 {#prepopulating_forms_with_flowable_layouts-1}

具有可流動佈局的Forms對於向用戶顯示未確定數量的資料非常有用。 由於表單的佈局會自動調整為合併的資料量，因此您不需要預先確定表單的固定佈局或頁數，因為您需要對具有固定佈局的表單進行操作。

表單通常填充有在運行時獲得的資料。 因此，您可以通過建立記憶體中XML資料源並將資料直接放入記憶體中XML資料源來預填充表單。

考慮基於Web的應用程式，如線上商店。 線上購物者完成購買物品後，所有購買的物品都放入記憶體中的XML資料源中，該資料源用於預填充表單。 下圖顯示了此過程，如圖後的表中所述。

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

下表介紹了此圖中的步驟。

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
   <td><p>用戶從基於Web的線上商店購買項目。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用戶完成採購項目並按一下「提交」按鈕後，將建立記憶體中的XML資料源。 購買的項目和用戶資訊被放入記憶體中的XML資料源。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML資料源用於預填充採購訂單表單（下表顯示了此表單的示例）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>採購訂單表單將呈現給客戶端Web瀏覽器。 </p></td>
  </tr>
 </tbody>
</table>

下圖顯示了採購訂單表單的示例。 表中的資訊可以根據XML資料中的記錄數進行調整。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>表單可以預先填充來自其它源的資料，如企業資料庫或外部應用程式。

### 窗體設計注意事項 {#form-design-considerations}

Forms具有可流動佈局，它基於在設計器中建立的窗體設計。 表單設計指定一組佈局、呈現和資料捕獲規則，包括基於用戶輸入計算值。 當資料輸入到表單中時，將應用規則。 添加到表單的欄位是表單設計中的子表單。 例如，在上圖所示的採購訂單表單中，每行都是子表單。 有關建立包含子表單的表單設計的資訊，請參見 [建立具有可流式佈局的採購訂單窗體](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9)。

### 瞭解資料子組 {#understanding-data-subgroups}

XML資料源用於用固定佈局和可流式佈局預填充表單。 但是，區別在於，用可流式佈局預填充表單的XML資料源包含用於預填充表單內重複的子表單的重複XML元素。 這些重複的XML元素稱為資料子組。

用於預填充上圖中顯示的採購訂單表單的XML資料源包含四個重複資料子組。 每個資料子組對應於採購的物料。 購買的物品包括顯示器、台燈、電話和通訊簿。

以下XML資料源用於預填充採購訂單表單。

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
* 物料說明
* 物料數量
* 單價

資料子組的父XML元素的名稱必須與窗體設計中子窗體的名稱匹配。 例如，在上一圖中，請注意資料子組的父XML元素的名稱是 `detail`。 這對應於採購訂單表單所基於的表單設計中的子表單的名稱。 如果資料子組的父XML元素的名稱與子表單不匹配，則不會預填充伺服器端表單。

每個資料子組必須包含與子表單中的欄位名稱匹配的XML元素。 的 `detail` 窗體設計中的子窗體包含以下欄位：

* txtPartNum
* txt描述
* 數量
* 數單價

>[!NOTE]
>
>如果嘗試使用包含重複XML元素的資料源預填充表單，並設定 `RenderAtClient` 選項 `No`，只將第一個資料記錄合併到窗體中。 要確保所有資料記錄都合併到表單中，請設定 `RenderAtClient` 至 `Yes`。 有關 `RenderAtClient` 選項，請參閱 [在客戶端呈現Forms](/help/forms/developing/rendering-forms-client.md)。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要使用可流式佈局預填充表單，請執行以下任務：

1. 包括項目檔案。
1. 建立記憶體中的XML資料源。
1. 轉換XML資料源。
1. 呈現預填充的窗體。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立記憶體中的XML資料源**

您可以使用 `org.w3c.dom` 類，建立記憶體中的XML資料源，以使用可流式佈局預填充表單。 必須將資料放入符合表單的XML資料源中。 有關具有可流式佈局的表單與XML資料源之間關係的資訊，請參見 [瞭解資料子組](#understanding-data-subgroups)。

**轉換XML資料源**

使用 `org.w3c.dom` 類可轉換為 `com.adobe.idp.Document` 對象，然後再將其用於預填充窗體。 記憶體中的XML資料源可以使用Java XML轉換類進行轉換。

>[!NOTE]
>
>如果使用Forms服務的WSDL預填充表單，則必須轉換 `org.w3c.dom.Document` 對象 `BLOB` 的雙曲餘切值。

**呈現預填充窗體**

您會像其他窗體一樣呈現預填充窗體。 唯一的區別是 `com.adobe.idp.Document` 包含要預填充表單的XML資料源的對象。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API預填充表單 {#prepopulating-forms-using-the-java-api}

要使用FormsAPI(Java)預填充可流式佈局的表單，請執行以下步驟：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。 有關這些檔案位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立記憶體中的XML資料源

   * 建立Java `DocumentBuilderFactory` 通過調用 `DocumentBuilderFactory` 類 `newInstance` 的雙曲餘切值。
   * 建立Java `DocumentBuilder` 通過調用 `DocumentBuilderFactory` 對象 `newDocumentBuilder` 的雙曲餘切值。
   * 呼叫 `DocumentBuilder` 對象 `newDocument` 實例化方法 `org.w3c.dom.Document` 的雙曲餘切值。
   * 通過調用XML資料源的根元素 `org.w3c.dom.Document` 對象 `createElement` 的雙曲餘切值。 這將建立 `Element` 表示根元素的對象。 將表示元素名稱的字串值傳遞到 `createElement` 的雙曲餘切值。 將返回值強制轉換為 `Element`。 接下來，通過調用 `Document` 對象 `appendChild` 方法，並將根元素對象作為參數傳遞。 以下代碼行顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 通過調用 `Document` 對象 `createElement` 的雙曲餘切值。 將表示元素名稱的字串值傳遞到 `createElement` 的雙曲餘切值。 將返回值強制轉換為 `Element`。 接下來，通過調用 `root` 對象 `appendChild` 方法，並將header元素對象作為參數傳遞。 附加到頭元素的XML元素對應於表單的靜態部分。 以下代碼行顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 通過調用 `Document` 對象 `createElement` 方法，並傳遞表示元素名稱的字串值。 將返回值強制轉換為 `Element`。 接下來，通過調用子元素的值來設定其值 `appendChild` 方法，並通過 `Document` 對象 `createTextNode` 方法作為參數。 指定顯示為子元素值的字串值。 最後，通過調用標頭元素的 `appendChild` 方法，並將子元素對象作為參數傳遞。 以下代碼行顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 通過重複表單靜態部分中顯示的每個欄位的最後一個子步驟（在XML資料源圖中，這些欄位在A節中顯示），將所有剩餘元素添加到頭元素。(請參閱 [瞭解資料子組](#understanding-data-subgroups)。)
   * 通過調用 `Document` 對象 `createElement` 的雙曲餘切值。 將表示元素名稱的字串值傳遞到 `createElement` 的雙曲餘切值。 將返回值強制轉換為 `Element`。 接下來，通過調用 `root` 對象 `appendChild` 方法，並將detail元素對象作為參數傳遞。 附加到細節元素的XML元素對應於表單的動態部分。 以下代碼行顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 通過調用 `Document` 對象 `createElement` 方法，並傳遞表示元素名稱的字串值。 將返回值強制轉換為 `Element`。 接下來，通過調用子元素的值來設定其值 `appendChild` 方法，並通過 `Document` 對象 `createTextNode` 方法作為參數。 指定顯示為子元素值的字串值。 最後，通過調用詳細資訊元素的 `appendChild` 方法，並將子元素對象作為參數傳遞。 以下代碼行顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對要追加到詳細資訊元素的所有XML元素重複最後一個子步驟。 要正確建立用於填充採購訂單表單的XML資料源，您必須將以下XML元素附加到詳細資訊元素： `txtDescription`。 `numQty`, `numUnitPrice`。
   * 對用於預填充表單的所有資料項重複最後兩個子步驟。

1. 轉換XML資料源

   * 建立 `javax.xml.transform.Transformer` 通過調用 `javax.xml.transform.Transformer` 對象的靜態 `newInstance` 的雙曲餘切值。
   * 建立 `Transformer` 通過調用 `TransformerFactory` 對象 `newTransformer` 的雙曲餘切值。
   * 建立 `ByteArrayOutputStream` 對象。
   * 建立 `javax.xml.transform.dom.DOMSource` 使用其建構子並傳遞對象 `org.w3c.dom.Document` 在步驟1中建立的對象。
   * 建立 `javax.xml.transform.dom.DOMSource` 使用其建構子並傳遞對象 `ByteArrayOutputStream` 的雙曲餘切值。
   * 填充Java `ByteArrayOutputStream` 通過調用 `javax.xml.transform.Transformer` 對象 `transform` 方法和傳遞 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 對象。
   * 建立位元組陣列並分配 `ByteArrayOutputStream` 對象。
   * 通過調用 `ByteArrayOutputStream` 對象 `toByteArray` 的雙曲餘切值。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞位元組陣列。

1. 呈現預填充窗體

   調用 `FormsServiceClient` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 確保使用 `com.adobe.idp.Document` 在步驟1和步驟2中建立的對象。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

   的 `renderPDFForm` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流發送到客戶端web瀏覽器的對象。
   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read` 方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。


**另請參閱**

[快速啟動（SOAP模式）:使用Java API使用可流式佈局預填充Forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API預填充表單 {#prepopulating-forms-using-the-web-service-api}

要使用FormsAPI（Web服務）預填充可流式佈局的表單，請執行以下步驟：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。 (請參閱 [使用Apache軸建立Java代理類](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)。)
   * 將Java代理類包括到類路徑中。

1. 建立記憶體中的XML資料源

   * 建立Java `DocumentBuilderFactory` 通過調用 `DocumentBuilderFactory` 類 `newInstance` 的雙曲餘切值。
   * 建立Java `DocumentBuilder` 通過調用 `DocumentBuilderFactory` 對象 `newDocumentBuilder` 的雙曲餘切值。
   * 呼叫 `DocumentBuilder` 對象 `newDocument` 實例化方法 `org.w3c.dom.Document` 的雙曲餘切值。
   * 通過調用XML資料源的根元素 `org.w3c.dom.Document` 對象 `createElement` 的雙曲餘切值。 這將建立 `Element` 表示根元素的對象。 將表示元素名稱的字串值傳遞到 `createElement` 的雙曲餘切值。 將返回值強制轉換為 `Element`。 接下來，通過調用 `Document` 對象 `appendChild` 方法，並將根元素對象作為參數傳遞。 以下代碼行顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 通過調用 `Document` 對象 `createElement` 的雙曲餘切值。 將表示元素名稱的字串值傳遞到 `createElement` 的雙曲餘切值。 將返回值強制轉換為 `Element`。 接下來，通過調用 `root` 對象 `appendChild` 方法，並將header元素對象作為參數傳遞。 附加到頭元素的XML元素對應於表單的靜態部分。 以下代碼行顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 通過調用 `Document` 對象 `createElement` 方法，並傳遞表示元素名稱的字串值。 將返回值強制轉換為 `Element`。 接下來，通過調用子元素的值來設定其值 `appendChild` 方法，並通過 `Document` 對象 `createTextNode` 方法作為參數。 指定顯示為子元素值的字串值。 最後，通過調用標頭元素的 `appendChild` 方法，並將子元素對象作為參數傳遞。 以下代碼行顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 通過重複表單靜態部分中顯示的每個欄位的最後一個子步驟（在XML資料源圖中，這些欄位在A節中顯示），將所有剩餘元素添加到頭元素。(請參閱 [瞭解資料子組](#understanding-data-subgroups)。)
   * 通過調用 `Document` 對象 `createElement` 的雙曲餘切值。 將表示元素名稱的字串值傳遞到 `createElement` 的雙曲餘切值。 將返回值強制轉換為 `Element`。 接下來，通過調用 `root` 對象 `appendChild` 方法，並將detail元素對象作為參數傳遞。 附加到細節元素的XML元素對應於表單的動態部分。 以下代碼行顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 通過調用 `Document` 對象 `createElement` 方法，並傳遞表示元素名稱的字串值。 將返回值強制轉換為 `Element`。 接下來，通過調用子元素的值來設定其值 `appendChild` 方法，並通過 `Document` 對象 `createTextNode` 方法作為參數。 指定顯示為子元素值的字串值。 最後，通過調用詳細資訊元素的 `appendChild` 方法，並將子元素對象作為參數傳遞。 以下代碼行顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對要追加到詳細資訊元素的所有XML元素重複最後一個子步驟。 要正確建立用於填充採購訂單表單的XML資料源，您必須將以下XML元素附加到詳細資訊元素： `txtDescription`。 `numQty`, `numUnitPrice`。
   * 對用於預填充表單的所有資料項重複最後兩個子步驟。

1. 轉換XML資料源

   * 建立 `javax.xml.transform.Transformer` 通過調用 `javax.xml.transform.Transformer` 對象的靜態 `newInstance` 的雙曲餘切值。
   * 建立 `Transformer` 通過調用 `TransformerFactory` 對象 `newTransformer` 的雙曲餘切值。
   * 建立 `ByteArrayOutputStream` 對象。
   * 建立 `javax.xml.transform.dom.DOMSource` 使用其建構子並傳遞對象 `org.w3c.dom.Document` 在步驟1中建立的對象。
   * 建立 `javax.xml.transform.dom.DOMSource` 使用其建構子並傳遞對象 `ByteArrayOutputStream` 的雙曲餘切值。
   * 填充Java `ByteArrayOutputStream` 通過調用 `javax.xml.transform.Transformer` 對象 `transform` 方法和傳遞 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 對象。
   * 建立位元組陣列並分配 `ByteArrayOutputStream` 對象。
   * 通過調用 `ByteArrayOutputStream` 對象 `toByteArray` 的雙曲餘切值。
   * 建立 `BLOB` 對象使用其建構子調用其 `setBinaryData` 方法並傳遞位元組陣列。

1. 呈現預填充窗體

   調用 `FormsService` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。
   * A `BLOB` 包含要與窗體合併的資料的對象。 確保使用 `BLOB` 在步驟1和步驟2中建立的對象。
   * A `PDFFormRenderSpecc` 儲存運行時選項的對象。 有關詳細資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的對象。 這用於儲存渲染的PDF窗體。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的對象。 （此參數將儲存表單中的頁數）。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。 （此參數將儲存區域設定值）。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   的 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個參數值傳遞的對象，其表單資料流必須寫入客戶端web瀏覽器。

   * 建立 `FormResult` 通過獲取 `com.adobe.idp.services.holders.FormsResultHolder` 對象 `value` 資料成員。
   * 建立 `BLOB` 通過調用包含表單資料的對象 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `BLOB` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `BLOB` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立位元組陣列，並通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。 此任務分配 `FormsResult` 對象。
   * 調用 `javax.servlet.http.HttpServletResponse` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

   >[!NOTE]
   >
   >的 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個參數值傳遞的對象，其表單資料流必須寫入客戶端web瀏覽器。

**另請參閱**

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
