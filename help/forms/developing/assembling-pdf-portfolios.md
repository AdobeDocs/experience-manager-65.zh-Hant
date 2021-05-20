---
title: 組裝PDFPortfolio
seo-title: 組裝PDFPortfolio
description: 組合PDF作品集，以組合多種類型的檔案，包括word檔案、影像檔案和PDF檔案。 您可以使用Java API和網站服務API來組合PDF檔案。
seo-description: 組合PDF作品集，以組合多種類型的檔案，包括word檔案、影像檔案和PDF檔案。 您可以使用Java API和網站服務API來組合PDF檔案。
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 0%

---

# 裝配PDFPortfolio{#assembling-pdf-portfolios}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以使用組合器Java和Web服務API來組合PDFPortfolio。 產品組合可以組合多種類型的多個文檔，包括word檔案、影像檔案（例如jpeg檔案）和PDF文檔。 產品組合的版面可設定為不同的樣式，例如&#x200B;*Grid with Preview*、*On a Image*&#x200B;版面，或甚至&#x200B;*Revolve*。

下圖是具有&#x200B;*On a Image*&#x200B;樣式配置的產品組合螢幕截圖。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

建立PDFPortfolio，除了傳遞檔案集外，還是無紙化替代方法。 使用AEM Forms，您可以借由叫用結構化DDX檔案的組合器服務來建立產品組合。 以下DDX文檔是建立PDFPortfolio的DDX文檔的示例。

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

DXX文檔必須包含`Portfolio`標籤，該標籤帶有嵌套的`Navigator`標籤。 請注意，只有在將`myNavigator`指派為onImage配置導覽器時，才需要標籤`<Resource name="navigator/image.xxx" source="myImage.png"/>`:`AdobeOnImage.nav`。 此標籤允許組合器服務選擇要用作組合背景的影像。 包含`PackageFiles`和`File`標籤，以定義封裝檔案的檔案名和MIME類型。

>[!NOTE]
>
>有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[組合器服務和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}的摘要

若要建立PDFPortfolio，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器客戶端。
1. 參考現有的DDX文檔。
1. 參考所需文檔。
1. 設定運行時選項。
1. 組合產品組合。
1. 保存組合的產品組合。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

**建立PDF組合器客戶端**

在以寫程式方式執行組合器操作之前，請建立組合器服務客戶端。

**參考現有的DDX文檔**

必須參考DDX文檔才能組合PDFPortfolio。 此DDX文檔必須包含`Portfolio`、`Navigator`和`PackageFiles`元素。

**參考所需文檔**

要組合PDFPortfolio，請參照表示要組合的文檔的所有檔案。 例如，將DDX文檔中指定的所有影像檔案傳遞到組合器服務。 請注意，在本節中指定的DDX文檔中引用了這些檔案：*myImage.png*&#x200B;和&#x200B;*saint_bernard.jpg*。

組裝PDFPortfolio時，將NAV檔案（導航檔案）傳遞到組合器服務。 您傳遞至組合器服務的NAV檔案取決於要建立的PDFPortfolio類型。 例如，若要建立&#x200B;*在影像*&#x200B;版面上，請傳遞AdobeOnImage.nav檔案。 您可以在下列資料夾中找到NAV檔案：

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

從Acrobat 9（或更新版本）安裝目錄複製NAV檔案。 將NAV檔案放置在用戶端應用程式可存取的位置。 所有檔案都會傳遞到映射集合對象中的組合器服務。

>[!NOTE]
>
>與組裝PDFPortfolio相關聯的快速入門使用AdobeOnImage.nav。

**設定運行時選項**

您可以設定運行時選項，以控制組合器服務在執行作業時的行為。 例如，您可以設定一個選項，指示組合器服務在遇到錯誤時繼續處理作業。

**組合產品組合**

要組合PDFPortfolio，請調用`invokeDDX`操作。 組合器服務返回集合對象內的PDFPortfolio。

**保存組合的產品組合**

PDFPortfolio會在集合物件中傳回。 逐一查看集合物件，並將PDFPortfolio儲存為PDF檔案。

**另請參閱**

[使用Java API組合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-java-api)

[使用Web服務API組合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-a-pdf-portfolio-using-the-java-api}組合PDFPortfolio

使用組合器服務API(Java)組合PDFPortfolio:

1. 包含專案檔案。

   在Java項目的類路徑中包含客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF組合器客戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`AssemblerServiceClient`物件。

1. 參考現有的DDX文檔。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。

1. 參考所需文檔。

   * 使用`HashMap`建構子建立用於儲存輸入PDF文檔的`java.util.Map`對象。
   * 使用其建構子建立`java.io.FileInputStream`物件。 傳遞所需NAV檔案的位置（對建立產品組合所需的每個檔案重複此任務）。
   * 建立`com.adobe.idp.Document`物件並傳遞包含NAV檔案的`java.io.FileInputStream`物件（對建立產品組合所需的每個檔案重複此工作）。
   * 調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象中：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的源元素的值匹配。 （對建立產品組合所需的每個檔案重複執行此任務）。
      * 包含PDF文檔的`com.adobe.idp.Document`對象。 （對建立產品組合所需的每個檔案重複執行此任務）。

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法來設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請調用`AssemblerOptionSpec`對象的`setFailOnError`方法並傳遞`false`。

1. 組合產品組合。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下必需值：

   * 表示要使用的DDX文檔的`com.adobe.idp.Document`對象
   * `java.util.Map`物件，包含建立PDFPortfolio所需的檔案。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`對象，它指定運行時選項，包括預設字型和作業日誌級別

   `invokeDDX`方法返回一個`com.adobe.livecycle.assembler.client.AssemblerResult`對象，該對象包含已裝配的PDFPortfolio和發生的任何異常。

1. 保存組合的產品組合。

   若要取得PDFPortfolio，請執行下列動作：

   * 調用`AssemblerResult`對象的`getDocuments`方法。 此方法會傳回`java.util.Map`物件。
   * 對`java.util.Map`對象進行迭代，直到找到結果`com.adobe.idp.Document`對象。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法以擷取PDFPortfolio。

**另請參閱**

[快速入門（SOAP模式）:使用Java API組裝PDFPortfolio](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API {#assemble-a-pdf-portfolio-using-the-web-service-api}組合PDFPortfolio

使用組合器服務API（Web服務）組合PDFPortfolio:

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 在設定服務引用時，請確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

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
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示DDX文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`物件指派包含位元組陣列內容的屬性，以填入`BLOB`物件。

1. 參考所需文檔。

   * 對於每個輸入檔案，使用其建構子建立`BLOB`對象。 `BLOB`對象用於儲存輸入檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示輸入檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`物件。 此集合對象用於儲存建立PDFPortfolio所需的輸入檔案。
   * 對於每個輸入檔案，建立`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配表示鍵名的字串值。 此值必須與DDX文檔中指定的元素的值匹配。 （對每個輸入檔案執行此任務。）
   * 將儲存輸入檔案的`BLOB`物件指派至`MyMapOf_xsd_string_To_xsd_anyType_Item`物件的`value`欄位。 （對每個輸入的PDF文檔執行此任務。）
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`物件新增至`MyMapOf_xsd_string_To_xsd_anyType`物件。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （對每個輸入的PDF文檔執行此任務。）

1. 設定運行時選項。

   * 使用其建構子建立`AssemblerOptionSpec`物件，以儲存執行時選項。
   * 為屬於`AssemblerOptionSpec`對象的資料成員分配值，以設定運行時選項以滿足您的業務要求。 例如，要指示組合器服務在發生錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合產品組合。

   調用`AssemblerServiceClient`對象的`invokeDDX`方法並傳遞以下值：

   * 代表DDX文檔的`BLOB`對象
   * 包含所需檔案的`MyMapOf_xsd_string_To_xsd_anyType`對象
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何異常。

1. 保存組合的產品組合。

   要獲取新建立的PDFPortfolio，請執行以下步驟：

   * 訪問`AssemblerResult`對象的`documents`欄位，該欄位是包含結果PDF文檔的`Map`對象。
   * 逐一查看`Map`對象，以獲取每個結果文檔。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 通過訪問其`BLOB`對象的`MTOM`屬性來提取表示PDF文檔的二進位資料。 這會傳回可寫出為PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
