---
title: 恢復AEM表單資料
seo-title: Recovering the AEM forms data
description: 本檔案說明復原AEM表單資料所需的步驟。
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# 恢復AEM表單資料 {#recovering-the-aem-forms-data}

本節說明復原AEM表單資料所需的步驟。 另請參閱 [備份和恢複方面的特殊考量](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>必須將資料庫、GDS、AEM儲存庫和內容儲存根目錄還原到與原始目錄具有相同DNS名稱的電腦。

AEM表單應可從下列故障中可靠地復原：

**磁碟故障：** 恢復資料庫內容需要最新的備份介質。

**資料損壞：** 檔案系統不會記錄過去的事務，並且系統可能會意外覆蓋所需的進程資料。

**用戶錯誤：** 恢復僅限於資料庫提供的資料。 如果資料已儲存且可用，則可簡化恢復。

**斷電，系統崩潰：** 檔案系統API的設計或使用通常不是以可靠的方式來防止意外的系統故障。 如果發生電源中斷或系統崩潰，儲存在資料庫中的文檔內容比儲存在檔案系統上的內容更可能是最新的。

如果您使用滾動式備份模式，則恢復後仍處於備份模式。 如果使用快照備份模式，則恢復後不處於備份模式。

從備份還原到新系統時，以下配置可能不同。 此差異不應影響AEM表單應用程式的成功復原：

* IP位址
* 物理系統配置（CPU、磁碟、記憶體）
* GDS位置

>[!NOTE]
>
>必須將內容儲存根目錄的備份還原到該目錄的位置，因為在內容服務配置期間設定了該目錄。

如果多節點群集的單個節點出現故障，且群集的其餘節點正常運行，請執行群集單節點恢復過程。

## 恢復AEM表單資料 {#recover-the-aem-forms-data}

1. 如果運行，請停止AEM forms服務和應用程式伺服器。
1. 如有必要，請從系統映像中重新建立物理系統。 例如，如果恢復原因是錯誤的資料庫伺服器，則可能不需要執行此步驟。
1. 將修補程式或更新套用至建立影像後所套用的AEM表單。 此資訊已記錄在備份過程中。 AEM表單必須修補到與備份系統時相同的修補程式級別。
1. （WebSphere應用程式伺服器）如果要恢復到WebSphere應用程式伺服器的新實例，請運行restoreConfig.bat/sh命令。
1. 首先使用資料庫備份檔案運行資料庫還原操作，然後將事務重做日誌應用到恢復的資料庫，以恢復AEM表單資料庫。 (請參閱 [AEM forms資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) 如需詳細資訊，請參閱以下其中一篇知識庫文章：

   * [OracleAEM表單的備份和恢復](https://www.adobe.com/go/kb403624)
   * [AEM表單的MySQL備份和恢復](https://www.adobe.com/go/kb403625)
   * [Microsoft SQL Server針對AEM表單的備份和恢復](https://www.adobe.com/go/kb403623)
   * [AEM表單的DB2備份和恢復](https://www.adobe.com/go/kb403626)

1. 通過先在AEM表單的現有安裝上刪除GDS目錄的內容，然後從備份的GDS中複製GDS目錄的內容，恢復GDS目錄。 如果更改了GDS目錄位置，請參閱 [在恢復期間更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. 更名要還原的GDS備份目錄，如以下示例所示：

   >[!NOTE]
   >
   >如果/restore目錄已存在，請備份該目錄，然後刪除該目錄，然後再更名包含最新資料的/backup目錄。

   * (JBoss)重新命名 `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` 至：

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`。

   * (WebLogic)重新命名 `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` 至：

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`。

   * (WebSphere)更名 `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` 至：

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`。

1. 先在AEM表單的現有安裝上刪除內容儲存根目錄的內容，然後按照獨立或群集環境的任務進行恢復，以恢復內容儲存根目錄：

   >[!NOTE]
   >
   >必須將內容儲存根目錄的備份還原到內容儲存根目錄的位置，因為它是在內容服務（已廢止）配置期間設定的。

   **獨立：** 在恢復過程中，恢復所有已備份的目錄。 當恢復這些目錄時，如果/backup-lucene-indexes目錄存在，請將其更名為/lucene-indexes。 否則，lucene-indexes目錄應已存在，不需要執行任何操作。

   **群集：** 在恢復過程中，恢復所有已備份的目錄。 要還原Index Root目錄，請在群集的每個節點上執行以下步驟：

   * 刪除索引根目錄中的所有內容。
   * 如果/backup-lucene-indexes目錄存在，則複製 *內容儲存根目錄*/backup-lucene-indexes目錄到Index Root目錄，然後刪除 *內容儲存根目錄*/backup-lucene-indexes目錄。
   * 如果/lucene-indexes目錄存在，則複製 *內容儲存根目錄*/lucene-indexes目錄到索引根目錄。

1. 還原/恢復CRX-repository。

   * **獨立**

      *還原製作和發佈執行個體*:如果發生災難，您可以執行 [備份和還原。](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      完整還原「作者」節點也可確認還原Forms Manager和AEM Forms Workspace資料。

   * **群集**

      有關在群集環境中進行恢復的資訊，請參見 [在群集環境中進行備份和恢復的策略](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. 刪除在java.io.temp目錄或AEM臨時目錄中建立的任何Adobe表單臨時檔案。
1. 啟動AEM表單(請參閱 [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## 在恢復期間更改GDS位置 {#changing-the-gds-location-during-recovery}

如果將GDS還原到原始位置以外的位置，請運行LCSetGDS指令碼將GDS設定為新位置。 指令碼位於 `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` 檔案夾。 指令碼需要兩個參數， `defaultGDS` 和 `newGDS`. 請參閱 `ReadMe.txt` 檔案，以取得如何執行指令碼的說明。

>[!NOTE]
>
>如果已在資料庫中啟用文檔儲存，則無需更改GDS位置。

>[!NOTE]
>
>這種情況是您唯一應使用此指令碼來更改GDS位置的情況。 要在AEM表單運行時更改GDS位置，請使用管理控制台。 (請參閱 [配置一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>如果GDS目錄位於驅動器根目錄(如D:\)，則Windows上的元件部署將失敗。 對於GDS，必須確保目錄不位於驅動器的根目錄中，而位於子目錄中。 例如，目錄應為D:\GDS and not simply D:\。

## 將GDS恢復到群集環境 {#recovering-the-gds-to-a-clustered-environment}

要更改群集環境中的GDS位置，請關閉整個群集並在群集的單個節點上運行LCSetGDS指令碼。 (請參閱 [在恢復期間更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) 僅啟動該節點。 當該節點完全啟動時，群集中的其他節點可能會安全啟動，並且將正確指向新GDS。

>[!NOTE]
>
>如果在啟動其他節點之前無法確保完全啟動一個節點，則必須在啟動群集之前在群集中的每個節點上運行LCSetGDS指令碼。
