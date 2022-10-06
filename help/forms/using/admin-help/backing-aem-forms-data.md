---
title: 備份AEM表單資料
seo-title: Backing up the AEM forms data
description: 本文檔介紹完成AEM表單資料庫、GDS和內容儲存根目錄的熱備份或聯機備份所需的步驟。
seo-description: This document describes the steps that are required to complete a hot, or online, backup of the AEM forms database, the GDS, and Content Storage Root directories.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 0%

---

# 備份AEM表單資料 {#backing-up-the-aem-forms-data}

本節介紹完成AEM表單資料庫、GDS和內容儲存根目錄的熱備份或聯機備份所需的步驟。

安裝AEM表單並部署到生產區後，資料庫管理員應執行資料庫的初始完整或冷備份。 必須關閉此備份的資料庫。 然後，應定期執行資料庫的差異或增量（或熱）備份。

為確保備份和恢復成功，系統映像備份必須始終可用。 然後，如果發生丟失，您可以將整個環境恢復到一致的狀態。

在備份資料庫的同時備份GDS、AEM儲存庫和內容儲存根目錄備份有助於在需要恢復時保持這些系統的同步。

本節中介紹的備份過程要求您在備份AEM表單資料庫、AEM儲存庫、GDS和內容儲存根目錄之前進入安全備份模式。 備份完成時，必須退出安全備份模式。 安全備份模式用於標籤駐留在GDS中的長期和持久文檔。 此模式可確保在釋放安全備份模式之前，自動檔案清理機制（檔案收集器）不會刪除過期的檔案。 必須使GDS備份與資料庫備份保持同步。

必須備份GDS位置的頻率取決於使用AEM表單的方式和備份窗口的可用性。 備份窗口可能受長期進程的影響，因為它們可以運行數天。 如果您不斷更改、添加和刪除此目錄中的檔案，則應更頻繁地備份GDS位置。

如果資料庫以記錄模式運行（如前一節所述），則還必須頻繁備份資料庫日誌，以便在介質出現故障時可以使用這些日誌來還原資料庫。

>[!NOTE]
>
>恢復過程後，未引用的檔案可能會保留在GDS目錄中。 這是目前已知的限制。

## 備份資料庫、 GDS、AEM儲存庫和內容儲存根目錄 {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

必須將AEM表單置於安全備份（快照）模式或滾動備份（連續覆蓋）模式。 在將AEM表單設定為進入任一備份模式之前，請確保：

* 驗證系統版本並記錄自上次完成系統映像備份後應用的補丁程式或更新。
* 如果您使用滾動或快照模式備份，請確保您的資料庫配置了正確的日誌設定以允許對資料庫進行熱備份。 (請參閱 [AEM forms資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

除了這些外，還要遵守以下備份/還原過程的准則。

* 使用可用的作業系統或第三方備份實用程式備份GDS目錄。 (請參閱 [GDS位置](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* （可選）使用可用的作業系統或第三方備份和實用程式備份內容儲存根目錄。 (請參閱 [內容儲存根位置（獨立環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) 或 [內容儲存根位置（群集環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* 備份製作和發佈執行個體（crx-repository備份）。

   若要備份通信管理解決方案環境，請執行製作和發佈例項的步驟，如 [備份和還原](/help/sites-administering/backup-and-restore.md).

   備份製作和發佈執行個體時，請考量下列幾點：

   * 請確定同步製作和發佈執行個體的備份，以便同時開始。雖然您可以在執行備份時繼續使用製作和發佈執行個體，但建議您不要在備份期間發佈任何資產，以避免任何未擷取的變更。 等待製作和發佈執行個體的備份結束，再發佈新資產。
   * 完整備份製作節點，包括備份Forms Manager和AEM Forms Workspace資料。
   * Workbench開發人員可繼續在本機處理其程式。 他們不應在備份階段部署任何新進程。
   * 每個備份會話（用於滾動備份模式）的長度的決定應基於備份AEM表單中所有資料(DB、GDS、AEM儲存庫和任何其他自定義資料)所花費的總時間。

您應備份AEM表單資料庫，包括任何事務日誌。 (請參閱 [AEM forms資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) 有關詳細資訊，請參閱資料庫的相應知識庫文章：

* [OracleAEM表單的備份和恢復](https://www.adobe.com/go/kb403624)
* [AEM表單的MySQL備份和恢復](https://www.adobe.com/go/kb403625)
* [Microsoft SQL Server針對AEM表單的備份和恢復](https://www.adobe.com/go/kb403623)
* [AEM表單的DB2備份和恢復](https://www.adobe.com/go/kb403626)

這些文章為資料備份和恢復提供了基本資料庫功能的指導。 它們不是特定供應商資料庫備份和恢復功能的全包性技術指南。 它們概述了為AEM表單應用程式資料建立可靠資料庫備份策略所需的命令。

>[!NOTE]
>
>在開始備份GDS之前，必須完成資料庫備份。 如果資料庫備份未完成，則您的資料將不同步。

### 進入備份模式 {#entering-the-backup-modes}

您可以使用管理控制台、LCBackupMode命令或AEM表單安裝中可用的API來進入和離開備份模式。 請注意，對於滾動備份（連續覆蓋），管理控制台選項不可用；您應使用命令列選項或API。 <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>如果您在表單伺服器上配置了SSL，則無法使用LCBackupMode.CMD指令碼將表單伺服器置於備份模式。

**使用管理控制台進入安全備份模式**

1. 登入管理控制台。
1. 按一下「設定」>「核心繫統設定」>「備份實用程式」。
1. 選擇「在安全備份模式下操作」 ，然後按一下「確定」。

   此方法會無限期地將AEM表單置於備份模式（沒有逾時），而且會進入快照模式，而非滾動備份模式。

**使用命令行選項進入安全備份模式**

可使用命令行介面 `LCBackupMode` 將AEM表單置於安全備份模式的指令碼。

1. 設定ADOBELIVECYCLE並啟動應用程式伺服器。
1. 前往 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 檔案夾。
1. 視您的作業系統而定，請編輯 `LCBackupMode.cmd` 或 `LCBackupMode.sh` 指令碼，提供適合您系統的預設值。
1. 在命令提示符下，在一行上運行以下命令：

   * (Windows) `LCBackupMode.cmd enter [-Host=`*主機名* `] [-port=`*portnumber* `] [-user=`*用戶名* `] [-password=`*密碼* `] [-label=`*標籤名稱* `] [-timeout=`*秒* `]`
   * (Linux、UNIX) `LCBackupMode.sh enter [-host=`*主機名* `] [-port=`*portnumber* `] [-user=`*用戶名* `] [-password=`*密碼* `] [-label=`*標籤名稱* `]`

   在前面的命令中，佔位符的定義如下：

   `Host` 是執行AEM表單的主機名稱。

   `port` 是運行AEM表單的應用程式伺服器的WebServices埠。

   `user` 是AEM forms管理員的使用者名稱。

   `password` 是AEM forms管理員的密碼。

   `label` 是此備份的文本標籤，可以是任何字串。

   `timeout` 是自動保留備份模式的秒數。 可以是0到10,080。 如果為0（預設值為），則備份模式永遠不會超時。

   有關指向備份模式的命令行介面的詳細資訊，請參閱BackupRestoreCommandline目錄中的自述檔案。

### 退出備份模式 {#leaving-backup-modes}

您可以使用管理控制台或命令行選項來保留備份模式。

**保持安全備份模式（快照模式）**

要使用Administration Console將AEM表單帶出安全備份模式（快照模式），請執行以下任務。

1. 登入管理控制台。
1. 按一下「設定」>「核心繫統設定」>「備份實用程式」。
1. 取消選擇「在安全備份模式下操作」 ，然後按一下「確定」。

**保留所有備份模式**

您可以使用命令行介面將AEM表單帶出安全備份模式（快照模式），或結束當前備份模式會話（滾動模式）。 請注意，您無法使用管理控制台來離開滾動備份模式。 在滾動式備份模式中，禁用管理控制台上的備份實用程式控制項。 您必須使用API呼叫或使用LCBackupMode命令。

1. 前往 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 檔案夾。
1. 視您的作業系統而定，請編輯 `LCBackupMode.cmd` 或 `LCBackupMode.sh` 指令碼，提供適合您系統的預設值。

   >[!NOTE]
   >
   >您必須依照 [準備安裝AEM表單](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. 在單行上運行以下命令：

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*主機名* `] [-port=`*portnumber* `] [-user=`*用戶名* `] [-password=`*密碼* `]`
   * (Linux、UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*主機名* `] [-port=`*portnumber* `] [-user=`*用戶名* `] [-password=`*密碼* `]`

      在前面的命令中，佔位符的定義如下：

      `Host` 是執行AEM表單的主機名稱。

      `port` 是應用程式伺服器上執行AEM表單的埠。

      `user` 是AEM forms管理員的使用者名稱。

      `password` 是AEM forms管理員的密碼。

      `leaveContinuousCoverage` 使用此選項可完全禁用滾動備份模式。
   >[!NOTE]
   >
   >在備份模式關閉時，無法重新建立連續覆蓋。 在此期間的任何更改都不受保護。

   >[!NOTE]
   >
   >如果在資料庫中啟用了文檔儲存，則快照備份模式和滾動備份模式不適用。

   有關指向備份模式的命令行介面的詳細資訊，請參閱BackupRestoreCommandline目錄中的自述檔案。
