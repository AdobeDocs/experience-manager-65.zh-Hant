---
title: OSGi上以Forms為中心的工作流程 | 處理使用者資料
description: OSGi上以Forms為中心的工作流程 | 處理使用者資料
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: fd0e17d7-c3e9-4dec-ad26-ed96a1881f42
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 1%

---

# OSGi上以Forms為中心的工作流程 | 處理使用者資料 {#forms-centric-workflows-on-osgi-handling-user-data}

以Forms為中心的AEM工作流程可讓您自動執行以Forms為中心的真實商業流程。 工作流程由一系列步驟組成，這些步驟會以關聯工作流程模型中指定的順序執行。 每個步驟都會執行特定動作，例如將任務指派給使用者或傳送電子郵件訊息。 工作流程可與存放庫中的資產、使用者帳戶和服務互動。 因此，工作流程可以協調涉及Experience Manager任何方面的複雜活動。

可透過下列任何方法觸發或啟動以表單為中心的工作流程：

* 從AEM收件匣提交應用程式
* 從AEM [!DNL Forms]應用程式提交應用程式
* 提交最適化表單
* 使用watched資料夾
* 提互動動式通訊或信件

如需以Forms為中心的AEM工作流程與功能的詳細資訊，請參閱OSGi上的[以Forms為中心的工作流程](/help/forms/using/aem-forms-workflow.md)。

## 使用者資料和資料存放區 {#user-data-and-data-stores}

觸發工作流程時，會自動為工作流程例項產生裝載。 每個工作流程例項都會獲指派唯一的例項ID及關聯的裝載ID。 裝載包含與工作流程例項相關聯之使用者和表單資料的存放庫位置。 此外，工作流程例項的草稿和歷史資料也會儲存在AEM存放庫中。

工作流程執行個體之裝載、草稿和歷史記錄所在的預設存放庫位置如下：

>[!NOTE]
>
>建立工作流程或應用程式時，您可以設定不同的位置來儲存裝載、草稿和歷程記錄資料。 若要識別工作流程或應用程式儲存資料的位置，請檢閱工作流程。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>工作流程<br />執行個體</strong></td>
   <td>/var/workflow/instances/[server_id]/&lt;date&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>總額</strong></td>
   <td>/var/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>草稿</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [日期]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>記錄</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以從存放庫的工作流程例項存取和刪除使用者資料。 若要完成此操作，您必須知道與使用者相關聯的工作流程例項的執行個體ID。 您可以使用起始工作流程例項的使用者名稱或工作流程例項的目前受指派人，來尋找工作流程例項的例項ID。

但是，在下列情況下識別與啟動器相關聯的工作流程時，您無法識別或結果可能模稜兩可：

* **透過watched資料夾觸發的工作流程**：如果工作流程是由watched資料夾觸發，則無法使用工作流程執行個體的啟動器來識別工作流程執行個體。 在此情況下，使用者資訊會編碼在儲存的資料中。
* **從發佈AEM執行個體啟動的工作流程**：從AEM發佈執行個體提交最適化表單、互動式通訊或字母時，所有工作流程執行個體都是使用服務使用者建立的。 在這些情況下，不會在工作流程例項資料中擷取登入使用者的使用者名稱。

### 存取使用者資料 {#access}

若要識別及存取為工作流程執行個體儲存的使用者資料，請執行下列步驟：

1. 在AEM作者執行個體上，前往`https://'[server]:[port]'/crx/de`並瀏覽至&#x200B;**[!UICONTROL 工具>查詢]**。

   從&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL SQL2]**。

1. 根據可用的資訊，執行下列其中一個查詢：

   * 如果已知工作流程發起人，請執行下列動作：

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * 如果您要尋找其資料的使用者是目前工作流程受指派人，請執行下列動作：

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   查詢會傳回指定工作流程發起人或目前工作流程受指派人之所有工作流程執行個體的位置。

   例如，下列查詢會從工作流程啟動器為`srose`的`/var/workflow/instances`節點傳回兩個工作流程執行個體路徑。

   ![工作流程執行個體](assets/workflow-instance.png)

1. 移至查詢傳回的工作流程例項路徑。 status屬性顯示工作流程執行個體的目前狀態。

   ![狀態](assets/status.png)

1. 在工作流程執行個體節點中，瀏覽至`data/payload/`。 `path`屬性會儲存工作流程執行個體之裝載的路徑。 您可以導覽至路徑，以存取裝載中儲存的資料。

   ![payload-path](assets/payload-path.png)

1. 導覽至工作流程例項的草稿與歷史記錄位置。

   例如：

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. 針對步驟2中查詢傳回的所有工作流程例項，重複步驟3至5。

   >[!NOTE]
   >
   >AEM [!DNL Forms]應用程式也會以離線模式儲存資料。 工作流程執行個體的資料可能會儲存在個別裝置上，並在應用程式與伺服器同步時，提交至[!DNL Forms]伺服器。

### 刪除使用者資料 {#delete-user-data}

您必須是AEM管理員，才能執行下列步驟，從工作流程例項刪除使用者資料：

1. 請依照[存取使用者資料](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access)中的指示操作，並注意下列事項：

   * 與使用者相關聯的工作流程例項的路徑
   * 工作流程例項的狀態
   * 工作流程例項裝載的路徑
   * 工作流程例項的草稿和歷程記錄的路徑

1. 針對&#x200B;**正在執行**、**已暫停**&#x200B;或&#x200B;**過時**&#x200B;狀態的工作流程執行個體執行此步驟：

   1. 前往`https://'[server]:[port]'/aem/start.html`並使用系統管理員認證登入。
   1. 瀏覽至&#x200B;**[!UICONTROL 工具>工作流程>執行個體]**。
   1. 選取使用者的相關工作流程執行個體，並選取&#x200B;**[!UICONTROL 終止]**&#x200B;以終止執行中的執行個體。

      如需有關使用工作流程執行個體的詳細資訊，請參閱[管理工作流程執行個體](/help/sites-administering/workflows-administering.md)。

1. 前往[!DNL CRXDE Lite]主控台，導覽至工作流程執行個體的裝載路徑，然後刪除`payload`節點。
1. 導覽至工作流程執行個體的草稿路徑，並刪除`draft`節點。
1. 導覽至工作流程執行個體的歷程記錄路徑，並刪除`history`節點。
1. 導覽至工作流程執行個體的工作流程執行個體路徑，並刪除工作流程的`[workflow-instance-ID]`節點。

   >[!NOTE]
   >
   >刪除工作流程例項節點將會移除所有工作流程參與者的工作流程例項。

1. 針對已識別的使用者之所有工作流程例項，重複步驟2至6。
1. 識別並刪除來自工作流程參與者AEM [!DNL Forms]應用程式寄件匣的離線草稿與提交資料，以避擴音交至伺服器。

您也可以使用API來存取及移除節點和屬性。 如需詳細資訊，請參閱下列檔案。

* [如何以程式設計方式存取AEM JCR](/help/sites-developing/access-jcr.md)
* [正在移除節點和屬性](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [API參考](https://helpx.adobe.com/tw/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)
