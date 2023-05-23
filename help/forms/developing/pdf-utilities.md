---
title: 使用PDF實用程式
seo-title: Working with PDF Utilities
description: 使用PDF實用程式服務在PDF和XDP檔案格式之間轉換，設定和檢索PDF文檔屬性，並處理元XMP資料。
seo-description: Use the PDF Utilities service to convert between PDF and XDP file formats, set and retrieve PDF document properties, and manipulate XMP metadata.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2579'
ht-degree: 1%

---

# 使用PDF實用程式 {#working-with-pdf-utilities}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於PDF實用程式服務**

PDF實用程式服務可以在PDF和XDP檔案格式之間轉換，設定和檢索PDF文檔屬性，以及處理XMP元資料。 例如，在將PDF文檔轉換為其他格式之前，檢查其屬性以確定要為轉換調用的服務操作非常有用。

您可以使用「PDF實用程式」服務完成以下任務：

* 將PDF文檔轉換為XDP文檔。
* 將XDP文檔轉換為PDF文檔。 (請參閱 [將XDP文檔轉換為PDF文檔](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)。)
* 檢索PDF文檔屬性。 (請參閱 [檢索PDF文檔屬性](pdf-utilities.md#retrieving-pdf-document-properties)。)
* 保存PDF文檔並優化它以快速查看Web。 (請參閱 [設定PDF文檔保存模式](pdf-utilities.md#setting-pdf-document-save-modes)。)

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PDF文檔轉換為XDP文檔 {#converting-pdf-documents-into-xdp-documents}

可以使用PDF實用程式Java和Web服務API以寫程式方式將PDF文檔轉換為XDP文檔。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要將PDF文檔轉換為XDP文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立PDFUtilityService客戶端。
1. 調用PDF到XDP轉換操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，通過建立 `PDFUtilityServiceClient` 的雙曲餘切值。 使用Web服務API，可通過使用 `PDFUtilityServiceService` 的雙曲餘切值。

**調用PDF到XDP轉換操作**

建立服務客戶端後，可以調用PDF到XDP轉換操作。

**另請參閱**

[使用Java API將PDF文檔轉換為XDP文檔](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服務API將PDF文檔轉換為XDP文檔](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將PDF文檔轉換為XDP文檔 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

使用PDF實用程式API(Java)將PDF文檔轉換為XDP文檔：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用PDF到XDP轉換操作

   要執行轉換，請調用 `PDFUtilityServiceClient` 對象 `convertPDFtoXDP` 方法和傳遞 `com.adobe.idp.Document` 表示PDF檔案的對象。 該方法返回 `com.adobe.idp.Document` 表示新建立的XDP檔案的對象。

**另請參閱**

[將PDF文檔轉換為XDP文檔](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將PDF文檔轉換為XDP文檔 {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

使用PDF實用程式API（Web服務）將PDF文檔轉換為XDP文檔：

1. 包括項目檔案

   * 建立一個Microsoft.NET客戶端程式集，該程式集佔用PDF實用程式服務WSDL檔案。
   * 引用Microsoft.NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceService` 對象。

1. 調用PDF到XDP轉換操作

   調用 `PDFUtilityServiceService` 對象 `convertPDFtoXDP` 方法和傳遞 `BLOB` 表示PDF檔案的對象。 該方法返回 `BLOB` 表示新建立的XDP檔案的對象。

**另請參閱**

[將PDF文檔轉換為XDP文檔](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 將XDP文檔轉換為PDF文檔 {#converting-xdp-documents-into-pdf-documents}

可以使用PDF實用程式Java和Web服務API以寫程式方式將XDP文檔轉換為PDF文檔。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要將XDP文檔轉換為PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立PDFUtilityService客戶端。
1. 調用XDP到PDF轉換操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，通過建立 `PDFUtilityServiceClient` 的雙曲餘切值。 使用Web服務API，可通過使用 `PDFUtilityServiceService` 的雙曲餘切值。

**調用XDP到PDF轉換操作**

建立服務客戶端後，可以調用XDP到PDF轉換操作。

**另請參閱**

[使用Java API將XDP文檔轉換為PDF文檔](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[使用Web服務API將XDP文檔轉換為PDF文檔](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將XDP文檔轉換為PDF文檔 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

使用PDF實用程式API(Java)將XDP文檔轉換為PDF文檔：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用XDP到PDF轉換操作

   要執行轉換，請調用 `PDFUtilityServiceClient` 對象 `convertXDPtoPDF` 方法和傳遞 `com.adobe.idp.Document` 表示XDP檔案的對象。 該方法返回 `com.adobe.idp.Document` 表示新建立的PDF檔案的對象。

**另請參閱**

[將XDP文檔轉換為PDF文檔](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將XDP文檔轉換為PDF文檔 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

使用PDF實用程式API（Web服務API）將XDP文檔轉換為PDF文檔：

1. 包括項目檔案

   * 建立一個Microsoft.NET客戶端程式集，該程式集佔用PDF實用程式服務WSDL檔案。
   * 引用Microsoft.NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceService` 對象。

1. 調用XDP到PDF轉換操作

   要執行轉換，請調用 `PDFUtilityServiceService` 對象 `convertXDPtoPDF` 方法和傳遞 `BLOB` 表示XDP檔案的對象。 該方法返回 `BLOB` 表示新建立的PDF檔案的對象。

**另請參閱**

[將XDP文檔轉換為PDF文檔](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 檢索PDF文檔屬性 {#retrieving-pdf-document-properties}

可以使用PDF實用程式Java和Web服務API以寫程式方式檢索PDF文檔屬性，如文檔是可填充表單還是讀取文檔所需的最低Acrobat版本。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟摘要 {#summary_of_steps-2}

要檢索PDF文檔屬性，請執行以下步驟：

1. 包括項目檔案。
1. 建立PDFUtilityService客戶端。
1. 調用屬性檢索操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，通過建立 `PDFUtilityServiceClient` 的雙曲餘切值。 使用Web服務API，可以使用 `PDFUtilityServiceService` 的雙曲餘切值。

**調用屬性檢索操作**

建立服務客戶端後，可以調用屬性檢索操作。

**另請參閱**

[使用Java API檢索PDF文檔屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[使用Web服務API檢索PDF文檔屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API檢索PDF文檔屬性 {#retrieve-pdf-document-properties-using-the-java-api}

使用PDF實用程式API(Java)檢索PDF文檔屬性：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用屬性檢索操作

   要執行轉換，請調用 `PDFUtilityServiceClient` 對象 `getPDFProperties` 方法和傳遞：

   * A `com.adobe.idp.Document` 表示PDF文檔的對象。
   * A `PDFPropertiesOptionSpec` 包含要計算的屬性的對象。

   該方法返回 `PDFPropertiesResult` 包含查詢結果的對象。

**另請參閱**

[檢索PDF文檔屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API檢索PDF文檔屬性 {#retrieve-pdf-document-properties-using-the-web-service-api}

使用PDF實用程式Web服務API檢索PDF文檔屬性：

1. 包括項目檔案

   * 建立一個Microsoft.NET客戶端程式集，該程式集佔用PDF實用程式服務WSDL檔案。
   * 引用Microsoft.NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceService` 對象。

1. 調用屬性檢索操作

   要執行轉換，請調用 `PDFUtilityServiceService` 對象 `getPDFProperties` 方法和傳遞：

   * A `BLOB` 表示PDF文檔的對象。
   * A `PDFPropertiesOptionSpec` 包含要計算的屬性的對象。

   該方法返回 `PDFPropertiesResult` 包含查詢結果的對象。

**另請參閱**

[檢索PDF文檔屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 設定PDF文檔保存模式 {#setting-pdf-document-save-modes}

可以使用PDF實用程式服務Java和Web服務API以寫程式方式為PDF文檔設定保存模式。 當使用PDF實用程式服務設定保存模式時，PDF實用程式服務僅設定保存模式，而實際上不會保存PDF文檔。 PDF文檔在傳遞到另一個服務操作時被保存。 例如，您可以使用PDF實用程式服務設定特定的保存模式並將其傳遞給加密服務，在該服務中實際保存並加密PDF文檔。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

要設定PDF文檔的保存選項，請執行以下步驟：

1. 包括項目檔案。
1. 建立PDFUtilityService客戶端。
1. 設定保存模式。
1. 調用保存操作。
1. 將PDF文檔傳遞到其他操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，通過建立 `PDFUtilityServiceClient` 的雙曲餘切值。 使用Web服務API，可以使用 `PDFUtilityServiceService` 的雙曲餘切值。

**設定保存模式**

您可以選擇以下保存選項之一：

* `INCREMENTAL`:以增量方式保存以減少保存所需的時間
* `FAST_WEB_VIEW`:保存，快速查看Web
* `FULL`:使用完全保存（不進行優化）進行保存

**調用保存樣式操作**

建立服務客戶端後，可以調用屬性檢索操作。

**將PDF文檔轉給另一個AEM Forms行動**

PDF實用程式服務設定指定的保存模式後，將PDF文檔傳遞到另一個AEM Forms操作。 從該操作返回後，PDF文檔將以指定模式保存。 例如，如果使用「PDF實用程式」服務來設定 `FAST_WEB_VIEW` 模式，然後將PDF文檔傳遞到加密服務 `encryptUsingPassword` 操作，返回的PDF文檔將用密碼進行加密並保存在 `FAST_WEB_VIEW` 的子菜單。

>[!NOTE]
>
>與此部分關聯的快速啟動設定 `FAST_WEB_VIEW` 模式，然後將PDF文檔傳遞給加密服務 `encryptUsingPassword` 的下界。

**另請參閱**

[使用Java API設定PDF文檔保存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[使用Web服務API設定PDF文檔保存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用密碼加密PDF文檔](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API設定PDF文檔保存選項 {#set-pdf-document-save-options-using-the-java-api}

使用PDF實用程式API(Java)設定PDF文檔保存選項：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 設定保存模式

   * 建立 `PDFUtilitySaveMode` 對象。
   * 通過調用 `PDFUtilitySaveMode` 對象 `setSaveStyle` 方法並傳遞指定保存模式的字串值。 例如，要保存以便快速查看Web，請傳遞 `FAST_WEB_VIEW`。

1. 調用保存樣式操作

   調用 `PDFUtilityServiceClient` 對象 `setSaveMode` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示PDF文檔的對象。
   * A `PDFUtilitySaveMode` 包含要使用的保存樣式的對象。
   * 用於確定是否覆蓋任何先前設定的布爾值。

   該方法返回 `com.adobe.idp.Document` 使用指定的保存樣式格式化的對象。

1. 將PDF文檔轉給另一個AEM Forms行動

   * 傳遞返回的 `com.adobe.idp.Document` 反對另一個AEM Forms行動。

**另請參閱**

[設定PDF文檔保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API設定PDF文檔保存選項 {#set-pdf-document-save-options-using-the-web-service-api}

使用PDF實用程式AP（Web服務）設定PDF文檔保存選項：

1. 包括項目檔案

   * 建立一個Microsoft.NET客戶端程式集，該程式集佔用PDF實用程式服務WSDL檔案。
   * 引用Microsoft.NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceService` 對象。

1. 設定保存模式

   * 建立 `PDFUtilitySaveMode` 對象。
   * 通過為 `PDFUtilitySaveMode` 對象 `saveStyle` 指定保存模式的方法。 例如，要保存以便快速查看Web，請指定 `FAST_WEB_VIEW`。

1. 調用保存樣式操作

   調用 `PDFUtilityServiceService` 對象 `setSaveMode` 方法並傳遞以下值：

   * A `BLOB` 表示PDF文檔的對象。
   * A `PDFUtilitySaveMode` 包含要使用的保存樣式的對象。
   * 用於確定是否覆蓋任何先前設定的布爾值。

   該方法返回 `BLOB` 使用指定的保存樣式格式化的對象。 然後，可將該對象另存為PDF文檔。

1. 將PDF文檔轉給另一個Forms行動

   * 傳遞返回的 `BLOB` 反對另一個AEM Forms行動。

**另請參閱**

[設定PDF文檔保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 清理PDF文檔 {#sanitizing-pdf-documents}

可以使用PDF實用程式Java API以寫程式方式將PDF文檔轉換為XDP文檔。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

要清理PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立PDFUtilityService客戶端。
1. 調用清理操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 要使用Java建立客戶端應用程式，請包括必要的JAR檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行清理操作之前，必須建立PDFUtilityService客戶端。 使用Java API，通過建立 `PDFUtilityServiceClient` 的雙曲餘切值。

**調用PDF到XDP轉換操作**

建立服務客戶端後，可以調用清理操作。

**另請參閱**

[使用Java API將PDF文檔轉換為XDP文檔](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服務API將PDF文檔轉換為XDP文檔](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API清理PDF文檔 {#sanitize-pdf-documents-using-the-java-api}

使用PDF實用程式API(Java)清理文檔：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用PDF到XDP轉換操作

   要執行轉換，請調用 `PDFUtilityServiceClient` 對象 `convertPDFtoXDP` 方法和傳遞 `com.adobe.idp.Document` 表示PDF檔案的對象。 該方法返回 `com.adobe.idp.Document` 表示新建立的XDP檔案的對象。

**另請參閱**

[清理PDF文檔](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
