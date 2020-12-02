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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# 為JBoss應用程式伺服器配置SSL {#configuring-ssl-for-jboss-application-server}

要在JBoss Application Server上配置SSL，需要SSL身份驗證憑證。 您可以使用Java鍵工具來建立憑證或要求，並從憑證授權機構(CA)匯入憑證。 然後，您必須在JBoss上啟用SSL。

您可以使用單一命令來執行keytool，該命令包含建立keystore所需的所有資訊。

在此過程中：

* `[appserver root]` 是執行AEM表單之應用程式伺服器的首頁目錄。
* `[type]` 是根據您執行的安裝類型而有所不同的資料夾名稱。

## 建立SSL憑證{#create-an-ssl-credential}

1. 在命令提示符下，導航至&#x200B;*[JAVA HOME]*/bin ，然後鍵入以下命令以建立憑據和密鑰庫：

   `keytool -genkey -dname "CN=`*主機* `, OU=`*名稱群* `, O=`*組名稱公司* `,L=`*名稱城市名* `, S=`** `, C=`稱狀態國 `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*家代碼&quot; key_* `-keystore`*passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >將`[JAVA_HOME]`替換為安裝JDK的目錄，並將斜體文本替換為與您的環境對應的值。 主機名是應用程式伺服器的完全限定域名。

1. 在提示輸入密碼時輸入`keystore_password`。 密鑰庫和密鑰的密碼必須相同。

   >[!NOTE]
   >
   >此步驟中輸入的`keystore_password` *可能與在步驟1中輸入的密碼(key_password)相同，也可能不同。*

1. 鍵入以下命令之一，將&#x200B;*keystorename*.keystore複製到`[appserver root]/server/[type]/conf`目錄：

   * （Windows單伺服器）`copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows伺服器群集）複製`keystorename.keystore[appserver root]\domain\configuration`
   * （Linux單伺服器）`cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux伺服器群集）`cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 鍵入以下命令以導出證書檔案：

   * （單伺服器）`keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （伺服器群集）`keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 當提示輸入密碼時，輸入&#x200B;*keystore_password*。
1. 鍵入以下命令，將AEMForms_cert.cer檔案複製到&#x200B;*[appserver root] \conf*&#x200B;目錄：

   * （Windows單伺服器）`copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows伺服器群集）`copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux單伺服器）`cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux伺服器群集）`cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 通過鍵入以下命令查看證書的內容：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 要提供對`[JAVA_HOME]\jre\lib\security`中cacerts檔案的寫訪問（如果需要），請執行以下任務：

   * (Windows)在快取檔案上按一下滑鼠右鍵，然後選取「屬性」，然後取消選取「唯讀」屬性。
   * (Linux)類型`chmod 777 cacerts`

1. 輸入以下命令以匯入憑證：

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_* `.cer -keystore`*certJAVA_HOME* `\jre\lib\security\cacerts`

1. 鍵入`changeit`作為口令。 此密碼是Java安裝的預設密碼，系統管理員可能已更改此密碼。
1. 當提示輸入`Trust this certificate? [no]`：時，鍵入`yes`。 將顯示確認&quot;Certificate was added to keystore&quot;。
1. 如果您要從Workbench透過SSL連線，請在Workbench電腦上安裝憑證。
1. 在文字編輯器中，開啟下列檔案以進行編輯：

   * 單伺服器- `[appserver root]`/standalone/configuration/lc_&lt;dbname/tunklypky>.xml

   * 伺服器群集- `[appserver root]`/domain/configuration/host.xml

   * 伺服器群集- `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **對於單個服** 務器，在lc_&lt;dbaname>.xml檔案中，添加以下 &lt;security-realms> 部分：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在下列程式碼後找到`<server>`區段：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列內容新增至上述程式碼後面顯示的&lt;server>區段：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **對於伺服器群** 集，在 [appserver ]root \domain\configuration\host.xml中，在所有節點上添加以下 &lt;security-realms> after節：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在伺服器群集的主節點上，在[appserver root]\domain\configuration\domain_&lt;dbname>.xml中，找到以下代碼後面顯示的&lt;server>部分：

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將下列內容新增至上述程式碼後面顯示的&lt;server>區段：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 將`keystoreFile`屬性和`keystorePass`屬性的值更改為建立密鑰庫時指定的密鑰庫密碼。
1. 重新啟動應用程式伺服器：

   * 對於完善的安裝：

      * 在Windows控制面板中，按一下管理工具，然後按一下服務。
      * 選擇「JBoss for Adobe Experience Manager」表單。
      * 選擇「操作」>「停止」。
      * 等待服務狀態顯示為已停止。
      * 選擇「操作」>「開始」。
   * 對於Adobe預先設定或手動設定的JBoss安裝：

      * 在命令提示符下，導航至&#x200B;*`[appserver root]`*/bin。
      * 輸入以下命令以停止伺服器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * 等到JBoss進程完全關閉（當JBoss進程將控制返回到其中啟動的終端時）。
      * 輸入以下命令啟動伺服器：

         * (Windows)`run.bat -c <profile>`
         * (Linux)`./run.sh -c <profile>`



1. 若要使用SSL存取管理控制台，請在網頁瀏覽器中輸入`https://[host name]:'port'/adminui`:

   JBoss的預設SSL埠為8443。 從這裡開始，在存取AEM表單時指定此連接埠。

## 向CA {#request-a-credential-from-a-ca}請求憑據

1. 在命令提示符下，導航至&#x200B;*[JAVA HOME]*/bin ，然後鍵入以下命令以建立密鑰庫和密鑰：

   `keytool -genkey -dname "CN=`*Host* `, OU=`*NameGroup* `, O=`*Company* `, L=`*NameCity* `, S=`** `, C=`*NameStateCountry Code*&quot;- `-alias "AEMForms Cert"` `-keyalg RSA -keypass`key_** `-keystore`*passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >將&#x200B;*`[JAVA_HOME]`*&#x200B;替換為安裝JDK的目錄，並將斜體文本替換為與您的環境對應的值。

1. 鍵入以下命令以生成要發送到證書頒發機構的證書請求：

   `keytool -certreq -alias` &quot;AEMForms Cert&quot;  `-keystore`** `.keystore -file`*keystorenameAEMFormscertRequest.csr*

1. 當您的憑證檔案要求完成時，請完成下一個程式。

## 使用從CA獲取的憑據啟用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示符下，導航到&#x200B;*`[JAVA HOME]`*/bin ，然後鍵入以下命令以導入已與CSR簽署的CA的根證書：

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   如果根證書不在瀏覽器中，也可將其導入。

   >[!NOTE]
   >
   >將&#x200B;*`[JAVA_HOME]`替換為安裝JDK的目錄，並將斜體文本替換為與您的環境對應的值。*

1. 在命令提示符下，導航至&#x200B;*`[JAVA HOME]`*/bin ，然後鍵入以下命令將憑據導入密鑰庫：

   `keytool -import -trustcacerts -file`*CACertificateNamekeystorename* `.crt -keystore`** `.keystore`

   >[!NOTE]
   >
   >* 將`[JAVA_HOME]`替換為安裝JDK的目錄，並將斜體文本替換為與您的環境對應的值。
   >* 導入的CA簽名證書將替換自簽名的公共證書（如果存在）。


1. 完成「Create an SSL credential（建立SSL憑證）」的步驟13 - 18。
