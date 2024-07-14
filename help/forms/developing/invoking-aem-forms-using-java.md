---
title: 使用JavaAPI叫用AEM Forms
description: 使用適用於RMI傳輸通訊協定的AEM Forms Java API進行遠端呼叫、使用VM傳輸進行本機呼叫、使用SOAP進行遠端呼叫、使用不同的驗證（例如使用者名稱和密碼）以及同步和非同步呼叫要求。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '5333'
ht-degree: 0%

---

# 使用Java API叫用AEM Forms {#invoking-aem-forms-using-the-javaapi}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

AEM Forms可透過使用AEM Forms Java API來叫用。 使用AEM Forms Java API時，您可以使用叫用API或Java使用者端資料庫。 Java使用者端程式庫可用於Rights Management服務之類的服務。 這些強型別API可讓您開發叫用AEM Forms的Java應用程式。

引動API是`com.adobe.idp.dsc`封裝中的類別。 使用這些類別，您可以直接傳送呼叫要求給服務，並處理傳回的呼叫回應。 使用叫用API來叫用使用Workbench建立的短期或長期程式。

以程式設計方式叫用服務的建議方法是使用與服務相對應的Java使用者端程式庫，而不是叫用API。 例如，若要叫用加密服務，請使用加密服務使用者端程式庫。 若要執行「加密」服務作業，請叫用屬於「加密」服務使用者端物件的方法。 您可以叫用`EncryptionServiceClient`物件的`encryptPDFUsingPassword`方法，以密碼加密PDF檔案。

Java API支援下列功能：

* 遠端呼叫的RMI傳輸通訊協定
* 本機呼叫的VM傳輸
* 用於遠端呼叫的SOAP
* 不同的驗證，例如使用者名稱和密碼
* 同步和非同步呼叫要求

[包含AEM Forms Java程式庫檔案](#including-aem-forms-java-library-files)

[叫用以人為中心的長期流程](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用網站服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md)

[設定連線屬性](#setting-connection-properties)

[使用Java API傳遞資料至AEM Forms服務](#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java使用者端程式庫叫用服務](#invoking-a-service-using-a-java-client-library)

[使用叫用API叫用短期程式](#invoking-a-short-lived-process-using-the-invocation-api)

[建立可叫用以人為中心的長期流程的Java網頁應用程式](/help/forms/developing/invoking-human-centric-long-lived.md)

## 包含AEM Forms Java程式庫檔案 {#including-aem-forms-java-library-files}

若要使用Java API以程式設計方式叫用AEM Forms服務，請在Java專案的類別路徑中加入必要的程式庫檔案（JAR檔案）。 包含在使用者端應用程式類別路徑中的JAR檔案取決於幾個因素：

* 要呼叫的AEM Forms服務。 使用者端應用程式可以叫用一或多個服務。
* 您要叫用AEM Forms服務的模式。 您可以使用EJB或SOAP模式。 （請參閱[設定連線屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。）

>[!NOTE]
>
>（僅全包式）使用命令`standalone.bat -b <Server IP> -c lc_turnkey.xml`啟動AEM Forms伺服器，以指定EJB的伺服器IP

* 部署AEM Forms的J2EE應用程式伺服器。

### 服務特定的JAR檔案 {#service-specific-jar-files}

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
   <td><p>必須一律包含在Java使用者端應用程式的類別路徑中。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>必須一律包含在Java使用者端應用程式的類別路徑中。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>必須一律包含在Java使用者端應用程式的類別路徑中。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk//client-libs/&lt;應用程式伺服器&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>呼叫Application Manager服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>需要才能叫用Assembler服務。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>呼叫備份和還原服務API時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>呼叫條碼式表單服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>呼叫轉換PDF服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>呼叫Distiller服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>呼叫DocConverter服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>呼叫Document Management服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>需要才能叫用加密服務。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>呼叫Forms服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>呼叫表單資料整合服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>呼叫產生PDF服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>必須呼叫「產生3DPDF」服務。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>呼叫「工作管理員」服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>需要才能叫用Output服務。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>呼叫「PDF公用程式」或「XMP公用程式」服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>呼叫Acrobat Reader DC擴充功能服務時需要。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>呼叫存放庫服務時需要。</p></td>
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
   <td><p>呼叫Rights Management服務時需要。</p><p>如果AEM Forms部署在JBoss上，請包含所有這些檔案。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p><p>JBoss專屬程式庫目錄</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>需要才能叫用簽名服務。</p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>呼叫Task Manager服務時需要。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>必須呼叫信任存放區服務。 </p></td>
   <td><p>&lt;<i>安裝目錄</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### 連線模式和J2EE應用程式JAR檔案 {#connection-mode-and-j2ee-application-jar-files}

下表列出的JAR檔案，視連線模式以及部署AEM Forms的J2EE應用程式伺服器而定。

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
   <td><p>如果使用SOAP模式叫用AEM Forms，請包含這些JAR檔案。</p> </td>
   <td><p>&lt;<em>安裝目錄</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>如果AEM Forms部署在JBoss Application Server上，請包含此JAR檔案。</p> <p>如果jboss-client.jar和參照的jar不在同一位置，則類別載入器找不到所需的類別。</p> </td>
   <td><p>JBoss使用者端程式庫目錄</p> <p>如果您將使用者端應用程式部署在同一J2EE應用程式伺服器上，則不需要包含此檔案。</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>如果AEM Forms部署在BEA WebLogic Server®上，則包含此JAR檔案。</p> </td>
   <td><p>WebLogic專屬程式庫目錄</p> <p>如果您將使用者端應用程式部署在同一J2EE應用程式伺服器上，則不需要包含此檔案。</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>如果AEM Forms部署在WebSphere Application Server上，請包含這些JAR檔案。</p> </li>
     <li><p>(Web服務呼叫需要com.ibm.ws.webservices.thinclient_6.1.0.jar)。</p> </li>
    </ul> </td>
   <td><p>WebSphere特定的lib目錄(<em>[WAS_HOME]</em>/runtime)</p> <p>如果您將使用者端應用程式部署在同一J2EE應用程式伺服器上，則不需要包含這些檔案。</p> </td>
  </tr>
 </tbody>
</table>

### 叫用案例 {#invoking-scenarios}

下表指定叫用案例，並列出成功叫用AEM Forms所需的JAR檔案。

<table>
 <thead>
  <tr>
   <th><p>服務</p> </th>
   <th><p>叫用模式</p> </th>
   <th><p>J2EE應用程式伺服器</p> </th>
   <th><p>必要的JAR檔案</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Forms服務</p> </td>
   <td><p>EJB</p> </td>
   <td><p>Jboss</p> </td>
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
   <td><p>Forms服務</p> <p>Acrobat Reader DC擴充功能服務</p> <p>簽章服務</p> </td>
   <td><p>EJB</p> </td>
   <td><p>Jboss</p> </td>
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
   <td><p>Forms服務</p> <p>Acrobat Reader DC擴充功能服務</p> <p>簽章服務</p> </td>
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

如果您從LiveCycle升級為AEM Forms，建議您在Java專案的類別路徑中包含AEM Forms JAR檔案。 例如，如果您使用Rights Management服務等服務，如果您未在類別路徑中包含AEM Forms JAR檔案，則會遇到相容性問題。

假設您要升級至AEM Forms。 若要使用叫用Rights Management服務的Java應用程式，請包含下列JAR檔案的AEM Forms版本：

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連線屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API傳遞資料至AEM Forms服務](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java使用者端程式庫叫用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 設定連線屬性 {#setting-connection-properties}

使用Java API時，您可以設定連線屬性來叫用AEM Forms。 設定連線屬性時，請指定從遠端還是從本機叫用服務，同時指定連線模式和驗證值。 如果啟用了服務安全性，則需要驗證值。 但是，如果停用服務安全性，則不需要指定驗證值。

連線模式可以是SOAP或EJB模式。 EJB模式使用RMI/IIOP通訊協定，而EJB模式的效能比SOAP模式的效能好。 SOAP模式用於消除J2EE應用程式伺服器相依性，或當防火牆位於AEM Forms和使用者端應用程式之間時。 SOAP模式使用https通訊協定做為基礎傳輸，而且可以跨防火牆邊界通訊。 如果J2EE應用程式伺服器相依性或防火牆都不是問題，建議您使用EJB模式。

若要成功叫用AEM Forms服務，請設定下列連線屬性：

* **DSC_DEFAULT_EJB_ENDPOINT：**&#x200B;如果您使用EJB連線模式，此值代表部署AEM Forms之J2EE應用程式伺服器的URL。 若要從遠端叫用AEM Forms，請指定部署AEM Forms的J2EE應用程式伺服器名稱。 如果您的使用者端應用程式位於相同的J2EE應用程式伺服器上，則可以指定`localhost`。 視建置AEM Forms的J2EE應用程式伺服器而定，請指定下列其中一個值：

   * JBoss： `https://<ServerName>:8080 (default port)`
   * WebSphere： `iiop://<ServerName>:2809 (default port)`
   * WebLogic： `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**：如果您使用SOAP連線模式，此值代表叫用要求傳送到的端點。 若要從遠端叫用AEM Forms，請指定部署AEM Forms的J2EE應用程式伺服器名稱。 如果您的使用者端應用程式位於相同的J2EE應用程式伺服器上，您可以指定`localhost` （例如，`http://localhost:8080`）。

   * 如果J2EE應用程式是JBoss，則通訊埠值`8080`適用。 如果J2EE應用程式伺服器是IBM® WebSphere®，請使用連線埠`9080`。 同樣地，如果J2EE應用程式伺服器是WebLogic，請使用連線埠`7001`。 (這些值是預設的連線埠值。 如果您變更連線埠值，請使用適用的連線埠號碼。)

* **DSC_TRANSPORT_PROTOCOL**：如果您使用EJB連線模式，請為此值指定`ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`。 如果您使用SOAP連線模式，請指定`ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`。
* **DSC_SERVER_TYPE**：指定部署AEM Forms的J2EE應用程式伺服器。 有效值為`JBoss`、`WebSphere`、`WebLogic`。

   * 如果您將此連線屬性設為`WebSphere`，則`java.naming.factory.initial`值會設為`com.ibm.ws.naming.util.WsnInitCtxFactory`。
   * 如果您將此連線屬性設為`WebLogic`，則`java.naming.factory.initial`值會設為`weblogic.jndi.WLInitialContextFactory`。
   * 同樣地，如果您將此連線屬性設為`JBoss`，則`java.naming.factory.initial`值會設為`org.jnp.interfaces.NamingContextFactory`。
   * 如果您不想使用預設值，您可以將`java.naming.factory.initial`屬性設定為符合您要求的值。

  >[!NOTE]
  >
  >您可以使用`ServiceClientFactoryProperties`類別的靜態成員，而不使用字串來設定`DSC_SERVER_TYPE`連線屬性。 可以使用下列值： `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`、`ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`或`ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`。

* **DSC_CREDENTIAL_USERNAME：**&#x200B;指定AEM表單使用者名稱。 使用者若要成功叫用AEM Forms服務，他們需要服務使用者角色。 使用者也可以擁有其他包含「服務啟動」許可權的角色。 否則，當他們嘗試叫用服務時，會擲回例外狀況。 如果停用服務安全性，則不需要指定此連線屬性。
* **DSC_CREDENTIAL_PASSWORD：**&#x200B;指定對應的密碼值。 如果停用服務安全性，則不需要指定此連線屬性。
* **DSC_REQUEST_TIMEOUT：** SOAP要求的預設要求逾時限製為1200000毫秒（20分鐘）。 有時候，要求可能需要更長的時間才能完成作業。 例如，擷取大量記錄的SOAP要求可能需要較長的逾時限制。 您可以使用`ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT`來增加SOAP要求的要求呼叫逾時限制。

  **注意**：只有SOAP型呼叫支援DSC_REQUEST_TIMEOUT屬性。

若要設定連線內容，請執行下列工作：

1. 使用物件的建構函式建立`java.util.Properties`物件。
1. 若要設定`DSC_DEFAULT_EJB_ENDPOINT`連線屬性，請叫用`java.util.Properties`物件的`setProperty`方法，並傳遞下列值：

   * `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`列舉值
   * 字串值，指定代管AEM Forms之J2EE應用程式伺服器的URL

   >[!NOTE]
   >
   >如果您使用SOAP連線模式，請指定`ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT`列舉值，而非`ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`列舉值。

1. 若要設定`DSC_TRANSPORT_PROTOCOL`連線屬性，請叫用`java.util.Properties`物件的`setProperty`方法，並傳遞下列值：

   * `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL`列舉值
   * `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`列舉值

   >[!NOTE]
   >
   >如果您使用SOAP連線模式，請指定`ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`列舉值，而非`ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`列舉值。

1. 若要設定`DSC_SERVER_TYPE`連線屬性，請叫用`java.util.Properties`物件的`setProperty`方法，並傳遞下列值：

   * `ServiceClientFactoryProperties.DSC_SERVER_TYPE`列舉值
   * 字串值，指定代管AEM Forms的J2EE應用程式伺服器(例如，如果AEM Forms部署在JBoss上，請指定`JBoss`)。

      1. 若要設定`DSC_CREDENTIAL_USERNAME`連線屬性，請叫用`java.util.Properties`物件的`setProperty`方法，並傳遞下列值：

   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME`列舉值
   * 字串值，指定呼叫AEM Forms所需的使用者名稱

      1. 若要設定`DSC_CREDENTIAL_PASSWORD`連線屬性，請叫用`java.util.Properties`物件的`setProperty`方法，並傳遞下列值：

   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD`列舉值
   * 字串值，指定對應的密碼值

**正在設定JBoss的EJB連線模式**

以下Java程式碼範例會設定連線屬性，以叫用部署在JBoss上的AEM Forms，並使用EJB連線模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**正在設定WebLogic的EJB連線模式**

下列Java程式碼範例會設定連線屬性，以叫用建置在WebLogic上的AEM Forms，並使用EJB連線模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**正在設定WebSphere的EJB連線模式**

下列Java程式碼範例會設定連線屬性，以叫用建置在WebSphere上的AEM Forms，並使用EJB連線模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**正在設定SOAP連線模式**

以下Java程式碼範例會在SOAP模式下設定連線屬性，以叫用部署在JBoss上的AEM Forms。

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
>如果您選取SOAP連線模式，請確定在使用者端應用程式的類別路徑中包含其他JAR檔案。

**在停用服務安全性時設定連線內容**

以下Java程式碼範例會設定呼叫JBoss Application Server上部署的AEM Forms以及停用服務安全性時所需的連線屬性。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>與「使用AEM Forms程式設計」相關聯的所有Java快速入門都會顯示EJB和SOAP連線設定。

**使用自訂要求逾時限制設定SOAP連線模式**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**使用內容物件來叫用AEM Forms**

您可以使用`com.adobe.idp.Context`物件來叫用具有已驗證使用者的AEM Forms服務（`com.adobe.idp.Context`物件代表已驗證的使用者）。 使用`com.adobe.idp.Context`物件時，您不需要設定`DSC_CREDENTIAL_USERNAME`或`DSC_CREDENTIAL_PASSWORD`屬性。 您可以使用`AuthenticationManagerServiceClient`物件的`authenticate`方法在驗證使用者時取得`com.adobe.idp.Context`物件。

`authenticate`方法傳回包含驗證結果的`AuthResult`物件。 您可以透過叫用它的建構函式來建立`com.adobe.idp.Context`物件。 接著叫用`com.adobe.idp.Context`物件的`initPrincipal`方法並傳遞`AuthResult`物件，如下列程式碼所示：

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

您可以叫用`ServiceClientFactory`物件的`setContext`方法並傳遞`com.adobe.idp.Context`物件，而不設定`DSC_CREDENTIAL_USERNAME`或`DSC_CREDENTIAL_PASSWORD`屬性。 使用AEM表單使用者叫用服務時，請確定他們具有叫用AEM Forms服務所需的名為`Services User`的角色。

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
>如需有關驗證使用者的完整詳細資訊，請參閱[驗證使用者](/help/forms/developing/users.md#authenticating-users)。

### 叫用案例 {#invoking_scenarios-1}

本節將討論下列叫用案例：

* 在其自己的Java虛擬機器器(JVM)中執行的使用者端應用程式會叫用獨立的AEM Forms執行個體。
* 在其自己的JVM中執行的使用者端應用程式會叫用叢集化AEM Forms執行個體。

### 叫用獨立AEM Forms執行個體的使用者端應用程式 {#client-application-invoking-a-stand-alone-aem-forms-instance}

下圖顯示在其自己JVM中執行並叫用獨立AEM Forms執行個體的使用者端應用程式。

在此案例中，使用者端應用程式在其自己的JVM中執行，並叫用AEM Forms服務。

>[!NOTE]
>
>此案例是所有快速入門所依據的叫用案例。

### 叫用叢集AEM Forms執行個體的使用者端應用程式 {#client-application-invoking-clustered-aem-forms-instances}

下圖顯示在其自己的JVM中執行並叫用叢集中的AEM Forms執行個體的使用者端應用程式。

此案例類似於叫用獨立AEM Forms例項的使用者端應用程式。 不過，提供者URL不同。 如果從屬端應用程式想要連線到特定的J2EE應用程式伺服器，應用程式必須將URL變更為參照特定的J2EE應用程式伺服器。

不建議參考特定的J2EE應用程式伺服器，因為如果應用程式伺服器停止，使用者端應用程式和AEM Forms之間的連線就會終止。 建議提供者URL參考儲存格層級JNDI管理員，而非特定的J2EE應用程式伺服器。

使用SOAP連線模式的使用者端應用程式可以使用叢集的HTTP負載平衡器連線埠。 使用EJB連線模式的從屬端應用程式可以連線到特定J2EE應用程式伺服器的EJB連線埠。 此動作會處理叢集節點之間的負載平衡。

**WebSphere**

下列範例顯示用來連線至WebSphere上所部署AEM Forms的jndi.properties檔案內容。

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

下面的示例演示用於連接到部署在 WebLogic 上的AEM Forms的 jndi.properties 文件的內容。

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

以下示例顯示了用於連接到部署在 JBoss 上的AEM Forms的 jndi.properties 文件的內容。

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>請洽詢您的管理員，以確定J2EE應用程式伺服器名稱和連線埠號碼。

**另請參閱**

[包括 AEM Forms Java 資料庫 檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用 Java API 將數據傳遞至 AEM Forms 服務](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用 Java 客戶機資料庫叫用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用 Java API 將數據傳遞至 AEM Forms 服務 {#passing-data-to-aem-forms-services-using-the-java-api}

AEM Forms服務作業通常會消耗或產生PDF檔案。 當您叫用服務時，有時必須將PDF檔案（或其他檔案型別，例如XML資料）傳遞給服務。 同樣地，有時候，處理從服務傳回的PDF檔案也是必要的。 可讓您在AEM Forms服務之間傳遞資料的Java類別是`com.adobe.idp.Document`。

AEM Forms服務不接受PDF檔案做為其他資料型別，例如`java.io.InputStream`物件或位元組陣列。 `com.adobe.idp.Document`物件也可用來將其他型別的資料（例如XML資料）傳遞至服務。

`com.adobe.idp.Document`物件是Java可序列化型別，因此可透過RMI呼叫傳遞。 接收端可以並置（相同主機、相同類別載入器）、本機（相同主機、不同類別載入器）或遠端（不同主機）。 檔案內容的傳遞已針對每個案例最佳化。 例如，如果傳送者與接收者位在相同主機上，則內容會透過本機檔案系統傳遞。 （在某些情況下，檔案可以在記憶體中傳遞。）

根據`com.adobe.idp.Document`物件大小，資料會在`com.adobe.idp.Document`物件中攜帶或儲存在伺服器的檔案系統中。 `com.adobe.idp.Document`物件所佔用的任何暫存資源會在`com.adobe.idp.Document`處置時自動移除。 （請參閱[處置檔案物件](invoking-aem-forms-using-java.md#disposing-document-objects)。）

有時您必須先知道`com.adobe.idp.Document`物件的內容型別，才能將其傳遞給服務。 例如，如果作業需要特定內容型別（例如`application/pdf`），建議您決定內容型別。 （請參閱[決定檔案的內容型別](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)。）

`com.adobe.idp.Document`物件會嘗試使用提供的資料來判斷內容型別。 如果無法從提供的資料中擷取內容型別（例如，當資料以位元組陣列提供時），請設定內容型別。 若要設定內容型別，請叫用`com.adobe.idp.Document`物件的`setContentType`方法。 （請參閱[決定檔案的內容型別](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)）

如果附屬檔案位於相同的檔案系統上，建立`com.adobe.idp.Document`物件會更快。 如果附屬檔案位於遠端檔案系統上，則必須進行複製操作，這會影響效能。

應用程式可包含`com.adobe.idp.Document`和`org.w3c.dom.Document`資料型別。 不過，請確定您已完全符合`org.w3c.dom.Document`資料型別的資格。 如需有關將`org.w3c.dom.Document`物件轉換為`com.adobe.idp.Document`物件的資訊，請參閱[快速入門（EJB模式）：使用Java API預先填入Forms的可流程配置](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)。

>[!NOTE]
>
>若要防止使用`com.adobe.idp.Document`物件時WebLogic中的記憶體洩漏，請以2048個位元組或更少的區塊讀取檔案資訊。 例如，下列程式碼會以2048位元組的區塊讀取檔案資訊：

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

[設定連線屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 建立檔案 {#creating-documents}

啟動需要PDF檔案（或其他檔案型別）作為輸入值的服務作業之前，請先建立`com.adobe.idp.Document`物件。 `com.adobe.idp.Document`類別提供的建構函式可讓您從下列內容型別建立檔案：

* 位元組陣列
* 現有的`com.adobe.idp.Document`物件
* `java.io.File`物件
* `java.io.InputStream`物件
* `java.net.URL`物件

#### 根據位元組陣列建立檔案 {#creating-a-document-based-on-a-byte-array}

下列程式碼範例會建立以位元組陣列為基礎的`com.adobe.idp.Document`物件。

**建立以位元組陣列為基礎的Document物件**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### 根據其他檔案建立檔案 {#creating-a-document-based-on-another-document}

下列程式碼範例會建立以其他`com.adobe.idp.Document`物件為基礎的`com.adobe.idp.Document`物件。

**建立以其他檔案為基礎的檔案物件**

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

#### 根據檔案建立檔案 {#creating-a-document-based-on-a-file}

下列程式碼範例會建立以名為&#x200B;*map.pdf*&#x200B;的PDF檔案為基礎的`com.adobe.idp.Document`物件。 此檔案位於C硬碟的根目錄。 此建構函式會嘗試使用副檔名來設定`com.adobe.idp.Document`物件的MIME內容型別。

接受`java.io.File`物件的`com.adobe.idp.Document`建構函式也接受布林引數。 透過將此引數設定為`true`，`com.adobe.idp.Document`物件會刪除檔案。 此動作表示您將檔案傳遞至`com.adobe.idp.Document`建構函式後，不必移除檔案。

將此引數設定為`false`表示您保留此檔案的所有權。 將此引數設定為`true`會更有效率。 原因在於`com.adobe.idp.Document`物件可以直接將檔案移至本機Managed區域，而非複製檔案（速度較慢）。

**建立以PDF檔案為基礎的Document物件**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### 根據InputStream物件建立檔案 {#creating-a-document-based-on-an-inputstream-object}

下列Java程式碼範例會建立以`java.io.InputStream`物件為基礎的`com.adobe.idp.Document`物件。

**根據InputStream物件建立檔案**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### 根據可從URL存取的內容建立檔案 {#creating-a-document-based-on-content-accessible-from-an-url}

以下Java程式碼範例會根據名為&#x200B;*map.pdf*&#x200B;的PDF檔案來建立`com.adobe.idp.Document`物件。 此檔案位於名為`WebApp`的Web應用程式中，該應用程式正在`localhost`上執行。 此建構函式會嘗試使用URL通訊協定傳回的內容型別來設定`com.adobe.idp.Document`物件的MIME內容型別。

提供給`com.adobe.idp.Document`物件的URL一律會在建立原始`com.adobe.idp.Document`物件的一側讀取，如以下範例所示：

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

c：/temp/input.pdf 文件必須位於用戶端電腦上（而不是伺服器計算機上）。 用戶端電腦是讀取URL和 `com.adobe.idp.Document` 創建物件的位置。

**根據可從URL存取內容建立文件**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連線屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 處理傳回的檔案 {#handling-returned-documents}

返回 PDF 檔（或其他資料類型，如 XML 資料）作為輸出值的服務操作傳回物件 `com.adobe.idp.Document` 。 收到 `com.adobe.idp.Document` 物件后，可以將其轉換為以下格式：

* 物件`java.io.File`
* 物件`java.io.InputStream`
* 位元組陣列

下列程式碼行會將`com.adobe.idp.Document`物件轉換為`java.io.InputStream`物件。 假設`myPDFDocument`代表`com.adobe.idp.Document`物件：

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

同樣地，您可以執行下列工作，將`com.adobe.idp.Document`的內容複製到本機檔案：

1. 建立`java.io.File`物件。
1. 叫用`com.adobe.idp.Document`物件的`copyToFile`方法並傳遞`java.io.File`物件。

下列程式碼範例將`com.adobe.idp.Document`物件的內容複製到名為&#x200B;*AnotherMap.pdf*&#x200B;的檔案。

**正在複製檔案物件的內容至檔案**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連線屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 決定檔案的內容型別 {#determining-the-content-type-of-a-document}

呼叫`com.adobe.idp.Document`物件的`getContentType`方法，判斷`com.adobe.idp.Document`物件的MIME型別。 此方法會傳回字串值，指定`com.adobe.idp.Document`物件的內容型別。 下表說明AEM Forms傳回的不同內容型別。

<table>
 <thead>
  <tr>
   <th><p>MIME型別</p></th>
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
   <td><p>XML資料封裝(XDP)用於轉存的XML Forms架構(XFA)表單</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>書籤、附件或其他XML檔案</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Forms資料格式(FDF)，用於轉存的Acrobat表單</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML Forms資料格式(XFDF)，用於轉存的Acrobat表單</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>豐富資料格式和XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>通用資料格式</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>未指定的MIME型別</p></td>
  </tr>
 </tbody>
</table>

下列程式碼範例決定`com.adobe.idp.Document`物件的內容型別。

**正在決定Document物件的內容型別**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[設定連線屬性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 處置檔案物件 {#disposing-document-objects}

當您不再需要`Document`物件時，建議您叫用其`dispose`方法來處置它。 每個`Document`物件會佔用一個檔案描述元，以及應用程式主機平台上最多75 MB的RAM空間。 如果未處置`Document`物件，則Java Garage收集程式會將其處置。 不過，使用`dispose`方法儘快處置它，您就可以釋放`Document`物件所佔用的記憶體。

**另請參閱**

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java使用者端程式庫叫用服務](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java使用者端程式庫叫用服務 {#invoking-a-service-using-a-java-client-library}

AEM Forms服務作業可使用服務的強型別API （稱為Java使用者端程式庫）來叫用。 *Java使用者端程式庫*&#x200B;是一組提供存取服務容器中部署之服務的具體類別。 您將Java物件例項化，該物件代表要叫用的服務，而不是使用叫用API建立`InvocationRequest`物件。 「叫用API」可用來叫用在Workbench中建立的程式，例如長期程式。 （請參閱[叫用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

若要執行服務作業，請叫用屬於Java物件的方法。 Java使用者端程式庫所包含的方法，通常會將服務操作對應到一。 使用Java使用者端程式庫時，請設定必要的連線屬性。 （請參閱[設定連線屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。）

在您設定連線屬性之後，請建立`ServiceClientFactory`物件，用來具現化Java物件，讓您叫用服務。 每個具有Java使用者端程式庫的服務都有對應的使用者端物件。 例如，若要叫用存放庫服務，請使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。 `ServiceClientFactory`物件負責維護呼叫AEM Forms服務所需的連線設定。

雖然取得`ServiceClientFactory`通常很快，但在第一次使用工廠時會產生一些額外負荷。 此物件已針對重複使用而最佳化，因此，當您建立多個Java使用者端物件時，請儘可能使用相同的`ServiceClientFactory`物件。 也就是說，請勿為您建立的每個使用者端程式庫物件建立個別的`ServiceClientFactory`物件。

有一個使用者管理員設定可控制影響`ServiceClientFactory`物件的`com.adobe.idp.Context`物件內SAML宣告的存留期。 此設定會控制整個AEM Forms的所有驗證內容存留期，包括使用Java API執行的所有叫用。 根據預設，可以使用`ServiceCleintFactory`物件的時段為兩個小時。

>[!NOTE]
>
>若要說明如何使用Java API來叫用服務，會叫用儲存庫服務的`writeResource`作業。 此操作會將新資源放入存放庫中。

您可以使用 Java 客戶機資料庫並執行以下步驟來呼叫儲存庫服務：

1. 將用戶端 JAR 檔案 （例如 adobe-存放庫-client.jar） 包含在 Java 專案的類別路徑中。 有關這些檔的位置的資訊，請參閱 [包括AEM Forms Java 資料庫檔](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 設置調用服務所需的連接屬性。
1. 呼叫`ServiceClientFactory`物件的靜態`createInstance`方法，並傳遞包含連線屬性的`java.util.Properties`物件，以建立`ServiceClientFactory`物件。
1. 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`ResourceRepositoryClient`物件。 使用該 `ResourceRepositoryClient` 物件來調用存儲庫服務操作。
1. `RepositoryInfomodelFactoryBean`使用物件的建構函數建立物件並傳遞 `null`.此物件允許您創建一個 `Resource` 表示添加到存放庫內容的物件。
1. `Resource`通過調用`RepositoryInfomodelFactoryBean`物件的方法`newImage`並傳遞以下值來建立物件：

   * 唯一 ID 值，方法是指定 `new Id()`.
   * 藉由指定`new Lid()`來指定唯一的UUID值。
   * 資源的名稱。 您可以指定XDP檔案的檔案名稱。

   將傳回值轉換為`Resource`。

1. 呼叫`RepositoryInfomodelFactoryBean`物件的`newImage`方法，並將傳回值轉型為`ResourceContent`，以建立`ResourceContent`物件。 此物件代表新增至存放庫的內容。
1. 傳遞儲存XDP檔案以新增至儲存庫的`java.io.FileInputStream`物件，以建立`com.adobe.idp.Document`物件。 （請參閱[根據InputStream物件建立檔案](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)。）
1. 呼叫`ResourceContent`物件的`setDataDocument`方法，將`com.adobe.idp.Document`物件的內容新增至`ResourceContent`物件。 傳遞`com.adobe.idp.Document`物件。
1. 呼叫`ResourceContent`物件的`setMimeType`方法並傳遞`application/vnd.adobe.xdp+xml`，以將XDP檔案的MIME型別設定為加入儲存庫。
1. 呼叫`Resource`物件的`setContent`方法並傳遞`ResourceContent`物件，將`ResourceContent`物件的內容新增至`Resource`物件。
1. 叫用`Resource`物件的`setDescription`方法並傳遞代表資源說明的字串值，以新增資源的說明。
1. 叫用`ResourceRepositoryClient`物件的`writeResource`方法並傳遞下列值，以將表單設計加入儲存庫：

   * 字串值，指定包含新資源的資源集合的路徑
   * 已建立的`Resource`物件

**另請參閱**

[快速入門（EJB模式）：使用Java API寫入資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[使用Java API叫用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 使用叫用API叫用短期程式 {#invoking-a-short-lived-process-using-the-invocation-api}

您可以使用Java叫用API來叫用短期流程。 當您使用叫用API叫用短期處理程式時，您會使用`java.util.HashMap`物件傳遞必要的引數值。 對於要傳遞給服務的每個引數，請叫用`java.util.HashMap`物件的`put`方法，並指定服務執行指定作業所需的名稱 — 值組。 指定屬於短期處理序之引數的確切名稱。

>[!NOTE]
>
>如需有關叫用長效處理序的資訊，請參閱[叫用以人為中心的長效處理序](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

此處的討論內容是關於使用引動API來叫用下列名為`MyApplication/EncryptDocument`的AEM Forms短期處理序。

>[!NOTE]
>
>此程式並非以現有AEM Forms程式為基礎。 若要跟隨程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

叫用此程式時，會執行下列動作：

1. 取得傳遞至程式的不安全PDF檔案。 此動作是以`SetValue`作業為基礎。 此處理序的輸入引數是名為`inDoc`的`document`處理序變數。
1. 使用密碼加密PDF檔案。 此動作是以`PasswordEncryptPDF`作業為基礎。 密碼加密的PDF檔案傳回名為`outDoc`的程式變數。

### 使用Java叫用API叫用MyApplication/EncryptDocument短期程式 {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

使用Java叫用API叫用`MyApplication/EncryptDocument`短期處理序：

1. 在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。 (請參閱[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)
1. 建立包含連線屬性的`ServiceClientFactory`物件。 （請參閱[設定連線屬性](invoking-aem-forms-using-java.md#setting-connection-properties)。）
1. 使用它的建構函式並傳遞`ServiceClientFactory`物件來建立`ServiceClient`物件。 `ServiceClient`物件可讓您叫用服務作業。 它會處理如尋找、分派及路由呼叫要求等工作。
1. 使用物件的建構函式建立`java.util.HashMap`物件。
1. 叫用每個輸入引數的`java.util.HashMap`物件的`put`方法，以傳遞至長效處理序。 由於`MyApplication/EncryptDocument`短期處理程式需要一個型別`Document`的輸入引數，因此您只需要叫用`put`方法一次，如下列範例所示。

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. 呼叫`ServiceClientFactory`物件的`createInvocationRequest`方法，並傳遞下列值以建立`InvocationRequest`物件：

   * 字串值，指定要叫用的長效處理序名稱。 若要叫用`MyApplication/EncryptDocument`處理序，請指定`MyApplication/EncryptDocument`。
   * 代表處理作業名稱的字串值。 一般而言，短期處理程式操作的名稱是`invoke`。
   * 包含服務作業所需之引數值的`java.util.HashMap`物件。
   * 指定`true`的布林值，會建立同步要求（此值適用於叫用短期處理程式）。

1. 透過叫用`ServiceClient`物件的`invoke`方法並傳遞`InvocationRequest`物件來傳送呼叫要求給服務。 `invoke`方法傳回`InvocationReponse`物件。

   >[!NOTE]
   >
   >可透過傳遞值`false`作為`createInvocationRequest`方法的第四個引數來叫用長期處理序。 傳遞值&#x200B;`false`*會建立非同步要求。*

1. 叫用`InvocationReponse`物件的`getOutputParameter`方法，並傳遞指定輸出引數名稱的字串值，以擷取處理序的傳回值。 在此情況下，請指定`outDoc` （`outDoc`是`MyApplication/EncryptDocument`處理序的輸出引數名稱）。 將傳回值轉換為`Document`，如下列範例所示。

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. 建立`java.io.File`物件，並確定副檔名為.pdf。
1. 叫用`com.adobe.idp.Document`物件的`copyToFile`方法，將`com.adobe.idp.Document`物件的內容複製到檔案。 確定您使用的是`getOutputParameter`方法傳回的`com.adobe.idp.Document`物件。

**另請參閱**

[快速入門：使用叫用API叫用短期流程](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[叫用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[包含AEM Forms Java程式庫檔案](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
