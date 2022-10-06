---
title: 使用PDF實用程式
seo-title: Working with PDF Utilities
description: 使用PDF實用程式服務在PDF和XDP檔案格式之間進行轉換、設定和檢索PDF文檔屬性，以及處理XMP元資料。
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

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於PDF公用程式服務**

PDF實用程式服務可在PDF和XDP檔案格式之間轉換、設定和檢索PDF文檔屬性，以及操控XMP元資料。 例如，在將PDF文檔轉換為其他格式之前，檢查其屬性以確定要為轉換調用的服務操作非常有用。

您可以使用PDF實用程式服務來完成這些工作：

* 將PDF檔案轉換為XDP檔案。
* 將XDP檔案轉換為PDF檔案。 (請參閱 [將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* 檢索PDF文檔屬性。 (請參閱 [檢索PDF文檔屬性](pdf-utilities.md#retrieving-pdf-document-properties).)
* 儲存PDF檔案並加以最佳化，以快速檢視網頁。 (請參閱 [設定PDF文檔保存模式](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將PDF檔案轉換為XDP檔案 {#converting-pdf-documents-into-xdp-documents}

您可以使用PDF公用程式Java和網頁服務API，以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要將PDF文檔轉換為XDP文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 調用PDF到XDP轉換操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，您可以建立 `PDFUtilityServiceClient` 物件。 若使用網站服務API，則需使用 `PDFUtilityServiceService` 物件。

**調用PDF到XDP轉換操作**

建立服務用戶端後，您可以叫用PDF至XDP轉換操作。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服務API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將PDF檔案轉換為XDP檔案 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

使用PDF公用程式API(Java)將PDF檔案轉換為XDP檔案：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用PDF到XDP轉換操作

   若要執行轉換，請叫用 `PDFUtilityServiceClient` 物件 `convertPDFtoXDP` 在 `com.adobe.idp.Document` 代表PDF檔案的物件。 方法會傳回 `com.adobe.idp.Document` 代表新建立之XDP檔案的物件。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將PDF檔案轉換為XDP檔案 {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

使用PDF公用程式API（網站服務）將PDF檔案轉換為XDP檔案：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集會使用PDF實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceService` 物件，使用您的proxy類別建構子。

1. 調用PDF到XDP轉換操作

   叫用 `PDFUtilityServiceService` 物件 `convertPDFtoXDP` 在 `BLOB` 代表PDF檔案的物件。 方法會傳回 `BLOB` 代表新建立之XDP檔案的物件。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 將XDP檔案轉換為PDF檔案 {#converting-xdp-documents-into-pdf-documents}

您可以使用PDF公用程式Java和網頁服務API，以程式設計方式將XDP檔案轉換為PDF檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

要將XDP文檔轉換為PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 調用XDP到PDF轉換操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，您可以建立 `PDFUtilityServiceClient` 物件。 若使用網站服務API，則需使用 `PDFUtilityServiceService` 物件。

**調用XDP到PDF轉換操作**

建立服務用戶端後，您可以叫用XDP以PDF轉換操作。

**另請參閱**

[使用Java API將XDP檔案轉換為PDF檔案](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[使用Web服務API將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將XDP檔案轉換為PDF檔案 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

使用PDF公用程式API(Java)將XDP檔案轉換為PDF檔案：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用XDP到PDF轉換操作

   若要執行轉換，請叫用 `PDFUtilityServiceClient` 物件 `convertXDPtoPDF` 在 `com.adobe.idp.Document` 代表XDP檔案的物件。 方法會傳回 `com.adobe.idp.Document` 代表新建立的PDF檔案的物件。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將XDP檔案轉換為PDF檔案 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

使用PDF公用程式API（網站服務API），將XDP檔案轉換為PDF檔案：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集會使用PDF實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceService` 物件，使用您的proxy類別建構子。

1. 調用XDP到PDF轉換操作

   若要執行轉換，請叫用 `PDFUtilityServiceService` 物件 `convertXDPtoPDF` 在 `BLOB` 代表XDP檔案的物件。 方法會傳回 `BLOB` 代表新建立的PDF檔案的物件。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 檢索PDF文檔屬性 {#retrieving-pdf-document-properties}

您可以使用PDF實用程式Java和Web服務API以寫程式方式檢索PDF文檔屬性，例如文檔是可填寫的表單還是讀取文檔所需的最低Acrobat版本。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟摘要 {#summary_of_steps-2}

要檢索PDF文檔屬性，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 調用屬性檢索操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，您可以建立 `PDFUtilityServiceClient` 物件。 若使用網站服務API，這是使用 `PDFUtilityServiceService` 物件。

**調用屬性檢索操作**

建立服務客戶端後，可以調用屬性檢索操作。

**另請參閱**

[使用Java API檢索PDF文檔屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[使用Web服務API檢索PDF文檔屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API檢索PDF文檔屬性 {#retrieve-pdf-document-properties-using-the-java-api}

使用PDF實用程式API(Java)檢索PDF文檔屬性：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用屬性檢索操作

   若要執行轉換，請叫用 `PDFUtilityServiceClient` 物件 `getPDFProperties` 方法，並傳遞下列內容：

   * A `com.adobe.idp.Document` 表示PDF文檔的對象。
   * A `PDFPropertiesOptionSpec` 包含要評估的屬性的對象。

   方法會傳回 `PDFPropertiesResult` 包含查詢結果的對象。

**另請參閱**

[檢索PDF文檔屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API檢索PDF文檔屬性 {#retrieve-pdf-document-properties-using-the-web-service-api}

使用PDF實用程式Web服務API檢索PDF文檔屬性：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集會使用PDF實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceService` 物件，使用您的proxy類別建構子。

1. 調用屬性檢索操作

   若要執行轉換，請叫用 `PDFUtilityServiceService` 物件 `getPDFProperties` 方法，並傳遞下列內容：

   * A `BLOB` 表示PDF文檔的對象。
   * A `PDFPropertiesOptionSpec` 包含要評估的屬性的對象。

   方法會傳回 `PDFPropertiesResult` 包含查詢結果的對象。

**另請參閱**

[檢索PDF文檔屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 設定PDF文檔保存模式 {#setting-pdf-document-save-modes}

您可以使用PDF實用程式服務Java和Web服務API，以寫程式方式為PDF文檔設定保存模式。 使用PDF實用程式服務設定保存模式時，PDF實用程式服務僅設定保存模式，實際上不保存PDF文檔。 PDF文檔在傳遞到其他服務操作時被保存。 例如，您可以使用PDF實用程式服務來設定特定的儲存模式，並將其傳遞至加密服務，在該服務中實際保存和加密PDF文檔。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-3}

要設定PDF文檔的保存選項，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 設定儲存模式。
1. 調用保存操作。
1. 將PDF文檔傳遞到其他操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，您可以建立 `PDFUtilityServiceClient` 物件。 若使用網站服務API，這是使用 `PDFUtilityServiceService` 物件。

**設定「儲存」模式**

您可以選擇下列其中一個儲存選項：

* `INCREMENTAL`:以增量方式儲存以縮短儲存所需的時間
* `FAST_WEB_VIEW`:保存以快速查看Web
* `FULL`:使用完整儲存來儲存（無最佳化）

**調用保存樣式操作**

建立服務客戶端後，可以調用屬性檢索操作。

**將PDF檔案傳遞至其他AEM Forms作業**

一旦PDF實用程式服務設定了指定的保存模式，請將PDF文檔傳遞到另一個AEM Forms操作。 從該操作返回後，PDF文檔將以指定模式保存。 例如，如果您使用PDF公用程式服務來設定 `FAST_WEB_VIEW` 模式，然後將PDF文檔傳遞到加密服務的 `encryptUsingPassword` 操作時，返回的PDF文檔會用密碼加密並保存在 `FAST_WEB_VIEW` 模式。

>[!NOTE]
>
>與此部分關聯的「快速入門」設定 `FAST_WEB_VIEW` 模式，然後將PDF文檔傳遞到加密服務 `encryptUsingPassword` 操作。

**另請參閱**

[使用Java API設定PDF文檔保存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[使用Web服務API設定PDF文檔保存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用密碼加密PDF文檔](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API設定PDF文檔保存選項 {#set-pdf-document-save-options-using-the-java-api}

使用PDF實用程式API(Java)設定PDF文檔保存選項：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 設定「儲存」模式

   * 建立 `PDFUtilitySaveMode` 物件，使用其建構子。
   * 調用 `PDFUtilitySaveMode` 物件 `setSaveStyle` 方法，並傳遞指定儲存模式的字串值。 例如，若要儲存以供快速Web檢視，請傳遞 `FAST_WEB_VIEW`.

1. 調用保存樣式操作

   叫用 `PDFUtilityServiceClient` 物件 `setSaveMode` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 表示PDF文檔的對象。
   * A `PDFUtilitySaveMode` 包含要使用的儲存樣式的物件。
   * 用於確定是否覆蓋任何先前設定的布林值。

   方法會傳回 `com.adobe.idp.Document` 使用指定保存樣式格式化的對象。

1. 將PDF檔案傳遞至其他AEM Forms作業

   * 傳回 `com.adobe.idp.Document` 物件至其他AEM Forms作業。

**另請參閱**

[設定PDF文檔保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API設定PDF文檔保存選項 {#set-pdf-document-save-options-using-the-web-service-api}

使用PDF實用程式AP（web服務）設定PDF文檔保存選項：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集會使用PDF實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceService` 物件，使用您的proxy類別建構子。

1. 設定「儲存」模式

   * 建立 `PDFUtilitySaveMode` 物件，使用其建構子。
   * 為 `PDFUtilitySaveMode` 物件 `saveStyle` 指定儲存模式的方法。 例如，要保存以便快速查看Web，請指定 `FAST_WEB_VIEW`.

1. 調用保存樣式操作

   叫用 `PDFUtilityServiceService` 物件 `setSaveMode` 方法，並傳遞下列值：

   * A `BLOB` 表示PDF文檔的對象。
   * A `PDFUtilitySaveMode` 包含要使用的儲存樣式的物件。
   * 用於確定是否覆蓋任何先前設定的布林值。

   方法會傳回 `BLOB` 使用指定保存樣式格式化的對象。 然後，您可以將該物件儲存為PDF檔案。

1. 將PDF檔案傳遞至其他Forms作業

   * 傳回 `BLOB` 物件至其他AEM Forms作業。

**另請參閱**

[設定PDF文檔保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 清理PDF文檔 {#sanitizing-pdf-documents}

您可以使用PDF公用程式Java API，以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-4}

要清理PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 調用淨化操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 要使用Java建立客戶端應用程式，請包括必要的JAR檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行淨化操作之前，必須建立PDFUtilityService客戶端。 使用Java API，您可以建立 `PDFUtilityServiceClient` 物件。

**調用PDF到XDP轉換操作**

建立服務客戶端後，可以調用淨化操作。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服務API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API處理PDF檔案 {#sanitize-pdf-documents-using-the-java-api}

使用PDF公用程式API(Java)處理檔案：

1. 包含項目檔案

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   建立 `PDFUtilityServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用PDF到XDP轉換操作

   若要執行轉換，請叫用 `PDFUtilityServiceClient` 物件 `convertPDFtoXDP` 在 `com.adobe.idp.Document` 代表PDF檔案的物件。 方法會傳回 `com.adobe.idp.Document` 代表新建立之XDP檔案的物件。

**另請參閱**

[清理PDF文檔](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
