---
title: 處理已提交的Forms
seo-title: 處理已提交的Forms
description: 使用Forms服務來擷取在互動式表單中輸入的已提交資料。 使用者可以以XML、PDF和URL UTF-16格式提交表單資料。
seo-description: 使用Forms服務來擷取在互動式表單中輸入的已提交資料。 使用者可以以XML、PDF和URL UTF-16格式提交表單資料。
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 0%

---

# 處理已提交的Forms {#handling-submitted-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

讓使用者能夠填寫互動式表單的網頁型應用程式，需要將資料提交回伺服器。 使用Forms服務，您可以擷取使用者在互動式表單中輸入的資料。 擷取資料後，您就可以處理資料以符合您的業務需求。 例如，您可以將資料儲存在資料庫中、將資料發送到其他應用程式、將資料發送到其他服務、將資料合併到表單設計中、在Web瀏覽器中顯示資料等。

表單資料會以XML或PDF資料的形式提交至Forms服務，此選項可在Designer中設定。 以XML提交的表單可讓您擷取個別欄位資料值。 也就是說，您可以擷取使用者在表單中輸入之每個表單欄位的值。 以PDF資料提交的表單是二進位資料，而非XML資料。 您可以將表單儲存為PDF檔案，或將表單傳送至其他服務。 如果要從以XML提交的表單中擷取資料，然後使用表單資料建立PDF檔案，請叫用其他AEM Forms操作。 （請參閱[使用已提交的XML資料建立PDF文檔](/help/forms/developing/creating-pdf-documents-submitted-xml.md)）

下圖顯示從Web瀏覽器中顯示的互動式表單提交到名為`HandleData`的Java Servlet的資料。

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
   <td><p>使用者填入互動式表單，並按一下表單的「提交」按鈕。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>資料以XML資料的形式提交到<code>HandleData</code> Java Servlet。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p><code>HandleData</code> Java Servlet包含用於檢索資料的應用程式邏輯。</p></td>
  </tr>
 </tbody>
</table>

## 處理已提交的XML資料{#handling-submitted-xml-data}

表單資料以XML形式提交時，您可以擷取代表已提交資料的XML資料。 所有表單欄位在XML架構中都顯示為節點。 節點值與使用者填入的值對應。 請考慮使用貸款表單，表單中的每個欄位在XML資料中都顯示為節點。 每個節點的值都與使用者填入的值對應。 假設使用者填入貸款表單，其中顯示以下表單的資料。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

下圖顯示使用Forms服務用戶端API擷取的對應XML資料。

![hs_hs_loanddata](assets/hs_hs_loandata.png)

貸款表單中的欄位。 可擷取這些值
使用Java XML類。

>[!NOTE]
>
>表單設計必須在設計工具中正確設定，才能以XML資料提交資料。 要正確配置表單設計以提交XML資料，請確保將表單設計上的「提交」按鈕設定為提交XML資料。 有關設定「提交」按鈕以提交XML資料的資訊，請參閱[AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 處理已提交的PDF資料{#handling-submitted-pdf-data}

請考慮叫用Forms服務的Web應用程式。 Forms服務將互動式PDF表單轉譯給用戶端網頁瀏覽器後，使用者會填入表單，並以PDF資料形式提交回。 Forms服務收到PDF資料時，可將PDF資料傳送至其他服務或儲存為PDF檔案。 下圖顯示應用程式的邏輯流程。

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

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
   <td><p>3</p></td>
   <td><p>網頁包含存取叫用Forms服務的Java Servlet的連結。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms服務會為用戶端網頁瀏覽器轉譯互動式PDF表單。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者填入互動式表單，然後按一下提交按鈕。 表單會以PDF資料形式提交回Forms服務。 此選項在Designer中設定。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms服務會將PDF資料儲存為PDF檔案。 </p></td>
  </tr>
 </tbody>
</table>

## 處理已提交的URL UTF-16資料{#handling-submitted-url-utf-16-data}

如果表單資料以URL UTF-16資料提交，用戶端電腦需要Adobe Reader或Acrobat 8.1或更新版本。 此外，如果表單設計包含具有URL編碼資料(HTTP Post)的提交按鈕，且資料編碼選項為UTF-16，則必須在文字編輯器（如記事本）中修改表單設計。 您可以為提交按鈕將編碼選項設定為`UTF-16LE`或`UTF-16BE`。 Designer不提供此功能。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟{#summary-of-steps}的摘要

要處理已提交的表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 擷取表單資料。
1. 確定表單提交是否包含檔案附件。
1. 處理提交的資料。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API作業。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms Web服務API，請建立`FormsService`物件。

**擷取表單資料**

若要擷取已提交的表單資料，請叫用`FormsServiceClient`物件的`processFormSubmission`方法。 叫用此方法時，您必須指定已提交表單的內容類型。 從用戶端網頁瀏覽器提交資料至Forms服務時，可以以XML或PDF資料的形式提交資料。 若要擷取輸入表單欄位中的資料，可以以XML資料提交資料。

您也可以設定下列執行階段選項，從以PDF資料提交的表單中擷取表單欄位：

* 將下列值作為內容類型參數傳遞至`processFormSubmission`方法：`CONTENT_TYPE=application/pdf`。
* 將`RenderOptionsSpec`物件的`PDFToXDP`值設為`true`
* 將`RenderOptionsSpec`物件的`ExportDataFormat`值設為`XMLData`

調用`processFormSubmission`方法時，可指定已提交表單的內容類型。 以下清單指定了適用的內容類型值：

* **text/xml**:表示PDF表單以XML提交表單資料時要使用的內容類型。
* **application/x-www-form-urlencoded**:表示HTML表單以XML提交資料時要使用的內容類型。
* **application/pdf**:表示PDF表單以PDF提交資料時要使用的內容類型。

>[!NOTE]
>
>您會發現，有三個對應的快速入門與處理已提交的Forms區段相關聯。 使用Java API快速入門處理以PDF提交的PDF forms，示範如何處理已提交的PDF資料。 此快速入門中指定的內容類型為`application/pdf`。 使用Java API快速入門處理以XML提交的PDF forms示範如何處理以PDF表單提交的已提交XML資料。 此快速入門中指定的內容類型為`text/xml`。 同樣地，使用Java API快速入門處理以XML提交的HTML表單，會示範如何處理從HTML表單提交的已提交XML資料。 此快速入門中指定的內容類型為application/x-www-form-urlencoded。

您會擷取張貼至Forms服務的表單資料，並判斷其處理狀態。 也就是說，將資料提交至Forms服務時，並不代表Forms服務已完成資料處理，且資料已準備好處理。 例如，資料可提交至Forms服務，以便執行計算。 計算完成後，表單將呈現給用戶並顯示計算結果。 處理提交的資料之前，建議您判斷Forms服務是否已完成資料處理。

Forms服務會傳回下列值，指出其是否已完成資料處理：

* **0（提交）:** 已提交的資料已準備好進行處理。
* **1（計算）:** Forms服務對資料執行計算操作，且必須將結果轉譯回使用者。
* **2（驗證）:** Forms服務驗證的表單資料，必須將結果轉譯回使用者。
* **3（下一步）:** 目前頁面已變更，且結果必須寫入用戶端應用程式。
* **4(上一個**):當前頁面已更改，結果必須寫入客戶端應用程式。

>[!NOTE]
>
>計算和驗證必須返回給用戶。 (請參閱[計算表單資料](/help/forms/developing/calculating-form-data.md#calculating-form-data)。

**確定表單提交是否包含檔案附件**

提交至Forms服務的Forms可包含檔案附件。 例如，使用Acrobat的內建附件窗格，使用者可以選取要連同表單一併提交的檔案附件。 此外，用戶還可以使用HTML工具欄（以HTML檔案呈現）選擇檔案附件。

在您確定表單是否包含檔案附件後，您就可以處理資料。 例如，您可以將檔案附件保存到本地檔案系統。

>[!NOTE]
>
>表單必須以PDF資料提交，才能擷取檔案附件。 如果表單以XML資料提交，則不會提交檔案附件。

**處理提交的資料**

您可以根據已提交資料的內容類型，從已提交的XML資料中擷取個別表單欄位值，或將已提交的PDF資料儲存為PDF檔案（或將其傳送至其他服務）。 要提取單個表單欄位，請將提交的XML資料轉換為XML資料源，然後使用`org.w3c.dom`類檢索XML資料源值。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#handle-submitted-forms-using-the-java-api}處理已提交的表單

使用Forms API(Java)處理已提交的表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormsServiceClient`物件。

1. 擷取表單資料

   * 要檢索發佈到Java Servlet的表單資料，請使用其建構子並從建構子中調用`javax.servlet.http.HttpServletResponse`對象的`getInputStream`方法，建立`com.adobe.idp.Document`對象。
   * 使用其建構子建立`RenderOptionsSpec`物件。 通過調用`RenderOptionsSpec`對象的`setLocale`方法並傳遞指定區域設定值的字串值來設定區域設定值。

   >[!NOTE]
   >
   >您可以叫用`RenderOptionsSpec`物件的`setPDF2XDP`方法並傳遞`true`，以及呼叫`setXMLData`並傳遞`true`，指示Forms服務從已提交的PDF內容建立XDP或XML資料。 然後，可以調用`FormsResult`對象的`getOutputXML`方法以檢索與XDP/XML資料對應的XML資料。 （`FormsResult`物件由`processFormSubmission`方法傳回，將於下一個子步驟說明。）

   * 調用`FormsServiceClient`對象的`processFormSubmission`方法並傳遞以下值：

      * 包含表單資料的`com.adobe.idp.Document`物件。
      * 一個字串值，它指定包括所有相關HTTP標題的環境變數。 指定要處理的內容類型。 要處理XML資料，請為此參數指定以下字串值：`CONTENT_TYPE=text/xml`。 若要處理PDF資料，請為此參數指定下列字串值：`CONTENT_TYPE=application/pdf`。
      * 指定`HTTP_USER_AGENT`標題值的字串值，例如。 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 此參數值為選用值。
      * 儲存運行時選項的`RenderOptionsSpec`對象。

      `processFormSubmission`方法會傳回包含表單提交結果的`FormsResult`物件。

   * 叫用`FormsResult`物件的`getAction`方法，判斷Forms服務是否已完成表單資料的處理。 如果此方法返回值`0`，則資料已準備好進行處理。



1. 確定表單提交是否包含檔案附件

   * 調用`FormsResult`對象的`getAttachments`方法。 此方法會傳回`java.util.List`物件，其中包含以表單提交的檔案。
   * 逐一查看`java.util.List`對象，以確定是否有檔案附件。 如果有檔案附件，則每個元素都是`com.adobe.idp.Document`實例。 您可以調用`com.adobe.idp.Document`對象的`copyToFile`方法並傳遞`java.io.File`對象，以保存檔案附件。

   >[!NOTE]
   >
   >此步驟僅適用於表單以PDF提交的情況。

1. 處理提交的資料

   * 如果資料內容類型為`application/vnd.adobe.xdp+xml`或`text/xml`，請建立應用程式邏輯以檢索XML資料值。

      * 調用`FormsResult`對象的`getOutputContent`方法，建立`com.adobe.idp.Document`對象。
      * 通過調用`java.io.DataInputStream`建構子並傳遞`com.adobe.idp.Document`對象來建立`java.io.InputStream`對象。
      * 呼叫靜態`org.w3c.dom.DocumentBuilderFactory`物件的`newInstance`方法，建立`org.w3c.dom.DocumentBuilderFactory`物件。
      * 調用`org.w3c.dom.DocumentBuilderFactory`對象的`newDocumentBuilder`方法，建立`org.w3c.dom.DocumentBuilder`對象。
      * 調用`org.w3c.dom.DocumentBuilder`對象的`parse`方法並傳遞`java.io.InputStream`對象，建立`org.w3c.dom.Document`對象。
      * 檢索XML文檔中每個節點的值。 完成此工作的一種方式是建立接受兩個參數的自訂方法：`org.w3c.dom.Document`對象以及要檢索其值的節點的名稱。 此方法會傳回代表節點值的字串值。 在此程式後的程式碼範例中，此自訂方法稱為`getNodeText`。 此方法的內文如所示。
   * 如果資料內容類型為`application/pdf`，請建立應用程式邏輯，將提交的PDF資料儲存為PDF檔案。

      * 調用`FormsResult`對象的`getOutputContent`方法，建立`com.adobe.idp.Document`對象。
      * 使用其公共建構子建立`java.io.File`對象。 請務必指定PDF作為副檔名。
      * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件，以填入PDF檔案。


**另請參閱**

[快速入門（SOAP模式）:使用Java API處理以XML提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[快速入門（SOAP模式）:使用Java API處理以XML提交的HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[快速入門（SOAP模式）:使用Java API處理以PDF提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#handle-submitted-pdf-data-using-the-web-service-api}處理已提交的PDF資料

使用Forms API（網站服務）處理提交的表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`物件並設定驗證值。

1. 擷取表單資料

   * 要檢索發佈到Java Servlet的表單資料，請使用其建構子建立`BLOB`對象。
   * 調用`javax.servlet.http.HttpServletResponse`對象的`getInputStream`方法，建立`java.io.InputStream`對象。
   * 使用其建構子並傳遞`java.io.InputStream`物件的長度，以建立`java.io.ByteArrayOutputStream`物件。
   * 將`java.io.InputStream`對象的內容複製到`java.io.ByteArrayOutputStream`對象中。
   * 調用`java.io.ByteArrayOutputStream`對象的`toByteArray`方法，建立位元組陣列。
   * 叫用`setBinaryData`方法並將位元組陣列傳遞為引數，以填入`BLOB`物件。
   * 使用其建構子建立`RenderOptionsSpec`物件。 通過調用`RenderOptionsSpec`對象的`setLocale`方法並傳遞指定區域設定值的字串值來設定區域設定值。
   * 調用`FormsService`對象的`processFormSubmission`方法並傳遞以下值：

      * 包含表單資料的`BLOB`物件。
      * 一個字串值，它指定包括所有相關HTTP標題的環境變數。 指定要處理的內容類型。 要處理XML資料，請為此參數指定以下字串值：`CONTENT_TYPE=text/xml`。 若要處理PDF資料，請為此參數指定下列字串值：`CONTENT_TYPE=application/pdf`。
      * 指定`HTTP_USER_AGENT`標題值的字串值；例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存運行時選項的`RenderOptionsSpec`對象。
      * 由方法填入的空`BLOBHolder`物件。
      * 由方法填入的空`javax.xml.rpc.holders.StringHolder`物件。
      * 由方法填入的空`BLOBHolder`物件。
      * 由方法填入的空`BLOBHolder`物件。
      * 由方法填入的空`javax.xml.rpc.holders.ShortHolder`物件。
      * 由方法填入的空`MyArrayOf_xsd_anyTypeHolder`物件。 此參數用於儲存隨表單提交的檔案附件。
      * 由方法填入的空白`FormsResultHolder`物件，其表單為已提交。

      `processFormSubmission`方法會以表單提交的結果填入`FormsResultHolder`參數。

   * 叫用`FormsResult`物件的`getAction`方法，判斷Forms服務是否已完成表單資料的處理。 如果此方法傳回值`0`，表單資料便已可供處理。 通過獲取`FormsResultHolder`對象的`value`資料成員的值，可以獲取`FormsResult`對象。


1. 確定表單提交是否包含檔案附件

   獲取`MyArrayOf_xsd_anyTypeHolder`對象的`value`資料成員的值（將`MyArrayOf_xsd_anyTypeHolder`對象傳遞到`processFormSubmission`方法）。 此資料成員返回`Objects`陣列。 `Object`陣列中的每個元素都是`Object`，與隨表單提交的檔案相對應。 您可以取得陣列內的每個元素，並將其轉換為`BLOB`物件。

1. 處理提交的資料

   * 如果資料內容類型為`application/vnd.adobe.xdp+xml`或`text/xml`，請建立應用程式邏輯以檢索XML資料值。

      * 調用`FormsResult`對象的`getOutputContent`方法，建立`BLOB`對象。
      * 調用`BLOB`對象的`getBinaryData`方法，建立位元組陣列。
      * 調用`java.io.ByteArrayInputStream`建構子並傳遞位元組陣列，建立`java.io.InputStream`物件。
      * 呼叫靜態`org.w3c.dom.DocumentBuilderFactory`物件的`newInstance`方法，建立`org.w3c.dom.DocumentBuilderFactory`物件。
      * 調用`org.w3c.dom.DocumentBuilderFactory`對象的`newDocumentBuilder`方法，建立`org.w3c.dom.DocumentBuilder`對象。
      * 調用`org.w3c.dom.DocumentBuilder`對象的`parse`方法並傳遞`java.io.InputStream`對象，建立`org.w3c.dom.Document`對象。
      * 檢索XML文檔中每個節點的值。 完成此工作的一種方式是建立接受兩個參數的自訂方法：`org.w3c.dom.Document`對象以及要檢索其值的節點的名稱。 此方法會傳回代表節點值的字串值。 在此程式後的程式碼範例中，此自訂方法稱為`getNodeText`。 此方法的內文如所示。
   * 如果資料內容類型為`application/pdf`，請建立應用程式邏輯，將提交的PDF資料儲存為PDF檔案。

      * 調用`FormsResult`對象的`getOutputContent`方法，建立`BLOB`對象。
      * 調用`BLOB`對象的`getBinaryData`方法，建立位元組陣列。
      * 使用其公共建構子建立`java.io.File`對象。 請務必指定PDF作為副檔名。
      * 使用其建構子並傳遞`java.io.File`物件，以建立`java.io.FileOutputStream`物件。
      * 叫用`java.io.FileOutputStream`物件的`write`方法並傳遞位元組陣列，以填入PDF檔案。


**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
