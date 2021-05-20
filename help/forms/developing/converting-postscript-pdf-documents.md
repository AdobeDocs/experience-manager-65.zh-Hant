---
title: 將Postscript轉換為PDF檔案
seo-title: 將Postscript轉換為PDF檔案
description: 使用Distiller服務將PostScript®、Encapsuled PostScript(EPS)和PRN檔案轉換為通過網路壓縮、可靠且更安全的PDF檔案。 Distiller服務會將大量列印檔案轉換為電子檔案，例如使用Java API和Web服務API的發票和報表。
seo-description: 使用Distiller服務將PostScript®、Encapsuled PostScript(EPS)和PRN檔案轉換為通過網路壓縮、可靠且更安全的PDF檔案。 Distiller服務會將大量列印檔案轉換為電子檔案，例如使用Java API和Web服務API的發票和報表。
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# 將Postscript轉換為PDF文檔{#converting-postscript-to-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於Distiller服務{#about-the-distiller-service}

Distiller®服務可將PostScript®、封裝的PostScript(EPS)和PRN檔案轉換為通過網路壓縮、可靠且更安全的PDF檔案。 Distiller服務經常用於將大量印刷檔案轉換為電子檔案，如發票和報表。 將文檔轉換為PDF還允許企業向其客戶發送文檔的紙面版本和電子版本。

>[!NOTE]
>
>如需Distiller服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PostScript轉換為PDF文檔{#converting-postscript-to-pdf-documents-inner}

本主題說明如何使用Distiller服務API（Java和Web服務），以程式設計方式將PostScript(PS)、封裝的PostScript(EPS)和PRN檔案轉換為PDF檔案。

>[!NOTE]
>
>如需Distiller服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>若要將PostScript檔案轉換為PDF檔案，需在托管AEM Forms的伺服器上安裝下列其中一項：Acrobat 9或Microsoft Visual C++ 2005可再發行套件。

### 步驟{#summary-of-steps}的摘要

要將任何支援的類型轉換為PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立Distiller服務用戶端。
1. 擷取要轉換的檔案。
1. 調用PDF建立操作。
1. 保存PDF文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Distiller服務用戶端**

您必須先建立Distiller服務用戶端，才能以程式設計方式執行Distiller服務作業。 如果您使用Java API，請建立`DistillerServiceClient`物件。 如果您使用Web服務API，請建立`DistillerServiceService`物件。

**擷取要轉換的檔案**

必須檢索要轉換的檔案。 例如，要將PS檔案轉換為PDF文檔，必須檢索PS檔案。

**調用PDF建立操作**

建立服務客戶端後，可以調用PDF建立操作。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**儲存PDF檔案**

您可以將PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用Web服務API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API {#convert-a-postscript-file-to-pdf-using-the-java-api}將PostScript檔案轉換為PDF

使用Distiller服務API(Java)將PostScript檔案轉換為PDF檔案：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-distiller-client.jar。

1. 建立Distiller服務用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`DistillerServiceClient`物件。

1. 擷取要轉換的檔案。

   * 建立`java.io.FileInputStream`對象，該對象使用其建構子並傳遞一個指定檔案位置的字串值來表示要轉換的檔案。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 調用PDF建立操作。

   調用`DistillerServiceClient`對象的`createPDF`方法並傳遞以下值：

   * 表示要轉換的PS、EPS或PRN檔案的`com.adobe.idp.Document`對象
   * `java.lang.String`對象，包含要轉換的檔案的名稱
   * `java.lang.String`物件，包含要使用的Adobe PDF設定名稱
   * `java.lang.String`物件，包含要使用的安全設定名稱
   * 選用的`com.adobe.idp.Document`物件，包含產生PDF檔案時要套用的設定
   * 可選`com.adobe.idp.Document`對象，包含要應用於PDF文檔的元資料資訊

   `createPDF`方法返回一個`CreatePDFResult`對象，該對象包含新的PDF文檔和可生成的日誌檔案。 記錄檔通常包含轉換請求產生的錯誤或警告訊息。

1. 保存PDF文檔。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 調用`CreatePDFResult`對象的`getCreatedDocument`方法。 這會傳回`com.adobe.idp.Document`物件。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取PDF文檔。

   同樣，要獲取日誌文檔，請執行以下操作。

   * 調用`CreatePDFResult`對象的`getLogDocument`方法。 這會傳回`com.adobe.idp.Document`物件。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取日誌文檔。


**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將PostScript檔案轉換為PDF檔案](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#converting-a-postscript-file-to-pdf-using-the-web-service-api}將PostScript檔案轉換為PDF

使用Distiller服務API（Web服務）將PostScript檔案轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立Distiller服務用戶端。

   * 使用其預設建構子建立`DistillerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`DistillerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/DistillerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`DistillerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`DistillerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`DistillerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取要轉換的檔案。

   * 使用其建構子建立`BLOB`物件。 此`BLOB`對象用於儲存要轉換為PDF文檔的檔案。
   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示檔案位置和在中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 調用PDF建立操作。

   調用`DistillerServiceService`對象的`CreatePDF2`方法並傳遞以下必需值：

   * 表示要轉換的PS檔案的`BLOB`對象
   * 包含要轉換的檔案的路徑名的字串
   * 包含要使用的Adobe PDF設定的字串物件（例如`Standard`）
   * 包含要使用的安全設定的字串對象（例如`No Securit`y）
   * 選用的`BLOB`物件，包含產生PDF檔案時要套用的設定
   * 可選`BLOB`對象，包含要應用於PDF文檔的元資料資訊
   * 用於儲存PDF文檔的`BLOB`輸出參數
   * 用於儲存日誌的`BLOB`輸出參數

1. 保存PDF文檔。

   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存`CreatePDF2`方法（輸出參數）返回的`BLOB`對象的內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
