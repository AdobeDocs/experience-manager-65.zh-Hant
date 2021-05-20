---
title: 使用PDF公用程式
seo-title: 使用PDF公用程式
description: 使用PDF實用程式服務在PDF和XDP檔案格式之間轉換、設定和檢索PDF文檔屬性，以及操控XMP元資料。
seo-description: 使用PDF實用程式服務在PDF和XDP檔案格式之間轉換、設定和檢索PDF文檔屬性，以及操控XMP元資料。
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
source-wordcount: '2606'
ht-degree: 1%

---

# 使用PDF實用程式{#working-with-pdf-utilities}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於PDF公用程式服務**

PDF實用程式服務可在PDF和XDP檔案格式之間轉換、設定和擷取PDF檔案屬性，以及操控XMP中繼資料。 例如，在將PDF文檔轉換為其他格式之前，檢查其屬性以確定要為轉換調用的服務操作非常有用。

您可以使用PDF公用程式服務來完成下列工作：

* 將PDF檔案轉換為XDP檔案。
* 將XDP檔案轉換為PDF檔案。 （請參閱[將XDP文檔轉換為PDF文檔](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)。）
* 檢索PDF文檔屬性。 （請參閱[檢索PDF文檔屬性](pdf-utilities.md#retrieving-pdf-document-properties)。）
* 儲存PDF檔案並加以最佳化，以快速進行網頁檢視。 （請參閱[設定PDF文檔保存模式](pdf-utilities.md#setting-pdf-document-save-modes)。）

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PDF文檔轉換為XDP文檔{#converting-pdf-documents-into-xdp-documents}

您可以使用PDF公用程式Java和網頁服務API，以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}的摘要

要將PDF文檔轉換為XDP文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 叫用PDF到XDP轉換操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，可建立`PDFUtilityServiceClient`物件來完成。 若使用Web服務API，則可使用`PDFUtilityServiceService`物件來完成。

**叫用PDF到XDP轉換操作**

建立服務用戶端後，您可以叫用PDF至XDP轉換操作。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服務API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#convert-pdf-documents-into-xdp-documents-using-the-java-api}將PDF檔案轉換為XDP檔案

使用PDF實用程式API(Java)將PDF文檔轉換為XDP文檔：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`PDFUtilityServiceClient`物件。

1. 叫用PDF到XDP轉換操作

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`convertPDFtoXDP`方法，並傳入代表PDF檔案的`com.adobe.idp.Document`物件。 方法會傳回`com.adobe.idp.Document`物件，代表新建立的XDP檔案。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}將PDF檔案轉換為XDP檔案

使用PDF公用程式API（Web服務）將PDF檔案轉換為XDP檔案：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用PDF實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   使用代理類建構子建立`PDFUtilityServiceService`對象。

1. 叫用PDF到XDP轉換操作

   叫用`PDFUtilityServiceService`物件的`convertPDFtoXDP`方法，並傳入代表PDF檔案的`BLOB`物件。 方法會傳回`BLOB`物件，代表新建立的XDP檔案。

**另請參閱**

[將PDF檔案轉換為XDP檔案](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 將XDP文檔轉換為PDF文檔{#converting-xdp-documents-into-pdf-documents}

您可以使用PDF公用程式Java和網頁服務API，以程式設計方式將XDP檔案轉換為PDF檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}的摘要

要將XDP文檔轉換為PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 叫用XDP轉換為PDF操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，可建立`PDFUtilityServiceClient`物件來完成。 若使用Web服務API，則可使用`PDFUtilityServiceService`物件來完成。

**叫用XDP轉換為PDF操作**

建立服務用戶端後，您可以叫用XDP轉換為PDF操作。

**另請參閱**

[使用Java API將XDP檔案轉換為PDF檔案](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[使用Web服務API將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#convert-xdp-documents-into-pdf-documents-using-the-java-api}將XDP檔案轉換為PDF檔案

使用PDF公用程式API(Java)將XDP檔案轉換為PDF檔案：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`PDFUtilityServiceClient`物件。

1. 叫用XDP轉換為PDF操作

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`convertXDPtoPDF`方法，並傳入代表XDP檔案的`com.adobe.idp.Document`物件。 此方法會傳回`com.adobe.idp.Document`物件，代表新建立的PDF檔案。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}將XDP檔案轉換為PDF檔案

使用PDF公用程式API（網站服務API）將XDP檔案轉換為PDF檔案：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用PDF實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   使用代理類建構子建立`PDFUtilityServiceService`對象。

1. 叫用XDP轉換為PDF操作

   若要執行轉換，請叫用`PDFUtilityServiceService`物件的`convertXDPtoPDF`方法，並傳入代表XDP檔案的`BLOB`物件。 此方法會傳回`BLOB`物件，代表新建立的PDF檔案。

**另請參閱**

[將XDP檔案轉換為PDF檔案](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 檢索PDF文檔屬性{#retrieving-pdf-document-properties}

您可以使用PDF實用程式Java和Web服務API以寫程式方式檢索PDF文檔屬性，例如文檔是可填寫的表單還是讀取文檔所需的最低Acrobat版本。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟{#summary_of_steps-2}的摘要

要檢索PDF文檔屬性，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 調用屬性檢索操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，可建立`PDFUtilityServiceClient`物件來完成。 使用Web服務API，可使用`PDFUtilityServiceService`物件來完成。

**調用屬性檢索操作**

建立服務客戶端後，可以調用屬性檢索操作。

**另請參閱**

[使用Java API檢索PDF文檔屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[使用Web服務API檢索PDF文檔屬性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#retrieve-pdf-document-properties-using-the-java-api}檢索PDF文檔屬性

使用PDF實用程式API(Java)檢索PDF文檔屬性：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`PDFUtilityServiceClient`物件。

1. 調用屬性檢索操作

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`getPDFProperties`方法，並傳入下列內容：

   * 代表PDF文檔的`com.adobe.idp.Document`對象。
   * `PDFPropertiesOptionSpec`物件，包含要評估的屬性。

   方法會傳回包含查詢結果的`PDFPropertiesResult`物件。

**另請參閱**

[檢索PDF文檔屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#retrieve-pdf-document-properties-using-the-web-service-api}檢索PDF文檔屬性

使用PDF實用程式Web服務API檢索PDF文檔屬性：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用PDF實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   使用代理類建構子建立`PDFUtilityServiceService`對象。

1. 調用屬性檢索操作

   若要執行轉換，請叫用`PDFUtilityServiceService`物件的`getPDFProperties`方法，並傳入下列內容：

   * 代表PDF文檔的`BLOB`對象。
   * `PDFPropertiesOptionSpec`物件，包含要評估的屬性。

   方法會傳回包含查詢結果的`PDFPropertiesResult`物件。

**另請參閱**

[檢索PDF文檔屬性](pdf-utilities.md#retrieving-pdf-document-properties)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 設定PDF文檔保存模式{#setting-pdf-document-save-modes}

您可以使用PDF實用程式服務Java和Web服務API，以寫程式方式設定PDF檔案的儲存模式。 使用「PDF實用程式」服務設定儲存模式時，「PDF實用程式」服務只會設定儲存模式，實際上不會儲存PDF檔案。 PDF文檔在傳遞至其他服務操作時保存。 例如，您可以使用PDF實用程式服務來設定特定的儲存模式，並將其傳遞至加密服務，即實際儲存並加密PDF檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-3}的摘要

要設定PDF文檔的保存選項，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 設定儲存模式。
1. 調用保存操作。
1. 將PDF檔案傳遞至其他操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行PDF實用程式操作之前，必須建立PDFUtilityService客戶端。 使用Java API，可建立`PDFUtilityServiceClient`物件來完成。 使用Web服務API，可使用`PDFUtilityServiceService`物件來完成。

**設定「儲存」模式**

您可以選擇下列其中一個儲存選項：

* `INCREMENTAL`:以增量方式儲存以縮短儲存所需的時間
* `FAST_WEB_VIEW`:保存以快速查看Web
* `FULL`:使用完整儲存來儲存（無最佳化）

**調用保存樣式操作**

建立服務客戶端後，可以調用屬性檢索操作。

**將PDF檔案傳遞至另一個AEM Forms作業**

PDF實用程式服務設定指定的「儲存」模式後，請將PDF檔案傳遞至另一個AEM Forms操作。 從該操作返回後，PDF文檔將保存到指定模式。 例如，如果您使用PDF實用程式服務設定`FAST_WEB_VIEW`模式，然後將PDF文檔傳遞到加密服務的`encryptUsingPassword`操作，則返回的PDF文檔將使用密碼加密，並保存在`FAST_WEB_VIEW`模式中。

>[!NOTE]
>
>與此部分關聯的快速入門設定`FAST_WEB_VIEW`模式，然後將PDF文檔傳遞到加密服務的`encryptUsingPassword`操作。

**另請參閱**

[使用Java API設定PDF檔案儲存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[使用Web服務API設定PDF文檔保存選項](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用密碼加密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#set-pdf-document-save-options-using-the-java-api}設定PDF文檔保存選項

使用PDF實用程式API(Java)設定PDF文檔保存選項：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`PDFUtilityServiceClient`物件。

1. 設定「儲存」模式

   * 使用其建構子建立`PDFUtilitySaveMode`物件。
   * 通過調用`PDFUtilitySaveMode`對象的`setSaveStyle`方法並傳遞指定保存模式的字串值來設定保存模式。 例如，要保存以便快速查看Web，請傳遞`FAST_WEB_VIEW`。

1. 調用保存樣式操作

   調用`PDFUtilityServiceClient`對象的`setSaveMode`方法並傳遞以下值：

   * 代表PDF文檔的`com.adobe.idp.Document`對象。
   * `PDFUtilitySaveMode`物件，包含要使用的儲存樣式。
   * 用於確定是否覆蓋任何先前設定的布林值。

   此方法會傳回使用指定儲存樣式格式化的`com.adobe.idp.Document`物件。

1. 將PDF檔案傳遞至另一個AEM Forms作業

   * 將傳回的`com.adobe.idp.Document`物件傳遞至其他AEM Forms作業。

**另請參閱**

[設定PDF文檔保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#set-pdf-document-save-options-using-the-web-service-api}設定PDF文檔保存選項

使用PDF實用程式AP（Web服務）設定PDF文檔保存選項：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用PDF實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端程式集。

1. 建立PDFUtilityService客戶端

   使用代理類建構子建立`PDFUtilityServiceService`對象。

1. 設定「儲存」模式

   * 使用其建構子建立`PDFUtilitySaveMode`物件。
   * 通過為`PDFUtilitySaveMode`對象的`saveStyle`方法指定保存模式來指定字串值，來設定保存模式。 例如，要保存以便快速查看Web，請指定`FAST_WEB_VIEW`。

1. 調用保存樣式操作

   調用`PDFUtilityServiceService`對象的`setSaveMode`方法並傳遞以下值：

   * 代表PDF文檔的`BLOB`對象。
   * `PDFUtilitySaveMode`物件，包含要使用的儲存樣式。
   * 用於確定是否覆蓋任何先前設定的布林值。

   此方法會傳回使用指定儲存樣式格式化的`BLOB`物件。 然後，您可以將該物件儲存為PDF檔案。

1. 將PDF檔案傳遞至另一個Forms作業

   * 將傳回的`BLOB`物件傳遞至其他AEM Forms作業。

**另請參閱**

[設定PDF文檔保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 清理PDF文檔{#sanitizing-pdf-documents}

您可以使用PDF實用程式Java API以程式設計方式將PDF檔案轉換為XDP檔案。

>[!NOTE]
>
>如需PDF公用程式服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-4}的摘要

要處理PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDFUtilityService客戶端。
1. 調用淨化操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 要使用Java建立客戶端應用程式，請包括必要的JAR檔案。

**建立PDFUtilityService客戶端**

在以寫程式方式執行淨化操作之前，必須建立PDFUtilityService客戶端。 使用Java API，可建立`PDFUtilityServiceClient`物件來完成。

**叫用PDF到XDP轉換操作**

建立服務客戶端後，可以調用淨化操作。

**另請參閱**

[使用Java API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服務API將PDF檔案轉換為XDP檔案](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#sanitize-pdf-documents-using-the-java-api}處理PDF檔案

使用PDF公用程式API(Java)處理檔案：

1. 包含項目檔案

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-pdfutility-client.jar。

1. 建立PDFUtilityService客戶端

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`PDFUtilityServiceClient`物件。

1. 叫用PDF到XDP轉換操作

   若要執行轉換，請叫用`PDFUtilityServiceClient`物件的`convertPDFtoXDP`方法，並傳入代表PDF檔案的`com.adobe.idp.Document`物件。 方法會傳回`com.adobe.idp.Document`物件，代表新建立的XDP檔案。

**另請參閱**

[淨化PDF檔案](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
