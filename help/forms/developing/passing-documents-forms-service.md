---
title: 將檔案傳送至FormsService
seo-title: 將檔案傳送至FormsService
description: '將包含表單設計的com.adobe.idp.Document物件傳遞至Forms服務。 Forms服務會轉譯位於com.adobe.idp.Document物件中的表單設計。 '
seo-description: 將包含表單設計的com.adobe.idp.Document物件傳遞至Forms服務。 Forms服務會轉譯位於com.adobe.idp.Document物件中的表單設計。
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 0%

---


# 將文檔傳遞至Forms服務{#passing-documents-to-the-formsservice}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

AEM Forms服務會將互動式PDF forms轉譯至用戶端裝置（通常是網頁瀏覽器），以收集使用者的資訊。 互動式PDF表格是以表格設計為基礎，通常會儲存為XDP檔案，並在Designer中建立。 從AEM Forms開始，您可以將包含表單設計的`com.adobe.idp.Document`物件傳遞至Forms服務。 然後，Forms服務將呈現位於`com.adobe.idp.Document`對象中的表單設計。

將`com.adobe.idp.Document`對象傳遞到Forms服務的一個好處是，其他服務操作返回`com.adobe.idp.Document`實例。 也就是說，您可以從其他服務操作中獲取一個`com.adobe.idp.Document`實例並進行渲染。 例如，假設XDP檔案儲存在名為`/Company Home/Form Designs`的Content Services（已過時）節點中，如下圖所示。

您可以以程式設計方式從Content Services（不建議使用）擷取Loan.xdp，並將XDP檔案傳遞至`com.adobe.idp.Document`物件內的Forms服務。

>[!NOTE]
>
>有關Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟{#summary-of-steps}摘要

若要將從Content Services取得的檔案（已過時）（已過時）傳遞至Forms服務，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms和檔案管理用戶端API物件。
1. 從Content Services擷取表單設計（已過時）。
1. 轉換互動式PDF表單。
1. 對表單資料流執行動作。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立Forms和檔案管理用戶端API物件**

在以程式設計方式執行Forms服務API操作之前，請先建立Forms客戶端API對象。 此外，由於此工作流程會從Content Services擷取XDP檔案（已停用），因此請建立Document Management API物件。

**從Content Services擷取表單設計（已過時）**

使用Java或web service API從Content Services（已過時）擷取XDP檔案。 在`com.adobe.idp.Document`實例（或在使用web services時為`BLOB`實例）中返回XDP檔案。 然後，您可以將`com.adobe.idp.Document`實例傳遞到Forms服務。

**轉換互動式PDF表單**

若要轉換互動式表單，請將從Content Services（不建議使用）傳回的`com.adobe.idp.Document`例項傳遞至Forms服務。

>[!NOTE]
>
>您可以將包含表單設計的`com.adobe.idp.Document`傳遞至Forms服務。 名為`renderPDFForm2`和`renderHTMLForm2`的兩種新方法接受包含表單設計的`com.adobe.idp.Document`物件。

**使用表單資料流執行動作**

視用戶端應用程式類型而定，您可將表單寫入用戶端網頁瀏覽器，或將表單儲存為PDF檔案。 網頁型應用程式通常會將表單寫入網頁瀏覽器。 不過，案頭應用程式通常會將表單儲存為PDF檔案。

**另請參閱**

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## 使用Java API {#pass-documents-to-the-forms-service-using-the-java-api}將檔案傳送至Forms服務

使用Forms服務和內容服務（已過時）API(Java)傳遞從Content Services取得的檔案（已過時）:

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar和adobe-contentservices-client.jar。

1. 建立Forms和檔案管理用戶端API物件

   * 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`DocumentManagementServiceClientImpl`對象。

1. 從Content Services擷取表單設計（已過時）

   叫用`DocumentManagementServiceClientImpl`物件的`retrieveContent`方法並傳遞下列值：

   * 一個字串值，它指定添加內容的儲存。 預設商店為`SpacesStore`。 此值為必要參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值為必要參數。
   * 指定版本的字串值。 此值為可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。

   `retrieveContent`方法返回包含XDP檔案的`CRCResult`對象。 調用`CRCResult`物件的`getDocument`方法，以取得`com.adobe.idp.Document`例項。

1. 轉換互動式PDF表單

   叫用`FormsServiceClient`物件的`renderPDFForm2`方法並傳遞下列值：

   * `com.adobe.idp.Document`物件，包含從Content Services擷取的表單設計（已過時）。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`com.adobe.idp.Document`物件。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 此值為可選參數，如果您不想指定運行時選項，可以指定`null`。
   * 包含URI值的`URLSpec`對象。 此值是可選參數，您可以指定`null`。
   * 儲存檔案附件的`java.util.HashMap`對象。 此值是可選參數，如果您不想將檔案附加到表單，則可以指定`null`。

   `renderPDFForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 使用表單資料流執行動作

   * 通過調用`FormsResult`對象「s `getOutputContent`」方法建立`com.adobe.idp.Document`對象。
   * 通過調用`getContentType`方法獲取`com.adobe.idp.Document`對象的內容類型。
   * 調用`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
   * 調用`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 建立位元組陣列，並呼叫`InputStream`物件的`read`方法，以表單資料流填入。 將位元組陣列作為引數傳遞。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將檔案傳送至Forms服務](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#pass-documents-to-the-forms-service-using-the-web-service-api}將檔案傳遞至Forms服務

使用Forms服務和內容服務（已過時）API(web service)傳遞從內容服務（已過時）獲得的文檔：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 由於此客戶端應用程式調用兩個AEM Forms服務，因此建立兩個服務引用。 對與Forms服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   對與「文檔管理」服務關聯的服務引用使用以下WSDL定義：`http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   由於`BLOB`資料類型對於兩個服務引用都很常見，因此使用`BLOB`資料類型時可完全限定資料類型。 在相應的Web服務快速啟動中，所有`BLOB`實例都完全限定。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立Forms和檔案管理用戶端API物件

   * 使用其預設建構子建立`FormsServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`FormsServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/FormsService?WSDL`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。)
   * 獲取`FormsServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`FormsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`FormsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對`DocumentManagementServiceClient`服務客戶端重複這些步驟。

1. 從Content Services擷取表單設計（已過時）

   叫用`DocumentManagementServiceClient`物件的`retrieveContent`方法並傳遞下列值，以擷取內容：

   * 一個字串值，它指定添加內容的儲存。 預設商店為`SpacesStore`。 此值為必要參數。
   * 一個字串值，它指定要檢索的內容的完全限定路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值為必要參數。
   * 指定版本的字串值。 此值為可選參數，您可以傳遞空字串。 在這種情況下，將檢索最新版本。
   * 儲存瀏覽連結值的字串輸出參數。
   * 儲存內容的`BLOB`輸出參數。 您可以使用此輸出參數來擷取內容。
   * 儲存內容屬性的`ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType`輸出參數。
   * `CRCResult`輸出參數。 您可以使用`BLOB`輸出參數來取得內容，而不是使用此物件。

1. 轉換互動式PDF表單

   叫用`FormsServiceClient`物件的`renderPDFForm2`方法並傳遞下列值：

   * `BLOB`物件，包含從Content Services擷取的表單設計（已過時）。
   * `BLOB`物件，包含要與表單合併的資料。 如果您不想合併資料，請傳遞空白的`BLOB`物件。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 此值為可選參數，如果您不想指定運行時選項，可以指定`null`。
   * 包含URI值的`URLSpec`對象。 此值是可選參數，您可以指定`null`。
   * 儲存檔案附件的`Map`對象。 此值是可選參數，如果您不想將檔案附加到表單，則可以指定`null`。
   * 用於儲存頁數的長輸出參數。
   * 用於儲存地區值的字串輸出參數。
   * 用於儲存互動式PDF表單`.`的`FormsResult`輸出參數

   `renderPDFForm2`方法會傳回包含互動式PDF表單的`FormsResult`物件。

1. 使用表單資料流執行動作

   * 透過取得`FormsResult`物件的`outputContent`欄位值，建立包含表單資料的`BLOB`物件。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表互動式PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存從`FormsResult`對象檢索的`BLOB`對象的內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
