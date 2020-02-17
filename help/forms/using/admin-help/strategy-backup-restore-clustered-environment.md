---
title: 在群集環境中備份和恢復的策略
seo-title: 在群集環境中備份和恢復的策略
description: 如果您的AEM表單實作將其他自訂資料儲存在不同的資料庫，您必須實作策略來備份此資料，以確保其與AEM表單資料保持同步。
seo-description: 如果您的AEM表單實作將其他自訂資料儲存在不同的資料庫，您必須實作策略來備份此資料，以確保其與AEM表單資料保持同步。
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在群集環境中備份和恢復的策略 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>如果您的AEM表單實作將其他自訂資料儲存在不同的資料庫，您必須實作策略來備份此資料，以確保其與AEM表單資料保持同步。 此外，應用程式必須經過設計，才能夠處理額外資料庫不同步的情況。 強烈建議在事務的上下文中執行任何資料庫操作，以幫助維持一致狀態。

您必須備份AEM表單系統的下列部分，才能從任何錯誤中復原：

* AEM表單使用的資料庫
* 長期保存資料和其他持久性文檔的GDS
* AEM資料庫(crx-repository)

>[!NOTE]
>
>您需要備份AEM表單設定所使用的任何其他資料，例如客戶字型、連線器資料等。

## 備份群集環境 {#back-up-a-clustered-environment}

本主題討論以下策略，以備份任何AEM表單叢集環境：

* 離線備份與停機
* 無停機的離線備份（關閉的從節點備份）
* 線上備份，無停機但響應延遲
* 備份引導屬性檔案

### 離線備份與停機 {#offline-backup-with-downtime}

1. 關閉整個群集和相關服務。 (請參 [閱啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何節點上，備份資料庫、GDS和連接器。 (請參 [閱要備份和恢復的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 執行下列步驟，離線備份AEM儲存庫：

   1. 對於每個群集節點，備份包含群集節點ID的檔案。
   1. 備份任何從群集節點（包括子目錄）的所有檔案。
   1. 分別備份每個群集節點的儲存庫／系統ID。
   有關詳細步驟，請參 [閱備份和還原](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)。

1. 備份任何其他資料，例如客戶字型。
1. 再次啟動群集。

### 無停機的離線備份 {#offline-backup-with-no-downtime}

1. 進入滾動備份模式。 (請參 [閱進入備份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   請注意，在恢復後，我們需要離開滾動備份模式。

1. 關閉叢集中與AEM相關的任何從節點。 (請參 [閱啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何節點上，備份資料庫、GDS和連接器。 (請參 [閱要備份和恢復的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 執行下列步驟，離線備份AEM儲存庫：

   1. 對於每個群集節點，備份包含群集節點ID的檔案。
   1. 備份任何從群集節點（包括子目錄）的所有檔案。
   1. 分別備份每個群集節點的repository/system.id。
   有關詳細步驟，請參 [閱備份和還原](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)。

1. 備份任何其他資料，例如客戶字型。
1. 再次啟動群集。

### 線上備份，無停機但響應延遲 {#online-backup-with-no-downtime-but-delay-in-response}

1. 進入滾動備份模式。 (請參 [閱進入備份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   請注意，在恢復後，您需要離開滾動備份模式。

1. 關閉叢集中與AEM相關的任何從節點。 (請參 [閱啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何節點上，備份資料庫、GDS和連接器。 (請參 [閱要備份和恢復的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 執行下列步驟以線上備份AEM資料庫：

   1. 對於每個群集節點，備份包含cluster_node.id的檔案。
   1. 分別備份每個群集節點的repository/system.id。
   1. 在任何從節點上，對儲存庫執行聯機備份以獲得詳細步驟，請參閱聯機備份。

1. 備份任何其他資料，例如客戶字型。
1. 再次啟動群集。

### 備份引導屬性檔案 {#back-up-the-bootstrap-properties-file}

當我們建立AEM叢集時，會在應用程式伺服器中為所有從屬節點建立屬性檔案。 建議備份引導屬性檔案。 您可以在應用程式伺服器上的下列位置找到檔案：

* JBoss:在BIN目錄中
* WebLogic:在域目錄中
* WebSphere:在配置檔案目錄中

您需要備份AEM從節點的災難恢復情形檔案，並在應用程式伺服器上的指定位置（如果已恢復）將其替換。

## 在群集環境中恢復 {#recovery-in-a-clustered-environment}

如果整個群集或單個節點出現故障，您需要使用備份進行恢復。

對於單節點恢復，只需關閉單節點並運行單節點恢復過程。

如果整個群集因資料庫崩潰等故障而失敗，您需要執行以下步驟。 還原取決於使用的備份方法。

### 恢復單個節點 {#restoring-a-single-node}

1. 停止損壞的節點。

   >[!NOTE]
   >
   >如果損壞的節點是AEM主節點，請關閉整個群集節點。

1. 從系統映像重新建立物理系統。
1. 將修補程式或更新套用至自影像建立以來套用的AEM表單。 在備份過程中記錄了此資訊。 AEM表單必須恢復到與備份系統時相同的修補程式層級。
1. (可&#x200B;*選*)如果所有其他節點都正常運作，AEM存放庫也可能已損毀。 在這種情況下，您會在AEM存放庫的error.log檔案中看到儲存庫不同步訊息。

   要恢復儲存庫，請執行以下步驟。

   >[!NOTE]
   >
   >如果壓縮的crx-repository備份已聯機，請在任何位置將其解壓縮，然後執行離線還原過程。

   1. 刪除節點的clusterNode目錄中的儲存庫、共用目錄、版本目錄和工作區目錄。
   1. 將群集節點（包括子目錄）的備份還原到該節點。
   1. 刪除節點上的檔案clusterNode/revision.log。
   1. 刪除節點上的。lock（如果存在）。
   1. 刪除節點上的repository/system.id目錄（如果存在）。
   1. 刪除節點上的檔案&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 恢復單個群集節點的repository/cluster_node.id。

>[!NOTE]
>
>請考慮以下幾點：

* 如果失敗的節點是AEM主節點，請將所有內容從從屬資料庫資料夾（crx-repository\crx.0000，其中0000可以是任何數字）複製到crx-repository\資料庫資料夾，並刪除從屬資料庫資料夾。
* 在重新啟動任何群集節點之前，請確保從主節點刪除儲存庫/clustered.txt。
* 確保主節點是先啟動的，一旦完全啟動，則啟動其他節點。

### 恢復整個群集 {#restoring-the-entire-cluster}

1. 停止所有群集節點。
1. 從系統映像中重新建立物理系統。
1. 將修補程式或更新套用至自影像建立以來套用的AEM表單AEM表單。 此資訊記錄在備份過程的步驟1中。 AEM表單必須恢復到與備份系統時相同的修補程式層級。
1. 恢復資料庫、GDS和連接器。
1. 請執行下列動作，以離線復原AEM存放庫：

   >[!NOTE]
   >
   >如果壓縮的crx-repository備份已聯機，請在任何位置將其解壓縮，然後執行離線還原過程。

   1. 在所有群集節點上，刪除clusterNode目錄中的儲存庫、共用目錄、版本目錄和工作區目錄。
   1. 刪除共用目錄中的所有檔案和目錄。
   1. 將群集節點（包括子目錄）的備份還原到一個群集節點。
   1. 將恢復的群集節點的所有檔案複製到所有其他群集節點。 完成後，每個群集節點都包含相同的資料。
   1. 刪除所有群集節點上的檔案clusterNode/revision.log。
   1. 刪除所有群集節點上的。lock（如果存在）。
   1. 刪除repository/system.id所有群集節點（如果存在）。
   1. 刪除所有群集節點上的檔案&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 恢復單個群集節點的repository/cluster_node.id。

>[!NOTE]
>
>請考慮以下幾點：

* 如果失敗的節點是AEM主節點，請將所有內容從從屬資料庫資料夾（看起來像crx-repository\crx.0000，其中0000可以是任何數字）複製到crx-repository\資料庫資料夾。
* 在重新啟動任何群集節點之前，請確保從主節點刪除儲存庫/clustered.txt。
* 確保主節點是先啟動的，一旦完全啟動，則啟動其他節點。

## 備份和恢復通信管理解決方案發佈節點 {#back-up-and-restore-correspondence-management-solution-publish-node}

發佈者節點在群集環境中沒有任何主從關係。 您可以通過以下「備份和還原」來備份任 [何Publisher節點](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)。

### 恢復單個發佈者節點 {#recover-a-single-publisher-node}

1. 關閉需要恢復的節點，在節點再次啟動之前不執行任何發佈活動。
1. 使用恢復備份(https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring [備份])恢復發佈節點。

### 恢復群集 {#recover-a-cluster}

1. 關閉群集。
1. 使用恢復備份(https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring [備份])恢復發佈節點。
1. 啟動主節點，然後啟動作者群集的從節點。

