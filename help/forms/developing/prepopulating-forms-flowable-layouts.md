---
title: 使用可排程的版面預先填入Forms
seo-title: 使用可排程的版面預先填入Forms
description: 使用可排列的版面預先填入表單，以使用Java API和Web服務API，在轉譯表單中向使用者顯示資料。
seo-description: 使用可排列的版面預先填入表單，以使用Java API和Web服務API，在轉譯表單中向使用者顯示資料。
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3534'
ht-degree: 0%

---


# 使用可排列的版面預先填入Forms{#prepopulating-forms-with-flowable-layouts1}

## 使用可排列的版面預先填入Forms{#prepopulating-forms-with-flowable-layouts2}

預先填入表單會在轉譯的表單中向使用者顯示資料。 例如，假設使用者使用使用者名稱和密碼登入網站。 如果驗證成功，客戶端應用程式將查詢資料庫以獲取用戶資訊。 資料會合併到表單中，然後再將表單轉譯給使用者。 因此，用戶能夠在表單中查看個性化資料。

預先填入表單具有以下優點：

* 可讓使用者檢視表單中的自訂資料。
* 減少使用者填寫表單時的輸入量。
* 控制資料的放置位置，以確保資料的完整性。

下列兩個XML資料來源可預先填入表單：

* XDP資料來源，是符合XFA語法的XML(或XFDF資料，以預先填入使用Acrobat建立的表格)。
* 任意XML資料來源，包含與表單欄位名稱相符的名稱／值配對（本節中的範例使用任意XML資料來源）。

您要預先填入的每個表單欄位都必須有XML元素。 XML元素名稱必須與欄位名稱相符。 如果XML元素與表單欄位不對應，或XML元素名稱與欄位名稱不符，則會忽略它。 只要指定了所有XML元素，就不需要與XML元素的顯示順序匹配。

當您預先填入已包含資料的表單時，必須指定XML資料來源中已顯示的資料。 假設一個包含10個欄位的表單有4個欄位中的資料。 接下來，假設您要預先填入其餘6個欄位。 在這種情況下，您必須在XML資料來源中指定10個XML元素，以便預先填入表單。 如果您只指定6個元素，原始的4個欄位會是空的。

例如，您可以預先填入表單，例如範例確認表單。 (請參閱[演算互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)中的「確認表單」。)

若要預先填入範例確認表單，您必須建立一個XML資料來源，其中包含三個XML元素，這些元素會符合表單中的三個欄位。 此表單包含下列三個欄位：`FirstName`、`LastName`和`Amount`。 第一步是建立XML資料來源，其中包含與表單設計欄位相符的XML元素。 下一步是為XML元素指派資料值，如下列XML程式碼所示。

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

使用此XML資料來源預先填入確認表單，然後轉譯表單後，就會顯示您指派給XML元素的資料值，如下圖所示。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 預先填入可排列版面的表格{#prepopulating_forms_with_flowable_layouts-1}

具有可排列版面的Forms對於向使用者顯示未確定的資料量非常有用。 由於表單的版面會自動調整為合併的資料量，因此您不需要預先決定表單的固定版面或頁數，就像使用固定版面的表單一樣。

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

### 表單設計注意事項{#form-design-considerations}

Forms的可排列版面是以在Designer中建立的表單設計為基礎。 表單設計指定一組版面配置、呈現和資料擷取規則，包括根據使用者輸入計算值。 當資料輸入表單時，就會套用規則。 新增至表單的欄位是表單設計中的子表單。 例如，在上圖中顯示的採購訂單表單中，每行都是子表單。 有關建立包含子表單的表單設計的資訊，請參閱[建立具有可流式佈局的採購訂單表單。](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9)

### 瞭解資料子群組{#understanding-data-subgroups}

XML資料來源可用來預先填入固定版面和可排列版面的表單。 但是，區別在於，預先填入可排列版面的XML資料來源包含重複的XML元素，這些元素會用來預先填入在表單中重複的子表單。 這些重複的XML元素稱為資料子群組。

用於預填上圖中所示採購訂單表單的XML資料源包含四個重複資料子組。 每個資料子群組都對應於購買的項目。 購買的物品包括顯示器、台燈、電話和地址簿。

以下XML資料來源用於預先填入採購單表單。

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

請注意，每個資料子群組包含四個與此資訊對應的XML元素：

* 項目部件號
* 項目說明
* 項目數量
* 單價

資料子群組的父XML元素名稱必須與表單設計中的子表單名稱相符。 例如，在上圖中，請注意資料子群組的父XML元素名稱為`detail`。 這對應於採購訂單表單所基於的表單設計中的子表單的名稱。 如果資料子群組的父XML元素名稱與子表單不符，則不會預先填入伺服器端表單。

每個資料子群組都必須包含符合子表單欄位名稱的XML元素。 表單設計中的`detail`子表單包含下列欄位：

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>如果您嘗試預先填入包含重複XML元素的資料來源的表單，並將`RenderAtClient`選項設為`No`，則只會將第一個資料記錄合併到表單中。 為確保所有資料記錄都合併到表單中，請將`RenderAtClient`設定為`Yes`。 有關`RenderAtClient`選項的資訊，請參見Client](/help/forms/developing/rendering-forms-client.md)上的[ RenderingForms。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

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

您可以使用`org.w3c.dom`類別來建立記憶體中的XML資料來源，以預先填入具有可排列版面的表單。 您必須將資料放入符合表單的XML資料來源。 有關具有可流式佈局的表單與XML資料源之間關係的資訊，請參閱[瞭解資料子組](#understanding-data-subgroups)。

**轉換XML資料來源**

使用`org.w3c.dom`類建立的記憶體中XML資料源可以轉換為`com.adobe.idp.Document`對象，然後再用於預填充表單。 記憶體中的XML資料源可以使用Java XML轉換類進行轉換。

>[!NOTE]
>
>如果您使用Forms服務的WSDL來預先填入表單，您必須將`org.w3c.dom.Document`物件轉換為`BLOB`物件。

**演算預先填入的表單**

您會像轉換其他表格一樣，轉換預先填入的表格。 唯一的區別是，您使用包含XML資料來源的`com.adobe.idp.Document`物件來預先填入表單。

**另請參閱**

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉換互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#prepopulating-forms-using-the-java-api}預填表單

若要使用FormsAPI(Java)預先填入具有可排程版面的表單，請執行下列步驟：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。 有關這些檔案位置的資訊，請參見[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 建立記憶體中的XML資料來源

   * 通過調用`DocumentBuilderFactory`類`newInstance`方法建立Java `DocumentBuilderFactory`對象。
   * 呼叫`DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立Java `DocumentBuilder`物件。
   * 呼叫`DocumentBuilder`物件的`newDocument`方法，以實例化`org.w3c.dom.Document`物件。
   * 呼叫`org.w3c.dom.Document`物件的`createElement`方法，以建立XML資料來源的根元素。 這會建立代表根元素的`Element`物件。 將表示元素名稱的字串值傳遞至`createElement`方法。 將返回值轉換為`Element`。 接著，呼叫`Document`物件的`appendChild`方法，將根元素附加至檔案，並將根元素物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫`Document`物件的`createElement`方法，以建立XML資料來源的標題元素。 將表示元素名稱的字串值傳遞至`createElement`方法。 將返回值轉換為`Element`。 接著，呼叫`root`物件的`appendChild`方法，將標題元素附加至根元素，並將標題元素物件傳遞為引數。 附加到標題元素的XML元素對應於表單的靜態部分。 下列程式碼行會顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 呼叫`Document`物件的`createElement`方法，建立屬於標題元素的子元素，並傳遞代表元素名稱的字串值。 將返回值轉換為`Element`。 接著，呼叫其`appendChild`方法來設定子元素的值，並將`Document`物件的`createTextNode`方法傳遞為引數。 指定顯示為子元素值的字串值。 最後，呼叫標題元素的`appendChild`方法，將子元素附加至標題元素，並將子元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 重複表格靜態部分（在XML資料來源圖中，這些欄位如A節所示）中每個欄位的最後一個子步驟，將所有剩餘的元素新增至標題元素。（請參閱[瞭解資料子群組](#understanding-data-subgroups)。）
   * 呼叫`Document`物件的`createElement`方法，以建立XML資料來源的詳細資料元素。 將表示元素名稱的字串值傳遞至`createElement`方法。 將返回值轉換為`Element`。 接著，呼叫`root`物件的`appendChild`方法，將詳細資料元素附加至根元素，並將詳細資料元素物件傳遞為引數。 附加到細節元素的XML元素對應於表單的動態部分。 下列程式碼行會顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫`Document`物件的`createElement`方法，建立屬於詳細資料元素的子元素，並傳遞代表元素名稱的字串值。 將返回值轉換為`Element`。 接著，呼叫其`appendChild`方法來設定子元素的值，並將`Document`物件的`createTextNode`方法傳遞為引數。 指定顯示為子元素值的字串值。 最後，呼叫詳細資料元素的`appendChild`方法，將子項元素附加至詳細資料元素，並將子項元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加至詳細資料元素。 要正確建立用於填充採購訂單表單的XML資料源，您必須將以下XML元素附加到詳細資訊元素：`txtDescription`、`numQty`和`numUnitPrice`。
   * 對用於預先填入表單的所有資料項目，重複最後兩個子步驟。

1. 轉換XML資料來源

   * 通過調用`javax.xml.transform.Transformer`對象的靜態`newInstance`方法建立`javax.xml.transform.Transformer`對象。
   * 調用`TransformerFactory`物件的`newTransformer`方法，以建立`Transformer`物件。
   * 使用其建構子建立`ByteArrayOutputStream`對象。
   * 使用其建構子並傳遞在步驟1中建立的`org.w3c.dom.Document`對象，建立`javax.xml.transform.dom.DOMSource`對象。
   * 使用其建構子並傳遞`ByteArrayOutputStream`對象，建立`javax.xml.transform.dom.DOMSource`對象。
   * 調用`javax.xml.transform.Transformer`物件的`transform`方法並傳遞`javax.xml.transform.dom.DOMSource`和`javax.xml.transform.stream.StreamResult`物件，以填入Java `ByteArrayOutputStream`物件。
   * 建立位元組陣列，並將`ByteArrayOutputStream`對象的大小分配給位元組陣列。
   * 調用`ByteArrayOutputStream`物件的`toByteArray`方法，以填入位元組陣列。
   * 使用`com.adobe.idp.Document`物件的建構函式並傳遞位元組陣列，以建立物件。

1. 演算預先填入的表單

   叫用`FormsServiceClient`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 請確定您使用步驟1和2中建立的`com.adobe.idp.Document`物件。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。

   `renderPDFForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

   * 建立`javax.servlet.ServletOutputStream`物件，用來傳送表單資料流至用戶端網頁瀏覽器。
   * 通過調用`FormsResult`對象「s `getOutputContent`」方法建立`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 呼叫`InputStream`物件的`read`方法，並將位元組陣列傳入為引數，以填入表單資料流的位元組陣列。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。


**另請參閱**

[快速入門（SOAP模式）:使用Java API將可排程的版面預填入Forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#prepopulating-forms-using-the-web-service-api}預填表單

若要使用FormsAPI(web service)以可排程的版面預先填入表單，請執行下列步驟：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。 （請參閱[使用Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)建立Java代理類。）
   * 將Java代理類包含到類路徑中。

1. 建立記憶體中的XML資料來源

   * 通過調用`DocumentBuilderFactory`類`newInstance`方法建立Java `DocumentBuilderFactory`對象。
   * 呼叫`DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立Java `DocumentBuilder`物件。
   * 呼叫`DocumentBuilder`物件的`newDocument`方法，以實例化`org.w3c.dom.Document`物件。
   * 呼叫`org.w3c.dom.Document`物件的`createElement`方法，以建立XML資料來源的根元素。 這會建立代表根元素的`Element`物件。 將表示元素名稱的字串值傳遞至`createElement`方法。 將返回值轉換為`Element`。 接著，呼叫`Document`物件的`appendChild`方法，將根元素附加至檔案，並將根元素物件傳遞為引數。 下列程式碼行會顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫`Document`物件的`createElement`方法，以建立XML資料來源的標題元素。 將表示元素名稱的字串值傳遞至`createElement`方法。 將返回值轉換為`Element`。 接著，呼叫`root`物件的`appendChild`方法，將標題元素附加至根元素，並將標題元素物件傳遞為引數。 附加到標題元素的XML元素對應於表單的靜態部分。 下列程式碼行會顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 呼叫`Document`物件的`createElement`方法，建立屬於標題元素的子元素，並傳遞代表元素名稱的字串值。 將返回值轉換為`Element`。 接著，呼叫其`appendChild`方法來設定子元素的值，並將`Document`物件的`createTextNode`方法傳遞為引數。 指定顯示為子元素值的字串值。 最後，呼叫標題元素的`appendChild`方法，將子元素附加至標題元素，並將子元素物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 重複表格靜態部分（在XML資料來源圖中，這些欄位如A節所示）中每個欄位的最後一個子步驟，將所有剩餘的元素新增至標題元素。（請參閱[瞭解資料子群組](#understanding-data-subgroups)。）
   * 呼叫`Document`物件的`createElement`方法，以建立XML資料來源的詳細資料元素。 將表示元素名稱的字串值傳遞至`createElement`方法。 將返回值轉換為`Element`。 接著，呼叫`root`物件的`appendChild`方法，將詳細資料元素附加至根元素，並將詳細資料元素物件傳遞為引數。 附加到細節元素的XML元素對應於表單的動態部分。 下列程式碼行顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫`Document`物件的`createElement`方法，建立屬於詳細資料元素的子元素，並傳遞代表元素名稱的字串值。 將返回值轉換為`Element`。 接著，呼叫其`appendChild`方法來設定子元素的值，並將`Document`物件的`createTextNode`方法傳遞為引數。 指定顯示為子元素值的字串值。 最後，呼叫詳細資料元素的`appendChild`方法，將子項元素附加至詳細資料元素，並將子項元素物件傳遞為引數。 下列程式碼行顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加至詳細資料元素。 要正確建立用於填充採購訂單表單的XML資料源，您必須將以下XML元素附加到詳細資訊元素：`txtDescription`、`numQty`和`numUnitPrice`。
   * 對用於預先填入表單的所有資料項目，重複最後兩個子步驟。

1. 轉換XML資料來源

   * 通過調用`javax.xml.transform.Transformer`對象的靜態`newInstance`方法建立`javax.xml.transform.Transformer`對象。
   * 調用`TransformerFactory`物件的`newTransformer`方法，以建立`Transformer`物件。
   * 使用其建構子建立`ByteArrayOutputStream`對象。
   * 使用其建構子並傳遞在步驟1中建立的`org.w3c.dom.Document`對象，建立`javax.xml.transform.dom.DOMSource`對象。
   * 使用其建構子並傳遞`ByteArrayOutputStream`對象，建立`javax.xml.transform.dom.DOMSource`對象。
   * 調用`javax.xml.transform.Transformer`物件的`transform`方法並傳遞`javax.xml.transform.dom.DOMSource`和`javax.xml.transform.stream.StreamResult`物件，以填入Java `ByteArrayOutputStream`物件。
   * 建立位元組陣列，並將`ByteArrayOutputStream`對象的大小分配給位元組陣列。
   * 調用`ByteArrayOutputStream`物件的`toByteArray`方法，以填入位元組陣列。
   * 使用其建構子建立`BLOB`對象並調用其`setBinaryData`方法並傳遞位元組陣列。

1. 演算預先填入的表單

   叫用`FormsService`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。
   * `BLOB`物件，包含要與表單合併的資料。 請確定您使用在步驟1和步驟2中建立的`BLOB`對象。
   * 儲存運行時選項的`PDFFormRenderSpecc`對象。 如需詳細資訊，請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`對象。 這可用來儲存轉譯的PDF表單。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`對象。 （此引數將儲存表單中的頁數）。
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`對象。 （此引數將儲存地區值）。
   * 空的`com.adobe.idp.services.holders.FormsResultHolder`對象，將包含此操作的結果。

   `renderPDFForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個參數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

   * 獲取`com.adobe.idp.services.holders.FormsResultHolder`對象`value`資料成員的值，建立`FormResult`對象。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 通過調用`getContentType`方法獲取`BLOB`對象的內容類型。
   * 調用`setContentType`方法並傳遞`BLOB`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 建立位元組陣列，並呼叫`BLOB`物件的`getBinaryData`方法以填入它。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

   >[!NOTE]
   >
   >`renderPDFForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個參數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

