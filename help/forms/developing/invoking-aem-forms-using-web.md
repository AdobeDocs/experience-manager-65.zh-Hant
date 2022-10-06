---
title: 使用Web服務叫用AEM Forms
seo-title: Invoking AEM Forms using Web Services
description: 使用完全支援WSDL生成的Web服務調用AEM Forms進程。
seo-description: Invoke AEM Forms processes using web services with full support for WSDL generation.
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
role: Developer
exl-id: 3139564f-9346-4933-8e39-2e1642bff097
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '9905'
ht-degree: 0%

---

# 使用Web服務叫用AEM Forms {#invoking-aem-forms-using-web-services}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

服務容器中的大多數AEM Forms服務都配置為公開Web服務，完全支援生成Web服務定義語言(WSDL)。 也就是說，您可以建立代理物件，使用AEM Forms服務的原生SOAP堆疊。 因此，AEM Forms服務可以交換及處理下列SOAP訊息：

* **SOAP請求**:由要求動作的用戶端應用程式傳送至Forms服務。
* **SOAP響應**:在處理SOAP請求後，由Forms服務傳送至用戶端應用程式。

使用網站服務，您可以執行與使用Java API相同的AEM Forms服務作業。 使用Web服務來叫用AEM Forms服務的好處是，您可以在支援SOAP的開發環境中建立用戶端應用程式。 客戶端應用程式不綁定到特定的開發環境或寫程式語言。 例如，您可以使用Microsoft Visual Studio .NET和C#作為寫程式語言來建立客戶端應用程式。

AEM Forms服務會透過SOAP通訊協定公開，且符合WSI基本設定檔1.1。 Web服務互操作性(WSI)是一個開放標準組織，它促進了不同平台間的Web服務互操作性。 如需詳細資訊，請參閱 [https://www.ws-i.org/](https://www.ws-i.org).

AEM Forms支援下列網站服務標準：

* **編碼**:僅支援文檔和常值編碼（根據WSI基本配置檔案，這是首選編碼）。 (請參閱 [使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**:表示使用SOAP請求對附件進行編碼的方法。 (請參閱 [使用MTOM叫用AEM Forms](#invoking-aem-forms-using-mtom).)
* **SwaRef**:表示另一種使用SOAP請求對附件進行編碼的方法。 (請參閱 [使用SwaRef叫用AEM Forms](#invoking-aem-forms-using-swaref).)
* **附件的SOAP**:支援MIME和DIME（直接Internet消息封裝）。 這些通訊協定是透過SOAP傳送附件的標準方式。 Microsoft Visual Studio .NET應用程式使用DIME。 (請參閱 [使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**:支援用戶名密碼令牌配置檔案，這是作為WS Security SOAP標頭的一部分發送用戶名和密碼的標準方式。 AEM Forms也支援HTTP基本驗證。 s

若要使用Web服務叫用AEM Forms服務，通常需建立會使用服務WSDL的代理程式庫。 此 *使用Web服務叫用AEM Forms* 節使用JAX-WS建立Java代理類以調用服務。 (請參閱 [使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws).)

您可以指定下列URL定義來擷取服務WDSL（方括弧中的項目為選用項目）:

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

其中：

* *your_serverhost* 代表托管AEM Forms的J2EE應用程式伺服器的IP位址。
* *your_port* 表示J2EE應用程式伺服器使用的HTTP埠。
* *service_name* 代表服務名稱。
* *版本* 代表服務的目標版本（預設會使用最新的服務版本）。
* `async` 指定值 `true` 啟用非同步調用的其他操作( `false` )。
* *lc_version* 代表您要叫用的AEM Forms版本。

下表列出了服務WSDL定義(假設已在本地主機上部署了AEM Forms，而貼文為8080)。

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
   <td><p>返回和還原</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>條碼式表單</p></td>
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
   <td><p>DocumentManagement</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>加密 </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Forms</p></td>
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
   <td><p>生成3DPDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>輸出</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>PDF實用程式 </p></td>
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
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>簽名 </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>XMP公用程式</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**AEM Forms進程WSDL定義**

您必須在WSDL定義中指定應用程式名稱和進程名稱，才能訪問屬於在Workbench中建立的進程的WSDL。 假設應用程式的名稱為 `MyApplication` 進程的名稱是 `EncryptDocument`. 在這種情況下，請指定以下WSDL定義：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>如需範例的相關資訊 `MyApplication/EncryptDocument` 短期過程 [短期流程示例](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>應用程式可以包含資料夾。 在這種情況下，請在WSDL定義中指定資料夾名稱：

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**使用網站服務存取新功能**

新的AEM Forms服務功能可使用網站服務來存取。 例如，在AEM Forms中，引入了使用MTOM對附件進行編碼的功能。 (請參閱 [使用MTOM叫用AEM Forms](#invoking-aem-forms-using-mtom).)

若要存取AEM Forms推出的新功能，請指定 `lc_version` 屬性。 例如，要訪問新服務功能（包括MTOM支援），請指定以下WSDL定義：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>設定 `lc_version` 屬性，請確定您使用三位數。 例如，9.0.1等於9.0版。

**Web服務BLOB資料類型**

AEM Forms服務WSDL定義了許多資料類型。 網站服務中公開的最重要資料類型之一，是 `BLOB` 類型。 此資料類型會對應至 `com.adobe.idp.Document` 類別。 (請參閱 [使用Java API將資料傳遞至AEM Forms服務](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

A `BLOB` 物件會傳送二進位資料(例如PDF檔案、XML資料等)至AEM Forms服務，並從中擷取二進位資料。 此 `BLOB` 類型在服務WSDL中定義如下：

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

此 `MTOM` 和 `swaRef` 只有AEM Forms支援欄位。 只有當您指定包含 `lc_version` 屬性。

**在服務請求中提供BLOB對象**

如果AEM Forms服務作業需要 `BLOB` 輸入值，建立例項 `BLOB` 輸入應用程式邏輯。 (許多Web服務快速入門位於 *使用AEM表單進行程式設計* 顯示如何使用BLOB資料類型。)

將值指派給屬於 `BLOB` 例項如下：

* **Base64**:若要以Base64格式編碼的文字來傳遞資料，請在 `BLOB.binaryData` 欄位，並以MIME格式設定資料類型(例如 `application/pdf`) `BLOB.contentType` 欄位。 (請參閱 [使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**:若要在MTOM附件中傳遞二進位資料，請在 `BLOB.MTOM` 欄位。 此設定使用Java JAX-WS框架或SOAP框架的本機API將資料附加到SOAP請求。 (請參閱 [使用MTOM叫用AEM Forms](#invoking-aem-forms-using-mtom).)
* **SwaRef**:要在WS-I SwaRef附件中傳遞二進位資料，請在 `BLOB.swaRef` 欄位。 此設定使用Java JAX-WS框架將資料附加到SOAP請求。 (請參閱 [使用SwaRef叫用AEM Forms](#invoking-aem-forms-using-swaref).)
* **MIME或DIME附件**:若要以MIME或DIME附件傳送資料，請使用SOAP架構的原生API將資料附加至SOAP請求。 在 `BLOB.attachmentID` 欄位。 (請參閱 [使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding).)
* **遠端URL**:如果資料托管於Web伺服器且可透過HTTP URL存取，請在 `BLOB.remoteURL` 欄位。 (請參閱 [透過HTTP使用BLOB資料叫用AEM Forms](#invoking-aem-forms-using-blob-data-over-http).)

**訪問從服務返回的BLOB對象中的資料**

返回的傳輸協定 `BLOB` 對象取決於多個因素，按以下順序進行考慮，在滿足主要條件時停止：

1. **目標URL指定傳輸協定**. 如果在SOAP調用中指定的目標URL包含參數 `blob="`*BLOB_TYPE*&quot;，然後 *BLOB_TYPE* 確定傳輸協定。 *BLOB_TYPE* 是base64、dime、mime、http、mtom或swaref的預留位置。
1. **服務SOAP端點是Smart**. 如果以下條件為真，則使用與輸入文檔相同的傳輸協定返回輸出文檔：

   * 輸出Blob對象的服務的SOAP端點參數預設協定設定為Smart。

      對於每個具有SOAP端點的服務，管理控制台允許您為任何返回的Blob指定傳輸協定。 (請參閱 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * AEM Forms服務會以一或多個檔案作為輸入。

1. **服務SOAP端點不是智慧的**. 配置的協定確定文檔傳輸協定，並且在相應的 `BLOB` 欄位。 例如，如果SOAP端點設為DIME，則傳回的blob位於 `blob.attachmentID` 欄位，而不考慮任何輸入檔案的傳輸協定。
1. **否則**. 如果服務沒有將文檔類型作為輸入，則輸出文檔將在 `BLOB.remoteURL` 欄位。

如第一個條件所述，您可以通過擴展尾碼為SOAP端點URL來確保任何返回文檔的傳輸類型，如下所示：

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

以下是傳輸類型與從中獲取資料的欄位之間的關聯：

* **Base64格式**:設定 `blob` 尾碼 `base64` 若要傳回 `BLOB.binaryData` 欄位。
* **MIME或DIME附件**:設定 `blob` 尾碼 `DIME` 或 `MIME` 將資料傳回為對應的附件類型，並在 `BLOB.attachmentID` 欄位。 使用SOAP框架的專有API從附件中讀取資料。
* **遠端URL**:設定 `blob` 尾碼 `http` 將資料保留在應用程式伺服器上，並傳回指向 `BLOB.remoteURL` 欄位。
* **MTOM或SwaRef**:設定 `blob` 尾碼 `mtom` 或 `swaref` 將資料傳回為對應的附件類型，並在 `BLOB.MTOM` 或 `BLOB.swaRef` 欄位。 使用SOAP框架的本機API從附件讀取資料。

>[!NOTE]
>
>建議您在填入 `BLOB` 對象 `setBinaryData` 方法。 否則，可能 `OutOfMemory` 異常。

>[!NOTE]
>
>使用MTOM傳輸協定的基於JAX WS的應用程式限制為25MB的已發送和已接收資料。 此限制是由於JAX-WS中的錯誤。 如果已發送和已接收檔案的總大小超過25MB，請使用SwaRef傳輸協定，而不是MTOM協定。 否則，可能 `OutOfMemory` 例外。

**基於64編碼位元組陣列的MTOM傳輸**

除了 `BLOB` 對象，則MTOM協定支援任何複雜類型的位元組陣列參數或位元組陣列欄位。 這表示支援MTOM的用戶端SOAP架構可傳送任何 `xsd:base64Binary` 元素作為MTOM附件（而非base64編碼的文字）。 AEM Forms SOAP端點可以讀取此類型的位元組陣列編碼。 不過，AEM Forms服務一律會傳回位元組陣列類型，作為base64編碼文字。 輸出位元組陣列參數不支援MTOM。

傳回大量二進位資料的AEM Forms服務會使用Document/BLOB類型，而非位元組陣列類型。 對於傳輸大量資料而言，「文檔」類型要高效得多。

## Web服務資料類型 {#web-service-data-types}

下表列出Java資料類型，並顯示對應的Web服務資料類型。

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
   <td><p>此 <code>DATE</code> 類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務作業 <code>java.util.Date</code> 值作為輸入，SOAP用戶端應用程式必須將日期傳入 <code>DATE.date</code> 欄位。 設定 <code>DATE.calendar</code> 在此情況下，欄位會造成執行階段例外。 如果服務傳回 <code>java.util.Date</code>，則日期會在 <code>DATE.date</code> 欄位。</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>此 <code>DATE</code> 類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務作業 <code>java.util.Calendar</code> 值作為輸入，SOAP用戶端應用程式必須將日期傳入 <code>DATE.caledendar</code> 欄位。 設定 <code>DATE.date</code> 在此情況下，欄位會造成執行時例外。 如果服務傳回 <code>java.util.Calendar</code>，則會在 <code>DATE.calendar</code> 欄位。 </p></td>
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
   <td><p>此 <code>apachesoap:Map</code>，在服務WSDL中定義如下：</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>地圖會以索引鍵/值組的順序呈現。</p></td>
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
   <td><p>XML類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務操作接受 <code>org.w3c.dom.Document</code> 值，請將XML資料傳入 <code>XML.document</code> 欄位。</p><p>設定 <code>XML.element</code> 欄位會造成執行階段例外。 如果服務傳回 <code>org.w3c.dom.Document</code>，則會在 <code>XML.document</code> 欄位。</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>XML類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務作業 <code>org.w3c.dom.Element</code> 作為輸入，將XML資料傳入 <code>XML.element</code> 欄位。</p><p>設定 <code>XML.document</code> 欄位會造成執行階段例外。 如果服務傳回 <code>org.w3c.dom.Element</code>，則會在 <code>XML.element</code> 欄位。</p></td>
  </tr>
 </tbody>
</table>

## 使用JAX-WS建立Java代理類 {#creating-java-proxy-classes-using-jax-ws}

可以使用JAX-WS將Forms服務WSDL轉換為Java代理類。 這些類別可讓您叫用AEM Forms服務作業。 Apache Ant可讓您建立生成指令碼，該指令碼通過引用AEM Forms服務WSDL來生成Java代理類。 通過執行以下步驟，可以生成JAX-WS代理檔案：

1. 在客戶端電腦上安裝Apache Ant。 (請參閱 [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * 將bin目錄添加到類路徑。
   * 設定 `ANT_HOME` 環境變數到安裝Ant的目錄。

1. 安裝JDK 1.6或更高版本。

   * 將JDK bin目錄添加到類路徑。
   * 將JRE bin目錄添加到類路徑。 此倉位於 `[JDK_INSTALL_LOCATION]/jre` 目錄。
   * 設定 `JAVA_HOME` 環境變數至您安裝JDK的目錄。

   JDK 1.6包括build.xml檔案中使用的wsimport程式。 JDK 1.5不包含該程式。

1. 在客戶端電腦上安裝JAX-WS。 (請參閱 [Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. 使用JAX-WS和Apache Ant生成Java代理類。 建立Ant生成指令碼以完成此任務。 以下指令碼是名為build.xml的示例Ant生成指令碼：

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

   在此Ant生成指令碼中，請注意 `url` 屬性設定為引用本地主機上運行的加密服務WSDL。 此 `username` 和 `password` 屬性必須設定為有效的AEM forms用戶名和密碼。 請注意，URL包含 `lc_version` 屬性。 不指定 `lc_version` 選項，則無法叫用新的AEM Forms服務作業。

   >[!NOTE]
   >
   >取代 `EncryptionService`使用您要使用Java代理類調用的AEM Forms服務名。 例如，要為Rights Management服務建立Java代理類，請指定：

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. 建立BAT檔案以執行Ant生成指令碼。 以下命令可位於負責執行Ant生成指令碼的BAT檔案中：

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   將ANT生成指令碼放在C:\Program Files\Java\jaxws-ri\bin directory中。 指令碼會將JAVA檔案寫入。/classes資料夾。 指令碼會產生可叫用服務的JAVA檔案。

1. 將JAVA檔案封裝為JAR檔案。 如果您使用Eclipse，請依照下列步驟操作：

   * 建立新的Java項目，用於將代理JAVA檔案包裝到JAR檔案中。
   * 在專案中建立來源資料夾。
   * 建立 `com.adobe.idp.services` 包。
   * 選取 `com.adobe.idp.services` 套件，然後從adobe/idp/services資料夾匯入JAVA檔案至套件。
   * 如有必要，請建立 `org/apache/xml/xmlsoap` 包。
   * 選取來源資料夾，然後從org/apache/xml/xmlsoap資料夾匯入JAVA檔案。
   * 將Java編譯器的合規性級別設定為5.0或更高。
   * 建立專案。
   * 將專案匯出為JAR檔案。
   * 將此JAR檔案導入客戶端項目的類路徑。 此外，匯入位於 &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty。

   >[!NOTE]
   >
   >使用AEM表單寫程式時，位於「使用JAX-WS建立Java代理檔案」中的所有Java Web服務快速啟動(Forms服務除外)。 此外，所有Java Web服務都快速啟動，請使用SwaRef。 (請參閱 [使用SwaRef叫用AEM Forms](#invoking-aem-forms-using-swaref).)

**另請參閱**

[使用Apache Axis建立Java代理類](#creating-java-proxy-classes-using-apache-axis)

[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[透過HTTP使用BLOB資料叫用AEM Forms](#invoking-aem-forms-using-blob-data-over-http)

[使用SwaRef叫用AEM Forms](#invoking-aem-forms-using-swaref)

## 使用Apache Axis建立Java代理類 {#creating-java-proxy-classes-using-apache-axis}

您可以使用Apache Axis WSDL2Java工具將Forms服務轉換為Java代理類。 這些類別可讓您叫用Forms服務作業。 使用Apache Ant，可以從服務WSDL生成Axis庫檔案。 您可以在URL下載Apache Axis [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>與Forms服務相關聯的Web服務快速入門使用使用Apache Axis建立的Java代理類。 Forms Web服務快速入門也使用Base64作為編碼類型。 (請參閱 [Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

通過執行以下步驟，可以生成Axis Java庫檔案：

1. 在客戶端電腦上安裝Apache Ant。 可於 [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * 將bin目錄添加到類路徑。
   * 設定 `ANT_HOME` 環境變數到安裝Ant的目錄。

1. 在用戶端電腦上安裝Apache Axis 1.4。 可於 [https://ws.apache.org/axis/](https://ws.apache.org/axis/).
1. 設定類路徑以在Web服務客戶端中使用Axis JAR檔案，如Axis安裝說明中所述： [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. 使用Axis中的Apache WSDL2Java工具生成Java代理類。 建立Ant生成指令碼以完成此任務。 以下指令碼是名為build.xml的示例Ant生成指令碼：

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

   在此Ant生成指令碼中，請注意 `url` 屬性設定為引用本地主機上運行的加密服務WSDL。 此 `username` 和 `password` 屬性必須設定為有效的AEM forms用戶名和密碼。

1. 建立BAT檔案以執行Ant生成指令碼。 以下命令可位於負責執行Ant生成指令碼的BAT檔案中：

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA檔案將寫入C:\JavaFiles folder as specified by the `output` 屬性。 若要成功叫用Forms服務，請將這些JAVA檔案匯入您的類別路徑。

   依預設，這些檔案屬於名為 `com.adobe.idp.services`. 建議您將這些JAVA檔案放入JAR檔案中。 然後將JAR檔案導入客戶端應用程式的類路徑。

   >[!NOTE]
   >
   >將.JAVA檔案放入JAR有不同的方法。 一種方式是使用Java IDE，如Eclipse。 建立Java專案並建立 `com.adobe.idp.services`包（所有.JAVA檔案均屬於此包）。 接下來，將所有.JAVA檔案匯入套件中。 最後，將專案匯出為JAR檔案。

1. 修改 `EncryptionServiceLocator` 類，以指定編碼類型。 例如，若要使用base64，請指定 `?blob=base64` 確保 `BLOB` 對象返回二進位資料。 即，在 `EncryptionServiceLocator` 類，請找到以下代碼行：

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   並將其變更為：

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. 將以下Axis JAR檔案添加到Java項目的類路徑中：

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-api-2.5.0.jar
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

   這些JAR檔案位於 `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` 目錄。

**另請參閱**

[使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws)

[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[透過HTTP使用BLOB資料叫用AEM Forms](#invoking-aem-forms-using-blob-data-over-http)

## 使用Base64編碼叫用AEM Forms {#invoking-aem-forms-using-base64-encoding}

您可以使用Base64編碼叫用AEM Forms服務。 Base64編碼對隨Web服務調用請求發送的附件進行編碼。 就是說， `BLOB` 資料是Base64編碼，而不是整個SOAP消息。

「使用Base64編碼叫用AEM Forms」討論叫用以下AEM Forms短期處理程式，命名為 `MyApplication/EncryptDocument` 使用Base64編碼。

>[!NOTE]
>
>此程式並非以現有的AEM Forms程式為基礎。 若要遵循程式碼範例，請建立以下程式： `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

叫用此程式時，會執行下列動作：

1. 獲取傳遞至流程的不安全PDF文檔。 此動作以 `SetValue` 操作。 此程式的輸入參數為 `document` 進程變數已命名 `inDoc`.
1. 使用密碼加密PDF文檔。 此動作以 `PasswordEncryptPDF` 操作。 密碼加密的PDF文檔在名為的進程變數中返回 `outDoc`.

### 建立使用Base64編碼的.NET客戶端程式集 {#creating-a-net-client-assembly-that-uses-base64-encoding}

您可以建立.NET客戶端程式集，從Microsoft Visual Studio .NET項目調用Forms服務。 要建立使用base64編碼的.NET客戶端程式集，請執行以下步驟：

1. 根據AEM Forms叫用URL建立Proxy類別。
1. 建立生成.NET客戶端程式集的Microsoft Visual Studio .NET項目。

**建立代理類**

您可以使用Microsoft Visual Studio附帶的工具，建立用於建立.NET客戶端程式集的代理類。 工具的名稱為wsdl.exe，位於Microsoft Visual Studio安裝資料夾中。 要建立代理類，請開啟命令提示符並導航到包含wsdl.exe檔案的資料夾。 有關wsdl.exe工具的詳細資訊，請參見 *MSDN幫助*.

在命令提示符下輸入以下命令：

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

預設情況下，此工具會在基於WSDL名稱的同一資料夾中建立CS檔案。 在此情況下，會建立名為 *EncryptDocumentService.cs*. 您可使用此CS檔案建立代理對象，該對象允許您調用調用URL中指定的服務。

修改Proxy類別中的URL以包括 `?blob=base64` 確保 `BLOB` 對象返回二進位資料。 在Proxy類別中，找出下列程式碼行：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

並將其變更為：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

此 *使用Base64編碼叫用AEM Forms* 區段使用 `MyApplication/EncryptDocument` 作為範例。 如果要為其他Forms服務建立.NET客戶端程式集，請確保替換 `MyApplication/EncryptDocument` 和服務的名稱。

**開發.NET客戶端程式集**

建立生成.NET客戶端程式集的Visual Studio類庫項目。 可以將使用wsdl.exe建立的CS檔案導入此項目。 此項目將生成一個DLL檔案（.NET客戶端程式集），您可以在其他Visual Studio .NET項目中使用該檔案來調用服務。

1. 啟動Microsoft Visual Studio .NET。
1. 建立類庫項目，並將其命名為DocumentService。
1. 導入使用wsdl.exe建立的CS檔案。
1. 在 **專案** 菜單，選擇 **新增參考**.
1. 在「添加引用」(Add Reference)對話框中，選擇 **System.Web.Services.dll**.
1. 按一下 **選擇** 然後按一下 **確定**.
1. 編譯並建置專案。

>[!NOTE]
>
>此過程將建立一個名為DocumentService.dll的.NET客戶端程式集，您可以用它將SOAP請求發送到 `MyApplication/EncryptDocument` 服務。

>[!NOTE]
>
>請確定您已新增 `?blob=base64` 到用於建立.NET客戶端程式集的代理類中的URL。 否則，您無法從 `BLOB` 物件。

**引用.NET客戶端程式集**

將新建立的.NET客戶端程式集放置在正在開發客戶端應用程式的電腦上。 將.NET客戶端程式集放置到目錄後，可以從項目中引用它。 另請參考 `System.Web.Services` 程式庫。 如果未引用此庫，則不能使用.NET客戶端程式集調用服務。

1. 在 **專案** 菜單，選擇 **新增參考**.
1. 按一下 **.NET** 標籤。
1. 按一下 **瀏覽** 並找到DocumentService.dll檔案。
1. 按一下 **選擇** 然後按一下 **確定**.

**使用使用Base64編碼的.NET客戶端程式集調用服務**

您可以叫用 `MyApplication/EncryptDocument` 使用使用Base64編碼的.NET用戶端程式集的服務（內建於Workbench中）。 叫用 `MyApplication/EncryptDocument` 服務，請執行以下步驟：

1. 建立使用的Microsoft .NET客戶端程式集 `MyApplication/EncryptDocument` 服務WSDL。
1. 建立客戶端Microsoft .NET項目。 在客戶端項目中引用Microsoft .NET客戶端程式集。 也參考 `System.Web.Services`.
1. 使用Microsoft .NET客戶端程式集，建立 `MyApplication_EncryptDocumentService` 對象，方法是調用其預設建構子。
1. 設定 `MyApplication_EncryptDocumentService` 物件 `Credentials` 具有 `System.Net.NetworkCredential` 物件。 在 `System.Net.NetworkCredential` 建構函式，指定AEM表單使用者名稱和對應的密碼。 設定驗證值，使您的.NET客戶端應用程式能夠成功與AEM Forms交換SOAP消息。
1. 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存PDF文檔傳遞到 `MyApplication/EncryptDocument` 程式。
1. 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
1. 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
1. 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
1. 填入 `BLOB` 對象，通過賦值 `binaryData` 屬性（包含位元組陣列的內容）。
1. 叫用 `MyApplication/EncryptDocument` 程式，方法是叫用 `MyApplication_EncryptDocumentService` 物件 `invoke` 方法和傳遞 `BLOB` 包含PDF文檔的對象。 此程式會在 `BLOB` 物件。
1. 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示密碼加密文檔的檔案位置。
1. 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `MyApplicationEncryptDocumentService` 物件 `invoke` 方法。 取得 `BLOB` 物件 `binaryData` 資料成員。
1. 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
1. 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

### 使用Java代理類和Base64編碼調用服務 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

您可以使用Java代理類和Base64調用AEM Forms服務。 叫用 `MyApplication/EncryptDocument` 服務，請執行以下步驟：

1. 使用JAX-WS建立Java代理類，該類使用 `MyApplication/EncryptDocument` 服務WSDL。 使用以下WSDL端點：

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >取代 `hiro-xp` *包含AEM Forms之J2EE應用程式伺服器的IP位址。*

1. 將使用JAX-WS建立的Java代理類打包到JAR檔案中。
1. 包括位於以下路徑中的Java代理JAR檔案和JAR檔案：

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   進入Java客戶端項目的類路徑。

1. 建立 `MyApplicationEncryptDocumentService` 物件，使用其建構子。
1. 建立 `MyApplicationEncryptDocument` 對象，方法是調用 `MyApplicationEncryptDocumentService` 物件 `getEncryptDocument` 方法。
1. 將值指派給下列資料成員，以設定叫用AEM Forms所需的連線值：

   * 將WSDL端點和編碼類型指派給 `javax.xml.ws.BindingProvider` 物件 `ENDPOINT_ADDRESS_PROPERTY` 欄位。 叫用 `MyApplication/EncryptDocument` 使用Base64編碼的服務，請指定以下URL值：

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * 將AEM表單使用者指派至 `javax.xml.ws.BindingProvider` 物件 `USERNAME_PROPERTY` 欄位。
   * 將對應的密碼值指派給 `javax.xml.ws.BindingProvider` 物件 `PASSWORD_PROPERTY` 欄位。

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

1. 檢索要發送到的PDF文檔 `MyApplication/EncryptDocument` 程式 `java.io.FileInputStream` 物件，使用其建構子。 傳遞指定PDF文檔位置的字串值。
1. 建立位元組陣列，並將 `java.io.FileInputStream` 物件。
1. 建立 `BLOB` 物件，使用其建構子。
1. 填入 `BLOB` 對象 `setBinaryData` 方法，並傳遞位元組陣列。 此 `BLOB` 物件 `setBinaryData` 是使用Base64編碼時要呼叫的方法。 請參閱在服務請求中提供BLOB對象。
1. 叫用 `MyApplication/EncryptDocument` 程式，方法是叫用 `MyApplicationEncryptDocument` 物件 `invoke` 方法。 傳遞 `BLOB` 包含PDF文檔的對象。 調用方法返回 `BLOB` 包含加密PDF文檔的對象。
1. 通過調用 `BLOB` 物件 `getBinaryData` 方法。
1. 將加密的PDF文檔另存為PDF檔案。 將位元組陣列寫入檔案。

**另請參閱**

[快速入門：使用Java代理檔案和Base64編碼調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](#creating-a-net-client-assembly-that-uses-base64-encoding)

## 使用MTOM叫用AEM Forms {#invoking-aem-forms-using-mtom}

您可以使用網站服務標準MTOM叫用AEM Forms服務。 此標準定義了二進位資料(如PDF文檔)如何通過Internet或內聯網傳輸。 MTOM的一項功能是使用 `XOP:Include` 元素。 此元素在XML二進位優化包裝(XOP)規範中定義，以引用SOAP消息的二進位附件。

這裡討論的是使用MTOM來調用以下名為的AEM Forms短期進程 `MyApplication/EncryptDocument`.

>[!NOTE]
>
>此程式並非以現有的AEM Forms程式為基礎。 若要遵循程式碼範例，請建立以下程式： `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

叫用此程式時，會執行下列動作：

1. 獲取傳遞至流程的不安全PDF文檔。 此動作以 `SetValue` 操作。 此程式的輸入參數為 `document` 進程變數已命名 `inDoc`.
1. 使用密碼加密PDF文檔。 此動作以 `PasswordEncryptPDF` 操作。 密碼加密的PDF文檔在名為的進程變數中返回 `outDoc`.

>[!NOTE]
>
>AEM Forms 9版新增MTOM支援。

>[!NOTE]
>
>使用MTOM傳輸協定的基於JAX WS的應用程式限制為25MB的已發送和已接收資料。 此限制是由於JAX-WS中的錯誤。 如果已發送和已接收檔案的總大小超過25MB，請使用SwaRef傳輸協定，而不是MTOM協定。 否則，可能 `OutOfMemory` 例外。

這裡討論的是在Microsoft .NET專案中使用MTOM來叫用AEM Forms服務。 使用的.NET框架為3.5，開發環境為Visual Studio 2008。 如果您的開發電腦上已安裝Web服務增強功能(WSE)，請將其移除。 .NET 3.5框架支援名為Windows Communication Foundation(WCF)的SOAP框架。 使用MTOM叫用AEM Forms時，僅支援WCF（不支援WSE）。

### 建立使用MTOM調用服務的.NET項目 {#creating-a-net-project-that-invokes-a-service-using-mtom}

您可以建立Microsoft .NET專案，以使用網站服務叫用AEM Forms服務。 首先，使用Visual Studio 2008建立Microsoft .NET專案。 若要叫用AEM Forms服務，請建立要在專案中叫用之AEM Forms服務的服務參考。 建立服務參考時，請指定AEM Forms服務的URL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

取代 `localhost` 包含AEM Forms之J2EE應用程式伺服器的IP位址。 取代 `MyApplication/EncryptDocument` 以叫用的AEM Forms服務名稱。 例如，要調用Rights Management操作，請指定：

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

此 `lc_version` 選項可確保AEM Forms功能（例如MTOM）可供使用。 不指定 `lc_version` 選項，則無法使用MTOM叫用AEM Forms。

建立服務參考後，與AEM Forms服務相關聯的資料類型便可在您的.NET專案中使用。 要建立調用AEM Forms服務的.NET項目，請執行以下步驟：

1. 使用Microsoft Visual Studio 2008建立.NET專案。
1. 在 **專案** 菜單，選擇 **添加服務引用**.
1. 在 **地址** 對話框，指定AEM Forms服務的WSDL。 例如，

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. 按一下 **開始** 然後按一下 **確定**.

### 在.NET項目中使用MTOM調用服務 {#invoking-a-service-using-mtom-in-a-net-project}

考慮 `MyApplication/EncryptDocument` 接受不安全PDF文檔並返回密碼加密PDF文檔的過程。 叫用 `MyApplication/EncryptDocument` 使用MTOM處理（內建於Workbench中），請執行下列步驟：

1. 建立Microsoft .NET專案。
1. 建立 `MyApplication_EncryptDocumentClient` 物件，使用其預設建構函式。
1. 建立 `MyApplication_EncryptDocumentClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞至AEM Forms服務和編碼類型：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   您不需要使用 `lc_version` 屬性。 建立服務參考時，會使用此屬性。 不過，請確定您指定 `?blob=mtom`.

   >[!NOTE]
   >
   >取代 `hiro-xp` *包含AEM Forms之J2EE應用程式伺服器的IP位址。*

1. 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `EncryptDocumentClient.Endpoint.Binding` 資料成員。 將傳回值轉換為 `BasicHttpBinding`.
1. 設定 `System.ServiceModel.BasicHttpBinding` 物件 `MessageEncoding` 資料成員 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
1. 通過執行以下任務來啟用基本HTTP身份驗證：

   * 將AEM表單使用者名稱指派給資料成員 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * 將相應的密碼值分配給資料成員 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * 指派常數值 `HttpClientCredentialType.Basic` 到資料成員 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到資料成員 `BasicHttpBindingSecurity.Security.Mode`.

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

1. 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 對象用於儲存要傳遞到的PDF文檔 `MyApplication/EncryptDocument` 程式。
1. 建立 `System.IO.FileStream` 對象，方法是調用其建構子。 傳遞一個字串值，該字串值表示PDF文檔的檔案位置以及開啟檔案的模式。
1. 建立位元組陣列，用於儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件 `Length` 屬性。
1. 叫用 `System.IO.FileStream` 物件 `Read` 方法。 傳遞位元組陣列、起始位置和資料流長度以讀取。
1. 填入 `BLOB` 對象，通過賦值 `MTOM` 包含位元組陣列內容的資料成員。
1. 叫用 `MyApplication/EncryptDocument` 程式，方法是叫用 `MyApplication_EncryptDocumentClient` 物件 `invoke` 方法。 傳遞 `BLOB` 包含PDF文檔的對象。 此程式會在 `BLOB` 物件。
1. 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示安全PDF文檔的檔案位置。
1. 建立位元組陣列，用於儲存 `BLOB` 由傳回的物件 `invoke` 方法。 取得 `BLOB` 物件 `MTOM` 資料成員。
1. 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
1. 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

>[!NOTE]
>
>大部分的AEM Forms服務作業都有MTOM快速入門。 您可以在服務的相應快速入門部分中查看這些快速入門。 例如，若要查看輸出快速入門區段，請參閱 [輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**另請參閱**

[快速入門：在.NET項目中使用MTOM調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[使用Web服務訪問多個服務](#accessing-multiple-services-using-web-services)

[建立ASP.NET Web應用程式，該應用程式調用以人為中心的長生命週期過程](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## 使用SwaRef叫用AEM Forms {#invoking-aem-forms-using-swaref}

您可以使用SwaRef叫用AEM Forms服務。 內容 `wsi:swaRef` XML元素會以附件的形式在儲存對附件的引用的SOAP主體內發送。 使用SwaRef叫用Forms服務時，請使用XML Web Services(JAX-WS)的Java API建立Java代理類。 (請參閱 [Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

這裡討論的話題是叫用以下Forms短期進程 `MyApplication/EncryptDocument` 使用SwaRef。

>[!NOTE]
>
>此程式並非以現有的AEM Forms程式為基礎。 若要遵循程式碼範例，請建立以下程式： `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

叫用此程式時，會執行下列動作：

1. 獲取傳遞至流程的不安全PDF文檔。 此動作以 `SetValue` 操作。 此程式的輸入參數為 `document` 進程變數已命名 `inDoc`.
1. 使用密碼加密PDF文檔。 此動作以 `PasswordEncryptPDF` 操作。 密碼加密的PDF文檔在名為的進程變數中返回 `outDoc`.

>[!NOTE]
>
>AEM Forms中新增SwaRef支援

以下討論如何在Java用戶端應用程式中使用SwaRef來叫用Forms服務。 Java應用程式使用由JAX-WS建立的代理類。

### 使用使用SwaRef的JAX-WS庫檔案調用服務 {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

叫用 `MyApplication/EncryptDocument` 使用使用JAX-WS和SwaRef建立的Java代理檔案進行處理，請執行以下步驟：

1. 使用JAX-WS建立Java代理類，該類使用 `MyApplication/EncryptDocument` 服務WSDL。 使用以下WSDL端點：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   如需詳細資訊，請參閱 [使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >取代 `hiro-xp` *包含AEM Forms之J2EE應用程式伺服器的IP位址。*

1. 將使用JAX-WS建立的Java代理類打包到JAR檔案中。
1. 包括位於以下路徑中的Java代理JAR檔案和JAR檔案：

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   進入Java客戶端項目的類路徑。

1. 建立 `MyApplicationEncryptDocumentService` 物件，使用其建構子。
1. 建立 `MyApplicationEncryptDocument` 對象，方法是調用 `MyApplicationEncryptDocumentService` 物件 `getEncryptDocument` 方法。
1. 將值指派給下列資料成員，以設定叫用AEM Forms所需的連線值：

   * 將WSDL端點和編碼類型指派給 `javax.xml.ws.BindingProvider` 物件 `ENDPOINT_ADDRESS_PROPERTY` 欄位。 叫用 `MyApplication/EncryptDocument` 使用SwaRef編碼的服務，請指定下列URL值：

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * 將AEM表單使用者指派至 `javax.xml.ws.BindingProvider` 物件 `USERNAME_PROPERTY` 欄位。
   * 將對應的密碼值指派給 `javax.xml.ws.BindingProvider` 物件 `PASSWORD_PROPERTY` 欄位。

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

1. 檢索要發送到的PDF文檔 `MyApplication/EncryptDocument` 程式 `java.io.File` 物件，使用其建構子。 傳遞指定PDF文檔位置的字串值。
1. 建立 `javax.activation.DataSource` 物件，使用 `FileDataSource` 建構子。 傳遞 `java.io.File` 物件。
1. 建立 `javax.activation.DataHandler` 對象，使用其建構子並傳遞 `javax.activation.DataSource` 物件。
1. 建立 `BLOB` 物件，使用其建構子。
1. 填入 `BLOB` 對象 `setSwaRef` 方法和傳遞 `javax.activation.DataHandler` 物件。
1. 叫用 `MyApplication/EncryptDocument` 程式，方法是叫用 `MyApplicationEncryptDocument` 物件 `invoke` 方法和傳遞 `BLOB` 包含PDF文檔的對象。 調用方法返回 `BLOB` 包含加密PDF文檔的對象。
1. 填入 `javax.activation.DataHandler` 對象，方法是調用 `BLOB` 物件 `getSwaRef` 方法。
1. 轉換 `javax.activation.DataHandler` 對象 `java.io.InputSteam` 執行個體 `javax.activation.DataHandler` 物件 `getInputStream` 方法。
1. 撰寫 `java.io.InputSteam` 執行個體至代表加密PDF檔案的PDF檔案。

>[!NOTE]
>
>大部分的AEM Forms服務操作都有SwaRef快速啟動。 您可以在服務的相應快速入門部分中查看這些快速入門。 例如，若要查看輸出快速入門區段，請參閱 [輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**另請參閱**

[快速入門：在Java項目中使用SwaRef調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## 透過HTTP使用BLOB資料叫用AEM Forms {#invoking-aem-forms-using-blob-data-over-http}

您可以使用網站服務叫用AEM Forms服務，並透過HTTP傳遞BLOB資料。 透過HTTP傳遞BLOB資料是替代技術，而非使用base64編碼、DIME或MIME。 例如，您可以在使用不支援DIME或MIME之Web服務增強功能3.0的Microsoft .NET專案中，透過HTTP傳遞資料。 透過HTTP使用BLOB資料時，會先上傳輸入資料，再叫用AEM Forms服務。

「透過HTTP叫用AEM Forms」討論叫用下列AEM Forms短期處理程式，命名為 `MyApplication/EncryptDocument` 透過HTTP傳遞BLOB資料。

>[!NOTE]
>
>此程式並非以現有的AEM Forms程式為基礎。 若要遵循程式碼範例，請建立以下程式： `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

叫用此程式時，會執行下列動作：

1. 獲取傳遞至流程的不安全PDF文檔。 此動作以 `SetValue` 操作。 此程式的輸入參數為 `document` 進程變數已命名 `inDoc`.
1. 使用密碼加密PDF文檔。 此動作以 `PasswordEncryptPDF` 操作。 密碼加密的PDF文檔在名為的進程變數中返回 `outDoc`.

>[!NOTE]
>
>建議您先熟悉如何使用SOAP叫用AEM Forms。 (請參閱 [使用Web服務叫用AEM Forms](#invoking-aem-forms-using-web-services).)

### 建立使用通過HTTP的資料的.NET客戶端程式集 {#creating-a-net-client-assembly-that-uses-data-over-http}

要建立使用通過HTTP的資料的客戶端程式集，請遵循 [使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding). 不過，請修改Proxy類別中的URL以包括 `?blob=http` 而非 `?blob=base64`. 此動作可確保資料透過HTTP傳遞。 在Proxy類別中，找出下列程式碼行：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

並將其變更為：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**引用.NET clienMyApplication/EncryptDocument程式集**

將新的.NET客戶端程式集放置在要開發客戶端應用程式的電腦上。 將.NET客戶端程式集放置到目錄後，可以從項目中引用它。 參考 `System.Web.Services` 程式庫。 如果未引用此庫，則不能使用.NET客戶端程式集調用服務。

1. 在 **專案** 菜單，選擇 **新增參考**.
1. 按一下 **.NET** 標籤。
1. 按一下 **瀏覽** 並找到DocumentService.dll檔案。
1. 按一下 **選擇** 然後按一下 **確定**.

**使用通過HTTP使用BLOB資料的.NET客戶端程式集調用服務**

您可以叫用 `MyApplication/EncryptDocument` 使用透過HTTP使用資料的.NET用戶端程式集的服務（此服務於Workbench中建置）。 叫用 `MyApplication/EncryptDocument` 服務，請執行以下步驟：

1. 建立.NET客戶端程式集。
1. 參考Microsoft .NET客戶端程式集。 建立客戶端Microsoft .NET項目。 在客戶端項目中引用Microsoft .NET客戶端程式集。 也參考 `System.Web.Services`.
1. 使用Microsoft .NET客戶端程式集，建立 `MyApplication_EncryptDocumentService` 對象，方法是調用其預設建構子。
1. 設定 `MyApplication_EncryptDocumentService` 物件 `Credentials` 具有 `System.Net.NetworkCredential` 物件。 在 `System.Net.NetworkCredential` 建構函式，指定AEM表單使用者名稱和對應的密碼。 設定驗證值，使您的.NET客戶端應用程式能夠成功與AEM Forms交換SOAP消息。
1. 建立 `BLOB` 物件，使用其建構子。 此 `BLOB` 物件可用來將資料傳遞至 `MyApplication/EncryptDocument` 程式。
1. 將字串值指派給 `BLOB` 物件 `remoteURL` 指定要傳遞到的PDF文檔的URI位置的資料成員 `MyApplication/EncryptDocument`服務。
1. 叫用 `MyApplication/EncryptDocument` 程式，方法是叫用 `MyApplication_EncryptDocumentService` 物件 `invoke` 方法和傳遞 `BLOB` 物件。 此程式會在 `BLOB` 物件。
1. 建立 `System.UriBuilder` 物件，方法是使用其建構子並傳遞傳回之值 `BLOB` 物件 `remoteURL` 資料成員。
1. 轉換 `System.UriBuilder` 對象 `System.IO.Stream` 物件。 （此清單後面的C#快速入門說明了如何執行此任務。）
1. 建立位元組陣列，並將位於 `System.IO.Stream` 物件。
1. 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
1. 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

### 使用Java代理類和BLOB資料通過HTTP調用服務 {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

您可以使用Java代理類和BLOB資料，透過HTTP叫用AEM Forms服務。 叫用 `MyApplication/EncryptDocument` 服務，請執行以下步驟：

1. 使用JAX-WS建立Java代理類，該類使用 `MyApplication/EncryptDocument` 服務WSDL。 使用以下WSDL端點：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   如需詳細資訊，請參閱 [使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >取代 `hiro-xp` *包含AEM Forms之J2EE應用程式伺服器的IP位址。*

1. 將使用JAX-WS建立的Java代理類打包到JAR檔案中。
1. 包括位於以下路徑中的Java代理JAR檔案和JAR檔案：

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   進入Java客戶端項目的類路徑。

1. 建立 `MyApplicationEncryptDocumentService` 物件，使用其建構子。
1. 建立 `MyApplicationEncryptDocument` 對象，方法是調用 `MyApplicationEncryptDocumentService` 物件 `getEncryptDocument` 方法。
1. 將值指派給下列資料成員，以設定叫用AEM Forms所需的連線值：

   * 將WSDL端點和編碼類型指派給 `javax.xml.ws.BindingProvider` 物件 `ENDPOINT_ADDRESS_PROPERTY` 欄位。 叫用 `MyApplication/EncryptDocument` 使用BLOB over HTTP編碼的服務，請指定下列URL值：

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * 將AEM表單使用者指派至 `javax.xml.ws.BindingProvider` 物件 `USERNAME_PROPERTY` 欄位。
   * 將對應的密碼值指派給 `javax.xml.ws.BindingProvider` 物件 `PASSWORD_PROPERTY` 欄位。

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

1. 建立 `BLOB` 物件，使用其建構子。
1. 填入 `BLOB` 對象 `setRemoteURL` 方法。 傳遞一個字串值，該字串值指定要傳遞到的PDF文檔的URI位置 `MyApplication/EncryptDocument` 服務。
1. 叫用 `MyApplication/EncryptDocument` 程式，方法是叫用 `MyApplicationEncryptDocument` 物件 `invoke` 方法和傳遞 `BLOB` 包含PDF文檔的對象。 此程式會在 `BLOB` 物件。
1. 建立位元組陣列以儲存代表加密PDF檔案的資料流。 叫用 `BLOB` 物件 `getRemoteURL` 方法(使用 `BLOB` 由傳回的物件 `invoke` 方法)。
1. 建立 `java.io.File` 物件，使用其建構子。 此對象表示加密的PDF文檔。
1. 建立 `java.io.FileOutputStream` 對象，使用其建構子並傳遞 `java.io.File` 物件。
1. 叫用 `java.io.FileOutputStream` 物件 `write` 方法。 傳遞包含代表加密PDF檔案之資料流的位元組陣列。

## 使用DIME叫用AEM Forms {#invoking-aem-forms-using-dime}

您可以使用SOAP搭配附件來叫用AEM Forms服務。 AEM Forms支援MIME和DIME網站服務標準。 DIME可讓您傳送二進位附件，例如PDF檔案，以及叫用請求，而非對附件編碼。 此 *使用DIME叫用AEM Forms* 小節討論調用以下AEM Forms短期進程，命名為 `MyApplication/EncryptDocument` 用DIME。

叫用此程式時，會執行下列動作：

1. 獲取傳遞至流程的不安全PDF文檔。 此動作以 `SetValue` 操作。 此程式的輸入參數為 `document` 進程變數已命名 `inDoc`.
1. 使用密碼加密PDF文檔。 此動作以 `PasswordEncryptPDF` 操作。 密碼加密的PDF文檔在名為的進程變數中返回 `outDoc`.

此程式並非以現有的AEM Forms程式為基礎。 若要遵循程式碼範例，請建立以下程式： `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>不建議使用DIME叫用AEM Forms服務作業。 建議您使用MTOM。 (請參閱 [使用MTOM叫用AEM Forms](#invoking-aem-forms-using-mtom).)

### 建立使用DIME的.NET項目 {#creating-a-net-project-that-uses-dime}

要建立可使用DIME調用Forms服務的.NET項目，請執行以下任務：

* 在您的開發電腦上安裝網站服務增強功能2.0。
* 從.NET專案內，建立FormsAEM Forms服務的網頁參考。

**安裝網站服務增強功能2.0**

在您的開發電腦上安裝Web服務增強功能2.0，並將其與Microsoft Visual Studio .NET整合。 您可以從以下網址下載網站服務增強功能2.0: [Microsoft下載中心。](https://www.microsoft.com/downloads/search.aspx)

從此網頁，搜索Web服務增強功能2.0，然後將其下載到您的開發電腦上。 此下載將名為Microsoft WSE 2.0 SPI.msi的檔案放在電腦上。 運行安裝程式，並遵循聯機指示。

>[!NOTE]
>
>網站服務增強功能2.0支援DIME。 使用網站服務增強功能2.0時，支援的Microsoft Visual Studio版本為2003。網站服務增強功能3.0不支援DIME;不過，它支援MTOM。

**建立AEM Forms服務的網頁參考**

在開發電腦上安裝Web服務增強功能2.0並建立Microsoft .NET專案後，請建立Forms服務的Web參考。 例如，要建立指向 `MyApplication/EncryptDocument` 處理程式，並假設Forms已安裝在本機電腦上，請指定下列URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

建立Web引用後，可在.NET項目中使用以下兩種代理資料類型： `EncryptDocumentService` 和 `EncryptDocumentServiceWse`. 叫用 `MyApplication/EncryptDocument` 使用DIME的流程，使用 `EncryptDocumentServiceWse` 類型。

>[!NOTE]
>
>在建立Forms服務的網頁參考之前，請務必在專案中參考網站服務增強功能2.0。 （請參閱「安裝網站服務增強功能2.0」。）

**參考WSE程式庫**

1. 在「項目」菜單中，選擇「添加引用」。
1. 在添加引用對話框中，選擇Microsoft.Web.Services2.dll。
1. 選擇System.Web.Services.dll。
1. 按一下「選擇」，然後按一下「確定」。

**建立Forms服務的網頁參考**

1. 在「項目」菜單中，選擇「添加Web引用」。
1. 在「URL」對話方塊中，指定Forms服務的URL。
1. 按一下「開始」 ，然後按一下「新增參考」 。

>[!NOTE]
>
>確保啟用.NET項目以使用WSE庫。 在「項目資源管理器」中，按一下右鍵項目名稱並選擇啟用WSE 2.0。確保選中顯示的對話框上的複選框。

**在.NET項目中使用DIME調用服務**

您可以使用DIME叫用Forms服務。 考慮 `MyApplication/EncryptDocument` 接受不安全PDF文檔並返回密碼加密PDF文檔的過程。 叫用 `MyApplication/EncryptDocument` 使用DIME處理，請執行以下步驟：

1. 建立Microsoft .NET專案，讓您使用DIME叫用Forms服務。 請確定您包含網站服務增強功能2.0，並建立AEM Forms服務的網頁參考。
1. 將Web參考設定為 `MyApplication/EncryptDocument` 進程，建立 `EncryptDocumentServiceWse` 物件，使用其預設建構函式。
1. 設定 `EncryptDocumentServiceWse` 物件 `Credentials` 具有 `System.Net.NetworkCredential` 指定AEM表單用戶名和密碼值的值。
1. 建立 `Microsoft.Web.Services2.Dime.DimeAttachment` 物件，方法是使用其建構子並傳遞下列值：

   * 指定GUID值的字串值。 您可以叫用 `System.Guid.NewGuid.ToString` 方法。
   * 指定內容類型的字串值。 因為此過程需要PDF文檔，請指定 `application/pdf`.
   * A `TypeFormat` 枚舉值。 指定 `TypeFormat.MediaType`.
   * 一個字串值，它指定要傳遞至AEM Forms進程的PDF文檔的位置。

1. 建立 `BLOB` 物件，使用其建構子。
1. 將DIME附件添加到 `BLOB` 對象，方法是 `Microsoft.Web.Services2.Dime.DimeAttachment` 物件 `Id` 資料成員值 `BLOB` 物件 `attachmentID` 資料成員。
1. 叫用 `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` 方法並傳遞 `Microsoft.Web.Services2.Dime.DimeAttachment` 物件。
1. 叫用 `MyApplication/EncryptDocument` 程式，方法是叫用 `EncryptDocumentServiceWse` 物件 `invoke` 方法和傳遞 `BLOB` 包含DIME附件的對象。 此程式會在 `BLOB` 物件。
1. 獲取返回的值，以獲取附件標識符值 `BLOB` 物件 `attachmentID` 資料成員。
1. 查看位於 `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` 並使用附件標識符值來獲取加密的PDF文檔。
1. 取得 `System.IO.Stream` 物件，方法是取得 `Attachment` 物件 `Stream` 資料成員。
1. 建立位元組陣列，並將該位元組陣列傳遞至 `System.IO.Stream` 物件 `Read` 方法。 此方法會以代表加密PDF檔案的資料流填入位元組陣列。
1. 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式並傳遞代表PDF檔案位置的字串值。 此對象表示加密的PDF文檔。
1. 建立 `System.IO.BinaryWriter` 對象，調用其建構子並傳遞 `System.IO.FileStream` 物件。
1. 調用 `System.IO.BinaryWriter` 物件 `Write` 方法，並傳遞位元組陣列。

### 建立使用DIME的Apache Axis Java代理類 {#creating-apache-axis-java-proxy-classes-that-use-dime}

可以使用Apache Axis WSDL2Java工具將服務WSDL轉換為Java代理類，以便調用服務操作。 使用Apache Ant，您可以從AEM Forms服務WSDL生成Axis庫檔案，該WSDL允許您調用該服務。 (請參閱 [使用Apache Axis建立Java代理類](#creating-java-proxy-classes-using-apache-axis).)

Apache Axis WSDL2Java工具會生成包含用於向服務發送SOAP請求的方法的JAVA檔案。 由服務接收的SOAP請求由Axis生成的庫解碼，並轉回為方法和參數。

叫用 `MyApplication/EncryptDocument` 使用軸產生的程式庫檔案和DIME的服務（內建於Workbench中），請執行下列步驟：

1. 建立使用 `MyApplication/EncryptDocument` 服務WSDL（使用Apache Axis）。 (請參閱 [使用Apache Axis建立Java代理類](#creating-java-proxy-classes-using-apache-axis).)
1. 將Java代理類包含到類路徑中。
1. 建立 `MyApplicationEncryptDocumentServiceLocator` 物件，使用其建構子。
1. 建立 `URL` 物件，方法是使用其建構函式並傳遞指定AEM Forms服務WSDL定義的字串值。 請確定您指定 `?blob=dime` 在SOAP端點URL的結尾。 例如，使用

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. 建立 `EncryptDocumentSoapBindingStub` 對象，調用其建構子並傳遞 `MyApplicationEncryptDocumentServiceLocator`物件和 `URL` 物件。
1. 叫用 `EncryptDocumentSoapBindingStub` 物件 `setUsername` 和 `setPassword` 方法。

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. 檢索要發送到的PDF文檔 `MyApplication/EncryptDocument` 服務，透過建立 `java.io.File` 物件。 傳遞指定PDF文檔位置的字串值。
1. 建立 `javax.activation.DataHandler` 對象，使用其建構子並傳遞 `javax.activation.FileDataSource` 物件。 此 `javax.activation.FileDataSource` 可使用物件的建構函式並傳遞來建立物件 `java.io.File` 表示PDF文檔的對象。
1. 建立 `org.apache.axis.attachments.AttachmentPart` 對象，使用其建構子並傳遞 `javax.activation.DataHandler` 物件。
1. 通過調用 `EncryptDocumentSoapBindingStub` 物件 `addAttachment` 方法和傳遞 `org.apache.axis.attachments.AttachmentPart` 物件。
1. 建立 `BLOB` 物件，使用其建構子。 填入 `BLOB` 對象，通過調用 `BLOB` 物件 `setAttachmentID` 方法，並傳遞附件識別碼值。 可借由叫用 `org.apache.axis.attachments.AttachmentPart` 物件 `getContentId` 方法。
1. 叫用 `MyApplication/EncryptDocument` 程式，方法是叫用 `EncryptDocumentSoapBindingStub` 物件 `invoke` 方法。 傳遞 `BLOB` 包含DIME附件的對象。 此程式會在 `BLOB` 物件。
1. 通過調用返回的 `BLOB` 物件 `getAttachmentID` 方法。 此方法會傳回字串值，代表傳回附件的識別碼值。
1. 調用 `EncryptDocumentSoapBindingStub` 物件 `getAttachments` 方法。 此方法會傳回陣列 `Objects` 表示附件。
1. 查看附件( `Object` 陣列)，並使用附件標識符值來獲取加密的PDF文檔。 每個元素都是 `org.apache.axis.attachments.AttachmentPart` 物件。
1. 取得 `javax.activation.DataHandler` 通過調用 `org.apache.axis.attachments.AttachmentPart` 物件 `getDataHandler` 方法。
1. 取得 `java.io.FileStream` 對象，方法是調用 `javax.activation.DataHandler` 物件 `getInputStream` 方法。
1. 建立位元組陣列，並將該位元組陣列傳遞至 `java.io.FileStream` 物件 `read` 方法。 此方法會以代表加密PDF檔案的資料流填入位元組陣列。
1. 建立 `java.io.File` 物件，使用其建構子。 此對象表示加密的PDF文檔。
1. 建立 `java.io.FileOutputStream` 對象，使用其建構子並傳遞 `java.io.File` 物件。
1. 叫用 `java.io.FileOutputStream` 物件 `write` 方法，並傳遞包含代表加密PDF檔案之資料流的位元組陣列。

**另請參閱**

[快速入門：在Java項目中使用DIME調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## 使用SAML型驗證 {#using-saml-based-authentication}

AEM Forms在叫用服務時支援各種web服務驗證模式。 一種驗證模式是使用Web服務調用中的基本授權頭指定用戶名和密碼值。 AEM Forms也支援SAML斷言式驗證。 當客戶端應用程式使用web服務調用AEM Forms服務時，客戶端應用程式可以以下列方式之一提供驗證資訊：

* 傳遞憑證作為基本授權的一部分
* 將用戶名令牌作為WS-Security標頭的一部分傳遞
* 將SAML斷言傳遞為WS-Security標頭的一部分
* 將Kerberos令牌作為WS-Security標頭的一部分傳遞

AEM Forms不支援標準憑證式驗證，但支援不同格式的憑證式驗證。

>[!NOTE]
>
>Web服務快速入門於使用AEM Forms進行程式設計，指定用戶名和密碼值以執行授權。

AEM表單使用者的身分可透過使用機密金鑰簽署的SAML斷言來表示。 以下XML程式碼顯示SAML斷言的範例。

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

向管理員用戶發出此示例聲明。 此斷言包含下列值得注意的項目：

* 在特定期間有效。
* 會為特定使用者核發。
* 它有數位簽名。 所以任何修改都會破壞簽名。
* 它可以以類似使用者名稱和密碼的使用者身分代號呈現給AEM Forms。

用戶端應用程式可從任何傳回的AEM Forms AuthenticationManager API擷取斷言 `AuthResult` 物件。 您可以取得 `AuthResult` 例項，方法如下列其中一種：

* 使用AuthenticationManager API公開的任何驗證方法驗證用戶。 通常，用戶會使用用戶名和密碼；不過，您也可以使用憑證驗證。
* 使用 `AuthenticationManager.getAuthResultOnBehalfOfUser` 方法。 此方法可讓用戶端應用程式取得 `AuthResult` 物件。

AEM表單使用者可使用所取得的SAML代號來驗證。 此SAML斷言（xml片段）可隨Web服務呼叫（用於用戶驗證）一併傳送，作為WS-Security標頭的一部分。 通常，客戶端應用程式已驗證用戶，但未儲存用戶憑據。 （或者，用戶已通過使用用戶名和密碼以外的機制登錄到該客戶端。） 在此情況下，用戶端應用程式必須叫用AEM Forms並模擬允許叫用AEM Forms的特定使用者。

若要模擬特定使用者，請叫用 `AuthenticationManager.getAuthResultOnBehalfOfUser` 方法。 此方法會傳回 `AuthResult` 包含該使用者之SAML斷言的例項。

接下來，使用該SAML斷言來叫用任何需要驗證的服務。 此動作包括將斷言傳送為SOAP標頭的一部分。 使用此斷言進行Web服務呼叫時，AEM Forms會將使用者識別為該斷言所代表的使用者。 也就是說，斷言中指定的使用者是叫用服務的使用者。

### 使用Apache Axis類別和SAML型驗證 {#using-apache-axis-classes-and-saml-based-authentication}

您可以使用Axis程式庫建立的Java代理類調用AEM Forms服務。 (請參閱 [使用Apache Axis建立Java代理類](#creating-java-proxy-classes-using-apache-axis).)

使用使用SAML型驗證的AXIS時，請使用Axis註冊請求和回應處理常式。 Apache Axis會先叫用處理常式，再將叫用請求傳送至AEM Forms。 要註冊處理程式，請建立擴展的Java類 `org.apache.axis.handlers.BasicHandler`.

**建立軸為的AssertionHandler**

以下Java類，名為 `AssertionHandler.java`，顯示延伸的Java類的範例 `org.apache.axis.handlers.BasicHandler`.

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

**註冊處理程式**

要用Axis註冊處理程式，請建立client-config.wsdd檔案。 依預設，Axis會尋找具有此名稱的檔案。 以下XML代碼是client-config.wsdd檔案的示例。 如需詳細資訊，請參閱軸檔案。

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

下列程式碼範例使用SAML型驗證來叫用AEM Forms服務。

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

### 使用.NET客戶端程式集和基於SAML的驗證 {#using-a-net-client-assembly-and-saml-based-authentication}

您可以使用.NET用戶端程式集和SAML型驗證來叫用Forms服務。 要執行此操作，必須使用網站服務增強功能3.0(WSE)。 有關建立使用WSE的.NET客戶端程式集的資訊，請參見 [建立使用DIME的.NET項目](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>DIME部分使用WSE 2.0。要使用基於SAML的驗證，請遵循在DIME主題中指定的相同說明。 但是，將WSE 2.0替換為WSE 3.0。請在開發電腦上安裝Web服務增強功能3.0，並將其與Microsoft Visual Studio .NET整合。 您可以從以下網址下載網站服務增強功能3.0: [Microsoft下載中心](https://www.microsoft.com/downloads/search.aspx).

WSE體系結構使用策略、斷言和SecurityToken資料類型。 簡短地，對於Web服務呼叫，請指定策略。 策略可以有多個斷言。 每個斷言都可包含篩選器。 在Web服務呼叫的某些階段會叫用篩選器，屆時可以修改SOAP請求。 如需完整詳細資訊，請參閱網站服務增強功能3.0檔案。

**建立斷言和篩選**

以下C#代碼示例建立篩選器和斷言類。 此程式碼範例會建立SamlAssertionOutputFilter。 在將SOAP請求發送到AEM Forms之前，WSE框架會叫用此篩選器。

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

**建立SAML代號**

建立類別以表示SAML斷言。 此類執行的主要任務是將資料值從字串轉換為xml並保留空白。 此斷言xml稍後會匯入SOAP請求中。

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

以下C#程式碼範例使用SAML型驗證來叫用Forms服務。

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

## 使用網站服務時的相關考量 {#related-considerations-when-using-web-services}

使用網站服務叫用特定AEM Forms服務作業時，有時會發生問題。 本次討論的目的是確定這些問題，並提供解決辦法（如果有）。

### 非同步調用服務操作 {#invoking-service-operations-asynchronously}

如果您嘗試非同步叫用AEM Forms服務作業，例如產生PDF `htmlToPDF` 操作，a `SoapFaultException` 發生。 若要解決此問題，請建立自訂系結XML檔案，以映射 `ExportPDF_Result` 元素和其他元素。 以下XML表示自定義綁定檔案。

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

使用JAX-WS建立Java代理檔案時，請使用此XML檔案。 (請參閱 [使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws).)

使用 — 執行JAX-WS工具(wsimport.exe)時，請參考此XML檔案 `b` 命令行選項。 更新 `wsdlLocation` 元素，以指定AEM Forms的URL。

若要確保非同步呼叫正常運作，請修改端點URL值並指定 `async=true`. 例如，對於使用JAX-WS建立的Java代理檔案，請為 `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

以下清單指定了非同步調用時需要自定義綁定檔案的其他服務：

* PDFG3D
* 任務管理員
* 應用程式管理員
* 目錄管理器
* Distiller
* Rights Management
* 檔案管理

### J2EE應用程式伺服器的差異 {#differences-in-j2ee-application-servers}

有時，使用特定J2EE應用程式伺服器建立的Proxy程式庫無法成功叫用托管在不同J2EE應用程式伺服器上的AEM Forms。 考慮使用部署在WebSphere上的AEM Forms產生的代理程式庫。 此代理程式庫無法成功調用部署在JBoss應用程式伺服器上的AEM Forms服務。

某些AEM Forms複雜的資料類型，例如 `PrincipalReference`，與JBoss Application Server相比，在WebSphere上部署AEM Forms時的定義不同。 不同J2EE應用程式服務使用的JDK中的差異是WSDL定義中出現差異的原因。 因此，請使用從相同J2EE應用程式伺服器產生的代理程式庫。

### 使用Web服務訪問多個服務 {#accessing-multiple-services-using-web-services}

由於命名空間衝突，資料對象無法在多個服務WSDL之間共用。 不同的服務可以共用資料類型，因此，服務在WSDL中共用這些類型的定義。 例如，不能添加包含 `BLOB` 資料類型到相同的.NET客戶端項目。 如果嘗試執行此操作，則會發生編譯錯誤。

以下清單指定了不能在多個服務WSDL之間共用的資料類型：

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

為避免此問題，建議您完全符合資料類型的資格。 例如，假設.NET應用程式使用服務引用同時引用Forms服務和簽名服務。 兩個服務參考都包含 `BLOB` 類別。 若要使用 `BLOB` 例項，完全限定 `BLOB` 物件。 此方法如下列程式碼範例所示。 如需此程式碼範例的相關資訊，請參閱 [數位簽署互動式Forms](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

下列C#程式碼範例會簽署由Forms服務轉譯的互動式表單。 客戶端應用程式有兩個服務引用。 此 `BLOB` 與Forms服務相關聯的例項屬於 `SignInteractiveForm.ServiceReference2` 命名空間。 同樣， `BLOB` 與簽名服務關聯的實例屬於 `SignInteractiveForm.ServiceReference1` 命名空間。 已簽名的互動式表單將另存為名為的PDF檔案 *LoanXFASided.pdf*.

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

### 以字母I開頭的服務會產生無效的代理檔案 {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

使用Microsoft .Net 3.5和WCF時，某些AEM Forms生成的代理類的名稱不正確。 當為IBMFilenetContentRepositoryConnector、IDPSschedulerService或任何其名稱以字母I開頭的其他服務建立代理類時，會發生此問題。例如，在IBMFileNetContentRepositoryConnector的情況下，生成的客戶端的名稱為 `BMFileNetContentRepositoryConnectorClient`. 生成的代理類中缺少字母I。
