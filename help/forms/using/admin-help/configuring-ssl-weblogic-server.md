---
title: 為WebLogic伺服器配置SSL
seo-title: Configuring SSL for WebLogic Server
description: 了解如何建立要在WebLogic伺服器上使用的SSL憑證，以及如何為WebLogic伺服器配置SSL。
seo-description: Learn how to create an SSL credential for use on WebLogic server and how to configure SSL for WebLogic Server.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---


# 為WebLogic伺服器配置SSL {#configuring-ssl-for-weblogic-server}

若要在WebLogic伺服器上設定SSL，您需要SSL憑證才能進行驗證。 您可以使用Java鍵工具執行下列任務以建立憑據：

* 建立公開/私密金鑰組，將公開金鑰包裝在X.509 v1自行簽署的憑證中（以單一元素憑證鏈形儲存），然後將憑證鏈和私密金鑰儲存在新金鑰存放區中。 此金鑰存放區是應用程式伺服器的自訂身分金鑰存放區。
* 擷取憑證並將其插入新的金鑰存放區。 此密鑰庫是應用程式伺服器的自定義信任密鑰庫。

然後，配置WebLogic，使其使用您建立的自訂身分金鑰存放區和自訂信任金鑰存放區。 另外，禁用WebLogic主機名驗證功能，因為用於建立密鑰庫檔案的可分辨名稱不包含承載WebLogic的電腦的名稱。

## 建立SSL憑據以在WebLogic伺服器上使用 {#creating-an-ssl-credential-for-use-on-weblogic-server}

keytool命令通常位於Java jre/bin目錄中，並且必須包括下表中列出的多個選項和選項值。

<table>
 <thead>
  <tr>
   <th><p>鍵工具選項</p></th>
   <th><p>說明</p></th>
   <th><p>選項值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>金鑰存放區的別名。</p></td>
   <td>
    <ul>
     <li><p>自訂身分金鑰存放區： <code>ads-credentials</code></p></li>
     <li><p>自定義信任密鑰庫： <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>用來產生索引鍵對的演算法。</p></td>
   <td><p>RSA</p><p>您可以根據公司的原則使用不同的演算法。</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>金鑰存放區檔案的位置和名稱。</p><p>位置可包含檔案的絕對路徑。 或者，它可以與輸入keytool命令的命令提示符的當前目錄相對。</p></td>
   <td>
    <ul>
     <li><p>自訂身分金鑰存放區： <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[伺服器名稱]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>自定義信任密鑰庫： <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[伺服器名稱]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>憑證檔案的位置和名稱。</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validity</p></td>
   <td><p>認為證書有效的天數。</p></td>
   <td><p>3650</p><p>您可以根據公司的原則使用不同的值。</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>保護金鑰存放區內容的密碼。 </p></td>
   <td>
    <ul>
     <li><p>自訂身分金鑰存放區：金鑰存放區密碼必須與為管理控制台的信任存放區元件指定的SSL憑據密碼相對應。</p></li>
     <li><p>自定義信任密鑰庫：使用與自訂身分金鑰存放區所用的相同密碼。</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>保護密鑰對的私鑰的密碼。</p></td>
   <td><p>使用與 <code>-storepass</code> 選項。 密鑰密碼必須至少為6個字元。</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>標識擁有密鑰庫的人員的可分辨名稱。</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> 是擁有金鑰存放區之使用者的身分識別。</p></li>
     <li><p><code><i>[Group Name]</i></code> 是金鑰存放區擁有者所屬之公司群組的識別碼。</p></li>
     <li><p><code><i>[Company Name]</i></code> 是貴組織的名稱。</p></li>
     <li><p><code><i>[City Name]</i></code> 是您的組織所在的城市。</p></li>
     <li><p><code><i>[State or province]</i></code> 是您的組織所在的州或省。</p></li>
     <li><p><code><i>[Country Code]</i></code> 是貴組織所在國家/地區的雙字母代碼。</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

有關使用keytool命令的詳細資訊，請參閱JDK文檔中的keytool.html檔案。

## 建立自訂身分和信任金鑰存放區 {#create-the-custom-identity-and-trust-keystores}

1. 從命令提示字元導覽至 *[appserverdomain]*/adobe/*[伺服器名稱]*.
1. 輸入以下命令：

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >取代 `[JAVA_HOME]`*使用安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   名為「ads-credentials.jks」的自訂身分金鑰存放區檔案會建立在 [appserverdomain]/adobe/[伺服器名稱] 目錄。

1. 輸入下列命令，從ads-credentials金鑰存放區中擷取憑證：

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**密碼**

   >[!NOTE]
   >
   >取代 `[JAVA_HOME]` 使用安裝JDK的目錄，然後取代 `store`*_* `password`*使用自訂身分金鑰存放區的密碼。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   名為「ads-ca.cer」的憑證檔案會建立在 [appserverdomain]/adobe/[*伺服器名稱*] 目錄。

1. 將ads-ca.cer檔案複製到需要與應用程式伺服器進行安全通信的任何主機。
1. 輸入以下命令，將憑證插入新的金鑰存放區檔案（自訂信任金鑰存放區）:

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >取代 `[JAVA_HOME]` 使用安裝JDK的目錄，然後取代 `store`*_* `password` 和 `key`*_* `password` *密碼。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

名為「ads-ca.jks」的自訂信任金鑰存放區檔案會建立在 [appserverdomain]/adobe/&#39;server&#39;目錄。

配置WebLogic，使其使用您建立的自訂身分金鑰存放區和自訂信任金鑰存放區。 另外，禁用WebLogic主機名驗證功能，因為用於建立密鑰庫檔案的可分辨名稱不包含承載WebLogic Server的電腦的名稱。

## 配置WebLogic以使用SSL {#configure-weblogic-to-use-ssl}

1. 輸入 `https://`*[主機名稱&#x200B;]*`:7001/console` 在網頁瀏覽器的URL行中。
1. 在「環境」下，在「域配置」中，選擇 **「伺服器」>「伺服器」>「配置」>「一般」**.
1. 在「一般」下，在「配置」中，確保 **已啟用偵聽埠** 和 **已啟用SSL偵聽埠** 中所有規則的URL。 如果未啟用，請執行下列操作：

   1. 在「變更中心」(Change Center)下，按一下 **鎖定和編輯** 來修改選取範圍和值。
   1. 檢查 **已啟用偵聽埠** 和 **已啟用SSL偵聽埠** 框。

1. 如果此伺服器是受管伺服器，請將偵聽埠更改為未使用的埠值（如8001），將SSL偵聽埠更改為未使用的埠值（如8002）。 在獨立伺服器上，預設SSL埠為7002。
1. 按一下 **發行設定**.
1. 在「環境」下，按一下「域配置」中的 **伺服器> [*托管伺服器*] >設定>一般**.
1. 在「常規」下，在「配置」中，選擇 **鑰匙庫**.
1. 在「變更中心」(Change Center)下，按一下 **鎖定和編輯** 來修改選取範圍和值。
1. 按一下 **變更** 若要將金鑰存放區清單設為下拉式清單，請選取 **自訂身分和自訂信任**.
1. 在「身分」下，指定下列值：

   **自訂身分金鑰存放區**: *[appserverdomain]*/adobe/*[伺服器名稱]*/ads-credentials.jks，其中*[appserverdomain] *是實際路徑， *[伺服器名稱]* 是應用程式伺服器的名稱。

   **自訂身分金鑰存放區類型**:JKS

   **自訂身份密鑰庫密碼**: *mypassword* （自訂身分金鑰存放區密碼）

1. 在「信任」下，指定以下值：

   **自定義信任密鑰庫檔案名**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`，其中 `*[appserverdomain]*` 是實際路徑

   **自定義信任密鑰庫類型**:JKS

   **自定義信任密鑰庫密碼片語**: *mypassword* （自定義信任密鑰密碼）

1. 在「常規」下，在「配置」中，選擇 **SSL**.
1. 預設情況下，為身份和信任位置選擇密鑰庫。 否則，將其變更為金鑰存放區。
1. 在「身分」下，指定下列值：

   **私鑰別名**:ads-credentials

   **密碼短語**: *mypassword*

1. 按一下 **發行設定**.

## 禁用主機名驗證功能 {#disable-the-hostname-verification-feature}

1. 在「設定」標籤上，按一下「SSL」。
1. 在「高級」下，從「主機名驗證」清單中選擇「無」。

   如果未禁用主機名驗證，則公用名(CN)必須包含伺服器主機名。

1. 在「更改中心」(Change Center)下，按一下「鎖定和編輯」(Lock &amp; Edit)以修改選取範圍和值。
1. 重新啟動應用程式伺服器。

