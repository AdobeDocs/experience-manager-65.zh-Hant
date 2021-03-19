---
title: 使用Bates編號組合文檔
seo-title: 使用Bates編號組合文檔
description: '使用Bates編號功能，使用Java和Web Service API來組合PDF檔案。 '
seo-description: '使用Bates編號功能，使用Java和Web Service API來組合PDF檔案。 '
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 0%

---


# 使用Bates編號{#assembling-documents-using-bates-numbering}組合文檔

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

您可以使用Bates編號來組合包含唯一頁面識別碼的PDF檔案。 *Bates編* 號是將唯一識別套用至一批相關檔案的方法。檔案（或檔案集）中的每個頁面都會指派一個Bates編號，以唯一識別頁面。 例如，包含物料清單資訊並與元件生產關聯的製造文檔可以包含標識符。 Bates數字包含循序遞增的數值，以及選用的首碼和字尾。 前置詞+數值+尾碼稱為&#x200B;*bates pattern*。

下圖顯示PDF檔案，其中包含位於檔案標題中的唯一識別碼。

![au_au_batesnumber](assets/au_au_batesnumber.png)

在此討論中，唯一的頁面識別碼會放在檔案的標題中。 假設使用下列DDX檔案。

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

此DDX檔案將名為&#x200B;*map.pdf*&#x200B;和&#x200B;*directions.pdf*&#x200B;的兩份PDF檔案合併為一份PDF檔案。 產生的PDF檔案包含由唯一頁面識別碼組成的頁首。 例如，上圖中的檔案顯示為000016。

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用Assembler服務來組合PDF檔案。 本節不討論這些概念，例如建立包含輸入文檔的集合對象，或從返回的集合對象中提取結果。 （請參閱[程式設計匯整PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)。）

>[!NOTE]
>
>有關Assembler服務的詳細資訊，請參見[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}摘要

要組合包含唯一頁面識別碼（Bates編號）的PDF文檔，請執行以下任務：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考輸入PDF檔案。
1. 設定初始Bates編號值。
1. 組合輸入的PDF檔案。
1. 擷取結果。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於部署了AEM Forms的J2EE應用程式伺服器的JAR檔案。 有關所有AEM FormsJAR檔案的位置資訊，請參見[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合PDF檔案。 例如，請考慮本節中介紹的DDX文檔。 要組合包含唯一頁面標識符的PDF文檔，DDX文檔必須包含`BatesNumber`元素。

**參考輸入PDF檔案**

必須參考輸入PDF檔案，才能組合PDF檔案。 例如，必須參考map.pdf和directions.pdf檔案，才能將這些PDF檔案組合為單一PDF檔案。

**設定初始Bates編號值**

您可以設定初始Bates編號值，以符合您的業務需求。 例如，假設需要將初始值設為000100。 如果您未設定初始值，則第一頁的值為000000。

**匯整輸入的PDF檔案**

在建立Assembler服務客戶端後，請參考包含`BatesNumber`元素資訊的DDX文檔、參考輸入的PDF文檔並設定運行時選項，您可以調用`invokeDDX`操作，使Assembler服務組合包含唯一頁標識符的PDF文檔。

**擷取結果**

Assembler服務返回包含作業結果的集合對象。 您可以擷取產生的PDF檔案，以及任何擲出的例外。 在這種情況下，加密的PDF檔案會位於系列物件中。

>[!NOTE]
>
>如果調用`invokeDDX`操作，則返回收集對象。 在將兩個或兩個以上輸入的PDF文檔傳遞至Assembler服務時，會使用此操作。 但是，如果只將一個輸入的PDF文檔傳遞到Assembler服務，則應調用`invokeOneDocument`操作。 有關使用此操作的資訊，請參閱[組合加密的PDF文檔](/help/forms/developing/assembling-encrypted-pdf-documents.md)。

**另請參閱**

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-documents-with-bates-numbering-using-the-java-api}以Bates編號組合檔案

使用Assembler Service API(Java)來組合使用唯一頁面識別碼（Bates編號）的PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 參考現有的DDX檔案。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 參考輸入PDF檔案。

   * 使用`HashMap`建構函式建立用來儲存輸入PDF檔案的`java.util.Map`物件。
   * 對於每個輸入的PDF檔案，請使用其建構函式並傳遞輸入的PDF檔案位置來建立`java.io.FileInputStream`物件。 在此情況下，請傳遞無擔保PDF檔案的位置。
   * 對於每個輸入的PDF文檔，請建立`com.adobe.idp.Document`對象並傳遞包含PDF文檔的`java.io.FileInputStream`對象。
   * 通過調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。 例如，本節中引入的DDX檔案中指定的PDF來源檔案名稱為Loan.pdf。
      * `com.adobe.idp.Document`物件，其中包含不安全的PDF檔案。

1. 設定初始Bates編號值。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 調用`AssemblerOptionSpec`物件的`setFirstBatesNumber`，並傳遞指定初始值的數值，以設定初始Bates編號。

1. 組合輸入的PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列必要值：

   * 代表DDX文檔的`com.adobe.idp.Document`對象。
   * `java.util.Map`物件，包含輸入的不安全PDF檔案。
   * 一個`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別。

   `invokeDDX`方法會傳回包含密碼加密PDF檔案的`com.adobe.livecycle.assembler.client.AssemblerResult`物件。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 此動作會傳回`java.util.Map`物件。
   * 重複`java.util.Map`物件，直到找到`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF檔案與bates編號組合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#assemble-documents-with-bates-numbering-using-the-web-service-api}以Bates編號組合檔案

使用Assembler Service API(web service)來組合使用唯一頁面識別碼（Bates編號）的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

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
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 參考輸入PDF檔案。

   * 對於每個輸入的PDF檔案，請使用其建構函式建立`BLOB`物件。 `BLOB`物件用來儲存輸入的PDF檔案。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表輸入PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`對象。 此收集物件用來儲存輸入的PDF檔案。
   * 對於每個輸入的PDF檔案，請建立`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。 例如，如果使用兩個輸入的PDF檔案，請建立兩個`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配代表鍵名的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。 （請對每個輸入的PDF檔案執行此工作。）
   * 將儲存PDF文檔的`BLOB`對象指定給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。 （請對每個輸入的PDF檔案執行此工作。）
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`對象添加到`MyMapOf_xsd_string_To_xsd_anyType`對象。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （請對每個輸入的PDF檔案執行此工作。）

1. 設定初始Bates編號值。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的`firstBatesNumber`資料成員分配一個數值來設定初始Bates數。

1. 組合輸入的PDF檔案。

   叫用`AssemblerServiceClient`物件的`invoke`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象。
   * 包含輸入PDF文檔的`MyMapOf_xsd_string_To_xsd_anyType`對象。 其鍵必須與PDF源檔案的名稱匹配，其值必須是與這些檔案對應的`BLOB`對象。
   * 指定運行時選項的`AssemblerOptionSpec`對象。

   `invoke`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何例外。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是包含結果PDF檔案的`Map`物件。
   * 重複`Map`物件，直到找到與結果檔案名稱相符的索引鍵。 然後將該陣列成員的`value`轉換為`BLOB`。
   * 存取PDF檔案的`BLOB`物件的`MTOM`屬性，擷取代表PDF檔案的二進位資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
