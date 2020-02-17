---
title: Barcoded Forms服務
seo-title: 使用AEM Forms Barcoded Forms服務
description: '使用AEM Forms Barcoded Forms服務，從條碼的電子影像擷取資料。 '
seo-description: '使用AEM Forms Barcoded Forms服務，從條碼的電子影像擷取資料。 '
uuid: b044a788-0e4a-4718-b71a-bd846933d51b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: d431c4cb-e4be-41a5-8085-42393d4d468c
docset: aem65
translation-type: tm+mt
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# Barcoded Forms服務{#barcoded-forms-service}

## 概覽 {#overview}

Barcoded Forms服務從條形碼的電子影像中提取資料。 該服務接受包含一個或多個條形碼的TIFF和PDF檔案作為輸入，並提取條形碼資料。 條碼資料可以使用多種方式進行格式化，包括XML、分隔字串或使用JavaScript建立的任何自訂格式。

Barcoded Forms服務支援下列二 **維(2D)符號** ，這些符號是掃描的TIFF或PDF檔案所提供：

* PDF417
* 資料矩陣
* QR Code

此服務也支援下列 **一維條碼符號** ，這些條碼符號是掃描的TIFF或PDF檔案提供：

* 科達巴爾
* Code128
* 代碼3（共9個）
* EAN13
* EAN8

您可以使用Barcoded Forms服務完成下列工作：

* 從條碼影像（TIFF或PDF）擷取條碼資料。 資料會儲存為分隔文字。
* 將分隔文字資料轉換為XML（XDP或XFDF）。 XML資料比分隔文字更容易剖析。 此外，XDP或XFDF格式的資料可用作AEM Forms中其他服務的輸入。

對於影像中的每個條形碼，Barcoded Forms服務會定位條形碼、對其進行解碼並提取資料。 服務在XML文檔的內容元素中返回條形碼資料（在需要時使用實體編碼）。 例如，下清單格的掃描TIFF影像包含兩個條碼：

![示例](assets/example.png)

Barcoded Forms服務在解碼條形碼後返回以下XML文檔：

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<xb:scanned_image xmlns:xb="https://decoder.barcodedforms.adobe.com/xmlbeans"     path="tiff" version="1.0"> 
    <xb:decode> 
        <xb:date>2007-05-11T15:07:49.965-04:00</xb:date>  
        <xb:host_name>myhost.adobe.com</xb:host_name>  
        <xb:status type="success"> 
            <xb:message />  
        </xb:status> 
    </xb:decode> 
    <xb:barcode id="1"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.78445125" />  
                    <xb:point x="0.119526625" y="0.78445125" />  
                </xb:coordinates> 
            </xb:location> 
        </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_SID t_FirstName t_MiddleName t_LastName t_nFirstName t_nMiddleName t_nLastName 90210 Patti Y Penne Patti P Prosciutto</xb:content>  
        </xb:body> 
    </xb:barcode> 
    <xb:barcode id="2"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.825" />  
                    <xb:point x="0.44457594" y="0.825" />  
                    <xb:point x="0.44457594" y="0.9167683" />  
                    <xb:point x="0.119526625" y="0.9167683" />  
                </xb:coordinates> 
            </xb:location> 
         </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_FormType t_FormVersion ChangeName 20061128</xb:content>  
         </xb:body> 
    </xb:barcode> 
</xb:scanned_image>
```

## 服務注意事項 {#considerations}

### 使用條碼表單的工作流程 {#workflows-that-use-barcoded-forms}

表單作者使用設計工具建立互動式條碼表單。 (請參 [閱設計人員說明](https://www.adobe.com/go/learn_aemforms_designer_63)。)當使用者使用Adobe Reader或Acrobat填寫條碼表格時，會自動更新條碼以編碼表格資料。

Barcoded Forms服務對於將紙本上的資料轉換為電子格式非常有用。 例如，當填入並列印條形碼表格時，可掃描列印的復本並用作Barcoded Forms服務的輸入。

監視的資料夾端點通常用來啟動使用Barcoded Forms服務的應用程式。 例如，檔案掃描器可將條碼表單的TIFF或PDF影像儲存在受監視的檔案夾中。 受監視的資料夾端點將影像傳送至服務以進行解碼。

### 建議的編碼和解碼格式 {#recommended-encoding-and-decoding-formats}

建議條形碼表單作者在以條形碼編碼資料時，使用簡單、分隔的格式（例如Tab分隔）。 此外，請避免使用歸位字元作為欄位分隔字元。 設計人員提供一系列分隔編碼，可自動產生JavaScript指令碼以編碼條碼。 解碼資料具有第一行上的欄位名稱和第二行上的值，每個欄位之間有制表符。

解碼條形碼時，請指定用於分隔欄位的字元。 為解碼指定的字元必須與用於編碼條形碼的字元相同。 例如，在使用建議的Tab分隔格式時，「擷取至XML」運算必須使用Tab的預設值作為欄位分隔字元。

### 用戶指定的字元集 {#user-specified-character-sets}

當表單作者使用設計工具將條形碼對象添加到表單時，他們可以指定字元編碼。 識別的編碼為UTF-8、ISO-8859-1、ISO-8859-2、ISO-8859-7、Shift-JIS、KSC-5601、Big-Five、GB-2312、UTF-16。 依預設，所有資料都會以UTF-8編碼為條碼。

解碼條形碼時，可以指定要使用的字元集編碼。 為確保所有資料都正確解碼，請指定與表單作者在設計表單時指定的相同字元集。

### API限制 {#api-limitations}

當您使用BCF API時，請考慮下列限制：

* 不支援動態表單。
* 互動式表單無法正確解碼，除非已平面化。
* 1-D條碼只能包含英數字元值（如果支援）。 不解碼包含特殊符號的1-D條形碼。

### 其他限制 {#other-limitations}

此外，在使用Barcoded Forms服務時，請考慮下列限制：

* 本服務完全支援使用Adobe Reader或Acrobat儲存的AcroForms和包含2D條碼的靜態表單。 不過，對於1D條形碼，請平面化表單或以掃描的PDF或TIFF檔案形式提供。
* 動態XFA表格未完全支援。 若要以動態格式正確解碼1D和2D條碼，請將表格平面化或以掃描的PDF或TIFF檔案形式提供。

此外，如果遵守上述限制，服務可解碼使用支援條碼的任何條碼。 如需如何建立互動式條碼表單的詳細資訊，請參閱設計 [人員說明](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 配置服務的屬性 {#configureproperties}

您可以使用 **AEM Console中的AEMFD Barcoded Forms** Service來設定此服務的屬性。 AEM主控台的預設URL為 `https://[host]:[port]/system/console/configMgr`。

## 使用服務 {#using}

Barcoded Forms service提供下列兩個API:

* **[decode](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:解碼輸入PDF檔案或tiff影像中所有可用的條碼。 它返回另一個XML文檔，該文檔包含從輸入文檔或影像中所有可用的條形碼檢索到的資料。

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:將使用解碼API解碼的資料轉換為XML資料。 此XML資料可與XFA表單合併。 它會傳回XML檔案清單，每個條碼各一份。

### 將BCF服務與JSP或Servlet一起使用 {#using-bcf-service-with-a-jsp-or-servlets}

下列范常式式碼會解碼檔案中的條碼，並將輸出的XML儲存至磁碟。

```java
<%@ page import="java.util.List,
                com.adobe.fd.bcf.api.BarcodedFormsService,
                com.adobe.fd.bcf.api.CharSet,
                com.adobe.fd.bcf.api.Delimiter,
                com.adobe.fd.bcf.api.XMLFormat,
                com.adobe.aemfd.docmanager.Document,
                javax.xml.transform.Transformer,
                javax.xml.transform.TransformerFactory,
                java.io.StringWriter,
                javax.xml.transform.stream.StreamResult,
                javax.xml.transform.dom.DOMSource,
                javax.servlet.jsp.JspWriter,
                org.apache.commons.lang.StringEscapeUtils" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to BarcodedForms OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 BarcodedFormsService bcfService = sling.getService(BarcodedFormsService.class);

 // Path to image containing barcodes in AEM repository. 
 // Replace this with path to image in your repository
 String documentPath = "/content/dam/TestImage-010.tif";

 // Create a Docmanager Document object for 
 // the tiff file containing barcode
 // Please see Docmanager Document javadoc for
 // more details
 Document inputDoc = new Document(documentPath);

 // Invoke decode operation of barcoded forms service 
 // Second parameter is set to true to decode PDF417 barcode symbology
 // Please see javadoc for details of parameters

 org.w3c.dom.Document result = bcfService.decode(inputDoc, // Input Document Object
                                                    true, 
                                                    false,  
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    CharSet.UTF_8);// use UTF-8 character encoding 

 out.println("<h2> Output Returned from decode operation </h2>");
 printDoc(result,out);

 // Invoke extractToXML to convert Carriage 
 // return / Tab delimited data to XML 

 List<org.w3c.dom.Document> listResult = bcfService.extractToXML(result, // w3c document from the output of decode operation
                                                                    Delimiter.Carriage_Return, // Lines are separated using "\r"
                                                                    Delimiter.Tab, // Fields are separated using "\t" 
                                                                    XMLFormat.XDP); // wraps generated XML in <xdp:xdp> packet

 out.println("<h2> Output returned from extractToXML </h2>");
 printDoc(listResult.get(0),out);

%><%!

 // helper function to convert w3c document to string

 String convertToString(org.w3c.dom.Document inputDoc) throws Exception {
   TransformerFactory tf = TransformerFactory.newInstance();
   Transformer tr = tf.newTransformer();
   StringWriter sw = new StringWriter();
   StreamResult sr = new StreamResult(sw);
   tr.transform(new DOMSource(inputDoc), sr);
   return sw.toString();
 }

 // helper function to render XML to response

 void printDoc(org.w3c.dom.Document inputDoc,JspWriter out) throws Exception {
   String escapedString = StringEscapeUtils.escapeHtml(convertToString(inputDoc));
   out.println(escapedString);
 }

%>
```

### 搭配AEM工作流程使用BCF服務 {#using-the-bcf-service-with-aem-workflows}

從工作流中運行Barcoded Forms服務類似於從JSP/Servlet運行服務。 唯一的區別是從JSP/Servlet運行服務，文檔對象會自動從ResourceResolverHelper對象中檢索ResourceResolver對象的實例。 從工作流程呼叫程式碼時，此自動機制無法運作。

對於工作流，將ResourceResolver對象的實例顯式傳遞到Document類建構子。 然後，Document對象使用提供的ResourceResolver對象從儲存庫讀取內容。

下面的示例工作流進程對文檔中的條形碼進行解碼並將結果保存到磁碟。 程式碼會寫入ECMAScript，檔案會以工作流程裝載的形式傳遞：

```
/*
 * Imports 
 */
var BarcodedFormsService = Packages.com.adobe.fd.bcf.api.BarcodedFormsService;
var CharSet = Packages.com.adobe.fd.bcf.api.CharSet;

var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var FileOutputStream = Packages.java.io.FileOutputStream;
var TransformerFactory = Packages.javax.xml.transform.TransformerFactory;
var Transformer = Packages.javax.xml.transform.Transformer;
var StreamResult = Packages.javax.xml.transform.stream.StreamResult;
var DOMSource = Packages.javax.xml.transform.dom.DOMSource;

var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to BarcodedFormsService
var bcfService = sling.getService(BarcodedFormsService);

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

// invoke decode operation to decode barcodes in inputDocument
var decodedBarcode = bcfService.decode(inputDocument, true, false, false, false, false, false, false, false, CharSet.UTF_8);

// save decoded barcode data to disk
saveW3CDocument(decodedBarcode, "C:/temp/decoded.xml");

/*
 * Helper function to save W3C Document
 * to a file on disk
 */
function saveW3CDocument(inputDoc, filePath) {
   var tf = TransformerFactory.newInstance();
   var tr = tf.newTransformer();
   var os = new FileOutputStream(filePath);
   var sr = new StreamResult(os);
   tr.transform(new DOMSource(inputDoc), sr);
   os.close();
}
```

