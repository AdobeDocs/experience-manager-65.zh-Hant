---
title: 開始工作流程
seo-title: Starting Workflows
description: 瞭解如何在中啟動工作AEM流。
seo-description: Learn how to start Workflows in AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 4%

---

# 開始工作流程{#starting-workflows}

管理工作流時，可以使用多種方法啟動它們：

* 手動：

   * 從 [工作流模型](#workflow-models)。
   * 使用工作流包 [批處理](#workflow-packages-for-batch-processing)。

* 自動：

   * 響應節點變化； [使用啟動程式](#workflows-launchers)。

>[!NOTE]
>
>其他方法也可供作者使用；有關完整詳細資訊，請參閱：
>
>* [將工作流程套用至頁面](/help/sites-authoring/workflows-applying.md)
>* [如何將工作流應用於DAM資產](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [翻譯專案](/help/sites-administering/tc-manage.md)
>


## 工作流程模型 {#workflow-models}

可以啟動工作流 [基於其中一個模型](/help/sites-administering/workflows.md#workflow-models-and-instances) 列在「工作流模型」(Workflow Models)控制台上。 唯一的強制資訊是負載，不過也可以添加標題和/或注釋。

## 工作流啟動程式 {#workflows-launchers}

工作流啟動程式監視內容儲存庫中的更改，以根據更改的節點的位置和資源類型啟動工作流。

使用 **啟動程式** 您可以：

* 請參閱已為特定節點啟動的工作流。
* 選擇在建立/修改/刪除特定節點/節點類型時要啟動的工作流。
* 刪除現有的工作流到節點關係。

可以為任何節點建立啟動程式。 但是，對某些節點所做的更改不會啟動工作流。 對以下路徑下的節點所做的更改不會導致工作流啟動：

* `/var/workflow/instances`
* 位於 `/home/users` 分支
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * 異常：對以下節點的更改 `/var/statistics/tracking` *做* 啟動工作流。

標準安裝中包含各種定義。 這些功能用於數字資產管理和社會協作任務：

![wf-100](assets/wf-100.png)

## 批處理的工作流包 {#workflow-packages-for-batch-processing}

工作流包是可以作為負載傳遞給工作流以進行處理的包，允許處理多個資源。

工作流包：

* 包含到一組資源（如頁面、資產）的連結。
* 包含包資訊，如建立日期、建立包的用戶和簡短說明。
* 使用專用頁面模板定義；這樣的頁面允許用戶指定包中的資源。
* 可多次使用。
* 可以由用戶在工作流實例實際運行時更改（添加或刪除資源）。

## 從模型控制台啟動工作流 {#starting-a-workflow-from-the-models-console}

1. 導航到 **模型** 控制台使用 **工具**。 **工作流**，則 **模型**。
1. 選擇工作流（根據控制台視圖）;如果需要，還可以使用搜索（左上）:

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >的 **[瞬態](/help/sites-developing/workflows.md#transient-workflows)** 指示符顯示不會保留工作流歷史記錄的工作流。

1. 選擇 **啟動工作流** 的子菜單。
1. 將會開啟「運行工作流」對話框，允許您指定：

   * **裝載**

      這可以是頁、節點、資產、包等其他資源。

   * **標題**

      幫助標識此實例的可選標題。

   * **評論**

      用於幫助指明此實例的詳細資訊的可選注釋。
   ![wf-104](assets/wf-104.png)

## 建立啟動程式配置 {#creating-a-launcher-configuration}

1. 導航到 **工作流啟動程式** 控制台使用 **工具**。 **工作流**，則 **發射器**。
1. 選擇 **建立**，則 **添加啟動程式** 開啟對話框：

   ![wf-105](assets/wf-105.png)

   * **事件類型**

      將啟動工作流的事件類型：

      * 建立日期
      * 修改時間
      * 已移除
   * **節點類型**

      工作流啟動程式應用於的節點類型。

   * **路徑**

      工作流啟動程式應用於的路徑。

   * **執行模式**

      工作流啟動程式應用於的伺服器類型。 選擇 **作者**。 **發佈**&#x200B;或 **作者和發佈**。

   * **條件**

      節點值的條件清單，在計算時，它確定是否啟動工作流。 例如，當節點具有具有值User的屬性名時，以下條件會導致工作流啟動：

      name==用戶

   * **功能**

      要啟用的功能清單。 使用下拉選擇器選取所需的特徵。

   * **停用的功能**

   要禁用的功能清單。 使用下拉選擇器選取所需的特徵。

   * **工作流程模型**

      在定義的「條件」下的「節點類型」和/或「路徑」上發生「事件類型」時要啟動的工作流。

   * **說明**

      您自己的文本，用於描述和標識啟動程式配置。

   * **啟動**

      控制是否激活工作流啟動程式：

      * 選擇 **啟用** 在滿足配置屬性時啟動工作流。
      * 選擇 **禁用** 當工作流不應執行時（即使配置屬性已滿足時也不會執行）。
   * **排除清單**

      這指定在確定是否應觸發工作流時要排除（即忽略）的任何JCR事件。

      此啟動器屬性是以逗號分隔的項清單：&quot;

      * `property-name` 忽略 `jcr` 在指定的屬性名稱上觸發的事件。&quot;
      * `event-user-data:<*someValue*>` 忽略包含 `*<someValue*`> `user-data` 穿過 [ `ObservationManager` API](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String)。

      例如：

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      此功能可用於通過添加排除項來忽略其他工作流進程觸發的任何更改：

      `event-user-data:changedByWorkflowProcess`





1. 選擇 **建立**，建立啟動程式並返回控制台。

   發生相應事件後，啟動程式將被觸發並啟動工作流。

## 管理啟動程式配置 {#managing-a-launcher-configuration}

建立啟動程式配置後，可以使用同一控制台選擇實例，然後 **查看屬性** （並編輯它們）或 **刪除**。
