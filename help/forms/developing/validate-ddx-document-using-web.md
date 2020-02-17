---
title: 使用web service API驗證DDX檔案
seo-title: 使用web service API驗證DDX檔案
description: 'null'
seo-description: 'null'
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用web service API驗證DDX檔案 {#validate-a-ddx-document-using-theweb-service-api}

使用Assembler Service API(web service)驗證DDX文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將localhost替換為表單伺服器的IP地址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其 `AssemblerServiceClient` 預設建構函式建立物件。
   * 使用建 `AssemblerServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `AssemblerServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存DDX文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示DDX文檔的檔案位置以及在中開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 設定執行時期選項以驗證DDX檔案。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 設定執行時選項，指示Assembler服務將值true指派給物件的資料成員，以驗證DDX `AssemblerOptionSpec` 文 `validateOnly` 件。
   * 通過為對象的資料成員分配字串值，設定Assembler服務寫入日誌檔案 `AssemblerOptionSpec` 的信 `logLevel` 息量。 方法驗證DDX文檔時，需要將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以指定值 `FINE` 或 `FINER`。 如需您可設定之執行時期選項的詳細資訊，請參閱 `AssemblerOptionSpec`[AEM Forms API參考中的類別參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 執行驗證。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列值：

   * 表 `BLOB` 示DDX文檔的對象。
   * 通常 `null` 儲存PDF文 `Map` 檔的對象的值。
   * 指定 `AssemblerOptionSpec` 運行時選項的對象。
   該方 `invokeDDX` 法返回一 `AssemblerResult` 個包含指定DDX文檔是否有效的資訊的對象。

1. 將驗證結果保存到日誌檔案中。

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示日誌檔案的檔案位置以及開啟檔案的模式。 請確定副檔名為。xml。
   * 透過 `BLOB` 取得物件資料成員的值，建立儲存記錄 `AssemblerResult` 資訊的 `jobLog` 物件。
   * 建立儲存物件內容的位元組 `BLOB` 陣列。 取得物件欄位的值，以填入 `BLOB` 位元組陣 `MTOM` 列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。
   >[!NOTE]
   >
   >如果DDX文檔無效，則拋 `OperationException` 出一個。 在catch語句中，可以獲取對象成 `OperationException` 員的值 `jobLog` 。

**另請參閱**

[驗證DDX文檔](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
