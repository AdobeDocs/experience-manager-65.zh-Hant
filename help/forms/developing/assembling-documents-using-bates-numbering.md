---
title: 使用Bates編號組合文檔
seo-title: Assembling Documents Using Bates Numbering
description: 使用Bates編號可使用Java和Web服務API匯編PDF文檔。
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

# 使用Bates編號組合文檔 {#assembling-documents-using-bates-numbering}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

可以使用Bates編號來匯編包含唯一頁面標識符的PDF文檔。 *貝茨編號* 是將唯一標識應用於一批相關文檔的方法。 文檔（或文檔集）中的每個頁面都分配了唯一標識該頁面的Bates編號。 例如，包含物料清單資訊並與元件生產相關聯的製造文檔可以包含標識符。 Bates數字包含一個按順序遞增的數字值以及一個可選前置詞和尾碼。 前置詞+數字+尾碼稱為 *貝茨模式*。

下圖顯示一個PDF文檔，該文檔包含位於文檔標題中的唯一標識符。

![au_au_batesnumber](assets/au_au_batesnumber.png)

為了進行此討論，將唯一的頁面標識符放置在文檔的標題中。 假定使用了以下DDX文檔。

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

此DDX文檔合併兩個名為 *地圖.pdf* 和 *方向.pdf* 一個PDF文檔。 結果PDF文檔包含由唯一頁面標識符組成的標題。 例如，上圖中的文檔顯示000016。

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用匯編器服務PDF文檔。 本節不討論這些概念，如建立包含輸入文檔的集合對象或從返回的集合對象中提取結果。 (請參閱 [以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要裝配包含唯一頁面標識符（Bates編號）的PDF文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立PDF匯編器客戶端。
1. 引用現有DDX文檔。
1. 引用輸入PDF文檔。
1. 設定初始Bates編號值。
1. 匯編輸入PDF文檔。
1. 提取結果。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援的J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署了AEM Forms的J2EE應用程式伺服器的JAR檔案。 有關所有AEM FormsJAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF匯編器客戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**引用現有DDX文檔**

必須引用DDX文檔來匯編PDF文檔。 例如，請考慮本節中介紹的DDX文檔。 要匯編包含唯一頁面標識符的PDF文檔，DDX文檔必須包含 `BatesNumber` 的子菜單。

**引用輸入PDF文檔**

必須引用輸入PDF文檔來匯編PDF文檔。 例如，必須引用map.pdf和directions.pdf文檔，才能將這些PDF文檔匯編為單個PDF文檔。

**設定初始Bates編號值**

您可以設定初始的Bates編號值以滿足您的業務要求。 例如，假定將初始值設定為000100是一項要求。 如果未設定初始值，則第一頁的值為000000。

**匯編輸入PDF文檔**

建立匯編器服務客戶端後，請參考包含 `BatesNumber` 元素資訊、引用輸入PDF文檔和設定運行時選項，您可以調用 `invokeDDX` 操作，該操作導致匯編器服務匯編包含唯一頁標識符的PDF文檔。

**提取結果**

匯編程式服務返回包含作業結果的集合對象。 可以提取結果PDF文檔和拋出的任何異常。 在這種情況下，加密的PDF文檔位於集合對象內。

>[!NOTE]
>
>如果調用 `invokeDDX` 的下界。 將兩個或多個輸入PDF文檔傳遞到匯編器服務時，將使用此操作。 但是，如果只將一個輸入PDF文檔傳遞給匯編器服務，則應調用 `invokeOneDocument` 的下界。 有關使用此操作的資訊，請參見 [組裝加密的PDF文檔](/help/forms/developing/assembling-encrypted-pdf-documents.md)。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API將文檔與Bates編號組合起來 {#assemble-documents-with-bates-numbering-using-the-java-api}

使用匯編器服務API(Java)匯編使用唯一頁標識符（Bates編號）的PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用現有DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定DDX檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 引用輸入PDF文檔。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象 `HashMap` 建構子。
   * 對於每個輸入PDF文檔，建立 `java.io.FileInputStream` 使用其建構子並傳遞輸入PDF文檔的位置。 在此情況下，請傳遞無擔保PDF文檔的位置。
   * 對於每個輸入PDF文檔，建立 `com.adobe.idp.Document` 並傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。
   * 向 `java.util.Map` 通過調用對象 `put` 方法並傳遞以下參數：

      * 表示鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 例如，在本節介紹的DDX文檔中指定的PDF源檔案的名稱是Loan.pdf。
      * A `com.adobe.idp.Document` 包含不安全PDF文檔的對象。

1. 設定初始Bates編號值。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過調用 `AssemblerOptionSpec` 對象 `setFirstBatesNumber` 並傳遞一個指定初始值的數值。

1. 匯編輸入PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下所需值：

   * A `com.adobe.idp.Document` 表示DDX文檔的對象。
   * A `java.util.Map` 包含輸入不安全PDF檔案的對象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項（包括預設字型和作業日誌級別）的對象。

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含密碼加密PDF文檔的對象。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 調用 `AssemblerResult` 對象 `getDocuments` 的雙曲餘切值。 此操作返回 `java.util.Map` 的雙曲餘切值。
   * 迭代 `java.util.Map` 直到找到 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取PDF文檔。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API將PDF文檔與bates編號一起裝配](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API將文檔與Bates編號組合起來 {#assemble-documents-with-bates-numbering-using-the-web-service-api}

使用匯編器服務API（Web服務）匯編使用唯一頁面標識符（Bates編號）的PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

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
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值（該字串值表示DDX文檔的檔案位置和開啟檔案的模式）來對對象。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 引用輸入PDF文檔。

   * 對於每個輸入PDF文檔，建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存輸入PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 此集合對象用於儲存輸入PDF文檔。
   * 對於每個輸入PDF文檔，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。 例如，如果使用兩個輸入PDF文檔，則建立兩個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象。
   * 為指定表示鍵名的字串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `key` 的子菜單。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 (為每個輸入PDF文檔執行此任務。)
   * 分配 `BLOB` 將PDF文檔儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `value` 的子菜單。 (為每個輸入PDF文檔執行此任務。)
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 調用 `MyMapOf_xsd_string_To_xsd_anyType` 對象 `Add` 方法和通過 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 (為每個輸入PDF文檔執行此任務。)

1. 設定初始Bates編號值。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過為Bates編號分配數值 `firstBatesNumber` 屬於的資料成員 `AssemblerOptionSpec` 的雙曲餘切值。

1. 匯編輸入PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invoke` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象。
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含輸入PDF文檔的對象。 其鍵必須與PDF源檔案的名稱匹配，其值必須為 `BLOB` 與這些檔案對應的對象。
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象。

   的 `invoke` 方法返回 `AssemblerResult` 包含作業結果和所發生的任何異常的對象。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問 `AssemblerResult` 對象 `documents` 欄位， `Map` 包含結果PDF文檔的對象。
   * 迭代 `Map` 對象，直到找到與結果文檔的名稱匹配的鍵。 然後轉換該陣列成員 `value` 到 `BLOB`。
   * 通過訪問PDF文檔來提取表示該文檔的二進位資料 `BLOB` 對象 `MTOM` 屬性。 這將返回可以寫入PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
