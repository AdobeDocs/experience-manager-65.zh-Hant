---
title: 將Postscript轉換為PDF檔案
description: 使用Distiller服務將PostScript®、封裝的PostScript (EPS)和PRN檔案轉換為透過網路的精簡、可靠且更安全的PDF檔案。 Distiller服務使用Java API和Web服務API將大量列印檔案轉換為電子檔案，例如發票和對帳單。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# 將Postscript轉換為PDF檔案 {#converting-postscript-to-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於Distiller服務 {#about-the-distiller-service}

Distiller®服務可將PostScript®、封裝式PostScript (EPS)和PRN檔案轉換為透過網路的精簡、可靠且更安全的PDF檔案。 Distiller服務通常用於將大量列印檔案轉換為電子檔案，例如發票和結算單。 將檔案轉換為PDF也可讓企業向客戶傳送檔案的書面版本和電子版本。

>[!NOTE]
>
>如需Distiller服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將PostScript轉換為PDF檔案 {#converting-postscript-to-pdf-documents-inner}

本主題說明如何使用Distiller服務API （Java和Web服務）以程式設計方式將PostScript (PS)、封裝的PostScript (EPS)和PRN檔案轉換為PDF檔案。

>[!NOTE]
>
>如需Distiller服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>若要將PostScript檔案轉換為PDF檔案，必須在託管AEM Forms的伺服器上安裝下列其中一項： Acrobat 9或Microsoft Visual C++ 2005可轉散發套件。

### 步驟摘要 {#summary-of-steps}

若要將任何支援的型別轉換成PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Distiller服務使用者端。
1. 擷取要轉換的檔案。
1. 叫用PDF建立作業。
1. 儲存PDF檔案。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Distiller服務使用者端**

您必須先建立Distiller服務使用者端，才能以程式設計方式執行Distiller服務作業。 如果您使用Java API，請建立`DistillerServiceClient`物件。 如果您使用網站服務API，請建立`DistillerServiceService`物件。

**擷取要轉換的檔案**

擷取您要轉換的檔案。 例如，若要將PS檔案轉換為PDF檔案，您必須擷取PS檔案。

**叫用PDF建立作業**

建立服務使用者端後，您可以叫用PDF建立作業。 此操作需要有關要轉換檔案的資訊，包括目標檔案的路徑。

**儲存PDF檔案**

您可以將PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用網站服務API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API將PostScript檔案轉換為PDF {#convert-a-postscript-file-to-pdf-using-the-java-api}

使用PostScript Service API (Java)將Distiller檔案轉換為PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-distiller-client.jar。

1. 建立Distiller服務使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DistillerServiceClient`物件。

1. 擷取要轉換的檔案。

   * 建立一個`java.io.FileInputStream`物件，代表要轉換的檔案，使用它的建構函式並傳遞字串值來指定檔案的位置。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 叫用PDF建立作業。

   叫用`DistillerServiceClient`物件的`createPDF`方法，並傳遞下列值：

   * 代表要轉換之PS、EPS或PRN檔案的`com.adobe.idp.Document`物件
   * 包含要轉換之檔案名稱的`java.lang.String`物件
   * 包含要使用的Adobe PDF設定名稱的`java.lang.String`物件
   * 包含要使用的安全性設定名稱的`java.lang.String`物件
   * 選擇性的`com.adobe.idp.Document`物件，其中包含產生PDF檔案時要套用的設定
   * 包含要套用至PDF檔案之中繼資料資訊的可選`com.adobe.idp.Document`物件

   `createPDF`方法傳回包含新PDF檔案及可產生的記錄檔的`CreatePDFResult`物件。 記錄檔通常包含轉換請求產生的錯誤或警告訊息。

1. 儲存PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用`CreatePDFResult`物件的`getCreatedDocument`方法。 這會傳回`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

   同樣地，若要取得日誌檔案，請執行下列動作。

   * 叫用`CreatePDFResult`物件的`getLogDocument`方法。 這會傳回`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取記錄檔案。

**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速入門(SOAP模式)：使用Java API將PostScript檔案轉換為PDF檔案](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將PostScript檔案轉換為PDF {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

使用PostScript服務API （Web服務）將Distiller檔案轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立Distiller服務使用者端。

   * 使用預設建構函式建立`DistillerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`DistillerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/DistillerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 但是，請指定`?blob=mtom`以使用MTOM。
   * 取得`DistillerServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`DistillerServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`DistillerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取要轉換的檔案。

   * 使用物件的建構函式建立`BLOB`物件。 此`BLOB`物件用來儲存要轉換成PDF檔案的檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表檔案位置和開啟檔案模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。

1. 叫用PDF建立作業。

   叫用`DistillerServiceService`物件的`CreatePDF2`方法，並傳遞下列必要值：

   * 代表要轉換之PS檔案的`BLOB`物件
   * 包含要轉換之檔案的路徑名稱的字串
   * 包含要使用的Adobe PDF設定的字串物件（例如，`Standard`）
   * 字串物件包含要使用的安全性設定（例如，`No Securit`y）
   * 選擇性的`BLOB`物件，其中包含產生PDF檔案時要套用的設定
   * 包含要套用至PDF檔案之中繼資料資訊的可選`BLOB`物件
   * 用來儲存PDF檔案的`BLOB`輸出引數
   * 用來儲存記錄檔的`BLOB`輸出引數

1. 儲存PDF檔案。

   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表已簽署PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存`CreatePDF2`方法（輸出引數）傳回的`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
