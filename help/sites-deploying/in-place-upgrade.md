---
title: 執行就地升級
description: 了解如何執行就地升級。
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: 6d2b7e341dcdedf3c000b9fb0ecd21722bdf2a27
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# 執行就地升級{#performing-an-in-place-upgrade}

>[!NOTE]
>
>本頁概述AEM 6.5的升級過程。如果您有部署到應用程式伺服器的安裝，請參閱 [應用程式伺服器安裝的升級步驟](/help/sites-deploying/app-server-upgrade.md).

## 升級前步驟 {#pre-upgrade-steps}

執行升級前，必須完成幾個步驟。 請參閱 [升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md) 和 [升級前維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 以取得更多資訊。 此外，請確定您的系統符合新版AEM的需求。 請參閱模式偵測器如何協助您評估升級的複雜度，並參閱升級範圍和需求一節。 [規劃升級](/help/sites-deploying/upgrade-planning.md) 以取得更多資訊。

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 移轉必要條件 {#migration-prerequisites}

* **最低必要Java版本：** 移轉工具只適用於Java 7及更新版本。 請注意，對於AEM 6.3及更高版本，Oracle的JRE 8和IBM的JRE 7和8是唯一支援的版本。

* **升級實例：** 如果您從版本升級 **大於5.6**，請依照升級說明檔案6.0版中所述的程式，確認您已執行AEM 6.0就地升級。

## 準備AEM Quickstart jar檔案 {#prep-quickstart-file}

1. 停止執行個體（如果執行中）。

1. 下載新的AEM jar檔案，並使用它來取代 `crx-quickstart` 檔案夾。

1. 運行以解壓縮新的快速啟動Jar:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 內容存放庫移轉 {#content-repository-migration}

如果您要從AEM 6.3升級，則不需要進行此移轉。若是6.3以前的版本，Adobe提供工具可將存放庫移轉至AEM 6.3中出現的新版Oak Segment Tar。此工具是快速入門套件的一部分，且對於將使用TarMK的任何升級，均強制執行。 使用MongoMK的環境升級不需要存放庫移轉。 如需新區段Tar格式的優點的詳細資訊，請參閱 [移轉至Oak Segment Tar常見問題集](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

實際遷移是使用標準AEM Quickstart Jar檔案執行的，使用新 `-x crx2oak` 選項，執行crx2oak工具以簡化升級並使其更強大。

>[!NOTE]
>
>如果您使用CRX2Oak Quickstart擴充功能執行TarMK存放庫內容移轉，您可以移除 **samplecontent** 在migration命令列中新增下列項目以執行模式：
>
>* `--promote-runmode nosamplecontent`
>


要確定應運行的命令，請使用以下命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

其中 `<<YOUR_PROFILE>>` 和 `<<ADDITIONAL_FLAGS>>` 會以下表中列出的設定檔和標幟取代：

<table>
 <tbody>
  <tr>
   <td><strong>源儲存庫</strong></td>
   <td><strong>目標儲存庫</strong></td>
   <td><strong>設定檔</strong></td>
   <td><strong>其他標幟</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2或TarMK搭配 <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>請參閱下方的疑難排解一節</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK或crx2搭配 <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>請參閱下方的疑難排解一節</td>
  </tr>
  <tr>
   <td>沒有資料存放區的TarMK</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>無需遷移</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**其中：**

* `mongo-host` 是MongoDB伺服器IP（例如127.0.0.1）

* `mongo-port` 是MongoDB伺服器埠(例如：27017)

* `mongo-database-name` 表示資料庫的名稱(例如：aem-author)

**在以下情況下，您可能還需要其他交換機：**

* 如果您在Java記憶體映射未正確處理的Windows系統上執行升級，請添加 `--disable-mmap` 參數。

* 如果您使用Java 7，請新增 `-XX:MaxPermSize=2048m` 參數 `-Xmx` 參數。

如需使用crx2oak工具的其他指示，請參閱使用 [CRX2Oak移轉工具](/help/sites-deploying/using-crx2oak.md). 如有需要，可手動升級crx2oak helper JAR，方法是在解壓縮快速入門程式後，以較新版本手動取代它。 其在AEM安裝資料夾中的位置為： `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. 最新版的CRX2Oak移轉工具可從Adobe存放庫下載： [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

如果移轉成功完成，則工具會退出，退出代碼為零。 此外，檢查 `upgrade.log` 檔案，位於 `crx-quickstart/logs` 在AEM安裝目錄中，因為這些可能表示移轉期間發生非致命錯誤。

檢查下方的組態檔 `crx-quickstart/install` 檔案夾。 如果需要移轉，則會更新以反映目標存放庫。

**資料儲存區的附註：**

同時 `FileDataStore` 是AEM 6.3安裝的新預設值，不需要使用外部資料存放區。 雖然建議使用外部資料存放區作為生產部署的最佳實務，但升級並非先決條件。 由於升級AEM中已存在複雜性，建議您執行升級而不執行資料存放區移轉。 如有需要，可在之後以單獨作業的方式執行資料存放區移轉。

## 疑難排解移轉問題 {#troubleshooting-migration-issues}

如果您從6.3升級，請略過本節。雖然提供的crx2oak設定檔應符合大部分客戶的需求，但有時需要其他參數。 如果您在移轉期間遇到錯誤，環境的某些方面可能需要提供其他設定選項。 若是如此，您可能會遇到下列錯誤：

**不會複製查核點，因為未指定外部資料存放區。 這會導致第一個開始時對完整的存放庫重新編製索引。 使用 — skip-chreckpoint強制移轉，或參閱https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration以取得詳細資訊。**

由於某些原因，移轉程式需要存取資料存放區中的二進位檔，且找不到。 若要指定您的資料存放區設定，請在 `<<ADDITIONAL_FLAGS>>` 遷移命令的一部分：

**S3資料存放區：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

其中 `/path/to/SharedS3DataStore.config` 代表S3資料存放區設定檔案的路徑，且 `/path/to/datastore` 代表S3資料存放區的路徑。

**對於檔案資料儲存：**

```shell
--src-datastore=/path/to/datastore
```

其中 `/path/to/datastore` 代表檔案資料存放區的路徑。

## 執行升級 {#performing-the-upgrade}

**如果使用S3:**

1. 移除下方的任何jar `crx-quickstart/install` 與舊版S3連接器相關聯。

1. 請從下載1.10.x S3連接器的最新版本 [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. 將包解壓到臨時資料夾並複製 `jcr_root/libs/system/install` 到 `crx-quickstart/install` 檔案夾。

### 確定正確的升級開始命令 {#determining-the-correct-upgrade-start-command}

若要執行升級，請務必使用jar檔案啟動AEM以開啟執行個體。 若要升級至6.5，另請參閱 [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md) 使用升級命令進行選擇。

>[!IMPORTANT]
>
>如果您正在運行OracleJava 11（或通常8以上的Java版本），則啟動AEM時，需要將其他開關添加到命令行中。 如需詳細資訊，請參閱 [Java 11考量事項](/help/sites-deploying/custom-standalone-install.md#java-considerations).

請注意，從開始指令碼啟動AEM將不會啟動升級。 大多數客戶都使用啟動指令碼啟動AEM，並且已自定義此啟動指令碼以包括用於環境配置的交換機，如記憶體設定、安全證書等。 因此，我們建議按照此過程確定正確的升級命令：

1. 在執行中的AEM執行個體上，從命令列執行下列動作：

   ```shell
   ps -ef | grep java
   ```

1. 尋找AEM程式。 看起來會像這樣：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 通過替換現有jar的路徑( `crx-quickstart/app/aem-quickstart*.jar` 在本例中)，新jar是 `crx-quickstart` 檔案夾。 以上一個命令為例，我們的命令會是：

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   這將確保所有正確的記憶體設定、自定義運行模式和其他環境參數都應用於升級。 升級完成後，執行個體可從未來啟動的開始指令碼開始。

## 部署升級的代碼庫 {#deploy-upgraded-codebase}

完成就地升級程式後，應部署更新的程式碼基底。 更新程式碼基底以在目標版AEM中運作的步驟，請參閱 [「升級代碼和自定義」頁](/help/sites-deploying/upgrading-code-and-customizations.md).

## 執行升級後檢查和疑難排解 {#perform-post-upgrade-check-troubleshooting}

請參閱 [升級後檢查和疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
