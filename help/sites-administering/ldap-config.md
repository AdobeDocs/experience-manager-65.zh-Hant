---
title: 使用AEM 6配置LDAP
seo-title: Configuring LDAP with AEM 6
description: 了解如何使用AEM設定LDAP。
seo-description: Learn how to configure LDAP with AEM.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 0%

---

# 使用AEM 6配置LDAP {#configuring-ldap-with-aem}

LDAP( **L**&#x200B;八八 **D**&#x200B;記錄 **A**&#x200B;存取 **P** rotocol)用於訪問集中目錄服務。 這有助於減少管理多個應用程式可存取的使用者帳戶所需的工作量。 Active Directory是此類LDAP伺服器。 LDAP通常用於實現單一登錄，該登錄允許用戶在登錄後訪問多個應用程式。

可在LDAP伺服器和儲存庫之間同步用戶帳戶，並將LDAP帳戶詳細資訊保存在儲存庫中。 這可讓帳戶指派給存放庫群組，以分配所需的權限。

儲存庫使用LDAP驗證來驗證此類用戶，並將憑據傳遞到LDAP伺服器進行驗證，這是允許訪問儲存庫之前所需的。 為了改善效能，存放庫可快取成功驗證的憑證，並設定到期逾時，以確保在適當的期間後會進行重新驗證。

從LDAP伺服器中刪除帳戶時，不再授予驗證權，因此對儲存庫的訪問被拒絕。 也可清除儲存庫中儲存的LDAP帳戶的詳細資訊。

這些帳戶的使用對您的用戶是透明的，他們發現從LDAP建立的用戶和組帳戶與僅在儲存庫中建立的用戶和組帳戶之間沒有區別。

在AEM 6中，LDAP支援隨附新實作，其需要的組態類型與舊版不同。

所有LDAP設定現在都可作為OSGi設定使用。 可透過Web管理控制台進行設定：
`https://serveraddress:4502/system/console/configMgr`

若要讓LDAP與AEM搭配使用，您需要建立三個OSGi設定：

1. LDAP身分提供者(IDP)。
1. 同步處理程式。
1. 外部登入模組。

>[!NOTE]
>
>Watch [Oak的外部登入模組 — 使用LDAP及更新進行驗證](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#) 深入探索外部登入模組。
>
>若要閱讀使用Apache DS配置Experience Manager的範例，請參閱 [將Adobe Experience Manager 6.5設定為使用Apache Directory Service。](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## 配置LDAP標識提供程式 {#configuring-the-ldap-identity-provider}

LDAP標識提供程式用於定義如何從LDAP伺服器檢索用戶。

您可在管理主控台的 **Apache Jackrabbit Oak LDAP身分提供程式** 名稱。

LDAP標識提供程式可使用以下配置選項：

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
   <td>指出是否應在連線上啟動TLS。</td>
  </tr>
  <tr>
   <td><strong>禁用證書檢查</strong></td>
   <td>指示是否應禁用伺服器證書驗證。</td>
  </tr>
  <tr>
   <td><strong>綁定DN</strong></td>
   <td>用於驗證的用戶的DN。 如果保留為空，則將執行匿名綁定。</td>
  </tr>
  <tr>
   <td><strong>綁定密碼</strong></td>
   <td>用於驗證的用戶密碼</td>
  </tr>
  <tr>
   <td><strong>搜尋逾時</strong></td>
   <td>搜索超時的時間</td>
  </tr>
  <tr>
   <td><strong>管理池最大活動</strong></td>
   <td>管理連接池的最大活動大小。</td>
  </tr>
  <tr>
   <td><strong>用戶池最大活動</strong></td>
   <td>用戶連接池的最大活動大小。</td>
  </tr>
  <tr>
   <td><strong>用戶庫DN</strong></td>
   <td>用戶搜索的DN</td>
  </tr>
  <tr>
   <td><strong>用戶對象類</strong></td>
   <td>用戶條目必須包含的對象類清單。</td>
  </tr>
  <tr>
   <td><strong>使用者ID屬性</strong></td>
   <td>包含用戶ID的屬性名稱。</td>
  </tr>
  <tr>
   <td><strong>使用者額外篩選</strong></td>
   <td>搜尋使用者時要使用的額外LDAP篩選器。 最終篩選器的格式如下：'(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'(user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>用戶DN路徑</strong></td>
   <td>控制是否應使用DN來計算中間路徑的一部分。</td>
  </tr>
  <tr>
   <td><strong>組基DN</strong></td>
   <td>組搜索的基本DN。</td>
  </tr>
  <tr>
   <td><strong>組對象類</strong></td>
   <td>組條目必須包含的對象類清單。</td>
  </tr>
  <tr>
   <td><strong>組名屬性</strong></td>
   <td>包含組名的屬性的名稱。</td>
  </tr>
  <tr>
   <td><strong>分組額外篩選</strong></td>
   <td>搜尋群組時要使用的額外LDAP篩選器。 最終篩選器的格式如下：'(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
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

同步處理程式將定義如何與儲存庫同步身份提供程式用戶和組。

位於 **Apache Jackrabbit Oak Default同步處理常式** 名稱。

以下配置選項適用於同步處理程式：

<table>
 <tbody>
  <tr>
   <td><strong>同步處理程式名稱</strong></td>
   <td>同步配置的名稱。</td>
  </tr>
  <tr>
   <td><strong>使用者過期時間</strong></td>
   <td>持續時間，直到同步的使用者過期。</td>
  </tr>
  <tr>
   <td><strong>用戶自動成員資格</strong></td>
   <td>已自動新增同步使用者的群組清單。</td>
  </tr>
  <tr>
   <td><strong>用戶屬性映射</strong></td>
   <td>外部屬性的本地屬性的清單映射定義。</td>
  </tr>
  <tr>
   <td><strong>用戶路徑前置詞</strong></td>
   <td>建立新使用者時使用的路徑首碼。</td>
  </tr>
  <tr>
   <td><strong>使用者成員資格有效期</strong></td>
   <td>會籍過期的時間。<br /> </td>
  </tr>
  <tr>
   <td><strong>用戶成員資格嵌套深度</strong></td>
   <td>傳回同步成員關係時的群組巢狀深度上限。 值0有效地禁用組成員資格查找。 值1隻會新增使用者的直接群組。 此值僅在同步使用者成員資格祖先時才會在同步個別群組時失效。</td>
  </tr>
  <tr>
   <td><strong>組到期時間</strong></td>
   <td>持續時間，直到同步的群組過期。</td>
  </tr>
  <tr>
   <td><strong>群組自動成員資格</strong></td>
   <td>同步組自動添加到的組清單。</td>
  </tr>
  <tr>
   <td><strong>組屬性映射</strong></td>
   <td>外部屬性的本地屬性的清單映射定義。</td>
  </tr>
  <tr>
   <td><strong>組路徑前置詞</strong></td>
   <td>建立新群組時使用的路徑首碼。</td>
  </tr>
 </tbody>
</table>

## 外部登入模組 {#the-external-login-module}

外部登入模組位於 **Apache Jackrabbit Oak External登入模組** 下。

>[!NOTE]
>
>Apache Jackrabbit Oak外部登入模組會實作Java驗證和授權服務(JAAS)規格。 請參閱 [官方OracleJava安全參考指南](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) 以取得更多資訊。

其工作是定義要使用的身份提供程式和同步處理程式，有效綁定這兩個模組。

可使用下列設定選項：

| **JAAS排名** | 指定此登錄模組條目的排名（即排序順序）。 項目會以遞減順序排序（亦即值排名設定會排在第一）。 |
|---|---|
| **JAAS控制標幟** | 指定LoginModule是否為必需、必要、充分或可選的屬性。有關這些標誌含義的詳細資訊，請參閱JAAS配置文檔。 |
| **JAAS王國** | 註冊LoginModule時所依據的領域名稱（或應用程式名稱）。 如果未提供領域名稱，則LoginModule將註冊為Felix JAAS配置中配置的預設領域。 |
| **身份提供程式名稱** | 身份提供程式的名稱。 |
| **同步處理程式名稱** | 同步處理程式的名稱。 |

>[!NOTE]
>
>如果您打算使用AEM執行個體建立多個LDAP設定，則需要為每個設定建立個別的身分提供者和同步處理常式。

## 通過SSL配置LDAP {#configure-ldap-over-ssl}

AEM 6可透過SSL設定以透過LDAP驗證，方法如下：

1. 檢查 **使用SSL** 或 **使用TLS** 配置時的複選框 [LDAP標識提供程式](#configuring-the-ldap-identity-provider).
1. 根據您的設定配置同步處理程式和外部登錄模組。
1. 視需要在您的Java VM中安裝SSL憑證。 這可透過使用鍵具來完成：

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. 測試與LDAP伺服器的連接。

### 建立SSL憑證 {#creating-ssl-certificates}

在設定AEM以透過SSL透過LDAP驗證時，可使用自行簽署的憑證。 以下是產生要與AEM搭配使用之憑證的工作程式範例。

1. 請確定您已安裝SSL程式庫且運作正常。 此程式將以OpenSSL為例。

1. 建立自訂的OpenSSL設定(cnf)檔案。 複製預設的**openssl.cnf **設定檔案並自訂，即可完成此操作。 在UNIX系統上，它通常位於 `/usr/lib/ssl/openssl.cnf`

1. 在終端中運行以下命令，繼續建立CA根密鑰：

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 接下來，建立新的自簽名證書：

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Inspect新產生的憑證，以確保一切都順序：

   `openssl x509 -noout -text -in root-ca.crt`

1. 請確定憑證設定(.cnf)檔案中指定的所有資料夾都存在。 否則，請建立。
1. 例如，執行以建立隨機種子：

   `openssl rand -out private/.rand 8192`

1. 將建立的.pem檔案移至.cnf檔案中設定的位置。

1. 最後，將憑證新增至Java金鑰存放區。

## 啟用偵錯記錄 {#enabling-debug-logging}

可以為LDAP身分提供程式和外部登錄模組啟用調試日誌記錄，以便對連接問題進行故障排除。

若要啟用偵錯記錄，您必須：

1. 前往Web管理控制台。
1. 尋找「Apache Sling Logging Logger Configuration」並使用下列選項建立兩個記錄器：

* 記錄層級：除錯
* 記錄檔logs/ldap.log
* 消息模式：{0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* 記錄器：org.apache.jackrabbit.oak.security.authentication.ldap

* 記錄層級：除錯
* 日誌檔案：logs/external.log
* 消息模式：{0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* 記錄器：org.apache.jackrabbit.oak.spi.security.authentication.external

## 關於團體隸屬關係的一個詞 {#a-word-on-group-affiliation}

透過LDAP同步的使用者可以是AEM中不同群組的一部分。 這些組可以是將作為同步過程的一部分添加到AEM的外部LDAP組，但也可以是單獨添加的組，而不是原始LDAP組關聯方案的一部分。

在大多數情況下，這些群組可以是由本機AEM管理員或任何其他身分提供者新增的群組。

如果從LDAP伺服器上的組中刪除了用戶，則同步時，該更改也將反映在AEM端。 但是，未由LDAP添加的用戶的所有其他組從屬關係將保持不變。

AEM會利用 `rep:externalId` 屬性。 此屬性將自動添加到由同步處理程式同步的任何用戶或組中，並包含有關原始身份提供程式的資訊。

如需詳細資訊，請參閱Apache Oak檔案，位於 [用戶和組同步](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## 已知問題 {#known-issues}

如果您打算使用LDAP over SSL，請確保您使用的證書建立時沒有Netscape注釋選項。 如果啟用此選項，驗證將會因SSL握手錯誤而失敗。
