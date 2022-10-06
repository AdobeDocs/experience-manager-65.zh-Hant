---
title: 為JBoss Application Server配置SSL
seo-title: Configuring SSL for JBoss Application Server
description: 了解如何為JBoss Application Server設定SSL。
seo-description: Learn how to configure SSL for JBoss Application Server.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---

# 為JBoss Application Server配置SSL {#configuring-ssl-for-jboss-application-server}

若要在JBoss Application Server上設定SSL，您需要SSL憑證才能進行驗證。 您可以使用Java鍵工具建立憑據或請求，並從證書頒發機構(CA)導入憑據。 然後，您必須在JBoss上啟用SSL。

您可以使用包含建立金鑰存放區所需所有資訊的單一命令來執行keytool。

在此過程中：

* `[appserver root]` 是執行AEM表單之應用程式伺服器的主目錄。
* `[type]` 資料夾名稱會因您執行的安裝類型而異。

## 建立SSL憑證 {#create-an-ssl-credential}

1. 在命令提示字元中，導覽至 *[JAVA首頁]*/bin並鍵入以下命令以建立憑據和密鑰庫：

   `keytool -genkey -dname "CN=`*主機名稱* `, OU=`*群組名稱* `, O=`*公司名稱* `,L=`*城市名稱* `, S=`*狀態* `, C=`國家/地區代碼」 `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >取代 `[JAVA_HOME]` 使用安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。 主機名是應用程式伺服器的完全限定域名。

1. 輸入 `keystore_password` 提示輸入密碼時。 金鑰存放區和金鑰的密碼必須相同。

   >[!NOTE]
   >
   >此 `keystore_password` *在此步驟中輸入的密碼可能與在步驟1中輸入的密碼相同，或者可能不同。*

1. 複製 *keystorename*.keystore到 `[appserver root]/server/[type]/conf` 目錄，方法是鍵入以下命令之一：

   * （Windows單伺服器） `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows Server群集）副本 `keystorename.keystore[appserver root]\domain\configuration`
   * （Linux單伺服器） `cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux伺服器群集） `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 輸入以下命令以導出證書檔案：

   * （單伺服器） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （伺服器群集） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 輸入 *keystore_password* 提示輸入密碼時。
1. 將AEMForms_cert.cer檔案複製到 *[appserver根] \conf* 目錄，方法是鍵入以下命令：

   * （Windows單伺服器） `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows Server群集） `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux單伺服器） `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux伺服器群集） `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 鍵入以下命令查看證書的內容：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 提供快取檔案的寫入訪問，位於 `[JAVA_HOME]\jre\lib\security`，視需要執行下列工作：

   * (Windows)按一下右鍵快取檔案，選擇「屬性」，然後取消選擇「只讀」屬性。
   * (Linux)類型 `chmod 777 cacerts`

1. 輸入以下命令以匯入憑證：

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. 類型 `changeit` 作為密碼。 此密碼是Java安裝的預設密碼，可能已由系統管理員更改。
1. 提示輸入時 `Trust this certificate? [no]`:，類型 `yes`. 將顯示確認「已將憑證新增至金鑰存放區」。
1. 如果您從Workbench透過SSL連線，請在Workbench電腦上安裝憑證。
1. 在文字編輯器中，開啟下列檔案以進行編輯：

   * 單伺服器 —  `[appserver root]`/standalone/configuration/lc_&lt;dbname turnkey=&quot;&quot;>.xml

   * 伺服器群集 —  `[appserver root]`/domain/configuration/host.xml

   * 伺服器群集 —  `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **對於單台伺服器，** 在lc_&lt;dbaname tunkey=&quot;&quot;>.xml檔案，在 &lt;security-realms> 小節：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   找出 `<server>` 下列程式碼後顯示的章節：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列項目新增至 &lt;server> 上述程式碼後出現的章節：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **對於伺服器群集，** 在 [appserver根]\domain\configuration\host.xml在所有節點上，在 &lt;security-realms> 小節：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在伺服器群集的主節點上， [appserver根]\domain\configuration\domain_&lt;dbname>.xml，找到 &lt;server> 下列程式碼後顯示的章節：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列項目新增至 &lt;server> 上述程式碼後出現的章節：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 變更 `keystoreFile` 屬性和 `keystorePass` 屬性至您建立金鑰存放區時指定的金鑰存放區密碼。
1. 重新啟動應用程式伺服器：

   * 對於統包安裝：

      * 在Windows控制面板中，按一下「管理工具」，然後按一下「服務」。
      * 選取Adobe Experience Manager表單適用的JBoss。
      * 選擇操作>停止。
      * 等待服務狀態顯示為已停止。
      * 選擇操作>開始。
   * 對於Adobe預配置或手動配置的JBoss安裝：

      * 從命令提示字元導覽至 *`[appserver root]`*/bin。
      * 輸入以下命令以停止伺服器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * 等到JBoss進程完全關閉（當JBoss進程將控制返回到其啟動的終端時）。
      * 輸入以下命令以啟動伺服器：

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. 若要使用SSL存取管理控制台，請輸入 `https://[host name]:'port'/adminui` 在網頁瀏覽器中：

   JBoss的預設SSL埠為8443。 從這裡，在存取AEM表單時指定此連接埠。

## 向CA請求憑據 {#request-a-credential-from-a-ca}

1. 在命令提示字元中，導覽至 *[JAVA首頁]*/bin ，並鍵入以下命令以建立密鑰庫和密鑰：

   `keytool -genkey -dname "CN=`*主機名稱* `, OU=`*群組名稱* `, O=`*公司名稱* `, L=`*城市名稱* `, S=`*狀態* `, C=`*國家/地區代碼*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >取代 *`[JAVA_HOME]`* 使用安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。

1. 鍵入以下命令生成要發送到證書頒發機構的證書請求：

   `keytool -certreq -alias` &quot;AEMForms Cert&quot; `-keystore`*keystorename* `.keystore -file`*AEMFormscertRequest.csr*

1. 當您的憑證檔案請求完成時，請完成下一個程式。

## 使用從CA獲得的憑據啟用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示字元中，導覽至 *`[JAVA HOME]`*/bin並鍵入以下命令以導入已簽名CSR的CA的根證書：

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   如果根憑證不在瀏覽器中，也請將其匯入該處。

   >[!NOTE]
   >
   >取代 *`[JAVA_HOME]`使用安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。*

1. 在命令提示字元中，導覽至 *`[JAVA HOME]`*/bin並鍵入以下命令將憑據導入密鑰庫中：

   `keytool -import -trustcacerts -file`*CACertificateName* `.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* 取代 `[JAVA_HOME]` 使用安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。
   >* 導入的CA簽名證書將替換自簽名的公共證書（如果存在）。


1. 完成建立SSL憑證的步驟13 - 18。
