---
title: 分配使用權
seo-title: 分配使用權
description: 'null'
seo-description: 'null'
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# 分配使用權 {#assigning-usage-rights}

## 關於Acrobat Reader DC擴充功能服務 {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC擴充功能服務可讓貴組織透過擴充Adobe Reader的功能，輕鬆分享互動式PDF檔案。 Acrobat Reader DC擴充功能服務完全支援任何PDF檔案，最高可支援PDF 1.7。它可與Adobe Reader 7.0及更新版本搭配使用。 本服務新增PDF檔案的使用權限，並啟用在使用Adobe reader開啟PDF檔案時通常無法使用的功能。 協力廠商使用者不需要額外的軟體或外掛程式，就能使用具版權的檔案。

您可以使用Acrobat Reader DC擴充功能服務完成下列工作：

* 套用PDF檔案的使用權。 如需詳細資訊，請 [參閱套用PDF檔案的使用權](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。
* 從PDF檔案移除使用權。 如需詳細資訊，請 [參閱「從PDF檔案移除使用權」](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)。
* 檢索憑據詳細資訊。 有關資訊，請參 [閱檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將使用權套用至PDF檔案 {#applying-usage-rights-to-pdf-documents}

您可以使用Acrobat Reader DC擴充功能Java Client API和web service，將使用權套用至PDF檔案。 使用權限與Acrobat預設為Acrobat但Adobe reader未提供的功能相關，例如在表格中新增註解或填寫表格欄位並儲存表格的功能。 具有套用使用權限的PDF檔案稱為具有權限的檔案。 在Adobe Reader中開啟具權限檔案的使用者，可以執行針對該特定檔案啟用的作業。

>[!NOTE]
>
>當使用Java API中的方 `applyUsageRights` 法套用PDF檔案的使用權時，您可將物件的 `isModeFinal` 參數設 `ReaderExtensionsOptionSpec` 定為 `false`。 這會導致表單處理計數器無法更新，而且效能有所提升。 如果您不擔心更新已處理表單的計數器，建議您將參數設 `isModeFinal` 定為 `false`。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將使用權套用至PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴充功能用戶端物件。
1. 擷取PDF檔案。
1. 指定要套用的使用權限。
1. 將使用權套用至PDF檔案。
1. 儲存具權限的PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Acrobat Reader DC擴充功能用戶端物件**

若要以程式設計方式執行Acrobat Reader DC擴充服務作業，您必須建立Acrobat Reader DC擴充功能服務用戶端物件。 如果您使用Acrobat Reader DC擴充功能Java API，請建立物 `ReaderExtensionsServiceClient` 件。 如果您使用Acrobat Reader DC擴充功能網站服務API，請建立物 `ReaderExtensionsServiceService` 件。

**擷取PDF檔案**

您必須擷取PDF檔案，才能套用使用權。 啟用權限的PDF檔案包含使用權限字典。 當Adobe Reader開啟包含此類字典的檔案時，它僅啟用該檔案字典中指定的使用權限。 如果檔案不包含使用權字典，Acrobat Reader DC擴充功能服務會建立一個字典。 如果Acrobat Reader DC擴充功能服務已包含字典，則會以您指定的字典覆寫現有的使用權限。 字典指定啟用哪些使用權限。 當使用者在Adobe Reader中開啟檔案時，僅允許字典中指定的使用權限。

**指定要套用的使用權限**

您可設定的使用權由您向Adobe Systems Incorporated購買的憑證決定。 憑證通常提供設定一組相關使用權限的權限，例如與互動式表單相關的使用權限。 每個憑證都提供建立特定數目且具權限的PDF檔案的權利。 評估憑證可讓您建立不限數量的草稿檔案。

>[!NOTE]
>
>如果您嘗試指派憑證未允許的使用權，將會造成例外。

**將使用權套用至PDF檔案**

若要將使用權套用至PDF檔案，請參考您用來套用使用權的憑證別名（憑證通常會在安裝AEM Forms時安裝）。 此外，您必須指定套用使用權限的PDF檔案。 如需有關設定憑證的詳細資訊，請參閱應用程式伺服器的安裝與部署指南。

**儲存已啟用權限的PDF檔案**

在Acrobat Reader DC擴充功能服務將使用權套用至PDF檔案後，您就可以將具有權限的PDF檔案儲存為PDF檔案。

**另請參閱**

[使用Java API套用使用權](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[使用網站服務API套用使用權](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions Service API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API套用使用權 {#apply-usage-rights-using-the-java-api}

使用Acrobat Reader DC Extensions API(Java)，將使用權套用至PDF檔案：

1. 包含專案檔案

   將用戶端JAR檔案，例如adobe-reader-extensions-client.jar，加入Java專案的類別路徑中。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `ReaderExtensionsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 擷取PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，以建立代表PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 指定要套用的使用權限。

   * 使用其 `UsageRights` 建構函式建立代表使用權限的物件。
   * 對於要應用的每個使用權，請調用屬於該對象的相應 `UsageRights` 方法。 例如，若要新增使 `enableFormFillIn` 用權，請叫用物 `UsageRights` 件的方法 `enableFormFillIn` 並傳遞 `true`。 （請針對每個要套用的使用項目重複此步驟）。

1. 將使用權套用至PDF檔案。

   * 使用其 `ReaderExtensionsOptionSpec` 建構函式建立物件。 此物件包含Acrobat Reader DC擴充功能服務所需的執行時期選項。 調用此建構子時，必須指定以下值：

      * 包 `UsageRights` 含要套用至檔案之使用權限的物件。
      * 一個字串值，指定當在Adobe Reader 7.x中開啟具權限的PDF檔案時，使用者會看見的訊息。Adobe Reader 8.0中不會顯示此訊息。
   * 調用物件的方法並傳遞下列值，以套用 `ReaderExtensionsServiceClient` 使用權 `applyUsageRights` 限至PDF檔案：

      * 包 `com.adobe.idp.Document` 含套用使用權限之PDF檔案的物件。
      * 一個字串值，它指定允許應用使用權限的憑據別名。
      * 指定相應口令值的字串值。 (目前會忽略此參數。 你可以通過 `null`的。)
   * 包 `ReaderExtensionsOptionSpec` 含運行時選項的對象。
   此方 `applyUsageRights` 法會傳回包 `com.adobe.idp.Document` 含啟用權限的PDF檔案的物件。

1. 儲存具權限的PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容複製至檔案(請確定您使用 `com.adobe.idp.Document` 由方法傳回的物 `com.adobe.idp.Document``applyUsageRights` 件)。

**另請參閱**

[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[快速入門（SOAP模式）：使用Java API套用使用權限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API套用使用權 {#apply-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC Extensions API(web service)，將使用權套用至PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   * 使用其 `ReaderExtensionsServiceClient` 預設建構函式建立物件。
   * 使用建 `ReaderExtensionsServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`。 確定您已指 `?blob=mtom`定。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `ReaderExtensionsServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 擷取PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用於儲存套用使用權限的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 指定要套用的使用權限。

   * 使用其 `UsageRights` 建構函式建立代表使用權限的物件。
   * 對於要應用的每個使用權，將值指 `true` 定給屬於該對象的相應資料成 `UsageRights` 員。 例如，若要正確 `enableFormFillIn` 新增使用，請指 `true` 派 `UsageRights` 給物件的資料 `enableFormFillIn` 成員。 （請針對每個要套用的使用項目重複此步驟）。

1. 將使用權套用至PDF檔案。

   * 使用其 `ReaderExtensionsOptionSpec` 建構函式建立物件。 此物件包含Acrobat Reader DC擴充功能服務所需的執行時期選項。
   * 將物 `UsageRights` 件指派給物 `ReaderExtensionsOptionSpec` 件的資料 `usageRights` 成員。
   * 將字串值指定當在Adobe Reader中開啟具權限的PDF檔案時，使用者會看見的訊息指派給物件的 `ReaderExtensionsOptionSpec` 資料 `message` 成員。
   * 調用物件的方法並傳遞下列值，以套用 `ReaderExtensionsServiceClient` 使用權 `applyUsageRights` 限至PDF檔案：

      * 包 `BLOB` 含套用使用權限之PDF檔案的物件。
      * 一個字串值，它指定允許應用使用權限的憑據別名。
      * 指定相應口令值的字串值。 (目前會忽略此參數。 你可以通過 `null`的。)
   * 包 `ReaderExtensionsOptionSpec` 含運行時選項的對象。
   此方 `applyUsageRights` 法會傳回包 `BLOB` 含啟用權限的PDF檔案的物件。

1. 儲存具權限的PDF檔案。

   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表啟用權限的PDF檔案的檔案位置。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `applyUsageRights` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 從PDF檔案移除使用權 {#removing-usage-rights-from-pdf-documents}

您可以從啟用權限的檔案中移除使用權限。 為了在PDF檔案上執行其他AEM Forms作業，也必須從具權限的PDF檔案移除使用權。 例如，您必須先數位簽署（或認證）PDF檔案，才能設定使用權。 因此，如果要對具有權限的文檔執行操作，則必須從PDF文檔中刪除使用權限，執行其他操作，例如對文檔進行數字簽名，然後對文檔重新應用使用權限。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要從啟用權限的PDF檔案移除使用權，請執行下列步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴充功能用戶端物件。
1. 擷取具權限的PDF檔案。
1. 從PDF檔案移除使用權。
1. 儲存PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Acrobat Reader DC擴充功能用戶端物件**

您必須先建立Acrobat Reader DC擴充功能服務用戶端物件，才能以程式設計方式執行Acrobat Reader DC擴充功能服務作業。 如果您使用Java API，請建立物 `ReaderExtensionsServiceClient` 件。 如果您使用Acrobat Reader DC擴充功能網站服務API，請建立物 `ReaderExtensionsServiceService` 件。

**擷取具權限的PDF檔案**

擷取具權限的PDF檔案，以移除使用權限。

**從PDF檔案移除使用權**

擷取具有權限的PDF檔案後，您就可以移除使用權限。 在您移除使用權後，在Adobe reader中檢視PDF檔案時，將不會再有其他功能。

**儲存PDF檔案**

您可以將不再包含使用權限的PDF檔案儲存為PDF檔案。 儲存為PDF檔案後，就可在Adobe Reader或Acrobat中檢視PDF檔案。

**另請參閱**

[使用Java API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用web service API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions Service API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[將使用權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### 使用Java API移除使用權限 {#remove-usage-rights-using-the-java-api}

使用Acrobat Reader DC擴充功能API(Java)，從啟用權限的PDF檔案移除使用權：

1. 包含專案檔案。

   將用戶端JAR檔案，例如adobe-reader-extensions-client.jar，加入Java專案的類別路徑中。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   使用其 `ReaderExtensionsServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 擷取PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，以建立代表啟用權限的PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 從PDF檔案移除使用權。

   叫用物件的方法並傳遞包含已啟用 `ReaderExtensionsServiceClient` 權限的PDF文 `removeUsageRights` 件的物 `com.adobe.idp.Document` 件，以移除PDF檔案的使用權。 此方法傳回 `com.adobe.idp.Document` 包含沒有使用權限之PDF檔案的物件。

1. 將使用權套用至PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為。PDF。
   * 叫用 `Document` 物件的方 `copyToFile` 法，將物件的內容複製至檔案(請確定您使用 `Document` 由方法傳回的物 `Document``removeUsageRights` 件)。

**另請參閱**

[從PDF檔案移除使用權](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[快速入門（SOAP模式）:使用Java API移除PDF檔案的使用權](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API移除使用權限 {#remove-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC擴充功能API(web service)，從具有版權的PDF檔案移除使用權：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   * 使用其 `ReaderExtensionsServiceClient` 預設建構函式建立物件。
   * 使用建 `ReaderExtensionsServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`。 確定您已指 `?blob=mtom`定。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `ReaderExtensionsServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 擷取PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 此物 `BLOB` 件用來儲存啟用權限的PDF檔案，從中移除使用權限。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 從PDF檔案移除使用權。

   叫用物件的方法並傳遞包含已啟用 `ReaderExtensionsServiceClient` 權限的PDF文 `removeUsageRights` 件的物 `BLOB` 件，以移除PDF檔案的使用權。 此方法傳回 `BLOB` 包含沒有使用權限之PDF檔案的物件。

1. 將使用權套用至PDF檔案。

   * 叫用 `System.IO.FileStream` 其建構函式並傳遞代表PDF檔案位置的字串值，以建立物件。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `removeUsageRights` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。

**另請參閱**

[從PDF檔案移除使用權](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢索憑據資訊 {#retrieving-credential-information}

您可以擷取有關憑證的資訊，此憑證用來將使用權套用至具權限的PDF檔案。 通過檢索有關憑據的資訊，您可以獲取諸如證書失效日期之類的資訊。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要檢索有關用於將使用權限應用於PDF文檔的憑據的資訊，請執行以下步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴充功能用戶端物件。
1. 擷取具權限的PDF檔案。
1. 檢索有關憑據的資訊。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立Acrobat Reader DC擴充功能用戶端物件**

您必須先建立Acrobat Reader DC擴充功能服務用戶端物件，才能以程式設計方式執行Acrobat Reader DC擴充功能服務作業。 如果您使用Java API，請建立物 `ReaderExtensionsServiceClient` 件。 如果您使用Acrobat Reader DC擴充功能網站服務API，請建立物 `ReaderExtensionsServiceService` 件。

**擷取具權限的PDF檔案**

您必須擷取具有權限的PDF檔案，才能擷取憑證的相關資訊。 您也可以通過指定憑據的別名來檢索有關憑據的資訊；不過，如果您想要擷取有關用於將使用權限套用至具特定權限之PDF檔案之憑證的資訊，則必須擷取該檔案。

**檢索有關憑據的資訊**

擷取具有權限的PDF檔案後，您就可取得有關用來套用使用權限之憑證的資訊。 您可取得有關憑證的下列資訊：

* 開啟具權限的PDF檔案時，Adobe Reader中會顯示的訊息。
* 憑據失效的日期。
* 憑證無效的日期。
* 為啟用權限的PDF檔案設定的使用權限。
* 已使用憑證的次數。

**另請參閱**

[使用Java API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用web service API移除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions Service API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API擷取憑證資訊 {#retrieve-credential-information-using-the-java-api}

使用Acrobat Reader DC擴充功能API(Java)擷取憑證資訊：

1. 包含專案檔案。

   將用戶端JAR檔案，例如adobe-reader-extensions-client.jar，加入Java專案的類別路徑中。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   使用其 `ReaderExtensionsServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 擷取PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞字串值，指定啟用權限的PDF檔案位置，以建立代表啟用權限的PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 從PDF檔案移除使用權。

   * 叫用物件的方法並傳遞包含已啟用權限的PDF檔案的物件，以擷 `ReaderExtensionsServiceClient` 取 `getDocumentUsageRights` 用於 `com.adobe.idp.Document` 套用使用權限之PDF檔案的憑證。 此方法會傳回包 `GetUsageRightsResult` 含憑證資訊的物件。
   * 呼叫物件的方法，以擷取此日期後憑證 `GetUsageRightsResult` 不再有 `getNotAfter` 效。 此方法傳回 `java.util.Date` 代表憑證失效日期的物件。
   * 在啟用權限的PDF檔案開啟時，透過叫用物件的方法來擷取在Adobe Reader中顯 `GetUsageRightsResult` 示的訊 `getMessage` 息。 此方法會傳回代表訊息的字串值。

**另請參閱**

[檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)

[快速入門（SOAP模式）:使用Java API檢索憑據資訊](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API擷取憑證資訊 {#retrieve-credential-information-using-the-web-service-api}

使用Acrobat Reader DC擴充功能API(web service)擷取憑證資訊：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Acrobat Reader DC擴充功能用戶端物件。

   * 使用其 `ReaderExtensionsServiceClient` 預設建構函式建立物件。
   * 使用建 `ReaderExtensionsServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`。 確定您已指 `?blob=mtom`定。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `ReaderExtensionsServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 擷取PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 此物 `BLOB` 件用來儲存具權限的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示啟用權限的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 從PDF檔案移除使用權。

   * 叫用物件的方法並傳遞包含已啟用權限的PDF檔案的物件，以擷 `ReaderExtensionsServiceClient` 取 `getDocumentUsageRights` 用於 `com.adobe.idp.Document` 套用使用權限之PDF檔案的憑證。 此方法返回包 `GetUsageRightsResult` 含憑據資訊的對象。
   * 取得物件資料成員的值，以擷取此日期之後憑證 `GetUsageRightsResult` 不再有 `notAfter` 效的日期。 此資料成員的資料類型為 `System.DateTime`。
   * 透過取得物件資料成員的值，擷取啟用權限的PDF檔案在Adobe Reader中開啟時 `GetUsageRightsResult` 顯示的 `message` 訊息。 此資料成員的資料類型是字串。
   * 獲取對象資料成員的值，以檢索憑 `GetUsageRightsResult` 據的使 `useCount` 用次數。 此資料成員的資料類型是整數。

**另請參閱**

[檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
