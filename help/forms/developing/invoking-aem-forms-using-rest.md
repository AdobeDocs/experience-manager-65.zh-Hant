---
title: 使用REST要求叫用AEM Forms
seo-title: 使用REST要求叫用AEM Forms
description: 使用REST請求叫用在Workbench中建立的程式。
seo-description: 使用REST請求叫用在Workbench中建立的程式。
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 0%

---

# 使用REST請求叫用AEM Forms {#invoking-aem-forms-using-rest-requests}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

可在Workbench中建立的程式可進行設定，以便您能透過「代表性狀態轉移(REST)」請求來叫用這些程式。 REST要求會從HTML頁面傳送。 也就是說，您可以使用REST要求直接從網頁叫用Forms程式。 例如，您可以開啟網頁的新例項。 接著，您可以叫用Forms程式，並載入已轉譯的PDF檔案，其中包含以HTTPPOST請求傳送的資料。

有兩種HTML用戶端。 第一個HTML用戶端是以JavaScript寫入的AJAX用戶端。 第二個用戶端是包含提交按鈕的HTML表單。 基於HTML的客戶端應用程式不是唯一可能的REST客戶端。 任何支援HTTP請求的客戶端應用程式都可以使用REST調用調用服務。 例如，您可以使用PDF表單的REST叫用來叫用服務。 (請參閱從Acrobat](#rest-invocation-examples)叫用MyApplication/EncryptDocument進程。)[

使用REST要求時，建議您不要直接叫用Forms服務。 請改為叫用在Workbench中建立的程式。 建立專用於REST調用的流程時，請使用程式化的起始點。 在此情況下，將自動添加REST端點。 有關在Workbench中建立流程的資訊，請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

當您使用REST叫用服務時，系統會提示您輸入AEM表單使用者名稱和密碼。 但是，如果您不想指定用戶名和密碼，則可禁用服務安全性。

要使用REST調用Forms服務（進程在激活進程時變為服務），請配置REST端點。 （請參閱[管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)中的「管理端點」。）

設定REST端點後，您可以使用HTTPGET方法或POST方法叫用Forms服務。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

強制`ServiceName`值是要叫用的Forms服務的名稱。 選用的`OperationName`值是服務操作的名稱。 如果未指定此值，則此名稱預設為`invoke`，即啟動進程的操作名稱。 選用的`ServiceVersion`值是以X.Y格式編碼的版本。 如果未指定此值，則使用最新版本。 `enctype`值也可以是`application/x-www-form-urlencoded`。

## 支援的資料類型{#supported-data-types}

使用REST要求叫用AEM Forms服務時，支援下列資料類型：

* Java基元資料類型，如字串和整數
* `com.adobe.idp.Document` 資料類型
* XML資料類型，如`org.w3c.Document`和`org.w3c.Element`
* 集合對象，如`java.util.List`和`java.util.Map`

   在Workbench中建立的程式中，通常會接受這些資料類型作為輸入值。

   如果使用HTTPPOST方法叫用Froms服務，則引數會傳入HTTP要求內文中。 如果AEM Forms服務的簽章有字串輸入參數，要求內文可包含輸入參數的文字值。 如果服務的簽名定義了多個字串參數，則請求可以遵循HTTP的`application/x-www-form-urlencoded`標籤法，並使用參數的名稱作為表單的欄位名稱。

   如果Forms服務傳回字串參數，則結果為輸出參數的文字表示。 如果服務返回多個字串參數，則結果為以下格式對輸出參數進行編碼的XML文檔：
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >`output-paramater1`值表示輸出參數名稱。

   如果Forms服務需要`com.adobe.idp.Document`參數，則只能使用HTTPPOST方法叫用該服務。 如果服務需要一個`com.adobe.idp.Document`參數，則HTTP要求內文會成為輸入Document物件的內容。

   如果AEM Forms服務需要多個輸入參數，HTTP要求內文必須是RFC 1867所定義的多部分MIME訊息。 （RFC 1867是網頁瀏覽器用來將檔案上傳至網站的標準。） 每個輸入參數必須作為多部分消息的單獨部分發送，並以`multipart/form-data`格式編碼。 每個部件的名稱必須與參數的名稱匹配。

   清單和地圖也可作為在Workbench中建立的AEM Forms程式的輸入值。 因此，在使用REST請求時，您可以使用這些資料類型。 不支援Java陣列，因為這些陣列不會作為AEM Forms程式的輸入值。

   如果輸入參數是清單，REST用戶端可以多次指定參數來傳送它（清單中每個項目一次）。 例如，如果A是文檔清單，則輸入必須是由多個名為A的部件組成的多部分消息。在這種情況下，每個名為A的部件將成為輸入清單中的項目。 如果B是字串的清單，則輸入可以是`application/x-www-form-urlencoded`消息，該消息由多個名為B的欄位組成。在這種情況下，每個名為B的表單欄位將成為輸入清單中的項。

   如果輸入參數是映射，並且它是服務僅輸入參數，則輸入消息的每個部分/欄位將成為映射中的鍵/值記錄。 每個部件/欄位的名稱將成為記錄的鍵。 每個部件/欄位的內容將成為記錄的值。

   如果輸入映射不是僅服務的輸入參數，則屬於該映射的每個鍵/值記錄可以使用一個參數來發送，該參數名為參數名稱和記錄的鍵的串連。 例如，名為`attributes`的輸入映射可隨下列鍵/值對的清單一起發送：

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   這將轉化為三條記錄的地圖：`Color=red`、`Shape=box`和`Width=5`。

   清單和映射類型的輸出參數將成為生成的XML消息的一部分。 輸出清單在XML中以一系列XML元素表示，清單中的每個項目都有一個元素。 每個元素的名稱都與輸出清單參數相同。 每個XML元素的值是兩項之一：

* 清單中項的文本表示（如果清單包含字串類型）
* 指向文檔內容的URL（如果清單包含`com.adobe.idp.Document`對象）

   以下示例是服務返回的XML消息，該服務具有名為&#x200B;*list*的單個輸出參數，該參數是整數的清單。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`輸出映射參數在結果XML消息中以一系列XML元素表示，其中每個記錄在映射中具有一個元素。每個元素的名稱都與地圖記錄的索引鍵相同。 每個元素的值是映射記錄值的文本表示（如果映射由包含字串值的記錄組成），或指向文檔內容的URL（如果映射由具有`com.adobe.idp.Document`值的記錄組成）。 以下是服務返回的XML消息的示例，該服務具有名為`map`的單個輸出參數。 此參數值是由將字母與`com.adobe.idp.Document`對象關聯的記錄組成的映射。
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 非同步調用{#asynchronous-invocations}

某些AEM Forms服務（例如以人為中心的長期流程）需要很長的時間才能完成。 這些服務可以非同步以非封鎖方式叫用。 （請參閱[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

可在叫用URL中以`async_invoke`取代`services`，以非同步叫用AEM Forms服務，如下列範例所示。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

此URL返回負責此調用的作業的標識符值（以「文本/純」格式）。

非同步調用的狀態可通過使用調用URL(`services`)替換`async_status`來檢索。 URL必須包含`job_id`參數，該參數指定與此調用關聯的作業的標識符值。 例如：

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

此URL返回一個整數值（以&quot;text/plain&quot;格式），根據作業管理器的規範對作業狀態進行編碼（例如，2表示正在運行，3表示已完成，4表示失敗等）。

如果作業完成，URL會傳回與同步叫用服務相同的結果。

完成作業並檢索結果後，可使用`services`的調用URL替換`async_dispose`，以處理作業。 該URL還應包含`job_id`參數，該參數指定作業的標識符值。 例如：

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

如果作業已成功處置，此URL會傳回空白訊息。

## 報告{#error-reporting}時出錯

如果由於伺服器上擲回例外狀況而無法完成同步或非同步呼叫請求，則會將例外狀況報告為HTTP回應訊息的一部分。 如果調用URL（或非同步調用的`async_result` URL）沒有.xml尾碼，則REST提供程式將返回HTTP代碼`500 Internal Server Error`，後跟異常消息。

如果調用URL（或非同步調用的`async_result` URL）的尾碼為.xml，則REST提供程式將返回HTTP代碼`200 OK`，後跟以下格式描述異常的XML文檔。

```xml
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

`DSCError`元素為選用元素，且僅當例外為`com.adobe.idp.dsc.DSCException`的例項時才會出現。

## 安全性和驗證{#security-and-authentication}

為了為REST叫用提供安全傳輸，AEM Forms管理員可以在托管AEM Forms的J2EE應用程式伺服器上啟用HTTPS通訊協定。 此配置是J2EE應用程式伺服器的專用配置；它不屬於forms伺服器配置。

>[!NOTE]
>
>身為Workbench開發人員，若想透過REST端點公開您的程式，請記住XSS弱點問題。 XSS漏洞可用來竊取或操控Cookie、修改內容呈現方式，以及危害機密資訊。 如果XSS漏洞是問題，建議您使用其他輸入和輸出資料驗證規則來擴充處理邏輯。

## 支援REST調用{#aem-forms-services-that-support-rest-invocation}的AEM Forms服務

雖然建議您叫用使用Workbench建立的程式，而非直接叫用服務，但有些AEM Forms服務確實支援REST叫用。 建議您直接調用進程而不是直接調用服務的原因是調用進程更有效。 請考量下列案例。 假設您要從REST客戶端建立策略。 也就是說，您希望REST客戶端定義策略名稱、離線租用期等值。

要建立策略，必須定義複雜的資料類型，如`PolicyEntry`對象。 `PolicyEntry`對象定義了與策略關聯的屬性，如權限。 （請參閱[建立策略](/help/forms/developing/protecting-documents-policies.md#creating-policies)。）

與其發送REST請求來建立策略（包括定義複雜的資料類型，如`PolicyEntry`對象），不如使用Workbench建立策略的過程。 定義流程以接受原始輸入變數，如定義流程名稱的字串值或定義離線租賃期的整數。

這樣，您就不必建立REST調用請求，該請求包含操作所需的複雜資料類型。 該進程定義了複雜的資料類型，您從REST客戶端執行的所有操作都是調用該進程並傳遞原始資料類型。 有關使用REST調用進程的資訊，請參閱[使用REST調用MyApplication/EncryptDocument進程](#rest-invocation-examples)。

以下清單指定了支援直接REST調用的AEM Forms服務。

* Distiller服務
* Rights Management服務
* GeneratePDF服務
* 產生3dPDF服務
* FormDataIntegration

## REST調用示例{#rest-invocation-examples}

提供了以下REST調用示例：

* 將布林值傳遞至AEM Forms程式
* 將日期值傳遞至AEM Forms程式
* 將檔案傳遞至AEM Forms程式
* 將檔案和文字值傳遞至AEM Forms程式
* 將分項清單傳遞至AEM Forms程式
* 使用REST調用MyApplication/EncryptDocument進程
* 從Acrobat叫用MyApplication/EncryptDocument程式

   每個範例都示範如何將不同的資料類型傳遞至AEM Forms程式

**將布林值傳遞至程式**

以下HTML範例會將兩個`Boolean`值傳遞至名為`RestTest2`的AEM Forms程式。 調用方法的名稱為`invoke`，版本為1.0。請注意，已使用HTML Post方法。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**將日期值傳遞至程式**

以下HTML範例會將日期值傳遞至名為`SOAPEchoService`的AEM Forms程式。 調用方法的名稱為`echoCalendar`。 請注意，已使用HTML `Post`方法。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**將檔案傳遞至程式**

以下HTML示例調用名為`MyApplication/EncryptDocument`的AEM Forms進程，該進程需要PDF文檔。 如需此程式的相關資訊，請參閱[使用MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)叫用AEM Forms。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**將文檔和文本值傳遞至進程**

以下HTML示例調用一個名為`RestTest3`的AEM Forms進程，該進程需要一個文檔和兩個文本值。 請注意，已使用HTML Post方法。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**將枚舉值傳遞至進程**

以下HTML範例會叫用名為`SOAPEchoService`的AEM Forms程式，該程式需要列舉值。 請注意，已使用HTML Post方法。

```html
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**使用REST調用MyApplication/EncryptDocument進程**

您可以使用REST來叫用名為&#x200B;*MyApplication/EncryptDocument*&#x200B;的AEM Forms短期進程。

>[!NOTE]
>
>此程式並非以現有的AEM Forms程式為基礎。 若要遵循程式碼範例，請使用workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

叫用此程式時，會執行下列動作：

1. 獲取傳遞至流程的不安全PDF文檔。 此操作基於`SetValue`操作。 此進程的輸入參數是名為`inDoc`的`document`進程變數。
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 在名為`outDoc`的進程變數中返回密碼加密的PDF文檔。

   使用REST請求叫用此程式時，加密的PDF檔案會顯示在網頁瀏覽器中。 在查看PDF文檔之前，請指定密碼（除非禁用了安全性）。 以下HTML代碼表示對`MyApplication/EncryptDocument`進程的REST調用請求。

   ```html
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**從Acrobat叫用MyApplication/EncryptDocument程式** {#invoke-process-acrobat}

您可以使用REST要求，從Acrobat叫用Forms程式。 例如，您可以調用&#x200B;*MyApplication/EncryptDocument*&#x200B;進程。 若要從Acrobat叫用Forms程式，請在Designer內的XDP檔案上放置提交按鈕。 （請參閱[Designer幫助](https://www.adobe.com/go/learn_aemforms_designer_63)。）

指定URL以在按鈕的&#x200B;*提交至URL*&#x200B;欄位內叫用程式，如下圖所示。

調用該進程的完整URL為https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument。

如果此過程需要PDF文檔作為輸入值，請確保您以PDF提交表單，如上圖所示。 此外，要成功調用進程，進程必須返回PDF文檔。 否則，Acrobat無法處理傳回值，且會發生錯誤。 您不必指定輸入進程變數的名稱。 例如， *MyApplication/EncryptDocument*&#x200B;進程具有名為`inDoc`的輸入變數。 只要表單已提交為PDF，您就不必在Doc中指定。

您也可以將表單資料以XML形式提交到Forms進程。要提交XML資料，請確保`Submit As`下拉清單指定XML。 由於處理程式的傳回值必須是PDF檔案，因此PDF檔案會顯示在Acrobat中。
