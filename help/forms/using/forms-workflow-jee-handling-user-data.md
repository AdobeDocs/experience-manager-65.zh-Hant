---
title: FormsJEE工作流程 |處理使用者資料
seo-title: FormsJEE工作流程 |處理使用者資料
description: FormsJEE工作流程 |處理使用者資料
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 0%

---


# FormsJEE工作流程 |處理用戶資料{#forms-jee-workflows-handling-user-data}

AEM FormsJEE工作流程提供設計、建立和管理商業程式的工具。 工作流進程由一系列按指定順序執行的步驟組成。 每個步驟都會執行特定動作，例如指派工作給使用者或傳送電子郵件訊息。 程式可與資產、使用者帳戶和服務互動，並可使用下列任一方法來觸發：

* 從AEM Forms工作區啟動流程
* 使用SOAP或REST風格的服務
* 提交最適化表單
* 使用監視資料夾
* 使用電子郵件

有關建立AEM FormsJEE工作流進程的詳細資訊，請參閱[ Workbench Help](http://www.adobe.com/go/learn_aemforms_workbench_65)。

## 用戶資料和資料儲存{#user-data-and-data-stores}

當某個進程被觸發並進行時，它會捕獲有關進程參與者的資料、參與者在與進程相關聯的表單中輸入的資料以及添加到表單中的附件。 資料儲存在AEM FormsJEE伺服器資料庫中，如果配置了，某些資料（如附件）將儲存在全局文檔儲存(GDS)目錄中。 GDS目錄可以配置在共用檔案系統或資料庫上。

## 存取和刪除使用者資料{#access-and-delete-user-data}

當觸發進程時，將生成唯一的進程實例ID和長壽命調用ID並與進程實例關聯。 您可以根據長期調用ID訪問和刪除流程實例的資料。 您可以使用已提交任務的進程啟動器或進程參與者的用戶名推斷進程實例的長期調用ID。

但是，在以下情況下，您無法標識啟動器的進程實例ID:

* **透過受監視資料夾觸發的程式**:如果進程由受監視資料夾觸發，則無法使用其啟動器來標識進程實例。在這種情況下，用戶資訊被編碼在儲存的資料中。
* **從發佈實例啟動的AEM流程**:從發佈實例觸發的所AEM有進程實例不會捕獲有關啟動器的資訊。但是，用戶資料可以以與進程相關聯的形式捕獲，該形式儲存在工作流變數中。
* **透過電子郵件啟動的程式**:傳送者的電子郵件ID會擷取為資料庫表格中不透明blob欄的 `tb_job_instance` 屬性，無法直接查詢。

### 在工作流啟動器或參與者已知{#initiator-participant}時識別流程實例ID

執行以下步驟以標識工作流啟動器或參與者的流程實例ID:

1. 在AEM Forms伺服器資料庫中執行以下命令，從`edcprincipalentity`資料庫表中檢索工作流啟動器或參與者的主ID。

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   查詢返回指定`user_ID`的主ID。

1. （**對於工作流啟動器**）執行以下命令，從`tb_task`資料庫表中檢索與啟動器的主ID相關的所有任務。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   查詢返回由指定的`initiator`_ `principal_id`啟動的任務。 任務分為兩種類型：

   * **完成的任務**:這些任務已提交，並在欄位中顯示一個字母 `process_instance_id` 數字值。記下已提交任務的所有進程實例ID並繼續執行步驟。
   * **已啟動但未完成的任務**:這些任務已啟動，但尚未提交。這些任務的`process_instance_id`欄位中的值為&#x200B;**0**（零）。 在這種情況下，請注意相應的任務ID，並參見[使用孤立任務](#orphan)。

1. （**對於工作流參與者**）執行以下命令，從`tb_assignment`資料庫表中檢索與啟動器的進程參與者的主ID相關聯的進程實例ID。

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   查詢返回與參與者關聯的所有進程的實例ID，包括參與者未提交任何任務的進程。

   記下已提交任務的所有進程實例ID並繼續執行步驟。

   對於`process_instance_id`為0（零）的孤立任務或任務，請記下相應的任務ID，並參閱[使用孤立任務](#orphan)。

1. 按照[根據流程實例ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge)部分從工作流實例中清除用戶資料中的說明刪除已標識流程實例ID的用戶資料。

### 識別將使用者資料儲存在基本變數{#primitive}時的處理例項ID

可以設計工作流，以便用戶資料被捕獲到一個變數中，該變數作為blob儲存在資料庫中。 在這種情況下，只有當使用者資料儲存在下列原始類型變數中時，您才可以查詢使用者資料：

* **字串**:直接包含用戶ID或作為子字串包含用戶ID，可使用SQL查詢。
* **數值**:直接包含使用者ID。
* **XML**:在儲存為資料庫文字欄的文字中，以子字串形式包含使用者ID，並可像字串一樣查詢。

執行下列步驟，以判斷以基本類型變數儲存資料的工作流程是否包含使用者的資料：

1. 執行以下資料庫命令：

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   查詢返回指定應用程式(`app_name`)和工作流(`workflow_name`)的`tb_<number>`格式的表名。

   >[!NOTE]
   >
   >如果工作流嵌套在應用程式內部的子資料夾中，則`name`屬性的值可能很複雜。 請確定您指定工作流程的完整路徑，您可從`omd_object_type`資料庫表格取得。

1. 查看`tb_<number>`表模式。 表格包含儲存指定工作流程之使用者資料的變數。 表格中的變數會對應至工作流程中的變數。

   識別並記下與包含使用者ID的工作流程變數相對應的變數。 如果識別的變數為基本類型，您可以執行查詢，以判斷與使用者ID相關的工作流程例項。

1. 執行以下資料庫命令。 在此命令中，`user_var`是包含用戶ID的基本類型變數。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   查詢返回與指定的`user_ID`關聯的所有進程實例ID。

1. 按照[根據流程實例ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge)部分從工作流實例中清除用戶資料中的說明刪除已標識流程實例ID的用戶資料。

### 根據流程實例ID {#purge}從工作流實例中清除用戶資料

現在您已識別與用戶關聯的流程實例ID，請執行下列操作以從相應的流程實例中刪除用戶資料。

1. 執行以下命令，從`tb_process_instance`表中檢索進程實例的長壽命調用ID和狀態。

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   查詢返回指定`process_instance_id`的長壽命調用ID和狀態。

1. 使用具有正確連接設定的`ServiceClientFactory`實例建立公共`ProcessManager`客戶端(`com.adobe.idp.workflow.client.ProcessManager`)實例。

   如需詳細資訊，請參閱[類別ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html)的Java API參考。

1. 檢查工作流實例的狀態。 如果狀態不是2(COMPLETE)或4(TERMINATED)，請先呼叫下列方法以終止例項：

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`。

1. 通過調用以下方法清除工作流實例：

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   `purgeProcessInstance`方法會從AEM Forms伺服器資料庫和GDS（如果配置）中完全刪除指定調用ID的所有資料。

### 處理孤立任務{#orphan}

孤立任務是指其包含進程已啟動但尚未提交的任務。 此時，`process_instance_id`為&#x200B;**0**（零）。 因此，您無法使用進程實例ID跟蹤為孤立任務儲存的用戶資料。 但是，您可以使用孤立任務的任務ID跟蹤該任務。 如[ Identify process instance IDs when workflow initiator or participant is know ](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant)中所述，您可以從`tb_task`表中為用戶標識任務ID。

在您擁有任務ID後，請執行以下操作以從GDS和資料庫中清除具有孤立任務的相關檔案和資料。

1. 在AEM Forms伺服器資料庫上執行以下命令，以檢索所標識任務ID的ID。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   查詢返回ID清單。 對於結果中返回的每個ID(`fd_id`)，建立會話ID字串清單，如下所示：

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

      1. 從檔案系統中刪除檔案名完全為`<file_name_guid>`的所有標籤檔案和其他檔案。
   1. **資料庫中的GDS**

      對每個會話ID執行以下命令：

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. 執行以下命令以刪除AEM Forms伺服器資料庫中任務ID的資料：

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```

