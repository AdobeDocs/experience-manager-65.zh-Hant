---
title: 開始工作流程
description: 瞭解如何在Adobe Experience Manager中管理工作流程，以便使用各種方法手動或自動啟動工作流程。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---

# 開始工作流程{#starting-workflows}

管理工作流程時，您可以使用各種方法來啟動工作流程：

* 手動：

   * 來自[工作流程模型](#workflow-models)。
   * 正在使用[批次處理](#workflow-packages-for-batch-processing)的工作流程封裝。

* 自動：

   * 回應節點變更；[使用啟動器](#workflows-launchers)。

>[!NOTE]
>
>作者也可以使用其他方法；如需完整詳細資訊，請參閱：
>
>* [將工作流程套用至頁面](/help/sites-authoring/workflows-applying.md)
>* [如何將工作流程套用至DAM資產](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [翻譯專案](/help/sites-administering/tc-manage.md)
>

## 工作流程模型 {#workflow-models}

您可以根據「工作流程模型」控制檯上列出的其中一個模型[&#128279;](/help/sites-administering/workflows.md#workflow-models-and-instances)來啟動工作流程。 唯一強制資訊是裝載，但也可以新增標題和/或評論。

## 工作流程啟動器 {#workflows-launchers}

工作流程啟動器會監控內容存放庫中的變更，以根據已變更節點的位置和資源型別啟動工作流程。

使用&#x200B;**啟動器**，您可以：

* 檢視已為特定節點啟動的工作流程。
* 選取在建立/修改/移除特定節點/節點型別時要啟動的工作流程。
* 移除現有的工作流程與節點關係。

可以為任何節點建立啟動器。 不過，變更某些節點不會啟動工作流程。 變更下列路徑下的節點不會導致工作流程啟動：

* `/var/workflow/instances`
* 位於`/home/users`分支中任何位置的任何工作流程收件匣節點
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * 例外狀況：變更`/var/statistics/tracking` *do*&#x200B;下的節點會導致工作流程啟動。

標準安裝包含各種定義。 這些是用於數位資產管理和社會合作任務：

![wf-100](assets/wf-100.png)

## 批次處理的工作流程封裝 {#workflow-packages-for-batch-processing}

工作流程封裝是可傳遞給工作流程作為處理之裝載的封裝，可允許處理多個資源。

工作流程封裝：

* 包含一組資源（如頁面、資產）的連結。
* 包含封裝資訊，例如，建立日期、建立封裝的使用者以及簡短說明。
* 是使用專用頁面範本定義的；這類頁面可讓使用者指定封裝中的資源。
* 可多次使用。
* 可在工作流程例項實際執行時由使用者變更（新增或移除資源）。

## 從模型控制檯啟動工作流程 {#starting-a-workflow-from-the-models-console}

1. 使用&#x200B;**工具**、**工作流程**，然後使用&#x200B;**模型**，瀏覽至&#x200B;**模型**&#x200B;主控台。
1. 選取工作流程（根據主控台檢視）；如有需要，您也可以使用搜尋（左上方）：

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >**[暫時](/help/sites-developing/workflows.md#transient-workflows)**&#x200B;指標顯示未保留工作流程歷史記錄的工作流程。

1. 從工具列選取&#x200B;**啟動工作流程**。
1. 「執行工作流程」對話方塊開啟，讓您指定：

   * **承載**

     這可以是頁面、節點、資產、套件和其他資源。

   * **標題**

     有助於識別此執行個體的選用標題。

   * **註解**

     可協助指出此執行個體詳細資料的可選註解。

   ![wf-104](assets/wf-104.png)

## 建立啟動器組態 {#creating-a-launcher-configuration}

1. 使用&#x200B;**工具**、**工作流程**，然後使用&#x200B;**啟動器**，瀏覽至&#x200B;**工作流程啟動器**&#x200B;主控台。
1. 選取&#x200B;**建立**，然後選取&#x200B;**新增啟動器**&#x200B;以開啟對話方塊：

   ![wf-105](assets/wf-105.png)

   * **事件型別**

     啟動工作流程的事件型別：

      * 已建立
      * 已修改
      * 已移除

   * **節點型別**

     工作流程啟動器套用的節點型別。

   * **路徑**

     工作流程啟動器套用的路徑。

   * **執行模式**

     工作流程啟動器套用的伺服器型別。 選取&#x200B;**作者**、**Publish**&#x200B;或&#x200B;**作者與Publish**。

   * **條件**

     節點值的條件清單，評估後會決定是否啟動工作流程。 例如，下列條件會導致工作流程在節點具有值為User的屬性名稱時啟動：

     name==User

   * **功能**

     要啟用的功能清單。 使用下拉式選取器選取所需的功能。

   * **已停用的功能**

   要停用的功能清單。 使用下拉式選取器選取所需的功能。

   * **工作流程模型**

     當事件型別發生在定義條件下的節點型別和/或路徑上時要啟動的工作流程。

   * **說明**

     您自己的文字，用於說明和識別啟動器設定。

   * **啟動**

     控制是否啟動工作流程啟動器：

      * 選取&#x200B;**啟用**，在組態屬性滿足時啟動工作流程。
      * 選取&#x200B;**當工作流程不應執行時停用** （即使組態屬性已滿足，也不會執行）。

   * **排除清單**

     這會指定在決定是否應觸發工作流程時，要排除的任何JCR事件（即忽略）。

     此啟動器屬性是以逗號分隔的專案清單： &quot;

      * `property-name`忽略在指定屬性名稱上觸發的任何`jcr`事件。&quot;
      * `event-user-data:<*someValue*>`會忽略任何包含透過[`ObservationManager` API](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String))設定的`*<someValue*`> `user-data`的事件。

     例如：

     `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

     此功能可用來新增排除專案，以忽略其他工作流程處理作業所觸發的任何變更：

     `event-user-data:changedByWorkflowProcess`

1. 選取&#x200B;**建立**，以建立啟動器並返回主控台。

   發生適當的事件時，就會觸發啟動器，並啟動工作流程。

## 管理啟動器設定 {#managing-a-launcher-configuration}

建立啟動器組態之後，您可以使用相同的主控台來選取執行個體，然後&#x200B;**檢視屬性** （並加以編輯）或&#x200B;**刪除**。
