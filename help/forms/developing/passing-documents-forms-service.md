---
title: 將文檔傳遞到FormsService
seo-title: Passing Documents to the FormsService
description: 將包含表單設計的com.adobe.idp.Document對象傳遞給Forms服務。 Forms服務呈現位於com.adobe.idp.Document對象中的窗體設計。
seo-description: Pass a com.adobe.idp.Document object that contains the form design to the Forms service. The Forms service renders the form design located in the com.adobe.idp.Document object.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 0%

---

# 將檔案轉給Forms {#passing-documents-to-the-formsservice}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

AEM Forms服務向客戶端設備（通常是web瀏覽器）提供互動式PDF forms，以從用戶收集資訊。 互動式PDF表單基於通常另存為XDP檔案並在設計器中建立的表單設計。 在AEM Forms，你可以通過 `com.adobe.idp.Document` 包含Forms服務的窗體設計的對象。 然後，Forms服務會在 `com.adobe.idp.Document` 的雙曲餘切值。

通過 `com.adobe.idp.Document` 對Forms服務的對象是其他服務操作返回 `com.adobe.idp.Document` 實例。 就是說，你可以 `com.adobe.idp.Document` 實例，並呈現它。 例如，假定XDP檔案儲存在名為「Content Services（不建議使用）」的節點中 `/Company Home/Form Designs`，如下圖所示。

您可以以寫程式方式從Content Services（不建議使用）中檢索Loan.xdp（已棄用），並將XDP檔案傳遞到Forms服務 `com.adobe.idp.Document` 的雙曲餘切值。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

要將從Content Services（棄用）（棄用）獲取的文檔傳遞到Forms服務，請執行以下任務：

1. 包括項目檔案。
1. 建立Forms和文檔管理客戶端API對象。
1. 從Content Services檢索表單設計（不建議使用）。
1. 呈現互動式PDF窗體。
1. 對表單資料流執行操作。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立Forms和文檔管理客戶端API對象**

在以寫程式方式執行Forms服務API操作之前，請建立一個Forms客戶端API對象。 此外，由於此工作流從Content Services（不建議使用）檢索XDP檔案，因此請建立Document Management API對象。

**從Content Services檢索表單設計（不建議使用）**

使用Java或Web服務API從Content Services（不建議使用）檢索XDP檔案。 在 `com.adobe.idp.Document` 實例(或 `BLOB` 實例)。 然後，您可以 `com.adobe.idp.Document` 向Forms局舉報。

**呈現互動式PDF窗體**

要呈現互動式窗體，請傳遞 `com.adobe.idp.Document` 從Content Services（不建議使用）返回到Forms服務的實例。

>[!NOTE]
>
>你可以通過 `com.adobe.idp.Document` 包含Forms服務的表格設計。 兩種新方法名為 `renderPDFForm2` 和 `renderHTMLForm2` 接受 `com.adobe.idp.Document` 包含窗體設計的對象。

**對表單資料流執行操作**

根據客戶端應用程式的類型，您可以將表單寫入客戶端Web瀏覽器或將表單另存為PDF檔案。 基於Web的應用程式通常將表單寫入Web瀏覽器。 但是，案頭應用程式通常將表單另存為PDF檔案。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## 使用Java API將文檔傳遞到Forms服務 {#pass-documents-to-the-forms-service-using-the-java-api}

使用Forms服務和Content Services（棄用）API(Java)傳遞從Content Services（棄用）獲取的文檔：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar和adobe-contentservices-client.jar。

1. 建立Forms和文檔管理客戶端API對象

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。
   * 建立 `DocumentManagementServiceClientImpl` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 從Content Services檢索表單設計（不建議使用）

   調用 `DocumentManagementServiceClientImpl` 對象 `retrieveContent` 方法並傳遞以下值：

   * 一個字串值，它指定添加內容的儲存。 預設儲存為 `SpacesStore`。 此值是必需參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需參數。
   * 指定版本的字串值。 此值是可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。

   的 `retrieveContent` 方法返回 `CRCResult` 包含XDP檔案的對象。 獲取 `com.adobe.idp.Document` 實例 `CRCResult` 對象 `getDocument` 的雙曲餘切值。

1. 呈現互動式PDF窗體

   調用 `FormsServiceClient` 對象 `renderPDFForm2` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 包含從Content Services檢索到的表單設計的對象（不建議使用）。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `com.adobe.idp.Document` 的雙曲餘切值。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 此值是可選參數，您可以指定 `null` 選項。
   * A `URLSpec` 包含URI值的對象。 此值是可選參數，您可以指定 `null`。
   * A `java.util.HashMap` 儲存檔案附件的對象。 此值是可選參數，您可以指定 `null` 的子菜單。

   的 `renderPDFForm` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 對表單資料流執行操作

   * 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
   * 獲取的內容類型 `com.adobe.idp.Document` 通過調用對象 `getContentType` 的雙曲餘切值。
   * 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
   * 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
   * 通過調用 `InputStream` 對象 `read` 的雙曲餘切值。 將位元組陣列作為參數傳遞。
   * 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API將文檔傳遞到Forms服務](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API將文檔傳遞給Forms服務 {#pass-documents-to-the-forms-service-using-the-web-service-api}

使用Forms服務和Content Services（棄用）API（Web服務）傳遞從Content Services（棄用）獲取的文檔：

1. 包括項目檔案

   建立使用MTOM的Microsoft.NET項目。 由於此客戶端應用程式調用兩個AEM Forms服務，因此建立兩個服務引用。 對與Forms服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   對與文檔管理服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   因為 `BLOB` 資料類型是兩種服務引用的公用類型，完全限定 `BLOB` 資料類型。 在相應的Web服務快速啟動中， `BLOB` 實例完全限定。

   >[!NOTE]
   >
   >替換 `localhost`IP地址為AEM Forms。

1. 建立Forms和文檔管理客戶端API對象

   * 建立 `FormsServiceClient` 對象。
   * 建立 `FormsServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/FormsService?WSDL`)。 你不需要 `lc_version` 屬性。 在建立服務引用時使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `FormsServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `FormsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `FormsServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對 `DocumentManagementServiceClient`服務客戶端。

1. 從Content Services檢索表單設計（不建議使用）

   通過調用 `DocumentManagementServiceClient` 對象 `retrieveContent` 方法並傳遞以下值：

   * 一個字串值，它指定添加內容的儲存。 預設儲存為 `SpacesStore`。 此值是必需參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需參數。
   * 指定版本的字串值。 此值是可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。
   * 儲存瀏覽連結值的字串輸出參數。
   * A `BLOB` 儲存內容的輸出參數。 可以使用此輸出參數檢索內容。
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 儲存內容屬性的輸出參數。
   * A `CRCResult` 輸出參數。 您可以使用 `BLOB` 輸出參數以獲取內容。

1. 呈現互動式PDF窗體

   調用 `FormsServiceClient` 對象 `renderPDFForm2` 方法並傳遞以下值：

   * A `BLOB` 包含從Content Services檢索到的表單設計的對象（不建議使用）。
   * A `BLOB` 包含要與窗體合併的資料的對象。 如果不想合併資料，請傳遞一個空 `BLOB` 的雙曲餘切值。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 此值是可選參數，您可以指定 `null` 選項。
   * A `URLSpec` 包含URI值的對象。 此值是可選參數，您可以指定 `null`。
   * A `Map` 儲存檔案附件的對象。 此值是可選參數，您可以指定 `null` 的子菜單。
   * 用於儲存頁數的長輸出參數。
   * 用於儲存區域設定值的字串輸出參數。
   * A `FormsResult` 用於儲存交互PDF窗體的輸出參數 `.`

   的 `renderPDFForm2` 方法返回 `FormsResult` 包含互動式PDF窗體的對象。

1. 對表單資料流執行操作

   * 建立 `BLOB` 包含表單資料的對象，方法是獲取 `FormsResult` 對象 `outputContent` 的子菜單。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示互動式PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 從 `FormsResult` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
