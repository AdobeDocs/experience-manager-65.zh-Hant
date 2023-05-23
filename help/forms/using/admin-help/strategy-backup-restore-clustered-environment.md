---
title: 群集環境中備份和恢復的策略
seo-title: Strategy for backup and restore in a clustered environment
description: 如AEM果表單實現將其他自定義資料儲存到不同的資料庫中，則必須實施一個策略來備份此資料，確保它與表單數AEM據保持同步。
seo-description: If your AEM forms implementation stores additional custom data in a different database, you must implement a strategy to back up this data ensuring that it remains in sync with the AEM forms data.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 0%

---

# 群集環境中備份和恢復的策略 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>如AEM果表單實現將其他自定義資料儲存到不同的資料庫中，則必須實施一個策略來備份此資料，確保它與表單數AEM據保持同步。 此外，必須設計應用程式，使其足夠強健，以處理附加資料庫不同步的情況。 強烈建議在事務的上下文中執行任何資料庫操作，以幫助保持一致狀態。

您需要備份表單系統的以AEM下部分以從任何錯誤中恢復：

* 表單使用的數AEM據庫
* 具有長期資料和其他持久性文檔的GDS
* AEM資料庫(crx-repository)

>[!NOTE]
>
>您需要備份表單設定正在使用的AEM任何其他資料，如客戶字型、連接器資料等。

## 備份群集環境 {#back-up-a-clustered-environment}

本主題討論備份任何表單群集環境AEM的以下策略：

* 離線備份，但停機
* 無停機的離線備份（關閉的輔助節點備份）
* 線上備份，無停機但響應延遲
* 備份Bootstrap屬性檔案

### 離線備份，但停機 {#offline-backup-with-downtime}

1. 關閉整個群集和相關服務。 （請參見） [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何節點上，備份資料庫、 GDS和連接器。 （請參見） [要備份和恢復的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 要離線備AEM份儲存庫，請執行以下步驟：

   1. 對於每個群集節點，備份包含群集節點id的檔案。
   1. 備份任何輔助群集節點（包括子目錄）的所有檔案。
   1. 單獨備份每個群集節點的儲存庫/系統ID。

   有關詳細步驟，請參見 [備份和恢復](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)。

1. 備份任何其他資料，如客戶字型。
1. 再次啟動群集。

### 離線備份，無停機 {#offline-backup-with-no-downtime}

1. 進入滾動備份模式。 （請參見） [進入備份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   恢復後，請退出滾動備份模式。

1. 關閉群集的任何次節點AEM。 （請參見） [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何節點上，備份資料庫、 GDS和連接器。 （請參見） [要備份和恢復的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 要離線備AEM份儲存庫，請執行以下步驟：

   1. 對於每個群集節點，備份包含群集節點id的檔案。
   1. 備份任何輔助群集節點（包括子目錄）的所有檔案。
   1. 分別備份每個群集節點的repository/system.id。

   有關詳細步驟，請參見 [備份和恢復](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)。

1. 備份任何其他資料，如客戶字型。
1. 再次啟動群集。

### 線上備份，無停機但響應延遲 {#online-backup-with-no-downtime-but-delay-in-response}

1. 進入滾動備份模式。 （請參見） [進入備份模式](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   恢復後，請退出滾動備份模式。

1. 關閉群集的任何次節點AEM。 （請參見） [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 在任何節點上，備份資料庫、 GDS和連接器。 （請參見） [要備份和恢復的檔案](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. 要聯機備AEM份儲存庫，請執行以下步驟：

   1. 對於每個群集節點，備份包含cluster_node.id的檔案。
   1. 分別備份每個群集節點的repository/system.id。
   1. 在任何輔助節點上，對儲存庫執行聯機備份以瞭解詳細步驟，請參閱聯機備份。

1. 備份任何其他資料，如客戶字型。
1. 再次啟動群集。

### 備份Bootstrap屬性檔案 {#back-up-the-bootstrap-properties-file}

建立群集時，會AEM在應用程式伺服器中為所有輔助節點建立屬性檔案。 建議備份Bootstrap屬性檔案。 您可以在應用程式伺服器上的以下位置找到該檔案：

* JBoss®:在BIN目錄中
* WebLogic:在域目錄中
* WebSphere®:在配置檔案目錄中

備份檔案以執行輔助節點的災AEM難恢複方案，並在應用程式伺服器上的指定位置將其替換（如果已恢復）。

## 群集環境中的恢復 {#recovery-in-a-clustered-environment}

如果整個群集或單個節點出現任何故障，請使用備份還原。

對於單節點恢復，關閉單節點並運行單節點恢復過程。

如果整個群集因資料庫崩潰等故障而失敗，請執行以下步驟。 恢復取決於使用的備份方法。

### 恢復單個節點 {#restoring-a-single-node}

1. 停止損壞的節點。

   >[!NOTE]
   >
   >如果損壞的節點是AEM主節點，請關閉整個群集節點。

1. 從系統映像重新建立物理系統。
1. 將修補程式或更新應AEM用到自建立映像以來應用的表單。 在備份過程中記錄了此資訊。 表AEM單必須恢復到備份系統時的修補程式級別。
1. (*可選*)如果所有其他節點工作正常，則可能存AEM儲庫也已損壞。 在這種情況下，在儲存庫的error.log檔案中將看到一個儲存庫不同步AEM消息。

   要恢復儲存庫，請執行以下步驟。

   >[!NOTE]
   >
   >如果已聯機執行壓縮的crx-repository備份，請在任何位置解壓並遵循離線還原過程。

   1. 刪除節點的clusterNode目錄中的儲存庫、共用目錄、版本目錄和工作區目錄。
   1. 將群集節點（包括子目錄）的備份還原到節點。
   1. 刪除節點上的檔案clusterNode/revision.log。
   1. 刪除節點上的.lock（如果存在）。
   1. 刪除節點上的repository/system.id（如果存在）。
   1. 刪除節點上的檔案&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 恢復單個群集節點的repository/cluster_node.id。

>[!NOTE]
>
>請考慮以下幾點：

* 如果故障節點是主節點AEM，請將所有內容從輔助資料庫資料夾（crx-repository\crx.0000，其中000可以是任何數字）複製到crx-repository\資料庫資料夾，然後刪除輔助資料庫資料夾。
* 在重新啟動任何群集節點之前，請確保從主節點中刪除儲存庫/clustered.txt。
* 確保主節點是先啟動的，在啟動後，啟動其他節點。

### 恢復整個群集 {#restoring-the-entire-cluster}

1. 停止所有群集節點。
1. 從系統映像重新建立物理系統。
1. 將修補程式或更新應AEM用到自建立映像後應用的表單AEM表單。 此資訊記錄在備份過程的步驟1中。 表AEM單必須恢復到備份系統時的修補程式級別。
1. 還原資料庫、 GDS和連接器。
1. 執行以下操作以離線AEM恢復儲存庫：

   >[!NOTE]
   >
   >如果已聯機執行壓縮的crx-repository備份，請在任何位置解壓並遵循離線還原過程。

   1. 在所有群集節點上，刪除clusterNode目錄中的儲存庫、共用目錄、版本目錄和工作區目錄。
   1. 刪除共用目錄中的所有檔案和目錄。
   1. 將群集節點（包括子目錄）的備份還原到一個群集節點。
   1. 將還原的群集節點的所有檔案複製到所有其他群集節點。 完成後，每個群集節點都包含相同的資料。
   1. 刪除所有群集節點上的檔案clusterNode/revision.log。
   1. 刪除所有群集節點上的.lock（如果存在）。
   1. 刪除repository/system.id所有群集節點（如果存在）。
   1. 刪除所有群集節點上的檔案&amp;ast;&amp;ast;/listener.properties（如果存在）。
   1. 恢復單個群集節點的repository/cluster_node.id。

>[!NOTE]
>
>請考慮以下幾點：

* 如果故障節點是主節AEM點，請將所有內容從輔助儲存庫資料夾（看起來類似於crx-repository\crx.0000 ，其中000可以是任意數字）複製到crx-repository\儲存庫資料夾。
* 在重新啟動任何群集節點之前，請確保從主節點中刪除儲存庫/clustered.txt。
* 確保主節點是先啟動的，在啟動後，啟動其他節點。

## 備份和恢復通信管理解決方案發佈節點 {#back-up-and-restore-correspondence-management-solution-publish-node}

發佈者節點在群集環境中沒有任何主次關係。 您可以通過以下方式備份任何發佈伺服器節點 [備份和恢復](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)。

### 恢復單個發佈者節點 {#recover-a-single-publisher-node}

1. 關閉必須恢復的節點，在節點再次啟動之前不執行任何發佈活動。
1. 使用 [恢復備份](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)。

### 恢復群集 {#recover-a-cluster}

1. 關閉群集。
1. 使用 [恢復備份](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)。
1. 啟動主節點，然後啟動作者群集的次節點。
