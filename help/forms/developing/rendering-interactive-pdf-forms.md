---
title: 呈現互動式PDF forms
seo-title: Rendering Interactive PDF Forms
description: 使用Forms服務向客戶端設備（通常是Web瀏覽器）提供互動式PDF forms，以從用戶收集資訊。 可以使用Forms服務使用Java API和Web服務API來呈現互動式表單。
seo-description: Use the Forms service to render interactive PDF forms to client devices, typically web browsers, to collect information from users. You can use Forms service to render interactive forms using the Java API and Web Service API.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 0%

---

# 呈現互動式PDF forms {#rendering-interactive-pdf-forms}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

Forms服務向客戶端設備（通常是web瀏覽器）提供互動式PDF forms，以從用戶收集資訊。 在呈現互動式表單後，用戶可以將資料輸入到表單欄位中，然後按一下表單上的提交按鈕，將資訊發回Forms服務。 Adobe Reader或Acrobat必須安裝在托管客戶端web瀏覽器的電腦上，才能看到互動式PDF表單。

>[!NOTE]
>
>在使用Forms服務呈現表單之前，請建立表單設計。 通常，表單設計在設計器中建立，並另存為XDP檔案。 有關建立窗體設計的資訊，請參見 [Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw)。

**貸款申請示例**

介紹了一個貸款申請示例，以說明Forms服務如何使用互動式表格從用戶處收集資訊。 此應用程式允許用戶填寫表單，其中包含確保貸款安全所需的資料，然後將資料提交到Forms服務。 下圖顯示了貸款應用程式的邏輯流。

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

下表介紹了此圖中的步驟。

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
   <td><p>的 <code>GetLoanForm</code> 從HTML頁調用Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>的 <code>GetLoanForm</code> Java Servlet使用Forms服務客戶端API將貸款表單呈現給客戶端Web瀏覽器。 (請參閱 <a href="#render-an-interactive-pdf-form-using-the-java-api">使用Java API呈現互動式PDF表單</a>。)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用戶填寫貸款表單並按一下提交按鈕後，資料將提交到 <code>HandleData</code> Java Servlet。 (請參閱 <i>"貸款表"</i>。)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>的 <code>HandleData</code> Java Servlet使用Forms服務客戶端API處理表單提交和檢索表單資料。 然後將資料儲存在企業資料庫中。 (請參閱 <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">處理已提交的Forms</a>。)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>確認表單被呈現回Web瀏覽器。 在呈現表單之前，會將用戶的名字和姓氏等資料與表單合併。 (請參閱 <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">用可流式佈局預填充Forms</a>。)</p></td>
  </tr>
 </tbody>
</table>

**貸款表**

此互動式貸款表格由貸款申請示例 `GetLoanForm` Java Servlet。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**確認表**

此表單由貸款申請的示例 `HandleData` Java Servlet。

![ri_ri_confirm](assets/ri_ri_confirm.png)

的 `HandleData` Java Servlet用用戶的名字和姓氏以及金額預填充此表單。 在預填充表單後，會將其發送到客戶端Web瀏覽器。 (請參閱 [用可流式佈局預填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlet**

示例貸款應用程式是作為Java Servlet存在的Forms服務應用程式的示例。 Java Servlet是在J2EE應用伺服器（如WebSphere）上運行的Java程式，包含Forms服務客戶端API代碼。

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

通常，您不會將Forms服務客戶端API代碼放在Java Servlet中 `doGet` 或 `doPost` 的雙曲餘切值。 將此代碼放在單獨的類中，從中實例化該類是更好的寫程式實踐 `doPost` 方法 `doGet` 方法)，並調用相應的方法。 但是，對於代碼簡化，本節中的代碼示例將保持為最小值，代碼示例將放在 `doPost` 的雙曲餘切值。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

**步驟摘要**

要呈現互動式PDF表單，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms客戶端API對象。
1. 指定URI值。
1. 將檔案附加到表單（可選）。
1. 呈現互動式PDF窗體。
1. 將表單資料流寫入客戶端Web瀏覽器。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms客戶端API對象**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立一個Forms客戶端API對象。 如果使用Java API，請建立 `FormsServiceClient` 的雙曲餘切值。 如果使用FormsWeb服務API，請建立 `FormsService` 的雙曲餘切值。

**指定URI值**

可以指定Forms服務呈現表單所需的URI值。 通過使用內容根URI值，可以引用保存為Forms應用程式一部分的窗體設計 `repository:///`。 例如，請考慮以下名為 *Loan.xdp* 位於名為「A.D.A.」的Forms應用程式 *窗體應用程式*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

要訪問此窗體設計，請指定 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` 表單名稱(傳遞給 `renderPDFForm` 方法)和 `repository:///` 作為內容根URI值。

>[!NOTE]
>
>有關使用Workbench建立Forms應用程式的資訊，請參閱 [工作台幫助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位於Forms應用程式中的資源的路徑是：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值顯示URI值的一些示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

在呈現互動式表單時，可以定義URI值，如將表單資料發佈到的目標URL。 目標URL可以通過以下方式之一定義：

* 在設計器中設計表單設計時在「提交」按鈕上
* 使用Forms服務客戶端API

如果目標URL是在表單設計中定義的，則不要用Forms服務客戶端API覆蓋它。 即，使用FormsAPI設定目標URL將表單設計中指定的URL重置為使用API指定的URL。 如果希望將PDF表單提交到在表單設計中指定的目標URL，則以寫程式方式將目標URL設定為空字串。

如果您的表單包含提交按鈕和計算按鈕（帶有在伺服器上運行的相應指令碼），則可以寫程式方式定義表單的發送位置以執行指令碼。 使用表單設計上的提交按鈕可指定將表單資料過帳到的URL。 (請參閱 [計算表單資料](/help/forms/developing/calculating-form-data.md)。)

>[!NOTE]
>
>您也可以傳遞XDP檔案，而不是指定URL值來引用XDP檔案 `com.adobe.idp.Document` 向Forms局舉報。 的 `com.adobe.idp.Document` 實例包含窗體設計。 (請參閱 [將檔案轉給Forms](/help/forms/developing/passing-documents-forms-service.md)。)

**將檔案附加到窗體**

可以將檔案附加到窗體。 當您呈現帶有檔案附件的PDF表單時，用戶可以使用檔案附件窗格在Acrobat檢索檔案附件。 可以將不同的檔案類型附加到表單（如文本檔案）或二進位檔案(如JPG檔案)。

>[!NOTE]
>
>將檔案附件附加到表單是可選的。

**呈現互動式PDF窗體**

要呈現表單，請使用在設計器中建立並另存為XDP或PDF檔案的表單設計。 此外，還可以渲染使用Acrobat建立並另存為PDF檔案的表單。 要呈現互動式PDF窗體，請調用 `FormsServiceClient` 對象 `renderPDFForm` 方法 `renderPDFForm2` 的雙曲餘切值。

的 `renderPDFForm` 使用 `URLSpec` 的雙曲餘切值。 XDP檔案的內容根目錄將通過 `URLSpec` 對象 `setContentRootURI` 的雙曲餘切值。 窗體設計名稱( `formQuery`)作為單獨的參數值傳遞。 將這兩個值連接起來，以獲得對表單設計的絕對參照。

的 `renderPDFForm2` 方法接受 `com.adobe.idp.Document` 包含要呈現的XDP或PDF文檔的實例。

>[!NOTE]
>
>如果輸入文檔是PDF文檔，則無法設定標籤的PDF運行時選項。 如果輸入檔案是XDP檔案，則可以設定標籤PDF選項。

## 使用Java API呈現互動式PDF表單 {#render-an-interactive-pdf-form-using-the-java-api}

使用FormsAPI(Java)呈現互動式PDF表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立Forms客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 指定URI值

   * 建立 `URLSpec` 使用其建構子儲存URI值的對象。
   * 調用 `URLSpec` 對象 `setApplicationWebRoot` 方法，並傳遞一個表示應用程式web根的字串值。
   * 調用 `URLSpec` 對象 `setContentRootURI` 方法並傳遞一個字串值，該字串值指定內容根URI值。 確保表單設計位於內容根URI中。 否則，Forms服務會引發異常。 要引用儲存庫，請指定 `repository:///`。
   * 調用 `URLSpec` 對象 `setTargetURL` 方法並傳遞一個字串值，該字串值指定將表單資料發佈到的目標URL值。 如果在表單設計中定義目標URL，則可以傳遞空字串。 您還可以指定表單發送到的URL以執行計算。

1. 將檔案附加到窗體

   * 建立 `java.util.HashMap` 使用其建構子儲存檔案附件的對象。
   * 調用 `java.util.HashMap` 對象 `put` 用於每個檔案附加到呈現的窗體的方法。 將以下值傳遞給此方法：

      * 一個字串值，它指定檔案附件的名稱，包括檔案副檔名。
   * A `com.adobe.idp.Document` 包含檔案附件的對象。

   >[!NOTE]
   >
   >對要附加到表單的每個檔案重複此步驟。 此步驟是可選的，您可以通過 `null` 的子菜單。

1. 呈現互動式PDF窗體

   調用 `FormsServiceClient` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `com.adobe.idp.Document` 的雙曲餘切值。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 這是可選參數，您可以指定 `null` 選項。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

   的 `renderPDFForm` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `com.adobe.idp.Document` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read` 方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

## 使用Web服務API呈現互動式PDF表單 {#render-an-interactive-pdf-form-using-the-web-service-api}

使用FormsAPI（Web服務）呈現互動式PDF表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包括到類路徑中。

1. 建立Forms客戶端API對象

   建立 `FormsService` 對象和設定驗證值。

1. 指定URI值

   * 建立 `URLSpec` 使用其建構子儲存URI值的對象。
   * 調用 `URLSpec` 對象 `setApplicationWebRoot` 方法，並傳遞一個表示應用程式web根的字串值。
   * 調用 `URLSpec` 對象 `setContentRootURI` 方法並傳遞一個字串值，該字串值指定內容根URI值。 確保表單設計位於內容根URI中。 否則，Forms服務會引發異常。 要引用儲存庫，請指定 `repository:///`。
   * 調用 `URLSpec` 對象 `setTargetURL` 方法並傳遞一個字串值，該字串值指定將表單資料發佈到的目標URL值。 如果在表單設計中定義目標URL，則可以傳遞空字串。 您還可以指定表單發送到的URL以執行計算。

1. 將檔案附加到窗體

   * 建立 `java.util.HashMap` 使用其建構子儲存檔案附件的對象。
   * 調用 `java.util.HashMap` 對象 `put` 用於每個檔案附加到呈現的窗體的方法。 將以下值傳遞給此方法：

      * 一個字串值，它指定檔案附件的名稱，包括檔案副檔名
   * A `BLOB` 包含檔案附件的對象

   >[!NOTE]
   >
   >對要附加到表單的每個檔案重複此步驟。

1. 呈現互動式PDF窗體

   調用 `FormsService` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `BLOB` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞 `null`。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 這是可選參數，您可以指定 `null` 選項。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的對象。 這用於儲存渲染的PDF窗體。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的對象。 （此參數將儲存表單中的頁數。）
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。 （此參數將儲存區域設定值。）
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   的 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個參數值傳遞的對象，其表單資料流必須寫入客戶端web瀏覽器。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `FormResult` 通過獲取 `com.adobe.idp.services.holders.FormsResultHolder` 對象 `value` 資料成員。
   * 建立 `BLOB` 通過調用包含表單資料的對象 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `BLOB` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `BLOB` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立位元組陣列，並通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。 此任務分配 `FormsResult` 對象。
   * 調用 `javax.servlet.http.HttpServletResponse` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**將表單資料流寫入客戶端Web瀏覽器**

當Forms服務呈現表單時，它將返回必須寫入客戶端Web瀏覽器的表單資料流。 當寫入客戶端Web瀏覽器時，該表單對用戶可見。
