---
title: 以Forms為中心的OSGi工作流 |處理用戶資料
seo-title: Forms-centric workflows on OSGi | Handling user data
description: 以Forms為中心的OSGi工作流 |處理用戶資料
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

# 以Forms為中心的OSGi工作流 |處理用戶資料 {#forms-centric-workflows-on-osgi-handling-user-data}

以Forms為AEM中心的工作流使您能夠自動化以Forms為中心的真實業務流程。 工作流由一系列步驟組成，這些步驟按在關聯工作流模型中指定的順序執行。 每個步驟都執行特定操作，例如將任務分配給用戶或發送電子郵件。 工作流可以與儲存庫、用戶帳戶和服務中的資產交互。 因此，工作流可以協調涉及Experience Manager任何方面的複雜活動。

可以通過以下任何方法觸發或啟動以表單為中心的工作流：

* 從收件箱提交應AEM用程式
* 提交申請AEM [!DNL Forms] 應用
* 提交自適應表單
* 使用監視資料夾
* 提交互動式通信或信函

有關以Forms為中心的工作流AEM和功能的詳細資訊，請參見 [基於OSGi的以Forms為中心的工作流](/help/forms/using/aem-forms-workflow.md)。

## 用戶資料和資料儲存 {#user-data-and-data-stores}

觸發工作流時，將自動為工作流實例生成負載。 為每個工作流實例分配一個唯一實例ID和一個關聯的負載ID。 負載包含與工作流實例關聯的用戶和表單資料的儲存庫位置。 此外，工作流實例的草稿和歷史資料也儲存在儲存AEM庫中。

工作流實例的負載、草稿和歷史記錄所在的預設儲存庫位置如下：

>[!NOTE]
>
>在建立工作流或應用程式時，可以配置不同的位置來儲存負載、草稿和歷史記錄資料。 要確定工作流或應用程式儲存資料的位置，請複查工作流。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>工作流 <br /> 實例</strong></td>
   <td>/var/workflow/instances/[server id]/&lt;date&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>裝載</strong></td>
   <td>/var/fd/dashboard/payload/[server id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/dashboard/payload/[server id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>草稿</strong></td>
   <td>/var/fd/dashboard/instances/[server id]/<br /> [日期]/[工作流實例]/draft/[workitem]/</td>
   <td>/etc/fd/dashboard/instances/[server id]/<br /> [日期]/[工作流實例]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>歷史</strong></td>
   <td>/var/fd/dashboard/instances/[server id]/<br /> [date]/[workflow_instance]/歷史記錄/</td>
   <td>/etc/fd/dashboard/instances/[server id]/<br /> [date]/[workflow_instance]/歷史記錄/</td>
  </tr>
 </tbody>
</table>

## 訪問和刪除用戶資料 {#access-and-delete-user-data}

您可以從儲存庫中的工作流實例訪問和刪除用戶資料。 要實現此目標，您必須知道與用戶關聯的工作流實例的實例ID。 通過使用啟動工作流實例的用戶或工作流實例的當前受分配者的用戶名，可以查找工作流實例的實例ID。

但是，在以下情形中識別與啟動器關聯的工作流時，您不能識別或結果可能不明確：

* **通過受監視資料夾觸發的工作流**:如果工作流由受監視的資料夾觸發，則無法使用其啟動器來標識工作流實例。 在這種情況下，用戶資訊被編碼在所儲存的資料中。
* **從發佈實例啟動的工AEM作流**:當從發佈實例提交自適應表單、交互通信或字母時，所有工作流實例都使用服務用戶AEM建立。 在這些情況下，不會在工作流實例資料中捕獲登錄用戶的用戶名。

### 訪問用戶資料 {#access}

要標識和訪問為工作流實例儲存的用戶資料，請執行以下步驟：

1. 在作AEM者實例中，轉到 `https://'[server]:[port]'/crx/de` 導航 **[!UICONTROL 「工具」>「查詢」]**。

   選擇 **[!UICONTROL SQL2]** 從 **[!UICONTROL 類型]** 下拉。

1. 根據可用資訊，執行下列查詢之一：

   * 如果已知工作流啟動器，請執行以下操作：

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * 如果要查找其資料的用戶是當前工作流受分配者，請執行以下操作：

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   查詢返回指定工作流啟動器或當前工作流任務負責人的所有工作流實例的位置。

   例如，以下查詢從 `/var/workflow/instances` 其工作流啟動器的節點 `srose`。

   ![工作流實例](assets/workflow-instance.png)

1. 轉到查詢返回的工作流實例路徑。 狀態屬性顯示工作流實例的當前狀態。

   ![狀態](assets/status.png)

1. 在工作流實例節點中，導航到 `data/payload/`。 的 `path` 屬性儲存工作流實例的負載路徑。 您可以導航到訪問儲存在負載中的資料的路徑。

   ![有效載荷路徑](assets/payload-path.png)

1. 導航到工作流實例的草稿和歷史記錄的位置。

   例如：

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. 對查詢在步驟2中返回的所有工作流實例重複步驟3 - 5。

   >[!NOTE]
   >
   >AEM [!DNL Forms] app還在離線模式下儲存資料。 工作流實例的資料可能本地儲存在單個設備上，並提交到 [!DNL Forms] 應用程式與伺服器同步時的伺服器。

### 刪除用戶資料 {#delete-user-data}

您必須是管理員AEM，才能通過執行以下步驟從工作流實例中刪除用戶資料：

1. 按照中的說明操作 [訪問用戶資料](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) 並注意以下事項：

   * 與用戶關聯的工作流實例的路徑
   * 工作流實例的狀態
   * 工作流實例的負載路徑
   * 工作流實例的草稿和歷史記錄路徑

1. 對中的工作流實例執行此步驟 **正在運行**。 **掛起**&#x200B;或 **過時** 狀態：

   1. 轉到 `https://'[server]:[port]'/aem/start.html` 並使用管理員憑據登錄。
   1. 導航到 **[!UICONTROL 「工具」>「工作流」>「實例」]**。
   1. 為用戶選擇相關的工作流實例並點擊 **[!UICONTROL 終止]** 終止正在運行的實例。

      有關使用工作流實例的詳細資訊，請參閱 [管理工作流實例](/help/sites-administering/workflows-administering.md)。

1. 轉到 [!DNL CRXDE Lite] 控制台，導航至工作流實例的負載路徑，並刪除 `payload` 的下界。
1. 導航到工作流實例的草稿路徑，然後刪除 `draft` 的下界。
1. 導航到工作流實例的歷史記錄路徑，然後刪除 `history` 的下界。
1. 導航到工作流實例的工作流實例路徑，然後刪除 `[workflow-instance-ID]` 的子菜單。

   >[!NOTE]
   >
   >刪除工作流實例節點將刪除所有工作流參與者的工作流實例。

1. 對為用戶標識的所有工作流實例重複步驟2 - 6。
1. 識別並刪除離線草稿和提交數AEM據 [!DNL Forms] 工作流參與者的應用程式外框，以避免提交到伺服器。

您還可以使用API訪問和刪除節點和屬性。 有關詳細資訊，請參閱以下文檔。

* [如何以寫程式方式訪問AEMJCR](/help/sites-developing/access-jcr.md)
* [刪除節點和屬性](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [API引用](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)
