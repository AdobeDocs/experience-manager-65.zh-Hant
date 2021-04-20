---
title: 執行就地升級
seo-title: 執行就地升級
description: 瞭解如何執行就地升級。
seo-description: 瞭解如何執行就地升級。
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---


# 執行就地升級{#performing-an-in-place-upgrade}

>[!NOTE]
>
>本頁概述6.5的AEM升級程式。如果您有部署到應用程式伺服器的安裝，請參閱[應用程式伺服器安裝升級步驟](/help/sites-deploying/app-server-upgrade.md)。

## 升級前步驟{#pre-upgrade-steps}

在執行升級之前，必須先執行數個步驟。 如需詳細資訊，請參閱[升級程式碼與自訂](/help/sites-deploying/upgrading-code-and-customizations.md)和[升級前維護工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。 此外，請確定您的系統符合新版本的需AEM求。 瞭解模式檢測器如何幫助您估計升級的複雜性，並參閱[規劃升級](/help/sites-deploying/upgrade-planning.md)的「升級範圍和要求」一節，瞭解更多資訊。

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 遷移先決條件{#migration-prerequisites}

* **最低需要的Java版本：** 移轉工具僅適用於Java版本7及更新版本。請注意，AEM在6.3和更新版本中，Oracle的JRE 8和IBM的JRE 7和8是唯一受支援的版本。

* **升級實** 例：如果您是從 **** 5.6以前的版本升級，請依照升級檔案6.0版中描述的程式，確定您已執行就地升級至AEM6.0。

## 準備Quickstart AEMjar檔案{#prep-quickstart-file}

1. 如果執行中，請停止執行個體。

1. 下載新AEM的jar檔案，並使用它替換`crx-quickstart`資料夾外的舊檔案。

1. 通過運行以下命令來解壓縮新的快速啟動jar:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 內容儲存庫遷移{#content-repository-migration}

如果您要從6.3升級，則不需要AEM進行此移轉。對於6.3以前的版本，Adobe提供了一個工具，可用來將儲存庫遷移到6.3中出現的Oak Segment Tar的新AEM版本。它是快速啟動軟體包的一部分，對於將使用TarMK的任何升級都是強制性的。 使用MongoMK的環境的升級不需要儲存庫遷移。 如需新區段Tar格式的優點的詳細資訊，請參閱[移轉至Oak區段Tar常見問答集](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)。

實際遷移是使用標準快速入門AEMjar檔案執行的，該檔案使用新的`-x crx2oak`選項執行crx2oak工具，以簡化升級並使其更加強穩。

>[!NOTE]
>
>如果您使用CRX2Oak Quickstart副檔名執行TarMK儲存庫內容遷移，則可以通過向遷移命令行添加以下內容來刪除&#x200B;**samplecontent**&#x200B;運行模式：
>
>* `--promote-runmode nosamplecontent`

>



要確定應運行的命令，請使用以下命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

其中`<<YOUR_PROFILE>>`和`<<ADDITIONAL_FLAGS>>`被下表中列出的配置檔案和標誌替換：

<table>
 <tbody>
  <tr>
   <td><strong>源資料庫</strong></td>
   <td><strong>目標儲存庫</strong></td>
   <td><strong>設定檔</strong></td>
   <td><strong>其他標幟</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2或TarMK搭配 <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>請參閱以下的疑難排解章節</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK或crx2含 <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>請參閱以下的疑難排解章節</td>
  </tr>
  <tr>
   <td>沒有資料儲存的TarMK</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>不需要移轉</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**其中：**

* `mongo-host` 是MongoDB伺服器IP（例如127.0.0.1）

* `mongo-port` 是MongoDB伺服器埠(例如：（郵編：27017）

* `mongo-database-name` 表示資料庫的名稱(例如：aem-author)

**您可能還需要為以下情況提供額外的交換機：**

* 如果在Java記憶體映射處理不正確的Windows系統上執行升級，請將`--disable-mmap`參數添加到命令中。

* 如果您使用Java 7，請在`-Xmx`參數後面加入`-XX:MaxPermSize=2048m`參數。

如需有關使用crx2oak工具的其他指示，請參閱使用[CRX2Oak Migration Tool](/help/sites-deploying/using-crx2oak.md)。 如果需要，可以手動升級crx2oak helper JAR，方法是在解壓縮快速啟動後手動將其替換為較新版本。 它在安裝資料夾AEM中的位置是：`<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`。 CRX2Oak移轉工具的最新版本可從Adobe資料庫下載，網址為：[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

如果移轉成功完成，工具將退出，退出代碼為零。 此外，請檢查安裝目錄中`crx-quickstart/logs`下方的`upgrade.log`檔案中的WARN和ERROR消息AEM，因為這些消息可能表示遷移過程中發生的非致命錯誤。

檢查`crx-quickstart/install`資料夾下的配置檔案。 如果需要遷移，將更新這些遷移以反映目標儲存庫。

**關於資料儲存的注釋：**

雖然`FileDataStore`是6.3安裝的新預設值，AEM但不需要使用外部資料儲存。 雖然建議使用外部資料儲存作為生產部署的最佳做法，但升級並非先決條件。 由於升級過程中已存在複雜性，AEM建議您執行升級而不執行資料儲存遷移。 如果需要，可以隨後執行資料儲存遷移作為單獨的工作。

## 移轉問題疑難排解{#troubleshooting-migration-issues}

如果您要從6.3升級，請略過本節。雖然提供的crx2oak設定檔應符合大部份客戶的需求，但有時需要額外的參數。 如果在遷移過程中遇到錯誤，則環境的某些方面可能需要提供額外的配置選項。 如果是，您可能會遇到下列錯誤：

**不會複製查核點，因為未指定外部資料存放區。這將導致在第一次啟動時對完整儲存庫重新編製索引。 使用—skip-chreciptory強制遷移，或查看https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration以獲取更多資訊。**

由於某些原因，遷移過程需要訪問資料儲存中的二進位檔案，因此找不到它。 要指定資料儲存配置，請在遷移命令的`<<ADDITIONAL_FLAGS>>`部分中包含以下標誌：

**對於S3資料儲存：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

其中`/path/to/SharedS3DataStore.config`代表S3資料儲存配置檔案的路徑，`/path/to/datastore`代表S3資料儲存的路徑。

**對於檔案資料儲存：**

```shell
--src-datastore=/path/to/datastore
```

其中`/path/to/datastore`代表檔案資料儲存區的路徑。

## 執行升級{#performing-the-upgrade}

**如果使用S3:**

1. 刪除`crx-quickstart/install`下與舊版S3連接器相關的所有jar。

1. 從[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)下載1.10.x S3連接器的最新版本

1. 將軟體包解壓到臨時資料夾，並將`jcr_root/libs/system/install`的內容複製到`crx-quickstart/install`資料夾。

### 確定正確的升級開始命令{#determining-the-correct-upgrade-start-command}

要執行升級，請務必開始使AEM用jar檔案來開啟實例。 若要升級至6.5，請參閱[Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md)中的其他內容重組和移轉選項，您可使用upgrade命令選擇這些選項。

>[!IMPORTANT]
>
>如果您正在運行Java 11Oracle（或通常8以上版本的Java），則啟動時需要將其他開關添加到命令行AEM。 如需詳細資訊，請參閱[Java 11考量事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)。

請注意，從AEM開始指令碼開始將不會啟動升級。 大多數客AEM戶都開始使用啟動指令碼並自定義此啟動指令碼，以包括用於環境配置的交換機，如記憶體設定、安全證書等。 因此，我們建議按照此過程確定正確的升級命令：

1. 在正在運行AEM的實例上，從命令行執行以下操作：

   ```shell
   ps -ef | grep java
   ```

1. 尋找程AEM序。 看起來會像：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 修改命令，方法是將現有jar的路徑(在本例中為`crx-quickstart`資料夾的同級新jar替換為`crx-quickstart/app/aem-quickstart*.jar`資料夾的同級路徑。 以我們的上一個命令為例，我們的命令為：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   這將確保所有正確的記憶體設定、自訂執行模式和其他環境參數都適用於升級。 升級完成後，實例可從未來初創公司的開始指令碼開始。

## 部署升級的代碼庫{#deploy-upgraded-codebase}

在就地升級程式完成後，應部署更新的程式碼庫。 有關將代碼庫更新為在目標版本的AEM步驟，請參閱[升級代碼和自定義頁](/help/sites-deploying/upgrading-code-and-customizations.md)。

## 執行升級後檢查和疑難排解{#perform-post-upgrade-check-troubleshooting}

請參閱[升級後檢查和疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
