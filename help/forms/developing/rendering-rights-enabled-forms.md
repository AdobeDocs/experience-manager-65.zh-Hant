---
title: 轉換具權限的表單
seo-title: 轉換具權限的表單
description: 'null'
seo-description: 'null'
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 轉換具權限的表單 {#rendering-rights-enabled-forms}

Forms服務可以呈現已套用使用權限的表單。 使用權限與Acrobat預設為Acrobat但Adobe reader未提供的功能相關，例如在表格中新增註解或填寫表格欄位並儲存表格的功能。 具有套用使用權限的表單稱為啟用權限的表單。 在Adobe Reader中開啟具權限的表格的使用者，可以執行為該表格啟用的作業。

若要將使用權套用至表單，Acrobat Reader DC擴充功能服務必須是AEM表單安裝的一部分。 此外，您必須擁有有效的憑證，才能將使用權套用至PDF檔案。 也就是說，您必須先正確設定Acrobat Reader DC擴充功能服務，才能轉換具權限的表格。 (請參 [閱關於Acrobat Reader DC擴充功能服務](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service))。

>[!NOTE]
>
>若要轉換包含使用權限的表單，您必須使用XDP檔案做為輸入，而非PDF檔案。 如果您使用PDF檔案作為輸入，表單仍會轉譯；但是，它不是啟用權限的表格。

>[!NOTE]
>
>當您指定下列使用權限時，無法預先填入XML資料的表格： `enableComments`、 `enableCommentsOnline``enableEmbeddedFiles`或 `enableDigitalSignatures`。 (請參 [閱使用可排程版面預填表單](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要呈現啟用權限的表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定使用權限執行時期選項。
1. 轉譯啟用權限的表單。
1. 將啟用權限的表單寫入客戶端Web瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

您必須先建立Forms服務用戶端，才能以程式設計方式執行Forms服務用戶端API操作。

**設定使用權限運行時選項**

您必須設定使用權限執行時期選項，才能產生啟用權限的表單。 您還必須指定用於對表單應用使用權限的憑據別名。 指定別名值後，您可以直接指定每個用法以套用至表單。

**轉譯啟用權限的表單**

若要轉換具有權限的表格，請使用與轉換沒有使用權限的表格相同的應用程式邏輯。 唯一的區別是，您必須確保應用程式邏輯中包含使用權限執行時間選項。

>[!NOTE]
>
>使用Forms web service API轉換具有權限的表格時，您無法將檔案附加至表格。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務轉換具有權限的表單時，它會傳回必須寫入用戶端網頁瀏覽器的表單資料流。 一旦寫入到客戶端Web瀏覽器，用戶就可以看到表單。 在Adobe Reader中檢視已啟用權限的表格的使用者，可以執行為該表格啟用的作業。

**另請參閱**

[使用Java API演算啟用權限的表單](#render-rights-enabled-forms-using-the-java-api)

[使用web service API演算具權限的表格](#render-rights-enabled-forms-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉換互動式PDF表單](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯表單的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API演算啟用權限的表單 {#render-rights-enabled-forms-using-the-java-api}

使用Forms API(Java)來轉譯啟用權限的表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定使用權限運行時選項

   * 使用其 `ReaderExtensionSpec` 建構函式建立物件。
   * 調用物件的方法以指定憑證的 `ReaderExtensionSpec` 別名，並 `setReCredentialAlias` 指定代表別名值的字串值。
   * 通過調用屬於對象的相應方法來設定每個使用 `ReaderExtensionSpec` 權。 不過，您只能在您引用的憑證允許您進行設定時，設定正確的使用方式。 也就是說，如果憑據不允許您設定，則不能設定正確的使用情形。 例如。 若要設定使用權，讓使用者可填寫表單欄位並儲存表單、叫用物 `ReaderExtensionSpec` 件的方 `setReFillIn` 法並傳遞 `true`。
   >[!NOTE]
   >
   >您不需要叫用物 `ReaderExtensionSpec` 件的方 `setReCredentialPassword` 法。 Forms服務不會使用此方法。

1. 轉譯啟用權限的表單

   叫用物 `FormsServiceClient` 件的方 `renderPDFFormWithUsageRights` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包 `com.adobe.idp.Document` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞空 `com.adobe.idp.Document` 物件。
   * 存 `PDFFormRenderSpec` 儲運行時選項的對象。
   * 存 `ReaderExtensionSpec` 儲使用權限運行時選項的對象。
   * 包 `URLSpec` 含Forms服務所需URI值的對象。
   該方 `renderPDFFormWithUsageRights` 法返回包 `FormsResult` 含必須寫入客戶端Web瀏覽器的表單資料流的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調 `com.adobe.idp.Document` 用對象的方法 `FormsResult` 建立對 `getOutputContent` 像。
   * 通過調用對象的方 `com.adobe.idp.Document` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `com.adobe.idp.Document` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 調用 `java.io.InputStream` 物件的方 `com.adobe.idp.Document` 法以建立物 `getInputStream` 件。
   * 呼叫物件的方法，並將位元組陣列傳 `InputStream` 入為引數， `read` 以表格資料流的方式建立位元組陣列。
   * 叫用物 `javax.servlet.ServletOutputStream` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API轉譯具權限的表格](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API演算具權限的表格 {#render-rights-enabled-forms-using-the-web-service-api}

使用Forms API(web service)來轉譯具有權限的表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立對 `FormsService` 像並設定驗證值。

1. 設定使用權限運行時選項

   * 使用其 `ReaderExtensionSpec` 建構函式建立物件。
   * 調用物件的方法以指定憑證的 `ReaderExtensionSpec` 別名，並 `setReCredentialAlias` 指定代表別名值的字串值。
   * 通過調用屬於對象的相應方法來設定每個使用 `ReaderExtensionSpec` 權。 不過，您只能在您引用的憑證允許您進行設定時，設定正確的使用方式。 也就是說，如果憑據不允許您設定，則不能設定正確的使用情形。 若要設定使用權，讓使用者可填寫表格欄位並儲存表格，請叫用物 `ReaderExtensionSpec` 件的方 `setReFillIn` 法並傳遞 `true`。

1. 轉譯啟用權限的表單

   叫用物 `FormsService` 件的方 `renderPDFFormWithUsageRights` 法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參照屬於Forms應用程式一部分的表單設計，請確定您指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包 `BLOB` 含要與表單合併的資料的對象。 如果您不想將資料與表單合併，則必須傳遞以空 `BLOB` 白XML資料來源為基礎的物件。 不能傳遞 `BLOB` 空的對象；否則，會拋出異常。
   * 存 `PDFFormRenderSpec` 儲運行時選項的對象。
   * 存 `ReaderExtensionSpec` 儲使用權限運行時選項的對象。
   * 包 `URLSpec` 含Forms服務所需URI值的對象。
   該方 `renderPDFFormWithUsageRights` 法返回包 `FormsResult` 含必須寫入客戶端Web瀏覽器的表單資料流的對象。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 呼叫 `BLOB` 物件的方法，以建立包含表 `FormsResult` 單資料的物 `getOutputContent` 件。
   * 通過調用對象的方 `BLOB` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `BLOB` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 建立位元組陣列，並透過叫用物件的方 `BLOB` 法來填入該 `getBinaryData` 陣列。 此任務將對象的內 `FormsResult` 容分配給位元組陣列。
   * 叫用物 `javax.servlet.http.HttpServletResponse` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[轉換具權限的表單](#rendering-rights-enabled-forms)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
