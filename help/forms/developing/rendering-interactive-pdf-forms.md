---
title: 轉譯互動式PDF forms
seo-title: 轉譯互動式PDF forms
description: 使用Forms服務向用戶端裝置（通常為網頁瀏覽器）轉譯互動式PDF forms，以收集使用者的資訊。 您可以使用Forms服務，使用Java API和網站服務API來轉譯互動式表單。
seo-description: 使用Forms服務向用戶端裝置（通常為網頁瀏覽器）轉譯互動式PDF forms，以收集使用者的資訊。 您可以使用Forms服務，使用Java API和網站服務API來轉譯互動式表單。
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2528'
ht-degree: 0%

---

# 呈現互動式PDF forms{#rendering-interactive-pdf-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

Forms服務會將互動式PDF forms轉譯給用戶端裝置（通常是網頁瀏覽器），以收集使用者的資訊。 轉譯互動式表單後，使用者可以在表單欄位中輸入資料，然後按一下表單上的提交按鈕，將資訊傳回Forms服務。 Adobe Reader或Acrobat必須安裝在托管用戶端網頁瀏覽器的電腦上，才能顯示互動式PDF表單。

>[!NOTE]
>
>使用Forms服務演算表單之前，請先建立表單設計。 通常，表單設計會在設計工具中建立，並儲存為XDP檔案。 如需建立表單設計的相關資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

**貸款申請示例**

推出了範例貸款應用程式，以示範Forms服務如何使用互動式表單來收集使用者的資訊。 此應用程式可讓使用者填寫表單，其中含有確保貸款安全所需的資料，然後將資料提交至Forms服務。 下圖顯示貸款應用程式的邏輯流程。

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

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
   <td><p>從HTML頁面叫用<code>GetLoanForm</code> Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Java Servlet使用Forms服務客戶端API來向客戶端Web瀏覽器呈現貸款表單。 （請參閱<a href="#render-an-interactive-pdf-form-using-the-java-api">使用Java API</a>轉譯互動式PDF表單。）</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用戶填寫貸款表並按一下提交按鈕後，資料將提交到<code>HandleData</code> Java Servlet。 （請參閱<i>"貸款表"</i>。）</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p><code>HandleData</code> Java Servlet使用Forms服務用戶端API來處理表單提交和擷取表單資料。 然後，將資料儲存在企業資料庫中。 (請參閱<a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">處理已提交的Forms</a>。)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>確認表格會呈現回網頁瀏覽器。 使用者的名字和姓氏等資料在轉譯前會與表單合併。 (請參閱<a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">使用可流動配置預填Forms</a>。)</p></td>
  </tr>
 </tbody>
</table>

**貸款表**

此互動式貸款表單由範例貸款應用程式的`GetLoanForm` Java Servlet轉譯。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**確認表**

此表單由範例貸款應用程式的`HandleData` Java Servlet呈現。

![ri_ri_confirm](assets/ri_ri_confirm.png)

`HandleData` Java Servlet會以使用者的名字和姓氏以及金額預先填入此表單。 預先填入表單後，表單會傳送至用戶端網頁瀏覽器。 (請參閱[使用可流動配置預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlet**

範例貸款應用程式是以Java Servlet存在的Forms服務應用程式的範例。 Java Servlet是在J2EE應用程式伺服器（如WebSphere）上運行的Java程式，包含Forms服務客戶端API代碼。

以下代碼顯示名為GetLoanForm的Java Servlet的語法：

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

通常，您不會將Forms服務用戶端API程式碼放入Java Servlet的`doGet`或`doPost`方法中。 將此程式碼放置在個別類別中、從`doPost`方法（或`doGet`方法）實例化類別，並呼叫適當方法，是較佳的程式設計實務。 不過，為了簡化程式碼，本區段中的程式碼範例會維持在最小值，且程式碼範例會放置在`doPost`方法中。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

**步驟摘要**

要呈現互動式PDF表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 指定URI值。
1. 將檔案附加到表單（可選）。
1. 轉譯互動式PDF表單。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms Client API物件，才能以程式設計方式執行Forms服務用戶端API作業。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms Web服務API，請建立`FormsService`物件。

**指定URI值**

您可以指定Forms服務呈現表單所需的URI值。 儲存為Forms應用程式一部分的表單設計，可使用內容根URI值`repository:///`來參照。 例如，請考慮以下名為&#x200B;*Loan.xdp*&#x200B;的表單設計，該表單設計位於名為&#x200B;*FormsApplication*&#x200B;的Forms應用程式中：

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

若要存取此表單設計，請指定`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`作為表單名稱（傳遞至`renderPDFForm`方法的第一個參數），指定`repository:///`作為內容根URI值。

>[!NOTE]
>
>如需使用Workbench建立Forms應用程式的相關資訊，請參閱[Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位於Forms應用程式中之資源的路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值顯示一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

呈現互動式表單時，您可以定義URI值，例如張貼表單資料的目標URL。 目標URL可透過下列其中一種方式定義：

* 在Designer中設計表單設計時的「提交」按鈕
* 使用Forms服務用戶端API

如果目標URL是在表單設計中定義，請勿以Forms服務用戶端API覆寫它。 也就是說，使用Forms API設定目標URL會將表單設計中指定的URL重設為使用API指定的URL。 如果要將PDF表單提交到表單設計中指定的目標URL，請以程式設計方式將目標URL設定為空字串。

如果您的表單包含提交按鈕和計算按鈕（具有在伺服器上運行的相應指令碼），則可以以寫程式方式定義表單要發送到的URL以執行指令碼。 使用表單設計上的提交按鈕，指定張貼表單資料的URL。 （請參閱[計算表單資料](/help/forms/developing/calculating-form-data.md)。）

>[!NOTE]
>
>您也可以將`com.adobe.idp.Document`例項傳遞至Forms服務，而不是指定URL值以參考XDP檔案。 `com.adobe.idp.Document`實例包含表單設計。 (請參閱[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)。)

**將檔案附加到表單**

您可以將檔案附加到表單。 在您轉譯含有檔案附件的PDF表單時，使用者可以使用檔案附件窗格在Acrobat中擷取檔案附件。 您可以將不同的檔案類型附加到表單（如文本檔案）或二進位檔案（如JPG檔案）。

>[!NOTE]
>
>將檔案附件附加到表單是可選的。

**轉譯互動式PDF表單**

若要呈現表單，請使用在Designer中建立並儲存為XDP或PDF檔案的表單設計。 您也可以轉譯使用Acrobat建立並儲存為PDF檔案的表單。 要呈現互動式PDF表單，請調用`FormsServiceClient`對象的`renderPDFForm`方法或`renderPDFForm2`方法。

`renderPDFForm`使用`URLSpec`物件。 XDP檔案的內容根會使用`URLSpec`物件的`setContentRootURI`方法傳遞至Forms服務。 表單設計名稱(`formQuery`)會以單獨的參數值傳遞。 這兩個值會串連，以取得表單設計的絕對參照。

`renderPDFForm2`方法接受要呈現的`com.adobe.idp.Document`實例，該實例包含XDP或PDF文檔。

>[!NOTE]
>
>如果輸入文檔是PDF文檔，則無法設定標籤的PDF運行時選項。 如果輸入檔案是XDP檔案，則可以設定標籤的PDF選項。

## 使用Java API {#render-an-interactive-pdf-form-using-the-java-api}轉譯互動式PDF表單

使用Forms API(Java)轉譯互動式PDF表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormsServiceClient`物件。

1. 指定URI值

   * 建立`URLSpec`對象，該對象使用其建構子儲存URI值。
   * 叫用`URLSpec`物件的`setApplicationWebRoot`方法，並傳遞代表應用程式Web根的字串值。
   * 調用`URLSpec`對象的`setContentRootURI`方法並傳遞指定內容根URI值的字串值。 確保表單設計位於內容根URI中。 否則，Forms服務會擲回例外狀況。 要引用儲存庫，請指定`repository:///`。
   * 叫用`URLSpec`物件的`setTargetURL`方法，並傳遞字串值，指定將表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單要傳送到哪個URL，以執行計算。

1. 將檔案附加到表單

   * 使用`java.util.HashMap`對象的建構子建立對象以儲存檔案附件。
   * 為每個檔案調用`java.util.HashMap`對象的`put`方法，以附加到呈現的表單。 將下列值傳遞至此方法：

      * 指定檔案附件名稱的字串值，包括檔案名副檔名。
   * 包含檔案附件的`com.adobe.idp.Document`對象。

   >[!NOTE]
   >
   >對要附加到表單的每個檔案重複此步驟。 此步驟為選用步驟，如果您不想傳送檔案附件，則可以傳遞`null`。

1. 轉譯互動式PDF表單

   調用`FormsServiceClient`對象的`renderPDFForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 這是可選參數，如果您不想指定運行時選項，可以指定`null`。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。

   `renderPDFForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 調用`FormsResult`對象s `getOutputContent`方法，建立`com.adobe.idp.Document`對象。
   * 調用`getContentType`方法，獲取`com.adobe.idp.Document`對象的內容類型。
   * 通過調用`setContentType`方法並傳遞`com.adobe.idp.Document`對象的內容類型來設定`javax.servlet.http.HttpServletResponse`對象的內容類型。
   * 通過調用`javax.servlet.http.HttpServletResponse`對象的`getOutputStream`方法，建立用於將表單資料流寫入客戶端Web瀏覽器的`javax.servlet.ServletOutputStream`對象。
   * 調用`com.adobe.idp.Document`對象的`getInputStream`方法，建立`java.io.InputStream`對象。
   * 叫用`InputStream`物件的`read`方法，並將位元組陣列傳遞為引數，借此建立位元組陣列，並填入表單資料流。
   * 調用`javax.servlet.ServletOutputStream`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

## 使用Web服務API {#render-an-interactive-pdf-form-using-the-web-service-api}轉譯互動式PDF表單

使用Forms API（網站服務）轉譯互動式PDF表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`物件並設定驗證值。

1. 指定URI值

   * 建立`URLSpec`對象，該對象使用其建構子儲存URI值。
   * 叫用`URLSpec`物件的`setApplicationWebRoot`方法，並傳遞代表應用程式Web根的字串值。
   * 調用`URLSpec`對象的`setContentRootURI`方法並傳遞指定內容根URI值的字串值。 確保表單設計位於內容根URI中。 否則，Forms服務會擲回例外狀況。 要引用儲存庫，請指定`repository:///`。
   * 叫用`URLSpec`物件的`setTargetURL`方法，並傳遞字串值，指定將表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單要傳送到哪個URL，以執行計算。

1. 將檔案附加到表單

   * 使用`java.util.HashMap`對象的建構子建立對象以儲存檔案附件。
   * 為每個檔案調用`java.util.HashMap`對象的`put`方法，以附加到呈現的表單。 將下列值傳遞至此方法：

      * 指定檔案附件名稱的字串值，包括檔案名副檔名
   * 包含檔案附件的`BLOB`對象

   >[!NOTE]
   >
   >對要附加到表單的每個檔案重複此步驟。

1. 轉譯互動式PDF表單

   調用`FormsService`對象的`renderPDFForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞`null`。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 這是可選參數，如果您不想指定運行時選項，可以指定`null`。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。
   * 由方法填入的空`com.adobe.idp.services.holders.BLOBHolder`物件。 這可用來儲存轉譯的PDF表單。
   * 由方法填入的空`javax.xml.rpc.holders.LongHolder`物件。 （此引數會以表單儲存頁數。）
   * 由方法填入的空`javax.xml.rpc.holders.StringHolder`物件。 （此參數將儲存區域設定值。）
   * 將包含此操作結果的空`com.adobe.idp.services.holders.FormsResultHolder`對象。

   `renderPDFForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個引數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 獲取`com.adobe.idp.services.holders.FormsResultHolder`對象的`value`資料成員的值，以建立`FormResult`對象。
   * 調用`FormsResult`對象的`getOutputContent`方法，建立包含表單資料的`BLOB`對象。
   * 調用`getContentType`方法，獲取`BLOB`對象的內容類型。
   * 通過調用`setContentType`方法並傳遞`BLOB`對象的內容類型來設定`javax.servlet.http.HttpServletResponse`對象的內容類型。
   * 通過調用`javax.servlet.http.HttpServletResponse`對象的`getOutputStream`方法，建立用於將表單資料流寫入客戶端Web瀏覽器的`javax.servlet.ServletOutputStream`對象。
   * 建立位元組陣列，並調用`BLOB`對象的`getBinaryData`方法來填入。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 調用`javax.servlet.http.HttpServletResponse`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務轉譯表單時，會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 寫入客戶端Web瀏覽器時，用戶可以看到該表單。
