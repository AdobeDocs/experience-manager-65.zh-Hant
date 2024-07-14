---
title: 計算表單資料
description: 使用Forms服務來計算使用者在表單中輸入的值並顯示結果。 Forms服務會使用Java API和Web服務API來計算值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# 計算表單資料 {#calculating-form-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

Forms服務可以計算使用者在表單中輸入的值並顯示結果。 若要計算表單資料，您必須執行兩項工作。 首先，建立表單設計指令碼，以計算表單資料。 表單設計支援三種型別的指令碼。 一種指令碼型別在使用者端上執行，另一種在伺服器上執行，第三種型別同時在伺服器和使用者端上執行。 本主題中討論的指令碼型別會在伺服器上執行。 HTML、PDF和表單指南（已棄用）轉換支援伺服器端計算。

在表單設計過程中，您可以使用計算和指令碼來提供更豐富的使用者體驗。 大多數的表單欄位和物件都可以新增計算與指令碼。 建立表單設計指令碼，以針對使用者輸入互動式表單的資料執行計算操作。

使用者在表單中輸入值，然後按一下「計算」按鈕來檢視結果。 下列程式說明可讓使用者計算資料的範例應用程式：

* 使用者存取名為StartLoan.html的HTML頁面，做為網頁應用程式的起始頁面。 此頁面會叫用名為`GetLoanForm`的Java Servlet。
* `GetLoanForm` servlet轉譯貸款表單。 此表單包含指令碼、互動欄位、計算按鈕和提交按鈕。
* 使用者在表單的欄位中輸入值，然後按一下計算按鈕。 表單會傳送至`CalculateData` Java Servlet，並在其中執行指令碼。 表單會傳回給使用者，並在表單中顯示計算結果。
* 使用者繼續輸入和計算值，直到顯示滿意的結果為止。 滿意後，使用者按一下「提交」按鈕處理表單。 表單會傳送給另一個名為`ProcessForm`的Java Servlet，負責擷取提交的資料。 (請參閱[處理已提交的Forms](/help/forms/developing/rendering-forms.md#handling-submitted-forms)。)


下圖顯示應用程式的邏輯流程。

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

下表說明此圖表中的步驟。

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
   <td><p>從HTML起始頁面叫用<code>GetLoanForm</code> Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Java Servlet使用Forms服務使用者端API將貸款表單轉譯給使用者端網頁瀏覽器。 轉譯含有設定要在伺服器上執行之指令碼的表單與轉譯不含指令碼的表單的區別在於，您必須指定用於執行指令碼的目標位置。 如果未指定目標位置，則不會執行設定為在伺服器上執行的指令碼。 例如，請考量本節中介紹的應用程式。 <code>CalculateData</code> Java Servlet是執行指令碼的目標位置。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者在互動式欄位中輸入資料，然後按一下計算按鈕。 表單會傳送至<code>CalculateData</code> Java Servlet，並在其中執行指令碼。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>表單會呈現回網頁瀏覽器，並在表單中顯示計算結果。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>值符合要求時，使用者按一下「提交」按鈕。 表單傳送至另一個名為<code>ProcessForm</code>的Java Servlet。</p></td>
  </tr>
 </tbody>
</table>

通常，作為PDF內容提交的表單包含使用者端執行的指令碼。 不過，也可以執行伺服器端計算。 提交按鈕無法用於計算指令碼。 在此情況下，計算不會執行，因為Forms服務會將互動視為完成。

為了說明表單設計指令碼的使用情況，本節將檢查一個簡單的互動式表單，其中包含設定為在伺服器上執行的指令碼。 下圖顯示一個表單設計，其中包含指令碼，該指令碼會新增使用者在前兩個欄位輸入的值，並在第三個欄位中顯示結果。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.**&#x200B;名為NumericField1 **B.**&#x200B;名為NumericField2 **C.**&#x200B;名為NumericField3的欄位

此表單設計中指令碼的語法如下：

```javascript
     NumericField3 = NumericField2 + NumericField1
```

在此表單設計中，[計算]按鈕是命令按鈕，而且指令碼位於此按鈕的`Click`事件中。 當使用者在前兩個欄位（NumericField1和NumericField2）中輸入值並按一下「計算」按鈕時，表單會傳送到Forms服務以執行指令碼。 Forms服務會將表單轉譯回使用者端裝置，且計算結果會顯示在NumericField3欄位中。

>[!NOTE]
>
>如需建立表單設計指令碼的詳細資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

若要計算表單資料，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 擷取包含計算指令碼的表單。
1. 將表單資料流寫回使用者端網頁瀏覽器

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API作業。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms Web服務API，請建立`FormsServiceService`物件。

**擷取包含計算指令碼的表單**

您可以使用Forms服務使用者端API建立應用程式邏輯，以處理包含已設定要在伺服器上執行的指令碼的表單。 此程式與處理提交的表單類似。 (請參閱[處理已提交的Forms](/help/forms/developing/handling-submitted-forms.md)。)

確認與提交的表單關聯的處理狀態為`1` `(Calculate)`，這表示Forms服務正在表單資料上執行計算作業，且結果必須寫回使用者。 在此情況下，會自動執行設定為要在伺服器上執行的指令碼。

**將表單資料流寫回使用者端網頁瀏覽器**

確認與已提交表單關聯的處理狀態為`1`之後，您必須將結果寫回使用者端網頁瀏覽器。 顯示表單時，計算值會出現在適當欄位中。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[使用Java API計算表單資料](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[使用網站服務API計算表單資料](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[正在設定連線內容](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)
[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API計算表單資料 {#calculate-form-data-using-the-java-api}

使用Forms API (Java)計算表單資料：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormsServiceClient`物件。

1. 擷取包含計算指令碼的表單

   * 若要擷取包含計算指令碼的表單資料，請使用其建構函式建立`com.adobe.idp.Document`物件，並從建構函式中叫用`javax.servlet.http.HttpServletResponse`物件的`getInputStream`方法。
   * 叫用`FormsServiceClient`物件的`processFormSubmission`方法，並傳遞下列值：

      * 包含表單資料的`com.adobe.idp.Document`物件。
      * 字串值，指定包含所有相關HTTP標頭的環境變數。 為`CONTENT_TYPE`環境變數指定一或多個值，以指定要處理的內容型別。 例如，若要處理XML和PDF資料，請為此引數指定下列字串值： `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * 字串值，指定`HTTP_USER_AGENT`標頭值；例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存執行階段選項的`RenderOptionsSpec`物件。

     `processFormSubmission`方法傳回包含表單提交結果的`FormsResult`物件。

   * 透過叫用`FormsResult`物件的`getAction`方法，確認與已提交表單關聯的處理狀態為`1`。 如果此方法傳回值`1`，則會執行計算，而且資料可以寫回使用者端網頁瀏覽器。

1. 將表單資料流寫回使用者端網頁瀏覽器

   * 建立用來傳送表單資料流至使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件。
   * 呼叫`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 呼叫`InputStream`物件的`read`方法，並將位元組陣列作為引數傳遞，以建立位元組陣列並以表單資料串流填入。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**


[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[正在設定連線內容](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API計算表單資料 {#calculate-form-data-using-the-web-service-api}

使用Forms API （網站服務）計算表單資料：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立`FormsService`物件並設定驗證值。

1. 擷取包含計算指令碼的表單

   * 若要擷取張貼到Java Servlet的表單資料，請使用其建構函式建立`BLOB`物件。
   * 使用`javax.servlet.http.HttpServletResponse`物件的`getInputStream`方法建立`java.io.InputStream`物件。
   * 使用物件的建構函式並傳遞`java.io.InputStream`物件的長度，以建立`java.io.ByteArrayOutputStream`物件。
   * 將`java.io.InputStream`物件的內容複製到`java.io.ByteArrayOutputStream`物件中。
   * 透過叫用`java.io.ByteArrayOutputStream`物件的`toByteArray`方法建立位元組陣列。
   * 叫用物件的`setBinaryData`方法，並將位元組陣列作為引數傳遞，以填入`BLOB`物件。
   * 使用物件的建構函式建立`RenderOptionsSpec`物件。 透過叫用`RenderOptionsSpec`物件的`setLocale`方法並傳遞指定地區設定值的字串值來設定地區設定值。
   * 叫用`FormsServiceClient`物件的`processFormSubmission`方法，並傳遞下列值：

      * 包含表單資料的`BLOB`物件。
      * 字串值，指定包含所有相關HTTP標頭的環境變數。 例如，您可以指定下列字串值： `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * 字串值，指定`HTTP_USER_AGENT`標頭值；例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存執行階段選項的`RenderOptionsSpec`物件。 如需詳細資訊，請參閱。
      * 方法填入的空白`BLOBHolder`物件。
      * 方法填入的空白`javax.xml.rpc.holders.StringHolder`物件。
      * 方法填入的空白`BLOBHolder`物件。
      * 方法填入的空白`BLOBHolder`物件。
      * 方法填入的空白`javax.xml.rpc.holders.ShortHolder`物件。
      * 方法填入的空白`MyArrayOf_xsd_anyTypeHolder`物件。 此引數用於儲存與表單一起提交的檔案附件。
      * 空的`FormsResultHolder`物件由方法以提交的表單填入。

     `processFormSubmission`方法會將表單提交的結果填入`FormsResultHolder`引數。 `processFormSubmission`方法傳回包含表單提交結果的`FormsResult`物件。

   * 透過叫用`FormsResult`物件的`getAction`方法，確認與已提交表單關聯的處理狀態為`1`。 如果此方法傳回值`1`，則會執行計算，而且資料可以寫回使用者端網頁瀏覽器。

1. 將表單資料流寫回使用者端網頁瀏覽器

   * 建立用來傳送表單資料流至使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 建立位元組陣列，並透過叫用`BLOB`物件的`getBinaryData`方法來填入該陣列。 此工作會將`FormsResult`物件的內容指派給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**
[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
