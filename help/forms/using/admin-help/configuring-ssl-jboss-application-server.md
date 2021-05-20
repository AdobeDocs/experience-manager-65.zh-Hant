---
title: 為JBoss Application Server配置SSL
seo-title: 為JBoss Application Server配置SSL
description: 了解如何為JBoss Application Server設定SSL。
seo-description: 了解如何為JBoss Application Server設定SSL。
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 為JBoss Application Server {#configuring-ssl-for-jboss-application-server}配置SSL

若要在JBoss Application Server上設定SSL，您需要SSL憑證才能進行驗證。 您可以使用Java鍵工具建立憑據或請求，並從證書頒發機構(CA)導入憑據。 然後，您必須在JBoss上啟用SSL。

您可以使用包含建立金鑰存放區所需所有資訊的單一命令來執行keytool。

在此過程中：

* `[appserver root]` 是執行AEM表單之應用程式伺服器的主目錄。
* `[type]` 資料夾名稱會因您執行的安裝類型而異。

## 建立SSL憑據{#create-an-ssl-credential}

1. 在命令提示符下，導航到&#x200B;*[JAVA HOME]*/bin ，然後鍵入以下命令以建立憑據和密鑰庫：

   `keytool -genkey -dname "CN=`*主* `, OU=`*機名* `, O=`*稱組名* `,L=`*稱公司名* `, S=`** `, C=`稱城市名稱狀態國 `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*家代碼」key_* `-keystore`*passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >將`[JAVA_HOME]`替換為安裝JDK的目錄，並將斜體文字替換為與您的環境相對應的值。 主機名是應用程式伺服器的完全限定域名。

1. 在提示輸入密碼時輸入`keystore_password`。 金鑰存放區和金鑰的密碼必須相同。

   >[!NOTE]
   >
   >在此步驟中輸入的`keystore_password` *可能與在步驟1中輸入的相同，或者可能不同。*

1. 鍵入以下命令之一，將&#x200B;*keystorename*.keystore複製到`[appserver root]/server/[type]/conf`目錄：

   * （Windows單伺服器）`copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows伺服器群集）複製`keystorename.keystore[appserver root]\domain\configuration`
   * （Linux單伺服器）`cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux伺服器群集）`cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 輸入以下命令以導出證書檔案：

   * （單伺服器）`keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （伺服器群集）`keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 在提示輸入密碼時，輸入&#x200B;*keystore_password*。
1. 鍵入以下命令，將AEMForms_cert.cer檔案複製到&#x200B;*[appserver root] \conf*&#x200B;目錄：

   * （Windows單伺服器）`copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows伺服器群集）`copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux單伺服器）`cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux伺服器群集）`cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 鍵入以下命令查看證書的內容：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 要提供對`[JAVA_HOME]\jre\lib\security`中快取檔案的寫訪問，如果需要，請執行以下任務：

   * (Windows)按一下右鍵快取檔案，選擇「屬性」，然後取消選擇「只讀」屬性。
   * (Linux)類型`chmod 777 cacerts`

1. 輸入以下命令以匯入憑證：

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_* `.cer -keystore`*certJAVA_HOME* `\jre\lib\security\cacerts`

1. 鍵入`changeit`作為密碼。 此密碼是Java安裝的預設密碼，可能已由系統管理員更改。
1. 提示輸入`Trust this certificate? [no]`時，鍵入`yes`。 將顯示確認「已將憑證新增至金鑰存放區」。
1. 如果您從Workbench透過SSL連線，請在Workbench電腦上安裝憑證。
1. 在文字編輯器中，開啟下列檔案以進行編輯：

   * 單伺服器 — `[appserver root]`/standalone/configuration/lc_&lt;dbname/tunkley>.xml

   * 伺服器群集 — `[appserver root]`/domain/configuration/host.xml

   * 伺服器群集 — `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **若為單一伺服器，** 在lc_&lt;dbaname>.xml檔案中，於區段後新增 &lt;security-realms> 下列：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   找到下列程式碼後面出現的`<server>`區段：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列程式碼新增至上述程式碼後面出現的&lt;server>區段：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **若為伺服器叢集，** 在所有節 [點上的appserver根]\domain\configuration\host.xml中，於區段後新增下列 &lt;security-realms> 項目：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在伺服器群集的主節點上，在[appserver root]\domain\configuration\domain_&lt;dbname>.xml中，找到以下代碼後出現的&lt;server>節：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列程式碼新增至上述程式碼後面出現的&lt;server>區段：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 將`keystoreFile`屬性和`keystorePass`屬性的值更改為建立密鑰庫時指定的密鑰庫密碼。
1. 重新啟動應用程式伺服器：

   * 對於統包安裝：

      * 在Windows控制面板中，按一下「管理工具」，然後按一下「服務」。
      * 選取Adobe Experience Manager表單適用的JBoss。
      * 選擇操作>停止。
      * 等待服務狀態顯示為已停止。
      * 選擇操作>開始。
   * 對於Adobe預配置或手動配置的JBoss安裝：

      * 從命令提示字元，導覽至&#x200B;*`[appserver root]`*/bin。
      * 輸入以下命令以停止伺服器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * 等到JBoss進程完全關閉（當JBoss進程將控制返回到其啟動的終端時）。
      * 輸入以下命令以啟動伺服器：

         * (Windows)`run.bat -c <profile>`
         * (Linux)`./run.sh -c <profile>`



1. 若要使用SSL存取管理控制台，請在網頁瀏覽器中輸入`https://[host name]:'port'/adminui`:

   JBoss的預設SSL埠為8443。 從這裡，在存取AEM表單時指定此連接埠。

## 從CA {#request-a-credential-from-a-ca}請求憑據

1. 在命令提示字元中，導覽至&#x200B;*[JAVA HOME]*/bin ，然後輸入以下命令以建立金鑰存放區和金鑰：

   `keytool -genkey -dname "CN=`*主* `, OU=`*機名* `, O=`*稱組名* `, L=`*稱公司名* `, S=`** `, C=`*稱城市名稱狀態國家代碼* `-alias "AEMForms Cert"` `-keyalg RSA -keypass`&quot; - *key_* `-keystore`*passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >將&#x200B;*`[JAVA_HOME]`*&#x200B;替換為安裝JDK的目錄，並將斜體文字替換為與您的環境相對應的值。

1. 鍵入以下命令生成要發送到證書頒發機構的證書請求：

   `keytool -certreq -alias` &quot;AEMForms Cert&quot;  `-keystore`** `.keystore -file`*keystorenameAEMFormscertRequest.csr*

1. 當您的憑證檔案請求完成時，請完成下一個程式。

## 使用從CA獲取的憑據啟用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示符中，導航到&#x200B;*`[JAVA HOME]`*/bin並鍵入以下命令以導入已與CSR簽名的CA的根證書：

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   如果根憑證不在瀏覽器中，也請將其匯入該處。

   >[!NOTE]
   >
   >將&#x200B;*`[JAVA_HOME]`替換為安裝JDK的目錄，並將斜體文本替換為與您的環境相對應的值。*

1. 在命令提示符中，導航到&#x200B;*`[JAVA HOME]`*/bin ，然後鍵入以下命令以將憑據導入密鑰庫中：

   `keytool -import -trustcacerts -file`** `.crt -keystore`*CACertificateNamekeystorename* `.keystore`

   >[!NOTE]
   >
   >* 將`[JAVA_HOME]`替換為安裝JDK的目錄，並將斜體文字替換為與您的環境相對應的值。
   >* 導入的CA簽名證書將替換自簽名的公共證書（如果存在）。


1. 完成建立SSL憑證的步驟13 - 18。
