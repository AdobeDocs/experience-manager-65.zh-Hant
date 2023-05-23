---
title: 編輯 Launch
description: 為頁面（或一組頁面）建立啟動後，可以在頁面的啟動副本中編輯內容。
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 3%

---

# 編輯 Launch{#editing-launches}

## 編輯啟動頁 {#editing-launch-pages}

為頁面（或一組頁面）建立啟動後，可以在頁面的啟動副本中編輯內容。

1. 開啟頁面進行編輯。
1. 在Sidekick中，選擇 **版本控制** ，然後展開 **啟動** 組。 當前正在編輯的啟動的標題使用粗體。

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 選擇要處理的啟動，然後按一下 **交換機**。
1. 開始編輯。

   >[!NOTE]
   >
   >您可以使用 **頁面** 執行操作(如 **「建立子頁」**&#x200B;其中包括：

## 編輯啟動配置 {#editing-a-launch-configuration}

建立啟動後，您可以更改啟動名稱和啟動日期。 還可以指定要與啟動關聯的映像。

1. 開啟啟動管理頁([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html))。

1. 選擇所需的啟動，然後按一下 **編輯** 開啟對話框：

   * 在 **常規** 頁籤：

      * **標題**
      * **即時日期**:這等於啟動日期
      * **生產就緒**

      請參閱 [啟動 — 事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events) 有關這些欄位的用途和交互的資訊。

   * 在 **影像** 頁籤，您可以上載影像檔案。


1. 按一下「**儲存**」。

## 發現頁面的啟動狀態 {#discovering-the-launch-status-of-a-page}

編輯頁面啟動時，有關啟動的資訊將顯示在 **版本控制** 頁籤：

* 發射的名稱。
* 上次更改後的時間。
* 執行上次更改的用戶。
* 的狀態 **生產就緒** 標誌（橙色=未設定）綠色=設定)。

![chlimage_1-186](assets/chlimage_1-186.png)
