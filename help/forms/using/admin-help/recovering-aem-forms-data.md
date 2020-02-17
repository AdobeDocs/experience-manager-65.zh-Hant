---
title: 恢復AEM表單資料
seo-title: 恢復AEM表單資料
description: 本檔案說明恢復AEM表單資料所需的步驟。
seo-description: 本檔案說明恢復AEM表單資料所需的步驟。
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
translation-type: tm+mt
source-git-commit: 3e83611f6b30cee774b72194bee1d03e323a6a57

---


# 恢復AEM表單資料 {#recovering-the-aem-forms-data}

本節說明恢復AEM表單資料所需的步驟。 另請參閱 [備份和恢復的特殊注意事項](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery)。

>[!NOTE]
>
>必須將資料庫、GDS、AEM儲存庫和內容儲存根目錄還原至與原始DNS名稱相同的電腦。

AEM表單應可靠地從下列失敗中恢復：

**** 磁碟故障：恢復資料庫內容需要最新的備份介質。

**** 資料損毀：檔案系統不會記錄過去的事務，並且系統可能會意外覆寫所需的流程資料。

**** 用戶錯誤：恢復僅限於資料庫提供的資料。 如果資料已儲存且可用，則恢復將得到簡化。

**** 停電、系統崩潰：檔案系統API的設計或使用通常不是以強穩的方式，來防止意外的系統故障。 如果發生斷電或系統崩潰，儲存在資料庫中的文檔內容比儲存在檔案系統中的內容更可能是最新的。

如果使用滾動備份模式，則恢復後仍處於備份模式。 如果使用快照備份模式，則恢復後不處於備份模式。

從備份恢復到新系統時，以下配置可能不同。 此差異不應影響AEM表單應用程式的成功復原：

* IP位址
* 物理系統配置（CPU、磁碟、記憶體）
* GDS位置

>[!NOTE]
>
>必須將內容儲存根目錄的備份還原到該目錄的位置，就像在Content services配置過程中設定的一樣。

如果多節點群集的單個節點出現故障，且群集的其餘節點運行正常，請執行群集單節點恢復過程。

## 恢復AEM表單資料 {#recover-the-aem-forms-data}

1. 如果執行中，請停止AEM表單服務和應用程式伺服器。
1. 如有必要，從系統映像重新建立物理系統。 例如，如果恢復原因是有故障的資料庫伺服器，則可能不需要此步驟。
1. 將修補程式或更新套用至自影像建立以來套用的AEM表單。 此資訊記錄在備份過程中。 AEM表格必須修補至與備份系統時相同的修補程式層級。
1. （WebSphere應用程式伺服器）如果要恢復到新的WebSphere應用程式伺服器實例，請運行restoreConfig.bat/sh命令。
1. 首先使用資料庫備份檔案執行資料庫還原作業，然後將交易重做記錄檔套用至已復原的資料庫，以復原AEM表單資料庫。 (請參 [閱AEM表單資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。)如需詳細資訊，請參閱下列其中一篇知識庫文章：

   * [Oracle Backup and Recovery for AEM forms](https://www.adobe.com/go/kb403624)
   * [AEM表單的MySQL備份和恢復](https://www.adobe.com/go/kb403625)
   * [適用於AEM表單的Microsoft SQL server備份和恢復](https://www.adobe.com/go/kb403623)
   * [AEM表單的DB2備份和恢復](https://www.adobe.com/go/kb403626)

1. 請先刪除現有AEM表單安裝上的GDS目錄內容，然後從備份的GDS複製GDS目錄內容，以恢復GDS目錄。 如果更改了GDS目錄位置，請參 [閱在恢復過程中更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。
1. 更名要還原的GDS備份目錄，如以下示例所示：

   >[!NOTE]
   >
   >如果/restore目錄已存在，請備份該目錄，然後在更名包含最新資料的/backup目錄之前將其刪除。

   * (JBoss)重命 `[appserver root]/server/[server]/svcnative/DocumentStorage/backup` 名為：

      `[appserver root]/server/[server]/svcnative/DocumentStorage/restore`.

   * (WebLogic)重新命 `[appserverdomain]/[server]/adobe/AEMformsserver/DocumentStorage/backup` 名為：

      `[appserverdomain]/[server]/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere)重新命 `[appserver root]/installedApps/adobe/[server]/DocumentStorage/backup` 名為：

      `[appserver root]/installedApps/adobe/[server]/DocumentStorage/restore`.

1. 請先刪除現有AEM表單安裝上的「內容儲存根目錄」內容，然後依照單機或叢集環境的工作，以復原內容，以恢復「內容儲存根目錄」:

   >[!NOTE]
   >
   >必須將內容儲存根目錄的備份還原到內容儲存根目錄的位置，這與在內容服務（已過時）配置期間設定的內容儲存根目錄相同。

   **** 獨立作業：在恢復過程中，恢復所有已備份的目錄。 恢復這些目錄時，如果存在/backup-lucene-indexes目錄，請將其更名為/lucene-indexes。 否則，lucene-indexes目錄應已存在，不需要執行任何操作。

   **** 叢集：在恢復過程中，恢復所有已備份的目錄。 要恢復「索引根目錄」，請在群集的每個節點上執行以下步驟：

   * 刪除「索引根目錄」中的所有內容。
   * 如果/backup-lucene-indexes目錄存在，請將 *Content Storage Root directory*/backup-lucene-indexes目錄的內容複製到Index Root目錄，並刪除 *Content Storage Root directory*/backup-lucene-indexes目錄。
   * 如果/lucene-indexes目錄存在，請將 *Content Storage Root directory*/lucene-indexes目錄的內容複製到Index Root目錄。

1. 恢復／恢復CRX儲存庫。

   * **獨立作業**

      *還原作者和發佈例項*:如果發生災難，您可以通過執行備份和還原中所述的步驟將儲存庫還原到上次備份 [狀態。](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      「作者」節點的完整還原也會確認Forms manager和AEM Forms Workspace資料的還原。

   * **叢集**

      有關在群集環境中恢復的資訊，請參 [閱在群集環境中備份和恢復的策略](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment)。

1. 刪除在java.io.temp目錄或Adobe temp目錄中建立的任何AEM表單暫存檔案。
1. 啟動AEM表單(請參 [閱啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->。

## 在恢復過程中更改GDS位置 {#changing-the-gds-location-during-recovery}

如果您的GDS已還原至原來位置以外的位置，請執行LCSetGDS指令碼，將GDS設定至新位置。 該指令碼在資料夾 `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` 中。 該指令碼需要兩個參 `defaultGDS` 數 `newGDS`。 如需如 `ReadMe.txt` 何執行指令碼的指示，請參閱相同檔案夾中的檔案。

>[!NOTE]
>
>如果您已在資料庫中啟用檔案儲存功能，則不需要變更GDS位置。

>[!NOTE]
>
>這種情況是您唯一應使用此指令碼來更改GDS位置的情況。 若要在AEM表單執行時變更GDS位置，請使用「管理控制台」。 (請參 [閱「設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)」。)

>[!NOTE]
>
>如果GDS目錄位於驅動器根目錄(例如D:\)，則Windows上的元件部署將失敗。 對於GDS，必須確保該目錄不位於驅動器的根目錄，而位於子目錄中。 例如，目錄應為D:\GDS and not simply D:\。

## 將GDS恢復到群集環境 {#recovering-the-gds-to-a-clustered-environment}

要更改群集環境中的GDS位置，請關閉整個群集並在群集的單個節點上運行LCSetGDS指令碼。 (請參 [閱在恢復過程中更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。)僅啟動該節點。 當該節點完全啟動時，群集中的其他節點可以安全啟動，並將正確指向新的GDS。

>[!NOTE]
>
>如果不能確保在啟動其他節點之前完全啟動一個節點，則必須在啟動群集之前在群集中的每個節點上運行LCSetGDS指令碼。

