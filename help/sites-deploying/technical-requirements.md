---
title: 技術需求
description: Adobe Experience Manager支援的使用者端和伺服器平台清單。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: fd54e28f5d774ca7ef42f2c81a7b57e125fdb1be
workflow-type: tm+mt
source-wordcount: '3706'
ht-degree: 4%

---

# 技術需求{#technical-requirements}

Adobe支援平台上的(AEM) Adobe Experience Manager，詳情請參閱本檔案的下列資訊。

如需瞭解任何與平台相關的問題，請聯絡平台廠商。

>[!NOTE]
>
>根據您安裝AEM的平台，使用者管理可能會有不同的需求集。

## 先決條件 {#prerequisites}

安裝Adobe Experience Manager的最低需求：

* 已安裝Java™ Platform、Standard Edition JDK或其他支援的[Java™虛擬機器器](#java-virtual-machines)
* Experience Manager Quickstart檔案（獨立JAR或Web應用程式部署WAR）

### 大小需求下限 {#minimum-sizing-requirements}

執行Adobe Experience Manager的最低需求：

* 安裝目錄中有5 GB的可用磁碟空間
* 2 GB記憶體

>[!NOTE]
>
>* 數位資產使用案例需要更多基本記憶體。 請參閱[部署與維護](/help/sites-deploying/deploy.md#default-local-install)以取得詳細資料。
>* [AEM Forms附加元件套件](/help/forms/using/installing-configuring-aem-forms-osgi.md)需要15 GB的暫存空間。
>

如需進一步資訊，請參閱[硬體調整指南](/help/managing/hardware-sizing-guidelines.md)。

### 支援層級 {#support-levels}

本檔案列出Adobe Experience Manager支援的使用者端和伺服器平台。 Adobe提供數個支援層級，針對建議設定和其他設定皆適用。

### 支援的設定 {#supported-configurations}

Adobe會推薦這些設定，並在標準軟體維護合約中提供完整支援。

<table>
 <tbody>
  <tr>
   <td>支援程度</td>
   <td>描述<br /> </td>
  </tr>
  <tr>
   <td><strong>A：支援</strong></td>
   <td>Adobe 為此設定提供完整的支援和維護。Adobe 品質保證流程涵蓋此設定。</td>
  </tr>
  <tr>
   <td><strong>R：限制支援</strong></td>
   <td>為確保客戶專案成功，Adobe在受限制的支援方案中提供完整支援，這要求符合特定條件。 R級支援需要正式的客戶請求和Adobe的確認。 如需更多詳細資訊，請聯絡 Adobe 客戶服務。</td>
  </tr>
 </tbody>
</table>

### 不支援的設定 {#unsupported-configurations}

| 支援程度 | 說明 |
|---|---|
| **Z：不支援** | 不支援此設定。Adobe 不會說明此設定是否適用，且不支援此設定。 |

## 支援平台 {#supported-platforms}

### Java™虛擬機器器 {#java-virtual-machines}

應用程式需要由Java™開發套件(JDK)散發提供的Java™虛擬機器器才能執行。

Adobe Experience Manager可搭配下列版本的Java™虛擬機器器運作：

>[!CAUTION]
>
>追蹤Java™廠商的安全性公告。 這麼做可確保生產環境的安全與保障。 此外，請務必安裝最新的Java™更新。

| **平台** | **支援等級** | **連結** |
|---|---|---|
| Oracle Java™ SE 21 JDK | Z：不支援`[1]` |
| Oracle Java™ SE 17 JDK | Z：不支援`[1]` |
| Oracle Java™ SE 11 JDK - 64位元 | A：支援的`[1]` | [下載](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=24<td>) |
| Oracle Java™ SE 10 JDK | Z：不支援`[1]` |
| Oracle Java™ SE 9 JDK | Z：不支援`[1]` |
| Oracle Java™ SE 8 JDK - 64位元 | A：支援的`[1]` | [下載](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=10) |
| IBM® J9 VM — 版本編號2.9、JRE 1.8.0 | A：支援的`[2]` |
| IBM® J9 VM — 版本編號2.8、JRE 1.8.0 | A：支援的`[2]` |
| Azul Zulu OpenJDK 11 - 64位元 | A：支援的`[3]` | |
| Azul Zulu OpenJDK 8 - 64位元 | A：支援的`[3]` | |

1. Oracle已改用Oracle Java™ SE產品的「長期支援」(LTS)模型。 Java™ 9、Java™ 10和Java™ 12是Oracle的非LTS版本(請參閱[Oracle Java™ SE支援藍圖](https://www.oracle.com/technetwork/java/eol-135779.html))。 若要在生產環境中部署AEM，Adobe僅支援Java™的LTS版本。 Adobe直接為所有使用Oracle Java™ SE技術的AEM客戶支援Oracle Java™ SE JDK的支援與發佈，包括公開更新結束之後的LTS版本的所有維護更新。 請參閱Adobe Experience Manager[的](assets/Java_Policy_for_Adobe_Experience_Manager.pdf)Java™支援原則。
   **重要：至少支援Oracle Java™ 11到2026年9月。 [Oracle 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/implementing/deploying/introduction/technical-requirements).**&#x200B;支援AEM Java™ 17和21

1. IBM® JRE僅與WebSphere®應用程式伺服器一起受支援。

1. 從6.5 SP9版開始的內部AEM部署支援Azul Zulu OpenJDK LTS版本。 Azul Zulu JDK LTS版本的支援和發佈必須由Adobe客戶直接從Azul授權。


### 儲存與持續性 {#storage-persistence}

有多種選項可用來部署Adobe Experience Manager的存放庫。 請參閱下列清單，瞭解支援的技術和儲存選項。

| **平台** | **說明** | **支援等級** |
|---|---|---|
| **含有TAR檔案的檔案系統** `[1]` | 存放庫 | A：支援 |
| **具有資料存放區的檔案系統** `[1]` | 二進位檔案 | A：支援 |
| 將二進位檔儲存在檔案系統`[1]`的TAR檔案中 | 二進位檔案 | Z：不支援用於生產 |
| Amazon S3 | 二進位檔案 | A：支援 |
| Microsoft® Azure Blob儲存體 | 二進位檔案 | A：支援 |
| MongoDB Enterprise 8.0 | 存放庫 | A：支援的`[3, 4]` |
| MongoDB Enterprise 7.0 | 存放庫 | A：支援的`[3, 4]` |
| MongoDB Enterprise 6.0 | 存放庫 | A：支援的`[3, 4]` |
| MongoDB Enterprise 5.0 | 存放庫 | A：支援的`[3, 4]` |
| MongoDB Enterprise 4.4 | 存放庫 | A：支援的`[2, 3, 4, 7]` |
| MongoDB Enterprise 4.2 | 存放庫 | A：支援的`[2, 3, 4, 7]` |
| MongoDB Enterprise 4.0 | 存放庫 | Z：不支援 |
| MongoDB Enterprise 3.6 | 存放庫 | Z：不支援 |
| MongoDB Enterprise 3.4 | 存放庫 | Z：不支援 |
| IBM® DB2® 10.5 | 存放庫和Forms資料庫 | R：受限制的支援`[5]` |
| Oracle資料庫12c (12.1.x) | 存放庫和Forms資料庫 | R：限制支援 |
| Oracle資料庫19c | 存放庫和Forms資料庫 | R：限制支援 |
| Microsoft® SQL Server 2016 | Forms資料庫 | A：支援 |
| Microsoft® SQL Server 2019 （已棄用） | Forms資料庫 | A：支援 |
| Microsoft® SQL Server 2022 | Forms資料庫 | A：支援 |
| **Apache Lucene （快速入門內建）** | 搜尋服務 | A：支援 |
| Apache Solr | 搜尋服務 | A：支援 |

1. 「檔案系統」包括符合POSIX的區塊儲存裝置。 包括網路儲存技術。 請注意，檔案系統效能可能會有所差異，並影響整體效能。 使用網路/遠端檔案系統載入測試AEM。
2. MongoDB Enterprise 4.2和4.4版至少需要AEM 6.5 SP9。
3. AEM不支援MongoDB Sharding。
4. 僅支援MongoDB Storage Engine WiredTiger。
5. 支援AEM Forms升級客戶。 新安裝不支援。
6. 僅適用於AEM Forms：
   * 移除對Oracle Database 12c的支援，並新增對Oracle Database 19c的支援。
   * 移除對Microsoft® SQL Server 2016的支援，並新增對Microsoft® SQL Server 2019和Microsoft® SQL Server 2022的支援。

>[!NOTE]
>
>請參閱[部署社群](/help/communities/deploy-communities.md)，瞭解有關AEM Communities功能的其他資訊。

>[!NOTE]
>
>MongoDB是協力廠商軟體程式，不包含AEM授權套件中。 如需詳細資訊，請參閱[MongoDB授權原則](https://www.mongodb.com/licensing/server-side-public-license/faq)頁面。
>
>若要透過MongoDB充分利用AEM部署，Adobe建議授權MongoDB企業版，以受益於專業支援。 如需詳細資訊，請參閱[建議的部署](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)。
>
>此授權包含標準復本集，該標準復本集由一個主要和兩個次要執行個體組成，可用於製作或發佈部署。
>
>如果您想要在MongoDB上同時執行author和publish，則必須購買兩個不同的授權。
>
>Adobe客戶服務可協助解決與AEM搭配使用MongoDB相關的資格確認問題。
>
>如需詳細資訊，請參閱[適用於Adobe Experience Manager的MongoDB頁面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。

<!--
>[!NOTE]
>
>Supported relational databases as listed above are third-party software and are not included in the AEM licensing package.
>
>To run AEM 6.5 with a supported relational database, a separate support contract with a database vendor is required. Adobe Customer Care assists qualifying issues related to the usage of relational databases with AEM 6.5.
>
>**Most relational databases are currently supported within Level-R on AEM 6.5, which comes with support criteria and a support program as stated in the Level-R description above.**-->

### Servlet引擎/應用程式伺服器 {#servlet-engines-application-servers}

Adobe Experience Manager能以獨立伺服器（快速入門JAR檔案）或協力廠商應用程式伺服器（WAR檔案）中的Web應用程式來執行。

需要的最低Servlet API版本是Servlet 3.1

| Platform | 支援程度 |
|---|---|
| **快速入門內建Servlet引擎(Jetty 9.4)** | A：支援 |
| Oracle WebLogic Server 12.2 (12cR2) | Z：不支援 |
| IBM® WebSphere® Application Server Continuous Delivery (LibertyProfile)，搭配Web Profile 7.0和IBM® JRE 1.8 | R：新合約`[2]`的限制支援 |
| IBM® WebSphere® Application Server 9.0和IBM® JRE 1.8 | R：新合約`[1]`的支援受限`[2]` |
| IBM® WebSphere®應用程式伺服器9.0.0.10 | R：新合約`[1]`的支援受限`[2]` |
| Apache Tomcat 8.5.x | R：新合約`[2]`的限制支援 |
| JBoss® EAP 7.2.x (含JBoss®應用程式伺服器) | Z：不支援 |
| JBoss® EAP 7.1.4含JBoss®應用程式伺服器 | R：新合約`[1]`的支援受限`[2]` |
| JBoss® EAP 7.0.x (含JBoss®應用程式伺服器) | Z：不支援 |
| JBoss® EAP 7.4含JBoss®應用程式伺服器<sup>[2] [3] [7] | A：支援 |

1. 建議使用AEM Forms進行部署。
2. 在應用程式伺服器上啟動AEM 6.5部署後，系統會移至「有限支援」。 現有客戶可升級至AEM 6.5，並繼續使用應用程式伺服器。 對於新客戶，如上方Level-R說明所述，隨附支援條件和支援計畫。
3. 僅適用AEM Forms：
   * 移除對JBoss® EAP 7.1.4的支援，並新增對JBoss® EAP 7.4.10的支援。

### 伺服器作業系統 {#server-operating-systems}

Adobe Experience Manager可與下列伺服器平台搭配使用以用於生產環境：

| **平台** | **支援等級** |
|---|---|
| **Linux®，根據Red Hat®分佈** | A：支援的`[1]` `[3]` |
| Linux®，根據Debian分佈，包括 烏本圖 | A：支援的`[1]` `[2]` |
| Linux®，根據SUSE®分佈 | A：支援的`[1]` |
| Microsoft® Windows Server 2022 | R：限制支援 |
| Microsoft® Windows Server 2019 `[4]` （已棄用） | R：新合約`[5]`的限制支援 |
| Microsoft® Windows Server 2016 `[4]` | R：新合約`[5]`的限制支援 |
| Microsoft® Windows Server 2012 R2 | Z：不支援 |
| Oracle Solaris™ 11 | Z：不支援 |
| IBM® AIX® 7.2 | Z：不支援 |

1. Linux® Kernel 2.6、3。 x， 4. x， 5. x， 6. x和9。 x包含來自Red Hat® Distribution的衍生程式，包括Red Hat® Enterprise Linux®、Oracle Linux®和Amazon Linux®。 只有Red Hat® Enterprise Linux® 7、Red Hat® Enterprise Linux® 8和Red Hat® Enterprise Linux® 9支援AEM Forms附加元件功能。
2. Ubuntu 20.04和SUSE® Linux® Enterprise Server 15 SP6 （64位元）支援AEM Forms。
3. Adobe Managed Services支援的Linux®發行版本。

   >[!NOTE]
   >
   >對於以Linux為基礎的伺服器（OSGI和JEE棧疊），AEM Forms附加元件需要以下執行階段相依性：
   >* glibc.x86_64 (2.17-196)
   >* libX11.x86_64 (1.6.7-4)
   >* zlib.x86-64 (1.2.7-17)
   >* libxcb.x86_64 (1.13-1.el7)
   >* libXau.x86_64 (1.0.8-2.1.el7)
   >* glibc-locale.x86_64 （2.17或更新版本）
   >* OpenSSL 3 （作業系統上的預設位置需要）。

   *若為OpenSSL 3安裝：程式庫libcrypto.so.3和libssl.so.3必須在LD_LIBRARY_PATH環境變數代表的預設程式庫路徑中可用。 如果它們安裝在非標準位置，請確定在啟動伺服器之前，將此路徑新增到LD_LIBRARY_PATH。*

4. Microsoft® Windows生產部署支援客戶升級至6.5版本及用於非生產用途。 AEM Sites和Assets會根據請求進行新部署。
5. Microsoft®視窗伺服器支援AEM Forms，但沒有支援層級R限制。
6. AEM Forms已移除對Microsoft® Windows Server 2016的支援。

>[!NOTE]
>
>如果您正在安裝AEM Forms 6.5，請確定您已安裝下列32位元Microsoft® Visual C++可轉散發套件。
>
>* Microsoft® Visual C++ 2008可轉散發套件
>* Microsoft® Visual C++ 2010可轉散發套件
>* Microsoft® Visual C++ 2012可轉散發套件
>* Microsoft® Visual C++ 2013可轉散發套件
>* Microsoft® Visual C++ 2019 （VC14.28或更新版本）可轉散發套件


### 虛擬與雲端運算環境 {#virtual-cloud-computing-environments}

支援Adobe Experience Manager在雲端運算環境的虛擬機器器中執行。 這些環境包括Microsoft®Azure和Amazon Web Services (AWS)，依照本頁所列的技術要求和Adobe的標準支援條款執行。

對於雲端原生環境，請檢閱AEM產品線的最新產品：Adobe Experience Manager as a Cloud Service 。 如需詳細資訊，請參閱[Adobe Experience Manager as a Cloud Service檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=zh-Hant)。

Adobe也提供Adobe Managed Services，可在Azure或AWS上部署AEM。 Adobe Managed Services為專家提供在這些雲端運算環境中部署和操作AEM的經驗和技能。 請參閱[有關Adobe Managed Services的其他檔案](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t)。

在Azure或AWS或任何其它雲端運算環境上部署AEM的所有其他情況下，虛擬運算環境會包含Adobe的支援。 該虛擬環境必須依照本頁所列的技術規格執行。 任何報告的問題與AEM在任一雲端環境中執行相關，必須可獨立於雲端運算環境特定的任何雲端服務重複產生。 換言之，除非本頁所列的技術需求(例如Azure Blob儲存或AWS S3)支援雲端服務，否則不會產生任何影響。

如需如何在Adobe Managed Services之外的Azure或AWS上部署AEM的建議，Adobe建議直接與雲端服務供應商合作。 或是與Adobe合作夥伴合作，支援在您選擇的雲端環境中部署AEM。 選取的雲端服務供應商或合作夥伴負責架構的規模規格、設計與實作，以符合您特定的效能、負載、擴充性與安全性需求。

### Dispatcher平台（網頁伺服器） {#dispatcher-platforms-web-servers}

Dispatcher是快取和負載平衡元件。 [下載最新的Dispatcher版本](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)。 Experience Manager 6.5需要Dispatcher版本4.3.2或更新版本。

下列Web伺服器支援與Dispatcher 4.3.2版搭配使用：

| Platform | 支援程度 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A：支援 |
| Microsoft® IIS 10 (Internet Information Server) | A：支援 |
| Microsoft® IIS 8.5 (Internet Information Server) | Z：不支援 |

1. 以Apache httpd原始程式碼為基礎建立的Web伺服器，與其所根據的httpd版本同樣具備支援。 如有疑問，請向Adobe索取確認個別伺服器產品相關的支援等級。 下列情況：

   1. HTTP伺服器是僅使用官方Apache來源發佈所建置，或
   1. HTTP伺服器是作為執行伺服器之作業系統的一部分所提供。 範例： IBM® HTTP伺服器、Oracle HTTP伺服器

1. Dispatcher不適用於適用於Windows作業系統的Apache 2.4.x。

## 支援的用戶端平台 {#supported-client-platforms}

### 編寫使用者介面的支援瀏覽器 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager使用者介面可與下列使用者端平台搭配使用。 所有瀏覽器均使用預設的外掛程式集和附加元件進行測試。

AEM使用者介面已針對大型熒幕（通常是筆記型電腦和桌上型電腦）和平板電腦外形規格(例如Apple iPad或Microsoft® Surface)進行最佳化。 不支援電話外形規格。

>[!NOTE]
>
>**支援發行週期快速的瀏覽器：**
>
>Mozilla Firefox、Google Chrome以及Microsoft®Edge每隔幾個月會發佈一次更新。 Adobe承諾為Adobe Experience Manager提供更新，以透過這些瀏覽器的未來版本維持以下所述的支援等級。

<table>
 <tbody>
  <tr>
   <td><strong>瀏覽器</strong></td>
   <td><strong>支援UI<br /> </strong></td>
   <td><strong>支援傳統UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome （長青）</strong></td>
   <td>A：支援</td>
   <td>A：支援</td>
  </tr>
  <tr>
   <td>Microsoft® Edge （長青）</td>
   <td>A：支援</td>
   <td>A：支援</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z：不支援</td>
   <td>Z：不支援</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A：支援</td>
   <td>A：支援</td>
  </tr>
  <tr>
   <td>Mozilla Firefox最後一個ESR [1]</td>
   <td>A：支援</td>
   <td>A：支援</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari （長青）</td>
   <td>A：支援</td>
   <td>A：支援</td>
  </tr>
  <tr>
   <td>macOS上的Apple Safari 11.x</td>
   <td>Z：不支援</td>
   <td>Z：不支援</td>
  </tr>
  <tr>
   <td>iOS 12.x上的Apple Safari</td>
   <td>答：支援[2]</td>
   <td>Z：不支援</td>
  </tr>
  <tr>
   <td>iOS 11.x上的Apple Safari</td>
   <td>Z：不支援</td>
   <td>Z：不支援</td>
  </tr>
 </tbody>
</table>

1. Firefox的延伸支援版本[深入瞭解mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)
1. 支援Apple iPad

### 網站支援的瀏覽器 {#supported-browsers-for-websites}

一般而言，AEM Sites轉譯的網站瀏覽器支援取決於AEM頁面範本的實作、設計和元件輸出，因此由實作這些部分的當事方控制。

### WebDAV使用者端 {#webdav-clients}

**Microsoft® Windows 7+**

當使用Microsoft® Windows 7+連線到不以SSL保護的AEM執行個體時，必須在Windows中啟用透過不保護網路的基本驗證。 它需要在WebClient的Windows登入中進行變更：

1. 找到登入子機碼：

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 使用2或以上的值將BasicAuthLevel登入專案新增至此子機碼。

## 其他平台注意事項 {#additional-platform-notes}

本節提供執行Adobe Experience Manager及其附加元件相關的特殊附註和更多詳細資訊。

### IPv4和IPv6 {#ipv-and-ipv}

Adobe Experience Manager (例項、Dispatcher)的所有元素都可以安裝在IPv4和IPv6網路上。

操作是順暢的，因為不需要特殊設定。 您可以視需要使用適合您網路型別的格式來指定IP位址。

當必須指定IP位址時，您可以（視需要）從下列專案選取：

* ipv6位址。 例如 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* ipv4位址。 例如 `https://123.1.1.4:4502`

* 伺服器名稱。 例如 `https://www.yourserver.com:4502`

* 會為IPv4和IPv6網路安裝解譯`localhost`的預設案例。 例如 `https://localhost:4502`

### AEM Dynamic Media附加元件的需求 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media預設為停用。 請參閱此處[啟用Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media)。

若啟用Dynamic Media，則適用下列額外技術要求。

>[!NOTE]
>
>若您使用Dynamic Media — 混合模式，這些系統需求&#x200B;**僅**&#x200B;適用；Dynamic Media — 混合模式具有內嵌影像伺服器，此伺服器僅能在特定作業系統上認證。
>
>對於執行Dynamic Media - Scene7模式（即&#x200B;**dynamicmedia_scene7**&#x200B;執行模式）的Dynamic Media客戶，沒有其他系統需求；只有與AEM相同的系統需求。 Dynamic Media - Scene7模式架構使用雲端型影像服務，而非內嵌於AEM中的服務。

#### 硬體 {#hardware}

下列硬體需求適用於Linux®和Windows：

* Intel Xeon®或AMD® Opteron CPU，至少配備四個核心
* 至少16 GB的RAM

#### Linux® {#linux}

如果您在Linux®上使用Dynamic Media，必須符合下列必要條件：

* Red Hat® Enterprise 7和更新版本，提供最新的修正修補程式
* 64位元作業系統
* 已停用交換（建議）
* SELinux已停用（請參閱以下說明）

>[!NOTE]
>
>如果地區設定設定設定為LC_CTYPE不等於`en_US.UTF-8`，就會導致Dynamic Media無法運作。 若要檢視其值，請在命令提示字元處輸入「locale」。 若未正確設定，請在執行AEM前輸入「export LC_CTYPE=」，將LC_CTYPE環境變數設為空字串。

>[!NOTE]
>
>**停用SELinux：** 「影像伺服」在開啟SELinux時無法運作。 此選項預設為啟用。 若要修正此問題，請編輯&#x200B;**/etc/selinux/config**&#x200B;檔案，並將SELinux值從下列位置變更：
>
>`SELINUX=enforcing` **至** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA架構：**&#x200B;處理器搭載AMD64和Intel® EM64T的系統通常設定為非統一記憶體架構(NUMA)平台。 也就是說，核心會在開機時建構多個記憶體節點，而不是建構單一記憶體節點。
>
>多節點結構可能會導致一或多個節點的記憶體耗盡，之後其他節點就會耗盡。 當記憶體用盡時，即使有可用的記憶體，核心仍可以決定終止處理序（例如，影像伺服器或平台伺服器）。
>
>因此，Adobe建議，若您執行的系統讓您使用&#x200B;**numa=off**&#x200B;開機選項來關閉NUMA，以避免核心造成這些處理程式停用。

>[!NOTE]
>
>**伺服器主機名稱必須解析：**&#x200B;請確定伺服器的主機名稱可解析為IP位址。 如果不可能，請將完整主機名稱和IP位址新增至&#x200B;**/etc/hosts**：
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* 交換空間至少相當於實體記憶體(RAM)容量的兩倍

若要在Windows上使用Dynamic Media，請安裝適用於x64和x86的Microsoft® Visual Studio 2010、2013和2015可轉散發套件。

若是Windows x64：

* 在[https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)取得Microsoft® Visual Studio 2010可轉散發套件
* 在[https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)取得Microsoft® Visual Studio 2013可轉散發套件
* 在[https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)取得Microsoft® Visual Studio 2015可轉散發套件

若是Windows x86：

* 在[https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)取得Microsoft® Visual Studio 2010可轉散發套件
* 在[https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)取得Microsoft® Visual Studio 2013可轉散發套件
* 在[https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)取得Microsoft® Visual Studio 2015可轉散發套件

#### macOS {#macos}

* 10.9.x和更新版本
* 僅支援試用和示範用途

### AEM Forms PDF Generator的需求 {#requirements-for-aem-forms-pdf-generator}

### PDF Generator的軟體支援 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>產品</strong></p> </th>
   <th><p><strong>支援的格式可轉換成PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020傳統路線</a>最新版本</td>
   <td>XPS、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017傳統路線</a>最新版本（已棄用）</td>
   <td>XPS、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 （已棄用）</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP、WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016 （已棄用）<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>公共</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016 （已棄用）<br /> </td>
   <td>公共</td>
  </tr>
  <tr>
   <td>Microsoft® 2016專案（已棄用）<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 （已棄用）</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator僅支援英文、法文、德文和日文版本的支援作業系統和應用程式。
>
>此外，
>
>* PDF Generator需要32位元版本的[Acrobat 2020 classic track version 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html)才能執行轉換。
>* PDF Generator僅支援32位元版本的Microsoft® Office Professional Plus及其他轉換所需的軟體。
>* Microsoft® Office Professional Plus安裝可能會使用零售或MAK/KMS/AD型大量授權。
>* 如果Microsoft® Office安裝由於任何原因（例如磁碟區授權安裝無法在指定期間內找到KMS主機）而停用或取消授權，轉換可能會失敗，直到安裝重新授權並重新啟用。
>* PDF Generator支援Linux®作業系統上的32位元版OpenOffice。
>* PDF Generator不支援Microsoft® Office 365。
>* 只有Windows和Linux®才支援OpenOffice適用的PDF Generator轉換。
>* 只有Windows支援OCR PDF、最佳化PDF和Export PDF功能。
>* Acrobat版本與AEM Forms搭配，可啟用PDF Generator功能。 在AEM Forms授權期間，僅以程式設計方式存取AEM Forms隨附的版本，以與AEM Forms PDF Generator搭配使用。 如需詳細資訊，請參閱根據您的部署([內部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)或[Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))提供的AEM Forms產品說明
>* PDF Generator服務不支援Microsoft® Windows 10。
>* PDF Generator無法使用Microsoft® Visio 2019轉換檔案。
>* PDF Generator無法使用Microsoft® Project 2019轉換檔案。

### AEM Forms Designer的需求 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server、Microsoft® Windows® 10或Windows® 11
* 1 GHz或更快的處理器，支援PAE、NX和SSE2。
* 32位元的1 GB RAM或64位元作業系統的2 GB RAM
* 16 GB磁碟空間，適用於32位元或20 GB磁碟空間，適用於64位元作業系統
* 顯示卡記憶體 — 128 MB的GPU （建議使用256 MB）
* 2.35 GB的可用硬碟空間
* 1024 X 768畫素或更高的熒幕解析度
* 視訊硬體加速（選購）
* Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC
* 安裝Designer的管理許可權
* Microsoft Visual C++ 2019 （VC 14.28或更新版本） 32位元AEM Forms Designer的32位元執行階段
* Microsoft Visual C++ 2019 （VC 14.28或更新版本）適用於64位元AEM Forms Designer的64位元執行階段（適用於OSGI和JEE棧疊）

[安裝及設定AEM Forms designer](/help/forms/using/installing-configuring-designer.md)

### AEM Assets XMP中繼資料回寫的需求 {#requirements-for-aem-assets-xmp-metadata-write-back}

下列平台和檔案格式支援並啟用XMP回寫：

* **作業系統：**

   * Linux® （64位元系統支援32位元和32位元應用程式）。

   * Windows Server
   * macOS X （64位元）

* **檔案格式**： JPEG、PNG、TIFF、PDF、INDD、AI和EPS。

### AEM Assets在Linux上處理中繼資料密集的資產的需求® {#assetsonlinux}

XMPFilesProcessor處理需要程式庫GLIBC_2.14才能運作。 使用包含GLIBC_2.14的Linux®核心，例如Linux®核心版本3.1.x。它可改善處理包含大量中繼資料的資產(例如PSD檔案)的效能。 使用舊版GLIBC會導致以`com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`開頭的記錄發生錯誤。
