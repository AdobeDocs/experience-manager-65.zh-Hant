---
title: 使用web service API拆解PDF檔案
seo-title: 使用web service API拆解PDF檔案
description: 使用Assembler Service API反匯編PDF檔案
seo-description: 使用Assembler Service API反匯編PDF檔案
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# 使用web service API {#disassemble-a-pdf-document-usingthe-web-service-api}解譯PDF檔案

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

使用Assembler Service API(web service)拆解PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms的伺服器的IP位址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞給AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將表AEM單用戶名分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存DDX檔案。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，該值代表DDX檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 參考要反匯編的PDF文檔。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存輸入的PDF檔案。 此`BLOB`對象作為參數傳遞給`invokeOneDocument`。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容，填充`BLOB`對象。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`對象。 此收集物件用來儲存要反匯編的PDF。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`key`欄位指派代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
   * 將儲存PDF檔案的`BLOB`物件指派至`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`欄位。
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`對象添加到`MyMapOf_xsd_string_To_xsd_anyType`對象。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的資料成員分配值，設定運行時選項以滿足您的業務要求。 例如，要指示Assembler服務在出現錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`欄位。

1. 反匯編PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * `BLOB`物件，代表DDX檔案，該檔案會分解PDF檔案
   * 包含要反匯編的PDF文檔的`MyMapOf_xsd_string_To_xsd_anyType`對象
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業結果和發生的任何例外。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是包含已拆解PDF檔案的`Map`物件。
   * 重複`Map`物件，以取得每個結果檔案。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 存取PDF檔案的`BLOB`物件的`MTOM`屬性，擷取代表PDF檔案的二進位資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[以程式設計方式解譯PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
