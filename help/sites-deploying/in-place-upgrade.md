---
title: 執行就地升級
description: 瞭解如何執行AEM 6.5的就地升級。
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 0%

---

# 執行就地升級{#performing-an-in-place-upgrade}

>[!NOTE]
>
>本頁面概述AEM 6.5的升級程式。如果安裝已部署到應用程式伺服器，請參閱[應用程式伺服器安裝的升級步驟](/help/sites-deploying/app-server-upgrade.md)。

## 升級前步驟 {#pre-upgrade-steps}

在執行升級之前，必須完成數個步驟。 如需詳細資訊，請參閱[升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md)和[升級前維護工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，請確認您的系統符合新版AEM的需求。 瞭解模式偵測器如何協助您估計升級作業的複雜性，並參閱[規劃升級](/help/sites-deploying/upgrade-planning.md)的升級範圍和需求一節，以取得詳細資訊。

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 移轉先決條件 {#migration-prerequisites}

* **最低必要的Java版本：**&#x200B;移轉工具只適用於Java 7及更高版本。 請注意，AEM 6.3及更高版本僅支援Oracle的JRE 8和IBM的JRE 7及8。

* **已升級的執行個體：**&#x200B;如果您要從5.6 **之前的**&#x200B;版本升級，請依照升級檔案6.0版本中所述的程式，確定您已執行就地升級到AEM 6.0。

## 準備AEM Quickstart jar檔案 {#prep-quickstart-file}

1. 如果執行個體正在執行，請停止執行個體。

1. 下載新的AEM jar檔案，並使用它來取代`crx-quickstart`資料夾之外的舊檔案。

1. 透過執行以下動作將新的quickstart jar解壓縮：

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 內容存放庫移轉 {#content-repository-migration}

如果您從AEM 6.3升級，則不需要進行此移轉。對於6.3之前的版本，Adobe提供了一個工具，可用來將存放庫移轉至AEM 6.3中存在的新版Oak Segment Tar。這是快速入門套件的一部分，且是任何將使用TarMK的升級的必要專案。 升級使用MongoMK的環境不需要移轉存放庫。 如需新的區段Tar格式優點詳細資訊，請參閱[移轉至Oak區段Tar常見問題集](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)。

實際移轉是使用標準AEM quickstart jar檔案執行，並使用新的`-x crx2oak`選項執行，該選項會執行crx2oak工具以簡化升級並使其更健全。

>[!NOTE]
>
>如果您使用CRX2Oak Quickstart擴充功能執行TarMK存放庫內容移轉，您可以將下列專案新增至移轉命令列，以移除&#x200B;**samplecontent**&#x200B;執行模式：
>
>* `--promote-runmode nosamplecontent`
>

若要決定應該執行的命令，請使用下列命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

其中`<<YOUR_PROFILE>>`和`<<ADDITIONAL_FLAGS>>`取代為下表列出的設定檔和旗標：

<table>
 <tbody>
  <tr>
   <td><strong>Source存放庫</strong></td>
   <td><strong>目標存放庫</strong></td>
   <td><strong>設定檔</strong></td>
   <td><strong>其他旗標</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2或TarMK，使用 <code>FileDataStore</code></td>
   <td>tarmk</td>
   <td>segment-fds</td>
   <td>請參閱下方的疑難排解一節</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMk</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK或crx2，帶 <code>S3DataStore</code></td>
   <td>tarmk</td>
   <td>segment-custom-ds</td>
   <td>請參閱下方的疑難排解一節</td>
  </tr>
  <tr>
   <td>沒有資料存放區的TarMK</td>
   <td>tarmk</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMk</td>
   <td>MongoMk</td>
   <td>不需要移轉</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**位置：**

* `mongo-host`是MongoDB伺服器IP （例如127.0.0.1）

* `mongo-port`是MongoDB伺服器連線埠(例如： 27017)

* `mongo-database-name`代表資料庫的名稱（例如：aem-author）

**下列情況可能也需要其他引數：**

* 如果您正在未正確處理Java記憶體對應的Windows系統上執行升級，請將`--disable-mmap`引數新增至命令。

如需使用crx2oak工具的其他指示，請參閱使用[CRX2Oak移轉工具](/help/sites-deploying/using-crx2oak.md)。 如果需要，可以手動升級crx2oak helper JAR，方法是在解壓縮快速入門後，以較新的版本手動將其取代。 它在AEM安裝資料夾中的位置是： `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`。 最新版本的CRX2Oak移轉工具可從Adobe存放庫下載，網址為： [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

如果移轉成功完成，工具將會以零的退出代碼結束。 此外，請檢查位於AEM安裝目錄`crx-quickstart/logs`下的`upgrade.log`檔案中的WARN和ERROR訊息，因為這些訊息可能表示移轉期間發生非嚴重錯誤。

檢查`crx-quickstart/install`資料夾下的組態檔。 如果需要進行移轉，這些將會更新以反映目標存放庫。

**資料存放區上的備註：**

雖然`FileDataStore`是AEM 6.3安裝的新預設值，但不需要使用外部資料存放區。 雖然我們建議使用外部資料存放區作為生產部署的最佳實務，但這並非升級的先決條件。 由於升級AEM中已存在的複雜性，Adobe建議執行升級而不執行資料存放區移轉。 如有需要，資料存放區移轉可以在之後作為單獨的工作執行。

## 疑難排解移轉問題 {#troubleshooting-migration-issues}

如果您從6.3升級，請略過本節。雖然提供的crx2oak設定檔應符合大部分客戶的需求，但有時仍需要其他引數。 如果您在移轉期間發生錯誤，可能是環境的某些方面需要提供額外的設定選項。 若是如此，您可能會遇到下列錯誤：

**未複製查核點，因為未指定外部資料存放區。 這將導致在第一次啟動時完整的存放庫重新索引。 使用 — skip-checkpoints強制移轉，或參閱https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration以取得更多資訊。**

由於某種原因，移轉程式需要存取資料存放區中的二進位檔案，但找不到該二進位檔案。 若要指定您的資料存放區組態，請在移轉命令的`<<ADDITIONAL_FLAGS>>`部分中包含下列標幟：

S3資料存放區的&#x200B;**：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

其中`/path/to/SharedS3DataStore.config`代表S3資料存放區設定檔案的路徑，`/path/to/datastore`代表S3資料存放區的路徑。

檔案資料存放區的&#x200B;**：**

```shell
--src-datastore=/path/to/datastore
```

其中`/path/to/datastore`代表檔案資料存放區的路徑。

## 執行升級 {#performing-the-upgrade}

**如果使用S3：**

1. 移除`crx-quickstart/install`底下與舊版S3聯結器關聯的所有jar。

1. 從[https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)下載1.10.x S3聯結器的最新版本

1. 將封裝解壓縮至暫存資料夾，並將`jcr_root/libs/system/install`的內容複製到`crx-quickstart/install`資料夾。

### 正在判斷正確的升級開始命令 {#determining-the-correct-upgrade-start-command}

若要執行升級，重要的是使用jar檔案啟動AEM以啟動執行個體。 若要升級至6.5，請參閱[延遲內容移轉](/help/sites-deploying/lazy-content-migration.md)中的其他內容重組和移轉選項，您可以使用升級命令來選擇這些選項。

>[!IMPORTANT]
>
>如果您執行OracleJava 11 （或通常是8以上的Java版本），啟動AEM時必須在命令列新增其他引數。 如需詳細資訊，請參閱[Java 11考量事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)。

請注意，從啟動指令碼啟動AEM將不會啟動升級。 大多數客戶使用啟動指令碼啟動AEM，並已自訂此啟動指令碼，以包含環境設定（例如記憶體設定、安全性憑證等）的開關。 因此，Adobe建議依照此程式來決定正確的升級命令：

1. 在執行中的AEM執行個體上，從命令列執行下列動作：

   ```shell
   ps -ef | grep java
   ```

1. 尋找AEM程式。 它看起來會像這樣：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 將現有jar （在此例中為`crx-quickstart/app/aem-quickstart*.jar`）的路徑取代為`crx-quickstart`資料夾的同層級新jar，以修改命令。 以我們先前的指令為例，我們的指令會是：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   這將確保所有適當的記憶體設定、自訂執行模式和其他環境引數都套用於升級。 升級完成後，執行個體可在未來啟動時從啟動指令碼啟動。

## 部署升級的程式碼基底 {#deploy-upgraded-codebase}

就地升級程式完成後，應部署更新的程式碼基底。 您可以在[升級程式碼和自訂頁面](/help/sites-deploying/upgrading-code-and-customizations.md)中找到更新程式碼基底以在AEM目標版本中運作的步驟。

## 執行Post升級檢查及疑難排解 {#perform-post-upgrade-check-troubleshooting}

請參閱[Post升級檢查與疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
