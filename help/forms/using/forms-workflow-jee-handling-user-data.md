---
title: FormsJEE工作流 |處理用戶資料
seo-title: Forms JEE workflows | Handling user data
description: FormsJEE工作流 |處理用戶資料
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
role: Admin
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# FormsJEE工作流 |處理用戶資料 {#forms-jee-workflows-handling-user-data}

AEM FormsJEE工作流提供設計、建立和管理業務流程的工具。 工作流進程由一系列按指定順序執行的步驟組成。 每個步驟都執行特定操作，例如將任務分配給用戶或發送電子郵件。 進程可以與資產、用戶帳戶和服務交互，並可以使用以下任何方法觸發：

* 從AEM Forms工作區啟動進程
* 使用SOAP或REST風格的服務
* 提交自適應表單
* 使用監視資料夾
* 使用電子郵件

有關建立AEM FormsJEE工作流進程的詳細資訊，請參閱 [工作台幫助](https://www.adobe.com/go/learn_aemforms_workbench_65)。

## 用戶資料和資料儲存 {#user-data-and-data-stores}

當某個進程被觸發並進行時，它將捕獲有關該進程參與者的資料、參與者在與該進程關聯的表單中輸入的資料以及添加到表單中的附件。 資料儲存在AEM FormsJEE伺服器資料庫中，如果配置了，某些資料（如附件）將儲存在全局文檔儲存(GDS)目錄中。 可以在共用檔案系統或資料庫上配置GDS目錄。

## 訪問和刪除用戶資料 {#access-and-delete-user-data}

當觸發進程時，生成唯一的進程實例ID和長壽命調用ID並與進程實例相關聯。 您可以基於長期調用ID訪問和刪除進程實例的資料。 您可以使用已提交任務的進程啟動器或進程參與者的用戶名推斷進程實例的長期調用ID。

但是，在以下情形中，您無法標識啟動器的進程實例ID:

* **通過受監視資料夾觸發的進程**:如果進程由受監視的資料夾觸發，則無法使用其啟動器標識該進程實例。 在這種情況下，用戶資訊被編碼在所儲存的資料中。
* **從發佈實例啟動的進AEM程**:從發佈實例觸發AEM的所有進程實例不會捕獲有關啟動器的資訊。 但是，用戶資料可以以與進程相關聯的形式捕獲，該形式儲存在工作流變數中。
* **通過電子郵件啟動的進程**:發件人的電子郵件ID將作為屬性捕獲到 `tb_job_instance` 資料庫表，不能直接查詢。

### 在已知工作流啟動器或參與者時標識進程實例ID {#initiator-participant}

執行以下步驟以標識工作流啟動器或參與者的進程實例ID:

1. 在AEM Forms伺服器資料庫中執行以下命令，從中檢索工作流啟動器或參與者的主ID `edcprincipalentity` 資料庫表。

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   查詢返回指定的主體ID `user_ID`。

1. (**對於工作流啟動器**)執行以下命令，從 `tb_task` 資料庫表。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   查詢返回由指定的 `initiator`_ `principal_id`。 任務分為兩種類型：

   * **已完成的任務**:這些任務已提交，並在 `process_instance_id` 的子菜單。 記下已提交任務的所有進程實例ID並繼續執行步驟。
   * **已啟動但未完成的任務**:這些任務已啟動但尚未提交。 中的值 `process_instance_id` 欄位 **0** （零）。 在這種情況下，請記下相應的任務ID，並參見 [處理孤立任務](#orphan)。

1. (**對於工作流參與者**)執行以下命令，從中檢索與啟動器的進程參與者的主體ID關聯的進程實例ID `tb_assignment` 資料庫表。

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   查詢將返回與參與者關聯的所有進程的實例ID，包括參與者尚未提交任何任務的進程。

   記下已提交任務的所有進程實例ID並繼續執行步驟。

   對於孤立任務或 `process_instance_id` 為0（零），記下相應的任務ID並參見 [處理孤立任務](#orphan)。

1. 按照中的說明操作 [根據流程實例ID從工作流實例中清除用戶資料](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 刪除已標識的進程實例ID的用戶資料。

### 在將用戶資料儲存在基元變數中時標識進程實例ID {#primitive}

可以設計工作流，使得用戶資料被捕獲到變數中，該變數被儲存為資料庫中的blob。 在這種情況下，僅當用戶資料儲存在以下基元類型變數之一時，才可查詢用戶資料：

* **字串**:直接或作為子字串包含用戶ID，可使用SQL查詢。
* **數字**:直接包含用戶ID。
* **XML**:包含用戶ID作為子字串，該用戶ID在儲存為資料庫中文本列的文本中，可以像字串一樣查詢。

執行以下步驟，以確定在基元類型變數中儲存資料的工作流是否包含用戶的資料：

1. 執行以下資料庫命令：

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   查詢返回中的表名 `tb_<number>` 指定應用程式的格式( `app_name`)和工作流( `workflow_name`)。

   >[!NOTE]
   >
   >的值 `name` 如果工作流嵌套在應用程式內的子資料夾中，則屬性可能比較複雜。 確保指定工作流的準確完整路徑，您可以從 `omd_object_type` 資料庫表。

1. 查看 `tb_<number>` 表架構。 該表包含用於儲存指定工作流的用戶資料的變數。 表中的變數與工作流中的變數相對應。

   標識並記錄與包含用戶ID的工作流變數對應的變數。 如果標識的變數為基元類型，則可以運行查詢以確定與用戶ID關聯的工作流實例。

1. 執行以下資料庫命令。 在此命令中， `user_var` 是包含用戶ID的primitive-type變數。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   查詢返回與指定的進程實例ID關聯的所有進程實例ID `user_ID`。

1. 按照中的說明操作 [根據流程實例ID從工作流實例中清除用戶資料](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 刪除已標識的進程實例ID的用戶資料。

### 根據流程實例ID從工作流實例中清除用戶資料 {#purge}

既然您已標識了與用戶關聯的進程實例ID，請執行以下操作以從各個進程實例中刪除用戶資料。

1. 執行以下命令，從中檢索進程實例的長壽命調用ID和狀態 `tb_process_instance` 的子菜單。

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   查詢返回指定的長期調用ID和狀態 `process_instance_id`。

1. 建立公共實例 `ProcessManager` 客戶端(C) `com.adobe.idp.workflow.client.ProcessManager`)使用 `ServiceClientFactory` 連接設定正確的實例。

   有關詳細資訊，請參見Java API參考 [類進程管理器](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html)。

1. 檢查工作流實例的狀態。 如果狀態不是2(COMPLETE)或4(TERMINATED)，則首先通過調用以下方法終止實例：

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`。

1. 通過調用以下方法清除工作流實例：

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   的 `purgeProcessInstance` 方法將從AEM Forms伺服器資料庫和GDS（如果已配置）中完全刪除指定調用ID的所有資料。

### 處理孤立任務 {#orphan}

孤立任務是指其包含進程已啟動但尚未提交的任務。 在這種情況下， `process_instance_id` 是 **0** （零）。 因此，無法使用進程實例ID跟蹤為孤立任務儲存的用戶資料。 但是，您可以使用孤立任務的任務ID跟蹤它。 可以從 `tb_task` 用戶的表，如中所述 [在已知工作流啟動器或參與者時標識進程實例ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant)。

一旦您擁有任務ID，請執行以下操作以從GDS和資料庫中清除具有孤立任務的關聯檔案和資料。

1. 在AEM Forms伺服器資料庫上執行以下命令，以檢索已標識任務ID的ID。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   查詢返回ID清單。 對於每個ID( `fd_id`)中返回的，建立會話ID字串清單，如下所示：

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. 根據GDS是指向檔案系統還是資料庫，執行以下步驟之一：

   1. **檔案系統中的GDS**

      在GDS檔案系統中：

      1. 搜索具有以下會話ID字串作為副檔名的檔案：
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      具有這些副檔名的檔案是標籤檔案。 這些檔案名以下列格式儲存：

      `<file_name_guid>.session<session_id_string>`

      1. 刪除所有標籤檔案和具有完全檔案名的其他檔案 `<file_name_guid>` 檔案系統。
   1. **資料庫中的GDS**

      對每個會話ID執行以下命令：

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. 執行以下命令以從AEM Forms伺服器資料庫中刪除任務ID的資料：

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
