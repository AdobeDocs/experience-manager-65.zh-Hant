---
title: 執行就地升級
description: 瞭解如何執行就地升級。
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: 64c9296554c55b539145dd59a14b2255b1750e47
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# 執行就地升級{#performing-an-in-place-upgrade}

>[!NOTE]
>
>本頁概述了6.5的AEM升級過程。如果已將安裝部署到應用程式伺服器，請參見 [應用程式伺服器安裝的升級步驟](/help/sites-deploying/app-server-upgrade.md)。

## 升級前步驟 {#pre-upgrade-steps}

在執行升級之前，必須完成幾個步驟。 請參閱 [升級代碼和自定義](/help/sites-deploying/upgrading-code-and-customizations.md) 和 [升級前維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 的子菜單。 此外，確保您的系統滿足新版本的要AEM求。 請參閱模式檢測器如何幫助您評估升級的複雜性，並參閱的升級範圍和要求部分 [計畫升級](/help/sites-deploying/upgrade-planning.md) 的子菜單。

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 遷移先決條件 {#migration-prerequisites}

* **所需的最低Java版本：** 遷移工具僅適用於Java版本7及更高版本。 請注意，AEM對於6.3及更高版本，Oracle的JRE 8和IBM的JRE 7和8是唯一受支援的版本。

* **已升級實例：** 如果要從版本升級 **大於5.6**，確保按照升級文檔6.0版中介紹的過程執行了到AEM6.0的就地升級。

## 準備AEMQuickstart jar檔案 {#prep-quickstart-file}

1. 如果實例正在運行，請停止該實例。

1. 下載新AEM的jar檔案，然後使用它替換 `crx-quickstart` 的子菜單。

1. 通過運行以下命令來解包新快速啟動jar:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## 內容儲存庫遷移 {#content-repository-migration}

如果從6.3升級，則不需要AEM此遷移。對於6.3版以前的版本，Adobe提供了一個工具，可用於將儲存庫遷移到6.3中提供的Oak Segment Tar的AEM新版本。它作為快速啟動軟體包的一部分提供，對於將使用TarMK的任何升級都是強制性的。 使用MongoMK的環境的升級不需要儲存庫遷移。 有關新段焦油格式的優勢的詳細資訊，請參見 [遷移到Oak Segment Tar常見問題](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)。

實際遷移使用標準快速啟AEM動jar檔案執行，並使用新檔案執行 `-x crx2oak` 選項，執行crx2oak工具以簡化升級並使其更強健。

>[!NOTE]
>
>如果使用CRX2Oak Quickstart擴展執行TarMK儲存庫內容遷移，則可以刪除 **示例** 將以下內容添加到遷移命令行以運行模式：
>
>* `--promote-runmode nosamplecontent`
>


要確定應運行的命令，請使用以下命令：

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

位置 `<<YOUR_PROFILE>>` 和 `<<ADDITIONAL_FLAGS>>` 替換為下表中列出的配置檔案和標誌：

<table>
 <tbody>
  <tr>
   <td><strong>源儲存庫</strong></td>
   <td><strong>目標儲存庫</strong></td>
   <td><strong>設定檔</strong></td>
   <td><strong>附加標誌</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2或TarMK <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>段fds</td>
   <td>請參閱下面的「疑難解答」部分</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>蒙戈MK</td>
   <td>從crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK或crx2 <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>段定制 — ds</td>
   <td>請參閱下面的「疑難解答」部分</td>
  </tr>
  <tr>
   <td>沒有資料儲存的TarMK</td>
   <td>TarMK</td>
   <td>段 — 無d</td>
   <td> </td>
  </tr>
  <tr>
   <td>蒙戈MK</td>
   <td>蒙戈MK</td>
   <td>不需要遷移</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**位置：**

* `mongo-host` 是MongoDB伺服器IP(例如，127.0.0.1)

* `mongo-port` 是MongoDB伺服器埠(例如：27017)

* `mongo-database-name` 表示資料庫的名稱(例如：aem author)

**您還可能需要為以下情形增加交換機：**

* 如果在未正確處理Java記憶體映射的Windows系統上執行升級，請添加 `--disable-mmap` 命令的參數。

* 如果使用Java 7，請添加 `-XX:MaxPermSize=2048m` 參數 `-Xmx` 的下界。

有關使用crx2oak工具的其他說明，請參閱使用 [CRX2Oak遷移工具](/help/sites-deploying/using-crx2oak.md)。 如果需要，可以手動升級crx2oak幫助程式JAR，方法是在解包快速啟動後用較新版本手動替換它。 它在安裝資料夾AEM中的位置是： `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`。 CRX2Oak遷移工具的最新版本可從Adobe資料庫下載，網址為： [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

如果遷移已成功完成，則該工具將退出，退出代碼為零。 此外，在 `upgrade.log` 檔案，位於 `crx-quickstart/logs` 安裝目AEM錄中，因為這些錯誤可能表示遷移期間發生的非致命錯誤。

檢查下面的配置檔案 `crx-quickstart/install` 的子菜單。 如果需要遷移，將更新這些遷移以反映目標儲存庫。

**有關資料儲存的注釋：**

同時 `FileDataStore` 是6.3安裝的AEM新預設值，不需要使用外部資料儲存。 雖然建議將使用外部資料儲存作為生產部署的最佳做法，但升級不是先決條件。 由於升級過程中已存在複雜性，AEM建議在不執行資料儲存遷移的情況下執行升級。 如果需要，可隨後作為單獨的工作執行資料儲存遷移。

## 遷移問題疑難解答 {#troubleshooting-migration-issues}

如果從6.3升級，請跳過此部分。雖然提供的crx2oak配置檔案應能滿足大多數客戶的需求，但有時需要額外的參數。 如果您在遷移過程中遇到錯誤，則可能需要提供其他配置選項。 如果是，您可能會遇到以下錯誤：

**不會複製檢查點，因為未指定外部資料儲存。 這將導致在第一次開始時對完整儲存庫重新編製索引。 使用 — skip-checkpoints強制遷移，或訪問https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration獲取詳細資訊。**

由於某些原因，遷移進程需要訪問資料儲存中的二進位檔案，但找不到它。 要指定資料儲存配置，請在 `<<ADDITIONAL_FLAGS>>` 遷移命令的一部分：

**對於S3資料儲存：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

位置 `/path/to/SharedS3DataStore.config` 表示S3資料儲存配置檔案的路徑， `/path/to/datastore` 表示S3資料儲存的路徑。

**對於檔案資料儲存：**

```shell
--src-datastore=/path/to/datastore
```

位置 `/path/to/datastore` 表示檔案資料儲存區的路徑。

## 執行升級 {#performing-the-upgrade}

**如果使用S3:**

1. 刪除下面的所有jar `crx-quickstart/install` 與早期版本的S3連接器關聯。

1. 從下載1.10.x S3連接器的最新版本 [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. 將包解壓到臨時資料夾並複製 `jcr_root/libs/system/install` 到 `crx-quickstart/install` 的子菜單。

### 確定正確的升級啟動命令 {#determining-the-correct-upgrade-start-command}

要執行升級，必須開始使AEM用jar檔案來啟動實例。 要升級到6.5，請參見中的其他內容重組和遷移選項 [懶惰內容遷移](/help/sites-deploying/lazy-content-migration.md) 可以使用升級命令進行選擇。

>[!IMPORTANT]
>
>如果您正在運行OracleJava 11（或Java的通常版本高於8），則啟動時需要將其他開關添加到命令行AEM。 有關詳細資訊，請參見 [Java 11注意事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)。

請注意，AEM從啟動指令碼開始不會啟動升級。 大多數客戶AEM都開始使用啟動指令碼，並已自定義此啟動指令碼，以包括用於環境配置的交換機，如記憶體設定、安全證書等。 因此，我們建議按照此過程確定正確的升級命令：

1. 在正在運行AEM的實例上，從命令行執行以下操作：

   ```shell
   ps -ef | grep java
   ```

1. 查看過AEM程。 它看起來會像：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 通過替換現有jar的路徑修改命令( `crx-quickstart/app/aem-quickstart*.jar` 在本例中)的新jar是 `crx-quickstart` 的子菜單。 以我們以前的命令為例，我們的命令將是：

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   這將確保為升級應用所有正確的記憶體設定、自定義運行模式和其他環境參數。 升級完成後，可以從將來啟動的啟動指令碼啟動實例。

## 部署升級的代碼庫 {#deploy-upgraded-codebase}

完成就地升級過程後，應部署更新的代碼庫。 有關更新代碼庫以在目標版本中工作的AEM步驟，請參見 [「升級代碼和自定義」頁](/help/sites-deploying/upgrading-code-and-customizations.md)。

## 執行升級後檢查和故障排除 {#perform-post-upgrade-check-troubleshooting}

請參閱 [升級後檢查和故障排除](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。
