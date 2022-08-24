---
title: 使用Web服務調用AEM Forms
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

# 使用Web服務調用AEM Forms {#invoking-aem-forms-using-web-services}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

服務容器中的大多數AEM Forms服務都配置為公開Web服務，完全支援Web服務定義語言(WSDL)生成。 即，您可以建立使用AEM Forms服務的本機SOAP堆棧的代理對象。 因此，AEM Forms服務可以交換和處理以下SOAP消息：

* **SOAP請求**:由請求操作的客戶端應用程式發送到Forms服務。
* **SOAP響應**:在處理SOAP請求後，Forms服務將其發送到客戶端應用程式。

使用Web服務，可以執行與使用Java API相同的AEM Forms服務操作。 使用Web服務調用AEM Forms服務的好處是，您可以在支援SOAP的開發環境中建立客戶端應用程式。 客戶端應用程式不綁定到特定的開發環境或寫程式語言。 例如，您可以使用MicrosoftVisual Studio .NET和C#作為寫程式語言建立客戶端應用程式。

AEM Forms服務通過SOAP協定公開，並符合WSI Basic Profile 1.1。 Web服務互操作性(WSI)是一個開放標準組織，可促進跨平台的Web服務互操作性。 有關資訊，請參見 [https://www.ws-i.org/](https://www.ws-i.org)。

AEM Forms支援以下Web服務標準：

* **編碼**:僅支援文檔和文字編碼（根據WSI基本配置檔案，這是首選編碼）。 (請參閱 [使用Base64編碼調用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **MTOM**:表示使用SOAP請求對附件進行編碼的方法。 (請參閱 [使用MTOM調用AEM Forms](#invoking-aem-forms-using-mtom)。)
* **SwaRef**:表示使用SOAP請求對附件進行編碼的另一種方法。 (請參閱 [使用SwaRef調用AEM Forms](#invoking-aem-forms-using-swaref)。)
* **帶附件的SOAP**:支援MIME和DIME（直接Internet消息封裝）。 這些協定是通過SOAP發送附件的標準方法。 MicrosoftVisual Studio .NET應用程式使用DIME。 (請參閱 [使用Base64編碼調用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **WS — 安全**:支援用戶名密碼令牌配置檔案，這是作為WS Security SOAP標頭一部分發送用戶名和密碼的標準方式。 AEM Forms還支援HTTP基本身份驗證。 s

要使用Web服務調用AEM Forms服務，通常需要建立一個代理庫，該代理庫使用服務WSDL。 的 *使用Web服務調用AEM Forms* 部分使用JAX-WS建立Java代理類以調用服務。 (請參閱 [使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws)。)

可通過指定以下URL定義（括弧中的項是可選項）來檢索服務WDSL:

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

其中：

* *您的伺服器主機* 表示承載AEM Forms的J2EE應用程式伺服器的IP地址。
* *您的埠* 表示J2EE應用程式伺服器使用的HTTP埠。
* *服務名稱* 表示服務名。
* *版本* 表示服務的目標版本（預設使用最新服務版本）。
* `async` 指定值 `true` 啟用非同步調用的其他操作( `false` )。
* *lc_version* 表示要調用的AEM Forms版本。

下表列出了服務WSDL定義(假定AEM Forms部署在本地主機上，帖子為8080)。

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
   <td><p>後退和恢復</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>條形碼</p></td>
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
   <td><p>文檔管理</p></td>
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
   <td><p>生成PDF</p></td>
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
   <td><p>Acrobat Reader DC擴展</p></td>
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
   <td><p>實XMP用程式</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**AEM Forms進程WSDL定義**

必須在WSDL定義中指定應用程式名和進程名，才能訪問屬於在Workbench中建立的進程的WSDL。 假定應用程式的名稱為 `MyApplication` 進程的名稱是 `EncryptDocument`。 在這種情況下，請指定以下WSDL定義：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>有關示例的資訊 `MyApplication/EncryptDocument` 短期過程，看 [短期流程示例](/help/forms/developing/aem-forms-processes.md)。

>[!NOTE]
>
>應用程式可以包含資料夾。 在這種情況下，請在WSDL定義中指定資料夾名稱：

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**使用Web服務訪問新功能**

可使用Web服務訪問新的AEM Forms服務功能。 例如，在AEM Forms，引入了使用MTOM對附件進行編碼的能力。 (請參閱 [使用MTOM調用AEM Forms](#invoking-aem-forms-using-mtom)。)

要訪問在AEM Forms引入的新功能，請指定 `lc_version` 屬性。 例如，要訪問新的服務功能（包括MTOM支援），請指定以下WSDL定義：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>設定 `lc_version` 屬性，確保使用三位。 例如， 9.0.1等於9.0版。

**Web服務BLOB資料類型**

AEM Forms服務WSDL定義了許多資料類型。 Web服務中公開的最重要資料類型之一是 `BLOB` 的雙曲餘切值。 此資料類型映射到 `com.adobe.idp.Document` 類。 (請參閱 [使用Java API將資料傳遞到AEM Forms服務](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)。)

A `BLOB` 對象向AEM Forms服務發送和檢索二進位資料(例如，PDF檔案、XML資料等)。 的 `BLOB` 類型在服務WSDL中定義如下：

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

的 `MTOM` 和 `swaRef` 欄位僅在AEM Forms支援。 僅當指定包含以下項的URL時，才可以使用這些新欄位 `lc_version` 屬性。

**在服務請求中提供BLOB對象**

如果AEM Forms服務操作需要 `BLOB` 鍵入為輸入值，建立實例 `BLOB` 鍵入應用程式邏輯。 (許多Web服務快速啟動位於 *用表格編AEM程* 顯示如何使用BLOB資料類型。)

將值分配給屬於 `BLOB` 實例：

* **基64**:要將資料作為以Base64格式編碼的文本傳遞，請在 `BLOB.binaryData` 欄位，並以MIME格式設定資料類型(例如 `application/pdf`) `BLOB.contentType` 的子菜單。 (請參閱 [使用Base64編碼調用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **MTOM**:要在MTOM附件中傳遞二進位資料，請在 `BLOB.MTOM` 的子菜單。 此設定使用Java JAX-WS框架或SOAP框架的本機API將資料附加到SOAP請求。 (請參閱 [使用MTOM調用AEM Forms](#invoking-aem-forms-using-mtom)。)
* **SwaRef**:要在WS-I SwaRef附件中傳遞二進位資料，請在 `BLOB.swaRef` 的子菜單。 此設定使用Java JAX-WS框架將資料附加到SOAP請求。 (請參閱 [使用SwaRef調用AEM Forms](#invoking-aem-forms-using-swaref)。)
* **MIME或DIME附件**:要在MIME或DIME附件中傳遞資料，請使用SOAP框架的本機API將資料附加到SOAP請求。 在 `BLOB.attachmentID` 的子菜單。 (請參閱 [使用Base64編碼調用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **遠程URL**:如果資料托管在Web伺服器上，並可通過HTTP URL訪問，請在 `BLOB.remoteURL` 的子菜單。 (請參閱 [通過HTTP調用AEM Forms使用BLOB資料](#invoking-aem-forms-using-blob-data-over-http)。)

**訪問從服務返回的BLOB對象中的資料**

返回的傳輸協定 `BLOB` 對象取決於幾個因素，這些因素按以下順序考慮，當滿足主要條件時停止：

1. **目標URL指定傳輸協定**。 如果在SOAP調用中指定的目標URL包含參數 `blob="`*BLOB_TYPE*」 *BLOB_TYPE* 確定傳輸協定。 *BLOB_TYPE* 是base64、dime、mime、http、mtom或swaref的佔位符。
1. **服務SOAP終結點為Smart**。 如果以下條件為true，則使用與輸入文檔相同的傳輸協定返回輸出文檔：

   * 輸出Blob對象的服務的SOAP終結點參數預設協定設定為Smart。

      對於每個具有SOAP端點的服務，管理控制台允許您為任何返回的Blob指定傳輸協定。 (請參閱 [管理幫助](https://www.adobe.com/go/learn_aemforms_admin_63)。)

   * AEM Forms服務將一個或多個文檔作為輸入。

1. **服務SOAP終結點不是Smart**。 所配置的協定確定文檔傳輸協定，並且資料在相應的協定中返回 `BLOB` 的子菜單。 例如，如果SOAP終結點設定為DIME，則返回的blob位於 `blob.attachmentID` 欄位，而不考慮任何輸入文檔的傳輸協定。
1. **否則**。 如果服務未將文檔類型作為輸入，則輸出文檔將在 `BLOB.remoteURL` 欄位。

如第一個條件中所述，可以通過以下方式擴展帶尾碼的SOAP端點URL來確保任何返回文檔的傳輸類型：

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

以下是傳輸類型與從中獲取資料的欄位之間的關聯：

* **Base64格式**:設定 `blob` 尾碼 `base64` 返回 `BLOB.binaryData` 的子菜單。
* **MIME或DIME附件**:設定 `blob` 尾碼 `DIME` 或 `MIME` 將資料作為相應的附件類型返回，並在 `BLOB.attachmentID` 的子菜單。 使用SOAP框架的專有API從附件中讀取資料。
* **遠程URL**:設定 `blob` 尾碼 `http` 將資料保留在應用程式伺服器上，並返回指向應用程式中資料的URL `BLOB.remoteURL` 的子菜單。
* **MTOM或SwaRef**:設定 `blob` 尾碼 `mtom` 或 `swaref` 將資料作為相應的附件類型返回，並在 `BLOB.MTOM` 或 `BLOB.swaRef` 的子菜單。 使用SOAP框架的本機API從附件中讀取資料。

>[!NOTE]
>
>建議在填充 `BLOB` 通過調用對象 `setBinaryData` 的雙曲餘切值。 否則，有可能 `OutOfMemory` 出現異常。

>[!NOTE]
>
>使用MTOM傳輸協定的基於JAX WS的應用程式被限制為25MB的發送和接收資料。 此限制是由於JAX-WS中存在錯誤。 如果已發送和已接收檔案的總大小超過25MB，請使用SwaRef傳輸協定，而不是MTOM協定。 否則，就有可能 `OutOfMemory` 例外。

**MTOM傳輸基本64編碼位元組陣列**

除 `BLOB` 對象，MTOM協定支援任何複雜類型的位元組陣列參數或位元組陣列欄位。 這意味著支援MTOM的客戶端SOAP框架可以發送任何 `xsd:base64Binary` 元素作為MTOM附件（而不是base64編碼的文本）。 AEM FormsSOAP端點可以讀取此類位元組陣列編碼。 但是，AEM Forms服務始終將位元組陣列類型返回為base64編碼的文本。 輸出位元組陣列參數不支援MTOM。

返回大量二進位資料的AEM Forms服務使用Document/BLOB類型，而不是位元組陣列類型。 文檔類型在傳輸大量資料時效率更高。

## Web服務資料類型 {#web-service-data-types}

下表列出了Java資料類型並顯示相應的Web服務資料類型。

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
   <td><p>的 <code>DATE</code> 類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms的服務 <code>java.util.Date</code> 值作為輸入，SOAP客戶端應用程式必須在 <code>DATE.date</code> 的子菜單。 設定 <code>DATE.calendar</code> 此情況下，欄位會導致運行時異常。 如果服務返回 <code>java.util.Date</code>，在 <code>DATE.date</code> 的子菜單。</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>的 <code>DATE</code> 類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms的服務 <code>java.util.Calendar</code> 值作為輸入，SOAP客戶端應用程式必須在 <code>DATE.caledendar</code> 的子菜單。 設定 <code>DATE.date</code> 在本例中，欄位會導致運行時異常。 如果服務返回 <code>java.util.Calendar</code>，則在 <code>DATE.calendar</code> 的子菜單。 </p></td>
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
   <td><p>的 <code>apachesoap:Map</code>，在服務WSDL中定義如下：</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>映射被表示為鍵/值對的序列。</p></td>
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
   <td><p>XML類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務操作接受 <code>org.w3c.dom.Document</code> 值，在 <code>XML.document</code> 的子菜單。</p><p>設定 <code>XML.element</code> 欄位會導致運行時異常。 如果服務返回 <code>org.w3c.dom.Document</code>，然後在 <code>XML.document</code> 的子菜單。</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>XML類型，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms的服務 <code>org.w3c.dom.Element</code> 作為輸入，在 <code>XML.element</code> 的子菜單。</p><p>設定 <code>XML.document</code> 欄位會導致運行時異常。 如果服務返回 <code>org.w3c.dom.Element</code>，然後在 <code>XML.element</code> 的子菜單。</p></td>
  </tr>
 </tbody>
</table>

## 使用JAX-WS建立Java代理類 {#creating-java-proxy-classes-using-jax-ws}

可以使用JAX-WS將Forms服務WSDL轉換為Java代理類。 這些類使您能夠調用AEM Forms服務操作。 Apache Ant允許您通過引用AEM Forms服務WSDL來建立生成Java代理類的生成指令碼。 通過執行以下步驟，可以生成JAX-WS代理檔案：

1. 在客戶機上安裝Apache Ant。 (請參閱 [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)。)

   * 將bin目錄添加到類路徑。
   * 設定 `ANT_HOME` 環境變數到您安裝Ant的目錄。

1. 安裝JDK 1.6或更高版本。

   * 將JDK bin目錄添加到類路徑。
   * 將JRE bin目錄添加到類路徑。 此紙盒位於 `[JDK_INSTALL_LOCATION]/jre` 的子菜單。
   * 設定 `JAVA_HOME` 環境變數到JDK的安裝目錄。

   JDK 1.6包括build.xml檔案中使用的wsimport程式。 JDK 1.5不包含該程式。

1. 在客戶機上安裝JAX-WS。 (請參閱 [用於XML Web服務的Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)。)
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

   在此Ant生成指令碼中，請注意 `url` 屬性設定為引用在localhost上運行的加密服務WSDL。 的 `username` 和 `password` 必須將屬性設定為有效AEM的表單用戶名和密碼。 請注意，URL包含 `lc_version` 屬性。 不指定 `lc_version` 選項，您無法調用新的AEM Forms服務操作。

   >[!NOTE]
   >
   >替換 `EncryptionService`使用Java代理類調用的AEM Forms服務名。 例如，要為Rights Management服務建立Java代理類，請指定：

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. 建立BAT檔案以執行Ant生成指令碼。 以下命令可位於負責執行Ant生成指令碼的BAT檔案中：

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   將ANT生成指令碼放在C:\Program Files\Java\jaxws-ri\bin directory目錄中。 指令碼將JAVA檔案寫入。/classes資料夾。 該指令碼生成可調用服務的JAVA檔案。

1. 將JAVA檔案打包到JAR檔案中。 如果您正在處理Eclipse，請執行以下步驟：

   * 建立一個新的Java項目，用於將代理JAVA檔案打包到JAR檔案中。
   * 在項目中建立源資料夾。
   * 建立 `com.adobe.idp.services` 檔案包。
   * 選擇 `com.adobe.idp.services` 包，然後將JAVA檔案從adobe/idp/services資料夾中導入到包中。
   * 如有必要，請建立 `org/apache/xml/xmlsoap` 檔案包。
   * 選擇源資料夾，然後從org/apache/xml/xmlsoap資料夾導入JAVA檔案。
   * 將Java編譯器的符合性級別設定為5.0或更高。
   * 生成項目。
   * 將項目導出為JAR檔案。
   * 在客戶端項目的類路徑中導入此JAR檔案。 此外，導入位於 &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty。

   >[!NOTE]
   >
   >使用表單寫程式中的所有Java Web服務快速啟動(除Forms服務外),AEM使用JAX-WS建立Java代理檔案。 此外，所有Java Web服務都會快速啟動，使用SwaRef。 (請參閱 [使用SwaRef調用AEM Forms](#invoking-aem-forms-using-swaref)。)

**另請參閱**

[使用Apache軸建立Java代理類](#creating-java-proxy-classes-using-apache-axis)

[使用Base64編碼調用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[通過HTTP調用AEM Forms使用BLOB資料](#invoking-aem-forms-using-blob-data-over-http)

[使用SwaRef調用AEM Forms](#invoking-aem-forms-using-swaref)

## 使用Apache軸建立Java代理類 {#creating-java-proxy-classes-using-apache-axis}

可以使用Apache Axis WSDL2Java工具將Forms服務轉換為Java代理類。 這些類使您能夠調用Forms服務操作。 使用Apache Ant，可以通過服務WSDL生成Axis庫檔案。 可以在URL下載Apache軸 [https://ws.apache.org/axis/](https://ws.apache.org/axis/)。

>[!NOTE]
>
>與Forms服務關聯的Web服務快速啟動使用使用Apache Axis建立的Java代理類。 FormsWeb服務快速啟動還使用Base64作為編碼類型。 (請參閱 [Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)。)

通過執行以下步驟，可以生成Axis Java庫檔案：

1. 在客戶機上安裝Apache Ant。 可在以下位置獲得 [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)。

   * 將bin目錄添加到類路徑。
   * 設定 `ANT_HOME` 環境變數到您安裝Ant的目錄。

1. 在客戶機上安裝Apache Axis 1.4。 可在以下位置獲得 [https://ws.apache.org/axis/](https://ws.apache.org/axis/)。
1. 設定類路徑以在Web服務客戶端中使用Axis JAR檔案，如Axis安裝說明中所述 [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html)。
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

   在此Ant生成指令碼中，請注意 `url` 屬性設定為引用在localhost上運行的加密服務WSDL。 的 `username` 和 `password` 必須將屬性設定為有效AEM的表單用戶名和密碼。

1. 建立BAT檔案以執行Ant生成指令碼。 以下命令可位於負責執行Ant生成指令碼的BAT檔案中：

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA檔案將寫入C:\JavaFiles folder as specified by the目錄 `output` 屬性。 要成功調用Forms服務，請將這些JAVA檔案導入到類路徑中。

   預設情況下，這些檔案屬於名為 `com.adobe.idp.services`。 建議將這些JAVA檔案放入JAR檔案。 然後，將JAR檔案導入到客戶端應用程式的類路徑中。

   >[!NOTE]
   >
   >將.JAVA檔案放入JAR有不同的方法。 一種方法是使用Java IDE，如Eclipse。 建立Java項目並建立 `com.adobe.idp.services`包（所有.JAVA檔案都屬於此包）。 然後，將所有.JAVA檔案導入包。 最後，將項目導出為JAR檔案。

1. 修改中的URL `EncryptionServiceLocator` 類以指定編碼類型。 例如，要使用base64，請指定 `?blob=base64` 確保 `BLOB` 對象返回二進位資料。 就是，在 `EncryptionServiceLocator` 類，找到以下代碼行：

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   並將其更改為：

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. 將以下Axis JAR檔案添加到Java項目的類路徑：

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio_jar
   * jaxen-1.1β-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   這些JAR檔案位於 `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` 的子菜單。

**另請參閱**

[使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws)

[使用Base64編碼調用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[通過HTTP調用AEM Forms使用BLOB資料](#invoking-aem-forms-using-blob-data-over-http)

## 使用Base64編碼調用AEM Forms {#invoking-aem-forms-using-base64-encoding}

可以使用Base64編碼調用AEM Forms服務。 Base64編碼對隨Web服務調用請求發送的附件進行編碼。 就是， `BLOB` 資料是Base64編碼的，不是整個SOAP消息。

「使用Base64編碼調用AEM Forms」討論調用以下名為的AEM Forms短生命進程 `MyApplication/EncryptDocument` 使用Base64編碼。

>[!NOTE]
>
>該進程不基於現有的AEM Forms進程。 要跟隨代碼示例，請建立一個名為 `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

調用此進程時，它執行以下操作：

1. 獲取傳遞給流程的無擔保PDF文檔。 此操作基於 `SetValue` 的下界。 此進程的輸入參數是 `document` 進程變數命名 `inDoc`。
1. 使用密碼加密PDF文檔。 此操作基於 `PasswordEncryptPDF` 的下界。 密碼加密的PDF文檔在名為 `outDoc`。

### 建立使用Base64編碼的.NET客戶端程式集 {#creating-a-net-client-assembly-that-uses-base64-encoding}

您可以建立.NET客戶端程式集，以從MicrosoftVisual Studio .NET項目調用Forms服務。 要建立使用base64編碼的.NET客戶端程式集，請執行以下步驟：

1. 基於AEM Forms調用URL建立代理類。
1. 建立生成.NET客戶端程式集的MicrosoftVisual Studio .NET項目。

**建立代理類**

您可以使用隨MicrosoftVisual Studio一起提供的工具建立用於建立.NET客戶端程式集的代理類。 工具的名稱為wsdl.exe，它位於MicrosoftVisual Studio安裝資料夾中。 要建立代理類，請開啟命令提示符並導航到包含wsdl.exe檔案的資料夾。 有關wsdl.exe工具的詳細資訊，請參見 *MSDN幫助*。

在命令提示符下輸入以下命令：

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

預設情況下，此工具會在基於WSDL名稱的同一資料夾中建立CS檔案。 在這種情況下，它會建立一個名為 *EncryptDocumentService.cs*。 使用此CS檔案可建立代理對象，該對象允許您調用在調用URL中指定的服務。

修改代理類中的URL以包括 `?blob=base64` 確保 `BLOB` 對象返回二進位資料。 在代理類中，找到以下代碼行：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

並將其更改為：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

的 *使用Base64編碼調用AEM Forms* 節使用 `MyApplication/EncryptDocument` 例如， 如果要為另一個Forms服務建立.NET客戶端程式集，請確保替換 `MyApplication/EncryptDocument` 以及服務的名稱。

**開發.NET客戶端程式集**

建立生成.NET客戶端程式集的Visual Studio類庫項目。 可以使用wsdl.exe建立的CS檔案可以導入到此項目中。 此項目生成一個DLL檔案（.NET客戶端程式集），您可以在其他Visual Studio .NET項目中使用該檔案來調用服務。

1. 啟動MicrosoftVisual Studio .NET。
1. 建立類庫項目並將其命名為DocumentService。
1. 導入使用wsdl.exe建立的CS檔案。
1. 在 **項目** 菜單，選擇 **添加引用**。
1. 在「添加參照」(Add Reference)對話框中，選擇 **System.Web.Services.dll**。
1. 按一下 **選擇** 然後按一下 **確定**。
1. 編譯和生成項目。

>[!NOTE]
>
>此過程建立名為DocumentService.dll的.NET客戶端程式集，您可以使用它將SOAP請求發送到 `MyApplication/EncryptDocument` 服務。

>[!NOTE]
>
>確保已添加 `?blob=base64` 到用於建立.NET客戶端程式集的代理類中的URL。 否則，無法從 `BLOB` 的雙曲餘切值。

**引用.NET客戶端程式集**

將新建立的.NET客戶端程式集放置在正在開發客戶端應用程式的電腦上。 將.NET客戶端程式集放置到目錄後，可從項目中引用它。 還引用 `System.Web.Services` 庫。 如果未引用此庫，則無法使用.NET客戶端程式集調用服務。

1. 在 **項目** 菜單，選擇 **添加引用**。
1. 按一下 **.NET** 頁籤。
1. 按一下 **瀏覽** 找到DocumentService.dll檔案。
1. 按一下 **選擇** 然後按一下 **確定**。

**使用使用Base64編碼的.NET客戶端程式集調用服務**

您可以調用 `MyApplication/EncryptDocument` 服務（在Workbench中構建），使用使用Base64編碼的.NET客戶端程式集。 調用 `MyApplication/EncryptDocument` 執行以下步驟：

1. 建立一個Microsoft.NET客戶端程式集， `MyApplication/EncryptDocument` 服務WSDL。
1. 建立客戶端Microsoft.NET項目。 在客戶端項目中引用Microsoft.NET客戶端程式集。 也引用 `System.Web.Services`。
1. 使用Microsoft.NET客戶端程式集，建立 `MyApplication_EncryptDocumentService` 調用其預設建構子。
1. 設定 `MyApplication_EncryptDocumentService` 對象 `Credentials` 具有 `System.Net.NetworkCredential` 的雙曲餘切值。 在 `System.Net.NetworkCredential` 建構子，指AEM定表單用戶名和相應密碼。 設定身份驗證值，使您的.NET客戶端應用程式能夠成功與AEM Forms交換SOAP消息。
1. 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存傳遞到PDF文檔 `MyApplication/EncryptDocument` 處理。
1. 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示PDF文檔的檔案位置和開啟檔案的模式。
1. 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
1. 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
1. 填充 `BLOB` 通過指定對象 `binaryData` 屬性。
1. 調用 `MyApplication/EncryptDocument` 通過調用 `MyApplication_EncryptDocumentService` 對象 `invoke` 方法和傳遞 `BLOB` 包含PDF文檔的對象。 此過程將返回加密的PDF文檔 `BLOB` 的雙曲餘切值。
1. 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個字串值，該字串值表示密碼加密文檔的檔案位置。
1. 建立一個位元組陣列，用於儲存 `BLOB` 由 `MyApplicationEncryptDocumentService` 對象 `invoke` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `binaryData` 資料成員。
1. 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
1. 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

### 使用Java代理類和Base64編碼調用服務 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

可以使用Java代理類和Base64調用AEM Forms服務。 調用 `MyApplication/EncryptDocument` 服務，請執行以下步驟：

1. 使用JAX-WS建立Java代理類，該類使用 `MyApplication/EncryptDocument` 服務WSDL。 使用以下WSDL終結點：

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >替換 `hiro-xp` *J2EE應用程式伺服器的IP地址托管AEM Forms。*

1. 將使用JAX-WS建立的Java代理類打包到JAR檔案中。
1. 包括位於以下路徑中的Java代理JAR檔案和JAR檔案：

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到Java客戶端項目的類路徑中。

1. 建立 `MyApplicationEncryptDocumentService` 對象。
1. 建立 `MyApplicationEncryptDocument` 通過調用 `MyApplicationEncryptDocumentService` 對象 `getEncryptDocument` 的雙曲餘切值。
1. 通過為以下資料成員分配值來設定調用AEM Forms所需的連接值：

   * 將WSDL終結點和編碼類型分配給 `javax.xml.ws.BindingProvider` 對象 `ENDPOINT_ADDRESS_PROPERTY` 的子菜單。 調用 `MyApplication/EncryptDocument` 使用Base64編碼的服務，請指定以下URL值：

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * 將表AEM單用戶分配給 `javax.xml.ws.BindingProvider` 對象 `USERNAME_PROPERTY` 的子菜單。
   * 將相應的密碼值分配給 `javax.xml.ws.BindingProvider` 對象 `PASSWORD_PROPERTY` 的子菜單。

   以下代碼示例顯示了此應用程式邏輯：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 檢索要發送到的PDF文檔 `MyApplication/EncryptDocument` 通過建立 `java.io.FileInputStream` 對象。 傳遞一個字串值，指定PDF文檔的位置。
1. 建立位元組陣列，並使用 `java.io.FileInputStream` 的雙曲餘切值。
1. 建立 `BLOB` 對象。
1. 填充 `BLOB` 通過調用對象 `setBinaryData` 和傳遞位元組陣列。 的 `BLOB` 對象 `setBinaryData` 是使用Base64編碼時調用的方法。 請參閱在服務請求中提供BLOB對象。
1. 調用 `MyApplication/EncryptDocument` 通過調用 `MyApplicationEncryptDocument` 對象 `invoke` 的雙曲餘切值。 通過 `BLOB` 包含PDF文檔的對象。 調用方法返回 `BLOB` 包含加密PDF文檔的對象。
1. 通過調用包含加密PDF文檔的位元組陣列 `BLOB` 對象 `getBinaryData` 的雙曲餘切值。
1. 將加密的PDF文檔另存為PDF檔案。 將位元組陣列寫入檔案。

**另請參閱**

[快速啟動：使用Java代理檔案和Base64編碼調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[建立使用Base64編碼的.NET客戶端程式集](#creating-a-net-client-assembly-that-uses-base64-encoding)

## 使用MTOM調用AEM Forms {#invoking-aem-forms-using-mtom}

可以使用Web服務標準MTOM調用AEM Forms服務。 此標準定義二進位資料(如PDF文檔)如何通過Internet或Intranet傳輸。 MTOM的一個特點是 `XOP:Include` 的子菜單。 此元素在XML二進位優化打包(XOP)規範中定義，以引用SOAP消息的二進位附件。

這裡討論的是使用MTOM來調用以下名為「AEM Forms短命進程」的進程 `MyApplication/EncryptDocument`。

>[!NOTE]
>
>該進程不基於現有的AEM Forms進程。 要跟隨代碼示例，請建立一個名為 `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

調用此進程時，它執行以下操作：

1. 獲取傳遞給流程的無擔保PDF文檔。 此操作基於 `SetValue` 的下界。 此進程的輸入參數是 `document` 進程變數命名 `inDoc`。
1. 使用密碼加密PDF文檔。 此操作基於 `PasswordEncryptPDF` 的下界。 密碼加密的PDF文檔在名為 `outDoc`。

>[!NOTE]
>
>MTOM支援在AEM Forms第9版中添加。

>[!NOTE]
>
>使用MTOM傳輸協定的基於JAX WS的應用程式被限制為25MB的發送和接收資料。 此限制是由於JAX-WS中存在錯誤。 如果已發送和已接收檔案的總大小超過25MB，請使用SwaRef傳輸協定，而不是MTOM協定。 否則，就有可能 `OutOfMemory` 例外。

這裡討論的是在Microsoft.NET項目中使用MTOM來調用AEM Forms服務。 使用的.NET框架為3.5，開發環境為Visual Studio 2008。 如果您的開發電腦上安裝了Web服務增強(WSE)，請將其刪除。 .NET 3.5框架支援名為Windows Communication Foundation(WCF)的SOAP框架。 使用MTOM調用AEM Forms時，僅支援WCF（而非WSE）。

### 建立使用MTOM調用服務的.NET項目 {#creating-a-net-project-that-invokes-a-service-using-mtom}

您可以建立一個Microsoft.NET項目，該項目可以使用Web服務調用AEM Forms服務。 首先，使用Visual Studio 2008建立Microsoft.NET項目。 要調用AEM Forms服務，請建立要在項目中調用的AEM Forms服務的服務引用。 建立服務引用時，請指定AEM Forms服務的URL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

替換 `localhost` J2EE應用程式伺服器的IP地址托管AEM Forms。 替換 `MyApplication/EncryptDocument` 以AEM Forms服務的名稱調用。 例如，要調用Rights Management操作，請指定：

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

的 `lc_version` 選項確保AEM Forms功能（如MTOM）可用。 不指定 `lc_version` 選項，您不能使用MTOM調用AEM Forms。

建立服務引用後，與AEM Forms服務關聯的資料類型可在.NET項目中使用。 要建立調用AEM Forms服務的.NET項目，請執行以下步驟：

1. 使用MicrosoftVisual Studio 2008建立.NET項目。
1. 在 **項目** 菜單，選擇 **添加服務引用**。
1. 在 **地址** 對話框，指定AEM Forms服務的WSDL。 例如，

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. 按一下 **開始** 然後按一下 **確定**。

### 在.NET項目中使用MTOM調用服務 {#invoking-a-service-using-mtom-in-a-net-project}

考慮 `MyApplication/EncryptDocument` 接受不安全PDF文檔並返回密碼加密PDF文檔的流程。 調用 `MyApplication/EncryptDocument` 使用MTOM處理（在Workbench中生成），請執行以下步驟：

1. 建立Microsoft.NET項目。
1. 建立 `MyApplication_EncryptDocumentClient` 對象。
1. 建立 `MyApplication_EncryptDocumentClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務和編碼類型：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請確保指定 `?blob=mtom`。

   >[!NOTE]
   >
   >替換 `hiro-xp` *J2EE應用程式伺服器的IP地址托管AEM Forms。*

1. 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `EncryptDocumentClient.Endpoint.Binding` 資料成員。 將返回值強制轉換為 `BasicHttpBinding`。
1. 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 資料成員 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
1. 通過執行以下任務啟用基本HTTP身份驗證：

   * 為數AEM據成員分配表單用戶名 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`。
   * 為資料成員分配相應的口令值 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`。
   * 分配常數值 `HttpClientCredentialType.Basic` 到資料成員 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到資料成員 `BasicHttpBindingSecurity.Security.Mode`。

   以下代碼示例顯示了這些任務。

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

1. 建立 `BLOB` 對象。 的 `BLOB` 對象用於儲存要傳遞給PDF文檔 `MyApplication/EncryptDocument` 處理。
1. 建立 `System.IO.FileStream` 調用其建構子。 傳遞一個字串值，該字串值表示PDF文檔的檔案位置和開啟檔案的模式。
1. 建立一個位元組陣列，用於儲存 `System.IO.FileStream` 的雙曲餘切值。 通過獲取 `System.IO.FileStream` 對象 `Length` 屬性。
1. 通過調用 `System.IO.FileStream` 對象 `Read` 的雙曲餘切值。 傳遞要讀取的位元組陣列、起始位置和流長度。
1. 填充 `BLOB` 通過指定對象 `MTOM` 包含位元組陣列內容的資料成員。
1. 調用 `MyApplication/EncryptDocument` 通過調用 `MyApplication_EncryptDocumentClient` 對象 `invoke` 的雙曲餘切值。 通過 `BLOB` 包含PDF文檔的對象。 此過程將返回加密的PDF文檔 `BLOB` 的雙曲餘切值。
1. 建立 `System.IO.FileStream` 通過調用其建構子並傳遞一個字串值來表示安全PDF文檔的檔案位置。
1. 建立一個位元組陣列，用於儲存 `BLOB` 返回的對象 `invoke` 的雙曲餘切值。 通過獲取 `BLOB` 對象 `MTOM` 資料成員。
1. 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
1. 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

>[!NOTE]
>
>大多數AEM Forms服務運營都有MTOM快速啟動。 您可以在服務的相應快速啟動部分中查看這些快速啟動。 例如，要查看「輸出快速啟動」部分，請參見 [輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**另請參閱**

[快速啟動：在.NET項目中使用MTOM調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[使用Web服務訪問多個服務](#accessing-multiple-services-using-web-services)

[建立ASP.NET Web應用程式，該應用程式調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## 使用SwaRef調用AEM Forms {#invoking-aem-forms-using-swaref}

您可以使用SwaRef調用AEM Forms服務。 內容 `wsi:swaRef` XML元素作為附件發送到SOAP主體中，該主體儲存對附件的引用。 使用SwaRef調用Forms服務時，使用Java API for XML Web Services(JAX-WS)建立Java代理類。 (請參閱 [用於XML Web服務的Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)。)

這裡討論的是如何調用以下名為&quot;Forms短命過程&quot;的過程 `MyApplication/EncryptDocument` 使用SwaRef。

>[!NOTE]
>
>該進程不基於現有的AEM Forms進程。 要跟隨代碼示例，請建立一個名為 `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

調用此進程時，它執行以下操作：

1. 獲取傳遞給流程的無擔保PDF文檔。 此操作基於 `SetValue` 的下界。 此進程的輸入參數是 `document` 進程變數命名 `inDoc`。
1. 使用密碼加密PDF文檔。 此操作基於 `PasswordEncryptPDF` 的下界。 密碼加密的PDF文檔在名為 `outDoc`。

>[!NOTE]
>
>SwaRef在AEM Forms添加了支援

下面的討論是如何在Java客戶端應用程式中使用SwaRef來調用Forms服務。 Java應用程式使用使用JAX-WS建立的代理類。

### 使用使用SwaRef的JAX-WS庫檔案調用服務 {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

調用 `MyApplication/EncryptDocument` 使用使用JAX-WS和SwaRef建立的Java代理檔案進行處理，請執行以下步驟：

1. 使用JAX-WS建立Java代理類，該類使用 `MyApplication/EncryptDocument` 服務WSDL。 使用以下WSDL終結點：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   有關資訊，請參見 [使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws)。

   >[!NOTE]
   >
   >替換 `hiro-xp` *J2EE應用程式伺服器的IP地址托管AEM Forms。*

1. 將使用JAX-WS建立的Java代理類打包到JAR檔案中。
1. 包括位於以下路徑中的Java代理JAR檔案和JAR檔案：

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到Java客戶端項目的類路徑中。

1. 建立 `MyApplicationEncryptDocumentService` 對象。
1. 建立 `MyApplicationEncryptDocument` 通過調用 `MyApplicationEncryptDocumentService` 對象 `getEncryptDocument` 的雙曲餘切值。
1. 通過為以下資料成員分配值來設定調用AEM Forms所需的連接值：

   * 將WSDL終結點和編碼類型分配給 `javax.xml.ws.BindingProvider` 對象 `ENDPOINT_ADDRESS_PROPERTY` 的子菜單。 調用 `MyApplication/EncryptDocument` 使用SwaRef編碼的服務，請指定以下URL值：

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * 將表AEM單用戶分配給 `javax.xml.ws.BindingProvider` 對象 `USERNAME_PROPERTY` 的子菜單。
   * 將相應的密碼值分配給 `javax.xml.ws.BindingProvider` 對象 `PASSWORD_PROPERTY` 的子菜單。

   以下代碼示例顯示了此應用程式邏輯：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 檢索要發送到的PDF文檔 `MyApplication/EncryptDocument` 通過建立 `java.io.File` 對象。 傳遞一個字串值，指定PDF文檔的位置。
1. 建立 `javax.activation.DataSource` 對象 `FileDataSource` 建構子。 通過 `java.io.File` 的雙曲餘切值。
1. 建立 `javax.activation.DataHandler` 使用其建構子並傳遞對象 `javax.activation.DataSource` 的雙曲餘切值。
1. 建立 `BLOB` 對象。
1. 填充 `BLOB` 通過調用對象 `setSwaRef` 方法和傳遞 `javax.activation.DataHandler` 的雙曲餘切值。
1. 調用 `MyApplication/EncryptDocument` 通過調用 `MyApplicationEncryptDocument` 對象 `invoke` 方法和傳遞 `BLOB` 包含PDF文檔的對象。 調用方法返回 `BLOB` 包含加密PDF文檔的對象。
1. 填充 `javax.activation.DataHandler` 通過調用 `BLOB` 對象 `getSwaRef` 的雙曲餘切值。
1. 轉換 `javax.activation.DataHandler` 對象 `java.io.InputSteam` 實例 `javax.activation.DataHandler` 對象 `getInputStream` 的雙曲餘切值。
1. 寫入 `java.io.InputSteam` 實例到表示加密的PDF文檔的PDF檔案。

>[!NOTE]
>
>大多數AEM Forms服務操作都有SwaRef快速啟動。 您可以在服務的相應快速啟動部分中查看這些快速啟動。 例如，要查看「輸出快速啟動」部分，請參見 [輸出服務API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**另請參閱**

[快速啟動：在Java項目中使用SwaRef調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## 通過HTTP調用AEM Forms使用BLOB資料 {#invoking-aem-forms-using-blob-data-over-http}

可以使用Web服務調用AEM Forms服務，並通過HTTP傳遞BLOB資料。 通過HTTP傳遞BLOB資料是一種替代技術，而不是使用base64編碼、DIME或MIME。 例如，在使用Web服務增強3.0的Microsoft.NET項目中，可以通過HTTP傳遞資料，該增強不支援DIME或MIME。 在HTTP上使用BLOB資料時，在調用AEM Forms服務之前上載輸入資料。

&quot;通過HTTP調用BLOB資料&quot;討論調用以下名為的AEM Forms短命進程 `MyApplication/EncryptDocument` 通過HTTP傳遞BLOB資料。

>[!NOTE]
>
>該進程不基於現有的AEM Forms進程。 要跟隨代碼示例，請建立一個名為 `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

調用此進程時，它執行以下操作：

1. 獲取傳遞給流程的無擔保PDF文檔。 此操作基於 `SetValue` 的下界。 此進程的輸入參數是 `document` 進程變數命名 `inDoc`。
1. 使用密碼加密PDF文檔。 此操作基於 `PasswordEncryptPDF` 的下界。 密碼加密的PDF文檔在名為 `outDoc`。

>[!NOTE]
>
>建議您熟悉使用SOAP調用AEM Forms。 (請參閱 [使用Web服務調用AEM Forms](#invoking-aem-forms-using-web-services)。)

### 建立使用HTTP上資料的.NET客戶端程式集 {#creating-a-net-client-assembly-that-uses-data-over-http}

要建立使用HTTP上資料的客戶端程式集，請遵循中指定的過程 [使用Base64編碼調用AEM Forms](#invoking-aem-forms-using-base64-encoding)。 但是，請修改代理類中的URL以包括 `?blob=http` 而不是 `?blob=base64`。 此操作可確保資料通過HTTP傳遞。 在代理類中，找到以下代碼行：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

並將其更改為：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**引用.NET clienMyApplication/EncryptDocument程式集**

將新的.NET客戶端程式集放置在正在開發客戶端應用程式的電腦上。 將.NET客戶端程式集放置到目錄後，可從項目中引用它。 引用 `System.Web.Services` 庫。 如果未引用此庫，則無法使用.NET客戶端程式集調用服務。

1. 在 **項目** 菜單，選擇 **添加引用**。
1. 按一下 **.NET** 頁籤。
1. 按一下 **瀏覽** 找到DocumentService.dll檔案。
1. 按一下 **選擇** 然後按一下 **確定**。

**使用.NET客戶端程式集調用使用BLOB資料（通過HTTP）的服務**

您可以調用 `MyApplication/EncryptDocument` 服務（在Workbench中構建），使用通過HTTP使用資料的.NET客戶端程式集。 調用 `MyApplication/EncryptDocument` 執行以下步驟：

1. 建立.NET客戶端程式集。
1. 引用Microsoft.NET客戶端程式集。 建立客戶端Microsoft.NET項目。 在客戶端項目中引用Microsoft.NET客戶端程式集。 也引用 `System.Web.Services`。
1. 使用Microsoft.NET客戶端程式集，建立 `MyApplication_EncryptDocumentService` 調用其預設建構子。
1. 設定 `MyApplication_EncryptDocumentService` 對象 `Credentials` 具有 `System.Net.NetworkCredential` 的雙曲餘切值。 在 `System.Net.NetworkCredential` 建構子，指AEM定表單用戶名和相應密碼。 設定身份驗證值，使您的.NET客戶端應用程式能夠成功與AEM Forms交換SOAP消息。
1. 建立 `BLOB` 對象。 的 `BLOB` 對象用於將資料傳遞到 `MyApplication/EncryptDocument` 處理。
1. 為 `BLOB` 對象 `remoteURL` 指定要傳遞到的PDF文檔的URI位置的資料成員 `MyApplication/EncryptDocument`服務。
1. 調用 `MyApplication/EncryptDocument` 通過調用 `MyApplication_EncryptDocumentService` 對象 `invoke` 方法和傳遞 `BLOB` 的雙曲餘切值。 此過程將返回加密的PDF文檔 `BLOB` 的雙曲餘切值。
1. 建立 `System.UriBuilder` 對象，使用其建構子並傳遞返回的值 `BLOB` 對象 `remoteURL` 資料成員。
1. 轉換 `System.UriBuilder` 對象 `System.IO.Stream` 的雙曲餘切值。 （此清單後面的C#快速啟動說明了如何執行此任務。）
1. 建立位元組陣列，並使用位於 `System.IO.Stream` 的雙曲餘切值。
1. 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
1. 通過調用 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

### 使用Java代理類和BLOB資料通過HTTP調用服務 {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

可以使用Java代理類和BLOB資料通過HTTP調用AEM Forms服務。 調用 `MyApplication/EncryptDocument` 服務，請執行以下步驟：

1. 使用JAX-WS建立Java代理類，該類使用 `MyApplication/EncryptDocument` 服務WSDL。 使用以下WSDL終結點：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   有關資訊，請參見 [使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws)。

   >[!NOTE]
   >
   >替換 `hiro-xp` *J2EE應用程式伺服器的IP地址托管AEM Forms。*

1. 將使用JAX-WS建立的Java代理類打包到JAR檔案中。
1. 包括位於以下路徑中的Java代理JAR檔案和JAR檔案：

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到Java客戶端項目的類路徑中。

1. 建立 `MyApplicationEncryptDocumentService` 對象。
1. 建立 `MyApplicationEncryptDocument` 通過調用 `MyApplicationEncryptDocumentService` 對象 `getEncryptDocument` 的雙曲餘切值。
1. 通過為以下資料成員分配值來設定調用AEM Forms所需的連接值：

   * 將WSDL終結點和編碼類型分配給 `javax.xml.ws.BindingProvider` 對象 `ENDPOINT_ADDRESS_PROPERTY` 的子菜單。 調用 `MyApplication/EncryptDocument` 使用BLOB over HTTP編碼的服務，請指定以下URL值：

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * 將表AEM單用戶分配給 `javax.xml.ws.BindingProvider` 對象 `USERNAME_PROPERTY` 的子菜單。
   * 將相應的密碼值分配給 `javax.xml.ws.BindingProvider` 對象 `PASSWORD_PROPERTY` 的子菜單。

   以下代碼示例顯示了此應用程式邏輯：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 建立 `BLOB` 對象。
1. 填充 `BLOB` 通過調用對象 `setRemoteURL` 的雙曲餘切值。 傳遞一個字串值，該字串值指定要傳遞到的PDF文檔的URI位置 `MyApplication/EncryptDocument` 服務。
1. 調用 `MyApplication/EncryptDocument` 通過調用 `MyApplicationEncryptDocument` 對象 `invoke` 方法和傳遞 `BLOB` 包含PDF文檔的對象。 此過程將返回加密的PDF文檔 `BLOB` 的雙曲餘切值。
1. 建立位元組陣列以儲存表示加密PDF文檔的資料流。 調用 `BLOB` 對象 `getRemoteURL` 方法(使用 `BLOB` 由 `invoke` )。
1. 建立 `java.io.File` 對象。 此對象表示加密的PDF文檔。
1. 建立 `java.io.FileOutputStream` 使用其建構子並傳遞對象 `java.io.File` 的雙曲餘切值。
1. 調用 `java.io.FileOutputStream` 對象 `write` 的雙曲餘切值。 傳遞包含表示加密PDF文檔的資料流的位元組陣列。

## 使用DIME調用AEM Forms {#invoking-aem-forms-using-dime}

您可以使用帶附件的SOAP調用AEM Forms服務。 AEM Forms支援MIME和DIME Web服務標準。 DIME允許您發送二進位附件(如PDF文檔)以及調用請求，而不是對附件進行編碼。 的 *使用DIME調用AEM Forms* 部分討論調用以下名為的AEM Forms短期進程 `MyApplication/EncryptDocument` 用DIME。

調用此進程時，它執行以下操作：

1. 獲取傳遞給流程的無擔保PDF文檔。 此操作基於 `SetValue` 的下界。 此進程的輸入參數是 `document` 進程變數命名 `inDoc`。
1. 使用密碼加密PDF文檔。 此操作基於 `PasswordEncryptPDF` 的下界。 密碼加密的PDF文檔在名為 `outDoc`。

該進程不基於現有的AEM Forms進程。 要跟隨代碼示例，請建立一個名為 `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

>[!NOTE]
>
>不建議使用DIME調用AEM Forms服務操作。 建議您使用MTOM。 (請參閱 [使用MTOM調用AEM Forms](#invoking-aem-forms-using-mtom)。)

### 建立使用DIME的.NET項目 {#creating-a-net-project-that-uses-dime}

要建立可使用DIME調用Forms服務的.NET項目，請執行以下任務：

* 在開發電腦上安裝Web服務增強2.0。
* 在.NET項目中，建立對FormsAEMForms服務的Web引用。

**安裝Web服務增強2.0**

在您的開發電腦上安裝Web服務增強2.0，並將其與MicrosoftVisual Studio .NET整合。 可以從 [Microsoft下載中心。](https://www.microsoft.com/downloads/search.aspx)

從此網頁中，搜索Web服務增強2.0並將其下載到您的開發電腦上。 此下載內容將名為MicrosoftWSE 2.0 SPI.msi的檔案放在您的電腦上。 運行安裝程式並遵循聯機說明。

>[!NOTE]
>
>Web服務增強2.0支援DIME。 使用Web服務增強2.0時，支援的MicrosoftVisual Studio版本為2003。Web服務增強3.0不支援DIME;但支援MTOM。

**建立對AEM Forms服務的Web引用**

在開發電腦上安裝Web服務增強2.0並建立Microsoft.NET項目後，請建立對Forms服務的Web引用。 例如，要建立對 `MyApplication/EncryptDocument` 進程，並假設Forms已安裝在本地電腦上，請指定以下URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

建立Web引用後，以下兩種代理資料類型可供您在.NET項目中使用： `EncryptDocumentService` 和 `EncryptDocumentServiceWse`。 調用 `MyApplication/EncryptDocument` 進程使用DIME，使用 `EncryptDocumentServiceWse` 的雙曲餘切值。

>[!NOTE]
>
>在建立對Forms服務的Web引用之前，請確保在項目中引用Web服務增強2.0。 （請參閱安裝Web服務增強2.0。）

**引用WSE庫**

1. 在「項目」菜單中，選擇「添加引用」。
1. 在「添加引用」對話框中，選擇「Microsoft」.Web.Services2.dll。
1. 選擇System.Web.Services.dll。
1. 按一下「Select（選擇）」 ，然後按一下「OK（確定）」。

**建立對Forms服務的Web引用**

1. 在「項目」菜單中，選擇「添加Web引用」。
1. 在「URL」對話框中，指定Forms服務的URL。
1. 按一下「Go（開始）」 ，然後按一下「Add Reference（添加參照）」。

>[!NOTE]
>
>確保啟用.NET項目以使用WSE庫。 在「項目瀏覽器」中，按一下右鍵項目名稱並選擇「啟用WSE 2.0」。確保選中了所顯示對話框上的複選框。

**在.NET項目中使用DIME調用服務**

您可以使用DIME調用Forms服務。 考慮 `MyApplication/EncryptDocument` 接受不安全PDF文檔並返回密碼加密PDF文檔的流程。 調用 `MyApplication/EncryptDocument` 處理時，請執行以下步驟：

1. 建立一個Microsoft.NET項目，使您能夠使用DIME調用Forms服務。 確保包括Web服務增強2.0並建立對AEM Forms服務的Web引用。
1. 將Web引用設定為 `MyApplication/EncryptDocument` 進程，建立 `EncryptDocumentServiceWse` 對象。
1. 設定 `EncryptDocumentServiceWse` 對象 `Credentials` 資料成員 `System.Net.NetworkCredential` 指定表單AEM用戶名和密碼值的值。
1. 建立 `Microsoft.Web.Services2.Dime.DimeAttachment` 對象，並傳遞以下值：

   * 指定GUID值的字串值。 通過調用 `System.Guid.NewGuid.ToString` 的雙曲餘切值。
   * 指定內容類型的字串值。 由於此過程需要PDF文檔，請指定 `application/pdf`。
   * A `TypeFormat` 枚舉值。 指定 `TypeFormat.MediaType`。
   * 一個字串值，它指定要傳遞到AEM Forms進程的PDF文檔的位置。

1. 建立 `BLOB` 對象。
1. 將DIME附件添加到 `BLOB` 對象 `Microsoft.Web.Services2.Dime.DimeAttachment` 對象 `Id` 資料成員值到 `BLOB` 對象 `attachmentID` 資料成員。
1. 調用 `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` 方法和通過 `Microsoft.Web.Services2.Dime.DimeAttachment` 的雙曲餘切值。
1. 調用 `MyApplication/EncryptDocument` 通過調用 `EncryptDocumentServiceWse` 對象 `invoke` 方法和傳遞 `BLOB` 包含DIME附件的對象。 此過程將返回加密的PDF文檔 `BLOB` 的雙曲餘切值。
1. 通過獲取返回的附件的值來獲取附件標識符值 `BLOB` 對象 `attachmentID` 資料成員。
1. 循環訪問位於 `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` 並使用附件標識符值獲取加密的PDF文檔。
1. 獲取 `System.IO.Stream` 通過獲取 `Attachment` 對象 `Stream` 資料成員。
1. 建立一個位元組陣列，並將該位元組陣列傳遞給 `System.IO.Stream` 對象 `Read` 的雙曲餘切值。 此方法使用表示加密PDF文檔的資料流填充位元組陣列。
1. 建立 `System.IO.FileStream` 對象，方法是調用其建構子並傳遞一個表示PDF檔案位置的字串值。 此對象表示加密的PDF文檔。
1. 建立 `System.IO.BinaryWriter` 通過調用其建構子並傳遞對象 `System.IO.FileStream` 的雙曲餘切值。
1. 通過調用PDF檔案，將位元組陣列的內容寫入 `System.IO.BinaryWriter` 對象 `Write` 和傳遞位元組陣列。

### 建立使用DIME的Apache Axis Java代理類 {#creating-apache-axis-java-proxy-classes-that-use-dime}

可以使用Apache Axis WSDL2Java工具將服務WSDL轉換為Java代理類，以便調用服務操作。 使用Apache Ant，可以通過AEM Forms服務WSDL生成Axis庫檔案，該服務允許您調用該服務。 (請參閱 [使用Apache軸建立Java代理類](#creating-java-proxy-classes-using-apache-axis)。)

Apache Axis WSDL2Java工具生成包含用於向服務發送SOAP請求的方法的JAVA檔案。 由服務接收的SOAP請求由Axis生成的庫解碼，並返回為方法和參數。

調用 `MyApplication/EncryptDocument` 使用Axis生成的庫檔案和DIME的服務（在Workbench中內置），請執行以下步驟：

1. 建立使用 `MyApplication/EncryptDocument` 使用Apache Axis的服務WSDL。 (請參閱 [使用Apache軸建立Java代理類](#creating-java-proxy-classes-using-apache-axis)。)
1. 將Java代理類包括到類路徑中。
1. 建立 `MyApplicationEncryptDocumentServiceLocator` 對象。
1. 建立 `URL` 對象，方法是使用其建構子並傳遞一個指定AEM Forms服務WSDL定義的字串值。 確保指定 `?blob=dime` 在SOAP終結點URL的末尾。 例如，使用

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. 建立 `EncryptDocumentSoapBindingStub` 通過調用其建構子並傳遞對象 `MyApplicationEncryptDocumentServiceLocator`對象和 `URL` 的雙曲餘切值。
1. 通過調AEM用表單用戶名和密碼值 `EncryptDocumentSoapBindingStub` 對象 `setUsername` 和 `setPassword` 的雙曲餘切值。

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. 檢索要發送到的PDF文檔 `MyApplication/EncryptDocument` 通過建立 `java.io.File` 的雙曲餘切值。 傳遞指定PDF文檔位置的字串值。
1. 建立 `javax.activation.DataHandler` 使用其建構子並傳遞對象 `javax.activation.FileDataSource` 的雙曲餘切值。 的 `javax.activation.FileDataSource` 可以使用其建構子並傳遞對象 `java.io.File` 表示PDF文檔的對象。
1. 建立 `org.apache.axis.attachments.AttachmentPart` 使用其建構子並傳遞對象 `javax.activation.DataHandler` 的雙曲餘切值。
1. 通過調用 `EncryptDocumentSoapBindingStub` 對象 `addAttachment` 方法和傳遞 `org.apache.axis.attachments.AttachmentPart` 的雙曲餘切值。
1. 建立 `BLOB` 對象。 填充 `BLOB` 通過調用 `BLOB` 對象 `setAttachmentID` 和傳遞附件標識符值。 通過調用 `org.apache.axis.attachments.AttachmentPart` 對象 `getContentId` 的雙曲餘切值。
1. 調用 `MyApplication/EncryptDocument` 通過調用 `EncryptDocumentSoapBindingStub` 對象 `invoke` 的雙曲餘切值。 通過 `BLOB` 包含DIME附件的對象。 此過程將返回加密的PDF文檔 `BLOB` 的雙曲餘切值。
1. 通過調用返回的附件標識符值 `BLOB` 對象 `getAttachmentID` 的雙曲餘切值。 此方法返回一個字串值，該字串值表示返回的附件的標識符值。
1. 通過調用 `EncryptDocumentSoapBindingStub` 對象 `getAttachments` 的雙曲餘切值。 此方法返回 `Objects` 表示附件。
1. 循環訪問附件( `Object` 並使用附件標識符值獲取加密的PDF文檔。 每個元素都是 `org.apache.axis.attachments.AttachmentPart` 的雙曲餘切值。
1. 獲取 `javax.activation.DataHandler` 通過調用 `org.apache.axis.attachments.AttachmentPart` 對象 `getDataHandler` 的雙曲餘切值。
1. 獲取 `java.io.FileStream` 通過調用 `javax.activation.DataHandler` 對象 `getInputStream` 的雙曲餘切值。
1. 建立一個位元組陣列，並將該位元組陣列傳遞給 `java.io.FileStream` 對象 `read` 的雙曲餘切值。 此方法使用表示加密PDF文檔的資料流填充位元組陣列。
1. 建立 `java.io.File` 對象。 此對象表示加密的PDF文檔。
1. 建立 `java.io.FileOutputStream` 使用其建構子並傳遞對象 `java.io.File` 的雙曲餘切值。
1. 調用 `java.io.FileOutputStream` 對象 `write` 方法並傳遞包含表示加密PDF文檔的資料流的位元組陣列。

**另請參閱**

[快速啟動：在Java項目中使用DIME調用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## 使用基於SAML的身份驗證 {#using-saml-based-authentication}

AEM Forms在調用服務時支援各種Web服務身份驗證模式。 一種驗證模式是使用Web服務調用中的基本授權頭指定用戶名和密碼值。 AEM Forms還支援基於SAML斷言的身份驗證。 當客戶端應用程式使用web服務調用AEM Forms服務時，客戶端應用程式可以以下列方式之一提供驗證資訊：

* 將憑據作為基本授權的一部分
* 作為WS-Security標頭的一部分傳遞用戶名令牌
* 作為WS-Security標頭的一部分傳遞SAML斷言
* 作為WS-Security標頭的一部分傳遞Kerberos令牌

AEM Forms不支援標準的基於證書的身份驗證，但支援以不同形式進行基於證書的身份驗證。

>[!NOTE]
>
>Web服務快速啟動於使用AEM Forms進行寫程式時，指定用戶名和密碼值以執行授權。

表單用AEM戶的標識可以通過使用密鑰簽名的SAML斷言來表示。 以下XML代碼顯示了SAML斷言的示例。

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

此示例聲明是為管理員用戶發出的。 此斷言包含以下可注意的項：

* 它在特定持續時間內有效。
* 為特定用戶發佈。
* 它是數字簽名的。 因此，對它所做的任何修改都會破壞簽名。
* 它可以作為與用戶名和密碼類似的用戶標識的令牌呈現給AEM Forms。

客戶端應用程式可以從任何返回AuthenticationManager的AEM FormsAPI中檢索斷言 `AuthResult` 的雙曲餘切值。 您可以 `AuthResult` 實例：

* 使用AuthenticationManager API公開的任何驗證方法驗證用戶。 通常，使用用戶名和密碼；但是，您也可以使用證書身份驗證。
* 使用 `AuthenticationManager.getAuthResultOnBehalfOfUser` 的雙曲餘切值。 此方法允許客戶端應用程式獲取 `AuthResult` 任何表單用AEM戶的對象。

使用AEM獲得的SAML令牌對表單用戶進行身份驗證。 此SAML斷言（xml片段）可以作為WS-Security標頭的一部分發送，並通過Web服務調用進行用戶身份驗證。 通常，客戶端應用程式已對用戶進行身份驗證，但未儲存用戶憑據。 （或者用戶已通過使用用戶名和密碼以外的機制登錄到該客戶端。） 在這種情況下，客戶端應用程式必須調用AEM Forms並模擬允許調用AEM Forms的特定用戶。

要模擬特定用戶，請調用 `AuthenticationManager.getAuthResultOnBehalfOfUser` 方法。 此方法返回 `AuthResult` 包含該用戶的SAML斷言的實例。

接下來，使用該SAML斷言來調用任何需要身份驗證的服務。 此操作涉及將斷言作為SOAP標頭的一部分發送。 當使用此斷言進行Web服務調用時，AEM Forms將用戶標識為由該斷言表示的用戶。 即，斷言中指定的用戶是調用服務的用戶。

### 使用Apache Axis類和基於SAML的身份驗證 {#using-apache-axis-classes-and-saml-based-authentication}

可以通過使用Axis庫建立的Java代理類調用AEM Forms服務。 (請參閱 [使用Apache軸建立Java代理類](#creating-java-proxy-classes-using-apache-axis)。)

使用使用基於SAML的身份驗證的AXIS時，請使用Axis註冊請求和響應處理程式。 Apache Axis在向AEM Forms發送調用請求之前調用該處理程式。 要註冊處理程式，請建立擴展的Java類 `org.apache.axis.handlers.BasicHandler`。

**建立帶軸的AssertionHandler**

以下Java類，名為 `AssertionHandler.java`，顯示了擴展的Java類的示例 `org.apache.axis.handlers.BasicHandler`。

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

要向Axis註冊處理程式，請建立client-config.wsdd檔案。 預設情況下，「軸」(Axis)查找具有此名稱的檔案。 以下XML代碼是client-config.wsdd檔案的示例。 有關詳細資訊，請參閱軸文檔。

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

**調用AEM Forms服務**

以下代碼示例使用基於SAML的驗證調用AEM Forms服務。

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

### 使用.NET客戶端程式集和基於SAML的身份驗證 {#using-a-net-client-assembly-and-saml-based-authentication}

可以使用.NET客戶端程式集和基於SAML的身份驗證來調用Forms服務。 為此，必須使用Web服務增強3.0(WSE)。 有關建立使用WSE的.NET客戶端程式集的資訊，請參見 [建立使用DIME的.NET項目](#creating-a-net-project-that-uses-dime)。

>[!NOTE]
>
>DIME部分使用WSE 2.0。要使用基於SAML的身份驗證，請按照DIME主題中指定的相同說明進行操作。 但是，將WSE 2.0替換為WSE 3.0。在開發電腦上安裝Web服務增強3.0，並將其與MicrosoftVisual Studio .NET整合。 可以從 [Microsoft下載中心](https://www.microsoft.com/downloads/search.aspx)。

WSE體系結構使用策略、斷言和SecurityToken資料類型。 簡而言之，對於Web服務調用，請指定策略。 策略可以具有多個斷言。 每個斷言都可以包含篩選器。 在Web服務調用的特定階段調用過濾器，並且在此時，過濾器可以修改SOAP請求。 有關詳細資訊，請參閱Web服務增強3.0文檔。

**建立斷言和篩選器**

下面的C#代碼示例建立篩選器類和斷言類。 此代碼示例建立SamlAssertionOutputFilter。 在將SOAP請求發送到AEM Forms之前，WSE框架會調用此篩選器。

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

**建立SAML令牌**

建立一個類以表示SAML斷言。 此類執行的主要任務是將資料值從字串轉換為xml並保留空白。 此斷言xml稍後會導入到SOAP請求中。

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

**調用AEM Forms服務**

以下C#代碼示例使用基於SAML的身份驗證調用Forms服務。

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

## 使用Web服務時的相關注意事項 {#related-considerations-when-using-web-services}

有時，使用Web服務調用某些AEM Forms服務操作時會出現問題。 本討論的目的是確定這些問題並提供解決辦法（如果有）。

### 非同步調用服務操作 {#invoking-service-operations-asynchronously}

如果嘗試非同步調用AEM Forms服務操作，如生成PDF `htmlToPDF` 操作，a `SoapFaultException` 。 要解決此問題，請建立一個自定義綁定XML檔案，該檔案映射 `ExportPDF_Result` 元素和其他元素到不同類中。 以下XML表示自定義綁定檔案。

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

使用JAX-WS建立Java代理檔案時，請使用此XML檔案。 (請參閱 [使用JAX-WS建立Java代理類](#creating-java-proxy-classes-using-jax-ws)。)

使用 — 執行JAX-WS工具(wsimport.exe)時引用此XML檔案 `b` 命令行選項。 更新 `wsdlLocation` 綁定XML檔案中的元素，以指定AEM Forms的URL。

要確保非同步調用工作，請修改端點URL值並指定 `async=true`。 例如，對於使用JAX-WS建立的Java代理檔案，請為 `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`。

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

以下清單指定非同步調用時需要自定義綁定檔案的其他服務：

* PDFG3D
* 任務管理器
* 應用程式管理器
* 目錄管理器
* Distiller
* Rights Management
* 文檔管理

### J2EE應用程式伺服器的差異 {#differences-in-j2ee-application-servers}

有時，使用特定J2EE應用程式伺服器建立的代理庫無法成功調用承載在不同J2EE應用程式伺服器上的AEM Forms。 請考慮使用部署在WebSphere上的AEM Forms生成的代理庫。 此代理庫無法成功調用部署在JBoss應用程式伺服器上的AEM Forms服務。

某些AEM Forms複雜資料類型，如 `PrincipalReference`，與JBoss應用程式伺服器相比，在WebSphere上部署AEM Forms時定義的不同。 不同J2EE應用程式服務使用的JDK的差異是WSDL定義存在差異的原因。 因此，使用從同一J2EE應用程式伺服器生成的代理庫。

### 使用Web服務訪問多個服務 {#accessing-multiple-services-using-web-services}

由於命名空間衝突，資料對象無法在多個服務WSDL之間共用。 不同的服務可以共用資料類型，因此服務可以在WSDL中共用這些類型的定義。 例如，不能添加包含 `BLOB` 資料類型到同一.NET客戶端項目。 如果嘗試執行此操作，則會出現編譯錯誤。

以下清單指定不能在多個服務WSDL之間共用的資料類型：

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

為避免此問題，建議您完全限定資料類型。 例如，請考慮使用服務引用同時引用Forms服務和簽名服務的.NET應用程式。 兩個服務引用都將包含 `BLOB` 類。 使用 `BLOB` 實例，完全限定 `BLOB` 對象。 此方法在以下代碼示例中顯示。 有關此代碼示例的資訊，請參見 [數字簽名互動式Forms](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)。

以下C#代碼示例標籤由Forms服務呈現的互動式表單。 客戶端應用程式有兩個服務引用。 的 `BLOB` 與Forms服務關聯的實例屬於 `SignInteractiveForm.ServiceReference2` 命名空間。 同樣， `BLOB` 與簽名服務關聯的實例屬於 `SignInteractiveForm.ServiceReference1` 命名空間。 簽名的交互表單將另存為名為的PDF檔案 *LoanXFASfiged.pdf*。

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

### 以字母I開頭的服務生成無效的代理檔案 {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

使用AEM Forms.Net 3.5和WCF時，某些Microsoft生成的代理類的名稱不正確。 當為IBMFilenetContentRepositoryConnector、IDPSchedulerService或名稱以字母I開頭的任何其他服務建立代理類時，會出現此問題。例如，如果IBMFileNetContentRepositoryConnector為 `BMFileNetContentRepositoryConnectorClient`。 生成的代理類中缺少字母I。
