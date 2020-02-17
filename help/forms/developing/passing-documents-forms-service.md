---
title: 將檔案傳送至FormsService
seo-title: 將檔案傳送至FormsService
description: 'null'
seo-description: 'null'
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 將檔案傳送至Forms服務 {#passing-documents-to-the-formsservice}

AEM Forms服務會將互動式PDF表單轉譯至用戶端裝置（通常是網頁瀏覽器），以收集使用者的資訊。 互動式PDF表格是以表格設計為基礎，通常會儲存為XDP檔案，並在Designer中建立。 從AEM Forms開始，您就可以將包含表 `com.adobe.idp.Document` 單設計的物件傳遞至Forms服務。 然後，Forms服務會轉譯位於物件中的表單 `com.adobe.idp.Document` 設計。

將物件傳遞至Forms `com.adobe.idp.Document` 服務的好處在於其他服務操作會傳回例 `com.adobe.idp.Document` 項。 也就是說，您可以從其他服務 `com.adobe.idp.Document` 操作中獲取實例並進行渲染。 例如，假設XDP檔案儲存在名為的Content Services（已過時）節點中， `/Company Home/Form Designs`如下圖所示。

您可以以程式設計方式從Content Services（已過時）（已過時）擷取Loan.xdp，並將XDP檔案傳遞至物件中的Forms服 `com.adobe.idp.Document` 務。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱「AEM Forms [的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

若要將從Content Services（已過時）（已過時）取得的檔案傳遞至Forms服務，請執行下列工作：

1. 包含專案檔案。
1. 建立表單和檔案管理用戶端API物件。
1. 從Content Services擷取表單設計（已過時）。
1. 轉換互動式PDF表單。
1. 對表單資料流執行動作。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立表單和檔案管理用戶端API物件**

在以程式設計方式執行Forms服務API操作之前，請先建立Forms Client API物件。 此外，由於此工作流程會從Content Services（不建議使用）擷取XDP檔案，因此請建立Document Management API物件。

**從Content services擷取表單設計（已過時）**

使用Java或web service API從Content Services（已過時）擷取XDP檔案。 XDP檔案會傳回至例 `com.adobe.idp.Document` 項(或是 `BLOB` 您使用web services的例項)。 然後，您可將執 `com.adobe.idp.Document` 行個體傳遞至Forms服務。

**轉換互動式PDF表單**

若要轉換互動式表單，請將 `com.adobe.idp.Document` 從Content Services（不建議使用）傳回的例項傳遞至Forms服務。

>[!NOTE]
>
>您可以將包含表 `com.adobe.idp.Document` 單設計的表單傳遞至Forms服務。 命名和接受包 `renderPDFForm2` 含表 `renderHTMLForm2` 單設 `com.adobe.idp.Document` 計的物件的兩種新方法。

**使用表單資料流執行動作**

視用戶端應用程式類型而定，您可將表單寫入用戶端網頁瀏覽器，或將表單儲存為PDF檔案。 網頁型應用程式通常會將表單寫入網頁瀏覽器。 不過，案頭應用程式通常會將表單儲存為PDF檔案。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## 使用Java API將檔案傳送至Forms Service {#pass-documents-to-the-forms-service-using-the-java-api}

使用Forms服務和Content Services（不建議使用）API(Java)傳遞從Content Services（不建議使用）取得的檔案：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar和adobe-contentservices-client.jar。

1. 建立表單和檔案管理用戶端API物件

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。 (請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。
   * 使用其 `DocumentManagementServiceClientImpl` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 從Content services擷取表單設計（已過時）

   叫用物 `DocumentManagementServiceClientImpl` 件的方 `retrieveContent` 法並傳遞下列值：

   * 一個字串值，它指定添加內容的儲存。 預設商店為 `SpacesStore`。 此值為必要參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑(例如 `/Company Home/Form Designs/Loan.xdp`)。 此值為必要參數。
   * 指定版本的字串值。 此值為可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。
   該方 `retrieveContent` 法返回包 `CRCResult` 含XDP檔案的對象。 調用 `com.adobe.idp.Document` 物件的方法 `CRCResult` 以取得例 `getDocument` 項。

1. 轉換互動式PDF表單

   叫用物 `FormsServiceClient` 件的方 `renderPDFForm2` 法並傳遞下列值：

   * 包 `com.adobe.idp.Document` 含從Content services擷取的表單設計（已過時）的物件。
   * 包 `com.adobe.idp.Document` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞空 `com.adobe.idp.Document` 物件。
   * 存 `PDFFormRenderSpec` 儲運行時選項的對象。 此值為可選參數，您可以指 `null` 定是否不想指定執行時選項。
   * 包 `URLSpec` 含URI值的對象。 此值是可選參數，您可以指定 `null`。
   * 儲存 `java.util.HashMap` 檔案附件的對象。 此值是可選參數，您可以指 `null` 定是否不要將檔案附加到表單。
   該方 `renderPDFForm` 法返回包 `FormsResult` 含必須寫入客戶端Web瀏覽器的表單資料流的對象。

1. 使用表單資料流執行動作

   * 通過調 `com.adobe.idp.Document` 用對象的方法 `FormsResult` 建立對 `getOutputContent` 像。
   * 通過調用對象的方 `com.adobe.idp.Document` 法來獲取對象的內 `getContentType` 容類型。
   * 調用 `javax.servlet.http.HttpServletResponse` 物件的方法並傳遞物件的內 `setContentType` 容類型，以設定物件的內容 `com.adobe.idp.Document` 類型。
   * 呼叫 `javax.servlet.ServletOutputStream` 物件的方法，建立用於將表單資料串流寫入用戶端Web `javax.servlet.http.HttpServletResponse` 瀏覽器的物 `getOutputStream` 件。
   * 調用 `java.io.InputStream` 物件的方 `com.adobe.idp.Document` 法以建立物 `getInputStream` 件。
   * 建立位元組陣列，並透過叫用物件的方法，以表單資料 `InputStream` 流填入該 `read` 陣列。 將位元組陣列作為引數傳遞。
   * 叫用物 `javax.servlet.ServletOutputStream` 件的方 `write` 法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將檔案傳送至Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API將檔案傳遞至Forms Service {#pass-documents-to-the-forms-service-using-the-web-service-api}

使用Forms服務和Content Services（不建議使用）API(web service)傳遞從Content Services（不建議使用）取得的檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 由於此用戶端應用程式會叫用兩個AEM Forms服務，因此請建立兩個服務參考。 對與Forms服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   對與「文檔管理」服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   由於兩 `BLOB` 個服務引用都使用資料類型，因此在使用資料類 `BLOB` 型時完全限定該資料類型。 在對應的Web服務快速啟動中，所有實例 `BLOB` 都完全限定。

   >[!NOTE]
   >
   >以代 `localhost`管AEM Forms之伺服器的IP位址取代。

1. 建立表單和檔案管理用戶端API物件

   * 使用其 `FormsServiceClient` 預設建構函式建立物件。
   * 使用建 `FormsServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/FormsService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `FormsServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `FormsServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `FormsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。
   >[!NOTE]
   >
   >對服務客戶端重複 `DocumentManagementServiceClient`這些步驟。

1. 從Content services擷取表單設計（已過時）

   叫用物件的方 `DocumentManagementServiceClient` 法並傳 `retrieveContent` 遞下列值，以擷取內容：

   * 一個字串值，它指定添加內容的儲存。 預設商店為 `SpacesStore`。 此值為必要參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑(例如 `/Company Home/Form Designs/Loan.xdp`)。 此值為必要參數。
   * 指定版本的字串值。 此值為可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。
   * 儲存瀏覽連結值的字串輸出參數。
   * 儲存 `BLOB` 內容的輸出參數。 您可以使用此輸出參數來擷取內容。
   * 儲存 `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 內容屬性的輸出參數。
   * 輸出 `CRCResult` 參數。 您可以使用輸出參數來取得內容，而 `BLOB` 非使用此物件。

1. 轉換互動式PDF表單

   叫用物 `FormsServiceClient` 件的方 `renderPDFForm2` 法並傳遞下列值：

   * 包 `BLOB` 含從Content services擷取的表單設計（已過時）的物件。
   * 包 `BLOB` 含要與表單合併的資料的對象。 如果您不想合併資料，請傳遞空 `BLOB` 物件。
   * 存 `PDFFormRenderSpec` 儲運行時選項的對象。 此值為可選參數，您可以指 `null` 定是否不想指定執行時選項。
   * 包 `URLSpec` 含URI值的對象。 此值是可選參數，您可以指定 `null`。
   * 儲存 `Map` 檔案附件的對象。 此值是可選參數，您可以指 `null` 定是否不要將檔案附加到表單。
   * 用於儲存頁數的長輸出參數。
   * 用於儲存地區值的字串輸出參數。
   * 用 `FormsResult` 來儲存互動式PDF表單的輸出參數 `.`
   此方 `renderPDFForm2` 法會傳回包 `FormsResult` 含互動式PDF表單的物件。

1. 使用表單資料流執行動作

   * 透過 `BLOB` 取得物件欄位的值，建立包含表單資 `FormsResult` 料的物 `outputContent` 件。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表互動式PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，該陣列儲存從對 `BLOB` 像檢索到的對象的 `FormsResult` 內容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
