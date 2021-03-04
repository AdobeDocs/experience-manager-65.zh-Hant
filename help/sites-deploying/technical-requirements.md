---
title: 技術需求
seo-title: 技術需求
description: 支援的客戶端和伺服器平台清單AEM。
seo-description: 支援的客戶端和伺服器平台清單AEM。
uuid: 597f8fc1-9ac7-458d-a7c1-f576dd0f189b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 16c7a97d-884a-447e-9aad-18a2db1bda1d
docset: aem65
translation-type: tm+mt
source-git-commit: d62249ee2e2d40f2a437c1cb7f2a80f3f8e67efe
workflow-type: tm+mt
source-wordcount: '3207'
ht-degree: 0%

---


# 技術要求{#technical-requirements}

Adobe支援Adobe Experience Manager(AEM)在平台上運行，如本文檔中的以下資訊所詳述。

如果有任何與平台特別相關的問題，請聯絡平台廠商。

>[!NOTE]
>
>視您所安裝的平台而定，AEM使用者管理的需求可能會有不同。

## 必備條件 {#prerequisites}

安裝Adobe Experience Manager的最低要求：

* 已安裝Java平台、標準版JDK或其他支援的[Java虛擬機](#java-virtual-machines)
* Experience Manager快速入門檔案（可獨立執行的JAR或Web應用程式部署WAR）

### 最小尺寸要求{#minimum-sizing-requirements}

運行Adobe Experience Manager的最低要求：

* 安裝目錄中有5 GB的可用磁碟空間
* 2 GB記憶體

>[!NOTE]
>
>* 數位資產使用案例需要更多的基本記憶體。 如需詳細資訊，請參閱[部署與維護](/help/sites-deploying/deploy.md#default-local-install)。
>* [AEM Forms附加](/help/forms/using/installing-configuring-aem-forms-osgi.md) 封裝需要15 GB的暫存空間。

>



有關詳細資訊，請參閱[硬體調整指南](/help/managing/hardware-sizing-guidelines.md)。

### 支援級別{#support-levels}

本檔案列出了Adobe Experience Manager支援的客戶端和伺服器平台。 Adobe提供多種支援級別，包括建議的配置和其他配置。

### 支援的配置{#supported-configurations}

Adobe建議這些配置，並作為標準軟體維護協定的一部分提供完整支援。

<table>
 <tbody>
  <tr>
   <td>支援等級</td>
   <td>說明<br /> </td>
  </tr>
  <tr>
   <td><strong>答：支援</strong></td>
   <td>Adobe為此配置提供完整支援和維護。 此配置由Adobe的質量保證流程涵蓋。</td>
  </tr>
  <tr>
   <td><strong>R:受限制的支援</strong></td>
   <td>為確保客戶專案成功，Adobe在受限制的支援計畫中提供完整支援，這需要符合特定條件。 R級支援需要正式的客戶要求及Adobe確認。 如需詳細資訊，請聯絡Adobe客戶服務。</td>
  </tr>
 </tbody>
</table>

### 不支援的配置{#unsupported-configurations}

| 支援等級 | 說明 |
|---|---|
| **Z:不支援** | 不支援配置。 Adobe不會就配置是否有效發表任何聲明，也不支援它。 |

## 支援的平台{#supported-platforms}

### Java虛擬機{#java-virtual-machines}

應用程式需要Java虛擬機器來執行，此程式由Java開發套件(JDK)散發提供。

Adobe Experience Manager運行下列版本的Java虛擬機：

>[!CAUTION]
>
>建議您追蹤Java廠商的安全性公告，以確保生產環境的安全性，並安裝最新的Java更新。

<table>
 <tbody>
  <tr>
   <td>平台</td>
   <td>支援等級</td>
  </tr>
  <tr>
   <td>OracleJava SE 12 JDK [1]</td>
   <td>Z:不支援 </td>
  </tr>
  <tr>
   <td><strong>OracleJava SE 11 JDK - 64位</strong></td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>OracleJava SE 10 JDK [1]</td>
   <td>Z:不支援 </td>
  </tr>
  <tr>
   <td>OracleJava SE 9 JDK [1]</td>
   <td>Z:不支援</td>
  </tr>
  <tr>
   <td>OracleJava SE 8 JDK - 64位元</td>
   <td>答：支援[3]</td>
  </tr>
  <tr>
   <td>IBM J9 VM —— 內部版本2.9、JRE 1.8.0 [2]</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>IBM J9 VM —— 內部版本2.8、JRE 1.8.0 [2]</td>
   <td>答：支援</td>
  </tr>
 </tbody>
</table>

1. Oracle已改為OracleJava SE產品的「長期支援」(LTS)模型。 Java 9、Java 10和Java 12是非LTS版本，依Oracle區分(請參閱OracleJava SE支援規劃藍圖](https://www.oracle.com/technetwork/java/eol-135779.html))。 [若要部署AEM在生產環境中，Adobe僅支援LTS版本的Java。

1. IBM JRE僅與WebSphere Application Server一起受支援。
1. 對OracleJava SE JDK的支援和分發，包括公開更新結束後LTS版本的所有維護更新，將直接由使用OracleJava SE技術的所有客AEM戶Adobe支援。 如需詳細資訊，請參閱[Adobe Experience ManagerQ&amp;A](assets/adobe-oracle-java-license-agreement.pdf)的OracleJava支援。

### 儲存和持久性{#storage-persistence}

有各種選項可部署Adobe Experience Manager的儲存庫。 有關支援的技術和儲存選項，請參見以下清單。

| **平台** | **說明** | **支援等級** |
|---|---|---|
| **具有TAR檔案的檔案系統** `[1]` | 存放庫 | 答：支援 |
| **具有資料儲存的檔案系統** `[1]` | 二進位檔 | 答：支援 |
| 將二進位檔案儲存在檔案系統`[1]`上的TAR檔案中 | 二進位檔 | Z:不支援生產 |
| AmazonS3 | 二進位檔 | 答：支援 |
| Microsoft Azure Blob儲存空間 | 二進位檔 | 答：支援 |
| MongoDB Enterprise 4.0 | 存放庫 | 答：支援`[2, 3]` |
| MongoDB Enterprise 3.6 | 存放庫 | Z:不支援 |
| MongoDB Enterprise 3.4 | 存放庫 | Z:不支援 |
| IBM DB2 10.5 | 儲存庫和Forms資料庫 | R:受限支援`[4]` |
| Oracle資料庫12c(12.1.x) | 儲存庫和Forms資料庫 | R:受限制的支援 |
| Microsoft SQL Server 2016 | Forms資料庫 | 答：支援 |
| **Apache Lucene（Quickstart內置）** | 搜尋服務 | 答：支援 |
| Apache Solr | 搜尋服務 | 答：支援 |

1. 「檔案系統」包括符合POSIX的塊儲存。 其中包括網路儲存技術。 請注意，檔案系統效能可能會有所不同，並影響整體效能。 建議將測試與網AEM絡／遠程檔案系統結合使用。
1. 中不支援MongoDB共用AEM。
1. 僅支援MongoDB儲存引擎WiredTiger。
1. 支援AEM Forms升級客戶。 不支援新安裝。

>[!NOTE]
>
>有關AEM Communities功能的其他資訊，請參見[部署社區](/help/communities/deploy-communities.md)。

>[!NOTE]
>
>MongoDB是協力廠商軟體，不包含在授權套件AEM中。 如需詳細資訊，請參閱[MongoDB授權政策](https://www.mongodb.org/about/licensing/)頁面。
>
>為充份運用MongoDBAEM部署，Adobe建議授權MongoDB企業版，以從專業支援中獲益。 如需詳細資訊，請參閱[建議部署](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)。
>
>該許可證包括一個標準副本集，該副本集由一個主實例和兩個輔助實例組成，可用於作者或發佈部署。
>
>如果您想要在MongoDB上執行作者和發佈，則需要購買兩個不同的授權。
>
>Adobe客戶服務將協助與MongoDB搭配使用相關的資格確認問AEM題。
>
>如需詳細資訊，請參閱[MongoDB forAdobe Experience Manager頁面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。

>[!NOTE]
>
>上述支援的關聯式資料庫是協力廠商軟體，不包含在授權套件AEM中。
>
>若要使用AEM支援的關係式資料庫執行6.5，必須與資料庫廠商簽訂個別的支援合約。 Adobe客戶服務將協助您針對6.5版使用關聯式資料庫的相關AEM資格問題。
>
>**大多數關係型資料庫目前都受Level-R AEM 6.5的支援，Level-R 6.5隨附支援標準和支援計畫，如上述Level-R說明所述。**

### Servlet引擎／應用程式伺服器{#servlet-engines-application-servers}

Adobe Experience Manager可以作為獨立伺服器（快速入門JAR檔案）或作為第三方應用程式伺服器（WAR檔案）中的Web應用程式運行。

Servlet 3.1需要的Servlet API最低版本

| 平台 | 支援等級 |
|---|---|
| **快速入門內置Servlet引擎(Jetty 9.4)** | 答：支援 |
| OracleWebLogic Server 12.2(12cR2) | Z:不支援 |
| IBM WebSphere Application Server Continuous Delivery(LibertyProfile)與Web Profile 7.0和IBM JRE 1.8 | R:新合約的受限制支援`[2]` |
| IBM WebSphere Application Server 9.0和IBM JRE 1.8 | R:新合約的受限支援`[1]` `[2]` |
| Apache Tomcat 8.5.x | R:新合約的受限制支援`[2]` |
| JBoss EAP 7.2.x與JBoss應用程式伺服器 | Z:不支援 |
| JBoss EAP 7.1.4與JBoss應用程式伺服器 | R:新合約的受限支援`[1]` `[2]` |
| JBoss EAP 7.0.x與JBoss應用程式伺服器 | Z:不支援 |

1. 建議在AEM Forms部署。
1. 從應AEM用程式伺服器的6.5部署開始，會移至「受限制支援」。 現有客戶可升級至AEM6.5，並持續使用應用程式伺服器。 對於新客戶，它隨附支援標準和支援方案，如上述R級說明所述。

### 伺服器作業系統{#server-operating-systems}

Adobe Experience Manager與下列伺服器平台搭配使用，適用於生產環境：

| **平台** | **支援等級** |
|---|---|
| **Linux，基於Red Hat分發** | 答：支援`[1]` `[3]` |
| Linux，基於Debian分發，包括 烏邦圖 | 答：支援`[2]` |
| Linux，基於SUSE分發 | 答：支援 |
| Microsoft Windows Server 2019 `[4]` | R:新合約的限制支援 |
| Microsoft Windows Server 2016 `[4]` | R:新合約的受限制支援`[5]` |
| Microsoft Windows Server 2012 R2 | Z:不支援 |
| OracleSolaris 11 | Z:不支援 |
| IBM AIX 7.2 | Z:不支援 |

1. Linux內核2.6、3.x和4.x包括Red Hat發佈的衍生產品，包括Red Hat Enterprise Linux、CentOS、OracleLinux和AmazonLinux。 AEM Forms附加功能僅在CentOS 7和Red Hat Enterprise Linux 7上受支援。
1. AEM Forms僅在Ubuntu 16.04 LTS上受支援
1. Adobe Managed Services支援的Linux散發
1. 升級至6.5且無生產用途的客戶可支援Microsoft Windows生產部署。 新部署可應AEM Sites和資產部門的要求提供。
1. AEM Forms在Microsoft Window Server上不受支援級R限制

### 虛擬和雲計算環境{#virtual-cloud-computing-environments}

Adobe Experience Manager在雲計算環境(如Microsoft Azure和AmazonWeb Services(AWS))上的虛擬機中運行時，受支援，符合本頁所列的技術要求，並且符合Adobe的標準支援條款。

Adobe建議使用Adobe Managed Services部署AEM在Azure或AWS上。 Adobe Managed Services為專家提供在這些雲計算環境中部署和AEM運作的經驗和技能。 請參閱[有關Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)的其他檔案。

在部署在Azure或AEMAWS或任何其他雲計算環境上的所有其他情況下，將根據本頁所列的技術規格，對虛擬計算環境提供Adobe支援。 與在任何這些雲環境中AEM運行相關的任何已報告問題，都必須獨立於特定於雲計算環境的任何雲服務進行重制，除非雲服務作為本頁所列技術要求（例如Azure Blob儲存或AWS S3）的一部分特別受支援。

如需有關如何在Adobe Managed Services以外部署AEMAzure或AWS的建議，Adobe強烈建議直接與雲端供應商或Adobe合作夥伴合作，以支援在您選擇的雲端AEM環境中部署。 所選雲端供應商或合作夥伴將負責架構的規模規格、設計和實作，以符合您的特定效能、負載、延展性及安全性需求。

### Dispatcher Platforms(Web Servers){#dispatcher-platforms-web-servers}

Dispatcher是快取和負載平衡元件。 [下載最新的Dispatcher版本](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html)。Experience Manager6.5需要Dispatcher 4.3.2版或更高版本。

支援與Dispatcher 4.3.2版一起使用的以下Web伺服器：

| 平台 | 支援等級 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | 答：支援 |
| Microsoft IIS 10(Internet Information Server) | 答：支援 |
| Microsoft IIS 8.5(Internet Information Server) | Z:不支援 |

1. 以Apache httpd原始碼為基礎的Web伺服器，其支援等級將與其所依據的httpd版本相同。 如果有疑問，請Adobe確認與各伺服器產品相關的支援級別。 以下情況：

   1. HTTP伺服器僅使用官方的Apache來源散發，或
   1. HTTP伺服器是以其執行作業系統的方式傳送。 範例：IBM HTTP Server,OracleHTTP Server

1. Dispatcher不適用於Windows作業系統的Apache 2.4.x。

## 支援的客戶端平台{#supported-client-platforms}

### 製作使用者介面{#supported-browsers-for-authoring-user-interface}支援的瀏覽器

Adobe Experience Manager用戶介面適用於以下客戶端平台。 所有瀏覽器都會使用預設的增效模組和附加元件集進行測試。

使用者AEM介面已針對較大螢幕（通常是筆記型電腦和桌上型電腦）和平板電腦外形規格（例如Apple iPad或Microsoft Surface）進行最佳化。 不支援電話外形。

>[!NOTE]
>
>**支援具快速發行週期的瀏覽器：**
>
>Mozilla Firefox、Google Chrome和Microsoft Edge發行版本每隔幾個月更新一次。 Adobe承諾為Adobe Experience Manager提供更新，以維持下列即將推出的這些瀏覽器版本的支援等級。

<table>
 <tbody>
  <tr>
   <td><strong>瀏覽器</strong></td>
   <td><strong>支援UI<br /> </strong></td>
   <td><strong>支援Classic UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome(Evergreen)</strong></td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Microsoft Edge(Evergreen)</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z:不支援</td>
   <td>Z:不支援</td>
  </tr>
  <tr>
   <td>Mozilla Firefox(Evergreen)</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Mozilla Firefox最後一個ESR [1]</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>macOS版Apple Safari(Evergreen)</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>macOS版Apple Safari 11.x</td>
   <td>Z:不支援</td>
   <td>Z:不支援</td>
  </tr>
  <tr>
   <td>iOS 12.x版的Apple Safari</td>
   <td>答：支援[2]</td>
   <td>Z:不支援</td>
  </tr>
  <tr>
   <td>iOS 11.x版的Apple Safari</td>
   <td>Z:不支援</td>
   <td>Z:不支援</td>
  </tr>
 </tbody>
</table>

1. Firefox的延伸支援版本[在mozilla.org](https://www.mozilla.org/en-US/firefox/organizations/faq/)上進一步瞭解此資訊
1. 支援Apple iPad

### 支援的網站瀏覽器{#supported-browsers-for-websites}

一般而言，AEM Sites網站的瀏覽器支援取決於頁面範本AEM的實作、設計和元件輸出，因此由執行這些部分的一方控制。

### WebDAV客戶端{#webdav-clients}

**Microsoft Windows 7+**

要成功與Microsoft Windows 7+連接到未使用AEMSSL保護的實例，必須在Windows中啟用基於不安全網路的基本身份驗證。 這要求在WebClient的Windows註冊表中進行更改：

1. 找到註冊表子項：

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 使用值2或更多的值，將BasicAuthLevel註冊表項添加到此子鍵。

要提高Windows下WebDav客戶端的響應性——請參見[ Microsoft支援KB 2445570](https://support.microsoft.com/kb/2445570)

## 其他平台說明{#additional-platform-notes}

本節提供有關運行Adobe Experience Manager及其附加元件的特殊說明和更詳細的資訊。

### IPv4和IPv6 {#ipv-and-ipv}

Adobe Experience Manager的所有元素（實例、Dispatcher）都可以安裝在IPv4和IPv6網路中。

操作是無縫的，因為無需特殊配置。 如有必要，您只需使用適合您網路類型的格式來指定IP位址。

這表示當需要指定IP位址時，您可以（視需要）從以下位置選擇：

* IPv6地址
例如`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址
例如`https://123.1.1.4:4502`

* 伺服器名稱
例如，`https://www.yourserver.com:4502`

* `localhost`的預設情況將解釋為IPv4和IPv6網路安裝
例如，`https://localhost:4502`

### Dynamic MediaAEM附加元件{#requirements-for-aem-dynamic-media-add-on}的要求

預設AEM禁用Dynamic Media。 請參閱此處啟用Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media)。[

啟用Dynamic Media後，將適用下列附加技術要求。

>[!NOTE]
>
>如果您使用Dynamic Media-混合模式，則這些系統要求僅&#x200B;****&#x200B;適用；Dynamic Media-混合模式具有嵌入式映像伺服器，僅在某些作業系統上通過認證。
>
>對於運行Dynamic Media-Scene7模式（即&#x200B;**dynamicmedia_scene7**&#x200B;運行模式）的Dynamic Media客戶，沒有其他系統要求；系統要求與相同AEM。 Dynamic Media-Scene7模式架構使用雲端影像服務，而非內嵌於中的服務AEM。

#### 硬體{#hardware}

下列硬體需求適用於Linux和Windows:

* 至少具有4個內核的Intel Xeon或AMD Opteron CPU
* 至少16 GB的記憶體

#### Linux {#linux}

如果您在Linux上使用Dynamic Media，則需要滿足以下先決條件：

* RedHat Enterprise 7或CentOS 7及更新版本及最新的修補程式
* 64位元作業系統
* 已停用交換（建議）
* SELinux已停用（請參閱以下附註）

>[!NOTE]
>
>如果設定了語言環境，使LC_CTYPE不等於`en_US.UTF-8` ，則會使Dynamic Media無法工作。 要查看其值是什麼，請在命令提示符下鍵入&quot;locale&quot;。 如果未設定為該值，則在運行前鍵入&quot;export LC_CTYPE=&quot;，將LC_CTYPE環境變數設定為空字串AEM。

>[!NOTE]
>
>**啟用SELinux時，** 禁用SELinux：影像服務無法工作。預設會啟用此選項。 要解決此問題，請編輯&#x200B;**/etc/selinux/config**&#x200B;檔案，並將SELinux值從：
>
>`SELINUX=enforcing` **to** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA體系結構：具有AMD64和英特爾EM64T處理器的系統通常配置為非統一記憶體體系結構(NUMA)平台，這意味著內核在啟動時構建多個記憶體節點，而不是構建單個記憶體節點。** 
>
>該多節點結構可導致在其它節點耗盡之前在一個或多個節點上耗盡儲存器。 當記憶體耗盡時，內核可以決定中止進程（例如，映像伺服器或平台伺服器），即使有可用記憶體。
>
>因此，Adobe建議，如果您運行這樣的系統，使用&#x200B;**numa=off**&#x200B;引導選項關閉NUMA，以避免內核導致這些進程中斷。

>[!NOTE]
>
>**伺服器主機名必須解析：** 確保伺服器的主機名可解析為IP地址。如果不能，請將完全限定的主機名和IP地址添加到&#x200B;**/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* 交換空間至少等於物理記憶體(RAM)的兩倍

若要在Windows上使用Dynamic Media，請安裝Microsoft Visual Studio 2010、2013和2015 x64和x86可轉散發套件。

對於Windows x64:

* 請至[https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)取得Microsoft Visual Studio 2010的可再散發版
* 請至[https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)取得Microsoft Visual Studio 2013可重新散發
* 請至[https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)取得Microsoft Visual Studio 2015可重新散發

對於Windows x86:

* 請至[https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)取得Microsoft Visual Studio 2010的可再散發版
* 請至[https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)取得Microsoft Visual Studio 2013可重新散發
* 請至[https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)取得Microsoft Visual Studio 2015可重新散發

#### MacOS {#macos}

* 10.9.x及更新版本
* 僅支援試用與示範用途

### AEM FormsPDF產生器的需求{#requirements-for-aem-forms-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>產品</strong></p> </th>
   <th><p><strong>支援的格式，可轉換為PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat2017經典軌跡</a> 最新版</td>
   <td>XPS，影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、PFF、 PNG)、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF和TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF產生器僅支援英文、法文、德文和日文版支援的作業系統和應用程式。
>
>此外：
>
>* PDF Generator需要32位元版本的[Acrobat2017傳統音軌17.011.30078或更新版本](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html)才能執行轉換。
>* PDF Generator僅支援32位元零售版Microsoft Office Professional Plus和轉換所需的其他軟體。
>* PDF產生器不支援Microsoft Office 365。
>* OpenOffice專用的PDF產生器轉換僅在Windows和Linux上受支援。
>* OCR PDF、Optimize PDF和Export PDF功能僅在Windows上受支援。
>* Acrobat的版本隨附於AEM Forms，以啟用PDF產生器功能。 套裝版本僅能在AEM Forms授權期間以程式設計方式存取，以搭配AEM FormsPDF產生器使用。 如需詳細資訊，請參閱AEM Forms產品說明（依部署而定）([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)或[Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;

   >
   >
* PDF Generator服務不支援Microsoft Windows 10。

>



### AEM Forms設計人員{#requirements-for-aem-forms-designer}的需求

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server或Microsoft Windows 10
* 支援PAE、NX和SSE2的1 GHz或速度更快的處理器。
* 64位元作業系統需1 GB的記憶體（32位元或2 GB的記憶體）
* 64位元作業系統需要16 GB的磁碟空間（32位元或20 GB的磁碟空間）
* 圖形記憶體- 128 MB的GPU（建議使用256 MB）
* 2.35 GB的可用硬碟空間
* DVD-ROM光碟機
* 1024 X 768像素或更高的螢幕解析度
* 視訊硬體加速（選用）
* Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC。
* 安裝Designer的管理權限。

### AEM Assets元XMP資料回寫{#requirements-for-aem-assets-xmp-metadata-write-back}的要求

支XMP持並啟用以下平台和檔案格式的回寫：

* **作業系統：**

   * Linux（64位元系統上支援32位元和32位元應用程式）。 如需安裝32位元用戶端程式庫的步驟，請參閱[如何啟XMP用64位元RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)上的擷取和回寫。

   * Windows Server
   * Mac OS X（64位元）

* **檔案格式**:JPEG、PNG、TIFF、PDF、INDD、AI和EPS。

### AEM Assets在Linux {#assetsonlinux}上處理繁重元資料資產的要求

XMPFiles處理器過程需要庫GLIBC_2.14才能工作。 使用包含GLIBC_2.14的Linux內核，例如Linux內核3.1.x版。它可改善處理包含大量中繼資料（例如PSD檔案）的資產的效能。 使用舊版GLIBC會導致從`com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`開始的日誌出錯。
