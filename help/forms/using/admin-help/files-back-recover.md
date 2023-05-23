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

以下各節將詳細介紹必須備份的應用程式和資料檔案。

請考慮以下有關備份和恢復的要點：

* 應在GDS和儲存庫之前備份數AEM據庫。
* 如果需要關閉群集環境中的節點進行備份，請確保在主節點之前關閉輔助節點。 否則，會導致群集或伺服器不一致。 此外，主節點應在任何輔助節點之前處於活動狀態。
* 對於群集的還原操作，應停止群集中每個節點的應用程式伺服器。

## 全局文檔儲存目錄 {#global-document-storage-directory}

GDS是用於儲存進程內使用的長壽命檔案的目錄。 長壽命檔案的生命週期用於跨一個或多個表單系統AEM的啟動，並可跨數天甚至數年。 這些長期存在的檔案可以包括PDF、策略和表單模板。 長期檔案是多種形式部署的整體狀態中的AEM關鍵部分。 如果某些或所有長期文檔丟失或損壞，表單伺服器可能會變得不穩定。

非同步作業調用的輸入文檔也儲存在GDS中，並且必須可用於處理請求。 因此，必須考慮承載GDS並採用獨立磁碟冗餘陣列(RAID)或其他技術的檔案系統的可靠性，以滿足您的服務質量和服務級別要求。

GDS的位置是在表單安裝過程中或更AEM後使用管理控制台確定的。 除了為GDS保留高可用性位置外，您還可以為文檔啟用資料庫儲存。 請參閱 [將資料庫用於文檔儲存時的備份選項](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)。

### GDS位置 {#gds-location}

如果在安裝期間將位置設定留空，則該位置預設為應用程式伺服器安裝下的目錄。 必須備份應用程式伺服器的以下目錄：

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

如果將GDS位置更改為非預設位置，則可以按如下方式確定：

* 登錄到管理控制台，然後按一下「設定」>「核心繫統設定」>「配置」。
* 記錄在「全局文檔儲存目錄」框中指定的位置。

在群集環境中， GDS通常指向網路上共用的目錄，並且每個群集節點都可讀/寫訪問該目錄。

如果原始位置不再可用，則在恢復期間可更改GDS的位置。 (請參閱 [在恢復期間更改GDS位置](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。)

### 將資料庫用於文檔儲存時的備份選項 {#backup-options-when-database-is-used-for-document-storage}

可以使用AEM管理控制台在表單數AEM據庫中啟用表單文檔儲存。 儘管此選項將資料庫中的所有持久性文檔保AEM留下來，但表單仍需要基於檔案系統的GDS目錄，因為它用於儲存與表單會話和調用相關的永久和臨時文AEM件和資源。

在管理控制台的核心繫統設定中或通過使用Configuration Manager選擇「在資料庫中啟用文檔儲存」選項時AEM，表單不允許快照備份模式和滾動備份模式。 因此，您不需要使用表單管理備份AEM模式。 如果使用此選項，則在啟用該選項後應僅備份一次GDS。 從備AEM份中恢復表單時，無需更名GDS或恢復GDS的備份目錄。

## AEM儲存庫 {#aem-repository}

如AEM果在安裝表單時配置了crx-repository ，則會建立儲存庫(crx-repository)AEM。 crx-repository目錄的位置是在表單安裝過程AEM中確定的。 要AEM在表單中實現一致的表單資料，需要儲存庫AEM備份和恢AEM復。 儲存AEM庫包含Tergement Management Solution、Forms經理和AEM FormsWorkspace的資料。

### 通信管理解決方案 {#correspondence-management-solution}

通信管理解決方案集中並管理安全、個性化和互動式通信的建立、裝配和交付。 它使您能夠在從建立到存檔的簡化流程中從預先批准的內容和自定義創作的內容快速匯集通信。 因此，您的客戶可以及時、準確、方便、安全且相關的通信。 您的業務通過簡化的流程實現客戶交互的最大價值，並最大限度地降低成本和風險，從而實現輕鬆、快速和生產效率。

簡單的「通信管理解決方案」設定包括作者實例和發佈實例，它們位於同一台電腦上或不同電腦上

### 表單管理器 {#forms-manager}

forms manager簡化了更新、管理和註銷表單的過程。

### AEM Forms工作區 {#html-workspace}

AEM Forms工作區與(JEE上的表單已棄用AEM)Flex工作區的功能相匹配，並添加了擴展和整合Workspace的新功能，使其更易於用戶使用。

>[!NOTE]
>
>不建議使用Flex工AEM作空間。

它允許在沒有Flash Player和Adobe Reader的客戶端上執行任務管理。 它除了PDF forms和Flex表格外，還方便了HTMLForms的引渡。

## 表AEM單資料庫 {#aem-forms-database}

表單數AEM據庫儲存對GDS和內容儲存根目錄（用於Content Services）中檔案的檔案的內容，如表單對象、服務配置、進程狀態和資料庫引用。 資料庫備份可以即時執行，而不會中斷服務，恢復可以到特定時間點或特定更改。 本節介紹如何配置資料庫以便能夠即時備份它。

在正確配置AEM的表單系統上，系統管理員和資料庫管理員可以輕鬆協作，將系統恢復到一致的已知狀態。

要即時備份資料庫，必須使用快照模式或配置資料庫以指定的日誌模式運行。 這允許在資料庫開啟且可用時備份資料庫檔案。 此外，當資料庫在這些模式下運行時，它會保留其回滾和事務日誌。

>[!NOTE]
>
>Adobe®LiveCycle®內容服務ES（已棄用）是安裝有LiveCycle的內容管理系統。 它使用戶能夠設計、管理、監控和優化以人為中心的流程。 Content Services（已棄用）支援在12/31/2014結束。 請參閱 [Adobe產品生命週期文檔](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。

### DB2 {#db2}

將DB2資料庫配置為以存檔日誌模式運行。

>[!NOTE]
>
>如AEM果您的表單環境是從以前版本的表AEM單升級並使用DB2，則不支援聯機備份。 在這種情況下，必須關閉表AEM單並執行離線備份。 未來版本AEM的表單將支援升級客戶的線上備份。

IBM有一套工具和幫助系統來幫助資料庫管理員管理其備份和恢復任務：

* IBMDB2歸檔日誌加速器
* IBMDB2資料存檔專家

DB2具有將資料庫備份到Tivoli Storage Manager的內置功能。 使用Tivoli Storage Manager , DB2備份可以儲存在其他介質或本地硬碟上。

### Oracle {#oracle}

使用快照備份或配置Oracle資料庫以在存檔日誌模式下運行。 (請參閱 [Oracle備份：簡介](https://www.databasedesign-resource.com/oracle-backup.md)。) 有關備份和恢復Oracle資料庫的詳細資訊，請轉到以下站點：

[Oracle備份和恢復：](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) 更詳細地解釋備份和恢復的概念以及使用Recovery Manager(RMAN)進行備份、恢復和報告的最常用技術，並提供有關如何規劃備份和恢復策略的更多資訊。

[Oracle資料庫備份和恢復使用手冊：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) 提供了有關RMAN體系結構、備份和恢復概念和機制、高級恢復技術（如時間點恢復和資料庫閃回功能）以及備份和恢復效能調整的深入資訊。 它還包括使用主機作業系統設施（而不是RMAN）進行用戶管理的備份和恢復。 此卷對於備份和恢復更複雜的資料庫部署以及高級恢複方案至關重要。

[Oracle資料庫備份和恢復參考：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 提供有關所有RMAN命令的語法和語義的完整資訊，並介紹可用於報告備份和恢復活動的資料庫視圖。

### SQL Server {#sql-server}

使用快照備份或將SQL Server資料庫配置為在事務日誌模式下運行。

SQL Server還提供了兩種備份和恢復工具：

* SQL Server Management Studio(GUI)
* T-SQL（命令行）

有關詳細資訊，請參見 [備份和恢復](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)。

### MySQL {#mysql}

使用MySQLAdmin或修改Windows中的INI檔案，以配置MySQL資料庫以二進位日誌模式運行。 (請參閱 [MySQL二進位日誌](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)。) InnoBase軟體也提供了MySQL的熱備份工具。 (請參閱 [Innobase熱備份](https://www.innodb.com/hot-backup/features.md)。)

>[!NOTE]
>
>MySQL的預設二進位日誌記錄模式是「語句」，它與Content Services使用的表（已棄用）不相容。 在此預設模式下使用二進位日誌會導致Content Services（已棄用）失敗。 如果您的系統包括Content Services（已棄用），請使用「混合」日誌記錄模式。 要啟用「混合」日誌記錄，請將以下參數添加到my.ini檔案： `binlog_format=mixed log-bin=logname`

可以使用mysqldump實用程式獲取完整資料庫備份。 需要完整備份，但並不總是方便。 它們會生成大型備份檔案，並且需要時間來生成。 要執行增量備份，請確保使用 —  `log-bin` 選項。 每次MySQL伺服器重新啟動時，它都停止寫入當前二進位日誌，建立一個新日誌，然後，新日誌從此變為當前日誌。 您可以手動強制交換機 `FLUSH LOGS SQL` 的子菜單。 在第一次完全備份後，使用mysqladmin實用程式和 `flush-logs` 命令，建立下一個日誌檔案。

請參閱 [備份策略摘要](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)。

```text
binlog_format=mixed
log-bin=logname
```

## 內容儲存根目錄（僅限Content Services） {#content-storage-root-directory-content-services-only}

內容儲存根目錄包含儲存所有文檔、對象和索引的內容服務（已棄用）儲存庫。 必須備份內容儲存根目錄樹。 本節介紹如何確定獨立和群集環境的內容儲存根目錄的位置。

### 內容儲存根位置（獨立環境） {#content-storage-root-location-stand-alone-environment}

安裝Content Services（不建議使用）時，將建立Content Storage Root目錄。 內容儲存根目錄的位置在表單安裝過程AEM中確定。

內容儲存根目錄的預設位置是 `[aem-forms root]/lccs_data`。

備份位於內容儲存根目錄中的以下目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，該目錄也位於內容儲存根目錄中。 如果/backup-lucene-indexes目錄存在，則不要備份/lucene-indexes目錄，因為它可能會導致錯誤。

### 內容儲存根位置（群集環境） {#content-storage-root-location-clustered-environment}

在群集環境中安裝Content Services（已棄用）時，內容儲存根目錄將被拆分為兩個單獨的目錄：

**內容儲存根目錄：** 通常，群集中所有節點都可訪問的讀/寫共用網路目錄

**索引根目錄：** 在群集中每個節點上建立的目錄，始終具有相同的路徑和目錄名

內容儲存根目錄的預設位置是 `[GDS root]/lccs_data`，也請參見Wiki頁。 `[GDS root]` 是中所述的位置 [GDS位置](files-back-recover.md#gds-location)。 備份位於內容儲存根目錄中的以下目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，該目錄也位於內容儲存根目錄中。 如果/backup-lucene-indexes目錄存在，則不要備份/lucene-indexes目錄，因為它可能會導致錯誤。

索引根目錄的預設位置是 `[aem-forms root]/lucene-indexes` 在每個節點上。

## 客戶安裝的字型 {#customer-installed-fonts}

如果在表單環境中安AEM裝了其他字型，則必須單獨備份它們。 備份在管理控制台中「設定」>「核心繫統」>「配置」下指定的所有Adobe和客戶字型目錄。 確保備份整個字型目錄。

>[!NOTE]
>
>預設情況下，隨表單安裝的AEMAdobe字型位於 `[aem-forms root]/fonts` 的子菜單。

如果正在重新初始化主機上的作業系統，並且希望使用以前作業系統中的字型，則還應備份系統字型目錄的內容。 （有關具體說明，請參閱作業系統的文檔）。
