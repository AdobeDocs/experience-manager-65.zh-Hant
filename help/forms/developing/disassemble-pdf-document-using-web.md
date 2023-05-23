---
title: 使用Web服務API拆解PDF文檔
seo-title: Disassemble a PDF document usingthe web service API
description: 使用匯編程式服務API拆解PDF文檔
seo-description: Disassemble a PDF document using the Assembler Service API
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
role: Developer
exl-id: de2f90ad-5dea-40a0-8c6d-d6b08228310d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# 使用Web服務API拆解PDF文檔 {#disassemble-a-pdf-document-usingthe-web-service-api}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

使用匯編程式服務API（Web服務）拆解PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 請確保在設定服務引用時使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

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
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 參照要拆卸的PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存輸入PDF文檔。 此 `BLOB` 對象被傳遞到 `invokeOneDocument` 作為論據。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位位元組陣列的內容。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 此集合對象用於儲存要拆卸的PDF。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。
   * 為指定表示鍵名的字串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `key` 的子菜單。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
   * 分配 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `value` 的子菜單。
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 調用 `MyMapOf_xsd_string_To_xsd_anyType` 對象 `Add` 方法和通過 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過將值分配給屬於的資料成員來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編程式服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 對象 `failOnError` 的子菜單。

1. 分解PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `BLOB` 表示分解PDF文檔的DDX文檔的對象
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含要拆卸的PDF文檔的對象
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作業結果和發生的任何異常的對象。

1. 保存已拆卸的PDF文檔。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問 `AssemblerResult` 對象 `documents` 欄位， `Map` 包含已拆卸的PDF文檔的對象。
   * 迭代 `Map` 對象，以獲取每個結果文檔。 然後，將該陣列成員 `value` 到 `BLOB`。
   * 通過訪問PDF文檔來提取表示該文檔的二進位資料 `BLOB` 對象 `MTOM` 屬性。 這將返回可以寫入PDF檔案的位元組陣列。

**另請參閱**

[以寫程式方式分解PDF文檔](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
