---
title: 為JBoss應用程式伺服器配置SSL
seo-title: 為JBoss應用程式伺服器配置SSL
description: 瞭解如何為JBoss Application Server配置SSL。
seo-description: 瞭解如何為JBoss Application Server配置SSL。
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 為JBoss應用程式伺服器配置SSL {#configuring-ssl-for-jboss-application-server}

要在JBoss Application server上配置SSL，需要SSL身份驗證憑證。 您可以使用Java鍵工具來建立憑證或要求，並從憑證授權機構(CA)匯入憑證。 然後，您必須在JBoss上啟用SSL。

您可以使用單一命令來執行keytool，該命令包含建立keystore所需的所有資訊。

在此過程中：

* *[appserver root]* 是執行AEM表單之應用程式伺服器的首頁目錄。
* *[type]* 是資料夾名稱，視您執行的安裝類型而定。

## 建立SSL憑證 {#create-an-ssl-credential}

1. 在命令提示符下，導航到 *[JAVA HOME]*/bin ，然後鍵入以下命令以建立憑據和密鑰庫：

   `keytool -genkey -dname "CN=`*主機名&#x200B;*組名`, OU=`*Group名Name* Company Name `, O=`*Company State Name *Company NameChantCountry`,L=`**`, S=`**`, C=`**`" -alias``"``*LC Cert*`**`-keyalg RSA -keypass`**`-keystore`**Code Company DignedChantKeyKeystostoRenamedCyMany`.keystore`

   >[!NOTE]
   >
   >將 [JAVA_HOME] 替換為安裝JDK的目錄，並將斜體文本替換為與您的環境相對應的值。 主機名是應用程式伺服器的完全限定域名。

1. 在提示輸 `keystore_password` 入密碼時輸入。 密鑰庫和密鑰的密碼必須相同。

   >[!NOTE]
   >
   >此步 `keystore_password` 驟中 *輸入的密碼可能與在步驟1中輸入的密碼相同(key_password)，也可能不同。*

1. 鍵入以 *下命令之一，將* keystorename *[.keystore複製到]* appserver root *[/server/]* type/conf目錄：

   * (Windows Single Server) `copy`*keystorename *`.keystore`*[appserver root ]*`\standalone\configuration`
   * (Windows Server Cluster)copy *keystorename*.keystore *[appserver root]*\domain\configuration
   * （Linux單伺服器） `cp`*keystorename *`.keystore`*[appserver root ]*`/standalone/configuration`
   * （Linux伺服器群集）

      ```
      cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration
      ```

1. 鍵入以下命令以導出證書檔案：

   * &quot;（單伺服器）keytool -export -alias &quot;LC Cert&quot; -file LC_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore
   * （伺服器群集）keytool -export -alias *&quot;LC Cert&quot;* -file *LC_cert*.cer -appserver root *[]***/domain/configuration/keystorenameKeystore

1. 在提示輸 *入密碼時輸入keystore_password* 。
1. 鍵入以下命令，將LC_cert.cer檔案復 *[制到appserver root]\conf *directory:

   * (Windows Single Server)copy LC_cert.cer [appserver root]\standalone\configuration
   * （Windows伺服器群集）複製LC_cert.cer [appserver root]\domain\configuration
   * （Linux單伺服器）cp LC _cert.cer [appserver root]\standalone\configuration
   * （Linux伺服器群集）cp LC _cert.cer [appserver root]\domain\configuration

1. 通過鍵入以下命令查看證書的內容：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\LC_cert.cer`
   * 

   ```
   keytool -printcert -v -file [appserver root]\domain\configuration\LC_cert.cer
   ```

   ``

1. 要在 *[JAVA_HOME]*\jre\lib\security中提供對cacerts檔案的寫訪問，請執行以下任務：

   * (Windows)在快取檔案上按一下滑鼠右鍵，然後選取「屬性」，然後取消選取「唯讀」屬性。
   * (Linux)類型 `chmod 777 cacerts`

1. 輸入以下命令以匯入憑證：

   `keytool -import -alias “LC Cert” -file`*LC_cert *`.cer -keystore`*JAVA_HOME*`\jre\lib\security\cacerts`

1. 鍵 `changeit` 入密碼。 此密碼是Java安裝的預設密碼，系統管理員可能已更改此密碼。
1. 當提示輸入 `Trust this certificate? [no]`：時，鍵入 `yes`。 將顯示確認&quot;Certificate was added to keystore&quot;。
1. 如果您要從Workbench透過SSL連線，請在Workbench電腦上安裝憑證。
1. 在文字編輯器中，開啟下列檔案以進行編輯：

   * 單伺服器- [appserver root]/standalone/configuration/lc_&lt;dbname/tunkney>.xml

   * 伺服器群集- [appserver root]/domain/configuration/host.xml

   * 伺服器群集- [appserver root]/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **對於單一伺服器** ，在lc_&lt;dbaname/tunkey>.xml檔案中，在&lt;security-erinds>部分後面添加以下內容：

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="adobe" alias="AEMformsCert" key-password="adobe"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在下列程 `<server>` 式碼後找到顯示的區段：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列內容新增至上述程式碼後面顯示的&lt;server>區段：

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **對於伺服器群集** ，在所有節 [點上的]\domain\configuration\host.xml根目錄中，在&lt;security-erinds>節後添加以下內容：

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="adobe" alias="AEMformsCert" key-password="adobe"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在伺服器群集的主節點上，在 [appserver]root \domain\configuration\domain_&lt;dbname>.xml中，找到下列代碼後面顯示的&lt;server>部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列內容新增至上述程式碼後面顯示的&lt;server>區段：

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 將屬性和屬 `keystoreFile` 性的值更 `keystorePass` 改為建立密鑰庫時指定的密鑰庫密碼。
1. 重新啟動應用程式伺服器：

   * 對於完善的安裝：

      * 在Windows控制面板中，按一下管理工具，然後按一下服務。
      * 選擇「JBoss for Adobe Experience Manager」表單。
      * 選擇「操作」>「停止」。
      * 等待服務狀態顯示為已停止。
      * 選擇「操作」>「開始」。
   * 對於Adobe預先設定或手動設定的JBoss安裝：

      * 在命令提示符下，導航到 *`[appserver root]`*/bin。
      * 輸入以下命令以停止伺服器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * 等到JBoss進程完全關閉（當JBoss進程將控制返回到其中啟動的終端時）。
      * 輸入以下命令啟動伺服器：

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. 若要使用SSL存取管理控制台，請在網 `https://[host name]:[port]/adminui` 頁瀏覽器中輸入：

   JBoss的預設SSL埠為8443。 從這裡開始，在存取AEM表單時指定此連接埠。

## 向CA請求憑證 {#request-a-credential-from-a-ca}

1. 在命令提示符下，導航到 *[JAVA HOME]*/bin ，然後鍵入以下命令以建立密鑰庫和密鑰：

   `keytool -genkey -dname "CN=`*Host Name *Group Name`, OU=`*NameNameNameNameCompanyName* NameCompanyState `, O=`*NameCity *`, L=`**`, S=`**`, C=`**`" -alias``"``*LC Cert*`**`-keyalg RSA -keypass`**`-keystore`** Conturity Code Company Company ChangDignetOrignHyDPagngnPDOryPamedC `.keystore`

   >[!NOTE]
   >
   >以安 *`[JAVA_HOME]`裝JDK的目錄取代，並以與您的環境對應的值取代斜體文字。*

1. 鍵入以下命令以生成要發送到證書頒發機構的證書請求：

   `keytool -certreq -alias`*&quot;LC Cert&quot;*keystorename`-keystore`**`.keystore -file`*LCcertRequest.csr *

1. 當您的憑證檔案要求完成時，請完成下一個程式。

## 使用從CA取得的憑證啟用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示符下，導航到 *`[JAVA HOME]`*/bin ，然後鍵入以下命令以導入已與CSR簽名的CA的根證書：

   `keytool -import -trustcacerts -file`*rootcert *`.pem -keystore`*keystorename*`.keystore -alias root`

   如果根證書不在瀏覽器中，也可將其導入。

   >[!NOTE]
   >
   >以安 *`[JAVA_HOME]`裝JDK的目錄取代，並以與您的環境對應的值取代斜體文字。*

1. 在命令提示符下，導航到 *`[JAVA HOME]`*/bin ，然後鍵入以下命令將憑據導入密鑰庫：

   `keytool -import -trustcacerts -file`*CACertificateName *`.crt -keystore`*keystorename*`.keystore`

   >[!NOTE]
   >
   >* 以安 `[JAVA_HOME]` 裝JDK的目錄取代，並以與您的環境對應的值取代斜體文字。
   >* 導入的CA簽名證書將替換自簽名的公共證書（如果存在）。


1. 完成「Create an SSL credential（建立SSL憑證）」的步驟13 - 18。
