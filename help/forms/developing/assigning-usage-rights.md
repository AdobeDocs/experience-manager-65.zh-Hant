---
title: 分配使用權限
seo-title: Assigning Usage Rights
description: 使用Acrobat Reader DC擴展Java客戶端API和Web服務API來應用和刪除PDF文檔中的使用權限。
seo-description: Use the Acrobat Reader DC extensions Java Client API and Web Service API to apply and remove usage rights from PDF documents.
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
source-wordcount: '3926'
ht-degree: 0%

---

# 分配使用權限 {#assigning-usage-rights}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 關於Acrobat Reader DC分機服務 {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC擴展服務通過擴展Adobe Reader的功能，使您的組織能夠輕鬆共用互動式PDF文檔。 Acrobat Reader DC分機處完全支援任何PDF檔案，直至和包括第1.7號PDF。它與Adobe Reader7.0及更高版本配合使用。 該服務將使用權限添加到PDF文檔，激活在使用Adobe Reader開啟PDF文檔時通常不可用的功能。 第三方用戶不需要額外的軟體或插件來處理啟用權限的文檔。

可以使用Acrobat Reader DC擴展服務完成以下任務：

* 將使用權限應用於PDF文檔。 有關資訊，請參見 [將使用權限應用於PDF文檔](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。
* 從PDF文檔中刪除使用權限。 有關資訊，請參見 [從PDF文檔中刪除使用權限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)。
* 檢索憑據詳細資訊。 有關資訊，請參見 [正在檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)。

>[!NOTE]
>
>有關Acrobat Reader DC擴展服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將使用權限應用於PDF文檔 {#applying-usage-rights-to-pdf-documents}

可以使用Acrobat Reader DC擴展Java客戶端API和Web服務對PDF文檔應用使用權限。 使用權限與預設在Acrobat但在Adobe Reader不可用的功能有關，例如向表單添加註釋或填寫表單域並保存表單的功能。 對其應用了使用權限的PDF文檔稱為啟用權限的文檔。 在Adobe Reader開啟啟用權限的文檔的用戶可以執行為該特定文檔啟用的操作。

>[!NOTE]
>
>將使用權限應用於PDF文檔時，使用 `applyUsageRights` 方法是Java API的一部分，可以設定 `isModeFinal` 參數 `ReaderExtensionsOptionSpec` 對象 `false`。 這導致未更新表單處理的計數器和效能改進。 如果您不關心更新表單處理的計數器，建議您設定 `isModeFinal` 參數 `false`。

>[!NOTE]
>
>有關Acrobat Reader DC擴展服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要對PDF文檔應用使用權限，請執行以下步驟：

1. 包括項目檔案。
1. 建立Acrobat Reader DC擴展客戶端對象。
1. 檢索PDF文檔。
1. 指定要應用的使用權限。
1. 對PDF文檔應用使用權限。
1. 保存啟用權限的PDF文檔。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Acrobat Reader DC擴展客戶端對象**

要以寫程式方式執行Acrobat Reader DC擴展服務操作，必須建立Acrobat Reader DC擴展服務客戶端對象。 如果使用Acrobat Reader DC擴展Java API，請建立 `ReaderExtensionsServiceClient` 的雙曲餘切值。 如果使用Acrobat Reader DC擴展Web服務API，請建立 `ReaderExtensionsServiceService` 的雙曲餘切值。

**檢索PDF文檔**

必須檢索PDF文檔才能應用使用權限。 啟用權限的PDF文檔包含使用權限詞典。 當Adobe Reader開啟包含此類字典的文檔時，它只啟用該文檔在字典中指定的使用權限。 如果文檔不包含使用權限字典，則Acrobat Reader DC擴展服務將建立一個。 如果它已包含字典，則Acrobat Reader DC擴展服務將用您指定的使用權限覆蓋現有的使用權限。 字典指定啟用哪些使用權限。 當用戶在Adobe Reader中開啟文檔時，只允許字典中指定的使用權限。

**指定要應用的使用權限**

您可以設定的使用權限由您從Adobe Systems Incorporated購買的憑據決定。 憑據通常提供設定一組相關使用權限的權限，如與互動式表單相關的權限。 每個憑據都提供建立特定數量的啟用權限的PDF文檔的權限。 評估憑據賦予建立無限制數量的草稿文檔的權利。

>[!NOTE]
>
>如果嘗試分配憑據不允許的使用權，將導致異常。

**將使用權限應用於PDF文檔**

要對PDF文檔應用使用權，請引用您正在應用使用權的憑據的別名(通常在安裝AEM Forms期間安裝憑據)。 此外，您還必須指定應用使用權限的PDF文檔。 有關配置憑據的資訊，請參閱應用程式伺服器的安裝和部署指南。

**保存啟用權限的PDF文檔**

在Acrobat Reader DC擴展服務將使用權限應用於PDF文檔後，可以將啟用權限的PDF文檔另存為PDF檔案。

**另請參閱**

[使用Java API應用使用權限](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[使用Web服務API應用使用權限](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴展服務API快速啟動](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API應用使用權限 {#apply-usage-rights-using-the-java-api}

使用Acrobat Reader DC擴展API(Java)將使用權限應用於PDF文檔：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-reader-extensions-client.jar。

1. 建立Acrobat Reader DC擴展客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `ReaderExtensionsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索PDF文檔。

   * 建立 `java.io.FileInputStream` 表示PDF文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 指定要應用的使用權限。

   * 建立 `UsageRights` 表示使用其建構子的使用權限的對象。
   * 對於每個要應用的使用權，調用屬於 `UsageRights` 的雙曲餘切值。 例如，要添加 `enableFormFillIn` 使用權，調用 `UsageRights` 對象 `enableFormFillIn` 方法 `true`。 （對要應用的每個使用權限重複此步驟）。

1. 對PDF文檔應用使用權限。

   * 建立 `ReaderExtensionsOptionSpec` 對象。 此對象包含Acrobat Reader DC擴展服務所需的運行時選項。 調用此建構子時，必須指定以下值：

      * 的 `UsageRights` 包含要應用於文檔的使用權限的對象。
      * 一個字串值，它指定用戶在Adobe Reader7.x中開啟啟用權限的PDF文檔時看到的消息。此消息未在Adobe Reader8.0中顯示。
   * 通過調用PDF文檔 `ReaderExtensionsServiceClient` 對象 `applyUsageRights` 方法並傳遞以下值：

      * 的 `com.adobe.idp.Document` 包含應用使用權限的PDF文檔的對象。
      * 一個字串值，它指定憑據的別名，您可以應用使用權限。
      * 一個字串值，它指定相應的口令值。 (當前忽略此參數。 你可以通過 `null`。)
   * 的 `ReaderExtensionsOptionSpec` 包含運行時選項的對象。

   的 `applyUsageRights` 方法返回 `com.adobe.idp.Document` 包含啟用權限的PDF文檔的對象。

1. 保存啟用權限的PDF文檔。

   * 建立 `java.io.File` 並確保檔案副檔名為.pdf。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象到檔案(確保 `com.adobe.idp.Document` 返回的對象 `applyUsageRights` )。

**另請參閱**

[將使用權限應用於PDF文檔](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[快速啟動（SOAP模式）：使用Java API應用使用權限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API應用使用權限 {#apply-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC擴展API（Web服務）將使用權限應用於PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立Acrobat Reader DC擴展客戶端對象。

   * 建立 `ReaderExtensionsServiceClient` 對象。
   * 建立 `ReaderExtensionsServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`。 確保指定 `?blob=mtom`。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `ReaderExtensionsServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 檢索PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存應用使用權限的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 指定要應用的使用權限。

   * 建立 `UsageRights` 表示使用其建構子的使用權限的對象。
   * 對於每個要應用的使用權限，分配值 `true` 到屬於 `UsageRights` 的雙曲餘切值。 例如，要添加 `enableFormFillIn` 使用權限，分配 `true` 到 `UsageRights` 對象 `enableFormFillIn` 資料成員。 （對要應用的每個使用權限重複此步驟）。

1. 對PDF文檔應用使用權限。

   * 建立 `ReaderExtensionsOptionSpec` 對象。 此對象包含Acrobat Reader DC擴展服務所需的運行時選項。
   * 分配 `UsageRights` 對象 `ReaderExtensionsOptionSpec` 對象 `usageRights` 資料成員。
   * 將一個字串值指定用戶在Adobe Reader中開啟啟用權限的PDF文檔時看到的消息分配給 `ReaderExtensionsOptionSpec` 對象 `message` 資料成員。
   * 通過調用PDF文檔 `ReaderExtensionsServiceClient` 對象 `applyUsageRights` 方法並傳遞以下值：

      * 的 `BLOB` 包含應用使用權限的PDF文檔的對象。
      * 一個字串值，它指定憑據的別名，您可以應用使用權限。
      * 一個字串值，它指定相應的口令值。 (當前忽略此參數。 你可以通過 `null`。)
   * 的 `ReaderExtensionsOptionSpec` 包含運行時選項的對象。

   的 `applyUsageRights` 方法返回 `BLOB` 包含啟用權限的PDF文檔的對象。

1. 保存啟用權限的PDF文檔。

   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示啟用權限的PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `applyUsageRights` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[將使用權限應用於PDF文檔](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 從PDF文檔中刪除使用權限 {#removing-usage-rights-from-pdf-documents}

可以從啟用權限的文檔中刪除使用權限。 從啟用權限的PDF文檔中刪除使用權限也是執行其他AEM Forms操作所必需的。 例如，在設定使用權限之前，必須對PDF文檔進行數字簽名（或認證）。 因此，如果要對啟用了權限的文檔執行操作，則必須從PDF文檔中刪除使用權限，執行其他操作，例如對文檔進行數字簽名，然後對文檔重新應用使用權限。

>[!NOTE]
>
>有關Acrobat Reader DC擴展服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要從啟用權限的PDF文檔中刪除使用權限，請執行以下步驟：

1. 包括項目檔案。
1. 建立Acrobat Reader DC擴展客戶端對象。
1. 檢索啟用權限的PDF文檔。
1. 從PDF文檔中刪除使用權限。
1. 保存PDF文檔。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Acrobat Reader DC擴展客戶端對象**

在以寫程式方式執行Acrobat Reader DC擴展服務操作之前，必須建立Acrobat Reader DC擴展服務客戶端對象。 如果使用Java API，請建立 `ReaderExtensionsServiceClient` 的雙曲餘切值。 如果使用Acrobat Reader DC擴展Web服務API，請建立 `ReaderExtensionsServiceService` 的雙曲餘切值。

**檢索啟用權限的PDF文檔**

檢索啟用權限的PDF文檔以刪除使用權限。

**從PDF文檔中刪除使用權限**

檢索啟用權限的PDF文檔後，可以刪除使用權限。 刪除使用權限後，在Adobe Reader內查看PDF文檔時將沒有任何附加功能。

**保存PDF文檔**

可以將不再包含使用權的PDF文檔另存為PDF檔案。 一旦保存為PDF檔案，PDF文檔可在Adobe Reader或Acrobat查看。

**另請參閱**

[使用Java API刪除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服務API刪除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴展服務API快速啟動](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[將使用權限應用於PDF文檔](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### 使用Java API刪除使用權限 {#remove-usage-rights-using-the-java-api}

使用Acrobat Reader DC擴展API(Java)從啟用權限的PDF文檔中刪除使用權限：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-reader-extensions-client.jar。

1. 建立Acrobat Reader DC擴展客戶端對象。

   建立 `ReaderExtensionsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 檢索PDF文檔。

   * 建立 `java.io.FileInputStream` 對象，該對象使用其建構子並傳遞一個字串值來表示啟用權限的PDF文檔，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 從PDF文檔中刪除使用權限。

   通過調用PDF文檔來刪除使用權限 `ReaderExtensionsServiceClient` 對象 `removeUsageRights` 方法和傳遞 `com.adobe.idp.Document` 包含啟用權限的PDF文檔的對象。 此方法返回 `com.adobe.idp.Document` 包含沒有使用權限的PDF文檔的對象。

1. 對PDF文檔應用使用權限。

   * 建立 `java.io.File` 對象，並確保檔案副檔名為。PDF。
   * 調用 `Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象到檔案(確保 `Document` 返回的對象 `removeUsageRights` )。

**另請參閱**

[從PDF文檔中刪除使用權限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[快速啟動（SOAP模式）:使用Java API從PDF文檔中刪除使用權限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API刪除使用權限 {#remove-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC擴展API（Web服務）從啟用權限的PDF文檔中刪除使用權限：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立Acrobat Reader DC擴展客戶端對象。

   * 建立 `ReaderExtensionsServiceClient` 對象。
   * 建立 `ReaderExtensionsServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`。 確保指定 `?blob=mtom`。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `ReaderExtensionsServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 檢索PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存啟用權限的PDF文檔，從中刪除使用權限。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 從PDF文檔中刪除使用權限。

   通過調用PDF文檔來刪除使用權限 `ReaderExtensionsServiceClient` 對象 `removeUsageRights` 方法和傳遞 `BLOB` 包含啟用權限的PDF文檔的對象。 此方法返回 `BLOB` 包含沒有使用權限的PDF文檔的對象。

1. 對PDF文檔應用使用權限。

   * 建立 `System.IO.FileStream` 調用其建構子並傳遞表示PDF檔案位置的字串值。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `removeUsageRights` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。

**另請參閱**

[從PDF文檔中刪除使用權限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 正在檢索憑據資訊 {#retrieving-credential-information}

您可以檢索有關用於將使用權限應用於啟用權限的PDF文檔的憑據的資訊。 通過檢索有關憑據的資訊，您可以獲取諸如證書不再有效的日期之類的資訊。

>[!NOTE]
>
>有關Acrobat Reader DC擴展服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要檢索有關用於將使用權限應用於PDF文檔的憑據的資訊，請執行以下步驟：

1. 包括項目檔案。
1. 建立Acrobat Reader DC擴展客戶端對象。
1. 檢索啟用權限的PDF文檔。
1. 檢索有關憑據的資訊。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立Acrobat Reader DC擴展客戶端對象**

在以寫程式方式執行Acrobat Reader DC擴展服務操作之前，必須建立Acrobat Reader DC擴展服務客戶端對象。 如果使用Java API，請建立 `ReaderExtensionsServiceClient` 的雙曲餘切值。 如果使用Acrobat Reader DC擴展Web服務API，請建立 `ReaderExtensionsServiceService` 的雙曲餘切值。

**檢索啟用權限的PDF文檔**

必須檢索啟用權限的PDF文檔，才能檢索有關憑據的資訊。 您還可以通過指定憑據的別名來檢索有關憑據的資訊；但是，如果要檢索有關用於將使用權限應用於啟用特定權限的PDF文檔的憑據的資訊，則必須檢索該文檔。

**檢索有關憑據的資訊**

檢索啟用權限的PDF文檔後，可以獲取有關用於對其應用使用權限的憑據的資訊。 您可以獲取有關憑據的以下資訊：

* 開啟啟用權限的PDF文檔時，在Adobe Reader內顯示的消息。
* 憑據不再有效的日期。
* 憑據無效的日期。
* 為此啟用權限的PDF文檔設定的使用權限。
* 已使用憑據的次數。

**另請參閱**

[使用Java API刪除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服務API刪除使用權限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴展服務API快速啟動](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API檢索憑據資訊 {#retrieve-credential-information-using-the-java-api}

使用Acrobat Reader DC擴展API(Java)檢索憑據資訊：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-reader-extensions-client.jar。

1. 建立Acrobat Reader DC擴展客戶端對象。

   建立 `ReaderExtensionsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 檢索PDF文檔。

   * 建立 `java.io.FileInputStream` 對象，該對象使用其建構子並傳遞一個字串值來表示啟用權限的PDF文檔，該字串值指定啟用權限的PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 從PDF文檔中刪除使用權限。

   * 通過調用PDF文檔，檢索有關用於將使用權應用於使用權的憑據的資訊 `ReaderExtensionsServiceClient` 對象 `getDocumentUsageRights` 方法和傳遞 `com.adobe.idp.Document` 包含啟用權限的PDF文檔的對象。 此方法返回 `GetUsageRightsResult` 包含憑據資訊的對象。
   * 通過調用 `GetUsageRightsResult` 對象 `getNotAfter` 的雙曲餘切值。 此方法返回 `java.util.Date` 表示憑據不再有效的日期的對象。
   * 通過調用啟用權限的PDF文檔開啟時，檢索在Adobe Reader顯示的消息 `GetUsageRightsResult` 對象 `getMessage` 的雙曲餘切值。 此方法返回表示消息的字串值。

**另請參閱**

[正在檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)

[快速啟動（SOAP模式）:使用Java API檢索憑據資訊](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API檢索憑據資訊 {#retrieve-credential-information-using-the-web-service-api}

使用Acrobat Reader DC擴展API（Web服務）檢索憑據資訊：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立Acrobat Reader DC擴展客戶端對象。

   * 建立 `ReaderExtensionsServiceClient` 對象。
   * 建立 `ReaderExtensionsServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`。 確保指定 `?blob=mtom`。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `ReaderExtensionsServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 檢索PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存啟用權限的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示啟用權限的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 從PDF文檔中刪除使用權限。

   * 通過調用PDF文檔，檢索有關用於將使用權應用於使用權的憑據的資訊 `ReaderExtensionsServiceClient` 對象 `getDocumentUsageRights` 方法和傳遞 `com.adobe.idp.Document` 包含啟用權限的PDF文檔的對象。 此方法返回 `GetUsageRightsResult` 包含憑據資訊的對象。
   * 通過獲取憑據的值，檢索憑據不再有效的日期 `GetUsageRightsResult` 對象 `notAfter` 資料成員。 此資料成員的資料類型為 `System.DateTime`。
   * 通過獲取的PDF的值，檢索在Adobe Reader開啟啟用權限的文檔時顯示的消息 `GetUsageRightsResult` 對象 `message` 資料成員。 此資料成員的資料類型是字串。
   * 通過獲取的 `GetUsageRightsResult` 對象 `useCount` 資料成員。 此資料成員的資料類型為整數。

**另請參閱**

[正在檢索憑據資訊](assigning-usage-rights.md#retrieving-credential-information)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
