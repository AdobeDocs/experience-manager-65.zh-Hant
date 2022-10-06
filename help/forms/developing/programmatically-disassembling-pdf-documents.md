---
title: 以寫程式方式分解PDF文檔
seo-title: Programmatically Disassembling PDF Documents
description: 使用組合器服務，使用Java API和Web服務API將單個PDF文檔拆解為多個PDF文檔。
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

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

通過將PDF文檔傳遞到組合器服務，可以拆解該文檔。 通常，當PDF文檔最初從許多單獨文檔（如語句集合）建立時，此任務很有用。 在下圖中，DocA被分為多個結果文檔，其中頁面上的第一級書籤標識新結果文檔的開始。

![pd_pd_pdf從書籤](assets/pd_pd_pdfsfrombookmarks.png)

要拆解PDF文檔，請確保 `PDFsFromBookmarks` 元素位於DDX文檔中。 此 `PDFsFromBookmarks` 元素是結果元素，只能是的子元素 `DDX` 元素。 沒有 `result` 屬性，因為它可產生多個檔案。

此 `PDFsFromBookmarks` 元素會為源文檔中的每個1級書籤生成單個文檔。

在本討論中，假設使用了以下DDX文檔。

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
>閱讀本節之前，建議您熟悉使用組合器服務來組合PDF文檔。 (請參閱 [以寫程式方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>將單個PDF文檔傳遞到組合器服務並返回單個文檔時，可以調用 `invokeOneDocument` 操作。 但是，要拆解PDF文檔，請使用 `invokeDDX` 操作，因為儘管將一個輸入PDF文檔傳遞到組合器服務，但組合器服務返回包含一個或多個文檔的集合對象。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

要拆解PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考要拆卸的PDF文檔。
1. 設定運行時選項。
1. 拆解PDF文檔。
1. 保存已拆解的PDF文檔。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

必須引用DDX文檔來拆解PDF文檔。 此DDX文檔必須包含 `PDFsFromBookmarks` 元素。

**參考要拆解的PDF文檔**

要拆解PDF文檔，請參考表示要拆解的PDF文檔的PDF檔案。 當傳遞到組合器服務時，將為文檔中的每個級別1書籤返回一個單獨的PDF文檔。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。

**拆解PDF文檔**

建立組合器服務客戶端後，參考DDX文檔，參考要拆解的PDF文檔，並設定運行時選項後，可以通過調用 `invokeDDX` 方法。 如果DDX文檔包含拆解PDF文檔的指令，則組合器服務返回收集對象內已拆解的PDF文檔。

**保存已拆解的PDF文檔**

所有已拆解的PDF文檔都返回在收集對象中。 逐一查看集合物件，並將每個PDF檔案儲存為PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API拆解PDF文檔 {#disassemble-a-pdf-document-using-the-java-api}

使用組合器服務API(Java)拆解PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞指定DDX檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 參考要拆卸的PDF文檔。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象，方法是使用 `HashMap` 建構子。
   * 建立 `java.io.FileInputStream` 對象，使用其建構子，並將PDF文檔的位置傳遞到反匯編。
   * 建立 `com.adobe.idp.Document` 物件，並傳遞 `java.io.FileInputStream` 包含要拆解的PDF文檔的對象。
   * 將項目新增至 `java.util.Map` 對象 `put` 方法，並傳遞下列引數：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
      * A `com.adobe.idp.Document` 包含要拆解的PDF文檔的對象。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 通過調用屬於的方法來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 物件 `setFailOnError` 方法和傳遞 `false`.

1. 拆解PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列必要值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含要拆解的PDF文檔的對象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象，包括預設字型和作業日誌級別

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已拆解的PDF文檔和發生的任何例外的對象。

1. 保存已拆解的PDF文檔。

   要獲取已拆解的PDF文檔，請執行以下操作：

   * 叫用 `AssemblerResult` 物件 `getDocuments` 方法。 這會傳回 `java.util.Map` 物件。
   * 重複 `java.util.Map` 對象，直到找到結果 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取PDF檔案。

**另請參閱**

[以寫程式方式分解PDF文檔](#programmatically-disassembling-pdf-documents)

[快速入門（SOAP模式）:使用Java API解譯PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API拆解PDF文檔 {#disassemble-a-pdf-document-using-the-web-service-api}

使用組合器服務API（web服務）拆解PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >取代 `localhost` 和托管AEM Forms之伺服器的IP位址。

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
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示DDX文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。

1. 參考要拆卸的PDF文檔。

   * 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存輸入PDF文檔。 此 `BLOB` 物件會傳遞至 `invokeOneDocument` 作為引數。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法，並傳遞位元組陣列、起始位置及流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 欄位位位元組陣列的內容。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此集合物件用於儲存要反匯編的PDF。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `key` 欄位。 此值必須與DDX文檔中指定的PDF源元素的值匹配。
   * 指派 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `value` 欄位。
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 為屬於的資料成員指定值，以設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 物件。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 物件 `failOnError` 欄位。

1. 拆解PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列值：

   * A `BLOB` 表示分解PDF文檔的DDX文檔的對象
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含要拆解的PDF文檔的對象
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含作業結果和發生的任何例外的對象。

1. 保存已拆解的PDF文檔。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 存取 `AssemblerResult` 物件 `documents` 欄位，即 `Map` 包含已拆解PDF文檔的對象。
   * 重複 `Map` 對象，以獲得每個生成的文檔。 然後，將陣列成員的 `value` 到 `BLOB`.
   * 通過訪問PDF文檔來提取代表文檔的二進位資料 `BLOB` 物件 `MTOM` 屬性。 這會傳回一個位元組陣列，您可將其寫出至PDF檔案。

**另請參閱**

[以寫程式方式分解PDF文檔](#programmatically-disassembling-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
