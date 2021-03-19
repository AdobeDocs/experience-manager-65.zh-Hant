---
title: 使用PDF公用程式
seo-title: 使用PDF公用程式
description: 使用PDF公用程式服務，在PDF和XDP檔案格式之間轉換、設定和擷取PDF檔案屬性，以及控制中XMP繼資料。
seo-description: 使用PDF公用程式服務，在PDF和XDP檔案格式之間轉換、設定和擷取PDF檔案屬性，以及控制中XMP繼資料。
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2607'
ht-degree: 1%

---


# 使用PDF實用程式{#working-with-pdf-utilities}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

**關於PDF公用程式服務**

PDF公用程式服務可在PDF和XDP檔案格式之間轉換、設定和擷取PDF檔案屬性，以及控制中繼XMP資料。 例如，在將PDF檔案轉換為其他格式之前，請先檢查其屬性，以判斷要叫用哪個服務操作來轉換。

您可以使用PDF公用程式服務完成下列工作：

* 將PDF檔案轉換為XDP檔案。
* 將XDP檔案轉換為PDF檔案。 （請參閱[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)。）
* 擷取PDF檔案屬性。 （請參閱[擷取PDF檔案屬性](pdf-utilities.md#retrieving-pdf-document-properties)。）
* 儲存PDF檔案並最佳化它，以快速進行網頁檢視。 （請參閱[設定PDF檔案儲存模式](pdf-utilities.md#setting-pdf-document-save-modes)）。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PDF檔案轉換為XDP檔案{#converting-pdf-documents-into-xdp-documents}

您可以使用PDF公用程式Java和web service API，以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

若要將PDF檔案轉換為XDP檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 叫用PDF至XDP轉換作業。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDF Utility用戶端，才能以程式設計方式執行PDF公用程式作業。 使用Java API，您可建立`PDFUtilityServiceClient`物件來完成此作業。 使用web service API，這是使用`PDFUtilityServiceService`物件來完成的。

**叫用PDF至XDP轉換作業**

建立服務用戶端後，您可以叫用PDF至XDP轉換作業。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用web service API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#convert-pdf-documents-into-xdp-documents-using-the-java-api}將PDF檔案轉換為XDP檔案

使用PDF公用程式API(Java)將PDF檔案轉換為XDP檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`PDFUtilityServiceClient`對象。

1. 叫用PDF至XDP轉換作業

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`convertPDFtoXDP`方法，並傳入代表PDF檔案的`com.adobe.idp.Document`物件。 該方法返回一個`com.adobe.idp.Document`對象，該對象表示新建立的XDP檔案。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}將PDF檔案轉換為XDP檔案

使用PDF公用程式API(web service)將PDF檔案轉換為XDP檔案：

1. 包含專案檔案

   * 建立會使用PDF公用程式服務WSDL檔案的Microsoft .NET用戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立PDFUlitiveService用戶端

   使用proxy類別建構函式建立`PDFUtilityServiceService`物件。

1. 叫用PDF至XDP轉換作業

   叫用`PDFUtilityServiceService`物件的`convertPDFtoXDP`方法，並傳入代表PDF檔案的`BLOB`物件。 該方法返回一個`BLOB`對象，該對象表示新建立的XDP檔案。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 將XDP檔案轉換為PDF檔案{#converting-xdp-documents-into-pdf-documents}

您可以使用PDF公用程式Java和web service API，以程式設計方式將XDP檔案轉換為PDF檔案。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}摘要

要將XDP文檔轉換為PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 叫用XDP至PDF轉換作業。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDF Utility用戶端，才能以程式設計方式執行PDF公用程式作業。 使用Java API，您可建立`PDFUtilityServiceClient`物件來完成此作業。 使用web service API，這是使用`PDFUtilityServiceService`物件來完成的。

**叫用XDP至PDF轉換作業**

建立服務用戶端後，您可以叫用XDP至PDF轉換作業。

**另請參閱**

[使用Java API將XDP檔案轉換為PDF檔案](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[使用web service API將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#convert-xdp-documents-into-pdf-documents-using-the-java-api}將XDP檔案轉換為PDF檔案

使用PDF公用程式API(Java)將XDP檔案轉換為PDF檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`PDFUtilityServiceClient`對象。

1. 叫用XDP至PDF轉換作業

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`convertXDPtoPDF`方法，並傳入代表XDP檔案的`com.adobe.idp.Document`物件。 該方法返回一個`com.adobe.idp.Document`對象，該對象表示新建立的PDF檔案。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}將XDP檔案轉換為PDF檔案

使用PDF公用程式API(web service API)將XDP檔案轉換為PDF檔案：

1. 包含專案檔案

   * 建立會使用PDF公用程式服務WSDL檔案的Microsoft .NET用戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立PDFUlitiveService用戶端

   使用proxy類別建構函式建立`PDFUtilityServiceService`物件。

1. 叫用XDP至PDF轉換作業

   若要執行轉換，請叫用`PDFUtilityServiceService`物件的`convertXDPtoPDF`方法，並傳入代表XDP檔案的`BLOB`物件。 該方法返回一個`BLOB`對象，該對象表示新建立的PDF檔案。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 擷取PDF檔案屬性{#retrieving-pdf-document-properties}

您可以使用PDF公用程式Java和web service API，以程式設計方式擷取PDF檔案屬性，例如檔案是可填寫的表單，還是讀取檔案所需的最低Acrobat版本。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟{#summary_of_steps-2}摘要

要檢索PDF文檔屬性，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 調用屬性檢索操作。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDF Utility用戶端，才能以程式設計方式執行PDF公用程式作業。 使用Java API，您可建立`PDFUtilityServiceClient`物件來完成此作業。 使用web service API，這是使用`PDFUtilityServiceService`物件來完成的。

**調用屬性檢索操作**

建立服務客戶端後，可以調用屬性檢索操作。

**另請參閱**

[使用Java API擷取PDF檔案屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[使用web service API擷取PDF檔案屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#retrieve-pdf-document-properties-using-the-java-api}擷取PDF檔案屬性

使用PDF公用程式API(Java)擷取PDF檔案屬性：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`PDFUtilityServiceClient`對象。

1. 調用屬性檢索操作

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`getPDFProperties`方法並傳入下列：

   * 代表PDF檔案的`com.adobe.idp.Document`物件。
   * 包含要評估的屬性的`PDFPropertiesOptionSpec`對象。

   方法返回包含查詢結果的`PDFPropertiesResult`對象。

**另請參閱**

[擷取PDF檔案屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#retrieve-pdf-document-properties-using-the-web-service-api}擷取PDF檔案屬性

使用PDF公用程式網站服務API擷取PDF檔案屬性：

1. 包含專案檔案

   * 建立會使用PDF公用程式服務WSDL檔案的Microsoft .NET用戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立PDFUlitiveService用戶端

   使用proxy類別建構函式建立`PDFUtilityServiceService`物件。

1. 調用屬性檢索操作

   若要執行轉換，請叫用`PDFUtilityServiceService`物件的`getPDFProperties`方法並傳入下列：

   * 代表PDF檔案的`BLOB`物件。
   * 包含要評估的屬性的`PDFPropertiesOptionSpec`對象。

   方法返回包含查詢結果的`PDFPropertiesResult`對象。

**另請參閱**

[擷取PDF檔案屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 設定PDF檔案儲存模式{#setting-pdf-document-save-modes}

您可以使用PDF公用程式服務Java和web service API，以程式設計方式為PDF檔案設定儲存模式。 當使用「PDF公用程式」服務來設定儲存模式時，「PDF公用程式」服務只會設定儲存模式，而不會實際儲存PDF檔案。 當PDF檔案傳遞至其他服務作業時，會儲存該檔案。 例如，您可以使用PDF公用程式服務來設定特定的儲存模式，並將它傳遞至加密服務，在此處會實際儲存並加密PDF檔案。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-3}摘要

要設定PDF文檔的保存選項，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 設定保存模式。
1. 調用保存操作。
1. 將PDF檔案傳遞至另一個作業。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDF Utility用戶端，才能以程式設計方式執行PDF公用程式作業。 使用Java API，您可建立`PDFUtilityServiceClient`物件來完成此作業。 使用web service API，這是使用`PDFUtilityServiceService`物件來完成的。

**設定保存模式**

您可以選擇下列其中一個儲存選項：

* `INCREMENTAL`:以增量方式節省成本，以縮短節省成本的時間
* `FAST_WEB_VIEW`:儲存以快速檢視網頁
* `FULL`:使用完整儲存進行儲存（無最佳化）

**調用保存樣式操作**

建立服務客戶端後，可以調用屬性檢索操作。

**將PDF檔案傳遞至另一個AEM Forms作業**

一旦PDF公用程式服務設定指定的儲存模式後，將PDF檔案傳遞至另一個AEM Forms作業。 從該操作返回後，PDF文檔將以指定模式保存。 例如，如果您使用PDF公用程式服務來設定`FAST_WEB_VIEW`模式，然後將PDF檔案傳遞至加密服務的`encryptUsingPassword`操作，傳回的PDF檔案會以密碼加密，並儲存在`FAST_WEB_VIEW`模式中。

>[!NOTE]
>
>與本節關聯的快速入門會設定`FAST_WEB_VIEW`模式，然後將PDF檔案傳遞至加密服務的`encryptUsingPassword`操作。

**另請參閱**

[使用Java API設定PDF檔案儲存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[使用web service API設定PDF檔案儲存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#set-pdf-document-save-options-using-the-java-api}設定PDF檔案儲存選項

使用PDF公用程式API(Java)設定PDF檔案儲存選項：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`PDFUtilityServiceClient`對象。

1. 設定保存模式

   * 使用其建構子建立`PDFUtilitySaveMode`對象。
   * 通過調用`PDFUtilitySaveMode`對象的`setSaveStyle`方法並傳遞指定保存模式的字串值來設定保存模式。 例如，若要儲存以便快速檢視Web，請傳遞`FAST_WEB_VIEW`。

1. 調用保存樣式操作

   叫用`PDFUtilityServiceClient`物件的`setSaveMode`方法並傳遞下列值：

   * 代表PDF檔案的`com.adobe.idp.Document`物件。
   * `PDFUtilitySaveMode`物件，包含要使用的儲存樣式。
   * 用於確定是否覆蓋任何先前設定的布爾值。

   該方法返回使用指定保存樣式格式化的`com.adobe.idp.Document`對象。

1. 將PDF檔案傳遞至另一個AEM Forms作業

   * 將傳回的`com.adobe.idp.Document`物件傳遞至另一個AEM Forms作業。

**另請參閱**

[設定PDF檔案儲存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#set-pdf-document-save-options-using-the-web-service-api}設定PDF檔案儲存選項

使用PDF公用程式AP(web service)來設定PDF檔案儲存選項：

1. 包含專案檔案

   * 建立會使用PDF公用程式服務WSDL檔案的Microsoft .NET用戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立PDFUlitiveService用戶端

   使用proxy類別建構函式建立`PDFUtilityServiceService`物件。

1. 設定保存模式

   * 使用其建構子建立`PDFUtilitySaveMode`對象。
   * 通過為`PDFUtilitySaveMode`對象的`saveStyle`方法指定保存模式，來設定保存模式。 例如，若要儲存以快速檢視Web，請指定`FAST_WEB_VIEW`。

1. 調用保存樣式操作

   叫用`PDFUtilityServiceService`物件的`setSaveMode`方法並傳遞下列值：

   * 代表PDF檔案的`BLOB`物件。
   * `PDFUtilitySaveMode`物件，包含要使用的儲存樣式。
   * 用於確定是否覆蓋任何先前設定的布爾值。

   該方法返回使用指定保存樣式格式化的`BLOB`對象。 然後，您可以將該物件儲存為PDF檔案。

1. 將PDF檔案傳遞至另一個Forms作業

   * 將傳回的`BLOB`物件傳遞至另一個AEM Forms作業。

**另請參閱**

[設定PDF檔案儲存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 淨化PDF檔案{#sanitizing-pdf-documents}

您可以使用PDF公用程式Java API，以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>有關PDF實用程式服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-4}摘要

若要淨化PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立PDFUlitiveService用戶端。
1. 調用淨化操作。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 要使用Java建立客戶端應用程式，請包括必要的JAR檔案。

**建立PDFUlitiveService用戶端**

您必須先建立PDFUtilityService用戶端，才能以程式設計方式執行淨化作業。 使用Java API，您可建立`PDFUtilityServiceClient`物件來完成此作業。

**叫用PDF至XDP轉換作業**

建立服務客戶端後，可以調用淨化操作。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用web service API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#sanitize-pdf-documents-using-the-java-api}淨化PDF檔案

使用PDF公用程式API(Java)淨化檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUlitiveService用戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`PDFUtilityServiceClient`對象。

1. 叫用PDF至XDP轉換作業

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`convertPDFtoXDP`方法，並傳入代表PDF檔案的`com.adobe.idp.Document`物件。 該方法返回一個`com.adobe.idp.Document`對象，該對象表示新建立的XDP檔案。

**另請參閱**

[淨化PDF檔案](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
