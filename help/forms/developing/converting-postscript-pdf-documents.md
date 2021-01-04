---
title: 將Postscript轉換為PDF檔案
seo-title: 將Postscript轉換為PDF檔案
description: 使用Distiller服務，將PostScript®、Encapsuled PostScript(EPS)和PRN檔案轉換為精簡、可靠且更安全的網路PDF檔案。 Distiller服務使用Java API和Web Service API將大量打印文檔轉換為電子文檔，如發票和對帳單。
seo-description: 使用Distiller服務，將PostScript®、Encapsuled PostScript(EPS)和PRN檔案轉換為精簡、可靠且更安全的網路PDF檔案。 Distiller服務使用Java API和Web Service API將大量打印文檔轉換為電子文檔，如發票和對帳單。
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---


# 將Postscript轉換為PDF檔案{#converting-postscript-to-pdf-documents}

## 關於Distiller服務{#about-the-distiller-service}

Distiller®服務可將PostScript®、Encapsulated PostScript(EPS)和PRN檔案透過網路轉換為精簡、可靠且更安全的PDF檔案。 Distiller服務常用於將大量打印文檔轉換為電子文檔，如發票和對帳單。 將檔案轉換為PDF也讓企業可以傳送書面版本和電子版檔案給客戶。

>[!NOTE]
>
>有關Distiller服務的詳細資訊，請參閱[Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PostScript轉換為PDF檔案{#converting-postscript-to-pdf-documents-inner}

本主題說明如何使用Distiller Service API（Java和web service）以程式設計方式將PostScript(PS)、封裝的PostScript(EPS)和PRN檔案轉換為PDF檔案。

>[!NOTE]
>
>有關Distiller服務的詳細資訊，請參閱[Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>若要將PostScript檔案轉換為PDF檔案，下列其中一項需要安裝在代管AEM Forms的伺服器上：Acrobat 9或Microsoft Visual C++ 2005可重新散發的套件。

### 步驟{#summary-of-steps}摘要

若要將任何支援的類型轉換為PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Distiller服務客戶端。
1. 擷取要轉換的檔案。
1. 叫用PDF建立作業。
1. 儲存PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Distiller服務客戶端**

在以寫程式方式執行Distiller服務操作之前，必須建立Distiller服務客戶端。 如果您使用Java API，請建立`DistillerServiceClient`物件。 如果您使用web service API，請建立`DistillerServiceService`物件。

**擷取要轉換的檔案**

必須檢索要轉換的檔案。 例如，若要將PS檔案轉換為PDF檔案，您必須擷取PS檔案。

**叫用PDF建立作業**

建立服務用戶端後，您就可以叫用PDF建立作業。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**儲存PDF檔案**

您可將PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用web service API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API {#convert-a-postscript-file-to-pdf-using-the-java-api}將PostScript檔案轉換為PDF

使用Distiller Service API(Java)將PostScript檔案轉換為PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-distiller-client.jar。

1. 建立Distiller服務客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`DistillerServiceClient`對象。

1. 擷取要轉換的檔案。

   * 建立一個`java.io.FileInputStream`對象，該對象表示要轉換的檔案，方法是使用其建構子並傳遞一個字串值，該字串值指定檔案的位置。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 叫用PDF建立作業。

   叫用`DistillerServiceClient`物件的`createPDF`方法並傳遞下列值：

   * 代表要轉換的PS、EPS或PRN檔案的`com.adobe.idp.Document`對象
   * `java.lang.String`對象，包含要轉換的檔案名
   * `java.lang.String`物件，其中包含要使用的Adobe PDF設定名稱
   * `java.lang.String`物件，其中包含要使用的安全設定名稱
   * 可選`com.adobe.idp.Document`物件，包含在產生PDF檔案時要套用的設定
   * 可選`com.adobe.idp.Document`物件，包含要套用至PDF檔案的中繼資料資訊

   `createPDF`方法返回包含新PDF文檔的`CreatePDFResult`對象和可能生成的日誌檔案。 日誌檔案通常包含由轉換請求生成的錯誤或警告消息。

1. 儲存PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用`CreatePDFResult`物件的`getCreatedDocument`方法。 這會傳回`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

   同樣，要獲取日誌文檔，請執行以下操作。

   * 叫用`CreatePDFResult`物件的`getLogDocument`方法。 這會傳回`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取記錄檔。


**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將PostScript檔案轉換為PDF檔案](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#converting-a-postscript-file-to-pdf-using-the-web-service-api}將PostScript檔案轉換為PDF

使用Distiller Service API(web service)將PostScript檔案轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立Distiller服務客戶端。

   * 使用其預設建構子建立`DistillerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`DistillerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/DistillerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`DistillerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`DistillerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`DistillerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取要轉換的檔案。

   * 使用其建構子建立`BLOB`對象。 此`BLOB`物件用來儲存檔案，以轉換為PDF檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的&lt;a1/>屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 叫用PDF建立作業。

   叫用`DistillerServiceService`物件的`CreatePDF2`方法並傳遞下列必要值：

   * 代表要轉換的PS檔案的`BLOB`對象
   * 包含要轉換的檔案路徑名的字串
   * 包含要使用的Adobe PDF設定的字串物件（例如`Standard`）
   * 包含要使用的安全設定的字串對象（例如`No Securit`y）
   * 可選`BLOB`物件，包含在產生PDF檔案時要套用的設定
   * 可選`BLOB`物件，包含要套用至PDF檔案的中繼資料資訊
   * 用於儲存PDF文檔的`BLOB`輸出參數
   * 用於儲存日誌的`BLOB`輸出參數

1. 儲存PDF檔案。

   * 通過調用`System.IO.FileStream`對象的建構子建立&lt;a0/>對象。 傳遞一個字串值，代表已簽署PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存`CreatePDF2`方法（輸出參數）返回的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立&lt;a0/>對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
