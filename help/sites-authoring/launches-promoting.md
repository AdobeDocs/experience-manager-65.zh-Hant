---
title: 提升啟動
description: 您可以提升啟動頁面，以在發佈前將內容移回來源（生產環境）。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# 提升啟動{#promoting-launches}

您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。 提升啟動頁面時，來源頁面的對應頁面會取代為提升頁面的內容。 提升啟動頁面時，可使用下列選項：

* 僅提升目前頁面還是整個啟動。
* 是否要升級目前頁面的子頁面。
* 是要升級完整啟動項，還是隻升級已變更的頁面。
* 升級後是否要刪除啟動。

>[!NOTE]
>
>將啟動頁面提升至目標之後(**生產**)，您可以啟動 **生產** 以實體形式顯示頁面（以加快處理速度）。 將頁面新增至Workflow封裝，並作為啟動頁面封裝的Workflow的裝載。 提升啟動項之前，必須先建立工作流程封裝。 另請參閱 [使用AEM工作流程處理提升頁面](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>無法同時提升單一啟動。 這表示在同一個啟動上同時執行兩個提升動作可能會導致錯誤 —  `Launch could not be promoted` （以及記錄檔中的衝突錯誤）。

>[!CAUTION]
>
>提升啟動時 *已修改* 頁面，來源和啟動分支中的修改都會被考慮。

## 提升啟動頁面 {#promoting-launch-pages}

>[!NOTE]
>
>當只有一個啟動層級時，這會涵蓋提升啟動頁面的手動動作。 請參閱：
>
>* [提升巢狀啟動](#promoting-a-nested-launch) 當結構中有多個啟動項時。
>* [啟動 — 事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events) 以取得有關自動促銷和發佈的進一步詳細資訊。
>

您可以透過以下任一專案提升啟動： **網站** 主控台或 **啟動** 主控台：

1. 開啟：

   * 此 **網站** 主控台：

      1. 開啟 [引用邊欄](/help/sites-authoring/author-environment-tools.md#showingpagereferences) 並使用以下方式選取所需的來源頁面 [選擇模式](/help/sites-authoring/basic-handling.md) （或是選取並開啟參照邊欄，順序並不重要）。 所有參照都會顯示。

      1. 選取 **啟動** (例如，「啟動」(1))會顯示特定啟動的清單。
      1. 選取特定啟動項以顯示可用的動作。
      1. 選取 **提升啟動** 以開啟精靈。

   * 此 **啟動** 主控台：

      1. 選取您的啟動項（按一下縮圖）。
      1. 選取 **提升**.

1. 在第一個步驟中，您可以指定：

   * **Target**

      * **促銷活動後刪除啟動**

   * **範圍**

      * **提升完整啟動項**
      * **提升已修改的頁面**
      * **提升目前頁面**
      * **提升目前頁面和子頁面**

   例如，當選取僅提升已修改的頁面時：

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >這涵蓋單一啟動（如果您有巢狀啟動），請參閱 [提升巢狀啟動](#promoting-a-nested-launch).

1. 選取 **下一個** 以繼續進行。
1. 您可以檢閱要提升的頁面，頁面視您選擇的頁面範圍而定：

   ![檢閱要提升的頁面](assets/chlimage_1-102.png)

1. 選取 **提升**.

## 編輯時提升啟動頁面 {#promoting-launch-pages-when-editing}

編輯啟動頁面時， **提升啟動** 動作也可從取得 **頁面資訊**. 這會開啟精靈以收集所需的資訊。

![提升啟動](assets/chlimage_1-103.png)

>[!NOTE]
>
>這適用於單一和 [巢狀啟動](#promoting-a-nested-launch).

## 提升巢狀啟動 {#promoting-a-nested-launch}

建立巢狀啟動後，您可以將其升級回任何來源，包括根來源（生產）。

![提升巢狀啟動項的概觀](assets/chlimage_1-104.png)

1. 如同 [建立巢狀啟動](#creatinganestedlaunchlaunchwithinalaunch)，導覽至並選取以下任一專案所需的啟動： **啟動** 主控台或 **引用** 邊欄。
1. 選取 **提升啟動** 以開啟精靈。

1. 輸入必要的明細：

   * **Target**

      * **促銷活動目標**
您可以升級至任何來源。

      * **促銷活動後刪除啟動**
提升後，選取的啟動項以及巢狀內嵌的所有啟動項都會被刪除。

   * **範圍**
您可以在此處選擇是提升整個啟動，還是僅提升已實際編輯的頁面。 如果是後者，您就可以選取包含/排除子頁面。 預設設定為僅提升目前頁面的頁面變更：

      * **提升完整啟動項**
      * **提升已修改的頁面**
      * **提升目前頁面**
      * **提升目前頁面和子頁面**

   ![提升啟動的設定](assets/chlimage_1-105.png)

1. 選取 **下一個**.
1. 請先檢閱促銷詳細資訊，再選取 **提升**：

   ![檢閱詳細資訊和提升](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >列出的頁面取決於 **範圍** 已定義，且可能還包括實際編輯的頁面。

1. 您的變更將會提升並反映在 **啟動** 主控台：

   ![啟動主控台](assets/chlimage_1-107.png)

## 使用 AEM 工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型來對提升的「啟動」頁面執行大量處理：

1. 建立Workflow封裝。
1. 作者提升Launch頁面時，會將頁面儲存在Workflow套件中。
1. 使用封裝作為裝載啟動工作流程模型。

若要在提升頁面時自動啟動工作流程， [設定工作流程啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers) （針對封裝節點）。

例如，您可以在作者提升啟動頁面時自動產生頁面啟用請求。 設定工作流程啟動器，以便在修改封裝節點時啟動「請求啟用」工作流程。

![工作流程啟動器](assets/chlimage_1-108.png)
