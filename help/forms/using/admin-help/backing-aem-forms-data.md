---
title: 備份表AEM單資料
seo-title: Backing up the AEM forms data
description: 本文檔介紹完成表單資料庫、GDS和內容儲存根目錄的熱備份或在AEM線備份所需的步驟。
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

# 備份表AEM單資料 {#backing-up-the-aem-forms-data}

本節介紹完成表單資料庫、GDS和內容儲存根目錄的熱備份或在AEM線備份所需的步驟。

在AEM將表單安裝並部署到生產區後，資料庫管理員應對資料庫執行初始完全或冷備份。 必須關閉此備份的資料庫。 然後，應定期執行資料庫的差異或增量（或熱）備份。

要確保成功備份和恢復，系統映像備份必須始終可用。 然後，如果發生丟失，您可以將整個環境恢復到一致狀態。

在備份GDS 、儲存庫和內容儲存根目錄的同時AEM備份資料庫有助於在需要恢復時保持這些系統的同步。

本節中介紹的備份過程要求您在備份表單資料庫、儲存庫、GDS和內AEM容儲存根目AEM錄之前，進入安全備份模式。 備份完成後，必須退出安全備份模式。 安全備份模式用於標籤駐留在GDS中的長期和持久文檔。 此模式確保在釋放安全備份模式之前，自動檔案清理機制（檔案收集器）不會刪除過期的檔案。 必須使GDS備份與資料庫備份同步。

必須備份GDS位置的頻率取決於表單的使AEM用方式和備份窗口的可用性。 備份窗口可能會受長期進程的影響，因為它們可以運行數天。 如果不斷更改、添加和刪除此目錄中的檔案，則應更頻繁地備份GDS位置。

如前一節所述，如果資料庫以記錄模式運行，則還必須頻繁備份資料庫日誌，以便在介質出現故障時可以使用它們恢復資料庫。

>[!NOTE]
>
>未引用的檔案在恢復過程後可能會保留在GDS目錄中。 這是目前已知的限制。

## 備份資料庫、 GDS 、存AEM儲庫和內容儲存根目錄 {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

您必須AEM將表單置於安全備份（快照）模式或滾動備份（連續覆蓋）模式。 在設定AEM表單以輸入任何一種備份模式之前，請確保：

* 驗證系統版本並記錄自上次執行完整系統映像備份後應用的修補程式或更新。
* 如果使用滾動或快照模式備份，請確保已使用正確的日誌設定配置資料庫，以允許對資料庫進行熱備份。 (請參閱 [表AEM單資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。)

除此之外，還要遵守以下備份/恢復過程的指導原則。

* 使用可用的作業系統或第三方備份實用程式備份GDS目錄。 (請參閱 [GDS位置](/help/forms/using/admin-help/files-back-recover.md#gds-location)。)
* （可選）使用可用的作業系統或第三方備份和實用程式備份內容儲存根目錄。 (請參閱 [內容儲存根位置（獨立環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) 或 [內容儲存根位置（群集環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment)。)
* 備份作者和發佈實例（crx -repository備份）。

   要備份Tergement Management Solution環境，請對作者執行步驟並發佈實例，如中所述 [備份和恢復](/help/sites-administering/backup-and-restore.md)。

   備份作者和發佈實例時請考慮以下幾點：

   * 確保對作者和發佈實例的備份同步以同時啟動。雖然在執行備份時可以繼續使用作者和發佈實例，但建議在備份期間不發佈任何資產以避免任何未捕獲的更改。 等待作者和發佈實例的備份結束，然後發佈新資產。
   * 「作者」節點的完整備份包括對Forms管理器和AEM Forms工作區資料的備份。
   * Workbench開發人員可以繼續在本地處理其流程。 在備份階段，他們不應部署任何新進程。
   * 有關每個備份會話（用於滾動備份模式）長度的決定應基於備份表單中所有資料(DB、GDS、儲存庫和任何其他自AEM定義資料)所花AEM費的總時間。

您應備份表單數AEM據庫，包括任何事務日誌。 (請參閱 [表AEM單資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。) 有關詳細資訊，請參閱資料庫的相應知識庫文章：

* [Oracle表單的備份和恢復AEM](https://www.adobe.com/go/kb403624)
* [表單的MySQL備份和恢復AEM](https://www.adobe.com/go/kb403625)
* [Microsoft表單的SQL Server備份和恢復AEM](https://www.adobe.com/go/kb403623)
* [表單的DB2備份和恢復AEM](https://www.adobe.com/go/kb403626)

這些文章為備份和恢復資料提供了基本的資料庫功能。 它們不是特定供應商資料庫備份和恢復功能的全面技術指南。 它們概述了為表單應用程式資料建立可靠資料庫備份策略所AEM需的命令。

>[!NOTE]
>
>在開始備份GDS之前，必須完成資料庫備份。 如果資料庫備份未完成，則資料將不同步。

### 進入備份模式 {#entering-the-backup-modes}

可以使用管理控制台、LCBackupMode命令或表單安裝附帶的APIAEM來輸入和退出備份模式。 請注意，對於滾動備份（連續覆蓋），管理控制台選項不可用；應使用命令行選項或API。 <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>如果在forms伺服器上配置了SSL，則不能使用LCBackupMode.CMD指令碼將forms伺服器置於備份模式。

**使用管理控制台進入安全備份模式**

1. 登錄到管理控制台。
1. 按一下「設定」>「核心繫統設定」>「備份實用程式」。
1. 選擇在安全備份模式下操作，然後按一下確定。

   此方法將表AEM單無限期地置於備份模式（無超時），並且它進入快照模式，而不是滾動備份模式。

**使用命令行選項進入安全備份模式**

可以使用命令行介面 `LCBackupMode` 將表單置於AEM安全備份模式的指令碼。

1. 設定ADOBELIVECYCLE並啟動應用程式伺服器。
1. 轉到 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 的子菜單。
1. 根據您的作業系統，編輯 `LCBackupMode.cmd` 或 `LCBackupMode.sh` 指令碼，提供適合您系統的預設值。
1. 在命令提示符下，在一行上運行以下命令：

   * (Windows) `LCBackupMode.cmd enter [-Host=`*主機名* `] [-port=`*埠號* `] [-user=`*用戶名* `] [-password=`*密碼* `] [-label=`*標籤名* `] [-timeout=`*秒* `]`
   * (Linux、UNIX) `LCBackupMode.sh enter [-host=`*主機名* `] [-port=`*埠號* `] [-user=`*用戶名* `] [-password=`*密碼* `] [-label=`*標籤名* `]`

   在前面的命令中，佔位符的定義如下：

   `Host` 是運行表單的主AEM機的名稱。

   `port` 是運行窗體的應用程式伺服器AEM的WebServices埠。

   `user` 是表單管理員的AEM用戶名。

   `password` 是表單管理AEM員的密碼。

   `label` 是此備份的文本標籤，可以是任意字串。

   `timeout` 是自動保留備份模式的秒數。 可以是0到10,080。 如果為0，則備份模式永遠不會超時。

   有關備份模式的命令行介面的詳細資訊，請參閱BackupRestoreCommandline目錄中的自述檔案。

### 退出備份模式 {#leaving-backup-modes}

可以使用管理控制台或命令行選項來保留備份模式。

**保持安全備份模式（快照模式）**

要使用Administration Console在安AEM全備份模式（快照模式）之外執行表單，請執行以下任務。

1. 登錄到Administration Console。
1. 按一下「設定」>「核心繫統設定」>「備份實用程式」。
1. 取消選擇「在安全備份模式下操作」，然後按一下「確定」。

**保留所有備份模式**

可以使用命令行介面在安全備AEM份模式（快照模式）或結束當前備份模式會話（滾動模式）之外採取表單。 請注意，不能使用管理控制台退出滾動備份模式。 在滾動備份模式下，管理控制台上的備份實用程式控制項被禁用。 必須使用API調用或使用LCBackupMode命令。

1. 轉到 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 的子菜單。
1. 根據您的作業系統，編輯 `LCBackupMode.cmd` 或 `LCBackupMode.sh` 指令碼，提供適合您系統的預設值。

   >[!NOTE]
   >
   >必須按照中的應用程式伺服器的相應章節中所述設定JAVA_HOME目錄 [準備安裝表AEM單](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*。*

1. 在單行上運行以下命令：

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*主機名* `] [-port=`*埠號* `] [-user=`*用戶名* `] [-password=`*密碼* `]`
   * (Linux、UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*主機名* `] [-port=`*埠號* `] [-user=`*用戶名* `] [-password=`*密碼* `]`

      在前面的命令中，佔位符的定義如下：

      `Host` 是運行表單的主AEM機的名稱。

      `port` 是應用程式服AEM務器上運行表單的埠。

      `user` 是表單管理員的AEM用戶名。

      `password` 是表單管理AEM員的密碼。

      `leaveContinuousCoverage` 使用此選項完全禁用滾動備份模式。
   >[!NOTE]
   >
   >在備份模式關閉時，無法重新建立連續覆蓋。 在此期間的任何更改都不受保護。

   >[!NOTE]
   >
   >如果在資料庫中啟用文檔儲存，則快照備份模式和滾動備份模式不適用。

   有關備份模式的命令行介面的詳細資訊，請參閱BackupRestoreCommandline目錄中的自述檔案。
