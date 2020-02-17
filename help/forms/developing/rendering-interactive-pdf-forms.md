---
title: 轉換互動式PDF表單
seo-title: 轉換互動式PDF表單
description: 'null'
seo-description: 'null'
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 轉換互動式PDF表單 {#rendering-interactive-pdf-forms}

Forms服務會將互動式PDF表格轉譯至用戶端裝置（通常是網頁瀏覽器），以收集使用者的資訊。 在轉譯互動式表單後，使用者可以在表單欄位中輸入資料，然後按一下表單上的提交按鈕，將資訊傳回至Forms服務。 Adobe Reader或Acrobat必須安裝在用戶端網頁瀏覽器的電腦上，才能顯示互動式PDF表格。

>[!NOTE]
>
>在使用Forms服務演算表單之前，請先建立表單設計。 通常，表單設計是在Designer中建立，並儲存為XDP檔案。 有關建立表單設計的資訊，請參 [閱表單設計器](https://www.adobe.com/go/learn_aemforms_designer_63)。

**貸款申請範例**

引入範例貸款應用程式，以示範Forms服務如何使用互動式表單來收集使用者的資訊。 此應用程式可讓使用者填寫表單，填入保證貸款安全所需的資料，然後將資料提交至表單服務。 下圖顯示貸款申請的邏輯流程。

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
   <td><p>Java <code>GetLoanForm</code> Servlet是從HTML頁面呼叫。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Java <code>GetLoanForm</code> Servlet使用Forms服務客戶端API將貸款表格轉換到客戶端Web瀏覽器。 (請參 <a href="#render-an-interactive-pdf-form-using-the-java-api">閱使用Java API演算互動式PDF表單</a>。)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>當使用者填入貸款表單並按一下提交按鈕後，資料就會送出至 <code>HandleData</code> Java Servlet。 (請參 <i>閱「貸款表」</i>。)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Java <code>HandleData</code> Servlet使用Forms服務客戶端API來處理表單提交和檢索表單資料。 然後，該資料被儲存在企業資料庫中。 (請參 <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">閱處理提交的表單</a>。)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>確認表單會轉譯回網頁瀏覽器。 使用者的名字和姓氏等資料會在轉譯前與表單合併。 (請參 <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">閱使用可排程版面預填表單</a>。)</p></td>
  </tr>
 </tbody>
</table>

**貸款表**

此互動式貸款表格由範例貸款應用程式的 `GetLoanForm` Java Servlet轉譯。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**確認表單**

此表單由範例貸款應用程式的 `HandleData` Java Servlet轉譯。

![ri_ri_confirm](assets/ri_ri_confirm.png)

Java `HandleData` Servlet會預先填入此表單，並填入使用者的名字和姓氏以及金額。 在預先填入表單後，會將它傳送至用戶端網頁瀏覽器。 (請參 [閱使用可排程版面預填表單](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlet**

範例貸款應用程式是Forms服務應用程式的範例，存在於Java Servlet中。 Java Servlet是在J2EE應用程式伺服器（例如WebSphere）上執行的Java程式，包含Forms服務用戶端API程式碼。

以下代碼顯示名為GetLoanForm的Java Servlet的語法：

```as3
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

通常，您不會將Forms服務用戶端API程式碼置於Java Servlet或方 `doGet` 法 `doPost` 中。 將此程式碼放在個別類別中、從方法（或方法）實例化該類別，並呼叫 `doPost` 適當的方 `doGet` 法，是更好的程式設計實務。 不過，若是程式碼簡寫，本節中的程式碼範例會維持在最小值，而程式碼範例則會置於方法 `doPost` 中。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

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

您必須先建立Forms Client API物件，才能以程式設計方式執行Forms服務用戶端API作業。 如果您使用Java API，請建立物 `FormsServiceClient` 件。 如果您使用Forms web service API，請建立物 `FormsService` 件。

**指定URI值**

您可以指定Forms服務呈現表單所需的URI值。 使用內容根URI值可以參考儲存為Forms應用程式一部分的表單設計 `repository:///`。 例如，請考慮以下名為 *Loan.xdp的表單設計* ，位於名為 *FormsApplication的Forms應用程式*&#x200B;中：

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

若要存取此表單設計，請 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` 指定為表單名稱(傳遞至方法的第一個 `renderPDFForm` 參數) `repository:///` 和內容根URI值。

>[!NOTE]
>
>有關使用工作台建立表單應用程式的資訊，請參 [閱工作台幫助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位於Forms應用程式中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值顯示一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

當您演算互動式表單時，可以定義URI值，例如表單資料張貼的目標URL。 目標URL可透過下列其中一種方式定義：

* 在設計人員中設計表單時的「提交」按鈕
* 使用Forms服務客戶端API

如果目標URL是在表單設計中定義的，請勿使用Forms服務用戶端API覆寫它。 也就是說，使用Forms API設定目標URL會將表單設計中指定的URL重設為使用API指定的URL。 如果您想要將PDF表單提交至表單設計中指定的目標URL，請以程式設計方式將目標URL設為空字串。

如果您的表單包含提交按鈕和計算按鈕（具有在伺服器上執行的對應指令碼），則可以程式設計方式定義表單傳送至何處以執行指令碼的URL。 使用表單設計上的提交按鈕，指定表單資料張貼的URL。 (請參閱 [計算表單資料](/help/forms/developing/calculating-form-data.md)。)

>[!NOTE]
>
>您也可以將例項傳遞至Forms服務，而不是指定URL值以 `com.adobe.idp.Document` 參考XDP檔案。 實 `com.adobe.idp.Document` 例包含表單設計。 (請參 [閱將檔案傳送至Forms服務](/help/forms/developing/passing-documents-forms-service.md))。

**將檔案附加至表單**

您可以將檔案附加至表單。 當您轉譯包含檔案附件的PDF表格時，使用者可以使用檔案附件窗格在Acrobat中擷取檔案附件。 您可以將不同的檔案類型附加至表單，例如文字檔案，或附加至二進位檔案，例如JPG檔案。

>[!NOTE]
>
>將檔案附件附加到表單是可選的。

**轉換互動式PDF表單**

若要轉換表單，請使用在Designer中建立並儲存為XDP或PDF檔案的表單設計。 此外，您也可以轉換使用Acrobat建立並儲存為PDF檔案的表格。 若要轉換互動式PDF表單，請叫 `FormsServiceClient` 用物件的方 `renderPDFForm` 法或 `renderPDFForm2` 方法。

使 `renderPDFForm` 用對 `URLSpec` 像。 XDP檔案的內容根目錄會使用物件的方法傳遞 `URLSpec` 至Forms服 `setContentRootURI` 務。 表單設計名稱( `formQuery`)會作為單獨的參數值傳遞。 這兩個值會串連起來，以取得表單設計的絕對參照。

該方 `renderPDFForm2` 法接受包 `com.adobe.idp.Document` 含要渲染的XDP或PDF文檔的實例。

>[!NOTE]
>
>如果輸入檔案是PDF檔案，則無法設定標籤的PDF執行時期選項。 如果輸入檔案是XDP檔案，則可以設定標籤的PDF選項。

## 使用Java API演算互動式PDF表單 {#render-an-interactive-pdf-form-using-the-java-api}

使用Forms API(Java)演算互動式PDF表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 指定URI值

   * 使用 `URLSpec` 其建構子建立儲存URI值的對象。
   * 叫用物 `URLSpec` 件的方 `setApplicationWebRoot` 法，並傳遞代表應用程式Web根目錄的字串值。
   * 叫用物 `URLSpec` 件的方 `setContentRootURI` 法並傳遞指定內容根URI值的字串值。 請確定表單設計位於內容根URI中。 否則，Forms服務會引發例外。 要引用儲存庫，請指定 `repository:///`。
   * 叫用物 `URLSpec` 件的方 `setTargetURL` 法，並傳遞字串值，指定表單資料張貼的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單傳送至的URL，以便執行計算。

1. 將檔案附加至表單

   * 使用建 `java.util.HashMap` 構函式建立物件以儲存檔案附件。
   * 調用每 `java.util.HashMap` 個檔案的 `put` 物件方法，以附加至轉譯的表單。 將下列值傳遞至此方法：

      * 一個字串值，它指定檔案附件的名稱，包括檔案副檔名。
   * 包 `com.adobe.idp.Document` 含檔案附件的對象。
   >[!NOTE]
   >
   >對要附加到表單的每個檔案重複此步驟。 此步驟為可選步驟，如果您 `null` 不想發送檔案附件，則可以通過。

1. 轉換互動式PDF表單

   叫用物 `FormsServiceClient` 件的方 `renderPDFForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包 `com.adobe.idp.Document` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞空 `com.adobe.idp.Document` 物件。
   * 存 `PDFFormRenderSpec` 儲運行時選項的對象。 此為可選參數，您可以指 `null` 定是否不想指定執行時選項。
   * 包 `URLSpec` 含Forms服務所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
   該方 `renderPDFForm` 法返回包 `FormsResult` 含必須寫入客戶端Web瀏覽器的表單資料流的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調 `com.adobe.idp.Document` 用對象的方法 `FormsResult` 建立對 `getOutputContent` 像。
   * 通過調用對象的方 `com.adobe.idp.Document` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `com.adobe.idp.Document` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 調用 `java.io.InputStream` 物件的方 `com.adobe.idp.Document` 法以建立物 `getInputStream` 件。
   * 建立位元組陣列，並借由調用物件的方法並將 `InputStream` 位元組陣列 `read` 傳入為引數，以表單資料流填入。
   * 叫用物 `javax.servlet.ServletOutputStream` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

## 使用web service API轉譯互動式PDF表單 {#render-an-interactive-pdf-form-using-the-web-service-api}

使用Forms API(web service)來轉換互動式PDF表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立對 `FormsService` 像並設定驗證值。

1. 指定URI值

   * 使用 `URLSpec` 其建構子建立儲存URI值的對象。
   * 叫用物 `URLSpec` 件的方 `setApplicationWebRoot` 法，並傳遞代表應用程式Web根目錄的字串值。
   * 叫用物 `URLSpec` 件的方 `setContentRootURI` 法並傳遞指定內容根URI值的字串值。 請確定表單設計位於內容根URI中。 否則，Forms服務會引發例外。 要引用儲存庫，請指定 `repository:///`。
   * 叫用物 `URLSpec` 件的方 `setTargetURL` 法，並傳遞字串值，指定表單資料張貼的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單傳送至的URL，以便執行計算。

1. 將檔案附加至表單

   * 使用建 `java.util.HashMap` 構函式建立物件以儲存檔案附件。
   * 調用每 `java.util.HashMap` 個檔案的 `put` 物件方法，以附加至轉譯的表單。 將下列值傳遞至此方法：

      * 指定檔案附件名稱的字串值，包括檔案副檔名
   * 包 `BLOB` 含檔案附件的對象
   >[!NOTE]
   >
   >對要附加到表單的每個檔案重複此步驟。

1. 轉換互動式PDF表單

   叫用物 `FormsService` 件的方 `renderPDFForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包 `BLOB` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞 `null`。
   * 存 `PDFFormRenderSpec` 儲運行時選項的對象。 此為可選參數，您可以指 `null` 定是否不想指定執行時選項。
   * 包 `URLSpec` 含Forms服務所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空對象。 這可用來儲存轉譯的PDF表單。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空對象。 （此引數將儲存表單中的頁數。）
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空對象。 （此引數將儲存地區值。）
   * 包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作結果的空對象。
   該方 `renderPDFForm` 法用必 `com.adobe.idp.services.holders.FormsResultHolder` 須寫入客戶端Web瀏覽器的表單資料流填充作為最後一個參數值傳遞的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 獲取 `FormResult` 對象資料成員的 `com.adobe.idp.services.holders.FormsResultHolder` 值以建立 `value` 對象。
   * 呼叫 `BLOB` 物件的方法，以建立包含表 `FormsResult` 單資料的物 `getOutputContent` 件。
   * 通過調用對象的方 `BLOB` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `BLOB` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 建立位元組陣列，並透過叫用物件的方 `BLOB` 法來填入該 `getBinaryData` 陣列。 此任務將對象的內 `FormsResult` 容分配給位元組陣列。
   * 叫用物 `javax.servlet.http.HttpServletResponse` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務轉譯表單時，它會傳回必須寫入用戶端網頁瀏覽器的表單資料流。 當寫入用戶端網頁瀏覽器時，使用者會看到表單。
