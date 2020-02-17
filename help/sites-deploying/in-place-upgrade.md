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
translation-type: tm+mt
source-git-commit: a8deb66b23e6ddde9c5f6379ef4f766668336369

---


# 執行就地升級{#performing-an-in-place-upgrade}

>[!NOTE]
>
>本頁概述AEM 6.5的升級程式。如果您有已部署至應用程式伺服器的安裝，請參閱應用程 [式伺服器安裝的升級步驟](/help/sites-deploying/app-server-upgrade.md)。

## 升級前步驟 {#pre-upgrade-steps}

在執行升級之前，必須先執行數個步驟。 如需 [詳細資訊，請參閱](/help/sites-deploying/upgrading-code-and-customizations.md)[升級程式碼與自訂與升級前維護工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 。 此外，請確定您的系統符合新版AEM的需求。 瞭解模式檢測器如何協助您估計升級的複雜性，並參閱規劃升級的升級範圍和 [需求一節](/help/sites-deploying/upgrade-planning.md) ，以取得詳細資訊。

## 移轉先決條件 {#migration-prerequisites}

* **** 最低需求Java版本：移轉工具僅適用於Java第7版（含）以上版本。 請注意，對於AEM 6.3和更新版本，Oracle的JRE 8和IBM的JRE 7 &amp; 8是唯一支援的版本。

* **** 升級實例：如果您是從5.6 **以上版本升級**，請依照6.0版升級檔案中所述的程式，確定您已執行就地升級至AEM 6.0。

## 準備AEM Quickstart jar檔案 {#prep-quickstart-file}

1. 如果執行中，請停止執行個體。

1. 下載新的AEM jar檔案，並使用它來取代檔案夾外的舊 `crx-quickstart` 檔案。

1. 通過運行以下命令來解壓縮新的快速啟動jar:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 內容儲存庫遷移 {#content-repository-migration}

如果您要從AEM 6.3升級，則不需要進行此移轉。對於6.3以上版本，Adobe提供可用來將儲存庫移轉至AEM 6.3中出現的新版Oak Segment Tar的工具。它是快速啟動軟體包的一部分，對於將使用TarMK的任何升級都是強制性的。 使用MongoMK的環境的升級不需要儲存庫遷移。 如需新區段Tar格式的優點的詳細資訊，請參閱移轉至 [Oak區段Tar常見問答](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)。

實際移轉是使用標準AEM快速入門jar檔案來執行，此檔案會使用新的 `-x crx2oak` 選項執行crx2oak工具，以簡化升級並使其更強穩。

>[!NOTE]
>
>如果您使用CRX2Oak Quickstart副檔名執行TarMK儲存庫內容遷移，則可以通過向遷移命令行添加以下內容來刪除 **samplecontent** runmode:
>
>* `--promote-runmode nosamplecontent`
>



要確定應運行的命令，請使用以下命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

其中 `<<YOUR_PROFILE>>` 和 `<<ADDITIONAL_FLAGS>>` 將替換為下表中列出的配置檔案和標誌：

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

* 如果您在Windows系統上執行升級，但Java記憶體映射處理不正確，請將該參 `--disable-mmap` 數添加到命令。

* 如果您使用Java 7，請在參數 `-XX:MaxPermSize=2048m` 後面加入參 `-Xmx` 數。

如需有關使用crx2oak工具的其他指示，請參閱「使用 [CRX2Oak移轉工具」](/help/sites-deploying/using-crx2oak.md)。 如果需要，可以手動升級crx2oak helper JAR，方法是在解壓縮快速啟動後手動將其替換為較新版本。 其在AEM安裝資料夾中的位置為： `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`。 CRX2Oak移轉工具的最新版本可從Adobe Repository下載，網址為： [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

如果移轉成功完成，工具將退出，退出代碼為零。 此外，請檢查檔案中的 `upgrade.log` WARN和ERROR訊息(位於 `crx-quickstart/logs` AEM安裝目錄下)，因為這些訊息可能表示在移轉期間發生非致命錯誤。

檢查資料夾下的配置 `crx-quickstart/install` 檔案。 如果需要遷移，將更新這些遷移以反映目標儲存庫。

**關於資料儲存的注釋：**

雖然 `FileDataStore` 是AEM 6.3安裝的新預設值，但不需要使用外部資料儲存區。 雖然建議使用外部資料儲存作為生產部署的最佳做法，但升級並非先決條件。 由於升級AEM已經相當複雜，我們建議您執行升級而不執行資料儲存區移轉。 如果需要，可以隨後執行資料儲存遷移作為單獨的工作。

## 疑難排解移轉問題 {#troubleshooting-migration-issues}

如果您要從6.3升級，請略過本節。雖然提供的crx2oak設定檔應符合大部份客戶的需求，但有時需要額外的參數。 如果在遷移過程中遇到錯誤，則環境的某些方面可能需要提供額外的配置選項。 如果是，您可能會遇到下列錯誤：

**不會複製查核點，因為未指定外部資料存放區。 這將導致在第一次啟動時對完整儲存庫重新編製索引。 使用—skip-chreckiptor強制遷移，或參閱https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration以取得更多資訊。**

由於某些原因，遷移過程需要訪問資料儲存中的二進位檔案，因此找不到它。 要指定資料儲存配置，請在遷移命令的部分中 `<<ADDITIONAL_FLAGS>>` 包含以下標誌：

**對於S3資料儲存：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

其中 `/path/to/SharedS3DataStore.config` 代表S3資料儲存配置檔案的路徑， `/path/to/datastore` 並代表S3資料儲存的路徑。

**對於檔案資料儲存：**

```shell
--src-datastore=/path/to/datastore
```

其中 `/path/to/datastore` 代表檔案資料儲存的路徑。

## 執行升級 {#performing-the-upgrade}

**如果使用S3:**

1. 刪除與舊版S3 `crx-quickstart/install` 連接器相關聯的所有jar。

1. 從https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/下載最新版1.8.x S3連接器 [](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. 將包解壓到臨時資料夾，並將其內容復 `jcr_root/libs/system/install` 制到該文 `crx-quickstart/install` 件夾。

### 確定正確的升級開始命令 {#determining-the-correct-upgrade-start-command}

若要執行升級，請務必使用jar檔案啟動AEM以啟動執行個體。 若要升級至6.5，另請參閱 [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) （懶惰內容移轉）中的其他內容重組和移轉選項，您可使用upgrade命令進行選擇。

請注意，從開始指令碼開始AEM將不會開始升級。 大部分客戶都使用開始指令碼來啟動AEM，並自訂此開始指令碼，以加入環境組態的開關，例如記憶體設定、安全憑證等。 因此，我們建議按照此過程確定正確的升級命令：

1. 在執行中的AEM例項上，從命令列執行下列動作：

   ```shell
   ps -ef | grep java
   ```

1. 尋找AEM程式。 看起來會像：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 通過用新jar（即資料夾的同級）替換現 `crx-quickstart/app/aem-quickstart*.jar` 有jar的路徑（在本例中）來修改該命 `crx-quickstart` 令。 以我們的上一個命令為例，我們的命令為：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   這將確保所有正確的記憶體設定、自訂執行模式和其他環境參數都適用於升級。 升級完成後，實例可從未來初創公司的開始指令碼開始。

## 部署升級的代碼庫 {#deploy-upgraded-codebase}

在就地升級程式完成後，應部署更新的程式碼庫。 升級程式碼和自訂頁面中提供更新程式碼庫以在AEM目標版本中運作 [的步驟](/help/sites-deploying/upgrading-code-and-customizations.md)。

## 執行升級後檢查和疑難排解 {#perform-post-upgrade-check-troubleshooting}

請參 [閱升級後檢查和疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
