---
title: 以寫程式方式分解PDF文檔
seo-title: Programmatically Disassembling PDF Documents
description: 使用匯編程式服務可以使用Java API和Web服務API將單個PDF文檔分解為多個PDF文檔。
seo-description: Use the Assembler service to disassemble a single PDF document into multiple PDF documents using the Java API and the Web Service API.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 0%

---

# 以寫程式方式分解PDF文檔 {#programmatically-disassembling-pdf-documents}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

通過將PDF文檔傳遞到匯編服務，可以拆卸該文檔。 通常，當PDF文檔最初是從許多單個文檔（如語句集合）建立時，此任務非常有用。 在下圖中，DocA被劃分為多個結果文檔，其中頁面上的第一級書籤標識新結果文檔的開始。

![pd_pd_pdf書籤](assets/pd_pd_pdfsfrombookmarks.png)

要拆卸PDF文檔，請確保 `PDFsFromBookmarks` 元素位於DDX文檔中。 的 `PDFsFromBookmarks` 元素是結果元素，並且只能是 `DDX` 的子菜單。 它沒有 `result` 屬性，因為它可導致生成多個文檔。

的 `PDFsFromBookmarks` 元素將生成源文檔中每個1級書籤的單個文檔。

在本討論中，假定使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用匯編器服務來PDF文檔。 (請參閱 [以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>將單個PDF文檔傳遞到匯編器服務並返回單個文檔時，可以調用 `invokeOneDocument` 的下界。 但是，要拆卸PDF文檔，請使用 `invokeDDX` 操作，因為儘管一個輸入PDF文檔被傳遞給匯編器服務，但匯編器服務返回包含一個或多個文檔的集合對象。

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要分解PDF文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立PDF匯編器客戶端。
1. 引用現有DDX文檔。
1. 參照要拆卸的PDF文檔。
1. 設定運行時選項。
1. 分解PDF文檔。
1. 保存已拆卸的PDF文檔。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在非JBoss的受支援的J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。

**建立PDF匯編器客戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**引用現有DDX文檔**

必須引用DDX文檔來拆卸PDF文檔。 此DDX文檔必須包含 `PDFsFromBookmarks` 的子菜單。

**引用要拆卸的PDF文檔**

要拆卸PDF文檔，請參照表示要拆卸的PDF文檔的PDF檔案。 傳遞到匯編程式服務時，將為文檔中的每個1級書籤返回單獨的PDF文檔。

**設定運行時選項**

您可以設定運行時選項，這些選項在匯編程式服務執行作業時控制其行為。 例如，您可以設定一個選項，指示匯編程式服務在遇到錯誤時繼續處理作業。

**分解PDF文檔**

在建立匯編器服務客戶端、引用DDX文檔、引用要分解的PDF文檔和設定運行時選項後，您可以通過調用PDF文檔來分解匯編文檔 `invokeDDX` 的雙曲餘切值。 如果DDX文檔包含分解PDF文檔的說明，則匯編器服務將返回收集對象內已分解的PDF文檔。

**保存已拆卸的PDF文檔**

所有已拆卸的PDF文檔都在收集對象中返回。 循環訪問集合對象並將每個PDF文檔另存為PDF檔案。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API拆解PDF文檔 {#disassemble-a-pdf-document-using-the-java-api}

使用匯編程式服務API(Java)拆解PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用現有DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定DDX檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 參照要拆卸的PDF文檔。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象 `HashMap` 建構子。
   * 建立 `java.io.FileInputStream` 對象，使用其建構子，並將PDF文檔的位置傳遞到反匯編。
   * 建立 `com.adobe.idp.Document` 並傳遞 `java.io.FileInputStream` 包含要拆卸的PDF文檔的對象。
   * 向 `java.util.Map` 通過調用對象 `put` 方法並傳遞以下參數：

      * 表示鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
      * A `com.adobe.idp.Document` 包含要拆卸的PDF文檔的對象。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過調用屬於的方法來設定運行時選項以滿足業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 對象 `setFailOnError` 方法 `false`。

1. 分解PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下所需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含要拆卸的PDF文檔的對象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象，包括預設字型和作業日誌級別

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已拆卸的PDF文檔和發生的任何異常的對象。

1. 保存已拆卸的PDF文檔。

   要獲取已拆卸的PDF文檔，請執行以下操作：

   * 調用 `AssemblerResult` 對象 `getDocuments` 的雙曲餘切值。 這返回 `java.util.Map` 的雙曲餘切值。
   * 迭代 `java.util.Map` 直到找到結果 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取PDF文檔。

**另請參閱**

[以寫程式方式分解PDF文檔](#programmatically-disassembling-pdf-documents)

[快速啟動（SOAP模式）:使用Java API拆解PDF文檔](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API拆解PDF文檔 {#disassemble-a-pdf-document-using-the-web-service-api}

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

[以寫程式方式分解PDF文檔](#programmatically-disassembling-pdf-documents)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
