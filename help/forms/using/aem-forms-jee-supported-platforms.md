---
title: JEE上支援的AEM Forms平台
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
source-git-commit: 73d5b894dfa1bbb3ae3f2973cc4f9db1ace90ef8
workflow-type: tm+mt
source-wordcount: '3515'
ht-degree: 1%

---


# JEE上支援的AEM Forms平台 {#supported-platforms-for-aem-forms-on-jee}

## 支援的平台 {#supported-platforms}

### 支援級別 {#support-levels}

JEE伺服器上的AEM Forms可以使用支援的作業系統、應用程式伺服器、資料庫、資料庫驅動程式、JDK、LDAP伺服器和電子郵件伺服器的任意組合來設定。

本文檔列出了JEE上AEM Forms支援的客戶端和伺服器平台。 Adobe為我們推薦的配置和其他配置提供了若干級別的支援。 該文檔還列出了其他受支援的軟體及其版本、異常、補丁程式定義和第三方軟體補丁程式支援策略。

>[!NOTE]
>
> - 有關受支援伺服器平台的例外的完整清單，請參見 [支援的伺服器平台的異常](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p)。
> - JEE上的AEM Forms僅支援受支援的作業系統和應用程式的英文、法文、德文和日文版本。


### 建議的配置 {#recommendedconfigurations}

Adobe推薦這些配置，並作為標準軟體維護協定的一部分提供完整或受限的支援：

<table>
 <tbody>
  <tr>
   <th>支援程度</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>答：支援<br /> </td>
   <td>Adobe為此配置提供全面支援和維護。 此配置由Adobe的質量保證流程覆蓋。</td>
  </tr>
  <tr>
   <td>R:限制支援</td>
   <td>Adobe在滿足某些先決條件後提供對此配置的完全支援。 與Adobe企業支援部門聯繫，瞭解先決條件並請求支援。</td>
  </tr>
  <tr>
   <td>L:有限支援</td>
   <td>Adobe在滿足某些先決條件後為此配置提供全面支援和維護。 並非所有功能在配置上都可用。 與Adobe企業支援部門聯繫，瞭解先決條件並請求支援。<br /> </td>
  </tr>
 </tbody>
</table>

### 不支援的配置 {#unsupported-configurations}

| 支援程度 | 說明 |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E:預計工作 | 預計該配置將起作用，沒有相反的報告。 |
| Z:不支援 | 不支援配置。 Adobe不會對配置是否有效發表任何聲明，也不支援它。 |

>[!NOTE]
>
> 為幫助AEM Forms客戶降低擁有成本、簡化部署體系結構並實現開發堆棧的現代化，Adobe Experience Manager企業平台正從基於應用伺服器的部署轉向基於OSGi的獨立部署。 Adobe繼續支援AEM FormsJEE堆棧，減少基礎設施元件。
>
> 隨著6.5版的發佈，不再支援在客戶中使用率最低的基礎架構元件，如下所示：
> ·IBMDB2資料庫
> ·IBMAIX和Sun Solaris作業系統
>
> 對於新安裝，建議在可行時在現代OSGi堆棧上部署AEM Forms，以利用響應性Adaptive Forms的最新創新，使用表單資料模型實現移動、多通道交互通信和後端資料整合。
>
> 我們認識到現有用戶需要繼續在JEE堆棧上部署AEM Forms。 在這些情形中，Adobe需要部署AEM FormsJEE，如本文檔所述。 如果您要升級到AEM6.5Forms，並在上一版的AEM Forms上使用不支援的平台，則可以聯繫Adobe支援以獲取升級到受支援平台的幫助。

### Java虛擬機(JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms需要運行Java虛擬機，該虛擬機由Java開發工具包(JDK)分發提供。 Adobe Experience Manager使用以下版本的Java虛擬機運行：

<table>
 <tbody>
  <tr>
   <th><p><strong>平台</strong></p> </th>
   <th><p><strong>支援程度</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>OracleJava™ SE 11（64位）</p> </td>
   <td><p>Z:不支援</p> </td>
   <td><p> </p> </td>
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
   <td>IBM® J9虛擬機(build 2.9, JRE 1.8.0)IBM® JDK SR6-FP26<br /> </td>
   <td>答：支援</td>
   <td>次要版本和更新</td>
  </tr>
  <tr>
   <td>IBMJAVA1.8.0_291(內部版8.0.6.30)<br /> </td>
   <td>答：支援</td>
   <td>次要版本和更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> - 建議從Java供應商跟蹤安全公告，以確保生產環境的安全和安全，並安裝最新的Java更新。
> - JEE上的AEM Forms僅支援生產環境上的64位JVM。


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
   <td><p>資料庫微內核（TAR MK檔案）</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 4.0（不建議使用） </p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.2 </p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>Oracle資料庫12c版本2(12.2.0.1.0)（不建議使用）</p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
   <tr>
   <td>Oracle資料庫19c(標準版、 Real Application Clusters(RAC)和企業版) </td>
   <td>儲存庫微核 </td>
   <td>支援</td>
  </tr>
  <tr>
   <td><p>MicrosoftSQL Server 2016（不建議使用）</p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td><p>MicrosoftSQL Server 2019</p> </td>
   <td><p>儲存庫微內核</p> </td>
   <td><p>支援</p> </td>
  </tr>
  <tr>
   <td>IBMDB2 11.1（不建議使用）</td>
   <td>儲存庫微內核</td>
   <td>R:限制支援</td>
  </tr>
  <tr>
   <td>MySQL 5.7.35（不建議使用） </td>
   <td>-</td>
   <td>R:限制支援</td>
  </tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R:限制支援</td>
  </tr>
 </tbody>
</table>

- IBMDB2不支援新安裝。 只支援現有客戶升級到AEM6.5Forms。
- MongoDB是第三方軟體，不包括在許AEM可包中。 有關詳細資訊，請參閱 [MongoDB許可策略](https://www.mongodb.org/about/licensing/) 的子菜單。
- 為了充分利用您的部署AEM,Adobe建議授予MongoDB Enterprise版本許可，以便從專業支援中獲益。
- Adobe客戶服務將幫助確定與MongoDB的使用有關的問AEM題。 有關詳細資訊，請參見 [用於Adobe Experience Manager的MongoDB頁](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。
- 「檔案系統」包括符合POSIX的塊儲存。 這包括網路儲存技術。 請注意，檔案系統效能可能會有所不同，並會影響整體效能。 建議將test與AEM網路/遠程檔案系統結合載入。
- 僅支援MongoDB儲存引擎WiredTiger。
- 中不支援MongoDB共用AEM。
- AEM Forms在JEE上不支援MySQL用於RDBMK持久性。
- 文檔安全模組不使用內容儲存庫。 這意味著，如果您只使用「文檔安全性」，並且不計畫使用「HTML工作區」、「HTML5」表單或自適應表單，則不要安裝「內容儲存庫」。
- AEM Forms在JEE上不支援使用MySQL來AEM保存儲存庫(CRX-Repository)。

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
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar(5.1.44版)</p> </td>
   <td><p>隨AEM Forms提供的JEE安裝</p> </td>
  </tr>
  <tr>
   <td>MicrosoftSQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驅動程式6.2.1.0（不建議使用） <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>隨AEM Forms提供，安裝JEE。</p> </td>
  </tr>
  <tr>
   <td>MicrosoftSQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC驅動程式8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>從Microsoft網站下載。</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle資料庫19.3.0.0.0 JDBC驅動程式</p> <p>ojdbc8.jar(19.3.0.0.0版)<br /> </p> </td>
   <td><p>從 <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Oracle網站</a>。</p> </td>
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
   <td>Service Pack和關鍵更新</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>答：支援</td>
   <td>Service Pack和關鍵更新</td>
  </tr>
  <tr>
   <td><p>JBoss®企業應用程式平台(EAP)7.1.4 <sup>[2] [3] [7]</sup> （不建議使用） </p> </td>
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
> IBM® WebSphere®群集僅在網路部署版中受支援。

### 伺服器作業系統 {#server-operating-systems}

#### 生產環境 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> 平台</strong></p> </th>
   <th><p><strong>支援級別</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
   <tr>
   <td>MicrosoftWindows Server 2019（64位）</td>
   <td>答：支援</td>
   <td>服務包和關鍵更新</td>
  </tr>
  <tr>
   <td>烏班圖20.04</td>
   <td>答：支援</td>
   <td>服務包和關鍵更新</td>
  </tr>
  <tr>
   <td> MicrosoftWindows Server 2016（64位）（不建議使用）</td>
   <td>答：支援</td>
   <td>服務包和關鍵更新</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 8（內核4.x）（64位）</p> </td>
   <td><p>答：支援</p> </td>
   <td><p>次要版本、累計更新和關鍵更新</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7（內核3.x）（64位）（不建議使用）</td>
   <td><p>答：支援</p> </td>
   <td><p>次要版本、累計更新和關鍵更新</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12（64位）</p> </td>
   <td><p>答：支援</p> </td>
   <td><p>服務包、累積補丁程式和關鍵安全更新</p> </td>
  </tr>
  <tr>
   <td>OracleLinux® 7 Update 3（64位）</td>
   <td>答：支援</td>
   <td>服務包、累積補丁程式和關鍵安全更新</td>
  </tr>
  <tr>
   <td>CentOS 7（64位）<sup> [6]</sup></td>
   <td>答：支援</td>
   <td>服務包、累積補丁程式和關鍵安全更新</td>
  </tr>
 </tbody>
</table>

#### 虛擬化環境 {#virtualized-environment}

您可以在物理機或虛擬環境上的JEE上運行AEM Forms。 但是，如果您在虛擬環境中與AEM Forms發生任何問題，請嘗試在物理機上複製該問題。 如果物理機上仍存在問題，請與Adobe支援聯繫以獲得解決方案。 有關無法在物理電腦上複製的問題，請與虛擬環境供應商聯繫。

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
   <td>E:預計工作</td>
   <td><p>Service Pack和關鍵更新</p> </td>
  </tr>
 </tbody>
</table>

### 支援的伺服器平台的異常 {#exceptions-to-supported-server-platforms}

在選擇平台以在JEE伺服器上設定AEM Forms時，請考慮以下例外。

1. AEM Forms在JEE上不支援IBM® WebSphere®和MySQL。
1. JEE上的AEM Forms不支援SUSE Linux Enterprise Server 12上的JBoss。 SUSE Linux Enterprise Server 12僅支援IBMWebSphere。
1. AEM FormsJEE不支援任何JDK(除OracleJava™ SE外)使用JBoss®。
1. AEM Forms在JEE上不支援除IBM® JDK外的任何帶IBM® WebSphere®的JDK。
1. CRX-repository支援TarMK、MongoDB和關係資料庫(RDBMK)類型的持久性。 應用程式伺服器和CRX-repository之間不能有兩個不同的資料庫系統。 但是，在JEE環境上的AEM Forms上，您可以將MongoMK與CRX-repository一起使用，並將受支援的關係資料庫與應用程式伺服器一起使用。
1. AEM Forms在JEE上不支援CentOS上的WebSphere應用程式伺服器。
1. AEM Forms在JEE上不支援基於JBoss角色的訪問控制(RBAC)。

此外，在選擇軟體以AdobeAEM Forms部署JEE時，請考慮以下幾點：

- JEE上的AEM Forms支援受支援軟體的指定主版本和次版本上的更新、修補程式和修復包。 但是，除非指定，否則不支援更新到下一個主版本或次版本。
- 基於群集的安裝不支援TarMK持久性。 有關支援的持久性的資訊，請參見 [為AEM Forms安裝選擇持久性類型](/help/forms/using/choosing-persistence-type-for-aem-forms.md)。
- AEM FormsJEE支援各種第三方軟體 [第三方軟體支援策略](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p)。
- AEM FormsJEE支援第三方供應商提供的平台。 第三方供應商可能不允許某些組合。 例如，許多供應商尚未通過Oracle對其應用程式伺服器進行認證。 因此，AEM Forms在JEE上也不支援這些組合。 為確保您選擇受支援的軟體版本，請檢查第三方供應商的支援清單。
- AEM Forms在JEE上不支援TarMK冷備用。
- AEM Forms的JEE不支援垂直聚類。
- JEE上的AEM Forms不支援群集環境上的MySQL資料庫。
- 有關已刪除或已更新的平台的清單，請參見 [AEM6.5Forms新功能摘要](../../forms/using/whats-new.md) 的子菜單。

### LDAP伺服器（可選） {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>產品（基本版本）</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft2016</td>
   <td>維護版本和修復包</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>功能包和臨時修復</p> </td>
  </tr>
 </tbody>
</table>

### 電子郵件伺服器（可選） {#email-servers-optional}

| 產品 |
| ----------------------- |
| MicrosoftExchange 2013 |
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
   <td>七點三</td>
  </tr>
  <tr>
   <td>IBM·菲萊內</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBMContent Manager伺服器（不建議使用） </td>
   <td>8.5修復包2</td>
  </tr>
  <tr>
   <td> IBMContent Manager客戶端（不建議使用）</td>
   <td>八點五 </td>
  </tr>
  <tr>
   <td>MicrosoftSharepoint</td>
   <td>2016<br /> </td>
  </tr>
 </tbody>
</table>

### 支援科爾多瓦 {#support-for-cordova}

AEM Forms應用現在支援Apache Cordova。 以下是支援的特定於平台的Cordova版本：

- 阿帕奇科爾多瓦6.4.0
- 科爾多瓦iOS4.3.0
- 科爾多瓦安卓6.0.0
- 科爾多瓦Windows 4.4.3

### 用於PDF發生器的軟體支援 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>產品</strong></p> </th>
   <th><p><strong>支援的轉換到PDF格式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat2020年經典賽道</a> 最新版本</td>
   <td>XPS，影像格式(BMP,GIF,JPEG,JPG, TIF,TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC),HTML, HTM, DWG, DXF和DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat2017年經典賽道</a> 最新版本（不建議使用）</td>
   <td>XPS，影像格式(BMP,GIF,JPEG,JPG, TIF,TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC),HTML, HTM, DWG, DXF和DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016（不建議使用）</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP,WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2019<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016（不建議使用）<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft®發行商2019<br /> </td>
   <td>酒吧</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016（不建議使用）<br /> </td>
   <td>酒吧</td>
  </tr>
  <tr>
   <td>Microsoft2019工程<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016（不建議使用）<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXD、XLS、XLS、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF和TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2（已棄用）</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXD、XLS、XLS、DOC、DOCX、PPT、PPTX、影像格式(BMP、GIF、JPEG、JPG、TIF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF和TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
> PDF生成器僅支援受支援的作業系統和應用程式的英文、法文、德文和日文版本。
>
> 此外：
>
> - PDF生成器需要32位版本 [Acrobat2020經典賽道20.004.30006版](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) 或Acrobat2017 17.011.30078版執行轉換。
> - PDF生成器僅支援32位Retail版的MicrosoftOffice Professional Plus和轉換所需的其他軟體。
> - PDF生成器不支援MicrosoftOffice 365。
> - OpenOffice的PDF生成器轉換僅在Windows和Linux上受支援。
> - OCRPDF、Optimize PDF和Export PDF功能僅在Windows上受支援。
> - Acrobat版本與AEM Forms捆綁，以啟用PDF生成器功能。 捆綁版本只應在AEM Forms許可證期間通過AEM Forms以寫程式方式訪問，以便與AEM FormsPDF生成器一起使用。 有關詳細資訊，請參閱按部署的AEM Forms產品說明([內部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) 或 [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
>
> - PDF生成器服務不支援MicrosoftWindows 10。


### 輔助功能支援例外 {#exceptions-to-accessibility-support}

以下AEM Forms子系統不是 [508](https://www.section508.gov/) 符合：

- 自適應Forms創作UI
- Forms經理創作UI
- 通信管理創作UI
- 管理UI（管理控制台UI）

## AEM Forms對JEE的系統要求 {#system-requirements-for-aem-forms-on-jee}

### 最低硬體要求 {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>平台</td>
   <td>最低硬體要求</td>
  </tr>
  <tr>
   <td>MicrosoftWindows伺服器</td>
   <td>英特爾®至強® E5-2680,2.4 GHz處理器或等效處理器<br /> VMWare ESX 5.1或更高版本<br /> 記憶體：6 GB（64位作業系統，帶64位JVM）<br /> 可用磁碟空間：15GB的臨時空間加22GB<br /> AEM Forms的JEE</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>英特爾至強E5-2670v2,1 vCPU,2.5 GHz處理器<br /> AWSM3.medium（3個ECU）<br /> 記憶體：6 GB（64位作業系統，帶64位JVM）<br /> 可用磁碟空間：6 GB的臨時空間加22 GB<br /> AEM Forms的JEE</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>英特爾至強E5-2670v2,1 vCPU,2.5 GHz處理器<br /> AWSM3.medium（3個ECU）<br /> 記憶體：6 GB（64位作業系統，帶64位JVM）<br /> 可用磁碟空間：6 GB的臨時空間加22 GB<br /> AEM Forms的JEE<br /> </td>
  </tr>
  <tr>
   <td>小型生產環境的硬體要求</td>
   <td>
    <ul>
     <li><strong>英特爾支援的環境</strong>:英特爾®至強® E5-2680,2.4 GHz或更高。 使用雙核處理器將進一步提高效能</li>
     <li><strong>記憶體： </strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

有關其他要求，請參閱：

- [JEE部署上單伺服器AEM Forms的系統要求](https://www.adobe.com/go/learn_aemforms_sysreq_single_65)
- [JEE部署群集AEM Forms的系統要求](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65)

## 在JEE上為AEM Forms提供支援的客戶端 {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>平台</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10（企業版、專業版、基本版）</p> <p>32位或64位版本</p> <p> </p> </td>
   <td>服務包和關鍵更新</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016伺服器</td>
   <td>服務包和關鍵更新</td>
  </tr>
 </tbody>
</table>

- 安裝的磁碟空間：僅Workbench為1.7 GB,Workbench、Designer和示例程式集的單個驅動器上為2.7 GB，用於完全安裝Workbench、Designer和示例程式集，400 MB用於臨時安裝目錄 — 200 MB用於用戶臨時目錄，200 MB。 如果所有這些位置都位於單個驅動器上，則安裝期間必須有1.5 GB的可用空間。 安裝完成後，將刪除複製到臨時目錄的檔案。

- 運行Workbench的記憶體：2 GB記憶體
- 硬體要求：英特爾®奔騰® 4或AMD等效處理器，1 GHz處理器
- 16位或更高顏色的顯示器解析度至少為1024 X 768像素或更高
- TCP/IPv4或TCP/IPv6網路連接到JEE伺服器上的AEM Forms
- 您必須具有管理權限才能在Windows上安裝Workbench。 如果您使用非管理員帳戶進行安裝，安裝程式將提示您輸入相應帳戶的憑據。

### 設計師 {#designer}

- Microsoft® Windows® 2016伺服器、Microsoft® Windows® 2019伺服器或Microsoft® Windows® 10
- 1 GHz或更快的處理器，支援PAE、NX和SSE2。
- 1 GB RAM（用於32位）或2 GB RAM（用於64位作業系統）
- 16 GB磁碟空間用於32位或20 GB磁碟空間用於64位作業系統
- 圖形記憶體 — 128 MB的GPU（建議256 MB）
- 2.35 GB的可用硬碟空間
- 1024 X 768像素或更高的顯示器解析度
- 視頻硬體加速（可選）
- Acrobat Pro DC,Acrobat Standard DC或Adobe Acrobat Reader DC。
- 安裝設計器的管理權限。

### Adobe Acrobat和Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat和Adobe Reader（基地）</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat2020（經典賽道）</td>
   <td>20.004.30006版或更高版本<br /> </td>
  </tr>
  <tr>
   <td>Acrobat2017（經典曲目）（不建議使用）</td>
   <td>17.011.30078版或更高版本<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
> Acrobat DC產品系列為Acrobat和Reader引入了兩種本質上不同的產品：&quot;經典&quot;和&quot;連續&quot; 有關詳細資訊和兩個軌道的比較，請參見 [https://www.adobe.com/go/acrobatdctracks。](https://www.adobe.com/go/acrobatdctracks)

### 瀏覽器 {#browsers}

#### 台式機 {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>瀏覽器（基本）</strong></p> </th>
   <th><p><strong>支援級別</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft邊（長青）</p> </td>
   <td><p>答：支援</p> </td>
   <td><p>服務包和更新</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox(Evergreen)</p> </td>
   <td><p>答：支援</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E:預計工作</td>
   <td> 所有更新</td>
  </tr>
  <tr>
   <td><p>Google克羅姆語（長青）</p> </td>
   <td><p>答：支援</p> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>GoogleChrome和MACOS X上的Firefox</td>
   <td>答：支援<br /> <br /> </td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Apple野生動物園11.x</td>
   <td>答：支援</td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Apple野生動物園12.x<br /> <br /> </td>
   <td>答：支援</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> 某些與瀏覽器相關的台式機例外如下：
>
> - 僅Macintosh OS X支援Safari。
> - Workspace支援Macintosh OS X 10.6和10.7上的Safari 5.1(含Acrobat DC或更高版本)。 有關Safari 5.1與AcrobatAdobe Reader的相容性的詳細資訊，請參見 [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html)。
> - Safari不支援管理控制台。
> - Tergementage Management不支援Windows® Internet Explorer 9.0 for AEM 6.1表單。
> - Forms門戶支援Internet Explorer 11上的JAWS 14.0螢幕閱讀器軟體，用於輔助功能。


#### Mobile客戶 {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>瀏覽器（基本）</strong></p> </th>
   <th><p><strong>支援的修補程式定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Android™ 4.1.2及以上版本上的Chrome</p> </td>
   <td><p>所有更新</p> </td>
  </tr>
  <tr>
   <td>iOS15.1及以上</td>
   <td>所有更新</td>
  </tr>
  <tr>
   <td>Microsoft邊<br /> </td>
   <td>所有更新<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4及更高版本上的Native Andriod瀏覽器</td>
   <td>所有更新</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> - Forms門戶僅在iPad的Safari上受支援。


### AEM Forms應用 {#aem-forms-workspace-app}

#### 移動設備支援 {#mobile-device-support}

AEM Forms應用可在以下平台上使用：

| **平台** | **支援的設備** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| AppleiOS | AppleiPhone,iPad,iPad航空和iPad迷你跑iOS15.1及以上 |
| Google安卓 | Android 5.1及更高版本。 AEM Forms的app通過7英吋和10英吋三星Galaxy平板電腦和流行智慧手機的認證。 |
| Microsoft窗 | Microsoft運行MicrosoftWindows 10作業系統的Surface設備、平板電腦、筆記型電腦和台式機。 |

### AdobeMicrosoft辦事處檔案安全擴展 {#adobe-rights-management-extension-for-microsoft-office}

按一下 [這裡](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) 查看Microsoft® OfficeAdobe文檔安全擴展的系統要求。

### 客戶端支援的異常 {#exceptions-to-client-support}

JEE上的AEM Forms支援受支援軟體的指定主版本和次版本上的更新、修補程式和修復包。 但是，除非指定，否則不支援更新到下一個主版本或次版本。

## 第三方修補程式支援策略 {#third-party-patch-support-policy}

AEM FormsJEE的第三方軟體要求記錄在其各自產品文檔的「系統要求」部分。 所有文檔都可以從 [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) 。

AEM Forms在JEE的第三方參考平台上說明了在開發和發佈JEE上的AEM Forms時當前的第三方基礎架構的特定補丁程式級別，以及該版本的AEM Forms在JEE上支援的基礎架構的最低補丁程式/服務包級別。

Adobe支援第三方供應商在其發佈時發佈的緊急或建議的修補程式，前提是第三方供應商保證向後相容AEM Forms在JEE上支援的版本。 Adobe將僅支援在AEM FormsJEE文檔中規定的最低修補程式級別之後發佈的修補程式。

在某些情況下，Adobe不支援更改主要功能的第三方更新，因此不支援完全向後相容。 有關支援的更新的詳細資訊，請參見 [支援的修補程式定義](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) 針對特定供應商產品和Adobe支援的修補程式類型。

在Adobe無法控制的情況下，聲稱向後相容的第三方補丁程式可能會對Adobe產品或客戶環境產生負面影響。 在這種情況下，Adobe建議客戶在將任何緊急補丁程式應用於關鍵系統之前，先評估第三方的任何緊急補丁程式的影響。 Adobe將與第三方合作，通過合理的業務努力解決此類問題，或通過正常的Adobe支援計畫，或通過第三方在他們的區域內糾正該問題。 這不能保證新發佈的受Adobe支援的第三方修補程式將按照供應商或AEM Forms在JEE上的記錄運行。

Adobe保留在任何給定時刻更改AEM Forms在JEE版本上支援的第三方參考平台及其支援的修補程式定義的權利。

通過搜索Adobe企業支援站點以查找與您的產品相關的知識庫文章，還可以找到有關第三方補丁程式的其他資訊。

## 平台更新 {#platform-updates}

2022年3月3日AEM Forms6.5.12.0版將以下平台標籤為不建議使用：

- MongoDB Enterprise 4.0
- IBMDB2 11.1
- Oracle資料庫12c版本2
- MySQL 5.7.35
- Microsoft® SQL Server JDBC驅動程式6.2.1.0
- JBoss®企業應用程式平台(EAP)7.1.4
- IBMContent Manager Server 8.5修復包2
- IBMContent Manager客戶端8.5
- MicrosoftSQL Server 2016

2021年9月7日AEM Forms6.5.10.0版將以下平台標籤為不建議使用：

- Adobe Acrobat2017 - [2017年Adobe Acrobat核心支助於2022年6月6日結束](https://helpx.adobe.com/tw/support/programs/eol-matrix.html)。
- MicrosoftWindows Server 2016（64位）
- Red Hat Enterprise Linux 7（內核3.x）（64位）
- Microsoft® Office 2016
- OpenOffice 4.1.2

>[!NOTE]
>
> 標籤為 [不建議使用AEM Forms6.5.12.0和6.5.10.0，在AEM Forms6.5 Service Pack 18(6.5.18.0版之前仍支援](https://helpx.adobe.com/support/programs/eol-matrix.html)。

## 修訂歷史記錄 {#revision-history}

- 2022年3月3日

   - 已刪除對以下內容的支援：
      - IBM® J9虛擬機(build 2.8, JRE 1.8.0)
      - Oracle資料庫12c版本1
      - Oracle資料庫18c
      - Oracle統一目錄(OUD)11g版本2
      - IBM蓮達樂9.0
      - IBMFilenet 5.2
      - AdobeFlash Player

- 2021年10月10日

   - 已將AEM Forms應用支援的iOS版更改為iOS15.1。以前的版本是iOS12

- 2021年9月7日
   - **平台更新**: [!DNL Adobe Experience Manager Forms] on JEE增加了對以下平台的支援：
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft Office 2019]
      - [!DNL Microsoft Windows Server 2019]
      - [!DNL RHEL8]
   - 2020年9月9日

      - 已將AEM Forms應用支援的iOS版更改為iOS12。 以前的版本是iOS11
