---
title: 使用條碼式表單
description: 使用Java API和網站服務API，從PDF表單或包含條碼的影像解碼資料。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,Barcoded Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 0%

---

# 使用條碼式表單 {#working-with-barcoded-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於條碼式Forms服務 {#about-the-barcoded-forms-service}

條碼式表單服務可自動從填寫並列印的表單中擷取資料，並將擷取的資訊整合到組織的核心IT系統中。

使用條碼式表單服務，您可以將一維與二維條碼新增至互動式PDF forms。 然後，您可以將條碼式表單發佈至網站，或透過電子郵件或CD分發。 當使用者使用Adobe Reader、Acrobat Professional或Acrobat Standard填寫條碼表單時，條碼會自動更新以編碼使用者提供的表單資料。 使用者可以電子方式提交表單，或列印為紙張，並以郵件、傳真或手遞方式提交。 您稍後可以擷取使用者提供的資料，做為自動化工作流程的一部分，在核准程式和業務系統之間路由傳送資料。

如需條碼式表單服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 解碼條碼式表單資料 {#decoding-barcoded-form-data}

您可以使用條碼式表單服務API，將PDF表單或包含條碼之影像中的資料解碼。 解碼表單資料表示擷取條碼中的資料。 在可從PDF表單（或影像）解碼資料之前，使用者必須先將資料填入表單。

>[!NOTE]
>
>如需條碼式表單服務的詳細資訊，請參閱[AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要解碼PDF表單中的資料，請執行下列步驟：

1. 包含專案檔案。
1. 建立條碼式formsClient API物件。
1. 取得包含條碼資料的PDF表單。
1. 解碼PDF表單中的資料。
1. 將資料轉換為XML資料來源。
1. 處理解碼的資料。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，則請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)
* xercesImpl.jar (位於&lt;安裝目錄>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

如果將AEM Forms部署在受支援的J2EE應用程式伺服器（不是JBOSS）上，則您必須將adobe-utilities.jar和jbossall-client.jar取代為特定於已部署AEM Forms之J2EE應用程式伺服器的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立條碼式表單使用者端API物件**

您必須先建立條碼式Forms服務使用者端，才能以程式設計方式執行條碼式表單服務作業。 如果您使用Java API，請建立`BarcodedFormsServiceClient`物件。 如果您使用條碼式表單Web服務API，請建立`BarcodedFormsServiceService`物件。

**取得包含條碼資料的PDF表單**

取得內含已填入使用者資料之條碼的PDF表單。

**從PDF表單解碼資料**

取得包含條碼的PDF表單（或影像）後，您就可以將資料解碼。 條碼Forms服務支援下列型別的條碼：

* PDF417條碼。
* 資料矩陣條碼。
* QR碼條碼。
* 程式碼標籤條碼。
* 代碼128條碼。
* 代碼39條碼。
* ean-13條碼。
* EAN-8條碼

在解碼API中將字元集輸入設為十六進位表示，條碼的內容會編碼為十六進位字串。 例如，如果在表單中將UTF-8指定為字元編碼，並在解碼作業中指定Hex，則條碼的內容會在解碼輸出中編碼為&lt; `xb:content`>專案中的Hex字串。 您可以在使用者端應用程式中建立應用程式邏輯，轉換此十六進位值以取得原始內容。

**將資料轉換為XML資料來源**

將表單資料解碼後，可將其轉換為XDP或XFDF資料。 例如，假設您要將資料匯入另一個表單。 若要將資料匯入XFA表單，您必須將資料轉換為XDP資料。 如需詳細資訊，請參閱[匯入表單資料](/help/forms/developing/importing-exporting-data.md#importing-form-data)。

**處理解碼的資料**

您可以處理轉換後的資料，以符合業務需求。 例如，解碼並轉換資料後，您可以將其儲存至檔案、儲存在企業資料庫中、填入其他表單等。 本節討論如何將轉換的資料儲存為XML檔案。

>[!NOTE]
>
>當行分隔符號和欄位分隔符號引數具有相同的值時，條碼式表單服務無法解碼條碼資料

**另請參閱**

[使用Java API將條碼式表單資料解碼](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[使用網站服務API將條碼式表單資料解碼](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將條碼式表單資料解碼 {#decode-barcoded-form-data-using-the-java-api}

使用條碼式Forms API(Java)將表單資料解碼：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立條碼式表單使用者端API物件

   使用它的建構函式並傳遞包含連線屬性的`ServiceClientFactory`物件來建立`BarcodedFormsServiceClient`物件。

1. 取得包含條碼資料的PDF表單

   * 使用它的建構函式，並傳遞指定PDF檔案位置的字串值，來建立代表包含條碼式資料的PDF表單的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 解碼PDF表單中的資料

   透過叫用`BarcodedFormsServiceClient`物件的`decode`方法並傳遞下列值來解碼表單資料：

   * 包含PDF表單的`com.adobe.idp.Document`物件。
   * `java.lang.Boolean`物件，指定是否要解碼PDF417條碼。
   * 指定是否要解碼資料矩陣條碼的`java.lang.Boolean`物件。
   * 指定是否要解碼QR碼條碼的`java.lang.Boolean`物件。
   * 指定是否要解碼程式碼標籤條碼的`java.lang.Boolean`物件。
   * `java.lang.Boolean`物件，指定是否要解碼代碼128條碼。
   * `java.lang.Boolean`物件，指定是否要解碼代碼39條碼。
   * 指定是否要解碼EAN-13條碼的`java.lang.Boolean`物件。
   * 指定是否要解碼EAN-8條碼的`java.lang.Boolean`物件。
   * 指定條碼中所使用字元集編碼值的`com.adobe.livecycle.barcodedforms.CharSet`列舉值。

   `decode`方法傳回包含已解碼表單資料的`org.w3c.dom.Document`物件。

1. 將資料轉換為XML資料來源

   呼叫`BarcodedFormsServiceClient`物件的`extractToXML`方法並傳遞下列值，將解碼的資料轉換為XDP或XFDF資料：

   * 包含已解碼資料的`org.w3c.dom.Document`物件（請確定您使用`decode`方法的傳回值）。
   * 指定行分隔符號的`com.adobe.livecycle.barcodedforms.Delimiter`列舉值。 建議您指定`Delimiter.Carriage_Return`。
   * 指定欄位分隔符號的`com.adobe.livecycle.barcodedforms.Delimiter`列舉值。 例如，指定`Delimiter.Tab`。
   * `com.adobe.livecycle.barcodedforms.XMLFormat`列舉值，指定要將條碼資料轉換為XDP或XFDF XML資料。 例如，指定`XMLFormat.XDP`將資料轉換為XDP資料。

   >[!NOTE]
   >
   >請勿為行分隔符號和欄位分隔符號引數指定相同的值。

   `extractToXML`方法傳回`java.util.List`物件，其中每個元素都是`org.w3c.dom.Document`物件。 位於表單上的每個條碼都有個別的元素。 也就是說，如果表單上有四個條碼，則傳回的`java.util.List`物件中有四個元素。

1. 處理解碼的資料

   * 逐一檢視`java.util.List`物件，以取得清單中的每個`org.w3c.dom.Document`物件。
   * 針對清單中的每個元素，將`org.w3c.dom.Document`物件轉換為`com.adobe.idp.Document`物件。 （將`org.w3c.dom.Document`物件轉換為`com.adobe.idp.Document`物件的應用程式邏輯會顯示在使用Java API範例解碼條碼式表單資料中）。
   * 呼叫`com.adobe.idp.Document`物件的`copyToFile`，並傳遞代表XML檔案的File物件，將XML資料儲存為XML檔案。

**另請參閱**

[快速入門(SOAP模式)：使用Java API將條碼式表單資料解碼](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將條碼式表單資料解碼 {#decode-barcoded-form-data-using-the-web-service-api}

使用條碼式Forms API （Web服務）將表單資料解碼：

1. 包含專案檔案

   * 建立使用條碼式表單服務WSDL的Microsoft .NET使用者端元件。 如需詳細資訊，請參閱[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。
   * 參考Microsoft .NET使用者端元件。 如需詳細資訊，請參閱[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)中的「參考.NET使用者端元件」。

1. 建立條碼式表單使用者端API物件

   使用使用條碼式表單服務WSDL的Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`BarcodedFormsServiceService`物件。

1. 取得包含條碼資料的PDF表單

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存包含條碼的PDF檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派物件的`binaryData`屬性，填入`BLOB`物件。

1. 解碼PDF表單中的資料

   透過叫用`BarcodedFormsServiceService`物件的`decode`方法並傳遞下列值來解碼表單資料：

   * 包含PDF表單的`BLOB`物件。
   * `Boolean`物件，指定是否要解碼PDF417條碼。
   * 指定是否要解碼資料矩陣條碼的`Boolean`物件。
   * 指定是否要解碼QR碼條碼的`Boolean`物件。
   * 指定是否要解碼程式碼標籤條碼的`Boolean`物件。
   * `Boolean`物件，指定是否要解碼代碼128條碼。
   * `Bolean`物件，指定是否要解碼代碼39條碼。
   * 指定是否要解碼EAN-13條碼的`Boolean`物件。
   * 指定是否要解碼EAN-8條碼的`Boolean`物件。
   * 指定條碼中所使用字元集編碼值的`CharSet`列舉值。

   `decode`方法傳回包含已解碼表單資料的字串值。

1. 將資料轉換為XML資料來源

   呼叫`BarcodedFormsServiceService`物件的`extractToXML`方法並傳遞下列值，將解碼的資料轉換為XDP或XFDF資料：

   * 包含已解碼資料的字串值（請確定您使用`decode`方法的傳回值）。
   * 指定行分隔符號的`Delimiter`列舉值。 建議您指定`Delimiter.Carriage_Return`。
   * 指定欄位分隔符號的`Delimiter`列舉值。 例如，指定`Delimiter.Tab`。
   * `XMLFormat`列舉值，指定要將條碼資料轉換為XDP或XFDF XML資料。 例如，指定`XMLFormat.XDP`將資料轉換為XDP資料。

   >[!NOTE]
   >
   >請勿為行分隔符號和欄位分隔符號引數指定相同的值。

   `extractToXML`方法傳回`Object`陣列，其中每個元素都是`BLOB`執行個體。 位於表單上的每個條碼都有個別的元素。 也就是說，如果表單上有四個條碼，則傳回的`Object`陣列中有四個元素。

1. 處理解碼的資料

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表受保護PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存`encryptPDFUsingPassword`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`binaryData`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
