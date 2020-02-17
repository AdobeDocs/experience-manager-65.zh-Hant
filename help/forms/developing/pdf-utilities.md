---
title: 使用PDF公用程式
seo-title: 使用PDF公用程式
description: 'null'
seo-description: 'null'
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用PDF公用程式 {#working-with-pdf-utilities}

**關於PDF公用程式服務**

PDF公用程式服務可在PDF和XDP檔案格式之間轉換、設定和擷取PDF檔案屬性，以及控制XMP中繼資料。 例如，在將PDF檔案轉換為其他格式之前，請先檢查其屬性，以判斷要叫用哪個服務操作來轉換。

您可以使用PDF公用程式服務完成下列工作：

* 將PDF檔案轉換為XDP檔案。
* 將XDP檔案轉換為PDF檔案。 (請參 [閱將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)。)
* 擷取PDF檔案屬性。 (請參閱 [擷取PDF檔案屬性](pdf-utilities.md#retrieving-pdf-document-properties)。)
* 儲存PDF檔案並最佳化它，以快速進行網頁檢視。 (請參閱 [設定PDF檔案儲存模式](pdf-utilities.md#setting-pdf-document-save-modes)。)

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PDF檔案轉換為XDP檔案 {#converting-pdf-documents-into-xdp-documents}

您可以使用PDF公用程式Java和web service API，以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將PDF檔案轉換為XDP檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 叫用PDF至XDP轉換作業。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDF utility用戶端，才能以程式設計方式執行PDF公用程式作業。 使用Java API，這是透過建立物件來 `PDFUtilityServiceClient` 完成。 使用web service API，這是透過使用物件來 `PDFUtilityServiceService` 完成。

**叫用PDF至XDP轉換作業**

建立服務用戶端後，您可以叫用PDF至XDP轉換作業。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用web service API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將PDF檔案轉換為XDP檔案 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

使用PDF公用程式API(Java)將PDF檔案轉換為XDP檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其 `PDFUtilityServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 叫用PDF至XDP轉換作業

   若要執行轉換，請叫 `PDFUtilityServiceClient` 用物件的方 `convertPDFtoXDP` 法並傳入代 `com.adobe.idp.Document` 表PDF檔案的物件。 該方法返回 `com.adobe.idp.Document` 表示新建立的XDP檔案的對象。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API將PDF檔案轉換為XDP檔案 {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

使用PDF公用程式API(web service)將PDF檔案轉換為XDP檔案：

1. 包含專案檔案

   * 建立會使用PDF公用程式服務WSDL檔案的Microsoft .NET用戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立PDFUlitiveService用戶端

   使用您 `PDFUtilityServiceService` 的proxy類別建構函式建立物件。

1. 叫用PDF至XDP轉換作業

   叫用物 `PDFUtilityServiceService` 件的方 `convertPDFtoXDP` 法並傳入代表 `BLOB` PDF檔案的物件。 該方法返回 `BLOB` 表示新建立的XDP檔案的對象。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 將XDP檔案轉換為PDF檔案 {#converting-xdp-documents-into-pdf-documents}

您可以使用PDF公用程式Java和web service API，以程式設計方式將XDP檔案轉換為PDF檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要將XDP文檔轉換為PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 叫用XDP至PDF轉換作業。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDF utility用戶端，才能以程式設計方式執行PDF公用程式作業。 使用Java API，這是透過建立物件來 `PDFUtilityServiceClient` 完成。 使用web service API，這是透過使用物件來 `PDFUtilityServiceService` 完成。

**叫用XDP至PDF轉換作業**

建立服務用戶端後，您可以叫用XDP至PDF轉換作業。

**另請參閱**

[使用Java API將XDP檔案轉換為PDF檔案](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[使用web service API將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將XDP檔案轉換為PDF檔案 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

使用PDF公用程式API(Java)將XDP檔案轉換為PDF檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其 `PDFUtilityServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 叫用XDP至PDF轉換作業

   若要執行轉換，請叫 `PDFUtilityServiceClient` 用物件的方 `convertXDPtoPDF` 法並傳入代 `com.adobe.idp.Document` 表XDP檔案的物件。 此方法會傳回 `com.adobe.idp.Document` 代表新建立之PDF檔案的物件。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API將XDP檔案轉換為PDF檔案 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

使用PDF公用程式API(web service API)將XDP檔案轉換為PDF檔案：

1. 包含專案檔案

   * 建立會使用PDF公用程式服務WSDL檔案的Microsoft .NET用戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立PDFUlitiveService用戶端

   使用您 `PDFUtilityServiceService` 的proxy類別建構函式建立物件。

1. 叫用XDP至PDF轉換作業

   若要執行轉換，請叫 `PDFUtilityServiceService` 用物件的方 `convertXDPtoPDF` 法並傳入代 `BLOB` 表XDP檔案的物件。 此方法會傳回 `BLOB` 代表新建立之PDF檔案的物件。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 擷取PDF檔案屬性 {#retrieving-pdf-document-properties}

您可以使用PDF公用程式Java和web service API，以程式設計方式擷取PDF檔案屬性，例如檔案是可填寫的表單，或是讀取檔案所需的最低Acrobat版本。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟摘要 {#summary_of_steps-2}

要檢索PDF文檔屬性，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 調用屬性檢索操作。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDF utility用戶端，才能以程式設計方式執行PDF公用程式作業。 使用Java API，這是透過建立物件來 `PDFUtilityServiceClient` 完成。 使用web service API，這是使用物件來完 `PDFUtilityServiceService` 成。

**調用屬性檢索操作**

建立服務客戶端後，可以調用屬性檢索操作。

**另請參閱**

[使用Java API擷取PDF檔案屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[使用web service API擷取PDF檔案屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API擷取PDF檔案屬性 {#retrieve-pdf-document-properties-using-the-java-api}

使用PDF公用程式API(Java)擷取PDF檔案屬性：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其 `PDFUtilityServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 調用屬性檢索操作

   若要執行轉換，請叫 `PDFUtilityServiceClient` 用物件的方 `getPDFProperties` 法並傳入下列項目：

   * 代 `com.adobe.idp.Document` 表PDF文檔的對象。
   * 包 `PDFPropertiesOptionSpec` 含要評估的屬性的對象。
   方法返回包 `PDFPropertiesResult` 含查詢結果的對象。

**另請參閱**

[擷取PDF檔案屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API擷取PDF檔案屬性 {#retrieve-pdf-document-properties-using-the-web-service-api}

使用PDF公用程式網站服務API擷取PDF檔案屬性：

1. 包含專案檔案

   * 建立會使用PDF公用程式服務WSDL檔案的Microsoft .NET用戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立PDFUlitiveService用戶端

   使用您 `PDFUtilityServiceService` 的proxy類別建構函式建立物件。

1. 調用屬性檢索操作

   若要執行轉換，請叫 `PDFUtilityServiceService` 用物件的方 `getPDFProperties` 法並傳入下列項目：

   * 代 `BLOB` 表PDF文檔的對象。
   * 包 `PDFPropertiesOptionSpec` 含要評估的屬性的對象。
   方法返回包 `PDFPropertiesResult` 含查詢結果的對象。

**另請參閱**

[擷取PDF檔案屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 設定PDF檔案儲存模式 {#setting-pdf-document-save-modes}

您可以使用PDF公用程式服務Java和web service API，以程式設計方式為PDF檔案設定儲存模式。 當使用「PDF公用程式」服務來設定儲存模式時，「PDF公用程式」服務只會設定儲存模式，而不會實際儲存PDF檔案。 當PDF檔案傳遞至其他服務作業時，會儲存該檔案。 例如，您可以使用PDF公用程式服務來設定特定的儲存模式，並將它傳遞至加密服務，在此處會實際儲存並加密PDF檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

要設定PDF文檔的保存選項，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 設定保存模式。
1. 調用保存操作。
1. 將PDF檔案傳遞至另一個作業。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDF utility用戶端，才能以程式設計方式執行PDF公用程式作業。 使用Java API，這是透過建立物件來 `PDFUtilityServiceClient` 完成。 使用web service API，這是使用物件來完 `PDFUtilityServiceService` 成。

**設定保存模式**

您可以選擇下列其中一個儲存選項：

* `INCREMENTAL`:以增量方式節省成本，以縮短節省成本的時間
* `FAST_WEB_VIEW`:儲存以快速檢視網頁
* `FULL`:使用完整儲存進行儲存（無最佳化）

**調用保存樣式操作**

建立服務客戶端後，可以調用屬性檢索操作。

**將PDF檔案傳遞至其他AEM Forms作業**

一旦PDF公用程式服務設定指定的「儲存」模式後，請將PDF檔案傳遞至其他AEM Forms作業。 從該操作返回後，PDF文檔將以指定模式保存。 例如，如果您使用PDF公用程式服務來設定模式，然後將 `FAST_WEB_VIEW` PDF檔案傳遞至加密服務的作業，則傳回的PDF檔案會以密碼加密，並儲存在 `encryptUsingPassword``FAST_WEB_VIEW` 模式中。

>[!NOTE]
>
>與本節關聯的快速入門會設定模 `FAST_WEB_VIEW` 式，然後將PDF檔案傳送至加密服務的作 `encryptUsingPassword` 業。

**另請參閱**

[使用Java API設定PDF檔案儲存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[使用web service API設定PDF檔案儲存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API設定PDF檔案儲存選項 {#set-pdf-document-save-options-using-the-java-api}

使用PDF公用程式API(Java)設定PDF檔案儲存選項：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其 `PDFUtilityServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 設定保存模式

   * 使用其 `PDFUtilitySaveMode` 建構函式建立物件。
   * 調用物件的方法並傳 `PDFUtilitySaveMode` 遞指定儲 `setSaveStyle` 存模式的字串值，以設定儲存模式。 例如，若要儲存以快速檢視網頁，請傳遞 `FAST_WEB_VIEW`。

1. 調用保存樣式操作

   叫用物 `PDFUtilityServiceClient` 件的方 `setSaveMode` 法並傳遞下列值：

   * 代 `com.adobe.idp.Document` 表PDF文檔的對象。
   * 包 `PDFUtilitySaveMode` 含要使用的保存樣式的對象。
   * 用於確定是否覆蓋任何先前設定的布爾值。
   該方法返回使 `com.adobe.idp.Document` 用指定的保存樣式格式化的對象。

1. 將PDF檔案傳遞至其他AEM Forms作業

   * 將傳回的物 `com.adobe.idp.Document` 件傳遞至另一個AEM Forms作業。

**另請參閱**

[設定PDF檔案儲存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API設定PDF檔案儲存選項 {#set-pdf-document-save-options-using-the-web-service-api}

使用PDF公用程式AP(web service)來設定PDF檔案儲存選項：

1. 包含專案檔案

   * 建立會使用PDF公用程式服務WSDL檔案的Microsoft .NET用戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立PDFUlitiveService用戶端

   使用您 `PDFUtilityServiceService` 的proxy類別建構函式建立物件。

1. 設定保存模式

   * 使用其 `PDFUtilitySaveMode` 建構函式建立物件。
   * 為指定儲存模式的物件方法指 `PDFUtilitySaveMode` 定字串值， `saveStyle` 以設定儲存模式。 例如，若要儲存以快速檢視網頁，請指定 `FAST_WEB_VIEW`。

1. 調用保存樣式操作

   叫用物 `PDFUtilityServiceService` 件的方 `setSaveMode` 法並傳遞下列值：

   * 代 `BLOB` 表PDF文檔的對象。
   * 包 `PDFUtilitySaveMode` 含要使用的保存樣式的對象。
   * 用於確定是否覆蓋任何先前設定的布爾值。
   該方法返回使 `BLOB` 用指定的保存樣式格式化的對象。 然後，您可以將該物件儲存為PDF檔案。

1. 將PDF檔案傳遞至其他Forms作業

   * 將傳回的物 `BLOB` 件傳遞至另一個AEM Forms作業。

**另請參閱**

[設定PDF檔案儲存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 淨化PDF檔案 {#sanitizing-pdf-documents}

您可以使用PDF公用程式Java API，以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

若要淨化PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 調用淨化操作。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 要使用Java建立客戶端應用程式，請包括必要的JAR檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDFUtilityService用戶端，才能以程式設計方式執行淨化作業。 使用Java API，這是透過建立物件來 `PDFUtilityServiceClient` 完成。

**叫用PDF至XDP轉換作業**

建立服務客戶端後，可以調用淨化操作。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用web service API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API淨化PDF檔案 {#sanitize-pdf-documents-using-the-java-api}

使用PDF公用程式API(Java)淨化檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其 `PDFUtilityServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 叫用PDF至XDP轉換作業

   若要執行轉換，請叫 `PDFUtilityServiceClient` 用物件的方 `convertPDFtoXDP` 法並傳入代 `com.adobe.idp.Document` 表PDF檔案的物件。 該方法返回 `com.adobe.idp.Document` 表示新建立的XDP檔案的對象。

**另請參閱**

[淨化PDF檔案](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
