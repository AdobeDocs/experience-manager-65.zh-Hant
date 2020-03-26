---
title: 使用JavaAPI叫用AEM Forms
seo-title: 使用JavaAPI叫用AEM Forms
description: 'null'
seo-description: 'null'
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
translation-type: tm+mt
source-git-commit: 3fe5f243c3e39029c1605a1a1977a48dba595d64

---


# 使用Java API叫用AEM Forms {#invoking-aem-forms-using-the-javaapi}

AEM Forms可使用AEM Forms Java API來呼叫。 使用AEM Forms Java API時，您可以使用「呼叫API」或Java用戶端程式庫。 Java客戶端庫可用於Rights Management服務等服務。 這些強式型別API可讓您開發叫用AEM Forms的Java應用程式。

調用API是位於包中的類 `com.adobe.idp.dsc` 別。 使用這些類，您可以直接向服務發送調用請求並處理返回的調用響應。 使用「呼叫API」來叫用使用Workbench建立的短期或長期流程。

建議以程式設計方式叫用服務的方式是使用與服務對應的Java用戶端程式庫，而非叫用API。 例如，要調用加密服務，請使用加密服務客戶端庫。 要執行加密服務操作，請調用屬於加密服務客戶端對象的方法。 您可以叫用物件的方法，以密碼來加 `EncryptionServiceClient` 密PDF文 `encryptPDFUsingPassword` 件。

Java API支援下列功能：

* 用於遠程調用的RMI傳輸協定
* 用於本地調用的虛擬機傳輸
* 用於遠程調用的SOAP
* 不同的驗證，例如使用者名稱和密碼
* 同步和非同步呼叫請求

**Adobe開發人員網站**

Adobe開發人員網站包含下列文章，討論如何使用Java API叫用AEM Forms服務：

[使用Java servlet來叫用AEM Forms程式](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[從Java叫用AEM Forms Distiller API](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**另請參閱**

[包含AEM Forms Java程式庫檔案](#including-aem-forms-java-library-files)

[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#main-pars-text-0)

[使用Web Services叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md)

[設定連接屬性](#setting-connection-properties)

[使用Java API將資料傳送至AEM Forms服務](#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](#invoking-a-service-using-a-java-client-library)

[使用調用API調用短期進程](#invoking-a-short-lived-process-using-the-invocation-api)

[建立Java Web應用程式，以叫用以人為中心的長壽命程式](/help/forms/developing/invoking-human-centric-long-lived.md)

## 包含AEM Forms Java程式庫檔案 {#including-aem-forms-java-library-files}

若要使用Java API以程式設計方式叫用AEM Forms服務，請在Java專案的類路徑中加入必要的程式庫檔案（JAR檔案）。 您在客戶端應用程式的類路徑中包含的JAR檔案取決於以下幾個因素：

* 要叫用的AEM Forms服務。 客戶端應用程式可以調用一個或多個服務。
* 您要叫用AEM Forms服務的模式。 您可以使用EJB或SOAP模式。 (請參 [閱設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。)

>[!NOTE] （僅限統包功能）使用命令啟動AEM Forms伺服器， `standalone.bat -b <Server IP> -c lc_turnkey.xml` 以指定EJB的伺服器IP

* 部署AEM Forms的J2EE應用程式伺服器。

### 特定於服務的JAR檔案 {#service-specific-jar-files}

下表列出呼叫AEM Forms服務所需的JAR檔案。

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
   <td><p>必須一律包含在Java用戶端應用程式的類別路徑中。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>必須一律包含在Java用戶端應用程式的類別路徑中。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>必須一律包含在Java用戶端應用程式的類別路徑中。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/&lt;app server&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>調用應用程式管理器服務時必需。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>調用Assembler服務所需。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>調用備份和還原服務API時必需。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>呼叫條形碼表單服務所需。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>需要叫用「轉換PDF」服務。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>調用Distiller服務時需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>調用DocConverter服務時必需。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>需要叫用「檔案管理」服務。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>調用加密服務時必需。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>需要呼叫Forms服務。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>需要呼叫表單資料整合服務。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>需要叫用「產生PDF」服務。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>需要叫用「產生3D PDF」服務。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>調用作業管理器服務時必需。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>調用輸出服務時需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>需要叫用PDF公用程式或XMP公用程式服務。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>需要叫用Acrobat Reader DC擴充功能服務。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client-jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>調用儲存庫服務所需。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>install directory</i>&gt;/sdk/client-libs\thirdparty</p></td>
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
     <li><p>relanchingDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>需要叫用Rights Management服務。</p><p>如果AEM Forms已部署在JBoss上，請包含所有這些檔案。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p><p>JBoss專用的lib目錄</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>需要叫用簽名服務。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>調用Task Manager服務時必需。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>需要叫用信任商店服務。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### 連接模式和J2EE應用程式JAR檔案 {#connection-mode-and-j2ee-application-jar-files}

下表列出依賴連線模式的JAR檔案，以及部署AEM Forms的J2EE應用程式伺服器。

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
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
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
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>如果使用SOAP模式呼叫AEM Forms，請包含這些JAR檔案。</p> </td>
   <td><p>&lt;<em>install directory</em>&gt;/sdk/client-libs/協力廠商</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>如果AEM Forms已部署在JBoss Application Server上，請包含此JAR檔案。</p> <p>如果jboss-client.jar和引用的jar未共同定位，則classloader將找不到所需的類。</p> </td>
   <td><p>JBoss客戶端lib目錄</p> <p>如果您將用戶端應用程式部署在相同的J2EE應用程式伺服器上，就不需要包含此檔案。</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>如果AEM Forms已部署在BEA WebLogic Server®上，請加入此JAR檔案。</p> </td>
   <td><p>WebLogic專用的lib目錄</p> <p>如果您將用戶端應用程式部署在相同的J2EE應用程式伺服器上，就不需要包含此檔案。</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>如果AEM Forms已部署在WebSphere Application Server上，請包含這些JAR檔案。</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar是Web服務呼叫的必要條件)。</p> </li>
    </ul> </td>
   <td><p>WebSphere專用的lib目<em>錄([WAS_HOME]</em>/運行時)</p> <p>如果您將用戶端應用程式部署在相同的J2EE應用程式伺服器上，就不必包含這些檔案。</p> </td>
  </tr>
 </tbody>
</table>

### 叫用藍本 {#invoking-scenarios}

下表指定叫用藍本，並列出成功叫用AEM Forms所需的JAR檔案。

<table>
 <thead>
  <tr>
   <th><p>服務</p> </th>
   <th><p>調用模式</p> </th>
   <th><p>J2EE應用程式伺服器</p> </th>
   <th><p>所需的JAR檔案</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>表單服務</p> </td>
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
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>表單服務</p> <p>Acrobat Reader DC擴充功能服務</p> <p>簽名服務</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>表單服務</p> </td>
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
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
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
   <td><p>表單服務</p> <p>Acrobat Reader DC擴充功能服務</p> <p>簽名服務</p> </td>
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
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
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

如果您要從LiveCycle升級至AEM Forms，建議您將AEM Forms JAR檔案加入Java專案的類別路徑中。 例如，如果您使用Rights Management服務等服務，如果您的類別路徑中未包含AEM Forms JAR檔案，就會遇到相容性問題。

假設您要升級至AEM Forms。 若要使用叫用Rights Management服務的Java應用程式，請包含下列JAR檔案的AEM Forms版本：

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API將資料傳送至AEM Forms服務](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 設定連接屬性 {#setting-connection-properties}

使用Java API時，您可設定連線屬性來叫用AEM Forms。 在設定連接屬性時，指定是遠程還是本地調用服務，並指定連接模式和驗證值。 啟用服務安全性時，需要驗證值。 但是，如果服務安全性被禁用，則不需要指定驗證值。

連接模式可以是SOAP或EJB模式。 EJB模式使用RMI/IIOP協定，而EJB模式的效能優於SOAP模式的效能。 SOAP模式可用來消除J2EE應用程式伺服器相依性，或是當防火牆位於AEM Forms和用戶端應用程式之間時。 SOAP模式使用https通訊協定做為基礎傳輸，並可跨防火牆邊界通訊。 如果J2EE應用程式伺服器相依性或防火牆都不是問題，建議您使用EJB模式。

若要成功叫用AEM Forms服務，請設定下列連線屬性：

* **DSC_DEFAULT_EJB_ENDPOINT:** 如果您使用EJB連線模式，此值代表部署AEM Forms的J2EE應用程式伺服器的URL。 若要遠端叫用AEM Forms，請指定部署AEM Forms的J2EE應用程式伺服器名稱。 如果您的用戶端應用程式位於相同的J2EE應用程式伺服器上，則可以指定 `localhost`。 視部署J2EE應用程式伺服器AEM Forms的位置而定，指定下列其中一個值：

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**:如果您使用SOAP連接模式，此值表示發送調用請求的端點。 若要遠端叫用AEM Forms，請指定部署AEM Forms的J2EE應用程式伺服器名稱。 如果您的用戶端應用程式位於相同的J2EE應用程式伺服器上，您可 `localhost` 以指定(例如 `http://localhost:8080`。)

   * 如果J2EE應 `8080` 用程式是JBoss，則埠值適用。 如果J2EE應用程式伺服器是IBM® WebSphere®，請使用連接埠 `9080`。 同樣地，如果J2EE應用程式伺服器是WebLogic，請使用連接埠 `7001`。 (這些值是預設埠值。 如果更改了埠值，請使用適用的埠號。)

* **DSC_TRANSPORT_PROTOCOL**:如果使用EJB連接模式，請為 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 此值指定。 如果您使用SOAP連接模式，請指定 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`。
* **DSC_SERVER_TYPE**:指定部署AEM Forms的J2EE應用程式伺服器。 有效值 `JBoss`為 `WebSphere`、 `WebLogic`。

   * 如果將此連接屬性設 `WebSphere`置為， `java.naming.factory.initial` 則值將設定為 `com.ibm.ws.naming.util.WsnInitCtxFactory`。
   * 如果將此連接屬性設 `WebLogic`置為， `java.naming.factory.initial` 則值將設定為 `weblogic.jndi.WLInitialContextFactory`。
   * 同樣地，如果將此連接屬性設 `JBoss`置為， `java.naming.factory.initial` 則值將設定為 `org.jnp.interfaces.NamingContextFactory`。
   * 如果您不 `java.naming.factory.initial` 想使用預設值，可將屬性設為符合您需求的值。
   *注&#x200B;**意**:您可以使用類的靜態成 `DSC_SERVER_TYPE` 員，而不是使用字串來設定連接屬 `ServiceClientFactoryProperties` 性。 可使用下列值： `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`、 `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`或 `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`。

* **DSC_CREDENTIAL_USERNAME:** 指定AEM表單使用者名稱。 若要讓使用者成功叫用AEM Forms服務，他們需要「服務使用者」角色。 用戶也可以具有包含「服務調用」權限的其他角色。 否則，當他們嘗試調用服務時會拋出異常。 如果服務安全性被禁用，則無需指定此連接屬性。
* **DSC_CREDENTIAL_PASSWORD:** 指定相應的口令值。 如果服務安全性被禁用，則無需指定此連接屬性。
* **DSC_REQUEST_TIMEOUT:** SOAP請求的預設請求逾時限制為1200000毫秒（20分鐘）。 有時，完成操作的請求可能需要更長的時間。 例如，擷取大量記錄的SOAP請求可能需要較長的逾時限制。 您可以使用 `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` 來增加SOAP請求的請求呼叫逾時限制。

   **注意**:只有基於SOAP的調用支援DSC_REQUEST_TIMEOUT屬性。

要設定連接屬性，請執行以下任務：

1. 使用其 `java.util.Properties` 建構函式建立物件。
1. 若要設定 `DSC_DEFAULT_EJB_ENDPOINT` 連線屬性，請叫用物 `java.util.Properties` 件的方法並 `setProperty` 傳遞下列值：

   * 枚舉 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 值
   * 一個字串值，指定代管AEM Forms的J2EE應用程式伺服器URL
   >[!NOTE]
   >
   >如果您使用SOAP連接模式，請指定枚舉 `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` 值而不是枚舉 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 值。

1. 若要設定 `DSC_TRANSPORT_PROTOCOL` 連線屬性，請叫用物 `java.util.Properties` 件的方法並 `setProperty` 傳遞下列值：

   * 枚舉 `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` 值
   * 枚舉 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 值
   >[!NOTE]
   >
   >如果您使用SOAP連接模式，請指定枚舉 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`值而不是枚舉 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 值。

1. 若要設定 `DSC_SERVER_TYPE` 連線屬性，請叫用物 `java.util.Properties` 件的方法並 `setProperty` 傳遞下列值：

   * 枚舉 `ServiceClientFactoryProperties.DSC_SERVER_TYPE`值
   * 一個字串值，指定主控AEM Forms的J2EE應用程式伺服器(例如，如果AEM Forms部署在JBoss上，請指定 `JBoss`)。

      1. 若要設定 `DSC_CREDENTIAL_USERNAME` 連線屬性，請叫用物 `java.util.Properties` 件的方法並 `setProperty` 傳遞下列值：
   * 枚舉 `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` 值
   * 一個字串值，指定呼叫AEM Forms所需的使用者名稱

      1. 若要設定 `DSC_CREDENTIAL_PASSWORD` 連線屬性，請叫用物 `java.util.Properties` 件的方法並 `setProperty` 傳遞下列值：
   * 枚舉 `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` 值
   * 指定相應口令值的字串值



**設定JBoss的EJB連接模式**

以下Java代碼示例設定連接屬性，以調用部署在JBoss上並使用EJB連接模式的AEM Forms。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**為WebLogic設定EJB連接模式**

下列Java程式碼範例會設定連線屬性，以叫用部署在WebLogic上的AEM Forms，並使用EJB連線模式。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**設定WebSphere的EJB連接模式**

下列Java程式碼範例會設定連線屬性，以叫用部署在WebSphere上的AEM Forms，並使用EJB連線模式。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**設定SOAP連接模式**

以下Java代碼示例在SOAP模式下設定連接屬性，以調用部署在JBoss上的AEM Forms。

```as3
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

以下Java代碼示例設定調用部署在JBoss Application Server上的AEM Forms以及禁用服務安全性時所需的連接屬性。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>與「使用AEM Forms進行程式設計」相關聯的所有Java快速入門都會顯示EJB和SOAP連線設定。

**使用自訂請求逾時限制設定SOAP連線模式**

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**使用內容物件來叫用AEM Forms**

您可以使用物 `com.adobe.idp.Context` 件來與已驗證的使用者叫用AEM Forms服務(該物 `com.adobe.idp.Context` 件代表已驗證的使用者)。 使用對 `com.adobe.idp.Context` 像時，不需要設定或 `DSC_CREDENTIAL_USERNAME` 屬 `DSC_CREDENTIAL_PASSWORD` 性。 您可以使用物 `com.adobe.idp.Context` 件的方法，在驗證使用者時 `AuthenticationManagerServiceClient` 取得物 `authenticate` 件。

該 `authenticate` 方法返回 `AuthResult` 包含驗證結果的對象。 可以通過調用其 `com.adobe.idp.Context` 建構子來建立對象。 然後叫用 `com.adobe.idp.Context` 物件的方 `initPrincipal` 法並傳遞 `AuthResult` 物件，如下列程式碼所示：

```as3
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

您可以叫用物 `DSC_CREDENTIAL_USERNAME` 件的方法並傳遞物件，而不是設 `DSC_CREDENTIAL_PASSWORD` 定或 `ServiceClientFactory``setContext``com.adobe.idp.Context` 屬性。 當使用AEM Forms使用者叫用服務時，請確定他們的角色名 `Services User` 稱為叫用AEM Forms服務所需的角色。

以下代碼示例說明如何在用 `com.adobe.idp.Context` 於建立對象的連接設定中使用對 `EncryptionServiceClient` 像。

```as3
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
>如需驗證使用者的完整詳細資訊，請參閱驗 [證使用者](/help/forms/developing/users.md#authenticating-users)。

### 叫用藍本 {#invoking_scenarios-1}

本節將討論以下調用的情形：

* 在其自己的Java虛擬機器(JVM)中執行的用戶端應用程式會叫用單機版AEM Forms例項。
* 在其JVM中執行的用戶端應用程式會叫用叢集的AEM Forms例項。

### 叫用獨立AEM Forms例項的用戶端應用程式 {#client-application-invoking-a-stand-alone-aem-forms-instance}

下圖顯示在其JVM中執行並叫用獨立AEM Forms例項的用戶端應用程式。

在此案例中，用戶端應用程式會在其專屬的JVM中執行，並叫用AEM Forms服務。

>[!NOTE]
>
>此方案是所有快速啟動都基於的調用方案。

### 用戶端應用程式叫用叢集AEM Forms例項 {#client-application-invoking-clustered-aem-forms-instances}

下圖顯示在自己的JVM中執行並叫用位於叢集中的AEM Forms例項的用戶端應用程式。

此情形類似於呼叫獨立AEM Forms例項的用戶端應用程式。 但是，提供者URL不同。 如果客戶端應用程式要連接到特定的J2EE應用程式伺服器，應用程式必須更改URL以引用特定的J2EE應用程式伺服器。

不建議參考特定的J2EE應用程式伺服器，因為當應用程式伺服器停止時，用戶端應用程式與AEM Forms之間的連線會終止。 建議提供者URL參考儲存格層級的JNDI管理器，而非特定的J2EE應用程式伺服器。

使用SOAP連接模式的客戶端應用程式可以使用群集的HTTP負載平衡器埠。 使用EJB連接模式的客戶端應用程式可以連接到特定J2EE應用程式伺服器的EJB埠。 此操作可處理群集節點之間的負載平衡。

**WebSphere**

下列範例顯示用來連線至部署在WebSphere上的AEM Forms的jndi.properties檔案的內容。

```as3
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

下列範例顯示用來連線至部署在WebLogic上的AEM Forms的jndi.properties檔案的內容。

```as3
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

以下示例顯示用於連接到部署在JBoss上的AEM Forms的jndi.properties檔案的內容。

```as3
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>請洽詢您的管理員以判斷J2EE應用程式伺服器名稱和埠號。

**另請參閱**

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java API將資料傳送至AEM Forms服務](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java API將資料傳送至AEM Forms服務 {#passing-data-to-aem-forms-services-using-the-java-api}

AEM Forms服務作業通常會使用或產生PDF檔案。 當您叫用服務時，有時需要將PDF檔案（或其他檔案類型，例如XML資料）傳遞至服務。 同樣地，有時也需要處理從服務傳回的PDF檔案。 可讓您傳遞資料至AEM Forms服務與資料的Java類別是 `com.adobe.idp.Document`。

AEM Forms服務不接受PDF檔案做為其他資料類型，例如物 `java.io.InputStream` 件或位元組陣列。 物 `com.adobe.idp.Document` 件也可用來將其他類型的資料（例如XML資料）傳遞至服務。

對 `com.adobe.idp.Document` 像是Java可序列化類型，因此可通過RMI調用傳遞。 接收端可以配置（同一主機、同一類載入器）、本地（同一主機、不同類載入器）或遠程（不同主機）。 每個案例都會最佳化檔案內容的傳遞。 例如，如果傳送者和接收者位於同一主機上，則內容會傳遞至本機檔案系統。 （在某些情況下，檔案可以傳入記憶體中。）

根據對 `com.adobe.idp.Document` 像大小，資料會在對象中傳 `com.adobe.idp.Document` 送或儲存在伺服器的檔案系統中。 在被處置時，該對象所佔 `com.adobe.idp.Document` 用的任何臨時儲存資源被自動 `com.adobe.idp.Document` 移除。 (請參 [閱處置文檔對象](invoking-aem-forms-using-java.md#disposing-document-objects)。)

有時，您必須先瞭解物件的內 `com.adobe.idp.Document` 容類型，才能將它傳遞至服務。 例如，如果某個操作需要特定內容類型， `application/pdf`例如，建議您確定內容類型。 (請參 [閱決定檔案的內容類型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)。)

對 `com.adobe.idp.Document` 像嘗試使用提供的資料確定內容類型。 如果無法從提供的資料擷取內容類型（例如，當資料以位元組陣列提供時），請設定內容類型。 若要設定內容類型，請叫 `com.adobe.idp.Document` 用物件的方 `setContentType` 法。 (請參 [閱決定檔案的內容類型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

如果宣傳檔案駐留在同一檔案系統上，建立對象的 `com.adobe.idp.Document` 速度會更快。 如果宣傳檔案駐留在遠程檔案系統上，則必須執行複製操作，這會影響效能。

應用程式可同時包含 `com.adobe.idp.Document` 資料 `org.w3c.dom.Document` 類型。 不過，請確定您完全符合資料 `org.w3c.dom.Document` 類型的資格。 有關將對象轉換為對 `org.w3c.dom.Document` 像的資訊，請 `com.adobe.idp.Document` 參閱快速 [啟動（EJB模式）:使用Java API將可排程的版面預先填入表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)。

>[!NOTE]
>
>為避免在使用物件時WebLogic中發生記憶體洩漏，請 `com.adobe.idp.Document` 以2048位元組或更少的區塊來讀取檔案資訊。 例如，以下代碼以2048位元組的塊讀取文檔資訊：

```as3
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

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 建立檔案 {#creating-documents}

在您叫 `com.adobe.idp.Document` 用需要PDF檔案（或其他檔案類型）作為輸入值的服務操作之前，先建立物件。 該類 `com.adobe.idp.Document` 提供了建構子，可讓您從以下內容類型建立文檔：

* 位元組陣列
* 現有對 `com.adobe.idp.Document` 像
* 物 `java.io.File` 件
* 物 `java.io.InputStream` 件
* 物 `java.net.URL` 件

#### 基於位元組陣列建立文檔 {#creating-a-document-based-on-a-byte-array}

以下代碼示例建立基 `com.adobe.idp.Document` 於位元組陣列的對象。

**建立基於位元組陣列的Document對象**

```as3
 Document myPDFDocument = new Document(myByteArray);
```

#### 基於其他文檔建立文檔 {#creating-a-document-based-on-another-document}

下面的代碼示例建立基 `com.adobe.idp.Document` 於另一個對象的對 `com.adobe.idp.Document` 像。

**建立基於其他文檔的文檔對象**

```as3
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

下列程式碼範例會建 `com.adobe.idp.Document` 立以PDF檔名為 *map.pdf的物件*。 此檔案位於C硬碟的根目錄中。 此建構子嘗試使用檔案副檔名設定對 `com.adobe.idp.Document` 像的MIME內容類型。

接受 `com.adobe.idp.Document` 物件的建構函 `java.io.File` 式也接受布林參數。 通過將此參數設 `true`置為， `com.adobe.idp.Document` 對象將刪除檔案。 此動作表示您不必在將檔案傳遞至建構函式後移除 `com.adobe.idp.Document` 檔案。

將此參數設 `false` 定為表示您保有此檔案的所有權。 將此參數設 `true` 定為更有效率。 原因是對象可 `com.adobe.idp.Document` 以將檔案直接移動到本地管理區，而不是複製檔案（速度較慢）。

**建立以PDF檔案為基礎的Document物件**

```as3
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### 基於InputStream對象建立文檔 {#creating-a-document-based-on-an-inputstream-object}

以下Java代碼示例建立基 `com.adobe.idp.Document` 於對象的對 `java.io.InputStream` 像。

**基於InputStream對象建立文檔**

```as3
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### 根據可從URL存取的內容建立檔案 {#creating-a-document-based-on-content-accessible-from-an-url}

以下Java代碼示例建立 `com.adobe.idp.Document` 基於名為map.pdf的PDF檔案 *的對象*。 此檔案位於執行於的名為Web `WebApp` 應用程式中 `localhost`。 此建構函式會嘗試使 `com.adobe.idp.Document` 用URL通訊協定傳回的內容類型來設定物件的MIME內容類型。

提供給對象的URL `com.adobe.idp.Document` 始終在建立原始對象的一 `com.adobe.idp.Document` 側讀取，如以下示例所示：

```as3
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

c:/temp/input.pdf檔案必須位於用戶端電腦上（而非伺服器電腦上）。 客戶端電腦是讀取URL和建立對象 `com.adobe.idp.Document` 的位置。

**根據可從URL存取的內容建立檔案**

```as3
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 處理傳回的檔案 {#handling-returned-documents}

將PDF檔案（或其他資料類型，例如XML資料）傳回為輸出值的服務作業會傳回 `com.adobe.idp.Document` 物件。 收到物件 `com.adobe.idp.Document` 後，可將其轉換為下列格式：

* 物 `java.io.File` 件
* 物 `java.io.InputStream` 件
* 位元組陣列

以下代碼行將對象 `com.adobe.idp.Document` 轉換為對 `java.io.InputStream` 像。 假設它 `myPDFDocument` 表示對 `com.adobe.idp.Document` 像：

```as3
     java.io.InputStream resultStream = myDocument.getInputStream();
```

同樣地，您也可以執行下列任 `com.adobe.idp.Document` 務，將本機檔案的內容複製：

1. 建立對 `java.io.File` 像。
1. 叫用物 `com.adobe.idp.Document` 件的方 `copyToFile` 法並傳遞物 `java.io.File`件。

下列程式碼範例會將物件的內 `com.adobe.idp.Document` 容複製至名為 *AnotherMap.pdf的檔案*。

**將文檔對象的內容複製到檔案**

```as3
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 確定文檔的內容類型 {#determining-the-content-type-of-a-document}

調用物件的方 `com.adobe.idp.Document` 法，以決定物 `com.adobe.idp.Document` 件的MIME類 `getContentType` 型。 此方法返回指定對象內容類型的字串 `com.adobe.idp.Document` 值。 下表說明AEM Forms傳回的不同內容類型。

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
   <td><p>PDF檔案</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>XML資料封裝(XDP)，用於匯出的XML表單架構(XFA)表單</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>書籤、附件或其他XML檔案</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>表單資料格式(FDF)，用於匯出的Acrobat表單</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML表單資料格式(XFDF)，用於匯出的Acrobat表單</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>多樣化資料格式與XML</p></td>
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

下列程式碼範例會決定物件的內容類 `com.adobe.idp.Document` 型。

**確定Document對象的內容類型**

```as3
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 處置文檔對象 {#disposing-document-objects}

當您不再需要物 `Document` 件時，建議您叫用其方法來處 `dispose` 理。 每個 `Document` 物件會在應用程式的主機平台上使用檔案描述子和高達75 MB的RAM空間。 如果未 `Document` 放置對象，則Java Garage收集過程會將其放置。 但是，通過使用該方法，可以更快 `dispose` 地處理它，從而釋放對象佔用的內 `Document` 存。

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java客戶端庫調用服務 {#invoking-a-service-using-a-java-client-library}

AEM Forms服務作業可使用服務的強式型別API（稱為Java用戶端程式庫）來呼叫。 *Java客戶端庫* (Java client library)是一組具體類，可提供對服務容器中部署的服務的訪問。 您使用調用API實例化表示要調用的服務的Java對 `InvocationRequest` 像，而不是建立對象。 調用API用於調用在Workbench中建立的進程，如長壽命進程。 (請參 [閱叫用以人為中心的長壽流程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。)

要執行服務操作，請調用屬於Java對象的方法。 Java客戶端庫包含通常以服務操作一對一映射的方法。 使用Java客戶端庫時，請設定所需的連接屬性。 (請參 [閱設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。)

設定連線屬性後，請建 `ServiceClientFactory` 立用來執行個體化Java物件的物件，讓您叫用服務。 每個具有Java客戶端庫的服務都有相應的客戶端對象。 例如，要調用Repository服務，請使用其建構子 `ResourceRepositoryClient` 並傳遞對象來建立對 `ServiceClientFactory` 像。 物 `ServiceClientFactory` 件負責維護呼叫AEM Forms服務所需的連線設定。

雖然獲取 `ServiceClientFactory` 的速度通常很快，但在首次使用工廠時，會涉及一些開銷。 此物件已最佳化以供重複使用，因此在建立多個Java用戶端物 `ServiceClientFactory` 件時，請盡可能使用相同的物件。 也就是說，請勿為您建立的每 `ServiceClientFactory` 個用戶端程式庫物件建立個別物件。

「使用者管理員」設定可控制SAML斷言在物件內的存留期，此斷言 `com.adobe.idp.Context` 會影響物件 `ServiceClientFactory` 。 此設定會控制整個AEM Forms中的所有驗證內容期限，包括使用Java API執行的所有呼叫。 依預設，可使用物件的時 `ServiceCleintFactory` 段為2小時。

>[!NOTE]
>
>要說明如何使用Java API調用服務，將調用儲存庫服務 `writeResource` 的操作。 此操作將新資源放入儲存庫。

通過使用Java客戶端庫並執行以下步驟，可以調用儲存庫服務：

1. 在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-repository-client.jar。 如需這些檔案位置的詳細資訊，請參 [閱「包含AEM Forms Java程式庫檔案」](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 設定調用服務所需的連接屬性。
1. 調用物 `ServiceClientFactory` 件的靜態方 `ServiceClientFactory` 法並傳遞包含連線屬性的物 `createInstance` 件，以建立 `java.util.Properties` 物件。
1. 使用其 `ResourceRepositoryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。 使用對 `ResourceRepositoryClient` 像調用儲存庫服務操作。
1. 使用其 `RepositoryInfomodelFactoryBean` 建構函式並傳遞來建立物件 `null`。 此對象允許您建立一 `Resource` 個對象，該對象表示添加到儲存庫的內容。
1. 調用物 `Resource` 件的方法並傳 `RepositoryInfomodelFactoryBean` 遞下列值， `newImage` 以建立物件：

   * 指定唯一的ID值 `new Id()`。
   * 通過指定唯一的UUID值 `new Lid()`。
   * 資源的名稱。 可以指定XDP檔案的檔案名。
   將返回值轉換為 `Resource`。

1. 調用 `ResourceContent` 物件的方法並 `RepositoryInfomodelFactoryBean` 將傳回值 `newImage` 轉換為，以建立物件 `ResourceContent`。 此對象表示添加到儲存庫的內容。
1. 通過傳 `com.adobe.idp.Document` 遞儲存XDP檔案的 `java.io.FileInputStream` 對象以添加到儲存庫來建立對象。 (請參 [閱基於InputStream對象建立文檔](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)。)
1. 調用物件的方 `com.adobe.idp.Document` 法，將物 `ResourceContent` 件的內容新 `ResourceContent` 增至物 `setDataDocument` 件。 傳遞物 `com.adobe.idp.Document` 件。
1. 調用物件的方法並傳遞，以設定要新增至儲存庫的XDP `ResourceContent` 檔案的MIME `setMimeType` 類型 `application/vnd.adobe.xdp+xml`。
1. 調用對象的方 `ResourceContent` 法並傳遞對 `Resource` 像，將對象的內容 `Resource` 添加到對象 `setContent``ResourceContent` 中。
1. 通過調用對象的方法並傳遞 `Resource` 表示資源 `setDescription` 說明的字串值，添加資源說明。
1. 調用物件的方法並傳遞下列值，將表 `ResourceRepositoryClient` 單設計新 `writeResource` 增至儲存庫：

   * 一個字串值，它指定包含新資源的資源集合的路徑
   * 已 `Resource` 建立的對象

**另請參閱**

[快速啟動（EJB模式）:使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 使用調用API調用短期進程 {#invoking-a-short-lived-process-using-the-invocation-api}

您可以使用Java調用API調用短時間進程。 當您使用「呼叫API」叫用短暫的程式時，您會使用物件傳遞必要的參 `java.util.HashMap` 數值。 對於要傳遞至服務的每個參數，請調 `java.util.HashMap` 用物件的方 `put` 法，並指定服務所需的名稱——值對，以執行指定的作業。 指定屬於短期進程的參數的確切名稱。

>[!NOTE]
>
>有關調用長壽命進程的資訊，請參 [閱調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

這裡討論的是使用Invocation API來叫用下列名為的AEM Forms短期程式 `MyApplication/EncryptDocument`。

>[!NOTE]
>
>此程式不以現有的AEM Forms程式為基礎。 要跟隨代碼示例，請使用Workbench建立一個名 `MyApplication/EncryptDocument` 為的流程。 (請參 [閱使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

調用此進程時，它執行以下操作：

1. 取得傳遞至程式的不安全PDF檔案。 此操作基於操 `SetValue` 作。 此進程的輸入參數是名為的 `document` 進程變數 `inDoc`。
1. 使用密碼加密PDF檔案。 此操作基於操 `PasswordEncryptPDF` 作。 密碼加密的PDF檔案會在名為的流程變數中傳回 `outDoc`。

### 使用Java調用API調用MyApplication/EncryptDocument短時進程 {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

使用 `MyApplication/EncryptDocument` Java調用API叫用短期流程：

1. 在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。 (請參 [閱「包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」)。
1. 建立包 `ServiceClientFactory` 含連接屬性的對象。 (請參 [閱設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。)
1. 使用其 `ServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。 對 `ServiceClient` 像可讓您調用服務操作。 它可處理如定位、調度和路由調用請求等任務。
1. 使用其 `java.util.HashMap` 建構函式建立物件。
1. 針對每 `java.util.HashMap` 個輸入參 `put` 數叫用物件的方法，以傳遞至長期的程式。 由於短 `MyApplication/EncryptDocument` 期進程需要一個類型的輸入參數 `Document`，因此只需調用一次 `put` 方法，如以下示例所示。

   ```as3
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. 調用物 `InvocationRequest` 件的方法並傳 `ServiceClientFactory` 遞下列值， `createInvocationRequest` 以建立物件：

   * 一個字串值，它指定要調用的長生命週期進程的名稱。 要調用該 `MyApplication/EncryptDocument` 進程，請指定 `MyApplication/EncryptDocument`。
   * 表示流程操作名稱的字串值。 通常，短期流程操作的名稱為 `invoke`。
   * 包 `java.util.HashMap` 含服務操作所需參數值的對象。
   * 一個布林值，它指 `true`定建立同步請求（此值適用於調用短時間進程）。

1. 調用物件的方法並傳遞物件，以傳 `ServiceClient` 送呼叫請 `invoke` 求至服務 `InvocationRequest` 。 方法 `invoke` 返回對 `InvocationReponse` 像。

   >[!NOTE]
   >
   >通過將值作為方法的第四個參 `false`數傳遞，可以調用長壽命 `createInvocationRequest` 進程。 傳遞值會 `false`*建立非同步請求。*

1. 調用物件的方法並傳遞指定 `InvocationReponse` 輸出參數名 `getOutputParameter` 稱的字串值，以擷取程式的傳回值。 在這種情況下，請指 `outDoc` 定( `outDoc` 是進程的輸出參數的 `MyApplication/EncryptDocument` 名稱)。 將返回值轉換 `Document`為，如下例所示。

   ```as3
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. 建立物 `java.io.File` 件，並確定副檔名為。pdf。
1. 叫用 `com.adobe.idp.Document` 物件的方 `copyToFile` 法，將物件的內容 `com.adobe.idp.Document` 複製至檔案。 請確定您使用 `com.adobe.idp.Document` 方法傳回的物 `getOutputParameter` 件。

**另請參閱**

[快速入門：使用調用API調用短期進程](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)