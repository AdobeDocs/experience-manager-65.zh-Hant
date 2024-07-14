---
title: 使用網站服務叫用AEM Forms
description: 使用Web服務叫用AEM Forms程式，並完全支援WSDL產生。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 3139564f-9346-4933-8e39-2e1642bff097
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '9814'
ht-degree: 0%

---

# 使用網站服務叫用AEM Forms {#invoking-aem-forms-using-web-services}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

服務容器中的大多數AEM Forms服務都設定為公開Web服務，並完整支援產生Web服務定義語言(WSDL)。 也就是說，您可以建立使用AEM Forms服務原生SOAP棧疊的Proxy物件。 因此，AEM Forms服務可以交換及處理下列SOAP訊息：

* **SOAP要求**：由使用者端應用程式要求動作傳送至Forms服務。
* **SOAP回應**：在處理SOAP要求之後，由Forms服務傳送至使用者端應用程式。

使用Web服務，您可以使用Java API執行與相同的AEM Forms服務操作。 使用Web服務來叫用AEM Forms服務的好處是，您可以在支援SOAP的開發環境中建立使用者端應用程式。 使用者端應用程式未繫結至特定的開發環境或程式設計語言。 例如，您可以使用Microsoft Visual Studio .NET和C#作為程式設計語言來建立使用者端應用程式。

AEM Forms服務會透過SOAP通訊協定公開，並符合WSI Basic Profile 1.1規範。 Web Services Interoperability (WSI)是一個開放式標準組織，可促進跨平台的Web服務互通性。 如需詳細資訊，請參閱[https://www.ws-i.org/](https://www.ws-i.org)。

AEM Forms支援下列Web服務標準：

* **編碼**：僅支援檔案和常值編碼（根據WSI基本設定檔，這是偏好的編碼）。 (請參閱[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **MTOM**：代表使用SOAP要求編碼附件的方式。 (請參閱[使用MTOM](#invoking-aem-forms-using-mtom)叫用AEM Forms。)
* **SwaRef**：代表使用SOAP要求編碼附件的另一種方式。 (請參閱[使用SwaRef](#invoking-aem-forms-using-swaref)叫用AEM Forms。)
* **具有附件的SOAP**：支援MIME和DIME （直接網際網路訊息封裝）。 這些通訊協定是透過SOAP傳送附件的標準方式。 Microsoft Visual Studio .NET應用程式使用DIME。 (請參閱[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **WS-Security**：支援使用者名稱密碼權杖設定檔，這是在WS Security SOAP標頭中傳送使用者名稱和密碼的標準方式。 AEM Forms也支援HTTP基本驗證。 s

若要使用Web服務來叫用AEM Forms服務，通常會建立使用服務WSDL的Proxy程式庫。 *使用Web服務叫用AEM Forms*&#x200B;區段使用JAX-WS來建立Java Proxy類別以叫用服務。 （請參閱[使用JAX-WS建立Java Proxy類別](#creating-java-proxy-classes-using-jax-ws)。）

您可以指定下列URL定義來擷取服務WDSL （方括弧中的專案是選用的）：

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

其中：

* *your_serverhost*&#x200B;代表裝載AEM Forms之J2EE應用程式伺服器的IP位址。
* *your_port*&#x200B;代表J2EE應用程式伺服器使用的HTTP連線埠。
* *service_name*&#x200B;代表服務名稱。
* *version*&#x200B;代表服務的目標版本（預設使用最新的服務版本）。
* `async`指定值`true`以啟用非同步叫用的其他作業（預設為`false`）。
* *lc_version*&#x200B;代表您要叫用的AEM Forms版本。

下表列出服務WSDL定義(假設AEM Forms已部署在本機主機上，且張貼內容為8080)。

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
   <td><p>返回並還原</p></td>
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
   <td><p>產生3DPDF</p></td>
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

**AEM Forms處理WSDL定義**

在WSDL定義中指定「應用程式」名稱和「處理序」名稱，以存取屬於在Workbench中建立之處理序的WSDL。 假設應用程式的名稱為`MyApplication`，而處理程式的名稱為`EncryptDocument`。 在此情況下，請指定下列WSDL定義：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>如需範例`MyApplication/EncryptDocument`短期處理序的相關資訊，請參閱[短期處理序範例](/help/forms/developing/aem-forms-processes.md)。

>[!NOTE]
>
>應用程式可以包含資料夾。 在這種情況下，請在WSDL定義中指定資料夾名稱：

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**使用Web服務存取新功能**

可使用網站服務存取新的AEM Forms服務功能。 例如，在AEM Forms中引進了使用MTOM編碼附件的功能。 (請參閱[使用MTOM](#invoking-aem-forms-using-mtom)叫用AEM Forms。)

若要存取AEM Forms引入的新功能，請在WSDL定義中指定`lc_version`屬性。 例如，若要存取新的服務功能（包括MTOM支援），請指定下列WSDL定義：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>設定`lc_version`屬性時，請確定您使用三位數。 例如，9.0.1等於版本9.0。

**Web服務BLOB資料型別**

AEM Forms服務WSDL定義許多資料型別。 Web服務中公開的最重要資料型別之一是`BLOB`型別。 使用AEM Forms Java API時，此資料型別對應至`com.adobe.idp.Document`類別。 (請參閱[使用Java API傳遞資料至AEM Forms服務](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)。)

`BLOB`物件會傳送二進位資料(例如，PDF檔案、XML資料等)到與從AEM Forms服務擷取。 `BLOB`型別在服務WSDL中定義如下：

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

只有AEM Forms支援`MTOM`和`swaRef`欄位。 您必須指定包含`lc_version`屬性的URL，才能使用這些新欄位。

**在服務要求中提供BLOB物件**

如果AEM Forms服務操作需要`BLOB`型別作為輸入值，請在應用程式邏輯中建立`BLOB`型別的執行個體。 (*使用AEM表單*&#x200B;進行程式設計時，許多Web服務都會快速啟動，顯示如何使用BLOB資料型別。)

將值指派給屬於`BLOB`執行個體的欄位，如下所示：

* **Base64**：若要以Base64格式編碼的文字傳遞資料，請在`BLOB.binaryData`欄位中設定資料，並在`BLOB.contentType`欄位中以MIME格式（例如，`application/pdf`）設定資料型別。 (請參閱[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **MTOM**：若要在MTOM附件中傳遞二進位資料，請在`BLOB.MTOM`欄位中設定資料。 此設定會使用Java JAX-WS架構或SOAP架構的原生API將資料附加至SOAP要求。 (請參閱[使用MTOM](#invoking-aem-forms-using-mtom)叫用AEM Forms。)
* **SwaRef**：若要在WS-I SwaRef附件中傳遞二進位資料，請在`BLOB.swaRef`欄位中設定資料。 此設定會使用Java JAX-WS架構將資料附加至SOAP要求。 (請參閱[使用SwaRef](#invoking-aem-forms-using-swaref)叫用AEM Forms。)
* **MIME或DIME附件**：若要在MIME或DIME附件中傳遞資料，請使用SOAP架構的原生API將資料附加至SOAP要求。 在`BLOB.attachmentID`欄位中設定附件識別碼。 (請參閱[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **遠端URL**：如果資料託管在Web伺服器上並可透過HTTP URL存取，請在`BLOB.remoteURL`欄位中設定HTTP URL。 (請參閱[透過HTTP](#invoking-aem-forms-using-blob-data-over-http)使用BLOB資料叫用AEM Forms。)

**存取從服務傳回的BLOB物件中的資料**

傳回`BLOB`物件的傳輸通訊協定取決於幾個因素，它們依下列順序考慮，當滿足主要條件時停止：

1. **目標URL指定傳輸通訊協定**。 如果SOAP呼叫時指定的目標URL包含引數&#x200B;`blob="`*BLOB_TYPE*」，則&#x200B;*BLOB_TYPE*&#x200B;會決定傳輸通訊協定。 *BLOB_TYPE*&#x200B;是base64、dime、mime、http、mtom或swaref的預留位置。
1. **服務SOAP端點是Smart**。 如果下列條件為true，則會使用與輸入檔案相同的傳輸通訊協定來傳回輸出檔案：

   * 服務的SOAP端點引數輸出Blob物件的預設通訊協定已設定為Smart。

     對於具有SOAP端點的每個服務，管理控制檯可讓您為任何傳回的blob指定傳輸通訊協定。 （請參閱[管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)。）

   * AEM Forms服務會以一或多個檔案作為輸入。

1. **服務SOAP端點不是Smart**。 設定的通訊協定會決定檔案傳輸通訊協定，而資料會傳回對應的`BLOB`欄位。 例如，如果SOAP端點設定為DIME，則無論任何輸入檔案的傳輸通訊協定為何，傳回的blob都會在`blob.attachmentID`欄位中。
1. **否則**。 如果服務未將檔案型別當作輸入，則會透過HTTP通訊協定在`BLOB.remoteURL`欄位中傳回輸出檔案。

如第一個條件中所述，您可以藉由擴充尾碼如下的SOAP端點URL，確保任何傳回檔案的傳輸型別：

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

以下是傳輸型別與您從中取得資料的欄位之間的關聯性：

* **Base64格式**：將`blob`尾碼設為`base64`以傳回`BLOB.binaryData`欄位中的資料。
* **MIME或DIME附件**：將`blob`尾碼設為`DIME`或`MIME`，以在`BLOB.attachmentID`欄位中傳回附件識別碼的對應附件型別形式傳回資料。 使用SOAP架構的專屬API從附件讀取資料。
* **遠端URL**：將`blob`尾碼設為`http`以保留應用程式伺服器上的資料，並傳回指向`BLOB.remoteURL`欄位中資料的URL。
* **MTOM或SwaRef**：將`blob`尾碼設為`mtom`或`swaref`，以將資料傳回為對應附件型別，並在`BLOB.MTOM`或`BLOB.swaRef`欄位中傳回附件識別碼。 使用SOAP架構的原生API從附件讀取資料。

>[!NOTE]
>
>透過叫用其`setBinaryData`方法填入`BLOB`物件時，建議您不要超過30 MB。 否則，可能會發生`OutOfMemory`例外狀況。

>[!NOTE]
>
>使用MTOM傳輸通訊協定的JAX WS型應用程式限製為25MB的已傳送及已接收資料。 此限制是由於JAX-WS中的錯誤所導致。 如果傳送和接收的檔案大小總和超過25MB，請使用SwaRef傳輸通訊協定，而不要使用MTOM傳輸通訊協定。 否則，可能會發生`OutOfMemory`例外狀況。

base64編碼位元組陣列的&#x200B;**MTOM傳輸**

除了`BLOB`物件之外，MTOM通訊協定還支援任何複雜型別的位元組陣列引數或位元組陣列欄位。 這表示支援MTOM的使用者端SOAP架構可以傳送任何`xsd:base64Binary`元素做為MTOM附件（而非base64編碼文字）。 AEM Forms SOAP端點可讀取此型別的位元組陣列編碼。 不過，AEM Forms服務一律會傳回位元組陣列型別為base64編碼文字。 輸出位元組陣列引數不支援MTOM。

傳回大量二進位資料的AEM Forms服務會使用Document/BLOB型別，而非位元組陣列型別。 檔案型別在傳輸大量資料時效率更高。

## Web服務資料型別 {#web-service-data-types}

下表列出Java資料型別，並顯示對應的Web服務資料型別。

<table>
 <thead>
  <tr>
   <th><p>Java資料型別</p></th>
   <th><p>Web服務資料型別</p></th>
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
   <td><p><code>DATE</code>型別，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務操作以<code>java.util.Date</code>值作為輸入，SOAP使用者端應用程式必須在<code>DATE.date</code>欄位中傳遞日期。 在此情況下設定<code>DATE.calendar</code>欄位會導致執行階段例外狀況。 如果服務傳回<code>java.util.Date</code>，則會在<code>DATE.date</code>欄位中傳回日期。</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p><code>DATE</code>型別，在服務WSDL中定義如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務操作以<code>java.util.Calendar</code>值作為輸入，SOAP使用者端應用程式必須在<code>DATE.caledendar</code>欄位中傳遞日期。 在此情況下設定<code>DATE.date</code>欄位會導致執行階段例外狀況。 如果服務傳回<code>java.util.Calendar</code>，則會在<code>DATE.calendar</code>欄位中傳回日期。 </p></td>
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
   <td><p><code>apachesoap:Map</code>，在服務WSDL中定義如下：</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>Map是以索引鍵/值配對的序列來表示。</p></td>
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
   <td><p>在服務WSDL中定義的XML型別，如下所示：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務作業接受<code>org.w3c.dom.Document</code>值，請在<code>XML.document</code>欄位中傳遞XML資料。</p><p>設定<code>XML.element</code>欄位會導致執行階段例外狀況。 如果服務傳回<code>org.w3c.dom.Document</code>，則會在<code>XML.document</code>欄位中傳回XML資料。</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>在服務WSDL中定義的XML型別，如下所示：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服務作業以<code>org.w3c.dom.Element</code>作為輸入，請在<code>XML.element</code>欄位中傳遞XML資料。</p><p>設定<code>XML.document</code>欄位會導致執行階段例外狀況。 如果服務傳回<code>org.w3c.dom.Element</code>，則會傳回<code>XML.element</code>欄位中的XML資料。</p></td>
  </tr>
 </tbody>
</table>

## 使用JAX-WS建立Java Proxy類別 {#creating-java-proxy-classes-using-jax-ws}

您可以使用JAX-WS將Forms服務WSDL轉換為Java Proxy類別。 這些類別可讓您叫用AEM Forms服務作業。 Apache Ant可讓您建立建置指令碼，透過參考AEM Forms服務WSDL來產生Java Proxy類別。 您可以執行下列步驟來產生JAX-WS Proxy檔案：

1. 在使用者端電腦上安裝Apache Ant。 (請參閱[https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)。)

   * 將bin目錄新增至類別路徑。
   * 將`ANT_HOME`環境變數設定為您安裝Ant的目錄。

1. 安裝JDK 1.6或更新版本。

   * 將JDK bin目錄新增至類別路徑。
   * 將JRE bin目錄新增至類別路徑。 此bin位於`[JDK_INSTALL_LOCATION]/jre`目錄中。
   * 將`JAVA_HOME`環境變數設定為您安裝JDK的目錄。

   JDK 1.6包含在build.xml檔案中使用的wsimport程式。 JDK 1.5不包含該程式。

1. 在使用者端電腦上安裝JAX-WS。 （請參閱[XML Web服務的Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)。）
1. 使用JAX-WS和Apache Ant來產生Java Proxy類別。 建立Ant建置指令碼以完成此工作。 下列指令碼是名為build.xml的範例Ant建置指令碼：

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

   在此Ant建置指令碼中，請注意`url`屬性設定為參照在localhost上執行的加密服務WSDL。 `username`和`password`屬性必須設定為有效的AEM表單使用者名稱和密碼。 請注意，URL包含`lc_version`屬性。 如果不指定`lc_version`選項，您將無法叫用新的AEM Forms服務作業。

   >[!NOTE]
   >
   >將`EncryptionService`取代為您要使用Java Proxy類別叫用的AEM Forms服務名稱。 例如，若要為Rights Management服務建立Java Proxy類別，請指定：

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. 建立BAT檔案以執行Ant建置指令碼。 下列指令可以位於負責執行Ant建置指令碼的BAT檔案中：

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   將ANT建置指令碼放在C:\Program Files\Java\jaxws-ri\bin目錄中。 指令碼會將JAVA檔案寫入。/classes資料夾。 指令碼會產生可呼叫服務的JAVA檔案。

1. 將JAVA檔案封裝成JAR檔案。 如果您正在使用Eclipse，請遵循下列步驟：

   * 建立用來將Proxy JAVA檔案封裝到JAR檔案中的Java專案。
   * 在專案中建立來源資料夾。
   * 在Source資料夾中建立`com.adobe.idp.services`套件。
   * 選取`com.adobe.idp.services`套件，然後將JAVA檔案從adobe/idp/services資料夾匯入套件中。
   * 如有必要，請在Source資料夾中建立`org/apache/xml/xmlsoap`套件。
   * 選取來源資料夾，然後從org/apache/xml/xmlsoap資料夾匯入JAVA檔案。
   * 將Java編譯器的相容性等級設定為5.0或更高。
   * 建立專案。
   * 將專案匯出為JAR檔案。
   * 在使用者端專案的類別路徑中匯入此JAR檔案。 此外，請匯入&lt;安裝目錄>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty中的所有JAR檔案。

   >[!NOTE]
   >
   >使用AEM表單進行程式設計中的所有Java Web服務快速啟動(Forms服務除外)都會使用JAX-WS建立Java Proxy檔案。 此外，所有Java Web服務都會快速啟動，請使用SwaRef。 (請參閱[使用SwaRef](#invoking-aem-forms-using-swaref)叫用AEM Forms。)

**另請參閱**

[使用Apache Axis建立Java Proxy類別](#creating-java-proxy-classes-using-apache-axis)

[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[透過HTTP使用BLOB資料叫用AEM Forms](#invoking-aem-forms-using-blob-data-over-http)

[使用SwaRef叫用AEM Forms](#invoking-aem-forms-using-swaref)

## 使用Apache Axis建立Java Proxy類別 {#creating-java-proxy-classes-using-apache-axis}

您可以使用Apache Axis WSDL2Java工具將Forms服務轉換為Java Proxy類別。 這些類別可讓您叫用Forms服務作業。 使用Apache Ant，您可以從服務WSDL產生Axis程式庫檔案。 您可以在URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/)下載Apache Axis。

>[!NOTE]
>
>與Forms服務相關聯的Web服務快速啟動，會使用使用Apache Axis建立的Java Proxy類別。 Forms Web服務快速入門也使用Base64作為編碼型別。 (請參閱[Forms服務API快速啟動](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)。)

您可以執行下列步驟來產生Axis Java程式庫檔案：

1. 在使用者端電腦上安裝Apache Ant。 它可在[https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)取得。

   * 將bin目錄新增至類別路徑。
   * 將`ANT_HOME`環境變數設定為您安裝Ant的目錄。

1. 在使用者端電腦上安裝Apache Axis 1.4。 它可在[https://ws.apache.org/axis/](https://ws.apache.org/axis/)取得。
1. 設定類別路徑以使用Web服務使用者端中的Axis JAR檔案，如位於[https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html)的Axis安裝指示中所述。
1. 使用Axis中的Apache WSDL2Java工具來產生Java Proxy類別。 建立Ant建置指令碼以完成此工作。 下列指令碼是名為build.xml的範例Ant建置指令碼：

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

   在此Ant建置指令碼中，請注意`url`屬性設定為參照在localhost上執行的加密服務WSDL。 `username`和`password`屬性必須設定為有效的AEM表單使用者名稱和密碼。

1. 建立BAT檔案以執行Ant建置指令碼。 下列指令可以位於負責執行Ant建置指令碼的BAT檔案中：

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA檔案會寫入`output`屬性所指定的C:\JavaFiles資料夾。 若要成功叫用Forms服務，請將這些JAVA檔案匯入您的類別路徑中。

   依預設，這些檔案屬於名為`com.adobe.idp.services`的Java套件。 建議您將這些JAVA檔案放入JAR檔案中。 然後將JAR檔案匯入使用者端應用程式的類別路徑中。

   >[!NOTE]
   >
   >有不同的方式可以將.JAVA檔案放入JAR中。 一種方法是使用Java IDE，例如Eclipse。 建立Java專案並建立`com.adobe.idp.services`封裝（所有.JAVA檔案都屬於此封裝）。 接著，將所有.JAVA檔案匯入套件中。 最後，將專案匯出為JAR檔案。

1. 修改`EncryptionServiceLocator`類別中的URL以指定編碼型別。 例如，若要使用base64，請指定`?blob=base64`以確保`BLOB`物件傳回二進位資料。 也就是說，在`EncryptionServiceLocator`類別中，找出下列程式碼行：

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   並將其變更為：

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

[使用JAX-WS建立Java Proxy類別](#creating-java-proxy-classes-using-jax-ws)

[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[透過HTTP使用BLOB資料叫用AEM Forms](#invoking-aem-forms-using-blob-data-over-http)

## 使用Base64編碼叫用AEM Forms {#invoking-aem-forms-using-base64-encoding}

您可以使用Base64編碼來叫用AEM Forms服務。 Base64編碼會對隨Web服務呼叫要求傳送的附件進行編碼。 也就是說，`BLOB`資料是以Base64編碼，而非整個SOAP訊息。

「使用Base64編碼叫用AEM Forms」會討論使用Base64編碼叫用下列名為`MyApplication/EncryptDocument`的AEM Forms短期處理序。

>[!NOTE]
>
>此程式並非以現有AEM Forms程式為基礎。 若要跟隨程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

叫用此程式時，會執行下列動作：

1. 取得傳遞至程式的不安全PDF檔案。 此動作是以`SetValue`作業為基礎。 此處理序的輸入引數是名為`inDoc`的`document`處理序變數。
1. 使用密碼加密PDF檔案。 此動作是以`PasswordEncryptPDF`作業為基礎。 密碼加密的PDF檔案傳回名為`outDoc`的程式變數。

### 建立使用Base64編碼的.NET使用者端元件 {#creating-a-net-client-assembly-that-uses-base64-encoding}

您可以建立.NET使用者端元件，以從Microsoft Visual Studio .NET專案叫用Forms服務。 若要建立使用base64編碼的.NET使用者端元件，請執行下列步驟：

1. 根據AEM Forms叫用URL建立Proxy類別。
1. 建立產生.NET使用者端元件的Microsoft Visual Studio .NET專案。

**正在建立Proxy類別**

您可以使用Microsoft Visual Studio隨附的工具，建立用來建立.NET使用者端元件的Proxy類別。 工具名稱為wsdl.exe，位於Microsoft Visual Studio安裝資料夾中。 若要建立Proxy類別，請開啟命令提示字元並瀏覽至包含wsdl.exe檔案的資料夾。 如需wsdl.exe工具的詳細資訊，請參閱&#x200B;*MSDN說明*。

在命令提示字元輸入以下命令：

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

依預設，此工具會在相同資料夾中建立以WSDL名稱為基礎的CS檔案。 在這種情況下，它會建立名為&#x200B;*EncryptDocumentService.cs*&#x200B;的CS檔案。 您可以使用此CS檔案來建立Proxy物件，讓您可以叫用叫用URL中指定的服務。

修改Proxy類別中的URL以包含`?blob=base64`，以確保`BLOB`物件傳回二進位資料。 在proxy類別中，找出下列程式碼行：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

並將其變更為：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

使用Base64編碼的&#x200B;*叫用AEM Forms*&#x200B;區段使用`MyApplication/EncryptDocument`作為範例。 如果您正在為其他Forms服務建立.NET使用者端元件，請確定您以服務名稱取代`MyApplication/EncryptDocument`。

**正在開發.NET使用者端元件**

建立產生.NET使用者端元件的Visual Studio類別庫專案。 您使用wsdl.exe建立的CS檔案可以匯入此專案。 此專案會產生DLL檔案（.NET使用者端元件），您可以在其他Visual Studio .NET專案中使用此檔案來呼叫服務。

1. 啟動Microsoft Visual Studio .NET。
1. 建立類別庫專案並將其命名為DocumentService。
1. 匯入您使用wsdl.exe建立的CS檔案。
1. 在&#x200B;**專案**&#x200B;功能表中，選取&#x200B;**新增參考**。
1. 在[新增參考]對話方塊中，選取&#x200B;**System.Web.Services.dll**。
1. 按一下&#x200B;**選取**，然後按一下&#x200B;**確定**。
1. 編譯及建置專案。

>[!NOTE]
>
>此程式會建立名為DocumentService.dll的.NET使用者端元件，可用來將SOAP要求傳送至`MyApplication/EncryptDocument`服務。

>[!NOTE]
>
>請確定您已將`?blob=base64`新增至用來建立.NET使用者端元件之Proxy類別中的URL。 否則，您無法從`BLOB`物件擷取二進位資料。

**正在參考.NET使用者端元件**

將您新建立的.NET使用者端元件放在您正在開發使用者端應用程式的電腦上。 將.NET使用者端元件放在目錄中之後，可以從專案中參照它。 同時參考專案中的`System.Web.Services`資料庫。 如果不參考此程式庫，就無法使用.NET使用者端元件來叫用服務。

1. 在&#x200B;**專案**&#x200B;功能表中，選取&#x200B;**新增參考**。
1. 按一下&#x200B;**.NET**&#x200B;標籤。
1. 按一下&#x200B;**瀏覽**&#x200B;並找到DocumentService.dll檔案。
1. 按一下&#x200B;**選取**，然後按一下&#x200B;**確定**。

**使用使用Base64編碼的.NET使用者端元件叫用服務**

您可以使用使用Base64編碼的.NET使用者端元件來叫用`MyApplication/EncryptDocument`服務（內建於Workbench）。 若要叫用`MyApplication/EncryptDocument`服務，請執行下列步驟：

1. 建立使用`MyApplication/EncryptDocument`服務WSDL的Microsoft .NET使用者端元件。
1. 建立使用者端Microsoft .NET專案。 參照使用者端專案中的Microsoft .NET使用者端元件。 也參考`System.Web.Services`。
1. 使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`MyApplication_EncryptDocumentService`物件。
1. 使用`System.Net.NetworkCredential`物件設定`MyApplication_EncryptDocumentService`物件的`Credentials`屬性。 在`System.Net.NetworkCredential`建構函式中，指定AEM表單使用者名稱和對應的密碼。 設定驗證值，讓您的.NET使用者端應用程式能夠成功與AEM Forms交換SOAP訊息。
1. 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存PDF檔案傳遞至`MyApplication/EncryptDocument`處理序。
1. 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表PDF檔案檔案位置和開啟檔案模式的字串值。
1. 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
1. 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
1. 以位元組陣列的內容指派物件的`binaryData`屬性，填入`BLOB`物件。
1. 叫用`MyApplication/EncryptDocument`處理序，方法是叫用`MyApplication_EncryptDocumentService`物件的`invoke`方法，並傳遞包含PDF檔案的`BLOB`物件。 此程式會傳回`BLOB`物件中的加密PDF檔案。
1. 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表密碼加密檔案檔案位置的字串值。
1. 建立位元組陣列，儲存`MyApplicationEncryptDocumentService`物件的`invoke`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`binaryData`資料成員的值，以填入位元組陣列。
1. 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
1. 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列內容寫入PDF檔案。

### 使用Java Proxy類別和Base64編碼叫用服務 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

您可以使用Java Proxy類別和Base64來叫用AEM Forms服務。 若要使用Java Proxy類別叫用`MyApplication/EncryptDocument`服務，請執行下列步驟：

1. 使用使用`MyApplication/EncryptDocument`服務WSDL的JAX-WS建立Java Proxy類別。 使用下列WSDL端點：

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >將`hiro-xp` *取代為主控AEM Forms的J2EE應用程式伺服器的IP位址。*

1. 將使用JAX-WS建立的Java Proxy類別封裝到JAR檔案中。
1. 請將Java Proxy JAR檔案和JAR檔案加入以下路徑中：

   &lt;安裝目錄>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到您的Java使用者端專案的類別路徑中。

1. 使用物件的建構函式建立`MyApplicationEncryptDocumentService`物件。
1. 呼叫`MyApplicationEncryptDocumentService`物件的`getEncryptDocument`方法，以建立`MyApplicationEncryptDocument`物件。
1. 將值指派給下列資料成員，以設定呼叫AEM Forms所需的連線值：

   * 將WSDL端點與編碼型別指派給`javax.xml.ws.BindingProvider`物件的`ENDPOINT_ADDRESS_PROPERTY`欄位。 若要使用Base64編碼叫用`MyApplication/EncryptDocument`服務，請指定下列URL值：

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * 將AEM表單使用者指派給`javax.xml.ws.BindingProvider`物件的`USERNAME_PROPERTY`欄位。
   * 將對應的密碼值指派給`javax.xml.ws.BindingProvider`物件的`PASSWORD_PROPERTY`欄位。

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

1. 使用建構函式建立`java.io.FileInputStream`物件，以擷取要傳送至`MyApplication/EncryptDocument`處理序的PDF檔案。 傳遞字串值，指定PDF檔案的位置。
1. 建立位元組陣列，並以`java.io.FileInputStream`物件的內容填入該陣列。
1. 使用物件的建構函式建立`BLOB`物件。
1. 叫用物件的`setBinaryData`方法並傳遞位元組陣列以填入`BLOB`物件。 `BLOB`物件的`setBinaryData`是使用Base64編碼時要呼叫的方法。 請參閱在服務要求中提供BLOB物件。
1. 叫用`MyApplicationEncryptDocument`物件的`invoke`方法，以叫用`MyApplication/EncryptDocument`處理序。 傳遞包含PDF檔案的`BLOB`物件。 叫用方法傳回包含加密PDF檔案的`BLOB`物件。
1. 呼叫`BLOB`物件的`getBinaryData`方法，建立包含加密PDF檔案的位元組陣列。
1. 將加密的PDF檔案儲存為PDF檔案。 將位元組陣列寫入檔案。

**另請參閱**

[快速入門：使用Java Proxy檔案和Base64編碼叫用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](#creating-a-net-client-assembly-that-uses-base64-encoding)

## 使用MTOM叫用AEM Forms {#invoking-aem-forms-using-mtom}

您可以使用Web服務標準MTOM來叫用AEM Forms服務。 此標準定義如何透過網際網路或內部網路傳輸二進位資料(例如PDF檔案)。 MTOM的一個功能是使用`XOP:Include`元素。 此元素在XML二進位最佳化封裝(XOP)規格中定義，以參照SOAP訊息的二進位附件。

此處的討論內容是關於使用MTOM來叫用下列名為`MyApplication/EncryptDocument`的AEM Forms短期處理序。

>[!NOTE]
>
>此程式並非以現有AEM Forms程式為基礎。 若要跟隨程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

叫用此程式時，會執行下列動作：

1. 取得傳遞至程式的不安全PDF檔案。 此動作是以`SetValue`作業為基礎。 此處理序的輸入引數是名為`inDoc`的`document`處理序變數。
1. 使用密碼加密PDF檔案。 此動作是以`PasswordEncryptPDF`作業為基礎。 密碼加密的PDF檔案傳回名為`outDoc`的程式變數。

>[!NOTE]
>
>AEM Forms版本9已新增MTOM支援。

>[!NOTE]
>
>使用MTOM傳輸通訊協定的JAX WS型應用程式限製為25MB的已傳送及已接收資料。 此限制是由於JAX-WS中的錯誤所導致。 如果傳送和接收的檔案大小總和超過25MB，請使用SwaRef傳輸通訊協定，而不要使用MTOM傳輸通訊協定。 否則，可能會發生`OutOfMemory`例外狀況。

此處的討論內容是關於在Microsoft .NET專案中使用MTOM來叫用AEM Forms服務。 使用的.NET Framework是3.5，而開發環境是Visual Studio 2008。 如果您的開發電腦上已安裝Web服務增強功能(WSE)，請將其移除。 .NET 3.5架構支援名為Windows Communication Foundation (WCF)的SOAP架構。 使用MTOM叫用AEM Forms時，僅支援WCF （不支援WSE）。

### 建立使用MTOM叫用服務的.NET專案 {#creating-a-net-project-that-invokes-a-service-using-mtom}

您可以建立Microsoft .NET專案，以使用Web服務叫用AEM Forms服務。 首先，使用Visual Studio 2008建立Microsoft .NET專案。 若要叫用AEM Forms服務，請建立您要在專案中叫用AEM Forms服務的服務參考。 建立服務參考時，請指定AEM Forms服務的URL：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

將`localhost`取代為裝載AEM Forms之J2EE應用程式伺服器的IP位址。 將`MyApplication/EncryptDocument`取代為要叫用的AEM Forms服務名稱。 例如，若要叫用Rights Management作業，請指定：

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

`lc_version`選項可確保AEM Forms功能（例如MTOM）可供使用。 若未指定`lc_version`選項，您就無法使用MTOM叫用AEM Forms。

建立「服務參考」後，與AEM Forms服務相關的資料型別便可在.NET專案中使用。 若要建立叫用AEM Forms服務的.NET專案，請執行下列步驟：

1. 使用Microsoft Visual Studio 2008建立.NET專案。
1. 在&#x200B;**專案**&#x200B;功能表中，選取&#x200B;**新增服務參考**。
1. 在&#x200B;**位址**&#x200B;對話方塊中，指定AEM Forms服務的WSDL。 例如，

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. 按一下&#x200B;**執行**，然後按一下&#x200B;**確定**。

### 在.NET專案中使用MTOM叫用服務 {#invoking-a-service-using-mtom-in-a-net-project}

請考慮接受不安全PDF檔案並傳回密碼加密PDF檔案的`MyApplication/EncryptDocument`程式。 若要使用MTOM叫用`MyApplication/EncryptDocument`處理序（內建於Workbench），請執行下列步驟：

1. 建立Microsoft .NET專案。
1. 使用預設建構函式建立`MyApplication_EncryptDocumentClient`物件。
1. 使用`System.ServiceModel.EndpointAddress`建構函式建立`MyApplication_EncryptDocumentClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務與編碼型別：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   您不需要使用`lc_version`屬性。 當您建立服務參考時，會使用此屬性。 不過，請確定您指定了`?blob=mtom`。

   >[!NOTE]
   >
   >將`hiro-xp` *取代為主控AEM Forms的J2EE應用程式伺服器的IP位址。*

1. 取得`EncryptDocumentClient.Endpoint.Binding`資料成員的值，以建立`System.ServiceModel.BasicHttpBinding`物件。 將傳回值轉換為`BasicHttpBinding`。
1. 將`System.ServiceModel.BasicHttpBinding`物件的`MessageEncoding`資料成員設定為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
1. 執行下列工作來啟用基本的HTTP驗證：

   * 將AEM表單使用者名稱指派給資料成員`MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`。
   * 將對應的密碼值指派給資料成員`MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`。
   * 將常數值`HttpClientCredentialType.Basic`指派給資料成員`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`指派給資料成員`BasicHttpBindingSecurity.Security.Mode`。

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

1. 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來儲存PDF檔案，以傳遞至`MyApplication/EncryptDocument`處理序。
1. 透過叫用它的建構函式來建立`System.IO.FileStream`物件。 傳遞代表PDF檔案檔案位置和開啟檔案模式的字串值。
1. 建立位元組陣列以儲存`System.IO.FileStream`物件的內容。 您可以取得`System.IO.FileStream`物件的`Length`屬性來決定位元組陣列的大小。
1. 呼叫`System.IO.FileStream`物件的`Read`方法，以串流資料填入位元組陣列。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
1. 以位元組陣列的內容指派物件的`MTOM`資料成員，以填入`BLOB`物件。
1. 叫用`MyApplication_EncryptDocumentClient`物件的`invoke`方法，以叫用`MyApplication/EncryptDocument`處理序。 傳遞包含PDF檔案的`BLOB`物件。 此程式會傳回`BLOB`物件中的加密PDF檔案。
1. 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表受保護PDF檔案檔案位置的字串值。
1. 建立位元組陣列，儲存`invoke`方法傳回的`BLOB`物件的資料內容。 取得`BLOB`物件的`MTOM`資料成員的值，以填入位元組陣列。
1. 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
1. 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

>[!NOTE]
>
>大部分的AEM Forms服務操作都有MTOM快速入門。 您可以在服務的對應快速入門區段中檢視這些快速啟動。 例如，若要檢視輸出快速入門區段，請參閱[輸出服務API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**另請參閱**

[快速入門：在.NET專案中使用MTOM叫用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[使用網站服務存取多項服務](#accessing-multiple-services-using-web-services)

[建立ASP.NET網頁應用程式，叫用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## 使用SwaRef叫用AEM Forms {#invoking-aem-forms-using-swaref}

您可以使用SwaRef叫用AEM Forms服務。 `wsi:swaRef` XML元素的內容會以附件形式傳送到SOAP內文，以儲存附件的參考。 使用SwaRef叫用Forms服務時，請使用適用於XML Web服務的Java API (JAX-WS)建立Java Proxy類別。 （請參閱[XML Web服務的Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)。）

此處的討論內容關於使用SwaRef叫用下列名為`MyApplication/EncryptDocument`的Forms短期處理序。

>[!NOTE]
>
>此程式並非以現有AEM Forms程式為基礎。 若要跟隨程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

叫用此程式時，會執行下列動作：

1. 取得傳遞至程式的不安全PDF檔案。 此動作是以`SetValue`作業為基礎。 此處理序的輸入引數是名為`inDoc`的`document`處理序變數。
1. 使用密碼加密PDF檔案。 此動作是以`PasswordEncryptPDF`作業為基礎。 密碼加密的PDF檔案傳回名為`outDoc`的程式變數。

>[!NOTE]
>
>AEM Forms新增SwaRef支援

以下討論是關於如何在Java使用者端應用程式中使用SwaRef來叫用Forms服務。 Java應用程式使用使用JAX-WS建立的Proxy類別。

### 使用使用SwaRef的JAX-WS程式庫檔案叫用服務 {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

若要使用以JAX-WS和SwaRef建立的Java Proxy檔案來叫用`MyApplication/EncryptDocument`處理序，請執行下列步驟：

1. 使用使用`MyApplication/EncryptDocument`服務WSDL的JAX-WS建立Java Proxy類別。 使用下列WSDL端點：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   如需詳細資訊，請參閱[使用JAX-WS建立Java Proxy類別](#creating-java-proxy-classes-using-jax-ws)。

   >[!NOTE]
   >
   >將`hiro-xp` *取代為裝載AEM Forms的J2EE應用程式伺服器的IP位址。*

1. 將使用JAX-WS建立的Java Proxy類別封裝到JAR檔案中。
1. 請將Java Proxy JAR檔案和JAR檔案加入以下路徑中：

   &lt;安裝目錄>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到您的Java使用者端專案的類別路徑中。

1. 使用物件的建構函式建立`MyApplicationEncryptDocumentService`物件。
1. 呼叫`MyApplicationEncryptDocumentService`物件的`getEncryptDocument`方法，以建立`MyApplicationEncryptDocument`物件。
1. 將值指派給下列資料成員，以設定呼叫AEM Forms所需的連線值：

   * 將WSDL端點與編碼型別指派給`javax.xml.ws.BindingProvider`物件的`ENDPOINT_ADDRESS_PROPERTY`欄位。 若要使用SwaRef編碼叫用`MyApplication/EncryptDocument`服務，請指定下列URL值：

     ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * 將AEM表單使用者指派給`javax.xml.ws.BindingProvider`物件的`USERNAME_PROPERTY`欄位。
   * 將對應的密碼值指派給`javax.xml.ws.BindingProvider`物件的`PASSWORD_PROPERTY`欄位。

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

1. 使用建構函式建立`java.io.File`物件，以擷取要傳送至`MyApplication/EncryptDocument`處理序的PDF檔案。 傳遞字串值，指定PDF檔案的位置。
1. 使用`FileDataSource`建構函式建立`javax.activation.DataSource`物件。 傳遞`java.io.File`物件。
1. 使用它的建構函式並傳遞`javax.activation.DataSource`物件來建立`javax.activation.DataHandler`物件。
1. 使用物件的建構函式建立`BLOB`物件。
1. 叫用物件的`setSwaRef`方法並傳遞`javax.activation.DataHandler`物件以填入`BLOB`物件。
1. 叫用`MyApplication/EncryptDocument`處理序，方法是叫用`MyApplicationEncryptDocument`物件的`invoke`方法，並傳遞包含PDF檔案的`BLOB`物件。 叫用方法傳回包含加密PDF檔案的`BLOB`物件。
1. 叫用`BLOB`物件的`getSwaRef`方法填入`javax.activation.DataHandler`物件。
1. 呼叫`javax.activation.DataHandler`物件的`getInputStream`方法，將`javax.activation.DataHandler`物件轉換為`java.io.InputSteam`執行個體。
1. 將`java.io.InputSteam`執行個體寫入代表加密PDF檔案的PDF檔案。

>[!NOTE]
>
>大部分的AEM Forms服務操作都有SwaRef快速入門。 您可以在服務的對應快速入門區段中檢視這些快速啟動。 例如，若要檢視輸出快速入門區段，請參閱[輸出服務API快速入門](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**另請參閱**

[快速入門：在Java專案中使用SwaRef叫用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## 透過HTTP使用BLOB資料叫用AEM Forms {#invoking-aem-forms-using-blob-data-over-http}

您可以使用網站服務並透過HTTP傳遞BLOB資料，以叫用AEM Forms服務。 透過HTTP傳遞BLOB資料是替代技術，可取代使用base64編碼、DIME或MIME。 例如，您可以在使用Web服務增強功能3.0 （不支援DIME或MIME）的Microsoft .NET專案中，透過HTTP傳送資料。 透過HTTP使用BLOB資料時，在叫用AEM Forms服務之前會先上傳輸入資料。

「透過HTTP使用BLOB資料叫用AEM Forms」會討論透過HTTP傳遞BLOB資料以叫用下列名為`MyApplication/EncryptDocument`的AEM Forms短期程式。

>[!NOTE]
>
>此程式並非以現有AEM Forms程式為基礎。 若要跟隨程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

叫用此程式時，會執行下列動作：

1. 取得傳遞至程式的不安全PDF檔案。 此動作是以`SetValue`作業為基礎。 此處理序的輸入引數是名為`inDoc`的`document`處理序變數。
1. 使用密碼加密PDF檔案。 此動作是以`PasswordEncryptPDF`作業為基礎。 密碼加密的PDF檔案傳回名為`outDoc`的程式變數。

>[!NOTE]
>
>建議您先熟悉如何使用SOAP叫用AEM Forms 。 (請參閱[使用Web服務叫用AEM Forms](#invoking-aem-forms-using-web-services)。)

### 建立透過HTTP使用資料的.NET使用者端元件 {#creating-a-net-client-assembly-that-uses-data-over-http}

若要建立透過HTTP使用資料的使用者端元件，請遵循[使用Base64編碼叫用AEM Forms](#invoking-aem-forms-using-base64-encoding)中指定的程式。 不過，請修改Proxy類別中的URL以包含`?blob=http`而非`?blob=base64`。 此動作可確保資料透過HTTP傳遞。 在proxy類別中，找出下列程式碼行：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

並將其變更為：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**正在參考.NET clienMyApplication/EncryptDocument元件**

將新的.NET使用者端元件放在您正在開發使用者端應用程式的電腦上。 將.NET使用者端元件放在目錄中之後，可以從專案中參照它。 從您的專案參考`System.Web.Services`資料庫。 如果不參考此程式庫，就無法使用.NET使用者端元件來叫用服務。

1. 在&#x200B;**專案**&#x200B;功能表中，選取&#x200B;**新增參考**。
1. 按一下&#x200B;**.NET**&#x200B;標籤。
1. 按一下&#x200B;**瀏覽**&#x200B;並找到DocumentService.dll檔案。
1. 按一下&#x200B;**選取**，然後按一下&#x200B;**確定**。

**使用透過HTTP使用BLOB資料的.NET使用者端元件叫用服務**

您可以使用透過HTTP使用資料的.NET使用者端元件，叫用`MyApplication/EncryptDocument`服務（內建於Workbench）。 若要叫用`MyApplication/EncryptDocument`服務，請執行下列步驟：

1. 建立.NET使用者端元件。
1. 參考Microsoft .NET使用者端元件。 建立使用者端Microsoft .NET專案。 參照使用者端專案中的Microsoft .NET使用者端元件。 也參考`System.Web.Services`。
1. 使用Microsoft .NET使用者端元件，透過叫用其預設建構函式來建立`MyApplication_EncryptDocumentService`物件。
1. 使用`System.Net.NetworkCredential`物件設定`MyApplication_EncryptDocumentService`物件的`Credentials`屬性。 在`System.Net.NetworkCredential`建構函式中，指定AEM表單使用者名稱和對應的密碼。 設定驗證值，讓您的.NET使用者端應用程式能夠成功與AEM Forms交換SOAP訊息。
1. 使用物件的建構函式建立`BLOB`物件。 `BLOB`物件是用來傳遞資料給`MyApplication/EncryptDocument`處理序。
1. 將字串值指派給`BLOB`物件的`remoteURL`資料成員，該資料成員指定要傳遞至`MyApplication/EncryptDocument`服務的PDF檔案的URI位置。
1. 叫用`MyApplication_EncryptDocumentService`物件的`invoke`方法並傳遞`BLOB`物件以叫用`MyApplication/EncryptDocument`處理序。 此程式會傳回`BLOB`物件中的加密PDF檔案。
1. 使用物件的建構函式，並傳遞傳回`BLOB`物件的`remoteURL`資料成員的值，以建立`System.UriBuilder`物件。
1. 將`System.UriBuilder`物件轉換為`System.IO.Stream`物件。 （此清單後面的C#快速入門說明如何執行此工作。）
1. 建立位元組陣列，並在`System.IO.Stream`物件中填入資料。
1. 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
1. 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列內容寫入PDF檔案。

### 透過HTTP使用Java Proxy類別和BLOB資料叫用服務 {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

您可以透過HTTP使用Java Proxy類別和BLOB資料來叫用AEM Forms服務。 若要使用Java Proxy類別叫用`MyApplication/EncryptDocument`服務，請執行下列步驟：

1. 使用使用`MyApplication/EncryptDocument`服務WSDL的JAX-WS建立Java Proxy類別。 使用下列WSDL端點：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   如需詳細資訊，請參閱[使用JAX-WS建立Java Proxy類別](#creating-java-proxy-classes-using-jax-ws)。

   >[!NOTE]
   >
   >將`hiro-xp` *取代為裝載AEM Forms的J2EE應用程式伺服器的IP位址。*

1. 將使用JAX-WS建立的Java Proxy類別封裝到JAR檔案中。
1. 請將Java Proxy JAR檔案和JAR檔案加入以下路徑中：

   &lt;安裝目錄>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到您的Java使用者端專案的類別路徑中。

1. 使用物件的建構函式建立`MyApplicationEncryptDocumentService`物件。
1. 呼叫`MyApplicationEncryptDocumentService`物件的`getEncryptDocument`方法，以建立`MyApplicationEncryptDocument`物件。
1. 將值指派給下列資料成員，以設定呼叫AEM Forms所需的連線值：

   * 將WSDL端點與編碼型別指派給`javax.xml.ws.BindingProvider`物件的`ENDPOINT_ADDRESS_PROPERTY`欄位。 若要使用BLOB over HTTP編碼來叫用`MyApplication/EncryptDocument`服務，請指定下列URL值：

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * 將AEM表單使用者指派給`javax.xml.ws.BindingProvider`物件的`USERNAME_PROPERTY`欄位。
   * 將對應的密碼值指派給`javax.xml.ws.BindingProvider`物件的`PASSWORD_PROPERTY`欄位。

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

1. 使用物件的建構函式建立`BLOB`物件。
1. 叫用物件的`setRemoteURL`方法來填入`BLOB`物件。 傳遞字串值，該值指定要傳遞至`MyApplication/EncryptDocument`服務的PDF檔案的URI位置。
1. 叫用`MyApplication/EncryptDocument`處理序，方法是叫用`MyApplicationEncryptDocument`物件的`invoke`方法，並傳遞包含PDF檔案的`BLOB`物件。 此程式會傳回`BLOB`物件中的加密PDF檔案。
1. 建立位元組陣列以儲存代表加密PDF檔案的資料流。 叫用`BLOB`物件的`getRemoteURL`方法（使用`invoke`方法傳回的`BLOB`物件）。
1. 使用物件的建構函式建立`java.io.File`物件。 此物件代表加密的PDF檔案。
1. 使用它的建構函式並傳遞`java.io.File`物件來建立`java.io.FileOutputStream`物件。
1. 叫用`java.io.FileOutputStream`物件的`write`方法。 傳遞包含代表加密PDF檔案之資料流的位元組陣列。

## 使用DIME叫用AEM Forms {#invoking-aem-forms-using-dime}

您可以使用含有附件的SOAP叫用AEM Forms服務。 AEM Forms支援MIME和DIME Web服務標準。 DIME可讓您傳送二進位附件(例如PDF檔案)以及叫用請求，而非編碼附件。 *使用DIME叫用AEM Forms*&#x200B;區段會討論使用DIME叫用下列名為`MyApplication/EncryptDocument`的AEM Forms短期處理序。

叫用此程式時，會執行下列動作：

1. 取得傳遞至程式的不安全PDF檔案。 此動作是以`SetValue`作業為基礎。 此處理序的輸入引數是名為`inDoc`的`document`處理序變數。
1. 使用密碼加密PDF檔案。 此動作是以`PasswordEncryptPDF`作業為基礎。 密碼加密的PDF檔案傳回名為`outDoc`的程式變數。

此程式並非以現有AEM Forms程式為基礎。 若要跟隨程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

>[!NOTE]
>
>不建議使用DIME叫用AEM Forms服務作業。 建議您使用MTOM。 (請參閱[使用MTOM](#invoking-aem-forms-using-mtom)叫用AEM Forms。)

### 建立使用DIME的.NET專案 {#creating-a-net-project-that-uses-dime}

若要建立可使用DIME呼叫Forms服務的.NET專案，請執行下列工作：

* 在開發電腦上安裝Web服務增強功能2.0。
* 在您的.NET專案中，建立FormsAEM Forms服務的Web參考。

**安裝Web服務增強功能2.0**

在開發電腦上安裝Web Services Enhancements 2.0，並將其與Microsoft Visual Studio .NET整合。 您可以從[Microsoft下載中心下載Web服務增強功能2.0。](https://www.microsoft.com/downloads/search.aspx)

從這個網頁搜尋Web Services Enhancements 2.0，並將其下載到您的開發電腦上。 此下載檔案會將名為Microsoft WSE 2.0 SPI.msi的檔案放在電腦上。 執行安裝程式，並遵循線上指示。

>[!NOTE]
>
>Web服務增強功能2.0支援DIME。 使用Web服務增強功能2.0時，支援的Microsoft Visual Studio版本是2003。Web服務增強功能3.0不支援DIME，但支援MTOM。

**建立AEM Forms服務的Web參考**

在開發電腦上安裝Web Services Enhancements 2.0並建立Microsoft .NET專案後，請建立Forms服務的Web參考。 例如，若要建立`MyApplication/EncryptDocument`處理序的Web參考，並假設Forms已安裝在本機電腦上，請指定下列URL：

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

建立Web參考後，下列兩種代理主機資料型別可供您在.NET專案中使用： `EncryptDocumentService`和`EncryptDocumentServiceWse`。 若要使用DIME叫用`MyApplication/EncryptDocument`處理序，請使用`EncryptDocumentServiceWse`型別。

>[!NOTE]
>
>在建立Forms服務的Web參考之前，請確定您在專案中參考了Web服務增強功能2.0。 （請參閱「安裝Web服務增強功能2.0」。）

**參考WSE資料庫**

1. 在「專案」選單中，選取「新增參照」。
1. 在「新增參照」對話方塊中，選取Microsoft.Web.Services2.dll。
1. 選取System.Web.Services.dll。
1. 按一下「選取」，然後按一下「確定」。

**建立Forms服務的Web參考**

1. 在「專案」功能表中，選取「新增Web參考」。
1. 在URL對話方塊中，指定Forms服務的URL。
1. 按一下執行，然後按一下新增參照。

>[!NOTE]
>
>請確定您已啟用.NET專案以使用WSE資料庫。 在「專案總管」中，以滑鼠右鍵按一下專案名稱並選取「啟用WSE 2.0」。確定已選取出現的對話方塊上的核取方塊。

**在.NET專案中使用DIME叫用服務**

您可以使用DIME叫用Forms服務。 請考慮接受不安全PDF檔案並傳回密碼加密PDF檔案的`MyApplication/EncryptDocument`程式。 若要使用DIME叫用`MyApplication/EncryptDocument`處理序，請執行下列步驟：

1. 建立Microsoft .NET專案，讓您使用DIME叫用Forms服務。 請確定您包含網站服務增強功能2.0，並建立AEM Forms服務的網站參考。
1. 在設定`MyApplication/EncryptDocument`處理序的Web參照之後，使用預設建構函式來建立`EncryptDocumentServiceWse`物件。
1. 將`EncryptDocumentServiceWse`物件的`Credentials`資料成員設定為指定AEM表單使用者名稱和密碼值的`System.Net.NetworkCredential`值。
1. 使用物件的建構函式並傳遞下列值來建立`Microsoft.Web.Services2.Dime.DimeAttachment`物件：

   * 字串值，指定GUID值。 您可以叫用`System.Guid.NewGuid.ToString`方法來取得GUID值。
   * 字串值，指定內容型別。 因為此程式需要PDF檔案，請指定`application/pdf`。
   * `TypeFormat`列舉值。 指定`TypeFormat.MediaType`。
   * 字串值，指定要傳遞至AEM Forms程式的PDF檔案位置。

1. 使用物件的建構函式建立`BLOB`物件。
1. 將`Microsoft.Web.Services2.Dime.DimeAttachment`物件的`Id`資料成員值指派至`BLOB`物件的`attachmentID`資料成員，以將DIME附件新增至`BLOB`物件。
1. 叫用`EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add`方法並傳遞`Microsoft.Web.Services2.Dime.DimeAttachment`物件。
1. 叫用`MyApplication/EncryptDocument`處理序，方法是叫用`EncryptDocumentServiceWse`物件的`invoke`方法，並傳遞包含DIME附件的`BLOB`物件。 此程式會傳回`BLOB`物件中的加密PDF檔案。
1. 取得傳回`BLOB`物件之`attachmentID`資料成員的值，以取得附件識別碼值。
1. 在`EncryptDocumentServiceWse.ResponseSoapContext.Attachments`中反複檢查附件，並使用附件識別碼值來取得加密的PDF檔案。
1. 取得`Attachment`物件之`Stream`資料成員的值，以取得`System.IO.Stream`物件。
1. 建立位元組陣列，並將該位元組陣列傳遞至`System.IO.Stream`物件的`Read`方法。 此方法會以代表加密PDF檔案的資料流填入位元組陣列。
1. 建立`System.IO.FileStream`物件，方法為叫用其建構函式，並傳遞代表PDF檔案位置的字串值。 此物件代表加密的PDF檔案。
1. 透過叫用它的建構函式並傳遞`System.IO.FileStream`物件來建立`System.IO.BinaryWriter`物件。
1. 呼叫`System.IO.BinaryWriter`物件的`Write`方法並傳遞位元組陣列，將位元組陣列的內容寫入PDF檔案。

### 建立使用DIME的Apache Axis Java Proxy類別 {#creating-apache-axis-java-proxy-classes-that-use-dime}

您可以使用Apache Axis WSDL2Java工具將服務WSDL轉換為Java Proxy類別，以便呼叫服務作業。 使用Apache Ant，您可以從AEM Forms服務WSDL產生Axis程式庫檔案，讓您叫用該服務。 （請參閱[使用Apache Axis](#creating-java-proxy-classes-using-apache-axis)建立Java Proxy類別。）

Apache Axis WSDL2Java工具會產生JAVA檔案，其中包含用來將SOAP要求傳送至服務的方法。 服務收到的SOAP要求會由Axis產生的程式庫解碼，並傳回方法和引數。

若要使用Axis產生的程式庫檔案和DIME來叫用`MyApplication/EncryptDocument`服務（內建於Workbench），請執行下列步驟：

1. 使用Apache Axis建立使用`MyApplication/EncryptDocument`服務WSDL的Java Proxy類別。 （請參閱[使用Apache Axis](#creating-java-proxy-classes-using-apache-axis)建立Java Proxy類別。）
1. 將Java Proxy類別納入您的類別路徑中。
1. 使用物件的建構函式建立`MyApplicationEncryptDocumentServiceLocator`物件。
1. 使用它的建構函式並傳遞指定AEM Forms服務WSDL定義的字串值，來建立`URL`物件。 請確定您在SOAP端點URL的結尾指定`?blob=dime`。 例如，使用

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. 建立`EncryptDocumentSoapBindingStub`物件，方法是叫用其建構函式，並傳遞`MyApplicationEncryptDocumentServiceLocator`物件和`URL`物件。
1. 透過叫用`EncryptDocumentSoapBindingStub`物件的`setUsername`和`setPassword`方法來設定AEM表單使用者名稱和密碼值。

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. 透過建立`java.io.File`物件來擷取要傳送至`MyApplication/EncryptDocument`服務的PDF檔案。 傳遞指定PDF檔案位置的字串值。
1. 使用它的建構函式並傳遞`javax.activation.FileDataSource`物件來建立`javax.activation.DataHandler`物件。 `javax.activation.FileDataSource`物件可以使用其建構函式並傳遞代表PDF檔案的`java.io.File`物件來建立。
1. 使用它的建構函式並傳遞`javax.activation.DataHandler`物件來建立`org.apache.axis.attachments.AttachmentPart`物件。
1. 透過叫用`EncryptDocumentSoapBindingStub`物件的`addAttachment`方法並傳遞`org.apache.axis.attachments.AttachmentPart`物件來附加附件。
1. 使用物件的建構函式建立`BLOB`物件。 呼叫`BLOB`物件的`setAttachmentID`方法並傳遞附件識別碼值，以附件識別碼值填入`BLOB`物件。 此值可透過叫用`org.apache.axis.attachments.AttachmentPart`物件的`getContentId`方法取得。
1. 叫用`EncryptDocumentSoapBindingStub`物件的`invoke`方法，以叫用`MyApplication/EncryptDocument`處理序。 傳遞包含DIME附件的`BLOB`物件。 此程式會傳回`BLOB`物件中的加密PDF檔案。
1. 透過叫用傳回的`BLOB`物件的`getAttachmentID`方法，取得附件識別碼值。 此方法會傳回代表傳回附件之識別碼值的字串值。
1. 透過叫用`EncryptDocumentSoapBindingStub`物件的`getAttachments`方法擷取附件。 此方法傳回代表附件的`Objects`陣列。
1. 逐一檢視附件（`Object`陣列），並使用附件識別碼值來取得加密的PDF檔案。 每個元素都是`org.apache.axis.attachments.AttachmentPart`物件。
1. 透過叫用`org.apache.axis.attachments.AttachmentPart`物件的`getDataHandler`方法，取得與附件相關聯的`javax.activation.DataHandler`物件。
1. 透過叫用`javax.activation.DataHandler`物件的`getInputStream`方法取得`java.io.FileStream`物件。
1. 建立位元組陣列，並將該位元組陣列傳遞至`java.io.FileStream`物件的`read`方法。 此方法會以代表加密PDF檔案的資料流填入位元組陣列。
1. 使用物件的建構函式建立`java.io.File`物件。 此物件代表加密的PDF檔案。
1. 使用它的建構函式並傳遞`java.io.File`物件來建立`java.io.FileOutputStream`物件。
1. 叫用`java.io.FileOutputStream`物件的`write`方法，並傳遞包含代表加密PDF檔案的資料串流的位元組陣列。

**另請參閱**

[快速入門：在Java專案中使用DIME叫用服務](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## 使用SAML型驗證 {#using-saml-based-authentication}

叫用服務時，AEM Forms支援各種Web服務驗證模式。 一種驗證模式是使用Web服務呼叫中的基本授權標頭同時指定使用者名稱和密碼值。 AEM Forms也支援SAML宣告式驗證。 當使用者端應用程式使用Web服務叫用AEM Forms服務時，使用者端應用程式可以透過下列其中一種方式提供驗證資訊：

* 以基本授權的一部分傳遞認證
* 在WS-Security標頭中傳遞使用者名稱權杖
* 在WS-Security標頭中傳遞SAML宣告
* 在WS-Security標頭中傳遞Kerberos權杖

AEM Forms不支援標準的憑證式驗證，但支援其他格式的憑證式驗證。

>[!NOTE]
>
>使用AEM Forms的程式設計中的Web服務快速啟動，可指定使用者名稱和密碼值以執行授權。

AEM表單使用者的身分可透過使用秘密金鑰簽署的SAML宣告來表示。 下列XML程式碼顯示SAML判斷提示的範例。

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

此範例宣告會針對管理員使用者發出。 此判斷提示包含下列值得注意的專案：

* 在特定期間內有效。
* 它是發行給特定使用者。
* 經過數位簽署。 因此，對其所做的任何修改都會破壞簽名。
* 這可向AEM Forms呈現為類似於使用者名稱和密碼的使用者身分權杖。

使用者端應用程式可從傳回`AuthResult`物件的任何AEM Forms AuthenticationManager API擷取宣告。 若要取得`AuthResult`執行個體，請執行下列其中一種方法：

* 使用AuthenticationManager API公開的任何驗證方法來驗證使用者。 一般而言，會使用使用者名稱和密碼；不過，您也可以使用憑證驗證。
* 使用`AuthenticationManager.getAuthResultOnBehalfOfUser`方法。 此方法可讓使用者端應用程式取得任何AEM表單使用者的`AuthResult`物件。

AEM表單使用者可使用取得的SAML權杖進行驗證。 此SAML宣告（xml片段）可以作為WS-Security標頭的一部分，連同用於使用者驗證的Web服務呼叫一起傳送。 一般而言，使用者端應用程式已經驗證使用者，但尚未儲存使用者認證。 （或使用者已透過使用使用者名稱和密碼以外的機制登入該使用者端。） 在此情況下，使用者端應用程式必須叫用AEM Forms，並模擬允許叫用AEM Forms的特定使用者。

若要模擬特定使用者，請使用Web服務叫用`AuthenticationManager.getAuthResultOnBehalfOfUser`方法。 此方法會傳回包含該使用者之SAML宣告的`AuthResult`執行個體。

接下來，使用該SAML宣告來叫用需要驗證的任何服務。 此動作包括傳送宣告作為SOAP標頭的一部分。 使用此宣告進行Web服務呼叫時，AEM Forms會將使用者識別為該宣告所代表的使用者。 也就是說，宣告中指定的使用者是叫用服務的使用者。

### 使用Apache Axis類別和SAML型驗證 {#using-apache-axis-classes-and-saml-based-authentication}

您可以透過使用Axis資料庫建立的Java Proxy類別來叫用AEM Forms服務。 （請參閱[使用Apache Axis](#creating-java-proxy-classes-using-apache-axis)建立Java Proxy類別。）

使用採用SAML型驗證的AXIS時，請使用Axis註冊請求和回應處理常式。 Apache Axis會在傳送叫用要求給AEM Forms之前叫用處理常式。 若要註冊處理常式，請建立擴充`org.apache.axis.handlers.BasicHandler`的Java類別。

**建立Axis為**&#x200B;的AssertionHandler

下列名為`AssertionHandler.java`的Java類別顯示延伸`org.apache.axis.handlers.BasicHandler`的Java類別範例。

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

若要使用Axis註冊處理常式，請建立client-config.wsdd檔案。 依預設，Axis會尋找具有此名稱的檔案。 下列XML程式碼為client-config.wsdd檔案的範例。 如需詳細資訊，請參閱Axis檔案。

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

以下程式碼範例會使用SAML型驗證叫用AEM Forms服務。

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

### 使用.NET使用者端元件和SAML型驗證 {#using-a-net-client-assembly-and-saml-based-authentication}

您可以使用.NET使用者端元件和SAML型驗證來叫用Forms服務。 若要這麼做，您必須使用Web服務增強功能3.0 (WSE)。 如需有關建立使用WSE的.NET使用者端元件的資訊，請參閱[建立使用DIME的.NET專案](#creating-a-net-project-that-uses-dime)。

>[!NOTE]
>
>DIME區段使用WSE 2.0。若要使用SAML型驗證，請遵循在DIME主題中指定的相同指示。 不過，請將WSE 2.0取代為WSE 3.0。在開發電腦上安裝Web Services Enhancements 3.0，並將其與Microsoft Visual Studio .NET整合。 您可以從[Microsoft下載中心](https://www.microsoft.com/downloads/search.aspx)下載Web服務增強功能3.0。

WSE架構使用原則、判斷提示和SecurityToken資料型別。 簡而言之，對於Web服務呼叫，請指定原則。 一個原則可以有多個判斷提示。 每個判斷提示都可以包含篩選器。 篩選器會在Web服務呼叫的特定階段叫用，而且他們當時可以修改SOAP請求。 如需完整詳細資訊，請參閱Web服務增強功能3.0檔案。

**建立判斷提示和篩選器**

下列C#程式碼範例會建立篩選和宣告類別。 此程式碼範例會建立SamlAssertionOutputFilter。 在將SOAP要求傳送至AEM Forms之前，WSE架構會叫用此篩選器。

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

建立類別以代表SAML宣告。 此類別執行的主要工作是將資料值從字串轉換為xml並保留空格。 此判斷提示xml稍後會匯入SOAP要求中。

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

以下C#程式碼範例使用SAML型驗證叫用Forms服務。

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

## 使用網站服務時的相關考量事項 {#related-considerations-when-using-web-services}

有時候，當透過使用網站服務叫用某些AEM Forms服務操作時，會發生問題。 本討論的目標是找出這些問題，並提供解決方案（如果有的話）。

### 非同步叫用服務作業 {#invoking-service-operations-asynchronously}

如果您嘗試非同步叫用AEM Forms服務作業(例如產生PDF的`htmlToPDF`作業)，就會發生`SoapFaultException`。 若要解決此問題，請建立自訂繫結XML檔案，將`ExportPDF_Result`元素與其他元素對應至不同的類別。 下列XML代表自訂繫結檔案。

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

使用JAX-WS建立Java Proxy檔案時，請使用此XML檔案。 （請參閱[使用JAX-WS建立Java Proxy類別](#creating-java-proxy-classes-using-jax-ws)。）

使用 — `b`命令列選項執行JAX-WS工具(wsimport.exe)時，參考此XML檔案。 更新繫結XML檔案中的`wsdlLocation`專案，以指定AEM Forms的URL。

若要確保非同步引動運作正常，請修改端點URL值並指定`async=true`。 例如，對於使用JAX-WS建立的Java Proxy檔案，請為`BindingProvider.ENDPOINT_ADDRESS_PROPERTY`指定下列專案。

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

下列清單指定以非同步方式叫用時，需要自訂繫結檔案的其他服務：

* PDFG3D
* 任務管理員
* 應用程式管理員
* 目錄管理員
* Distiller
* Rights Management
* 檔案管理

### J2EE應用程式伺服器的差異 {#differences-in-j2ee-application-servers}

有時候，使用特定J2EE應用程式伺服器建立的Proxy程式庫無法成功叫用託管於其他J2EE應用程式伺服器上的AEM Forms。 假設使用WebSphere上部署的AEM Forms產生的Proxy程式庫。 此Proxy程式庫無法成功叫用部署在JBoss應用程式伺服器上的AEM Forms服務。

在WebSphere上部署AEM Forms時，有些AEM Forms複雜資料型別（例如`PrincipalReference`）的定義與JBoss Application Server不同。 不同J2EE應用程式服務所使用的JDK不同，是WSDL定義有差異的原因。 因此，請使用從相同J2EE應用程式伺服器產生的Proxy程式庫。

### 使用網站服務存取多項服務 {#accessing-multiple-services-using-web-services}

由於名稱空間衝突，資料物件無法在多個服務WSDL之間共用。 不同的服務可以共用資料型別，因此這些服務在WSDL中共用這些型別的定義。 例如，您無法將包含`BLOB`資料型別的兩個.NET使用者端元件新增至相同的.NET使用者端專案。 如果嘗試執行此動作，會發生編譯錯誤。

下列清單指定無法在多個服務WSDL之間共用的資料型別：

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

若要避免此問題，建議您完全限定資料型別。 例如，假設一個.NET應用程式使用服務參照同時參照Forms服務和簽章服務。 兩個服務參考將包含`BLOB`類別。 若要使用`BLOB`執行個體，請在宣告`BLOB`物件時完全限定該物件。 以下程式碼範例說明此方法。 如需此程式碼範例的相關資訊，請參閱[數位簽署互動式Forms](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)。

以下C#程式碼範例對Forms服務轉譯的互動式表單加上簽名。 使用者端應用程式有兩個服務參考。 與Forms服務關聯的`BLOB`執行個體屬於`SignInteractiveForm.ServiceReference2`名稱空間。 同樣地，與簽章服務相關聯的`BLOB`執行個體屬於`SignInteractiveForm.ServiceReference1`名稱空間。 已簽署的互動式表單會儲存為名為&#x200B;*LoanXFASigned.pdf*&#x200B;的PDF檔案。

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
                    //it is necessary to fully qualify the BLOB objects
 
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
 
                    //Specify an XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify an XML form data
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

### 以字母開頭的服務會產生無效的Proxy檔案 {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

使用Microsoft .Net 3.5和WCF時，某些AEM Forms產生的Proxy類別名稱不正確。 為IBMFilenetContentRepositoryConnector、IDPchedulerService或其名稱以字母I開頭的任何其他服務建立Proxy類別時，就會發生此問題。例如，如果有IBMFileNetContentRepositoryConnector，則產生的使用者端名稱為`BMFileNetContentRepositoryConnectorClient`。 產生的Proxy類別中缺少字母I。
