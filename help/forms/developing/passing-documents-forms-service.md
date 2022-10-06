---
title: 將檔案傳遞至FormsService
seo-title: Passing Documents to the FormsService
description: 將包含表單設計的com.adobe.idp.Document物件傳遞至Forms服務。 Forms服務會轉譯位於com.adobe.idp.Document物件中的表單設計。
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

# 將檔案傳遞至Forms服務 {#passing-documents-to-the-formsservice}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

AEM Forms服務會將互動式PDF forms轉譯給用戶端裝置（通常是網頁瀏覽器），以收集使用者的資訊。 互動式PDF表單以表單設計為基礎，通常會儲存為XDP檔案，並在Designer中建立。 從AEM Forms開始，您可以 `com.adobe.idp.Document` 包含Forms服務表單設計的物件。 接著，Forms服務會轉譯位於 `com.adobe.idp.Document` 物件。

傳遞 `com.adobe.idp.Document` 物件至Forms服務是指其他服務操作傳回 `com.adobe.idp.Document` 例項。 就是說，你可以 `com.adobe.idp.Document` 執行個體（從其他服務操作）並呈現。 例如，假設XDP檔案儲存在名為的內容服務（已廢止）節點中 `/Company Home/Form Designs`，如下圖所示。

您可以以程式設計方式從內容服務（已淘汰）擷取Loan.xdp，並將XDP檔案傳遞至Forms服務(位於 `com.adobe.idp.Document` 物件。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步驟摘要 {#summary-of-steps}

若要將從內容服務取得的檔案（已過時）（已過時）傳遞至Forms服務，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms和Document Management用戶端API物件。
1. 從內容服務擷取表單設計（已淘汰）。
1. 轉譯互動式PDF表單。
1. 對表單資料流執行動作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立Forms和Document Management用戶端API物件**

在以程式設計方式執行Forms服務API操作之前，請先建立Forms用戶端API物件。 此外，由於此工作流程會從內容服務擷取XDP檔案（已淘汰），因此請建立檔案管理API物件。

**從內容服務擷取表單設計（已淘汰）**

使用Java或Web服務API從內容服務擷取XDP檔案（已淘汰）。 在 `com.adobe.idp.Document` 例項(或 `BLOB` 例項（若您使用網站服務）。 然後，您就可以傳遞 `com.adobe.idp.Document` 例項至Forms服務。

**轉譯互動式PDF表單**

若要轉譯互動式表單，請傳遞 `com.adobe.idp.Document` 從內容服務（已淘汰）傳回至Forms服務的例項。

>[!NOTE]
>
>您可以傳遞 `com.adobe.idp.Document` 包含Forms服務的表單設計。 兩種新方法已命名 `renderPDFForm2` 和 `renderHTMLForm2` 接受 `com.adobe.idp.Document` 包含表單設計的物件。

**使用表單資料流執行動作**

根據客戶端應用程式的類型，您可以將表單寫入客戶端Web瀏覽器，或將表單另存為PDF檔案。 基於Web的應用程式通常會將表單寫入Web瀏覽器。 但是，案頭應用程式通常會將表單儲存為PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## 使用Java API將檔案傳遞至Forms服務 {#pass-documents-to-the-forms-service-using-the-java-api}

使用Forms服務和內容服務（已過時）API(Java)傳遞從內容服務取得的檔案（已過時）:

1. 包含項目檔案

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar和adobe-contentservices-client.jar。

1. 建立Forms和Document Management用戶端API物件

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 建立 `FormsServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。
   * 建立 `DocumentManagementServiceClientImpl` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 從內容服務擷取表單設計（已淘汰）

   叫用 `DocumentManagementServiceClientImpl` 物件 `retrieveContent` 方法，並傳遞下列值：

   * 一個字串值，它指定添加內容的儲存區。 預設商店為 `SpacesStore`. 此值是必要參數。
   * 指定要檢索的內容的完全限定路徑的字串值(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必要參數。
   * 指定版本的字串值。 此值是選用參數，您可以傳遞空白字串。 在此情況下，會擷取最新版本。

   此 `retrieveContent` 方法傳回 `CRCResult` 包含XDP檔案的物件。 取得 `com.adobe.idp.Document` 執行個體 `CRCResult` 物件 `getDocument` 方法。

1. 轉譯互動式PDF表單

   叫用 `FormsServiceClient` 物件 `renderPDFForm2` 方法，並傳遞下列值：

   * A `com.adobe.idp.Document` 包含從內容服務擷取的表單設計的物件（已淘汰）。
   * A `com.adobe.idp.Document` 包含要與表單合併資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 此值是選用參數，您可以指定 `null` 如果您不想指定執行時選項。
   * A `URLSpec` 包含URI值的對象。 此值是選用參數，您可以指定 `null`.
   * A `java.util.HashMap` 儲存檔案附件的物件。 此值是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 使用表單資料流執行動作

   * 建立 `com.adobe.idp.Document` 對象，方法是調用 `FormsResult` 物件s `getOutputContent` 方法。
   * 取得 `com.adobe.idp.Document` 對象 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 對象的內容類型，方法是調用 `setContentType` 方法，並傳遞 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 物件 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 對象，方法是調用 `com.adobe.idp.Document` 物件 `getInputStream` 方法。
   * 建立位元組陣列，並叫用 `InputStream` 物件 `read` 方法。 將位元組陣列傳遞為引數。
   * 叫用 `javax.servlet.ServletOutputStream` 物件 `write` 將表單資料流傳送至用戶端網頁瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將檔案傳遞至Forms服務](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API將檔案傳遞至Forms服務 {#pass-documents-to-the-forms-service-using-the-web-service-api}

使用Forms服務與內容服務（已過時）API（網站服務），傳遞從內容服務取得的檔案（已過時）:

1. 包含項目檔案

   建立使用MTOM的Microsoft .NET專案。 由於此客戶端應用程式調用了兩個AEM Forms服務，因此請建立兩個服務引用。 為與Forms服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   為與文檔管理服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   因為 `BLOB` 資料類型是兩個服務參考的共同類型，完全限定 `BLOB` 資料類型。 在相應的Web服務快速入門中，所有 `BLOB` 例項已完全限定。

   >[!NOTE]
   >
   >取代 `localhost`和托管AEM Forms之伺服器的IP位址。

1. 建立Forms和Document Management用戶端API物件

   * 建立 `FormsServiceClient` 物件，使用其預設建構函式。
   * 建立 `FormsServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/FormsService?WSDL`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `FormsServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `FormsServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >對 `DocumentManagementServiceClient`服務客戶端。

1. 從內容服務擷取表單設計（已淘汰）

   叫用 `DocumentManagementServiceClient` 物件 `retrieveContent` 方法並傳遞下列值：

   * 一個字串值，它指定添加內容的儲存區。 預設商店為 `SpacesStore`. 此值是必要參數。
   * 指定要檢索的內容的完全限定路徑的字串值(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必要參數。
   * 指定版本的字串值。 此值是選用參數，您可以傳遞空白字串。 在此情況下，會擷取最新版本。
   * 儲存瀏覽連結值的字串輸出參數。
   * A `BLOB` 儲存內容的輸出參數。 您可以使用此輸出參數來擷取內容。
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 儲存內容屬性的輸出參數。
   * A `CRCResult` 輸出參數。 您可以使用 `BLOB` 輸出參數來取得內容。

1. 轉譯互動式PDF表單

   叫用 `FormsServiceClient` 物件 `renderPDFForm2` 方法，並傳遞下列值：

   * A `BLOB` 包含從內容服務擷取的表單設計的物件（已淘汰）。
   * A `BLOB` 包含要與表單合併資料的物件。 如果您不想合併資料，請傳遞空白 `BLOB` 物件。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 此值是選用參數，您可以指定 `null` 如果您不想指定執行時選項。
   * A `URLSpec` 包含URI值的對象。 此值是選用參數，您可以指定 `null`.
   * A `Map` 儲存檔案附件的物件。 此值是選用參數，您可以指定 `null` 如果您不想將檔案附加到表單。
   * 用於儲存頁數的長輸出參數。
   * 用於儲存地區設定值的字串輸出參數。
   * A `FormsResult` 用於儲存交互PDF表單的輸出參數 `.`

   此 `renderPDFForm2` 方法傳回 `FormsResult` 包含互動式PDF表單的物件。

1. 使用表單資料流執行動作

   * 建立 `BLOB` 包含表單資料的物件，方法是取得 `FormsResult` 物件 `outputContent` 欄位。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示交互PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `BLOB` 從 `FormsResult` 物件。 取得 `BLOB` 物件 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
