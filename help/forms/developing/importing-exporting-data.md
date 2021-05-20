---
title: 匯入和匯出資料
seo-title: 匯入和匯出資料
description: 使用表單資料整合服務將資料匯入PDF表單，並使用Java API和網站服務API從PDF表單匯出資料。
seo-description: 使用表單資料整合服務將資料匯入PDF表單，並使用Java API和網站服務API從PDF表單匯出資料。
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2810'
ht-degree: 0%

---

# 匯入和匯出資料{#importing-and-exporting-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於表單資料整合服務{#about-the-form-data-integration-service}

表單資料整合服務可將資料匯入PDF表單，並從PDF表單匯出資料。 匯入和匯出作業支援兩種PDF forms:

* Acrobat表單(在Acrobat中建立)是包含表單欄位的PDF檔案。
* AdobeXML表單（在設計工具中建立）是符合XMLAdobeXML Forms架構(XFA)的PDF文檔。

根據PDF表單的類型，表單資料可以以下列格式之一存在：

* XFDF檔案，此檔案是Acrobat表單資料格式的XML版本。
* XDP檔案，此檔案是包含表單欄位定義的XML檔案。 也可包含表單欄位資料和內嵌的PDF檔案。 Designer產生的XDP檔案必須攜帶內嵌的基本64編碼PDF檔案，才能使用。

您可以使用表單資料整合服務來完成下列工作：

* 將資料匯入PDF forms。 如需詳細資訊，請參閱[匯入表單資料](importing-exporting-data.md#importing-form-data)。
* 從PDF forms匯出資料。 如需詳細資訊，請參閱[匯出表單資料](importing-exporting-data.md#exporting-form-data)。

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 導入表單資料{#importing-form-data}

您可以使用表單資料整合服務，將表單資料匯入互動式PDF forms。 互動式PDF表單是PDF檔案，其中包含一或多個欄位，用於從使用者收集資訊或顯示自訂資訊。 表單資料整合服務不支援表單計算、驗證或指令碼。

若要將資料匯入在Designer中建立的表單，您必須參考有效的XDP XML資料來源。 請考量下列抵押申請表範例。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

若要將資料值匯入此表單，您必須具備與表單對應的有效XDP XML資料來源。 不能使用任意XML資料源來使用表單資料整合服務將資料導入表單中。 任意XML資料源與XDP XML資料源的區別在於，XDP資料源符合XML Forms體系結構(XFA)。 以下XML表示與抵押申請表示例對應的XDP XML資料源。

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
>如需表單資料整合服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}的摘要

要將表單資料導入PDF表單，請執行以下步驟：

1. 包含專案檔案。
1. 建立表單資料整合服務用戶端。
1. 參考PDF表單。
1. 參考XML資料源。
1. 將資料匯入PDF表單。
1. 將PDF表單儲存為PDF檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

有關這些JAR檔案的位置的資訊，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立表單資料整合服務用戶端**

您必須先建立資料整合服務用戶端，才能以程式設計方式將資料匯入PDF表單用戶端API。 建立服務客戶端時，您定義調用服務所需的連接設定。 有關資訊，請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**參考PDF表單**

若要將資料匯入PDF表單，您必須參考在Designer中建立的XML表單或在Acrobat中建立的Acrobat表單。

**參考XML資料源**

若要匯入表單資料，您必須參考有效的資料來源。 若要將資料匯入在Designer中建立的XFA XML表單，您必須使用XDP XML資料來源。 如果您參考Acrobat表單，則必須使用XFDF資料來源。 對於要將資料匯入的每個欄位，必須指定值。 如果位於XML資料源中的元素與窗體中的欄位不對應，則忽略該元素。

**將資料匯入PDF表單**

參考PDF表單和有效的XML資料源後，可以將資料導入PDF表單。

**將PDF表單儲存為PDF檔案**

將資料匯入表單後，您可以將表單儲存為PDF檔案。 儲存為PDF檔案後，使用者就可以在Adobe Reader或Acrobat中開啟表單，並查看含有匯入資料的表單。

**另請參閱**

[使用Java API匯入表單資料](importing-exporting-data.md#import-form-data-using-the-java-api)

[使用網站服務API匯入表單資料](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速入門](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[匯出表單資料](importing-exporting-data.md#exporting-form-data)

### 使用Java API {#import-form-data-using-the-java-api}匯入表單資料

使用表單資料整合API(Java)匯入表單資料：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormDataIntegrationClient`物件。

1. 參考PDF表單。

   * 使用其建構子建立`java.io.FileInputStream`物件。 傳遞指定PDF表單位置的字串值。
   * 使用`com.adobe.idp.Document`建構子建立`com.adobe.idp.Document`物件以儲存PDF表單。 將包含PDF表單的`java.io.FileInputStream`物件傳遞至建構函式。

1. 參考XML資料源。

   * 使用其建構子建立`java.io.FileInputStream`對象，並傳遞一個字串值，該字串值指定包含要導入到窗體中資料的XML檔案的位置。
   * 使用`com.adobe.idp.Document`建構子建立`com.adobe.idp.Document`物件，以儲存表單資料。 將包含表單資料的`java.io.FileInputStream`物件傳遞至建構函式。

1. 將資料匯入PDF表單。

   叫用`FormDataIntegrationClient`物件的`importData`方法並傳遞下列值，將資料匯入PDF表單：

   * 儲存PDF表單的`com.adobe.idp.Document`物件。
   * 儲存表單資料的`com.adobe.idp.Document`物件。

   `importData`方法返回一個`com.adobe.idp.Document`對象，該對象儲存包含位於XML資料源中的資料的PDF表單。

1. 將PDF表單儲存為PDF檔案。

   * 建立`java.io.File`物件，並確認副檔名為「.PDF」。
   * 調用`Document`對象的`copyToFile`方法，將`Document`對象的內容複製到檔案（確保使用`importData`方法返回的`Document`對象）。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API匯入表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API {#import-form-data-using-the-web-service-api}匯入表單資料

使用表單資料整合API（網站服務）匯入表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立表單資料整合服務用戶端。

   * 使用其預設建構子建立`FormDataIntegrationClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`FormDataIntegrationClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`FormDataIntegrationClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF表單。

   * 使用其建構子建立`BLOB`物件。 此`BLOB`物件用於儲存PDF表單。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，指定PDF表單的位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 參考XML資料源。

   * 使用其建構子建立`BLOB`物件。 此`BLOB`物件用於儲存匯入表單的資料。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，該字串值指定包含要導入資料的XML檔案的位置，以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 叫用`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置和資料流長度以讀取。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 將資料匯入PDF表單。

   叫用`FormDataIntegrationClient`物件的`importData`方法並傳遞下列值，將資料匯入PDF表單：

   * 儲存PDF表單的`BLOB`物件。
   * 儲存表單資料的`BLOB`物件。

   `importData`方法返回一個`BLOB`對象，該對象儲存包含位於XML資料源中的資料的PDF表單。

1. 將PDF表單儲存為PDF檔案。

   * 叫用`System.IO.FileStream`物件的建構函式並傳遞代表PDF檔案檔案位置的字串值，以建立物件。
   * 建立位元組陣列，用於儲存`importData`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`欄位的值，填入位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 導出表單資料{#exporting-form-data}

您可以使用表單資料整合服務，從互動式PDF表單匯出表單資料。 匯出的資料格式取決於表單類型。 如果表單類型是在Acrobat中建立的Acrobat表單，則匯出的資料為XFDF。 如果表單類型是在Designer中建立的XML表單，則導出的資料為XDP。

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱[AEM Forms適用的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}的摘要

要從PDF表單導出表單資料，請執行以下步驟：

1. 包含項目檔案
1. 建立表單資料整合服務用戶端。
1. 參考PDF表單。
1. 從PDF表單匯出資料。
1. 將匯出的資料儲存為XML檔案。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss上則為必要)

**建立表單資料整合服務用戶端**

您必須先建立資料整合服務用戶端，才能以程式設計方式將資料匯入PDF formClient API。 建立服務客戶端時，您定義調用服務所需的連接設定。 有關資訊，請[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**參考PDF表單**

若要從PDF表單匯出資料，您必須參考在Designer或Acrobat中建立且包含表單資料的PDF表單。 如果嘗試從空的PDF表單導出資料，將得到空的XML架構。

**從PDF表單匯出資料**

參考包含表單資料的PDF表單後，即可從表單中匯出資料。 資料會以表單為基礎的XML架構中匯出。

**將表單資料另存為XML檔案**

導出表單資料後，可以將資料另存為XML檔案。 保存為XML檔案後，您可以在XML查看器中開啟XML檔案以查看表單資料。

**另請參閱**

[使用Java API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-java-api)

[使用網站服務API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速入門](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[匯入表單資料](importing-exporting-data.md#importing-form-data)

### 使用Java API {#export-form-data-using-the-java-api}匯出表單資料

使用表單資料整合API(Java)匯出表單資料：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務用戶端。

   * 建立包含連接屬性的`ServiceClientFactory`對象。
   * 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`FormDataIntegrationClient`物件。

1. 參考PDF表單。

   * 使用其建構子建立`java.io.FileInputStream`物件，並傳遞字串值，指定要匯出的PDF表單的位置。
   * 使用`com.adobe.idp.Document`建構子建立`com.adobe.idp.Document`物件以儲存PDF表單。 將包含PDF表單的`java.io.FileInputStream`物件傳遞至建構函式。

1. 從PDF表單匯出資料。

   叫用`FormDataIntegrationClient`物件的`exportData`方法，並傳遞儲存PDF表單的`com.adobe.idp.Document`物件，以匯出表單資料。 此方法會傳回`com.adobe.idp.Document`物件，將表單資料儲存為XML架構。

1. 將PDF表單儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為XML。
   * 調用`Document`對象的`copyToFile`方法，將`Document`對象的內容複製到檔案（確保使用`exportData`方法返回的`Document`對象）。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API匯出表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API {#export-form-data-using-the-web-service-api}匯出表單資料

使用表單資料整合API（網站服務）匯出表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET項目。 確保使用以下WSDL定義：`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   * 將`localhost`取代為托管AEM Forms之伺服器的IP位址。

1. 建立表單資料整合服務用戶端。

   * 使用其預設建構子建立`FormDataIntegrationClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構子建立`FormDataIntegrationClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞到AEM Forms服務（例如`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請指定`?blob=mtom`以使用MTOM。
   * 獲取`FormDataIntegrationClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 通過執行以下任務來啟用基本HTTP身份驗證：

      * 將AEM表單使用者名稱指派給欄位`FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位`FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF表單。

   * 使用其建構子建立`BLOB`物件。 此`BLOB`對象用於儲存從中導出資料的PDF表單。
   * 調用`System.IO.FileStream`對象的建構子以建立對象。 傳遞一個字串值，指定PDF表單的位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 通過獲取`System.IO.FileStream`對象的`Length`屬性，可以確定位元組陣列的大小。
   * 調用`System.IO.FileStream`對象的`Read`方法並傳遞要讀取的位元組陣列、啟動位置和流長度，以流資料填充位元組陣列。
   * 為`MTOM`欄位指定位元組陣列的內容，以填入`BLOB`物件。

1. 從PDF表單匯出資料。

   叫用`FormDataIntegrationClient`物件的`exportData`方法，並傳遞儲存PDF表單的`BLOB`物件，將資料匯入PDF表單。 此方法會傳回`BLOB`物件，將表單資料儲存為XML架構。

1. 將PDF表單儲存為PDF檔案。

   * 調用`System.IO.FileStream`對象的建構子並傳遞表示XML檔案位置的字串值，以建立對象。
   * 建立位元組陣列，用於儲存`exportData`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象的`MTOM`欄位的值，填入位元組陣列。
   * 通過調用其建構子並傳遞`System.IO.FileStream`對象來建立`System.IO.BinaryWriter`對象。
   * 調用`System.IO.BinaryWriter`對象的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
