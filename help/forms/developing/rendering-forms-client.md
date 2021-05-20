---
title: 在用戶端呈現Forms
seo-title: 在用戶端呈現Forms
description: 使用Acrobat或Adobe Reader的用戶端轉譯功能，最佳化PDF內容的傳送，並改善Forms服務處理網路負載的能力
seo-description: 使用Acrobat或Adobe Reader的用戶端轉譯功能，最佳化PDF內容的傳送，並改善Forms服務處理網路負載的能力
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
source-wordcount: '1730'
ht-degree: 0%

---

# 在用戶端{#rendering-forms-at-the-client}呈現Forms

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 在用戶端{#rendering-forms-at-the-client-inner}呈現Forms

您可以使用Acrobat或Adobe Reader的用戶端轉譯功能，最佳化PDF內容的傳送，並改善Forms服務處理網路負載的能力。 此程式稱為在用戶端轉譯表單。 若要在用戶端上轉譯表單，用戶端裝置（通常為網頁瀏覽器）必須使用Acrobat 7.0或Adobe Reader 7.0或更新版本。

伺服器端指令碼執行所產生的表單變更不會反映在用戶端上呈現的表單中，除非根子表單包含設為`auto`的`restoreState`屬性。 有關此屬性的詳細資訊，請參閱[Forms Designer。](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}的摘要

要在客戶端上呈現表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定客戶端呈現運行時選項。
1. 在用戶端轉譯表單。
1. 將表單寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API作業。 如果您使用Java API，請建立`FormsServiceClient`物件。 如果您使用Forms Web服務API，請建立`FormsService`物件。

**設定客戶端呈現運行時選項**

您必須將`RenderAtClient`運行時選項設定為`true`，以設定客戶端呈現運行時選項以在客戶端呈現表單。 這會導致表單傳送至呈現該表單的用戶端裝置。 如果`RenderAtClient`為`auto`（預設值），則表單設計將確定表單是否在客戶端呈現。 表單設計必須是具有可流動版面的表單設計。

您可以設定的可選運行時選項是`SeedPDF`選項。 `SeedPDF`選項將PDF容器（種子PDF文檔）與表單設計和XML資料結合。 表單設計和XML資料都會傳送至Acrobat或Adobe Reader，以便轉譯表單。 當客戶端電腦中沒有使用的字型時（例如，當最終用戶未獲許可使用表單所有者授權使用的字型時），可使用`SeedPDF`選項。

您可以使用Designer建立簡單的動態PDF檔案，以用作種子PDF檔案。 執行此任務需要下列步驟：

1. 確定是否需要在種子PDF檔案中嵌入任何字型。 種子PDF檔案需要包含要呈現的表單所需的其他字型。 將字型嵌入種子PDF檔案時，請確保您未違反任何字型授權協定。 在Designer中，您可以確定是否可以合法嵌入字型。 保存時，如果有無法嵌入到表單中的字型，Designer將顯示一條消息，列出不能嵌入的字型。 對於靜態PDF文檔，Designer中不顯示此消息。
1. 如果要在Designer中建立種子PDF檔案，建議至少添加包含消息的文本欄位。 訊息應針對舊版Adobe Reader的使用者，指出他們需要Acrobat 7.0或更新版本或Adobe Reader 7.0或更新版本才能檢視檔案。
1. 將種子PDF檔案儲存為動態PDF檔案，副檔名為PDF。

>[!NOTE]
>
>您不需要定義種子PDF運行時選項，即可在用戶端上呈現表單。 如果您未指定種子PDF,Forms服務會建立殼層PDF，該殼層PDF將不包含COS物件，但將包含內嵌實際XDP內容的PDF包裝函式。 本節中的步驟不設定種子PDF運行時選項。 有關COS對象的資訊，請參閱Adobe PDF參考指南。

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

### 使用Java API {#render-a-form-at-the-client-using-the-java-api}在用戶端轉譯表單

使用Forms API(Java)在用戶端轉譯表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormsServiceClient`物件。

1. 設定客戶端呈現運行時選項

   * 使用其建構子建立`PDFFormRenderSpec`物件。
   * 叫用`PDFFormRenderSpec`物件的`setRenderAtClient`方法並傳遞列舉值`RenderAtClient.Yes`，以設定`RenderAtClient`執行時間選項。

1. 在用戶端轉譯表單

   調用`FormsServiceClient`對象的`renderPDFForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於AEM Forms應用程式一部分的表單設計，請務必指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * `PDFFormRenderSpec`物件，儲存在用戶端轉譯表單所需的執行階段選項。
   * `URLSpec`物件，包含Forms服務演算表單所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。

   `renderPDFForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 調用`FormsResult`對象s `getOutputContent`方法，建立`com.adobe.idp.Document`對象。
   * 調用`getContentType`方法，獲取`com.adobe.idp.Document`對象的內容類型。
   * 通過調用`setContentType`方法並傳遞`com.adobe.idp.Document`對象的內容類型來設定`javax.servlet.http.HttpServletResponse`對象的內容類型。
   * 通過調用`javax.servlet.http.HttpServletResponse`對象的`getOutputStream`方法，建立用於將表單資料流寫入客戶端Web瀏覽器的`javax.servlet.ServletOutputStream`對象。
   * 調用`com.adobe.idp.Document`對象的`getInputStream`方法，建立`java.io.InputStream`對象。
   * 叫用`InputStream`物件的`read`方法，並將位元組陣列傳遞為引數，借此建立位元組陣列，並填入表單資料流。
   * 調用`javax.servlet.ServletOutputStream`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API在用戶端轉譯表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#render-a-form-at-the-client-using-the-web-service-api}在客戶端上呈現表單

使用Forms API（網站服務）在用戶端轉譯表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`物件並設定驗證值。

1. 設定客戶端呈現運行時選項

   * 使用其建構子建立`PDFFormRenderSpec`物件。
   * 調用`PDFFormRenderSpec`物件的`setRenderAtClient`方法並傳遞字串值`RenderAtClient.Yes`，以設定`RenderAtClient`執行時間選項。

1. 在用戶端轉譯表單

   調用`FormsService`對象的`renderPDFForm`方法並傳遞以下值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞`null`。 (請參閱[使用可流動配置預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
   * `PDFFormRenderSpec`物件，儲存在用戶端轉譯表單所需的執行階段選項。
   * `URLSpec`物件，包含Forms服務所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 這是可選參數，如果不想將檔案附加到表單，可以指定`null`。
   * 由方法填入的空`com.adobe.idp.services.holders.BLOBHolder`物件。 此參數用於儲存已呈現的PDF表單。
   * 由方法填入的空`javax.xml.rpc.holders.LongHolder`物件。 （此引數會以表單儲存頁數）。
   * 由方法填入的空`javax.xml.rpc.holders.StringHolder`物件。 （此參數將儲存區域設定值）。
   * 將包含此操作結果的空`com.adobe.idp.services.holders.FormsResultHolder`對象。

   `renderPDFForm`方法會以必須寫入用戶端網頁瀏覽器的表單資料流填入作為最後一個引數值傳遞的`com.adobe.idp.services.holders.FormsResultHolder`物件。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 獲取`com.adobe.idp.services.holders.FormsResultHolder`對象的`value`資料成員的值，以建立`FormResult`對象。
   * 調用`FormsResult`對象的`getOutputContent`方法，建立包含表單資料的`BLOB`對象。
   * 調用`getContentType`方法，獲取`BLOB`對象的內容類型。
   * 通過調用`setContentType`方法並傳遞`BLOB`對象的內容類型來設定`javax.servlet.http.HttpServletResponse`對象的內容類型。
   * 通過調用`javax.servlet.http.HttpServletResponse`對象的`getOutputStream`方法，建立用於將表單資料流寫入客戶端Web瀏覽器的`javax.servlet.ServletOutputStream`對象。
   * 建立位元組陣列，並調用`BLOB`對象的`getBinaryData`方法來填入。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 調用`javax.servlet.http.HttpServletResponse`對象的`write`方法，將表單資料流發送到客戶端Web瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[在用戶端呈現Forms](#rendering-forms-at-the-client)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
