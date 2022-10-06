---
title: 條碼式Forms服務
seo-title: Using AEM Forms Barcoded Forms Service
description: 使用AEM Forms Barcoded Forms服務從條碼的電子影像中擷取資料。
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
ht-degree: 0%

---

# 條碼式Forms服務{#barcoded-forms-service}

## 總覽 {#overview}

條碼式Forms服務從條碼的電子影像中擷取資料。 該服務接受包括一個或多個條形碼的TIFF和PDF檔案作為輸入，並提取條形碼資料。 條碼資料可以以多種方式格式化，包括XML、分隔字串或使用JavaScript建立的任何自訂格式。

Barcoded Forms服務支援下列項目 **二維(2D)** 作為掃描TIFF或PDF文檔提供的符號：

* PDF417
* 資料矩陣
* QR碼

此服務也支援下列功能 **一維** 作為掃描TIFF或PDF文檔提供的符號：

* 科達巴爾
* Code128
* 代碼3（共9）
* EAN13
* EAN8

您可以使用條碼式Forms服務來完成下列工作：

* 從條形碼影像(TIFF或PDF)中提取條形碼資料。 資料會以分隔文字的形式儲存。
* 將分隔文字資料轉換為XML（XDP或XFDF）。 XML資料比分隔文字更容易剖析。 此外，XDP或XFDF格式的資料可作為AEM Forms中其他服務的輸入。

對於影像中的每個條形碼，條形碼Forms服務將定位條形碼，對其進行解碼，並提取資料。 該服務在XML文檔的內容元素中返回條形碼資料（在需要時使用實體編碼）。 例如，下清單單的掃描TIFF影像包含兩個條碼：

![範例](assets/example.png)

條碼式Forms服務在解碼條碼後傳回下列XML檔案：

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

## 服務的考量事項 {#considerations}

### 使用條碼式表單的工作流程 {#workflows-that-use-barcoded-forms}

表單作者可使用Designer建立互動式條碼表單。 (請參閱 [設計工具說明](https://www.adobe.com/go/learn_aemforms_designer_63).) 當使用者使用Adobe Reader或Acrobat填入條碼式表單時，條碼會自動更新，以編碼表單資料。

Barcoded Forms服務用於將紙上存在的資料轉換為電子格式。 例如，當填寫和打印條碼式表單時，可以掃描打印的副本並用作條碼式Forms服務的輸入。

觀看的資料夾端點通常用於啟動使用條碼式Forms服務的應用程式。 例如，檔案掃描器可將條碼式表單的TIFF或PDF影像儲存在已觀看的資料夾中。 觀看的資料夾端點會將影像傳遞至服務進行解碼。

### 建議的編碼和解碼格式 {#recommended-encoding-and-decoding-formats}

在條碼中編碼資料時，建議條碼格式作者使用簡單的分隔格式（例如以Tab分隔）。 此外，請避免使用歸位作為欄位分隔字元。 Designer提供一系列分隔編碼，可自動產生JavaScript指令碼來編碼條碼。 解碼資料在第一行上具有欄位名稱，在第二行上具有其值，每個欄位之間具有標籤。

解碼條形碼時，請指定用於分隔欄位的字元。 為解碼指定的字元必須與用於編碼條形碼的字元相同。 例如，使用建議的Tab分隔格式時，「提取到XML」操作必須使用Tab的預設值作為欄位分隔符。

### 用戶指定的字元集 {#user-specified-character-sets}

當表單作者使用Designer將條碼物件新增至其表單時，可指定字元編碼。 認可的編碼為UTF-8、ISO-8859-1、ISO-8859-2、ISO-8859-7、Shift-JIS、KSC-5601、Big-Five、GB-2312、UTF-16。 依預設，所有資料都以條碼編碼為UTF-8。

解碼條形碼時，可以指定要使用的字元集編碼。 為保證所有資料都正確解碼，請指定與表單作者在設計表單時指定的字元集相同。

### API限制 {#api-limitations}

使用BCF API時，請考量下列限制：

* 不支援動態表單。
* 除非將互動式表單平面化，否則這些表單無法正確解碼。
* 1-D條形碼只能包含英數字元值（如果支援）。 不解碼包含特殊符號的1-D條形碼。

### 其他限制 {#other-limitations}

此外，使用條碼式Forms服務時，請考量下列限制：

* 此服務完全支援包含使用Adobe Reader或Acrobat儲存之2D條碼的AcroForms和靜態表單。 但是，對於1D條形碼，可以平面化表單，或作為掃描PDF或TIFF文檔提供。
* 動態XFA表單未完全支援。 要以動態形式正確解碼1D和2D條形碼，請平面化表單，或將其作為掃描PDF或TIFF文檔提供。

此外，如果發現上述限制，則服務可以解碼使用支援的條碼符號的任何條形碼。 如需如何建立互動式條碼式表單的詳細資訊，請參閱 [設計工具說明](https://www.adobe.com/go/learn_aemforms_designer_63).

## 配置服務的屬性   {#configureproperties}

您可以使用 **AEMFD條碼式Forms服務** 在AEM Console中設定此服務的屬性。 AEM控制台的預設URL為 `https://[host]:'port'/system/console/configMgr`.

## 使用服務 {#using}

條碼式Forms服務提供下列兩個API:

* **[解碼](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:對輸入PDF文檔或Tiff影像中可用的所有條形碼進行解碼。 它返回另一個XML文檔，該文檔包含從輸入文檔或影像中可用的所有條形碼中檢索到的資料。

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:將使用解碼API解碼的資料轉換為XML資料。 此XML資料可與XFA表單合併。 它返回XML文檔的清單，每個條碼各一個。

### 搭配JSP或Servlet使用BCF服務 {#using-bcf-service-with-a-jsp-or-servlets}

以下示例代碼將文檔中的條形碼解碼，並將輸出XML保存到磁碟。

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

### 搭配AEM工作流程使用BCF服務 {#using-the-bcf-service-with-aem-workflows}

從工作流程執行條碼式Forms服務類似於從JSP/Servlet執行服務。 唯一的差異是從JSP/Servlet運行服務，文檔對象會自動從ResourceResolverHelper對象中檢索ResourceResolver對象的實例。 從工作流程呼叫程式碼時，此自動機制無法運作。

對於工作流，將ResourceResolver對象的實例顯式傳遞到Document類建構子。 然後，Document物件會使用提供的ResourceResolver物件來從存放庫讀取內容。

以下示例工作流進程會解碼文檔中的條形碼並將結果保存到磁碟。 程式碼會寫入ECMAScript中，而檔案會以工作流程裝載的形式傳遞：

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
