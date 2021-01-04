---
title: 計算表單資料
seo-title: 計算表單資料
description: 使用Forms服務計算用戶在表單中輸入的值並顯示結果。 Forms服務使用Java API和Web服務API計算值。
seo-description: 使用Forms服務計算用戶在表單中輸入的值並顯示結果。 Forms服務使用Java API和Web服務API計算值。
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1902'
ht-degree: 0%

---


# 計算表單資料{#calculating-form-data}

Forms服務可計算使用者在表單中輸入的值，並顯示結果。 若要計算表單資料，您必須執行兩項工作。 首先，您建立可計算表單資料的表單設計指令碼。 表單設計支援三種類型的指令碼。 一種指令碼類型在客戶端上運行，另一種指令碼類型在伺服器上運行，第三種指令碼類型在伺服器和客戶端上運行。 本主題中討論的指令碼類型在伺服器上運行。 HTML、PDF和表單指南（已過時）轉換支援伺服器端計算。

在表單設計流程中，您可以運用計算和指令碼來提供更豐富的使用者體驗。 計算和指令碼可新增至大部分的表格欄位和物件。 您必須建立表單設計指令碼，以對使用者輸入互動式表單的資料執行計算作業。

用戶在表單中輸入值，然後按一下「計算」按鈕查看結果。 下列程式說明可讓使用者計算資料的範例應用程式：

* 使用者存取名為StartLoan.html的HTML頁面，該頁面可當成網頁應用程式的開始頁面。 此頁調用名為`GetLoanForm`的Java Servlet。
* `GetLoanForm` servlet將呈現貸款表單。 此表單包含指令碼、互動式欄位、計算按鈕和送出按鈕。
* 使用者在表單欄位中輸入值，然後按一下「計算」按鈕。 表單會傳送至執行指令碼的`CalculateData` Java Servlet。 表單會傳回給使用者，其計算結果會顯示在表單中。
* 用戶繼續輸入和計算值，直到顯示滿意的結果。 當使用者滿意時，會按一下「提交」按鈕以處理表單。 表單會傳送至另一個名為`ProcessForm`的Java Servlet，負責擷取已提交的資料。 （請參閱[處理提交的表單](/help/forms/developing/rendering-forms.md#handling-submitted-forms)）。


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
   <td><p><code>GetLoanForm</code> Java Servlet是從HTML開始頁調用的。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Java Servlet使用Forms服務客戶端API將貸款表格呈現給客戶端Web瀏覽器。 呈現包含配置為在伺服器上運行的指令碼的表單和呈現不包含指令碼的表單之間的區別在於，您必須指定用於執行指令碼的目標位置。 如果未指定目標位置，則不會執行配置為在伺服器上運行的指令碼。 例如，請考慮本節中介紹的應用程式。 <code>CalculateData</code> Java Servlet是執行指令碼的目標位置。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者將資料輸入互動欄位，然後按一下「計算」按鈕。 表單會傳送至執行指令碼的<code>CalculateData</code> Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>表單會轉譯回網頁瀏覽器，其計算結果會顯示在表單中。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>當值滿意時，使用者會按一下「提交」按鈕。 表單會傳送至另一個名為<code>ProcessForm</code>的Java Servlet。</p></td>
  </tr>
 </tbody>
</table>

通常，提交為PDF內容的表單包含在用戶端上執行的指令碼。 不過，伺服器端的計算也可以執行。 「提交」按鈕不能用於計算指令碼。 在這種情況下，不會執行計算，因為Forms服務認為交互已完成。

為了說明表單設計指令碼的使用，本節將檢查一個簡單的互動式表單，其中包含已設定為可在伺服器上執行的指令碼。 下圖顯示的表單設計包含一個指令碼，該指令碼將用戶輸入到前兩個欄位中的值添加到第三個欄位中，並在第三個欄位中顯示結果。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** A欄位，名為NumericField1  **B.** A欄位，名為NumericField2  **C.** A欄位，名為NumericField3

位於此表單設計中的指令碼語法如下：

```javascript
     NumericField3 = NumericField2 + NumericField1
```

在此表單設計中，「計算」按鈕是命令按鈕，而指令檔位於此按鈕的`Click`事件中。 當使用者在前兩個欄位（NumericField1和NumericField2）中輸入值，然後按一下「計算」按鈕時，表格會傳送至Forms服務，並執行指令碼。 Forms服務會將表單轉譯回用戶端裝置，計算結果會顯示在NumericField3欄位中。

>[!NOTE]
>
>有關建立表單設計指令碼的資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟{#summary-of-steps}摘要

要計算表單資料，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 檢索包含計算指令碼的表單。
1. 將表單資料流寫回用戶端網頁瀏覽器

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API操作。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms web service API，請建立`FormsServiceService`物件。

**檢索包含計算指令碼的表單**

您可使用Forms服務用戶端API來建立應用程式邏輯，以處理包含設定為在伺服器上執行之指令碼的表單。 此程式類似於處理提交的表單。 （請參閱[處理提交的表單](/help/forms/developing/handling-submitted-forms.md)）。

驗證與提交表單關聯的處理狀態為`1` `(Calculate)`，這表示Forms服務正在對表單資料執行計算操作，且結果必須寫回給用戶。 在這種情況下，將自動執行配置為在伺服器上運行的指令碼。

**將表單資料流寫回用戶端網頁瀏覽器**

在驗證與提交的表單相關聯的處理狀態為`1`後，您必須將結果寫回客戶端Web瀏覽器。 當顯示表單時，計算值會出現在適當的欄位中。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[使用Java ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[APIC計算表單資料使用web service ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[APISeting connection propertiesForms Service API快速啟動轉譯互動式PDF](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[](/help/forms/developing/rendering-interactive-pdf-forms.md)
[表單建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#calculate-form-data-using-the-java-api}計算表單資料

使用Forms API(Java)計算表單資料：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。

1. 檢索包含計算指令碼的表單

   * 若要擷取包含計算指令碼的表單資料，請使用其建構函式建立`com.adobe.idp.Document`物件，並從建構函式中叫用`javax.servlet.http.HttpServletResponse`物件的`getInputStream`方法。
   * 叫用`FormsServiceClient`物件的`processFormSubmission`方法並傳遞下列值：

      * 包含表單資料的`com.adobe.idp.Document`物件。
      * 一個字串值，它指定包括所有相關HTTP標題的環境變數。 必須通過為`CONTENT_TYPE`環境變數指定一個或多個值來指定要處理的內容類型。 例如，若要處理XML和PDF資料，請為此參數指定下列字串值：`CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * 指定`HTTP_USER_AGENT`標題值的字串值；例如，`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存運行時選項的`RenderOptionsSpec`對象。

      `processFormSubmission`方法返回包含表單提交結果的`FormsResult`對象。

   * 呼叫`FormsResult`物件的`getAction`方法，確認與提交表單相關的處理狀態為`1`。 如果此方法返回值`1`，則會執行計算並將資料寫回客戶端Web瀏覽器。


1. 將表單資料流寫回用戶端網頁瀏覽器

   * 建立`javax.servlet.ServletOutputStream`物件，用來傳送表單資料串流至用戶端網頁瀏覽器。
   * 通過調用`FormsResult`對象「s `getOutputContent`」方法建立`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 建立位元組陣列，並以`InputStream`物件的`read`方法來填入表單資料流，並將位元組陣列傳入為引數。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**


[包含AEM Forms Java程式庫檔案設](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#calculate-form-data-using-the-web-service-api}計算表單資料

使用Forms API(web service)計算表單資料：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`對象並設定驗證值。

1. 檢索包含計算指令碼的表單

   * 要檢索張貼到Java Servlet的表單資料，請使用其建構子建立`BLOB`對象。
   * 使用`javax.servlet.http.HttpServletResponse`物件的`getInputStream`方法建立`java.io.InputStream`物件。
   * 使用其建構子並傳遞`java.io.InputStream`對象的長度，建立`java.io.ByteArrayOutputStream`對象。
   * 將`java.io.InputStream`對象的內容複製到`java.io.ByteArrayOutputStream`對象中。
   * 通過調用`java.io.ByteArrayOutputStream`對象的`toByteArray`方法建立位元組陣列。
   * 調用`setBinaryData`方法並將位元組陣列作為參數傳遞，以填充`BLOB`對象。
   * 使用其建構子建立`RenderOptionsSpec`對象。 調用`RenderOptionsSpec`物件的`setLocale`方法並傳遞指定地區值的字串值，以設定地區值。
   * 叫用`FormsServiceClient`物件的`processFormSubmission`方法並傳遞下列值：

      * 包含表單資料的`BLOB`物件。
      * 指定環境變數的字串值包括所有相關的HTTP標頭。 例如，您可以指定下列字串值：`HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * 指定`HTTP_USER_AGENT`標題值的字串值；例如，`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存運行時選項的`RenderOptionsSpec`對象。 如需詳細資訊，請造訪。
      * 由方法填充的空`BLOBHolder`對象。
      * 由方法填充的空`javax.xml.rpc.holders.StringHolder`對象。
      * 由方法填充的空`BLOBHolder`對象。
      * 由方法填充的空`BLOBHolder`對象。
      * 由方法填充的空`javax.xml.rpc.holders.ShortHolder`對象。
      * 由方法填充的空`MyArrayOf_xsd_anyTypeHolder`對象。 此參數用於儲存隨表單一起提交的檔案附件。
      * 由方法填入的空`FormsResultHolder`對象，其表單為已提交。

      `processFormSubmission`方法會以表單提交的結果填入`FormsResultHolder`參數。 `processFormSubmission`方法返回包含表單提交結果的`FormsResult`對象。

   * 呼叫`FormsResult`物件的`getAction`方法，確認與提交表單相關的處理狀態為`1`。 如果此方法返回值`1`，則會執行計算並將資料寫回客戶端Web瀏覽器。


1. 將表單資料流寫回用戶端網頁瀏覽器

   * 建立`javax.servlet.ServletOutputStream`物件，用來傳送表單資料串流至用戶端網頁瀏覽器。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 建立位元組陣列，並呼叫`BLOB`物件的`getBinaryData`方法以填入它。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請**
[參閱使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
