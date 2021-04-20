---
title: 分配使用權
seo-title: 分配使用權
description: 使用Acrobat Reader DC擴充功能Java Client API和Web Service API，套用和移除PDF檔案的使用權。
seo-description: 使用Acrobat Reader DC擴充功能Java Client API和Web Service API，套用和移除PDF檔案的使用權。
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3952'
ht-degree: 0%

---


# 分配使用權{#assigning-usage-rights}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

## 關於Acrobat Reader DC擴展服務{#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC擴充功能服務可讓貴組織透過擴充Adobe Reader的功能，輕鬆分享互動式PDF檔案。 Acrobat Reader DC擴充功能服務完全支援任何PDF檔案，最高可支援PDF 1.7。它適用於Adobe Reader7.0及更新版本。 本服務新增PDF檔案的使用權限，以啟用在使用Adobe Reader開啟PDF檔案時通常無法使用的功能。 協力廠商使用者不需要額外的軟體或外掛程式，就能使用具版權的檔案。

您可以使用Acrobat Reader DC擴展服務完成以下任務：

* 套用PDF檔案的使用權。 如需詳細資訊，請參閱[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。
* 從PDF檔案移除使用權。 如需詳細資訊，請參閱[從PDF檔案移除使用權](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)。
* 檢索憑據詳細資訊。 有關資訊，請參閱[檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)。

>[!NOTE]
>
>有關Acrobat Reader DC擴展服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將使用權套用至PDF檔案{#applying-usage-rights-to-pdf-documents}

您可以使用Acrobat Reader DC擴充功能Java用戶端API和web service，將使用權套用至PDF檔案。 使用權限與Acrobat預設在Adobe Reader但不在的功能相關，例如在表單中新增註解或填寫表單欄位並儲存表單的功能。 具有套用使用權限的PDF檔案稱為具有權限的檔案。 在Adobe Reader開啟啟用權限的檔案的使用者可以執行針對該特定檔案啟用的作業。

>[!NOTE]
>
>使用Java API的`applyUsageRights`方法套用PDF檔案的使用權時，您可以將`ReaderExtensionsOptionSpec`物件的`isModeFinal`參數設定為`false`。 這會導致表單處理計數器無法更新，而且效能有所提升。 如果您不擔心更新已處理的表單計數器，建議您將`isModeFinal`參數設為`false`。

>[!NOTE]
>
>有關Acrobat Reader DC擴展服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

若要將使用權套用至PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴展客戶端對象。
1. 擷取PDF檔案。
1. 指定要套用的使用權限。
1. 將使用權套用至PDF檔案。
1. 儲存具權限的PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Acrobat Reader DC擴展客戶端對象**

要以寫程式方式執行Acrobat Reader DC擴展服務操作，必須建立Acrobat Reader DC擴展服務客戶端對象。 如果您使用Acrobat Reader DC擴展Java API，請建立`ReaderExtensionsServiceClient`對象。 如果您使用Acrobat Reader DC擴展Web服務API，請建立`ReaderExtensionsServiceService`對象。

**擷取PDF檔案**

您必須擷取PDF檔案，才能套用使用權。 啟用權限的PDF檔案包含使用權限字典。 當Adobe Reader開啟包含此類字典的文檔時，它僅啟用該文檔字典中指定的使用權限。 如果文檔不包含使用權字典，Acrobat Reader DC擴展服務將建立一個。 如果它已包含字典，Acrobat Reader DC擴充功能服務會以您指定的字典覆寫現有的使用權限。 字典指定啟用哪些使用權限。 當使用者在Adobe Reader開啟檔案時，僅允許字典中指定的使用權限。

**指定要套用的使用權限**

您可以設定的使用權由您向Adobe Systems Incorporated購買的憑證決定。 憑證通常提供設定一組相關使用權限的權限，例如與互動式表單相關的使用權限。 每個憑證都提供建立特定數目且具權限的PDF檔案的權利。 評估憑證可讓您建立不限數量的草稿檔案。

>[!NOTE]
>
>如果您嘗試指派憑證未允許的使用權，將會造成例外。

**將使用權套用至PDF檔案**

若要將使用權套用至PDF檔案，請參考您用來套用使用權之憑證的別名(憑證通常在安裝AEM Forms期間安裝)。 此外，您必須指定套用使用權限的PDF檔案。 如需有關設定憑證的詳細資訊，請參閱應用程式伺服器的安裝與部署指南。

**儲存已啟用權限的PDF檔案**

在Acrobat Reader DC擴充功能服務將使用權套用至PDF檔案後，您就可以將具權限的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API套用使用權](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[使用網站服務API套用使用權](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴充功能服務API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API {#apply-usage-rights-using-the-java-api}套用使用權

使用Acrobat Reader DC擴充功能API(Java)，將使用權套用至PDF檔案：

1. 包含專案檔案

   將用戶端JAR檔案，例如adobe-reader-extensions-client.jar，加入Java專案的類別路徑中。

1. 建立Acrobat Reader DC擴展客戶端對象。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`ReaderExtensionsServiceClient`對象。

1. 擷取PDF檔案。

   * 使用PDF檔案的建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 指定要套用的使用權限。

   * 使用其建構函式建立代表使用權限的`UsageRights`物件。
   * 對於要應用的每個使用權，請調用屬於`UsageRights`對象的相應方法。 例如，若要新增`enableFormFillIn`使用權限，請叫用`UsageRights`物件的`enableFormFillIn`方法並傳遞`true`。 （請針對每個要套用的使用項目重複此步驟）。

1. 將使用權套用至PDF檔案。

   * 使用其建構子建立`ReaderExtensionsOptionSpec`對象。 此對象包含Acrobat Reader DC擴展服務所需的運行時選項。 調用此建構子時，必須指定以下值：

      * `UsageRights`物件，包含套用至檔案的使用權限。
      * 一個字串值，指定當在Adobe Reader7.x中開啟具權限的PDF檔案時，使用者會看到的訊息。此消息不顯示在Adobe Reader8.0中。
   * 調用`ReaderExtensionsServiceClient`物件的`applyUsageRights`方法並傳遞下列值，以套用PDF檔案的使用權：

      * `com.adobe.idp.Document`物件，包含套用使用權限的PDF檔案。
      * 一個字串值，它指定允許應用使用權限的憑據別名。
      * 指定相應口令值的字串值。 (目前會忽略此參數。 您可以傳遞`null`。)
   * 包含運行時選項的`ReaderExtensionsOptionSpec`對象。

   `applyUsageRights`方法會傳回包含啟用權限的PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存具權限的PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為。pdf。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製至檔案（請確定您使用`applyUsageRights`方法傳回的`com.adobe.idp.Document`物件）。

**另請參閱**

[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[快速入門（SOAP模式）：使用Java API套用使用權限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#apply-usage-rights-using-the-web-service-api}套用使用權

使用Acrobat Reader DC擴充功能API(web service)，將使用權套用至PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立Acrobat Reader DC擴展客戶端對象。

   * 使用其預設建構子建立`ReaderExtensionsServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`ReaderExtensionsServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 請確定您指定`?blob=mtom`。)
   * 獲取`ReaderExtensionsServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存套用使用權限的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 指定要套用的使用權限。

   * 使用其建構函式建立代表使用權限的`UsageRights`物件。
   * 對於要應用的每個使用權，將值`true`分配給屬於`UsageRights`對象的相應資料成員。 例如，若要正確新增`enableFormFillIn`使用，請將`true`指派給`UsageRights`物件的`enableFormFillIn`資料成員。 （請針對每個要套用的使用項目重複此步驟）。

1. 將使用權套用至PDF檔案。

   * 使用其建構子建立`ReaderExtensionsOptionSpec`對象。 此對象包含Acrobat Reader DC擴展服務所需的運行時選項。
   * 將`UsageRights`物件指派給`ReaderExtensionsOptionSpec`物件的`usageRights`資料成員。
   * 為`ReaderExtensionsOptionSpec`物件的`message`資料成員指派字串值，此字串值會指定使用者在Adobe Reader開啟啟用權限的PDF檔案時看到的訊息。
   * 調用`ReaderExtensionsServiceClient`物件的`applyUsageRights`方法並傳遞下列值，以套用PDF檔案的使用權：

      * `BLOB`物件，包含套用使用權限的PDF檔案。
      * 一個字串值，它指定允許應用使用權限的憑據別名。
      * 指定相應口令值的字串值。 (目前會忽略此參數。 您可以傳遞`null`。)
   * 包含運行時選項的`ReaderExtensionsOptionSpec`對象。

   `applyUsageRights`方法會傳回包含啟用權限的PDF檔案的`BLOB`物件。

1. 儲存具權限的PDF檔案。

   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表啟用權限的PDF檔案的檔案位置。
   * 建立一個位元組陣列，用於儲存`applyUsageRights`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 從PDF檔案移除使用權{#removing-usage-rights-from-pdf-documents}

您可以從啟用權限的檔案中移除使用權限。 為了對PDF檔案執行其他AEM Forms作業，也必須從具權限的PDF檔案移除使用權。 例如，您必須先數位簽署（或認證）PDF檔案，才能設定使用權。 因此，如果要對具有權限的文檔執行操作，則必須從PDF文檔中刪除使用權限，執行其他操作，例如對文檔進行數字簽名，然後對文檔重新應用使用權限。

>[!NOTE]
>
>有關Acrobat Reader DC擴展服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}摘要

若要從啟用權限的PDF檔案移除使用權，請執行下列步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴展客戶端對象。
1. 擷取具權限的PDF檔案。
1. 從PDF檔案移除使用權。
1. 儲存PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Acrobat Reader DC擴展客戶端對象**

在以寫程式方式執行Acrobat Reader DC擴展服務操作之前，必須建立Acrobat Reader DC擴展服務客戶端對象。 如果您使用Java API，請建立`ReaderExtensionsServiceClient`物件。 如果您使用Acrobat Reader DC擴展Web服務API，請建立`ReaderExtensionsServiceService`對象。

**擷取具權限的PDF檔案**

擷取具權限的PDF檔案，以移除使用權限。

**從PDF檔案移除使用權**

擷取具有權限的PDF檔案後，您就可以移除使用權限。 在您移除使用權後，在Adobe Reader檢視PDF檔案時，將不會再有其他功能。

**儲存PDF檔案**

您可以將不再包含使用權限的PDF檔案儲存為PDF檔案。 儲存為PDF檔案後，就可在Adobe Reader或Acrobat檢視PDF檔案。

**另請參閱**

[使用Java API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用web service API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴充功能服務API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### 使用Java API {#remove-usage-rights-using-the-java-api}移除使用權

使用Acrobat Reader DC擴充功能API(Java)，從啟用權限的PDF檔案移除使用權：

1. 包含專案檔案。

   將用戶端JAR檔案，例如adobe-reader-extensions-client.jar，加入Java專案的類別路徑中。

1. 建立Acrobat Reader DC擴展客戶端對象。

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ReaderExtensionsServiceClient`對象。

1. 擷取PDF檔案。

   * 使用PDF檔案的建構函式並傳遞指定PDF檔案位置的字串值，建立代表具有權限的PDF檔案的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 從PDF檔案移除使用權。

   叫用`ReaderExtensionsServiceClient`物件的`removeUsageRights`方法，並傳遞包含啟用權限的PDF檔案的`com.adobe.idp.Document`物件，以移除PDF檔案的使用權限。 此方法會傳回`com.adobe.idp.Document`物件，其中包含沒有使用權限的PDF檔案。

1. 將使用權套用至PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為。PDF。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製至檔案（請確定您使用`removeUsageRights`方法傳回的`Document`物件）。

**另請參閱**

[從PDF檔案移除使用權](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[快速入門（SOAP模式）:使用Java API移除PDF檔案的使用權](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#remove-usage-rights-using-the-web-service-api}移除使用權限

使用Acrobat Reader DC擴充功能API(web service)，從具版權的PDF檔案移除使用權：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立Acrobat Reader DC擴展客戶端對象。

   * 使用其預設建構子建立`ReaderExtensionsServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`ReaderExtensionsServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 請確定您指定`?blob=mtom`。)
   * 獲取`ReaderExtensionsServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存已啟用權限的PDF檔案，從中移除使用權限。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 從PDF檔案移除使用權。

   叫用`ReaderExtensionsServiceClient`物件的`removeUsageRights`方法，並傳遞包含啟用權限的PDF檔案的`BLOB`物件，以移除PDF檔案的使用權限。 此方法會傳回`BLOB`物件，其中包含沒有使用權限的PDF檔案。

1. 將使用權套用至PDF檔案。

   * 叫用其建構函式並傳遞代表PDF檔案位置的字串值，以建立`System.IO.FileStream`物件。
   * 建立一個位元組陣列，用於儲存`removeUsageRights`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。

**另請參閱**

[從PDF檔案移除使用權](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢索憑據資訊{#retrieving-credential-information}

您可以擷取有關憑證的資訊，此憑證用來將使用權套用至具權限的PDF檔案。 通過檢索有關憑據的資訊，您可以獲取諸如證書失效日期之類的資訊。

>[!NOTE]
>
>有關Acrobat Reader DC擴展服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-2}摘要

要檢索有關用於將使用權限應用於PDF文檔的憑據的資訊，請執行以下步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴展客戶端對象。
1. 擷取具權限的PDF檔案。
1. 檢索有關憑據的資訊。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Acrobat Reader DC擴展客戶端對象**

在以寫程式方式執行Acrobat Reader DC擴展服務操作之前，必須建立Acrobat Reader DC擴展服務客戶端對象。 如果您使用Java API，請建立`ReaderExtensionsServiceClient`物件。 如果您使用Acrobat Reader DC擴展Web服務API，請建立`ReaderExtensionsServiceService`對象。

**擷取具權限的PDF檔案**

您必須擷取具有權限的PDF檔案，才能擷取憑證的相關資訊。 您也可以通過指定憑據的別名來檢索有關憑據的資訊；不過，如果您想要擷取有關用於將使用權限套用至具特定權限之PDF檔案之憑證的資訊，則必須擷取該檔案。

**檢索有關憑據的資訊**

擷取具有權限的PDF檔案後，您就可取得有關用來套用使用權限之憑證的資訊。 您可取得有關憑證的下列資訊：

* 啟用權限的PDF檔案開啟時，在Adobe Reader顯示的訊息。
* 憑據失效的日期。
* 憑證無效的日期。
* 為啟用權限的PDF檔案設定的使用權限。
* 已使用憑證的次數。

**另請參閱**

[使用Java API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用web service API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴充功能服務API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API {#retrieve-credential-information-using-the-java-api}擷取憑證資訊

使用Acrobat Reader DC擴展API(Java)來檢索憑據資訊：

1. 包含專案檔案。

   將用戶端JAR檔案，例如adobe-reader-extensions-client.jar，加入Java專案的類別路徑中。

1. 建立Acrobat Reader DC擴展客戶端對象。

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ReaderExtensionsServiceClient`對象。

1. 擷取PDF檔案。

   * 使用`java.io.FileInputStream`物件的建構函式，並傳遞字串值，指定啟用權限的PDF檔案位置，以建立代表啟用權限的PDF檔案的物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 從PDF檔案移除使用權。

   * 叫用`ReaderExtensionsServiceClient`物件的`getDocumentUsageRights`方法並傳遞包含啟用權限的PDF檔案的`com.adobe.idp.Document`物件，以擷取用於套用使用權限之PDF檔案之憑證的相關資訊。 此方法返回包含憑證資訊的`GetUsageRightsResult`物件。
   * 調用`GetUsageRightsResult`物件的`getNotAfter`方法，擷取憑證不再有效的日期。 此方法傳回`java.util.Date`物件，該物件代表憑證不再有效的日期。
   * 呼叫`GetUsageRightsResult`物件的`getMessage`方法，以擷取啟用權限的PDF檔案開啟時在Adobe Reader顯示的訊息。 此方法會傳回代表訊息的字串值。

**另請參閱**

[檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)

[快速入門（SOAP模式）:使用Java API檢索憑據資訊](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#retrieve-credential-information-using-the-web-service-api}擷取憑證資訊

使用Acrobat Reader DC擴展API(web service)檢索憑據資訊：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立Acrobat Reader DC擴展客戶端對象。

   * 使用其預設建構子建立`ReaderExtensionsServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`ReaderExtensionsServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 請確定您指定`?blob=mtom`。)
   * 獲取`ReaderExtensionsServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 擷取PDF檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存啟用權限的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示啟用權限的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 從PDF檔案移除使用權。

   * 叫用`ReaderExtensionsServiceClient`物件的`getDocumentUsageRights`方法並傳遞包含啟用權限的PDF檔案的`com.adobe.idp.Document`物件，以擷取用於套用使用權限之PDF檔案之憑證的相關資訊。 此方法返回包含憑據資訊的`GetUsageRightsResult`對象。
   * 取得`GetUsageRightsResult`物件的`notAfter`資料成員的值，以擷取憑證不再有效的日期。 此資料成員的資料類型為`System.DateTime`。
   * 取得`GetUsageRightsResult`物件`message`資料成員的值，擷取啟用權限的PDF檔案在Adobe Reader開啟時顯示的訊息。 此資料成員的資料類型是字串。
   * 獲取`GetUsageRightsResult`對象`useCount`資料成員的值，以檢索憑據的使用次數。 此資料成員的資料類型是整數。

**另請參閱**

[檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
