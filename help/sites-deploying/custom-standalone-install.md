---
title: 自定義獨立安裝
seo-title: 自定義獨立安裝
description: 了解安裝獨立AEM執行個體時可用的選項。
seo-description: 了解安裝獨立AEM執行個體時可用的選項。
uuid: 83fc49d8-2c44-4bb2-988a-f29475066efc
contentOwner: Tyler Rushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: deae8ecb-a2ee-4442-97ca-98bfd1b85738
docset: aem65
exl-id: d6484bb7-8123-4f42-96e8-aa441b1093f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# 自定義獨立安裝{#custom-standalone-install}

本節說明安裝獨立AEM執行個體時可用的選項。 您也可以閱讀[儲存元素](/help/sites-deploying/storage-elements-in-aem-6.md) ，以取得在新安裝AEM 6後選擇後端儲存類型的詳細資訊。

## 通過更名檔案{#changing-the-port-number-by-renaming-the-file}更改埠號

AEM的預設埠為4502。 如果該埠不可用或已在使用中，Quickstart會自動配置自身以使用第一個可用埠號，如下所示：4502、8080、8081、8082、8083、8084、8085、8888、9362、`<*random*>`。

您也可以通過更名quickstart jar檔案來設定埠號，以便檔案名包括埠號；例如， `cq5-publish-p4503.jar`或`cq5-author-p6754.jar`。

更名quickstart jar檔案時，應遵循各種規則：

* 重新命名檔案時，其開頭必須為`cq;`，如`cq5-publish-p4503.jar`中。

* 建議您&#x200B;*always*&#x200B;為埠號加上前置詞 — p;如cq5-publish-p4503.jar或cq5-author-p6754.jar中。

>[!NOTE]
>
>這是為了確保您無需擔心完全填寫用於提取埠號的規則：
>
>* 埠號必須為4位或5位
>* 這些數字必須在破折號後
>* 如果檔案名中有其他位數，則埠號必須帶有前置詞`-p`
>* 檔案名稱開頭的&quot;cq5&quot;前置詞會遭忽略

>



>[!NOTE]
>
>您也可以使用start命令中的`-port`選項更改埠號。

### Java 11考量事項{#java-considerations}

如果您正在運行OracleJava 11（或通常8以上的Java版本），則啟動AEM時，需要將其他開關添加到命令行中。

* 需要添加以下 — `-add-opens`交換機，以防止`stdout.log`中出現相關的反射訪問警告消息

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* 此外，您需要使用`-XX:+UseParallelGC`交換機，以緩解任何潛在的效能問題。

以下是在Java 11上啟動AEM時，其他JVM參數的樣本：

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

最後，如果您執行的是從AEM 6.3升級的執行個體，請確定`sling.properties`下的下列屬性已設為&#x200B;**true**:

* `felix.bootdelegation.implicit`

## 執行模式 {#run-modes}

**執** 行模式，根據特定用途調整AEM執行個體；例如，製作或發佈、測試、開發、內部網路等。這些模式也可讓您控制範例內容的使用。 此示例內容在構建快速入門之前定義，可以包括包、配置等。 如果您想要保持安裝精簡，且不含範例內容，此功能對於生產就緒型安裝特別有用。 如需詳細資訊，請參閱：

* [執行模式](/help/sites-deploying/configure-runmodes.md)

## 添加檔案安裝提供程式{#adding-a-file-install-provider}

預設情況下，會監視檔案的資料夾`crx-quickstart/install`。
此資料夾不存在，但只需在執行階段建立即可。

如果將包、配置或內容包放入此目錄中，則會自動拾取並安裝該包。 如果移除，則會解除安裝。
這是將套件組合、內容套件或設定放入存放庫的另一種方式。

這在幾個使用案例中特別有趣：

* 在開發期間，將某些內容放入檔案系統可能會比較容易。
* 如果發生錯誤，則無法存取Web主控台和存放庫。 通過此操作，您可以將其他套件組合放入此目錄中，並應安裝這些套件組合。
* 在快速入門之前可以建立`crx-quickstart/install`資料夾，並可將其他包放在那裡。

>[!NOTE]
>
>如需範例，請參閱[如何在伺服器啟動時自動安裝CRX套件](https://helpx.adobe.com/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html) 。

## 安裝和啟動Adobe Experience Manager as a Windows Service {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>請務必在以管理員身份登錄時執行以下過程，或使用&#x200B;**以管理員身份運行**&#x200B;上下文菜單選擇開始/運行這些步驟。
>
>以具有管理員權限的用戶身份登錄的是&#x200B;**indequited**。 如果完成這些步驟時未以管理員身份登錄，則會收到&#x200B;**拒絕訪問**&#x200B;錯誤。

若要安裝AEM as a Windows服務並啟動：

1. 在文字編輯器中開啟crx-quickstart\opt\helpers\instsrv.bat檔案。
1. 如果要配置64位Windows伺服器，請根據您的作業系統，用以下命令之一替換prunsrv的所有實例：

   * prunsrv_amd64
   * prunsrv_ia64

   此命令調用適當的指令碼，該指令碼以64位Java（而非32位Java）啟動Windows服務守護程式。

1. 要防止進程跳入多個進程，請增加最大堆大小和PermGen JVM參數。 找到`set jvm_options`命令，然後按如下方式設定值：

   `set jvm_options=-XX:MaxPermSize=256M;-Xmx1792m`

1. 開啟命令提示字元，將當前目錄更改為AEM安裝的crx-quickstart/opt/helpers資料夾，然後輸入以下命令以建立服務：

   `instsrv.bat cq5`

   要驗證是否已建立服務，請開啟「管理工具」控制面板中的「服務」，或在命令提示符中鍵入`start services.msc`。 cq5服務會出現在清單中。

1. 執行下列任一操作以啟動服務：

   * 在「服務」控制面板中，按一下cq5，然後按一下「開始」。

   ![chlimage_1-11](assets/chlimage_1-11.png)

   * 在命令行中，鍵入net start cq5。

   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows表示服務正在運行。 AEM啟動，並且prunsrv執行檔出現在任務管理器中。 在網頁瀏覽器中，導覽至AEM，例如`https://localhost:4502`以開始使用AEM。

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>建立Windows服務時，將使用instsrv.bat檔案中的屬性值。 如果在instsrv.bat中編輯屬性值，則必須卸載，然後重新安裝服務。

>[!NOTE]
>
>安裝AEM as服務時，必須從Configuration Manager為`com.adobe.xmp.worker.files.ncomm.XMPFilesNComm`中的日誌目錄提供絕對路徑。

要卸載服務，請按一下&#x200B;**Services**&#x200B;控制面板或命令行中的&#x200B;**Stop**，導航到資料夾並鍵入`instsrv.bat -uninstall cq5`。 鍵入`net start`時，該服務將從&#x200B;**服務**&#x200B;控制面板的清單或命令行的清單中刪除。

## 重新定義臨時工作目錄{#redefining-the-location-of-the-temporary-work-directory}的位置

Java電腦的臨時資料夾的預設位置為`/tmp`。 AEM也會使用此資料夾，例如在建立套件時。

如果要更改臨時資料夾的位置（例如，如果需要具有更多可用空間的目錄），請通過添加JVM參數來定義* `<new-tmp-path>`*:

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

至以下任一項：

* 伺服器啟動命令行
* serverctl或啟動指令碼中的CQ_JVM_OPTS環境參數

## 快速入門檔案{#further-options-available-from-the-quickstart-file}中提供的其他選項

快速入門幫助檔案中介紹了更多選項和更名約定，該檔案可通過 — help選項獲得。 若要存取說明，請輸入：

* `java -jar cq5-<*version*>.jar -help`

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/cq-quickstart-5.6.0.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20130129)
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
-ll <level>
         Define launchpad log level (1 = error...4 = debug)
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
         Include -publish in the renamed jar filename to run cq5 in "publish"
         mode, example: cq5-publish-7502.jar
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
  ./crx-quickstart/logs.
--------------------------------------------------------------------------------
```

## 在Amazon EC2環境{#installing-aem-in-the-amazon-ec-environment}中安裝AEM

在Amazon Elastic Compute Cloud(EC2)實例上安裝AEM時，如果在EC2實例上同時安裝作者和發佈，則按照[安裝AEM Manager](#installinginstancesofaemmanager)實例上的過程，可以正確安裝作者實例；不過，Publish例項會變成「作者」。

在EC2環境上安裝發佈實例之前，請執行以下操作：

1. 首次啟動執行個體之前，先解壓縮Publish執行個體的jar檔案。 要解壓縮檔案，請使用以下命令：

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >如果您在第一次啟動執行個體後變更&#x200B;**模式，則無法變更執行模式。**

1. 執行以啟動執行個體：

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >請務必在解壓縮執行個體後，先執行上述命令，以便執行執行個體。 否則，將不會生成quickstart.properties填充。 若沒有此檔案，任何日後的AEM升級都將失敗。

1. 在&#x200B;**bin**&#x200B;資料夾中，開啟&#x200B;**start**&#x200B;指令碼並檢查以下部分：

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. 將執行模式變更為&#x200B;**publish**&#x200B;並儲存檔案。

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. 停止執行個體，並執行&#x200B;**start**&#x200B;指令碼以重新啟動。

## 驗證安裝{#verifying-the-installation}

以下連結可用來驗證您的安裝是否可運作（所有範例都以執行個體在localhost的連接埠8080上執行，以及CRX安裝在/crx下，而Launchpad安裝在/下）為基礎：

* `https://localhost:8080/crx/de`
CRXDE Lite主控台。

* `https://localhost:8080/system/console`
Web控制台。

## 安裝後的操作{#actions-after-installation}

雖然設定AEM WCM有許多可能，但您應採取某些動作，或至少在安裝後立即檢閱：

* 請參閱[安全檢查清單](/help/sites-administering/security-checklist.md)以了解確保系統安全所需的任務。
* 查看隨AEM WCM安裝的預設用戶和組清單。 檢查您是否要對任何其他帳戶採取操作 — 有關詳細資訊，請參閱[安全和用戶管理](/help/sites-administering/security.md)。

## 訪問CRXDE Lite和Web控制台{#accessing-crxde-lite-and-the-web-console}

AEM WCM啟動後，您也可以存取：

* [CRXDE Lite](#accessing-crxde-lite)  — 用於存取和管理存放庫
* [Web主控台](#accessing-the-web-console)  — 用於管理或配置OSGi套件組合（也稱為OSGi主控台）

### 訪問CRXDE Lite{#accessing-crxde-lite}

若要開啟CRXDE Lite，您可以從歡迎畫面選取&#x200B;**CRXDE Lite**，或使用瀏覽器導覽至

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

例如：`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### 訪問Web控制台{#accessing-the-web-console}

若要存取Adobe CQ Web主控台，您可以從歡迎畫面中選取&#x200B;**OSGi主控台**，或使用瀏覽器導覽至

```
 https://<host>:<port>/system/console
```

例如：
`https://localhost:4502/system/console`
或「套件組合」頁面
`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

如需詳細資訊，請參閱[使用Web控制台進行OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 。

## 疑難排解 {#troubleshooting}

有關處理安裝過程中可能出現的問題的資訊，請參閱：

* [疑難排解](/help/sites-deploying/troubleshooting.md)

## 解除安裝Adobe Experience Manager {#uninstalling-adobe-experience-manager}

由於AEM會安裝至單一目錄，因此不需要解除安裝公用程式。 卸載過程可能與刪除整個安裝目錄一樣簡單，不過卸載AEM的方式取決於您要實現什麼，以及您使用什麼持久儲存。

如果永久儲存嵌入安裝目錄（例如，在預設的TarPM安裝中），則刪除資料夾也會刪除資料。

>[!NOTE]
>
>Adobe強烈建議您先備份儲存庫再刪除AEM。 如果刪除整個&lt;cq-installation-directory>，則會刪除儲存庫。 若要在刪除前保留存放庫資料，請先將&lt;cq-installation-directory>/crx-quickstart/repository資料夾移動或複製到其他位置，然後再刪除其他資料夾。

如果安裝AEM時使用外部儲存（例如資料庫伺服器），則刪除資料夾不會自動刪除資料，但會刪除儲存配置，這會使JCR內容的還原變得困難。
