---
title: 使用網站服務API驗證DDX檔案
description: 使用組合器服務API來驗證DDX檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# 使用網站服務API驗證DDX檔案 {#validate-a-ddx-document-using-theweb-service-api}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

使用組合器服務API （Web服務）驗證DDX檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以Forms伺服器的IP位址取代localhost。

1. 建立PDF組合器使用者端。

   * 使用預設建構函式建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。
   * 取得`AssemblerServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存DDX檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表DDX檔案檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。

1. 設定執行階段選項以驗證DDX檔案。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 將值true指派給`AssemblerOptionSpec`物件的`validateOnly`資料成員，以設定執行階段選項，指示Assembler服務驗證DDX檔案。
   * 將字串值指派給`AssemblerOptionSpec`物件的`logLevel`資料成員，以設定Assembler服務寫入記錄檔的資訊量。 方法驗證DDX檔案時，您想要將更多資訊寫入記錄檔，以協助進行驗證程式。 因此，您可以指定值`FINE`或`FINER`。 如需您可以設定的執行階段選項相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

1. 執行驗證。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列值：

   * 代表DDX檔案的`BLOB`物件。
   * 通常儲存PDF檔案的`Map`物件的值`null`。
   * 指定執行階段選項的`AssemblerOptionSpec`物件。

   `invokeDDX`方法傳回`AssemblerResult`物件，其中包含指定DDX檔案是否有效的資訊。

1. 將驗證結果儲存在記錄檔中。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表記錄檔之檔案位置的字串值，以及開啟檔案的模式。 確認副檔名為.xml。
   * 取得`AssemblerResult`物件的`jobLog`資料成員的值，建立儲存記錄資訊的`BLOB`物件。
   * 建立位元組陣列以儲存`BLOB`物件的內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

   >[!NOTE]
   >
   >如果DDX檔案無效，則會擲回`OperationException`。 在catch陳述式中，您可以取得`OperationException`物件的`jobLog`成員的值。

**另請參閱**

[驗證DDX檔案](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
