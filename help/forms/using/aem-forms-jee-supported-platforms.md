---
title: AEM Forms on JEE的支援平台
seo-title: Supported Platforms for AEM Forms on JEE
description: 在JEE上安裝AEM Forms所需和支援的基礎架構元件清單
seo-description: List of infrastructure components required and supported for installing AEM Forms on JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 060bfb2ed3288b0ef9fbb5ba7f6b06ee027062b6
workflow-type: tm+mt
source-wordcount: '3624'
ht-degree: 1%

---


# AEM Forms on JEE的支援平台 {#supported-platforms-for-aem-forms-on-jee}

## 支援平台 {#supported-platforms}

<div class="preview">

AEM 6.5 Forms Service Pack 12(6.5.12.0)提供JEE上AEM 6.5 Forms的最新完整安裝程式。

Adobe建議使用 <a href="https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html"> AEM 6.5.12.0 JEE上的Forms </a> 完整安裝程式（於2022年3月03日發行），而非AEM 6.5。安裝程式（於2019年4月08日發行）。

</div>

### 支援層級 {#support-levels}

JEE伺服器上的AEM Forms可使用支援的作業系統、應用程式伺服器、資料庫、資料庫驅動程式、 JDK、LDAP伺服器和電子郵件伺服器的任意組合來設定。

本檔案列出JEE版AEM Forms支援的用戶端和伺服器平台。 Adobe提供數種支援級別，包括我們建議的配置和其他配置。 該文檔還列出了其他受支援的軟體及其版本、例外、補丁程式定義和第三方軟體補丁程式支援策略。

>[!NOTE]
>
> - 如需支援伺服器平台的例外狀況完整清單，請參閱 [受支援伺服器平台的例外情況](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
> - AEM Forms on JEE僅支援英文、法文、德文和日文版本的支援作業系統和應用程式。


### 建議的設定 {#recommendedconfigurations}

Adobe建議這些配置，並在標準軟體維護協定中提供完整或受限的支援：

<table>
 <tbody>
  <tr>
   <th>支援程度</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>答：支援<br /> </td>
   <td>Adobe對此配置提供完全支援和維護。 此設定由Adobe的品質保證程式涵蓋。</td>
  </tr>
  <tr>
   <td>R:受限支援</td>
   <td>Adobe在符合特定必要條件後，即可完全支援此設定。 聯絡Adobe企業支援，了解必要條件並提出支援要求。</td>
  </tr>
  <tr>
   <td>L:有限支援</td>
   <td>Adobe在滿足特定必要條件後，即可提供此設定的完整支援和維護。 並非所有功能都可在設定中使用。 聯絡Adobe企業支援，了解必要條件並提出支援要求。<br /> </td>
  </tr>
 </tbody>
</table>

### 不支援的配置 {#unsupported-configurations}

| 支援程度 | 說明 |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E:預期可運作 | 預期該配置會正常運作，而且沒有相反的報告。 |
| Z:不支援 | 不支援配置。 Adobe不會針對設定是否有效發表任何陳述，也不支援。 |

>[!NOTE]
>
> 為協助AEM Forms客戶降低擁有成本、簡化部署架構，並導入最新的開發堆疊，Adobe Experience Manager企業平台正從以應用程式伺服器為基礎的部署，轉向以獨立OSGi為基礎的部署。 Adobe持續支援AEM Forms JEE堆疊，並縮減基礎架構元件矩陣。
>
> 隨著6.5版的推出，在客戶中使用率最低的基礎架構元件不再受支援，如下所示：
> · IBM DB2資料庫
> · IBM AIX和Sun Solaris作業系統
>
> 若為全新安裝，建議在可行時將AEM Forms部署在現代OSGi堆疊上，以運用回應式Forms的最新創新功能，搭配行動裝置、多管道互動式通訊以及使用表單資料模型的後端資料整合。
>
> 我們了解現有使用者需要繼續在JEE堆疊上部署AEM Forms。 在這類情況下，Adobe需要依照本檔案所述，在支援的基礎架構上部署AEM Forms JEE。 如果您要升級至AEM 6.5 Forms，並在舊版AEM Forms上使用不支援的平台，請聯絡Adobe支援，以取得升級至支援平台的相關協助。

### Java虛擬機(JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms需要Java虛擬機才能運行，該虛擬機由Java開發套件(JDK)分發提供。 Adobe Experience Manager可搭配下列版本的Java虛擬機運作：

<table>
 <tbody>
  <tr>
   <th><p><strong>平台</strong></p> </th>
   <th><p><strong>支援程度</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr> 
   <td><p>OracleJava™ SE 11（64位） <sup> [8] </sup> </p>  </td>
   <td><p>答：支援</p> </td>
   <td><p>次要版本和更新 </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 11 - 64位</td>
   <td>Z:不支援</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 8 - 64位</td>
   <td>Z:不支援</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>OracleJava™ SE 8（64位）</td>
   <td>答：支援</td>
   <td>次要版本和更新</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine（版本編號2.9, JRE 1.8.0）IBM® JDK SR6-FP26<br /> </td>
   <td>答：支援</td>
   <td>次要版本和更新</td>
  </tr>
  <tr>
   <td>IBM JAVA1.8.0_291(build 8.0.6.30)<br /> </td>
   <td>答：支援</td>
   <td>次要版本和更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> - 建議您追蹤來自Java廠商的安全性佈告欄，以確保生產環境的安全性，並安裝最新的Java更新。
> - JEE版AEM Forms僅支援生產環境上的64位元JVM。


### 資料庫和CRX持久性 {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>平台</strong></p> </td>
   <td><p><strong> 說明</strong></p> </td>
   <td><p><strong>支援程度</strong></p> </td>
  </tr>
  <tr>
   <td><p>檔案系統</p> </td>
   <td><p>儲存庫微內核（TAR MK檔案）</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 4.0（已廢止） </p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.2 </p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>Oracle資料庫12c版本2(12.2.0.1.0)（已廢止）</p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
   <tr>
   <td>Oracle資料庫19c(標準、Real Application Clusters(RAC)和企業版) </td>
   <td>存放庫微內核 </td>
   <td>支援</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016（已過時）</p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2019</p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1（已過時）</td>
   <td>儲存庫微內核</td>
   <td>R:受限支援</td>
  </tr>
  <tr>
   <td>MySQL 5.7.35（已過時） </td>
   <td>-</td>
   <td>R:受限支援</td>
  </tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R:受限支援</td>
  </tr>
 </tbody>
</table>

- IBM DB2不支援全新安裝。 僅AEM 6.5 Forms的現有客戶才支援此功能。
- MongoDB是協力廠商軟體，不包含在AEM授權套件中。 如需詳細資訊，請參閱 [MongoDB許可策略](https://www.mongodb.org/about/licensing/) 頁面。
- 為了充分利用您的AEM部署，Adobe建議您授權MongoDB企業版本，以便從專業支援中受益。
- Adobe客戶服務將協助確認與搭配AEM使用MongoDB的相關問題。 如需詳細資訊，請參閱 [適用於Adobe Experience Manager的MongoDB頁](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
- 「檔案系統」包括符合POSIX的塊儲存。 這包括網路儲存技術。 請注意，檔案系統效能可能會有所不同，並影響整體效能。 建議結合網路/遠端檔案系統載入測試AEM。
- 僅支援MongoDB儲存引擎WiredTiger。
- AEM不支援MongoDB共用。
- JEE上的AEM Forms不支援MySQL用於RDBMK持續性。
- 檔案安全性模組不使用內容存放庫。 這表示，如果您只使用檔案安全性，且不打算使用HTML工作區、HTML5表單或最適化表單，則請勿安裝內容存放庫。
- JEE上的AEM Forms不支援使用MySQL來存放AEM存放庫(CRX-Repository)。

### 資料庫驅動程式 {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>資料庫 </th>
   <th><p><strong>平台</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar（5.1.44版）</p> </td>
   <td><p>在JEE安裝上隨AEM Forms提供</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驅動程式6.2.1.0（已廢止） <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>在JEE安裝上隨AEM Forms提供。</p> </td>
  </tr>
    <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驅動程式6.2.2.0 <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>在JEE安裝上隨AEM Forms提供。</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驅動程式8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>從Microsoft網站下載。</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle資料庫19.3.0.0.0 JDBC驅動程式</p> <p>ojdbc8.jar（19.3.0.0.0版）<br /> </p> </td>
   <td><p>從下載 <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Oracle網站</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 應用程式伺服器 {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> 平台</strong></p> </td>
   <td><p><strong>支援程度</strong></p> </td>
   <td><p><strong>支援的修補程式定義</strong></p> </td>
  </tr>
  <tr>
   <td>OracleWebLogic Server 12.2.1(12c R2)</td>
   <td>答：支援</td>
   <td>Service Pack和重要更新</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>答：支援</td>
   <td>Service Pack和重要更新</td>
  </tr>
  <tr>
   <td><p>JBoss®企業應用程式平台(EAP)7.1.4 <sup>[2] [3] [7]</sup> （已過時） </p> </td>
   <td><p>答：支援</p> </td>
   <td><p>支援的EAP版本的修補程式和累積修補程式</p> </td>
  </tr>
  <tr>
   <td><p>JBoss®企業應用程式平台(EAP)7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>答：支援</p> </td>
   <td><p>支援的EAP版本的修補程式和累積修補程式</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> IBM® WebSphere®叢集僅支援網路部署版本。

### 伺服器作業系統 {#server-operating-systems}

#### 生產環境 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> 平台</strong></p> </th>
   <th><p><strong>支援層級</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft Windows Server 2019（64位）</td>
   <td>答：支援</td>
   <td>服務包和重要更新</td>
  </tr>
  <tr>
   <td>烏本圖20.04</td>
   <td>答：支援</td>
   <td>服務包和重要更新</td>
  </tr>
  <tr>
   <td> Microsoft Windows Server 2016（64位元）（已過時）</td>
   <td>答：支援</td>
   <td>服務包和重要更新</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 8（內核4.x）（64位）</p> </td>
   <td><p>答：支援</p> </td>
   <td><p>次要版本、累積更新和重要更新</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7（內核3.x）（64位）（已廢止）</td>
   <td><p>答：支援</p> </td>
   <td><p>次要版本、累積更新和重要更新</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12（64位）</p> </td>
   <td><p>答：支援</p> </td>
   <td><p>服務包、累積修補程式和關鍵安全更新</p> </td>
  </tr>
  <tr>
   <td>OracleLinux® 7更新3（64位）</td>
   <td>答：支援</td>
   <td>服務包、累積修補程式和關鍵安全更新</td>
  </tr>
  <tr>
   <td>CentOS 7（64位）<sup> [6]</sup></td>
   <td>答：支援</td>
   <td>服務包、累積修補程式和關鍵安全更新</td>
  </tr>
 </tbody>
</table>

#### 虛擬化環境 {#virtualized-environment}

您可以在物理機器或虛擬環境上於JEE上執行AEM Forms。 不過，如果您在虛擬環境中遇到AEM Forms的任何問題，請嘗試在物理電腦上複製問題。 如果問題在物理電腦上持續存在，請與Adobe支援聯繫以獲得解決。 有關無法在物理電腦上複製的問題，請與虛擬環境供應商聯繫。

#### 開發環境 {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>平台（基本版本）</strong></p> </th>
   <th>支援程度</th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64位</p> </td>
   <td>E:預期可運作</td>
   <td><p>Service Pack和重要更新</p> </td>
  </tr>
 </tbody>
</table>

### 受支援伺服器平台的例外情況 {#exceptions-to-supported-server-platforms}

選擇平台以在JEE伺服器上設定AEM Forms時，請考量下列例外情況。

1. JEE上的AEM Forms不支援IBM® WebSphere®搭配MySQL。
1. JEE版AEM Forms不支援SUSE Linux Enterprise Server 12版的JBoss。 SUSE Linux Enterprise Server 12僅支援IBM WebSphere。
1. AEM Forms on JEE不支援使用JBoss®的任何JDK，但OracleJava™ SE除外。
1. AEM Forms on JEE不支援使用IBM® WebSphere®(IBM® JDK除外)的任何JDK。
1. CRX-repository支援TarMK、MongoDB類型和關係資料庫(RDBMK)的持久性。 應用程式伺服器和CRX-repository之間不能有兩個不同的資料庫系統。 不過，在JEE環境上的AEM Forms上，您可以搭配CRX存放庫使用MongoMK，以及搭配應用程式伺服器使用支援的關係資料庫。
1. JEE上的AEM Forms不支援CentOS上的WebSphere應用程式伺服器。
1. AEM Forms on JEE不支援JBoss角色型存取控制(RBAC)。
1. AEM Forms on JEE僅支援應用程式伺服器JBoss EAP 7.4的OracleJava™ SE 11（64位）SDK。

此外，在選擇軟體以AdobeJEE部署上的AEM Forms時，請考量下列幾點：

- AEM Forms on JEE支援在指定的主要和次要支援軟體版本之上更新、修補程式和修正套件。 但是，除非另有指定，否則不支援更新至下一個主要或次要版本。
- 基於群集的安裝不支援TarMK持久性。 有關支援的持久性的資訊，請參見 [為AEM Forms安裝選擇持續性類型](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms on JEE依我們的規定，支援各種協力廠商軟體 [第三方軟體支援策略](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
- AEM Forms on JEE根據協力廠商提供的支援支援支援平台。 協力廠商可能不允許某些組合。 例如，許多供應商尚未通過Oracle認證其應用程式伺服器。 因此，JEE上的AEM Forms也不支援這些組合。 為確保您選擇支援的軟體版本，請檢查第三方供應商的支援清單。
- JEE上的AEM Forms不支援TarMK冷備。
- AEM Forms on JEE不支援垂直叢集。
- JEE上的AEM Forms不支援群集環境上的MySQL資料庫。
- 如需已移除或已更新平台的清單，請參閱 [AEM 6.5 Forms新功能摘要](../../forms/using/whats-new.md) 檔案。

### LDAP伺服器（可選） {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>產品（基本版本）</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>維護髮行和修正套件</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>功能套件和臨時修正</p> </td>
  </tr>
 </tbody>
</table>

### 電子郵件伺服器（可選） {#email-servers-optional}

| 產品 |
| ----------------------- |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### 內容管理器和相應的連接器 {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>產品<br /> </strong></td>
   <td><strong>版本</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager伺服器（已過時） </td>
   <td>8.5 Fix Pack 2</td>
  </tr>
  <tr>
   <td> IBM Content Manager用戶端（已淘汰）</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2016年（已過時）<br /> </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2019年<br /> </td>
  </tr>
 </tbody>
</table>

### 支援Cordova {#support-for-cordova}

AEM Forms應用程式現在支援Apache Cordova。 以下是支援的平台特定版本Cordova:

- Apache Cordova 6.4.0
- 科爾多瓦iOS 4.3.0
- Cordova Android 6.0.0
- Cordova Windows 4.4.3

### PDF產生器的軟體支援 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>產品</strong></p> </th>
   <th><p><strong>支援的格式，可轉換為PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020傳統賽道</a> 最新版本</td>
   <td>XPS，影像格式(BMP,GIF,JPEG,JPG, TIF,TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC),HTML, HTM, DWG, DXF，和DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017傳統賽道</a> 最新版本（已過時）</td>
   <td>XPS，影像格式(BMP,GIF,JPEG,JPG, TIF,TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC),HTML, HTM, DWG, DXF，和DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016（已過時）</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2019<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016（已過時）<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016（已過時）<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® 2019工程<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>Microsoft® 2016專案（已淘汰）<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、XLS、XLSX、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JP2、J2K、J2C、JPC、HTM、TF和RTF)</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2（已過時）</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、XLS、XLSX、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JP2、J2K、J2C、JPC、HTM、TF和RTF)</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
> PDF產生器僅支援支援的作業系統和應用程式的英文、法文、德文和日文版本。
>
> 此外：
>
> - PDF產生器需要32位元版本 [Acrobat 2020 classic track 20.004.30006版](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 或Acrobat 2017 17.011.30078版，以執行轉換。
> - PDF生成器僅支援32位的Microsoft Office Professional Plus零售版和轉換所需的其他軟體。
> - PDF生成器不支援Microsoft Office 365。
> - 只有Windows和Linux支援OpenOffice的PDF生成器轉換。
> - OCRPDF、Optimize PDF和Export PDF功能僅在Windows上受支援。
> - Acrobat版本與AEM Forms搭配，以啟用PDF產生器功能。 套件版本在AEM Forms授權期間，僅能透過AEM Forms以程式設計方式存取，以便與AEM FormsPDF產生器搭配使用。 如需詳細資訊，請參閱根據您的部署的AEM Forms產品說明([內部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 或 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
>
> - PDF產生器服務不支援Microsoft Windows 10。


### 協助工具支援的例外情況 {#exceptions-to-accessibility-support}

下列AEM Forms子系統不是 [508](https://www.section508.gov/) 符合性：

- 適用性Forms編寫UI
- Forms Manager編寫UI
- 通信管理編寫UI
- 管理UI（管理控制台UI）

## JEE版AEM Forms的系統需求 {#system-requirements-for-aem-forms-on-jee}

### 最低硬體需求 {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>平台</td>
   <td>最低硬體需求</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>英特爾®至強® E5-2680、2.4 GHz處理器或同等處理器<br /> VMWare ESX 5.1或更高版本<br /> RAM:6 GB（64位作業系統，64位JVM）<br /> 可用磁碟空間：15GB的臨時空間加22GB<br /> 適用於JEE版AEM Forms</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>英特爾至強E5-2670v2,1 vCPU,2.5 GHz處理器<br /> AWS m3.medium（3個ECU）<br /> RAM:6 GB（64位作業系統，64位JVM）<br /> 可用磁碟空間：6 GB臨時空間加22 GB<br /> 適用於JEE版AEM Forms</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>英特爾至強E5-2670v2,1 vCPU,2.5 GHz處理器<br /> AWS m3.medium（3個ECU）<br /> RAM:6 GB（64位作業系統，64位JVM）<br /> 可用磁碟空間：6 GB臨時空間加22 GB<br /> 適用於JEE版AEM Forms<br /> </td>
  </tr>
  <tr>
   <td>小型生產環境的硬體需求</td>
   <td>
    <ul>
     <li><strong>英特爾供電環境</strong>:英特爾®至強® E5-2680,2.4 GHz或更高。 使用雙核處理器將進一步提高效能</li>
     <li><strong>記憶體： </strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

如需其他需求，請參閱：

- [JEE部署上單伺服器AEM Forms的系統需求](https://www.adobe.com/go/learn_aemforms_sysreq_single_65)
- [JEE部署上的叢集AEM Forms的系統需求](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65)

## JEE版AEM Forms的支援用戶端 {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>平台</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10（企業版、專業版、基本版）</p> <p>32位元或64位元版本</p> <p> </p> </td>
   <td>服務包和重要更新</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>服務包和重要更新</td>
  </tr>
 </tbody>
</table>

- 要安裝的磁碟空間：僅適用於Workbench的1.7 GB，在單一驅動器上為2.7 GB，以完整安裝Workbench、Designer和示常式式集400 MB用於臨時安裝目錄 — 在用戶臨時目錄中為200 MB，在Windows臨時目錄中為200 MB。 如果所有這些位置都駐留在單個驅動器上，則安裝期間必須有1.5 GB的可用空間。 安裝完成後，將刪除複製到臨時目錄的檔案。

- 運行Workbench的記憶體：2 GB記憶體
- 硬體需求：英特爾®奔騰® 4或AMD等效處理器，1 GHz處理器
- 至少1024 X 768像素或更高的監視器解析度，使用16位元顏色或更高
- TCP/IPv4或TCP/IPv6網路連線至JEE伺服器上的AEM Forms
- 您必須擁有管理權限，才能在Windows上安裝Workbench。 如果您使用非管理員帳戶進行安裝，安裝程式會提示您輸入適當帳戶的憑證。

### Designer {#designer}

- Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server或Microsoft® Windows® 10
- 支援PAE、NX和SSE2的1 GHz或更快的處理器。
- 1 GB的RAM（32位）或2 GB的RAM（64位作業系統）
- 32位或20 GB磁碟空間（64位作業系統）為16 GB磁碟空間
- 圖形記憶體 — 128 MB的GPU（建議256 MB）
- 2.35 GB可用硬碟空間
- 1024 X 768像素或更高的監視器解析度
- 視頻硬體加速（可選）
- Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC。
- 安裝Designer的管理權限。

### Adobe Acrobat和Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat和Adobe Reader（基地）</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020（傳統曲目）</td>
   <td>20.004.30006版或更新版本<br /> </td>
  </tr>
  <tr>
   <td>Acrobat 2017（傳統追蹤）（已過時）</td>
   <td>17.011.30078版或更新版本<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
> Acrobat DC產品系列針對Acrobat和Reader推出了兩種基本上不同的產品：「Classic」和「Continuous」。 如需這兩個追蹤的詳細資訊和比較，請參閱 [https://www.adobe.com/go/acrobatdctracks。](https://www.adobe.com/go/acrobatdctracks)

### 瀏覽器 {#browsers}

#### 台式機 {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>瀏覽器（基礎）</strong></p> </th>
   <th><p><strong>支援層級</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge(Evergreen)</p> </td>
   <td><p>答：支援</p> </td>
   <td><p>Service Pack和更新</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox(Evergreen)</p> </td>
   <td><p>答：支援</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E:預期可運作</td>
   <td> 所有更新</td>
  </tr>
  <tr>
   <td><p>Google Chrome(Evergreen)</p> </td>
   <td><p>答：支援</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Google OS X上的Chrome和Firefox</td>
   <td>答：支援<br /> <br /> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>答：支援</td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /> <br /> </td>
   <td>答：支援</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> 案頭的某些瀏覽器相關例外如下：
>
> - Safari僅在Macintosh OS X上受支援。
> - 工作區支援Macintosh OS X 10.6和10.7上的Safari 5.1(含Acrobat DC或更新版本)。 如需Safari 5.1與Acrobat Adobe Reader相容性的詳細資訊，請參閱 [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
> - Safari不支援Administration Console。
> - 通信管理不支援AEM 6.1表單的Windows® Internet Explorer 9.0。
> - Forms入口網站支援Internet Explorer 11上的JAWS 14.0螢幕助讀程式軟體，以提供協助工具。


#### 行動用戶端 {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>瀏覽器（基礎）</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Android™ 4.1.2及更新版本上的Chrome</p> </td>
   <td><p>所有更新</p> </td>
  </tr>
  <tr>
   <td>iOS 15.1及更新版本上的Safari</td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>所有更新<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4及更新版本上的原生Android瀏覽器</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> - Forms Portal僅支援iPad上的Safari。


### AEM Forms應用程式 {#aem-forms-workspace-app}

#### 行動裝置支援 {#mobile-device-support}

AEM Forms應用程式適用於下列平台：

| **平台** | **支援的裝置** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| AppleiOS | Apple iPhone、iPad、iPad Air和執行iOS 15.1及以上版本的iPad mini。 |
| Google Android | Android 5.1及更新版本。 AEM Forms應用在7英吋和10英吋的三星Galaxy平板電腦和流行智慧手機上獲得認證。 |
| Microsoft Windows | Microsoft執行Microsoft Windows 10作業系統的表面裝置、平板電腦、筆記型電腦和桌上型電腦。 |

### AdobeMicrosoft Office的Document Security Extension {#adobe-rights-management-extension-for-microsoft-office}

按一下 [此處](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) 了解Microsoft® Office的Adobe檔案安全性擴充功能的系統需求。

### 客戶支援例外 {#exceptions-to-client-support}

AEM Forms on JEE支援在指定的主要和次要支援軟體版本之上更新、修補程式和修正套件。 但是，除非另有指定，否則不支援更新至下一個主要或次要版本。

## 第三方修補程式支援策略 {#third-party-patch-support-policy}

JEE版AEM Forms的協力廠商軟體需求記錄在其各自產品檔案的「系統需求」一節中。 所有檔案皆可從 [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

JEE第三方參考平台上的AEM Forms會說明在JEE上開發和發行AEM Forms期間，以及該版本JEE上的AEM Forms所支援基礎架構的最低修補程式/服務包層級，所支援的協力廠商基礎架構的特定修補程式層級。

Adobe在第三方廠商發佈時，支援其發佈的緊急或建議修補程式，假設第三方廠商保證與AEM Forms on JEE支援的版本回溯相容。 Adobe僅支援在JEE檔案中AEM Forms所述的最低修補程式級別之後發行的修補程式。

在某些情況下，Adobe不支援會變更主要功能的協力廠商更新，因此不支援完全回溯相容性。 如需支援更新的詳細資訊，請參閱 [支援的修補程式定義](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) 針對特定供應商產品和補丁程式類型Adobe支援。

在Adobe無法控制的情況下，聲稱向後相容性的第三方補丁程式可能會對Adobe產品或客戶環境產生負面影響。 在這種情況下，Adobe建議客戶在將任何緊急補丁程式應用到關鍵系統之前，先評估這些補丁程式對第三方的影響。 Adobe將與第三方合作，通過正常的Adobe支援計畫或第三方在其補丁程式中糾正該問題，通過合理的業務努力解決此類問題。 這無法保證新發行且受Adobe支援的協力廠商修補程式，能如廠商所記錄或JEE上的AEM Forms所運作。

Adobe保留在任何指定時間點變更AEM Forms JEE版本支援的第三方參考平台及其支援的修補程式定義的權利。

有關第三方修補程式的其他資訊，也可通過搜索Adobe企業支援站點中與產品相關的知識庫文章來找到。

## 平台更新 {#platform-updates}

2022年6月2日發行的AEM Forms 6.5.13.0版本將下列平台標示為已過時：

- MicrosoftSharePoint2016

2022年3月3日發行的AEM Forms 6.5.12.0版本將下列平台標示為已過時：

- MongoDB Enterprise 4.0
- IBM DB2 11.1
- Oracle資料庫12c版本2
- MySQL 5.7.35
- Microsoft® SQL Server JDBC驅動程式6.2.1.0
- JBoss®企業應用程式平台(EAP)7.1.4
- IBM Content Manager Server 8.5 Fix Pack 2
- IBM Content Manager Client 8.5
- Microsoft SQL Server 2016

2021年9月7日發行的AEM Forms 6.5.10.0版本將下列平台標示為已過時：

- Adobe Acrobat2017 - [對Adobe Acrobat 2017的核心支援將於2022年6月6日終止](https://helpx.adobe.com/tw/support/programs/eol-matrix.html).
- Microsoft Windows Server 2016（64位）
- Red Hat Enterprise Linux 7（內核3.x）（64位）
- Microsoft® Office 2016
- OpenOffice 4.1.2

>[!NOTE]
>
> 標示為 [在AEM Forms 6.5.12.0和6.5.10.0中遭取代，在AEM Forms 6.5 Service Pack 18(6.5.18.0)版本之前，仍持續支援](https://helpx.adobe.com/support/programs/eol-matrix.html).

## 修訂歷史記錄 {#revision-history}

- 2022年9月01日

   - 新增對OracleJava™ SE 11（64位）SDK的支援，用於應用程式伺服器JBoss EAP 7.4。

- 2022年3月03日

   - 移除對下列項目的支援：
      - IBM® J9 Virtual Machine（版本編號2.8、JRE 1.8.0）
      - Oracle資料庫12c版本1
      - Oracle資料庫18c
      - Oracle統一目錄(OUD)11g第2版
      - IBM Lotus Domino 9.0
      - IBM Filenet 5.2
      - AdobeFlash Player

- 2021年10月10日

   - 將支援的AEM Forms應用程式iOS版本變更為iOS 15.1。舊版為iOS 12。

- 2021年9月07日
   - **平台更新**: [!DNL Adobe Experience Manager Forms] on JEE已新增對下列平台的支援：
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft Office 2019]
      - [!DNL Microsoft Windows Server 2019]
      - [!DNL RHEL8]
   - 2020年9月09日

      - 將支援的iOS for AEM Forms App版本變更為iOS 12。 舊版是iOS 11。
