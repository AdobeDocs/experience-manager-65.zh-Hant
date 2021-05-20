---
title: 使用Bates編號來裝配文檔
seo-title: 使用Bates編號來裝配文檔
description: '使用Bates編號功能，使用Java和Web服務API來組合PDF檔案。 '
seo-description: '使用Bates編號功能，使用Java和Web服務API來組合PDF檔案。 '
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
source-wordcount: '1941'
ht-degree: 0%

---

# 使用Bates編號{#assembling-documents-using-bates-numbering}裝配文檔

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以使用Bates編號來組合包含唯一頁面識別碼的PDF檔案。 *Bates* 編號是將唯一標識應用到一批相關文檔的方法。文檔（或一組文檔）中的每個頁面都被分配一個Bates編號，該編號唯一標識該頁面。 例如，包含物料清單資訊且與元件生產相關聯的製造文檔可以包含標識符。 Bates數字包含循序遞增的數值以及選用的前置詞和尾碼。 前置詞+數值+尾碼稱為&#x200B;*bates模式*。

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

此DDX文檔將名為&#x200B;*map.pdf*&#x200B;和&#x200B;*directions.pdf*&#x200B;的兩個PDF文檔合併為單個PDF文檔。 生成的PDF文檔包含由唯一頁標識符組成的標題。 例如，上圖中的檔案顯示000016。

>[!NOTE]
>
>閱讀本節之前，建議您先熟悉使用組合器服務組合PDF文檔。 本節不討論這些概念，例如建立包含輸入文檔的集合對象，或從返回的集合對象中提取結果。 （請參閱[以程式設計方式組合PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)。）

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}的摘要

要組合包含唯一頁標識符（Bates編號）的PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考輸入的PDF文檔。
1. 設定初始Bates編號值。
1. 組合輸入的PDF文檔。
1. 提取結果。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

如果AEM Forms部署在JBoss以外的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案。 有關所有AEM Forms JAR檔案的位置資訊，請參閱[包含AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，必須建立組合器服務客戶端。

**參考現有的DDX文檔**

必須參考DDX文檔才能組合PDF文檔。 例如，請考量本節中引入的DDX檔案。 要組合包含唯一頁標識符的PDF文檔，DDX文檔必須包含`BatesNumber`元素。

**參考輸入PDF文檔**

必須參考輸入的PDF文檔才能組合PDF文檔。 例如，必須參考map.pdf和directions.pdf文檔，才能將這些PDF文檔組合為單個PDF文檔。

**設定初始Bates數字值**

您可以設定初始的Bates編號值以符合您的業務要求。 例如，假設需要將初始值設為000100。 若您未設定初始值，則第一頁的值為000000。

**組合輸入的PDF文檔**

建立組合器服務客戶端後，請參考包含`BatesNumber`元素資訊的DDX文檔、引用輸入的PDF文檔和設定運行時選項，您可以調用`invokeDDX`操作，該操作導致組合器服務組合包含唯一頁標識符的PDF文檔。

**擷取結果**

組合器服務返回包含作業結果的集合對象。 您可以擷取產生的PDF檔案，以及擲回的任何例外。 在此情況下，加密的PDF檔案會位於收集物件中。

>[!NOTE]
>
>如果調用`invokeDDX`操作，則返回集合對象。 將兩個或多個輸入PDF文檔傳遞到組合器服務時，將使用此操作。 但是，如果只將一個輸入PDF文檔傳遞到組合器服務，則應調用`invokeOneDocument`操作。 有關使用此操作的資訊，請參閱[組合加密的PDF文檔](/help/forms/developing/assembling-encrypted-pdf-documents.md)。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-documents-with-bates-numbering-using-the-java-api}以Bates編號組合文檔

使用組合器服務API(Java)來組合使用唯一頁標識符（Bates編號）的PDF文檔：

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 參考現有的DDX文檔。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 參考輸入的PDF文檔。

   * 使用`HashMap`建構函式建立用於儲存輸入PDF文檔的`java.util.Map`對象。
   * 對於每個輸入PDF文檔，使用其建構子並傳遞輸入PDF文檔的位置來建立`java.io.FileInputStream`對象。 在此情況下，請傳遞不安全PDF檔案的位置。
   * 對於每個輸入的PDF文檔，建立`com.adobe.idp.Document`對象，並傳遞包含PDF文檔的`java.io.FileInputStream`對象。
   * 調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象中：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 例如，本節中引入的DDX檔案中指定的PDF源檔案名稱為Loan.pdf。
      * `com.adobe.idp.Document`物件，包含不安全的PDF檔案。

1. 設定初始Bates編號值。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 調用`AssemblerOptionSpec`對象的`setFirstBatesNumber`並傳遞指定初始值的數值，以設定初始Bates編號。

1. 組合輸入的PDF文檔。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下必需值：

   * 代表DDX文檔的`com.adobe.idp.Document`對象。
   * `java.util.Map`物件，包含輸入的不安全PDF檔案。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別。

   `invokeDDX`方法返回包含密碼加密PDF文檔的`com.adobe.livecycle.assembler.client.AssemblerResult`對象。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 調用`AssemblerResult`對象的`getDocuments`方法。 此動作會傳回`java.util.Map`物件。
   * 逐一查看`java.util.Map`物件，直到找到`com.adobe.idp.Document`物件。
   * 調用`com.adobe.idp.Document`對象的`copyToFile`方法以提取PDF文檔。

**另請參閱**

[快速入門（SOAP模式）:使用Java API以Bates編號方式組裝PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#assemble-documents-with-bates-numbering-using-the-web-service-api}使用Bates編號組合文檔

使用組合器服務API（Web服務）來組合使用唯一頁標識符（Bates編號）的PDF文檔：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

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
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 參考輸入的PDF文檔。

   * 對於每個輸入的PDF文檔，使用其建構子建立`BLOB`對象。 `BLOB`對象用於儲存輸入的PDF文檔。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此收集對象用於儲存輸入的PDF文檔。
   * 對於每個輸入的PDF文檔，建立`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。 例如，如果使用兩個輸入的PDF文檔，請建立兩個`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配表示鍵名的字串值。 此值必須與DDX文檔中指定的PDF源元素的值匹配。 （對每個輸入的PDF文檔執行此任務。）
   * 將儲存PDF文檔的`BLOB`對象指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。 （對每個輸入的PDF文檔執行此任務。）
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （對每個輸入的PDF文檔執行此任務。）

1. 設定初始Bates編號值。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 為屬於`AssemblerOptionSpec`對象的`firstBatesNumber`資料成員分配一個數值，以設定初始Bates編號。

1. 組合輸入的PDF文檔。

   調用`AssemblerServiceClient`對象的`invoke`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象。
   * 包含輸入PDF文檔的`MyMapOf_xsd_string_To_xsd_anyType`對象。 其鍵必須與PDF源檔案的名稱匹配，且其值必須是與這些檔案對應的`BLOB`對象。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invoke`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何異常。

1. 提取結果。

   要獲取新建立的PDF文檔，請執行以下操作：

   * 訪問`AssemblerResult`對象的`documents`欄位，該欄位是包含結果PDF文檔的`Map`對象。
   * 逐一查看`Map`對象，直到找到與結果文檔的名稱匹配的鍵。 然後將該陣列成員的`value`轉換為`BLOB`。
   * 通過訪問其`BLOB`對象的`MTOM`屬性來提取表示PDF文檔的二進位資料。 這會傳回可寫出為PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
