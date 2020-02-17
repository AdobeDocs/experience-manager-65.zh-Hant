---
title: JEE上AEM Forms的一般安全性考量
seo-title: JEE上AEM Forms的一般安全性考量
description: 瞭解如何準備在JEE環境中強化您的AEM Forms。
seo-description: 瞭解如何準備在JEE環境中強化您的AEM Forms。
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# JEE上AEM Forms的一般安全性考量{#general-security-considerations-for-aem-forms-on-jee}

本文提供入門資訊，協助您準備強化AEM Forms環境。 其中包含JEE上AEM Forms、作業系統、應用程式伺服器和資料庫安全性的先決條件資訊。 在您繼續鎖定環境之前，請先查看此資訊。

## 特定於供應商的安全資訊 {#vendor-specific-security-information}

本節包含與作業系統、應用程式伺服器和資料庫相關的安全性資訊，這些資訊會併入您的AEM Forms on JEE解決方案。

使用本節中的連結可查找特定於供應商的作業系統、資料庫和應用程式伺服器的安全資訊。

### 作業系統安全性資訊 {#operating-system-security-information}

在確保作業系統安全時，請仔細考慮實施作業系統供應商描述的措施，包括：

* 定義和控制用戶、角色和權限
* 監控日誌和審核記錄
* 移除不必要的服務和應用程式
* 備份檔案

如需AEM Forms on JEE支援之作業系統的安全性資訊，請參閱表格中的資源：

<table>
 <thead>
  <tr>
   <th><p>作業系統</p> </th>
   <th><p>安全資源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">IBM AIX Security Benefits</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Windows Server 2016安全指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP或ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Red Hat Enterprise linux安全指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">安全性與強化准則</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7更新3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">第7版安全性指南</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup></sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">保護檔案</a></td>
  </tr>
 </tbody>
</table>

### 應用程式伺服器安全性資訊 {#application-server-security-information}

在保護應用程式伺服器的安全時，請仔細考慮實作您的伺服器廠商描述的措施，包括：

* 使用非顯而易見的管理員用戶名
* 禁用不必要的服務
* 保護控制台管理器
* 啟用安全Cookie
* 關閉不需要的埠
* 依IP位址或網域限制用戶端
* 使用Java™ Security manager以程式設計方式限制權限

如需AEM Forms on JEE支援之應用程式伺服器的安全性資訊，請參閱本表格中的資源。

<table>
 <thead>
  <tr>
   <th><p>應用程式伺服器</p> </th>
   <th><p>安全資源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Oracle webLogic®</p> </td>
   <td><p>如需瞭解WebLogic安全性，請造訪https://download.oracle.com/docs/ <a href="https://download.oracle.com/docs/"></a>。</p> </td>
  </tr>
  <tr>
   <td><p>IBM webSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">保護應用程式及其環境的安全</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security+subsystem+configuration">安全子系統配置</a></p> </td>
  </tr>
 </tbody>
</table>

### 資料庫安全資訊 {#database-security-information}

在保護資料庫時，請考慮實施資料庫供應商描述的措施，包括：

* 使用訪問控制清單(ACL)限制操作
* 使用非標準埠
* 在防火牆後隱藏資料庫
* 在將敏感資料寫入資料庫之前加密敏感資料（請參閱資料庫製造商的檔案）

如需AEM Forms on JEE支援之資料庫的安全性資訊，請參閱本表格中的資源。

<table>
 <thead>
  <tr>
   <th><p>資料庫</p> </th>
   <th><p>安全資源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">DB2產品系列庫</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td>在Web上搜索「SQL Server 2016:安全性」</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">MySQL 5.0一般安全性問題</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">MySQL 5.1一般安全性問題</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>請參閱 <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle 12g文檔中的「安全性」一章</a></p> </td>
  </tr>
 </tbody>
</table>

下表說明在AEM Forms on JEE設定程式期間需要開啟的預設埠。 如果您是透過https連線，請依此調整您的連接埠資訊和IP位址。 如需有關設定埠的詳細資訊，請參 *閱適用於您應用程式伺服器的「在JEE上安裝和部署AEM* Forms」檔案。

<table>
 <thead>
  <tr>
   <th><p>產品或服務</p> </th>
   <th><p>埠號</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebLogic Managed Server</p> </td>
   <td><p>配置期間由管理員設定</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere</p> </td>
   <td><p>9060，如果啟用「全域安全性」，則預設的SSL埠值為9043。</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>BAM伺服器</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SOAP</p> </td>
   <td><p>8880</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>MySQL</p> </td>
   <td><p>3306</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>運行LDAP伺服器的埠。 預設埠通常為389。 不過，如果您選取SSL選項，預設埠通常為636。 向LDAP管理員確認要指定的埠。</p> </td>
  </tr>
 </tbody>
</table>

### 配置JBoss以使用非預設HTTP埠 {#configuring-jboss-to-use-a-non-default-http-port}

JBoss Application server使用8080作為預設HTTP埠。 JBoss還具有預配置的埠8180 、 8280和8380 ，這些埠在jboss-service.xml檔案中加以注釋。 如果您的電腦上有已使用此連接埠的應用程式，請依照下列步驟變更AEM Forms on JEE使用的連接埠：

1. 開啟下列檔案以進行編輯：

   單伺服器安裝： [JBoss root]/standalone/configuration/standalone.xml

   群集安裝： [JBoss root]/domain/configuration/domain.xml

1. 將&lt;socket-binding>標 **簽中****** 的port屬性值變更為自訂的埠號。 例如，以下使用埠8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. 儲存並關閉檔案。
1. 重新啟動JBoss應用程式伺服器。

## AEM Forms on JEE安全性考量 {#aem-forms-on-jee-security-considerations}

本節說明您應瞭解的AEM Forms有關JEE特定安全性問題。

### 未在資料庫中加密電子郵件憑據 {#email-credentials-not-encrypted-in-database}

應用程式儲存的電子郵件憑證在儲存在JEE資料庫的AEM Forms之前，不會加密。 當您將服務端點配置為使用電子郵件時，作為該端點配置一部分使用的任何密碼資訊在儲存在資料庫中時都不會加密。

### 資料庫中權限管理的敏感內容 {#sensitive-content-for-rights-management-in-the-database}

AEM Forms on JEE使用JEE資料庫上的AEM Forms來儲存機密檔案金鑰資訊和其他用於原則檔案的加密資料。 保護資料庫不受入侵，有助於保護這些敏感資訊。

### 明文格式的密碼 {#password-in-clear-text-format-in-adobe-ds-xml}

用於在JEE上執行AEM Forms的應用程式伺服器需要有其專屬的組態，才能透過應用程式伺服器上設定的資料來源存取您的資料庫。 確保應用程式伺服器在資料源配置檔案中不會以明文形式公開資料庫密碼。

lc_[database].xml檔案不應包含明文格式的口令。 請洽詢您的應用程式伺服器廠商，瞭解如何為您的應用程式伺服器加密這些密碼。

>[!NOTE]
>
>JEE JBoss統包安裝程式上的AEM Forms會加密資料庫密碼。

預設情況下，IBM webSphere Application server和Oracle webLogic server可加密資料源密碼。 不過，請使用應用程式伺服器檔案進行確認，以確保發生此情況。

### 保護儲存在信任儲存中的私鑰 {#protecting-the-private-key-stored-in-trust-store}

匯入信任商店的私密金鑰或憑證會儲存在JEE資料庫的AEM Forms中。 採取適當的預防措施來保護資料庫，並將訪問權限限制到指定的管理員。
