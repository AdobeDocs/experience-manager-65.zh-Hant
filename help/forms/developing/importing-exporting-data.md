---
title: 匯入和匯出資料
seo-title: 匯入和匯出資料
description: 使用表單資料整合服務，將資料匯入PDF表單，並使用Java API和Web Service API從PDF表單匯出資料。
seo-description: 使用表單資料整合服務，將資料匯入PDF表單，並使用Java API和Web Service API從PDF表單匯出資料。
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '2810'
ht-degree: 0%

---


# 導入和導出資料{#importing-and-exporting-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於表單資料整合服務{#about-the-form-data-integration-service}

表單資料整合服務可將資料匯入PDF表單，並從PDF表單匯出資料。 匯入和匯出作業支援兩種PDF表單：

* Acrobat表單（在Acrobat中建立）是包含表單欄位的PDF檔案。
* Adobe XML表單（在設計人員中建立）是符合XML Adobe XML表單架構(XFA)的PDF檔案。

表單資料可依PDF表單類型以下列其中一種格式存在：

* XFDF檔案，是Acrobat表單資料格式的XML版本。
* XDP檔案，此為包含表單欄位定義的XML檔案。 它也可能包含表單欄位資料和內嵌的PDF檔案。 只有當設計人員產生的XDP檔案包含內嵌的64位元編碼PDF檔案時，才能使用它。

您可以使用表單資料整合服務完成下列工作：

* 將資料匯入PDF表單。 如需詳細資訊，請參閱[匯入表單資料](importing-exporting-data.md#importing-form-data)。
* 從PDF表單匯出資料。 如需詳細資訊，請參閱[匯出表單資料](importing-exporting-data.md#exporting-form-data)。

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 導入表單資料{#importing-form-data}

您可以使用表單資料整合服務，將表單資料匯入互動式PDF表單。 互動式PDF表單是PDF檔案，其中包含一或多個欄位，用於收集使用者的資訊或顯示自訂資訊。 表單資料整合服務不支援表單計算、驗證或指令碼。

若要將資料匯入在Designer中建立的表單，您必須參考有效的XDP XML資料來源。 請考慮以下抵押貸款申請表示例。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

若要將資料值匯入此表單，您必須有與表單對應的有效XDP XML資料來源。 您不能使用任意XML資料來源，使用「表單資料整合」服務將資料匯入表單。 任意XML資料來源與XDP XML資料來源的區別在於，XDP資料來源符合XML表單架構(XFA)。 以下XML代表與範例抵押申請表格對應的XDP XML資料來源。

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
>如需表單資料整合服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

若要將表單資料匯入PDF表單，請執行下列步驟：

1. 包含專案檔案。
1. 建立表單資料整合服務用戶端。
1. 參考PDF表格。
1. 參考XML資料來源。
1. 將資料匯入PDF表單。
1. 將PDF表格儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立表單資料整合服務客戶端**

您必須先建立資料整合服務用戶端，才能以程式設計方式將資料匯入PDF表單用戶端API。 建立服務客戶端時，您定義調用服務所需的連接設定。 有關資訊，請參見[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**參考PDF表格**

若要將資料匯入PDF表單，您必須參考在Designer中建立的XML表單或在Acrobat中建立的Acrobat表單。

**參考XML資料來源**

若要匯入表單資料，您必須參考有效的資料來源。 若要將資料匯入在Designer中建立的XFA XML表單，您必須使用XDP XML資料來源。 如果您參考Acrobat表單，則必須使用XFDF資料來源。 對於要將資料導入的每個欄位，必須指定一個值。 如果XML資料來源中的元素與表單中的欄位不對應，則會忽略該元素。

**將資料匯入PDF表單**

參考PDF表單和有效的XML資料來源後，您可將資料匯入PDF表單。

**將PDF表格儲存為PDF檔案**

將資料匯入表單後，您可將表單儲存為PDF檔案。 當使用者儲存為PDF檔案後，就可以在Adobe Reader或Acrobat中開啟表格，並檢視已匯入資料的表格。

**另請參閱**

[使用Java API匯入表單資料](importing-exporting-data.md#import-form-data-using-the-java-api)

[使用web service API匯入表單資料](importing-exporting-data.md#import-form-data-using-the-web-service-api)

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
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormDataIntegrationClient`對象。

1. 參考PDF表格。

   * 使用其建構子建立`java.io.FileInputStream`對象。 傳遞指定PDF表單位置的字串值。
   * 使用`com.adobe.idp.Document`建構函式建立儲存PDF表單的`com.adobe.idp.Document`物件。 將包含PDF表單的`java.io.FileInputStream`物件傳遞至建構函式。

1. 參考XML資料來源。

   * 使用其建構子建立`java.io.FileInputStream`對象，並傳遞一個字串值，該字串值指定要導入表單的資料的XML檔案的位置。
   * 使用`com.adobe.idp.Document`建構函式建立儲存表單資料的`com.adobe.idp.Document`物件。 將包含表單資料的`java.io.FileInputStream`物件傳遞至建構函式。

1. 將資料匯入PDF表單。

   調用`FormDataIntegrationClient`物件的`importData`方法並傳遞下列值，將資料匯入PDF表單：

   * 儲存PDF表單的`com.adobe.idp.Document`對象。
   * 儲存表單資料的`com.adobe.idp.Document`對象。

   `importData`方法返回一個`com.adobe.idp.Document`對象，該對象儲存一個包含位於XML資料源中的資料的PDF表單。

1. 將PDF表格儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為&quot;。PDF&quot;。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製至檔案（請確定您使用`importData`方法傳回的`Document`物件）。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API匯入表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#import-form-data-using-the-web-service-api}匯入表單資料

使用表單資料整合API(web service)匯入表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立表單資料整合服務用戶端。

   * 使用其預設建構子建立`FormDataIntegrationClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`FormDataIntegrationClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`FormDataIntegrationClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF表格。

   * 使用其建構子建立`BLOB`對象。 此`BLOB`物件用來儲存PDF表單。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，指定PDF表單的位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 參考XML資料來源。

   * 使用其建構子建立`BLOB`對象。 此`BLOB`物件用來儲存匯入表單的資料。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，指定包含要匯入資料的XML檔案位置，以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 將資料匯入PDF表單。

   調用`FormDataIntegrationClient`物件的`importData`方法並傳遞下列值，將資料匯入PDF表單：

   * 儲存PDF表單的`BLOB`對象。
   * 儲存表單資料的`BLOB`對象。

   `importData`方法返回一個`BLOB`對象，該對象儲存一個包含位於XML資料源中的資料的PDF表單。

1. 將PDF表格儲存為PDF檔案。

   * 調用`System.IO.FileStream`對象的建構子並傳遞一個字串值，該字串值表示PDF檔案的檔案位置。
   * 建立一個位元組陣列，用於儲存`importData`方法返回的`BLOB`對象的資料內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 導出表單資料{#exporting-form-data}

您可以使用表單資料整合服務，從互動式PDF表單匯出表單資料。 匯出的資料格式取決於表單類型。 如果表單類型是在Acrobat中建立的Acrobat表單，則匯出的資料是XFDF。 如果表單類型是在Designer中建立的XML表單，則導出的資料是XDP。

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}摘要

若要從PDF表單匯出表單資料，請執行下列步驟：

1. 包含專案檔案
1. 建立表單資料整合服務用戶端。
1. 參考PDF表格。
1. 從PDF表單匯出資料。
1. 將匯出的資料儲存為XML檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立表單資料整合服務客戶端**

您必須先建立資料整合服務用戶端，才能以程式設計方式將資料匯入PDF formClient API。 建立服務客戶端時，您定義調用服務所需的連接設定。 有關資訊，請[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**參考PDF表格**

若要從PDF表單匯出資料，您必須參考在Designer或Acrobat中建立且包含表單資料的PDF表單。 如果您嘗試從空的PDF表單匯出資料，將會看到空的XML架構。

**從PDF表單匯出資料**

參考包含表單資料的PDF表單後，您就可以從表單匯出資料。 資料會匯出在以表單為基礎的XML架構中。

**將表單資料儲存為XML檔案**

匯出表單資料後，您可將資料儲存為XML檔案。 儲存為XML檔案後，您就可以在XML檢視器中開啟XML檔案，以檢視表單資料。

**另請參閱**

[使用Java API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-java-api)

[使用web service API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-web-service-api)

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
   * 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormDataIntegrationClient`對象。

1. 參考PDF表格。

   * 使用其建構函式建立`java.io.FileInputStream`物件，並傳遞字串值，指定要匯出資料的PDF表單位置。
   * 使用`com.adobe.idp.Document`建構函式建立儲存PDF表單的`com.adobe.idp.Document`物件。 將包含PDF表單的`java.io.FileInputStream`物件傳遞至建構函式。

1. 從PDF表單匯出資料。

   叫用`FormDataIntegrationClient`物件的`exportData`方法，並傳遞儲存PDF表單的`com.adobe.idp.Document`物件，以匯出表單資料。 此方法返回將表單資料儲存為XML架構的`com.adobe.idp.Document`對象。

1. 將PDF表格儲存為PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為XML。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製至檔案（請確定您使用`exportData`方法傳回的`Document`物件）。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API匯出表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#export-form-data-using-the-web-service-api}匯出表單資料

使用表單資料整合API(web service)匯出表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義：`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   * 將`localhost`取代為代管AEM Forms之伺服器的IP位址。

1. 建立表單資料整合服務用戶端。

   * 使用其預設建構子建立`FormDataIntegrationClient`對象。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`FormDataIntegrationClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。 您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請指定`?blob=mtom`以使用MTOM。
   * 獲取`FormDataIntegrationClient.Endpoint.Binding`欄位的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 將相應的口令值分配給欄位`FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`分配給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF表格。

   * 使用其建構子建立`BLOB`對象。 此`BLOB`物件用來儲存匯出資料的PDF表單。
   * 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，指定PDF表單的位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`MTOM`對象的欄位分配位元組陣列的內容來填充`BLOB`對象。

1. 從PDF表單匯出資料。

   調用`FormDataIntegrationClient`物件的`exportData`方法，並傳遞儲存PDF表單的`BLOB`物件，將資料匯入PDF表單。 此方法返回將表單資料儲存為XML架構的`BLOB`對象。

1. 將PDF表格儲存為PDF檔案。

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞表示XML檔案位置的字串值來建立對象。
   * 建立一個位元組陣列，用於儲存`exportData`方法返回的`BLOB`對象的資料內容。 取得`BLOB`物件的`MTOM`欄位值，以填入位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入XML檔案。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
