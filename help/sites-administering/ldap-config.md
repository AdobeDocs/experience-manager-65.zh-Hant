---
title: 使用AEM 6設定LDAP
seo-title: 使用AEM 6設定LDAP
description: 瞭解如何使用AEM設定LDAP。
seo-description: 瞭解如何使用AEM設定LDAP。
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# 使用AEM 6設定LDAP {#configuring-ldap-with-aem}

LDAP(輕量型目 ****&#x200B;錄訪 ****&#x200B;問協 ****&#x200B;議)用 ****&#x200B;於訪問集中式目錄服務。 這有助於減少管理使用者帳戶所需的工作，因為使用者帳戶可供多個應用程式存取。 Active Directory是此類LDAP伺服器之一。 LDAP通常用於實現單一登入，允許用戶在登錄一次後訪問多個應用程式。

用戶帳戶可以在LDAP伺服器和儲存庫之間同步，LDAP帳戶詳細資訊將保存在儲存庫中。 這允許將帳戶分配給儲存庫組以分配所需的權限和權限。

儲存庫使用LDAP驗證來驗證這些用戶，並將憑據傳遞到LDAP伺服器進行驗證，這是允許訪問儲存庫之前所必需的。 為了提高效能，儲存庫可以快取成功驗證的憑據，並使用到期超時以確保在適當的時間段後進行重新驗證。

當帳戶從LDAP伺服器驗證中刪除時，將不再授予驗證權，因此對儲存庫的訪問被拒絕。 也可以清除儲存庫中保存的LDAP帳戶的詳細資訊。

這些帳戶的使用對用戶是透明的，它們在從LDAP建立的用戶和組帳戶和僅在儲存庫中建立的用戶和組帳戶之間沒有差別。

在AEM 6中，LDAP支援隨附新實作，其需要的組態類型與舊版不同。

所有LDAP配置現在都可作為OSGi配置使用。 您可以透過Web管理主控台(網址為：
`https://serveraddress:4502/system/console/configMgr`

為了讓LDAP與AEM搭配運作，您需要建立三個OSGi組態：

1. LDAP身分提供者(IDP)。
1. 同步處理常式。
1. 外部登錄模組。

>[!NOTE]
>
>觀看 [Oak的外部登入模組——使用LDAP和Expeind](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#) ，深入探討外部登入模組。
>
>若要閱讀使用Apache DS設定Experience Manager的範例，請參 [閱設定Adobe Experience Manager 6.5以使用Apache Directory Service。](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## 配置LDAP身份提供程式 {#configuring-the-ldap-identity-provider}

LDAP身份提供程式用於定義如何從LDAP伺服器檢索用戶。

它位於管理主控台的 **Apache Jackrabbit Oak LDAP身分提供者名稱下** 。

LDAP身份提供程式可使用以下配置選項：

<table>
 <tbody>
  <tr>
   <td><strong>LDAP提供程式名稱</strong></td>
   <td>此LDAP提供程式配置的名稱。</td>
  </tr>
  <tr>
   <td><strong>LDAP伺服器主機名</strong><br /> </td>
   <td>LDAP伺服器的主機名</td>
  </tr>
  <tr>
   <td><strong>LDAP伺服器埠</strong></td>
   <td>LDAP伺服器的埠</td>
  </tr>
  <tr>
   <td><strong>使用SSL</strong></td>
   <td>指示是否應使用SSL(LDAP)連接。</td>
  </tr>
  <tr>
   <td><strong>使用TLS</strong></td>
   <td>指示是否應在連接上啟動TLS。</td>
  </tr>
  <tr>
   <td><strong>禁用證書檢查</strong></td>
   <td>指示是否應禁用伺服器證書驗證。</td>
  </tr>
  <tr>
   <td><strong>綁定DN</strong></td>
   <td>用於驗證的用戶的DN。 如果保留為空，則會執行匿名綁定。</td>
  </tr>
  <tr>
   <td><strong>綁定密碼</strong></td>
   <td>驗證用戶的密碼</td>
  </tr>
  <tr>
   <td><strong>搜尋逾時</strong></td>
   <td>直到搜索超時</td>
  </tr>
  <tr>
   <td><strong>管理池最大活動時間</strong></td>
   <td>管理連接池的最大活動大小。</td>
  </tr>
  <tr>
   <td><strong>使用者池最大活動值</strong></td>
   <td>用戶連接池的最大活動大小。</td>
  </tr>
  <tr>
   <td><strong>用戶基本DN</strong></td>
   <td>用戶搜索的DN</td>
  </tr>
  <tr>
   <td><strong>用戶對象類</strong></td>
   <td>用戶條目必須包含的對象類清單。</td>
  </tr>
  <tr>
   <td><strong>用戶ID屬性</strong></td>
   <td>包含用戶ID的屬性的名稱。</td>
  </tr>
  <tr>
   <td><strong>使用者額外篩選</strong></td>
   <td>搜尋使用者時要使用的額外LDAP篩選器。 最終篩選器的格式如下：'(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'(user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>用戶DN路徑</strong></td>
   <td>控制是否應使用DN來計算中間路徑的一部分。</td>
  </tr>
  <tr>
   <td><strong>組基本DN</strong></td>
   <td>群組搜尋的基本DN。</td>
  </tr>
  <tr>
   <td><strong>組對象類</strong></td>
   <td>組條目必須包含的對象類清單。</td>
  </tr>
  <tr>
   <td><strong>群組名稱屬性</strong></td>
   <td>包含組名的屬性的名稱。</td>
  </tr>
  <tr>
   <td><strong>群組額外篩選</strong></td>
   <td>搜索組時要使用的額外LDAP篩選器。 最終篩選器的格式如下：'(&amp;(&lt;nameAttr&gt;=&lt;groupName&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>組DN路徑</strong></td>
   <td>控制是否應使用DN來計算中間路徑的一部分。</td>
  </tr>
  <tr>
   <td><strong>組成員屬性</strong></td>
   <td>包含組成員的組屬性。</td>
  </tr>
 </tbody>
</table>

## 配置同步處理程式 {#configuring-the-synchronization-handler}

同步處理程式將定義Indentity Provider用戶和組與儲存庫的同步方式。

它位於管理主控 **台的Apache Jackrabbit Oak Default Sync Handler** name下方。

以下配置選項可用於同步處理程式：

<table>
 <tbody>
  <tr>
   <td><strong>同步處理常式名稱</strong></td>
   <td>同步配置的名稱。</td>
  </tr>
  <tr>
   <td><strong>使用者過期時間</strong></td>
   <td>持續時間，直到同步的使用者過期。</td>
  </tr>
  <tr>
   <td><strong>使用者自動會籍</strong></td>
   <td>同步使用者自動新增至的群組清單。</td>
  </tr>
  <tr>
   <td><strong>用戶屬性映射</strong></td>
   <td>清單映射外部屬性的本地屬性定義。</td>
  </tr>
  <tr>
   <td><strong>用戶路徑前置詞</strong></td>
   <td>建立新使用者時使用的路徑首碼。</td>
  </tr>
  <tr>
   <td><strong>使用者會籍有效期</strong></td>
   <td>會籍的過期時間。<br /> </td>
  </tr>
  <tr>
   <td><strong>使用者會籍巢狀深度</strong></td>
   <td>傳回在成員關係同步時群組巢狀的最大深度。 值0可有效停用群組成員資格查閱。 值1隻會新增使用者的直接群組。 此值僅在同步使用者會籍祖先時，才會在同步個別群組時產生任何效果。</td>
  </tr>
  <tr>
   <td><strong>群組到期時間</strong></td>
   <td>持續時間，直到同步的群組過期。</td>
  </tr>
  <tr>
   <td><strong>群組自動會籍</strong></td>
   <td>同步群組自動新增至的群組清單。</td>
  </tr>
  <tr>
   <td><strong>群組屬性對應</strong></td>
   <td>清單映射外部屬性的本地屬性定義。</td>
  </tr>
  <tr>
   <td><strong>群組路徑首碼</strong></td>
   <td>建立新群組時使用的路徑首碼。</td>
  </tr>
 </tbody>
</table>

## 外部登錄模組 {#the-external-login-module}

外部登入模組位於 **Apache Jackrabbit Oak External Login Module** ，位於管理控制台下。

>[!NOTE]
>
>Apache Jackrabbit Oak外部登入模組實作Java驗證與授權服務(JAAS)規格。 有關詳 [細資訊，請參閱官方的Oracle Java Security Reference Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) 。

其工作是定義要使用的身份提供者和同步處理程式，有效地綁定兩個模組。

可使用下列配置選項：

| **JAAS排名** | 指定此登錄模組條目的排名（即排序順序）。 條目按降序排序（即，值較高的排名配置優先）。 |
|---|---|
| **JAAS控制標幟** | 指定LoginModule是否為必需、必要、充分或可選的屬性。有關這些標誌含義的詳細資訊，請參閱JAAS配置文檔。 |
| **JAAS Realm** | 註冊LoginModule時所依據的領域名稱（或應用程式名稱）。 如果未提供領域名稱，則LoginModule會註冊到Felix JAAS配置中配置的預設領域。 |
| **身分提供者名稱** | 身分提供者的名稱。 |
| **同步處理常式名稱** | 同步處理常式的名稱。 |

>[!NOTE]
>
>如果您打算使用AEM例項建立多個LDAP設定，則需要為每個設定建立個別的身分提供者和同步處理常式。

## 通過SSL配置LDAP {#configure-ldap-over-ssl}

AEM 6可依下列程式設定，以透過SSL使用LDAP進行驗證：

1. 在配置 **LDAP身分提供** 器時，選中「使用SSL **」或「使用TLS** 」複選框 [](#configuring-the-ldap-identity-provider)。
1. 根據您的設定配置同步處理程式和外部登錄模組。
1. 視需要在Java VM中安裝SSL憑證。 您可使用keytool:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. 測試與LDAP伺服器的連接。

### 建立SSL憑證 {#creating-ssl-certificates}

當設定AEM以透過SSL向LDAP驗證時，可使用自簽名憑證。 以下是產生要與AEM搭配使用之憑證的工作程式範例。

1. 請確定您已安裝並運作SSL程式庫。 此程式將以OpenSSL為例。

1. 建立自訂的OpenSSL設定(cnf)檔案。 您可複製預設的**openssl.cnf **組態檔並加以自訂，即可完成此作業。 在UNIX系統上，它通常位於 `/usr/lib/ssl/openssl.cnf`

1. 通過在終端機中運行以下命令，繼續建立CA根密鑰：

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 接著，建立新的自簽名憑證：

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. 檢查新產生的憑證，確保一切順序：

   `openssl x509 -noout -text -in root-ca.crt`

1. 確保證書配置(.cnf)檔案中指定的所有資料夾都存在。 否則，請建立它們。
1. 例如，執行以建立隨機種子：

   `openssl rand -out private/.rand 8192`

1. 將建立的。pem檔案移動到。cnf檔案中配置的位置。

1. 最後，將憑證新增至Java金鑰庫。

## 啟用除錯記錄 {#enabling-debug-logging}

可以為LDAP身份提供程式和外部登錄模組啟用調試日誌記錄，以排除連接問題。

若要啟用除錯記錄，您必須：

1. 前往Web管理主控台。
1. 尋找&quot;Apache Sling Logging Logger Configuration&quot;並建立兩個記錄程式及下列選項：

* 記錄層級：除錯
* 記錄檔logs/ldap.log
* 消息模式：{0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* 記錄器：org.apache.jackrabbit.oak.security.ldap

* 記錄層級：除錯
* 日誌檔案：logs/external.log
* 消息模式：{0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* 記錄器：org.apache.jackrabbit.oak.spi.security.authentication.external

## 團體關係論 {#a-word-on-group-affiliation}

透過LDAP同步化的使用者可以是AEM中不同群組的一部分。 這些群組可以是外部LDAP群組，這些LDAP群組將作為同步程式的一部分新增至AEM，但也可以是個別新增且不屬於原始LDAP群組附屬機制的群組。

在大多數情況下，這些群組可以是由本機AEM管理員或任何其他身分提供者新增的群組。

如果從LDAP伺服器上的群組移除使用者，同步時變更也會反映在AEM端。 但是，LDAP未添加的用戶的所有其他組從屬關係都將保留。

AEM會偵測並處理使用者從外部群組中清除的情 `rep:externalId` 況。 此屬性會自動添加到由同步處理程式同步的任何用戶或組，並包含有關原始身份提供程式的資訊。

如需詳細資訊，請參閱「使用者與群組同步」 [上的Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html)。

## 已知問題 {#known-issues}

如果您打算使用SSL上的LDAP，請確定您使用的憑證是在沒有Netscape註解選項的情況下建立的。 如果啟用此選項，驗證將失敗，並出現SSL握手錯誤。

