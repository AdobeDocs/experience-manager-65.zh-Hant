---
title: 使用條形碼表單
seo-title: 使用條形碼表單
description: 使用Java API和Web Service API，從PDF表單或包含條碼的影像解碼資料。
seo-description: 使用Java API和Web Service API，從PDF表單或包含條碼的影像解碼資料。
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 0%

---


# 使用條形碼表單{#working-with-barcoded-forms}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

## 關於條形碼表單服務{#about-the-barcoded-forms-service}

條形碼表單服務可自動從填寫及列印表單擷取資料，並將擷取的資訊整合至組織的核心IT系統。

使用條碼表單服務，您可以將一維和二維條碼新增至互動式PDF forms。 然後，您可以將條形碼表格發佈至網站，或以電子郵件或光碟散發。 當使用者使用Adobe Reader、Acrobat專業版或Acrobat Standard填寫條碼表格時，會自動更新條碼，以編碼使用者提供的表格資料。 使用者可以電子方式提交表格，或列印成紙本，再以郵件、傳真或手形方式提交。 您稍後可以擷取使用者提供的資料作為自動化工作流程的一部分，在核准程式和商業系統之間傳送資料。

有關條形碼表單服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 解碼條形碼表單資料{#decoding-barcoded-form-data}

您可以使用條碼表單服務API來解碼PDF表單或包含條碼的影像中的資料。 解碼表單資料意味著提取位於條形碼中的資料。 在從PDF表單（或影像）解碼資料之前，使用者必須先在表單中填入資料。

>[!NOTE]
>
>有關條形碼表單服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

若要解碼PDF表單中的資料，請執行下列步驟：

1. 包含專案檔案。
1. 建立條碼表單用戶端API物件。
1. 取得包含條形碼資料的PDF表格。
1. 解碼PDF表單中的資料。
1. 將資料轉換為XML資料來源。
1. 處理解碼的資料。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，則為必要項)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)
* xercesImpl.jar(位於&lt;install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

如果AEM Forms部署在非JBOSS的受支援J2EE應用程式伺服器上，則您將需要以部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案來取代adobe-utilities.jar和jbossall-client.jar。 有關所有AEM FormsJAR檔案的位置資訊，請參見[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立條碼表單用戶端API物件**

在以寫程式方式執行條形編碼表單服務操作之前，必須建立一個條形編碼Forms服務客戶端。 如果您使用Java API，請建立`BarcodedFormsServiceClient`物件。 如果您使用條形編碼表單Web服務API，請建立`BarcodedFormsServiceService`物件。

**取得包含條形碼資料的PDF表格**

您必須取得包含已填入使用者資料之條碼的PDF表單。

**從PDF表單解碼資料**

取得包含條碼的PDF表單（或影像）後，您就可以解碼資料。 BarcodedForms服務支援下列條碼類型：

* PDF417條碼。
* 資料矩陣條碼。
* 二維碼條碼。
* 科達巴爾條碼。
* 代碼128條碼。
* 39條碼。
* EAN-13條形碼。
* EAN-8條碼。

在解碼API中輸入為十六進位的字元集表示條形碼的內容會編碼為十六進位字串。 例如，如果UTF-8在形式中指定為字元編碼，而Hex在解碼操作中指定，則條形碼的內容在解碼輸出的&lt;`xb:content`元素中被編碼為Hex字串。 您可以在用戶端應用程式中建立應用程式邏輯，將此十六進位值轉換為原始內容。

**將資料轉換為XML資料來源**

在解碼表單資料後，您可將其轉換為XDP或XFDF資料。 例如，假設您要將資料匯入其他表單。 若要將資料匯入XFA表單，您必須將資料轉換為XDP資料。 如需詳細資訊，請參閱[匯入表單資料](/help/forms/developing/importing-exporting-data.md#importing-form-data)。

**處理解碼的資料**

您可以處理轉換的資料，以符合您的業務需求。 例如，在解碼並轉換資料後，您可以將其儲存至檔案、儲存在企業資料庫、填入其他表格等。 本節討論如何將轉換的資料儲存為XML檔案。

>[!NOTE]
>
>當行分隔字元和欄位分隔字元參數具有相同值時，條形碼表單服務無法解碼條形碼資料

**另請參閱**

[使用Java API解碼條形碼表單資料](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[使用web service API解碼條形碼表單資料](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#decode-barcoded-form-data-using-the-java-api}解碼條形碼表單資料

使用條形編碼表單API(Java)解碼表單資料：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立條碼表單用戶端API物件

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`BarcodedFormsServiceClient`對象。

1. 取得包含條形碼資料的PDF表格

   * 使用其建構函式並傳遞指定PDF檔案位置的字串值，建立代表包含條形碼資料之PDF表單的`java.io.FileInputStream`物件。
   * 使用其建構子並傳遞`java.io.FileInputStream`對象，建立`com.adobe.idp.Document`對象。

1. 從PDF表單解碼資料

   調用`BarcodedFormsServiceClient`物件的`decode`方法並傳遞下列值，以解碼表單資料：

   * 包含PDF表單的`com.adobe.idp.Document`物件。
   * `java.lang.Boolean`物件，指定是否解碼PDF417條碼。
   * `java.lang.Boolean`物件，指定是否解碼資料矩陣條碼。
   * `java.lang.Boolean`物件，指定是否解碼QR Code條碼。
   * `java.lang.Boolean`物件，指定是否解碼codabar條碼。
   * `java.lang.Boolean`對象，它指定是否解碼代碼128條形碼。
   * `java.lang.Boolean`物件，指定是否解碼代碼39條碼。
   * `java.lang.Boolean`對象，它指定是否解碼EAN-13條形碼。
   * `java.lang.Boolean`對象，它指定是否解碼EAN-8條形碼。
   * `com.adobe.livecycle.barcodedforms.CharSet`枚舉值，它指定條形碼中使用的字元集編碼值。

   `decode`方法返回包含已解碼表單資料的`org.w3c.dom.Document`對象。

1. 將資料轉換為XML資料來源

   調用`BarcodedFormsServiceClient`物件的`extractToXML`方法並傳遞下列值，將解碼的資料轉換為XDP或XFDF資料：

   * 包含解碼資料的`org.w3c.dom.Document`物件（請確定您使用`decode`方法的傳回值）。
   * `com.adobe.livecycle.barcodedforms.Delimiter`列舉值，指定行分隔字元。 建議您指定`Delimiter.Carriage_Return`。
   * `com.adobe.livecycle.barcodedforms.Delimiter`列舉值，指定欄位分隔字元。 例如，指定`Delimiter.Tab`。
   * `com.adobe.livecycle.barcodedforms.XMLFormat`列舉值，指定要將條形碼資料轉換為XDP或XFDF XML資料。 例如，指定`XMLFormat.XDP`將資料轉換為XDP資料。

   >[!NOTE]
   >
   >請勿為行分隔字元和欄位分隔字元參數指定相同的值。

   `extractToXML`方法返回`java.util.List`對象，其中每個元素都是`org.w3c.dom.Document`對象。 表單上的每個條形碼都有一個單獨的元素。 也就是說，如果表單上有四個條碼，則傳回的`java.util.List`物件中有四個元素。

1. 處理解碼的資料

   * 重複`java.util.List`物件，以取得位於清單中的每個`org.w3c.dom.Document`物件。
   * 對於清單中的每個元素，將`org.w3c.dom.Document`對象轉換為`com.adobe.idp.Document`對象。 （使用Java API示例將`org.w3c.dom.Document`對象轉換為`com.adobe.idp.Document`對象的應用程式邏輯顯示在解碼條形碼表單資料中）。
   * 調用`com.adobe.idp.Document`物件的`copyToFile`，並傳遞代表XML檔案的File物件，將XML資料儲存為XML檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API解碼條形碼表單資料](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#decode-barcoded-form-data-using-the-web-service-api}解碼條形碼表單資料

使用條形編碼表單API(web service)解碼表單資料：

1. 包含專案檔案

   * 建立一個使用條形碼表單服務WSDL的Microsoft .NET客戶端元件。 如需詳細資訊，請參閱[使用Base64編碼叫用AEM Forms。](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
   * 參考Microsoft .NET客戶端元件。 如需詳細資訊，請參閱[使用Base64編碼叫用AEM Forms的](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)中的「參考。NET客戶端元件」。

1. 建立條碼表單用戶端API物件

   使用使用條形碼表單服務WSDL的Microsoft .NET客戶端元件，通過調用其預設建構子建立`BarcodedFormsServiceService`對象。

1. 取得包含條形碼資料的PDF表格

   * 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存包含條碼的PDF檔案。
   * 通過調用其建構子並傳遞一個字串值來建立`System.IO.FileStream`對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
   * 調用`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為`binaryData`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。

1. 從PDF表單解碼資料

   調用`BarcodedFormsServiceService`物件的`decode`方法並傳遞下列值，以解碼表單資料：

   * 包含PDF表單的`BLOB`物件。
   * `Boolean`物件，指定是否解碼PDF417條碼。
   * `Boolean`物件，指定是否解碼資料矩陣條碼。
   * `Boolean`物件，指定是否解碼QR Code條碼。
   * `Boolean`物件，指定是否解碼codabar條碼。
   * `Boolean`對象，它指定是否解碼代碼128條形碼。
   * `Bolean`物件，指定是否解碼代碼39條碼。
   * `Boolean`對象，它指定是否解碼EAN-13條形碼。
   * `Boolean`對象，它指定是否解碼EAN-8條形碼。
   * `CharSet`枚舉值，它指定條形碼中使用的字元集編碼值。

   `decode`方法會傳回包含已解碼表單資料的字串值。

1. 將資料轉換為XML資料來源

   調用`BarcodedFormsServiceService`物件的`extractToXML`方法並傳遞下列值，將解碼的資料轉換為XDP或XFDF資料：

   * 包含解碼資料的字串值（請確定您使用`decode`方法的傳回值）。
   * `Delimiter`列舉值，指定行分隔字元。 建議您指定`Delimiter.Carriage_Return`。
   * `Delimiter`列舉值，指定欄位分隔字元。 例如，指定`Delimiter.Tab`。
   * `XMLFormat`列舉值，指定要將條形碼資料轉換為XDP或XFDF XML資料。 例如，指定`XMLFormat.XDP`將資料轉換為XDP資料。

   >[!NOTE]
   >
   >請勿為行分隔字元和欄位分隔字元參數指定相同的值。

   `extractToXML`方法返回`Object`陣列，其中每個元素都是`BLOB`實例。 表單上的每個條形碼都有一個單獨的元素。 也就是說，如果表單上有四個條碼，則傳回的`Object`陣列中有四個元素。

1. 處理解碼的資料

   * 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立對象，該字串值表示受保護PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存`encryptPDFUsingPassword`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象`binaryData`資料成員的值，以填充位元組陣列。
   * 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
   * 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
