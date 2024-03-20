---
title: ConvertPDF服務
description: 使用Adobe Experience Manager Forms ConvertPDF服務將PDF檔案轉換為PostScript或影像檔案。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services
exl-id: 50c7a385-b56d-4573-932f-1f44eec948f8
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# ConvertPDF服務 {#convertpdf-service}

## 概觀 {#overview}

「轉換PDF」服務會將PDF檔案轉換為PostScript或影像檔案(JPEG、JPEG2000、PNG和TIFF)。 將PDF檔案轉換為PostScript對於任何PostScript印表機上的自動伺服器式列印很有用。 將PDF檔案轉換為多頁TIFF檔案對於在不支援PDF檔案的內容管理系統中封存檔案而言是切實可行的。

您可以使用轉換PDF服務來達到下列目的：

* 將PDF檔案轉換為PostScript。 轉換為PostScript時，您可以使用轉換作業來指定來原始檔，以及是否要轉換成PostScript第2級或第3級。 您轉換成PostScript檔案的PDF檔案必須是非互動式的。
* 將PDF檔案轉換為JPEG、JPEG2000、PNG和TIFF影像格式。 當轉換為任何這些影像格式時，您可以使用轉換作業來指定來原始檔和影像選項規格。 規格包含各種偏好設定，例如影像轉換格式、影像解析度和色彩轉換。

## 設定服務的屬性   {#properties}

您可以使用 **AEMFD ConvertPDF服務** 在AEM Console中設定此服務的屬性。 AEM主控台的預設URL為 `https://[host]:'port'/system/console/configMgr`.

## 使用服務 {#using-the-service}

ConvertPDF服務提供下列兩個API：

* **[toPS](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**：將PDF檔案轉換為PostScript檔案。

* **[toImage](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**：將PDF檔案轉換為影像檔案。 支援的影像格式為JPEG、JPEG2000、PNG和TIFF。

### 搭配JSP或Servlet使用toPS API {#using-tops-api-with-a-jsp-or-servlets}

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
 // replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript language
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### 搭配JSP或Servlet使用toImage API {#using-toimage-api-with-a-jsp-or-servlets}

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
 // replace this with path to your document
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

### 搭配AEM工作流程使用ConvertPDF服務 {#using-convertpdf-service-with-aem-workflows}

從工作流程執行ConvertPDF服務類似於從JSP/Servlet執行。

唯一的差別是從JSP/Servlet執行服務，檔案物件會自動從ResourceResolverHelper物件擷取ResourceResolver物件的執行個體。 從工作流程呼叫程式碼時，此自動機制無法運作。 對於工作流程，請將ResourceResolver物件的執行個體明確傳遞給Document類別建構函式。 接著，Document物件會使用提供的ResourceResolver物件來讀取存放庫中的內容。

下列範例工作流程程式會將輸入檔案轉換為PostScript檔案。 程式碼會以ECMAScript撰寫，而檔案會以工作流程裝載的方式傳遞：

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
