---
title: 組合加密的PDF檔案
description: 使用Java API和Web服務API彙編加密的PDF檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---

# 組合加密的PDF檔案 {#assembling-encrypted-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

您可以使用Assembler服務，以密碼加密PDF檔案。 使用密碼加密PDF檔案後，使用者必須指定密碼，才能在Adobe Reader或Acrobat中檢視PDF檔案。 若要使用密碼加密PDF檔案，DDX檔案必須包含加密PDF檔案所需的加密元素值。

為了進行此討論，假設使用下列DDX檔案。

```xml
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

在此DDX檔案中，請注意來源屬性已指派值`inDoc`。 如果只有一個輸入PDF檔案傳遞至Assembler服務並傳回一個PDF檔案，而您叫用`invokeOneDocument`作業，請將值`inDoc`指派給PDF來源屬性。 叫用`invokeOneDocument`作業時，`inDoc`值是必須在DDX檔案中指定的預先定義金鑰。

相反地，將兩個或多個輸入PDF檔案傳遞至Assembler服務時，您可以叫用`invokeDDX`作業。 在此情況下，將輸入PDF檔案的檔案名稱指派給`source`屬性。

加密服務不一定要成為AEM表單安裝的一部分，才能使用密碼加密PDF檔案。 請參閱[加密和解密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md)。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱[組合器服務與DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

若要組合已加密的PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考不安全的PDF檔案。
1. 設定執行階段選項。
1. 加密檔案。
1. 儲存加密的PDF檔案。

**包含專案檔**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在J2EE應用程式伺服器的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立組合器使用者端**

您必須先建立組合器服務使用者端，才能以程式設計方式執行組合器作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDF檔案。 例如，以本節介紹的DDX檔案為例。 若要加密PDF檔案，DDX檔案必須包含`PasswordEncryptionProfile`專案。

**參考不安全的PDF檔案**

不安全的PDF檔案必須參考並傳遞給Assembler服務才能加密。 如果您參照已加密的PDF檔案，則會擲回例外狀況。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。 如需您可以設定的執行階段選項相關資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`類別參考。

**加密檔案**

建立Assembler服務使用者端、參照包含加密資訊的DDX檔案、參照不安全的PDF檔案，以及設定執行階段選項之後，您可以叫用`invokeOneDocument`作業。 因為只有一個輸入PDF檔案傳遞至組合器服務（且傳回了一個檔案），所以您可以使用`invokeOneDocument`作業而非`invokeDDX`作業。

**儲存加密的PDF檔案**

如果只將單一PDF檔案傳遞到Assembler服務，則Assembler服務會傳回單一檔案，而非集合物件。 也就是說，叫用`invokeOneDocument`作業時，會傳回單一檔案。 因為本節中參考的DDX檔案包含加密資訊，所以Assembler服務會傳回使用密碼加密的PDF檔案。

**另請參閱**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組合PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API彙編加密的PDF檔案 {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立組合器使用者端。

   * 建立包含連線屬性的`ServiceClientFactory`物件。
   * 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`AssemblerServiceClient`物件。

1. 參考現有的DDX檔案。

   * 使用它的建構函式並傳遞指定DDX檔案位置的字串值，建立代表DDX檔案的`java.io.FileInputStream`物件。
   * 使用它的建構函式並傳遞`java.io.FileInputStream`物件來建立`com.adobe.idp.Document`物件。

1. 參考不安全的PDF檔案。

   * 使用建構函式並傳遞不安全PDF檔案的位置，來建立`java.io.FileInputStream`物件。
   * 建立`com.adobe.idp.Document`物件並傳遞包含PDF檔案的`java.io.FileInputStream`物件。 此`com.adobe.idp.Document`物件已傳遞至`invokeOneDocument`方法。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 透過叫用屬於`AssemblerOptionSpec`物件的方法，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用`AssemblerOptionSpec`物件的`setFailOnError`方法，然後傳遞`false`。

1. 加密檔案。

   叫用`AssemblerServiceClient`物件的`invokeOneDocument`方法，並傳遞下列值：

   * 代表DDX檔案的`com.adobe.idp.Document`物件。 確定此DDX檔案包含PDF來源專案的值`inDoc`。
   * 包含不安全PDF檔案的`com.adobe.idp.Document`物件。
   * 指定執行階段選項（包括預設字型和作業記錄層級）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`物件。

   `invokeOneDocument`方法傳回包含密碼加密PDF檔案的`com.adobe.idp.Document`物件。

1. 儲存加密的PDF檔案。

   * 建立`java.io.File`物件，並確定副檔名為.pdf。
   * 叫用`Document`物件的`copyToFile`方法，將`Document`物件的內容複製到檔案。 請確定您使用的是`invokeOneDocument`方法傳回的`Document`物件。

**另請參閱**

[快速入門(SOAP模式)：使用Java API彙編加密的PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## 使用網站服務API彙編加密的PDF檔案 {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 確定您在設定服務參考時使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >將`localhost`取代為主控AEM Forms之伺服器的IP位址。

1. 建立組合器使用者端。

   * 使用預設建構函式建立`AssemblerServiceClient`物件。
   * 使用`System.ServiceModel.EndpointAddress`建構函式建立`AssemblerServiceClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務（例如，`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。
   * 取得`AssemblerServiceClient.Endpoint.Binding`欄位的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
   * 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`欄位設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
   * 執行下列工作來啟用基本的HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將對應的密碼值指派給欄位`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 將常數值`HttpClientCredentialType.Basic`指派給欄位`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給欄位`BasicHttpBindingSecurity.Security.Mode`。

1. 參考現有的DDX檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存DDX檔案。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表DDX檔案檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 參考不安全的PDF檔案。

   * 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存輸入PDF檔案。 此`BLOB`物件會以引數的形式傳遞至`invokeOneDocument`。
   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置及開啟檔案的模式的字串值。
   * 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
   * 呼叫`System.IO.FileStream`物件的`Read`方法，並傳遞要讀取的位元組陣列、起始位置和資料流長度，以資料流資料填入位元組陣列。
   * 以位元組陣列的內容指派其`MTOM`欄位，填入`BLOB`物件。

1. 設定執行階段選項。

   * 使用建構函式建立儲存執行階段選項的`AssemblerOptionSpec`物件。
   * 將值指派給屬於`AssemblerOptionSpec`物件的資料成員，設定執行階段選項以符合您的業務需求。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請將`false`指派給`AssemblerOptionSpec`物件的`failOnError`資料成員。

1. 加密檔案。

   叫用`AssemblerServiceClient`物件的`invokeOneDocument`方法，並傳遞下列值：

   * 代表DDX檔案的`BLOB`物件
   * 代表不安全PDF檔案的`BLOB`物件
   * 指定執行階段選項的`AssemblerOptionSpec`物件

   `invokeOneDocument`方法傳回包含加密PDF檔案的`BLOB`物件。

1. 儲存加密的PDF檔案。

   * 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表加密PDF檔案檔案位置的字串值，以及用來開啟檔案的模式。
   * 建立位元組陣列，儲存`invokeOneDocument`方法傳回的`BLOB`物件內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
   * 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
   * 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

**另請參閱**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
