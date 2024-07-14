---
title: 使用CRX2Oak移轉工具
description: 瞭解如何將CRX2Oak移轉工具與Adobe Experience Manager搭配使用。 此工具旨在協助您在不同的存放庫之間移轉資料。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# 使用CRX2Oak移轉工具{#using-the-crx-oak-migration-tool}

## 簡介 {#introduction}

CRX2Oak工具專為在不同存放庫之間移轉資料而設計。

它可用來將資料從以Apache Jackrabbit 2為基礎的舊CQ版本移轉至Oak，也可用來在Oak存放庫之間複製資料。

您可以從公共Adobe存放庫下載最新版本的crx2oak，網址為：
[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

>[!NOTE]
>
>如需Apache Oak和Adobe Experience Manager (AEM)持續性的重要概念的詳細資訊，請參閱[AEM平台簡介](/help/sites-deploying/platform.md)。

## 移轉使用案例 {#migration-use-cases}

此工具可用於：

* 從較舊的CQ 5版本移轉至AEM 6
* 在多個Oak存放庫之間複製資料
* 在不同的Oak MicroKernel實作之間轉換資料。

對於使用外部Blob存放區（通常稱為資料存放區）移轉存放庫的支援，以不同的組合提供。 一個可能的移轉路徑是從使用外部`FileDataStore`的CRX2存放庫，移轉至使用`S3DataStore`的Oak存放庫。

下圖說明CRX2Oak支援的所有可能移轉組合：

![chlimage_1-151](assets/chlimage_1-151.png)

## 功能 {#features}

在AEM升級期間以使用者可以指定預先定義的移轉設定檔的方式來呼叫CRX2Oak，以自動重新設定持續性模式。 這稱為快速入門模式。

它也可以單獨執行，以備需要更多自訂時使用。 不過，在此模式中，僅會對存放庫進行變更，而且必須手動執行AEM的任何其他重新配置。 這稱為獨立模式。

另外請注意，使用獨立模式中的預設設定，只會移轉節點存放區，而新的存放庫會重複使用舊的二進位存放區。

### 自動快速入門模式 {#automated-quickstart-mode}

自AEM 6.3起，CRX2Oak就能夠處理使用者定義的移轉設定檔，這些設定檔可設定為可用的所有移轉選項。 這樣可擁有更高的彈性和自動設定AEM的能力，而如果您在獨立模式下使用工具，則無法使用這些功能。

若要將CRX2Oak切換為快速入門模式，請透過此作業系統環境變數，在AEM安裝目錄中定義crx-quickstart資料夾的路徑：

**對於UNIX系統和macOS：**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

適用於Windows的&#x200B;**：**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### 繼續支援 {#resume-support}

移轉作業可隨時中斷，之後可繼續進行。

#### 可自訂的升級邏輯 {#customizable-upgrade-logic}

可使用`CommitHooks`實作自訂Java™邏輯。 可以實作自訂`RepositoryInitializer`類別，以使用自訂值初始化存放庫。

#### 支援記憶體對應作業 {#support-for-memory-mapped-operations}

依預設，CRX2Oak也支援記憶體對應作業。 記憶體對應可大幅提升效能，應儘可能使用。

>[!CAUTION]
>
>但是請注意，Windows平台不支援記憶體對應作業。 因此，建議在Windows上執行移轉時新增&#x200B;**—disable-mmap**&#x200B;引數。

#### 選擇性移轉內容 {#selective-migration-of-content}

依預設，工具會移轉`"/"`路徑下的整個存放庫。 不過，您可以完全控制應該移轉哪些內容。

如果新執行個體上有不需要的內容的任何部分，您可以使用`--exclude-path`引數來排除內容並最佳化升級程式。

#### 路徑合併 {#path-merging}

如果資料必須在兩個存放庫之間複製，且您的內容路徑在兩個執行個體上不同，您可以在`--merge-path`引數中定義它。 當您這樣做時，CRX2Oak只會將新節點複製到目的地存放庫，並保持舊節點不變。

![chlimage_1-152](assets/chlimage_1-152.png)

#### 版本支援 {#version-support}

依預設，AEM會為每個要修改的節點或頁面建立版本，並將其儲存在存放庫中。 然後可以使用版本將頁面還原成先前的狀態。

不過，即使刪除原始頁面，系統也不會清除這些版本。 處理已運作很久的存放庫時，移轉可能會重新處理孤立版本所導致的冗餘資料。

對於這些型別的情況，有用的功能是加上`--copy-versions`引數。 它可用來在移轉期間略過版本節點或複製存放庫。

您也可以透過新增`--copy-orphaned-versions=true`來選擇是否要複製孤立的版本。

這兩個引數也支援`YYYY-MM-DD`日期格式，以備您不遲於特定日期復製版本時使用。

![chlimage_1-153](assets/chlimage_1-153.png)

#### 開啟Source版本 {#open-source-version}

CRX2Oak的開放原始碼版本可透過Oak-upgrade取得。 支援所有功能，但以下功能除外：

* CRX2支援
* 移轉設定檔支援
* 支援自動化AEM重新配置

如需詳細資訊，請參閱[Apache檔案](https://jackrabbit.apache.org/oak/docs/migration.html)。

## 參數 {#parameters}

### 節點存放區選項 {#node-store-options}

* `--cache`：快取大小（以MB為單位，預設為`256`）

* `--mmap`：啟用區段存放區的記憶體對應檔案存取
* 來源RDB資料庫的`--src-password:`密碼

* 來源RDB的`--src-user:`位使用者

* `--user`：目標資料庫的使用者

* `--password`：目標RDB密碼。

### 移轉選項 {#migration-options}

* `--early-shutdown`：在複製節點之後和套用認可掛接之前關閉來源JCR2存放庫
* `--fail-on-error`：如果無法從來源存放庫讀取節點，強制移轉失敗。
* `--ldap`：將LDAP使用者從CQ 5.x執行個體移轉至Oak型執行個體。 為了讓此功能發揮作用，Oak設定中的身分提供者必須命名為ldap。 如需詳細資訊，請參閱[LDAP檔案](/help/sites-administering/ldap-config.md)。

* `--ldap-config:`將此用於使用多個LDAP伺服器驗證的CQ 5.x存放庫的`--ldap`引數。 您可以使用它指向CQ 5.x `ldap_login.conf`或`jaas.conf`組態檔。 格式為`--ldapconfig=path/to/ldap_login.conf`。

### 版本存放區選項 {#version-store-options}

* `--copy-orphaned-versions`：略過複製孤立的版本。 支援的引數有： `true`、`false`和`yyyy-mm-dd`。 預設為`true`。

* `--copy-versions:`復製版本儲存體。 引數： `true`、`false`、`yyyy-mm-dd`。 預設為`true`。

#### 路徑選項 {#path-options}

* `--include-paths:`複製期間要包含的以逗號分隔的路徑清單
* `--merge-paths`：複製期間要合併的逗號分隔路徑清單
* `--exclude-paths:`複製期間要排除的逗號分隔路徑清單。

### Source Blob存放區選項 {#source-blob-store-options}

* `--src-datastore:`要做為來源`FileDataStore`的資料存放區目錄

* `--src-fileblobstore`：要做為來源`FileBlobStore`的資料存放區目錄

* `--src-s3datastore`：要用於來源`S3DataStore`的資料存放區目錄

* `--src-s3config`：來源`S3DataStore`的組態檔。

### 目的地BlobStore選項 {#destination-blobstore-options}

* `--datastore:`要當作目標`FileDataStore`使用的資料存放區目錄

* `--fileblobstore:`要當作目標`FileBlobStore`使用的資料存放區目錄

* `--s3datastore`：要用於目標`S3DataStore`的資料存放區目錄

* `--s3config`：目標`S3DataStore`的組態檔。

### 說明選項 {#help-options}

* `-?, -h, --help:`顯示說明資訊。

## 偵錯 {#debugging}

您也可以啟用移轉程式的偵錯資訊，以疑難排解程式期間可能出現的任何問題。 您可以根據您想要在其中執行工具的模式，以不同方式執行此操作：

<table>
 <tbody>
  <tr>
   <td><strong>CRX2Oak模式</strong></td>
   <td><strong>動作</strong></td>
  </tr>
  <tr>
   <td>快速入門模式</td>
   <td>執行CRX2Oak時，您可以將<strong> — 記錄層級TRACE</strong>或<strong> — 記錄層級DEBUG </strong>選項新增至命令列。 在此模式中，記錄檔會自動重新導向至<strong>upgrade.log檔案</strong>。</td>
  </tr>
  <tr>
   <td>獨立模式</td>
   <td><p>將<strong>—trace</strong>選項新增至CRX2Oak命令列，以便您在標準輸出上顯示TRACE事件（您必須使用重新導向字元： '&gt;'或'tee'命令自行重新導向記錄，以供稍後檢查）。</p> </td>
  </tr>
 </tbody>
</table>

## 其他考量 {#other-considerations}

移轉至MongoDB復本集時，請務必將Mongo資料庫的所有連線上的`WriteConcern`引數設為`2`。

您可以在連線字串的結尾新增`w=2`引數，如下所示：

```xml
java -Xmx4092m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>如需詳細資訊，請參閱[寫入問題](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options)上的MongoDB連線字串檔案。
