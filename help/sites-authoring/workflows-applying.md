---
title: 將工作流程套用至頁面
seo-title: 將工作流程套用至頁面
description: 撰寫時，您可以叫用工作流程，在頁面上採取行動；您也可以套用多個工作流程。
seo-description: 撰寫時，您可以叫用工作流程，在頁面上採取行動；您也可以套用多個工作流程。
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# 將工作流程套用至頁面{#applying-workflows-to-pages}

撰寫時，您可以叫用工作流程，在頁面上採取行動；您也可以套用多個工作流程。

應用工作流時，您指定以下資訊：

* 要套用的工作流程。
您可以套用您有權存取的任何工作流程（由AEM管理員指派）。
* （可選）幫助標識用戶收件箱中工作流實例的標題。
* 工作流負載；這可以是一或多個頁面。

工作流程可從以下網址啟動：

* [Sites **主控** 台](#starting-a-workflow-from-the-sites-console)。
* [編輯頁面時，從「頁面 **資訊」**](#starting-a-workflow-from-the-page-editor)。

>[!NOTE]
>
>另請參閱:
>
>* [如何將工作流程套用至DAM資產](/help/assets/assets-workflow.md)。
>* [使用專案工作流程](/help/sites-authoring/projects-with-workflows.md)。
>



>[!NOTE]
>
>AEM管理員可以使 [用數種其他方法來啟動工作流程](/help/sites-administering/workflows-starting.md)。

## 從Sites Console啟動工作流 {#starting-a-workflow-from-the-sites-console}

您可以從以下任一位置啟動工作流：

* [「站 **點** 」工具欄的「建立」選項](#starting-a-workflow-from-the-sites-toolbar)。
* [站點 **控制台的** 「時間軸」邊欄](#starting-a-workflow-from-the-timeline)。

在這兩種情況下，您需要：

* [在「建立工作流嚮導」中指定「工作流詳細資訊」](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 從「站點」工具欄啟動工作流 {#starting-a-workflow-from-the-sites-toolbar}

您可以從Sites主控台的工具列啟動工 **作流程** :

1. 導覽至並選取所需頁面。

1. 您現在可 **以從工具列的** 「建立」選項中選取「工 **作流程」**。

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. 「創 **建工作流** 」嚮導將幫助您 [指定工作流詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 從時間軸啟動工作流 {#starting-a-workflow-from-the-timeline}

從時 **間軸** ，可以啟動要應用於選定資源的工作流。

1. [選擇資源](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) ，然後打 [開時間軸](/help/sites-authoring/basic-handling.md#timeline) （或開啟時間軸，然後選擇資源）。
1. 注釋欄位旁的箭頭可用來顯示「開始工 **作流程**:

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. 「創 **建工作流** 」嚮導將幫助您 [指定工作流詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 在建立工作流嚮導中指定工作流詳細資訊 {#specifying-workflow-details-in-the-create-workflow-wizard}

「創 **建工作流** 」嚮導將幫助您選擇工作流並指定所需的詳細資訊。

在從以下任一 **項開啟「建立工作流** 」嚮導後：

* [「站 **點** 」工具欄的「建立」選項](#starting-a-workflow-from-the-sites-toolbar)。
* [站點 **控制台的** 「時間軸」邊欄](#starting-a-workflow-from-the-timeline)。

您可以指定詳細資訊：

1. 在「屬 **性** 」(Properties)步驟中，定義了工作流的基本選項：

   * **工作流程模型**
   * **工作流程標題**

      * 您可以指定此例項的標題，以協助您在稍後階段進行識別。
   根據工作流模型，還提供以下選項。 這些功能可讓建立為裝載的套件在工作流程完成後保留。

   * **保留工作流程封裝**
   * **封裝標題**

      * 您可以指定套件的標題，以協助識別。
   >[!NOTE]
   >
   >當為「 **多資源支援」配置了工作流且已選擇多個資源時，「保**[](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) 留工作流包」選項可用。

   完成後，請使 **用** Next繼續。

   ![wf-52](assets/wf-52.png)

1. 在「范 **圍** 」步驟中，您可以選擇：

   * **新增內容** ，以開啟路 [徑瀏覽器](/help/sites-authoring/author-environment-tools.md#path-browser) ，並選取其他資源；在瀏覽器中，按一下／點選「選 **取** 」，將內容新增至工作流程例項。

   * 查看其他操作的現有資源：

      * **包含子項** ，以指定該資源的子項將包含在工作流中。
將開啟一個對話框，允許您根據以下內容調整選擇：

         * 僅包含直接子項.
         * 僅包含修改過的頁面.
         * 僅包含已發佈的頁面.
         所有指定的子項都將添加到將應用工作流的資源清單中。

      * **刪除選擇** ，從工作流中刪除該資源。
   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >如果添加其他資源，則可以使用「上 **一步** 」( **Back** )在「屬性」(Properties)步驟中調整「保留工作流程包 **」(Keep workflow package** )的設定。

1. 使用 **「建立** 」關閉嚮導並建立工作流實例。 通知會顯示在「網站」主控台中。

## 從頁面編輯器啟動工作流 {#starting-a-workflow-from-the-page-editor}

編輯頁面時，您可以從工具 **列選取「頁面資訊** 」。 下拉式選單中有「開始 **工作流程」選項**。 這將會開啟對話方塊，您可在其中指定所需的工作流程，並視需要加上標題：

![wf-54](assets/wf-54.png)
