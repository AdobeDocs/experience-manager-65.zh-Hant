---
title: 打印通道和Web通道
seo-title: 打印通道和Web通道
description: 匯入列印管道範本以及建立和啟用網頁管道範本
seo-description: 匯入列印管道範本以及建立和啟用網頁管道範本
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: 互動式通訊
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# 打印通道和Web通道{#print-channel-and-web-channel}

互動式通訊可透過兩個通道提供：打印和網路。 打印渠道用於建立PDF和紙面通信，例如作為保險費付款提醒的打印信函，而Web渠道用於提供線上體驗，如網站上的信用卡對帳單。

互動式通訊作者可重複使用檔案片段和影像等資產，以建立互動式通訊的列印版和網頁版。

[建立互動式通信](../../forms/using/create-interactive-communication.md)的先決條件之一是伺服器上可用的打印和/或Web通道模板。 雖然範本作者在AEM本身建立Web管道範本，但列印管道範本XDP是在AdobeForms Designer中建立並上傳至伺服器。

## 列印管道 {#printchannel}

互動式通訊的列印通道使用XFA表單範本XDP。 XDP是在AdobeForms Designer中設計。 有關建立打印通道模板的詳細資訊，請參閱[佈局設計](../../forms/using/layout-design-details.md)。 若要在互動式通訊中使用列印管道範本，您必須將範本上傳至AEM Forms伺服器。

### 上傳互動式通訊列印通道範本{#upload-interactive-communication-print-channel-template}

若要上傳範本，您必須是表單使用者群組的成員。 使用下列步驟將列印管道範本(XDP)上傳至AEM Forms:

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。

1. 點選「**[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**」。

   導覽並選取適當的列印通道範本(XDP)，然後點選&#x200B;**[!UICONTROL Open]**。

## Web通道{#web-channel}

範本作者和管理員可以建立、編輯和啟用網頁範本。 若要允許其他使用者製作網頁範本，您必須授予他們權限。 有關詳細資訊，請參閱[用戶、組和訪問權限管理](/help/sites-administering/user-group-ac-admin.md)。

### 編寫Web通道模板{#authoring-web-channel-template}

若要建立Web管道範本，您必須先建立「範本」資料夾。 在模板資料夾內建立Web模板後，您需要啟用該模板，以允許表單用戶根據模板建立互動式通信的Web通道。

製作網路管道範本請完成下列步驟：

1. 建立「模板」資料夾以保留您的互動式通信Web模板（如果尚未建立）。 如需詳細資訊，請參閱[頁面範本 — 可編輯](/help/sites-developing/page-templates-editable.md)中的範本資料夾。

   1. 點選&#x200B;**[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 設定瀏覽器]**。
      * 如需詳細資訊，請參閱[設定瀏覽器](/help/sites-administering/configurations.md)檔案。
   1. 在「設定瀏覽器」頁面中，點選&#x200B;**[!UICONTROL Create]**。
   1. 在「建立配置」對話框中，指定資料夾的標題，檢查&#x200B;**[!UICONTROL 可編輯的模板]**，然後點選&#x200B;**[!UICONTROL 建立]**。

      資料夾會建立並列在「設定瀏覽器」頁面中。

1. 導覽至適當的範本資料夾並建立網頁範本。

   1. 通過選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 模板]** > **`[Folder]`**&#x200B;導航到相應的模板資料夾。
   1. 點選&#x200B;**[!UICONTROL 建立]**。
   1. 選擇「**[!UICONTROL 互動式通信 — Web Channel]**」，然後點選「**[!UICONTROL Next]**」。
   1. 輸入範本標題和說明，然後點選&#x200B;**[!UICONTROL Create]**。

      模板隨即建立，並出現對話框。

   1. 點選&#x200B;**[!UICONTROL 開啟]**&#x200B;以開啟您在範本編輯器中建立的範本。

      此時將顯示「模板編輯器」。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      建立或編輯範本時，範本作者可以定義各種方面。 建立或編輯範本類似於頁面編寫。 如需詳細資訊，請參閱[建立頁面範本](/help/sites-authoring/templates.md)中的編輯範本 — 範本作者。

1. 要允許使用此模板建立互動式通信，請啟用該模板。

   1. 點選&#x200B;**[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 範本]**。
   1. 導覽至適當的範本，選取它，然後點選&#x200B;**[!UICONTROL 啟用]**，在警報訊息中，點選&#x200B;**[!UICONTROL 啟用]**。

      範本已啟用，其狀態會顯示為已啟用。 現在，您可以繼續建立互動式通訊，以便使用新建立的Web通道範本。

### 將通道打印為Web通道{#print-channel-as-master-for-web-channel}的主通道

製作互動式通訊時，作者可以選取此選項，以建立與列印通道同步的網頁通道。 使用打印通道作為Web通道的主通道，確保從打印通道導出Web通道的內容、繼承和資料綁定，並且在打印通道中所做的更改可以反映在Web通道中。 不過，互動式通訊作者可視需要中斷網路通道中特定元件的繼承。

![將通道打印](assets/create_ic_print_master_new.png) ![為主Web通道將打印通道打印為主](assets/create_ic_print_master_web_new.png)
