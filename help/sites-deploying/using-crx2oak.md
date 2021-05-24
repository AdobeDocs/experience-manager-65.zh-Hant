---
title: 使用CRX2Oak移轉工具
seo-title: 使用CRX2Oak移轉工具
description: 了解如何使用CRX2Oak移轉工具。
seo-description: 了解如何使用CRX2Oak移轉工具。
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
feature: 升級
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 0%

---

# 使用CRX2Oak移轉工具{#using-the-crx-oak-migration-tool}

## 簡介 {#introduction}

CRX2Oak工具專為在不同存放庫之間移轉資料而設計。

它可用來將資料從以前根據Apache Jackrabbit 2的CQ版本移轉至Oak，也可用來在Oak存放庫之間複製資料。

您可以從以下位置的公用Adobe存放庫下載最新版的crx2oak:
[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

最新版本的變更和修正清單位於[CRX2Oak發行說明](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/crx2oak.html)中。

>[!NOTE]
>
>如需Apache Oak和AEM永續性重要概念的詳細資訊，請參閱[AEM Platform簡介](/help/sites-deploying/platform.md)。

## 遷移使用案例{#migration-use-cases}

此工具可用於：

* 從舊版CQ 5移轉至AEM 6
* 在多個Oak存放庫之間複製資料
* 在不同Oak MicroKernel實作之間轉換資料。

支援使用外部Blob儲存區（通常稱為資料儲存區）來移轉存放庫，這是以不同組合提供。 一個可能的移轉路徑是從使用外部`FileDataStore`的CRX2存放庫，移轉至使用`S3DataStore`的Oak存放庫。

下圖說明CRX2Oak支援的所有可能移轉組合：

![chlimage_1-151](assets/chlimage_1-151.png)

## 功能 {#features}

AEM升級期間會呼叫CRX2Oak，使用者可指定預先定義的移轉設定檔，以自動重新配置永續性模式。 這稱為快速入門模式。

您也可以個別執行，以備需要更多自訂項目時使用。 不過，請注意，在此模式中只會變更存放庫，而且需要手動執行AEM的任何其他重新設定。 這稱為獨立模式。

另一點需要注意的是，如果以獨立模式使用預設設定，則只會遷移節點儲存區，而新儲存庫將重新使用舊的二進位儲存。

### 自動快速啟動模式{#automated-quickstart-mode}

自AEM 6.3起，CRX2Oak能夠處理使用者定義的移轉設定檔，這些設定檔可以設定所有可用的移轉選項。 這既提供了更高的靈活性，也提供了自動配置AEM的功能，這些功能在您以獨立模式使用工具時無法使用。

若要將CRX2Oak切換為快速入門模式，您需要透過此作業系統環境變數，定義AEM安裝目錄中crx-quickstart資料夾的路徑：

**對於基於UNIX的系統和macOS:**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**對於Windows:**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### 恢復支援{#resume-support}

移轉可能隨時中斷，之後可繼續。

#### 可自定義升級邏輯{#customizable-upgrade-logic}

自訂Java邏輯，也可使用`CommitHooks`實作。 可以實施自定義`RepositoryInitializer`類，以便使用自定義值初始化儲存庫。

#### 支援記憶體映射操作{#support-for-memory-mapped-operations}

依預設，CRX2Oak也支援記憶體對應作業。 記憶體映射可大幅提升效能，並應盡可能使用。

>[!CAUTION]
>
>但請注意，Windows平台不支援記憶體映射操作。 因此，建議在Windows上執行遷移時添加&#x200B;**—disable-mmap**&#x200B;參數。

#### 內容的選擇性移轉{#selective-migration-of-content}

依預設，工具會在`"/"`路徑下遷移整個儲存庫。 不過，您可以完全控制應移轉的內容。

如果新實例上不需要的內容有任何部分，則可以使用`--exclude-path`參數來排除內容並優化升級過程。

#### 合併路徑{#path-merging}

如果資料需要在兩個儲存庫之間複製，而且您在兩個執行個體上的內容路徑不同，則可以在`--merge-path`參數中定義。 執行此操作後，CRX2Oak只會將新節點複製到目的地存放庫，並保留舊節點。

![chlimage_1-152](assets/chlimage_1-152.png)

#### 版本支援{#version-support}

依預設，AEM會建立經修改的每個節點或頁面的版本，並將其儲存在存放庫中。 然後，可使用這些版本將頁面還原為較舊狀態。

不過，即使刪除原始頁面，這些版本也不會清除。 處理已運行了很長時間的儲存庫時，遷移可能需要處理由孤立版本導致的大量冗餘資料。

對於這些類型的情況，一個有用的功能是添加`--copy-versions`參數。 它可用來在移轉或複製存放庫期間略過版本節點。

您也可以新增`--copy-orphaned-versions=true`來選擇是否複製孤立版本。

這兩個參數也支援`YYYY-MM-DD`日期格式，以備您要在特定日期之前復製版本時使用。

![chlimage_1-153](assets/chlimage_1-153.png)

#### 開放原始碼版本{#open-source-version}

CRX2Oak的開放原始碼版本以oak-upgrade形式提供。 它支援除以下功能之外的所有功能：

* CRX2支援
* 移轉設定檔支援
* 支援自動AEM重新配置

如需詳細資訊，請參閱[Apache檔案](https://jackrabbit.apache.org/oak/docs/migration.html) 。

## 參數 {#parameters}

### 節點儲存選項{#node-store-options}

* `--cache`:快取大小(MB)(預設 `256`為)

* `--mmap`:為區段存放區啟用記憶體對應檔案存取
* `--src-password:` 源RDB資料庫的口令

* `--src-user:` 源RDB的用戶

* `--user`:目標RDB的用戶

* `--password`:目標RDB的密碼。

### 遷移選項{#migration-options}

* `--early-shutdown`:在複製節點和應用提交掛接之前關閉源JCR2儲存庫
* `--fail-on-error`:如果無法從源儲存庫讀取節點，則強制遷移失敗。
* `--ldap`:將LDAP使用者從CQ 5.x執行個體移轉至Oak型執行個體。為了讓此功能發揮作用，Oak設定中的身分提供者必須命名為ldap。 有關詳細資訊，請參閱[LDAP文檔](/help/sites-administering/ldap-config.md)。

* `--ldap-config:` 搭配使用這項功能的 `--ldap` CQ 5.x存放庫參數（使用多個LDAP伺服器進行驗證）。您可以使用它指向CQ 5.x `ldap_login.conf`或`jaas.conf`組態檔。 格式為`--ldapconfig=path/to/ldap_login.conf`。

### 版本儲存選項{#version-store-options}

* `--copy-orphaned-versions`:略過複製孤立的版本。支援的參數包括：`true`、`false`和`yyyy-mm-dd`。 預設為 `true`.

* `--copy-versions:` 復製版本儲存。參數：`true`、`false`、`yyyy-mm-dd`。 預設為 `true`.

#### 路徑選項{#path-options}

* `--include-paths:` 複製期間要包含的路徑清單（以逗號分隔）
* `--merge-paths`:複製期間要合併的路徑清單（以逗號分隔）
* `--exclude-paths:` 複製期間要排除的逗號分隔路徑清單。

### 源Blob儲存選項{#source-blob-store-options}

* `--src-datastore:` 要用作源的資料儲存目錄  `FileDataStore`

* `--src-fileblobstore`:要用作源的資料儲存目錄  `FileBlobStore`

* `--src-s3datastore`:要用於源的資料儲存目錄  `S3DataStore`

* `--src-s3config`:源的配置檔 `S3DataStore`案。

### 目標BlobStore選項{#destination-blobstore-options}

* `--datastore:` 要用作目標的資料儲存目錄  `FileDataStore`

* `--fileblobstore:` 要用作目標的資料儲存目錄  `FileBlobStore`

* `--s3datastore`:用於目標的資料儲存目錄  `S3DataStore`

* `--s3config`:目標的設定檔 `S3DataStore`案。

### 幫助選項{#help-options}

* `-?, -h, --help:` 顯示幫助資訊。

## 除錯 {#debugging}

您也可以為移轉程式啟用除錯資訊，以疑難排解該程式期間可能出現的任何問題。 視您要在中執行工具的模式而定，您可以以不同方式執行此作業：

<table>
 <tbody>
  <tr>
   <td><strong>CRX2Oak模式</strong></td>
   <td><strong>動作</strong></td>
  </tr>
  <tr>
   <td>快速入門模式</td>
   <td>在執行CRX2Oak時，您可以將<strong>—log-levelTRACE</strong>或<strong>—log-level DEBUG </strong>選項新增至命令列。 在此模式中，日誌會自動重定向到<strong>upgrade.log檔案</strong>。</td>
  </tr>
  <tr>
   <td>獨立模式</td>
   <td><p>將<strong>—trace</strong>選項新增至CRX2Oak命令列，以在標準輸出上顯示TRACE事件(您需要使用重新導向字元來重新導向記錄：「&gt;」或「tee」命令，以供以後檢查)。</p> </td>
  </tr>
 </tbody>
</table>

## 其他注意事項{#other-considerations}

遷移到MongoDB複製副本集時，請確保在與Mongo資料庫的所有連接上將`WriteConcern`參數設定為`2`。

您可以在連線字串的結尾新增`w=2`參數，如下所示：

```xml
java -Xmx4092m -XX:MaxPermSize=1024m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>如需詳細資訊，請參閱[寫入關注](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options)上的MongoDB連線字串檔案。
