---
title: 提升啟動
seo-title: 提升啟動
description: '發佈前，您必須促銷啟動頁面，才能將內容移回來源（生產）。 '
seo-description: '發佈前，您必須促銷啟動頁面，才能將內容移回來源（生產）。 '
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 6%

---

# 提升啟動{#promoting-launches}

發佈前，您必須促銷啟動頁面，才能將內容移回來源（生產）。 啟動頁面升級時，來源頁面的對應頁面會取代為升級頁面的內容。 提升啟動頁面時，可使用下列選項：

* 僅促銷目前頁面還是整個啟動。
* 是否促銷目前頁面的子頁面。
* 是要促銷完整啟動，還是只促銷已變更的頁面。
* 升級後是否刪除啟動。

>[!NOTE]
>
>將啟動頁面提升至目標(**Production**)之後，您可以以實體形式啟動&#x200B;**Production**&#x200B;頁面（以加快處理速度）。 將頁面新增至工作流程套件，並將其用作啟用頁面套件之工作流程的裝載。 您必須先建立工作流程套件，才能提升啟動。 請參閱使用AEM Workflow](#processing-promoted-pages-using-aem-workflow)處理提升頁面。[

>[!CAUTION]
>
>無法同時促銷單一啟動。 這表示同一次啟動時，兩個提升動作可能會導致錯誤 — `Launch could not be promoted`（連同記錄中的衝突錯誤）。

>[!CAUTION]
>
>促銷&#x200B;*已修改*&#x200B;頁面的啟動時，會考量來源和啟動分支中的修改。

## 提升啟動頁面{#promoting-launch-pages}

>[!NOTE]
>
>這涵蓋只有一個啟動層級時，提升啟動頁面的手動動作。 請參閱：
>
>* [當結構中](#promoting-a-nested-launch) 有多個啟動時，提升巢狀啟動。
>* [啟動 — 事件順序，以](/help/sites-authoring/launches.md#launches-the-order-of-events) 取得關於自動促銷和發佈的詳細資訊。

>



您可以從&#x200B;**Sites**&#x200B;主控台或&#x200B;**Launches**&#x200B;主控台促銷啟動：

1. 開啟:

   * **Sites**&#x200B;控制台：

      1. 開啟[參考邊欄](/help/sites-authoring/author-environment-tools.md#showingpagereferences)，並使用[選取模式](/help/sites-authoring/basic-handling.md)選取所需的來源頁面（或選取並開啟參考邊欄，順序不重要）。 將顯示所有引用。

      1. 選取&#x200B;**啟動**(例如啟動(1))以顯示特定啟動的清單。
      1. 選取特定啟動以顯示可用的動作。
      1. 選擇&#x200B;**Promote launch**&#x200B;以開啟嚮導。
   * **啟動**&#x200B;控制台：

      1. 選取您的啟動（點選/按一下縮圖）。
      1. 選擇&#x200B;**Promote**。


1. 在第一個步驟中，您可以指定：

   * **目標**

      * **刪除促銷活動後啟動**
   * **範圍**

      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級目前頁面**
      * **升級目前頁面與子頁面**

   例如，選取「僅促銷修改的頁面」時：

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >如果您有巢狀啟動，則涵蓋單次啟動，請參閱[提升巢狀啟動](#promoting-a-nested-launch)。

1. 選擇&#x200B;**Next**&#x200B;以繼續。
1. 您可以檢閱要升級的頁面，這些將取決於您選取的頁面範圍：

   ![chlimage_1-102](assets/chlimage_1-102.png)

1. 選擇&#x200B;**Promote**。

## 編輯{#promoting-launch-pages-when-editing}時提升啟動頁面

編輯啟動頁面時，也可從&#x200B;**頁面資訊**&#x200B;使用&#x200B;**促銷啟動**&#x200B;動作。 這會開啟精靈以收集所需資訊。

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>這適用於單次和[巢狀啟動](#promoting-a-nested-launch)。

## 提升巢狀啟動{#promoting-a-nested-launch}

建立巢狀啟動後，您可將其升級回任何來源，包括根來源（生產）。

![chlimage_1-104](assets/chlimage_1-104.png)

1. 與[建立巢狀啟動](#creatinganestedlaunchlaunchwithinalaunch)一樣，在&#x200B;**啟動**&#x200B;主控台或&#x200B;**參考**&#x200B;邊欄中導覽至並選取所需的啟動。
1. 選擇&#x200B;**Promote launch**&#x200B;以開啟嚮導。

1. 輸入所需詳細資訊：

   * **目標**

      * **促銷**
目標您可以促銷至任何來源。

      * **促銷後刪除啟**
動促銷後，會刪除所選啟動及其內嵌的任何啟動。
   * ****
範圍您可以在此選取是否促銷整個啟動，或僅促銷實際已編輯的頁面。若是後者，您可以選取「包含/排除」子頁面。 預設設定為僅提升目前頁面的頁面變更：

      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級目前頁面**
      * **升級目前頁面與子頁面**

   ![chlimage_1-105](assets/chlimage_1-105.png)

1. 選擇&#x200B;**Next**。
1. 在選擇&#x200B;**Promote**&#x200B;之前，請查看升級詳細資訊：

   ![chlimage_1-105](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >列出的頁面取決於所定義的&#x200B;**範圍**，可能取決於實際已編輯的頁面。

1. 您的變更將會升級並反映在&#x200B;**Launches**&#x200B;主控台中：

   ![chlimage_1-107](assets/chlimage_1-107.png)

## 使用AEM工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型來執行大量處理提升的啟動頁面：

1. 建立工作流程套件。
1. 作者促銷Launch頁面時，會將其儲存在工作流程套件中。
1. 以套件作為裝載，啟動工作流程模型。

要在頁面升級時自動啟動工作流，請為包節點配置工作流啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers)。[

例如，當作者促銷啟動頁面時，您可以自動產生頁面啟動請求。 設定工作流程啟動器，以在修改套件節點時啟動「請求啟動」工作流程。

![chlimage_1-108](assets/chlimage_1-108.png)
