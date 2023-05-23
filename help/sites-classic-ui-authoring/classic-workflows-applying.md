---
title: 將工作流程套用至頁面
description: 可以從網站控制台或編輯頁面時從Sidekick啟動工作流。
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

應用工作流時，可指定以下資訊：

* 要套用的工作流程。

   您可以套用您有權存取的任何工作流程 (由AEM管理員指派)。
* （可選）:

   * 提供有關啟動工作流原因的資訊的注釋。
   * 幫助標識用戶收件箱中工作流實例的標題。

>[!NOTE]
>
>AEM管理員使用 [其它幾種方法](/help/sites-administering/workflows-starting.md)。

## 應用工作流 {#applying-workflows}

可以從網站控制台或編輯頁面時從Sidekick啟動工作流。

的 **狀態** 列 **網站** console指示工作流是否已應用於頁面：

![工作流狀態](assets/workflowstatus.png)

### 從網站控制台啟動工作流 {#starting-a-workflow-from-the-websites-console}

1. 開啟網站控制台。 ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. 在「網站」樹中，選擇要應用工作流的頁面的父級。
1. 在頁面清單中，選擇頁面，然後按一下「工作流」。
1. 在「啟動工作流」對話框中，選擇要應用的工作流。 可選，輸入注釋和標題。 然後，按一下「Start（開始）」。

### 使用Sidekick啟動工作流 {#starting-a-workflow-using-sidekick}

1. 開啟網站控制台。
1. 開啟所需頁面。
1. 從Sidekick中選擇Workflow頁籤。
1. 展開 **工作流** 對話框，允許您選擇 **工作流** （可選）輸入 **工作流標題** 和 **注釋**。

   ![工作流啟動項](assets/workflowstartsidekick.png)

1. 按一下 **啟動工作流** 以配置的屬性和當前頁作為負載啟動新的工作流實例。 現在工作流正在運行。
