---
title: 使用Web服務API驗證DDX檔案
seo-title: Validate a DDX document using theweb service API
description: 使用組合器服務API驗證DDX文檔。
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

# 使用網站服務API驗證DDX檔案 {#validate-a-ddx-document-using-theweb-service-api}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

使用組合器服務API（Web服務）驗證DDX文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >用表單伺服器的IP地址替換localhost。

1. 建立PDF組合器客戶端。

   * 建立 `AssemblerServiceClient` 物件，使用其預設建構函式。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 建立服務參考時，會使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `AssemblerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 為欄位分配相應的密碼值 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參考現有的DDX文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存DDX文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置以及在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。

1. 設定運行時選項以驗證DDX文檔。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 設定運行時間選項，該選項指示組合器服務通過將值true指定給 `AssemblerOptionSpec` 物件 `validateOnly` 資料成員。
   * 通過為 `AssemblerOptionSpec` 物件 `logLevel` 資料成員。 方法驗證DDX文檔時，您希望將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以指定值 `FINE` 或 `FINER`. 如需可設定的執行階段選項相關資訊，請參閱 `AssemblerOptionSpec` 類引用 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 執行驗證。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列值：

   * A `BLOB` 表示DDX文檔的對象。
   * 值 `null` 針對 `Map` 通常儲存PDF文檔的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含指定DDX文檔是否有效的資訊的對象。

1. 將驗證結果保存在日誌檔案中。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子，並傳遞一個字串值，該字串值表示日誌檔案的檔案位置，以及在中開啟檔案的模式。 請確定副檔名為.xml。
   * 建立 `BLOB` 透過取得 `AssemblerResult` 物件 `jobLog` 資料成員。
   * 建立位元組陣列，用於儲存 `BLOB` 物件。 取得 `BLOB` 物件 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
   * 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

   >[!NOTE]
   >
   >如果DDX檔案無效，則 `OperationException` 被擲回。 在catch陳述式中，您可以取得 `OperationException` 物件 `jobLog` 成員。

**另請參閱**

[驗證DDX文檔](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
