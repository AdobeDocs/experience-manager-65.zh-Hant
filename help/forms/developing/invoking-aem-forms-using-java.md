---
title: 使用JavaAPI調用AEM Forms
seo-title: Invoking AEM Forms using the JavaAPI
description: 使用AEM FormsJava API（用於RMI傳輸協定）進行遠程調用，使用VM傳輸進行本地調用，使用SOAP進行遠程調用，使用不同的身份驗證，如用戶名和口令，以及同步和非同步調用請求。
seo-description: Use the AEM Forms Java API for RMI transport protocol for remote invocation, VM transport for local invocation, SOAP for remote invocation, different authentication, such as user name and password, and synchronous and asynchronous invocation requests.
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '5398'
ht-degree: 0%

---

# 使用Java API調用AEM Forms {#invoking-aem-forms-using-the-javaapi}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

AEM Forms可以使用AEM FormsJava API調用。 使用AEM FormsJava API時，可以使用調用API或Java客戶端庫。 Java客戶端庫可用於Rights Management服務等服務。 這些強類型API使您能夠開發調用AEM Forms的Java應用程式。

調用API是位於 `com.adobe.idp.dsc` 檔案。 使用這些類，您可以直接向服務發送調用請求並處理返回的調用響應。 使用調用API調用使用Workbench建立的短壽命或長壽命進程。

以寫程式方式調用服務的建議方法是使用與調用API相對應的服務的Java客戶端庫。 例如，要調用加密服務，請使用加密服務客戶端庫。 要執行加密服務操作，請調用屬於加密服務客戶端對象的方法。 您可以通過調用PDF `EncryptionServiceClient` 對象 `encryptPDFUsingPassword` 的雙曲餘切值。

Java API支援以下功能：

* 用於遠程調用的RMI傳輸協定
* 用於本地調用的VM傳輸
* 用於遠程調用的SOAP
* 不同的身份驗證，如用戶名和密碼
* 同步和非同步調用請求

[包括AEM FormsJava庫檔案](#including-aem-forms-java-library-files)

[調用以人為中心的長壽命進程](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用Web服務調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md)

[設定連接屬性](#setting-connection-properties)

[使用Java API將資料傳遞到AEM Forms服務](#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](#invoking-a-service-using-a-java-client-library)

[使用調用API調用短期進程](#invoking-a-short-lived-process-using-the-invocation-api)

[建立調用以人為中心的長壽命進程的Java Web應用程式](/help/forms/developing/invoking-human-centric-long-lived.md)

## 包括AEM FormsJava庫檔案 {#including-aem-forms-java-library-files}

要通過使用Java API以寫程式方式調用AEM Forms服務，請在Java項目的類路徑中包含所需的庫檔案（JAR檔案）。 您在客戶端應用程式的類路徑中包含的JAR檔案取決於以下幾個因素：

* AEM Forms服務調用。 客戶端應用程式可以調用一個或多個服務。
* 要調用AEM Forms服務的模式。 可以使用EJB或SOAP模式。 (請參閱 [設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。)

>[!NOTE]
>
>（僅全包式）使用命令啟動AEM Forms伺服器 `standalone.bat -b <Server IP> -c lc_turnkey.xml` 為EJB指定伺服器IP

* 部署了AEM Forms的J2EE應用程式伺服器。

### 特定於服務的JAR檔案 {#service-specific-jar-files}

下表列出了調用AEM Forms服務所需的JAR檔案。

<table>
 <thead>
  <tr>
   <th><p>檔案</p></th>
   <th><p>說明</p></th>
   <th><p>位置</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>必須始終包含在Java客戶端應用程式的類路徑中。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>必須始終包含在Java客戶端應用程式的類路徑中。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>必須始終包含在Java客戶端應用程式的類路徑中。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk//client libs/&lt;app server=""&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>調用Application Manager服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>調用匯編器服務時必需。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>調用備份和還原服務API時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>調用條形碼表單服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>調用轉換PDF服務時必需。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>調用Distiller服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>調用DocConverter服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>調用文檔管理服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>調用加密服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>調用Forms服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>調用表單資料整合服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>調用生成PDF服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>調用「生成3DPDF」服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>調用作業管理器服務時必需。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>調用輸出服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>調用PDF實用程式或實用程式XMP服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>調用Acrobat Reader DC擴展服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>調用儲存庫服務時必需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端 — libs\thirparty</p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>調用Rights Management服務時必需。</p><p>如果AEM Forms部署在JBoss上，請包括所有這些檔案。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p><p>JBoss特定庫目錄</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>調用簽名服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>調用任務管理器服務時必需。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>調用信任儲存服務時必需。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/客戶端libs/common</p></td>
  </tr>
 </tbody>
</table>

### 連接模式和J2EE應用程式JAR檔案 {#connection-mode-and-j2ee-application-jar-files}

下表列出了依賴於連接模式的JAR檔案以及部署了AEM Forms的J2EE應用程式伺服器。

<table>
 <thead>
  <tr>
   <th><p>檔案</p> </th>
   <th><p>說明</p> </th>
   <th><p>位置</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1β-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>如果使用SOAP模式調用AEM Forms，請包括這些JAR檔案。</p> </td>
   <td><p>&lt;<em>安裝目錄</em>&gt;/sdk/客戶端 — libs/第三方</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>如果AEM Forms部署在JBoss Application Server，請包括此JAR檔案。</p> <p>如果jboss-client.jar和引用的jar未共同定位，則classloader將找不到所需的類。</p> </td>
   <td><p>JBoss客戶端庫目錄</p> <p>如果在同一J2EE應用程式伺服器上部署客戶端應用程式，則無需包括此檔案。</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>如果AEM Forms部署在BEA WebLogic Server®上，則包括此JAR檔案。</p> </td>
   <td><p>WebLogic特定庫目錄</p> <p>如果在同一J2EE應用程式伺服器上部署客戶端應用程式，則無需包括此檔案。</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>如果AEM Forms部署在WebSphere應用程式伺服器上，請包括這些JAR檔案。</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar是Web服務調用的必需項)。</p> </li>
    </ul> </td>
   <td><p>WebSphere特定庫目錄(<em>[WAS_HOME]</em>/runtimes)</p> <p>如果在同一J2EE應用程式伺服器上部署客戶端應用程式，則不必包括這些檔案。</p> </td>
  </tr>
 </tbody>
</table>

### 調用方案 {#invoking-scenarios}

下表指定調用方案並列出成功調用AEM Forms所需的JAR檔案。

<table>
 <thead>
  <tr>
   <th><p>服務</p> </th>
   <th><p>調用模式</p> </th>
   <th><p>J2EE應用伺服器</p> </th>
   <th><p>所需的JAR檔案</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Forms</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Forms</p> <p>Acrobat Reader DC擴展服務</p> <p>簽名服務</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Forms</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio_jar</p> </li>
     <li><p>jaxen-1.1β-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Forms</p> <p>Acrobat Reader DC擴展服務</p> <p>簽名服務</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio_jar</p> </li>
     <li><p>jaxen-1.1β-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### 升級JAR檔案 {#upgrading-jar-files}

如果要從LiveCycle升級到AEM Forms，建議將AEM FormsJAR檔案包含在Java項目的類路徑中。 例如，如果您使用的是Rights Management服務等服務，則如果類路徑中未包含AEM FormsJAR檔案，則將遇到相容性問題。

假設你要升級到AEM Forms。 要使用調用Rights Management服務的Java應用程式，請包括以下JAR檔案的AEM Forms版本：

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**另請參閱**

[使用Java API調用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API將資料傳遞到AEM Forms服務](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 設定連接屬性 {#setting-connection-properties}

使用Java API時，可設定連接屬性以調用AEM Forms。 設定連接屬性時，指定是遠程還是本地調用服務，還指定連接模式和驗證值。 如果啟用了服務安全性，則需要驗證值。 但是，如果禁用了服務安全性，則無需指定驗證值。

連接模式可以是SOAP模式或EJB模式。 EJB模式使用RMI/IIOP協定，EJB模式的效能優於SOAP模式。 SOAP模式用於消除J2EE應用程式伺服器依賴性或當防火牆位於AEM Forms和客戶端應用程式之間時。 SOAP模式使用https協定作為基礎傳輸，並可跨防火牆邊界進行通信。 如果J2EE應用程式伺服器依賴項或防火牆都不是問題，則建議使用EJB模式。

要成功調用AEM Forms服務，請設定以下連接屬性：

* **DSC_DEFAULT_EJB_ENDPOINT:** 如果使用EJB連接模式，則此值表示部署了AEM Forms的J2EE應用程式伺服器的URL。 要遠程調用AEM Forms，請指定部署AEM Forms的J2EE應用程式伺服器名稱。 如果客戶端應用程式位於同一J2EE應用程式伺服器上，則可以指定 `localhost`。 根據部署J2EE應用程式伺服器AEM Forms的位置，指定以下值之一：

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**:如果使用SOAP連接模式，此值表示將調用請求發送到的終結點。 要遠程調用AEM Forms，請指定部署AEM Forms的J2EE應用程式伺服器名稱。 如果客戶端應用程式位於同一J2EE應用程式伺服器上，可以指定 `localhost` (例如， `http://localhost:8080`。)

   * 埠值 `8080` 如果J2EE應用程式是JBoss，則適用。 如果J2EE應用程式伺服器是IBM® WebSphere®，請使用埠 `9080`。 同樣，如果J2EE應用程式伺服器是WebLogic，則使用埠 `7001`。 (這些值是預設埠值。 如果更改了埠值，請使用適用的埠號。)

* **DSC_TRANSPORT_PROTOCOL**:如果使用EJB連接模式，請指定 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 值。 如果使用SOAP連接模式，請指定 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`。
* **DSC_SERVER_TYPE**:指定部署AEM Forms的J2EE應用程式伺服器。 有效值為 `JBoss`。 `WebSphere`。 `WebLogic`。

   * 如果將此連接屬性設定為 `WebSphere`，也請參見Wiki頁。 `java.naming.factory.initial` 值設定為 `com.ibm.ws.naming.util.WsnInitCtxFactory`。
   * 如果將此連接屬性設定為 `WebLogic`，也請參見Wiki頁。 `java.naming.factory.initial` 值設定為 `weblogic.jndi.WLInitialContextFactory`。
   * 同樣，如果將此連接屬性設定為 `JBoss`，也請參見Wiki頁。 `java.naming.factory.initial` 值設定為 `org.jnp.interfaces.NamingContextFactory`。
   * 可以設定 `java.naming.factory.initial` 屬性到滿足您要求的值（如果您不想使用預設值）。

   >[!NOTE]
   >
   >而不是使用字串來設定 `DSC_SERVER_TYPE` connection屬性，可以使用 `ServiceClientFactoryProperties` 類。 可以使用以下值： `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`。 `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`或 `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`。

* **DSC_CREDENTIAL_USERNAME:** 指定表AEM單用戶名。 用戶若要成功調用AEM Forms服務，需要「服務用戶」角色。 用戶還可以具有包含「服務調用」權限的其他角色。 否則，當它們嘗試調用服務時會引發異常。 如果禁用了服務安全性，則無需指定此連接屬性。
* **DSC_CREDENTIAL_PASSWORD:** 指定相應的密碼值。 如果禁用了服務安全性，則無需指定此連接屬性。
* **DSC_REQUEST_TIMEOUT:** SOAP請求的預設請求超時限制為1200000毫秒（20分鐘）。 有時，請求完成操作可能需要更長的時間。 例如，檢索大量記錄集的SOAP請求可能需要較長的超時限制。 您可以使用 `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` 以增加SOAP請求的請求調用超時限制。

   **附註**:只有基於SOAP的調用支援DSC_REQUEST_TIMEOUT屬性。

要設定連接屬性，請執行以下任務：

1. 建立 `java.util.Properties` 對象。
1. 設定 `DSC_DEFAULT_EJB_ENDPOINT` connection屬性，調用 `java.util.Properties` 對象 `setProperty` 方法並傳遞以下值：

   * 的 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 枚舉值
   * 一個字串值，它指定承載AEM Forms的J2EE應用程式伺服器的URL

   >[!NOTE]
   >
   >如果使用SOAP連接模式，請指定 `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` 枚舉值而不是 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 枚舉值。

1. 設定 `DSC_TRANSPORT_PROTOCOL` connection屬性，調用 `java.util.Properties` 對象 `setProperty` 方法並傳遞以下值：

   * 的 `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` 枚舉值
   * 的 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 枚舉值

   >[!NOTE]
   >
   >如果使用SOAP連接模式，請指定 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`枚舉值而不是 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 枚舉值。

1. 設定 `DSC_SERVER_TYPE` connection屬性，調用 `java.util.Properties` 對象 `setProperty` 方法並傳遞以下值：

   * 的 `ServiceClientFactoryProperties.DSC_SERVER_TYPE`枚舉值
   * 一個字串值，它指定承載AEM Forms的J2EE應用程式伺服器(例如，如果AEM Forms部署在JBoss上，請指定 `JBoss`)。

      1. 設定 `DSC_CREDENTIAL_USERNAME` connection屬性，調用 `java.util.Properties` 對象 `setProperty` 方法並傳遞以下值：
   * 的 `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` 枚舉值
   * 一個字串值，它指定調用AEM Forms所需的用戶名

      1. 設定 `DSC_CREDENTIAL_PASSWORD` connection屬性，調用 `java.util.Properties` 對象 `setProperty` 方法並傳遞以下值：
   * 的 `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` 枚舉值
   * 指定相應密碼值的字串值



**設定JBoss的EJB連接模式**

以下Java代碼示例設定連接屬性以調用在JBoss上部署的AEM Forms並使用EJB連接模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**設定WebLogic的EJB連接模式**

以下Java代碼示例設定連接屬性以調用部署在WebLogic上的AEM Forms並使用EJB連接模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**設定WebSphere的EJB連接模式**

以下Java代碼示例設定連接屬性以調用部署在WebSphere上的AEM Forms並使用EJB連接模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**設定SOAP連接模式**

以下Java代碼示例在SOAP模式下設定連接屬性以調用部署在JBoss上的AEM Forms。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>如果選擇SOAP連接模式，請確保在客戶端應用程式的類路徑中包含其他JAR檔案。

**禁用服務安全性時設定連接屬性**

以下Java代碼示例設定調用JBoss應用程式伺服器上部署的AEM Forms和禁用服務安全時所需的連接屬性。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>與AEM Forms寫程式關聯的所有Java快速啟動都顯示EJB和SOAP連接設定。

**使用自定義請求超時限制設定SOAP連接模式**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**使用Context對象調用AEM Forms**

您可以使用 `com.adobe.idp.Context` 用已驗證用戶調用AEM Forms服務的對象( `com.adobe.idp.Context` 對象表示已驗證的用戶)。 使用 `com.adobe.idp.Context` 對象，您不需要設定 `DSC_CREDENTIAL_USERNAME` 或 `DSC_CREDENTIAL_PASSWORD` 屬性。 您可以 `com.adobe.idp.Context` 使用 `AuthenticationManagerServiceClient` 對象 `authenticate` 的雙曲餘切值。

的 `authenticate` 方法返回 `AuthResult` 包含驗證結果的對象。 可以建立 `com.adobe.idp.Context` 調用其建構子。 然後調用 `com.adobe.idp.Context` 對象 `initPrincipal` 方法和通過 `AuthResult` 對象，如以下代碼所示：

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

而不是設定 `DSC_CREDENTIAL_USERNAME` 或 `DSC_CREDENTIAL_PASSWORD` 屬性，可以調用 `ServiceClientFactory` 對象 `setContext` 方法和通過 `com.adobe.idp.Context` 的雙曲餘切值。 使用表AEM單用戶調用服務時，請確保他們的角色名為 `Services User` 需要調用AEM Forms服務。

以下代碼示例說明如何使用 `com.adobe.idp.Context` 連接設定中用於建立的對象 `EncryptionServiceClient` 的雙曲餘切值。

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>有關驗證用戶身份的完整詳細資訊，請參閱 [驗證用戶](/help/forms/developing/users.md#authenticating-users)。

### 調用方案 {#invoking_scenarios-1}

本節將討論以下調用方案：

* 在其自己的Java虛擬機(JVM)中運行的客戶端應用程式調用獨立的AEM Forms實例。
* 在其自己的JVM中運行的客戶端應用程式調用群集的AEM Forms實例。

### 調用獨立AEM Forms實例的客戶端應用程式 {#client-application-invoking-a-stand-alone-aem-forms-instance}

下圖顯示了在自己的JVM中運行並調用獨立的AEM Forms實例的客戶端應用程式。

在此方案中，客戶端應用程式正在其自己的JVM中運行並調用AEM Forms服務。

>[!NOTE]
>
>此方案是所有快速啟動都基於的調用方案。

### 客戶端應用程式調用群集AEM Forms實例 {#client-application-invoking-clustered-aem-forms-instances}

下圖顯示了在自己的JVM中運行並調用群集中的AEM Forms實例的客戶端應用程式。

此方案類似於調用獨立AEM Forms實例的客戶端應用程式。 但是，提供程式URL不同。 如果客戶端應用程式要連接到特定的J2EE應用程式伺服器，則該應用程式必須更改URL以引用特定的J2EE應用程式伺服器。

不建議引用特定的J2EE應用程式伺服器，因為如果應用程式伺服器停止，客戶端應用程式與AEM Forms之間的連接將終止。 建議提供程式URL引用單元級JNDI管理器，而不是特定的J2EE應用程式伺服器。

使用SOAP連接模式的客戶端應用程式可以使用群集的HTTP負載平衡器埠。 使用EJB連接模式的客戶端應用程式可以連接到特定J2EE應用程式伺服器的EJB埠。 此操作處理群集節點之間的負載平衡。

**WebSphere**

以下示例顯示用於連接到部署在WebSphere上的AEM Forms的jndi.properties檔案的內容。

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

以下示例顯示用於連接到部署在WebLogic上的AEM Forms的jndi.properties檔案的內容。

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

以下示例顯示用於連接到部署在JBoss上的AEM Forms的jndi.properties檔案的內容。

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>請咨詢管理員以確定J2EE應用程式伺服器名稱和埠號。

**另請參閱**

[包括AEM FormsJava庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java API將資料傳遞到AEM Forms服務](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java API將資料傳遞到AEM Forms服務 {#passing-data-to-aem-forms-services-using-the-java-api}

AEM Forms服務操作通常使用或生成PDF文檔。 在調用服務時，有時需要將PDF文檔（或其它文檔類型，如XML資料）傳遞到服務。 同樣，有時還需要處理從服務返回的PDF文檔。 使您能夠向AEM Forms服務傳遞資料和從Java服務傳遞資料的Java類是 `com.adobe.idp.Document`。

AEM Forms服務不接受PDF文檔作為其他資料類型，如 `java.io.InputStream` 對象或位元組陣列。 A `com.adobe.idp.Document` 對象還可用於將其他類型的資料（如XML資料）傳遞給服務。

A `com.adobe.idp.Document` object是可序列化的Java類型，因此可以通過RMI調用傳遞它。 接收端可以配置（同一主機、同一類載入器）、本地（同一主機、不同類載入器）或遠程（不同主機）。 針對每種情況優化文檔內容的傳遞。 例如，如果發送者和接收者位於同一台主機上，則內容將通過本地檔案系統傳遞。 （在某些情況下，文檔可以在記憶體中傳遞。）

取決於 `com.adobe.idp.Document` 對象大小，資料在 `com.adobe.idp.Document` 對象或儲存在伺服器的檔案系統上。 所佔用的任何臨時儲存資源 `com.adobe.idp.Document` 對象在 `com.adobe.idp.Document` 處置。 (請參閱 [處理文檔對象](invoking-aem-forms-using-java.md#disposing-document-objects)。)

有時需要瞭解 `com.adobe.idp.Document` 對象，然後將其傳遞給服務。 例如，如果操作需要特定內容類型，如 `application/pdf`，建議您確定內容類型。 (請參閱 [確定文檔的內容類型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)。)

的 `com.adobe.idp.Document` 對象嘗試使用提供的資料確定內容類型。 如果無法從提供的資料中檢索內容類型（例如，當資料作為位元組陣列提供時），請設定內容類型。 要設定內容類型，請調用 `com.adobe.idp.Document` 對象 `setContentType` 的雙曲餘切值。 (請參閱 [確定文檔的內容類型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

如果宣傳資料檔案位於同一檔案系統上，則建立 `com.adobe.idp.Document` 對象更快。 如果宣傳資料檔案位於遠程檔案系統上，則必須執行複製操作，這會影響效能。

應用程式可以同時包含 `com.adobe.idp.Document` 和 `org.w3c.dom.Document` 資料類型。 但是，請確保您完全符合 `org.w3c.dom.Document` 資料類型。 有關轉換的資訊 `org.w3c.dom.Document` 對象 `com.adobe.idp.Document` 對象，請參閱 [快速啟動（EJB模式）:使用Java API使用可流式佈局預填充Forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)。

>[!NOTE]
>
>在使用 `com.adobe.idp.Document` 對象，以2048位元組或更少的塊為單位讀取文檔資訊。 例如，以下代碼以2048位元組的塊為單位讀取文檔資訊：

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**另請參閱**

[使用Java API調用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 建立文檔 {#creating-documents}

建立 `com.adobe.idp.Document` 調用需要PDF文檔（或其他文檔類型）作為輸入值的服務操作之前。 的 `com.adobe.idp.Document` 類提供了建構子，使您能夠從以下內容類型建立文檔：

* 位元組陣列
* 現有 `com.adobe.idp.Document` 對象
* A `java.io.File` 對象
* A `java.io.InputStream` 對象
* A `java.net.URL` 對象

#### 基於位元組陣列建立文檔 {#creating-a-document-based-on-a-byte-array}

下面的代碼示例建立 `com.adobe.idp.Document` 基於位元組陣列的對象。

**建立基於位元組陣列的Document對象**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### 基於其他文檔建立文檔 {#creating-a-document-based-on-another-document}

下面的代碼示例建立 `com.adobe.idp.Document` 基於另一個對象 `com.adobe.idp.Document` 的雙曲餘切值。

**建立基於其他文檔的文檔對象**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### 基於檔案建立文檔 {#creating-a-document-based-on-a-file}

下面的代碼示例建立 `com.adobe.idp.Document` 基於名為的PDF檔案的對象 *地圖.pdf*。 此檔案位於C硬碟的根目錄中。 此建構子嘗試設定 `com.adobe.idp.Document` 對象。

的 `com.adobe.idp.Document` 接受的建構子 `java.io.File` 對象也接受布爾參數。 通過將此參數設定為 `true`，也請參見Wiki頁。 `com.adobe.idp.Document` 對象刪除檔案。 此操作意味著您不必在將檔案傳遞到 `com.adobe.idp.Document` 建構子。

將此參數設定為 `false` 表示您保留此檔案的所有權。 將此參數設定為 `true` 效率更高。 原因是 `com.adobe.idp.Document` 對象可以將檔案直接移動到本地管理區域，而不是複製（速度較慢）。

**建立基於PDF檔案的文檔對象**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### 基於InputStream對象建立文檔 {#creating-a-document-based-on-an-inputstream-object}

以下Java代碼示例建立 `com.adobe.idp.Document` 基於 `java.io.InputStream` 的雙曲餘切值。

**基於InputStream對象建立文檔**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### 基於可從URL訪問的內容建立文檔 {#creating-a-document-based-on-content-accessible-from-an-url}

以下Java代碼示例建立 `com.adobe.idp.Document` 基於名為的PDF檔案的對象 *地圖.pdf*。 此檔案位於名為 `WebApp` 它正在運行 `localhost`。 此建構子嘗試設定 `com.adobe.idp.Document` 使用URL協定返回的內容類型返回的對象的MIME內容類型。

提供給的URL `com.adobe.idp.Document` 對象始終在原始 `com.adobe.idp.Document` 對象已建立，如本示例所示：

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

c:/temp/input.pdf檔案必須位於客戶端電腦上（不在伺服器電腦上）。 客戶端電腦是讀取URL的位置， `com.adobe.idp.Document` 已建立對象。

**基於可從URL訪問的內容建立文檔**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**另請參閱**

[使用Java API調用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 處理返回的文檔 {#handling-returned-documents}

將PDF文檔（或其他資料類型，如XML資料）作為輸出值返回的服務操作 `com.adobe.idp.Document` 的雙曲餘切值。 在您收到 `com.adobe.idp.Document` 對象，可將其轉換為以下格式：

* A `java.io.File` 對象
* A `java.io.InputStream` 對象
* 位元組陣列

以下代碼行將轉換 `com.adobe.idp.Document` 對象 `java.io.InputStream` 的雙曲餘切值。 假設 `myPDFDocument` 表示 `com.adobe.idp.Document` 對象：

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

同樣，您可以複製 `com.adobe.idp.Document` 執行以下任務，將檔案複製到本地檔案：

1. 建立 `java.io.File` 的雙曲餘切值。
1. 調用 `com.adobe.idp.Document` 對象 `copyToFile` 方法和通過 `java.io.File`的雙曲餘切值。

以下代碼示例複製 `com.adobe.idp.Document` 對象到名為 *OtherMap.pdf*。

**將文檔對象的內容複製到檔案**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**另請參閱**

[使用Java API調用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 確定文檔的內容類型 {#determining-the-content-type-of-a-document}

確定MIME類型 `com.adobe.idp.Document` 通過調用 `com.adobe.idp.Document` 對象 `getContentType` 的雙曲餘切值。 此方法返回一個字串值，它指定 `com.adobe.idp.Document` 的雙曲餘切值。 下表介紹了AEM Forms返回的不同內容類型。

<table>
 <thead>
  <tr>
   <th><p>MIME類型</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>PDF文檔</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>XML資料打包(XDP)，用於導出的XMLForms體系結構(XFA)表單</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>書籤、附件或其他XML文檔</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Forms資料格式(FDF)，用於導出的Acrobat表單</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XMLForms資料格式(XFDF)，用於導出的Acrobat表單</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>富資料格式和XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>通用資料格式</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>未指定的MIME類型</p></td>
  </tr>
 </tbody>
</table>

下面的代碼示例確定 `com.adobe.idp.Document` 的雙曲餘切值。

**確定文檔對象的內容類型**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**另請參閱**

[使用Java API調用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 處理文檔對象 {#disposing-document-objects}

當你不再需要 `Document` 對象，建議您通過調用 `dispose` 的雙曲餘切值。 每個 `Document` 對象在應用程式的主機平台上消耗檔案描述符和高達75 MB的RAM空間。 如果 `Document` 對象未處置，則Java Garage收集進程將處理它。 但是，通過使用 `dispose` 方法，可釋放 `Document` 的雙曲餘切值。

**另請參閱**

[使用Java API調用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包括AEM FormsJava庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java客戶端庫調用服務 {#invoking-a-service-using-a-java-client-library}

AEM Forms服務操作可通過使用服務的強類型API（稱為Java客戶端庫）來調用。 A *Java客戶端庫* 是一組具體類，它們提供對部署在服務容器中的服務的訪問。 實例化表示要調用的服務的Java對象，而不是建立 `InvocationRequest` 對象。 調用API用於調用在Workbench中建立的進程，如長壽命進程。 (請參閱 [調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。)

要執行服務操作，請調用屬於Java對象的方法。 Java客戶端庫包含通常通過服務操作一對一映射的方法。 使用Java客戶端庫時，設定所需的連接屬性。 (請參閱 [設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。)

設定連接屬性後，建立 `ServiceClientFactory` 用於實例化Java對象的對象，該對象允許您調用服務。 每個具有Java客戶端庫的服務都具有相應的客戶端對象。 例如，要調用儲存庫服務，請建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。 的 `ServiceClientFactory` 對象負責維護調用AEM Forms服務所需的連接設定。

儘管獲取 `ServiceClientFactory` 通常速度很快，在首次使用工廠時會涉及一些開銷。 此對象經過優化以便重新使用，因此，如果可能，使用相同 `ServiceClientFactory` 建立多個Java客戶端對象時的對象。 即，不要建立單獨的 `ServiceClientFactory` 建立的每個客戶端庫對象的對象。

用戶管理器設定控制位於 `com.adobe.idp.Context` 影響 `ServiceClientFactory` 的雙曲餘切值。 此設定控制整個AEM Forms的所有驗證上下文生存期，包括使用Java API執行的所有調用。 預設情況下， `ServiceCleintFactory` 對象可以用兩小時。

>[!NOTE]
>
>要說明如何使用Java API（儲存庫服務）調用服務 `writeResource` 調用操作。 此操作將新資源放入儲存庫。

可以使用Java客戶端庫並執行以下步驟來調用儲存庫服務：

1. 在Java項目的類路徑中包括客戶端JAR檔案，如adobe-repository-client.jar。 有關這些檔案位置的資訊，請參見 [包括AEM FormsJava庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 設定調用服務所需的連接屬性。
1. 建立 `ServiceClientFactory` 通過調用 `ServiceClientFactory` 對象的靜態 `createInstance` 方法和傳遞 `java.util.Properties` 包含連接屬性的對象。
1. 建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。 使用 `ResourceRepositoryClient` 用於調用儲存庫服務操作的對象。
1. 建立 `RepositoryInfomodelFactoryBean` 對象使用其建構子和傳遞 `null`。 此對象允許您建立 `Resource` 表示添加到儲存庫的內容的對象。
1. 建立 `Resource` 通過調用 `RepositoryInfomodelFactoryBean` 對象 `newImage` 方法並傳遞以下值：

   * 通過指定 `new Id()`。
   * 通過指定唯一UUID值 `new Lid()`。
   * 資源的名稱。 可以指定XDP檔案的檔案名。

   將返回值強制轉換為 `Resource`。

1. 建立 `ResourceContent` 通過調用 `RepositoryInfomodelFactoryBean` 對象 `newImage` 將返回值轉換為 `ResourceContent`。 此對象表示添加到儲存庫的內容。
1. 建立 `com.adobe.idp.Document` 通過傳遞對象 `java.io.FileInputStream` 儲存要添加到儲存庫的XDP檔案的對象。 (請參閱 [基於InputStream對象建立文檔](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)。)
1. 添加 `com.adobe.idp.Document` 對象 `ResourceContent` 通過調用 `ResourceContent` 對象 `setDataDocument` 的雙曲餘切值。 通過 `com.adobe.idp.Document` 的雙曲餘切值。
1. 通過調用 `ResourceContent` 對象 `setMimeType` 方法 `application/vnd.adobe.xdp+xml`。
1. 添加 `ResourceContent` 對象 `Resource` 通過調用 `Resource` 對象s `setContent` 方法和傳遞 `ResourceContent` 的雙曲餘切值。
1. 通過調用 `Resource` 對象s `setDescription` 方法，並傳遞表示資源說明的字串值。
1. 通過調用 `ResourceRepositoryClient` 對象 `writeResource` 方法並傳遞以下值：

   * 一個字串值，它指定包含新資源的資源集合的路徑
   * 的 `Resource` 建立的對象

**另請參閱**

[快速啟動（EJB模式）:使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[使用Java API調用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包括AEM FormsJava庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 使用調用API調用短期進程 {#invoking-a-short-lived-process-using-the-invocation-api}

可以使用Java調用API調用短期進程。 使用調用API調用短期進程時，使用 `java.util.HashMap` 的雙曲餘切值。 對於要傳遞到服務的每個參數，調用 `java.util.HashMap` 對象 `put` 方法，並指定服務執行指定操作所需的名稱 — 值對。 指定屬於短期進程的參數的確切名稱。

>[!NOTE]
>
>有關調用長期進程的資訊，請參見 [調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

這裡討論的是使用調用API來調用以下名為的AEM Forms短期進程 `MyApplication/EncryptDocument`。

>[!NOTE]
>
>該進程不基於現有的AEM Forms進程。 要跟隨代碼示例，請建立一個名為 `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

調用此進程時，它執行以下操作：

1. 獲取傳遞給流程的無擔保PDF文檔。 此操作基於 `SetValue` 的下界。 此進程的輸入參數是 `document` 進程變數命名 `inDoc`。
1. 使用密碼加密PDF文檔。 此操作基於 `PasswordEncryptPDF` 的下界。 密碼加密的PDF文檔在名為 `outDoc`。

### 使用Java調用API調用MyApplication/EncryptDocument短期進程 {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

調用 `MyApplication/EncryptDocument` 使用Java調用API的短期進程：

1. 在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。 (請參閱 [包括AEM FormsJava庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)
1. 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。)
1. 建立 `ServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。 A `ServiceClient` object用於調用服務操作。 它處理諸如查找、調度和路由調用請求等任務。
1. 建立 `java.util.HashMap` 對象。
1. 調用 `java.util.HashMap` 對象 `put` 方法將每個輸入參數傳遞給長壽命過程。 因為 `MyApplication/EncryptDocument` 短壽命過程需要一個類型的輸入參數 `Document`，您只需調用 `put` 方法一次，如下例所示。

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. 建立 `InvocationRequest` 通過調用 `ServiceClientFactory` 對象 `createInvocationRequest` 方法並傳遞以下值：

   * 一個字串值，它指定要調用的長壽命進程的名稱。 調用 `MyApplication/EncryptDocument` 進程，指定 `MyApplication/EncryptDocument`。
   * 表示流程操作名稱的字串值。 通常，短時間流程操作的名稱是 `invoke`。
   * 的 `java.util.HashMap` 包含服務操作所需的參數值的對象。
   * 一個布爾值，它指定 `true`，建立同步請求（此值適用於調用短期進程）。

1. 通過調用 `ServiceClient` 對象 `invoke` 方法和傳遞 `InvocationRequest` 的雙曲餘切值。 的 `invoke` 方法返回 `InvocationReponse` 的雙曲餘切值。

   >[!NOTE]
   >
   >通過傳遞值可以調用長期進程 `false`作為 `createInvocationRequest` 的雙曲餘切值。 傳遞值 `false`*建立非同步請求。*

1. 通過調用 `InvocationReponse` 對象 `getOutputParameter` 方法並傳遞一個字串值，該字串值指定輸出參數的名稱。 在這種情況下，指定 `outDoc` ( `outDoc` 是 `MyApplication/EncryptDocument` 處理)。 將返回值強制轉換為 `Document`，如下例所示。

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. 建立 `java.io.File` 並確保檔案副檔名為.pdf。
1. 調用 `com.adobe.idp.Document` 對象 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 對象。 確保使用 `com.adobe.idp.Document` 返回的對象 `getOutputParameter` 的雙曲餘切值。

**另請參閱**

[快速啟動：使用調用API調用短期進程](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[包括AEM FormsJava庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
