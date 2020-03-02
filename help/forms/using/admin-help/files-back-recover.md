---
title: 要備份和恢復的檔案
seo-title: 要備份和恢復的檔案
description: 本文檔介紹了必須備份的應用程式和資料檔案。
seo-description: 本文檔介紹了必須備份的應用程式和資料檔案。
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec

---


# 要備份和恢復的檔案 {#files-to-back-up-and-recover}

必須備份的應用程式和資料檔案將在以下幾節中詳細說明。

請考慮以下有關備份和恢復的要點：

* 應在GDS和AEM資料庫之前備份資料庫。
* 如果需要關閉群集環境中的節點進行備份，請確保在主節點之前關閉從節點。 否則，會導致叢集或伺服器不一致。 此外，主節點應在任何從節點之前變為活動節點。
* 對於群集的恢復操作，應停止群集中每個節點的應用程式伺服器。

## 全局文檔儲存目錄 {#global-document-storage-directory}

GDS是一個目錄，用於儲存進程中使用的長壽命檔案。 長效檔案的存留期可跨AEM表單系統的一或多次啟動，而且可跨日期甚至數年。 這些長期使用的檔案可包含PDF、原則和表單範本。 長期使用的檔案是許多AEM表單部署整體狀態的重要部分。 如果某些或所有長期使用的檔案遺失或損毀，表單伺服器可能會變得不穩定。

非同步作業調用的輸入文檔也儲存在GDS中，並且必須可用於處理請求。 因此，務必考慮托管GDS並採用獨立磁碟冗餘陣列(RAID)或其他技術的檔案系統的可靠性，以滿足您的服務質量和服務級別要求。

GDS的位置是在AEM表單安裝程式期間或更新版本中，使用管理控制台來決定。 除了保留GDS的高可用性位置外，您還可以為文檔啟用資料庫儲存。 請參 [閱將資料庫用於文檔儲存時的備份選項](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)。

### GDS位置 {#gds-location}

如果在安裝期間將位置設定保留為空，則位置預設為應用程式伺服器安裝下的目錄。 您必須備份應用程式伺服器的以下目錄：

* (JBoss) `[appserver root]/server/[server]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/[server]/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/[server]/DocumentStorage`

如果將GDS位置更改為非預設位置，則可以按如下方式確定該位置：

* 登入管理控制台，然後按一下「設定>核心繫統設定>設定」。
* 記錄在「全局文檔儲存目錄」框中指定的位置。

在群集環境中，GDS通常指向網路上共用的目錄，並且每個群集節點都可讀／寫訪問該目錄。

如果原始位置不再可用，則在恢復期間可更改GDS的位置。 (請參 [閱在恢復過程中更改GDS位置](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。)

### 資料庫用於文檔儲存時的備份選項 {#backup-options-when-database-is-used-for-document-storage}

您可以使用管理主控台，在AEM表單資料庫中啟用AEM表單檔案儲存。 即使這個選項會保留資料庫中的所有永久性檔案，AEM表單仍需要以檔案系統為基礎的GDS目錄，因為它可用來儲存與AEM表單作業和呼叫相關的永久和暫時檔案和資源。

當您在管理控制台的「核心繫統設定」或使用Configuration Manager中選取「在資料庫中啟用檔案儲存」選項時，AEM表單不允許快照備份模式和滾動備份模式。 因此，您不需要使用AEM表單來管理備份模式。 如果您使用此選項，則在啟用該選項後，您應該只備份一次GDS。 從備份中恢復AEM表單時，您不需要為GDS重新命名備份目錄或還原GDS。

## AEM存放庫 {#aem-repository}

如果在安裝AEM表單時設定crx-repository，則會建立AEM資料庫(crx-repository)。 crx-repository目錄的位置是在AEM表單安裝程式期間決定。 AEM儲存庫備份和還原需要資料庫和GDS，才能在AEM表單中取得一致的AEM表單資料。 AEM儲存庫包含Correponsement Management Solution、Forms manager和AEM Forms Workspace的資料。

### 通信管理解決方案 {#correspondence-management-solution}

通信管理解決方案集中管理安全、個人化和互動式通信的建立、組裝和交付。 它可讓您從預先核准和自訂製作的內容，以簡化的流程，從建立到封存，快速整合對應內容。 因此，您的客戶可以即時、準確、方便、安全且相關的通訊。 您的企業透過簡化的流程，以簡化流程，以簡化流程、加快流程並提高生產力，進而最大化客戶互動的價值並將成本與風險降至最低。

簡單的「對應管理解決方案」設定包括作者執行個體和發佈執行個體，這些執行個體位於同一部電腦或不同的電腦上

### 表單管理器 {#forms-manager}

forms manager可簡化更新、管理和淘汰表單的程式。

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace符合（JEE上的AEM Forms已過時）Flex Workspace的功能，並新增功能以擴充和整合工作區，讓它更方便使用。

>[!NOTE]
>
>AEM表單版本不建議使用Flex Workspace。

它可讓用戶端不需使用Flash player和Adobe Reader即可進行任務管理。 除了PDF表單和Flex表單外，它還可協助轉譯HTML表格。

## AEM表單資料庫 {#aem-forms-database}

AEM表單資料庫會儲存GDS和「內容儲存根目錄」（針對Content Services）中檔案的表單對象、服務設定、處理狀態和資料庫參考等內容。 資料庫備份可以即時執行而不中斷服務，恢復可以到特定時間點或特定更改。 本節介紹如何配置資料庫以便即時備份。

在正確設定的AEM表單系統上，系統管理員和資料庫管理員可輕鬆協作，將系統還原為一致的已知狀態。

要即時備份資料庫，必須使用快照模式或將資料庫配置為在指定的日誌模式下運行。 這允許在資料庫開啟並可供使用時備份資料庫檔案。 此外，當資料庫在這些模式下運行時，它將保留其回滾和事務日誌。

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES（已過時）是與LiveCycle一起安裝的內容管理系統。 它可讓使用者設計、管理、監控和最佳化以人為中心的流程。 內容服務（已過時）支援將於2014年12月31日截止。 請參閱 [Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。 如需有關設定Content Services（已過時）的資訊，請參 [閱管理Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)。

### DB2 {#db2}

配置DB2資料庫以在歸檔日誌模式下運行。

>[!NOTE]
>
>如果您的AEM表單環境是從舊版AEM表單升級並使用DB2，則不支援線上備份。 在此情況下，您必須關閉AEM表單並執行離線備份。 未來版本的AEM表格將支援升級客戶的線上備份。

IBM提供一套工具和幫助系統，幫助資料庫管理員管理其備份和恢復任務：

* IBM DB2 Archive Log Accelerator(請參閱 [IBM DB2 Archive Log Accelerator for z/OS User&#39;s Guide](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true))
* IBM DB2 Data Archive專家(請參 [閱IBM DB2 Data Archive Expert使用手冊和參考](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true)。)

DB2具有將資料庫備份到Tivoli Storage Manager的內置功能。 通過使用Tivoli Storage Manager , DB2備份可以儲存在其他介質或本地硬碟上。

有關DB2資料庫備份和恢復的詳細資訊，請參 [閱開發DB2的備份和恢復策略](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm)。

### Oracle {#oracle}

使用快照備份或將Oracle資料庫配置為在歸檔日誌模式下運行。 (請參 [閱Oracle備份：簡介](https://www.databasedesign-resource.com/oracle-backup.md)。)有關備份和恢復Oracle資料庫的詳細資訊，請轉至以下站點：

[](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Oracle備份和恢復：詳細說明了備份和恢復的概念以及使用Recovery Manager(RMAN)進行備份、恢復和報告的最常用技術，並提供了有關如何規劃備份和恢復策略的詳細資訊。

[](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Oracle Database Backup and Recovery User&#39;s Guide:提供有關RMAN體系結構、備份和恢復概念和機制、高級恢復技術（如時間點恢復和資料庫閃回功能）以及備份和恢復效能調整的深入資訊。 它還包括使用主機作業系統功能（而非RMAN）的用戶管理備份和恢復。 此卷對於備份和恢復更複雜的資料庫部署以及高級恢複方案至關重要。

[](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Oracle資料庫備份和恢復參考：提供有關所有RMAN命令的語法和語義的完整資訊，並介紹可用於報告備份和恢復活動的資料庫視圖。

### SQL Server {#sql-server}

使用快照備份或將SQL server資料庫配置為在事務日誌模式下運行。

SQL Server還提供了兩種備份和恢復工具：

* SQL Server Management Studio(GUI)
* T-SQL（命令行）

請參 [閱備](https://articles.techrepublic.com.com/5100-1035_61-1043671.md)份策 [略和備份和還原](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)。

### MySQL {#mysql}

使用MySQLAdmin或修改Windows中的INI檔案，以配置MySQL資料庫以二進位日誌模式運行。 (請參 [閱MySQL二進位日誌](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)。)InnoBase軟體也提供了MySQL的熱備份工具。 (請參 [閱Innobase熱備份](https://www.innodb.com/hot-backup/features.md)。)

**注意**:MySQL *的預設二進位日誌記錄模式是「語句」，它與Content services使用的表（已過時）不相容。 在此預設模式中使用二進位記錄會導致Content Services（已過時）失敗。 如果您的系統包含Content Services（已過時），請使用「混合」記錄模式。*要啟用「混合」日誌，請將以下引數添加到my.ini檔案：
`binlog_format=mixed log-bin=logname`

您可以使用mysqldump實用程式獲得完整的資料庫備份。 需要完整備份，但並不總是方便的。 它們會生成大型備份檔案，並需要時間生成。 要執行增量備份，請確保使用——選項啟動服 `log-bin` 務器，如上節所述。 每次MySQL伺服器重新啟動時，它都停止寫入當前二進位日誌，建立新日誌，然後，從此開始，新日誌將變為當前日誌。 可以使用命令手動強制切換 `FLUSH LOGS SQL` 器。 在第一次完全備份後，後續增量備份將使用mysqladmin實用程式和命令來完成，該命 `flush-logs` 令將建立下一個日誌檔案。

請參 [閱備份策略摘要](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)。

```as3
binlog_format=mixed
log-bin=logname
```

## 內容儲存根目錄（僅限Content Services） {#content-storage-root-directory-content-services-only}

內容儲存根目錄包含儲存所有文檔、對象和索引的Content Services（已過時）儲存庫。 必須備份內容儲存根目錄樹。 本節介紹如何確定獨立環境和群集環境的內容儲存根目錄的位置。

### 內容儲存根位置（獨立環境） {#content-storage-root-location-stand-alone-environment}

當安裝Content Services（已過時）時，會建立內容儲存根目錄。 在AEM表單安裝程式期間，會決定內容儲存根目錄的位置。

內容儲存根目錄的預設位置為 `[aem-forms root]/lccs_data`。

備份位於「內容儲存根目錄」中的以下目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，該目錄也位於「內容儲存根目錄」中。 如果/backup-lucene-indexes目錄存在，請不要備份/lucene-indexes目錄，因為該目錄可能導致錯誤。

### 內容儲存根位置（群集環境） {#content-storage-root-location-clustered-environment}

在叢集環境中安裝Content Services（已過時）時，Content Storage Root目錄會分割為兩個不同的目錄：

**** 內容儲存根目錄：通常，共用網路目錄可供群集中所有節點讀／寫訪問

**** 索引根目錄：在群集中每個節點上建立的目錄，始終具有相同的路徑和目錄名

內容儲存根目錄的預設位置是 `[GDS root]/lccs_data`，其中 `[GDS root]` 是 [GDS位置中描述的位置](files-back-recover.md#gds-location)。 備份位於「內容儲存根目錄」中的以下目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，該目錄也位於「內容儲存根目錄」中。 如果/backup-lucene-indexes目錄存在，請不要備份/lucene-indexes目錄，因為該目錄可能導致錯誤。

索引根目錄的預設位置位於每 `[aem-forms root]/lucene-indexes` 個節點上。

## 客戶安裝字型 {#customer-installed-fonts}

如果您在AEM表單環境中安裝了其他字型，您必須個別備份這些字型。 備份管理控制台中「設定>核心繫統>設定」下所指定的所有Adobe和客戶字型目錄。 請確定您已備份整個字型目錄。

>[!NOTE]
>
>依預設，隨AEM表單安裝的Adobe字型位於目 `[aem-forms root]/fonts` 錄中。

如果您正在重新初始化主機上的作業系統，並想要使用先前作業系統的字型，則系統字型目錄的內容也應加以備份。 （如需特定指示，請參閱作業系統的檔案）。
