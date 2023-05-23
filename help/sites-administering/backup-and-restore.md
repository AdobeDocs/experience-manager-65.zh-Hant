---
title: 備份和還原
seo-title: Backup and Restore
description: 瞭解如何備份和還原您的AEM內容。
seo-description: Learn how to backup and restore your AEM content.
uuid: 446a466f-f508-4430-9e50-42cd4463760e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: eb8bbb85-ca2f-4877-8ee0-bb1ee8b7d8de
exl-id: dd26dade-b769-483e-bc11-dcfa5ed1f87e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 0%

---

# 備份和還原{#backup-and-restore}

在中備份和恢復儲存庫內容有兩種方AEM法：

* 您可以建立儲存庫的外部備份並將其儲存在安全位置。 如果儲存庫出現故障，您可以將其恢復到以前的狀態。
* 您可以建立儲存庫內容的內部版本。 這些版本與內容一起儲存在儲存庫中，因此您可以快速恢復已更改或刪除的節點和樹。

## 一般 {#general}

此處介紹的方法適用於系統備份和恢復。

如果您需要備份和恢復丟失的少量內容，則不一定需要恢復系統：

* 您可以通過包從另一個系統獲取資料
* 或者，在臨時系統上恢復備份，建立內容包並在缺少此內容的系統上部署它。

有關詳細資訊，請參閱 [包備份](/help/sites-administering/backup-and-restore.md#package-backup) 下。

## 計時 {#timing}

不要與資料儲存垃圾收集並行運行備份，因為這可能會損害兩個進程的結果。

## 離線備份 {#offline-backup}

您始終可以執行離線備份。 這需要停機時間AEM，但與線上備份相比，在所需時間方面可以非常高效。

在大多數情況下，您將使用檔案系統快照在此時建立儲存的只讀副本。 要建立離線備份，請執行以下步驟：

* 停止應用程式
* 建立快照備份
* 啟動應用程式

由於快照備份通常只需幾秒鐘，因此整個停機時間不到幾分鐘。

## 線上備份 {#online-backup}

此備份方法建立整個儲存庫的備份，包括其下部署的任何應用程式，AEM如。 備份包括內容、版本歷史記錄、配置、軟體、修補程式、自定義應用程式、日誌檔案、搜索索引等。 如果正在使用群集且共用資料夾是 `crx-quickstart` （物理或使用軟連結），也會備份共用目錄。

您可以在以後恢復整個儲存庫（和任何應用程式）。

此方法作為「熱」或「線上」備份運行，因此可以在儲存庫運行時執行。 因此，在備份運行時，儲存庫是可用的。 此方法適用於預設的基於Tar儲存的儲存庫實例。

建立備份時，您有以下選項：

* 使用整合備份工具備AEM份到目錄。
* 使用檔案系統快照備份到目錄

在任何情況下，備份都會建立儲存庫的映像（或快照）。 然後，系統備份代理應該注意將此映像實際傳輸到專用備份系統（磁帶機）。

>[!NOTE]
>
>如AEM果在具有自定義Blobstore配置的AEM實例上使用了聯機備份功能，則建議將資料儲存的路徑配置為位於「 」之外 `crx-quickstart`»目錄，並分別備份資料儲存。

>[!CAUTION]
>
>聯機備份僅備份檔案系統。 如果將儲存庫內容和/或儲存庫檔案儲存在資料庫中，則需要單獨備份該資料庫。 如果正在與AEMMongoDB一起使用，請參閱有關如何使用 [MongoDB本機備份工具](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/)。

### 聯AEM機備份 {#aem-online-backup}

儲存庫的聯機備份允許您建立、下載和刪除備份檔案。 它是「熱」或「線上」備份功能，因此可以在儲存庫正常以讀寫模式使用時執行。

>[!CAUTION]
>
>不同AEM時運行聯機備份 [資料儲存垃圾收集](/help/sites-administering/data-store-garbage-collection.md) 或 [修訂版清除](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)。 它將對系統效能產生負面影響。

啟動備份時，可以指定 **目標路徑** 和/或 **延遲**。

**目標路徑** 備份檔案通常保存在存放快速啟動jar檔案(.jar)的資料夾的父資料夾中。 例如，如果您的jar文AEM件位於/InstallationKits/AEM下，則備份將在/InstallationKits下生成。 也可以指定目標到您選擇的位置。

如果 **目標路徑** 是目錄，儲存庫的映像是在此目錄中建立的。 如果同一目錄多次（或始終）用於儲存備份，

* 在TargetPath中相應修改儲存庫中修改的檔案
* 刪除的儲存庫中的檔案將在TargetPath中刪除
* 在儲存庫中建立的檔案是在TargetPath中建立的

>[!NOTE]
>
>如果 **目標路徑** 設定為副檔名為的檔案名 **.zip**，將儲存庫備份到臨時目錄，然後壓縮此臨時目錄的內容並將其儲存在ZIP檔案中。
>
>這種方法是不鼓勵的，因為
>
>* 在備份過程中需要額外的磁碟儲存（臨時目錄加zip檔案）
>* 壓縮過程由儲存庫完成，並可能影響其效能。
>* 它延遲了備份過程。
>* Java 1.6 Java最多只能建立4 GB大小的ZIP檔案。
>
>如果需要建立ZIP作為備份格式，則應備份到目錄，然後使用壓縮程式建立ZIP檔案。

**延遲** 指示時間延遲（以毫秒為單位），以便不影響儲存庫效能。 預設情況下，儲存庫備份以全速運行。 您可以減慢建立線上備份的速度，以便不會減慢其他任務的速度。

使用非常大的延遲時，請確保線上備份不超過24小時。 如果備份了，請放棄此備份，因為它可能不包含所有二進位檔案。
1毫秒的延遲通常導致10%的CPU使用率，而10毫秒的延遲通常導致3%的CPU使用率。 總延遲（秒）可估計如下：儲存庫大小(MB)，乘以延遲（毫秒），除以2（如果使用zip選項），或除以4（備份到目錄時）。 這意味著備份到200 MB儲存庫的目錄時延遲1毫秒，備份時間將增加大約50秒。

>[!NOTE]
>
>請參閱 [聯機AEM備份的工作原理](#how-aem-online-backup-works) 的子菜單。

要建立備份：

1. 以管理員身AEM份登錄。

1. 轉到 **工具 — 操作 — 備份。**
1. 按一下&#x200B;**建立**。將開啟備份控制台。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. 在備份控制台上，指定 **[目標路徑](#aem-online-backup)** 和 **[延遲](#aem-online-backup)**。

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >備份控制台也可使用：
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. 按一下 **保存**，進度欄將指示備份進度。

   >[!NOTE]
   >
   >你可以 **取消** 隨時運行備份。

1. 備份完成後，zip檔案將列在備份窗口中。

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >可以使用控制台刪除不再需要的備份檔案。 在左窗格中選擇備份檔案，然後按一下 **刪除**。

   >[!NOTE]
   >
   >如果已備份到目錄：備份過程完成後AEM將不寫入目標目錄。

### 自AEM動線上備份 {#automating-aem-online-backup}

如果可能，應在系統負載很小時運行線上備份，例如在早晨。

使用 `wget` 或 `curl` HTTP客戶端。 下面顯示了如何使用curl自動備份的示例。

#### 備份到預設目標目錄 {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>在以下示例中， `curl` 可能需要為實例配置命令；例如，主機名( `localhost`)，埠( `4502`)，管理密碼( `xyz`)和檔案名( `backup.zip`)。

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

備份檔案/目錄是在伺服器上建立的，位於包含 `crx-quickstart` 資料夾（與使用瀏覽器建立備份時相同）。 例如，如果已在AEM目錄中安裝 `/InstallationKits/crx-quickstart/`，然後在 `/InstallationKits` 的子菜單。

curl命令會立即返回，因此您必須監視此目錄，以查看zip檔案準備好的時間。 在建立備份時，可以看到臨時目錄（其名稱基於最終zip檔案的名稱），最後將壓縮該目錄。 例如：

* 生成的zip檔案的名稱： `backup.zip`
* 臨時目錄的名稱： `backup.f4d5.temp`

#### 備份到非預設目標目錄 {#backing-up-to-a-non-default-target-directory}

通常，備份檔案/目錄是在包含以下內容的資料夾的父資料夾中的伺服器上建立的 `crx-quickstart` 的子菜單。

如果要將備份（按任意排序）保存到其他位置，可以將絕對路徑「」設定為 `target` 參數 `curl` 的子菜單。

例如，要生成 `backupJune.zip` 目錄中的 `/Backups/2012`:

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>使用其他應用程式伺服器（如JBoss）時，聯機備份可能無法按預期工作，因為目標目錄不可寫。 在這種情況下，請與支援部門聯繫。

>[!NOTE]
>
>還可以觸發備份 [使用由提供的MBean AEM](/help/sites-administering/jmx-console.md)。

### 檔案系統快照備份 {#filesystem-snapshot-backup}

此處描述的過程特別適合於大型儲存庫。

>[!NOTE]
>
>如果要使用此備份方法，則系統必須支援檔案系統快照。 例如，對於Linux，這意味著您的檔案系統應放在邏輯卷上。

1. 是否部署了檔案系AEM統的快照。

1. 裝載檔案系統快照。
1. 執行備份並卸載快照。

### 聯機AEM備份的工作原理 {#how-aem-online-backup-works}

聯AEM機備份由一系列內部操作組成，以確保正在備份的資料和正在建立的備份檔案的完整性。 下面列出了感興趣的人。

聯機備份使用以下算法：

1. 建立zip檔案時，第一步是建立或查找目標目錄。

   * 如果備份到zip檔案，則會建立臨時目錄。 目錄名稱以開頭 `backup.` 結尾 `.temp`;例如 `backup.f4d3.temp`。
   * 如果備份到目錄，則使用在目標路徑中指定的名稱。 可以使用現有目錄，否則將建立新目錄。

      名為的空檔案 `backupInProgress.txt` 在目標目錄中建立。 備份完成後，將刪除此檔案。

1. 檔案將從源目錄複製到目標目錄（或建立zip檔案時的臨時目錄）。 在資料儲存之前複製段儲存，以避免儲存庫損壞。 建立備份時，將省略索引和快取資料。 因此，來自 `crx-quickstart/repository/cache` 和 `crx-quickstart/repository/index` 不包括在備份中。 建立zip檔案時，進程進度條指示符介於0% - 70%之間；如果未建立zip檔案，則顯示0% - 100%。

1. 如果備份到預先存在的目錄，則目標目錄中的「舊」檔案將被刪除。 舊檔案是源目錄中不存在的檔案。

檔案將分四個階段複製到目標目錄：

1. 在第一個複製階段（建立zip檔案時的進度指示器0% - 63%，如果沒有建立zip檔案時的進度指示器0% - 90%），在儲存庫正常運行時複製所有檔案。 該過程分為兩個階段：

   * 階段A — 除資料儲存（延遲）外，所有內容都被複製。
   * 階段B — 僅複製資料儲存（帶延遲）。

1. 在第二個複製階段（建立zip檔案時進度指示器為63% - 65.8%，如果沒有建立zip檔案時為90% - 94%），僅複製自第一個複製階段啟動後在源目錄中建立或修改的檔案。 根據儲存庫的活動，這種範圍可能從根本沒有檔案到大量檔案（因為第一個檔案複製階段通常需要很長時間）。 複製過程與第一階段（帶延遲的階段A和階段B）類似。
1. 在第三個複製階段（建立zip檔案時進度指示器65.8% - 68.6%，如果沒有建立zip檔案時進度指示器94% - 98%），僅複製自啟動第二個複製階段以來在源目錄中建立或修改的檔案。 根據儲存庫的活動，可能沒有要複製的檔案，或者檔案數量非常少（因為第二個檔案複製階段通常速度很快）。 複製過程與第二階段類似 — 階段A和階段B，但無延遲。
1. 檔案複製階段一到三個在儲存庫運行時同時完成。 僅複製自啟動第三個複製階段後在源目錄中建立或修改的檔案。 根據儲存庫的活動，可能沒有要複製的檔案，或者只有非常、非常少的檔案（因為第二個檔案複製階段通常非常快）。 建立zip檔案時進度指標為68.6% - 70%；如果未建立zip檔案，則進度指標為98% - 100%。 複製過程與第三階段類似。
1. 根據目標：

   * 如果指定了zip檔案，則現在將從臨時目錄建立該檔案。 進展指標70%-100%。 然後刪除臨時目錄。
   * 如果目標是目錄，則名為 `backupInProgress.txt` 刪除以指示備份已完成。

## 恢復備份 {#restoring-the-backup}

可以按如下方式恢復備份：

* 在執行檔案系統快照備份時，只需恢復系統的映像即可。
* 如果將備份建立為zip檔案，只需解壓縮新資料夾中的內容，然後從該位AEM置開始即可。

## 包備份 {#package-backup}

要備份和還原內容，可以使用「包管理器」之一，該管理器使用「內容包」格式來備份和恢復內容。 「包管理器」在定義和管理包方面提供了更大的靈活性。

有關這些單獨內容包格式的功能和權衡的詳細資訊，請參見 [如何使用包](/help/sites-administering/package-manager.md)。

### 備份範圍 {#scope-of-backup}

使用「包管理器」或「內容拉鍊」備份節點時，CRX會保存以下資訊：

* 所選樹下的儲存庫內容。
* 用於備份內容的節點類型定義。
* 用於備份內容的命名空間定義。

備份時，將AEM丟失以下資訊：

* 版本歷史記錄。
