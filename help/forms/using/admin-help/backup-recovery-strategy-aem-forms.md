---
title: 表單的備份和恢復策AEM略
seo-title: Backup and recovery strategy for AEM forms
description: 瞭解如何實施備份資料的策略並確保其與表單資料保持AEM同步。
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

# 表單的備份和恢復策AEM略{#backup-and-recovery-strategy-for-aem-forms}

如果您AEM的表單實現將其他自定義資料儲存在不同的資料庫中，則您負責實施一個策略來備份此資料並確保其與表單數AEM據保持同步。 此外，必須設計應用程式，使其足夠強健，以處理附加資料庫不同步的情況。 強烈建議在事務的上下文中執行任何資料庫操作，以幫助保持一致狀態。

確定表單的使AEM用方式後，確定必須備份哪些檔案、備份頻率以及備份窗口的可用性。

>[!NOTE]
>
>與表單實施的其他方面一樣AEM，備份和恢復策略必須在開發或試運行環境中進行開發和測試，然後才能用於生產，以確保整個解決方案能夠按預期工作而不丟失資料。

Adobe Experience Manager(AEM)是形式的一個AEM組成部分。 因此，您AEM需要備份並與表AEM單同步，因為Tergence Management解決方案和服務（如Formence Manager）基於部分表單中儲存的資料。為防止資料丟失，必須以一種方式備份表單特定資料AEM，以確保GDS和資料庫（關聯）。已還原到與原始DNS名稱相同的電腦。

## 備份類型 {#types-of-backups}

表單AEM備份策略涉及兩種備份類型：

**系統映像：** 如果硬碟或整個電腦停止工作，則可以使用完整的系統備份還原電腦的內容。 系統映像備份僅在表單的生產部署之前AEM必需。 然後，公司內部策略規定需要系統映像備份的頻率。

**AEM表單特定資料：** 應用程式資料存在於資料庫、全局文檔儲存(GDS)AEM和儲存庫中，必須即時備份。 GDS是一個目錄，用於儲存進程內使用的長壽命檔案。 這些檔案可能包括PDF、策略或表單模板。

>[!NOTE]
>
>如果安裝了Content Services（已棄用），還請備份Content Storage Root目錄。 請參閱 [內容儲存根目錄（僅限Content Services）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only)。

資料庫用於儲存對GDS檔案的表單對象、服務配置、進程狀態和資料庫引用。 如果在資料庫中啟用文檔儲存，則GDS中的持久性資料和文檔也儲存在資料庫中。 可以使用以下方法備份和恢復資料庫：

* **快照備份** mode指示AEMforms系統處於無限期備份模式或指定的分鐘數內，此後不再啟用備份模式。 要進入或離開快照備份模式，可以使用以下選項之一。 恢複方案後，不應啟用快照備份模式。

   * 使用Administration Console中的「備份設定」頁。 要進入快照模式，請選中「在安全備份模式下操作」複選框。 取消選中複選框以退出快照模式。
   * 使用LCBackupMode指令碼(請參見 [備份資料庫、 GDS和內容儲存根目錄](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories))。 要退出快照備份模式，請在指令碼參數中設定 `continuousCoverage` 參數 `false` 或 `leaveContinuousCoverage` 的雙曲餘切值。
   * 使用提供的備份/恢復API。 <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **滾動備份** mode指示系統始終處於備份模式，新備份模式會話在上一個會話釋放後立即啟動。 沒有超時與滾動備份模式關聯。 調用LCBackupMode指令碼或API以退出滾動備份模式時，將開始新的滾動備份模式會話。 此模式對於支援連續備份非常有用，但仍允許將舊的和不需要的文檔從GDS目錄中清除。 「備份和恢復」頁不支援滾動備份模式。 恢複方案後，仍然啟用滾動備份模式。 使用LCBackupMode指令碼和 `leaveContinuousCoverage` 的雙曲餘切值。

>[!NOTE]
>
>離開滾動備份模式會立即開始新的備份模式會話。 要完全禁用滾動備份模式，請使用 `leaveContinuousCoverage` 的子菜單。 在快照備份模式下，您可能會像通常那樣退出備份模式。

為防止資料丟失，AEM必須以一種確保GDS和內容儲存根目錄文檔與資料庫引用關聯的方式備份表單特定資料。

>[!NOTE]
>
>當GDS儲存在檔案系統上而不是資料庫中時，在GDS備份之前執行資料庫備份。

## 備份和恢復的特殊注意事項 {#special-considerations-for-backup-and-recovery}

如果由於以下更改而AEM必須將表單恢復到其他環境中，請使用以下准則：

* 更改Forms伺服器的IP地址、主機名AEM或埠
* 更改驅動器盤符或目錄路徑
* 更改為其他資料庫主機、埠或名稱

通常，此類恢複方案是由承載應用程式伺服器、資料庫伺服器或表單伺服器的伺服器的硬體故障引起的。 除本節AEM中介紹的特定於表單的配置外，如果表單伺服器的主機名或IP地址發生更改，還應對表單部署的其AEM他部分（如負載平衡器和防火牆）進行必要AEM的更改。

### 無法更改的內容 {#what-cannot-be-changed}

即使您可以更改資料庫伺服器和許多其他參數，但在從備份中恢復表單時，您也不能更改應用伺服器AEM類型或資料庫類型。 例如，如果要恢復表單AEM備份，則無法將應用程式伺服器從JBoss更改為WebLogic或資料庫從Oracle更改為DB2。 此外，恢復的AEM表單必須使用相同的檔案系統路徑，如字型目錄。

### 恢復後重新啟動 {#restarting-after-a-recovery}

在恢復後重新啟動forms伺服器之前，請執行以下操作：

1. 以維護模式啟動系統。
1. 執行以下操作以確保表單管理器與維AEM護模式下的表單同步：

   1. 請訪問https://&lt;*伺服器*>:&lt;*埠*>/lc/fm ，並使用管理員/密碼憑據登錄。
   1. 按一下右上角的用戶名稱（本例中為「超級管理員」）。
   1. 按一下 **管理選項**。
   1. 按一下 **開始** 以同步儲存庫中的資產。

1. 在群集環境中，主節點(相對於AEM)應位於次節點之前。
1. 確保在驗證系統的正常操作之前，不會從內部或外部源（如Web、SOAP或EJB進程啟動器）啟動任何進程。

如果主表AEM單資料庫被移動或更改，請查看與應用程式伺服器相關的安裝指南，以獲取有關更新表單資料源IDP_DS和AEMEDC_DS的資料庫連接資訊的資訊。

### 更改AEM表單主機名或IP地址 {#changing-the-aem-forms-hostname-or-ip-address}

在群集中，如果使用TCP快取而不是UDP ，則必須更新快取定位器配置。 請參閱與應用程式伺服器相關的配置指南中的「配置快取定位器（僅使用TCP進行快取）」。

### 更改表AEM單節點檔案系統路徑 {#changing-the-aem-forms-node-file-system-paths}

如果更改獨立節點的檔案系統路徑，則必須更新首選項、其他系統配置、自定義應用程式和已部署的表單應用程式中的相AEM應引用。 另一方面，對於群集，所有節點必須使用相同的檔案系統路徑配置。 必須設定全局文檔儲存(GDS)根目錄，並確保它指向與恢復的資料庫同步的已恢復GDS的副本。 設定GDS路徑非常重要，因為GDS可以包含要在應用程式伺服器重新啟動期間保留的資料。

在群集環境中，在備份之前和恢復之後，儲存庫的檔案系統路徑配置應與所有群集節點相同。

使用 `LCSetGDS`指令碼 `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` 資料夾以在更改檔案系統路徑後設定GDS路徑。 查看 `ReadMe.txt` 的子檔案。 如果無法使用舊GDS目錄路徑， `LCSetGDS` 在啟動表單之前，必須使用指令碼來設定GDS的新路AEM徑。

>[!NOTE]
>
>在這種情況下，您應使用此指令碼更改GDS位置。 要在表單運行時更AEM改GDS位置，請使用管理控制台。 (請參閱 [配置常規AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.)*

設定GDS路徑後，以維護模式啟動forms伺服器，並使用管理控制台更新新節點的其餘檔案系統路徑。 在驗證所有必要的配置都已更新後，重新啟動並testAEM表單。
