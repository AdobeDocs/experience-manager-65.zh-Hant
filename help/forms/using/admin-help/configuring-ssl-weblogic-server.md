---
title: 為WebLogic Server設定SSL
seo-title: Configuring SSL for WebLogic Server
description: 瞭解如何建立SSL認證以用於WebLogic伺服器，以及如何設定WebLogic伺服器的SSL。
seo-description: Learn how to create an SSL credential for use on WebLogic server and how to configure SSL for WebLogic Server.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 1%

---


# 為WebLogic Server設定SSL {#configuring-ssl-for-weblogic-server}

若要在WebLogic Server上設定SSL，您需要用於驗證的SSL認證。 您可以使用Java keytool執行下列工作來建立認證：

* 建立公開/私密金鑰組，將公開金鑰包裝在X.509 v1自我簽署憑證（儲存為單一元素憑證鏈）中，然後將憑證鏈結和私密金鑰儲存在新的金鑰儲存庫中。 此金鑰存放區是應用程式伺服器的自訂身分金鑰存放區。
* 擷取憑證並將其插入新的金鑰存放區。 此金鑰存放區是應用程式伺服器的自訂信任金鑰存放區。

接著，設定WebLogic，使其使用您建立的「自訂身分」金鑰儲存庫和「自訂信任」金鑰儲存庫。 此外，請停用「WebLogic主機名稱驗證」功能，因為用來建立金鑰存放區檔案的辨別名稱不包含裝載WebLogic的電腦名稱。

## 建立SSL認證以用於WebLogic Server {#creating-an-ssl-credential-for-use-on-weblogic-server}

keytool指令通常位於Java jre/bin目錄中，而且必須包含下表所列的多個選項和選項值。

<table>
 <thead>
  <tr>
   <th><p>Keytool選項</p></th>
   <th><p>說明</p></th>
   <th><p>選項值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p> — 別名</p></td>
   <td><p>金鑰存放區的別名。</p></td>
   <td>
    <ul>
     <li><p>自訂身分金鑰存放區： <code>ads-credentials</code></p></li>
     <li><p>自訂信任金鑰存放區： <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>用來產生金鑰組的演演算法。</p></td>
   <td><p>RSA</p><p>您可以使用不同的演演算法，具體取決於貴公司的原則。</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>金鑰存放區檔案的位置和名稱。</p><p>位置可包含檔案的絕對路徑。 或者，它可以相對於命令提示字元目前的目錄，也就是輸入keytool命令的位置。</p></td>
   <td>
    <ul>
     <li><p>自訂身分金鑰存放區： <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[伺服器名稱]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>自訂信任金鑰存放區： <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[伺服器名稱]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>憑證檔案的位置和名稱。</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>憑證被視為有效的天數。</p></td>
   <td><p>3650</p><p>您可以使用不同的值，具體取決於貴公司的原則。</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>保護金鑰存放區內容的密碼。 </p></td>
   <td>
    <ul>
     <li><p>自訂身分識別金鑰存放區：金鑰存放區密碼必須與為Administration Console的Trust Store元件所指定的SSL認證密碼相對應。</p></li>
     <li><p>自訂信任金鑰存放區：使用與自訂身分金鑰存放區相同的密碼。</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>保護金鑰組私密金鑰的密碼。</p></td>
   <td><p>使用您用於的相同密碼 <code>-storepass</code> 選項。 金鑰密碼必須至少為六個字元。</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>識別金鑰儲存庫擁有者的辨別名稱。</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> 是擁有金鑰存放區之使用者的身分識別。</p></li>
     <li><p><code><i>[Group Name]</i></code> 是金鑰存放區擁有者所屬的公司群組的識別碼。</p></li>
     <li><p><code><i>[Company Name]</i></code> 是您組織的名稱。</p></li>
     <li><p><code><i>[City Name]</i></code> 是您的組織所在的城市。</p></li>
     <li><p><code><i>[State or province]</i></code> 是貴組織所在的州或省。</p></li>
     <li><p><code><i>[Country Code]</i></code> 是貴組織所在國家/地區的雙字母代碼。</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

如需有關使用keytool指令的詳細資訊，請參閱keytool.html檔案，此檔案是JDK檔案的一部分。

## 建立自訂身分和信任金鑰存放區 {#create-the-custom-identity-and-trust-keystores}

1. 在命令提示字元中，瀏覽至 *[appserverdomain]*/adobe/*[伺服器名稱]*.
1. 輸入以下命令：

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >取代 `[JAVA_HOME]`*使用安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   名為「ads-credentials.jks」的自訂身分識別金鑰存放區檔案會建立於 [appserverdomain]/adobe/[伺服器名稱] 目錄。

1. 輸入以下命令，從ads-credentials金鑰儲存區擷取憑證：

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**密碼**

   >[!NOTE]
   >
   >取代 `[JAVA_HOME]` ，並使用安裝JDK的目錄取代 `store`*_* `password`*使用自訂身分金鑰儲存庫的密碼。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   名為「ads-ca.cer」的憑證檔案建立於 [appserverdomain]/adobe/[*伺服器名稱*] 目錄。

1. 將ads-ca.cer檔案複製到任何需要與應用程式伺服器安全通訊的主機電腦。
1. 輸入下列命令，將憑證插入新的金鑰儲存庫檔案（自訂信任金鑰儲存庫）：

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >取代 `[JAVA_HOME]` ，並使用安裝JDK的目錄取代 `store`*_* `password` 和 `key`*_* `password` *使用您自己的密碼。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

名為「ads-ca.jks」的自訂信任金鑰存放區檔案會建立於 [appserverdomain]/adobe/&#39;server&#39;目錄。

設定WebLogic，使其使用您建立的自訂身分金鑰儲存庫和自訂信任金鑰儲存庫。 此外，請停用「WebLogic主機名稱驗證」功能，因為用來建立金鑰存放區檔案的辨別名稱不包含裝載WebLogic Server的電腦名稱。

## 設定WebLogic以使用SSL {#configure-weblogic-to-use-ssl}

1. 輸入WebLogic伺服器管理主控台，以啟動 `https://`*[主機名稱&#x200B;]*`:7001/console` 在網頁瀏覽器的URL行中。
1. 在「環境」下的「網域設定」中，選取 **伺服器> &#39;伺服器&#39; >設定>一般**.
1. 在「一般」底下的「組態」中，確認 **監聽連線埠已啟用** 和 **已啟用SSL監聽連線埠** 已選取。 如果未啟用，請執行下列動作：

   1. 在「變更中心」下，按一下 **鎖定和編輯** 修改選取範圍和值。
   1. 檢查 **監聽連線埠已啟用** 和 **已啟用SSL監聽連線埠** 核取方塊。

1. 如果此伺服器是受管理的伺服器，請將監聽連線埠變更為未使用的連線埠值（例如8001），並將SSL監聽連線埠變更為未使用的連線埠值（例如8002）。 在獨立伺服器上，預設的SSL連線埠為7002。
1. 按一下 **發行設定**.
1. 在環境底下的網域設定中，按一下 **伺服器> [*受管理的伺服器*] >設定>一般**.
1. 在一般底下的組態中，選取 **金鑰存放區**.
1. 在「變更中心」下，按一下 **鎖定和編輯** 修改選取範圍和值。
1. 按一下 **變更** 若要以下拉式清單形式取得金鑰存放區清單，請選取 **自訂身分和自訂信任**.
1. 在「識別」下，指定下列值：

   **自訂身分識別金鑰存放區**： *[appserverdomain]*/adobe/*[伺服器名稱]*/ads-credentials.jks，其中*[appserverdomain] *是實際路徑，且 *[伺服器名稱]* 是應用程式伺服器的名稱。

   **自訂身分金鑰存放區型別**：JKS

   **自訂身分金鑰庫密碼**： *我的密碼* （自訂身分金鑰庫密碼）

1. 在「信任」底下，指定下列值：

   **自訂信任Keystore檔案名稱**： `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`，其中 `*[appserverdomain]*` 是實際路徑

   **自訂信任金鑰存放區型別**：JKS

   **自訂信任金鑰庫密語**： *我的密碼* （自訂信任金鑰密碼）

1. 在一般底下的組態中，選取 **SSL**.
1. 依預設，會針對識別與信任位置選取Keystore。 如果沒有，請將其變更為Keystore。
1. 在「識別」下，指定下列值：

   **私密金鑰別名**： ads-credentials

   **複雜密碼**： *我的密碼*

1. 按一下 **發行設定**.

## 停用主機名稱驗證功能 {#disable-the-hostname-verification-feature}

1. 在「組態」標籤上，按一下「SSL」。
1. 在「進階」下，從「主機名稱驗證」清單中選擇「無」。

   如果未停用主機名稱驗證，一般名稱(CN)必須包含伺服器主機名稱。

1. 在「變更中心」下，按一下「鎖定與編輯」來修改選取專案和值。
1. 重新啟動應用程式伺服器。

