---
title: 技術需求
seo-title: 技術需求
description: AEM支援的用戶端和伺服器平台清單。
seo-description: AEM支援的用戶端和伺服器平台清單。
uuid: 597f8fc1-9ac7-458d-a7c1-f576dd0f189b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 16c7a97d-884a-447e-9aad-18a2db1bda1d
docset: aem65
translation-type: tm+mt
source-git-commit: 7065a6b984afb18c188acd848b9b77da7da67749
workflow-type: tm+mt
source-wordcount: '3118'
ht-degree: 0%

---


# 技術要求{#technical-requirements}

Adobe支援平台上的Adobe Experience Manager(AEM)，如本檔案下列資訊所詳述。

如果有任何與平台特別相關的問題，請聯絡平台廠商。

>[!NOTE]
>
>視您安裝AEM的平台而定，可能會有不同的使用者管理需求集。

## 必備條件 {#prerequisites}

安裝Adobe Experience Manager的最低要求：

* 已安裝Java平台、標準版JDK或其他支援的[Java虛擬機](#java-virtual-machines)
* Experience Manager Quickstart檔案（獨立JAR或Web應用程式部署WAR）

### 最小尺寸要求{#minimum-sizing-requirements}

執行Adobe Experience Manager的最低需求：

* 安裝目錄中有5 GB的可用磁碟空間
* 2 GB記憶體

>[!NOTE]
>
>* 數位資產使用案例需要更多的基本記憶體。 如需詳細資訊，請參閱[部署與維護](/help/sites-deploying/deploy.md#default-local-install)。
>* [AEM Forms附加元件套件](/help/forms/using/installing-configuring-aem-forms-osgi.md) 需要15 GB的暫存空間。

>



有關詳細資訊，請參閱[硬體調整指南](/help/managing/hardware-sizing-guidelines.md)。

### 支援級別{#support-levels}

本檔案列出Adobe Experience Manager支援的用戶端和伺服器平台。 Adobe針對建議的組態和其他組態提供數種支援等級。

### 支援的配置{#supported-configurations}

Adobe建議您進行這些組態，並在標準軟體維護合約中提供完整支援。

<table>
 <tbody>
  <tr>
   <td>支援等級</td>
   <td>說明<br /> </td>
  </tr>
  <tr>
   <td><strong>答：支援</strong></td>
   <td>Adobe提供此組態的完整支援與維護。 Adobe的品質保證程式涵蓋此設定。</td>
  </tr>
  <tr>
   <td><strong>R:受限制的支援</strong></td>
   <td>為確保客戶專案成功，Adobe在受限制的支援計畫中提供完整支援，這需要符合特定條件。 R級支援需要Adobe正式向客戶提出要求及確認。 如需詳細資訊，請聯絡Adobe客戶服務。</td>
  </tr>
 </tbody>
</table>

### 不支援的配置{#unsupported-configurations}

| 支援等級 | 說明 |
|---|---|
| **Z:不支援** | 不支援配置。 Adobe不會就設定是否有效發表任何陳述，也不支援。 |

## 支援的平台{#supported-platforms}

### Java虛擬機{#java-virtual-machines}

應用程式需要Java虛擬機器來執行，此程式由Java開發套件(JDK)散發提供。

Adobe Experience Manager可與下列Java虛擬機版本搭配運作：

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
   <td>Oracle Java SE 12 JDK [1]</td>
   <td>Z:不支援 </td>
  </tr>
  <tr>
   <td><strong>Oracle Java SE 11 JDK - 64位</strong></td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Oracle Java SE 10 JDK [1]</td>
   <td>Z:不支援 </td>
  </tr>
  <tr>
   <td>Oracle Java SE 9 JDK [1]</td>
   <td>Z:不支援</td>
  </tr>
  <tr>
   <td>Oracle Java SE 8 JDK - 64位</td>
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

1. Oracle已改為Oracle Java SE產品的「長期支援」(LTS)模型。 Java 9、Java 10和Java 12是Oracle發行的非LTS版本（請參閱[Oracle Java SE支援路線圖](https://www.oracle.com/technetwork/java/eol-135779.html)）。 若要在生產環境中部署AEM,Adobe僅提供LTS版Java的支援。

1. IBM JRE僅與WebSphere Application Server一起受支援。
1. Adobe將直接支援所有使用Oracle Java SE技術的AEM客戶，支援和散發Oracle Java SE JDK，包括公開更新結束後所有LTS版本的維護更新。 如需詳細資訊，請參閱[Adobe Experience Manager Q&amp;A](assets/adobe-oracle-java-license-agreement.pdf)的Oracle Java支援。

### 儲存和持久性{#storage-persistence}

Adobe Experience Manager的儲存庫有多種部署選項。 有關支援的技術和儲存選項，請參見以下清單。

| **平台** | **說明** | **支援等級** |
|---|---|---|
| **具有TAR檔案的檔案系統** `[1]` | 存放庫 | 答：支援 |
| **具有資料儲存的檔案系統** `[1]` | 二進位檔 | 答：支援 |
| 將二進位檔案儲存在檔案系統`[1]`上的TAR檔案中 | 二進位檔 | Z:不支援生產 |
| Amazon S3 | 二進位檔 | 答：支援 |
| Microsoft Azure Blob儲存空間 | 二進位檔 | 答：支援 |
| MongoDB Enterprise 4.0 | 存放庫 | 答：支援`[2, 3]` |
| MongoDB Enterprise 3.6 | 存放庫 | Z:不支援 |
| MongoDB Enterprise 3.4 | 存放庫 | Z:不支援 |
| IBM DB2 10.5 | 儲存庫和表單資料庫 | R:受限支援`[4]` |
| Oracle Database 12c(12.1.x) | 儲存庫和表單資料庫 | R:受限制的支援 |
| Microsoft SQL Server 2016 | Forms資料庫 | 答：支援 |
| **Apache Lucene（Quickstart內置）** | 搜尋服務 | 答：支援 |
| Apache Solr | 搜尋服務 | 答：支援 |

1. 「檔案系統」包括符合POSIX的塊儲存。 其中包括網路儲存技術。 請注意，檔案系統效能可能會有所不同，並影響整體效能。 建議您將測試AEM與網路／遠端檔案系統結合載入。
1. AEM不支援MongoDB Sharding。
1. 僅支援MongoDB儲存引擎WiredTiger。
1. AEM Forms升級客戶支援。 不支援新安裝。

>[!NOTE]
>
>如需AEM Communities功能的詳細資訊，請參閱[部署社群](/help/communities/deploy-communities.md)。

>[!NOTE]
>
>MongoDB是協力廠商軟體，不包含在AEM授權套件中。 如需詳細資訊，請參閱[MongoDB授權政策](https://www.mongodb.org/about/licensing/)頁面。
>
>為了充份運用MongoDB的AEM部署，Adobe建議授權MongoDB企業版，以從專業支援中獲益。 如需詳細資訊，請參閱[建議部署](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)。
>
>該許可證包括一個標準副本集，該副本集由一個主實例和兩個輔助實例組成，可用於作者或發佈部署。
>
>如果您想要在MongoDB上執行作者和發佈，則需要購買兩個不同的授權。
>
>Adobe客戶服務將協助您針對搭配AEM使用MongoDB的相關資格問題。
>
>如需詳細資訊，請參閱[MongoDB for Adobe Experience Manager頁面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。

>[!NOTE]
>
>上述支援的關聯式資料庫是協力廠商軟體，不包含在AEM授權套件中。
>
>若要使用支援的關聯式資料庫執行AEM 6.5，必須與資料庫廠商簽訂個別的支援合約。 Adobe客戶服務將協助您針對AEM 6.5使用關係式資料庫的相關資格問題。
>
>**AEM 6.5的Level-R目前支援大部分的關聯式資料庫，此Level-R說明隨附支援標準和支援方案，如上述Level-R說明所述。**

### Servlet引擎／應用程式伺服器{#servlet-engines-application-servers}

Adobe Experience Manager可以作為獨立伺服器（快速入門JAR檔案）或作為第三方應用程式伺服器（WAR檔案）中的Web應用程式運行。

Servlet 3.1需要的Servlet API最低版本

| 平台 | 支援等級 |
|---|---|
| **快速入門內置Servlet引擎(Jetty 9.4)** | 答：支援 |
| Oracle WebLogic Server 12.2(12cR2) | Z:不支援 |
| IBM WebSphere Application Server Continuous Delivery(LibertyProfile)與Web Profile 7.0和IBM JRE 1.8 | R:新合約的受限制支援`[2]` |
| IBM WebSphere Application Server 9.0和IBM JRE 1.8 | R:新合約的受限支援`[1]` `[2]` |
| Apache Tomcat 8.5.x | R:新合約的受限制支援`[2]` |
| JBoss EAP 7.2.x與JBoss應用程式伺服器 | Z:不支援 |
| JBoss EAP 7.1.4與JBoss應用程式伺服器 | R:新合約的受限支援`[1]` `[2]` |
| JBoss EAP 7.0.x與JBoss應用程式伺服器 | Z:不支援 |

1. 建議使用AEM Forms進行部署。
1. 在應用程式伺服器上啟動AEM 6.5部署會移至「受限制支援」。 現有客戶可升級至AEM 6.5並持續使用應用程式伺服器。 對於新客戶，它隨附支援標準和支援方案，如上述R級說明所述。

### 伺服器作業系統{#server-operating-systems}

Adobe Experience Manager適用於下列生產環境的伺服器平台：

| **平台** | **支援等級** |
|---|---|
| **Linux，基於Red Hat分發** | 答：支援`[1]` `[3]` |
| Linux，基於Debian分發，包括 烏邦圖 | 答：支援`[2]` |
| Linux，基於SUSE分發 | 答：支援 |
| Microsoft Windows Server 2019 `[4]` | R:新合約的限制支援 |
| Microsoft Windows Server 2016 `[4]` | R:新合約的受限制支援`[5]` |
| Microsoft Windows Server 2012 R2 | Z:不支援 |
| Oracle Solaris 11 | Z:不支援 |
| IBM AIX 7.2 | Z:不支援 |

1. Linux內核2.6、3.x和4.x包括Red Hat分發的衍生產品，包括Red Hat Enterprise Linux、CentOS、Oracle Linux和Amazon Linux。 AEM Forms附加元件功能僅在CentOS 7和Red Hat Enterprise Linux 7上受支援。
1. AEM Forms僅在Ubuntu 16.04 LTS上受支援
1. Adobe Managed Services支援的Linux散發
1. 升級至6.5且無生產用途的客戶可支援Microsoft Windows生產部署。 AEM Sites和Assets的新部署是隨選的。
1. AEM Forms不受Support-Level R限制，在Microsoft Window Server上受支援

### 虛擬和雲計算環境{#virtual-cloud-computing-environments}

Adobe Experience Manager在雲計算環境(例如Microsoft Azure和Amazon Web Services(AWS))的虛擬機器中執行時受到支援，符合本頁所列的技術要求，並符合Adobe的標準支援條款。

Adobe建議使用Adobe Managed Services在Azure或AWS上部署AEM。 Adobe Managed Services為專家提供在這些雲端運算環境中部署和操作AEM的經驗和技能。 請參閱[有關Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)的其他檔案。

在部署AEM至Azure或AWS或任何其他雲端運算環境的所有其他情況下，Adobe將依照本頁所列技術規格，對虛擬計算環境提供支援。 與在任何這些雲端環境中執行的AEM相關的任何已報告問題，都必須獨立於雲端計算環境專用的任何雲端服務來重制，除非雲端服務是本頁所列技術需求中特別支援的一部分，例如Azure Blob儲存空間或AWS S3。

如需有關如何在Adobe Managed Services以外的Azure或AWS上部署AEM的建議，Adobe強烈建議直接與雲端供應商或支援在您選擇的雲端環境中部署AEM的Adobe合作夥伴合作。 所選雲端供應商或合作夥伴將負責架構的規模規格、設計和實作，以符合您的特定效能、負載、延展性及安全性需求。

### Dispatcher Platforms(Web Servers){#dispatcher-platforms-web-servers}

Dispatcher是快取和負載平衡元件。 [下載最新的Dispatcher版本](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html)。Experience Manager 6.5需要Dispatcher 4.3.2版或更高版本。

支援與Dispatcher 4.3.2版一起使用的以下Web伺服器：

| 平台 | 支援等級 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | 答：支援 |
| Microsoft IIS 10(Internet Information Server) | 答：支援 |
| Microsoft IIS 8.5(Internet Information Server) | Z:不支援 |

1. 以Apache httpd原始碼為基礎的Web伺服器，其支援等級將與其所依據的httpd版本相同。 如有疑問，請向Adobe洽詢有關個別伺服器產品的支援等級。 以下情況：

   1. HTTP伺服器僅使用官方的Apache來源散發，或
   1. HTTP伺服器是以其執行作業系統的方式傳送。 範例：IBM HTTP Server、Oracle HTTP Server

1. Dispatcher不適用於Windows作業系統的Apache 2.4.x。

## 支援的客戶端平台{#supported-client-platforms}

### 製作使用者介面{#supported-browsers-for-authoring-user-interface}支援的瀏覽器

Adobe Experience Manager使用者介面適用於下列用戶端平台。 所有瀏覽器都會使用預設的增效模組和附加元件集進行測試。

AEM使用者介面已針對較大螢幕（通常是筆記型電腦和桌上型電腦）和平板電腦外形規格（例如Apple iPad或Microsoft Surface）進行最佳化。 不支援電話外形。

>[!NOTE]
>
>**支援具快速發行週期的瀏覽器：**
>
>Mozilla Firefox、Google Chrome和Microsoft Edge發行版本每隔幾個月更新一次。 Adobe致力於提供Adobe Experience Manager更新，以維持下列對這些瀏覽器即將推出的版本的支援等級。

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

一般而言，AEM Sites提供的網站瀏覽器支援取決於AEM頁面範本的實作、設計和元件輸出，因此可由實作這些部分的一方控制。

### WebDAV客戶端{#webdav-clients}

**Microsoft Windows 7+**

若要成功連線至未使用SSL保護的AEM例項，Windows中必須啟用透過不安全網路的基本驗證。 這要求在WebClient的Windows註冊表中進行更改：

1. 找到註冊表子項：

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 使用值2或更多的值，將BasicAuthLevel註冊表項添加到此子鍵。

要提高Windows下WebDav客戶端的響應性——請參見[ Microsoft支援KB 2445570](https://support.microsoft.com/kb/2445570)

## 其他平台說明{#additional-platform-notes}

本節提供有關執行Adobe Experience Manager及其附加元件的特殊注意事項和詳細資訊。

### IPv4和IPv6 {#ipv-and-ipv}

Adobe Experience Manager(Instance, Dispatcher)的所有元素都可安裝在IPv4和IPv6網路中。

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

### AEM Dynamic Media Add-on {#requirements-for-aem-dynamic-media-add-on}的需求

AEM Dynamic Media預設為停用。 請參閱此處啟用動態媒體[。](/help/assets/config-dynamic.md#enabling-dynamic-media)

啟用動態媒體後，將適用下列其他技術需求。

>[!NOTE]
>
>如果您使用動態媒體——混合模式，則這些系統要求僅&#x200B;****&#x200B;適用；動態媒體——混合模式具有內嵌的影像伺服器，僅在特定作業系統上取得認證。
>
>對於執行Dynamic Media - Scene7模式（即&#x200B;**dynamicmedia_scene7**&#x200B;執行模式）的Dynamic Media客戶，不需額外的系統需求；只有與AEM相同的系統需求。 動態媒體- Scene7模式架構使用雲端影像服務，而非內嵌於AEM中的服務。

#### 硬體{#hardware}

下列硬體需求適用於Linux和Windows:

* 至少具有4個內核的Intel Xeon或AMD Opteron CPU
* 至少16 GB的記憶體

#### Linux {#linux}

如果您在Linux上使用Dynamic Media，則必須符合下列先決條件：

* RedHat Enterprise 7或CentOS 7及更新版本及最新的修補程式
* 64位元作業系統
* 已停用交換（建議）
* SELinux已停用（請參閱以下附註）

>[!NOTE]
>
>如果設定了LC_CTYPE不等於`en_US.UTF-8` ，則會阻止動態媒體工作。 要查看其值是什麼，請在命令提示符下鍵入&quot;locale&quot;。 如果未設定為該值，則在運行AEM之前，通過鍵入&quot;export LC_CTYPE=&quot;將LC_CTYPE環境變數設定為空字串。

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
>因此，Adobe建議您，如果您運行的系統使用&#x200B;**numa=off**&#x200B;引導選項關閉NUMA，以避免內核導致這些進程中斷。

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

### AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}的需求

<table>
 <tbody>
  <tr>
   <th><p><strong>產品</strong></p> </th>
   <th><p><strong>支援的格式，可轉換為PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017傳統追蹤</a> 最新版本</td>
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
>* PDF Generator需要32位元版本的[Acrobat 2017傳統音軌17.011.30078或更新版本](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html)才能執行轉換。
>* PDF Generator僅支援32位元零售版Microsoft Office Professional Plus和轉換所需的其他軟體。
>* PDF產生器不支援Microsoft Office 365。
>* OpenOffice專用的PDF產生器轉換僅在Windows和Linux上受支援。
>* OCR PDF、最佳化PDF和匯出PDF功能僅在Windows上受支援。
>* AEM Forms隨附Acrobat版本，以啟用PDF Generator功能。 在AEM Forms授權期間，僅能透過AEM Forms以程式設計方式存取搭售版本，以便與AEM Forms PDF Generator搭配使用。 如需詳細資訊，請參閱AEM Forms產品說明（依您的部署而定）（[On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)或[Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)）&quot;

   >
   >
* PDF Generator服務不支援Microsoft Windows 10。

>



### AEM Assets XMP中繼資料回寫{#requirements-for-aem-assets-xmp-metadata-write-back}的需求

支援XMP回寫功能，並啟用下列平台和檔案格式：

* **作業系統：**

   * Linux（64位元系統上支援32位元和32位元應用程式）。 如需安裝32位元用戶端程式庫的步驟，請參閱[如何在64位元RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)上啟用XMP擷取和回寫。

   * Windows Server
   * Mac OS X（64位元）

* **檔案格式**:JPEG、PNG、TIFF、PDF、INDD、AI和EPS。

### AEM Assets在Linux {#assetsonlinux}上處理大量中繼資料資產的需求

XMPFiles處理器過程需要庫GLIBC_2.14才能工作。 使用包含GLIBC_2.14的Linux內核，例如Linux內核3.1.x版。它可改善處理包含大量中繼資料（例如PSD檔案）的資產的效能。 使用舊版GLIBC會導致從`com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`開始的日誌出錯。
