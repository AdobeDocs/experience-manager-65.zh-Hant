---
title: 啟用版權的呈現Forms
seo-title: Rendering Rights-Enabled Forms
description: 使用Forms服務可呈現對其應用了使用權限的表單。 可以使用Java API和Web服務API呈現啟用權限的表單。
seo-description: Use the Forms service to render forms that have usage rights applied to them. You can render rights-enabled forms using the Java API and Web Service API.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 0%

---

# 啟用版權的呈現Forms {#rendering-rights-enabled-forms}

Forms服務可以呈現具有應用其使用權限的表單。 使用權限與預設在Acrobat但在Adobe Reader不可用的功能有關，例如向表單添加註釋或填寫表單域並保存表單的功能。 對其應用了使用權限的Forms稱為啟用權限的表單。 在Adobe Reader開啟啟用了權限的表單的用戶可以執行為該表單啟用的操作。

為了對表單應用使用權限，Acrobat Reader DC擴展服務必須是您表單安裝的AEM一部分。 此外，您必須具有有效的憑據，以便將使用權限應用於PDF文檔。 也就是說，必須正確配置Acrobat Reader DC擴展服務，才能呈現啟用權限的表單。 (請參閱 [關於Acrobat Reader DC分機服務](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)。)

>[!NOTE]
>
>要呈現包含使用權限的表單，必須使用XDP檔案作為輸入，而不是PDF檔案。 如果使用PDF檔案作為輸入，則表單仍呈現；但是，它不是啟用權限的表單。

>[!NOTE]
>
>指定以下使用權限時，不能用XML資料預填充表單： `enableComments`。 `enableCommentsOnline`。 `enableEmbeddedFiles`或 `enableDigitalSignatures`。 (請參閱 [用可流式佈局預填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要呈現啟用權限的表單，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms客戶端API對象。
1. 設定使用權限運行時選項。
1. 呈現啟用權限的窗體。
1. 將啟用權限的表單寫入客戶端Web瀏覽器。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Forms客戶端API對象**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立Forms服務客戶端。

**設定使用權限運行時選項**

必須設定使用權限運行時選項以呈現啟用權限的表單。 您還必須指定用於將使用權限應用於表單的憑據的別名。 指定別名值後，指定每個用法權限以應用於表單。

**呈現啟用權限的窗體**

要呈現啟用權限的表單，請使用與呈現沒有使用權限的表單相同的應用程式邏輯。 唯一的區別是必須確保應用程式邏輯中包含使用權限運行時選項。

>[!NOTE]
>
>使用FormsWeb服務API呈現啟用權限的表單時，不能將檔案附加到表單。

**將表單資料流寫入客戶端Web瀏覽器**

當Forms服務呈現啟用權限的表單時，它將返回必須寫入客戶端Web瀏覽器的表單資料流。 一旦寫入到客戶端Web瀏覽器，用戶就可以看到表單。 在Adobe Reader查看啟用權限的表單的用戶能夠執行為該表單啟用的操作。

**另請參閱**

[使用Java API呈現啟用權限的表單](#render-rights-enabled-forms-using-the-java-api)

[使用Web服務API呈現啟用權限的表單](#render-rights-enabled-forms-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立呈現Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API呈現啟用權限的表單 {#render-rights-enabled-forms-using-the-java-api}

使用FormsAPI(Java)呈現啟用權限的表單：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。

1. 建立Forms客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定使用權限運行時選項

   * 建立 `ReaderExtensionSpec` 對象。
   * 通過調用 `ReaderExtensionSpec` 對象 `setReCredentialAlias` 方法並指定表示別名值的字串值。
   * 通過調用屬於 `ReaderExtensionSpec` 的雙曲餘切值。 但是，只有在引用的憑據允許您設定使用權限時，才能設定使用權限。 也就是說，如果憑據不允許設定使用權限，則不能設定使用權限。 比如說， 要設定使用戶能夠填寫表單域並保存表單的使用權限，請調用 `ReaderExtensionSpec` 對象 `setReFillIn` 方法 `true`。

   >[!NOTE]
   >
   >不必調用 `ReaderExtensionSpec` 對象 `setReCredentialPassword` 的雙曲餘切值。 Forms服務未使用此方法。

1. 呈現啟用權限的窗體

   調用 `FormsServiceClient` 對象 `renderPDFFormWithUsageRights` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `com.adobe.idp.Document` 的雙曲餘切值。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。
   * A `ReaderExtensionSpec` 儲存使用權限運行時選項的對象。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。

   的 `renderPDFFormWithUsageRights` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `com.adobe.idp.Document` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read` 方法，並將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API呈現啟用權限的表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API呈現啟用權限的表單 {#render-rights-enabled-forms-using-the-web-service-api}

使用FormsAPI（Web服務）呈現啟用權限的表單：

1. 包括項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包括到類路徑中。

1. 建立Forms客戶端API對象

   建立 `FormsService` 對象和設定驗證值。

1. 設定使用權限運行時選項

   * 建立 `ReaderExtensionSpec` 對象。
   * 通過調用 `ReaderExtensionSpec` 對象 `setReCredentialAlias` 方法並指定表示別名值的字串值。
   * 通過調用屬於 `ReaderExtensionSpec` 的雙曲餘切值。 但是，只有在引用的憑據允許您設定使用權限時，才能設定使用權限。 也就是說，如果憑據不允許設定使用權限，則不能設定使用權限。 要設定使用戶能夠填寫表單域並保存表單的使用權限，請調用 `ReaderExtensionSpec` 對象 `setReFillIn` 方法 `true`。

1. 呈現啟用權限的窗體

   調用 `FormsService` 對象 `renderPDFFormWithUsageRights` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。 如果引用屬於Forms應用程式的表單設計，請確保指定完整路徑，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * A `BLOB` 包含要與窗體合併的資料的對象。 如果不想將資料與表單合併，則必須傳遞 `BLOB` 基於空XML資料源的對象。 無法通過 `BLOB` 空的對象；否則，將引發異常。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。
   * A `ReaderExtensionSpec` 儲存使用權限運行時選項的對象。
   * A `URLSpec` 包含Forms服務所需的URI值的對象。

   的 `renderPDFFormWithUsageRights` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `BLOB` 通過調用包含表單資料的對象 `FormsResult` 對象 `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `BLOB` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `BLOB` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立位元組陣列，並通過調用 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。 此任務分配 `FormsResult` 對象。
   * 調用 `javax.servlet.http.HttpServletResponse` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[啟用版權的呈現Forms](#rendering-rights-enabled-forms)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
