---
title: AEM Forms關於JEE的一般安全考慮
seo-title: General Security Considerations for AEM Forms on JEE
description: 瞭解如何準備在JEE環境中強化您的AEM Forms。
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

# AEM Forms關於JEE的一般安全考慮{#general-security-considerations-for-aem-forms-on-jee}

本文提供介紹性資訊，幫助您為強化AEM Forms環境做好準備。 它包括有關JEE、作業系統、應用伺服器和資料庫安全的AEM Forms的先決條件資訊。 在繼續鎖定環境之前，請查看此資訊。

## 特定於供應商的安全資訊 {#vendor-specific-security-information}

本部分包含有關作業系統、應用程式伺服器和資料庫的安全相關資訊，這些資訊已併入您的AEM FormsJEE解決方案中。

使用本節中的連結可查找作業系統、資料庫和應用程式伺服器的特定於供應商的安全資訊。

### 作業系統安全資訊 {#operating-system-security-information}

在保護作業系統時，請仔細考慮實施作業系統供應商描述的措施，包括：

* 定義和控制用戶、角色和權限
* 監視日誌和審計跟蹤
* 刪除不必要的服務和應用程式
* 備份檔案

有關AEM FormsJEE上支援的作業系統的安全資訊，請參閱表中的資源：

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
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Red Hat® Enterprise Linux®安全指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris™ 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">安全和強化准則</a></p> </td>
  </tr>
  <tr>
   <td>OracleLinux® 7更新3</td>
   <td><a href="https://docs.oracle.com/en/operating-systems/oracle-linux/7/security/" target="_blank">7版安全指南</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">保護文檔</a></td>
  </tr>
 </tbody>
</table>

### 應用程式伺服器安全資訊 {#application-server-security-information}

在保護應用程式伺服器時，請仔細考慮實施伺服器供應商描述的措施，包括：

* 使用非顯而易見的管理員用戶名
* 禁用不必要的服務
* 保護控制台管理器
* 啟用安全Cookie
* 關閉不需要的埠
* 按IP地址或域限制客戶端
* 使用Java™ Security Manager以寫程式方式限制權限

有關JEE上的AEM Forms支援的應用程式伺服器的安全資訊，請參見下表中的資源。

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
   <td><p>搜索以瞭解WebLogic安全 <a href="https://docs.oracle.com/">https://docs.oracle.com/</a>。</p> </td>
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

* 使用訪問控制清單(ACL)限制操作
* 使用非標準埠
* 將資料庫隱藏在防火牆之後
* 在將敏感資料寫入資料庫之前對其進行加密（請參閱資料庫製造商的文檔）

有關AEM Forms在JEE上支援的資料庫的安全資訊，請參見此表中的資源。

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
   <td>在Web上搜索「SQL Server 2016:安全性"</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">MySQL 5.0一般安全問題</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">MySQL 5.1一般安全問題</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>請參閱 <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle12g文檔</a></p> </td>
  </tr>
 </tbody>
</table>

此表介紹了在AEM FormsJEE配置過程中需要開啟的預設埠。 如果您通過https連接，請相應地調整埠資訊和IP地址。 有關配置埠的詳細資訊，請參見 *在JEE上安裝和部署AEM Forms* 文檔。

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
   <td>&gt;<p>WebLogic托管伺服器</p> </td>
   <td><p>配置期間由管理員設定</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere®</p> </td>
   <td><p>9060，如果啟用了「Global Security（全局安全）」，則預設的SSL埠值為9043。</p> <p>9080</p> </td>
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
   <td><p>運行LDAP伺服器的埠。 預設埠通常為389。 但是，如果選擇SSL選項，則預設埠通常為636。 向LDAP管理員確認要指定的埠。</p> </td>
  </tr>
 </tbody>
</table>

### 配置JBoss®使用非預設HTTP埠 {#configuring-jboss-to-use-a-non-default-http-port}

JBoss® Application Server使用8080作為預設HTTP埠。 JBoss®還具有預配置的埠8180、8280和8380，這些埠在jboss-service.xml檔案中注釋掉。 如果您的電腦上有已使用此埠的應用程式，請通過以下步驟更改JEE上的AEM Forms使用的埠：

1. 開啟以下檔案進行編輯：

   單伺服器安裝： [JBoss®根]/standalone/configuration/standalone.xml

   群集安裝： [JBoss®根]/domain/configuration/domain.xml

1. 更改 **埠** 屬性 **&lt;socket-binding>** 標籤為自定義埠號。 例如，以下程式使用埠8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. 保存並關閉檔案。
1. 重新啟動JBoss®應用程式伺服器。

## AEM Forms關於JEE安全考慮 {#aem-forms-on-jee-security-considerations}

本節介紹一些您應該瞭解的AEM Forms關於JEE特定安全問題的資訊。

### 未在資料庫中加密電子郵件憑據 {#email-credentials-not-encrypted-in-database}

應用程式儲存的電子郵件憑據在儲存到AEM Forms的JEE資料庫中之前不會進行加密。 將服務終結點配置為使用電子郵件時，當該終結點配置儲存在資料庫中時，用作該終結點配置一部分的任何密碼資訊都不會加密。

### 資料庫中Rights Management的敏感內容 {#sensitive-content-for-rights-management-in-the-database}

AEM FormsJEE資料庫使用AEM FormsJEE資料庫來儲存敏感文檔密鑰資訊和用於策略文檔的其他加密材料。 保護資料庫免受入侵，有助於保護此敏感資訊。

### 明文形式的密碼 {#password-in-clear-text-format-in-adobe-ds-xml}

用於在JEE上運行AEM Forms的應用程式伺服器需要其自己的配置，以便通過在應用程式伺服器上配置的資料源訪問資料庫。 確保應用程式伺服器不會在其資料源配置檔案中以明文形式公開資料庫密碼。

lc_[資料庫].xml檔案不應包含明文格式的密碼。 請咨詢您的應用程式伺服器供應商，瞭解如何為您的應用程式伺服器加密這些密碼。

>[!NOTE]
>
>JEE JBoss®交鑰匙安裝程式上的AEM Forms加密資料庫密碼。

IBM® WebSphere®應用程式伺服器和OracleWebLogic伺服器在預設情況下可能會加密資料源密碼。 但是，您應該與應用程式伺服器文檔進行確認，以確保發生這種情況。

### 保護儲存在信任儲存中的私鑰 {#protecting-the-private-key-stored-in-trust-store}

在信任儲存中導入的私鑰或憑據儲存在JEE資料庫的AEM Forms中。 要保護資料庫並僅限制對指定管理員的訪問，請採取適當的預防措施。
