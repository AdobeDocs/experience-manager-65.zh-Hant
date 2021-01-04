---
title: 組合PDF資料夾
seo-title: 組合PDF資料夾
description: 組合PDF資料夾，以組合多種類型的檔案，包括Word檔案、影像檔和PDF檔案。 您可以使用Java API和Web Service API來組合PDF資料夾。
seo-description: 組合PDF資料夾，以組合多種類型的檔案，包括Word檔案、影像檔和PDF檔案。 您可以使用Java API和Web Service API來組合PDF資料夾。
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 0%

---


# 組合PDF資料夾{#assembling-pdf-portfolios}

您可以使用Assembler Java和web service API來組合PDF資料夾。 作品集可以結合多種類型的檔案，包括Word檔、影像檔（例如jpeg檔）和PDF檔案。 作品集的版面可設定為不同的樣式，例如「預覽格線」(Grid with Preview)、「影像上的&#x200B;*」(On a Image*)版面，或甚至「旋轉」(Revolve)。****

下圖為具有&#x200B;*On an Image*&#x200B;樣式版面的作品集螢幕擷取。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

建立PDF資料夾是傳遞檔案集的無紙化替代選擇。 使用AEM Forms，您可以使用結構化DDX檔案來叫用Assembler服務來建立作品集。 以下DDX檔案是建立PDF資料夾的DDX檔案範例。

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

DXX檔案必須包含`Portfolio`標籤，並附上巢狀`Navigator`標籤。 請注意，只有當`myNavigator`被指派為onImage版面導覽器時，才需要`<Resource name="navigator/image.xxx" source="myImage.png"/>`標籤：`AdobeOnImage.nav`。 此標籤允許Assembler服務選擇要用作資料夾背景的影像。 包含`PackageFiles`和`File`標籤，以定義封裝檔案的檔案名稱和MIME類型。

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參閱[匯編器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟{#summary-of-steps}摘要

若要建立PDF資料夾，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考所需檔案。
1. 設定執行時期選項。
1. 組合作品集。
1. 儲存組合的作品集。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立PDF匯寫程式式用戶端**

在以寫程式方式執行匯編器操作之前，請建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合PDF資料夾。 此DDX文檔必須包含`Portfolio`、`Navigator`和`PackageFiles`元素。

**參考所需檔案**

若要組合PDF資料夾，請參考所有代表要組合的檔案的檔案。 例如，將DDX文檔中指定的所有影像檔案傳遞到Assembler服務。 請注意，在本節中指定的DDX檔案中會參照這些檔案：*myImage.png*&#x200B;和&#x200B;*saint_bernard.jpg*。

當組合PDF資料夾時，請將NAV檔案（導覽檔案）傳遞至Assembler服務。 您傳遞至Assembler服務的NAV檔案取決於要建立的PDF資料夾類型。 例如，若要建立&#x200B;*On an Image*&#x200B;版面，請傳遞AdobeOnImage.nav檔案。 您可以在下列資料夾中找到NAV檔案：

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

從Acrobat 9（或更新版本）安裝目錄複製NAV檔案。 將NAV檔案置於您的用戶端應用程式可存取的位置。 所有檔案都會傳遞到Map集合對象中的Assembler服務。

>[!NOTE]
>
>與「組合PDF資料夾」相關的快速入門使用AdobeOnImage.nav。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。

**組合作品集**

若要組合PDF資料夾，請呼叫`invokeDDX`操作。 Assembler服務會在集合物件中傳回PDF資料夾。

**儲存組合的作品集**

PDF資料夾會在系列物件中傳回。 重複收集物件並將PDF資料夾儲存為PDF檔案。

**另請參閱**

[使用Java API組合PDF資料夾](#assemble-a-pdf-portfolio-using-the-java-api)

[使用web service API組合PDF資料夾](#assemble-a-pdf-portfolio-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-a-pdf-portfolio-using-the-java-api}組合PDF資料夾

使用Assembler Service API(Java)來組合PDF資料夾：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF匯寫程式式用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`AssemblerServiceClient`對象。

1. 參考現有的DDX檔案。

   * 使用DDX文檔的建構子並傳遞指定DDX檔案位置的字串值，建立代表DDX文檔的`java.io.FileInputStream`對象。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 參考所需檔案。

   * 使用`HashMap`建構函式建立`java.util.Map`物件，用來儲存輸入的PDF檔案。
   * 使用其建構子建立`java.io.FileInputStream`對象。 傳遞所需NAV檔案的位置（針對建立作品集所需的每個檔案重複此工作）。
   * 建立`com.adobe.idp.Document`物件並傳遞包含NAV檔案的`java.io.FileInputStream`物件（對建立作品集所需的每個檔案重複此工作）。
   * 通過調用`put`方法並傳遞以下參數，將條目添加到`java.util.Map`對象：

      * 代表索引鍵名稱的字串值。 此值必須與DDX文檔中指定的源元素的值匹配。 （針對建立作品集所需的每個檔案重複此工作）。
      * 包含PDF文檔的`com.adobe.idp.Document`對象。 （針對建立作品集所需的每個檔案重複此工作）。

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過調用屬於`AssemblerOptionSpec`對象的方法，設定運行時選項以滿足您的業務要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法並傳遞`false`。

1. 組合作品集。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列必要值：

   * `com.adobe.idp.Document`物件，代表要使用的DDX檔案
   * `java.util.Map`物件，包含建立PDF資料夾所需的檔案。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件，指定執行時期選項，包括預設字型和工作記錄層級

   `invokeDDX`方法會傳回`com.adobe.livecycle.assembler.client.AssemblerResult`物件，其中包含已組合的PDF資料夾和發生的任何例外。

1. 儲存組合的作品集。

   若要取得PDF資料夾，請執行下列動作：

   * 叫用`AssemblerResult`物件的`getDocuments`方法。 此方法返回`java.util.Map`對象。
   * 重複`java.util.Map`物件，直到找到結果`com.adobe.idp.Document`物件。
   * 叫用`com.adobe.idp.Document`物件的`copyToFile`方法來擷取PDF資料夾。

**另請參閱**

[快速入門（SOAP模式）:使用Java API組合PDF資料夾](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用web service API {#assemble-a-pdf-portfolio-using-the-web-service-api}組合PDF資料夾

使用Assembler Service API(web service)來組合PDF資料夾：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立PDF匯寫程式式用戶端。

   * 使用其預設建構子建立`AssemblerServiceClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。
   * 獲取`AssemblerServiceClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存DDX檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立&lt;a0/>對象，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的&lt;a1/>屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 參考所需檔案。

   * 對於每個輸入檔案，使用其建構子建立`BLOB`對象。 `BLOB`對象用於儲存輸入檔案。
   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立&lt;a0/>對象，該字串值表示輸入檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。
   * 建立`MyMapOf_xsd_string_To_xsd_anyType`對象。 此收集物件用於儲存建立PDF資料夾所需的輸入檔案。
   * 對於每個輸入檔案，建立一個`MyMapOf_xsd_string_To_xsd_anyType_Item`對象。
   * 為`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`key`欄位分配代表鍵名的字串值。 此值必須與DDX文檔中指定的元素值匹配。 （對每個輸入檔案執行此任務。）
   * 將儲存輸入檔案的`BLOB`對象分配給`MyMapOf_xsd_string_To_xsd_anyType_Item`對象的`value`欄位。 （請對每個輸入的PDF檔案執行此工作。）
   * 將`MyMapOf_xsd_string_To_xsd_anyType_Item`對象添加到`MyMapOf_xsd_string_To_xsd_anyType`對象。 調用`MyMapOf_xsd_string_To_xsd_anyType`對象的`Add`方法並傳遞`MyMapOf_xsd_string_To_xsd_anyType`對象。 （請對每個輸入的PDF檔案執行此工作。）

1. 設定執行時期選項。

   * 使用其建構子建立一個`AssemblerOptionSpec`對象，該對象儲存運行時選項。
   * 通過為屬於`AssemblerOptionSpec`對象的資料成員分配值，設定運行時選項以滿足您的業務要求。 例如，要指示Assembler服務在出現錯誤時繼續處理作業，請將`false`分配給`AssemblerOptionSpec`對象的`failOnError`資料成員。

1. 組合作品集。

   叫用`AssemblerServiceClient`物件的`invokeDDX`方法並傳遞下列值：

   * 代表DDX文檔的`BLOB`對象
   * 包含所需檔案的`MyMapOf_xsd_string_To_xsd_anyType`對象
   * 指定運行時選項的`AssemblerOptionSpec`對象

   `invokeDDX`方法返回一個`AssemblerResult`對象，該對象包含作業的結果和發生的任何例外。

1. 儲存組合的作品集。

   若要取得新建立的PDF資料夾，請執行下列動作：

   * 存取`AssemblerResult`物件的`documents`欄位，此欄位是`Map`物件，包含產生的PDF檔案。
   * 重複`Map`物件，以取得每個結果檔案。 然後，將該陣列成員的`value`轉換為`BLOB`。
   * 存取PDF檔案的`BLOB`物件的`MTOM`屬性，擷取代表PDF檔案的二進位資料。 這會傳回可寫出至PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
