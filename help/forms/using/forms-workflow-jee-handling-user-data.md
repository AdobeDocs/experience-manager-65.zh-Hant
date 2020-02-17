---
title: Forms JEE工作流程|處理使用者資料
seo-title: Forms JEE工作流程|處理使用者資料
description: 'null'
seo-description: 'null'
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# Forms JEE工作流程|處理使用者資料 {#forms-jee-workflows-handling-user-data}

AEM Forms JEE工作流程提供設計、建立和管理商業程式的工具。 工作流進程由一系列按指定順序執行的步驟組成。 每個步驟都會執行特定動作，例如指派工作給使用者或傳送電子郵件訊息。 程式可與資產、使用者帳戶和服務互動，並可使用下列任一方法來觸發：

* 從AEM Forms Workspace啟動程式
* 使用SOAP或REST風格的服務
* 提交最適化表單
* 使用監視資料夾
* 使用電子郵件

如需建立AEM Forms JEE工作流程程式的詳細資訊，請參閱「 [Workbench說明」](http://www.adobe.com/go/learn_aemforms_workbench_65)。

## 使用者資料與資料儲存 {#user-data-and-data-stores}

當某個進程被觸發並進行時，它會捕獲有關進程參與者的資料、參與者在與進程相關聯的表單中輸入的資料以及添加到表單中的附件。 資料會儲存在AEM Forms JEE伺服器資料庫中，若已設定，某些資料（例如附件）會儲存在「全域檔案儲存(GDS)」目錄中。 GDS目錄可以配置在共用檔案系統或資料庫上。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

當觸發進程時，將生成唯一的進程實例ID和長壽命調用ID並與進程實例關聯。 您可以根據長期調用ID訪問和刪除流程實例的資料。 您可以使用已提交任務的進程啟動器或進程參與者的用戶名推斷進程實例的長期調用ID。

但是，在以下情況下，您無法標識啟動器的進程實例ID:

* **透過受監視資料夾觸發的程式**:如果進程由受監視資料夾觸發，則無法使用其啟動器來標識進程實例。 在這種情況下，用戶資訊被編碼在儲存的資料中。
* **從發佈AEM例項開始的程式**:所有從AEM發佈例項觸發的程式例項都不會擷取有關啟動器的資訊。 但是，用戶資料可以以與進程相關聯的形式捕獲，該形式儲存在工作流變數中。
* **透過電子郵件啟動的程式**:傳送者的電子郵件ID會擷取為資料庫表格中不透明blob欄的 `tb_job_instance` 屬性，無法直接查詢。

### 在已知工作流啟動器或參與者時識別流程實例ID {#initiator-participant}

執行以下步驟以標識工作流啟動器或參與者的流程實例ID:

1. 在AEM Forms伺服器資料庫中執行下列命令，從資料庫表格擷取工作流程啟動者或參與者的 `edcprincipalentity` 主要ID。

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   查詢返回指定的承擔者ID `user_ID`。

1. (對&#x200B;**於工作流啟動器**)執行以下命令，從資料庫表中檢索與啟動器的主ID相關的所有 `tb_task` 任務。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   查詢返回由指定 `initiator`_啟動的任 `principal_id`務。 任務分為兩種類型：

   * **完成的任務**:這些任務已提交，並在欄位中顯示一個字母 `process_instance_id` 數字值。 記下已提交任務的所有進程實例ID並繼續執行步驟。
   * **已啟動但未完成的任務**:這些任務已啟動，但尚未提交。 這些任務 `process_instance_id` 的欄位值 **為** 0（零）。 在這種情況下，請記下相應的任務ID並參 [閱使用孤立任務](#orphan)。

1. (對&#x200B;**於工作流參與者**)執行以下命令，從資料庫表中檢索與啟動器的進程參與者的主ID關聯的進程實例 `tb_assignment` ID。

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   查詢返回與參與者關聯的所有進程的實例ID，包括參與者未提交任何任務的進程。

   記下已提交任務的所有進程實例ID並繼續執行步驟。

   對於孤立任務或任務（零） `process_instance_id` 為0（零）時，請記下相應的任務ID，並參閱 [使用孤立任務](#orphan)。

1. 按照「根據流程實 [例ID從工作流實例中清除用戶資料](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 」部分中的說明刪除已標識的流程實例ID的用戶資料。

### 識別將使用者資料儲存在基本變數中的流程例項ID {#primitive}

可以設計工作流，以便用戶資料被捕獲到一個變數中，該變數作為blob儲存在資料庫中。 在這種情況下，只有當使用者資料儲存在下列原始類型變數中時，您才能查詢使用者資料：

* **字串**:直接包含用戶ID或作為子字串，可使用SQL查詢。
* **數值**:直接包含使用者ID。
* **XML**:在儲存為資料庫文字欄的文字中，以子字串形式包含使用者ID，並可像字串一樣查詢。

執行下列步驟，以判斷以基本類型變數儲存資料的工作流程是否包含使用者的資料：

1. 執行以下資料庫命令：

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   查詢返回指定應用程 `tb_<number>` 序()和工作流( `app_name`)的格式 `workflow_name`表名。

   >[!NOTE]
   >
   >如果工作流在應 `name` 用程式內的子資料夾中巢狀化，則屬性的值可能會很複雜。 請確定您指定可從資料庫表格取得的工作流程完整 `omd_object_type` 路徑。

1. 查看表 `tb_<number>` 模式。 表格包含儲存指定工作流程之使用者資料的變數。 表格中的變數會對應至工作流程中的變數。

   識別並記下與包含使用者ID的工作流程變數相對應的變數。 如果識別的變數為基本類型，您可以執行查詢，以判斷與使用者ID相關的工作流程例項。

1. 執行以下資料庫命令。 在此命令中， `user_var` 是包含用戶ID的基本類型變數。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   查詢返回與指定的關聯的所有進程實例ID `user_ID`。

1. 按照「根據流程實 [例ID從工作流實例中清除用戶資料](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 」部分中的說明刪除已標識的流程實例ID的用戶資料。

### 根據流程實例ID從工作流實例中清除用戶資料 {#purge}

現在您已識別與用戶關聯的流程實例ID，請執行下列操作以從相應的流程實例中刪除用戶資料。

1. 執行以下命令，從表中檢索進程實例的長壽命調用ID和狀 `tb_process_instance` 態。

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   查詢返回指定的長壽命調用ID和狀態 `process_instance_id`。

1. 使用具有正確連接設 `ProcessManager` 置的實例建立公 `com.adobe.idp.workflow.client.ProcessManager``ServiceClientFactory` 用客戶端()實例。

   如需詳細資訊，請參閱類別ProcessManager的Java API [參考](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html)。

1. 檢查工作流實例的狀態。 如果狀態不是2(COMPLETE)或4(TERMINATED)，請先呼叫下列方法以終止例項：

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. 通過調用以下方法清除工作流實例：

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   此方 `purgeProcessInstance` 法會從AEM Forms伺服器資料庫和GDS（若已設定）中完全刪除指定呼叫ID的所有資料。

### 處理孤立任務 {#orphan}

孤立任務是指其包含進程已啟動但尚未提交的任務。 在本例中， `process_instance_id` 為 **0** （零）。 因此，您無法使用進程實例ID跟蹤為孤立任務儲存的用戶資料。 但是，您可以使用孤立任務的任務ID跟蹤該任務。 當工作流啟動器或參與者已知時， `tb_task` 可以從表中為用戶標識任 [務ID，如「標識流程實例ID」中所述](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant)。

在您擁有任務ID後，請執行以下操作以從GDS和資料庫中清除具有孤立任務的相關檔案和資料。

1. 在AEM Forms伺服器資料庫上執行下列命令，以擷取已識別之工作ID的ID。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   查詢返回ID清單。 對於結果中傳 `fd_id`回的每個ID()，請建立工作階段ID字串清單，如下所示：

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. 根據GDS指向檔案系統還是資料庫，執行以下步驟之一：

   1. **檔案系統中的GDS**

      在GDS檔案系統中：

      1. 搜尋具有下列工作階段ID字串的檔案作為副檔名：
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`
      具有這些副檔名的檔案是標籤檔案。 這些檔案會以下列格式儲存為檔案名稱：

      `<file_name_guid>.session<session_id_string>`

      1. 從檔案系統中刪除所有標籤檔案和其他檔案，其檔案名 `<file_name_guid>` 與檔案名完全相同。
   1. **資料庫中的GDS**

      對每個會話ID執行以下命令：

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. 執行下列命令，從AEM Forms伺服器資料庫刪除工作ID的資料：

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```

