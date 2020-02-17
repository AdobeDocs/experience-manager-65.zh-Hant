---
title: 匯入和匯出資料
seo-title: 匯入和匯出資料
description: 'null'
seo-description: 'null'
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 匯入和匯出資料 {#importing-and-exporting-data}

## 關於表單資料整合服務 {#about-the-form-data-integration-service}

表單資料整合服務可將資料匯入PDF表單，並從PDF表單匯出資料。 匯入和匯出作業支援兩種PDF表單：

* Acrobat表單（在Acrobat中建立）是包含表單欄位的PDF檔案。
* Adobe XML表單（在設計人員中建立）是符合XML Adobe XML表單架構(XFA)的PDF檔案。

表單資料可依PDF表單類型以下列其中一種格式存在：

* XFDF檔案，是Acrobat表單資料格式的XML版本。
* XDP檔案，此為包含表單欄位定義的XML檔案。 它也可能包含表單欄位資料和內嵌的PDF檔案。 只有當設計人員產生的XDP檔案包含內嵌的64位元編碼PDF檔案時，才能使用它。

您可以使用表單資料整合服務完成下列工作：

* 將資料匯入PDF表單。 如需詳細資訊，請參 [閱匯入表單資料](importing-exporting-data.md#importing-form-data)。
* 從PDF表單匯出資料。 如需詳細資訊，請參 [閱匯出表單資料](importing-exporting-data.md#exporting-form-data)。

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 匯入表單資料 {#importing-form-data}

您可以使用表單資料整合服務，將表單資料匯入互動式PDF表單。 互動式PDF表單是PDF檔案，其中包含一或多個欄位，用於收集使用者的資訊或顯示自訂資訊。 表單資料整合服務不支援表單計算、驗證或指令碼。

若要將資料匯入在Designer中建立的表單，您必須參考有效的XDP XML資料來源。 請考慮以下抵押貸款申請表示例。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

若要將資料值匯入此表單，您必須有與表單對應的有效XDP XML資料來源。 您不能使用任意XML資料來源，使用「表單資料整合」服務將資料匯入表單。 任意XML資料來源與XDP XML資料來源的區別在於，XDP資料來源符合XML表單架構(XFA)。 以下XML代表與範例抵押申請表格對應的XDP XML資料來源。

```as3
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
>如需表單資料整合服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將表單資料匯入PDF表單，請執行下列步驟：

1. 包含專案檔案。
1. 建立表單資料整合服務用戶端。
1. 參考PDF表格。
1. 參考XML資料來源。
1. 將資料匯入PDF表單。
1. 將PDF表格儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立表單資料整合服務客戶端**

您必須先建立資料整合服務用戶端，才能以程式設計方式將資料匯入PDF表單用戶端API。 建立服務客戶端時，您定義調用服務所需的連接設定。 有關資訊，請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

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

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速入門](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[匯出表單資料](importing-exporting-data.md#exporting-form-data)

### 使用Java API匯入表單資料 {#import-form-data-using-the-java-api}

使用表單資料整合API(Java)匯入表單資料：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormDataIntegrationClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考PDF表格。

   * 使用其 `java.io.FileInputStream` 建構函式建立物件。 傳遞指定PDF表單位置的字串值。
   * 使用 `com.adobe.idp.Document` 建構函式建立儲存PDF表單的物 `com.adobe.idp.Document` 件。 將包含 `java.io.FileInputStream` PDF表格的物件傳遞至建構函式。

1. 參考XML資料來源。

   * 使用 `java.io.FileInputStream` 其建構函式建立物件，並傳遞字串值，指定XML檔案（包含要匯入表單的資料）的位置。
   * 使用建 `com.adobe.idp.Document` 構函式建立儲存表單資料的物 `com.adobe.idp.Document` 件。 將包含 `java.io.FileInputStream` 表單資料的物件傳遞至建構函式。

1. 將資料匯入PDF表單。

   調用物件的方法並傳遞下 `FormDataIntegrationClient` 列值，將 `importData` 資料匯入PDF表單：

   * 儲存 `com.adobe.idp.Document` PDF表單的物件。
   * 存 `com.adobe.idp.Document` 儲表單資料的對象。
   此方 `importData` 法會傳回 `com.adobe.idp.Document` 儲存PDF表單的物件，該PDF表單包含位於XML資料來源中的資料。

1. 將PDF表格儲存為PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為&quot;。PDF&quot;。
   * 叫用 `Document` 物件的方 `copyToFile` 法，將物件的內容複製至檔案(請確定您使用 `Document` 由方法傳回的物 `Document``importData` 件)。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API匯入表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API匯入表單資料 {#import-form-data-using-the-web-service-api}

使用表單資料整合API(web service)匯入表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立表單資料整合服務用戶端。

   * 使用其 `FormDataIntegrationClient` 預設建構函式建立物件。
   * 使用建 `FormDataIntegrationClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。 不過，請指 `?blob=mtom` 定使用MTOM。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `FormDataIntegrationClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF表格。

   * 使用其 `BLOB` 建構函式建立物件。 此 `BLOB` 物件用來儲存PDF表格。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，指定PDF表單的位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 參考XML資料來源。

   * 使用其 `BLOB` 建構函式建立物件。 此 `BLOB` 物件用來儲存匯入表單的資料。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，指定包含要匯入資料的XML檔案位置，以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 將資料匯入PDF表單。

   調用物件的方法並傳遞下 `FormDataIntegrationClient` 列值，將 `importData` 資料匯入PDF表單：

   * 儲存 `BLOB` PDF表單的物件。
   * 存 `BLOB` 儲表單資料的對象。
   此方 `importData` 法會傳回 `BLOB` 儲存PDF表單的物件，該PDF表單包含位於XML資料來源中的資料。

1. 將PDF表格儲存為PDF檔案。

   * 呼叫 `System.IO.FileStream` 其建構函式並傳遞代表PDF檔案檔案位置的字串值，以建立物件。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `importData` 容。 取得物件欄位的值，以填入 `BLOB` 位元組陣 `MTOM` 列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 匯出表單資料 {#exporting-form-data}

您可以使用表單資料整合服務，從互動式PDF表單匯出表單資料。 匯出的資料格式取決於表單類型。 如果表單類型是在Acrobat中建立的Acrobat表單，則匯出的資料是XFDF。 如果表單類型是在Designer中建立的XML表單，則導出的資料是XDP。

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

若要從PDF表單匯出表單資料，請執行下列步驟：

1. 包含專案檔案
1. 建立表單資料整合服務用戶端。
1. 參考PDF表格。
1. 從PDF表單匯出資料。
1. 將匯出的資料儲存為XML檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立表單資料整合服務客戶端**

您必須先建立資料整合服務用戶端，才能以程式設計方式將資料匯入PDF formClient API。 建立服務客戶端時，您定義調用服務所需的連接設定。 有關資訊，請 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**參考PDF表格**

若要從PDF表單匯出資料，您必須參考在Designer或Acrobat中建立且包含表單資料的PDF表單。 如果您嘗試從空的PDF表單匯出資料，將會看到空的XML架構。

**從PDF表單匯出資料**

參考包含表單資料的PDF表單後，您就可以從表單匯出資料。 資料會匯出在以表單為基礎的XML架構中。

**將表單資料儲存為XML檔案**

匯出表單資料後，您可將資料儲存為XML檔案。 儲存為XML檔案後，您就可以在XML檢視器中開啟XML檔案，以檢視表單資料。

**另請參閱**

[使用Java API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-java-api)

[使用web service API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速入門](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[匯入表單資料](importing-exporting-data.md#importing-form-data)

### 使用Java API匯出表單資料 {#export-form-data-using-the-java-api}

使用表單資料整合API(Java)匯出表單資料：

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `FormDataIntegrationClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考PDF表格。

   * 使用 `java.io.FileInputStream` 其建構函式建立物件，並傳遞字串值，指定PDF表單（包含要匯出的資料）的位置。
   * 使用 `com.adobe.idp.Document` 建構函式建立儲存PDF表單的物 `com.adobe.idp.Document` 件。 將包含 `java.io.FileInputStream` PDF表格的物件傳遞至建構函式。

1. 從PDF表單匯出資料。

   調用物件的方 `FormDataIntegrationClient` 法匯出表 `exportData` 單資料，並傳 `com.adobe.idp.Document` 遞儲存PDF表單的物件。 此方法傳回 `com.adobe.idp.Document` 將表單資料儲存為XML架構的物件。

1. 將PDF表格儲存為PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為XML。
   * 叫用 `Document` 物件的方 `copyToFile` 法，將物件的內容複製至檔案(請確定您使用 `Document` 由方法傳回的物 `Document``exportData` 件)。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門（SOAP模式）:使用Java API匯出表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API匯出表單資料 {#export-form-data-using-the-web-service-api}

使用表單資料整合API(web service)匯出表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   * 以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立表單資料整合服務用戶端。

   * 使用其 `FormDataIntegrationClient` 預設建構函式建立物件。
   * 使用建 `FormDataIntegrationClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`。)您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。 不過，請指 `?blob=mtom` 定使用MTOM。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `FormDataIntegrationClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `FormDataIntegrationClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 參考PDF表格。

   * 使用其 `BLOB` 建構函式建立物件。 此 `BLOB` 物件用來儲存匯出資料的PDF表單。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，指定PDF表單的位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 從PDF表單匯出資料。

   調用物件的方法並傳遞儲 `FormDataIntegrationClient` 存PDF表單的 `exportData` 物件，將 `BLOB` 資料匯入PDF表單。 此方法傳回 `BLOB` 將表單資料儲存為XML架構的物件。

1. 將PDF表格儲存為PDF檔案。

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞表示XML檔案位置的字串值來建立對象。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `exportData` 容。 取得物件欄位的值，以填入 `BLOB` 位元組陣 `MTOM` 列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入XML檔案。

**另請參閱**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
