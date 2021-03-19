---
title: 使用Web Services叫用AEM Forms
seo-title: 使用Web Services叫用AEM Forms
description: 使用網頁服務來叫用AEM Forms程式，並完整支援WSDL產生。
seo-description: 使用網頁服務來叫用AEM Forms程式，並完整支援WSDL產生。
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '10005'
ht-degree: 0%

---


# 使用Web服務調用AEM Forms{#invoking-aem-forms-using-web-services}

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

服務容器中的大多數AEM Forms服務都配置為公開Web服務，完全支援Web服務定義語言(WSDL)生成。 也就是說，您可以建立使用AEM Forms服務之原生SOAP堆疊的Proxy物件。 因此，AEM Forms服務可以交換和處理以下SOAP消息：

* **SOAP請求**:由要求動作的用戶端應用程式傳送至Forms服務。
* **SOAP響應**:在處理SOAP請求後，由Forms服務傳送至用戶端應用程式。

使用web services，您可以執行與使用Java API相同的AEM Forms服務操作。 使用web services來叫用AEM Forms服務的好處在於，您可以在支援SOAP的開發環境中建立用戶端應用程式。 用戶端應用程式不會與特定開發環境或程式設計語言相連結。 例如，您可以使用Microsoft Visual Studio .NET和C#作為寫程式語言來建立客戶端應用程式。

AEM Forms服務是透過SOAP通訊協定公開的，並符合WSI Basic Profile 1.1規範。 Web Services Interoperability(WSI)是開放標準組織，可促進跨平台的Web服務互操作性。 如需詳細資訊，請參閱[https://www.ws-i.org/](https://www.ws-i.org)。

AEM Forms支援下列Web服務標準：

* **編碼**:僅支援檔案和文字編碼（根據WSI基本設定檔，這是偏好的編碼）。(請參閱[使用Base64編碼叫用AEM Forms。)](#invoking-aem-forms-using-base64-encoding)
* **MTOM**:表示使用SOAP請求對附件進行編碼的方法。(請參閱[使用MTOM](#invoking-aem-forms-using-mtom)叫用AEM Forms。)
* **SwaRef**:表示使用SOAP請求對附件進行編碼的另一種方法。(請參閱[使用SwaRef](#invoking-aem-forms-using-swaref)叫用AEM Forms。)
* **帶附件的SOAP**:支援MIME和DIME（直接網際網路訊息封裝）。這些協定是通過SOAP發送附件的標準方法。 Microsoft Visual Studio .NET應用程式使用DIME。 (請參閱[使用Base64編碼叫用AEM Forms。)](#invoking-aem-forms-using-base64-encoding)
* **WS-安全性**:支援使用者名稱密碼Token設定檔，此為傳送使用者名稱和密碼的標準方式，是WS Security SOAP標題的一部分。AEM Forms也支援HTTP基本驗證。 （請參閱[使用WS-Security標頭](https://www.adobe.com/devnet/livecycle/articles/passing_credentials.html)傳遞憑證。）

若要使用Web服務來叫用AEM Forms服務，通常您會建立使用服務WSDL的代理程式庫。 *使用Web服務調用AEM Forms*&#x200B;部分使用JAX-WS建立Java代理類來調用服務。 （請參閱[使用JAX-WS](#creating-java-proxy-classes-using-jax-ws)建立Java代理類。）

您可以指定下列URL定義來擷取服務WDSL（方括弧中的項目是可選的）:

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

其中：

* *your_* serverhostst代表代管AEM Forms的J2EE應用程式伺服器的IP位址。
* *your_* port代表J2EE應用程式伺服器使用的HTTP連接埠。
* *service_* name表示服務名。
* *版* 本代表服務的目標版本（預設使用最新服務版本）。
* `async` 指定值， `true` 以啟用非同步調用的其 `false` 他操作（預設）。
* *lc_* version表示要調用的AEM Forms版本。

下表列出服務WSDL定義(假設AEM Forms部署在本機主機上，而貼文為8080)。

<table>
 <thead>
  <tr>
   <th><p>服務</p></th>
   <th><p>WSDL定義</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>組合器</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>備份和恢復</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>條形碼表格</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>轉換PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>DocConverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>檔案管理</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>加密 </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>表單</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>表單資料整合</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>產生PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>產生3D PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>輸出</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>PDF公用程式 </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Acrobat Reader DC擴充功能</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>存放庫</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>版權管理 </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>簽名 </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>公XMP用程式</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**AEM Forms進程WSDL定義**

必須在WSDL定義中指定應用程式名和進程名，才能訪問屬於在Workbench中建立的進程的WSDL。 假設應用程式的名稱為`MyApplication` ，進程的名稱為`EncryptDocument`。 在這種情況下，請指定以下WSDL定義：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>有關示例`MyApplication/EncryptDocument`短壽命進程的資訊，請參見[短壽命進程示例](/help/forms/developing/aem-forms-processes.md)。

>[!NOTE]
>
>應用程式可以包含資料夾。 在這種情況下，請在WSDL定義中指定資料夾名稱：

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**使用web services存取新功能**

可使用web services存取新的AEM Forms服務功能。 例如，在AEM Forms，引進了使用MTOM對附件進行編碼的能力。 (請參閱[使用MTOM](#invoking-aem-forms-using-mtom)叫用AEM Forms。)

若要存取AEM Forms引進的新功能，請在WSDL定義中指定`lc_version`屬性。 例如，若要存取新的服務功能（包括MTOM支援），請指定下列WSDL定義：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>設定`lc_version`屬性時，請確定您使用三位數。 例如，9.0.1等於9.0版。

**Web服務BLOB資料類型**

AEM Forms服務WSDL定義了許多資料類型。 Web服務中公開的最重要資料類型之一是`BLOB`類型。 使用AEM FormsJava API時，此資料類型映射到`com.adobe.idp.Document`類。 (請參閱[使用Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)將資料傳遞至AEM Forms服務。)

`BLOB`物件會傳送及擷取二進位資料（例如PDF檔案、XML資料等）至AEM Forms服務。 `BLOB`類型在服務WSDL中定義如下：

```xml
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

`MTOM`和`swaRef`欄位僅在AEM Forms受支援。 只有指定包含`lc_version`屬性的URL時，才能使用這些新欄位。

**在服務請求中提供BLOB對象**

如果AEM Forms服務操作需要`BLOB`類型作為輸入值，請在應用程式邏輯中建立`BLOB`類型的實例。 (*Programming with forms*&#x200B;中的許多Web服務快速啟動都AEM顯示了如何使用BLOB資料類型。)

將值分配給屬於`BLOB`實例的欄位，如下所示：

* **Base64**:若要將資料傳遞為以Base64格式編碼的文字，請在欄位中設 `BLOB.binaryData` 定資料，並在欄位中以MIME格式(例如 `application/pdf`)設定資 `BLOB.contentType` 料類型。(請參閱[使用Base64編碼叫用AEM Forms。)](#invoking-aem-forms-using-base64-encoding)
* **MTOM**:若要在MTOM附件中傳遞二進位資料，請在欄位中設定 `BLOB.MTOM` 資料。此設定會使用Java JAX-WS架構或SOAP架構的原生API，將資料附加至SOAP要求。 (請參閱[使用MTOM](#invoking-aem-forms-using-mtom)叫用AEM Forms。)
* **SwaRef**:要在WS-I SwaRef附件中傳遞二進位資料，請在欄位中設定 `BLOB.swaRef` 資料。此設定會使用Java JAX-WS架構將資料附加至SOAP要求。 (請參閱[使用SwaRef](#invoking-aem-forms-using-swaref)叫用AEM Forms。)
* **MIME或DIME附件**:若要在MIME或DIME附件中傳送資料，請使用SOAP架構的原生API，將資料附加至SOAP要求。在`BLOB.attachmentID`欄位中設定附件標識符。 (請參閱[使用Base64編碼叫用AEM Forms。)](#invoking-aem-forms-using-base64-encoding)
* **遠端URL**:如果資料是裝載在網頁伺服器上，並可透過HTTP URL存取，請在欄位中設定HTTP  `BLOB.remoteURL` URL。(請參閱[使用HTTP](#invoking-aem-forms-using-blob-data-over-http)上的BLOB資料調用AEM Forms。)

**訪問從服務返回的BLOB對象中的資料**

返回的`BLOB`對象的傳輸協定取決於幾個因素，這些因素按以下順序考慮，當滿足主要條件時停止：

1. **目標URL指定傳輸協定**。如果在SOAP調用中指定的目標URL包含參數&#x200B;`blob="`*BLOB_TYPE*&quot;，則&#x200B;*BLOB_TYPE*&#x200B;將確定傳輸協定。 *BLOB_* TYPE是base64、dime、mime、http、mtom或swaref的預留位置。
1. **服務SOAP端點是Smart**。如果以下條件成立，則使用與輸入文檔相同的傳輸協定返回輸出文檔：

   * 服務的SOAP端點參數輸出Blob對象的預設協定設定為Smart。

      對於每個具有SOAP端點的服務，管理控制台允許您為任何返回的blob指定傳輸協定。 （請參閱[管理幫助](https://www.adobe.com/go/learn_aemforms_admin_63)。）

   * AEM Forms服務會以一或多份檔案為輸入。

1. **服務SOAP端點不是Smart**。配置的協定確定文檔傳輸協定，並且資料在相應的`BLOB`欄位中返回。 例如，如果SOAP端點設定為DIME，則返回的blob位於`blob.attachmentID`欄位中，而不管任何輸入文檔的傳輸協定如何。
1. **否則**。如果服務未將文檔類型作為輸入，則輸出文檔將在HTTP協定的`BLOB.remoteURL`欄位中返回。

如第一個條件所述，您可以通過以下方式擴展SOAP端點URL來確保任何返回文檔的傳輸類型：

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

以下是傳輸類型與從中獲取資料的欄位之間的關聯：

* **Base64格式**:將尾碼 `blob` 設定為 `base64` 以返回欄位中的 `BLOB.binaryData` 資料。
* **MIME或DIME附件**:將尾碼設 `blob` 置為 `DIME` 或 `MIME` 將資料作為相應的附件類型返回，並在欄位中返回附件標 `BLOB.attachmentID` 識符。使用SOAP架構的專有API讀取附件中的資料。
* **遠端URL**:將尾碼 `blob` 設定為 `http` 保留應用程式伺服器上的資料，並返回指向欄位中資料的URL `BLOB.remoteURL` 。
* **MTOM或SwaRef**:將尾碼設 `blob` 置為 `mtom` 或 `swaref` 將資料作為相應的附件類型返回，並在或欄位中返回附 `BLOB.MTOM` 件標 `BLOB.swaRef` 識符。使用SOAP架構的原生API讀取附件中的資料。

>[!NOTE]
>
>建議在調用`setBinaryData`方法填入`BLOB`對象時，不要超過30 MB。 否則，可能出現`OutOfMemory`例外。

>[!NOTE]
>
>使用MTOM傳輸通訊協定的JAX WS應用程式的已傳送和已接收資料限制為25MB。 此限制是由於JAX-WS中的錯誤。 如果您所傳送和接收檔案的總大小超過25MB，請使用SwaRef傳輸通訊協定，而非MTOM傳輸通訊協定。 否則，可能出現`OutOfMemory`例外。

**MTOM傳輸BASE64編碼位元組陣列**

除了`BLOB`物件外，MTOM通訊協定還支援任何複雜類型的位元組陣列參數或位元組陣列欄位。 這表示支援MTOM的用戶端SOAP架構可以傳送任何`xsd:base64Binary`元素作為MTOM附件（而非base64編碼文字）。 AEM FormsSOAP端點可以讀取此類位元組陣列編碼。 但是，AEM Forms服務始終會傳回位元組陣列類型，做為base64編碼文字。 輸出位元組陣列參數不支援MTOM。

傳回大量二進位資料的AEM Forms服務使用Document/BLOB類型，而非byte-array類型。 「檔案」類型在傳輸大量資料時更有效率。

## Web服務資料類型{#web-service-data-types}

下表列出Java資料類型並顯示相應的Web服務資料類型。

<table>
 <thead>
  <tr>
   <th><p>Java資料類型</p></th>
   <th><p>Web服務資料類型</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p><code>DATE</code>類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務操作將<code>java.util.Date</code>值作為輸入，則SOAP客戶端應用程式必須在<code>DATE.date</code>欄位中傳遞日期。 在本例中，設定<code>DATE.calendar</code>欄位會導致執行時期例外。 如果服務返回<code>java.util.Date</code>，則日期將在<code>DATE.date</code>欄位中重新調整。</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p><code>DATE</code>類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務操作將<code>java.util.Calendar</code>值作為輸入，則SOAP客戶端應用程式必須在<code>DATE.caledendar</code>欄位中傳遞日期。 在此例中，設定<code>DATE.date</code>欄位會導致運行時異常。 如果服務返回<code>java.util.Calendar</code>，則在<code>DATE.calendar</code>欄位中返回日期。 </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p><code>apachesoap:Map</code>，在服務WSDL中定義如下：</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>映射被表示為鍵／值對的序列。</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>XML類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務操作接受<code>org.w3c.dom.Document</code>值，請在<code>XML.document</code>欄位中傳遞XML資料。</p><p>設定<code>XML.element</code>欄位會造成執行時期例外。 如果服務返回<code>org.w3c.dom.Document</code>，則在<code>XML.document</code>欄位中返回XML資料。</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>XML類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務操作將<code>org.w3c.dom.Element</code>作為輸入，請在<code>XML.element</code>欄位中傳遞XML資料。</p><p>設定<code>XML.document</code>欄位會造成執行時期例外。 如果服務返回<code>org.w3c.dom.Element</code>，則在<code>XML.element</code>欄位中重新調整XML資料。</p></td>
  </tr>
 </tbody>
</table>

**Adobe開發人員網站**

「Adobe開發人員」網站包含下列文章，討論如何使用web service API叫用AEM Forms服務：

[建立表單轉換ASP.NET應用程式](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)

[使用自訂元件叫用web services](https://www.adobe.com/devnet/livecycle/articles/extend_webservices.html)

>[!NOTE]
>
>使用自訂元件叫用web services，說明如何建立叫用協力廠商web services的AEM Forms元件。

## 使用JAX-WS {#creating-java-proxy-classes-using-jax-ws}建立Java代理類

您可以使用JAX-WS將Forms服務WSDL轉換為Java代理類。 這些類可以調用AEM Forms服務操作。 Apache Ant可讓您建立建立指令碼，透過參考AEM Forms服務WSDL來產生Java代理類別。 通過執行以下步驟，可以生成JAX-WS代理檔案：

1. 在客戶端電腦上安裝Apache Ant。 (請參閱[https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)。)

   * 將bin目錄添加到類路徑。
   * 將`ANT_HOME`環境變數設定為安裝Ant的目錄。

1. 安裝JDK 1.6或更新版本。

   * 將JDK bin目錄添加到類路徑。
   * 將JRE bin目錄添加到類路徑中。 此bin位於`[JDK_INSTALL_LOCATION]/jre`目錄中。
   * 將`JAVA_HOME`環境變數設定為JDK的安裝目錄。

   JDK 1.6包含build.xml檔案中使用的wsimport程式。 JDK 1.5不包含該程式。

1. 在客戶端電腦上安裝JAX-WS。 （請參閱[Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)。）
1. 使用JAX-WS和Apache Ant生成Java代理類。 建立Ant構建指令碼以完成此任務。 以下指令碼是名為build.xml的示例Ant構建指令碼：

   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   在此Ant構建指令碼中，請注意`url`屬性已設定為引用在localhost上運行的加密服務WSDL。 `username`和`password`屬性必須設定為有效的表AEM單用戶名和口令。 請注意，URL包含`lc_version`屬性。 如果不指定`lc_version`選項，則無法調用新的AEM Forms服務操作。

   >[!NOTE]
   >
   >將`EncryptionService`替換為要使用Java代理類調用的AEM Forms服務名。 例如，要為Rights Management服務建立Java代理類，請指定：

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. 建立BAT檔案以執行Ant構建指令碼。 以下命令可以位於負責執行Ant構建指令碼的BAT檔案中：

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   將ANT構建指令碼放在C:\Program Files\Java\jaxws-ri\bin directory目錄中。 該指令碼將JAVA檔案寫入。/classes資料夾。 該指令碼生成可調用服務的JAVA檔案。

1. 將JAVA檔案打包到JAR檔案中。 如果您正在使用Eclipse，請依照下列步驟進行：

   * 建立新的Java專案，用來將Proxy JAVA檔案封裝到JAR檔案中。
   * 在項目中建立源資料夾。
   * 在Source資料夾中建立`com.adobe.idp.services`套件。
   * 選擇`com.adobe.idp.services`套件，然後將JAVA檔案從adobe/idp/services檔案夾匯入套件中。
   * 如有必要，請在「源」資料夾中建立`org/apache/xml/xmlsoap`軟體包。
   * 選擇源資料夾，然後從org/apache/xml/xmlsoap資料夾導入JAVA檔案。
   * 將Java編譯器的相容性層級設為5.0或更高。
   * 建立專案。
   * 將項目導出為JAR檔案。
   * 將此JAR檔案導入客戶端項目的類路徑中。 此外，導入位於&lt;安裝目錄>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty中的所有JAR檔案。

   >[!NOTE]
   >
   >使用表單進行寫程式時，所有Java web service快速啟動(除Forms服務外)AEM都使用JAX-WS建立Java代理檔案。 此外，所有Java web service都可快速啟動，請使用SwaRef。 (請參閱[使用SwaRef](#invoking-aem-forms-using-swaref)叫用AEM Forms。)

**另請參閱**

[使用Apache Axis建立Java代理類](#creating-java-proxy-classes-using-apache-axis)

[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[通過HTTP使用BLOB資料調用AEM Forms](#invoking-aem-forms-using-blob-data-over-http)

[使用SwaRef叫用AEM Forms](#invoking-aem-forms-using-swaref)

## 使用Apache Axis {#creating-java-proxy-classes-using-apache-axis}建立Java代理類

您可以使用Apache Axis WSDL2Java工具將Forms服務轉換為Java代理類。 這些類可以調用Forms服務操作。 使用Apache Ant，可以通過服務WSDL生成Axis庫檔案。 您可以在URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/)下載Apache Axis。

>[!NOTE]
>
>與Forms服務關聯的web服務快速啟動使用使用Apache Axis建立的Java代理類。 FormsWeb服務快速啟動還使用Base64作為編碼類型。 (請參閱[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts))。

通過執行以下步驟，可以生成Axis Java庫檔案：

1. 在客戶端電腦上安裝Apache Ant。 您可在[https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)取得。

   * 將bin目錄添加到類路徑。
   * 將`ANT_HOME`環境變數設定為安裝Ant的目錄。

1. 在客戶端電腦上安裝Apache Axis 1.4。 您可在[https://ws.apache.org/axis/](https://ws.apache.org/axis/.md)取得。
1. 按照[https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html)的Axis安裝說明中所述，設定類路徑以在Web服務客戶端中使用Axis JAR檔案。
1. 使用Axis中的Apache WSDL2Java工具來產生Java代理類。 建立Ant構建指令碼以完成此任務。 以下指令碼是名為build.xml的示例Ant構建指令碼：

   ```java
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   在此Ant構建指令碼中，請注意`url`屬性已設定為引用在localhost上運行的加密服務WSDL。 `username`和`password`屬性必須設定為有效的表AEM單用戶名和口令。

1. 建立BAT檔案以執行Ant構建指令碼。 以下命令可以位於負責執行Ant構建指令碼的BAT檔案中：

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA檔案將寫入C:\JavaFiles folder as specified by the `output`屬性。 要成功調用Forms服務，請將這些JAVA檔案導入到類路徑中。

   預設情況下，這些檔案屬於名為`com.adobe.idp.services`的Java包。 建議將這些JAVA檔案放入JAR檔案中。 然後，將JAR檔案匯入用戶端應用程式的類別路徑。

   >[!NOTE]
   >
   >將。JAVA檔案放入JAR有不同的方法。 一種方式是使用Java IDE，例如Eclipse。 建立Java項目並建立`com.adobe.idp.services`包（所有。JAVA檔案均屬於此包）。 接著，將所有。JAVA檔案匯入套件。 最後，將項目導出為JAR檔案。

1. 修改`EncryptionServiceLocator`類別中的URL以指定編碼類型。 例如，若要使用base64，請指定`?blob=base64`以確保`BLOB`對象返回二進位資料。 也就是說，在`EncryptionServiceLocator`類別中，找到以下代碼行：

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   並將其更改為：

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. 將下列Axis JAR檔案新增至Java專案的類別路徑：

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   這些JAR檔案位於`[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty`目錄中。

**另請參閱**

[使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws)

[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[通過HTTP使用BLOB資料調用AEM Forms](#invoking-aem-forms-using-blob-data-over-http)

## 使用Base64編碼{#invoking-aem-forms-using-base64-encoding}調用AEM Forms

您可以使用Base64編碼叫用AEM Forms服務。 Base64編碼對隨Web服務調用請求發送的附件進行編碼。 也就是說，`BLOB`資料是Base64編碼，而非整個SOAP訊息。

「使用Base64編碼叫用AEM Forms」討論使用Base64編碼叫用以下名為`MyApplication/EncryptDocument`的AEM Forms短時進程。

>[!NOTE]
>
>此程式不基於現有的AEM Forms程式。 要跟隨代碼示例，請使用Workbench建立名為`MyApplication/EncryptDocument`的流程。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

調用此進程時，它執行以下操作：

1. 取得傳遞至程式的不安全PDF檔案。 此操作基於`SetValue`操作。 此進程的輸入參數是名為`inDoc`的`document`進程變數。
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 密碼加密的PDF檔案會在名為`outDoc`的流程變數中傳回。

### 建立使用Base64編碼{#creating-a-net-client-assembly-that-uses-base64-encoding}的。NET客戶端元件

您可以建立。NET客戶端元件，從Microsoft Visual Studio .NET項目調用Forms服務。 要建立使用base64編碼的。NET客戶端元件，請執行以下步驟：

1. 根據AEM Forms呼叫URL建立代理類。
1. 建立生成。NET客戶端元件的Microsoft Visual Studio .NET項目。

**建立代理類**

您可以使用Microsoft Visual Studio附帶的工具來建立用於建立。NET客戶端元件的代理類。 此工具的名稱為wsdl.exe，它位於Microsoft Visual Studio安裝資料夾中。 要建立代理類，請開啟命令提示符並導航到包含wsdl.exe檔案的資料夾。 有關wsdl.exe工具的詳細資訊，請參見&#x200B;*MSDN幫助*。

在命令提示符下輸入以下命令：

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

依預設，此工具會在以WSDL名稱為基礎的相同資料夾中建立CS檔案。 在這種情況下，它會建立名為&#x200B;*EncryptDocumentService.cs*&#x200B;的CS檔案。 您可使用此CS檔案來建立Proxy物件，讓您叫用在呼叫URL中指定的服務。

將proxy類別中的URL修改為包含`?blob=base64`，以確保`BLOB`物件傳回二進位資料。 在proxy類別中，找出下列程式碼行：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

並將其更改為：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

*使用Base64 Encoding*&#x200B;調用AEM Forms部分使用`MyApplication/EncryptDocument`作為示例。 如果要為另一個Forms服務建立。NET客戶端元件，請確保用服務的名稱替換`MyApplication/EncryptDocument`。

**開發。NET客戶端元件**

建立生成。NET客戶端元件的Visual Studio類庫項目。 您使用wsdl.exe建立的CS檔案可匯入此專案。 此項目生成一個DLL檔案（.NET客戶端元件），可用於其他Visual Studio .NET項目以調用服務。

1. 啟動Microsoft Visual Studio .NET。
1. 建立類別程式庫專案，並將其命名為DocumentService。
1. 匯入您使用wsdl.exe建立的CS檔案。
1. 在&#x200B;**Project**&#x200B;菜單中，選擇&#x200B;**添加引用**。
1. 在「添加參考」對話框中，選擇&#x200B;**System.Web.Services.dll**。
1. 按一下&#x200B;**選擇** ，然後按一下&#x200B;**確定**。
1. 編譯和建立專案。

>[!NOTE]
>
>此過程建立一個名為DocumentService.dll的。NET客戶端程式集，可用於向`MyApplication/EncryptDocument`服務發送SOAP請求。

>[!NOTE]
>
>請確定您已將`?blob=base64`新增至用於建立。NET用戶端元件的proxy類別中的URL。 否則，無法從`BLOB`對象中檢索二進位資料。

**引用。NET客戶端元件**

將新建立的。NET客戶端元件放在您正在開發客戶端應用程式的電腦上。 將。NET客戶端元件放置到目錄後，可以從項目中參照它。 另請參考專案的`System.Web.Services`程式庫。 如果未引用此庫，則不能使用。NET客戶端元件調用服務。

1. 在&#x200B;**Project**&#x200B;菜單中，選擇&#x200B;**添加引用**。
1. 按一下&#x200B;**.NET**&#x200B;頁籤。
1. 按一下&#x200B;**瀏覽**&#x200B;並找到DocumentService.dll檔案。
1. 按一下&#x200B;**選擇** ，然後按一下&#x200B;**確定**。

**使用使用Base64編碼的。NET客戶端元件調用服務**

您可以使用使用Base64編碼的。NET客戶端元件調用`MyApplication/EncryptDocument`服務（在Workbench中構建）。 要調用`MyApplication/EncryptDocument`服務，請執行以下步驟：

1. 建立一個使用`MyApplication/EncryptDocument`服務WSDL的Microsoft .NET客戶端元件。
1. 建立客戶端Microsoft .NET項目。 在客戶端項目中參考Microsoft .NET客戶端元件。 另請參閱`System.Web.Services`。
1. 使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`MyApplication_EncryptDocumentService`對象。
1. 使用`System.Net.NetworkCredential`物件設定`MyApplication_EncryptDocumentService`物件的`Credentials`屬性。 在`System.Net.NetworkCredential`建構函式中，指定表AEM單使用者名稱和對應的密碼。 設定驗證值，使。NET客戶端應用程式能夠成功地與AEM Forms交換SOAP消息。
1. 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存傳遞至`MyApplication/EncryptDocument`程式的PDF檔案。
1. 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表PDF檔案的檔案位置和開啟檔案的模式。
1. 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
1. 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
1. 通過為`binaryData`對象的屬性指定位元組陣列的內容來填充`BLOB`對象。
1. 叫用`MyApplication_EncryptDocumentService`物件的`invoke`方法並傳遞包含PDF檔案的`BLOB`物件，以叫用`MyApplication/EncryptDocument`程式。 此程式會傳回`BLOB`物件內的加密PDF檔案。
1. 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立對象，該字串值表示密碼加密文檔的檔案位置。
1. 建立位元組陣列，儲存`MyApplicationEncryptDocumentService`物件`invoke`方法傳回之`BLOB`物件的資料內容。 獲取`BLOB`對象`binaryData`資料成員的值，以填充位元組陣列。
1. 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
1. 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列內容寫入PDF檔案。

### 使用Java代理類和Base64編碼{#invoking-a-service-using-java-proxy-classes-and-base64-encoding}調用服務

您可以使用Java代理類和Base64調用AEM Forms服務。 要使用Java代理類調用`MyApplication/EncryptDocument`服務，請執行以下步驟：

1. 使用使用`MyApplication/EncryptDocument`服務WSDL的JAX-WS建立Java代理類。 使用以下WSDL端點：

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >將`hiro-xp` *取代為代管AEM Forms的J2EE應用程式伺服器的IP位址。*

1. 將使用JAX-WS建立的Java代理類包裝到JAR檔案中。
1. 將Java代理JAR檔案和JAR檔案包含在以下路徑中：

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   Java用戶端專案的類別路徑。

1. 使用其建構子建立`MyApplicationEncryptDocumentService`對象。
1. 調用`MyApplicationEncryptDocumentService`物件的`getEncryptDocument`方法，以建立`MyApplicationEncryptDocument`物件。
1. 通過為以下資料成員分配值來設定調用AEM Forms所需的連接值：

   * 為`javax.xml.ws.BindingProvider`物件的`ENDPOINT_ADDRESS_PROPERTY`欄位指定WSDL端點和編碼類型。 要使用Base64編碼調用`MyApplication/EncryptDocument`服務，請指定以下URL值：

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * 將表AEM單使用者指派至`javax.xml.ws.BindingProvider`物件的`USERNAME_PROPERTY`欄位。
   * 為`javax.xml.ws.BindingProvider`物件的`PASSWORD_PROPERTY`欄位指派對應的密碼值。

   下列程式碼範例顯示此應用程式邏輯：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 使用PDF文檔的建構子建立`java.io.FileInputStream`對象，以檢索要發送到`MyApplication/EncryptDocument`進程的PDF文檔。 傳遞指定PDF檔案位置的字串值。
1. 建立位元組陣列，並用`java.io.FileInputStream`對象的內容填充該陣列。
1. 使用其建構子建立`BLOB`對象。
1. 調用`setBinaryData`方法並傳遞位元組陣列，以填充`BLOB`對象。 `BLOB`物件的`setBinaryData`是使用Base64編碼時要呼叫的方法。 請參閱在服務請求中提供BLOB對象。
1. 叫用`MyApplicationEncryptDocument`物件的`invoke`方法，以叫用`MyApplication/EncryptDocument`程式。 傳遞包含PDF檔案的`BLOB`物件。 invoke方法返回包含加密PDF文檔的`BLOB`對象。
1. 呼叫`BLOB`物件的`getBinaryData`方法，以建立包含加密PDF檔案的位元組陣列。
1. 將加密的PDF檔案儲存為PDF檔案。 將位元組陣列寫入檔案。

**另請參閱**

[快速入門：使用Java代理檔案和Base64編碼調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[建立使用Base64編碼的。NET客戶端元件](#creating-a-net-client-assembly-that-uses-base64-encoding)

## 使用MTOM {#invoking-aem-forms-using-mtom}調用AEM Forms

您可以使用web services標準MTOM來叫用AEM Forms服務。 此標準定義二進位資料（例如PDF檔案）如何透過網際網路或內部網路傳輸。 MTOM的功能是使用`XOP:Include`元素。 此元素在XML二進位優化打包(XOP)規範中定義，以引用SOAP消息的二進位附件。

這裡討論的是使用MTOM調用以下名為`MyApplication/EncryptDocument`的AEM Forms短期進程。

>[!NOTE]
>
>此程式不基於現有的AEM Forms程式。 要跟隨代碼示例，請使用Workbench建立名為`MyApplication/EncryptDocument`的流程。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

調用此進程時，它執行以下操作：

1. 取得傳遞至程式的不安全PDF檔案。 此操作基於`SetValue`操作。 此進程的輸入參數是名為`inDoc`的`document`進程變數。
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 密碼加密的PDF檔案會在名為`outDoc`的流程變數中傳回。

>[!NOTE]
>
>MTOM支援已新增至第9版AEM Forms。

>[!NOTE]
>
>使用MTOM傳輸通訊協定的JAX WS應用程式的已傳送和已接收資料限制為25MB。 此限制是由於JAX-WS中的錯誤。 如果您所傳送和接收檔案的總大小超過25MB，請使用SwaRef傳輸通訊協定，而非MTOM傳輸通訊協定。 否則，可能出現`OutOfMemory`例外。

這裡討論的是在Microsoft .NET項目中使用MTOM調用AEM Forms服務。 使用的。NET架構為3.5，開發環境為Visual Studio 2008。 如果您的開發電腦上已安裝Web服務增強功能(WSE)，請將其移除。 .NET 3.5框架支援名為Windows通信基礎(WCF)的SOAP框架。 當使用MTOM調用AEM Forms時，只支援WCF（非WSE）。

### 建立使用MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}調用服務的。NET項目

您可以建立一個Microsoft .NET項目，該項目可以使用web services調用AEM Forms服務。 首先，使用Visual Studio 2008建立Microsoft .NET項目。 要調用AEM Forms服務，請建立要在項目中調用的AEM Forms服務的服務參考。 當您建立服務參考時，請指定AEM Forms服務的URL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

將`localhost`取代為代管AEM Forms的J2EE應用程式伺服器的IP位址。 將`MyApplication/EncryptDocument`替換為要調用的AEM Forms服務的名稱。 例如，要調用Rights Management操作，請指定：

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

`lc_version`選項可確保AEM Forms功能（如MTOM）可用。 若未指定`lc_version`選項，就無法使用MTOM叫用AEM Forms。

建立服務參考後，與AEM Forms服務關聯的資料類型可用於。NET項目中。 要建立調用AEM Forms服務的。NET項目，請執行以下步驟：

1. 使用Microsoft Visual Studio 2008建立。NET專案。
1. 在&#x200B;**Project**&#x200B;菜單中，選擇&#x200B;**添加服務參考**。
1. 在&#x200B;**地址**&#x200B;對話框中，為AEM Forms服務指定WSDL。 例如，

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. 按一下&#x200B;**Go** ，然後按一下&#x200B;**OK**。

### 在。NET項目{#invoking-a-service-using-mtom-in-a-net-project}中使用MTOM調用服務

請考慮`MyApplication/EncryptDocument`程式，該程式接受不安全的PDF文檔並返回密碼加密的PDF文檔。 要使用MTOM調用`MyApplication/EncryptDocument`進程（在Workbench中構建），請執行以下步驟：

1. 建立Microsoft .NET項目。
1. 使用其預設建構子建立`MyApplication_EncryptDocumentClient`對象。
1. 使用`System.ServiceModel.EndpointAddress`建構函式建立`MyApplication_EncryptDocumentClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務和編碼類型：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   您不需要使用`lc_version`屬性。 建立服務參考時，將使用此屬性。 不過，請確定您指定`?blob=mtom`。

   >[!NOTE]
   >
   >將`hiro-xp` *取代為代管AEM Forms的J2EE應用程式伺服器的IP位址。*

1. 獲取`EncryptDocumentClient.Endpoint.Binding`資料成員的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將返回值轉換為`BasicHttpBinding`。
1. 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`資料成員設為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
1. 執行下列工作以啟用基本HTTP驗證：

   * 將表AEM單用戶名分配給資料成員`MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`。
   * 為資料成員`MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`分配相應的口令值。
   * 將常數值`HttpClientCredentialType.Basic`分配給資料成員`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給資料成員`BasicHttpBindingSecurity.Security.Mode`。

   下列程式碼範例顯示這些工作。

   ```java
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. 使用其建構子建立`BLOB`對象。 `BLOB`物件用來儲存PDF檔案，以傳遞至`MyApplication/EncryptDocument`程式。
1. 通過調用`System.IO.FileStream`對象的建構子建立對象。 傳遞一個字串值，代表PDF檔案的檔案位置和開啟檔案的模式。
1. 建立儲存`System.IO.FileStream`對象內容的位元組陣列。 您可以取得`System.IO.FileStream`物件的`Length`屬性，以判斷位元組陣列的大小。
1. 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞要讀取的位元組陣列、起始位置和串流長度。
1. 通過為`MTOM`資料成員分配位元組陣列的內容來填充`BLOB`對象。
1. 叫用`MyApplication_EncryptDocumentClient`物件的`invoke`方法，以叫用`MyApplication/EncryptDocument`程式。 傳遞包含PDF檔案的`BLOB`物件。 此程式會傳回`BLOB`物件內的加密PDF檔案。
1. 通過調用`System.IO.FileStream`對象的建構子並傳遞一個字串值來建立對象，該字串值表示受保護PDF文檔的檔案位置。
1. 建立一個位元組陣列，用於儲存`invoke`方法返回的`BLOB`對象的資料內容。 獲取`BLOB`對象`MTOM`資料成員的值，以填充位元組陣列。
1. 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
1. 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

>[!NOTE]
>
>大多數AEM Forms服務業務都有MTOM快速入門。 您可以在服務的對應快速入門區段中檢視這些快速入門。 例如，要查看「輸出快速啟動」部分，請參閱[Output Service API Quick Starts](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**另請參閱**

[快速入門：在。NET專案中使用MTOM叫用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[使用web services存取多個服務](#accessing-multiple-services-using-web-services)

[建立ASP.NET網路應用程式，以叫用以人為中心的長壽命程式](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## 使用SwaRef {#invoking-aem-forms-using-swaref}調用AEM Forms

您可以使用SwaRef叫用AEM Forms服務。 `wsi:swaRef` XML元素的內容會以附件形式在儲存對附件的引用的SOAP主體內發送。 使用SwaRef調用Forms服務時，請使用Java API for XML Web Services(JAX-WS)來建立Java代理類。 （請參閱[Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)。）

這裡討論的是使用SwaRef調用以下名為`MyApplication/EncryptDocument`的Forms短壽命進程。

>[!NOTE]
>
>此程式不基於現有的AEM Forms程式。 要跟隨代碼示例，請使用Workbench建立名為`MyApplication/EncryptDocument`的流程。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

調用此進程時，它執行以下操作：

1. 取得傳遞至程式的不安全PDF檔案。 此操作基於`SetValue`操作。 此進程的輸入參數是名為`inDoc`的`document`進程變數。
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 密碼加密的PDF檔案會在名為`outDoc`的流程變數中傳回。

>[!NOTE]
>
>AEM Forms新增SwaRef支援

以下討論如何在Java客戶端應用程式中使用SwaRef來叫用Forms服務。 Java應用程式使用通過使用JAX-WS建立的代理類。

### 使用使用SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}的JAX-WS庫檔案調用服務

要使用使用JAX-WS和SwaRef建立的Java代理檔案調用`MyApplication/EncryptDocument`進程，請執行以下步驟：

1. 使用使用`MyApplication/EncryptDocument`服務WSDL的JAX-WS建立Java代理類。 使用以下WSDL端點：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   有關資訊，請參見[使用JAX-WS](#creating-java-proxy-classes-using-jax-ws)建立Java代理類。

   >[!NOTE]
   >
   >將`hiro-xp` *取代為代管AEM Forms的J2EE應用程式伺服器的IP位址。*

1. 將使用JAX-WS建立的Java代理類包裝到JAR檔案中。
1. 將Java代理JAR檔案和JAR檔案包含在以下路徑中：

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   Java用戶端專案的類別路徑。

1. 使用其建構子建立`MyApplicationEncryptDocumentService`對象。
1. 調用`MyApplicationEncryptDocumentService`物件的`getEncryptDocument`方法，以建立`MyApplicationEncryptDocument`物件。
1. 通過為以下資料成員分配值來設定調用AEM Forms所需的連接值：

   * 為`javax.xml.ws.BindingProvider`物件的`ENDPOINT_ADDRESS_PROPERTY`欄位指定WSDL端點和編碼類型。 若要使用SwaRef編碼叫用`MyApplication/EncryptDocument`服務，請指定下列URL值：

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * 將表AEM單使用者指派至`javax.xml.ws.BindingProvider`物件的`USERNAME_PROPERTY`欄位。
   * 為`javax.xml.ws.BindingProvider`物件的`PASSWORD_PROPERTY`欄位指派對應的密碼值。

   下列程式碼範例顯示此應用程式邏輯：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 使用PDF文檔的建構子建立`java.io.File`對象，以檢索要發送到`MyApplication/EncryptDocument`進程的PDF文檔。 傳遞指定PDF檔案位置的字串值。
1. 使用`FileDataSource`建構函式建立`javax.activation.DataSource`物件。 傳遞`java.io.File`物件。
1. 使用其建構子並傳遞`javax.activation.DataSource`對象，建立`javax.activation.DataHandler`對象。
1. 使用其建構子建立`BLOB`對象。
1. 調用`setSwaRef`方法並傳遞`javax.activation.DataHandler`物件，以填入`BLOB`物件。
1. 叫用`MyApplicationEncryptDocument`物件的`invoke`方法並傳遞包含PDF檔案的`BLOB`物件，以叫用`MyApplication/EncryptDocument`程式。 invoke方法返回包含加密PDF文檔的`BLOB`對象。
1. 調用`BLOB`物件的`getSwaRef`方法，以填入`javax.activation.DataHandler`物件。
1. 調用`javax.activation.DataHandler`物件的`getInputStream`方法，將`javax.activation.DataHandler`物件轉換為`java.io.InputSteam`例項。
1. 將`java.io.InputSteam`例項寫入代表加密PDF檔案的PDF檔案。

>[!NOTE]
>
>大多數AEM Forms服務操作都有SwaRef快速啟動。 您可以在服務的對應快速入門區段中檢視這些快速入門。 例如，要查看「輸出快速啟動」部分，請參閱[Output Service API Quick Starts](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**另請參閱**

[快速入門：在Java項目中使用SwaRef調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## 使用HTTP {#invoking-aem-forms-using-blob-data-over-http}上的BLOB資料調用AEM Forms

您可以使用web services叫用AEM Forms服務，並透過HTTP傳遞BLOB資料。 將BLOB資料透過HTTP傳遞是另一種技術，而非使用base64編碼、DIME或MIME。 例如，您可以在使用Web服務增強功能3.0（不支援DIME或MIME）的Microsoft .NET專案中，透過HTTP傳遞資料。 在HTTP上使用BLOB資料時，輸入資料會在呼叫AEM Forms服務之前上傳。

「使用HTTP上的BLOB資料調用AEM Forms」討論通過通過HTTP傳遞BLOB資料來調用以下名為`MyApplication/EncryptDocument`的AEM Forms短期進程。

>[!NOTE]
>
>此程式不基於現有的AEM Forms程式。 要跟隨代碼示例，請使用Workbench建立名為`MyApplication/EncryptDocument`的流程。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

調用此進程時，它執行以下操作：

1. 取得傳遞至程式的不安全PDF檔案。 此操作基於`SetValue`操作。 此進程的輸入參數是名為`inDoc`的`document`進程變數。
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 密碼加密的PDF檔案會在名為`outDoc`的流程變數中傳回。

>[!NOTE]
>
>建議您熟悉使用SOAP叫用AEM Forms。 (請參閱[使用Web Services叫用AEM Forms](#invoking-aem-forms-using-web-services)。)

### 建立通過HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}使用資料的。NET客戶端元件

要建立通過HTTP使用資料的客戶端元件，請遵循[使用Base64編碼](#invoking-aem-forms-using-base64-encoding)調用AEM Forms中指定的過程。 不過，請將proxy類別中的URL修改為包含`?blob=http`，而非`?blob=base64`。 此動作可確保資料透過HTTP傳遞。 在proxy類別中，找出下列程式碼行：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

並將其更改為：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**引用。NET clienMyApplication/EncryptDocument元件**

將新的。NET客戶端元件放在您正在開發客戶端應用程式的電腦上。 將。NET客戶端元件放置到目錄後，可以從項目中參照它。 從您的專案參考`System.Web.Services`程式庫。 如果未引用此庫，則不能使用。NET客戶端元件調用服務。

1. 在&#x200B;**Project**&#x200B;菜單中，選擇&#x200B;**添加引用**。
1. 按一下&#x200B;**.NET**&#x200B;頁籤。
1. 按一下&#x200B;**瀏覽**&#x200B;並找到DocumentService.dll檔案。
1. 按一下&#x200B;**選擇** ，然後按一下&#x200B;**確定**。

**使用通過HTTP使用BLOB資料的。NET客戶端元件調用服務**

您可以使用透過HTTP使用資料的。NET用戶端元件來叫用`MyApplication/EncryptDocument`服務（此服務是在Workbench中建立的）。 要調用`MyApplication/EncryptDocument`服務，請執行以下步驟：

1. 建立。NET客戶端元件。
1. 參考Microsoft .NET客戶端元件。 建立客戶端Microsoft .NET項目。 在客戶端項目中參考Microsoft .NET客戶端元件。 另請參閱`System.Web.Services`。
1. 使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`MyApplication_EncryptDocumentService`對象。
1. 使用`System.Net.NetworkCredential`物件設定`MyApplication_EncryptDocumentService`物件的`Credentials`屬性。 在`System.Net.NetworkCredential`建構函式中，指定表AEM單使用者名稱和對應的密碼。 設定驗證值，使。NET客戶端應用程式能夠成功地與AEM Forms交換SOAP消息。
1. 使用其建構子建立`BLOB`對象。 `BLOB`對象用於將資料傳遞到`MyApplication/EncryptDocument`進程。
1. 為`BLOB`物件的`remoteURL`資料成員指派字串值，指定要傳遞至`MyApplication/EncryptDocument`服務之PDF檔案的URI位置。
1. 調用`MyApplication_EncryptDocumentService`物件的`invoke`方法並傳遞`BLOB`物件，以叫用`MyApplication/EncryptDocument`程式。 此程式會傳回`BLOB`物件內的加密PDF檔案。
1. 使用其建構函式建立`System.UriBuilder`物件，並傳遞傳回`BLOB`物件之`remoteURL`資料成員的值。
1. 將`System.UriBuilder`物件轉換為`System.IO.Stream`物件。 （此清單後面的C#快速啟動說明了如何執行此任務。）
1. 建立位元組陣列，並將位於`System.IO.Stream`物件中的資料填入該陣列。
1. 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
1. 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列內容寫入PDF檔案。

### 通過HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}使用Java代理類和BLOB資料調用服務

您可以使用Java代理類和通過HTTP的BLOB資料調用AEM Forms服務。 要使用Java代理類調用`MyApplication/EncryptDocument`服務，請執行以下步驟：

1. 使用使用`MyApplication/EncryptDocument`服務WSDL的JAX-WS建立Java代理類。 使用以下WSDL端點：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   有關資訊，請參見[使用JAX-WS](#creating-java-proxy-classes-using-jax-ws)建立Java代理類。

   >[!NOTE]
   >
   >將`hiro-xp` *取代為代管AEM Forms的J2EE應用程式伺服器的IP位址。*

1. 將使用JAX-WS建立的Java代理類包裝到JAR檔案中。
1. 將Java代理JAR檔案和JAR檔案包含在以下路徑中：

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   Java用戶端專案的類別路徑。

1. 使用其建構子建立`MyApplicationEncryptDocumentService`對象。
1. 調用`MyApplicationEncryptDocumentService`物件的`getEncryptDocument`方法，以建立`MyApplicationEncryptDocument`物件。
1. 通過為以下資料成員分配值來設定調用AEM Forms所需的連接值：

   * 為`javax.xml.ws.BindingProvider`物件的`ENDPOINT_ADDRESS_PROPERTY`欄位指定WSDL端點和編碼類型。 若要使用BLOB over HTTP編碼來叫用`MyApplication/EncryptDocument`服務，請指定下列URL值：

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * 將表AEM單使用者指派至`javax.xml.ws.BindingProvider`物件的`USERNAME_PROPERTY`欄位。
   * 為`javax.xml.ws.BindingProvider`物件的`PASSWORD_PROPERTY`欄位指派對應的密碼值。

   下列程式碼範例顯示此應用程式邏輯：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 使用其建構子建立`BLOB`對象。
1. 調用`setRemoteURL`方法來填入`BLOB`物件。 傳遞一個字串值，指定要傳遞至`MyApplication/EncryptDocument`服務的PDF檔案的URI位置。
1. 叫用`MyApplicationEncryptDocument`物件的`invoke`方法並傳遞包含PDF檔案的`BLOB`物件，以叫用`MyApplication/EncryptDocument`程式。 此程式會傳回`BLOB`物件內的加密PDF檔案。
1. 建立位元組陣列，以儲存代表加密PDF檔案的資料流。 叫用`BLOB`物件的`getRemoteURL`方法（使用`invoke`方法傳回的`BLOB`物件）。
1. 使用其建構子建立`java.io.File`對象。 此物件代表加密的PDF檔案。
1. 使用其建構子並傳遞`java.io.File`對象，建立`java.io.FileOutputStream`對象。
1. 叫用`java.io.FileOutputStream`物件的`write`方法。 傳遞包含代表加密PDF檔案之資料流的位元組陣列。

## 使用DIME調用AEM Forms{#invoking-aem-forms-using-dime}

您可以使用帶附件的SOAP調用AEM Forms服務。 AEM Forms支援MIME和DIME網站服務標準。 DIME可讓您傳送二進位附件，例如PDF檔案，以及呼叫請求，而非對附件進行編碼。 *使用DIME*&#x200B;調用AEM Forms部分討論使用DIME調用以下名為`MyApplication/EncryptDocument`的AEM Forms短期進程。

調用此進程時，它執行以下操作：

1. 取得傳遞至程式的不安全PDF檔案。 此操作基於`SetValue`操作。 此進程的輸入參數是名為`inDoc`的`document`進程變數。
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 密碼加密的PDF檔案會在名為`outDoc`的流程變數中傳回。

此程式不基於現有的AEM Forms程式。 要跟隨代碼示例，請使用Workbench建立名為`MyApplication/EncryptDocument`的流程。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

>[!NOTE]
>
>不建議使用DIME調用AEM Forms服務操作。 建議您使用MTOM。 (請參閱[使用MTOM](#invoking-aem-forms-using-mtom)叫用AEM Forms。)

### 建立使用DIME {#creating-a-net-project-that-uses-dime}的。NET項目

要建立可使用DIME調用Forms服務的。NET項目，請執行以下任務：

* 在您的開發電腦上安裝Web Services Enhancements 2.0。
* 從您的。NET專案中，建立FormsAEMForms服務的網頁參考。

**安裝Web Services增強功能2.0**

在您的開發電腦上安裝Web Services Enhancements 2.0，並將它與Microsoft Visual Studio .NET整合。 您可以從[Microsoft下載中心下載Web Services Enhancements 2.0。](https://www.microsoft.com/downloads/search.aspx)

從這個網頁，搜尋Web Services Enhancements 2.0，並將它下載到您的開發電腦。 此下載內容會在您的電腦上放置名為Microsoft WSE 2.0 SPI.msi的檔案。 運行安裝程式並遵循聯機指示。

>[!NOTE]
>
>網站服務增強功能2.0支援DIME。 使用Web Services Enhancements 2.0時，支援的Microsoft Visual Studio版本為2003。網站服務增強功能3.0不支援DIME;但是，它支援MTOM。

**建立對AEM Forms服務的Web引用**

在您的開發電腦上安裝Web Services Enhancements 2.0並建立Microsoft .NET專案後，請建立Forms服務的Web參考。 例如，要建立`MyApplication/EncryptDocument`進程的Web引用，並假定本地電腦上已安裝Forms，請指定以下URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

建立Web引用後，以下兩種代理資料類型可供您在。NET項目中使用：`EncryptDocumentService`和`EncryptDocumentServiceWse`。 要使用DIME調用`MyApplication/EncryptDocument`進程，請使用`EncryptDocumentServiceWse`類型。

>[!NOTE]
>
>在建立Forms服務的Web參考之前，請確定您在專案中參考Web服務增強功能2.0。 （請參閱「安裝網站服務增強功能2.0」）。

**參考WSE程式庫**

1. 在「項目」菜單中，選擇「添加參考」。
1. 在「添加參考」對話框中，選擇Microsoft.Web.Services2.dll。
1. 選擇System.Web.Services.dll。
1. 按一下「選取」，然後按一下「確定」。

**建立Forms服務的Web參考**

1. 在「項目」菜單中，選擇「添加Web參考」。
1. 在「URL」對話方塊中，指定Forms服務的URL。
1. 按一下「執行」，然後按一下「新增參考」。

>[!NOTE]
>
>請確定您啟用。NET專案以使用WSE程式庫。 在「項目瀏覽器」中，按一下右鍵項目名稱，然後選擇「啟用WSE 2.0」。請確定已選取出現之對話方塊的核取方塊。

**在。NET專案中使用DIME叫用服務**

您可以使用DIME叫用Forms服務。 請考慮`MyApplication/EncryptDocument`程式，該程式接受不安全的PDF文檔並返回密碼加密的PDF文檔。 要使用DIME調用`MyApplication/EncryptDocument`進程，請執行以下步驟：

1. 建立Microsoft .NET專案，讓您使用DIME叫用Forms服務。 請確定您包含Web Services Enhancements 2.0並建立AEM Forms服務的Web參考。
1. 將Web引用設定為`MyApplication/EncryptDocument`進程後，使用其預設建構子建立`EncryptDocumentServiceWse`對象。
1. 將`EncryptDocumentServiceWse`物件的`Credentials`資料成員設定為`System.Net.NetworkCredential`值，以指定表單使用AEM者名稱和密碼值。
1. 使用其建構子並傳遞以下值來建立`Microsoft.Web.Services2.Dime.DimeAttachment`對象：

   * 指定GUID值的字串值。 您可以叫用`System.Guid.NewGuid.ToString`方法來取得GUID值。
   * 指定內容類型的字串值。 由於此程式需要PDF檔案，請指定`application/pdf`。
   * `TypeFormat`枚舉值。 指定`TypeFormat.MediaType`。
   * 一個字串值，它指定要傳遞到AEM Forms進程的PDF文檔的位置。

1. 使用其建構子建立`BLOB`對象。
1. 將`Microsoft.Web.Services2.Dime.DimeAttachment`物件的`Id`資料成員值指派給`BLOB`物件的`attachmentID`資料成員，將DIME附件新增至`BLOB`物件。
1. 調用`EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add`方法並傳遞`Microsoft.Web.Services2.Dime.DimeAttachment`對象。
1. 調用`EncryptDocumentServiceWse`物件的`invoke`方法並傳遞包含DIME附件的`BLOB`物件，以叫用`MyApplication/EncryptDocument`程式。 此程式會傳回`BLOB`物件內的加密PDF檔案。
1. 獲取返回的`BLOB`對象的`attachmentID`資料成員的值，以獲取附件標識符值。
1. 重複`EncryptDocumentServiceWse.ResponseSoapContext.Attachments`中的附件，並使用附件標識符值來獲取加密的PDF文檔。
1. 獲取`Attachment`對象`Stream`資料成員的值，以獲得`System.IO.Stream`對象。
1. 建立位元組陣列，並將該位元組陣列傳遞至`System.IO.Stream`物件的`Read`方法。 此方法會以代表加密PDF檔案的資料流填入位元組陣列。
1. 叫用其建構函式並傳遞代表PDF檔案位置的字串值，以建立`System.IO.FileStream`物件。 此物件代表加密的PDF檔案。
1. 調用`System.IO.BinaryWriter`對象的建構子並傳遞`System.IO.FileStream`對象，以建立對象。
1. 調用`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

### 建立使用DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}的Apache Axis Java代理類

您可以使用Apache Axis WSDL2Java工具將服務WSDL轉換為Java代理類，以便調用服務操作。 使用Apache Ant，您可以通過AEM Forms服務WSDL生成Axis庫檔案，該服務WSDL允許您調用服務。 （請參閱[使用Apache Axis](#creating-java-proxy-classes-using-apache-axis)建立Java代理類。）

Apache Axis WSDL2Java工具會產生JAVA檔案，其中包含用於傳送SOAP請求至服務的方法。 由服務接收的SOAP請求由Axis生成的庫解碼，並返回到方法和參數中。

要使用Axis生成的庫檔案和DIME調用`MyApplication/EncryptDocument`服務（在Workbench中內置），請執行以下步驟：

1. 使用Apache Axis建立使用`MyApplication/EncryptDocument`服務WSDL的Java代理類。 （請參閱[使用Apache Axis](#creating-java-proxy-classes-using-apache-axis)建立Java代理類。）
1. 將Java代理類包含到類路徑中。
1. 使用其建構子建立`MyApplicationEncryptDocumentServiceLocator`對象。
1. 使用`URL`物件的建構函式並傳遞指定AEM Forms服務WSDL定義的字串值，以建立物件。 請確定您在SOAP端點URL的結尾處指定`?blob=dime`。 例如，使用

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. 通過調用`EncryptDocumentSoapBindingStub`對象的建構子並傳遞`MyApplicationEncryptDocumentServiceLocator`對象和`URL`對象來建立對象。
1. 通過調AEM用`EncryptDocumentSoapBindingStub`對象的`setUsername`和`setPassword`方法來設定表單用戶名和口令值。

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. 建立`java.io.File`物件，擷取要傳送至`MyApplication/EncryptDocument`服務的PDF檔案。 傳遞指定PDF檔案位置的字串值。
1. 使用其建構子並傳遞`javax.activation.FileDataSource`對象，建立`javax.activation.DataHandler`對象。 `javax.activation.FileDataSource`物件可使用其建構函式並傳遞代表PDF檔案的`java.io.File`物件來建立。
1. 使用其建構子並傳遞`javax.activation.DataHandler`對象，建立`org.apache.axis.attachments.AttachmentPart`對象。
1. 通過調用`EncryptDocumentSoapBindingStub`對象的`addAttachment`方法並傳遞`org.apache.axis.attachments.AttachmentPart`對象來附加附件。
1. 使用其建構子建立`BLOB`對象。 調用`BLOB`對象的`setAttachmentID`方法並傳遞附件標識符值，以附件標識符值填充`BLOB`對象。 此值可透過叫用`org.apache.axis.attachments.AttachmentPart`物件的`getContentId`方法來取得。
1. 叫用`EncryptDocumentSoapBindingStub`物件的`invoke`方法，以叫用`MyApplication/EncryptDocument`程式。 傳遞包含DIME附件的`BLOB`物件。 此程式會傳回`BLOB`物件內的加密PDF檔案。
1. 通過調用返回的`BLOB`對象的`getAttachmentID`方法來獲取附件標識符值。 此方法會傳回字串值，代表傳回之附件的識別碼值。
1. 調用`EncryptDocumentSoapBindingStub`對象的`getAttachments`方法來檢索附件。 此方法返回代表附件的`Objects`陣列。
1. 重複附件（`Object`陣列），並使用附件標識符值來獲取加密的PDF文檔。 每個元素都是`org.apache.axis.attachments.AttachmentPart`物件。
1. 通過調用`org.apache.axis.attachments.AttachmentPart`對象的`getDataHandler`方法，獲取與附件關聯的`javax.activation.DataHandler`對象。
1. 調用`javax.activation.DataHandler`物件的`getInputStream`方法，以取得`java.io.FileStream`物件。
1. 建立位元組陣列，並將該位元組陣列傳遞至`java.io.FileStream`物件的`read`方法。 此方法會以代表加密PDF檔案的資料流填入位元組陣列。
1. 使用其建構子建立`java.io.File`對象。 此物件代表加密的PDF檔案。
1. 使用其建構子並傳遞`java.io.File`對象，建立`java.io.FileOutputStream`對象。
1. 叫用`java.io.FileOutputStream`物件的`write`方法，並傳遞包含代表加密PDF檔案之資料流的位元組陣列。

**另請參閱**

[快速入門：在Java專案中使用DIME叫用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## 使用SAML驗證{#using-saml-based-authentication}

AEM Forms在調用服務時支援各種Web服務驗證模式。 一種驗證模式是使用web service呼叫中的基本授權標題同時指定用戶名和口令值。 AEM Forms也支援SAML斷言式驗證。 當客戶端應用程式使用web服務調用AEM Forms服務時，客戶端應用程式可以以下列方式之一提供驗證資訊：

* 將認證傳入基本授權
* 將使用者名稱Token傳遞為WS-Security標題的一部分
* 將SAML斷言傳遞為WS-Security標題的一部分
* 將Kerberos令牌作為WS-Security標頭的一部分傳遞

AEM Forms不支援標準的憑證式驗證，但支援不同形式的憑證式驗證。

>[!NOTE]
>
>Web服務快速啟動於「使用AEM Forms進行寫程式」，指定用戶名和密碼值以執行授權。

表單使用AEM者的身分可透過使用機密金鑰簽署的SAML斷言來表示。 下列XML程式碼顯示SAML斷言的範例。

```xml
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

此示例斷言是為管理員用戶發出的。 此斷言包含下列值得注意的項目：

* 它在特定期間有效。
* 它是針對特定使用者所核發。
* 它是數位簽署的。 因此，任何修改都會破壞簽名。
* 它可以呈現給AEM Forms，作為與用戶名和密碼類似的用戶標識的令牌。

客戶端應用程式可以從任何返回`AuthResult`對象的AEM FormsAuthenticationManager API中檢索斷言。 通過執行以下兩種方法之一，可以獲得`AuthResult`實例：

* 使用AuthenticationManager API公開的任何驗證方法驗證使用者。 通常，使用者會使用使用者名稱和密碼；不過，您也可以使用憑證驗證。
* 使用`AuthenticationManager.getAuthResultOnBehalfOfUser`方法。 此方法可讓用戶端應用程式取得任何表單使用者的`AuthResult`AEM物件。

表AEM單使用者可使用所取得的SAML Token進行驗證。 此SAML斷言（xml片段）可隨Web服務呼叫使用者驗證一起傳送，作為WS-Security標題的一部分。 通常，客戶端應用程式已驗證用戶，但未儲存用戶憑據。 （或者，使用者已透過使用使用者名稱和密碼以外的機制登入該用戶端。） 在這種情況下，客戶端應用程式必須調用AEM Forms並模擬允許調用AEM Forms的特定用戶。

若要模擬特定使用者，請使用web services叫用`AuthenticationManager.getAuthResultOnBehalfOfUser`方法。 此方法會傳回包含該使用者之SAML斷言的`AuthResult`例項。

接著，使用該SAML斷言來叫用任何需要驗證的服務。 此操作涉及將斷言作為SOAP標題的一部分發送。 當使用此斷言進行Web服務調用時，AEM Forms將用戶標識為由該斷言表示的用戶。 也就是說，斷言中指定的用戶是調用服務的用戶。

### 使用Apache Axis類和基於SAML的驗證{#using-apache-axis-classes-and-saml-based-authentication}

可以通過使用Axis庫建立的Java代理類調用AEM Forms服務。 （請參閱[使用Apache Axis](#creating-java-proxy-classes-using-apache-axis)建立Java代理類。）

當使用使用SAML驗證的AXIS時，請使用Axis註冊請求和回應處理常式。 Apache Axis會先叫用處理常式，再傳送呼叫請求至AEM Forms。 要註冊處理程式，請建立擴展`org.apache.axis.handlers.BasicHandler`的Java類。

**建立具有軸的AssertionHandler**

以下名為`AssertionHandler.java`的Java類顯示了擴展`org.apache.axis.handlers.BasicHandler`的Java類的示例。

```java
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**註冊處理常式**

要向Axis註冊處理程式，請建立client-config.wsdd檔案。 預設情況下，Axis查找具有此名稱的檔案。 以下XML程式碼是client-config.wsdd檔案的範例。 如需詳細資訊，請參閱Axis檔案。

```xml
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**叫用AEM Forms服務**

下列程式碼範例使用SAML驗證叫用AEM Forms服務。

```java
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### 使用。NET客戶端元件和基於SAML的驗證{#using-a-net-client-assembly-and-saml-based-authentication}

您可以使用。NET用戶端元件和SAML驗證來叫用Forms服務。 若要這麼做，您必須使用Web服務增強功能3.0(WSE)。 有關建立使用WSE的。NET客戶端程式集的資訊，請參見[建立使用DIME](#creating-a-net-project-that-uses-dime)的。NET項目。

>[!NOTE]
>
>DIME部分使用WSE 2.0。若要使用SAML驗證，請遵循與DIME主題中指定的相同指示。 不過，請將WSE 2.0替換為WSE 3.0。在您的開發電腦上安裝Web Services Enhancements 3.0，並將它與Microsoft Visual Studio .NET整合。 您可以從[Microsoft下載中心](https://www.microsoft.com/downloads/search.aspx)下載Web Services Enhancements 3.0。

WSE體系結構使用策略、斷言和SecurityToken資料類型。 簡而言之，若為web service呼叫，請指定原則。 策略可以有多個斷言。 每個斷言都可以包含篩選器。 在Web服務呼叫的特定階段會呼叫篩選器，當時可修改SOAP要求。 如需完整詳細資訊，請參閱Web Service Enhancements 3.0檔案。

**建立斷言和篩選**

以下C#代碼示例建立過濾器和斷言類。 此程式碼範例會建立SamlAssertionOutputFilter。 在將SOAP請求發送到AEM Forms之前，WSE框架會調用此過濾器。

```java
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**建立SAML Token**

建立類別以表示SAML斷言。 此類執行的主要任務是將資料值從字串轉換為xml並保留空格。 此斷言xml稍後會匯入至SOAP請求。

```java
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**叫用AEM Forms服務**

以下C#程式碼範例使用SAML驗證來叫用Forms服務。

```java
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## 使用web services {#related-considerations-when-using-web-services}時的相關考量

有時，當使用web services調用某些AEM Forms服務操作時會發生問題。 本次討論的目的是確定這些問題並提供解決辦法（如果有）。

### 非同步調用服務操作{#invoking-service-operations-asynchronously}

如果您嘗試非同步地叫用AEM Forms服務作業，例如產生PDF的`htmlToPDF`作業，則會發生`SoapFaultException`。 若要解決此問題，請建立自訂系結XML檔案，將`ExportPDF_Result`元素和其他元素對應至不同的類別。 以下XML代表自訂系結檔案。

```xml
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

使用JAX-WS建立Java代理檔案時使用此XML檔案。 （請參閱[使用JAX-WS](#creating-java-proxy-classes-using-jax-ws)建立Java代理類。）

使用- `b`命令行選項執行JAX-WS工具(wsimport.exe)時，請參考此XML檔案。 更新綁定XML檔案中的`wsdlLocation`元素，以指定AEM Forms的URL。

若要確保非同步呼叫正常運作，請修改端點URL值並指定`async=true`。 例如，對於使用JAX-WS建立的Java代理檔案，請為`BindingProvider.ENDPOINT_ADDRESS_PROPERTY`指定以下內容。

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

以下清單指定非同步調用時需要自定義綁定檔案的其他服務：

* PDFG3D
* 任務管理器
* 應用程式管理員
* 目錄管理器
* Distiller
* 版權管理
* 檔案管理

### J2EE應用程式伺服器{#differences-in-j2ee-application-servers}的差異

有時，使用特定J2EE應用程式伺服器建立的代理程式庫無法成功叫用其他J2EE應用程式伺服器上裝載的AEM Forms。 考慮使用部署在WebSphere上的AEM Forms產生的代理程式庫。 此代理庫無法成功調用部署在JBoss Application Server上的AEM Forms服務。

與JBoss Application Server相比，在WebSphere上部署AEM Forms時，某些AEM Forms複雜資料類型（如`PrincipalReference`）的定義不同。 不同J2EE應用程式服務使用的JDK差異，是WSDL定義有差異的原因。 因此，請使用從相同J2EE應用程式伺服器產生的Proxy程式庫。

### 使用web services {#accessing-multiple-services-using-web-services}訪問多個服務

由於名稱空間衝突，資料物件無法在多個服務WSDL之間共用。 不同的服務可以共用資料類型，因此服務可以在WSDL中共用這些類型的定義。 例如，不能將包含`BLOB`資料類型的兩個。NET客戶端程式集添加到同一。NET客戶端項目。 如果您嘗試這麼做，則會發生編譯錯誤。

以下清單指定不能在多個服務WSDL之間共用的資料類型：

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

為避免此問題，建議您完全限定資料類型。 例如，請考慮使用服務引用同時引用Forms服務和簽名服務的。NET應用程式。 兩個服務引用都將包含`BLOB`類。 要使用`BLOB`實例，請在聲明`BLOB`對象時完全限定該對象。 以下代碼示例顯示了此方法。 如需此程式碼範例的詳細資訊，請參閱[數位簽署互動式Forms](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)。

下列C#程式碼範例會簽署由Forms服務轉譯的互動式表單。 客戶端應用程式有兩個服務引用。 與Forms服務關聯的`BLOB`實例屬於`SignInteractiveForm.ServiceReference2`命名空間。 同樣地，與簽名服務關聯的`BLOB`實例也屬於`SignInteractiveForm.ServiceReference1`命名空間。 簽署的互動式表單會儲存為名為&#x200B;*LoanXFASpid.pdf*&#x200B;的PDF檔案。

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully-qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify a XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify a XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### 服務從字母I開始生成無效的代理檔案{#services-starting-with-the-letter-i-produce-invalid-proxy-files}

使用Microsoft .Net 3.5和WCF時，某些AEM Forms生成的代理類的名稱不正確。 當為IBMFilenetContentRepositoryConnector、IDPShedulerService或任何其他名稱以字母I開頭的服務建立代理類時，就會發生此問題。例如，在IBMFileNetContentRepositoryConnector的情況下，生成的客戶機的名稱為`BMFileNetContentRepositoryConnectorClient`。 生成的代理類中缺少的字母I。

