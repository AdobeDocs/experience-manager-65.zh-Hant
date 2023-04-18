---
title: 將工作流程套用至頁面
description: 工作流程可從網站主控台啟動，或在編輯頁面時從Sidekick啟動。
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
exl-id: d8b604c5-a6da-47c4-9422-b519e224c7ca
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 11%

---

# 將工作流程套用至頁面{#applying-workflows-to-pages}

套用工作流程時，需指定下列資訊：

* 要套用的工作流程。

   您可以套用您有權存取的任何工作流程 (由AEM管理員指派)。
* （可選）:

   * 提供啟動工作流程原因的資訊的備注。
   * 可協助識別使用者收件匣中工作流程例項的標題。

>[!NOTE]
>
>AEM管理員可使用 [其他幾種方法](/help/sites-administering/workflows-starting.md).

## 套用工作流程 {#applying-workflows}

工作流程可從網站主控台啟動，或在編輯頁面時從Sidekick啟動。

此 **狀態** 欄中 **網站** console指示工作流是否已應用到頁面：

![工作流程狀態](assets/workflowstatus.png)

### 從網站主控台啟動工作流程 {#starting-a-workflow-from-the-websites-console}

1. 開啟網站主控台。 ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. 在「網站」樹中，選擇要應用工作流的頁面的父級。
1. 在頁面清單中，選取頁面，然後按一下「工作流程」。
1. 在「開始工作流」對話框中，選擇要應用的工作流。 或者，輸入注釋和標題。 然後，按一下「開始」。

### 使用Sidekick啟動工作流程 {#starting-a-workflow-using-sidekick}

1. 開啟網站主控台。
1. 開啟必要的頁面。
1. 從Sidekick中選取Workflow索引標籤。
1. 展開 **工作流程** 對話框，允許您選擇 **工作流程** （可選）輸入 **工作流程標題** 和 **註解**.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. 按一下 **開始工作流程** 以您設定的屬性和目前的頁面作為裝載，來啟動新的工作流程例項。 現在工作流程正在執行。
