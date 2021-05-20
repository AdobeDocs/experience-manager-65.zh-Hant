---
title: 分配使用權
seo-title: 分配使用權
description: 使用Acrobat Reader DC擴充功能Java Client API和Web服務API，套用PDF檔案的使用權限，並從中移除該權限。
seo-description: 使用Acrobat Reader DC擴充功能Java Client API和Web服務API，套用PDF檔案的使用權限，並從中移除該權限。
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3951'
ht-degree: 0%

---

# 分配使用權{#assigning-usage-rights}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於Acrobat Reader DC擴充功能服務{#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC擴充功能服務可讓您的組織透過擴充Adobe Reader的功能，輕鬆共用互動式PDF檔案。 Acrobat Reader DC擴充功能服務完全支援任何PDF檔案，最多及包含PDF 1.7。可與Adobe Reader 7.0及更新版本搭配使用。 此服務會為PDF檔案新增使用權限，啟用使用Adobe Reader開啟PDF檔案時通常無法使用的功能。 協力廠商使用者不需要其他軟體或外掛程式，即可搭配啟用權限的檔案使用。

您可以使用Acrobat Reader DC擴充功能服務來完成下列工作：

* 將使用權應用於PDF文檔。 如需詳細資訊，請參閱[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。
* 從PDF檔案中移除使用權限。 如需詳細資訊，請參閱[從PDF檔案中移除使用權限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)。
* 檢索憑據詳細資訊。 有關資訊，請參閱[檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將使用權應用於PDF文檔{#applying-usage-rights-to-pdf-documents}

您可以使用Acrobat Reader DC擴充功能Java Client API和Web服務，將使用權套用至PDF檔案。 使用權限屬於Acrobat預設提供但Adobe Reader未提供的功能，例如可向表單新增註解，或填寫表單欄位並儲存表單。 套用使用權限的PDF檔案稱為啟用權限的檔案。 在Adobe Reader中開啟啟用權限的檔案的使用者可以執行針對該特定檔案啟用的操作。

>[!NOTE]
>
>使用`applyUsageRights`方法（Java API的一部分）對PDF文檔應用使用權時，您可以將`ReaderExtensionsOptionSpec`對象的`isModeFinal`參數設定為`false`。 這會導致未更新表單處理計數器，並提升效能。 若您不關心更新已處理的表單計數器，建議您將`isModeFinal`參數設為`false`。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}的摘要

要將使用權應用於PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴充功能用戶端物件。
1. 檢索PDF文檔。
1. 指定要應用的使用權限。
1. 將使用權應用於PDF文檔。
1. 儲存已啟用權限的PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Acrobat Reader DC擴充功能用戶端物件**

若要以程式設計方式執行Acrobat Reader DC擴充功能服務操作，您必須建立Acrobat Reader DC擴充功能服務用戶端物件。 如果您使用Acrobat Reader DC擴充功能Java API，請建立`ReaderExtensionsServiceClient`物件。 如果您使用Acrobat Reader DC擴充功能Web服務API，請建立`ReaderExtensionsServiceService`物件。

**檢索PDF文檔**

您必須檢索PDF文檔才能應用使用權。 啟用權限的PDF檔案包含使用權限字典。 Adobe Reader開啟包含此類字典的檔案時，僅會啟用該檔案在字典中指定的使用權限。 如果檔案不包含使用權限字典，Acrobat Reader DC擴充功能服務會建立字典。 如果已包含字典，Acrobat Reader DC擴充功能服務會使用您指定的使用權限覆寫現有的使用權限。 字典指定啟用的使用權限。 使用者在Adobe Reader中開啟檔案時，僅允許字典中指定的使用權限。

**指定要應用的使用權限**

您可以設定的使用權限由您從Adobe Systems Incorporated購買的憑證決定。 憑證通常會提供設定一組相關使用權限的權限，例如與互動式表單相關的權限。 每個憑證都提供建立特定數量已啟用權限之PDF檔案的權利。 評估憑證有權建立不限數量的檔案草稿。

>[!NOTE]
>
>如果嘗試分配憑據不允許的使用權，將導致異常。

**將使用權應用於PDF文檔**

若要將使用權套用至PDF檔案，請參考您用來套用使用權之憑證的別名(憑證通常會在安裝AEM Forms期間安裝)。 您還必須指定應用使用權限的PDF文檔。 有關配置憑據的資訊，請參閱應用程式伺服器的安裝和部署指南。

**儲存已啟用權限的PDF檔案**

在Acrobat Reader DC擴充功能服務將使用權套用至PDF檔案後，您可以將已啟用權限的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API套用使用權限](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[使用網站服務API套用使用權限](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴充功能服務API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API {#apply-usage-rights-using-the-java-api}套用使用權限

使用Acrobat Reader DC Extensions API(Java)將使用權套用至PDF檔案：

1. 包含項目檔案

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-reader-extensions-client.jar。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`ReaderExtensionsServiceClient`物件。

1. 檢索PDF文檔。

   * 使用PDF文檔的建構子並傳遞指定PDF文檔位置的字串值，建立代表PDF文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 指定要應用的使用權限。

   * 使用其建構子建立代表使用權的`UsageRights`物件。
   * 對於要應用的每個使用權限，調用屬於`UsageRights`對象的相應方法。 例如，若要新增`enableFormFillIn`使用權限，請叫用`UsageRights`物件的`enableFormFillIn`方法，然後傳遞`true`。 （請針對每個使用權限重複此步驟以套用）。

1. 將使用權應用於PDF文檔。

   * 使用其建構子建立`ReaderExtensionsOptionSpec`物件。 此物件包含Acrobat Reader DC擴充功能服務所需的執行階段選項。 調用此建構子時，必須指定以下值：

      * `UsageRights`對象，包含要應用到文檔的使用權限。
      * 一個字串值，指定在Adobe Reader 7.x中開啟啟用權限的PDF檔案時，使用者會看見的訊息。Adobe Reader 8.0未顯示此訊息。
   * 調用`ReaderExtensionsServiceClient`對象的`applyUsageRights`方法並傳遞以下值，將使用權應用於PDF文檔：

      * `com.adobe.idp.Document`物件，包含套用使用權限的PDF檔案。
      * 一個字串值，它指定憑據的別名，使您能夠應用使用權限。
      * 指定相應密碼值的字串值。 (目前會忽略此參數。 您可以傳遞`null`。)
   * 包含運行時選項的`ReaderExtensionsOptionSpec`對象。

   `applyUsageRights`方法返回包含已啟用權限的PDF文檔的`com.adobe.idp.Document`對象。

1. 儲存已啟用權限的PDF檔案。

   * 建立`java.io.File`物件，並確認副檔名為.pdf。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案（確保使用`applyUsageRights`方法返回的`com.adobe.idp.Document`對象）。

**另請參閱**

[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[快速入門（SOAP模式）：使用Java API套用使用權限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#apply-usage-rights-using-the-web-service-api}應用使用權限

使用Acrobat Reader DC Extensions API（Web服務），將使用權套用至PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   * 使用其預設建構子建立`ReaderExtensionsServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`ReaderExtensionsServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 請確定您指定`?blob=mtom`。)
   * 獲取`ReaderExtensionsServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 檢索PDF文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存應用使用權限的PDF文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 指定要應用的使用權限。

   * 使用其建構子建立代表使用權的`UsageRights`物件。
   * 對於要應用的每個使用權限，將值`true`分配給屬於`UsageRights`對象的相應資料成員。 例如，要添加`enableFormFillIn`使用權限，請將`true`分配給`UsageRights`對象的`enableFormFillIn`資料成員。 （請針對每個使用權限重複此步驟以套用）。

1. 將使用權應用於PDF文檔。

   * 使用其建構子建立`ReaderExtensionsOptionSpec`物件。 此物件包含Acrobat Reader DC擴充功能服務所需的執行階段選項。
   * 將`UsageRights`對象分配給`ReaderExtensionsOptionSpec`對象的`usageRights`資料成員。
   * 將一個字串值指定在Adobe Reader中開啟啟用權限的PDF文檔時用戶看到的消息，指定給`ReaderExtensionsOptionSpec`對象的`message`資料成員。
   * 調用`ReaderExtensionsServiceClient`對象的`applyUsageRights`方法並傳遞以下值，將使用權應用於PDF文檔：

      * `BLOB`物件，包含套用使用權限的PDF檔案。
      * 一個字串值，它指定憑據的別名，使您能夠應用使用權限。
      * 指定相應密碼值的字串值。 (目前會忽略此參數。 您可以傳遞`null`。)
   * 包含運行時選項的`ReaderExtensionsOptionSpec`對象。

   `applyUsageRights`方法返回包含已啟用權限的PDF文檔的`BLOB`對象。

1. 儲存已啟用權限的PDF檔案。

   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示啟用權限的PDF檔案的檔案位置。
   * 建立位元組陣列，用於儲存`applyUsageRights`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 從PDF文檔{#removing-usage-rights-from-pdf-documents}中刪除使用權限

您可以從啟用權限的文檔中刪除使用權限。 若要對啟用權限的PDF檔案執行其他AEM Forms作業，也必須移除其使用權限。 例如，您必須先以數位方式簽署（或認證）PDF檔案，才能設定使用權限。 因此，如果要對啟用權限的文檔執行操作，必須從PDF文檔中刪除使用權限，執行其他操作，例如對文檔進行數字簽名，然後對文檔重新應用使用權限。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}的摘要

要從啟用權限的PDF文檔中刪除使用權限，請執行以下步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴充功能用戶端物件。
1. 檢索啟用權限的PDF文檔。
1. 從PDF文檔中刪除使用權限。
1. 保存PDF文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Acrobat Reader DC擴充功能用戶端物件**

您必須先建立Acrobat Reader DC擴充功能服務用戶端物件，才能以程式設計方式執行Acrobat Reader DC擴充功能服務作業。 如果您使用Java API，請建立`ReaderExtensionsServiceClient`物件。 如果您使用Acrobat Reader DC擴充功能Web服務API，請建立`ReaderExtensionsServiceService`物件。

**檢索啟用權限的PDF文檔**

檢索啟用權限的PDF文檔，以刪除使用權限。

**從PDF文檔中刪除使用權限**

擷取已啟用權限的PDF檔案後，您可以移除使用權限。 移除使用權限後，在Adobe Reader中檢視PDF檔案時，將沒有任何其他功能。

**儲存PDF檔案**

您可以將不再包含使用權限的PDF檔案儲存為PDF檔案。 儲存為PDF檔案後，即可在Adobe Reader或Acrobat中檢視PDF檔案。

**另請參閱**

[使用Java API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用網站服務API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴充功能服務API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### 使用Java API {#remove-usage-rights-using-the-java-api}移除使用權限

使用Acrobat Reader DC擴充功能API(Java)，從啟用權限的PDF檔案中移除使用權限：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-reader-extensions-client.jar。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`ReaderExtensionsServiceClient`物件。

1. 檢索PDF文檔。

   * 使用其建構子並傳遞指定PDF文檔位置的字串值，建立`java.io.FileInputStream`對象，該對象表示啟用權限的PDF文檔。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 從PDF文檔中刪除使用權限。

   調用`ReaderExtensionsServiceClient`對象的`removeUsageRights`方法並傳遞包含已啟用權限的PDF文檔的`com.adobe.idp.Document`對象，從PDF文檔中刪除使用權限。 此方法會傳回`com.adobe.idp.Document`物件，其中包含沒有使用權限的PDF檔案。

1. 將使用權應用於PDF文檔。

   * 建立`java.io.File`物件，並確定副檔名為.PDF。
   * 調用`Document`對象的`copyToFile`方法，將`Document`對象的內容複製到檔案（確保使用`removeUsageRights`方法返回的`Document`對象）。

**另請參閱**

[從PDF檔案中移除使用權限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[快速入門（SOAP模式）:使用Java API從PDF檔案中移除使用權限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#remove-usage-rights-using-the-web-service-api}刪除使用權限

使用Acrobat Reader DC擴充功能API（網站服務），從啟用權限的PDF檔案中移除使用權限：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   * 使用其預設建構子建立`ReaderExtensionsServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`ReaderExtensionsServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 請確定您指定`?blob=mtom`。)
   * 獲取`ReaderExtensionsServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 檢索PDF文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存啟用權限的PDF文檔，從中刪除使用權限。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 從PDF文檔中刪除使用權限。

   調用`ReaderExtensionsServiceClient`對象的`removeUsageRights`方法並傳遞包含已啟用權限的PDF文檔的`BLOB`對象，從PDF文檔中刪除使用權限。 此方法會傳回`BLOB`物件，其中包含沒有使用權限的PDF檔案。

1. 將使用權應用於PDF文檔。

   * 叫用`System.IO.FileStream`物件的建構子並傳遞代表PDF檔案位置的字串值，以建立物件。
   * 建立位元組陣列，用於儲存`removeUsageRights`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`資料成員的值，以填充位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。

**另請參閱**

[從PDF檔案中移除使用權限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢索憑據資訊{#retrieving-credential-information}

您可以檢索有關用於將使用權應用於啟用權限的PDF文檔的憑據的資訊。 通過檢索有關憑據的資訊，可以獲取諸如證書失效日期等資訊。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-2}的摘要

要檢索有關用於將使用權應用於PDF文檔的憑據的資訊，請執行以下步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴充功能用戶端物件。
1. 檢索啟用權限的PDF文檔。
1. 檢索有關憑據的資訊。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Acrobat Reader DC擴充功能用戶端物件**

您必須先建立Acrobat Reader DC擴充功能服務用戶端物件，才能以程式設計方式執行Acrobat Reader DC擴充功能服務作業。 如果您使用Java API，請建立`ReaderExtensionsServiceClient`物件。 如果您使用Acrobat Reader DC擴充功能Web服務API，請建立`ReaderExtensionsServiceService`物件。

**檢索啟用權限的PDF文檔**

必須檢索啟用權限的PDF文檔，才能檢索有關憑據的資訊。 您還可以通過指定憑據的別名來檢索有關憑據的資訊；但是，如果要檢索有關用於將使用權應用於啟用特定權限的PDF文檔的憑據的資訊，則必須檢索該文檔。

**檢索有關憑據的資訊**

檢索啟用權限的PDF文檔後，您可以獲取有關用於應用使用權限的憑據的資訊。 您可以獲取有關憑據的以下資訊：

* 開啟啟用權限的PDF檔案時，Adobe Reader中顯示的訊息。
* 憑據失效的日期。
* 憑據無效的日期。
* 為啟用此權限的PDF文檔設定的使用權限。
* 已使用憑據的次數。

**另請參閱**

[使用Java API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用網站服務API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴充功能服務API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API {#retrieve-credential-information-using-the-java-api}檢索憑據資訊

使用Acrobat Reader DC擴充功能API(Java)擷取憑證資訊：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-reader-extensions-client.jar。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   使用其建構子並傳遞包含連線屬性的`ServiceClientFactory`物件，以建立`ReaderExtensionsServiceClient`物件。

1. 檢索PDF文檔。

   * 使用其建構子並傳遞字串值來指定啟用權限的PDF檔案的位置，以建立代表啟用權限的PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 從PDF文檔中刪除使用權限。

   * 調用`ReaderExtensionsServiceClient`對象的`getDocumentUsageRights`方法並傳遞包含已啟用權限的PDF文檔的`com.adobe.idp.Document`對象，檢索有關用於將使用權限應用到PDF文檔的憑據的資訊。 此方法返回包含憑據資訊的`GetUsageRightsResult`對象。
   * 調用`GetUsageRightsResult`對象的`getNotAfter`方法，檢索在此日期之後憑據不再有效。 此方法會傳回`java.util.Date`物件，代表憑證失效的日期。
   * 叫用`GetUsageRightsResult`物件的`getMessage`方法，以開啟啟用權限的PDF檔案時，擷取Adobe Reader中顯示的訊息。 此方法會傳回代表訊息的字串值。

**另請參閱**

[檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)

[快速入門（SOAP模式）:使用Java API檢索憑據資訊](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API {#retrieve-credential-information-using-the-web-service-api}檢索憑據資訊

使用Acrobat Reader DC擴充功能API（網站服務）擷取憑證資訊：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   * 使用其預設建構子建立`ReaderExtensionsServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`ReaderExtensionsServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 請確定您指定`?blob=mtom`。)
   * 獲取`ReaderExtensionsServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 檢索PDF文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`物件可用來儲存啟用權限的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示啟用權限的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 從PDF文檔中刪除使用權限。

   * 調用`ReaderExtensionsServiceClient`對象的`getDocumentUsageRights`方法並傳遞包含已啟用權限的PDF文檔的`com.adobe.idp.Document`對象，檢索有關用於將使用權限應用到PDF文檔的憑據的資訊。 此方法返回包含憑據資訊的`GetUsageRightsResult`對象。
   * 通過獲取`GetUsageRightsResult`對象的`notAfter`資料成員的值，檢索在此日期之後憑據不再有效的日期。 此資料成員的資料類型為`System.DateTime`。
   * 通過獲取`GetUsageRightsResult`對象的`message`資料成員的值，檢索在Adobe Reader中開啟啟用權限的PDF文檔時顯示的消息。 此資料成員的資料類型為字串。
   * 通過獲取`GetUsageRightsResult`對象的`useCount`資料成員的值來檢索憑據的使用次數。 此資料成員的資料類型是整數。

**另請參閱**

[檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
