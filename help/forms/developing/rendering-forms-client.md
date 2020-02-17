---
title: 在用戶端轉換表單
seo-title: 在用戶端轉換表單
description: 'null'
seo-description: 'null'
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在用戶端轉換表單 {#rendering-forms-at-the-client}

## 在用戶端轉換表單 {#rendering-forms-at-the-client-inner}

您可以使用Acrobat或Adobe Reader的用戶端轉譯功能，最佳化PDF內容的傳送，並改善Forms服務處理網路負載的能力。 此程式稱為在客戶端上呈現表單。 若要在用戶端上轉譯表格，用戶端裝置（通常是網頁瀏覽器）必須使用Acrobat 7.0或Adobe Reader 7.0或更新版本。

伺服器端指令碼執行對表單所做的變更不會反映在用戶端上呈現的表單中，除非根子表單包含設 `restoreState` 定為的屬性 `auto`。 有關此屬性的詳細資訊，請參 [閱Forms Designer。](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要在客戶端上渲染表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定用戶端轉譯執行時期選項。
1. 在用戶端上演算表格。
1. 將表單寫入用戶端網頁瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API操作。 如果您使用Java API，請建立物 `FormsServiceClient` 件。 如果您使用Forms web service API，請建立物 `FormsService` 件。

**設定客戶端渲染運行時選項**

您必須將客戶端渲染運行時選項設定為，以便在客戶端上渲染表 `RenderAtClient` 單，方法是將運行時選項設定為 `true`。 這會導致表單被傳送至要轉譯的用戶端裝置。 如果 `RenderAtClient` 是 `auto` （預設值），表單設計會決定是否在用戶端上呈現表單。 表單設計必須是具有可流動版面的表單設計。

您可以設定的可選執行時期選項為 `SeedPDF` 選項。 此選 `SeedPDF` 項結合了PDF容器（種子PDF檔案）與表單設計和XML資料。 表單設計和XML資料都會傳送至Acrobat或Adobe Reader，然後在Acrobat或Adobe Reader中轉譯表單。 當用 `SeedPDF` 戶端電腦沒有表單中使用的字型時，可使用此選項，例如當使用者未取得授權使用表單擁有者有權使用的字型時。

您可以使用Designer建立簡單的動態PDF檔案，做為種子PDF檔案。 執行此任務需要執行以下步驟：

1. 確定您是否需要在種子PDF檔案中嵌入任何字型。 種子PDF檔案必須包含所轉譯表單所需的其他字型。 將字型內嵌至種子PDF檔案時，請確定您未違反任何字型授權合約。 在Designer中，您可以決定是否可以合法地內嵌字型。 在儲存時，如果有字型無法內嵌在表單中，設計人員會顯示訊息，列出您無法內嵌的字型。 對於靜態PDF文檔，Designer中不會顯示此消息。
1. 如果您要在Designer中建立種子PDF檔案，建議您至少新增包含訊息的文字欄位。 訊息應針對舊版Adobe Reader的使用者，指出他們需要Acrobat 7.0或更新版本或Adobe Reader 7.0或更新版本才能檢視檔案。
1. 將種子PDF檔案儲存為動態PDF檔案，副檔名為PDF。

>[!NOTE]
>
>您不需要定義種子PDF執行時期選項，就能在用戶端上轉換表單。 如果您未指定種子PDF,Forms服務會建立一個外殼pdf，其中不包含COS物件，但將包含內嵌實際XDP內容的PDF包裝函式。 本節中的步驟不會設定種子PDF執行時期選項。 如需COS物件的詳細資訊，請參閱Adobe PDF參考指南。

**在用戶端上演算表格**

若要在用戶端上轉換表格，您必須確保在應用程式邏輯中包含用戶端轉換執行時期選項，才能轉換表格。

**將表單資料串流寫入用戶端網頁瀏覽器**

Forms服務會建立必須寫入客戶端Web瀏覽器的表單資料流。 當寫入用戶端網頁瀏覽器時，表格會由Acrobat 7.0或Adobe Reader 7.0或更新版本轉譯，而且使用者可以看見。

**另請參閱**

[使用Java API在用戶端演算表格](#render-a-form-at-the-client-using-the-java-api)

[使用web service API在用戶端演算表格](#render-a-form-at-the-client-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳送至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API在用戶端演算表格 {#render-a-form-at-the-client-using-the-java-api}

使用Forms API(Java)在用戶端演算表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定客戶端渲染運行時選項

   * 使用其 `PDFFormRenderSpec` 建構函式建立物件。
   * 調用 `RenderAtClient` 物件的方法並傳遞 `PDFFormRenderSpec` 列舉值， `setRenderAtClient` 以設定執行時期選項 `RenderAtClient.Yes`。

1. 在用戶端上演算表格

   叫用物 `FormsServiceClient` 件的方 `renderPDFForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參考屬於AEM Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包 `com.adobe.idp.Document` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞空 `com.adobe.idp.Document` 物件。
   * 存 `PDFFormRenderSpec` 儲在客戶端上渲染表單所需運行時選項的對象。
   * 包 `URLSpec` 含Forms服務渲染表單所需的URI值的對象。
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

**另請參閱**

[快速入門（SOAP模式）:使用Java API在用戶端轉譯表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API在用戶端演算表格 {#render-a-form-at-the-client-using-the-web-service-api}

使用Forms API(web service)在用戶端演算表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立對 `FormsService` 像並設定驗證值。

1. 設定客戶端渲染運行時選項

   * 使用其 `PDFFormRenderSpec` 建構函式建立物件。
   * 調用 `RenderAtClient` 物件的方法並傳遞字串值， `PDFFormRenderSpec` 以設定 `setRenderAtClient` 執行時期選項 `RenderAtClient.Yes`。

1. 在用戶端上演算表格

   叫用物 `FormsService` 件的方 `renderPDFForm` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包 `BLOB` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞 `null`。 (請參 [閱「使用可排程版面預填表單」](/help/forms/developing/rendering-forms-rendering-forms preming-forms-flowable-layouts-premilting.md#preming-forms-with-flowable-layouts)。
   * 存 `PDFFormRenderSpec` 儲在客戶端上渲染表單所需運行時選項的對象。
   * 包 `URLSpec` 含Forms服務所需URI值的對象。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空對象。 此參數用於儲存轉譯的PDF表單。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空對象。 （此引數將儲存表單中的頁數）。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空對象。 （此引數將儲存地區值）。
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

**另請參閱**

[在用戶端轉換表單](#rendering-forms-at-the-client)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
