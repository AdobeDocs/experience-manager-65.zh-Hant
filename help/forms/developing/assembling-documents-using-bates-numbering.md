---
title: 使用Bates編號來裝配文檔
seo-title: Assembling Documents Using Bates Numbering
description: 使用Bates編號來使用Java和Web服務API來組合PDF文檔。
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 0%

---

# 使用Bates編號來裝配文檔 {#assembling-documents-using-bates-numbering}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以使用Bates編號來組合包含唯一頁標識符的PDF文檔。 *Bates編號* 是將唯一識別套用至一批相關檔案的方法。 文檔（或一組文檔）中的每個頁面都被分配一個Bates編號，該編號唯一標識該頁面。 例如，包含物料清單資訊且與元件生產相關聯的製造文檔可以包含標識符。 Bates數字包含循序遞增的數值以及選用的前置詞和尾碼。 前置詞+數值+尾碼稱為 *Bates模式*.

下圖顯示的PDF文檔包含位於文檔標題中的唯一標識符。

![au_au_batenumber](assets/au_au_batesnumber.png)

就本討論而言，唯一的頁面標識符會放在文檔的標題中。 假設使用以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

此DDX文檔將合併兩個PDF文檔，命名為 *map.pdf* 和 *directions.pdf* 整合到單一PDF檔案中。 生成的PDF文檔包含由唯一頁標識符組成的標題。 例如，上圖中的檔案顯示000016。

>[!NOTE]
>
>閱讀本節之前，建議您熟悉使用組合器服務來組合PDF文檔。 本節不討論這些概念，例如建立包含輸入文檔的集合對象，或從返回的集合對象中提取結果。 (請參閱 [以寫程式方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

要組合包含唯一頁標識符的PDF文檔（Bates編號），請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考輸入PDF文檔。
1. 設定初始Bates編號值。
1. 組合輸入PDF文檔。
1. 提取結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在JBoss以外的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。 如需所有AEM Forms JAR檔案位置的相關資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

必須引用DDX文檔來組合PDF文檔。 例如，請考量本節中引入的DDX檔案。 要組合包含唯一頁標識符的PDF文檔，DDX文檔必須包含 `BatesNumber` 元素。

**參考輸入PDF文檔**

必須引用輸入PDF文檔來組合PDF文檔。 例如，必須參考map.pdf和directions.pdf檔案，才能將這些PDF檔案組合成單一PDF檔案。

**設定初始Bates數字值**

您可以設定初始的Bates編號值以符合您的業務要求。 例如，假設需要將初始值設為000100。 若您未設定初始值，則第一頁的值為000000。

**組合輸入PDF文檔**

建立組合器服務客戶端後，請參考包含的DDX文檔 `BatesNumber` 元素資訊、引用輸入PDF文檔和設定運行時選項，可以調用 `invokeDDX` 操作，該操作導致組合器服務組合包含唯一頁標識符的PDF文檔。

**擷取結果**

組合器服務返回包含作業結果的集合對象。 您可以擷取產生的PDF檔案，以及擲回的任何例外。 在此情況下，加密的PDF文檔位於收集對象中。

>[!NOTE]
>
>如果您叫用 `invokeDDX` 操作。 將兩個或多個輸入PDF文檔傳遞到組合器服務時，將使用此操作。 但是，如果只將一個輸入PDF文檔傳遞到組合器服務，則應調用 `invokeOneDocument` 操作。 如需使用此操作的詳細資訊，請參閱 [組裝加密的PDF文檔](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API使用Bates編號來組合文檔 {#assemble-documents-with-bates-numbering-using-the-java-api}

使用組合器服務API(Java)來組合使用唯一頁標識符（Bates編號）的PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞指定DDX檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 對象，使用其建構子並傳遞 `java.io.FileInputStream` 物件。

1. 參考輸入PDF文檔。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象，方法是使用 `HashMap` 建構子。
   * 對於每個輸入PDF文檔，建立 `java.io.FileInputStream` 對象，使用其建構子並傳遞輸入PDF文檔的位置。 在此情況下，請傳遞不安全PDF檔案的位置。
   * 對於每個輸入PDF文檔，建立 `com.adobe.idp.Document` 物件，並傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。
   * 將項目新增至 `java.util.Map` 對象 `put` 方法，並傳遞下列引數：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 例如，本節中引入的DDX文檔中指定的PDF源檔案的名稱為Loan.pdf。
      * A `com.adobe.idp.Document` 包含不安全PDF文檔的對象。

1. 設定初始Bates編號值。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 叫用 `AssemblerOptionSpec` 物件 `setFirstBatesNumber` 並傳遞指定初始值的數值。

1. 組合輸入PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invokeDDX` 方法，並傳遞下列必要值：

   * A `com.adobe.idp.Document` 表示DDX文檔的對象。
   * A `java.util.Map` 包含輸入不安全PDF檔案的對象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象，包括預設字型和作業日誌級別。

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含密碼加密PDF文檔的對象。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 叫用 `AssemblerResult` 物件 `getDocuments` 方法。 此動作會傳回 `java.util.Map` 物件。
   * 重複 `java.util.Map` 物件，直到您找到 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法來擷取PDF檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API以Bates編號組合PDF文檔](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API使用Bates編號來組合文檔 {#assemble-documents-with-bates-numbering-using-the-web-service-api}

通過使用組合器服務API（Web服務）來組合使用唯一頁標識符（Bates編號）的PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置以及在中開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 位元組陣列內容的欄位。

1. 參考輸入PDF文檔。

   * 對於每個輸入PDF文檔，建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存輸入PDF文檔。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 填入 `BLOB` 對象，通過賦值 `MTOM` 屬性（包含位元組陣列的內容）。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此收集對象用於儲存輸入PDF文檔。
   * 對於每個輸入PDF文檔，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。 例如，如果使用兩個輸入PDF檔案，請建立兩個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `key` 欄位。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 (對每個輸入PDF文檔執行此任務。)
   * 指派 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `value` 欄位。 (對每個輸入PDF文檔執行此任務。)
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` 物件 `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 (對每個輸入PDF文檔執行此任務。)

1. 設定初始Bates編號值。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存執行時選項的物件。
   * 為 `firstBatesNumber` 屬於的資料成員 `AssemblerOptionSpec` 物件。

1. 組合輸入PDF文檔。

   叫用 `AssemblerServiceClient` 物件 `invoke` 方法，並傳遞下列值：

   * A `BLOB` 表示DDX文檔的對象。
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含輸入PDF文檔的對象。 其鍵必須與PDF源檔案的名稱匹配，且其值必須為 `BLOB` 對應於這些檔案的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   此 `invoke` 方法傳回 `AssemblerResult` 包含作業結果的對象以及發生的任何例外。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 存取 `AssemblerResult` 物件 `documents` 欄位，即 `Map` 包含結果PDF文檔的對象。
   * 重複 `Map` 對象，直到找到與生成文檔的名稱匹配的鍵。 然後將該陣列成員的 `value` 到 `BLOB`.
   * 通過訪問PDF文檔來提取代表文檔的二進位資料 `BLOB` 物件 `MTOM` 屬性。 這會傳回一個位元組陣列，您可將其寫出至PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
