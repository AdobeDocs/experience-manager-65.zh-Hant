---
title: 計算表單資料
seo-title: 計算表單資料
description: 'null'
seo-description: 'null'
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
translation-type: tm+mt
source-git-commit: 4b9e2ceafc301db9337868b78bcae87c0f07e14b

---


# 計算表單資料 {#calculating-form-data}

Forms服務可計算使用者在表單中輸入的值，並顯示結果。 若要計算表單資料，您必須執行兩項工作。 首先，您建立可計算表單資料的表單設計指令碼。 表單設計支援三種類型的指令碼。 一種指令碼類型在客戶端上運行，另一種指令碼類型在伺服器上運行，第三種指令碼類型在伺服器和客戶端上運行。 本主題中討論的指令碼類型在伺服器上運行。 HTML、PDF和表單指南（已過時）轉換支援伺服器端計算。

在表單設計流程中，您可以運用計算和指令碼來提供更豐富的使用者體驗。 計算和指令碼可新增至大部分的表格欄位和物件。 您必須建立表單設計指令碼，以對使用者輸入互動式表單的資料執行計算作業。

用戶在表單中輸入值，然後按一下「計算」按鈕查看結果。 下列程式說明可讓使用者計算資料的範例應用程式：

* 使用者存取名為StartLoan.html的HTML頁面，該頁面可當成網頁應用程式的開始頁面。 此頁調用名為的Java Servlet `GetLoanForm`。
* Servlet `GetLoanForm` 會轉換貸款表單。 此表單包含指令碼、互動式欄位、計算按鈕和送出按鈕。
* 使用者在表單欄位中輸入值，然後按一下「計算」按鈕。 表單會傳送至執行指令 `CalculateData` 碼的Java Servlet。 表單會傳回給使用者，其計算結果會顯示在表單中。
* 用戶繼續輸入和計算值，直到顯示滿意的結果。 當使用者滿意時，會按一下「提交」按鈕以處理表單。 表單會傳送至另一個名為Java Servlet的表 `ProcessForm` 單，負責擷取已提交的資料。 (請參 [閱處理提交的表單](/help/forms/developing/rendering-forms.md#handling-submitted-forms)。)


下圖顯示應用程式的邏輯流程。

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

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
   <td><p>從 <code>GetLoanForm</code> HTML開始頁調用Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Java <code>GetLoanForm</code> Servlet使用Forms服務客戶端API將貸款表格轉換到客戶端Web瀏覽器。 呈現包含配置為在伺服器上運行的指令碼的表單和呈現不包含指令碼的表單之間的區別在於，您必須指定用於執行指令碼的目標位置。 如果未指定目標位置，則不會執行配置為在伺服器上運行的指令碼。 例如，請考慮本節中介紹的應用程式。 Java <code>CalculateData</code> Servlet是執行指令碼的目標位置。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者將資料輸入互動欄位，然後按一下「計算」按鈕。 表單會傳送至 <code>CalculateData</code> Java Servlet，並在其中執行指令碼。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>表單會轉譯回網頁瀏覽器，其計算結果會顯示在表單中。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>當值滿意時，使用者會按一下「提交」按鈕。 表單會傳送至另一個名為的Java Servlet <code>ProcessForm</code>。</p></td>
  </tr>
 </tbody>
</table>

通常，提交為PDF內容的表單包含在用戶端上執行的指令碼。 不過，伺服器端的計算也可以執行。 「提交」按鈕不能用於計算指令碼。 在這種情況下，不會執行計算，因為Forms服務認為交互已完成。

為了說明表單設計指令碼的使用，本節將檢查一個簡單的互動式表單，其中包含已設定為可在伺服器上執行的指令碼。 下圖顯示的表單設計包含一個指令碼，該指令碼將用戶輸入到前兩個欄位中的值添加到第三個欄位中，並在第三個欄位中顯示結果。

![cf_cf_caldata](assets/cf_cf_caldata.png)

******答：名為NumericField1** B的欄位。名為NumericField2 **C.** a的欄位名為NumericField3

位於此表單設計中的指令碼語法如下：

```as3
     NumericField3 = NumericField2 + NumericField1
```

在此表單設計中，「計算」按鈕是命令按鈕，而指令檔位於此按鈕的事 `Click` 件中。 當使用者在前兩個欄位（NumericField1和NumericField2）中輸入值，然後按一下「計算」按鈕時，表格會傳送至Forms服務，並執行指令碼。 Forms服務會將表單轉譯回用戶端裝置，計算結果會顯示在NumericField3欄位中。

>[!NOTE]
>
>如需建立表單設計指令碼的詳細資訊，請參閱 [表單設計器](https://www.adobe.com/go/learn_aemforms_designer_63)。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要計算表單資料，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 檢索包含計算指令碼的表單。
1. 將表單資料流寫回用戶端網頁瀏覽器

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API操作。 如果您使用Java API，請建立物 `FormsServiceClient` 件。 如果您使用Forms web service API，請建立物 `FormsServiceService` 件。

**檢索包含計算指令碼的表單**

您可使用Forms服務用戶端API來建立應用程式邏輯，以處理包含設定為在伺服器上執行之指令碼的表單。 此程式類似於處理提交的表單。 (請參 [閱處理提交的表單](/help/forms/developing/rendering-forms-rendering-forms handling-submitted-forms-handling-submitted.md#handling-submitted-forms)。

驗證與提交表單關聯的處理狀態是否為 `1``(Calculate)`，這表示Forms服務正在對表單資料執行計算操作，且結果必須寫回給用戶。 在這種情況下，將自動執行配置為在伺服器上運行的指令碼。

**將表單資料流寫回用戶端網頁瀏覽器**

在驗證與已提交表單關聯的處理狀態為 `1`後，您必須將結果寫回用戶端網頁瀏覽器。 當顯示表單時，計算值會出現在適當的欄位中。

**另請參閱**

[使用Web服務API](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)[](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)Setting使用Web服務API計算表單資料使用Web服務API API計算表單資料[Java連接屬性](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)[](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)[](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)[](/help/forms/developing/rendering-interactive-pdf-forms.md)[Forms Service Forms Quick StartsInteractive Pdf Forms Renderinged Web Applications，使用Web服務APIAPIAPIAPI SpipiaSSiSS PriProSSS Pr PreS PromSSSSSSSSSSSSProSSSSSSSS PriSSiSSSiSSSSProSiSSinSSinSSSSSS Pr](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API計算表單資料 {#calculate-form-data-using-the-java-api}

使用Forms API(Java)計算表單資料：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 檢索包含計算指令碼的表單

   * 若要擷取包含計算指令碼的表單資料，請使 `com.adobe.idp.Document` 用其建構函式建立物件，並從建構函式 `javax.servlet.http.HttpServletResponse` 內叫用 `getInputStream` 物件的方法。
   * 叫用物 `FormsServiceClient` 件的方 `processFormSubmission` 法並傳遞下列值：

      * 包 `com.adobe.idp.Document` 含表單資料的物件。
      * 一個字串值，它指定包括所有相關HTTP標題的環境變數。 必須通過為環境變數指定一個或多個值來指定要處理的內 `CONTENT_TYPE` 容類型。 例如，若要處理XML和PDF資料，請為此參數指定下列字串值： `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * 指定標題值的 `HTTP_USER_AGENT` 字串值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存 `RenderOptionsSpec` 儲運行時選項的對象。
      該方 `processFormSubmission` 法返回包 `FormsResult` 含表單提交結果的對象。

   * 請叫用物件的方法，以確認與已提交表 `1` 單相關聯的處 `FormsResult` 理狀態 `getAction` 為。 如果此方法返回值 `1`，則會執行計算，並將資料寫回客戶端Web瀏覽器。


1. 將表單資料流寫回用戶端網頁瀏覽器

   * 建立用 `javax.servlet.ServletOutputStream` 於傳送表單資料串流至用戶端網頁瀏覽器的物件。
   * 通過調 `com.adobe.idp.Document` 用對象的方法 `FormsResult` 建立對 `getOutputContent` 像。
   * 調用 `java.io.InputStream` 物件的方 `com.adobe.idp.Document` 法以建立物 `getInputStream` 件。
   * 建立位元組陣列，並借由調用物件的方法並將 `InputStream` 位元組陣列 `read` 傳入為引數，以表單資料流填入。
   * 叫用物 `javax.servlet.ServletOutputStream` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**


[包含AEM Forms java程式庫檔案設](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)[定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API計算表單資料 {#calculate-form-data-using-the-web-service-api}

使用Forms API(web service)計算表單資料：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立對 `FormsService` 像並設定驗證值。

1. 檢索包含計算指令碼的表單

   * 要檢索張貼到Java servlet的表單資料，請使用其 `BLOB` 建構子建立對象。
   * 使用 `java.io.InputStream` 物件的方法 `javax.servlet.http.HttpServletResponse` 建立物 `getInputStream` 件。
   * 使用 `java.io.ByteArrayOutputStream` 其建構函式並傳遞物件長度，以建立物 `java.io.InputStream` 件。
   * 將對象的內 `java.io.InputStream` 容複製到對 `java.io.ByteArrayOutputStream` 像。
   * 叫用物件的方法，以 `java.io.ByteArrayOutputStream` 建立位元組 `toByteArray` 陣列。
   * 調用對 `BLOB` 像的方法並將字 `setBinaryData` 節陣列作為引數傳遞，以填充對象。
   * 使用其 `RenderOptionsSpec` 建構函式建立物件。 調用物件的方法並傳 `RenderOptionsSpec` 遞指定地區 `setLocale` 值的字串值，以設定地區值。
   * 叫用物 `FormsServiceClient` 件的方 `processFormSubmission` 法並傳遞下列值：

      * 包 `BLOB` 含表單資料的物件。
      * 指定環境變數的字串值包括所有相關的HTTP標頭。 例如，您可以指定下列字串值： `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * 指定標題值的 `HTTP_USER_AGENT` 字串值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存 `RenderOptionsSpec` 儲運行時選項的對象。 如需詳細資訊，請造訪。
      * 由方 `BLOBHolder` 法填充的空對象。
      * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空對象。
      * 由方 `BLOBHolder` 法填充的空對象。
      * 由方 `BLOBHolder` 法填充的空對象。
      * 由方 `javax.xml.rpc.holders.ShortHolder` 法填充的空對象。
      * 由方 `MyArrayOf_xsd_anyTypeHolder` 法填充的空對象。 此參數用於儲存隨表單一起提交的檔案附件。
      * 由方 `FormsResultHolder` 法填入的空對象，其表單為已提交。
      方 `processFormSubmission` 法會以表 `FormsResultHolder` 單提交的結果填入參數。 該方 `processFormSubmission` 法返回包 `FormsResult` 含表單提交結果的對象。

   * 請叫用物件的方法，以確認與已提交表 `1` 單相關聯的處 `FormsResult` 理狀態 `getAction` 為。 如果此方法返回值 `1`，則會執行計算，並將資料寫回客戶端Web瀏覽器。


1. 將表單資料流寫回用戶端網頁瀏覽器

   * 建立用 `javax.servlet.ServletOutputStream` 於傳送表單資料串流至用戶端網頁瀏覽器的物件。
   * 呼叫 `BLOB` 物件的方法，以建立包含表 `FormsResult` 單資料的物 `getOutputContent` 件。
   * 建立位元組陣列，並透過叫用物件的方 `BLOB` 法來填入該 `getBinaryData` 陣列。 此任務將對象的內 `FormsResult` 容分配給位元組陣列。
   * 叫用物 `javax.servlet.http.HttpServletResponse` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
