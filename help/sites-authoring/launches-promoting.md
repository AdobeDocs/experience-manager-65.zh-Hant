---
title: 促銷啟動
seo-title: 促銷啟動
description: '發佈前，您需要促銷啟動頁面，將內容移回來源（生產）。 '
seo-description: '發佈前，您需要促銷啟動頁面，將內容移回來源（生產）。 '
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# 促銷啟動{#promoting-launches}

發佈前，您需要促銷啟動頁面，將內容移回來源（生產）。 升級啟動頁面時，來源頁面的對應頁面會以升級頁面的內容取代。 升級啟動頁面時可使用下列選項：

* 是僅促銷目前頁面還是整個啟動。
* 是否提升目前頁面的子頁面。
* 是要促銷完整啟動，還是只促銷已變更的頁面。
* 是否在升級後刪除啟動。

>[!NOTE]
>
>將啟動頁面提升至目標(**Production**)後，您可以將 **Production** 頁面當做實體來啟動（以加快程式）。 將頁面新增至工作流程套件，並將它當成啟動頁面套件之工作流程的裝載。 您必須先建立工作流程套件，才能升級啟動。 請參 [閱「使用AEM工作流程處理提升頁面」](#processing-promoted-pages-using-aem-workflow)。

>[!CAUTION]
>
>單一啟動無法同時提升。 這表示同一次啟動時，兩個提升動作會導致錯誤- `Launch could not be promoted` （以及記錄檔中的衝突錯誤）。

>[!CAUTION]
>
>在促銷已修改頁面 *的啟動* 時，會同時考慮來源和啟動分支中的修改。

## 升級啟動頁面 {#promoting-launch-pages}

>[!NOTE]
>
>這包括在只有一個啟動層級時，促銷啟動頁面的手動動作。 請參閱：
>
>* [在結構中有多個啟動時](#promoting-a-nested-launch) ，提升巢狀啟動。
>* [啟動——事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events) ，以取得有關自動促銷和發佈的詳細資訊。
>



您可以從Sites控制台或 **Launches** 控制台 **促銷啟動** :

1. 開啟:

   * Sites控 **制台** :

      1. 開啟 [參照邊欄](/help/sites-authoring/author-environment-tools.md#showingpagereferences) ，然後使用選擇模式選 [擇所需的源頁](/help/sites-authoring/basic-handling.md) （或者選擇並開啟參照邊欄，順序不重要）。 將顯示所有引用。

      1. 選 **擇啟動** (例如啟動(1))以顯示特定啟動的清單。
      1. 選取特定的啟動以顯示可用的動作。
      1. 選擇 **提升啟動** ，以開啟精靈。
   * 啟動 **控制台** :

      1. 選取您的啟動（點選／按一下縮圖）。
      1. 選擇 **升級**。


1. 在第一個步驟中，您可以指定：

   * **目標**

      * **刪除促銷活動後啟動**
   * **範圍**

      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級目前頁面**
      * **升級目前頁面與子頁面**
   例如，當選擇僅提升修改的頁時：

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >如果您有巢狀啟動，此功能涵蓋單次啟動，請參閱「 [提升巢狀啟動」](#promoting-a-nested-launch)。

1. 選擇 **下一步** ，繼續。
1. 您可以檢閱要升級的頁面，這些會視您選擇的頁面範圍而定：

   ![chlimage_1-102](assets/chlimage_1-102.png)

1. 選擇 **升級**。

## 在編輯時提升啟動頁面 {#promoting-launch-pages-when-editing}

當您編輯啟動頁面時，「頁面資 **訊」中也提供** 「升級啟動 **」動作**。 這將開啟嚮導以收集所需資訊。

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>這適用於單次和巢狀 [啟動](#promoting-a-nested-launch)。

## 提升巢狀啟動 {#promoting-a-nested-launch}

建立巢狀啟動後，您可將它升級回任何來源，包括根來源（生產）。

![chlimage_1-104](assets/chlimage_1-104.png)

1. 與「建 [立巢狀啟動」一樣](#creatinganestedlaunchlaunchwithinalaunch)，請導覽至「啟動」控制台或「參考」邊欄，並選取所需的啟 **動****** 。
1. 選擇 **提升啟動** ，以開啟精靈。

1. 輸入所需的詳細資訊：

   * **目標**

      * **促銷目**&#x200B;標您可以促銷至任何來源。

      * **促銷後刪除啟動**&#x200B;促銷後，所選的啟動以及其中巢狀的任何啟動都會刪除。
   * **範圍**&#x200B;您可在此處選擇是升級整個啟動，還是僅升級實際已編輯的頁面。 如果是後者，則可以選擇包含／排除子頁面。 預設配置是僅提升當前頁面的頁面更改：

      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級目前頁面**
      * **升級目前頁面與子頁面**
   ![chlimage_1-105](assets/chlimage_1-105.png)

1. 選擇 **下一步**。
1. 在選擇「升級」之前，請先查看升級詳 **細資訊**:

   ![chlimage_1-106](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >列出的頁面將取決於已定 **義的範圍** ，可能取決於實際已編輯的頁面。

1. 您的變更將會在啟動主控台中提 **升** ，並反映：

   ![chlimage_1-107](assets/chlimage_1-107.png)

## 使用AEM工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型，對提升的啟動頁面執行大量處理：

1. 建立工作流程套件。
1. 當作者促銷「啟動」頁面時，會將其儲存在工作流程套件中。
1. 使用套件作為裝載，啟動工作流程模型。

要在升級頁面時自動啟動工作流，請 [為包節點配置工作流啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers) 。

例如，當作者促銷「啟動」頁面時，您可以自動產生頁面啟動請求。 設定工作流程啟動程式，以在修改封裝節點時啟動「請求啟動」工作流程。

![chlimage_1-108](assets/chlimage_1-108.png)
