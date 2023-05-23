---
title: 恢復表AEM單資料
seo-title: Recovering the AEM forms data
description: 本文檔介紹恢復表單資料所AEM需的步驟。
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---

# 恢復表AEM單資料 {#recovering-the-aem-forms-data}

本節介紹恢復表單資料所AEM需的步驟。 另請參閱 [備份和恢復的特殊注意事項](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery)。

>[!NOTE]
>
>資料庫、 GDS 、存AEM儲庫和內容儲存根目錄必須還原到與原始目錄具有相同DNS名稱的電腦。

表AEM單應可靠地從以下故障中恢復：

**磁碟故障：** 恢復資料庫內容需要最新的備份介質。

**資料損壞：** 檔案系統不記錄過去的事務，並且系統可能會意外覆蓋所需的進程資料。

**用戶錯誤：** 恢復僅限於資料庫提供的資料。 如果資料已儲存且可用，則恢復將簡化。

**停電、系統崩潰：** 檔案系統API通常設計或使用時不是穩健的，無法防止意外的系統故障。 如果發生停電或系統崩潰，儲存在資料庫中的文檔內容比儲存在檔案系統上的內容更可能是最新的。

如果使用滾動備份模式，則恢復後仍處於備份模式。 如果使用快照備份模式，則恢復後不處於備份模式。

從備份恢復到新系統時，以下配置可能不同。 此差異不應影響表單應用程式AEM的成功恢復：

* IP地址
* 物理系統配置（CPU、磁碟、記憶體）
* GDS位置

>[!NOTE]
>
>必須將內容儲存根目錄的備份還原到該目錄的位置，這與在Content Services配置過程中設定該目錄時的備份一樣。

如果多節點群集的單個節點出現故障，且該群集的其餘節點正常運行，請執行群集單節點恢復過程。

## 恢復表AEM單資料 {#recover-the-aem-forms-data}

1. 如果正在AEM運行，請停止forms服務和應用程式伺服器。
1. 如有必要，請從系統映像重新建立物理系統。 例如，如果恢復原因是資料庫伺服器故障，則可能不需要執行此步驟。
1. 將修補程式或更新應AEM用到自建立映像以來應用的表單。 此資訊記錄在備份過程中。 必AEM須將表單修補到與備份系統時相同的修補程式級別。
1. （WebSphere®應用程式伺服器）如果要恢復到WebSphere®應用程式伺服器的新實例，請運行restoreConfig.bat/sh命令。
1. 通過先使用AEM資料庫備份檔案運行資料庫還原操作，然後將事務重做日誌應用到恢復的資料庫，恢復表單資料庫。 (請參閱 [表AEM單資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。) 有關詳細資訊，請參閱以下知識文庫文章之一：

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [Oracle表單的備份和恢復AEM](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [表單的MySQL備份和恢復AEM](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. 通過先刪除現有窗體安裝上的GDS目錄內容AEM，然後從備份的GDS複製GDS目錄內容，恢復GDS目錄。 如果更改了GDS目錄位置，請參見 [在恢復期間更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。
1. 更名要還原的GDS備份目錄，如以下示例所示：

   >[!NOTE]
   >
   >如果/restore目錄已存在，請先備份該目錄，然後將其刪除，然後再更名包含最新資料的/backup目錄。

   * (JBoss®)更名 `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` 至：

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`。

   * (WebLogic)更名 `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` 至：

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`。

   * (WebSphere®)更名 `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` 至：

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`。

1. 通過先刪除現有表單安裝上的內容儲存根目錄的內容，然後按照單機或群集環境的任務進行恢復，AEM恢復內容儲存根目錄：

   >[!NOTE]
   >
   >必須將內容儲存根目錄的備份還原到內容儲存根目錄的位置，因為該目錄是在Content Services（已棄用）配置期間設定的。

   **獨立：** 在恢復過程中，恢復備份的所有目錄。 恢復這些目錄時，如果存在/backup-lucene-indexes目錄，請將其更名為/lucene-indexes。 否則，lucene-indexes目錄應已存在，無需執行任何操作。

   **群集：** 在恢復過程中，恢復備份的所有目錄。 要恢復索引根目錄，請在群集的每個節點上執行以下步驟：

   * 刪除索引根目錄中的所有內容。
   * 如果/backup-lucene-indexes目錄存在，請複製 *內容儲存根目錄*/backup-lucene-indexes目錄到索引根目錄並刪除 *內容儲存根目錄*/backup-lucene-indexes目錄。
   * 如果/lucene-indexes目錄存在，請複製 *內容儲存根目錄*/lucene-indexes目錄到索引根目錄。

1. 恢復/恢復CRX儲存庫。

   * **獨立**

      *還原作者和發佈實例*:如果發生災難，您可以通過執行中介紹的步驟將儲存庫恢復到上次備份狀態 [備份和恢復。](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

      「作者」節點的完全恢復也確定了「Forms管理器」和「AEM Forms工作區」資料的恢復。

   * **群集**

      有關在群集環境中恢復的資訊，請參見 [群集環境中備份和恢復的策略](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment)。

1. 刪除在AEMjava.io.temp目錄或Adobe臨時目錄中建立的任何表單臨時檔案。
1. 開始AEM表單(請參閱 [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->。

## 在恢復期間更改GDS位置 {#changing-the-gds-location-during-recovery}

如果GDS恢復到原來位置以外的位置，請運行LCSetGDS指令碼將GDS設定到新位置。 指令碼位於 `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` 的子菜單。 指令碼需要兩個參數， `defaultGDS` 和 `newGDS`。 查看 `ReadMe.txt` 檔案，瞭解有關如何運行指令碼的說明。

>[!NOTE]
>
>如果已在資料庫中啟用文檔儲存，則無需更改GDS位置。

>[!NOTE]
>
>在這種情況下，您應使用此指令碼更改GDS位置。 要在表單運行時更AEM改GDS位置，請使用管理控制台。 (請參閱 [配置常規AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。)

>[!NOTE]
>
>如果GDS目錄位於驅動器根目錄(例如D:\)，則Windows上的元件部署將失敗。 對於GDS，必須確保目錄不位於驅動器的根目錄，而位於子目錄中。 例如，目錄應為D:\GDS and not simply D:\。

## 將GDS恢復到群集環境 {#recovering-the-gds-to-a-clustered-environment}

要更改群集環境中的GDS位置，請關閉整個群集並在群集的單個節點上運行LCSetGDS指令碼。 (請參閱 [在恢復期間更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。) 僅啟動該節點。 當該節點完全啟動時，群集中的其他節點可以安全啟動，並將正確指向新的GDS。

>[!NOTE]
>
>如果無法確保在啟動其他節點之前完全啟動一個節點，則必須在啟動群集之前在群集中的每個節點上運行LCSetGDS指令碼。
