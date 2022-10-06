---
title: 在用戶端呈現Forms
seo-title: Rendering Forms at the Client
description: 使用Acrobat或Adobe Reader的用戶端轉譯功能，最佳化PDF內容的傳送，並改善Forms服務處理網路負載的能力
seo-description: Optimize the delivery of PDF content and improve the Forms service’s ability to handle network load by using the client-side rendering capability of Acrobat or Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 0%

---

# 在用戶端呈現Forms {#rendering-forms-at-the-client}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 在用戶端呈現Forms {#rendering-forms-at-the-client-inner}

您可以使用Acrobat或Adobe Reader的用戶端轉譯功能，最佳化PDF內容的傳送，並改善Forms服務處理網路負載的能力。 此程式稱為在用戶端轉譯表單。 若要在用戶端上轉譯表單，用戶端裝置（通常為網頁瀏覽器）必須使用Acrobat 7.0或Adobe Reader 7.0或更新版本。

因伺服器端指令碼執行而產生的表單變更不會反映在用戶端上呈現的表單中，除非根子表單包含 `restoreState` 屬性 `auto`. 如需此屬性的詳細資訊，請參閱 [Forms設計師。](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要在客戶端上呈現表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定客戶端呈現運行時選項。
1. 在用戶端轉譯表單。
1. 將表單寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API作業。 如果您使用Java API，請建立 `FormsServiceClient` 物件。 如果您使用Forms網站服務API，請建立 `FormsService` 物件。

**設定客戶端呈現運行時選項**

您必須設定客戶端呈現運行時選項，以便通過設定 `RenderAtClient` 運行時選項 `true`. 這會導致表單傳送至呈現該表單的用戶端裝置。 若 `RenderAtClient` is `auto` （預設值），表單設計會決定表單是否在用戶端呈現。 表單設計必須是具有可流動版面的表單設計。

您可設定的選用執行時選項為 `SeedPDF` 選項。 此 `SeedPDF` 選項會結合PDF容器(種子PDF檔案)與表單設計和XML資料。 表單設計和XML資料都會傳送至Acrobat或Adobe Reader，以便轉譯表單。 此 `SeedPDF` 當客戶端電腦沒有窗體中使用的字型時，可以使用選項，例如當最終用戶未獲許可使用窗體所有者有權使用的字型時。

您可以使用Designer建立簡單的動態PDF檔案，以用作種子PDF檔案。 執行此任務需要下列步驟：

1. 確定是否需要在種子PDF檔案中嵌入任何字型。 種子PDF檔案需要包含要呈現的表單所需的其他字型。 將字型嵌入種子PDF檔案時，請確保您未違反任何字型許可協定。 在Designer中，您可以確定是否可以合法嵌入字型。 保存時，如果有無法嵌入到表單中的字型，Designer將顯示一條消息，列出不能嵌入的字型。 靜態PDF文檔的設計器中不顯示此消息。
1. 如果要在Designer中建立種子PDF檔案，建議至少添加包含消息的文本欄位。 訊息應針對舊版Adobe Reader的使用者，指出他們需要Acrobat 7.0或更新版本或Adobe Reader 7.0或更新版本才能檢視檔案。
1. 將種子PDF檔案儲存為動態PDF檔案，副檔名為PDF檔案。

>[!NOTE]
>
>您不需要定義種子PDF運行時選項，即可在客戶端上呈現表單。 如果您未指定種子PDF,Forms服務會建立殼層pdf，此pdf將不包含COS物件，但將包含內嵌實際XDP內容的PDF包裝函式。 本節中的步驟不設定種子PDF運行時選項。 有關COS對象的資訊，請參閱Adobe PDF參考指南。

**在用戶端轉譯表單**

若要在用戶端轉譯表單，您必須確保在應用程式邏輯中包含用戶端轉譯執行階段選項，才能轉譯表單。

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務會建立您必須寫入用戶端網頁瀏覽器的表單資料流。 將表單寫入用戶端網頁瀏覽器時，表單會由Acrobat 7.0或Adobe Reader 7.0或更新版本轉譯，且使用者可看見。

**另請參閱**

[使用Java API在用戶端轉譯表單](#render-a-form-at-the-client-using-the-java-api)

[使用網站服務API在用戶端轉譯表單](#render-a-form-at-the-client-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API在用戶端轉譯表單 {#render-a-form-at-the-client-using-the-java-api}

使用Forms API(Java)在用戶端轉譯表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 設定客戶端呈現運行時選項

   * 建立 `PDFFormRenderSpec` 物件，使用其建構子。
   * 設定 `RenderAtClient` 執行時間選項，方法是叫用 `PDFFormRenderSpec` 物件 `setRenderAtClient` 方法並傳遞列舉值 `RenderAtClient.Yes`.

1. 在用戶端轉譯表單

   叫用 `FormsServiceClient` 物件 `renderPDFForm` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於AEM Forms應用程式一部分的表單設計，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要與表單合併資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * A `PDFFormRenderSpec` 用於儲存在客戶端呈現表單所需的運行時選項的對象。
   * A `URLSpec` 包含Forms服務轉譯表單所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 對象，方法是調用 `FormsResult` 物件s `getOutputContent` 方法。
   * 取得 `com.adobe.idp.Document` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 對象，方法是調用 `com.adobe.idp.Document` 物件 `getInputStream` 方法。
   * 建立位元組陣列，並叫用 `InputStream` 物件 `read` 方法，並將位元組陣列傳遞為引數。
   * 叫用 `javax.servlet.ServletOutputStream` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API在用戶端轉譯表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API在用戶端轉譯表單 {#render-a-form-at-the-client-using-the-web-service-api}

使用Forms API（網站服務）在用戶端轉譯表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立 `FormsService` 對象和設定驗證值。

1. 設定客戶端呈現運行時選項

   * 建立 `PDFFormRenderSpec` 物件，使用其建構子。
   * 設定 `RenderAtClient` 執行時間選項，方法是叫用 `PDFFormRenderSpec` 物件 `setRenderAtClient` 方法和傳遞字串值 `RenderAtClient.Yes`.

1. 在用戶端轉譯表單

   叫用 `FormsService` 物件 `renderPDFForm` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要與表單合併資料的物件。 如果您不想合併資料，請傳遞 `null`. (請參閱 [使用可流式配置預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` 用於儲存在客戶端呈現表單所需的運行時選項的對象。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 這是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 由方法填入的物件。 此參數用於儲存已呈現的PDF表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 由方法填入的物件。 （此引數會以表單儲存頁數）。
   * 空白 `javax.xml.rpc.holders.StringHolder` 由方法填入的物件。 （此參數將儲存區域設定值）。
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作結果的對象。

   此 `renderPDFForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 作為最後一個引數值傳遞的物件，具有必須寫入用戶端網頁瀏覽器的表單資料流。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件 `value` 資料成員。
   * 建立 `BLOB` 包含表單資料的物件，方法是叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得 `BLOB` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立位元組陣列，並叫用 `BLOB` 物件 `getBinaryData` 方法。 此任務分配 `FormsResult` 位元組陣列的物件。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[在用戶端呈現Forms](#rendering-forms-at-the-client)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
