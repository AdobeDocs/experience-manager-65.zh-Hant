---
title: 使用Web服務API驗證DDX文檔
seo-title: Validate a DDX document using theweb service API
description: 使用匯編器服務API驗證DDX文檔。
seo-description: Use the Assembler Service API to validate a DDX document.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 使用Web服務API驗證DDX文檔 {#validate-a-ddx-document-using-theweb-service-api}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

使用匯編器服務API（Web服務）驗證DDX文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將localhost替換為表單伺服器的IP地址。

1. 建立PDF匯編器客戶端。

   * 建立 `AssemblerServiceClient` 對象。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `AssemblerServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用現有DDX文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存DDX文檔。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值（該字串值表示DDX文檔的檔案位置和開啟檔案的模式）來對對象。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 設定運行時選項以驗證DDX文檔。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 設定運行時選項，該選項指示匯編器服務通過將值true賦給 `AssemblerOptionSpec` 對象 `validateOnly` 資料成員。
   * 通過為匯編程式服務指定字串值，設定匯編程式服務寫入日誌檔案的資訊量 `AssemblerOptionSpec` 對象 `logLevel` 資料成員。 方法驗證DDX文檔時，希望將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，可以指定值 `FINE` 或 `FINER`。 有關可設定的運行時選項的資訊，請參見 `AssemblerOptionSpec` 類引用 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 執行驗證。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象。
   * 值 `null` 為 `Map` 通常儲存PDF文檔的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含指定DDX文檔是否有效的資訊的對象。

1. 將驗證結果保存到日誌檔案中。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示日誌檔案的檔案位置以及在中開啟檔案的模式。 確保檔案副檔名為.xml。
   * 建立 `BLOB` 通過獲取日誌資訊 `AssemblerResult` 對象 `jobLog` 資料成員。
   * 建立一個位元組陣列，用於儲存 `BLOB` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 的子菜單。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

   >[!NOTE]
   >
   >如果DDX文檔無效，則 `OperationException` 。 在catch語句中，可以獲取 `OperationException` 對象 `jobLog` 成員。

**另請參閱**

[驗證DDX文檔](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
