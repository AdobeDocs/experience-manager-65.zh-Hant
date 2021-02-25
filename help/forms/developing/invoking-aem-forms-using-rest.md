---
title: 使用REST請求叫用AEM Forms
seo-title: 使用REST請求叫用AEM Forms
description: 使用REST請求調用在Workbench中建立的流程。
seo-description: 使用REST請求調用在Workbench中建立的流程。
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 0%

---


# 使用REST請求叫用AEM Forms {#invoking-aem-forms-using-rest-requests}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

可以配置在Workbench中建立的流程，以便通過「代表性狀態轉移(REST)」請求調用這些流程。 REST請求是從HTML頁面傳送。 也就是說，您可以使用REST請求直接從網頁叫用表單程式。 例如，您可以開啟網頁的新例項。 接著，您可以叫用表單程式，並載入轉譯的PDF檔案，其中包含以HTTP POST請求傳送的資料。

HTML用戶端有兩種類型。 第一個HTML用戶端是以JavaScript編寫的AJAX用戶端。 第二個用戶端是包含送出按鈕的HTML表單。 基於HTML的客戶端應用程式並非唯一可能的REST客戶端。 任何支援HTTP請求的客戶端應用程式都可以使用REST調用來調用服務。 例如，您可以使用PDF表單的REST呼叫來叫用服務。 （請參閱[從Acrobat叫用MyApplication/EncryptDocument程式。）](#rest-invocation-examples)

使用REST請求時，建議您不要直接叫用Forms服務。 請改為叫用在Workbench中建立的流程。 建立用於調用REST的流程時，請使用程式化起點。 在這種情況下，會自動添加REST端點。 有關在Workbench中建立流程的資訊，請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

當您使用REST叫用服務時，系統會提示您輸入AEM表單的使用者名稱和密碼。 不過，如果您不想指定使用者名稱和密碼，則可停用服務安全性。

要使用REST調用Forms服務（當激活進程時，進程將變為服務），請配置REST端點。 （請參閱[管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)中的「管理端點」。）

在配置REST端點後，您可以使用HTTP GET方法或POST方法來叫用Forms服務。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

強制`ServiceName`值是要調用的Forms服務的名稱。 可選`OperationName`值是服務操作的名稱。 如果未指定此值，則此名稱預設為`invoke` ，即啟動進程的操作名。 可選`ServiceVersion`值是以X.Y格式編碼的版本。 如果未指定此值，則會使用最新版本。 `enctype`值也可以是`application/x-www-form-urlencoded`。

## 支援的資料類型{#supported-data-types}

使用REST請求叫用AEM Forms服務時，支援下列資料類型：

* Java基本資料類型，例如字串和整數
* `com.adobe.idp.Document` 資料類型
* XML資料類型，如`org.w3c.Document`和`org.w3c.Element`
* 收集物件，例如`java.util.List`和`java.util.Map`

   這些資料類型通常被接受為在Workbench中建立之程式的輸入值。

   如果使用HTTP POST方法調用Froms服務，則會在HTTP請求主體內傳遞參數。 如果AEM Forms服務的簽名有字串輸入參數，請求主體可以包含輸入參數的文字值。 如果服務的簽名定義多個字串參數，請求可遵循HTTP的`application/x-www-form-urlencoded`符號，並使用參數名稱做為表單的欄位名稱。

   如果Forms服務返回字串參數，則結果是輸出參數的文本表示。 如果服務返回多個字串參數，則結果是XML文檔以下列格式對輸出參數進行編碼：
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >`output-paramater1`值代表輸出參數名稱。

   如果Forms服務需要`com.adobe.idp.Document`參數，則只能使用HTTP POST方法調用該服務。 如果服務需要一個`com.adobe.idp.Document`參數，HTTP請求主體將成為輸入的Document對象的內容。

   如果AEM Forms服務需要多個輸入參數，HTTP請求主體必須是RFC 1867所定義的多部分MIME訊息。 （RFC 1867是Web瀏覽器將檔案上傳到網站的標準。） 每個輸入參數都必須作為多部分消息的單獨部分發送，並以`multipart/form-data`格式編碼。 每個部件的名稱必須與參數的名稱匹配。

   清單和地圖也會用作在Workbench中建立的AEM Forms流程的輸入值。 因此，在使用REST請求時，您可以使用這些資料類型。 不支援Java陣列，因為它們不會用作AEM Forms程式的輸入值。

   如果輸入參數是清單，REST客戶端可以通過多次指定該參數來發送該參數（對於清單中的每個項，一次）。 例如，如果A是文檔清單，則輸入必須是由多個名為A的部件組成的多部件消息。在這種情況下，每個名為A的部件都將成為輸入清單中的項目。 如果B是字串清單，則輸入可以是`application/x-www-form-urlencoded`訊息，包含多個名為B的欄位。在這種情況下，每個名為B的表單欄位都會變成輸入清單中的項目。

   如果輸入參數是映射，並且它是僅服務的輸入參數，則輸入消息的每個部分／欄位將成為映射中的鍵／值記錄。 每個部件／欄位的名稱會成為記錄的索引鍵。 每個部件／欄位的內容都會變成記錄的值。

   如果輸入映射不是僅服務的輸入參數，則可使用名為參數名稱與記錄密鑰的串連的參數來傳送屬於映射的每個鍵／值記錄。 例如，可以隨下列鍵／值對的清單發送名為`attributes`的輸入映射：

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   這可以轉化為三個記錄的地圖：`Color=red`、`Shape=box`和`Width=5`。

   清單和映射類型的輸出參數將成為生成的XML消息的一部分。 輸出清單以XML表示為一系列XML元素，每個元素在清單中各有一個元素。 每個元素的名稱都與輸出清單參數相同。 每個XML元素的值是兩個方面之一：

* 清單中項的文本表示（如果清單包含字串類型）
* 指向「文檔」內容的URL（如果清單包含`com.adobe.idp.Document`對象）

   以下示例是服務返回的XML消息，該服務具有名為&#x200B;*list*的單一輸出參數，該參數是整數清單。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`輸出映射參數被表示為一系列的XML元素，每個元素用於映射中的每個記錄。每個元素的名稱都與地圖記錄的索引鍵相同。 每個元素的值是地圖記錄值的文字表示法（如果地圖包含含有字串值的記錄），或是指向檔案內容的URL（如果地圖包含具有`com.adobe.idp.Document`值的記錄）。 以下是服務返回的XML消息示例，該服務具有名為`map`的單個輸出參數。 此參數值是由將字母與`com.adobe.idp.Document`對象關聯的記錄組成的映射。
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 非同步調用{#asynchronous-invocations}

有些AEM Forms服務（例如以人為中心的長期流程）需要很長的時間才能完成。 這些服務可以以非阻塞方式非同步調用。 （請參閱[叫用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

AEM Forms服務可以非同步呼叫，方法是在呼叫URL中以`async_invoke`取代`services`，如下列範例所示。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

此URL會傳回負責此呼叫之工作的識別碼值（以「文字／純文字」格式）。

可以使用用`async_status`替換的`services`調用URL來檢索非同步調用的狀態。 URL必須包含`job_id`參數，該參數指定與此調用相關聯的作業的標識符值。 例如：

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

此URL會傳回整數值（以「文字／純」格式），根據「工作管理員」的規格來編碼工作狀態（例如，2表示執行、3表示完成、4表示失敗等）。

如果作業完成，URL會傳回與同步呼叫服務相同的結果。

一旦作業完成並檢索結果，就可以使用具有`services`的調用URL替換`async_dispose`來處理作業。 URL也應包含`job_id`參數，用以指定工作的識別碼值。 例如：

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

如果作業已成功處理，此URL會傳回空白訊息。

## 報告{#error-reporting}時出錯

如果由於伺服器上拋出異常而無法完成同步或非同步調用請求，則會將異常報告為HTTP響應消息的一部分。 如果調用URL（或非同步調用的`async_result` URL）沒有。xml尾碼，REST提供程式將返回HTTP代碼`500 Internal Server Error`，後面跟有例外消息。

如果調用URL（或非同步調用的`async_result` URL）具有。xml尾碼，REST提供程式將返回HTTP代碼`200 OK`，後面跟有以下格式描述異常的XML文檔。

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

`DSCError`元素是可選的，且僅當例外為`com.adobe.idp.dsc.DSCException`的例項時才會顯示。

## 安全性和身份驗證{#security-and-authentication}

若要為REST呼叫提供安全傳輸，AEM Forms管理員可在代管AEM Forms的J2EE應用程式伺服器上啟用HTTPS通訊協定。 此組態是J2EE應用程式伺服器專用的；它不是表單伺服器組態的一部分。

>[!NOTE]
>
>身為想要透過REST端點公開您程式的Workbench開發人員，請記住XSS弱點問題。 XSS弱點可用來竊取或操縱Cookie、修改內容的呈現方式，以及危害機密資訊。 如果存在XSS弱點，建議您使用額外的輸入與輸出資料驗證規則來擴充程式邏輯。

## 支援REST呼叫{#aem-forms-services-that-support-rest-invocation}的AEM Forms服務

雖然建議您叫用使用Workbench建立的程式，而非直接使用服務，但是有些AEM Forms服務確實支援REST呼叫。 建議您直接叫用程式而不是直接叫用服務的原因，是因為叫用程式更有效。 請考慮以下情況。 假設您要從REST客戶端建立策略。 也就是說，您希望REST客戶端定義策略名稱、離線租用期間等值。

要建立策略，必須定義複雜的資料類型，如`PolicyEntry`對象。 `PolicyEntry`物件定義屬性，例如與原則相關的權限。 （請參閱[建立策略](/help/forms/developing/protecting-documents-policies.md#creating-policies)。）

與其發送REST請求以建立策略（包括定義複雜資料類型，如`PolicyEntry`對象），請使用Workbench建立策略的流程。 定義流程以接受基本輸入變數，例如定義流程名稱的字串值或定義離線租用期間的整數。

這樣，您就不必建立包含操作所需的複雜資料類型的REST調用請求。 該流程定義了複雜的資料類型，您從REST客戶端所做的就是調用該流程並傳遞基本資料類型。 有關使用REST調用進程的資訊，請參見[使用REST調用MyApplication/EncryptDocument進程。](#rest-invocation-examples)

下列清單會指定支援直接REST呼叫的AEM Forms服務。

* Distiller服務
* Rights Management服務
* GeneratePDF服務
* 產生3dPDF服務
* FormDataIntegration

## REST調用示例{#rest-invocation-examples}

提供了以下REST調用示例：

* 將布林值傳入AEM Forms程式
* 將日期值傳入AEM Forms程式
* 將檔案傳送至AEM Forms程式
* 將檔案和文字值傳遞至AEM Forms程式
* 將列舉值傳遞至AEM Forms程式
* 使用REST調用MyApplication/EncryptDocument進程
* 從Acrobat叫用MyApplication/EncryptDocument程式

   每個範例都示範將不同的資料類型傳遞至AEM Forms程式

**將布爾值傳遞至流程**

下列HTML範例會將兩個`Boolean`值傳遞給名為`RestTest2`的AEM Forms程式。 調用方法的名稱為`invoke` ，版本為1.0。請注意，已使用HTML Post方法。

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

**將日期值傳遞至流程**

下列HTML範例會將日期值傳遞至名為`SOAPEchoService`的AEM Forms程式。 調用方法的名稱為`echoCalendar`。 請注意，已使用HTML `Post`方法。

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

**將檔案傳遞至流程**

以下HTML範例會叫用名為`MyApplication/EncryptDocument`的AEM Forms程式，此程式需要PDF檔案。 如需此程式的詳細資訊，請參閱[使用MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)叫用AEM表單。

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

**將檔案和文字值傳遞至程式**

以下HTML範例會叫用名為`RestTest3`的AEM Forms程式，此程式需要一個檔案和兩個文字值。 請注意，已使用HTML Post方法。

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

您可以使用REST來叫用名為&#x200B;*MyApplication/EncryptDocument*&#x200B;的AEM Forms短期程式。

>[!NOTE]
>
>此程式不以現有的AEM Forms程式為基礎。 要跟隨代碼示例，請使用工作台建立名為`MyApplication/EncryptDocument`的流程。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

調用此進程時，它執行以下操作：

1. 取得傳遞至程式的不安全PDF檔案。 此操作基於`SetValue`操作。 此進程的輸入參數是名為`inDoc`的`document`進程變數。
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 密碼加密的PDF檔案會在名為`outDoc`的流程變數中傳回。

   當使用REST請求呼叫此程式時，加密的PDF檔案會顯示在網頁瀏覽器中。 在檢視PDF檔案之前，請先指定密碼（除非已停用安全性）。 以下HTML代碼表示對`MyApplication/EncryptDocument`進程的REST調用請求。

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

您可以使用REST要求從Acrobat叫用表單程式。 例如，您可以叫用&#x200B;*MyApplication/EncryptDocument*&#x200B;程式。 若要從Acrobat叫用表單程式，請在Designer中的XDP檔案上放置送出按鈕。 （請參閱[設計人員說明](https://www.adobe.com/go/learn_aemforms_designer_63)。）

指定URL以叫用按鈕的「送出至URL *」欄位中的程式，如下圖所示。*

要叫用此程式的完整URL為https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument。

如果程式需要PDF檔案作為輸入值，請確定您以PDF格式提交表單，如上圖所示。 此外，若要成功叫用程式，程式必須傳回PDF檔案。 否則，Acrobat無法處理返回值，並會出現錯誤。 您不必指定輸入流程變數的名稱。 例如，*MyApplication/EncryptDocument*&#x200B;程式具有名為`inDoc`的輸入變數。 只要表單已提交為PDF，您就不需要指定inDoc。

您也可以以XML格式將表單資料提交至表單流程，若要提交XML資料，請確定`Submit As`下拉式清單指定XML。 由於程式的返回值必須是PDF檔案，因此PDF檔案會顯示在Acrobat中。
