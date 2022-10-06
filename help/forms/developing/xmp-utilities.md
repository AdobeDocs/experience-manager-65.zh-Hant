---
title: 使用XMP公用程式
seo-title: Working with XMP Utilities
description: 使用XMP公用程式Java和Web服務API，以程式設計方式將XMP中繼資料匯入PDF檔案，以及從PDF檔案擷取和儲存XMP中繼資料。
seo-description: Use the XMP Utilities Java and Web Service APIs to programmatically import XMP metadata into a PDF document and retrieve and save XMP metadata from a PDF document.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---

# 使用XMP公用程式 {#working-with-xmp-utilities}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於XMP公用程式服務**

PDF文檔包含元資料，元資料是與文檔內容（如文本和圖形）區別的文檔的資訊。 Adobe可擴充中繼資料平台(XMP)是處理檔案中繼資料的標準。

XMP公用程式服務可從PDF檔案擷取和儲存XMP中繼資料，並將XMP中繼資料匯入PDF檔案。

您可以使用XMP公用程式服務來完成下列工作：

* 將中繼資料匯入PDF檔案。 (請參閱 [將中繼資料匯入PDF檔案](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* 從PDF文檔導出元資料。 (請參閱 [從PDF文檔導出元資料](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>如需XMP公用程式服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將中繼資料匯入PDF檔案 {#importing-metadata-into-pdf-documents}

您可以使用XMP公用程式Java和網站服務API，以程式設計方式將XMP中繼資料匯入PDF檔案。 元資料提供關於PDF文檔的資訊，如文檔的作者和與文檔相關的關鍵字。 可以在文檔的「文檔屬性」對話框中找到元資料，如下圖所示。

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

要以寫程式方式將元資料導入PDF文檔，可以使用指定元資料值的現有XML文檔，或者可以使用類型的對象 `XMPUtilityMetadata`. (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>本節討論如何使用XML文檔將元資料導入PDF文檔。

以下XML代碼包含與上圖對應的元資料值。 例如，請注意指定關鍵字的粗體項目。

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>如需XMP公用程式服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要將XMP中繼資料匯入PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立XMPUtilityService客戶端。
1. 叫用XMP中繼資料匯入操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立XMPUtilityService客戶端**

在以寫程式方式執行XMP實用程式操作之前，必須建立XMPUtilityService客戶端。 使用Java API，您可以建立 `XMPUtilityServiceClient` 物件。 若使用網站服務API，則需使用 `XMPUtilityServiceService` 物件。

**叫用XMP中繼資料匯入作業**

建立服務客戶端後，可以調用其中一個XMP元資料導入操作，將XMP元資料導入指定的PDF文檔。

**另請參閱**

[使用Java API匯入XMP中繼資料](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用網站服務API匯入XMP中繼資料](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API匯入XMP中繼資料 {#import-xmp-metadata-using-the-java-api}

使用XMP公用程式API(Java)匯入XMP中繼資料：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar檔案包含可讓您以程式設計方式叫用XMP公用程式服務的類別。

1. 建立XMPUtilityService客戶端

   建立 `XMPUtilityServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 叫用XMP中繼資料匯入作業

   若要修改XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件 `importMetadata` 方法或其 `importXMP` 方法。

   如果您使用 `importMetadata` 方法，請傳入下列值：

   * A `com.adobe.idp.Document` 代表PDF檔案的物件。
   * 安 `XMPUtilityMetadata` 包含要匯入中繼資料的物件。

   如果您使用 `importXMP` 方法，請傳入下列值：

   * A `com.adobe.idp.Document` 代表PDF檔案的物件。
   * A `com.adobe.idp.Document` 表示包含要導入元資料的XML檔案的對象。

   在任何情況下，傳回的值都是 `com.adobe.idp.Document` 物件，用新匯入的中繼資料代表PDF檔案。 然後，您可以將此對象保存到磁碟。

**另請參閱**

[將中繼資料匯入PDF檔案](xmp-utilities.md#importing-metadata-into-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API匯入XMP中繼資料 {#importing-xmp-metadata-using-the-web-service-api}

若要使用XMP公用程式網站服務API以程式設計方式匯入XMP中繼資料，請執行下列工作：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用XMP實用程式服務WSDL檔案。 (請參閱 [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * 參考Microsoft .NET客戶端程式集。 (請參閱 [建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. 建立XMPUtilityService客戶端

   建立 `XMPUtilityServiceService` 物件，使用您的proxy類別建構子。

1. 叫用XMP中繼資料匯入作業

   若要修改XMP中繼資料，請叫用 `XMPUtilityServiceService` 物件 `importMetadata` 方法或其 `importXMP` 方法。

   如果您使用 `importMetadata` 方法，請傳入下列值：

   * A `BLOB` 代表PDF檔案的物件。
   * 安 `XMPUtilityMetadata` 包含要匯入中繼資料的物件。

   如果您使用 `importXMP` 方法，請傳入下列值：

   * A `BLOB` 代表PDF檔案的物件。
   * A `BLOB` 表示包含要導入元資料的XML檔案的對象。

   在任何情況下，傳回的值都是 `BLOB` 物件，用新匯入的中繼資料代表PDF檔案。 然後，您可以將此對象保存到磁碟。

**另請參閱**

[將中繼資料匯入PDF檔案](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 從PDF文檔導出元資料 {#exporting-metadata-from-pdf-documents}

您可以使用XMP公用程式Java和網頁服務API，以程式設計方式擷取和儲存PDF檔案中的XMP中繼資料。

>[!NOTE]
>
>如需XMP公用程式服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

要從PDF文檔導出XMP元資料，請執行以下步驟：

1. 包含專案檔案。
1. 建立XMPUtilityService客戶端。
1. 叫用XMP中繼資料匯出操作。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立XMPUtilityService客戶端**

在以寫程式方式執行XMP實用程式操作之前，必須建立XMPUtilityService客戶端。 使用Java AP，若要完成此作業，請建立 `XMPUtilityServiceClient` 物件。 若使用網站服務API，這是使用 `XMPUtilityServiceService` 物件。

**叫用XMP中繼資料匯出作業**

建立服務用戶端後，您可以叫用其中一個XMP中繼資料匯出作業，這可用來檢查XMP中繼資料或將其儲存至磁碟。

**另請參閱**

[使用Java API匯入XMP中繼資料](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用網站服務API匯入XMP中繼資料](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API匯出XMP中繼資料 {#export-xmp-metadata-using-the-java-api}

使用XMP公用程式API(Java)匯出XMP中繼資料：

1. 包含項目檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar檔案包含可讓您以程式設計方式叫用XMP公用程式服務的類別。

1. 建立XMPUtilityService客戶端

   建立 `XMPUtilityServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 叫用XMP中繼資料匯入作業

   若要檢查XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件 `exportMetadata` 在 `com.adobe.idp.Document` 代表PDF檔案的物件。 方法會傳回 `XMPUtilityMetadata` 包含擷取中繼資料的物件。

   若要擷取並儲存XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件 `exportXMP` 在 `com.adobe.idp.Document` 代表PDF檔案的物件。 方法會傳回 `com.adobe.idp.Document` 包含檢索到的元資料的對象，您隨後可以將其另存為XML檔案。

**另請參閱**

[從PDF文檔導出元資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API匯出XMP中繼資料 {#export-xmp-metadata-using-the-web-service-api}

使用XMP公用程式API（網站服務）匯出XMP中繼資料：

1. 包含項目檔案

   * 建立一個Microsoft .NET客戶端程式集，該程式集將使用XMP實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端程式集。

1. 建立XMPUtilityService客戶端

   建立 `XMPUtilityServiceService` 物件，使用您的proxy類別建構子。

1. 叫用XMP中繼資料匯入作業

   若要檢查XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件 `exportMetadata` 在 `BLOB` 代表PDF檔案的物件。 方法會傳回 `XMPUtilityMetadata` 包含擷取中繼資料的物件。

   若要擷取並儲存XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件 `exportXMP` 在 `BLOB` 代表PDF檔案的物件。 方法會傳回 `BLOB` 包含檢索到的元資料的對象，您隨後可以將其另存為XML檔案。

**另請參閱**

[從PDF文檔導出元資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
