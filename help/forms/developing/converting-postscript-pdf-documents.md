---
title: 將Postscript轉換為PDF文檔
seo-title: Converting Postscript to PDF Documents
description: 使用Distiller服務將PostScript®、Encapsuled PostScript(EPS)和PRN檔案轉換為通過網路壓縮、可靠且更安全的PDF檔案。 Distiller服務會將大量列印檔案轉換為電子檔案，例如使用Java API和Web服務API的發票和報表。
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
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
source-wordcount: '1325'
ht-degree: 0%

---

# 將Postscript轉換為PDF文檔 {#converting-postscript-to-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於Distiller服務 {#about-the-distiller-service}

Distiller®服務通過網路將PostScript®、Encapsuled PostScript(EPS)和PRN檔案轉換為精簡、可靠且更安全的PDF檔案。 Distiller服務經常用於將大量印刷檔案轉換為電子檔案，如發票和報表。 將文檔轉換為PDF還允許企業向其客戶發送文檔的紙面版本和電子版本。

>[!NOTE]
>
>如需Distiller服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將PostScript轉換為PDF文檔 {#converting-postscript-to-pdf-documents-inner}

本主題說明如何使用Distiller服務API（Java和Web服務），以程式設計方式將PostScript(PS)、封裝的PostScript(EPS)和PRN檔案轉換為PDF文檔。

>[!NOTE]
>
>如需Distiller服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>若要將PostScript檔案轉換為PDF檔案，必須在托管AEM Forms的伺服器上安裝下列其中一項：Acrobat 9或Microsoft Visual C++ 2005可再發行套件。

### 步驟摘要 {#summary-of-steps}

要將任何支援的類型轉換為PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立Distiller服務用戶端。
1. 擷取要轉換的檔案。
1. 調用PDF建立操作。
1. 保存PDF文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Distiller服務用戶端**

您必須先建立Distiller服務用戶端，才能以程式設計方式執行Distiller服務作業。 如果您使用Java API，請建立 `DistillerServiceClient` 物件。 如果您使用網站服務API，請建立 `DistillerServiceService` 物件。

**擷取要轉換的檔案**

必須檢索要轉換的檔案。 例如，要將PS檔案轉換為PDF文檔，必須檢索PS檔案。

**調用PDF建立操作**

建立服務客戶端後，可以調用PDF建立操作。 此操作需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**保存PDF文檔**

可以將PDF文檔另存為PDF檔案。

**另請參閱**

[使用Java API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用網站服務API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API將PostScript檔案轉換為PDF {#convert-a-postscript-file-to-pdf-using-the-java-api}

使用Distiller服務API(Java)將PostScript檔案轉換為PDF檔案：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-distiller-client.jar。

1. 建立Distiller服務用戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DistillerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 擷取要轉換的檔案。

   * 建立 `java.io.FileInputStream` 使用其建構子並傳遞指定檔案位置的字串值來表示要轉換的檔案的對象。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 調用PDF建立操作。

   叫用 `DistillerServiceClient` 物件 `createPDF` 方法，並傳遞下列值：

   * 此 `com.adobe.idp.Document` 表示要轉換的PS、EPS或PRN檔案的對象
   * A `java.lang.String` 包含要轉換的檔案名稱的對象
   * A `java.lang.String` 包含要使用的Adobe PDF設定名稱的物件
   * A `java.lang.String` 包含要使用的安全設定名稱的對象
   * 可選 `com.adobe.idp.Document` 包含在生成PDF文檔時要應用的設定的對象
   * 可選 `com.adobe.idp.Document` 包含要應用到PDF文檔的元資料資訊的對象

   此 `createPDF` 方法傳回 `CreatePDFResult` 包含新PDF文檔的對象和可生成的日誌檔案。 記錄檔通常包含轉換請求產生的錯誤或警告訊息。

1. 保存PDF文檔。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 叫用 `CreatePDFResult` 物件 `getCreatedDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取PDF檔案。

   同樣，要獲取日誌文檔，請執行以下操作。

   * 叫用 `CreatePDFResult` 物件 `getLogDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取記錄檔。


**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API將PostScript檔案轉換為PDF檔案](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將PostScript檔案轉換為PDF {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

使用Distiller服務API（網站服務）將PostScript檔案轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

1. 建立Distiller服務用戶端。

   * 建立 `DistillerServiceClient` 物件，使用其預設建構函式。
   * 建立 `DistillerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 來使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DistillerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取要轉換的檔案。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存要轉換為PDF文檔的檔案。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示檔案位置和在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。

1. 調用PDF建立操作。

   叫用 `DistillerServiceService` 物件 `CreatePDF2` 方法，並傳遞下列必要值：

   * 此 `BLOB` 表示要轉換的PS檔案的對象
   * 包含要轉換的檔案的路徑名的字串
   * 包含要使用的Adobe PDF設定的字串物件(例如 `Standard`)
   * 包含要使用的安全設定的字串物件(例如 `No Securit`y)
   * 可選 `BLOB` 包含在生成PDF文檔時要應用的設定的對象
   * 可選 `BLOB` 包含要應用到PDF文檔的元資料資訊的對象
   * A `BLOB` 用於儲存PDF文檔的輸出參數
   * A `BLOB` 用於儲存日誌的輸出參數

1. 保存PDF文檔。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `CreatePDF2` 方法（輸出參數）。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
