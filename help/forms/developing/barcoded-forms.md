---
title: 使用條形碼表單
seo-title: 使用條形碼表單
description: 'null'
seo-description: 'null'
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# 使用條形碼表單 {#working-with-barcoded-forms}

## 關於條碼表單服務 {#about-the-barcoded-forms-service}

條形碼表單服務可自動從填寫及列印表單擷取資料，並將擷取的資訊整合至組織的核心IT系統。

使用條碼表單服務，您可以將一維和二維條碼新增至互動式PDF表單。 然後，您可以將條形碼表格發佈至網站，或以電子郵件或光碟散發。 當使用者使用Adobe Reader、Acrobat Professional或Acrobat Standard填寫條碼表格時，會自動更新條碼，以編碼使用者提供的表格資料。 使用者可以電子方式提交表格，或列印成紙本，再以郵件、傳真或手形方式提交。 您稍後可以擷取使用者提供的資料作為自動化工作流程的一部分，在核准程式和商業系統之間傳送資料。

如需有關條碼表單服務的詳細資訊，請參 [閱「AEM表單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 解碼條形碼表單資料 {#decoding-barcoded-form-data}

您可以使用條碼表單服務API來解碼PDF表單或包含條碼的影像中的資料。 解碼表單資料意味著提取位於條形碼中的資料。 在從PDF表單（或影像）解碼資料之前，使用者必須先在表單中填入資料。

>[!NOTE]
>
>如需有關條碼表單服務的詳細資訊，請參 [閱「AEM表單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要解碼PDF表單中的資料，請執行下列步驟：

1. 包含專案檔案。
1. 建立條碼表單用戶端API物件。
1. 取得包含條形碼資料的PDF表格。
1. 解碼PDF表單中的資料。
1. 將資料轉換為XML資料來源。
1. 處理解碼的資料。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）
* xercesImpl.jar（位於&lt;install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty）

如果AEM Forms部署在非JBOSS的受支援J2EE應用程式伺服器上，則您將需要以JAR檔案取代adobe-utilities.jar和jbossall-client.jar，這些檔案是部署AEM Forms的J2EE應用程式伺服器專用的。 如需所有AEM Forms JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立條碼表單用戶端API物件**

在以寫程式方式執行條形碼表單服務操作之前，必須建立Barcoded Forms服務客戶端。 如果您使用Java API，請建立物 `BarcodedFormsServiceClient` 件。 如果您使用條形編碼表單Web服務API，請建立物 `BarcodedFormsServiceService` 件。

**取得包含條形碼資料的PDF表格**

您必須取得包含已填入使用者資料之條碼的PDF表單。

**從PDF表單解碼資料**

取得包含條碼的PDF表單（或影像）後，您就可以解碼資料。 Barcoded Forms服務支援下列條碼類型：

* PDF417條碼。
* 資料矩陣條碼。
* 二維碼條碼。
* 科達巴爾條碼。
* 代碼128條碼。
* 39條碼。
* EAN-13條形碼。
* EAN-8條碼。

在解碼API中輸入為十六進位的字元集表示條形碼的內容會編碼為十六進位字串。 例如，如果UTF-8在形式中指定為字元編碼，而Hex在解碼操作中指定，則條形碼的內容在解碼輸出的&lt; `xb:content`>元素中被編碼為Hex字串。 您可以在用戶端應用程式中建立應用程式邏輯，將此十六進位值轉換為原始內容。

**將資料轉換為XML資料來源**

在解碼表單資料後，您可將其轉換為XDP或XFDF資料。 例如，假設您要將資料匯入其他表單。 若要將資料匯入XFA表單，您必須將資料轉換為XDP資料。 如需詳細資訊，請參 [閱匯入表單資料](/help/forms/developing/importing-exporting-data.md#importing-form-data)。

**處理解碼的資料**

您可以處理轉換的資料，以符合您的業務需求。 例如，在解碼並轉換資料後，您可以將其儲存至檔案、儲存在企業資料庫、填入其他表格等。 本節討論如何將轉換的資料儲存為XML檔案。

>[!NOTE]
>
>當行分隔字元和欄位分隔字元參數具有相同值時，條形碼表單服務無法解碼條形碼資料

**另請參閱**

[使用Java API解碼條形碼表單資料](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[使用web service API解碼條形碼表單資料](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API解碼條形碼表單資料 {#decode-barcoded-form-data-using-the-java-api}

使用條形編碼表單API(Java)解碼表單資料：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立條碼表單用戶端API物件

   使用其 `BarcodedFormsServiceClient` 建構函式並傳遞包含連線屬性 `ServiceClientFactory` 的物件，以建立物件。

1. 取得包含條形碼資料的PDF表格

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表包含條形碼資料之PDF表單的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 從PDF表單解碼資料

   調用物件的方法並傳 `BarcodedFormsServiceClient` 遞下列值， `decode` 以解碼表單資料：

   * 包 `com.adobe.idp.Document` 含PDF表單的物件。
   * 指定 `java.lang.Boolean` 是否解碼PDF417條碼的物件。
   * 指定 `java.lang.Boolean` 是否解碼資料矩陣條形碼的對象。
   * 指定 `java.lang.Boolean` 是否解碼QR code條形碼的對象。
   * 指定 `java.lang.Boolean` 是否解碼codabar條形碼的對象。
   * 指定 `java.lang.Boolean` 是否解碼代碼128條形碼的對象。
   * 指定 `java.lang.Boolean` 是否解碼代碼39條形碼的對象。
   * 指定 `java.lang.Boolean` 是否解碼EAN-13條形碼的對象。
   * 指定 `java.lang.Boolean` 是否對EAN-8條形碼進行解碼的對象。
   * 一 `com.adobe.livecycle.barcodedforms.CharSet` 個枚舉值，它指定條形碼中使用的字元集編碼值。
   該方 `decode` 法返回包 `org.w3c.dom.Document` 含已解碼表單資料的對象。

1. 將資料轉換為XML資料來源

   調用物件的方法並傳遞下列值，將解碼的資 `BarcodedFormsServiceClient` 料轉 `extractToXML` 換為XDP或XFDF資料：

   * 包 `org.w3c.dom.Document` 含解碼資料的物件(請確定您使 `decode` 用方法的傳回值)。
   * 指定 `com.adobe.livecycle.barcodedforms.Delimiter` 行分隔符的枚舉值。 建議您指定 `Delimiter.Carriage_Return`。
   * 指定 `com.adobe.livecycle.barcodedforms.Delimiter` 欄位分隔符的枚舉值。 例如，指定 `Delimiter.Tab`。
   * 一 `com.adobe.livecycle.barcodedforms.XMLFormat` 個枚舉值，它指定將條形碼資料轉換為XDP或XFDF XML資料。 例如，指定 `XMLFormat.XDP` 將資料轉換為XDP資料。
   >[!NOTE]
   >
   >請勿為行分隔字元和欄位分隔字元參數指定相同的值。

   該方 `extractToXML` 法返回一 `java.util.List` 個對象，其中每個元素都是 `org.w3c.dom.Document` 對象。 表單上的每個條形碼都有一個單獨的元素。 也就是說，如果表單上有四個條碼，則傳回的物件中會有四個 `java.util.List` 元素。

1. 處理解碼的資料

   * 重複該對 `java.util.List` 像，以獲 `org.w3c.dom.Document` 取清單中的每個對象。
   * 對於清單中的每個元素，將對 `org.w3c.dom.Document` 像轉換為對 `com.adobe.idp.Document` 像。 (使用Java API範例將物 `org.w3c.dom.Document` 件轉換為物 `com.adobe.idp.Document` 件的應用程式邏輯，會顯示在「解碼條形碼表單資料」中)。
   * 調用物件並傳遞代表XML檔案的 `com.adobe.idp.Document` 檔案物件， `copyToFile`將XML資料儲存為XML檔案。

**另請參閱**

[快速入門（SOAP模式）:使用Java API解碼條形碼表單資料](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API解碼條形碼表單資料 {#decode-barcoded-form-data-using-the-web-service-api}

使用條形編碼表單API(web service)解碼表單資料：

1. 包含專案檔案

   * 建立一個使用條形碼表單服務WSDL的Microsoft .NET客戶端元件。 如需詳細資訊，請 [參閱「使用Base64編碼叫用AEM Forms」](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。
   * 參考Microsoft .NET客戶端元件。 如需詳細資訊，請參閱使用Base64編碼叫用AEM Forms [中的「參考。NET用戶端元件」](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。

1. 建立條碼表單用戶端API物件

   使用使用條形碼表單服務WSDL的Microsoft .NET客戶端元件，通過調用其缺 `BarcodedFormsServiceService` 省建構子來建立對象。

1. 取得包含條形碼資料的PDF表格

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存包含條形碼的PDF文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `binaryData` 使其包含位元組陣列的內容。

1. 從PDF表單解碼資料

   調用物件的方法並傳 `BarcodedFormsServiceService` 遞下列值， `decode` 以解碼表單資料：

   * 包 `BLOB` 含PDF表單的物件。
   * 指定 `Boolean` 是否解碼PDF417條碼的物件。
   * 指定 `Boolean` 是否解碼資料矩陣條形碼的對象。
   * 指定 `Boolean` 是否解碼QR code條形碼的對象。
   * 指定 `Boolean` 是否解碼codabar條形碼的對象。
   * 指定 `Boolean` 是否解碼代碼128條形碼的對象。
   * 指定 `Bolean` 是否解碼代碼39條形碼的對象。
   * 指定 `Boolean` 是否解碼EAN-13條形碼的對象。
   * 指定 `Boolean` 是否對EAN-8條形碼進行解碼的對象。
   * 一 `CharSet` 個枚舉值，它指定條形碼中使用的字元集編碼值。
   該方 `decode` 法返回包含已解碼表單資料的字串值。

1. 將資料轉換為XML資料來源

   調用物件的方法並傳遞下列值，將解碼的資 `BarcodedFormsServiceService` 料轉 `extractToXML` 換為XDP或XFDF資料：

   * 包含解碼資料的字串值(請確定您使用 `decode` 方法的傳回值)。
   * 指定 `Delimiter` 行分隔符的枚舉值。 建議您指定 `Delimiter.Carriage_Return`。
   * 指定 `Delimiter` 欄位分隔符的枚舉值。 例如，指定 `Delimiter.Tab`。
   * 一 `XMLFormat` 個枚舉值，它指定將條形碼資料轉換為XDP或XFDF XML資料。 例如，指定 `XMLFormat.XDP` 將資料轉換為XDP資料。
   >[!NOTE]
   >
   >請勿為行分隔字元和欄位分隔字元參數指定相同的值。

   該方 `extractToXML` 法返回 `Object` 一個陣列，其中每個元素都是 `BLOB` 實例。 表單上的每個條形碼都有一個單獨的元素。 也就是說，如果表單上有4個條碼，則傳回的陣列中有4個元 `Object` 素。

1. 處理解碼的資料

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示受保護PDF文檔的檔案位置。
   * 建立一個位元組陣列，該陣列儲存由方 `BLOB` 法返回的對象的資料內 `encryptPDFUsingPassword` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `binaryData` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
