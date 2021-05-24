---
title: 執行就地升級
seo-title: 執行就地升級
description: 了解如何執行就地升級。
seo-description: 了解如何執行就地升級。
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
feature: 升級
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---

# 執行就地升級{#performing-an-in-place-upgrade}

>[!NOTE]
>
>本頁概述AEM 6.5的升級過程。如果您有部署到應用程式伺服器的安裝，請參閱[應用程式伺服器安裝的升級步驟](/help/sites-deploying/app-server-upgrade.md)。

## 升級前步驟{#pre-upgrade-steps}

執行升級前，必須完成幾個步驟。 有關詳細資訊，請參閱[升級代碼和自定義](/help/sites-deploying/upgrading-code-and-customizations.md)和[升級前維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，請確定您的系統符合新版AEM的需求。 請參閱模式偵測器如何協助您評估升級的複雜性，並參閱[規劃升級](/help/sites-deploying/upgrade-planning.md)的升級範圍和需求一節以取得詳細資訊。

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 遷移必備條件{#migration-prerequisites}

* **最低必要Java版本：** 移轉工具僅適用於Java 7及更新版本。請注意，對於AEM 6.3和更高版本，Oracle的JRE 8和IBM的JRE 7和8是唯一支援的版本。

* **升級執行個體：** 如果您從5.6 **版以前的版本升級**，請依照升級說明檔案6.0版中所述的程式，確定您已執行AEM 6.0就地升級。

## 準備AEM Quickstart jar檔案{#prep-quickstart-file}

1. 停止執行個體（如果執行中）。

1. 下載新的AEM jar檔案，並使用它取代`crx-quickstart`資料夾外部的舊檔案。

1. 運行以解壓縮新的快速啟動Jar:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 內容儲存庫遷移{#content-repository-migration}

如果您要從AEM 6.3升級，則不需要進行此移轉。若是6.3以前的版本，Adobe提供工具可將存放庫移轉至AEM 6.3中出現的新版Oak Segment Tar。此工具是快速入門套件的一部分，且對於將使用TarMK的任何升級，均強制執行。 使用MongoMK的環境升級不需要存放庫移轉。 如需新區段Tar格式的優點的詳細資訊，請參閱[移轉至Oak區段Tar常見問題集](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)。

實際移轉是使用標準AEM Quickstart jar檔案執行，此檔案會使用新的`-x crx2oak`選項執行，此選項會執行crx2oak工具，以簡化升級並使其更穩健。

>[!NOTE]
>
>如果您使用CRX2Oak Quickstart擴充功能執行TarMK存放庫內容移轉，您可以將下列項目新增至移轉命令列，以移除&#x200B;**samplecontent**&#x200B;執行模式：
>
>* `--promote-runmode nosamplecontent`

>



要確定應運行的命令，請使用以下命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

其中`<<YOUR_PROFILE>>`和`<<ADDITIONAL_FLAGS>>`被下表中列出的設定檔和標幟取代：

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

* 如果在Java記憶體映射未正確處理的Windows系統上執行升級，請將`--disable-mmap`參數添加到命令中。

* 如果您使用Java 7，請在`-Xmx`參數後面新增`-XX:MaxPermSize=2048m`參數。

如需使用crx2oak工具的其他指示，請參閱使用[CRX2Oak移轉工具](/help/sites-deploying/using-crx2oak.md)。 如有需要，可手動升級crx2oak helper JAR，方法是在解壓縮快速入門程式後，以較新版本手動取代它。 其在AEM安裝資料夾中的位置為：`<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`。 最新版的CRX2Oak移轉工具可從Adobe存放庫下載：[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

如果移轉成功完成，則工具會退出，退出代碼為零。 此外，在位於AEM安裝目錄`crx-quickstart/logs`下的`upgrade.log`檔案中檢查WARN和ERROR消息，因為這些消息可能表示遷移過程中發生的非致命錯誤。

檢查`crx-quickstart/install`資料夾下的配置檔案。 如果需要移轉，則會更新以反映目標存放庫。

**資料儲存區的附註：**

雖然`FileDataStore`是AEM 6.3安裝的新預設值，但不需要使用外部資料存放區。 雖然建議使用外部資料存放區作為生產部署的最佳實務，但升級並非先決條件。 由於升級AEM中已存在複雜性，建議您執行升級而不執行資料存放區移轉。 如有需要，可在之後以單獨作業的方式執行資料存放區移轉。

## 疑難排解移轉問題{#troubleshooting-migration-issues}

如果您從6.3升級，請略過本節。雖然提供的crx2oak設定檔應符合大部分客戶的需求，但有時需要其他參數。 如果您在移轉期間遇到錯誤，環境的某些方面可能需要提供其他設定選項。 若是如此，您可能會遇到下列錯誤：

**不會複製查核點，因為未指定外部資料存放區。這會導致第一個開始時對完整的存放庫重新編製索引。 使用 — skip-checkpoint強制遷移，或查看https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration以了解更多資訊。**

由於某些原因，移轉程式需要存取資料存放區中的二進位檔，且找不到。 若要指定資料存放區設定，請在移轉命令的`<<ADDITIONAL_FLAGS>>`部分加入下列標幟：

**S3資料存放區：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

其中`/path/to/SharedS3DataStore.config`代表S3資料存放區設定檔案的路徑，而`/path/to/datastore`代表S3資料存放區的路徑。

**對於檔案資料儲存：**

```shell
--src-datastore=/path/to/datastore
```

其中`/path/to/datastore`代表檔案資料存放區的路徑。

## 執行升級{#performing-the-upgrade}

**如果使用S3:**

1. 移除與舊版S3連接器相關聯的`crx-quickstart/install`下方的任何jar。

1. 從[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)下載1.10.x S3連接器的最新版本

1. 將包解壓縮到臨時資料夾，並將`jcr_root/libs/system/install`的內容複製到`crx-quickstart/install`資料夾。

### 確定正確的升級開始命令{#determining-the-correct-upgrade-start-command}

若要執行升級，請務必使用jar檔案啟動AEM以開啟執行個體。 若要升級至6.5，請在[延遲內容遷移](/help/sites-deploying/lazy-content-migration.md)中查看其他內容重組和遷移選項，您可以使用升級命令選擇這些選項。

>[!IMPORTANT]
>
>如果您正在運行OracleJava 11（或通常8以上的Java版本），則啟動AEM時，需要將其他開關添加到命令行中。 如需詳細資訊，請參閱[Java 11考量事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)。

請注意，從開始指令碼啟動AEM將不會啟動升級。 大多數客戶都使用啟動指令碼啟動AEM，並且已自定義此啟動指令碼以包括用於環境配置的交換機，如記憶體設定、安全證書等。 因此，我們建議按照此過程確定正確的升級命令：

1. 在執行中的AEM執行個體上，從命令列執行下列動作：

   ```shell
   ps -ef | grep java
   ```

1. 尋找AEM程式。 看起來會像這樣：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 修改命令，方法是使用作為`crx-quickstart`資料夾的同級的新jar替換現有jar的路徑（在本例中為`crx-quickstart/app/aem-quickstart*.jar`）。 以上一個命令為例，我們的命令會是：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   這將確保所有正確的記憶體設定、自定義運行模式和其他環境參數都應用於升級。 升級完成後，執行個體可從未來啟動的開始指令碼開始。

## 部署升級的代碼庫{#deploy-upgraded-codebase}

完成就地升級程式後，應部署更新的程式碼基底。 在[升級代碼和自訂頁面](/help/sites-deploying/upgrading-code-and-customizations.md)中，可找到更新代碼庫以在AEM目標版本中運作的步驟。

## 執行升級後檢查和故障排除{#perform-post-upgrade-check-troubleshooting}

請參閱[升級後檢查和疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
