---
title: 使用實XMP用程式
seo-title: Working with XMP Utilities
description: 使用實XMP用程式Java和Web服務API以寫程式方式將元資料XMP導入PDF文檔，並檢索和保XMP存PDF文檔中的元資料。
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

# 使用實XMP用程式 {#working-with-xmp-utilities}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於實XMP用程式服務**

PDF文檔包含元資料，該元資料是與文檔內容（如文本和圖形）區分的有關文檔的資訊。 Adobe可擴展元資料平XMP台()是處理文檔元資料的標準。

實用XMP程式服務可從PDF文檔中檢XMP索和保存元資料，並將元XMP資料導入PDF文檔。

可以使用「實用程式」(XMPUtilities)服務完成以下任務：

* 將元資料導入PDF文檔。 (請參閱 [將元資料導入PDF文檔](xmp-utilities.md#importing-metadata-into-pdf-documents)。)
* 從PDF文檔導出元資料。 (請參閱 [從PDF文檔導出元資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)。)

>[!NOTE]
>
>有關實用程式服務的XMP詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將元資料導入PDF文檔 {#importing-metadata-into-pdf-documents}

可以使用實XMP用程式Java和Web服務API以寫程式方式將元資料XMP導入PDF文檔。 元資料提供有關PDF文檔的資訊，如文檔的作者和與文檔相關的關鍵字。 元資料可以位於文檔的「文檔屬性」對話框中，如下圖所示。

![ww_ww_元資料對話框](assets/ww_ww_metadatadialog.png)

要以寫程式方式將元資料導入PDF文檔，可以使用指定元資料值的現有XML文檔，或者可以使用類型的對象 `XMPUtilityMetadata`。 (請參閱 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

>[!NOTE]
>
>本節討論如何使用XML文檔將元資料導入PDF文檔。

以下XML代碼包含與上圖對應的元資料值。 例如，請注意指定關鍵字的粗體項。

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
>有關實用程式服務的XMP詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要將元XMP資料導入PDF文檔，請執行以下步驟：

1. 包括項目檔案。
1. 建立XMPUtilityService客戶端。
1. 調用元XMP資料導入操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立XMPUtilityService客戶端**

在以寫程式方式執行實用程XMP序操作之前，必須建立XMPUtilityService客戶端。 使用Java API，通過建立 `XMPUtilityServiceClient` 的雙曲餘切值。 使用Web服務API，可通過使用 `XMPUtilityServiceService` 的雙曲餘切值。

**調用元XMP資料導入操作**

建立服務客戶端後，可以調用元資料導XMP入操作之一，將元XMP資料導入指定的PDF文檔。

**另請參閱**

[使用XMPJava API導入元資料](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用XMPWeb服務API導入元資料](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用XMPJava API導入元資料 {#import-xmp-metadata-using-the-java-api}

使XMP用實用程XMP序API(Java)導入元資料：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar檔案包含允許以寫程式方式調用「實用程式」服務XMP的類。

1. 建立XMPUtilityService客戶端

   建立 `XMPUtilityServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用元XMP資料導入操作

   要修改元XMP資料，請調用 `XMPUtilityServiceClient` 對象 `importMetadata` 方法 `importXMP` 的雙曲餘切值。

   如果使用 `importMetadata` 方法，傳遞以下值：

   * A `com.adobe.idp.Document` 表示PDF檔案的對象。
   * 安 `XMPUtilityMetadata` 包含要導入的元資料的對象。

   如果使用 `importXMP` 方法，傳遞以下值：

   * A `com.adobe.idp.Document` 表示PDF檔案的對象。
   * A `com.adobe.idp.Document` 表示包含要導入的元資料的XML檔案的對象。

   無論哪種情況，返回的值都是 `com.adobe.idp.Document` 用新導入的元資料表示PDF檔案的對象。 然後，可以將此對象保存到磁碟。

**另請參閱**

[將元資料導入PDF文檔](xmp-utilities.md#importing-metadata-into-pdf-documents)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用XMPWeb服務API導入元資料 {#importing-xmp-metadata-using-the-web-service-api}

要使用實用程XMP序Web服務XMPAPI以寫程式方式導入元資料，請執行以下任務：

1. 包括項目檔案

   * 建立使用實用程式服務WSDL檔案的MicrosoftXMP.NET客戶端程式集。 (請參閱 [使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 引用Microsoft.NET客戶端程式集。 (請參閱 [建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。)

1. 建立XMPUtilityService客戶端

   建立 `XMPUtilityServiceService` 對象。

1. 調用元XMP資料導入操作

   要修改元XMP資料，請調用 `XMPUtilityServiceService` 對象 `importMetadata` 方法 `importXMP` 的雙曲餘切值。

   如果使用 `importMetadata` 方法，傳遞以下值：

   * A `BLOB` 表示PDF檔案的對象。
   * 安 `XMPUtilityMetadata` 包含要導入的元資料的對象。

   如果使用 `importXMP` 方法，傳遞以下值：

   * A `BLOB` 表示PDF檔案的對象。
   * A `BLOB` 表示包含要導入的元資料的XML檔案的對象。

   無論哪種情況，返回的值都是 `BLOB` 用新導入的元資料表示PDF檔案的對象。 然後，可以將此對象保存到磁碟。

**另請參閱**

[將元資料導入PDF文檔](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 從PDF文檔導出元資料 {#exporting-metadata-from-pdf-documents}

可以使用實XMP用程式Java和Web服務API以寫程式方式從PDF文檔中檢索XMP和保存元資料。

>[!NOTE]
>
>有關實用程式服務的XMP詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要從XMPPDF文檔導出元資料，請執行以下步驟：

1. 包括項目檔案。
1. 建立XMPUtilityService客戶端。
1. 調用元XMP資料導出操作。

**包括項目檔案**

在開發項目中包含必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

**建立XMPUtilityService客戶端**

在以寫程式方式執行實用程XMP序操作之前，必須建立XMPUtilityService客戶端。 使用Java AP，如果通過建立 `XMPUtilityServiceClient` 的雙曲餘切值。 使用Web服務API，可以使用 `XMPUtilityServiceService` 的雙曲餘切值。

**調用元XMP資料導出操作**

建立服務客戶端後，可以調用元資料導XMP出操作之一，該操作可用於檢查元資料XMP或將其保存到磁碟。

**另請參閱**

[使用XMPJava API導入元資料](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用XMPWeb服務API導入元資料](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用XMPJava API導出元資料 {#export-xmp-metadata-using-the-java-api}

使XMP用實用程XMP序API(Java)導出元資料：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar檔案包含允許以寫程式方式調用實用程式XMP服務的類。

1. 建立XMPUtilityService客戶端

   建立 `XMPUtilityServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 調用元XMP資料導入操作

   要檢查元XMP資料，請調用 `XMPUtilityServiceClient` 對象 `exportMetadata` 方法和傳遞 `com.adobe.idp.Document` 表示PDF檔案的對象。 該方法返回 `XMPUtilityMetadata` 包含檢索到的元資料的對象。

   要檢索和保存元XMP資料，請調用 `XMPUtilityServiceClient` 對象 `exportXMP` 方法和傳遞 `com.adobe.idp.Document` 表示PDF檔案的對象。 該方法返回 `com.adobe.idp.Document` 包含檢索到的元資料的對象，您隨後可以將其另存為XML檔案到磁碟。

**另請參閱**

[從PDF文檔導出元資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用XMPWeb服務API導出元資料 {#export-xmp-metadata-using-the-web-service-api}

使XMP用實用程XMP序API（Web服務）導出元資料：

1. 包括項目檔案

   * 建立使用實用程式服務WSDL檔案的MicrosoftXMP.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立XMPUtilityService客戶端

   建立 `XMPUtilityServiceService` 對象。

1. 調用元XMP資料導入操作

   要檢查元XMP資料，請調用 `XMPUtilityServiceClient` 對象 `exportMetadata` 方法和傳遞 `BLOB` 表示PDF檔案的對象。 該方法返回 `XMPUtilityMetadata` 包含檢索到的元資料的對象。

   要檢索和保存元XMP資料，請調用 `XMPUtilityServiceClient` 對象 `exportXMP` 方法和傳遞 `BLOB` 表示PDF檔案的對象。 該方法返回 `BLOB` 包含檢索到的元資料的對象，您隨後可以將其另存為XML檔案到磁碟。

**另請參閱**

[從PDF文檔導出元資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
