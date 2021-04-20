---
title: 在客戶端呈現Forms
seo-title: 在客戶端呈現Forms
description: 使用Acrobat或Adobe Reader的用戶端轉換功能，以最佳化PDF內容的傳送方式，並改善Forms服務處理網路負載的能力
seo-description: 使用Acrobat或Adobe Reader的用戶端轉換功能，以最佳化PDF內容的傳送方式，並改善Forms服務處理網路負載的能力
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# 在客戶端上呈現Forms{#rendering-forms-at-the-client}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

## 在客戶端上呈現Forms{#rendering-forms-at-the-client-inner}

您可以使用Acrobat或Adobe Reader的用戶端轉譯功能，最佳化PDF內容的傳送，並改善Forms服務處理網路負載的能力。 此程式稱為在客戶端上呈現表單。 若要在用戶端上轉譯表格，用戶端裝置（通常是網頁瀏覽器）必須使用Acrobat 7.0或Adobe Reader7.0或更新版本。

對伺服器端指令碼執行的表單所做的更改不會反映在客戶端呈現的表單中，除非根子表單包含設定為`auto`的`restoreState`屬性。 有關此屬性的詳細資訊，請參閱[Forms設計師。](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

要在客戶端上渲染表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定用戶端轉譯執行時期選項。
1. 在用戶端上演算表格。
1. 將表單寫入用戶端網頁瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立Forms服務客戶端。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms網站服務API，請建立`FormsService`物件。

**設定客戶端渲染運行時選項**

您必須將`RenderAtClient`運行時選項設定為`true`，將客戶端渲染運行時選項設定為在客戶端渲染表單。 這會導致表單被傳送至要轉譯的用戶端裝置。 如果`RenderAtClient`是`auto`（預設值），表單設計會決定表單是否在用戶端呈現。 表單設計必須是具有可流動版面的表單設計。

您可以設定的選用執行時期選項是`SeedPDF`選項。 `SeedPDF`選項結合了PDF容器（種子PDF檔案）與表單設計和XML資料。 表單設計和XML資料都會傳送至Acrobat或Adobe Reader，以便轉換表單。 `SeedPDF`選項可在用戶端電腦沒有表單中使用的字型時使用，例如當使用者未取得授權使用表單擁有者有權使用的字型時。

您可以使用Designer建立簡單的動態PDF檔案，做為種子PDF檔案。 執行此任務需要執行以下步驟：

1. 確定您是否需要在種子PDF檔案中嵌入任何字型。 種子PDF檔案必須包含所轉譯表單所需的其他字型。 將字型內嵌至種子PDF檔案時，請確定您未違反任何字型授權合約。 在Designer中，您可以決定是否可以合法地內嵌字型。 在儲存時，如果有字型無法內嵌在表單中，設計人員會顯示訊息，列出您無法內嵌的字型。 對於靜態PDF文檔，Designer中不會顯示此消息。
1. 如果您要在Designer中建立種子PDF檔案，建議您至少新增包含訊息的文字欄位。 訊息應針對舊版Adobe Reader的使用者，指出他們需要Acrobat 7.0或更新版本或Adobe Reader7.0或更新版本才能檢視檔案。
1. 將種子PDF檔案儲存為動態PDF檔案，副檔名為PDF。

>[!NOTE]
>
>您不需要定義種子PDF執行時期選項，就能在用戶端上轉換表單。 如果您未指定種子PDF,Forms服務會建立一個殼層pdf，其中不包含COS物件，但將包含內嵌實際XDP內容的PDF包裝函式。 本節中的步驟不會設定種子PDF執行時期選項。 有關COS對象的資訊，請參閱《Adobe PDF參考指南》。

**在用戶端上演算表格**

若要在用戶端上轉換表格，您必須確保在應用程式邏輯中包含用戶端轉換執行時期選項，才能轉換表格。

**將表單資料串流寫入用戶端網頁瀏覽器**

Forms服務會建立一個表單資料流，您必須將其寫入客戶端Web瀏覽器。 當寫入用戶端網頁瀏覽器時，表單會由Acrobat 7.0或Adobe Reader7.0或更新版本轉譯，並且對使用者可見。

**另請參閱**

[使用Java API在用戶端演算表格](#render-a-form-at-the-client-using-the-java-api)

[使用web service API在用戶端演算表格](#render-a-form-at-the-client-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms](/help/forms/developing/passing-documents-forms-service.md)

[建立轉譯Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#render-a-form-at-the-client-using-the-java-api}在用戶端演算表格

使用FormsAPI(Java)在用戶端演算表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。

1. 設定客戶端渲染運行時選項

   * 使用其建構子建立`PDFFormRenderSpec`對象。
   * 調用`PDFFormRenderSpec`物件的`setRenderAtClient`方法並傳遞列舉值`RenderAtClient.Yes`，以設定`RenderAtClient`執行時期選項。

1. 在用戶端上演算表格

   叫用`FormsServiceClient`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參考屬於AEM Forms應用程式的表單設計，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * `PDFFormRenderSpec`物件，儲存在用戶端上轉譯表單所需的執行時期選項。
   * `URLSpec`物件，包含Forms服務在轉換表單時所需的URI值。
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

**另請參閱**

[快速入門（SOAP模式）:使用Java API在用戶端轉譯表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#render-a-form-at-the-client-using-the-web-service-api}在用戶端演算表格

使用FormsAPI(web service)在用戶端轉譯表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`對象並設定驗證值。

1. 設定客戶端渲染運行時選項

   * 使用其建構子建立`PDFFormRenderSpec`對象。
   * 調用`PDFFormRenderSpec`物件的`setRenderAtClient`方法並傳遞字串值`RenderAtClient.Yes`，以設定`RenderAtClient`執行時期選項。

1. 在用戶端上演算表格

   叫用`FormsService`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參考屬於Forms應用程式的表單設計，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞`null`。 (請參閱[使用可流式版面預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md))。
   * `PDFFormRenderSpec`物件，儲存在用戶端上轉譯表單所需的執行時期選項。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`對象。 此參數用於儲存轉譯的PDF表單。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`對象。 （此引數將儲存表單中的頁數）。
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`對象。 （此引數將儲存地區值）。
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

**另請參閱**

[在客戶端呈現Forms](#rendering-forms-at-the-client)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
