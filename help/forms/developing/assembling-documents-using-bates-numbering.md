---
title: 使用Bates編號來組合檔案
description: 使用Bates編號，以使用Java和Web服務API組合PDF檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# 使用Bates編號來組合檔案 {#assembling-documents-using-bates-numbering}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以使用Bates編號來組合包含唯一頁面識別碼的PDF檔案。 *Bates編號*&#x200B;是將唯一識別套用至一整批相關檔案的方法。 檔案（或檔案集）中的每一頁都會指定唯一識別該頁面的Bates編號。 例如，包含用料表資訊且與組裝料號生產相關聯的製造檔案可以包含識別碼。 Bates數字包含循序遞增的數值，以及選用的首碼和尾碼。 前置詞+數值+後置詞稱為&#x200B;*bates模式*。

下圖顯示的PDF檔案在檔案標題中包含唯一識別碼。

![au_au_batesnumber](assets/au_au_batesnumber.png)

為了進行此討論，唯一頁面識別碼會放置在檔案的頁首中。 假設使用下列DDX檔案。

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

此DDX檔案將兩個名為&#x200B;*map.pdf*&#x200B;和&#x200B;*directions.pdf*&#x200B;的PDF檔案合併為單一PDF檔案。 產生的PDF檔案包含由唯一頁面識別碼組成的標頭。 例如，上圖中的檔案顯示000016。

>[!NOTE]
>
>閱讀本節之前，建議您先熟悉使用Assembler服務組合PDF檔案。 本節不討論概念，例如建立包含輸入檔案的集合物件，或從傳回的集合物件中擷取結果。 (請參閱[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱[組合器服務與DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

若要組合包含唯一頁面識別碼（Bates編號）的PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考輸入PDF檔案。
1. 設定初始Bates數字值。
1. 組合輸入PDF檔案。
1. 擷取結果。

**包含專案檔**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立PDF組合器使用者端**

您必須先建立組合器服務使用者端，才能以程式設計方式執行組合器作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDF檔案。 例如，以本節介紹的DDX檔案為例。 若要組合包含唯一頁面識別碼的PDF檔案，DDX檔案必須包含`BatesNumber`元素。

**參考輸入PDF檔案**

必須參考輸入PDF檔案才能組合PDF檔案。 例如，必須參照map.pdf和directions.pdf檔案，才能將這些PDF檔案組合成單一PDF檔案。

**設定初始Bates數字值**

您可以設定初始Bates編號值，以符合您的業務需求。 例如，假設需要將初始值設為000100。 如果您未設定初始值，則會顯000000第一頁的值。

**組合輸入PDF檔案**

建立Assembler服務使用者端、參照包含`BatesNumber`專案資訊的DDX檔案、參照輸入PDF檔案，以及設定執行階段選項之後，您可以叫用`invokeDDX`作業，使Assembler服務組合包含唯一頁面識別碼的PDF檔案。

**擷取結果**

Assembler服務會傳回包含工作結果的集合物件。 您可以擷取產生的PDF檔案以及擲回的任何例外狀況。 在此情況下，加密的PDF檔案會位於集合物件內。

>[!NOTE]
>
>如果您叫用`invokeDDX`作業，會傳回集合物件。 將兩個或多個輸入PDF檔案傳遞至Assembler服務時，會使用此作業。 不過，如果您只傳遞一個輸入PDF檔案給組合器服務，您應該叫用`invokeOneDocument`作業。 如需有關使用此作業的資訊，請參閱[組合加密的PDF檔案](/help/forms/developing/assembling-encrypted-pdf-documents.md)。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API以Bates編號組合檔案 {#assemble-documents-with-bates-numbering-using-the-java-api}

使用Assembler Service API (Java)來組合使用唯一頁面識別碼（Bates編號）的PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`AssemblerServiceClient`物件。

1. 參考現有的DDX檔案。

   * 使用它的建構函式並傳遞指定DDX檔案位置的字串值，建立代表DDX檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 參考輸入PDF檔案。

   * 使用`HashMap`建構函式建立用來儲存輸入PDF檔案的`java.util.Map`物件。
   * 對於每個輸入PDF檔案，使用其建構函式並傳遞輸入PDF檔案的位置來建立`java.io.FileInputStream`物件。 在此情況下，請傳送不安全PDF檔案的位置。
   * 針對每個輸入PDF檔案，建立`com.adobe.idp.Document`物件並傳遞包含PDF檔案的`java.io.FileInputStream`物件。
   * 透過叫用物件的`put`方法並傳遞下列引數，將專案新增至`java.util.Map`物件：

      * 代表索引鍵名稱的字串值。 此值必須符合DDX檔案中指定的PDF來源元素的值。 例如，本節介紹的DDX檔案中指定的PDF來源檔案名稱為Loan.pdf。
      * 包含不安全PDF檔案的`com.adobe.idp.Document`物件。

1. 設定初始Bates數字值。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 透過叫用`AssemblerOptionSpec`物件的`setFirstBatesNumber`並傳遞指定初始值的數值來設定初始Bates數字。

1. 組合輸入PDF檔案。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法，並傳遞下列必要值：

   * 代表DDX檔案的`com.adobe.idp.Document`物件。
   * 包含輸入不安全PDF檔案的`java.util.Map`物件。
   * 指定執行階段選項（包括預設字型和作業記錄層級）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件。

   `invokeDDX`方法傳回包含密碼加密PDF檔案的`com.adobe.livecycle.assembler.client.AssemblerResult`物件。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 此動作傳回`java.util.Map`物件。
   * 逐一檢視`java.util.Map`物件，直到找到`com.adobe.idp.Document`物件為止。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF檔案。

**另請參閱**

[快速入門(SOAP模式)：使用Java API組合Bates編號的PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API以Bates編號組合檔案 {#assemble-documents-with-bates-numbering-using-the-web-service-api}

使用Assembler Service API （Web服務）來組合使用唯一頁面識別碼（Bates編號）的PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立PDF組合器使用者端。

   * 使用預設建構函式建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。
   * 取得`AssemblerServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存DDX檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表DDX檔案檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 參考輸入PDF檔案。

   * 對於每個輸入PDF檔案，使用其建構函式來建立`BLOB`物件。 `BLOB`物件是用來儲存輸入PDF檔案。
   * 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表輸入PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 以位元組陣列的內容指派物件的`MTOM`屬性，填入`BLOB`物件。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此集合物件是用來儲存輸入PDF檔案。
   * 針對每個輸入PDF檔案，建立`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。 例如，如果使用兩個輸入PDF檔案，請建立兩個`MyMapOf_xsd_string_To_xsd_anyType_Item`物件。
   * 將代表索引鍵名稱的字串值指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`key`欄位。 此值必須符合DDX檔案中指定的PDF來源元素的值。 (針對每個輸入PDF檔案執行此工作。)
   * 將儲存PDF檔案的`BLOB`物件指派給`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`欄位。 (針對每個輸入PDF檔案執行此工作。)
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 叫用`MyMapOf_xsd_string_To_xsd_anyType`物件的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`物件。 (針對每個輸入PDF檔案執行此工作。)

1. 設定初始Bates數字值。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 將數值指派給屬於`AssemblerOptionSpec`物件的`firstBatesNumber`資料成員，以設定初始Bates數字。

1. 組合輸入PDF檔案。

   叫用`AssemblerServiceClient`物件的`invoke`方法，並傳遞下列值：

   * 代表DDX檔案的`BLOB`物件。
   * 包含輸入PDF檔案的`MyMapOf_xsd_string_To_xsd_anyType`物件。 其金鑰必須與PDF來源檔案的名稱相符，其值必須是與這些檔案相對應的`BLOB`物件。
   * 指定執行階段選項的`AssemblerOptionSpec`物件。

   `invoke`方法傳回`AssemblerResult`物件，其中包含工作的結果和發生的任何例外狀況。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，這是包含結果PDF檔案的`Map`物件。
   * 反複檢查`Map`物件，直到找到符合結果檔名稱的金鑰。 然後將該陣列成員的`value`轉換為`BLOB`。
   * 存取其`BLOB`物件的`MTOM`屬性，以擷取代表PDF檔案的二進位資料。 這會傳回您可以寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
