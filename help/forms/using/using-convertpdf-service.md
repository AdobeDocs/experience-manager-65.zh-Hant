---
title: ConvertPDF Service
seo-title: ConvertPDF Service
description: 使用AEM Forms ConvertPDF服務將PDF檔案轉換為PostScript或影像檔案。
seo-description: 使用AEM Forms ConvertPDF服務將PDF檔案轉換為PostScript或影像檔案。
uuid: 7fa94c8c-485b-4a77-bcd3-ed716e3cf316
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 5ec4f0ec-a9fd-4571-9b9a-278f4622c028
exl-id: 575bab27-d973-47fa-a0da-fa889cec6f27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# ConvertPDF服務{#convertpdf-service}

## 概覽 {#overview}

「轉換PDF」服務可將PDF文檔轉換為PostScript或影像檔案（JPEG、JPEG 2000、PNG和TIFF）。 將PDF文檔轉換為PostScript對於在任何PostScript打印機上基於伺服器的無人值守打印非常有用。 將PDF檔案轉換為多頁TIFF檔案，在不支援PDF檔案的內容管理系統中封存檔案時非常實用。

您可以使用「轉換PDF」服務來完成下列工作：

* 將PDF檔案轉換為PostScript。 轉換為PostScript時，可以使用轉換操作指定源文檔以及轉換為PostScript級別2或3。 轉換為PostScript檔案的PDF文檔必須是非互動式的。
* 將PDF文檔轉換為JPEG、JPEG 2000、PNG和TIFF影像格式。 轉換為任何這些影像格式時，可以使用轉換操作來指定源文檔和影像選項規範。 規範包含各種首選項，如影像轉換格式、影像解析度和顏色轉換。

## 配置服務的屬性   {#properties}

您可以在AEM Console中使用&#x200B;**AEMFD ConvertPDF服務**&#x200B;來設定此服務的屬性。 AEM控制台的預設URL為`https://[host]:'port'/system/console/configMgr`。

## 使用服務{#using-the-service}

ConvertPDF服務提供下列兩個API:

* **[toPS](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**:將PDF文檔轉換為PostScript檔案。

* **[toImage](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**:將PDF文檔轉換為影像檔案。支援的影像格式為JPEG、JPEG2000、PNG和TIFF。

### 搭配JSP或Servlet {#using-tops-api-with-a-jsp-or-servlets}使用toPS API

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToPSOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.PSLevel,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // please replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript langauge
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### 搭配JSP或Servlet {#using-toimage-api-with-a-jsp-or-servlets}使用toImage API

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToImageOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.ImageConvertFormat,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // please replace this with path to your document
 String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to image

 Document inputPDF = new Document(documentPath);

 // options object to pass to toImage API
 ToImageOptionsSpec toImageOptions = new ToImageOptionsSpec();

 // mandatory option to pass, image format
 toImageOptions.setImageConvertFormat(ImageConvertFormat.JPEG);

 // invoke toImage method to convert inputPDF to Image
 List<Document> convertedImages = cpdfService.toImage(inputPDF, toImageOptions);

 // save converted image files to disk
 for(int i=0;i<convertedImages.size();i++){
     Document pageImage = convertedImages.get(i);
     pageImage.copyToFile(new File("C:/temp/out_"+(i+1)+".jpeg"));
 }

%>
```

### 將ConvertPDF服務與AEM工作流程搭配使用{#using-convertpdf-service-with-aem-workflows}

從工作流運行ConvertPDF服務與從JSP/Servlet運行類似。

唯一的差異是從JSP/Servlet運行服務，文檔對象會自動從ResourceResolverHelper對象中檢索ResourceResolver對象的實例。 這個自動機
從工作流程呼叫程式碼時無法運作。 對於工作流，將ResourceResolver對象的實例顯式傳遞到Document類建構子。 然後，文檔對象使用
已提供ResourceResolver物件，可從存放庫讀取內容。

以下工作流進程示例將輸入文檔轉換為PostScript文檔。 程式碼會寫入ECMAScript中，而檔案會以工作流程裝載的形式傳遞：

```javascript
/*
 * Imports
 */
var ConvertPdfService = Packages.com.adobe.fd.cpdf.api.ConvertPdfService;
var ToPSOptionsSpec = Packages.com.adobe.fd.cpdf.api.ToPSOptionsSpec;
var PSLevel = Packages.com.adobe.fd.cpdf.api.enumeration.PSLevel;
var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to ConvertPdfService
var cpdfService = sling.getService(ConvertPdfService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from
 * crx repository.
 */

/* get ResourceResolverFactory service reference , used
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path
var inputDocument = new Document(payload_path, resourceResolver);

// options object to be passed to toPS operation
var toPSOptions = new ToPSOptionsSpec();

// Set PostScript Language Three
toPSOptions.setPsLevel(PSLevel.LEVEL_3);

// invoke toPS operation to convert inputDocument to PS
var convertedPS = cpdfService.toPS(inputDocument, toPSOptions);

// save converted PostScript file to disk
convertedPS.copyToFile(new File("C:/temp/out.ps"));
```
