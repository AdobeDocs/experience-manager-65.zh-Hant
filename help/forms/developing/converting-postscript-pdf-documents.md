---
title: 將Postscript轉換為PDF文檔
seo-title: Converting Postscript to PDF Documents
description: 使用Distiller服務將Encapsulated PostScript(EPS)和PRN檔案轉換為通過網路壓縮、可靠和更安全的PDF檔案。 Distiller服務使用Java API和Web服務API將大量打印文檔轉換為電子文檔，如發票和報表。
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

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 關於Distiller {#about-the-distiller-service}

Distiller®服務將PostScript®、封裝的PostScript(EPS)和PRN檔案通過網路轉換為緊湊、可靠和更安全的PDF檔案。 Distiller服務經常用於將大量打印檔案轉換成電子檔案，如發票和報表。 將文檔轉換為PDF還允許企業向其客戶發送文檔的紙面版本和電子版本。

>[!NOTE]
>
>有關Distiller服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PostScript轉換為PDF文檔 {#converting-postscript-to-pdf-documents-inner}

本主題介紹如何使用Distiller服務API（Java和Web服務）以寫程式方式將PostScript(PS)、封裝的PostScript(EPS)和PRN檔案轉換為PDF文檔。

>[!NOTE]
>
>有關Distiller服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>要將PostScript檔案轉換為PDF文檔，需要在承載AEM Forms的伺服器上安裝以下一項：Acrobat 9或MicrosoftVisual C++ 2005可再發行軟體包。

### 步驟摘要 {#summary-of-steps}

要將任何受支援的類型轉換為PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立Distiller服務客戶端。
1. 檢索要轉換的檔案。
1. 調用PDF建立操作。
1. 保存PDF文檔。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Distiller服務客戶端**

在以寫程式方式執行Distiller服務操作之前，必須建立Distiller服務客戶端。 如果使用Java API，請建立 `DistillerServiceClient` 的雙曲餘切值。 如果使用Web服務API，請建立 `DistillerServiceService` 的雙曲餘切值。

**檢索要轉換的檔案**

必須檢索要轉換的檔案。 例如，要將PS檔案轉換為PDF文檔，必須檢索PS檔案。

**調用PDF建立操作**

建立服務客戶端後，可以調用PDF建立操作。 此操作將需要有關要轉換的文檔的資訊，包括目標文檔的路徑。

**保存PDF文檔**

可以將PDF文檔另存為PDF檔案。

**另請參閱**

[使用Java API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用Web服務API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API將PostScript檔案轉換為PDF {#convert-a-postscript-file-to-pdf-using-the-java-api}

使用Distiller服務API(Java)將PostScript檔案轉換為PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案（如adobe-distiller-client.jar）。

1. 建立Distiller服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `DistillerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索要轉換的檔案。

   * 建立 `java.io.FileInputStream` 表示要轉換的檔案的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 調用PDF建立操作。

   調用 `DistillerServiceClient` 對象 `createPDF` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 表示要轉換的PS、EPS或PRN檔案的對象
   * A `java.lang.String` 包含要轉換的檔案名稱的對象
   * A `java.lang.String` 包含要使用的Adobe PDF設定名稱的對象
   * A `java.lang.String` 包含要使用的安全設定名稱的對象
   * 可選 `com.adobe.idp.Document` 包含生成PDF文檔時要應用的設定的對象
   * 可選 `com.adobe.idp.Document` 包含要應用到PDF文檔的元資料資訊的對象

   的 `createPDF` 方法返回 `CreatePDFResult` 包含新PDF文檔的對象和可能生成的日誌檔案。 日誌檔案通常包含由轉換請求生成的錯誤或警告消息。

1. 保存PDF文檔。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 調用 `CreatePDFResult` 對象 `getCreatedDocument` 的雙曲餘切值。 這返回 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取PDF文檔。

   同樣，要獲取日誌文檔，請執行以下操作。

   * 調用 `CreatePDFResult` 對象 `getLogDocument` 的雙曲餘切值。 這返回 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取日誌文檔。


**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API將PostScript檔案轉換為PDF文檔](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將PostScript檔案轉換為PDF {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

使用Distiller服務API（Web服務）將PostScript檔案轉換為PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立Distiller服務客戶端。

   * 建立 `DistillerServiceClient` 對象。
   * 建立 `DistillerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/DistillerService?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `DistillerServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `DistillerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `DistillerServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 檢索要轉換的檔案。

   * 建立 `BLOB` 對象。 此 `BLOB` 對象用於儲存要轉換為PDF文檔的檔案。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示檔案位置以及在中開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 調用PDF建立操作。

   調用 `DistillerServiceService` 對象 `CreatePDF2` 方法並傳遞以下所需值：

   * 的 `BLOB` 表示要轉換的PS檔案的對象
   * 包含要轉換的檔案的路徑名的字串
   * 包含要使用的Adobe PDF設定的字串對象(例如， `Standard`)
   * 包含要使用的安全設定的字串對象(例如， `No Securit`y)
   * 可選 `BLOB` 包含生成PDF文檔時要應用的設定的對象
   * 可選 `BLOB` 包含要應用到PDF文檔的元資料資訊的對象
   * A `BLOB` 用於儲存PDF文檔的輸出參數
   * A `BLOB` 用於儲存日誌的輸出參數

1. 保存PDF文檔。

   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `CreatePDF2` 方法（輸出參數）。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
