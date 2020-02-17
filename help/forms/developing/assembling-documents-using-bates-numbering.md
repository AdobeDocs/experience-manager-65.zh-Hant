---
title: 使用Bates編號組合文檔
seo-title: 使用Bates編號組合文檔
description: 'null'
seo-description: 'null'
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 使用Bates編號組合文檔 {#assembling-documents-using-bates-numbering}

您可以使用Bates編號來組合包含唯一頁面識別碼的PDF檔案。 *Bates編號* （Bates編號）是將唯一標識應用到一批相關文檔的方法。 檔案（或檔案集）中的每個頁面都會指派一個Bates編號，以唯一識別頁面。 例如，包含物料清單資訊並與元件生產關聯的製造文檔可以包含標識符。 Bates數字包含循序遞增的數值，以及選用的首碼和字尾。 前置詞+數值+尾碼稱為 *Bates模式*。

下圖顯示PDF檔案，其中包含位於檔案標題中的唯一識別碼。

![au_au_batesnumber](assets/au_au_batesnumber.png)

在此討論中，唯一的頁面識別碼會放在檔案的標題中。 假設使用下列DDX檔案。

```as3
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

此DDX檔案將兩份名為 *map.pdf* 和 ** directions.pdf的PDF檔案合併為單一PDF檔案。 產生的PDF檔案包含由唯一頁面識別碼組成的頁首。 例如，上圖中的檔案顯示為000016。

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用Assembler服務來組合PDF檔案。 本節不討論這些概念，例如建立包含輸入文檔的集合對象，或從返回的集合對象中提取結果。 (請參閱 [以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參 [閱Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

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
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如果AEM Forms部署在JBoss以外的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為JAR檔案，此為部署AEM Forms的J2EE應用程式伺服器專屬檔案。 如需所有AEM Forms JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合PDF檔案。 例如，請考慮本節中介紹的DDX文檔。 要組合包含唯一頁面標識符的PDF文檔，DDX文檔必須包含該 `BatesNumber` 元素。

**參考輸入PDF檔案**

必須參考輸入PDF檔案，才能組合PDF檔案。 例如，必須參考map.pdf和directions.pdf檔案，才能將這些PDF檔案組合為單一PDF檔案。

**設定初始Bates編號值**

您可以設定初始Bates編號值，以符合您的業務需求。 例如，假設需要將初始值設為000100。 如果您未設定初始值，則第一頁的值為000000。

**匯整輸入的PDF檔案**

建立Assembler服務客戶端後，請參考包含元素資訊的DDX文檔、參考輸入的 `BatesNumber``invokeDDX` PDF文檔並設定運行時選項，您可以調用導致Assembler服務組合包含唯一頁標識符的PDF文檔的操作。

**擷取結果**

Assembler服務返回包含作業結果的集合對象。 您可以擷取產生的PDF檔案，以及任何擲出的例外。 在這種情況下，加密的PDF檔案會位於系列物件中。

>[!NOTE]
>
>如果您叫用此操作，則會傳回系列 `invokeDDX` 物件。 在將兩個或兩個以上輸入的PDF文檔傳遞至Assembler服務時，會使用此操作。 但是，如果只將一個輸入的PDF文檔傳遞給Assembler服務，則應調用該操 `invokeOneDocument` 作。 如需使用此作業的詳細資訊，請參 [閱組合加密的PDF檔案](/help/forms/developing/assembling-encrypted-pdf-documents.md)。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API以Bates編號組合檔案 {#assemble-documents-with-bates-numbering-using-the-java-api}

使用Assembler Service API(Java)來組合使用唯一頁面識別碼（Bates編號）的PDF檔案：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `AssemblerServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考現有的DDX檔案。

   * 使用 `java.io.FileInputStream` 其建構子並傳遞指定DDX檔案位置的字串值，建立表示DDX文檔的對象。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 參考輸入PDF檔案。

   * 使用建 `java.util.Map` 構函式建立用來儲存輸入PDF檔案的物 `HashMap` 件。
   * 對於每個輸入的PDF檔案，請使 `java.io.FileInputStream` 用其建構函式並傳遞輸入的PDF檔案位置來建立物件。 在此情況下，請傳遞無擔保PDF檔案的位置。
   * 對於每個輸入的PDF檔案，請建 `com.adobe.idp.Document` 立物件並傳遞包 `java.io.FileInputStream` 含PDF檔案的物件。
   * 通過調用對象的方 `java.util.Map` 法並傳遞以 `put` 下參數，向對象添加條目：

      * 代表索引鍵名稱的字串值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。 例如，本節中引入的DDX檔案中指定的PDF來源檔案名稱為Loan.pdf。
      * 包 `com.adobe.idp.Document` 含不安全PDF文檔的對象。

1. 設定初始Bates編號值。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 調用物件並傳遞指定初始值 `AssemblerOptionSpec` 的數值， `setFirstBatesNumber` 以設定初始Bates編號。

1. 組合輸入的PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invokeDDX` 法並傳遞下列必要值：

   * 表 `com.adobe.idp.Document` 示DDX文檔的對象。
   * 包 `java.util.Map` 含輸入不安全PDF檔案的物件。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 運行時選項（包括預設字型和作業日誌級別）的對象。
   此方 `invokeDDX` 法會傳回包 `com.adobe.livecycle.assembler.client.AssemblerResult` 含密碼加密PDF檔案的物件。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的方 `getDocuments` 法。 此動作會傳回 `java.util.Map` 物件。
   * 重複該對 `java.util.Map` 像，直到找到該對 `com.adobe.idp.Document` 像。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法以擷取PDF檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API將PDF檔案與bates編號組合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API使用Bates編號來組合檔案 {#assemble-documents-with-bates-numbering-using-the-web-service-api}

使用Assembler Service API(web service)來組合使用唯一頁面識別碼（Bates編號）的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

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
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示DDX文檔的檔案位置以及在中開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 參考輸入PDF檔案。

   * 對於每個輸入的PDF檔案，請使用 `BLOB` 其建構函式來建立物件。 物件 `BLOB` 用來儲存輸入的PDF檔案。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表輸入PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。
   * 建立對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 此收集物件用來儲存輸入的PDF檔案。
   * 對於每個輸入的PDF檔案，請建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。 例如，如果使用兩個輸入的PDF檔案，請建立兩個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 為對象欄位指定代表鍵名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字串 `key` 值。 此值必須與DDX檔案中指定之PDF來源元素的值相符。 （請對每個輸入的PDF檔案執行此工作。）
   * 將存 `BLOB` 儲PDF文檔的對象指 `MyMapOf_xsd_string_To_xsd_anyType_Item` 派到對 `value` 像欄位。 （請對每個輸入的PDF檔案執行此工作。）
   * 將對象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 添加到對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 調用對 `MyMapOf_xsd_string_To_xsd_anyType` 像的方 `Add` 法並傳遞對 `MyMapOf_xsd_string_To_xsd_anyType` 像。 （請對每個輸入的PDF檔案執行此工作。）

1. 設定初始Bates編號值。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 通過為屬於對象的資料成員分配數 `firstBatesNumber` 值來設定初始Bates `AssemblerOptionSpec` 編號。

1. 組合輸入的PDF檔案。

   叫用物 `AssemblerServiceClient` 件的方 `invoke` 法並傳遞下列值：

   * 表 `BLOB` 示DDX文檔的對象。
   * 包 `MyMapOf_xsd_string_To_xsd_anyType` 含輸入PDF檔案的物件。 其鍵必須與PDF源檔案的名稱匹配，其值必須是與這些文 `BLOB` 件對應的對象。
   * 指定 `AssemblerOptionSpec` 運行時選項的對象。
   該方 `invoke` 法返回 `AssemblerResult` 一個對象，該對象包含作業結果和所發生的任何異常。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取物 `AssemblerResult` 件的欄 `documents` 位，此欄位是包含 `Map` 結果PDF檔案的物件。
   * 重複該對 `Map` 像，直到找到與生成文檔的名稱匹配的鍵。 然後將該陣列成員轉 `value` 換為 `BLOB`。
   * 存取PDF檔案的物件屬性，以擷取代表PDF文 `BLOB` 件的二進位 `MTOM` 資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
