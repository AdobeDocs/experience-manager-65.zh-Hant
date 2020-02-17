---
title: 數位簽署和認證檔案
seo-title: 數位簽署和認證檔案
description: 'null'
seo-description: 'null'
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 數位簽署和認證檔案 {#digitally-signing-and-certifying-documents}

**關於簽名服務**

簽名服務可讓貴組織保護其發送及接收之Adobe PDF檔案的安全性和隱私權。 本服務使用數位簽章和認證，以確保只有預期的收件者才能變更檔案。 由於安全性功能會套用至檔案本身，因此檔案在整個生命週期中都會保持安全並受到控制。 檔案在防火牆外、離線下載時，以及送出回您的組織時，都能保有安全。

>[!NOTE]
>
>您可以為「簽名」服務建立自訂的簽名處理常式，該處理常式會在呼叫特定作業（例如簽署PDF檔案）時被叫用。

**簽名欄位名**

某些簽名服務操作要求您指定執行操作的簽名欄位的名稱。 例如，在簽署PDF檔案時，您可以指定要簽署的簽名欄位名稱。 假設簽名欄位的完整名稱為 `form1[0].Form1[0].SignatureField1[0]`。 您可以指定 `SignatureField1[0]` 而非 `form1[0].Form1[0].SignatureField1[0]`。

有時衝突會導致簽名服務在錯誤欄位中籤名（或執行另一個需要簽名欄位名稱的操作）。 此衝突是同一PDF檔案中 `SignatureField1[0]` 兩個或兩個以上位置出現的名稱的結果。 例如，假設PDF檔案包含兩個名為和且您指定 `form1[0].Form1[0].SignatureField1[0]` 的簽 `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` 名欄位 `SignatureField1[0]`。 在這種情況下，簽章服務會簽署它在重複檔案中所有簽名欄位時所找到的第一個簽名欄位。

如果PDF檔案中有多個簽名欄位，建議您指定簽名欄位的完整名稱。 即，指定 `form1[0].Form1[0].SignatureField1[0]`而非 `SignatureField1[0]`。

您可以使用簽名服務完成下列工作：

* 將數位簽章欄位新增及刪除至PDF檔案。 (請參 [閱新增簽名欄](digitally-signing-certifying-documents.md#adding-signature-fields)。)
* 擷取PDF檔案中的簽名欄位名稱。 (請參 [閱擷取簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)。)
* 修改簽名欄位。 (請參 [閱修改簽名欄](digitally-signing-certifying-documents.md#modifying-signature-fields)。)
* 數位簽署PDF檔案。 (請參 [閱數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)
* 認證PDF檔案。 (請參閱 [認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)。)
* 驗證PDF檔案中的數位簽名。 (請參閱 [驗證數位簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。)
* 驗證PDF檔案中的所有數位簽名。 (請參閱 [驗證多個數位簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。)
* 從簽名欄位移除數位簽名。 (請參閱 [移除數位簽章](digitally-signing-certifying-documents.md#removing-digital-signatures)。)

   ***注意&#x200B;**:如需簽名服務的詳細資訊，請參閱「AEM表[單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。*

## 新增簽名欄位 {#adding-signature-fields}

數位簽名會出現在簽名欄位中，這些欄位是包含簽名圖形表示的表格欄位。 簽名欄位可以是可見或不可見的。 簽署者可以使用預先存在的簽名欄位，或以程式設計方式新增簽名欄位。 在這兩種情況下，簽名欄位必須存在，才能簽署PDF檔案。

您可以使用簽名服務Java API或簽名網站服務API，以程式設計方式新增簽名欄位。 您可以在PDF檔案中新增多個簽名欄位；但是，每個簽名欄位名必須是唯一的。

>[!NOTE]
>
>有些PDF檔案類型不允許您以程式設計方式新增簽名欄位。 如需「簽名服務」和新增簽名欄位的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

若要將簽名欄位新增至PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得新增簽名欄位的PDF檔案。
1. 新增簽名欄位。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得新增簽名欄位的PDF檔案**

您必須取得新增簽名欄位的PDF檔案。

**新增簽名欄位**

若要成功將簽名欄位新增至PDF檔案，請指定用以識別簽名欄位位置的坐標值。 （如果您新增不可見的簽名欄位，則不需要這些值。）此外，您也可以指定在將簽名套用至簽名欄位後，PDF檔案中的哪些欄位會被鎖定。

**將PDF檔案儲存為PDF檔案**

在簽章服務新增簽名欄位至PDF檔案後，您可以將檔案儲存為PDF檔案，讓使用者在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API新增簽名欄位 {#add-signature-fields-using-the-java-api}

使用簽名API(Java)新增簽名欄位：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `SignatureServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得新增簽名欄位的PDF檔案

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，以建立代表PDF檔案的物件，以新增簽名欄位。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 新增簽名欄位

   * 使用 `PositionRectangle` 其建構子建立指定簽名欄位位置的對象。 在建構函式中，指定坐標值。
   * 如果需要，請創 `FieldMDPOptions` 建一個對象，該對象指定在將數字簽名應用於簽名欄位時鎖定的欄位。
   * 叫用物件的方法並傳遞下列值，將簽 `SignatureServiceClient` 名欄位新 `addSignatureField` 增至PDF檔案：

      * A `com.adobe.idp`. `Document` 物件，代表新增簽名欄位的PDF檔案。
      * 指定簽名欄位名稱的字串值。
      * 一 `java.lang.Integer` 個值，代表將簽名欄位添加到的頁碼。
      * 指 `PositionRectangle` 定簽名欄位位置的對象。
      * 指定 `FieldMDPOptions` 在數位簽名套用至簽名欄位後鎖定之PDF檔案欄位的物件。 此參數值是可選的，您可以通過 `null`。
   * 指定 `PDFSeedValueOptions` 各種運行時值的對象。 此參數值是可選的，您可以通過 `null`。

      方 `addSignatureField` 法傳回 `com.adobe.idp`。 `Document` 物件，代表包含簽名欄位的PDF檔案。
   >[!NOTE]
   >
   >您可以叫用物 `SignatureServiceClient` 件的方法， `addInvisibleSignatureField` 以新增不可見的簽名欄位。

1. 將PDF檔案儲存為PDF檔案

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `com.adobe.idp`。 `Document` 物件的方 `copyToFile` 法，將物件的內容復 `Document` 制至檔案。 請確定您使用 `com.adobe.idp`。 `Document` 由方法返回的對 `addSignatureField` 像。

**另請參閱**

[簽章服務API快速入門](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用web service API新增簽名欄位 {#add-signature-fields-using-the-web-service-api}

若要使用簽名API(web service)新增簽名欄位：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立簽名用戶端

   * 使用其 `SignatureServiceClient` 預設建構函式建立物件。
   * 使用建 `SignatureServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `SignatureServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得新增簽名欄位的PDF檔案

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用來儲存包含簽名欄位的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 新增簽名欄位

   叫用物件的方法並傳遞下列值，將簽 `SignatureServiceClient` 名欄位新 `addSignatureField` 增至PDF檔案：

   * 表 `BLOB` 示PDF文檔的對象，其中添加了簽名欄位。
   * 指定簽名欄位名稱的字串值。
   * 一個整數值，它表示要向其添加簽名欄位的頁碼。
   * 指 `PositionRect` 定簽名欄位位置的對象。
   * 指定 `FieldMDPOptions` 在數位簽名套用至簽名欄位後鎖定之PDF檔案欄位的物件。 此參數值是可選的，您可以通過 `null`。
   * 指定 `PDFSeedValueOptions` 各種運行時值的對象。 此參數值是可選的，您可以通過 `null`。
   此方 `addSignatureField` 法會傳回 `BLOB` 代表包含簽名欄位之PDF檔案的物件。

1. 將PDF檔案儲存為PDF檔案

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示將包含簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，該陣列儲存方 `BLOB` 法返回的對象的內 `addSignatureField` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `binaryData` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 檢索簽名欄位名稱 {#retrieving-signature-field-names}

您可以擷取位於要簽署或認證之PDF檔案中之所有簽名欄位的名稱。 如果您不確定PDF檔案中的簽名欄位名稱，或想要驗證名稱，則可以以程式設計方式擷取這些名稱。 簽名服務會傳回簽名欄位的完全限定名稱，例如 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

>[!NOTE]
>
>如需簽名服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟摘要 {#summary_of_steps-1}

要檢索簽名欄位名稱，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含簽名欄位的PDF檔案。
1. 擷取簽名欄位名稱。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得包含簽名欄位的PDF檔案**

擷取包含簽名欄位的PDF檔案。

**擷取簽名欄位名稱**

在擷取包含一或多個簽名欄位的PDF檔案後，可以擷取簽名欄位名稱。

**另請參閱**

[使用Java API擷取簽名欄位名稱](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用web service API擷取簽名欄位](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API擷取簽名欄位名稱 {#retrieve-signature-field-names-using-the-java-api}

使用簽名API(Java)擷取簽名欄位名稱：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `SignatureServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得包含簽名欄位的PDF檔案

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表包含簽名欄位之PDF檔案的物件。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 擷取簽名欄位名稱

   * 叫用物件的方法並傳遞包 `SignatureServiceClient` 含簽名欄 `getSignatureFieldList` 位的PDF `com.adobe.idp.Document` 檔案物件，以擷取簽名欄位名稱。 此方法傳回 `java.util.List` 物件，其中每個元素都包含一 `PDFSignatureField` 個物件。 使用此對象，您可以獲取有關簽名欄位的其他資訊，如簽名欄位是否可見。
   * 重複物件以 `java.util.List` 判斷是否有簽名欄位名稱。 對於PDF檔案中的每個簽名欄位，您可以取得個別的 `PDFSignatureField` 物件。 若要取得簽名欄位的名稱，請叫 `PDFSignatureField` 用物件的方 `getName` 法。 此方法傳回指定簽名欄位名稱的字串值。

**另請參閱**

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速入門（SOAP模式）:使用Java API檢索簽名欄位名稱](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API擷取簽名欄位 {#retrieve-signature-field-using-the-web-service-api}

使用簽名API(web service)擷取簽名欄位名稱：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立簽名用戶端

   * 使用其 `SignatureServiceClient` 預設建構函式建立物件。
   * 使用建 `SignatureServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `SignatureServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含簽名欄位的PDF檔案

   * 使用其 `BLOB` 建構函式建立物件。 此物 `BLOB` 件用於儲存包含簽名欄位的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為對 `BLOB` 像的欄位分配位元組 `MTOM` 陣列內容來填充對象。

1. 擷取簽名欄位名稱

   * 叫用物件的方法並傳 `SignatureServiceClient` 遞包含簽名欄 `getSignatureFieldList` 位之PDF `BLOB` 檔案的物件，以擷取簽名欄位名稱。 此方法會傳回 `MyArrayOfPDFSignatureField` 每個元素都包含物件的集合 `PDFSignatureField` 物件。
   * 重複物件以 `MyArrayOfPDFSignatureField` 判斷是否有簽名欄位名稱。 對於PDF檔案中的每個簽名欄位，您可以取得 `PDFSignatureField` 物件。 若要取得簽名欄位的名稱，請叫 `PDFSignatureField` 用物件的方 `getName` 法。 此方法傳回指定簽名欄位名稱的字串值。

**另請參閱**

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改簽名欄位 {#modifying-signature-fields}

您可以使用Java API和web service API修改PDF檔案中的簽名欄位。 修改簽名欄位涉及操作其簽名欄位鎖定字典值或種子值字典值。

字 *段鎖定字典* ，指定簽名欄位簽名時鎖定的欄位清單。 鎖定的欄位可防止使用者變更欄位。 種 *子值字典* ，包含在套用簽名時使用的約束資訊。 例如，您可以變更權限，以控制發生動作，而不會使簽名無效。

修改現有的簽名欄位，您就可以變更PDF檔案，以反映不斷變更的業務需求。 例如，新業務要求可能要求在簽署檔案後鎖定所有檔案欄位。

本節說明如何通過修改欄位鎖定字典和種子值字典值來修改簽名欄位。 對簽名欄位鎖定字典所做的變更，會在簽名欄位時鎖定PDF檔案中的所有欄位。 對種子值字典所做的更改禁止對文檔進行特定類型的更改。

>[!NOTE]
>
>如需「簽名服務」和修改簽名欄位的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要修改PDF文檔中的簽名欄位，請執行以下任務：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含要修改之簽名欄位的PDF檔案。
1. 設定字典值。
1. 修改簽名欄位。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含LiveCycle Java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得包含要修改之簽名欄位的PDF檔案**

擷取包含要修改之簽名欄位的PDF檔案。

**設定字典值**

要修改簽名欄位，請為其欄位鎖定字典或種子值字典指定值。 指定簽名欄位鎖定字典值涉及指定簽名欄位時鎖定的PDF文檔欄位。 （本節討論如何鎖定所有欄位。）

可以設定以下種子值字典值：

* **修訂檢查**:指定在將簽名應用到簽名欄位時是否執行撤銷檢查。
* **憑證選項**:為證書種子值字典指定值。 在指定憑證選項之前，建議您熟悉憑證種子值字典。 (請參閱 [PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。)
* **摘要選項**:指派用於簽署的摘要演算法。 有效值為SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **篩選**:指定與簽名欄位一起使用的篩選器。 例如，您可以使用Adobe.PPKLite篩選器。 (請參閱 [PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。)
* **標籤選項**:指定與此簽名欄位關聯的標籤值。 值1表示簽署者只能使用指定的值來輸入項目。 值0表示允許其他值。 以下是位元位置：

   * **** 1（篩選）:用於簽署簽名欄位的簽名處理程式
   * **** 2（子篩選）:一組名稱，指出在簽署時要使用的可接受編碼
   * **3(V)**:用於簽署簽名欄位之簽名處理常式的最低必要版本號碼
   * **** 4（理由）:一系列字串，可指定簽署檔案的可能原因
   * **** 5(PDFegalWarnings):指定可能的合法證明的字串陣列

* **法律證明**:當檔案獲得認證時，會自動掃描特定類型的內容，這些內容可能會使檔案的可見內容模糊或產生誤導。 例如，註解可以遮蔽對瞭解認證內容很重要的文字。 掃描過程生成指示存在此類內容的警告。 此外，也會針對可能產生警告的內容提供其他說明。
* **權限**:指定可在PDF檔案上使用而不會使簽名無效的權限。
* **原因**:指定必須簽署此檔案的原因。
* **時間戳**:指定時間戳記選項。 例如，您可以設定所使用之時間戳記伺服器的URL。
* **版本**:指定用於簽署簽名欄位的簽名處理程式的最小版本號。

**修改簽名欄位**

在您建立簽名服務用戶端後，請擷取包含要修改之簽名欄位的PDF檔案，並設定字典值，您可以指示簽名服務修改簽名欄位。 然後，簽名服務會傳回包含已修改簽名欄位的PDF檔案。 原始PDF檔案不受影響。

**將PDF檔案儲存為PDF檔案**

將包含已修改簽名欄位的PDF檔案儲存為PDF檔案，讓使用者可以在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[簽章服務API快速入門](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API修改簽名欄位 {#modify-signature-fields-using-the-java-api}

使用簽名API(Java)修改簽名欄位：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `SignatureServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得包含要修改之簽名欄位的PDF檔案

   * 建立一 `java.io.FileInputStream` 個對象，該對象表示包含要修改的簽名欄位的PDF文檔，方法是使用其建構子並傳遞一個字串值，該字串值指定PDF文檔的位置。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 設定字典值

   * 使用其 `PDFSignatureFieldProperties` 建構函式建立物件。 對象 `PDFSignatureFieldProperties` 儲存簽名欄位鎖定字典和種子值字典資訊。
   * 使用其 `PDFSeedValueOptionSpec` 建構函式建立物件。 此物件可讓您設定種子值字典值。
   * 叫用物件的方法並傳遞列舉值， `PDFSeedValueOptionSpec` 以禁止變更 `setMdpValue` PDF `MDPPermissions.NoChanges` 檔案。
   * 使用其 `FieldMDPOptionSpec` 建構函式建立物件。 此物件可讓您設定簽名欄位鎖定字典值。
   * 叫用物件的方法並傳遞列舉值，以鎖 `FieldMDPOptionSpec` 定PDF文 `setMdpValue` 件中的所 `FieldMDPAction.ALL` 有欄位。
   * 調用物件的方法並傳遞物件， `PDFSignatureFieldProperties` 以設定種 `setSeedValue` 子值字典 `PDFSeedValueOptionSpec` 資訊。
   * 調用物件的方法並傳遞物件，以設 `PDFSignatureFieldProperties`定簽名欄位鎖 `setFieldMDP` 定字典 `FieldMDPOptionSpec` 資訊。
   >[!NOTE]
   >
   >要查看您可以設定的所有種子值字典值，請查看類 `PDFSeedValueOptionSpec` 參考。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

1. 修改簽名欄位

   調用物件的方法並傳 `SignatureServiceClient` 遞下列值， `modifySignatureField` 以修改簽名欄位：

   * 儲存 `com.adobe.idp.Document` 包含要修改之簽名欄位之PDF檔案的物件
   * 指定簽名欄位名稱的字串值
   * 存 `PDFSignatureFieldProperties` 儲簽名欄位鎖定字典和種子值字典資訊的對象
   此方 `modifySignatureField` 法會傳回 `com.adobe.idp.Document` 儲存包含已修改簽名欄位之PDF檔案的物件。

1. 將PDF檔案儲存為PDF檔案

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容 `com.adobe.idp.Document` 複製至檔案。 請確定您使用 `com.adobe.idp.Document` 方法傳回的 `modifySignatureField` 物件。

### 使用web service API修改簽名欄位 {#modify-signature-fields-using-the-web-service-api}

使用簽名API(web service)修改簽名欄位：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立簽名用戶端

   * 使用其 `SignatureServiceClient` 預設建構函式建立物件。
   * 使用建 `SignatureServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `SignatureServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要修改之簽名欄位的PDF檔案

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存包含要修改的簽名欄位的PDF文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 對象的屬性指 `MTOM` 定位元組陣列的內容來填充對象。

1. 設定字典值

   * 使用其 `PDFSignatureFieldProperties` 建構函式建立物件。 該對象儲存簽名欄位鎖定字典和種子值字典資訊。
   * 使用其 `PDFSeedValueOptionSpec` 建構函式建立物件。 此物件可讓您設定種子值字典值。
   * 不允許將列舉值指派給物件的資 `MDPPermissions.NoChanges` 料成員，以 `PDFSeedValueOptionSpec` 變更PDF `mdpValue` 檔案。
   * 使用其 `FieldMDPOptionSpec` 建構函式建立物件。 此物件可讓您設定簽名欄位鎖定字典值。
   * 將列舉值指派給物件的資料成員，以 `FieldMDPAction.ALL` 鎖定PDF檔案 `FieldMDPOptionSpec` 中的所 `mdpValue` 有欄位。
   * 將物件指派給物件的資料成 `PDFSeedValueOptionSpec` 員，以設定 `PDFSignatureFieldProperties` 種子值字 `seedValue` 典資訊。
   * 將物件指派給物件的資料成員，以設 `FieldMDPOptionSpec` 定簽名欄位鎖 `PDFSignatureFieldProperties` 定字典 `fieldMDP` 資訊。
   >[!NOTE]
   >
   >要查看您可以設定的所有種子值字典值，請查看類 `PDFSeedValueOptionSpec` 參考。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 修改簽名欄位

   調用物件的方法並傳 `SignatureServiceClient` 遞下列值， `modifySignatureField` 以修改簽名欄位：

   * 儲存 `BLOB` 包含要修改之簽名欄位之PDF檔案的物件
   * 指定簽名欄位名稱的字串值
   * 存 `PDFSignatureFieldProperties` 儲簽名欄位鎖定字典和種子值字典資訊的對象
   此方 `modifySignatureField` 法會傳回 `BLOB` 儲存包含已修改簽名欄位之PDF檔案的物件。

1. 將PDF檔案儲存為PDF檔案

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示將包含簽名欄位的PDF文檔的檔案位置，以及開啟檔案的模式。
   * 建立一個位元組陣列，該陣列儲存方 `BLOB` 法返回的對 `addSignatureField` 像內容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署PDF檔案 {#digitally-signing-pdf-documents}

數位簽章可套用至PDF檔案，以提供更高的安全性。 數位簽章（如手寫簽章）提供簽署者識別自己並對檔案進行陳述的方式。 以數位方式簽署檔案的技術有助於確保簽署者和收件者都清楚已簽署的內容，並確信檔案自簽署後未變更。

PDF檔案是透過公開金鑰技術簽署。 簽章者有兩個密鑰：公鑰和私鑰。 私密金鑰會儲存在使用者的憑證中，當簽署時，該憑證必須可供使用。 公開金鑰會儲存在使用者的憑證中，而收件者必須能使用此憑證來驗證簽名。 有關已撤銷證書的資訊可在證書撤銷清單(CRL)和由證書頒發機構(CA)分發的線上證書狀態協定(OCSP)響應中找到。 簽署時間可從稱為時間戳記授權機構的受信任來源取得。

>[!NOTE]
>
>您必須先確定將憑證新增至AEM Forms，才能數位簽署PDF檔案。 憑證是使用管理控制台或使用信任管理器API以程式設計方式新增。 (請參 [閱使用Trust Manager API匯入認證](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。)

您可以以程式設計方式數位簽署PDF檔案。 在數位簽署PDF檔案時，您必須參考AEM Forms中的安全憑證。 憑證是用於簽署的私密金鑰。

簽署PDF檔案時，簽名服務會執行下列步驟：

1. 簽名服務通過傳遞請求中指定的別名從Truststore檢索憑據。
1. Truststore會搜尋指定的憑證。
1. 憑證會傳回給簽章服務，並用來簽署檔案。 此憑證也會根據別名快取，以供日後請求使用。

如需有關處理安全性憑證的詳細資訊，請參 *閱應用程式伺服器的安裝與部署AEM Forms* 指南。

>[!NOTE]
>
>簽署和認證檔案之間有差異。 (請參閱 [認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)。)

>[!NOTE]
>
>並非所有PDF檔案都支援簽署。 如需有關「簽名」服務和數位簽署檔案的詳細資訊，請參閱「AEM [表格的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>簽章服務不支援將內嵌PDF資料的XDP檔案輸入至作業，例如認證檔案。 此動作會導致簽章服務擲出 `PDFOperationException`。 若要解決此問題，請使用PDF公用程式服務將XDP檔案轉換為PDF檔案，然後將轉換的PDF檔案傳遞至簽名服務作業。 (請參 [閱使用PDF公用程式](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)。)

**nCypher nShield HSM憑證**

當使用nCypher nShield HSM憑證來簽署或認證PDF檔案時，必須重新啟動AEM Forms所部署的J2EE應用程式伺服器，才能使用新憑證。 不過，您可以設定設定值，讓簽署或認證作業運作正常，而不需重新啟動J2EE應用程式伺服器。

您可以在cknfastrc檔案中新增下列組態值，該檔案位於/opt/nfast/cknfastrc(或c:\nfast\cknfastrc):

```as3
 CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此配置值添加到cknfastrc檔案後，無需重新啟動J2EE應用程式伺服器即可使用新憑據。

**不信任簽名**

在認證和簽署相同PDF檔案時，如果不信任認證簽名，在Acrobat或Adobe Reader中開啟PDF檔案時，第一個簽名會出現黃色三角形。 為避免這種情況，認證簽名必須受到信任。

**簽署以XFA為基礎的表格檔案**

如果您嘗試使用簽名服務API簽署以XFA為基礎的表單，Acrobat中的資料可 `View` 能 `Signed` 會 `Version` 遺失。 例如，請考慮下列工作流程：

* 使用Designer建立的XDP檔案，可以合併包含簽名欄位的表單設計和包含表單資料的XML資料。 您可使用Forms服務產生互動式PDF檔案。
* 您使用簽名服務API簽署PDF檔案。

### 步驟摘要 {#summary_of_steps-3}

若要數位簽署PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名服務用戶端。
1. 取得要簽署的PDF檔案。
1. 簽署PDF檔案。
1. 將簽署的PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得PDF檔案以簽署**

若要簽署PDF檔案，您必須取得包含簽名欄位的PDF檔案。 如果PDF檔案不包含簽名欄位，則無法簽署。 可使用設計工具或程式設計方式新增簽名欄位。

**簽署PDF檔案**

在簽署PDF檔案時，您可以設定簽章服務使用的執行時期選項。 您可以設定下列選項：

* 外觀選項
* 撤銷檢查
* 時間戳記值

通過使用對象來設定外觀 `PDFSignatureAppearanceOptionSpec` 選項。 例如，您可以叫用物件的方法並傳遞，以 `PDFSignatureAppearanceOptionSpec` 顯示簽 `setShowDate` 名中的日期 `true`。

您也可以指定是否執行撤銷檢查，以判斷用於數位簽署PDF檔案的憑證是否已被撤銷。 要執行撤銷檢查，您可以指定以下值之一：

* **NoCheck**:請勿執行撤銷檢查。
* **BestEffort**:請務必檢查是否撤銷鏈中的所有證書。 如果檢查中發生任何問題，則假定撤銷有效。 如果發生任何失敗，請假定憑證未被撤銷。
* **** CheckIfAvailable:如果有撤銷資訊，請檢查是否撤銷鏈中的所有憑證。 如果檢查中發生任何問題，則假定撤銷無效。 如果發生任何故障，請假定憑證已撤銷且無效。 （這是預設值。）
* **AlwaysCheck**:檢查是否撤銷鏈中的所有證書。 如果撤銷資訊未出現在任何憑證中，則假定撤銷無效。

要對證書執行撤銷檢查，可以使用對象指定證書撤銷清單(CRL)伺服器的URL `CRLOptionSpec` 。 但是，如果您要執行撤銷檢查，而您未指定CRL伺服器的URL，則簽名服務會從憑證取得URL。

執行撤銷檢查時，您可以使用線上證書狀態協定(OCSP)伺服器，而不是使用CRL伺服器。 通常在使用OCSP伺服器而非CRL伺服器時，會更快地執行撤銷檢查。 (請參閱https://tools.ietf.org/html/rfc2560上的「線上認證狀態通 [訊協定](https://tools.ietf.org/html/rfc2560)」)。

您可以使用Adobe應用程式與服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe Applications and services中設定，則會檢查OCSP伺服器，接著檢查CRL伺服器。 （請參閱AAC說明中的「使用信任商店管理憑證和認證」）。

如果您指定不執行撤銷檢查，則簽章服務不會檢查用來簽署或認證檔案的憑證是否已被撤銷。 即，忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>雖然CRL或OCSP伺服器可在憑證中指定，但您仍可使用和物件來覆寫憑證中指定 `CRLOptionSpec` 的 `OCSPOptionSpec` URL。 例如，若要覆寫CRL伺服器，您可以叫用 `CRLOptionSpec` 物件的方 `setLocalURI` 法。

時間戳記是指追蹤已簽署或已認證檔案修改時間的程式。 簽署檔案後，即使檔案擁有者也不應修改檔案。 時間戳記有助於強制簽署或認證檔案的有效性。 可以使用對象設定時間戳 `TSPOptionSpec` 選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和web服務中，通過各個部分和相應的快速啟動，使用撤銷檢查。 由於未指定CRL或OCSP伺服器資訊，因此伺服器資訊是從用於數位簽署PDF檔案的憑證中取得。

若要成功簽署PDF檔案，您可以指定包含數位簽章的簽名欄位的完全限定名稱，例如 `form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，也可以使用簽名欄位的部分名稱： `SignatureField3[3]`。

您也必須參考安全憑證才能數位簽署PDF檔案。 要引用安全憑據，請指定別名。 別名是對PKCS#12檔案（副檔名為。pfx）或硬體安全模組(HSM)中實際憑據的引用。 如需安全性憑證的詳細資訊，請參 *閱應用程式伺服器的安裝與部署AEM Forms* 指南。

**儲存已簽署的PDF檔案**

在簽名服務數位簽署PDF檔案後，您可以將它儲存為PDF檔案，讓使用者在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用web service API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

[檢索簽名欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API數位簽署PDF檔案 {#digitally-sign-pdf-documents-using-the-java-api}

使用簽名API(Java)數位簽署PDF檔案：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `SignatureServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得PDF檔案以簽署

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的物件以進行數位簽署。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 簽署PDF檔案

   叫用物件的方法並傳 `SignatureServiceClient` 遞下列值， `sign` 以簽署PDF檔案：

   * 代 `com.adobe.idp.Document` 表要簽署的PDF檔案的物件。
   * 一個字串值，代表將包含數位簽名之簽名欄位的名稱。
   * 代 `Credential` 表用於數位簽署PDF檔案的憑證的物件。 調用對 `Credential` 像的靜態方 `Credential``getInstance` 法並傳遞一個字串值，該字串值指定與安全憑據對應的別名值，以建立對象。
   * 指 `HashAlgorithm` 定靜態資料成員的物件，代表用於摘要PDF檔案的雜湊演算法。 例如，您可以指 `HashAlgorithm.SHA1` 定使用SHA1演算法。
   * 一個字串值，代表PDF檔案數位簽章的原因。
   * 代表簽署者聯絡資訊的字串值。
   * 控 `PDFSignatureAppearanceOptions` 制數位簽名外觀的物件。 例如，您可使用此物件將自訂標誌新增至數位簽名。
   * 指定 `java.lang.Boolean` 是否對簽章者的憑證執行撤銷檢查的物件。
   * 存 `OCSPOptionSpec` 儲聯機證書狀態協定(OCSP)支援首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。
   * 儲存 `CRLPreferences` 證書撤銷清單(CRL)首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。
   * 儲存 `TSPPreferences` 時間戳記提供者(TSP)支援偏好設定的物件。 此參數為可選參數，可以是 `null`。 如需詳細資訊，請參 [閱「AEM Forms API參考」](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   此方 `sign` 法會傳回 `com.adobe.idp.Document` 代表已簽署PDF檔案的物件。

1. 儲存已簽署的PDF檔案

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法並傳遞 `java.io.File`以將物件的內容 `Document` 複製至檔案。 請確定您使用 `com.adobe.idp.Document` 方法傳回的物 `sign` 件。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速入門（SOAP模式）:使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API數位簽署PDF檔案 {#digitally-signing-pdf-documents-using-the-web-service-api}

若要使用簽名API(web service)數位簽署PDF檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立簽名用戶端

   * 使用其 `SignatureServiceClient` 預設建構函式建立物件。
   * 使用建 `SignatureServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `SignatureServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得PDF檔案以簽署

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用於儲存已簽署的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示要簽名的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 對象的屬性指 `MTOM` 定位元組陣列的內容來填充對象。

1. 簽署PDF檔案

   叫用物件的方法並傳 `SignatureServiceClient` 遞下列值， `sign` 以簽署PDF檔案：

   * 代 `BLOB` 表要簽署的PDF檔案的物件。
   * 一個字串值，代表將包含數位簽名之簽名欄位的名稱。
   * 代 `Credential` 表用於數位簽署PDF檔案的憑證的物件。 使用 `Credential` 其建構函式建立物件，並指定別名，方法是為物件的屬 `Credential` 性指定 `alias` 值。
   * 指 `HashAlgorithm` 定靜態資料成員的物件，代表用於摘要PDF檔案的雜湊演算法。 例如，您可以指 `HashAlgorithm.SHA1` 定使用SHA1演算法。
   * 一個布爾值，它指定是否使用散列算法。
   * 一個字串值，代表PDF檔案數位簽章的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * 控 `PDFSignatureAppearanceOptions` 制數位簽名外觀的物件。 例如，您可使用此物件將自訂標誌新增至數位簽名。
   * 指定 `System.Boolean` 是否對簽章者的憑證執行撤銷檢查的物件。 如果完成此撤銷檢查，則會將其嵌入簽名中。 預設值為 `false`。
   * 存 `OCSPOptionSpec` 儲聯機證書狀態協定(OCSP)支援首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。 如需此物件的詳細資訊，請參 [閱「AEM Forms API參考」](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 儲存 `CRLPreferences` 證書撤銷清單(CRL)首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。
   * 儲存 `TSPPreferences` 時間戳記提供者(TSP)支援偏好設定的物件。 此參數為可選參數，可以是 `null`。
   此方 `sign` 法會傳回 `BLOB` 代表已簽署PDF檔案的物件。

1. 儲存已簽署的PDF檔案

   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表已簽署PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，該陣列儲存方 `BLOB` 法返回的對象的內 `sign` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署互動式表單 {#digitally-signing-interactive-forms}

您可以簽署Forms服務所建立的互動式表單。 例如，請考慮下列工作流程：

* 您可以合併使用Designer建立的以XFA為基礎的PDF表單，以及使用Forms服務在XML檔案中的表單資料。 Forms伺服器會轉譯互動式表單。
* 您可使用簽名服務API簽署互動式表單。

結果是以數位簽章的互動式PDF表單。 在簽署以XFA表單為基礎的PDF表單時，請確定您將PDF檔案儲存為Adobe Static PDF表單。 如果您嘗試簽署儲存為Adobe動態PDF表單的PDF表單，就會發生例外。 由於您正在簽署從Forms服務傳回的表單，請確定表單包含簽名欄位。

>[!NOTE]
>
>您必須先確定將憑證新增至AEM Forms，才能數位簽署互動式表單。 憑證是使用管理控制台或使用信任管理器API以程式設計方式新增。 (請參 [閱使用Trust Manager API匯入認證](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。)

使用Forms Service API時，請將執 `GenerateServerAppearance` 行時間選項設為 `true`。 此執行時期選項可確保在Acrobat或Adobe Reader中開啟時，伺服器上產生的表格外觀仍然有效。 建議您在使用Forms API產生要簽署的互動式表單時，設定這個執行時期選項。

>[!NOTE]
>
>在閱讀數位簽署互動式表單之前，建議您熟悉簽署PDF檔案。 (請參 [閱數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)

### 步驟摘要 {#summary_of_steps-4}

若要數位簽署Forms服務傳回的互動式表單，請執行下列工作：

1. 包含專案檔案。
1. 建立表單和簽名用戶端。
1. 使用Forms服務取得互動式表單。
1. 簽署互動式表單。
1. 將簽署的PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立表單和簽名用戶端**

由於此工作流程會同時叫用Forms和Signature services，因此請同時建立Forms服務用戶端和Signature服務用戶端。

**使用Forms服務取得互動式表單**

您可以使用Forms服務取得要簽署的互動式PDF表單。 從AEM Forms開始，您可以將物件傳 `com.adobe.idp.Document` 遞至包含要演算的表單的Forms服務。 此方法的名稱為 `renderPDFForm2`。 此方法會傳 `com.adobe.idp.Document` 回包含要簽署之表單的物件。 您可以將此例 `com.adobe.idp.Document` 項傳遞至簽名服務。

同樣地，如果您使用web services，則可將Forms服 `BLOB` 務傳回的例項傳遞至Signature服務。

>[!NOTE]
>
>與「數位簽署互動式表單」區段關聯的快速入門會叫用 `renderPDFForm2` 方法。

**簽署互動式表單**

在簽署PDF檔案時，您可以設定簽章服務使用的執行時期選項。 您可以設定下列選項：

* 外觀選項
* 撤銷檢查
* 時間戳記值

通過使用對象來設定外觀 `PDFSignatureAppearanceOptionSpec` 選項。 例如，您可以叫用物件的方法並傳遞，以 `PDFSignatureAppearanceOptionSpec` 顯示簽 `setShowDate` 名中的日期 `true`。

**儲存已簽署的PDF檔案**

在簽名服務數位簽署PDF檔案後，您就可將它儲存為PDF檔案。 PDF檔案可在Acrobat或Adobe Reader中開啟。

**另請參閱**

[使用Java API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用web service API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[轉換互動式PDF表單](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API數位簽署互動式表單 {#digitally-sign-an-interactive-form-using-the-java-api}

使用表單與簽名API(Java)數位簽署互動式表單：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar和adobe-forms-client.jar。

1. 建立表單和簽名用戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `SignatureServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。
   * 使用其 `FormsServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 使用Forms服務取得互動式表單

   * 使用 `java.io.FileInputStream` 其建構函式建立代表PDF檔案的物件，以傳遞至Forms服務。 傳遞指定PDF檔案位置的字串值。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。
   * 建立一 `java.io.FileInputStream` 個對象，該對象表示包含表單資料的XML文檔，並使用其建構子傳遞給Forms服務。 傳遞指定XML檔案位置的字串值。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。
   * 建立 `PDFFormRenderSpec` 用於設定執行時期選項的物件。 叫用 `PDFFormRenderSpec` 物件的方 `setGenerateServerAppearance` 法並傳遞 `true`。
   * 叫用物 `FormsServiceClient` 件的方 `renderPDFForm2` 法並傳遞下列值：

      * 包含 `com.adobe.idp.Document` 要渲染的PDF表單的對象。
      * 包 `com.adobe.idp.Document` 含要與表單合併的資料的對象。
      * 存 `PDFFormRenderSpec` 儲運行時選項的對象。
      * 包 `URLSpec` 含Forms服務所需URI值的對象。 您可以指 `null` 定此參數值。
      * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
      該方 `renderPDFForm2` 法返回包 `FormsResult` 含表單資料流的對象

   * 調用物件的方法，以 `FormsResult` 擷取PDF表 `getOutputContent` 格。 此方法返回 `com.adobe.idp.Document` 表示互動式表單的對象。


1. 簽署互動式表單

   叫用物件的方法並傳 `SignatureServiceClient` 遞下列值， `sign` 以簽署PDF檔案：

   * 代 `com.adobe.idp.Document` 表要簽署的PDF檔案的物件。 請確定此物件是從Forms `com.adobe.idp.Document` 服務取得的物件。
   * 一個字串值，代表已簽署的簽名欄位名稱。
   * 代 `Credential` 表用於數位簽署PDF檔案的憑證的物件。 調用 `Credential` 物件的靜態方 `Credential` 法來建立物 `getInstance` 件。 傳遞一個字串值，該字串值指定與安全憑據對應的別名值。
   * 指 `HashAlgorithm` 定靜態資料成員的物件，代表用於摘要PDF檔案的雜湊演算法。 例如，您可以指 `HashAlgorithm.SHA1` 定使用SHA1演算法。
   * 一個字串值，代表PDF檔案數位簽章的原因。
   * 代表簽署者聯絡資訊的字串值。
   * 控 `PDFSignatureAppearanceOptions` 制數位簽名外觀的物件。 例如，您可使用此物件將自訂標誌新增至數位簽名。
   * 指定 `java.lang.Boolean` 是否對簽章者的憑證執行撤銷檢查的物件。
   * 存 `OCSPPreferences` 儲聯機證書狀態協定(OCSP)支援首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。
   * 儲存 `CRLPreferences` 證書撤銷清單(CRL)首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。
   * 儲存 `TSPPreferences` 時間戳記提供者(TSP)支援偏好設定的物件。 此參數為可選參數，可以是 `null`。
   此方 `sign` 法會傳回 `com.adobe.idp.Document` 代表已簽署PDF檔案的物件。

1. 儲存已簽署的PDF檔案

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法並傳遞 `java.io.File`以將物件的內容 `Document` 複製至檔案。 請確定您使用 `com.adobe.idp.Document` 方法傳回的 `sign` 物件。

**另請參閱**

[數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速入門（SOAP模式）:使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API數位簽署互動式表單 {#digitally-sign-an-interactive-form-using-the-web-service-api}

使用表單與簽名API(web service)數位簽署互動式表單：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 由於此用戶端應用程式會叫用兩個AEM Forms服務，因此請建立兩個服務參考。 對與簽名服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   對與Forms服務關聯的服務引用使用以下WSDL定義： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   由於兩 `BLOB` 個服務引用都使用資料類型，因此在使用資料類 `BLOB` 型時完全限定該資料類型。 在對應的Web服務快速啟動中，所有實例 `BLOB` 都完全限定。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立表單和簽名用戶端

   * 使用其 `SignatureServiceClient` 預設建構函式建立物件。
   * 使用建 `SignatureServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `SignatureServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。
   >[!NOTE]
   >
   >對Forms服務客戶端重複這些步驟。

1. 使用Forms服務取得互動式表單

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用於儲存已簽署的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示要簽名的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 對象的屬性指 `MTOM` 定位元組陣列的內容來填充對象。
   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用來儲存表單資料。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示包含表單資料的XML檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 對象的屬性指 `MTOM` 定位元組陣列的內容來填充對象。
   * 建立 `PDFFormRenderSpec` 用於設定執行時期選項的物件。 將值指 `true` 派至物 `PDFFormRenderSpec` 件的欄 `generateServerAppearance` 位。
   * 叫用物 `FormsServiceClient` 件的方 `renderPDFForm2` 法並傳遞下列值：

      * 包含 `BLOB` 要渲染的PDF表單的對象。
      * 包 `BLOB` 含要與表單合併的資料的對象。
      * 存 `PDFFormRenderSpec` 儲運行時選項的對象。
      * 包 `URLSpec` 含Forms服務所需URI值的對象。 您可以指 `null` 定此參數值。
      * 儲存 `java.util.HashMap` 檔案附件的對象。 這是可選參數，您可以指 `null` 定是否不想將檔案附加到表單。
      * 用於儲存表單中頁數的長輸出參數。
      * 用於地區值的字串輸出參數。
      * 用 `FormResult` 於儲存互動式表單的輸出參數的值。
   * 叫用物件欄位，以重 `FormsResult` 新建立PDF `outputContent` 表格。 此欄位會儲存 `BLOB` 代表互動式表單的物件。


1. 簽署互動式表單

   叫用物件的方法並傳 `SignatureServiceClient` 遞下列值， `sign` 以簽署PDF檔案：

   * 代 `BLOB` 表要簽署的PDF檔案的物件。 使用Forms `BLOB` 服務傳回的例項。
   * 一個字串值，代表已簽署的簽名欄位名稱。
   * 代 `Credential` 表用於數位簽署PDF檔案的憑證的物件。 使用 `Credential` 其建構函式建立物件，並指定別名，方法是為物件的屬 `Credential` 性指定 `alias` 值。
   * 指 `HashAlgorithm` 定靜態資料成員的物件，代表用於摘要PDF檔案的雜湊演算法。 例如，您可以指 `HashAlgorithm.SHA1` 定使用SHA1演算法。
   * 一個布爾值，它指定是否使用散列算法。
   * 一個字串值，代表PDF檔案數位簽章的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * 控 `PDFSignatureAppearanceOptions` 制數位簽名外觀的物件。 例如，您可使用此物件將自訂標誌新增至數位簽名。
   * 指定 `System.Boolean` 是否對簽章者的憑證執行撤銷檢查的物件。 如果完成此撤銷檢查，則會將其嵌入簽名中。 預設值為 `false`。
   * 存 `OCSPPreferences` 儲聯機證書狀態協定(OCSP)支援首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。 如需此物件的詳細資訊，請參 [閱「AEM Forms API參考」](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 儲存 `CRLPreferences` 證書撤銷清單(CRL)首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。
   * 儲存 `TSPPreferences` 時間戳記提供者(TSP)支援偏好設定的物件。 此參數為可選參數，可以是 `null`。
   此方 `sign` 法會傳回 `BLOB` 代表已簽署PDF檔案的物件。

1. 儲存已簽署的PDF檔案

   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表已簽署PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，該陣列儲存方 `BLOB` 法返回的對象的內 `sign` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 認證PDF檔案 {#certifying-pdf-documents}

您可以使用稱為認證簽名的特定簽名類型來認證PDF檔案，以保全PDF檔案。 認證簽名與數位簽名的區別在於：

* 它必須是套用至PDF檔案的第一個簽名；也就是說，在套用認證簽名時，檔案中的任何其他簽名欄位都必須未簽署。 在PDF檔案中僅允許使用一個認證簽名。 如果您想要簽署和認證PDF檔案，您必須先取得認證，才能簽署。 在認證PDF檔案後，您可以數位簽署其他簽名欄位。
* 文檔的作者或發起者可以指定文檔可以通過某些方式進行修改，而不使經認證的簽名失效。 例如，檔案可能允許填寫表格或加上註解。 如果作者指定不允許進行某些修改，Acrobat會限制使用者以此方式修改檔案。 如果進行此類修改，例如使用其他應用程式，認證的簽名無效，當使用者開啟檔案時，Acrobat會發出警告。 （使用未認證的簽名時，不會防止修改，而一般的編輯作業也不會使原始簽名無效。）
* 在簽署時，會掃描檔案，以找出可能導致檔案內容模糊或誤導的特定內容類型。 例如，註解可能會遮蔽頁面上對瞭解所認證內容而言很重要的文字。 可以提供有關此類內容的說明（法律證明）。

您可以使用簽名服務Java API或簽名網站服務API，以程式設計方式認證PDF檔案。 認證PDF檔案時，您必須參考憑證服務中的安全憑證。 如需安全性憑證的詳細資訊，請參 *閱應用程式伺服器的安裝與部署AEM Forms* 指南。

>[!NOTE]
>
>當認證並簽署相同的PDF檔案時，如果不信任認證簽名，當您在Acrobat或Adobe Reader中開啟PDF檔案時，第一個簽名旁會出現黃色三角形。 必須信任認證簽名才能避免這種情況。

>[!NOTE]
>
>當使用nCypher nShield HSM憑證來簽署或認證PDF檔案時，必須重新啟動部署AEM Forms的J2EE應用程式伺服器，才能使用新憑證。 不過，您可以設定設定值，讓簽署或認證作業運作正常，而不需重新啟動J2EE應用程式伺服器。

您可以在cknfastrc檔案中新增下列組態值，該檔案位於/opt/nfast/cknfastrc(或c:\nfast\cknfastrc):

```as3
             CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此配置值添加到cknfastrc檔案後，無需重新啟動J2EE應用程式伺服器即可使用新憑據。

>[!NOTE]
>
>如需簽章服務與認證檔案的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

若要認證PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得PDF檔案以進行認證。
1. 認證PDF檔案。
1. 將認證的PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

您必須先建立「簽名」用戶端，才能以程式設計方式執行「簽名」操作。

**取得PDF檔案以取得認證**

若要認證PDF檔案，您必須取得包含簽名欄位的PDF檔案。 如果PDF檔案不包含簽名欄位，則無法取得認證。 可使用設計工具或程式設計方式新增簽名欄位。 如需以程式設計方式新增簽名欄位的詳細資訊，請參 [閱新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)。

**認證PDF檔案**

若要成功認證PDF檔案，您需要下列由簽章服務用來認證PDF檔案的輸入值：

* **PDF檔案**:包含簽名欄位的PDF文檔，該欄位是包含已認證簽名的圖形表示的表單欄位。 PDF檔案必須先包含簽名欄位，才能取得認證。 可使用設計工具或程式設計方式新增簽名欄位。 (請參 [閱新增簽名欄](digitally-signing-certifying-documents.md#adding-signature-fields)。)
* **簽名欄位名稱**:經認證的簽名欄位的全限定名稱。 以下是一個示例： `form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，也可以使用簽名欄位的部分名稱： `SignatureField3[3]`。 如果為欄位名稱傳遞空值，則會動態建立並認證不可見的簽名欄位。
* **安全憑證**:用於認證PDF檔案的憑證。 此安全憑證包含密碼和別名，這些密碼和別名必須與位於憑證服務中的憑證中顯示的別名相符。 別名是對PKCS#12檔案（副檔名為。pfx）或硬體安全模組(HSM)中實際憑據的引用。
* **雜湊算法**:用於摘要PDF檔案的雜湊演算法。
* **簽署原因**:顯示在Acrobat或Adobe Reader中的值，讓其他使用者知道PDF檔案獲得認證的原因。
* **簽署者的位置**:憑證指定之簽署者的位置。
* **聯絡資訊**:簽署者的聯絡資訊，例如地址和電話號碼。
* **權限資訊**:控制一般使用者可在檔案上執行動作而不導致認證簽名無效的權限。 例如，您可以設定權限，如此對PDF檔案所做的任何變更，都會導致認證的簽名無效。
* **法律解釋**:當檔案獲得認證時，會自動掃描特定類型的內容，這些內容可能會使檔案的內容模糊或產生誤導。 例如，註解可能會遮蔽頁面上對瞭解所認證內容而言很重要的文字。 掃描過程生成關於這些類型內容的警告。 此值提供可能產生警告之內容的額外說明。
* **外觀選項**:控制認證簽名外觀的選項。 例如，認證的簽名可顯示日期資訊。
* **撤銷檢查**:此值指定是否對簽署者的憑證執行撤銷檢查。 預設的設定 `false` 表示不會執行撤銷檢查。
* **OCSP設定**:線上認證狀態通訊協定(OCSP)支援的設定，提供用來認證PDF檔案之憑證狀態的相關資訊。 例如，您可以指定伺服器的URL，以提供您用來登入PDF檔案之憑證的相關資訊。
* **CRL設定**:完成撤銷檢查時，證書撤銷清單(CRL)首選項的設定。 例如，您可以指定一律檢查憑證是否已撤銷。
* **時間戳記**:定義套用至認證簽名之時間戳記資訊的設定。 時間戳表示特定資料在某個時間之前建立。 這項知識有助於在簽署者與驗證者之間建立信任關係。

**將認證的PDF檔案儲存為PDF檔案**

在簽章服務認證PDF檔案後，您可以將它儲存為PDF檔案，讓使用者在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用web service API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API認證PDF檔案 {#certify-pdf-documents-using-the-java-api}

使用簽名API(Java)認證PDF檔案：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `SignatureServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得PDF檔案以取得認證

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的物件以進行認證。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 認證PDF檔案

   叫用物件的方法並傳 `SignatureServiceClient` 遞下列值， `certify` 以認證PDF檔案：

   * 表示 `com.adobe.idp.Document` 要認證的PDF檔案的物件。
   * 一個字串值，它表示將包含簽名的簽名欄位的名稱。
   * 代 `Credential` 表用來認證PDF檔案的憑證的物件。 調用對 `Credential` 像的靜態方 `Credential``getInstance` 法並傳遞一個字串值，該字串值指定與安全憑據對應的別名值，以建立對象。
   * 一 `HashAlgorithm` 個對象，它指定表示用於摘要PDF文檔的散列算法的靜態資料成員。 例如，您可以指 `HashAlgorithm.SHA1` 定使用SHA1演算法。
   * 一個字串值，代表PDF檔案獲得認證的原因。
   * 代表簽署者聯絡資訊的字串值。
   * 一 `MDPPermissions` 個對象，它指定可對PDF文檔執行的使簽名無效的操作。
   * 控 `PDFSignatureAppearanceOptions` 制認證簽名外觀的物件。 如果需要，可通過調用方法（如）修改簽名的外觀 `setShowDate`。
   * 字串值，可說明哪些動作使簽名無效。
   * 指定 `java.lang.Boolean` 是否對簽章者的憑證執行撤銷檢查的物件。 如果完成此撤銷檢查，則會將其嵌入簽名中。 預設值為 `false`。
   * 一 `java.lang.Boolean` 個對象，它指定是否鎖定要認證的簽名欄位。 如果欄位已鎖定，則簽名欄位會標示為唯讀，其屬性無法修改，而且沒有必要權限的任何人也無法清除。 預設值為 `false`。
   * 存 `OCSPPreferences` 儲聯機證書狀態協定(OCSP)支援首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。 如需此物件的詳細資訊，請參 [閱AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 儲存 `CRLPreferences` 證書撤銷清單(CRL)首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。
   * 儲存 `TSPPreferences` 時間戳記提供者(TSP)支援偏好設定的物件。 例如，在建立物件 `TSPPreferences` 後，您可以叫用物件的方法來設定TSP `TSPPreferences` 伺服器的 `setTspServerURL` URL。 此參數為可選參數，可以是 `null`。 如需詳細資訊，請參 [閱「AEM Forms的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。
   此方 `certify` 法會傳回 `com.adobe.idp.Document` 代表已認證PDF檔案的物件。

1. 將認證的PDF檔案儲存為PDF檔案

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容 `com.adobe.idp.Document` 複製至檔案。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速入門（SOAP模式）:使用Java API認證PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API認證PDF檔案 {#certify-pdf-documents-using-the-web-service-api}

使用簽名API(web service)認證PDF檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立簽名用戶端

   * 使用其 `SignatureServiceClient` 預設建構函式建立物件。
   * 使用建 `SignatureServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `SignatureServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得PDF檔案以取得認證

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用來儲存經認證的PDF檔案。
   * 呼叫 `System.IO.FileStream` 其建構函式並傳遞字串值來建立物件，此字串值代表要認證的PDF檔案檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 通過為 `BLOB` 其資料成員分配位元組 `MTOM` 陣列的內容來填充對象。

1. 認證PDF檔案

   叫用物件的方法並傳 `SignatureServiceClient` 遞下列值， `certify` 以認證PDF檔案：

   * 表示 `BLOB` 要認證的PDF檔案的物件。
   * 一個字串值，它表示將包含簽名的簽名欄位的名稱。
   * 代 `Credential` 表用來認證PDF檔案的憑證的物件。 使用 `Credential` 其建構函式建立物件，並指定別名，方法是為物件的屬 `Credential` 性指定 `alias` 值。
   * 一 `HashAlgorithm` 個對象，它指定表示用於摘要PDF文檔的散列算法的靜態資料成員。 例如，您可以指 `HashAlgorithm.SHA1` 定使用SHA1演算法。
   * 一個布爾值，它指定是否使用散列算法。
   * 一個字串值，代表PDF檔案獲得認證的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * 物 `MDPPermissions` 件的靜態資料成員，指定可在PDF檔案上執行使簽名無效的動作。
   * 一個布爾值，它指定是否將傳遞 `MDPPermissions` 的對象用作前一個參數值。
   * 一個字串值，它解釋哪些操作使簽名無效。
   * 控 `PDFSignatureAppearanceOptions` 制認證簽名外觀的物件。 使用其 `PDFSignatureAppearanceOptions` 建構函式建立物件。 您可以通過設定簽名的一個資料成員來修改簽名的外觀。
   * 指定 `System.Boolean` 是否對簽章者的憑證執行撤銷檢查的物件。 如果完成此撤銷檢查，則會將其嵌入簽名中。 預設值為 `false`。
   * 一 `System.Boolean` 個對象，它指定是否鎖定要認證的簽名欄位。 如果欄位已鎖定，則簽名欄位會標示為唯讀，其屬性無法修改，而且沒有必要權限的任何人也無法清除。 預設值為 `false`。
   * 指定 `System.Boolean` 簽名欄位是否被鎖定的對象。 也就是說，如果傳遞 `true` 至上一個參數，則傳遞 `true` 至此參數。
   * 儲 `OCSPPreferences` 存線上認證狀態通訊協定(OCSP)支援偏好設定的物件，提供用來認證PDF檔案之憑證狀態的資訊。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。
   * 儲存 `CRLPreferences` 證書撤銷清單(CRL)首選項的對象。 如果未完成撤銷檢查，則不使用此參數，您可以指定 `null`。
   * 儲存 `TSPPreferences` 時間戳記提供者(TSP)支援偏好設定的物件。 例如，建立物件 `TSPPreferences` 後，您可以設定物件的資料成員，以設 `TSPPreferences` 定TSP的 `tspServerURL` URL。 此參數為可選參數，可以是 `null`。
   此方 `certify` 法會傳回 `BLOB` 代表已認證PDF檔案的物件。

1. 將認證的PDF檔案儲存為PDF檔案

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示將包含經認證的PDF文檔的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，該陣列儲存方 `BLOB` 法返回的對象的內 `certify` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `binaryData` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證數位簽名 {#verifying-digital-signatures}

數位簽章可進行驗證，以確保已簽署的PDF檔案未修改，且數位簽章有效。 在驗證數位簽名時，您可以檢查簽名的狀態和簽名的屬性，例如簽章者的身分。 在信任數位簽名之前，建議您先進行驗證。 在驗證數位簽名時，請參考包含數位簽名的PDF檔案。

假設簽章者的身分不明。 當您在Acrobat中開啟PDF檔案時，會出現警告訊息，指出簽署者的身分不明，如下圖所示。

![vd_vd_verifisig](assets/vd_vd_verifysig.png)

同樣地，當您以程式設計方式驗證數位簽章時，您也可以決定簽署者身分的狀態。 例如，如果您驗證上圖所示檔案中的數位簽名，結果會是簽章者的身分不明。

>[!NOTE]
>
>如需「簽名」服務和驗證數位簽章的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

若要驗證數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含要驗證之簽名的PDF檔案。
1. 設定PKI執行時期選項。
1. 驗證數位簽名。
1. 確定簽名的狀態。
1. 決定簽署者的身分。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

在您以程式設計方式執行簽名服務操作之前，請先建立簽名服務用戶端。

**取得包含簽章的PDF檔案以驗證**

若要驗證用於數位簽署或認證PDF檔案的簽名，請取得包含簽名的PDF檔案。

**設定PKI執行時期選項**

在PDF檔案中驗證簽名時，請設定簽名服務使用的這些PKI執行時期選項：

* 驗證時間
* 撤銷檢查
* 時間戳記值

在設定這些選項時，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），指出使用目前時間。 如需不同時間值的詳細資訊，請參閱 `VerificationTime`[AEM Forms API參考中的列舉值](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

您也可以指定是否在驗證程式中執行撤銷檢查。 例如，您可以執行撤銷檢查，以判斷憑證是否已撤銷。 如需有關撤銷檢查選項的詳細資訊，請參閱 `RevocationCheckStyle`[AEM Forms API參考中的列舉值](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

要對證書執行撤銷檢查，請使用對象指定證書撤銷清單(CRL)伺服器的URL `CRLOptionSpec` 。 但是，如果您未指定CRL伺服器的URL，則簽名服務會從憑證取得URL。

執行撤銷檢查時，您可以使用線上證書狀態協定(OCSP)伺服器，而不是使用CRL伺服器。 通常，與CRL伺服器相比，使用OCSP伺服器時，撤銷檢查的執行速度更快。 (請參閱 [線上憑證狀態通訊協定](https://tools.ietf.org/html/rfc2560))。

您可以使用Adobe應用程式與服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe Applications and services中設定，則會檢查OCSP伺服器，接著檢查CRL伺服器。

如果您未執行撤銷檢查，「簽名服務」不會檢查憑證是否已撤銷。 即，忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用和物件來覆寫憑證中指定 `CRLOptionSpec` 的URL `OCSPOptionSpec` 。 例如，若要覆寫CRL伺服器，您可以叫用 `CRLOptionSpec` 物件的方 `setLocalURI` 法。

時間戳記是追蹤已簽署或已認證檔案修改時間的程式。 簽署檔案後，任何人都無法修改它。 時間戳記有助於強制簽署或認證檔案的有效性。 可以使用對象設定時間戳 `TSPOptionSpec` 選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和web服務快速啟動中，將驗證時間設定為， `VerificationTime.CURRENT_TIME` 將撤銷檢查設定為 `RevocationCheckStyle.BestEffort`。 由於未指定CRL或OCSP伺服器資訊，因此從證書中獲取伺服器資訊。

**驗證數位簽名**

要成功驗證簽名，請指定包含簽名的簽名欄位的完全限定名稱，例如 `form1[0].#subform[1].SignatureField3[3]`。 使用XFA表單欄位時，您也可以使用簽名欄位的部分名稱： `SignatureField3`。

依預設，簽章服務會將檔案在驗證後可簽署的時間限制為65分鐘。 如果使用者嘗試在目前時間驗證簽名，而簽署時間晚於目前時間且在65分鐘內，則簽名服務不會建立驗證錯誤。

>[!NOTE]
>
>如需您在驗證簽名時需要的其他值，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**確定簽名的狀態**

在驗證數位簽名時，您可以檢查簽名的狀態。

**決定簽署者的身分**

您可以決定簽章者的身分，這可以是下列其中一個值：

* **未知**:此簽署者未知，因為無法執行簽署者驗證。
* **受信任**:此簽署者是受信任的。
* **不受信任**:此簽署者不受信任。

**另請參閱**

[使用Java API驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[使用web service API驗證數位簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證數位簽名 {#verify-digital-signatures-using-the-java-api}

使用簽名服務API(Java)驗證數位簽名：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `SignatureServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得包含簽章的PDF檔案以驗證

   * 建立一 `java.io.FileInputStream` 個物件，代表包含要使用其建構函式驗證之簽名的PDF檔案。 傳遞指定PDF檔案位置的字串值。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 設定PKI執行時期選項

   * 使用其 `PKIOptions` 建構函式建立物件。
   * 調用物件的方法並傳 `PKIOptions` 遞指定驗 `setVerificationTime` 證時間的 `VerificationTime` 列舉值，以設定驗證時間。
   * 借由叫用物件的方法並傳遞列舉值( `PKIOptions` 指定是否執行 `setRevocationCheckStyle` 撤銷檢查), `RevocationCheckStyle` 來設定撤銷檢查選項。

1. 驗證數位簽名

   調用物件的方法並傳 `SignatureServiceClient` 遞下列值， `verify2` 以驗證簽名：

   * 包含 `com.adobe.idp.Document` 數位簽章或認證PDF檔案的物件。
   * 一個字串值，代表包含要驗證之簽名的簽名欄位名稱。
   * 包 `PKIOptions` 含PKI運行時選項的對象。
   * 包 `VerifySPIOptions` 含SPI資訊的實例。 您可以指定 `null` 此參數。
   該方 `verify2` 法傳回包 `PDFSignatureVerificationInfo` 含可用於驗證數字簽名的資訊的對象。

1. 確定簽名的狀態

   * 調用物件的方法，以決定 `PDFSignatureVerificationInfo` 簽名的 `getStatus` 狀態。 此方法返回 `SignatureStatus` 指定簽名狀態的對象。 例如，如果未修改已簽署的PDF檔案，此方法會傳回 `SignatureStatus.DocumentSigNoChanges`。

1. 決定簽署者的身分

   * 叫用物件的方法，以決定簽 `PDFSignatureVerificationInfo` 署者的身 `getSigner` 分。 此方法返回對 `IdentityInformation` 像。
   * 叫用物 `IdentityInformation` 件的方 `getStatus` 法，以判斷簽署者的身分。 此方法返回指 `IdentityStatus` 定身份的枚舉值。 例如，如果簽署者受信任，此方法會傳回 `IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[快速入門（SOAP模式）:使用Java API驗證數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API驗證數位簽名 {#verify-digital-signatures-using-the-web-service-api}

使用簽名服務API(web service)驗證數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立簽名用戶端

   * 使用其 `SignatureServiceClient` 預設建構函式建立物件。
   * 使用建 `SignatureServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `SignatureServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含簽章的PDF檔案以驗證

   * 使用其 `BLOB` 建構函式建立物件。 此物 `BLOB` 件用來儲存包含數位或認證簽名以進行驗證的PDF檔案。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表已簽署PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為 `BLOB` 對象的屬性指 `MTOM` 定位元組陣列的內容來填充對象。

1. 設定PKI執行時期選項

   * 使用其 `PKIOptions` 建構函式建立物件。
   * 為物件的資料成員指派 `PKIOptions` 列舉值，以 `verificationTime` 指定驗 `VerificationTime` 證時間，以設定驗證時間。
   * 通過為對象的資料成員分配列舉值來設 `PKIOptions` 置撤銷檢查選 `revocationCheckStyle` 項， `RevocationCheckStyle` 該枚舉值指定是否執行撤銷檢查。

1. 驗證數位簽名

   調用物件的方法並傳 `SignatureServiceClient` 遞下列值， `verify2` 以驗證簽名：

   * 包含 `BLOB` 數位簽章或認證PDF檔案的物件。
   * 一個字串值，代表包含要驗證之簽名的簽名欄位名稱。
   * 包 `PKIOptions` 含PKI運行時選項的對象。
   * 包 `VerifySPIOptions` 含SPI資訊的實例。 您可以指定 `null` 此參數。
   該方 `verify2` 法傳回包 `PDFSignatureVerificationInfo` 含可用於驗證數字簽名的資訊的對象。

1. 確定簽名的狀態

   取得物件資料成員的值，以決定 `PDFSignatureVerificationInfo` 簽名的 `status` 狀態。 此資料成員儲存 `SignatureStatus` 指定簽名狀態的物件。 例如，如果已簽署的PDF檔案已修改，資料成 `status` 員會儲存值 `SignatureStatus.DocumentSigNoChanges`。

1. 決定簽署者的身分

   * 擷取物件資料成員的值，以決定簽 `PDFSignatureVerificationInfo` 署者的 `signer` 身分。 此成員返回一 `IdentityInformation` 個對象。
   * 擷取物 `IdentityInformation` 件的資料 `status` 成員，以判斷簽署者的身分。 此資料成員返回 `IdentityStatus` 指定身份的枚舉值。 例如，如果簽署者受信任，此成員會傳回 `IdentityStatus.TRUSTED`。

**另請參閱**

[驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證多個數位簽名 {#verifying-multiple-digital-signatures}

AEM Forms提供驗證PDF檔案中所有數位簽名的方式。 假設PDF檔案包含多個數位簽名，因為業務流程需要多個簽署者的簽名。 例如，請考慮要求貸款主管和經理簽名的財務交易。 您可以使用簽名服務Java API或web service API來驗證PDF檔案中的所有簽名。 驗證多個數位簽名時，您可以檢查每個簽名的狀態和屬性。 在您信任數位簽名之前，建議您先進行驗證。 建議您熟悉驗證單一數位簽名。

>[!NOTE]
>
>如需「簽名」服務和驗證數位簽章的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

若要驗證多個數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含要驗證之簽名的PDF檔案。
1. 設定PKI執行時期選項。
1. 擷取所有數位簽名。
1. 重複所有簽名。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

在您以程式設計方式執行簽名服務操作之前，請先建立簽名服務用戶端。

**取得包含簽名的PDF檔案，以驗證**

若要驗證用於數位簽署或認證PDF檔案的簽名，請取得包含簽名的PDF檔案。

**設定PKI執行時期選項**

設定簽章服務在驗證PDF檔案中所有簽名時使用的這些PKI執行時期選項：

* 驗證時間
* 撤銷檢查
* 時間戳記值

在設定這些選項時，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），指出使用目前時間。 如需不同時間值的詳細資訊，請參閱 `VerificationTime`[AEM Forms API參考中的列舉值](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

您也可以指定是否在驗證程式中執行撤銷檢查。 例如，您可以執行撤銷檢查，以判斷憑證是否已撤銷。 如需有關撤銷檢查選項的詳細資訊，請參閱 `RevocationCheckStyle`[AEM Forms API參考中的列舉值](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

要對證書執行撤銷檢查，請使用對象指定證書撤銷清單(CRL)伺服器的URL `CRLOptionSpec` 。 但是，如果您未指定CRL伺服器的URL，則簽名服務會從憑證取得URL。

執行撤銷檢查時，您可以使用線上證書狀態協定(OCSP)伺服器，而不是使用CRL伺服器。 通常，使用OCSP伺服器而非CRL伺服器時，撤銷檢查的執行速度會更快。 (請參閱 [線上憑證狀態通訊協定](https://tools.ietf.org/html/rfc2560))。

您可以使用Adobe應用程式與服務來設定簽名服務使用的CRL和OCSP伺服器順序。 例如，如果OCSP伺服器是先在Adobe Applications and services中設定，則會檢查OCSP伺服器，接著檢查CRL伺服器。

如果您未執行撤銷檢查，「簽名服務」不會檢查憑證是否已撤銷。 即，忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用和物件來覆寫憑證中指定 `CRLOptionSpec` 的URL `OCSPOptionSpec` 。 例如，若要覆寫CRL伺服器，您可以叫用 `CRLOptionSpec` 物件的方 `setLocalURI` 法。

時間戳記是追蹤已簽署或已認證檔案修改時間的程式。 簽署檔案後，任何人都無法修改它。 時間戳記有助於強制簽署或認證檔案的有效性。 您可以使用物件來設定時間戳記 `TSPOptionSpec` 選項。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和web服務快速啟動中，將驗證時間設定為， `VerificationTime.CURRENT_TIME` 將撤銷檢查設定為 `RevocationCheckStyle.BestEffort`。 由於未指定CRL或OCSP伺服器資訊，因此從證書中獲取伺服器資訊。

**擷取所有數位簽名**

若要確認PDF檔案中的所有數位簽名，請從PDF檔案擷取數位簽名。 所有簽名都會在清單中傳回。 在驗證數位簽名時，請檢查簽名的狀態。

>[!NOTE]
>
>與驗證單一數位簽名不同，當您驗證多個簽名時，不需要指定簽名欄位名稱。

**重複所有簽名**

逐一重複每個簽名。 也就是說，對於每個簽名，請驗證數位簽名，並檢查簽章者的身分和每個簽名的狀態。 (請參閱 [驗證數位簽名](#verify-digital-signatures-using-the-java-api)。)

>[!NOTE]
>
>如果要求是整份檔案，則不需要重複所有簽名。

**另請參閱**

[使用Java API驗證多個數位簽名](#verify-digital-signatures-using-the-java-api)

[使用web service API驗證多個數位簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證多個數位簽名 {#verify-multiple-digital-signatures-using-the-java-api}

使用簽名服務API(Java)驗證多個數位簽名：

1. 包含專案檔案

   在Java專案的類路徑中包含用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `SignatureServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得包含簽名的PDF檔案，以驗證

   * 建立一 `java.io.FileInputStream` 個物件，代表包含多個數位簽章的PDF檔案，並使用其建構函式加以驗證。 傳遞指定PDF檔案位置的字串值。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 設定PKI執行時期選項

   * 使用其 `PKIOptions` 建構函式建立物件。
   * 調用物件的方法並傳 `PKIOptions` 遞指定驗 `setVerificationTime` 證時間的 `VerificationTime` 列舉值，以設定驗證時間。
   * 借由叫用物件的方法並傳遞 `PKIOptions` 列舉值來設定 `setRevocationCheckStyle` 撤銷檢查選項， `RevocationCheckStyle` 指定是否執行撤銷檢查。

1. 擷取所有數位簽名

   叫用物 `SignatureServiceClient` 件的方 `verifyPDFDocument` 法並傳遞下列值：

   * 包 `com.adobe.idp.Document` 含包含多個數位簽名之PDF檔案的物件。
   * 包 `PKIOptions` 含PKI運行時選項的對象。
   * 包 `VerifySPIOptions` 含SPI資訊的實例。 您可以指定 `null` 此參數。
   此方 `verifyPDFDocument` 法會傳回包 `PDFDocumentVerificationInfo` 含PDF檔案中所有數位簽名資訊的物件。

1. 重複所有簽名

   * 叫用物件的方法，以重複 `PDFDocumentVerificationInfo` 所有簽 `getVerificationInfos` 名。 此方法返回每個 `java.util.List` 元素都是對象的對 `PDFSignatureVerificationInfo` 像。 使用物 `java.util.Iterator` 件來重複簽名清單。
   * 使用 `PDFSignatureVerificationInfo` 物件，您可以執行工作，例如呼叫物件的方法，以判斷 `PDFSignatureVerificationInfo` 簽章的狀 `getStatus` 態。 此方法傳回 `SignatureStatus` 靜態資料成員通知您簽名狀態的物件。 例如，如果簽名未知，則此方法會傳回 `SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數位簽名](#verifying-multiple-digital-signatures)

[快速入門（SOAP模式）:使用Java API驗證多個數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API驗證多個數位簽名 {#verifying-multiple-digital-signatures-using-the-web-service-api}

使用簽名服務API(web service)驗證多個數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立簽名用戶端

   * 使用其 `SignatureServiceClient` 預設建構函式建立物件。
   * 使用建 `SignatureServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `SignatureServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含簽名的PDF檔案，以驗證

   * 使用其 `BLOB` 建構函式建立物件。 物件 `BLOB` 會儲存包含多個數位簽章的PDF檔案以進行驗證。
   * 通過調用 `System.IO.FileStream` 其建構子建立對象。 傳遞一個字串值，代表PDF檔案的檔案位置和開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 通過為 `BLOB` 對象的屬性指 `MTOM` 定位元組陣列的內容來填充對象。

1. 設定PKI執行時期選項

   * 使用其 `PKIOptions` 建構函式建立物件。
   * 為物件的資料成員指派 `PKIOptions` 列舉值，以 `verificationTime` 指定驗 `VerificationTime` 證時間，以設定驗證時間。
   * 通過為對象的資料成員分配一 `PKIOptions` 個枚舉值來設 `revocationCheckStyle` 置撤銷檢 `RevocationCheckStyle` 查選項，該枚舉值指定是否執行撤銷檢查。

1. 擷取所有數位簽名

   叫用物 `SignatureServiceClient` 件的方 `verifyPDFDocument` 法並傳遞下列值：

   * 包 `BLOB` 含包含多個數位簽名之PDF檔案的物件。
   * 包 `PKIOptions` 含PKI運行時選項的對象。
   * 包 `VerifySPIOptions` 含SPI資訊的實例。 您可以為此參數指定null。
   此方 `verifyPDFDocument` 法會傳回包 `PDFDocumentVerificationInfo` 含PDF檔案中所有數位簽名資訊的物件。

1. 重複所有簽名

   * 取得物件的資料成員，以 `PDFDocumentVerificationInfo` 重複所有 `verificationInfos` 簽名。 此資料成員返回每個 `Object` 元素都是對象的陣 `PDFSignatureVerificationInfo` 列。
   * 使用 `PDFSignatureVerificationInfo` 物件，您可以取得物件的資料成員，以執行如決定簽 `PDFSignatureVerificationInfo` 名狀態等 `status` 工作。 此資料成員返回一 `SignatureStatus` 個對象，其靜態資料成員會通知您有關簽名的狀態。 例如，如果簽名未知，則此方法會傳回 `SignatureStatus.DocumentSignatureUnknown`。

**另請參閱**

[驗證多個數位簽名](#verifying-multiple-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 移除數位簽名 {#removing-digital-signatures}

必須先從簽名欄位移除數位簽名，才能套用較新的數位簽名。 無法覆寫數位簽名。 如果您嘗試將數位簽名套用至包含簽名的簽名欄位，則會發生例外。

>[!NOTE]
>
>如需簽名服務的詳細資訊，請參閱「AEM表 [單的服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

若要從簽名欄位移除數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽名用戶端。
1. 取得包含要移除之簽名的PDF檔案。
1. 從簽名欄位移除數位簽名。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立簽名用戶端**

您必須先建立簽名服務用戶端，才能以程式設計方式執行簽名服務作業。

**取得包含要移除之簽名的PDF檔案**

若要從PDF檔案移除簽名，您必須取得包含簽名的PDF檔案。

**從簽名欄位移除數位簽名**

若要成功從PDF檔案移除數位簽章，您必須指定包含數位簽章的簽名欄位名稱。 此外，您必須擁有移除數位簽名的權限；否則，會發生例外。

**將PDF檔案儲存為PDF檔案**

在簽名服務從簽名欄位移除數位簽名後，您可以將PDF檔案儲存為PDF檔案，讓使用者在Acrobat或Adobe Reader中開啟它。

**另請參閱**

[使用Java API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用web service API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API移除數位簽名 {#remove-digital-signatures-using-the-java-api}

使用簽名API(Java)移除數位簽名：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名用戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `SignatureServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 取得包含要移除之簽名的PDF檔案

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞指定PDF檔案位置的字串值，建立代表PDF檔案的物件，其中包含要移除的簽名。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 從簽名欄位移除數位簽名

   叫用物件的方法並傳遞下列值，從簽名欄 `SignatureServiceClient` 位移除 `clearSignatureField` 數位簽名：

   * 表 `com.adobe.idp.Document` 示PDF檔案的物件，其中包含要移除的簽名。
   * 一個字串值，它指定包含數字簽名的簽名欄位的名稱。
   此方 `clearSignatureField` 法會傳回 `com.adobe.idp.Document` 一個物件，該物件代表移除數位簽名的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法。 傳遞 `java.io.File` 物件，將物件的內容 `com.adobe.idp.Document` 複製到檔案。 請確定您使用 `Document` 方法傳回的物 `clearSignatureField` 件。

**另請參閱**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速入門（SOAP模式）:使用Java API移除數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API移除數位簽名 {#remove-digital-signatures-using-the-web-service-api}

使用簽名API(web service)移除數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立簽名用戶端

   * 使用其 `SignatureServiceClient` 預設建構函式建立物件。
   * 使用建 `SignatureServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。)
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `SignatureServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 取得包含要移除之簽名的PDF檔案

   * 使用其 `BLOB` 建構函式建立物件。 該 `BLOB` 物件用來儲存包含要移除之數位簽名的PDF檔案。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示已簽名PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法，以串流資料填 `System.IO.FileStream` 入位元組 `Read` 陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
   * 為對象 `BLOB` 賦值其屬性， `MTOM` 使其包含位元組陣列的內容。

1. 從簽名欄位移除數位簽名

   叫用物件的方法並傳 `SignatureServiceClient` 遞下列值， `clearSignatureField` 以移除數位簽名：

   * 包含 `BLOB` 已簽署PDF檔案的物件。
   * 一個字串值，代表包含要移除之數位簽名之簽名欄位的名稱。
   此方 `clearSignatureField` 法會傳回 `BLOB` 一個物件，該物件代表移除數位簽名的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示包含空簽名欄位的PDF文檔的檔案位置以及開啟檔案的模式。
   * 建立一個位元組陣列，該陣列儲存方 `BLOB` 法返回的對象的內 `sign` 容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
