---
title: AEM表單的備份和恢復策略
seo-title: Backup and recovery strategy for AEM forms
description: 了解如何實作策略以備份資料，並確保其與AEM表單資料保持同步。
seo-description: Learn how to implement a strategy to back up data and ensuring that it remains in sync with the AEM forms data.
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 0%

---

# AEM表單的備份和恢復策略{#backup-and-recovery-strategy-for-aem-forms}

如果您的AEM表單實作會將其他自訂資料儲存在不同的資料庫中，您有責任實作策略以備份此資料，並確保其與AEM表單資料保持同步。 此外，必須設計應用程式，使其足夠強大，以處理其他資料庫不同步的情況。 強烈建議在事務的上下文中執行所執行的任何資料庫操作，以幫助保持一致的狀態。

在確定如何使用AEM表單後，確定必須備份哪些檔案、備份頻率以及備份窗口。

>[!NOTE]
>
>與AEM表單實施的任何其他方面一樣，您的備份和恢復策略必須在開發或測試環境中開發和測試，然後才用於生產，以確保整個解決方案能夠正常運作，不會丟失資料。

Adobe Experience Manager(AEM)是AEM表單的必要部分。 因此，您需要備份AEM並與AEM表單備份同步，因為通信管理解決方案和服務（如forms manager）基於儲存在AEM部分的資料。為避免任何資料丟失，必須備份AEM表單特定資料，以確保GDS和AEM（儲存庫）與資料庫引用相關聯。必須將資料庫、GDS、AEM和內容儲存根目錄還原到與原始目錄具有相同DNS名稱的電腦。

## 備份類型 {#types-of-backups}

AEM表單備份策略涉及兩種備份類型：

**系統映像：** 完整的系統備份，當硬碟或整台電腦停止工作時，可用於還原電腦的內容。 系統映像備份僅在生產部署AEM表單之前是必需的。 然後，內部公司策略規定系統映像備份的需要頻率。

**AEM表單特定資料：** 應用程式資料存在於資料庫、全局文檔儲存(GDS)和AEM儲存庫中，必須即時備份。 GDS是一個目錄，用於儲存進程內使用的長期檔案。 這些檔案可能包括PDF、策略或表單模板。

>[!NOTE]
>
>如果安裝了「內容服務」（已廢止），請同時備份「內容儲存根目錄」。 請參閱 [內容儲存根目錄（僅限內容服務）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

資料庫用於儲存表單對象、服務配置、進程狀態和對GDS檔案的資料庫引用。 如果在資料庫中啟用了文檔儲存，則GDS中的持久資料和文檔也會儲存在資料庫中。 可以使用以下方法備份和恢復資料庫：

* **快照備份** mode表示AEM forms系統處於無限期備份模式，或處於指定的分鐘數，之後不再啟用備份模式。 要進入或離開快照備份模式，可以使用以下選項之一。 恢複方案後，不應啟用快照備份模式。

   * 使用管理控制台中的「備份設定」頁。 要進入快照模式，請選中「在安全備份模式下操作」複選框。 取消選中複選框以退出快照模式。
   * 使用LCBackupMode指令碼(請參見 [備份資料庫、GDS和內容儲存根目錄](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories))。 要退出快照備份模式，請在指令碼參數中設定 `continuousCoverage` 參數 `false` 或使用 `leaveContinuousCoverage` 選項。
   * 使用提供的備份/恢復API。 <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **滾動備份** 模式指示系統始終處於備份模式，新備份模式會話在前一會話釋放後立即啟動。 沒有超時與滾動備份模式相關聯。 當調用LCBackupMode指令碼或API以離開滾動備份模式時，將開始新的滾動備份模式會話。 此模式對於支援連續備份非常有用，但仍允許將舊的和不需要的文檔清除出GDS目錄。 「備份和恢復」頁不支援滾動備份模式。 恢複方案後，仍將啟用滾動備份模式。 通過使用LCBackupMode指令碼和 `leaveContinuousCoverage` 選項。

>[!NOTE]
>
>若離開滾動式備份模式，則會立即開始新的備份模式會話。 要完全禁用滾動備份模式，請使用 `leaveContinuousCoverage` 選項，會覆寫現有的滾動式備份工作階段。 在快照備份模式下，您可能會像通常那樣離開備份模式。

為防止資料丟失，AEM表單特定資料的備份方式必須確保GDS和內容儲存根目錄文檔與資料庫引用相互關聯。

>[!NOTE]
>
>當GDS儲存在檔案系統而不是資料庫中時，在GDS備份之前執行資料庫備份。

## 備份和恢複方面的特殊考量 {#special-considerations-for-backup-and-recovery}

如果您因下列變更而必須將AEM表單復原至不同環境，請使用下列准則：

* 變更AEM表單伺服器的IP位址、主機名稱或埠
* 更改驅動器盤符或目錄路徑
* 更改到不同的資料庫主機、埠或名稱

通常，此類恢複方案是由承載應用程式伺服器、資料庫伺服器或表單伺服器的伺服器的硬體故障造成的。 除了本節所述的AEM表單專用設定外，如果AEM表單伺服器的主機名稱或IP位址變更，您也應為AEM表單部署的其他部分（例如負載平衡器和防火牆）進行必要的變更。

### 無法變更的項目 {#what-cannot-be-changed}

即使您可以更改資料庫伺服器和許多其他參數，但在從備份中恢復AEM表單時，您無法更改應用程式伺服器類型或資料庫類型。 例如，如果您正在恢復AEM表單備份，則無法將應用程式伺服器從JBoss更改為WebLogic或資料庫從Oracle更改為DB2。 此外，恢復的AEM表單必須使用相同的檔案系統路徑，如字型目錄。

### 恢復後重新啟動 {#restarting-after-a-recovery}

在恢復後重新啟動表單伺服器之前，請執行以下操作：

1. 以維護模式啟動系統。
1. 請執行下列操作，確保在維護模式下將Form Manager與AEM Forms同步：

   1. 轉到https://&lt;*伺服器*>:&lt;*埠*>/lc/fm ，並使用管理員/密碼憑據登錄。
   1. 按一下右上角的使用者名稱（此為「超級管理員」）。
   1. 按一下 **管理選項**.
   1. 按一下 **開始** 從存放庫同步資產。

1. 在群集環境中，主節點(相對於AEM)應位於次節點之前。
1. 確保在驗證系統的正常操作之前，不會從內部或外部源（如Web、SOAP或EJB進程啟動器）啟動任何進程。

如果移動或更改了主AEM表單資料庫，請查看與您的應用程式伺服器相關的安裝指南，以了解有關更新AEM表單資料源IDP_DS和EDC_DS的資料庫連接資訊的資訊。

### 變更AEM表單主機名稱或IP位址 {#changing-the-aem-forms-hostname-or-ip-address}

在群集中，如果使用TCP快取而不是UDP，則必須更新快取定位器配置。 請參閱與應用程式伺服器相關的配置指南中的「配置快取定位器（僅使用TCP快取）」。

### 更改AEM Forms節點檔案系統路徑 {#changing-the-aem-forms-node-file-system-paths}

如果更改獨立節點的檔案系統路徑，則必須在首選項、其他系統配置、自定義應用程式和部署的AEM表單應用程式中更新相應的引用。 另一方面，對於群集，所有節點必須使用相同的檔案系統路徑配置。 必須設定全局文檔儲存(GDS)根目錄，並確保它指向與恢復的資料庫同步的已恢復GDS的副本。 設定GDS路徑很重要，因為GDS可以包含要在應用程式伺服器重新啟動期間保存的資料。

在群集環境中，備份前和恢復後，儲存庫的檔案系統路徑配置應與所有群集節點相同。

使用 `LCSetGDS`指令碼 `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` 資料夾，以在更改檔案系統路徑後設定GDS路徑。 請參閱 `ReadMe.txt` 檔案以取得詳細資訊。 如果無法使用舊的GDS目錄路徑， `LCSetGDS` 在啟動AEM表單之前，必須使用指令碼來設定GDS的新路徑。

>[!NOTE]
>
>這種情況是您唯一應使用此指令碼來更改GDS位置的情況。 要在AEM表單運行時更改GDS位置，請使用管理控制台。 (請參閱 [配置一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.)*

設定GDS路徑後，以維護模式啟動表單伺服器，並使用管理控制台為新節點更新剩餘的檔案系統路徑。 確認所有必要的設定皆已更新後，請重新啟動並測試AEM表單。
