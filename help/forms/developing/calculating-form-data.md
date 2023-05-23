---
title: 計算表單資料
seo-title: Calculating Form Data
description: 使用Forms服務計算用戶輸入到表單中的值並顯示結果。 Forms服務使用Java API和Web服務API計算值。
seo-description: Use the Forms service to calculate values that a user enters into a form and display the results. Forms service calculates the values using the Java API and Web Service API.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 0%

---

# 計算表單資料 {#calculating-form-data}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

Forms服務可以計算用戶輸入到表單中的值並顯示結果。 要計算表單資料，必須執行兩項任務。 首先，建立計算表單資料的表單設計指令碼。 表單設計支援三種類型的指令碼。 一種指令碼類型在客戶端上運行，另一種指令碼類型在伺服器上運行，第三種指令碼類型在伺服器和客戶端上運行。 本主題中討論的指令碼類型在伺服器上運行。 HTML、PDF和表單指南（不建議使用）轉換支援伺服器端計算。

作為表單設計流程的一部分，您可以利用計算和指令碼來提供更豐富的用戶體驗。 計算和指令碼可以添加到大多數表單域和對象。 您必須建立表單設計指令碼，以對用戶輸入到互動式表單中的資料執行計算操作。

用戶在表單中輸入值，然後按一下「計算」按鈕查看結果。 以下過程描述了一個示例應用程式，它使用戶能夠計算資料：

* 用戶訪問名為StartLoan.html的HTML頁，該頁用作Web應用程式的起始頁。 此頁調用名為 `GetLoanForm`。
* 的 `GetLoanForm` servlet提供貸款表單。 此表單包含指令碼、交互欄位、計算按鈕和提交按鈕。
* 用戶在表單的欄位中輸入值，然後按一下「計算」按鈕。 表單將發送到 `CalculateData` 執行指令碼的Java Servlet。 該表單將返回給用戶，並在表單中顯示計算結果。
* 用戶繼續輸入和計算值，直到顯示滿意的結果。 滿足要求後，用戶按一下「提交」按鈕處理表單。 該表單將被發送到另一個名為 `ProcessForm` 負責檢索已提交資料。 (請參閱 [處理已提交的Forms](/help/forms/developing/rendering-forms.md#handling-submitted-forms)。)


下圖顯示了應用程式的邏輯流。

![cf_cf_finsrv_localcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

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
   <td><p>的 <code>GetLoanForm</code> 從HTML開始頁調用Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>的 <code>GetLoanForm</code> Java Servlet使用Forms服務客戶端API將貸款表單呈現給客戶端Web瀏覽器。 呈現包含配置為在伺服器上運行的指令碼的表單與呈現不包含指令碼的表單之間的差異在於，您必須指定用於執行指令碼的目標位置。 如果未指定目標位置，則不執行配置為在伺服器上運行的指令碼。 例如，請考慮本節中介紹的應用程式。 的 <code>CalculateData</code> Java Servlet是執行指令碼的目標位置。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用戶將資料輸入到互動式欄位中，然後按一下「計算」按鈕。 表單將發送到 <code>CalculateData</code> 執行指令碼的Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>表單將以表單形式顯示的計算結果呈現回Web瀏覽器。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>當值令人滿意時，用戶按一下「提交」按鈕。 該表單將被發送到另一個名為 <code>ProcessForm</code>。</p></td>
  </tr>
 </tbody>
</table>

通常，作為PDF內容提交的表單包含在客戶端上執行的指令碼。 但是，也可以執行伺服器端計算。 「提交」按鈕不能用於計算指令碼。 在這種情況下，不執行計算，因為Forms服務認為交互已完成。

為了說明窗體設計指令碼的使用，本節將檢查一個簡單的互動式窗體，該窗體包含一個配置為在伺服器上運行的指令碼。 下圖顯示了包含指令碼的表單設計，該指令碼將用戶輸入的值添加到前兩個欄位中，並在第三個欄位中顯示結果。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**答：** 名為NumericField1的欄位 **B** 名為NumericField2的欄位 **C.** 名為NumericField3的欄位

此窗體設計中指令碼的語法如下：

```javascript
     NumericField3 = NumericField2 + NumericField1
```

在此窗體設計中，「計算」按鈕是命令按鈕，指令碼位於此按鈕的 `Click` 的子菜單。 當用戶在前兩個欄位（NumericField1和NumericField2）中輸入值並按一下「計算」按鈕時，表單將發送到執行指令碼的Forms服務。 Forms服務將表單呈現回客戶端設備，計算結果顯示在NumericField3欄位中。

>[!NOTE]
>
>有關建立表單設計指令碼的資訊，請參見 [Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw)。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要計算表單資料，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms客戶端API對象。
1. 檢索包含計算指令碼的表單。
1. 將表單資料流寫回客戶端Web瀏覽器

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms客戶端API對象**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立Forms服務客戶端。 如果使用Java API，請建立 `FormsServiceClient` 的雙曲餘切值。 如果使用FormsWeb服務API，請建立 `FormsServiceService` 的雙曲餘切值。

**檢索包含計算指令碼的表單**

您可以使用Forms服務客戶端API建立應用程式邏輯，該邏輯處理包含配置為在伺服器上運行的指令碼的表單。 該過程類似於處理提交的表單。 (請參閱 [處理已提交的Forms](/help/forms/developing/handling-submitted-forms.md)。)

驗證與提交的表單關聯的處理狀態是否為 `1` `(Calculate)`，這意味著Forms服務正在對表單資料執行計算操作，結果必須寫回給用戶。 在這種情況下，將自動執行配置為在伺服器上運行的指令碼。

**將表單資料流寫回客戶端Web瀏覽器**

驗證與已提交表單關聯的處理狀態後 `1`，必須將結果寫回客戶端web瀏覽器。 顯示表單時，計算值將出現在相應的欄位中。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[使用Java API計算表單資料](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[使用Web服務API計算表單資料](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)
[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API計算表單資料 {#calculate-form-data-using-the-java-api}

使用FormsAPI(Java)計算表單資料：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立Forms客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索包含計算指令碼的表單

   * 要檢索包含計算指令碼的表單資料，請建立 `com.adobe.idp.Document` 使用其建構子調用對象 `javax.servlet.http.HttpServletResponse` 對象 `getInputStream` 方法。
   * 調用 `FormsServiceClient` 對象 `processFormSubmission` 方法並傳遞以下值：

      * 的 `com.adobe.idp.Document` 包含窗體資料的對象。
      * 一個字串值，它指定包括所有相關HTTP標頭的環境變數。 必須通過為 `CONTENT_TYPE` 環境變數。 例如，要處理XML和PDF資料，請為此參數指定以下字串值： `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值；比如說， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * A `RenderOptionsSpec` 儲存運行時選項的對象。

      的 `processFormSubmission` 方法返回 `FormsResult` 包含表單提交結果的對象。

   * 驗證與已提交表單關聯的處理狀態是否為 `1` 通過調用 `FormsResult` 對象 `getAction` 的雙曲餘切值。 如果此方法返回值 `1`進行了計算，資料可以寫回客戶端web瀏覽器。


1. 將表單資料流寫回客戶端Web瀏覽器

   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流發送到客戶端web瀏覽器的對象。
   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read` 方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**


[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API計算表單資料 {#calculate-form-data-using-the-web-service-api}

使用FormsAPI（Web服務）計算表單資料：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包括到類路徑中。

1. 建立Forms客戶端API對象

   建立 `FormsService` 對象和設定驗證值。

1. 檢索包含計算指令碼的表單

   * 要檢索已發佈到Java Servlet的表單資料，請建立 `BLOB` 對象。
   * 建立 `java.io.InputStream` 對象 `javax.servlet.http.HttpServletResponse` 對象 `getInputStream` 的雙曲餘切值。
   * 建立 `java.io.ByteArrayOutputStream` 對象，使用其建構子並傳遞 `java.io.InputStream` 的雙曲餘切值。
   * 複製 `java.io.InputStream` 對象 `java.io.ByteArrayOutputStream` 的雙曲餘切值。
   * 通過調用 `java.io.ByteArrayOutputStream` 對象 `toByteArray` 的雙曲餘切值。
   * 填充 `BLOB` 通過調用對象 `setBinaryData` 方法，並將位元組陣列作為參數傳遞。
   * 建立 `RenderOptionsSpec` 對象。 通過調用 `RenderOptionsSpec` 對象 `setLocale` 方法，並傳遞指定區域設定值的字串值。
   * 調用 `FormsServiceClient` 對象 `processFormSubmission` 方法並傳遞以下值：

      * 的 `BLOB` 包含窗體資料的對象。
      * 一個字串值，它指定包含所有相關HTTP標頭的環境變數。 例如，可以指定以下字串值： `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * 一個字串值，它指定 `HTTP_USER_AGENT` 標題值；比如說， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * A `RenderOptionsSpec` 儲存運行時選項的對象。 有關詳細資訊，。
      * 空 `BLOBHolder` 由方法填充的對象。
      * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。
      * 空 `BLOBHolder` 由方法填充的對象。
      * 空 `BLOBHolder` 由方法填充的對象。
      * 空 `javax.xml.rpc.holders.ShortHolder` 由方法填充的對象。
      * 空 `MyArrayOf_xsd_anyTypeHolder` 由方法填充的對象。 此參數用於儲存隨表單一起提交的檔案附件。
      * 空 `FormsResultHolder` 由方法填充且已提交表單的對象。

      的 `processFormSubmission` 方法填充 `FormsResultHolder` 參數。 的 `processFormSubmission` 方法返回 `FormsResult` 包含表單提交結果的對象。

   * 驗證與已提交表單關聯的處理狀態是否為 `1` 通過調用 `FormsResult` 對象 `getAction` 的雙曲餘切值。 如果此方法返回值 `1`進行了計算，資料可以寫回客戶端web瀏覽器。


1. 將表單資料流寫回客戶端Web瀏覽器

   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流發送到客戶端web瀏覽器的對象。
   * 建立 `BLOB` 通過調用包含表單資料的對象 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
   * 建立位元組陣列，並通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。 此任務分配 `FormsResult` 對象。
   * 調用 `javax.servlet.http.HttpServletResponse` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**
[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
