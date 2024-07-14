---
title: 將檔案傳遞至FormsService
description: 將包含表單設計的com.adobe.idp.Document物件傳遞至Forms服務。 Forms服務會呈現com.adobe.idp.Document物件中的表單設計。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 0%

---

# 將檔案傳遞至Forms服務 {#passing-documents-to-the-formsservice}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

AEM Forms服務會將互動式PDF forms轉譯給使用者端裝置（通常是網頁瀏覽器），以收集使用者的資訊。 互動式PDF表單是以表單設計為基礎，通常會儲存為XDP檔案並在Designer中建立。 自AEM Forms起，您可以將包含表單設計的`com.adobe.idp.Document`物件傳遞至Forms服務。 Forms服務接著會轉譯`com.adobe.idp.Document`物件中的表單設計。

將`com.adobe.idp.Document`物件傳遞至Forms服務的好處是，其他服務作業會傳回`com.adobe.idp.Document`執行個體。 也就是說，您可以從另一個服務作業取得`com.adobe.idp.Document`執行個體並加以轉譯。 例如，假設XDP檔案儲存在名為`/Company Home/Form Designs`的Content Services （已過時）節點中，如下圖所示。

您可以程式設計方式從內容服務擷取Loan.xdp （已棄用） （已棄用），並將XDP檔案傳遞至`com.adobe.idp.Document`物件中的Forms服務。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步驟摘要 {#summary-of-steps}

若要將從Content Services （已棄用）取得的檔案傳遞至Forms服務，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms和Document Management使用者端API物件。
1. 從內容服務擷取表單設計（已棄用）。
1. 演算互動式PDF表單。
1. 使用表單資料流執行動作。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立Forms和Document Management Client API物件**

在您以程式設計方式執行Forms服務API作業之前，請先建立Forms使用者端API物件。 此外，由於此工作流程會從內容服務中擷取XDP檔案（已棄用），請建立檔案管理API物件。

**從內容服務擷取表單設計（已棄用）**

使用Java或網站服務API從內容服務擷取XDP檔案（已棄用）。 XDP檔案是在`com.adobe.idp.Document`執行個體中傳回（如果您使用Web服務，則是`BLOB`執行個體）。 然後您可以將`com.adobe.idp.Document`執行個體傳遞至Forms服務。

**演算互動式PDF表單**

若要呈現互動式表單，請將從Content Services （已棄用）傳回的`com.adobe.idp.Document`執行個體傳遞至Forms服務。

>[!NOTE]
>
>您可以將包含表單設計的`com.adobe.idp.Document`傳遞給Forms服務。 名為`renderPDFForm2`和`renderHTMLForm2`的兩個新方法接受包含表單設計的`com.adobe.idp.Document`物件。

**使用表單資料流執行動作**

根據使用者端應用程式的型別，您可以將表單寫入使用者端網頁瀏覽器，或將表單儲存為PDF檔案。 網頁式應用程式通常會將表單寫入網頁瀏覽器。 不過，案頭應用程式通常會將表單儲存為PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## 使用Java API將檔案傳遞至Forms服務 {#pass-documents-to-the-forms-service-using-the-java-api}

使用Forms服務和內容服務（已棄用） API (Java)，傳遞從內容服務（已棄用）取得的檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar和adobe-contentservices-client.jar。

1. 建立Forms和Document Management使用者端API物件

   * 建立包含連線屬性的`ServiceClientFactory`物件。 （請參閱[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`FormsServiceClient`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`DocumentManagementServiceClientImpl`物件。

1. 從內容服務擷取表單設計（已棄用）

   叫用`DocumentManagementServiceClientImpl`物件的`retrieveContent`方法，並傳遞下列值：

   * 字串值，指定新增內容的存放區。 預設存放區為`SpacesStore`。 此值為必要引數。
   * 字串值，指定要擷取之內容的完整路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值為必要引數。
   * 字串值，指定版本。 此值是選用引數，您可以傳遞空字串。 在此情況下，會擷取最新版本。

   `retrieveContent`方法傳回包含XDP檔案的`CRCResult`物件。 透過叫用`CRCResult`物件的`getDocument`方法取得`com.adobe.idp.Document`執行個體。

1. 演算互動式PDF表單

   叫用`FormsServiceClient`物件的`renderPDFForm2`方法，並傳遞下列值：

   * 包含從Content Services擷取之表單設計的`com.adobe.idp.Document`物件（已棄用）。
   * 包含要與表單合併之資料的`com.adobe.idp.Document`物件。 如果您不想合併資料，請傳遞空的`com.adobe.idp.Document`物件。
   * 儲存執行階段選項的`PDFFormRenderSpec`物件。 此值是選用引數，如果您不想指定執行階段選項，可以指定`null`。
   * 包含URI值的`URLSpec`物件。 此值是選用引數，您可以指定`null`。
   * 儲存檔案附件的`java.util.HashMap`物件。 此值是選用引數，如果您不想將檔案附加至表單，可以指定`null`。

   `renderPDFForm`方法傳回`FormsResult`物件，其中包含必須寫入使用者端網頁瀏覽器的表單資料流。

1. 使用表單資料流執行動作

   * 呼叫`FormsResult`物件的`getOutputContent`方法，以建立`com.adobe.idp.Document`物件。
   * 透過叫用物件的`getContentType`方法，取得`com.adobe.idp.Document`物件的內容型別。
   * 透過叫用其`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容型別來設定`javax.servlet.http.HttpServletResponse`物件的內容型別。
   * 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立用來將表單資料流寫入使用者端網頁瀏覽器的`javax.servlet.ServletOutputStream`物件。
   * 呼叫`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
   * 呼叫`InputStream`物件的`read`方法，建立位元組陣列並以表單資料流填入該陣列。 傳遞位元組陣列作為引數。
   * 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料流傳送至使用者端網頁瀏覽器。 將位元組陣列傳遞至`write`方法。

**另請參閱**

[快速入門(SOAP模式)：使用Java API將檔案傳遞至Forms服務](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API將檔案傳遞至Forms服務 {#pass-documents-to-the-forms-service-using-the-web-service-api}

使用Forms服務和內容服務（已棄用） API （網頁服務），傳遞從內容服務（已棄用）取得的檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 由於此使用者端應用程式會叫用兩個AEM Forms服務，請建立兩個服務參考。 使用下列WSDL定義作為與Forms服務相關聯的服務參考： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   使用下列WSDL定義作為與Document Management服務相關聯的服務參考： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   因為`BLOB`資料型別是兩個服務參考的共同型別，使用它時，請完全限定`BLOB`資料型別。 在對應的Web服務快速入門中，所有`BLOB`執行個體都是完全合格的。

   >[!NOTE]
   >
   >將`localhost`取代為裝載AEM Forms之伺服器的IP位址。

1. 建立Forms和Document Management使用者端API物件

   * 使用預設建構函式建立`FormsServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`FormsServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/FormsService?WSDL`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。)
   * 取得`FormsServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`FormsServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`FormsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >對`DocumentManagementServiceClient`服務使用者端重複這些步驟。

1. 從內容服務擷取表單設計（已棄用）

   叫用`DocumentManagementServiceClient`物件的`retrieveContent`方法並傳遞下列值以擷取內容：

   * 字串值，指定新增內容的存放區。 預設存放區為`SpacesStore`。 此值為必要引數。
   * 字串值，指定要擷取之內容的完整路徑（例如`/Company Home/Form Designs/Loan.xdp`）。 此值為必要引數。
   * 字串值，指定版本。 此值是選用引數，您可以傳遞空字串。 在此情況下，會擷取最新版本。
   * 儲存瀏覽連結值的字串輸出引數。
   * 儲存內容的`BLOB`輸出引數。 您可以使用此輸出引數來擷取內容。
   * 儲存內容屬性的`ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType`輸出引數。
   * `CRCResult`輸出引數。 您可以使用`BLOB`輸出引數來取得內容，而不使用此物件。

1. 演算互動式PDF表單

   叫用`FormsServiceClient`物件的`renderPDFForm2`方法，並傳遞下列值：

   * 包含從Content Services擷取之表單設計的`BLOB`物件（已棄用）。
   * 包含要與表單合併之資料的`BLOB`物件。 如果您不想合併資料，請傳遞空的`BLOB`物件。
   * 儲存執行階段選項的`PDFFormRenderSpec`物件。 此值是選用引數，如果您不想指定執行階段選項，可以指定`null`。
   * 包含URI值的`URLSpec`物件。 此值是選用引數，您可以指定`null`。
   * 儲存檔案附件的`Map`物件。 此值是選用引數，如果您不想將檔案附加至表單，可以指定`null`。
   * 用來儲存頁數的長輸出引數。
   * 用來儲存地區設定值的字串輸出引數。
   * `FormsResult`輸出引數，用來儲存互動PDF表單`.`

   `renderPDFForm2`方法傳回包含互動式PDF表單的`FormsResult`物件。

1. 使用表單資料流執行動作

   * 取得`FormsResult`物件之`outputContent`欄位的值，建立包含表單資料的`BLOB`物件。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表互動式PDF檔案檔案位置及開啟檔案模式的字串值。
   * 建立位元組陣列，儲存從`FormsResult`物件擷取的`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
