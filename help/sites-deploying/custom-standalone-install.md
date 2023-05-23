---
title: 自定義獨立安裝
seo-title: Custom Standalone Install
description: 瞭解安裝獨立實例時可用的AEM選項。
seo-description: Learn about the options available when installing a standalone AEM instance.
content-type: reference
topic-tags: deploying
exl-id: d6484bb7-8123-4f42-96e8-aa441b1093f3
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 0%

---

# 自定義獨立安裝{#custom-standalone-install}

本節介紹安裝獨立實例時可用AEM的選項。 您也可以閱讀 [儲存元素](/help/sites-deploying/storage-elements-in-aem-6.md) 有關在新安裝6後選擇後端儲存類型的詳細AEM資訊。

## 通過更名檔案更改埠號 {#changing-the-port-number-by-renaming-the-file}

預設端AEM口為4502。 如果該埠不可用或已在使用中，Quickstart會自動配置自己使用第一個可用的埠號，如下所示：4502、8080、8081、8082、8083、8084、8085、8888、9362、 `<*random*>`。

也可以通過更名快速啟動jar檔案來設定埠號，以便檔案名包括埠號；比如說， `cq5-publish-p4503.jar` 或 `cq5-author-p6754.jar`。

更名快速啟動jar檔案時要遵循多種規則：

* 更名檔案時，必須以 `cq;` 在 `cq5-publish-p4503.jar`。

* 建議您 *總是* 在埠號前加上 — p;如cq5-publish-p4503.jar或cq5-author-p6754.jar中所示。

>[!NOTE]
>
>這是為了確保您無需擔心是否滿足用於提取埠號的規則：
>
>* 埠號必須為4位或5位
>* 這些數字必須在短划線後
>* 如果檔案名中有其他數字，則必須在埠號前加上 `-p`
>* 忽略檔案名開頭的&quot;cq5&quot;前置詞
>


>[!NOTE]
>
>您還可以使用 `-port` 的子菜單。

### Java 11注意事項 {#java-considerations}

如果您正在運行OracleJava 11（或Java的通常版本高於8），則啟動時需要將其他開關添加到命令行AEM。

* 以下內容 —  `-add-opens` 需要添加交換機，以防止相關反射訪問中的警告消息 `stdout.log`

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* 另外，您需要 `-XX:+UseParallelGC` 切換以緩解任何潛在的效能問題。

以下是在Java 11上啟動時，其他JVM參數的樣例AEM:

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

最後，如果運行的實例是從AEM6.3升級的，請確保以下屬性設定為 **真** 在 `sling.properties`:

* `felix.bootdelegation.implicit`

## 執行模式 {#run-modes}

**運行模式** 允許您針對特定目AEM的調整實例；例如，作者或發佈、test、開發、內部網等。 這些模式還允許您控制示例內容的使用。 此示例內容是在構建快速入門之前定義的，可包括包、配置等。 當您希望保持安裝精簡且沒有示例內容時，這對於生產就緒型安裝尤其有用。 有關詳細資訊，請參閱：

* [執行模式](/help/sites-deploying/configure-runmodes.md)

## 添加檔案安裝提供程式 {#adding-a-file-install-provider}

預設情況下，資料夾 `crx-quickstart/install` 監視檔案。
此資料夾不存在，但只需在運行時建立即可。

如果將包、配置或內容包放入此目錄，則系統會自動獲取並安裝它。 如果刪除，則卸載。
這是將捆綁包、內容包或配置放到儲存庫的另一種方法。

這對於以下幾個使用情形特別有趣：

* 在開發過程中，將某些內容放入檔案系統可能會更容易。
* 如果出現問題，則無法訪問Web控制台和儲存庫。 通過此操作，您可以將其他捆綁包放入此目錄，並且應安裝這些捆綁包。
* 的 `crx-quickstart/install` 可以在啟動快速啟動之前建立資料夾，還可以將其他包放在那裡。

>[!NOTE]
>
>另請參閱 [如何在伺服器啟動時自動安裝CRX包](https://helpx.adobe.com/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html) 的上界。

## 將Adobe Experience Manager安裝和啟動為Windows服務 {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>請確保在以管理員身份登錄時執行以下步驟，或使用 **以管理員身份運行** 上下文菜單選擇。
>
>以具有管理員權限的用戶身份登錄 **不足**。 如果在完成這些步驟時您未以管理員身份登錄 **拒絕訪問** 錯誤。

要安裝並作為WindowsAEM服務啟動，請執行以下操作：

1. 在文本編輯器中開啟crx-quickstart\opt\helpers\instsrv.bat檔案。
1. 如果要配置64位Windows伺服器，請根據您的作業系統，使用以下命令之一替換prunsrv的所有實例：

   * prunsrv_amd64
   * prunsrv_ia64

   此命令調用適當的指令碼，該指令碼在64位Java中啟動Windows服務守護程式，而不是在32位Java中啟動。

1. 要防止進程進入多個進程，請增加PermGen JVM參數。 查找 `set jvm_options` 命令，並按如下方式設定值：

   `set jvm_options=-Xmx1792m`

1. 開啟命令提示符，將當前目錄更改為安裝的crx-quickstart/opt/helpers文AEM件夾，然後輸入以下命令以建立服務：

   `instsrv.bat cq5`

   要驗證是否已建立服務，請在「管理工具」控制面板中開啟「服務」或鍵入 `start services.msc` 命令提示符下。 cq5服務將出現在清單中。

1. 通過執行以下操作之一啟動服務：

   * 在「服務」控制面板中，按一下cq5 ，然後按一下「開始」。

   ![chlimage_1-11](assets/chlimage_1-11.png)

   * 在命令行中，鍵入net start cq5。

   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows表示服務正在運行。 啟AEM動並在任務管理器中顯示prunsrv執行檔。 在Web瀏覽器中，導AEM航到，例如， `https://localhost:4502` 開始使AEM用。

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>建立Windows服務時，將使用inssrv.bat檔案中的屬性值。 如果在instsrv.bat中編輯屬性值，則必須卸載並重新安裝服務。

>[!NOTE]
>
>作為服AEM務安裝時，必須提供中日誌目錄的絕對路徑 `com.adobe.xmp.worker.files.ncomm.XMPFilesNComm` 從Configuration Manager中。

要卸載服務，請按一下 **停止** 的 **服務** 控制項面板或命令行中，導航到資料夾並鍵入 `instsrv.bat -uninstall cq5`。 服務從 **服務** 鍵入時從命令行的清單中 `net start`。

## 重新定義臨時工作目錄的位置 {#redefining-the-location-of-the-temporary-work-directory}

Java電腦的臨時資料夾的預設位置是 `/tmp`。 也AEM使用此資料夾，例如在生成包時。

如果要更改臨時資料夾的位置（例如，如果需要具有更多可用空間的目錄），則定義* `<new-tmp-path>`*通過添加JVM參數：

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

至以下任一：

* 伺服器啟動命令行
* serverctl或啟動指令碼中的CQ_JVM_OPTS環境參數

## Quickstart檔案中提供的其他選項 {#further-options-available-from-the-quickstart-file}

Quickstart幫助檔案中介紹了更多選項和更名約定，該幫助檔案可通過 — help選項提供。 要訪問幫助，請鍵入：

* `java -jar cq-quickstart-6.5.0.jar -help`

>[!CAUTION]
>
>這些選項自6.5(6.5.0.0)AEM的原始版本起生效。 以後的SP版本可能會發生更改。

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/cq-quickstart-6.5.0.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20190328)                            
--------------------------------------------------------------------------------
Usage:                                                                          
 Use these options on the Quickstart command line.                              
--------------------------------------------------------------------------------

-help (--help,-h)
         Show this help message                                                 
-quickstart.server.port (-p,-port) <port>
         Set server port number                                                 
-contextpath (-c,-org.apache.felix.http.context_path) <contextpath>
         Set context path                                                       
-debug <port>
         Enable Java Debugging on port number; forces forking                   
-gui 
         Show GUI if running on a terminal                                      
-nobrowser (-quickstart.nobrowser)
         Do not open browser at startup                                         
-unpack
         Unpack installation files only, do not start the server (implies       
         -verbose)                                                              
-v (-verbose)
         Do not redirect stdout/stderr to files and do not close stdin          
-nofork
         Do not fork the JVM, even if not running on a console                  
-fork
         Force forking the JVM if running on a console, using recommended       
         default memory settings for the forked JVM.                            
-forkargs <args> [<args> ...]
         Additional arguments for the forked JVM, defaults to '-Xmx1024m        
         -XX:MaxPermSize=256m '.  Use -- to specify values starting with -,     
         example: '-forkargs -- -server'                                        
-a (--interface) <interface>
         Optional IP address (interface) to bind to                             
-pt <string>
         Process type (main/fork) - do not use directly, used when forking a    
         process                                                                
-r <string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string>]]]]]]]]]
         Runmode(s) - Use this to define the run mode(s)                        
-b <string>
         Base folder - defines the path under which the quickstart work folder  
         is created                                                             
-low-mem-action <string>
         Low memory action - what to do if memory is insufficient at startup    
-use-control-port
         Start a control port                                                   
-nointeractive
         Start with no interactivity                                            
-ll <level>
         Define launchpad log level (1 = error...4 = debug)                     
-n   
         Do not install shutdown hook                                           
-D<property>=<value>
         Additional framework properties.                                       
-listener-port <listener-port>
         Set listener port number                                               
-x <string>
         Run a Quickstart extension.                                            
  Options for executing Quickstart extensions:
                                                                                
    -xargs <arg> [<arg> ...]
         Construct an arguments list for a Quickstart extension (e.g. -xargs -- 
         -arg1 val1 -arg2 val2).                                                
--------------------------------------------------------------------------------
Quickstart filename options                                                     
--------------------------------------------------------------------------------
Usage:                                                                          
 Rename the jar file, including one of the patterns shown below, to set the     
corresponding option. Command-line options have priority on these filename      
patterns.                                                                       
--------------------------------------------------------------------------------

-NNNN
         Include -NNNN.jar or -pNNNN in the renamed jar filename to run on port 
         NNNN, for example: quickstart-8085.jar                                 
-nobrowser
         Include -nobrowser in the renamed jar filename to avoid opening the    
         browser at startup, example: quickstart-nobrowser-8085.jar             
-publish
         Include -publish in the renamed jar filename to run in "publish" mode, 
         example: cq-publish-7502.jar                                           
-dynamicmedia
         Include -dynamicmedia in the renamed jar filename to run in            
         "dynamicmedia" mode, example: quickstart-dynamicmedia-4502.jar         
-dynamicmedia_scene7
         Include -dynamicmedia_scene7 in the renamed jar filename to run in     
         "dynamicmedia_scene7" mode, example:                                   
         quickstart-dynamicmedia_scene7-p4502.jar                               
--------------------------------------------------------------------------------
The license.properties file
--------------------------------------------------------------------------------
  The license.properties file stores licensing information, created from the    
  licensing form displayed on first startup and stored in the folder from where 
  Quickstart is run.                                                            
--------------------------------------------------------------------------------
Log files
--------------------------------------------------------------------------------
  Once Quickstart has been unpacked and started, log files can be found under   
  /Users/aemdocs/CQInstallationKits/AEM-65150-L8/crx-quickstart/logs.           
--------------------------------------------------------------------------------
```

## 在AEMAmazonEC2環境中安裝 {#installing-aem-in-the-amazon-ec-environment}

在AmazonAEM彈性計算雲(EC2)實例上安裝時，如果同時在EC2實例上安裝作者和發佈，則按照上的步驟正確安裝了作者實例 [安裝Manager實AEM例](#installinginstancesofaemmanager);但是，「發佈」實例將變為「作者」。

在EC2環境上安裝發佈實例之前，請執行以下操作：

1. 在首次啟動實例之前，先解壓縮Publish實例的jar檔案。 要解壓縮檔案，請使用以下命令：

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >如果更改模式 **後** 首次啟動實例時，無法更改運行模式。

1. 通過運行以下程式啟動實例：

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >請確保在解壓縮實例後，首先運行上面的命令。 否則，將不生成quickstart.properties填充。 如果沒有此檔案，任何未AEM來升級都將失敗。

1. 在 **賓** 資料夾，開啟 **開始** 指令碼並檢查以下部分：

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. 將運行模式更改為 **發佈** 並保存檔案。

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. 停止實例並通過運行 **開始** 的下界。

## 驗證安裝 {#verifying-the-installation}

以下連結可用於驗證您的安裝是否可操作（所有示例都基於實例在localhost的埠8080上運行，CRX在/crx和/下的Launchpad下安裝）:

* `https://localhost:8080/crx/de`
CRXDE Lite控制台。

* `https://localhost:8080/system/console`
Web控制台。

## 安裝後的操作 {#actions-after-installation}

雖然配置WCM有很多可能AEM性，但應執行某些操作，或至少在安裝後立即進行檢查：

* 咨詢 [安全核對表](/help/sites-administering/security-checklist.md) 確保系統保持安全所需的任務。
* 查看隨WCM一起安裝的預設用戶和組AEM清單。 檢查是否要對任何其他帳戶執行操作 — 請參閱 [安全性和用戶管理](/help/sites-administering/security.md) 的上界。

## 訪問CRXDE Lite和Web控制台 {#accessing-crxde-lite-and-the-web-console}

啟AEM動WCM後，您還可以訪問：

* [CRXDE Lite](#accessing-crxde-lite)  — 用於訪問和管理儲存庫
* [Web控制台](#accessing-the-web-console)  — 用於管理或配置OSGi捆綁包（也稱為OSGi控制台）

### 訪問CRXDE Lite {#accessing-crxde-lite}

要開啟CRXDE Lite，可以選擇 **CRXDE Lite** 從歡迎螢幕或使用瀏覽器導航到

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

例如：
`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### 訪問Web控制台 {#accessing-the-web-console}

要訪問Adobe CQWeb控制台，可以選擇 **OSGi控制台** 從歡迎螢幕或使用瀏覽器導航到

```
 https://<host>:<port>/system/console
```

例如：
`https://localhost:4502/system/console`
或「捆綁」頁
`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

請參閱 [OSGi與Web控制台的配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 的上界。

## 疑難排解 {#troubleshooting}

有關處理安裝過程中可能出現的問題的資訊，請參閱：

* [疑難排解](/help/sites-deploying/troubleshooting.md)

## 卸載Adobe Experience Manager {#uninstalling-adobe-experience-manager}

因AEM為安裝到單個目錄中，所以不需要卸載實用程式。 卸載可以與刪除整個安裝目錄一樣簡單，AEM但卸載方式取決於要實現的內容和使用的持久性儲存。

如果永久儲存嵌入到安裝目錄中，例如，在預設的TarPM安裝中，刪除資料夾也會刪除資料。

>[!NOTE]
>
>Adobe強烈建議您在刪除之前備份儲存AEM庫。 如果刪除整個 &lt;cq-installation-directory>，將刪除儲存庫。 在刪除、移動或複製儲存庫資料之前保留 &lt;cq-installation-directory>在刪除其他資料夾之前，在其他位置使用/crx-quickstart/repository資料夾。

如果安裝時AEM使用外部儲存，則刪除資料夾不會自動刪除資料，而是會刪除儲存配置，這會使恢復JCR內容變得困難。
