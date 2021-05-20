---
title: 使用JavaAPI叫用AEM Forms
seo-title: 使用JavaAPI叫用AEM Forms
description: 使用AEM Forms Java API for RMI傳輸協定進行遠程調用，使用VM傳輸進行本地調用，使用SOAP進行遠程調用，使用不同的身份驗證，如用戶名和密碼，以及同步和非同步調用請求。
seo-description: 使用AEM Forms Java API for RMI傳輸協定進行遠程調用，使用VM傳輸進行本地調用，使用SOAP進行遠程調用，使用不同的身份驗證，如用戶名和密碼，以及同步和非同步調用請求。
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '5494'
ht-degree: 0%

---

# 使用Java API {#invoking-aem-forms-using-the-javaapi}叫用AEM Forms

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

AEM Forms可透過使用AEM Forms Java API來叫用。 使用AEM Forms Java API時，您可以使用叫用API或Java用戶端程式庫。 Java用戶端程式庫適用於服務，例如Rights Management服務。 這些強式類型API可讓您開發叫用AEM Forms的Java應用程式。

調用API是位於`com.adobe.idp.dsc`包中的類。 使用這些類，您可以直接將調用請求發送到服務並處理返回的調用響應。 使用叫用API來叫用使用Workbench建立的短期或長期處理程式。

以程式設計方式叫用服務的建議方式，是使用與服務相對應的Java用戶端程式庫，而非叫用API。 例如，要調用加密服務，請使用加密服務客戶端庫。 要執行加密服務操作，請調用屬於加密服務客戶端對象的方法。 您可以叫用`EncryptionServiceClient`物件的`encryptPDFUsingPassword`方法，以密碼加密PDF檔案。

Java API支援下列功能：

* 用於遠程調用的RMI傳輸協定
* 用於本地調用的VM傳輸
* 遠程調用的SOAP
* 不同的驗證，如用戶名和密碼
* 同步和非同步調用請求

**Adobe開發人員網站**

「Adobe開發人員」網站包含下列文章，討論如何使用Java API叫用AEM Forms服務：

[使用Java servlet叫用AEM Forms程式](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[從Java叫用AEM Forms Distiller API](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**另請參閱**

[包含AEM Forms Java程式庫檔案](#including-aem-forms-java-library-files)

[調用以人為中心的長壽命過程](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md)

[設定連接屬性](#setting-connection-properties)

[使用Java API將資料傳遞至AEM Forms服務](#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客戶端庫調用服務](#invoking-a-service-using-a-java-client-library)

[使用叫用API叫用短期處理程式](#invoking-a-short-lived-process-using-the-invocation-api)

[建立調用以人為中心的長生命週期過程的Java Web應用程式](/help/forms/developing/invoking-human-centric-long-lived.md)

## 包含AEM Forms Java庫檔案{#including-aem-forms-java-library-files}

要使用Java API以寫程式方式調用AEM Forms服務，請在Java項目的類路徑中包括所需的庫檔案（JAR檔案）。 您在客戶端應用程式的類路徑中包括的JAR檔案取決於以下幾個因素：

* 要叫用的AEM Forms服務。 客戶端應用程式可以調用一個或多個服務。
* 您要叫用AEM Forms服務的模式。 可以使用EJB或SOAP模式。 （請參閱[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。）

>[!NOTE]
>
>（僅交鑰匙）使用`standalone.bat -b <Server IP> -c lc_turnkey.xml`命令啟動AEM Forms伺服器，以指定EJB的伺服器IP

* 部署了AEM Forms的J2EE應用程式伺服器。

### 服務特定JAR檔案{#service-specific-jar-files}

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
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>必須始終包含在Java客戶端應用程式的類路徑中。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>必須始終包含在Java客戶端應用程式的類路徑中。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk//client-libs/&lt;app server=""&gt;<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>調用應用程式管理器服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>調用組合器服務時需要。 </p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>調用備份和還原服務API時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>叫用條碼式表單服務時需要。 </p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>叫用轉換PDF服務時需要。 </p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>叫用Distiller服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>調用DocConverter服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>調用文檔管理服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>調用加密服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>叫用Forms服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>叫用表單資料整合服務所需。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>叫用產生PDF服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>調用生成3D PDF服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>調用作業管理器服務時需要。 </p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>調用輸出服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>叫用PDF公用程式或XMP公用程式服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>叫用Acrobat Reader DC擴充功能服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>調用儲存庫服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs\thirdparty<i></i></p></td>
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
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p><p>JBoss專用的lib目錄</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>調用簽名服務時需要。</p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>調用任務管理器服務時需要。 </p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>調用信任儲存服務所需。 </p></td>
   <td><p>&lt;&gt;安裝目錄</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
 </tbody>
</table>

### 連接模式和J2EE應用程式JAR檔案{#connection-mode-and-j2ee-application-jar-files}

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
   <td><p>&lt;&gt;安裝目錄</em>&gt;/sdk/client-libs/thirdparty<em></em></p> </td>
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
   <td><p>WebSphere特定的lib目錄(<em>[WAS_HOME]</em>/runtimes)</p> <p>如果將客戶端應用程式部署在同一個J2EE應用程式伺服器上，則無需包括這些檔案。</p> </td>
  </tr>
 </tbody>
</table>

### 調用方案{#invoking-scenarios}

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

### 升級JAR檔案{#upgrading-jar-files}

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

## 設定連接屬性{#setting-connection-properties}

使用Java API時，您可以設定連線屬性來叫用AEM Forms。 在設定連接屬性時，指定是遠程還是本地調用服務，還指定連接模式和驗證值。 如果已啟用服務安全性，則需要驗證值。 但是，如果禁用了服務安全性，則無需指定驗證值。

連接模式可以是SOAP模式或EJB模式。 EJB模式使用RMI/IIOP協定，EJB模式的效能比SOAP模式的效能好。 SOAP模式用於消除J2EE應用程式伺服器依賴性，或當防火牆位於AEM Forms和客戶端應用程式之間時。 SOAP模式使用https協定作為基礎傳輸，並可跨防火牆邊界通信。 如果J2EE應用程式伺服器依賴關係或防火牆均不是問題，則建議使用EJB模式。

若要成功叫用AEM Forms服務，請設定下列連線屬性：

* **DSC_DEFAULT_EJB_ENDPOINT:** 如果使用EJB連接模式，則此值表示部署了AEM Forms的J2EE應用程式伺服器的URL。要遠程調用AEM Forms，請指定部署了AEM Forms的J2EE應用程式伺服器名稱。 如果您的客戶端應用程式位於相同的J2EE應用程式伺服器上，則可以指定`localhost`。 根據部署了哪些J2EE應用程式伺服器AEM Forms，指定以下值之一：

   * JBoss:`https://<ServerName>:8080 (default port)`
   * WebSphere:`iiop://<ServerName>:2809 (default port)`
   * WebLogic:`t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**:如果您使用SOAP連接模式，此值表示將調用請求發送到的端點。要遠程調用AEM Forms，請指定部署了AEM Forms的J2EE應用程式伺服器名稱。 如果您的客戶端應用程式位於相同的J2EE應用程式伺服器上，則可以指定`localhost`（例如`http://localhost:8080`）。

   * 如果J2EE應用程式為JBoss，則埠值`8080`適用。 如果J2EE應用程式伺服器是IBM® WebSphere®，請使用埠`9080`。 同樣，如果J2EE應用程式伺服器是WebLogic，請使用埠`7001`。 (這些值是預設埠值。 如果更改埠值，請使用適用的埠號。)

* **DSC_TRANSPORT_PROTOCOL**:如果使用EJB連接模式，請為 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 此值指定。如果使用SOAP連接模式，請指定`ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`。
* **DSC_SERVER_TYPE**:指定部署了AEM Forms的J2EE應用程式伺服器。有效值為`JBoss`、`WebSphere`、`WebLogic`。

   * 如果將此連接屬性設定為`WebSphere`，則`java.naming.factory.initial`值將設定為`com.ibm.ws.naming.util.WsnInitCtxFactory`。
   * 如果將此連接屬性設定為`WebLogic`，則`java.naming.factory.initial`值將設定為`weblogic.jndi.WLInitialContextFactory`。
   * 同樣，如果將此連接屬性設定為`JBoss`，則`java.naming.factory.initial`值將設定為`org.jnp.interfaces.NamingContextFactory`。
   * 如果您不想使用預設值，可以將`java.naming.factory.initial`屬性設定為符合您要求的值。

   >[!NOTE]
   >
   >您可以使用`ServiceClientFactoryProperties`類的靜態成員，而不使用字串來設定`DSC_SERVER_TYPE`連接屬性。 可使用下列值：`ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`、`ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`或`ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`。

* **DSC_CREDENTIAL_USERNAME:** 指定AEM表單使用者名稱。若要讓使用者成功叫用AEM Forms服務，他們需要「服務使用者」角色。 用戶也可以具有包含服務調用權限的其他角色。 否則，當它們嘗試調用服務時會引發異常。 如果禁用了服務安全，則無需指定此連接屬性。
* **DSC_CREDENTIAL_PASSWORD:** 指定對應的密碼值。如果禁用了服務安全，則無需指定此連接屬性。
* **DSC_REQUEST_TIMEOUT:** SOAP請求的預設請求逾時限制為1200000毫秒（20分鐘）。某個時候，請求完成操作可能需要較長的時間。 例如，擷取大量記錄的SOAP請求可能需要較長的逾時限制。 您可以使用`ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT`來增加SOAP請求的請求呼叫逾時限制。

   **注意**:只有基於SOAP的調用支援DSC_REQUEST_TIMEOUT屬性。

要設定連接屬性，請執行以下任務：

1. 使用其建構子建立`java.util.Properties`物件。
1. 要設定`DSC_DEFAULT_EJB_ENDPOINT`連接屬性，請調用`java.util.Properties`對象的`setProperty`方法並傳遞以下值：

   * `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`枚舉值
   * 指定承載AEM Forms之J2EE應用程式伺服器URL的字串值

   >[!NOTE]
   >
   >如果您使用SOAP連接模式，請指定`ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT`枚舉值，而不是`ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`枚舉值。

1. 要設定`DSC_TRANSPORT_PROTOCOL`連接屬性，請調用`java.util.Properties`對象的`setProperty`方法並傳遞以下值：

   * `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL`枚舉值
   * `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`枚舉值

   >[!NOTE]
   >
   >如果您使用SOAP連接模式，請指定`ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`枚舉值，而不是`ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`枚舉值。

1. 要設定`DSC_SERVER_TYPE`連接屬性，請調用`java.util.Properties`對象的`setProperty`方法並傳遞以下值：

   * `ServiceClientFactoryProperties.DSC_SERVER_TYPE`枚舉值
   * 指定承載AEM Forms的J2EE應用程式伺服器的字串值(例如，如果AEM Forms部署在JBoss上，請指定`JBoss`)。

      1. 要設定`DSC_CREDENTIAL_USERNAME`連接屬性，請調用`java.util.Properties`對象的`setProperty`方法並傳遞以下值：
   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME`枚舉值
   * 字串值，指定叫用AEM Forms所需的使用者名稱

      1. 要設定`DSC_CREDENTIAL_PASSWORD`連接屬性，請調用`java.util.Properties`對象的`setProperty`方法並傳遞以下值：
   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD`枚舉值
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

您可以使用`com.adobe.idp.Context`物件，透過已驗證的使用者叫用AEM Forms服務（`com.adobe.idp.Context`物件代表已驗證的使用者）。 使用`com.adobe.idp.Context`物件時，您不需要設定`DSC_CREDENTIAL_USERNAME`或`DSC_CREDENTIAL_PASSWORD`屬性。 使用`AuthenticationManagerServiceClient`對象的`authenticate`方法驗證用戶時，可以獲取`com.adobe.idp.Context`對象。

`authenticate`方法返回包含驗證結果的`AuthResult`對象。 可以通過調用其建構子來建立`com.adobe.idp.Context`對象。 然後調用`com.adobe.idp.Context`對象的`initPrincipal`方法並傳遞`AuthResult`對象，如以下代碼所示：

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

您可以叫用`ServiceClientFactory`物件的`setContext`方法並傳遞`com.adobe.idp.Context`物件，而不設定`DSC_CREDENTIAL_USERNAME`或`DSC_CREDENTIAL_PASSWORD`屬性。 使用AEM表單使用者叫用服務時，請確定他們擁有叫用AEM Forms服務所需的角色`Services User`。

下列程式碼範例說明如何在用來建立`EncryptionServiceClient`物件的連線設定中使用`com.adobe.idp.Context`物件。

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
>有關驗證用戶的完整詳細資訊，請參閱[驗證用戶](/help/forms/developing/users.md#authenticating-users)。

### 調用方案{#invoking_scenarios-1}

本節將討論以下叫用的情況：

* 在自己的Java虛擬機(JVM)中運行的客戶端應用程式調用獨立的AEM Forms實例。
* 在自己的JVM中運行的客戶端應用程式調用群集的AEM Forms實例。

### 調用獨立AEM Forms實例{#client-application-invoking-a-stand-alone-aem-forms-instance}的客戶端應用程式

下圖顯示在其JVM中執行並叫用獨立AEM Forms例項的用戶端應用程式。

在此情況下，客戶端應用程式在其自己的JVM中運行，並調用AEM Forms服務。

>[!NOTE]
>
>此情境是調用所有快速啟動的基礎情形。

### 客戶端應用程式調用群集AEM Forms實例{#client-application-invoking-clustered-aem-forms-instances}

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

## 使用Java API {#passing-data-to-aem-forms-services-using-the-java-api}將資料傳遞至AEM Forms服務

AEM Forms服務作業通常會使用或產生PDF檔案。 叫用服務時，有時需要將PDF檔案（或其他檔案類型，例如XML資料）傳遞至服務。 同樣，有時也需要處理從服務傳回的PDF檔案。 可讓您將資料傳遞至AEM Forms服務及從Java類別為`com.adobe.idp.Document`。

AEM Forms服務不接受PDF檔案作為其他資料類型，例如`java.io.InputStream`物件或位元組陣列。 `com.adobe.idp.Document`物件也可用來將其他類型的資料（例如XML資料）傳遞至服務。

`com.adobe.idp.Document`對象是Java可序列化的類型，因此可通過RMI調用傳遞。 接收方可以配置（同一主機、同一類載入器）、本地（同一主機、不同類載入器）或遠程（不同主機）。 針對每個案例最佳化檔案內容的傳遞。 例如，如果傳送者和接收者位於相同的主機上，則內容會透過本機檔案系統傳遞。 （在某些情況下，檔案可以傳入記憶體。）

根據`com.adobe.idp.Document`對象大小，資料在`com.adobe.idp.Document`對象中攜帶或儲存在伺服器的檔案系統中。 `com.adobe.idp.Document`對象佔用的任何臨時儲存資源在`com.adobe.idp.Document`處理時自動刪除。 （請參閱[處置文檔對象](invoking-aem-forms-using-java.md#disposing-document-objects)。）

有時，您必須先知道`com.adobe.idp.Document`物件的內容類型，才能將其傳遞至服務。 例如，如果操作需要特定內容類型，例如`application/pdf`，則建議您確定內容類型。 （請參閱[確定文檔的內容類型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)。）

`com.adobe.idp.Document`對象嘗試使用提供的資料確定內容類型。 如果無法從提供的資料中檢索內容類型（例如，當資料以位元組陣列形式提供時），請設定內容類型。 要設定內容類型，請調用`com.adobe.idp.Document`對象的`setContentType`方法。 （請參閱[確定文檔的內容類型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)）

如果宣傳資料檔案位於同一檔案系統上，則建立`com.adobe.idp.Document`對象的速度會更快。 如果宣傳資料檔案位於遠程檔案系統上，則必須執行複製操作，這會影響效能。

應用程式可以同時包含`com.adobe.idp.Document`和`org.w3c.dom.Document`資料類型。 不過，請確定您完全符合`org.w3c.dom.Document`資料類型的資格。 有關將`org.w3c.dom.Document`對象轉換為`com.adobe.idp.Document`對象的資訊，請參閱[快速啟動（EJB模式）:使用Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)以可流式配置預填Forms。

>[!NOTE]
>
>為了在使用`com.adobe.idp.Document`對象時防止WebLogic中的記憶體洩漏，請以2048位元組或更少的塊讀取文檔資訊。 例如，以下代碼以2048位元組的塊讀取文檔資訊：

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

### 建立文檔{#creating-documents}

在調用需要PDF文檔（或其他文檔類型）作為輸入值的服務操作之前，建立`com.adobe.idp.Document`對象。 `com.adobe.idp.Document`類提供建構子，使您能夠從以下內容類型中建立文檔：

* 位元組陣列
* 現有`com.adobe.idp.Document`對象
* `java.io.File`物件
* `java.io.InputStream`物件
* `java.net.URL`物件

#### 根據位元組陣列{#creating-a-document-based-on-a-byte-array}建立文檔

以下代碼示例建立基於位元組陣列的`com.adobe.idp.Document`對象。

**建立基於位元組陣列的文檔對象**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### 根據另一文檔{#creating-a-document-based-on-another-document}建立文檔

以下代碼示例建立基於另一個`com.adobe.idp.Document`對象的`com.adobe.idp.Document`對象。

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

#### 根據檔案{#creating-a-document-based-on-a-file}建立文檔

下列程式碼範例會根據名為&#x200B;*map.pdf*&#x200B;的PDF檔案建立`com.adobe.idp.Document`物件。 此檔案位於C硬碟的根目錄中。 此建構子嘗試使用副檔名設定`com.adobe.idp.Document`對象的MIME內容類型。

接受`java.io.File`對象的`com.adobe.idp.Document`建構子也接受布爾參數。 將此參數設定為`true`後， `com.adobe.idp.Document`對象將刪除該檔案。 此操作表示您不必在將檔案傳遞至`com.adobe.idp.Document`建構子後將其移除。

將此參數設為`false`表示您保留此檔案的所有權。 將此參數設為`true`會更有效率。 原因在於`com.adobe.idp.Document`對象可以將檔案直接移動到本地管理區，而不是複製它（速度較慢）。

**建立基於PDF檔案的文檔對象**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### 根據InputStream對象{#creating-a-document-based-on-an-inputstream-object}建立文檔

以下Java代碼示例建立基於`java.io.InputStream`對象的`com.adobe.idp.Document`對象。

**根據InputStream對象建立文檔**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### 根據可從URL {#creating-a-document-based-on-content-accessible-from-an-url}存取的內容建立文檔

以下Java代碼示例基於名為&#x200B;*map.pdf*&#x200B;的PDF檔案建立`com.adobe.idp.Document`對象。 此檔案位於`localhost`上運行的名為`WebApp`的Web應用程式中。 此建構子嘗試使用隨URL協定返回的內容類型來設定`com.adobe.idp.Document`對象的MIME內容類型。

提供給`com.adobe.idp.Document`對象的URL始終在建立原始`com.adobe.idp.Document`對象的一側讀取，如以下示例所示：

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

c:/temp/input.pdf檔案必須位於客戶端電腦上（而不是伺服器電腦上）。 客戶端電腦是讀取URL和建立`com.adobe.idp.Document`對象的位置。

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

### 處理返回的文檔{#handling-returned-documents}

將PDF文檔（或其他資料類型，如XML資料）作為輸出值返回`com.adobe.idp.Document`對象的服務操作。 收到`com.adobe.idp.Document`物件後，可將其轉換為下列格式：

* `java.io.File`物件
* `java.io.InputStream`物件
* 位元組陣列

下面一行代碼將`com.adobe.idp.Document`對象轉換為`java.io.InputStream`對象。 假設`myPDFDocument`代表`com.adobe.idp.Document`物件：

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

同樣，您可以執行以下任務將`com.adobe.idp.Document`的內容複製到本地檔案：

1. 建立`java.io.File`物件。
1. 調用`com.adobe.idp.Document`對象的`copyToFile`方法並傳遞`java.io.File`對象。

以下代碼示例將`com.adobe.idp.Document`對象的內容複製到名為&#x200B;*OtherMap.pdf*&#x200B;的檔案。

**將文檔對象的內容複製到檔案**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 確定文檔{#determining-the-content-type-of-a-document}的內容類型

調用`com.adobe.idp.Document`對象的`getContentType`方法，確定`com.adobe.idp.Document`對象的MIME類型。 此方法會傳回字串值，指定`com.adobe.idp.Document`物件的內容類型。 下表說明AEM Forms傳回的不同內容類型。

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

下列程式碼範例決定`com.adobe.idp.Document`物件的內容類型。

**確定文檔對象的內容類型**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 處理文檔對象{#disposing-document-objects}

當您不再需要`Document`物件時，建議您借由叫用其`dispose`方法來處理該物件。 每個`Document`對象佔用一個檔案描述符，在應用程式的主機平台上佔用多達75 MB的RAM空間。 如果`Document`對象未處置，則Java Garage收集過程會處理它。 但是，通過使用`dispose`方法，可以更快地處理它，從而釋放由`Document`對象佔用的記憶體。

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java客戶端庫調用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java客戶端庫{#invoking-a-service-using-a-java-client-library}調用服務

AEM Forms服務作業可透過服務的強制類型API來叫用，此API稱為Java用戶端程式庫。 *Java客戶端庫*&#x200B;是一組具體類，它提供對服務容器中部署的服務的訪問。 使用調用API實例化表示要調用的服務的Java對象，而不是建立`InvocationRequest`對象。 叫用API可用來叫用在Workbench中建立的程式，例如長期使用的程式。 （請參閱[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

要執行服務操作，請調用屬於Java對象的方法。 Java用戶端程式庫包含通常會將一對一與服務操作對應的方法。 使用Java客戶端庫時，請設定所需的連接屬性。 （請參閱[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。）

設定連接屬性後，建立`ServiceClientFactory`對象，該對象用於實例化允許您調用服務的Java對象。 每個具有Java客戶端庫的服務都有相應的客戶端對象。 例如，要調用Repository服務，請使用其建構子並傳遞`ServiceClientFactory`對象來建立`ResourceRepositoryClient`對象。 `ServiceClientFactory`物件負責維護叫用AEM Forms服務所需的連線設定。

雖然獲取`ServiceClientFactory`通常速度很快，但首次使用工廠時會涉及一些開銷。 此對象已優化，以便重複使用，因此，如果可能，在建立多個Java客戶端對象時，請使用相同的`ServiceClientFactory`對象。 也就是說，請勿為您建立的每個客戶端庫對象建立單獨的`ServiceClientFactory`對象。

有一個「用戶管理器」設定，它控制`com.adobe.idp.Context`對象內影響`ServiceClientFactory`對象的SAML聲明的存留期。 此設定會控制整個AEM Forms中的所有驗證內容存留期，包括使用Java API執行的所有叫用。 預設情況下，可使用`ServiceCleintFactory`對象的時段為2小時。

>[!NOTE]
>
>要說明如何使用Java API調用服務，將調用儲存庫服務的`writeResource`操作。 此操作會將新資源放入儲存庫。

您可以使用Java客戶端庫並執行以下步驟來調用儲存庫服務：

1. 在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-repository-client.jar。 有關這些檔案的位置資訊，請參閱[包含AEM Forms Java庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 設定調用服務所需的連接屬性。
1. 調用`ServiceClientFactory`對象的靜態`createInstance`方法並傳遞包含連接屬性的`java.util.Properties`對象，建立`ServiceClientFactory`對象。
1. 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`ResourceRepositoryClient`物件。 使用`ResourceRepositoryClient`對象調用儲存庫服務操作。
1. 使用其建構子建立`RepositoryInfomodelFactoryBean`物件，並傳遞`null`。 此物件可讓您建立`Resource`物件，用來代表新增至存放庫的內容。
1. 調用`RepositoryInfomodelFactoryBean`對象的`newImage`方法並傳遞以下值，建立`Resource`對象：

   * 通過指定`new Id()`的唯一ID值。
   * 通過指定`new Lid()`的唯一UUID值。
   * 資源的名稱。 您可以指定XDP檔案的檔案名。

   將傳回值轉換為`Resource`。

1. 調用`RepositoryInfomodelFactoryBean`對象的`newImage`方法並將返回值轉換為`ResourceContent`，建立`ResourceContent`對象。 此物件代表新增至存放庫的內容。
1. 通過傳遞`java.io.FileInputStream`對象來建立`com.adobe.idp.Document`對象，該對象儲存要添加到儲存庫的XDP檔案。 （請參閱[根據InputStream對象建立文檔](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)。）
1. 調用`ResourceContent`對象的`setDataDocument`方法，將`com.adobe.idp.Document`對象的內容添加到`ResourceContent`對象。 傳遞`com.adobe.idp.Document`物件。
1. 調用`ResourceContent`對象的`setMimeType`方法並傳遞`application/vnd.adobe.xdp+xml`，設定要添加到儲存庫的XDP檔案的MIME類型。
1. 調用`Resource`對象的`setContent`方法並傳遞`ResourceContent`對象，將`ResourceContent`對象的內容添加到`Resource`對象。
1. 調用`Resource`對象的`setDescription`方法並傳遞表示資源說明的字串值，以添加資源的說明。
1. 叫用`ResourceRepositoryClient`物件的`writeResource`方法並傳遞下列值，將表單設計新增至存放庫：

   * 一個字串值，它指定包含新資源的資源集合的路徑
   * 建立的`Resource`對象

**另請參閱**

[快速入門（EJB模式）:使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 使用調用API {#invoking-a-short-lived-process-using-the-invocation-api}調用短期進程

您可以使用Java調用API調用短期進程。 使用調用API調用短期進程時，需使用`java.util.HashMap`對象傳遞所需的參數值。 對於要傳遞到服務的每個參數，調用`java.util.HashMap`對象的`put`方法，並指定服務所需的名稱值對，以執行指定的操作。 指定屬於短期進程的參數的確切名稱。

>[!NOTE]
>
>有關調用長壽命進程的資訊，請參見[調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

這裡討論的是使用叫用API來叫用下列名為`MyApplication/EncryptDocument`的AEM Forms短期處理程式。

>[!NOTE]
>
>此程式並非以現有的AEM Forms程式為基礎。 若要遵循程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

叫用此程式時，會執行下列動作：

1. 獲取傳遞至流程的不安全PDF文檔。 此操作基於`SetValue`操作。 此進程的輸入參數是名為`inDoc`的`document`進程變數。
1. 使用密碼加密PDF檔案。 此操作基於`PasswordEncryptPDF`操作。 在名為`outDoc`的進程變數中返回密碼加密的PDF文檔。

### 使用Java調用API {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}調用MyApplication/EncryptDocument短期進程

使用Java調用API調用`MyApplication/EncryptDocument`短期進程：

1. 在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。 (請參閱[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)
1. 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。）
1. 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`ServiceClient`物件。 `ServiceClient`物件可讓您叫用服務操作。 它處理諸如查找、調度和路由調用請求等任務。
1. 使用其建構子建立`java.util.HashMap`物件。
1. 為每個輸入參數調用`java.util.HashMap`對象的`put`方法，以傳遞至長期進程。 因為`MyApplication/EncryptDocument`短期進程需要一個類型`Document`的輸入參數，您只需調用`put`方法一次，如以下示例所示。

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. 調用`ServiceClientFactory`對象的`createInvocationRequest`方法並傳遞以下值，建立`InvocationRequest`對象：

   * 一個字串值，它指定要調用的長期進程的名稱。 要調用`MyApplication/EncryptDocument`進程，請指定`MyApplication/EncryptDocument`。
   * 表示流程操作名稱的字串值。 短期進程操作的名稱通常為`invoke`。
   * `java.util.HashMap`物件，包含服務操作所需的參數值。
   * 指定`true`的布爾值，它建立同步請求（此值適用於調用短期進程）。

1. 調用`ServiceClient`對象的`invoke`方法並傳遞`InvocationRequest`對象，將調用請求發送到服務。 `invoke`方法返回`InvocationReponse`對象。

   >[!NOTE]
   >
   >可通過傳遞值`false`作為`createInvocationRequest`方法的第四個參數來調用長壽命進程。 傳遞值&#x200B;`false`*會建立非同步請求。*

1. 調用`InvocationReponse`對象的`getOutputParameter`方法並傳遞指定輸出參數名稱的字串值，以檢索進程的返回值。 在此情況下，請指定`outDoc`（`outDoc`是`MyApplication/EncryptDocument`進程的輸出參數名稱）。 將傳回值轉換為`Document`，如下列範例所示。

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. 建立`java.io.File`物件，並確認副檔名為.pdf。
1. 調用`com.adobe.idp.Document`對象的`copyToFile`方法，將`com.adobe.idp.Document`對象的內容複製到檔案。 請確定您使用`getOutputParameter`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[快速入門：使用叫用API叫用短期處理程式](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[調用以人為中心的長壽命過程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
