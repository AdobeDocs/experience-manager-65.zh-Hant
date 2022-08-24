---
title: 導入和導出資料
seo-title: Importing and Exporting Data
description: 使用表單資料整合服務將資料導入到PDF表單，並使用Java API和Web服務API從PDF表單導出資料。
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 0%

---

# 導入和導出資料 {#importing-and-exporting-data}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 關於表單資料整合服務 {#about-the-form-data-integration-service}

表單資料整合服務可以將資料導入到PDF表單中，並從PDF表單中導出資料。 進出口業務支援兩種PDF forms:

* Acrobat表單(在Acrobat建立)是包含表單域的PDF文檔。
* AdobeXML表單（在設計器中建立）是符合XMLAdobeXMLForms體系結構(XFA)的PDF文檔。

表單資料可以以下列格式之一存在，具體取決於PDF表單的類型：

* XFDF檔案，是Acrobat表單資料格式的XML版本。
* XDP檔案，是包含表單域定義的XML檔案。 它還可以包含表單域資料和嵌入式PDF檔案。 只有Designer生成的XDP檔案攜帶嵌入的基64編碼PDF文檔時，才能使用它。

您可以使用表單資料整合服務完成以下任務：

* 將資料導入PDF forms。 有關資訊，請參見 [導入表單資料](importing-exporting-data.md#importing-form-data)。
* 從PDF forms導出資料。 有關資訊，請參見 [導出表單資料](importing-exporting-data.md#exporting-form-data)。

>[!NOTE]
>
>有關表單資料整合服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 導入表單資料 {#importing-form-data}

您可以使用表單資料整合服務將表單資料導入互動式PDF forms。 互動式PDF表單是PDF文檔，包含一個或多個欄位，用於從用戶收集資訊或顯示自定義資訊。 表單資料整合服務不支援表單計算、驗證或指令碼編寫。

要將資料導入到在設計器中建立的表單中，必須引用有效的XDP XML資料源。 請考慮以下抵押申請表示例。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

要將資料值導入此窗體，必須具有與窗體對應的有效XDP XML資料源。 不能使用任意XML資料源使用表單資料整合服務將資料導入表單。 任意XML資料源與XDP XML資料源的區別在於XDP資料源符合XMLForms體系結構(XFA)。 以下XML表示與示例抵押申請表單對應的XDP XML資料源。

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>有關表單資料整合服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要將表單資料導入PDF表單，請執行以下步驟：

1. 包括項目檔案。
1. 建立表單資料整合服務客戶端。
1. 引用PDF窗體。
1. 引用XML資料源。
1. 將資料導入PDF窗體。
1. 將PDF窗體另存為PDF檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立表單資料整合服務客戶端**

在以寫程式方式將資料導入PDF表單Client API之前，必須建立Data Integration服務客戶端。 建立服務客戶端時，定義調用服務所需的連接設定。 有關資訊，請參見 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**引用PDF窗體**

要將資料導入到PDF表單中，必須引用在設計器中建立的XML表單或在Acrobat建立的Acrobat表單。

**引用XML資料源**

要導入表單資料，必須引用有效的資料源。 要將資料導入到在設計器中建立的XFA XML表單中，必須使用XDP XML資料源。 如果引用Acrobat表單，則必須使用XFDF資料源。 對於要將資料導入的每個欄位，必須指定一個值。 如果位於XML資料源中的元素與表單中的欄位不對應，則忽略該元素。

**將資料導入PDF窗體**

引用PDF表單和有效的XML資料源後，可以將資料導入PDF表單。

**將PDF窗體另存為PDF檔案**

將資料導入表單後，可以將表單另存為PDF檔案。 一旦保存為PDF檔案，用戶就可以在Adobe Reader或Acrobat中開啟表單，並使用導入的資料查看表單。

**另請參閱**

[使用Java API導入表單資料](importing-exporting-data.md#import-form-data-using-the-java-api)

[使用Web服務API導入表單資料](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速啟動](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[導出表單資料](importing-exporting-data.md#exporting-form-data)

### 使用Java API導入表單資料 {#import-form-data-using-the-java-api}

使用表單資料整合API(Java)導入表單資料：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormDataIntegrationClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用PDF窗體。

   * 建立 `java.io.FileInputStream` 對象。 傳遞一個字串值，該字串值指定PDF窗體的位置。
   * 建立 `com.adobe.idp.Document` 使用PDF `com.adobe.idp.Document` 建構子。 通過 `java.io.FileInputStream` 包含建構子的PDF窗體的對象。

1. 引用XML資料源。

   * 建立 `java.io.FileInputStream` 對象，並傳遞一個字串值，該字串值指定包含要導入到表單中的資料的XML檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用 `com.adobe.idp.Document` 建構子。 通過 `java.io.FileInputStream` 包含建構子的表單資料的對象。

1. 將資料導入PDF窗體。

   通過調用PDF `FormDataIntegrationClient` 對象 `importData` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 儲存PDF窗體的對象。
   * 的 `com.adobe.idp.Document` 儲存窗體資料的對象。

   的 `importData` 方法返回 `com.adobe.idp.Document` 儲存包含XML資料源中資料的PDF表單的對象。

1. 將PDF窗體另存為PDF檔案。

   * 建立 `java.io.File` 並確保檔案副檔名為「。PDF」。
   * 調用 `Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象到檔案(確保 `Document` 返回的對象 `importData` )。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API導入表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API導入表單資料 {#import-form-data-using-the-web-service-api}

使用表單資料整合API（Web服務）導入表單資料：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立表單資料整合服務客戶端。

   * 建立 `FormDataIntegrationClient` 對象。
   * 建立 `FormDataIntegrationClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `FormDataIntegrationClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用PDF窗體。

   * 建立 `BLOB` 對象。 此 `BLOB` 對象用於儲存PDF窗體。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值指定PDF表單的位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 引用XML資料源。

   * 建立 `BLOB` 對象。 此 `BLOB` 對象用於儲存導入到窗體中的資料。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值指定包含要導入資料的XML檔案的位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 將資料導入PDF窗體。

   通過調用PDF `FormDataIntegrationClient` 對象 `importData` 方法並傳遞以下值：

   * 的 `BLOB` 儲存PDF窗體的對象。
   * 的 `BLOB` 儲存窗體資料的對象。

   的 `importData` 方法返回 `BLOB` 儲存包含XML資料源中資料的PDF表單的對象。

1. 將PDF窗體另存為PDF檔案。

   * 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示PDF檔案的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `importData` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 的子菜單。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 導出表單資料 {#exporting-form-data}

您可以使用表單資料整合服務從互動式PDF表單導出表單資料。 導出的資料的格式取決於窗體類型。 如果表單類型是在Acrobat建立的Acrobat表單，則導出的資料為XFDF。 如果表單類型是在Designer中建立的XML表單，則導出的資料為XDP。

>[!NOTE]
>
>有關表單資料整合服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要從PDF表單導出表單資料，請執行以下步驟：

1. 包括項目檔案
1. 建立表單資料整合服務客戶端。
1. 引用PDF窗體。
1. 從PDF窗體導出資料。
1. 將導出的資料另存為XML檔案。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

**建立表單資料整合服務客戶端**

在以寫程式方式將資料導入PDFformClient API之前，必須建立Data Integration服務客戶端。 建立服務客戶端時，定義調用服務所需的連接設定。 有關資訊， [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**引用PDF窗體**

要從PDF表單導出資料，必須引用在設計器或Acrobat中建立的包含表單資料的PDF表單。 如果嘗試從空的PDF表單中導出資料，將獲得空的XML架構。

**從PDF窗體導出資料**

引用包含表單資料的PDF表單後，可以從表單中導出資料。 資料在基於表單的XML架構中導出。

**將表單資料另存為XML檔案**

導出表單資料後，可以將資料另存為XML檔案。 保存為XML檔案後，可以在XML查看器中開啟XML檔案以查看表單資料。

**另請參閱**

[使用Java API導出表單資料](importing-exporting-data.md#export-form-data-using-the-java-api)

[使用Web服務API導出表單資料](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速啟動](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[導入表單資料](importing-exporting-data.md#importing-form-data)

### 使用Java API導出表單資料 {#export-form-data-using-the-java-api}

使用Form Data Integration API(Java)導出表單資料：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `FormDataIntegrationClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用PDF窗體。

   * 建立 `java.io.FileInputStream` 對象，並傳遞一個字串值，該字串值指定包含要導出資料的PDF表單的位置。
   * 建立 `com.adobe.idp.Document` 使用PDF `com.adobe.idp.Document` 建構子。 通過 `java.io.FileInputStream` 包含建構子的PDF窗體的對象。

1. 從PDF窗體導出資料。

   通過調用 `FormDataIntegrationClient` 對象 `exportData` 方法和通過 `com.adobe.idp.Document` 儲存PDF窗體的對象。 此方法返回 `com.adobe.idp.Document` 將表單資料儲存為XML架構的對象。

1. 將PDF窗體另存為PDF檔案。

   * 建立 `java.io.File` 並確保檔案副檔名為XML。
   * 調用 `Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象到檔案(確保 `Document` 返回的對象 `exportData` )。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速啟動（SOAP模式）:使用Java API導出表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API導出表單資料 {#export-form-data-using-the-web-service-api}

使用表單資料整合API（Web服務）導出表單資料：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   * 替換 `localhost` IP地址為AEM Forms。

1. 建立表單資料整合服務客戶端。

   * 建立 `FormDataIntegrationClient` 對象。
   * 建立 `FormDataIntegrationClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`。) 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請指定 `?blob=mtom` 使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `FormDataIntegrationClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用PDF窗體。

   * 建立 `BLOB` 對象。 此 `BLOB` 對象用於儲存從中導出資料的PDF窗體。
   * 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值指定PDF表單的位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 從PDF窗體導出資料。

   通過調用PDF `FormDataIntegrationClient` 對象 `exportData` 方法和通過 `BLOB` 儲存PDF窗體的對象。 此方法返回 `BLOB` 將表單資料儲存為XML架構的對象。

1. 將PDF窗體另存為PDF檔案。

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞表示XML檔案位置的字串值來對對象。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `exportData` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 的子菜單。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
