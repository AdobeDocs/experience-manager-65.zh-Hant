---
title: 發佈內容頁面
description: 瞭解如何在Adobe Experience Manager 6.5中發佈內容頁面。
exl-id: 61144bbe-6710-4cae-a63e-e708936ff360
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 7%

---

# 發佈頁面 {#publishing-pages}

在製作環境中建立和檢閱您的內容後， [使其可在您的公用網站上使用](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) （您的發佈環境）。

這稱為發佈頁面。 從發佈環境中移除頁面時，系統會將其稱為取消發佈。 發佈和取消發佈頁面時，作者環境仍會提供進一步的變更，直到您刪除它為止。

您也可以立即發佈/取消發佈頁面，或在預先定義的未來日期/時間發佈/取消發佈頁面。

>[!NOTE]
>
>可能會混淆與發佈相關的某些術語：
>
>* **發佈/取消發佈**
>  這些是讓您的內容在發佈環境中公開使用（或不公開使用）的動作主要詞語。
>
>* **啟用/停用**
>  這些辭彙與發佈/取消發佈同義。
>
>* **復寫/複製**
>  這些是技術術語，說明資料（例如頁面內容、檔案、程式碼、使用者註解）從一個環境移動到另一個環境，例如發佈或反向複製使用者註解時。
>

>[!NOTE]
>
>如果您沒有發佈特定頁面所需的許可權：
>
>* 系統會觸發工作流程，將您要發佈的請求通知適當人員。
>* 這個 [工作流程可能已經過自訂](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) 由您的開發團隊提供。
>* 系統會顯示簡短的訊息，通知您工作流程已觸發。
>

## 發佈頁面 {#publishing-pages-1}

根據您的位置，您可以發佈：

* [從頁面編輯器](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [從網站主控台](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### 從編輯器發佈 {#publishing-from-the-editor}

如果您正在編輯頁面，可以直接從編輯器發佈頁面。

1. 選取 **頁面資訊** 圖示以開啟功能表，然後 **發佈頁面** 選項。

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. 視頁面是否有需要發佈的參照而定：

   * 如果沒有要發佈的引用，則會直接發佈頁面。
   * 如果頁面含有需要發佈的引用，這些引用將會列在 **發佈** 精靈，您可在其中執行以下其中一項作業：

      * 指定要與頁面一起發佈的資產或標籤，然後使用 **發佈** 以完成程式。

      * 使用 **取消** 以中止動作。

   ![chlimage_1](assets/chlimage_1.png)

1. 選取 **發佈** 會將頁面復寫至發佈環境。 在頁面編輯器中，會顯示確認發佈動作的資訊橫幅。

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   在主控台中檢視相同頁面時，會顯示更新的發佈狀態。

   ![pp-01](assets/pp-01.png)

>[!NOTE]
>
>從編輯器發佈是淺層發佈，也就是說，僅發佈選定的一個或多個頁面，不發佈任何子頁面。

>[!NOTE]
>
>頁面存取者： [別名](/help/sites-authoring/editing-page-properties.md#advanced) 在編輯器中無法發佈。 編輯器中的發佈選項僅適用於透過實際路徑存取的頁面。

### 從主控台發佈 {#publishing-from-the-console}

在網站主控台中，有兩個發佈選項：

* [快速發佈](/help/sites-authoring/publishing-pages.md#quick-publish)
* [管理發佈](/help/sites-authoring/publishing-pages.md#manage-publication)

#### 快速發佈 {#quick-publish}

**快速發佈** 適用於簡單案例，並立即發佈所選頁面，無需進行任何進一步互動。 因此，任何未發佈的參考也會自動發佈。

若要使用「快速發佈」功能發佈頁面：

1. 在網站主控台中選取一個或多個頁面，然後按一下 **快速發佈** 按鈕。

   ![pp-02](assets/pp-02.png)

1. 在「快速發佈」對話方塊中，按一下以確認發佈 **發佈** 或按一下以取消 **取消**. 請記住，任何未發佈的參考也會自動發佈。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 發佈頁面時，畫面會顯示確認發佈的警報。

>[!NOTE]
>
>快速發佈是淺層發佈，也就是說，只會發佈選取的頁面，而不會發佈任何子頁面。

#### 管理發佈 {#manage-publication}

**管理發布** 提供比「快速發佈」更多的選項，允許包含子頁面、自訂參照和啟動任何適用的工作流程，並提供在以後的日期發佈的選項。

若要使用「管理發布」來發佈或取消發佈頁面：

1. 在網站主控台中選取一個或多個頁面，然後按一下 **管理發布** 按鈕。

   ![pp-02-1](assets/pp-02-1.png)

1. 「管 **理出版物** 」嚮導將啟動。第一步， **選項**，可讓您：

   * 選擇發佈或取消發佈選取的頁面。
   * 選擇現在或稍後採取該動作。

   稍後發佈會啟動工作流程，以在指定時間發佈選取的一或多個頁面。 相反地，稍後取消發佈會啟動工作流程，以在特定時間取消發佈選取的一個或多個頁面。

   如果您想稍後再取消發佈/取消發佈，請前往 [工作流程主控台](/help/sites-administering/workflows.md) 以終止對應的工作流程。

   ![chlimage_1-2](assets/chlimage_1-2.png)

   按一下 **下一個** 以繼續。

1. 在管理出版物精靈的下一個步驟中， **範圍**，您可以定義發佈/取消發佈的範圍，例如包括子頁面和/或包括引用。

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   您可以使用「新 **增內容** 」按鈕，在要發佈的頁面清單中新增其他頁面，以防您在啟動「管理出版物」精靈之前未選取其中一個頁面。

   按一下「新增內容」按鈕以開始 [路徑瀏覽器](/help/sites-authoring/author-environment-tools.md#path-browser) 以允許選擇內容。

   選取所需頁面，然後按一下 **選取** 將內容新增到精靈，或**取消**取消選取並返回精靈。

   回到精靈，您可以選取清單中的專案以設定其進一步的選項，例如：

   * 包括其子項。
   * 將其從選取範圍中移除。
   * 管理其已發佈的引用。

   ![pp-03](assets/pp-03.png)

   按一下 **包含子項** 開啟對話方塊，允許您：

   * 僅包含直接子項。
   * 僅包含已修改的頁面。
   * 僅包含已發佈的頁面。

   按一下 **新增** 根據選取選項，將子頁面新增至要發佈或取消發佈的頁面清單中。 按一下 **取消** 以取消選取範圍並返回精靈。

   ![chlimage_1-3](assets/chlimage_1-3.png)

   回到精靈後，您會看到根據您在「包含子項」對話方塊中選擇的選項新增的頁面。

   選取頁面，然後按一下「 」，即可檢視及修改該頁面要發佈或取消發佈的引用 **已發佈引用** 按鈕。

   ![pp-04](assets/pp-04.png)

   此 **已發佈引用** 對話方塊會顯示所選內容的參照。 預設會選取這些變數，並將予以發佈/取消發佈，但您可以取消勾選以取消選取，以便這些變數不會包含在動作中。

   按一下 **完成** 儲存變更或 **取消** 以取消選取並返回精靈。

   回到精靈中， **引用** 欄將會更新，以反映您選取的要發佈或取消發佈的引用。

   ![pp-05](assets/pp-05.png)

1. 按一下 **發佈** 完成。

   回到網站主控台，系統會傳送通知訊息確認發佈。

1. 如果發佈的頁面與工作流程相關聯，它們可能會顯示在最終版本中 **工作流程** 發佈精靈的步驟。

   >[!NOTE]
   >
   >此 **工作流程** 根據使用者可能擁有也可能沒有的許可權顯示步驟。 請參閱 [此頁面上的上一個附註](/help/sites-authoring/publishing-pages.md#main-pars-note-0-ejsjqg-refd) 關於發佈許可權和 [管理工作流程存取許可權](/help/sites-administering/workflows-managing.md) 和 [將工作流程套用至頁面](/help/sites-authoring/workflows-applying.md#main-pars-text-5-bvhbkh-refd) 以取得詳細資訊。

   資源會依觸發的工作流程分組，每個指定選項用於：

   * 定義工作流程的標題。
   * 保留工作流程封裝，前提是工作流程具有 [多資源支援](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
   * 如果已選擇保留工作流程封裝的選項，則定義工作流程封裝的標題。

   按一 **下「發佈** 」或「 **稍後發佈** 」以完成出版。

   ![chlimage_1-4](assets/chlimage_1-4.png)

## 取消發佈頁面 {#unpublishing-pages}

取消發佈頁面會將其從發佈環境中移除，因此不再開放給您的讀者使用。

在 [發佈方式](/help/sites-authoring/publishing-pages.md#publishing-pages)，可取消發佈一或多個頁面：

* [從頁面編輯器](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [從網站主控台](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### 從編輯器中取消發佈 {#unpublishing-from-the-editor}

編輯頁面時，如果您想取消發佈該頁面，請選取「 」 **取消發佈頁面** 在 **頁面資訊** 功能表，視需要而定 [發佈頁面](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor).

>[!NOTE]
>
>頁面存取者： [別名](/help/sites-authoring/editing-page-properties.md#advanced) 無法取消發佈編輯器中的。 編輯器中的發佈選項僅適用於透過實際路徑存取的頁面。

### 從主控台取消發佈 {#unpublishing-from-the-console}

就像您一樣 [使用「管理出版物」選項進行發佈](/help/sites-authoring/publishing-pages.md#manage-publication)，您也可以用它來取消發佈。

1. 在網站主控台中選取一個或多個頁面，然後按一下 **管理發布** 按鈕。
1. 「管 **理出版物** 」嚮導將啟動。在第一個步驟中， **選項**，選擇「取消發佈」(Unpublish **)，而非「發佈」(Publish)的預設** 選項 ****。

   ![chlimage_1-5](assets/chlimage_1-5.png)

   正如稍後發佈會啟動工作流程，以在指定時間發佈此版本的頁面一樣，稍後停用也會啟動工作流程，以在指定時間取消發佈選取的一或多個頁面。

   如果您想稍後再取消發佈/取消發佈，請前往 [工作流程主控台](/help/sites-administering/workflows.md) 以終止對應的工作流程。

1. 若要完成取消發佈，請按照您想要的方式繼續完成精靈 [發佈頁面](/help/sites-authoring/publishing-pages.md#manage-publication).

## 發佈和取消發佈樹狀結構 {#publishing-and-unpublishing-a-tree}

當您輸入或更新了相當數量的內容頁面時 — 所有這些頁面都位於同一個根頁面下 — 在一個動作中發佈整個樹狀結構會比較容易。

您可以使用 [管理發布](/help/sites-authoring/publishing-pages.md#manage-publication) 選項，執行此操作。

1. 在網站主控台中，選取您要發佈或取消發佈之樹狀結構的根頁面，然後選取 **管理發布**.
1. 「管 **理出版物** 」嚮導將啟動。選擇發佈或取消發佈的時機，然後選取 **下一個** 以繼續。
1. 在 **範圍** 步驟，選取根頁面並選取 **包含子項**.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. 在 **包含子項** 對話方塊，取消核取選項：

   * 僅包含直接子項
   * 僅包含已發佈的頁面

   預設會選取這些選項，因此您必須記得取消選取它們。 按一下 **新增** 以確認並將內容新增至發佈/取消發佈。

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. 此 **管理發布** 精靈會列出樹狀結構的內容以供檢閱。 您可以新增其他頁面或移除選取的頁面，以進一步自訂選取範圍。

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   請記住，您也可以透過以下方式檢閱要發佈的引用： **已發佈引用** 選項。

1. [照常繼續管理發布精靈](#manage-publication) 完成發佈或取消發佈樹狀結構。

## 決定發佈狀態 {#determining-publication-status}

您可以決定頁面的發佈狀態：

* 在 [sites console上的資源概觀資訊](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

  ![screen-shot_2019-03-05at112019](assets/screen-shot_2019-03-05at112019.png)

  發佈狀態會顯示在 [網站主控台](/help/sites-authoring/basic-handling.md#card-view)[的卡片](/help/sites-authoring/basic-handling.md#column-view)、欄和 [清單檢視中](/help/sites-authoring/basic-handling.md#list-view) 。

* 在 [時間表](/help/sites-authoring/basic-handling.md#timeline)

  ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* 在 [頁面資訊功能表](/help/sites-authoring/author-environment-tools.md#page-information) 編輯頁面時

  ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
