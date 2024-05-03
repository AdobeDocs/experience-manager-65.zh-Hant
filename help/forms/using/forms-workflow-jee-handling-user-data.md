---
title: Forms JEE工作流程 | 處理使用者資料
description: 瞭解如何使用AEM Forms JEE工作流程來設計、建立和管理業務流程。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Forms JEE工作流程 | 處理使用者資料 {#forms-jee-workflows-handling-user-data}

AEM Forms JEE工作流程提供設計、建立和管理業務流程的工具。 工作流程處理包含一系列以指定順序執行的步驟。 每個步驟都會執行特定動作，例如將任務指派給使用者或傳送電子郵件訊息。 程式可與資產、使用者帳戶和服務互動，並可使用下列任何方法觸發：

* 從AEM Forms工作區啟動程式
* 使用SOAP或RESTful服務
* 提交最適化表單
* 使用watched資料夾
* 使用電子郵件

如需建立AEM Forms JEE工作流程程式的詳細資訊，請參閱 [Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_65).

## 使用者資料和資料存放區 {#user-data-and-data-stores}

當流程被觸發且進行時，它會擷取流程參與者的相關資料、參與者在與流程相關的表單中輸入的資料，以及新增至表單的附件。 資料會儲存在AEM Forms JEE伺服器資料庫中，而有些資料（如已設定）會儲存在全域檔案儲存(GDS)目錄中。 GDS目錄可在共用檔案系統或資料庫上設定。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

觸發程式時，系統會產生唯一的程式執行個體ID和長效引動過程ID，並與程式執行個體建立關聯。 您可以根據長效引動識別碼，存取和刪除程式執行個體的資料。 您可以使用已提交其任務的程式發起人或程式參與者的使用者名稱，來推算程式執行個體的長期引動識別碼。

但是，在下列情況下，您無法識別初始器的程式執行個體ID：

* **透過watched資料夾觸發的程式**：如果程式是由watched資料夾觸發，則無法使用啟動器識別程式執行個體。 在此情況下，使用者資訊會編碼在儲存的資料中。
* **從發佈AEM執行個體初始的程式**：從AEM發佈執行個體觸發的所有流程執行個體都不會擷取關於初始器的資訊。 不過，使用者資料可能會以與程式相關聯的表單擷取，並儲存在工作流程變數中。
* **透過電子郵件初始的流程**：寄件者的電子郵件ID會被擷取為的不透明blob欄中的屬性，而 `tb_job_instance` 無法直接查詢的資料庫表格。

### 在已知工作流程發起人或參與者時，識別流程執行個體ID {#initiator-participant}

執行下列步驟，以便您識別工作流程發起人或參與者的流程執行處理ID：

1. 在AEM Forms伺服器資料庫中執行以下命令，以從擷取工作流程發起人或參與者的主體ID `edcprincipalentity` 資料庫表格。

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   查詢會傳回指定之主體ID `user_ID`.

1. (**針對工作流程發起人**)執行以下命令，從擷取與初始器的主參與者ID相關的所有工作 `tb_task` 資料庫表格。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   查詢會傳回由指定的所起始的任務 `initiator`_ `principal_id`. 任務分為兩種型別：

   * **已完成的任務**：這些工作已提交，並在以下位置顯示英數字元： `process_instance_id` 欄位。 記下已提交任務的所有程式執行個體ID，並繼續這些步驟。
   * **已起始但未完成的工作**：這些工作已開始，但尚未提交。 中的值 `process_instance_id` 這些任務的欄位是 **0** （零）。 在此情況下，請記下對應的任務ID，並參閱 [處理孤立任務](#orphan).

1. (**對於工作流程參與者**)執行以下命令，從擷取與啟動器之程式參與者的主參與者ID相關聯的程式執行個體ID。 `tb_assignment` 資料庫表格。

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   查詢會傳回與參與者相關的所有處理序的執行環境ID，包括參與者尚未提交任何任務的處理序。

   記下已提交任務的所有程式執行個體ID，並繼續這些步驟。

   對於孤立任務或任務，如果 `process_instance_id` 為0 （零），記下對應的任務ID並檢視 [處理孤立任務](#orphan).

1. 請依照中的指示操作 [根據流程執行個體ID從工作流程執行個體中清除使用者資料](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 區段，以便刪除已識別程式執行個體ID的使用者資料。

### 當使用者資料儲存在原始變數中時，識別程式執行個體ID {#primitive}

您可以設計工作流程，將使用者資料擷取到變數中，並儲存為資料庫中的blob。 在這種情況下，只有當使用者資料儲存在下列其中一個基本型別變數中時，您才能查詢使用者資料：

* **字串**：直接包含使用者ID或作為子字串包含，且可使用SQL查詢。
* **數值**：直接包含使用者ID。
* **XML**：包含使用者ID，作為儲存為資料庫中文字欄的文字中的子字串，且可像字串一樣進行查詢。

執行以下步驟，以便您可以確定在基本型別變數中儲存資料的工作流程是否包含使用者的資料：

1. 執行以下資料庫命令：

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   查詢傳回的資料表名稱位於 `tb_<number>` 指定應用程式的格式( `app_name`)和工作流程( `workflow_name`)。

   >[!NOTE]
   >
   >的值 `name` 如果工作流程巢狀內嵌於應用程式內的子資料夾中，屬性可能會很複雜。 請確定您指定的工作流程完整路徑，您可從取得 `omd_object_type` 資料庫表格。

1. 檢閱 `tb_<number>` 表格結構描述。 此表格包含儲存指定工作流程之使用者資料的變數。 表格中的變數與工作流程中的變數對應。

   識別並記下與包含使用者ID的工作流程變數相對應的變數。 如果識別的變數屬於基本型別，您可以執行查詢來判斷與使用者ID相關聯的工作流程例項。

1. 執行以下資料庫命令。 在此命令中， `user_var` 是包含使用者ID的原始型別變數。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   查詢會傳回與指定之關聯的所有處理序執行個體ID `user_ID`.

1. 請依照中的指示操作 [根據流程執行個體ID從工作流程執行個體中清除使用者資料](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 區段，以便刪除已識別程式執行個體ID的使用者資料。

### 根據流程執行個體ID從工作流程執行個體中清除使用者資料 {#purge}

現在您已識別與使用者關聯的程式執行個體ID，請執行以下動作以從個別程式執行個體中刪除使用者資料。

1. 執行以下命令，您便可以從擷取處理序執行個體的長期引動識別碼和狀態 `tb_process_instance` 表格。

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   查詢會傳回指定之長期引動識別碼和狀態 `process_instance_id`.

1. 建立公開的執行個體 `ProcessManager` 使用者端( `com.adobe.idp.workflow.client.ProcessManager`)使用 `ServiceClientFactory` 具有正確連線設定的執行個體。

   如需詳細資訊，請參閱以下專案的Java™ API參考： [類別ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. 檢查工作流程例項的狀態。 如果狀態不是2 (COMPLETE)或4 (TERMINATED)，請先呼叫下列方法來終止執行個體：

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`。

1. 呼叫下列方法以清除工作流程執行個體：

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   此 `purgeProcessInstance` 如果已設定，方法會從AEM Forms Server資料庫和GDS中完全刪除指定之叫用ID的所有資料。

### 處理孤立任務 {#orphan}

孤立任務是包含已啟動但尚未提交的流程的任務。 在此案例中， `process_instance_id` 是 **0** （零）。 因此，您無法使用程式執行個體ID來追蹤為孤立任務儲存的使用者資料。 不過，您可以使用孤立任務的工作ID來追蹤它。 您可透過以下連結識別任務ID： `tb_task` 使用者表格（如所述） [在已知工作流程發起人或參與者時，識別流程執行個體ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

取得工作ID後，請執行以下作業從GDS和資料庫中清除具有孤立工作的相關檔案和資料。

1. 在AEM Forms伺服器資料庫上執行下列命令，以便擷取已識別工作ID的ID。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   查詢會傳回ID清單。 對於每個ID ( `fd_id`)，建立工作階段ID字串的清單，如下所示：

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. 視您的GDS指向檔案系統或資料庫而定，請執行下列其中一個步驟：

   1. **檔案系統中的GDS**

      在GDS檔案系統中：

      1. 搜尋副檔名為下列工作階段ID字串的檔案：

      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      具有這些副檔名的檔案是標籤檔案。 檔案名稱會以下列格式儲存：

      `<file_name_guid>.session<session_id_string>`

      1. 刪除所有標籤檔案和其他檔案，檔案名稱完全符合 `<file_name_guid>` 從檔案系統。

   1. **資料庫中的GDS**

      針對每個工作階段ID執行以下命令：

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```

1. 執行以下命令，以便從AEM Forms伺服器資料庫刪除工作ID的資料：

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
