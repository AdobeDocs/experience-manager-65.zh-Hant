---
title: 列印頻道和網頁頻道
seo-title: 列印頻道和網頁頻道
description: 匯入列印渠道範本，並建立和啟用網頁渠道範本
seo-description: 匯入列印渠道範本，並建立和啟用網頁渠道範本
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
translation-type: tm+mt
source-git-commit: a326e508a781b3afaba8b5e371aa862a30536740

---


# 列印頻道和網頁頻道{#print-channel-and-web-channel}

互動式通訊可透過兩個通道提供：平面和網頁。 列印渠道用來建立PDF和紙本通訊，例如列印信函，以提醒保險費付款，而網路渠道則用來提供線上體驗，例如在網站上提供信用卡帳單。

互動式通訊的作者可重複使用檔案片段和影像等資產，以建立互動式通訊的列印和網頁版本。

建立互動式通 [訊的先決條件之一](../../forms/using/create-interactive-communication.md) ，就是伺服器上提供列印和／或網路頻道的範本。 當範本作者在AEM中建立網頁頻道範本時，列印頻道範本XDP會在Adobe Forms Designer中建立，並上傳至伺服器。

## Print channel {#printchannel}

互動式通訊的列印頻道使用XFA表單範本XDP。 XDP是在Adobe Forms Designer中設計。 如需建立列印渠道範本的詳細資訊，請參閱版 [面設計](../../forms/using/layout-design-details.md)。 若要在您的互動式通訊中使用列印渠道範本，您必須將範本上傳至AEM Forms伺服器。

### 上傳互動式通訊列印渠道範本 {#upload-interactive-communication-print-channel-template}

若要上傳範本，您必須是表單使用者群組的成員。 使用下列步驟將列印渠道範本(XDP)上傳至AEM Forms:

1. 選擇「 **[!UICONTROL 表單]** 」>「 **[!UICONTROL 表單與檔案」]**。

1. 點選「 **[!UICONTROL 建立]** >檔案 **[!UICONTROL 上傳」]**。

   導覽並選取適當的列印渠道範本(XDP)，然後點選「 **[!UICONTROL 開啟]**」。

## Web channel {#web-channel}

範本作者和管理員可以建立、編輯和啟用Web範本。 若要允許其他使用者製作網頁範本，您必須授予他們權限。 如需詳細資訊，請參 [閱使用者、群組和存取權限管理](/help/sites-administering/user-group-ac-admin.md)。

### 編寫Web Channel範本 {#authoring-web-channel-template}

若要建立Web頻道範本，您必須先建立「範本」檔案夾。 在範本資料夾中建立Web範本後，您必須啟用範本，讓表單使用者能夠根據範本建立互動式通訊的Web頻道。

要編寫Web渠道模板，請完成以下步驟：

1. 如果您尚未建立範本，請建立範本檔案夾以保留您的互動式通訊網頁範本。 如需詳細資訊，請參閱「頁面範本中的范 [本資料夾——可編輯](/help/sites-developing/page-templates-editable.md)」。

   1. 點選「 **[!UICONTROL 工具]**![>設定](assets/tools.png) 瀏覽器 ****」。
   1. 在「設定瀏覽器」頁面中，點選「 **[!UICONTROL 建立]**」。
   1. 在「建立配置」對話框中，指定資料夾的標題，選中「可編 **[!UICONTROL 輯模板]**」，然後點 **[!UICONTROL 選「建立」]**。

      資料夾已建立並列在「配置瀏覽器」頁中。

1. 導覽至適當的範本資料夾並建立網頁範本。

   1. 選擇「工具」>「範本」>以導覽至 **[!UICONTROL 適當的範本資]********`[Folder]`**&#x200B;料夾。
   1. 點選「 **[!UICONTROL 建立]**」。
   1. 選取 **[!UICONTROL 互動式通訊——網路頻道]** ，然後點 **[!UICONTROL 選「下一步]**」。
   1. 輸入範本標題和說明，然後點選「 **[!UICONTROL 建立]**」。

      模板即會建立並顯示對話框。

   1. 點選 **[!UICONTROL 「開啟]** 」以開啟您在範本編輯器中建立的範本。

      此時將顯示「模板編輯器」。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      建立或編輯範本時，範本作者可以定義多個方面。 建立或編輯範本類似於頁面製作。 如需詳細資訊，請參閱「建立頁面範本」中的「編輯範本——范 [本作者」](/help/sites-authoring/templates.md)。

1. 若要允許使用此範本建立互動式通訊，請啟用範本。

   1. 點選「 **[!UICONTROL 工具]**![>范](assets/tools.png) 本 ****」。
   1. 導覽至適當的範本，選取範本，然後點選「 **[!UICONTROL 啟用]** 」，並在警報訊息中點選「 **[!UICONTROL 啟用」]**。

      範本已啟用，其狀態會顯示為「已啟用」。 現在，您可以繼續建立互動式通訊，以便使用新建立的Web頻道範本。

### 列印頻道為網頁頻道的主要內容 {#print-channel-as-master-for-web-channel}

在製作互動式通訊時，作者可以選取這個選項來建立與列印頻道同步的網頁頻道。 使用印刷頻道作為網頁頻道的主版，可確保網頁頻道的內容、繼承和資料系結是從印刷頻道衍生而來，而且印刷頻道中所做的變更可反映在網頁頻道中。 不過，「互動式通訊」作者可視需要中斷網頁頻道中特定元件的繼承。

![列印頻道為主](assets/create_ic_print_master_new.png) Web ![頻道，列印頻道為主](assets/create_ic_print_master_web_new.png)

