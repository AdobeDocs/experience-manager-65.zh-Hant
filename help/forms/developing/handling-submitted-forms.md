---
title: 處理已提交的Forms
description: 使用Forms服務來擷取以互動式表單輸入的提交資料。 使用者可以提交XML、PDF和URL UTF-16格式的表單資料。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2894'
ht-degree: 0%

---

# 處理已提交的Forms {#handling-submitted-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

讓使用者能夠填寫互動式表單的網頁式應用程式，需要資料提交回伺服器。 使用Forms服務，您可以擷取使用者在互動式表單中輸入的資料。 擷取資料後，您可以處理資料以符合業務需求。 例如，您可以將資料儲存在資料庫中、將資料傳送至其他應用程式、將資料傳送至其他服務、將資料合併至表單設計、在網頁瀏覽器中顯示資料等等。

表單資料會以XML或PDF資料(在Designer中設定的選項)提交至Forms服務。 以XML形式提交的表單可讓您擷取個別欄位資料值。 也就是說，您可以擷取使用者在表單中輸入的每個表單欄位的值。 以PDF資料形式提交的表單是二進位資料，而非XML資料。 您可以將表單儲存為PDF檔案，或將表單傳送至其他服務。 如果您想要從以XML格式提交的表單中擷取資料，然後使用表單資料來建立PDF檔案，請叫用另一個AEM Forms作業。 (請參閱[使用已提交的XML資料建立PDF檔案](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

下圖顯示從網頁瀏覽器中顯示的互動式表單提交至名為`HandleData`的Java Servlet的資料。

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

下表說明圖表中的步驟。

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
   <td><p>使用者填寫互動式表單，然後按一下表單的「提交」按鈕。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>資料會以XML資料形式提交至<code>HandleData</code> Java Servlet。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p><code>HandleData</code> Java Servlet包含用來擷取資料的應用程式邏輯。</p></td>
  </tr>
 </tbody>
</table>

## 處理提交的XML資料 {#handling-submitted-xml-data}

表單資料以XML格式提交時，您可以擷取代表已提交資料的XML資料。 所有表單欄位都會顯示為XML結構描述中的節點。 節點值對應至使用者填入的值。 考慮貸款表單，其中表單中的每個欄位都會顯示為XML資料中的節點。 每個節點的值與使用者填入的值相對應。 假設使用者填入貸款表單，其資料顯示於下清單單。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

下圖顯示使用Forms服務使用者端API擷取的對應XML資料。

![hs_hs_loandata](assets/hs_hs_loandata.png)

貸款表單中的欄位。 這些值是可擷取的
使用Java XML類別。

>[!NOTE]
>
>在Designer中必須正確設定表單設計，資料才能以XML資料形式提交。 若要正確設定表單設計以提交XML資料，請確保表單設計上的提交按鈕已設定為提交XML資料。 如需設定[提交]按鈕以提交XML資料的相關資訊，請參閱[AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 處理提交的PDF資料 {#handling-submitted-pdf-data}

假設有一個叫用Forms服務的Web應用程式。 在Forms服務將互動式PDF表單轉譯給使用者端Web瀏覽器後，使用者會填寫表單並將其提交回PDF資料。 Forms服務收到PDF資料時，會將PDF資料傳送至其他服務或儲存為PDF檔案。 下圖顯示應用程式的邏輯流程。

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

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
   <td><p>網頁含有一個連結，可存取叫用Forms服務的Java Servlet。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms服務會將互動式PDF表單轉譯給使用者端網頁瀏覽器。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者填寫互動式表單並按一下提交按鈕。 表單會以PDF資料的形式提交回Forms服務。 此選項是在Designer中設定。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms服務會將PDF資料儲存為PDF檔案。 </p></td>
  </tr>
 </tbody>
</table>

## 處理提交的URL UTF-16資料 {#handling-submitted-url-utf-16-data}

如果表單資料以URL UTF-16資料提交，使用者端電腦會需要Adobe Reader或Acrobat 8.1或更新版本。 此外，如果表單設計包含具有URL編碼資料(HTTP Post)的提交按鈕，且資料編碼選項為UTF-16，則表單設計必須在文字編輯器（例如記事本）中修改。 您可以針對送出按鈕將編碼選項設定為`UTF-16LE`或`UTF-16BE`。 Designer不提供此功能。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

若要處理提交的表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 擷取表單資料。
1. 決定表單提交是否包含檔案附件。
1. 處理提交的資料。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API作業。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms Web服務API，請建立`FormsService`物件。

**擷取表單資料**

若要擷取提交的表單資料，請叫用`FormsServiceClient`物件的`processFormSubmission`方法。 叫用此方法時，您必須指定已提交表單的內容型別。 從使用者端Web瀏覽器將資料提交至Forms服務時，資料可以以XML或PDF資料形式提交。 若要擷取輸入表單欄位中的資料，資料可以提交為XML資料。

您也可以設定下列執行階段選項，從提交為PDF資料的表單中擷取表單欄位：

* 將下列值傳遞給`processFormSubmission`方法，做為內容型別引數： `CONTENT_TYPE=application/pdf`。
* 將`RenderOptionsSpec`物件的`PDFToXDP`值設定為`true`
* 將`RenderOptionsSpec`物件的`ExportDataFormat`值設定為`XMLData`

當您叫用`processFormSubmission`方法時，請指定已提交表單的內容型別。 下列清單指定適用的內容型別值：

* **text/xml**：代表PDF表單以XML形式提交表單資料時所使用的內容型別。
* **application/x-www-form-urlencoded**：代表HTML表單以XML形式提交資料時所使用的內容型別。
* **application/pdf**：代表PDF表單將資料提交為PDF時要使用的內容型別。

>[!NOTE]
>
>您會發現有三個與處理已提交的Forms區段相關的快速入門。 使用Java API快速入門處理以PDF形式提交的PDF forms會示範如何處理提交的PDF資料。 此快速入門中指定的內容型別為`application/pdf`。 使用Java API快速入門以XML格式提交的處理PDF forms示範如何處理從PDF表單提交的提交XML資料。 此快速入門中指定的內容型別為`text/xml`。 同樣地，使用Java API快速入門以XML格式提交的處理HTML表單會示範如何處理從HTML表單提交的已提交XML資料。 此快速入門中指定的內容型別為application/x-www-form-urlencoded。

您可以擷取發佈至Forms服務的表單資料，並判斷其處理狀態。 也就是說，將資料提交至Forms服務時，未必代表Forms服務已完成資料處理，而資料已準備好進行處理。 例如，資料可提交至Forms服務，以便執行計算。 計算完成後，表單會轉譯回使用者並顯示計算結果。 在處理提交的資料之前，建議您先判斷Forms服務是否已完成資料處理。

Forms服務會傳回下列值，指出是否已完成資料處理：

* **0 （提交）：**&#x200B;已提交的資料已準備就緒可供處理。
* **1 （計算）：** Forms服務已針對資料執行計算作業，結果必須轉譯回使用者。
* **2 （驗證）：** Forms服務已驗證的表單資料與結果必須轉譯回使用者。
* **3 （下一步）：**&#x200B;目前頁面已變更，結果必須寫入使用者端應用程式。
* **4 (Previous**)：目前頁面已變更，結果必須寫入使用者端應用程式。

>[!NOTE]
>
>計算與驗證必須轉譯回使用者。 (請參閱[計算表單資料](/help/forms/developing/calculating-form-data.md#calculating-form-data)。

**判斷表單提交是否包含檔案附件**

提交至Forms服務的Forms可包含檔案附件。 例如，使用Acrobat的內建附件窗格，使用者可以選擇要與表單一起提交的檔案附件。 此外，使用者也可以使用以HTML檔案呈現的HTML工具列來選取檔案附件。

確定表單是否包含檔案附件後，即可處理資料。 例如，您可以將檔案附件儲存至本機檔案系統。

>[!NOTE]
>
>表單必須以PDF資料的形式提交，才能擷取檔案附件。 如果表單以XML資料形式提交，則不會提交檔案附件。

**處理提交的資料**

根據提交資料的內容型別，您可以從提交的XML資料中擷取個別表單欄位值，或將提交的PDF資料儲存為PDF檔案（或將其傳送至其他服務）。 若要擷取個別表單欄位，請將提交的XML資料轉換為XML資料來源，然後使用`org.w3c.dom`類別擷取XML資料來源值。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API處理提交的表單 {#handle-submitted-forms-using-the-java-api}

使用Forms API (Java)處理提交的表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormsServiceClient`物件。

1. 擷取表單資料

   * 若要擷取張貼到Java Servlet的表單資料，請使用其建構函式並從建構函式中叫用`javax.servlet.http.HttpServletResponse`物件的`getInputStream`方法來建立`com.adobe.idp.Document`物件。
   * 使用物件的建構函式建立`RenderOptionsSpec`物件。 透過叫用`RenderOptionsSpec`物件的`setLocale`方法並傳遞指定地區設定值的字串值來設定地區設定值。

   >[!NOTE]
   >
   >您可以透過叫用`RenderOptionsSpec`物件的`setPDF2XDP`方法並傳遞`true`以及呼叫`setXMLData`並傳遞`true`，指示Forms服務從提交的PDF內容建立XDP或XML資料。 然後您可以叫用`FormsResult`物件的`getOutputXML`方法，以擷取對應至XDP/XML資料的XML資料。 （`FormsResult`物件由`processFormSubmission`方法傳回，這會在下一個子步驟中說明。）

   * 叫用`FormsServiceClient`物件的`processFormSubmission`方法，並傳遞下列值：

      * 包含表單資料的`com.adobe.idp.Document`物件。
      * 字串值，指定包含所有相關HTTP標頭的環境變數。 指定要處理的內容型別。 若要處理XML資料，請為此引數指定下列字串值： `CONTENT_TYPE=text/xml`。 若要處理PDF資料，請為此引數指定下列字串值： `CONTENT_TYPE=application/pdf`。
      * 字串值，指定`HTTP_USER_AGENT`標頭值，例如。 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。此引數值為選用。
      * 儲存執行階段選項的`RenderOptionsSpec`物件。

     `processFormSubmission`方法傳回包含表單提交結果的`FormsResult`物件。

   * 判斷Forms服務是否已透過叫用`FormsResult`物件的`getAction`方法來完成表單資料的處理。 如果此方法傳回值`0`，資料即可處理。

1. 決定表單提交是否包含檔案附件

   * 叫用`FormsResult`物件的`getAttachments`方法。 此方法會傳回`java.util.List`物件，其中包含以表單提交的檔案。
   * 逐一檢視`java.util.List`物件，以判斷是否有檔案附件。 如果有檔案附件，則每個元素都是`com.adobe.idp.Document`執行個體。 您可以叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件來儲存檔案附件。

   >[!NOTE]
   >
   >此步驟僅適用於表單以PDF提交的情況。

1. 處理提交的資料

   * 如果資料內容型別為`application/vnd.adobe.xdp+xml`或`text/xml`，請建立應用程式邏輯以擷取XML資料值。

      * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件。
      * 呼叫`java.io.DataInputStream`建構函式並傳遞`com.adobe.idp.Document`物件以建立`java.io.InputStream`物件。
      * 呼叫靜態`org.w3c.dom.DocumentBuilderFactory`物件的`newInstance`方法，以建立`org.w3c.dom.DocumentBuilderFactory`物件。
      * 呼叫`org.w3c.dom.DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立`org.w3c.dom.DocumentBuilder`物件。
      * 呼叫`org.w3c.dom.DocumentBuilder`物件的`parse`方法並傳遞`java.io.InputStream`物件，以建立`org.w3c.dom.Document`物件。
      * 擷取XML檔案中每個節點的值。 完成此工作的一種方式是建立接受兩個引數的自訂方法： `org.w3c.dom.Document`物件以及您要擷取其值的節點名稱。 此方法會傳回代表節點值的字串值。 在此程式之後的程式碼範例中，此自訂方法稱為`getNodeText`。 會顯示此方法的內文。

   * 如果資料內容型別為`application/pdf`，請建立應用程式邏輯以將提交的PDF資料儲存為PDF檔案。

      * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件。
      * 使用物件的公用建構函式來建立`java.io.File`物件。 請務必指定PDF作為副檔名。
      * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件以填入PDF檔案。

**另請參閱**

[快速入門(SOAP模式)：使用Java API處理以XML格式提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[快速入門(SOAP模式)：使用Java API處理以XML格式提交的HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[快速入門(SOAP模式)：使用Java API處理以PDF形式提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API處理提交的PDF資料 {#handle-submitted-pdf-data-using-the-web-service-api}

使用Forms API （網站服務）處理提交的表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立`FormsService`物件並設定驗證值。

1. 擷取表單資料

   * 若要擷取張貼到Java Servlet的表單資料，請使用其建構函式建立`BLOB`物件。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 使用物件的建構函式並傳遞`java.io.InputStream`物件的長度，以建立`java.io.ByteArrayOutputStream`物件。
   * 將`java.io.InputStream`物件的內容複製到`java.io.ByteArrayOutputStream`物件中。
   * 透過叫用`java.io.ByteArrayOutputStream`物件的`toByteArray`方法建立位元組陣列。
   * 叫用物件的`setBinaryData`方法，並將位元組陣列作為引數傳遞，以填入`BLOB`物件。
   * 使用物件的建構函式建立`RenderOptionsSpec`物件。 透過叫用`RenderOptionsSpec`物件的`setLocale`方法並傳遞指定地區設定值的字串值來設定地區設定值。
   * 叫用`FormsService`物件的`processFormSubmission`方法，並傳遞下列值：

      * 包含表單資料的`BLOB`物件。
      * 字串值，指定包含所有相關HTTP標頭的環境變數。 指定要處理的內容型別。 若要處理XML資料，請為此引數指定下列字串值： `CONTENT_TYPE=text/xml`。 若要處理PDF資料，請為此引數指定下列字串值： `CONTENT_TYPE=application/pdf`。
      * 字串值，指定`HTTP_USER_AGENT`標頭值；例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存執行階段選項的`RenderOptionsSpec`物件。
      * 方法填入的空白`BLOBHolder`物件。
      * 方法填入的空白`javax.xml.rpc.holders.StringHolder`物件。
      * 方法填入的空白`BLOBHolder`物件。
      * 方法填入的空白`BLOBHolder`物件。
      * 方法填入的空白`javax.xml.rpc.holders.ShortHolder`物件。
      * 方法填入的空白`MyArrayOf_xsd_anyTypeHolder`物件。 此引數用於儲存與表單一起提交的檔案附件。
      * 空的`FormsResultHolder`物件由方法以提交的表單填入。

     `processFormSubmission`方法會將表單提交的結果填入`FormsResultHolder`引數。

   * 判斷Forms服務是否已透過叫用`FormsResult`物件的`getAction`方法來完成表單資料的處理。 如果此方法傳回值`0`，即可處理表單資料。 您可以取得`FormsResultHolder`物件之`value`資料成員的值，以取得`FormsResult`物件。

1. 決定表單提交是否包含檔案附件

   取得`MyArrayOf_xsd_anyTypeHolder`物件之`value`資料成員的值（`MyArrayOf_xsd_anyTypeHolder`物件已傳遞至`processFormSubmission`方法）。 此資料成員傳回`Objects`的陣列。 `Object`陣列中的每個元素都是`Object`，對應到與表單一起提交的檔案。 您可以取得陣列中的每個元素，並將其轉換成`BLOB`物件。

1. 處理提交的資料

   * 如果資料內容型別為`application/vnd.adobe.xdp+xml`或`text/xml`，請建立應用程式邏輯以擷取XML資料值。

      * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`BLOB`物件。
      * 透過叫用`BLOB`物件的`getBinaryData`方法建立位元組陣列。
      * 呼叫`java.io.ByteArrayInputStream`建構函式並傳遞位元組陣列，以建立`java.io.InputStream`物件。
      * 呼叫靜態`org.w3c.dom.DocumentBuilderFactory`物件的`newInstance`方法，以建立`org.w3c.dom.DocumentBuilderFactory`物件。
      * 呼叫`org.w3c.dom.DocumentBuilderFactory`物件的`newDocumentBuilder`方法，以建立`org.w3c.dom.DocumentBuilder`物件。
      * 呼叫`org.w3c.dom.DocumentBuilder`物件的`parse`方法並傳遞`java.io.InputStream`物件，以建立`org.w3c.dom.Document`物件。
      * 擷取XML檔案中每個節點的值。 完成此工作的一種方式是建立接受兩個引數的自訂方法： `org.w3c.dom.Document`物件以及您要擷取其值的節點名稱。 此方法會傳回代表節點值的字串值。 在此程式之後的程式碼範例中，此自訂方法稱為`getNodeText`。 會顯示此方法的內文。

   * 如果資料內容型別為`application/pdf`，請建立應用程式邏輯以將提交的PDF資料儲存為PDF檔案。

      * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`BLOB`物件。
      * 透過叫用`BLOB`物件的`getBinaryData`方法建立位元組陣列。
      * 使用物件的公用建構函式來建立`java.io.File`物件。 請務必指定PDF作為副檔名。
      * 使用它的建構函式並傳遞`java.io.File`物件來建立`java.io.FileOutputStream`物件。
      * 呼叫`java.io.FileOutputStream`物件的`write`方法並傳遞位元組陣列，以填入PDF檔案。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
