---
title: 在群集環境中進行備份和恢復的策略
seo-title: Strategy for backup and restore in a clustered environment
description: 如果您的AEM表單實作會將其他自訂資料儲存在不同的資料庫中，您必須實作策略來備份此資料，以確保其與AEM表單資料保持同步。
seo-description: If your AEM forms implementation stores additional custom data in a different database, you must implement a strategy to back up this data ensuring that it remains in sync with the AEM forms data.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 0%

---

# 在群集環境中進行備份和恢復的策略 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>如果您的AEM表單實作會將其他自訂資料儲存在不同的資料庫中，您必須實作策略來備份此資料，以確保其與AEM表單資料保持同步。 此外，必須設計應用程式，使其足夠強大，以處理其他資料庫不同步的情況。 強烈建議在事務的上下文中執行所執行的任何資料庫操作，以幫助保持一致的狀態。

您需要備份AEM表單系統的以下部分，才能從任何錯誤中恢復：

* AEM表單使用的資料庫
* 具有長期資料和其他持久文檔的GDS
* AEM資料庫(crx-repository)

>[!NOTE]
>
>您需要備份AEM表單設定程式正在使用的任何其他資料，例如客戶字型、連接器資料等。

## 備份群集環境 {#back-up-a-clustered-environment}

本主題探討備份任何AEM表單叢集環境的下列策略：

* 離線備份，並且停機
* 無停機的離線備份（關閉的次節點備份）
* 線上備份，無停機，但響應延遲
* 備份Bootstrap屬性檔案

### 離線備份，並且停機 {#offline-backup-with-downtime}

1. 關閉整個群集和相關服務。 (請參閱 [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何節點上，備份資料庫、GDS和連接器。 (請參閱 [要備份和恢復的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 執行下列步驟離線備份AEM存放庫：

   1. 對於每個群集節點，備份包含群集節點id的檔案。
   1. 備份任何輔助群集節點的所有檔案，包括子目錄。
   1. 分別備份每個群集節點的儲存庫/系統ID。

   如需詳細步驟，請參閱 [備份和還原](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. 備份任何其他資料，例如客戶字型。
1. 再次啟動群集。

### 無停機的離線備份 {#offline-backup-with-no-downtime}

1. 進入滾動備份模式。 (請參閱 [進入備份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   請注意，在恢復後，我們需要離開滾動備份模式。

1. 關閉與AEM相關的群集的任何輔助節點。 (請參閱 [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何節點上，備份資料庫、GDS和連接器。 (請參閱 [要備份和恢復的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 執行下列步驟離線備份AEM存放庫：

   1. 對於每個群集節點，備份包含群集節點id的檔案。
   1. 備份任何輔助群集節點的所有檔案，包括子目錄。
   1. 分別備份每個群集節點的repository/system.id。

   如需詳細步驟，請參閱 [備份和還原](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. 備份任何其他資料，例如客戶字型。
1. 再次啟動群集。

### 線上備份，無停機，但響應延遲 {#online-backup-with-no-downtime-but-delay-in-response}

1. 進入滾動備份模式。 (請參閱 [進入備份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   請注意，恢復後，您需要離開滾動備份模式。

1. 關閉與AEM相關的群集的任何輔助節點。 (請參閱 [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何節點上，備份資料庫、GDS和連接器。 (請參閱 [要備份和恢復的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 執行下列步驟以線上備份AEM存放庫：

   1. 對於每個群集節點，備份包含cluster_node.id的檔案。
   1. 分別備份每個群集節點的repository/system.id。
   1. 在任何輔助節點上，對儲存庫進行聯機備份，以了解詳細步驟，請參閱聯機備份。

1. 備份任何其他資料，例如客戶字型。
1. 再次啟動群集。

### 備份Bootstrap屬性檔案 {#back-up-the-bootstrap-properties-file}

建立AEM群集時，會在應用程式伺服器中為所有次節點建立屬性檔案。 建議備份Bootstrap屬性檔案。 您可以在應用程式伺服器上的以下位置找到檔案：

* JBoss:（在BIN目錄中）
* WebLogic:在域目錄中
* WebSphere:在配置檔案目錄中

您需要備份該檔案以備AEM次節點的災難恢復情況，如果恢復，則在應用程式伺服器上的指定位置替換該檔案。

## 在群集環境中恢復 {#recovery-in-a-clustered-environment}

如果整個群集或單個節點出現任何故障，則需要使用備份來還原它。

對於單節點恢復，只需關閉單節點並運行單節點恢復過程。

如果整個群集因資料庫崩潰等故障而失敗，則需要執行以下步驟。 恢復取決於使用的備份方法。

### 還原單個節點 {#restoring-a-single-node}

1. 停止損壞的節點。

   >[!NOTE]
   >
   >如果損壞的節點是AEM主節點，請關閉整個群集節點。

1. 從系統映像重新建立物理系統。
1. 將修補程式或更新套用至建立影像後所套用的AEM表單。 備份過程中記錄了此資訊。 AEM表單必須恢復到備份系統時的相同修補程式級別。
1. (*可選*)如果其他所有節點都正常運作，AEM存放庫也可能已損毀。 在此情況下，您會在AEM存放庫的error.log檔案中看到存放庫未同步訊息。

   要還原儲存庫，請執行以下步驟。

   >[!NOTE]
   >
   >如果壓縮的crx儲存庫備份已聯機，請在任何位置將其解壓縮，然後按照離線還原過程進行。

   1. 在節點的clusterNode目錄中刪除儲存庫、共用目錄、版本目錄和工作區目錄。
   1. 將群集節點的備份（包括子目錄）還原到節點。
   1. 刪除節點上的檔案clusterNode/revision.log。
   1. 刪除節點上的.lock（如果存在）。
   1. 刪除節點上的repository/system.id（如果存在）。
   1. 刪除節點上的檔案&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 為單個群集節點還原repository/cluster_node.id。

>[!NOTE]
>
>請考量下列幾點：

* 如果失敗的節點是AEM主節點，請將輔助儲存庫資料夾（crx-repository\crx.0000，其中0000可以是任何數字）中的所有內容複製到crx-repository\儲存庫資料夾，並刪除輔助儲存庫資料夾。
* 重新啟動任何群集節點之前，請確保從主節點刪除儲存庫/clustered.txt。
* 請確定主節點是先啟動的，一旦完全啟動，就啟動其他節點。

### 還原整個群集 {#restoring-the-entire-cluster}

1. 停止所有群集節點。
1. 從系統映像中重新建立物理系統。
1. 將修補程式或更新套用至建立影像後所套用的AEM formsAEM表單。 此資訊記錄在備份過程的步驟1中。 AEM表單必須恢復到備份系統時的相同修補程式級別。
1. 還原資料庫、GDS和連接器。
1. 執行下列操作以離線恢復AEM儲存庫：

   >[!NOTE]
   >
   >如果壓縮的crx儲存庫備份已聯機，請在任何位置將其解壓縮，然後按照離線還原過程進行。

   1. 在所有群集節點上，刪除clusterNode目錄中的儲存庫、共用目錄、版本目錄和工作區目錄。
   1. 刪除共用目錄中的所有檔案和目錄。
   1. 將群集節點（包括子目錄）的備份還原到一個群集節點。
   1. 將還原的群集節點的所有檔案複製到所有其他群集節點。 完成後，每個群集節點都包含相同的資料。
   1. 刪除所有群集節點上的檔案clusterNode/revision.log。
   1. 刪除所有群集節點上的.lock（如果存在）。
   1. 刪除repository/system.id所有群集節點（如果存在）。
   1. 刪除所有群集節點上的檔案&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 為單個群集節點還原repository/cluster_node.id。

>[!NOTE]
>
>請考量下列幾點：

* 如果失敗的節點是AEM主節點，請將從次要存放庫資料夾（看起來類似crx-repository\crx.0000，其中000可以是任何位數）中的所有內容複製到crx-repository\存放庫資料夾。
* 重新啟動任何群集節點之前，請確保從主節點刪除儲存庫/clustered.txt。
* 請確定主節點是先啟動的，一旦完全啟動，就啟動其他節點。

## 備份和還原通信管理解決方案發佈節點 {#back-up-and-restore-correspondence-management-solution-publish-node}

發佈者節點在群集環境中沒有任何主次關係。 您可以通過以下方式備份任何Publisher節點 [備份和還原](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

### 恢復單個發佈者節點 {#recover-a-single-publisher-node}

1. 關閉需要恢復的節點，在該節點再次啟動之前，不執行任何發佈活動。
1. 使用 [還原備份](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring備份)。

### 恢復群集 {#recover-a-cluster}

1. 關閉群集。
1. 使用 [還原備份](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring備份)。
1. 啟動主節點，然後啟動製作叢集的次節點。
