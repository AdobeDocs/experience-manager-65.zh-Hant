---
title: 編輯啟動
description: 為某個頁面（或一組頁面）建立啟動後，您可以在頁面的啟動副本中編輯內容。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 編輯啟動{#editing-launches}

## 編輯啟動頁面 {#editing-launch-pages}

為某個頁面（或一組頁面）建立啟動後，您可以在頁面的啟動副本中編輯內容。

1. 開啟頁面以進行編輯。
1. 在Sidekick中，選取 **版本設定** 標籤，然後展開 **啟動** 群組。 目前正在編輯的啟動項標題會使用粗體字型。

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 選取您要處理的啟動，然後按一下 **切換**.
1. 開始編輯。

   >[!NOTE]
   >
   >您可以使用 **頁面** sidekick的標籤以執行動作，例如 **建立子頁面**，以及其他專案。

## 編輯啟動設定 {#editing-a-launch-configuration}

建立啟動後，您可以變更啟動名稱和啟動日期。 您也可以指定要與啟動建立關聯的影像。

1. 開啟啟動管理頁面([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html))。

1. 選取所需的啟動項，然後按一下 **編輯** 若要開啟對話方塊：

   * 在 **一般** 標籤，您可以編輯：

      * **標題**
      * **上線日期**：這等同於啟動日期
      * **生產就緒**

     另請參閱 [啟動 — 事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events) 這些欄位的用途和互動相關資訊。

   * 在 **影像** 標籤，您可以上傳影像檔案。

1. 按一下「**儲存**」。

## 探索頁面的啟動狀態 {#discovering-the-launch-status-of-a-page}

當您編輯頁面的啟動時，啟動的相關資訊會顯示在 **版本設定** Sidekick的索引標籤：

* 啟動項的名稱。
* 上次變更後的時間。
* 執行上次變更的使用者。
* 的狀態 **生產就緒** 標幟（橘色=未設定；綠色=設定）。

![chlimage_1-186](assets/chlimage_1-186.png)
