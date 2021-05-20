---
title: 計算表單資料
seo-title: 計算表單資料
description: 使用Forms服務來計算使用者輸入表單中的值，並顯示結果。 Forms服務會使用Java API和網站服務API來計算值。
seo-description: 使用Forms服務來計算使用者輸入表單中的值，並顯示結果。 Forms服務會使用Java API和網站服務API來計算值。
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
source-wordcount: '1916'
ht-degree: 0%

---

# 計算表單資料{#calculating-form-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

Forms服務可計算使用者在表單中輸入的值，並顯示結果。 若要計算表單資料，您必須執行兩項工作。 首先，您要建立計算表單資料的表單設計指令碼。 表單設計支援三種類型的指令碼。 一種指令碼類型在客戶端上運行，另一種類型在伺服器上運行，第三種類型在伺服器和客戶端上運行。 本主題中討論的指令碼類型在伺服器上運行。 HTML、PDF和表單指南（已過時）轉換支援伺服器端計算。

在表單設計程式中，您可以運用計算和指令碼，提供更豐富的使用者體驗。 計算和指令碼可新增至大部分表單欄位和物件。 您必須建立表單設計指令碼，以對使用者進入互動式表單的資料執行計算操作。

使用者在表單中輸入值，然後按一下「計算」按鈕以檢視結果。 以下過程描述了一個示例應用程式，它使用戶能夠計算資料：

* 使用者存取名為StartLoan.html的HTML頁面，該頁面作為Web應用程式的開始頁面。 此頁調用名為`GetLoanForm`的Java Servlet。
* `GetLoanForm` servlet呈現貸款表單。 此表單包含指令碼、互動式欄位、計算按鈕和提交按鈕。
* 使用者在表單的欄位中輸入值，然後按一下「計算」按鈕。 表單會傳送至`CalculateData`執行指令碼的Java Servlet。 表單會傳回給使用者，且表單中會顯示計算結果。
* 用戶繼續輸入和計算值，直到顯示滿意的結果。 完成確認後，用戶按一下「提交」按鈕以處理表單。 表單會傳送至另一個名為`ProcessForm`的Java Servlet，該Servlet負責擷取已提交的資料。 (請參閱[處理已提交的Forms](/help/forms/developing/rendering-forms.md#handling-submitted-forms)。)


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
   <td><p>從HTML開始頁面叫用<code>GetLoanForm</code> Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Java Servlet使用Forms服務客戶端API來向客戶端Web瀏覽器呈現貸款表單。 呈現包含配置為在伺服器上運行的指令碼的表單和呈現不包含指令碼的表單之間的差異在於，您必須指定用於執行指令碼的目標位置。 如果未指定目標位置，則不會執行配置為在伺服器上運行的指令碼。 例如，請考量本節中引入的應用程式。 <code>CalculateData</code> Java Servlet是執行指令碼的目標位置。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者將資料輸入互動式欄位，然後按一下「計算」按鈕。 表單會傳送至<code>CalculateData</code> Java Servlet，在其中執行指令碼。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>表單會呈現回網頁瀏覽器，且表單中會顯示計算結果。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>當值滿意時，使用者按一下「提交」按鈕。 表單會傳送至另一個名為<code>ProcessForm</code>的Java Servlet。</p></td>
  </tr>
 </tbody>
</table>

通常，以PDF內容提交的表單包含在用戶端上執行的指令碼。 不過，也可執行伺服器端計算。 「提交」按鈕無法用於計算指令碼。 在此情況下，不會執行計算，因為Forms服務會將互動視為完成。

為了說明表單設計指令碼的使用方式，本節將檢查一個簡單的互動式表單，該表單包含一個配置為在伺服器上運行的指令碼。 下圖顯示的表單設計包含一個指令碼，該指令碼將用戶輸入到前兩個欄位中的值添加到第三個欄位中，並顯示結果。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** 名為NumericField1的 **欄位B.** 名為NumericField2 C. **A的欄** 位名為NumericField3

此表單設計中指令碼的語法如下：

```javascript
     NumericField3 = NumericField2 + NumericField1
```

在此窗體設計中，「計算」按鈕是命令按鈕，該指令碼位於此按鈕的`Click`事件中。 當使用者在前兩個欄位（NumericField1和NumericField2）中輸入值，然後按一下「計算」按鈕時，表單會傳送至Forms服務，在該服務中執行指令碼。 Forms服務會將表單轉譯回用戶端裝置，而NumericField3欄位中會顯示計算結果。

>[!NOTE]
>
>有關建立表單設計指令碼的資訊，請參閱[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟{#summary-of-steps}的摘要

要計算表單資料，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 檢索包含計算指令碼的表單。
1. 將表單資料流寫回客戶端Web瀏覽器

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API作業。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms Web服務API，請建立`FormsServiceService`物件。

**檢索包含計算指令碼的表單**

您可使用Forms服務用戶端API來建立應用程式邏輯，以處理包含設定為在伺服器上執行之指令碼的表單。 此程式類似於處理提交的表單。 (請參閱[處理已提交的Forms](/help/forms/developing/handling-submitted-forms.md)。)

確認與提交的表單相關聯的處理狀態為`1` `(Calculate)` ，這表示Forms服務正在對表單資料執行計算操作，且必須將結果寫回給用戶。 在此情況下，會自動執行設定為在伺服器上執行的指令碼。

**將表單資料流寫回客戶端Web瀏覽器**

在驗證與已提交表單相關聯的處理狀態為`1`後，必須將結果寫回客戶端Web瀏覽器。 顯示表單時，計算值會出現在適當欄位中。

**另請參閱**

[包括AEM Forms Java庫檔](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[案使用Java APIC計算表單資料使用Web](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[服務API計算表單資](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[料設定連](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[接屬性Forms服務API快速入門轉](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[譯互動式PDF表單建](/help/forms/developing/rendering-interactive-pdf-forms.md)
[立轉譯Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#calculate-form-data-using-the-java-api}計算表單資料

使用Forms API(Java)計算表單資料：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormsServiceClient`物件。

1. 檢索包含計算指令碼的表單

   * 要檢索包含計算指令碼的表單資料，請使用其建構子並從建構子中調用`javax.servlet.http.HttpServletResponse`對象的`getInputStream`方法來建立`com.adobe.idp.Document`對象。
   * 調用`FormsServiceClient`對象的`processFormSubmission`方法並傳遞以下值：

      * 包含表單資料的`com.adobe.idp.Document`物件。
      * 一個字串值，它指定包括所有相關HTTP標題的環境變數。 您必須為`CONTENT_TYPE`環境變數指定一或多個值，以指定要處理的內容類型。 例如，要處理XML和PDF資料，請為此參數指定以下字串值：`CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * 指定`HTTP_USER_AGENT`標題值的字串值；例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存運行時選項的`RenderOptionsSpec`對象。

      `processFormSubmission`方法會傳回包含表單提交結果的`FormsResult`物件。

   * 叫用`FormsResult`物件的`getAction`方法，以確認與已提交表單相關聯的處理狀態為`1`。 如果此方法返回值`1`，則執行了計算，並可將資料寫回客戶端Web瀏覽器。


1. 將表單資料流寫回客戶端Web瀏覽器

   * 建立`javax.servlet.ServletOutputStream`物件，用於將表單資料流傳送至用戶端網頁瀏覽器。
   * 調用`FormsResult`對象s `getOutputContent`方法，建立`com.adobe.idp.Document`對象。
   * 調用`com.adobe.idp.Document`對象的`getInputStream`方法，建立`java.io.InputStream`對象。
   * 叫用`InputStream`物件的`read`方法，並將位元組陣列傳遞為引數，借此建立位元組陣列，並填入表單資料流。
   * 調用`javax.servlet.ServletOutputStream`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**


[包括AEM Forms Java庫檔](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[案設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API {#calculate-form-data-using-the-web-service-api}計算表單資料

使用Forms API（網站服務）計算表單資料：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`物件並設定驗證值。

1. 檢索包含計算指令碼的表單

   * 要檢索發佈到Java Servlet的表單資料，請使用其建構子建立`BLOB`對象。
   * 使用`javax.servlet.http.HttpServletResponse`對象的`getInputStream`方法建立`java.io.InputStream`對象。
   * 使用其建構子並傳遞`java.io.InputStream`物件的長度，以建立`java.io.ByteArrayOutputStream`物件。
   * 將`java.io.InputStream`對象的內容複製到`java.io.ByteArrayOutputStream`對象中。
   * 調用`java.io.ByteArrayOutputStream`對象的`toByteArray`方法，建立位元組陣列。
   * 叫用`setBinaryData`方法並將位元組陣列傳遞為引數，以填入`BLOB`物件。
   * 使用其建構子建立`RenderOptionsSpec`物件。 通過調用`RenderOptionsSpec`對象的`setLocale`方法並傳遞指定區域設定值的字串值來設定區域設定值。
   * 調用`FormsServiceClient`對象的`processFormSubmission`方法並傳遞以下值：

      * 包含表單資料的`BLOB`物件。
      * 指定環境變數的字串值包含所有相關的HTTP標題。 例如，您可以指定下列字串值：`HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * 指定`HTTP_USER_AGENT`標題值的字串值；例如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 儲存運行時選項的`RenderOptionsSpec`對象。 如需詳細資訊，請參閱。
      * 由方法填入的空`BLOBHolder`物件。
      * 由方法填入的空`javax.xml.rpc.holders.StringHolder`物件。
      * 由方法填入的空`BLOBHolder`物件。
      * 由方法填入的空`BLOBHolder`物件。
      * 由方法填入的空`javax.xml.rpc.holders.ShortHolder`物件。
      * 由方法填入的空`MyArrayOf_xsd_anyTypeHolder`物件。 此參數用於儲存隨表單提交的檔案附件。
      * 由方法填入的空白`FormsResultHolder`物件，其表單為已提交。

      `processFormSubmission`方法會以表單提交的結果填入`FormsResultHolder`參數。 `processFormSubmission`方法會傳回包含表單提交結果的`FormsResult`物件。

   * 叫用`FormsResult`物件的`getAction`方法，以確認與已提交表單相關聯的處理狀態為`1`。 如果此方法返回值`1`，則執行了計算，並可將資料寫回客戶端Web瀏覽器。


1. 將表單資料流寫回客戶端Web瀏覽器

   * 建立`javax.servlet.ServletOutputStream`物件，用於將表單資料流傳送至用戶端網頁瀏覽器。
   * 調用`FormsResult`對象的`getOutputContent`方法，建立包含表單資料的`BLOB`對象。
   * 建立位元組陣列，並調用`BLOB`對象的`getBinaryData`方法來填入。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 調用`javax.servlet.http.HttpServletResponse`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請**
[參閱使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
