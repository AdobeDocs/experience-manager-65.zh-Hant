---
title: 巴克德Forms局
seo-title: Using AEM Forms Barcoded Forms Service
description: 使用AEM Forms·巴克德·Forms服務從條形碼的電子影像中提取資料。
seo-description: Use AEM Forms Barcoded Forms service to extract data from electronic images of barcodes.
uuid: b044a788-0e4a-4718-b71a-bd846933d51b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: d431c4cb-e4be-41a5-8085-42393d4d468c
docset: aem65
exl-id: edaf12be-473f-4175-b4e0-549b41159a55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# 巴克德Forms局{#barcoded-forms-service}

## 概觀 {#overview}

條形碼Forms服務從條形碼的電子影像中提取資料。 該服務接受包括一個或多個條形碼的TIFF和PDF檔案作為輸入，並提取條形碼資料。 條形碼資料可以採用多種方式進行格式化，包括XML、分隔字串或使用JavaScript建立的任何自定義格式。

BarcodedForms服務支援以下 **二維(2D)** 作為掃描TIFF或PDF文檔提供的符號：

* PDF417
* 資料矩陣
* QR碼

該服務還支援以下 **一維** 作為掃描TIFF或PDF文檔提供的符號：

* 科達巴爾
* Code128
* 代碼3（共9）
* EAN13
* EAN8

您可以使用BarcodedForms服務完成以下任務：

* 從條形碼影像(TIFF或PDF)中提取條形碼資料。 資料以分隔文本的形式儲存。
* 將分隔的文本資料轉換為XML（XDP或XFDF）。 XML資料比分隔文本更容易分析。 此外，XDP或XFDF格式的資料可用作AEM Forms其他服務的輸入。

對於影像中的每個條形碼，BarcodedForms服務會定位條形碼，對其進行解碼，並提取資料。 該服務返回XML文檔的內容元素中的條形碼資料（在需要時使用實體編碼）。 例如，以下表單的掃描TIFF影像包含兩個條形碼：

![示例](assets/example.png)

條形碼Forms服務在解碼條形碼後返回以下XML文檔：

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

### 使用條形碼表單的工作流 {#workflows-that-use-barcoded-forms}

表單作者使用設計器建立互動式條形碼表單。 (請參閱 [設計器幫助](https://www.adobe.com/go/learn_aemforms_designer_63_tw)。) 當用戶使用Adobe Reader或Acrobat填充條形碼表單時，條形碼會自動更新以編碼表單資料。

BarcodedForms服務用於將紙上資料轉換為電子格式。 例如，當填寫和打印條形碼表格時，可掃描打印的副本並將其用作BarcodedForms服務的輸入。

受監視的資料夾終結點通常用於啟動使用BarcodedForms服務的應用程式。 例如，文檔掃描程式可以將條形碼表單的TIFF或PDF影像保存在監視資料夾中。 受監視的資料夾終結點將影像傳遞給服務以進行解碼。

### 建議的編碼和解碼格式 {#recommended-encoding-and-decoding-formats}

鼓勵條形碼表單的作者在用條形碼對資料進行編碼時使用簡單、分隔的格式（例如制表符分隔）。 另外，避免使用回車作為欄位分隔符。 設計器提供了一組分隔的編碼，這些編碼可自動生成JavaScript指令碼以編碼條形碼。 解碼資料具有第一行上的欄位名稱和第二行上的欄位值，每個欄位之間有制表符。

解碼條形碼時，指定用於分隔欄位的字元。 為解碼指定的字元必須與用於編碼條形碼的字元相同。 例如，在使用建議的制表符分隔格式時，「提取到XML」操作必須使用Tab作為欄位分隔符的預設值。

### 用戶指定的字元集 {#user-specified-character-sets}

當表單作者使用設計器將條形碼對象添加到其表單時，他們可以指定字元編碼。 識別的編碼是UTF-8、ISO-8859-1、ISO-8859-2、ISO-8859-7、Shift-JIS、KSC-5601、Big-Five、GB-2312、UTF-16。 預設情況下，所有資料都以條形碼編碼為UTF-8。

在解碼條形碼時，可以指定要使用的字元集編碼。 為確保正確解碼所有資料，請指定在設計表單時表單作者指定的相同字元集。

### API限制 {#api-limitations}

使用BCF API時，請考慮以下限制：

* 不支援動態表單。
* 除非將交互表單拼合，否則無法正確解碼這些表單。
* 1-D條形碼必須只包含字母數字值（如果支援）。 不解碼包含特殊符號的一維條形碼。

### 其他限制 {#other-limitations}

另外，使用BarcodedForms服務時，請考慮以下限制：

* 該服務完全支援包含使用Adobe Reader或Acrobat保存的2D條形碼的AcroForms和靜態表單。 但是，對於1D條形碼，請拼合表單或將其作為PDF或TIFF文檔提供。
* 不完全支援動態XFA表單。 要以動態形式正確解碼1D和2D條形碼，請拼合該格式或將其作為掃描PDF或TIFF文檔提供。

此外，如果發現上述限制，該服務可以解碼使用支援的符號的任何條形碼。 有關如何建立互動式條形碼表單的詳細資訊，請參見 [設計器幫助](https://www.adobe.com/go/learn_aemforms_designer_63_tw)。

## 配置服務的屬性   {#configureproperties}

您可以使用 **AEMFD條形碼Forms服務** 在控AEM制台中配置此服務的屬性。 控制台的預設AEMURL為 `https://[host]:'port'/system/console/configMgr`。

## 使用服務 {#using}

條形碼Forms服務提供以下兩個API:

* **[解碼](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:對輸入PDF文檔或tiff影像中可用的所有條形碼進行解碼。 它返回另一個XML文檔，該文檔包含從輸入文檔或影像中所有可用的條形碼檢索到的資料。

* **[抽取到XML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:將使用解碼API解碼的資料轉換為XML資料。 此XML資料可以與XFA表單合併。 它返回XML文檔清單，每個條形碼一個。

### 將BCF服務與JSP或Servlet一起使用 {#using-bcf-service-with-a-jsp-or-servlets}

下面的示例代碼對文檔中的條形碼進行解碼並將輸出XML保存到磁碟。

```jsp
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

### 將BCF服務與工作流AEM一起使用 {#using-the-bcf-service-with-aem-workflows}

從工作流運行BarcodedForms服務與從JSP/Servlet運行服務類似。 唯一的區別是從JSP/Servlet運行服務，文檔對象會自動從ResourceResolverHelper對象中檢索ResourceResolver對象的實例。 當從工作流調用代碼時，此自動機制不起作用。

對於工作流，將ResourceResolver對象的實例顯式傳遞給Document類建構子。 然後，Document對象使用提供的ResourceResolver對象從儲存庫讀取內容。

下面的示例工作流進程解碼文檔中的條形碼並將結果保存到磁碟。 代碼以ECMAScript編寫，文檔作為工作流負載傳遞：

```javascript
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
