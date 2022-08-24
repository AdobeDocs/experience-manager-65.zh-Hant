---
title: 為WebLogic伺服器配置SSL
seo-title: Configuring SSL for WebLogic Server
description: 瞭解如何建立SSL憑據以在WebLogic伺服器上使用，以及如何為WebLogic伺服器配置SSL。
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

要在WebLogic Server上配置SSL，需要SSL憑據進行身份驗證。 可以使用Java鍵工具執行以下任務來建立憑據：

* 建立公共/私鑰對，將公鑰包裝在X.509 v1自簽名證書中，該證書儲存為單元素證書鏈，然後將證書鏈和私鑰儲存在新密鑰庫中。 此密鑰庫是應用程式伺服器的自定義標識密鑰庫。
* 提取證書並將其插入新密鑰庫。 此密鑰庫是應用程式伺服器的自定義信任密鑰庫。

然後，配置WebLogic，使其使用您建立的自定義標識密鑰庫和自定義信任密鑰庫。 另外，禁用WebLogic主機名驗證功能，因為用於建立密鑰庫檔案的可分辨名稱不包括承載WebLogic的電腦的名稱。

## 建立SSL憑據以在WebLogic伺服器上使用 {#creating-an-ssl-credential-for-use-on-weblogic-server}

keytool命令通常位於Java jre/bin目錄中，必須包括下表中列出的幾個選項和選項值。

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
   <td><p> — 別名</p></td>
   <td><p>密鑰庫的別名。</p></td>
   <td>
    <ul>
     <li><p>自定義標識密鑰庫： <code>ads-credentials</code></p></li>
     <li><p>自定義信任密鑰庫： <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>用於生成密鑰對的算法。</p></td>
   <td><p>RSA</p><p>您可以使用不同的算法，具體取決於您公司的策略。</p></td>
  </tr>
  <tr>
   <td><p> — 密鑰庫</p></td>
   <td><p>密鑰庫檔案的位置和名稱。</p><p>該位置可以包括檔案的絕對路徑。 或者，它可以相對於輸入keytool命令的命令提示符的當前目錄。</p></td>
   <td>
    <ul>
     <li><p>自定義標識密鑰庫： <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[伺服器名稱]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>自定義信任密鑰庫： <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[伺服器名稱]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p> — 檔案</p></td>
   <td><p>證書檔案的位置和名稱。</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p> — 有效性</p></td>
   <td><p>認為證書有效的天數。</p></td>
   <td><p>3650</p><p>根據公司的策略，您可以使用不同的值。</p></td>
  </tr>
  <tr>
   <td><p> — 儲存傳遞</p></td>
   <td><p>保護密鑰庫內容的口令。 </p></td>
   <td>
    <ul>
     <li><p>自定義標識密鑰庫：密鑰庫密碼必須與為管理控制台的信任儲存元件指定的SSL憑據密碼相對應。</p></li>
     <li><p>自定義信任密鑰庫：使用與自定義標識密鑰庫使用的口令相同。</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p> — 鍵通</p></td>
   <td><p>保護密鑰對的私鑰的密碼。</p></td>
   <td><p>使用與 <code>-storepass</code> 的雙曲餘切值。 密鑰密碼必須至少為6個字元。</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>標識擁有密鑰庫的人員的可分辨名稱。</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> 是擁有密鑰庫的用戶的標識。</p></li>
     <li><p><code><i>[Group Name]</i></code> 是密鑰庫所有者所屬的公司組的標識。</p></li>
     <li><p><code><i>[Company Name]</i></code> 是你組織的名字。</p></li>
     <li><p><code><i>[City Name]</i></code> 是您所在的城市。</p></li>
     <li><p><code><i>[State or province]</i></code> 是您的組織所在的州或省。</p></li>
     <li><p><code><i>[Country Code]</i></code> 是貴組織所在國家/地區的雙字母代碼。</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

有關使用keytool命令的詳細資訊，請參見JDK文檔中的keytool.html檔案。

## 建立自定義標識和信任密鑰庫 {#create-the-custom-identity-and-trust-keystores}

1. 從命令提示符導航到 *[appserverdomain]*/adobe/*[伺服器名稱]*。
1. 輸入以下命令：

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >替換 `[JAVA_HOME]`*將JDK安裝到的目錄中，並將斜體文本替換為與您的環境對應的值。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   在中建立名為&quot;ads-credentials.jks&quot;的自定義標識密鑰庫檔案 [appserverdomain]/adobe/[伺服器名稱] 的子菜單。

1. 通過輸入以下命令從ads-credentials密鑰庫中提取證書：

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**密碼**

   >[!NOTE]
   >
   >替換 `[JAVA_HOME]` 將JDK安裝到的目錄中，並替換 `store`*_* `password`*帶有自定義標識密鑰庫的口令。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   名為&quot;ads-ca.cer&quot;的證書檔案是在 [appserverdomain]/adobe/[*伺服器名稱*] 的子菜單。

1. 將ads-ca.cer檔案複製到需要與應用程式伺服器進行安全通信的任何主機。
1. 通過輸入以下命令將證書插入新密鑰庫檔案（自定義信任密鑰庫）:

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >替換 `[JAVA_HOME]` 將JDK安裝到的目錄中，並替換 `store`*_* `password` 和 `key`*_* `password` *密碼。*

   例如：

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

名為&quot;ads-ca.jks&quot;的自定義信任密鑰庫檔案是在 [appserverdomain]/adobe/&#39;server&#39;目錄。

配置WebLogic，使其使用您建立的自定義標識密鑰庫和自定義信任密鑰庫。 另外，禁用WebLogic主機名驗證功能，因為用於建立密鑰庫檔案的可分辨名稱不包括承載WebLogic Server的電腦的名稱。

## 將WebLogic配置為使用SSL {#configure-weblogic-to-use-ssl}

1. 通過鍵入以啟動WebLogic Server管理控制台 `https://`*[主機名&#x200B;]*`:7001/console` 的子菜單。
1. 在環境下，在域配置中，選擇 **伺服器>「伺服器」>配置>常規**。
1. 在「常規」下，在「配置」中，確保 **已啟用偵聽埠** 和 **已啟用SSL偵聽埠** 的上界。 如果未啟用，請執行以下操作：

   1. 在「變更中心」(Change Center)下，按一下 **鎖定和編輯** 修改選定內容和值。
   1. 檢查 **已啟用偵聽埠** 和 **已啟用SSL偵聽埠** 的雙曲餘切值。

1. 如果此伺服器是受控伺服器，請將偵聽埠更改為未使用的埠值（如8001），將SSL偵聽埠更改為未使用的埠值（如8002）。 在單機伺服器上，預設SSL埠為7002。
1. 按一下 **發佈配置**。
1. 在環境下，在域配置中，按一下 **伺服器> [*受控伺服器*] >配置>常規**。
1. 在常規下，在配置中，選擇 **密鑰庫**。
1. 在「變更中心」(Change Center)下，按一下 **鎖定和編輯** 修改選定內容和值。
1. 按一下 **更改** 要獲取密鑰庫清單作為下拉清單並選擇 **自定義標識和自定義信任**。
1. 在標識下，指定以下值：

   **自定義標識密鑰庫**: *[appserverdomain]*/adobe/*[伺服器名稱]*/ads-credentials.jks，其中*[appserverdomain] *是實際路徑 *[伺服器名稱]* 是應用程式伺服器的名稱。

   **自定義標識密鑰庫類型**:JKS

   **自定義標識密鑰庫密碼**: *mypassword* （自定義標識密鑰庫密碼）

1. 在信任下，指定以下值：

   **自定義信任密鑰庫檔案名**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`，也請參見Wiki頁。 `*[appserverdomain]*` 是實際路徑

   **自定義信任密鑰庫類型**:JKS

   **自定義信任密鑰庫密碼短語**: *mypassword* （自定義信任密鑰密碼）

1. 在常規下，在配置中，選擇 **SSL**。
1. 預設情況下，為「標識和信任位置」選擇「密鑰庫」。 否則，將其更改為密鑰庫。
1. 在標識下，指定以下值：

   **私鑰別名**:廣告憑證

   **密碼短語**: *mypassword*

1. 按一下 **發佈配置**。

## 禁用主機名驗證功能 {#disable-the-hostname-verification-feature}

1. 在「配置」頁籤上，按一下「SSL」。
1. 在「高級」下，從「主機名驗證」清單中選擇「無」。

   如果未禁用主機名驗證，則公用名(CN)必須包含伺服器主機名。

1. 在「變更中心」(Change Center)下，按一下「鎖定和編輯」(Lock &amp; Edit)以修改選定內容和值。
1. 重新啟動應用程式伺服器。

