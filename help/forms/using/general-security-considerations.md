---
title: JEE版AEM Forms的一般安全性考量事項
description: 瞭解如何準備在JEE環境中強化AEM Forms。
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
docset: aem65
role: Admin,User
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 1%

---

# JEE版AEM Forms的一般安全性考量事項{#general-security-considerations-for-aem-forms-on-jee}

本文提供的簡介資訊可協助您做好強化AEM Forms環境的準備。 其中包括JEE版AEM Forms、作業系統、應用程式伺服器和資料庫安全性的相關先決條件資訊。 在繼續鎖定您的環境之前，請先檢閱此資訊。

## 廠商特定的安全性資訊 {#vendor-specific-security-information}

本節包含整合至AEM Forms on JEE解決方案之作業系統、應用程式伺服器和資料庫的安全性相關資訊。

使用本節中的連結，為您的作業系統、資料庫和應用程式伺服器尋找供應商特定的安全性資訊。

### 作業系統安全性資訊 {#operating-system-security-information}

保護作業系統的安全時，請仔細考慮實施作業系統供應商所說明的措施，包括：

* 定義和控制使用者、角色和許可權
* 監控日誌和稽核軌跡
* 移除不必要的服務和應用程式
* 備份檔案

如需AEM Forms on JEE支援之作業系統的安全性資訊，請參閱下表中的資源：

<table>
 <thead>
  <tr>
   <th><p>作業系統</p> </th>
   <th><p>安全性資源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">IBM® AIX®安全性優點</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Windows Server 2016安全性指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP或ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Red Hat® Enterprise Linux®安全性指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris™ 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">安全性與強化准則</a></p> </td>
  </tr>
  <tr>
   <td>oracleLinux® 7更新3</td>
   <td>版本7</a><br />的<a href="https://docs.oracle.com/en/operating-systems/oracle-linux/7/security/" target="_blank">安全性指南 </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">保護檔案</a></td>
  </tr>
 </tbody>
</table>

### 應用程式伺服器安全性資訊 {#application-server-security-information}

保護應用程式伺服器的安全時，請仔細考慮實施伺服器供應商所說明的措施，包括：

* 使用不明顯的管理員使用者名稱
* 停用不必要的服務
* 保護主控台管理員
* 啟用安全Cookie
* 關閉不需要的連線埠
* 依IP位址或網域限制使用者端
* 使用Java™安全管理員以程式設計方式限制許可權

如需AEM Forms on JEE支援之應用程式伺服器的安全性資訊，請參閱此表格中的資源。

<table>
 <thead>
  <tr>
   <th><p>應用程式伺服器</p> </th>
   <th><p>安全性資源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>oracleWebLogic®</p> </td>
   <td><p>在<a href="https://docs.oracle.com/">https://docs.oracle.com/</a>搜尋瞭解WebLogic安全性。</p> </td>
  </tr>
  <tr>
   <td><p>IBM® WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">保護應用程式及其環境</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security%20subsystem%20configuration.html">安全性子系統設定</a></p> </td>
  </tr>
 </tbody>
</table>

### 資料庫安全性資訊 {#database-security-information}

保護資料庫安全時，請考慮實施資料庫供應商所說明的措施，包括：

* 使用存取控制清單(ACL)限製作業
* 使用非標準連線埠
* 將資料庫隱藏在防火牆後面
* 將敏感資料寫入資料庫之前先加以加密（請參閱資料庫製造商的檔案）

如需AEM Forms on JEE支援之資料庫的安全性資訊，請參閱此表格中的資源。

<table>
 <thead>
  <tr>
   <th><p>資料庫</p> </th>
   <th><p>安全性資源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">DB2®產品系列庫</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016</p> </td>
   <td>在Web上搜尋「SQL Server 2016：安全性」</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">MySQL 5.0一般安全性問題</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">MySQL 5.1一般安全性問題</a></p> </td>
  </tr>
  <tr>
   <td><p>oracle® 12c</p> </td>
   <td><p>請參閱<a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle12g檔案</a>中的「安全性」一章</p> </td>
  </tr>
 </tbody>
</table>

此表格說明在AEM Forms on JEE設定程式期間需要開啟的預設連線埠。 如果您是透過https連線，請相應地調整連線埠資訊和IP位址。 如需有關設定連線埠的詳細資訊，請參閱應用程式伺服器的&#x200B;*在JEE上安裝和部署AEM Forms*&#x200B;檔案。

<table>
 <thead>
  <tr>
   <th><p>產品或服務</p> </th>
   <th><p>連線埠號碼</p> </th>
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
   <td><p>由管理員在設定期間設定</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere®</p> </td>
   <td><p>9060，如果啟用全域安全性，預設SSL連線埠值為9043。</p> <p>9080</p> </td>
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
   <td>&gt;<p>oracle</p> </td>
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
   <td><p>執行LDAP伺服器的連線埠。 預設連線埠通常為389。 不過，如果您選取SSL選項，預設連線埠通常是636。 請向您的LDAP管理員確認要指定哪個連線埠。</p> </td>
  </tr>
 </tbody>
</table>

### 設定JBoss®使用非預設HTTP連線埠 {#configuring-jboss-to-use-a-non-default-http-port}

JBoss® Application Server使用8080作為預設HTTP連線埠。 JBoss®也有預先設定的連線埠8180、8280和8380，這些連線埠在jboss-service.xml檔案中被註解。 如果您的電腦上有已使用此連線埠的應用程式，請依照下列步驟變更AEM Forms on JEE使用的連線埠：

1. 開啟下列檔案進行編輯：

   單一伺服器安裝： [JBoss® root]/standalone/configuration/standalone.xml

   叢集安裝： [JBoss® root]/domain/configuration/domain.xml

1. 將&#x200B;**&lt;socket-binding>**&#x200B;標籤中&#x200B;**連線埠**&#x200B;屬性的值變更為自訂連線埠號碼。 例如，下列使用連線埠8090：

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. 儲存並關閉檔案。
1. 重新啟動JBoss®應用程式伺服器。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

## JEE安全性考量事項上的AEM Forms {#aem-forms-on-jee-security-considerations}

本節說明關於JEE專屬安全性問題的部分AEM Forms，您應瞭解這些問題。

### 資料庫中未加密電子郵件認證 {#email-credentials-not-encrypted-in-database}

應用程式儲存的電子郵件認證在儲存至JEE資料庫的AEM Forms之前不會加密。 將服務端點設定為使用電子郵件時，當該端點設定中所使用的任何密碼資訊儲存在資料庫中時，都不會加密。

### 資料庫中Rights Management的敏感內容 {#sensitive-content-for-rights-management-in-the-database}

JEE上的AEM Forms使用JEE上的AEM Forms資料庫來儲存敏感檔案金鑰資訊和用於原則檔案的其他密碼編譯材料。 保護資料庫不受入侵有助於保護這些敏感資訊。

### 以純文字格式輸入密碼 {#password-in-clear-text-format-in-adobe-ds-xml}

在JEE上執行AEM Forms所用的應用程式伺服器，必須自行設定，才能透過應用程式伺服器上設定的資料來源存取資料庫。 請確定您的應用程式伺服器沒有在其資料來源組態檔中以純文字公開您的資料庫密碼。

lc_[資料庫].xml檔案不應包含純文字格式的密碼。 請洽詢您的應用程式伺服器廠商，瞭解如何為應用程式伺服器加密這些密碼。

>[!NOTE]
>
>JEE JBoss®上的AEM Forms全金安裝程式會加密資料庫密碼。

IBM® WebSphere® Application Server和OracleWebLogic Server預設可能會加密資料來源密碼。 不過，您應透過應用程式伺服器檔案確認，以確保確實發生這種情況。

### 保護儲存在信任存放區中的私密金鑰 {#protecting-the-private-key-stored-in-trust-store}

在信任存放區中匯入的私密金鑰或認證儲存在JEE資料庫的AEM Forms中。 若要保護資料庫安全並限制僅供指定的管理員存取，請採取適當的預防措施。
