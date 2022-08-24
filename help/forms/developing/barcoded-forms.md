---
title: 使用條形碼表單
seo-title: Working with barcoded forms
description: 使用Java API和Web服務API從包含條形碼的PDF表單或影像中解碼資料。
seo-description: Decode data from a PDF form or an image that contains a barcode using the Java API and Web Service API.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# 使用條形碼表單 {#working-with-barcoded-forms}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 關於條形碼表單服務 {#about-the-barcoded-forms-service}

條形碼表單服務自動從填寫和打印表單中捕獲資料，並將捕獲的資訊整合到組織的核心IT系統中。

使用條形碼表單服務，可以將一維和二維條形碼添加到互動式PDF forms。 然後，您可以將條形碼表格發佈到網站或通過電子郵件或光碟分發。 當用戶使用Adobe Reader、Acrobat專業或Acrobat Standard填寫條形碼表單時，條形碼會自動更新以編碼用戶提供的表單資料。 用戶可以以電子方式提交表單，或將表單打印到紙張上，然後通過郵件、傳真或手提方式提交。 您以後可以提取用戶提供的資料作為自動工作流的一部分，在審批流程和業務系統之間傳送資料。

有關條形碼表單服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 對條形碼表單資料進行解碼 {#decoding-barcoded-form-data}

您可以使用條形碼表單服務API從PDF表單或包含條形碼的影像中解碼資料。 解碼表單資料意味著提取位於條形碼中的資料。 在從PDF表單（或影像）解碼資料之前，用戶必須用資料填充表單。

>[!NOTE]
>
>有關條形碼表單服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要從PDF窗體中解碼資料，請執行以下步驟：

1. 包括項目檔案。
1. 建立條形碼formsClient API對象。
1. 獲取包含條形碼資料的PDF表單。
1. 從PDF窗體中解碼資料。
1. 將資料轉換為XML資料源。
1. 處理已解碼的資料。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，則包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)
* xercesImpl.jar(位於 &lt;install directory=&quot;&quot;>/Adobe/Adobe_體驗_Manager_forms/sdk/client-libs\thirdparty)

如果AEM Forms部署在非JBOSS的受支援的J2EE應用程式伺服器上，則需要將adobe-utilities.jar和jbossall-client.jar替換為特定於部署AEM Forms的J2EE應用程式伺服器的JAR檔案。 有關所有AEM FormsJAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立條形碼表單客戶端API對象**

在以寫程式方式執行條形碼表單服務操作之前，必須建立BarcodedForms服務客戶端。 如果使用Java API，請建立 `BarcodedFormsServiceClient` 的雙曲餘切值。 如果使用條形碼表單Web服務API，請建立 `BarcodedFormsServiceService` 的雙曲餘切值。

**獲取包含條形碼資料的PDF窗體**

必須獲取包含已填充有用戶資料的條形碼的PDF表單。

**從PDF窗體中解碼資料**

獲取包含條形碼的PDF表單（或影像）後，可以對資料進行解碼。 條形碼Forms服務支援以下類型的條形碼：

* PDF417條形碼。
* 資料矩陣條形碼。
* QR碼條形碼。
* 科達巴爾條形碼。
* 128條條形碼。
* 39條條形碼。
* EAN-13條形碼。
* EAN-8條形碼。

在解碼API中以十六進位輸入的字元集表示條形碼的內容被編碼為十六進位字串。 例如，如果UTF-8以格式指定為字元編碼，而Hex在解碼操作中指定，則條形碼的內容將在&lt; Comper Compore Conding(UTF-8)中以Hex字串形式編碼 `xb:content`>解碼輸出中的元素。 您可以通過在客戶端應用程式中建立應用程式邏輯來轉換此十六進位值以獲取原始內容。

**將資料轉換為XML資料源**

對表單資料進行解碼後，可將其轉換為XDP或XFDF資料。 例如，假定要將資料導入到其他窗體。 要將資料導入到XFA表單中，則必須將資料轉換為XDP資料。 有關資訊，請參見 [導入表單資料](/help/forms/developing/importing-exporting-data.md#importing-form-data)。

**處理已解碼的資料**

您可以處理轉換後的資料以滿足您的業務需求。 例如，在對資料進行解碼和轉換後，可以將其保存到檔案，將其儲存在企業資料庫中，填充其他表單等。 本節討論如何將轉換後的資料另存為XML檔案。

>[!NOTE]
>
>當行分隔符和欄位分隔符參數具有相同的值時，條形碼表單服務無法解碼條形碼資料

**另請參閱**

[使用Java API對條形碼表單資料進行解碼](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[使用Web服務API對條形碼表單資料進行解碼](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API對條形碼表單資料進行解碼 {#decode-barcoded-form-data-using-the-java-api}

使用條形碼表單API(Java)對表單資料進行解碼：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案。

1. 建立條形碼表單客戶端API對象

   建立 `BarcodedFormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 獲取包含條形碼資料的PDF窗體

   * 建立 `java.io.FileInputStream` 表示PDF表單的對象，該表單使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 從PDF窗體中解碼資料

   通過調用 `BarcodedFormsServiceClient` 對象 `decode` 方法並傳遞以下值：

   * 的 `com.adobe.idp.Document` 包含PDF窗體的對象。
   * A `java.lang.Boolean` 指定是否解碼PDF417條形碼的對象。
   * A `java.lang.Boolean` 指定是否解碼資料矩陣條形碼的對象。
   * A `java.lang.Boolean` 指定是否解碼QR碼條形碼的對象。
   * A `java.lang.Boolean` 指定是否解碼codabar條形碼的對象。
   * A `java.lang.Boolean` 指定是否解碼代碼128條形碼的對象。
   * A `java.lang.Boolean` 指定是否解碼代碼39條形碼的對象。
   * A `java.lang.Boolean` 指定是否解碼EAN-13條形碼的對象。
   * A `java.lang.Boolean` 指定是否解碼EAN-8條形碼的對象。
   * A `com.adobe.livecycle.barcodedforms.CharSet` 指定條形碼中使用的字元集編碼值的枚舉值。

   的 `decode` 方法返回 `org.w3c.dom.Document` 包含已解碼表單資料的對象。

1. 將資料轉換為XML資料源

   通過調用 `BarcodedFormsServiceClient` 對象 `extractToXML` 方法並傳遞以下值：

   * 的 `org.w3c.dom.Document` 包含已解碼資料的對象(確保使用 `decode` 方法的返回值)。
   * A `com.adobe.livecycle.barcodedforms.Delimiter` 指定行分隔符的枚舉值。 建議您指定 `Delimiter.Carriage_Return`。
   * A `com.adobe.livecycle.barcodedforms.Delimiter` 指定欄位分隔符的枚舉值。 例如，指定 `Delimiter.Tab`。
   * A `com.adobe.livecycle.barcodedforms.XMLFormat` 指定是將條形碼資料轉換為XDP還是XFDF XML資料的枚舉值。 例如，指定 `XMLFormat.XDP` 將資料轉換為XDP資料。

   >[!NOTE]
   >
   >不要為行分隔符和欄位分隔符參數指定相同的值。

   的 `extractToXML` 方法返回 `java.util.List` 其中每個元素為 `org.w3c.dom.Document` 的雙曲餘切值。 窗體上的每個條形碼都有單獨的元素。 即，如果表單上有四個條形碼，則返回的表單中有四個元素 `java.util.List` 的雙曲餘切值。

1. 處理已解碼的資料

   * 迭代 `java.util.List` 對象獲取每個對象 `org.w3c.dom.Document` 清單中的對象。
   * 對於清單中的每個元素，轉換 `org.w3c.dom.Document` 對象 `com.adobe.idp.Document` 的雙曲餘切值。 (轉換 `org.w3c.dom.Document` 對象 `com.adobe.idp.Document` 對象顯示在使用Java API示例對條形碼表單資料進行解碼中)。
   * 通過調用 `com.adobe.idp.Document` 對象 `copyToFile`，並傳遞表示XML檔案的檔案對象。

**另請參閱**

[快速啟動（SOAP模式）:使用Java API解碼條形碼表單資料](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API對條形碼表單資料進行解碼 {#decode-barcoded-form-data-using-the-web-service-api}

使用條形碼表單API（Web服務）對表單資料進行解碼：

1. 包括項目檔案

   * 建立使用條形碼表單服務WSDL的Microsoft.NET客戶端程式集。 有關資訊，請參見 [使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。
   * 引用Microsoft.NET客戶端程式集。 有關資訊，請參閱中的「引用.NET客戶端程式集」 [使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。

1. 建立條形碼表單客戶端API對象

   使用使用條形碼表單服務WSDL的Microsoft.NET客戶端程式集，建立 `BarcodedFormsServiceService` 調用其預設建構子。

1. 獲取包含條形碼資料的PDF窗體

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存包含條形碼的PDF文檔。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 方法，將位元組陣列、起始位置和流長度傳遞給讀取。
   * 填充 `BLOB` 通過指定對象 `binaryData` 屬性。

1. 從PDF窗體中解碼資料

   通過調用 `BarcodedFormsServiceService` 對象 `decode` 方法並傳遞以下值：

   * 的 `BLOB` 包含PDF窗體的對象。
   * A `Boolean` 指定是否解碼PDF417條形碼的對象。
   * A `Boolean` 指定是否解碼資料矩陣條形碼的對象。
   * A `Boolean` 指定是否解碼QR碼條形碼的對象。
   * A `Boolean` 指定是否解碼codabar條形碼的對象。
   * A `Boolean` 指定是否解碼代碼128條形碼的對象。
   * A `Bolean` 指定是否解碼代碼39條形碼的對象。
   * A `Boolean` 指定是否解碼EAN-13條形碼的對象。
   * A `Boolean` 指定是否解碼EAN-8條形碼的對象。
   * A `CharSet` 指定條形碼中使用的字元集編碼值的枚舉值。

   的 `decode` 方法返回包含已解碼表單資料的字串值。

1. 將資料轉換為XML資料源

   通過調用 `BarcodedFormsServiceService` 對象 `extractToXML` 方法並傳遞以下值：

   * 包含已解碼資料的字串值(確保使用 `decode` 方法的返回值)。
   * A `Delimiter` 指定行分隔符的枚舉值。 建議您指定 `Delimiter.Carriage_Return`。
   * A `Delimiter` 指定欄位分隔符的枚舉值。 例如，指定 `Delimiter.Tab`。
   * A `XMLFormat` 指定是將條形碼資料轉換為XDP還是XFDF XML資料的枚舉值。 例如，指定 `XMLFormat.XDP` 將資料轉換為XDP資料。

   >[!NOTE]
   >
   >不要為行分隔符和欄位分隔符參數指定相同的值。

   的 `extractToXML` 方法返回 `Object` 陣列，其中每個元素是 `BLOB` 實例。 窗體上的每個條形碼都有單獨的元素。 即，如果表單上有四個條形碼，則返回的表單中有四個元素 `Object` 陣列。

1. 處理已解碼的資料

   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示安全PDF文檔的檔案位置。
   * 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `encryptPDFUsingPassword` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

**另請參閱**

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
