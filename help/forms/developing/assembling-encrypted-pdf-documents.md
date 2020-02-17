---
title: 組合加密的PDF檔案
seo-title: 組合加密的PDF檔案
description: 'null'
seo-description: 'null'
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 組合加密的PDF檔案 {#assembling-encrypted-pdf-documents}

您可以使用Assembler服務，以密碼加密PDF檔案。 使用密碼加密PDF檔案後，使用者必須指定密碼才能在Adobe Reader或Acrobat中檢視PDF檔案。 要使用密碼加密PDF文檔，DDX文檔必須包含加密PDF文檔所需的加密元素值。

在本討論中，假設使用了以下DDX文檔。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

在此DDX文檔中，請注意源屬性已分配值 `inDoc`。 在僅將一個輸入的PDF檔案傳遞至Assembler服務並傳回一個PDF檔案，而您叫用該操作的情 `invokeOneDocument` 況下，請將值指 `inDoc` 派給PDF來源屬性。 調用操 `invokeOneDocument` 作時，值 `inDoc` 是必須在DDX文檔中指定的預定義鍵。

相反地，將兩個或兩個以上輸入的PDF檔案傳遞至Assembler服務時，您可以叫用該 `invokeDDX` 操作。 在此情況下，請將輸入PDF檔案的檔案名稱指派給屬 `source` 性。

Encryption服務不必是AEM表單安裝的一部分，就能以密碼加密PDF檔案。 請參 [閱加密和解密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md)。

>[!NOTE]
>
>如需Assembler服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參 [閱Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要組合加密的PDF文檔，請執行以下步驟：

1. 包含專案檔案。
1. 建立PDF匯寫程式式用戶端。
1. 參考現有的DDX檔案。
1. 參考不安全的PDF檔案。
1. 設定執行時期選項。
1. 加密文檔。
1. 儲存加密的PDF檔案。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（若AEM Forms部署在JBoss上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss上，則為必要）

如果AEM Forms部署在JBoss以外的支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為JAR檔案，而AEM Forms部署在該J2EE應用程式伺服器上。 如需所有AEM Forms JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立Assembler客戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合PDF檔案。 例如，請考慮本節中介紹的DDX文檔。 若要加密PDF檔案，DDX檔案必須包含元 `PasswordEncryptionProfile` 素。

**參考不安全的PDF檔案**

必須參考不安全的PDF檔案，並將它傳送至Assembler服務，才能加密它。 如果您參考已加密的PDF檔案，則會擲出例外。

**設定執行時期選項**

您可以設定運行時選項，以控制Assembler服務在執行作業時的行為。 例如，您可以設定一個選項，指示Assembler服務在遇到錯誤時繼續處理作業。 如需您可設定之執行時期選項的詳細資訊，請參閱 `AssemblerOptionSpec`[AEM Forms API參考中的類別參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**加密檔案**

在建立Assembler服務客戶端後，請參考包含加密資訊的DDX文檔、引用不安全的PDF文檔並設定運行時選項，您可以調用該操 `invokeOneDocument` 作。 由於只有一個輸入的PDF文檔被傳遞到Assembler服務（並且有一個文檔被傳回），因此您可以使用該 `invokeOneDocument` 操作而不是該操 `invokeDDX` 作。

**儲存加密的PDF檔案**

如果僅將單一PDF文檔傳遞給Assembler服務，Assembler服務將返回單一文檔而非集合對象。 即，調用操作時， `invokeOneDocument` 將返回單個文檔。 由於本節中引用的DDX文檔包含加密資訊，因此Assembler服務返回使用密碼加密的PDF文檔。

**另請參閱**

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API組合加密的PDF檔案 {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. 包含專案檔案。

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-assembler-client.jar。

1. 建立Assembler客戶端。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `AssemblerServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 參考現有的DDX檔案。

   * 使用 `java.io.FileInputStream` 其建構子並傳遞指定DDX檔案位置的字串值，建立表示DDX文檔的對象。
   * 使用其 `com.adobe.idp.Document` 建構函式並傳遞物件，以建立物 `java.io.FileInputStream` 件。

1. 參考不安全的PDF檔案。

   * 使用 `java.io.FileInputStream` 其建構函式並傳遞不安全PDF檔案的位置，以建立物件。
   * 建立物 `com.adobe.idp.Document` 件並傳遞包 `java.io.FileInputStream` 含PDF檔案的物件。 此對 `com.adobe.idp.Document` 像會傳遞至方 `invokeOneDocument` 法。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 調用屬於該對象的方法，以設定運行時選項以滿足您的業務 `AssemblerOptionSpec` 要求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請叫用 `AssemblerOptionSpec` 物件的方 `setFailOnError` 法並傳遞 `false`。

1. 加密文檔。

   叫用物 `AssemblerServiceClient` 件的方 `invokeOneDocument` 法並傳遞下列值：

   * 表 `com.adobe.idp.Document` 示DDX文檔的對象。 請確定此DDX檔案包含PDF `inDoc` 來源元素的值。
   * 包 `com.adobe.idp.Document` 含不安全PDF文檔的對象。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 運行時選項（包括預設字型和作業日誌級別）的對象。
   此方 `invokeOneDocument` 法會傳回包 `com.adobe.idp.Document` 含密碼加密PDF檔案的物件。

1. 儲存加密的PDF檔案。

   * 建立物 `java.io.File` 件，並確定副檔名為。pdf。
   * 叫用 `Document` 物件的方 `copyToFile` 法，將物件的內容 `Document` 複製至檔案。 請確定您使用 `Document` 方法傳回的 `invokeOneDocument` 物件。

**另請參閱**

[快速入門（SOAP模式）:使用Java API組合加密的PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## 使用web service API組合加密的PDF檔案 {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 在設定服務引用時，請確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >以代 `localhost` 管AEM Forms之伺服器的IP位址取代。

1. 建立Assembler客戶端。

   * 使用其 `AssemblerServiceClient` 預設建構函式建立物件。
   * 使用建 `AssemblerServiceClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。
   * 獲取 `System.ServiceModel.BasicHttpBinding` 欄位值以建立對 `AssemblerServiceClient.Endpoint.Binding` 像。 將返回值轉換為 `BasicHttpBinding`。
   * 將物 `System.ServiceModel.BasicHttpBinding` 件欄位設 `MessageEncoding` 為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作以啟用基本HTTP驗證：

      * 指派AEM表單使用者名稱至欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 為欄位分配相應的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值指 `HttpClientCredentialType.Basic` 派給欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值指 `BasicHttpSecurityMode.TransportCredentialOnly` 派給欄位 `BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用其 `BLOB` 建構函式建立物件。 對 `BLOB` 像用於儲存DDX文檔。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示DDX文檔的檔案位置以及在中開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 參考不安全的PDF檔案。

   * 使用其 `BLOB` 建構函式建立物件。 物件 `BLOB` 用來儲存輸入的PDF檔案。 此 `BLOB` 對象作為引數 `invokeOneDocument` 傳遞給。
   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示輸入PDF文檔的檔案位置和開啟檔案的模式。
   * 建立儲存物件內容的位元組 `System.IO.FileStream` 陣列。 您可以取得物件的屬性，以決定位元組 `System.IO.FileStream` 的大 `Length` 小。
   * 調用物件的方法並傳遞 `System.IO.FileStream` 位元組陣列、 `Read` 開始位置和串流長度，以串流資料填入位元組陣列。
   * 為對象 `BLOB` 分配欄位時， `MTOM` 請使用位元組陣列的內容來填充該對象。

1. 設定執行時期選項。

   * 使用 `AssemblerOptionSpec` 其建構函式建立儲存執行時期選項的物件。
   * 通過為屬於該對象的資料成員分配值，設定運行時選項以滿足您的業務需 `AssemblerOptionSpec` 求。 例如，若要指示Assembler服務在發生錯誤時繼續處理作業，請指 `false` 派給 `AssemblerOptionSpec` 物件的資料 `failOnError` 成員。

1. 加密文檔。

   叫用物 `AssemblerServiceClient` 件的方 `invokeOneDocument` 法並傳遞下列值：

   * 代 `BLOB` 表DDX文檔的對象
   * 表示 `BLOB` 不安全PDF文檔的對象
   * 指定 `AssemblerOptionSpec` 運行時選項的對象
   此方 `invokeOneDocument` 法會傳回包 `BLOB` 含加密PDF檔案的物件。

1. 儲存加密的PDF檔案。

   * 通過調 `System.IO.FileStream` 用其建構子並傳遞一個字串值來建立對象，該字串值表示加密的PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立位元組陣列，該陣列儲存方法 `BLOB` 返回的對 `invokeOneDocument` 像內容。 取得物件資料成員的值，以填 `BLOB` 入位元組 `MTOM` 陣列。
   * 通過調 `System.IO.BinaryWriter` 用其建構子並傳遞對象來建立 `System.IO.FileStream` 對象。
   * 調用物件的方法並傳遞位元組陣列，將位元組 `System.IO.BinaryWriter` 的內容 `Write` 寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
