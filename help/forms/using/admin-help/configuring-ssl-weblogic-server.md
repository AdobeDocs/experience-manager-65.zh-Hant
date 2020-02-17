---
title: 為WebLogic伺服器配置SSL
seo-title: 為WebLogic伺服器配置SSL
description: 瞭解如何建立SSL憑證以用於WebLogic伺服器，以及如何為WebLogic伺服器設定SSL。
seo-description: 瞭解如何建立SSL憑證以用於WebLogic伺服器，以及如何為WebLogic伺服器設定SSL。
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# 為WebLogic伺服器配置SSL {#configuring-ssl-for-weblogic-server}

若要在WebLogic伺服器上設定SSL，您需要驗證的SSL憑證。 您可以使用Java鍵工具執行下列工作來建立憑證：

* 建立公用／私用金鑰對、將公用金鑰包裝在X.509 v1自簽名憑證中，並儲存為單一元素憑證鏈，然後將憑證鏈和私用金鑰儲存在新的金鑰庫中。 此密鑰庫是應用程式伺服器的自訂身分密鑰庫。
* 擷取憑證並將其插入新的金鑰庫。 此金鑰庫是應用程式伺服器的自訂信任金鑰庫。

然後，設定WebLogic，使其使用您建立的自訂身分密鑰庫和自訂信任密鑰庫。 此外，由於用於建立密鑰庫檔案的唯一判別名不包括托管WebLogic的電腦的名稱，因此禁用「WebLogic主機名驗證」功能。

## 建立SSL憑證以用於WebLogic伺服器 {#creating-an-ssl-credential-for-use-on-weblogic-server}

keytool命令通常位於Java jre/bin目錄中，且必須包含數個選項和選項值，這些選項和選項值列在下表中。

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
   <td><p>-alias</p></td>
   <td><p>密鑰庫的別名。</p></td>
   <td>
    <ul>
     <li><p>自訂身分密鑰庫： <code>ads-credentials</code></p></li>
     <li><p>自訂信任金鑰庫： <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>用於生成密鑰對的算法。</p></td>
   <td><p>RSA</p><p>您可以根據公司的政策，使用不同的演算法。</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>密鑰庫檔案的位置和名稱。</p><p>該位置可以包含檔案的絕對路徑。 或者，它可以相對於輸入keytool命令的命令提示符的當前目錄。</p></td>
   <td>
    <ul>
     <li><p>自訂身分密鑰庫： <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[伺服器名稱]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>自訂信任金鑰庫： <code>[</code><i>appserverdomain]</i><code>/adobe/</code><i>[伺服器名稱]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>證書檔案的位置和名稱。</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>認為證書有效的天數。</p></td>
   <td><p>3650</p><p>您可以使用不同的值，視您公司的政策而定。</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>保護密鑰庫內容的口令。 </p></td>
   <td>
    <ul>
     <li><p>自訂身分密鑰庫：密鑰庫密碼必須與為管理控制台的信任儲存元件指定的SSL憑證密碼對應。</p></li>
     <li><p>自訂信任金鑰庫：使用與您用於自訂身分密鑰庫的相同密碼。</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>保護密鑰對的私鑰的口令。</p></td>
   <td><p>使用與您用於選項的相同密 <code>-storepass</code> 碼。 密鑰密碼必須至少為6個字元。</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>標識擁有密鑰庫的人員的可辨識名稱。</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> 是擁有密鑰庫的用戶的標識。</p></li>
     <li><p><code><i>[Group Name]</i></code> 是密鑰庫所有者所屬的公司組的標識。</p></li>
     <li><p><code><i>[Company Name]</i></code> 是您組織的名稱。</p></li>
     <li><p><code><i>[City Name]</i></code> 是貴組織所在的城市。</p></li>
     <li><p><code><i>[State or province]</i></code> 是貴組織所在的州或省。</p></li>
     <li><p><code><i>[Country Code]</i></code> 是貴組織所在國家／地區的雙字母代碼。</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

如需使用keytool命令的詳細資訊，請參閱JDK檔案中的keytool.html檔案。

## 建立自訂身分與信任關鍵庫 {#create-the-custom-identity-and-trust-keystores}

1. 在命令提示符下，導 *[覽至appserverdomain]*/adobe/*[server name]*。
1. 輸入以下命令：

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >以 `[JAVA_HOME]`*安裝JDK的目錄取代，並以與您的環境對應的值取代斜體文字。*

   例如：

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   名為&quot;ads-credentials.jks&quot;的自訂身分密鑰庫檔案會建立在 [appserverdomain]/adobe/[server name目錄中] 。

1. 輸入以下命令，從ads-credentials密鑰庫中提取證書：

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >以 `[JAVA_HOME]` 安裝JDK的目錄取代，並以自訂身分密鑰庫的 `store`**`password`密碼取代_*。*

   例如：

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   名為&quot;ads-ca.cer&quot;的憑證檔案會建立在 [appserverdomain]/adobe/[*server name目錄中*] 。

1. 將ads-ca.cer檔案複製至需要與應用程式伺服器進行安全通訊的任何主機。
1. 輸入以下命令，將證書插入新的密鑰庫檔案（自定義信任密鑰庫）:

   [JAVA_HOME]`/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >以安 `[JAVA_HOME]` 裝JDK的目錄取代，並以您自己的密碼取代 `store`*_*_和_`password``key`**`password`*_ 。*

   例如：

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

名為&quot;ads-ca.jks&quot;的自訂信任密鑰庫檔案會建立在 [appserverdomain]/adobe/[server] 目錄中。

設定WebLogic，使其使用您建立的自訂身分密鑰庫和自訂信任密鑰庫。 此外，由於用於建立密鑰庫檔案的唯一判別名不包括托管WebLogic伺服器的電腦名，因此禁用WebLogic主機名驗證功能。

## 設定WebLogic以使用SSL {#configure-weblogic-to-use-ssl}

1. 在Web瀏覽器的URL行中輸入 `https://`*[主機名稱&#x200B;]*`:7001/console`，啟動WebLogic server管理控制台。
1. 在「環境」下的「域配置」中，選 **擇「服[務器]」>「配置」>「常規」**。
1. 在「常規」下，在「配置」中，確 **保選擇「啟用監聽端** 」 **和「啟用SSL監聽埠** 」。 如果未啟用，請執行下列動作：

   1. 在「變更中心」(Change Center)下，按一下「 **鎖定並編輯」(Lock &amp; Edit** )以修改選擇和值。
   1. 選中「 **Listen Port Enabled(啟用監聽埠** )」和「 **SSL Listen Port Enabled(啟用監聽埠** )」複選框。

1. 如果此伺服器是受控伺服器，請將「監聽埠」更改為未使用的埠值（如8001），將「SSL監聽埠」更改為未使用的埠值（如8002）。 在獨立伺服器上，預設的SSL埠為7002。
1. 按一 **下「發行設定**」。
1. 在「環境」下的「域配置」中，單 **擊「服&#x200B;[*務器」>「受控伺服器*]」>「配置」>「常規」**。
1. 在「常規」下，在「配置」中，選擇「 **Keystores**」。
1. 在「變更中心」(Change Center)下，按一下「 **鎖定並編輯」(Lock &amp; Edit** )以修改選擇和值。
1. 按一 **下「變更** 」，以將密鑰庫清單取為下拉式清單，並選取「自訂身 **分和自訂信任」**。
1. 在「身分」下，指定下列值：

   **自訂身分密鑰庫**: *[appserverdomain]*/adobe/*[server name]*/ads-credentials.jks，其中*[appserverdomain] *是實際路徑，而伺服器 *[]* 名稱是應用程式伺服器的名稱。

   **自訂身份密鑰庫類型**:JKS

   **自訂身分密鑰庫密碼**: *mypassword* （自訂身分密鑰庫密碼）

1. 在「信任」下，指定下列值：

   **自定義信任密鑰庫檔案名**: `*[appserverdomain]*/adobe/*[server]*/ads-ca.jks`，其中 `*[appserverdomain]*` 是實際路徑

   **自定義信任密鑰庫類型**:JKS

   **自訂信任金鑰庫密碼片語**: *mypassword* （自訂信任金鑰密碼）

1. 在「常規」下的「配置」中，選擇 **SSL**。
1. 預設情況下，為「身份和信任位置」選擇「密鑰庫」。 否則，請將其更改為密鑰庫。
1. 在「身分」下，指定下列值：

   **私密金鑰別名**:ads-credentials

   **密碼短語**: *mypassword*

1. 按一 **下「發行設定**」。

## 禁用主機名驗證功能 {#disable-the-hostname-verification-feature}

1. 在「設定」標籤上，按一下「SSL」。
1. 在「高級」下，從「主機名驗證」清單中選擇「無」。

   如果未禁用主機名驗證，則公共名稱(CN)必須包含伺服器主機名。

1. 在「更改中心」(Change Center)下，按一下「鎖定和編輯」(Lock &amp; Edit)以修改選擇和值。
1. 重新啟動應用程式伺服器。

