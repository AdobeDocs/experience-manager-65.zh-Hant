---
title: Forms OSGi工作流程 |處理用戶資料
seo-title: Forms-centric workflows on OSGi | Handling user data
description: Forms OSGi工作流程 |處理用戶資料
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
role: Admin
exl-id: fd0e17d7-c3e9-4dec-ad26-ed96a1881f42
source-git-commit: fb9363a39ffc9d3929a31a3a19a124b806607ef4
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 0%

---

# Forms OSGi工作流程 |處理用戶資料 {#forms-centric-workflows-on-osgi-handling-user-data}

以Forms為中心的AEM工作流程可讓您自動化以Forms為中心的實際業務流程。 工作流由一系列步驟組成，這些步驟按關聯工作流模型中指定的順序執行。 每個步驟都會執行特定動作，例如指派任務給使用者或傳送電子郵件訊息。 工作流程可與存放庫、使用者帳戶和服務中的資產互動。 因此，工作流程可以協調涉及任何Experience Manager方面的複雜活動。

可透過下列任何方法來觸發或啟動表單導向工作流程：

* 從AEM收件匣提交應用程式
* 從AEM提交應用程式 [!DNL Forms] 應用程式
* 提交最適化表單
* 使用已監看的資料夾
* 提交互動式通訊或信函

如需以Forms為中心的AEM工作流程和功能的詳細資訊，請參閱 [Forms以OSGi為中心的工作流程](/help/forms/using/aem-forms-workflow.md).

## 使用者資料和資料儲存 {#user-data-and-data-stores}

觸發工作流程時，會自動為工作流程例項產生裝載。 每個工作流程例項都會獲指派一個唯一例項ID和一個相關聯的裝載ID。 裝載包含與工作流程例項相關聯的使用者和表單資料的存放庫位置。 此外，工作流程例項的草稿和歷史資料也會儲存在AEM存放庫中。

工作流程例項的裝載、草稿和歷史記錄所在的預設存放庫位置如下：

>[!NOTE]
>
>您可以在建立工作流程或應用程式時，設定不同的位置以儲存裝載、草稿和歷史記錄資料。 要標識工作流或應用程式儲存資料的位置，請複查工作流。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>工作流程 <br /> 執行個體</strong></td>
   <td>/var/workflow/instances/[server_id]/&lt;date&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>裝載</strong></td>
   <td>/var/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>草稿</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>歷史</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以從存放庫的工作流程例項中存取和刪除使用者資料。 要達到此目的，您必須知道與使用者相關聯的工作流程例項的例項ID。 通過使用啟動工作流實例的用戶的用戶名或工作流實例的當前受託人，可以查找工作流實例的實例ID。

但是，在以下情況下，在標識與啟動器關聯的工作流時，您不能識別或結果可能不明確：

* **透過已監看資料夾觸發的工作流程**:如果工作流程是由已觀看的資料夾觸發，則無法使用其啟動器來識別工作流程例項。 在這種情況下，用戶資訊被編碼在儲存的資料中。
* **從發佈AEM例項啟動的工作流程**:從AEM發佈例項提交最適化表單、互動式通訊或信函時，所有工作流程例項都是使用服務使用者建立。 在這些情況下，工作流程例項資料中不會擷取登入使用者的使用者名稱。

### 存取使用者資料 {#access}

要標識和訪問為工作流實例儲存的用戶資料，請執行以下步驟：

1. 在AEM製作例項上，前往 `https://'[server]:[port]'/crx/de` 並導覽至 **[!UICONTROL 工具>查詢]**.

   選擇 **[!UICONTROL SQL2]** 從 **[!UICONTROL 類型]** 下拉式清單。

1. 根據可用資訊，執行以下查詢之一：

   * 如果工作流啟動器已知，請執行以下操作：

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * 如果您要尋找其資料的使用者是目前工作流程受託人，請執行下列作業：

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   查詢返回指定的工作流啟動器或當前工作流受託人的所有工作流實例的位置。

   例如，下列查詢會從 `/var/workflow/instances` 其工作流啟動器的節點 `srose`.

   ![workflow-instance](assets/workflow-instance.png)

1. 轉至查詢返回的工作流實例路徑。 狀態屬性顯示工作流實例的當前狀態。

   ![狀態](assets/status.png)

1. 在工作流程例項節點中，導覽至 `data/payload/`. 此 `path` 屬性會儲存工作流程例項之裝載的路徑。 您可以導覽至路徑，以存取儲存在裝載中的資料。

   ![裝載路徑](assets/payload-path.png)

1. 導覽至工作流程例項的草稿和歷史記錄位置。

   例如：

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. 對於步驟2中查詢傳回的所有工作流程例項，重複步驟3 - 5。

   >[!NOTE]
   >
   >AEM [!DNL Forms] 應用程式也會以離線模式儲存資料。 工作流程例項的資料可能儲存在本機個別裝置上，並提交至 [!DNL Forms] 伺服器。

### 刪除使用者資料 {#delete-user-data}

您必須是AEM管理員，才能執行下列步驟，從工作流程例項刪除使用者資料：

1. 遵循 [存取使用者資料](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) 並注意以下事項：

   * 與使用者相關聯的工作流程例項路徑
   * 工作流實例的狀態
   * 工作流實例的裝載路徑
   * 工作流程例項的草稿和歷史記錄路徑

1. 在中對工作流程例項執行此步驟 **執行中**, **已暫停**，或 **過時** 狀態：

   1. 前往 `https://'[server]:[port]'/aem/start.html` 並使用管理員憑證登入。
   1. 導覽至 **[!UICONTROL 「工具」>「工作流」>「實例」]**.
   1. 為使用者選取相關的工作流程例項，然後點選 **[!UICONTROL 終止]** 終止正在運行的實例。

      如需使用工作流程例項的詳細資訊，請參閱 [管理工作流程例項](/help/sites-administering/workflows-administering.md).

1. 前往 [!DNL CRXDE Lite] 主控台，導覽至工作流程例項的裝載路徑，然後刪除 `payload` 節點。
1. 導覽至工作流程例項的草稿路徑，並刪除 `draft` 節點。
1. 導覽至工作流程例項的歷史記錄路徑，並刪除 `history` 節點。
1. 導覽至工作流程例項的工作流程例項路徑，並刪除 `[workflow-instance-ID]` 節點。

   >[!NOTE]
   >
   >刪除工作流實例節點將刪除所有工作流參與者的工作流實例。

1. 對於為使用者識別的所有工作流程例項，重複步驟2至6。
1. 識別並刪除AEM中的離線草稿和提交資料 [!DNL Forms] 應用程式工作流程參與者的輸出方塊，以避免任何提交至伺服器。

您也可以使用API來存取和移除節點與屬性。 如需詳細資訊，請參閱下列檔案。

* [如何以程式設計方式存取AEM JCR](/help/sites-developing/access-jcr.md)
* [刪除節點和屬性](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [API參考](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)
