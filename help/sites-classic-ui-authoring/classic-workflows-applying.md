---
title: 將工作流程套用至頁面
seo-title: 將工作流程套用至頁面
description: 工作流程可從網站主控台或在編輯頁面時，從Sidekick開始。
seo-description: 工作流程可從網站主控台或在編輯頁面時，從Sidekick開始。
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 將工作流程套用至頁面{#applying-workflows-to-pages}

應用工作流時，您指定以下資訊：

* 要套用的工作流程。

   您可以套用您有權存取的任何工作流程（由AEM管理員指派）。
* （可選）:

   * 提供您啟動工作流程原因的註解。
   * 幫助識別用戶收件箱中工作流實例的標題。

>[!NOTE]
>
>AEM管理員可使用數種其他方 [法來啟動工作流程](/help/sites-administering/workflows-starting.md)。

## 套用工作流程 {#applying-workflows}

工作流程可從網站主控台或在編輯頁面時，從Sidekick開始。

「網 **站控制台** 」中的「狀態」欄 **** 會指出工作流程是否已套用至頁面：

![工作流狀態](assets/workflowstatus.png)

### 從網站主控台啟動工作流程 {#starting-a-workflow-from-the-websites-console}

1. 開啟網站主控台。 ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. 在「網站」樹狀結構中，選取您要套用工作流程之頁面的父項。
1. 在頁面清單中，選取頁面，然後按一下「工作流程」。
1. 在「啟動工作流」對話框中，選擇要應用的工作流。 可選地，輸入注釋和標題。 然後，按一下「開始」。

### 使用Sidekick啟動工作流 {#starting-a-workflow-using-sidekick}

1. 開啟網站主控台。
1. 開啟必要的頁面。
1. 從Sidekick中選取「工作流程」標籤。
1. 展開「工 **作流** 」對話框，允許您選擇「工作流 **」，並可選擇輸入「工作流** 標題 **」和「******&#x200B;注釋」。

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. 按一 **下「啟動工作流程** 」，以啟動新的工作流程例項，其中包含您所設定的屬性和目前頁面作為裝載。 現在工作流程正在執行。

