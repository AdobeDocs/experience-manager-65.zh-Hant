---
title: 要備份和復原的檔案
description: 本檔案說明必須備份的應用程式和資料檔案。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '2029'
ht-degree: 0%

---

# 要備份和復原的檔案 {#files-to-back-up-and-recover}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

以下各節將更詳細地說明必須備份的應用程式和資料檔案。

請考量下列有關備份與復原的要點：

* 資料庫應在GDS和AEM儲存庫之前進行備份。
* 如果您需要關閉叢集叢集環境中的節點以進行備份，請確定次要節點在主要節點之前關閉。 否則，可能會導致叢集或伺服器中的不一致。 此外，主要節點應在任何次要節點之前上線。
* 若要進行叢集的還原作業，應該針對叢集中的每個節點停止應用程式伺服器。

## 全域檔案儲存目錄 {#global-document-storage-directory}

GDS是用來儲存處理程式中所使用之長期檔案的目錄。 長效檔案的存留期旨在橫跨一或多個AEM表單系統的啟動，並可橫跨數天甚至數年。 這些長效檔案可以包含PDF、原則和表單範本。 長效檔案是許多AEM Forms部署整體狀態的重要部分。 如果部分或所有長期檔案遺失或損毀，Forms伺服器可能會變得不穩定。

非同步作業引動的輸入檔案也儲存在GDS中，並且必須可用於處理請求。 因此，您必須考量裝載GDS的檔案系統的可靠性，並採用獨立磁碟備援陣列(RAID)或其他適合您品質和服務等級需求的技術。

GDS的位置是在AEM Forms安裝過程中或之後使用管理主控台確定的。 除了保留GDS的高可用性位置之外，您還可以啟用檔案的資料庫儲存。 當資料庫用於檔案儲存體[&#128279;](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)時，請參閱備份選項。

### GDS位置 {#gds-location}

如果您在安裝期間將位置設定保留為空白，則該位置會預設為應用程式伺服器安裝下的目錄。 備份應用程式伺服器的下列目錄：

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

如果您將GDS位置變更為非預設位置，您可以依照下列方式加以確定：

* 登入管理主控台，然後按一下設定>核心系統設定>設定。
* 記錄在「全域檔案儲存目錄」方塊中指定的位置。

在叢集環境中，GDS通常會指向網路上共用的目錄，而且每個叢集節點都可以讀取/寫入存取該目錄。

如果原始位置不再可用，則在復原期間可能會變更GDS的位置。 （請參閱[在復原期間變更GDS位置](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。）

### 當資料庫用於檔案儲存時的備份選項 {#backup-options-when-database-is-used-for-document-storage}

您可以使用管理主控台在AEM表單資料庫中啟用AEM表單檔案儲存。 即使此選項會保留資料庫中的所有永久檔案，AEM表單仍需要檔案系統型GDS目錄，因為它可用來儲存與AEM表單的工作階段和呼叫相關的永久和暫存檔案及資源。

當您在管理控制檯的「核心系統設定」中選取「啟用資料庫中的檔案儲存」選項，或使用Configuration Manager時，AEM Forms不允許快照備份模式和滾動備份模式。 因此，您不需要使用AEM表單管理備份模式。 如果您使用此選項，您應在啟用選項後，只備份一次GDS。 當您從備份復原AEM表單時，不需要重新命名GDS的備份目錄或還原GDS。

## AEM存放庫 {#aem-repository}

如果在安裝AEM表單時配置了crx-repository，則會建立AEM存放庫(crx-repository)。 crx-repository目錄的位置是在AEM表單安裝過程中確定的。 AEM儲存區域需要備份和還原，以及資料庫和GDS，才能在AEM表單中保持一致AEM表單資料。 AEM存放庫包含通訊管理解決方案、Forms manager和AEM Forms Workspace的資料。

### 通訊管理解決方案 {#correspondence-management-solution}

通訊管理解決方案集中管理安全、個人化和互動通訊的建立、組裝和交付。 它可讓您以從建立到封存的簡化流程，快速組合來自預先核准和自訂編寫內容的通訊。 因此，您的客戶可獲得及時、準確、方便、安全且相關的通訊。 您的企業透過簡化流程以輕鬆、快速和生產力，將客戶互動的價值最大化，並將成本和風險降至最低。

簡單的通訊管理解決方案設定包含相同電腦上或不同電腦上的作者執行個體和發佈執行個體

### 表單管理員 {#forms-manager}

forms manager可簡化更新、管理和淘汰表單的程式。

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace符合(JEE上的AEM表單已棄用) Flex Workspace的功能，並新增擴充和整合Workspace的新功能，使其更人性化。

>[!NOTE]
>
>AEM Forms版本已棄用Flex工作區。

它允許在沒有Flash Player和Adobe Reader的使用者端上進行任務管理。 除了PDF forms和Flex表單外，它還有助於轉譯HTMLForms。

## AEM forms資料庫 {#aem-forms-database}

AEM Forms資料庫會儲存內容，例如表單人工因素、服務組態、處理狀態，以及對GDS和內容儲存根目錄（適用於內容服務）中檔案的資料庫參考。 您可以即時執行資料庫備份，而不會中斷服務，而且可復原到特定時間點或特定變更。 本節說明如何設定資料庫，以便可以即時進行備份。

在正確設定的AEM表單系統上，系統管理員和資料庫管理員可以輕鬆地共同作業，將系統復原到一致的已知狀態。

若要即時備份資料庫，您必須使用快照模式，或設定資料庫以指定的記錄模式執行。 這可在資料庫開啟且可供使用時，備份您的資料庫檔案。 此外，當資料庫在這些模式中執行時，會保留其倒回和作業事件日誌。

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES （已淘汰）是隨LiveCycle安裝的內容管理系統。 它可讓使用者設計、管理、監控及最佳化以人為中心的流程。 內容服務（已棄用）支援將於2014年12月31日終止。 請參閱[Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。

### DB2 {#db2}

設定DB2資料庫以存檔日誌模式執行。

>[!NOTE]
>
>如果您的AEM表單環境是從舊版AEM表單升級而來，並使用DB2，則不支援線上備份。 在這種情況下，您必須關閉AEM表單並執行離線備份。 未來版本的AEM表單將支援為升級客戶進行線上備份。

IBM有一套工具和協助系統，可協助資料庫管理員管理其備份和復原工作：

* IBM DB2封存記錄加速器
* IBM DB2資料封存專家

DB2具有將資料庫備份至Tivoli Storage Manager的內建功能。 使用Tivoli Storage Manager，DB2備份可以儲存在其他媒體或本機硬碟上。

### Oracle {#oracle}

使用快照集備份，或設定Oracle資料庫以存檔日誌模式執行。 (請參閱[Oracle備份：簡介](https://www.databasedesign-resource.com/oracle-backup.md)。)如需有關備份和復原Oracle資料庫的詳細資訊，請前往下列網站：

[Oracle備份與復原：](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html)說明備份與復原的概念，以及使用Recovery Manager (RMAN)進行備份、復原與報告的最常用技術，並提供有關如何規劃備份與復原策略的詳細資訊。

[Oracle Database Backup and Recovery User&#39;s Guide：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf)提供有關RMAN架構、備份與復原概念與機制、進階復原技術（例如時間點復原與資料庫倒溯功能）以及備份與復原效能調整的深入資訊。 此外也涵蓋使用者管理的備份與復原，使用主機作業系統設施，而非RMAN。 此磁碟區對於更複雜的資料庫部署以及進階復原案例的備份與復原是必要的。

[Oracle資料庫備份與復原參考：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf)提供所有RMAN命令的語法和語意的完整資訊，並說明可用來報告備份與復原活動的資料庫檢視。

### SQL Server {#sql-server}

使用快照備份或設定SQL Server資料庫以交易記錄模式執行。

SQL Server還提供兩種備份與復原工具：

* SQL Server Management Studio (GUI)
* T-SQL （命令列）

如需詳細資訊，請參閱[備份與還原](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)。

### MySQL {#mysql}

使用MySQLAdmin或修改Windows中的INI檔案，設定MySQL資料庫以二進位記錄模式執行。 （請參閱[MySQL二進位記錄](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)。）InnoBase軟體也提供MySQL的熱備份工具。 （請參閱[Innobase熱備份](https://www.innodb.com/hot-backup/features.md)。）

>[!NOTE]
>
>MySQL的預設二進位記錄模式為「陳述式」，與Content Services使用的表格不相容（已棄用）。 在此預設模式下使用二進位記錄會導致Content Services （已棄用）失敗。 如果您的系統包含Content Services （已棄用），請使用「混合」記錄模式。 若要啟用「混合」記錄，請將下列引數新增至my.ini檔案： `binlog_format=mixed log-bin=logname`

您可以使用mysqldump公用程式來取得完整的資料庫備份。 需要完整備份，但並不總是方便的。 它們會產生大型備份檔案，並需要時間來產生。 若要執行增量備份，請確定您是使用 — `log-bin`選項啟動伺服器，如上一節所述。 每當MySQL伺服器重新啟動時，它就會停止寫入目前的二進位記錄檔，建立新的記錄檔，從那時起，新的記錄檔就會變成目前的記錄檔。 您可以使用`FLUSH LOGS SQL`命令手動強制切換。 在第一次完整備份之後，後續的增量備份會使用mysqladmin公用程式搭配`flush-logs`命令來完成，這會建立下一個記錄檔。

請參閱[備份策略摘要](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)。

```text
binlog_format=mixed
log-bin=logname
```

## 內容儲存根目錄（僅限Content Services） {#content-storage-root-directory-content-services-only}

「內容儲存根目錄」包含Content Services (Deprecated)存放庫，其中儲存所有檔案、人工因素及索引。 必須備份內容儲存根目錄樹狀結構。 本節說明如何為獨立和叢集環境確定「內容儲存根目錄」的位置。

### 內容儲存根目錄位置（獨立環境） {#content-storage-root-location-stand-alone-environment}

內容儲存根目錄是在安裝Content Services （已棄用）時建立。 「內容儲存根目錄」的位置是在AEM Forms安裝過程中確定的。

內容儲存根目錄的預設位置為`[aem-forms root]/lccs_data`。

備份內容儲存根目錄中的下列目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-index

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，也在「內容儲存根目錄」中。 如果/backup-lucene-indexes目錄存在，請勿備份/lucene-indexes目錄，因為它可能會導致錯誤。

### 內容儲存根目錄位置（叢集環境） {#content-storage-root-location-clustered-environment}

當您在叢集環境中安裝Content Services （已棄用）時，內容儲存根目錄會分割成兩個不同的目錄：

**內容儲存根目錄：**&#x200B;一般而言，叢集中所有節點都可讀取/寫入存取的共用網路目錄

**索引根目錄：**&#x200B;在叢集中的每個節點上建立的目錄，路徑和目錄名稱一律相同

內容儲存根目錄的預設位置為`[GDS root]/lccs_data`，其中`[GDS root]`是[GDS位置](files-back-recover.md#gds-location)中說明的位置。 備份內容儲存根目錄中的下列目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-index

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，也在「內容儲存根目錄」中。 如果/backup-lucene-indexes目錄存在，請勿備份/lucene-indexes目錄，因為它可能會導致錯誤。

索引根目錄的預設位置是每個節點上的`[aem-forms root]/lucene-indexes`。

## 客戶安裝的字型 {#customer-installed-fonts}

如果您在AEM表單環境中安裝了其他字型，則必須分別備份這些字型。 備份在「設定>核心系統>設定」下的「管理主控台」中指定的所有Adobe和客戶字型目錄。 請確定您備份整個字型目錄。

>[!NOTE]
>
>依預設，隨AEM表單安裝的Adobe字型在`[aem-forms root]/fonts`目錄中。

如果您正在重新初始化主機電腦上的作業系統，並且想要使用先前作業系統的字型，則系統字型目錄的內容也應進行備份。 （如需特定指示，請參閱作業系統的檔案）。
