---
title: 組裝PDFPortfolio
seo-title: Assembling PDF Portfolios
description: 組合PDF產品組合以組合多種類型的文檔，包括word檔案、影像檔案和PDF文檔。 您可以使用Java API和Web服務API來組合PDF組合。
seo-description: Assemble a PDF portfolio to combine several documents of various types, including word file, image files, and PDF documents. You can assemble a PDF portfolio using a Java API and a Web Service API.
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
source-wordcount: '1828'
ht-degree: 0%

---

# 組裝PDFPortfolio {#assembling-pdf-portfolios}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

可以使用匯編器Java和Web服務API來匯編PDFPortfolio。 組合可以組合多種類型的多個文檔，包括word檔案、影像檔案（例如jpeg檔案）和PDF文檔。 可以將產品組合的佈局設定為不同的樣式，如 *帶預覽的網格*，也請參見Wiki頁。 *在影像上* 佈局 *旋轉*。

下圖是一個包含 *在影像上* 樣式佈局。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

建立PDFPortfolio是無紙化的替代辦法，不能通過檔案集。 使用AEM Forms，您可以通過使用結構化DDX文檔調用匯編器服務來建立包。 以下DDX文檔是建立PDFPortfolio的DDX文檔的示例。

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

DXX文檔必須包含 `Portfolio` 帶有嵌套的標籤 `Navigator` 標籤。 注意標籤 `<Resource name="navigator/image.xxx" source="myImage.png"/>` 只有在 `myNavigator` 已指定為onImage佈局導航器： `AdobeOnImage.nav`。 此標籤允許匯編器服務選擇用作組合背景的影像。 包括 `PackageFiles` 和 `File` 標籤，以定義打包檔案的檔案名和MIME類型。

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要建立PDFPortfolio，請執行以下任務：

1. 包括項目檔案。
1. 建立PDF匯編器客戶端。
1. 引用現有DDX文檔。
1. 引用所需文檔。
1. 設定運行時選項。
1. 組合投資組合。
1. 保存已裝配的產品組合。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

**建立PDF匯編器客戶端**

在以寫程式方式執行匯編器操作之前，請建立匯編器服務客戶端。

**引用現有DDX文檔**

必須引用DDX文檔來裝配PDFPortfolio。 此DDX文檔必須包含 `Portfolio`。 `Navigator` 和 `PackageFiles` 元素。

**引用所需文檔**

要裝配PDFPortfolio，請參照表示要裝配的文檔的所有檔案。 例如，將DDX文檔中指定的所有影像檔案傳遞給匯編程式服務。 請注意，在本節中指定的DDX文檔中引用了這些檔案： *myImage.png* 和 *聖伯納德.jpg*。

PDFPortfolio組裝時，將NAV檔案（導航器檔案）傳遞給匯編器服務。 傳遞給匯編器服務的NAV檔案取決於要建立的PDFPortfolio的類型。 例如，要建立 *在影像上* 版式，傳遞AdobeOnImage.nav檔案。 可以在以下資料夾中找到NAV檔案：

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

從Acrobat 9（或更高版本）安裝目錄複製NAV檔案。 將NAV檔案放置在客戶端應用程式可以訪問它的位置。 所有檔案都會傳遞到映射集合對象內的匯編器服務。

>[!NOTE]
>
>與「裝配PDF」Portfolio關聯的快速啟動使用AdobeOnImage.nav。

**設定運行時選項**

您可以設定運行時選項，這些選項在匯編程式服務執行作業時控制其行為。 例如，您可以設定一個選項，指示匯編程式服務在遇到錯誤時繼續處理作業。

**組合產品組合**

要裝配PDFPortfolio，請將 `invokeDDX` 的下界。 匯編器服務返回集合對象內的PDFPortfolio。

**保存已裝配的產品組合**

PDFPortfolio在集合對象內返回。 循環訪問集合對象並將PDFPortfolio另存為PDF檔案。

**另請參閱**

[使用Java API裝配PDFPortfolio](#assemble-a-pdf-portfolio-using-the-java-api)

[使用Web服務API裝配PDFPortfolio](#assemble-a-pdf-portfolio-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API裝配PDFPortfolio {#assemble-a-pdf-portfolio-using-the-java-api}

使用匯編器服務API(Java)匯編PDFPortfolio:

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立PDF匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用現有DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定DDX檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 引用所需文檔。

   * 建立 `java.util.Map` 用於儲存輸入PDF文檔的對象 `HashMap` 建構子。
   * 建立 `java.io.FileInputStream` 對象。 傳遞所需NAV檔案的位置（對建立項目組合所需的每個檔案重複此任務）。
   * 建立 `com.adobe.idp.Document` 並傳遞 `java.io.FileInputStream` 包含NAV檔案的對象（對建立項目組合所需的每個檔案重複此任務）。
   * 向 `java.util.Map` 通過調用對象 `put` 方法並傳遞以下參數：

      * 表示鍵名稱的字串值。 此值必須與DDX文檔中指定的源元素的值匹配。 （對建立產品組合所需的每個檔案重複此任務）。
      * A `com.adobe.idp.Document` 包含PDF文檔的對象。 （對建立產品組合所需的每個檔案重複此任務）。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過調用屬於的方法來設定運行時選項以滿足業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 對象 `setFailOnError` 方法 `false`。

1. 組合投資組合。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下所需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文檔的對象
   * A `java.util.Map` 包含生成PDFPortfolio所需檔案的對象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項的對象，包括預設字型和作業日誌級別

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已裝配的PDFPortfolio和發生的任何異常的對象。

1. 保存已裝配的產品組合。

   要獲取PDFPortfolio，請執行以下操作：

   * 調用 `AssemblerResult` 對象 `getDocuments` 的雙曲餘切值。 此方法返回 `java.util.Map` 的雙曲餘切值。
   * 迭代 `java.util.Map` 直到找到結果 `com.adobe.idp.Document` 的雙曲餘切值。
   * 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法提取PDFPortfolio。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API裝配PDFPortfolio](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API裝配PDFPortfolio {#assemble-a-pdf-portfolio-using-the-web-service-api}

使用匯編器服務API（Web服務）匯編PDFPortfolio:

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
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示DDX文檔的檔案位置和開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 屬性。

1. 引用所需文檔。

   * 對於每個輸入檔案，建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存輸入檔案。
   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示輸入檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 此集合對象用於儲存建立PDFPortfolio所需的輸入檔案。
   * 對於每個輸入檔案，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的雙曲餘切值。
   * 為指定表示鍵名的字串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `key` 的子菜單。 此值必須與DDX文檔中指定的元素的值匹配。 （對每個輸入檔案執行此任務。）
   * 分配 `BLOB` 將輸入檔案儲存到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `value` 的子菜單。 (為每個輸入PDF文檔執行此任務。)
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 對象 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 調用 `MyMapOf_xsd_string_To_xsd_anyType` 對象 `Add` 方法和通過 `MyMapOf_xsd_string_To_xsd_anyType` 的雙曲餘切值。 (為每個輸入PDF文檔執行此任務。)

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過將值分配給屬於的資料成員來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編程式服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 對象 `failOnError` 資料成員。

1. 組合投資組合。

   調用 `AssemblerServiceClient` 對象 `invokeDDX` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含所需檔案的對象
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作業結果和所發生的任何異常的對象。

1. 保存已裝配的產品組合。

   要獲取新建立的PDFPortfolio，請執行以下操作：

   * 訪問 `AssemblerResult` 對象 `documents` 欄位， `Map` 包含結果PDF文檔的對象。
   * 迭代 `Map` 對象，以獲取每個結果文檔。 然後，將該陣列成員 `value` 到 `BLOB`。
   * 通過訪問PDF文檔來提取表示該文檔的二進位資料 `BLOB` 對象 `MTOM` 屬性。 這將返回可以寫入PDF檔案的位元組陣列。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
