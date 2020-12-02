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
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---


# 使用web service API {#validate-a-ddx-document-using-theweb-service-api}驗證DDX檔案

使用Assembler Service API(web service)驗證DDX文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將localhost替換為表單伺服器的IP地址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存DDX檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的&lt;a1/>屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 設定執行時期選項以驗證DDX檔案。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 設定執行時選項，指示Assembler服務將值true指派給`AssemblerOptionSpec`物件的`validateOnly`資料成員，以驗證DDX檔案。
   * 通過為`AssemblerOptionSpec`對象的`logLevel`資料成員分配字串值，設定Assembler服務寫入日誌檔案的資訊量。 方法驗證DDX文檔時，需要將更多資訊寫入日誌檔案，以幫助驗證過程。 因此，您可以指定值`FINE`或`FINER`。 如需您可設定之執行時期選項的詳細資訊，請參閱[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

1. 執行驗證。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象。
   * 通常儲存PDF文檔的`Map`對象的`null`值。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invokeDDX`方法返回`AssemblerResult`對象，該對象包含指定DDX文檔是否有效的資訊。

1. 將驗證結果保存到日誌檔案中。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示日誌檔案的檔案位置和開啟檔案的模式。 請確定副檔名為。xml。
   * 通過獲取`AssemblerResult`對象的`jobLog`資料成員的值，建立儲存日誌資訊的`BLOB`對象。
   * 建立儲存`BLOB`對象內容的位元組陣列。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立&lt;a0/>對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

   >[!NOTE]
   >
   >如果DDX文檔無效，則拋出`OperationException`。 在catch語句中，可以獲取`OperationException`對象`jobLog`成員的值。

**另請參閱**

[驗證DDX文檔](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
