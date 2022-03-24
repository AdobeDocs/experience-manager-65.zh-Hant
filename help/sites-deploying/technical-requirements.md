---
title: 技術要求
seo-title: Technical Requirements
description: 支援的客戶端和伺服器平台的清單AEM。
seo-description: A list of the supported client and server platforms for AEM.
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 9e9a01cddf56d23bfe4e84812534c295be1595f4
workflow-type: tm+mt
source-wordcount: '3294'
ht-degree: 1%

---

# 技術要求{#technical-requirements}

Adobe支AEM持Adobe Experience Manager()在平台上，如本文檔的以下資訊所詳述。

有關與平台具體相關的任何問題，請與平台供應商聯繫。

>[!NOTE]
>
>根據您安裝的平台AEM，可能有不同的用戶管理要求。

## 必備條件 {#prerequisites}

安裝Adobe Experience Manager的最低要求：

* 已安裝的Java平台、Standard Edition JDK或其他受支援的 [Java虛擬機](#java-virtual-machines)
* Experience Manager快速啟動檔案（獨立JAR或Web應用程式部署WAR）

### 最小規模要求 {#minimum-sizing-requirements}

運行Adobe Experience Manager的最低要求：

* 安裝目錄中的5 GB可用磁碟空間
* 2 GB記憶體

>[!NOTE]
>
>* 數字資產使用案例需要更多基本記憶體。 請參閱 [部署和維護](/help/sites-deploying/deploy.md#default-local-install) 的雙曲餘切值。
>* [AEM Forms附加包](/help/forms/using/installing-configuring-aem-forms-osgi.md) 需要15 GB的臨時空間。
>


有關詳細資訊，請參見 [硬體調整指南](/help/managing/hardware-sizing-guidelines.md)。

### 支援級別 {#support-levels}

本文檔列出了Adobe Experience Manager支援的客戶端和伺服器平台。 Adobe提供多種級別的支援，包括建議的配置和其他配置。

### 支援的配置 {#supported-configurations}

Adobe推薦這些配置，並作為標準軟體維護協定的一部分提供全面支援。

<table>
 <tbody>
  <tr>
   <td>支援程度</td>
   <td>說明<br /> </td>
  </tr>
  <tr>
   <td><strong>答：支援</strong></td>
   <td>Adobe為此配置提供全面支援和維護。 此配置由Adobe的質量保證流程覆蓋。</td>
  </tr>
  <tr>
   <td><strong>R:限制支援</strong></td>
   <td>為確保客戶項目成功，Adobe在受限制的支援計畫中提供全面支援，這要求滿足特定條件。 R級支援需要正式的客戶請求和Adobe確認。 有關詳細資訊，請與Adobe客戶服務部門聯繫。</td>
  </tr>
 </tbody>
</table>

### 不支援的配置 {#unsupported-configurations}

| 支援程度 | 說明 |
|---|---|
| **Z:不支援** | 不支援配置。 Adobe不會對配置是否有效發表任何聲明，也不支援它。 |

## 支援的平台 {#supported-platforms}

### Java虛擬機 {#java-virtual-machines}

應用程式需要運行Java虛擬機，該虛擬機由Java開發工具包(JDK)分發提供。

Adobe Experience Manager使用以下版本的Java虛擬機運行：

>[!CAUTION]
>
>建議跟蹤Java供應商提供的安全公告，以確保生產環境的安全和安全，並安裝最新的Java更新。

| **平台** | **支援程度** | **連結** |
|---|---|---|
| OracleJava SE 11 JDK - 64位 | 答：支援 `[1]` | [下載](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| OracleJava SE 10 JDK | Z:不支援 `[1]` |
| OracleJava SE 9 JDK | Z:不支援 `[1]` |
| OracleJava SE 8 JDK - 64位 | 答：支援 `[1]` | [下載](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBMJ9 VM — 內部版本2.9,JRE 1.8.0 | 答：支援 `[2]` |
| IBMJ9 VM — 內部版本2.8,JRE 1.8.0 | 答：支援 `[2]` |
| Azul Zulu OpenJDK 11 - 64位 | 答：支援 `[3]` |  |
| Azul Zulu OpenJDK 8 - 64位 | 答：支援 `[3]` |  |

1. Oracle已經轉向了OracleJava SE產品的&quot;長期支援&quot;(LTS)模型。 Java 9、Java 10和Java 12是按Oracle排列的非LTS版本（請參見） [OracleJava SE支援路線圖](https://www.oracle.com/technetwork/java/eol-135779.html))。 要在生AEM產環境中部署，Adobe僅支援Java的LTS版本。 支援和分發OracleJava SE JDK，包括所有在公共更新結束之後的LTS版本的維護更新，將直接由使用OracleJava SE技術的所有客AEM戶Adobe支援。 查看 [OracleJava支援Adobe Experience Manager問答](assets/adobe-oracle-java-license-agreement.pdf) 的子菜單。

1. IBMJRE僅與WebSphere Application Server一起受支援。

1. 從6.5 SP9版開始的內部部署支援Azul Zulu OpenJDK LTSAEM版本。 支援和分發阿祖爾祖魯JDK LTS版本必須由我們的客戶直接從阿祖爾獲得許可。


### 儲存和持久性 {#storage-persistence}

部署Adobe Experience Manager儲存庫有各種選項。 有關支援的技術和儲存選項，請參見以下清單。

| **平台** | **說明** | **支援程度** |
|---|---|---|
| **具有TAR檔案的檔案系統** `[1]` | 存放庫 | 答：支援 |
| **具有資料儲存的檔案系統** `[1]` | 二進位檔案 | 答：支援 |
| 將二進位檔案儲存在檔案系統上的TAR檔案中 `[1]` | 二進位檔案 | Z:不支援生產 |
| AmazonS3 | 二進位檔案 | 答：支援 |
| MicrosoftAzure Blob儲存 | 二進位檔案 | 答：支援 |
| MongoDB Enterprise 4.2 | 存放庫 | 答：支援 `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | 存放庫 | Z:不支援 |
| MongoDB Enterprise 3.6 | 存放庫 | Z:不支援 |
| MongoDB Enterprise 3.4 | 存放庫 | Z:不支援 |
| IBMDB2 10.5 | 資料庫和Forms資料庫 | R:限制支援 `[5]` |
| Oracle資料庫12c(12.1.x) | 資料庫和Forms資料庫 | R:限制支援 |
| MicrosoftSQL Server 2016 | Forms資料庫 | 答：支援 |
| **Apache Lucene（Quickstart內置）** | 搜索服務 | 答：支援 |
| 阿帕奇索爾 | 搜索服務 | 答：支援 |

1. 「檔案系統」包括符合POSIX的塊儲存。 這包括網路儲存技術。 請注意，檔案系統效能可能會有所不同，並會影響整體效能。 建議將test與AEM網路/遠程檔案系統結合載入。
1. MongoDB Enterprise 4.2最AEM少需要6.5 SP9。
1. 中不支援MongoDB共用AEM。
1. 僅支援MongoDB儲存引擎WiredTiger。
1. 支援AEM Forms升級客戶。 不支援新安裝。

>[!NOTE]
>
>請參閱 [部署社區](/help/communities/deploy-communities.md) 有關AEM Communities能力的更多資訊。

>[!NOTE]
>
>MongoDB是第三方軟體，不包括在許AEM可包中。 有關詳細資訊，請參閱 [MongoDB許可策略](https://www.mongodb.org/about/licensing/) 的子菜單。
>
>要充分利用MongoDB的部AEM署，Adobe建議授權MongoDB企業版，以從專業支援中獲益。 請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) 的子菜單。
>
>許可證包括標準副本集，該副本集由一個主實例和兩個輔助實例組成，這些實例可用於作者或發佈部署。
>
>如果要同時運行作者和在MongoDB上發佈，則需要購買兩個單獨的許可證。
>
>Adobe客戶服務將幫助確定與MongoDB的使用有關的問AEM題。
>
>有關詳細資訊，請參見 [用於Adobe Experience Manager的MongoDB頁](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。

>[!NOTE]
>
>上面列出的受支援的關係資料庫是第三方軟體，不包括在許AEM可包中。
>
>要使用AEM受支援的關係資料庫運行6.5，需要與資料庫供應商簽訂單獨的支援合同。 Adobe客戶服務將幫助確定與使用6.5的關係資料庫AEM相關的問題。
>
>**大多數關係資料庫目前都受AEM到6.5版Level-R的支援，它附帶支援標準和支援計畫，如上面Level-R說明中所述。**

### Servlet引擎/應用程式伺服器 {#servlet-engines-application-servers}

Adobe Experience Manager可以作為獨立伺服器（快速啟動JAR檔案）或作為第三方應用程式伺服器（WAR檔案）中的Web應用程式運行。

需要的Servlet API最低版本是Servlet 3.1

| 平台 | 支援程度 |
|---|---|
| **Quickstart內置Servlet引擎(Jetty 9.4)** | 答：支援 |
| OracleWebLogic Server 12.2(12cR2) | Z:不支援 |
| IBMWebSphere Application Server Continuous Delivery(LibertyProfile)，帶Web Profile 7.0和IBMJRE 1.8 | R:新合同的限制支援 `[2]` |
| IBMWebSphere Application Server 9.0和IBMJRE 1.8 | R:新合同的限制支援 `[1]` `[2]` |
| Apache Tomcat 8.5.x | R:新合同的限制支援 `[2]` |
| JBoss EAP 7.2.x與JBoss應用程式伺服器 | Z:不支援 |
| JBoss EAP 7.1.4與JBoss應用程式伺服器 | R:新合同的限制支援 `[1]` `[2]` |
| JBoss EAP 7.0.x與JBoss應用程式伺服器 | Z:不支援 |

1. 建議部署AEM Forms。
1. 在應用AEM程式伺服器上啟動6.5部署將移至「受限支援」。 現有客戶可以升級到AEM6.5並繼續使用應用程式伺服器。 對於新客戶，它附帶支援標準和支援計畫，如上面R級說明中所述。

### 伺服器作業系統 {#server-operating-systems}

Adobe Experience Manager與以下生產環境伺服器平台協作：

| **平台** | **支援程度** |
|---|---|
| **Linux，基於Red Hat分發** | 答：支援 `[1]` `[3]` |
| Linux，基於Debian分發，包括 烏邦圖 | 答：支援 `[2]` |
| Linux，基於SUSE分發 | 答：支援 |
| MicrosoftWindows Server 2019 `[4]` | R:新合同的限制支援 |
| MicrosoftWindows Server 2016 `[4]` | R:新合同的限制支援 `[5]` |
| MicrosoftWindows Server 2012 R2 | Z:不支援 |
| OracleSolaris 11 | Z:不支援 |
| IBMAIX 7.2 | Z:不支援 |

1. Linux內核2.6、3.x和4.x包括來自Red Hat發行版的衍生產品，包括Red Hat Enterprise Linux、CentOS、OracleLinux和AmazonLinux。 AEM Forms附加功能僅在CentOS 7、Red Hat Enterprise Linux 7和Red Hat Enterprise Linux 8上受支援。
1. AEM Forms僅在Ubuntu 16.04 LTS上受支援
1. Adobe Managed Services支援的Linux分發
1. MicrosoftWindows生產部署支援升級到6.5和非生產用途的客戶。 新部署是應AEM Sites和資產部門的要求而部署的。
1. AEM Forms在MicrosoftWindow Server上不受支援級別R限制。


### 虛擬和雲計算環境 {#virtual-cloud-computing-environments}

支援Adobe Experience Manager在雲計算環境(如MicrosoftAzure和Amazon Web Services(AWS))上的虛擬機中運行，以符合本頁所列的技術要求，並且符合Adobe的標準支援條款。

Adobe建議使用Adobe托管服務在AEMAzure或AWS上部署。 Adobe Managed Services為專家提供了在這些雲計算環境中部署和運AEM營的經驗和技能。 請參閱 [有關Adobe Managed Services的其他文檔](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)。

在Azure或AEMAWS或任何其他雲計算環境上部署的所有其他情況下，將根據此頁上列出的技術規範將來自Adobe的支援包含到虛擬計算環境。 任何與在這些雲環境中運行相關的AEM報告問題都需要獨立於特定於雲計算環境的任何雲服務可重複，除非雲服務作為本頁所列技術要求的一部分特別受支援，例如Azure Blob儲存或AWSS3。

有關如何在Azure或AEMAWS（Adobe托管服務之外）上部署的建議，Adobe強烈建議直接與雲提供商或Adobe合作夥伴協作，支援在您選擇的雲環境AEM中部署。 選定的雲提供商或合作夥伴將負責規模規格、體系結構的設計和實施，以滿足您的特定效能、負載、可擴充性和安全性要求。

### Dispatcher平台（Web伺服器） {#dispatcher-platforms-web-servers}

Dispatcher是快取和負載平衡元件。 [下載最新的Dispatcher版本](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html)。 Experience Manager6.5要求Dispatcher版本4.3.2或更高版本。

支援以下Web伺服器與Dispatcher 4.3.2版一起使用：

| 平台 | 支援程度 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | 答：支援 |
| MicrosoftIIS 10(Internet Information Server) | 答：支援 |
| MicrosoftIIS 8.5(Internet Information Server) | Z:不支援 |

1. 基於Apache httpd原始碼構建的Web伺服器將具有與其所基於的httpd版本相同的支援級別。 如果有疑問，請向Adobe詢問與相應伺服器產品相關的支援級別的確認。 以下案例：

   1. HTTP伺服器僅使用官方的Apache源分發，或
   1. HTTP伺服器作為運行該伺服器的作業系統的一部分被傳送。 示例：IBMHTTP伺服器，OracleHTTP伺服器

1. Dispatcher不適用於Apache 2.4.x for Windows作業系統。

## 支援的客戶端平台 {#supported-client-platforms}

### 創作用戶介面支援的瀏覽器 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager用戶介面可與以下客戶端平台配合使用。 所有瀏覽器都使用預設的插件和載入項集進行測試。

用戶界AEM面針對較大螢幕（通常是筆記型電腦和台式電腦）和平板電腦外形規格(如AppleiPad或Microsoft表面)進行了優化。 不支援電話機外形。

>[!NOTE]
>
>**支援具有快速發佈週期的瀏覽器：**
>
>Mozilla Firefox、GoogleChrome和MicrosoftEdge版本每隔幾個月更新一次。 Adobe承諾為Adobe Experience Manager提供更新，以保持以下所列支援級別，即將推出的這些瀏覽器版本。

<table>
 <tbody>
  <tr>
   <td><strong>瀏覽器</strong></td>
   <td><strong>支援UI<br /> </strong></td>
   <td><strong>支援經典UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google克羅姆語（長青）</strong></td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Microsoft邊（長青）</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>MicrosoftInternet Explorer 11</td>
   <td>Z:不支援</td>
   <td>Z:不支援</td>
  </tr>
  <tr>
   <td>Mozilla Firefox(Evergreen)</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Mozilla Firefox上一個ESR [1]</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>Apple·薩法里(macOS)</td>
   <td>答：支援</td>
   <td>答：支援</td>
  </tr>
  <tr>
   <td>AppleSafari 11.x在macOS</td>
   <td>Z:不支援</td>
   <td>Z:不支援</td>
  </tr>
  <tr>
   <td>Apple·薩法里iOS12.x</td>
   <td>答：支援的[2]</td>
   <td>Z:不支援</td>
  </tr>
  <tr>
   <td>Apple·薩法里iOS11.x</td>
   <td>Z:不支援</td>
   <td>Z:不支援</td>
  </tr>
 </tbody>
</table>

1. Firefox的擴展支援版本 [在mozilla.org上瞭解有關此內容的詳細資訊](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. 支援AppleiPad

### 網站支援的瀏覽器 {#supported-browsers-for-websites}

一般來說，AEM Sites提供的網站的瀏覽器支援取決於頁面模板AEM、設計和元件輸出的實現，因此控制了這些部分的實施方。

### WebDAV客戶端 {#webdav-clients}

**MicrosoftWindows 7+**

要成功與MicrosoftWindows 7+連接到AEM未使用SSL保護的實例，必須在Windows中啟用基於不安全網路的基本身份驗證。 這要求更改WebClient的Windows註冊表：

1. 找到註冊表子項：

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 使用值2或更大值將BasicAuthLevel註冊表項添加到此子項。

要提高Windows下WebDav客戶端的響應能力 — 請參見 [Microsoft支援KB 2445570](https://support.microsoft.com/kb/2445570)

## 其他平台說明 {#additional-platform-notes}

本節提供有關運行Adobe Experience Manager及其載入項的特別說明和更詳細的資訊。

### IPv4和IPv6 {#ipv-and-ipv}

Adobe Experience Manager的所有元素（實例、調度程式）都可以安裝在IPv4和IPv6網路中。

操作是無縫的，因為不需要特殊配置。 如有必要，您只需使用適合網路類型的格式指定IP地址即可。

這意味著，當需要指定IP地址時，您可以從以下位置（根據需要）選擇：

* 例如IPv6地址 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* 例如IPv4地址 `https://123.1.1.4:4502`

* 例如， `https://www.yourserver.com:4502`

* 預設大小寫 `localhost` 將解釋為IPv4和IPv6網路安裝，例如， `https://localhost:4502`

### Dynamic Media附AEM件要求 {#requirements-for-aem-dynamic-media-add-on}

默AEM認情況下禁用Dynamic Media。 請參閱此處以 [啟用Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media)。

啟用Dynamic Media後，將適用以下附加技術要求。

>[!NOTE]
>
>這些系統要求 **僅** 使用Dynamic Media — 混合模式時應用；Dynamic Media — 混合模式具有嵌入式映像伺服器，該伺服器僅在某些作業系統上獲得認證。
>
>對於運行Dynamic Media-Scene7模式的Dynamic Media客戶(即， **動態媒體_場景7** runmode)，沒有其他系統要求；只與系統要求相同AEM。 Dynamic Media-Scene7模式體系結構使用基於雲的影像服務，而不是嵌入在中的服AEM務。

#### 硬體 {#hardware}

以下硬體要求適用於Linux和Windows:

* 至少具有4核的英特爾至強或AMD皓龍CPU
* 至少16 GB的RAM

#### Linux {#linux}

如果您在Linux上使用Dynamic Media，則需要滿足以下先決條件：

* RedHat Enterprise 7或CentOS 7及更高版本及最新修補程式
* 64位作業系統
* 已禁用交換（推薦）
* SELinux已禁用（請參閱以下注釋）

>[!NOTE]
>
>如果區域設定為LC_CTYPE不等於 `en_US.UTF-8`它阻止了Dynamic Media工作。 要查看其值是什麼，請在命令提示符下鍵入&quot;locale&quot;。 如果未設定為該值，則在運行前鍵入&quot;export LC_CTYPE=&quot;，將LC_CTYPE環境變數設定為空字串AEM。

>[!NOTE]
>
>**禁用SELinux:** 開啟SELinux時，影像服務不工作。 預設情況下，此選項處於啟用狀態。 要解決此問題，請編輯 **/etc/selinux/config** 檔案，並將SELinux值從：
>
>`SELINUX=enforcing` **至** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA體系結構：** 具有AMD64和英特爾EM64T處理器的系統通常配置為非統一記憶體體系結構(NUMA)平台，這意味著內核在啟動時構造多個記憶體節點，而不是構造單個記憶體節點。
>
>該多節點構造可導致在其它節點耗盡之前在一個或多個節點上耗盡記憶體。 當記憶體耗盡時，內核可以決定終止進程（例如，映像伺服器或平台伺服器），即使有可用記憶體。
>
>因此，Adobe建議，如果您運行的系統使用 **numa=off** 引導選項，以避免內核終止這些進程。

>[!NOTE]
>
>**伺服器主機名必須解析：** 確保伺服器的主機名可解析為IP地址。 如果不可能，請將完全限定的主機名和IP地址添加到 **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* MicrosoftWindows Server 2016
* 交換空間等於物理記憶體(RAM)的至少兩倍

要在Windows上使用Dynamic Media，請為x64和x86安裝MicrosoftVisual Studio 2010、2013和2015可再分發版。

對於Windows x64:

* 獲取MicrosoftVisual Studio 2010可再發行版 [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* 獲取MicrosoftVisual Studio 2013可再發行版 [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* 獲取MicrosoftVisual Studio 2015可再發行版 [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

對於Windows x86:

* 獲取MicrosoftVisual Studio 2010可再發行版 [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* 獲取MicrosoftVisual Studio 2013可再發行版 [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* 獲取MicrosoftVisual Studio 2015可再發行版 [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x及更高版本
* 僅支援試用和演示

### AEM FormsPDF發電機要求 {#requirements-for-aem-forms-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>產品</strong></p> </th>
   <th><p><strong>支援的轉換到PDF格式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat2017年經典賽道</a> 最新版本</td>
   <td>XPS，影像格式(BMP,GIF,JPEG,JPG, TIF,TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC),HTML, HTM, DWG, DXF和DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP,WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft®發行商2016<br /> </td>
   <td>酒吧</td>
  </tr>
  <tr>
   <td>Microsoft2016工程<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXD、XLS、XLS、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF和TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF生成器僅支援受支援的作業系統和應用程式的英文、法文、德文和日文版本。
>
>此外：
>
>* PDF生成器需要32位版本 [Acrobat2017經典曲目17.011.30078版或更高版本](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 的子菜單。
>* PDF生成器僅支援32位Retail版的MicrosoftOffice Professional Plus和轉換所需的其他軟體。
>* PDF生成器不支援MicrosoftOffice 365。
>* OpenOffice的PDF生成器轉換僅在Windows和Linux上受支援。
>* OCRPDF、Optimize PDF和Export PDF功能僅在Windows上受支援。
>* Acrobat版本與AEM Forms捆綁，以啟用PDF生成器功能。 捆綁版本只應在AEM Forms許可證期間通過AEM Forms以寫程式方式訪問，以便與AEM FormsPDF生成器一起使用。 有關詳細資訊，請參閱按部署的AEM Forms產品說明([內部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 或 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
>
>* PDF生成器服務不支援MicrosoftWindows 10。
>


### AEM Forms設計師要求 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016伺服器、Microsoft® Windows® 2019伺服器或Microsoft® Windows® 10
* 1 GHz或更快的處理器，支援PAE、NX和SSE2。
* 1 GB RAM（用於32位）或2 GB RAM（用於64位作業系統）
* 16 GB磁碟空間用於32位或20 GB磁碟空間用於64位作業系統
* 圖形記憶體 — 128 MB的GPU（建議256 MB）
* 2.35 GB的可用硬碟空間
* 1024 X 768像素或更高的顯示器解析度
* 視頻硬體加速（可選）
* Acrobat Pro DC,Acrobat Standard DC或Adobe Acrobat Reader DC。
* 安裝設計器的管理權限。

### AEM Assets元XMP資料回寫要求 {#requirements-for-aem-assets-xmp-metadata-write-back}

支XMP持並啟用以下平台和檔案格式的回寫：

* **作業系統：**

   * Linux（64位系統上支援32位和32位應用程式）。 有關安裝32位客戶端庫的步驟，請參見 [如何在XMP64位RedHat Linux上啟用提取和回寫](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)。

   * Windows伺服器
   * MacOS X（64位）

* **檔案格式**:JPEG、巴布亞紐幾內亞、TIFF、PDF、印度國防、人工智慧和EPS。

### AEM Assets在Linux上處理元資料密集型資產的要求 {#assetsonlinux}

XMPFilesProcessor進程需要庫GLIBC_2.14才能工作。 使用包含GLIBC_2.14的Linux內核，例如Linux內核3.1.x版。它改進了處理包含大量元資料的資產(如PSD檔案)的效能。 使用GLIBC的早期版本會導致日誌中的錯誤 `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`。
