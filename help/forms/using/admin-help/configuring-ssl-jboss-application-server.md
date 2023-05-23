---
title: 為JBoss應用程式伺服器配置SSL
seo-title: Configuring SSL for JBoss Application Server
description: 瞭解如何為JBoss Application Server配置SSL。
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

# 為JBoss應用程式伺服器配置SSL {#configuring-ssl-for-jboss-application-server}

要在JBoss Application Server上配置SSL，需要SSL憑據進行身份驗證。 可以使用Java鍵工具建立憑據或請求，並從證書頒發機構(CA)導入憑據。 然後，必須在JBoss上啟用SSL。

可以使用包含建立密鑰庫所需的所有資訊的單個命令來運行keytool。

在此過程中：

* `[appserver root]` 是運行表單的應用程式伺服器的AEM主目錄。
* `[type]` 資料夾名稱會因您執行的安裝類型而異。

## 建立SSL憑據 {#create-an-ssl-credential}

1. 在命令提示符下，導航到 *[JAVA首頁]*/bin並鍵入以下命令以建立憑據和密鑰庫：

   `keytool -genkey -dname "CN=`*主機名* `, OU=`*組名稱* `, O=`*公司名稱* `,L=`*城市名稱* `, S=`*州* `, C=`國家/地區代碼」 `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*密鑰密碼* `-keystore`*鍵更名* `.keystore`

   >[!NOTE]
   >
   >替換 `[JAVA_HOME]` 將JDK安裝到的目錄中，並將斜體文本替換為與您的環境對應的值。 主機名是應用程式伺服器的完全限定域名。

1. 輸入 `keystore_password` 提示輸入密碼。 密鑰庫和密鑰的密碼必須相同。

   >[!NOTE]
   >
   >的 `keystore_password` *在此步驟中輸入的口令可能與在步驟1中輸入的口令相同(keypassword)，也可能不同。*

1. 複製 *鍵更名*.keystore到 `[appserver root]/server/[type]/conf` 鍵入以下命令之一：

   * （Windows單伺服器） `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows Server群集）副本 `keystorename.keystore[appserver root]\domain\configuration`
   * （Linux單伺服器） `cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux伺服器群集） `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 鍵入以下命令導出證書檔案：

   * （單伺服器） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （伺服器群集） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. 輸入 *密鑰庫_密碼* 提示輸入密碼。
1. 將AEMForms_cert.cer檔案複製到 *[appserver根] \conf* 命令：

   * （Windows單伺服器） `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows Server群集） `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux單伺服器） `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux伺服器群集） `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 通過鍵入以下命令查看證書的內容：

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. 提供對中的cacerts檔案的寫訪問 `[JAVA_HOME]\jre\lib\security`，如果需要，請執行以下任務：

   * (Windows)按一下右鍵快取檔案並選擇「屬性」，然後取消選擇「只讀」屬性。
   * (Linux)類型 `chmod 777 cacerts`

1. 鍵入以下命令導入證書：

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. 類型 `changeit` 的雙曲餘切值。 此密碼是Java安裝的預設密碼，可能已由系統管理員更改。
1. 提示時 `Trust this certificate? [no]`:，類型 `yes`。 將顯示確認「證書已添加到密鑰庫」。
1. 如果要通過Workbench的SSL連接，請在Workbench電腦上安裝證書。
1. 在文本編輯器中，開啟以下檔案進行編輯：

   * 單伺服器 —  `[appserver root]`/獨立/配置/lc_&lt;dbname turnkey=&quot;&quot;>.xml

   * 伺服器群集 —  `[appserver root]`/domain/configuration/host.xml

   * 伺服器群集 —  `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **對於單台伺服器，** 在lc_&lt;dbaname tunkey=&quot;&quot;>.xml檔案，在 &lt;security-realms> 部分：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   查找 `<server>` 下面的代碼後顯示。

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將以下內容添加到 &lt;server> 上述代碼後的部分：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **對於伺服器群集，** 的 [appserver根]\domain\configuration\host.xml在所有節點上，在 &lt;security-realms> 部分：

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   在伺服器群集的主節點上， [appserver根]\domain\configuration\domain_&lt;dbname>.xml ，找到 &lt;server> 下面的代碼後顯示。

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   將以下內容添加到 &lt;server> 上述代碼後的部分：

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. 更改 `keystoreFile` 屬性和 `keystorePass` 屬於建立密鑰庫時指定的密鑰庫密碼。
1. 重新啟動應用程式伺服器：

   * 對於交鑰匙安裝：

      * 在Windows控制面板中，按一下管理工具，然後按一下服務。
      * 為Adobe Experience Manager表單選擇JBoss。
      * 選擇操作>停止。
      * 等待服務的狀態顯示為已停止。
      * 選擇操作>開始。
   * 對於Adobe預配置或手動配置的JBoss安裝：

      * 從命令提示符導航到 *`[appserver root]`*/bin。
      * 輸入以下命令停止伺服器：

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * 等待JBoss進程完全關閉（當JBoss進程將控制權返回到其在中啟動的終端時）。
      * 輸入以下命令啟動伺服器：

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. 要使用SSL訪問管理控制台，請鍵入 `https://[host name]:'port'/adminui` 在web瀏覽器中：

   JBoss的預設SSL埠為8443。 從此處開始，在訪問表單時指定AEM此埠。

## 從CA請求憑據 {#request-a-credential-from-a-ca}

1. 在命令提示符下，導航到 *[JAVA首頁]*/bin並鍵入以下命令以建立密鑰庫和密鑰：

   `keytool -genkey -dname "CN=`*主機名* `, OU=`*組名稱* `, O=`*公司名稱* `, L=`*城市名稱* `, S=`*州* `, C=`*國家/地區代碼*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*密鑰密碼* `-keystore`*鍵更名* `.keystore`

   >[!NOTE]
   >
   >替換 *`[JAVA_HOME]`* 將JDK安裝到的目錄中，並將斜體文本替換為與您的環境對應的值。

1. 鍵入以下命令以生成要發送到證書頒發機構的證書請求：

   `keytool -certreq -alias` &quot;AEMForms證書&quot; `-keystore`*鍵更名* `.keystore -file`*AEMFormscertRequest.csr*

1. 完成證書檔案請求後，請完成下一步。

## 使用從CA獲取的憑據啟用SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. 在命令提示符下，導航到 *`[JAVA HOME]`*/bin ，然後鍵入以下命令以導入CSR已簽名的CA的根證書：

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   如果根證書不在瀏覽器中，也將其導入。

   >[!NOTE]
   >
   >替換 *`[JAVA_HOME]`將JDK安裝到的目錄中，並將斜體文本替換為與您的環境對應的值。*

1. 在命令提示符下，導航到 *`[JAVA HOME]`*/bin並鍵入以下命令將憑據導入密鑰庫中：

   `keytool -import -trustcacerts -file`*CACertificateName* `.crt -keystore`*鍵更名* `.keystore`

   >[!NOTE]
   >
   >* 替換 `[JAVA_HOME]` 將JDK安裝到的目錄中，並將斜體文本替換為與您的環境對應的值。
   >* 導入的CA簽名證書將替換自簽名的公共證書（如果存在）。


1. 完成「Create a SSL credential（建立SSL憑據）」的步驟13 - 18。
