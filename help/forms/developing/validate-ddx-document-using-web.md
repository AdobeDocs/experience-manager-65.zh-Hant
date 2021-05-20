---
title: 使用Web服務API驗證DDX檔案
seo-title: 使用Web服務API驗證DDX檔案
description: 使用組合器服務API驗證DDX文檔。
seo-description: 使用組合器服務API驗證DDX文檔。
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
source-wordcount: '658'
ht-degree: 0%

---

# 使用Web服務API {#validate-a-ddx-document-using-theweb-service-api}驗證DDX文檔

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

使用組合器服務API（Web服務）驗證DDX文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >用表單伺服器的IP地址替換localhost。

1. 建立PDF組合器客戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX文檔。

   * 使用其建構子建立`BLOB`物件。 `BLOB`對象用於儲存DDX文檔。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示DDX文檔的檔案位置以及在中開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 設定運行時選項以驗證DDX文檔。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 設定運行時間選項，該選項指示組合器服務通過將值true分配給`AssemblerOptionSpec`對象的`validateOnly`資料成員來驗證DDX文檔。
   * 通過將字串值分配給`AssemblerOptionSpec`對象的`logLevel`資料成員，設定組合器服務寫入日誌檔案的資訊量。 方法驗證DDX文檔時，您希望將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以指定值`FINE`或`FINER`。 如需可設定的執行階段選項相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

1. 執行驗證。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象。
   * 通常儲存PDF文檔的`Map`對象的值`null`。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含指定DDX文檔是否有效的資訊。

1. 將驗證結果保存在日誌檔案中。

   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示日誌檔案的檔案位置以及在中開啟檔案的模式。 請確定副檔名為.xml。
   * 通過獲取`AssemblerResult`對象的`jobLog`資料成員的值，建立儲存日誌資訊的`BLOB`對象。
   * 建立儲存`BLOB`對象內容的位元組陣列。 獲取`BLOB`對象的`MTOM`欄位的值，填入位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

   >[!NOTE]
   >
   >如果DDX文檔無效，則擲回`OperationException`。 在catch語句中，可以獲取`OperationException`對象的`jobLog`成員的值。

**另請參閱**

[驗證DDX文檔](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
