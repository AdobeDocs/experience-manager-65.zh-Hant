---
title: 使用REST請求調用AEM Forms
seo-title: Invoking AEM Forms using REST Requests
description: 使用REST請求調用在Workbench中建立的流程。
seo-description: Invoke processes created in Workbench using REST requests.
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 0%

---

# 使用REST請求調用AEM Forms {#invoking-aem-forms-using-rest-requests}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

可以配置在Workbench中建立的流程，以便您可以通過表示狀態轉移(REST)請求調用這些流程。 REST請求從HTML頁發送。 即，您可以使用REST請求直接從網頁調用Forms進程。 例如，可以開啟網頁的新實例。 然後，您可以調用Forms進程並載入已呈現的PDF文檔，其中包含在HTTPPOST請求中發送的資料。

存在兩種類型的HTML客戶端。 第一個HTML客AJAX戶端是用JavaScript編寫的客戶端。 第二個客戶端是包含提交按鈕的HTML表單。 基於HTML的客戶端應用程式不是唯一可能的REST客戶端。 任何支援HTTP請求的客戶端應用程式都可以使用REST調用來調用服務。 例如，可以通過使用PDF表單的REST調用來調用服務。 (請參閱 [從Acrobat調用MyApplication/EncryptDocument進程](#rest-invocation-examples)。)

使用REST請求時，建議您不要直接調用Forms服務。 而是調用在Workbench中建立的流程。 建立用於調用REST的進程時，請使用寫程式起點。 在這種情況下，將自動添加REST端點。 有關在Workbench中建立流程的資訊，請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

使用REST調用服務時，系統會提示您輸入表AEM單用戶名和密碼。 但是，如果您不想指定用戶名和密碼，則可以禁用服務安全性。

要使用REST調用Forms服務（當該進程被激活時，該進程將成為服務），請配置REST端點。 (請參閱中的「管理端點」 [管理幫助](https://www.adobe.com/go/learn_aemforms_admin_63)。)

配置REST端點後，可以使用HTTPGET方法或POST方法調用REST服務。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

強制 `ServiceName` value是要調用的Forms服務的名稱。 可選 `OperationName` value是服務操作的名稱。 如果未指定此值，則此名稱預設為 `invoke`，即啟動進程的操作名。 可選 `ServiceVersion` value是以X.Y格式編碼的版本。 如果未指定此值，則使用最新版本。 的 `enctype` 值也可以 `application/x-www-form-urlencoded`。

## 支援的資料類型 {#supported-data-types}

使用REST請求調用AEM Forms服務時，支援以下資料類型：

* Java基元資料類型，如字串和整數
* `com.adobe.idp.Document` 資料類型
* XML資料類型，如 `org.w3c.Document` 和 `org.w3c.Element`
* 集合對象，如 `java.util.List` 和 `java.util.Map`

   這些資料類型通常被接受為在Workbench中建立的流程的輸入值。

   如果使用HTTPPOST方法調用Froms服務，則參數會在HTTP請求體內傳遞。 如果AEM Forms服務的簽名具有字串輸入參數，則請求主體可以包含輸入參數的文本值。 如果服務的簽名定義了多個字串參數，則請求可以遵循HTTP的 `application/x-www-form-urlencoded` 用參數名稱作為窗體欄位名稱的符號表示。

   如果Forms服務返回字串參數，則結果是輸出參數的文本表示。 如果服務返回多個字串參數，則結果是以下格式對輸出參數進行編碼的XML文檔：
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >的 `output-paramater1` value表示輸出參數名稱。

   如果Forms服務需要 `com.adobe.idp.Document` 參數，只能使用HTTPPOST方法調用服務。 如果服務需要 `com.adobe.idp.Document` 參數，HTTP請求主體將成為輸入文檔對象的內容。

   如果AEM Forms服務需要多個輸入參數，則HTTP請求正文必須是RFC 1867定義的多部分MIME消息。 （RFC 1867是Web瀏覽器用於將檔案上載到網站的標準。） 每個輸入參數必須作為多部分消息的單獨部分發送，並在 `multipart/form-data` 的子菜單。 每個零件的名稱必須與參數的名稱匹配。

   清單和映射也用作在Workbench中建立的AEM Forms進程的輸入值。 因此，在使用REST請求時，可以使用這些資料類型。 不支援Java陣列，因為它們不用作AEM Forms進程的輸入值。

   如果輸入參數是清單，則REST客戶端可以通過多次指定該參數（對於清單中的每個項都指定一次）來發送該參數。 例如，如果A是文檔清單，則輸入必須是由多個名為A的部件組成的多部件消息。在這種情況下，每個名為A的部件都會成為輸入清單中的項目。 如果B是字串清單，則輸入可以是 `application/x-www-form-urlencoded` 消息，包含多個名為B的欄位。在這種情況下，每個名為B的表單欄位都將成為輸入清單中的項。

   如果輸入參數是映射，並且它只是服務輸入參數，則輸入消息的每個部分/欄位將成為映射中的鍵/值記錄。 每個部件/欄位的名稱將成為記錄的鍵。 每個部件/欄位的內容將成為記錄的值。

   如果輸入映射不是僅服務的輸入參數，則可以使用名為參數名稱和記錄的鍵的級聯的參數來發送屬於映射的每個鍵/值記錄。 例如，一個名為 `attributes` 可以隨下列鍵/值對的清單一起發送：

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   這轉化為一張三條記錄的地圖： `Color=red`。 `Shape=box`, `Width=5`。

   清單和映射類型的輸出參數成為結果XML消息的一部分。 輸出清單以XML形式表示為一系列XML元素，其中每個元素在清單中都有一個元素。 每個元素與輸出清單參數的名稱相同。 每個XML元素的值是以下兩項之一：

* 清單中項的文本表示（如果清單包含字串類型）
* 指向文檔內容的URL(如果清單由 `com.adobe.idp.Document` 對象)

   以下示例是服務返回的XML消息，該服務具有名為 *清單*，是整數清單。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`輸出映射參數在結果XML消息中表示為一系列XML元素，其中每個元素都對應於映射中的每個記錄。 每個元素的名稱與映射記錄的鍵相同。 每個元素的值是映射記錄值的文本表示形式（如果映射包含具有字串值的記錄）或指向文檔內容的URL(如果映射包含帶有 `com.adobe.idp.Document` 值)。 下面是服務返回的XML消息的示例，該服務具有名為 `map`。 此參數值是由將字母與 `com.adobe.idp.Document` 對象。
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 非同步調用 {#asynchronous-invocations}

一些AEM Forms服務，如以人為中心的長期服務過程，需要很長的時間才能完成。 這些服務可以以非阻塞方式非同步調用。 (請參閱 [調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。)

通過替換AEM Forms服務 `services` 與 `async_invoke` 中，如下例所示。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

此URL返回負責此調用的作業的標識符值（「文本/純」格式）。

通過使用調用URL和 `services` 取代 `async_status`。 URL必須包含 `job_id` 參數，指定與此調用關聯的作業的標識符值。 例如：

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

此URL返回一個整數值（以「文本/純格式」格式），根據作業管理器的規範對作業狀態進行編碼（例如，2表示正在運行，3表示已完成，4表示失敗，等等）。

如果作業完成，URL將返回與同步調用服務相同的結果。

一旦作業完成並檢索到結果，就可以使用調用URL來處理作業 `services` 替換為 `async_dispose`。 URL還應包含 `job_id` 指定作業標識符值的參數。 例如：

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

如果作業已成功處置，則此URL返回一條空消息。

## 報告錯誤 {#error-reporting}

如果由於伺服器上引發異常而無法完成同步或非同步調用請求，則會將異常報告為HTTP響應消息的一部分。 如果調用URL(或 `async_result` 非同步調用的URL)沒有.xml尾碼，REST提供程式返回HTTP代碼 `500 Internal Server Error` 後跟異常消息。

如果調用URL(或 `async_result` 非同步調用的URL)確實有.xml尾碼，REST提供程式返回HTTP代碼 `200 OK`然後是以下格式描述異常的XML文檔。

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

的 `DSCError` 元素是可選的，並且僅當異常是 `com.adobe.idp.dsc.DSCException`。

## 安全性和身份驗證 {#security-and-authentication}

要為REST調用提供安全傳輸，AEM表單管理員可以在托管AEM Forms的J2EE應用程式伺服器上啟用HTTPS協定。 此配置特定於J2EE應用伺服器；它不是forms伺服器配置的一部分。

>[!NOTE]
>
>作為希望通過REST終結點公開流程的Workbench開發人員，切記XSS漏洞問題。 XSS漏洞可用於竊取或操縱Cookie、修改內容的呈現方式以及危害機密資訊。 如果XSS漏洞是問題，建議使用附加的輸入和輸出資料驗證規則擴展進程邏輯。

## AEM Forms支援REST調用的服務 {#aem-forms-services-that-support-rest-invocation}

儘管建議您調用使用Workbench而不是直接使用服務建立的進程，但是有一些AEM Forms服務確實支援REST調用。 建議您直接調用進程而不是直接調用服務的原因是，調用進程更加高效。 請考慮以下情形。 假定您要從REST客戶端建立策略。 即，您希望REST客戶端定義策略名稱、離線租用期等值。

要建立策略，必須定義複雜資料類型，如 `PolicyEntry` 的雙曲餘切值。 A `PolicyEntry` 對象定義屬性，如與策略關聯的權限。 (請參閱 [建立策略](/help/forms/developing/protecting-documents-policies.md#creating-policies)。)

而不是發送REST請求以建立策略(包括定義複雜資料類型，如 `PolicyEntry` 對象)，建立使用Workbench建立策略的流程。 定義接受基元輸入變數的流程，如定義流程名稱的字串值或定義離線租用期的整數。

這樣，您就不必建立包含操作所需的複雜資料類型的REST調用請求。 該進程定義了複雜的資料類型，而您從REST客戶端執行的所有操作都是調用該進程並傳遞基元資料類型。 有關使用REST調用進程的資訊，請參見 [使用REST調用MyApplication/EncryptDocument進程](#rest-invocation-examples)。

以下清單指定支援直接調用REST的AEM Forms服務。

* Distiller
* Rights Management服務
* 生成PDF服務
* 生成3dPDF服務
* 表單資料整合

## REST調用示例 {#rest-invocation-examples}

提供了以下REST調用示例：

* 將布爾值傳遞給AEM Forms進程
* 將日期值傳遞給AEM Forms進程
* 將檔案傳遞給AEM Forms進程
* 將文檔和文本值傳遞給AEM Forms進程
* 將枚舉值傳遞給AEM Forms進程
* 使用REST調用MyApplication/EncryptDocument進程
* 從Acrobat調用MyApplication/EncryptDocument進程

   每個示例都演示將不同的資料類型傳遞給AEM Forms進程

**將布爾值傳遞給進程**

以下HTML示例將兩個 `Boolean` 值到名為的AEM Forms進程 `RestTest2`。 調用方法的名稱為 `invoke` 版本為1.0。請注意，已使用HTML過帳方法。

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

**將日期值傳遞給流程**

以下HTML示例將日期值傳遞給名為 `SOAPEchoService`。 調用方法的名稱為 `echoCalendar`。 注意HTML `Post` 中。

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

**將文檔傳遞到流程**

以下HTML示例調用名為 `MyApplication/EncryptDocument` 需要PDF檔案。 有關此流程的資訊，請參見 [使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)。

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

**將文檔和文本值傳遞到流程**

以下HTML示例調用名為 `RestTest3` 需要一個文檔和兩個文本值。 請注意，已使用HTML過帳方法。

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

**將枚舉值傳遞到進程**

以下HTML示例調用名為 `SOAPEchoService` 需要枚舉值。 請注意，已使用HTML過帳方法。

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

您可以調用一個名為「AEM Forms」 *MyApplication/EncryptDocument* 使用REST。

>[!NOTE]
>
>該進程不基於現有的AEM Forms進程。 要跟隨代碼示例，請建立一個名為 `MyApplication/EncryptDocument` 使用workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

調用此進程時，它執行以下操作：

1. 獲取傳遞給流程的無擔保PDF文檔。 此操作基於 `SetValue` 的下界。 此進程的輸入參數是 `document` 進程變數命名 `inDoc`。
1. 使用密碼加密PDF文檔。 此操作基於 `PasswordEncryptPDF` 的下界。 密碼加密的PDF文檔在名為 `outDoc`。

   當使用REST請求調用此進程時，加密的PDF文檔將顯示在Web瀏覽器中。 在查看PDF文檔之前，請指定密碼（除非禁用了安全性）。 以下HTML代碼表示對 `MyApplication/EncryptDocument` 處理。

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

**從Acrobat調用MyApplication/EncryptDocument進程** {#invoke-process-acrobat}

您可以使用REST請求從Acrobat調用Forms進程。 例如，可以調用 *MyApplication/EncryptDocument* 處理。 要從Acrobat調用Forms進程，請在設計器內的XDP檔案上放置一個提交按鈕。 (請參閱 [設計器幫助](https://www.adobe.com/go/learn_aemforms_designer_63)。)

指定在按鈕的 *提交到URL* 欄位，如下圖所示。

調用該進程的完整URL為https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument。

如果流程要求將PDF文檔作為輸入值，請確保將表單作為PDF提交，如上圖所示。 此外，要成功調用進程，進程必須返回PDF文檔。 否則，Acroabt無法處理返回值，並出現錯誤。 不必指定輸入進程變數的名稱。 例如， *MyApplication/EncryptDocument* 進程具有名為 `inDoc`。 只要表單被提交為PDF，就不必指定inDoc。

您還可以將表單資料作為XML提交到Forms進程，要提交XML資料，請確保 `Submit As` 下拉清單指定XML。 由於流程的返回值必須是PDF文檔，因此PDF文檔顯示在Acrobat。
