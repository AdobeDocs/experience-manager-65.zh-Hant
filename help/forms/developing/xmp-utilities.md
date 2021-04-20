---
title: 使用實用程式XMP
seo-title: 使用實用程式XMP
description: 使用XMP公用程式Java和Web Service API，以程式設計方式將中繼資料匯XMP入PDF檔案，並從PDF檔案擷取XMP和儲存中繼資料。
seo-description: 使用XMP公用程式Java和Web Service API，以程式設計方式將中繼資料匯XMP入PDF檔案，並從PDF檔案擷取XMP和儲存中繼資料。
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---


# 使用實XMP用程式{#working-with-xmp-utilities}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

**關於公用XMP程式服務**

PDF檔案包含中繼資料，此為與檔案內容（例如文字和圖形）區隔的檔案資訊。 Adobe可擴充中繼資料平台(XMP)是處理檔案中繼資料的標準。

公用程XMP式服務可從PDF檔案擷取和儲XMP存中繼資料，並將中XMP繼資料匯入PDF檔案。

您可以使用實用程式服務XMP完成以下任務：

* 將中繼資料匯入PDF檔案。 （請參閱[將中繼資料匯入PDF檔案](xmp-utilities.md#importing-metadata-into-pdf-documents)。）
* 從PDF檔案匯出中繼資料。 （請參閱[從PDF檔案匯出中繼資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)）。

>[!NOTE]
>
>有關實用程式服XMP務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 將中繼資料匯入PDF檔案{#importing-metadata-into-pdf-documents}

您可以使用XMP公用程式Java和web service API，以程式設計方式將中XMP繼資料匯入PDF檔案。 中繼資料提供有關PDF檔案的資訊，例如檔案的作者和與檔案相關的關鍵字。 中繼資料可位於檔案的「檔案屬性」對話方塊中，如下圖所示。

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

若要以程式設計方式將中繼資料匯入PDF檔案，您可以使用指定中繼資料值的現有XML檔案，或使用類型`XMPUtilityMetadata`的物件。 (請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

>[!NOTE]
>
>本節討論如何使用XML檔案將中繼資料匯入PDF檔案。

下列XML程式碼包含與上圖對應的中繼資料值。 例如，請注意指定關鍵字的粗體項目。

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
>有關實用程式服XMP務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

若要將XMP中繼資料匯入PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立XMPUtilityService用戶端。
1. 叫用中XMP繼資料匯入作業。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立XMPUtilityService客戶端**

您必須先建立XMPUtilityService客戶端，XMP才能以寫程式方式執行實用程式操作。 使用Java API，您可建立`XMPUtilityServiceClient`物件來完成此作業。 使用web service API，這是使用`XMPUtilityServiceService`物件來完成的。

**叫用中XMP繼資料匯入作業**

建立服務用戶端後，您可以叫用其中一個中繼XMP資料匯入作業，將中繼資料XMP匯入指定的PDF檔案。

**另請參閱**

[使用XMPJava API匯入中繼資料](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用XMPweb service API匯入中繼資料](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用XMPJava API {#import-xmp-metadata-using-the-java-api}匯入中繼資料

使用XMP公用程式API(Java)XMP匯入中繼資料：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar檔案包含可讓您以程式設計方式叫用公用程式XMP服務的類別。

1. 建立XMPUtilityService客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`XMPUtilityServiceClient`對象。

1. 叫用中XMP繼資料匯入作業

   若要修XMP改中繼資料，請叫用`XMPUtilityServiceClient`物件的`importMetadata`方法或其`importXMP`方法。

   如果您使用`importMetadata`方法，請傳入下列值：

   * 代表PDF檔案的`com.adobe.idp.Document`物件。
   * `XMPUtilityMetadata`物件，包含要匯入的中繼資料。

   如果您使用`importXMP`方法，請傳入下列值：

   * 代表PDF檔案的`com.adobe.idp.Document`物件。
   * `com.adobe.idp.Document`物件，代表包含要匯入之中繼資料的XML檔案。

   無論何種情況，傳回的值都是`com.adobe.idp.Document`物件，代表包含新匯入中繼資料的PDF檔案。 然後，可以將此對象保存到磁碟。

**另請參閱**

[將中繼資料匯入PDF檔案](xmp-utilities.md#importing-metadata-into-pdf-documents)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用XMPweb service API {#importing-xmp-metadata-using-the-web-service-api}匯入中繼資料

若要使用公用程XMP式網站服務XMPAPI以程式設計方式匯入中繼資料，請執行下列工作：

1. 包含專案檔案

   * 建立一個Microsoft .NET客戶端元件，該元件將使XMP用實用程式服務WSDL檔案。 (請參閱[使用Base64編碼叫用AEM Forms。)](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
   * 參考Microsoft .NET客戶端元件。 （請參閱[建立使用Base64編碼的。NET客戶端元件。）](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

1. 建立XMPUtilityService客戶端

   使用proxy類別建構函式建立`XMPUtilityServiceService`物件。

1. 叫用中XMP繼資料匯入作業

   若要修XMP改中繼資料，請叫用`XMPUtilityServiceService`物件的`importMetadata`方法或其`importXMP`方法。

   如果您使用`importMetadata`方法，請傳入下列值：

   * 代表PDF檔案的`BLOB`物件。
   * `XMPUtilityMetadata`物件，包含要匯入的中繼資料。

   如果您使用`importXMP`方法，請傳入下列值：

   * 代表PDF檔案的`BLOB`物件。
   * `BLOB`物件，代表包含要匯入之中繼資料的XML檔案。

   無論何種情況，傳回的值都是`BLOB`物件，代表包含新匯入中繼資料的PDF檔案。 然後，可以將此對象保存到磁碟。

**另請參閱**

[將中繼資料匯入PDF檔案](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 從PDF檔案匯出中繼資料{#exporting-metadata-from-pdf-documents}

您可以使用XMP公用程式Java和web service API，以程式設計方式擷取並儲XMP存PDF檔案的中繼資料。

>[!NOTE]
>
>有關實用程式服XMP務的詳細資訊，請參閱[AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}摘要

若要從XMPPDF檔案匯出中繼資料，請執行下列步驟：

1. 包含專案檔案。
1. 建立XMPUtilityService用戶端。
1. 叫用中XMP繼資料匯出作業。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

**建立XMPUtilityService客戶端**

您必須先建立XMPUtilityService客戶端，XMP才能以寫程式方式執行實用程式操作。 使用Java AP，如果通過建立`XMPUtilityServiceClient`對象來完成此操作。 使用web service API，這是使用`XMPUtilityServiceService`物件來完成的。

**叫用中XMP繼資料匯出作業**

建立服務客戶端後，可以調用其中一XMP個元資料導出操作，該操作可用於檢查元XMP資料或將其保存到磁碟。

**另請參閱**

[使用XMPJava API匯入中繼資料](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用XMPweb service API匯入中繼資料](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用XMPJava API {#export-xmp-metadata-using-the-java-api}匯出中繼資料

使用XMP公用程式APIXMP(Java)匯出中繼資料：

1. 包含專案檔案

   在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar檔案包含可讓您以程式設計方式叫用公用程式XMP服務的類別。

1. 建立XMPUtilityService客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`XMPUtilityServiceClient`對象。

1. 叫用中XMP繼資料匯入作業

   若要檢XMP查中繼資料，請叫用`XMPUtilityServiceClient`物件的`exportMetadata`方法，並傳入代表PDF檔案的`com.adobe.idp.Document`物件。 該方法返回包含檢索到的元資料的`XMPUtilityMetadata`對象。

   若要擷取並儲XMP存中繼資料，請叫用`XMPUtilityServiceClient`物件的`exportXMP`方法，並傳入代表PDF檔案的`com.adobe.idp.Document`物件。 該方法返回包含檢索到的元資料的`com.adobe.idp.Document`對象，您隨後可將其另存為XML檔案。

**另請參閱**

[從PDF檔案匯出中繼資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[包含AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用XMPweb service API {#export-xmp-metadata-using-the-web-service-api}匯出中繼資料

使用XMP公用程式APIXMP(web service)匯出中繼資料：

1. 包含專案檔案

   * 建立一個Microsoft .NET客戶端元件，該元件將使XMP用實用程式服務WSDL檔案。
   * 參考Microsoft .NET客戶端元件。

1. 建立XMPUtilityService客戶端

   使用proxy類別建構函式建立`XMPUtilityServiceService`物件。

1. 叫用中XMP繼資料匯入作業

   若要檢XMP查中繼資料，請叫用`XMPUtilityServiceClient`物件的`exportMetadata`方法，並傳入代表PDF檔案的`BLOB`物件。 該方法返回包含檢索到的元資料的`XMPUtilityMetadata`對象。

   若要擷取並儲XMP存中繼資料，請叫用`XMPUtilityServiceClient`物件的`exportXMP`方法，並傳入代表PDF檔案的`BLOB`物件。 該方法返回包含檢索到的元資料的`BLOB`對象，您隨後可將其另存為XML檔案。

**另請參閱**

[從PDF檔案匯出中繼資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
