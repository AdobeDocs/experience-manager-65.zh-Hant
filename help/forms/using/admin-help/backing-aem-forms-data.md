---
title: 備份AEM表單資料
seo-title: 備份AEM表單資料
description: 本檔案說明完成AEM表單資料庫、GDS和內容儲存根目錄的熱備份或線上備份所需的步驟。
seo-description: 本檔案說明完成AEM表單資料庫、GDS和內容儲存根目錄的熱備份或線上備份所需的步驟。
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 備份AEM表單資料 {#backing-up-the-aem-forms-data}

本節說明完成AEM表單資料庫、GDS和內容儲存根目錄的熱備份或線上備份所需的步驟。

在AEM表單安裝並部署至生產區後，資料庫管理員應執行資料庫的初始完整備份或冷備份。 此備份必須關閉資料庫。 然後，應定期執行資料庫的差異或增量（或熱）備份。

為確保備份和恢復成功，系統映像備份必須隨時可用。 然後，如果發生損失，您可以將整個環境恢復到一致的狀態。

在備份GDS、AEM儲存庫和內容儲存根目錄的同時備份資料庫有助於在需要恢復時使這些系統保持同步。

本節所述的備份程式要求您在備份AEM表單資料庫、AEM儲存庫、GDS和內容儲存根目錄之前，先進入安全備份模式。 備份完成後，必須退出安全備份模式。 安全備份模式用於標籤駐留在GDS中的長期和持久文檔。 此模式可確保自動檔案清理機制（檔案收集器）在安全備份模式釋放之前不會刪除過期的檔案。 必須使GDS備份與資料庫備份保持同步。

必須備份GDS位置的頻率取決於AEM表單的使用方式和備份窗口的可用性。 備份窗口可能受到長期進程的影響，因為它們可以運行數天。 如果您不斷更改、添加和刪除此目錄中的檔案，則應更頻繁地備份GDS位置。

如果資料庫以記錄模式運行（如上節所述），則資料庫日誌也必須經常備份，以便在介質出現故障時用於恢復資料庫。

>[!NOTE]
>
>未引用的檔案可能在恢復過程後保存在GDS目錄中。 這是目前已知的限制。

## 備份資料庫、GDS、AEM儲存庫和內容儲存根目錄 {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

您必須將AEM表單置於安全備份（快照）模式或滾動備份（連續覆蓋）模式。 在您設定AEM表單以進入任一備份模式之前，請確定：

* 驗證系統版本並記錄自上次完成系統映像備份後應用的修補程式或更新。
* 如果您使用滾動或快照模式備份，請確保資料庫已配置了正確的日誌設定以允許資料庫的熱備份。 (請參 [閱AEM表單資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。)

除了這些外，請遵守以下備份／恢復過程的指導方針。

* 使用可用的作業系統或第三方備份實用程式備份GDS目錄。 (請參 [閱GDS位置](/help/forms/using/admin-help/files-back-recover.md#gds-location)。)
* （可選）使用可用的作業系統或第三方備份和實用程式備份內容儲存根目錄。 (請參 [閱內容儲存根位置（單機環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment)[或內容儲存根位置（叢集環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment)。)
* 備份作者和發佈實例（crx -repository備份）。

   要備份Correponse Management Solution環境，請對作者執行步驟並發佈實例，如備份和還 [原中所述](/help/sites-administering/backup-and-restore.md)。

   備份作者和發佈實例時，請考慮以下幾點：

   * 請確定作者和發佈實例的備份已同步，以便同時啟動。雖然在執行備份時可以繼續使用作者和發佈實例，但建議您不要在備份期間發佈任何資產，以避免任何未捕獲的更改。 等待作者和發佈例項的備份結束，再發佈新資產。
   * 完整的「作者」節點備份包括Forms manager和AEM Forms Workspace資料的備份。
   * 工作台開發人員可繼續在本機處理其程式。 在備份階段，他們不應部署任何新進程。
   * 決定每個備份作業長度（用於滾動備份模式）時，應以備份AEM表單中所有資料（DB、GDS、AEM儲存庫和任何其他自訂資料）所花的總時間為準。

您應備份AEM表單資料庫，包括任何交易記錄檔。 (請參 [閱AEM表單資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。)如需詳細資訊，請參閱您資料庫的適當知識庫文章：

* [Oracle Backup and Recovery for AEM forms](https://www.adobe.com/go/kb403624)
* [AEM表單的MySQL備份和恢復](https://www.adobe.com/go/kb403625)
* [適用於AEM表單的Microsoft SQL server備份和恢復](https://www.adobe.com/go/kb403623)
* [AEM表單的DB2備份和恢復](https://www.adobe.com/go/kb403626)

這些文章為資料備份和恢復提供了基本資料庫功能的指導。 它們不是作為特定供應商資料庫備份和恢復功能的全面性技術指南。 它們概述為您的AEM表單應用程式資料建立可靠資料庫備份策略所需的命令。

>[!NOTE]
>
>在開始備份GDS之前，必須完成資料庫備份。 如果資料庫備份未完成，則您的資料將不同步。

### 進入備份模式 {#entering-the-backup-modes}

您可以使用管理控制台、LCBackupMode命令或AEM表單安裝隨附的API來輸入和離開備份模式。 請注意，對於滾動備份（連續覆蓋），管理控制台選項不可用；您應使用命令行選項或API。 <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>如果您在表單伺服器上設定了SSL，則無法使用LCBackupMode.CMD指令碼將表單伺服器置於備份模式。

**使用管理控制台進入安全備份模式**

1. 登入管理控制台。
1. 按一下「設定」>「核心繫統設定」>「備份實用程式」。
1. 選擇「在安全備份模式下操作」 ，然後按一下「確定」。

   此方法會無限期地將AEM表單置於備份模式（沒有逾時），而且會進入快照模式，而非滾動備份模式。

**使用命令行選項進入安全備份模式**

您可以使用命令列介面指 `LCBackupMode` 令碼，將AEM表單置於安全備份模式。

1. 設定ADOBE_LIVECYCLE並啟動應用程式伺服器。
1. Go to the `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` folder.
1. 視您的作業系統而定，編 `LCBackupMode.cmd` 輯或 `LCBackupMode.sh` 指令碼以提供適合您系統的預設值。
1. 在命令提示符下，在單行上運行以下命令：

   * (Windows)主機名稱 `LCBackupMode.cmd enter [-Host=`**主機名稱`] [-port=`*,Portnumber用戶名* 稱密 `] [-user=`*碼Label *Name(`] [-password=`**`] [-label=`**`] [-timeout=`** 秒) `]`
   * (Linux, UNIX)埠 `LCBackupMode.sh enter [-host=`*號&#x200B;*`] [-port=`*主機* 名 `] [-user=`*稱&#x200B;*用`] [-password=`*戶名Password*`] [-label=`*Labelname *密碼`]`
   在上面的命令中，佔位符的定義如下：

   `Host` 是執行AEM表單的主機名稱。

   `port` 是執行AEM表單之應用程式伺服器的WebServices埠。

   `user` 是AEM表單管理員的使用者名稱。

   `password` 是AEM表單管理員的密碼。

   `label` 是此備份的文本標籤，可以是任何字串。

   `timeout` 是自動離開備份模式的秒數。 可以是0到10,080。 如果為0（預設值），則備份模式永遠不會超時。

   有關備份模式的命令行介面的詳細資訊，請參閱BackupRestoreCommandline目錄中的自述檔案。

### 離開備份模式 {#leaving-backup-modes}

可以使用管理控制台或命令行選項來保留備份模式。

**保持安全備份模式（快照模式）**

若要使用Administration console將AEM表單帶出安全備份模式（快照模式），請執行下列工作。

1. 登入管理控制台。
1. 按一下「設定」>「核心繫統設定」>「備份實用程式」。
1. 取消選擇「在安全備份模式下操作」，然後按一下「確定」。

**保留所有備份模式**

您可以使用命令列介面，將AEM表單帶出安全備份模式（快照模式），或結束目前的備份模式工作階段（滾動模式）。 請注意，不能使用管理控制台來離開滾動備份模式。 在滾動備份模式下，管理控制台上的備份實用程式控制項將被禁用。 您必須使用API呼叫或使用LCBackupMode命令。

1. Go to the `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` folder.
1. 視您的作業系統而定，編 `LCBackupMode.cmd` 輯或 `LCBackupMode.sh` 指令碼以提供適合您系統的預設值。

   >[!NOTE]
   >
   >您必須依照「準備安裝AEM表單」中應用程式伺服器的適當章節中所述， [設定JAVA_HOME目錄](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*。*

1. 在單行上運行以下命令：

   * (Windows)主機名稱主機名 `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*,*埠號`] [-port=`** , `] [-user=`*用&#x200B;*戶`] [-password=`** 名密碼 `]`
   * (Linux, UNIX)埠號 `LCBackupMode.sh leaveContinuousCoverage [-Host=`*主機&#x200B;*名`] [-port=`*稱*`] [-user=`*,*密`] [-password=`*碼* 碼A `]`

      在上面的命令中，佔位符的定義如下：

      `Host` 是執行AEM表單的主機名稱。

      `port` 是應用程式伺服器上執行AEM表單的埠。

      `user` 是AEM表單管理員的使用者名稱。

      `password` 是AEM表單管理員的密碼。

      `leaveContinuousCoverage` 使用此選項可完全禁用滾動備份模式。
   >[!NOTE]
   >
   >在備份模式關閉時，無法重新建立連續覆蓋。 在此期間的任何變更都不受保護。

   >[!NOTE]
   >
   >如果在資料庫中啟用了文檔儲存，則快照備份模式和滾動備份模式不適用。

   有關備份模式的命令行介面的詳細資訊，請參閱BackupRestoreCommandline目錄中的自述檔案。

