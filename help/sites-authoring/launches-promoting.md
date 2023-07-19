---
title: 提升啟動
description: 您可以提升啟動頁面，在發佈之前將內容移回來源（生產環境）。
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 6%

---

# 提升啟動{#promoting-launches}

您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。 提升啟動頁面時，來源頁面的對應頁面會取代為提升頁面的內容。 提升啟動頁面時，有以下選項可供使用：

* 僅提升目前頁面還是整個啟動。
* 是否要升級目前頁面的子頁面。
* 是提升完整啟動項，還是僅提升已變更的頁面。
* 升級後是否要刪除啟動。

>[!NOTE]
>
>將啟動頁面升級至目標之後(**生產**)，則您可啟動 **生產** 以圖元形式顯示頁面（以加快處理速度）。 將頁面新增至Workflow封裝，並當做啟動頁面封裝的Workflow的裝載。 在提升啟動項之前，您需要建立工作流程套件。 另請參閱 [使用AEM工作流程處理提升頁面](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>無法同時提升單一啟動。 這表示對同一個啟動項同時執行兩個提升動作可能會導致錯誤 —  `Launch could not be promoted` （連同記錄檔中的衝突錯誤）。

>[!CAUTION]
>
>提升啟動時 *已修改* 頁面，會同時考慮來源分支和啟動分支中的修改。

## 提升啟動頁面 {#promoting-launch-pages}

>[!NOTE]
>
>當只有一個啟動層級時，這會涵蓋提升啟動頁面的手動動作。 請參閱：
>
>* [提升巢狀啟動](#promoting-a-nested-launch) 當結構中有多個啟動項時。
>* [啟動 — 事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events) 以取得有關自動促銷和發佈的更多詳細資訊。
>

您可以透過以下任一項提升啟動： **網站** 主控台或 **啟動** 主控台：

1. 開啟:

   * 此 **網站** 主控台：

      1. 開啟 [參考邊欄](/help/sites-authoring/author-environment-tools.md#showingpagereferences) 並使用以下方式選取所需的來源頁面 [選擇模式](/help/sites-authoring/basic-handling.md) （或是選取並開啟參照邊欄，順序並不重要）。 將顯示所有參考。

      1. 選取 **啟動** (例如，「啟動」(1))會顯示特定啟動的清單。
      1. 選取特定啟動項以顯示可用的動作。
      1. 選取 **提升啟動** 以開啟精靈。

   * 此 **啟動** 主控台：

      1. 選取您的啟動項（點選/按一下縮圖）。
      1. 選取 **提升**.

1. 在第一個步驟中，您可以指定：

   * **目標**

      * **刪除促銷活動後啟動**

   * **範圍**

      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級目前頁面**
      * **升級目前頁面與子頁面**

   例如，當選取僅提升已修改的頁面時：

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >這涵蓋單一啟動（如果您有巢狀啟動），請參閱 [提升巢狀啟動](#promoting-a-nested-launch).

1. 選取 **下一個** 以繼續進行。
1. 您可以檢閱要提升的頁面，這些頁面取決於您選擇的頁面範圍：

   ![檢閱要提升的頁面](assets/chlimage_1-102.png)

1. 選取 **提升**.

## 編輯時提升啟動頁面 {#promoting-launch-pages-when-editing}

編輯啟動頁面時， **提升啟動** 動作也可從 **頁面資訊**. 這會開啟精靈，以收集所需的資訊。

![提升啟動](assets/chlimage_1-103.png)

>[!NOTE]
>
>這適用於單一和 [巢狀啟動](#promoting-a-nested-launch).

## 提升巢狀啟動 {#promoting-a-nested-launch}

建立巢狀啟動後，您可以將其升級回任何來源，包括根來源（生產）。

![提升巢狀啟動概述](assets/chlimage_1-104.png)

1. 與 [建立巢狀啟動](#creatinganestedlaunchlaunchwithinalaunch)，導覽至並選取「 」中所需的啟動。 **啟動** 主控台或 **引用** 邊欄。
1. 選取 **提升啟動** 以開啟精靈。

1. 輸入必要的明細：

   * **目標**

      * **促銷目標**
您可以升級至任何來源。

      * **促銷活動後刪除啟動**
提升後，選取的啟動項以及巢狀內嵌的任何啟動項都會被刪除。

   * **範圍**
您可以在此處選擇是提升整個啟動，還是僅提升已實際編輯的頁面。 如果是後者，您就可以選取包含/排除子頁面。 預設設定為僅提升目前頁面的頁面變更：

      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級目前頁面**
      * **升級目前頁面與子頁面**

   ![提升啟動的設定](assets/chlimage_1-105.png)

1. 選取 **下一個**.
1. 請先檢閱促銷詳細資訊，再選取 **提升**：

   ![檢閱詳細資訊和提升](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >列出的頁面取決於 **範圍** 已定義，且可能包括實際編輯的頁面。

1. 您的變更將會提升並反映在 **啟動** 主控台：

   ![啟動主控台](assets/chlimage_1-107.png)

## 使用 AEM 工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型來大量處理提升的「啟動」頁面：

1. 建立工作流程封裝。
1. 作者提升Launch頁面時，會將頁面儲存在Workflow套件中。
1. 使用封裝作為裝載啟動工作流程模型。

若要在提升頁面時自動啟動工作流程， [設定工作流程啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers) （針對套件節點）。

例如，您可以在作者提升啟動頁面時自動產生頁面啟用請求。 設定工作流程啟動器，以便在修改封裝節點時啟動「請求啟用」工作流程。

![工作流程啟動器](assets/chlimage_1-108.png)
