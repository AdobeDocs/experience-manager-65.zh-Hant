---
title: JEE版AEM Forms的一般安全性考量事項
seo-title: General Security Considerations for AEM Forms on JEE
description: 了解如何準備在JEE環境中強化AEM Forms。
seo-description: Learn how to prepare for hardening your AEM Forms on JEE environment.
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
role: Admin
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---

# JEE版AEM Forms的一般安全性考量事項{#general-security-considerations-for-aem-forms-on-jee}

本文提供入門資訊，協助您為強化AEM Forms環境做好準備。 其中包含JEE上AEM Forms、作業系統、應用程式伺服器和資料庫安全性的先決條件資訊。 請先查看此資訊，然後再繼續鎖定環境。

## 特定於供應商的安全資訊 {#vendor-specific-security-information}

本節包含與作業系統、應用程式伺服器和資料庫相關的安全性資訊，這些資訊已整合至您的JEE AEM Forms解決方案中。

使用本節中的連結查找作業系統、資料庫和應用程式伺服器的特定於供應商的安全資訊。

### 作業系統安全資訊 {#operating-system-security-information}

保護作業系統時，請仔細考慮實施作業系統供應商描述的措施，包括：

* 定義和控制用戶、角色和權限
* 監控日誌和審核跟蹤
* 刪除不必要的服務和應用程式
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
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">IBM® AIX®安全優勢</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Windows Server 2016安全指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP或ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">《 Red Hat® Enterprise Linux®安全指南》</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris™ 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">安全性與強化准則</a></p> </td>
  </tr>
  <tr>
   <td>OracleLinux® 7更新3</td>
   <td><a href="https://docs.oracle.com/en/operating-systems/oracle-linux/7/security/" target="_blank">第7版安全性指南</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">保護檔案</a></td>
  </tr>
 </tbody>
</table>

### 應用程式伺服器安全資訊 {#application-server-security-information}

保護應用程式伺服器時，請仔細考慮實施伺服器供應商描述的措施，包括：

* 使用不明顯的管理員用戶名
* 禁用不必要的服務
* 保護主控台管理員
* 啟用安全Cookie
* 關閉不需要的埠
* 按IP地址或域限制客戶端
* 使用Java™ Security Manager以程式設計方式限制權限

如需JEE上AEM Forms支援之應用程式伺服器的安全性資訊，請參閱下表中的資源。

<table>
 <thead>
  <tr>
   <th><p>應用程式伺服器</p> </th>
   <th><p>安全資源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>OracleWebLogic®</p> </td>
   <td><p>在以下位置搜索了解WebLogic安全 <a href="https://docs.oracle.com/">https://docs.oracle.com/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM® WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">保護應用程式及其環境</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security%20subsystem%20configuration.html">安全子系統配置</a></p> </td>
  </tr>
 </tbody>
</table>

### 資料庫安全資訊 {#database-security-information}

保護資料庫時，請考慮實施資料庫供應商描述的措施，包括：

* 限制使用訪問控制清單(ACL)的操作
* 使用非標準埠
* 在防火牆後隱藏資料庫
* 在將敏感資料寫入資料庫之前對其進行加密（請參閱資料庫製造商的文檔）

如需AEM Forms JEE上支援之資料庫的安全性資訊，請參閱下表中的資源。

<table>
 <thead>
  <tr>
   <th><p>資料庫</p> </th>
   <th><p>安全資源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">DB2®產品系列庫</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016</p> </td>
   <td>在Web上搜索「SQL Server 2016:安全性」</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">MySQL 5.0一般安全問題</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">MySQL 5.1一般安全問題</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>請參閱 <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle12g檔案</a></p> </td>
  </tr>
 </tbody>
</table>

下表說明在AEM Forms on JEE設定程式期間需要開啟的預設埠。 如果您是通過https連接，請相應地調整埠資訊和IP地址。 有關配置埠的詳細資訊，請參閱 *在JEE上安裝和部署AEM Forms* 應用程式伺服器的文檔。

<table>
 <thead>
  <tr>
   <th><p>產品或服務</p> </th>
   <th><p>埠號</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss®</p> </td>
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
   <td>&gt;<p>WebSphere®</p> </td>
   <td><p>9060，如果啟用了「全局安全性」，則預設SSL埠值為9043。</p> <p>9080</p> </td>
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
   <td>&gt;<p>DB2®</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>運行LDAP伺服器的埠。 預設埠通常為389。 不過，如果您選取SSL選項，預設連接埠通常為636。 向LDAP管理員確認要指定的埠。</p> </td>
  </tr>
 </tbody>
</table>

### 將JBoss®配置為使用非預設HTTP埠 {#configuring-jboss-to-use-a-non-default-http-port}

JBoss® Application Server使用8080作為預設HTTP埠。 JBoss®還具有預先配置的埠8180、8280和8380，這些埠在jboss-service.xml檔案中注釋。 如果您的電腦上有已使用此埠的應用程式，請依照下列步驟變更AEM Forms在JEE上使用的埠：

1. 開啟下列檔案進行編輯：

   單伺服器安裝： [JBoss®根]/standalone/configuration/standalone.xml

   群集安裝： [JBoss®根]/domain/configuration/domain.xml

1. 變更 **埠** 屬性 **&lt;socket-binding>** 標籤為自訂連接埠號。 例如，下列程式使用埠8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. 儲存並關閉檔案。
1. 重新啟動JBoss®應用程式伺服器。

## AEM Forms JEE安全性考量事項 {#aem-forms-on-jee-security-considerations}

本節說明一些您應了解之JEE專用AEM Forms安全性問題。

### 資料庫中未加密電子郵件憑據 {#email-credentials-not-encrypted-in-database}

應用程式儲存的電子郵件憑證在儲存於JEE資料庫的AEM Forms中之前，不會先加密。 將服務端點配置為使用電子郵件時，作為該端點配置一部分使用的任何密碼資訊在儲存到資料庫時都不會加密。

### 資料庫中Rights Management的敏感內容 {#sensitive-content-for-rights-management-in-the-database}

AEM Forms on JEE使用AEM Forms on JEE資料庫來儲存敏感檔案密鑰資訊以及用於政策檔案的其他加密材料。 保護資料庫免受入侵，有助於保護此敏感資訊。

### 明文格式的密碼 {#password-in-clear-text-format-in-adobe-ds-xml}

在JEE上執行AEM Forms的應用程式伺服器需要其自己的設定，才能透過應用程式伺服器上設定的資料來源存取您的資料庫。 確保應用程式伺服器不會在其資料源配置檔案中以明文形式公開資料庫密碼。

lc_[資料庫].xml檔案不應包含明文格式的密碼。 請向應用程式伺服器供應商咨詢如何為應用程式伺服器加密這些密碼。

>[!NOTE]
>
>JEE JBoss®統包安裝程式上的AEM Forms會加密資料庫密碼。

IBM® WebSphere®應用程式伺服器和OracleWebLogic伺服器預設會加密資料源密碼。 不過，您應該向應用程式伺服器檔案確認，以確保檔案確實發生。

### 保護儲存在信任儲存中的私鑰 {#protecting-the-private-key-stored-in-trust-store}

匯入信任存放區的私密金鑰或憑證會儲存在JEE資料庫的AEM Forms中。 要保護資料庫並僅限指定管理員訪問，請採取適當的預防措施。
