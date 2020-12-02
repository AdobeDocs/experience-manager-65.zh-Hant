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
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 11%

---


# 將工作流程套用至頁面{#applying-workflows-to-pages}

應用工作流時，您指定以下資訊：

* 要套用的工作流程。

   您可以套用您有權存取的任何工作流程 (由AEM管理員指派)。
* （可選）:

   * 提供您啟動工作流程原因的註解。
   * 幫助識別用戶收件箱中工作流實例的標題。

>[!NOTE]
>
>AEM管理員可使用[數種其他方法](/help/sites-administering/workflows-starting.md)來啟動工作流程。

## 套用工作流程{#applying-workflows}

工作流程可從網站主控台或在編輯頁面時，從Sidekick開始。

**Websites**&#x200B;控制台中的&#x200B;**Status**&#x200B;欄會指出工作流程是否已套用至頁面：

![工作流狀態](assets/workflowstatus.png)

### 從網站主控台{#starting-a-workflow-from-the-websites-console}啟動工作流程

1. 開啟網站主控台。 ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. 在「網站」樹狀結構中，選取您要套用工作流程之頁面的父項。
1. 在頁面清單中，選取頁面，然後按一下「工作流程」。
1. 在「啟動工作流」對話框中，選擇要應用的工作流。 可選地，輸入注釋和標題。 然後，按一下「開始」。

### 使用Sidekick {#starting-a-workflow-using-sidekick}啟動工作流

1. 開啟網站主控台。
1. 開啟必要的頁面。
1. 從Sidekick中選取「工作流程」標籤。
1. 展開「**Workflow**」對話框，允許您選擇「**Workflow**」，並可選擇輸入「Workflow Title **」和「Comment**」。****

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. 按一下&#x200B;**啟動工作流**&#x200B;以啟動新的工作流實例，其中包含您配置的屬性和當前頁作為裝載。 現在工作流程正在執行。

