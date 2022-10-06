---
title: 要備份和恢復的檔案
seo-title: Files to back up and recover
description: 本文檔介紹必須備份的應用程式和資料檔案。
seo-description: This document describes the application and data files that must be backed up.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---

# 要備份和恢復的檔案 {#files-to-back-up-and-recover}

以下各節將詳細說明必須備份的應用程式和資料檔案。

請考慮以下有關備份和恢復的要點：

* 應在GDS和AEM儲存庫之前備份資料庫。
* 如果需要關閉群集環境中的節點進行備份，請確保在主節點之前關閉輔助節點。 否則，可能會導致叢集或伺服器不一致。 此外，主節點應在任何次要節點之前上線。
* 對於群集的還原操作，應停止群集中每個節點的應用程式伺服器。

## 全局文檔儲存目錄 {#global-document-storage-directory}

GDS是一個目錄，用於儲存進程內使用的長期檔案。 長期檔案的存留期可跨越一或多次啟動AEM表單系統，且可跨越數天甚至數年。 這些長期的檔案可以包括PDF、策略和表單模板。 長期檔案是許多AEM表單部署整體狀態的關鍵部分。 如果某些或所有長期文檔丟失或損壞，表單伺服器可能會變得不穩定。

非同步作業調用的輸入文檔也儲存在GDS中，並且必須可用於處理請求。 因此，務必考慮承載GDS並採用獨立磁碟冗餘陣列(RAID)或其他技術的檔案系統的可靠性，以滿足您的服務質量和服務級別要求。

GDS的位置是在AEM表單安裝過程中或更新時使用管理控制台確定的。 除了為GDS保留高可用性位置之外，您還可以為文檔啟用資料庫儲存。 請參閱 [將資料庫用於文檔儲存時的備份選項](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### GDS位置 {#gds-location}

如果在安裝期間將位置設定保留為空，則該位置預設為應用程式伺服器安裝下的目錄。 必須備份應用程式伺服器的以下目錄：

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

如果將GDS位置更改為非預設位置，則可以按如下方式確定：

* 登入管理控制台，然後按一下「設定>核心繫統設定>設定」。
* 記錄在「全局文檔儲存目錄」框中指定的位置。

在群集環境中，GDS通常指向網路上共用的目錄，並且每個群集節點都可讀/寫訪問該目錄。

如果原始位置不再可用，則在恢復期間，GDS的位置可以更改。 (請參閱 [在恢復期間更改GDS位置](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### 將資料庫用於文檔儲存時的備份選項 {#backup-options-when-database-is-used-for-document-storage}

您可以使用管理控制台在AEM表單資料庫中啟用AEM表單檔案儲存。 即使此選項保留資料庫中的所有永久性文檔，AEM表單仍需要基於檔案系統的GDS目錄，因為它用於儲存與AEM表單的會話和調用相關的永久和臨時檔案和資源。

在管理控制台的「核心繫統設定」中或通過使用Configuration Manager選擇「在資料庫中啟用文檔儲存」選項時，AEM表單不允許快照備份模式和滾動備份模式。 因此，您不需要使用AEM表單來管理備份模式。 如果使用此選項，則在啟用該選項後，您應僅備份GDS一次。 從備份中恢復AEM表單時，無需更名GDS或恢復GDS的備份目錄。

## AEM存放庫 {#aem-repository}

如果在安裝AEM表單時設定crx-repository，則會建立AEM存放庫(crx-repository)。 crx-repository目錄的位置是在AEM表單安裝過程中確定的。 AEM存放庫備份和還原需要資料庫和GDS，才能在AEM表單中使用一致的AEM表單資料。 AEM存放庫包含通信管理解決方案、Forms manager和AEM Forms Workspace的資料。

### 通信管理解決方案 {#correspondence-management-solution}

通信管理解決方案可集中處理和管理安全、個人化及互動式通信的建立、組合及傳遞。 它可讓您透過從建立到封存的簡化程式，從預先核准和自訂撰寫的內容，快速組合對應內容。 因此，您的客戶可以及時、準確、方便、安全且相關的通訊。 您的業務通過簡化的流程實現客戶交互的最大價值，並將成本和風險降至最低，以便輕鬆、快速和高效地完成。

簡單的通信管理解決方案設定包含製作執行個體和位於相同電腦或不同電腦上的發佈執行個體

### forms manager {#forms-manager}

forms manager可簡化更新、管理和停用表單的流程。

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace與的功能相符(JEE上的AEM Forms已遭取代)Flex Workspace，並新增了擴充和整合Workspace的新功能，讓其更方便使用。

>[!NOTE]
>
>AEM Forms版本已不再使用Flex Workspace。

它允許在不使用Flash Player和Adobe Reader的客戶端上進行任務管理。 除了PDF forms和Flex表單外，還可促進HTMLForms的轉譯。

## AEM forms資料庫 {#aem-forms-database}

AEM表單資料庫儲存諸如表單對象、服務配置、進程狀態和對GDS和內容儲存根目錄（針對內容服務）中檔案的資料庫引用等內容。 資料庫備份可以即時執行而不中斷服務，並且恢復可以在特定時間點或特定更改。 本節介紹如何配置資料庫，以便即時備份資料庫。

在正確配置的AEM表單系統上，系統管理員和資料庫管理員可以輕鬆協作，將系統恢復到一致的已知狀態。

要即時備份資料庫，必須使用快照模式或配置資料庫以在指定的日誌模式下運行。 這允許在資料庫開啟且可供使用時備份資料庫檔案。 此外，當資料庫以這些模式運行時，資料庫將保留其回滾和事務日誌。

>[!NOTE]
>
>Adobe®LiveCycle® Content Services ES（已過時）是隨LiveCycle安裝的內容管理系統。 它使用戶能夠設計、管理、監控和優化以人為中心的流程。 內容服務（已過時）支援將於12/31/2014終止。 請參閱 [Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

配置DB2資料庫以在歸檔日誌模式下運行。

>[!NOTE]
>
>如果您的AEM表單環境已從舊版AEM表單升級，且使用DB2，則不支援線上備份。 在此情況下，您必須關閉AEM表單並執行離線備份。 未來版本的AEM表單將支援升級客戶的線上備份。

IBM提供一套工具和幫助系統，幫助資料庫管理員管理其備份和恢復任務：

* IBM DB2封存記錄加速器
* IBM DB2資料封存專家

DB2具有將資料庫備份到Tivoli Storage Manager的內置功能。 通過使用Tivoli Storage Manager, DB2備份可以儲存在其他介質或本地硬碟上。

### Oracle {#oracle}

使用快照備份或配置Oracle資料庫以在歸檔日誌模式下運行。 (請參閱 [Oracle備份：簡介](https://www.databasedesign-resource.com/oracle-backup.md).) 有關備份和恢復Oracle資料庫的詳細資訊，請轉至以下站點：

[Oracle備份和恢復：](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) 詳細說明了備份和恢復的概念以及使用Recovery Manager(RMAN)進行備份、恢復和報告的最常見技術，並提供了有關如何規劃備份和恢復策略的詳細資訊。

[《oracle資料庫備份和恢復使用手冊》：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) 提供有關RMAN體系結構、備份和恢復概念和機制、高級恢復技術（如時間點恢復和資料庫閃回功能）以及備份和恢復效能調整的深入資訊。 它還包括用戶管理的備份和恢復，使用主機作業系統設施，而不是RMAN。 此卷對於備份和恢復更複雜的資料庫部署以及高級恢複方案至關重要。

[Oracle資料庫備份和恢復參考：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 提供有關所有RMAN命令的語法和語義的完整資訊，並描述可用於報告備份和恢復活動的資料庫視圖。

### SQL Server {#sql-server}

使用快照備份或配置SQL Server資料庫以在事務日誌模式下運行。

SQL Server還提供了兩種備份和恢復工具：

* SQL Server Management Studio(GUI)
* T-SQL（命令行）

如需詳細資訊，請參閱 [備份和還原](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

使用MySQLAdmin或在Windows中修改INI檔案，以配置MySQL資料庫以二進位日誌模式運行。 (請參閱 [MySQL二進位日誌記錄](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) InnoBase軟體還提供了MySQL的熱備份工具。 (請參閱 [Innobase熱備份](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
>MySQL的預設二進位記錄模式為「語句」，與Content Services使用的表不相容（已廢止）。 在此預設模式下使用二進位記錄會導致內容服務（已過時）失敗。 如果您的系統包含內容服務（已淘汰），請使用「混合」記錄模式。 若要啟用「混合」記錄，請將下列引數新增至my.ini檔案： `binlog_format=mixed log-bin=logname`

您可以使用mysqldump實用程式獲取完整資料庫備份。 需要完整備份，但並不總是方便。 它們會生成大型備份檔案，並需要時間才能生成。 要執行增量備份，請確保使用啟動伺服器的 —  `log-bin` 選項，如前一節所述。 每次MySQL伺服器重新啟動時，它都停止寫入當前的二進位日誌，建立新的日誌，然後，新的日誌就變成當前日誌。 您可以手動強制切換，使用 `FLUSH LOGS SQL` 命令。 在第一次完全備份後，使用mysqladmin實用程式和 `flush-logs` 命令，該命令將建立下一個日誌檔案。

請參閱 [備份策略摘要](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## 內容儲存根目錄（僅限內容服務） {#content-storage-root-directory-content-services-only}

內容儲存根目錄包含內容服務（已過時）儲存庫，儲存所有文檔、對象和索引。 必須備份內容儲存根目錄樹。 本節介紹如何為獨立環境和群集環境確定內容儲存根目錄的位置。

### 內容儲存根位置（獨立環境） {#content-storage-root-location-stand-alone-environment}

安裝內容服務（已過時）時會建立內容儲存根目錄。 在AEM表單安裝過程中確定內容儲存根目錄的位置。

內容儲存根目錄的預設位置為 `[aem-forms root]/lccs_data`.

備份位於「內容儲存根目錄」中的以下目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，該目錄也位於內容儲存根目錄中。 如果/backup-lucene-indexes目錄存在，則不要備份/lucene-indexes目錄，因為它可能會導致錯誤。

### 內容儲存根位置（群集環境） {#content-storage-root-location-clustered-environment}

在群集環境中安裝Content Services（已過時）時，內容儲存根目錄將拆分為兩個不同的目錄：

**內容儲存根目錄：** 通常是可對群集中的所有節點讀/寫訪問的共用網路目錄

**索引根目錄：** 在群集中每個節點上建立的目錄，始終具有相同的路徑和目錄名

內容儲存根目錄的預設位置為 `[GDS root]/lccs_data`，其中 `[GDS root]` 是 [GDS位置](files-back-recover.md#gds-location). 備份位於「內容儲存根目錄」中的以下目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，該目錄也位於內容儲存根目錄中。 如果/backup-lucene-indexes目錄存在，則不要備份/lucene-indexes目錄，因為它可能會導致錯誤。

索引根目錄的預設位置為 `[aem-forms root]/lucene-indexes` 在每個節點上。

## 客戶安裝的字型 {#customer-installed-fonts}

如果您在AEM表單環境中安裝了其他字型，則必須分別進行備份。 備份在管理控制台中「設定>核心繫統>配置」下指定的所有Adobe和客戶字型目錄。 確保備份整個字型目錄。

>[!NOTE]
>
>依預設，隨AEM表單安裝的Adobe字型位於 `[aem-forms root]/fonts` 目錄。

如果要重新初始化主機上的作業系統，並且要使用以前作業系統的字型，則還應備份系統字型目錄的內容。 （如需具體指示，請參閱作業系統的檔案）。
