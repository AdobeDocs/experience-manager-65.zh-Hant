---
title: 呈現已啟用權限的Forms
seo-title: Rendering Rights-Enabled Forms
description: 使用Forms服務來轉譯已套用使用權限的表單。 您可以使用Java API和網站服務API來轉譯已啟用權限的表單。
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

# 呈現已啟用權限的Forms {#rendering-rights-enabled-forms}

Forms服務可轉譯套用使用權限的表單。 使用權限屬於Acrobat預設提供但Adobe Reader未提供的功能，例如可向表單新增註解，或填寫表單欄位並儲存表單。 套用使用權限的Forms稱為已啟用權限的表單。 在Adobe Reader中開啟已啟用權限的表單的使用者可以執行針對該表單啟用的操作。

若要將使用權套用至表單，Acrobat Reader DC擴充功能服務必須是AEM表單安裝程式的一部分。 此外，您必須具有有效的憑據，以便對PDF文檔應用使用權限。 也就是說，您必須正確設定Acrobat Reader DC擴充功能服務，才能轉譯已啟用權限的表單。 (請參閱 [關於Acrobat Reader DC擴充功能服務](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>若要呈現包含使用權限的表單，您必須使用XDP檔案作為輸入，而非PDF檔案。 如果您使用PDF檔案作為輸入，表單仍會呈現；不過，它不會是啟用權限的表單。

>[!NOTE]
>
>指定下列使用權限時，無法將XML資料預填入表單： `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`，或 `enableDigitalSignatures`. (請參閱 [使用可流式配置預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步驟摘要 {#summary-of-steps}

要呈現啟用權限的表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定使用權運行時間選項。
1. 轉譯已啟用權限的表單。
1. 將已啟用權限的表單寫入客戶端Web瀏覽器。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API作業。

**設定使用權運行時間選項**

您必須設定使用權限運行時選項，才能呈現已啟用權限的表單。 您還必須指定用於將使用權應用於表單的憑據的別名。 指定別名值後，您可以指定每個使用方式以套用至表單。

**轉譯已啟用權限的表單**

若要呈現已啟用權限的表單，您使用的應用程式邏輯與呈現沒有使用權限的表單相同。 唯一的差異是您必須確保應用程式邏輯中包含使用權限執行時間選項。

>[!NOTE]
>
>使用Forms網站服務API轉譯已啟用權限的表單時，您無法將檔案附加至表單。

**將表單資料流寫入客戶端Web瀏覽器**

Forms服務轉譯已啟用權限的表單時，會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 寫入客戶端Web瀏覽器後，用戶將看到該表單。 在Adobe Reader中檢視已啟用權限的表單的使用者，可以執行針對該表單啟用的操作。

**另請參閱**

[使用Java API呈現已啟用權限的表單](#render-rights-enabled-forms-using-the-java-api)

[使用網站服務API呈現已啟用權限的表單](#render-rights-enabled-forms-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉譯互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立可轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API呈現已啟用權限的表單 {#render-rights-enabled-forms-using-the-java-api}

使用Forms API(Java)轉譯已啟用權限的表單：

1. 包含項目檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormsServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 設定使用權運行時間選項

   * 建立 `ReaderExtensionSpec` 物件，使用其建構子。
   * 通過調用 `ReaderExtensionSpec` 物件 `setReCredentialAlias` 方法，並指定代表別名值的字串值。
   * 通過調用屬於的相應方法來設定每個使用權 `ReaderExtensionSpec` 物件。 但是，只有當引用的憑據允許您設定使用權限時，才可以設定使用權限。 也就是說，如果憑據不允許設定，則無法設定使用權。 例如。 若要設定使用權限，讓使用者能夠填寫表單欄位並儲存表單，請叫用 `ReaderExtensionSpec` 物件 `setReFillIn` 方法和傳遞 `true`.

   >[!NOTE]
   >
   >不需要叫用 `ReaderExtensionSpec` 物件 `setReCredentialPassword` 方法。 Forms服務不會使用此方法。

1. 轉譯已啟用權限的表單

   叫用 `FormsServiceClient` 物件 `renderPDFFormWithUsageRights` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要與表單合併資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。
   * A `ReaderExtensionSpec` 儲存使用權運行時選項的對象。
   * A `URLSpec` 包含Forms服務所需URI值的物件。

   此 `renderPDFFormWithUsageRights` 方法傳回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `com.adobe.idp.Document` 對象，方法是調用 `FormsResult` 物件s `getOutputContent` 方法。
   * 取得 `com.adobe.idp.Document` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 對象，方法是調用 `com.adobe.idp.Document` 物件 `getInputStream` 方法。
   * 叫用 `InputStream` 物件 `read` 方法，並將位元組陣列傳遞為引數。
   * 叫用 `javax.servlet.ServletOutputStream` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API轉譯已啟用權限的表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API呈現已啟用權限的表單 {#render-rights-enabled-forms-using-the-web-service-api}

使用Forms API（網站服務）轉譯已啟用權限的表單：

1. 包含項目檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立 `FormsService` 對象和設定驗證值。

1. 設定使用權運行時間選項

   * 建立 `ReaderExtensionSpec` 物件，使用其建構子。
   * 通過調用 `ReaderExtensionSpec` 物件 `setReCredentialAlias` 方法，並指定代表別名值的字串值。
   * 通過調用屬於的相應方法來設定每個使用權 `ReaderExtensionSpec` 物件。 但是，只有當引用的憑據允許您設定使用權限時，才可以設定使用權限。 也就是說，如果憑據不允許設定，則無法設定使用權。 若要設定使用權限，讓使用者能夠填寫表單欄位並儲存表單，請叫用 `ReaderExtensionSpec` 物件 `setReFillIn` 方法和傳遞 `true`.

1. 轉譯已啟用權限的表單

   叫用 `FormsService` 物件 `renderPDFFormWithUsageRights` 方法，並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案名副檔名。 如果您參考屬於Forms應用程式一部分的表單設計，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要與表單合併資料的物件。 如果您不想合併表單中的資料，必須傳遞 `BLOB` 基於空XML資料源的對象。 您無法傳遞 `BLOB` 為null的對象；否則，會擲回例外。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。
   * A `ReaderExtensionSpec` 儲存使用權運行時選項的對象。
   * A `URLSpec` 包含Forms服務所需URI值的物件。

   此 `renderPDFFormWithUsageRights` 方法傳回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 將表單資料流寫入客戶端Web瀏覽器

   * 建立 `BLOB` 包含表單資料的物件，方法是叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得 `BLOB` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立位元組陣列，並叫用 `BLOB` 物件 `getBinaryData` 方法。 此任務分配 `FormsResult` 位元組陣列的物件。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[呈現已啟用權限的Forms](#rendering-rights-enabled-forms)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
