---
title: 使用JavaAPI叫用AEM Forms
seo-title: Invoking AEM Forms using the JavaAPI
description: 使用AEM Forms Java API for RMI傳輸協定進行遠程調用，使用VM傳輸進行本地調用，使用SOAP進行遠程調用，使用不同的身份驗證，如用戶名和密碼，以及同步和非同步調用請求。
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

# 使用Java API叫用AEM Forms {#invoking-aem-forms-using-the-javaapi}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

AEM Forms可透過使用AEM Forms Java API來叫用。 使用AEM Forms Java API時，您可以使用叫用API或Java用戶端程式庫。 Java用戶端程式庫適用於服務，例如Rights Management服務。 這些強式類型API可讓您開發叫用AEM Forms的Java應用程式。

叫用API是位於 `com.adobe.idp.dsc` 包。 使用這些類，您可以直接將調用請求發送到服務並處理返回的調用響應。 使用叫用API來叫用使用Workbench建立的短期或長期處理程式。

以程式設計方式叫用服務的建議方式，是使用與服務相對應的Java用戶端程式庫，而非叫用API。 例如，要調用加密服務，請使用加密服務客戶端庫。 要執行加密服務操作，請調用屬於加密服務客戶端對象的方法。 您可以叫用以下命令，以密碼加密PDF檔案： `EncryptionServiceClient` 物件 `encryptPDFUsingPassword` 方法。

Java API支援下列功能：

* 用於遠程調用的RMI傳輸協定
* 用於本地調用的VM傳輸
* 遠程調用的SOAP
* 不同的驗證，如用戶名和密碼
* 同步和非同步調用請求

[包含AEM Forms Java程式庫檔案](#including-aem-forms-java-library-files)

[調用以人為中心的長壽命過程](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md)

[設定連接屬性](#setting-connection-properties)

[使用Java API將資料傳遞至AEM Forms服務](#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](#invoking-a-service-using-a-java-client-library)

[使用叫用API叫用短期處理程式](#invoking-a-short-lived-process-using-the-invocation-api)

[建立調用以人為中心的長生命週期過程的Java Web應用程式](/help/forms/developing/invoking-human-centric-long-lived.md)

## 包含AEM Forms Java程式庫檔案 {#including-aem-forms-java-library-files}

要使用Java API以寫程式方式調用AEM Forms服務，請在Java項目的類路徑中包括所需的庫檔案（JAR檔案）。 您在客戶端應用程式的類路徑中包括的JAR檔案取決於以下幾個因素：

* 要叫用的AEM Forms服務。 客戶端應用程式可以調用一個或多個服務。
* 您要叫用AEM Forms服務的模式。 可以使用EJB或SOAP模式。 (請參閱 [設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>（僅交鑰匙）使用命令啟動AEM Forms伺服器 `standalone.bat -b <Server IP> -c lc_turnkey.xml` 為EJB指定伺服器IP

* 部署了AEM Forms的J2EE應用程式伺服器。

### 特定於服務的JAR檔案 {#service-specific-jar-files}

下表列出調用AEM Forms服務所需的JAR檔案。

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
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>必須始終包含在Java客戶端應用程式的類路徑中。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>必須始終包含在Java客戶端應用程式的類路徑中。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk//client-libs/&lt;app server=""&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>調用應用程式管理器服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>調用組合器服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>調用備份和還原服務API時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>叫用條碼式表單服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>叫用轉換PDF服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>叫用Distiller服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>調用DocConverter服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>調用文檔管理服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>調用加密服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>叫用Forms服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>叫用表單資料整合服務所需。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>調用生成PDF服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>調用生成3DPDF服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>調用作業管理器服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>調用輸出服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>調用PDF實用程式或XMP實用程式服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>叫用Acrobat Reader DC擴充功能服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>調用儲存庫服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs\thirdparty</p></td>
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
   <td><p>叫用Rights Management服務時需要。</p><p>如果AEM Forms部署在JBoss上，請納入所有這些檔案。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p><p>JBoss專用的lib目錄</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>調用簽名服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>調用任務管理器服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>調用信任儲存服務所需。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### 連接模式和J2EE應用程式JAR檔案 {#connection-mode-and-j2ee-application-jar-files}

下表列出了取決於連接模式和部署了AEM Forms的J2EE應用程式伺服器的JAR檔案。

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
     <li><p>dom3-xml-api-2.5.0.jar</p> </li>
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
   <td><p>如果使用SOAP模式調用了AEM Forms，請包括這些JAR檔案。</p> </td>
   <td><p>&lt;<em>安裝目錄</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>如果AEM Forms部署在JBoss Application Server上，請包含此JAR檔案。</p> <p>如果jboss-client.jar和引用的jar不是共用的，則類載入器將找不到所需類。</p> </td>
   <td><p>JBoss客戶端庫目錄</p> <p>如果將客戶端應用程式部署在同一個J2EE應用程式伺服器上，則無需包含此檔案。</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>如果AEM Forms部署在BEA WebLogic Server®上，則包括此JAR檔案。</p> </td>
   <td><p>WebLogic特定庫目錄</p> <p>如果將客戶端應用程式部署在同一個J2EE應用程式伺服器上，則無需包含此檔案。</p> </td>
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
   <td><p>WebSphere特定庫目錄(<em>[WAS_HOME]</em>/runtimes)</p> <p>如果將客戶端應用程式部署在同一個J2EE應用程式伺服器上，則無需包括這些檔案。</p> </td>
  </tr>
 </tbody>
</table>

### 叫用方案 {#invoking-scenarios}

下表指定調用方案，並列出了成功調用AEM Forms所需的JAR檔案。

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
   <td><p>Forms服務</p> </td>
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
   <td><p>Forms服務</p> <p>Acrobat Reader DC擴充功能</p> <p>簽名服務</p> </td>
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
   <td><p>Forms服務</p> </td>
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
     <li><p>dom3-xml-api-2.5.0.jar</p> </li>
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
   <td><p>Forms服務</p> <p>Acrobat Reader DC擴充功能</p> <p>簽名服務</p> </td>
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
     <li><p>dom3-xml-api-2.5.0.jar</p> </li>
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

如果您要從LiveCycle升級為AEM Forms，建議您將AEM Forms JAR檔案包含在Java專案的類別路徑中。 例如，如果您使用Rights Management服務等服務，若您的類路徑中未包含AEM Forms JAR檔案，則會遇到相容性問題。

假設您要升級至AEM Forms。 要使用調用Rights Management服務的Java應用程式，請包括以下JAR檔案的AEM Forms版本：

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API將資料傳遞至AEM Forms服務](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 設定連接屬性 {#setting-connection-properties}

使用Java API時，您可以設定連線屬性來叫用AEM Forms。 在設定連接屬性時，指定是遠程還是本地調用服務，還指定連接模式和驗證值。 如果已啟用服務安全性，則需要驗證值。 但是，如果禁用了服務安全性，則無需指定驗證值。

連接模式可以是SOAP模式或EJB模式。 EJB模式使用RMI/IIOP協定，EJB模式的效能比SOAP模式的效能好。 SOAP模式用於消除J2EE應用程式伺服器依賴性，或當防火牆位於AEM Forms和客戶端應用程式之間時。 SOAP模式使用https協定作為基礎傳輸，並可跨防火牆邊界通信。 如果J2EE應用程式伺服器依賴關係或防火牆均不是問題，則建議使用EJB模式。

若要成功叫用AEM Forms服務，請設定下列連線屬性：

* **DSC_DEFAULT_EJB_ENDPOINT:** 如果使用EJB連接模式，則此值表示部署了AEM Forms的J2EE應用程式伺服器的URL。 要遠程調用AEM Forms，請指定部署了AEM Forms的J2EE應用程式伺服器名稱。 如果您的客戶端應用程式位於相同的J2EE應用程式伺服器上，則可以指定 `localhost`. 根據部署了哪些J2EE應用程式伺服器AEM Forms，指定以下值之一：

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**:如果您使用SOAP連接模式，此值表示將調用請求發送到的端點。 要遠程調用AEM Forms，請指定部署了AEM Forms的J2EE應用程式伺服器名稱。 如果您的客戶端應用程式位於同一個J2EE應用程式伺服器上，則可以指定 `localhost` (例如， `http://localhost:8080`.)

   * 埠值 `8080` 若J2EE應用程式為JBoss，則適用。 如果J2EE應用程式伺服器是IBM® WebSphere®，請使用埠 `9080`. 同樣，如果J2EE應用程式伺服器是WebLogic，請使用埠 `7001`. (這些值是預設埠值。 如果更改埠值，請使用適用的埠號。)

* **DSC_TRANSPORT_PROTOCOL**:如果使用EJB連接模式，請指定 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 的值。 如果使用SOAP連接模式，請指定 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**:指定部署了AEM Forms的J2EE應用程式伺服器。 有效值為 `JBoss`, `WebSphere`, `WebLogic`.

   * 如果將此連接屬性設定為 `WebSphere`, `java.naming.factory.initial` 值設為 `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * 如果將此連接屬性設定為 `WebLogic`, `java.naming.factory.initial` 值設為 `weblogic.jndi.WLInitialContextFactory`.
   * 同樣地，如果將此連接屬性設定為 `JBoss`, `java.naming.factory.initial` 值設為 `org.jnp.interfaces.NamingContextFactory`.
   * 您可以設定 `java.naming.factory.initial` 屬性，以取得符合您要求的值（如果您不想使用預設值）。

   >[!NOTE]
   >
   >而非使用字串來設定 `DSC_SERVER_TYPE` connection屬性，您可以使用 `ServiceClientFactoryProperties` 類別。 可使用下列值： `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`，或 `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** 指定AEM表單使用者名稱。 若要讓使用者成功叫用AEM Forms服務，他們需要「服務使用者」角色。 用戶也可以具有包含服務調用權限的其他角色。 否則，當它們嘗試調用服務時會引發異常。 如果禁用了服務安全，則無需指定此連接屬性。
* **DSC_CREDENTIAL_PASSWORD:** 指定相應的密碼值。 如果禁用了服務安全，則無需指定此連接屬性。
* **DSC_REQUEST_TIMEOUT:** SOAP請求的預設請求超時限制為1200000毫秒（20分鐘）。 某個時候，請求完成操作可能需要較長的時間。 例如，擷取大量記錄的SOAP請求可能需要較長的逾時限制。 您可以使用 `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` 以增加SOAP請求的請求呼叫逾時限制。

   **附註**:只有基於SOAP的調用支援DSC_REQUEST_TIMEOUT屬性。

要設定連接屬性，請執行以下任務：

1. 建立 `java.util.Properties` 物件，使用其建構子。
1. 若要設定 `DSC_DEFAULT_EJB_ENDPOINT` 連接屬性，調用 `java.util.Properties` 物件 `setProperty` 方法，並傳遞下列值：

   * 此 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 枚舉值
   * 指定承載AEM Forms之J2EE應用程式伺服器URL的字串值

   >[!NOTE]
   >
   >如果您使用SOAP連接模式，請指定 `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` 分項清單值，而非 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 枚舉值。

1. 若要設定 `DSC_TRANSPORT_PROTOCOL` 連接屬性，調用 `java.util.Properties` 物件 `setProperty` 方法，並傳遞下列值：

   * 此 `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` 枚舉值
   * 此 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 枚舉值

   >[!NOTE]
   >
   >如果您使用SOAP連接模式，請指定 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`分項清單值，而非 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 枚舉值。

1. 若要設定 `DSC_SERVER_TYPE` 連接屬性，調用 `java.util.Properties` 物件 `setProperty` 方法，並傳遞下列值：

   * 此 `ServiceClientFactoryProperties.DSC_SERVER_TYPE`枚舉值
   * 指定托管AEM Forms的J2EE應用程式伺服器的字串值(例如，如果已在JBoss上部署AEM Forms，請指定 `JBoss`)。

      1. 若要設定 `DSC_CREDENTIAL_USERNAME` 連接屬性，調用 `java.util.Properties` 物件 `setProperty` 方法，並傳遞下列值：
   * 此 `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` 枚舉值
   * 字串值，指定叫用AEM Forms所需的使用者名稱

      1. 若要設定 `DSC_CREDENTIAL_PASSWORD` 連接屬性，調用 `java.util.Properties` 物件 `setProperty` 方法，並傳遞下列值：
   * 此 `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` 枚舉值
   * 指定相應密碼值的字串值



**為JBoss設定EJB連接模式**

以下Java代碼示例設定連接屬性，以調用部署在JBoss上的AEM Forms並使用EJB連接模式。

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

以下Java代碼示例設定連接屬性，以調用部署在WebLogic上的AEM Forms並使用EJB連接模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**設定WebSphere的EJB連接模式**

以下Java代碼示例設定連接屬性，以調用部署在WebSphere上的AEM Forms並使用EJB連接模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**設定SOAP連接模式**

以下Java代碼示例在SOAP模式下設定連接屬性，以調用部署在JBoss上的AEM Forms。

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

**在禁用服務安全時設定連接屬性**

以下Java代碼示例設定調用部署在JBoss Application Server上的AEM Forms以及禁用服務安全時所需的連接屬性。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>與「寫程式」與「AEM Forms」關聯的所有Java快速入門都顯示EJB和SOAP連接設定。

**使用自訂請求逾時限制設定SOAP連線模式**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**使用內容物件叫用AEM Forms**

您可以使用 `com.adobe.idp.Context` 物件以向已驗證的使用者叫用AEM Forms服務( `com.adobe.idp.Context` 物件代表已驗證的使用者)。 使用 `com.adobe.idp.Context` 物件，您不需要設定 `DSC_CREDENTIAL_USERNAME` 或 `DSC_CREDENTIAL_PASSWORD` 屬性。 您可以取得 `com.adobe.idp.Context` 對象 `AuthenticationManagerServiceClient` 物件 `authenticate` 方法。

此 `authenticate` 方法傳回 `AuthResult` 包含驗證結果的物件。 您可以建立 `com.adobe.idp.Context` 對象，方法是調用其建構子。 然後叫用 `com.adobe.idp.Context` 物件 `initPrincipal` 方法並傳遞 `AuthResult` 物件，如下列程式碼所示：

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

而非設定 `DSC_CREDENTIAL_USERNAME` 或 `DSC_CREDENTIAL_PASSWORD` 屬性，您可以叫用 `ServiceClientFactory` 物件 `setContext` 方法並傳遞 `com.adobe.idp.Context` 物件。 使用AEM表單使用者叫用服務時，請確定他們的角色為 `Services User` 叫用AEM Forms服務時所需的URL。

下列程式碼範例說明如何使用 `com.adobe.idp.Context` 連接設定內用於建立的對象 `EncryptionServiceClient` 物件。

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
>如需驗證使用者的完整詳細資訊，請參閱 [驗證使用者](/help/forms/developing/users.md#authenticating-users).

### 叫用方案 {#invoking_scenarios-1}

本節將討論以下叫用的情況：

* 在自己的Java虛擬機(JVM)中運行的客戶端應用程式調用獨立的AEM Forms實例。
* 在自己的JVM中運行的客戶端應用程式調用群集的AEM Forms實例。

### 叫用獨立AEM Forms例項的用戶端應用程式 {#client-application-invoking-a-stand-alone-aem-forms-instance}

下圖顯示在其JVM中執行並叫用獨立AEM Forms例項的用戶端應用程式。

在此情況下，客戶端應用程式在其自己的JVM中運行，並調用AEM Forms服務。

>[!NOTE]
>
>此情境是調用所有快速啟動的基礎情形。

### 客戶端應用程式調用群集AEM Forms實例 {#client-application-invoking-clustered-aem-forms-instances}

下圖顯示在自己的JVM中運行並調用群集中的AEM Forms實例的客戶端應用程式。

此情境類似於叫用獨立AEM Forms例項的用戶端應用程式。 但提供者URL不同。 如果客戶端應用程式要連接到特定的J2EE應用程式伺服器，應用程式必須更改URL以引用特定的J2EE應用程式伺服器。

不建議參考特定的J2EE應用程式伺服器，因為如果應用程式伺服器停止，客戶端應用程式與AEM Forms之間的連接將終止。 建議提供程式URL引用單元級JNDI管理器，而不是特定的J2EE應用程式伺服器。

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

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java API將資料傳遞至AEM Forms服務](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java API將資料傳遞至AEM Forms服務 {#passing-data-to-aem-forms-services-using-the-java-api}

AEM Forms服務作業通常會使用或產生PDF檔案。 叫用服務時，有時需要將PDF檔案（或其他檔案類型，如XML資料）傳遞至服務。 同樣，有時也需要處理從服務傳回的PDF檔案。 可讓您將資料傳遞至AEM Forms服務及從Java類別為 `com.adobe.idp.Document`.

AEM Forms服務不接受PDF檔案作為其他資料類型，例如 `java.io.InputStream` 物件或位元組陣列。 A `com.adobe.idp.Document` 物件也可用來將其他類型的資料（例如XML資料）傳遞至服務。

A `com.adobe.idp.Document` 對象是Java可序列化的類型，因此可通過RMI調用傳遞。 接收方可以配置（同一主機、同一類載入器）、本地（同一主機、不同類載入器）或遠程（不同主機）。 針對每個案例最佳化檔案內容的傳遞。 例如，如果傳送者和接收者位於相同的主機上，則內容會透過本機檔案系統傳遞。 （在某些情況下，檔案可以傳入記憶體。）

視 `com.adobe.idp.Document` 物件大小，則會在 `com.adobe.idp.Document` 對象或儲存在伺服器的檔案系統上。 由 `com.adobe.idp.Document` 物件會在 `com.adobe.idp.Document` 處置。 (請參閱 [處理文檔對象](invoking-aem-forms-using-java.md#disposing-document-objects).)

有時需要知道 `com.adobe.idp.Document` 物件，才能將其傳遞至服務。 例如，如果操作需要特定內容類型，例如 `application/pdf`，建議您判斷內容類型。 (請參閱 [確定文檔的內容類型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

此 `com.adobe.idp.Document` 物件會嘗試使用提供的資料來判斷內容類型。 如果無法從提供的資料中檢索內容類型（例如，當資料以位元組陣列形式提供時），請設定內容類型。 若要設定內容類型，請叫用 `com.adobe.idp.Document` 物件 `setContentType` 方法。 (請參閱 [確定文檔的內容類型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

如果宣傳資料檔案位於同一檔案系統上，請建立 `com.adobe.idp.Document` 物件速度更快。 如果宣傳資料檔案位於遠程檔案系統上，則必須執行複製操作，這會影響效能。

應用程式可包含兩者 `com.adobe.idp.Document` 和 `org.w3c.dom.Document` 資料類型。 不過，請確定您完全符合 `org.w3c.dom.Document` 資料類型。 如需轉換 `org.w3c.dom.Document` 對象 `com.adobe.idp.Document` 對象，請參見 [快速入門（EJB模式）:使用Java API以可流式配置預填Forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>使用 `com.adobe.idp.Document` 對象，以2048位元組或更少的塊讀取文檔資訊。 例如，以下代碼以2048位元組的塊讀取文檔資訊：

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

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 建立文檔 {#creating-documents}

建立 `com.adobe.idp.Document` 在調用需要PDF文檔（或其他文檔類型）作為輸入值的服務操作之前，對象。 此 `com.adobe.idp.Document` 類提供了建構子，使您能夠從以下內容類型中建立文檔：

* 位元組陣列
* 現有 `com.adobe.idp.Document` 物件
* A `java.io.File` 物件
* A `java.io.InputStream` 物件
* A `java.net.URL` 物件

#### 根據位元組陣列建立文檔 {#creating-a-document-based-on-a-byte-array}

下列程式碼範例會建立 `com.adobe.idp.Document` 基於位元組陣列的對象。

**建立基於位元組陣列的文檔對象**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### 根據其他文檔建立文檔 {#creating-a-document-based-on-another-document}

下列程式碼範例會建立 `com.adobe.idp.Document` 以其他 `com.adobe.idp.Document` 物件。

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

#### 根據檔案建立文檔 {#creating-a-document-based-on-a-file}

下列程式碼範例會建立 `com.adobe.idp.Document` 以名為的PDF檔案為基礎的物件 *map.pdf*. 此檔案位於C硬碟的根目錄中。 此建構函式會嘗試設定 `com.adobe.idp.Document` 物件，使用副檔名。

此 `com.adobe.idp.Document` 接受的建構子 `java.io.File` 物件也接受布林值參數。 將此參數設為 `true`, `com.adobe.idp.Document` 物件會刪除檔案。 此動作表示您不必在將檔案傳遞至 `com.adobe.idp.Document` 建構子。

將此參數設為 `false` 表示您保留此檔案的所有權。 將此參數設為 `true` 效率更高。 原因是 `com.adobe.idp.Document` 對象可以將檔案直接移動到本地管理區域，而不是複製它（速度較慢）。

**建立基於PDF檔案的文檔對象**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### 根據InputStream對象建立文檔 {#creating-a-document-based-on-an-inputstream-object}

下列Java程式碼範例會建立 `com.adobe.idp.Document` 以 `java.io.InputStream` 物件。

**根據InputStream對象建立文檔**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### 根據可從URL存取的內容建立檔案 {#creating-a-document-based-on-content-accessible-from-an-url}

下列Java程式碼範例會建立 `com.adobe.idp.Document` 以名為的PDF檔案為基礎的物件 *map.pdf*. 此檔案位於名為的Web應用程式中 `WebApp` 正在運行 `localhost`. 此建構子會嘗試將 `com.adobe.idp.Document` 物件的MIME內容類型，使用隨URL通訊協定傳回的內容類型。

提供給 `com.adobe.idp.Document` 在原始 `com.adobe.idp.Document` 物件已建立，如以下範例所示：

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

c:/temp/input.pdf檔案必須位於客戶端電腦上（而不是伺服器電腦上）。 用戶端電腦是讀取URL的位置，以及 `com.adobe.idp.Document` 對象已建立。

**根據可從URL存取的內容建立檔案**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 處理返回的文檔 {#handling-returned-documents}

將PDF文檔（或其他資料類型，如XML資料）作為輸出值返回的服務操作將返回 `com.adobe.idp.Document` 物件。 在您收到 `com.adobe.idp.Document` 物件，您可將其轉換為下列格式：

* A `java.io.File` 物件
* A `java.io.InputStream` 物件
* 位元組陣列

下列一行程式碼會轉換 `com.adobe.idp.Document` 對象 `java.io.InputStream` 物件。 假設 `myPDFDocument` 代表a `com.adobe.idp.Document` 物件：

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

同樣地，您也可以複製 `com.adobe.idp.Document` 執行下列工作，將檔案重新命名為本機檔案：

1. 建立 `java.io.File` 物件。
1. 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 方法並傳遞 `java.io.File`物件。

下列程式碼範例會複製 `com.adobe.idp.Document` 對象為 *AnotherMap.pdf*.

**將文檔對象的內容複製到檔案**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 確定文檔的內容類型 {#determining-the-content-type-of-a-document}

決定的MIME類型 `com.adobe.idp.Document` 對象，方法是調用 `com.adobe.idp.Document` 物件 `getContentType` 方法。 此方法會傳回字串值，指定 `com.adobe.idp.Document` 物件。 下表說明AEM Forms傳回的不同內容類型。

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
   <td><p>XML資料封裝(XDP)，用於匯出的XML Forms架構(XFA)表單</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>書籤、附件或其他XML文檔</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Forms資料格式(FDF)，用於匯出的Acrobat表單</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML Forms資料格式(XFDF)，用於匯出Acrobat表單</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>豐富資料格式和XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>一般資料格式</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>未指定的MIME類型</p></td>
  </tr>
 </tbody>
</table>

下列程式碼範例會判斷 `com.adobe.idp.Document` 物件。

**確定文檔對象的內容類型**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 處理文檔對象 {#disposing-document-objects}

當您不再需要 `Document` 對象，建議您通過調用其 `dispose` 方法。 每個 `Document` 對象佔用應用程式的主機平台上的檔案描述符和多達75 MB的RAM空間。 若 `Document` 對象未處理，則Java Garage收集過程會處理它。 不過，使用 `dispose` 方法，您可以釋放 `Document` 物件。

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java客戶端庫調用服務 {#invoking-a-service-using-a-java-client-library}

AEM Forms服務作業可透過服務的強制類型API來叫用，此API稱為Java用戶端程式庫。 A *Java客戶端庫* 是一組具體類，可提供對服務容器中部署的服務的訪問。 將代表服務的Java物件實例化以叫用，而非建立 `InvocationRequest` 物件（使用叫用API）。 叫用API可用來叫用在Workbench中建立的程式，例如長期使用的程式。 (請參閱 [調用以人為中心的長壽命過程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

要執行服務操作，請調用屬於Java對象的方法。 Java用戶端程式庫包含通常會將一對一與服務操作對應的方法。 使用Java客戶端庫時，請設定所需的連接屬性。 (請參閱 [設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties).)

設定連線屬性後，請建立 `ServiceClientFactory` 用於實例化Java對象的對象，它允許您調用服務。 每個具有Java客戶端庫的服務都有相應的客戶端對象。 例如，要調用儲存庫服務，請建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。 此 `ServiceClientFactory` 物件負責維護叫用AEM Forms服務所需的連線設定。

雖然已取得 `ServiceClientFactory` 通常速度很快，當首次使用工廠時，會涉及一些開銷。 此對象經過優化以便重複使用，因此，如果可能，請使用 `ServiceClientFactory` 對象。 也就是說，請勿建立個別 `ServiceClientFactory` 您建立的每個用戶端程式庫物件的物件。

有一個「使用者管理員」設定，可控制位於 `com.adobe.idp.Context` 影響 `ServiceClientFactory` 物件。 此設定會控制整個AEM Forms中的所有驗證內容存留期，包括使用Java API執行的所有叫用。 依預設， `ServiceCleintFactory` 物件的使用時間為2小時。

>[!NOTE]
>
>若要說明如何使用Java API叫用服務，請參閱 `writeResource` 叫用操作。 此操作會將新資源放入儲存庫。

您可以使用Java客戶端庫並執行以下步驟來調用儲存庫服務：

1. 在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-repository-client.jar。 如需這些檔案的位置資訊，請參閱 [包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. 設定調用服務所需的連接屬性。
1. 建立 `ServiceClientFactory` 對象，方法是調用 `ServiceClientFactory` 對象的靜態 `createInstance` 方法和傳遞 `java.util.Properties` 包含連接屬性的對象。
1. 建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。 使用 `ResourceRepositoryClient` 對象，以調用儲存庫服務操作。
1. 建立 `RepositoryInfomodelFactoryBean` 使用其建構子來對象 `null`. 此物件可讓您建立 `Resource` 代表新增至存放庫之內容的物件。
1. 建立 `Resource` 對象，方法是調用 `RepositoryInfomodelFactoryBean` 物件 `newImage` 方法並傳遞下列值：

   * 唯一ID值，需指定 `new Id()`.
   * 唯一UUID值，需指定 `new Lid()`.
   * 資源的名稱。 您可以指定XDP檔案的檔案名。

   將傳回值轉換為 `Resource`.

1. 建立 `ResourceContent` 對象，方法是調用 `RepositoryInfomodelFactoryBean` 物件 `newImage` 將返回值轉換為 `ResourceContent`. 此物件代表新增至存放庫的內容。
1. 建立 `com.adobe.idp.Document` 物件，透過傳遞 `java.io.FileInputStream` 儲存要新增至存放庫之XDP檔案的物件。 (請參閱 [根據InputStream對象建立文檔](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. 新增 `com.adobe.idp.Document` 物件 `ResourceContent` 對象，方法是調用 `ResourceContent` 物件 `setDataDocument` 方法。 傳遞 `com.adobe.idp.Document` 物件。
1. 叫用 `ResourceContent` 物件 `setMimeType` 方法與傳遞 `application/vnd.adobe.xdp+xml`.
1. 新增 `ResourceContent` 物件 `Resource` 對象，方法是調用 `Resource` 物件s `setContent` 方法和傳遞 `ResourceContent` 物件。
1. 叫用 `Resource` 物件s `setDescription` 方法，並傳遞代表資源說明的字串值。
1. 叫用 `ResourceRepositoryClient` 物件 `writeResource` 方法並傳遞下列值：

   * 一個字串值，它指定包含新資源的資源集合的路徑
   * 此 `Resource` 建立的對象

**另請參閱**

[快速入門（EJB模式）:使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 使用叫用API叫用短期處理程式 {#invoking-a-short-lived-process-using-the-invocation-api}

您可以使用Java調用API調用短期進程。 當您使用叫用API叫用短期處理程式時，請使用 `java.util.HashMap` 物件。 對於要傳遞至服務的每個參數，請叫用 `java.util.HashMap` 物件 `put` 方法，並指定服務執行指定操作所需的名稱值組。 指定屬於短期進程的參數的確切名稱。

>[!NOTE]
>
>有關調用長期進程的資訊，請參見 [調用以人為中心的長壽命過程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

這裡討論的是使用叫用API來叫用下列名為的AEM Forms短期處理程式 `MyApplication/EncryptDocument`.

>[!NOTE]
>
>此程式並非以現有的AEM Forms程式為基礎。 若要遵循程式碼範例，請建立以下程式： `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

叫用此程式時，會執行下列動作：

1. 獲取傳遞至流程的不安全PDF文檔。 此動作以 `SetValue` 操作。 此程式的輸入參數為 `document` 進程變數已命名 `inDoc`.
1. 使用密碼加密PDF文檔。 此動作以 `PasswordEncryptPDF` 操作。 密碼加密的PDF文檔在名為的進程變數中返回 `outDoc`.

### 使用Java調用API調用MyApplication/EncryptDocument短期進程 {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

叫用 `MyApplication/EncryptDocument` 使用Java調用API的短期過程：

1. 在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。 (請參閱 [包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. 建立 `ServiceClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。 A `ServiceClient` 物件可讓您叫用服務操作。 它處理諸如查找、調度和路由調用請求等任務。
1. 建立 `java.util.HashMap` 物件，使用其建構子。
1. 叫用 `java.util.HashMap` 物件 `put` 方法，將每個輸入參數傳遞至長期處理。 因為 `MyApplication/EncryptDocument` 短期過程需要一個類型的輸入參數 `Document`，您只需叫用 `put` 方法一次，如下列範例所示。

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. 建立 `InvocationRequest` 對象，方法是調用 `ServiceClientFactory` 物件 `createInvocationRequest` 方法並傳遞下列值：

   * 一個字串值，它指定要調用的長期進程的名稱。 叫用 `MyApplication/EncryptDocument` 進程，指定 `MyApplication/EncryptDocument`.
   * 表示流程操作名稱的字串值。 短期流程操作的名稱通常為 `invoke`.
   * 此 `java.util.HashMap` 包含服務操作所需參數值的對象。
   * 一個布爾值，它指定 `true`，會建立同步請求（此值適用於叫用短期處理程式）。

1. 叫用 `ServiceClient` 物件 `invoke` 方法和傳遞 `InvocationRequest` 物件。 此 `invoke` 方法傳回 `InvocationReponse` 物件。

   >[!NOTE]
   >
   >傳遞值可叫用長期的程式 `false`作為 `createInvocationRequest` 方法。 傳遞值 `false`*建立非同步請求。*

1. 叫用 `InvocationReponse` 物件 `getOutputParameter` 方法，並傳遞指定輸出參數名稱的字串值。 在此情況下，請指定 `outDoc` ( `outDoc` 是 `MyApplication/EncryptDocument` 程式)。 將傳回值轉換為 `Document`，如下列範例所示。

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. 建立 `java.io.File` 物件，並確定副檔名為.pdf。
1. 叫用 `com.adobe.idp.Document` 物件 `copyToFile` 複製內容的方法 `com.adobe.idp.Document` 物件。 請確定您使用 `com.adobe.idp.Document` 由傳回的物件 `getOutputParameter` 方法。

**另請參閱**

[快速入門：使用叫用API叫用短期處理程式](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[調用以人為中心的長壽命過程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
