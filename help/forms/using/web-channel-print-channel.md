---
title: 打印通道和Web通道
seo-title: Print channel and web channel
description: 導入打印渠道模板以及建立和啟用Web渠道模板
seo-description: Importing print channel templates and creating and enabling web channel templates
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 打印通道和Web通道{#print-channel-and-web-channel}

互動式通信可以通過兩種渠道進行：打印和Web。 該打印通道用於建立PDF和紙張通信，例如作為保險費支付的提醒的打印信函，而該網路通道用於提供諸如網站上的信用卡對帳單等線上體驗。

互動式通信作者可以重用諸如文檔片段和影像之類的資產來建立互動式通信的打印和Web版本。

其中一個先決條件 [建立互動式通信](../../forms/using/create-interactive-communication.md) 即使伺服器上有可用於打印和/或Web通道的模板。 當模板作者自己建立Web通道模板AEM時，打印通道模板XDP是在AdobeForms設計器中建立的，並上載到伺服器。

## 打印通道 {#printchannel}

互動式通信的打印通道使用XFA表單模板XDP。 XDP是在AdobeForms設計師中設計的。 有關建立打印渠道模板的詳細資訊，請參閱 [佈局設計](../../forms/using/layout-design-details.md)。 要在交互通信中使用打印通道模板，您需要將模板上載到AEM Forms伺服器。

### 上載交互通信打印通道模板 {#upload-interactive-communication-print-channel-template}

要上載模板，您需要是表單用戶組的成員。 使用以下步驟將打印通道模板(XDP)上載到AEM Forms:

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。

1. 點擊 **[!UICONTROL 建立]** > **[!UICONTROL 檔案上載]**。

   導航並選擇適當的打印通道模板(XDP)，然後點擊 **[!UICONTROL 開啟]**。

## Web通道 {#web-channel}

模板作者和管理員可以建立、編輯和啟用Web模板。 要允許其他用戶建立Web模板，您需要授予其權限。 有關詳細資訊，請參見 [用戶、組和訪問權限管理](/help/sites-administering/user-group-ac-admin.md)。

### 創作Web渠道模板 {#authoring-web-channel-template}

要建立Web通道模板，需要先建立Template資料夾。 在模板資料夾內建立Web模板後，需要啟用該模板，以便表單用戶能夠基於該模板建立互動式通信的Web通道。

要編寫Web通道模板，請完成以下步驟：

1. 建立模板資料夾以保留Interactive Communication Web模板（如果尚沒有）。 有關詳細資訊，請參閱中的模板資料夾 [頁面模板 — 可編輯](/help/sites-developing/page-templates-editable.md)。

   1. 點擊 **[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 配置瀏覽器]**。
      * 查看 [配置瀏覽器](/help/sites-administering/configurations.md) 的子菜單。
   1. 在「配置瀏覽器」頁中，按一下 **[!UICONTROL 建立]**。
   1. 在「建立配置」對話框中，指定資料夾的標題，選中 **[!UICONTROL 可編輯模板]**，然後點擊 **[!UICONTROL 建立]**。

      資料夾將建立並列在「配置瀏覽器」頁中。

1. 導航到相應的模板資料夾並建立Web模板。

   1. 通過選擇 **[!UICONTROL 工具]** > **[!UICONTROL 模板]** > **`[Folder]`**。
   1. 點擊 **[!UICONTROL 建立]**。
   1. 選擇 **[!UICONTROL 互動式通信 — Web通道]** 點擊 **[!UICONTROL 下一個]**。
   1. 輸入模板標題和說明，然後點擊 **[!UICONTROL 建立]**。

      將建立模板並顯示一個對話框。

   1. 點擊 **[!UICONTROL 開啟]** 開啟在模板編輯器中建立的模板。

      此時將顯示「模板編輯器」。

      ![WebChannel模板](assets/webchanneltemplate.png)

      建立或編輯模板時，「模板作者」可以定義多個方面。 建立或編輯模板與頁面創作類似。 有關詳細資訊，請參閱中的編輯模板 — 模板作者 [建立頁面模板](/help/sites-authoring/templates.md)。

1. 要允許使用此模板建立交互通信，請啟用該模板。

   1. 點擊 **[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 模板]**。
   1. 導航到相應模板，選擇它，然後點擊 **[!UICONTROL 啟用]** 在警報消息中，點擊 **[!UICONTROL 啟用]**。

      模板已啟用，其狀態顯示為「已啟用」。 現在，您可以繼續建立互動式通信，以便使用新建立的Web通道模板。

### 作為Web頻道首頁打印頻道 {#print-channel-as-master-for-web-channel}

創作交互通信時，作者可以選擇此選項以建立與打印通道同步的Web通道。 使用打印通道作為Web頻道的主節點，確保Web頻道的內容、繼承和資料綁定從打印通道導出，並且打印通道中所做的更改可以反映在Web頻道中。 但是，允許互動式通信作者根據需要中斷Web通道中特定元件的繼承。

![將通道打印為主](assets/create_ic_print_master_new.png) ![以打印通道為主的Web通道](assets/create_ic_print_master_web_new.png)
