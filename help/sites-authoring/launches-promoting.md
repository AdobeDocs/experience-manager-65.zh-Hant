---
title: 升級啟動
description: 在發佈之前，您可以升級啟動頁面，將內容移回源（生產）。
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 7%

---

# 提升 Launch{#promoting-launches}

在發佈之前，您需要升級啟動頁面，以將內容移回源（生產）。 當啟動頁面被升級時，源頁面的相應頁面被升級頁面的內容替換。 升級啟動頁時可使用以下選項：

* 是僅升級當前頁面還是整個啟動。
* 是否提升當前頁的子頁。
* 是升級完整啟動，還是僅升級已更改的頁面。
* 是否在升級後刪除啟動。

>[!NOTE]
>
>將啟動頁提升到目標(**生產**)，您可以激活 **生產** 頁面作為實體（以加快流程）。 將頁面添加到工作流包，並將其用作激活頁麵包的工作流的負載。 在升級啟動之前，需要建立工作流包。 請參閱 [使用工作流處理已升級AEM頁](#processing-promoted-pages-using-aem-workflow)。

>[!CAUTION]
>
>不能同時升級單個啟動。 這意味著在同一次啟動上同時執行兩個升級操作可能導致錯誤 —  `Launch could not be promoted` （以及日誌中的衝突錯誤）。

>[!CAUTION]
>
>在為 *修改* 頁面，將考慮源分支和啟動分支中的修改。

## 升級啟動頁 {#promoting-launch-pages}

>[!NOTE]
>
>這包括在只有一個發射級別時升級發射頁面的手動操作。 請參閱：
>
>* [升級嵌套啟動](#promoting-a-nested-launch) 當結構中有多個發射時。
>* [啟動 — 事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events) 的子菜單。
>


您可以從以下任一 **站點** 控制台或 **啟動** 控制台：

1. 開啟:

   * 這樣 **站點** 控制台：

      1. 開啟 [參考軌](/help/sites-authoring/author-environment-tools.md#showingpagereferences) 並使用 [選擇模式](/help/sites-authoring/basic-handling.md) （或選擇並開啟參照滑軌，訂單不重要）。 將顯示所有引用。

      1. 選擇 **啟動** (例如，啟動(1))，以顯示特定啟動的清單。
      1. 選擇特定啟動以顯示可用操作。
      1. 選擇 **促進啟動** 的子菜單。
   * 這樣 **啟動** 控制台：

      1. 選擇啟動（點擊/按一下縮略圖）。
      1. 選擇 **提升**。


1. 在第一步中，您可以指定：

   * **目標**

      * **刪除促銷活動後啟動**
   * **範圍**

      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級目前頁面**
      * **升級目前頁面與子頁面**

   例如，當選擇僅升級修改的頁面時：

   ![pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >這包括單次啟動，如果已嵌套啟動，請參閱 [升級嵌套啟動](#promoting-a-nested-launch)。

1. 選擇 **下一個** 繼續。
1. 您可以複查要升級的頁面，這些頁面將取決於您選擇的頁面範圍：

   ![chlimage_1-102](assets/chlimage_1-102.png)

1. 選擇 **提升**。

## 編輯時升級啟動頁面 {#promoting-launch-pages-when-editing}

編輯啟動頁面時， **升級啟動** 操作也可從 **頁面資訊**。 這將開啟嚮導以收集所需資訊。

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>這適用於單個和 [嵌套啟動](#promoting-a-nested-launch)。

## 升級嵌套啟動 {#promoting-a-nested-launch}

建立嵌套啟動後，您可以將其升級回任何源，包括根源（生產）。

![chlimage_1-104](assets/chlimage_1-104.png)

1. 與 [建立嵌套啟動](#creatinganestedlaunchlaunchwithinalaunch)，導航到並選擇 **啟動** 控制台或 **引用** 鐵軌。
1. 選擇 **促進啟動** 的子菜單。

1. 輸入所需的詳細資訊：

   * **目標**

      * **升級目標**
您可以升級到任何源。

      * **升級後刪除啟動**
升級後，將刪除選定的啟動以及嵌套在其中的任何啟動。
   * **範圍**
在此，您可以選擇是升級整個啟動，還是僅升級實際已編輯的頁面。 如果是後者，則可以選擇包括/排除子頁。 預設配置是僅升級當前頁面的頁面更改：

      * **提升完整啟動項**
      * **提升已修改頁面**
      * **升級目前頁面**
      * **升級目前頁面與子頁面**

   ![chlimage_1-105](assets/chlimage_1-105.png)

1. 選擇 **下一個**。
1. 在選擇之前查看升級詳細資訊 **提升**:

   ![chlimage_1-106](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >列出的頁面將取決於 **範圍** 已定義，可能是已實際編輯的頁面。

1. 您的更改將在 **啟動** 控制台：

   ![chlimage_1-107](assets/chlimage_1-107.png)

## 使用 AEM 工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流模型對已升級的「啟動」頁執行批量處理：

1. 建立工作流包。
1. 當作者升級「啟動」頁面時，他們會將其儲存在工作流包中。
1. 使用包作為負載啟動工作流模型。

要在升級頁面時自動啟動工作流， [配置工作流啟動程式](/help/sites-administering/workflows-starting.md#workflows-launchers) 的子菜單。

例如，當作者提升「啟動」頁面時，可以自動生成頁面激活請求。 配置工作流啟動程式以在修改包節點時啟動請求激活工作流。

![chlimage_1-108](assets/chlimage_1-108.png)
