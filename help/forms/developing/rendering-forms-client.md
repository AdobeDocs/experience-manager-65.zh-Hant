---
title: 在客戶端呈現Forms
seo-title: Rendering Forms at the Client
description: 優化PDF內容的交付，通過使用Acrobat或Adobe Reader的客戶端渲染能力提高Forms服務處理網路負載的能力
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

# 在客戶端呈現Forms {#rendering-forms-at-the-client}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 在客戶端呈現Forms {#rendering-forms-at-the-client-inner}

您可以通過使用Acrobat或Adobe Reader的客戶端渲染功能來優化PDF內容的交付並提高Forms服務處理網路負載的能力。 此過程稱為在客戶端呈現表單。 要在客戶端上呈現表單，客戶端設備（通常為Web瀏覽器）必須使用Acrobat 7.0或Adobe Reader7.0或更高版本。

伺服器端指令碼執行對表單所做的更改不會反映在在客戶端呈現的表單中，除非根子表單包含 `restoreState` 設定為的屬性 `auto`。 有關此屬性的詳細資訊，請參見 [Forms設計師。](https://www.adobe.com/go/learn_aemforms_designer_63_tw)

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要在客戶端上呈現表單，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms客戶端API對象。
1. 設定客戶端呈現運行時選項。
1. 在客戶端上呈現表單。
1. 將表單寫入客戶端Web瀏覽器。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms客戶端API對象**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立Forms服務客戶端。 如果使用Java API，請建立 `FormsServiceClient` 的雙曲餘切值。 如果使用FormsWeb服務API，請建立 `FormsService` 的雙曲餘切值。

**設定客戶端呈現運行時選項**

必須設定客戶端呈現運行時選項，以通過設定 `RenderAtClient` 運行時選項到 `true`。 這將導致表單被傳送到呈現它的客戶端設備。 如果 `RenderAtClient` 是 `auto` （預設值），表單設計將確定是否在客戶端上呈現表單。 表單設計必須是具有可流動層的表單設計。

您可以設定的可選運行時選項是 `SeedPDF` 的雙曲餘切值。 的 `SeedPDF` 選項將PDF容器(種子PDF文檔)與窗體設計和XML資料組合在一起。 表單設計和XML資料都被傳送到Acrobat或Adobe Reader，在那裡呈現表單。 的 `SeedPDF` 當客戶端電腦沒有表單中使用的字型時，可以使用該選項，例如當最終用戶未獲得使用表單所有者授權使用的字型的許可時。

可以使用設計器建立簡單的動態PDF檔案，以用作種子PDF檔案。 執行此任務需要執行以下步驟：

1. 確定是否需要在種子PDF檔案中嵌入任何字型。 種子PDF檔案需要包含要呈現的表單所需的附加字型。 將字型嵌入到種子PDF檔案時，確保不違反任何字型許可協定。 在設計器中，您可以確定是否可以合法嵌入字型。 保存時，如果有無法嵌入到表單中的字型，Designer將顯示一條消息，列出您不能嵌入的字型。 靜態PDF文檔的設計器中不顯示此消息。
1. 如果在設計器中建立種子PDF檔案，建議至少添加包含消息的文本欄位。 該消息應針對Adobe Reader早期版本的用戶，這些用戶聲明他們需要Acrobat 7.0或更高版本或Adobe Reader7.0或更高版本才能查看該文檔。
1. 將種子PDF檔案另存為具有PDF檔案副檔名的動態PDF檔案。

>[!NOTE]
>
>您不需要定義種子PDF運行時選項來在客戶端上呈現表單。 如果未指定種子PDF，則Forms服務將建立一個shell pdf，該pdf將不包含COS對象，但將包含一個PDF包裝，其中嵌入了實際的XDP內容。 本節中的步驟未設定種子PDF運行時選項。 有關COS對象的資訊，請參閱《Adobe PDF參考指南》。

**在客戶端上呈現表單**

要在客戶端上呈現表單，必須確保在應用程式邏輯中包含客戶端呈現運行時選項以呈現表單。

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務會建立必須寫入客戶端Web瀏覽器的表單資料流。 當寫入客戶端Web瀏覽器時，表單由Acrobat 7.0或Adobe Reader7.0或更高版本呈現，並且對用戶可見。

**另請參閱**

[使用Java API在客戶端呈現表單](#render-a-form-at-the-client-using-the-java-api)

[使用Web服務API在客戶端上呈現表單](#render-a-form-at-the-client-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案轉給Forms](/help/forms/developing/passing-documents-forms-service.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API在客戶端呈現表單 {#render-a-form-at-the-client-using-the-java-api}

使用FormsAPI(Java)在客戶端呈現表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立Forms客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定客戶端呈現運行時選項

   * 建立 `PDFFormRenderSpec` 對象。
   * 設定 `RenderAtClient` 通過調用運行時選項 `PDFFormRenderSpec` 對象 `setRenderAtClient` 方法和傳遞枚舉值 `RenderAtClient.Yes`。

1. 在客戶端上呈現表單

   調用 `FormsServiceClient` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於AEM Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `com.adobe.idp.Document` 的雙曲餘切值。
   * A `PDFFormRenderSpec` 儲存在客戶端呈現表單所需的運行時選項的對象。
   * A `URLSpec` 包含Forms服務呈現表單所需的URI值的對象。
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

**另請參閱**

[快速啟動（SOAP模式）:使用Java API在客戶端呈現表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API在客戶端上呈現表單 {#render-a-form-at-the-client-using-the-web-service-api}

使用FormsAPI（Web服務）在客戶端上呈現表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包括到類路徑中。

1. 建立Forms客戶端API對象

   建立 `FormsService` 對象和設定驗證值。

1. 設定客戶端呈現運行時選項

   * 建立 `PDFFormRenderSpec` 對象。
   * 設定 `RenderAtClient` 通過調用運行時選項 `PDFFormRenderSpec` 對象 `setRenderAtClient` 方法和傳遞字串值 `RenderAtClient.Yes`。

1. 在客戶端上呈現表單

   調用 `FormsService` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `BLOB` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞 `null`。 (請參閱 [用可流式佈局預填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
   * A `PDFFormRenderSpec` 儲存在客戶端呈現表單所需的運行時選項的對象。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的對象。 此參數用於儲存渲染的PDF窗體。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的對象。 （此參數將儲存表單中的頁數）。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的對象。 （此參數將儲存區域設定值）。
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

**另請參閱**

[在客戶端呈現Forms](#rendering-forms-at-the-client)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
