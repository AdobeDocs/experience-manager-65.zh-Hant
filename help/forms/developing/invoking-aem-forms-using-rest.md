---
title: 使用REST要求叫用AEM Forms
description: 使用REST要求叫用Workbench中建立的程式。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 0%

---

# 使用REST要求叫用AEM Forms {#invoking-aem-forms-using-rest-requests}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以設定在Workbench中建立的程式，以便透過代表性狀態轉移(REST)請求叫用它們。 從HTML頁面傳送REST要求。 也就是說，您可以使用REST要求，直接從網頁叫用Forms程式。 例如，您可以開啟網頁的新例項。 接著，您可以叫用Forms程式，並載入轉譯後的PDF檔案，其中包含在HTTPPOST要求中傳送的資料。

存在兩種型別的HTML使用者端。 第一個HTML使用者端是以JavaScript撰寫的AJAX使用者端。 第二個使用者端是包含提交按鈕的HTML表單。 以HTML為基礎的使用者端應用程式並非唯一可能的REST使用者端。 任何支援HTTP要求的使用者端應用程式都可以使用REST叫用來叫用服務。 例如，您可以使用PDF表單中的REST呼叫來呼叫服務。 (請參閱[從Acrobat](#rest-invocation-examples)叫用MyApplication/EncryptDocument程式。)

使用REST要求時，建議您不要直接叫用Forms服務。 而是叫用在Workbench中建立的程式。 當建立要用於REST呼叫的處理程式時，請使用程式化的起點。 在此情況下，REST端點會自動新增。 如需有關在Workbench中建立程式的資訊，請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

當您使用REST叫用服務時，系統會提示您輸入AEM表單使用者名稱和密碼。 但是，如果您不想指定使用者名稱和密碼，則可以停用服務安全性。

若要使用REST叫用Forms服務（流程啟動時會變成服務），請設定REST端點。 （請參閱[管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)中的「管理端點」。）

設定REST端點後，您可以使用HTTPGET方法或POST方法來叫用Forms服務。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必要的`ServiceName`值是要叫用的Forms服務名稱。 選用的`OperationName`值是服務作業的名稱。 如果未指定這個值，這個名稱會預設為`invoke`，這是啟動處理序的作業名稱。 選用的`ServiceVersion`值是以X.Y格式編碼的版本。 如果未指定此值，則會使用最新版本。 `enctype`值也可以是`application/x-www-form-urlencoded`。

## 支援的資料型別 {#supported-data-types}

使用REST要求叫用AEM Forms服務時，支援下列資料型別：

* Java基本資料型別，例如字串和整數
* `com.adobe.idp.Document`資料型別
* XML資料型別，例如`org.w3c.Document`和`org.w3c.Element`
* 集合物件，例如`java.util.List`和`java.util.Map`

  這些資料型別通常被接受為Workbench中建立之程式的輸入值。

  如果以HTTPPOST方法叫用Froms服務，引數會在HTTP要求內文中傳遞。 如果AEM Forms服務的簽章有字串輸入引數，請求內文可包含輸入引數的文字值。 如果服務的簽章定義了多個字串引數，則請求可以遵循HTTP的`application/x-www-form-urlencoded`標籤法，以引數名稱作為表單的欄位名稱。

  如果Forms服務傳回字串引數，結果會是輸出引數的文字表示法。 如果服務傳回多個字串引數，結果會產生XML檔案，以下列格式編碼輸出引數：
  ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

  >[!NOTE]
  >
  >`output-paramater1`值代表輸出引數名稱。

  如果Forms服務需要`com.adobe.idp.Document`引數，則只能使用HTTPPOST方法叫用該服務。 如果服務需要一個`com.adobe.idp.Document`引數，則HTTP要求內文會成為輸入Document物件的內容。

  如果AEM Forms服務需要多個輸入引數，則HTTP要求內文必須是如RFC 1867定義的多部分MIME訊息。 （RFC 1867是網頁瀏覽器用來將檔案上傳至網站的標準。） 每個輸入引數都必須以多部分訊息的個別部分傳送，並以`multipart/form-data`格式編碼。 每個零件的名稱都必須與引數的名稱相符。

  清單與地圖也會當作在Workbench中建立之AEM Forms流程的輸入值。 因此，您可以在使用REST請求時使用這些資料型別。 不支援Java陣列，因為它們未用作AEM Forms程式的輸入值。

  如果輸入引數是清單，REST使用者端可以多次指定引數來傳送它（針對清單中的每個專案指定一次）。 例如，如果A是檔案清單，則輸入必須是包含多個名為A之部分的多部分訊息。在這種情況下，每個名為A的零件都會成為輸入清單中的專案。 如果B是字串清單，則輸入可以是包含多個名為B的欄位的`application/x-www-form-urlencoded`訊息。在這種情況下，每個名為B的表單欄位都會成為輸入清單中的專案。

  如果輸入引數為對應，且為服務專用輸入引數，則輸入訊息的每個部分/欄位都會成為對映中的鍵/值記錄。 每個零件/欄位的名稱會成為記錄的鍵。 每個部分/欄位的內容會成為記錄的值。

  如果輸入對應不是僅服務輸入引數，則屬於對應的每個索引鍵/值記錄都可以使用名為的引數來傳送，該引數為引數名稱和記錄的索引鍵的串連。 例如，名為`attributes`的輸入對應可以隨下列索引鍵/值配對清單一起傳送：

  `attributesColor=red`

  `attributesShape=box`

  `attributesWidth=5`

  這會轉譯成包含三個記錄的地圖： `Color=red`、`Shape=box`和`Width=5`。

  清單和對應型別的輸出引數會成為結果XML訊息的一部分。 輸出清單以XML表示為一系列的XML元素，清單中的每個專案都有一個元素。 每個元素都會獲得與輸出清單引數相同的名稱。 每個XML元素的值是下列兩個專案之一：

* 清單中專案的文字表示（如果清單包含字串型別）
* 指向檔案內容的URL （如果清單包含`com.adobe.idp.Document`個物件）

  下列範例是服務傳回的XML訊息，其單一輸出引數名為&#x200B;*list*，為整數清單。
  ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`輸出map引數在產生的XML訊息中以一系列XML元素表示，對應中的每個記錄都有一個元素。 每個元素的名稱都和對應記錄的鍵相同。 每個元素的值是對應記錄值的文字表示（如果對應包含具有字串值的記錄）或指向檔案內容的URL （如果對應包含具有`com.adobe.idp.Document`值的記錄）。 以下是服務傳回的XML訊息範例，此服務具有名為`map`的單一輸出引數。 此引數值是由字母與`com.adobe.idp.Document`物件關聯的記錄所組成的對映。
  ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 非同步叫用 {#asynchronous-invocations}

有些AEM Forms服務（例如以人為中心的長期流程）需要很長時間才能完成。 這些服務可以非同步方式叫用，而不會造成封鎖。 （請參閱[叫用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

可在叫用URL中以`async_invoke`取代`services`，以非同步叫用AEM Forms服務，如下列範例所示。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

此URL會傳回負責此叫用之工作的識別碼值（以「文字/純」格式）。

使用以`services`取代為`async_status`的引動URL，可以擷取非同步引動的狀態。 URL必須包含`job_id`引數，以指定與此呼叫相關之工作的識別碼值。 例如：

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

此URL會根據工作管理員的規格傳回一個整數值（以「文字/純文字」格式）來編碼工作狀態（例如2表示正在執行、3表示已完成、4表示失敗等）。

如果工作完成，URL會傳回與同步叫用服務相同的結果。

工作完成並擷取結果後，可以使用具有`services`的引動URL將工作處置為`async_dispose`。 URL也應包含指定工作識別碼值的`job_id`引數。 例如：

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

如果成功處置工作，此URL會傳回空白訊息。

## 錯誤報告 {#error-reporting}

如果因為伺服器上擲回例外狀況而無法完成同步或非同步呼叫要求，例外狀況會回報為HTTP回應訊息的一部分。 如果引動URL （或如果發生非同步引動，則為`async_result` URL）沒有.xml尾碼，則REST提供者會傳回HTTP代碼`500 Internal Server Error`，然後傳回例外狀況訊息。

如果引動URL （或如果發生非同步引動，則為`async_result` URL）確實有.xml尾碼，則REST提供者會傳回HTTP代碼`200 OK`，後面接著以下列格式描述例外狀況的XML檔案。

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

`DSCError`專案是選用專案，而且只有在例外狀況是`com.adobe.idp.dsc.DSCException`的執行個體時才會出現。

## 安全性與驗證 {#security-and-authentication}

為了提供REST呼叫的安全傳輸，AEM Forms管理員可以在裝載AEM Forms的J2EE應用程式伺服器上啟用HTTPS通訊協定。 此設定專用於J2EE應用程式伺服器；它不是Forms伺服器設定的一部分。

>[!NOTE]
>
>作為想要透過REST端點公開您的流程的Workbench開發人員，請記住XSS弱點問題。 XSS漏洞可以用來竊取或操縱Cookie、修改內容的呈現方式，以及危害機密資訊。 如果XSS弱點是個問題，建議您使用其他輸入和輸出資料驗證規則來擴充流程邏輯。

## 支援REST叫用的AEM Forms服務 {#aem-forms-services-that-support-rest-invocation}

雖然建議您叫用使用Workbench而非直接服務所建立的程式，但還是有一些支援REST叫用的AEM Forms服務。 建議您叫用處理序而非直接叫用服務的原因，是因為叫用處理序更有效率。 請考量下列情況。 假設您要從REST使用者端建立原則。 也就是說，您希望REST使用者端定義原則名稱、離線租期等值。

若要建立原則，您必須定義複雜的資料型別，例如`PolicyEntry`物件。 `PolicyEntry`物件定義與原則關聯的屬性，例如許可權。 （請參閱[建立原則](/help/forms/developing/protecting-documents-policies.md#creating-policies)。）

不要傳送REST要求來建立原則（將包括定義複雜的資料型別，例如`PolicyEntry`物件），而是使用Workbench建立建立原則的程式。 定義程式以接受基本輸入變數，例如定義程式名稱的字串值，或定義離線租期的整數。

如此一來，您就不必建立包含作業所需複雜資料型別的REST呼叫要求。 程式會定義複雜的資料型別，而您從REST使用者端所做的一切就是叫用程式並傳遞基本資料型別。 如需有關使用REST叫用處理序的資訊，請參閱[使用REST叫用MyApplication/EncryptDocument處理序](#rest-invocation-examples)。

下列清單指定支援直接REST呼叫的AEM Forms服務。

* Distiller服務
* Rights Management服務
* GeneratePDF服務
* Generate3dPDF服務
* FormDataIntegration

## REST引動範例 {#rest-invocation-examples}

提供下列REST呼叫範例：

* 將布林值傳遞至AEM Forms程式
* 將日期值傳遞至AEM Forms程式
* 將檔案傳遞至AEM Forms程式
* 將檔案和文字值傳遞至AEM Forms程式
* 將分項清單值傳遞至AEM Forms程式
* 使用REST叫用MyApplication/EncryptDocument程式
* 從Acrobat叫用MyApplication/EncryptDocument程式

  每個範例都會示範如何將不同的資料型別傳遞至AEM Forms程式

**傳遞布林值給處理序**

下列HTML範例將兩個`Boolean`值傳遞至名為`RestTest2`的AEM Forms處理序。 叫用方法的名稱是`invoke`，而版本是1.0。請注意，已使用HTMLPost方法。

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

**傳遞日期值給處理序**

下列HTML範例將日期值傳遞至名為`SOAPEchoService`的AEM Forms程式。 叫用方法的名稱為`echoCalendar`。 請注意，已使用HTML`Post`方法。

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

**傳遞檔案至處理序**

下列HTML範例會叫用名為`MyApplication/EncryptDocument`且需要PDF檔案的AEM Forms程式。 如需此程式的相關資訊，請參閱[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)。

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

**傳遞檔案和文字值至處理序**

以下HTML範例會叫用名為`RestTest3`的AEM Forms處理序，此處理序需要檔案和兩個文字值。 請注意，已使用HTMLPost方法。

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

**傳遞列舉值給處理序**

下列HTML範例會叫用名為`SOAPEchoService`且需要列舉值的AEM Forms處理序。 請注意，已使用HTMLPost方法。

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

**使用REST叫用MyApplication/EncryptDocument程式**

您可以使用REST叫用名為&#x200B;*MyApplication/EncryptDocument*&#x200B;的AEM Forms短期處理序。

>[!NOTE]
>
>此程式並非以現有AEM Forms程式為基礎。 若要遵循程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

叫用此程式時，會執行下列動作：

1. 取得傳遞至程式的不安全PDF檔案。 此動作是以`SetValue`作業為基礎。 此處理序的輸入引數是名為`inDoc`的`document`處理序變數。
1. 使用密碼加密PDF檔案。 此動作是以`PasswordEncryptPDF`作業為基礎。 密碼加密的PDF檔案傳回名為`outDoc`的程式變數。

   使用REST要求叫用此程式時，加密的PDF檔案會顯示在網頁瀏覽器中。 在檢視PDF檔案之前，您必須指定密碼（除非已停用安全性）。 下列HTML程式碼代表對`MyApplication/EncryptDocument`處理序的REST呼叫要求。

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

您可以使用REST要求，從Acrobat叫用Forms程式。 例如，您可以叫用&#x200B;*MyApplication/EncryptDocument*&#x200B;程式。 若要從Acrobat叫用Forms程式，請在Designer內的XDP檔案上放置提交按鈕。 (請參閱[Designer說明](https://www.adobe.com/go/learn_aemforms_designer_63)。)

在按鈕的&#x200B;*送出至URL*&#x200B;欄位中指定要叫用處理序的URL，如下圖所示。

叫用處理程式的完整URL為https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument。

如果程式需要PDF檔案作為輸入值，請確保您以PDF提交表單，如上圖所示。 此外，若要成功叫用處理序，處理序必須傳回PDF檔案。 否則Acroabt無法處理傳回值，並發生錯誤。 您不必指定輸入程式變數的名稱。 例如，*MyApplication/EncryptDocument*&#x200B;處理序有一個名為`inDoc`的輸入變數。 只要表單已提交為PDF，您就不需要指定inDoc。

您也可以將表單資料以XML形式提交至Forms程式。若要提交XML資料，請確定`Submit As`下拉式清單指定XML。 由於流程的傳回值必須是PDF檔案，因此PDF檔案會顯示在Acrobat中。
