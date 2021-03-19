---
title: 轉換互動式PDF forms
seo-title: 轉換互動式PDF forms
description: 使用Forms服務，向用戶端裝置（通常是網頁瀏覽器）轉譯互動式PDF forms，以收集使用者的資訊。 您可以使用Forms服務，使用Java API和Web服務API來轉換互動式表單。
seo-description: 使用Forms服務，向用戶端裝置（通常是網頁瀏覽器）轉譯互動式PDF forms，以收集使用者的資訊。 您可以使用Forms服務，使用Java API和Web服務API來轉換互動式表單。
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2529'
ht-degree: 0%

---


# 呈現互動式PDF forms{#rendering-interactive-pdf-forms}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

Forms服務會將互動式PDF forms轉譯至用戶端裝置（通常是網頁瀏覽器），以收集使用者的資訊。 在轉譯互動式表單後，使用者可以在表單欄位中輸入資料，然後按一下表單上的提交按鈕，將資訊傳回Forms服務。 Adobe Reader或Acrobat必須安裝在代管用戶端網頁瀏覽器的電腦上，才能顯示互動式PDF表格。

>[!NOTE]
>
>在您使用Forms服務演算表格之前，請先建立表格設計。 通常，表單設計是在Designer中建立，並儲存為XDP檔案。 有關建立表單設計的資訊，請參閱[Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63)。

**貸款申請範例**

引入一個貸款申請範例，以示範Forms服務如何使用互動式表單來收集使用者的資訊。 此應用程式可讓使用者填寫表單，填入保證貸款安全所需的資料，然後將資料提交至Forms服務。 下圖顯示貸款申請的邏輯流程。

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
   <td><p><code>GetLoanForm</code> Java Servlet是從HTML頁調用的。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Java Servlet使用Forms服務客戶端API向客戶端Web瀏覽器呈現貸款表單。 （請參閱<a href="#render-an-interactive-pdf-form-using-the-java-api">使用Java API</a>轉換互動式PDF表單。）</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>當使用者填入貸款表單並按一下提交按鈕後，資料就會送出至<code>HandleData</code> Java Servlet。 （請參閱<i>"貸款表"</i>）。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p><code>HandleData</code> Java Servlet使用Forms服務客戶端API來處理表單提交和檢索表單資料。 然後，該資料被儲存在企業資料庫中。 (請參閱<a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">處理已提交的Forms</a>)。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>確認表單會轉譯回網頁瀏覽器。 使用者的名字和姓氏等資料會在轉譯前與表單合併。 (請參閱<a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">使用可流式版面預填Forms</a>)。</p></td>
  </tr>
 </tbody>
</table>

**貸款表**

此互動式貸款表格由範例貸款應用程式的`GetLoanForm` Java Servlet轉譯。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**確認表單**

此表單由範例貸款應用程式的`HandleData` Java Servlet轉譯。

![ri_ri_confirm](assets/ri_ri_confirm.png)

`HandleData` Java Servlet會預先填入此表單中使用者的名字和姓氏以及金額。 在預先填入表單後，會將它傳送至用戶端網頁瀏覽器。 (請參閱[使用可流式版面預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlet**

範例貸款應用程式是以Java Servlet形式存在的Forms服務應用程式的範例。 Java Servlet是在J2EE應用程式伺服器（例如WebSphere）上執行的Java程式，包含Forms服務用戶端API程式碼。

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

通常，您不會將Forms服務用戶端API程式碼置於Java Servlet的`doGet`或`doPost`方法中。 最好的程式設計實務是將此程式碼放置在個別的類別中、從`doPost`方法（或`doGet`方法）實例化類別，並呼叫適當的方法。 但是，對於代碼簡寫，本節中的代碼示例將保持在最小值，代碼示例將放在`doPost`方法中。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

**步驟摘要**

若要轉換互動式PDF表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 指定URI值。
1. 將檔案附加至表單（選用）。
1. 轉換互動式PDF表單。
1. 將表單資料流寫入用戶端網頁瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立Forms客戶端API對象。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms網站服務API，請建立`FormsService`物件。

**指定URI值**

您可以指定Forms服務在轉換表單時所需的URI值。 使用內容根URI值`repository:///`可參考儲存為Forms應用程式一部分的表單設計。 例如，請考慮以下名為&#x200B;*Loan.xdp*&#x200B;的表單設計，它位於名為&#x200B;*FormsApplication*&#x200B;的Forms應用程式中：

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

若要存取此表單設計，請指定`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`作為表單名稱（傳遞至`renderPDFForm`方法的第一個參數），並指定`repository:///`作為內容根URI值。

>[!NOTE]
>
>有關使用Workbench建立Forms應用程式的資訊，請參閱[Workbench幫助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位於Forms應用程式中的資源路徑是：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值顯示一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

當您演算互動式表單時，可以定義URI值，例如表單資料張貼的目標URL。 目標URL可透過下列其中一種方式定義：

* 在設計人員中設計表單時的「提交」按鈕
* 使用Forms服務客戶端API

如果目標URL是在表單設計中定義的，請勿使用Forms服務用戶端API覆寫它。 也就是說，使用FormsAPI設定目標URL，會將表單設計中指定的URL重設為使用API指定的URL。 如果您想要將PDF表單提交至表單設計中指定的目標URL，請以程式設計方式將目標URL設為空字串。

如果您的表單包含提交按鈕和計算按鈕（具有在伺服器上執行的對應指令碼），則可以程式設計方式定義表單傳送至何處以執行指令碼的URL。 使用表單設計上的提交按鈕，指定表單資料張貼的URL。 （請參閱[計算表單資料](/help/forms/developing/calculating-form-data.md)）。

>[!NOTE]
>
>您也可以將`com.adobe.idp.Document`例項傳遞至Forms服務，而不是指定URL值以參考XDP檔案。 `com.adobe.idp.Document`實例包含表單設計。 (請參閱[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)。)

**將檔案附加至表單**

您可以將檔案附加至表單。 當您轉換包含檔案附件的PDF表格時，使用者可以使用檔案附件窗格在Acrobat擷取檔案附件。 您可以將不同的檔案類型附加至表單，例如文字檔案，或附加至二進位檔案，例如JPG檔案。

>[!NOTE]
>
>將檔案附件附加到表單是可選的。

**轉換互動式PDF表單**

若要轉換表單，請使用在Designer中建立並儲存為XDP或PDF檔案的表單設計。 此外，您也可以轉換使用Acrobat建立並儲存為PDF檔案的表格。 若要轉換互動式PDF表單，請叫用`FormsServiceClient`物件的`renderPDFForm`方法或`renderPDFForm2`方法。

`renderPDFForm`使用`URLSpec`物件。 使用`URLSpec`物件的`setContentRootURI`方法，將XDP檔案的內容根目錄傳遞至Forms服務。 表單設計名稱(`formQuery`)會作為單獨的參數值傳遞。 這兩個值會串連起來，以取得表單設計的絕對參照。

`renderPDFForm2`方法接受包含要渲染的XDP或PDF文檔的`com.adobe.idp.Document`實例。

>[!NOTE]
>
>如果輸入檔案是PDF檔案，則無法設定標籤的PDF執行時期選項。 如果輸入檔案是XDP檔案，則可以設定標籤的PDF選項。

## 使用Java API {#render-an-interactive-pdf-form-using-the-java-api}轉換互動式PDF表單

使用FormsAPI(Java)來轉換互動式PDF表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。

1. 指定URI值

   * 使用`URLSpec`的建構函式建立儲存URI值的物件。
   * 叫用`URLSpec`物件的`setApplicationWebRoot`方法，並傳遞代表應用程式Web根目錄的字串值。
   * 叫用`URLSpec`物件的`setContentRootURI`方法，並傳遞指定內容根URI值的字串值。 請確定表單設計位於內容根URI中。 如果沒有，Forms服務會提出例外。 要引用儲存庫，請指定`repository:///`。
   * 叫用`URLSpec`物件的`setTargetURL`方法，並傳遞字串值，指定表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單傳送至的URL，以便執行計算。

1. 將檔案附加至表單

   * 使用`java.util.HashMap`物件的建構函式建立檔案附件。
   * 調用每個檔案的`java.util.HashMap`物件的`put`方法，以附加至轉譯的表單。 將下列值傳遞至此方法：

      * 一個字串值，它指定檔案附件的名稱，包括檔案副檔名。
   * 包含檔案附件的`com.adobe.idp.Document`對象。

   >[!NOTE]
   >
   >對要附加到表單的每個檔案重複此步驟。 此步驟為可選步驟，如果您不想發送檔案附件，則可以通過`null`。

1. 轉換互動式PDF表單

   叫用`FormsServiceClient`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參考屬於Forms應用程式的表單設計，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 此為可選參數，如果您不想指定執行時選項，可以指定`null`。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。

   `renderPDFForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調用`FormsResult`對象「s `getOutputContent`」方法建立`com.adobe.idp.Document`對象。
   * 通過調用`getContentType`方法獲取`com.adobe.idp.Document`對象的內容類型。
   * 調用`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 調用`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 建立位元組陣列，並以`InputStream`物件的`read`方法來填入表單資料流，並將位元組陣列傳入為引數。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

## 使用web service API {#render-an-interactive-pdf-form-using-the-web-service-api}轉譯互動式PDF表單

使用FormsAPI(web service)來轉換互動式PDF表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`對象並設定驗證值。

1. 指定URI值

   * 使用`URLSpec`的建構函式建立儲存URI值的物件。
   * 叫用`URLSpec`物件的`setApplicationWebRoot`方法，並傳遞代表應用程式Web根目錄的字串值。
   * 叫用`URLSpec`物件的`setContentRootURI`方法，並傳遞指定內容根URI值的字串值。 請確定表單設計位於內容根URI中。 如果沒有，Forms服務會提出例外。 要引用儲存庫，請指定`repository:///`。
   * 叫用`URLSpec`物件的`setTargetURL`方法，並傳遞字串值，指定表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單傳送至的URL，以便執行計算。

1. 將檔案附加至表單

   * 使用`java.util.HashMap`物件的建構函式建立檔案附件。
   * 調用每個檔案的`java.util.HashMap`物件的`put`方法，以附加至轉譯的表單。 將下列值傳遞至此方法：

      * 指定檔案附件名稱的字串值，包括檔案副檔名
   * 包含檔案附件的`BLOB`對象

   >[!NOTE]
   >
   >對要附加到表單的每個檔案重複此步驟。

1. 轉換互動式PDF表單

   叫用`FormsService`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參考屬於Forms應用程式的表單設計，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞`null`。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 此為可選參數，如果您不想指定執行時選項，可以指定`null`。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`對象。 這可用來儲存轉譯的PDF表單。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`對象。 （此引數將儲存表單中的頁數。）
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`對象。 （此引數將儲存地區值。）
   * 空的`com.adobe.idp.services.holders.FormsResultHolder`對象，將包含此操作的結果。

   `renderPDFForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個參數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 獲取`com.adobe.idp.services.holders.FormsResultHolder`對象`value`資料成員的值，建立`FormResult`對象。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 通過調用`getContentType`方法獲取`BLOB`對象的內容類型。
   * 調用`setContentType`方法並傳遞`BLOB`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 建立位元組陣列，並呼叫`BLOB`物件的`getBinaryData`方法以填入它。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務轉換表單時，它會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 當寫入用戶端網頁瀏覽器時，使用者會看到表單。
