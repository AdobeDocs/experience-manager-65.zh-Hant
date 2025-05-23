---
title: 為JBoss應用程式伺服器設定SSL
description: 瞭解如何設定JBoss Application Server的SSL。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# 為JBoss應用程式伺服器設定SSL {#configuring-ssl-for-jboss-application-server}

若要在JBoss Application Server上設定SSL，您需要用於驗證的SSL認證。 您可以使用Java keytool來建立認證，或是從憑證授權單位(CA)要求及匯入認證。 接著，您必須在JBoss上啟用SSL。

您可以使用包含建立金鑰儲存庫所需的所有資訊的單一指令來執行keytool。

在此程式中：

* `[appserver root]`是執行AEM表單的應用程式伺服器的主目錄。
* `[type]`是資料夾名稱，會依您執行的安裝型別而有所不同。

## 建立SSL認證 {#create-an-ssl-credential}

1. 在命令提示字元中，瀏覽至&#x200B;*[JAVA HOME]*/bin，然後輸入下列命令以建立認證和金鑰存放區：

   `keytool -genkey -dname "CN=`*主機名稱* `, OU=`*群組名稱* `, O=`*公司名稱* `,L=`*城市名稱* `, S=`*州* `, C=`國家/地區代碼&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >將`[JAVA_HOME]`取代為安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。 主機名稱是應用程式伺服器的完整網域名稱。

1. 在提示輸入密碼時輸入`keystore_password`。 金鑰存放區的密碼和金鑰必須相同。

   >[!NOTE]
   >
   >在此步驟輸入的`keystore_password` *可能與您在步驟1輸入的密碼(key_password)相同，或可能不同。*

1. 輸入下列其中一個命令，將&#x200B;*keystorename*.keystore複製到`[appserver root]/server/[type]/conf`目錄：

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows Server叢集）復本`keystorename.keystore[appserver root]\domain\configuration`
   * （Linux單一伺服器） `cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux伺服器叢集） `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 鍵入以下命令以匯出憑證檔案：

   * （單一伺服器） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （伺服器叢集） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 提示輸入密碼時，請輸入&#x200B;*keystore_password*。
1. 輸入下列命令，將AEMForms_cert.cer檔案複製到&#x200B;*[appserver root] \conf*&#x200B;目錄：

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows Server叢集） `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux單一伺服器） `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux伺服器叢集） `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 鍵入以下命令以檢視憑證內容：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 若要在`[JAVA_HOME]\jre\lib\security`中提供對cacerts檔案的寫入許可權，請視需要執行下列工作：

   * (Windows)在cacerts檔案上按一下滑鼠右鍵，選取「內容」，然後取消選取「唯讀」屬性。
   * (Linux)型別`chmod 777 cacerts`

1. 輸入下列命令以匯入憑證：

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. 鍵入`changeit`作為密碼。 此密碼是Java安裝的預設密碼，系統管理員可能已變更此密碼。
1. 當系統提示`Trust this certificate? [no]`時，請輸入`yes`。 隨即顯示「憑證已新增至金鑰存放區」確認訊息。
1. 如果您是從Workbench透過SSL連線，請在Workbench電腦上安裝憑證。
1. 在文字編輯器中，開啟下列檔案進行編輯：

   * 單一伺服器 — `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * 伺服器叢集 — `[appserver root]`/domain/configuration/host.xml

   * 伺服器叢集 — `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. &#x200B;
   * **若為單一伺服器，請在lc_&lt;dbaname/tunkey>.xml檔案的&lt;security-realms>區段後面新增下列內容：**

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   找出下列程式碼之後出現的`<server>`區段：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列內容新增至上述程式碼之後出現的&lt;server>區段：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **針對所有節點上的[appserver根目錄]\domain\configuration\host.xml中的伺服器叢集**，在&lt;security-realms>區段後新增下列專案：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在伺服器叢集的主要節點上，在[appserver root]\domain\configuration\domain_&lt;dbname>.xml中，找出下列程式碼之後出現的&lt;server>區段：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列內容新增至上述程式碼之後出現的&lt;server>區段：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 將`keystoreFile`屬性和`keystorePass`屬性的值變更為您在建立金鑰存放區時指定的金鑰存放區密碼。
1. 重新啟動應用程式伺服器：

   * 若為整套安裝：

      * 在Windows「控制檯」中，按一下「管理工具」，然後按一下「服務」。
      * 選取適用於Adobe Experience Manager表單的JBoss。
      * 選取「動作>停止」。
      * 等候服務的狀態顯示為已停止。
      * 選取「動作>開始」。

   * 對於Adobe預先設定或手動設定的JBoss安裝：

      * 從命令提示字元瀏覽至&#x200B;*`[appserver root]`*/bin。
      * 輸入下列命令來停止伺服器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`

      * 等候JBoss處理作業完全關閉（當JBoss處理作業將控制項傳回開始使用的終端機時）。
      * 輸入下列命令啟動伺服器：

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`

1. 若要使用SSL存取管理主控台，請在網頁瀏覽器中輸入`https://[host name]:'port'/adminui`：

   JBoss的預設SSL連線埠為8443。 從此處，存取時指定此連線埠AEM表單。

## 向CA要求認證 {#request-a-credential-from-a-ca}

1. 在命令提示字元中，瀏覽至&#x200B;*[JAVA HOME]*/bin，然後輸入下列命令以建立金鑰庫和金鑰：

   `keytool -genkey -dname "CN=`*主機名稱* `, OU=`*群組名稱* `, O=`*公司名稱* `, L=`*城市名稱* `, S=`*州別* `, C=`*國家代碼*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >將&#x200B;*`[JAVA_HOME]`*&#x200B;取代為安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。

1. 輸入以下命令來產生要傳送給憑證授權單位的憑證要求：

   `keytool -certreq -alias` &quot;AEMForms Cert&quot; `-keystore`*keystorename* `.keystore -file`*AEMFormscertRequest.csr*

1. 當您要求憑證檔案完成時，請完成下一個程式。

## 使用從CA取得的認證來啟用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示字元中，瀏覽至&#x200B;*`[JAVA HOME]`*/bin並輸入下列命令，以匯入已簽署CSR之CA的根憑證：

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   如果根憑證不在瀏覽器中，也請將其匯入。

   >[!NOTE]
   >
   >將&#x200B;*`[JAVA_HOME]`取代為安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。*

1. 在命令提示字元中，瀏覽至&#x200B;*`[JAVA HOME]`*/bin並輸入下列命令，將認證匯入金鑰存放區：

   `keytool -import -trustcacerts -file`*CACertificateName* `.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* 將`[JAVA_HOME]`取代為安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。
   >* 匯入的CA簽署憑證將會取代自我簽署公開憑證（如果存在）。

1. 完成建立SSL認證的步驟13 - 18。
