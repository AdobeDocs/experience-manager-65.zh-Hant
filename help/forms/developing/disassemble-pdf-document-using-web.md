---
title: 使用web service API拆解PDF檔案
seo-title: 使用web service API拆解PDF檔案
description: 'null'
seo-description: 'null'
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用web service API解譯PDF檔案 {#disassemble-a-pdf-document-usingthe-web-service-api}

使用Assembler Service API(web service)拆解PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

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
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，該值代表DDX檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 參考要反匯編的PDF文檔。

   * 使用其 `BLOB` 建構函式建立物件。 物件 `BLOB` 用來儲存輸入的PDF檔案。 此 `BLOB` 對象作為引數 `invokeOneDocument` 傳遞給。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 對象的欄位分 `MTOM` 配位元組陣列的內容來填充對象。
   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 此收集物件用來儲存要反匯編的PDF。
   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType_Item` 像。
   * 為物件欄位指派代表索引鍵名稱 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字串 `key` 值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。
   * 將儲 `BLOB` 存PDF檔案的物件指派至物 `MyMapOf_xsd_string_To_xsd_anyType_Item` 件的欄 `value` 位。
   * 將對象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 添加到對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 調用對 `MyMapOf_xsd_string_To_xsd_anyType` 像的方 `Add` 法並傳遞對 `MyMapOf_xsd_string_To_xsd_anyType` 像。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 通過為屬於該對象的資料成員分配值，設定運行時選項以滿足您的業務需 `AssemblerOptionSpec` 求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請指 `false` 派給 `AssemblerOptionSpec` 物件的欄 `failOnError` 位。

1. 反匯編PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列值：

   * 代 `BLOB` 表DDX文檔的對象，該PDF文檔會拆分
   * 包含 `MyMapOf_xsd_string_To_xsd_anyType` 要反匯編的PDF文檔的對象
   * 指定 `AssemblerOptionSpec` 運行時選項的對象
   該方 `invokeDDX` 法返回一個對 `AssemblerResult` 像，該對象包含作業結果和所發生的任何異常。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取物 `AssemblerResult` 件的欄 `documents` 位，此欄位是包含 `Map` 已拆解PDF檔案的物件。
   * 重複該對 `Map` 像，以獲得每個結果文檔。 然後，將該陣列成員轉 `value` 換為 `BLOB`。
   * 存取PDF檔案的物件屬性，以擷取代表PDF文 `BLOB` 件的二進位 `MTOM` 資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[以程式設計方式解譯PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
