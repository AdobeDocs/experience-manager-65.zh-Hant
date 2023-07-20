---
title: 備份Adobe Experience Manager Forms資料
description: 本檔案說明完成Adobe Experience Manager (AEM)表單資料庫、GDS和內容儲存根目錄之即時或線上備份所需的步驟。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 0%

---

# 備份Adobe Experience Manager (AEM) Forms資料 {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

本節說明完成AEM Forms資料庫、GDS和內容儲存根目錄之即時或線上備份所需的步驟。

安裝AEM Forms並部署至生產區域後，資料庫管理員應執行資料庫的初始完整或冷備份。 必須關閉資料庫才能進行此備份。 然後，應該定期對資料庫進行差異或增量（或熱備份）。

為確保成功備份和復原，系統映像備份必須始終可用。 然後，如果發生遺失，您可以將整個環境復原到一致的狀態。

在GDS、AEM儲存庫和內容儲存根目錄備份的同時備份資料庫，有助於在需要復原時讓這些系統保持同步。

本節所述的備份程式要求您在備份AEM Forms資料庫、AEM儲存區域、GDS和內容儲存根目錄之前，先進入安全備份模式。 備份完成後，您必須退出安全備份模式。 安全備份模式用於標示位於GDS中的長期和持續性檔案。 此模式可確保自動檔案清理機制（檔案收集器）在釋放安全備份模式之前不會刪除過期的檔案。 必須使GDS備份與資料庫備份保持同步。

GDS位置的備份頻率取決於AEM Forms的使用方式以及可用的備份視窗。 備份期間可能會受到長期程式的影響，因為這些程式可能會執行幾天。 如果您持續變更、新增及移除此目錄中的檔案，您應該更頻繁地備份GDS位置。

如果資料庫是在記錄模式下執行（如上一節所述），則必須經常備份資料庫記錄檔，以便在發生媒體故障時可用來還原資料庫。

>[!NOTE]
>
>復原程式之後，未參考的檔案可能會保留在GDS目錄中。 這是目前已知的限制。

## 備份資料庫、GDS、AEM儲存庫和內容儲存根目錄 {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

您必須將AEM Forms置於安全備份（快照）模式或滾動備份（連續涵蓋範圍）模式。 在設定AEM Forms進入任一備份模式之前，請確定下列事項：

* 驗證系統版本，並記錄自上次執行完整系統映像備份後套用的修補程式或更新。
* 如果您使用滾動或快照模式備份，請確定您的資料庫已設定正確的記錄檔設定值，以允許對資料庫進行熱備份。 (請參閱 [AEM Forms資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

除了這些以外，請遵循以下備份/還原程式准則。

* 使用可用的作業系統或協力廠商備份公用程式來備份GDS目錄。 (請參閱 [GDS位置](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* （可選）使用可用的作業系統或協力廠商備份與公用程式來備份內容儲存根目錄。 (請參閱 [內容儲存根目錄位置（獨立環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) 或 [內容儲存根目錄位置（叢集環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* 備份作者和發佈執行個體（ crx -repository備份）。

  若要備份Correspondence Management Solution環境，請依照中的說明，對作者和發佈執行個體執行步驟 [備份與還原](/help/sites-administering/backup-and-restore.md).

  備份作者和發佈執行個體時，請考慮以下幾點：

   * 請確定製作和發佈執行個體的備份已同步處理，以便同時啟動。 雖然您可以在執行備份時繼續使用作者和發佈例項，但建議不要在備份期間發佈任何資產，以避免任何未擷取的變更。 等候製作和發佈執行個體的備份結束，然後再發佈新資產。
   * 「作者」節點的完整備份包括Forms Manager和AEM Forms Workspace資料的備份。
   * Workbench開發人員可以繼續在本機處理其程式。 他們不應在備份階段部署任何新程式。
   * 決定每個備份工作階段的長度（用於滾動備份模式）時，應依據備份AEM Forms中所有資料(DB、GDS、AEM存放庫和任何其他自訂資料)所花費的總時間。

備份AEM Forms資料庫，包括任何交易記錄。 另請參閱 [AEM Forms資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).

如需詳細資訊，請參閱適用於您資料庫的知識庫文章：
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [AEM Forms的Oracle備份與回覆](https://www.adobe.com/go/kb403624)
* [適用於AEM Forms的MySQL備份與復原](https://www.adobe.com/go/kb403625)
* [適用於AEM Forms的Microsoft® SQL Server備份與復原](https://www.adobe.com/go/kb403623)
* [適用於AEM Forms的DB2®備份與復原](https://www.adobe.com/go/kb403626)

這些文章提供基本資料庫功能的指引，以備份及復原資料。 這些指南並非特定廠商的資料庫備份與復原功能之包含所有內容的技術指南。 它們概述了為您的AEM Forms應用程式資料建立可靠資料庫備份策略所需的命令。

>[!NOTE]
>
>開始備份GDS之前，必須先完成資料庫備份。 如果資料庫備份未完成，表示您的資料不同步。

### 進入備份模式 {#entering-the-backup-modes}

您可以使用管理主控台、LCBackupMode指令或AEM Forms安裝提供的API來進入和離開備份模式。 對於滾動式備份（連續涵蓋範圍），管理控制檯選項無法使用；您應使用命令列選項或API。 <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>如果您在Forms伺服器上設定SSL，則無法使用LCBackupMode.CMD指令碼將Forms伺服器置於備份模式。

**使用管理主控台進入安全備份模式**

1. 登入管理主控台。
1. 按一下「設定」>「核心系統設定」>「備份公用程式」。
1. 選取「在安全備份模式下操作」，然後按一下「確定」。

   此方法會無限期地將AEM Forms置於備份模式（無逾時），且會進入快照模式，而非捲動備份模式。

**使用命令列選項進入安全備份模式**

您可以使用命令列介面 `LCBackupMode` 可將AEM Forms置於安全備份模式的指令碼。

1. 設定ADOBE_LIVECYCLE並啟動應用程式伺服器。
1. 前往 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 資料夾。
1. 根據您的作業系統，編輯 `LCBackupMode.cmd` 或 `LCBackupMode.sh` 指令碼，提供適用於您的系統的預設值。
1. 在命令提示字元下，在一行上執行下列命令：

   * (Windows) `LCBackupMode.cmd enter [-Host=`*主機名稱* `] [-port=`*portnumber* `] [-user=`*使用者名稱* `] [-password=`*密碼* `] [-label=`*標簽名稱* `] [-timeout=`*秒* `]`
   * (Linux®、UNIX®) `LCBackupMode.sh enter [-host=`*主機名稱* `] [-port=`*portnumber* `] [-user=`*使用者名稱* `] [-password=`*密碼* `] [-label=`*標簽名稱* `]`

   在前面的命令中，預留位置的定義如下：

   `Host` 是執行AEM Forms的主機名稱。

   `port` 是執行AEM Forms之應用程式伺服器的WebServices連線埠。

   `user` 是AEM Forms管理員的使用者名稱。

   `password` 是AEM Forms管理員的密碼。

   `label` 為此備份的文字標籤，可以是任何字串。

   `timeout` 是自動離開備份模式的秒數。 它可以是0到10,080。 如果預設值為0，則備份模式不會逾時。

   如需備份模式之命令列介面的詳細資訊，請參閱BackupRestoreCommandline目錄中的Readme檔案。

### 離開備份模式 {#leaving-backup-modes}

您可以使用管理主控台或命令列選項來離開備份模式。

**保留安全備份模式（快照模式）**

若要使用Administration Console將AEM Forms帶出安全備份模式（快照模式），請執行下列工作。

1. 登入管理主控台。
1. 按一下「設定」>「核心系統設定」>「備份公用程式」。
1. 取消選取「在安全備份模式下操作」，然後按一下「確定」。

**保留所有備份模式**

您可以使用命令列介面將AEM Forms帶出安全備份模式（快照模式）或結束目前的備份模式工作階段（滾動模式）。 您無法使用管理控制檯來離開正在復原的備份模式。 在捲動備份模式中，「管理主控台」上的「備份公用程式」控制項會停用。 使用API呼叫或使用LCBackupMode命令。

1. 前往 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 資料夾。
1. 根據您的作業系統，編輯 `LCBackupMode.cmd` 或 `LCBackupMode.sh` 指令碼，提供適用於您的系統的預設值。

   >[!NOTE]
   >
   >您必須依照應用程式伺服器的相關章節中所述設定JAVA_HOME目錄 [準備安裝AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. 在一行上執行下列命令：

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*主機名稱* `] [-port=`*portnumber* `] [-user=`*使用者名稱* `] [-password=`*密碼* `]`
   * (Linux®、UNIX®) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*主機名稱* `] [-port=`*portnumber* `] [-user=`*使用者名稱* `] [-password=`*密碼* `]`

     在前面的命令中，預留位置的定義如下：

     `Host` 是執行AEM Forms的主機名稱。

     `port` 是應用程式伺服器上執行AEM Forms的連線埠。

     `user` 是AEM Forms管理員的使用者名稱。

     `password` 是AEM Forms管理員的密碼。

     `leaveContinuousCoverage` 使用此選項可完全停用滾動備份模式。

   >[!NOTE]
   >
   >在備份模式關閉時，無法重新建立連續涵蓋範圍。 在此期間所做的任何變更都不會受到保護。

   >[!NOTE]
   >
   >如果您在資料庫中啟用了檔案儲存，則快照備份模式和捲動備份模式不適用。

   如需備份模式之命令列介面的詳細資訊，請參閱BackupRestoreCommandline目錄中的readme檔案。
