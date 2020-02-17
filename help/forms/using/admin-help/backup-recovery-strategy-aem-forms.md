---
title: AEM表單的備份和恢復策略
seo-title: AEM表單的備份和恢復策略
description: 瞭解如何實作策略以備份資料，並確保其與AEM表單資料保持同步。
seo-description: 瞭解如何實作策略以備份資料，並確保其與AEM表單資料保持同步。
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM表單的備份和恢復策略{#backup-and-recovery-strategy-for-aem-forms}

如果您的AEM表單實作將其他自訂資料儲存在不同的資料庫，您有責任實作策略來備份此資料，並確保其與AEM表單資料保持同步。 此外，應用程式必須經過設計，才能夠處理額外資料庫不同步的情況。 強烈建議在事務的上下文中執行任何資料庫操作，以幫助維持一致狀態。

在您識別AEM表格的使用方式後，請決定哪些檔案必須備份、備份的頻率，以及備份視窗。

>[!NOTE]
>
>如同您AEM表單實作的任何其他方面，您的備份與復原策略必須在開發或測試環境中進行開發與測試，才能用於生產環境，以確保整個解決方案能如預期般運作，而不會造成資料遺失。

Adobe Experience Manager(AEM)是AEM表單的一個組成部分。 因此，您必須備份AEM，並與AEM表單備份同步，因為Correponse Management Solution和服務（例如Forms Manager）是以儲存在AEM表單AEM部分的資料為基礎。為避免資料遺失，AEM表單特定資料必須以一種方式進行備份，以確保GDS和AEM（儲存庫）與資料庫參考資料庫建立關聯。、GDS、AEM和內容儲存根目錄必須還原至與原始DNS名稱相同的電腦。

## 備份類型 {#types-of-backups}

AEM表單備份策略包含兩種備份類型：

**** 系統映像：完整的系統備份，當硬碟或整個電腦停止工作時，可用於恢復電腦內容。 系統映像備份僅在生產部署AEM表單之前才需要。 然後，內部公司策略決定需要系統映像備份的頻率。

**** AEM表單特定資料：應用程式資料存在於資料庫、全域檔案儲存(GDS)和AEM儲存庫中，且必須即時備份。 GDS是一個目錄，用於儲存進程中使用的長壽命檔案。 這些檔案可能包含PDF、原則或表單範本。

***注意&#x200B;**:如果已安裝Content Services（已過時），也請備份Content Storage Root目錄。 (請參[閱內容儲存根目錄（僅限Content Services）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only)。)*

資料庫用於儲存表單對象、服務配置、進程狀態和對GDS檔案的資料庫引用。 如果您在資料庫中啟用了文檔儲存，則GDS中的持久資料和文檔也會儲存在資料庫中。 可以使用以下方法備份和恢復資料庫：

* **快照備份** 模式表示AEM表單系統處於無限期備份模式，或處於指定的分鐘數內，之後不再啟用備份模式。 要進入或離開快照備份模式，可使用以下選項之一。 恢複方案後，不應啟用快照備份模式。

   * 使用「管理控制台」中的「備份設定」頁。 要進入快照模式，請選中「在安全備份模式下操作」複選框。 取消選中複選框以退出快照模式。
   * 使用LCBackupMode指令碼(請 [參閱備份資料庫、GDS和內容儲存根目錄](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories))。 要退出快照備份模式，請在指令碼參數中將參 `continuousCoverage` 數設定為 `false` 或使用 `leaveContinuousCoverage` 選項。
   * 使用提供的備份／恢復API。 <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **滾動備份模式** (Rolling backup mode)表示系統始終處於備份模式，新備份模式會話在前一會話發佈後立即啟動。 沒有超時與滾動備份模式關聯。 當調用LCBackupMode指令碼或API以離開滾動備份模式時，將開始新的滾動備份模式會話。 此模式對於支援連續備份非常有用，但仍允許將舊的和不需要的文檔從GDS目錄中清除。 「備份和恢復」頁不支援滾動備份模式。 恢複方案後，仍然啟用滾動備份模式。 通過使用帶有選項的LCBackupMode指令碼，可以離開連續備份模式(滾動備份 `leaveContinuousCoverage` 模式)。

*注&#x200B;**意**:離開滾動備份模式會立即開始新的備份模式會話。 要完全禁用滾動備份模式，請使 `leaveContinuousCoverage` 用指令碼中的選項，該選項覆蓋現有滾動備份會話。 在快照備份模式下，您可以像通常那樣離開備份模式。*

為避免資料遺失，AEM表單的特定資料必須以確保GDS和內容儲存根目錄檔案與資料庫參考建立關聯的方式進行備份。

>[!NOTE]
>
>當GDS儲存在檔案系統中而不是儲存在資料庫中時，請在GDS備份之前執行資料庫備份。

## 備份和恢復的特殊注意事項 {#special-considerations-for-backup-and-recovery}

如果您因下列變更而必須將AEM表單復原到其他環境，請使用下列准則：

* 變更AEM Forms伺服器的IP位址、主機名稱或埠
* 更改驅動器盤符或目錄路徑
* 更改為不同的資料庫主機、埠或名稱

通常，此類恢復情形是由托管應用程式伺服器、資料庫伺服器或表單伺服器的伺服器的硬體故障引起的。 除了本節所述的AEM表單特定設定外，如果AEM表單伺服器的主機名稱或IP位址變更，您也應對AEM表單部署的其他部分（例如負載平衡器和防火牆）進行必要的變更。

### 無法變更的項目 {#what-cannot-be-changed}

即使您可以變更資料庫伺服器和許多其他參數，但在從備份中復原AEM表單時，您無法變更應用程式伺服器類型或資料庫類型。 例如，如果您要恢復AEM表單備份，則無法將應用程式伺服器從JBoss更改為WebLogic或資料庫從Oracle更改為DB2。 此外，已復原的AEM表單必須使用相同的檔案系統路徑，例如字型目錄。

### 恢復後重新啟動 {#restarting-after-a-recovery}

在恢復後重新啟動表單伺服器之前，請執行以下操作：

1. 以維護模式啟動系統。
1. 請執行下列動作，以確保「表單管理員」在維護模式中與AEM表單同步：

   1. 請前往https://&lt;*server*>:&lt;*port*>/lc/fm，並使用管理員／密碼憑證登入。
   1. 按一下右上角的使用者名稱（本例中為「超級管理員」）。
   1. 按一 **下管理選項**。
   1. 按一 **下「開始** 」，從儲存庫同步資產。

1. 在叢集環境中，主節點（與AEM相關）應在從節點之前啟動。
1. 確保在驗證系統正常操作之前，不會從內部或外部源（如Web、SOAP或EJB進程啟動器）啟動進程。

如果主要AEM表單資料庫已移動或變更，請參閱與您的應用程式伺服器相關的安裝指南，以取得更新AEM表單資料來源IDP_DS和EDC_DS資料庫連線資訊的相關資訊。

### 變更AEM表單的主機名稱或IP位址 {#changing-the-aem-forms-hostname-or-ip-address}

在群集中，如果使用TCP快取而不是UDP ，則必須更新快取定位器配置。 請參閱與應用程式伺服器相關的設定指南中的「設定快取定位器（僅使用TCP進行快取）」。

### 變更AEM表單節點檔案系統路徑 {#changing-the-aem-forms-node-file-system-paths}

如果您變更獨立節點的檔案系統路徑，則必須更新偏好設定、其他系統組態、自訂應用程式和部署的AEM表單應用程式中的適當參照。 另一方面，對於群集，所有節點必須使用相同的檔案系統路徑配置。 必須設定全局文檔儲存(GDS)根目錄，並確保它指向與恢復的資料庫同步的已恢復GDS的副本。 設定GDS路徑非常重要，因為GDS可以包含要在應用程式伺服器重新啟動期間保存的資料。

在群集環境中，在備份前和恢復後，儲存庫的檔案系統路徑配置應與所有群集節點的檔案系統路徑配置相同。

在更改 `LCSetGDS`檔案系統 `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` 路徑後，使用資料夾中的指令碼設定GDS路徑。 如需詳細 `ReadMe.txt` 資訊，請參閱相同檔案夾中的檔案。 如果無法使用舊的GDS目錄路徑， `LCSetGDS` 則在啟動AEM表單之前，必須使用指令碼來設定GDS的新路徑。

>[!NOTE]
>
>這種情況是您唯一應使用此指令碼來更改GDS位置的情況。 若要在AEM表單執行時變更GDS位置，請使用「管理控制台」。 (請參 [閱「設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*」)*

設定GDS路徑後，以維護模式啟動Forms伺服器，並使用管理控制台為新節點更新剩餘的檔案系統路徑。 在您確認所有必要的組態都已更新後，請重新啟動並測試AEM表格。
