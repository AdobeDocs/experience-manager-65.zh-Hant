---
title: 啟用版權的Forms
seo-title: 啟用版權的Forms
description: 使用Forms服務來轉譯已套用使用權的表單。 您可以使用Java API和Web服務API來轉譯具有權限的表格。
seo-description: 使用Forms服務來轉譯已套用使用權的表單。 您可以使用Java API和Web服務API來轉譯具有權限的表格。
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---


# 啟用版權的Forms{#rendering-rights-enabled-forms}

Forms服務可轉譯具有套用使用權的表單。 使用權限與Acrobat預設在Adobe Reader但不在的功能相關，例如在表單中新增註解或填寫表單欄位並儲存表單的功能。 對其適用使用權限的Forms稱為具有權限的表單。 在Adobe Reader開啟啟用權限的表格的使用者可以執行為該表格啟用的作業。

為了將使用權套用至表格，Acrobat Reader DC擴充功能服務必須是您表格安裝的一AEM部分。 此外，您必須擁有有效的憑證，才能將使用權套用至PDF檔案。 也就是說，您必須先正確設定Acrobat Reader DC擴充功能服務，才能轉換具版權的表格。 (請參閱[關於Acrobat Reader DC擴展服務](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)。)

>[!NOTE]
>
>若要轉換包含使用權限的表單，您必須使用XDP檔案做為輸入，而非PDF檔案。 如果您使用PDF檔案作為輸入，表單仍會轉譯；但是，它不是啟用權限的表格。

>[!NOTE]
>
>當您指定下列使用權限時，無法預先填入XML資料的表格：`enableComments`、`enableCommentsOnline`、`enableEmbeddedFiles`或`enableDigitalSignatures`。 (請參閱[使用可流式版面預填Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md))。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟{#summary-of-steps}摘要

要呈現啟用權限的表單，請執行以下任務：

1. 包含專案檔案。
1. 建立Forms用戶端API物件。
1. 設定使用權限執行時期選項。
1. 轉譯啟用權限的表單。
1. 將啟用權限的表單寫入客戶端Web瀏覽器。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Forms用戶端API物件**

在以寫程式方式執行Forms服務客戶端API操作之前，必須建立Forms服務客戶端。

**設定使用權限運行時選項**

您必須設定使用權限執行時期選項，才能產生啟用權限的表單。 您還必須指定用於對表單應用使用權限的憑據別名。 指定別名值後，您可以直接指定每個用法以套用至表單。

**轉譯啟用權限的表單**

若要轉換具有權限的表格，請使用與轉換沒有使用權限的表格相同的應用程式邏輯。 唯一的區別是，您必須確保應用程式邏輯中包含使用權限執行時間選項。

>[!NOTE]
>
>使用Forms網站服務API轉換具有權限的表格時，您無法將檔案附加至表格。

**將表單資料串流寫入用戶端網頁瀏覽器**

當Forms服務轉換具有權限的表單時，它會傳回您必須寫入用戶端網頁瀏覽器的表單資料流。 一旦寫入到客戶端Web瀏覽器，用戶就可以看到表單。 在Adobe Reader查看具有權限的表單的用戶能夠執行為該表單啟用的操作。

**另請參閱**

[使用Java API演算啟用權限的表單](#render-rights-enabled-forms-using-the-java-api)

[使用web service API演算具權限的表格](#render-rights-enabled-forms-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[轉換互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯Forms的Web應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#render-rights-enabled-forms-using-the-java-api}演算啟用權限的表格

使用FormsAPI(Java)來轉譯啟用權限的表格：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。

1. 設定使用權限運行時選項

   * 使用其建構子建立`ReaderExtensionSpec`對象。
   * 調用`ReaderExtensionSpec`物件的`setReCredentialAlias`方法以指定憑證的別名，並指定代表別名值的字串值。
   * 通過調用屬於`ReaderExtensionSpec`對象的相應方法來設定每個使用權限。 不過，您只能在您引用的憑證允許您進行設定時，設定正確的使用方式。 也就是說，如果憑據不允許您設定，則不能設定正確的使用情形。 例如。 若要設定使用權，讓使用者可填寫表格欄位並儲存表格，請叫用`ReaderExtensionSpec`物件的`setReFillIn`方法並傳遞`true`。

   >[!NOTE]
   >
   >您不需要叫用`ReaderExtensionSpec`物件的`setReCredentialPassword`方法。 Forms服務不使用此方法。

1. 轉譯啟用權限的表單

   叫用`FormsServiceClient`物件的`renderPDFFormWithUsageRights`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參考屬於Forms應用程式的表單設計，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。
   * `ReaderExtensionSpec`物件，可儲存使用權限執行時間選項。
   * `URLSpec`物件，包含Forms服務所需的URI值。

   `renderPDFFormWithUsageRights`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 通過調用`FormsResult`對象「s `getOutputContent`」方法建立`com.adobe.idp.Document`對象。
   * 通過調用`getContentType`方法獲取`com.adobe.idp.Document`對象的內容類型。
   * 調用`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 調用`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 呼叫`InputStream`物件的`read`方法，並將位元組陣列傳入為引數，以填入表單資料流的位元組陣列。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API轉譯具權限的表格](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#render-rights-enabled-forms-using-the-web-service-api}轉譯啟用權限的表單

使用FormsAPI(web service)來轉譯啟用權限的表格：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java代理類。
   * 將Java代理類包含到類路徑中。

1. 建立Forms用戶端API物件

   建立`FormsService`對象並設定驗證值。

1. 設定使用權限運行時選項

   * 使用其建構子建立`ReaderExtensionSpec`對象。
   * 調用`ReaderExtensionSpec`物件的`setReCredentialAlias`方法以指定憑證的別名，並指定代表別名值的字串值。
   * 通過調用屬於`ReaderExtensionSpec`對象的相應方法來設定每個使用權限。 不過，您只能在您引用的憑證允許您進行設定時，設定正確的使用方式。 也就是說，如果憑據不允許您設定，則不能設定正確的使用情形。 若要設定使用權，讓使用者可填寫表格欄位並儲存表格，請叫用`ReaderExtensionSpec`物件的`setReFillIn`方法並傳遞`true`。

1. 轉譯啟用權限的表單

   叫用`FormsService`物件的`renderPDFFormWithUsageRights`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。 如果您參考屬於Forms應用程式的表單設計，請確定您指定完整路徑，例如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想將資料與表單合併，則必須傳遞以空XML資料來源為基礎的`BLOB`物件。 不能傳遞`BLOB`對象為null;否則，會拋出異常。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。
   * `ReaderExtensionSpec`物件，可儲存使用權限執行時間選項。
   * `URLSpec`物件，包含Forms服務所需的URI值。

   `renderPDFFormWithUsageRights`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 將表單資料串流寫入用戶端網頁瀏覽器

   * 呼叫`FormsResult`物件的`getOutputContent`方法，建立包含表單資料的`BLOB`物件。
   * 通過調用`getContentType`方法獲取`BLOB`對象的內容類型。
   * 調用`setContentType`方法並傳遞`BLOB`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 建立位元組陣列，並呼叫`BLOB`物件的`getBinaryData`方法以填入它。 此任務將`FormsResult`對象的內容分配給位元組陣列。
   * 叫用`javax.servlet.http.HttpServletResponse`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**

[啟用版權的Forms](#rendering-rights-enabled-forms)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
