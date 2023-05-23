---
title: 配置LDAPAEM 6
description: 瞭解如何使用配置LDAPAEM。
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---

# 配置LDAPAEM 6 {#configuring-ldap-with-aem}

LDAP( **L**&#x200B;八八 **D**&#x200B;記錄 **A**&#x200B;訪問 **P**&#x200B;協定)用於訪問集中式目錄服務。 它有助於減少管理用戶帳戶所需的工作量，因為用戶帳戶可以被多個應用程式訪問。 此類LDAP伺服器之一是Active Directory。 LDAP通常用於實現單一登錄，允許用戶在一次登錄後訪問多個應用程式。

用戶帳戶可以在LDAP伺服器和儲存庫之間同步，LDAP帳戶詳細資訊將保存在儲存庫中。 此功能允許將帳戶分配給儲存庫組以分配所需的權限和權限。

儲存庫使用LDAP身份驗證來驗證這些用戶，憑據將傳遞到LDAP伺服器進行驗證，這是允許訪問儲存庫之前所必需的。 為了提高效能，儲存庫可以快取成功驗證的憑據，並設定到期超時，以確保在適當的時間段後重新驗證。

從LDAP伺服器中刪除帳戶後，將不再授予驗證權，並拒絕訪問儲存庫。 也可以清除儲存庫中保存的LDAP帳戶的詳細資訊。

此類帳戶的使用對用戶是透明的。 也就是說，他們看不到從LDAP建立的用戶和組帳戶與僅在儲存庫中建立的帳戶之間的差異。

在AEM6中，LDAP支援附帶了一種新的實現，它要求與以前版本不同的配置類型。

所有LDAP配置現在都可作為OSGi配置使用。 可通過Web管理控制台在以下位置進行配置：
`https://serveraddress:4502/system/console/configMgr`

要使LDAP與之配合使用AEM，必須建立三個OSGi配置：

1. LDAP標識提供程式(IDP)。
1. 同步處理程式。
1. 外部登錄模組。

>[!NOTE]
>
>監視 [Oak的外部登錄模組 — 使用LDAP和更高版本進行身份驗證](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html?lang=en) 深入查看外部登錄模組。
>
>要閱讀使用Apache DS配置Experience Manager的示例，請參見 [正在配置Adobe Experience Manager6.5以使用Apache目錄服務。](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/configuring-adobe-experience-manager-6-to-use-apache-directory/m-p/183805)

## 配置LDAP標識提供程式 {#configuring-the-ldap-identity-provider}

LDAP標識提供程式用於定義如何從LDAP伺服器檢索用戶。

在管理控制台中， **Apache Jackrabbit Oak LDAP標識提供程式** 名稱。

以下配置選項可用於LDAP標識提供程式：

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
   <td>用於驗證的用戶的DN。 如果此欄位為空，則執行匿名綁定。</td>
  </tr>
  <tr>
   <td><strong>綁定密碼</strong></td>
   <td>用於驗證的用戶密碼</td>
  </tr>
  <tr>
   <td><strong>搜索超時</strong></td>
   <td>直到搜索超時</td>
  </tr>
  <tr>
   <td><strong>管理池最大活動</strong></td>
   <td>管理員連接池的最大活動大小。</td>
  </tr>
  <tr>
   <td><strong>最大活動用戶池</strong></td>
   <td>用戶連接池的最大活動大小。</td>
  </tr>
  <tr>
   <td><strong>用戶基DN</strong></td>
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
   <td><strong>用戶額外篩選器</strong></td>
   <td>搜索用戶時要使用的額外LDAP篩選器。 最終篩選器的格式如下：'(&amp;)&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'(user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>用戶DN路徑</strong></td>
   <td>控制是否應將DN用於計算中間路徑的一部分。</td>
  </tr>
  <tr>
   <td><strong>組基本DN</strong></td>
   <td>組搜索的基本DN。</td>
  </tr>
  <tr>
   <td><strong>組對象類</strong></td>
   <td>組條目必須包含的對象類清單。</td>
  </tr>
  <tr>
   <td><strong>組名稱屬性</strong></td>
   <td>包含組名稱的屬性的名稱。</td>
  </tr>
  <tr>
   <td><strong>組額外篩選器</strong></td>
   <td>搜索組時要使用的額外LDAP篩選器。 最終篩選器的格式如下：'(&amp;)&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>組DN路徑</strong></td>
   <td>控制是否應將DN用於計算中間路徑的一部分。</td>
  </tr>
  <tr>
   <td><strong>組成員屬性</strong></td>
   <td>包含組的一個或多個成員的組屬性。</td>
  </tr>
 </tbody>
</table>

## 配置同步處理程式 {#configuring-the-synchronization-handler}

同步處理程式定義身份提供程式用戶和組如何與儲存庫同步。

位於 **Apache Jackrabbit Oak預設同步處理程式** 名稱。

以下配置選項可用於同步處理程式：

<table>
 <tbody>
  <tr>
   <td><strong>同步處理程式名稱</strong></td>
   <td>同步配置的名稱。</td>
  </tr>
  <tr>
   <td><strong>用戶到期時間</strong></td>
   <td>持續時間，直到同步用戶過期。</td>
  </tr>
  <tr>
   <td><strong>用戶自動成員身份</strong></td>
   <td>已同步用戶自動添加到的組清單。</td>
  </tr>
  <tr>
   <td><strong>用戶屬性映射</strong></td>
   <td>外部屬性的清單映射定義。</td>
  </tr>
  <tr>
   <td><strong>用戶路徑前置詞</strong></td>
   <td>建立用戶時使用的路徑前置詞。</td>
  </tr>
  <tr>
   <td><strong>用戶成員資格過期</strong></td>
   <td>成員資格過期的時間。<br /> </td>
  </tr>
  <tr>
   <td><strong>用戶成員身份嵌套深度</strong></td>
   <td>返回成員關係同步時組嵌套的最大深度。 值0有效禁用組成員身份查找。 值1隻添加用戶的直接組。 僅當同步用戶成員身份祖先時，此值才在同步單個組時無效。</td>
  </tr>
  <tr>
   <td><strong>組到期時間</strong></td>
   <td>同步組到期前的持續時間。</td>
  </tr>
  <tr>
   <td><strong>組自動成員身份</strong></td>
   <td>同步組自動添加到的組清單。</td>
  </tr>
  <tr>
   <td><strong>組屬性映射</strong></td>
   <td>外部屬性的清單映射定義。</td>
  </tr>
  <tr>
   <td><strong>組路徑前置詞</strong></td>
   <td>建立組時使用的路徑前置詞。</td>
  </tr>
 </tbody>
</table>

## 外部登錄模組 {#the-external-login-module}

外部登錄模組位於 **Apache Jackrabbit Oak外部登錄模組** 的下界。

>[!NOTE]
>
>Apache Jackrabbit Oak外部登錄模組實現Java™身份驗證和授權服務(JAAS)規範。 查看 [官方OracleJava™安全參考指南](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) 的子菜單。

其工作是定義要使用的身份提供程式和同步處理程式，有效地綁定兩個模組。

以下配置選項可用：

| **JAAS排名** | 指定此登錄模組條目的等級（即排序順序）。 這些條目按降序排序（即，排名較高的配置優先）。 |
|---|---|
| **JAAS控制標誌** | 指定LOGINModule是必需、PROMENTIAL、EFPULITION還是OPTIONAL的屬性。 有關這些標誌含義的詳細資訊，請參閱JAAS配置文檔。 |
| **雅斯王國** | 註冊LoginModule的領域名稱（或應用程式名稱）。 如果未提供領域名稱，則LoginModule將註冊到Felix JAAS配置中配置的預設領域。 |
| **標識提供程式名稱** | 標識提供程式的名稱。 |
| **同步處理程式名稱** | 同步處理程式的名稱。 |

>[!NOTE]
如果您計畫與實例一起使用多個LDAP配置AEM，則必須為每個配置建立單獨的身份提供程式和同步處理程式。

## 通過SSL配置LDAP {#configure-ldap-over-ssl}

按AEM照以下步驟配置6以通過SSL進行LDAP驗證：

1. 檢查 **使用SSL** 或 **使用TLS** 複選框 [LDAP標識提供程式](#configuring-the-ldap-identity-provider)。
1. 根據您的設定配置同步處理程式和外部登錄模組。
1. 如果需要，請在Java™ VM中安裝SSL證書。 此安裝可通過使用keytool完成：

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Test到LDAP伺服器的連接。

### 建立SSL證書 {#creating-ssl-certificates}

通過SSL配置到LDAP驗證時，可AEM以使用自簽名證書。 下面是生成用於的證書的工作過程示例AEM。

1. 確保已安裝並正在運行SSL庫。 此過程以OpenSSL為例。

1. 建立自定義的OpenSSL配置(cnf)檔案。 可以通過複製預設的**openssl.cnf **配置檔案並自定義它來完成此配置。 在UNIX®系統上，它位於 `/usr/lib/ssl/openssl.cnf`

1. 通過在終端中運行以下命令，繼續建立CA根鍵：

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 接下來，建立自簽名證書：

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. 要確保一切正常，請檢查新生成的證書：

   `openssl x509 -noout -text -in root-ca.crt`

1. 確保證書配置(.cnf)檔案中指定的所有資料夾都存在。 否則，建立它們。
1. 通過運行(例如：

   `openssl rand -out private/.rand 8192`

1. 將建立的.pem檔案移動到.cnf檔案中配置的位置。

1. 最後，將證書添加到Java™密鑰庫。

## 啟用調試日誌記錄 {#enabling-debug-logging}

可以為LDAP身份提供程式和外部登錄模組啟用調試日誌記錄以解決連接問題。

要啟用調試日誌記錄，必須執行以下操作：

1. 轉到Web管理控制台。
1. 查找「Apache Sling日誌記錄記錄器配置」，並建立兩個具有以下選項的記錄器：

* 日誌級別：調試
* 日誌檔案logs/ldap.log
* 消息模式：{0，日期，dd.MM.yyyy HH:mm:ss.SSS}&amp;ast;{4}&amp;ast;{2} {3} {5}
* 記錄器：org.apache.jackrabbit.oak.security.authentication.ldap

* 日誌級別：調試
* 日誌檔案：logs/external.log
* 消息模式：{0，日期，dd.MM.yyyy HH:mm:ss.SSS}&amp;ast;{4}&amp;ast;{2} {3} {5}
* 記錄器：org.apache.jackrabbit.oak.spi.security.authentication.external

## 關於群體隸屬關係 {#a-word-on-group-affiliation}

通過LDAP同步的用戶可以是中不同組的一AEM部分。 這些組可以是作為同步過程的一部分添加AEM到的外部LDAP組。 但是，它們也可以是單獨添加的組，並且不是原始LDAP組隸屬方案的一部分。

通常，這些組由本地管理員或AEM任何其他身份提供程式添加。

如果從LDAP伺服器上的組中刪除用戶，則同步時會在一AEM側反映更改。 但是，未由LDAP添加的用戶的所有其他組從屬關係仍然有效。

通過AEM使用 `rep:externalId` 屬性。 此屬性將自動添加到同步處理程式同步的任何用戶或組，並包含有關原始身份提供程式的資訊。

請參閱上的Apache Oak文檔 [用戶和組同步](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html)。

## 已知問題 {#known-issues}

如果計畫通過SSL使用LDAP，請確保建立您使用的證書時沒有使用Netscape注釋選項。 如果啟用此選項，驗證將失敗，並出現SSL握手錯誤。
