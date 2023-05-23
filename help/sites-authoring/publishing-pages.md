---
title: 發佈內容頁面
description: 瞭解如何發佈內容頁面。
uuid: 57795e4a-e528-4e74-ad9c-e13f868daebb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1f5eb646-acc7-49d5-b839-e451e68ada9e
docset: aem65
exl-id: 61144bbe-6710-4cae-a63e-e708936ff360
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 7%

---

# 發佈頁面 {#publishing-pages}

在您建立並查看了有關作者環境的內容後， [在你的公共網站上公佈](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) （您的發佈環境）。

這稱為發佈頁面。 當要從發佈環境中刪除頁面時，稱為取消發佈。 在發佈和取消發佈頁面時，該頁面在作者環境中仍然可用，以便進行進一步更改，直到您將其刪除。

您還可以立即發佈/取消發佈頁面，或在將來的預定義日期/時間發佈/取消發佈頁面。

>[!NOTE]
>
>某些與發佈相關的術語可能會被混淆：
>
>* **發佈/取消發佈**
   >  這些是使您的內容在發佈環境中（或不在發佈環境中）公開可用的操作的主要條款。
>
>* **激活/停用**
   >  這些術語與發佈/取消發佈是同義的。
>
>* **複製/複製**
   >  這些技術術語描述資料從一個環境移動到另一個環境（例如發佈或反向複製用戶注釋時）的移動。
>


>[!NOTE]
>
>如果您沒有發佈特定頁面所需的權限：
>
>* 將觸發一個工作流以通知相應人員您的發佈請求。
>* 此 [工作流可能已定制](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) 你的開發團隊。
>* 將短暫顯示一條消息，通知您工作流已觸發。
>


## 發佈頁面 {#publishing-pages-1}

根據您的位置，您可以發佈：

* [從頁面編輯器](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [從站點控制台](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### 從編輯器發佈 {#publishing-from-the-editor}

如果正在編輯頁面，則可以直接從編輯器發佈該頁面。

1. 選擇 **頁面資訊** 表徵圖，然後 **發佈頁面** 的雙曲餘切值。

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. 根據頁面是否具有需要發佈的引用：

   * 如果沒有要發佈的引用，將直接發佈該頁面。
   * 如果頁面有需要發佈的引用，則這些引用將列在 **發佈** 中，您可以執行以下操作：

      * 指定哪些資產/標籤/等。 要與頁面一起發佈，然後使用 **發佈** 來完成此過程。

      * 使用 **取消** 中止操作。

   ![chlimage_1](assets/chlimage_1.png)

1. 選擇 **發佈** 將該頁面複製到發佈環境。 在頁面編輯器中，將顯示確認發佈操作的資訊標題。

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   在控制台中查看同一頁時，更新的發佈狀態可見。

   ![pp-01](assets/pp-01.png)

>[!NOTE]
>
>從編輯器發佈是淺層發佈，即僅發佈/發佈所選頁面/頁面，而任何子頁面均未發佈。

>[!NOTE]
>
>訪問者 [別名](/help/sites-authoring/editing-page-properties.md#advanced) 無法發佈。 編輯器中的發佈選項僅可用於通過實際路徑訪問的頁面。

### 從控制台發佈 {#publishing-from-the-console}

在站點控制台中，有兩個發佈選項：

* [快速發佈](/help/sites-authoring/publishing-pages.md#quick-publish)
* [管理發佈](/help/sites-authoring/publishing-pages.md#manage-publication)

#### 快速發佈 {#quick-publish}

**快速發佈** 是針對簡單情況，並立即發佈所選頁面，而不需要進行任何進一步的交互。 因此，任何未發佈的引用也將自動發佈。

要發佈具有「快速發佈」的頁面：

1. 在站點控制台中選擇頁面，然後按一下 **快速發佈** 按鈕

   ![pp-02](assets/pp-02.png)

1. 在「快速發佈」對話框中，按一下 **發佈** 或按一下取消 **取消**。 請記住，所有未發佈的引用都將自動發佈。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 在發佈頁面時，將顯示確認發佈的警報。

>[!NOTE]
>
>「快速發佈」是淺層發佈，即僅發佈/發佈選定的頁面/頁面，而任何子頁面均未發佈。

#### 管理發佈 {#manage-publication}

**管理發布** 提供了比「快速發佈」更多的選項，允許包含子頁、自定義引用、啟動任何適用的工作流，以及提供以後發佈的選項。

要使用「管理發布」發佈或取消發佈頁面：

1. 在站點控制台中選擇頁面，然後按一下 **管理發布** 按鈕

   ![pp-02-1](assets/pp-02-1.png)

1. 「管 **理出版物** 」嚮導將啟動。第一步， **選項**，允許您：

   * 選擇以發佈或取消發佈所選頁面。
   * 選擇立即或稍後執行該操作。

   稍後發佈將啟動工作流，以在指定時間發佈所選頁或頁。 相反，稍後取消發佈會啟動工作流以在特定時間取消發佈所選頁面。

   如果要在以後取消發佈/取消發佈，請轉到 [工作流控制台](/help/sites-administering/workflows.md) 以終止相應的工作流。

   ![chlimage_1-2](assets/chlimage_1-2.png)

   按一下 **下一個** 繼續。

1. 在「管理發布」嚮導的下一步中， **範圍**，可以定義發佈/取消發佈的範圍，例如包括以包括子頁和/或包括引用。

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   您可以使用「新 **增內容** 」按鈕，在要發佈的頁面清單中新增其他頁面，以防您在啟動「管理出版物」精靈之前未選取其中一個頁面。

   按一下「添加內容」按鈕將啟動 [路徑瀏覽器](/help/sites-authoring/author-environment-tools.md#path-browser) 允許內容選擇。

   選擇所需的頁面，然後按一下 **選擇** 將內容添加到嚮導或**取消**取消選擇並返回嚮導。

   返回嚮導後，可以在清單中選擇項目以配置其其他選項，如：

   * 包括其子項。
   * 將其從所選內容中刪除。
   * 管理其已發佈的引用。

   ![pp-03](assets/pp-03.png)

   按一下 **包括子項** 開啟對話框，您可以：

   * 僅包含直接子項.
   * 僅包含修改過的頁面.
   * 僅包含已發佈的頁面.

   按一下 **添加** 將子頁面添加到要發佈或未發佈的頁面清單中。 按一下 **取消** 的子菜單。

   ![chlimage_1-3](assets/chlimage_1-3.png)

   返回到嚮導時，您會看到根據您在「包括子項」對話框中的選項選擇添加的頁。

   通過選擇頁面，然後按一下 **已發佈引用** 按鈕

   ![pp-04](assets/pp-04.png)

   的 **已發佈引用** 對話框顯示所選內容的引用。 預設情況下，它們都被選中並將被發佈/取消發佈，但您可以取消選中以將其指定為操作，以便不將它們包括在操作中。

   按一下 **完成** 保存更改或 **取消** 的子菜單。

   回到嚮導中， **引用** 將更新列以反映您選擇的要發佈或未發佈的引用。

   ![pp-05](assets/pp-05.png)

1. 按一下 **發佈** 完成。

   在站點控制台中，一條通知消息將確認發佈。

1. 如果已發佈頁面與工作流關聯，則它們可能會在最終檔案中顯示 **工作流** 的子菜單。

   >[!NOTE]
   >
   >的 **工作流** 步驟將根據用戶可能擁有或不擁有的權限顯示。 查看 [此頁上的前一個注釋](/help/sites-authoring/publishing-pages.md#main-pars-note-0-ejsjqg-refd) 關於發佈權限 [管理對工作流的訪問](/help/sites-administering/workflows-managing.md) 和 [將工作流應用於頁面](/help/sites-authoring/workflows-applying.md#main-pars-text-5-bvhbkh-refd) 的雙曲餘切值。

   資源按觸發的工作流和每個給定選項分組，以：

   * 定義工作流的標題。
   * 保留工作流包，前提是工作流具有 [多資源支援](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)。
   * 如果選擇了保留工作流包的選項，則定義工作流包的標題。

   按一 **下「發佈** 」或「 **稍後發佈** 」以完成出版。

   ![chlimage_1-4](assets/chlimage_1-4.png)

## 取消發佈頁面 {#unpublishing-pages}

取消發佈頁面將從您的發佈環境中刪除它，這樣讀者就無法再使用它了。

在 [與出版類似](/help/sites-authoring/publishing-pages.md#publishing-pages)，可以取消發佈一個或多個頁面：

* [從頁面編輯器](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [從站點控制台](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### 從編輯器取消發佈 {#unpublishing-from-the-editor}

編輯頁面時，如果要取消發佈該頁面，請選擇 **取消發佈頁面** 的 **頁面資訊** 菜單，就像你 [發佈頁面](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)。

>[!NOTE]
>
>訪問者 [別名](/help/sites-authoring/editing-page-properties.md#advanced) 不能取消發佈。 編輯器中的發佈選項僅可用於通過實際路徑訪問的頁面。

### 從控制台取消發佈 {#unpublishing-from-the-console}

就像你 [使用「管理發布」選項發佈](/help/sites-authoring/publishing-pages.md#manage-publication)，也可以使用它取消發佈。

1. 在站點控制台中選擇頁面，然後按一下 **管理發布** 按鈕
1. 「管 **理出版物** 」嚮導將啟動。在第一個步驟中， **選項**，選擇「取消發佈」(Unpublish **)，而非「發佈」(Publish)的預設** 選項 ****。

   ![chlimage_1-5](assets/chlimage_1-5.png)

   正如稍後發佈啟動工作流以在指定時間發佈此版本的頁面一樣，稍後停用將啟動工作流以在特定時間取消發佈所選頁面或頁面。

   如果要在以後取消發佈/取消發佈，請轉到 [工作流控制台](/help/sites-administering/workflows.md) 以終止相應的工作流。

1. 要完成取消發佈，請按您希望的方式繼續嚮導 [發佈頁面](/help/sites-authoring/publishing-pages.md#manage-publication)。

## 發佈和取消發佈樹 {#publishing-and-unpublishing-a-tree}

當您輸入或更新了大量內容頁面（所有內容都駐留在同一根頁面下）時，在一個操作中發佈整個樹會更容易。

您可以使用 [管理發布](/help/sites-authoring/publishing-pages.md#manage-publication) 選項。

1. 在站點控制台中，選擇要發佈或取消發佈的樹的根頁，然後選擇 **管理發布**。
1. 「管 **理出版物** 」嚮導將啟動。選擇發佈或取消發佈，並選擇何時發佈 **下一個** 繼續。
1. 在 **範圍** 步驟，選擇根頁並選擇 **包括子項**。

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. 在 **包括子項** 對話框，取消選中選項：

   * 僅包含直接子項
   * 僅包含已發佈的頁面

   預設情況下，這些選項處於選中狀態，因此必須記住要取消選擇它們。 按一下 **添加** 確認內容並將其添加到發佈/取消發佈。

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. 的 **管理發布** 嚮導列出要查看的樹的內容。 可以通過添加附加頁或刪除那些選定的頁來進一步定制所選內容。

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   請記住，您也可以通過 **已發佈引用** 的雙曲餘切值。

1. [繼續正常管理發布嚮導](#manage-publication) 完成樹的發佈或取消發佈。

## 確定發佈狀態 {#determining-publication-status}

您可以確定頁面的發佈狀態：

* 在 [站點控制台上的資源概述資訊](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   ![螢幕抓拍_2019-03-05at112019](assets/screen-shot_2019-03-05at112019.png)

   發佈狀態會顯示在 [網站主控台](/help/sites-authoring/basic-handling.md#card-view)[的卡片](/help/sites-authoring/basic-handling.md#column-view)、欄和 [清單檢視中](/help/sites-authoring/basic-handling.md#list-view) 。

* 在 [時間](/help/sites-authoring/basic-handling.md#timeline)

   ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* 在 [頁面資訊菜單](/help/sites-authoring/author-environment-tools.md#page-information) 編輯頁面時

   ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
