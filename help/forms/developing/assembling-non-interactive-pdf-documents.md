---
title: 匯編非互動式PDF文檔
seo-title: Assembling Non-Interactive PDF Documents
description: 使用非互動式PDF表單作為輸入，使用Java API和Web服務API匯編非互動式PDF文檔。
seo-description: Use a non-interactive PDF form as input to assemble a non-interactive PDF document using the Java API and Web Service API.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# 匯編非互動式PDF文檔 {#assembling-non-interactive-pdf-documents}

使用互動式PDF表單作為輸入時，可以匯編非互動式PDF文檔。 也就是說，假定您有一個表單，用戶可以使用它將資料輸入到其欄位中。 您可以將該表單傳遞給匯編器服務，導致匯編器服務返回PDF文檔，該文檔阻止用戶在其欄位中輸入資料。 此文檔是非互動式PDF窗體。 例如，下圖顯示了表示互動式表單的抵押申請。

在本討論中，假定使用了以下DDX文檔。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

在此DDX文檔中，請注意已為源屬性分配了值 `inDoc`。 在僅將一個輸入PDF文檔傳遞給匯編器服務並返回一個PDF文檔的情況下，您將調用 `invokeOneDocument` 操作，分配值 `inDoc` PDF源屬性。 調用 `invokeOneDocument` 操作， `inDoc` value是必須在DDX文檔中指定的預定義鍵。

相反，將兩個或多個輸入PDF文檔傳遞到匯編器服務時，可以調用 `invokeDDX` 的下界。 在這種情況下，將輸入PDF文檔的檔案名分配給 `source` 屬性。

此DDX文檔包含 `NoXFA` 元素，指示匯編器服務返回非互動式PDF文檔。

如果輸入PDF文檔基於Acrobat表單或靜態XFA表單，則匯編服務可以匯編非互動式PDF文檔，AEM而「輸出」服務不是表單安裝的一部分。 但是，如果輸入PDF文檔是動態XFA表單，則輸出服務必須是表單安裝的AEM一部分。 如果在裝配動態XFA表單AEM時輸出服務不是表單安裝的一部分，則會引發異常。 請參閱 [建立文檔輸出流](/help/forms/developing/creating-document-output-streams.md)。

>[!NOTE]
>
>在閱讀本節之前，建議您熟悉使用匯編器服務PDF文檔。 本節不討論概念，如建立包含輸入文檔的集合對象或學習如何從返回的集合對象中提取結果。 (請參閱 [以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>有關匯編器服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有關DDX文檔的詳細資訊，請參見 [匯編程式服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步驟摘要 {#summary-of-steps}

要匯編非互動式PDF文檔，請執行以下任務：

1. 包括項目檔案。
1. 建立PDF匯編器客戶端。
1. 引用現有DDX文檔。
1. 引用互動式PDF文檔。
1. 設定運行時選項。
1. 匯編PDF文檔。
1. 保存非互動式PDF文檔。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms時必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss上，則為必需)

如果AEM Forms部署在JBoss以外的受支援的J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案替換為特定於AEM Forms部署在其上的J2EE應用程式伺服器的JAR檔案。

**建立匯編器客戶端**

在以寫程式方式執行匯編器操作之前，必須建立匯編器服務客戶端。

**引用現有DDX文檔**

必須引用DDX文檔來匯編PDF文檔。 此DDX文檔必須包含 `NoXFA` 元素，指示匯編器服務返回非互動式PDF文檔。

**引用互動式PDF文檔**

必須引用互動式PDF文檔並將其傳遞給匯編程式服務，才能返回非互動式PDF文檔。

**設定運行時選項**

您可以設定運行時選項，這些選項在匯編程式服務執行作業時控制其行為。 例如，您可以設定一個選項，指示匯編程式服務在遇到錯誤時繼續處理作業。

**匯編PDF文檔**

在建立匯編器服務客戶端、引用DDX文檔、引用互動式PDF文檔和設定運行時選項後，可以調用 `invokeOneDocument` 的下界。 由於只有一個輸入PDF文檔被傳遞給匯編器服務，並且返回了單個文檔，因此您可以使用 `invokeOneDocument` 與 `invokeDDX` 的下界。

**保存非互動式PDF文檔**

如果僅將單個PDF文檔傳遞給匯編器服務，匯編器服務將返回單個文檔，而不是集合對象。 就是說，當調用 `invokeOneDocument` 操作，返回單個文檔。 由於本節中引用的DDX文檔包含建立非互動式PDF文檔的說明，因此匯編器服務將返回非互動式PDF文檔，該文檔可保存為PDF檔案。

**另請參閱**

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以寫程式方式裝配PDF文檔](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API匯編非互動式PDF文檔 {#assemble-a-non-interactive-pdf-document-using-the-java-api}

使用匯編器服務API(Java)匯編非互動式PDF文檔：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-assembler-client.jar。

1. 建立匯編器客戶端。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `AssemblerServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 引用現有DDX文檔。

   * 建立 `java.io.FileInputStream` 表示DDX文檔的對象，方法是使用其建構子並傳遞一個字串值，該字串值指定DDX檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用其建構子並傳遞對象 `java.io.FileInputStream` 的雙曲餘切值。

1. 引用互動式PDF文檔。

   * 建立 `java.io.FileInputStream` 使用其建構子並傳遞互動式PDF文檔的位置。
   * 建立 `com.adobe.idp.Document` 並傳遞 `java.io.FileInputStream` 包含PDF文檔的對象。 此 `com.adobe.idp.Document` 對象被傳遞到 `invokeOneDocument` 的雙曲餘切值。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過調用屬於的方法來設定運行時選項以滿足業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編器服務在發生錯誤時繼續處理作業，請調用 `AssemblerOptionSpec` 對象 `setFailOnError` 方法 `false`。

1. 匯編PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeOneDocument` 方法並傳遞以下值：

   * A `com.adobe.idp.Document` 表示DDX文檔的對象。 確保此DDX文檔包含值 `inDoc` PDF源元素。
   * A `com.adobe.idp.Document` 包含互動式PDF文檔的對象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定運行時選項（包括預設字型和作業日誌級別）的對象。

   的 `invokeOneDocument` 方法返回 `com.adobe.idp.Document` 包含非互動式PDF文檔的對象。

1. 保存非互動式PDF文檔。

   * 建立 `java.io.File` 對象，並確保檔案副檔名為.pdf。
   * 調用 `Document` 對象 `copyToFile` 複製內容的方法 `Document` 對象。 確保使用 `Document` 對象 `invokeOneDocument` 返回。

* 「快速啟動（SOAP模式）:使用Java API匯編非互動式PDF文檔&quot;

## 使用Web服務API匯編非互動式PDF文檔 {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

使用匯編器服務API（Web服務）匯編非互動式PDF文檔：

1. 包括項目檔案。

   建立使用MTOM的Microsoft.NET項目。 確保使用以下WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >替換 `localhost` IP地址為AEM Forms。

1. 建立匯編器客戶端。

   * 建立 `AssemblerServiceClient` 對象。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `AssemblerServiceClient.Endpoint.Binding` 的子菜單。 將返回值強制轉換為 `BasicHttpBinding`。
   * 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 欄位 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
   * 通過執行以下任務啟用基本HTTP身份驗證：

      * 將表AEM單用戶名分配給欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 將相應的密碼值分配給欄位 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 分配常數值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用現有DDX文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存DDX文檔。
   * 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值（該字串值表示DDX文檔的檔案位置和開啟檔案的模式）來對對象。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 引用互動式PDF文檔。

   * 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存輸入PDF文檔。 此 `BLOB` 對象被傳遞到 `invokeOneDocument` 作為論據。
   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示輸入PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
   * 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
   * 填充 `BLOB` 通過指定對象 `MTOM` 欄位。

1. 設定運行時選項。

   * 建立 `AssemblerOptionSpec` 使用其建構子儲存運行時選項的對象。
   * 通過將值分配給屬於的資料成員來設定運行時選項以滿足您的業務需求 `AssemblerOptionSpec` 的雙曲餘切值。 例如，要指示匯編程式服務在發生錯誤時繼續處理作業，請分配 `false` 到 `AssemblerOptionSpec` 對象 `failOnError` 資料成員。

1. 匯編PDF文檔。

   調用 `AssemblerServiceClient` 對象 `invokeOneDocument` 方法並傳遞以下值：

   * A `BLOB` 表示DDX文檔的對象
   * A `BLOB` 表示互動式PDF文檔的對象
   * 安 `AssemblerOptionSpec` 指定運行時選項的對象

   的 `invokeOneDocument` 方法返回 `BLOB` 包含非互動式PDF文檔的對象。

1. 保存非互動式PDF文檔。

   * 建立 `System.IO.FileStream` 調用其建構子並傳遞一個字串值，該字串值表示非互動式PDF文檔的檔案位置以及在中開啟檔案的模式。
   * 建立一個位元組陣列，用於儲存 `BLOB` 對象 `invokeOneDocument` 返回。 通過獲取 `BLOB` 對象 `MTOM` 的子菜單。
   * 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
   * 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

* 「快速啟動(MTOM):使用Web服務API匯編非互動式PDF文檔」。

**另請參閱**

[使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
